# Week 2 Lecture 2 - Non-Deterministic Finite Automata

## Definition
>[!definition] Definition (Non-Deterministic Finite Automaton)
>A **Non-Deterministic Finite Automaton (NFA)** is a 5-tuple $(Q, \Sigma, \delta, q_0, F)$ where:
>- $Q$ is a finite set of **states**
>- $\Sigma$ is a finite **alphabet**
>- $\delta : Q \times \Sigma \to \mathcal{P}(Q)$ is the **transition function**
>- $q_0 \in Q$ is the **start state**
>- $F \subseteq Q$ is the set of **accepting states**

### Key Difference from DFA
- In a DFA, $\delta(q, a)$ returns **one state**.
- In an NFA, $\delta(q, a)$ returns a **set of possible states** (subset of $Q$).

## Transition Function Behaviour
- $\delta(q, a) = \emptyset$ → no transitions on $a$.
- $\delta(q, a) = \{q_1\}$ → one possible transition.
- $\delta(q, a) = \{q_1, q_2, ...\}$ → multiple possible transitions.

>[!note] Concept
>NFAs **branch** into several paths — each path represents one possible computation.  
>If *any* path reaches an accepting state, the input is accepted.

## Extended Transition Function for Strings
>[!definition] Definition (Extended Transition Function for NFA)
>For an NFA $M = (Q, \Sigma, \delta, q_0, F)$, define $\hat{\delta}: Q \times \Sigma^* \to \mathcal{P}(Q)$ recursively:
>
>- **Base case:** $\hat{\delta}(q, \epsilon) = \{q\}$  
>- **Recursive case:** if $w = xa$, then  
>$$\hat{\delta}(q, w) = \bigcup_{p \in \hat{\delta}(q, x)} \delta(p, a)$$

>[!definition] Definition (Language Accepted by NFA)
>The **language** accepted by an NFA $M$ is:
>
>$$L(M) = \{w \in \Sigma^* \mid \hat{\delta}(q_0, w) \cap F \neq \emptyset\}$$
>
>A string is accepted if *any* computation path ends in an accepting state.

## Example
>[!example] Example: NFA accepting strings ending in "01"
>Alphabet: $\Sigma = \{0,1\}$
>
>```mermaid
>graph LR
>    A((q0)) -->|0,1| A
>    A -->|0| B((q1))
>    B -->|1| C((q2))
>```
>
>|$\delta$|0|1|
>|---|---|---|
>|$q_0$|${q_0, q_1}$|${q_0}$|
>|$q_1$|$\emptyset$|${q_2}$|
>|$q_2$|$\emptyset$|$\emptyset$|
>
>Accepting state: $F = \{q_2\}$

Processing input “001”:
- $\hat{\delta}(q_0, \epsilon) = \{q_0\}$
- $\hat{\delta}(q_0, 0) = \{q_0, q_1\}$
- $\hat{\delta}(q_0, 00) = \{q_0, q_1\}$
- $\hat{\delta}(q_0, 001) = \{q_0, q_2\}$  
$\Rightarrow$ Accepted since $q_2 \in F$.

## Comparison with DFA
| Aspect | DFA | NFA |
|--------|-----|-----|
| Transition Output | One state | Set of states |
| Execution Paths | Single | Multiple |
| Acceptance | Single path ends in F | Any path ends in F |

## Applications
- NFAs and DFAs recognize the **same class of languages** — the **Regular Languages**.
- NFAs are often easier to **design**, though DFAs are easier to **implement**.
