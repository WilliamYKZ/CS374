# Lecture 3



## Graphical Representation/State Machine

![](https://github.com/WilliamYKZ/Picture/raw/main/Picture/Screen%20Shot%202022-09-17%20at%209.40.40%20PM.png)

1. Directed graph with nodes representing **states** and edge representing **transition** labeled by symbols in $\Sigma$. 
2. For each state $q$ and symbol $a\in \Sigma$ there is exactly one outgoing edge labeled by $a$. 
3. Initial/states has a pointer (or labeled as $s,q_0$ or start).
4. Some states with double circles labeled as accepting states. 



5. Every string $w$ has a unique walk that it follows from a given state $q$ by reading one letter of $w$ from left to right. 



## Definition

1. A DFA $M$ accepts a string $w$ if and only if the unique walk starting at the start state and speeling out $w$ ends in an accepting state.

2. The **language accepted** (or recognized) by a DFA $M$ is denote by $L(M)$ and define as $L(M)=\{w| M \ accepts \ w\}$.



### Formal definition of DFA

A **deterministic finite automata(DFA)** $M=(Q,\Sigma, \delta,s,A)$ is a five tuple where.

- Q is a finite set whose elements are called **states**.
- $\Sigma$ is a finite set called the **input alphabet**.
- $\delta: Q\times \Sigma\rightarrow Q$ is the **transition function**,
- $s\in Q$ is the **start state**,
- $A\subseteq Q$ is the set of **accepting** states.  



### Example:

![](https://github.com/WilliamYKZ/Picture/raw/main/Picture/Screen%20Shot%202022-09-17%20at%209.40.40%20PM.png)

- $Q:$ $\{q_0,q_1\}$.
- $\Sigma:$ $\{0,1\}$

- $\delta:$​ 

  |      | 0    | 1    |
  | ---: | ---- | ---- |
  |  q0: | q1   | q0   |
  |  q1: | q0   | Q1   |

  

- $s:$ $q_0$

- $A: \{q_1\}$ 

Remember: Accepting state is a set. 



## Extending the transition function to strings

Given DFA $M=(Q,\Sigma,\delta,s,A)$ , $\delta(q,a)$ is the state that $M$ goes to from $q$ on reading letter $a$. Useful to have notation to specify the unique state that $M$ will reach from $q$ on reading string $w$.

1. Transition function $\delta^*(q,w)=q$ if $w=\varepsilon$.
2. $\delta^*(q,w)=\delta^*(\delta(q,a),x)$ if $w=ax$. 



## Formal Definition on language accepted by $M$.

The language $L(M)$ accepted by a DFA $M=(Q,\Sigma,\delta,s,A)$ is 
$$
\left\{w \in \Sigma^* \mid \delta^*(s, w) \in A\right\}
$$


### Example

![](https://github.com/WilliamYKZ/Picture/raw/main/Picture/Screen%20Shot%202022-09-17%20at%209.40.40%20PM.png)

- $\delta^*\left(q_1, \epsilon\right)=$ $q_1$
- $\delta^*\left(q_0, 1011\right)=$ $q_1$
- $\delta^*\left(q_1, 010\right)=$ $q_1$



## Constructing Regular Expressions

1. There are two ways we can find regular expression using DFAs.

   - State removal method
   - Algebraic method

2. State removal method 

   If we have $q_1 = \delta(q_0,x)$ and $q_2=\delta(q_1,y)$,

   Then we can know $q_2=\delta(q_1,y)=\delta(\delta(q_0,x),y) = \delta(q_0,xy)$. 

   **That is a way we can simplify the DFA**



### Example1

![](https://github.com/WilliamYKZ/Picture/raw/main/Picture/Screen%20Shot%202022-09-17%20at%2011.31.38%20PM.png)

Then we can change the DFA to:

![](https://github.com/WilliamYKZ/Picture/raw/main/Picture/Screen%20Shot%202022-09-17%20at%2011.35.13%20PM.png)

Then we can get the regular expression: $\left(01+(1+00)(10)^*(0+11)\right)^*$



3. We can also use the Algebraic method: That is we can rewrite $q_1=\delta\left(q_0, x\right) \text { as } q_1=q_0 x$. 

### Example2

![](https://github.com/WilliamYKZ/Picture/raw/main/Picture/Screen%20Shot%202022-09-17%20at%2011.43.51%20PM.png)

First we can rewrite the each state.

- $q_0 = \varepsilon+q_11+q_20$
- $q_1=q_00$
- $q_2=q_01$
- $q_3=q_21+q_10+q_3(0+1)$

Since the $q_0$ is the accepting state, we just need to simplify the $q_0$.
$$
q_0 =\varepsilon +q_11+q_20\\
q_0 = \varepsilon +q_01+q_010\\
q_0 = \varepsilon+q_0(01+10)
$$
By the **Arden's Theorem**: $R=Q+RP=QP^*$

Then we can simplfy the $q_0$
$$
\begin{aligned}
&q_0=\epsilon+q_0(01+10) \\
&q_0=\epsilon(01+10)^*=(01+10)^*
\end{aligned}
$$


## Complement Language

1. If $M$ is a DFA, is there a DFA $M^\prime$ such that $L(M^\prime)=\Sigma^*\backslash L(M)$. 

![](https://github.com/WilliamYKZ/Picture/raw/main/Picture/Screen%20Shot%202022-09-18%20at%2023.21.05%20PM.png)

**Just flip the state of the states**



2. Theorem: Languages accepted by DFAs are closed under complement. 

   Which is means If $L$ is regular then $\bar{L}$ is reguar. 





## Product Construction

1. Definition: $M_1=\left(Q_1, \Sigma, \delta_1, s_1, A_1\right)$ and $M_2=\left(Q_2, \Sigma, \delta_2, s_2, A_2\right)$. The **theorem** is $L(M)=L\left(M_1\right) \cap L\left(M_2\right)$

   Now, we can have a new DFA $M=(Q, \Sigma, \delta, s, A)$

   - $Q= Q_1\times Q_2 = \{(q_1,q_2)|q_1\in Q_1,q_2\in Q_2\}$
   - $s=(s_1,s_2)$
   - $\delta:Q\times\Sigma\rightarrow Q$ where $\delta((q_1,q_2),a) = (\delta_1(q_1,a),\delta_2(q_2,a))$
   - $A=A_1\times A_2 = \{(q_1,q_2)|q_1\in A_1,q_2\in A_2\}$

### Example1:

![](https://github.com/WilliamYKZ/Picture/raw/main/Picture/Screen%20Shot%202022-09-18%20at%2023.52.35%20PM.png)



2. Definition: $M_1=\left(Q_1, \Sigma, \delta_1, s_1, A_1\right)$ and $M_2=\left(Q_2, \Sigma, \delta_2, s_2, A_2\right)$. The **theorem** is $L(M)=L\left(M_1\right) \cup L\left(M_2\right)$
   - $Q= Q_1\times Q_2 = \{(q_1,q_2)|q_1\in Q_1,q_2\in Q_2\}$
   - $s=(s_1,s_2)$
   - $\delta:Q\times\Sigma\rightarrow Q$ where $\delta((q_1,q_2),a) = (\delta_1(q_1,a),\delta_2(q_2,a))$
   - $A=\{(q_1,q_2)|q_1\in A_1 \ or\ q_2\in A_2\}$

The only different here is the accepting state. 

