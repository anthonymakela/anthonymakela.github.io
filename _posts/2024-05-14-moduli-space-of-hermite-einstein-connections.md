---
layout: post
title: "Moduli Space of Hermite-Einstein Connections"
categories: [Complex Geometry, Differential Geometry]
mathjax: true
published: true
excerpt_separator: <!--more-->
---

This is the first of three posts where we will delve into the moduli space of Hermite-Einstein connections. We will start by examining some of the properties of these connections. Next, we will prove that the moduli space of irreducible Hermite-Einstein connections constitutes an open subset of the moduli space of stable bundles. After that, we will demonstrate that the moduli space of Hermite-Einstein connections is a smooth manifold and explore an application of this theory in the context of surfaces. Finally, we will consider the Kobayashi–Hitchin correspondence.

<!--more-->

---

Throughout the trilogy, $M$ denotes a compact, connected Kähler manifold with a Kähler form $\omega$, and $\dim_\Bbb C M \ge 2$ unless stated otherwise. Recall that in complex geometry, we have the three important operators

<ol>
    <li>
    The <b>Lefschetz operator</b> 
    $$
    \begin{align*}
    L : \Omega^k(M) &\to \Omega^{k+2}(M) \\
    \alpha &\mapsto \alpha \wedge \omega.
    \end{align*}
    $$
    </li>
    <li>
    The <b>Hodge $\star$-operator</b>
    $$
    \begin{align*}
    \star : \Omega^k(M) &\to \Omega^{2n-k}(M).
    \end{align*}
    $$
    </li>
    <li>
    The <b>dual Lefschetz operator</b>
    $$
    \begin{align*}
    \Lambda : \Omega^k(M) &\to \Omega^{k-2}(M).
    \end{align*}
    $$
    </li>
</ol>

Also $\frac{\omega^n}{n!}$ serves as the volume form of $M$. This is used implicitly as a measure in order to integrate functions on $M$. Recall from <a href="https://anthonymakela.com/complex%20geometry/differential%20geometry/2024/03/25/hermite-einstein-and-k%C3%A4hler-einstein-metrics.html" style="color:#680530; text-decoration: underline;">Hermite-Einstein Metrics and Stability</a> the definition for a Hermite-Einstein connection.

<div class="definition">
A connection $\nabla$ on a Hermitian vector bundle $(E,h)$ is called <b>Hermite-Einstein</b> if 
$$
i\Lambda_\omega F_\nabla = \lambda\operatorname{id}_E
$$
for some constant $\lambda$.
</div>

Since we've already had discussions about the properties of these kinds of connections in the past, we'll go straight into the properties of bundles admitting such connections.

<div class="proposition">
Let $\nabla$ be a Hermite-Einstein connection on a Hermitian vector bundle $(E,h)$. Then
<ol>
    <li>
    There exists a unique holomorphic structure on $E$ compatible with $\nabla$.
    </li>
    <li>
    If $\deg(E) := \int_M c_1(E) \wedge [\omega]^{n-1} < 0$, then $E$ has no holomorphic sections.
    </li>
    <li>
    $E$ is semi-stable and is a direct sum of stable bundles.
    </li>
    <li>
    $\nabla$ minimizes the Yang-Mills functional
    $$
    \operatorname{YM}(\nabla) = \int_M |F_\nabla|^2.
    $$
    </li>
</ol>
</div>

