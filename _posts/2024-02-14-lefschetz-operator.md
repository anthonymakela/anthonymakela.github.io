---
layout: post
title: "The Lefschetz Operator"
categories: [Complex Geometry, Differential Geometry, Linear Algebra]
mathjax: true
published: true
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
&= i(ig( u, J(v)) + g( u,v)) \\
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
J : \bigwedge^p V^{1,0} &\to \bigwedge^p V^{1,0} \\
v_1\wedge \dots \wedge v_p &\mapsto iv_1\wedge\dots\wedge iv_p = i^pv_1\wedge \dots \wedge v_p,
\end{align*}
$$

and

$$
\begin{align*}
J : \bigwedge^q V^{0,1} &\to \bigwedge^q V^{0,1} \\
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
    We've seen that $\omega$ is alternating and hence $\omega \in \bigwedge^2 V^\ast$. To see that $\omega \in \bigwedge^{1,1} V^\ast$, note that since $\omega \in \bigwedge^{2}V^\ast_\Bbb C = \bigwedge^{2,0}V^\ast \oplus \bigwedge^{1,1}V^\ast \oplus \bigwedge^{0,2}V^\ast$ we can write

    $$
    \omega = \omega^{2,0} + \omega^{1,1} + \omega^{0,2}.
    $$

    It suffices to show that $\omega^{2,0} = \omega^{0,2} = 0$. Since the extension of $J$ to $\bigwedge^2 V_\Bbb C$ gives us that \[J\omega(u,v) = \omega(Ju,Jv) = \omega(u,v)\] and $J\omega = -\omega^{2,0} + \omega^{1,1} -\omega^{0,2}$ we conclude that $\omega^{2,0} = \omega^{0,2} = 0$.
    </li>
</ol>
</div>

The following lemma describes the relationship of $h$ and $g$.

<div class="lemma">
Let $(V, g)$ be a real vector space with a compatible almost complex structure $J$. Under the isomorphism $(V,J) \cong (V^{1,0},i)$ we have that $\frac{1}{2}h = g\vert_{V^{1,0}}$.
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
Let $(V,\langle \cdot, \cdot \rangle)$ be a real vector space equipped with an almost complex structure $J$, and suppose that $\omega$ is the associated fundamental form. Then the <b>Lefschetz operator</b> $L : \bigwedge^\ast V^\ast_\Bbb C \to \bigwedge^\ast V^\ast_\Bbb C$ is defined by $\alpha \mapsto \alpha \wedge \omega$.
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

There is also an alternative proof for the above theorem using $\mathfrak{sl}(2)$-representations, but I find the one I gave much neater. When we eventually prove this on the cohomology on Kähler manifolds we obtain the so-called <b>Hard Lefschetz theorem</b>.

The Lefschetz operator comes along with its dual $\Lambda$ and in order to describe this, we need to remind ourselves about the Hodge $\star$-operator. Consider an oriented real inner product space $(V, \langle \cdot ,\cdot \rangle)$ of dimension $d$ with basis $e_1,\dots,e_d$, then $\langle \cdot, \cdot \rangle$ defines an inner product on all the exterior powers $\bigwedge^k V$ via

$$
\langle u_1 \wedge \dots \wedge u_k, v_1 \wedge \dots \wedge v_k\rangle := \det\left(\langle u_i, v_j \rangle\right).
$$

Let $\operatorname{vol} \in \bigwedge^d V$ be the orientation of $V$ of norm $1$ given by $\operatorname{vol} = e_1\wedge\dots\wedge e_d$. Then the Hodge $\star$-operator is a linear operator on the exterior algebra of $V$, mapping $k$-vectors to $(n - k)$-vectors, for $0 \le k \le d$. It has the following property which defines it completely[^2]

$$
\alpha \wedge \star \beta = \langle \alpha,\beta\rangle \operatorname{vol},
$$

