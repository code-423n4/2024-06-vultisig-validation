
### [GAS-0] Usage of array length variable in loops which is not in variables 

**Description:** 

By putting the length of an array in a variable before the loop we can safe up gas since the array length is stored in memory/storage and every single time we check it and we spend gas for doing so.

- Found in src/ILOManager.sol `ILOManager::launch` (src/ILOManager.sol#L204)

	```solidity
	    for (uint256 i = 0; i < initializedPools.length; i++) {
	```

- Found in src/ILOPool.sol `ILOPool::unlockedLiquidity` (src/ILOPool.sol#L405)

	```solidity
        for (uint256 index = 0; index < vestingSchedule.length; index++) {
	```

- Found in src/ILOVest.sol `ILOVest::_validateSharesAndVests` (src/ILOVest.sol#L20)

	```solidity
	    for (uint256 i = 0; i < vestingConfigs.length; i++) {
	```

**Recommended Mitigation:**

Saving gas is as easy as creating a new variable storing the length of the array and using it in the for loop instead, for example:

```solidity
+   uint256 initializedPoolsLength = initializedPools.length;
    for (uint256 i = 0; i < initializedPoolsLength; i++) {
```

```solidity
+   uint256 vestingScheduleLength = vestingSchedule.length;
    for (uint256 index = 0; index < vestingScheduleLength; index++) {
```

```solidity
+   uint256 vestingConfigsLength = vestingConfigs.length;
	for (uint256 i = 0; i < vestingConfigsLength; i++) {
```

**--------------------------------**

### [GAS-1] Usage of calldata instead of memory

**Description:** 

By using calldata instead of memory we can reduce the gas consumption. Since the variable is not being changed and is read only using calldata is better.

- Found in src/ILOVest.sol `ILOVest::_validateSharesAndVests` (src/ILOVest.sol#L17)

	```solidity
	    function _validateSharesAndVests(uint64 launchTime, VestingConfig[] memory vestingConfigs) internal pure { 
            // ...     
        }
	```

**Recommended Mitigation:**

Change memory to calldata:

```solidity
	function _validateSharesAndVests(uint64 launchTime,
+        VestingConfig[] calldata vestingConfigs)
-        VestingConfig[] memory vestingConfigs) 
        internal pure { }
```
