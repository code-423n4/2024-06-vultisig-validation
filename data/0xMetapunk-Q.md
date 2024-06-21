# Lines of code

https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol#L41

# Vulnerability details
## Impact
The impact will be that the TWAP will be calculated for shorter timeframe which can lead to price manipulation also the price feed is of a low liquidity pool 

## Proof of Concept
```solidity
   uint32 longestPeriod = OracleLibrary.getOldestObservationSecondsAgo(pool);
    uint32 period = PERIOD < longestPeriod ? PERIOD : longestPeriod;
    int24 tick = OracleLibrary.consult(pool, period);
```

Here the TWAP price is being used as an oracle from a low liquidity pool, since the liquidity provided is low w.r.t to other big pools even though the TWAP price is taken it could be susceptible for multiple small flash loans attacks over the period which could effect the price, also in the above code if `longestPeriod` is taken are the period then a small flash loan can also cause big price manipulation since longestPeriod is less than the min 30 minutes and if it in seconds then manipulation is possible 

Also according to Uniswap docs regarding using TWAP pricing as oracle, they have pointed to an interesting find that is miners who control 3blocks in a row can manipulate the pool and even for big pools if a miner can mine 3blocks in a row he can still effect the pool and here its a small pool so it could for sure be impacted also after shifting to the POS a miner can well in advance know the blocks they will mine so it is not recommended to use TWAP as an oracle 

https://blog.uniswap.org/uniswap-v3-oracles

as u can see the cost to manipulates falls down rapidly for big pools if a miner can control continuous blocks and its looking at etherscan we can clearly see that similar miners are able to mine a block   

## Tools Used
Manual Review, Foundry


