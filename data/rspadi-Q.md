# Vultisig Low Risk and Non-Critical Issues

# Table of Contents
- [Low Risk Findings](#lowrisk)
    - [[L-01] Whitelist::setAllowedWhitelistIndex : Already whitelisted users may not be able to receive SALE tokens](#l01)
    - [[L-02] Whitelist::_addWhitelistedAddress : Whitelisted user may not be able to receive SALE tokens](#l02)
    - [[L-03] Whitelist::_addWhitelistedAddress : Check if user has been blacklisted](#l03)
   
  
<a id="lowrisk"></a>    
## Low Risk Findings

<a id="l01"></a>
### [L-01] Whitelist::setAllowedWhitelistIndex : Already whitelisted users may not be able to receive SALE tokens

Source: https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/contracts/Whitelist.sol#L180

Let's assume, 100 addresses have been whitelisted for the ILO. Then, the Owner calls setAllowedWhitelistIndex() and specifies 80 for the newIndex parameters. Now, whenever a legitimately whitelisted user should receive SALE tokens, the _beforeTokenTransfer hook in the VultisigWhitelisted contract will be called and the checkWhitelist function in the Whitelist contract will be executed. 

This function executes the following code:

```
if (_allowedWhitelistIndex == 0 || _whitelistIndex[to] > _allowedWhitelistIndex) {
    revert NotWhitelisted();
} 
```

Now, because _allowedWhitelistIndex was changed from 100 to 80, the token transfer will fail for the last 20 users in the whitelist.
 
 
If specific users should be blacklisted, use the setBlacklisted() function and add the following code to the setAllowedWhitelistIndex function:

```
require(newIndex <= _whitelistCount);
```


<a id="l02"></a>
### [L-02] Whitelist::_addWhitelistedAddress : Check the _whitelistCount before whitelisting the user

Source: https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/contracts/Whitelist.sol#L234

The functions allows to add a user to the whitelist. However, if the current _whitelistCount is larger than _allowedWhitelistIndex, the checkWhitelist() function will fail if that user receives SALE tokens.

The _addWhitelistedAddress function should check the value of _allowedWhitelistIndex and revert if the current _whitelistCount  is larger than _allowedWhitelistIndex.

That way, the Owner can react accordingliy and increase the _allowedWhitelistIndex, by calling setAllowedWhitelistIndex() if necessary.   

Add the following code to the _addWhitelistedAddress function:

```
uint256 newWhitelistCount = _whitelistCount + 1;
require(newWhitelistCount <=  _allowedWhitelistIndex, "Whitelist count needs to be increased");
       
```


<a id="l03"></a>
### [L-03] Whitelist::_addWhitelistedAddress : Check if user has been blacklisted

Source: https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/contracts/Whitelist.sol#L232

Let's assume the following scenarion:

Alice is blacklisted by accident
Various users are whitelisted
The Owner adds Alice to the whitelist

Now, Alice is whitelisted and blacklisted, which means, she is actually still blacklisted.

When calling _addWhitelistedAddress, the function should verify if that user is already blacklisted and revert if that is the case. That way, the Owner can act accordingly and either decide to keep that user blacklisted or to call setBlacklisted(user, false) and then call addWhitelistedAddress(user) to effectivly whitelist that user.
   

Add the following code to the _addWhitelistedAddress function:

```
require(!_isBlacklisted[whitelisted], "The user has already been blacklisted"); 
       
```
