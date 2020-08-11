# Proposed Technical Evaluation Criteria for Trusted Systems

## TOC (of the paper)

- Introduction
  - Primary factors
    - Policy
    - Mechanism
    - Assurance
  - Supporting factors
- Evaluation factors
  - Level 0: no protection
  - Level 1: limited controlled sharing
  - Level 2: extensive mandatory security
  - Level 3: structured protection mechanism
  - Level 4: design correspondence
  - Level 5: implementation correspondence
  - Level 6: object code analysis
- Levels of protection
- Conclusion

Evaluation factors - Policy, Mechanism, Assurance

## Policy

- With no policy there's no way to determine if a system meets our requirements
- Protection policy written as well-defined rules regarding access--by whom, to what, under what conditions, and how (subject POV)
- Can also be written in terms of service: a protection policy prescribes the manner and conditions under which a subject is served by the system
  - Subject may be user, process, etc
  - In other words, what operations can the user do? (Eg, log in? execute a program? access a IO device?) And what are the conditions for each action?

...

## Mechanism

## Assurance

## Design

## Levels of protection

- Level 0 = no basis for confidence in system's protection ability
- Level 1 = some attempts to control access
- Level 2 = minimal requirements are satisfied, assurance comes from paying attention to protection during system design and extensive testing
- Level 3 = additional confidence gained through methodically building TCB, modern programming techniques
- Level 4 = formal methods used to verify TCB implementation
