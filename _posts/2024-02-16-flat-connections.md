---
layout: post
title: "Flat Connections"
categories: [Differential Geometry]
mathjax: true
published: true
keywords: "Flat Connections"
excerpt_separator: <!--more-->
---

I've been currently reading about results considering certain characteristic classes on holomorphic vector bundles on Kähler manifolds and the notion of a <i>flat connection</i> plays an important role in the theory. This is by no means a surprise, if you think about it, the condition $d^2_\nabla = 0$ gives us a cochain complex and lets us wonder about all things cohomology. It turns out that the cohomology theory we obtain from this is very useful and appears, for example in the Riemann-Hilbert correspondence.

<!--more-->

---

A fair warning — this is going to involve some quite heavy computation — so if that isn't your cup of tea, feel free to skip the computations. Let's kick things off with the notion of an <i>exterior covariant derivative</i>. Recall that if $M$ is a smooth manifold and $E \to M$ a vector bundle, a connection on $E$ is an $\Bbb R$-linear map

$$
\nabla : \Gamma(E) \to \Gamma(T^\ast M \otimes E),
$$

satisfying $\nabla(fs) = df\otimes s + f \nabla s$. In the complex setting, we require $\nabla$ to be $\Bbb C$-linear.



Recall now that at the end of the post <a href="https://anthonymakela.com/differential%20geometry/2023/09/07/tensor-characterization-lemma.html" style="color:#680530; text-decoration: underline;">Tensor Characterization Lemma</a> we introduced forms with values in a vector space — or more generally in a vector bundle. Introducing the notation[^1]

$$
\Omega^k(E) = \Omega^k(M,E) = \Gamma\left(\Lambda^k T^\ast M \otimes E\right)
$$

we can rephrase the definition of a connection as

$$
\nabla : \Omega^0(E) \to \Omega^1(E).
$$

This raises a question on whether we can extend $\nabla$ to a map

$$
d_\nabla : \Omega^k(E) \to \Omega^{k+1}(E)
$$

which satisfies a suitable version of the Leibniz rule. The coordinate-free formula for the exterior derivative $d : \Omega^k(M) \to \Omega^{k+1}(M)$ is given by 

$$
\begin{align*}
d\omega(X_0,\dots, X_k) &= \sum_{i=0}^k(-1)^iX_i(\omega(X_0,\dots,\widehat{X}_i,\dots, X_k)) \\
&+ \sum_{0\le i \le j \le k} (-1)^{i+j}\omega\left([X_i,X_j],\dots, \widehat{X}_i,\dots,\widehat{X}_j,\dots, X_k\right)
\end{align*}
$$

Using this and the connection $\nabla$, we define

$$
\begin{align*}
d_\nabla\omega(X_0,\dots, X_k) &= \sum_{i=0}^k(-1)^i\nabla_{X_i}(\omega(X_0,\dots,\widehat{X}_i,\dots, X_k)) \\
&+ \sum_{0\le i \le j \le k} (-1)^{i+j}\omega\left([X_i,X_j],\dots, \widehat{X}_i,\dots,\widehat{X}_j,\dots, X_k\right).
\end{align*}
$$

For $k = 0$ and $s \in \Omega^0(E)$ this yields 

$$
d_\nabla s(X_0)= \nabla_{X_0}s
$$

i.e. $d_\nabla = \nabla$, when $k = 0$.

Let $E$ and $F$ be vector bundles over $M$. There is an $\Omega^0(M)$-bilinear product

$$
\wedge : \Omega^k(E) \otimes \Omega^l(F) \to \Omega^{k+l}(E \otimes F)
$$

given by $(\omega \otimes s) \\wedge (\alpha \otimes t) = \omega \wedge \alpha \otimes (s \otimes t)$, where $\omega \in \Omega^k(M), \alpha \in \Omega^l(M), s \in \Omega^0(E)$ and $t \in \Omega^0(F)$. For $k = 0$ the product is just the $\Omega^0(M)$-module. Note also that $\omega \wedge s = \omega \otimes s$ for $\omega \in \Omega^k(M)$ and $s \in \Omega^0(E)$.

<div class="proposition">
Let $\omega \in \Omega^k(M)$, $s \in \Omega^0(E)$ and consider $\omega \otimes s \in \Omega^k(E)$. Then

$$
d_\nabla(\omega \otimes s) = d\omega \otimes s + (-1)^k\omega \wedge \nabla s.
$$
</div>

