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

Recall that $V_\Bbb C$ splits as $V^{1,0} \oplus V^{0,1}$ under the eigenspace decomposition associated to $J$. We define $\bigwedge^{p,q}V := \bigwedge^p V^{1,0} \otimes_\Bbb C \bigwedge^q V^{0,1}$. To emphasize, Both exterior products should be taken here as exterior products of complex vector spaces. Analogously we set $\bigwedge^{p,q} V^* := \bigwedge^pV^\ast_{1,0} \otimes_{\Bbb C} \bigwedge^qV^\ast_{0,1}$.

Given the endomorphism $J \in \operatorname{End}(V)$ we can extend this to $V_\Bbb C$ also by defining for $v = v^{1,0} + v^{0,1} \in V_\Bbb C$

$$
J(v) = iv^{1,0} + -iv^{0,1}.
$$

Or more succintly using the projection maps $\pi^{1,0} : V_\Bbb C \to V^{1,0}$ and $\pi^{0,1} : V_\Bbb C \to V^{0,1}$ 

$$
J = i\pi^{1,0} + -i\pi^{0,1}.
$$

Furthemore $J$ can be extend to $\bigwedge^p V^{1,0}$ and $\bigwedge^q V^{0,1}$ by

$$
\begin{align*}
J : \bigwedge^p V^{1,0} &\to \bigwedge^p V^{1,0} \\
v_1\wedge \dots \wedge v_p &\mapsto iv_1\wedge\dots\wedge iv_p = i^pv_1\wedge \dots \wedge v_p,
\end{align*}
$$

and

$$
\begin{align*}
J : \bigwedge^q V^{0,1} &\to \bigwedge^q V^{0,1} \\
v_1\wedge \dots \wedge v_q &\mapsto -iv_1\wedge\dots\wedge -iv_p = (-i^q)v_1\wedge \dots \wedge v_q.
\end{align*}
$$

Putting two and two together, we extend $J$ to $J : \bigwedge^{p,q}V \to \bigwedge^{p,q}V$ with

$$
\alpha \otimes \beta \mapsto i^p\alpha \otimes (-i)^q \beta = i^{p-q}(\alpha \otimes \beta),
$$

or more succintly $\bigwedge^{p,q}V \ni \omega \mapsto i^{p-q}\omega \in \bigwedge^{p,q}V$.

<div class="definition">
With respect to the direct sum decompositions \[\bigwedge^\ast V_\Bbb C = \bigoplus_{k=0}^n \bigwedge^k V_\Bbb C \cong \bigoplus_{k=0}^n \bigoplus_{p+q=k} \bigwedge^{p} V^{1,0} \otimes \bigwedge^{q} V^{0,1} = \bigoplus_{k=0}^n \bigoplus_{p+q=k} \bigwedge^{p,q}V \] we define the following projections: \[\pi^k : \bigwedge^\ast V_\Bbb C \to \bigwedge^k V_\Bbb C\] and \[\pi^{p,q}:\bigwedge^\ast V_\Bbb C \to \bigwedge^{p,q} V\] where the first one is given by \[\alpha = \sum_{k=0}^n \alpha_k \mapsto \alpha_k\] and the second one by \[\alpha = \sum_{k=0}^n \sum_{p+q=k} \alpha^{p,q} \mapsto \alpha^{p,q}.\]
</div>

We establish that the extension of $J$ to $\bigwedge^k V_\Bbb C \to \bigwedge^k V_\Bbb C$ is given by 

$$
\alpha = \sum_{p+q=k}\alpha^{p,q} \mapsto \sum_{p+q=k}i^{p-q}\alpha^{p,q}.
$$

<div class="lemma">
Let $(V, g)$ be a real vector space with a compatible almost complex structure $J$. Then
<ol>
    <li>
    The decomposition $V_\Bbb C = V^{1,0} \oplus V^{0,1}$ is orthogonal with respect to the Hermitian inner product $g$.
    </li>
    <li>
    The fundamental form $\omega$ is real and of type $(1,1)$. That is $\omega \in \bigwedge^2 V^\ast \cap \bigwedge^{1,1} V^\ast$.
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
    We've seen that $\omega$ is alternating and hence $\omega \in \bigwedge^2 V^\ast$. To see that $\omega \in \bigwedge^{1,1} V^\ast$, note that since $\omega \in \bigwedge^{2}V^\ast_\Bbb C = \bigwedge^{2,0}V^\ast \oplus \bigwedge^{1,1}V^\ast \oplus \bigwedge^{0,2}V^\ast$ we can write

    $$
    \omega = \omega^{2,0} + \omega^{1,1} + \omega^{0,2}.
    $$

    It suffices to show that $\omega^{2,0} = \omega^{0,2} = 0$. Since the extension of $J$ to $\bigwedge^2 V_\Bbb C$ gives us that \[J\omega(u,v) = \omega(Ju,Jv) = \omega(u,v)\] and $J\omega = -\omega^{2,0} + \omega^{1,1} -\omega^{0,2}$ we conclude that $\omega^{2,0} = \omega^{0,2} = 0$.
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
Let $(V,g)$ be a real vector space equipped with an almost complex structure $J$, and suppose that $\omega$ is the associated fundamental form. Then the <b>Lefschetz operator</b> $L : \bigwedge^\ast V^\ast_\Bbb C \to \bigwedge^\ast V^\ast_\Bbb C$ is defined by $\alpha \mapsto \alpha \wedge \omega$.
</div>