<div class="proof">
<ol>
    <li>
    This is just an application of the Newlander-Nirenberg theorem.
    </li>
    <li>
    Note that for any holomorphic section $s$ we have that
    $$
    \frac{1}{2}\Delta |s|^2 = h(i\Lambda_\omega F_\nabla(s), s) - |\nabla s|^2.
    $$
    Now the Hermite-Einstein condition gives
    $$
    \frac{1}{2}\Delta |s|^2 = \lambda|s|^2 - |\nabla s|^2.
    $$
    Integrating this equation yields
    $$
    \int_M \frac{1}{2}\Delta |s|^2 = \int_M \lambda|s|^2 - \int_M |\nabla s|^2
    $$
    and since $\int_M \frac{1}{2}\Delta |s|^2 = 0$ by the divergence theorem we obtain
    $$
    \lambda \int_M |s|^2 - \int_M |\nabla s|^2 = 0.
    $$
    Both of these integrands are non-negative and so both of the integrals are non-negative. Hence
    $$
    \lambda \int_M |s|^2 = 0 \quad \text{and} \quad \int_M |\nabla s|^2 = 0.
    $$
    As $\deg(E) < 0$ we know that $\lambda < 0$ and so $|s|^2 = 0$ everywhere on $M$ giving us that $s = 0$. 
    </li>
    <li>
    Let $F$ be a reflexive subsheaf of $E$ with
    $$
    0 < s = \operatorname{rank}(F) < r = \operatorname{rank}(E).
    $$
    The inclusion $\iota : F \hookrightarrow E$ induces a morphism $\det \iota : \det(F) \to \left(\bigwedge^s E\right)^{\ast\ast} \cong \bigwedge^s E$ which is a monomorphism of sheaves since $F$ is torsion-free. Tensoring with $(\det(F))^\ast$ one obtains a non-trivial global holomorphic section
    $$
    f : \mathcal{O}_M \to \bigwedge^s E \otimes (\det(F))^\ast.
    $$
    Also $\lambda = \frac{\pi n}{\operatorname{vol}(M)} \mu(E)$, and $\det(F)$ as a line bundle admits a Hermite-Einstein metric with a factor
    $$
    \gamma = \frac{\pi n s}{\operatorname{vol}(M)}\mu(F).
    $$
    The bundle $\bigwedge^s E \otimes (\det(F))^\ast$ is thus Hermite-Einstein with a factor $s\lambda - \gamma$, and from the existence of the section $f$ one gets 
    $$
    s\lambda - \gamma \ge 0
    $$
    or equivalently
    $$
    \mu(F) \le \mu(E)
    $$
    as desired. To see the second assertation, note that if $E$ is not stable, then there exists a reflexive subsheaf $F$ with $\mu(F) = \mu(E)$ and the sequence
    $$
    0 \longrightarrow F \longrightarrow E \longrightarrow E/F \longrightarrow 0
    $$
    splits. From $\mu(F) = \mu(E)$ one gets that $F$ and $E/F$ satisfy the Hermite-Einstein condition with a factor $\lambda$ and inducting on the rank of $E$ completes the proof.
    </li>
    <li>
    For any curvature tensor $F$ of $E$ consider the characteristic number
    $$
    C=\int_{M} \operatorname{tr}\left(\frac{i}{2 \pi} F_\nabla-a \omega \operatorname{id}_{E}\right)^2 \wedge \omega^{n-2},
    $$
    where $a = \frac{\mu(E)}{\int_M \omega^n}$. Expanding the square yields
    $$
    C=\int_M \left(c_{1}^{2}(E)-2 c_{2}(E)\right)\wedge [\omega]^{n-2} -ra^{2} \int_{M} \omega^{n}.
    $$
    Decomposing $F_\nabla$ into its self-dual and anti-self-dual parts $F_\nabla = F^+_\nabla + F^-_\nabla$ we obtain
    $$
    C=-(n-1)!\left\|\frac{i}{2 \pi} F^{-}_\nabla\right\|^{2}+\int_{M} \operatorname{tr}\left(\frac{i}{2 \pi} F^{+}_\nabla - a \omega \operatorname{id}_{E}\right)^{2} \wedge \omega^{n-2}.
    $$
    Let $k$ be the last integral in the above expression, then $k \ge 0$ and the equality holds if and only if $F_\nabla$ is Einstein. Now
    $$
    \begin{aligned}
    k & =\int_{M} \operatorname{tr}\left(\frac{i}{2 \pi} F^{+}_\nabla\right)^{2} \wedge \omega^{n-2}-2 a c_{1}(E) \wedge \omega^{n-1}+r a^{2} \omega^{n} \\
    & =(n-1)!\left\|\frac{i}{2 \pi} F^{+}_{\nabla}\right\|^{2}-2(n-1) \cdot(n-2)!\left\|\frac{i}{2 \pi} F_\nabla^{2,0}\right\|^{2}-r a^{2} \int_{M} \omega^{n}
    \end{aligned}
    $$
    and so
    $$
    \left\|\frac{i}{2 \pi} F^{+}_{\nabla}\right\|^{2} = \frac{1}{(n-1)!}\left(k+2(n-2) \cdot(n-2)!\left\|\frac{\sqrt{-1}}{2 \pi} F_\nabla^{2,0}\right\|^{2}+r a^{2} \int_{M} \omega^{n}\right),
    $$
    which combined with $\left\|\frac{i}{2 \pi} F_\nabla\right\|^{2}=-\frac{1}{(n-2)!} C+\frac{1}{(n-2)!} k$ gives
    $$
    \begin{aligned}
        \int_{M} |F_\nabla |^{2} &= \left\|F^{+}_{\nabla}\right\|^{2}+\left\|F^{-}_{\nabla}\right\|^{2} \\
        &= 4 \pi^{2}\left(\frac{n C}{(n-1)!}+\frac{2(n-2)}{n-1}\left\|\frac{\sqrt{-1}}{2 \pi} F_\nabla^{2,0}\right\|^{2}+\frac{n r}{(n-1)!} a^{2} \int_{M} \omega^{n}\right. \\
        & \left.-\frac{1}{(n-2)!}\int_M \left(c_{1}^{2}(E)-2 c_{2}(E)\right) \wedge [\omega]^{n-2}\right).
        \end{aligned}
    $$
    It follows that $\operatorname{YM}$ is bounded below by a topological constant given by
    $$
    \begin{aligned}
        \operatorname{YM} &\ge \frac{4 \pi^{2}}{r(n-2)!}\left(\frac{\left(\int_M c_{1}(E) \wedge [\omega]^{n-1} \right)^{2}}{\int_M [\omega]^{n}}-\int_M c_{1}^{2}(E)\wedge [\omega]^{n-2}\right) \\
        & +\frac{1}{n-1}\frac{\left(\int_M c_{1}(E) \wedge [\omega]^{n-1} \right)^{2}}{\int_M [\omega]^{n} } \\
        & \left.+\int_M \left(2 r c_{2}(E)-(r-1) c_{1}^{2}(E)\right)\wedge [\omega]^{n-2}\right).
    \end{aligned}
    $$
    </li>
