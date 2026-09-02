---
layout: post
title: "Ample Line Bundles, Positivity and Polarizations"
categories: [Complex Geometry]
mathjax: true
published: false
excerpt_separator: <!--more-->
---

Line bundles are of fundamental importance in the study of holomorphic manifolds for two principal reasons. First, their sections play the role of
global holomorphic functions, which are lacking on compact manifolds. Second, line bundles have a cohomological interpretation, which helps make their  classification amenable to homological methods. The latter is of course mostly of importance because of the former; results about vanishing of cohomology can be used to extract information about global sections of line bundles. Interesting geometric theorems may in turn be expressible in terms of sections of line bundles.

In both algebraic and complex geometry, line bundles have a kind of “positivity” that’s key to understanding the shapes and structures of varieties. Some bundles are “positive,” others “negative,” and some a mix of both. Ample line bundles are particularly special: they give us enough global sections to map varieties into projective space in a way that reveals a lot about their geometry. These bundles play a big role in both embedding varieties and in stability conditions, where their positivity helps control the geometry and complex structure of the space.

<!--more-->

In this post, we’ll dive into what it means for a line bundle to be ample, very ample, or base point-free, and why these properties matter in complex and algebraic geometry. We’ll also look at divisors and explore criteria, like Nakai–Moishezon and Kleiman’s, for ampleness. 

---

Suppose that $X$ is a compact complex manifold and $L \to X$ a holomorphic line bundle over $X$. The theme that our discussion today will follow centers around the fact that line bundles provide us means to embed $X$ into projective spaces. 

The first thing to note is that the space of global holomorphic sections $H^0(X,L)$ is finite-dimensional. To see this, we'll utilize a bit of Hodge theory.

<div class="proposition">
Let $X$ be a compact complex manifold and $E$ a holomorphic vector bundle over $X$. Then the sheaf cohomology groups $H^q(X,\Omega^p(E))$ are all finite-dimensional, and are zero unless $0 \le p,q\le \dim X$.
</div>

<div class="proof">
Recall that the Dolbeault isomorphism states that
$$
H^q(X,\Omega^p(E)) \cong H^{p,q}(X, E).
$$
Equip $X$ now with a Hermitian metric, then the Hodge–Dolbeault Theorem yields
$$
H^{p,q}(X,E) \cong \mathcal{H}_{\bar{\partial}}^{p,q}(X, E),
$$
which is finite-dimensional. Moreover, since there are no non-trivial $(p,q)$-forms unless $0 \le p,q \le \dim X$, those are the only values of $p$ and $q$ for which the groups $H^{q}(X, \Omega^p(E))$ can be non-trivial.
</div>

Note that the above proposition is quite restrictive. If you consider smooth functions on a smooth manifold you get an infinite dimensional space. Holomorphic functions on a compact complex manifold yield a $1$-dimensional space (they are all constants). In some sense holomorphic sections have just enough rigidty to not be too complicated nor too simple.

Now, a point $x \in X$ is called a <b>base point</b> for $L$ if every global section of $L$ vanishes at $x$. We denote the set of base points $B(L)$ and call it the <b>base locus</b> of $L$. If $L$ has at least one non-trivial holomorphic section, by picking a basis $(s_0,\dots,s_m)$ for $H^0(X,L)$, we can define a map

$$
X \setminus B(L) \to \Bbb P^m
$$

in the following way. Given $y \in X \setminus B(L)$, consider a local frame $e$ for $L$ in a neighborhood $U \ni y$ and write each section $s_i$ of the basis as

$$
s_i = f_ie,
$$

for some holomorphic function $f_i \in \mathcal{O}_X(U)$. Then for any $x \in U$ map it to 

$$
[f_0(x):\cdots:f_m(x)] \in \Bbb P^m.
$$

It's quite direct to verify that this does not depend on the choice of the frame by utilizing transition maps. Henceforth, we denote with $[s_0(x):\cdots:s_m(x)]$ the point $[f_0(x) : \cdots : f_m(x)]$ and define a holomorphic map

$$
\begin{align*}
    &F : X \setminus B(L) \to \Bbb P^m \\
    x &\mapsto [s_0(x):\dots:s_m(x)],
