---
layout: post
title: "Local Operators"
categories: [Differential Geometry]
mathjax: true
---

In the following we consider vector bundles $E \to M$ and $F \to M$ over a smooth manifold $M$ and instead of focusing on the bundles we'll digress on something called local operators which we will need in a upcoming post. Most of this is just paraphrasing results from the book by Loring W. Tu on Differential Geometry which I gladly recommend.

<div class="definition">
For vector bundles $E$ and $F$ over a smooth manifold $M$ we call an $\Bbb R$-linear map $\alpha : \Gamma(E) \to \Gamma(F)$ a <b>local operator</b> if whenever $s \in \Gamma(E)$ vanishes on an open set $U \subset M$, then $\alpha(s) \in \Gamma(F)$ vanishes on $U$ also.
</div>

There is also a notion of a <b>point operator</b> which replaces $U$ with a single point $p \in M$.

Before we look at the first example note that for a trivial bundle $M \times \Bbb R \to M$ a section $s$ of $M \times \Bbb R$ is a map $s(p) = (p, f(p))$ for some function $f : M \to \Bbb R$. We thus have a one-to-one correspondence

$$
\{ \text{sections of } M \times \Bbb R \} \longleftrightarrow \{f \mid f : M \to \Bbb R\}.
$$

In particular the space of smooth sections $\Gamma(M \times \Bbb R)$ can be identified with $C^\infty(M)$.

<div class="example">
The most basic example of a local operator is $\frac{d}{dx} : C^\infty(\Bbb R) \to C^\infty(\Bbb R)$. Here we are identifying $C^\infty(\Bbb R)$ with $\Gamma(\Bbb R \times \Bbb R)$ as noted above. If $f(x) \equiv 0$ on a neighborhood $U \ni p$, then $f'(x) \equiv 0$ on $U$.
</div>

<div class="example">
Another great example is the exterior derivative $d : \Gamma\left(\bigwedge^k T^\ast M\right) \to \Gamma\left(\bigwedge^{k+1} T^\ast M\right)$.
</div>

<div class="proposition">
If a map $\alpha : \Gamma(E) \to \Gamma(F)$ is $C^\infty(M)$-linear, then it is a local operator.
</div>

<div class="proof">
Consider $s \in \Gamma(E)$ such that $s$ vanishes on an open set $U \subset M$. Let $p \in U$ and consider a smooth bump function $f$ such that $f(p) = 1$ and the support of $f$ is contained in $U$. Now $fs$ is a section of $E$ and $fs \equiv 0$ on $M$. Thus $\alpha(fs) = 0$ and since $\alpha$ is $C^\infty(M)$-linear
$$
\alpha(fs) = f\alpha(s) = 0.
$$
At $p$ we have $\alpha(s)(p) = 0$ so $\alpha(s) \equiv 0$ on $U$.
</div>

<div class="theorem">
If a map $\alpha : \Gamma(E) \to \Gamma(F)$ is a local operator, then for each open subset $U \subset M$ there exists a unique linear map
$$
\alpha\vert_U : \Gamma(U, E) \to \Gamma(U, F)
$$
such that for any $s \in \Gamma(E)$ we have that
$$
\alpha\vert_U(s\vert_U) = \alpha(s)\vert_U.
$$
</div>
<div class="proof">
Let $s \in \Gamma(U, E)$ be a section and $p \in U$. Utilizing bump functions there exists a global section $\overline{s}$ such that $\overline{s}$ agrees with $s$ in some neighborhood $W$ of $p$ in $U$. Define
$$
\alpha\vert_U(s)(p) := \alpha(\overline{s})(p).
$$
If $\sigma \in \Gamma(E)$ is another global section with $\sigma = s$ in $W$, then $\sigma = \overline{s}$ in $W$. Now as $\alpha$ is a local operator we conclude that $\alpha(\sigma) = \alpha(\overline{s})$ in $W$ i.e. $\alpha(\sigma)(p) = \alpha(\overline{s})(p)$ which shows that $\alpha\vert_U(s)(p)$ is independent of the choice of $\overline{s}$ and so $\alpha\vert_U$ is well-defined and unique. To show that $\alpha\vert_U$ is smooth we note that if $s \in \Gamma(U,E)$ and $\overline{s} \in \Gamma(M, E)$ agree on a neighborhood $W \ni p$, then $\alpha\vert_U(s) = \alpha(\overline{s})$ on $W$ and the left-hand side is smooth. Lastly if $s \in \Gamma(M,E)$ is a global section, then it is a global section of it's restriction $s\vert_U$ and so $\alpha\vert_U(s\vert_U)(p) = \alpha(s)(p)$ for all $p \in U$. Thus $\alpha\vert_U(s) = \alpha(\overline{s})$.
</div>

It's relatively simple to show also that if $\alpha :\Gamma(E) \to \Gamma(F)$ is $C^\infty(M)$-linear, then $\alpha\vert_U : \Gamma(U, E) \to \Gamma(U, F)$ is $C^\infty(U)$-linear.

Let's go over couple more lemmas before our main result.

<div class="lemma">
A fiber-preserving map $\Phi : E \to F$ that is linear on each fiber is smooth if and only if the induced map $\widetilde{\Phi} : \Gamma(E) \to \Gamma(F)$ takes smooth sections of $E$ to smooth sections of $F$.
</div>

