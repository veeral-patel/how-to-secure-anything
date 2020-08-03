# Learn Security Engineering

Security engineering, to me, is the discipline of building secure systems.
Ultimately, I hope to learn how to systematically secure anything --
whether it's a computer network or medieval castle.

I tried for several years to read [Ross Anderson's book](https://www.cl.cam.ac.uk/~rja14/book.html), and eventually I realized it wasn't structured correctly for me. This learning path is, and hopefully it is for you, too.

## What is security engineering?

Security engineering isn't about adding a bunch of controls to something.

It's about coming up with security properties you'd like a system to have, choosing
mechanisms that enforce these properties, and assuring yourself that your security properties hold.

- ["What is security engineering?" (from Anderson's book)](https://www.cl.cam.ac.uk/~rja14/Papers/SEv3-ch1-dec18.pdf) - [my notes](anderson/anderson-ch1.md)
- [What's the problem? (from Saydjari's book)](https://www.oreilly.com/library/view/engineering-trustworthy-systems/9781260118186/ch1.xhtml) - [my notes](saydjari/saydjari-ch1.md)
- [Computer security in the real world](what_is_it/computer_security_in_the_real_world.pdf)

## Security policies & models

Policies are the high level properties we want our system to have. Policies are what we want to happen.

If we're designing a prison, one of our policies might be:

> No prisoner may escape the prison.

We can then turn our policy into a more detailed model. A model is a set of rules, a specification, to achieve our policy.

> Each individual in the prison facility must have a ID that identifies him/her as a "prisoner" or "not a prisoner"

> A prisoner may have the written consent of the warden to leave.

> A non-prisoner may leave at any time.

- [Computer Security: Art and Science](https://www.amazon.com/Computer-Security-Art-Science-Set/dp/013428951X) covers this topic very well
- [Flask security architecture](https://www.cs.cmu.edu/~dga/papers/flask-usenixsec99.pdf)

Luckily, in information security, our policies often revolve around confidentiality, integrity, and availability and so there are popular existing security models for each of these policies.

For confidentiality, for example, you can choose between:

- [multilevel security](#multilevel), for which [Bell-Padula](https://en.wikipedia.org/wiki/Bell%E2%80%93LaPadula_model) can be used
- [multilateral security](#multilateral), for which compartmentation, BMA, [Chinese wall](https://people.csail.mit.edu/alinush/6.858-fall-2014/papers/chinese-wall-sec-pol.pdf) can be used (according to Anderson's book)

## Understand your adversaries

There's no such thing as a system being secure, only being secure against a particular adversary.

This is why it's important to understand who your adversaries are, as well as the motivation behind
and capabilities of each adversary.

Consider non-human threats, too. If you're asked to secure a painting in a museum, a fire may technically not be a security issue -- but it's something to guard against, regardless.

- ["Who is your opponent?" (from Anderson's book)](https://www.cl.cam.ac.uk/~rja14/Papers/SEv3-ch2-dec18.pdf)
- [Threat Modeling: Designing for Security](https://www.amazon.com/Threat-Modeling-Designing-Adam-Shostack/dp/1118809998)

## Design techniques

I think you can make a system fairly secure just by trying to design in security from
the beginning. Here are some techniques for doing this.

### Minimize attack surface

See tptacek's [HN comment on this](https://news.ycombinator.com/item?id=17014818):

> For instance: you can set up fail2ban, sure. But what's it doing for you? If you have password SSH authentication enabled anywhere, you're already playing to lose, and logging and reactive blocking isn't really going to help you. Don't scan your logs for this problem; scan your configurations and make sure the brute-force attack simply can't work.

> The same goes for most of the stuff shrink-wrap tools look for in web logs. OSSEC isn't bad, but the things you're going to light up on with OSSEC out of the box all mean something went so wrong that you got owned up.

> Same with URL regexes. You can set up log detection for people hitting your admin interfaces. But then you have to ask: why is your admin interface available on routable IPs to begin with?

- [OWASP Attack Surface Analysis Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Attack_Surface_Analysis_Cheat_Sheet.html)
- See the papers in [this folder](attack_surface)

### Minimize, simplify, verify your trusted computing base (TCB)

When evaluating a design, it's useful to see how much of the system must be trusted in order for a security goal
to be achieved. The smaller this trusted computing base is, the better.

Also, once you identify the TCB for an existing system, you know that you only need to secure your TCB. You don't
need to worry about securing components outside your TCB.

You want to make your TCB as small, simple, unbypassable, tamper-resistant, and verifiable as you can, as I
write about [here](https://github.com/veeral-patel/learn-security-engineering/blob/master/ucb-tcb-notes.md#remember).

- [OS Security Concepts (from CS 161 from UC Berkeley)](https://inst.eecs.berkeley.edu/~cs161/fa16/slides/lec4.pdf)
- [Design patterns for building secure systems](https://inst.eecs.berkeley.edu/~cs161/fa16/notes/1.27.patterns.pdf) - [my notes](ucb-tcb-notes.md)
- [TSAFE: Building a Trusted Computing Base forAir Traffic Control Software](tcbs/tsafe.pdf)
- [Ten page intro to trusted computing](tcbs/ten_page_intro_to_trusted_computing.pdf)

### Separate and minimize privilege; sandbox if possible

When designing a system, a great way to mitigate the impact of a successful attack is to break the system
down into components based upon their privilege level.

Then, ask what's the least amount of privilege each component needs -- and then enforce the allowed privileges
with a [sandbox](https://github.com/veeral-patel/learn-security-engineering#sandboxing) (if applicable).

Say one of our SRE SSH's into a production EC2 instance as `root` to check the instance's memory and CPU usage.
Instead, we can assign the SRE a non-root account. Even better, we can whitelist the commands this account can run.
Even better, we can even remove SSH access entirely and set up [Prometheus](https://prometheus.io/) for monitoring.

- [Lecture 4: Privilege Separation (6.858 from MIT)](https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-858-computer-systems-security-fall-2014/video-lectures/lecture-4-privilege-separation/) - [my notes](mit-6858-lec-4-privilege-separation.md)
- [OKWS paper](https://pdos.csail.mit.edu/papers/okws-usenix04.pdf)
- [SSH daemon (from Niels Provos)](http://www.citi.umich.edu/u/provos/ssh/privsep.html)
- [Security architecture of the Chromium browser](http://seclab.stanford.edu/websec/chromium/chromium-security-architecture.pdf)
- [Make least privilege a right (not a privilege)](https://www.scs.stanford.edu/~dm/home/papers/krohn:least-privilege.pdf)

### Security design principles

- [Stop buying bad security prescriptions](https://medium.com/@justin.schuh/stop-buying-bad-security-prescriptions-f18e4f61ba9e)
- [Design principles (from US CERT)](https://www.us-cert.gov/bsi/articles/knowledge/principles/design-principles)

## Analysis techniques

Once you've come up with an initial design, the techniques below help you find
additional controls you can add and vulnerabilities you need to resolve.

### Prevent/detect/respond framework

The way I see it, every defense falls into one of these categories:

- Prevent: consists of deter, stop
- Detect
- Respond: consists of delay, contain, investigate, remediate

Take any attack. Then, for each of the seven categories, brainstorm defenses that fall into that category.

### Attack trees

After building an attack tree, you can query it easily: "list all the attack paths costing
less than \$100k". (Remember: we don't seek absolute security, but rather security against
a certain set of adversaries.)

Also, remember the [weakest link principle](https://www.us-cert.gov/bsi/articles/knowledge/principles/securing-the-weakest-link). You can query your attack tree for the lowest cost attack
path and ensure that the cost isn't too low.

- [Attack trees (from Bruce Schneier)](https://www.schneier.com/academic/archives/1999/12/attack_trees.html)

### Kill chains

By mapping out an adversary's kill chain, we can then identify controls to counteract
each step in the kill chain. Check out [MITRE ATT&CK](https://attack.mitre.org/).

- [Kill chains (Wikipedia)](https://en.wikipedia.org/wiki/Kill_chain)

### Control analysis

Every security control must be impossible to bypass, tamperproof, and functionally correct. It must
also fail closed.

If this is not the case, then an attacker can violate a system's security properties by subverting its
controls.

Saydjari writes an entire chapter on this:

- [Architecting cybersecurity (from Saydjari's book)](https://learning.oreilly.com/library/view/engineering-trustworthy-systems/9781260118186/ch20.xhtml) - [my notes](saydjari/saydjari-ch20.md)

### Protocol analysis

Protocols aren't a tool for securing something. But all communication between two components of a system is done through
a protocol, so it's worth learning how to analyze protocols for vulnerabilities.

- ["Protocols" (from Anderson's book)](https://www.cl.cam.ac.uk/~rja14/Papers/SEv3-ch4-dec18.pdf)
- [A logic of authentication](protocols/a_logic_of_authentication.pdf)
- [Programming Satan's computer](protocols/programming_satans_computer.pdf)
- [Prudent engineering practice for cryptographic protocols](protocols/prudent_engineering_practice_for_cryptographic_protocols.pdf)
- [Robustness principles for public key protocols](protocols/robustness_principles_for_public_key_protocols.pdf)
- [Using Encryption for Authentication in Large Networks of Computers](protocols/using_encryption_for_authentication_in_large_networks_of_computers.pdf)
- [Three systems for cryptographic protocol analysis](protocols/three_systems_for_cryptographic_protocol_analysis.pdf)

### Failure analysis

We want our security controls to fail closed, not open. There's two ways to analyze the ways something
might fail: failure tree analysis (FTA), which is top down, and failure modes and effects analysis (FMEA),
which is bottom up.

- [How to avoid failures](https://www.dsiintl.com/wp-content/uploads/2017/04/HOW-TO-AVOID-FAILURES-FMEA-andor-FTA.pdf)
- [FMEA (from ASQ)](https://asq.org/quality-resources/fmea)
- [There's several FMEA books](https://www.google.com/search?q=fmea+books)

### Side channel identification

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

## Popular mechanisms

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

- [Deterrence and adversarial risk (from Saydjari's book)](https://learning.oreilly.com/library/view/Engineering+Trustworthy+Systems:+Get+Cybersecurity+Design+Right+the+First+Time/9781260118186/ch16.xhtml#ch16lev1) - [my notes](saydjari/saydjari-ch16.md)

### Tamper resistance

- ["Physical tamper resistance" (from Anderson's book)](https://www.cl.cam.ac.uk/~rja14/Papers/SEv3-ch18-dec18.pdf)
- [Cryptographic processors – a survey](https://www.cl.cam.ac.uk/techreports/UCAM-CL-TR-641.pdf)
- [Smartcard Handbook](https://www.amazon.com/Smart-Card-Handbook-Wolfgang-Rankl/dp/0470743670)
- [Tamper Resistance - a Cautionary Note](https://www.cl.cam.ac.uk/~rja14/tamper.html)
- [Low Cost Attacks on Tamper Resistant Devices](http://web.cse.msstate.edu/~ramkumar/tamper2.pdf)
- [Design Principles for Tamper-Resistant Smartcard Processors](https://www.cl.cam.ac.uk/~mgk25/sc99-tamper.pdf)

### Tamper detection

If we can't prevent tampering, we can try to make it obvious when something has been tampered with.

This is one reason why bags of chips or gallons of milk, for example, are sealed.

- [Optimal Document Security](https://www.amazon.com/Optical-Document-Security-Rudolf-Renesse/dp/1580532586/)
- ["Security printing and seals" (from Anderson's book)](https://www.cl.cam.ac.uk/~rja14/Papers/SEv3-ch16-dec18.pdf)

### Access control

- ["Access Control" (from Anderson's book)](https://www.cl.cam.ac.uk/~rja14/Papers/SEv2-c04.pdf)
- [OS Security Concepts (from CS 161 from UC Berkeley)](https://inst.eecs.berkeley.edu/~cs161/fa16/slides/lec4.pdf)

### Biometrics

Biometrics are a mechanism for authentication, in my view. It does this by indicating who you are. (The other two mechanisms are what you know and what you have)

- ["Biometrics" (from Anderson's book)](https://www.cl.cam.ac.uk/~rja14/Papers/SEv3-ch17-dec20.pdf)

### Authorization

Without authorization, anyone who authenticates to our system would have full access to everything. We'd like to make it more difficult than that for attackers, and likely don't trust all insiders that much, either.

#### Multilevel

Think about the intel classification hierarchy: some documents are top secret, others are secret, others are confidential, and so on. This is a multi-level scheme.

- ["Multilevel Security" (from Anderson's book)](https://www.cl.cam.ac.uk/~rja14/Papers/SEv2-c08.pdf)
- [An analysis of the systemic security weaknesses of the U.S. Navy fleet broadcasting system, 1967-1974, as exploited by CWO John Walker](multilevel/walker_spy_ring.pdf)

#### Multilateral

Even if an analyst has a secret clearance, you may not want him to be able to any access documents from other departments. This is a multi-lateral scheme.

- ["Boundaries" (from Anderson's book)](https://www.cl.cam.ac.uk/~rja14/Papers/SEv3-ch10-dec18.pdf)
- [Security in clinical information systems](multilateral/security_in_clinical_info_systems.pdf)
- [Implementing access control to protect the confidentiality of patient information in clinical information systems in the acute hospital](multilateral/implementing_access_control_to_protect_patient_data.pdf)
- [Privacy in clinical information systems in secondary care](multilateral/privacy_in_clinical_info_systems.pdf)

### Inference control

- ["Inference Control" (from Anderson's book)](https://www.cl.cam.ac.uk/~rja14/Papers/SEv3-ch10-dec18.pdf)
- [Report on Statistical Disclosure Limitation Methodology](https://ecommons.cornell.edu/bitstream/handle/1813/22991/WP-22-OMB-totalreport.pdf)

### Sandboxing

Sandboxes let us take a untrusted component of a system and apply a security policy to it.

Say you're a king, ruling over some citizens and criminals. You may want to sandbox the criminals to prevent them from harming your citizens, by, say, putting them in jail. While they can still harm each other, you've contained the damage.

- [On Safes, Sandboxes, and Spies (CS 161 at UC Berkeley)](https://inst.eecs.berkeley.edu/~cs161/fa16/slides/lec5.pdf)
- [A Theory and Tools for Applying Sandboxes Effectively](http://www.cs.cmu.edu/~mmaass/pdfs/dissertation.pdf)
- [Chrome Sandbox Design Doc](https://chromium.googlesource.com/chromium/src/+/master/docs/design/sandbox.md)
- [Chrome Sandbox Design FAQ](https://chromium.googlesource.com/chromium/src/+/master/docs/design/sandbox_faq.md)
- [Sandboxing Applications](sandboxing/sandboxing_applications.pdf)
- [A Security Study of Chrome’s Process-based Sandboxing](sandboxing/ChromeDOP.pdf)
- [SELinux, Seccomp, Sysdig Falco, and you: A technical discussion](https://sysdig.com/blog/selinux-seccomp-falco-technical-discussion/)
- [gvisor](https://github.com/google/gvisor)
- [sandy](https://github.com/hobochild/sandy)

### Obscurity

Obscurity, not its own, does not count as security. However, it can be added on top of real security measures, to make attacks on you
require more time and a higher skill level.

- [Obscurity is a valid security layer](https://danielmiessler.com/study/security-by-obscurity/) - see the [HN comments](https://news.ycombinator.com/item?id=15541792) as well

## Learn about how real world systems are secured

The chapters in Anderson's book fall into two categories, in my view: mechanisms for securing systems and examples of how some real world systems are secured.

We've already learned about the first category; this section is about the second category.

### Physical protection

- [Introduction to physical security](https://www.cdse.edu/documents/student-guides/PY011-guide.pdf)
- ["Physical protection" (from Anderson's book)](https://www.cl.cam.ac.uk/~rja14/Papers/SEv2-c11.pdf)
- [Design and evaluation of physical protection systems](https://www.amazon.com/Design-Evaluation-Physical-Protection-Systems/dp/075068352X)
- [Physical security: 150 things you should know](https://www.amazon.com/Physical-Security-Things-Should-Know/dp/0128094877)
- [The complete guide to physical security](https://www.amazon.com/Complete-Guide-Physical-Security/dp/1420099639)
- [Physical security systems handbook](https://www.amazon.com/Physical-Security-Systems-Handbook-Implementation/dp/075067850X)

### Nuclear command and control

- ["Nuclear command and control" (from Anderson's book)](https://www.cl.cam.ac.uk/~rja14/Papers/SEv3-ch15-dec18.pdf)
- [Nuclear Security Recommendations on Physical Protection of Nuclear Material and Nuclear Facilities](https://www-pub.iaea.org/MTCD/Publications/PDF/Pub1481_web.pdf)
- [Nuclear Security Series](https://www.iaea.org/publications/search/type/nuclear-security-series)

### Monitoring and metering

- ["Monitoring and metering" (from Anderson's book)](https://www.cl.cam.ac.uk/~rja14/Papers/SEv2-c12.pdf)
- [Electronic Postage Systems: Technology, Security, Economics](https://www.amazon.com/Electronic-Postage-Systems-Technology-Information/dp/1489986677)
- [Reliability of Electronic Payment Systems](meters/reliability_of_electronic_payment_systems.pdf)
- [On the Security of Digital Tachographs](https://www.cl.cam.ac.uk/~rja14/Papers/tacho.pdf)

### Banking and bookkeeping

- ["Banking and bookkeeping" (from Anderson's book)](https://www.cl.cam.ac.uk/~rja14/Papers/SEv2-c10.pdf)
- [Security and Privacy Analysis of Automatic Meter Reading Systems](meters/security_and_privacy_analysis_of_automatic_meter_reading_systems.pdf)

### Distributed systems

- ["Distributed systems" (from Anderson's book)](https://www.cl.cam.ac.uk/~rja14/Papers/SEv3-ch7-dec18.pdf)

### Copyright and DRM

- ["Copyright and DRM" (from Anderson's book)](https://www.cl.cam.ac.uk/~rja14/Papers/SEv2-c22.pdf)
- [The Protection of Computer Software: Its Technology and Application](https://www.amazon.com/Protection-Computer-Software-Application-Informatics/dp/0521424623)
- [European Scrambling Systems, Circuits, Tactics and Techniques](https://www.amazon.com/dp/1873556012/ref=cm_sw_em_r_mt_dp_cx1jFbVMZ87JY)

### Web browsers

- [Security architecture of the Chromium browser](http://seclab.stanford.edu/websec/chromium/chromium-security-architecture.pdf)

### BeyondCorp & zero trust

- [BeyondCorp I: A new approach to enterprise security](https://storage.googleapis.com/pub-tools-public-publication-data/pdf/43231.pdf)
- [BeyondCorp II: Design to deployment at Google](https://storage.googleapis.com/pub-tools-public-publication-data/pdf/44860.pdf)
- [BeyondCorp III: The access proxy](https://storage.googleapis.com/pub-tools-public-publication-data/pdf/45728.pdf)
- [Migrating to BeyondCorp](https://storage.googleapis.com/pub-tools-public-publication-data/pdf/f29b3e764b1122d508b7b53544a3bbadd6cd1101.pdf)
- [BeyondCorp: The user experience](https://storage.googleapis.com/pub-tools-public-publication-data/pdf/c8da594124dab1f91e6750995e2b7805403b19f1.pdf)
- [Zero Trust Networks: Building Secure Systems in Untrusted Networks](https://www.amazon.com/Zero-Trust-Networks-Building-Untrusted/dp/1491962194)

### Apple

- [Apple platform security](https://manuals.info.apple.com/MANUALS/1000/MA1902/en_US/apple-platform-security-guide.pdf)

### Cloud providers

- [Google Cloud Security Whitepapers (97 page PDF)](cloud/security_whitepapers_march2018.pdf)

### Operating systems

- [Operating System Security (by Trent Jaegar)](https://www.amazon.com/Operating-Security-Synthesis-Lectures-Information/dp/1598292129)
- [SELinux introduction](https://web.mit.edu/rhel-doc/5/RHEL-5-manual/Deployment_Guide-en-US/ch-selinux.html)
- [Original AppArmor paper](operating_systems/apparmor_original.pdf)

### Prisons

- [Jail Design Guide (National Institute of Corrections)](prisons/jail_design_guide.pdf)
- [Prison Architecture](https://www.amazon.com/Prison-Architecture-Leslie-Fairweather-RIBA/dp/0750642122)
- [A Practical Guide to Understanding and Evaluating Prison Systems](prisons/understanding_and_evaluating_prison_sysytems.pdf)
- [Technical Guidance for Prison Planning](https://content.unops.org/publications/Technical-guidance-Prison-Planning-2016_EN.pdf)
- [Handbook on Dynamic Security and Prison Intelligence](https://www.unodc.org/documents/justice-and-prison-reform/UNODC_Handbook_on_Dynamic_Security_and_Prison_Intelligence.pdf)
- [Correctional Facility Design and Detailing](https://www.amazon.com/Correctional-Facility-Design-Detailing-Krasnow/dp/0070361738)

### Museums

- [Museum Property Security and Fire Protection (from Interior Dept. Museum Property Handbook)](https://www.doi.gov/sites/doi.gov/files/migrated/museum/policy/upload/mphi-11.pdf)
- [Suggested Practices For Museum Security](http://www.securitycommittee.org/securitycommittee/Guidelines_and_Standards_files/SuggestedPracticesRev06.pdf)
- [Museum Collections Security](https://www.nps.gov/museum/publications/MHI/Chapter%209.pdf)
- [Museum Security and Protection](https://www.amazon.com/Museum-Security-Protection-Institutions-Care-Preservation-Management-ebook/dp/B000OI0Z0I)

## Assurance

The goal of security engineering is to build a system that satisfies certain security properties -- not just to add a lot of controls.
Assurance is how we prove that our system satisfies the properties we want it to.

- [Public Pentesting Reports](https://github.com/juliocesarfort/public-pentesting-reports)
- [CH26 Managing the Development of Secure Systems (from Anderson's book)](https://www.cl.cam.ac.uk/~rja14/Papers/SEv3-ch26-jul24.pdf)
- [CH27 Assurance & Sustainability (from Anderson's book)](https://www.cl.cam.ac.uk/~rja14/Papers/SEv3-ch27-jul24.pdf)
- [The Orange Book](https://csrc.nist.gov/csrc/media/publications/conference-paper/1998/10/08/proceedings-of-the-21st-nissc-1998/documents/early-cs-papers/dod85.pdf)
- See the papers in [this folder](assurance)

## Books

### Recommended (by me)

- Computer Security: Art and Science (by Bishop) - I'd read this first; it teaches security engineering in the right order: policies and models, then mechanisms, then assurance.
- Security Engineering (by Ross Anderson)
- Engineering Trustworthy Systems (by Sami Saydjari)
- "Security in Computing" (by Pfleeger) - I liked the chapter on trusted operating systems in particular.
- [Building Secure and Reliable Systems](https://www.amazon.com/Building-Secure-Reliable-Systems-Implementing/dp/1492083127)

### Not recommended

- [Time Based Security](https://www.amazon.com/Time-Based-Security-Winn-Schwartau/dp/0962870048) - [my notes](time-based-security.md). Wasn't information dense.
- "Engineering Information Security" (by Jacobs) - Mostly contains general security content, not content on security engineering. Only the systems engineering chapter felt new.
- "The Craft of System Security" (by Smith and Marchesini) - Also mostly general security content
- "Cyber Security Engineering" (by Woody and Mead) - Wasn't very information dense or well organized

### Haven't read yet

- NIST 800-16 Vol I: System Security Engineering
- NIST 800-16 Vol II: Developing Cyber Resilient Systems
- [Learning from the enemy: the GUNMAN project (NSA)](https://www.nsa.gov/Portals/70/documents/news-features/declassified-documents/cryptologic-histories/Learning_from_the_Enemy.pdf)
- [The spy in Moscow station](https://www.amazon.com/Spy-Moscow-Station-Counterspys-Deadly/dp/1250301165)

#### System engineering

- [The Art of Systems Engineering](https://www.amazon.com/Art-Systems-Architecting-Engineering/dp/1420079131)
- [Engineering Systems: Meeting Human Needs in a Complex Technological World](https://www.amazon.com/Engineering-Systems-Meeting-Complex-Technological-ebook/dp/B006QIMTKO)
- [The Engineering Design of Systems](https://www.amazon.com/Engineering-Design-Systems-Methods-Management-ebook/dp/B01BKJIDZ8)
- [Applied Space Systems Engineering](https://www.amazon.com/Applied-Space-Systems-Engineering-Technology/dp/0073408867)
- [Systems Engineering Book of Knowledge (SeBOK)](<https://www.sebokwiki.org/wiki/Guide_to_the_Systems_Engineering_Body_of_Knowledge_(SEBoK)>) - here's the [pdf](https://www.sebokwiki.org/w/images/sebokwiki-farm!w/0/0a/Guide_to_the_Systems_Engineering_Body_of_Knowledge.pdf)

## Future improvements to this repo

- Include a set of case studies where I write up how I'd secure something, following the steps above. This will help
  me make the steps more practical as well and fill in any gaps I'm missing.
