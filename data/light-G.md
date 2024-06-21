# Use a merkle tree for whitelisting

Whilst the operations of an enumerable set are gas-efficient even with a large amount of addresses, storing these addresses on Ethereum mainnet is relatively costly.

Adding new addresses to the set costs 20,000 gas (`SSTORE`) for each address. For example, creating a whitelist of 100 addresses would require more than two million gas. However, when using a merkle tree, you only need to call `SSTORE` once to store the root, which can be computed off-chain.

Additionally, merkle trees make it easier and more gas-efficient to store multiple user tiers of the `maxCapPerUser` mentioned in `IILOPool.sol:90`.

### Possible implementation using OpenZeppelin's `MerkleProof` library

```solidity
bytes32 public wlRoot; // make this empty to disable the whitelist

if (wlRoot != bytes32(0) && !MerkleProof.verifyCalldata(proof, wlRoot, keccak256((abi.encode(msg.sender))))) {
    revert NotWhitelisted();
}
```
