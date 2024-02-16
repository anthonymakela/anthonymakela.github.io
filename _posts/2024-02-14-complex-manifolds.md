---
layout: post
title: "Complex Manifolds"
categories: [Complex Geometry]
mathjax: true
published: false
excerpt_separator: <!--more-->
---

We are currently about to start a small reading group with a bunch of fellow students on Complex Geometry and Kähler Manifolds. I, having background on the topic already, thought it would be a good idea to write about it here. I'll be mostly writing about the material, but occasionally might delve deeper into some subtleties that might occur in our discussions.

<!--more-->

The thing that makes the theory of complex manifolds interesting is the rigidness of holomorphic functions compared to smooth functions. This in turn makes the theory drastically different. For example, there is no analogue for the Whitney embedding theorem in the complex case since the only connected, compact submanifold that embeds holomorphically in $\Bbb C^n$ is a point. Compact complex manifolds are much closer to algebraic varieties than to smooth manifolds.

---

Let's begin by recalling some notions of holomorphic functions of several variables. Let $\Bbb C$ denote the complex plane and $\Bbb C^n$ the $n$-dimensional complex space. Topologically $\Bbb C^n$ is $2n$-dimensional and can be identified with $\Bbb R^{2n}$ in the following way: if $(z_1,\dots,z_n) \in \Bbb C^n$ and if $z_j = x_j + iy_j$, then $(z_1,\dots,z_n)$ is identified with $(\Re z_1, \Im z_1, \dots \Re z_n, \Im z_n)$.

<div class="definition">
A function $f : U \to \Bbb C$ defined on an open subset $U$ of $\Bbb C^n$ is <i>holomorphic</i> if $f$ considered as a function from $U \subset \Bbb R^{2n}$ to $\Bbb R^2$ is smooth and satisfies the Cauchy-Riemann equations: \[\frac{\partial \Re f}{\partial x_j} = \frac{\partial \Im f}{\partial y_j} \ \text{ and } \ \frac{\partial \Re f}{\partial y_j} = -\frac{\partial \Im f}{\partial x_j}\] for all $j \in \{1,\dots,n\}$.
</div>


A mapping $f : U \to \Bbb C^m$ is <i>holomorphic</i> if each component of $f = (f_1,\dots,f_m)$ is holomorphic. A convenient way to state holomorphicity is to define[^1] 

$$
\frac{\partial}{\partial z_j} = \frac{1}{2}\left( \frac{\partial}{\partial x_j} - i \frac{\partial}{\partial y_j} \right) \ \text{ and } \ \frac{\partial}{\partial \bar{z}_j} = \frac{1}{2}\left( \frac{\partial}{\partial x_j} + i \frac{\partial}{\partial y_j} \right).
$$
 
Now holomorphicity of $f$ is equivalent with $\frac{\partial}{\partial \bar{z}_j} = 0$ for all $j$. 


Multiplication by $i$ i.e. $(z_1,\dots, z_n) \mapsto (iz_1,\dots, iz_n)$ defines a map $\Bbb C^n \to \Bbb C^n$ which squares to multiplication by $-1$. This induces a real linear map $J \in \operatorname{End}(\Bbb R^{2n})$ whose composition with itself is again multiplication by $-1$. It turns out that this is an effective way to characterize holomorphic mappings since we have the following:

<div class="lemma">
A map $f : U \subset \Bbb C^n \to \Bbb C^m$ that is smooth when considered as a map $U \subset \Bbb R^{2n} \to \Bbb R^{2m}$ is <i>holomorphic</i> if and only if 

$$
df \circ J_{\Bbb R^{2n}} = J_{\Bbb R^{2m}}\circ df
$$

where $df$ is the real Jacobian of $f$.
</div>

<div class="proof">
Writing $f(z) = (f_1(z),\dots, f_m(z))$ the Jacobian takes the form 

$$
df = \begin{pmatrix}
    \frac{\partial \Re f_1}{\partial x_1} & \frac{\partial \Re f_1}{\partial y_1} & \cdots & \frac{\partial \Re f_m}{\partial y_n} \\
    \frac{\partial \Im f_1}{\partial x_1} &\frac{\partial \Im f_1}{\partial y_1} & \cdots & \frac{\partial \Im f_m}{\partial y_n} \\
    \vdots & \vdots & \ddots & \vdots \\
    \frac{\partial \Im f_m}{\partial x_1} & \frac{\partial \Im f_m}{\partial y_1} & \cdots & \frac{\partial \Im f_m}{\partial y_n} \\
