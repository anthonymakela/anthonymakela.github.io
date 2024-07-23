---
layout: post
title: "Infinitesimal Deformations and The Kodaira-Spencer Map"
categories: [Complex Geometry, Differential Geometry]
mathjax: true
published: true
excerpt_separator: <!--more-->
---

Infinitesimal deformation, broadly speaking, considers the infinitesimal variations in the _structures_ of certain mathematical objects. Imagine an object in space, potentially rigid, whose shape changes due to the application of external forces. At each moment in time, $t$, the object assumes a slightly different shape.

<!--more-->

In particular, given a compact complex manifold $M$, deformation theory allows us to study the variations of different complex manifold structures on $M$ which depend (either continuously, smoothly, or holomorphically) on a variable $t$. Recall that a compact complex manifold $M$ can be constructed by gluing domains in $\mathbb{C}^n$ via the holomorphic transition functions. By allowing these transition functions to depend on an additional variable $t$, we can create a family of different ways to glue the same domains together. Consequently, we obtain a family of compact complex manifolds $M_t$, each representing a deformation of the original manifold $M$. This concept ties into moduli spaces and moduli problems.

These moduli spaces are central to many areas of algebraic geometry and complex analysis. A moduli space, in broad terms, is a parameter space for a class of objects, meaning that each point in this space represents an equivalence class of these objects. For instance, the moduli space of compact complex manifolds of a given dimension parametrizes all such manifolds up to isomorphism.

When studying deformations of a compact complex manifold $M$, one often examines the tangent space to the moduli space at the point corresponding to $M$. This tangent space can be identified with the first cohomology group of the tangent sheaf of $M$, denoted as $H^1(M, T_M)$. Elements of this cohomology group correspond to infinitesimal deformations of the complex structure on $M$.


---

As mentioned above, a compact complex manifold $M$ is obtained by gluing domains $U_1,\dots,U_j,\dots, U_l$ in $\Bbb C^n$. We'll denote the biholomorphic transition maps of the charts $(U_j,z_j)$ by

$$
f_{jk} = z_j \circ z^{-1}_k : z_k(U_j \cap U_k) \to z_j(U_j \cap U_k),
$$

where $z_j : U_j \to z_j(U_j) \subset \Bbb C^n$ is the map $z_j(p) = (z^{1}\_j(p),\dots,z^{n}\_j(p))$. Since $z_j(U_j \cap U_k) \subset \Bbb C^n$, $f_{jk}$ can be written in terms of its components as

$$
f_{jk} = (f^1_{jk},\dots,f^{n}_{jk})
$$

and so $z^\alpha_j = f^\alpha_{jk} \circ z_k$. Without loss of generality, one can assume that the $U_j$'s are polydiscs of radius $1$.

<div class="definition">
Let $B$ be a domain in $\Bbb C^m$. A complex analytic family of compact complex manifolds is a family of compact complex manifolds $\{M_t \mid t \in B \}$ such that there is a complex manifold $\mathscr{M}$ of dimension $d$ and a holomorphic map $\pi$ from $\mathscr{M}$ onto $B$ satisfying the following conditions:
<ol>
    <li>
 The rank of the Jacobian of $\pi$ is equal to $m$ at every point of $\mathscr{M}$.
    </li>
    <li>
 For every $t \in B$, the fiber $\pi^{-1}(t)$ is a compact submanifold of $\mathscr{M}$.
    </li>
    <li>
 $\pi^{-1}(t) \cong M_t$ for every $t \in B$.
    </li>
</ol>
</div>

In the above definition, $\mathscr{M}$ is called the total space of the family and $B$ the parameter space. The first condition ensures, utilizing the implicit function theorem, that $\pi^{-1}(t)$ is a closed complex submanifold of $\mathscr{M}$ of dimension $n := d-m$ for each $t \in B$. The second condition just yields that $\pi^{-1}(t)$ are compact complex manifolds and the last condition states that the submanifold $\pi^{-1}(t)$ is biholomorphic to the compact complex manifold $M_t$.

As a set, we have $\mathscr{M} = \bigcup_{t \in B} M_t \times \\{t\\}$. Now, using the implicit function theorem, one constructs local coordinates for $\mathscr{M}$ such that $\\{U_j\\}_{j \in J}$ is a locally finite covering and 

$$
z_j : U_j \to z_j(U_j) \subset \Bbb C^{n+m}
$$

is a holomorphic map with $U_j \ni p \mapsto (z^1_j(p),\dots,z^n_j(p),t^1,\dots,t^m)$, where 

