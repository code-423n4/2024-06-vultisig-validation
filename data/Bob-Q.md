# No range checks on fees can lead to underflow.

`PLATFORM_FEE` and `PERFORMANCE_FEE` are meant to be BPS, i.e. <= 10000. However, [they can be set](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/ILOManager.sol#L149-L157) to more than that. 

This leads to an underflow in `_deductFees()`.

```
    function _deductFees(uint256 amount0, uint256 amount1, uint16 feeBPS) internal pure 
        returns (
            uint256 amount0Left, 
            uint256 amount1Left
        ) {
        amount0Left = amount0 - FullMath.mulDiv(amount0, feeBPS, BPS);
        amount1Left = amount1 - FullMath.mulDiv(amount1, feeBPS, BPS);
    }
```
[Link](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/ILOPool.sol#L438-L445)

This undeflow bricks `claim()` functionality. However, the fees can only be set by owner of ILOManager though.

Consider adding range checks when setting `PLATFORM_FEE` and `PERFORMANCE_FEE`.

# Missing checks on `LinearVest` interval.


[_validateVestSchedule()](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/base/ILOVest.sol#L35) does not check that LinearVest.start is before LinearVest.end. This makes it possible to add vesting config with overlapping vesting schedules or vesting schedules before the launch date. 

Add this test case to `test/ILOPool.t.sol`. It illustrates how to add misconfigured vesting schedules.

```
    function testVestBeforeLaunch() external {
        IILOVest.LinearVest[] memory attackVestConfigs = new IILOVest.LinearVest[](2);
        // This schedule has start and end flipped.
        attackVestConfigs[0] = IILOVest.LinearVest({
            shares: 3000, // 30%
            start: LAUNCH_START + 1,
            end: LAUNCH_START - 100
        });
        // This schedule is before launch time.
        attackVestConfigs[1] = IILOVest.LinearVest({
            shares: 7000, // 70%
            start: LAUNCH_START - 99,
            end: LAUNCH_START - 90
        });

        IILOVest.VestingConfig[] memory vestingConfigs = new IILOVest.VestingConfig[](4);
        vestingConfigs[0] = IILOVest.VestingConfig({
            shares: 2000, // 20%
            recipient: address(0),
            schedule: attackVestConfigs
        });
        vestingConfigs[1] = IILOVest.VestingConfig({
            shares: 3000, // 30%
            recipient: TREASURY_RECIPIENT,
            schedule: _getLinearVesting()
        });
        vestingConfigs[2] = IILOVest.VestingConfig({
            shares: 2000, // 20%
            recipient: DEV_RECIPIENT,
            schedule: _getLinearVesting()
        });
        vestingConfigs[3] = IILOVest.VestingConfig({
            shares: 3000, // 30%
            recipient: LIQUIDITY_RECIPIENT,
            schedule: _getLinearVesting()
        });

        IILOManager.InitPoolParams memory params = _getInitPoolParams();
        params.vestingConfigs = vestingConfigs;

        iloPool = _initPool(PROJECT_OWNER, params);
        _launch();
    }
```

Consider enforcing that `LinearVest.start` < `LinearVest.end`.

# Refund deadline calculation can overflow

[initProject()](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/ILOManager.sol#L58) doesn't have overflow checks. So, it's possible to trigger a refund before launch time (for very large values of the latter).

Add this test case to `test/ILOManager.t.sol` for a demonstration.

```
    function testRefundTimeOverflow() external {
        address uniswapV3pool = iloManager.initProject(
            IILOManager.InitProjectParams({
                saleToken: mockProject().saleToken,
                raiseToken: mockProject().raiseToken,
                fee: 10000,
                initialPoolPriceX96: mockProject().initialPoolPriceX96 + 1,
                launchTime: type(uint64).max
            })
        );

        uint64 launchTime = iloManager.project(uniswapV3pool).launchTime;
        uint64 refundDeadline = iloManager.project(uniswapV3pool).refundDeadline;

        assertGt(uint256(refundDeadline), uint256(launchTime));
    }
```