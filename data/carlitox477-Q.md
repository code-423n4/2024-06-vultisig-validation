# Low
## `Whitelist`: anyone can be whitelisted at 0 cost from begining
Given that `_isSelfWhitelistDisabled` is set to false by default, anyone can become whitelisting at 0 cost (only gas fees) through `receive`.

To avoid this, set `_isSelfWhitelistDisabled` to true in `Whitelist` constructor.

## `ILOManager`: Sum of `PLATFORM_FEE` and `PERFORMANCE_FEE` are not capped
Contract owner can set them to any value, even sum of them can be over 100%. It is recommended to of at least 100% for the sum of them.

## `ILOManager.initILOPool(InitPoolParams)` does not check that `block.timestamp < params.start` 
This check provide a more robust input validation.

## `ILOManager` owner can front-run the `ILOManager.initILOProject(InitProjectParams)` and affect desired refundDeadline
It is recommended to add a check that `refundDeadline` is lower that one specified by function caller.

## Project admin can always avoid lunching
While refund mechanism can be triggered by any investro through refundable modifier through function `ILOPool.claimRefund(uint256)`, this is not the case for lunch, only project admin can trigger it through `ILOManager.lunchILOProject(uint256)`. This means that even if softcap is reached, project admin can still avoid lunching and refund funds.

## Use `_safeMint` instead of `_mint`
Use of `_safeMint` is recommended over `_mint` for ERC721 tokens to assure that recipient is prepared to handle the token. However, this also would introduce a reentrancy risk in `buy`, given that the hook introduced by `_safeMint` would allow to bypass `maxCapPerUser` check by reenteryong `buy`. Therefore, if `_safeMint` is used instead of `mint` also consider adding a `nonReentrant` modifier to function `ILOPool.buy(uint256,address)`

## Cliff period is not specified
In documentation it is specified that some stake holders will be enforced a cliff period, however, this is not implemented in the code. To do it, add a parameter in VestingConfig that specifiy the end of the cliff period, and consider it when a claim is done.