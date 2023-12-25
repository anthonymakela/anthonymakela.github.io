---
layout: post
title: "Invariant Polynomials"
categories: [Algebra]
published: false
mathjax: true
---

I'm finally done with the talk regarding the Bochner Technique. I was planning on writing about the actual result we proved, but it turned out to be such an analytic mess that I don't think any of the readers here would find reading about it enjoyable. Instead, I'll begin with a journey toward something called <b>Characteristic Classes</b>.

To set the stage we need to begin by discussing polynomials. Not just any polynomials, but a special class of polynomials called <b>Invariant Polynomials</b>. More specifically we are going to discuss invariant polynomials on $\mathfrak{gl}(n,F)$ where $F$ is a field. I'm not going to give you the punchline just yet on why we need such polynomials, but rest assured there is one.

Let's begin with the definition.

<div class="definition">
Let $A = [a_{ij}]$ be an $n \times n$ matrix with indeterminate entries $a_{ij}$. A polynomial $P(A)$ on $\mathfrak{gl}(n,F) = F^{n \times n}$ is an element of the commutative $F$-algebra $F[a_{ij}]$. A polynomial on $\mathfrak{gl}(n,F)$ is said to be <b>invariant</b> if
$$
P(XAX^{-1}) = P(A)
$$
is true for all $X \in \mathrm{GL}(n,F)$.
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
If $F$ is a infinite field of any characteristic, then a polynomial function $\widetilde{P}: F^n \to F$ is the zero function if and only if $P$ is the zero polynomial, that is the map 
$$
\operatorname{ev} : R[x_1,\dots,x_n] \to \mathrm{Fun}(R^n, R)
$$
is injective.
</div>

<div class="proof">
If $P$ is the zero polynomial, then $\operatorname{ev}(P)(a_1,\dots,a_n) = \widetilde{P}(a_1,\dots,a_n) = P(a_1,\dots,a_n) = 0$. To prove the converse we proceed by induction. For $n = 1$ suppose that $P(x)$ is a polynomial of degree $m$ such that $\widetilde{P}$ is the zero function. Since a nonzero polynomial of degree $m$ can have at most $m$ zeros, and $P(x)$ vanishes on  an infinite field, $P(x)$ must be the zero polynomial.

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

and let $P(A) = a_{11}a_{22} - a_{12}a_{21} = \det(A)$. For the invertible matrix given by

$$
X = \begin{pmatrix}1&1\\ 0&1\end{pmatrix}
$$

we have that

$$
\begin{align*}
XAX^{-1} = \begin{pmatrix} a_{11}+a_{21} & -a_{11}+a_{12}-a_{21}+a_{22} \\ a_{21} & -a_{21}+a_{22} \end{pmatrix}.
\end{align*}
$$

It follows that

$$
\begin{align*}
P(XAX^{-1}) &= (a_{11}+a_{21})(-a_{21}+a_{22}) - (-a_{11}+a_{12}-a_{21}+a_{22})(a_{21}) \\
&= a_{11}a_{22} - a_{12}a_{21} \\
&= P(A).
\end{align*}
$$

So we've found one matrix $X$ for which $P(XAX^{-1}) = P(A)$. If this would be to hold for all matrices $X$ in say $\mathrm{GL}(n, \Bbb C)$, then $P(A)$ would be invariant. It's a simple matter to verify this using the properties of the determinat as for any $X \in \mathrm{GL}(n, \Bbb C)$

$$
\begin{align*}
P(XAX^{-1}) &= \det\left(XAX^{-1}\right) \\
&= \det(X)\det(A)\det\left(X^{-1}\right) \\
&= \det(A) \\
&= P(A).
\end{align*}
$$

So $P(A)$ is indeed invariant. Another example is the trace $\operatorname{tr}(X)$. Note that each of the above examples follow directly from the proposition above. 



