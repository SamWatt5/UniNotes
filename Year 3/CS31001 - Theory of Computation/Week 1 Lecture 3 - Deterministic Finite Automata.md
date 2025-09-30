# Motivation and Simple Example
## Why Deterministic Finite Automata
- To study the limitation of computers precisely, we need some *model* of a computer
- The model needs to be general enough to encompass all the current and future computers, abstracting away complicated details.
- It also needs to be "equivalent" in some way to a computer.
	- For example, anything computable in our model has to be computable on a real computer and vice versa.
## What is Deterministic Finite Automaton?
- The simplest model (and least powerful) that we will consider is the **deterministic finite automaton (DFA)**
- DFA has a finite set of *states* and is always in *exactly one* of these states
- It allows input symbols from some fixed alphabet
- It operates over string of input symbols from that alphabet. It reads the string symbol-by-symbol from left to right until all  the symbols have been read
- Each time a symbol is read, the DFA either stays in the same state it is currently, or moves to some other state
- Produces no output - after reading the string, it returns one of two possible answers - *accept* or *reject*
- The state in which the automaton is depends solely on the sequence of input symbols that have been processed so far.
## Limitations of DFAs
- Has some obvious limitations - no readable-writeable memory (but can still remember information), no output other than binary *accept* or *reject*.
- Finite automaton is still a very powerful abstraction.
- They are very useful as an introduction to a precise mathematical definition of a computer and of a computation.
## DFA Example
>[!example] Parking Ticket Machine
>Suppose we need to design a parking ticket machine as a DFA. The machine should accept 50p, £1 and £2 coins and should require a payment of £2 (no change given) to issue a whole day parking ticket.

- Input is a sequence of coins put in by a machine user, where each coin belongs to a set $\{50p,£1,£2\}$.
- There is no output - after the sequence of coins is inserted, the machine either *accept* the sequence (and issues a ticket) or, otherwise, *rejects* it (by simply not issuing a ticket)
- We need to have some states in out automaton and the way of moving between the states depending on the coin inserted.
- We need to memorise the amount of money put in so far after each coin is inserted
- *But wait, we said that the DFA has no writable/readable memory!*
- We can use the states to keep information about this - each state should correspond to a specific amount of money put in.
- The possible states are **0p, 50p, £1, £1.50** and **£2 or more**
- Our automaton *starts* in the state **0p**.
- From that state, it can move to state **50p** (upon receiving 50p coin), **£1** (upon receiving £1 coin) and **£2** (upon receiving £2 coin).
- Similarly we can determine to what state the automaton move from each other state on each input (coin) received.
- If, at the end of processing the sequence of coins inserted, the automaton is in the state **£2 or more**, it issues the ticket
We will name the states by the amount of pennies put in, with the state 200 representing **£2 or more**
![[Pasted image 20250930113324.png]]
What did we need in order to describe this automaton completely?
- What states the automaton has, together with their names (so that we can distinguish between the states)
- What are the allowed inputs.
- How we move between the states when we receive an input.
- In which state the automaton starts and in which state(s) it needs to end the computation in order to "accept" the input.

- In this example the automaton is always in **exactly one** state
- Later we will see generalisation of DFAs that can also be in **more or less than one state** at a time
# Definition of Deterministic Finite Automaton
>[!definition] Deterministic Finite Automaton (DFA)
>Deterministic Finite Automaton is a 5-tuple ($Q,\Sigma, \delta, q_0, F$) where
>- $Q$ is a finite set of *states*
>- $\Sigma$ is a finite *alphabet* (set of possible inputs)
>- $\delta:Q\times \Sigma \rightarrow Q$ is the transition function
>- $q_0 \in Q$ is the start state
>- $F \subset Q$ is the set of *accepting states*

>[!definition] Acceptance of a String (Informal)
>String $w$ over the alphabet $\Sigma$ is accepted by DFA $M$ if, after processing it completely, the automaton ends up in one of the accepting states

## Transition Function $\delta:Q\times \Sigma \rightarrow Q$
- Takes a pair $(p, a)$ as an input, where $p$ is a state and $a$ is an input symbol, and returns a state $q$.
- if $\delta(p,a)=q$ then we say there is a *transition* from state $p$ to state $q$ on input symbol $a$
- A transition has to be defined for *every* state and *every* input symbol
- Therefore, from every stare we have to have a transition for every input symbol.
- Transition function can be represented by a table

