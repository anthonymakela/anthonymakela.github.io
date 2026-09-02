---
layout: post
title: "Serre–Swan theorem"
categories: [Differential Geometry, Abstract Algebra]
published: false
mathjax: true
keywords: "Serre-Swan, Serre-Swan Theorem"
excerpt_separator: <!--more-->
---

You may have heard about the famous Serre–Swan theorem relating geometry to algebra via vector bundles and projective modules. The idea here is that the theorem identifies modules over an algebra of functions on some space with the modules of sections of vector bundles over that space and thus yields an identification between projective modules and vector bundles. Said differently, the theorem states that the functor $\Gamma : \textbf{Vect}\_M \to \textbf{Mod}\_{C^\infty(M)}$ from the category of vector bundles over $M$ to the category of finitely generated projective modules over $C^\infty(M)$ is an equivalence. We'll be digesting this today.

<!--more-->

---

As usual we have the definition of a vector bundle.

<div class="definition">
A fiber bundle $\pi : E \to M$ with fiber $V$ is called a real <i>vector bundle</i> if
<ol>
    <li>
    $V$ is an $\Bbb R$-vector space.
    </li>
    <li>
    For any $x \in M$, the fiber $\pi^{-1}(x)$ is a vector space.
    </li>
    <li>
    For any $x \in M$, there exists a neighborhood $U \subset M$ of $x$ and a trivializing diffeomorphism $\varphi : \pi^{-1}(U) \to U \times V$ such that the restriction maps $\varphi_y : \pi^{-1}(y) \to V, y \in U$ on fibers are linear.
    </li>
</ol> 
</div>

As usual, the rnak of a vector bundle is the dimension of its fiber. An open set satisfying the third condition in the above definition is called an <i>trivializing open subset</i>. We also have the notion of adapted coordinates for vector bundles. Let $U$ be a trivializing open set, 

$$
\varphi: \pi^{-1}(U) \to U \times V
$$

the corresponding trivialization, and $v \in V$. The map

$$
s^\varphi_v : U \to \pi^{-1}(U), \quad U \ni x \mapsto \varphi^{-1}(x,v) \in \pi^{-1}(U),
$$

yields then a section of $E\vert_U$. Now, let $b_1,\dots,b_m$ be a basis for $V$ and set $e_j := s^\varphi_{b_j}$ for $1 \le j \le m$. Now for every $x \in U$, the vectors 

$$
e_1(x),\dots,e_m(x)
$$

form a basis[^1] for $\pi^{-1}(z) \cong V$. We'll later see that the space $\Gamma(E)$ of sections of a vector bundle $E$ over $M$ has a natural $C^\infty(M)$-module structure induced by the linear structure on each fiber $\pi^{-1}(x)$. This makes it possible for us to state that given the trivializing open set $U$, the module of local sections $\Gamma(U,E)$ is free and the $e_j$'s form its free basis.

If $y \in U$ and $(x_1,\dots,x_n)$ are the local coordinates on $U$, then a point $z \in \pi^{-1}(y) \subset \pi^{-1}(U)$ is defined by $(x_1,\dots,x_n,u^1,\dots,u^m)$, where $(x_1,\dots,x_n)$ are the coordinates for $y$ and $(u^1,\dots,u^m)$ the coordinates for the point $z$ in terms of the basis $e_1,\dots,e_m$. These functions $(x_1,\dots,x_n,u^1,\dots,u^m)$ form the so-called adapted coordinate system on $\pi^{-1}(U)$ which give rise to adapted charts and atlases as well.

Recall that a morphism $f : E \to F$ of vector bundles over $M$ is a bundle map such that the following diagram commutes:

$$
\xymatrix{
E \ar@{->}[rr]^{f} \ar@{->}[rd]_{\pi_E} &  & F \ar@{->}[ld]^{\pi_F} \\
 & M. & 
}
$$

Since locally $E$ and $F$ are trivial its a worthy remark to note that a morphism of trivial bundles over $M$ is the same thing as an operator-valued function on the manifold $M$.

