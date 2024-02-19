- __`nativeBalances[address]`__ is a built in mapping in certora spec that checks the native eth balance of any address
- suppose i need to check eth balance of contract under verification,
    ```solidity
    nativeBalances[currentContract]
    ```
- similarly
  ```solidity
  // example one
  function balanceHelper() returns (uint){
    return nativeBalances[msg.sender];
  }

  // example two
  assert nativeBalances[e.msg.sender] >= property;

  ```
