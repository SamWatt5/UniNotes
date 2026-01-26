- We will now use a concept of a **Non-Deterministic Turing Machine** to define a particular class of problems.
- These will be the problems that are not necessarily easy to *solve*, but for which it is easy to *verify* that something is a solution
- It will turn out that these problems are exactly the problems that can be solved by a Non-Deterministic Turing machine in polynomial time.

## Standard Definition of a Non-Deterministic Turing Machine
- **Non-Deterministic Turing Machine** (NDTM) can be defined in a similar way as we have defines an NFA.
- For each input symbol and each state, this TM can have a finite number of possible moves, each of which is of the form $(q,Y,D)$, where $q$ is a state, $Y$ is a tape symbol and $D$ is a direction
- Therefore, $\delta(q,X)$ can be $\{(p_1,Y_1,D_1),(p_2,Y_2,D_2),...,(p_k,Y_k,D_k)\}$.
- NDTM $M$ halts on some input string $w$ if any sequence of moves leads to $M$ halting.
- The string $w$ is accepted by a NDTM if any sequence of moves leads to $M$ halting in an accepting state.

> [!Theorem]
> Let $L$ be a language recognised by a NDTM $M$. Then there is a DTM $M'$ that recognises $L$

## Alternative Definition of a NDTM
- Alternatively, we can define a NDTM so that is has exactly the same components as a DTM (including a transition function that makes at most one move for each state and each tape symbol).
- However, a NDTM operates on a *two-way infinite* tape, with the input string $w$ being written on cells $1$ to $|w|$, and the operation involves two stages
- **The Guessing Stage:** A *guess* (a sequence of tape symbols) is written to the left of the string $w$ on the tape (positions $-1,-2,...$).
- **The Checking Stage:** If and when the guessing stage finishes, the head moves back to the beginning of the input string $w$ and the TM proceeds in a deterministic way.
- This is a definition of a NDTM as a *verifier*

## An Example NDTM $M$
![[Pasted image 20251128113614.png]]
![[Pasted image 20251128113634.png]]![[Pasted image 20251128113642.png]]
## NDTM as a Verifier
- In the checking stage, the NDTM will examine and use the guess for computation in some way.
- The computation ends if and when the NDTM halts in the checking stage.

> The computation is **accepting** if it halts in an accepting state in the checking stage. In any other case, it is **non-accepting**

> The string is **accepted** by the NDTM if at least one computation (with some guess) is accepting. Note that, for each input string, there is an unlimited number of computations (with an unlimited number of guesses).

