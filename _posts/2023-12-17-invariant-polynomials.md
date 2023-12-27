---
layout: post
title: "Invariant Polynomials"
categories: [Algebra]
mathjax: true
---

I'm finally done with the talk regarding the Bochner Technique. I was planning on writing about the actual result we proved, but it turned out to be such an analytic mess that I don't think any of the readers here would find reading about it enjoyable. Instead, I'll begin with a journey toward something called <b>Characteristic Classes</b>.

To set the stage we need to begin by discussing polynomials. Not just any polynomials, but a special class of polynomials called <b>Invariant Polynomials</b>. More specifically we are going to discuss invariant polynomials on $\mathfrak{gl}(n,F)$ where $F$ is a field. I'm not going to give you the punchline just yet on why we need such polynomials, but rest assured there is one.

Let's begin with the definition.

<div class="definition">
Let $A = [a_{ij}]$ be an $n \times n$ matrix with indeterminate entries $a_{ij}$. A polynomial $P(A)$ on $\mathfrak{gl}(n,F) = F^{n \times n}$ is an element of the commutative $F$-algebra $F[a_{ij}]$. A polynomial on $\mathfrak{gl}(n,F)$ is said to be <b>invariant</b> if
$$
P(X^{-1}AX) = P(A)
$$
is true for all $X \in \mathrm{GL}(n,F)$.
</div>

Before we dive into some examples let's first take a moment to understand a subtle difference between a polynomial and a polynomial function.

Let $R$ be a commutative ring with identity $1$. A <b>polynomial</b> in $n$ variables over $R$ is an element of the $R$-algebra $R[x_1,\dots,x_n]$. A polynomial $P(x) \in R[x_1,\dots,x_n]$ defines a function $\widetilde{P}: R^n \to R$ by evaluation. This means that we have a map

$$
\begin{align*}
\operatorname{ev} : R[x_1,\dots,x_n] &\to \mathrm{Fun}(R^n, R) \\
P &\longmapsto \widetilde{P}
\end{align*}
$$

where $\mathrm{Fun}(R^n, R)$ denotes the $R$-algebra of functions from $R^n$ to $R$. An element in the image of $\operatorname{ev}$ is then called a <b>polynomial function</b> over $R$.

<div class="proposition">
If $F$ is an infinite field of any characteristic, then a polynomial function $\widetilde{P}: F^n \to F$ is the zero function if and only if $P$ is the zero polynomial, that is the map 
$$
\operatorname{ev} : R[x_1,\dots,x_n] \to \mathrm{Fun}(R^n, R)
$$
is injective.
</div>

<div class="proof">
If $P$ is the zero polynomial, then $\operatorname{ev}(P)(a_1,\dots,a_n) = \widetilde{P}(a_1,\dots,a_n) = P(a_1,\dots,a_n) = 0$. To prove the converse we proceed by induction. For $n = 1$ suppose that $P(x)$ is a polynomial of degree $m$ such that $\widetilde{P}$ is the zero function. Since a nonzero polynomial of degree $m$ can have at most $m$ zeros, and $P(x)$ vanishes on an infinite field, $P(x)$ must be the zero polynomial.

We proceed by making the induction hypothesis that $\operatorname{ev}$ is injective when the number of variables is less than or equal to $n-1$. Let
$$
P(x_1,\dots,x_{n-1},x_n) = \sum_{k=0}^m P_k(x_1,\dots,x_{n-1})x^k_n.
$$
Fix $(a_1,\dots,a_{n-1}) \in F^{n-1}$, then $P(a_1,\dots,a_{n-1},x_n)$ is a polynomial in $x_n$ and $\widetilde{P}(a_1,\dots,a_{n-1},x_n)$ the zero function by assumption. The one-variable case yields that $P(a_1,\dots,a_{n-1},x_n)$ is the zero polynomial. It follows that each $P_k(a_1,\dots,a_{n-1})$ is zero and since $(a_1,\dots,a_{n-1})$ is an arbitary point of $F^{n-1}$, the polynomial function $\widetilde{P}_k$ is the zero function on $F^{n-1}$. It follows that $P(x_1,\dots,x_{n-1},x_n)$ is the zero polynomial.
</div>

The above proposition shows that for an infinite field $F$ we may identify the polynomial functions on $F^n$ with polynomials in $F[x_1,\dots,x_n]$.

---

Now for the examples. Let's start with one that you have probably met before. Consider the $2\times 2$ matrix 

