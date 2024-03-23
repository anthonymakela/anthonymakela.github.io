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

To set the stage, fix a real finite-dimensional inner product space $(V,\langle \cdot, \cdot \rangle)$ and let $J \in \operatorname{End}(V)$ be an almost complex structure.

<div class="definition">
The almost complex structure $J$ is compatible with the inner product $g$ if 

$$
\langle u, v \rangle = \langle J(u), J(v)\rangle,
$$

for all $u,v \in V$.
</div>


<div class="definition">
The <b>fundamental form</b> associated to $(V,\langle \cdot, \cdot \rangle,J)$ is the form given by

$$
\omega(u,v) := \langle J(u), v\rangle.
$$

</div>

Note that the fundamental form is antisymmetric as:

$$
\begin{align*}
\omega(u,v) &= \langle J(u),v\rangle \\
&= \langle J^2(u), J(v)\rangle \\
&= \langle -u, J(v)\rangle \\
&= -\langle u,J(v)\rangle \\
&= -\langle J(v), u\rangle \\
&= -\omega(v,u).
\end{align*}
$$

We'll now extend these notions to the complexification $V_\Bbb C = V \otimes_\Bbb R \Bbb C$ of $V$. The inner product extends to a Hermitian inner product by

$$
\langle u \otimes \lambda, v \otimes \mu\rangle_\Bbb C := \lambda\bar{\mu}\langle u,v\rangle.
$$

<div class="lemma">
Let $(V,\langle \cdot, \cdot \rangle,J)$ be a real vector space endowed with a compatible complex structure. Then the form 

$$
(u, v) := \langle u, v\rangle - i\omega(u,v),
$$

is a positive Hermitian form on $(V,J)$.
</div>

<div class="proof">
For $u,v,w \in V$ and $a,b \in \Bbb R$ we have that

$$
\begin{align*}
(au + bv, w) &= \langle au + bv, w\rangle - i\omega(au + bv, w) \\
&= a\langle u , w\rangle + b\langle v,w\rangle -i\langle J(au + bv), w\rangle \\
&= a\langle u , w\rangle + b\langle v,w\rangle -i\langle aJ(u) + bJ(v), w\rangle \\
&= a\langle u , w\rangle + b\langle v,w\rangle -i(a\langle J(u), w\rangle +  b\langle J(v), w\rangle) \\
&= a(\langle u, w\rangle -i \langle J(u), w\rangle) + b(\langle v,w\rangle - i\langle J(v), w\rangle) \\
&= a(u,w) + b(v,w),
\end{align*}
$$

which proves $\Bbb R$-linearity. Also $(u,v) = \overline{(v,u)}$ since $\omega$ is antilinear. Lastly

$$
\begin{align*}
(J(u), v) &= \langle J(u), v \rangle - i\omega(J(u), v) \\
&= \langle J(u), v \rangle + i\langle u,v\rangle \\
&= \langle J^2(u), J(v)\rangle + i\langle u,v\rangle \\
&= 
\end{align*}
$$

</div>