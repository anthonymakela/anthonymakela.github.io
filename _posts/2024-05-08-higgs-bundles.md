---
layout: post
title: "Higgs Bundles"
categories: [Complex Geometry, Differential Geometry]
mathjax: true
published: false
excerpt_separator: <!--more-->
---

The following is going to be based mostly on a talk I'm going to give in a student seminar organized at the University of Helsinki. The theme is going to be that of Higgs bundles. 

<!--more-->

---

Around $1978$, Hitchin authored a paper titled "The Self-Duality Equations on a Riemann Surface," where he explored a specialized version of the self-dual Yang-Mills equations, originally rooted in quantum field theory. Rather than seeking solutions within the conventional $4$-dimensional space—where the Yang-Mills equations typically reside—Hitchin focused on finding solutions on Riemann surfaces, reducing the problem to two dimensions. This reduction endowed the equations with conformal invariance, allowing the search for solutions on any surface with a complex structure.

What Hitchin found out was that a solution to the Yang-Mills equation on a Riemann surface $\Sigma$ entails two things:
<ol>
    <li>
    A holomorphic vector bundle $E \to \Sigma$.
    </li>
    <li>
    A holomorphic section $\Phi$ of $\operatorname{End}(E) \otimes K$.
    </li>
</ol>

The so-called Hitchin equations are given by

$$
\begin{cases}F_{\nabla}+[\Phi ,\Phi ^{*}]=0\\{\bar {\partial }}\Phi =0,\end{cases}
$$

where $\nabla$ is a unitary connection on $E$.

What we'll be covering today will be slightly different from the usual treatment of these. The interesting bit about Higgs bundles are the moduli spaces. For a complex vector bundle $E$ on a compact Riemann surface $\Sigma$, the theorem of Narasimhan and Seshadri gives a correspondence of stable holomorphic structures to irreducible Hermite-Einstein connections or, equivalently, _unitary_ representations of the fundamental group.

These equations are invariant under unitary vector bundle automorphisms, also called gauge transformations, and the equivalence classes of solutions form a moduli space $\mathscr{M}$. When we restrict our study to the moduli space of irreducible solutions $\mathscr{M}^\ast$, that is solutions which cannot be decomposed into a product of solutions on lower–rank subbundles, it becomes a finite–dimensional smooth manifold. Somewhat surprisingly, this moduli space has an interesting geometric structure, and is therefore often studied in its own right. Most notably, it admits a Hyperkähler structure, consisting of a Riemannian metric and three compatible complex structures satisfying the quaternion relations. Each of these complex structures defines, together with the metric, an independent symplectic structure on $\mathscr{M}^\ast$.

The focus today will be in Hithcin systems, mirror symmetry and something called $P = W$ phenomena.

---

The goal here is to explore the application of infinite-dimensional symplectic reduction in constructing different moduli spaces, specifically focusing on the Higgs moduli space and the de Rham moduli space. Both of these spaces are non-compact hyper-Kähler manifolds, and interestingly, one can be seen as a hyper-Kähler rotation of the other. The Higgs moduli space, in particular, possesses a fibration by holomorphic Lagrangian tori, which is an example of an algebraically completely integrable system. When considering the rotated complex structure, this fibration corresponds to a special Lagrangian torus fibration in the de Rham moduli space. For vector bundles with the structure group $\mathrm{GL}(r,\mathbb{C})$, it turns out that the de Rham moduli space is self-mirror.

There is also a third moduli space known as the Betti moduli space. This space is an affine variety and, while it is analytically isomorphic to the de Rham moduli space, it is not algebraically isomorphic to it. However, from the perspective of mirror symmetry, whether the isomorphism is algebraic or analytic is irrelevant, so the Betti moduli space can be considered mirror to the de Rham moduli space.

A key difference is that the Betti moduli space has a filtration on its cohomology ring due to its nature as an algebraic variety. This filtration is preserved by algebraic maps but not by analytic ones. This raises the question: how does this filtration behave under the analytic isomorphism between the Betti and de Rham moduli spaces?

From the viewpoint of mirror symmetry, the special Lagrangian torus fibration in the de Rham moduli space is crucial. The $P = W$ conjecture proposes that this fibration induces a filtration on the cohomology of the de Rham moduli space that matches the filtration on the Betti moduli space's cohomology. Thus, mirror symmetry leads to a significant mathematical conjecture, which has been confirmed for the structure group $G = \mathrm{GL}(r,\mathbb{C})$.

Mirror symmetry is exhibited by one particularly beautiful class of examples, namely by various Hitchin systems. These are algebraically completely integrable systems, which are generally quite rare to find. Hitchin constructed a whole class of these, depending on a choice of Riemann surface and a complex reductive algebraic group $G$. Such a group has a so-called Langlands dual group $G^\lor$, and it turns out that certain moduli spaces associated to $G$-bundles and $G^\lor$-bundles over the chosen Riemann surface exhibit mirror symmetry. These moduli spaces can be obtained through infinite dimensional quotients, in the same way that one obtains the moduli space of HYM equations. This way, mirror symmetry can be used to relate areas within mathematics such as the geometric Langlands correspondence and the duality theory of Lie groups.

---

The Hermitian-Yang-Mills (HYM) equation is a partial differential equation which involves the curvature of a connection on a Hermitian vector bundle over a Kähler manifold. In essence, its solutions correspond to connections with the most "convenient" curvature properties. For instance, we would prefer to have flat connections. But flat connections on a vector bundle do not always exist, for example if $c_1(E) \ne 0$. $F_{A} \cdot \omega \in \Gamma(X, \operatorname{End}(E))$ by $F_{A} \wedge \omega^{n-1}=\left(F_{A} \cdot \omega\right) \omega^{n}$. This corresponds to orthogonal projection in $\Omega^{2}(X, \operatorname{End}(E))$ onto the span of $\omega \otimes \mathrm{id}_{E}$. The inner product on $\Omega^{2}(X, \operatorname{End}(E))$ is induced by the Kähler metric on $\mathcal{X}$ and the Hermitian metric on $\operatorname{End}(E)$.

<div class="definition">
Let $A$ be a connection on a Hermitian vector bundle $E$ over a Kähler manifold $\mathcal{X}$. Then we say that $A$ has constant central curvature if

