## [I-1]
Anyone can front run the owner and can get added into whitelist using `Whitelist.sol:receive()` function even if the owner had their own whitelist addresses. The owner can blacklist them but it would take time and efforts.

## Recommended Mitigation Steps
make `_isSelfWhiteListDisabled = true` in the constructor of `Whitelist.sol`, so that no one can get added to whitelist when owner have enough whitelist address and can make it false later when they need more addresses.


## [I-2]
`DEFAULT_DEADLINE_OFFSET` is the deadline before which no one should be able to claim refund but In `ILOManager.sol::initILOPool` function we are not checking if `params.launch > block.timestamp` or not, without this checking admins can initalized a ILOPool with `params.launchTime` less than block.timestamp, means they can also claim refund before the expected `DEFAULT_DEADLINE_OFFSET` set by owner

## Recommended Mitigation Steps
```diff
function initILOPool(InitPoolParams calldata params)
        external
        override
        onlyProjectAdmin(params.uniV3Pool)
        returns (address iloPoolAddress)
    {
.
.
.
-     require(params.start < params.end && params.end < _project.launchTime, "PT");
+     require(params.launchTime >= block.timestamp && params.start < params.end && params.end < _project.launchTime, "PT");
```


## [I-3]
In `ILOManager.sol::_initUniV3PoolIfNecessary()` there are 2 conditions if pool == address(0) or not, but if we initialize with `sqrtPriceX96 = 0` then it will revert as in `TickMath.sol` file `MIN_SQRT_RATIO == 4295128739`, so any sqrtPriceX96 less then this value will revert.

So when we create a new pool then we have to send sqrtPriceX96 value greater then MIN_SQRT_RATIO else it will revert and if we take a existing pool then `sqrtPriceX96Existing` can never be less than `MIN_SQRT_RATIO` because it would've revert if it was less then `MIN_SQRT_RATIO`

So it's impossible to set a sqrtPriceX96 of a existing Pool, so we can remove that functionality

## Recommended Mitigation 
```diff
    function _initUniV3PoolIfNecessary(PoolAddress.PoolKey memory poolKey, uint160 sqrtPriceX96)
        internal
        returns (address pool)
    {
        pool = IUniswapV3Factory(UNIV3_FACTORY).getPool(poolKey.token0, poolKey.token1, poolKey.fee);
        if (pool == address(0)) {
            pool = IUniswapV3Factory(UNIV3_FACTORY).createPool(poolKey.token0, poolKey.token1, poolKey.fee);
            IUniswapV3Pool(pool).initialize(sqrtPriceX96);
        } else {
            (uint160 sqrtPriceX96Existing,,,,,,) = IUniswapV3Pool(pool).slot0();
-            if (sqrtPriceX96Existing == 0) {
-                IUniswapV3Pool(pool).initialize(sqrtPriceX96);
-            } else {
                require(sqrtPriceX96Existing == sqrtPriceX96, "UV3P");
-            }
        }
    }
```