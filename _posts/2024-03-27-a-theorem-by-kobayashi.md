---
layout: post
title: "Instability in the Sense of Bogomolov"
categories: [Complex Geometry, Differential Geometry]
mathjax: true
published: true
excerpt_separator: <!--more-->
---

This is going to be a quick one. We'll cover the fact that an Hermite-Einstein vector bundle $E$ over a compact complex manifold $X$ is not instable in the sense of Bogomolov. The most important tool for proving this is a vanishing theorem for holomorphic sections in Hermite-Einstein bundles with negative proportionality factor.

<!--more-->

---

In the following, $X$ will always denote a compact complex manifold, $(E,h)$ a holomorphic Hermitian vector bundle over $X$ and $\nabla$ the Chern connection. If $g$ is a Hermitian metric on $X$, then recall that the Laplace-Beltrami operator $\Delta : \Omega^0(X) \to \Omega^0(X)$ is given in local coordiantes $(z^1,\dots,z^n)$ by

$$
\Delta f = \sum_{j,k} g^{jk}\frac{\partial^2 f}{\partial z^j \partial \bar{z}^k}.
$$

Note that $\Delta = i\Lambda \circ \partial\bar{\partial}$, where $\Lambda = -i\sum_{j,k}g^{jk}\bar{\iota}_k\iota_j.$

<div class="lemma" text="(Bochner)">
If $f \in \Omega^0(X)$ is a real-valued function such that $\Delta f \ge 0$, then $\Delta f =0$ and $f$ is constant.
</div>

The vanishing theorem we are aiming for follows from Bochner's result and the following lemma.

<div class="lemma">
Let $U \subset X$ be an open subset. For a holomorphic section $\xi \in H^0(U,E)$ we have that
$$
\Delta h(\xi,\xi) = -i\Lambda h(F_\nabla \xi, \xi) + i\Lambda|\nabla \xi|^2,
$$
where $F_\nabla$ denotes the curvature of the Chern connection on $(E,h)$.
</div>

<div class="proof">
Let $\xi \in H^0(U,E)$ be a holomorphic section. Then as the Chern connection is compatible with $h$ we have that
$$
dh(\xi,\xi) = h(\nabla \xi, \xi) + h(\xi,\nabla \xi).
$$
Also as $\nabla^{0,1} = \bar{\partial}$ for the Chern connection and $\xi$ is holomorphic, $\nabla \xi$ is of type $(1,0)$. A type comparison yields
$$
\partial h(\xi,\xi) = h(\nabla \xi, \xi).
$$
It follows that
$$
\begin{align*}
\bar{\partial}\partial h(\xi,\xi) &= d\partial h(\xi,\xi) \\
&= dh(\nabla \xi,\xi) \\
&= h(F_\nabla \xi, \xi) - h(\nabla \xi, \nabla \xi),
\end{align*}
$$
since generally for a $p$-form $\eta \in \Omega^p(U,E)$ and $1$-form $\beta \in \Omega^1(U,E)$ we have 
$$
dh(\eta,\beta) = h(\nabla \eta, \beta) + (-1)^ph(\eta,\nabla \beta).
$$
So all in all
$$
\begin{align*}
\Delta h(\xi,\xi) &= i\Lambda(\partial\bar{\partial}h(\xi,\xi)) \\
&= -i\Lambda(\bar{\partial}\partial h(\xi,\xi)) \\
&= -i\Lambda h(F_\nabla \xi, \xi) + i \Lambda h(\nabla \xi, \nabla \xi) \\
&= -i\Lambda h(F_\nabla \xi, \xi) + i\Lambda|\nabla \xi|^2.
\end{align*}
$$
</div>

<div class="proposition">
If $(E,h)$ is a Hermite-Einstein vector bundle over $X$ with proportionality factor $\lambda < 0$, then $E$ has no non-trivial global holomorphic sections. If $\lambda = 0$, then $\nabla \xi = 0$ for every $\xi \in H^0(X,E)$.
</div>

