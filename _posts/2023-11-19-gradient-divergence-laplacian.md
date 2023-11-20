---
layout: post
title: "Gradient, Divergence and the Laplacian"
published: false
categories: [Differential Geometry, Riemannian Geometry]
mathjax: true
---

I'm currently tasked to give a short presentation about the Bochner Technique and I thought that it would probably be beneficial to track my thoughts prior to the presentation. As you might now the Bochner Technique is a way to relate the Laplacian to the curvature tensor. Before this, however we need to understand what the gradient, divergence and Laplacian are on a Riemannian manifold. This is going to be the topic for this post. 

For the remaining of this post $(M,g)$ is a Riemannian $n$-manifold.

Let's begin with the gradient. Notation wise the gradient of a smooth function $f \in C^\infty(M)$ is denoted either via $\nabla f$ or $\operatorname{grad} f$. I will most likely end up using both since the former is more convenient to write, but since it might result in confusion with the symbol we use for connections in some cases I might resort to the latter. 

So, the definition then. 

<div class="definition">
Let $f \in C^\infty(M)$. The <b>gradient</b> $\nabla f$ of $f$ is defined to be the smooth vector field such that
$$
g(\nabla f, X) = Xf = df(X)
$$
for all $X \in \Gamma(TM)$.
</div>

Astute readers may recognize a similarity here to the musical operator $\sharp$, and they would be correct. Indeed, we have the following relationship:

$$
\nabla f = df^\sharp.
$$

For those unfamiliar with musical isomorphisms, here is a brief explanation. In linear algebra, one learns that a finite-dimensional vector space $V$ is isomorphic to its dual space $V^\ast$. However, this isomorphism is not <i>canonical</i>. This means that to describe the isomorphism, one must first fix a basis for $V$, from which a corresponding dual basis for $V^\ast$ can be derived. Nevertheless, if the vector space $V$ has additional structure, such as a non-degenerate bilinear form $g: V \times V \to \mathbb{R}$, a canonical isomorphism from $V$ to $V^\ast$ can be defined. This isomorphism is given by:

$$
\begin{align*}
    &\flat : V \to V^\ast \\
    &v^\flat = g(v,-).
\end{align*}
$$

To see why it is an isomorphism note that the non-degeneracy of $g$ implies that 

$$
v^\flat = 0 \iff g(v,-) = 0  \implies v = 0
$$

so $\flat$ is injective. Since $V$ and $V^\ast$ are of the same dimension $\flat$ is also surjective. The inverse is denoted by $\sharp : V^\ast \to V$. 

Since $M$ is equipped with a Riemannian metric we have the same construction for each $T_pM$. Generalizing this we define $\flat : TM \to T^\ast M$ by $X^\flat = g(X,-)$ with an inverse $\sharp : T^\ast M \to TM$.

Given a frame $(e_i)$ and a coframe $(\varepsilon^i)$, then we have the following coordinate expressions: