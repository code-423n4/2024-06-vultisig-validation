## Title
Unused modifier `onlyProjectAdmin()` in `ILOPool.sol`, can lead to access control vulnerability

## Impact
The `onlyProjectAdmin()` modifier is declared in `ILOPool.sol` but is not implemented. Initially it might look harmless but the purpose of the `onlyProjectAdmin()` modifier is to 
restrict access to certain functions to only the project admin. If it's meant to be used in some function described in `ILOPool.sol` which is to be controlled just by the admin,
then it can lead to severe malfunctioning of the contract/ protocol.

## Proof of Concept

Modifier `onlyProjectAdmin()`
```
    modifier onlyProjectAdmin() override { 
        IILOManager.Project memory _project = IILOManager(MANAGER).project(_cachedUniV3PoolAddress);
        require(msg.sender == _project.admin, "UA");
        _;
    }
```
https://github.com/code-423n4/2024-06-vultisig/blob/7fb0da757c98116090f35810146ea742ca3b94da/src/ILOPool.sol#L463-L467

The above mentioned modifier is declared in the `ILOPool.sol` contract, is declared but not implemented.
When we search for the modifier in the `ILOPool.sol` we only get the modifier declaration.

## Tools Used
Manual review

## Recommended Mitigation Steps
Implement the `onlyProjectAdmin()` modifier in the functions where it's intended to be used or if it's not meant to be used, the declaration should be removed to save contract size.