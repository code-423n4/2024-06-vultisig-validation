
### [LOW-0] TransferOwnership tx.origin argument could cause ownership problems

**Description:** 
(src/ILOManager.sol#L19) Since tx.origin returns the original external account that initiated the transaction, if the contract is deployed from another contract than the ownership of ILOManager would be to the address of the orignal external account (EOA) that initiated the transaction instead of the deployer contract.

```solidity
    constructor () {
        transferOwnership(tx.origin);
    }
```

**Recommended Mitigation:**

Use an address passed as argument instead:

```solidity
-    constructor () {
+    constructor (address owner) {
+        transferOwnership(owner);
-        transferOwnership(tx.origin);
    }
```

**--------------------------------**

### [LOW-1] Define and use `constant` variables instead of using literals

**Description:** 

If the same constant literal value is used multiple times, create a constant state variable and reference it throughout the contract.

- Found in src/base/ILOVest.sol (src/base/ILOVest.sol#L19)

	```solidity
	        uint16 BPS = 10000;
	```

- Found in src/base/ILOVest.sol (src/base/ILOVest.sol#L37)

	```solidity
	        uint16 BPS = 10000;
	```

**Recommended Mitigation:**

Create the constant then reused it in the functions instead of creating a new variable every single time inside each function

    ```solidity
        uint16 constant BPS = 10000;
    ```

In addition, some gas is saved this way.

**--------------------------------**

### [LOW-2] `public` functions not used internally could be marked `external`

**Description:** 

Instead of marking a function as `public`, consider marking it as `external` if it is not used internally.

- Found in src/ILOPool.sol (src/ILOPool.sol#L53)

	```solidity
	    function name() public pure override(ERC721, IERC721Metadata) returns (string memory) {
	```

- Found in src/ILOPool.sol (src/ILOPool.sol#L57)

	```solidity
	    function symbol() public pure override(ERC721, IERC721Metadata) returns (string memory) {
	```

- Found in src/base/Multicall.sol (src/base/Multicall.sol#L11)

	```solidity
	    function multicall(bytes[] calldata data) public payable override returns (bytes[] memory results) {
	```

**Recommended Mitigation:**
Change all of the above mentioned functions to be `public`:

```solidity
+    function name() external pure override(ERC721, IERC721Metadata)returns (string memory) { }
-    function name() public pure override(ERC721, IERC721Metadata) returns(string memory) { }      
```

    Same goes for the rest of the functions as the example above.

Additionally, a bit of gas would be saved this way.

**--------------------------------**

### [LOW-3] Missing checks for `address(0)` when assigning values to address state variables

**Description:** 

Check for `address(0)` when assigning values to address state variables.

- Found in src/ILOManager.sol (src/ILOManager.sol#L44)

	```solidity
	    FEE_TAKER = _feeTaker;
	```

- Found in src/ILOManager.sol (src/ILOManager.sol#L46)

	```solidity
	    UNIV3_FACTORY = uniV3Factory;
	```

- Found in src/ILOManager.sol (src/ILOManager.sol#L47)

	```solidity
	    ILO_POOL_IMPLEMENTATION = iloPoolImplementation;
	```

- Found in src/ILOManager.sol (src/ILOManager.sol#L48)

	```solidity
	    WETH9 = weth9;
	```

- Found in src/ILOManager.sol (src/ILOManager.sol#L161)

	```solidity
	    FEE_TAKER = _feeTaker;
	```

- Found in src/ILOManager.sol (src/ILOManager.sol#L166)

	```solidity
	    ILO_POOL_IMPLEMENTATION = iloPoolImplementation;
	```

- Found in src/ILOPool.sol (src/ILOPool.sol#L70)

	```solidity
	    _cachedUniV3PoolAddress = params.uniV3Pool;
	```

- Found in src/ILOManager.sol (src/ILOManager.sol#L103)

	```solidity
	    function _initUniV3PoolIfNecessary(PoolAddress.PoolKey memory poolKey, uint160 sqrtPriceX96) internal returns (address pool) {
            // missing params checks here 
            pool = IUniswapV3Factory(UNIV3_FACTORY).getPool(poolKey.token0, poolKey.token1, poolKey.fee);
            if (pool == address(0)) { 
                //...
            }
            //...
        }
	```

- Found in src/ILOManager.sol (src/ILOManager.sol#73)

    In the `ILOManager::initILOPool` function
	
    ```solidity
	    function initILOPool(InitPoolParams calldata params) external override onlyProjectAdmin(params.uniV3Pool) returns (address iloPoolAddress) {
            // missing params checks here
            Project storage _project = _cachedProject[params.uniV3Pool];
            // _; rest of the logic here
        }
	```

**Recommended Mitigation:**

Add zero address checks, for instance:

```solidity
    require(_feeTaker != address(0), "FeeTaker address is zero");
    FEE_TAKER = _feeTaker;

    require(uniV3Factory != address(0), "UniV3Factory address is zero");
    UNIV3_FACTORY = uniV3Factory;

    // same goes for the rest of them ...
```

**--------------------------------**

### [LOW-4] Empty `require()` / `revert()` statements

**Description:** 

Use descriptive reason strings or custom errors for revert paths.

- Found in src/ILOPool.sol (src/ILOPool.sol#L202)

	```solidity
	    require(positionLiquidity >= liquidity2Claim);
	```

- Found in src/base/Initializable.sol (src/base/Initializable.sol#L11)

	```solidity
	    require(!_initialized);
	```

- Found in src/base/Initializable.sol (src/base/Initializable.sol#L16)

	```solidity
	    require(_initialized);
	```

- Found in src/base/LiquidityManagement.sol (src/base/LiquidityManagement.sol#L25)

	```solidity
	    require(msg.sender == _cachedUniV3PoolAddress);
	```

- Found in src/base/Multicall.sol (src/base/Multicall.sol#L18)

	```solidity
	    if (result.length < 68) revert();
	```

- Found in src/libraries/LiquidityAmounts.sol (src/libraries/LiquidityAmounts.sol#L15)

	```solidity
	    require((y = uint128(x)) == x);
	```

- Found in src/libraries/PoolAddress.sol (src/libraries/PoolAddress.sol#L34)

	```solidity
	    require(key.token0 < key.token1);
	```

- Found in src/libraries/SqrtPriceMathPartial.sol (src/libraries/SqrtPriceMathPartial.sol#L31)

	```solidity
	    require(sqrtRatioAX96 > 0);
	```

**Recommended Mitigation:**

Descriptive message should be added in order for the callee to get a properly explained error, for instance:

    ```solidity
        require(positionLiquidity >= liquidity2Claim, "PositionLiquidity must be greater than liquidity2Claim");
    ```

Same goes for the rest of the statements aforementioned.

**--------------------------------**

### [LOW-5] Using `ERC721::_mint()` can be dangerous

**Description:** 

Using `ERC721::_mint()` can mint ERC721 tokens to addresses which don't support ERC721 tokens. Use `_safeMint()` instead of `_mint()` for ERC721.

- Found in src/ILOPool.sol (src/ILOPool.sol#L144)

	```solidity
	    _mint(recipient, (tokenId = _nextId++));
	```

- Found in src/ILOPool.sol (src/ILOPool.sol#L315)

	```solidity
	    _mint(projectConfig.recipient, (tokenId = _nextId++));
	```

Reference: https://bailsec.io/tpost/4kgs4p0m31-is-the-safemint-function-safer-than-the

**Recommended Mitigation:**

```solidity
+	_safeMint(recipient, (tokenId = _nextId++));
-       _mint(recipient, (tokenId = _nextId++));    
```

Same goes for the rest of the statements aforementioned.

**--------------------------------**

### [LOW-6] Missing zero checks when assigning values to state variables

**Description:** 

Check for `address(0)` or 0 values for uints when assigning values to address state variables.

- Found in hardhat-vultisig/contracts/Whitelist.sol (hardhat-vultisig/contracts/Whitelist.sol#L143)

	```solidity
	    function setMaxAddressCap(uint256 newCap) external onlyOwner {
            _maxAddressCap = newCap;
        }
	```

- Found in hardhat-vultisig/contracts/Whitelist.sol (hardhat-vultisig/contracts/Whitelist.sol#L149)

	```solidity
        function setVultisig(address newVultisig) external onlyOwner {
            _vultisig = newVultisig;
        }
	```

- Found in hardhat-vultisig/contracts/Whitelist.sol (hardhat-vultisig/contracts/Whitelist.sol#L161)

	```solidity
        function setOracle(address newOracle) external onlyOwner {
            _oracle = newOracle;
        }
	```

- Found in hardhat-vultisig/contracts/Whitelist.sol (hardhat-vultisig/contracts/Whitelist.sol#L167)

	```solidity
        function setPool(address newPool) external onlyOwner {
            _pool = newPool;
        }
	```

- Found in hardhat-vultisig/contracts/Whitelist.sol (hardhat-vultisig/contracts/Whitelist.sol#L174)

	```solidity
        function setBlacklisted(address blacklisted, bool flag) external onlyOwner {
            _isBlacklisted[blacklisted] = flag;
        }
	```

- Found in hardhat-vultisig/contracts/Whitelist.sol (hardhat-vultisig/contracts/Whitelist.sol#L143)

	```solidity
        function _addWhitelistedAddress(address whitelisted) private {
            if (_whitelistIndex[whitelisted] == 0) {
                _whitelistIndex[whitelisted] = ++_whitelistCount;
            }
        }
	```

- Found in src/ILOManager.sol (src/ILOManager.sol#L58)

	```solidity
        function initProject(InitProjectParams calldata params) external override afterInitialize() returns(address uniV3PoolAddress) {
            
            // no checks for params here as well

            uint64 refundDeadline = params.launchTime + DEFAULT_DEADLINE_OFFSET;
            // ...
        }
	```

**Recommended Mitigation:**

Descriptive message should be added in order for the callee to get a properly explained error, for instance:

	```solidity
	    function setMaxAddressCap(uint256 newCap) external onlyOwner {
+           require(newCap > 0, "Max address cap cannot be 0");
            _maxAddressCap = newCap;
        }
	```

    ```solidity
        function setPool(address newPool) external onlyOwner {
+           require(newPool != address(0), "Pool address cannot be 0");
            _pool = newPool;
        }
	```

Same goes for the rest of the statements aforementioned.

**--------------------------------**

### [LOW-7] Unprotected initializer

**Description:** 

The `Initializable::_disableInitialize` does not have protection and anyone can call the function and disable the initialization via a contract which inherits it.

- Found in src/base/Initializable.sol (src/base/Initializable.sol#L7)

	```solidity
	    function _disableInitialize() internal {
	```

**Recommended Mitigation:**

Add ownership modifier so only the deployer of the contract which inherits `Initializable` can use `_disableInitialize`. 

