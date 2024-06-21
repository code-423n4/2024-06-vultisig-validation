## There is no way for ILOPool to send ETH back to the user in case of mistake during work with payable **multicall()**
https://github.com/code-423n4/2024-06-vultisig/blob/main/src/base/Multicall.sol#L11-L26

```
function multicall(bytes[] calldata data) public payable override returns (bytes[] memory results) 

```

### Recommendation
Create manager/owner only function to send eth back