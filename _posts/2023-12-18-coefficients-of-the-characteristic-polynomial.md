---
layout: post
title: "Coefficients and Characteristic Polynomials"
categories: [Algebra]
mathjax: true
excerpt_separator: <!--more-->
---

Last time in our discussion regarding invariant polynomials, I mentioned that the coefficients $f_k(A)$ of the characteristic polynomial of a matrix $A$ are sums of the principal $k \times k$ minors modulo signs. This post will be a short one, giving some justification for this claim.

<!--more-->

---

Before we prove the result I mentioned above, let's recall what is meant by the <b>Adjoint</b> or <b>Adjugate</b> of a matrix. Given an $n \times n$ matrix $A = [a^i_j]$, the $(i,j)$ cofactors $C^i_j$ defined by 

$$
C^i_j := (-1)^{i+j}M^i_j
$$

where $M^i_j$ is the $(i,j)$ minor of $A$, can be arranged into a matrix $C = [C^i_j]$ giving rise to the following definition.

<div class="definition">
The adjugate of an $n \times n$ matrix $A$ is defined by

$$
\operatorname{adj}(A)= C^T = \begin{pmatrix}C^1_1&C^2_1&\cdots &C^n_1\\C^1_2&C^2_2&\cdots &C^n_2\\\vdots &\vdots &\ddots &\vdots \\C^1_n&C^2_n&\cdots &C^n_n\end{pmatrix}.
$$

</div>

The adjugate satisfies some reasonable properties such as $\operatorname{adj}(cA) = c^{n-1}A$ for any scalar $c$, but the one we are mostly interested in today is something called <b>Jacobi's formula</b> which relates the derivative of the _determinant_ of a $A$ in terms of the adjugate of $A$ and the derivative of $A$.

<div class="theorem" text="(Jacobi's formula)">
If $A$ is a differentiable map from the real numbers to the $n \times n$ matrices, then

$$
\frac{d}{dt} \det A(t) = \operatorname{tr}\left(\operatorname{adj}(A(t))\frac{d A(t)}{dt}\right).
$$

</div>

---

The above formula will be extremely useful in proving the following fact about the coefficients of the characteristic polynomial $\det(t I - A)$.

<div class="proposition">
Let $A$ be an $n \times n$ matrix and denote by $E_k(A)$ the sum of $k \times k$ principal minors of $A.$ If $p_A(t) = \det(t I - A) = \sum_{k=0}^n f_k(A)t^{n-k}$, then the coefficient of $t^{k}$ is given by

$$
f_{n-k}(A) = (-1)^{n-k}E_{n-k}(A)
$$

for $k = 1,\dots, n$.
</div>

<div class="proof">
Note first that $f_{n-k}(A) = \frac{1}{k!}p^{(k)}_A(0)$. Using the Jacobi formula we obtain

$$
p'_A(t) = \operatorname{tr}(\operatorname{adj}(t I - A)).
$$

Observe now that $\operatorname{tr}(\operatorname{adj}(A))$ is exactly the sum of the principal minors of size $(n-1) \times (n-1)$ of $A$.

Evaluating the derivative at $t = 0$ yields

$$
\begin{align*}
f_{n-1}(A) &= p'_A(t)\vert_{t = 0} \\
&= \operatorname{tr}(\operatorname{adj}(t I - A))\vert_{t = 0} \\
&= \operatorname{tr}(\operatorname{adj}(- A)) \\
&= (-1)^{n-1}\operatorname{tr}(\operatorname{adj}(A)) \\
&=(-1)^{n-1}E_{n-1}(A).
\end{align*}
$$

Now, denoting the principal submatrices of $A$ of size $(n-1) \times (n-1)$ by $A_i$ we see that $\operatorname{tr}(\operatorname{adj}(t I - A)) = \sum_{i=1}^n p_{A_i}(t)$ since the $(i,i)$'th entry of $\operatorname{adj}(t I - A)$ is given by the determinant of the submatrix obtained by removing the $i$'th row and column from $t I - A$ which is exactly $p_{A_i}(t) = \det(t I - A_i)$.

Utilizing the Jacobi formula again, we get