</ol>
</div>

---

Next, we'll define so-called <b>irreducible</b> connections.

<div class="definition">
A connection $\nabla$ on $(E,h)$ is called irreducible if one of the following equivalent conditions holds.
<ol>
    <li>
    $E$ has no $\nabla$-invariant subbundle $F$ except the trivial one and itself.
    </li>
    <li>
    The holonomy group acts irreducibly on each fibre.
    </li>
    <li>
    Every parallel skew-Hermitian endomorphism of $E$ is constant.
    </li>
    <li>
    Every parallel endomorphism of $E$ is constant.
    </li>
    <li>
    $E$ is not a direct sum of proper $\nabla$-invariant subbundles.
    </li>
    <li>
    $E$ is not an orthogonal sum of proper $\nabla$-invariant subbundles.
    </li>
</ol>
</div>

Under certain topological constraints one can show that for every rank $2$ bundle over $M$, any Hermite-Einstein connection is irreducible. Moreover this yields stability for $E$.

<div class="proposition">
Let $M$ be a compact Kähler manifold with $H^{1,1}(M) \cong \Bbb C$ and let $E \to M$ be a rank $2$ vector bundle over $M$ with non-zero discriminant. That is,
$$
\Delta(E) = 4c_2(E) - c^2_1(E) \ne 0.
$$
Then any Hermite-Einstein connection on $E$ is irreducible.
</div>

<div class="proof">
Suppose that $E$ admits a reducible Hermite-Einstein connection $\nabla$. Then $E = L_1 \oplus L_2$ for line bundles $L_1$ and $L_2$. Thus the curvature $F$ of $E$ is locally given by a matrix
$$
\begin{pmatrix}F _1&0\\ 0&F_2\end{pmatrix},
$$
where $F_1$ and $F_2$ the respective curvatures of $L_1$ and $L_2$. The Hermite-Einstein condition yields $\Lambda(F_1-F_2) = 0$ and the condition $H^{1,1}(M) \cong \Bbb C$ implies that there is no harmonic $2$-form perpendicular to $\omega$ and so $F_1 = F_2$. It follows that $E$ is projectively flat and since
$$
c_k(E) = \binom{r}{k}(c_1(E)/r)^k,
$$
holds for projectively flat bundles, we obtain $4c_2(E) = c^2_1(E)$ i.e. $\Delta(E) = 0$.
</div>

Ultimately, we are aiming to build the theory around the <b>Kobayashi–Hitchin correspondence</b>. I've briefly mentioned about this in <a href="https://anthonymakela.com/complex%20geometry/differential%20geometry/2024/03/25/hermite-einstein-and-k%C3%A4hler-einstein-metrics.html" style="color:#680530; text-decoration: underline;">Hermite-Einstein Metrics and Stability</a> as the theorem by Donaldson, Uhlenbeck and Yau, but let's briefly go over a bit of history around this before we march onto looking at moduli spaces.

The whole concept of stability originates from algebro-geometric notions, whereas the Hermite-Einstein condition is purely differential-geometric. On one hand we have the moduli space of (poly)stable holomorphic vector bundles and on the ohter, the moduli space of Hermite-Einstein connections up to gauge equivalence. The Kobayashi–Hitchin correspondence states that these two moduli spaces are the same.

---

To set up shop, let $E$ be a complex vector bundle of rank $r$ over a complex manifold $M$ and denote the group of smooth bundle automorphisms of $E$ by $\mathrm{GL}(E)$. The following propositions will serve as our guiding light towards the definition for the moduli space of holomorphic structures.

<div class="proposition">
Let $E$ be a holomorphic vector bundle over a complex manifold $M$. Then there exists a unique connection $\nabla$ such that
$$
\nabla^{0,1} = \bar{\partial}.
$$
For such a connection, the $(0,2)$-component $\nabla^{0,1} \circ \nabla^{0,1}$ of the curvature $F_\nabla$ vanishes.
</div>

The connection in the above proof is called the Chern connection. For a proof of the proposition, see <a href="https://anthonymakela.com/complex%20geometry/differential%20geometry/2024/03/01/holomorphic-connections-atiyah-class.html" style="color:#680530; text-decoration: underline;">Holomorphic Connections and The Atiyah Class</a>. The converse is the bit about which we are mostly interested today.

