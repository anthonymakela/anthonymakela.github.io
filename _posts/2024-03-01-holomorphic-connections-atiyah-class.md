---
layout: post
title: "Holomorphic Connections and The Atiyah Class"
categories: [Complex Geometry, Differential Geometry]
mathjax: true
published: true
excerpt_separator: <!--more-->
---

Until now, our blog discussions have centered on real or complex vector bundles over real manifolds. However, today we'll delve into connections on holomorphic vector bundles. I will assume a certain level of familiarity with complex geometry; however, if you possess a solid understanding of differential geometry, you should find this discussion accessible.

<!--more-->

---

As I mentioned, so far we've dealt with a real manifold $M$ and a real or complex vector bundle $E$ over $M$. For the remainder of this post, we'll consider a complex manifold $X$ and a holomorphic vector bundle $E$ over $X$.

Recall that on a complex manifold there exists a natural almost complex structure $J : TX \to TX$ corresponding to the complex structure on $X$. Complexifying the real tangent bundle to $T_\Bbb C X$, the endomorphism $J$ can be extended complex-linearly to an endomorphism $J : T_\Bbb C X \to T_\Bbb C X$. Since the eigenvalues of $J$ are $i$ and $-i$, the bundle $T_\Bbb C X$ splits as a direct sum:

$$
T_\Bbb C X = T^{1,0}X \oplus T^{0,1}X,
$$

where $T^{1,0}X$ and $T^{0,1}X$ are the eigenbundles corresponding to $i$ and $-i$ respectively. The bundle $T^{1,0}X$ is called the <b>holomorphic tangent bundle</b>, and the bundle $T^{0,1}X$ is called the <b>anti-holomorphic tangent bundle</b>. Denoting the respective holomorphic and anti-holomorphic cotangent bundles as $T^\ast_{1,0}X$ and $T^\ast_{0,1}X$,  The decomposition gives us  

$$
\begin{align*}
    \Lambda^k T_{\Bbb C}^\ast X &= \Lambda^k\left(T^\ast_{1,0}X \oplus T^\ast_{0,1}X\right) \\
    &=  \bigoplus_{p+q=k} \Lambda^pT^\ast_{1,0}X  \otimes \Lambda^qT^\ast_{0,1}X .
\end{align*}
$$

We will write $\Lambda^{p,q} T^*X := \Lambda^pT^\ast_{1,0}X \otimes_{\Bbb C} \Lambda^qT^\ast_{0,1}X$. A complex differential form of type $(p,q)$ is a section of the sheaf $\Omega^{p,q}(-) := \Gamma\left(-, \Lambda^{p,q}T^\ast X\right)$. Note that this also gives a decomposition

$$
\begin{align*}
\Omega^k(X) &= \Gamma\left(X, \Lambda^kT^\ast X\right) \\
&= \Gamma\left(X, \bigoplus_{p+q=k} \Lambda^{p,q}T^*X\right) \\
&= \bigoplus_{p+q=k}  \Gamma\left(X, \Lambda^{p,q}T^*X\right) \\
&= \bigoplus_{p+q=k} \Omega^{p,q}(X),
\end{align*}
$$

since $\Gamma$ is an additive functor. For a complex vector bundle $E$, we define $\Omega^{p,q}(-,E)$ to be the sheaf

$$
U \mapsto \Omega^{p,q}(U,E) := \Gamma\left(U, \Lambda^{p,q}T^*X \otimes E \right).
$$

<div class="lemma">
If $E$ is a holomorphic vector bundle, then there exists a natural $\Bbb C$-linear operator $\bar{\partial}_E : \Omega^{p,q}(E) \to \Omega^{p,q+1}(E)$ with $\bar{\partial}^2_E = 0$ and which satisfies the Leibniz rule 
$$
\bar{\partial}_E(f\alpha) = \bar{\partial} f \wedge \alpha + f\bar{\partial}_E \alpha.
$$
</div>

<div class="proof">
Let $U$ be a framed open set with a frame $e = (e_1,\dots, e_k)$. A section $\alpha \in \Omega^{p,q}(U,E)$ can be written as $\alpha = \sum_i \alpha^i \otimes e_i$ for $\alpha^i \in \Omega^{p,q}(U)$. Set

$$
\bar{\partial}_E \alpha := \sum_i \bar{\partial}\alpha^i \otimes e_i.
$$

To see that this expression is independent of the choice of local frame, let $e' = (e'_1,\dots,e'_k)$ be another frame over $U$, by the above construction, we obtain an operator $\bar{\partial}'_E$. Now $e_i = \sum_j g^j_i e'_j$ for a transition matrix of holomorphic functions $[g^j_i]$, and

