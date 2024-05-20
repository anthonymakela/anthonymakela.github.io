---
layout: post
title: "Calabi-Yau Manifolds"
categories: [Complex Geometry, Differential Geometry]
mathjax: true
published: true
excerpt_separator: <!--more-->
---

Today, we'll be diving into the so-called <b>Calabi-Yau manifolds</b>. These are manifolds that play an important role in several areas of mathematical physics, most notably in string theory. <!--more--> A Calabi-Yau manifold is a compact Kähler manifold with a vanishing first Chern class, or equivalently vanishing Ricci tensor[^1]. This property not only characterizes its geometric structure but also aligns with the requirements for supersymmetry in string theory. From a purely mathematical perspective, Calabi-Yau manifolds are interesting due to their complex structure, Ricci-flat metric, and holonomy group properties.


Einstein’s theory of gravity, general relativity, constructs equations that the metric of a Riemannian space-time manifold must obey. The equations involve three symmetric tensors: the metric, the Ricci tensor, and the energy-momentum tensor. A Riemannian manifold whose Ricci tensor vanishes is a solution to these equations when there is no matter, and is a special case of an Einstein manifold. A Calabi–Yau manifold has a vanishing Ricci tensor and is therefore of interest in general relativity. A fundamental problem in theoretical physics is the incorporation of Einstein’s theory into the quantum theory of particles. This enterprise is known as quantum gravity, and Calabi–Yau manifolds figure prominently in the leading theory of quantum gravity and string theory.


---

Let's begin our discussions by talking about <i>Ricci-flatness</i>. To start with, consider a Riemannian manifold $(M,g)$ of dimension $n$. <a href="https://anthonymakela.com/differential%20geometry/2023/09/09/tensor-contraction.html" style="color:#680530; text-decoration: underline;">Recall</a> that the Ricci tensor is defined either as the contraction of 

$$
R = R^{\,\,\,\,\,\,l}_{ijk} dx^i \otimes dx^j \otimes dx^k \otimes \partial_l
$$

with respect to the bilinear pairing $T^\ast M \times TM \to \Bbb R$, or as the contraction of

$$
Rm = R_{ijkl}dx^i \otimes dx^j \otimes dx^k \otimes dx^l
$$

with the metric $g$. Generally speaking, we have that $R \equiv 0 \implies \operatorname{Ric} \equiv 0$. The converse depends quite heavily on the dimension $n$. When $n = 1$ both $R \equiv 0$ and $\operatorname{Ric} \equiv 0$. When $n = 2$ or $n = 3$ the vanishing of the Ricci tensor implies that of the Riemann tensor, but when $n \ge 4$ the converse of $R \equiv 0 \implies \operatorname{Ric} \equiv 0$ is hard to determine.

<div class="definition">
A Riemannian manifold $(M,g)$ is called Ricci-flat if $\operatorname{Ric} \equiv 0$.
</div>

---

We'll now introduce the concept of Calabi-Yau manifolds, which are a particular case of Kähler manifolds.

<div class="definition">
A Calabi-Yau manifold of real dimension $2n$ is a compact $n$-dimensional Kähler manifold $(M,J,g)$ such that $g$ is a Ricci-flat metric.
</div>

I haven't yet described the Ricci tensor on a Kähler manifold so that's what we are going to do next. Recall that classically the curvature tensor $R$ of a Riemannian manifold $(M,g)$ is defined as

$$
R(X,Y) = \nabla_X\nabla_Y - \nabla_Y\nabla_X - \nabla_{[X,Y]},
$$

where $\nabla$ is the Levi-Civita connection. The way we have been discussing curvature is by defining it as $F_\nabla = \nabla \circ \nabla$. How do these two notions compare? Not surprisingly they coincide. For the sake of simplicity, assume that $\nabla s = \alpha \otimes t$. We obtain

