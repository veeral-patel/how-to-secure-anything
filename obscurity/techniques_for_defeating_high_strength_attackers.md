# Obfuscation for Security: Techniques for Defeating High-Strength Attackers

> This was NOT written by me. This was written by [nickpsecurity](https://news.ycombinator.com/user?id=nickpsecurity) on [Pastebin](https://pastebin.com/RS5FxKAe); I've just saved his writeup to the repo in case the Pastebin paste gets deleted.

Obfuscation has been one of my strongest measures for security for a long time. Cold War espionage writing taught me it's absolutely critical to defeating nation-state opponents given they'll always outsmart your specific, known techniques. What obfuscation does, if used effectively, is require the attacker to already have succeeded in some attack to even launch an attack. Defeating that paradox forces them to attack you in many ways, increasing work and exposure risk. The more obfuscation you have built in, the more that goes up. Very important moves to keep them effective are to ensure the obfuscation is invisible from users' or network perspective, make sure obfuscation itself doesn't negate key properties of security controls, make darned sure there are security controls rather than only obfuscation, only a few individual people knowing the obfuscations, and air gapped (or guarded) machines controlling them.

Here are some obfuscations I've used in practice with success, including against strong attackers, per monitoring results, third party tests, and occasional feedback from sysadmins that apply them or independently invented them:

1. Use non-x86 and non-ARM processor combined with strong Linux or BSD configuration that also _advertises as x86 box_. Leave no visible evidence you're buying non-x86 boxes. This can work for servers. Some did it with PPC Mac's after they got discontinued. This one trick has stopped so many code execution attempts for so long it's crazy. I really thought a clever shortcut would appear by now outside browser Javascript, memory leaks, or something. An expansion on it with FPGA's is randomized instruction sets with logs & fail-safe for significant, repeated failures.

2. Non-standard ports, names, whatever for about everything. Works best if you're not relying on commercial boxes that might assume specific ports and such. So, be careful there. This one, though, just keeps out riff raff. Combine it with strong HIDS and NIDS in case smarter attackers slip up. Don't rely on it for them, though.

3. Covert, port-knocking schemes. An example of a design I think I modified and deployed was SILENTKNOCK. It gives no evidence a port-knocking scheme is in use unless they have clear picture of network activity. Even still, they can't be sure _how_ your traffic was authorized by looking at the packets. Modifications to that scheme that don't negate security properties and/or use of safety-enhanced languages/compilers can improve its effectiveness. My deployment strategy for this and guards was a box in front of the server that did it transparently. Lets you protect Windows services prone to 0-days. Think it stopped an SSH attack or something on Linux once. Can't recall. Very flexible. Can be improved if combined with IP-level tunneling protocol machine-to-machine in intranet. Which can also be obfuscated.

4. Use of unpopular, but well-coded, software for key servers or apps. I especially did this for mail, DNS, web servers, and so on. Black hat economics means they usually focus on what brings them the most hacks for least time investment. This obfuscation counters their economic incentive by making them invest in attacking a niche market with almost no uptake. Works on desktops, too, where I recommended alternative Office suits, PDF readers, browsers, and so on that had at least same quality but not likely same 0-days as what was getting hit.

5. Security via Diversity. This builds on 4 where you combine economics and technology to force black hats to turn a general, one-size-fits-all hack into a targeted attack specifically for _you_. You might choose among safe libraries, languages, protocols, whatever without advertising their use in the critical app or service. Additionally, there's work in CompSci on compilers that automatically transform your code into equivalent, but slightly different, code with different probabilities of exploits due to different internal structure. That's not mature, yet, imho. You could say all the randomization schemes in things like OpenBSD and grsecurity fit into this too. Those are more mature & field-tested. If Googling, the key words for CompSci research here are "moving target," "security," "diversity," and "obfuscation" in various combinations.

6. My old, polymorphic crypto uses obfuscation. The strongest version combined three AES candidates in counter mode in layers. The candidates, their order, the counters, and of course the keys/nonces were randomized with exception being same one couldn't be used twice. That came from only criticism I got with evidence: DES meet in middle. FPGA's got good at accelerating specific algorithms. So, I modified it to allow weaker ciphers like IDEA or Blowfish in middle layer but _no less than one_ AES candidate in _evaluated configuration and implementation_ preferably on outer layer. Preferably two AES + 1 non-AES for computational complexity. All kinds of crypto people griped about this but never posted a single attack against such a scheme. Whereas, I provably stop one-size-fits-all attacks on crypto by layering several randomly with at least one strong one. Later, I saw TripleSec do a tiny subset of it with some praise. Also convinced Markus Ottella of Tinfoil Chat to create a non-OTP variant using a polycipher. He incorporated that plus our covert-channel mitigations to prevent traffic analysis. Fixed-size, fixed-transmission is obfuscation that does that which I learned from high-security, military stuff.

7. Last one, inspired by recent research, is to use any SW or HW improvements from academia that have been robustly coded and evaluated. These usually make your system immune to common attacks [2], mitigate unauthorized information flows [3], create minimal TCB's [4][5], use crypto to protect key ops [6], or obfuscate the crap out of everything [7]. I mainly recommend 1-6, though. ;) Then, don't advertise which ones you use. Also, I encourage FOSS developers to build on any that have been open-sourced to get them into better shape and quality than academics leave them. Academics tend to jump from project to project. They deserve to see their designs hit production quality if they did the hard work of getting it toward practical and FOSSing a demo for us.

[1] http://www-users.cs.umn.edu/~hopper/silentknock_esorics.pdf

[2] https://www.cis.upenn.edu/acg/softbound/

[3] https://www.cs.cornell.edu/projects/fabric/

Note: See related project in bottom-right for other good tech this builds on or was inspired by.

[4] http://genode.org/

[5] https://robigalia.org/

[6] https://theses.lib.vt.edu/theses/available/etd-10112006-204811/unrestricted/edmison_joshua_dissertation.pdf

[7] http://www.ics.forth.gr/_publications/papadog-asist-ccs.pdf

Nick P.
Security Engineer/Researcher
(specialize in solutions against high-strength attackers)
