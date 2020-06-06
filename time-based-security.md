# Notes on "Time Based Security"

A book by Winn Schwartau

## Disclaimer

This book introduces an interesting idea but it uses 200 pages to describe an idea that could be described in one blog post. You may be disappointed by it.

## CH5: A brief history of security models

- The "Orange Book" introduces the reference monitor, or something that either accepts or denies every access request
- On a computer, an example may be a process requesting a file descriptor or network socket
- This kind of mandatory access control made sense for the military but not for the private sector
- Schwartau calls this an example of a Fortress Mentality, or "prevent everything"

## CH8: Fast forward one century

- Vaults are not 100% secure. They can be broken into
- The purpose of a vault is not to secure something on its own
- It's to prevent the robbers from stealing what's inside before the police come

## CH9: The PDR security formula

- Pt > Dt + Rt
- The amount of time offered by the prevention controls must exceed the amount of time it takes to detect and respond to the attack