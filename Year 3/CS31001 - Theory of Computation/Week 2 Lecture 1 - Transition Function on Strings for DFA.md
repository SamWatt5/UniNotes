## Reminder
- We have informally and formally defined a deterministic finite automaton (DFA)
- Formally, a DFA $M$ is a 5-tuple $M=(Q,\Sigma,\delta,q_0,F)$ where $\delta$ is a transition function
- $\delta(q,a)=p$ tells us that the DFA transitions to state $p$ from state $q$ when it reads input symbol $a$
- A string $w$ of symbols from $\Sigma$ is accepted if the DFA ends up in an accepting state when it reads the whole string $w$
- To reason formally about DFAs, we need a more formal definition of when the string is accepted by a DFA
- For this purpose, we extend the transition function to strings (i.e. define the transition functions for complete strings, not only individual symbols)













