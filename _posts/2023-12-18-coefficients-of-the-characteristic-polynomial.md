---
layout: post
title: "Coefficients and Characteristic Polynomials"
categories: [Algebra]
mathjax: true
published: false
excerpt_separator: <!--more-->
---

Last time in our discussion regarding invariant polynomials, I mentioned that the coefficients of the characteristic polynomial of a matrix $A$ are sums of the principal $k \times k$ minors. This post will be a short one, giving some justification for this claim.

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

The adjugate satisfies some reasonable properties such as $\operatorname{adj}(cA) = c^{n-1}A$ for any scalar $c$, but the one we are mostly interested today is something called <b>Jacobi's formula</b> which relates the derivative of the determinant of a $A$ in terms of the adjugate of $A$ and the derivative of $A$.

<div class="theorem" text="(Jacobi's formula)">
If $A$ is a differentiable map from the real numbers to the $n \times n$ matrices, then

$$
\frac{d}{dt} \det A(t) = \operatorname{tr}\left(\operatorname{adj}(A(t))\frac{d A(t)}{dt}\right).
$$

</div>

<div class="proof">

</div>

---

The above formula will be extremely useful in proving the following fact about the coefficients of the characteristic polynomial $\det(\lambda I - A)$.

<div class="proposition">
Let $A$ be an $n \times n$ matrix. If $p_A(\lambda) = \det(\lambda I - A) = \sum_{k=0}^n f_k(A)\lambda^{n-k}$, then the coefficient of $\lambda^{k}$ is given by

$$
f_{n-k}(A) = \frac{1}{k!}p^{(k)}_A(0)
$$

for $k = 1,\dots, n$.
</div>

<div class="proof">
Using the Jacobi formula we obtain

$$
p'_A(\lambda) = \operatorname{tr}(\operatorname{adj}(\lambda I - A)).
$$

Observe now that $\operatorname{tr}(\operatorname{adj}(A))$ is exactly the sum of the principal minors of size $n-1$ of $A$. Denoting the sum of principal minors of size $k$ of $A$ by $E_k(A)$ we have $\operatorname{tr}(\operatorname{adj}(A)) = E_{n-1}(A)$.

Evaluating the derivative at $\lambda = 0$ yields

$$
\begin{align*}
f_{n-1}(A) &= p'_A(\lambda)\vert_{\lambda = 0} \\
&= \operatorname{tr}(\operatorname{adj}(\lambda I - A))\vert_{\lambda = 0} \\
&= \operatorname{tr}(\operatorname{adj}(- A)) \\
&= (-1)^{n-1}\operatorname{tr}(\operatorname{adj}(A)) \\
&=(-1)^{n-1}E_{n-1}(A).
\end{align*}
$$

Now, denoting the principal submatrices of $A$ of size $n-1$ by $A_i$ we see that $\operatorname{tr}(\operatorname{adj}(\lambda I - A)) = \sum_{i=1}^n p_{A_i}(\lambda)$ since the diagonal elements of $\operatorname{adj}(\lambda I - A)$ are given by the determinants of the submatrices obtained by removing the $i$'th row and column from $\lambda I - A$ which is just $\det(\lambda I - A_i)$.

Utilizing the Jacobi formula again, we get

$$
\begin{align*}
p''_A(\lambda) &= \frac{d}{dt}\operatorname{tr}(\operatorname{adj}(\lambda I - A)) \\
&= \frac{d}{dt}\sum_{i=1}^n p_{A_i}(\lambda) \\
&= \sum_{i=1}^n \frac{d}{dt} p_{A_i}(\lambda) \\
&= \sum_{i=1}^n\operatorname{tr}(\operatorname{adj}(\lambda I - A_i)).
\end{align*}
$$


Each of the summands $\operatorname{tr}(\operatorname{adj}(\lambda I - A_i))$ is the sum of the $n-1$ principal minors of size $n-2$ of a principal minor of $\operatorname{tr}(\operatorname{adj}(\lambda I - A))$, it follows that each of the $\binom{n}{n-2}$ principal minors of $\operatorname{tr}(\operatorname{adj}(\lambda I - A))$ of size $n-2$ appears twice in the sum. This yields

$$
\begin{align*}
f_{n-2}(A) &= \frac{1}{2!}p''_A(\lambda)\vert_{\lambda = 0} \\
&= \frac{1}{2!} \sum_{i=1}^n\operatorname{tr}(\operatorname{adj}(\lambda I - A_i))\vert_{\lambda = 0} \\
&= \frac{1}{2!} \sum_{i=1}^n\operatorname{tr}(\operatorname{adj}(- A_i)) \\
&= \frac{1}{2!} (-1)^{n-2}\sum_{i=1}^n\operatorname{tr}(\operatorname{adj}(A_i)) \\
&= \frac{1}{2!} (-1)^{n-2}(2E_{n-2}(A)) \\
&= (-1)^{n-2}(E_{n-2}(A))
\end{align*}
$$

and repeating this yields the desired result.

</div>

---

To make the last part of the above proof a bit more explicit, let's look at an example. Let

$$
A = \begin{pmatrix}
    a^1_1 & a^1_2 & a^1_3 & a^1_4 \\
    a^2_1 & a^2_2 & a^2_3 & a^2_4 \\
    a^3_1 & a^3_2 & a^3_3 & a^3_4 \\
    a^4_1 & a^4_2 & a^4_3 & a^4_4
\end{pmatrix}.
$$

The matrix $\lambda I - A$ is now given by

$$
\lambda I - A = \begin{pmatrix}
    \lambda - a^1_1 & -a^1_2 & -a^1_3 & -a^1_4 \\
    -a^2_1 & \lambda - a^2_2 & -a^2_3 & -a^2_4 \\
    -a^3_1 & -a^3_2 & \lambda -a^3_3 & -a^3_4 \\
    -a^4_1 & -a^4_2 & -a^4_3 & \lambda - a^4_4
\end{pmatrix}
$$

and the principal submatrices of size $4-1 = 3$ are now given by

$$
A_1 = \begin{pmatrix}
a^{2}_{2} & a^{2}_{3} & a^{2}_{4} \\
a^{3}_{2} & a^{3}_{3} & a^{3}_{4} \\
a^{4}_{2} & a^{4}_{3} & a^{4}_{4}
\end{pmatrix}
$$

$$
A_2 = \begin{pmatrix}
a^{1}_{1} & a^{1}_{3} & a^{1}_{4} \\
a^{3}_{1} & a^{3}_{3} & a^{3}_{4} \\
a^{4}_{1} & a^{4}_{3} & a^{4}_{4}
\end{pmatrix}
$$

$$
A_3 = \begin{pmatrix}
a^{1}_{1} & a^{1}_{2} & a^{1}_{4} \\
a^{2}_{1} & a^{2}_{2} & a^{2}_{4} \\
a^{4}_{1} & a^{4}_{2} & a^{4}_{4}
\end{pmatrix}
$$ 

$$
A_4 = \begin{pmatrix}
a^{1}_{1} & a^{1}_{2} & a^{1}_{3} \\
a^{2}_{1} & a^{2}_{2} & a^{2}_{3} \\
a^{3}_{1} & a^{3}_{2} & a^{3}_{3}
\end{pmatrix}.
$$
