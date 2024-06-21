## NC-01: Events are missing in functions that make state changes

Events in smart contracts serve as logs to record significant actions/changes in state, providing an immutable audit trail on the blockchain. Missing events can hinder monitoring contract activities, debugging issues, and ensuring accountability.

- Found in hardhat-vultisig/contracts/Vultsig.sol [Line: 16](hardhat-vultisig/contracts/Vultsig.sol#L16)

```javascript
function approveAndCall(address spender, uint256 amount, bytes calldata extraData) external returns (bool) {
    // Approve the spender to spend the tokens
    _approve(msg.sender, spender, amount);
+   emit ApproveAndCall(spender, amount, extraData);
   // Call the receiveApproval function on the spender contract
   IApproveAndCallReceiver(spender).receiveApproval(msg.sender, amount, address(this), extraData);

   return true;
}
```

- Found in hardhat-vultisig/contracts/Whitelist.sol [Line: 136](hardhat-vultisig/contracts/Whitelist.sol#L136)

```javascript

function setLocked(bool newLocked) external onlyOwner {
   _locked = newLocked;
+  emit SetLocked(newLocked);
}

```

- Found in hardhat-vultisig/contracts/Whitelist.sol [Line: 142](hardhat-vultisig/contracts/Whitelist.sol#L142)

```javascript

function setMaxAddressCap(uint256 newCap) external onlyOwner {
   _maxAddressCap = newCap;
+  emit SetMaxAddressCap(newCap);
}

```

- Found in hardhat-vultisig/contracts/Whitelist.sol [Line: 148](hardhat-vultisig/contracts/Whitelist.sol#L148)

```javascript

function setVultisig(address newVultisig) external onlyOwner {
   _vultisig = newVultisig;
+  emit SetVultisig(newVultisig);
}

```

- Found in hardhat-vultisig/contracts/Whitelist.sol [Line: 154](hardhat-vultisig/contracts/Whitelist.sol#L154)

```javascript

function setIsSelfWhitelistDisabled(bool newFlag) external onlyOwner {
   _isSelfWhitelistDisabled = newFlag;
+  emit SetIsSelfWhitelistDisabled(newFlag);
}

```

- Found in hardhat-vultisig/contracts/Whitelist.sol [Line: 160](hardhat-vultisig/contracts/Whitelist.sol#L160)

```javascript
function setOracle(address newOracle) external onlyOwner {
   _oracle = newOracle;
+  emit SetOracle(newOracle);
}

```

- Found in hardhat-vultisig/contracts/Whitelist.sol [Line: 166](hardhat-vultisig/contracts/Whitelist.sol#L166)

```javascript

function setPool(address newPool) external onlyOwner {
   _pool = newPool;
+  emit SetPool(newPool);
}

```

- Found in hardhat-vultisig/contracts/Whitelist.sol [Line: 173](hardhat-vultisig/contracts/Whitelist.sol#L173)

```javascript

function setBlacklisted(address blacklisted, bool flag) external onlyOwner {
   _isBlacklisted[blacklisted] = flag;
+  emit SetBlacklisted(blacklisted, flag);
}

```

- Found in hardhat-vultisig/contracts/Whitelist.sol [Line: 179](hardhat-vultisig/contracts/Whitelist.sol#L179)

```javascript

function setAllowedWhitelistIndex(uint256 newIndex) external onlyOwner {
   _allowedWhitelistIndex = newIndex;
+  emit SetAllowedWhitelistIndex(newIndex);
}
```

- Found in hardhat-vultisig/contracts/Whitelist.sol [Line: 232](hardhat-vultisig/contracts/Whitelist.sol#L232)

```javascript
function _addWhitelistedAddress(address whitelisted) private {
   if (_whitelistIndex[whitelisted] == 0) {
       _whitelistIndex[whitelisted] = ++_whitelistCount;
+      emit AddWhitelistedAddress(whitelisted, _whitelistCount);
    }
}
```

- Found in hardhat-vultisig/contracts/extensions/VultsigWhitelist.sol [Line: 22](hardhat-vultisig/contracts/extensions/VultsigWhitelist.sol#L22)

```javascript

function setWhitelistContract(address newWhitelistContract) external onlyOwner {
   _whitelistContract = newWhitelistContract;
+  emit SetWhitelistContract(newWhitelistContract);
}

```

## L-01: Checks are missing in functions that make state changes

State changes are critical operations that alter the contract’s data or behavior. Missing checks can lead to vulnerabilities, unauthorized state modifications, and unexpected behaviors.

- Found in src/ILOManager.sol [Line: 169](src/ILOManager.sol#L169)

```javascript

function transferAdminProject(address admin, address uniV3Pool) external override onlyProjectAdmin(uniV3Pool) {
+  require(admin != address(0) && uniV3Pool != address(0), "Null address");
   Project storage _project = _cachedProject[uniV3Pool];
   _project.admin = admin;
   emit ProjectAdminChanged(uniV3Pool, msg.sender, admin);
}

```

- Found in src/ILOPool.sol [Line: 350](src/ILOPool.sol#L350)

```javascript

function claimRefund(uint256 tokenId) external override refundable() isAuthorizedForToken(tokenId) {
   uint256 refundAmount = _positions[tokenId].raiseAmount;
+  if (refundAmount != 0) {
       address tokenOwner = ownerOf(tokenId);

       delete _positions[tokenId];
       delete _positionVests[tokenId];
       _burn(tokenId);

       TransferHelper.safeTransfer(RAISE_TOKEN, tokenOwner, refundAmount);
       emit UserRefund(tokenOwner, tokenId,refundAmount+);
+   }
}
```

- Found in hardhat-vultisig/contracts/extensions/VultsigWhitelist.sol [Line: 22](hardhat-vultisig/contracts/extensions/VultsigWhitelist.sol#L22)

```javascript

function setWhitelistContract(address newWhitelistContract) external onlyOwner {
+  require(newWhitelistContract != address(0), "Null address");
   _whitelistContract = newWhitelistContract;
}

```
- Found in hardhat-vultisig/contracts/Whitelist.sol [Line: 148](hardhat-vultisig/contracts/Whitelist.sol#L148)

```javascript

function setVultisig(address newVultisig) external onlyOwner {
+  require(newVultisig != address(0), "Null address");
   _vultisig = newVultisig;
}

```

## L-02: Floating pragma version

Floating pragma versions allow the contract to compile with multiple versions of the Solidity compiler. While this can provide flexibility, it may also introduce risks due to compatibility issues and unanticipated behavior with newer compiler versions.

- Found in src/libraries/ChainId.sol [Line: 2](src/libraries/ChainId.sol#2)

```javascript
-   pragma solidity >=0.7.0;
+   pragma solidity 0.8.24;
```

- Found in src/libraries/PositionKey.sol [Line: 2](src/libraries/PositionKey.sol#2)

```javascript
-   pragma solidity >=0.5.0;
+   pragma solidity 0.8.24;
```
- Found in hardhat-vultisig/contracts/Whitelist.sol [Line: 2](hardhat-vultisig/contracts/Whitelist.sol#L2)

```javascript
-  pragma solidity ^0.8.24;
+  pragma solidity 0.8.24;
```