---
layout: post
title: "Derived Torelli Theorem for K3 Surfaces"
categories: [Complex Geometry, Algebraic Geometry, Category Theory]
mathjax: true
published: true
excerpt_separator: <!--more-->
---

We've been discussing derived categories and Fourier-Mukai transformations lately. This time, we'll be focusing on $K3$ surfaces. Alongside two-dimensional compact complex tori, $K3$ surfaces represent the two-dimensional Calabi–Yau manifolds, which are also hyperkähler manifolds. These surfaces occupy a central role in the classification of algebraic surfaces, positioned between the positively curved Fano surfaces, which are relatively straightforward to classify, and the negatively curved surfaces of general type, which are largely resistant to classification.

<!--more-->

---

We'll begin by recalling some basic facts about $K3$ surfaces.

<div class="definition">
A $K3$ surface is a compact complex surface $X$ with trivial canonical bundle, i.e. $\omega_X \cong \mathcal{O}_X$ and $H^1(X, \mathcal{O}_X) = 0$.
</div>

The simplest example of a $K3$ surface is given by the Fermat quartic

$$
x^4 + y^4 + z^4 + w^4 = 0
$$

in $\Bbb P^3$. An important result due to Siu is that every $K3$ surface $X$ admits a Kähler metric. Since the canonical bundle of $X$ is trivial, $c_1(X) = 0$, and hence Yau's solution to the Calabi conjecture implies that every $K3$ surface is Calabi-Yau.

It's important to note here that there are two different flavors of $K3$ surfaces, algebraic and complex. I won't be making much distinction between these two since the famous GAGA principle of Serre states that for any scheme of finite type over the complex numbers, we can associate a complex space $X^{\mathrm{an}}$ whose set of points is given by the closed points of $X$. This association carries on also to coherent sheaves over $X$ and if $X$ is projective one obtains an equivalence between $\textbf{Coh}(X)$ and $\textbf{Coh}(X^{\mathrm{an}})$. These give the following:

<div class="proposition">
If $X$ is an algebraic $K3$ surface over $\Bbb C$, then the associated complex space $X^{\mathrm{an}}$ is a complex $K3$ surface.
</div>

Now $c_1(X) = 0$, but what about higher degree Chern classes? The Hirzebruch–Riemann–Roch gives us $c_2(X)$ as well as the Hodge numbers[^1]

$$
h^{p,q}(X) := \dim H^q(X,\Omega^p_X).
$$

Recall that if $\mathcal{F}$ is a coherent sheaf of $\mathcal{O}_X$-modules on $X$, the Hirzebruch–Riemann–Roch formula states

$$
\chi(X,\mathcal{F}) = \int \operatorname{ch}(\mathcal{F})\operatorname{td}(X) = \operatorname{ch}_2(\mathcal{F}) + 2\operatorname{rk}(\mathcal{F}).
$$

If $\mathcal{F} = \mathcal{O}_X$, then one obtains Noether's formula

$$
\chi(X,\mathcal{O}_X) = \frac{1}{12}(c^2_1(X) + c_2(X)) = \frac{c_2(X)}{12}.
$$

Now $\chi(X,\mathcal{O}_X) = \sum_i (-1)^i \dim H^i(X,\mathcal{O}_X) = 1 - 0 + 1 = 2$ since $H^0(X,\mathcal{O}_X) \cong \Bbb C$ by Liouville’s theorem, $H^1(X,\mathcal{O}_X) = 0$ by definition and 

$$
\begin{align*}
H^2(X,\mathcal{O}_X) &\cong H^0(X,\mathcal{O}_X^\ast \otimes \omega_X)^\ast \\
&= H^0(X,\mathcal{O}_X^\ast \otimes \mathcal{O}_X)^\ast \\
&= H^0(X,\mathcal{O}_X^\ast)^\ast \\
& \cong \Bbb C
\end{align*}
$$

by Serre duality. Therefore 

$$
c_2(X) = 24.
$$

Recall now from <a href="https://anthonymakela.com/differential%20geometry/2024/01/11/chern-classes.html" style="color:#680530; text-decoration: underline;">Chern Classes</a> that the top degree Chern class is given by the Euler class and hence

