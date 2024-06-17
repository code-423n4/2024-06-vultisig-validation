There is a temporary Denial of Service Issue here: https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/contracts/Whitelist.sol#L221-L224 on the `checkWhitelist` function as 
```
 if (_contributed[to] + estimatedETHAmount > _maxAddressCap) {
     revert MaxAddressCapOverflow();
  }
```
In checking the contract would revert if `contributed[to] + estimatedETHAmount` surpases `maxAddressCap`. This means that when the `maxAddressCap` is almost reached, the user needs to pass the exact balance amount to ensure their transaction does not revert. It would good for UI if the function simply deducts the balance instead of reverting as follows:
```
  if (_contributed[to] + estimatedETHAmount > _maxAddressCap && _contributed[to] != _maxAddressCap) {
      _contributed[to] += _maxAddressCap - _contributed[to];
            }