<div class="theorem" text="(Koszul-Malgrange)">
Let $E$ be a complex vector bundle over a complex manifold $M$. If $\nabla$ is a connection in $E$ such that
$$
\nabla^{0,1} \circ \nabla^{0,1} = 0,
$$
then there exists a unique holomorphic vector bundle structure in $E$ such that $\nabla^{0,1} = \bar{\partial}$.
</div>


Denote now by $\mathscr{D}^{0,1}(E)$ the set of all $\Bbb C$-linear maps

$$
\nabla^{0,1} : \Omega^0(E) \to \Omega^{0,1}(E),
$$

satisfying $\nabla^{0,1}(fs) = \bar{\partial}f \otimes s + f \nabla^{0,1}s$. Recall from <a href="https://anthonymakela.com/differential%20geometry/2023/10/11/connections.html" style="color:#680530; text-decoration: underline;">Connections</a> that $\mathscr{D}^{0,1}(E)$ is an affine space. Let $\mathscr{H}^{0,1}(E) \subset \mathscr{D}^{0,1}(E)$ be the subset consisting of $\nabla^{0,1}$ with

$$
\left(\nabla^{0,1}\right)^2 = \nabla^{0,1} \circ \nabla^{0,1} = 0.
$$

Now if $E$ is a holomorphic vector bundle, then $\bar{\partial} : \Omega^0(E) \to \Omega^{0,1}(E)$ gives a well-defined element of $\mathscr{H}^{0,1}(E)$. Conversely, by the Koszul-Malgrange Theorem every $\nabla^{0,1} \in \mathscr{H}^{0,1}(E)$ defines a unique holomorphic structure in $E$ for which $\nabla^{0,1} = \bar{\partial}$. Hence one can consider $\mathscr{H}^{0,1}(E)$ as the set of holomorphic bundle structures in $E$. The action of $\mathrm{GL}(E)$ on $\mathscr{D}^{0,1}(E)$ is given by conjugation

$$
(f,\nabla^{0,1}) \mapsto f^{-1} \circ \nabla^{0,1} \circ f.
$$

Note that $f^{-1} \circ \nabla^{0,1} \circ f = \nabla^{0,1} + f^{-1}\bar{\partial}f$. For $\nabla^{0,1} \in \mathscr{H}^{0,1}(E)$ we have that

$$
\begin{align*}
(f^{-1} \circ \nabla^{0,1} \circ f)^2 = 0
\end{align*}
$$

and so $\mathrm{GL}(E)$ preserves $\mathscr{H}^{0,1}(E)$. Therefore, one can introduce the orbit space 

$$
\mathscr{H}^{0,1}(E)/\mathrm{GL}(E),
$$

which we will call the <b>moduli space of holomorphic structures</b> in $E$. Unfortunately, there is a slight problem with this definition. The space we are considering is in general non-Hausdorff. The way to resolve this is to consider (semi)stable bundles.

Fix now a Hermitian structure $h$ in the complex vector bundle $E$ and consider the subgroup $\mathrm{U}(E,h)$ of $\mathrm{GL}(E)$ consisting of unitary automorphisms of $E$. Let $\mathscr{D}(E,h)$ be the set of connections $\nabla$ in $E$ that preserve $h$. That is, $\mathscr{D}(E,h)$ consits of $\Bbb C$-linear maps $\nabla : \Omega^0(E) \to \Omega^1(E)$ for which 

$$
\nabla(fs) = df \otimes s + f\nabla s
$$

and

$$
dh(s,t) = h(\nabla s, t) + h(s,\nabla t).
$$

Recall that such connections extend to connections $\nabla : \Omega^{p,q}(E) \to \Omega^{p+1,q}(E) \oplus \Omega^{p,q+1}(E)$. Now for $\nabla = \nabla^{1,0} + \nabla^{0,1}$, we have that $\nabla^{0,1} \in \mathscr{D}^{0,1}(E)$ and so we have a natural bijection

$$
\begin{align*}
\mathscr{D}(E,h) &\to \mathscr{D}^{0,1}(E) \\
\nabla &\mapsto \nabla^{0,1}.
\end{align*}
$$

Indeed for $\nabla^{0,1} \in \mathscr{D}^{0,1}(E)$, the map $\nabla^{1,0}$ is determined by 

$$
\bar{\partial}h(s,t) = h(\nabla^{0,1}s,t) + h(s,\nabla^{1,0}t).
$$

Let $\operatorname{End}(E,h)$ denote the vector bundle of skew-Hermitian endomorphisms of $(E,h)$. If one fixes a connection $\nabla_0 \in \mathscr{D}(E,h)$, then for every $\nabla \in \mathscr{D}(E,h)$ the difference $\alpha = \nabla - \nabla_0$ satisfies

$$
h(\alpha s, t) + h(s,\alpha t) = 0.
$$

