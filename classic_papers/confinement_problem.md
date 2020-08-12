# A Note on the Confinement Problem

## The problem

- Want to confine an arbitrary program
- Doesn't mean any program which works when free will still work under confinement
- Does mean that any program, which confined, won't leak data

## Confinement rules

- total isolation: a confined program may make no calls, or transfers of controls
- transitivity: If a confined program calls another program which is not trusted, the called program must also be confined
- Masking: A program to be confined must allow its caller to determine all its inputs into
  legitimate and covert channels. We say that the channels are masked by the caller (to block all legitimate and covert channels)
- Enforcement: The supervisor must ensure that a confined program's input to covert
  channels conforms to the caller's specifications.
