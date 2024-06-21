## NO function to remove `Blacklisted` user from the BlackList.

As there is function to `Blacklist` the user
```
/// @notice Setter for blacklist
    /// @param blacklisted Address to be added
    /// @param flag New flag for address
    function setBlacklisted(address blacklisted, bool flag) external onlyOwner {
        _isBlacklisted[blacklisted] = flag;
    }
```
 but what happens if there is a miss-understanding or any mishap which by-mistake add the good user to the blacklist , There should be a function which only owner can call which can help to whitelist the user if he is not proven guilty . 
This issue can also loss of value in the context of users as it leads to negative impact on the users if this happens, which can indirectly leads to loss of users for protocol which is not good.

There should be a function `removeBlacklistFlag()` in the `Whitelist.sol` contract