<div class="lemma">
Let $\pi_1 : M \times V \to M$ and $\pi_2 : M \times W \to M$ be trivial vector bundles over $M$. Then for every fiberwise linear map $f : M \times V \to M \times W$, one can assign a family of linear operators 
$$
\widetilde{f} : M \to \operatorname{Hom}(V,W)
$$
by setting 
$$
\widetilde{f}(x)(v) := \pi_W(f(x,v)) \in W,
$$
where $\pi_W : M \times W \to W$ is the projection. The following are equivalent:
<ol>
    <li>
    $f$ is a bundle morphism. That is, $f$ is smooth.
    </li>
    <li>
    The map $\widetilde{f}$ is smooth.
    </li>
</ol>
</div>

---

Let's next look at the module structure on the space $\Gamma(M,E)$ of smooth sections of a vector bundle $E \to M$. Note first that this space is non-empty, we always have the zero section $s_0$. Utilizing the linear structure on the fibers we can introduce pointwise addition and multiplication by a smooth function on $M$,

$$
(s_1+s_2)(x) = s_1(x) + s_2(x), \quad (fs)(x) = f(x)s(x),
$$

for sections $s,s_1,s_2 \in \Gamma(M,E)$, $f \in C^\infty(M)$ and $x \in M$. These operations turn $\Gamma(M,E)$ into a $C^\infty(M)$-module. Consider now for $x \in M$ the maximal ideal 

$$
\mu_x = \{f \in C^\infty(M) \mid f(x) = 0\}
$$

of the algbera $C^\infty(M)$.

<div class="lemma">
Let $E \to M$ be a vector bundle and $x \in M$. Then
<ol>
    <li>
    For any $y \in \pi^{-1}(x)$ there exists a section $s \in \Gamma(M,E)$ such that $s(x) = y$.
    </li>
    <li>
    If $s \in \Gamma(M,E)$ and $s(x) = 0$, then there exists functions $f_i \in \mu_x$ and sections $s_i \in \Gamma(M,E)$ such that
    $$
    s = \sum_{i=1}^m f_i s_i.
    $$
    </li>
</ol>
</div>

<div class="proof">
<ol>
    <li>
    For a trivial bundle the asseration holds always. Now we just do the usual order of business and pick a trivializing open set $U$ of $x$ and obtain a local section $\sigma \in \Gamma(U,E)$ such that $\sigma(x) = y$. Then pick a smooth function $f$ with support contained in $U$, $f(x) = 1$ and define $s := f\sigma$.
    </li>
    <li>
    If $E$ is trivial there exists a global frame $(e_1,\dots,e_m)$ and any section $s \in \Gamma(M,E)$ can be expressed as
    $$
    s = \sum_{i=1}^m f_ie_i.
    $$
    Since $s(x) = 0$ we conclude that each $f_i \in \mu_x$. When $E$ is an arbitary bundle we can again consider a trivializing open set $U$ and a local frame $(e_1,\dots,e_m)$ such that $s\vert_U = \sum_{i=1}^m f_ie_i$. Pick $g \in C^\infty(M)$ such that $\operatorname{supp}(f) \subset U$ and $g(x) = 1$ and extend $gf_i$'s and $ge_i$'s as the function that is identically zero outside $U$ to obtain smooth functions on the whole manifold $M.$ Continuing to denote these extensions as $gf_i$ and $ge_i$ note that $gs = gs\vert_U$ and
    $$
    g^2s = \sum_{i=1}^m (gf_i)(ge_i),
    $$
    and hence
    $$
    s = (1-g^2)s + \sum_{i=1}^m (gf_i)(ge_i).
    $$
    </li>
</ol>
</div>

<div class="corollary">
For any vector bundle $E \to M$, the sequence
$$
\xymatrix{
0 \ar@{->}[r] & \mu_x\Gamma(M,E) \ar@{->}[r] & \Gamma(M,E) \ar@{->}[r] & \pi^{-1}(x) \ar@{->}[r] & 0,
}
$$
where the first map is given by the inclusion, and the second map by evaluation at $x \in M$, is exact. Hence $\Gamma(M,E)/\mu_x\Gamma(M,E) \cong \pi^{-1}(x)$.
</div>

The corollary aligns with the intuitive idea that the fiber $\pi^{-1}(x)$ is captured by evaluating sections at $x$ and forgetting about those that vanish at $x$.

