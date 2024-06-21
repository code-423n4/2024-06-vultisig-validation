## 1. Insecure Use of `delegatecall` in Multicall Contract
[Multicall.sol#L11-L27](https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/base/Multicall.sol#L11-L27)
The `Multicall` contract allows for multiple function calls to be executed within a single transaction by using the `delegatecall` opcode. Here is the relevant part of the code:
```solidity
function multicall(bytes[] calldata data) public payable override returns (bytes[] memory results) {
    results = new bytes[](data.length);
    for (uint256 i = 0; i < data.length; i++) {
        (bool success, bytes memory result) = address(this).delegatecall(data[i]);

        if (!success) {
            if (result.length < 68) revert();
            assembly {
                result := add(result, 0x04)
            }
            revert(abi.decode(result, (string)));
        }

        results[i] = result;
    }
}
```
The `delegatecall` function executes the provided function call in the context of the calling contract. This means that the called function has access to and can modify the state of the `Multicall` contract, potentially leading to unintended side effects or malicious manipulation of the contract’s storage.
### Impact
Using delegatecall can expose the Multicall contract to severe risks, including reentrancy attacks and unauthorized state modifications. For instance, an attacker could exploit this by crafting a malicious call that re-enters the multicall function and manipulates the contract's state, potentially leading to loss of funds or corruption of contract logic.
### Mitigation
Replace `delegatecall` with `call`. The `call` function executes the provided function call in the context of the called contract, not the calling contract, thereby isolating the state and reducing the risk of unintended state changes.