for $\alpha, \beta \in \bigwedge^k V$. The following proposition summarizes the most important properties of the $\star$-operator.

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
    (\star \circ \star) \alpha = (-1)^{k(d-k)}\alpha.
    $$
    </li>
    <li>
    The $\star$-operator is an isometry on $\left(\bigwedge^\ast V, \langle \cdot, \cdot \rangle\right)$.
    </li>
</ol>
</div>

Coming back to the Lefschetz operator, let's now consider the dual $\Lambda$.

<div class="definition">
The dual Lefschetz operator $\Lambda$ is an operator 
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
&= L\beta \wedge \star\alpha \\
&= \omega \wedge \beta \wedge \star\alpha \\
&= \beta \wedge (\omega \wedge \star\alpha) \\
&= \langle \beta, \star^{-1}(L(\star\alpha))\rangle\operatorname{vol} \\
&= \langle \star^{-1}(L(\star\alpha),\beta)\rangle\operatorname{vol} .
\end{align*}
$$
</div>

The extensions of $L$ and $\Lambda$ are also formally adjoint to each other on $\bigwedge^\ast V^\ast_\Bbb C$ with respect to the extension of $\langle \cdot, \cdot\rangle_\Bbb C$ to $\bigwedge^\ast V^\ast_\Bbb C$. The lemma holds on $\bigwedge^\ast V^\ast_\Bbb C$ as well. Considering the $\star$-operator, on $\bigwedge^\ast V^\ast_\Bbb C$ we have

$$
\alpha \wedge \star\bar{\beta} = \langle \alpha,\beta\rangle_\Bbb C \operatorname{vol}.
$$

<div class="lemma">
Consider $\langle \cdot, \cdot\rangle_\Bbb C$, $\Lambda$ and $\star$ on $\bigwedge^\ast V^\ast_\Bbb C$. Then
<ol>
    <li>
    The decomposition $\bigwedge^k V^\ast_\Bbb C = \bigoplus_{p+q = k} \bigwedge^{p,q}V^\ast$ is orthogonal with respect to $\langle \cdot, \cdot\rangle_\Bbb C$.
    </li>
    <li>
    The $\star$-operator maps $\bigwedge^{p,q}V^\ast$ to $\bigwedge^{n-q,n-p}V^\ast$, where $n = \dim_\Bbb C V$.
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
    This follows quite directly from the orthogonality of $\langle \cdot, \cdot \rangle_\Bbb C$ with respect to $V^\ast_\Bbb C = V^\ast_{1,0} \oplus V^\ast_{0,1}$. It suffices to look at pure tensors. For $\alpha \in \bigwedge^{p,q}V^\ast$ and $\beta \in \bigwedge^{r,s}V^\ast$ with $p+q = r+ s = k$, but $(p,q) \ne (r,s)$, we can write 
    $$
    \alpha = \alpha^{1,0}_1\wedge \dots \wedge \alpha^{1,0}_p \wedge \alpha^{0,1}_1\wedge \dots \wedge \alpha^{0,1}_q
    $$
    as well as 
    $$
    \beta = \beta^{1,0}_1\wedge \dots \wedge \beta^{1,0}_r \wedge \beta^{0,1}_1\wedge \dots \wedge \beta^{0,1}_s.
    $$
    Now $\langle \alpha, \beta \rangle_\Bbb C$ is computed by taking the determinant of a matrix consisting of elements $\langle \alpha^{1,0}_i, \beta^{1,0}_j\rangle_\Bbb C, \langle \alpha^{1,0}_i, \beta^{0,1}_j\rangle_\Bbb C, \langle \alpha^{0,1}_i, \beta^{1,0}_j\rangle_\Bbb C$ and $\langle \alpha^{0,1}_i, \beta^{0,1}_j\rangle_\Bbb C$. Given the orthogonality of $\langle \cdot, \cdot \rangle_\Bbb C$ with respect to $V^\ast_\Bbb C = V^\ast_{1,0} \oplus V^\ast_{0,1}$, the terms of the form $\langle \alpha^{1,0}_i, \beta^{0,1}_j\rangle_\Bbb C$ and $\langle \alpha^{0,1}_i, \beta^{1,0}_j\rangle_\Bbb C$ will always vanish. Since $p \ne r$ or $q \ne s$, the matrix will always have either a row or a column full of zeros implying that $\langle \alpha,\beta\rangle_\Bbb C = 0$.
    </li>
    <li>
    Consider the expression $\alpha \wedge \star\bar{\beta} = \langle \alpha,\beta\rangle_\Bbb C \operatorname{vol}$. Note that both $\alpha$ and $\beta$ must be $(p,q)$-forms due to the orthogonality of the inner product. Suppose that $\star\bar{\beta}$ is of type $(r,s)$. Since the right-hand side is a form of type $(n,n)$ and $\bar{\beta}$ is of type $(q,p)$, we see that $q+r = n$ and $p+s = n$ yielding $r = n-q$ and $s = n-p$. That is $\star\bar{\beta}$ is of type $(n-q,n-p)$.
    </li>
    <li>
    Since $\Lambda = \star^{-1} \circ L \circ \star$, it maps a $(p,q)$-form to a $(n-q,n-p)$ first, then to a $(n-q+1,n-p+1)$-form and lastly $\star^{-1}$ maps the $(n-q+1,n-p+1)$-form to a form of type $(n-(n-p+1), n-(n-q+1)) = (p-1,q-1)$.
    </li>
