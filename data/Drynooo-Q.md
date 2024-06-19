1. Make a preemptive transaction before [the whitelist address is set](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/contracts/extensions/VultisigWhitelisted.sol#L22-L24), and you can buy VULT at will.

2. There is no check that hardCap must be greater than softCap, and softCap may never be reached, resulting in failure to launch.

3. The claim function can transfer ETH to the contract, and this part of ETH will be locked in the contract.