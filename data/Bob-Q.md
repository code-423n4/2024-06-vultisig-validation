## Summary

No range checks on fees can lead to underflow.

## Vulnerability Details

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

## Recommended Mitigation Steps
Add range checks to when setting `PLATFORM_FEE` and `PERFORMANCE_FEE`. 