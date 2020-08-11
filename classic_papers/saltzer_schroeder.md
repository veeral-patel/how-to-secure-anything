# The protection of information in computer systems

> My notes on this paper are not complete.

About the architectural structures needed to support info protection

Section I - desired functions, design principles, examples of elementary protection, auth mechanisms

Section II - capabilities vs ACLs, protected subsystems + objects

Section III - reviews state of the art, current research projects, future projects

Basic principles of info protection

Defines security as techniques to control who may use/modify the computer or info in it

Anderson divides security violations into:

- Unauthorized info release (confidentiality)
- Unauthorized info modification (integrity)
- Unauthorized denial of use (availability)

Divide protection schemes into:

- unprotected systems (no auth)
- all or nothing systems - user can access everything or nothing (auth, all or nothing authz)
- controlled sharing (auth + authz to access info)
  - who may access each data item in the system
  - eg, user wants to only let a user be viewed on weekdays between 9am and 4pm, and edited only if two users agree
  - user-defined protected objects
  - protected subsystems - collection of programs and data such that only the programs in the subsystem may have direct access to the data (protected objects)
  - access to these programs is limited to specified entry points
  - these programs are really just reference monitors!
  - then, you allow users to create their own reference monitors (aka programs)
- user programmed sharing controls
- putting strings on information - maintain control over user of info even after it’s been released (auth + authz + restrictions after authz)
  - tax advisors shouldn’t be able to pass your info onto unwanted people
  - can’t share top secret material (it’s labeled Top Secret)

Dynamics of use

- how one establishes, changes spec of who may access what
- a system may statically enforce a security policy
- but who can change that security policy?

example - “can John access file X?”

- does John have access to file X?
- can he change the spec of X’s accessibility? (eg, by increasing his security clearance)
- can John change the security clearance process, to get a higher security clearance, to increase his access?

another problem - owner revokes access to file while it’s being used

- letting now unauthorized user keep accessing file may not be accessible
- but immediate withdrawal of authorization may disrupt the user

computer-aided enforcement may not be enough!

- can use contracts, barbed wire fence for example

> Since no one knows how to build a system without flaws, the alternative is to rely on eight design principles, which tend to reduce both the number and the seriousness of any flaws: Economy of mechanism, fail-safe defaults, complete mediation, open design, separation of privilege, least privilege, least common mechanism, and psychological acceptability.

TECHNICAL UNDERPINNINGS

Development plan

- can do this:
  - top down - emphasize the abstract concepts involved
  - bottom up - identify insights by studying example systems

Authentication mechanisms

- basic setup - user has a password
- can be modified
  - user carries a list of one time passwords
  - passwords may have an expiration time or a usage count
- concern: users often choose weak passwords
- concern: passwords can be wiretapped

alternative approach - unforgettability

- user given a key or magnetically striped plastic card or something else that’s hard to fabricate
- terminal has an input that transmit the key’s unique code (which doesn’t need to be secret) to the computer
  - basically a yubikey!
- fingerprints, dynamic signature readers also reduce forgeability

Shared information

key question - how to authorize users?

- list-oriented implementations
  - guard holds list of identifiers of authorized users
  - user carries unique unforgeable identifier which must appear on guard’s list
  - store clerk checking list of credit customers is also an ACL; user may use driver’s license as identifier
  - authorize user by putting him on a list
- ticket oriented implementations
  - lots of locked doors. each room has an object.
  - user has a collection of unforgeable identifiers, or keys
  - one key per object he’s been authorized access to
  - authorize user by giving him a key / ticket

list oriented - centralized, ticket oriented - decentralized

list oriented - system searches list of users, ticket oriented - user searches list of tickets

Protected objects and domains

We want a course grade system where:

- students can read their grades
- but not other students’ grades
- any student can view histogram of class grades
- assistant can enter new grades but can’t change a grade later without an instructor’s approval

Current research directions (in 1975)

- certification of correctness of protection system designs and implementations
- invulnerability to single faults
- constraints on use of information after release
- encipherment of information with secret keys
- improved authentication mechanisms
