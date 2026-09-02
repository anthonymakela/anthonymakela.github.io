---
layout: post
title: "Koszul-Malgrange Theorem"
categories: [Complex Geometry]
mathjax: true
published: false
excerpt_separator: <!--more-->
---

Today, we'll cover the Koszul-Malgrange theorem. The Koszul-Malgrange theorem is a fundamental result in complex geometry that relates smooth and holomorphic structures on vector bundles. Simply put, it gives a one-to-one correspondence between holomorphic structures on a smooth complex vector bundle $E$, and operators $\bar{\partial}_E$ satisfying the integrability condition $\bar{\partial}^2_E = 0$.

<!--more-->

---

Let $X$ be a complex manifold and $E \to X$ a holomorphic vector bundle. Then there exists an operator 

$$
\bar{\partial}_E : \mathcal{A}^{0}(X,E) \to \mathcal{A}^{0,1}(X,E)
$$

defined in the following manner. Let $\{U_i\}$ be a trivializing open cover for $X$, and let $e = (e_1,\dots,e_r)$ be a local frame for $U_i$. For $s = s^ie_i \in \mathcal{A}^{0,0}(U_i,E)$, set

$$
\bar{\partial}_E(s) = \bar{\partial}(s^i) \otimes e_i,
$$

where $\bar{\partial}$ is the Dolbeault operator on $X$. To see that this is well-defined on all of $E$, note that if $U_i \cap U_j \ne \emptyset$, then

$$
\widetilde{e}_j = g_{ij}e_i,
$$

where $\widetilde{e} = (\widetilde{e}\_1,\dots,\widetilde{e}\_r)$ is a local frame for $U_j$ and $g_{ij}$ the transition functions. For

$$
s = s^ie_i = \widetilde{s}^j\widetilde{e}_j,
$$

this gives 

$$
s^i = g_{ij}\widetilde{s}^j,
$$

and hence

$$
\bar{\partial}_E(s) = \bar{\partial}(s^i)\otimes e_i = \bar{\partial}(g_{ij}\widetilde{s}^j) \otimes e_i = (\bar{\partial}(g_{ij})\widetilde{s}^j) + g_{ij}\bar{\partial}(\widetilde{s}^j)) \otimes e_i.
$$


Since $E$ is holomorphic, the transition maps $g_{ij}$ are holomorphic and so

$$
(\bar{\partial}(g_{ij})\widetilde{s}^j) + g_{ij}\bar{\partial}(\widetilde{s}^j)) \otimes e_i = g_{ij}\bar{\partial}(\widetilde{s}^j)\otimes e_i,
$$

yields

$$
\bar{\partial}_E(s) = g_{ij}\bar{\partial}(\widetilde{s}^j)\otimes e_i = g_{ij}\bar{\partial}(\widetilde{s}^j)\otimes g_{ji}\widetilde{e}_j = \bar{\partial}(\widetilde{s}^j)\otimes \widetilde{e}_j.
$$

<div class="definition">
A Dolbeault operator on a smooth complex vector bundle is a $\mathbb{C}$-linear operator
$$
\bar{\partial}_E : \mathcal{A}^{0}(X,E) \to \mathcal{A}^{0,1}(X,E)
$$
that satisfies $\bar{\partial}_E^2 = 0$ and the Leibniz rule
$$
\bar{\partial}_E(fs) = \bar{\partial}f \otimes s + f\bar{\partial}_E(s),
$$
for any smooth function \( f \) and \( s \in \mathcal{A}^{0}(X,E) \).
</div>

<div class="lemma">
Let $E \to X$ be a smooth complex vector bundle over a complex manifold $X$. Let $U \subset X$ be an open set, and let $\eta \in \Omega^{0,1}(U,\operatorname{End}(E))$ be a $(0,1)$-form satisfying 
$$
\bar{\partial}\eta = \eta \wedge \eta.
$$
Then for any $x \in U$, there exists $$
</div>