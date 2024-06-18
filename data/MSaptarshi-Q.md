# [L-01] Custom retrun data/result due to revert in multicall
some contracts  may return data by implementing custom error handling procedures , so assuming the [result](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/base/Multicall.sol#L22) is always a string is wrong and utilizing abi.decode for that is may result in failures

https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/base/Multicall.sol#L11
## Recommendation
 Eliminate the string upon a revert to mitigate any potential adverse effects on contract functionality

# [L-02] Weird Approve behaviour
Vultisig uses `approve` that do not handle non standard erc20 tokens like

> Some token contracts do not return value{Tether Gold]
> Some token contacts revert the transaction when the allowance is not 0[USDT]

https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/contracts/Vultisig.sol#L18
In worst case scenario user's may have to double approve or see their transactions get revert
## Recommendation 
Use Solmate safeApprove which handles this case

# [L-03] Hardcoded TWAP interval
Although having 30min if twap interval is a fine duration, since the cost of twap manipulation will also increase with time. But with known duration a manipulation attack can be carried out because of not having any way to change the duration.
https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol#L16
## Recommendation 
Don't hardcode it and have a function for changing the duration

# [L-04] Hardcoded Slippage parameters
In times of high market volatality like UST/LUNA crash users may be able to transfer out their exact required amount due to the hardcoded slippage
https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol#L45
## Recommendation
Instead of hardcoding it let it be user specified or set/change upto a certain amount by some trusted entity 