<div class="proof">
Let $X_0,\dots, X_k \in \Gamma(TM)$. We have that

$$
\begin{align*}
d_\nabla(\omega \otimes s)(X_0,\dots, X_k) &= \sum_{i=0}^k(-1)^i\nabla_{X_i}((\omega \otimes s)(X_0,\dots,\widehat{X}_i,\dots, X_k)) \\
&+ \sum_{0\le i \le j \le k} (-1)^{i+j}(\omega \otimes s)\left([X_i,X_j],\dots, \widehat{X}_i,\dots,\widehat{X}_j,\dots, X_k\right) \\
&= \sum_{i=0}^k(-1)^i\nabla_{X_i}(\omega(X_0,\dots,\widehat{X}_i,\dots, X_k)s) \\
&+ \sum_{0\le i \le j \le k} (-1)^{i+j}\omega\left([X_i,X_j],\dots, \widehat{X}_i,\dots,\widehat{X}_j,\dots, X_k\right)s \\
&= \sum_{i=0}^k(-1)^iX_i(\omega(X_0,\dots,\widehat{X}_i,\dots, X_k))s \\
&+ \sum_{i=0}^k(-1)^i\omega(X_0,\dots,\widehat{X}_i,\dots, X_k)\nabla_{X_i}s \\
&+ \sum_{0\le i \le j \le k} (-1)^{i+j}\omega\left([X_i,X_j],\dots, \widehat{X}_i,\dots,\widehat{X}_j,\dots, X_k\right)s \\
&= d\omega(X_0,\dots,X_k)s + (-1)^k(\omega \wedge \nabla s)(X_0,\dots,X_k)
\end{align*}
$$

which yields $d_\nabla(\omega \otimes s) = d\omega \otimes s + (-1)^k\omega \wedge \nabla s$.
</div>
 

Alternatively, we could have defined $d_\nabla$ by setting $d_\nabla(\omega \otimes s) = d\omega \wedge s + (-1)^k\omega \wedge \nabla s$ for $\omega \in \Omega^k(M)$ and $s \in \Omega^0(E)$. Showing that this satisfies

<ol>
    <li>
    $d_\nabla = \nabla$, when $k = 0$,
    </li>
    <li>
    $d_\nabla(\omega \wedge s) = d\omega \wedge s + (-1)^k\omega \wedge d_\nabla s$, when $\omega \in \Omega^k(M)$ and $s \in \Omega^l(E)$,
    </li>
</ol>

determines $d_\nabla$ completely. The second condition follows as for $\omega \in \Omega^k(M)$ and $s = \alpha \otimes t \in \Omega^l(E)$ we have

$$
\begin{align*}
d_\nabla(\omega \wedge s) &= d_\nabla(\omega \wedge (\alpha \otimes t)) \\
&= d_\nabla((\omega \wedge \alpha) \otimes t) \\
&= d(\omega \wedge \alpha) \otimes t + (-1)^{k+l}(\omega \wedge \alpha) \wedge \nabla t \\
&= (d\omega \wedge \alpha) \otimes t + (-1)^k\omega \wedge d\alpha \otimes t + (-1)^{k+l}(\omega \wedge \alpha) \wedge \nabla t \\
&= d\omega \wedge (\alpha \otimes t) + (-1)^k \omega \wedge d_\nabla(\alpha \otimes t) \\
&= d\omega \wedge s + (-1)^k \omega \wedge d_\nabla s.
\end{align*}
$$

---

Using the exterior covariant derivative we obtain the following sequence

$$
\xymatrix{
0 \ar@{->}[r] & \Omega^0(E) \ar@{->}[r]^{\nabla} & \Omega^1(E) \ar@{->}[r]^{d_\nabla} & \Omega^2(E) \ar@{->}[r] & {\dots,} 
}
$$

which, when $E = M \times \Bbb R$ is the trivial bundle, is exactly the de Rham complex[^2]. Now, in general, this sequence _does not_ yield a complex. That is $d_\nabla \circ \nabla = 0$ and $d^2\_\nabla = d_\nabla \circ d_\nabla = 0$ do not hold generally. Our aim here is to figure out what kind of conditions we need to impose in order to obtain a complex.

Recall that the curvature $R$ of a connection $\nabla$ on a vector bundle $E \to M$ is an $\operatorname{End}(E)$-valued $2$-form i.e. $R \in \\Gamma\left(\Lambda^k T^\ast M \otimes \operatorname{End}(E)\right) = \Omega^2(\operatorname{End}(E))$, given by 

