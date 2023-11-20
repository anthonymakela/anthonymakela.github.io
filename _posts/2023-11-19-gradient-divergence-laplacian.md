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

Given a frame $(e_i)$ and a coframe $(\varepsilon^i)$ we can express the metric as $g = g_{ij} \varepsilon^i \otimes \varepsilon^j$. For $X = X^ie_i$ we get the following coordinate expression 

$$
\begin{align*}
X^\flat &= g\left(X,-\right) \\
&= \left(g_{ij}X^i\right)\varepsilon^j.
\end{align*}
$$

Now since the matrix $[g_{ij}]$ is invertible the matrix for $\sharp$ is given by the inverse matrix $[g^{ij}]$. For $\omega = \omega_j\varepsilon^j$ we have

$$
\begin{align*}
\omega^\sharp &= \left(g^{ij}\omega_j\right)e_i.
\end{align*}
$$

Note that if the frames are orthonormal, then[^1] $X^\flat = \left(g_{ij}X^i\right)\varepsilon^j = X^j\varepsilon^j$ and likewise $\omega^\sharp = \left(g^{ij}\omega_j\right)e_i = \omega_ie_i$ which should justify the names "flat" and "sharp".

Since the sharp operator satisfies the following:

$$
g(\omega^\sharp, X) = \left(\omega^\sharp\right)^\flat(X) = \omega(X)
$$

for any $\omega \in \Gamma(T^\ast M)$ and $X \in \Gamma(TM)$ it should be clear why $\nabla f = df^\sharp$. Given this, it's a simple matter to find a local expression for the gradient. We have that

$$
\nabla f = df^\sharp = (\partial_i f dx^i)^\sharp = \left(g^{ij}\partial_i f\right) \partial_j.
$$

On a Riemannian manifold, the gradient can be understood similarly to its Euclidean counterpart: it points in the direction where the function $f$ increases most rapidly and stands perpendicular to the level sets of $f$.

What about the divergence? This one is slightly more trickier to describe, but after we've done the hard work we are rewarded by the simplicity of describing the Laplacian using the gradient and divergence.

There are two equivalent ways to define the divergence, we will start with the slightly more abstract one and show later that it's equivalent to the simpler description.

<div class="definition">
Let $X \in \Gamma(TM)$ and denote by $\nabla$ the Levi-Civita connection on $M$. The divergence of $X$ is given by 
$$
\operatorname{div}(X) = \operatorname{tr}(Y \longmapsto \nabla_Y X).
$$
</div>

Let's take a moment to understand this definition. The right-hand side of the equality is the trace of the linear map $\nabla X : \Gamma(TM) \to \Gamma(TM)$ which by our discussions in the post <a href="https://anthonymakela.com/differential%20geometry/2023/09/07/tensor-characterization-lemma.html" style="color:#680530; text-decoration: underline;">Tensor Characterization Lemma</a> can be viewed as a $(1,1)$-tensor field.

You might remember from your vector analysis class that the divergence of a vector field $F = (F_1,F_2,F_3  ) : \Bbb R^3 \to \Bbb R^3$ is defined by

$$
\nabla \cdot F = {\partial F_1\over\partial x}+{\partial F_2\over\partial y}+{\partial F_3\over\partial z}.
$$

If stare at this for a while you might realize that this is exactly the trace of the Jacobian

$$
J = \begin{bmatrix}\frac{\partial F_1}{\partial x}&\frac{\partial F_1}{\partial y}&\frac{\partial F_1}{\partial z}\\ \frac{\partial F_2}{\partial x}&\frac{\partial F_2}{\partial y}&\frac{\partial F_2}{\partial z}\\ \frac{\partial F_3}{\partial x}&\frac{\partial F_3}{\partial y}&\frac{\partial F_3}{\partial z}\end{bmatrix}.
$$

So again our definition can be thought of as the generalization of the familiar vector calculus counterpart.


---

[^1]: In the expression $X^\flat = \left(g_{ij}X^i\right)\varepsilon^j = X^j\varepsilon^j$ the term $X^j\varepsilon^j$ unfortunately doesn't follow our summation convention, but it should be understood to be summed over $j$ since $\left(\delta_{ij}X^i\right)\varepsilon^j = X^j\varepsilon^j$. Similarly for $\omega^\sharp$.
