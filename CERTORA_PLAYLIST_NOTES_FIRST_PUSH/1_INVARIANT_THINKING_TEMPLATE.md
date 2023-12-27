# Video 8 / THINKING ABOUT PROPERTIES

## QUICK NOTES

- Always start from the end (assert ) and work backwards
  that is while specifying invariant rule first write down assert
  statement defining what you wanna check now think about all the 
  pre-conditions and dependencies

- give a read on various spec rules to get ideas (check aave spec by certora)
  and check diff kinda asserts in use
  ```solidity
  assert allowanceBefore != allowanceAfter => owner == e.msg.sender 
  //two conditions that will fails only in T F case (implication)
  ```

- also while writing invariants think about it think whether you are not
  writing tautology (i think there are tools to check specification bugs) 
  like that check certora doc, internet here and there to verify
  WORK ON YOU INVARIANTS THINKING

## VIDEO NOTES  
- Don't copy the original code, reason about specific arguments.
- compare different runs
- `valid state:`
- expressions about the systems variable that always hold
- identify groups of related variables, including variable of related contracts "underlying.balanceof(currentcontract)"
- Think about what should never ever happen
- custom => that parallel datastructure bug that owenThurm brags can be easily found using spec, tryout
- `variable transition:`
- reason about changes to the variable
- **`when can something change? which method ? who ? what change is valid? under what conditions ? what else should change?`**
- useful (=> , <=>, ) 
- **`state transition:`**
- think of the system as state machine
- define valid changes
- **`High-Level properties:`**
- reason about fundamental parts of the sytem (like: totalamounts)
- refer to external contract like `token.balanceOf(System)` and develop your
  invariants that should hold in system

- `RISK ANALYSIS:`
- Think in terms of analysing risks and threats, (swot-analysis)
- what are the most dangerous behaviours we dont want in system
- what would be devastating behaviour? think as an attacker? and write specs
- 21-26 -> liquidity pool exercise
- **`DO THE ETHCC LIQUIDITY POOL EXERCISE`**

## WHILE DEBUGGING CALL TRACE DEBUG BACKWARDS

## PRACTICE THINKING ABOUT INVARIANT ON REAL WORLD CODEBASES