We immediately see that $L$ is the $\Bbb C$-linear extension of the real operator $\bigwedge^\ast V^\ast \to \bigwedge^\ast V^\ast$ sending $\alpha \mapsto w\wedge \alpha$. Also, since we can choose an orthonormal basis $z_1,\dots,z_n$ for $V_\Bbb C$ and write

$$
\omega = \frac{i}{2}\sum_{i} z^i \wedge \bar{z}^i,
$$

then for $\alpha \in \bigwedge^{p,q}V^\ast$ we have that $(z^i \wedge \bar{z}^i) \wedge \alpha \in \bigwedge^{p+1,q+1}V^\ast$. It follows that

$$
L\left(\bigwedge^{p,q}V^\ast\right) \subset \bigwedge^{p+1,q+1}V^\ast,
$$

i.e. $L$ is of bidegree $(1,1)$.

<div class="theorem">
Suppose that $\dim_\Bbb R V = 2n$. Then, for $1 \le k \le n$, the Lefschetz operator 

$$
\begin{align*}
L^k : \bigwedge^{n-k} V^\ast &\to \bigwedge^{n+k} V^\ast \\
\alpha &\mapsto \omega^k \wedge \alpha,
\end{align*}
$$

is an isomorphism.

</div>

<div class="proof">
It's sufficient to show that $L^k$ is injective since the domain and codomain are of equal dimension. The proof is done by inducting backwards starting with $k = n$. Recall that $\omega^n = n!\operatorname{vol}$ and $L^n$ is injective for obvious reasons. Suppose now that the result holds for $k$ and that $L^{k-1}(\alpha) = \omega^{k-1}\wedge \alpha = 0$, for $\alpha \in \bigwedge^{n-(k-1)}V^\ast$. Since $\omega^k \wedge \alpha = 0$, for any $v \in V$ we obtain

$$
\begin{align*}
0 &= \iota_v(\omega^k \wedge \alpha) \\
&= \iota_v(\omega^k) \wedge \alpha + \omega^k \wedge \iota_v(\alpha) \\
&= k \iota_v(\omega) \wedge \omega^{k-1} \wedge \alpha + \omega^k \wedge \iota_v(\alpha) \\
&= \omega^k \wedge \iota_v(\alpha),
\end{align*}
$$

and so $L^k(\iota_v(\alpha)) = \omega^k \wedge \iota_v(\alpha) = 0$ which in turn gives that $\iota_v(\alpha) = 0$ by the injectivity of $L^k$. Since $\iota_v(\alpha) = 0$ for every $v \in V$, we conclude that $\alpha = 0$ which completes the proof.

</div>

There is also an alternative proof for the above theorem using $\mathfrak{sl}(2)$-representations, but I find the one I gave much neater.

The Lefschetz operator comes along with its dual $\Lambda$ and in order to describe this, we need to remind ourselves about the Hodge $\star$-operator. Consider an oriented real inner product space $(V, \langle \cdot ,\cdot \rangle)$ of dimension $d$ with basis $e_1,\dots,e_d$, then $\langle \cdot, \cdot \rangle$ defines an inner product on all the exterior powers $\bigwedge^k V$ via

$$
\langle u_1 \wedge \dots \wedge u_k, v_1 \wedge \dots \wedge v_k\rangle := \det\left(\langle u_i, v_j \rangle\right).
$$

Let $\operatorname{vol} \in \bigwedge^d V$ be the orientation of $V$ of norm $1$ given by $\operatorname{vol} = e_1\wedge\dots\wedge e_d$. Then the Hodge $\star$-operator is a linear operator on the exterior algebra of $V$, mapping $k$-vectors to $(n - k)$-vectors, for $0 \le k \le d$. It has the following property which defines it completely[^2]

$$
\alpha \wedge \star \beta = \langle \alpha,\beta\rangle \operatorname{vol},
$$

for $\alpha, \beta \in \bigwedge^k V$. The following proposition summarizes the most important properties of the $\star$-operator.

<div class="proposition">
Let $(V, \langle \cdot ,\cdot \rangle)$ be an oriented inner product of dimension $d$ with basis $e_1,\dots,e_d$ and let $\operatorname{vol} \in \bigwedge^d V$ be the volume form given by $e_1\wedge\dots\wedge e_d$. Then

