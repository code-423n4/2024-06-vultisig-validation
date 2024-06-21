[Q1] `Unused investorShares Field in Project Struct`
The investorShares field in the Project struct is not utilized or assigned any value through out the protocol remove the unused investorShares field from the Project struct to simplify the code
https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/interfaces/IILOManager.sol#L27

[Q2] `Missing Blacklist Check in _addWhitelistedAddress`
The `_addWhitelistedAddress` function does not verify if an address is blacklisted before incrementing the whitelist count, potentially allowing blacklisted addresses to be whitelisted. This will ultimately give a whitelist count to a black listed addresses when `function addBatchWhitelist` is called
https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/contracts/Whitelist.sol#L232

[Q3] `Validation check`
add validation check to ensure that hardCap > softCap, 