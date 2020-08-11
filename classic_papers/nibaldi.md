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

- security features that enforce our protection policy
- keep in mind that TCB includes both hardware, software
- four categories: prevention, detection, recovery, support ops/maintenance

### Prevention

Few important areas

- data protection - protect info + flow, authz policies
- system integrity - protection from tampering, protect users from each other
- denial of service mechanisms
- authentication
- confinement

### Detection

- Auditing - capture all the important actions, tie them to users
- Surveillance - monitor your logs!

Remember, detection mechanisms need to be protected too!

### Recovery

- Restore the secure state of the system in case of a fault
  - Fault may be induced by software (malicious program) or hardware (failed component)
- Not always possible
  - Example: unauthorized user viewed file
- In the security industry we have response tools, but not automated recovery tools

## Assurance

- good news: with TCB approach you only need to assure the TCB, nothing else!
- design top down: high level design specs, lower level design specs
- programming techniques: modularity, abstract typing, structured programming

...

## 7 Levels of protection

- Level 0 = no basis for confidence in system's protection ability
- Level 1 = some attempts to control access
- Level 2 = minimal requirements are satisfied, assurance comes from paying attention to protection during system design and extensive testing
- Level 3 = additional confidence gained through methodically building TCB, modern programming techniques
- Level 4 = formal methods used to verify design of TCB implementation
- Level 5 = formal methods employed to verify software implementation of the design
- Level 6 = object code analyzed, hardware support strengthened

...
