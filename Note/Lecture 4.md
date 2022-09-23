# Lecture 4

## Basic 

![](https://github.com/WilliamYKZ/Picture/raw/main/Picture/Screen%20Shot%202022-09-21%20at%2015.54.11%20PM.png)

1. Informal definition: An NFA N accepts a string $w$ if and only if some accepting state is reached by $N$ from the start state on input $w$.
2. The Language accepted by a NFA N is denoted by $L(N)$ and define as $L(N):\{w\mid N\  accepts\ w\}$. 

### Example 1: 

If $010110$ accepted?

Yes, and there is many ways to accept the 010110. 

<img src="https://github.com/WilliamYKZ/Picture/raw/main/Picture/Screen%20Shot%202022-09-21%20at%2015.57.37%20PM.png" style="zoom:25%;" />

### Example 2:

What is the language accepted by $N$.

All $w$ with $11$ or $101$ as substring. 



## Formal Definition of NFA

A non-deterministic finite automata (NFA) $N=(Q,\Sigma, \delta,s,A)$ is a five tuple where 

- $Q$ is finite set whose elements are called states.
- $\Sigma$ is a finite set called the input alphabet.
- $\delta: Q \times \Sigma \cup\{\varepsilon\} \rightarrow \mathcal{P}(Q)$ is the **transition function**. ($\mathcal{P}(Q)$ is the power set)
- $s\in Q$ is the start state
- $A\subseteq Q$ is the set of accepting state. 

**Different:** The transition function of NFA is $\delta(q,a)=\{q_1,...q_r\}$ it can equal to a **set** of state. But the transition function of DFA will only go to **one state**. Also NFA will have $\varepsilon$ transition.



$\delta^*(q,w)$: set of states reachable on input $w$ starting in state $q$.

### Example 1:

![](https://github.com/WilliamYKZ/Picture/raw/main/Picture/Screen%20Shot%202022-09-21%20at%2015.54.11%20PM.png)

- $Q=\{q_0,q_1,q_2,q_3\}$

- $\Sigma= \{0,1\}$

- $\delta=$

  |      | e    | 0    | 1       |
  | ---- | ---- | ---- | ------- |
  | q0   | {}   | {q0} | {q0,q1} |
  | q1   | q2   | {q2} | {}      |
  | q2   | {}   | {}   | {q3}    |
  | q3   | {}   | {q3} | {q3}    |

- $s=q_0$

- $A=\{q_3\}$



## Extending the transition function to strings

For NFA $N=(Q,\Sigma,\delta,s,A)$ and $q\in Q$ the $\varepsilon$ reach $(q)$ is the set of all states that $q$ can reach using only $\varepsilon-$transitions.

![](https://github.com/WilliamYKZ/Picture/raw/main/Picture/Screen%20Shot%202022-09-21%20at%2016.30.34%20PM.png)

1. Definition: For $X\subseteq Q:$ $\varepsilon$ reach $(X)=\bigcup_{x\in X}\varepsilon$ reach $(x)$. 

2. $\operatorname{\epsilon reach}(q)$ : set of all states that $q$ can reach using only $\varepsilon-$transitions.

3. Defintion: Inductive definition of $\delta^*:Q\times\Sigma^*\rightarrow \mathcal{P}(Q):$

   - if $w=\varepsilon, \delta^*(q, w)=\epsilon \operatorname{reach}(q)$
   - if $w=a$ where $a \in \Sigma$ : $\delta^*(q, a)=\epsilon \operatorname{reach}\left(\bigcup_{p \in \epsilon \operatorname{reach}(q)} \delta(p, a)\right)$
   - if $w=a x$ :$\delta^*(q, w)=\epsilon \operatorname{reach}\left(\bigcup_{p \in \epsilon \text { reach }(q)}\left(\bigcup_{r \in \delta^*(p, a)} \delta^*(r, x)\right)\right)$

4. **String accept by NFA**: A string $w$ is accepted by NFA $N$ if $\delta_N^*(s, w) \cap A \neq \emptyset$.

5. **Language accept by NFA**: The language $L(N)$ accepted by a NFA $N=(Q, \Sigma, \delta, s, A)$ is
   $$
   $\left\{w \in \Sigma^* \mid \delta^*(s, w) \cap A \neq \emptyset\right\}$.
   $$



### Example 1:

What is $\delta^*(s,\varepsilon)=\{d,a,s\}$

**s** should include in the set because start state can accept $\varepsilon$. 

### Example 2:

What is $\delta^*(s,0)=\{s,d,a,b\}$

### Example 3:

What is $\delta^*(b,0)= \{c,g,d,a\}$ 

### Example 4:

What is $\delta^*(b,00)=\{g,b\}$ 

**c,d,a** should not include because we need to make sure all the string are accepted. 





## Constructing Generalized NFAs

1. Every DFA is a NFA so DNFAs are at least as powerful as DFAs.

### Example 1:

Strings that represent decimal numbers.

154, 	345.75332, 	534677567.1, 	-1, 	0.1234



### Example 2:

Strings that represent valid C comments.

```C
\* Comment 1 *\
\\Comment 2
```

![](https://github.com/WilliamYKZ/Picture/raw/main/Picture/Screen%20Shot%202022-09-21%20at%2017.30.29%20PM.png)

2. Theorem: For every NFA N there is another NFA $N^\prime $ such that $L(N)=L(N^\prime)$ and such that $N^\prime$ has the following two properties:
   - $N^\prime$ has a single final state $f$ that has no outgoing transitions.
   - The start state $s$ of $N$ different from $f$. 

​	**Important:** we can use $\varepsilon-$ transition to make two accept state in one. 

![](https://github.com/WilliamYKZ/Picture/raw/main/Picture/Screen%20Shot%202022-09-21%20at%2017.57.02%20PM.png)



## Closure Properties of NFAs

1. Theorem: For any two NFAs $N_1$ and $N_2$ there is a NFA N such that $L(N)=L(N_2)\cup L(N_2)$.

![](https://github.com/WilliamYKZ/Picture/raw/main/Picture/Screen%20Shot%202022-09-21%20at%2018.27.31%20PM.png)



2. Theorem: For any two NFAs $N_1$ and $N_2$ there is a NFA N such that $L(N)=L(N_1)\cdot L(N_2)$

![](https://github.com/WilliamYKZ/Picture/raw/main/Picture/Screen%20Shot%202022-09-21%20at%2018.29.26%20PM.png)

3. Theorem: For any NFA $N_1$ there is a NFA N such that $L(N)=(L(N_1))^*$.

![](https://github.com/WilliamYKZ/Picture/raw/main/Picture/Screen%20Shot%202022-09-21%20at%2018.31.38%20PM.png)