$$
R(X,Y)s=\nabla _{X}\nabla _{Y}s-\nabla _{Y}\nabla _{X}s-\nabla _{[X,Y]}s,
$$

for $X,Y \in \Gamma(TM)$ and $s \in \Gamma(E)$. The following two propositions will be crucial for what we are going to define next.

<div class="proposition">
Let $R \in \Omega^2(\operatorname{End}(E))$ be the curvature of a connection $\nabla$ on a vector bundle $E \to M$. Then

$$
R = d_\nabla \circ \nabla : \Omega^0(E) \to \Omega^2(E).
$$

</div>

<div class="proof">
A calculation shows that for $s \in \Omega^0(E)$ and $X,Y \in \Gamma(TM)$

$$
\begin{align*}
d_\nabla(\nabla s)(X,Y) &= \nabla_X(\nabla s(Y)) - \nabla_Y(\nabla s(X)) - (\nabla s)([X,Y]) \\
&= \nabla_X\nabla_Y s - \nabla_Y\nabla_X s - \nabla_{[X,Y]}s \\
&= R(X,Y)s,
\end{align*}
$$

which concludes the proof.
</div>

Before I state the next proposition, let's take a small digression on vector-valued forms and their products. In general, if you have vector spaces $V, W$ and $Z$, and a bilinear map $\mu : V \times W \to Z$ you can define a product of a $V$-valued covector and a $W$-valued covector on a vector space $T$ by

$$
\begin{align}
\wedge_{\mu}:\operatorname{Hom}\left(\Lambda^k T,V\right)\times \operatorname{Hom}\left(\Lambda^l T,W\right) 
&\to \operatorname{Hom}\left(\Lambda^{k+l} T, Z\right) \\
\alpha\wedge_\mu \beta(t_1,\dots,t_{k+l})&\mapsto \sum_{\sigma}\operatorname{sgn}(\sigma)\mu\left(\alpha(t_{\sigma(1)},\dots, t_{\sigma(k)}), \beta(t_{\sigma(k+1)}, \dots, t_{\sigma(k+1)})\right)
\end{align}
$$

where $\sigma$ runs through all $(k,l)$-shuffles. When applied pointwise on a manifold with $T_pM$, the product above gives rise to a bilinear map

$$
\Omega^k(M,V) \times \Omega^k(M,W) \to \Omega^{k+l}(M,Z).
$$

The same story holds for general vector bundles. Consider for example a bundle $E$ over $M$ and the End-bundle $\operatorname{End}(E)$. We have an obvious bilinear pairing $\operatorname{End}(E_p) \times E_p \to E_p$, given by $(\varphi, e) \mapsto \varphi(e)$ which gives a map $\operatorname{End}(E) \times E \to E$ defined pointwise. This gives us a way to consider products of $E$ and $\operatorname{End}(E)$-valued forms. That is a bilinear map

$$
\Omega^l(\operatorname{End}(E)) \times \Omega^k(E)  \to \Omega^{k+l}(E),
$$

with

$$
\left(\sum_i \omega_i \otimes F_i,  \sum_j \alpha_j \otimes s_j \right) \mapsto \sum_{ij} \omega_i \wedge \alpha_j \otimes  F_i(s_j).
$$

<div class="proposition">
Let $\nabla$ be a connection in a vector bundle $E \to M$, and let $R$ be the curvature of $\nabla$. Then for all $\omega \in \Omega^k(E)$ 

$$
d_\nabla(d_\nabla(\omega)) = R \wedge \omega.
$$
</div>

<div class="proof">
It suffices to show this for a pure tensor $\omega = \alpha \otimes s$ with $\alpha \in \Omega^k(M)$ and $s \in \Omega^0(E)$. Again, we proceed by calculation and using the Leibniz rule

$$
\begin{align}
    d_\nabla(d_\nabla \omega)  &= d_\nabla(d_\nabla(\alpha \otimes s)) \\ 
    &= d_\nabla(d\alpha \otimes s + (-1)^k \alpha \wedge \nabla s) \\
    &= d_\nabla(d\alpha \otimes s) + (-1)^{k} d_\nabla (\alpha \wedge \nabla s) \\
    &= d^2 \alpha \otimes s + (-1)^{k+1} d\alpha \wedge \nabla s + (-1)^k (d\alpha\wedge \nabla s + \alpha \wedge d_\nabla \circ \nabla s) \\
    &= \alpha \wedge R s \\
    &= R \wedge (\alpha \otimes s) \\
    &= R \wedge \omega.
