## FUNCTION FILTERING

## USING only f.selector
- if you wanna test if some behaviour is only happening with specific function you can use f.selector along with function signature, 
  ```c
    // we wanna test that allowances are updated through specific functions not as side effect of any other function
    rule onlyCertainMethodsChangeAllowance {
	      method f;
	      env e;
	      calldataarg args;
 	      address owner;
        address spender;
 	
	      uint allowanceBefore = allowance(owner, spender); //envFree 
        
	      f(e, args);

	      uint allowanceAfter = allowance(owner, spender); //envFree

	      assert allowanceBefore != allowanceAfter => (f.selector == approve(address, uint256).selector || f.selector == xyz), "Users Balance must not increase by any other functions"; // xyz := transferFrom, increaseAllowance, decreaseAllowance......

    }
 
  ```

- That Also means filtering methods can be done using contrapositive, i.e: f.selector != foo().selector && etc etc

## USING filtered{} along with f.selector `ALPHA_WAY`

- **For blacklisting certain functions, use `filtered Block` with `!= and &&` operators**
- - - - ```f -> f.selector != approve && xyz...``` 
- For WhiteListing certain functions, use `filtered Block` with `== and &&` operators, example 
- - ```f -> f.selector == approve && xyz...``` 
- `CAUTION` (exception in filtered block is you have to pass method f to rule definition 
- - `rule foo(method f) {}` 
- - NOT `rule foo {method f;}`) <br>
- **why use filtered instead of require? `Efficiency`**
```c
rule onlyCertainMethodsChangeAllowance(method f) {
    
        // All these functions will be blacklisted
	     filtered {
          f -> f.selector != approve(address, uint256).selector && f.selector != transferFrom(xyz).selector && xyz-xyz //increase and decrease allowance {no semicolon at end}
       }
	      env e;
	      calldataarg args;
 	      address owner;
        address spender;
 	
	      uint allowanceBefore = allowance(owner, spender); //envFree 
        
	      f(e, args);

	      uint allowanceAfter = allowance(owner, spender); //envFree

	      assert allowanceBefore != allowanceAfter, "Users Balance must not increase by any other functions";
}

```