$$
e(X) = \sum_i (-1)^ib_i(X) = b_0(X) - b_1(X) + b_2(X) - b_3(X) + b_4(X) = 24.
$$

The exponential sequence

$$
0 \longrightarrow \Bbb Z \longrightarrow \mathcal{O}_X \longrightarrow \mathcal{O}^\ast_X \longrightarrow 0
$$

induces

$$
0 \longrightarrow H^1(X,\Bbb Z) \longrightarrow H^1(X,\mathcal{O}_X),
$$

but $H^1(X,\mathcal{O}_X) = 0$ and so $ H^1(X,\Bbb Z) = 0$ also. This yields $b_1(X) = 0$ and Poincaré duality furthermore gives $b_3(X) = 0$. All in all, we have

$$
b_0(X) = b_4(X) = 1, b_1(X) = b_3(X) = 0,
$$

and $b_2(X) = 22$. Thus $b_2(X) = h^{2,0} + h^{1,1} + h^{0,2} = 22 \implies h^{1,1} = 20$. The Hodge diamond of a $K3$ surface thus reads

$$
\begin{array}{ccccccc}
 & & & 1 & & & \\
 & & 0 & & 0 & & \\
 & 1 & & 20 & & 1 & \\
 & & 0 & & 0 & & \\
 & & & 1 & & & \\
\end{array}
$$

A very neat theorem is that all complex $K3$ surfaces turn out to be deformation equivalent, hence diffeomorphic. This means that we only need to study the simple $K3$ surfaces to understand the behavior of all of them.

An important structure on the cohomology of a $K3$ surface is given by its weight $2$ Hodge structure

$$
H^2(X,\Bbb C) = H^{2,0}(X) \oplus H^{1,1}(X) \oplus H^{0,2}(X).
$$

As $h^{2,0} = h^{0,2} = 1$ and $H^1(X,\mathcal{O}_X) = 0$, the map

$$
c_1 : \operatorname{Pic}(X) \to H^{1,1}(X) \cap H^{2}(X,\Bbb Z)
$$

is injective. This follows from the long exact sequence

$$
H^{1}(X,\mathcal{O}_X) \longrightarrow H^{1}(X,\mathcal{O}^\ast_X) \longrightarrow H^{2}(X,\Bbb Z)  \longrightarrow H^{2}(X,\mathcal{O}_X),
$$

obtained from the exponential sequence

$$
0 \longrightarrow \Bbb Z \longrightarrow \mathcal{O}_X \longrightarrow \mathcal{O}^\ast_X \longrightarrow 0.
$$

Since $b_2(X) = 22$, we obtain an upper bound for the Picard number

$$
\operatorname{rk}(\operatorname{Pic}(X)) \le 20.
$$

The single most important theorem for $K3$ surfaces is the global Torelli theorem. Before we state this, let's recall what is meant by an Hodge isometry.

<div class="definition">
A <i>Hodge isometry</i> between two complex $K3$ surfaces $X$ and $Y$ is a group isomorphism

$$
\varphi : H^2(X,\Bbb Z) \to H^2(Y,\Bbb Z)
$$

such that

<ol>
    <li>
 The intersection product is preserved: $(\varphi(\alpha),\varphi(\beta)) = (\alpha,\beta)$ for every $\alpha,\beta \in H^2(X,\Bbb Z)$.
    </li>
    <li>
 $\varphi$ sends holomorphic sections of $\omega_X$ to $\omega_Y$. That is $\varphi(H^{2,0}(X)) \subset H^{2,0}(Y)$ as $H^{2,0}(-) \cong H^{0}(-,\omega_{-})$.
    </li>
</ol>

</div>

<div class="theorem" text="(Global Torelli)">
Let $X$ and $Y$ be two complex $K3$ surfaces. Then $X$ and $Y$ are isomorphic as complex varieties if and only if there is a Hodge isometry

$$
\varphi : H^2(X,\Bbb Z) \to H^2(Y,\Bbb Z).
$$

Moreover, if $\varphi$ maps at least one Kähler class of $X$ to a Kähler class of $Y$, then there is a unique isomorphism 

$$
f : X \to Y
$$

such that $f_\ast = \varphi$.

</div>

