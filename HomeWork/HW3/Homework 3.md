# Homework 3

## Question 1

### **Part a**: 

Set NFA $N_1=(\Sigma,Q_1,s_1,A_1,\delta_1),N_2=(\Sigma,Q_2,s_2,A_2,\delta_2)$. $N_1$ accepts all string that contains odd number of 0s, $N_2$ accept all string that contains substring $101$.

Then we can construct an NFA $N=(\Sigma, Q,s,A,\delta)$ based on $N_1,N_2$:
$$
N=\left\{
\begin{array}{l}
	\Sigma\\
	Q=Q_1\times Q_2\\
	s= (s_1,s_2)\\
	A= \{(x,y)\mid x\in A_1\text{ or } y \in (Q_2- A_2)\}\\
	\delta((q_1,q_2),a)=(\delta_1(q_1,a),\delta_2(q_2,a))\\
\end{array}
\right.
$$
 For arbitrary state $(q_i,q_j)\in Q$ returned by $N$ with input $w$,   $q_i, q_j$ equals to the state returned by $N_1, N_2$ with input $w$ separately. Since we set $A=\{(x,y)\mid x\in A_1\text{ or } y \in (Q_2- A_2)\}$, then the state returned by $N$ will be in $A$ if the input is at least get accepted by $N_1$ or rejected by $N_2$, which means the input have an odd number of 0s or do not contain the substring 101



<div style="page-break-after: always;"></div>

### **Part b**:

Set NFA $N_{2\or3}=(\Sigma,Q,s,A,\delta)$:
$$
N_{2\or3}=\left\{
\begin{array}{l}
	\Sigma=\{0,1\}\\
	Q=\{(x,y,z)\mid x,y,z\in\Z^+\}\\
	s= (0,0,0)\\
	A= \{(x,y,z)\mid (x,y,z)\in Q, y=0 \text{ or } z=0\}\\
	\delta((x,y,z),a)=
	\left\{
	\begin{array}{l}
		(2x+a, (2x+a)\text{ mod } 2, (2x+a)\text{ mod } 3) & \text{,if }a\in\Sigma\\
		(x, y) & \text{, if }a=\epsilon\\
	\end{array}
	\right.
\end{array}
\right.
$$
For arbitrary state $(q_i,q_j,q_k)\in Q$ returned by $N_{2\or3}$ with input $w$, $q_i$ represent the decimal value of $w$, $q_j=q_i \text{ mod } 2, q_k=q_i \text{ mod } 3 $. if the value of $w$ is divisible by $2$ or $3$, then at least one of $q_j$ and $q_k$ should be 0. Thus all state with $q_j=0$ or $q_k=0$ are the accept state. If the input is $\epsilon, \delta(s,\epsilon)=s=(0,0,0)\in A$, since 0 is divisible by any whole number.



<div style="page-break-after: always;"></div>

### **Part c**:

<img src="https://github.com/WilliamYKZ/Picture/raw/main/Picture/pc%20(1).png" alt="6" style="zoom:67%;" />

We construct the NFA shown above that accept the regular expression. The start state can accept $1^*$, and go to state $q1,q3,q5$ with input $0,1,\epsilon$. State $q1,q2$ and $q3,q4$ are used to detect $01^*$ and $11$  separately. Once $q2, q4$ receive $0$, the string contains $(01^*0)$ or $(110)$. State $q5$ is used to detect $(\epsilon 0)$ pattern in the input. State $q6$ is "unaccepted" state, any un-expected input that broke the pattern given by regular expression will lead to $q6$



<div style="page-break-after: always;"></div>

### **Part d**:

Set $NFA=(\Sigma,Q,s,A,\delta)$ 
$$
\left\{
\begin{array}{ll}
\Sigma=\{0,1\} \\
Q = \{(x,y,z)\mid x,y\in\Z^+\cup\{0\}, z\in\{0,1\}\} \\
A = \{(x,y,z)\mid (x,y,z)\in Q, x=y\}\\
s = (0,0,0)\\
\delta((x,y,z),b)=
\left\{
\begin{array}{ll}
\{(x+1,y,0),(x,y+1,1),(x,y,z)\}&\text{ if } b=0\text{ and } z=0\\
\{(x,y+1,1),(x,y,1)\}&\text{ if } b=0\text{ and } z=1\\
\{(m,0,1)\mid \forall m\in \Z\cap[0,x+y]\} &\text{ if } b=1\text{ and } z=0\\
\{(m,0,1)\mid \forall m\in \Z\cap[0,x]\} &\text{ if } b=1\text{ and } z=1\\
\end{array}
\right.
\end{array}
\right.
$$
For arbitrary state $(x,y,z)\in Q$, $x$ is the number of $0$ we assume as the prefix of the string, $y$ is the number of $0$ we assume as the suffix of the string. So such a state assume that we can represent the input as $0^x(0+1)^* 0^y$. if current state assume it has not met $(0+1)^*$ part (or have not get $1$ as input), then $z=0$, otherwise $z=1$. A state will be  accepting state if $x=y$, which means the given string can be written as $0^x(0+1)^* 0^y$ and $x=y=a$ (equals to $a$ if $a$ is a constant) 

In the transition function, if we have not process $(0+1)^*$ in the input, we assume each $0$ can belongs to either prefix or suffix, or $0$ are included in $(0+1)^*$. Thus the resulting state will be $(x+1,y,0),(x,y+1,1),(x,y,z)$. 

If we received $1$ or assumed that the past input was included in $(0+1)^*$, then we can only count $0$ to y, or we can assume $0$ is also in $(0+1)^*$

if we received $1$ for the first time ($z=0$), then we should set $x$ be a set of value in range $[0,x+y]$ and zero out $y$ because we should calculate $y$ after $(0+1)^*$ pattern, and all suffix length calculated before $(0+1)^*$ can be counted as the length of prefix.

if we keep receiving 1, we will keep $y$ as zero, and re-distribute x value



<div style="page-break-after: always;"></div>

## Question 2

### Part(a) 

Consider a NFA accept double(L) $M^{\prime}=\left(Q^{\prime}, s^{\prime}, A^{\prime}, \delta^{\prime}\right)$, where it includes a special state $s^{\prime\prime}$ with $\varepsilon-$transitions to every start states of $M$. and $M^\prime$ includes a new accepting state $a^{\prime\prime}$, and the origional state read an input $1$ to reach $a^{\prime\prime}$.

- $Q^{\prime}=Q \cup\left\{s^{\prime \prime}\right\} \cup\left\{a^{\prime \prime}\right\}$
- $S^{\prime}=\{\delta(s, a) \mid a \in \Sigma\}$
- $A^{\prime}=\left\{a^{\prime \prime}\right\}$
- $\delta^{\prime}\left(s^{\prime \prime}, \varepsilon\right)=\{\delta(s, a) \mid a \in \Sigma\}$
- $\delta^{\prime}\left(s^{\prime \prime}, a\right)=\varnothing$, when $\forall a \in \Sigma$
- $\delta^{\prime}(p, \varepsilon)=\varnothing$, when $\forall p\in Q$
- $\delta^{\prime}(p, a)=\delta(\delta(p, a), a)$, when $\forall p \in Q \and a\in \Sigma$
- $\delta^{\prime}(a, 0)=a^{\prime \prime}$,  $\forall a \in A$
- $\delta^{\prime}(a, \varepsilon)=\varnothing$, $\forall a \in A$
- $\delta^{\prime}(a, 1)=\varnothing$, $\forall a\in A$

Since the NFA we construct $M^\prime$ accepts double(L), then we can conclude double(L) is regular. 

<div style="page-break-after: always;"></div>

### Part(b)

Consider a NFA accepts $L_b$, $M^{\prime}=\left(Q^{\prime}, s^{\prime}, A^{\prime}, \delta^{\prime}\right)$ and $M^\prime$ includes a special state $s^{\prime\prime}$ with $\varepsilon-$ transitions to every double of the form $(s,s)$.

- $Q^{\prime}=\{Q \times Q\} \cup\left\{s^{\prime \prime}\right\}$
- $s^{\prime}=(s, s)$
- $A^{\prime}=A \times A$
- $\delta^{\prime}\left(s^{\prime \prime}, \varepsilon\right)=(s, s)$
- $\delta^{\prime}\left(s^{\prime \prime}, a\right)=\varnothing$, $\forall a \in \Sigma$
- $\delta^{\prime}((p, q), \varepsilon)=\varnothing$, $\forall p,q\in L$
- $\delta^{\prime}((p, q), 1)=(\delta(p, 1), \delta(q, 0)) \quad \forall p, q \in L$
- $\delta^{\prime}((p, q), 1)=(\delta(p, 0), \delta(q, 1))$, $\forall p,q\in L$
- $\delta^{\prime}((p, q), 0)=(\delta(p, 1), \delta(q, 1))$, $\forall p,q\in L$
- $\delta^{\prime}((p, q), 0)=(\delta(p, 0), \delta(q, 0))$, $\forall p,q\in L$

Since the NFA $M^\prime$ accepts $L_b$, then we can conlcude $L_b$ is regular.

<div style="page-break-after: always;"></div>

### Part(c)

Consider a NFA accepts $L_c$, $$M^{\prime}=\left(Q^{\prime}, s^{\prime}, A^{\prime}, \delta^{\prime}\right)$$ And $M^\prime$ includes a special state $s^{\prime\prime}$ with $\varepsilon-$ transitions to every start states of $M$.

- $Q^{\prime}=Q$
- $s^{\prime}=s$
- $A^{\prime}=A$
- $\delta^{\prime}(q, a)=\delta(q, a) \quad \forall q \in Q, a \in \Sigma$
- $\delta^{\prime}(q, 1)=\delta(\delta(q, 1), a) \quad \forall q \in Q, a \in \Sigma$
- $\delta^{\prime}(q, a)=\delta(q, 1) \quad \forall q \in Q, a \in \Sigma$

Since the NFA $M^\prime $ accepts $L_c$ then $L_c$ is regular. 



<div style="page-break-after: always;"></div>

## Question 3

### Part(a,b)

![](https://github.com/WilliamYKZ/Picture/raw/main/Picture/Screen%20Shot%202022-09-19%20at%2002.37.20%20AM.png)

<div style="page-break-after: always;"></div>

### Part c

![](https://github.com/WilliamYKZ/Picture/raw/main/Picture/Screen%20Shot%202022-09-19%20at%2002.37.25%20AM.png)

<div style="page-break-after: always;"></div>

### Part(d)

