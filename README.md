# Learn Security Engineering

Security engineering, to me, is the discipline of building secure systems. 
Ultimately, I hope to learn how to systematically secure anything --
whether it's a computer network or medieval castle.

This documents how I'm going about learning about security engineering. It may
not be the learning path that works best for you.

Also, this is a curated, not comprehensive, list of resources.

## Learn the fundamental tools for securing anything

### Cryptography

- ["Cryptography Engineering" book](https://www.amazon.com/Cryptography-Engineering-Principles-Practical-Applications-ebook/dp/B004NSW9JU/ref=sr_1_1?crid=WBP1JC682B4V&dchild=1&keywords=cryptography+engineering&qid=1586149852&s=books&sprefix=cryptography+eng%2Cstripbooks%2C-1&sr=1-1)
- ["Cryptography" (from Ross Anderson's book)](https://www.cl.cam.ac.uk/~rja14/Papers/SEv3-ch5-dec18.pdf)
- ["Advanced Cryptographic Engineering" (from Ross Anderson's book)](https://www.cl.cam.ac.uk/~rja14/Papers/SEv3-ch20-mar17.pdf)

To learn about later: secure enclaves 

### Economics

The idea here is to make it economically, not technically, infeasible for the attacker to attack us. He can still attack us, but his expected effort will exceed his expected gain.

Say a scammer manages to scam one of every hundred people out of $5. If we can add a $0.10 fee to every call, then he'd need to pay $10 in fees to earn $5.

- ["Economics" (from Ross Anderson's book)](https://www.cl.cam.ac.uk/~rja14/Papers/SEv3-ch8-dec18.pdf)

### Tamper resistance

- ["Physical tamper resistance" (from Ross Anderson's book)](https://www.cl.cam.ac.uk/~rja14/Papers/SEv3-ch18-dec18.pdf)

### Tamper detection

If we can't prevent tampering, we can try to make it obvious when something has been tampered with.

This one reason why bags of chips or gallons of milk, for example, are sealed.

- ["Security printing and seals" (from Ross Anderson's book)](https://www.cl.cam.ac.uk/~rja14/Papers/SEv3-ch16-dec18.pdf)

### Authentication

### Biometrics

Biometrics are a mechanism for authentication, in my view. It does this by indicating who you are. (The other two mechanisms are what you know and what you have)

- ["Biometrics" (from Ross Anderson's book)](https://www.cl.cam.ac.uk/~rja14/Papers/SEv3-ch17-dec20.pdf)


### Authorization

Without authorization, anyone who authenticates to our system would have full access to everything. We'd like to make it more difficult than that for attackers, and likely don't trust all insiders that much, either.

#### Multi-level

Think about the intel classification hierarchy: some documents are top secret, others are secret, others are confidential, and so on. This is a multi-level scheme.

#### Multi-lateral

Even if an analyst has a secret clearance, you may not want him to be able to any access documents from other departments. This is a multi-lateral scheme.

### Sandboxing

Sandboxes let us take a untrusted component of a system and apply a security policy to it.

Say you're a king, ruling over some citizens and criminals. You may want to sandbox the criminals to prevent them from harming your citizens, by, say, putting them in jail. While they can still harm each other, you've contained the damage.

- [A Theory and Tools for Applying Sandboxes Effectively](http://www.cs.cmu.edu/~mmaass/pdfs/dissertation.pdf)
- [Chrome Sandbox Design Doc](https://chromium.googlesource.com/chromium/src/+/master/docs/design/sandbox.md)
- [Chrome Sandbox Design FAQ](https://chromium.googlesource.com/chromium/src/+/master/docs/design/sandbox_faq.md)
- [gvisor](https://github.com/google/gvisor)
- [sandy](https://github.com/hobochild/sandy)

## Understand your adversaries

- ["Who is your opponent?" (from Ross Anderson's book)](https://www.cl.cam.ac.uk/~rja14/Papers/SEv3-ch2-dec18.pdf)

## Learn how some real world systems are secured

The chapters in Anderson's book fall into two categories, in my view: mechanisms for securing systems and examples of how some real world systems are secured.

We've already learned about the first category; this section is about the second category.

- ["Physical protection" (from Ross Anderson's book)](https://www.cl.cam.ac.uk/~rja14/Papers/SEv2-c11.pdf)