$$
A = \begin{pmatrix}a_{11}&a_{12}\\ a_{21}&a_{22}\end{pmatrix}
$$

on $\mathfrak{gl}(2,\Bbb R)$ and let $P(A) = a_{11}a_{22} - a_{12}a_{21} = \det(A)$. For the invertible matrix given by

$$
X = \begin{pmatrix}1&1\\ 0&1\end{pmatrix}
$$

we have that

$$
\begin{align*}
X^{-1}AX = \begin{pmatrix} a_{11}-a_{21} & a_{11}-a_{21}+a_{12}-a_{22} \\ a_{21} & a_{21}+a_{22} \end{pmatrix}.
\end{align*}
$$

It follows that

$$
\begin{align*}
P(X^{-1}AX) &= (a_{11}-a_{21})(a_{21}+a_{22}) - (a_{11}-a_{12}+a_{21}-a_{22})(a_{21}) \\
&= a_{11}a_{22} - a_{12}a_{21} \\
&= P(A).
\end{align*}
$$

So we've found one matrix $X$ for which $P(XAX^{-1}) = P(A)$. If this would be to hold for all matrices $X$ in say $\mathrm{GL}(n, \Bbb R)$, then $P(A)$ would be invariant. It's a simple matter to verify this using the properties of the determinant as for any $X \in \mathrm{GL}(n, \Bbb R)$

$$
\begin{align*}
P(X^{-1}AX) &= \det\left(X^{-1}AX\right) \\
&= \det(X^{-1})\det(A)\det\left(X\right) \\
&= \det(A) \\
&= P(A).
\end{align*}
$$

So $P(A)$ is indeed invariant. Another example is the trace $\operatorname{tr}(A)$. Note that each of the above examples follows directly from the proposition above since each of them holds for $n \times n$ matrices of real numbers.


Another interesting example of invariant polynomials is <b>coefficients of the characteristic polynomial</b> $\det(\lambda I + A)$ of $-A$. If $A = [a_{ij}]$ is an $n \times n$ matrix of indeterminates and $\lambda$ is another indeterminate, then the coefficients $f_k(A)$ of $\lambda^{n-k}$ in

$$
\det(\lambda I + A) = \lambda^n + f_1(A)\lambda^{n-1} + \dots f_{n-1}(A)\lambda + f_{n}(X)
$$

are polynomials on $\mathfrak{gl}(n,\Bbb R)$. Notice that for any $X \in \mathrm{GL}(n,\Bbb R)$ we have that

$$
\det(X^{-1}(\lambda I + A)X)  = \det(\lambda I + A).
$$

Comparing the coefficients of $\lambda^{n-k}$ we get that $f_k(X^{-1}AX) = f_k(A)$ which yields by our proposition above that $f_k(A)$'s are all invariant polynomials on $\mathfrak{gl}(n,\Bbb R)$.

Lastly we consider the <b>trace polynoimals</b> defined by $\sum_k X = \operatorname{tr}(A^k)$. Now as $\operatorname{tr}(A) = f_1(A)$ we have that

$$
\sum_k(X^{-1}AX) = \operatorname{tr}(X^{-1}A^kX) = \operatorname{tr}(A^k) = \sum_k A.
$$

---

Before we wrap this up let's turn our attention to the special case when $F = \Bbb C$. Suppose that $A \in \mathfrak{gl}(n, \Bbb C)$ is a diagonalizable matrix with complex entries. Since $A$ is diagonalizable, there exists a nonsingular $X \in \mathrm{GL}(n,\Bbb C)$ such that

$$
X^{-1}AX = \operatorname{diag}(\lambda_1,\dots,\lambda_n)
$$

where the $\lambda$'s are now the eigenvalues of $A$. Since the trace and determinant of such matrix are the sum and product of the eigenvalues respectively it follows that both can be expressed as symmetric polynomials of their eigenvalues.

This example hints at the fact that there might be a correspondence between the algebra $\mathrm{Inv}(\mathfrak{gl}(n,\Bbb C))$ of all invariant complex polynomials on $\mathfrak{gl}(n,\Bbb C)$ and $\Bbb C[\lambda_1,\dots,\lambda_n]^{S_n}$, the algebra of complex symmetric polynomials in $\lambda_1,\dots,\lambda_n$. To an invariant polynomial $P(A) \in \mathrm{Inv}(\mathfrak{gl}(n,\Bbb C))$ we can associate the polynomial