Thus $\alpha$ can be regarded as an element of $\Omega^1(\operatorname{End}(E,h))$. Conversely, given any such form $\alpha$, setting $\nabla = \nabla_0 + \alpha$ gives an element in $\mathscr{D}(E,h)$. It follows that $\mathscr{D}(E,h)$ is an affine space over $\Omega^1(\operatorname{End}(E,h))$. Let $\mathscr{H}(E,h)$ denote the subset of $\mathscr{D}(E,h)$ consisting of elements with $\nabla = \nabla^{1,0} + \nabla^{0,1}$ such that

$$
\nabla^{0,1} \circ \nabla^{0,1} = 0.
$$

That is,

$$
\mathscr{H}(E,h) = \{\nabla \in \mathscr{D}(E,h) \mid \nabla^{0,1} \in \mathscr{H}^{0,1}(E)\}.
$$

It's not too hard to verify that we again obtain a bijection $\mathscr{H}(E,h) \to \mathscr{H}^{0,1}(E)$. Putting two and two together we have the following diagram:

$$
\xymatrix{
\mathscr{D}(E,h) \ar@{<->}[r] & \mathscr{D}^{0,1}(E) \\
\mathscr{H}(E,h) \ar@{->}[u] \ar@{<->}[r] & \mathscr{H}^{0,1}(E). \ar@{->}[u]
}
$$

Note that for $f \in \mathrm{U}(E,h)$ and $\nabla \in \mathscr{H}(E,h)$ we have

$$
(f^{-1} \circ \nabla \circ f)^2 = 0
$$

and so the action of $\mathrm{U}(E,h)$ on $\mathscr{D}(E,h)$ by conjugation preserves $\mathscr{H}(E,h)$. Since there is a one-to-one correspondence between $\mathscr{D}(E,h)$ and $\mathscr{D}^{0,1}(E)$, the group $\mathrm{GL}(E)$ acting on $\mathscr{D}^{0,1}(E)$ must act also on $\mathscr{D}(E,h)$. This action is given by

$$
(f,\nabla) \mapsto f^\ast \circ \nabla^{1,0} \circ (f^{\ast})^{-1} + f^{-1} \circ \nabla^{0,1} \circ f.
$$

Here $f^\ast$ is the adjoint of $f$. Now since the action of $\mathrm{GL}(E)$ on $\mathscr{D}^{0,1}(E)$ preserves $\mathscr{H}^{0,1}(E)$, the action on $\mathscr{D}(E,h)$ will also preserve $\mathscr{H}(E,h)$.

The action of $\mathrm{U}(E,h)$ on $\mathscr{D}(E,h)$ or $\mathscr{H}(E,h)$ is not effective. For a unitary automorphism $f$, the equality

$$
f^\ast \circ \nabla^{1,0} \circ (f^{\ast})^{-1} + f^{-1} \circ \nabla^{0,1} \circ f = \nabla
$$

yields $\nabla \circ f = f \circ \nabla$, i.e. $f$ is parallel with respect to $\nabla$. We obtain the following proposition.

<div class="proposition">
The subgroup of $\mathrm{U}(E,h)$ fixing a given $\nabla \in \mathscr{D}(E,h)$ consists of automorphisms of $E$ which are parallel with respect to $\nabla$. It is therefore naturally isomorphic to the centralizer in the unitary group $\mathrm{U}(r)$ of the holonomy group of the connection $\nabla$. In particular, it is compact.
</div>

What we would like to achieve here is that the spaces $\mathscr{D}(E,h)/\mathrm{U}(E,h)$ and $\mathscr{H}(E,h)/\mathrm{U}(E,h)$ were Hausdorff. To do so there is one more thing we need to consider. Is the action of $\mathrm{U}(E,h)$ to these spaces proper?

<div class="proposition">
The action of $\mathrm{U}(E,h)$ on $\mathscr{D}(E,h)$ or $\mathscr{H}(E,h)$ is proper.
</div>

<div class="proof">
Let $\nabla_j \in \mathscr{D}(E,h)$ be a sequence of connections such that $\nabla_j \to \nabla_\infty \in \mathscr{D}(E,h)$ and let $f_j \in \mathrm{U}(E,h)$ be a sequence of automorphisms of $E$ such that 

$$
\nabla^{f_j}_j := f_j^\ast \circ \nabla_j^{1,0} \circ (f_j^{\ast})^{-1} + f_j^{-1} \circ \nabla_j^{0,1} \circ f_j \to \nabla^\ast \in \mathscr{D}(E,h).
$$

It suffices to show that a subsequence of $f_j$ converges to some element $f_\infty \in \mathrm{U}(E,h)$ and $\nabla^\ast = \nabla^{f_\infty}_\infty$. Consider the principal $\mathrm{U}(r)$-bundle $P$ associated to $(E,h)$. Fix $x_0 \in M$ and $v_0 \in P$ over $x_0$. Taking a subsequence, we have

$$
f_j(v_0) \to v^\ast_0 \in P.
$$

Since $f_j$'s commute with the right action of the structure group $\mathrm{U}(r)$of $P$, one obtains

