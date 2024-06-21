[l-1]
## Summary
`Whitelist.sol::setMaxAddressCap` does'nt ensure the `new cap` provided is less than maxAddressCap. 

## Vulnerability Details
In contract `Whitlist.sol`, the function `setMaxAddressCap` sets new address cap proivided by onlyOwner, however it does'nt ensure that the new cap is less than MaxaddressCap.The onlyOwner entity can set the new cap which exceeds the desired max cap i.e 3 ether, which is intented by the protocol. This will lead to certain functionality of the protocol to behave unexpectly.

## Impact
User can contribute more than max capped amount(3 ether), since one if block in `checkWhitelist` check for it and revert if its more than max cap(3 eth), however if max cap is set more than desired maxCap(3 eth) , it won't revert and a user can contribute more than desired max cap.

## Tools Used
Manual review

## Recommendations
Adding an if block that ensures the new cap is less than max cap will do
```diff
if(newCap>maxAddressCap){
   revert MaxAddressCapOverflow();
}
```

[l-2]
## Summary
`Whitelist.sol::addWhitelistedAddress` does'nt check whitelistCount before adding a new address to whitelist which is 1k. 

## Vulnerability Details
In contract `Whitelist.sol`, the function `addWhitelistedAddress` doesnt check if there are enough slots left for more whitelist addresses or by adding this address if we're exceeding the max `_whitelistCount` which is 1k.

## Impact
In the case when all the 1k whitelist slots are filled, genuine addresses cant be added to whitelist. or it can be case where we are adding addresses even after the set limit.

## Tools Used
Manual review

## Recommendations
Add a check for whitelist count which ensures if the count is less than 1k then act accordingly as this issue relates to the overall structure of the protocol, and not some specific one liner issue, I am unable to give an exact solution.


[l-3]
## Summary
The event `ILOPoolCreated` in `ILOManager::initILOPool` is emitted before actually pushing new ilo pool to initializedILOPools.

## Vulnerability Details and impact
The event `ILOPoolCreated` in `ILOManager::initILOPool` is emitted before actually pushing new ilo pool to initializedILOPools. not only this but it will also emit wrong length, this length is length before the new pool is added which is not intended.

`emit ILOPoolCreated(_project.uniV3PoolAddress, iloPoolAddress, _initializedILOPools[params.uniV3Pool].length);`

and the new pool is pushed on last line after the event emission
` _initializedILOPools[params.uniV3Pool].push(iloPoolAddress);`
 
not only this, there are certain calculations too after the event is emitted if any one of them revert, we already have emitted event before that the pool is created which is problematic, This may lead to the incorrect assumption of the contract state changes when tracking off-chain.

## Tools Used
Manual review

## Recommendations
Always emit the events in the end of all.

[l-4]
##summary
`ILOPool::_unlockedLiquidity` doesnt check if vest.end > vest.start , in the case when both are equal, the else statement will revert because of division from zero.

#vulnerabilty detail and impact
`ILOPool::_unlockedLiquidity` doesnt check if vest.end > vest.start , in the case when both are equal, i.e vest.end == vest.start, the function will revert since we're dividing with zero as (vest.end - vest.start) will be zero.

`else {
                //@audit zero
                liquidityUnlocked += uint128(FullMath.mulDiv(
                    vest.shares * totalLiquidity, 
                    block.timestamp - vest.start, 
                    (vest.end - vest.start) * BPS
                ));
            }
        }`
##recommandation
employ a check which insures vest.end and vest.start are not equal


[nc-1]
## Summary
There are certain instances in code where events are emitted before actually updating the state.

## Instances
1.`ILOManager::setILOPoolImplementation`
2.`ILOManager::setDefaultDeadlineOffset`
3.`ILOManager::setRefundDeadlineForProject`

## Impact
This may lead to the incorrect assumption of the contract state changes when tracking off-chain.

## Recommendations
event emission should be in the end when the states are updated successfully

[nc-2]
## Summary
require statement in `liquidityManagement::uniswapV3MintCallback` wont revert with a message, causes hardship for users and decrease code quality

## Vulnerability detail
`    function uniswapV3MintCallback(
        uint256 amount0Owed,
        uint256 amount1Owed,
        bytes calldata data
    ) external override {
        ///@audit qa revert msg
        require(msg.sender == _cachedUniV3PoolAddress);
`

## Recommendation
```diff
-require(msg.sender == _cachedUniV3PoolAddress);
+require(msg.sender == _cachedUniV3PoolAddress, "appropriate message for revert");
```

[nc-3]
## Summary
The protocol is using block.timestamp for many calculations.

## Vulnerability details and impact
The protocol is using block.timestamp for many calculations and it is to be deployed on diffrent chains, and value of block.timestamp would be different so the protocol will behave unexpectedly. relaying on block.timestamp when we know we're deploying our protocol on different chains is not safe.

## Recommendation
Because I am unsure of how the developers want this protocol to function, I am unable to propose an effective solution to resolve this issue. Significant parts of the system need to be redone.

[nc-4]
## Summary
An event emission missing in `ILOManager`

## Vulnerability details and impact
The funtion in ILOManager doesnt emit event

` function claimRefund(address uniV3PoolAddress) external override onlyProjectAdmin(uniV3PoolAddress) returns(uint256 totalRefundAmount) {
        require(_cachedProject[uniV3PoolAddress].refundDeadline < block.timestamp, "RFT");
        address[] memory initializedPools = _initializedILOPools[uniV3PoolAddress];
        for (uint256 i = 0; i < initializedPools.length; i++) {
            totalRefundAmount += IILOPool(initializedPools[i]).claimProjectRefund(_cachedProject[uniV3PoolAddress].admin);
        }
      //@audit is any event missing  + yes, projectRefund event
    }`

protocol has a event dedicated for this funtion which is`event ProjectRefund(address indexed project, uint256 refundAmount);
` and its emission is missing here
Any functionality associated with the protocol depends on this event emission will be affected.

## Recommendation
Just add the already defined event to the function in the end.