\end{align*}
$$

called the <b>associated map</b> for $L$. Ultimately our aim is to figure out when $F$ is an embedding. For this to happen, $F$ must be an injective immersion. Its quite clear how to discuss the injectivity of $F$, but for $F$ to be an immersion one has to prove that the differential of $F$ is injective. In other words, for every $v \in T_x X$, there exists a section $s$ of $L$ vanishing at $x$ such that $\text{"}ds(v)\text{"} \ne 0$. A priori, this $ds$ is not really a well-defined object, but it turns out that we can do the usual order of business here. Consider a framed neighborhood $U$ of $x$ with a frame $e_U$ so that $s = fe_U$ for $f : U \to \Bbb C$, and define $ds$ locally to be $df$. On overlapping domains $U \cap V$, the frames $e_U$ and $e_V$ are related by $e_V = g_{UV}e_U$ for some transition map $g_{UV}$. If $s = fe_U$ on $U$ and $s = he_V$ on $V$, then $f = hg_{UV}$ and for $v \in T_xX$

$$
df_x(v) = d(hg_{UV})_x(v) = h(x)d(g_{UV})_x(v) + g_{UV}(x)dh_x(v) = g_{UV}(x)dh_x(v),
$$

since $h(x) = 0$. Hence $ds$ does not depend on the chosen local frame. The following lemma gives the criteria for $F$ to be an injective immersion.

<div class="lemma">
Let $X$ be a compact complex manifold and $L \to X$ a holomorphic line bundle that admits at least one non-trivial global section. Let $F : X \setminus B(L) \to \Bbb P^m$ be an associated map. Then:
<ol>
    <li>
    $F$ is injective if and only if there exists a holomorphic section $s \in H^0(X,L)$ such that $s(x) = 0$ and $s(y) \ne 0$ for distinct points $x,y \in X \setminus B(L)$.
    </li>
    <li>
    Given $x \in X \setminus B(L)$ and $v \in T^{1,0}_x X$, $D^{1,0}F(x)v \ne 0$ if and only if there exists $s \in H^0(X,L)$ such that $s(x) = 0$ and $df_x(v) \ne 0$, where $f$ is the component function of $s$ with respect to some holomorphic local frame.
    </li>
</ol>
</div>

Given a holomorphic line bundle $L$ over $X$, we say that $H^0(X,L)$ <b>separates points</b> if for every pair of distinct $x$ and $y$ in $X$, there exists a global holomorphic section $s$ of $L$ such that $s(x) = 0$ and $s(y) \ne 0$. Also $H^0(X,L)$ is said to <b>separate directions</b> if for every $x \in X$ and every non-zero $v \in T^{1,0}_x X$, there exists a global holomorphic section $s$ such that $s(x) = 0$ and $df_x(v) \ne 0$, where $f$ is the component function of $\sigma$ with respect to some holomorphic local frame. 

<div class="definition">
A holomorphic line bundle $L$ over a compact complex manifold $X$ is called <b>very ample</b> if 
<ol>
    <li>
    $H^0(X,L)$ separates points.
    </li>
    <li>
    $H^0(X,L)$ separates directions.
    </li>
</ol>
</div>

<div class="theorem">
Let $X$ be a compact complex manifold and $L \to X$ a holomorphic line bundle. Each associated map for $L$ is a global embedding of $X$ into a projective space if and only if $L$ is very ample.
</div>

<div class="proof">
Suppose that $L$ is a very ample holomorphic line bundle. Let $x \in X$. Then for $y \ne x$ since $H^0(X,L)$ separates points, there exists $s \in H^0(X,L)$ such that $s(y) = 0$ and $s(x) \ne 0$. Hence for any given point we can find a section that doesn't vanish at that point which yields $B(L) = \emptyset$. Thus $L$ has no base points and hence any associated map $F$ is defined on all of $X$. The definition of very ampleness for $L$ alongside the previous lemma implies each associated map $F$ is an injective immersion into $\Bbb P^m$ for some $m$. The closed map lemma shows that $F$ is indeed an embedding. Conversely, suppose that an associated map $F : X \to \Bbb P^m$ is a global embedding. As $F$ is globally defined $L$ has no base points and since $F$ is an injective holomorphic immersion the previous lemma shows that $H^0(X,L)$ separates points and directions and hence $L$ is very ample.
</div>

