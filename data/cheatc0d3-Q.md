# QA Report: Vultisig

## L-01: Absence of Address Removal Functionality in Whitelist and Blacklist

## Impact
The lack of functionality to remove addresses from the whitelist and blacklist restricts the dynamic management of these lists, potentially impacting the adaptability and security of the contract. Without the ability to remove addresses, the contract cannot adjust to changing conditions or rectify erroneous additions, which may lead to inefficient or unsafe contract operations. This could hinder the contract's ability to respond to evolving security threats or operational requirements, leading to possible stagnation of the whitelist/blacklist and misuse of the contract functionality.

## Proof of Concept
The current contract implementation includes mappings for whitelisted and blacklisted addresses but lacks methods to remove an address once added. For example, the `_whitelistIndex` and `_isBlacklisted` mappings are only modified to add addresses but not to remove them:

https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/contracts/Whitelist.sol#L41

https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/contracts/Whitelist.sol#L185

```solidity
mapping(address => uint256) private _whitelistIndex;  // Tracks whitelisted addresses
mapping(address => bool) private _isBlacklisted;      // Tracks blacklisted addresses

function addWhitelistedAddress(address whitelisted) external onlyOwner {
    if (_whitelistIndex[whitelisted] == 0) {
        _whitelistIndex[whitelisted] = ++_whitelistCount;
    }
}

function setBlacklisted(address blacklisted, bool flag) external onlyOwner {
    _isBlacklisted[blacklisted] = flag;
}
```

These functions add addresses but do not provide a mechanism for removal, which can be verified by the absence of corresponding removal functions in the contract.

## Recommended Mitigation Steps
Introduce functions to remove addresses from both the whitelist and blacklist. Ensure these functions reset the mapping values to their default state and include necessary access control checks to prevent unauthorized modifications.


## L-02: Inadequate Validation of Whitelist Index Setting Leading to Potential Whitelist Bypass

## Impact
The current implementation of `setAllowedWhitelistIndex` does not check whether the newly set index is within the bounds of existing whitelist entries. This oversight could lead to security vulnerabilities where an unauthorized or unintended address remains whitelisted, potentially allowing unauthorized access or actions. Additionally, setting an index beyond the bounds of actual whitelisted entries may inadvertently block all whitelisted users from performing actions they are normally permitted to, disrupting normal operations and user trust.

## Proof of Concept
The function `setAllowedWhitelistIndex` allows the owner to set the index that determines which addresses are considered whitelisted:

https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/contracts/Whitelist.sol#L179

```solidity
function setAllowedWhitelistIndex(uint256 newIndex) external onlyOwner {
    _allowedWhitelistIndex = newIndex;
}
```

This function sets `_allowedWhitelistIndex` without verifying that the new index is within the range of indices assigned to currently whitelisted addresses. This lack of validation means that the contract owner could unintentionally or maliciously set an index that does not correlate to the actual number of addresses whitelisted, thus either excluding or wrongly including addresses.

## Recommended Mitigation Steps
Modify the `setAllowedWhitelistIndex` function to include a check that the new index is not greater than the total count of whitelisted addresses. This ensures that the index remains within valid bounds.

```solidity
   function setAllowedWhitelistIndex(uint256 newIndex) external onlyOwner {
       require(newIndex <= _whitelistCount, "Index exceeds number of whitelisted addresses");
       _allowedWhitelistIndex = newIndex;
   }
```

## L-03: Lack of Batch Update Functionality for Contribution Limits Affects Scalability and Efficiency

## Impact
The absence of a batch update function for setting contribution limits in the current smart contract design hinders scalability and operational efficiency. This limitation compels contract administrators to update contribution limits on a per-address basis, which is time-consuming, costly in terms of gas fees, and prone to human error, especially when dealing with large numbers of users. This inefficiency could lead to delays in updating critical operational parameters, affecting user experience and potentially leading to missed opportunities for timely adjustments based on market conditions or specific promotional campaigns.

## Proof of Concept
The existing contract does not provide a method for updating the contribution limits for multiple addresses simultaneously. Currently, administrators must manually set contribution limits one at a time, as demonstrated by the absence of a batch function in the contract's code:

https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/contracts/Whitelist.sol#L222

## Recommended Mitigation Steps
Introduce a new function to handle the batch updating of contribution limits. This function should accept two arrays – one for addresses and one for their corresponding new limits – and iterate through them to update each address. This can also be used to customize limits based on different criteria or user categories.

```solidity
function updateBatchContributionLimits(address[] calldata addresses, uint256[] calldata limits) external onlyOwner {
    require(addresses.length == limits.length, "Arrays must have the same length");
    for (uint i = 0; i < addresses.length; i++) {
        _contributed[addresses[i]] = limits[i];
    }
}
```

## L-04: Inability to Reset or Adjust Contributions Hinders Flexible Fund Management

## Impact
The current smart contract lacks the capability to reset or adjust the contributions tracked in the `_contributed` mapping. This limitation impedes the contract's flexibility and adaptability, especially in scenarios where the contract might be reused for multiple funding rounds or phases. Without the ability to reset contributions, administrators cannot clear or correct the contribution records efficiently, potentially leading to inaccuracies in fund tracking and allocation. This might result in operational challenges, disputes, or errors in fund management, especially if contribution limits or conditions change over time.

## Proof of Concept
The contract contains a mapping `_contributed` which tracks the amount of ETH contributed by each address. However, there is no functionality provided to reset or adjust these contributions, which is a significant oversight in scenarios where contribution data needs to be updated or corrected.

