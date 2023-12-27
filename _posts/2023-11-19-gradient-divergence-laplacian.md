---
layout: post
title: "Gradient, Divergence and the Laplacian"
categories: [Differential Geometry]
mathjax: true
---

I'm currently tasked to give a short presentation about the Bochner Technique and I thought that it would probably be beneficial to track my thoughts prior to the presentation. As you might know, the Bochner Technique is a way to relate the Laplacian to the curvature tensor. Before this, however, we need to understand what the gradient, divergence, and Laplacian are on a Riemannian manifold. This is going to be the topic for this post. 

For the remaining of this post, $(M,g)$ denotes a Riemannian $n$-manifold.

Let's begin with the gradient. Notation-wise the gradient of a smooth function $f \in C^\infty(M)$ is denoted either via $\nabla f$ or $\operatorname{grad} f$. I will most likely end up using both since the former is more convenient to write, but since it might result in confusion with the symbol we use for connections in some cases I might resort to the latter. 

So, the definition then. 

<div class="definition">
Let $f \in C^\infty(M)$. The <b>gradient</b> $\nabla f$ of $f$ is defined to be the smooth vector field such that
$$
g(\nabla f, X) = Xf = df(X)
$$
for all $X \in \Gamma(TM)$.
</div>

Astute readers might recognize a similarity here to the musical operator $\sharp$, and they would be correct. Indeed, we have the following relationship:

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

To see why it is an isomorphism, note that the non-degeneracy of $g$ implies that 

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

Now as the matrix $[g_{ij}]$ is invertible, the matrix for $\sharp$ is given by the inverse matrix $[g^{ij}]$. For $\omega = \omega_j\varepsilon^j$ we have

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

---

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

Let's now try to derive a local expression for the divergence. Consider a local frame $(e_i)$ and $X = X^je_j$. Now effectively we are trying to find the elements on the diagonal of the linear map $\nabla X : \Gamma(TM) \to \Gamma(TM)$. You know from linear algebra that we can obtain the columns of the resulting matrix by considering $\nabla_{e_i}X$. We have

$$
\begin{align*}
    \nabla_{e_i}X &= \nabla_{e_i}(X^je_j) \\
    &= X^j\nabla_{e_i}e_j + e_i(X^j)e_j \\
    &= X^j\Gamma^k_{ij}e_k + e_i(X^j)e_j \\
    &= X^j\Gamma^k_{ij}e_k + e_i(X^k)e_k \\
    &= (X^j\Gamma^k_{ij} + e_i(X^k))e_k
\end{align*}
$$

and hence the $(i,k)$'th entry of the resulting matrix is $X^j\Gamma^k_{ij} + e_i(X^k)$. Since we are after the diagonal we want to consider the terms $X^j\Gamma^i_{ij} + e_i(X^i)$. Alternatively, we could have extracted these using the metric by $g\left(\nabla_{e_i}X, e_i\right)$. It follows that

$$
\begin{align*}
    \operatorname{div}(X) &= \operatorname{tr}(Y \longmapsto \nabla_Y X) \\
    &= \sum_{i} g\left(\nabla_{e_i}X, e_i\right) \\
    &= X^j\Gamma^i_{ij} + e_i(X^i).
\end{align*}
$$

Now, I'm just going to pull of a description[^2] from the magician's hat for $\Gamma^i_{ij}$ and you should convince yourself that it is true. We end up with

$$
\begin{align*}
    \operatorname{div}(X) &= \operatorname{tr}(Y \longmapsto \nabla_Y X) \\
    &= \sum_{i} g\left(\nabla_{e_i}X, e_i\right) \\
    &= X^j\Gamma^i_{ij} + e_i(X^i) \\
    &= X^j\underbrace{\frac{1}{\sqrt{|g|}} e_{j}\left(\sqrt{|g|}\right)}_{\Gamma_{ij}^i} + e_i(X^i) \\
    &= X^j\frac{1}{\sqrt{|g|}} e_{j}\left(\sqrt{|g|}\right) + e_j(X^j) \\
    &= \frac{1}{\sqrt{|g|}}e_j\left(\sqrt{|g|}X^j\right).
\end{align*}
$$

