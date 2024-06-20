## Issue
Anyone can front run the owner and can get added into whitelist using `Whitelist.sol:receive()` function even if the owner had their own whitelist addresses. The owner can blacklist them but it would take time and efforts.

## Tools Used
Manual Review

## Recommended Mitigation Steps
make `_isSelfWhiteListDisabled = true` in the constructor of `Whitelist.sol`, so that no one can get added to whitelist when owner have enough whitelist address and can make it false later when they need more addresses.