<div class="definition">
A holomorphic line bundle $L$ over a compact complex manifold $X$ is called <b>ample</b> if for some positive integer $k$, the tensor power $L^{\otimes k}$ is very ample.
</div>

<div class="lemma">
Let $X$ and $Y$ be compact complex manifolds and $f : X \to Y$ an embedding. If $L$ is an ample holomorphic vector bundle over $Y$, then $f^\ast L$ is an ample vector bundle over $X$.
</div>

<div class="proof">
Let $L \to Y$ be an ample holomorphic line bundle. Then there exists an integer $k$ for which $L^{\otimes k}$ is very ample. The claim is that $f^\ast L^{\otimes k}$ is very ample. Pick distinct $x,y \in X$, since $f$ is an embedding $f(x) \ne f(y)$ and as $L^{\otimes k}$ is very ample, there exists $s \in H^0(Y,L^{\otimes k})$ such that
$$
(f^\ast s)(x) = s(f(x)) = 0 \ \text{ and } \ (f^\ast s)(y) = s(f(y)) \ne 0.
$$
Hence $H^0(X, f^\ast L^{\otimes k})$ separates points. Suppose then that $x \in X \setminus B\left(f^\ast L^{\otimes k}\right)$ and $v \in T^{1,0}_x X$. Since $L^{\otimes k}$ is very ample, $B(L^{\otimes k}) = \emptyset$ so $f(x)$ is not a base point. Set 
$$
w := df_x(v) \in T^{1,0}_{f(x)}Y.
$$ 
Then there exists $s \in H^0(X,L^{\otimes k})$ such that $s(f(x)) = 0$ and $ds_{f(x)}(w) \ne 0$. Now $(f^\ast s)(x) = s(f(x)) = 0$ and 
$$
d(f^\ast s)_x(v) = d(s \circ f)_x(v) = ds_{f(x)}(df_x(v)) = ds_{f(x)}(w) \ne 0,
$$
which shows that $H^0(X,f^\ast L^{\otimes k})$ separates directions.
</div>

<div class="proposition">
The hyperplane bundle $\mathcal{O}(1) \to \Bbb P^n$ is very ample.
</div>

<div class="proof">
Recall that $H^0(\Bbb P^n, \mathcal{O}(1))$ is isomorphic to the space homogeneous holomorphic degree $1$ polynomials, i.e. linear functions. Pick distinct $[x] = [x^0:\cdots:x^n]$ and $[y] = [y^0:\cdots:y^n]$ in $\Bbb P^n$. As the vectors $(x^0,\dots,x^n), (y^0,\dots,y^n) \in \Bbb C^{n+1}$ are linearly independent, there exists a linear map $f : \Bbb C^{n+1} \to \Bbb C$ such that
$$
f(x^0,\dots,x^n) = 0 \ \text{ and } \ f(y^0,\dots,y^n) \ne 0.
$$
This yields a global section $s_f \in H^0(\Bbb P^n, \mathcal{O}(1))$ by restricting $f$ to each $1$-dimensional subspace, i.e.
$$
s_f(\ell) = f\vert_{\ell}.
$$
Now $s_f([x]) = f\vert_{[x]}$ and this is the zero map as any $z$ lying in the line spanned by $[x]$ is of the form $\lambda x$ and so $f(z) = \lambda f(x^0,\dots,x^n) = 0$. Thus $s_f([x])$. Similar argument shows that $s_f([y]) \ne 0$, i.e. $H^0(\Bbb P^n, \mathcal{O}(1))$ separates points. Suppose then that $[x] \in \Bbb P^n \setminus B(\mathcal{O}(1))$, and $v \in T^{1,0}_{[x]}\Bbb P^n$. There is some open $U_i = \{[w] \mid w^i \ne 0\}$ containing $[x]$ and we may assume without loss of generality that $[x] \in U_0$, i.e. $[x] = [1: x^1 :\cdots:x^n]$. In terms of affine coordinates $(z^1,\dots,z^n)$ we have $v = v^j \partial/\partial z^j$ and since $v \ne 0$, it has a non-zero component $v^k$. We seek for a section $s \in H^0(\Bbb P^n, \mathcal{O}(1))$ that vanishes at $[x]$ and satisfies $ds_{[x]}(v) \ne 0$. Such a section is given by a linear function $f : \Bbb C^{n+1} \to \Bbb C$, so define $f$ by
$$
f(w^0,\dots,w^n) = w^k - x^kw^0.
$$
This yields a section $s_f$ for which $s_f([x]) = f\vert_{[x]} = 0$ since 
$$
f(\lambda(1,x^1,\dots,x^n)) = \lambda f(1,x^1,\dots,x^n) = 0
$$
for any $\lambda \in \Bbb C$. Also in $U_0$, $s_{w^0}$ given by the coordinate function $w^0 : \Bbb C^{n+1} \to \Bbb C$ yields a non-vanishing section and can be therefore used as a local frame for $\mathcal{O}(1)$ in $U_0$. Thus $s_f = gs_{w^0}$ for some $g \in \mathcal{O}_{\Bbb P^n}(U_0)$. We see that
$$
g([w]) = \frac{w^k-x^kw^0}{w^0},
$$
and in terms of affine coordinates
$$
g(z) = z^k-x^k.
$$
Moreover, $dg_{x}(v) = v^k \ne 0$, which yields that $H^0(\Bbb P^n, \mathcal{O}(1))$ separates directions.
</div>

