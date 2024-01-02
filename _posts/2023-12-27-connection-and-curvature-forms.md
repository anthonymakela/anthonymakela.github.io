---
layout: post
title: "Connection and Curvature Forms"
categories: [Differential Geometry]
mathjax: true
excerpt_separator: <!--more-->
---

In the previous post, we looked at invariant polynomials. The topic for this one is going to be something called <b>connection $1$-forms</b> and <b>curvature $2$-forms</b>.

<!--more-->

For the remaining of this post let $M$ be a smooth manifold and $\nabla$ a connection on a smooth rank $n$ vector bundle $\pi : E \to M$. To begin with, if you have taken a class in Riemannian Geometry, you might know a way to describe connections locally using the Christoffel symbols $\Gamma^k_{ij}$. Instead of this, we are going to adapt to the Cartan Formalism and describe the connection locally using differential forms.

Let's first remind ourselves that a connection $\nabla : \Gamma(TM) \times \Gamma(E) \to \Gamma(E)$ is $C^\infty(M)$-linear in the first argument, but <i>not</i> $C^\infty(M)$-linear in the second argument. However, it turns out that being $C^\infty(M)$-linear in the first argument and satisfying the Leibniz rule in the second argument is enough to imply that $\nabla$ is a <a href="https://anthonymakela.com/differential%20geometry/2023/07/01/local-operators.html" style="color:#680530; text-decoration: underline;">Local Operator</a>. The proof can be found in Lee's book on Riemannian Geometry, but for the sake of completeness, I'll prove it here.

<div class="proposition">
Let $\nabla$ be a connection on a vector bundle $E$ over a manifold $M$, $X \in \Gamma(TM)$, and $s \in \Gamma(E)$. If either $X$ or $s$ vanishes identically on an open subset $U \subset M$, then $\nabla_X s \equiv 0$ on $U$.
</div>

<div class="proof">
Consider an open neighborhood $U \subset M$ and $p \in U$. Suppose that $X$ vanishes identically on $U$. Choose a bump function $\varphi \in C^\infty(M)$ with support in $U$ such that $\varphi(p) = 1$. Now $\varphi X \equiv 0$ on $M$ since $X$ vanishes on $U$ and $\varphi$ on $M \setminus U$. Thus

$$
\nabla_{\varphi X}s = 0.
$$

Since $\nabla$ is $C^\infty(M)$-linear in the first argument we have

$$
0 = \nabla_{\varphi X}s = \varphi\nabla_X s.
$$

Evaluating at $p$ yields

$$
0 = \nabla_{\varphi X}s\vert_p = \varphi(p)\nabla_X s\vert_p = \nabla_X s\vert_p.
$$

As $p$ is arbitary, $\nabla_X s \equiv 0$ on $U$.

Suppose then that $s \equiv 0$ on $U$ and $p \in U$. Again, choose a bump function $\psi$ supported on $U$ such that $\psi(p) \equiv 1$ in a neighborhood of $p$. By our choice of $\psi$ the derivative $X_p\psi$ vanishes. Since $s$ vanishes on the support of $\psi$ we have that $\psi s \equiv 0$ on $M$. It follows that $\nabla_X(\psi s) \equiv 0$ on $M$. Evaluating at $p$ yields

$$
0 =\nabla_X(\psi s)\vert_p = (X_p\psi) s(p) + \psi(p)\nabla_X s\vert_p = \nabla_X s\vert_p
$$

and the result follows.
</div>

---

Now since local operators can be restricted to any open subset, a connection on a vector bundle can be restricted to any open subset.

Suppose now that $U$ is a trivializing open set for $E$ and $(e_i)$ a frame for $E$ over $U$. Let $X \in \Gamma(U, TM)$. Since any local section $s \in \Gamma(U, E)$ is a linear combination $s = \sum a^je_j$, the section $\nabla_X s$ can be computed from $\nabla_X e_j$ by using linearity and the Leibniz rule. Describing $\nabla_X e_j$ is merely linear algebra. Let $(\varepsilon^i)$ be the dual coframe, we have that

$$
\nabla_X e_j = \sum_i \varepsilon^i(\nabla_X e_j)e_i.
$$

We set $\omega^i_j(X) := \varepsilon^i(\nabla_X e_j)$ and call these the <b>connection $1$-forms</b>[^1]. The matrix $[\omega^i_j]$ is called the <b>connection matrix</b> of the connection $\nabla$ relative to the local frame.