$$
\pi(p) = (t^1,\dots,t^m) = t \in B.
$$

Thus each $z_j$ maps $U_j$ into the product $\Bbb C^n \times B \subset \Bbb C^{n+m}$. The manifold $M_t = \pi^{-1}(t)$ has local coordinates given by $(V_j,z_j)$, where $V_j$ belongs to the open cover $\\{U_j \cap \pi^{-1}(t)\\}$, and $z_j$ is a holomorphic map on $V_j \cap \pi^{-1}(t)$ given by $p \mapsto z_j(p)=(z^1_j(p),\dots,z^n_j(p))$.

The transition functions $f_{jk} = z\_j \circ z^{-1}\_k$ will now also incorporate the parameter $t$ from where we see that the compact complex manifold $M_{t_0}$ for $t_0 \in B$ is obtained by gluing finite number of open sets

$$
z_j(U_j)_{t_0} = \{\pi^{-1}(t_0) \cap z_j(U_j) \mid j \in J\}
$$

of $\Bbb C^n$ via $f_{jk}$.

<div class="definition">
Let $M$ and $N$ be two compact complex manifolds and $B$ a domain in $\Bbb C^n$. $N$ is called a deformation of $M$ if there exists an analytic family $(\mathscr{M}, B, \pi)$ such that $M = \pi^{-1}(t_0)$ and $N = \pi^{-1}(t_1)$, for some $t_0,t_1 \in B$.
</div>

For the notion of equivalence between complex analytic families $(\mathscr{M}, B, \pi_\mathscr{M})$ and $(\mathscr{N}, B, \pi_\mathscr{N})$ we have the following definition.

<div class="definition">
Let $(\mathscr{M}, B, \pi_\mathscr{M})$ and $(\mathscr{N}, B, \pi_\mathscr{N})$ be complex analytic families. Then $(\mathscr{M}, B, \pi_\mathscr{M})$ and $(\mathscr{N}, B, \pi_\mathscr{N})$ are equivalent if there exists a biholomorphic map $F : \mathscr{M} \to \mathscr{N}$ such that for each $t \in B$, $F$ maps $M_t = \pi^{-1}_\mathscr{M}(t)$ biholomorphically to $N_t = \pi^{-1}_\mathscr{N}(t)$.
</div>

Considering the simplest possible choice for $\mathscr{M}$, we give a notion of triviality for these complex analytic families.

<div class="definition">
Let $(\mathscr{M}, B, \pi)$ be a complex analytic family and $M = \pi^{-1}(t_0)$ for a fixed $t_0 \in B$. Then $(\mathscr{M}, B, \pi)$ is called <b>trivial</b> if it is equivalent to $(M \times B, B, \pi)$.
</div>

As you might expect, we also have a notion of local triviality. Before giving you the definition, note that if $I \subset B$ is a subdomain of $B$, then $(\mathscr{M}_I, I, \pi)$ yields a complex analytic family with $\mathscr{M}_I = \pi^{-1}(I)$.

<div class="definition">
A complex analytic family $(\mathscr{M}, B, \pi)$ is said to be <b>locally trivial</b> if, for each $t \in B$, there is a subdomain $I \subset B$ with $t \in I$ such that $(\mathscr{M}_I, I, \pi)$ is trivial.
</div>

If $(\mathscr{M}, B, \pi)$ is a complex analytic family and $f : D \to B$ a holomorphic map of complex manifolds, one can ask can we produce a complex analytic family with $D$ as the base space? In other words, can we perform a "change of parameters"?  The answer to this question is affirmative and the way to proceed is by first considering the pullback $\mathscr{M} \times_B D$ of the diagram

$$
\xymatrix{
 & \mathscr{M} \ar@{->}[d]^{\pi} \\
D \ar@{->}[r]_{h} & B
}
$$

and then consider the image of $\mathscr{M} \times_B D$ under the map

$$
\Pi : \mathscr{M} \times D \to B \times D.
$$

This yields the graph $G_h$ of $h$, which is a submanifold of $B \times D$ and is biholomorphic to $D$ via $p : B \times D \to D$. Since $\pi$ is a holomorphic map with maximal rank, the map $\pi \times \operatorname{id}_D$ is also. It follows that $\mathscr{M} \times_B D = (\pi \times \operatorname{id}_D)^{-1}(G_h)$ obtains a complex submanifold structure of $\mathscr{M} \times B$. The complex analytic family $(\mathscr{M} \times_B D, D, p \circ \Pi)$ is called the induced family or pullback from $(\mathscr{M}, B, \pi)$ via $h$.

