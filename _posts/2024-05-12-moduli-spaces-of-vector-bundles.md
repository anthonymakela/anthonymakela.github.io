---
layout: post
title: "Moduli Spaces of Holomorphic Structures"
categories: [Complex Geometry, Differential Geometry]
mathjax: true
published: false
excerpt_separator: <!--more-->
---

I've recently been thinking about Higgs Bundles and their moduli spaces. Before diving into that topic, I'd like to start with a discussion on the moduli spaces of holomorphic structures and look at the moduli spaces of specific types of bundles we've previously explored.

<!--more-->

I know that I have not been talking about moduli spaces or moduli problems on the blog before, and I won't be getting into the nitty-gritty details here either. The basic premise is that one wants to classify geometric objects by organizing them into a collection and hoping that this collection can be given the structure of a geometric space itself. The simplest example is the real projective line $\Bbb R P^1$. One begins with the question of classifying lines passing through the origin in $\Bbb R^2$ and finds out that for each line $L$, we can assign a parameter $\theta_L \in [0,\pi)$. The collection of lines parametrized like this is exactly $\Bbb R P^1$.

Let's take a slightly different viewpoint on the previous example in terms of groups and their actions. Consider $\Bbb R^2 \setminus \\{0\\}$ and the group $\Bbb R^\ast$. This group acts on $\Bbb R^2 \setminus \\{0\\}$ by $(\lambda,v) \mapsto \lambda v$ and the orbit of a point $(x,y) \in \Bbb R^2 \setminus \\{0\\}$ consists of points $(\lambda x,\lambda y)$ for $\lambda \in \Bbb R^\ast$. I.e. a line through the origin. One obtains the moduli space $\Bbb RP^1$ as the quotient of this action. There is much more to be said about moduli spaces in a more algebro-geometric context, but we won't be going into that today.

---

To set up shop, let $E$ be a complex vector bundle of rank $r$ over a complex manifold $M$ and denote the group of smooth bundle automorphisms of $E$ by $\mathrm{GL}(E)$. The following propositions will serve as our guiding light towards the definition for the moduli space in question.

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

which we will call the <b>moduli space of holomorphic structures</b> in $E$. Unfortunately, there is a slight problem with this definition. The space we are considering is in general non-Hausdorff. The way to resolve this is to consider (semi-)stable bundles.

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

---

We'll now look into something called <b>infinitesimal deformations</b> or "tangent spaces" to these moduli spaces. Recall from <a href="https://anthonymakela.com/complex%20geometry/differential%20geometry/2024/05/03/infinitesimal-deformations-and-the-kodaira-spencer-map.html" style="color:#680530; text-decoration: underline;">Infinitesimal Deformations and The Kodaira-Spencer Map</a> that we should be expecting a space we can identify with $H^{0,1}(M, \operatorname{End}(E, \nabla^{0,1}))$.

Consider perturbing $\nabla^{0,1}$ by $\alpha^{0,1}_t \in \Omega^{0,1}(\operatorname{End}(E))$ for some small $t$ such that

$$
\nabla^{0,1}_t = \nabla^{0,1} + \alpha^{0,1}_t
$$

and $\alpha^{0,1}_0 = 0$. Then for any section $s$ we have

$$
\begin{align*}
0 &= \nabla^{0,1}_t(\nabla^{0,1}_t(s)) \\
&= \nabla^{0,1}_t(\nabla^{0,1}s + \alpha^{0,1}_t s) \\
&= \nabla^{0,1}_t(\nabla^{0,1}s) + \nabla^{0,1}_t(\alpha^{0,1}_t s) \\
&= \nabla^{0,1}(\nabla^{0,1}s) + \alpha^{0,1}_t(\nabla^{0,1}s) + \nabla^{0,1}(\alpha^{0,1}_t s) + \alpha^{0,1}_t(\alpha^{0,1}_t s) \\
&= \alpha^{0,1}_t(\nabla^{0,1}s) + \nabla^{0,1}(\alpha^{0,1}_t s) + (\alpha^{0,1}_t \wedge \alpha^{0,1}_t)s \\
&= (\nabla^{0,1}\alpha^{0,1}_t)s + (\alpha^{0,1}_t \wedge \alpha^{0,1}_t)s.
\end{align*}
$$

Hence $\nabla^{0,1}\alpha^{0,1}_t + \alpha^{0,1}_t \wedge \alpha^{0,1}_t = 0$. Now differentiating this with respect to $t$ we obtain

$$
\nabla^{0,1}\left(\frac{\partial}{\partial t} \alpha^{0,1}_t\right) + \frac{\partial}{\partial t} \alpha^{0,1}_t \wedge \alpha^{0,1}_t + \alpha^{0,1}_t \wedge \frac{\partial}{\partial t} \alpha^{0,1}_t = 0.
$$

At $t = 0$ we have $\alpha^{0,1}_t = \alpha^{0,1}_0 = 0$ so this yields

$$
\nabla^{0,1}\left(\alpha^{0,1}\right) = 0,
$$

where $\alpha^{0,1} = \frac{\partial}{\partial t} \alpha^{0,1}_t \Big\vert\_{t=0}$. If $\nabla^{0,1}_t$ is obtained by a gauge transformation

$$
\nabla^{0,1}_t = f^{-1}_t \circ \nabla^{0,1} \circ f_t,
$$

where $f_t \in \mathrm{GL}(E)$ and $f_0 = \operatorname{id}_E$, then for $s \in \Omega^0(E)$

$$
\begin{align*}
\nabla^{0,1}_t(s) &= f^{-1}_t(\nabla^{0,1}(f_t(s))) \\
&= \nabla^{0,1} s + (f^{-1}_t \bar{\partial} f_t)s. 
\end{align*}
$$

Setting $\alpha^{0,1}_t = f^{-1}_t \bar{\partial}f_t$ and $\alpha^{0,1} = \frac{\partial}{\partial t} \alpha^{0,1}_t \Big\vert\_{t=0}$ we have

$$
\alpha^{0,1} = \nabla^{0,1}f,
$$

where $f = \frac{\partial}{\partial t} f_t \Big\vert\_{t=0}$. It follows that the infinitesimal deformations are given by

$$
H^{0,1}(M, \operatorname{End}(E,\nabla^{0,1})) = \frac{\{\alpha^{0,1} \in \Omega^{0,1}(\operatorname{End}(E) \mid \nabla^{0,1}\alpha^{0,1} = 0\}}{\{\nabla^{0,1}f \mid f \in \Omega^0(E)\}}
$$

provided that $\mathscr{H}^{0,1}(E)/\mathrm{GL}(E)$ is a manifold.

Suppose now that $M$ is a compact Kähler manifold. Then, given an Hermite-Einstein connection $\nabla \in \mathscr{E}(E,h)$ in $E$, we'll determine the tangent space of $\mathscr{E}(E,h)/\mathrm{U}(E,h)$ at $\nabla$. Consider

$$
\nabla_t = \nabla + \alpha_t,
$$

where $\alpha_t \in \Omega^1(\operatorname{End}(E,h))$ and $\alpha_0 = 0$.