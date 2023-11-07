---
layout: post
title: "Sections, Tensor Products and Duals"
categories: differential-geometry
mathjax: true
---

This will be a quickie regarding some of the properties of the global sections of a vector bundle $\pi : E \to M$ on a smooth manifold $M$.

Let's begin by recalling what sections are. A <b>section</b> of a vector bundle over an open set $U$ is a function $s : U \to E$ such that $\pi \circ s = \operatorname{id}_U$. For each $p \in U$ the section picks out one element in the fiber $E_p$. The set of all smooth sections of $E$ over $U$ is denoted by $\Gamma(U,E)$. When $U = M$ we call the elements of $\Gamma(M,E) =: \Gamma(M)$ global sections.

The set $\Gamma(U,E)$ forms a vector space over $\Bbb R$ and is in fact a module over the ring $C^\infty$. If $f$ is a smooth function on $U$ and $s \in \Gamma(U,E)$, then for $p \in U$

$$
(fs)(p) := f(p)s(p) \in E_p
$$

makes $fs$ a smooth section of $E$ over $U$.

<div class="proposition" text="1.">
There is a canonical isomorphism 
$$
\Gamma(T^\ast M) \cong \operatorname{Hom}_{C^\infty(M)}(\Gamma(TM), C^\infty(M)).
$$
</div>

For the proof we are going to need a couple of lemmas.

<div class="lemma">
Let $\alpha \in \operatorname{Hom}_{C^\infty(M)}(\Gamma(TM), C^\infty(M))$ and let $U \subset M$ be an open set. If $X \in \Gamma(TM)$ and $X\vert_U \equiv 0$, then $\alpha(X)\vert_U \equiv 0$.
</div>

<div class="proof">

</div>

<div class="proof" text="Proposition 1">
Consider $\omega \in \Gamma(T^\ast M)$ and $X \in \Gamma(TM)$. We get $\omega(X) \in C^\infty(M)$ by
$$
\omega(X)(p) := \omega_p(X_p).
$$
For $f \in C^\infty(M)$ we have that $\omega(fX) = f\omega(X)$ so we can view $\omega$ as an element of $\operatorname{Hom}_{C^\infty(M)}(\Gamma(TM), C^\infty(M))$. We therefore have an injective $C^\infty(M)$-module homomorphism $\Gamma(T^\ast M) \hookrightarrow \operatorname{Hom}_{C^\infty(M)}(\Gamma(TM), C^\infty(M))$.
</div>
