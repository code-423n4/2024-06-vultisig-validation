# QA Report

## Findings

| Finding | Title                                          | Severity |
|---------|------------------------------------------------|----------|
| L-01    | Misleading Events in `batchWhitelist` and `batchRemoveWhitelist` | Low      |
| L-02    | Unresolved TODOs in `IILOManager` Interface    | Low      |

---

### L-01: Misleading Events in `batchWhitelist` and `batchRemoveWhitelist`

#### Impact
The methods `batchWhitelist` and `batchRemoveWhitelist` can lead to emitting misleading events because the return values of the sub calls to the underlying `EnumerableSet.add()` and `EnumerableSet.remove()` methods are not checked.

#### Proof of Concept
https://github.com/code-423n4/2024-06-vultisig/blob/main/src/base/ILOWhitelist.sol#L47-#L54

For example, `add()` returns false if the object is already in the set, but in our case, because this returned false is not checked, still a `SetWhitelist(user, true);` event will be emitted.

Similarly, if an object that is not present in the set is attempted to get removed, although it is not in the set, the `remove` function would return false. Without checking this, the contract would emit an event indicating the address was removed.

Not checking the return values might also lead to situations where addresses that should have been whitelisted are not whitelisted and vice versa, addresses that should have been removed are not actually removed.

#### Tools Used
Manual Review

#### Recommended Mitigation Steps
Check the return values of OZ `EnumerableSet.add` and `EnumerableSet.remove` and emit events if `true`. The code should look like this:

```solidity
function _setWhitelist(address user) internal {
    bool added = EnumerableSet.add(_whitelisted, user);
    if (added) {
        emit SetWhitelist(user, true);
    }
}

function _removeWhitelist(address user) internal {
    bool removed = EnumerableSet.remove(_whitelisted, user);
    if (removed) {
        emit SetWhitelist(user, false);
    }
}
```

### L-02: Unresolved TODOs in `IILOManager` Interface

#### Impact
There are unresolved TODOs in the `IILOManager` interface, which indicates incomplete code and potential missing features or logic that needs to be addressed.

#### Proof of Concept
https://github.com/code-423n4/2024-06-vultisig/blob/main/src/interfaces/IILOManager.sol#L60

```solidity
struct InitPoolParams {
    address uniV3Pool;
    int24 tickLower; 
    int24 tickUpper;
    uint256 hardCap; // total amount of raise tokens
    uint256 softCap; // minimum amount of raise token needed for launch pool
    uint256 maxCapPerUser; // TODO: user tiers
    uint64 start;
    uint64 end;

    // config for vests and shares. 
    // First element is allways for investor 
    // and will mint nft when investor buy ilo
    IILOVest.VestingConfig[] vestingConfigs;
```

## Tools Used
Manual Review

## Recommended Mitigation Steps
Code architecture, incentives, and error handling/reporting questions/issues should be resolved before deployment.


