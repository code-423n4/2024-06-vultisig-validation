 uint16 BPS = 10000 declared several times in the following paths:

line 13: src/base/ILOVest.sol
line 19, 37: src/base/ILOPoolImmutableState.sol

Wasteful of gas, more optimal to declare once in a file of constants and import from there.

Suggestion example:
// constants.sol

pragma solidity ^0.7.6;

library Constants {
    uint16 constant BPS = 10000;
}

importing example:

import './constants.sol';

abstract contract ILOVest {
    using Constants for uint16;

    function _validateSharesAndVests(uint64 launchTime, VestingConfig[] memory vestingConfigs) internal pure {
        uint16 totalShares;
        for (uint256 i = 0; i < vestingConfigs.length; i++) {
            // ...
            require(Constants.BPS - totalShares >= vestingConfigs[i].shares, "TS");
            // ...
        }
        // ...
    }