$$
\begin{align*}
\bar{\partial}'_E \alpha &= \bar{\partial}'_E\left(\sum_{i,j} \alpha^i \otimes g^j_i e'_j\right) \\
&= \sum_{i,j} \bar{\partial}(\alpha^i g^j_i) \otimes e'_j \\
&= \sum_{i,j} \bar{\partial}\alpha^i \otimes g^j_ie'_j \\
&= \sum_i \bar{\partial}\alpha^i \otimes e_i \\
&= \bar{\partial}_E \alpha.
\end{align*}
$$

Hence we can extend this to all of $\Omega^{p,q}(E)$. By construction, this satisfies $\bar{\partial}^2_E = 0$ and the Leibniz rule.

</div>

If $\nabla$ is now any connection on $E$, then since $\Omega^1(E) = \Omega^{1,0}(E) \oplus \Omega^{0,1}(E)$, we can decompose $\nabla$ on $E$ into its two components $\nabla = \nabla^{1,0} \oplus \nabla^{0,1}$. Note that

$$
\nabla^{0,1}(fs) = \bar{\partial}f\otimes s + f\nabla^{0,1}s,
$$

where $\bar{\partial} : \Omega^0(E) \to \Omega^{0,1}(E)$ is the operator we discussed above. Just as we've seen compatible connections in the case of Riemannian manifolds, there is an analog in the complex setting.

<div class="definition">
Let $(E,h)$ be a Hermitian vector bundle. A connection $\nabla$ on $E$ is said to be compatible with the metric if for sections $s,t$, we have

$$
d(h(s,t)) = h(\nabla s, t) + h(s,\nabla t).
$$
</div>

Note that the above equation is an equality of $1$-forms. The terms $h(\nabla s, t)$ and $h(s, \nabla t)$ are both sections of $T^\ast_\Bbb C X$.

<div class="lemma">
A connection $\nabla$ on a Hermitian vector bundle $(E,h)$ is compatible with the metric if and only if $\nabla h = 0$, where by $\nabla$ we also denote the naturally induced connection on the bundle $(E \otimes \bar{E})^\ast$.
</div>

<div class="proof">
This follows directly by calculating the covariant derivative of the tensor field $h$. We have that

$$
\begin{align*}
\nabla h(s,t) &= d(h(s,t)) - h(\nabla s, t) - h(s,\nabla t),
\end{align*}
$$

which when $\nabla h = 0$ gives exactly the compatibility condition. 
</div>

In the Riemannian setting, we have the canonical Levi-Civita connection on the tangent bundle, you might wonder whether or not we have something analogous when we have a holomorphic vector bundle with a Hermitian metric. The answer is affirmative and we'll state this as the following proposition.

<div class="proposition">
Let $E$ be a holomorphic vector bundle with a Hermitian metric $h$. Then there exists a unique connection that is compatible with the metric, and compatible with the holomorphic structure, in the sense that

$$
\nabla^{0,1} = \bar{\partial}.
$$
</div>

<div class="proof">
We will first prove uniqueness. This is a local problem so consider a framed open set $U$ with a holomorphic frame $e = (e_1,\dots,e_k)$. Since $E\vert_U \cong U \times \Bbb C^k$, the connection is then determined completely by the connection $1$-forms $\omega^j_i$ given by 

$$
\nabla e_j = \sum \omega^i_j \otimes e_i.
$$

Since $\nabla$ is compatible with $h$, we obtain

$$
\begin{align*}
dh(e_i,e_j) &= h\left(\nabla e_i, e_j\right) +h\left(e_i, \nabla e_j\right) \\
&= h\left(\omega^k_i \otimes e_k, e_j\right) +h\left(e_i, \omega^k_j \otimes e_k\right) \\
&= \omega^k_i h(e_k,e_j) + h(e_i,e_k)\bar{\omega}^k_j.
\end{align*}
$$

Now, note that $\nabla$ being compatible with the holomorphic structure means that $\nabla s \in \Omega^{1,0}(U,E)$ for any holomorphic local section $s$. It follows that $\omega^k_i$ is of type $(1,0)$ so 

$$
\partial h(e_i,e_j) = \omega^k_ih(e_k,e_j) \ \text{ and } \ \bar{\partial} h(e_i,e_j) = h(e_i,e_k)\bar{\omega}^k_j,
$$

or as matrices $\partial h = \omega^T h$ and $\bar{\partial}h = h\bar{\omega}$. This yields that $\omega = \bar{h}^{-1}\partial\bar{h}$ is a unique solution to both equations. So $\omega$ is completely determined locally by the Hermitian metric, and thus so is $\nabla$. The argument also constructs such a connection on each framed open set. Then by uniqueness, these local connections glue to a connection on all of $E$ and so we are done.
</div>

The unique connection described in the previous proposition is called the <b>Chern connection</b>[^1]. To get a better feel for this, let's see how this behaves in terms of holomorphic line bundles.

<div class="example">
Let $L \to X$ be a holomorphic line bundle. Then, locally on a framed open set $U$ with a frame $e$, a Hermitian metric $h$ is given by a positive real function $h(e,e)$. It follows that 

$$
\omega = \partial \log h,
$$

so locally the Chern connection on $L$ is given by $\nabla = d + \partial \log h$.
</div>

---

Let's now turn our attention to <b>holomorphic connections</b>[^2]. These kinds of connections are much more restrictive and their existence on any holomorphic vector bundle is not guaranteed.

<div class="definition">
Let $E$ be a holomorphic vector bundle over a complex manifold $X$. A holomorphic connection on $E$ is a $\Bbb C$-linear map of sheaves

$$
\nabla : E \to T^\ast_{1,0}X \otimes E,
$$

such that $\nabla fs = \partial f \otimes s + f\nabla s$ for any local holomorphic function $f$ and any local holomorphic section $s$.

</div>

Here $E$ and $T^\ast_{1,0}X \otimes E$ both the the vector bundle and the sheaf of holomorphic sections of these bundles[^3]. To see that $\partial f \in \Lambda^{1,0}T^\ast X$ in the above definition, recall that $\bar{\partial}\partial f = - \partial\bar{\partial}f$. Since $f$ is holomorphic $-\partial\bar{\partial}f = 0$ so $\bar{\partial}\partial f = 0$, i.e. $\partial f$ is of type $(1,0)$.

Most of the basic constructions of connections carry over to holomorphic connections. Notably the difference $\nabla_1 - \nabla_2$ is a holomorphic section of $T^\ast_{1,0}X \otimes E$ and so locally any holomorphic connection is of the form $\partial + A$, where $A$ is a holomorphic section of $T^\ast_{1,0}X \otimes E$.

Given this local description, we see that holomorphic connection induces a $\Bbb C$-linear map $\nabla : \Omega^0(E) \to \Omega^{1,0}(E)$ for which $\nabla fs = \partial f \otimes s + f\nabla s$. So $\nabla$ "looks like" the $(1,0)$-part of a regular connection and indeed $\nabla + \bar{\partial}$ defines an ordinary connection on $E$.

As mentioned before, for an arbitrary connection on $E$, the $(1,0)$-part need not be a holomorphic connection in general. It can send holomorphic sections on $E$ to those of $\Omega^{1,0}(E)$ which are not holomorphic, i.e. in $\Gamma(T^\ast_{1,0}X \otimes E)$.

Since these kinds of connections do not generally exist, as often done in mathematics, we want to find an obstruction for the existence of such a thing. To do so, we consider the problem locally and see whether or not we can glue our local data to something global.

Let's begin by considering a a trivializing open cover $\\{U_i\\}$ with holomorphic trivializations $\varphi_{i} : E\vert_{U_i} \to U_i \times \Bbb C^k$ for the bundle $E$. The local holomorphic connections are now of the form $\partial + A_i$. Recall from <a href=" https://anthonymakela.com/differential%20geometry/2023/12/27/connection-and-curvature-forms.html" style="color:#680530; text-decoration: underline;">Connection and Curvature Forms</a> that over $U_i \cap U_j$, these glue if and only if 

$$
A_j = g^{-1}_{ij}A_ig_{ij} + g^{-1}_{ij}\partial g_{ij},
$$

where $g_{ij}$'s are the transition functions. Composing with $\varphi^{-1}_j$ from the left and $\varphi_j$ from the right one obtains

$$
\varphi^{-1}_j \circ g^{-1}_{ij} \partial g_{ij} \circ \varphi_j = \varphi^{-1}_j \circ A_j \circ \varphi_j - \varphi^{-1}_i \circ A_i \circ \varphi_i. 
$$

Now, if you stare at this for a while you might notice that the right-hand side of the equation looks like a boundary. Knowing that the transition maps $g_{ij}$ form a Čech cocycle implies that the right-hand side does so as well. This motivates the following definition.

<div class="definition">
The <b>Atiyah class</b> 

$$
A(E) \in H^1\left(X, T^{\ast}_{1,0}X \otimes \operatorname{End}(E)\right)
$$

of the holomorphic vector bundle $E$ is given by the Čech cocycle

$$
A(E) = \{U_i \cap U_j, \varphi^{-1}_j \circ g^{-1}_{ij} \partial g_{ij} \circ \varphi_j\}.
$$
</div>

We also obtain the following proposition which follows directly from what we discussed above.

<div class="proposition">
A holomorphic vector bundle $E$ admits a holomorphic connection if and only if its Atiyah class $A(E)$ is trivial.
</div>

---

A quick digression on curvature before we continue with the theory regarding Atiyah classes. Recall that the curvature $F_\nabla$ of a connection $\nabla$ on a vector bundle $E$ is given by 

$$
F_\nabla = \nabla \circ \nabla : \Omega^0(E) \to \Omega^2(E).
$$

In <a href="https://anthonymakela.com/differential%20geometry/2024/02/16/flat-connections.html" style="color:#680530; text-decoration: underline;">Flat Connections</a> we denoted the exterior covariant derivative by $d_\nabla$, but here, we'll just stick with using $\nabla$ for both the connection and its natural extension $\Omega^k(E) \to \Omega^{k+1}(E)$.  


Since we are going to need the local expression for $F_\nabla$, let's see how this behaves on the trivial bundle $M \times \Bbb C^k$. For the trivial connection $\nabla = d$, we just obtain $F_\nabla = 0$. Suppose now that $\nabla = d + A$ and $s$ is a section of $M \times \Bbb C^k$. We have that

$$
\begin{align*}
F_\nabla s &= (d+A)(d+A)s \\
&= (d+A)(ds + As) \\
&= d^2s + d(As) + A(ds) + A(As) \\
&= dA(s) - A(ds) + A(ds) + (A \wedge A)s \\
&= (dA + A \wedge A)s.
\end{align*}
$$

That is, on the trivial bundle, the curvature is given by $F_\nabla = dA + A \wedge A$. Recall now that I briefly mentioned in the beginning of <a href="https://anthonymakela.com/differential%20geometry/2023/12/29/pontryagin-euler-chern.html" style="color:#680530; text-decoration: underline;">Pontryagin and Euler Classes
</a> that if we have a connection compatible with the metric, we obtain more information about the connection and curvature matrices. Not surprisingly, we obtain something similar in our current setting.

<div class="proposition">
<ol>
    <li>
    If $(E,h)$ is a Hermitian vector bundle and $\nabla$ is compatible with $h$, then 

    $$
    h(F_\nabla s_i, s_j) + h(s_i, F_\nabla s_j) = 0,
    $$

    i.e. $F_\nabla$ is skew-Hermitian.
    </li>
    <li>
    If $\nabla$ is compatible with the holomorphic structure, then $F_\nabla$ has no $(0,2)$-component, i.e.

    $$
    F_\nabla \in \Omega^{2,0}(X, \operatorname{End}(E)) \oplus \Omega^{1,1}(X, \operatorname{End}(E)). 
    $$

    </li>

    <li>
    If $\nabla$ is the Chern connection, then $F_\nabla$ is a skew-Hermitian real form in $\Omega^{1,1}(X, \operatorname{End}(E))$.
    </li>
</ol>
</div>

<div class="proof">
<ol>
    <li>
        It suffices to prove this locally, and as we did at the beginning of <a href="https://anthonymakela.com/differential%20geometry/2023/12/29/pontryagin-euler-chern.html" style="color:#680530; text-decoration: underline;">Pontryagin and Euler Classes</a>, we only need to show that the compatibility of $\nabla$ with the metric implies that the connection matrix is skew-Hermitian since then the argument follows directly from the second structural equation. To this end, let $e = (e_1,\dots, e_k)$ be a local orthonormal frame. Then 

        $$
        \begin{align*}
        0 &= dh(e_i,e_j) \\
        &= h(\nabla e_i, e_j) + h(e_i,\nabla e_j) \\
        &= h(\omega^k_i \otimes e_k, e_j) + h(e_i, \omega^k_j \otimes e_k) \\
        &= \omega^k_ih(e_k,e_j) + \bar{\omega}^k_jh(e_i,e_k) \\
        &= \omega^j_i + \bar{\omega}^i_j,
        \end{align*}
        $$

        i.e. $\omega^j_i = -\bar{\omega}^i_j$ which yields that $F_\nabla$ is skew-Hermitian. 
    </li>
    <li>
    Since $\nabla$ splits into a $(1,0)$-component and a $(0,1)$-component for which the latter equals $\bar{\partial}$, we obtain
    
    $$
    \begin{align*}
    F_\nabla &= \nabla^2 \\
    &= \nabla^{1,0} \circ \nabla^{1,0} + \nabla^{1,0} \circ \bar{\partial} + \bar{\partial} \circ \nabla^{1,0} + \bar{\partial}  \circ \bar{\partial} \\
    &= \nabla^{1,0} \circ \nabla^{1,0} + \nabla^{1,0} \circ \bar{\partial} + \bar{\partial} \circ \nabla^{1,0},
    \end{align*}
    $$
    where $\nabla^{1,0} \circ \bar{\partial} + \bar{\partial} \circ \nabla^{1,0}$ maps to the $(1,1)$-part.
    </li>
    <li>
    This follows from combining the two above items. Note that $\nabla^{1,0} \circ \nabla^{1,0}$ maps to the $(2,0)$-part and since $F_\nabla$ is skew-Hermitian, conjugating yields a map to the $(0,2)$-part, but this is zero since the Chern connection is compatible with the holomorphic structure. Locally one could argue as follows: Since $F_\nabla = dA + A \wedge A$ and $A = \bar{h}^{-1}\partial \bar{h}$, we obtain

    $$
    \begin{align*}
    dA &= (\partial + \bar{\partial})A \\
    &= \bar{\partial}A + \partial(\bar{h}^{-1}\partial \bar{h}) \\
    &= \bar{\partial}A + \partial\bar{h}^{-1}\wedge \partial \bar{h} + \bar{h}^{-1} \wedge \partial(\partial \bar{h}) \\
    &= \bar{\partial}A + \partial\bar{h}^{-1}\wedge \partial \bar{h} \\
    &= \bar{\partial}A - \bar{h}^{-1}\partial \bar{h}\bar{h}^{-1} \wedge \partial \bar{h} \\
    &= \bar{\partial}A - \bar{h}^{-1}\partial \bar{h} \wedge \bar{h}^{-1}\partial \bar{h}.
    \end{align*}
    $$
    Hence

    $$
    \begin{align*}
    F_\nabla &= dA + A \wedge A \\
    &= dA + \bar{h}^{-1}\partial \bar{h} \wedge \bar{h}^{-1}\partial \bar{h} \\
    &= \bar{\partial}A \\
    &= \bar{\partial}(\bar{h}^{-1}\partial \bar{h}) \in \Omega^{1,1}(X,\operatorname{End}(E)).
    \end{align*}
    $$

    </li>
</ol>
</div>

Again, to get our hands dirty, let's consider the line bundle case.

<div class="example">
Let $(L,h)$ be a Hermitian holomorphic line bundle and $\nabla$ the corresponding Chern connection. The above proposition gives that $F_\nabla$ is a real form of type $(1,1)$. We know that $A = \partial \log(h)$ and so

$$
\begin{align*}
F_\nabla &= dA + A \wedge A \\
&= (\partial + \bar{\partial})(\partial \log(h)) + \partial \log(h) \wedge \partial \log(h) \\
&= \bar{\partial}\partial \log(h).
\end{align*}
$$

</div>

Considering now the Chern connection of a holomorphic Hermitian bundle, the Bianchi identity gives us

$$
\bar{\partial} F_\nabla = \nabla(F_\nabla)^{1,2} = 0.
$$

That is, as an element of $\Omega^{1,1}(X, \operatorname{End}(E))$, $F_\nabla$ is $\bar{\partial}$-closed. We therefore obtain a natural Dolbeault cohomology class $[F_\nabla] \in H^1(X, T^{\ast}_{1,0}X \otimes \operatorname{End}(E))$. To see that $[F\_\nabla]$ does not depend on $\nabla$, locally any other connection is of the form $\nabla + A$ and 

$$
\begin{align*}
F_{\nabla + A} &= F_\nabla + \nabla A + A \wedge A.
\end{align*}
$$

If $\nabla$ and $\nabla + A$ are both Chern connections that are compatible with certain Hermitian metrics, then both $F_{\nabla + A}$ and $F_\nabla$ are of type $(1,1)$ and $A \wedge A \in \Omega^{2,0}(X,\operatorname{End}(E))$. It follows that

$$
\begin{align*}
\nabla A + A \wedge A &= \left(\nabla A + A \wedge A\right)^{1,1} \\
&= (\nabla A)^{1,1} \\
&= \bar{\partial} A.
\end{align*}
$$

Hence $F_{\nabla + A} = F_\nabla + \bar{\partial} A$ which yields $[F_{\nabla + A}] = [F_\nabla]$.

---

Eventually, we want to study the correspondence between holomorphic vector bundles that admit a flat connection and holomorphic vector bundles with trivial Atiyah class. Since flat connections are characterized by their vanishing curvature, it's reasonable to ask whether or not there is a relationship between the curvature of a connection and the Atiyah class of a holomorphic vector bundle. 

<div class="theorem">
Let $(E,h)$ be a Hermitian holomorphic vector bundle and $\nabla$ the Chern connection on $E$. Then

$$
[F_\nabla] = A(E) \in H^1(X, T^\ast_{1,0} \otimes \operatorname{End}(E)).
$$

</div>

<div class="proof">
The proof will be done by comparing Dolbeault and Čech cohomology. Let $\mathcal{U} = \{U_i\}$ be a trivializing open cover for $E$, with trivializations $\varphi_i : E\vert_{U_i} \to U_i \times \Bbb C^k$. Consider the following commutative diagram of sheaves:

$$
\xymatrix{
T^\ast_{1,0}\otimes \operatorname{End}(E) \ar@{->}[d] \ar@{->}[r] & C^0(\mathcal{U},T^\ast_{1,0}\otimes \operatorname{End}(E)) \ar@{->}[r] \ar@{->}[d] & C^1(\mathcal{U},T^\ast_{1,0}\otimes \operatorname{End}(E)) \ar@{->}[d]^{i} \\
\Omega^{1,0}(\operatorname{End}(E)) \ar@{->}[d] \ar@{->}[r] & C^0(\mathcal{U},\Omega^{1,0}(\operatorname{End}(E)) \ar@{->}[r]^{\delta_1} \ar@{->}[d]^{\bar{\partial}} & C^1(\mathcal{U},\Omega^{1,0}(\operatorname{End}(E)) \\
\Omega^{1,1}(\operatorname{End}(E)) \ar@{->}[r]^{\delta_0} & C^0(\mathcal{U},\Omega^{1,1}(\operatorname{End}(E)). & 
}
$$

The curvature $F_\nabla$ of the Chern connection on $E$ is given locally on a trivializing open set $U_i$ by

$$
F_\nabla\vert_{U_i} = \varphi^{-1}_i \circ \bar{\partial}(\bar{h}_i^{-1}\partial \bar{h}_i) \circ \varphi_i,
$$

where $h_i$ is the matrix of the Hermitian metric $h$ on $U_i$. We obtain

$$
\begin{align*}
\delta_0(F_\nabla) &= \{U_i, \varphi^{-1}_i \circ \bar{\partial}(\bar{h}_i^{-1}\partial \bar{h}_i) \circ \varphi_i \} \\
&= \bar{\partial}\{U_i, \varphi^{-1}_i \circ (\bar{h}_i^{-1}\partial \bar{h}_i) \circ \varphi_i \}
\end{align*}
$$

as $\varphi_i$'s are holomorphic. It's thus sufficient to show that

$$
i\{U_i \cap U_j, \varphi^{-1}_j \circ (\varphi^{-1}_{ij}\partial g_{ij}) \circ \varphi_j\} = \delta_1\{U_i, \varphi^{-1}_i \circ (\bar{h}_i^{-1}\partial \bar{h}_i) \circ \varphi_i\},
$$

since $A(E) = \{U_i \cap U_j, \varphi^{-1}_j \circ (\varphi^{-1}_{ij}\partial g_{ij}) \circ \varphi_j\}$. Using the definition for $\delta_1$, the right-hand side of the above equation yields

$$
\{U_i \cap U_j,  \varphi^{-1}_j \circ (\bar{h}_j^{-1}\partial \bar{h}_j) \circ \varphi_j - \varphi^{-1}_i \circ (\bar{h}_i^{-1}\partial \bar{h}_i) \circ \varphi_i \},
$$

and 

$$
\varphi^{-1}_j \circ (\bar{h}_j^{-1}\partial \bar{h}_j) \circ \varphi_j - \varphi^{-1}_i \circ (\bar{h}_i^{-1}\partial \bar{h}_i) \circ \varphi_i = \varphi^{-1}_j \circ (\bar{h}_j^{-1}\partial \bar{h}_j - g^{-1}_{ij} \circ (\bar{h}_i^{-1}\partial \bar{h}_i) \circ g_{ij}) \circ \varphi_j.
$$

Now the matrices $h_i$ and $h_j$ are related by $h_j = g^T_{ij}h_i\bar{g}_{ij}$ or, $\bar{h}_j = g_{ij}^\ast \bar{h}_i g_{ij}$. using this we have

$$
\begin{align*}
\bar{h}_j^{-1}\partial \bar{h}_j &= g^{-1}_{ij}\bar{h}^{-1}_{i}(g^\ast_{ij})^{-1}(g^\ast_{ij}\partial\bar{h}_ig_{ij} + g^\ast_{ij}\bar{h}_i\partial g_{ij}) \\
&= g^{-1}_{ij}(\bar{h}^{-1}_i\partial\bar{h}_i)g_{ij} + g^{-1}_{ij}\partial g_{ij},
\end{align*}
$$

where $\partial \bar{h}_j = g^\ast_{ij}\partial\bar{h}_ig_{ij} + g^\ast_{ij}\bar{h}_i\partial g_{ij}$ since $\partial g^\ast_{ij} = 0$. It follows that

$$
\varphi^{-1}_j \circ (\bar{h}_j^{-1}\partial \bar{h}_j) \circ \varphi_j - \varphi^{-1}_i \circ (\bar{h}_i^{-1}\partial \bar{h}_i) \circ \varphi_i = \varphi^{-1}_j \circ (\varphi^{-1}_{ij}\partial g_{ij}) \circ \varphi_j.
$$

</div>

<div class="corollary">
If a holomorphic vector bundle $E$ has a holomorphic connection, then all rational Chern classes vanish.
</div>

Notice again the similarity with flat connections. To study the relationship between these two classes of vector bundles, for a complex manifold $X$ we set

$$
\begin{align}
   \mathfrak{Fl}(X) := \left\{ 
   \begin{array}{c}
       \text{Holomorphic vector bundles over $X$} \\
       \text{that admit a flat connection.}
   \end{array}
   \right\}
\end{align}
$$

and

$$
\begin{align}
   \mathfrak{At}(X) := \left\{ 
   \begin{array}{c}
       \text{Holomorphic vector bundles over $X$} \\
       \text{for which $A(E)$ = 0.}
   \end{array}
   \right\}
\end{align}
$$

<div class="proposition">
Let $X$ be a complex manifold. Then $\mathfrak{Fl}(X) \subset \mathfrak{At}(X)$.
</div>

<div class="proof">
Let $E \to X$ be a vector bundle with a flat connection and $\widetilde{X}$ the universal cover of $X$. Then $E$ is of the form $\widetilde{X} \times_\rho \Bbb C^k$ for a representation $\rho : \pi_1(X) \to \mathrm{GL}(k, \Bbb C)$. The holomorphic connection $\partial$ on $\widetilde{X} \times \Bbb C^k$ is invariant under the action on $\pi_1(X)$ and hence descends to a holomorphic connection on $E$.
</div>

The converse of the aforementioned proposition is the interesting question, and as far as I'm aware, open when $X$ is for example compact and Kähler.

As we've done multiple times today, let's focus on line bundles first.

<div class="proposition">
Let $X$ be a compact Kähler manifold and $L$ a holomorphic line bundle with $A(L)=0$. Then $L$ is flat.
</div>

<div class="proof">
Any holomorphic line bundle over a compact Kähler manifold admits a <i>Hermite-Einstein</i> metric. Since the curvature of the corresponding Chern connection $\nabla$ is harmonic and $[F_\nabla] = A(L) = 0$ we obtain $F_\nabla = 0$, yielding the flatness of $\nabla$.
</div>

Note that the same argument works always when we have a connection with a harmonic curvature. 

We know that all Chern classes of a holomorphic vector bundle with a holomorphic connection vanish. It turns out that the existence of a holomorphic connection is a much stronger requirement in higher dimensions. For complex manifolds of dimension $1$, we automatically have that $\mathfrak{At}(X) = \mathfrak{Fl}(X)$. Next, I'll present a few definitions and then a theorem of Weil which gives some information on the case with dimension $1$.

<div class="definition">
A vector bundle $E$ is said to be <b>decomposable</b> if it is isomorphic to a nontrivial direct sum of subbundles. If not, it is said to be <b>indecomposable</b>.
</div>

<div class="definition">
The degree of a vector bundle $E$ is the degree of the line bundle $\det(E)$.
</div>

<div class="theorem" text="(Weil)">
An indecomposable vector bundle $E$ on a compact curve with $\deg(E) = 0$ has a flat connection.
</div>

If we now decompose a holomorphic vector bundle on a curve into a direct sum of indecomposable bundles

$$
E = E_1\oplus E_2 \oplus \dots \oplus  E_n,
$$

we can show that $E$ is flat if and only if each of the summands is flat. Thus, a vector bundle on a compact curve is flat (or equivalently has a holomorphic connection) if the Chern classes of the summands vanish.

On high-dimensional varieties the following theorem of Atiyah's yields a way to test whether or not a holomorphic connection exists on a holomorphic vector bundle. More precisely, we can test it on a suitable surface in $X$.

<div class="theorem">
Let $X$ be a projective manifold with $\dim X \ge 3$, $L$ an ample line bundle, and $E$ a holomorphic vector bundle on $X$. Then there is an $n_0$, such that for all larger $n$ and all smooth hypersurfaces $S$ with $\mathcal{O}_X(S) = L^n$ the following holds: The Atiyah class of $E$ vanishes if and only if the Atiyah class of $E\vert_S$ vanishes.
</div>


<div class="corollary">
Let $X$ be a projective manifold of dimension greater than or equal to $3$, and $E$ be a holomorphic vector bundle over $X$. Then there exists a complete intersection $S \subset X$ of dimension two such that

$$
A(E) = 0 \iff A\left(E\vert_S\right) = 0.
$$
</div>

The unfortunate thing now is that neither of these can be generalized. Before we see why, here are two notions regarding short exact sequences of vector bundles that we are going to need. 

<div class="definition">
Let $E$ and $G$ be vector bundles over $X$. Then $E$ is called an extension of $G$ if there is an short exact sequence of vector bundles

$$
0 \longrightarrow E \longrightarrow F \longrightarrow G \longrightarrow 0.
$$
</div>

<div class="definition">
Two extensions of $G$ by $E$ are <i>equivalent</i> if we have a commutative diagram

$$
\xymatrix{
0 \ar@{->}[r] & E \ar@{->}[r] \ar@{=}[d] & F_1 \ar@{->}[r] \ar@{->}[d] & G \ar@{->}[r] \ar@{=}[d] & 0 \\
0 \ar@{->}[r] & E \ar@{->}[r] & F_2 \ar@{->}[r] & G \ar@{->}[r] & 0.
}
$$

Note that the five lemma implies that the middle arrow is an isomorphism.
</div>


If the exact sequence $0 \longrightarrow E \longrightarrow F \longrightarrow G \longrightarrow 0$ splits we say that the extension is trivial. Also, given our correspondence with locally free sheaves, the extensions of $G$ by $E$ correspond one-to-one with the extensions of the associated sheaves $0 \longrightarrow \mathcal{E} \longrightarrow \mathcal{F} \longrightarrow \mathcal{G} \longrightarrow 0$. Henceforth, we will make very little distinction between locally free sheaves and vector bundles.

<div class="lemma">
The equivalence classes of extensions of $\mathcal{G}$ by $\mathcal{E}$ are in one-to-one correspondence with the elements of $H^1(X, \mathcal{Hom}(\mathcal{G}, \mathcal{E}))$. Said differently, we have

$$
\operatorname{Ext}^1(\mathcal{G}, \mathcal{F}) \cong H^1(X, \mathcal{Hom}(\mathcal{G}, \mathcal{E})).
$$

</div>

<div class="proof">

As a special case of the Grothendieck spectral sequence, we have a convergent spectral sequence

$$
E^{p,q}_2 = H^p(X, \mathcal{Ext}^q(\mathcal{G}, \mathcal{F})) \implies \operatorname{Ext}^{p+q}(\mathcal{G}, \mathcal{F}).
$$

From where we obtain a long exact sequence

$$
0 \rightarrow H^1(X, \mathcal{Hom}(\mathcal{G}, \mathcal{F})) \rightarrow \operatorname{Ext}^1(\mathcal{G}, \mathcal{F}) \rightarrow H^1(X, \mathcal{Ext}^1(\mathcal{G}, \mathcal{F})) \rightarrow H^2(X, \mathcal{Hom}(\mathcal{G}, \mathcal{F})) \rightarrow \dots
$$

Since we are dealing with the sheaves associated to vector bundles, each of them is locally free. In particular it follows that $\mathcal{Ext}^1$ vanishes and so the sequence reduces to

$$
0 \longrightarrow H^1(X, \mathcal{Hom}(\mathcal{G}, \mathcal{F})) \longrightarrow \operatorname{Ext}^1(\mathcal{G}, \mathcal{F}) \longrightarrow 0,
$$

yielding the desired result.

</div>

Consider now the following. Let $Y = \Bbb P^1$, $Z$ be an elliptic curve, and $X = Y \times Z$. Fix $(y_0,z_0) \in X$ and consider $Y = Y \times \{z_0\}$ and $Z = \{y_0\} \times Z$ as subspaces of $X$. For the canonical bundle of $X$ we obtain $\mathcal{O}_X(-2Z)$. Tensoring the structure sequence of $Z$ with $\mathcal{O}_X(2Z)$ we obtain

$$
0 \longrightarrow \mathcal{O}_X(Z) \longrightarrow \mathcal{O}_X(2Z) \longrightarrow \mathcal{O}_Z \otimes \mathcal{O}_X(2Z) \cong \mathcal{O}_Z \longrightarrow 0.
$$

Using the induced long exact sequence on cohomology and Serre duality this yields

$$
H^1(X, \mathcal{O}_X(2Z)) \longrightarrow H^1(Z, \mathcal{O}_Z) \longrightarrow H^2(X, \mathcal{O}_X(Z)) \cong H^0(X, \mathcal{O}_X(-3Z))^\ast = 0.
$$

Since $Z$ is an elliptic curve, the rank of $H^1(X, \mathcal{O}_X(2Z))$ is one, and we can pick an element $\xi \in H^1(X, \mathcal{O}_X(2Z))$ with $\varphi(\xi) = \eta \ne 0$, where $\varphi$ is the map $H^1(X, \mathcal{O}_X(2Z)) \to H^1(Z, \mathcal{O}_Z)$. The elements of $H^1(X, \mathcal{O}_X(2Z)) = H^1(X, \operatorname{Hom}(\mathcal{O}_X(-Z), \mathcal{O}_X(Z)))$ correspond exactly to the extensions of $\mathcal{O}_X(-Z)$ by $\mathcal{O}_X(Z)$. It follows that there exists a vector bundle $E$ of rank $2$ such that the exact sequence

$$
0 \longrightarrow \mathcal{O}_X(Z) \longrightarrow E \longrightarrow \mathcal{O}_X(-Z) \longrightarrow 0
$$

corresponds to $\xi$. Now

<ol>
    <li>
    The total Chern class of $E$ is trivial. Indeed 
    $$
    \begin{align*}
    c(E) &= c(\mathcal{O}_X(Z))c(\mathcal{O}_X(-Z)) \\
    &= 1 - c^2_1(\mathcal{O}_X(Z)) \\
    &= 1 - c^2_1(\pi^\ast_Y\mathcal{O}_Y(y_0)) \\
    &= 1 - \pi^\ast_Yc^2_1(\mathcal{O}_Y(y_0)) \\
    &= 1.
    \end{align*}
    $$
    </li>
    <li>
    $E$ is indecomposable. If we restrict the sequence corresponding to $\xi$ to $Z$, we obtain the exact sequence

    $$
    0 \longrightarrow \mathcal{O}_Z \longrightarrow E\vert_Z \longrightarrow \mathcal{O}_Z \longrightarrow 0,
    $$

    which corresponds to $\eta \ne 0 \in H^1(Z, \mathcal{O}_Z)$, hence $E\vert_Z$ is indecomposable and so is $E$.
    </li>

    <li>
    $E$ doesn't admit a holomorphic connection. If we now restrict the sequence corresponding to $\xi$ to $Y$, we obtain the exact sequence

    $$
    0 \longrightarrow \mathcal{O}_Y(y_0) \longrightarrow E\vert_Y \longrightarrow \mathcal{O}_Y(y_0) \longrightarrow 0.
    $$

    This corresponds to a class in

    $$
    H^1(Y, \mathcal{O}_Y(2y_0)) \cong H^0(Y, \mathcal{O}_Y(-4y_0))^\ast = 0,
    $$

    that is, the extension is trivial and $E\vert_Y \cong \mathcal{O}_Y(y_0) \oplus \mathcal{O}_Y(-y_0)$. Thus

    $$
    A\left(E\vert_Y\right) = A(\mathcal{O}_Y(y_0)) \oplus A(\mathcal{O}_Y(-y_0)) \ne 0,
    $$

    so the Atiyah class of $E$ cannot be zero yielding that $E$ doesn't admit a holomorphic connection.
    </li>
</ol>

The above calculations imply that Weil's theorem is already false in dimension $2$. That is, the vanishing of all Chern classes of an indecomposable bundle is not a sufficient condition for the existence of a holomorphic connection.

The following proposition from Atiyah's original paper "Complex Analytic Connections in Fibre Bundles" yields why the theorem on projective manifolds won't generalize.

<div class="proposition">
Let $E$ be an indecomposable holomorphic vector bundle on a projective manifold $X$ and suppose that $\dim X \ge 2$. Then $E\vert_S$ is indecomposable on every hyperplane $S$ of sufficiently high degree.
</div>

If $C$ is now a curve of sufficiently high degree in $X$, then $E\vert_C$ is indecomposable and has vanishing Chern classes. In other words, $A\left(E\vert_C\right) = 0$ and $E\vert_C$ is flat, but $A(E) \ne 0$.

That's all for today, next time we will likely take a look at semistable bundles.

---

[^1]: Note that some authors have $\omega = \partial h \cdot h^{-1}$. This depends on whether the group action (change of frame) is on the left or the right.

[^2]: Don't confuse the notion of a holomorphic connection with the notion of a connection that is compatible with the holomorphic structure. These are different things.

[^3]: There is a justification for the notation here. In the smooth category, when we define a connection as a map $\nabla : \Gamma(E) \to \Gamma(T^\ast M \otimes E)$, we are talking about global sections of the bundles $E$ and $T^\ast M \otimes E$. In the holomorphic case, this will not work. If $E$ is a holomorphic vector bundle over a complex manifold $X$, then there is no reason to believe that $\Gamma(X, E) \ne 0$. The way to get over this is to define connections as morphisms of sheaves.