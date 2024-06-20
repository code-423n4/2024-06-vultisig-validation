## [I-1]
Anyone can front run the owner and can get added into whitelist using `Whitelist.sol:receive()` function even if the owner had their own whitelist addresses. The owner can blacklist them but it would take time and efforts.

## Recommended Mitigation Steps
make `_isSelfWhiteListDisabled = true` in the constructor of `Whitelist.sol`, so that no one can get added to whitelist when owner have enough whitelist address and can make it false later when they need more addresses.


## [I-2]
`DEFAULT_DEADLINE_OFFSET` is the deadline before which no one should be able to claim refund but In `ILOManager.sol::initILOPool` function we are not checking if `params.launch > block.timestamp` or not, without this checking admins can initalized a ILOPool with `params.launchTime` less than block.timestamp, means they can also claim refund before the expected `DEFAULT_DEADLINE_OFFSET` set by owner

## Recommended Mitigation Steps
```diff
function initILOPool(InitPoolParams calldata params)
        external
        override
        onlyProjectAdmin(params.uniV3Pool)
        returns (address iloPoolAddress)
    {
.
.
.
-     require(params.start < params.end && params.end < _project.launchTime, "PT");
+     require(params.launchTime >= block.timestamp && params.start < params.end && params.end < _project.launchTime, "PT");
```