I'm going to take a slightly unconventional approach to smooth manifolds adhering to the philosophy that one has in algebraic geometry[^2]. In algebraic geometry, one considers varieties or schemes as geometric objects that are described by rings of functions. For instance, if you have a variety $V$ over an algebraically closed field $k$, its coordinate ring $A = k[V]$ consists of regular functions on $V$. The points of $V$ correspond to the maximal ideals of the ring $A$, or equivalently, to $k$-algebra homomorphisms from $A$ to $k$. To understand what exactly I mean by "equivalently" here, recall that Nullstellensatz gives a one-to-one correspondence between points of $V$ and the maximal ideals of $A$. That is, for each $p \in V$, we can associate a maximal ideal $\mathfrak{m}_p \subset A$. Nullstellensatz gives an explicit form for $\mathfrak{m}_p$ as $\langle x_1 - a_1,\dots,x_n-a_n\rangle$ where $p = (a_1,\dots,a_n) \in \Bbb A^n$. This maximal ideal is exactly $\\{f \in A \mid f(p) = 0\\}$ and the way we obtain a $k$-algebra homomorphism from $A$ to $k$ is that we form the quotient

$$
A/\mathfrak{m}_p \cong k,
$$

and consider the natural projection $\pi_p : A \to A/\mathfrak{m}_p \cong k$ given by $\pi_p(f) = f(p)$. Conversely given a $k$-algebra homomorphism $\varphi : A \to k$, we note that $\ker(\varphi) \subset A$ is of course an ideal in $A$, but its also maximal. Since $A$ contains a copy of $k$ the map $\varphi$ is surjective and hence $A/\ker(f) \cong k$, i.e., $\ker(f)$ is maximal.

The idea now is that sufficiently nice manifolds can be reconstructed[^3] from the $\Bbb R$-algebra $C^\infty(M)$ so what we do is begin with a commutative unital $\Bbb R$-algebra $A$ and obtain a manifold $M$ by setting $M = \|A\|$ to be the spectrum, i.e, the set of all $\Bbb R$-algebra homomorphisms from $A$ to $\Bbb R$:

$$
M \ni x : A \to \Bbb R, \quad f \mapsto x(f).
$$

As an example, consider the $\Bbb R$-algebra $A = C^\infty(\Bbb R^3)/(x^2+y^2+z^2-1)$. One has $C^\infty(S^2) \cong A$ and hence $\|A\| = S^2$.

Suppose then that $A$ is an $\Bbb R$-algebra. Then for every $h \in \|A\|$, we can assign $\mu_h = \ker(h) \subset A$. Define the fiber $P_h$ of an $A$-module $P$ over a point $h \in \|A\|$ as the quotient $P/\mu_h P$. For an element $p \in P$, the value $p_h$ at $h$ is the image of $p$ under the projection $P \to P_h$. When $A = C^\infty(M)$ and $h = h_x$ for $x \in M$, we define $P_x := P/\mu_x P$.

<div class="example">
Consider the module $P = \Gamma(M,TM)$ of vector fields over the algebra $A = C^\infty(M)$. Then for $x \in M$ the above corollary gives
$$
P_x = \Gamma(M,TM)/\mu_x\Gamma(M,TM) \cong T_xM.
$$
For a vector field $Y \in P$, the value of $Y$ at $x \in M$ is given by the vector $Y_x \in T_xM$.
</div>

Let's now prove the following crucial proposition:

<div class="proposition">
Let $E \to M$ be a vector bundle and suppose that sections $s_1,\dots,s_l \in \Gamma(M,E)$ have the property that for every $x \in X$, the vectors
$$
s_1(x),\dots,s_l(x)
$$
span the fiber $\pi^{-1}(x)$. Then these sections generate the module $\Gamma(M,E)$.
</div>

<div class="proof">
Suppose that $\operatorname{rank}(E) = k$. Set
$$
U_I = \{x \in M \mid s_{i_1}(x),\dots,s_{i_k}(z) \in \pi^{-1}(x) \text{ are linearly independent}\},
$$
where $I = (i_1,\dots,i_k), 1 \le i_1 < \dots < i_k \le l$ is a multi-index. Firstly, consider the map $\det_I : M \to \Bbb R$ given by
$$
x \mapsto \det \begin{bmatrix}
    \vert & \vert & \vert \\
    s_{i_1}(x) & \cdots & s_{i_k}(x) \\
    \vert & \vert & \vert
