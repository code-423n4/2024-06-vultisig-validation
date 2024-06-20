### Title
Missing Event
### Severity
Low
### Target
https://github.com/code-423n4/2024-06-vultisig/blob/main/hardhat-vultisig/contracts/Whitelist.sol#L136-L138
https://github.com/code-423n4/2024-06-vultisig/blob/main/hardhat-vultisig/contracts/Whitelist.sol#L142-L144
https://github.com/code-423n4/2024-06-vultisig/blob/main/hardhat-vultisig/contracts/Whitelist.sol#L148-L150
https://github.com/code-423n4/2024-06-vultisig/blob/main/hardhat-vultisig/contracts/Whitelist.sol#L154-L156
https://github.com/code-423n4/2024-06-vultisig/blob/main/hardhat-vultisig/contracts/Whitelist.sol#L160-L162
https://github.com/code-423n4/2024-06-vultisig/blob/main/hardhat-vultisig/contracts/Whitelist.sol#L166-L168
https://github.com/code-423n4/2024-06-vultisig/blob/main/hardhat-vultisig/contracts/Whitelist.sol#L173-L175
https://github.com/code-423n4/2024-06-vultisig/blob/main/hardhat-vultisig/contracts/Whitelist.sol#L179-L181
https://github.com/code-423n4/2024-06-vultisig/blob/main/hardhat-vultisig/contracts/extensions/VultisigWhitelisted.sol#L22-L24
## Description
In functions such as:

- `setLocked`,
- `setMaxAddressCap`,
- `setVultisig`,
- `setIsSelfWhitelistDisabled`,
- `setOracle`,
- `setPool`,
- `setBlacklisted`,
- `setAllowedWhitelistIndex`,
- `setWhitelistContract`

no events, which makes it difficult to track changes
## Recommendations
Add an event and emit that at the end of  functions .

---

### Title
Incorrect NatSpec 
### Severity
Low
### Target
https://github.com/code-423n4/2024-06-vultisig/blob/main/hardhat-vultisig/contracts/Whitelist.sol#L230-L236
## Description
The `NatSpec` says this is an `internal` function, but `private` is used
```solidity
->  /// @notice Internal function used for whitelisting. Only increase whitelist count if address is not whitelisted before
    /// @param whitelisted Address to be added
->  function _addWhitelistedAddress(address whitelisted) private {
        if (_whitelistIndex[whitelisted] == 0) {
            _whitelistIndex[whitelisted] = ++_whitelistCount;
        }
    }
```
### Title
incorrect function name
### Severity
Informational
### Target
https://github.com/code-423n4/2024-06-vultisig/blob/main/src/ILOManager.sol#L67-L69
## Description
consider changing the name of the function to `getProject`

```solidity
function getProject(
        address uniV3PoolAddress
    ) external view override returns (Project memory) {
        return _cachedProject[uniV3PoolAddress];
    }
```