$$
F_{A} \cdot \omega=\lambda(E) \mathrm{id}_{E}
$$

for some constant ${ }^{1} \lambda(E)$.
</div>

If $\lambda(E)=0$, i.e. when the vector bundle has degree 0 , then a connection has constant central curvature if and only if it is flat. However, when $E$ does not admit a flat connection, constant central curvature connections are those which are projectively flat, which is the next best thing that one could hope for.

<div class="definition">
Let $E \rightarrow X$ be a smooth vector bundle with Hermitian metric over a compact Kähler manifold $\mathcal{X}$. Let $A$ be a unitary connection on $E$ with curvature $F_{A}$. Then $A$ satisfies the HYM equation if

$$
\left\{\begin{array}{l}
F_{A} \cdot \omega=\lambda(E) \operatorname{id}_{E} \\
F_{A}^{0,2}=0
\end{array}\right.
$$
</div>

The first condition says that we are "minimising" the curvature, and the second condition says that the $\bar{\partial}$-operator determined by the $(0,1)$-part of the covariant derivative of $A$

$$
\nabla^{0,1}: \Gamma(X, E) \rightarrow \Omega^{0,1}(X, E)
$$

is the Dolbeault operator of some holomorphic structure $\mathcal{E}$ on $E$. The name is derived from Yang-Mills theory, combined with the theory of complex Hermitian geometry. We refer to the paper by Donaldson [74] as well as the book [8] by Donaldson and Kronheimer for its relation to Yang-Mills theory, in which they relate stability of bundles to Yang-Mills connections on complex surfaces. Presently, however, we are interested in complex threefolds, for which the following was proved by Uhlenbeck and Yau in [7].

<div class="theorem" text="(Kobayashi-Hitchin Correspondence)">
Let $\mathcal{E}$ be a Hermitian holomorphic vector bundle over a compact Kähler manifold. Then $\mathcal{E}$ is $\mu$-(poly)stable$ if and only if $E$ admits a HYM connection. This is the unique HYM connection in the orbit of the Chern connection.
</div>

This beautiful theorem relates something which can be defined algebraically, to something which requires the analysis of infinite dimensional vector spaces, partial differential equations and Hermitian metrics. This is quite a remarkable result, which gives us yet another insight into why complex geometry is a fascinating playground in which to combine algebraic and analytic methods. Another example of such interplay is, of course, mirror symmetry. Is the Kobayashi-Hitchin correspondence related to mirror symmetry in any tangible way? The Thomas-Yau conjecture asserts that the answer to this question is affirmative, as we will explain when discussing the conjecture.

Next, Hermitian-Yang-Mills as a Symplectic Quotient. The Kobayashi-Hitchin correspondence can also be viewed as a version of the KempfNess theorem, but now in infinite dimensions. We first recall the Kempf-Ness theorem in finite dimensions, which states the following. Suppose that $\mathcal{X} \subseteq \mathbb{P^{N}}$ is a complex manifold, with a complex reductive Lie group $G$ acting on $\mathcal{X}$ holomorphically. Suppose that $K$ is the maximal compact subgroup (e.g. $\operatorname{SU}(n) \subset \operatorname{SL}(n, \mathbb{C})$, which is not itself a complex Lie group, only a smooth Lie group) of $G$ acting on the symplectic manifold $(X, \omega)$ by symplectomorphisms, as well as preserving the complex structure. Suppose this action admits a momentum map $\mu: X \rightarrow \mathfrak{g}^{\ast}$ Let $\xi \in \mathfrak{g}^{*}$ be a central element. Then we can consider two quotients: the symplectic reduction $X / / K:=\mu^{-1}(\xi) / K$, or the GIT quotient $\mathcal{X} / G$. The Kempf-Ness theorem asserts that $X / / K \cong \mathcal{X} / G$ is an isomorphism.

We explain an important feature of the theorem above, for which we first need to recall some geometric invariant theory. The GIT quotient $\mathcal{X} / G$ requires a linearisation of the action, to an action of $G$ on $\mathcal{O}_{\mathcal{X}}(-1)$. The latter is the restriction of the tautological line bundle $\mathbb{C}^{N+1} \supset \mathcal{O}(-1) \rightarrow \mathbb{C} \mathbb{P}^{N}$. Choose a lift $\tilde{x}$ of a point $x \in X$ to the fibre $\pi^{-1}(x)$. Then the point $x$ is said to be semi-stable if and only if the closure of $G \cdot \tilde{x}$ does not contain the origin. There is a surjective morphism $\mathcal{X}^{s s} \rightarrow \mathcal{X} / G$ from the semi-stable points to the GIT quotient. Thus, in some sense, the GIT quotient only sees those points which are semi-stable. On the other hand, we have the symplectic quotient $X / / K$. The KempfNess theorem then implies that the momentum map allows us to select distinguished representatives of the (semi-)stable points. In particular, the momentum map informs us about the "right" notion of stability. This perspective is important for the ThomasYau conjecture, but more immediately, for what we are about to demonstrate.

We now move on to the infinite dimensional case. Let $E \rightarrow X$ be a Hermitian vector bundle on a complex manifold $\mathcal{X}$, and consider the space of unitary connections $\mathscr{A}$, which we identify with $\Omega^{1}(X, \mathfrak{u}(r))$, the 1-forms with values in the adjoint bundle of the $\mathrm{U}(r)$-bundle over $X$. We will consider Kähler manifolds $(\mathcal{X}, \omega)$.

<div class="proposition">
Define $\vartheta: T_{A} \mathscr{A} \times T_{A} \mathscr{A} \rightarrow \mathbb{R}$ by

$$
(a, b) \mapsto \int_{X} \operatorname{tr}(a \wedge b) \wedge \omega^{n-1}
$$

Then $\vartheta$ is a symplectic form on the infinite dimensional manifold $\mathscr{A}$.
</div>

For the proof, we use some Hodge theory. We recall that the Hermitian metric on $E$ together with the Riemannian metric on $X$ give us an inner product $\langle\cdot, \cdot\rangle$ on $\Omega^{k}(X, \mathfrak{u}(r))$, defined using the Hodge star operator $\star: \Omega^{k}(X, \mathfrak{u}(r)) \rightarrow \Omega^{n-k}(X, \mathfrak{u}(r))$ by

$$
(a, b) \mapsto \int_{X} \operatorname{tr}(a \wedge \star b)
$$

Here, the trace map is induced by the Hermitian metric, and we have

$$
\operatorname{tr}: \Omega^{k}(X, \mathfrak{u}(r)) \times \Omega^{l}(X, \mathfrak{u}(r)) \rightarrow \Omega^{k+l}(X)
$$

which is non-degenerate. The operator $L: \Omega^{k}(X, \mathfrak{u}(r)) \rightarrow \Omega^{k+2}(X, \mathfrak{u}(r))$ defined by $a \rightarrow$ $a \wedge \omega$ is called the Lefschetz operator, and its adjoint with respect to the inner product is denoted by $\Lambda: \Omega^{k}(X, \mathfrak{u}(r)) \rightarrow \Omega^{k-2}(X, \mathfrak{u}(r))$. Both $L$ and $\Lambda$ are isometries with respect to the inner product.

<div class="proof">
The form $\vartheta$ is evidently skew-symmetric and bilinear. It is defined independently of $A \in \mathscr{A}$, hence closed. For non-degeneracy, suppose that $0 \neq a \in T_{A} \mathscr{A}$. Consider the 1 -form $b:=\Lambda^{n-1} \circ \star a \in \Omega^{1}(X, \mathfrak{u}(r))$. Then

$$
\begin{array}{r}
\vartheta(a, b)=\int_{X} \operatorname{tr}(a \wedge b) \wedge \omega^{n-1}=\int_{X} \operatorname{tr}\left(a \wedge \Lambda^{n-1} \circ \star a \wedge \omega^{n-1}\right)=\int_{X} \operatorname{tr}\left(a \wedge L^{n-1} \circ \Lambda^{n-1} \circ \star a\right)= \\
\left\langle a, L^{n-1} \circ \Lambda^{n-1} a\right\rangle=\left\langle\Lambda^{n-1} a, \Lambda^{n-1} a\right\rangle=\|a\|^{2}>0
\end{array}
$$

where we used that $\Lambda$ is an isometry w.r.t. $\langle\cdot, \cdot\rangle$.
</div>

There an an infinite dimensional Lie group acting on $\mathscr{A}$, namely the group of unitary bundle automorphisms $\mathscr{G}$. It acts on connections $\nabla$ as $(\varphi \cdot \nabla) s=\varphi \circ \nabla \varphi^{-1}(s)$.

<div class="proposition">
The group $\mathscr{G}$ acts on $(\mathscr{A}, \vartheta)$ by symplectomorphisms.
</div>

<div class="proof">
First, we need to calculate the differential of the group action $\Theta^{\varphi}: \mathscr{A} \mapsto \mathscr{A}$, for $\varphi \in \mathscr{G}$. Using the transformation rule of connection 1-form and taking the curve $A+t a$ in $\mathscr{A}$, we obtain

$$
d \Theta_{A}^{\varphi}(a)=\left.\frac{d}{d t}\right|_{t=0} \varphi \cdot(A+t a)=\left.\frac{d}{d t}\right|_{t=0} \operatorname{Ad}_{\varphi} A+t \operatorname{Ad}_{\varphi} a+\varphi d \varphi^{-1}=\operatorname{Ad}_{\varphi^{-1}} a \in \Omega^{1}(X, \mathfrak{u}(r))
$$

We conclude that $d \Theta_{A}^{\varphi}=\operatorname{Ad}_{\varphi^{-1}}$. Since the trace is invariant under conjugation, it follows that $\Theta^{\varphi}$ is a symplectomorphism of $(\mathscr{A}, \vartheta)$.
</div>

<div class="proposition">
The symplectic action of $\mathscr{G}$ on $(\mathscr{A}, \vartheta)$ has momentum map

$$
\mu: A \mapsto F_{A} \wedge \omega^{n-1}
$$

</div>

---

<div class="definition">
Let $(X,g)$ be a Kähler manifold and $G$ a complex reductive algebraic group. A $G$-Higgs bundle on $X$ is a pair $(E,\Phi)$, where $E$ is a holomorphic $G$-bundle, and $\Phi \in H^0(X, T^\ast_{1,0}X \otimes \operatorname{Ad}(E))$ such that

$$
\begin{cases}\bar{\partial}\Phi=0\\\Phi \wedge \Phi =0.\end{cases}
$$

</div>

A Higgs bundle $E$ is called (semi-)stable if, for every subbundle $F \subset E$ such that $\Phi(F) \subset \Omega^1_X \otimes F$, we have $\mu(F) \le \mu(E)$. In most of our cases today we have $G = \mathrm{GL}(r,\Bbb C)$, but the theory can be generalized to any complex reductive algebraic group.

For now, fix a smooth vector bundle $E \to \Sigma$ over a Riemann surface $\Sigma$ and denote the moduli space of holomorphic structures on $E$ by $\mathcal{M}(r,d)$. Recall that the tangent space is given by $H^{0,1}(\Sigma, \operatorname{End}(E))$ and dual to this space is $H^{1,0}(\Sigma, \operatorname{End}(E))$ via the intergration map

$$
(\Phi, A) \mapsto \int_\Sigma \operatorname{tr}(\Phi \wedge A).
$$

In other words, the space of Higgs fields for a given complex structure $\bar{\partial} = \bar{\partial}_0 + A$ on $E$ is precisely $T^\ast_A \mathcal{M}(r,d)$. One can now consider the affine space $\mathscr{A} \times \Omega^{1,0}(\Sigma, \operatorname{End}(E)) = T^\ast \mathscr{A}$. This has a natural integrable complex structure, with respect to which the map

$$
((\alpha_1,\beta_1), (\alpha_2,\beta_2)) \mapsto i \int_{\Sigma}\operatorname{tr}(\alpha_1\wedge \beta_2 - \alpha_2\wedge \beta_1)
$$

is a holomorphic symplectic form. We also have a natural action of $\mathscr{G}_{\Bbb C}$ given by

$$
\Psi \cdot (\bar{\partial}, \Phi) = (\Psi \circ \bar{\partial} \circ \Phi^{-1}, \Psi \circ \Phi \circ \Psi^{-1}).
$$

<div class="proposition">
The action of $\mathscr{G}_{\Bbb C}$ on $T^\ast \mathscr{A}$ is symplectic, with moment map
$$
\mu(\bar{\partial},\Phi) = i\int_\Sigma \operatorname{tr}(\xi \wedge \bar{\partial}\Phi),
$$
where $\xi \in H^0(\Sigma, \operatorname{End}(E))$.
</div>

<div class="definition">
The moduli space of stable Higgs bundles of rank $r$ and degree $d$ is defined by
$$
\mathcal{M}_H(r,d) = T^\ast \mathscr{A} /\!\!/ \mathscr{G}.
$$
</div>

The curcial thing now is that $T^\ast \mathscr{A}$ is in fact a hyper-Kähler manifold. In these cases it is often possible to take the hyper-Kähler quotient which gives a hyper-Kähler structure on the quotient. To do this, we equip $E$ with a Hermitian connection and consider pairs $(A,\varphi)$, where $\nabla = \nabla_0 + A$ is a unitary connection on $E$, and $\varphi \in \Omega^1(\Sigma, \mathfrak{u}(E))$. The space $\mathscr{H}$ of such pairs is an affine space over $\Omega^1(\Sigma, \mathfrak{u}(E)) \oplus \Omega^1(\Sigma, \mathfrak{u}(E))$ and isomorphic to $T^\ast \mathscr{A}$ via $(\bar{\partial}, \varphi) \mapsto (\partial + \bar{\partial}, \varphi - \varphi^\dagger)$. This carries the following three complex structures

$$
\begin{align*}
I(\alpha,\beta) &= (\star \alpha, -\star\beta) \\
J(\alpha,\beta) &= (-\beta,\alpha) \\
K(\alpha,\beta) &= I \circ J(\alpha,\beta).
\end{align*}
$$

Furthermore, $\mathscr{H}$ carries three distinct symplectit forms which are holomorphic with respect to the respective complex structures:

$$
\begin{align*}
\omega_I((\alpha_1,\beta_1), (\alpha_2,\beta_2)) &= \int_\Sigma \operatorname{tr}(-\alpha_1\wedge \alpha_2 + \beta_1\wedge \beta_2) \\
\omega_J((\alpha_1,\beta_1), (\alpha_2,\beta_2)) &= \int_\Sigma \operatorname{tr}(\beta_1 \wedge \star \alpha_2 - \alpha_1 \wedge \star \beta_2) \\
\omega_K((\alpha_1,\beta_1), (\alpha_2,\beta_2)) &= \int_\Sigma \operatorname{tr}(\beta_1 \wedge \alpha_2 + \alpha_1\wedge \beta_2).
\end{align*}
$$

The unitary gauge group $\mathscr{G}$ acts on $\mathscr{H}$ by conjugation on both factors, as $\mathscr{G}_\Bbb C$ does on $T^\ast \mathscr{A}$.

<div class="theorem">
The metric $g$ on $\mathscr{H}$ defined by
$$
g((\alpha_1,\beta_1), (\alpha_2,\beta_2)) = - \int_\Sigma  \operatorname{tr}(\alpha_1\wedge \star \alpha_2 + \beta_1\wedge \star \beta_2)
$$
is a hyper-Kähler metric on $\mathscr{H}$ with respect to $I,J, K$, and $\omega_I,\omega_J,\omega_K$ are the corresponding symplectic forms. The group $\mathscr{G}$ acts by symplectomorphisms w.r.t each symplectit form, and carries a hyper-Kähler moment map defined by

$$
\begin{align*}
\mu_1(A,\Phi) &= -F_A + \Phi \wedge \Phi - 2\pi i \mu(E)\omega \\
(\mu_2 + i\mu_3)(A,\Phi) &= 2i\bar{\partial}\Phi,
\end{align*}
$$

where $\omega$ is the Kähler form on $\Sigma$.
</div>

The equations $F_A - \Phi \wedge \Phi = -2\pi i \mu(E) \omega$ and $\bar{\partial}\Phi = 0$ are precisely Hitchin's equations, and we would like to say that we have a diffeomorphism 

$$
\mathcal{M}_H(r,d) \cong \mathscr{H}  /\!\!/_h \mathscr{G},
$$

but this is not quite true since there are discrepancies between stability conditions. What is true is that $\mathcal{M}_H(r,d)$ is a dense open subset in the quotient. From here on, we define $\mathcal{M}_H(r,d)$ as this quotient.

So now, we are in a situation where the moduli space of stable Higgs bundles $\mathcal{M}_H(r,d)$ is itself a (non-compact) hyper-Kähler manifold. However, Hitchin showed that even more is true. One can give $\mathcal{M}_H(r,d)$ the structure of an algebraically completely integrable system. Define the Hitchin base as

$$
\mathcal{B} = \bigoplus_{k=1}^r H^0(\Sigma, K^{\otimes k}).
$$

We can compute the dimension of this space using the Riemann-Roch theorem, which states

$$
\dim H^0(\Sigma, \mathcal{F}) - \dim H^1(\Sigma, \mathcal{F}) = \int_\Sigma \operatorname{ch}(\mathcal{F})\operatorname{td}(\Sigma) = \deg(\mathcal{F}) - g + 1.
$$

Set $\mathcal{F} = K^{\otimes k}$. Serre duality gives now

$$
H^1(\Sigma, K^{\otimes k}) = H^0\left(\Sigma, \left(K^{\otimes k}\right)^\ast \otimes K\right)^\ast = H^0(\Sigma, K^{1-k})^\ast.
$$

Assuming $g > 1$, we have $\deg(K) = 2g-2 > 0$ and so $\dim H^0(\Sigma, K^{1-k}) = 0$ for $k > 1$. Using Riemann-Roch again we get

$$
\dim H^0(\Sigma, K^{\otimes k}) = \deg(K^{\otimes k}) - g +1 = k(2g-2) - g+1 = (2k-1)(g-1).
$$

It follows that

$$
\dim \mathcal{B} = g + \sum_{k=1}^r (2k-1)(g-1) = 1-r^2(1-g).
$$

The extra $g$ comes from separate consideration of $H^0(\Sigma, K)$. Now, morally $\mathcal{M}_H(r,d) = T^\ast \mathcal{M}(d,r)$ and 

$$
T_E \mathcal{M}(r,d) = H^1(\Sigma, \operatorname{End}(E)).
$$

Since $\operatorname{ch}(\operatorname{End}(E)) = \operatorname{ch}(E)\operatorname{ch}(E^\ast) = (r+c_1(E))(r-c_1(E)) = r^2$ we obtain

$$
\dim \mathcal{M}_H(r,d) = 2\dim\mathcal{M}(r,d) = 2\left(1- \int_\Sigma r^2\operatorname{td}(\Sigma)\right) = 2(1-r^2(1-g)),
$$

where we used the fact that $\dim H^0(\Sigma, \operatorname{End}(E)) = 1$ since $E$ is stable. All in all

$$
\dim \mathcal{B} = \frac{1}{2}\mathcal{M}_H(r,d).
$$

The next thing Hitchin does is define a map 

$$
F : \mathcal{M}_H(r,d) \to \mathcal{B}
$$

via

$$
(E,\Phi) \mapsto (\operatorname{tr}(\Phi), \dots, \operatorname{tr}(\wedge^r \Phi)),
$$

where $\wedge^k \Phi : \bigwedge^k E \to \bigwedge^k(E \otimes K) = \bigwedge^k E \otimes K^{\otimes k}$ and take the natural trace map so that

$$
\det(\lambda - \Phi) = \lambda^r + \sum_{k=1}^r \operatorname{tr}(\bigwedge^k \Phi)\lambda^{r-k}.
$$

In other words, the Hitchin map sends $\Phi$ to the coefficients of its characteristic polynomial. Choosing a basis for $H^0(\Sigma, K^{\otimes k})$ we can identify $\mathcal{B}$ with $\Bbb C^m$, where $m  = 1- r^2(1-g)$. We can then split $F$ into its components

$$
F_j = \pi_j \circ F : \mathcal{M}_H(r,d) \to \Bbb C^m \to \Bbb C.
$$

<div class="definition">
Let $b \in \mathcal{B}$. Define the <i>spectral curve</i> of $b$ to be
$$
\mathcal{C}_b = \{(z,w) \in T^\ast \Sigma \mid \det(w-\Phi(z)) = 0\},
$$
where $z$ is a local holomorphic coordinate on $\Sigma$, and $w$ a holomorphic coordinate on the fibre of $T^\ast \Sigma$.
</div>

The characteristic polynomial has generally speaking $r$ distinct roots and so this yields an $r$-sheeted ramified covering map $\pi : \mathcal{C}_b \to \Sigma$. Hitchin then proves the following

<div class="theorem">
The fibre $f^{-1}(b)$ of the Hitchin map is $\operatorname{Jac}(\mathcal{C}_b)$, the Jacobian variety of the spectral curve.
</div>

More generally, there is a singular locus, the discriminant locus, in the base $\mathcal{B}$ over which the spectral curve is singular, and one has to be somewhat more careful. But for a dense open subset in $\mathcal{B}$, the generic fibre is a projective complex torus. In summary we've obtained the following:

<div class="theorem" text="(Hitchin)">
The moduli space of stable Higgs bundles $\mathcal{M}_H(r,d)$ is a hyper-Kähler manifold, which admits the structure of an algebraically completely integrable system $F : \mathcal{M}_H(r,d) \to \mathcal{B}$. The fibers of $F$ are the Jacobian varieties of the spectral curves $\mathcal{C}_b \subset T^\ast \Sigma$ which are Lagrangian with respect to the holomorphic symplectic form $\vartheta_I = \omega_I + i\omega_K$.
</div>

<div class="proof">
It remains to show that the fibers are Lagrangian. Fix $1 \le k \le r$ and pick $a \in \Omega^{0,1}(\Sigma, K^{\otimes(1-k)})$. Define

$$
f(\bar{\partial},\psi) = \int_\Sigma \operatorname{tr}(\psi^k) \wedge a : T^\ast \mathscr{A} \to \Bbb C.
$$

Then

$$
\begin{align*}
df_a(\alpha,\beta) &= \int_\Sigma \operatorname{tr}(\dot{\psi} \wedge \psi^{k-1}) \wedge a \\
&= i \int_\Sigma \operatorname{tr}(\dot{\psi} \wedge (-ia)\wedge \psi^{k-1}) \\
&= \vartheta_I((-ia\psi^{k-1}, 0), (\alpha,\beta)),
\end{align*}
$$

where we have taken a curve $\gamma$ with $\dot{\gamma}(0) = (\alpha,\beta)$ to compute the differential. It follows that the Hamiltonian vector field of $df_a$ is $(-ia\psi^{k-1},0)$ which are all tangent to the fibers since the second component, which is the component in $T\mathcal{B}$ vanishes. For this reason all the $f_a$ Poisson commute with varying $a$, also after descending to the quotient $\mathcal{M}_H(r,d)$. We can pick sufficiently many $a_i$ such that $\{df_{a_i}\}$ span $T^\ast\mathcal{B}$ due to the non-degenerate pairing between $H^{0,1}(\Sigma, K^{\otimes (1-k)})$ and $H^0(\Sigma, K^{\otimes k})$. By the non-degeneracy of $\Omega_I$, the corresponding Hamiltonian vector field span the tangent space to the fiber, which leads one to conclude that $\Phi_I\vert_{f^{-1}(b)} = 0$ for all $b \in \mathcal{B}$.

</div>

Now, the fact that the Lagrangian fibres are holomorphically embedded w.r.t.to the complex structure I means that they are calibrated by $\omega_I$. This means that these fibers are volume-minimizing with respect to the Kähler form $\omega_I$ and that they are special submanifolds that are in some sense "optimal" or "canonical" within the geometry of the moduli space. The fact that they are Lagrangian w.r.t. $\vartheta_I$ means that, for each fibre $f^{-1}(b) = L_b$, we have 

$$
\omega_J \vert_{L_b} = \omega_K\vert_{L_b} = 0.
$$

This yields the following.

<div class="corollary">
The Hitchin map $f : \mathcal{M}_H(r,d) \to \mathcal{B}$ is a special Lagrangian fibration for the Calabi-Yau manifold $(M_H(r,d), \omega_K, \Omega_K = (\omega_I + i\omega_J)^{n/2})$, where $n = \dim_\Bbb C \mathcal{M}_H(r,d)$.
</div>

A natural question to pose is what kind of interpretation do the complex structures $J$ and $K$ have on $\mathcal{M}\_H(r,d)$ have, if any? Fortunately for us, these has a very nice geometric interpretation. Recall that $J$ acts by $J(\alpha,\beta) = (-\beta,\alpha)$. This corresponds to multiplying $\alpha + i \beta$ via $i$, so the space $(T^\ast\mathscr{A}, J)$ consists of all complex connections on $E$, not unitary ones. We can split a complex connection $\nabla$ into its unitary and self-adjoint part, writing $\nabla = D + i\Phi$. Then $\mathscr{G}_\Bbb C$ acts by complex gauge transformations on the space of complex connections. Its momentum map is given by

$$
\mu(D,\Phi) = \mu_3 + i\mu_1 = D\Phi + i(-F_D + \Phi \wedge \Phi - 2\pi i \mu(E)\omega).
$$

The space $\mu^{-1}(0)$ consists of those complex connections satisfying $F_D + i D\Phi - \Phi \wedge \Phi = F_\nabla = -2\pi i \mu(E)\omega$. In other words, those complex connections with constant central curvature. We consider the case with $d = 0$, meaning we obtain the space of flat complex connections. In other words, $(M_H(r,0),J)$ is the moduli space of flat connections on $E$. Its topology and smooth structure comes from infinite dimensional symplectic reduction. Denote this moduli space by $\mathcal{M}_{dR}(r,d)$ and recall that a flat  connection on $E$ corresponds to a representation 

$$
\rho : \pi_1(\Sigma) \to \mathrm{GL}(r,\Bbb C).
$$

Connections are gauge equivalent if and only if the representations are conjugate. Associated to the general linear group is its representation variety, which is an affine variety. Using geometric invariant theory, one can look at the moduli space of these representations (i.e. the conjugacy classes of representations) which is an affine algebraic variety associated to a ring of invariant polynomials. After endowing it with the analytic topology instead of the Zariski topology, we get a non-compact algebraic complex manifold denoted $\mathcal{M}_B(r,0)$. Now its not clear whether or not $\mathcal{M}_{dR}(r,0)$ and $\mathcal{M}_B(r,0)$ are diffeomorphic, since their constructions are very different. All we know is that there is a natural bijection between them, which may or may not preserve the possibly very distinct topologies and smooth structures.

<div class="theorem" text="(Non-abelian Hodge Correspondence)">
Let $X$ be a projective Kähler manifold. Then there are diffeomorphisms

$$
\mathcal{M}_H(r,d) \cong \mathcal{M}_{dR}(r,d) \cong \mathcal{M}_B(r,d).
$$

</div>

The Riemann-Hilbert correspondence gives an analytic isomorphism $\mathcal{M}_{dR}(r,d) \cong \mathcal{M}_B(r,d)$, but we are not dealing with projective manifolds now, so analytic isomorphisms are not necessarily algebraic, and indeed, this isomorphism is not an algebraic one. In conclusion we have a non-compact hyper-Kähler manifold $(M_H(r,d),g)$ for which

$$
(M_H(r,d),g,I) \cong \mathcal{M}_H(r,d)
$$ 

and

$$
(M_H(r,d),g,J) \cong \mathcal{M}_{dR}(r,d) \cong \mathcal{M}_B(r,d),
$$

but the final isomorphism is only complex analytic, and not algebraic. We have outlined the intuition for the case when $X = \Sigma$ is a Riemann surface, but remarkably this theorem holds much more generally. Of course, one has to impose the additional condition $\Phi \wedge \Phi = 0$ on the Higgs field in higher dimensions.

Before moving onto the next topic, let's quickly consider the moduli spaces of $G_\Bbb C$-Higgs bundles for any complex reductive algebraic group $G_\Bbb C$.  In this case, the Higgs field becomes a holomorphic section 

$$
\Phi \in H^0(\Sigma, \operatorname{Ad}(E) \otimes K_\Sigma),
$$

and the topological type is fixed by an element $d \in \pi_1(G_\Bbb C)$. The resulting constructions are highly analogous and can be found in Hitchin’s original paper. We denote the respective moduli spaces by $\mathcal{M}\_H(G_{\Bbb C},d)$. For a complex reductive algebraic group $G_\Bbb C$, we can consider the root datum $(\Gamma^\ast, \Delta, \Gamma_\ast, \Delta^\lor)$, where $\Gamma^\ast$ is the lattice of characters of a maximal torus, $\Gamma_\ast$ the dual lattice, $\Delta$ the roots of the Lie algebra and $\Delta^\lor$ the coroots. There is an involution on the set of complex reductive algebraic groups, defined by

$$
(\Gamma^\ast, \Delta, \Gamma_\ast, \Delta^\lor) \to (\Gamma_\ast, \Delta^\lor, \Gamma^\ast, \Delta)
$$

and the image of a group $G_\Bbb C$ under this involution is called its <i>Langlands dual</i>, denoted by $G^{\lor}_{\Bbb C}$.

<div class="example">
Some examples of Langlands duals are given by the following:
<ol>
    <li>
    $\mathrm{GL}(r,\Bbb C)^{\lor} = \mathrm{GL}(r,\Bbb C)$.
    </li>
    <li>
    $\mathrm{SL}(r,\Bbb C)^{\lor} = \mathrm{PGL}(r,\Bbb C)$.
    </li>
    <li>
    $\mathrm{SO}(2n+1,\Bbb C)^{\lor} = \mathrm{Sp}(2n,\Bbb C)$.
    </li>
    <li>
    $\mathrm{SO}(2n,\Bbb C)^{\lor} = \mathrm{SO}(2n,\Bbb C)$.
    </li>
</ol>
</div>

<div class="theorem">
Let $G_\Bbb C$ be a complex reductive algebraic group and $G^{\lor}_{\Bbb C}$ its Langlands dual. Let $f : \mathcal{M}_{dR}(G_\Bbb C, d) \to B$ and $f^\lor : \mathcal{M}_{dR}(G^{\lor}_\Bbb C, d) \to B^\lor$ be the respective special Lagrangian fibrations obtained from the Hitchin system, for some Riemann surface. Then $B = B^\lor$ and the fibrations are an SYZ mirror pair.
</div>

The Langlands dual group of GL(r,C) is itself, which means the corresponding special Lagrangian fibration is mirror to itself. Recall also that we have a complex analytic isomorphism $\mathcal{M}\_{dR}(r,d) \cong \mathcal{M}\_B(r,d)$, so $\mathcal{M}\_B(r,d)$ is mirror to $\mathcal{M}\_{dR}(r,d)$. The question is: can the Betti moduli space "see" the special Lagrangian fibration of the de Rham moduli space in some way? The $P = W$ conjecture claims that it can, through a certain filtration on its cohomology which we explore next.

---

We'll now look at the so-called $P = W$ phenomenom. Every complex algebraic variety comes equipped with its weight filtration, which is an
abstraction of the Hodge decomposition on $H^\bullet(X,\Bbb Q)$ that also works for for non-projective varieties. In particular, the Betti moduli space has a canonical weight filtration associated to it, denote it by 

$$
W_\bullet(H^\bullet(M_B(r,d),\Bbb Q)).
$$

I'll define this properly shortly. The special Lagrangian fibration $\mathcal{M}\_{dR}(r,d) \to B$ also induces a filtration on cohomology, through something called the perverse filtration. This is a filtration which can be associated to a proper morphism between irreducible smooth quasi-projective varieties. We can hyperKähler rotate our special Lagrangian fibration to return to the Hitchin map, which satisfies these conditions. As such, we get a filtration

$$
P_\bullet(H^\bullet(M_{H}(r,d),\Bbb Q)).
$$

Again, I'll define this precisely in a moment. 

<div class="conjecture">
Under $M_H(r,d) = M_{dR}(r,d) \cong M_B(r,d)$, we have
$$
P_k(H^m(M_H(r,d),\Bbb Q)) = W_{2k}(H^m(M_B(r,d), \Bbb Q)) = W_{2k+1}(H^m(M_B(r,d),\Bbb Q)).
$$
</div>

One can really think of this as a refined version of topological mirror symmetry (i.e. at the level of Hodge numbers) for non-projective varieties. The $P = W$ conjecture has been shown to hold for $G = \mathrm{GL}(r,\Bbb C)$. Other structure groups and their Langlands duals give rise to a similar statement, as was addressed in the original paper, where they prove their conjecture for certain low rank groups and their duals.  In [15], it was observed that the $P = W$ phenomenon holds for the Higgs and Betti moduli spaces associated to abelian varieties of any dimension. This is the example that we will investigate
further, as it allows for some explicit computations.

To treat these examples, we need to familiarise ourselves with the respective cohomology filtrations, starting with Deligne’s weight filtration.

<div class="definition">
A pure <i>Hodge structure</i> of weight $k$ is an abelian group $H_\Bbb Z$ of finite rank, together with a filtration
$$
H_\Bbb Z \otimes \Bbb C = F^0 \supset F^1 \supset \dots \supset F^{k+1} = 0
$$
such that $F^p \cap \overline{F^q} = 0$ and $F^p \oplus \overline{F^q} = H_\Bbb Z \otimes \Bbb C$ for all $p+q = k+1$.
</div>

<div class="example">
Let $X$ be a Kähler manifold and consider $H_\Bbb Z = H^k(X,\Bbb Z)$ and $F^p = \bigoplus_{i\ge p} H^{i,k-1}$. This yields a pure Hodge structure of weight $k$.
</div>

<div class="theorem" text="(Deligne)">
Let $X$ be a quasi-projective variety. Then every cohomology group $H^m(X,\Bbb Q)$ carries a natural weight filtration
$$
0 = W_{-1}(H^m(X,\Bbb Q)) \subset W_0(H^m(X,\Bbb Q)) \subset \dots \subset W_{2m}(H^m(X,\Bbb Q)) = H^m(X,\Bbb Q)
$$
and a Hodge filtration
$$
H^m(X,\Bbb C) = F^0H^m(X,\Bbb C) \supset \dots \supset F^mH^m(X,\Bbb C) \supset F^{m+1}H^m(X,\Bbb C) = 0
$$
such that the sub-quotients $\operatorname{Gr}^W_k = W_kH^m(X,\Bbb C)/W_{k-1}H^m(X,\Bbb C)$ carry a pure Hodge structure of weight $k$ induced by $F^\bullet$.
</div>

The obtained Hodge structure in the above theorem is called a <i>mixed Hodge structure</i>. It satisfies the following properties:
<ol>
    <li>
    If $X$ is projective and smooth, then 
    $$
    0 = W_{m-1}H^m(X,\Bbb Q) \subset W_mH^m(X,\Bbb Q) = H^m(X,\Bbb Q).
    $$
    </li>
    <li>
    If $X$ is smooth (not necessarily projective) then 
    $$
    0 = W_{-1}H^m(X,\Bbb Q) \subset \dots \subset W_{2m}H^m(X,\Bbb Q) = H^m(X,\Bbb Q)
    $$
    and for any smooth compactification $\iota : X \to \widetilde{X}$ one has
    $$
    W_mH^m(X,\Bbb Q) = \iota^\ast H^m(\widetilde{X}, \Bbb Q).
    $$
    </li>
    <li>
    For any algebraic map $f : X \to Y$, one has
    $$
    f^\ast(W_kH^m(Y,\Bbb Q)) = W_kH^m(X,\Bbb Q).
    $$
    </li>
    <li>
    The weight filtration is compatible with the cup product.
    </li>
    <li>
    The weight filtration is compatible with the Künneth formula.
    </li>
</ol>

The theorem above is rather lengthy, but it mostly just expresses the naturality of the weight filtration with respect to natural operations such as compactifications, pullback, products, etc. The weight filtration of Deligne’s theorem will be denoted by $W_\bullet H^\bullet(X,\Bbb Q)$.

<div class="example">
Let $X = \Bbb C^\times$. There is a smooth compactification $\iota : X \to \Bbb P^1$ and $H^1(\Bbb P^1,\Bbb Q) = 0$. The second property of the above list yields $$
W_1H^1(X,\Bbb Q) = 0.
$$
In this instance, this is sufficient to determine the entire weight filtration of $X$. Since $\mathbb{C}^\times$ is smooth and quasi-projective, Deligne’s theorem applies. The weight filtration $W_\bullet H^\bullet(\mathbb{C}^\times, \mathbb{Q})$ must satisfy:

$$
0 = W_{-1}H^1(\mathbb{C}^\times, \mathbb{Q}) \subset W_0H^1(\mathbb{C}^\times, \mathbb{Q}) \subset W_1H^1(\mathbb{C}^\times, \mathbb{Q}) \subset W_2H^1(\mathbb{C}^\times, \mathbb{Q}) = H^1(\mathbb{C}^\times, \mathbb{Q}).
$$
We obtain 
$$
W_0H^1(\mathbb{C}^\times, \mathbb{Q}) = 0, \quad W_1H^1(\mathbb{C}^\times, \mathbb{Q}) = 0, \quad W_2H^1(\mathbb{C}^\times, \mathbb{Q}) = H^1(\mathbb{C}^\times, \mathbb{Q}) \cong \mathbb{Q}.
$$
Using this and the Künneth formula, one can now compute the weight filtrarion for $\mathcal{M}_B(1,0) = (\Bbb C^\times)^{2n}$.
</div>

We set $H^{k,p,q}(X) := \operatorname{Gr}^p_F \operatorname{Gr}^W_{p+q}H^k(X,\Bbb C)$ and state the following definition fo the so-called Deligne-Hodge numbers.

<div class="definition">
The Deligne-Hodge numbers are $h^{k,p,q}(X) = \dim_\Bbb C H^{k,p,q}(X)$. The Deligne-Hodge polynomial is defined as

$$
\mathfrak{W}_X(t,u,v) = \sum_{k,p,q\ge 0} h^{k,p,q}(X)t^ku^pv^q.
$$

</div>

The Deligne-Hodge polynomial can be treated as a refinement of the Hodge numbers of a compact Kähler manifold, which satisfies additional convenient properties and relations. For example, it follows from Deligne’s theorem that the polynomials are multiplicative with respect to Cartesian products. Evidently we have $\mathfrak{W}_{\mathcal{M}_H} \ne \mathfrak{W}_{\mathcal{M}_B}$ in spite of the diffeomorphism between the two spaces. Instead, the $P = W$ conjecture says that the perverse filtration of $\mathcal{M}_H$ should coincide with the weight filtration of $\mathcal{M}_B$, so let us see how this perverse filtration is defined.

<div class="definition">
Let $Y$ be a quasi-projective variety equipped with a flag $Y_0 \subset \dots \subset Y_d = Y$, and let $f : X \to Y$ be a morphism of varieties. The the perverse filtration $P_\bullet$ on $H^\bullet(X,\Bbb Q)$ is defined by
$$
P_{m-k-1}H^m(X,\Bbb Q) = \ker(H^m(X,\Bbb Q) \to H^m(f^{-1}(Y_k), \Bbb Q)).
$$
</div>

<div class="definition">
Let $P_\bullet H^\bullet(X,\Bbb Q)$ be a perverse filtration. Then the perverse Hodge numbers $h^{p,q}_{\mathfrak{P}}(X)$ are defined as
$$
h^{p,q}_{\mathfrak{P}}(X) = \dim_{\Bbb Q} \operatorname{Gr}^P_p H^q(X,\Bbb Q) = \dim_\Bbb Q P_pH^q(X,\Bbb Q)/P_{p-1}H^q(X,\Bbb Q).
$$
</div>

We're interested in seeing whether or not

$$
h^{p,q}_{\mathfrak{P}}(\mathcal{M}_H(r,0)) = h^{p,q}(\mathcal{M}_B(r,0)).
$$

Let $X$ be an abelian variety. We have the Hitchin map $f : \mathcal{M}_H(r,0) \cong \operatorname{Sym}^r(X \times \Bbb C^n) \to \Bbb C^{rn}$. So let's begin with $r = 1$ which gives the projection $f : X \times \Bbb C^n \to \Bbb C^{n}$. Homotopy invariance of cohomology gives

$$
P_kH^\bullet(X\times \Bbb C^n, \Bbb Q) \cong P_kH^\bullet(X, \Bbb Q)
$$

So the perverse filtration on $\mathcal{M}_H$ is induced by the constant map $c : X \to \{\ast\}$. It follows from the definition that

$$
P_kH^m(M_H, \Bbb Q) = P_kH^m(X,\Bbb Q) = H^m(X,\Bbb Q)
$$

if $k \ge m$ and $0$ if $k < m$. Equivalently

$$
P_kH^\bullet(M_H,\Bbb Q) = \bigoplus_{j=0}^k \wedge^j \Bbb Q^{2n}
$$

which shows that $P = W$ holds for $X$ and $r = 1$. To find $h^{p,q}_{\mathfrak{P}}(\mathcal{M}_H)$ we need the dimension of

$$
P_pH^{p+q}(M_H, \Bbb Q)/P_{p-1}H^{p+q}H^{p+q}(M_H, \Bbb Q).
$$
 
Fix $p,q \in \Bbb N$ and let $k = p+q$. From the description of the perverse filtration we see that this quotient is non-trivial if and only if $H^k(X,\Bbb Q) \ne 0$ and $p = k$, in which case it is $H^p(X,\Bbb Q)$. We conclude that 

$$
h^{p,q}_{\mathfrak{P}}(\mathcal{M}_H) = b_p(X)
$$

if $p = q$ and $0$ else. It follows that $\mathfrak{W}\_{\mathcal{B}}(1,u,v) = \mathfrak{P}\_{\mathcal{M}\_H}(uv,v)$, where

$$
\mathfrak{P}_{\mathcal{M}_H}(u,v) = \sum_{p,q} h^{p,q}_{\mathcal{P}}(\mathcal{M}_H)u^pv^q = (1+uv)^{2n}.
$$


<div class="theorem">
Let $X$ be an abelian variety and let $\mathcal{M}_H(r,0)$ and $\mathcal{M}_B(r,0)$ be the Higgs
moduli space and the Betti moduli space, respectively. Then 
$$
h^{p,q}_{\mathfrak{P}}(\mathcal{M}_H(r,0)) = h^{p,q}(\mathcal{M}_B(r,0)).
$$
</div>