The next thing on our agenda is to consider, given a compact complex manifold $M$ that occurs as the fiber over some $t_0 \in B$ of a complex analytic family $(\mathscr{M}, B, \pi)$, for which $t \in B$ the manifold $M_t = \pi^{-1}(t)$ is a deformation of $M$. The following theorem provides an answer to this.

<div class="theorem">
Let $(\mathscr{M}, B, \pi)$ be a complex analytic family of compact complex manifolds and $M_{t_0} = \pi^{-1}(t_0)$ a compact complex manifold for a fixed $t_0 \in B$, obtained by gluing polydiscs $\{U_j\}_{j \in J}$ via the transition maps $f_{jk}$ defined on $U_j \cap U_k \ne \emptyset$. Then there exists a domain $I \subset B$ such that for each $t \in I$, $M_t = \pi^{-1}(t)$ is a compact complex manifold obtained by gluing the same polydiscs $\{U_j\}_{j \in J}$ using different transition maps $f_{jk}(z_k, t)$, with the initial condition $f_{jk}(z_k,t_0) = f_{jk}(z_k)$.
</div>

<div class="proof">
Consider a locally finite open cover $\{U_j\}_{j \in J}$ for $\mathscr{M}$ and local coordinates $\{(U_j,z_j)\}_{j \in J}$ with $z_j(U_j) = V_j \times I_j$, where $V_j$ can be assumed to be a polydisc in $\Bbb C^n$ and $I_j \subset B$ a polydisc in $\Bbb C^m$. Let $\{f_{jk}\}$ be the transition maps that glue the domains $\{V_j \times I_j\}$ to form $\mathscr{M}$. For $t_0 \in B$, $M_{t_0} = \pi^{-1}(t_0)$ is the compact complex manifold obtained by gluing 
$$
\{V_j \times \{t_0\} \cong V_j \mid U_j \cap M_{t_0} \ne \emptyset \}
$$
via the transition maps $\{f_{jk}(z_k,t_0)\}$. Since the fibers of $\pi$ are compact and the cover is locally finite, there exists an open neighborhood $I$ of $t_0 \in B$ that can be identified with a polydisc in $\Bbb C^m$ such that $\pi^{-1}(I)$ is contained in the union of a finite number of $U_j$'s. Set $U'_j = U_j \cap M_{t_0}$. Then by construction, for any $t \in I$ the compact complex manifold $\pi^{-1}(t) = M_t$ is obtained by gluing $\{ V_j \times \{t\} \cong V_j \mid j = 1,\dots,l\}$ via the transition maps $\{f_{jk}(z_k,t)\}$. Hence, the restriction $(\mathscr{M}_I, I, \pi)$ of $(\mathscr{M}, B, \pi)$ to $I$ consists of fibers which are all obtained by gluing the same polydiscs $\{V_1,\dots,V_l\}$ with the transition maps $f_{jk}(z_k,t)$ depending on $t \in I$.
</div>

---

We'll now turn to formalize the thing we've been calling "infinitesimal deformation". For a complex analytic family $(\mathscr{M}, B, \pi)$, we seek to give a meaningful definition for

$$
\dfrac{\partial}{\partial t}M_t.
$$

Meaningful in the sense that $\frac{\partial}{\partial t}M_t \Bigr\|_{t_0} = 0$ if $(\mathscr{M}, B, \pi)$ is locally trivial at $t_0 \in B$. Since a deformation of a compact complex manifold $M$ with a cover $\{U\_j\}$ is given by different gluings with the transition maps $\{f\_{jk}\}$, one would expect the infinitesimal deformation to be determined by the datum of $\left\\{\frac{\partial}{\partial t} f\_{jk}\right\\}$.

Let's begin by looking at what this data gives us with a simple example. Consider $\mathscr{M} = \bigcup_{t \in \Bbb C^\ast} \Bbb CP^1 \times \\{t\\}$ with $\Bbb CP^1 = U_0 \cup U_1$ being covered by $U_0 = \\{[w_0:w_1] \mid w_0 \ne 0\\}$ and $U_1 = \\{[w_0:w_1] \mid w_1 \ne 0\\}$. We have two chart maps given by

$$
\begin{align*}
z_0 : U_0 &\to \Bbb C \\
[w_0 : w_1] &\mapsto t\frac{w_1}{w_0}
\end{align*}
$$

and

$$
\begin{align*}
z_1 : U_1 &\to \Bbb C \\
[w_0 : w_1] &\mapsto t\frac{w_0}{w_1}.
\end{align*}
$$

Now $z^{-1}_0(\lambda) = [1 : \lambda/t]$ and likewise for $z^{-1}_1$. The transition functions are thus given by

