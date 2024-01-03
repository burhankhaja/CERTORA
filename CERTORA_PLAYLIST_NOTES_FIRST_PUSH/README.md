## **Notes from certora prover playlist**
[`LINK`](https://www.youtube.com/watch?v=sdEfc-58CUE&list=PLKtu7wuOMP9XHbjAevkw2nL29YMubqEFj&index=1&pp=iAQB)

## Dummy commands
**cli**
```bash
 certoraRun  TESTME.sol:IndirectBug --verify IndirectBug:testme.spec --solc /home/whoami/.local/bin/solc --rule_sanity basic --x c
```
**certcmd.sh**
```
//run certcmd
solc-select use <version> 
 
 export PATH=$PATH:/home/whoami/.local/bin/solc  
 
 export CERTORAKEY=$private
 
 certoraRun ERC20.sol --verify ERC20:ERC20.spec --solc /home/whoami/.local/bin/solc
```