$$
f_j(v_0a) = (f_j(v_0))a \to v^\ast_0a,
$$

for every $a \in \mathrm{U}(r)$. We'll define $f_\infty$ in the following way. Let $x \in M$ and let $c$ be a curve from $x_0$ to $x$. Let $\widetilde{c}_j$ be the horizontal lift of $c$ with respect to $\nabla_j$ such that the starting point is $v_0$. It follows that $f_j(\widetilde{c}_j)$ is the horizontal lift of $c$ with respect to the connection $\nabla^{f_j}_j$ with the starting point $f_j(v_0)$. Since $\nabla_j \to \nabla_\infty$ we have that $\widetilde{c}_j \to \widetilde{c}_\infty$, where $\widetilde{c}_\infty$ is the horizontal lift of $c$ with respect to $\nabla_\infty$ with a starting point $v_0$. Let $\widetilde{c}^\ast$ be the horizontal lift of $c$ with respect to $\nabla^\ast$ such that its starting point if $v_0^\ast$. From $\nabla^{f_j}_j \to \nabla^\ast$ and $f_j(v_0) \to v_0^\ast$ we obtain that $f_j(\widetilde{c}_j) \to \widetilde{c}^\ast$. Defining $f_\infty$ in such a way that $f_\infty(\widetilde{c}_\infty) = \widetilde{c}^\ast$ defines $f_\infty$ completely with the additional information that $f_\infty$ commutes with the right action of $\mathrm{U}(r)$.

</div>

<div class="corollary">
The spaces $\mathscr{D}(E,h)/\mathrm{U}(E,h)$ and $\mathscr{H}(E,h)/\mathrm{U}(E,h)$ are Hausdorff.
</div>

---

Let's then see what kind of data we obtain if we give $M$ more structure. Suppose that $M$ is a compact Kähler manifold with a Kähler metric $g$. Let $\mathscr{E}(E,h)$ denote the subset of $\mathscr{H}(E,h)$ consisting of Hermite-Einstein connections $\nabla$. That is, 

$$
\mathscr{E}(E,h) = \{ \nabla \in \mathscr{H}(E,h) \mid i\Lambda F_\nabla = \lambda \operatorname{id}_E\}.
$$

The first thing to look at is whether or not the action of $\mathrm{U}(E,h)$ on $\mathscr{D}(E,h)$ preserves $\mathscr{E}(E,h)$. Note that for $\nabla \in \mathscr{D}(E,h)$ and $f \in \mathrm{U}(E,h)$ we have that

$$
\begin{align*}
F_{f^{-1} \circ \nabla \circ f} &= (f^{-1} \circ \nabla \circ f) \circ (f^{-1} \circ \nabla \circ f) \\
&= f^{-1} \circ \nabla \circ \nabla \circ f \\
&= f^{-1} \circ F_\nabla \circ f.
\end{align*}
$$

Using this we obtain

$$
\begin{align*}
i\Lambda F_{f^{-1} \circ \nabla \circ f} &= i\Lambda(f^{-1} \circ F_\nabla \circ f) \\
&= f^{-1} \circ i\Lambda F_\nabla \circ f.
\end{align*}
$$

It follows that the action of $\mathrm{U}(E,h)$ on $\mathscr{D}(E,h)$ preserves $\mathscr{E}(E,h)$. Also the natural map

$$
\mathscr{E}(E,h)/\mathrm{U}(E,h) \to \mathscr{H}(E,h)/\mathrm{U}(E,h) 
$$

is injective for obvious reasons. The uniqueness of Hermite-Einstein connections guarantees that even the map

$$
\mathscr{E}(E,h)/\mathrm{U}(E,h) \to \mathscr{H}^{0,1}(E,h)/\mathrm{GL}(E) 
$$

is injective. The space $\mathscr{E}(E,h)/\mathrm{U}(E,h)$ is called the <b>moduli space of Hermite-Einstein structures</b> in $E$.

<div class="proposition">
The moduli space $\mathscr{E}(E,h)/\mathrm{U}(E,h)$ of Hermite-Einstein structures in $E$ is Hausdorff and injects into $\mathscr{H}^{0,1}(E,h)/\mathrm{GL}(E)$.
</div>

The next thing we aim to show is that the moduli space of Hermite-Einstein connections $\mathscr{E}(E,h)/\mathrm{U}(E,h)$ is open in the moduli space $\mathscr{H}^{0,1}(E)/\mathrm{GL}(E)$ of stable holomorphic structures on $E$.

<div class="theorem">
The moduli space of Hermite-Einstein connections $\mathscr{E}(E,h)/\mathrm{U}(E,h)$ is open in the moduli space $\mathscr{H}^{0,1}(E)/\mathrm{GL}(E)$ of stable holomorphic structures on $E$.
</div>