The second to last equality is just renaming the indexes on the sum over $i$ and the last equality follows since we can recognize the above one as a differential of a product.

It's probably no surprise that $\operatorname{div}$ satisfies some kind of a product rule. We have the following:

<div class="lemma">
    For $f \in C^\infty(M)$ and $X \in \Gamma(TM)$ the divergence satisfies
    $$
    \operatorname{div}(fX) = f\operatorname{div}(X) + g(\nabla f, X).
    $$
</div>

<div class="proof">
Recall that the connection $\nabla$ satisfies the Leibniz rule: 
$$
\nabla(fX) = df \otimes X + f\nabla X.
$$

Now we have that:

$$
\begin{align*}
\operatorname{div}(fX) &= \operatorname{tr}\left(\nabla(fX)\right) \\
&= \operatorname{tr}\left(df \otimes X + f\nabla X\right) \\
&= \operatorname{tr}(df \otimes X) + f\operatorname{tr}(\nabla X) \\
&= df(X) + f\operatorname{div}(\nabla X) \\
&= f\operatorname{div}(\nabla X) + g(\nabla f, X)
\end{align*}
$$

which yields the proof.
</div>

I mentioned earlier that there is an alternative way to express the divergence. Indeed we have the following characterization:

<div class="lemma">
Let $dV_g$ denote the Riemannian volume form and $X \in \Gamma(TM)$. The divergence is characterized by the following:
$$
d(\iota(dV_g)) = (\operatorname{div}(X))dV_g.
$$
</div>

<div class="proof">
We proceed to prove this locally. Let $p \in M$ and consider a <i markdown=1>normal[^3]</i> coordinate chart $(U,x^1,\dots,x^n)$ centered at $p$. For $X = X^j\partial_j$ we have that
$$
\begin{align*}
\operatorname{div}(X)(p) &= \operatorname{tr}(\nabla X)(p) \\
&= \sum g\left(\nabla_{\partial_i} X, \partial_i\right)(p) \\
&= \sum_i g\left(X^j\nabla_{\partial_i}\partial_j + \partial_i(X^j)\partial_j, \partial_i\right)(p) \\
&= \sum_i g\left(\partial_i(X^j)\partial_j, \partial_i\right)(p) \\
&= \sum_i \partial_i X^i(p).
\end{align*}
$$

On the other hand

$$
\begin{align*}
d(\iota_X(dV_g))(p) &= \sum_{j=1}^n\sum_{i=1}^n(-1)^{i+1}(\partial_j X^i)(p)dx^j\wedge dx^1\wedge\ldots\widehat{dx^i}\wedge\ldots\wedge dx^n \\
&= \left(\sum_{i=1}^n(\partial_i X^i)(p)\right)\ dx^1\wedge\ldots\wedge dx^n \\
&= \operatorname{tr}(\nabla X)(p) dV_g \\
&= \operatorname{div}(X)(p) dV_g
\end{align*}
$$

where the second equality follows from permuting the term $dx^j$ and using the antisymmetric properties of $\wedge$ to conclude that terms with $i \ne j$ are all zero.
</div>

The reason we needed this characterization is that now we have a neat proof for the so-called divergence theorem.

<div class="theorem">
Let $X \in \Gamma(TM)$ and suppose that $M$ is orientable. Then
$$
\int_M \left(\operatorname{div} X\right) \ dV_g = \int_{\partial M} \langle X, N\rangle_g \ dV_{\widehat{g}},
$$
where $N$ is the outward unit normal to $\partial M$ and $\widehat{g}$ is the induced metric on $\partial M$.
</div>

<div class="proof">
Let's first recall Cartan's homotopy formula: 
$$
\mathscr{L}_X = d\iota_X + \iota_X d.
$$

Using this we can write $\left(\operatorname{div} X\right)dV_g = \mathscr{L}_X(dV_g) - \iota_X d(dV_g) = \mathscr{L}_X(dV_g)$. Now Stokes' theorem yields the following:

$$
\begin{align*}
\int_M \left(\operatorname{div} X\right) \ dV_g &= \int_M \mathscr{L}_X(dV_g)  \\
&= \int_{\partial M} \iota_X(dV_g).
\end{align*}
$$

