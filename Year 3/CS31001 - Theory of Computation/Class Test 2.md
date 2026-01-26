1. 
A language L is partially decidable but not totally decidable if there exists a turing machine that accepts the language, but there does not exist a turing machine that accepts the language that halts on every input.

2. 
(a) Give the transition table for M. 
(b) Is $\langle M, w\rangle \in L_{halt}$? Give a very brief reason for your answer. 
(Recall that X1 = 0, X2 = 1, X3 = B, D1 = L, D2 = R.)**
a) 

| $\delta$ | 0           | 1           | $B$ |
| -------- | ----------- | ----------- | --- |
| $q_0$    | $(q_0,0,L)$ | $(q_0,1,R)$ | $-$ |
b) Yes, $\langle M, w\rangle \in L_{halt}$, since $M$ halts on input $w$.

3. 
(1)$L_{10} = \{1^n0^n|n\leq 1\}$
(2)$L_{d} = \{w_i|M_i$ does not accept $w_i\}$
(3)$L_{halt} = \{\langle M, w\rangle|M$ halts on input $w\}$

(1) 
*(a)* is true for $L_{10}$ since there exists 