So a connection $\nabla$ on $E\vert_U$ determines a unique connection matrix $[\omega^i_j]$ relative to the local frame. Conversely, any matrix $[\omega^i_j]$ of $1$-forms determines a connection on $E\vert_U$ as follows. For $X, Y \in \Gamma(U,TM)$ set

$$
\nabla_X e_j = \sum \omega^i_j(X)e_i,
$$

and define $\nabla_X Y$ by applying the Leibniz rule to $Y = \sum_j Y^je_j$:

$$
\begin{align*}
    \nabla_X Y &= \nabla_X\left(\sum_j Y^je_j\right) \\
    &= (XY^j)e_j + Y^j\omega^i_j(X)e_i \\
    &=(XY^j + Y^j\omega^i_j(X))e_i.
\end{align*}
$$

As you might notice the story here is pretty much the same as with the Christoffel symbols[^2]. The reason we do it in terms of differential forms now is that we get a neat pathway to characteristic classes.

---

What about curvature? Similarly for $X,Y \in \Gamma(TM)$ and $s \in \Gamma(E)$ the section $R(X,Y)s \in \Gamma(E)$ can be computed from $R(X,Y)e_j$ when $(e_i)$ is a local frame over $U \subset M$. Again if $(\varepsilon^i)$ is the dual coframe

$$
R(X,Y)e_j = \sum \varepsilon^i(R(X,Y)e_j)e_i.    
$$

Analogously as with the connection $1$-forms we define the <b>curvature $2$-forms</b> as $\Omega^i_j(X,Y) := \varepsilon^i(R(X,Y)e_j)$.

You might recall from your studies in Riemannian Geometry that the curvature endomorphism can be written in terms of local coordinates $(U,x^1,\dots,x^n)$ as

$$
R = R^l_{ijk} dx^i \otimes dx^j \otimes dx^k \otimes \partial_l
$$

where the coefficients $R^l_{ijk}$ are defined by

$$
R^l_{ijk} = \partial_i\Gamma^l_{jk} - \partial_j\Gamma^l_{ik} + \Gamma^m_{jk}\Gamma^l_{im} - \Gamma^m_{ik}\Gamma^l_{jm}.
$$

Well in terms of this so-called Cartan Formalism, we end up having $\Omega^l_k(\partial_i,\partial_j) = R^l_{ijk}$ and since $R^l_{ijk}$ is expressible by the Christoffel symbols it would be reasonable to expect that there is a relationship between the connection $1$-forms and curvature $2$-forms right? This turns out to be true and we state it as the following theorem.

<div class="theorem">
Let $\nabla$ be a connection on a vector bundle $E \to M$ of rank $n$. Relative to a local frame $(e_i)$ over $U$, the curvature forms $\Omega^i_j$ are related to the connection forms $\omega^i_j$ by the <b>second structural equation:</b>

$$
\Omega^i_j = d\omega^i_j + \sum_k \omega^i_k \wedge \omega^k_j.
$$
</div>

<div class="proof">
Let $X, Y \in \Gamma(U, TM)$. We have that

$$
\begin{align*}
\nabla_X\nabla_Y e_j &= \nabla_X \sum_k\left(\omega^k_j(Y)e_k\right) \\
&= \sum_k X\omega^k_j(Y)e_k + \sum_k\omega^k_j(Y)\nabla_X e_k \\
&= \sum_i X\omega^i_j(Y)e_i + \sum_{i,k} \omega^k_j(Y)\omega^i_k(X)e_i.
\end{align*}
$$

Swapping $X$ and $Y$ yields

$$
\begin{align*}
\nabla_Y\nabla_Xe_j = \sum_i Y\omega^i_j(X)e_i + \sum_{i,k} \omega^k_j(X)\omega^i_k(Y)e_i.
\end{align*}
$$

Hence

$$
\begin{align*}
R(X,Y)e_j &= \nabla_X\nabla_Y e_j - \nabla_Y\nabla_X e_j - \nabla_{[X,Y]}e_j \\
&= (X\omega^i_j(Y) - Y\omega^i_j(X) - \omega^i_j([X,Y]))e_i + (\omega^i_k(X)\omega^k_j(Y)- \omega^i_k(Y)\omega^k_j(X))e_i \\
&= d\omega^i_j(X,Y)e_i + \omega^i_k\wedge \omega^k_j(X,Y)e_i \\
&= (d\omega^i_j + \omega^i_k\wedge \omega^k_j)(X,Y)e_i. 
\end{align*}
$$

Comparing this with how we defined $\Omega^i_j(X,Y)$ we see that

