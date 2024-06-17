
# L1. renounceOwnership can lock this contract forever in Whitelist.sol
When the `renounceOwnership` function is called by the owner in the Whitelist contract and the `locked` variable is set to true, it permanently locks the contract, making it impossible for anyone to unlock it.
To address this issue, it is necessary to modify the renounceOwnership function in the Whitelist contract to include a check for the locked variable before allowing the owner to proceed with the renouncement.
https://github.com/code-423n4/2024-06-vultisig/blob/main/hardhat-vultisig/contracts/Whitelist.sol#L208
https://github.com/code-423n4/2024-06-vultisig/blob/main/hardhat-vultisig/contracts/extensions/VultisigWhitelist.sol#L29


# L2. Use the same validation for the refundDeadline in ILOManager and ILOPool
[claimRefund](https://github.com/code-423n4/2024-06-vultisig/blob/main/src/ILOManager.sol#L202)
> require(_cachedProject[uniV3PoolAddress].refundDeadline < block.timestamp, "RFT");

[refundable](https://github.com/code-423n4/2024-06-vultisig/blob/main/src/ILOPool.sol#L342)
> require(block.timestamp >= _project.refundDeadline, "RFT");

# L3. Vulnerability in ILOManager contract initialization
The `initialize` function in the ILOManager contract lacks the onlyOwner modifier, making it susceptible to front-running attacks. If the initialize function is not called in the same block as the contract deployment, an attacker can exploit this vulnerability by front-running the initialization process.
[initialize](https://github.com/code-423n4/2024-06-vultisig/blob/main/src/ILOManager.sol#L41)

# L4. Not enough validation in _validateVestSchedule in ILOVest.sol
https://github.com/code-423n4/2024-06-vultisig/blob/main/src/base/ILOVest.sol#L43

While the start time of the schedule is validated to ensure it is greater than the `lastEnd`, there is no validation for the end time being greater than the start time.
This allows the project owner to set the end time to be less than the start time, resulting in incorrect calculations for `unlockedLiquidity`.
In cases where `vest.start` is equal to `vest.end`, the `unlockedLiquidity` may be reverted if the `block.timestamp` is equal to `vest.start`.
To address this issue, it is recommended to add validation for the end time in the `_validateVestSchedule` function.

# L5. Missing validation if the new project admin is address(0) in transferAdminProject function in ILOManager.sol
https://github.com/code-423n4/2024-06-vultisig/blob/main/src/ILOManager.sol#L171
When the project admin is set to address(0), both the `launch` and `claimRefund` functions will be disabled and cannot be called.

# L6. PLATFORM_FEE + PERFORMANCE_FEE should be less than BPS(10000)
In the [ILOManager.sol](https://github.com/code-423n4/2024-06-vultisig/blob/main/src/ILOManager.sol#L137) contract, there is a missing validation for the sum of the PLATFORM_FEE and PERFORMANCE_FEE.
If the sum exceeds BPS(10000), an overflow will occur in the [_deductFees](https://github.com/code-423n4/2024-06-vultisig/blob/main/src/ILOPool.sol#L208) function.
This can result in incorrect calculations for the claimable amount of users.