\end{bmatrix}.
$$
Clearly this is continuous and $U_I = \det^{-1}_{I}\left(\Bbb R \setminus \{0\}\right)$, hence $U_I$ is open. Also the sections $s_{i_1}\vert_{U_I},\dots,s_{i_k}\vert_{U_I}$ generate the $C^\infty(U_I)$-module $\Gamma(U_I, E)$. Note now that $M = \bigcup_I U_I$ and for a section $s \in \Gamma(M,E)$ we have
$$
s\vert_{U_I} = \sum_{j=1}^k g_{I,j}s_{i_j}\vert_{U_I},
$$
with $g_{I,j} \in C^\infty(U_I)$. Let $h_I \in C^\infty(M)$ be a function that is strictly positive inside $U_I$, vanishes outside of it and has the property that the functions
$$
\rho_{I,j}(x) = \begin{cases} h_Ig_{I,j}(x), & x \in U_I \\ 0, & x \notin U_I  \end{cases}
$$
are smooth on $M$. Then $h = \sum_I h_I$ is everywhere positive on $M$ and
$$
h_I s = \sum_i \rho_{I,i}s_i.
$$
Thus
$$
s = \frac{1}{h}\sum_{I}h_Is = \sum_{I,i}\frac{\rho_{I,i}}{h}s_i.
$$
</div>

---

We'll now begin geometrizing modules. Suppose that $A$ is an commutative $k$-algebra and $P$ and $A$-module. For each such module we can associate a geometric object

$$
|P| = \bigcup_{h \in |A|}P_h
$$

with a natural projection $\pi$ given by

$$
|P| \supset P_h \ni p_h \mapsto h \in |A|
$$

onto $\|A\|$. You should think of this just like you would think of the map

$$
TM \supset T_xM \ni Y_x \mapsto x \in M,
$$

in the case of the tangent bundle. When $A = C^\infty(M)$, we have $\|P\| = \bigcup_{x \in M}P_x$. Notice how this seems very similar to a bundle construction from its tangent spaces. Indeed, we will soon observe that when $A = C^\infty(M)$ and $P$ is projective and finitely generated this corresponds to a vector bundle.

When $P = \Gamma(M,TM)$, every vector field $Y \in P$ corresponds to a section $s_Y : M \to TM$ given by

$$
x \mapsto Y_x \in T_xM.
$$

This turns out to be a more general construction and can be defined in the following manner. For $p \in P$, we define a section $s_p : \|A\| \to \|P\|$ by

$$
h \mapsto p_h.
$$

One can now view the elements of an arbitary module $P$ as sections of the bundle $\|P\|$ in the same manner as one can view elements of an arbitary algebra $A$ as functions on its spectrum $\|A\|$. We'll eventually see that vector bundles are obtained from projective modules in the same manner as smooth manifolds are obtained from smooth algebras[^4]. The set of sections $s_p : \|A\| \to \|P\|$ will be denoted by $\Gamma(P)$ and we'll immediately note that this has an $A$-module structure as we have

$$
(s_{p_1}+s_{p_2}) = s_{p_1+p_2}, \quad p_1,p_2 \in P
$$

and

$$
(as_p) = s_{ap}, \quad a \in A, p \in P.
$$

For every $A$-module $P$, we can now assign the $A$-module $\Gamma(P)$ of sections of the bundle $\|P\|$. The thing we aim to show now is that when $A = C^\infty(M)$, and $P$ is a finitely generated projective $A$-module, the bundle $\|P\|$ is actually a vector bundle and $P$ and $\Gamma(P)$ are isomorphic.

<div class="proposition">
The assignment $P \mapsto \Gamma(P)$ defines a functor $\Gamma : \textbf{Mod}_A \to \textbf{Mod}_A$.
</div>

<div class="proof">
We've already seen that if $P$ is an $A$-module, then $\Gamma(P)$ has an $A$-module structure. Suppose that $f : P \to Q$ is a morphism of $A$-modules $P$ and $Q$. Then for any $s_p \in \Gamma(P)$ with $p \in P$, we can define $\Gamma(f) : \Gamma(P) \to \Gamma(Q)$ as
$$
\Gamma(f)(s_p) = s_{f(p)} : |A| \to |Q|,
$$

