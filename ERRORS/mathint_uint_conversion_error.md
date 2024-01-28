## Backstory
i was trying to prove this invariant with 3 getters each returning uint256
```
invariant test()
   g1() + g2() >= g3();
```
i got `mathint uint conversion error`.
## **`Fix`**
```
invariant test()
  require_uint256(g1() + g2()) >= require_uint256(g3());
```
## Further reads
[casting](https://docs.certora.com/en/latest/docs/cvl/cvl2/changes.html#implicit-and-explicit-casting)