$$
f_{01}(z_1,t) = \frac{t^2}{z_1}
$$

and 

$$
f_{10}(z_0,t) = \frac{t^2}{z_0}.
$$

Thus $\frac{\partial f_{01}}{\partial t} = \frac{2t}{z_1} \ne 0$ and $\frac{\partial f_{10}}{\partial t} = \frac{2t}{z_0} \ne 0$. However the coordinates $z_0$ and $z_1$ are clearly compatible with the standard coordinates $z'_0 = \frac{w_1}{w_0}$ and $z'_1 = \frac{w_0}{w_1}$ so $\Bbb CP^1_t \cong \Bbb CP^1$. 

The moral here is that we need something stronger than $\left\\{\frac{\partial}{\partial t} f\_{jk}\right\\}$. Note that the transition maps satisfy

$$
f_{ik}(z_k,t) = f_{ij}(f_{jk}(z_k,t),t)
$$

on $U_i \cap U_j \cap U_k \ne \emptyset$. In more detail we have

$$
f_{ik}^{\alpha }(z_{k},t)=f_{ij}^{\alpha }(f_{jk}^{1}(z_{k},t),\ldots ,f_{jk}^{n}(z_{k},t),t),
$$

for $\alpha = 1,\dots,n$. Now $z^\alpha_j = f^{\alpha}_{jk}(z_k,t)$ so from

$$
{\displaystyle {\begin{aligned}{\frac {\partial f_{ik}^{\alpha }(z_{k},t)}{\partial t}}&={\frac {\partial f_{ij}^{\alpha }(z_{j},t)}{\partial t}}+\sum _{\beta =0}^{n}{\frac {\partial f_{ij}^{\alpha }(z_{j},t)}{\partial f_{jk}^{\beta }(z_{k},t)}}\cdot {\frac {\partial f_{jk}^{\beta }(z_{k},t)}{\partial t}}\\\end{aligned}}}
$$

we obtain

$$
{\displaystyle {\begin{aligned}{\frac {\partial f_{ik}^{\alpha }(z_{k},t)}{\partial t}}&={\frac {\partial f_{ij}^{\alpha }(z_{j},t)}{\partial t}}+\sum _{\beta =0}^{n}{\frac {\partial z_{i}^{\alpha }}{\partial z_{j}^{\beta }}}\cdot {\frac {\partial f_{jk}^{\beta }(z_{k},t)}{\partial t}}\\\end{aligned}}}.
$$

Also 

$$
{\displaystyle {\frac {\partial }{\partial z_{j}^{\beta }}}=\sum _{\alpha =1}^{n}{\frac {\partial z_{i}^{\alpha }}{\partial z_{j}^{\beta }}}\cdot {\frac {\partial }{\partial z_{i}^{\alpha }}}}
$$

and so we obtain the following

$$
{\displaystyle {\begin{aligned}\sum _{\alpha =0}^{n}{\frac {\partial f_{ik}^{\alpha }(z_{k},t)}{\partial t}}{\frac {\partial }{\partial z_{i}^{\alpha }}}=&\sum _{\alpha =0}^{n}{\frac {\partial f_{ij}^{\alpha }(z_{j},t)}{\partial t}}{\frac {\partial }{\partial z_{i}^{\alpha }}}\\&+\sum _{\beta =0}^{n}{\frac {\partial f_{jk}^{\beta }(z_{k},t)}{\partial t}}{\frac {\partial }{\partial z_{j}^{\beta }}.}\\\end{aligned}}}
$$

Then defining

$$
\theta_{ik}(t) = \sum _{\alpha =0}^{n}\frac {\partial f_{ik}^{\alpha }(z_{k},t)}{\partial t}\frac {\partial }{\partial z_{i}^{\alpha }},
$$

the equality becomes

$$
\theta_{ik}(t) = \theta_{ij}(t) + \theta_{jk}(t).
$$

Note that $\theta_{jk}(t) - \theta_{ik}(t) + \theta_{ij}(t) = 0$ and for $i = k$ since $f^\alpha_{kk} = z^\alpha_k$, we have that $\theta_{kk}(t) = 0$ as well as $\theta_{kj}(t) = -\theta_{jk}(t)$. It follows that $\{\theta_{jk}(t)\}$ forms a $1$-cocycle. Let $T_{M_t}$ be the sheaf of holomorphic vector fields on $M_t$, then

$$
\theta_{jk}(t) \in \Gamma(U_j \cap U_k, T_{M_t}).
$$