\end{align}
$$

Here the pairing $R \wedge \omega$ is given by the $\Omega^0(M)$-bilinear product 

$$
\wedge : \Omega^2(\operatorname{End}(E)) \times \Omega^k(E) \to \Omega^{k+2}(E)
$$ 

with $(G, \alpha \otimes s) \mapsto G \wedge (\alpha \otimes s) = \alpha \wedge G(s)$.
</div>

You might now guess what I'm going to say next. Indeed when $R = 0$ we have that $d_\nabla \circ d_\nabla = 0$ which makes the sequence 

$$
\xymatrix{
0 \ar@{->}[r] & \Omega^0(E) \ar@{->}[r]^{\nabla} & \Omega^1(E) \ar@{->}[r]^{d_\nabla} & \Omega^2(E) \ar@{->}[r] & {\dots,} 
}
$$

a complex.

<div class="definition">
Let $\nabla$ be a connection on $E \to M$ and $R \in \Omega^2(\operatorname{End}(E))$ the curvature of $\nabla$. The connection $\nabla$ is called <b>flat</b> if $R = 0$ identically.
</div>

Let's now go over a subtlety considering local trivializations of $E \to M$ and local frames. A trivializing open cover for a vector bundle $E \to M$ of rank $k$ consists of the data $\\{(U_i, \varphi_i : E\vert_{U_i} \to U_i \times \Bbb R^k) \\}$ where $\\{U_i\\}$ is an open cover for $M$ and $\varphi_i$'s are trivializations.

For $U_i \cap U_j \ne \emptyset$, the transition functions $g_{ij} : U_i \cap U_j \to \mathrm{GL}(k, \Bbb R)$ are given by

$$
\begin{align*}
\varphi _i \circ \varphi^{-1}_j : (U_i \cap U_j) \times \Bbb R^k &\to (U_i \cap U_j) \times \Bbb R^k \\
(p, v) &\mapsto (p, g_{ij}(p)v).
\end{align*}
$$

Now, note that the trivializations are in correspondence with local frames over $U \subset M$. Indeed, given a trivialization $\varphi : E\vert_{U} \to U \times \Bbb R^k$ we can define $s_i : U \to E$ via $s_i(p) := \varphi^{-1}(p, e_i)$, with $e_1,\dots, e_k$ being the standard basis for $\Bbb R^k$. The $k$-tuple $s = (s_1,\dots, s_k)$ yields a basis for $E_p$ at $p \in U$, i.e. its a local frame. Conversely, given a local frame $s = (s_1,\dots, s_k)$, for any $p \in U$ and $v_p \in E_p$, there exists scalars $a_1,\dots,a_k$ such that $v_p = a^i s_i(p)$. Defining 

$$
\varphi(p, v_p) = (p,a_1,\dots,a_k) \in U \times \Bbb R^k,
$$

we obtain a local trivialization.

What happens to the transition functions under this correspondence? Suppose that $U \cap V \ne \emptyset$ and that we have two frames $s = (s_1,\dots, s_k)$ and $\sigma = (\sigma_1,\dots,\sigma_k)$ over $U$ and $V$ associated to trivializations $\varphi_U : E\vert_U \to U \times \Bbb R^k$ and $\varphi_V : E\vert_V \to V \times \Bbb R^k$ respectively. At each point $p \in U \cap V$, we have that 

$$
\begin{align*}
\varphi_U \circ \varphi^{-1}_V(p,e_j) &= (p, g_{UV}(p)e_j) \\
&= \left(p, \sum_i g^i_j(p)e_i\right) \\
&= \sum_i g^i_j(p) (p, e_i),
\end{align*}
$$

where $g_{UV} = [g^i_j]$ is a matrix of smooth functions. Applying $\varphi^{-1}_U$ yields

$$
\begin{align*}
\varphi^{-1}_V(p,e_j) &= \varphi^{-1}_U\left(\sum_i g^i_j(p) (p, e_i)\right) \\
&= \sum_{i} g^i_j(p) \varphi^{-1}_U(p,e_i).
\end{align*}
$$

As $s$ is associated to $\varphi_U$ and $\sigma$ to $\varphi_V$ this gives the relationship 

