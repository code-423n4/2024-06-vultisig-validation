## Title
Incorrect exponentiation.


## Code
https://github.com/Uniswap/v3-core/blob/d8b1c635c275d2a9450bd6a78f3fa2484fef73eb/contracts/libraries/FullMath.sol#L87


## Impact
Has bitwise-xor operator ^ instead of the exponentiation operator **


## Recommendation
Use the correct operator ** for exponentiation.