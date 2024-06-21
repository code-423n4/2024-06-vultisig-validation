### Report 1:
#### Invalid Schedule Can be Set due to Improper Validation
The look at how Vest Schedule is validated in the ILOVest.sol contract shows that schedule[i].start is greater than the previous schedule[i].end i.e lastEnd in the array, the problem is that this validation is incomplete as all schedule end in the array can be set to zero without reverting which will unlock liquidity improperly due to invalid validation of schedule at [L417](https://github.com/code-423n4/2024-06-vultisig/blob/main/src/ILOPool.sol#L417) of pool contract.
As adjusted below the validation should be completed by ensuring end is greater than start at each schedule cycle
https://github.com/code-423n4/2024-06-vultisig/blob/main/src/base/ILOVest.sol#L42-L47
```solidity
 function _validateVestSchedule(uint64 launchTime, LinearVest[] memory schedule) internal pure {
        require(schedule[0].start >= launchTime, "VT");
        uint16 BPS = 10000;
        uint16 totalShares;
        uint64 lastEnd;
        uint256 scheduleLength = schedule.length;
        for (uint256 i = 0; i < scheduleLength; i++) {
+++         require ( schedule[i].end > schedule[i].start, "Invalid Schedule");
            // vesting schedule must not overlap
            require(schedule[i].start >= lastEnd, "VT");
            lastEnd = schedule[i].end;
            // we need to subtract fist in order to avoid int overflow
            require(BPS - totalShares >= schedule[i].shares, "VS");
            totalShares += schedule[i].shares;
        }
        // total shares should be exactly equal BPS
        require(totalShares == BPS, "VS");
    }
```
This is considered of low severity as error is only possible by manager during initialization however it should be adjusted and corrected as invalid end schedule would go unnoticed in contract.