<div class="proof">
Let $\xi$ be a global holomorphic section. Then $\nabla \xi$ is of type $(1,0)$ and locally
$$
\nabla \xi = \sum \eta_j \otimes dz^j.
$$
Now
$$
\begin{align*}
i\Lambda h(\nabla \xi, \nabla \xi) &= i\Lambda \sum_{j,k} h(\eta_j,\eta_k)dz^j \wedge d\bar{z}^k \\
&= \sum_{j,k} h(\eta_j,\eta_k)g^{jk},
\end{align*}
$$
and for each point $p \in X$ there are local coordinates with $g^{jk}(p) = \delta^{jk}$. It follows that
$$
i\Lambda h(\nabla \xi, \nabla \xi) \ge 0,
$$
and the equality holds when $\nabla \xi = 0$. The previous lemma gives
$$
\begin{align*}
\Delta h(\xi,\xi) = -i\Lambda h(F_\nabla \xi, \xi) + i\Lambda |\nabla \xi|^2,
\end{align*}
$$
and since $F_\nabla \in \Omega^2(X,\operatorname{End}(E))$ we can write it locally on a framed open set $U$ as $F_\nabla = \sum \Omega^i_j \otimes \varepsilon^j \otimes e_i$. where $\Omega^i_j = R^i_{j\alpha\beta} dz^\alpha \wedge d\bar{z}^\beta$ denote the curvature $2$-forms. Writing $\xi = \xi^ke_k$ we obtain $F_\nabla \xi = \sum \Omega^i_j \xi^j \otimes e_i$ and so
$$
\begin{align*}
h(F_\nabla \xi, \xi) &= h(\Omega^i_j \xi^j \otimes e_i, \xi^ke_k) \\
&= \Omega^i_j\xi^j\bar{\xi}^k h(e_i,e_k) \\
&=h_{ik}\Omega^i_j\xi^j\bar{\xi}^k \\
&= h_{ik}R^i_{j\alpha\beta} \xi^j\bar{\xi}^k dz^\alpha \wedge d\bar{z}^\beta.
\end{align*}
$$
We obtain
$$
\begin{align*}
\Lambda h(F_\nabla \xi, \xi) &= -ih_{ik}g^{\alpha\beta}R^i_{j\alpha\beta}\xi^j\bar{\xi}^k \\
&= -ig^{\alpha\beta}R^i_{j\alpha\beta}h(\xi,\xi),
\end{align*}
$$
which yields $-i\Lambda h(F_\nabla \xi,\xi) = -g^{\alpha\beta}R^i_{j\alpha\beta}h(\xi,\xi)$ and the Hermite-Einstein condition gives
$$
-i\Lambda h(F_\nabla \xi,\xi) = -\lambda h(\xi,\xi).
$$
Thus
$$
\Delta h(\xi,\xi) = -\lambda h(\xi,\xi) + i\Lambda |\nabla \xi|^2.
$$
When $\lambda < 0$ we have $\Delta h(\xi,\xi) \ge 0$ and Bochner's lemma implies that $\Delta h(\xi,\xi) = 0$ and $h(\xi,\xi)$ is constant. Since both of the terms $-\lambda h(\xi,\xi)$ and $i\Lambda |\nabla \xi|^2$ are non-negative, they both vanish. In particular $\nabla \xi = 0$ and
$$
h(\xi,\xi) = 0,
$$
i.e. $\xi = 0$.
</div>

This gives the following neat theorem due to Kobayashi.

<div class="theorem" text="(Kobayashi)">
Let $(E,h)$ be a Hermite-Einstein vector bundle over $X$ with proportionality factor $\lambda$. For the bundle $E^{\otimes r} \otimes {E^\ast}^{\otimes s}$ the following holds:
<ol>
    <li>
    If $0 \ne \lambda \le 0$, then $H^0(X, E^{\otimes r} \otimes {E^\ast}^{\otimes s}) = 0$ for $r > s$, and for every 
    $$
    \xi \in H^0(X, E^{\otimes r} \otimes {E^\ast}^{\otimes r})
    $$
    we have that $\nabla \xi = 0$.
    </li>
    <li>
    If $\lambda = 0$, then for any $\xi \in H^0(X, E^{\otimes r} \otimes {E^\ast}^{\otimes s})$, $\nabla \xi = 0$ holds for all $r$ and $s$.
    </li>
    <li>
    If $0\ne\lambda \ge 0$, then $H^0(X, E^{\otimes r} \otimes {E^\ast}^{\otimes s}) = 0$ for $r < s$, and for every 
    $$
    \xi \in H^0(X, E^{\otimes r} \otimes {E^\ast}^{\otimes r})
    $$
    we have that $\nabla \xi = 0$.
    </li>
</ol>
</div>
<div class="proof">
Recall that the tensor power $E^{\otimes r}$ of a Hermite-Einstein bundle $E$ is Hermite-Einstein with proportionality factor $r\lambda$ and the dual bundle $E^\ast$ is Hermite-Einstein with proportionality factor $-\lambda$. It follows that $E^{\otimes r} \otimes {E^\ast}^{\otimes s}$ is Hermite-Einstein with proportionality factor $(r-s)\lambda$. All of the statements now follow from the previous propositions by analyzing the sign of $(r-s)\lambda$.
</div>
<div class="corollary">
If $(E,h)$ is a Hermite-Einstein vector bundle over $X$ with proportionality factor $\lambda = 0$ and $\xi \in H^0(X, E)$ has a zero, then $\xi = 0$.
</div>
<div class="proof">
Let $\xi \in H^0(X,E)$, then the above theorem states that $\nabla \xi = 0$ and so
$$
dh(\xi,\xi) = h(\nabla \xi, \xi) + h(\xi,\nabla \xi) = 0,
$$
hence $h(\xi,\xi)$ is constant. If there exist $p \in X$ with $\xi(p) = 0$, then
$$
h(\xi,\xi) = h(\xi(p),\xi(p)) = 0,
$$
and so $\xi = 0$.
</div>