The <i>period</i> of a $K3$ surface $X$ is by definition the natural weight-two Hodge structure on $H^2(X,\Bbb Z)$. Thus the above theorem states that two $K3$ surfaces are isomorphic if and only if their periods are isomorphic.

---

Let's now turn to the derived viewpoint.

<div class="proposition">
Let $X$ be an algebraic $K3$ surface over $\Bbb C$ and $Y$ a smooth projective variety over $\Bbb C$. If there exists an equivalence

$$
F : D^b(X) \to D^b(Y),
$$

then $Y$ is an algebraic $K3$ surface.
</div>

<div class="proof">
Since $F$ is an exact equivalence of categories, we have $\omega_Y \cong \mathcal{O}_Y$. As $\Omega^2_X \cong \mathcal{O}_X$ and $\Omega^2_Y \cong \mathcal{O}_Y$ the Hodge decomposition yields
$$
h^{1,2}(X) = h^{2,1}(X) = h^{0,1}(X)
$$ 
and
$$
h^{1,2}(Y) = h^{2,1}(Y) = h^{0,1}(Y).
$$ 
Recall now from <a href="https://anthonymakela.com/category%20theory/2024/08/01/the-derived-category-of-coherent-sheaves.html" style="color:#680530; text-decoration: underline;">The Derived Category of Coherent Sheaves and Fourier-Mukai Theory</a> that Orlov's representability theorem gives the existence for an object $\mathcal{E} \in D^b(X \times Y)$ unique up to isomorphism, such that
$$
F \cong \Phi_{\mathcal{E}}.
$$
Now $\Phi_{\mathcal{E}}$ induces a cohomological Fourier-Mukai transform $\Phi^H_{\mathcal{E}} : H^\ast(X,\Bbb Q) \to H^\ast(Y,\Bbb Q)$ which yields isomorphisms
$$
\bigoplus_{p-q=k}H^{p,q}(X) \cong \bigoplus_{p-q=k}H^{p,q}(Y), 
$$
for every $k = -\dim(X),\dots,0,\dots,\dim(X)$. When $k = -1$ we obtain an isomorphism
$$
H^{0,1}(X) \oplus H^{1,2}(X) \to H^{0,1}(Y) \oplus H^{1,2}(Y).
$$
As $X$ is a $K3$ surface we have
$$
\begin{align*}
h^1(Y,\mathcal{O}_Y) &= h^{0,1}(Y) \\
&= \frac{1}{2}(h^{0,1}(Y) + h^{1,2}(Y)) \\
&= \frac{1}{2}(h^{0,1}(X) + h^{1,2}(X)) \\
&= h^{0,1}(X) \\
&= h^{0,1}(X,\mathcal{O}_X) \\
&= 0
\end{align*}
$$
and the result follows.
</div>

To derive a cohomological criterion that decides when two $K3$ surfaces have equivalent derived categories we need to go over some basic constructions introduced by Mukai. Recall that for $\mathcal{E}^\bullet \in D^b(X)$, the <i>Mukai vector</i> is defined by

$$
v(\mathcal{E}^\bullet) := \operatorname{ch}(\mathcal{E}^\bullet)\sqrt{\operatorname{td}(X)}.
$$

<div class="lemma">
Let $X$ and $Y$ be two $K3$ surfaces. Then the Mukai vector $v(\mathcal{E}^\bullet)$ of an object $\mathcal{E}^\bullet \in D^b(X \times Y)$ is an integral cohomology class in $H^\ast(X\times Y, \Bbb Z)$.
</div>

Also for an equivalence $\Phi_{\mathcal{E}} : D^b(X) \to D^b(Y)$, the induced map $\Phi^H_{\mathcal{E}}$ on cohomology is an isometry with respect to the <i>Mukai pairing</i> given by

$$
\langle v, v'\rangle_X := \int_X \exp\left(\frac{1}{2}c_1(X)\right) \cdot (v^\lor \cdot v'),
$$

where for $v = \sum_j v_j \in \bigoplus_j H^j(X,\Bbb C)$, the dual $v^\lor$ is defined by $\sum_j \left(\sqrt{-1}\right)^j v_j \in  \bigoplus_j H^j(X,\Bbb C)$. Mukai then introduced a weight $2$ Hodge structure on $H^\ast(X,\Bbb Z)$ by declaring $H^{0}(X,\Bbb C) \oplus H^4(X,\Bbb C)$ to be of type $(1,1)$ and by keeping the standard Hodge structure on $H^2(X,\Bbb C)$. More concretely,