Combining the above lemma and proposition, we have the following corollary by pulling back the ample line bundle $\mathcal{O}(1) \to \Bbb P^n$ via an embedding.

<div class="corollary">
A compact complex manifold is projective if and only if it admits an ample line bundle.
</div>

Perhaps not too surprisingly we have the following proposition.

<div class="proposition">
Let $X$ be a compact complex manifold, $L \to X$ a very ample holomorphic line bundle and $F : X \to \Bbb P^m$ its associated map. Then
$$
L \cong F^{\ast}\mathcal{O}(1),
$$
where $\mathcal{O}(1) \to \Bbb P^m$ is the hyperplane bundle.
</div>

<div class="proof">
Let $(s_0,\dots,s_m)$ be a basis for $H^0(X,L)$ such that $F$ is given by the map
$$
x \mapsto [s_0(x):\cdots:s_m(x)].
$$
Consider the open cover $\{U_i\}$ with $U_i = \{[w] \mid w^i \ne 0\}$ for $\Bbb P^m$. Then $V_i = F^{-1}(U_i)$ consists of points $x \in X$ such that $s_i(x)\ne 0$. Therefore, the sections $s_i$ form a local frame for $L$ on each $V_i$. Now $\{V_i\}$ forms an open cover for $X$ that trivializes both $L$ and $F^\ast \mathcal{O}(1)$. Let $g_{ij} : V_i \cap V_j \to \mathrm{GL}(1,\Bbb C)$ denote the transition maps for $L$. Then on $V_i \cap V_j$ we have that $s_j = g_{ij}s_i$, i.e. 
$$
g_{ij} = \frac{s_j}{s_i}
$$
since $s_i$ is non-vanishing on $V_i \cap V_j$. The transition functions for the hyperplane bundle $\mathcal{O}(1) \to \Bbb P^m$ on $U_i \cap U_j$ are given by
$$
\tau_{ij} = \frac{w^j}{w^i}.
$$
Therefore, the pullback bundle $F^\ast \mathcal{O}(1)$ has transition maps given by
$$
F^\ast \tau_{ij} = \tau_{ij} \circ F = \frac{s_j}{s_i}.
$$
We conclude that $L \cong F^\ast\mathcal{O}(1)$.
</div>

---

Ampleness is originally an algebro-geometric notion. Since I have not discussed schemes properly on the blog, I'm currently avoiding most of the algebro-geometric interpretations and gave the treatment in a differential-geometric framework. The precise differential-geometric analogue of ampleness is called
<b>positivity</b>.

<div class="definition">
Let $X$ be a complex manifold. A real $(1,1)$-form $\omega$ on $X$ is said to be positive if 
$$
\omega(v,Jv) > 0
$$
for every non-zero real tangent vector $v$.
</div>