\end{pmatrix}
$$

and the matrix corresponding to $J_{\Bbb R^{2m}}$ is given by 

$$
J_{\Bbb R^{2m}}={\begin{pmatrix}0&-1\\1&0\\&&0&-1\\&&1&0\\&&&&\ddots \\&&&&&\ddots \\&&&&&&0&-1\\&&&&&&1&0\end{pmatrix}}.
$$

Similarly for $J_{\Bbb R^{2n}}$. Now it's a simple matter of matrix multiplication which shows that $df \circ J_{\Bbb R^{2n}} = J_{\Bbb R^{2m}}\circ df$ if and only if the Cauchy-Riemann equations are satisfied.
</div>


<div class="corollary">
Let $U$ be an open subset of $\Bbb C^n$. If $f : U \to \Bbb C^n$ is holomorphic and homeomorphic onto it's image considered as a map $\Bbb R^{2n} \to \Bbb R^{2n}$, then $f^{-1} : f(U) \to \Bbb C^n$ is holomorphic.
</div>

Let $r = (r_1,r_2, \dots, r_n)$ be an $n$-tuple of positive real numbers called a radius. Let $w = (w_1,\dots, w_n)$. The <i>polydisc</i> of radius $r$ centered at $w$ is defined to be 

$$
\begin{align*}
    \Delta_r(w) &=  \{z \in \mathbb{C}^n \mid |z_i - w_i| < r_i \} \\
    &= \{z \in \mathbb{C}^n \mid |z-w| < r\}.
\end{align*}
$$

So a polydisc is just a Cartesian product of ordinary discs.


<div class="proposition">
Let $U \subset \Bbb C^n$ be a domain, $f : U \to \Bbb C$ a holomorphic function and suppose that $f\vert_V \equiv 0$ for some non-empty open subset $V \subset U$. Then $f \equiv 0$.
</div>

<div class="proof">
Suppose that $Z$ is the set where the derivatives of $f$ are zero, then $V \subset Z$ so $Z$ is non-empty. The set $Z$ is closed in $U$ as an intersection of closed sets. Let $z_0 \in Z$ and expand $f$ as a power series around $z_0$ in a polydisc $\Delta_r(z_0) \subset U$. Since the coefficients are 
$$
    a_{i_1,\dots,i_n} = \frac{1}{i_1!\cdots i_n!} \frac{\partial^{i_1+\dots+i_n} f}{\partial^{i_1}z_1\cdots \partial^{i_n}z_n}
$$
we have that $f \equiv 0$ in $\Delta_r(z_0)$ so $Z$ is open. Since $U$ is connected $Z = U$.
</div>

<div class="proposition">
Let $U \subset \mathbb{C}^n$. If $f : U \to \Bbb C$ is holomorphic and if $|f|$ has a local maximum at $p \in \Delta$, then $f$ is constant on $U$.
</div>

<div class="proof">
Suppose that $f$ attains a local maximum at $p \in U$. Consider the polydisc $\Delta = \Delta_1 \times \dots \times \Delta_n \subset U$ centered at $p$. The function
$$
    z_1 \mapsto f(z_1,p_2,\dots,p_n)
$$
is holomorphic on $\Delta_1$ and attains a maximum at the center. It is therefore constant by the maximum modulus principle on one variable. Iterating this procedure we have that $f(z) = f(p)$ for all $z \in \Delta$ and so  by the identity theorem $f(z) = f(p)$ for all $z \in U$.
</div>

A powerful result on for holomorphic functions of several variables is the so called Hartog's theorem. 

<div class="proposition">
Let $\Delta$ be a polydisc in $\Bbb C^n$ with $n \ge 2$ and let $K \subset \Delta$ be a compact set. If $f : \Delta \setminus K \to \Bbb C$ is holomorphic, then there exists a holomorphic function $\tilde{f} : \Delta \to \Bbb C$ extending $f$.
</div>


If $f :\Delta \to \Bbb C$ is a holomorphic function on a polydisc in $\Bbb C^n$ with $n \ge 2$, then the above proposition implies that $f$ cannot have an isolated singularity, nor an isolated zero since otherwise $1/f$ would have an isolated singularity. Generally the zero set of $f$ cannot be compact and cannot be contained in a set of complex codimension greater than one.

---

To harness the tools of differential geometry and bundle theory for examining complex manifolds, we should frame holomorphic atlases using the language of bundle theory. Initially, we focus on "pointwise" objects by transforming real linear algebra data into complex linear algebra. Subsequently, we extend these methods to tensor bundles on smooth manifolds that have specific supplementary structures.