We are left to show that $\iota_X(dV_g) = \langle X, N \rangle_g dV_{\widehat{g}}$. Given that the right-hand side involves the normal component of $X$ we can split $X$ into its normal and tangential components $X = X_\perp + X_\parallel$. Let $(e_1,\dots,e_{n-1}, N)$ be a local orthonormal frame. We have that

$$
\begin{align*}
\iota_X(dV_g)(e_1,\dots,e_{n-1}) &= dV_g(X_\perp + X_\parallel, e_1,\dots,e_{n-1}) \\
&= dV_g(\langle X, N\rangle_g N + \langle X, e_1\rangle_g e_1 + \dots + \langle X, e_{n-1}\rangle_g e_{n-1}, e_1,\dots,e_{n-1}) \\
&= \langle X, N\rangle_gdV_g(N,e_1,\dots,e_{n-1}) \\
&= \langle X, N\rangle_g\iota_{N}(dV_g)(e_1,\dots,e_{n-1}) \\
&= \langle X, N\rangle_g(dV_\widehat{g})(e_1,\dots,e_{n-1}).
\end{align*}
$$

The third equality follows since $dV_g$ is alternating, meaning that if two of its arguments are the same, or linearly dependent, the result is zero.
</div>

As a corollary we get the following "integration by parts" formula:

$$
\int_M \langle \nabla f, X\rangle_g \ dV_g = \int_{\partial M} f\langle X,N\rangle_g \ dV_{\widehat{g}} - \int_M f \operatorname{div}(X) \ dV_g.
$$

The naming comes from considering for example $M = [0,1] \subset \Bbb R$. We recover the usual integration by parts formula as

$$
\int_{[0,1]} f'(x)X(x) \ dx = f(1)X(1) - f(0)X(0) - \int_{[0,1]} f(x)X'(x) \ dx
$$

since $N$ is $+1$ at $1$ and $-1$ at $0$.

---

Let's move on to the Laplacian. This one is particularly interesting as it provides a bridge between the analytical and topological sides of compact oriented Riemannian manifolds. It's a theorem of Hodge that 

$$
\ker(\Delta) \cong H^k_{dR}(M)
$$

where $\ker(\Delta) = \\{\omega \in \Omega^k(M) \mid \Delta \omega = 0\\}$. The astonishing thing here is that the kernel of the Laplacian depends a priori only on the metric and the cohomology of course on the homotopy type of $M$. We'll discuss this later, but for now, let's focus on the Laplacian and some of its properties.

<div class="definition">
The Laplacian or Laplace-Beltrami operator is the linear operator $\Delta : C^\infty(M) \to C^\infty(M)$ defined by
$$
\Delta f = \operatorname{div}(\nabla f) = \operatorname{tr}(Y \longmapsto \nabla_Y\operatorname{grad} f).
$$
</div>

Again we have an analogous definition for the Euclidean counterpart. The Laplacian for a function $f: \Bbb R^3 \to \Bbb R^3$ is defined by

$$
\Delta f = \nabla \cdot \nabla f = \frac{\partial^2 f}{\partial x^2} + \frac{\partial^2 f}{\partial y^2} + \frac{\partial^2 f}{\partial z^2}
$$

and staring at this for a while we recognize it as the trace of the <i>Hessian</i> of $f$.

What about the local expression? As I mentioned earlier we did the heavy lifting with the divergence and already computed the local expression for the gradient. If you look at the local expression for the divergence you can see that we only need the components of the gradient. Thus in a local frame $(e_i)$ the Laplacian has the form:

$$
\begin{align*}
\Delta f &=\operatorname{tr}(Y \longmapsto \nabla_Y\operatorname{grad} f) \\
&= \frac{1}{\sqrt{|g|}}e_j\left(\sqrt{|g|}g^{ij}e_i f\right).
\end{align*}
$$

As you might suspect, the Laplacian should also satisfy some kind of a product rule. Indeed it does.

<div class="lemma">
For smooth functions $f,h \in C^\infty(M)$ we have:
$$
\Delta(fh) = f\Delta h + h\Delta f + 2g\left(\nabla f, \nabla h\right).
$$
</div>

