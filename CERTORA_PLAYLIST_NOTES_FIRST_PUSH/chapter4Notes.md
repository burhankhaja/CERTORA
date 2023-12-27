## TABLE OF CONTENT
- parametric rules
- method {} block
- implication and correlation
- @withRevert and lastReverted
- NONDET
- DISPATCHER(true)




## PARAMETRIC RULES

- while writing asserts , the string message should be in must and must not 
  format to make it clear what the intended behaviour is
  ex
  assert shouldAlwaysRevert, "this must always revert";
  assert noMoreMints, "contract must not mint any more";

- ok so, you do system level sverification by snapshotting states b/w and after f method call but does it try only one function during that time
  ex
  ```solidity
  balance before;
  f(e, args);
  balance after;
  assert allowance;
  ```




## METHOD BLOCK

- `method {} block` <br>
  it is best to declare view functions as envFree to save computation <br>
  like balanceOf() function, here is how you do it
  ```c
    methods {
      balanceOf(address)    returns (uint256) envfree
      allowance(address,address) returns(uint256) envfree
      // if it causes problems may be you have to also declare other env methods but without envfree at the end
    }

    //Now you can easily call them in your rule without passing e variable
    uint balanceBefore == balanceOf(e.msg.sender);
    //instead of
    uint balanceBefore == balanceOf(e, e.msg.sender);
  ```

  ## IMPLICATION AND CORRELATION
- `=> IMPLICATION` <br>
  remember implications returns false only in "T -> F" case, so it is best to use
  ```c
  rule foo(uint amount, ...) {
    ...
    ...
    ...
    assert amount > 0 => balanceAfter > balanceBefore
  }
  ```
  instead of
  ```c
  rule foo(uint amount, ...) {
    require amount > 0;
    ...
    ...
    ...
    assert balanceAfter > balanceBefore;
  }
  ```
  - `CORRELATION` <br>
  if in particular case you want to check two conditions and want to make sure if one fails or succeeds
  the otherone should also follow the suit <br>
  `use <=> double-implication`
  ```c
    rule foo {
      ....
      assert invariant1 == holds <=> invariant2 == holds, "they must behave same";
    }
  ```



========================================================================================================
<hr>


- - - - - - - - - - - - - - - - - - - - - - - 
## @withRevert and lastReverted

- create a job that checks if function reverts by any means again introduce
  bug indirectly in function by another public function without directly 
  linked to target function

  Remember (not_sure) := @withrevert gives boolean
  then assert lastReverted; is the condition for 2 cases
  if as it is it checks whether the function reverted or not, fails when
  function won't revert
  case2:=> assert !lastReverted;
  checks functions shouldn't fail, fails when function reverts
  test this behaviour (quite not sure how it will unfold)

  Remember lastReverted is a bool that catches true if function has reverted
  solidity by default doesn't consider reverts so you have to do it with using this @withrevert tag
  ```c
  rule foo {
  transfer@withrevert(foo,foo);
  assert lastReverted; //assert function always reverts
  assert !lastReverted; // assert functions never revert.
  }
  ```
- test := use parametric  rule to check system wide that no function reverts
  hint may be
  ```c
  rule foo {
    e,f,arg
    f@withrevert(e, args);
    assert !lastReverted, "no function should revert";
  }

  ```
  you can capitalize this behaviour when you don't know how specific function works by asserting that function always reverts that way certora will give you 
  control flow to successfully execute function
  ```c
   rule figureOutHowThisFunctionMayWork {
      unknownFun@withrevert(foo);
      assert lastReverted, "figuring out when this func won't revert";
   }
  ```
  
  but remember to do some precondition ju-jitsu ortherwise you gonna smesh into walls

<hr>


----------------------------------------------------------------------------------------------------

<hr>

## NONDET && DISPATCHER(true)
- More about method block `NONDET` && `DISPATCHER(true)`
- `NONDET` is used when we wanna get random number each time
  ```c
  method {
    //consider this example from kashipair that requires oracle to compute prices
    get(address token1, address token2) returns(uint256) => NONDET
  }
  ```

- `DISPATCHER(true)` generalizes context and tries to do extra lifiting, used when dealing with mulitiple contracts
  ```c
  method {
    //Assume this function transfers tokenA, while in contract context multiple tokens are used
    transfer(address recipient, uint256 amount) => DISPATCHER(true)

    // so this dispatcher thing will break the assumption of tokenA and start fuzzing with other possibilites

    //similarly the example has assigned dispacther to transferFrom() function also
    
  }
  ```
- `not sure about dispatcher still lookup to docs`







                        