</ol>
</div>

---

To properly motivate what's about to come we need to take a small detour on $\mathfrak{sl}(2,\Bbb C)$. Recall that  $\mathfrak{sl}(2,\Bbb C)$ is the Lie algebra of the group $\operatorname{SL}(2,\Bbb C)$ that is realized as the vector space of $2 \times 2$ complex matrices with trace zero together with the bracket

$$
[A,B] = AB -BA.
$$

The defining feature of $\mathfrak{sl}(2,\Bbb C)$ is that it contains a basis $e,h,f$ given by

$$
e = \begin{bmatrix}0&1\\0&0\end{bmatrix}, f = \begin{bmatrix}0&0\\1&0\end{bmatrix} \text{ and } h = {\begin{bmatrix}1&0\\0&-1\end{bmatrix}},
$$

satisfying

$$
[e,f] = h, [h,f] = -2f \text{ and } [h,e] = 2e.
$$

When we move from the linear algebra to the theory of compact Kähler manifolds, we will see that the representations of $\mathfrak{sl}(2,\Bbb C)$ will be of great interest.

---


We'll define one more operator on the exterior powers $\bigwedge^\ast V$ and then investigate the interplay between all of these operators we've defined.

<div class="definition">
Let $H : \bigwedge^\ast V \to \bigwedge^\ast V$ be the <i>counting operator</i> defined by
$$
H\vert_{\bigwedge^k V} = (k-n) \cdot \operatorname{id},
$$
where $\dim_\Bbb R = 2n$. Equivalently
$$
H = \sum_{k=0}^{2n} (k-n)\cdot \pi^k.
$$
</div>

Now one might ask questions about whether or not the operators $L, \Lambda$, and $H$ commute. They do not, but we can still compute their commutators.

<div class="proposition">
Let $(V, \langle \cdot, \cdot\rangle)$ be a finite-dimensional inner product space equipped with an almost complex structure. The operators $L, \Lambda$ and $H$ satisfy
$$
[L,\Lambda] = H, [H,\Lambda] = -2\Lambda \text{ and } [H,L] = 2L.
$$
</div>