So $\{\theta_{jk}(t)\} \in Z^1(\mathcal{U}_t, T\_{M_t})$, where $\mathcal{U}_t = \{U_j\}$ is the covering $M_t = \bigcup U_j$. We denote the corresponding cohomology class $\theta(t) \in H^1(\mathcal{U}_t,T\_{M_t}) \subset H^1(M_t,T\_{M_t})$. We call $\theta(t)$ the <i>infinitesimal deformation</i> of $M_t$ and denote it by

$$
\frac{\partial}{\partial t} M_t := \theta(t).
$$

There are a few things we need to check here. The first question arising is that is $\frac{\partial}{\partial t} M_t$ independent of the choice of local data?

<div class="proposition">
The infinitesimal deformation $\frac{\partial}{\partial t} M_t$ independent of the choice of local coordinates.
</div>

<div class="proof">
First, fix a complex analytic family $(\mathscr{M}, B, \pi)$ with of local coordinates $\left(U_{i}, z_{i}\right)_{i \in I}$, we show that $\theta(t)$ does not change if we consider a refinement of the open covering $\mathcal{U}=\left\{U_{i}\right\}_{i \in I}$ of $\mathscr{M}$. Let $\mathcal{V}=\left\{V_{j}\right\}_{j \in J}$ be any refinement of $\mathcal{U}=\left\{U_{i}\right\}_{i \in I}$, such that $V_{j} \subset U_{i(j)}$ for all $j \in J$. Let $z_{j}^{\prime}: V_{j} \longrightarrow \mathbb{C}^{n}$ be a local coordinate defined on $V_{j}$ for each $j \in J$, which is the restriction of the local coordinate $z_{i(j)}: U_{i(j)} \longrightarrow \mathbb{C}^{n}$. Thus the holomorphic vector field $\theta_{j k}^{\prime}(t)$ is the restriction of $\theta_{i(j) i(k)}(t)$ to $V_{j} \cap V_{k} \cap M_t$. In fact, setting $\mathcal{B}_{t}=\left\{V_{j t}\right\}_{j \in J}$ where $V_{j t}=V_{j} \cap M_t \neq \emptyset$, we have

$$
\theta_{j k}^{\prime}(t)=\theta_{i(j) i(k)}^{\prime}(t)_{\mid V}, \quad V=V_{j t} \cap V_{k t}
$$

Hence the 1-cocycles $\left\{\theta_{j k}(t)\right\} \in Z^{1}(\mathcal{U}, T_{M_t})$ and $\left\{\theta_{j k}^{\prime}(t)\right\} \in Z^{1}(\mathcal{V}, T_{M_t})$ satisfy 

$$
\left\{\theta_{j k}^{\prime}(t)\right\}=\Pi_{\mathfrak{B}_{t}}^{\mathcal{U}_{t}}\left(\left\{\theta_{j k}(t)\right\}\right).
$$

Now, we consider two sets of local coordinates $\left(V_{l}, z_{l}\right)_{l \in L}$ and $\left(V_{\lambda}^{\prime}, z_{\lambda}^{\prime}\right)_{\lambda \in \Lambda}$. Since two locally finite coverings have a common refinement and since $\theta(t)$ does not depend on the choice of refinement, we can work with local coordinates $\left(U_{i}, z_{i}\right)_{i \in I}$ consisting of open subsets belonging to a refinement of both $\left\{V_{l}\right\}_{l \in L}$ and $\left\{V_{\lambda}^{\prime}\right\}_{l \in \Lambda}$, as well as the restrictions of the local coordinates $z_{l}$ and $z_{\lambda}^{\prime}$ to those open subsets.

Therefore given $z_{i}$ and $w_{i}$ defined on each $U_{i}$, we want to show that the infinitesimal deformation $\eta(t)$ defined with respect to $w_{i}$ coincides with $\theta(t)$. That is, on intersections, $\{\theta_{jk}(t)\} -\{\eta_{jk}(t)\}$ is a coboundary. If $h_{j k}: w_{k} \longmapsto w_{j}$ are transition maps for the local coordinates $\left\{w_{i}\right\}$, then we obtain the holomorphic vector field

$$
\begin{equation*}
\eta_{j k}(t)=\sum_{\beta=1}^{n} \frac{\partial h_{j k}^{\beta}\left(w_{k}, t\right)}{\partial t} \frac{\partial}{\partial w_{j}^{\beta}}, \quad w_{k}=h_{k j}\left(w_{j}, t\right)
\end{equation*}
$$

