# [L-01] Custom retrun data/result due to revert in multicall
## Impact
some contracts  may return data by implementing custom error handling procedures , so assuming the [result](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/base/Multicall.sol#L22) is always a string is wrong and utilizing abi.decode for that is may result in failures

https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/base/Multicall.sol#L11
## Recommendation
 Eliminate the string upon a revert to mitigate any potential adverse effects on contract functionality

# [L-02] Weird Approve behaviour
## Impact
Vultisig uses `approve` that do not handle non standard erc20 tokens like

>  token contracts do not return value
>  token contacts revert the transaction when the allowance is not 0[USDT]

https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/contracts/Vultisig.sol#L18
In worst case scenario user's may have to double approve or see their transactions get revert
## Recommendation 
Use Solmate safeApprove which handles this case

# [L-03] Hardcoded TWAP interval
## Impact
Although having 30min in twap interval is a fine duration, since the cost of twap manipulation will also increase with time. But with known duration a manipulation attack can be carried out because of not having any way to change the duration.
https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol#L16
## Recommendation 
Don't hardcode it and have a function for changing the duration

# [L-04] Hardcoded Slippage parameters
## Impact
In times of high market volatality like UST/LUNA crash users may not be able to transfer out their exact required amount due to the hardcoded slippage
https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol#L45
## Recommendation
Instead of hardcoding it let it be user specified or set/change upto a certain percentage by some trusted entity 

# [L-05] Lack of validation of create2 return value
## Impact
`initILOPool` function is used to deploy lightweight proxy contracts that act as corresponding to a uniswap pool. The function does not revert properly if there is a failed contract deployment or revert from the create2 opcode as it does not properly check the returned address for bytecode. The create2 opcode returns the expected address which will never be the zero address (as is what is currently checked in [here](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/442886ed5ff8a0b9ab477b191f5238541ee6d772/contracts/proxy/Clones.sol#L87).

https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/ILOManager.sol#L84

## Recommendation
Have a check for `iszero(extcodesize(result))` for `iloPoolAddress`