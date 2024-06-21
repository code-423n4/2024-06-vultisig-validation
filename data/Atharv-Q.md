
## 1. Missing Validation for Vesting Schedule End Time in _validateVestSchedule() Function

## Impact
The lack of validation in the `_validateVestSchedule()` function can lead to system malfunctions. Currently, there is no check to ensure that the end time of any particular vesting schedule is greater than its start time. This can create discrepancies within the system.

## Code
[Link](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/base/ILOVest.sol#L43)

## Tools Used
Manual Review

## Recommended Mitigation Steps
```diff
function _validateVestSchedule(uint64 launchTime, LinearVest[] memory schedule) internal pure {
        require(schedule[0].start >= launchTime, "VT");  
        uint16 BPS = 10000;
        uint16 totalShares;
        uint64 lastEnd;
        uint256 scheduleLength = schedule.length;
        for (uint256 i = 0; i < scheduleLength; i++) {
            // vesting schedule must not overlap
            require(schedule[i].start >= lastEnd, "VT");
+           require(schedule[i].start < schedule[i].end, "VE");  
            lastEnd = schedule[i].end;  //@audit - not checking end is greater than start for 1st one 
            require(BPS - totalShares >= schedule[i].shares, "VS");
            totalShares += schedule[i].shares; 
        }
        // total shares should be exactly equal BPS
        require(totalShares == BPS, "VS");
    }
```


## 2. Unnecessary payable Modifier in claim() Function of ILOPool.sol

## Impact
In the ILOPool.sol file, the claim() function is intended to claim liquidity from the pool without transferring native tokens. However, the claim() function is currently marked as payable, which is unnecessary and could lead to confusion or potential misuse.

## Code
[Link](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/ILOPool.sol#L184-L189)

## Recommended Mitigation Steps

```diff
- function claim(uint256 tokenId)external payable override isAuthorizedForToken(tokenId) returns (uint256 amount0, uint256 amount1){
+ function claim(uint256 tokenId)external override isAuthorizedForToken(tokenId) returns (uint256 amount0, uint256 amount1){
```

## 3. Inconsistent Refund Deadline Check Between `ILPPool.sol` and `ILOManager.sol`.

## Impact
In the `ILPPool.sol` file, the refundable modifier checks if the current timestamp is `greater than or equal` to the project's refund deadline using `require(block.timestamp >= _project.refundDeadline, "RFT");`. However, in the ILOManager.sol file, the `claimRefund()` function checks if the current timestamp is `strictly greater than` the refund deadline using `require(_cachedProject[uniV3PoolAddress].refundDeadline < block.timestamp, "RFT");`. This discrepancy can lead to inconsistent behavior.

## Code

[refundable modifier](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/ILOPool.sol#L342)
[claimRefund](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/ILOManager.sol#L202)


## Recommended Mitigation Steps

```diff
function claimRefund(address uniV3PoolAddress) external override onlyProjectAdmin(uniV3PoolAddress) returns(uint256 totalRefundAmount) {
-       require(_cachedProject[uniV3PoolAddress].refundDeadline < block.timestamp, "RFT");
+       require(_cachedProject[uniV3PoolAddress].refundDeadline <= block.timestamp, "RFT"); 
        address[] memory initializedPools = _initializedILOPools[uniV3PoolAddress];
        for (uint256 i = 0; i < initializedPools.length; i++) {
            totalRefundAmount += IILOPool(initializedPools[i]).claimProjectRefund(_cachedProject[uniV3PoolAddress].admin);
        }
    } 
``` 

## 4. Improve Security in approveAndCall() by Using safeIncreaseAllowance and safeDecreaseAllowance

In the Vultisig.sol file, the approveAndCall() function currently calls _approve to set the allowance. However, it is best practice to use safeIncreaseAllowance and safeDecreaseAllowance to prevent potential frontrunning attacks. This change enhances security by mitigating the risk of unexpected allowance manipulations.

## Code

[_approve function](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/contracts/Vultisig.sol#L18)

## Recommended Mitigation Steps

```diff
function approveAndCall(address spender, uint256 amount, bytes calldata extraData) external returns (bool) {
        // Approve the spender to spend the tokens
-       _approve(msg.sender, spender, amount);
+       safeIncreaseAllowance(address(this),spender,amount); 

        // Call the receiveApproval function on the spender contract
        IApproveAndCallReceiver(spender).receiveApproval(msg.sender, amount, address(this), extraData);

        return true;
    }
```

