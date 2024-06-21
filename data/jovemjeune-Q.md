## L-01 Incorrect Check In mulDiv method of FullMath library 
This vulnerability exists in the following code snippet of the [FullMath](https://github.com/code-423n4/2024-06-vultisig/blob/main/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/FullMath.sol#L22-L35) library
```
      assembly {
            let mm := mulmod(a, b, not(0))
            prod0 := mul(a, b)
            prod1 := sub(sub(mm, prod0), lt(mm, prod0))
        }

        // Handle non-overflow cases, 256 by 256 division
        if (prod1 == 0) {
            require(denominator > 0);
            assembly {
                result := div(prod0, denominator)
            }
            return result;
        }

```
The existing overflow detection mechanism within the mulDiv function assumes that if the prod1 is 0 then there is no overflow in the product however if a * b = 2 ** 256,which is same with uint256.max + 1, then the value of the prod0 will overflow and being set to 0.Afterall,the value of prod1 will be assigned to 0 as well due to the following reason : 
if prod0 is 0 then prod1 will be equal to sub(0,lt(0,0)) which is again 0 and even through the product overflows,the if (prod1 == 0) condition will be true.This limitation can be mitigated by utilizing following library for the multiplication [OpenZeppelin Math Library](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/utils/math/Math.sol#L44-L54).
