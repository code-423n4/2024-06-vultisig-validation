## [L-01] Potential Division by Zero in `getAmount0ForLiquidity` and `getAmount1ForLiquidity`

## Description
Add checks to be sure there is no division to zero.

## [L-02] Deleting position vests will not delete schedule array

## Description
`delete _positionVests[tokenId];` will not delete schedule array values

