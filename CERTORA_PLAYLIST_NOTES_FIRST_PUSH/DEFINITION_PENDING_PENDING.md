# https://docs.certora.com/en/latest/docs/confluence/anatomy/definitions.html

- **I think they are like creating global constants that can be used for harness purposes**
- **In short they are similar to solidity functions**
```c
definition MAX_UINT256() returns uint256 = 0xffffffffffffffffffffffffffffffff;

//usage
assert x/MAX_UINT256() == 55;

//spec vs solidity

//spec
definition kuchBhi(uint256 x) returns bool = x == 10;

//is equal to solidity
function kuchBhi(uint256 x) public pure return(bool) {
    return x == 10;
}
```