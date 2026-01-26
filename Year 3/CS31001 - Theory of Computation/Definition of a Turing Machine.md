> [!definition] Turing Machine - Formal Definition
> A Turing Machine is a 7-tuple $$M=(Q,\Sigma,\Gamma,\theta,q_0,B,F)$$
> Where:
> $Q$ - Finite set of states
> 
> $\Sigma$ - Input Alphabet
> 
> $\Gamma$ - Tape Alphabet
> 
> $\theta$ - Transition Function: $$\theta : Q \times \Gamma \rightarrow Q \times \Gamma \times {L,R}$$
> Given the current state, and the tape symbol under the head, he machine:
> 1. moves to a new state
> 2. writes a symbol on the tape (possibly the same one)
> 3. moves the head **left** or **right**
> 
> $q_0$ - Start state
> 
> $B$ - Blank symbol from $\Gamma, B \notin\Sigma$
> 
> $F\subseteq Q$ - Set of final states

00