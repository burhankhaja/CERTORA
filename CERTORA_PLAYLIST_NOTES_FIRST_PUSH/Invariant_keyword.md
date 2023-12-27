## invariants
- **`invariant` keyword** learn more about it from doc not clear what it is
  ```c
    // if a user has borrowed x, they must have deposited y as collateral
    invariant onlyCollateralCanBorrow(address user)
        userBorrowAmount(user) > 0 => userCollateralAmount(user) > 0
    // i think here best way was to prove using bi-conditional to handle win-lose on both sides
  ```
  

- if invariant keyword is easy way of rule writing then test the dummy contract function with this keyword
  see how it behaves (because i dont fully understand what it does)
- little context was given in video but no clear, 
- May be it is used like in constructor (assumption) that is assumed each time we verify any function
  still check the doc

## `requireInvariant and preserved {} block`
**for extra practical understanding, [`clickMe`](https://docs.certora.com/projects/tutorials/en/latest/lesson4_invariants/invariants/preserved.html)

- The requireInvariant statement in a preserved block is used to specify that a certain invariant must hold before a method is executed. 
- This is important because the verification process relies on the assumption that the invariant holds before the method is invoked. 
- If the invariant doesn't hold, the method might lead to unexpected states that could violate the invariant after the method is executed.
- In short, it prevents us from edge cases that aren't possible in our contracts
  
  ```c
   // These are dummy examples, they won't make much sense, lol

   // proved invariant
   invariant balanceOfZeroAddressIsZero(uint token)
        balanceOf(0, token) == 0;

   // requiring above invariants to prevent from false positives
   invariant totalSupplyIsSumOfBalances(uint token)
        sumOfBalances[token] == totalSupply(token);
        {
            preserved {
                requireInvariant balanceOfZeroAddressIsZero(token);
            }
        }
    // Requiring first invariant on rule,
    rule held_token {
        address x; uint token;
        requireInvariant balanceOfZeroAddressIsZero(token);
    }
  ```