where $s_{f(p)}(h) = f(p)_h$, for $h \in |A|$.

To verify that \( \Gamma(f) \) is a module homomorphism, note that

$$
\begin{align*}
\Gamma(f)(s_{p_1} + s_{p_2})(h) &= \Gamma(f)((p_1 + p_2)_h)\\
&= (f(p_1 + p_2))_h\\
&= f(p_1)_h + f(p_2)_h\\
&= \Gamma(f)(s_{p_1})(h) + \Gamma(f)(s_{p_2})(h),
\end{align*}
$$

and

$$
\begin{align*}
\Gamma(f)(as_p)(h) &= \Gamma(f)((ap)_h)\\
&= (f(ap))_h\\
&= a_h (f(p))_h\\
&= a \Gamma(f)(s_p)(h).
\end{align*}
$$

Lastly, if we consider the identity map $\operatorname{id}_P : P \to P$, we have $\Gamma(\operatorname{id}_P)(s_p) = s_{\operatorname{id}_P(s_p)} = s_p$ so $\Gamma(\operatorname{id}_P) = \operatorname{id}_{\Gamma(P)}$. For two morphisms $f:P \to Q$ and $g : Q \to R$ we have

$$
\begin{align*}
\Gamma(g \circ f)(s_p)(h) &= ((g \circ f)(p))_h \\
&= (g(f(p)))_h \\
&= \Gamma(g)(\Gamma(f)(s_p))(h).
\end{align*}
$$
</div>

Suppose now that $P$ is a $C^\infty(M)$-module and $p \in P$ is such that it belongs to the intersection $\bigcap_{x \in M} \mu_x P$. Then the value[^5] of $p$ at each $x \in M$ is called <i>unobservable</i>. We call an $C^\infty(M)$-module $P$ <i>geometric</i> if all elements of $P$ are observable. That is, $P$ is geometric if

$$
\bigcap_{x\in M} \mu_xP = 0.
$$

$P$ being geometric makes the surjection $P \to \Gamma(P)$ sending $p$ to $s_p$ injective and we obtain the following proposition:

<div class="proposition">
Let $P$ be an $C^\infty(M)$-module. Then $P$ is geometric if and only if $P$ and $\Gamma(P)$ are isomorphic.
</div>

---

We'll now strive to put a topology on $\|P\|$. As you might expect, the topology we'll put on it will be that of Zariski's. Before we get into the details, let's go over how the cotangent space $T^\ast_xM$ is defined in a purely algebraic way as you might have seen in your algebraic geometry class. 

<div class="proposition">
There exists a natural isomorphism between $T^\ast_x M$ and the quotient $\mu_z/\mu^2_x$.
</div>

<div class="proof">
Consider the first order jet space
$$
J^1_xM = C^\infty(M)/\mu^2_x,
$$
and the map $\widetilde{d}_x : J^1_xM \to T^\ast_xM$ given by
$$
[f] \mapsto d_xf.
$$
Now if $f \in \mu^2_x$, then $d_xf = 0$ so the map above is well-defined. It is also $\Bbb R$-linear and surjective. Decomposing 
$$
C^\infty(M) = \Bbb R \oplus \mu_x
$$
with $f = f(x) + (f - f(x))$ gives 
$$
J^1_x M = R\oplus \mu_z/\mu^2_z
$$
and $d_z$ annihilates the first summand. On the other hand, Hadamard's lemma shows that $f \in \mu_x$ and $d_xf = 0$ imply $f \in \mu^2_x$. It follows that the restriction of $\widetilde{d}_x$ to $\mu_z/\mu^2_z$ is an isomorphism.
</div>

Now a very interesting fact is that the algebra whose spectrum is the cotangent space $T^\ast M$ turns out to be $\mathcal{S}_\ast(C^\infty(M))$, the algebra of symbols. I might go over this fact in another post, but this time we'll just take it for granted and use it as a heuristic to turn $\|P\|$ into a topological space. Consider the symmetric algebra $\mathcal{S}(P^\ast)$ of the module

$$
P^\ast = \operatorname{Hom}_A(P,A).
$$

By definition we have

$$
\mathcal{S}(P^\ast) = \bigoplus_{k \ge 0} \mathcal{S}_k(P^\ast),
$$