Let's first recall the notion of extension of coefficients from module theory. Let $R$ and $S$ be rings and $f : R \to S$ a ring homomorphism. We can now think of $S$ as an $R$-module simply by defining 

$$
rs = f(r)s.
$$

If $M$ is any $R$-module, we can now form the tensor product

$$
M_S = M \otimes_{R} S
$$

where $S$ is regarded as an $R$-module via $f$. $M^S$ is now an $S$-module since it inherits a ring action from $S$ given by

$$
(m \otimes s)s' =  m \otimes ss'.
$$

We can use this now to complexify a real vector space $V$. Simply consider the inclusion $i : \Bbb R \hookrightarrow \Bbb C$ and $V$ as an $\Bbb R$-vector space and define $V_\Bbb C = V \otimes_{\Bbb R} \Bbb C$. The action of a complex number $\lambda$ is now given by $(v \otimes \alpha)\lambda = v \otimes \alpha\lambda$.

<div class="lemma">
If $V$ is a real vector space with $\dim_\Bbb R V = n$ and $\{e_1,\dots, e_n\}$ is a basis for $V$, then $\dim_\Bbb C V_\Bbb C = n$ and $\{e_1 \otimes 1, \dots, e_n \otimes 1\}$ is a basis for $V_\Bbb C$ as a complex vector space. Considered as a real vector space $V_\Bbb C$ has dimension $2n$ and $\{e_1 \otimes 1, \dots, e_n \otimes 1, e_1 \otimes i, \dots, e_n \otimes i\}$ is a real basis for $V_\Bbb C$.
</div>

<div class="proof">
Recall that if $V$ and $W$ are finite-dimensional vector spaces with bases $\{v_1,\dots,v_n\}$ and $\{w_1,\dots,w_m\}$, the the tensor product $V \otimes W$ has a basis $\{v_i \otimes w_j \mid 1 \le i \le n, 1 \le j \le m \}$. The tensor product $V \otimes_{\Bbb R} \Bbb C$ thus has a basis $\{e_1 \otimes 1, \dots, e_n \otimes 1, e_1 \otimes i, \dots, e_n \otimes i\}$. 

Considering this now as a complex vector space, note that the vectors $e_1 \otimes i, \dots, e_n \otimes i$ are redundant. Indeed $e_j \otimes i = i(e_j \otimes 1)$.
</div>

Maybe it's worth noting that for an arbitary vector $v \in V_\Bbb C$ we have

$$
\begin{align*}
v &= \sum_{j=1}^n \lambda_j(e_j \otimes 1) \\
&= \sum_{j=1}^n(x_j + iy_j)(e_j \otimes 1) \\
&= \sum_{j=1}^n x_j(e_j \otimes 1) + \sum_{j=1}^n y_j(e_j \otimes i) \\
&= \sum_{j=1}^n x_je_j \otimes 1 + \sum_{j=1}^n y_je_j \otimes i \\
&= v_1\otimes 1 + v_2 \otimes i
\end{align*}
$$

where $v_1 = \sum_{j=1}^n = x_je_j$ and $v_2 = \sum_{j=1}^n y_je_j$ are vectors in $V$.

Note also that $V \subset V_\Bbb C$ is the part that is left invariant under complex conjugation on $V_\Bbb C$ which is defined by $\overline{v \otimes \lambda} := v \otimes \overline{\lambda}$

Here is a slightly different viewpoint.

<div class="definition">
If $V$ is a real finite-dimensional vector space, an endomorphism $J : V \to V$ with $J^2 = -\operatorname{id}$ is called an <i>almost complex structure</i> on $V$.
</div>

If $V$ is the real vector space underlying a complex vector space, then $v \mapsto iv$ defines an almost complex structure $J$ on $V$. The converse is true also:

<div class="lemma">
If $J$ is an almost complex structure on a real vector space $V$, then $V$ admits in a natural way the structure of a complex vector space.
</div>

<div class="proof">
The $\Bbb C$-module structure on $V$ is defined by

$$
(x+iy)v = xv + yJ(v),
$$
where $x,y \in \Bbb R$. The $\Bbb R$-linearity of $J$ and the assumption $J^2 = -\operatorname{id}$ yields that $((x+iy)(z+iw))v = (x+iy)((z+iw)v)$ and in particular $i(iv)=-v$.
</div>