| $\delta$ | 50p | £1  | £2  |
| -------- | --- | --- | --- |
| 0        | 50  | 100 | 200 |
| 50       | 100 | 150 | 200 |
| 100      | 150 | 200 | 200 |
| 150      | 200 | 200 | 200 |
| 200      | 200 | 200 | 200 |
## Coming Back to Our Example
>[!example] Our Finite Automaton
>$M=(Q,\Sigma,\delta,0,F)$ where
>- $Q=\{0,50,100,150,200\}$
>- $\Sigma=\{50p,£1,£2\}$
>- $\delta$ is given by a table 
>
>| $\delta$ | 50p | £1  | £2  |
>| -------- | --- | --- | --- |
>| 0        | 50  | 100 | 200 |
>| 50       | 100 | 150 | 200 |
>| 100      | 150 | 200 | 200 |
>| 150      | 200 | 200 | 200 |
>| 200      | 200 | 200 | 200 |
>- $F=\{200\}$
>- Because form the state $50$ on input $50p$ the automaton moves to the state $100$, we have that $$\delta(50,50p)=100$$

## A Few Points and Conventions
- Accepting states are also sometimes called **final states**
- The set of accepting states can also be empty
- The naming of the states does not have any impact on the operation of automaton
- It is usual convention to name the states $q_0,q_1,...,q_n$.
- DFA operates on strings over its input alphabet.
- The main questions that we will be considering in our study of finite automata are
	- Is a given string $w$ accepted by the given DFA?
	- What are all the strings that are accepted by the given DFA?
	- Can we design a DFA that will accept all the strings from a given language $L$, and no other strings?
## Representing DFA - Transition Graph
- Nodes of a graph represent states.
- Directed edges (arrows) represent transitions between states, with the labels of the arrows representing input symbols.
- The starting state is represented by an arrow labeled "start" going to it.
- Every final state is represented by a double circle.
![[Pasted image 20250930113324.png]]
## Representing DFA - Transition Table
| $\delta$        | 50p | £1  | £2  |
| --------------- | --- | --- | --- |
| $\rightarrow$ 0 | 50  | 100 | 200 |
| 50              | 100 | 150 | 200 |
| 100             | 150 | 200 | 200 |
| 150             | 200 | 200 | 200 |
| $^* $200        | 200 | 200 | 200 |
# Another Example of DFA
>[!Example]
>Design a DFA that will accept all strings over alphabet $\{0,1\}$ that end with substring $01$

>[!tip] How do We Design a DFA?
>- Consider what information about the input read so far we need to remember
>- Represent this information through the states of the DFA (designating one state as a starting state, and one or more as final states)
>- Determine transition out of each state on each possible input symbol
>- States need to be designed in such a way that the DFA transits, from each state on each input symbol, to a single correct state
>- DFA does not know what symbols it has read so far, nor how many symbols there are remaining in the string
>- After each symbol read, the DFA has to be in an accepting state if the string read so far should be accepted, and in non-accepting state otherwise

>[!question] What States Should We Have?
>**How about just two states?**
>- The state $q_1$ when the last two symbols read were $0$ and $1$ (in that order)
>- The state $q_0$ when the last two symbols read were something else
![[Pasted image 20250930121453.png]]
>We just need to transition from $q_0$ on input symbol $1$. But where should this transition lead? $q_0$? $q_1$?
>**How about three states?**
>- The state $q_2$ when the last two symbols were $0$ and $1$ (in that order)
>- The state $q_1$ when the last two symbols read were not $0$ and $1$(in that order), but the last symbol read was $0$
>- The state $q_0$ when the last two symbols read were not $0$ and $1$ (in that order), but the last symbol read was $1$ or we haven't read anything so far.
![[Pasted image 20250930121924.png]]
>**Another solution: Four states**
>- One state for each combination of the last two symbols read so far: $00, 01, 10, 11$.

## Acceptance of a String by a DFA
- String $w$ is accepted by a DFA $M$ if $M$ ends up in accepting state when it finishes reading $w$.
- This definition is understandable, but it is not formal enough.
- Transition function gives us a precise notion of a *computational step* of a DFA
- If $\delta(p,a)=q$, we say that the automaton moves from state $p$ to state $q$ when it reads the symbol $a$ in one step.
- We need some similar definition of a state that the automaton moves to when it reads the complete string.
- More on that next week...













