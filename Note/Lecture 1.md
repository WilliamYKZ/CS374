# Lecture 1

## Basic Definition

1. Definition: An **algorithm** is a step-by-step way to slove a problem.



2. Definition: A problem is some question that we'd like answered given seom input. it should be decision problem of the form "Does a given input fulfill property X"



3. Definition: A **language** is a set of strings. Given a alphabet, $\Sigma$ a language is a subset of $\Sigma^*$ 

### Example

Now we have problem called multiplication. Define $L$ as language where inputs are separated by comma and output is separated by $|$.

Mechine accepts a $x*y=z$ if $x*y|z$ is in $L$.  Reject otherwise. 

The problem here is $x\cdot y = z$. And the language is $L=\{''1,1|1'', ''1,2|2'', ''2,1|2'' .....\}$ 

So if we have a multiplication questionlike $3*3$ we can find a substring $3,3|9$ in the language. 



4. Language help us to compare complexity of two question. we can compare language set to know the complexity. 





## String

1. A **alphabet** is a finite set of symbols.
   - $\Sigma = \{0,1\}$
   - $\Sigma=\{a, b, c, \ldots, z\}$
   - ASCII



2. Definition: A **String/Word** over $\Sigma$ is a **finite sequence** of symbols over $\Sigma$. For example, '0101001', 'string'



3. $x\cdot y = xy$ is the concatenation of two strings 



4. The **length** of a string $w$ (Denoted by $|w|$) is the number of symbols in $w$. For example $|101|=3, |\epsilon| = 0$



5. For integer $n\ge 0$, $\Sigma^n$ is set of all string over $\Sigma$ of length $n$.   $\Sigma ^*$ is the set of all strings over $\Sigma$.



6. $\Sigma^*$ set of all strings of all lengths including empry string. 



7. $\epsilon$ is a string containing no symbols. it is not a set.



8. $\{\epsilon \}$ is a set containing one string: the empty string. it is a set, not a string. 



9. $\empty$ is the empty set. it contains no strings. 



10. $\{\empty\}$ is the set with one elements which is empty set. $\{\{\}\}$





## Concatenation and Properties

1. Concatenation defined recursively: 
   - $xy=y$ if $x=\epsilon$
   - $xy=a(wy)$ if $x=aw$



2. Concatenation is associative $(uv)w = u(vw)$ hence write $uvw=(uv)w=u(vw)$.



3. not commutative: $uv$ not necessarily equal to $vu$.



4. The identity element is the empty string $\epsilon$:

$$
\epsilon u=u\epsilon =u
$$



## Substrings, Prefixed, Suffixes

1. Definition: $v$ is substring of $w$ $\Leftrightarrow$ there exist string $x,y$ such that $w=xvy$
   - If $X=\epsilon$ then $v$ is a prefix of $w$
   - If $Y=\epsilon$ then $v$ is a suffix of $w$



## Subsequence

1. A subsequence of a string $w[1...n]$ is either a subsequence of $w[2...n]$ or $w[1]$ followed by a subsequence of $w[2...n]$.

### Example 1

kapa is a subsequence of knapsack

### Example 2

How many subsequence are there in a string $|w|=5$

$2^5=32$ if there are no repeat element





## String Exponent

If w is a string then $w^n$ is defined inductively as follows:

- $w^n=\epsilon$ if $n=0$
- $w^n=ww^{n-1}$ if $n>0$

### Question

$(blah)^3=blahblahblah$



## Set Concatenation

Given two sets $X$ and $Y$ of string (over some common alphabet $\Sigma$) the concatenation of $X$ and $Y$ is 
$$
XY=\{xy|x\in X, y\in Y\}
$$

### Example

X={fido, rover,spot} Y={fluffy, tabby}

XY={fidofluffy, fidotabby, roverfluffy, rovertabby, spotfluffy, spottabby}





## Language

1. Definition: A **language** $L$ is a set of string over $\Sigma$. in other words $L\subseteq \Sigma^*$.
   - For language $A,B$ the concatenation of $A,B$ is $AB=\{xy|x\in A, y\in B\}$
   - For languages $A,B$ their union is $A\cup B$, intersection is $A\cap B$. and difference is $A \backslash B $.
   - For language $A\subseteq \Sigma^*$ the complement of $A$ is $\bar{A}=\Sigma^* \backslash A$.



## $\Sigma^*$ and language

1. $\Sigma ^n$ is the set of all strings of length $n$. Defined inductively: 
   - $\Sigma^n=\{\epsilon\}$ if $n=0$
   - $\Sigma^n=\Sigma \Sigma^{n-1}$ if $n>0$.



2. $\Sigma^* = \cup_{n\ge 0}\Sigma^n$ is the set of all finite length strings. 



3. $\Sigma^+ = \cup_{n\ge 1}\Sigma^n$ is the set of all non-empty strings. 





## Qeustion

1. What is $\empty ^0$

$\{\epsilon\}$

2. if $|L|=2$, then what is $|L^4|$

$|L^4|=16$