Now if $V$ is endowed with an almost complex structure $J$ we denote the extension to $V_\Bbb C \to V_\Bbb C$ also via $J$ i.e. the map $J(v + iw) = J(v) + iJ(w)$.  Note that if $J(v) = \lambda v$, then $J(J(v)) = J(\lambda v) \implies -v = \lambda^2v$ i.e. the eigenvalues of $J$ are $\pm i$.

<div class="definition">
Let $J$ be an almost complex structure on $V$ and let $J : V_\Bbb C \to V_\Bbb C$ be it's $\Bbb C$-linear extension. Then the eigenspaces corresponding to $\pm i$ are denoted by \begin{align*}
    V^{1,0} &= \{ v\in V_\Bbb C \mid J(v) = iv \} \\
    V^{0,1} &=\{ v\in V_\Bbb C \mid J(v) = -iv \}.
\end{align*} 
</div>

<div class="lemma">
Let $V$ be a real vector space with an almost complex structure $J$. Then $V_\Bbb C = V^{1,0} \oplus V^{0,1}.$
</div>

<div class="proof">
Note that $V^{1,0} \cap V^{0,1} = 0$ so the map $\alpha: V^{1,0} \oplus V^{0,1} \to V_\Bbb C$ given by $(v,w) \mapsto v+w$ is injective. Now to see that this is an isomorphism we need a map $\beta : V_\Bbb C \to V^{1,0} \oplus V^{0,1}$ such that $\alpha \circ \beta = \operatorname{id}$. To find $\beta$ let $\beta(v) = (a,b) \in V^{1,0} \oplus V^{0,1}$. We want $a$ and $b$ such that $a + b = v$, but we also know that $J(a) = ia$ and $J(b) = -ib$ and these give that $J(a+b) = J(v) \implies J(a) + J(b) = ia - ib = J(v) \implies b - a    = iJ(v)$. So given \begin{align*}
    a + b &= v \\
    b - a &= J(v)
\end{align*}
we just solve for $a$ and $b$ to get $a = \frac{1}{2}(v-iJ(v))$ and $b = \frac{1}{2}(v + iJ(v))$. Thus $\beta(v) = (\frac{1}{2}(v-iJ(v)), \frac{1}{2}(v + iJ(v)))$ is our desired inverse.
</div>

I'll leave it for the reader to verify that the dual space $V^\ast_\Bbb C = \operatorname{Hom}_\Bbb R(V, \Bbb C)$ has a natural almost complex structure that gives similar eigenspace decomposition.

An algebra $A$ is a vector space over a field equipped with a bilinear product $\mu : A \times A \to A$. We say that an algebra $A$ over a field $k$ is <i>graded</i> if it can be written as a direct sum $A = \bigoplus_{k=0}^\infty A^k$ of vector spaces over $k$ such that the multiplication map sends $A^k \times A^\ell$ to $A^{k + \ell}$. The notation $A = \bigoplus_{k=0}^\infty A^k$ means that each non-zero element of $A$ is uniquely a finite sum $a = a_{i_1} + \dots +a_{i_m}$ where $a_{i_j} \ne 0 \in A^{i_j}.$


If $V$ is a real vector space with $\dim V = n$, then the exterior algerba $\bigwedge^\ast V$ naturally decomposes as $\bigoplus_{k=0}^n \bigwedge^kV$. Similarly $\bigwedge^\ast V_\Bbb C = \bigoplus_{k=0}^n \bigwedge^k V_\Bbb C$.

If $V$ is endowed with an almost complex structure, then $n$ is even, say $n = 2m$ and so $V_\Bbb C$ decomposes as above with $V_\Bbb C = V^{1,0} \oplus V^{0,1}$ where both $V^{1,0}$ and $V^{0,1}$ are of dimension $m$.

We now have the following 

$$
\bigwedge^k V_\Bbb C = \bigwedge^k V^{1,0} \oplus V^{0,1} = \bigoplus_{p+q=k} \bigwedge^p V^{1,0} \otimes \bigwedge^q V^{0,1}
$$

via the isomorphism $\bigoplus_{p+q=k} \bigwedge^p V^{1,0} \otimes \bigwedge^q V^{0,1} \to \bigwedge^k V_\Bbb C$ sending 

$$
(v_1 \wedge \dots \wedge v_p) \otimes (w_1 \wedge \dots \wedge w_q) \mapsto v_1 \wedge \dots \wedge v_p \wedge w_1 \wedge \dots \wedge w_q.
$$

<div class="definition">
We define 

