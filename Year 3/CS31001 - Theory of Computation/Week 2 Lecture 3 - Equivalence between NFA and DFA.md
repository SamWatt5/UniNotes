# Week 2 Lecture 3 - Equivalence between NFA and DFA

## Theorem
>[!theorem] Fundamental Equivalence Theorem
>Let $N$ be the set of all languages accepted by **NFAs**, and $D$ be the set of all languages accepted by **DFAs**.  
>Then: $$N = D$$

### Meaning
- NFAs and DFAs recognize **exactly the same languages**
- These are called **Regular Languages**

### Proof Strategy
1. $D \subseteq N$: Every DFA can be seen as an NFA  
2. $N \subseteq D$: Every NFA can be converted into a DFA

## Part 1 — DFA to NFA ($D \subseteq N$)
>[!proof]
>- Every DFA is an NFA where each transition set has **exactly one** element.
>- Given a DFA $M = (Q, \Sigma, \delta, q_0, F)$, construct an NFA $N = (Q, \Sigma, \delta', q_0, F)$ where:
>
>$$\delta'(q, a) = \{\delta(q, a)\}$$
>
>This NFA accepts exactly the same language as $M$.

## Part 2 — NFA to DFA ($N \subseteq D$)
>[!proof]
>Every NFA can be simulated by a DFA using the **Subset Construction Algorithm**:
>- Each DFA state represents a **set of NFA states**
>- DFA simulates all NFA computation paths in parallel
>- The DFA accepts if any of those simulated paths reaches an accepting state

## Implications
- **Regular Languages** = Languages accepted by DFAs = Languages accepted by NFAs  
- Non-determinism **does not increase computational power**
- NFAs are usually more **intuitive to design**, DFAs more **efficient to execute**

## Applications
- Used in **regular expression engines**, **lexical analyzers**, and **pattern matching**
- Provides theoretical basis for converting high-level regex to efficient deterministic machines
