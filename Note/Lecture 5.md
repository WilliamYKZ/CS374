# Lecture 5

## Pre-lecture Brain Teaser

Find the regular expressions for the following languages:

(1) All strings that end in $1011$

$(0+1)^*1011$

(2) All strings that contain $101$ or $010$ as a substring. 

$(0+1)^*(010+101)(0+1)^*$

(3) All strings that do not contain $111$ as a substring. 

$0^*((\varepsilon+1+11)^*0^+)^*$ 



## Basic 

1. Theorem: Languages accepted by DFA, NFA, and regular expressions are the same. 

   - DFAs are special cases of NFAs.

   - NFAs accept regular expressions 

   - DFAs accept languages accepted by NFAs

   - Regular expressions for languages accepted by DFAs



2. Thompson's Algorithm: Given two NFAs s and t:

![](https://github.com/WilliamYKZ/Picture/raw/main/Picture/Screen%20Shot%202022-09-22%20at%2002.04.15%20AM.png)





## Regular Expression to NFA

Let take a regular expression and convert it to a DFA. 

$(0+1)^*(101+010)(0+1)^*$

![](https://github.com/WilliamYKZ/Picture/raw/main/Picture/JPEG%20image-F700EBE5F3E4-1.jpeg)





## Another way to look at NFA

![](https://github.com/WilliamYKZ/Picture/raw/main/Picture/Screen%20Shot%202022-09-22%20at%2002.49.40%20AM.png)



Two graph are showing the same thing. Graph 1 is showing the what state is accepting the string, when string add one by one. 

Same as graph 2.



## Equivalence of NFAs and DFAs

1.  Theorem: For every NFA N there is a DFA M such that $L(M)=L(N)$. 
2. Remember, in the DFA you will have a unique pass of the accepting string. but NFA will have many paths. 
3. We can see each term in last graph of NFA as a state in DFA.

![](https://github.com/WilliamYKZ/Picture/raw/main/Picture/Screen%20Shot%202022-09-22%20at%2003.08.25%20AM.png)



4. NFA $N=(Q,\Sigma,s,\delta,A)$. We create a DFA $D=\left(Q^{\prime}, \Sigma, \delta^{\prime}, s^{\prime}, A^{\prime}\right)$. 

- $Q^\prime = \{\mathcal{P}(Q)\}$
- $s^\prime = \epsilon reach (s)=\delta^*(s,\varepsilon)$. 
- $A^\prime = \{X\subseteq Q\mid X\cap A\neq \empty\}$
- $\delta^\prime(X,a) = \bigcup_{q\in X}\delta^*(q,a)$.



## Converting NFAs to Regular Expression. 

![](https://github.com/WilliamYKZ/Picture/raw/main/Picture/JPEG%20image-169E58B94E03-1.jpeg)