## [I-1]
In `ILOVest.sol::_validateSharesAndVests()` inside for loop we are checking for index `i == 0` for each iteration, we can simply handle the `i == 0` condition outside the loop.

## Recommended Mitigation Steps
```diff
.
.
+  require(vestingConfigs[0].recipient == address(0), "VR");
+  require(BPS - totalShares >= vestingConfigs[i].shares, "TS");
+  _validateVestSchedule(launchTime, vestingConfigs[i].schedule);
+  totalShares += vestingConfigs[i].shares;

-    for (uint256 i = 0; i < vestingConfigs.length; i++) {
+    for (uint256 i = i; i < vestingConfigs.length; i++) {
-            if (i == 0) {
-                require(vestingConfigs[i].recipient == address(0), "VR");
-            } else {
                require(vestingConfigs[i].recipient != address(0), "VR");
-            }
            // we need to subtract fist in order to avoid int overflow
            require(BPS - totalShares >= vestingConfigs[i].shares, "TS");
            _validateVestSchedule(launchTime, vestingConfigs[i].schedule);
            totalShares += vestingConfigs[i].shares;
        }
.
.
```