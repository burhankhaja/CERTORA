# Inductive Reasoning 
**Effective Way to Think About Invariants**[link](https://www.youtube.com/watch?v=30BspXZs7q8)

- prove stronger claim, reason with induction
  ```c
    //instead of this
   assert x0 != B && x0 != D;

    //assert this
   assert Xm != B && Xm != D => Xm+1 != B && Xm+1 != D;

  ```
- why is overflow checked like this in certora?
  ```c
  //max_uint built in
  assert targetVar <= max_uint;
  // may be because it stores values in unlimited int which doesn't overflow on max_uint as opposed to solidity.... so then it becomes clear that adding Bigx() + OverflowPeak = max_uint like adding maxuint+1 to alreadymaxuint value:

  //((max_uint+1) + max_uint) == max_uint 
  ```
- may be using `invaraint` keyword, you have to take care that your invariant statement should be inductive
  otherwise you will get errors.   `TEST_THIS_BEHAVIOUR`-
  ---------------------------------------------------------------------------------------------
  <hr>