$$
\sigma_j(p) = \sum_i g^i_j(p)s_i(p)
$$

which in terms of matrices[^3] is $\sigma = sg_{UV}$.

<div class="proposition">
A vector bundle $E \to M$ admits a flat connection if and only if it admits a trivializing open cover in which all the transition functions are constant.
</div>

<div class="proof">
Suppose that $\nabla$ is a flat connection on $E$. Choose a good cover $\\{U_i\\}$ for $M$, i.e. a cover such that $U_i$ and $U_i \cap U_j$ are contractible. For each $U_i$, pick $p_i \in U_i$ and consider a basis for $E_{p_i}$. Extend this to a local parallel frame $e_i$ using the flatness of $\nabla$ and the good cover. Now on $U_i \cap U_j$ the frames $e_i$ and $e_j$ are related by $e_j = e_ig$ where $g : U_i \cap U_j \to \mathrm{GL}(n,\Bbb R)$ is a matrix $g = [g^i_j]$ of smooth functions. This gives

$$
\begin{align*}
\nabla e_j &= \nabla(e_i g) \\
&= \nabla(e_i)g + e_idg,
\end{align*}
$$

where $dg$ is the matrix $[dg^i_j]$. Since $e_i$ and $e_j$ are both parallel we obtain that $e_idg = 0$ which implies that $dg = 0$ i.e. $g$ is constant. The local trivializations corresponding to these frames and transition functions yield a trivializing open cover with constant transition functions.

Conversely, if the collection $\{(U_i, \varphi_i : E\vert_{U_i} \to U_i \times \Bbb R^k) \}$ is a trivializing open cover with constant transition functions $g_{ij} : U_i \cap U_j \to \mathrm{GL}(k,\Bbb R)$, then on each $U_i$ we can define a flat connection $\nabla_i$ by specifying that the local frames associated to the trivializations are parallel. That is $\nabla_i e_i = 0$. Since the transition functions are constant $\nabla_i$ and $\nabla_j$ agree on $U_i \cap U_j$. Gluing these $\nabla_i$'s together we obtain a global flat connection.
 
</div>


---

Recall from our discussions about the Pontryagin and Chern classes that each of them is defined using the curvature matrix $\Omega$ of a connection. We thus obtain a necessary condition for a vector bundle to admit a flat[^4] connection.

<div class="proposition">
If a real or complex vector bundle possesses a flat connection then all of its Pontryagin or Chern classes with rational coefficients are zero.
</div>

For example, the tangent bundle of $\Bbb CP^2$ does not admit a flat connection. The above proposition illustrates that vector bundles admitting flat connections are quite rare.

To see that the condition on vanishing characteristic classes is not sufficient, note that the Pontryagin classes of the tangent bundles of $\Bbb S^n$ for any $n$ vanish as the spheres are stably trivial[^5]. However, $T\Bbb S^2$ does _not_ admit any flat connections.

Heuristically speaking, the reason for this is that if we pick any point $p$ on $M$, the flatness of the connection yields that the parallel transport $P_\gamma$ along a loop $\gamma$ depends only on the homotopy class of $\gamma$. Since $\pi_1(\Bbb S^2) = 0$, we are free to move vectors around the sphere to generate a nowhere-vanishing vector field. This contradicts the Poincaré–Hopf theorem and so $T\Bbb S^2$ cannot admit a flat connection.

The reasoning above is actually part of a more general theory. Parallel transport gives rise to a representation 

$$
\rho : \pi_1(M,p_0) \to \mathrm{GL}(k,\Bbb C),
$$

and the image of $\rho$ is the holonomy group of $\nabla$. Conversely, given a representation $\rho : \pi_1(M, p_0) \to \mathrm{GL}(k, \Bbb C)$ we can construct a flat vector bundle $E$ by defining

$$
E = \widetilde{M} \times \Bbb C^k / \sim,
$$

where $\widetilde{M}$ is the universal cover of $M$ and $\sim$ the equivalence relation given by the action 

$$
\gamma \cdot (p, v) = (\gamma(p), \rho(\gamma)v),
$$

of $\pi_1(M,p_0)$. The idea is that the natural flat connection of $\widetilde{M} \times \Bbb C^k$ descends to a flat connection on $E$ as the action of $\pi_1(M,p_0)$ via $\rho$ preserves the flat structure.

There is actually a whole chain of equivalences between the three categories 