Consider now the cohomology class $\eta(t) \in H^1(M_t, T_{M_t})$ corresponding to the cocycle $\{\eta_{jk}(t)\} \in Z^1(\mathcal{U}_t, T_{M_t})$. For a holomorphic function $g^\alpha_j$ on the variables $z^1_j,\dots,z^n_j,t$ we have that $w^\alpha_j = g^\alpha_j(z_j,t)$. Since

$$
g_{j}^{\alpha}\left(z_{j}, t\right)=w_{j}^{\alpha}=h_{j k}^{\alpha}\left(w_{k}, t\right)=h_{j k}^{\alpha}\left(g_{k}\left(z_{k}, t\right), t\right)
$$


and $z_{j}=f_{j k}\left(z_{k}, t\right)$, we obtain

$$
\begin{equation*}
g_{j}^{\alpha}\left(f_{j k}\left(z_{k}, t\right), t\right)=h_{j k}^{\alpha}\left(g_{k}\left(z_{k}, t\right), t\right)
\end{equation*}
$$

on $U_{j} \cap U_{k} \neq \emptyset$. Differentiating this with respect to $t$ yields

$$
\sum_{\beta=1}^{n} \frac{\partial g_{j}^{\alpha}}{\partial z_{j}^{\beta}} \frac{\partial f_{j k}^{\beta}}{\partial t}+\frac{\partial g_{j}^{\alpha}}{\partial t}=\sum_{\beta=1}^{n} \frac{\partial h_{j k}^{\alpha}}{\partial w_{k}^{\beta}} \frac{\partial g_{k}^{\beta}}{\partial t}+\frac{\partial h_{j k}^{\alpha}}{\partial t}
$$

i.e.,

$$
\sum_{\beta=1}^{n} \frac{\partial g_{j}^{\alpha}}{\partial t}+\frac{\partial w_{j}^{\alpha}}{\partial z_{j}^{\beta}} \frac{\partial f_{j k}^{\beta}}{\partial t}=\sum_{\beta=1}^{n} \frac{\partial w_{j}^{\alpha}}{\partial w_{k}^{\beta}} \frac{\partial g_{k}^{\beta}}{\partial t}+\frac{\partial h_{j k}^{\alpha}}{\partial t}.
$$

Multiplying by $\frac{\partial}{\partial w_{j}^{\alpha}}$ from the right and taking the summation $\sum_{\alpha=1}^{n}$, we furthermore obtain the following equality

$$
\sum_{\beta=1}^{n} \frac{\partial f_{j k}^{\beta}}{\partial t} \frac{\partial}{\partial z_{j}^{\beta}}+\sum_{\alpha=1}^{n} \frac{\partial g_{j}^{\alpha}}{\partial t} \frac{\partial}{\partial w_{j}^{\alpha}}=\sum_{\beta=1}^{n} \frac{\partial g_{k}^{\beta}}{\partial t} \frac{\partial}{\partial w_{k}^{\beta}}+\sum_{\alpha=1}^{n} \frac{\partial h_{j k}^{\alpha}}{\partial t} \frac{\partial}{\partial w_{j}^{\alpha}}
$$

where we use the equalities

$$
\frac{\partial}{\partial z_{j}^{\beta}}=\sum_{\alpha=1}^{n} \frac{\partial w_{j}^{\alpha}}{\partial z_{j}^{\beta}} \frac{\partial}{\partial w_{j}^{\alpha}}
$$

and

$$
\frac{\partial}{\partial w_{k}^{\beta}}=\sum_{\alpha=1}^{n} \frac{\partial w_{j}^{\alpha}}{\partial w_{k}^{\beta}} \frac{\partial}{\partial w_{j}^{\alpha}}.
$$

Now setting $\theta_{j}(t)=\sum_{\alpha=1}^{n} \frac{\partial g_{j}^{\alpha}\left(z_{j}, t\right)}{\partial t} \frac{\partial}{\partial w_{j}^{\alpha}}, w_{j}^{\alpha}=g_{j}^{\alpha}\left(z_{j}, t\right)$, we have

$$
\begin{equation*}
\theta_{j k}(t)-\eta_{j k}(t)=\theta_{k}(t)-\theta_{j}(t).
\end{equation*}
$$

Since $\theta_{j}(t)$ is a holomorphic vector field on $U_{j t}=U_{j} \cap M_{t}$, there exists a coboundary $\left\{\theta_{j}(t)\right\} \in C^{0}\left(\mathcal{U}_{t}, \Theta_{t}\right)$, moreover we obtain

$$
\left\{\theta_{j k}(t)\right\}-\left\{\eta_{j k}(t)\right\}=\delta\left(\left\{\theta_{j}(t)\right\}\right),
$$

