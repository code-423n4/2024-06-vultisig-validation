# [L-01] wrong logical operator leading to inconsistencies during claim Refunds in `ILOManager::claimRefund()`
in order of project Admin to refund he calls `ILOManager::claimRefund()` -> `IloPool::claimProjectRefund()` -> the modifier is checked `refundable()` then we call  `_refundProject()`

in [this snippet](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/ILOManager.sol#L201-L206)

```solidity
File: ILOManager.sol
201:     function claimRefund(address uniV3PoolAddress) external override onlyProjectAdmin(uniV3PoolAddress) returns(uint256 totalRefundAmount) {
202:         require(_cachedProject[uniV3PoolAddress].refundDeadline < block.timestamp, "RFT");
203:         address[] memory initializedPools = _initializedILOPools[uniV3PoolAddress];
204:         for (uint256 i = 0; i < initializedPools.length; i++) {
205:             totalRefundAmount += IILOPool(initializedPools[i]).claimProjectRefund(_cachedProject[uniV3PoolAddress].admin);
206:         }

```
we see that in line #202 a check is made to make sure that we are not refunding before the actual deadline
but if we look at **`IloPool`** contract at `refundable()` we see 
[this snippet](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/ILOPool.sol#L337-L347)

```solidity
File: ILOPool.sol
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

``` 
in Line #342 a check is made to check if `block.timestamp >= _project.refundDeadline` .
now this would make normal users who is calling [**`ILOPool::claimRefund()`**](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/ILOPool.sol#L350)

```solidity
function claimRefund(uint256 tokenId) external override refundable() isAuthorizedForToken(tokenId)
```
to be able to initiate refund before project Owners
**in addition to that**
- project Admin may get unnecessary reverts and confused 

# [L-02] Inconsistent Code comments in `ILOManager::setPerformanceFee()` and `ILOManager::setFeeTaker()`

in [**`ILOManager::setPerformanceFee()`**](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/ILOManager.sol#L155-L157)

```solidity
File: ILOManager.sol
154:     /// @notice set platform fee for decrease liquidity. Platform fee is imutable among all project's pools
155:     function setPerformanceFee(uint16 _performanceFee) external onlyOwner() {
156:         PERFORMANCE_FEE = _performanceFee;
157:     }
```
we see that in line #154 the comments says *set platform fee for decrease liquidity. Platform fee is imutable among all project's pools* 
which is wrong as this **function** is setting `PERFORMANCE_FEE` which is a fee taken from uniSwapV3 Pool fees not from the actual liquidity

In Addition to the above problem we see another inconsistency in [**`ILOManager::setFeeTaker()`**](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/ILOManager.sol#L159-L162)

```solidity
File: ILOManager.sol
159:     /// @notice set platform fee for decrease liquidity. Platform fee is imutable among all project's pools
160:     function setFeeTaker(address _feeTaker) external override onlyOwner() {
161:         FEE_TAKER = _feeTaker;
162:     }

```
As we See in the above Comments in Line #159 it says `set platform fee for decrease liquidity. Platform fee is imutable among all project's pools`
which is completely wrong as this function sets `FEE_TAKER` which is an address of the **Owner** of `ILOManager.sol`