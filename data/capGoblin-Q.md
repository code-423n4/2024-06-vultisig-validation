# QA Report

## [L-01] `ILOPool::initialize` & `Multicall::multicall` susecptible to DOS attack
The `initialize` function in `ILOPool` and the `multicall` function in `Multicall` are vulnerable to Denial of Service (DoS) attacks due to their handling of large input arrays. In `initialize`, the `params.vestingConfigs` parameter leads to nested loops in `_validateSharesAndVests` and `_validateVestSchedule`, risking high gas consumption due to large `params.vestingConfigs`. Similarly, `multicall` loops through the `data` array, risking excessive gas use if the array is very large. Malicious user can exploit this by submitting large arrays to exhaust the gas limit, causing transaction failures and network congestion.

https://github.com/code-423n4/2024-06-vultisig/blob/main/src/ILOPool.sol#L61-L103
```solidity
 function initialize(InitPoolParams calldata params) external override whenNotInitialized() {
        _nextId = 1;
        // initialize imutable state
        MANAGER = msg.sender;
        IILOManager.Project memory _project = IILOManager(MANAGER).project(params.uniV3Pool);

        WETH9 = IILOManager(MANAGER).WETH9();
        RAISE_TOKEN = _project.raiseToken;
        SALE_TOKEN = _project.saleToken;
        _cachedUniV3PoolAddress = params.uniV3Pool;
        _cachedPoolKey = _project._cachedPoolKey;
        TICK_LOWER = params.tickLower;
        TICK_UPPER = params.tickUpper;
        SQRT_RATIO_LOWER_X96 = params.sqrtRatioLowerX96;
        SQRT_RATIO_UPPER_X96 = params.sqrtRatioUpperX96;
        SQRT_RATIO_X96 = _project.initialPoolPriceX96;

        // rounding up to make sure that the number of sale token is enough for sale
        (uint256 maxSaleAmount,) = _saleAmountNeeded(params.hardCap);
        // initialize sale
        saleInfo = SaleInfo({
            hardCap: params.hardCap,
            softCap: params.softCap,
            maxCapPerUser: params.maxCapPerUser,
            start: params.start,
            end: params.end,
            maxSaleAmount: maxSaleAmount
        });

@>      _validateSharesAndVests(_project.launchTime, params.vestingConfigs);
        // initialize vesting
@>      for (uint256 index = 0; index < params.vestingConfigs.length; index++) {
            _vestingConfigs.push(params.vestingConfigs[index]);
        }

        emit ILOPoolInitialized(
            params.uniV3Pool,
            TICK_LOWER,
            TICK_UPPER,
            saleInfo,
            params.vestingConfigs
        );
    }
```
https://github.com/code-423n4/2024-06-vultisig/blob/main/src/base/Multicall.sol#L11-L27

