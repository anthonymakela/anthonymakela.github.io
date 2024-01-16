---
layout: post
title: "Chern Classes"
categories: [Differential Geometry]
mathjax: true
published: false
excerpt_separator: <!--more-->
---

The final topic in our discussions considering characteristic classes will be that of <b>Chern classes</b>. In the foreseeable future, I might write about characteristic classes from a different viewpoint. The way we have been doing this for now is based on the Chern-Weil Theory, but there is an alternative, more topological approach using something called <i>classifying spaces</i>.

<!--more-->

Since Chern classes are characteristic classes associated with complex vector bundles, we need to define what such bundles are and how we talk about connections and curvature of such bundles.

---

A complex vector bundle of rank $n$ is nothing more than a fiber bundle with fiber $\Bbb C^n$ and a structure group $\mathrm{GL}(n,\Bbb C)$. More concretely we have the following definition.

<div class="definition">
A complex vector bundle of rank $n$ on $M$ is a smooth manifold together with a smooth map $\pi : E \to M$ and the structure of an $n$-dimensional complex vector space on any fibre $E_p := \pi^{-1}(p)$ satisfying the following conditions:

<ul>
  <li>
    For every $p \in M$, there is a neighborhood $U \ni p$ and a diffeomorphism $\varphi : \pi^{-1}(U) \to U \times \Bbb C^n$ such that the following diagram:  
    $$
    \xymatrix{
        \pi^{-1}(U) \ar[rr]^{\varphi} \ar[dr]_{\pi} && U \times \mathbb{C}^n \ar[dl]^{\operatorname{pr}_1} \\
        & U
    }
    $$
    commutes. The map $\varphi$ is called a local trivialization of $E$ over $U$.
  </li>
  <li>
    For each $p \in M$, the map $\varphi\vert_p : E_p \to \{p\} \times \Bbb C^n$ is a linear isomorphism.
  </li>
</ul>
</div>

As you might see, the definition is pretty much identical to the one you met when you studied smooth manifolds and their vector bundles for the first time.

There are slight nuances we need to consider when we transition from the real case to the complex. For starters, the module $\Gamma(E)$ is no longer only a module over the ring $C^\infty(M)$ of smooth real-valued functions, but also a module over the set of all complex-valued smooth functions denoted by $C^\infty(M,\Bbb C)$[^1]. 

Similarly for differential forms we set 

$$
\Omega^k(M,\Bbb C) := \Omega^k(M) \otimes \Bbb C
$$

and call the elements of $\Omega^k(M,\Bbb C)$ complex $k$-forms. Exterior differentiation 

$$
\Omega^k(M,\Bbb C) \to \Omega^{k+1}(M,\Bbb C)
$$

is now defined by extending $d$ linearly over $\Bbb C$.


You might wonder what happens to our de Rham cohomology theory now as we've transitioned to consider forms in $\Omega^k(M,\Bbb C)$. We call the cochain complex $(\Omega^k(M,\Bbb C), d)$ the complex de Rham complex and denote the cohomology of this complex by $H^\ast_{dR}(M,\Bbb C)$ or simply $H^\ast(M,\Bbb C)$.

---

In the real case we were able to consider the Riemannian metric on vector bundles $E \to M$ since the fibers were real vector spaces. The analogue of this in the complex case is the <b>Hermitian metric</b> which I will define shortly.

On the complex vector space $\Bbb C^n$, the Hermitian inner product is given by

$$
\langle z, w\rangle = \sum_{j=1}^n z_j\bar{w}_j.
$$

Using this we can define a complex inner product on any complex vector space $V$.

<div class="definition">
A <b>complex inner product</b> on a complex vector space $V$ is a positive-definite, Hermitian-symmetric, sesquilinear form $\langle \ , \ \rangle : V \times V \to \Bbb C$. 
</div>

We now have the ingredients to define a Hermitian metric on a complex vector bundle $E \to M$.

<div class="definition">
A Hermitian metric on a complex vector bundle $E \to M$ assigns to each $p \in M$ a complex inner product $\langle \ , \ \rangle_p$ on the fiber $E_p$. This assignment is required to be smooth in the sense that if $s$ and $\sigma$ are sections of $E$, then $\langle s,  \sigma\rangle : M \to \Bbb C$ is a smooth complex-valued function on $M$.
</div>

It is not too difficult to see that a finite positive linear combination $\sum a_i \langle \ , \ \rangle_i$ of complex inner products on a complex vector space $V$ is again a complex inner product. This in turn yields that we can use partitions of unity to obtain the existence of a Hermitian metric on any complex vector bundle. 

