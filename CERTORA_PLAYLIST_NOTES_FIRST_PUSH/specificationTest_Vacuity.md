# `video 10: Vacuity`
**Learn to craft rules that define alternate states not a one that defines two sides of same coin**[`link`](https://www.youtube.com/watch?v=csTe6ub3Jwg&list=PLKtu7wuOMP9XHbjAevkw2nL29YMubqEFj&index=12)

## `vacous rule/property`
- `A Property/Rule That lacks contents which could or should be present`

## Some Logical Definitions
- **FALSE STATEMENT:**
- The existence of counter example to the claim

## characteristics
- unreachability
- tautology

## Method Unreachability detection [ALPHA]
**`Run this rule to check if any methods in contract are unreachable from all the possible variable combinations`**
```c
rule MethodVacuityCheck(method f) {
    env e;
    calldataarg args;

    f(e,args);
    // if a function fails to fail that means it has reachability issue
    // in other words all the passing functions are unreachable
    assert false, "this method should have non reverting path";
}

```

**Better to run it before running the invariant verification rules**


## Best__Easiest__way__to__check__allkinda__vacuity
**use `--rule_sanity:`**
- basic
- advanced

**Run certora prover first, if all properties seem to satisfy run sanity checks to check if anything has been missed (custom_advice)**




  
