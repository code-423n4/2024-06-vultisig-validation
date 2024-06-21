# TickMath might revert in solidity versions > 0.8

## Description

UniswapV3’s TickMath library was changed to allow compilations for solidity version 0.8. However, adjustments to account for the implicit overflow behavior that the contract relies upon were not performed. The [UniswapV3Oracle.sol](https://github.com/code-423n4/2024-06-vultisig/blob/main/hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol) is compiled with version `> 0.8` and indirectly uses this library through the [OracleLibrary](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol#L5). In the worst case, it could be that the library always reverts (instead of overflowing as in previous versions), leading to broken protocol functionalities.

## Impact

The protocol might falsely revert in situations where overflowing/underflowing is required (due to the nature of Uniswap's math), leading to incorrect behavior.

## Tools used

Manual review

## Recommendation

Either use SOLC < 0.8 in the UniswapV3Oracle contract or add `unchecked`, to the `peek()` function. 