$$
\widetilde{P}(\lambda_1,\dots,\lambda_n) = P(\operatorname{diag}(\lambda_1,\dots,\lambda_n)).
$$

If $\sigma \in S_n$ is a permutation of $\\{1,\dots,n\\}$, the permutation matrix $P_\sigma \in \mathrm{GL}(n,\Bbb Z)$ is the matrix whose $(i,\sigma(i))$-entry is $1$ and $0$ otherwise. For example the permutation 

$$
\sigma ={\begin{pmatrix}1&2&3&4&5\\1&4&2&5&3\end{pmatrix}}
$$

yields the following permutation matrix

$$
P_\sigma = \begin{pmatrix}1&0&0&0&0\\0&0&0&1&0\\0&1&0&0&0\\0&0&0&0&1\\0&0&1&0&0\end{pmatrix}.
$$

It follows that conjugating $\operatorname{diag}(\lambda_1,\dots,\lambda_n)$ by the transposition matrix $P_{(ij)}$ corresponds to swapping $\lambda_i$ and $\lambda_j$ in $\operatorname{diag}(\lambda_1,\dots,\lambda_n)$. Using products of transposition matrices we can get any ordering of $\lambda_1,\dots,\lambda_n$ and therefore $\widetilde{P}(\lambda_1,\dots,\lambda_n)$ is invariant under all permutations of $\lambda_1,\dots,\lambda_n$ i.e. $\widetilde{P}(\lambda_1,\dots,\lambda_n)$ is symmetric in $\lambda_1,\dots,\lambda_n$.

<div class="theorem">
The map 

$$
\begin{align*}
\varphi : \mathrm{Inv}(\mathfrak{gl}(n,\Bbb C)) &\to \Bbb C[\lambda_1,\dots,\lambda_n]^{S_n} \\
P(A) &\longmapsto \widetilde{P}(\lambda_1,\dots,\lambda_n)
\end{align*}
$$

given by restricting an invariant polynomial $P(A)$ to the diagonal matrix $\operatorname{diag}(\lambda_1,\dots,\lambda_n)$ is an isomorphism of algebras over $\Bbb C$.
</div>

<div class="proof">
Since $\Bbb C$ is infinite, polynomials can be identified with complex polynomial functions. Suppose that $P(A)$ vanishes on all diagonal matrices $A \in \mathfrak{gl}(n,\Bbb C)$. As $P(A)$ is invariant under conjugation, $P(A)$ vanishes on all diagonalizable matrices $A \in \mathfrak{gl}(n,\Bbb C)$. Since the subset of diagonalizable matrices is dense in $\mathfrak{gl}(n,\Bbb C)$, by continuity $P(A)$ vanishes on $\mathfrak{gl}(n,\Bbb C)$. It follows that $P(A)$ is the zero function and hence the zero polynomial on $\mathfrak{gl}(n,\Bbb C)$.

To see that $\varphi$ is surjective, note that the <b>elementary symmetric polynoimal</b> $\sigma_k(\lambda_1,\dots,\lambda_n)$ is the image of $f_k(A)$ under $\varphi$. By the fundamental theorem on symmetric polynomials, every element of $\Bbb C[\lambda_1,\dots,\lambda_n]^{S_n}$ is of the form $Q(\sigma_1,\dots,\sigma_n)$ for some polynomial $Q$. Then
$$
\begin{align*}
Q(\sigma_1,\dots,\sigma_n) &= Q(\varphi(f_1(A)),\dots,\varphi(f_n(A))) \\
&= \varphi(Q(f_1(A), \dots, f_n(A))) \\
&= \varphi(P(A))
\end{align*}
$$
where $P(A) = Q(f_1(A), \dots, f_n(A)) \in \mathrm{Inv}(\mathfrak{gl}(n,\Bbb C))$.
</div>

From here it's quite easy to see that the ring of invariant complex polynomials $\mathrm{Inv}(\mathfrak{gl}(n,\Bbb C))$ is generated as an algebra over $\Bbb C$ by the coefficients $f_i(A)$ of the characteristic polynomial $\det(\lambda I + A)$. That is 

$$
\mathrm{Inv}(\mathfrak{gl}(n,\Bbb C)) = \Bbb C[f_1(A),\dots,f_n(A)].
$$

This post was merely a technical tool we need to get to characteristic classes and follows quite heavily Appendix B from Tu Loring's book on Differential Geometry.