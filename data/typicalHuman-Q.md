# 1. Setting launchtime in the past could lead to unexpected behaviour

https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/ILOManager.sol#L58

The initProject function in the ILOManager allows the initialization of a project with a launch time parameter. However, the current implementation contains a bug where it is possible to initialize a project with a launchTime that is set in the past. This can lead to unexpected behavior and potential exploitation.


```javascript
    function initProject(InitProjectParams calldata params) external override afterInitialize() returns(address uniV3PoolAddress) {
 no check @>    uint64 refundDeadline = params.launchTime + DEFAULT_DEADLINE_OFFSET;

        PoolAddress.PoolKey memory poolKey = PoolAddress.getPoolKey(params.saleToken, params.raiseToken, params.fee);
        uniV3PoolAddress = _initUniV3PoolIfNecessary(poolKey, params.initialPoolPriceX96);
        
        _cacheProject(uniV3PoolAddress, params.saleToken, params.raiseToken, params.fee, params.initialPoolPriceX96, params.launchTime, refundDeadline);
        emit ProjectCreated(uniV3PoolAddress, _cachedProject[uniV3PoolAddress]);
    }
```

## Recommended Mitigation Steps
Add block.timestamp validation to launchTime parameter.

## Assessed type

Input validation.

---

# 2. The initialization of a project with an already existing Uniswap pool can be blocked.

https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/ILOManager.sol#L114-L122

The initProject function in the contract is susceptible to griefing vulnerability due to the manipulable nature of its parameter data. Malicious actors can exploit this vulnerability by copying parameter data from mempool transactions, enabling them to become administrators of existing Uniswap pools without authorization. This unauthorized access could lead to launching project with the uniswap pool created by another user. Malicious user can potentially block one or several specific users from being able to initiate a project with any existing pool by copying their transaction data and frontrunning them.

```solidity
   function _initUniV3PoolIfNecessary(PoolAddress.PoolKey memory poolKey, uint160 sqrtPriceX96) internal returns (address pool) {
        pool = IUniswapV3Factory(UNIV3_FACTORY).getPool(poolKey.token0, poolKey.token1, poolKey.fee);
        if (pool == address(0)) {
            pool = IUniswapV3Factory(UNIV3_FACTORY).createPool(poolKey.token0, poolKey.token1, poolKey.fee);
            IUniswapV3Pool(pool).initialize(sqrtPriceX96);
condition for existing pools @>     } else {
            (uint160 sqrtPriceX96Existing, , , , , , ) = IUniswapV3Pool(pool).slot0();
            if (sqrtPriceX96Existing == 0) {
                IUniswapV3Pool(pool).initialize(sqrtPriceX96);
            } else {
                require(sqrtPriceX96Existing == sqrtPriceX96, "UV3P");
            }
        }
    }

```

## Recommended Mitigation Steps
Remove the option of using an already existing Uniswap pool.

## Assessed type

Griefing


# 3. Incorrect vestConfig end parameter validation

https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/base/ILOVest.sol#L43-L44

The current implementation of the code fails to validate that the end parameter of a schedule is greater than the start parameter. This oversight allows for the creation of schedules where the end time can be less than the start time, which is logically incorrect and can lead to various issues in the scheduling functionality.

ILOVest.sol#L43-L44:
```solidity
require(schedule[i].start >= lastEnd, "VT");
lastEnd = schedule[i].end;
```


## Recommended Mitigation Steps
Add condition ` require(schedule[i].start < schedule[i].end, "VT");`

## Assessed type

Incorrect input validation.