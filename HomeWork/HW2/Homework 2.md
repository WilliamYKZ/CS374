# Homework 2

## Question 1:

Given $w\in \Sigma^*$, we can represent the number in the first row of $w$ as $w_{up}$, the number of the second row as $w_{dw}$. Then we can define D as $\forall w\in D, $  $w_{up}>w_{dw}$ (**Def of D**)  

To show D is regular, we can construct an DFA $M=(\Sigma,Q,s,A,\delta)$ that accept strings in D.
$$
\begin{array}{l}
\Sigma = \{
\left[ \begin{array}{c} 0\\0 \end{array} \right],
\left[ \begin{array}{c} 0\\1 \end{array} \right],
\left[ \begin{array}{c} 1\\0 \end{array} \right],
\left[ \begin{array}{c} 1\\1 \end{array} \right]
\}\\
Q=\{q|q\in\R\}\\
A=\{q\in Q | q>0 \}\\
s=0\\
\delta:\Sigma\to\R,\\
\delta(a)=a_{up}-a_{dw}=
\left\{
\begin{array}{c}  
	1 & \text{,if a=} \left[ \begin{array}{c} 1\\0 \end{array} \right]\\
	-1 & \text{,if a=} \left[ \begin{array}{c} 0\\1 \end{array} \right]\\
	0   & \text{,otherwise}
\end{array}\right.\\
\end{array}
$$
We use $w[i]$ to represent the $i$-th digit in $w$, counting from left to right. Since we need to compare two rows' value digit by digit, and the $i$-th digit is 2 times larger than the $(i+1)$-th digit, we construct our extended transition function as:
$$
\delta^*(w)=
\left\{
\begin{array}{ll}  
	2^{|x|}(\delta(a))+\delta^*(x) & \text{,if }w=a\cdot x\\
	0 & \text{,if }w=\epsilon\\
\end{array}\right.\\
$$
Since any binary number $a_1a_2...a_n=\sum_i 2^{n-i}a_i$ (we denote this summation as **Bi_sum**), and $\sum_{i=1}^{|\epsilon|}x=\sum_{i=1}^0x=0$ (one of properties of summation), we can merge and fully expand $\delta^*(w)$ as:
$$
\delta^*(w)=
\sum_{i=1}^{|w|}2^{|w|-i}(\delta(w[i]))
$$
Proof $\forall w\in\Sigma^*, \delta^*(w)\in A\iff w\in D$  

- $\Rightarrow$ $\delta^*(w)\in A$. Then we have:
  $$
  \begin{array}{rl}
  	\delta^*(w)&=\sum_{i=1}^{|w|}2^{|w|-i}(\delta(w[i])) & \text{Def of }\delta^*\\
      &=\sum_{i=1}^{|w|}2^{|w|-i}(w[i]_{up}-w[i]_{dw}) & \text{Def of }\delta\\
      &=\sum_{i=1}^{|w|}2^{|w|-i}(w[i]_{up})-\sum_{i=1}^{|w|}2^{|w|-i}(w[i]_{dw})&\text{Sumation Property} \\
      &=w_{up}-w_{dw}& \text{Def of Bi\_sum}\\\\
      \delta^*(w)\in A &\Rightarrow (w_{up}-w_{dw})>0 & \text{Def of A}\\
      &\Rightarrow w_{up}>w_{dw}\\
      &\Rightarrow w\in D& \text{Def of D}
  \end{array}
  $$
  Thus if $\delta^*(w)\in A\Rightarrow w\in D$

- $\Leftarrow w\in D$:
  $$
  \begin{array}{rl}
  	w\in D&\Rightarrow w_{up}>w_{dw}& \text{Def of D}\\
      &\Rightarrow w_{up}-w_{dw}>0\\
      &\Rightarrow \sum_{i=1}^{|w|}2^{|w|-i}(w[i]_{up})-\sum_{i=1}^{|w|}2^{|w|-i}(w[i]_{dw})>0 & \text{Def of Bi\_sum}\\
      &\Rightarrow\sum_{i=1}^{|w|}2^{|w|-i}(w[i]_{up}-w[i]_{dw})>0&\text{Sumation Property}\\
      &\Rightarrow\sum_{i=1}^{|w|}2^{|w|-i}(\delta(w[i]))>0 & \text{Def of }\delta\\
  	&\Rightarrow\delta^*(w)>0 & \text{Def of }\delta^*\\
  	&\Rightarrow\delta^*(w)\in A&\text{Def of A}
   	
  \end{array}
  $$
   Thus it is true that $w\in D\Rightarrow \delta^*(w)\in A$

Therefore, it is true that $\forall w\in\Sigma^*, \delta^*(w)\in A\iff w\in D$. So D can be accepted by DFA $M=(\Sigma,Q,s,A,\delta)$. According to Kleene’s Theorem, D is regular.



<div style="page-break-after: always;"></div>

## Question 2

- **Part a**:

  We use $(w, s)$ to represent the current output string $w$ and current state $s$, the new output character will be added to the right side of $w$. The character shown above the arrow is input character, the transition rule applied to the input is shown below the arrow. Then we can have: 

  - input **aaca**:
    $$
    (\epsilon,n_0)\xrightarrow[a:b]{a}(b,n_0)\xrightarrow[a:b]{a}(bb,n_0)\xrightarrow[c:a]{c}(bba,n_1)\xrightarrow[a:a]{a}(bbaa,n_1)
    $$

  - input **cbbc**:
    $$
    (\epsilon,n_0)\xrightarrow[c:a]{c}(a,n_1)\xrightarrow[b:b]{b}(ab,n_0)\xrightarrow[b:c]{b}(abc,n_0)\xrightarrow[c:a]{c}(abca,n_1)
    $$

  - input **bcba**:
    $$
    (\epsilon,n_0)\xrightarrow[b:c]{b}(c,n_0)\xrightarrow[c:a]{c}(ca,n_1)\xrightarrow[b:b]{b}(cab,n_0)\xrightarrow[a:b]{a}(cabb,n_0)
    $$

  - input **acbbca**:
    $$
    (\epsilon,n_0)\xrightarrow[a:b]{a}(b,n_0)\xrightarrow[c:a]{c}(ba,n_1)\xrightarrow[b:b]{b}(bab,n_0)\xrightarrow[b:c]{b}(babc,n_0)\xrightarrow[c:a]{c}(babca,n_1)\xrightarrow[a:a]{a}(babcaa,n_1)
    $$

<div style="page-break-after: always;"></div>

- **Part b**:
  $$
  \begin{array}{l}
  	FST_1=(\Sigma_1,\Gamma_1,Q_1,s,\delta_1)\\\\
  	\left\{
  	\begin{array}{l}
  	\Sigma_1:\text{ input alphabet}\\
  	\Gamma_1:\text{ output alphabet}\\
  	Q_1:\text{ set of states }\\
  	s:\text{ starting state, }s\in Q\\
  	\delta_1:Q_1\times\Sigma_1 \to Q_1\times\Gamma_1 \\
  	\end{array}
  	\right.
  \end{array}
  $$



<div style="page-break-after: always;"></div>

- **Part c**:

  For $FST_0$, we set the input alphabet as $\Sigma_0$, output alphabet as $\Gamma_0$, set of state as $Q_0$, the initial state as $s$
  $$
  \begin{array}{l}
  	FST_0=(\Sigma_0,\Gamma_0,Q_0,s,\delta_0)\\\\
  	\Rightarrow
  	\left\{
  	\begin{array}{l}
  	\Sigma_0=\{a,b,c\}\\
  	\Gamma_0=\{a,b,c\}\\
  	Q_0=\{n_0,n_1\}\\
  	s=n_0\\
  	\delta_0:Q_0\times\Sigma_0 \to Q_0\times\Gamma_0 \\
  	\delta_0(q,x)=
  	\left\{
  	\begin{array}{ccc}
  		(n_0,b) & \text{, if }(q,x)=(n_0, a)\\
  		(n_0,c) & \text{, if }(q,x)=(n_0, b)\\
  		(n_1,a) & \text{, if }(q,x)=(n_0, c)\\
  		(n_1,a) & \text{, if }(q,x)=(n_1, a)\\
  		(n_1,c) & \text{, if }(q,x)=(n_1, c)\\
  		(n_0,b) & \text{, if }(q,x)=(n_1, b)\\
  	\end{array}
  	\right.
  	\end{array}
  	\right.
  \end{array}
  $$



<div style="page-break-after: always;"></div>

-  **Part d:**

![](/Users/williamyan/Desktop/Screen Shot 2022-09-12 at 00.28.38 AM.png)

​	



<div style="page-break-after: always;"></div>

## Question 3

- **Part a:**

![](/Users/williamyan/Desktop/Screen Shot 2022-09-12 at 00.31.27 AM.png)

Because the length of $w$ and $w^R$ are the same, and we can start from the start state of $M$ and the accepting state of $M$ simultaneously to find the middle state of $M$. Thus, we use the cross product of two states in $M$ as the states in $M^\prime$. The start state of the first state of $Q^\prime $ is the start state of $M$ and it goes to the middle state of $M$. And the start state of the second state of $Q^\prime$ is the accepting state of $M$ and it goes to the middle state as well. The cross product of the two same middle states is the accepting state of $M^\prime$.

<div style="page-break-after: always;"></div>

- **Part b:**

![](/Users/williamyan/Desktop/Screen Shot 2022-09-12 at 00.31.56 AM.png)

To distinguish $x$ and $y$, we need to the break point between them, and $h$ is the break point. And then we need to switch their positions. After that, the start state and end state of $M’$ are both the break point. Then, the break point of $M’$ is from the accepting state of $M$ to the start state of $M$. Thus, for the transition function, when we find the accepting state of $M$, we need to take a free step to reach the start state of $M$. That’s how yx becomes $xy$.

<div style="page-break-after: always;"></div>



- **Part c:**

![](/Users/williamyan/Desktop/Screen Shot 2022-09-12 at 02.02.50 AM.png)

To use the subsequence in $M’$ to simulate the full input in $M$, we need to skip some characters. Thus, we have transition function $\delta’(q, \varepsilon) = \delta(q, a)$, then we can have free steps to skip some characters.