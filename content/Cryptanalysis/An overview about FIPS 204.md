## Mathematical Background

You can read my previous post on basic lattice methods and hard problems: [[Lattice Methods]]
In what follows, we review some more advanced topics before going deeper into these schemes.
**Disclaimer:** I’m not a mathematician, so there may be mistakes. If you spot any, please let me know so I can revise the article. Thank you!
### Ring 

Recall that a binary operation on a set $R$ is a function $* : R \times R \rightarrow R$, denote by $(r,r') \rightarrow r*r'$. 

**Ring**. A ring $R$ is a set with two binary operations $R \times R \rightarrow R$ : addition $(a,b)\rightarrow a+b$ and multiplication $(a,b) \rightarrow ab$, such that
- $R$ is an abelian group under addition
- Associativity: $a(bc) = (ab)c$ for every $a,b,c\in R$ 
- there is an element $1 \in R$ with $1a=a1=a$ for every $a \in R$
- Distributitvity: $a(b+c)=ab+ac$ and $(b+c)a=ba+ca$ for every $a,b,c\in R$ 
The element 1 in a ring $R$ is called one or the unit of $R$ or the identity of $R$. 
A subring $S$ of a ring $R$ is a ring contained in $R$ such that $S$ and $R$ have the same addition, multiplication and unit. 
**Definition.** A subset $S$ of a ring $R$ is a subring of $R$ if 
- $1 \in S$ 
- if $a,b \in S$ then $a-b \in S$ 
- if $a,b\in S$ then $ab \in S$ 

A ring $R$ is commutative if $ab=ba$ for all $a,b\in R$. 
The sets $\mathbb{Z}, \mathbb{Q},\mathbb{R}, \mathbb{C}$ are commutative rings with the usual addition and multiplication. From now on, all rings mentioned in this article are commutative rings. 

**Definition** A domain (often called an integral domain) is a commutative ring $R$ that satisfies two extra axioms: 
- $1 \neq 0$ 
- Cancellation law: for all $a,b,c\in R$, if $ca=cb$ and $c\neq 0$ then $a=b$
Once again, all $\mathbb{Z,Q,R,C}$  are domains;  elements $a,b \in R$ are called zero divisors if $ab=0$ and $a \neq 0, b\neq 0$ . Thus domains have no zero divisors.


**Example**: Prove that the commutative ring $\mathbb{Z}_{m}$ is a domain if and only if $m$ is prime
**Proof.** If $m$ is not prime, then $m = ab$ where $1<a,b<m$. Hence, both $[a]$ and $[b]$ are not zero in $\mathbb{Z}_m$. Where $[a]$ represent for the congruence class of the integer $a$ for modulo $m$. Hence, both $[a]$ and $[b]$ are not zero in $\mathbb{Z}_m$, yet $[a][b] = [m]=0$.
Conversely, if $m$ is prime and $[a][b]=[ab]=[0]$, where $[a],[b] \neq 0$ , then $m|ab$. From Euclid's lemma, we have $m|a$ or $m|b$, if, $m|a$, then $a=md$ and $[a]=[m][d]=[0]$ which is a contradiction. 

### Polynomials Ring 

We now carefully review the basic definitions of polynomials.

**Definition 1.** If $R$ is a commutative ring, then a formal power series over $R$ is sequence of elements $s_i \in R$ for all $i \geq 0$, called the coefficients of $\sigma$: 
$$
\sigma = (s_0,s_1,...,s_i,...)
$$
To determine whether two formal power series are equal or not, we will use the fact that a formal power series $\sigma$ is a sequence; that is, $\sigma$ is a function $\sigma : \mathbb{N} \rightarrow R$ where $\mathbb{N}$ is the set of natural numbers, with $\sigma(i)=s_i$. Thus if $\tau=(t_0,t_1,...,t_i,...)$ is a formal power series over $R$ then $\sigma=\tau$ is and only if $\sigma(i)=\tau(i), \forall i \geq 0$. 

**Definition 2.** A polynomial over a commutative ring $R$ is a formal power series $\sigma = (s_0,s_1,...,s_i,...)$ over $R$ for which there exists some integer $n \geq 0$ with $s_i=0$ for all $i>n$. That is: 
$$
\sigma = (s_0,s_1,...,s_n,0,0,...)
$$
A polynomial has only finitely many nonzero coefficients. The zero polynomial is a sequence where all elements equal to $0$. 
We also call $s_n$ the leading coefficient of $\sigma$ or the degree of $\sigma$ and denote by $n = \deg(\sigma)$.
If $s_n=1$ then $\sigma$ is called monic. 

Note: If $R$ is a commutative ring, then 
$$ 
R[[x]]
$$
denotes the set of all formal power series over $R$ where $R[x] \subseteq R[[x]]$ denotes the set of all polynomials over $R$. 

If $\sigma=(s_0,s_1,...,s_n,0,0,...) \in R[x]$ has degree $n$ then $\sigma = s_0+s_1x+...+s_nx^n$ and we shall use this notation from now on. 
Some lemma: Let $\sigma, \tau \in R[x]$ be nonzero polynomials 
1. Either $\sigma\tau = 0$ or $deg(\sigma\tau) \leq \deg(\sigma) + \deg(\tau)$ 
2. If R is a domain then $R[x]$ is a domain
3. If $R$ is a domain $\sigma,\tau \neq 0$ and $\tau | \sigma$ in $R[x]$ then $\deg(\tau) \leq \deg(\sigma)$ 
4. If $R$ is a domain then $\sigma\tau \neq 0$ and $\deg(\sigma\tau) = \deg(\sigma)+\deg(\tau)$ 

**Definition 3.** Let $k$ be a field. The fraction field $Frac(k[x])$ or $k[x]$ denoted by $k(x)$ is called the field of rational functions over $k$. 
Thus, if $k$ is a field, then the elements of $k(x)$ have the form $f(x)/g(x)$, where $f(x),g(x)\in k[x]$ and $g(x) \neq 0$.


### Quotient Rings

We are now going to mimic the construction of the commutative ring $\mathbb{Z}_m$ 
**Definition 1**. Let $I$ be an ideal in a commutative ring $R$. If $a \in R$ then the coset $a+I$ is the subset 
$$
a + I = \{a+i : i \in I\}
$$
The coset $a+I$ is often called $a \bmod I$. The family of all cosets is denoted by $R/I$: 
$$
R/I = \{a+I:a \in R\}
$$
Example: If $R= \mathbb{Z}, I = (m)$ and $a \in \mathbb{Z}$, we can show that the coset 
$$
a+I=a+(m)=\{a+km : k \in \mathbb{Z}\}
$$

### Polynomials Arithmetic 



## Computational Background

### Shortest Vector Problem (SVP)

### Bounded-Distance Decoding (BDD)




## SIS and LWE

Shortest Integer Solution and Learning with errors are consider hard problems on lattices




## Resources

[Module-Lattice-Based Digital Signature Standard](https://csrc.nist.gov/pubs/fips/204/final)
[Some Complexity Results and Bit Unpredictable for Short Vector Problem](https://eprint.iacr.org/2013/052.pdf)
[Solving Hard Lattice Problems and the Security of Lattice-Based Cryptosystems](https://eprint.iacr.org/2012/533.pdf)
[CRYSTALS-Dilithium/Algorithm Specifications and Supporting Documentation](https://pq-crystals.org/dilithium/data/dilithium-specification-round3-20210208.pdf)
[Algebraic isomorphic spaces of ideal lattices, reduction of Ring-SIS problem, and new reduction of Ring-LWE problem](https://eprint.iacr.org/2023/1412.pdf)
[Practical Implementation of Ring-SIS/LWE based Signature and IBE](https://langloi227.users.greyc.fr/webpage/18BFRS_author.pdf)
[The Complexity of the Shortest Vector Problem - Huck Bennett](https://eccc.weizmann.ac.il/report/2022/170/revision/1/download)
[The Hardness of LWE and Ring-LWE](https://eprint.iacr.org/2021/1358.pdf)