<div class="proof">
This follows directly from the product rule for the divergence and the gradient we proved earlier. We have
$$
\begin{align*}
\Delta(fh) &= \operatorname{div}(\nabla(fh))\\
&= \operatorname{div}(f\nabla h + h\nabla f) \\
&= \operatorname{div}(f\nabla h) + \operatorname{div}(h\nabla f) \\
&= f\operatorname{div}(\nabla h) + g(\nabla f, \nabla h) + h\operatorname{div}(\nabla f) + g(\nabla h, \nabla f)\\
&= f\Delta h + h\Delta f + 2g(\nabla f, \nabla h)
\end{align*}
$$
which concludes the proof.
</div>

Remember the integration by parts formula we had before? It's tempting to see what happens if the consider the gradient of some smooth function in place of $X$ in order to recover the Laplacian. Let $f,h \in C^\infty(M)$. The integration by parts formula says now that

$$
\begin{align*}
    \int_M \langle \nabla f, \nabla h\rangle_g \ dV_g &= \int_{\partial M} f\langle \nabla h, N\rangle_g \ dV_{\widehat{g}} - \int_M f \Delta h \ dV_g \\
    &= \int_{\partial M} fNh \ dV_{\widehat{g}} - \int_M f \Delta h \ dV_g.
\end{align*}
$$

From this we can also derive that:

$$
\begin{align*}
\int_M (f\Delta h - h\Delta f) \ dV_g = \int_{\partial M} (f N h - h N f) \ dV_g.
\end{align*}
$$

These are called <b>Green's identities</b>.

At the beginning of our discussion about the Laplacian I briefly mentioned about forms that vanish under $\Delta$. Such things have a name and are called <b>harmonic</b> forms.    

Harmonic functions are in general quite interesting as they are in some sense "rigid". The intuition you should be having for harmonicity is that it is a function whose value at a point is equal to the average of its values on a ball centered at that point.

For example if $M$ is compact, connected, and has boundary, then for any two harmonic functions $f,h$ on $M$ which agree on merely $\partial M$ we have $f \equiv h$. Why? Given the first one of Green's identities, we have that

$$
\int_M \langle \nabla(f-h), \nabla(f-h)\rangle_g \ dV_g = 0
$$

since $f-h = 0$ on $\partial M$ and both functions are harmonic. Also as the metric is positive-definite $\langle \nabla(f-h), \nabla(f-h)\rangle_g = 0$ which implies that $\nabla(f-h) = 0$ and so $f-h$ must be constant. If it's zero on the boundary it must be zero everywhere i.e. $f \equiv h$.

If $M$ has no boundary, then the only harmonic functions are constants and every smooth function $h$ satisfies $\int_M \Delta h \ dV_g = 0$. The proof again follows quite easily from the identities we derived. If $f$ is harmonic, setting $h = f$ we have

$$
\int_M \langle \nabla f, \nabla f\rangle_g \ dV_g = \int_{\partial M} f N f \ dV_{\widehat{g}} - \int_M f \Delta f \ dV_g = 0
$$

and using the positive-definite property of the metric again we conclude that $\langle \nabla f, \nabla f\rangle_g = 0$ i.e. $\nabla f = 0$ which implies that $f$ is constant.

To see that every smooth function $h$ satisfies $\int_M \Delta h \ dV_g = 0$ set $f = 1$ and use the identity again.

That's all I have for you this time around. Next time we will probably look at some basic Hodge Theory or the Bochner formula. I also need to get back on the posts concerning sheaf cohomology which I'll try to do fairly soon.

---

[^1]: In the expression $X^\flat = \left(g_{ij}X^i\right)\varepsilon^j = X^j\varepsilon^j$ the term $X^j\varepsilon^j$ unfortunately doesn't follow our summation convention, but it should be understood to be summed over $j$ since $\left(\delta_{ij}X^i\right)\varepsilon^j = X^j\varepsilon^j$. Similarly for $\omega^\sharp$.

[^2]: This is a consequence of Jacobi's formula.

[^3]: A coordinate chart in which the Christoffel symbols vanish. That is $\nabla_{\partial_i}\partial_j(p) = 0$.