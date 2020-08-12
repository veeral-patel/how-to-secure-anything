# How Coinbase Builds Secure Infrastructure To Store Bitcoin In The Cloud

Notes on [this article](https://blog.coinbase.com/how-coinbase-builds-secure-infrastructure-to-store-bitcoin-in-the-cloud-30a6504e40ba)

- "Today, Coinbase securely stores about 10% of all bitcoin in circulation."

## Layered security & no single point of failure

- Securing your AWS admin account with a 2 factor token controlled by a second person
- Store the second factor in a vault or off site safe deposit box

## Lock down production access

- developers shouldn't have or need production SSH access

but if people need production SSH access:

- add 2 factor to your SSH
  - use FIDO U2F key or Duo two factor
  - can separate these keys and require SSH to be pair programmed
- use special laptops for SSH access
  - set aside special machines in office in a locked room that you only use for SSH access
  - use Dropcam to record who enters, leaves
  - don't use these laptops to open email, browse Internet
  - wipe these special machines regularly too
- heavily audit SSH access
  - set up bastion hosts that all SSH requests run through
  - "Restrict who has access to these least-privilege hosts"
  - "let the team know when they’re accessed (via Slack notifications"
  - "You can also wake people up (PagerDuty) when certain commands are issued"
  - "To avoid an untraceable action after getting inside, durably log every action and keystroke which goes through the bastion host"
  - "The storage of the SSH logs is just as important, since they often contain sensitive info."
    - "We run a separate disaster recovery environment that guarantees storage of every action in our environment for at least 10 years."
    - "Immutable logging is important because it gives you an audit trail if a breach ever happens to find the root cause."
- limit SSH access to those who are less likely to steal
  - run background check, make copies of drivers license/passport, get copy of fingerprints, everything you need to make an arrest warrant
  - "only grant production access to people who are citizens of the country where you operate, especially if they have family ties there. Most people would be unwilling to steal \$1M if it meant never being able to see their friends and family ever again"

## Cold storage

- try storing sensitive keys (like bitcoin private keys) entirely offline
- 98% of customer bitcoin stored offline in safe deposit boxes
- Q: is storing these keys offline really that much more secure? can a burglar not break in?

## Log all the things

- "log everything happening across all containers in your infrastructure"
- "It is critical to have a good audit trail if there ever is an incident"
- "Great logging also creates a deterrent against theft"
- "pipe every event across Coinbase through a streaming, distributed log (Kinesis) that provides flexible at-least-once guaranteed processing and a multi-day buffer of data that can be replayed as needed"
- "We run a fleet of Docker containers that process the entirety of this pipe to perform a variety of transformations, evaluations and transfer data to more permanent homes for archival, search and more."

## Consensus based deploys

- requires 2 +1s on PRs before code can be deployed
- more sensitive services can requie more +1s
- can dial up number of +1s during times of higher risk
