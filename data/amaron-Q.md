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