<div class="definition">
A complex vector bundle $E$ of rank $r$ over $X$ is said to be <b>instable</b> in the sense of Bogomolov if there exists a representation $\rho$ of $\mathrm{GL}(r,\Bbb C)$ with determinant $1$ (i.e., a representation which factors through $\mathrm{PGL}(r,\Bbb C)$) such that the associated vector bundle $E_\rho$ has a non-zero section $s$ which vanishes at some point of $X$.
</div>

In case you haven't seen it before, the associated bundle $E_\rho$ in the above definition is defined so that if $E$ is given by transition maps $g_{ij}$, then $E_\rho$ is given by transition maps $\rho(g_{ij})$.

<div class="theorem" text="(Kobayashi)">
Let $(E,h)$ be an Hermite-Einstein vector bundle over $X$. Then $E$ is not instable in the sense of Bogomolov.
</div>

<div class="proof">
To prove that $E$ is not instable in the sense of Bogomolov, we need to show that there is no representation $\rho$ of $\mathrm{GL}(r,\mathbb{C})$ with determinant $1$ such that the associated vector bundle $E_\rho$ has a non-zero section that vanishes at some point of $X$.

Since the decomposition of a representation into irreducible factors corresponds to the decomposition of the associated bundle into direct sum of the bundles associated with the factors, it is sufficient to show that if $\rho$ is an irreducible representation of $\mathrm{GL}(r,\Bbb C)$ with determinant $1$, and $\xi \in H^0(X,E_\rho)$ a global holomorphic section with a zero, then $\xi = 0$.

Suppose $\rho$ is an irreducible representation of $\mathrm{GL}(r,\mathbb{C})$ with determinant $1$. Consider a global holomorphic section $\xi \in H^0(X, E_\rho)$.

First, note that any irreducible representation $\rho$ of $\mathrm{GL}(r,\mathbb{C})$ with determinant $1$ can be decomposed into tensor products of fundamental representations, specifically exterior powers of the standard representation $\mathbb{C}^r$. This means $\rho$ can be viewed as an irreducible factor of a representation $\lambda$ acting on a space $W$ defined by
$$ 
W = \left(\Lambda^{m_1} \mathbb{C}^r\right)^{\otimes q_1} \otimes \cdots \otimes \left(\Lambda^{m_s} \mathbb{C}^r\right)^{\otimes q_s} \otimes \left(\Lambda^{m} \mathbb{C}^r\right)^{\otimes q}, 
$$
where $1 \le m_1 < \dots < m_s \le m$, and $\sum_i q_i m_i = qm$ for some integers $q_1, \ldots, q_s, q$.

Also note that $W$ is a subspace of
$$ 
\left(\mathbb{C}^r\right)^{\otimes qm} \otimes \left(\left(\mathbb{C}^r\right)^*\right)^{\otimes qm}.
$$

Thus, $\lambda$, and consequently $\rho$, can be seen as a subrepresentation of a representation $\sigma$ on the space
$$ 
V = \left(\mathbb{C}^r\right)^{\otimes qm} \otimes \left(\left(\mathbb{C}^r\right)^*\right)^{\otimes qm}.
$$

Now, let $E_\sigma$ denote the vector bundle associated with the representation $\sigma$. Then, 
$$ 
E_\sigma = \left(E^{\otimes qm}\right) \otimes \left({E^*}^{\otimes qm}\right).
$$

Since subrepresentations correspond to subbundles, we have an inclusion:
$$
E_\rho \subset \left(E^{\otimes qm}\right) \otimes \left({E^*}^{\otimes qm}\right).
$$

Thus, we can think of $\xi$ as a section of $\left(E^{\otimes qm}\right) \otimes \left({E^*}^{\otimes qm}\right)$. Note that $\left(E^{\otimes qm}\right) \otimes \left({E^*}^{\otimes qm}\right)$ is a Hermite-Einstein vector bundle with proportionality factor $\lambda = 0$. 

According to our previous corollary, if a section of a Hermite-Einstein bundle with proportionality factor $\lambda = 0$ has a zero, then the section must be identically zero. Therefore, if $\xi$ has a zero, it must be the zero section, which completes the proof.
</div>