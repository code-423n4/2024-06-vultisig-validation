# QA Report

## Summary

| Label                                                                         | Issue Description                                                   |
| ----------------------------------------------------------------------------- | ------------------------------------------------------------------- |
| [L-01](#l-01-functions-in-ilomanagersol-are-lacking-important-checks)         | Functions in `ILOManager.sol` are lacking important checks          |
| [L-02](#l-02-wrong-natspec-comments-in-ilomanagersol)                         | Wrong natspec comments in `ILOManager.sol`                          |
| [L-03](#l-03-use-two-step-transfer-process-in-ilomanagertransferadminproject) | Use two-step transfer process in `ILOManager::transferAdminProject` |

## [L-01] Functions in `ILOManager.sol` are lacking important checks

Some functions in `ILOManager.sol` lack important checks

https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/ILOManager.sol#L57-L65

https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/ILOManager.sol#L90

```js
file: src/ILOManager.sol

    function initProject(InitProjectParams calldata params) external override afterInitialize() return (address uniV3PoolAddress) {
        // @audit missing check for `params.launchTime` > block.timestamp
        uint64 refundDeadline = params.launchTime + DEFAULT_DEADLINE_OFFSET;

        // @audit missing check for `params.fee` is enabled in UniswapV3Factory
        PoolAddress.PoolKey memory poolKey = PoolAddress.getPoolKey(params.saleToken, params.raiseToken, params.fee);

        ...
    }

    function initILOPool(InitPoolParams calldata params) external override onlyProjectAdmin(params.uniV3Pool) returns (address iloPoolAddress) {
        ...

        // @audit missing check for `sqrtRatioUpperX96` > `_project.initialPoolPriceX96`
        require(sqrtRatioLowerX96 < _project.initialPoolPriceX96 && sqrtRatioLowerX96 < sqrtRatioUpperX96, "RANGE");
        ...
    }
```

## [L-02] Wrong natspec comments in `ILOManager.sol`

https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/ILOManager.sol#L154

https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/ILOManager.sol#L159

```js
file: src/ILOManager.sol

    /// @audit sets `Performance` fee
    /// @notice set platform fee for decrease liquidity. Platform fee is imutable among all project's pools
    function setPerformanceFee(uint16 _performanceFee) external onlyOwner() {
        PERFORMANCE_FEE = _performanceFee;
    }

    /// @audit sets `FEE_TAKER` address
    /// @notice set platform fee for decrease liquidity. Platform fee is imutable among all project's pools
    function setFeeTaker(address _feeTaker) external override onlyOwner() {
        FEE_TAKER = _feeTaker;
    }
```

## [L-03] Use two-step transfer process in `ILOManager::transferAdminProject`
https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/ILOManager.sol#L169-L173

A project admin is responsible for executing functions crutial to the project like `ILOManager::initILOPool` and `ILOManager::claimRefund`.
Using a two-step transfer process will help prevent a project admin from accidentally transferring admin rights to an unintended address.
