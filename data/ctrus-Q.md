## Summary
`Whitlist.sol::setMaxAddressCap` does'nt ensure the `new cap` provided is less than maxAddressCap. 

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