# Title: The [claim](https://github.com/code-423n4/2024-06-vultisig/blob/0957ff9e50441cd6de6b4f6e28c7ea93f5cffa85/src/ILOManager.sol#L184-L261) function shouldn't be payable
    
The [ILOPool.claim](https://github.com/code-423n4/2024-06-vultisig/blob/0957ff9e50441cd6de6b4f6e28c7ea93f5cffa85/src/ILOManager.sol#L184-L261) function doesn't need to be a payable function.

```diff
File: src\ILOPool.sol
184:     function claim(uint256 tokenId)
185:         external
-            payable
187:         override
188:         isAuthorizedForToken(tokenId)
189:         returns (uint256 amount0, uint256 amount1)
```