# [L-01] Custom retrun data/result due to revert in multicall
some contracts  may return data by implementing custom error handling procedures , so assuming the [result](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/base/Multicall.sol#L22) is always a string is wrong and utilizing abi.decode for that is may result in failures

https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/base/Multicall.sol#L11
## Recommendation
 Eliminate the string upon a revert to mitigate any potential adverse effects on contract functionality