<ol>
    <li>
    If $\{i_1,\dots,i_k,j_1,\dots,j_{d-k} \} = \{1,\dots,d\}$ we have that
    $$
    \star(e_{i_1}\wedge \dots \wedge e_{i_k}) = \varepsilon \cdot e_{j_1}\wedge \dots \wedge e_{j_{d-k}},
    $$
    where $\varepsilon = \operatorname{sgn}(i_1,\dots,i_k, j_1,\dots,j_{d-k})$.
    </li>
    <li>
    The $\star$-operator is self-adjoint up to sign: For $\alpha \in \bigwedge^k V$ one has
    $$
    \langle \alpha, \star\beta\rangle = (-1)^{k(d-k)}\langle \star \alpha, \beta\rangle.
    $$
    </li>
    <li>
    The $\star$-operator is involutive up to sign: 
    $$
    (\star \circ \star) \alpha = (-1)^{k(d-k)}\alpha.
    $$
    </li>
    <li>
    The $\star$-operator is an isometry on $\left(\bigwedge^\ast V, \langle \cdot, \cdot \rangle\right)$.
    </li>
</ol>
</div>

Coming back to the Lefschetz operator, let's now consider the dual $\Lambda$.

<div class="definition">
The dual Lefschetz operator $\Lambda$ is a the operator 
$$
\Lambda : \bigwedge^\ast V^\ast \to \bigwedge^\ast V^\ast
$$
that is adjoint to $L$ with respect to $\langle \cdot, \cdot \rangle$. That is, for $\alpha \in \bigwedge^\ast V^\ast$, $\Lambda \alpha$ is uniquely determined by the condition
$$
\langle \Lambda \alpha, \beta\rangle = \langle \alpha, L\beta\rangle,
$$
for all $\beta \in \bigwedge^\ast V^\ast$.
</div>

The $\Bbb C$-linear extension of $\Lambda$ to $\bigwedge^\ast V^\ast_\Bbb C$ will also be denoted by $\Lambda$. The following lemma will tie together the relationship between $L, \Lambda$ and the $\star$-operator.

<div class="lemma">
The dual Lefschetz operator $\Lambda$ is of degree $-2$, that is
$$
\Lambda\left(\bigwedge^k V^\ast\right) \subset \left(\bigwedge^{k-2} V^\ast\right). 
$$
Moreover, we have that
$$
\Lambda = \star^{-1} \circ L \circ \star.
$$
</div>

<div class="proof">
Using the definition for $\star$, we obtain

$$
\begin{align*}
\langle \alpha, L\beta \rangle\operatorname{vol} &= \langle L\beta, \alpha \rangle\operatorname{vol} \\
&= L\beta \wedge \star\alpha \\
&= \omega \wedge \beta \wedge \star\alpha \\
&= \beta \wedge (\omega \wedge \star\alpha) \\
&= \langle \beta, \star^{-1}(L(\star\alpha))\rangle\operatorname{vol} \\
&= \langle \star^{-1}(L(\star\alpha),\beta)\rangle\operatorname{vol} .
\end{align*}
$$
</div>

The extensions of $L$ and $\Lambda$ are also formally adjoint to each other on $\bigwedge^\ast V^\ast_\Bbb C$ with respect to the extension of $\langle \cdot, \cdot\rangle_\Bbb C$ to $\bigwedge^\ast V^\ast_\Bbb C$. The lemma holds on $\bigwedge^\ast V^\ast_\Bbb C$ as well.

<div class="lemma">
Consider $\langle \cdot, \cdot\rangle_\Bbb C$, $\Lambda$ and $\star$ on $\bigwedge^\ast V^\ast_\Bbb C$. Then
<ol>
    <li>
    The decomposition $\bigwedge^k V^\ast_\Bbb C = \bigoplus_{p+q = k} \bigwedge^{p,q}V^\ast$ is orthogonal with respect to $\langle \cdot, \cdot\rangle_\Bbb C$.
    </li>
    <li>
    The $\star$-operator maps $\bigwedge^{p,q}V^\ast$ to $\bigwedge^{n-p,n-q}V^\ast$, where $n = \dim_\Bbb C V$.
    </li>
    <li>
    The operator $\Lambda$ is of bidegree $(-1,-1)$. That is
    $$
    \Lambda\left(\bigwedge^{p,q}V^\ast\right) \subset \bigwedge^{p-1,q-1}V^\ast.
    $$
    </li>
</ol>
</div>

<div class="proof">
<ol>
    <li>

    </li>
</ol>
</div>

---

[^1]: Note that I'm denoting the dual basis for $z_1,\dots,z_n$ as $z^1,\dots,z^n$.

[^2]: What this means is that if $\beta$ is a $k$-form, then $\star \beta$ is the <i>unique</i> $(n-k)$-form which satisfies $\alpha \wedge \star \beta = \langle \alpha,\beta\rangle \operatorname{vol}$.