$$
\begin{align*}
R(X,Y)s &= \nabla_X\nabla_Y s - \nabla_Y\nabla_X s - \nabla_{[X,Y]}s \\
&= \nabla_X(\alpha(Y)t) - \nabla_Y(\alpha(X)t) - \alpha\left([X,Y]\right)t \\
&= \textcolor{green}{X(\alpha(Y))t} + \alpha(Y)\nabla_X t - \textcolor{green}{Y(\alpha(X))t} - \alpha(X)\nabla_Y t - \textcolor{green}{\alpha\left([X,Y]\right)t} \\
&= \textcolor{green}{d\alpha(X,Y)t} + \alpha(Y)\nabla_X t - \alpha(X)\nabla_Y t \\
&= ((d\alpha)t + \alpha\wedge \nabla t)(X,Y) \\
&= \nabla(\alpha \otimes t)(X,Y) \\
&= F_\nabla(X,Y)s.
\end{align*}
$$


<div class="definition">
The Ricci curvature $\operatorname{Ric}$ of a Kähler manifold $(M,J,g)$ is the real two-form given by
$$
\operatorname{Ric}(X,Y) = r(J(X),Y),
$$
where $r(X,Y) = \operatorname{tr}(Z \mapsto R(Z,X)Y)$ is the ordinary Ricci tensor.
</div>

Compare this to how we defined the fundamental form $\omega$. The symmetry of $r$ implies analogously that $\operatorname{Ric}$ is a $2$-form. I mentioned in the beginning that this is equivalent to the vanishing of the first Chern class of $M$. Let's go over a lemma and then justify this claim.

<div class="lemma">
Let $(M,J,g)$ be a Kähler manifold and $\nabla$ the Levi-Civita or, equivalently, the Chern connection. Then 
$$
\operatorname{Ric} = i\operatorname{tr}(F_\nabla).
$$
</div>

<div class="proof">
Consider an orthonormal basis $e_1,\dots,e_n,\widetilde{e}_1 = J(e_1),\dots,\widetilde{e}_n = J(e_n)$. Then, utilizing some of the identities from Riemannian geometry we obtain
$$
\begin{align*}
\operatorname{Ric}(X,Y) &= \operatorname{tr}(Z \mapsto R(Z,Y)J(X)) \\
&= \sum g(R(e_i,Y)J(X), e_i) + g(R(\widetilde{e}_i, Y)J(X), \widetilde{e}_i) \\
&= -\sum g(J(X), R(e_i,Y)e_i) + g(J(X),R(\widetilde{e}_i, Y)\widetilde{e}_i) \\
&= \sum g(X, R(e_i, Y)\widetilde{e}_i) - g(X, R(\widetilde{e}_i,Y)e_i) \\
&= -\sum g(X, R(\widetilde{e}_i,e_i)Y) \\
&= -\sum g(R(e_i,\widetilde{e}_i)X, Y).
\end{align*}
$$

Also

$$
\begin{align*}
\operatorname{tr}(F_\nabla)(X,Y) &= \operatorname{tr}(Z \mapsto F_\nabla(X,Y)Z) \\
&= \operatorname{tr}(Z \mapsto R(X,Y)Z) \\
&= \sum \langle R(X,Y)e_i, e_i\rangle \\
&= \sum g(R(X,Y)e_i, e_i) - i\omega(R(X,Y)e_i, e_i) \\
&= \sum g(R(X,Y)e_i, e_i) + ig(R(X,Y)e_i, e_i) \\
&= \sum g(R(e_i,e_i)X, Y) + ig(R(e_i,\widetilde{e_i})X, Y) \\
&= \sum ig(R(e_i,\widetilde{e_i})X, Y),
\end{align*}
$$

which yields the desired result.
</div>

<div class="proposition">
Let $(M,J,g)$ be a Calabi-Yau manifold. Then $c_1(M) = 0$.
</div>

<div class="proof">
Recall that the Chern classes of $M$ are defined in terms of the holomorphic tangent bundle. Also, in general if $E$ is a vector bundle over $M$ with curvature $F_\nabla$, then 
$$
c_1(E) = \left[\frac{i}{2\pi}\operatorname{tr} F_\nabla\right].
$$
Now since $\operatorname{tr}(F_\nabla) = -i\operatorname{Ric}$ we have that 
$$
c_1(M) = \left[\frac{1}{2\pi}\operatorname{Ric}\right] = 0,
$$
when $\operatorname{Ric} \equiv 0$.
</div>

