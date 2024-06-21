# Low Errors:
1. 
Incorrect use of payable.transfer()

`Whitelist::receive` implements potentially dangerous transfer

```javascript
    receive() external payable {
        if (_isSelfWhitelistDisabled) {
            revert SelfWhitelistDisabled();
        }
        if (_isBlacklisted[_msgSender()]) {
            revert Blacklisted();
        }
        _addWhitelistedAddress(_msgSender());
@>        payable(_msgSender()).transfer(msg.value);
    }
```

https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/contracts/Whitelist.sol#L73


When transferring ETH to recipients using Solidity's transfer() or send() methods, certain limitations can prevent a successful transfer, especially if the recipient is a smart contract. These limitations arise under the following conditions:

1. The smart contract does not implement a payable fallback function.
2. The smart contract implements a payable fallback function that requires more than 2300 gas units.
3. The smart contract implements a payable fallback function that uses less than 2300 gas units, but the call is made through a proxy that increases the gas usage beyond 2300 gas units.

read more about it:
https://consensys.io/diligence/blog/2019/09/stop-using-soliditys-transfer-now/

## Impact
a smart contract might not be able to Safe-whitelist in some cases.


## Tools Use

Manual Review

## Recommended Mitigation Steps

Using call with its returned boolean checked in combination with re-entrancy guard is highly recommended.

```
        (bool success, ) = payable(msg.sender).call{value: msg.value}("");
        require(success, " Transfer of ETH Failed");
```

2. 
## Issue 
The `VultisigWhitelisted::setWhitelistContract` function can be called multiple times, potentially leading to unexpected behaviors, financial losses, and token freezing or pausing.

https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/contracts/extensions/VultisigWhitelisted.sol#L10

https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/contracts/extensions/VultisigWhitelisted.sol#L21-L24


## Explanation 
The `VultisigWhitelisted` contract includes the following specification:

` * @notice If whitelist period is ended, owner will set whitelist contract address back to address(0) and tokens will be transferred freely`

however, the `VultisigWhitelisted::setWhitelistContract` function lacks any modifier or flag to restrict its invocation, allowing it to be called at any time and multiple times.


## Impact
in more advanced stages, whether due to an error or a malicious actor gaining control of the owner's private key, the unrestricted `setWhitelistContract` function can be called, leading to unexpected behaviors. These behaviors might include financial losses and token freezing or pausing, significantly affecting the contract's integrity and users' trust.

## Tools Used
Manual Review

## Recommended Mitigation Steps
Implement a modifier or a flag to ensure `VultisigWhitelisted::setWhitelistContract` is only callable once or until a specific period. This will prevent unauthorized or repeated calls, safeguarding the contract from the outlined risks.

3.
The `ILOManager::initILOPool` function lacks input validation for `params.softCap` and `params.hardCap`. If the protocol inadvertently sets a higher softCap than hardCap, it will render the entire project unable to launch.

https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/ILOManager.sol#L71-L107
## Recommended Mitigation Steps
make sure hardcap is higher than softcap.

4. 
`ILOPool::claimRefund` will revert if a token is paused, and might cause enexpected result for the user.
```javascript
    /// @inheritdoc IILOPool
    function claimRefund(uint256 tokenId) external override refundable() isAuthorizedForToken(tokenId) {
        uint256 refundAmount = _positions[tokenId].raiseAmount;
        address tokenOwner = ownerOf(tokenId);

        delete _positions[tokenId];
        delete _positionVests[tokenId];
        _burn(tokenId);

  @>      TransferHelper.safeTransfer(RAISE_TOKEN, tokenOwner, refundAmount);
        emit UserRefund(tokenOwner, tokenId,refundAmount);
    }
```
since the `claimRefund` function tries to transfer the token inside the refund invocation, it will revert for the user,and the project might launch after than, even if the user want to get his refund.
## Recommended Mitigation Steps
seperate this into two functions, and allow invoke a refund, so the project will be unlaunchable, and a function to claim the refund, so the refund modifier will not depend on the transfer of a token.


 