# L-1 - use of `tx.origin` to `transferOwnership` in the ILOManager::constructor()

## Impact

Using `tx.origin` is generally not a good practice since it can be abused by malicious contracts when whitelisted or trusted users are interacting with them. Users have to be very careful to avoid being impersonated when interacting with contracts from other protocols, which could unnecessarily burden users, even though the intended user is trusted he can still be impersonated with use of `tx.origin`.

## Proof of Concept

Provide direct links to all referenced code in GitHub. Add screenshots, logs, or any other relevant proof that illustrates the concept.

## Tools Used

Referenced Line of Code : [ILOManager.sol#L30](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/ILOManager.sol#L30)

Please refer to the following link [Solidity issue - Remove tx.origin](https://github.com/ethereum/solidity/issues/683)

## Recommended Mitigation Steps

Use `msg.sender` to initially transfer ownership or pass the address of initial owner as argument to the constructor