## There is no way for ILOPool to send ETH back to the user in case of mistake during work with payable **multicall()**
https://github.com/code-423n4/2024-06-vultisig/blob/main/src/base/Multicall.sol#L11-L26

```
function multicall(bytes[] calldata data) public payable override returns (bytes[] memory results) 
```

### Recommendation
Create manager/owner only function to send eth back

## DEFAULT_DEADLINE_OFFSET can be bypassed during project creation
When project initialized it should have two time parameters:
**launchTime** - provided by user
**refundDeadline** - calculated by the protocol
```
uint64 refundDeadline = params.launchTime + DEFAULT_DEADLINE_OFFSET;
```

Because compiler for this contract is pretty old there is no overflow protection and malicious address can provide big launch time and adding the constant will move **refundDeadline** in the past.

This **refundDeadline** important for ILOPool, because it shows is anyone eligible to start refunding process and basically lock the pool for the launch.

### Marked as QA because there is no damage for the protocol from this attack vector.
1) Projects with huge Launch date won't be able to be launched anyway.
2) Such refund shouldn't harm Project admin or users of this project.

## ILOPool **claim()** don't require payable modificator.
Because don't work with eth but still it can bring an issue for user who can send eth that will stuck there forever.
https://github.com/code-423n4/2024-06-vultisig/blob/main/src/interfaces/IILOPool.sol#L101