where $\left\{\theta_{j k}(t)\right\} \in Z^{1}\left(\mathcal{U}_{t}, \Theta_{t}\right)$. Therefore $\eta(t)$ coincides with $\theta(t)$, and the infinitesimal deformation $\frac{\partial}{\partial t} M_t$ does not depend on the choice of local coordinates.

</div>

<div class="proposition">
If $(\mathscr{M}, B, \pi)$ is locally trivial, then 
$$
\frac{\partial}{\partial t} M_t = 0.
$$
</div>

<div class="proof">
Suppose that $(\mathscr{M}, B, \pi)$ is locally trivial. Then there exists an open set $I \subset B$ such that $(\mathscr{M}_I, I, \pi)$ is equivalent to $(M \times B, B, \pi)$, where $M = \pi^{-1}(t_0)$ for a fixed $t_0 \in B$. Let $\{w_j\}_{j \in J}$ be local coordinates of $M$. since $\frac{\partial}{\partial t} M_t$ does not depend on the chosen local coordinates, we can construct $\theta(t)$ for $t \in I$ in terms of the local coordinates $\{u_j\}$ given by $u_j = (w_j,t)$ of $M \times I$. Let $h_{jk}$ be the transition map

$$
(w_j, t) \mapsto (w_k,t) = (h_{jk}(w_k),t).
$$

Since $h_{jk}$ is independent of $t$, we have

$$
\theta_{jk}(t) = \sum_{\beta=1}^n \frac{\partial h^\beta_{jk}(w_k)}{\partial t} \frac{\partial}{\partial u^\beta_j} = 0.
$$

Thus $\frac{\partial}{\partial t} M_t = 0$.

</div>

Referring back to our example on the projective space $\mathscr{M} = \bigcup_{t \in \Bbb C^\ast} \Bbb CP^1 \times \\{t\\}$, we obtained $\frac{\partial f_{01}}{\partial t} = \frac{2t}{z_1}$. This gives

$$
\theta_{01}(t) = \frac{2t}{z_1}\frac{\partial}{\partial z_0}.
$$

Note that $\frac{\partial z_0}{\partial z_1} = -\frac{t^2}{z^2_1}$ since on $U_0 \cap U_1$ we have $z_0 = \frac{t^2}{z_1}$. Also  

$$
\frac{\partial}{\partial z_0} = \frac{\partial z_1}{\partial z_0}\frac{\partial}{\partial z_1} = -\frac{z^2_1}{t^2}\frac{\partial}{\partial z_1}
$$ 

on the intersection. Hence

$$
\begin{align*}
\theta_{01}(t) &= 2 \frac{z_0}{t}\frac{\partial}{\partial z_0} \\
&= - 2 \frac{z_1}{t}\frac{\partial}{\partial z_1} \\
&= \frac{z_0}{t}\frac{\partial}{\partial z_0} - \frac{z_1}{t}\frac{\partial}{\partial z_1},
\end{align*}
$$

and so $\theta_{01}(t)$ is a coboundary $\theta_{01}(t) = \theta_0(t) - \theta_1(t)$ where $\theta_i(t) = \frac{z_i}{t}\frac{\partial}{\partial z_i}$. The converse of the previous proposition is not in general true without forcing an additional condition on the dimension of $H^1(M_t, T_{M_t})$.

<div class="proposition">
Let $(\mathscr{M}, B, \pi)$ be a complex analytic family and $M = \pi^{-1}(t_0)$ for some $t_0 \in B$. If $\dim H^1(M_t, T_{M_t})$ does not depend on $t$ and
$$
\frac{\partial}{\partial t}M_t \equiv 0,
$$
then $(\mathscr{M}, B, \pi)$ is locally trivial.
</div>

To sum up the above discussions, I'll now give you the definition of the famous Kodaira-Spencer map that one encounters more often than not when working on deformation theory.

<div class="definition">
The $\Bbb C$-linear map 
$$
\begin{align*}
\rho_t : T_t B &\to H^1(M_t, T_{M_t}) \\
\frac{\partial}{\partial t} &\mapsto \frac{\partial}{\partial t}M_t
\end{align*}
$$
is called the <b>Kodaira-Spencer</b> map at $t \in B$ for the complex analytic family $(\mathscr{M}, B, \pi)$.
</div>

---

For a slightly different viewpoint, let $X$ be a compact analytic space (or a complete scheme). A deformation of $X$ parameterized by a pointed analytic space (pointed scheme) $(Y,y_0)$ is a proper flat morphism

