## Title
Incorrect exponentiation.


## Code
https://github.com/Uniswap/v3-core/blob/d8b1c635c275d2a9450bd6a78f3fa2484fef73eb/contracts/libraries/FullMath.sol#L87


## Impact
Has bitwise-xor operator ^ instead of the exponentiation operator **


## Tools Used
Slither


## Recommendation
Use the correct operator ** for exponentiation.




## Title
Payable functions using delegatecall inside a loop


## Code
https://github.com/code-423n4/2024-06-vultisig/blob/main/src/base/Multicall.sol#L14


## Impact
This means that each delegatecall within the
for loop will retain the msg.value of the transaction.


## Tools Used
Slither


## Recommended Mitigation Steps
Carefully check that the function called by delegatecall is not payable/doesn't use msg.value.