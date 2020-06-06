# Notes on TCBs

From this [document](https://inst.eecs.berkeley.edu/~cs161/fa16/notes/1.27.patterns.pdf)

## Trusted vs trustworthy

- A trusted component is a part of the system that we rely on to operate correctly
- If a trusted component misbehaves, our security goals are violated
- A trustworthy component is a part of the system that we'd be justified in trusting
- `root` is trusted in Unix, and hopefully the people with access to this account are trustworthy

## What is a TCB?

- It's the portion of the system that must operate correctly in order for the security goals of the system to be assured
- But we don't rely on anything outside our TCB. Our system's security goals aren't affected if anything outside our TCB is compromised.

## Example: SSH
- Security goal: only authorized users can log into my server using SSH
- TCB includes SSH daemon. If it didn't, and the SSH daemon was compromised, then anyone could log into my server over SSH, violating the security goal
- Includes OS too. And CPU, as CPU needs to execute the SSH daemon's instructions correctly
- A web browser on the server should not be in the TCB!

## Example: Firewall
- Security goal: only authorized external connections are allowed into our internal network
- Q: what do we need to do to enforce this security goal?
- A: before any external host can make a connection to a host in our network, the connection needs to be allowed by our firewall
- So the TCB has two parts:
    - Our firewall
    - Network configuration

## TCB Design Principles
Note that these are the same principles when evaluating a control!

- Unbypassable
- Tamper-resistant
- Verifiable

Keep the TCB small and simple!