$$
\bigwedge^{p,q} V := \bigwedge^p V^{1,0} \otimes \bigwedge^q V^{0,1}
$$

where the exterior products of $V^{1,0}$ and $V^{0,1}$ are taken as complex vector spaces. An element $\alpha \in \bigwedge^{p,q} V$ is said to be of type $(p,q)$.
</div>

---

A complex $n$-manifold is a topological Hausdorff space that is locally homeomorphic to (an open subset of) $\Bbb C^n$ and has holomorphic transition functions. Explicitly, $M$ is a complex manifold if it admits a complex atlas: a choice of open covering $\{U_i\}$ of $M$ together with homeomorphisms $\varphi_i : U_i \to \varphi(U_i) \subset \Bbb C^n$ such that for each pair of overlapping charts $U_i,U_j$, the transition map

$$
\varphi_{ij} := \varphi^{-1}_j \circ \varphi_i : \varphi_i(U_i \cap U_j) \to \varphi_i(U_i \cap U_j) 
$$

and its inverse are holomorphic. A <b>complex structure</b> on $M$ is the choice of such a complex atlas, up to holomorphic equivalence of charts, defined by a similar condition to the above.

<div class="example">
The complex space $\Bbb C^n$ is a holomorphic manifold. More interesting examples are gotten with quotienting by a lattice $\Lambda \subset \Bbb C^n$. Since $\Lambda$ acts on $\Bbb C^n$ by translation and this action is properly discontinuous and holomorphic the quotient $\Bbb C^n/\Lambda$ inhertis the holomorphic structure from the standard atlas on $\Bbb C^n$.
</div>

<div class="example">
One of the most important example of compact $n$-manifolds is the complex projective space $\mathbb{P}^n$. Intuitively a point in $\mathbb{P}^n$ is a line through the origin in $\Bbb C^{n+1}$. More precisely the group $\Bbb C^\times$ acts on $\Bbb C^{n+1} \setminus \{0\}$ by scalar multiplication. If the orbit space is given the quotient topology, then the holomorphic structure of $\Bbb C^{n+1}$ descends. The equivalence class of a point $z = (z_0,\dots, z_n) \in \Bbb C^{n+1} \setminus \{0\}$ is denoted $[z] = [z_0 : \dots : z_n]$ and the coordinates are called <i>homogeneous coordinates</i>. We get an atlas by exhibiting the following charts: Let $U_j = \{[z] \in \mathbb{P}^n \mid z_j \ne 0\}$ and defining $\varphi_j : U_j \to \Bbb C^n$ by 
$$
    [z_0 : \dots : z_n] \mapsto \left(\frac{z_0}{z_j}, \dots, \frac{z_{j-1}}{z_j}, \frac{z_{j+1}}{z_j},\dots, \frac{z_n}{z_j}\right).
$$
The inverse $\varphi_j^{-1} : \Bbb C^n \to U_j$ is given by 
$$
    (z_0,\dots ,z_{j-1}, z_{j+1}, \dots ,z_n) \mapsto [z_0 : \dots : 1 : \dots : z_n].
$$    
</div>

<div class="example">
A closed complex submanifold of $\Bbb P^n$ is called a <i>projective manifold</i>. The <i>Kodaira Embedding Theorem</i> gives a necessary and sufficient condition for a compact complex manifold to be projective. A <i>projective variety</i> is the image of in $\Bbb P^n$ of the common zero set of a finite set of homogeneous polynomials on $\Bbb C^{n+1}$. A marvelous fact is that the converse is also true by something called <i>Chow's theorem</i>. That is every compact complex submanifold of $\Bbb P^n$ is the zero set of a finite set of homogeneous polynomials.
</div>

Let $M$ be a complex manifold and $p \in M$. An endomorphism $J_p : T_pM \to T_pM$ that squares to $-1$ can be defined on the real tangent space at $p$ as follows: Let $(U, \varphi : U \to \Bbb R^{2n})$ be a holomorphic chart at $p$. Now 

$$
(d\varphi)_p : T_pM \to T_p\Bbb R^{2n} \cong \Bbb R^{2n}
$$

is an isomorphism and $J_p$ is defined by $(d\varphi)^{-1}\_p \circ J_{\Bbb R^{2n}} \circ (d\varphi)_p$ and $J_p$ doesn't depend on the choice of the chart.

Notice that $J : TM \to TM$ is actually a bundle isomorphism and can be considered as a tensor field of type $(1,1)$: in a coordinate chart $(U, x_1,\dots,x_n)$ we can write $J\left( \frac{\partial}{\partial_j} \right) = \sum J_j^k\frac{\partial}{\partial x_k}$ and so 

