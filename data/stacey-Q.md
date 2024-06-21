# L-1 The `Project` structure field is not used 

## Description

To initialize a new project inside the `initProject(InitProjectParams calldata params)` function calls the internal function `_cacheProject (...)`. It sets the fields of the `Project` structure. [Link to code](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/ILOManager.sol#L124-L147)

But the field `uint16 investorShares` is not set in this function. [Link to code](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/interfaces/IILOManager.sol#L27)

Also, this field is not used anywhere else in the code. Even if the field itself is not directly exploitable, its existence could lead to confusion about the protocol's state, potentially allowing for more subtle attacks. Every piece of code that is not used adds unnecessary complexity to the project. It increases the size of the codebase, making it harder to maintain and understand. Over time, this can lead to bugs being introduced more easily, especially if changes are made elsewhere in the code that inadvertently affect the unused field.

## Recommended Mitigation Steps

Delete the field `uint16 investorShares` from the `Project` struct.

# L-2 Incorrect comment

## Description

Incorrect comments for functions `setPerformanceFee(uint16 _performanceFee)` and `setFeeTaker(address _feeTaker)`. Incorrect comments can provide misleading information to developers, testers, or auditors, leading to misunderstandings about the functionality, behavior, or security implications of the code. This misinformation can result in incorrect assumptions, which in turn can lead to the introduction of vulnerabilities or the overlooking of existing ones.

Incorrect comments in lines: 

[Link to code](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/ILOManager.sol#L154)

[Link to code](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/ILOManager.sol#L159)

## Recommended Mitigation Steps

It is recommended that the comments be corrected.

# L-3 Function `claimRefund(address uniV3PoolAddress)` can be called before `launchTime`

## Description

Potential vulnerability leading to violation of the protocol logic is in the function `setRefundDeadlineForProject(address uniV3Pool, uint64 refundDeadline)`. Vulnerability requires an owner error. If the owner sets the `refundDeadline` earlier than `launchTime`, it will enable the possibility to call the `claimRefund(address uniV3PoolAddress)` function from the `ILOManager.sol` contract and the `claimRefund(uint256 tokenId)` function from the `ILOPool.sol` contract before `launchTime`. This allows users and the project admin to request refunds outside of the provided window, thus disrupting the launch of the ILO Pools.


[Link to code](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/ILOManager.sol#L180-L184)


## Recommended Mitigation Steps

It is recommended to add to the `setRefundDeadlineForProject(...)` function a check that `refundDeadline` > `launchTime`.

```diff
    function setRefundDeadlineForProject(
        address uniV3Pool,
        uint64 refundDeadline
    ) external override onlyOwner {
        Project storage _project = _cachedProject[uniV3Pool];
+       require(refundDeadline > _project.launchTime, "Error refundDeadline");
        emit RefundDeadlineChanged(
            uniV3Pool,
            _project.refundDeadline,
            refundDeadline
        );
        _project.refundDeadline = refundDeadline;
    }
```