$$
\begin{align*}
\widetilde{H}^{1,1}(X) &:= H^0(X,\Bbb C) \oplus H^{4}(X,\Bbb C) \oplus H^{1,1}(X), \\
\widetilde{H}^{2,0}(X) &= H^{2,0}(X) \ \text{ and } \ \widetilde{H}^{0,2}(X) = H^{2,0}(X).
\end{align*}
$$

In what follows, $\widetilde{H}(X,\Bbb Z)$ denotes $H^\ast(X,\Bbb Z)$ coupled with the Mukai pairing and this weight $2$ Hodge structure.

<div class="definition">
Let $X$ and $Y$ be $K3$ surfaces over $\Bbb C$. With the weight $2$ Hodge structure on $\widetilde{H}(-,\Bbb Z)$, a Hodge isometry of two $K3$ surfaces $X$ and $Y$ is a group homomorphism
$$
\varphi : \widetilde{H}(X,\Bbb Z) \to \widetilde{H}(Y,\Bbb Z)
$$
such that
<ol>
    <li>
 The Mukai pairing is preserved: $\langle(\varphi(\alpha),\varphi(\beta)\rangle_X = \langle \alpha,\beta\rangle_X$ for every $\alpha,\beta \in H^2(X,\Bbb Z)$.
    </li>
    <li>
 $\varphi\left(H^{2,0}(X)\right) \subset H^{2,0}(Y)$.
    </li>
</ol>
</div>

Note that $\varphi$ preserves the new weight $2$ Hodge structure as $H^{4}(X,\Bbb C) \cong \Bbb C$.

<div class="theorem" text="(Mukai)">
Let $X$ be a complex $K3$ surface, $Y$ a smooth complex projective variety and $\mathcal{E}^\bullet \in D^b(X \times Y)$. If
$$
\Phi_{\mathcal{E}^\bullet} : D^b(X) \to D^b(Y)
$$
is an equivalence, the induced cohomological Fourier-Mukai transform defines a Hodge isometry
$$
\Phi^H_{\mathcal{E}^\bullet} : \widetilde{H}(X,\Bbb Z) \to \widetilde{H}(Y,\Bbb Z).
$$
</div>

<div class="proof">
By our previous proposition, $Y$ obtains the structure of a complex $K3$ surface also. The induced cohomological Fourier-Mukai transform is given by
$$
\alpha \mapsto p_{Y\ast}(v(\mathcal{E}^\bullet) \cdot p^\ast_X(\alpha))
$$
and is an isometry with respect to the Mukai pairing. Now by the previous lemma, $\Phi^H_{\mathcal{E}^\bullet}(\alpha) \in H^\ast(Y,\Bbb Z)$, for every $\alpha \in H^\ast(X,\Bbb Z)$. Since the quasi-inverse of $\Phi_{\mathcal{E}^\bullet}$ is also a Fourier-Mukai functor, applying the same argument for it shows that that the induced map
$$
\Phi^H_{\mathcal{E}^\bullet} : \widetilde{H}(X,\Bbb Z) \to \widetilde{H}(Y,\Bbb Z)
$$
is indeed an isomorphism. To conclude that $\Phi^H_{\mathcal{E}^\bullet}$ is a Hodge isometry, note that its $\Bbb C$-linear extension sends $H^{2,0}(X)$ to $H^{2,0}(Y)$.
</div>

<div class="theorem" text="(Derived Torelli Theorem)">
Let $X$ and $Y$ be two $K3$ surfaces over $\Bbb C$. Then $X$ and $Y$ are derived equivalent if and only if there exists a Hodge isometry
$$
\widetilde{H}(X,\Bbb Z) \to \widetilde{H}(Y,\Bbb Z).
$$
</div>

<div class="proof">
Since any exact equivalence $D^b(X) \to D^b(Y)$ is isomorphic to a Fourier-Mukai functor by Orlov’s representability theorem, the above theorem reduces the proof to show that the existence of a Hodge isometry $\widetilde{H}(X,\Bbb Z) \to \widetilde{H}(Y,\Bbb Z)$ implies an exact equivalence of derived categories $D^b(X) \to D^b(Y)$. Suppose that there exists a Hodge isometry $\widetilde{H}(X,\Bbb Z) \to \widetilde{H}(Y,\Bbb Z)$. If $\varphi(0,0,1) = \pm(0,0,1)$, then $\varphi$ respects the intersection product on $H^2(-,\Bbb Z)$ and sends $H^{2,0}(X)$ to $H^{2,0}(Y)$, thus yielding a Hodge isometry. The Global Torelli Theorem now gives an exact equivalence $D^b(X) \to D^b(Y)$. If $\varphi(0,0,1) = (r,\ell,s) =: v$ with $r$ non-zero, then replacing $\varphi$ with $-\varphi$, if needed, we may assume $r < 0$ or $r > 0$ depending on whether we want to work with the classical or general Mukai pairing. If $v' := \varphi(-1,0,0)$, then
$$
\langle v,v\rangle = 0 \ \text{ and } \ \langle v, v'\rangle = 1.
$$
The idea is to now apply the following general fact from the theory of moduli spaces of bundles over $K3$ surfaces: If $Y$ is a $K3$ surface and $v,v' \in \widetilde{H}^{1,1}(Y,\Bbb Z)$ with $\langle v,v\rangle = 0$ and $\langle v,v'\rangle = 1$, then there exists another $K3$ surface $Z$ and a sheaf $\mathcal{F}$ on $Y \times Z$ such that for each closed point $z \in Z$, the Mukai vector of the sheaf $\mathcal{F}_{Y \times \{z\}}$ on $Y \times \{z\} \cong Y$ is $v$, and the integral functor with kernel $\mathcal{F}$ 
$$
\Phi_{\mathcal{F}} : D^b(Y) \to D^b(Z)
$$ 
is an equivalence of categories. Considering then the composite
$$
\psi : \xymatrix{
\widetilde{H}(X,\Bbb Z) \ar@{->}[r]^{\varphi} & \widetilde{H}(Y,\Bbb Z) \ar@{->}[r]^{\Phi^H_{\mathcal{F}}} & \widetilde{H}(Z,\Bbb Z),
}
$$
this satisfies $\psi(0,0,1)=(0,0,1)$. Then using Global Torelli theorem again, one finds an isomorphism of $X$ with $Z$, which gives an exact equivalence $D^b(X) \to D^b(Z)$. Since the inverse $D^b(Z) \to D^b(Y)$ is also an exact equivalence, we obtain an equivalence $D^b(X) \to D^b(Y)$. Finally, suppose that $\varphi(0, 0, 1) = (0,\ell,s) =: v$, with $\ell \ne 0$. Then use a Hodge isometry
$$
\exp(c_1(L))\cdot- : \widetilde{H}(Y,\Bbb Z) \to \widetilde{H}(Y,\Bbb Z),
$$
for some $L \in \operatorname{Pic}(Y)$ to obtain $\exp(c_1(L))(0,\ell,s)=(0,\ell,s+(c_1(L),\ell))$. As $\ell \ne 0$, one can pick choose $L$ such that $s+(c_1(L),\ell) \ne 0$. Hence $(r',\ell',s') := T^H_{\mathcal{O}_Y}(v)$ satisfies $r' \ne 0$. Continuing as in the case before, we conclude the result.
</div>

In the above proof, the last step uses tacitly the fact that the structure sheaf $\mathcal{O}_Y$ on a $K3$ surface $Y$ is a spherical object and thus induces an autoequivalence 

$$
T_{\mathcal{O}_Y} : D^b(Y) \to D^b(Y).
$$

Here $T\_{\mathcal{O}\_Y}$ is defined as the Fourier–Mukai transform whose kernel is the cone of the natural map $\mathcal{O}\_{Y\times Y} \to \mathcal{O}\_{\Delta}$.

---

[^1]: Recall that these are given by $h^{p,q}(X) = \dim H^{p,q}(X)$ and $H^{p,q}(X) \cong H^{q}(X, \Omega^p)$ by the Dolbeault isomorphism.