with $\mathcal{S}_k(P^\ast)$ being the $k$th symmetric power of the module $P^\ast$. Elements $f \in P^\ast = \mathcal{S}_1(P^\ast)$ can be viewed as functions on $\|P\|$ by setting

$$
f(p_h) = f(p) \pmod{\mu_h} \in A/\mu_h = k,
$$

where $h \in \|A\|$ and $p \in P$. This can be extended to $(P^\ast)^{\otimes}$ in the usual way. To understand what we are doing here, consider again $P = \Gamma(M,TM)$ and $A = C^\infty(M)$. Then 

$$
P^\ast = \operatorname{Hom}_{C^\infty(M)}(\Gamma(M,T^\ast M),C^\infty(M))
$$

and any $f \in P^\ast$ can be viewed as a function on $\|P\| = \bigcup_{x \in M} T_xM$ by setting

$$
f(Y_x) = f(Y) \pmod{\mu_x} = f(Y)(x) \in C^\infty(M)/\mu_x \cong \Bbb R,
$$

for $x \in M$ and $Y \in P$. We're literally just applying the $1$-form $f$ to a vector field to obtain a smooth function and then evaluating that at $x$.


We'll now specialize to the algebra $A = C^\infty(M)$. Let $\mathcal{F}(\|P\|)$ denote the $k$-algebra of functions on $\|P\|$ that correspond to elements of the algebra $\mathcal{S}(P^\ast)$. Using this, we'll turn $\|P\|$ into a topological space with the Zariski topology, in which the closed sets are zero sets of the functions in $\mathcal{F}(\|P\|)$.

<div class="proposition">
The maps $\pi : |P| \to |A|$ and $s_p : |A| \to |P|, p \in P$, are continuous in this topology.
</div>

---

The remaining discussion today will revolve around the functor $\Gamma$ relating the geometry of vector bundles with the algebra of modules. The main benefit of this functor is that it allows us to express the geometric properties of vector bundles and operations with them in algebraic language. For example.

<div class="proposition">
A vector bundle $E \to M$ is trivial if and only if $\Gamma(M,E)$ is free.
</div>


It is natural to suspect that section modules of vector bundles must possess certain specific properties originating from the fact that all fibers of a given bundle are equal to each other. The way this translates to the algebraic side is by <i>projectivity</i>. Recall that an $A$-module $P$ is called projective if it has the following property: For any epimorphism of $A$-modules $f : Q \to R$ and any homomorphism $g : P \to R$ there exists a homomorphism $\varphi : P \to R$ such that the following diagram commutes

$$
\xymatrix{
 & Q \ar@{->}[d]^{f} \\
P \ar@{->}[r]^{g} \ar@{-->}[ru]^{\varphi} & R.
}
$$

We need a few more technical tools before we can prove the smooth Serre-Swan theorem. We'll begin with the following illustrating the fact that we can obtain every vector bundle with a connected base by pulling back from the tautological bundle over the Grassmannian.

<div class="theorem">
Every vector bundle with a connected base can be induced from the tautological bundle over an appropriate Grassmannian.
</div>

<div class="proof">
Let $\pi : E \to M$ be a vector bundle of rank $n+k$, where $n = \dim M$.
</div>

---

[^1]: This is just the correspondence between local frames and local trivializations that we are describing here.

[^2]: I will go in detail on this in a future post.

[^3]: There are many things I'm glossing over here, but gist is that the functor $C^\infty(-) : \textbf{Man}\_\infty \to \textbf{Alg}^{\text{op}}\_\Bbb R$ is full and faithful.

[^4]: I haven't told you what a smooth algebra is. I'll elaborate on this in a future post.

[^5]: Just to make this as clear as possible. In the general case for an $A$-module $P$ and $h \in \|A\|$, the value of $p \in P$ at $h$ is defined to be the image of $p$ under the projection $P \to \mu_hP$. When $A = C^\infty(M)$ and $P = \Gamma(M,TM)$ the natural projection of $Y \in P$ at $x \in \|A\| = M$ is given by $\Gamma(M,TM) \to \Gamma(M,TM)/\mu_x \Gamma(M,TM) \cong T_xM$ sending $Y$ to $Y_x$.