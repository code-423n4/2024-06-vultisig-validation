## 1) Modifier `onlyVultisig()` is only used once, 

https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/contracts/Whitelist.sol#L53C1-L59C6.

It would be more gas-efficient to turn this into an in-line check for the function `checkWhitelist()` where it is called

Helps to save 20 - 40 gas because of,
1) 2 extra `JUMP` instructions
2) additional stack operations needed for function calls

## 2) Costs more gas to initialize variables to 0 than to let the default of 0 be applied

`uint i = 0` => `uint i`

https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/contracts/Whitelist.sol#L192

