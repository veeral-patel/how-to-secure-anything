# Thirty Years Later: Lessons from the Multics Security Evaluation

- 30 years later, most OSs still don't include the security mechanisms that Multics introduced
- Security was an original primary goal in Multics
- Security was built into Multics and shipped to all users, not just those users who requested them
  - This meant application developers made sure their applications worked with these controls
- Multics didn't suffer from buffer overflows, because of the choice of implementation language and use of several hardware features
- Multics was small! 628K bytes of executable code for Multics (the whole OS) vs 1767K bytes for SELinux
- "Security has gotten worse, not better"

> It is unthinkable that another thirty years will go by without one of two occurrences: either there will be horrific cyber disasters that will deprive society of much of the value computers can provide, or the available technology will be delivered, and hopefully enhanced, in products that provide effective security. We hope it will be the latter.
