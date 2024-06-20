Note:
  This report includes additional instances of an issue listed in the automated findings report.

## Gas Optimizations

| |Issue|Instances| Gas Savings
|-|:-|:-:|:-:|
| [[G-01](#g-01)] | Argument validation should be at the top of the function/block | 24| 0|
| [[G-02](#g-02)] | Use `Array.unsafeAccess()` to avoid repeated array length checks | 12| 25200|
| [[G-03](#g-03)] | Avoid fetching a low-level call's return data by using assembly | 4| 636|
| [[G-04](#g-04)] | Avoid updating storage when the value hasn't changed | 3| 2400|
| [[G-05](#g-05)] | Avoid zero transfer to save gas | 10| 1000|
| [[G-06](#g-06)] | Cache array length outside of loop | 12| 1164|
| [[G-07](#g-07)] | Use `calldata` instead of `memory` for immutable arguments | 2| 3000|
| [[G-08](#g-08)] | Constructors can be marked as `payable` to save deployment gas | 5| 105|
| [[G-09](#g-09)] | Use custom errors rather than `revert()/require()` strings to save gas | 43| 2150|
| [[G-10](#g-10)] | `do-while` is cheaper than `for`-loops when the initial check can be skipped | 11| 0|
| [[G-11](#g-11)] | Duplicated `require()`/`revert()` checks should be refactored to a modifier or function to save deployment gas | 4| 0|
| [[G-12](#g-12)] | Avoid emitting event on every iteration | 1| 375|
| [[G-13](#g-13)] | It is a waste of GAS to emit variable literals | 3| 24|
| [[G-14](#g-14)] | Consider using `ERC721A` over `ERC721` | 1| 0|
| [[G-15](#g-15)] | Counting down in `for` statements is more gas efficient | 12| 96|
| [[G-16](#g-16)] | Function names can be optimized | 22| 2816|
| [[G-17](#g-17)] | Don't initialize variables with default value | 12| 0|
| [[G-18](#g-18)] | Optimize Deployment Size by Fine-tuning IPFS Hash | 22| 33308|
| [[G-19](#g-19)] | Use assembly hashing | 1| 80|
| [[G-20](#g-20)] | Use local variables for emitting | 3| 288|
| [[G-21](#g-21)] | State variable read in a loop | 1| 97|
| [[G-22](#g-22)] | use assembly for Low-Level Calls' Return Data | 4| 636|
| [[G-23](#g-23)] | Merge events to save gas | 5| 1875|
| [[G-24](#g-24)] | Inline modifiers used only once | 1| 0|
| [[G-25](#g-25)] | Multiple accesses of the same mapping/array key/index should be cached | 10| 420|
| [[G-26](#g-26)] | Multiple mappings can be replaced with a single struct mapping | 5| 210|
| [[G-27](#g-27)] | State variables should be cached in stack variables rather than re-reading them from storage | 10| 1067|
| [[G-28](#g-28)] | Use Only Named Returns | 24| 1056|
| [[G-29](#g-29)] | Nested for loops should be avoided due to high gas costs resulting from O^2 time complexity | 1| 0|
| [[G-30](#g-30)] | Nesting `if`-statements is cheaper than using `&&` | 3| 12|
| [[G-31](#g-31)] | Shorten the array rather than copying to a new one | 2| 0|
| [[G-32](#g-32)] | Expression ('') is cheaper than new bytes(0) | 1| 259|
| [[G-33](#g-33)] | Only emit event in setter function if the state variable was changed | 2| 0|
| [[G-34](#g-34)] | Operator `>=`/`<=` costs less gas than operator `>`/`<` | 45| 135|
| [[G-35](#g-35)] | Functions that revert when called by normal users can be marked as `payable` | 26| 650|
| [[G-36](#g-36)] | Using `++i/--i` instead of `i++/i--` can save gas | 16| 80|
| [[G-37](#g-37)] | Using `private` for constants saves gas | 8| 27248|
| [[G-38](#g-38)] | Refactor modifiers to call a local function | 8| 8000|
| [[G-39](#g-39)] | Use assembly scratch space for building calldata for external calls | 40| 8800|
| [[G-40](#g-40)] | Use shift right/left instead of division if possible | 5| 0|
| [[G-41](#g-41)] | Usage of smaller `uint`/`int` types causes overhead | 92| 5060|
| [[G-42](#g-42)] | Consider using solady's 'FixedPointMathLib' | 39| 0|
| [[G-43](#g-43)] | Newer versions of solidity are more gas efficient | 26| 0|
| [[G-44](#g-44)] | Splitting `require()` statements that use `&&` saves gas | 8| 24|
| [[G-45](#g-45)] | `address(this)` can be stored in state variable that will ultimately cost less, than every time calculating this, specifically when it used multiple times in a contract | 12| 0|
| [[G-46](#g-46)] | Stack variable cost less than state variables while used in emiting event | 5| 45|
| [[G-47](#g-47)] | Mappings are cheaper to use than storage arrays | 1| 2100|
| [[G-48](#g-48)] | Gas savings can be achieved by changing the model for assigning value to the structure | 2| 260|
| [[G-49](#g-49)] | Optimize Storage with Byte Truncation for Time Related State Variables | 4| 8000|
| [[G-50](#g-50)] | Trade-offs Between Modifiers and Internal Functions | 40| 420000|
| [[G-51](#g-51)] | Use `uint256(1)`/`uint256(2)` instead of `true`/`false` to save gas for changes | 7| 119700|
| [[G-52](#g-52)] | Divisions can be `unchecked` to save gas | 5| 100|
| [[G-53](#g-53)] | Increments can be `unchecked` to save gas | 11| 330|
| [[G-54](#g-54)] | Avoid unnecessary public variables | 18| 396000|
| [[G-55](#g-55)] | Use `!= 0` instead of `> 0` for unsigned integer comparison | 10| 40|
| [[G-56](#g-56)] | Unused non-constant state variables waste gas | 11| 220000|
| [[G-57](#g-57)] | Using assembly to check for `address(0)` can save gas | 6| 36|
| [[G-58](#g-58)] | Use assembly to `emit` events | 19| 722|
| [[G-59](#g-59)] | Use assembly to validate `msg.sender` | 5| 60|
| [[G-60](#g-60)] | Simple checks for zero can be done using assembly to save gas | 48| 48|
| [[G-61](#g-61)] | Use assembly in place of `abi.decode` to extract calldata values more efficiently | 4| 0|
| [[G-62](#g-62)] | Use `byte32` in place of `string` | 4| 0|
| [[G-63](#g-63)] | `internal` functions not called by the contract should be removed to save deployment gas | 26| 0|
| [[G-64](#g-64)] | Use `x = x + y` instead of `x += y` for state variables | 3| 30|
| [[G-65](#g-65)] | Use solady library where possible to save gas | 9| 9000|
| [[G-66](#g-66)] | Using bools for `storage` incurs overhead | 6| 600|
| [[G-67](#g-67)] | Variable declared within iteration | 8| 0|
| [[G-68](#g-68)] | Enable IR-based code generation | 22| 0|
| [[G-69](#g-69)] | WETH address definition can be use directly | 5| 0|
| [[G-70](#g-70)] | Using XOR (^) and AND (&) bitwise equivalents for gas optimizations | 28| 0|
| [[G-71](#g-71)] | Don't use `_msgSender()` if not supporting EIP-2771 | 5| 80|

Total: 871 instances over 71 issues with an estimate of 1305422 gas saved.

## Gas Optimizations

### [G-01]<a name="g-01"></a> Argument validation should be at the top of the function/block

Checks that involve function arguments should come before checks that involve state variables, function calls, and calculations. By doing these checks first, the function is able to revert before wasting a Gcoldsload (2100 gas*) in a function that may ultimately revert in the unhappy case.

*There are 24 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/Whitelist.sol

212:             if (_isBlacklisted[to]) {

216:             if (_allowedWhitelistIndex == 0 || _whitelistIndex[to] > _allowedWhitelistIndex) {

222:             if (_contributed[to] + estimatedETHAmount > _maxAddressCap) {

```


*GitHub* : [212](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L212-L212), [216](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L216-L216), [222](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L222-L222)

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/FullMath.sol

30:             require(denominator > 0);

39:         require(denominator > prod1);

111:         if (mulmod(a, b, denominator) > 0) {

```


*GitHub* : [30](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/FullMath.sol#L30-L30), [39](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/FullMath.sol#L39-L39), [111](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/FullMath.sol#L111-L111)

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol

27:         if (tickCumulativesDelta < 0 && (tickCumulativesDelta % int56(uint56(period)) != 0)) timeWeightedAverageTick--;

```


*GitHub* : [27](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol#L27-L27)

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol

48:         if (tick > 0) ratio = type(uint256).max / ratio;

```


*GitHub* : [48](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L48-L48)

```solidity
📁 File: src/ILOManager.sol

77:             require(params.start < params.end && params.end < _project.launchTime, "PT");

119:                 require(sqrtPriceX96Existing == sqrtPriceX96, "UV3P");

190:         require(_cachedProject[uniV3PoolAddress].initialPoolPriceX96 == sqrtPriceX96, "UV3P");

```


*GitHub* : [77](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L77-L77), [119](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L119-L119), [190](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L190-L190)

```solidity
📁 File: src/ILOPool.sol

136:         require(saleInfo.hardCap - totalRaised >= raiseAmount, "HC");

143:         if (balanceOf(recipient) == 0) {

151:         require(raiseAmount <= saleInfo.maxCapPerUser - _position.raiseAmount, "UC");

```


*GitHub* : [136](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L136-L136), [143](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L143-L143), [151](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L151-L151)

```solidity
📁 File: src/base/ILOVest.sol

22:                 require (vestingConfigs[i].recipient == address(0), "VR");

24:                 require(vestingConfigs[i].recipient != address(0), "VR");

27:             require(BPS - totalShares >= vestingConfigs[i].shares, "TS");

43:             require(schedule[i].start >= lastEnd, "VT");

46:             require(BPS - totalShares >= schedule[i].shares, "VS");

```


*GitHub* : [22](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L22-L22), [24](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L24-L24), [27](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L27-L27), [43](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L43-L43), [46](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L46-L46)

```solidity
📁 File: src/base/LiquidityManagement.sol

27:         if (amount0Owed > 0) pay(_cachedPoolKey.token0, address(this), msg.sender, amount0Owed);

28:         if (amount1Owed > 0) pay(_cachedPoolKey.token1, address(this), msg.sender, amount1Owed);

56:         require(amount0 >= params.amount0Min && amount1 >= params.amount1Min, 'Price slippage check');

```


*GitHub* : [27](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/LiquidityManagement.sol#L27-L27), [28](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/LiquidityManagement.sol#L28-L28), [56](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/LiquidityManagement.sol#L56-L56)

```solidity
📁 File: src/base/PeripheryPayments.sol

31:         } else if (payer == address(this)) {

```


*GitHub* : [31](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/PeripheryPayments.sol#L31-L31)

```solidity
📁 File: src/libraries/SqrtPriceMathPartial.sol

31:         require(sqrtRatioAX96 > 0);

```


*GitHub* : [31](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/SqrtPriceMathPartial.sol#L31-L31)

### [G-02]<a name="g-02"></a> Use `Array.unsafeAccess()` to avoid repeated array length checks

When using storage arrays, solidity adds an internal lookup of the array's length (a Gcoldsload **2100 gas**) to ensure you don't read past the array's end. You can avoid this lookup by using [Array.unsafeAccess()](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/94697be8a3f0dfcd95dfb13ffbd39b5973f5c65d/contracts/utils/Arrays.sol#L57) in cases where the length has already been checked, as is the case with the instances below

*There are 12 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/Whitelist.sol

192:         for (uint i = 0; i < whitelisted.length; i++) {

```


*GitHub* : [192](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L192-L192)

```solidity
📁 File: src/ILOManager.sol

193:         for (uint256 i = 0; i < initializedPools.length; i++) {

204:         for (uint256 i = 0; i < initializedPools.length; i++) {

```


*GitHub* : [193](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L193-L193), [204](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L204-L204)

```solidity
📁 File: src/ILOPool.sol

92:         for (uint256 index = 0; index < params.vestingConfigs.length; index++) {

311:         for (uint256 index = 1; index < _vestingConfigs.length; index++) {

324:             for (uint256 i = 0; i < projectConfig.schedule.length; i++) {

405:         for (uint256 index = 0; index < vestingSchedule.length; index++) {

```


*GitHub* : [92](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L92-L92), [311](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L311-L311), [324](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L324-L324), [405](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L405-L405)

```solidity
📁 File: src/base/ILOVest.sol

20:         for (uint256 i = 0; i < vestingConfigs.length; i++) {

```


*GitHub* : [20](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L20-L20)

```solidity
📁 File: src/base/ILOWhitelist.sol

28:         for (uint256 i = 0; i < users.length; i++) {

35:         for (uint256 i = 0; i < users.length; i++) {

```


*GitHub* : [28](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOWhitelist.sol#L28-L28), [35](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOWhitelist.sol#L35-L35)

```solidity
📁 File: src/base/Multicall.sol

13:         for (uint256 i = 0; i < data.length; i++) {

18:                 if (result.length < 68) revert();

```


*GitHub* : [13](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/Multicall.sol#L13-L13), [18](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/Multicall.sol#L18-L18)

### [G-03]<a name="g-03"></a> Avoid fetching a low-level call's return data by using assembly

Even if you don't assign the call's second return value, it still gets copied to memory. Use assembly instead to prevent this and save **159** [gas](https://gist.github.com/IllIllI000/0e18a40f3afb0b83f9a347b10ee89ad2):
`(bool success,) = payable(receiver).call{gas: gas, value: value}(''); -> bool success; assembly { success := call(gas, receiver, value, 0, 0, 0, 0) }`

*There are 4 instance(s) of this issue:*

```solidity
📁 File: src/libraries/TransferHelper.sol

20:             token.call(abi.encodeWithSelector(IERC20.transferFrom.selector, from, to, value));

34:         (bool success, bytes memory data) = token.call(abi.encodeWithSelector(IERC20.transfer.selector, to, value));

48:         (bool success, bytes memory data) = token.call(abi.encodeWithSelector(IERC20.approve.selector, to, value));

57:         (bool success, ) = to.call{value: value}(new bytes(0));

```


*GitHub* : [20](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/TransferHelper.sol#L20-L20), [34](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/TransferHelper.sol#L34-L34), [48](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/TransferHelper.sol#L48-L48), [57](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/TransferHelper.sol#L57-L57)

### [G-04]<a name="g-04"></a> Avoid updating storage when the value hasn't changed

If the old value is equal to the new value, not re-storing the value will avoid a Gsreset (**2900 gas**), potentially at the expense of a Gcoldsload (**2100 gas**) or a Gwarmaccess (**100 gas**)

*There are 3 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol

28:         pool = _pool;

29:         baseToken = _baseToken;

30:         WETH = _WETH;

```


*GitHub* : [28](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol#L28-L28), [29](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol#L29-L29), [30](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol#L30-L30)

### [G-05]<a name="g-05"></a> Avoid zero transfer to save gas

In Solidity, unnecessary operations can waste gas. For example, a transfer function without a zero amount check uses gas even if called with a zero amount, since the contract state remains unchanged. Implementing a zero amount check avoids these unnecessary function calls, saving gas and improving efficiency.

*There are 10 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/extensions/VultisigWhitelisted.sol

32:         super._beforeTokenTransfer(from, to, amount);

```


*GitHub* : [32](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/extensions/VultisigWhitelisted.sol#L32-L32)

```solidity
📁 File: src/ILOPool.sol

173:         TransferHelper.safeTransferFrom(RAISE_TOKEN, msg.sender, address(this), raiseAmount);

252:         TransferHelper.safeTransfer(_cachedPoolKey.token0, ownerOf(tokenId), amount0);

253:         TransferHelper.safeTransfer(_cachedPoolKey.token1, ownerOf(tokenId), amount1);

259:         TransferHelper.safeTransfer(_cachedPoolKey.token0, feeTaker, amountCollected0-amount0);

260:         TransferHelper.safeTransfer(_cachedPoolKey.token1, feeTaker, amountCollected1-amount1);

358:         TransferHelper.safeTransfer(RAISE_TOKEN, tokenOwner, refundAmount);

```


*GitHub* : [173](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L173-L173), [252](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L252-L252), [253](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L253-L253), [259](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L259-L259), [260](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L260-L260), [358](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L358-L358)

```solidity
📁 File: src/base/PeripheryPayments.sol

30:             IWETH9(WETH9).transfer(recipient, value);

33:             TransferHelper.safeTransfer(token, recipient, value);

36:             TransferHelper.safeTransferFrom(token, payer, recipient, value);

```


*GitHub* : [30](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/PeripheryPayments.sol#L30-L30), [33](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/PeripheryPayments.sol#L33-L33), [36](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/PeripheryPayments.sol#L36-L36)

### [G-06]<a name="g-06"></a> Cache array length outside of loop

If not cached, the solidity compiler will always read the length of the array during each iteration. That is, if it is a storage array, this is an extra sload operation (100 additional extra gas for each iteration except for the first) and if it is a memory array, this is an extra mload operation (3 additional gas for each iteration except for the first).

*There are 12 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/Whitelist.sol

192:         for (uint i = 0; i < whitelisted.length; i++) {

```


*GitHub* : [192](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L192-L192)

```solidity
📁 File: src/ILOManager.sol

193:         for (uint256 i = 0; i < initializedPools.length; i++) {

204:         for (uint256 i = 0; i < initializedPools.length; i++) {

```


*GitHub* : [193](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L193-L193), [204](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L204-L204)

```solidity
📁 File: src/ILOPool.sol

92:         for (uint256 index = 0; index < params.vestingConfigs.length; index++) {

311:         for (uint256 index = 1; index < _vestingConfigs.length; index++) {

324:             for (uint256 i = 0; i < projectConfig.schedule.length; i++) {

405:         for (uint256 index = 0; index < vestingSchedule.length; index++) {

```


*GitHub* : [92](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L92-L92), [311](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L311-L311), [324](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L324-L324), [405](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L405-L405)

```solidity
📁 File: src/base/ILOVest.sol

20:         for (uint256 i = 0; i < vestingConfigs.length; i++) {

```


*GitHub* : [20](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L20-L20)

```solidity
📁 File: src/base/ILOWhitelist.sol

28:         for (uint256 i = 0; i < users.length; i++) {

35:         for (uint256 i = 0; i < users.length; i++) {

```


*GitHub* : [28](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOWhitelist.sol#L28-L28), [35](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOWhitelist.sol#L35-L35)

```solidity
📁 File: src/base/Multicall.sol

13:         for (uint256 i = 0; i < data.length; i++) {

18:                 if (result.length < 68) revert();

```


*GitHub* : [13](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/Multicall.sol#L13-L13), [18](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/Multicall.sol#L18-L18)

### [G-07]<a name="g-07"></a> Use `calldata` instead of `memory` for immutable arguments

Mark data types as `calldata` instead of `memory` where possible. This makes it so that the data is not automatically loaded into memory. If the data passed into the function does not need to be changed (like updating values in an array), it can be passed in as `calldata`. The one exception to this is if the argument must later be passed into another function that takes an argument that specifies `memory` storage.

*There are 2 instance(s) of this issue:*

```solidity
📁 File: src/base/ILOVest.sol

// @audit  vestingConfigs
17:     function _validateSharesAndVests(uint64 launchTime, VestingConfig[] memory vestingConfigs) internal pure {

// @audit  schedule
35:     function _validateVestSchedule(uint64 launchTime, LinearVest[] memory schedule) internal pure {

```


*GitHub* : [17](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L17-L17), [35](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L35-L35)

### [G-08]<a name="g-08"></a> Constructors can be marked as `payable` to save deployment gas

`payable` functions cost less gas to execute, because the compiler does not have to add extra checks to ensure that no payment is provided. A constructor can be safely marked as payable, because only the deployer would be able to pass funds, and the project itself would not pass any funds.

*There are 5 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/Vultisig.sol

12:     constructor() ERC20("Vultisig Token", "VULT") {

```


*GitHub* : [12](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Vultisig.sol#L12-L12)

```solidity
📁 File: hardhat-vultisig/contracts/Whitelist.sol

48:     constructor() {

```


*GitHub* : [48](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L48-L48)

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol

27:     constructor(address _pool, address _baseToken, address _WETH) {

```


*GitHub* : [27](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol#L27-L27)

```solidity
📁 File: src/ILOManager.sol

29:     constructor () {

```


*GitHub* : [29](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L29-L29)

```solidity
📁 File: src/ILOPool.sol

49:     constructor() ERC721('', '') {

```


*GitHub* : [49](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L49-L49)

### [G-09]<a name="g-09"></a> Use custom errors rather than `revert()/require()` strings to save gas

Custom errors are available from solidity version 0.8.4. Custom errors save [~50 gas](https://gist.github.com/IllIllI000/ad1bd0d29a0101b25e57c293b4b0c746) each time they're hit by [avoiding having to allocate and store the revert string](https://soliditylang.org/blog/2021/04/21/custom-errors/#errors-in-depth). Not defining the strings also save deployment gas.

*There are 43 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol

15:         require(period != 0, "BP");

63:         require(observationCardinality > 0, "NI");

```


*GitHub* : [15](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol#L15-L15), [63](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol#L63-L63)

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol

25:         require(absTick <= uint256(uint24(MAX_TICK)), "T");

63:         require(sqrtPriceX96 >= MIN_SQRT_RATIO && sqrtPriceX96 < MAX_SQRT_RATIO, "R");

```


*GitHub* : [25](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L25-L25), [63](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L63-L63)

```solidity
📁 File: src/ILOManager.sol

52:         require(_cachedProject[uniV3Pool].admin == msg.sender, "UA");

75:             require(_project.uniV3PoolAddress != address(0), "NI");

77:             require(params.start < params.end && params.end < _project.launchTime, "PT");

90:         require(sqrtRatioLowerX96 < _project.initialPoolPriceX96 && sqrtRatioLowerX96 < sqrtRatioUpperX96, "RANGE");

119:                 require(sqrtPriceX96Existing == sqrtPriceX96, "UV3P");

134:         require(_project.uniV3PoolAddress == address(0), "RE");

188:         require(block.timestamp > _cachedProject[uniV3PoolAddress].launchTime, "LT");

190:         require(_cachedProject[uniV3PoolAddress].initialPoolPriceX96 == sqrtPriceX96, "UV3P");

192:         require(initializedPools.length > 0, "NP");

202:         require(_cachedProject[uniV3PoolAddress].refundDeadline < block.timestamp, "RFT");

```


*GitHub* : [52](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L52-L52), [75](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L75-L75), [77](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L77-L77), [90](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L90-L90), [119](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L119-L119), [134](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L134-L134), [188](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L188-L188), [190](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L190-L190), [192](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L192-L192), [202](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L202-L202)

```solidity
📁 File: src/ILOPool.sol

133:         require(_isWhitelisted(recipient), "UA");

134:         require(block.timestamp > saleInfo.start && block.timestamp < saleInfo.end, "ST");

136:         require(saleInfo.hardCap - totalRaised >= raiseAmount, "HC");

139:         require(totalSold() <= saleInfo.maxSaleAmount, "SA");

151:         require(raiseAmount <= saleInfo.maxCapPerUser - _position.raiseAmount, "UC");

161:         require(liquidityDelta > 0, "ZA");

179:         require(_isApprovedOrOwner(msg.sender, tokenId), 'UA');

192:         require(_launchSucceeded, "PNL");

264:         require(msg.sender == MANAGER, "UA");

270:         require(!_launchSucceeded, "PL");

272:         require(!_refundTriggered, "IRF");

274:         require(totalRaised >= saleInfo.softCap, "SC");

340:             require(!_launchSucceeded, "PL");

342:             require(block.timestamp >= _project.refundDeadline, "RFT");

465:         require(msg.sender == _project.admin, "UA");

```


*GitHub* : [133](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L133-L133), [134](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L134-L134), [136](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L136-L136), [139](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L139-L139), [151](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L151-L151), [161](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L161-L161), [179](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L179-L179), [192](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L192-L192), [264](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L264-L264), [270](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L270-L270), [272](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L272-L272), [274](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L274-L274), [340](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L340-L340), [342](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L342-L342), [465](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L465-L465)

```solidity
📁 File: src/base/ILOVest.sol

22:                 require (vestingConfigs[i].recipient == address(0), "VR");

24:                 require(vestingConfigs[i].recipient != address(0), "VR");

27:             require(BPS - totalShares >= vestingConfigs[i].shares, "TS");

32:         require(totalShares == BPS, "TS");

36:         require(schedule[0].start >= launchTime, "VT");

43:             require(schedule[i].start >= lastEnd, "VT");

46:             require(BPS - totalShares >= schedule[i].shares, "VS");

50:         require(totalShares == BPS, "VS");

```


*GitHub* : [22](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L22-L22), [24](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L24-L24), [27](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L27-L27), [32](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L32-L32), [36](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L36-L36), [43](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L43-L43), [46](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L46-L46), [50](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L50-L50)

```solidity
📁 File: src/base/LiquidityManagement.sol

56:         require(amount0 >= params.amount0Min && amount1 >= params.amount1Min, 'Price slippage check');

```


*GitHub* : [56](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/LiquidityManagement.sol#L56-L56)

```solidity
📁 File: src/base/PeripheryPayments.sol

14:         require(msg.sender == WETH9, 'Not WETH9');

```


*GitHub* : [14](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/PeripheryPayments.sol#L14-L14)

```solidity
📁 File: src/libraries/TransferHelper.sol

21:         require(success && (data.length == 0 || abi.decode(data, (bool))), 'STF');

35:         require(success && (data.length == 0 || abi.decode(data, (bool))), 'ST');

49:         require(success && (data.length == 0 || abi.decode(data, (bool))), 'SA');

58:         require(success, 'STE');

```


*GitHub* : [21](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/TransferHelper.sol#L21-L21), [35](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/TransferHelper.sol#L35-L35), [49](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/TransferHelper.sol#L49-L49), [58](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/TransferHelper.sol#L58-L58)

### [G-10]<a name="g-10"></a> `do-while` is cheaper than `for`-loops when the initial check can be skipped

`for (uint256 i; i < len; ++i){ ... }` -> `do { ...; ++i } while (i < len);`

*There are 11 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/Whitelist.sol

192:         for (uint i = 0; i < whitelisted.length; i++) {

```


*GitHub* : [192](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L192-L192)

```solidity
📁 File: src/ILOManager.sol

193:         for (uint256 i = 0; i < initializedPools.length; i++) {

204:         for (uint256 i = 0; i < initializedPools.length; i++) {

```


*GitHub* : [193](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L193-L193), [204](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L204-L204)

```solidity
📁 File: src/ILOPool.sol

92:         for (uint256 index = 0; index < params.vestingConfigs.length; index++) {

324:             for (uint256 i = 0; i < projectConfig.schedule.length; i++) {

405:         for (uint256 index = 0; index < vestingSchedule.length; index++) {

```


*GitHub* : [92](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L92-L92), [324](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L324-L324), [405](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L405-L405)

```solidity
📁 File: src/base/ILOVest.sol

20:         for (uint256 i = 0; i < vestingConfigs.length; i++) {

41:         for (uint256 i = 0; i < scheduleLength; i++) {

```


*GitHub* : [20](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L20-L20), [41](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L41-L41)

```solidity
📁 File: src/base/ILOWhitelist.sol

28:         for (uint256 i = 0; i < users.length; i++) {

35:         for (uint256 i = 0; i < users.length; i++) {

```


*GitHub* : [28](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOWhitelist.sol#L28-L28), [35](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOWhitelist.sol#L35-L35)

```solidity
📁 File: src/base/Multicall.sol

13:         for (uint256 i = 0; i < data.length; i++) {

```


*GitHub* : [13](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/Multicall.sol#L13-L13)

### [G-11]<a name="g-11"></a> Duplicated `require()`/`revert()` checks should be refactored to a modifier or function to save deployment gas

This will cost more runtime gas, but will reduce deployment gas when the function is (optionally called via a modifier) called more than once as is the case for the examples below. Most projects do not make this trade-off, but it's available nonetheless.

*There are 4 instance(s) of this issue:*

```solidity
📁 File: src/ILOPool.sol

270:         require(!_launchSucceeded, "PL");

340:             require(!_launchSucceeded, "PL");

```


*GitHub* : [270](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L270-L270), [340](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L340-L340)

```solidity
📁 File: src/base/ILOVest.sol

32:         require(totalShares == BPS, "TS");

50:         require(totalShares == BPS, "VS");

```


*GitHub* : [32](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L32-L32), [50](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L50-L50)

### [G-12]<a name="g-12"></a> Avoid emitting event on every iteration

Emitting an event has an overhead of **375 gas**, which will be incurred on every iteration of the loop. It is cheaper to `emit` only [once](https://github.com/ethereum/EIPs/blob/adad5968fd6de29902174e0cb51c8fc3dceb9ab5/EIPS/eip-1155.md?plain=1#L68) after the loop has finished.

*There are 1 instance(s) of this issue:*

```solidity
📁 File: src/ILOPool.sol

328:             emit Buy(projectConfig.recipient, tokenId, 0, liquidityShares);

```


*GitHub* : [328](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L328-L328)

### [G-13]<a name="g-13"></a> It is a waste of GAS to emit variable literals

Emitting variable literals (`true`, `false`, `'hello'`, `1` etc...) in events is inefficient, as it consumes extra gas without providing added value. These literals are fixed values that can be accessed or hardcoded elsewhere in the smart contract or application, making their inclusion in events redundant and an unnecessary drain on resources during transaction execution.

*There are 3 instance(s) of this issue:*

```solidity
📁 File: src/ILOPool.sol

328:             emit Buy(projectConfig.recipient, tokenId, 0, liquidityShares);

```


*GitHub* : [328](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L328-L328)

```solidity
📁 File: src/base/ILOWhitelist.sol

49:         emit SetWhitelist(user, false);

54:         emit SetWhitelist(user, true);

```


*GitHub* : [49](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOWhitelist.sol#L49-L49), [54](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOWhitelist.sol#L54-L54)

### [G-14]<a name="g-14"></a> Consider using `ERC721A` over `ERC721`

[ERC721A](https://www.azuki.com/erc721a) is much more gas-efficient for minting multiple NFTs in the same transaction

*There are 1 instance(s) of this issue:*

```solidity
📁 File: src/ILOPool.sol

25:     ERC721,

```


*GitHub* : [25](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L25-L25)

### [G-15]<a name="g-15"></a> Counting down in `for` statements is more gas efficient

Counting down is more gas efficient than counting up because neither we are making zero variable to non-zero variable and also we will get gas refund in the last transaction when making non-zero to zero variable. [More info](https://solodit.xyz/issues/g-02-counting-down-in-for-statements-is-more-gas-efficient-code4rena-pooltogether-pooltogether-git)

*There are 12 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/Whitelist.sol

192:         for (uint i = 0; i < whitelisted.length; i++) {

```


*GitHub* : [192](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L192-L192)

```solidity
📁 File: src/ILOManager.sol

193:         for (uint256 i = 0; i < initializedPools.length; i++) {

204:         for (uint256 i = 0; i < initializedPools.length; i++) {

```


*GitHub* : [193](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L193-L193), [204](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L204-L204)

```solidity
📁 File: src/ILOPool.sol

92:         for (uint256 index = 0; index < params.vestingConfigs.length; index++) {

311:         for (uint256 index = 1; index < _vestingConfigs.length; index++) {

324:             for (uint256 i = 0; i < projectConfig.schedule.length; i++) {

405:         for (uint256 index = 0; index < vestingSchedule.length; index++) {

```


*GitHub* : [92](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L92-L92), [311](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L311-L311), [324](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L324-L324), [405](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L405-L405)

```solidity
📁 File: src/base/ILOVest.sol

20:         for (uint256 i = 0; i < vestingConfigs.length; i++) {

41:         for (uint256 i = 0; i < scheduleLength; i++) {

```


*GitHub* : [20](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L20-L20), [41](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L41-L41)

```solidity
📁 File: src/base/ILOWhitelist.sol

28:         for (uint256 i = 0; i < users.length; i++) {

35:         for (uint256 i = 0; i < users.length; i++) {

```


*GitHub* : [28](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOWhitelist.sol#L28-L28), [35](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOWhitelist.sol#L35-L35)

```solidity
📁 File: src/base/Multicall.sol

13:         for (uint256 i = 0; i < data.length; i++) {

```


*GitHub* : [13](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/Multicall.sol#L13-L13)

### [G-16]<a name="g-16"></a> Function names can be optimized

Function that are `public`/`external` and public state variable names can be optimized to save gas.

Method IDs that have two leading zero bytes can save **128 gas** each during deployment, and renaming functions to have lower method IDs will save **22 gas** per call, per sorted position shifted. [Reference](https://blog.emn178.cc/en/post/solidity-gas-optimization-function-name/)

*There are 22 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/Vultisig.sol

11: contract Vultisig is ERC20, Ownable {

```


*GitHub* : [11](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Vultisig.sol#L11-L11)

```solidity
📁 File: hardhat-vultisig/contracts/Whitelist.sol

16: contract Whitelist is Ownable {

```


*GitHub* : [16](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L16-L16)

```solidity
📁 File: hardhat-vultisig/contracts/extensions/VultisigWhitelisted.sol

12: contract VultisigWhitelisted is Vultisig {

```


*GitHub* : [12](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/extensions/VultisigWhitelisted.sol#L12-L12)

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol

14: contract UniswapV3Oracle is IOracle {

```


*GitHub* : [14](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol#L14-L14)

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/FullMath.sol

7: library FullMath {

```


*GitHub* : [7](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/FullMath.sol#L7-L7)

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol

9: library OracleLibrary {

```


*GitHub* : [9](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol#L9-L9)

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol

7: library TickMath {

```


*GitHub* : [7](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L7-L7)

```solidity
📁 File: src/ILOManager.sol

15: contract ILOManager is IILOManager, Ownable, Initializable {

```


*GitHub* : [15](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L15-L15)

```solidity
📁 File: src/ILOPool.sol

24: contract ILOPool is

```


*GitHub* : [24](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L24-L24)

```solidity
📁 File: src/base/ILOPoolImmutableState.sol

9: abstract contract ILOPoolImmutableState is IILOPoolImmutableState {

```


*GitHub* : [9](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOPoolImmutableState.sol#L9-L9)

```solidity
📁 File: src/base/ILOVest.sol

7: abstract contract ILOVest is IILOVest {

```


*GitHub* : [7](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L7-L7)

```solidity
📁 File: src/base/ILOWhitelist.sol

8: abstract contract ILOWhitelist is IILOWhitelist {

```


*GitHub* : [8](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOWhitelist.sol#L8-L8)

```solidity
📁 File: src/base/Initializable.sol

5: abstract contract Initializable {

```


*GitHub* : [5](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/Initializable.sol#L5-L5)

```solidity
📁 File: src/base/LiquidityManagement.sol

17: abstract contract LiquidityManagement is IUniswapV3MintCallback, ILOPoolImmutableState, PeripheryPayments {

```


*GitHub* : [17](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/LiquidityManagement.sol#L17-L17)

```solidity
📁 File: src/base/Multicall.sol

9: abstract contract Multicall is IMulticall {

```


*GitHub* : [9](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/Multicall.sol#L9-L9)

```solidity
📁 File: src/base/PeripheryPayments.sol

12: abstract contract PeripheryPayments is ILOPoolImmutableState {

```


*GitHub* : [12](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/PeripheryPayments.sol#L12-L12)

```solidity
📁 File: src/libraries/ChainId.sol

5: library ChainId {

```


*GitHub* : [5](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/ChainId.sol#L5-L5)

```solidity
📁 File: src/libraries/LiquidityAmounts.sol

10: library LiquidityAmounts {

```


*GitHub* : [10](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/LiquidityAmounts.sol#L10-L10)

```solidity
📁 File: src/libraries/PoolAddress.sol

5: library PoolAddress {

```


*GitHub* : [5](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/PoolAddress.sol#L5-L5)

```solidity
📁 File: src/libraries/PositionKey.sol

4: library PositionKey {

```


*GitHub* : [4](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/PositionKey.sol#L4-L4)

```solidity
📁 File: src/libraries/SqrtPriceMathPartial.sol

11: library SqrtPriceMathPartial {

```


*GitHub* : [11](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/SqrtPriceMathPartial.sol#L11-L11)

```solidity
📁 File: src/libraries/TransferHelper.sol

6: library TransferHelper {

```


*GitHub* : [6](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/TransferHelper.sol#L6-L6)

### [G-17]<a name="g-17"></a> Don't initialize variables with default value



*There are 12 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/Whitelist.sol

192:         for (uint i = 0; i < whitelisted.length; i++) {

```


*GitHub* : [192](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L192-L192)

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol

67:         uint256 msb = 0;

```


*GitHub* : [67](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L67-L67)

```solidity
📁 File: src/ILOManager.sol

193:         for (uint256 i = 0; i < initializedPools.length; i++) {

204:         for (uint256 i = 0; i < initializedPools.length; i++) {

```


*GitHub* : [193](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L193-L193), [204](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L204-L204)

```solidity
📁 File: src/ILOPool.sol

92:         for (uint256 index = 0; index < params.vestingConfigs.length; index++) {

324:             for (uint256 i = 0; i < projectConfig.schedule.length; i++) {

405:         for (uint256 index = 0; index < vestingSchedule.length; index++) {

```


*GitHub* : [92](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L92-L92), [324](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L324-L324), [405](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L405-L405)

```solidity
📁 File: src/base/ILOVest.sol

20:         for (uint256 i = 0; i < vestingConfigs.length; i++) {

41:         for (uint256 i = 0; i < scheduleLength; i++) {

```


*GitHub* : [20](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L20-L20), [41](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L41-L41)

```solidity
📁 File: src/base/ILOWhitelist.sol

28:         for (uint256 i = 0; i < users.length; i++) {

35:         for (uint256 i = 0; i < users.length; i++) {

```


*GitHub* : [28](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOWhitelist.sol#L28-L28), [35](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOWhitelist.sol#L35-L35)

```solidity
📁 File: src/base/Multicall.sol

13:         for (uint256 i = 0; i < data.length; i++) {

```


*GitHub* : [13](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/Multicall.sol#L13-L13)

### [G-18]<a name="g-18"></a> Optimize Deployment Size by Fine-tuning IPFS Hash

The Solidity compiler appends 53 bytes of metadata to the smart contract code, incurring an extra cost of 10,600 gas. This additional expense arises from 200 gas per bytecode, plus calldata cost, which amounts to 16 gas for non-zero bytes and 4 gas for zero bytes. This results in a maximum of 848 extra gas in calldata cost.

Reducing this cost is crucial for the following reasons:

The metadata's 53-byte addition leads to a deployment cost increase of 10,600 gas. It can also result in an additional calldata cost of up to 848 gas. Ways to Minimize Gas Consumption:

Employ the `--no-cbor-metadata` compiler option to exclude metadata. Be cautious as this might impact contract verification. Search for code comments that yield an IPFS hash with more zeros, thereby reducing calldata costs.

*There are 22 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/Vultisig.sol

1: // SPDX-License-Identifier: MIT

```


*GitHub* : [1](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Vultisig.sol#L1-L1)

```solidity
📁 File: hardhat-vultisig/contracts/Whitelist.sol

1: // SPDX-License-Identifier: MIT

```


*GitHub* : [1](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L1-L1)

```solidity
📁 File: hardhat-vultisig/contracts/extensions/VultisigWhitelisted.sol

1: // SPDX-License-Identifier: MIT

```


*GitHub* : [1](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/extensions/VultisigWhitelisted.sol#L1-L1)

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol

1: // SPDX-License-Identifier: UNLICENSED

```


*GitHub* : [1](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol#L1-L1)

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/FullMath.sol

1: // SPDX-License-Identifier: MIT

```


*GitHub* : [1](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/FullMath.sol#L1-L1)

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol

1: // SPDX-License-Identifier: GPL-2.0-or-later

```


*GitHub* : [1](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol#L1-L1)

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol

1: // SPDX-License-Identifier: GPL-2.0-or-later

```


*GitHub* : [1](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L1-L1)

```solidity
📁 File: src/ILOManager.sol

1: // SPDX-License-Identifier: BUSL-1.1

```


*GitHub* : [1](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L1-L1)

```solidity
📁 File: src/ILOPool.sol

1: // SPDX-License-Identifier: BUSL-1.1

```


*GitHub* : [1](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L1-L1)

```solidity
📁 File: src/base/ILOPoolImmutableState.sol

1: // SPDX-License-Identifier: GPL-2.0-or-later

```


*GitHub* : [1](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOPoolImmutableState.sol#L1-L1)

```solidity
📁 File: src/base/ILOVest.sol

1: // SPDX-License-Identifier: BUSL-1.1 

```


*GitHub* : [1](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L1-L1)

```solidity
📁 File: src/base/ILOWhitelist.sol

1: // SPDX-License-Identifier: BUSL-1.1 

```


*GitHub* : [1](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOWhitelist.sol#L1-L1)

```solidity
📁 File: src/base/Initializable.sol

1: // SPDX-License-Identifier: BUSL-1.1 

```


*GitHub* : [1](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/Initializable.sol#L1-L1)

```solidity
📁 File: src/base/LiquidityManagement.sol

1: // SPDX-License-Identifier: GPL-2.0-or-later

```


*GitHub* : [1](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/LiquidityManagement.sol#L1-L1)

```solidity
📁 File: src/base/Multicall.sol

1: // SPDX-License-Identifier: GPL-2.0-or-later

```


*GitHub* : [1](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/Multicall.sol#L1-L1)

```solidity
📁 File: src/base/PeripheryPayments.sol

1: // SPDX-License-Identifier: GPL-2.0-or-later

```


*GitHub* : [1](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/PeripheryPayments.sol#L1-L1)

```solidity
📁 File: src/libraries/ChainId.sol

1: // SPDX-License-Identifier: GPL-2.0-or-later

```


*GitHub* : [1](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/ChainId.sol#L1-L1)

```solidity
📁 File: src/libraries/LiquidityAmounts.sol

1: // SPDX-License-Identifier: GPL-2.0-or-later

```


*GitHub* : [1](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/LiquidityAmounts.sol#L1-L1)

```solidity
📁 File: src/libraries/PoolAddress.sol

1: // SPDX-License-Identifier: GPL-2.0-or-later

```


*GitHub* : [1](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/PoolAddress.sol#L1-L1)

```solidity
📁 File: src/libraries/PositionKey.sol

1: // SPDX-License-Identifier: GPL-2.0-or-later

```


*GitHub* : [1](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/PositionKey.sol#L1-L1)

```solidity
📁 File: src/libraries/SqrtPriceMathPartial.sol

1: // SPDX-License-Identifier: GPL-2.0-or-later

```


*GitHub* : [1](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/SqrtPriceMathPartial.sol#L1-L1)

```solidity
📁 File: src/libraries/TransferHelper.sol

1: // SPDX-License-Identifier: GPL-2.0-or-later

```


*GitHub* : [1](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/TransferHelper.sol#L1-L1)

### [G-19]<a name="g-19"></a> Use assembly hashing

From a gas standpoint, the assembly version of the `keccak256` hashing function can be more efficient than the high-level Solidity version. This is because Solidity has additional overhead when handling function calls and memory management, which can increase the gas cost.

*There are 1 instance(s) of this issue:*

```solidity
📁 File: src/ILOManager.sol

79:             bytes32 salt = keccak256(abi.encodePacked(
80:                 ChainId.get(),
81:                 params.uniV3Pool,
82:                 _initializedILOPools[params.uniV3Pool].length
83:             ));

```


*GitHub* : [79](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L79-L83)

### [G-20]<a name="g-20"></a> Use local variables for emitting

Use the function/modifier's local copy of the non-simple state variable, rather than incurring an extra Gwarmaccess ([100 gas](https://gist.github.com/IllIllI000/4a138405b8834bc9dc66b5bdf94715f9)). In the unlikely event that the state variable hasn't already been used by the function/modifier, consider whether it is really necessary to include it in the event, given the fact that it incurs a Gcoldsload (**2100 gas**), or whether it can be passed in to or back out of the functions that do use it, or whether it should be removed from the event, and instead be emitted separately when its value actually changes.

*There are 3 instance(s) of this issue:*

```solidity
📁 File: src/ILOManager.sol

// @audit ILO_POOL_IMPLEMENTATION
165:         emit PoolImplementationChanged(ILO_POOL_IMPLEMENTATION, iloPoolImplementation);

// @audit DEFAULT_DEADLINE_OFFSET
176:         emit DefaultDeadlineOffsetChanged(owner(), DEFAULT_DEADLINE_OFFSET, defaultDeadlineOffset);

```


*GitHub* : [165](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L165-L165), [176](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L176-L176)

```solidity
📁 File: src/ILOPool.sol

// @audit saleInfo
96:         emit ILOPoolInitialized(
97:             params.uniV3Pool,
98:             TICK_LOWER,
99:             TICK_UPPER,
100:             saleInfo,
101:             params.vestingConfigs
102:         );

```


*GitHub* : [96](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L96-L102)

### [G-21]<a name="g-21"></a> State variable read in a loop

The state variable should be cached in a local variable rather than reading it on every iteration of the loop, which will replace each Gwarmaccess (**100 gas**) with a much cheaper stack read.

*There are 1 instance(s) of this issue:*

```solidity
📁 File: src/ILOPool.sol

// @audit _nextId
315:             _mint(projectConfig.recipient, (tokenId = _nextId++));

```


*GitHub* : [315](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L315-L315)

### [G-22]<a name="g-22"></a> use assembly for Low-Level Calls' Return Data

Using assembly for low-level calls in Solidity can provide gas savings, especially when dealing with return data. High-level Solidity calls include overhead for decoding return data, which can be bypassed with assembly. By directly accessing return data in assembly, you can eliminate unnecessary memory allocation and data copying, leading to a more gas-efficient execution. However, this approach requires a deep understanding of the Ethereum Virtual Machine (EVM) and is prone to errors. It’s crucial to ensure security and correctness in the implementation. This technique is best suited for advanced users aiming to optimize contract performance in specific, gas-critical scenarios.

*There are 4 instance(s) of this issue:*

```solidity
📁 File: src/libraries/TransferHelper.sol

19:         (bool success, bytes memory data) =
20:             token.call(abi.encodeWithSelector(IERC20.transferFrom.selector, from, to, value));

34:         (bool success, bytes memory data) = token.call(abi.encodeWithSelector(IERC20.transfer.selector, to, value));

48:         (bool success, bytes memory data) = token.call(abi.encodeWithSelector(IERC20.approve.selector, to, value));

57:         (bool success, ) = to.call{value: value}(new bytes(0));

```


*GitHub* : [19](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/TransferHelper.sol#L19-L20), [34](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/TransferHelper.sol#L34-L34), [48](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/TransferHelper.sol#L48-L48), [57](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/TransferHelper.sol#L57-L57)

### [G-23]<a name="g-23"></a> Merge events to save gas

Consolidating multiple event emissions into a single event in Solidity can result in significant gas savings. Each event emission in Ethereum involves a gas cost, specifically for the topics logged with the event. By merging sequential events into a singular event, you can save on the Glogtopic cost, which is incurred for each topic of each event. This approach can save around 375 gas per additional topic. This strategy is particularly beneficial in functions where multiple related events are emitted in sequence. However, it's crucial to balance gas optimization with the clarity and utility of the event data for off-chain consumers

*There are 5 instance(s) of this issue:*

```solidity
📁 File: src/ILOPool.sol

238:             emit DecreaseLiquidity(tokenId, liquidity2Claim, amount0, amount1);

249:         emit Collect(tokenId, address(this), amountCollected0, amountCollected1);

255:         emit Claim(ownerOf(tokenId), tokenId,liquidity2Claim, amount0, amount1, position.feeGrowthInside0LastX128, position.feeGrowthInside1LastX128);

305:             emit PoolLaunch(uniV3PoolAddress, liquidity, amount0, amount1);

328:             emit Buy(projectConfig.recipient, tokenId, 0, liquidityShares);

```


*GitHub* : [238](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L238-L238), [249](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L249-L249), [255](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L255-L255), [305](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L305-L305), [328](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L328-L328)

### [G-24]<a name="g-24"></a> Inline modifiers used only once



*There are 1 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/Whitelist.sol

54:     modifier onlyVultisig() {
55:         if (_msgSender() != _vultisig) {
56:             revert NotVultisig();
57:         }
58:         _;
59:     }

```


*GitHub* : [54](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L54-L59)

### [G-25]<a name="g-25"></a> Multiple accesses of the same mapping/array key/index should be cached

Access of a value inside a mapping/array, within a function. Caching a mapping's value in a local `storage` or `calldata` variable when the value is accessed [multiple times](https://gist.github.com/IllIllI000/ec23a57daa30a8f8ca8b9681c8ccefb0), saves **~42 gas per access** due to not having to recalculate the key's `keccak256` hash (Gkeccak256 - **30 gas**) and that calculation's associated stack operations. Caching an array's struct avoids recalculating the array offsets into `memory`/`calldata`

*There are 10 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/Whitelist.sol

// @audit '_contributed[to]' also accessed on line 222
226:             _contributed[to] += estimatedETHAmount;

// @audit '_whitelistIndex[whitelisted]' also accessed on line 233
234:             _whitelistIndex[whitelisted] = ++_whitelistCount;

```


*GitHub* : [226](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L226-L226), [234](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L234-L234)

```solidity
📁 File: src/ILOManager.sol

// @audit '_initializedILOPools[params.uniV3Pool]' also accessed on line 82, 106
85:             emit ILOPoolCreated(_project.uniV3PoolAddress, iloPoolAddress, _initializedILOPools[params.uniV3Pool].length);

205:             totalRefundAmount += IILOPool(initializedPools[i]).claimProjectRefund(_cachedProject[uniV3PoolAddress].admin);

```


*GitHub* : [85](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L85-L85), [205](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L205-L205)

```solidity
📁 File: src/ILOPool.sol

// @audit '_positions[tokenId]' also accessed on line 118, 120, 121
119:             _positions[tokenId].raiseAmount,

// @audit '_vestingConfigs[0]' also accessed on line 145
164:         liquidityDelta = uint128(FullMath.mulDiv(liquidityDelta, _vestingConfigs[0].shares, BPS));

// @audit '_positionVests[tokenId]' also accessed on line 145
170:         _positionVests[tokenId].totalLiquidity = _position.liquidity;

// @audit '_positionVests[tokenId]' also accessed on line 320
323:             LinearVest[] storage schedule = _positionVests[tokenId].schedule;

// @audit '_positions[tokenId]' also accessed on line 351
354:         delete _positions[tokenId];

```


*GitHub* : [119](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L119-L119), [164](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L164-L164), [170](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L170-L170), [323](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L323-L323), [354](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L354-L354)

```solidity
📁 File: src/base/ILOVest.sol

// @audit 'schedule[i]' also accessed on line 47
44:             lastEnd = schedule[i].end;

```


*GitHub* : [44](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L44-L44)

### [G-26]<a name="g-26"></a> Multiple mappings can be replaced with a single struct mapping

Saves a storage slot for the mapping. Depending on the circumstances and sizes of types, can avoid a Gsset (20000 gas) per mapping combined. Reads and subsequent writes can also be cheaper when a function requires both values and they both fit in the same storage slot. Finally, if both fields are accessed in the same function, can save ~42 gas per access due to [not having to recalculate the key's keccak256 hash](https://gist.github.com/IllIllI000/ec23a57daa30a8f8ca8b9681c8ccefb0) (Gkeccak256 - 30 gas) and that calculation's associated stack operations.

*There are 5 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/Whitelist.sol

41:     mapping(address => uint256) private _whitelistIndex;

43:     mapping(address => bool) private _isBlacklisted;

45:     mapping(address => uint256) private _contributed;

```


*GitHub* : [41](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L41-L41), [43](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L43-L43), [45](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L45-L45)

```solidity
📁 File: src/ILOManager.sol

25:     mapping(address => Project) private _cachedProject; // map uniV3Pool => project (aka projectId => project)

26:     mapping(address => address[]) private _initializedILOPools; // map uniV3Pool => list of initialized ilo pools

```


*GitHub* : [25](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L25-L25), [26](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L26-L26)

### [G-27]<a name="g-27"></a> State variables should be cached in stack variables rather than re-reading them from storage

The instances below point to the **second+** access of a state variable within a function. Caching of a state variable replaces each Gwarmaccess (**100 gas**) with a much cheaper stack read. Other less obvious fixes/optimizations include having local memory caches of state variable structs, or having local caches of state variable contracts/addresses.

*There are 10 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/Whitelist.sol

// @audit '_allowedWhitelistIndex' also accessed on same line
216:             if (_allowedWhitelistIndex == 0 || _whitelistIndex[to] > _allowedWhitelistIndex) {

```


*GitHub* : [216](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L216-L216)

```solidity
📁 File: hardhat-vultisig/contracts/extensions/VultisigWhitelisted.sol

// @audit '_whitelistContract' also accessed on line 29
30:             IWhitelist(_whitelistContract).checkWhitelist(from, to, amount);

```


*GitHub* : [30](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/extensions/VultisigWhitelisted.sol#L30-L30)

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol

// @audit 'PERIOD' also accessed on same line
41:         uint32 period = PERIOD < longestPeriod ? PERIOD : longestPeriod;

// @audit 'pool' also accessed on line 40
42:         int24 tick = OracleLibrary.consult(pool, period);

```


*GitHub* : [41](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol#L41-L41), [42](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol#L42-L42)

```solidity
📁 File: src/ILOManager.sol

// @audit 'UNIV3_FACTORY' also accessed on line 110
112:             pool = IUniswapV3Factory(UNIV3_FACTORY).createPool(poolKey.token0, poolKey.token1, poolKey.fee);

// @audit 'ILO_POOL_IMPLEMENTATION' also accessed on line 165
166:         ILO_POOL_IMPLEMENTATION = iloPoolImplementation;

// @audit 'DEFAULT_DEADLINE_OFFSET' also accessed on line 176
177:         DEFAULT_DEADLINE_OFFSET = defaultDeadlineOffset;

```


*GitHub* : [112](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L112-L112), [166](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L166-L166), [177](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L177-L177)

```solidity
📁 File: src/ILOPool.sol

// @audit 'saleInfo' also accessed on line 81
100:             saleInfo,

137:         totalRaised += raiseAmount;

// @audit 'totalRaised' also accessed on line 287, 288, 290, 291, 292
286:                 amount0 = totalRaised;

```


*GitHub* : [100](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L100-L100), [137](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L137-L137), [286](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L286-L286)

### [G-28]<a name="g-28"></a> Use Only Named Returns

The Solidity compiler can generate more efficient bytecode when using named returns. It's recommended to replace anonymous returns with named returns for potential gas savings.

*There are 24 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/Vultisig.sol

16:     function approveAndCall(address spender, uint256 amount, bytes calldata extraData) external returns (bool) {

```


*GitHub* : [16](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Vultisig.sol#L16-L16)

```solidity
📁 File: hardhat-vultisig/contracts/Whitelist.sol

77:     function maxAddressCap() external view returns (uint256) {

82:     function vultisig() external view returns (address) {

88:     function whitelistIndex(address account) external view returns (uint256) {

94:     function isBlacklisted(address account) external view returns (bool) {

99:     function isSelfWhitelistDisabled() external view returns (bool) {

104:     function oracle() external view returns (address) {

109:     function pool() external view returns (address) {

114:     function whitelistCount() external view returns (uint256) {

119:     function allowedWhitelistIndex() external view returns (uint256) {

125:     function contributed(address to) external view returns (uint256) {

130:     function locked() external view returns (bool) {

```


*GitHub* : [77](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L77-L77), [82](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L82-L82), [88](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L88-L88), [94](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L94-L94), [99](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L99-L99), [104](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L104-L104), [109](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L109-L109), [114](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L114-L114), [119](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L119-L119), [125](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L125-L125), [130](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L130-L130)

```solidity
📁 File: hardhat-vultisig/contracts/extensions/VultisigWhitelisted.sol

17:     function whitelistContract() external view returns (address) {

```


*GitHub* : [17](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/extensions/VultisigWhitelisted.sol#L17-L17)

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol

34:     function name() external pure returns (string memory) {

39:     function peek(uint256 baseAmount) external view returns (uint256) {

```


*GitHub* : [34](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol#L34-L34), [39](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol#L39-L39)

```solidity
📁 File: src/ILOManager.sol

67:     function project(address uniV3PoolAddress) external override view returns (Project memory) {

```


*GitHub* : [67](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L67-L67)

```solidity
📁 File: src/ILOPool.sol

53:     function name() public pure override(ERC721, IERC721Metadata) returns (string memory) {

57:     function symbol() public pure override(ERC721, IERC721Metadata) returns (string memory) {

457:     function _claimableLiquidity(uint256 tokenId) internal view override returns (uint128) {

```


*GitHub* : [53](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L53-L53), [57](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L57-L57), [457](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L457-L457)

```solidity
📁 File: src/base/ILOWhitelist.sol

17:     function isOpenToAll() external override view returns(bool) {

22:     function isWhitelisted(address user) external override view returns (bool) {

57:     function _isWhitelisted(address user) internal view returns(bool) {

```


*GitHub* : [17](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOWhitelist.sol#L17-L17), [22](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOWhitelist.sol#L22-L22), [57](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOWhitelist.sol#L57-L57)

```solidity
📁 File: src/libraries/PoolAddress.sol

20:     function getPoolKey(
21:         address tokenA,
22:         address tokenB,
23:         uint24 fee
24:     ) internal pure returns (PoolKey memory) {

```


*GitHub* : [20](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/PoolAddress.sol#L20-L24)

```solidity
📁 File: src/libraries/PositionKey.sol

6:     function compute(
7:         address owner,
8:         int24 tickLower,
9:         int24 tickUpper
10:     ) internal pure returns (bytes32) {

```


*GitHub* : [6](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/PositionKey.sol#L6-L10)

### [G-29]<a name="g-29"></a> Nested for loops should be avoided due to high gas costs resulting from O^2 time complexity

In Solidity, avoiding nested for loops is a recommended practice primarily due to the high gas costs associated with them. These loops can lead to quadratic (O^2) time complexity, especially when they iterate over large data sets or perform complex computations. Since every operation in a smart contract consumes gas, and users pay for this gas, optimizing for lower gas usage is crucial. Nested loops, which inherently have higher computational complexity, can significantly increase the gas costs of a contract. To optimize for efficiency, it's advisable to minimize the use of loops, limit their range, and reduce computations within each loop iteration. Alternative patterns like map/filter/reduce might often be cheaper than traditional for loops in terms of gas usage

*There are 1 instance(s) of this issue:*

```solidity
📁 File: src/ILOPool.sol

311:         for (uint256 index = 1; index < _vestingConfigs.length; index++) {
312:             uint256 tokenId;
313:             VestingConfig memory projectConfig = _vestingConfigs[index];
314:             // mint nft for recipient
315:             _mint(projectConfig.recipient, (tokenId = _nextId++));
316:             uint128 liquidityShares = uint128(FullMath.mulDiv(liquidity, projectConfig.shares, BPS));
317: 
318:             Position storage _position = _positions[tokenId];
319:             _position.liquidity = liquidityShares;
320:             _positionVests[tokenId].totalLiquidity = liquidityShares;
321: 
322:             // assign vesting schedule
323:             LinearVest[] storage schedule = _positionVests[tokenId].schedule;
324:             for (uint256 i = 0; i < projectConfig.schedule.length; i++) {
325:                 schedule.push(projectConfig.schedule[i]);
326:             }
327: 
328:             emit Buy(projectConfig.recipient, tokenId, 0, liquidityShares);
329:         }

```


*GitHub* : [311](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L311-L329)

### [G-30]<a name="g-30"></a> Nesting `if`-statements is cheaper than using `&&`

Using a double if statement instead of logical AND (&&) can provide similar short-circuiting behavior whereas double if is slightly more efficient.

*There are 3 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/Whitelist.sol

205:         if (from == _pool && to != owner()) {

```


*GitHub* : [205](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L205-L205)

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol

27:         if (tickCumulativesDelta < 0 && (tickCumulativesDelta % int56(uint56(period)) != 0)) timeWeightedAverageTick--;

```


*GitHub* : [27](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol#L27-L27)

```solidity
📁 File: src/base/PeripheryPayments.sol

27:         if (token == WETH9 && address(this).balance >= value) {

```


*GitHub* : [27](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/PeripheryPayments.sol#L27-L27)

### [G-31]<a name="g-31"></a> Shorten the array rather than copying to a new one

Leveraging inline assembly in Solidity provides the ability to directly manipulate the length slot of an array, thereby altering its length without the need to copy the elements to a new array of the desired size. This technique is more gas-efficient as it avoids the computational expense associated with array duplication. However, this method circumvents the type-checking and safety mechanisms of high-level Solidity and should be used judiciously. Always ensure that the array doesn't contain vital data beyond the revised length, as this data will become unreachable yet still consume storage space.

*There are 2 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol

17:         uint32[] memory secondAgos = new uint32[](2);

```


*GitHub* : [17](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol#L17-L17)

```solidity
📁 File: src/base/Multicall.sol

12:         results = new bytes[](data.length);

```


*GitHub* : [12](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/Multicall.sol#L12-L12)

### [G-32]<a name="g-32"></a> Expression ('') is cheaper than new bytes(0)

In Solidity, using an empty string `('')` instead of `new bytes(0)` in expressions can result in cheaper gas costs. This is because `new bytes(0)` creates a dynamic byte array, leading to additional overhead. By simply using `('')` when an empty bytes array is needed, you can optimize for gas efficiency.

*There are 1 instance(s) of this issue:*

```solidity
📁 File: src/libraries/TransferHelper.sol

57:         (bool success, ) = to.call{value: value}(new bytes(0));

```


*GitHub* : [57](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/TransferHelper.sol#L57-L57)

### [G-33]<a name="g-33"></a> Only emit event in setter function if the state variable was changed

Emitting events in setter functions of smart contracts only when state variables change saves gas. This is because emitting events consumes gas, and unnecessary events, where no actual state change occurs, lead to wasteful consumption.

*There are 2 instance(s) of this issue:*

```solidity
📁 File: src/ILOManager.sol

182:         emit RefundDeadlineChanged(uniV3Pool, _project.refundDeadline, refundDeadline);

```


*GitHub* : [182](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L182-L182)

```solidity
📁 File: src/base/ILOWhitelist.sol

54:         emit SetWhitelist(user, true);

```


*GitHub* : [54](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOWhitelist.sol#L54-L54)

### [G-34]<a name="g-34"></a> Operator `>=`/`<=` costs less gas than operator `>`/`<`

The compiler uses opcodes `GT` and `ISZERO` for code that uses `>`, but only requires `LT` for `>=`. A similar behavior applies for `>`, which uses opcodes `LT` and `ISZERO`, but only requires `GT` for `<=`. It can [save 3 gas](https://gist.github.com/IllIllI000/3dc79d25acccfa16dee4e83ffdc6ffde) for each. It should be converted to the `<=`/`>=` equivalent when comparing against integer literals.

*There are 45 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/Whitelist.sol

192:         for (uint i = 0; i < whitelisted.length; i++) {

216:             if (_allowedWhitelistIndex == 0 || _whitelistIndex[to] > _allowedWhitelistIndex) {

222:             if (_contributed[to] + estimatedETHAmount > _maxAddressCap) {

```


*GitHub* : [192](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L192-L192), [216](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L216-L216), [222](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L222-L222)

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol

41:         uint32 period = PERIOD < longestPeriod ? PERIOD : longestPeriod;

```


*GitHub* : [41](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol#L41-L41)

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/FullMath.sol

30:             require(denominator > 0);

39:         require(denominator > prod1);

111:         if (mulmod(a, b, denominator) > 0) {

112:             require(result < type(uint256).max);

```


*GitHub* : [30](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/FullMath.sol#L30-L30), [39](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/FullMath.sol#L39-L39), [111](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/FullMath.sol#L111-L111), [112](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/FullMath.sol#L112-L112)

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol

27:         if (tickCumulativesDelta < 0 && (tickCumulativesDelta % int56(uint56(period)) != 0)) timeWeightedAverageTick--;

47:             quoteAmount = baseToken < quoteToken

52:             quoteAmount = baseToken < quoteToken

63:         require(observationCardinality > 0, "NI");

```


*GitHub* : [27](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol#L27-L27), [47](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol#L47-L47), [52](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol#L52-L52), [63](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol#L63-L63)

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol

24:         uint256 absTick = tick < 0 ? uint256(-int256(tick)) : uint256(int256(tick));

48:         if (tick > 0) ratio = type(uint256).max / ratio;

```


*GitHub* : [24](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L24-L24), [48](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L48-L48)

```solidity
📁 File: src/ILOManager.sol

188:         require(block.timestamp > _cachedProject[uniV3PoolAddress].launchTime, "LT");

192:         require(initializedPools.length > 0, "NP");

193:         for (uint256 i = 0; i < initializedPools.length; i++) {

202:         require(_cachedProject[uniV3PoolAddress].refundDeadline < block.timestamp, "RFT");

204:         for (uint256 i = 0; i < initializedPools.length; i++) {

```


*GitHub* : [188](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L188-L188), [192](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L192-L192), [193](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L193-L193), [202](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L202-L202), [204](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L204-L204)

```solidity
📁 File: src/ILOPool.sol

92:         for (uint256 index = 0; index < params.vestingConfigs.length; index++) {

161:         require(liquidityDelta > 0, "ZA");

311:         for (uint256 index = 1; index < _vestingConfigs.length; index++) {

324:             for (uint256 i = 0; i < projectConfig.schedule.length; i++) {

369:         if (refundAmount > 0) {

405:         for (uint256 index = 0; index < vestingSchedule.length; index++) {

410:             if (block.timestamp < vest.start) {

417:             if (vest.end < block.timestamp) {

460:         return liquidityClaimed < liquidityUnlocked ? liquidityUnlocked - liquidityClaimed : 0;

```


*GitHub* : [92](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L92-L92), [161](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L161-L161), [311](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L311-L311), [324](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L324-L324), [369](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L369-L369), [405](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L405-L405), [410](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L410-L410), [417](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L417-L417), [460](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L460-L460)

```solidity
📁 File: src/base/ILOVest.sol

20:         for (uint256 i = 0; i < vestingConfigs.length; i++) {

41:         for (uint256 i = 0; i < scheduleLength; i++) {

```


*GitHub* : [20](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L20-L20), [41](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L41-L41)

```solidity
📁 File: src/base/ILOWhitelist.sol

28:         for (uint256 i = 0; i < users.length; i++) {

35:         for (uint256 i = 0; i < users.length; i++) {

```


*GitHub* : [28](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOWhitelist.sol#L28-L28), [35](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOWhitelist.sol#L35-L35)

```solidity
📁 File: src/base/LiquidityManagement.sol

27:         if (amount0Owed > 0) pay(_cachedPoolKey.token0, address(this), msg.sender, amount0Owed);

28:         if (amount1Owed > 0) pay(_cachedPoolKey.token1, address(this), msg.sender, amount1Owed);

```


*GitHub* : [27](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/LiquidityManagement.sol#L27-L27), [28](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/LiquidityManagement.sol#L28-L28)

```solidity
📁 File: src/base/Multicall.sol

13:         for (uint256 i = 0; i < data.length; i++) {

18:                 if (result.length < 68) revert();

```


*GitHub* : [13](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/Multicall.sol#L13-L13), [18](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/Multicall.sol#L18-L18)

```solidity
📁 File: src/libraries/LiquidityAmounts.sol

29:         if (sqrtRatioAX96 > sqrtRatioBX96) (sqrtRatioAX96, sqrtRatioBX96) = (sqrtRatioBX96, sqrtRatioAX96);

45:         if (sqrtRatioAX96 > sqrtRatioBX96) (sqrtRatioAX96, sqrtRatioBX96) = (sqrtRatioBX96, sqrtRatioAX96);

59:         if (sqrtRatioAX96 > sqrtRatioBX96) (sqrtRatioAX96, sqrtRatioBX96) = (sqrtRatioBX96, sqrtRatioAX96);

79:         if (sqrtRatioAX96 > sqrtRatioBX96) (sqrtRatioAX96, sqrtRatioBX96) = (sqrtRatioBX96, sqrtRatioAX96);

```


*GitHub* : [29](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/LiquidityAmounts.sol#L29-L29), [45](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/LiquidityAmounts.sol#L45-L45), [59](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/LiquidityAmounts.sol#L59-L59), [79](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/LiquidityAmounts.sol#L79-L79)

```solidity
📁 File: src/libraries/PoolAddress.sol

25:         if (tokenA > tokenB) (tokenA, tokenB) = (tokenB, tokenA);

34:         require(key.token0 < key.token1);

```


*GitHub* : [25](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/PoolAddress.sol#L25-L25), [34](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/PoolAddress.sol#L34-L34)

```solidity
📁 File: src/libraries/SqrtPriceMathPartial.sol

26:         if (sqrtRatioAX96 > sqrtRatioBX96) (sqrtRatioAX96, sqrtRatioBX96) = (sqrtRatioBX96, sqrtRatioAX96);

31:         require(sqrtRatioAX96 > 0);

55:         if (sqrtRatioAX96 > sqrtRatioBX96) (sqrtRatioAX96, sqrtRatioBX96) = (sqrtRatioBX96, sqrtRatioAX96);

```


*GitHub* : [26](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/SqrtPriceMathPartial.sol#L26-L26), [31](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/SqrtPriceMathPartial.sol#L31-L31), [55](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/SqrtPriceMathPartial.sol#L55-L55)

### [G-35]<a name="g-35"></a> Functions that revert when called by normal users can be marked as `payable`

If a function modifier such as `onlyOwner` is used, the function will revert if a normal user tries to pay the function. Marking the function as `payable` will lower the gas cost for legitimate callers because the compiler will not include checks for whether a payment was provided. The extra opcodes avoided are: `CALLVALUE(2), DUP1(3), ISZERO(3), PUSH2(3), JUMPI(10), PUSH1(3), DUP1(3), REVERT(0), JUMPDEST(1), POP(2)` which cost an average of about 21 gas per call to the function, in addition to the extra deployment cost.

*There are 26 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/Whitelist.sol

136:     function setLocked(bool newLocked) external onlyOwner {

142:     function setMaxAddressCap(uint256 newCap) external onlyOwner {

148:     function setVultisig(address newVultisig) external onlyOwner {

154:     function setIsSelfWhitelistDisabled(bool newFlag) external onlyOwner {

160:     function setOracle(address newOracle) external onlyOwner {

166:     function setPool(address newPool) external onlyOwner {

173:     function setBlacklisted(address blacklisted, bool flag) external onlyOwner {

179:     function setAllowedWhitelistIndex(uint256 newIndex) external onlyOwner {

185:     function addWhitelistedAddress(address whitelisted) external onlyOwner {

191:     function addBatchWhitelist(address[] calldata whitelisted) external onlyOwner {

204:     function checkWhitelist(address from, address to, uint256 amount) external onlyVultisig {

```


*GitHub* : [136](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L136-L136), [142](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L142-L142), [148](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L148-L148), [154](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L154-L154), [160](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L160-L160), [166](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L166-L166), [173](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L173-L173), [179](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L179-L179), [185](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L185-L185), [191](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L191-L191), [204](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L204-L204)

```solidity
📁 File: hardhat-vultisig/contracts/extensions/VultisigWhitelisted.sol

22:     function setWhitelistContract(address newWhitelistContract) external onlyOwner {

```


*GitHub* : [22](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/extensions/VultisigWhitelisted.sol#L22-L22)

```solidity
📁 File: src/ILOManager.sol

72:     function initILOPool(InitPoolParams calldata params) external override onlyProjectAdmin(params.uniV3Pool) returns (address iloPoolAddress) {

150:     function setPlatformFee(uint16 _platformFee) external onlyOwner() {

155:     function setPerformanceFee(uint16 _performanceFee) external onlyOwner() {

160:     function setFeeTaker(address _feeTaker) external override onlyOwner() {

164:     function setILOPoolImplementation(address iloPoolImplementation) external override onlyOwner() {

169:     function transferAdminProject(address admin, address uniV3Pool) external override onlyProjectAdmin(uniV3Pool) {

175:     function setDefaultDeadlineOffset(uint64 defaultDeadlineOffset) external override onlyOwner() {

180:     function setRefundDeadlineForProject(address uniV3Pool, uint64 refundDeadline) external override onlyOwner() {

201:     function claimRefund(address uniV3PoolAddress) external override onlyProjectAdmin(uniV3PoolAddress) returns(uint256 totalRefundAmount) {

```


*GitHub* : [72](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L72-L72), [150](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L150-L150), [155](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L155-L155), [160](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L160-L160), [164](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L164-L164), [169](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L169-L169), [175](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L175-L175), [180](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L180-L180), [201](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L201-L201)

```solidity
📁 File: src/ILOPool.sol

269:     function launch() external override OnlyManager() {

363:     function claimProjectRefund(address projectAdmin) external override refundable() OnlyManager() returns(uint256 refundAmount) {

```


*GitHub* : [269](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L269-L269), [363](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L363-L363)

```solidity
📁 File: src/base/ILOWhitelist.sol

12:     function setOpenToAll(bool openToAll) external override onlyProjectAdmin{

27:     function batchWhitelist(address[] calldata users) external override onlyProjectAdmin{

34:     function batchRemoveWhitelist(address[] calldata users) external override onlyProjectAdmin{

```


*GitHub* : [12](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOWhitelist.sol#L12-L12), [27](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOWhitelist.sol#L27-L27), [34](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOWhitelist.sol#L34-L34)

### [G-36]<a name="g-36"></a> Using `++i/--i` instead of `i++/i--` can save gas

*Saves 5 gas per instance*

*There are 16 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/Whitelist.sol

192:         for (uint i = 0; i < whitelisted.length; i++) {

```


*GitHub* : [192](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L192-L192)

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/FullMath.sol

113:             result++;

```


*GitHub* : [113](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/FullMath.sol#L113-L113)

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol

27:         if (tickCumulativesDelta < 0 && (tickCumulativesDelta % int56(uint56(period)) != 0)) timeWeightedAverageTick--;

```


*GitHub* : [27](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol#L27-L27)

```solidity
📁 File: src/ILOManager.sol

193:         for (uint256 i = 0; i < initializedPools.length; i++) {

204:         for (uint256 i = 0; i < initializedPools.length; i++) {

```


*GitHub* : [193](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L193-L193), [204](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L204-L204)

```solidity
📁 File: src/ILOPool.sol

92:         for (uint256 index = 0; index < params.vestingConfigs.length; index++) {

144:             _mint(recipient, (tokenId = _nextId++));

311:         for (uint256 index = 1; index < _vestingConfigs.length; index++) {

315:             _mint(projectConfig.recipient, (tokenId = _nextId++));

324:             for (uint256 i = 0; i < projectConfig.schedule.length; i++) {

405:         for (uint256 index = 0; index < vestingSchedule.length; index++) {

```


*GitHub* : [92](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L92-L92), [144](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L144-L144), [311](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L311-L311), [315](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L315-L315), [324](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L324-L324), [405](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L405-L405)

```solidity
📁 File: src/base/ILOVest.sol

20:         for (uint256 i = 0; i < vestingConfigs.length; i++) {

41:         for (uint256 i = 0; i < scheduleLength; i++) {

```


*GitHub* : [20](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L20-L20), [41](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L41-L41)

```solidity
📁 File: src/base/ILOWhitelist.sol

28:         for (uint256 i = 0; i < users.length; i++) {

35:         for (uint256 i = 0; i < users.length; i++) {

```


*GitHub* : [28](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOWhitelist.sol#L28-L28), [35](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOWhitelist.sol#L35-L35)

```solidity
📁 File: src/base/Multicall.sol

13:         for (uint256 i = 0; i < data.length; i++) {

```


*GitHub* : [13](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/Multicall.sol#L13-L13)

### [G-37]<a name="g-37"></a> Using `private` for constants saves gas

If needed, the values can be read from the verified contract source code, or if there are multiple values there can be a single getter function that [returns a tuple](https://github.com/code-423n4/2022-08-frax/blob/90f55a9ce4e25bceed3a74290b854341d8de6afa/src/contracts/FraxlendPair.sol#L156-L178) of the values of all currently-public constants. Saves **3406-3606 gas** in deployment gas due to the compiler not having to create non-payable getter functions for deployment calldata, not having to store the bytes of the value outside of where it's used, and not adding another entry to the method ID table

*There are 8 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol

16:     uint32 public constant PERIOD = 30 minutes;

18:     uint128 public constant BASE_AMOUNT = 1e18; // VULT has 18 decimals

```


*GitHub* : [16](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol#L16-L16), [18](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol#L18-L18)

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol

9:     int24 internal constant MIN_TICK = -887272;

11:     int24 internal constant MAX_TICK = -MIN_TICK;

14:     uint160 internal constant MIN_SQRT_RATIO = 4295128739;

16:     uint160 internal constant MAX_SQRT_RATIO = 1461446703485210103287273052203988822378723970342;

```


*GitHub* : [9](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L9-L9), [11](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L11-L11), [14](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L14-L14), [16](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L16-L16)

```solidity
📁 File: src/base/ILOPoolImmutableState.sol

13:     uint16 constant BPS = 10000;

```


*GitHub* : [13](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOPoolImmutableState.sol#L13-L13)

```solidity
📁 File: src/libraries/PoolAddress.sol

6:     bytes32 internal constant POOL_INIT_CODE_HASH = 0xe34f199b19b2b4f47f68442619d555527d244f78a3297ea89325f843f87b8b54;

```


*GitHub* : [6](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/PoolAddress.sol#L6-L6)

### [G-38]<a name="g-38"></a> Refactor modifiers to call a local function

Modifiers code is copied in all instances where it's used, increasing bytecode size. By doing a refractor to the internal function, one can reduce bytecode size significantly at the cost of one JUMP.

*There are 8 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/Whitelist.sol

54:     modifier onlyVultisig() {
55:         if (_msgSender() != _vultisig) {
56:             revert NotVultisig();
57:         }
58:         _;
59:     }

```


*GitHub* : [54](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L54-L59)

```solidity
📁 File: src/ILOManager.sol

51:     modifier onlyProjectAdmin(address uniV3Pool) {
52:         require(_cachedProject[uniV3Pool].admin == msg.sender, "UA");
53:         _;
54:     }

```


*GitHub* : [51](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L51-L54)

```solidity
📁 File: src/ILOPool.sol

178:     modifier isAuthorizedForToken(uint256 tokenId) {
179:         require(_isApprovedOrOwner(msg.sender, tokenId), 'UA');
180:         _;
181:     }

263:     modifier OnlyManager() {
264:         require(msg.sender == MANAGER, "UA");
265:         _;
266:     }

337:     modifier refundable() {
338:         if (!_refundTriggered) {
339:             // if ilo pool is lauch sucessfully, we can not refund anymore
340:             require(!_launchSucceeded, "PL");
341:             IILOManager.Project memory _project = IILOManager(MANAGER).project(_cachedUniV3PoolAddress);
342:             require(block.timestamp >= _project.refundDeadline, "RFT");
343: 
344:             _refundTriggered = true;
345:         }
346:         _;
347:     }

463:     modifier onlyProjectAdmin() override {
464:         IILOManager.Project memory _project = IILOManager(MANAGER).project(_cachedUniV3PoolAddress);
465:         require(msg.sender == _project.admin, "UA");
466:         _;
467:     }

```


*GitHub* : [178](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L178-L181), [263](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L263-L266), [337](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L337-L347), [463](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L463-L467)

```solidity
📁 File: src/base/Initializable.sol

10:     modifier whenNotInitialized() {
11:         require(!_initialized);
12:         _;
13:         _initialized = true;
14:     }

15:     modifier afterInitialize() {
16:         require(_initialized);
17:         _;
18:     }

```


*GitHub* : [10](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/Initializable.sol#L10-L14), [15](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/Initializable.sol#L15-L18)

### [G-39]<a name="g-39"></a> Use assembly scratch space for building calldata for external calls

If an external call's calldata can fit into two or fewer words, use the scratch space to build the calldata, rather than allowing Solidity to do a memory expansion.

*There are 40 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/Vultisig.sol

21:         IApproveAndCallReceiver(spender).receiveApproval(msg.sender, amount, address(this), extraData);

```


*GitHub* : [21](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Vultisig.sol#L21-L21)

```solidity
📁 File: hardhat-vultisig/contracts/Whitelist.sol

73:         payable(_msgSender()).transfer(msg.value);

221:             uint256 estimatedETHAmount = IOracle(_oracle).peek(amount);

```


*GitHub* : [73](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L73-L73), [221](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L221-L221)

```solidity
📁 File: hardhat-vultisig/contracts/extensions/VultisigWhitelisted.sol

30:             IWhitelist(_whitelistContract).checkWhitelist(from, to, amount);

32:         super._beforeTokenTransfer(from, to, amount);

```


*GitHub* : [30](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/extensions/VultisigWhitelisted.sol#L30-L30), [32](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/extensions/VultisigWhitelisted.sol#L32-L32)

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol

40:         uint32 longestPeriod = OracleLibrary.getOldestObservationSecondsAgo(pool);

42:         int24 tick = OracleLibrary.consult(pool, period);

43:         uint256 quotedWETHAmount = OracleLibrary.getQuoteAtTick(tick, BASE_AMOUNT, baseToken, WETH);

```


*GitHub* : [40](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol#L40-L40), [42](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol#L42-L42), [43](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol#L43-L43)

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol

42:         uint160 sqrtRatioX96 = TickMath.getSqrtRatioAtTick(tick);

62:         (, , uint16 observationIndex, uint16 observationCardinality, , , ) = IUniswapV3Pool(pool).slot0();

65:         (uint32 observationTimestamp, , , bool initialized) = IUniswapV3Pool(pool).observations(
66:             (observationIndex + 1) % observationCardinality
67:         );

```


*GitHub* : [42](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol#L42-L42), [62](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol#L62-L62), [65](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol#L65-L67)

```solidity
📁 File: src/ILOManager.sol

88:         uint160 sqrtRatioLowerX96 = TickMath.getSqrtRatioAtTick(params.tickLower);

89:         uint160 sqrtRatioUpperX96 = TickMath.getSqrtRatioAtTick(params.tickUpper);

105:         IILOPool(iloPoolAddress).initialize(initParams);

113:             IUniswapV3Pool(pool).initialize(sqrtPriceX96);

115:             (uint160 sqrtPriceX96Existing, , , , , , ) = IUniswapV3Pool(pool).slot0();

117:                 IUniswapV3Pool(pool).initialize(sqrtPriceX96);

189:         (uint160 sqrtPriceX96, , , , , , ) = IUniswapV3Pool(uniV3PoolAddress).slot0();

194:             IILOPool(initializedPools[i]).launch();

```


*GitHub* : [88](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L88-L88), [89](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L89-L89), [105](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L105-L105), [113](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L113-L113), [115](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L115-L115), [117](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L117-L117), [189](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L189-L189), [194](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L194-L194)

```solidity
📁 File: src/ILOPool.sol

173:         TransferHelper.safeTransferFrom(RAISE_TOKEN, msg.sender, address(this), raiseAmount);

210:             bytes32 positionKey = PositionKey.compute(address(this), TICK_LOWER, TICK_UPPER);

213:             (, uint256 feeGrowthInside0LastX128, uint256 feeGrowthInside1LastX128, , ) = pool.positions(positionKey);

242:         (uint128 amountCollected0, uint128 amountCollected1) = pool.collect(
243:             address(this),
244:             TICK_LOWER,
245:             TICK_UPPER,
246:             type(uint128).max,
247:             type(uint128).max
248:         );

252:         TransferHelper.safeTransfer(_cachedPoolKey.token0, ownerOf(tokenId), amount0);

253:         TransferHelper.safeTransfer(_cachedPoolKey.token1, ownerOf(tokenId), amount1);

257:         address feeTaker = IILOManager(MANAGER).FEE_TAKER();

259:         TransferHelper.safeTransfer(_cachedPoolKey.token0, feeTaker, amountCollected0-amount0);

260:         TransferHelper.safeTransfer(_cachedPoolKey.token1, feeTaker, amountCollected1-amount1);

358:         TransferHelper.safeTransfer(RAISE_TOKEN, tokenOwner, refundAmount);

370:             TransferHelper.safeTransfer(SALE_TOKEN, projectAdmin, refundAmount);

```


*GitHub* : [173](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L173-L173), [210](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L210-L210), [213](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L213-L213), [242](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L242-L248), [252](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L252-L252), [253](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L253-L253), [257](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L257-L257), [259](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L259-L259), [260](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L260-L260), [358](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L358-L358), [370](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L370-L370)

```solidity
📁 File: src/base/ILOWhitelist.sol

48:         EnumerableSet.remove(_whitelisted, user);

53:         EnumerableSet.add(_whitelisted, user);

```


*GitHub* : [48](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOWhitelist.sol#L48-L48), [53](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOWhitelist.sol#L53-L53)

```solidity
📁 File: src/base/Multicall.sol

14:             (bool success, bytes memory result) = address(this).delegatecall(data[i]);

```


*GitHub* : [14](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/Multicall.sol#L14-L14)

```solidity
📁 File: src/base/PeripheryPayments.sol

30:             IWETH9(WETH9).transfer(recipient, value);

33:             TransferHelper.safeTransfer(token, recipient, value);

36:             TransferHelper.safeTransferFrom(token, payer, recipient, value);

```


*GitHub* : [30](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/PeripheryPayments.sol#L30-L30), [33](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/PeripheryPayments.sol#L33-L33), [36](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/PeripheryPayments.sol#L36-L36)

```solidity
📁 File: src/libraries/TransferHelper.sol

19:         (bool success, bytes memory data) =
20:             token.call(abi.encodeWithSelector(IERC20.transferFrom.selector, from, to, value));

34:         (bool success, bytes memory data) = token.call(abi.encodeWithSelector(IERC20.transfer.selector, to, value));

48:         (bool success, bytes memory data) = token.call(abi.encodeWithSelector(IERC20.approve.selector, to, value));

57:         (bool success, ) = to.call{value: value}(new bytes(0));

```


*GitHub* : [19](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/TransferHelper.sol#L19-L20), [34](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/TransferHelper.sol#L34-L34), [48](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/TransferHelper.sol#L48-L48), [57](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/TransferHelper.sol#L57-L57)

### [G-40]<a name="g-40"></a> Use shift right/left instead of division if possible

While the `DIV` opcode uses 5 gas, the `SHR` / `SHL` opcode only uses 3 gas. Furthermore, beware that Solidity's division operation also includes a division-by-0 prevention which is bypassed using shifting. Eventually, overflow checks are never performed for shift operations as they are done for arithmetic operations. Instead, the result is always truncated, so the calculation can be unchecked in Solidity version `0.8+`
- Use `>> 1` instead of `/ 2`
- Use `>> 2` instead of `/ 4`
- Use `<< 3` instead of `* 8`
- ...
- Use `>> 5` instead of `/ 2^5 == / 32`
- Use `<< 6` instead of `* 2^6 == * 64`

TL;DR:
- Shifting left by N is like multiplying by 2^N (Each bits to the left is an increased power of 2)
- Shifting right by N is like dividing by 2^N (Each bits to the right is a decreased power of 2)

*Saves around 2 gas + 20 for unchecked per instance*

*There are 5 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol

45:         return (quotedWETHAmount * baseAmount * 95) / 1e20; // 100 / 1e18

```


*GitHub* : [45](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol#L45-L45)

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol

24:         timeWeightedAverageTick = int24(tickCumulativesDelta / int56(uint56(period)));

```


*GitHub* : [24](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol#L24-L24)

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol

48:         if (tick > 0) ratio = type(uint256).max / ratio;

```


*GitHub* : [48](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L48-L48)

```solidity
📁 File: src/libraries/LiquidityAmounts.sol

62:             FullMath.mulDiv(
63:                 uint256(liquidity) << FixedPoint96.RESOLUTION,
64:                 sqrtRatioBX96 - sqrtRatioAX96,
65:                 sqrtRatioBX96
66:             ) / sqrtRatioAX96;

```


*GitHub* : [62](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/LiquidityAmounts.sol#L62-L66)

```solidity
📁 File: src/libraries/SqrtPriceMathPartial.sol

39:                 : FullMath.mulDiv(numerator1, numerator2, sqrtRatioBX96) / sqrtRatioAX96;

```


*GitHub* : [39](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/SqrtPriceMathPartial.sol#L39-L39)

### [G-41]<a name="g-41"></a> Usage of smaller `uint`/`int` types causes overhead

When using a smaller int/uint type it first needs to be converted to it's 258 bit counterpart to be operated, this increases the gass cost and thus should be avoided. However it does make sense to use smaller int/uint values within structs provided you pack the struct properly.

*There are 92 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol

16:     uint32 public constant PERIOD = 30 minutes;

18:     uint128 public constant BASE_AMOUNT = 1e18; // VULT has 18 decimals

40:         uint32 longestPeriod = OracleLibrary.getOldestObservationSecondsAgo(pool);

41:         uint32 period = PERIOD < longestPeriod ? PERIOD : longestPeriod;

42:         int24 tick = OracleLibrary.consult(pool, period);

```


*GitHub* : [16](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol#L16-L16), [18](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol#L18-L18), [40](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol#L40-L40), [41](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol#L41-L41), [42](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol#L42-L42)

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol

14:     function consult(address pool, uint32 period) internal view returns (int24 timeWeightedAverageTick) {

22:         int56 tickCumulativesDelta = tickCumulatives[1] - tickCumulatives[0];

37:         int24 tick,

38:         uint128 baseAmount,

42:         uint160 sqrtRatioX96 = TickMath.getSqrtRatioAtTick(tick);

61:     function getOldestObservationSecondsAgo(address pool) internal view returns (uint32 secondsAgo) {

62:         (, , uint16 observationIndex, uint16 observationCardinality, , , ) = IUniswapV3Pool(pool).slot0();

65:         (uint32 observationTimestamp, , , bool initialized) = IUniswapV3Pool(pool).observations(

```


*GitHub* : [14](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol#L14-L14), [22](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol#L22-L22), [37](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol#L37-L37), [38](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol#L38-L38), [42](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol#L42-L42), [61](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol#L61-L61), [62](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol#L62-L62), [65](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol#L65-L65)

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol

9:     int24 internal constant MIN_TICK = -887272;

11:     int24 internal constant MAX_TICK = -MIN_TICK;

14:     uint160 internal constant MIN_SQRT_RATIO = 4295128739;

16:     uint160 internal constant MAX_SQRT_RATIO = 1461446703485210103287273052203988822378723970342;

23:     function getSqrtRatioAtTick(int24 tick) internal pure returns (uint160 sqrtPriceX96) {

61:     function getTickAtSqrtRatio(uint160 sqrtPriceX96) internal pure returns (int24 tick) {

200:         int24 tickLow = int24((log_sqrt10001 - 3402992956809132418596140100660247210) >> 128);

201:         int24 tickHi = int24((log_sqrt10001 + 291339464771989622907027621153398088495) >> 128);

```


*GitHub* : [9](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L9-L9), [11](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L11-L11), [14](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L14-L14), [16](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L16-L16), [23](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L23-L23), [61](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L61-L61), [200](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L200-L200), [201](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L201-L201)

```solidity
📁 File: src/ILOManager.sol

19:     uint64 private DEFAULT_DEADLINE_OFFSET = 7 * 24 * 60 * 60; // 7 days

20:     uint16 public override PLATFORM_FEE;

21:     uint16 public override PERFORMANCE_FEE;

39:         uint16 platformFee,

40:         uint16 performanceFee

58:         uint64 refundDeadline = params.launchTime + DEFAULT_DEADLINE_OFFSET;

88:         uint160 sqrtRatioLowerX96 = TickMath.getSqrtRatioAtTick(params.tickLower);

89:         uint160 sqrtRatioUpperX96 = TickMath.getSqrtRatioAtTick(params.tickUpper);

109:     function _initUniV3PoolIfNecessary(PoolAddress.PoolKey memory poolKey, uint160 sqrtPriceX96) internal returns (address pool) {

115:             (uint160 sqrtPriceX96Existing, , , , , , ) = IUniswapV3Pool(pool).slot0();

128:         uint24 fee,

129:         uint160 initialPoolPriceX96,

130:         uint64 launchTime,

131:         uint64 refundDeadline

150:     function setPlatformFee(uint16 _platformFee) external onlyOwner() {

155:     function setPerformanceFee(uint16 _performanceFee) external onlyOwner() {

175:     function setDefaultDeadlineOffset(uint64 defaultDeadlineOffset) external override onlyOwner() {

180:     function setRefundDeadlineForProject(address uniV3Pool, uint64 refundDeadline) external override onlyOwner() {

189:         (uint160 sqrtPriceX96, , , , , , ) = IUniswapV3Pool(uniV3PoolAddress).slot0();

```


*GitHub* : [19](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L19-L19), [20](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L20-L20), [21](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L21-L21), [39](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L39-L39), [40](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L40-L40), [58](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L58-L58), [88](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L88-L88), [89](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L89-L89), [109](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L109-L109), [115](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L115-L115), [128](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L128-L128), [129](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L129-L129), [130](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L130-L130), [131](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L131-L131), [150](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L150-L150), [155](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L155-L155), [175](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L175-L175), [180](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L180-L180), [189](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L189-L189)

```solidity
📁 File: src/ILOPool.sol

111:             uint128 liquidity,

130:             uint128 liquidityDelta

195:         uint128 liquidity2Claim = _claimableLiquidity(tokenId);

201:             uint128 positionLiquidity = position.liquidity;

242:         (uint128 amountCollected0, uint128 amountCollected1) = pool.collect(

275:         uint128 liquidity;

316:             uint128 liquidityShares = uint128(FullMath.mulDiv(liquidity, projectConfig.shares, BPS));

384:         uint128 liquidity

400:     function _unlockedLiquidity(uint256 tokenId) internal view override returns (uint128 liquidityUnlocked) {

403:         uint128 totalLiquidity = _positionVest.totalLiquidity;

438:     function _deductFees(uint256 amount0, uint256 amount1, uint16 feeBPS) internal pure 

449:         uint128 unlockedLiquidity,

450:         uint128 claimedLiquidity

457:     function _claimableLiquidity(uint256 tokenId) internal view override returns (uint128) {

458:         uint128 liquidityClaimed = _positionVests[tokenId].totalLiquidity - _positions[tokenId].liquidity;

459:         uint128 liquidityUnlocked = _unlockedLiquidity(tokenId);

```


*GitHub* : [111](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L111-L111), [130](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L130-L130), [195](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L195-L195), [201](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L201-L201), [242](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L242-L242), [275](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L275-L275), [316](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L316-L316), [384](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L384-L384), [400](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L400-L400), [403](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L403-L403), [438](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L438-L438), [449](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L449-L449), [450](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L450-L450), [457](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L457-L457), [458](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L458-L458), [459](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L459-L459)

```solidity
📁 File: src/base/ILOPoolImmutableState.sol

13:     uint16 constant BPS = 10000;

17:     int24 public override TICK_LOWER;

18:     int24 public override TICK_UPPER;

19:     uint160 public override SQRT_RATIO_X96;

20:     uint160 internal SQRT_RATIO_LOWER_X96;

21:     uint160 internal SQRT_RATIO_UPPER_X96;

```


*GitHub* : [13](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOPoolImmutableState.sol#L13-L13), [17](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOPoolImmutableState.sol#L17-L17), [18](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOPoolImmutableState.sol#L18-L18), [19](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOPoolImmutableState.sol#L19-L19), [20](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOPoolImmutableState.sol#L20-L20), [21](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOPoolImmutableState.sol#L21-L21)

```solidity
📁 File: src/base/ILOVest.sol

13:     function _unlockedLiquidity(uint256 tokenId) internal view virtual returns (uint128 liquidityUnlocked);

15:     function _claimableLiquidity(uint256 tokenId) internal view virtual returns (uint128 claimableLiquidity);

17:     function _validateSharesAndVests(uint64 launchTime, VestingConfig[] memory vestingConfigs) internal pure {

18:         uint16 totalShares;

19:         uint16 BPS = 10000;

35:     function _validateVestSchedule(uint64 launchTime, LinearVest[] memory schedule) internal pure {

37:         uint16 BPS = 10000;

38:         uint16 totalShares;

39:         uint64 lastEnd;

```


*GitHub* : [13](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L13-L13), [15](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L15-L15), [17](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L17-L17), [18](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L18-L18), [19](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L19-L19), [35](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L35-L35), [37](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L37-L37), [38](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L38-L38), [39](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L39-L39)

```solidity
📁 File: src/libraries/LiquidityAmounts.sol

14:     function toUint128(uint256 x) private pure returns (uint128 y) {

25:         uint160 sqrtRatioAX96,

26:         uint160 sqrtRatioBX96,

28:     ) internal pure returns (uint128 liquidity) {

41:         uint160 sqrtRatioAX96,

42:         uint160 sqrtRatioBX96,

44:     ) internal pure returns (uint128 liquidity) {

55:         uint160 sqrtRatioAX96,

56:         uint160 sqrtRatioBX96,

57:         uint128 liquidity

75:         uint160 sqrtRatioAX96,

76:         uint160 sqrtRatioBX96,

77:         uint128 liquidity

```


*GitHub* : [14](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/LiquidityAmounts.sol#L14-L14), [25](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/LiquidityAmounts.sol#L25-L25), [26](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/LiquidityAmounts.sol#L26-L26), [28](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/LiquidityAmounts.sol#L28-L28), [41](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/LiquidityAmounts.sol#L41-L41), [42](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/LiquidityAmounts.sol#L42-L42), [44](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/LiquidityAmounts.sol#L44-L44), [55](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/LiquidityAmounts.sol#L55-L55), [56](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/LiquidityAmounts.sol#L56-L56), [57](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/LiquidityAmounts.sol#L57-L57), [75](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/LiquidityAmounts.sol#L75-L75), [76](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/LiquidityAmounts.sol#L76-L76), [77](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/LiquidityAmounts.sol#L77-L77)

```solidity
📁 File: src/libraries/PositionKey.sol

8:         int24 tickLower,

9:         int24 tickUpper

```


*GitHub* : [8](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/PositionKey.sol#L8-L8), [9](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/PositionKey.sol#L9-L9)

```solidity
📁 File: src/libraries/SqrtPriceMathPartial.sol

21:         uint160 sqrtRatioAX96,

22:         uint160 sqrtRatioBX96,

23:         uint128 liquidity,

50:         uint160 sqrtRatioAX96,

51:         uint160 sqrtRatioBX96,

52:         uint128 liquidity,

```


*GitHub* : [21](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/SqrtPriceMathPartial.sol#L21-L21), [22](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/SqrtPriceMathPartial.sol#L22-L22), [23](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/SqrtPriceMathPartial.sol#L23-L23), [50](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/SqrtPriceMathPartial.sol#L50-L50), [51](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/SqrtPriceMathPartial.sol#L51-L51), [52](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/SqrtPriceMathPartial.sol#L52-L52)

### [G-42]<a name="g-42"></a> Consider using solady's 'FixedPointMathLib'

Using Solady's 'FixedPointMathLib' for multiplication or division operations in Solidity can lead to significant gas savings. This library is designed to optimize fixed-point arithmetic operations, which are common in financial calculations involving tokens or currencies. By implementing more efficient algorithms and assembly optimizations, 'FixedPointMathLib' minimizes the computational resources required for these operations. For contracts that frequently perform such calculations, integrating this library can reduce transaction costs, thereby enhancing overall performance and cost-effectiveness. However, developers must ensure compatibility with their existing codebase and thoroughly test for accuracy and expected behavior to avoid any unintended consequences.

*There are 39 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/Vultisig.sol

13:         _mint(_msgSender(), 100_000_000 * 1e18);

```


*GitHub* : [13](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Vultisig.sol#L13-L13)

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol

45:         return (quotedWETHAmount * baseAmount * 95) / 1e20; // 100 / 1e18

```


*GitHub* : [45](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol#L45-L45)

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/FullMath.sol

76:         prod0 |= prod1 * twos;

83:         uint256 inv = (3 * denominator) ^ 2;

87:         inv *= 2 - denominator * inv; // inverse mod 2**8

88:         inv *= 2 - denominator * inv; // inverse mod 2**16

89:         inv *= 2 - denominator * inv; // inverse mod 2**32

90:         inv *= 2 - denominator * inv; // inverse mod 2**64

91:         inv *= 2 - denominator * inv; // inverse mod 2**128

92:         inv *= 2 - denominator * inv; // inverse mod 2**256

100:         result = prod0 * inv;

```


*GitHub* : [76](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/FullMath.sol#L76-L76), [83](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/FullMath.sol#L83-L83), [87](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/FullMath.sol#L87-L87), [88](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/FullMath.sol#L88-L88), [89](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/FullMath.sol#L89-L89), [90](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/FullMath.sol#L90-L90), [91](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/FullMath.sol#L91-L91), [92](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/FullMath.sol#L92-L92), [100](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/FullMath.sol#L100-L100)

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol

24:         timeWeightedAverageTick = int24(tickCumulativesDelta / int56(uint56(period)));

46:             uint256 ratioX192 = uint256(sqrtRatioX96) * sqrtRatioX96;

```


*GitHub* : [24](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol#L24-L24), [46](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol#L46-L46)

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol

28:         if (absTick & 0x2 != 0) ratio = (ratio * 0xfff97272373d413259a46990580e213a) >> 128;

29:         if (absTick & 0x4 != 0) ratio = (ratio * 0xfff2e50f5f656932ef12357cf3c7fdcc) >> 128;

30:         if (absTick & 0x8 != 0) ratio = (ratio * 0xffe5caca7e10e4e61c3624eaa0941cd0) >> 128;

31:         if (absTick & 0x10 != 0) ratio = (ratio * 0xffcb9843d60f6159c9db58835c926644) >> 128;

32:         if (absTick & 0x20 != 0) ratio = (ratio * 0xff973b41fa98c081472e6896dfb254c0) >> 128;

33:         if (absTick & 0x40 != 0) ratio = (ratio * 0xff2ea16466c96a3843ec78b326b52861) >> 128;

34:         if (absTick & 0x80 != 0) ratio = (ratio * 0xfe5dee046a99a2a811c461f1969c3053) >> 128;

35:         if (absTick & 0x100 != 0) ratio = (ratio * 0xfcbe86c7900a88aedcffc83b479aa3a4) >> 128;

36:         if (absTick & 0x200 != 0) ratio = (ratio * 0xf987a7253ac413176f2b074cf7815e54) >> 128;

37:         if (absTick & 0x400 != 0) ratio = (ratio * 0xf3392b0822b70005940c7a398e4b70f3) >> 128;

38:         if (absTick & 0x800 != 0) ratio = (ratio * 0xe7159475a2c29b7443b29c7fa6e889d9) >> 128;

39:         if (absTick & 0x1000 != 0) ratio = (ratio * 0xd097f3bdfd2022b8845ad8f792aa5825) >> 128;

40:         if (absTick & 0x2000 != 0) ratio = (ratio * 0xa9f746462d870fdf8a65dc1f90e061e5) >> 128;

41:         if (absTick & 0x4000 != 0) ratio = (ratio * 0x70d869a156d2a1b890bb3df62baf32f7) >> 128;

42:         if (absTick & 0x8000 != 0) ratio = (ratio * 0x31be135f97d08fd981231505542fcfa6) >> 128;

43:         if (absTick & 0x10000 != 0) ratio = (ratio * 0x9aa508b5b7a84e1c677de54f3e99bc9) >> 128;

44:         if (absTick & 0x20000 != 0) ratio = (ratio * 0x5d6af8dedb81196699c329225ee604) >> 128;

45:         if (absTick & 0x40000 != 0) ratio = (ratio * 0x2216e584f5fa1ea926041bedfe98) >> 128;

46:         if (absTick & 0x80000 != 0) ratio = (ratio * 0x48a170391f7dc42444e8fa2) >> 128;

48:         if (tick > 0) ratio = type(uint256).max / ratio;

198:         int256 log_sqrt10001 = log_2 * 255738958999603826347141; // 128.128 number

```


*GitHub* : [28](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L28-L28), [29](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L29-L29), [30](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L30-L30), [31](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L31-L31), [32](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L32-L32), [33](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L33-L33), [34](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L34-L34), [35](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L35-L35), [36](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L36-L36), [37](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L37-L37), [38](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L38-L38), [39](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L39-L39), [40](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L40-L40), [41](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L41-L41), [42](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L42-L42), [43](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L43-L43), [44](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L44-L44), [45](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L45-L45), [46](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L46-L46), [48](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L48-L48), [198](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L198-L198)

```solidity
📁 File: src/ILOManager.sol

19:     uint64 private DEFAULT_DEADLINE_OFFSET = 7 * 24 * 60 * 60; // 7 days

```


*GitHub* : [19](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L19-L19)

```solidity
📁 File: src/ILOPool.sol

425:                     vest.shares * totalLiquidity, 

427:                     (vest.end - vest.start) * BPS

```


*GitHub* : [425](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L425-L425), [427](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L427-L427)

```solidity
📁 File: src/libraries/LiquidityAmounts.sol

62:             FullMath.mulDiv(
63:                 uint256(liquidity) << FixedPoint96.RESOLUTION,
64:                 sqrtRatioBX96 - sqrtRatioAX96,
65:                 sqrtRatioBX96
66:             ) / sqrtRatioAX96;

```


*GitHub* : [62](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/LiquidityAmounts.sol#L62-L66)

```solidity
📁 File: src/libraries/SqrtPriceMathPartial.sol

39:                 : FullMath.mulDiv(numerator1, numerator2, sqrtRatioBX96) / sqrtRatioAX96;

```


*GitHub* : [39](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/SqrtPriceMathPartial.sol#L39-L39)

### [G-43]<a name="g-43"></a> Newer versions of solidity are more gas efficient

he solidity language continues to pursue more efficient gas optimization schemes. Adopting a [newer version of solidity](https://github.com/ethereum/solc-js/tags) can be more gas efficient.

*There are 26 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/Vultisig.sol

2: pragma solidity ^0.8.24;

```


*GitHub* : [2](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Vultisig.sol#L2-L2)

```solidity
📁 File: hardhat-vultisig/contracts/Whitelist.sol

2: pragma solidity ^0.8.24;

```


*GitHub* : [2](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L2-L2)

```solidity
📁 File: hardhat-vultisig/contracts/extensions/VultisigWhitelisted.sol

2: pragma solidity ^0.8.24;

```


*GitHub* : [2](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/extensions/VultisigWhitelisted.sol#L2-L2)

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol

2: pragma solidity ^0.8.24;

```


*GitHub* : [2](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol#L2-L2)

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/FullMath.sol

2: pragma solidity >=0.4.0;

```


*GitHub* : [2](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/FullMath.sol#L2-L2)

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol

2: pragma solidity >=0.5.0;

```


*GitHub* : [2](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol#L2-L2)

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol

2: pragma solidity >=0.5.0;

```


*GitHub* : [2](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L2-L2)

```solidity
📁 File: src/ILOManager.sol

2: pragma solidity =0.7.6;

3: pragma abicoder v2;

```


*GitHub* : [2](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L2-L2), [3](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L3-L3)

```solidity
📁 File: src/ILOPool.sol

2: pragma solidity =0.7.6;

3: pragma abicoder v2;

```


*GitHub* : [2](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L2-L2), [3](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L3-L3)

```solidity
📁 File: src/base/ILOPoolImmutableState.sol

2: pragma solidity =0.7.6;

```


*GitHub* : [2](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOPoolImmutableState.sol#L2-L2)

```solidity
📁 File: src/base/ILOVest.sol

3: pragma solidity =0.7.6;

```


*GitHub* : [3](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L3-L3)

```solidity
📁 File: src/base/ILOWhitelist.sol

3: pragma solidity =0.7.6;

```


*GitHub* : [3](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOWhitelist.sol#L3-L3)

```solidity
📁 File: src/base/Initializable.sol

3: pragma solidity =0.7.6;

```


*GitHub* : [3](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/Initializable.sol#L3-L3)

```solidity
📁 File: src/base/LiquidityManagement.sol

2: pragma solidity =0.7.6;

3: pragma abicoder v2;

```


*GitHub* : [2](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/LiquidityManagement.sol#L2-L2), [3](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/LiquidityManagement.sol#L3-L3)

```solidity
📁 File: src/base/Multicall.sol

2: pragma solidity =0.7.6;

3: pragma abicoder v2;

```


*GitHub* : [2](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/Multicall.sol#L2-L2), [3](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/Multicall.sol#L3-L3)

```solidity
📁 File: src/base/PeripheryPayments.sol

2: pragma solidity >=0.7.5;

```


*GitHub* : [2](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/PeripheryPayments.sol#L2-L2)

```solidity
📁 File: src/libraries/ChainId.sol

2: pragma solidity >=0.7.0;

```


*GitHub* : [2](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/ChainId.sol#L2-L2)

```solidity
📁 File: src/libraries/LiquidityAmounts.sol

2: pragma solidity >=0.5.0;

```


*GitHub* : [2](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/LiquidityAmounts.sol#L2-L2)

```solidity
📁 File: src/libraries/PoolAddress.sol

2: pragma solidity >=0.5.0;

```


*GitHub* : [2](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/PoolAddress.sol#L2-L2)

```solidity
📁 File: src/libraries/PositionKey.sol

2: pragma solidity >=0.5.0;

```


*GitHub* : [2](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/PositionKey.sol#L2-L2)

```solidity
📁 File: src/libraries/SqrtPriceMathPartial.sol

2: pragma solidity >=0.5.0;

```


*GitHub* : [2](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/SqrtPriceMathPartial.sol#L2-L2)

```solidity
📁 File: src/libraries/TransferHelper.sol

2: pragma solidity >=0.6.0;

```


*GitHub* : [2](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/TransferHelper.sol#L2-L2)

### [G-44]<a name="g-44"></a> Splitting `require()` statements that use `&&` saves gas



*There are 8 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol

63:         require(sqrtPriceX96 >= MIN_SQRT_RATIO && sqrtPriceX96 < MAX_SQRT_RATIO, "R");

```


*GitHub* : [63](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L63-L63)

```solidity
📁 File: src/ILOManager.sol

77:             require(params.start < params.end && params.end < _project.launchTime, "PT");

90:         require(sqrtRatioLowerX96 < _project.initialPoolPriceX96 && sqrtRatioLowerX96 < sqrtRatioUpperX96, "RANGE");

```


*GitHub* : [77](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L77-L77), [90](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L90-L90)

```solidity
📁 File: src/ILOPool.sol

134:         require(block.timestamp > saleInfo.start && block.timestamp < saleInfo.end, "ST");

```


*GitHub* : [134](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L134-L134)

```solidity
📁 File: src/base/LiquidityManagement.sol

56:         require(amount0 >= params.amount0Min && amount1 >= params.amount1Min, 'Price slippage check');

```


*GitHub* : [56](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/LiquidityManagement.sol#L56-L56)

```solidity
📁 File: src/libraries/TransferHelper.sol

21:         require(success && (data.length == 0 || abi.decode(data, (bool))), 'STF');

35:         require(success && (data.length == 0 || abi.decode(data, (bool))), 'ST');

49:         require(success && (data.length == 0 || abi.decode(data, (bool))), 'SA');

```


*GitHub* : [21](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/TransferHelper.sol#L21-L21), [35](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/TransferHelper.sol#L35-L35), [49](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/TransferHelper.sol#L49-L49)

### [G-45]<a name="g-45"></a> `address(this)` can be stored in state variable that will ultimately cost less, than every time calculating this, specifically when it used multiple times in a contract



*There are 12 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/Vultisig.sol

21:         IApproveAndCallReceiver(spender).receiveApproval(msg.sender, amount, address(this), extraData);

```


*GitHub* : [21](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Vultisig.sol#L21-L21)

```solidity
📁 File: src/ILOPool.sol

173:         TransferHelper.safeTransferFrom(RAISE_TOKEN, msg.sender, address(this), raiseAmount);

210:             bytes32 positionKey = PositionKey.compute(address(this), TICK_LOWER, TICK_UPPER);

243:             address(this),

249:         emit Collect(tokenId, address(this), amountCollected0, amountCollected1);

368:         refundAmount = IERC20(SALE_TOKEN).balanceOf(address(this));

```


*GitHub* : [173](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L173-L173), [210](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L210-L210), [243](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L243-L243), [249](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L249-L249), [368](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L368-L368)

```solidity
📁 File: src/base/LiquidityManagement.sol

27:         if (amount0Owed > 0) pay(_cachedPoolKey.token0, address(this), msg.sender, amount0Owed);

28:         if (amount1Owed > 0) pay(_cachedPoolKey.token1, address(this), msg.sender, amount1Owed);

49:             address(this),

```


*GitHub* : [27](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/LiquidityManagement.sol#L27-L27), [28](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/LiquidityManagement.sol#L28-L28), [49](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/LiquidityManagement.sol#L49-L49)

```solidity
📁 File: src/base/Multicall.sol

14:             (bool success, bytes memory result) = address(this).delegatecall(data[i]);

```


*GitHub* : [14](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/Multicall.sol#L14-L14)

```solidity
📁 File: src/base/PeripheryPayments.sol

27:         if (token == WETH9 && address(this).balance >= value) {

31:         } else if (payer == address(this)) {

```


*GitHub* : [27](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/PeripheryPayments.sol#L27-L27), [31](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/PeripheryPayments.sol#L31-L31)

### [G-46]<a name="g-46"></a> Stack variable cost less than state variables while used in emiting event

When emitting events in Solidity, using stack variables (local variables within a function) instead of state variables can lead to significant gas savings. Stack variables reside in memory only for the duration of the function execution and are less costly to access compared to state variables, which are stored on the blockchain. When an event is emitted, accessing these stack variables requires less gas than fetching data from state variables, which involves reading from the contract's storage - a more expensive operation. Thus, for efficiency, prefer using local variables within functions for event emission, especially in functions that are called frequently.

*There are 5 instance(s) of this issue:*

```solidity
📁 File: src/ILOManager.sol

// @audit  _cachedProject
64:         emit ProjectCreated(uniV3PoolAddress, _cachedProject[uniV3PoolAddress]);

// @audit  _initializedILOPools
85:             emit ILOPoolCreated(_project.uniV3PoolAddress, iloPoolAddress, _initializedILOPools[params.uniV3Pool].length);

// @audit  ILO_POOL_IMPLEMENTATION
165:         emit PoolImplementationChanged(ILO_POOL_IMPLEMENTATION, iloPoolImplementation);

// @audit  DEFAULT_DEADLINE_OFFSET
176:         emit DefaultDeadlineOffsetChanged(owner(), DEFAULT_DEADLINE_OFFSET, defaultDeadlineOffset);

```


*GitHub* : [64](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L64-L64), [85](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L85-L85), [165](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L165-L165), [176](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L176-L176)

```solidity
📁 File: src/ILOPool.sol

// @audit  saleInfo
96:         emit ILOPoolInitialized(
97:             params.uniV3Pool,
98:             TICK_LOWER,
99:             TICK_UPPER,
100:             saleInfo,
101:             params.vestingConfigs
102:         );

```


*GitHub* : [96](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L96-L102)

### [G-47]<a name="g-47"></a> Mappings are cheaper to use than storage arrays

When using storage arrays, solidity adds an internal lookup of the array's length (a Gcoldsload **2100 gas**) to ensure you don't read past the array's end. You can avoid this lookup by using a `mapping` and storing the number of entries in a separate storage variable. In cases where you have sentinel values (e.g. 'zero' means invalid), you can avoid length checks

*There are 1 instance(s) of this issue:*

```solidity
📁 File: src/ILOPool.sol

44:     VestingConfig[] private _vestingConfigs;

```


*GitHub* : [44](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L44-L44)

### [G-48]<a name="g-48"></a> Gas savings can be achieved by changing the model for assigning value to the structure

Here's an example to illustrate this:

```solidity
struct MyStruct {
  uint256 a;
  uint256 b;
  uint256 c;
}

function assignValuesToStruct(uint256 _a, uint256 _b, uint256 _c) public {
  MyStruct memory myStruct = MyStruct(_a, _b, _c);
  // Do something with myStruct
}
```

In this example, we have a simple MyStruct data structure with three uint256 fields. The assignValuesToStruct function takes three input parameters _a, _b, and _c, and assigns them to the corresponding fields in a new myStruct variable. This is done using the struct constructor syntax, which creates a new instance of the MyStruct struct with the specified field values.

The following approach can be more efficient than assigning values to the struct fields:

```solidity
function assignValuesToStruct(uint256 _a, uint256 _b, uint256 _c) public {
  MyStruct memory myStruct;
  myStruct.a = _a;
  myStruct.b = _b;
  myStruct.c = _c;
  // Do something with myStruct
}
```

By changing the pattern of assigning value to the structure, gas savings of ~130 per instance are achieved. In addition, this use will provide significant savings in distribution costs.

*There are 2 instance(s) of this issue:*

```solidity
📁 File: src/ILOPool.sol

81:         saleInfo = SaleInfo({
82:             hardCap: params.hardCap,
83:             softCap: params.softCap,
84:             maxCapPerUser: params.maxCapPerUser,
85:             start: params.start,
86:             end: params.end,
87:             maxSaleAmount: maxSaleAmount
88:         });

296:             (amount0, amount1) = addLiquidity(AddLiquidityParams({
297:                 pool: IUniswapV3Pool(uniV3PoolAddress),
298:                 liquidity: liquidity,
299:                 amount0Desired: amount0,
300:                 amount1Desired: amount1,
301:                 amount0Min: amount0Min,
302:                 amount1Min: amount1Min
303:             }));

```


*GitHub* : [81](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L81-L88), [296](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L296-L303)

### [G-49]<a name="g-49"></a> Optimize Storage with Byte Truncation for Time Related State Variables

Storage optimization in Solidity contracts is vital for reducing gas costs, especially when storing time-related state variables. Using `uint32` for storing time values like timestamps is often sufficient, given it can represent dates up to the year 2106. By truncating larger default integer types to `uint32`, you significantly save on storage space and consequently on gas costs for deployment and state modifications. However, ensure that the truncation does not lead to overflow issues and that the variable's size is adequate for the application's expected lifespan and precision requirements. Adopting this optimization practice contributes to more efficient and cost-effective smart contract development.

*There are 4 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol

14:     function consult(address pool, uint32 period) internal view returns (int24 timeWeightedAverageTick) {

```


*GitHub* : [14](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol#L14-L14)

```solidity
📁 File: src/ILOManager.sol

130:         uint64 launchTime,

```


*GitHub* : [130](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L130-L130)

```solidity
📁 File: src/base/ILOVest.sol

17:     function _validateSharesAndVests(uint64 launchTime, VestingConfig[] memory vestingConfigs) internal pure {

35:     function _validateVestSchedule(uint64 launchTime, LinearVest[] memory schedule) internal pure {

```


*GitHub* : [17](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L17-L17), [35](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L35-L35)

### [G-50]<a name="g-50"></a> Trade-offs Between Modifiers and Internal Functions

In Solidity, both modifiers and internal functions can be used to modularize and reuse code, but they have different trade-offs.

Modifiers are primarily used to augment the behavior of functions, often for checks or validations. They can access parameters of the function they modify and are integrated into the function’s code at compile time. This makes them syntactically cleaner for repetitive precondition checks. However, modifiers can sometimes lead to less readable code, especially when the logic is complex or when multiple modifiers are used on a single function.

Internal functions, on the other hand, offer more flexibility. They can contain complex logic, return values, and be called from other functions. This makes them more suitable for reusable chunks of business logic. Since internal functions are separate entities, they can be more readable and easier to test in isolation compared to modifiers.

Using internal functions can result in slightly more gas consumption, as it involves an internal function call. However, this cost is usually minimal and can be a worthwhile trade-off for increased code clarity and maintainability.

In summary, while modifiers offer a concise way to include checks and simple logic across multiple functions, internal functions provide more flexibility and are better suited for complex and reusable code. The choice between the two should be based on the specific use case, considering factors like code complexity, readability, and gas efficiency.

*There are 40 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/extensions/VultisigWhitelisted.sol

28:     function _beforeTokenTransfer(address from, address to, uint256 amount) internal override {

```


*GitHub* : [28](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/extensions/VultisigWhitelisted.sol#L28-L28)

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/FullMath.sol

14:     function mulDiv(uint256 a, uint256 b, uint256 denominator) internal pure returns (uint256 result) {

109:     function mulDivRoundingUp(uint256 a, uint256 b, uint256 denominator) internal pure returns (uint256 result) {

```


*GitHub* : [14](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/FullMath.sol#L14-L14), [109](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/FullMath.sol#L109-L109)

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol

14:     function consult(address pool, uint32 period) internal view returns (int24 timeWeightedAverageTick) {

36:     function getQuoteAtTick(
37:         int24 tick,
38:         uint128 baseAmount,
39:         address baseToken,
40:         address quoteToken
41:     ) internal pure returns (uint256 quoteAmount) {

61:     function getOldestObservationSecondsAgo(address pool) internal view returns (uint32 secondsAgo) {

```


*GitHub* : [14](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol#L14-L14), [36](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol#L36-L41), [61](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol#L61-L61)

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol

23:     function getSqrtRatioAtTick(int24 tick) internal pure returns (uint160 sqrtPriceX96) {

61:     function getTickAtSqrtRatio(uint160 sqrtPriceX96) internal pure returns (int24 tick) {

```


*GitHub* : [23](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L23-L23), [61](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L61-L61)

```solidity
📁 File: src/ILOManager.sol

109:     function _initUniV3PoolIfNecessary(PoolAddress.PoolKey memory poolKey, uint160 sqrtPriceX96) internal returns (address pool) {

124:     function _cacheProject(
125:         address uniV3PoolAddress,
126:         address saleToken,
127:         address raiseToken,
128:         uint24 fee,
129:         uint160 initialPoolPriceX96,
130:         uint64 launchTime,
131:         uint64 refundDeadline
132:     ) internal {

```


*GitHub* : [109](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L109-L109), [124](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L124-L132)

```solidity
📁 File: src/ILOPool.sol

367:     function _refundProject(address projectAdmin) internal returns (uint256 refundAmount) {

382:     function _saleAmountNeeded(uint256 raiseAmount) internal view returns (
383:         uint256 saleAmountNeeded,
384:         uint128 liquidity
385:     ) {

400:     function _unlockedLiquidity(uint256 tokenId) internal view override returns (uint128 liquidityUnlocked) {

438:     function _deductFees(uint256 amount0, uint256 amount1, uint16 feeBPS) internal pure 
439:         returns (
440:             uint256 amount0Left, 
441:             uint256 amount1Left
442:         ) {

457:     function _claimableLiquidity(uint256 tokenId) internal view override returns (uint128) {

```


*GitHub* : [367](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L367-L367), [382](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L382-L385), [400](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L400-L400), [438](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L438-L442), [457](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L457-L457)

```solidity
📁 File: src/base/ILOVest.sol

13:     function _unlockedLiquidity(uint256 tokenId) internal view virtual returns (uint128 liquidityUnlocked);

15:     function _claimableLiquidity(uint256 tokenId) internal view virtual returns (uint128 claimableLiquidity);

17:     function _validateSharesAndVests(uint64 launchTime, VestingConfig[] memory vestingConfigs) internal pure {

35:     function _validateVestSchedule(uint64 launchTime, LinearVest[] memory schedule) internal pure {

```


*GitHub* : [13](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L13-L13), [15](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L15-L15), [17](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L17-L17), [35](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L35-L35)

```solidity
📁 File: src/base/ILOWhitelist.sol

42:     function _setOpenToAll(bool openToAll) internal {

47:     function _removeWhitelist(address user) internal {

52:     function _setWhitelist(address user) internal {

57:     function _isWhitelisted(address user) internal view returns(bool) {

```


*GitHub* : [42](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOWhitelist.sol#L42-L42), [47](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOWhitelist.sol#L47-L47), [52](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOWhitelist.sol#L52-L52), [57](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOWhitelist.sol#L57-L57)

```solidity
📁 File: src/base/Initializable.sol

7:     function _disableInitialize() internal {

```


*GitHub* : [7](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/Initializable.sol#L7-L7)

```solidity
📁 File: src/base/LiquidityManagement.sol

41:     function addLiquidity(AddLiquidityParams memory params)
42:         internal
43:         returns (
44:             uint256 amount0,
45:             uint256 amount1
46:         )
47:     {

```


*GitHub* : [41](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/LiquidityManagement.sol#L41-L47)

```solidity
📁 File: src/base/PeripheryPayments.sol

21:     function pay(
22:         address token,
23:         address payer,
24:         address recipient,
25:         uint256 value
26:     ) internal {

```


*GitHub* : [21](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/PeripheryPayments.sol#L21-L26)

```solidity
📁 File: src/libraries/ChainId.sol

8:     function get() internal pure returns (uint256 chainId) {

```


*GitHub* : [8](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/ChainId.sol#L8-L8)

```solidity
📁 File: src/libraries/LiquidityAmounts.sol

24:     function getLiquidityForAmount0(
25:         uint160 sqrtRatioAX96,
26:         uint160 sqrtRatioBX96,
27:         uint256 amount0
28:     ) internal pure returns (uint128 liquidity) {

40:     function getLiquidityForAmount1(
41:         uint160 sqrtRatioAX96,
42:         uint160 sqrtRatioBX96,
43:         uint256 amount1
44:     ) internal pure returns (uint128 liquidity) {

54:     function getAmount0ForLiquidity(
55:         uint160 sqrtRatioAX96,
56:         uint160 sqrtRatioBX96,
57:         uint128 liquidity
58:     ) internal pure returns (uint256 amount0) {

74:     function getAmount1ForLiquidity(
75:         uint160 sqrtRatioAX96,
76:         uint160 sqrtRatioBX96,
77:         uint128 liquidity
78:     ) internal pure returns (uint256 amount1) {

```


*GitHub* : [24](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/LiquidityAmounts.sol#L24-L28), [40](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/LiquidityAmounts.sol#L40-L44), [54](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/LiquidityAmounts.sol#L54-L58), [74](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/LiquidityAmounts.sol#L74-L78)

```solidity
📁 File: src/libraries/PoolAddress.sol

20:     function getPoolKey(
21:         address tokenA,
22:         address tokenB,
23:         uint24 fee
24:     ) internal pure returns (PoolKey memory) {

33:     function computeAddress(address factory, PoolKey memory key) internal pure returns (address pool) {

```


*GitHub* : [20](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/PoolAddress.sol#L20-L24), [33](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/PoolAddress.sol#L33-L33)

```solidity
📁 File: src/libraries/PositionKey.sol

6:     function compute(
7:         address owner,
8:         int24 tickLower,
9:         int24 tickUpper
10:     ) internal pure returns (bytes32) {

```


*GitHub* : [6](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/PositionKey.sol#L6-L10)

```solidity
📁 File: src/libraries/SqrtPriceMathPartial.sol

20:     function getAmount0Delta(
21:         uint160 sqrtRatioAX96,
22:         uint160 sqrtRatioBX96,
23:         uint128 liquidity,
24:         bool roundUp
25:     ) internal pure returns (uint256 amount0) {

49:     function getAmount1Delta(
50:         uint160 sqrtRatioAX96,
51:         uint160 sqrtRatioBX96,
52:         uint128 liquidity,
53:         bool roundUp
54:     ) internal pure returns (uint256 amount1) {

```


*GitHub* : [20](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/SqrtPriceMathPartial.sol#L20-L25), [49](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/SqrtPriceMathPartial.sol#L49-L54)

```solidity
📁 File: src/libraries/TransferHelper.sol

13:     function safeTransferFrom(
14:         address token,
15:         address from,
16:         address to,
17:         uint256 value
18:     ) internal {

29:     function safeTransfer(
30:         address token,
31:         address to,
32:         uint256 value
33:     ) internal {

43:     function safeApprove(
44:         address token,
45:         address to,
46:         uint256 value
47:     ) internal {

56:     function safeTransferETH(address to, uint256 value) internal {

```


*GitHub* : [13](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/TransferHelper.sol#L13-L18), [29](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/TransferHelper.sol#L29-L33), [43](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/TransferHelper.sol#L43-L47), [56](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/TransferHelper.sol#L56-L56)

### [G-51]<a name="g-51"></a> Use `uint256(1)`/`uint256(2)` instead of `true`/`false` to save gas for changes

Use `uint256(1)` and `uint256(2)` for `true`/`false` to avoid a Gwarmaccess (100 gas), and to avoid Gsset (20000 gas) when changing from `false` to `true`, after having been `true` in the past. Refer to the [source](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/5ae630684a0f57de400ef69499addab4c32ac8fb/contracts/security/ReentrancyGuard.sol#L23-L27).

*There are 7 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/Whitelist.sol

27:     bool private _locked;

29:     bool private _isSelfWhitelistDisabled;

43:     mapping(address => bool) private _isBlacklisted;

```


*GitHub* : [27](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L27-L27), [29](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L29-L29), [43](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L43-L43)

```solidity
📁 File: src/ILOPool.sol

37:     bool private _launchSucceeded;

40:     bool private _refundTriggered;

```


*GitHub* : [37](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L37-L37), [40](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L40-L40)

```solidity
📁 File: src/base/ILOWhitelist.sol

9:     bool private _openToAll;

```


*GitHub* : [9](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOWhitelist.sol#L9-L9)

```solidity
📁 File: src/base/Initializable.sol

6:     bool private _initialized;

```


*GitHub* : [6](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/Initializable.sol#L6-L6)

### [G-52]<a name="g-52"></a> Divisions can be `unchecked` to save gas

The expression `type(int).min/(-1)` is the only case where division causes an overflow. Therefore, uncheck can be used to [save gas](https://gist.github.com/DadeKuma/3bc597338ae774b8b3bd43280d55271f) in scenarios where it is certain that such an overflow will not occur.

*There are 5 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol

45:         return (quotedWETHAmount * baseAmount * 95) / 1e20; // 100 / 1e18

```


*GitHub* : [45](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol#L45-L45)

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol

24:         timeWeightedAverageTick = int24(tickCumulativesDelta / int56(uint56(period)));

```


*GitHub* : [24](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol#L24-L24)

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol

48:         if (tick > 0) ratio = type(uint256).max / ratio;

```


*GitHub* : [48](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L48-L48)

```solidity
📁 File: src/libraries/LiquidityAmounts.sol

62:             FullMath.mulDiv(
63:                 uint256(liquidity) << FixedPoint96.RESOLUTION,
64:                 sqrtRatioBX96 - sqrtRatioAX96,
65:                 sqrtRatioBX96
66:             ) / sqrtRatioAX96;

```


*GitHub* : [62](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/LiquidityAmounts.sol#L62-L66)

```solidity
📁 File: src/libraries/SqrtPriceMathPartial.sol

39:                 : FullMath.mulDiv(numerator1, numerator2, sqrtRatioBX96) / sqrtRatioAX96;

```


*GitHub* : [39](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/SqrtPriceMathPartial.sol#L39-L39)

### [G-53]<a name="g-53"></a> Increments can be `unchecked` to save gas

Using `unchecked` increments can save gas by bypassing the built-in overflow checks. This can save [30-40 gas](https://gist.github.com/hrkrshnn/ee8fabd532058307229d65dcd5836ddc#the-increment-in-for-loop-post-condition-can-be-made-unchecked) per iteration. So it is recommended to use `unchecked` increments when overflow is not possible.

*There are 11 instance(s) of this issue:*

```solidity
📁 File: src/ILOManager.sol

193:         for (uint256 i = 0; i < initializedPools.length; i++) {

204:         for (uint256 i = 0; i < initializedPools.length; i++) {

```


*GitHub* : [193](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L193-L193), [204](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L204-L204)

```solidity
📁 File: src/ILOPool.sol

92:         for (uint256 index = 0; index < params.vestingConfigs.length; index++) {

311:         for (uint256 index = 1; index < _vestingConfigs.length; index++) {

324:             for (uint256 i = 0; i < projectConfig.schedule.length; i++) {

405:         for (uint256 index = 0; index < vestingSchedule.length; index++) {

```


*GitHub* : [92](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L92-L92), [311](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L311-L311), [324](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L324-L324), [405](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L405-L405)

```solidity
📁 File: src/base/ILOVest.sol

20:         for (uint256 i = 0; i < vestingConfigs.length; i++) {

41:         for (uint256 i = 0; i < scheduleLength; i++) {

```


*GitHub* : [20](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L20-L20), [41](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L41-L41)

```solidity
📁 File: src/base/ILOWhitelist.sol

28:         for (uint256 i = 0; i < users.length; i++) {

35:         for (uint256 i = 0; i < users.length; i++) {

```


*GitHub* : [28](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOWhitelist.sol#L28-L28), [35](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOWhitelist.sol#L35-L35)

```solidity
📁 File: src/base/Multicall.sol

13:         for (uint256 i = 0; i < data.length; i++) {

```


*GitHub* : [13](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/Multicall.sol#L13-L13)

### [G-54]<a name="g-54"></a> Avoid unnecessary public variables

Public state variables in Solidity automatically generate getter functions, increasing contract size and potentially leading to higher deployment and interaction costs. To optimize gas usage and contract efficiency, minimize the use of public variables unless external access is necessary. Instead, use internal or private visibility combined with explicit getter functions when required. This practice not only reduces contract size but also provides better control over data access and manipulation, enhancing security and readability. Prioritize lean, efficient contracts to ensure cost-effectiveness and better performance on the blockchain.

*There are 18 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol

16:     uint32 public constant PERIOD = 30 minutes;

18:     uint128 public constant BASE_AMOUNT = 1e18; // VULT has 18 decimals

21:     address public immutable pool;

23:     address public immutable baseToken;

25:     address public immutable WETH;

```


*GitHub* : [16](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol#L16-L16), [18](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol#L18-L18), [21](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol#L21-L21), [23](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol#L23-L23), [25](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol#L25-L25)

```solidity
📁 File: src/ILOManager.sol

16:     address public override UNIV3_FACTORY;

17:     address public override WETH9;

20:     uint16 public override PLATFORM_FEE;

21:     uint16 public override PERFORMANCE_FEE;

22:     address public override FEE_TAKER;

23:     address public override ILO_POOL_IMPLEMENTATION;

```


*GitHub* : [16](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L16-L16), [17](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L17-L17), [20](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L20-L20), [21](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L21-L21), [22](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L22-L22), [23](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L23-L23)

```solidity
📁 File: src/base/ILOPoolImmutableState.sol

11:     address public override WETH9;

14:     address public override MANAGER;

15:     address public override RAISE_TOKEN;

16:     address public override SALE_TOKEN;

17:     int24 public override TICK_LOWER;

18:     int24 public override TICK_UPPER;

19:     uint160 public override SQRT_RATIO_X96;

```


*GitHub* : [11](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOPoolImmutableState.sol#L11-L11), [14](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOPoolImmutableState.sol#L14-L14), [15](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOPoolImmutableState.sol#L15-L15), [16](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOPoolImmutableState.sol#L16-L16), [17](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOPoolImmutableState.sol#L17-L17), [18](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOPoolImmutableState.sol#L18-L18), [19](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOPoolImmutableState.sol#L19-L19)

### [G-55]<a name="g-55"></a> Use `!= 0` instead of `> 0` for unsigned integer comparison

`> 0` is less efficient than `!= 0` for unsigned integers.`!= 0` costs less gas compared to `> 0` for unsigned integers in `require` statements with the optimizer enabled (6 gas). While it may seem that `> 0` is cheaper than `!=`, this is only true without the optimizer enabled and outside a `require` statement. If you enable the optimizer at 10k AND you're in a `require` statement, this will save gas. You can see this tweet for more proofs: https://twitter.com/gzeon/status/1485428085885640706

*There are 10 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/FullMath.sol

30:             require(denominator > 0);

111:         if (mulmod(a, b, denominator) > 0) {

```


*GitHub* : [30](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/FullMath.sol#L30-L30), [111](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/FullMath.sol#L111-L111)

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol

63:         require(observationCardinality > 0, "NI");

```


*GitHub* : [63](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol#L63-L63)

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol

48:         if (tick > 0) ratio = type(uint256).max / ratio;

```


*GitHub* : [48](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L48-L48)

```solidity
📁 File: src/ILOManager.sol

192:         require(initializedPools.length > 0, "NP");

```


*GitHub* : [192](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L192-L192)

```solidity
📁 File: src/ILOPool.sol

161:         require(liquidityDelta > 0, "ZA");

369:         if (refundAmount > 0) {

```


*GitHub* : [161](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L161-L161), [369](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L369-L369)

```solidity
📁 File: src/base/LiquidityManagement.sol

27:         if (amount0Owed > 0) pay(_cachedPoolKey.token0, address(this), msg.sender, amount0Owed);

28:         if (amount1Owed > 0) pay(_cachedPoolKey.token1, address(this), msg.sender, amount1Owed);

```


*GitHub* : [27](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/LiquidityManagement.sol#L27-L27), [28](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/LiquidityManagement.sol#L28-L28)

```solidity
📁 File: src/libraries/SqrtPriceMathPartial.sol

31:         require(sqrtRatioAX96 > 0);

```


*GitHub* : [31](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/SqrtPriceMathPartial.sol#L31-L31)

### [G-56]<a name="g-56"></a> Unused non-constant state variables waste gas

If the variable is assigned a non-zero value, saves Gsset (20000 gas). If it's assigned a zero value, saves Gsreset (2900 gas). If the variable remains unassigned, there is no gas savings unless the variable is `public`, in which case the compiler-generated non-payable getter deployment cost is saved. If the state variable is overriding an interface's public function, mark the variable as `constant` or `immutable` so that it does not use a storage slot.

*There are 11 instance(s) of this issue:*

```solidity
📁 File: src/base/ILOPoolImmutableState.sol

11:     address public override WETH9;

14:     address public override MANAGER;

15:     address public override RAISE_TOKEN;

16:     address public override SALE_TOKEN;

17:     int24 public override TICK_LOWER;

18:     int24 public override TICK_UPPER;

19:     uint160 public override SQRT_RATIO_X96;

20:     uint160 internal SQRT_RATIO_LOWER_X96;

21:     uint160 internal SQRT_RATIO_UPPER_X96;

23:     PoolAddress.PoolKey internal _cachedPoolKey;

24:     address internal _cachedUniV3PoolAddress;

```


*GitHub* : [11](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOPoolImmutableState.sol#L11-L11), [14](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOPoolImmutableState.sol#L14-L14), [15](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOPoolImmutableState.sol#L15-L15), [16](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOPoolImmutableState.sol#L16-L16), [17](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOPoolImmutableState.sol#L17-L17), [18](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOPoolImmutableState.sol#L18-L18), [19](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOPoolImmutableState.sol#L19-L19), [20](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOPoolImmutableState.sol#L20-L20), [21](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOPoolImmutableState.sol#L21-L21), [23](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOPoolImmutableState.sol#L23-L23), [24](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOPoolImmutableState.sol#L24-L24)

### [G-57]<a name="g-57"></a> Using assembly to check for `address(0)` can save gas

Using assembly to check for `address(0)` can save gas by allowing more direct access to the evm and reducing some of the overhead associated with high-level operations in solidity.

*There are 6 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/extensions/VultisigWhitelisted.sol

29:         if (_whitelistContract != address(0)) {

```


*GitHub* : [29](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/extensions/VultisigWhitelisted.sol#L29-L29)

```solidity
📁 File: src/ILOManager.sol

75:             require(_project.uniV3PoolAddress != address(0), "NI");

111:         if (pool == address(0)) {

134:         require(_project.uniV3PoolAddress == address(0), "RE");

```


*GitHub* : [75](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L75-L75), [111](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L111-L111), [134](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L134-L134)

```solidity
📁 File: src/base/ILOVest.sol

22:                 require (vestingConfigs[i].recipient == address(0), "VR");

24:                 require(vestingConfigs[i].recipient != address(0), "VR");

```


*GitHub* : [22](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L22-L22), [24](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L24-L24)

### [G-58]<a name="g-58"></a> Use assembly to `emit` events

To efficiently `emit` events, it's possible to utilize assembly by making use of scratch space and the free memory pointer. This approach has the advantage of potentially avoiding the costs associated with memory expansion.
However, it's important to note that in order to safely optimize this process, it is preferable to cache and restore the free memory pointer.
A good example of such practice can be seen in [Solady's](https://github.com/Vectorized/solady/blob/main/src/tokens/ERC1155.sol#L167) codebase.

*There are 19 instance(s) of this issue:*

```solidity
📁 File: src/ILOManager.sol

64:         emit ProjectCreated(uniV3PoolAddress, _cachedProject[uniV3PoolAddress]);

85:             emit ILOPoolCreated(_project.uniV3PoolAddress, iloPoolAddress, _initializedILOPools[params.uniV3Pool].length);

165:         emit PoolImplementationChanged(ILO_POOL_IMPLEMENTATION, iloPoolImplementation);

172:         emit ProjectAdminChanged(uniV3Pool, msg.sender, admin);

176:         emit DefaultDeadlineOffsetChanged(owner(), DEFAULT_DEADLINE_OFFSET, defaultDeadlineOffset);

182:         emit RefundDeadlineChanged(uniV3Pool, _project.refundDeadline, refundDeadline);

197:         emit ProjectLaunch(uniV3PoolAddress);

```


*GitHub* : [64](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L64-L64), [85](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L85-L85), [165](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L165-L165), [172](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L172-L172), [176](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L176-L176), [182](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L182-L182), [197](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L197-L197)

```solidity
📁 File: src/ILOPool.sol

96:         emit ILOPoolInitialized(
97:             params.uniV3Pool,
98:             TICK_LOWER,
99:             TICK_UPPER,
100:             saleInfo,
101:             params.vestingConfigs
102:         );

175:         emit Buy(recipient, tokenId, raiseAmount, liquidityDelta);

238:             emit DecreaseLiquidity(tokenId, liquidity2Claim, amount0, amount1);

249:         emit Collect(tokenId, address(this), amountCollected0, amountCollected1);

255:         emit Claim(ownerOf(tokenId), tokenId,liquidity2Claim, amount0, amount1, position.feeGrowthInside0LastX128, position.feeGrowthInside1LastX128);

305:             emit PoolLaunch(uniV3PoolAddress, liquidity, amount0, amount1);

328:             emit Buy(projectConfig.recipient, tokenId, 0, liquidityShares);

359:         emit UserRefund(tokenOwner, tokenId,refundAmount);

371:             emit ProjectRefund(projectAdmin, refundAmount);

```


*GitHub* : [96](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L96-L102), [175](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L175-L175), [238](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L238-L238), [249](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L249-L249), [255](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L255-L255), [305](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L305-L305), [328](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L328-L328), [359](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L359-L359), [371](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L371-L371)

```solidity
📁 File: src/base/ILOWhitelist.sol

44:         emit SetOpenToAll(openToAll);

49:         emit SetWhitelist(user, false);

54:         emit SetWhitelist(user, true);

```


*GitHub* : [44](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOWhitelist.sol#L44-L44), [49](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOWhitelist.sol#L49-L49), [54](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOWhitelist.sol#L54-L54)

### [G-59]<a name="g-59"></a> Use assembly to validate `msg.sender`

We can use assembly to efficiently validate `msg.sender` with the least amount of opcodes necessary. For more details check the following report [Here](https://code4rena.com/reports/2023-05-juicebox#g-06-use-assembly-to-validate-msgsender)

*There are 5 instance(s) of this issue:*

```solidity
📁 File: src/ILOManager.sol

52:         require(_cachedProject[uniV3Pool].admin == msg.sender, "UA");

```


*GitHub* : [52](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L52-L52)

```solidity
📁 File: src/ILOPool.sol

264:         require(msg.sender == MANAGER, "UA");

465:         require(msg.sender == _project.admin, "UA");

```


*GitHub* : [264](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L264-L264), [465](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L465-L465)

```solidity
📁 File: src/base/LiquidityManagement.sol

25:         require(msg.sender == _cachedUniV3PoolAddress);

```


*GitHub* : [25](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/LiquidityManagement.sol#L25-L25)

```solidity
📁 File: src/base/PeripheryPayments.sol

14:         require(msg.sender == WETH9, 'Not WETH9');

```


*GitHub* : [14](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/PeripheryPayments.sol#L14-L14)

### [G-60]<a name="g-60"></a> Simple checks for zero can be done using assembly to save gas



*There are 48 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/Whitelist.sol

216:             if (_allowedWhitelistIndex == 0 || _whitelistIndex[to] > _allowedWhitelistIndex) {

233:         if (_whitelistIndex[whitelisted] == 0) {

```


*GitHub* : [216](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L216-L216), [233](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L233-L233)

```solidity
📁 File: hardhat-vultisig/contracts/extensions/VultisigWhitelisted.sol

29:         if (_whitelistContract != address(0)) {

```


*GitHub* : [29](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/extensions/VultisigWhitelisted.sol#L29-L29)

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/FullMath.sol

29:         if (prod1 == 0) {

30:             require(denominator > 0);

111:         if (mulmod(a, b, denominator) > 0) {

```


*GitHub* : [29](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/FullMath.sol#L29-L29), [30](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/FullMath.sol#L30-L30), [111](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/FullMath.sol#L111-L111)

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol

15:         require(period != 0, "BP");

27:         if (tickCumulativesDelta < 0 && (tickCumulativesDelta % int56(uint56(period)) != 0)) timeWeightedAverageTick--;

63:         require(observationCardinality > 0, "NI");

```


*GitHub* : [15](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol#L15-L15), [27](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol#L27-L27), [63](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol#L63-L63)

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol

24:         uint256 absTick = tick < 0 ? uint256(-int256(tick)) : uint256(int256(tick));

27:         uint256 ratio = absTick & 0x1 != 0 ? 0xfffcb933bd6fad37aa2d162d1a594001 : 0x100000000000000000000000000000000;

28:         if (absTick & 0x2 != 0) ratio = (ratio * 0xfff97272373d413259a46990580e213a) >> 128;

29:         if (absTick & 0x4 != 0) ratio = (ratio * 0xfff2e50f5f656932ef12357cf3c7fdcc) >> 128;

30:         if (absTick & 0x8 != 0) ratio = (ratio * 0xffe5caca7e10e4e61c3624eaa0941cd0) >> 128;

31:         if (absTick & 0x10 != 0) ratio = (ratio * 0xffcb9843d60f6159c9db58835c926644) >> 128;

32:         if (absTick & 0x20 != 0) ratio = (ratio * 0xff973b41fa98c081472e6896dfb254c0) >> 128;

33:         if (absTick & 0x40 != 0) ratio = (ratio * 0xff2ea16466c96a3843ec78b326b52861) >> 128;

34:         if (absTick & 0x80 != 0) ratio = (ratio * 0xfe5dee046a99a2a811c461f1969c3053) >> 128;

35:         if (absTick & 0x100 != 0) ratio = (ratio * 0xfcbe86c7900a88aedcffc83b479aa3a4) >> 128;

36:         if (absTick & 0x200 != 0) ratio = (ratio * 0xf987a7253ac413176f2b074cf7815e54) >> 128;

37:         if (absTick & 0x400 != 0) ratio = (ratio * 0xf3392b0822b70005940c7a398e4b70f3) >> 128;

38:         if (absTick & 0x800 != 0) ratio = (ratio * 0xe7159475a2c29b7443b29c7fa6e889d9) >> 128;

39:         if (absTick & 0x1000 != 0) ratio = (ratio * 0xd097f3bdfd2022b8845ad8f792aa5825) >> 128;

40:         if (absTick & 0x2000 != 0) ratio = (ratio * 0xa9f746462d870fdf8a65dc1f90e061e5) >> 128;

41:         if (absTick & 0x4000 != 0) ratio = (ratio * 0x70d869a156d2a1b890bb3df62baf32f7) >> 128;

42:         if (absTick & 0x8000 != 0) ratio = (ratio * 0x31be135f97d08fd981231505542fcfa6) >> 128;

43:         if (absTick & 0x10000 != 0) ratio = (ratio * 0x9aa508b5b7a84e1c677de54f3e99bc9) >> 128;

44:         if (absTick & 0x20000 != 0) ratio = (ratio * 0x5d6af8dedb81196699c329225ee604) >> 128;

45:         if (absTick & 0x40000 != 0) ratio = (ratio * 0x2216e584f5fa1ea926041bedfe98) >> 128;

46:         if (absTick & 0x80000 != 0) ratio = (ratio * 0x48a170391f7dc42444e8fa2) >> 128;

48:         if (tick > 0) ratio = type(uint256).max / ratio;

53:         sqrtPriceX96 = uint160((ratio >> 32) + (ratio % (1 << 32) == 0 ? 0 : 1));

```


*GitHub* : [24](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L24-L24), [27](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L27-L27), [28](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L28-L28), [29](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L29-L29), [30](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L30-L30), [31](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L31-L31), [32](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L32-L32), [33](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L33-L33), [34](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L34-L34), [35](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L35-L35), [36](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L36-L36), [37](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L37-L37), [38](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L38-L38), [39](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L39-L39), [40](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L40-L40), [41](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L41-L41), [42](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L42-L42), [43](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L43-L43), [44](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L44-L44), [45](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L45-L45), [46](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L46-L46), [48](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L48-L48), [53](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L53-L53)

```solidity
📁 File: src/ILOManager.sol

75:             require(_project.uniV3PoolAddress != address(0), "NI");

111:         if (pool == address(0)) {

116:             if (sqrtPriceX96Existing == 0) {

134:         require(_project.uniV3PoolAddress == address(0), "RE");

192:         require(initializedPools.length > 0, "NP");

```


*GitHub* : [75](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L75-L75), [111](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L111-L111), [116](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L116-L116), [134](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L134-L134), [192](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L192-L192)

```solidity
📁 File: src/ILOPool.sol

143:         if (balanceOf(recipient) == 0) {

161:         require(liquidityDelta > 0, "ZA");

369:         if (refundAmount > 0) {

386:         if (raiseAmount == 0) return (0, 0);

```


*GitHub* : [143](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L143-L143), [161](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L161-L161), [369](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L369-L369), [386](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L386-L386)

```solidity
📁 File: src/base/ILOVest.sol

21:             if (i == 0) {

22:                 require (vestingConfigs[i].recipient == address(0), "VR");

24:                 require(vestingConfigs[i].recipient != address(0), "VR");

36:         require(schedule[0].start >= launchTime, "VT");

```


*GitHub* : [21](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L21-L21), [22](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L22-L22), [24](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L24-L24), [36](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L36-L36)

```solidity
📁 File: src/base/LiquidityManagement.sol

27:         if (amount0Owed > 0) pay(_cachedPoolKey.token0, address(this), msg.sender, amount0Owed);

28:         if (amount1Owed > 0) pay(_cachedPoolKey.token1, address(this), msg.sender, amount1Owed);

```


*GitHub* : [27](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/LiquidityManagement.sol#L27-L27), [28](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/LiquidityManagement.sol#L28-L28)

```solidity
📁 File: src/libraries/SqrtPriceMathPartial.sol

31:         require(sqrtRatioAX96 > 0);

```


*GitHub* : [31](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/SqrtPriceMathPartial.sol#L31-L31)

### [G-61]<a name="g-61"></a> Use assembly in place of `abi.decode` to extract calldata values more efficiently

Using inline assembly to extract calldata values can be more gas-efficient than using `abi.decode` in Solidity. Inline assembly gives more direct access to EVM operations, enabling optimized usage of calldata. However, assembly should be used judiciously as it's more prone to errors. Opt for this approach when performance is critical and the complexity it introduces is manageable

*There are 4 instance(s) of this issue:*

```solidity
📁 File: src/base/Multicall.sol

22:                 revert(abi.decode(result, (string)));

```


*GitHub* : [22](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/Multicall.sol#L22-L22)

```solidity
📁 File: src/libraries/TransferHelper.sol

21:         require(success && (data.length == 0 || abi.decode(data, (bool))), 'STF');

35:         require(success && (data.length == 0 || abi.decode(data, (bool))), 'ST');

49:         require(success && (data.length == 0 || abi.decode(data, (bool))), 'SA');

```


*GitHub* : [21](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/TransferHelper.sol#L21-L21), [35](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/TransferHelper.sol#L35-L35), [49](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/TransferHelper.sol#L49-L49)

### [G-62]<a name="g-62"></a> Use `byte32` in place of `string`

For strings of 32 char strings and below you can use bytes32 instead as it's more gas efficient

*There are 4 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol

34:     function name() external pure returns (string memory) {

```


*GitHub* : [34](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol#L34-L34)

```solidity
📁 File: src/ILOPool.sol

53:     function name() public pure override(ERC721, IERC721Metadata) returns (string memory) {

57:     function symbol() public pure override(ERC721, IERC721Metadata) returns (string memory) {

```


*GitHub* : [53](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L53-L53), [57](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L57-L57)

```solidity
📁 File: src/base/Multicall.sol

22:                 revert(abi.decode(result, (string)));

```


*GitHub* : [22](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/Multicall.sol#L22-L22)

### [G-63]<a name="g-63"></a> `internal` functions not called by the contract should be removed to save deployment gas



*There are 26 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/extensions/VultisigWhitelisted.sol

28:     function _beforeTokenTransfer(address from, address to, uint256 amount) internal override {

```


*GitHub* : [28](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/extensions/VultisigWhitelisted.sol#L28-L28)

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/FullMath.sol

109:     function mulDivRoundingUp(uint256 a, uint256 b, uint256 denominator) internal pure returns (uint256 result) {

```


*GitHub* : [109](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/FullMath.sol#L109-L109)

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol

14:     function consult(address pool, uint32 period) internal view returns (int24 timeWeightedAverageTick) {

36:     function getQuoteAtTick(
37:         int24 tick,
38:         uint128 baseAmount,
39:         address baseToken,
40:         address quoteToken
41:     ) internal pure returns (uint256 quoteAmount) {

61:     function getOldestObservationSecondsAgo(address pool) internal view returns (uint32 secondsAgo) {

```


*GitHub* : [14](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol#L14-L14), [36](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol#L36-L41), [61](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol#L61-L61)

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol

61:     function getTickAtSqrtRatio(uint160 sqrtPriceX96) internal pure returns (int24 tick) {

```


*GitHub* : [61](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L61-L61)

```solidity
📁 File: src/base/ILOVest.sol

13:     function _unlockedLiquidity(uint256 tokenId) internal view virtual returns (uint128 liquidityUnlocked);

15:     function _claimableLiquidity(uint256 tokenId) internal view virtual returns (uint128 claimableLiquidity);

17:     function _validateSharesAndVests(uint64 launchTime, VestingConfig[] memory vestingConfigs) internal pure {

```


*GitHub* : [13](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L13-L13), [15](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L15-L15), [17](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L17-L17)

```solidity
📁 File: src/base/Initializable.sol

7:     function _disableInitialize() internal {

```


*GitHub* : [7](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/Initializable.sol#L7-L7)

```solidity
📁 File: src/base/LiquidityManagement.sol

41:     function addLiquidity(AddLiquidityParams memory params)
42:         internal
43:         returns (
44:             uint256 amount0,
45:             uint256 amount1
46:         )
47:     {

```


*GitHub* : [41](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/LiquidityManagement.sol#L41-L47)

```solidity
📁 File: src/base/PeripheryPayments.sol

21:     function pay(
22:         address token,
23:         address payer,
24:         address recipient,
25:         uint256 value
26:     ) internal {

```


*GitHub* : [21](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/PeripheryPayments.sol#L21-L26)

```solidity
📁 File: src/libraries/ChainId.sol

8:     function get() internal pure returns (uint256 chainId) {

```


*GitHub* : [8](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/ChainId.sol#L8-L8)

```solidity
📁 File: src/libraries/LiquidityAmounts.sol

24:     function getLiquidityForAmount0(
25:         uint160 sqrtRatioAX96,
26:         uint160 sqrtRatioBX96,
27:         uint256 amount0
28:     ) internal pure returns (uint128 liquidity) {

40:     function getLiquidityForAmount1(
41:         uint160 sqrtRatioAX96,
42:         uint160 sqrtRatioBX96,
43:         uint256 amount1
44:     ) internal pure returns (uint128 liquidity) {

54:     function getAmount0ForLiquidity(
55:         uint160 sqrtRatioAX96,
56:         uint160 sqrtRatioBX96,
57:         uint128 liquidity
58:     ) internal pure returns (uint256 amount0) {

74:     function getAmount1ForLiquidity(
75:         uint160 sqrtRatioAX96,
76:         uint160 sqrtRatioBX96,
77:         uint128 liquidity
78:     ) internal pure returns (uint256 amount1) {

```


*GitHub* : [24](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/LiquidityAmounts.sol#L24-L28), [40](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/LiquidityAmounts.sol#L40-L44), [54](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/LiquidityAmounts.sol#L54-L58), [74](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/LiquidityAmounts.sol#L74-L78)

```solidity
📁 File: src/libraries/PoolAddress.sol

20:     function getPoolKey(
21:         address tokenA,
22:         address tokenB,
23:         uint24 fee
24:     ) internal pure returns (PoolKey memory) {

33:     function computeAddress(address factory, PoolKey memory key) internal pure returns (address pool) {

```


*GitHub* : [20](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/PoolAddress.sol#L20-L24), [33](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/PoolAddress.sol#L33-L33)

```solidity
📁 File: src/libraries/PositionKey.sol

6:     function compute(
7:         address owner,
8:         int24 tickLower,
9:         int24 tickUpper
10:     ) internal pure returns (bytes32) {

```


*GitHub* : [6](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/PositionKey.sol#L6-L10)

```solidity
📁 File: src/libraries/SqrtPriceMathPartial.sol

20:     function getAmount0Delta(
21:         uint160 sqrtRatioAX96,
22:         uint160 sqrtRatioBX96,
23:         uint128 liquidity,
24:         bool roundUp
25:     ) internal pure returns (uint256 amount0) {

49:     function getAmount1Delta(
50:         uint160 sqrtRatioAX96,
51:         uint160 sqrtRatioBX96,
52:         uint128 liquidity,
53:         bool roundUp
54:     ) internal pure returns (uint256 amount1) {

```


*GitHub* : [20](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/SqrtPriceMathPartial.sol#L20-L25), [49](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/SqrtPriceMathPartial.sol#L49-L54)

```solidity
📁 File: src/libraries/TransferHelper.sol

13:     function safeTransferFrom(
14:         address token,
15:         address from,
16:         address to,
17:         uint256 value
18:     ) internal {

29:     function safeTransfer(
30:         address token,
31:         address to,
32:         uint256 value
33:     ) internal {

43:     function safeApprove(
44:         address token,
45:         address to,
46:         uint256 value
47:     ) internal {

56:     function safeTransferETH(address to, uint256 value) internal {

```


*GitHub* : [13](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/TransferHelper.sol#L13-L18), [29](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/TransferHelper.sol#L29-L33), [43](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/TransferHelper.sol#L43-L47), [56](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/TransferHelper.sol#L56-L56)

### [G-64]<a name="g-64"></a> Use `x = x + y` instead of `x += y` for state variables

Using `x = x + y` instead of `x += y` for simple state variables can save 10 gas. The same applies to `-=` , `*=` , etc.

*There are 3 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/Whitelist.sol

226:             _contributed[to] += estimatedETHAmount;

```


*GitHub* : [226](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L226-L226)

```solidity
📁 File: src/ILOManager.sol

205:             totalRefundAmount += IILOPool(initializedPools[i]).claimProjectRefund(_cachedProject[uniV3PoolAddress].admin);

```


*GitHub* : [205](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L205-L205)

```solidity
📁 File: src/ILOPool.sol

137:         totalRaised += raiseAmount;

```


*GitHub* : [137](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L137-L137)

### [G-65]<a name="g-65"></a> Use solady library where possible to save gas

The following OpenZeppelin imports have a Solady equivalent, as such they can be used to save GAS as Solady modules have been specifically designed to be as GAS efficient as possible

*There are 9 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/Vultisig.sol

4: import {ERC20} from "@openzeppelin/contracts/token/ERC20/ERC20.sol";

5: import {Ownable} from "@openzeppelin/contracts/access/Ownable.sol";

```


*GitHub* : [4](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Vultisig.sol#L4-L4), [5](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Vultisig.sol#L5-L5)

```solidity
📁 File: hardhat-vultisig/contracts/Whitelist.sol

4: import {Ownable} from "@openzeppelin/contracts/access/Ownable.sol";

```


*GitHub* : [4](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L4-L4)

```solidity
📁 File: src/ILOManager.sol

12: import "@openzeppelin/contracts/access/Ownable.sol";

13: import '@openzeppelin/contracts/proxy/Clones.sol';

```


*GitHub* : [12](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L12-L12), [13](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L13-L13)

```solidity
📁 File: src/ILOPool.sol

9: import '@openzeppelin/contracts/token/ERC721/ERC721.sol';

```


*GitHub* : [9](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L9-L9)

```solidity
📁 File: src/base/ILOWhitelist.sol

5: import '@openzeppelin/contracts/utils/EnumerableSet.sol';

```


*GitHub* : [5](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOWhitelist.sol#L5-L5)

```solidity
📁 File: src/base/PeripheryPayments.sol

4: import '@openzeppelin/contracts/token/ERC20/IERC20.sol';

```


*GitHub* : [4](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/PeripheryPayments.sol#L4-L4)

```solidity
📁 File: src/libraries/TransferHelper.sol

4: import '@openzeppelin/contracts/token/ERC20/IERC20.sol';

```


*GitHub* : [4](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/TransferHelper.sol#L4-L4)

### [G-66]<a name="g-66"></a> Using bools for `storage` incurs overhead

[Booleans are more expensive than uint256](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/58f635312aa21f947cae5f8578638a85aa2519f5/contracts/security/ReentrancyGuard.sol#L23-L27) or any type that takes up a full word because each write operation emits an extra `SLOAD` to first read the slot's contents, replace the bits taken up by the boolean, and then write back. This is the compiler's defense against contract upgrades and pointer aliasing, and it cannot be disabled. Use `uint256(0)` and `uint256(1)` for `true`/`false` to avoid a Gwarmaccess ([100 gas](https://gist.github.com/IllIllI000/1b70014db712f8572a72378321250058)) for the extra `SLOAD`.

*There are 6 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/Whitelist.sol

27:     bool private _locked;

29:     bool private _isSelfWhitelistDisabled;

```


*GitHub* : [27](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L27-L27), [29](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L29-L29)

```solidity
📁 File: src/ILOPool.sol

37:     bool private _launchSucceeded;

40:     bool private _refundTriggered;

```


*GitHub* : [37](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L37-L37), [40](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L40-L40)

```solidity
📁 File: src/base/ILOWhitelist.sol

9:     bool private _openToAll;

```


*GitHub* : [9](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOWhitelist.sol#L9-L9)

```solidity
📁 File: src/base/Initializable.sol

6:     bool private _initialized;

```


*GitHub* : [6](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/Initializable.sol#L6-L6)

### [G-67]<a name="g-67"></a> Variable declared within iteration

Please elaborate and generalise the following with detail and feel free to use your own knowledge and lmit ur words to 100 words please:

*There are 8 instance(s) of this issue:*

```solidity
📁 File: src/ILOPool.sol

312:             uint256 tokenId;

313:             VestingConfig memory projectConfig = _vestingConfigs[index];

316:             uint128 liquidityShares = uint128(FullMath.mulDiv(liquidity, projectConfig.shares, BPS));

318:             Position storage _position = _positions[tokenId];

323:             LinearVest[] storage schedule = _positionVests[tokenId].schedule;

324:             for (uint256 i = 0; i < projectConfig.schedule.length; i++) {

407:             LinearVest storage vest = vestingSchedule[index];

```


*GitHub* : [312](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L312-L312), [313](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L313-L313), [316](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L316-L316), [318](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L318-L318), [323](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L323-L323), [324](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L324-L324), [407](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L407-L407)

```solidity
📁 File: src/base/Multicall.sol

14:             (bool success, bytes memory result) = address(this).delegatecall(data[i]);

```


*GitHub* : [14](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/Multicall.sol#L14-L14)

### [G-68]<a name="g-68"></a> Enable IR-based code generation

Enabling Intermediate Representation (IR)-based code generation in Solidity, via the --via-ir compiler flag or setting {'viaIR': true} in the configuration, activates an advanced optimization phase. This approach allows the compiler to perform more sophisticated optimizations across multiple functions, potentially leading to significant gas savings. IR-based compilation can optimize contract bytecode more efficiently, making smart contracts cheaper to deploy and execute by reducing the gas required for transactions

*There are 22 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/Vultisig.sol

11: contract Vultisig is ERC20, Ownable {

```


*GitHub* : [11](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Vultisig.sol#L11-L11)

```solidity
📁 File: hardhat-vultisig/contracts/Whitelist.sol

16: contract Whitelist is Ownable {

```


*GitHub* : [16](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L16-L16)

```solidity
📁 File: hardhat-vultisig/contracts/extensions/VultisigWhitelisted.sol

12: contract VultisigWhitelisted is Vultisig {

```


*GitHub* : [12](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/extensions/VultisigWhitelisted.sol#L12-L12)

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol

14: contract UniswapV3Oracle is IOracle {

```


*GitHub* : [14](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol#L14-L14)

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/FullMath.sol

7: library FullMath {

```


*GitHub* : [7](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/FullMath.sol#L7-L7)

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol

9: library OracleLibrary {

```


*GitHub* : [9](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol#L9-L9)

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol

7: library TickMath {

```


*GitHub* : [7](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L7-L7)

```solidity
📁 File: src/ILOManager.sol

15: contract ILOManager is IILOManager, Ownable, Initializable {

```


*GitHub* : [15](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L15-L15)

```solidity
📁 File: src/ILOPool.sol

24: contract ILOPool is

```


*GitHub* : [24](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L24-L24)

```solidity
📁 File: src/base/ILOPoolImmutableState.sol

9: abstract contract ILOPoolImmutableState is IILOPoolImmutableState {

```


*GitHub* : [9](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOPoolImmutableState.sol#L9-L9)

```solidity
📁 File: src/base/ILOVest.sol

7: abstract contract ILOVest is IILOVest {

```


*GitHub* : [7](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L7-L7)

```solidity
📁 File: src/base/ILOWhitelist.sol

8: abstract contract ILOWhitelist is IILOWhitelist {

```


*GitHub* : [8](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOWhitelist.sol#L8-L8)

```solidity
📁 File: src/base/Initializable.sol

5: abstract contract Initializable {

```


*GitHub* : [5](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/Initializable.sol#L5-L5)

```solidity
📁 File: src/base/LiquidityManagement.sol

17: abstract contract LiquidityManagement is IUniswapV3MintCallback, ILOPoolImmutableState, PeripheryPayments {

```


*GitHub* : [17](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/LiquidityManagement.sol#L17-L17)

```solidity
📁 File: src/base/Multicall.sol

9: abstract contract Multicall is IMulticall {

```


*GitHub* : [9](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/Multicall.sol#L9-L9)

```solidity
📁 File: src/base/PeripheryPayments.sol

12: abstract contract PeripheryPayments is ILOPoolImmutableState {

```


*GitHub* : [12](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/PeripheryPayments.sol#L12-L12)

```solidity
📁 File: src/libraries/ChainId.sol

5: library ChainId {

```


*GitHub* : [5](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/ChainId.sol#L5-L5)

```solidity
📁 File: src/libraries/LiquidityAmounts.sol

10: library LiquidityAmounts {

```


*GitHub* : [10](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/LiquidityAmounts.sol#L10-L10)

```solidity
📁 File: src/libraries/PoolAddress.sol

5: library PoolAddress {

```


*GitHub* : [5](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/PoolAddress.sol#L5-L5)

```solidity
📁 File: src/libraries/PositionKey.sol

4: library PositionKey {

```


*GitHub* : [4](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/PositionKey.sol#L4-L4)

```solidity
📁 File: src/libraries/SqrtPriceMathPartial.sol

11: library SqrtPriceMathPartial {

```


*GitHub* : [11](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/SqrtPriceMathPartial.sol#L11-L11)

```solidity
📁 File: src/libraries/TransferHelper.sol

6: library TransferHelper {

```


*GitHub* : [6](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/TransferHelper.sol#L6-L6)

### [G-69]<a name="g-69"></a> WETH address definition can be use directly

WETH is a wrap Ether contract with a specific address in the Ethereum network, giving the option to define it may cause false recognition, it is healthier to define it directly.

    Advantages of defining a specific contract directly:
    
    It saves gas,
    Prevents incorrect argument definition,
    Prevents execution on a different chain and re-signature issues,
    WETH Address : 0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2

*There are 5 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol

25:     address public immutable WETH;

27:     constructor(address _pool, address _baseToken, address _WETH) {

```


*GitHub* : [25](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol#L25-L25), [27](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol#L27-L27)

```solidity
📁 File: src/ILOManager.sol

17:     address public override WETH9;

38:         address weth9,

```


*GitHub* : [17](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L17-L17), [38](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L38-L38)

```solidity
📁 File: src/base/ILOPoolImmutableState.sol

11:     address public override WETH9;

```


*GitHub* : [11](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOPoolImmutableState.sol#L11-L11)

### [G-70]<a name="g-70"></a> Using XOR (^) and AND (&) bitwise equivalents for gas optimizations

Given 4 variables a, b, c and d represented as such:

```

0 0 0 0 0 1 1 0 <- a
0 1 1 0 0 1 1 0 <- b
0 0 0 0 0 0 0 0 <- c
1 1 1 1 1 1 1 1 <- d

```

To have a == b means that every 0 and 1 match on both variables. Meaning that a XOR (operator ^) would evaluate to 0 ((a ^ b) == 0), as it excludes by definition any equalities.Now, if a != b, this means that there’s at least somewhere a 1 and a 0 not matching between a and b, making (a ^ b) != 0.Both formulas are logically equivalent and using the XOR bitwise operator costs actually the same amount of gas.However, it is much cheaper to use the bitwise OR operator (|) than comparing the truthy or falsy values.These are logically equivalent too, as the OR bitwise operator (|) would result in a 1 somewhere if any value is not 0 between the XOR (^) statements, meaning if any XOR (^) statement verifies that its arguments are different.

*There are 28 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/Whitelist.sol

205:         if (from == _pool && to != owner()) {

216:             if (_allowedWhitelistIndex == 0 || _whitelistIndex[to] > _allowedWhitelistIndex) {

233:         if (_whitelistIndex[whitelisted] == 0) {

```


*GitHub* : [205](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L205-L205), [216](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L216-L216), [233](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L233-L233)

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/FullMath.sol

29:         if (prod1 == 0) {

```


*GitHub* : [29](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/FullMath.sol#L29-L29)

```solidity
📁 File: hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol

53:         sqrtPriceX96 = uint160((ratio >> 32) + (ratio % (1 << 32) == 0 ? 0 : 1));

203:         tick = tickLow == tickHi

```


*GitHub* : [53](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L53-L53), [203](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/TickMath.sol#L203-L203)

```solidity
📁 File: src/ILOManager.sol

52:         require(_cachedProject[uniV3Pool].admin == msg.sender, "UA");

111:         if (pool == address(0)) {

116:             if (sqrtPriceX96Existing == 0) {

119:                 require(sqrtPriceX96Existing == sqrtPriceX96, "UV3P");

134:         require(_project.uniV3PoolAddress == address(0), "RE");

190:         require(_cachedProject[uniV3PoolAddress].initialPoolPriceX96 == sqrtPriceX96, "UV3P");

```


*GitHub* : [52](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L52-L52), [111](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L111-L111), [116](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L116-L116), [119](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L119-L119), [134](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L134-L134), [190](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOManager.sol#L190-L190)

```solidity
📁 File: src/ILOPool.sol

143:         if (balanceOf(recipient) == 0) {

155:         if (RAISE_TOKEN == _cachedPoolKey.token0) {

264:         require(msg.sender == MANAGER, "UA");

285:             if (token0Addr == RAISE_TOKEN) {

386:         if (raiseAmount == 0) return (0, 0);

388:         if (_cachedPoolKey.token0 == SALE_TOKEN) {

465:         require(msg.sender == _project.admin, "UA");

```


*GitHub* : [143](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L143-L143), [155](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L155-L155), [264](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L264-L264), [285](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L285-L285), [386](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L386-L386), [388](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L388-L388), [465](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L465-L465)

```solidity
📁 File: src/base/ILOVest.sol

21:             if (i == 0) {

22:                 require (vestingConfigs[i].recipient == address(0), "VR");

32:         require(totalShares == BPS, "TS");

50:         require(totalShares == BPS, "VS");

```


*GitHub* : [21](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L21-L21), [22](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L22-L22), [32](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L32-L32), [50](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/ILOVest.sol#L50-L50)

```solidity
📁 File: src/base/LiquidityManagement.sol

25:         require(msg.sender == _cachedUniV3PoolAddress);

```


*GitHub* : [25](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/LiquidityManagement.sol#L25-L25)

```solidity
📁 File: src/base/PeripheryPayments.sol

14:         require(msg.sender == WETH9, 'Not WETH9');

27:         if (token == WETH9 && address(this).balance >= value) {

31:         } else if (payer == address(this)) {

```


*GitHub* : [14](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/PeripheryPayments.sol#L14-L14), [27](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/PeripheryPayments.sol#L27-L27), [31](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/base/PeripheryPayments.sol#L31-L31)

```solidity
📁 File: src/libraries/LiquidityAmounts.sol

15:         require((y = uint128(x)) == x);

```


*GitHub* : [15](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/libraries/LiquidityAmounts.sol#L15-L15)

### [G-71]<a name="g-71"></a> Don't use `_msgSender()` if not supporting EIP-2771

Use `msg.sender` if the code does not implement [EIP-2771 trusted forwarder](https://eips.ethereum.org/EIPS/eip-2771) support

*There are 5 instance(s) of this issue:*

```solidity
📁 File: hardhat-vultisig/contracts/Vultisig.sol

13:         _mint(_msgSender(), 100_000_000 * 1e18);

```


*GitHub* : [13](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Vultisig.sol#L13-L13)

```solidity
📁 File: hardhat-vultisig/contracts/Whitelist.sol

55:         if (_msgSender() != _vultisig) {

69:         if (_isBlacklisted[_msgSender()]) {

72:         _addWhitelistedAddress(_msgSender());

73:         payable(_msgSender()).transfer(msg.value);

```


*GitHub* : [55](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L55-L55), [69](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L69-L69), [72](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L72-L72), [73](https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/hardhat-vultisig/contracts/Whitelist.sol#L73-L73)

