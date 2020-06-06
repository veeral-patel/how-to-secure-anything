# Lecture 4: Privilege Separation

From MIT 6.858

[Lecture Link](https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-858-computer-systems-security-fall-2014/video-lectures/lecture-4-privilege-separation/)

[Written lecture notes](https://people.csail.mit.edu/alinush/6.858-fall-2014/l04-okws.html)

## Privilege separation is employed in...

- [OKWS](https://pdos.csail.mit.edu/papers/okws-usenix04.pdf) - OkCupid's web server
- Google Chrome
- SSH daemon
- UNIX

## Background: protection in UNIX
- _Principals_ are entities that want access to _objects_
- In UNIX, typical principals are user IDs and group IDs (32 bit integers)
- Every process has a user ID (uid) and a list of group IDs (gid + grouplist)
- Superuser principal (root) has a uid of 0
- In what operations does UNIX enforce access control?
    - Files, directories
        - File operations: read, write, execute, change perms
        - Directory operations: lookup, create, remove, rename, change perms

... (incomplete)