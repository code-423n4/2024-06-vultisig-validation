https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/ILOManager.sol#L149-L162

This function allows the owner to set the performance fee.
It uses the onlyOwner modifier to restrict access to the contract owner.
Consider implementing limits or checks on the _performanceFee value to prevent setting unreasonable fees.