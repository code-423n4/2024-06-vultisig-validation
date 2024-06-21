## Possible over/underflows due to 0.7.6.

Affected link:
https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/ILOPool.sol#L136
```
        // check if raise amount over capacity
        require(saleInfo.hardCap - totalRaised >= raiseAmount, "HC");
        totalRaised += raiseAmount;
```
The above code is compiled in 0.7.6, therefore no over/underflow checks are built in. The contract mainly uses fullMath from uniswap to check for these with some exceptions like this one. Since parameters are never checked to be truthful values, a hardCap of 2 could be exploited into the max uint256 value near it.
Lets assume:
hardCap = 2;
1) buy() -> totalRaised = 0 -> we provide 1 wei. -> 2-1 >= 1 passes.
2) buy() -> totalRaised = 1 -> we can now provide how ever much we want as long that its > than 1, since: 2 - 1e18 = (2**256-1) - (1e18 - 1).

## Lp calculation for share distribution is unfair seen from a dollar value.

Uniswapv3's liquidity calculation is chosen from its lowest value between the sqrting the difference dividing the exchange rate. In an x axis where the x axis represents the weth amount in dollars, a NON linear relation is seen. So like the previous audit of PREDY finance or any other perpetuals calculation a lp distribution must use a smoothing factor like Gamma or so, in order to keep the lp shares given to users truthful with their deposits.

This basically means that if i create my token 0xMango/USDC to start at a price of 20 dollars. Anyone buying 100 dollars worth of lp shares, might be exploited by the admin of the project, due to them owning the tokens and being able to move the price before the ILOPool.sol deposits liquidity. This will lead to deposits which are valued LESS than the deposit amount.

See more about the math of this here: (Written by someoen from uniswap i believe)
https://www.desmos.com/calculator/oiv0rti0ss

I calculated this myself and the equation for a smoothing factor does not lead to a exponential equation but rather a more complex, multi base polynomial.

Attack/Exploit:
Usdc deposits were made and the contract will make a lp deposit to a fixed range. The admin can move the spot price or sqrtPriceX96 from the pool to a arbitrary place to make the lp deposit worth LESS in terms of uint128 liquidityAmout to shareholders than the actual capital going in, since as mentioned, the graph is not linear to dollar value amounts.