---

A connection on a complex vector bundle $E \to M$ is defined exactly the same way as it is defined on a real vector bundle. It is an $\Bbb R$-bilinear map 

$$
\nabla : \Gamma(TM) \times \Gamma(E) \to \Gamma(E)
$$

that is $C^\infty(M)$-linear in the first argument, $\Bbb C$-linear in the second argument and satisfies the Leibniz rule. Using partitions of unity it is again not too difficult to show that every complex vector bundle has a connection.

If $E \to M$ is equipped with a Hermitian metric we call $\nabla$ a metric connection, and it is said to be compatible with the Hermitian metric if for all $X \in \Gamma(TM)$ and $s,\sigma \in \Gamma(E)$

$$
X\langle s,\sigma\rangle = \langle \nabla_X s, \sigma\rangle + \langle s, \nabla_X \sigma\rangle.
$$

If $e_1,\dots,e_n$ is a local frame over $U$, a connection $\nabla$ can be represented by a matrix $\omega = [\omega^i_j]$ of complex-valued $1$-forms:

$$
\nabla_X e_j = \sum_i \omega^i_j(X)e_i.
$$

The only difference to the real case is that the $1$-forms are now complex. Same story holds for the curvature tensor $R$. As for the curvature matrix $\Omega = [\Omega^i_j]$, the structural equation $\Omega = d\omega + \omega \wedge \omega$ holds also in the complex case.

---

Its probably no surprise that if $e = \begin{bmatrix} e_1 & \cdots & e_n\end{bmatrix}$ and $\bar{e} = \begin{bmatrix} \bar{e}_1 & \cdots & \bar{e}_n\end{bmatrix}$ are two local frames for which $\bar{e} = ea$ for $a \in \mathrm{GL}(n,\Bbb C)$, then the connection matrix and curvature matrix transform exactly the same as in the real case:

$$
\begin{align*}
\bar{\omega} &= a^{-1}\omega a + a^{-1}da \\
\bar{\Omega} &= a^{-1}\Omega a.
\end{align*}
$$

This yields that a complex polynomial $P$ on $\mathfrak{gl}(n,\Bbb C)$ that is invariant under conjugation by elements of $\mathrm{Gl}(n,\Bbb C)$ will define a global form $P(\Omega)$ on $M$. Like we have shown previously, the form $P(\Omega)$ is closed and the cohomology class $[P(\Omega)]$ will be independent of the connection.

<div class="definition">
The Chern classes $c_i(E)$ on a complex vector bundle $E \to M$ are defined by

$$
c_k(E) = \left[f_k\left(\frac{i}{2\pi}\Omega\right)\right] \in H^{2k}(M, \Bbb C).
$$
</div>

Notice the similarity to the Pontryagin classes. The Pontryagin classes can actually be regarded as the Chern classes of a complexification $E \otimes_{\Bbb R} \Bbb C$ of a real vector bundle $E$. Indeed with our definition[^2] $p_k(E) = c_{2k}(E \otimes \Bbb C) \in H^{4k}(M)$.


As before, we'll define the <b>total Chern class</b> by

$$
c(E) := \left[\det\left(I + \frac{i}{2\pi} \Omega\right)\right] = 1 + c_1(E) + \dots + c_n(E).
$$

---

For the sake of concreteness, let's calculate the Chern classes of the complex projective space $\Bbb CP^n.$ Before we do this we need to go over a few results on vector bundles

---


[^1]: Note that $C^\infty(M,\Bbb C) = C^\infty(M) \otimes \Bbb C$.

[^2]: The definition here follows the practices from Bott & Tu. The usual way to define Pontryagin classes in terms of the Chern classes is to set $p_k(E) = (-1)^kc_{2k}(E \otimes \Bbb C)$ to ignore the odd Chern classes. Had we defined $p_k(E) = \left[f_{2k}\left(\frac{1}{2\pi}\Omega\right)\right]$, we would indeed have ended up with $p_k(E) =  \left[f_{2k}\left(\frac{1}{2\pi}\Omega\right)\right] =  \left[\left(\frac{1}{2\pi}\right)^{2k}f_{2k}\left(\Omega\right)\right]$. If you're careful enough with the coefficient $\left(1/2\pi\right)^{2k}$, you'll see that it equals $(-1)^k\left(i/2\pi\right)^{2k}$ and hence $p_k(E) = (-1)^kc_{2k}(E \otimes \Bbb C)$.