## [L-01] `claimRefund()` doesn't update `totalRaised` 

## Details

Investors of ILOPool can claim their refund if the pool hasn't been launched and the refundDeadline is passed, but it was noticed that the claimed raised amount is not deducted from the `totalRaised`, which would result in extracting wrong result from the `totalSold()` function:

```js
    function claimRefund(
        uint256 tokenId
    ) external override refundable isAuthorizedForToken(tokenId) {
        uint256 refundAmount = _positions[tokenId].raiseAmount;
        address tokenOwner = ownerOf(tokenId);

        delete _positions[tokenId];
        delete _positionVests[tokenId];
        _burn(tokenId);

        TransferHelper.safeTransfer(RAISE_TOKEN, tokenOwner, refundAmount);
        emit UserRefund(tokenOwner, tokenId, refundAmount);
    }
```

## Recommendation

Update `ILOPool.claimRefund()` to deduct the refunded amount from the `totalRaised` variable:

```diff
    function claimRefund(
        uint256 tokenId
    ) external override refundable isAuthorizedForToken(tokenId) {
        uint256 refundAmount = _positions[tokenId].raiseAmount;
        address tokenOwner = ownerOf(tokenId);

        delete _positions[tokenId];
        delete _positionVests[tokenId];
        _burn(tokenId);
+        totalRaised - = refundAmount;
        TransferHelper.safeTransfer(RAISE_TOKEN, tokenOwner, refundAmount);
        emit UserRefund(tokenOwner, tokenId, refundAmount);
    }
```

## [L-02] `Whitelist.whitelistCount()` doesn't return the correct count of whitelisted addresses

## Details

`Whitelist.whitelistCount()` function is supposed to return the current number of the whitelisted addresses, and this is done by returning the `_whitelistCount` that is supposed to track that number:

```js
   function whitelistCount() external view returns (uint256) {
       return _whitelistCount;
   }
```

but this is not correct as this `_whitelistCount` is not updated when a whitelisted address is removed via `setBlacklisted`, which would result in returning an incorrect number of the current whitelisted addresses.

## Recommendation

Add another variable to track the blacklisted accounts count in `Whitelist.setBlacklisted()` (`_blacklistCount`), and upadte `Whitelist.whitelistCount()` function to return `_whitelistCount - _blacklistCount` as the current count of whitelisted accounts.
