## Missing _disableInitializers() in the constructor of ILOManager.sol 

## Impact
Contract implementation could be initialized when this should not be possible.

## PoC

For example in the OZ documentation can be found similar pattern with recommendations.

1. https://docs.openzeppelin.com/contracts/4.x/api/proxy#Initializable-_disableInitializers--

2. https://docs.openzeppelin.com/upgrades-plugins/1.x/writing-upgradeable#initializing_the_implementation_contract

## Recommendation
Add _disableInitializers() in the constructor of ILOManager.sol as it is in ILOPool.sol.