<div class="proof">
For $\alpha \in \bigwedge^k V^\ast$ we have that
$$
\begin{align*}
[H,L]\alpha &= H(L(\alpha)) - L(H(\alpha)) \\
&= H(\omega \wedge \alpha) - L((k-n)\alpha) \\
&= (k+2-n)(\omega \wedge \alpha) - \omega \wedge ((k-n)\alpha) \\
&= \left((k+2-n) - (k-n)\right)\omega \wedge \alpha \\
&= 2\omega \wedge \alpha \\
&= 2L(\alpha).
\end{align*}
$$
This proves the last assertion. For the second one, we obtain
$$
\begin{align*}
[H,\Lambda]\alpha &= H(\Lambda(\alpha)) - \Lambda(H(\alpha)) \\
&= (k-2-n)\Lambda(\alpha) - \Lambda((k-n)\alpha) \\
&= \left((k-2-n) - (k-n)\right)\Lambda(\alpha) \\
&= -2\Lambda(\alpha),
\end{align*}
$$
proving the second assertion. The first one is a bit more trickier. We'll prove it by induction on the dimension of $V$. Suppose that $V = W_1 \oplus W_2$ is a decomposition that is compatible with the inner product and the almost complex structure. Then
$$
\bigwedge^\ast V^\ast = \bigwedge^\ast W_1^\ast \otimes \bigwedge^\ast W_2^\ast.
$$
The fundamental form $\omega$ on $V$ decomposes as $\omega = \omega_1 + \omega_2$, where $\omega_j \in W_j$. Thus $L = L_1 + L_2$ with $L_1$ acting as $L_1 \otimes 1$ and $L_2$ acting as $1 \otimes L_2$ on $\bigwedge^\ast W_1^\ast \otimes \bigwedge^\ast W_2^\ast$. For $\alpha,\beta \in \bigwedge^\ast V^\ast$ with $\alpha = \alpha_1 \otimes \alpha_2$ and $\beta = \beta_1 \otimes \beta_2$ we have that 
$$
\begin{align*}
\langle \alpha, L(\beta)\rangle &= \langle \alpha, L_1(\beta_1)\otimes \beta_2\rangle + \langle \alpha, \beta_1\otimes L(\beta_2)\rangle \\
&= \langle\alpha_1, L_1(\beta_1)\rangle\langle \alpha_2,\beta_2\rangle + \langle \alpha_1,\beta_1\rangle\langle \alpha_2,L_2(\beta_2)\rangle \\
&= \langle\Lambda_1(\alpha_1), \beta_1\rangle\langle \alpha_2,\beta_2\rangle + \langle \alpha_1,\beta_1\rangle\langle \Lambda_2(\alpha_2),\beta_2\rangle \\
&= \langle\Lambda_1(\alpha_1)\otimes \alpha_2, \beta_1\otimes \beta_2\rangle + \langle \alpha_1\otimes\Lambda_2(\alpha_2),\beta_1\otimes\beta_2\rangle \\
&= \langle \Lambda(\alpha), \beta\rangle.
\end{align*}
$$
Thus $\Lambda = \Lambda_1 + \Lambda_2$. This gives
$$
\begin{align*}
[L,\Lambda](\alpha_1 \otimes \alpha_2) &= (L_1 + L_2)(\Lambda_1(\alpha_1) \otimes \alpha_2 + \alpha_1 \otimes \Lambda_2(\alpha_2)) \\
&-(\Lambda_1 + \Lambda_2)(L_1(\alpha_1) \otimes \alpha_2 + \alpha_1 \otimes L_2(\alpha_2)) \\
&= [L_1,\Lambda_1](\alpha_1) \otimes \alpha_2 + \alpha_1 \otimes [L_2,\Lambda_2](\alpha_2).
\end{align*}
$$
By our inductive hypothesis, $[L_i,\Lambda_i] = H_i$, and so
$$
\begin{align*}
[L,\Lambda](\alpha_1 \otimes \alpha_2) &= H_1(\alpha_1) \otimes \alpha_2 + \alpha_1 \otimes H_2(\alpha_2) \\
&= (k_1-n_1)(\alpha_1 \otimes \alpha_2) + (k_2-n_2)(\alpha_1\otimes\alpha_2),
\end{align*}
$$
for $\alpha_j \in \bigwedge^{k_j}W_j^\ast$ and $n_j = \dim_\Bbb C W_j$. For the case with $\dim_\Bbb C V = 1$, given a basis $x_1,y_1$ of $V$ we have that
$$
\begin{align*}
\bigwedge^\ast V^\ast &= \bigwedge^0V^\ast \oplus \bigwedge^1V^\ast \oplus \bigwedge^2 V^\ast \\
&= \Bbb R \oplus (x^1\Bbb R \oplus y^1\Bbb R) \oplus \omega\Bbb R.
\end{align*}
$$
Also $L : \bigwedge^0 V^\ast \to \bigwedge^2 V^\ast$ and $\Lambda :  \bigwedge^2 V^\ast \to  \bigwedge^0 V^\ast$ are given by $1 \mapsto \omega$ and $\omega \mapsto 1$ respectively. It follows that
$$
[L,\Lambda]\vert_{\bigwedge^0 V^\ast} = -\Lambda \circ L \vert_{\bigwedge^0  V^\ast} = -\operatorname{id}.
$$
Also $[L,\Lambda]\vert_{\bigwedge^1 V^\ast} = 0$ and $[L,\Lambda]\vert_{\bigwedge^2 V^\ast} = \operatorname{id}$. Hence $[L,\Lambda]\vert_{\bigwedge^k V^\ast} = (k-1) \cdot \operatorname{id}$.
</div>