> The **language** accepted by a NDTM is the set of all strings for which there is at least one accepting computation.
## Equivalence Between Definitions of a NDTM
- In the language $L$ is accepted by some NDTM $M$ that uses the standard definition, then it is also accepted by some verifier NDTM $M$ that accepts $L$.
- The reverse is also true.
## Time Complexity of a NDTM
- With a DTM that always halts, determining time complexity was easy, because there was only a single computation on each fixed input.
- With a verifier NDTM, the situation is more complicated
- There are infinitely many computations for each fixed input.
- We haven't assumed that all of the computations (with all of the guesses) for a particular input halt!
- How can we then define the time complexity of a verifier NDTM?
- We are going to define the time it takes for a NDTM to finish computation for some input only in the cases when the input is accepted.
> The time it takes for a NDTM $M$ to accept some string $W\in L(M)$, denoted by $t_M(w)$, is the *minimal* time over all the accepting computations for $w$.
- We can imagine a NDTM running on all guesses *in parallel*, so it makes sense to halt as soon as the first of these computations accepts and terminate all the others.
- On the other hand, if none of them accepts, then (since there is infinitely many of them, the NDTM will never halt.
>[!Definition] Time Complexity of a NDTM
>The time complexity of a NDTM $M$, $T_M(n)$, is the maximum time that $M$ takes to accept any of the input strings $w$ of size $n$:$$T_M(n) = max\{t_M(w)||w|=n\}$$
>If M does not accept any string of length $n$, then $T_M(n) = 1$

- $t_M(w)$ is the *minimum* time over all accepting computations for $w$, but $T_M(n)$ is the *maximum* time over all accepted strings of length $n$.
- $T_M(n)$ is the function of the size of the input string $w$, but *not* of the size of the guess for $w$.
- In most of the literature, the time complexity of a NDTM is defined in a different way.
- A standard NDTM $M$ is considered to be a **decider** of the language L(over some $\Sigma$) if $M$ halts on *every branch of computation over any string from $\Sigma$*.
- The time complexity of a NDTM that is a decider of the language $L$ is then defined in a similar way as for a DTM - the maximum number of steps taken in any computation over any input string of length $n$.
- This is obviously a different definition compared to the one we use, but the principal results remain the same.
## Time Complexity Classes for NDTM's
>[!Definition] NTIME
>We say that the language/problem $L$ belongs to the class of languages/problems NTIME$(t(n))$ if there is a verifier NDTM $M$ that accepts $L$ such that the time complexity $T_M(n)$ of $M$ is $O(t(n))$.

## Class $\mathcal{NP}$ of Languages/Problems
>[!Definition] Class $\mathcal{NP}$
>The language/problem $L$ belongs to the class of languages $\mathcal{NP}$ if it belongs to the class NTIME$(n^k)$ for some $k\in\mathbb{N}$. In other words,$$\mathcal{NP}=\bigcup\limits_{k=1}^{\infty} NTIME(n^k)$$
- The language $L$ is in $\mathcal{NP}$ if there exists a verifier NDTM of polynomial-time complexity that accepts exactly the language $L$.
- The name $\mathcal{NP}$ comes from *nondeterministic polynomial* time.
- It can be easily show that $L\in\mathcal{NP}$ if and only if there exists a standard NDTM $M$ that decides on $L$ in polynomial time.

## What Does it Mean for a Problem to be in $\mathcal{NP}$
- If the problem is in $\mathcal{NP}$, then there is a verifier NDTM $M$ with the property that for each instance of the problem $w$ for which the answer to the problem is "yes", it is possible to find a guess $c$ for which $M$ accepts that instance in the polynomial time.
- $c$ is usually called **certificate** or **proof**, and most often it represents the guess of the solution of the more general problem.
- In other words, $M$ **verifies** a solution in a polynomial-time.
- The problem might not be **solvable** in polynomial-time, but it is **verifiable** in polynomial-time
## An Example Problem: Hamiltonian Path in a Graph

>[!example] HAMPATH Problem
>Given a graph $G$ and two nodes $v_i$ and $v_j$, does there exist a Hamiltonian Path between $v_i$ and $v_j$
- A guess for this problem can be a sequence of $n$ nodes $v_i,v_l,v_{l+1},...,v_m,v_j$.
- This guess would be a certificate (proof) only if there exist edges $(v_i,v_j),(v_l,v_{l+1}),...,(v_m,v_j)$ and if all the nodes are distinct.
- In other words, the sequence of $n$ distinct nodes $v_i,v_l,v_{l+1},...,v_m,v_j$ such that $v_i\rightarrow v_l\rightarrow v_{l+1}\rightarrow ...\rightarrow v_m\rightarrow v_j$ is a Hamiltonian Path.
- We could devise a NDTM that would, for one computation over an instance of the problem, firstly make a guess (in the above format) and then check whether this guess is a certificate.
- The checking stage is simple - it just needs to check whether each of the edges $(v_i,v_j),(v_l,v_{l+1}),...,(v_m,v_j)$ exists. This is easily done in polynomial (with respect to the number of nodes in the graph) time.
- The complete computation over some input instance $(G,v_i,v_j)$ would include computations over all different guesses (guessing and checking stage for each of them).
- If there exists a Hamiltonian Path in $G$ from $v_i$ to $v_j$, then a certificate for this instance will exist and NDTM will answer "yes".
- If there does not exist a Hamiltonian Path in $G$, no guess will result in an accepting computation, therefore NDTM will not answer "yes".
![[Pasted image 20251128123245.png]]
> We could guess the solution for this graph and nodes $v_1$ and $v_8$ is $(v_1,v_3,v_5,v_4,v_2,v_6,v_7,v_8)$ and verify easily that this is a solution.

> In this case it is equally easy to check that some sequence is **not** a solution!

- Alternatively, we can consider a standard NDTM that follows all the paths from $v_i$.
- Whenever there is more than one edge from some node, we split the computation in as many branches as there are edges and follow them all in parallel.
- A computation halts in a non-accepting state when the length of path is less than $n$ (where $n$ is the number of nodes) and we encounter the same node we have already found in that path or when there are no more edges to follow.
- If the path is of length $n$, and if the last node is $v_j$ then we halt in an accepting state. Otherwise we halt in a non-accepting state.
- Each path is of length at most $n$ and it takes at most $O(n)$ time or each new node on the path to check whether it is already on the path.
- Therefore, each branch of computation will take at most $O(n^2)$ time.
- Each branch terminates in $O(n^2)$ time, therefore time complexity of this NDTM would be $O(n^2)$.
- There is a polynomial-time NDTM that decided on each instance of the HAMPATH problem.
## Are There problems that are Not in $\mathcal{NP}$?
- We may intuitively think that every problem is $\mathcal{NP}$.
- If we are given a solution to a problem, it is surely always easy to verify that this is a solution
- However, this is not necessarily true.
- 
> [!example] $\overline{HAMPATH}$ Problem
-Given a graph G and two nodes $v_i$ and $v_j$, return *yes* if there **does not** exist a Hamiltonian Path from $v_i$ to $v_j$ and *no* otherwise.

- Even if we know that the answer to this problem is *yes*, it is hard to verify that this is the correct answer without trying all the paths in the graph (which is definitely not a polynomial-time computation).
- Therefore, it is not clear whether $\overline{HAMPATH}$ is in $\mathcal{NP}$

## $\mathcal{P} = \mathcal{NP}$ Problem
- Since every DTM can be seen as a NDTM (with one choice of a move for every state and every input symbol), it is obvious that $\mathcal{P} \subset \mathcal{NP}$
- This is intuitively obvious - if we can solve a problem in polynomial-time, we can certainly verify the guessed solution in polynomial time. We simply ignore the guessed solution, compute a solution and then compare it with the guessed one.
- It also looks like the $\mathcal{NP}$ class should be larger than the $\mathcal{P}$, that there are polynomially-verifiable problems that are not polynomially-solvable.
- But this has not been proven yet. There is still no known problem for which it was proven that it is in $\mathcal{NP}$ but not in $\mathcal{P}$.

>[!Fail] $\mathcal{P} = \mathcal{NP}$ Problem
>Whether $\mathcal{P} = \mathcal{NP}$ or $\mathcal{P} \neq \mathcal{NP}$ is universally recognised as the most important open problem in theoretical computer science.

- To prove that $\mathcal{P} \neq \mathcal{NP}$, we would need to find a problem from the class $\mathcal{NP}$ for which no polynomial-time DTM can exist that solves this.
- On the other hand, to prove that $\mathcal{P} = \mathcal{NP}$, we would need to prove that every polynomially-verifiable problem is also polynomially-solvable.
- Many scientists believe that $\mathcal{P}\neq \mathcal{NP}$, because $\mathcal{NP}$ problems have been known for a long time for which still no polynomial-time solution has been found.
$L_d = \{ w_i \mid M_i \text{ **does not** accept } w_i \} \] :contentReference[oaicite:0]{index=0} and then *assume* \(L_d\) is partially decidable by some TM \(D\). Using \(D\), we construct a new machine \(E\) that, on input \(w_i\): - runs \(D\) on \(w_i\); - **if** \(D\) accepts \(w_i\), then \(E\) goes into an infinite loop (so it does *not* accept); - **if** \(D\) never accepts \(w_i\), then \(E\) is arranged so that it *does* accept \(w_i\). So \(E\) recognises the **complement** of \(L_d\). Now let \(w_k\) be the code of \(E\) itself. From the construction you get: - \(w_k \in L_d \iff M_k\) (which *is* \(E\)) **does not** accept \(w_k\), - but by how \(E\) was built, that is equivalent to “\(w_k\) is **not** in \(L_d\)”. So you end up with \[ w_k \in L_d \iff w_k \notin L_d$