Note that this is a special definition for forms on complex manifolds — it does not make sense to ask that a differential form be literally positive in the sense of taking only positive values, because changing the sign of one of its arguments will always convert a positive value to a negative one.

<div class="lemma">
Let $\omega$ be a real $(1,1)$-form on a complex manifold $X$. Then the following are equivalent:
<ol>
    <li>
    $\omega$ is positive.
    </li>
    <li>
    $-i\omega(v,\bar{v}) > 0$ for every non-zero $v \in T^{1,0}X$.
    </li>
    <li>
    $\omega$ restricts to a positively oriented volume form on every $1$-dimensional complex submanifold of $X$.
    </li>
</ol>
</div>

Recall that if $E$ is a Hermitian holomorphic vector bundle over a complex manifold $X$, then the curvature $F_\nabla$ of the Chern connection $\nabla$ is a purely imaginary $(1,1)$-form.

<div class="definition">
Let $X$ be a complex manifold, and let $L$ be a holomorphic line bundle over $X$. We say that $L$ is positive if there exists a Hermitian metric $h$ on $L$ such that the curvature $F_\nabla$ of the associated Chern connection satisfies 
$$
\frac{i}{2\pi}F_\nabla
$$
being a positive $(1,1)$-form on $X$.
</div>

The respective notion for a negative line bundle is obtained by requiring the form to be negative. Let's go over some consequences of the above definition.

<div class="proposition">
Let $\Sigma$ be a connected, compact Riemann surface and $L \to \Sigma$ a holomorphic line bundle. Then $L$ is positive if and only if $\deg L > 0$.
</div>

<div class="proof">
Suppose that $L$ is positive. Then there exists a Hermitian metric $h$ on $L$ such that $i/2\pi F_\nabla$ is positive. That is,
$$
c_1(L) = \left[\frac{i}{2\pi}\operatorname{tr}(F_\nabla)\right] = \left[\frac{i}{2\pi}F_\nabla\right]
$$
is represented by a positive $(1,1)$-form. Now $i/2\pi F_\nabla$ gives a positively oriented volume form on $\Sigma$ and so
$$
\deg(L) = \int_\Sigma c_1(L) = \frac{i}{2\pi}\int_\Sigma F_\nabla > 0.
$$
Conversely, suppose that $\deg(L) > 0$. Let $dV_g$ be the Riemannian volume form for some Riemannian metric on $\Sigma$. Since $\Sigma$ is of complex dimension $1$, there are no $(2,0)$-forms or $(0,2)$-forms. Hence $dV_g$ is a form of type $(1,1)$. Since $H^2(\Sigma, \Bbb R)$ is $1$-dimensional, it is spanned by $[dV_g]$. It follows that the Chern class $c_1(L)$ is represented by $adV_g$ for some real constant $a$. From
$$
0 < \deg(L) = \int_\Sigma adV_g = a\operatorname{Vol}(\Sigma),
$$
we conclude that $a >0$ and so $adV_g$ is a positive $(1,1)$-form representing $c_1(L)$.
</div>

Similar results carry on when $X$ is Kähler. We'll begin by first recalling the following lemma.

<div class="lemma">
Let $X$ be a compact Kähler manifold and $L \to X$ a holomorphic line bundle. If $\eta$ is any closed real $(1,1)$-form representing the first Chern class $c_1(L)$, then there exists a Hermitian metric on $L$ whose Chern connection $\nabla$ has curvature $F_\nabla$ satisfying
$$
\frac{i}{2\pi} F_\nabla = \eta.
$$
</div>

