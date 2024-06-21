# [01] Use of one step transfer for critical privileges instead of a two step process and also lack of zero address check

`owner` has critical privilages in the protocol. `ILOManager::transferAdminProject` allows the `owner` to transfer ownership (and associated critical privilages) in a one-step process.

https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/ILOManager.sol#L169-L173

```javascript
    function transferAdminProject(address admin, address uniV3Pool) external override onlyProjectAdmin(uniV3Pool) {
        Project storage _project = _cachedProject[uniV3Pool];
        _project.admin = admin;
        emit ProjectAdminChanged(uniV3Pool, msg.sender, admin);
    }
```

## Impact

Critical `admin` priviliges could be transferred to an incorrect address e.g. if
- `admin` mistakeanly inputs an incorrect address when calling `ILOManager::transferAdminProject`,
- the protocol becomes the victim of a Clipboard Replacement Attack: protocol owner copies the address that ownership is supposed to be transferred to, but a malware replaces the address on the clipboard with a different, attacker-controlled address that the protocol owner will eventually end of pasting when preparing to call `ILOManager::transferAdminProject`.

With the ownership privilages transferred to an incorrect account, the whole protocol will be compromised/unusable.

## Recommended Mitigation Steps

Transfer critical priviliges in a 2-step process. Modify `ILOManager` as follows:

```diff

contract ILOManager {

     ...

+    address public newOwner;

     ...

-    event OwnerUpdated(address newOwner);
+    event OwnershipTransferred(address indexed previousOwner, address indexed newOwner);
+    event NewOwnerProposed(address indexed proposedOwner);

...

-    function transferAdminProject(address admin, address uniV3Pool) external override onlyProjectAdmin(uniV3Pool) {
-        Project storage _project = _cachedProject[uniV3Pool];
-        _project.admin = admin;
-        emit ProjectAdminChanged(uniV3Pool, msg.sender, admin);
-    }


+    // Step 1: Propose a new admin
+    function proposeNewAdmin(address _newAdmin, address uniV3Pool) external onlyAuthorized {
+        _project.newAdmin = admin;
+        emit NewAdminProposed(_newAdmin);
+    }

+    // Step 2: New owner accepts the ownership
+    function acceptOwnership() external {
+        require(msg.sender == _project.newAdmin, "Not the proposed owner");
+        emit OwnershipTransferred(owner, _project.newAdmin);
+        _project.admin = _project.newAdmin;
+        _project.newAdmin = address(0);
+    }

     ...
}
```

# [02] No event emissions for critical state changes in `ILOManager::setPlatformFee` and `ILOManager::setPerformanceFee`

`ILOManager::setPlatformFee` and `ILOManager::setPerformanceFee` modify critical state variables, but no events are defined and emitted to broadcast the changes.

## Impact

1. Reduced transparency
2. Difficulty in tracking changes
3. Inefficient or impossible integration with other contracts and services


## Recommended Mitigation Steps

Define and emit events for critical changes performed in `ILOManager::setPlatformFee` and `ILOManager::setPerformanceFee`:


https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/ILOManager.sol#L149-L157
```diff
// Define events to be emitted on state changes
+ event SetPlatformFeeSet(bool mode);
+ event PerformanceFeeSet(address token);

contract ILOManager {

    ...
    /// @notice set platform fee for decrease liquidity. Platform fee is imutable among all project's pools
    function setPlatformFee(uint16 _platformFee) external onlyOwner() {
+       emit SetPlatformFeeSet(_platformFee);
        PLATFORM_FEE = _platformFee;
    }

    /// @notice set platform fee for decrease liquidity. Platform fee is imutable among all project's pools
    function setPerformanceFee(uint16 _performanceFee) external onlyOwner() {
+       emit PerformanceFeeSet(_performanceFee);
        PERFORMANCE_FEE = _performanceFee;
    }
    ...
}
```

# [03] `ILOPool::buy` accepts `zero value` as a valid value for `raiseAmount`

`ILOPool::buy` accepts `zero value` as a valid value for the `raiseAmount` does not perform input validation on `raiseAmount`. Transaction flow will continue and only fail much later in the execution. 

## Impact 
Users calling `ILOPool::buy` and accidentally inputting `0` for `raiseAmount` will waste more gas, as the transaction will fail much later in the execution.

## Recommended Mitigation Steps

Perform input validation on `_percentage` as follows:

```diff

    function buy(uint256 raiseAmount, address recipient)
        external override 
        returns (
            uint256 tokenId,
            uint128 liquidityDelta
        )
    {

+       require(raiseAmount > 0, "Invalid raiseAmount");

        ...


    }
```
