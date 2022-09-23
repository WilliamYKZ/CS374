# Lecture 6

## Closure Properties

1. Informal Definition: A set $A$ is **closed** under an operation $op$ is applying $op$ to any elements of A results in an element that also belongs to A. 

### Example

- Integer: closed under $+,-,*$, but not division. 
- Rrgular Languages: Closed under union, intersection, Kleene star, complement, difference, homomorphism, inverse homomorphism, reverse,...



## Not all Languages are Regular

1. Theorem: Languages accepted by DFAs, NFAs, and regular expressions are the same. 

2. Is every language a regular language? 

   No, Prove: Since each DFA M can be represented as a string over a finite alphabet $\Sigma$ by appropriate encoding. HEnce number of regular languages is countably infinite, Number of languages is uncountably infinite, Hence there must be a non-regular language. 



### Example 1: 

$L=\left\{0^n 1^n \mid n \geq 0\right\}$, Prove $L$ is non-regular.

Proof: Suppose $L$ is regular. Then there is a DFA M such that $L(M)=L$. Let Let $M=(Q,\{0,1\}, \delta, s, A)$ where $|Q|$ is finite.

Consider strings $\epsilon, 0,00,000, \cdots, 0^n$, total of $n+1$ strings. Let $q_i = \delta^*(s,0^i)$. 

By pigeon hole principle $q_i=q_j$ for some $0\le i\le j\le n$. That is, $M$ is in the same state after reading $0^i$ and $0^j$ where $i \neq j$. 

$M$ should accept $0^i 1^i$ but then it will also accept $0^j 1^i$ where $i \neq j$.
This contradicts the fact that $M$ accepts $L$. Thus, there is no DFA for $L$.



## Equivalence States

1. Definition: $M=(Q, \Sigma, \delta, s, A):$ DFA. Two state $p,q\in Q$ are equivalent if for all strings $w\in \Sigma^*$, we have that 
   $$
   \delta^*(p, w) \in A \Longleftrightarrow \delta^*(q, w) \in A
   $$
   One can merge any two states that are equivalent into a single state. 



2. Definition: Two states $p,q\in Q$ are distinguishable if there exists a string $w\in\Sigma^*$, such that.
   $$
   \delta^*(p, w) \in A \quad \text { and } \quad \delta^*(q, w) \notin A\\
   OR\\
   \delta^*(p, w) \notin A \quad \text { and } \quad \delta^*(q, w) \in A
   $$
   

3. Definition: Every string $w\in \Sigma^*$ defines a state $\nabla w=\delta^*(s,w)$.



4. Definition: Two string $u,w\in\Sigma^*$ are ditinguishable for $M$ if $\nabla u$ and $\nabla w$ are distinguishable.



5. Definition: (Direct restaement) Two prefixes $u,w\in\Sigma^*$ are distinguishable for a language $L$ is there exists a string $x$, such that $ux\in L$ and $wx\notin L$. 