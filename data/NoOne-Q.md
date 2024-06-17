https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/contracts/Whitelist.sol#L232

in natspec says `Internal function used for whitelisting. Only increase whitelist count if address is not whitelisted before` but the function is `Private`. If the function is planned to be used in other contract it should to be `Internal` or it have to change the natspec