https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/contracts/Whitelist.sol#L45

```solidity
mapping(address => uint256) private _contributed; // Tracks contributed amounts in ETH
```

This mapping is used to enforce contribution limits but lacks methods to manage or rectify the data it holds once set.

## Recommended Mitigation Steps
1. Provide a function to reset individual contribution records or the entire mapping. This allows for greater control and flexibility in managing contributions, particularly useful between different phases of funding or in correcting errors.

```solidity
function resetContribution(address user) external onlyOwner {
    _contributed[user] = 0;
}

function resetAllContributions(address[] calldata users) external onlyOwner {
    for (uint i = 0; i < users.length; i++) {
        _contributed[users[i]] = 0;
    }
}
```

2. Add functions to adjust contributions up or down, allowing for corrections without the need to fully reset the contribution amount.

```solidity
function adjustContribution(address user, int256 amount) external onlyOwner {
    require(_contributed[user] + amount >= 0, "Invalid adjustment leads to negative contribution");
    _contributed[user] += uint256(int256(_contributed[user]) + amount);
}
```

3. Emit events for any reset or adjustment of contributions to ensure transparency and enable tracking of changes over time.

```solidity
event ContributionReset(address indexed user);
event ContributionAdjusted(address indexed user, int256 amount);
```


## L-05: Excessive Gas Usage and Information Dislcosure Risks Due to Overly Verbose Event Parameters

## Impact
The logging of the entire `Project` struct in the `ProjectCreated` event and potentially excessive parameters in the `ILOPoolCreated` event could lead to higher gas costs during transactions. This inefficiency impacts the overall cost-effectiveness of interacting with the contract, potentially deterring users due to higher transaction fees. Additionally, the excessive detail in event logs could lead to unnecessary exposure of contract state details, which may not always be desirable from a data privacy or contract integrity standpoint.

## Proof of Concept

https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/ILOManager.sol#L64

```solidity
  emit ProjectCreated(uniV3PoolAddress, _cachedProject[uniV3PoolAddress]);
```

This event is emitted in the `initProject` function after initializing a project. The event logs the entire `Project` struct, which includes multiple fields such as `saleToken`, `raiseToken`, `fee`, `initialPoolPriceX96`, `launchTime`, `refundDeadline`, `admin`, and more. This can result in a high gas cost due to the storage and processing of extensive data.

https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/src/ILOManager.sol#L85

```solidity
  emit ILOPoolCreated(_project.uniV3PoolAddress, iloPoolAddress, _initializedILOPools[params.uniV3Pool].length);
```

This event is emitted in the `initILOPool` function after initializing an ILO pool. It logs the Uniswap V3 pool address, the new ILO pool address, and the index of the new pool. Depending on the utility of the index information and the frequency of calls, this might be streamlined if the index does not provide significant tracking or operational benefits.

## Recommended Mitigation Steps
For the `ProjectCreated` event, consider only logging critical identifiers such as `uniV3PoolAddress` and any key state changes that are necessary for tracking the project status externally.

For the `ILOPoolCreated` event, assess whether the index of the new pool (`_initializedILOPools[params.uniV3Pool].length`) is necessary for external tracking or if it can be omitted to reduce the verbosity of the logs.

## L-06: Potential Timestamp Manipulation in `getOldestObservationSecondsAgo` Leading to Stale Data Usage

## Impact
The `getOldestObservationSecondsAgo` function in the `OracleLibrary` relies on `block.timestamp` to calculate the age of the oldest observation in a Uniswap V3 pool. Since miners can manipulate `block.timestamp` within certain limits (up to approximately 900 seconds forward or backward), there is a risk that the calculated `secondsAgo` could inaccurately reflect the age of the data. This can lead to scenarios where the data is either considered more current or more outdated than it actually is, potentially affecting financial decisions based on this stale or erroneously fresh data.

## Proof of Concept

https://github.com/code-423n4/2024-06-vultisig/blob/cb72b1e9053c02a58d874ff376359a83dc3f0742/hardhat-vultisig/contracts/oracles/uniswap/uniswapv0.8/OracleLibrary.sol#L75

```solidity
secondsAgo = uint32(block.timestamp) - observationTimestamp;
```
In this line, `block.timestamp` is used directly to compute the age of the data. Miners could set a future `block.timestamp` close to the 900 seconds limit, making the `secondsAgo` appear smaller than actual, implying fresher data. Conversely, a lower `block.timestamp` could artificially age the data. Both scenarios could mislead financial strategies relying on this timestamp for decision-making processes.

Affected code snippet:
```solidity
function getOldestObservationSecondsAgo(address pool) internal view returns (uint32 secondsAgo) {
    (, , uint16 observationIndex, uint16 observationCardinality, , , ) = IUniswapV3Pool(pool).slot0();
    require(observationCardinality > 0, "NI");

    (uint32 observationTimestamp, , , bool initialized) = IUniswapV3Pool(pool).observations(
        (observationIndex + 1) % observationCardinality
    );

    if (!initialized) {
        (observationTimestamp, , , ) = IUniswapV3Pool(pool).observations(0);
    }

    secondsAgo = uint32(block.timestamp) - observationTimestamp;
}
```

## Recommended Mitigation Steps

Implement checks to guard against significant deviations in `block.timestamp` that could affect the outcome of the timestamp calculation. This might include using an average or median timestamp of the last several blocks as a reference to reduce the impact of manipulation in a single block.
