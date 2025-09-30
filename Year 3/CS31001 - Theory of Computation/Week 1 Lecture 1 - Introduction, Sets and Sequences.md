## What is this module about?
- Fundamental question: *What are the limits of current (and any future) computers?*
	- *Are there any problems that the computers cannot solve?
	- *Are there problems that the computers can solve, but that require impractical amount of resources (computing power, time etc.)
- In order to answer these, we need some *model* of a computer
- Model needs to be powerful enough to represent the computers in some way, but also needs to abstract over complicated features of computers
- Two main models that we will consider are *finite state automata* and *Turing machines.*
## Finite State Automata and Regular Expressions
- Finite automata are very simple "computers" with limited but important capabilities
- They are very well understood
- Regular expressions are a useful way of describing various kinds of strings
- Finite automata and regular expressions are closely related - a first example of the relationship between languages and machines
## Computability
- What does it mean to say that something can be computed?
  Are there things which cannot be computed?
- If so, how could this be proved?
- We need a model of a computer that has the same capabilites as the current (and future) computers

## Complexity
- What can be computed given reasonable constraints on the time (and space) available?
- Many problems share a common feature - solutions are hard to find but easy to verify
- This leads to the very important notion of NP-completeness, a vital tool in trying to develop good algorithms
- The $P \stackrel{?}{=} NP$ problem
# Sets
- **Set** is a basic term that is usually not defined, but is intuitively understood.
- Elements can be any type of objects (numbers, letters, symbols, functions, other sets...).
- The symbol $\in$ denotes set membership. Conversely, $\notin$ denoted non-membership
	- $1 \in \{1,2,3\}$
	- $4 \notin \{1,2,3\}$
	- Mostly, we use membership to a set and assumptions of theorems etc.
	- For example, "Let $a \in X$" means "Let us take one element that belongs to the set $X$ and name it $a$"
	- **Empty set**, denoted by $\emptyset$, is a set that has no elements
## Describing sets
- We can describe the set by listing all the elements of the set
- $\{1,2,3,4\}, \{$blue, orange, yellow$\},\{\{1,2\},\{3,4,5\}\}$
- We can use similar notation for the infinite sets, as long as it is completely obvious what elements are in the set
- $\{1,2,3,...\}$ for the set of natural numbers, or $\{...,-2,-1,0,1,2,...\}$ for the set of whole numbers
- Or we can describe a set by listing all the rules that its elements satisfy
- {$n|n$ is a whole number, $n > 4$} describes the set $\{5,6,7,8,...\}$
- Or even $\{2k+1|k$ is a whole number, $k \leq 0\}$ which describes the set $\{1,3,5,7,...\}$
## Subset
##### Definition
>[!definition]
>Set $A$ is a subset of set $B$ if every element of $A$ is also an element of $B$. This is denoted by $A \subset B$.

- $\{1,3\} \subset \{1,2,3,4\}$ 
- is $\{1,2,3,4\} \subset \{1,2,3,4\}$ ?
	- Yes! $A \subset B$ does not preclude $A$ and $B$ from being equal.
- $\{1,2,3,4\} \subset \{1,2,2,3,3,4\}$ 
	- Yes, because every element of $\{1,2,3\}$ is also an element of $\{1,2,2,3,3,4\}$ 
- $\{1,3\} \subset \{4,1,2,3\}$ 
- How about $\emptyset \subset \{1,2,3\}$?
	- *The empty set is a subset of every set*
## Equality of Sets
$\{1,2,3,4\} \subset \{1,2,2,3,3,4\}$ and $\{1,2,2,3,3,4\} \subset \{1,2,3,4\}$ prompts the question of **When are two sets equal?**
>[!definition] Definition (Equality of Sets)
>Sets $A$ and $B$ are equal if they comprise of the same elements.

but also
>[!definition] Definition (Equality of Sets)
>Sets $A$ and $B$ are equal if $A \subset B$ and $B \subset A$

Very often, it is the second definition that we use to prove that two sets are equal.
## Finite Union of Sets
>[!definition] Definition (Union of Two Sets)
>Union of sets $A$ and $B$ denoted by $A \cup B$ is the set that comprises all the elements that are in $A$ or $B$ or both.

- $\{1,2\} \cup \{2,3,4\} = \{1,2,3,4\}$ 
- Union is commutative, meaning that $A \cup B = B \cup A$
- Union is associative, meaning that $(A\cup B)\cup C = A \cup (B\cup C)$
- What is $A \cup \emptyset$
- $A \cup \emptyset = A$ for every set $A$
>[!definition] Definition (Finite Union of Sets)
>Union of a finite number of sets $A_1,A_2,...,A_n$ denoted by $\bigcup\limits_{i=1}^{n} A_{i}$, is the set that comprises all the elements that are in any of the sets $A_1,A_2,...,A_n$.

