# Week 2 Lecture 1 - Transition Function on Strings for DFA

## Review: Deterministic Finite Automaton (DFA)
>[!definition] Definition (Deterministic Finite Automaton)
>A **Deterministic Finite Automaton (DFA)** is a 5-tuple $(Q, \Sigma, \delta, q_0, F)$ where:
>- $Q$ is a finite set of **states**
>- $\Sigma$ is a finite **alphabet** (input symbols)
>- $\delta: Q \times \Sigma \to Q$ is the **transition function**
>- $q_0 \in Q$ is the **start state**
>- $F \subseteq Q$ is the set of **accepting states**

### Key Properties
- Exactly one transition per state-symbol pair (deterministic behaviour)
- Always in **one** state at a time
- No external memory — only the current state stores information
- Reads input **symbol-by-symbol** from left to right

## Extended Transition Function for Strings
>[!definition] Definition (Extended Transition Function)
>The **extended transition function** $\hat{\delta}: Q \times \Sigma^* \to Q$ is defined recursively as:
>
>- **Base case:** $\hat{\delta}(q, \epsilon) = q$
>- **Recursive case:** $\hat{\delta}(q, wa) = \delta(\hat{\delta}(q, w), a)$
>
>for string $w \in \Sigma^*$ and symbol $a \in \Sigma$.

### Interpretation
- $\hat{\delta}(q, w)$ gives the **state reached** after processing the entire string $w$ starting from $q$.
- The DFA processes input **left to right**, maintaining a single active state.

## Formal Definition
$$
\hat{\delta}(q, w) =
\begin{cases}
q & \text{if } w = \epsilon \\
\delta(\hat{\delta}(q, x), a) & \text{if } w = xa, x \in \Sigma^*, a \in \Sigma
\end{cases}
$$

>[!definition] Definition (Language Accepted by a DFA)
>The **language** accepted by DFA $M$ is:
>
>$$L(M) = \{w \in \Sigma^* \mid \hat{\delta}(q_0, w) \in F\}$$

## Examples
>[!example] Example 1: DFA accepting strings with an even number of 0s
>Alphabet: $\Sigma = \{0,1\}$
>
>States: $Q = \{q_0, q_1\}$, with $F = \{q_0\}$.
>
>Transitions:
>```mermaid
>graph LR
>    A((q0)) -->|1| A
>    A -->|0| B((q1))
>    B -->|1| B
>    B -->|0| A
>```
>Processing examples:
>- $\hat{\delta}(q_0, "010") = q_1$ → reject
>- $\hat{\delta}(q_0, "0101") = q_0$ → accept

>[!example] Example 2: Step-by-Step Processing
>Let $Q = \{q_0, q_1, q_2\}$ and $\Sigma = \{a, b\}$.
>
>|$\delta$|$a$|$b$|
>|---|---|---|
>|$q_0$|$q_1$|$q_2$|
>|$q_1$|$q_2$|$q_0$|
>|$q_2$|$q_0$|$q_1$|
>
>Process $w = aba$ starting from $q_0$:
>- $\hat{\delta}(q_0, a) = q_1$
>- $\hat{\delta}(q_0, ab) = q_0$
>- $\hat{\delta}(q_0, aba) = q_1$

If $F = \{q_1\}$, then **"aba"** is accepted.

## Applications
- DFAs recognize **Regular Languages**
- Used in **lexical analysis**, **text processing**, **hardware design**, and **protocol validation**
