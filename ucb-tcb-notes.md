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

## Benefits of TCBs?

- TCBs lets us separate a system into two parts: the part that is security-critical and everything else
- As someone looking to secure a system, this means we can ignore the parts that don't matter to us!

## Example: National Archives

- Need to save a copy of every email ever sent by government officials
- Want to ensure that an email, once sent, cannot be edited or deleted in the future

### Approach 1: store emails on a special directory on officials' laptops

- TCB: every copy of every email application on each laptop, and OSs, and sysadmins with root access to those laptps

### Approach 2: print emails

- TCB: printer, physical security of the room

### Approach 3: computer with archiving service and a read only filesystem

- TCB: computer, archiving service, OS, filesystem, privileged code, sysadmins of machine, physical security of the room this computer is in

### Remember

- Know what's in your TCB
- Make your TCB as small, simple, unbypassable, tamper-resistant, and verifiable as you can
- When designing your system, decompose it into components such that the TCB is as small as possible

## Separate + minimize privilege

(Should go under my "Separate + minimize privilege" section in my README.)

When designing a system:

- break it down into modules, based on how much privilege each module requires
- then give each module the least amount of privilege you can

## Example: web application
- Problem: we want to run a web app we've written at port 80 on a server. But binding to a port with number below 1024 requires rot