<div class="proof">
Let $h$ be a Hermitian metric on $L$, and let $F_\nabla$ be the curvature of the Chern connection $\nabla$. Now $i/2\pi F_\nabla$ and $\eta$ are both real $(1,1)$-forms representing $c_1(L)$ so
$$
\left[\frac{i}{2\pi} F_\nabla\right] = \left[\eta\right], 
$$
i.e. $\left[\frac{i}{2\pi} F_\nabla -\eta\right] = 0$ which means that they differ by an exact form. The $\partial\bar{\partial}$-lemma states that there exists a real function $f$ such that
$$
i\partial\bar{\partial}\left(\frac{1}{2\pi}f\right) = \frac{i}{2\pi}F_\nabla - \eta.
$$
Consider now the conformal change to $h$ given by $\widetilde{h} = e^fh$, and let $F_{\widetilde{\nabla}}$ be the curvature form of the resulting Chern connection. In terms of a local holomorphic frame $e$ we have 
$$
F_\nabla = \bar{\partial}\partial \log |s|^2_h,
$$
and
$$
\begin{align*}
F_{\widetilde{\nabla}} &= \bar{\partial}\partial \log|s|^2_{\widetilde{h}} \\
&= \bar{\partial}\partial \log(e^f|s|^2_h) \\
&= \bar{\partial}\partial \log(e^f) + \bar{\partial}\partial \log|s|^2_h \\
&= \bar{\partial}\partial f + F_\nabla \\
&= \frac{2\pi}{i}\eta.
\end{align*}
$$
We conclude that $\widetilde{h}$ results in the metric we were seeking.
</div>

<div class="proposition">
Let $X$ be a compact Kähler manifold and $L$ a holomorphic line bundle over $X$. Then $L$ is positive if and only if its first Chern class is positive. 
</div>

<div class="proof">
The first implication follows directly from the definition. Conversely, suppose that $c_1(L)$ is positive. Then there exists a positive closed real $(1,1)$-form $\omega$ representing $c_1(L)$. The lemma above gives the existence for a Hermitian metric on $L$ for which the curvature of the Chern connection satisfies
$$
\frac{i}{2\pi} F_\nabla = \omega.
$$
Since $\omega$ is positive, $i/2\pi F_\nabla$ is positive and we conclude that $L$ is positive.
</div>

<div class="theorem">
Let $X$ be a compact Kähler manifold and $L \to X$ a negative holomorphic line bundle. Then $H^0(X,L) = 0$.
</div>

<div class="proof">
Let $s \in H^0(X,L)$ be non-vanishing. Recall Bochner's formula stating that for a holomorphic section $s$ of $L$, we have
$$
\Delta h(s,s) = -i\Lambda h(F_\nabla s, s) + i\Lambda|\nabla s|^2,
$$
where $\Lambda$ is the contraction with respect to the Kähler form $\omega$. Since $i/2\pi F_\nabla$ is negative, 
$$
-i\Lambda h(F_\nabla s, s) \ge 0
$$
and hence 
$$
\Delta h(s,s) \ge 0.
$$
Bochner's lemma implies that $\Delta h(s,s) = 0$ and so $h(s,s)$ is constant. As $-i\Lambda h(F_\nabla s, s)$ and $ i\Lambda|\nabla s|^2$ are both non-negative, each of them vanish and we conclude that $\nabla s = 0$, as well as $h(s,s) = 0$, i.e. $s = 0$.
</div>

Some of the most interesting properties related to positive line bundles is that they give us some control over the vanishing of certain higher cohomology groups. In essence, the positivity provides enough "room" for sections to exist without obstructions, leading to the vanishing of higher cohomology.

Recall the following Kähler identities for bundle-valued forms:

<ol>
    <li>
    $[\left(\nabla^{0,1}\right)^\ast, L] = i\nabla^{1,0}$.
    </li>
    <li>
    $[\left(\nabla^{1,0}\right)^\ast, L] = -i\nabla^{0,1}$.
    </li>
    <li>
    $[\Lambda,\nabla^{0,1}] = -i(\nabla^{1,0})^\ast$.
    </li>
    <li>
    $[\Lambda, \nabla^{1,0}] = i(\nabla^{0,1})^\ast$.
    </li>
</ol>

Here again, $L$ denotes the Lefschetz operator and $\Lambda$ its adjoint. We also have the bundle-valued Laplace operators given by

$$
\Delta^{1,0}\alpha = \nabla^{1,0}(\nabla^{1,0})^\ast\alpha + (\nabla^{1,0})^\ast\nabla^{1,0}\alpha
$$

and

$$
\Delta^{0,1}\alpha = \nabla^{0,1}(\nabla^{0,1})^\ast\alpha + (\nabla^{0,1})^\ast\nabla^{0,1}\alpha,
$$