```solidity
    function multicall(bytes[] calldata data) public payable override returns (bytes[] memory results) {
        results = new bytes[](data.length);
@>      for (uint256 i = 0; i < data.length; i++) {
            (bool success, bytes memory result) = address(this).delegatecall(data[i]);

            if (!success) {
                // Next 5 lines from https://ethereum.stackexchange.com/a/83577
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
## Recommended Mitigation:
To prevent such attacks, you can set a reasonable limit on the size of the arrays processed by these functions and revert if the length exceeds the limit. Or you can also monitor gas consumption to handle near-limit scenarios gracefully.
For example to monitor gas consumption and handle near-limit scenario,
```solidity
    function multicall(bytes[] calldata data) public payable override returns (bytes[] memory results) {
      uint256 initialGas = gasleft();
      for (uint256 i = 0; i < data.length; i++) {
        // Perform some operations
        // Check gas consumption
        if (initialGas - gasleft() > GAS_LIMIT_THRESHOLD) {
            // Store state and exit gracefully
            break;
        }
    }
```

## [L-02] Incorrect input data type for `observations` in `OracleLibrary::getOldestObservationSecondsAgo`
According to `contract.MockObservations.md` the signature for observations is `function observations(uint256 index) external view returns (uint32, int56, uint160, bool);` where the input `index` is `uint256`. Where in `OracleLibrary::getOldestObservationSecondsAgo` the arg is of data type `uint16`.

https://github.com/code-423n4/2024-06-vultisig/blob/main/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol#L61-L76
```solidity
    function getOldestObservationSecondsAgo(address pool) internal view returns (uint32 secondsAgo) {
        (, , uint16 observationIndex, uint16 observationCardinality, , , ) = IUniswapV3Pool(pool).slot0();
        require(observationCardinality > 0, "NI");

        (uint32 observationTimestamp, , , bool initialized) = IUniswapV3Pool(pool).observations(
@>         (observationIndex + 1) % observationCardinality
        );

        // The next index might not be initialized if the cardinality is in the process of increasing
        // In this case the oldest observation is always in index 0
        if (!initialized) {
            (observationTimestamp, , , ) = IUniswapV3Pool(pool).observations(0);
        }

        secondsAgo = uint32(block.timestamp) - observationTimestamp;
    }
```

https://github.com/code-423n4/2024-06-vultisig/blob/main/docs/src/src/test/MockObservations.sol/contract.MockObservations.md
```solidity
function observations(uint256 index) external view returns (uint32, int56, uint160, bool);
```

## Recommended Mitigation:
```solidity
function getOldestObservationSecondsAgo(address pool) internal view returns (uint32 secondsAgo) {
    (, , uint16 observationIndex, uint16 observationCardinality, , , ) = IUniswapV3Pool(pool).slot0();
    require(observationCardinality > 0, "NI");

    (uint32 observationTimestamp, , , bool initialized) = IUniswapV3Pool(pool).observations(
@>       uint256((observationIndex + 1) % observationCardinality) // Cast observationIndex to uint256
    );

    // The next index might not be initialized if the cardinality is in the process of increasing
    // In this case the oldest observation is always in index 0
    if (!initialized) {
        (observationTimestamp, , , ) = IUniswapV3Pool(pool).observations(0);
    }

    secondsAgo = uint32(block.timestamp) - observationTimestamp;
}
```

## [L-03] Use `ERC721::_safeMint()` instead of `_mint()`

Use `ERC721::_safeMint()` instead of `ERC721::_mint()` in `ILOPool.sol` L144 & L315. Using ERC721::_mint() can mint ERC721 tokens to addresses that don't support ERC721 tokens, while ERC721::_safeMint() ensures that ERC721 tokens are only minted to addresses which support them. [OpenZeppelin discourages the use of `_mint()`, use `_safeMint` whenever possible.
](https://docs.openzeppelin.com/contracts/4.x/api/token/erc721#ERC721-_safeMint-address-uint256-)

https://github.com/code-423n4/2024-06-vultisig/blob/main/src/ILOPool.sol#L126-L176
```solidity
 function buy(uint256 raiseAmount, address recipient)
        external override 
        returns (
            uint256 tokenId,
            uint128 liquidityDelta
        )
    {
        require(_isWhitelisted(recipient), "UA");
        require(block.timestamp > saleInfo.start && block.timestamp < saleInfo.end, "ST");
        // check if raise amount over capacity
        require(saleInfo.hardCap - totalRaised >= raiseAmount, "HC");
        totalRaised += raiseAmount;

        require(totalSold() <= saleInfo.maxSaleAmount, "SA");

        // if investor already have a position, just increase raise amount and liquidity
        // otherwise, mint new nft for investor and assign vesting schedules
        if (balanceOf(recipient) == 0) {
@>          _mint(recipient, (tokenId = _nextId++));
            _positionVests[tokenId].schedule = _vestingConfigs[0].schedule;
        } else {
            tokenId = tokenOfOwnerByIndex(recipient, 0);
        }

        Position storage _position = _positions[tokenId];
        require(raiseAmount <= saleInfo.maxCapPerUser - _position.raiseAmount, "UC");
        _position.raiseAmount += raiseAmount;

        // get amount of liquidity associated with raise amount
        if (RAISE_TOKEN == _cachedPoolKey.token0) {
            liquidityDelta = LiquidityAmounts.getLiquidityForAmount0(SQRT_RATIO_X96, SQRT_RATIO_UPPER_X96, raiseAmount);
        } else {
            liquidityDelta = LiquidityAmounts.getLiquidityForAmount1(SQRT_RATIO_LOWER_X96, SQRT_RATIO_X96, raiseAmount);
        }

        require(liquidityDelta > 0, "ZA");

        // calculate amount of share liquidity investor recieve by INVESTOR_SHARES config
        liquidityDelta = uint128(FullMath.mulDiv(liquidityDelta, _vestingConfigs[0].shares, BPS));
        
        // increase investor's liquidity
        _position.liquidity += liquidityDelta;

        // update total liquidity locked for vest and assiging vesing schedules
        _positionVests[tokenId].totalLiquidity = _position.liquidity;

        // transfer fund into contract
        TransferHelper.safeTransferFrom(RAISE_TOKEN, msg.sender, address(this), raiseAmount);

        emit Buy(recipient, tokenId, raiseAmount, liquidityDelta);
    }
```
https://github.com/code-423n4/2024-06-vultisig/blob/main/src/ILOPool.sol#L269-L335
```solidity
function launch() external override OnlyManager() {
        require(!_launchSucceeded, "PL");
        // when refund triggered, we can not launch pool anymore
        require(!_refundTriggered, "IRF");
        // make sure that soft cap requirement match
        require(totalRaised >= saleInfo.softCap, "SC");
        uint128 liquidity;
        address uniV3PoolAddress = _cachedUniV3PoolAddress;
        {
            uint256 amount0;
            uint256 amount1;
            uint256 amount0Min;
            uint256 amount1Min;
            address token0Addr = _cachedPoolKey.token0;

            // calculate sale amount of tokens needed for launching pool
            if (token0Addr == RAISE_TOKEN) {
                amount0 = totalRaised;
                amount0Min = totalRaised;
                (amount1, liquidity) = _saleAmountNeeded(totalRaised);
            } else {
                (amount0, liquidity) = _saleAmountNeeded(totalRaised);
                amount1 = totalRaised;
                amount1Min = totalRaised;
            }

            // actually deploy liquidity to uniswap pool
            (amount0, amount1) = addLiquidity(AddLiquidityParams({
                pool: IUniswapV3Pool(uniV3PoolAddress),
                liquidity: liquidity,
                amount0Desired: amount0,
                amount1Desired: amount1,
                amount0Min: amount0Min,
                amount1Min: amount1Min
            }));

            emit PoolLaunch(uniV3PoolAddress, liquidity, amount0, amount1);
        }

        IILOManager.Project memory _project = IILOManager(MANAGER).project(uniV3PoolAddress);

        // assigning vests for the project configuration
        for (uint256 index = 1; index < _vestingConfigs.length; index++) {
            uint256 tokenId;
            VestingConfig memory projectConfig = _vestingConfigs[index];
            // mint nft for recipient
@>          _mint(projectConfig.recipient, (tokenId = _nextId++));
            uint128 liquidityShares = uint128(FullMath.mulDiv(liquidity, projectConfig.shares, BPS));

            Position storage _position = _positions[tokenId];
            _position.liquidity = liquidityShares;
            _positionVests[tokenId].totalLiquidity = liquidityShares;

            // assign vesting schedule
            LinearVest[] storage schedule = _positionVests[tokenId].schedule;
            for (uint256 i = 0; i < projectConfig.schedule.length; i++) {
                schedule.push(projectConfig.schedule[i]);
            }

            emit Buy(projectConfig.recipient, tokenId, 0, liquidityShares);
        }

        // transfer back leftover sale token to project admin
        _refundProject(_project.admin);

        _launchSucceeded = true;
    }
```

## Recommended Mitigation: 
Use `_safeMint()` instead of `_mint()` for ERC721.

## [L-04] Use Openzepplin's `Ownable2Step` instead of `Ownable` for the transfer of ownership
To enhance the security of ownership transfer in your Solidity contract, it's advisable to use OpenZeppelin's Ownable2Step pattern instead of Ownable. In `ILOManager` the `initialize` and `constructor` where `transferOwnership` is used. Here can use `Ownable2Step::transferOwnership`. This adds an extra layer of security by requiring confirmation from the new owner before finalizing the transfer

https://github.com/code-423n4/2024-06-vultisig/blob/main/src/ILOManager.sol#L29-L49
```solidity
    constructor () {
@>      transferOwnership(tx.origin);
    }

    function initialize(
        address initialOwner,
        address _feeTaker,
        address iloPoolImplementation,
        address uniV3Factory,
        address weth9,
        uint16 platformFee,
        uint16 performanceFee
    ) external override whenNotInitialized() {
        PLATFORM_FEE = platformFee;
        PERFORMANCE_FEE = performanceFee;
        FEE_TAKER = _feeTaker;
@>      transferOwnership(initialOwner);
        UNIV3_FACTORY = uniV3Factory;
        ILO_POOL_IMPLEMENTATION = iloPoolImplementation;
        WETH9 = weth9;
    }
```
## Recommended Mitigation:
Just import `Ownable2Step.sol` from `Openzeppelin` and inherit it to use `Ownable2Step::transferOwnership`
```solidity
import "@openzeppelin/contracts/access/Ownable2Step.sol";
contract ILOManager is IILOManager, Ownable2Step, Initializable {
  ...
}
```

## [L-05] Missing Input validations
Ensure proper input validation and zero value checks are implemented in `constructor` for `UniswapV3Oracle` where `pool` is direcly used in `OracleLibrary.getOldestObservationSecondsAgo` without any validations. Also in `initialize` in `ILOPool` and `initProject`, `initialize` in `ILOManager`.

https://github.com/code-423n4/2024-06-vultisig/blob/main/hardhat-vultisig/contracts/oracles/uniswap/UniswapV3Oracle.sol#L27-L31
https://github.com/code-423n4/2024-06-vultisig/blob/main/src/ILOPool.sol#L61-L103
https://github.com/code-423n4/2024-06-vultisig/blob/main/src/ILOManager.sol#L33-L49
https://github.com/code-423n4/2024-06-vultisig/blob/main/src/ILOManager.sol#L57-L69

## Recommended Mitigation:
Ensure that every function validates its inputs against invalid or zero values. Use `require` or using if Statements with `revert` like `revert ZeroValue()`, and `revert ZeroAddress()` effectively to check conditions before executing any logic.

## [L-06] Critical Changes Should Use Two-Step Procedure
`owner` has critical privileges in the protocol. Multiple Functions in `ILOManager`, `WhiteList` and `VultigWhitelisted`. Where the protocol might become the victim of a Clipboard Replacement Attack, where the owner copies the address that does critical changes to the protocol, but malware replaces the address on the clipboard with a different attacker-controlled address. 

https://github.com/code-423n4/2024-06-vultisig/blob/main/src/ILOManager.sol#L150-L184
https://github.com/code-423n4/2024-06-vultisig/blob/main/hardhat-vultisig/contracts/Whitelist.sol#L136-L195
https://github.com/code-423n4/2024-06-vultisig/blob/main/hardhat-vultisig/contracts/extensions/VultisigWhitelisted.sol#L22-L24

## Recommended Mitigation:
Lack of two-step procedure for critical operations leaves them error-prone. Consider adding two step procedure on the critical functions.

## [L-07] Incomplete NatSpec comments
Some of the functions have missing or incomplete Ethereum Natural Specification Format (NatSpec) comments. 
- `compute` function in `PositionKey.sol`
- `addLiquidity` function in `LiquidityManagement.sol`

## [L-08] Missing param comment
The `peek` function in `UniswapV3Oracle.sol` is missing param `baseAmount`, add `baseAmount` in NatSpec comments as `@param` tag with a short description, enhancing readability and consistency.

## [L-09] Remove Unused imports
In `UniswapV3Oracle` the import statement `import {IUniswapV3Pool} from "@uniswap/v3-core/contracts/interfaces/IUniswapV3Pool.sol";` is not used in the contract anywhere. Consider removing it, to maintain clean and consistent code.

## [L-10] Typos in Comments
- The comment for `_launchSucceeded` in `ILOPool` is `/// @dev when lauch successfully we can not refund anymore` Consider correcting it to `/// @dev when launch successful, we can not refund anymore`.
- The comment in `ILOPool::initialize` before assigning `MANAGER` the comment says `// initialize imutable state` we can change it to `// initialize immutable state`
- And in `ILOPool::buy`  before assigning `_positionVests[tokenId].totalLiquidity` we have the comment `// update total liquidity locked for vest and assiging vesing schedules` which we can change to `// update total liquidity locked for vest and assigning vesting schedules`

## [L-11] Iconsistency in documentation and implementation
- According to the interface documentation (interface.IILOSale.md), the signature for the `buy` function specifies the return type as `(uint256 tokenId, uint128 liquidity)`. However, in the implementation within `ILOPool`, the return variable `liquidityDelta` is used instead of `liquidity`. To align with the documentation, it is recommended to rename `liquidityDelta` to `liquidity` in the implementation of the `buy` function.
- According to `ILOVest.sol`, the signature for the `_claimableLiquidity` function specifies the return type as `function _claimableLiquidity(uint256 tokenId) internal view virtual returns (uint128 claimableLiquidity)`. But in the implementation within `ILOPool`, the return type is specified as `function _claimableLiquidity(uint256 tokenId) internal view virtual returns (uint128) {}`, without explicitly naming the variable `claimableLiquidity`. For consistency between documentation and implementation, it is recommended to modify the implementation to explicitly name the return variable as `claimableLiquidity`.

## [L-12] Can improve readability in `OracleLibrary`
We can improve the readability of the `consult` function, by removing redundant casting operations of `int56(uint56(period))`, The cast of period twice is redundant and do not provide additional type safety or clarity but add complexity and reduce readability, we can save in a stack variable and use it all around the function.
```solidity
   function consult(address pool, uint32 period) internal view returns (int24 timeWeightedAverageTick) {
        require(period != 0, "BP");

        uint32[] memory secondAgos = new uint32[](2);
        secondAgos[0] = period;
        secondAgos[1] = 0;

        (int56[] memory tickCumulatives, ) = IUniswapV3Pool(pool).observe(secondAgos);
        int56 tickCumulativesDelta = tickCumulatives[1] - tickCumulatives[0];

        timeWeightedAverageTick = int24(tickCumulativesDelta / int56(uint56(period)));

        // Always round to negative infinity
        if (tickCumulativesDelta < 0 && (tickCumulativesDelta % int56(uint56(period)) != 0)) timeWeightedAverageTick--;
    }
```

## [L-13] Add Inline Comments in `UniswapV3Oracle::peek`
The `peek` function calculates a quoted WETH amount based on some operations involving `baseAmount`. While the function is relatively straightforward, adding inline comments can improve code readability and understanding. This practice aligns with Solidity's best practices and improves the overall quality of the codebase.

## [L-14] New version of OpenZeppelin Contracts can be used
Using old versions of 3rd-party libraries in the build process can introduce vulnerabilities to the protocol code. The latest version is 5.0.2, version used in project is 4.x.x.

### Risks
Older versions of OpenZeppelin contracts might not have fixes for known security vulnerabilities.
Older versions might contain features or functionality that have been deprecated in recent versions.
Newer versions often come with new features, optimizations, and improvements that are not available in older versions.


## [L-15] Order of functions
Ordering helps readers identify which functions they can call and to find the constructor and fallback definitions easier. But there are contracts in the project that do not comply with this. Eg. `vestingStatus` function in `ILOPool` which is an external function defined in-between two internal functions. 
The solidity documentation recommends the following order for functions:

- constructor
- receive function (if exists)
- fallback function (if exists)
- external
- public
- internal
- private