$$
\begin{align*}
p''_A(t) &= \frac{d}{dt}\operatorname{tr}(\operatorname{adj}(t I - A)) \\
&= \frac{d}{dt}\sum_{i=1}^n p_{A_i}(t) \\
&= \sum_{i=1}^n \frac{d}{dt} p_{A_i}(t) \\
&= \sum_{i=1}^n\operatorname{tr}(\operatorname{adj}(t I - A_i)).
\end{align*}
$$


Each of the summands $\operatorname{tr}(\operatorname{adj}(t I - A_i))$ is the sum of the $n-1$ principal minors of size $(n-2) \times (n-2)$ of a principal minor of $\operatorname{tr}(\operatorname{adj}(t I - A))$, it follows that each of the $\binom{n}{n-2}$ principal minors of $t I - A$ of size $(n-2) \times (n-2)$ appears twice in the sum. This yields

$$
\begin{align*}
f_{n-2}(A) &= \frac{1}{2!}p''_A(t)\vert_{t = 0} \\
&= \frac{1}{2!} \sum_{i=1}^n\operatorname{tr}(\operatorname{adj}(t I - A_i))\vert_{t = 0} \\
&= \frac{1}{2!} \sum_{i=1}^n\operatorname{tr}(\operatorname{adj}(- A_i)) \\
&= \frac{1}{2!} (-1)^{n-2}\sum_{i=1}^n\operatorname{tr}(\operatorname{adj}(A_i)) \\
&= \frac{1}{2!} (-1)^{n-2}(2E_{n-2}(A)) \\
&= (-1)^{n-2}(E_{n-2}(A))
\end{align*}
$$

and repeating this yields the desired result.

</div>

---

The last argument in the above proof might be a bit cryptic, so here is an illustration of what's happening. Consider a $4 \times 4$ matrix $A$ given by

$$
A = \begin{pmatrix}
a^1_1 & a^1_2 & a^1_3 & a^1_4 \\
a^2_1 & a^2_2 & a^2_3 & a^2_4 \\
a^3_1 & a^3_2 & a^3_3 & a^3_4 \\
a^4_1 & a^4_2 & a^4_3 & a^4_4
\end{pmatrix}.
$$

The principal submatrices of size $3 \times 3$ are given by

$$
\begin{equation}
\begin{pmatrix}
a^2_2 & a^2_3 & a^2_4 \\
a^3_2 & a^3_3 & a^3_4 \\
a^4_2 & a^4_3 & a^4_4
\end{pmatrix} \quad
\begin{pmatrix}
a^1_1 & a^1_3 & a^1_4 \\
a^3_1 & a^3_3 & a^3_4 \\
a^4_1 & a^4_3 & a^4_4
\end{pmatrix} \quad
\begin{pmatrix}
a^1_1 & a^1_2 & a^1_4 \\
a^2_1 & a^2_2 & a^2_4 \\
a^4_1 & a^4_2 & a^4_4
\end{pmatrix} \quad
\begin{pmatrix}
a^1_1 & a^1_2 & a^1_3 \\
a^2_1 & a^2_2 & a^2_3 \\
a^3_1 & a^3_2 & a^3_3
\end{pmatrix}.
\end{equation}
$$


Looking at, for example $A_1$, the sum $\operatorname{tr}(\operatorname{adj}(A_1))$ is given by summing the $2 \times 2$ minors 

$$
{\color{ForestGreen}\begin{vmatrix}
a^3_3 & a^3_4 \\
a^4_3 & a^4_4 
\end{vmatrix}} \quad
{\color{Sepia}\begin{vmatrix}
a^2_2 & a^2_4 \\
a^4_2 & a^4_4 
\end{vmatrix}} \quad
{\color{RoyalBlue}\begin{vmatrix}
a^2_2 & a^2_3 \\
a^3_2 & a^3_3 
\end{vmatrix}}.
$$

For $A_2$ we sum over

$$
{\color{ForestGreen}\begin{vmatrix}
a^3_3 & a^3_4 \\
a^4_3 & a^4_4 
\end{vmatrix}} \quad
{\color{Mulberry}\begin{vmatrix}
a^1_1 & a^1_4 \\
a^4_1 & a^4_4 
\end{vmatrix}} \quad
{\color{ProcessBlue}\begin{vmatrix}
a^1_1 & a^1_3 \\
a^3_1 & a^3_3 
\end{vmatrix}}
$$

