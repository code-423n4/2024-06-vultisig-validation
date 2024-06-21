# [L-1] `Vultisig::approveAndCall` doesn't return `false` if call fails

[Vultisig.sol#L16-L24](https://github.com/code-423n4/2024-06-vultisig/blob/main/hardhat-vultisig/contracts/Vultisig.sol#L16-L24)
```javascript
    function approveAndCall(address spender, uint256 amount, bytes calldata extraData) external returns (bool) {
        // Approve the spender to spend the tokens
        _approve(msg.sender, spender, amount);

        // Call the receiveApproval function on the spender contract
        IApproveAndCallReceiver(spender).receiveApproval(msg.sender, amount, address(this), extraData);

        return true;
    }
```

This function is designed to be an alternative to `ERC20::approve` for the `Vultisig token`. It returns a bool, but only `true` if it succeeds. If the function fails, it reverts rather than returning `false`.

If a contract is calling this function and handling the case in which this function returns `false`, that branch will never execute, and instead will revert. This can be problematic for smart contracts that implement this case, as it can cause DoS.