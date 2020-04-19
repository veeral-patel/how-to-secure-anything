# CH20: Architecting cybersecurity

from "Engineering Trustworthy Systems" by Saydjari

## What is a reference monitor

- A reference monitor is something that checks access requests
- For example, you might have an SELinux reference monitor that checks if a process is
allowed to write to a file
- Or you might have an armed guard at the gate of a secure bunker who's checking
visitors' ID cards

## Properties of mechanisms

Reference monitors, and all security mechanisms, should have these properties:

### Functional correctness

- the mechanism should have a spec
- the spec should be correct
- the mechanism should follow the spec
- the mechanism should do no more than the spec [1]

In other words, the mechanism needs to _work_.

### Tamper proof

- an attacker should not be able to corrupt or modify the mechanism

### Bypassable

- an attacker should not be able to get around the mechanism

[1] The spec can be either informal or formal. If formal we can apply formal methods to
verify it

Whenever you're analyzing whether a system is secure, check that each of its controls meet
the three criteria above