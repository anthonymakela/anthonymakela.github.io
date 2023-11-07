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

<div class="proposition">
There is a canonical isomorphism 
$$
\Gamma(T^\ast M) \cong \operatorname{Hom}_{C^\infty(M)}(\Gamma(TM), C^\infty(M)).
$$
</div>

For the proof we need couple of lemmas from the post on Local Properties.

<div class="proof">
Consider the map $\Phi : \Gamma(T^\ast M) \to \Gamma(TM)^\ast$ given by
$$
\omega \longmapsto (X \longmapsto \omega(X)).
$$
This map is $C^\infty(M)$-linear and to see that it's injective suppose that $\Phi(\omega)=\Phi(\alpha)$, then $$\Phi(\omega)(X)=\Phi(\alpha)(X)$$ that is $$\omega(X)=\alpha(X)$$ for all $X \in \Gamma(TM)$. Now for any $p \in M$ $$\omega(X)(p)=\omega_p(X_p)=\alpha(X)(p)=\alpha_p(X_p).$$ Thus $\Phi$ is injective.

To show that this map is surjective consider $\tau \in \Gamma(TM)^\ast$. We want to exhibit $\eta \in \Gamma(T^\ast M)$ such that $\Phi(\eta) = \tau$ or $\Phi(\eta)(X) = \eta(X) = \tau(X)$ and $\eta_p(X_p) = \tau(X)(p)$ for every $X \in \Gamma(TM)$ and $p \in M$. We proceed as follows: given $p  \in M$ and $X_p \in T_pM$ we extend $X_p$ to $X \in \Gamma(TM)$ and set $\eta_p(X_p) = \tau(X)(p)$. Even though this seems like it should not be well-defined as we extended $X_p$ arbitarily it is since we know that $\tau$ is a local operator.

<br>
<br>

For the sake of completeness here is the argument that $\tau$ depends only on $X_p$. It suffices to show that if $X_p = 0$, then for any extension $X$ the equality $\tau(X)(p) = 0$ holds. Consider a neighborhood $U \ni p$ in $M$ and choose a bump function $\rho$ such that $\rho(p)=1$ and $\operatorname{supp}\rho \subset U$. Now $\rho X$ is $0$ at $p$ and so $\tau(\rho X)(p) = 0$. Since $\tau$ is $C^\infty(M)$-linear
$$
0 = \tau(\rho X)(p) = \rho(p)\tau(X)(p) 
$$
which implies that $\tau(X)(p) = 0$.