# QA Report  
2024-06-VULTISIG
## [L-1] Consider implementing two-step transfer process for important roles
`owner` and `admin` have privileged role and functions within certain contracts. For the contracts that have inherited `Ownable.sol` allows the owner to transfer ownership in a one-step process. It is a simlar case for `admin` in their respective contracts.
### Impact
Critical owner priviliges could be transferred to an incorrect address e.g. 
- if owner mistakenly inputs an incorrect address 
- Clipboard Replacement Attack: An attack that involves the protocol owner copying the address that ownership is supposed to be transferred to, but a malware replaces the address on the clipboard with a different, attacker-controlled address.
### Recommended Mitigation Steps
1. For `Ownable.sol`, developers can opt to inherit openzeppelin's new `Ownable2Step.sol` or modify the current `Ownable.sol` to have a similar architecture. 
Reference: https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/access/Ownable2Step.sol 
2. For `admin` role, alike the above, developers can opt to implement a 2 step transfer process within respective contracts. For example in `ILOManager.sol`:
```diff
+   mapping(address => address) private pendingNewAdmins;
+   event ProjectAdminChangeProposed(address, address, address);

-   function transferAdminProject(address admin, address uniV3Pool) external override onlyProjectAdmin(uniV3Pool) {
-       Project storage _project = _cachedProject[uniV3Pool];
-       _project.admin = admin;
-       emit ProjectAdminChanged(uniV3Pool, msg.sender, admin);
-   }

+   function transferAdminProject(
+       address admin, 
+       address uniV3pool
+   ) external override onlyProjectAdmin(uniV3Pool) {
+       pendingNewAdmins(uniV3Pool) = admin;
+       emit ProjectAdminChangeProposed(uniV3Pool, msg.sender, admin);
+   }

+   function confirmTransferAdminProject(
+       address admin, 
+       address uniV3pool
+   ) external onlyProjectAdmin(uniV3Pool) {
+       //NOTE: whether to double check admin is OPTIONAL
+       require(admin == pendingNewAdmins(uniV3Pool) = admin);
+       Project storage _project = _cachedProject[uniV3Pool];
+       _project.admin = admin;
+       emit ProjectAdminChanged(uniV3Pool, msg.sender, admin);
+   }
```
## [L-2] No require statements in owner functions that changes uint256 variables in the Whitelist.sol contract
In `Whitelist.sol`, the two variables `_maxAddressCap` and `_allowedWhitelistIndex` can both be modified through owner functions `setMaxAddressCap` and `setAllowedWhitelistIndex` respectively. However, both do not have require statements to prevent any possible errors. 
### Impact
Both above mentioned variables will affect the purchase of the token. However, if the owner had a typo while changing the above variables, it may affect the functionality of the contract. 
1. If `_maxAddressCap` was decided to be set to 4 ether but accidentally input 4e17, then users will be reverted even with 0.4 worth of purchase.
2. If `_allowedWhitelistIndex` was decided to be set to 1010 but accidentally input 101. than near 900 users who were initially whitelisted may be reverted when purchasing the token.
### Recommended Mitigation Steps
1. If their is a minimum value for both variables, add a require statement to prevent it from going any lower than that value.
```diff
    function setMaxAddressCap(uint256 newCap) external onlyOwner {
+       require(newCap > 3 ether);        
        _maxAddressCap = newCap;
    }
    function setAllowedWhitelistIndex(uint256 newIndex) external onlyOwner {
+       require(newIndex > 1000);
        _allowedWhitelistIndex = newIndex;
    }
```
2. Another option is to let it be strictly increasing.
```diff
    function setMaxAddressCap(uint256 newCap) external onlyOwner {
+       require(newCap > _maxAddressCap);        
        _maxAddressCap = newCap;
    }
    function setAllowedWhitelistIndex(uint256 newIndex) external onlyOwner {
+       require(newIndex > _allowedWhitelistIndex);
        _allowedWhitelistIndex = newIndex;
    }
```