<div class="proof">
Suppose that $\Phi : E \to F$ is smooth. Then for a smooth section $s \in \Gamma(E)$ the composition $\widetilde{\Phi}(s) = \Phi \circ s$ is smooth as it's a composition of smooth maps. Conversely suppose that $\widetilde{\Phi}$ takes smooth sections of $E$ to smooth sections of $F$. As usual we proceed locally. Fix $p \in M$ and consider a chart $(U, x^1,\dots,x^n)$ at $p$ over which $E$ and $F$ are both trivial. Let $e_1,\dots, e_r \in \Gamma(E)$ be a frame for $E$ over $U$ and $f_1,\dots, f_m \in \Gamma(F)$ be a frame for $F$ over $U$. Now a point in $E\vert_U$ can be written as a linear combination $\sum a^j e_j$. Suppose
$$
\Phi \circ e_j = \sum_i b^i_jf_i.
$$
Then
$$
\Phi\left(\sum_{j}a^je_j\right) = \sum_{i,j} a^jb^i_jf_i.
$$
Taking local coordinates on $E\vert_U$ to be $(x^1,\dots,x^n,a^1,\dots,a^r)$ we have
$$
\Phi(x^1,\dots,x^n,a^1,\dots,a^r) = \left(x^1,\dots,x^n, \sum_ja^j b^1_j,\dots,\sum_ja^j b^m_j\right)
$$
which is smooth.
</div>

<div class="lemma">
An $C^\infty(M)$-linear map $\alpha : \Gamma(E) \to \Gamma(F)$ is a point operator.
</div>

<div class="proof">
Suppose that $s \in \Gamma(E)$ such that $s$ vanishes at $p \in M$. Let $U$ be an open neighborhood of $p$ over which $E$ is trivial. Consider a frame $e_1,\dots,e_r$ of $E$ over $U$. We can write 
$$
s\vert_U = \sum_i a^ie_i
$$
where the $a^i$'s are smooth functions on $U$. Since 
$$
0 = s\vert_U(p) = \sum_i a^i(p)e_i(p)
$$
we conclude that $a^i(p) = 0$ for every $i$. By our theorem before we know that $\alpha$ restricts to a unique map $\alpha\vert_U : \Gamma(U,E) \to \Gamma(U,F)$ and so
$$
\begin{align*}
\alpha(s)(p) &= \alpha\vert_U(s\vert_U)(p) \\
&= \alpha\vert_U(\sum_i a^ie_i)(p) \\
&= \left(\sum_i a^i \alpha\vert_U(e_i)\right)(p) \\
&= \sum_i a^i(p)\alpha\vert_U(e_i)(p) \\
&= 0.
\end{align*}
$$
</div>

<div class="lemma">
If $\alpha : \Gamma(E) \to \Gamma(F)$ is $C^\infty(M)$-linear, then for each $p \in M$, there is a unique linear map $\Phi_p : E_p \to F_p$ such that for all $s \in \Gamma(E)$,
$$
\Phi_p(s(p)) = \alpha(s)(p).
$$
</div>

<div class="proof">
Given $v \in E_p$ choose any $s \in \Gamma(E)$ such that $s(p) = v$ and set
$$
\Phi_p(v) = \alpha(s)(p) \in F_p.
$$
This definition is independent of the choice of $s$ since as we saw previously $\alpha$ is a point operator. To show that $\Phi_p$ is linear suppose that $v_1,v_2 \in E_p$ and $a_1,a_2 \in \Bbb R$. Let $s_1$ and $s_2$ be global sections of $E$ with $s_i(p) = v_i$. Now
$$
\begin{align*}
\Phi_p(a_1v_1+a_2v_2) &= \alpha(a_1s_1 + a_2s_2)(p) \\
&= a_1\alpha(s_1)(p) + a_2\alpha(s_2)(p) \\
&= a_1\Phi_p(v_1) + a_2\Phi_p(v_2).
\end{align*}
$$
</div>

Alright now onto the fun stuff. It turns out that the following is true.

<div class="theorem">
There is a one-to-one correspondence between bundle maps $\Phi : E \to F$ and $C^\infty(M)$-linear maps $\alpha :\Gamma(E) \to \Gamma(F)$ given by $\Phi \mapsto \widetilde{\Phi}$.
</div>
<div class="proof">
Suppose that $\alpha :\Gamma(E) \to \Gamma(F)$ is $C^\infty(M)$-linear. For each $p \in M$ there is a linear map $\Phi_p : E_p \to F_p$ such that for any $s \in \Gamma(E)$,
$$
\Phi_p(s(p)) = \alpha(s)(p).
$$
Define $\Phi : E \to F$ by setting $\Phi(v) = \Phi_p(v)$ if $v \in E_p$. Now for any $s \in \Gamma(E)$ and $p \in M$
$$
\widetilde{\Phi}(s)(p) = \Phi(s(p)) = \alpha(s)(p),
$$
and so $\alpha = \widetilde{\Phi}$ which prove surjectivity. Consider then bundle maps $\Phi, \Psi : E \to F$ with $\widetilde{\Phi} = \widetilde{\Psi}$. For any $v \in E_p$ pick $s \in \Gamma(E)$ with $s(p) = e$. Then
$$
\begin{align*}
\Phi(v) &= \Phi(s(p))\\
&= \widetilde{\Phi}(s)(p)\\
&= \widetilde{\Psi}(s)(p) \\
&= \Psi(s(p)) \\
&= \Psi(v).
\end{align*}
$$
i.e. $\Phi = \Psi$.
</div>