for $\alpha \in \Omega^{p,q}(X,E)$. Here $E$ is any Hermitian vector bundle over $X$. Using these, we obtain the so-calld Akizuki-Nakano identity.

<div class="theorem">
Let $X$ be a Kähler manifold and $E$ a Hermitian holomorphic vector bundle. Let $\Delta^{1,0}$ and $\Delta^{0,1}$ be the two Laplace operators with respect to the Chern connection on $E$, and let $\Xi : \Omega^{p,q}(X,E) \to \Omega^{p,q}(X,E)$ be the operator $\Xi(\alpha) = i\Theta \wedge \alpha$, where $\Theta$ is the curvature of the Chern connection. Then
    \[
     [\Xi, \Lambda] = \Delta^{0,1} - \Delta^{1,0}.
    \]
</div>

We'll omit the proof of this, but it basically follows directly from the Kähler identities for bundle-valued forms and the fact that for a Hermitian holomorphic vector bundle $E$ over a complex manifold $X$, the curvature $F_\nabla$ of the Chern connection satisfies

$$
F_\nabla \wedge \alpha = \nabla^{1,0}\nabla^{0,1}\alpha + \nabla^{0,1}\nabla^{1,0}\alpha,
$$

where $\alpha \in \Omega^{p,q}(X,E)$.

<div class="theorem" text="(Akizuki–Nakano Vanishing Theorem)">
Let $X$ be a compact $n$-dimensional complex manifold and $L$ a positive line bundle. Then

\[
H^{p,q}(X,L) = 0
\]

for $p+q > n$.
</div>

<div class="proof">
    Note that since $L$ is positive, there exists a Kähler metric on $X$ and a Hermitian metric on $L$ such that $\frac{i}{2\pi}\Theta$ equals the Kähler form, where $\Theta$ is the curvature of the Chern connection on $L$. By the Hodge-Dolbeault theorem for bundle-valued forms, every cohomology class in $H^{p,q}(X,L)$ has a $\bar{\partial}_L$-harmonic representative. Let $\alpha \in \mathcal{H}^{p,q}(X,L)$ be such a form. Since the Chern connection is compatible with the metric $\nabla^{0,1} = \bar{\partial}_L$, and 
    \[
    \Delta_{\bar{\partial}_L} = \bar{\partial}_L\bar{\partial}^\ast_L + \bar{\partial}^\ast_L\bar{\partial}_L = \Delta^{0,1}.
    \]
    The Akizuki-Nakano identity yields
    \begin{align*}
        0 &= \Delta_{\bar{\partial}_L}\alpha \\
        &= \Delta^{0,1}\alpha \\
        &= \nabla^{1,0}\alpha + [\Xi, \Lambda]\alpha.
    \end{align*}
    On the other hand, 
    \[
    \Xi\alpha = i\Theta \wedge \alpha = 2\pi L\alpha.
    \]
    Thus
    \begin{align*}
        -\Delta^{1,0}\alpha &= [\Xi, \Lambda]\alpha \\
        &= \Xi\Lambda\alpha-\Lambda\Xi\alpha \\
        &= 2\pi L\Lambda\alpha - \Lambda 2\pi L\alpha \\
        &= 2\pi[L,\Lambda]\alpha \\
        &= 2\pi(p+q-n)\alpha,
    \end{align*}
    where in the last equality we use the identity $[L,\Lambda]\alpha = (p+q-n)\alpha$ which holds also for bundle-valued forms by acting only on the differential form part. Finally, this gives
    \begin{align*}
        2\pi(p+q-n)\|\alpha\|^2 &= -(\Delta^{1,0}\alpha,\alpha) \\
        &= -(\nabla^{1,0}(\nabla^{1,0})^\ast \alpha,\alpha) - ((\nabla^{1,0})^\ast \nabla^{1,0}\alpha,\alpha) \\
        &= -\|(\nabla^{1,0})^\ast\alpha\|^2 - \|\nabla^{1,0}\alpha\|^2 \\
        &\le 0.
    \end{align*}
    When $p+q-n>0$, this yields $\alpha = 0$.
</div>

The famous Kodaira vanishing theorem is an immediate corollary of the theorem above.

---

To wrap this up, 