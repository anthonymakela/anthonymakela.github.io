---
layout: post
title: "The Lefschetz Operator"
categories: [Complex Geometry, Differential Geometry, Linear Algebra]
mathjax: true
published: false
excerpt_separator: <!--more-->
---

Soon, I'll be diving into Kähler manifolds and Hodge theory on these manifolds. This post is going to act as a warm-up in linear algebra for what's to come in the next posts.

<!--more-->

In the world of complex geometry, Kähler identities are like a set of rules that link different operators on a Kähler manifold. These operators include the Dolbeault operators, their adjoints, contraction and wedge operators of the Kähler form, and the Laplacians of the Kähler metric. What's cool is how these Kähler identities, when they get together with Hodge theory stuff, end up creating a bunch of relationships in the de Rham and Dolbeault cohomology for compact Kähler manifolds. This leads to some pretty neat results, such as the Lefschetz hyperplane theorem, the hard Lefschetz theorem, the Hodge-Riemann bilinear relations, and the Hodge index theorem. And that's not all—when you mix these identities with Hodge theory again, they play a key role in proving some major analytical concepts on Kähler manifolds, like the $\partial\bar{\partial}$-lemma, the Nakano inequalities, and the Kodaira vanishing theorem.

---

To set the stage, fix a real finite-dimensional inner product space $(V,g)$ and let $J \in \operatorname{End}(V)$ be an almost complex structure.

<div class="definition">
The almost complex structure $J$ is compatible with the inner product $g$ if 

$$
g( u, v ) = g( J(u), J(v)),
$$

for all $u,v \in V$.
</div>


<div class="definition">
The <b>fundamental form</b> associated to $(V,g,J)$ is the form given by

$$
\omega(u,v) := g( J(u), v).
$$

</div>

Note that the fundamental form is antisymmetric as:

$$
\begin{align*}
\omega(u,v) &= g( J(u),v) \\
&= g( J^2(u), J(v)) \\
&= g( -u, J(v)) \\
&= -g( u,J(v)) \\
&= -g( J(v), u) \\
&= -\omega(v,u).
\end{align*}
$$

<div class="lemma">
Let $(V,g,J)$ be a real vector space endowed with a compatible complex structure. Then the form 

$$
h(u, v) := g( u, v) - i\omega(u,v),
$$

is a positive Hermitian form on $(V,J)$.
</div>

<div class="proof">
For $u,v,w \in V$ and $a,b \in \Bbb R$ we have that

$$
\begin{align*}
h(au + bv, w) &= g( au + bv, w) - i\omega(au + bv, w) \\
&= ag( u , w) + bg( v,w) -ig( J(au + bv), w) \\
&= ag( u , w) + bg( v,w) -ig( aJ(u) + bJ(v), w) \\
&= ag( u , w) + bg( v,w) -i(ag( J(u), w) +  bg( J(v), w)) \\
&= a(g( u, w) -i g( J(u), w)) + b(g( v,w) - ig( J(v), w)) \\
&= ah(u,w) + bh(v,w),
\end{align*}
$$

which proves $\Bbb R$-linearity. Also $h(u,v) = \overline{h(v,u)}$ since $\omega$ is antilinear. Lastly

$$
\begin{align*}
h(J(u), v) &= g( J(u), v ) - i\omega(J(u), v) \\
&= g( J(u), v ) + ig( u,v) \\
&= g( J^2(u), J(v)) + ig( u,v) \\
&= g( -u, J(v)) + ig( u,v) \\
&= i(ig( u, J(v)) + g( u,v)) \\
&= ih(u,v).
\end{align*}
$$
</div>

We'll now extend these notions to the complexification $V_\Bbb C = V \otimes_\Bbb R \Bbb C$ of $V$. The inner product extends to a Hermitian inner product by

$$
g( u \otimes \lambda, v \otimes \mu) := \lambda\bar{\mu}g( u,v).
$$

