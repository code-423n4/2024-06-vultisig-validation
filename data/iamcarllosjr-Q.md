# `totalSold` in `ILOPool.sol::buy` will always be 2.5x the value of `totalRaised` !

**Description** 
In `ILOPool.sol::buy` function, is made to check the value of `totalSold` : `require(totalSold() <= saleInfo.maxSaleAmount, "SA");`
, where it should round the value up, but it turns out that the value will always be 2.5x the value stored in `totalRaised`.

```javascript
function totalSold() public view override returns (uint256 _totalSold) {
        (_totalSold,) =_saleAmountNeeded(totalRaised);
    }
``` 

**Impact**
For project participants, this discrepancy can create confusion or a lack of transparency about the actual financial status of the contract. It is important that users have a clear understanding of how values are calculated and reported.

Depending on the applicable regulations, this practice may violate accounting or tax compliance standards, as it may suggest that the contract is carrying out commercial activities without proper financial compensation.

**Proof of Concept** 
Add this part of code in `testBuy()` in `ILOPool.t.sol`

```javascript
uint256 totalRaised = IILOPool(iloPool).totalSold();
uint256 totalRaisedScaled = 250 * liquidity / 100; // liquidity or totalRaised x 2.5
assertEq(totalRaised, totalRaisedScaled);
console.log("totalRaised RoundUp", totalRaised);
// logs : "totalRaised RoundUp" = liquidity or totalRaised x 2.5
```

**Recommend Mitigation**
To mitigate these impacts, it is recommended to carefully review the liquidity calculation and token sale functions to ensure that they correctly reflect the project's intentions and comply with all legal and ethical obligations.