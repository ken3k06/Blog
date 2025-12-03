
## Introduction 

The resultant of $f(x)$ and $g(x)$ is a value which is zero if and only if $f$ and $g$ have a root in common, in the algebraic closure of the field being discussed. 
This can be used to determine whether $f$ has repeated roots or not, by calculating the resultant of $f(x)$ and $f'(x)$. 
The resultant of $f(x)$ and $f'(x)$ is called the discriminant of $f(x)$. 
The discriminant is important in its own right in algebraic geometry, because when it equals zero, the polynomial has a repeated root and is in some way "degenerate". For example, the discriminant of $ax^2+bx+c$ is $b^2-4ac$. We have known that if $b^2-4ac=0$ then the quadratic equation has a double roots.

The main applications of resultant are to solve systems of polynomial equations, to determine whether or not solutions exist, or to reduce a given system to one with fewer variables and fewer equations. 

The input of our problem should be something like this: 
$$
\begin{array}{l}
f_{1}( x_{1} ,...,x_{n}) =0\\
\vdots \\
f_{m}( x_{1} ,...,x_{n}) =0
\end{array}
$$
That is, a system of polynomial equations in $n$ variables and each equation has an associated degree $d_i \geq 1$. Recall that $f_i(x_1,...,x_n)$ has degree $d_i$ if all monomials $x_1^{e_1}x_2^{e_2}...x_n^{e_n}$ appearing in $f_i$ have $\sum_{i}^ne_i\leq d_i$ and at least one monomial has $\sum_{i}^{n}e_i = d_i$. 

For the output, there are two essentially different cases:

**CASE 1:** $m>n$ (overdetermined) This is the case where we have more equations than unknowns, and where we generally expect to have no solutions. The resultant will be a system of equations (one equation when $m=n+1$) in the symbolic coefficients of the $f_i$ that has the following property:  when we substitute the specific numerical coefficients of the $f_i$ we will get zero in every equation in the resultant system if and only if the original overdetermined system has a solution.
**CASE 2:** $m\leq n$  (exact and underdetermined) In this case the number of equations is less than or equal to the number of variables, and we expect to have solutions.  In fact, if we allow complex solutions and solutions at infinity we are guaranteed to have solutions.

The first major distinction in methods based on the number of variables $n$. The case $n=1$ of a single variable and the multivariate case where $n \geq 2$. 


## Resultants of Univariate Polynomials 

Given two positive integers $\displaystyle r,s\geqslant 1$ and two polynomials in one variable
$$
\begin{equation*}
f( x) =a_{r} x^{r} +...+a_{1} x+a_{0} ,\ g( x) =b_{s} x^{s} +...+b_{1} x+b_{0}
\end{equation*}
$$
of degree less than or equal to $\displaystyle r$ and $\displaystyle s$ respectively, we define their resultant $\displaystyle R_{r,s}( f,g)$ by Slyvester's formula 

$$
\begin{equation*}
R_{r,s}( f,g) =\det\begin{pmatrix}
a_{0} & a_{1} & \dotsc  & \dotsc  & a_{r} & 0 & \dotsc  &  & 0\\
0 & a_{0} & a_{1} & \dotsc  & \dotsc  & a_{r} & 0 & \dotsc  & 0\\
\vdots  &  &  &  &  &  &  &  & \\
0 & 0 & \dotsc  & 0 & a_{0} & a_{1} & \dotsc  &  & a_{r}\\
b_{0} & b_{1} & \dotsc  &  & b_{s-1} & b_{s} &  &  & \\
0 & b_{0} & b_{1} & \dotsc  &  &  & b_{s} & 0 & \dotsc \\
\vdots  &  &  &  &  &  &  & \vdots  & \\
0 & \dotsc  & \dotsc  & 0 & 0 & b_{0} & \dotsc  &  & b_{s}
\end{pmatrix}
\end{equation*}
$$
Example: 

```python
from sage.all import *

R.<t> = PolynomialRing(ZZ)
f = R.random_element(degree=5, monic=True)
g = R.random_element(degree=6, monic=True)
print("f =", f)
print("g =", g)
r = f.degree()
s = g.degree()
a = f.list()
b = g.list()
M = matrix(ZZ, r + s, r + s)
for i in range(s):
    row = [0]*i + a + (s-i-1)*[0]
    r_ = vector(ZZ,row)
    M[i,:] = r_
for j in range(r):
    row = [0]*j + b + (r-j-1)*[0]
    r_ = vector(ZZ,row)
    M[s+j, :] = r_
print(M.det())
print(f.resultant(g))
```

Some basic properties of the resultant $R_{r,s}(f,g)$:
- $R_{r,s}(f,g) = a_r^{s}b_s^{r}\prod_{i,j}(x_i-y_j)$ where $x_1,...,x_r$ are the roots of $f$ and $y_1,...,y_s$ are the roots of $g$.
- Let $R_{r,s}(f,g) \in \mathbb{Z}[a_0,...,a_r,b_0,...,b_s]$ then $R_{r,s}(f,g)$ is irreducible, i.e the resultant is an irreducible polynomial with integer coefficients in $(r+1)(s+1)$ variables.
- Symmetry: $R_{r,s}(f,g)=(-1)^{rs}R_{s,r}(g,f)$ 
- Factorization: $R_{r_1+r_2,s}(f_1f_2,g)=R_{r_1,s}(f_1,g)R_{r_2,s}(f_2,g)$  
Thus, if the polynomials we are taking the resultant of can be factored, then the resultant can be factored too.