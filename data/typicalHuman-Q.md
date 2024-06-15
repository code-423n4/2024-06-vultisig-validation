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