<div class="corollary">
Let $(V, \langle \cdot, \cdot\rangle)$ be a finite-dimensional inner product space with an almost complex structure. The action of $L,\Lambda$ and $H$ defines a natural $\mathfrak{sl}(2)$-representation on $\bigwedge^\ast V^\ast$.
</div>

<div class="proof">
This is seen by mapping the basis elements $e,h$, and $f$ by
$$
\begin{align*}
e &\mapsto L \\
f &\mapsto \Lambda \\
h &\mapsto H.
\end{align*}
$$
This gives a Lie algebra homomorphism $\mathfrak{sl}(2) \to \operatorname{End}\left(\bigwedge^\ast V^\ast\right)$. The $\mathfrak{sl}(2, \Bbb C)$-representation is obtained by tensoring with $\Bbb C$.
</div>

<div class="lemma">
For any $\alpha \in \bigwedge^kV^\ast$, we have that
$$
[L^i, \Lambda](\alpha) = i(k-n+i-1)L^{i-1}(\alpha).
$$
</div>

<div class="proof">
This can be deduced from inducting on $i$ as follows:
$$
\begin{align*}
[L^i,\Lambda](\alpha) &= L^i(\Lambda (\alpha)) - \Lambda(L^i(\alpha)) \\
&= L(L^{i-1}(\Lambda(\alpha))-\Lambda(L^{i-1}(\alpha))) + L(\Lambda(L^{i-1}(\alpha)))-\Lambda(L(L^{i-1}(\alpha))) \\
&= L[L^{i-1}, \Lambda](\alpha) + [L,\Lambda](L^{i-1}(\alpha)) \\
&= (i-1)(k-n + (i-1) - 1)L^{i-1}(\alpha) + (2i-2+k-n)L^{i-1}(\alpha) \\
&= i(k-n+i-1)L^{i-1}(\alpha).
\end{align*}
$$
</div>

<div class="definition">
Let $(V, \langle \cdot, \cdot\rangle)$ be a finite-dimensional inner product space equipped with an almost complex structure $J$. An element $\alpha \in \bigwedge^k V^\ast$ is called <b>primitive</b> if $\Lambda \alpha = 0$. The linear subspace of all primitive forms is denoted by $P^k \subset \bigwedge^k V^\ast$.
</div>

As before, the definition extends to the complexified version. We will now prove the infamous Lefschetz decomposition, but before we do that, we'll go over a small amount of representation theory of $\mathfrak{sl}(2,\Bbb C)$.