and for $A_3$

$$
{\color{Sepia}\begin{vmatrix}
a^2_2 & a^2_4 \\
a^4_2 & a^4_4 
\end{vmatrix}} \quad
{\color{Mulberry}\begin{vmatrix}
a^1_1 & a^1_4 \\
a^4_1 & a^4_4 
\end{vmatrix}} \quad
{\color{BurntOrange}\begin{vmatrix}
a^1_1 & a^1_2 \\
a^2_1 & a^2_2 
\end{vmatrix}}.
$$

Lastly, for the matrix $A_4$ we have

$$
{\color{RoyalBlue}\begin{vmatrix}
a^2_2 & a^2_3 \\
a^3_2 & a^3_3 
\end{vmatrix}} \quad
{\color{ProcessBlue}\begin{vmatrix}
a^1_1 & a^1_3 \\
a^3_1 & a^3_3 
\end{vmatrix}} \quad
{\color{BurntOrange}\begin{vmatrix}
a^1_1 & a^1_2 \\
a^2_1 & a^2_2 
\end{vmatrix}}.
$$

The reason this happens is that if we omit, say the $1$st and the $3$rd rows and columns of $A$ we obtain the minor

$$
  \begin{vmatrix}
a^2_2 & a^2_4 \\
a^4_2 & a^4_4 
\end{vmatrix}
$$

which shows up in the sum $\sum_{i=1}^n\operatorname{tr}(\operatorname{adj}(t I - A_i))$ first when $i = 1$ and for the second time when $i = 3$ as illustrated above. Similar reasoning shows that the $1 \times 1$ minors appear $6 = 3!$ times.

---

Before wrapping this up, I want to give a different viewpoint on the matter. The classical definition of the determinant for an $n \times n$ matrix $A$ is given by

$$
\det(A) = \sum_{\pi \in S_n} \operatorname{sgn}(\pi)a^1_{\pi(1)}\cdots a^n_{\pi(n)}.
$$

Now, there might be a time[^1] in your life when you would like to have an alternative description for this, and turns out there is one. The Levi-Civita symbol is defined by

$$
\varepsilon^{i_{1}i_{2}i_{3}\ldots i_{n}}={\begin{cases}+1&{\text{if }}(i_{1},i_{2},i_{3},\ldots,i_{n}){\text{ is an even permutation of }}(1,2,3,\dots ,n)\\-1&{\text{if }}(i_{1},i_{2},i_{3},\ldots ,i_{n}){\text{ is an odd permutation of }}(1,2,3,\dots ,n)\\\;\;\,0&{\text{otherwise}}\end{cases}}
$$

allows us to write

$$
\det(A) = \varepsilon^{i_{1}i_{2}i_{3}\ldots i_{n}}a^1_{i_1}\cdots a^n_{i_n}
$$

which has a whopping $n^n$ terms[^2] compared to the $n!$ from the classical definition, but at least we can use the Einstein summation here. Let's make this even worse and get rid of the explicit indices. We obtain

$$
\begin{align*}
\det(A) &= \frac{1}{n!}\varepsilon^{i_{1}i_{2}i_{3}\ldots i_{n}}\varepsilon_{j_{1}j_{2}j_{3}\ldots j_{n}}a^{j_1}_{i_1}\cdots a^{j_n}_{i_n} \\ 
&= \frac{1}{n!}\delta^{i_{1}i_{2}i_{3}\ldots i_{n}}_{j_{1}j_{2}j_{3}\ldots j_{n}}a^{j_1}_{i_1}\cdots a^{j_n}_{i_n}.
\end{align*}
$$

The reason I wanted to do this is that now we have a more explicit description for the coefficient $f_{k}(A)$ of $t^{n-k}$ as 

$$
f_k(A) = \frac{1}{k!}\delta^{i_{1}i_{2}i_{3}\ldots i_{k}}_{j_{1}j_{2}j_{3}\ldots j_{k}}a^{j_1}_{i_1}\cdots a^{j_k}_{i_k},
$$

which is... actually, I believe this is a good point to end this.

---

[^1]: I may or may not be foreshadowing an upcoming post on Pontryagin classes.

[^2]: Though most of them are $0$ except for the $n!$.