<div class="proof">
Let $\nabla \in \mathscr{E}(E,h)$ and $\nabla^{0,1} \in \mathscr{H}^{0,1}(E)$ be the corresponding connection. We aim to show that given $\widetilde{\nabla}^{0,1} \in \mathscr{H}^{0,1}(E)$ close enough to $\nabla^{0,1}$, there exists $\nabla_1 \in \mathscr{E}(E,h)$ and $f_1 \in \mathrm{GL}(E)$ such that $\nabla^{0,1}_1 = f^{-1}_1 \circ \widetilde{\nabla}^{0,1} \circ f_1$. Denote by $P$ the space of positive definite Hermitian symmetric endomorphisms of $(E,h)$ with determinant $1$. Its tangent space $T_I P$ consists of Hermitian endomorphisms of $E$ with no trace.

For a general connection $\nabla \in \mathscr{D}(E,h)$ and $f \in P$, we have that
$$
\nabla^f :=  f^\ast \circ \nabla^{1,0} \circ (f^{\ast})^{-1} + f^{-1} \circ \nabla^{0,1} \circ f =  f \circ \nabla^{1,0} \circ f^{-1} + f^{-1} \circ \nabla^{0,1} \circ f,
$$

and so the curvature $F_{\nabla^f}$ is given by

$$
\begin{align*}
F_{\nabla^f} &= f \circ \nabla^{1,0} \circ \nabla^{1,0} \circ f^{-1} + f^{-1} \circ \nabla^{0,1} \circ \nabla^{0,1} \circ f \\
&+ (f \circ \nabla^{1,0} \circ f^{-1} \circ f^{-1} \circ \nabla^{0,1} \circ f + f^{-1} \circ \nabla^{0,1} \circ f \circ f \circ \nabla^{1,0} \circ f^{-1}).
\end{align*}
$$

For $i\Lambda F_{\nabla^f}$ we consider its trace-free part 

$$
i\Lambda F^\circ_{\nabla^f} = i\Lambda F_{\nabla^f} - \left(\frac{1}{r} i\Lambda \operatorname{tr}(F_{\nabla^f})\right)I \in T_I P.
$$

Define then a map

$$
\begin{align*}
F : \mathscr{D}(E,h) \times P &\to T_I P \\
(\nabla, f) &\mapsto i\Lambda F^\circ_{\nabla^f},
\end{align*}
$$

and note that the tangent space $T_\nabla(\mathscr{D}(E,h))$ is naturally isomorphic to $\Omega^1(\operatorname{End}(E,h))$. The next step is to calculate the differential 

$$
dF_{(\nabla,I)} : \Omega^1(\operatorname{End}(E,h)) \times T_IP \to T_IP,
$$

at $(\nabla,I)$. Let $a \in T_IP$ and $f(t) = e^{at}$. The $(1,1)$-component of $F_{\nabla^{f(t)}}$ is given by

$$
F^{(1,1)}_{\nabla^{f(t)}} = e^{at} \circ \nabla^{1,0} \circ e^{-2at} \circ \nabla^{0,1} \circ e^{at} + e^{-at} \circ \nabla^{0,1} \circ e^{2at} \circ \nabla^{1,0} \circ e^{-at}.
$$

Differentiating this with respect to $t$ at $t = 0$ yields

$$
\frac{\partial}{\partial t}F^{(1,1)}_{\nabla^{f(t)}}\Big|_{t = 0} = \nabla^{1,0}\nabla^{0,1}a - \nabla^{0,1}\nabla^{1,0}a,
$$

and furthermore

$$
\frac{\partial}{\partial t}i\Lambda F_{\nabla^{f(t)}}\Big|_{t = 0} = \Delta a.
$$

We obtain

$$
dF_{(\nabla,I)}(0,a) = \Delta a.
$$

Extending $F$ to a smooth map on the appropriate Sobolev spaces

$$
F : L^2_k(\mathscr{D}(E,h)) \times L^2_{k+1}(P) \to L^{2}_{k-1}(T_IP),
$$

we have $dF_{(\nabla,I)}(0,a) = \Delta a$, for $a \in L^2_{k+1}(T_IP)$. Now for $\nabla$ irreducible, the map $\Delta : L^2_{k+1}(T_IP) \to L^2_{k-1}(T_IP)$ is an isomorphism. To show this, note that $I = H + G \circ \Delta$ and thus it suffices to show that $\Delta$ is injective. If $\Delta a = 0$, then $a$ is smooth and

$$
0 = (\Delta a, a) = (\nabla^\ast \nabla a, a) = (\nabla a, \nabla a),
$$

that is, $a$ is parallel. It follows that $a$ is of the form $cI_E$ where $c$ is a constant. On the other hand, $a$ is traceless and so $a = 0$. In addition, if $\nabla \in \mathscr{E}(E,h)$, then

$$
F(\nabla, I) = i\Lambda F^{\circ}_\nabla = 0.
$$

Since

$$
L^2_{k+1}(T_IP) \ni a \longmapsto F_{(0,I)}(0,a) = \Delta a \in L^2_{k-1}(T_IP)
$$

