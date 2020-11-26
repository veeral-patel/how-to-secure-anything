# Agile Threat Modeling - Notes

(from Martin Fowler)

https://martinfowler.com/articles/agile-threat-modelling.html

- What is a threat model? No agreed standard
- Threat modeling is about understanding causes in relation to cybersecurity losses
    - Then, using that understanding to protect your system in a risk based way
    - Starting from potential threats in your particular case, rather than following a checklist blindly
- Problem: unlimited number of possible threats; many of them could be likely
    - Also, causality can be complicated. For instance, Mersk had to stop shipping and Cadbury's had to stop making chocolate due to NotPetya
- Also - threat model little and often

## Start from technical threats, not broad threats

- Broad threats include hacker groups, insiders, human error, etc
    - Very broad, uncertain, unpredictable, varied
- Technical threats include missing encryption or authz

## Three key questions

- Explain and explore: What are you building? Technical diagram
- What can go wrong? A list of technical threats
- What are you going to do? Prioritized fixes added to the backlog

## Explain and explore

### Draw a lo-fi technical diagram

- Don't pull an outdated diagram off the wiki
- Draw out what the system looks like now

1. Show relevant components

2. Show users on diagram

- Some users can be more trusted than others
- "Not all systems are user facing. If your system is  let's say a downstream microservice which only accepts requests from other systems then represent collaborating systems that are authorised to interact with the system"

(incomplete)