$$
\varphi : \mathscr{X} \to (Y, y_0)
$$

plus a given isomorphism between $X$ and the fiber $\varphi^{-1}(y_0)$. A morphism of deformations between $\varphi : \mathscr{X} \to (Y,y_0)$ and $\varphi' : \mathscr{X}' \to (Y',y'_0)$ is a cartesian diagram

$$
\xymatrix{
\mathscr{X} \ar@{->}[d]_{\varphi} \ar@{->}[r]^{\alpha} & \mathscr{X}' \ar@{->}[d]^{\varphi'} \\
(Y,y_0) \ar@{->}[r]^{\beta} & (Y',y'_0)
}
$$

where $\alpha$ and $\beta$ are morphisms inducing the identity on $X$. Now an infinitesimal deformation of $X$ is simply a deformation of $X$ parameterized by $\operatorname{Spec}\Bbb C[\varepsilon]$. Again, $X$ is given by the transition data $\\{U_i,z_i,f_{ij}(z_j)\\}$. The total space $\mathscr{X}$ of an infinitesimal deformation $\varphi : \mathscr{X} \to \operatorname{Spec}\Bbb C[\varepsilon]$ of $X$ may be thought of as being given by gluing $U_i \times \operatorname{Spec}\Bbb C[\varepsilon]$ via the identifications

$$
z_i = \widetilde{f}_{ij}(z_j,\varepsilon) = f_{ij}(z_j) + \varepsilon b_{ij}(z_j),
$$

while $\varphi$ is given locally by $\varphi(z_i,\varepsilon) = \varepsilon$. These $\widetilde{f}_{ij}$ also have to satisfy the cocycle rule 

$$
\widetilde{f}_{ij}(\widetilde{f}_{jk}(z_k,\varepsilon),\varepsilon) = \widetilde{f}_{ik}(z_k,\varepsilon),
$$

which gives

$$
\widetilde{f}_{ik}(z_k,\varepsilon) = f_{ij}(f_{jk}(z_k) + \varepsilon b_{jk}(z_k)) + \varepsilon b_{ij}(f_{jk}(z_k) + \varepsilon b_{jk}(z_k)).
$$

Since the dual numbers satisfy $g(a+b\varepsilon )=g(a)+\varepsilon g'(a)b$ we obtain

$$
f_{ij}(f_{jk}(z_k) + \varepsilon b_{jk}(z_k)) = f_{ij}(f_{jk}(z_k)) + \varepsilon \frac{\partial f_{ij}(z_i)}{\partial z_i}b_{jk}(z_k)
$$

and

$$
\begin{align*}
\varepsilon b_{ij}(f_{jk}(z_k) + \varepsilon b_{jk}(z_k)) &= \varepsilon b_{ij}(f_{jk}(z_k)) + \varepsilon^2\frac{\partial b_{ij}(z_i)}{\partial z_i}b_{jk}(z_k)\\
&= \varepsilon b_{ij}(f_{jk}(z_k)) \\
&= \varepsilon b_{ij}(z_j).
\end{align*}
$$

Hence the cocycle condition on $\widetilde{f}\_{ij}$ reduces to the cocycle condition on $f\_{ij}$ plus $b\_{ik} = \frac{\partial f\_{ij}}{\partial z\_j}b_{jk} + b_{ij}$. One can then form $\theta_{ij} = \sum_{\alpha = 1}^n b^\alpha_{ij}\frac{\partial}{\partial z^\alpha_i}$ and see that the $1$-cochain $\theta = \{\theta_{ij}\} \in C^1(\mathcal{U}, T_X)$ is a cocycle. The class

$$
[\theta] \in H^1(X, T_X)
$$
 
defines the Kodaira-Spencer class. Note that there is an exact sequence of sheaves of $\mathcal{O}_X$-modules 

$$
0 \longrightarrow T_X \longrightarrow T_{\mathscr{X}} \longrightarrow \varphi^\ast T_{\operatorname{Spec}\Bbb C[\varepsilon]} \longrightarrow 0.
$$

Passing this to the cohomology sequence one obtains the Kodaira-Spencer class as the coboundary of

$$
\varphi^\ast\left(\frac{\partial}{\partial \varepsilon}\right) \in H^0(X, T_{\operatorname{Spec}\Bbb C[\varepsilon]} ).
$$

Hence $[\theta]$ depends only on the equivalence class of the first-order deformation $\mathscr{X} \to \operatorname{Spec}\Bbb C[\varepsilon]$.

Much more can be said about the theory, but I have other things that I need to focus on for now so we'll leave this here for now and maybe come back to it later on.