$$
J = \sum J^k_j dx_j \otimes \frac{\partial}{\partial x_k}.
$$

This is just due to the isomorphism given by $\operatorname{Hom}(V, W) \cong V^* \otimes W$ for vector spaces $V$ and $W$ with the isomorphism given by 

$$
V^*\otimes W \ni f\otimes w \mapsto (v \mapsto f(v)w) \in {\rm Hom}(V,W)
$$

and the inverse by 

$$
{\rm Hom}(V,W) \ni T \mapsto \sum e^i\otimes T(e_i) \in V^*\otimes W.
$$

It is also worth noting that this tensor completely determines the complex structure on $M$ since the chart $(U, \varphi : U \to \Bbb R^{2n})$ is holomorphic if and only if $(d\varphi)\_p \circ J_p = J_{\Bbb R^{2n}} \circ (d\varphi)_p$.

<div class="definition">
A smooth map between complex manifolds $f : M \to N$ is holomorphic if $df \circ J_M = J_N \circ df$.
</div>

The map $J$ will turn out to be very important and we will get back to it later.

Notice that this definition is equivalent to $f$ being holomorphic when expressed locally with holomorphic charts on the manifolds. Here is a neat exercise: show that if $M'$ is a submanifold of $M$ and $i : M' \hookrightarrow M$ the inclusion, then $M'$ has at most one complex structure such that the injection is holomorphic.

---

Up to this point we've treated manifolds with complex structures. In the following we will consider manifolds that posses a bundle map $J : TM \to TM$ independent of any complex structure.

<div class="definition">
Let $M$ be a smooth manifold. An <i>almost complex structure</i> on $M$ is a bundle map $J : TM \to TM$ such that $J^2 = -\operatorname{id}$. 
</div>

The pair $(M, J)$ consisting of a smooth manifold and an almost complex structure is called an <i>almost complex manifold</i>.

<div class="lemma">
A real real finite dimensional vector space $V$ with an endomorphism $J : V \to V$ for which $J^2 = -\operatorname{id}$ is even dimensional.
</div>

<div class="proof">
Let $\dim V = n$. Notice that $\det(J)^2 = \det(J^2) = (-1)^n\det(\operatorname{id}) = (-1)^n$. Since $V$ is real $\det(J)$ is real and so $n$ must be even.
</div>

The previous lemma shows that any manifold which admits an almost complex structure is neccesarily even dimensional.

<div class="lemma">
Let $(M,J)$ be an almost complex manifold. Then $J$ is the almost complex structure associated to an complex structure on $M$ if and only if for every $p \in M$ there exists a smooth chart $(U, \varphi : U \to \Bbb R^{2n})$ such that $d\varphi \circ J = J_{\Bbb R^{2n}} \circ d\varphi$.
</div>

<div class="proof">
Suppose that $J$ is an almost complex structure associated to a complex structure on $M$. Then on a holomorphic chart $(U, \varphi)$ at $p \in M$, $J$ is given by $J = (d\varphi)^{-1}_p \circ J_{\Bbb R^{2n}} \circ (d\varphi)_p$. It follows that \[d\varphi \circ J = J_{\Bbb R^{2n}} \circ d\varphi.\]
If for smooth charts $\varphi : U \to \Bbb R^{2n}$ and $\psi : V \to \Bbb R^{2n}$ both satisfy $d\varphi \circ J = J_{\Bbb R^{2n}} \circ d\varphi$ and $d\psi \circ J = J_{\Bbb R^{2n}} \circ d\psi$ on $U$ and $V$ respectively, then the transition map $\varphi \circ \psi^{-1}$ on $\psi(U \cap V)$ satisfies 

$$
\begin{align*}
    d(\varphi \circ \psi^{-1}) \circ J_{\Bbb R^{2n}} &= d\varphi \circ d\psi^{-1} \circ J_{\Bbb R^{2n}} \\
    &= d\varphi \circ J \circ d\psi^{-1} \\
    &= J_{\Bbb R^{2n}} \circ d\varphi \circ d\psi^{-1} \\
    &= J_{\Bbb R^{2n}} \circ d(\varphi \circ \psi^{-1})
\end{align*}
$$

and so $\varphi \circ \psi^{-1}$ is holomorphic on $\psi(U\cap V)$ and thus determines a complex structure on $M$.
</div>
---

[^1]: We will later see that there is a very good motivation on defining these.