<div class="lemma">
Let $(V, g)$ be a real vector space with a compatible almost complex structure $J$. Then
<ol>
    <li>
    The decomposition $V_\Bbb C = V^{1,0} \oplus V^{0,1}$ corresponding to the almost complex structure $J$ is orthogonal with respect to the Hermitian inner product $g_\Bbb C$.
    </li>
    <li>
    The fundamental form $\omega$ is of type $(1,1)$. That is $\omega \in \Lambda^{1,1}V^\ast_\Bbb C$.
    </li>
</ol>
</div>

<div class="proof">
<ol>
    <li>
    Pick $u \in V^{1,0}$ and $v \in V^{0,1}$. Then $J(u) = iu$ and $J(v) = -iv$. We have that

    $$
    \begin{align*}
    g( u, v) &= g( J(u), J(v)) \\
    &= g( iu, -iv) \\
    &= i^2g( u, v) \\
    &= -g( u, v),
    \end{align*}
    $$
    
    which implies that $g( u, v) = 0$.
    </li>
    <li>
    For any $u,v \in V^{1,0}$ we have that

    $$
    \begin{align*}
    \omega(u,v) &= g( J(u), v)\\
    &= g( J^2(u),J(v) ) \\
    &= \omega(J(u), J(v)) \\
    &= \omega(iu, iv) \\
    &= -\omega(u,v),
    \end{align*}
    $$

    implying that $\omega(u,v) = 0$ for $u,v \in V^{1,0}$. A similar calculation shows that $\omega(u,v) = 0$ for $u,v \in V^{0,1}$, hence $\omega$ is non-zero only on $V^{1,0} \oplus V^{0,1}$ and $V^{0,1} \oplus V^{1,0}$, i.e. $\omega \in \Lambda^{1,1}V^\ast_\Bbb C$. 

    </li>
</ol>
</div>

The following lemma describes the relationship of $h$ and $g$.

<div class="lemma">
Let $(V, g)$ be a real vector space with a compatible almost complex structure $J$. Under the isomorphism $(V,J) \cong (V^{1,0},i)$ we have that $h = g\vert_{V^{1,0}}$.
</div>

<div class="proof">
The isomorphism $(V,J) \cong (V^{1,0},i)$ is given by 

$$
v \mapsto \frac{1}{2}(v - iJ(v)).
$$

It follows that

$$
\begin{align*}
g(u - iJ(u),v - iJ(v)) &= g(u,v) + ig(u,J(v)) - ig(J(u),v) + g(J(u),J(v)) \\
&= 2g(u,v) + 2ig(u,J(v)) \\
&= 2h(u,v).
\end{align*}
$$

</div>

Note now that $g = \Re h = \frac{1}{2}(h +\bar{h})$ and $\omega = -\Im h = \frac{i}{2}(h - \bar{h})$. Choosing a $\Bbb C$-basis $z_1,\dots,z_n$ for $V^{1,0}$ gives the two expressions[^1]

$$
\begin{align*}
g &= \frac{1}{2}(h_{jk} z^j \otimes \bar{z}^k + h_{kj} \bar{z}^j \otimes z^k) \\
&= \frac{1}{2}h_{jk} (z^j \otimes \bar{z}^k + \bar{z}^k \otimes z^j),
\end{align*}
$$

and

$$
\begin{align*}
\omega &= \frac{i}{2}(h_{jk} z^j \otimes \bar{z}^k - h_{kj} \bar{z}^j \otimes z^k) \\
&= \frac{i}{2}h_{jk} (z^j \otimes \bar{z}^k - \bar{z}^k \otimes z^j) \\
&= \frac{i}{2}h_{jk} z^j \wedge \bar{z}^k,
\end{align*}
$$

which will be useful when we transition to manifolds and need local expressions. 

---

We'll now get to the actual point of this post.

<div class="definition">
Let $(V,g)$ be a real vector space equipped with an almost complex structure $J$, and suppose that $\omega$ is the associated fundamental form. Then the <b>Lefschetz operator</b> $L : \Lambda^\ast V^\ast_\Bbb C \to \Lambda^\ast V^\ast_\Bbb C$ is defined by $\alpha \mapsto \alpha \wedge \omega$.
</div>

---

[^1]: Note that I'm denoting the dual basis for $z_1,\dots,z_n$ as $z^1,\dots,z^n$.