---
layout: post
title: "The Moduli Space of Curves"
categories: [Complex Geometry, Algebraic Geometry]
mathjax: true
published: false
excerpt_separator: <!--more-->
---

This is going to serve as a preliminary for an upcoming post on curve counting on Calabi–Yau $3$-folds. We will cover fine and coarse moduli spaces in general and then focus on curves. Finally, we'll look at some examples.

<!--more-->

---

The idea behind what we are trying to do is, of course, trying to classify algebro-geometric objects. In our case, the objects of interest will be curves. The word classify is relatively vague, as it can mean different things depending on the context. As a simple example to illustrate this, recall from linear algebra that finite-dimensional vector spaces are classified by their dimension: any two vector spaces of the same dimension over a given field are isomorphic. The map

$$
\begin{align*}
\{ V \mid V \text{ is a vector space over } k \}/\operatorname{\sim} &\to \{0,1,2,\dots\} \\
[V] &\mapsto \dim V
\end{align*}
$$

therefore classifies vector spaces up to isomorphism. The intuition here is that the left-hand side is a difficult space to study, but the right-hand side (the natural numbers) are something we understand very well. This kind of phenomena is what we are after in the case of algebraic curves as well. By a <i>variety</i>, we mean an integral, separated scheme of finite type over $\Bbb C$ and a <i>curve</i> is a variety of dimension $1$. We will begin this by considering the set

$$
\mathcal{M} = \{C \mid V \text{ is a smooth, irreducible, complex projective curve }\}/\operatorname{\sim}.
$$

We require $C$ to be smooth to avoid complications arising from singularities. Under this assumption, irreducibility is equivalent to connectedness. Moreover, every smooth, irreducible curve can be embedded into a smooth, irreducible, and projective curve, which justifies our focus on projective curves. 

Recall now that the <i>genus</i> of a curve $C \in \mathcal{M}$ is defined by 

$$
g(C) = \dim H^1(C, \mathcal{O}_C),
$$

or equivalently by $g(C) = H^0(C, \Omega^1_C)$ via Serre duality. This gives a well-defined map

$$
\begin{align*}
\mathcal{M} &\to \{0,1,2,\dots\} \\
[C] &\mapsto g(C).
\end{align*}
$$

For a $g \in \{0,1,2\dots\}$, we will define $\mathcal{M}_g$ to be the preimage of the above map. 

<div class="proposition">
If $C$ is a projective non-singular curve of genus $0$, then $C$ is isomorphic to $\Bbb P^1$.
</div>

<div class="proof">
Pick any $p \in C$ and consider the line bundle $\mathcal{O}(p)$. Since $\deg(\mathcal{O}(p)) = 1$, Riemann–Roch gives

$$
h^0(C, \mathcal{O}(p)) - h^1(C,\mathcal{O}(p)) = \deg(\mathcal{O}(p)) + 1 - g = 2.
$$

Now $H^1(C,\mathcal{O}(p)) \cong H^0(C, \mathcal{O}(p) \otimes K_C)^\ast$ by Serre duality and since

$$
\deg(K_C) = 2g-2 = -2,
$$

we have

$$
\deg(\mathcal{O}(p) \otimes K_C) = 1 - 2 -1 < 0.
$$

That is, $h^0(C,\mathcal{O}(p) \otimes K_C) = 0$ so $h^1(C,\mathcal{O}(p)) = 0$ which gives

$$
h^0(C, \mathcal{O}(p)) = 2.
$$

Choosing a basis $\{1,f\}$ for $H^0(C, \mathcal{O}(p))$ provides us with a nonconstant meromorphic function $f$ that has at most a simple pole at $p$. The map

$$
\begin{align*}
\varphi : C &\to \Bbb P^1 \\
x &\mapsto [1:f(x)]
\end{align*}
$$

is then well-defined and nonconstant. Since $C$ is smooth, projective, and of genus $0$, any non-constant map to $\Bbb P^1$ must be a degree one map, hence birational. We conclude as on smooth projective curves, birational maps are isomorphisms.
</div>

The proposition above gives us $\mathcal{M}_0$ as the set with only one element, namely $[\Bbb P^1]$. The situation gets already more complicated for $g = 1$. For each $t \in \Bbb C$, consider the family 

$$
C_t = \{[x:y:z]\in \Bbb P^2 \mid y^2z + x(x-z)(x-tz) = 0\},
$$

of plane cubics. It turns out that every smooth, irreducible complex projective curve $C$ of genus $1$ is isomorphic to one of the curves $C_t$ for $t \in \Bbb C \setminus \\{0,1\\}$. Moreover, $C_{t_1} \cong C_{t_2}$ if and only if $t_2$ is given by any one of

$$
\left\{t_1,\frac{1}{t_1},1-t_1,\frac{1}{1-t_1}, \frac{t_1-1}{t_1}, \frac{t_1}{t_1-1}\right\} \tag{1}.
$$

Note that for $t \in \Bbb C \setminus \\{0,1\\}$ the topological spaces $C_t(\Bbb C)$ of complex points of $C_t$ are all isomorphic to the tori $S^1 \times S^1$ and hence independent of $t$, but it turns out that the algebraic curves $C_t$ are not all isomorphic. $\mathcal{M}_1$ turns out to consist of uncountably many isomorphism classes and this holds true also for each $g \ge 2$. However, stating that, for example, $\mathcal{M}_1$ is just an infinite set is not very informative and we can seek to obtain more structure. 

Now, even though every genus $1$ curve can be realized as one of the curves $C_t$ with $t \in U := \Bbb C \setminus \\{0,1\\}$ the correspondence is not one-to-one, different values of $t$ in the set given by $(1)$ yield curves that are isomorphic to each other. To get rid of this redundancy, we quotient out these multiple parameters that give the same isomorphism class of curves. We will define an $S_3$ action on $U$ by setting

$$
(12)\cdot t = \frac{1}{t}, \quad (23)\cdot t = 1-t,
$$

for the generators $(12)$ and $(23)$ of $S_3$. This yields an identification of $\mathcal{M}_1$ with the orbit space $U/S_3$.