The converse of this is much more complicated. It was conjectured by Calabi that a compact Kähler manifold with vanishing first Chern class admits a unique
Ricci-flat metric. The uniqueness was proved by Calabi, while the existence by Yau later on. We'll get back to this shortly, but for now, let's look at some properties of $\operatorname{Ric}$.

<div class="proposition">
<ol>
    <li>
    In local coordinates, $\operatorname{Ric}$ can be expressed as
    $$
     \operatorname{Ric} = \sqrt{-1}\partial\bar{\partial}\log\det(g_{j\bar{k}}).
    $$
    
    </li>
    <li>
    The Ricci form $\operatorname{Ric}$ is closed.
    </li>
    <li>
    The cohomology class of $\operatorname{Ric}$ is (up to some real factor) equal to the Chern class of the canonical bundle of $M$.
    </li>
</ol>
</div>

<div class="proof">
<ol>
    <li>
    Note that
    $$
    \begin{align*}
        \operatorname{Ric}(JX,JY) &= \operatorname{Ric}(J^2X,JY) \\
        &= -\operatorname{Ric}(X, JY) \\
        &= -\operatorname{Ric}(JY, X) \\
        &= -\operatorname{Ric}(Y,X) \\
        &= \operatorname{Ric}(X,Y).
    \end{align*}
    $$
    That is $\operatorname{Ric}$ is a $(1,1)$-form. Now $\operatorname{Ric}_{i\bar{j}} = \operatorname{Ric}(\partial_i,\partial_{j}) = \operatorname{Ric}(J\partial_i,\partial_j) = \sqrt{-1}R_{i\bar{j}}$. It follows that
    $$
    \begin{align*}
        \operatorname{Ric} &= \operatorname{Ric}_{i\bar{j}}dz^i \wedge d\bar{z}^j \\
        &=\sqrt{-1}R_{i\bar{j}}dz^i \wedge d\bar{z}^j \\
        &=-\sqrt{-1}\left(\partial_i\partial_j \log \det(g_{k\bar{l}})\right)dz^i \wedge d\bar{z}^j \\
        &=-\sqrt{-1}\left(\partial\bar{\partial} \log \det(g_{k\bar{l}})\right)
    \end{align*}    
    $$
    </li>
    <li>
    This follows directly from $1$.
    </li>
    <li>
    Recall that $c_1(M) = \left[\frac{1}{2\pi}\operatorname{Ric}\right]$. Hence $[\operatorname{Ric}] = 2\pi c_1(M)$.
    </li>
</ol>
</div>