<div class="definition">
Let $\rho$ be a representation of $\mathfrak{sl}(2,\Bbb C)$ on a finite-dimensional vector complex space $V$. Let $V^\lambda$ denote the eigenvectors of $\rho(h)$ with eigenvalue $\lambda$. That is, for $\lambda \in \Bbb C$
$$
V^\lambda = \{v \in V \mid \rho(h)v = \lambda v\}.
$$
We say that a vector $v \in V^\lambda$ has weight $\lambda$. A vector $v \in V$ is said to be <b>primitive</b> of weight $\lambda$ if $v$ is non-zero, $v \in V^\lambda$ and $\rho(e)v = 0$.
</div>

<div class="lemma">
<ol>
    <li>
        The sum $\sum_{\lambda \in \Bbb C} V^\lambda$ is a direct sum.
    </li>
    <li>
        If $v$ is of weight $\lambda$, then $\rho(e)v$ is of weight $\lambda +2$ and $\rho(f)v$ is of weight $\lambda - 2$.
    </li>
</ol>
</div>

<div class="proof">
<ol>
    <li>
    Consider $\sum_{\lambda \in \Bbb C} v_\lambda = 0$, where $v_\lambda \in V^\lambda$ for each $\lambda$. The action of $\rho(h)$ on the sum $\sum_{\lambda \in \Bbb C} v_\lambda = 0$ gives
    $$
    \begin{align*}
    \rho(h)\left(\sum_{\lambda \in \Bbb C} v_\lambda\right) &= \sum_{\lambda \in \Bbb C} \rho(h)v_\lambda \\
    &= \sum_{\lambda \in \Bbb C} \lambda v_\lambda \\
    &= 0.
    \end{align*}
    $$
    Since the eigenvectors corresponding to distinct eigenvalues are linearly independent we conclude that $\lambda v_\lambda = 0$ which gives that $v_\lambda = 0$ for non-trivial eigenvalues.
    </li>
    <li>
    Note that
    $$
    \begin{align*}
    \rho(h)\rho(e)v &= (\rho(h)\rho(e) - \rho(e)\rho(h))v + \rho(e)\rho(h)v \\
    &= \rho([e,f])v + \lambda\rho(e)v \\
    &= \rho(2e)v + \lambda\rho(e)v \\
    &= (\lambda + 2)\rho(e)v.
    \end{align*}    
    $$
    Similarly $\rho(h)\rho(f)v = (\lambda -2)\rho(f)v$.
    </li>
</ol>
</div>

<div class="lemma">
Every representation of $\mathfrak{sl}(2,\Bbb C)$ on a finite-dimensional complex vector space has at least one primitive vector. 
</div>

<div class="proof">
Let $v_0$ be an eigenvector of $\rho(h)$, and consider the sequence of eigenvectors of $\rho(h)$ given by
$$
v_0, \rho(e)v_0,\rho(e)^2v_0,\dots,\rho(e)^nv_0,\dots
$$
By our previous lemma, the non-zero terms in the sequence are linearly independent since they are eigenvectors with differing eigenvalues. It follows that the sequence must terminate, and hence for some fixed $k$, $\rho(e)^kv_0 = 0, \rho(e)^{k-1}v_0 \ne 0$. Thus $v := \rho(e)^{k-1}v_0$ is primitive.
</div>

<div class="proposition">
Let $(V, \langle \cdot, \cdot\rangle)$ be a $2n$-dimensional inner product space equipped with an almost complex structure $J$. Then
<ol>
    <li>
    There exists a direct sum decomposition (<b>Lefschetz decomposition</b>) of the form:
    $$
    \bigwedge^k V^\ast = \bigoplus_{i \ge 0} L^i\left(P^{k-2i}\right)
    $$
    </li>
    <li>
    The map $L^{n-k} : P^k \to \bigwedge^{2n-k}V^\ast$ is injective for $k \le n$.
    </li>
    <li>
    If $k > n$, then $P^k = 0$.
    </li>
    <li>
    If $k \le n$, then $P^k = \{\alpha \in \bigwedge^kV^\ast \mid L^{n-k+1}\alpha = 0 \}$.
    </li>
