### L-1: Centralization Risk for trusted owners

Contracts have owners with privileged rights to perform admin tasks and need to be trusted to not perform malicious updates or drain funds.

<details><summary>7 Found Instances</summary>


- Found in src/ILOManager.sol [Line: 15](src/ILOManager.sol#L15)

	```solidity
	contract ILOManager is IILOManager, Ownable, Initializable {
	```

- Found in src/ILOManager.sol [Line: 150](src/ILOManager.sol#L150)

	```solidity
	    function setPlatformFee(uint16 _platformFee) external onlyOwner() {
	```

- Found in src/ILOManager.sol [Line: 155](src/ILOManager.sol#L155)

	```solidity
	    function setPerformanceFee(uint16 _performanceFee) external onlyOwner() {
	```

- Found in src/ILOManager.sol [Line: 160](src/ILOManager.sol#L160)

	```solidity
	    function setFeeTaker(address _feeTaker) external override onlyOwner() {
	```

- Found in src/ILOManager.sol [Line: 164](src/ILOManager.sol#L164)

	```solidity
	    function setILOPoolImplementation(address iloPoolImplementation) external override onlyOwner() {
	```

- Found in src/ILOManager.sol [Line: 175](src/ILOManager.sol#L175)

	```solidity
	    function setDefaultDeadlineOffset(uint64 defaultDeadlineOffset) external override onlyOwner() {
	```

- Found in src/ILOManager.sol [Line: 180](src/ILOManager.sol#L180)

	```solidity
	    function setRefundDeadlineForProject(address uniV3Pool, uint64 refundDeadline) external override onlyOwner() {
	```

</details>



### L-2: Unsafe ERC20 Operations should not be used

ERC20 functions may not behave as expected. For example: return values are not always meaningful. It is recommended to use OpenZeppelin's SafeERC20 library.

<details><summary>4 Found Instances</summary>


- Found in src/base/PeripheryPayments.sol [Line: 30](src/base/PeripheryPayments.sol#L30)

	```solidity
	            IWETH9(WETH9).transfer(recipient, value);
	```

- Found in src/libraries/TransferHelper.sol [Line: 20](src/libraries/TransferHelper.sol#L20)

	```solidity
	            token.call(abi.encodeWithSelector(IERC20.transferFrom.selector, from, to, value));
	```

- Found in src/libraries/TransferHelper.sol [Line: 34](src/libraries/TransferHelper.sol#L34)

	```solidity
	        (bool success, bytes memory data) = token.call(abi.encodeWithSelector(IERC20.transfer.selector, to, value));
	```

- Found in src/libraries/TransferHelper.sol [Line: 48](src/libraries/TransferHelper.sol#L48)

	```solidity
	        (bool success, bytes memory data) = token.call(abi.encodeWithSelector(IERC20.approve.selector, to, value));
	```

</details>

### L-3: Missing checks for `address(0)` when assigning values to address state variables

Check for `address(0)` when assigning values to address state variables.

<details><summary>7 Found Instances</summary>


- Found in src/ILOManager.sol [Line: 44](src/ILOManager.sol#L44)

	```solidity
	        FEE_TAKER = _feeTaker;
	```

- Found in src/ILOManager.sol [Line: 46](src/ILOManager.sol#L46)

	```solidity
	        UNIV3_FACTORY = uniV3Factory;
	```

- Found in src/ILOManager.sol [Line: 47](src/ILOManager.sol#L47)

	```solidity
	        ILO_POOL_IMPLEMENTATION = iloPoolImplementation;
	```

- Found in src/ILOManager.sol [Line: 48](src/ILOManager.sol#L48)

	```solidity
	        WETH9 = weth9;
	```

- Found in src/ILOManager.sol [Line: 161](src/ILOManager.sol#L161)

	```solidity
	        FEE_TAKER = _feeTaker;
	```

- Found in src/ILOManager.sol [Line: 166](src/ILOManager.sol#L166)

	```solidity
	        ILO_POOL_IMPLEMENTATION = iloPoolImplementation;
	```

- Found in src/ILOPool.sol [Line: 70](src/ILOPool.sol#L70)

	```solidity
	        _cachedUniV3PoolAddress = params.uniV3Pool;
	```

</details>


### L-4: `public` functions not used internally could be marked `external`

Instead of marking a function as `public`, consider marking it as `external` if it is not used internally.

<details><summary>2 Found Instances</summary>


- Found in src/ILOPool.sol [Line: 53](src/ILOPool.sol#L53)

	```solidity
	    function name() public pure override(ERC721, IERC721Metadata) returns (string memory) {
	```

- Found in src/ILOPool.sol [Line: 57](src/ILOPool.sol#L57)

	```solidity
	    function symbol() public pure override(ERC721, IERC721Metadata) returns (string memory) {
	```

</details>


### L-5: Define and use `constant` variables instead of using literals

If the same constant literal value is used multiple times, create a constant state variable and reference it throughout the contract.

<details><summary>2 Found Instances</summary>


- Found in src/base/ILOVest.sol [Line: 19](src/base/ILOVest.sol#L19)

	```solidity
	        uint16 BPS = 10000;
	```

- Found in src/base/ILOVest.sol [Line: 37](src/base/ILOVest.sol#L37)

	```solidity
	        uint16 BPS = 10000;
	```

</details>

### L-6: Event is missing `indexed` fields

Index event fields make the field more quickly accessible to off-chain tools that parse events. However, note that each index field costs extra gas during emission, so it's not necessarily best to index the maximum allowed per event (three fields). Each event should use three indexed fields if there are three or more fields, and gas usage is not particularly of concern for the events in question. If there are fewer than three fields, all of the fields should be indexed.

<details><summary>17 Found Instances</summary>


- Found in src/interfaces/IILOManager.sol [Line: 10](src/interfaces/IILOManager.sol#L10)

	```solidity
	    event ProjectCreated(address indexed uniV3PoolAddress, Project project);
	```

- Found in src/interfaces/IILOManager.sol [Line: 11](src/interfaces/IILOManager.sol#L11)

	```solidity
	    event ILOPoolCreated(address indexed uniV3PoolAddress, address indexed iloPoolAddress, uint256 index);
	```

- Found in src/interfaces/IILOManager.sol [Line: 13](src/interfaces/IILOManager.sol#L13)

	```solidity
	    event ProjectAdminChanged(address indexed uniV3PoolAddress, address oldAdmin, address newAdmin);
	```

- Found in src/interfaces/IILOManager.sol [Line: 14](src/interfaces/IILOManager.sol#L14)

	```solidity
	    event DefaultDeadlineOffsetChanged(address indexed owner, uint64 oldDeadlineOffset, uint64 newDeadlineOffset);
	```

- Found in src/interfaces/IILOManager.sol [Line: 15](src/interfaces/IILOManager.sol#L15)

	```solidity
	    event RefundDeadlineChanged(address indexed project, uint64 oldRefundDeadline, uint64 newRefundDeadline);
	```

- Found in src/interfaces/IILOManager.sol [Line: 17](src/interfaces/IILOManager.sol#L17)

	```solidity
	    event ProjectRefund(address indexed project, uint256 refundAmount);
	```

- Found in src/interfaces/IILOPool.sol [Line: 29](src/interfaces/IILOPool.sol#L29)

	```solidity
	    event IncreaseLiquidity(uint256 indexed tokenId, uint128 liquidity, uint256 amount0, uint256 amount1);
	```

- Found in src/interfaces/IILOPool.sol [Line: 36](src/interfaces/IILOPool.sol#L36)

	```solidity
	    event DecreaseLiquidity(uint256 indexed tokenId, uint128 liquidity, uint256 amount0, uint256 amount1);
	```

- Found in src/interfaces/IILOPool.sol [Line: 44](src/interfaces/IILOPool.sol#L44)

	```solidity
	    event Collect(uint256 indexed tokenId, address recipient, uint256 amount0, uint256 amount1);
	```

- Found in src/interfaces/IILOPool.sol [Line: 46](src/interfaces/IILOPool.sol#L46)

	```solidity
	    event ILOPoolInitialized(address indexed univ3Pool, int32 tickLower, int32 tickUpper, SaleInfo saleInfo, VestingConfig[] vestingConfig);
	```

- Found in src/interfaces/IILOPool.sol [Line: 48](src/interfaces/IILOPool.sol#L48)

	```solidity
	    event Claim(address indexed user, uint256 tokenId,uint128 liquidity, uint256 amount0, uint256 amount1, uint256 feeGrowthInside0LastX128, uint256 feeGrowthInside1LastX128);
	```

- Found in src/interfaces/IILOPool.sol [Line: 49](src/interfaces/IILOPool.sol#L49)

	```solidity
	    event Buy(address indexed investor, uint256 tokenId, uint256 raiseAmount, uint128 liquidity);
	```

- Found in src/interfaces/IILOPool.sol [Line: 50](src/interfaces/IILOPool.sol#L50)

	```solidity
	    event PoolLaunch(address indexed project, uint128 liquidity, uint256 token0, uint256 token1);
	```

- Found in src/interfaces/IILOPool.sol [Line: 51](src/interfaces/IILOPool.sol#L51)

	```solidity
	    event UserRefund(address indexed user, uint256 tokenId, uint256 raiseTokenAmount);
	```

- Found in src/interfaces/IILOPool.sol [Line: 52](src/interfaces/IILOPool.sol#L52)

	```solidity
	    event ProjectRefund(address indexed projectAdmin, uint256 saleTokenAmount);
	```

- Found in src/interfaces/IILOWhitelist.sol [Line: 7](src/interfaces/IILOWhitelist.sol#L7)

	```solidity
	    event SetWhitelist(address indexed user, bool isWhitelist);
	```

- Found in src/interfaces/IILOWhitelist.sol [Line: 8](src/interfaces/IILOWhitelist.sol#L8)

	```solidity
	    event SetOpenToAll(bool openToAll);
	```

</details>



### L-7: Empty `require()` / `revert()` statements

Use descriptive reason strings or custom errors for revert paths.

<details><summary>8 Found Instances</summary>


- Found in src/ILOPool.sol [Line: 202](src/ILOPool.sol#L202)

	```solidity
	            require(positionLiquidity >= liquidity2Claim);
	```

- Found in src/base/Initializable.sol [Line: 11](src/base/Initializable.sol#L11)

	```solidity
	        require(!_initialized);
	```

- Found in src/base/Initializable.sol [Line: 16](src/base/Initializable.sol#L16)

	```solidity
	        require(_initialized);
	```

- Found in src/base/LiquidityManagement.sol [Line: 25](src/base/LiquidityManagement.sol#L25)

	```solidity
	        require(msg.sender == _cachedUniV3PoolAddress);
	```

- Found in src/base/Multicall.sol [Line: 18](src/base/Multicall.sol#L18)

	```solidity
	                if (result.length < 68) revert();
	```

- Found in src/libraries/LiquidityAmounts.sol [Line: 15](src/libraries/LiquidityAmounts.sol#L15)

	```solidity
	        require((y = uint128(x)) == x);
	```

- Found in src/libraries/PoolAddress.sol [Line: 34](src/libraries/PoolAddress.sol#L34)

	```solidity
	        require(key.token0 < key.token1);
	```

- Found in src/libraries/SqrtPriceMathPartial.sol [Line: 31](src/libraries/SqrtPriceMathPartial.sol#L31)

	```solidity
	        require(sqrtRatioAX96 > 0);
	```

</details>


### L-8: Modifiers invoked only once can be shoe-horned into the function



<details><summary>1 Found Instances</summary>


- Found in src/base/Initializable.sol [Line: 15](src/base/Initializable.sol#L15)

	```solidity
	    modifier afterInitialize() {
	```

</details>




### L-9: Internal functions called only once can be inlined

Instead of separating the logic into a separate function, consider inlining the logic into the calling function. This can reduce the number of function calls and improve readability.

<details><summary>1 Found Instances</summary>


- Found in src/base/LiquidityManagement.sol [Line: 41](src/base/LiquidityManagement.sol#L41)

	```solidity
	    function addLiquidity(AddLiquidityParams memory params)
	```

</details>


### L-10: Unused Modifier

it is recommended that the definition be removed when modifier is unused

<details><summary>1 Found Instances</summary>


- Found in src/interfaces/IILOWhitelist.sol [Line: 16](src/interfaces/IILOWhitelist.sol#L16)

	```solidity
	    modifier onlyProjectAdmin virtual;
	```

</details>