<div class="theorem" text="(Calabi-Yau)">
Let $(M,J,g)$ be a compact Kähler manifold with Kähler form $\omega$. Suppose that $\rho'$ is a real, closed $(1,1)$-form on $M$ with $[\rho'] = 2\pi c_1(M)$. Then there exists a unique Kähler metric $g'$ on $M$ with Kähler form $\omega'$, such that $[\omega'] = [\omega] \in H^2(M, \Bbb R)$, and $\rho'$ is the Ricci form of $g'$.
</div>

Note that $[\omega'] = [\omega]$ says that $g$ and $g'$ are in the same Kähler class. The conjecture was originally posed by Calabi in $1954$ and proved by Yau in $1976$. The important aspect of this is that whenever $c_1(M) = 0$ we can choose $\rho' \equiv 0$, and then $g'$ becomes a Ricci-flat metric[^2].

<div class="corollary">
Let $(M,J)$ be a compact complex manifold with $c_1(M) = 0 \in H^2(M, \Bbb R)$. Then every Kähler class on $M$ contains a unique Ricci-flat Kähler metric $g$.
</div>

The reason why this is useful is that it allows us to find Calabi-Yau manifolds. Another straightforward consequence of the Calabi-Yau theorem states:

<div class="corollary">
Every compact complex manifold with a positive (negative) first Chern class admits a Kähler structure with a positive (negative) Ricci form.
</div>

Note that we do not have to additionally assume the existence of a Kähler structure here. This is because the real $(1, 1)$-form that represents the first Chern class can already supplement the existing complex structure to serve as the Kähler form.

Because Ricci-flatness essentially says that a metric is Einstein with proportionality constant zero, the first of the two above corollaries can be understood as asserting the existence of a Kähler-Einstein structure with vanishing scalar curvature. A natural question to ask would be a stronger version of the above corollary yielding the existence of a Kähler-Einstein metric with a non-zero proportionality constant. In the negative case, Aubin and Yau both independently answered to the question affirmatively.

<div class="theorem" text="(Aubin-Yau)">
Any compact complex manifold with a negative first Chern class admits a Kähler-Einstein metric.
</div>

The positive case turns out to be false in general. However, Tian proposed the concept of <i>$K$-stability</i> as both a necessary and sufficient condition for a complex manifold to satisfy this statement, building on top of the work initially introduced by Yau.

Since the low-dimensional Calabi-Yau manifolds seem to be the interesting stuff in today's research the following definition is in place.

<div class="definition">
Let $M$ be a Calabi-Yau manifold of complex dimension $n$. Then we say that $M$ is
<ul>
    <li>
    A Calabi-Yau elliptic curve, if $n = 1$.
    </li>
    <li>
    A $K3$-surface, if $n = 2$.
    </li>
    <li>
    A Calabi-Yau threefold, if $n = 3$.
    </li>
</ul>
</div>

Let's focus a a bit on the case with $n = 3$, i.e. Calabi-Yau threefolds before we move on. Recall that for Kähler manifolds, the Hodge numbers satisfy

$$
h^{p,q} = h^{q,p} = h^{n-p,n-q} = h^{n-q,n-p},
$$

by conjugation and Serre duality. For Calabi-Yau manifolds, there is even more symmetry in the Hodge diamond which we will see soon. 

<div class="lemma">
Let $(M,J,g)$ be a compact Kähler manifold. The canonical bundle $K_M$ is trivial if and only if there exists a globally defined, nowhere vanishing $(m,0)$-form.
</div>

<div class="proof">
Recall that $K_M = \bigwedge^{m,0}M$, so the sections are $(m,0)$-forms. Triviality of this bundle implies that the total space of $K_M$ is given by $M \times \Bbb C$. Therefore, corresponding to the unit section $M \times \{1\}$, that is the constant function $1$, there is a globally defined and nowhere vanishing holomorphic $(m,0)$-form $\eta$, which is usually called the <i>holomorphic volume form</i>. Conversely, the existence of a globally-defined nowhere vanishing $(m,0)$-form implies that $K_M$ is trivial directly.
</div>

From the lemma above it is clear that any globally defined $(m, 0)$-form can be written as $f\eta$ for some function $f$ on $M$. If $M$ is compact and the form is holomorphic, $f$ must be holomorphic and hence constant. This gives $h^{m,0}(M) = 1$.

In our case, we obtain $h^{3,0}(M) = 1$, i.e. the existence of a unique holomorphic volume form $\eta$. Given a $(0,q)$ cohomology class $[\alpha]$, there is a unique $(0,3-q)$ class $[\beta]$ such that $\int_M \alpha \wedge \beta \wedge \eta = 1$. Thus $h^{0,q}(M) = h^{0,3-q}(M)$. It follows that 

$$
h^{3,0}(M) = h^{0,3}(M) = h^{0,0}(M) = h^{3,3}(M) = 1.
$$

Also, one can show that $h^{1,0}(M) = 0$ and so 

$$
h^{1,0} = h^{0,1} = h^{0,2} = h^{2,0} = h^{2,3} = h^{3,2} = h^{3,1} = h^{1,3} = 0.
$$

The remaining independent Hodge numbers are $h^{1,1}$ and $h^{2,1}$, hence the Hodge diamond takes the form:

$$
\begin{array}{cccccccc}
  &   &   &   & 1 &   &   &   \\
  &   &   & 0 &   & 0 &   &   \\
  &   & 0 &   & h^{1,1} &   & 0 &   \\
  & 1 &   & h^{2,1} &   & h^{2,1} &   & 1 \\
  &   & 0 &   & h^{1,1} &   & 0 &   \\
  &   &   & 0 &   & 0 &   &   \\
  &   &   &   & 1 &   &   &   \\
\end{array}
$$

One can use the Euler characteristic to get a constraint on the remaining two Hodge numbers. This yields

$$
\chi(M) = 2(h^{1,1}-h^{2,1}).
$$

Thus, if we can compute the Euler characteristic, we only have to compute one of the two independent Hodge numbers to get all the topological data. Recall from <a href="https://anthonymakela.com/differential%20geometry/2024/01/11/chern-classes.html" style="color:#680530; text-decoration: underline;">Chern Classes
</a> the relationship between Chern classes and the Euler class. This and the Generalized Gauss-Bonnet Theorem yield yet another constraint for the Hodge numbers:

$$
\int_M c_3(M) = 2(h^{1,1}-h^{2,1}).
$$

There is an interesting property of Calabi-Yau threefolds which is that they apparently come in mirror pairs $(M,W)$ such that $H^{2,1}(W) = H^{1,1}(M)$ and $H^{1,1}(W) = H^{2,1}(M)$. This seems to have something to do with exchanging the complex structure moduli with the Kähler structure moduli and is supposedly the basic idea behind mirror symmetry.

---

Now, my current interests lie in studying the question posed by Atiyah on whether or not all holomorphic vector bundles admit a holomorphic connection over a compact Kähler manifold that also admits a flat connection. Equivalently whether or not the vanishing of the Atiyah class implies that the bundle admits a flat connection. Yau's proof of the Calabi conjecture gives an affirmative answer to this when we specialize in the case of a holomorphic tangent space $TM$ of a compact Kähler manifold $M$.  

Recall that for the Atiyah class, we have

$$
A(E) = [F_\nabla].
$$

<div class="proposition">
Let $X$ be a compact Kähler manifold and let $E$ be a holomorphic vector bundle admitting a holomorphic connection $\nabla : E \to T^\ast_{1,0} \otimes \operatorname{End}(E)$. Then $c_k(E) = 0$ for all $k > 0$.
</div>

<div class="proof">
The $k$'th Chern character can be written in terms of the Atiyah class as
$$
\operatorname{ch}_k(E) = \frac{1}{k!}\left(\frac{i}{2\pi}\right)^k \operatorname{tr}\left(A(E)^{\otimes k}\right).
$$
Since $A(E)$ vanishes when $E$ admits a holomorphic connection, the Chern characters $\operatorname{ch}_k(E)$ vanish also for $k > 0$. Thus $c_k(E) = 0$ for all $k > 0$.
</div>

Notice how this implies that any compact Kähler manifold that has a holomorphic tangent bundle equipped with a holomorphic connection is Calabi-Yau.

<div class="proposition">
Let $(M,J,g)$ be a compact Kähler manifold and suppose that $A(TM) = 0$. Then $TM$ admits a flat connection.
</div>

<div class="proof">
The proof follows from the above proposition, the Calabi-Yau theorem, and the uniformization theorem. Note that by the above proposition $A(TM) = 0$ implies that $c_1(M) = 0$ and $c_2(M) = 0$. Since $c_1(M) = 0$, $M$ admits a Ricci-flat metric and is thus a Kähler-Einstein manifold. Recall now that by the uniformization theorem $\widetilde{X} \cong \Bbb C^n$ since 
$$
\left(2(n+1)c_2(X) - nc_1(X)^2\right)\wedge [\omega]^{n-2} = 0.
$$
Therefore $M \cong \Bbb C^n/\Gamma$ and hence, up to a finite unramified covering, $TM$ is holomorphically trivial yielding that it admits a holomorphic flat connection.
</div>

Note that in the above proof, $A(TM) = 0$ is significantly stronger than what we actually needed. The flatness of $TM$ was characterized by the first two Chern classes, but $A(TM) = 0$ gave that $c_k(TM) = 0$ for all $k > 0$.

---

[^1]: These are just two of many definitions. We'll see that there are multiple different ways to define these things.

[^2]: It's worth mentioning here that we know pretty much nothing about the Ricci-flat metric other than that it exists. In fact, no explicit non-flat examples of Calabi-Yau metrics on compact manifolds are known at all.