</ol>
</div>

<div class="proof">
<ol>
    <li>
    To prove the first item, we will resort to using representation theory. Since $\bigwedge^k V^\ast_\Bbb C$ is a finite-dimensional $\mathfrak{sl}(2)$-representation, it decomposes as the direct sum of irreducible ones. Any finite-dimensional $\mathfrak{sl}(2)$-representation admits a primitive vector $\alpha$, i.e. $\Lambda \alpha = 0$. Since $[L^i, \Lambda](\alpha) = i(k-n+i-1)L^{i-1}(\alpha)$, for any primitive $\alpha$ the subspace $\alpha, L\alpha, L^2\alpha,\dots$ defines a subrepresentation. It follows that the irreducible $\mathfrak{sl}(2)$-representations are of this form, giving the desired decomposition.
    </li>
    <li>
    Let $0\ne\alpha \in P^k$, $k \le n$ and pick minimal $i > 0$ with $L^i\alpha = 0$. Then
    $$
    0 = [L^i, \Lambda](\alpha) = i(k-n+i-1)L^{i-1}(\alpha).
    $$
    Since $L^{i-1}(\alpha) \ne 0$ and $i > 0$ we have that $k-n+i-1 =0$. That is $i = n-k+1 > n-k$, so $L^{n-k}\alpha \ne 0$. Moreover, $L^{n-k+1} \alpha = 0$.
    </li>
    <li>
    If $\alpha \in P^k$, $k > n$ and $i > 0$ is minimal with $L^i\alpha = 0$, then
    $$
    0 = [L^i, \Lambda](\alpha) = i(k-n+i-1)L^{i-1}(\alpha).
    $$    
    Thus $k-n+i-1 = 0$, i.e. $i = n-k+1 \le 0$ contradicting $i > 0$. Thus $i = 0$.
    </li>
    <li>
    Suppose that $\alpha \in P^k$ with $k \le n$. We have already seen that $P^k \subset \ker\left(L^{n-k+1}\right)$. Conversely, suppose that $\alpha \in \ker\left(L^{n-k+1}\right)$. Then 
    $$
    \begin{align*}
    L^{n-k+2}(\Lambda(\alpha)) &= L^{n-k+2}(\Lambda(\alpha)) - \Lambda\left(L^{n-k+2}(\alpha)\right) \\
    &= (n-k+2)L^{n-k+1}(\alpha) \\
    &= 0.
    \end{align*}
    $$
    Now since $L^{n-k+2}$ is injective on $\bigwedge^{k-2}V^\ast$, we obtain that $\Lambda(\alpha) = 0$.
    </li>
</ol>
</div>

Roughly speaking, the operators $L$ and $\Lambda$ induce a reflection of $\bigwedge^\ast V^\ast$ in the middle exterior power $\bigwedge^n V^\ast$. However, as you might recall, there is another operator with the same property. The $\star$-operator works in the same way and the interplay between these is described in the following proposition which I won't prove here.

<div class="proposition">
For all $\alpha \in P^k$ one has
$$
\star L^j(\alpha) = (-1)^{\frac{k(k+1)}{2}}\frac{j!}{(n-k-j)!}L^{n-k-j}J(\alpha),
$$
where $J : \bigwedge^\ast V^\ast_\Bbb C \to \bigwedge^\ast V^\ast_\Bbb C$ is the natural multilinear extension of the almost complex structure to the exterior algebra given by $J = \sum_{p,q}i^{p-q}\pi^{p,q}$.
</div>

As an example of the usefulness of the above proposition, for $j=k=0$ and $\alpha = 1$ we obtain

$$
\star 1 = \frac{1}{n!}L^{n}1 = \frac{\omega^n}{n!}.
$$

