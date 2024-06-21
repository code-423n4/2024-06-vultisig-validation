Contracts should be deployed with the same compiler version.Locking the pragma helps to ensure that contracts do not accidentally get deployed using another pragma.

Code Reference
https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/contracts/Whitelist.sol#L2

https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/ILOPool.sol#L2

https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/libraries/LiquidityAmounts.sol#L2

Recommendation
Consider locking the pragma in all the contracts to the particular version.
It is not recommended to use a floating pragma in production