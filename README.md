# Learn Security Engineering

Security engineering, to me, is the discipline of building secure systems.
Ultimately, I hope to learn how to systematically secure anything --
whether it's a computer network or medieval castle.

I tried for several years to read [Ross Anderson's book](https://www.cl.cam.ac.uk/~rja14/book.html), and eventually I realized it wasn't structured correctly for me. This learning path is, and hopefully it is for you, too.

## Learn the theory

- ["What is security engineering?" (from Anderson's book)](https://github.com/veeral-patel/learn-security-engineering)

## Fundamental tools for securing anything

In order to secure something, you need to know what tools are available to you. Here are some that which can be used in many different contexts.

A lot of tools are context-specific, however. Before I start trying to secure a building, for example, I'd spend the time to learn about all the tools I can use: walls, sensors, natural barriers, guards, CCTV cameras, etc

### Cryptography

- ["Cryptography Engineering" book](https://www.amazon.com/Cryptography-Engineering-Principles-Practical-Applications-ebook/dp/B004NSW9JU/ref=sr_1_1?crid=WBP1JC682B4V&dchild=1&keywords=cryptography+engineering&qid=1586149852&s=books&sprefix=cryptography+eng%2Cstripbooks%2C-1&sr=1-1)
- ["Cryptography" (from Ross Anderson's book)](https://www.cl.cam.ac.uk/~rja14/Papers/SEv3-ch5-dec18.pdf)
- ["Advanced Cryptographic Engineering" (from Ross Anderson's book)](https://www.cl.cam.ac.uk/~rja14/Papers/SEv3-ch20-mar17.pdf)

To learn about later: secure enclaves

### Economics

The idea here is to make it economically, not technically, infeasible for the attacker to attack us. He can still attack us, but his expected effort will exceed his expected gain.

Say a scammer manages to scam one of every hundred people out of $5. If we can add a $0.10 fee to every call, then he'd need to pay $10 in fees to earn $5.

Another example would be not storing credit card data ourselves, and instead outsourcing this to a payment processor, so the reward of attacking us is less.

If the attacker isn't motivated by money, this doesn't work.

- ["Economics" (from Anderson's book)](https://www.cl.cam.ac.uk/~rja14/Papers/SEv3-ch8-dec18.pdf)
- [Security Economics](https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-858-computer-systems-security-fall-2014/video-lectures/lecture-23-security-economics/) - here's the [transcript](https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-858-computer-systems-security-fall-2014/video-lectures/lecture-23-security-economics/8PdnOZI7H5E.pdf)

### Laws and regulations (deterrence by the government)

Deterrence has three parts: certainty, severity, and swiftness. In other words, to deter attackers most effectively, someone should be able to catch most
or all of them -- and do this quickly -- and then sufficiently punish them once you do catch them.

This someone could be the government, via laws and regulations against whatever you're trying to defend against. The government may not catch everyone,
but these laws and regulations will deter most people. Copyright protection, anti-shoplifting, and anti-trespassing laws all are examples of this.

### Retaliation (deterrence by you or third parties)

The government is not the only third party who can deter attacks on you. Organizations, like NATO, can as well.

Alternatively, you can try to retaliate against attacks yourself. Take, for example, media companies that sue people that pirate their movies.

### Tamper resistance

- ["Physical tamper resistance" (from Anderson's book)](https://www.cl.cam.ac.uk/~rja14/Papers/SEv3-ch18-dec18.pdf)

### Tamper detection

If we can't prevent tampering, we can try to make it obvious when something has been tampered with.

This one reason why bags of chips or gallons of milk, for example, are sealed.

- ["Security printing and seals" (from Anderson's book)](https://www.cl.cam.ac.uk/~rja14/Papers/SEv3-ch16-dec18.pdf)

### Access control

- ["Access Control" (from Anderson's book)](https://www.cl.cam.ac.uk/~rja14/Papers/SEv2-c04.pdf)
- [OS Security Concepts (from CS 161 from UC Berkeley)](https://inst.eecs.berkeley.edu/~cs161/fa16/slides/lec4.pdf)

### Biometrics

Biometrics are a mechanism for authentication, in my view. It does this by indicating who you are. (The other two mechanisms are what you know and what you have)

- ["Biometrics" (from Anderson's book)](https://www.cl.cam.ac.uk/~rja14/Papers/SEv3-ch17-dec20.pdf)

### Authorization

Without authorization, anyone who authenticates to our system would have full access to everything. We'd like to make it more difficult than that for attackers, and likely don't trust all insiders that much, either.

#### Multi-level

Think about the intel classification hierarchy: some documents are top secret, others are secret, others are confidential, and so on. This is a multi-level scheme.

- ["Multilevel Security" (from Anderson's book)](https://www.cl.cam.ac.uk/~rja14/Papers/SEv2-c08.pdf)

#### Multi-lateral

Even if an analyst has a secret clearance, you may not want him to be able to any access documents from other departments. This is a multi-lateral scheme.

- ["Boundaries" (from Anderson's book)](https://www.cl.cam.ac.uk/~rja14/Papers/SEv3-ch10-dec18.pdf)
- ["Inference Control" (from Anderson's book)](https://www.cl.cam.ac.uk/~rja14/Papers/SEv3-ch10-dec18.pdf)

### Sandboxing

Sandboxes let us take a untrusted component of a system and apply a security policy to it.

Say you're a king, ruling over some citizens and criminals. You may want to sandbox the criminals to prevent them from harming your citizens, by, say, putting them in jail. While they can still harm each other, you've contained the damage.

- [On Safes, Sandboxes, and Spies (CS 161 at UC Berkeley)](https://inst.eecs.berkeley.edu/~cs161/fa16/slides/lec5.pdf)
- [A Theory and Tools for Applying Sandboxes Effectively](http://www.cs.cmu.edu/~mmaass/pdfs/dissertation.pdf)
- [Chrome Sandbox Design Doc](https://chromium.googlesource.com/chromium/src/+/master/docs/design/sandbox.md)
- [Chrome Sandbox Design FAQ](https://chromium.googlesource.com/chromium/src/+/master/docs/design/sandbox_faq.md)
- [gvisor](https://github.com/google/gvisor)
- [sandy](https://github.com/hobochild/sandy)

### Protocols

Protocols aren't a tool for securing something. But all communication between two components of a system is done through
a protocol, so it's worth learning how to analyze protocols for vulnerabilities.

- ["Protocols" (from Anderson's book)](https://www.cl.cam.ac.uk/~rja14/Papers/SEv3-ch4-dec18.pdf)
- [Secure Transaction Protocol Analysis](https://www.amazon.com/Secure-Transaction-Protocol-Analysis-Applications/dp/3540850732)

## Learn how some real world systems are secured

The chapters in Anderson's book fall into two categories, in my view: mechanisms for securing systems and examples of how some real world systems are secured.

We've already learned about the first category; this section is about the second category.

#### Read actively!

It's a lot more educational (and fun!) to try to figure out how you'd secure a system yourself than it is to just look at the answer and move on.

(You can't do this for systems you don't understand, of course, like nuclear power plants.)

As you read, try answering these questions:

- Who are our adversaries? What are their motives, capabilities, and TTPs?
- Draw out attack trees for possible attacks against us. Are we secure against the weakest link?
- Draw kill chains to map the attacks our adversaries use. Then, think of ways to disrupt each step in the kill chain
- What defenses can I put in place for prevention? Detection? Response?
- See if you can apply any of the basic security design principles (least privilege, defense in depth, privilege separation, etc)
- See if you can use any of the mechanisms from the section above
- After you learn how the system is secured in real life, ask: did you derive any controls that exist? If you came up with controls that don't exist, why don't they exist today? What controls did you miss and why?

### Physical protection

- ["Physical protection" (from Anderson's book)](https://www.cl.cam.ac.uk/~rja14/Papers/SEv2-c11.pdf)

### Nuclear command and control

- ["Nuclear command and control" (from Anderson's book)](https://www.cl.cam.ac.uk/~rja14/Papers/SEv3-ch15-dec18.pdf)
- [Nuclear Security Recommendations on Physical Protection of Nuclear Material and Nuclear Facilities](https://www-pub.iaea.org/MTCD/Publications/PDF/Pub1481_web.pdf)
- [Nuclear Security Series](https://www.iaea.org/publications/search/type/nuclear-security-series)

### Monitoring and metering

- ["Monitoring and metering" (from Anderson's book)](https://www.cl.cam.ac.uk/~rja14/Papers/SEv2-c12.pdf)

### Banking and bookkeeping

- ["Banking and bookkeeping" (from Anderson's book)](https://www.cl.cam.ac.uk/~rja14/Papers/SEv2-c10.pdf)

### Distributed systems

- ["Distributed systems" (from Anderson's book)](https://www.cl.cam.ac.uk/~rja14/Papers/SEv3-ch7-dec18.pdf)

### Copyright and DRM

- ["Copyright and DRM" (from Anderson's book)](https://www.cl.cam.ac.uk/~rja14/Papers/SEv2-c22.pdf)

### Chromium

- [Security Architecture of the Chromium Browser](http://seclab.stanford.edu/websec/chromium/chromium-security-architecture.pdf)

### Apple

- [Apple Platform Security](https://manuals.info.apple.com/MANUALS/1000/MA1902/en_US/apple-platform-security-guide.pdf)

### Elections

Find resources!

## Understand your adversaries

There's no such thing as a system being secure, only being secure against a particular adversary.

- ["Who is your opponent?" (from Anderson's book)](https://www.cl.cam.ac.uk/~rja14/Papers/SEv3-ch2-dec18.pdf)

## Assurance

- [The Orange Book](https://csrc.nist.gov/csrc/media/publications/conference-paper/1998/10/08/proceedings-of-the-21st-nissc-1998/documents/early-cs-papers/dod85.pdf)

## Side channels

Even if something isn't vulnerable to attacks (on confidentiality, integrity, or
availability), it may leak information which makes these attacks easier.

For example, take a login program that checks if the username is valid, returns
a generic "login failed" error if it's not, then checks if the password is valid,
and returns the same generic error if it's not.

At a first glance, determining if a particular username is valid may seem
impossible. After all, the error message is the same regardless of whether the
username is invalid or the username is valid and the password is invalid.

However, an attacker could examine the time it takes to get the error to
determine if the username is valid or not.

- ["Side channels" (from Anderson's book)](https://www.cl.cam.ac.uk/~rja14/Papers/SEv3-ch19-dec18.pdf)

## Trusted computing base

- [OS Security Concepts (from CS 161 from UC Berkeley)](https://inst.eecs.berkeley.edu/~cs161/fa16/slides/lec4.pdf)