$$
\Omega^i_j = d\omega^i_j + \sum_k \omega^i_k \wedge \omega^k_j.
$$
</div>

In matrix notation, the above can be written as $\Omega = d\omega + \omega \wedge \omega$.

---

Before we wrap this up, let's consider how the connection $1$-forms and curvature $2$-forms transform under a change of frame. Recalling that the curvature endomorphism is a section of the bundle $\left(\bigotimes^2 T^\ast M \right) \otimes \operatorname{End}(E)$ i.e. an $\operatorname{End}(E)$-valued $(0,2)$-tensor field. These two observations will end up looking awfully similar to what we discussed in <a href="https://anthonymakela.com/algebra/2023/12/17/invariant-polynomials.html" style="color:#680530; text-decoration: underline;">Invariant Polynomials</a>, guiding us towards characteristic classes.

Suppose that $U \subset M$ is an open set and $(e_i)$ a local frame over $U$. Writing the frame as a row vector $e = \begin{bmatrix} e_1 & \cdots & e_n\end{bmatrix}$, then in matrix notation we can write $\nabla_X e_j = \sum \omega^i_j(X)e_i$ as

$$
\nabla_X e = e\omega(X).
$$

As a function of $X$ we have $\nabla e = e\omega$. Suppose now that $(\bar{e}_i)$ is another local frame over $U$. Let $\bar{\omega} = [\bar{\omega}^i_j]$ and $\bar{\Omega} = [\bar{\Omega}^i_j]$ be the connection and curvature matrices with respect to the frame $(\bar{e}_i)$. As sections over $U$ we can write

$$
\bar{e}_j = \sum_i a^i_je_i
$$

which yields a matrix of functions $a = [a^i_j]$ where each $a^i_j$ is a smooth function on $U$. It follows that $a : U \to \mathrm{GL}(n,\Bbb R)$. In matrix notation $\bar{e} = ea$.

<div class="theorem">
Suppose that $(e_i)$ and $(\bar{e}_i)$ are two local frames over $U \subset M$ such that $\bar{e} = ea$ for some $a : U \to \mathrm{GL}(n,\Bbb R)$. If $\omega$ and $\bar{\omega}$ are the connection matrices and $\Omega$ and $\bar{\Omega}$ the curvature matrices of a connection $\nabla$ relative to the two frames, then
<ol>
  <li>$\bar{\omega} = a^{-1}\omega a + a^{-1}da$.</li>
  <li>$\bar{\Omega} = a^{-1}\Omega a$.</li>
</ol> 
</div>

<div class="proof">
For the first item note that
$$
\begin{align*}
\nabla \bar{e} &= \nabla(ea) \\
&= (\nabla e)a + eda \\
&= (e\omega)a + eda \\
&= \bar{e}a^{-1}\omega a + \bar{e}a^{-1}da \\
&= \bar{e}(a^{-1}\omega a + a^{-1}da).
\end{align*}
$$

As $\nabla \bar{e} = \bar{e}\bar{\omega}$ it follows that $\bar{\omega} = a^{-1}\omega a + a^{-1}da$. For the second item remember that the curvature is $\operatorname{End}(E)$-valued. That is for a point $p$ and $X_p, Y_p \in T_pM$ we have that $R(X_p,Y_P) \in \operatorname{End}(E_p)$ with matrix $[\Omega^i_j(X_p,Y_p)]$ relative to the basis $(e_i)$ at $p$. A change of basis should thus lead to a conjugate matrix. Writing $R(X,Y)e_j = \sum \Omega^i_j(X,Y)e_i$ in matrix notation yields

$$
R(X,Y)e = \begin{bmatrix} e_1 & \cdots & e_n\end{bmatrix}[\Omega^i_j(X,Y)] = e\Omega(X,Y)
$$

and so $R(e) = e\Omega$. It follows that

$$
\begin{align*}
R(\bar{e}) &= R(ea) \\
&= R(e)a \\
&=e\Omega a \\
&= \bar{e}a\Omega a
\end{align*}
$$

which yields that $\bar{\Omega} = a^{-1}\Omega a$.
</div>

Ring a bell regarding those invariant polynomials and conjugation? That's what we'll discuss in the next post. 

---

[^1]: These are indeed $1$-forms as $\omega^i_j : \Gamma(TM) \to C^\infty(M)$ is a $C^\infty(M)$-linear map.

[^2]: Infact, note that in local coordinates $(U, x^1,\dots,x^n)$ we have $\omega^k_j(\partial_i) = \Gamma^k_{ij}$.