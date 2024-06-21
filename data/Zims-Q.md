`Whitelist::receive` has no minimum value to get on the whitelist.

https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/contracts/Whitelist.sol#L65-L74

Has a function to add `msg.sender` to whitelist. It returns the `msg.value` to the sender and adds him to the whitelist. But there is no min of the value meaning that it can be called by bot accounts with minimal setup.
Seting a minimum txn value should reflect genuine interest and engagement from users.

``` javascript
    /// @notice minimum ETH amount to use for self-whitelisting.
    uint256 private _minWhitelistEth;
...
        constructor() {
        _maxAddressCap = 3 ether;
        _minWhitelistEth = 0.1 ether;
        _locked = true; // Initially, liquidity will be locked
    }
...
    receive() external payable {
        if (_minWhitelistEth > msg.value) {
           revert TxnValueToLow()
        }
        if (_isSelfWhitelistDisabled) {
            revert SelfWhitelistDisabled();
        }
        if (_isBlacklisted[_msgSender()]) {
            revert Blacklisted();
        }
        _addWhitelistedAddress(_msgSender());
        payable(_msgSender()).transfer(msg.value);
    }
```
Also, create a function to change the min later.
```javascript

    function setMinWhitelistEth(uint256 newCap) external onlyOwner {
        _minWhitelistEth = newCap;
    }
```