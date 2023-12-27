# Optimistic Loop

## doc

- **`In optimistic mode (enabled by passing the --optimistic_loop option), the Prover ignores any examples that would cause the loop to execute too many times. In optimistic mode, the rule bogus_rule above would be reported as passing.`**

- **CAUTION** 

- `Optimistic mode is unsound since it may miss counterexamples like these. It should be used with care since it may hide bugs.`


- Despite the unsoundness, optimistic mode is quite useful in practice. For example, it allows us to document that slow_copy satisfies the specification given in its documentation:

```c
rule slow_copy_correct(uint n) {
    assert slow_copy(n) == n, "slow_copy(n) always returns n";
}
```

- In optimistic mode, this rule will pass (as it should), but in pessimistic mode it will fail if n > 2.
- [`Link_2_DOC`](https://docs.certora.com/en/latest/docs/prover/approx/loops.html)
- [`ALPHA_LINK_2_DOC`](https://docs.certora.com/en/latest/docs/prover/cli/options.html#optimistic-loop)

## random
When running the spec ERC20.spec you must add "optimistic_loop": "true" to your config file, or use --optimistic_loop flag if running from command line. 
Otherwise, you will get a violation whenever the Prover encounters the getters name() and symbol(). 

The violation occurs because the Prover uses loops to handle strings, or any dynamic array. 

Loops require special care and handling which we will address in a later lesson. For now, `simply use this flag whenever you have a string.`
