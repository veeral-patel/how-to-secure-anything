# Attack Planning in the Real World

- problem: most attack graph algorithms have only been able to generate attack graphs on small networks with <= 20 hosts
- on medium sized networks, building complete attack graphs becomes unfeasible (graph size increases exponentially with number of machines + possible actions)
- idea - use planning algorithms to find attack graphs without building entire attack graph

## PDDL

- serves as bridge between pentesting tool and the planner
- exploits have strict platform + connectivity requirements so failing to express those requirements in PPDL would create plans that can't be executed against real networks