- $\{1,2\}\cup\{2,3\}\cup\{1,3\} = \{1,2,3\}$
## Finite Intersection of Sets
>[!definition] Definition (Intersection of Two Sets)
>Intersection of sets $A$ and $B$, denoted by $A\cap B$, is the set that comprises all the elements that both in $A$ and $B$.

- $\{1,2\}\cap\{2,3,4\} = \{2\}$
- Intersection is commutative, meaning that $A \cap B = B \cap A$
- Intersection is associative, meaning that $(A\cap B)\cap C = A \cap (B\cap C)$
- What is $\{1,2\}\cap\{3,4\}$?
>[!definition] Definition (Finite Intersection of Sets)
>Union of a finite number of sets $A_1,A_2,...,A_n$ denoted by $\bigcap\limits_{i=1}^{n} A_{i}$, is the set that comprises all the elements that are in all the sets $A_1,A_2,...,A_n$.

- $\{1,2\}\cap\{2,3\}\cap\{2,4\} = \{2\}$
- $\{1,2\}\cap\{2,3\}\cap\{3,4\} = \emptyset$
## Union and Intersection of Infinitely Many Sets
>[!definition] Definition (Union of Infinitely Many Sets)
>Union of a finite number of sets $A_1,A_2,...,A_n,...,$ denoted by $\bigcup\limits_{i=1}^{\infty} A_{i}$, is the set that comprises all the elements that are in at least one of the sets $A_1,A_2,...$

- $\bigcup\limits_{i=1}^{\infty} \{1,i\} = \{1,2,3,...\}$
- Note that the union of infinitely many sets does not need to be an infinite set. For example - $\bigcup\limits_{i=1}^{\infty} \{1\} = \{1\}$
>[!definition] Definition (Intersection of Infinitely Many Sets)
>Intersection of infinitely many sets, $A_1,A_2,...$, denoted by $\bigcap\limits_{i=1}^{\infty} A_i$, is the set of all elements that are in all of the sets $A_1,A_2,...$

- $\bigcap\limits_{i=1}^{\infty} \{1,i\} = \{1\}$
## Power Set
>[!definition] Definition (Power Set)
>Power set of the set $A$, denoted by $\mathcal{P}(A)$ is the set of all subsets of $A$

- Let $A = \{1,2,3\}$. Then $\mathcal{P} (A) = \{\emptyset,\{1\},\{2\},\{3\},\{1,2\},\{1,3\},\{2,3\},\{1,2,3\}\}$
- What is $\mathcal{P}(\{0\})$?
	- $\mathcal{P}(\{0\}) = \{\emptyset,\{0\}\}$
- What is $\mathcal{P}(\emptyset)$?
	- $\mathcal{P}(\emptyset) = \{\emptyset\}$
- How many elements are there in $\mathcal{P}(A)$ if $A$ has $n$ elements?
## Set Difference and Complement of a Set
>[!definition] Definition (Set Difference)
>Set difference between the two sets $A$ and $B$, denoted by $A\textbackslash B$, is the set of all elements that are in $A$, but not in $B$

- $A\backslash{B}$ is generally not equal to $B\backslash{A}$
- $A=\{1,2,3,4\}, B=\{4,5,6\}$, then $A\backslash{B} = \{1,2,3\}$ and $B\backslash{A}=\{5,6\}$
>[!definition] Definition (Set Complement)
>The complement of a set $A$ (a subset of set $B$), denoted by $A^\mathsf{C}$, is the set $B\backslash{A}$

- The definition of the complement requires that $A\subset{B}$
- If $A = \{1,2\}$ and $B = \{1,2,3,4\}$, then $A^\mathsf{C} = \{3,4\}$
# Sequences and Tuples
- A sequence of objects is a list of these objects in some order
- We ususally denote a sequence by a parentheses, together with the list of elements e.g. $(1,5,9,14)$
- Compared to sets, the order of the elements in the sequence *does matter* and *repetitions are allowed*
- $(1,1,5,8,9,9)$ is not equal to $(1,5,8,9)$, nor to $(5,1,1,8,9,9)$
- *Two sequences are equal if they are of the same length, and have the same elements in the same places*
- Sequences may be finite or infinite
- Finite sequences with $k$ elements is called a $k$-**tuple**
- 2-tuple is called a **pair**
## Cartesian Product
>[!definiton] Definition (Cartesian Product)
>Cartesian product of sets $A$ and $B$ is  set of all pairs, where the first element of the pair comes from the set $A$ and the second element of the pair comes from the set $B$

- Let $A = \{1,2\}$ and $B = \{x,y\}$, then $A\times{B}=\{(1,x),(1,y),(2,x),(2,y)\}$
- It is easy to extend this notion to the product of more than two sets
- $A^k$ denotes a Cartesian product o the set with itself $k$ times
- Let $A = \{1,2\}$. Then$$A^3=\{(1,1,1),(1,1,2),(1,2,1),(2,1,1),(2,1,2),(2,2,1),(2,2,2)\}$$


