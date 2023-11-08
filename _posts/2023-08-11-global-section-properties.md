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
</div>

The main topic of this post is to focus on the behavior of $\Gamma(-)$ with the tensor product $\otimes$. It would not be farfethced to suspect that for vector bundles $E$ and $F$ over $M$ the natural map

$$
\alpha : \Gamma(E) \otimes_{C^\infty(M)} \Gamma(F) \to \Gamma(E \otimes F)
$$

is an isomorphism. It turns out that this holds, but before this let's go over some results regarding the map $\alpha$.

<div class="lemma">
If $E$ and $F$ are both trivial bundles, then $\alpha$ is an isomorphism of $C^\infty(M)$-modules.
</div>

<div class="proof">
Since the bundles are trivial we can choose global frames $(\sigma_1,\dots,\sigma_n)$ and $(\tau_1,\dots,\tau_m)$ of $E$ and $F$ respectively. These form free bases for $\Gamma(E)$ and $\Gamma(F)$ and so 
$$
\{\sigma_i \otimes_{C^\infty(M)} \tau_j \mid 1 \le i \le n, \ 1 \le j \le m \}
$$
is a free basis for $\Gamma(E) \otimes_{C^\infty(M)} \Gamma(F)$. Since  
$$
\{\sigma_i \otimes \tau_j \mid 1 \le i \le n, \ 1 \le j \le m \}
$$
trivializes $E \otimes F$ and is a free basis for $\Gamma(E \otimes F)$. Now
$$
\alpha(\sigma_i \otimes_{C^\infty(M)} \tau_j) = \sigma_i \otimes \tau_j
$$
yields that $\alpha$ is an isomorphism.
</div>

Now in order to prove the genral case we need the following theorem which I won't be proving here.

<div class="theorem">
Given a vector bundle $E \to M$, there exists a vector bundle $E^\perp \to M$ such that $E \oplus E^\perp$ is trivial. 
</div>

The proof is rather technical, but this will be the main workhorse in proving that $\alpha$ is an isomorphism in the general case.

A quick digression in linear algebra. If we have finite-dimensional vector spaces $V_1,V_2$ and $W$ there is a linear isomorphism
$$
\varphi : (V_1 \oplus V_2) \otimes W \to (V_1 \otimes W) \oplus (V_2 \otimes W).
$$

Consider the map $\varphi : (V_1 \oplus V_2) \times W \to (V_1 \otimes W) \oplus (V_2 \otimes W)$ given by $((v_1,v_2),w) \longmapsto v_1 \otimes w + v_2 \otimes w$.

This map is bilinear since the tensor product distributes over sums and we can pull out scalars so it induces a linear map $\varphi : (V_1 \oplus V_2) \otimes W \to (V_1 \otimes W) \oplus (V_2 \otimes W)$. To see that this is a linear isomorphism instead of getting our hands dirty with explicit constructions we will take the abstract nonsense approach. Note that $- \otimes W$ is left-adjoint to $\operatorname{Hom}(W,-)$ and so for $U \in \textbf{FDVect}_k$

$$
\begin{align*}
\operatorname{Hom}((V_1 \oplus V_2)\otimes W,U) &\cong \operatorname{Hom}(V_1 \oplus V_2,\operatorname{Hom}(W,U)) \\
&\cong \operatorname{Hom}(V_1,\operatorname{Hom}(W,U)) \oplus \operatorname{Hom}(V_2,\operatorname{Hom}(W,U)) \\
&\cong \operatorname{Hom}(V_1 \otimes W,U) \oplus \operatorname{Hom}(V_2 \otimes W,U) \\
&\cong \operatorname{Hom}((V_1 \otimes W) \oplus (V_2 \otimes W), U)
\end{align*}
$$

and since this holds for every object $U \in \textbf{FDVect}_k$ the Yoneda lemma yields that $(V_1 \oplus V_2)\otimes W$ and $(V_1 \otimes W) \oplus (V_2 \otimes W)$ are isomorphic.

The reason we did this is that now we can conclude that there is a natural isomorphism of bundles $(E \oplus E^{\perp}) \otimes (F \oplus F^{\perp}) \cong (E \otimes F) \oplus (E \otimes F^{\perp}) \oplus (E^{\perp} \otimes F) \oplus (E^{\perp} \otimes F^{\perp})$ which contains $E \otimes F$.

Onto the main event.

<div class="theorem">
The $C^\infty(M)$-linear map $\alpha : \Gamma(E) \otimes_{C^\infty(M)} \Gamma(F) \to \Gamma(E \otimes F)$ is a canonical isomorphism of $C^\infty(M)$-modules.
</div>

<div class="proof">
Consider the following commutative diagram and the maps $\iota : E \otimes F \to (E \oplus E^{\perp}) \otimes (F \oplus F^{\perp})$ and $\rho : (E \oplus E^{\perp}) \otimes (F \oplus F^{\perp}) \to E \otimes F$

$$
\require{AMScd}
\begin{CD}
\Gamma((E \oplus E^{\perp}) \otimes (F \oplus F^{\perp})) @<{\alpha}<< \Gamma(E \oplus E^{\perp}) \otimes_{C^{\infty}(M)} \Gamma(F \oplus F^{\perp}) \\
@AA{\iota_\ast}A @A{\iota_\ast \otimes \iota_\ast}AA \\
\Gamma(E \otimes F) @<{\alpha}<< \Gamma(E) \otimes_{C^{\infty}(M)} \Gamma(F)
\end{CD}
$$
by our previous results the map on the top is an isomorphism of $C^{\infty}(M)$-modules. Since $\rho \circ \iota = \operatorname{id}_{E \otimes F}$ the functoriality of $\Gamma$ implies that the vertical arrows are injective from which it follows that $\alpha : \Gamma(E) \otimes_{C^\infty(M)} \Gamma(F) \to \Gamma(E \otimes F)$ is injective. Consider now the diagram

$$
\require{AMScd}
\begin{CD}
\Gamma((E \oplus E^{\perp}) \otimes (F \oplus F^{\perp})) @<{\alpha}<< \Gamma(E \oplus E^{\perp}) \otimes_{C^{\infty}(M)} \Gamma(F \oplus F^{\perp}) \\
@VV{\rho_\ast}V @V{\rho_\ast \otimes \rho_\ast}VV \\
\Gamma(E \otimes F) @<{\alpha}<< \Gamma(E) \otimes_{C^{\infty}(M)} \Gamma(F)
\end{CD}
$$
in which the vertical arrows are surjective by the same reasoning. It follows that $\alpha : \Gamma(E) \otimes_{C^\infty(M)} \Gamma(F) \to \Gamma(E \otimes F)$ is surjective which yields the result.
</div>
