# CH5: Approximating Reality

from "Engineering Trustworthy Systems"

## States and the need for models

- If you think about it, a program has as many states as it has memory arrangements
- But we can't reason about so many states, so we need to create models
- Remember that all models are wrong. After all, models don't represent reality in perfect detail (this is what makes them useful!)

## The adversary's point of view

- An adversary needs only one attack to succeed
- An adversary also has the element of surprise. They know when/how they are going to attack the target system. The defender doesn't know this.
- An adversary can attack the beliefs of the defender. It can impersonate someone and then attack the defender, causing the defender to retaliate against the wrng person

## Dependability

- A fault is the cause of an error (eg, a bug in a program)
- An error is what happens when the fault occurs
- The error, if not handled, can cause a failure of some kind