That is, $\operatorname{vol} = \frac{\omega^n}{n!}$. Before we wrap this up, there is one more thing I would like to cover. In the near future, I would like to cover Hodge structures and when we talk about the Lefschetz theorems on compact Kähler manifolds, we'll prove something called the Hodge index theorem. There is a bilinear pairing that will be useful in both occasions given by the following definition.

<div class="definition">
Let $(V, \langle \cdot, \cdot\rangle)$ be a finite-dimensional inner product space equipped with an almost complex structure, and let $\omega$ be the fundamental form. The <b>Hodge-Riemann pairing</b> is the bilinear form
$$
\begin{align*}
Q : \bigwedge^{k}V^\ast \times \bigwedge^{k}V^\ast &\to \Bbb R \\
(\alpha,\beta) &\mapsto (-1)^{\frac{k(k-1)}{2}}\alpha\wedge\beta\wedge\omega^{n-k},
\end{align*} 
$$
where $\bigwedge^{2n}V^\ast$ is identified with $\Bbb R$ via the volume form.
</div>

By definition $Q = 0$ on $\bigwedge^k V^\ast$ for $k > n$. The complex extension will also be denoted by $Q$.

<div class="corollary">
Let $(V, \langle \cdot, \cdot\rangle)$ be a finite-dimensional inner product space equipped with an almost complex structure. Then the associated Hodge-Riemann pairing $Q$ satisfies:
$$
Q\left(\bigwedge^{p,q},\bigwedge^{r,s}\right) = 0
$$
for $(p,q) \ne (r,s)$. Also
$$
i^{p-q}Q(\alpha,\bar{\alpha}) = (n-(p+q))! \langle \alpha,\alpha\rangle_\Bbb C > 0,
$$
for $0 \ne \alpha \in P^{p,q}$ with $p+q \le n$.
</div>

<div class="proof">
The first assertion follows from considering types. For the second assertation, we have
$$
\begin{align*}
Q(\alpha,\bar{\alpha}) &= (-1)^{\frac{k(k-1)}{2}}\alpha\wedge\bar{\alpha}\wedge\omega^{n-k} \\
&= (-1)^{\frac{k(k-1)}{2}}\alpha\wedge L^{n-k}(\bar{\alpha}) \\
&= (-1)^{\frac{k(k-1)}{2}}\langle \alpha,\beta\rangle_\Bbb C \operatorname{vol}, 
\end{align*}
$$
where $k=p+q$ and $\beta \in \bigwedge^k V^\ast$ is such that $\star\bar{\beta} = L^{n-k}(\bar{\alpha})$. Now $\star^2\bar{\beta} = (-1)^k\bar{\beta}$, but on the other hand,
$$
\star^2 \bar{\beta} = \star L^{n-k}(\bar{\alpha}) = (-1)^{\frac{k(k+1)}{2}}(n-k)!i^{q-p}\bar{\alpha}.
$$
Thus $\beta = (-1)^{k + \frac{k(k+1)}{2}}(n-k)!i^{q-p}\alpha$ and therefore,
$$
Q(\alpha,\bar{\alpha}) = (-1)^{k + \frac{k(k+1)}{2} + \frac{k(k-1)}{2}}(n-k)! i^{q-p}\langle\alpha,\alpha\rangle_\Bbb C.
$$
This gives $i^{p-q}Q(\alpha,\bar{\alpha}) = (n-k)!\langle\alpha,\alpha\rangle_\Bbb C > 0$, for $0 \ne \alpha \in P^{p,q}$.
</div>

Most of the theory we've covered here is just linear algebra and tediuous calculations, but as mentioned, these will be useful later on when we consider the three operators $L, \Lambda$ and $H$ on a compact Kähler manifold.

---

[^1]: Note that I'm denoting the dual basis for $z_1,\dots,z_n$ as $z^1,\dots,z^n$.

[^2]: What this means is that if $\beta$ is a $k$-form, then $\star \beta$ is the <i>unique</i> $(n-k)$-form which satisfies $\alpha \wedge \star \beta = \langle \alpha,\beta\rangle \operatorname{vol}$.