is an isomorphism, the implicit function theorem implies that if $\widetilde{\nabla}^{0,1} \in \mathscr{H}^{0,1}(E)$ is sufficiently close to $\nabla^{0,1} \in \mathscr{H}^{0,1}(E)$ so that the corresponding $\widetilde{\nabla} \in \mathscr{D}(E,h)$ is sufficiently close to $\nabla$, then there exists a unique $f \in L^2_{k+1}(P)$ near $I_E$ such that

$$
F(\widetilde{\nabla}, f) = i\Lambda F^\circ_{\widetilde{\nabla}^f} = 0.
$$

Noting that the above equation is elliptic, we obtain from elliptic regularity that $f$ is smooth. We'll now show that there exists $\nabla_1 \in \mathscr{E}(E,h)$ and $f_1 \in \mathrm{GL}(E)$ such that $\nabla^{0,1}_1 = f^{-1}_1 \circ \widetilde{\nabla}^{0,1} \circ f_1$. Since $\mathrm{GL}(E)$ acting on $\mathscr{D}(E,h)$ leaves $\mathscr{H}(E,h)$ invariant, $\widetilde{\nabla} \in \mathscr{H}(E,h)$ implies $\widetilde{\nabla}^f \in \mathscr{H}(E,h)$. On the other hand $i\Lambda F^\circ_{\widetilde{\nabla}^f} = 0$ gives

$$
i\Lambda F_{\widetilde{\nabla}^f} = \varphi I_E,
$$

where $\varphi$ is a function on $M$. Now a conformal change gives a positive function $b$ on $M$ such that the new Hermitian structure $h' = b^2 h$ together with the holomorphic structure $(\widetilde{\nabla}^{0,1})^f$ satisfies the Hermite-Einstein condition. Let $\widehat{\nabla}$ be the connection defined by $h'$ and the holomorphic structure $(\widetilde{\nabla}^{0,1})^f$. That is, $\widehat{\nabla} h' = 0$ and $\widehat{\nabla}^{0,1} = (\widetilde{\nabla}^{0,1})^f$. Now

$$
d(h(\xi,\eta)) = h(b\widehat{\nabla}(b^{-1}\xi), \eta) + h(\xi, b\widehat{\nabla}(b^{-1}\eta)),
$$

and we set $\nabla_1 = b \circ \widehat{\nabla} \circ b^{-1}$, where $b$ is understood as $bI_E$. Then $\nabla_1 h = 0$ and $\nabla_1 \circ \nabla_1 = \widehat{\nabla} \circ \widehat{\nabla}$. Thus $\nabla_1 \in \mathscr{E}(E,h)$. Moreover,

$$
\nabla^{0,1}_1 = f^{-1}_1 \circ \widetilde{\nabla}^{0,1} \circ f_1,
$$

where $f_1 = fb^{-1}$.

</div>

The surjectivity of $\mathscr{E}(E,h)/\mathrm{U}(E,h) \to \mathscr{H}^{0,1}(E,h)/\mathrm{GL}(E)$ was open for quite a while, but eventually resolved by the  Kobayashi–Hitchin correspondence. There was though, some evidence that this should hold:

<div class="proposition">
Let $E$ be a simple holomorphic vector bundle. Then there exists a connection $\nabla$ compatible with the holomorphic structure such that
$$
i\Lambda F_\nabla = \varphi \operatorname{id}_E,
$$
for some constant $\varphi$.
</div>

<div class="proof">
Recall that a holomorphic vector bundle is called simple if every holomorphic endomorphism is constant. Equipping $E$ with a Hermitian structure and letting $\widetilde{\nabla}$ denote the Chern connection we know that
$$
\nabla = \widetilde{\nabla} + \alpha,
$$
for some $\alpha \in \Omega^{1}(\operatorname{End}(E))$. Moreover,
$$
F_{\nabla} = F_{\widetilde{\nabla}} + \widetilde{\nabla}\alpha + \alpha \wedge \alpha.
$$
This gives
$$
i\Lambda F_\nabla = i\Lambda F_{\widetilde{\nabla}} + \partial^\ast \alpha.
$$ 
Since $E$ is simple, the kernel of $\bar{\partial} : \Omega^0(\operatorname{End}(E)) \to \Omega^{0,1}(\operatorname{End}(E))$ consists of constant endomorphisms. Now Hodge theory states that one can solve
$$
\partial^\ast = c\operatorname{id}_E - i\Lambda F_{\widetilde{\nabla}}
$$
if $c\operatorname{id}_E - i\Lambda F_{\widetilde{\nabla}}$ is perpendicular to constants. By taking the constant $c$ so that 
$$
\int_M \operatorname{tr}(c\operatorname{id}_E - i\Lambda F_{\widetilde{\nabla}}) = 0,
$$ 
we are done.
</div>

Next time we'll look at an elliptic complex that arises from the infinitesimal deformations of a Hermitian-Einstein structure and compute its index.
