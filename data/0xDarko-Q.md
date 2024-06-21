## `Whitelist.sol` `_isSelfWhitelistDisabled` is set to false at launch

## Description
According to the docs on code4arena, this should not be disabled at launch -
```
Set allowed whitelisted index(Especially when self whitelist is allowed, anyone can just send ETH and get whitelisted slot and each slot will be assigned by an index called whitelistIndex.
```

## Impact
With `_isSelfWhitelistDisabled` not being disabled at launch, user's can mass send eth on multiple accounts to the `Whitelist` contract and obtain their whitelist, leading to a headache for the owner to either increase index or blacklist those addresses since by the time it's set to `true`, the `_allowedWhitelistIndex` could be filled ruining the flow of how the whitelisting was supposed to be done.

## Recommended Mitigation
In the constructor set `_isSelfWhitelistDisabled` to true.
```diff
    constructor() {
        _maxAddressCap = 3 ether;
        _locked = true; // Initially, liquidity will be locked
+       _isSelfWhitelistDisabled = true;
    }
```

## `Whitelist::_addWhitelistedAddress` Is Marked As Private Not Internal

## Description
`ILOManager::initialize` natspec states the following indicating improper visibility set -
```
    /// @notice Internal function used for whitelisting. Only increase whitelist count if address is not whitelisted before
    /// @param whitelisted Address to be added
    function _addWhitelistedAddress(address whitelisted) private {
        ....
    }
```

## Recommended Mitigation
Simply swap `private` to `internal`
```diff
-    function _addWhitelistedAddress(address whitelisted) private {
+    function _addWhitelistedAddress(address whitelisted) internal {

        ....
    }
```