<ol>
    <li>Local Systems over a connected manifold $M$,</li>
    <li>Finite dimensional representations of $\pi_1(M, p_0)$,</li>
    <li>Vector bundles $E \to M$ with a flat connection $\nabla$,</li>
</ol>

due to Deligne. I won't go into these this time around, but to end this, let's go over the correspondence of vector bundles and locally free $\mathcal{O}_X$-modules which we will need in a future post. This correspondence turns out to be in fact an equivalence of categories.

Let $E \to X$ be a vector bundle of rank $k$ over a smooth manifold $X$. Consider $\mathcal{O}_X$-module $\Gamma$ given by the sheaf of sections of $E$. For each open $U \subset X$ the sheaf $\Gamma \vert_U$ is locally free, that is $\Gamma \vert_U \cong \bigoplus\_{i=1}^k \mathcal{O}_X \vert_U$. The reason is that we can identify sections $s : U \to E\vert_U \cong U \times \Bbb R^k$ with maps $U \to \Bbb R^k$.

Conversely, if $\mathcal{F}$ is a locally free sheaf of rank $k$ on $X$ and $\\{U_i\\}$ a cover which trivializes $\mathcal{F}$, i.e. $\mathcal{F}\vert\_{U_i} \cong \bigoplus\_{i=1}^k \mathcal{O}_X\vert\_{U_i}$. On $U_i \cap U_j$ we have maps of sheaves

$$
\xymatrix{
\bigoplus_{i=1}^k \mathcal{O}_X\vert_{U_i \cap U_j} \ar@/_1pc/@{->}[rr]_{\varphi_i\circ\varphi_j^{-1}} & \mathcal{F}\vert_{U_i\cap U_j} \ar@{->}[l]_{\varphi_j} \ar@{->}[r]^{\varphi_i} & \bigoplus_{i=1}^k \mathcal{O}_X\vert_{U_i \cap U_j},
}
$$

with $\varphi_i \circ \varphi^{-1}_j$ being an $\mathcal{O}_X\vert\_{U_i \cap U_j}$-module isomorphism. This yields an invertible $(k \times k)$-matrix, i.e. an element in $\mathrm{GL}(k, \mathcal{O}_X(U_i \cap U_j))$ which we can identify with a map $g\_{ij} : U_i \cap U_j \to \mathrm{GL}(k,\Bbb R)$. Recall now that these transition functions $g\_{ij}$ determine a vector bundle of rank $k$ on $X$ via the vector bundle construction theorem[^6].

That's all this time around, in the near future I'll probably come back to this topic from the viewpoint of local systems and those representations of the fundamental group.

---

[^1]: Note that here we also have $\Gamma\left(\Lambda^k T^\ast M \otimes E\right) \cong \Gamma\left(\Lambda^k T^\ast M\right) \otimes_{C^\infty(M)} \Gamma(E) = \Omega^k(M) \otimes_{C^\infty(M)} \Gamma(E)$.

[^2]: When $E = M \times \Bbb R$ we have that $\Omega^k(E) = \Gamma\left(\Lambda^k T^\ast M \otimes (M \times \Bbb R)\right)$ which gives $\Omega^k(M) \otimes_{C^\infty(M)} \Gamma(M \times \Bbb R)$, but $\Gamma(M \times \Bbb R)$ can be identified with $C^\infty(M)$ which yields $\Omega^k(M \times \Bbb R) = \Omega^k(M)$.

[^3]: It is worth mentioning here that we are thinking about $s$ and $\sigma$ as row vectors. In literature, you may see this as $\sigma = g_{UV}s$, in which case the authors are treating $s$ and $\sigma$ as column vectors. This is just transposing the equation $\sigma = sg_{UV}$ we obtained.

[^4]: It's probably worth emphasizing here that "flatness" is a property of the connection, _not_ the bundle. Curvature is always defined with respect to some connection on the bundle and thus is not an inherent property of the bundle. Asking something about the "flatness of a bundle" does not make sense. It's like asking how fast a car is without considering any wheels on it. Think about the torus in $\Bbb R^3$. The picture that comes to your head is probably a donut sitting in three-space. You are implicitly assuming that it is equipped with a non-flat connection, but the tangent bundle of the torus actually admits a flat connection as well.

[^5]: Stably trivial meaning that $T\Bbb S^n \oplus \Bbb R$ is trivial. 

[^6]: For the theorem, see exercise $10$-$6$ from Introduction to Smooth Manifolds by John M. Lee.
