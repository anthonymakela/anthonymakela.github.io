---
layout: post
title: "Curvature"
categories: [Differential Geometry, Riemannian Geometry]
published: false
mathjax: true
---

Today will be all about curvature. Specifically, we will be looking at the <b>Riemann curvature tensor</b> and something called  <b>Ricci curvature</b>.

Let's begin with a heuristic approach before we dive into the formal definitions. What is curvature? You might have some sort of an idea about what it is for example it might not be too difficult for you to convince yourself that the following surface has some <i>curvature</i>.

<p align="center">
    <img src="/assets/images/ddg_saddle.png" alt="image" width="300" height="auto">
</p>

You might even know a method to quantify curvature from your background in vector analysis. Indeed the <i>Frenet frame</i> gives you a way to quantify curvature, but we are now in the realm of Riemannian Geometry and have moved on from the extrinsic geometry which is required for the Frenet frame.

So how can we come up with a method to capture this curviness of a manifold in an intrinsic way? Here is an idea, if $(M,g)$ is a Riemannian manifold, then we know that there exists a unique connection $\nabla$ which is compatible with $g$ i.e. the Levi-Civita connection. Given the connection, we have the ability to transport vectors since we can define the so-called <i>parallel transport</i> which we have discussed before. Maybe the transportation captures the curvature of the manifold somehow? Let's investigate this.

---

Consider first the manifold $\Bbb R^2$ with the usual Riemannian metric. Again heuristically speaking, we would expect this space to be flat even though we don't yet know how to address this properly. Fix a point $p$ in $\Bbb R^2$, coordinates $(x^1,x^2)$ and consider a vector $X_p$ emanating from $p$. Observe now the following: transporting this vector first along the $x^2$-direction and then along the $x^1$-direction back to the point $p$ yields the same vector as the one we started with. The following illustration depicts this.



<p align="center">
    <img src="/assets/images/r2.png" alt="image" width="350" height="auto">
</p>

This innocent idea that you might even consider obvious turns out to be of utmost importance. Let's now consider a manifold like $\Bbb S^2$ which you probably expect to have some sort of curvature. Fix again a point $p$ on the equator, and pick a vector $X_p$ emanating from $p$ and start transporting it around a closed spherical triangle. We see that the resulting vector is different than the vector we started with. Again the following illustration depicts this phenomenon.

<p align="center">
    <img src="/assets/images/sphere.png" alt="image" width="400" height="auto">
</p>

Aha! Seems like we are onto something. It's exactly this curviness that $\Bbb S^2$ has and $\Bbb R^2$ doesn't which is causing the transported vectors to be different. Motivated by this we can define curvature such that it measures in some sense how far away the connection is from being the standard connection on the Euclidean space. Said differently it should measure the deviation from local flatness[^1].

---

So how exactly should we go about defining curvature? Let's look at the situation a bit more closely with the $2$-manifolds $\Bbb R^2$ and $\Bbb S^2$.

Beginning with $\Bbb R^2$ consider a point $p \in \Bbb R^2$ and a vector $X_p$ emanating from $p$.

<p align="center">
    <img src="/assets/images/grid.png" alt="image" width="600" height="auto">
</p>

We can now try to create a parallel extension of $X_p$ in the following manner. Fixing a coordinate system $(x^1,x^2)$, first parallel transport $X_p$ along the $x^1$-axis and then parallel transport each of the resulting vectors along the coordinate lines parallel to the $x^2$-axis. We end up with a vector field $X$ that looks as follows.

<p align="center">
    <img src="/assets/images/field.png" alt="image" width="600" height="auto">
</p>

Now given our construction, $X$ is parallel along every $x^2$-coordinate line i.e. $\overline\nabla_{\partial_2} X = 0$ where $\overline\nabla$ is the standard Euclidean connection. When $x^2 = 0$ we have $\overline\nabla_{\partial_1} X = 0$. The question is now whether or not $X$ is parallel along every other $x^1$-coordinate line? Of course from our picture it's clear, but we need to justify this. Notice that 

$$
\overline\nabla_{\partial_2}(\overline\nabla_{\partial_1} X) = 0 \implies \overline\nabla_{\partial_1} X = 0
$$

by the uniqueness of parallel transports. Here is where the flatness of $\Bbb R^2$ comes into play. $\Bbb R^2$ is special in the sense that 

$$
\begin{align*}
\overline\nabla_{\partial_2}(\overline\nabla_{\partial_1} X) &= \overline\nabla_{\partial_2}\left((\partial_1 X^k)\partial_k\right) \\
&= (\partial_2\partial_1 X^k)\partial_k \\
&= (\partial_1\partial_2 X^k)\partial_k \\
&= \overline\nabla_{\partial_1}(\overline\nabla_{\partial_2} X)
\end{align*}
$$

and as $\overline\nabla_{\partial_2} X = 0$ everywhere, we conclude that $\overline\nabla_{\partial_2}(\overline\nabla_{\partial_1} X) = 0$ i.e. $\overline\nabla_{\partial_1} X = 0$ everywhere. This essentially means that it doesn't matter whether we parallel translate along $x^2$
first, and then along $x^1$ or vice versa.

Again the situation changes drastically when we consider a curved space such as $\Bbb S^2$. Hopefully, you can convince yourself from the image below that the equation $\nabla_{\partial_2}(\nabla_{\partial_1} X) = \nabla_{\partial_1}(\nabla_{\partial_2} X)$ need not hold for the sphere.

<p align="center">
    <img src="/assets/images/sphere2.png" alt="image" width="400" height="auto">
</p>

More generally, on $\Bbb R^n$ for vector fields $X,Y,Z \in \Gamma(T\Bbb R^n)$ we have that:

$$
\begin{align*}
\overline\nabla_X \nabla_Y Z &= \overline\nabla_X(Y(Z^k)\partial_k) \\
&= XY(Z^k)\partial_k
\end{align*}
$$

and likewise

$$
\begin{align*}
\overline\nabla_Y \nabla_X Z &= \overline\nabla_Y(X(Z^k)\partial_k) \\
&= YX(Z^k)\partial_k.
\end{align*}
$$

Looking at the difference we see

$$
\begin{align*}
\overline\nabla_X \overline\nabla_Y Z - \overline\nabla_Y \overline\nabla_X Z &= XY(Z^k)\partial_k - YX(Z^k)\partial_k \\ 
&= (XY(Z^k) - YX(Z^k))\partial_k \\
&= \overline\nabla_{[X,Y]}Z.
\end{align*}
$$

So in $\Bbb R^n$ the equality $\overline\nabla_X \overline\nabla_Y Z - \overline\nabla_Y \overline\nabla_X Z = \overline\nabla_{[X,Y]}Z$ holds for all vector fields $X,Y$ and $Z$ defined on an open subset of $\Bbb R^n$. 

As we discussed above we want to define curvature such that measures the deviation from flatness. Well, now we have an expression that gives us exactly this. We say that a connection $\nabla$ on a Riemannian manifold satisfies the <b>flatness criterion</b> if 

$$
\nabla_X \nabla_Y Z - \nabla_Y \nabla_X Z = \nabla_{[X,Y]}Z
$$

holds for $X,Y,Z \in \Gamma(TM)$. This yields a necessary condition for a Riemannian manifold to be flat.

Since the Levi-Civita connection is natural[^2], if $M$ is flat, then $\nabla$ satisfies the flatness criterion.

---

Let's get on with the formalities then. Motivated by the above discussions we define the <b>Riemann curvature endomorphism</b> $R : \Gamma(TM) \times \Gamma(TM)\times \Gamma(TM) \to \Gamma(TM)$ by 

$$
R(X,Y)Z = \nabla_X \nabla_Y Z - \nabla_Y \nabla_X Z - \nabla_{[X,Y]}Z.
$$

As usual, when you meet an expression like this you should be asking yourself whether or not you are dealing with a tensor field.

<div class="proposition">
The Riemann curvature endomorphism is multilinear over $C^\infty(M)$, and thus defines a $(1,3)$-tensor field on $M$.
</div>

<div class="proof">
Linearity over $\Bbb R$ is clear. For $f \in C^\infty(M)$ we have
$$
\begin{align*}
R(X,fY)Z &= \nabla_X \nabla_{fY} Z - \nabla_{fY} \nabla_X Z - \nabla_{[X,fY]}Z \\
&= \nabla_X\left(f\nabla_{Y} Z\right) - f\nabla_{Y} \nabla_X Z - \nabla_{X(f)Y + f[X,Y]}Z \\
&= X(f)\nabla_YZ + f\nabla_X\nabla_Y Z - f\nabla_{Y} \nabla_X Z - X(f)\nabla_YZ - f\nabla_{[X,Y]}Z \\
&= fR(X,Y)Z.
\end{align*}
$$

As $R(X,Y)Z = -R(Y,X)Z$ the same reasoning works for $C^\infty(M)$-linearity in $X$. Now in $Z$ we have:

$$
\begin{align*}
R(X,Y)fZ &= \nabla_X \nabla_{Y} fZ - \nabla_{Y} \nabla_X fZ - \nabla_{[X,Y]}fZ \\
&= \nabla_X\left(Yf(Z) + f\nabla_Y Z\right) - \nabla_Y(Xf(Z) + f\nabla_X Z) - ([X,Y]f)Z - f\nabla_{[X,Y]}Z \\
&= \nabla_X Yf(Z) + \nabla_X(f\nabla_Y Z) - \nabla_Y Xf(Z) \\
&\quad - \nabla_Y(f\nabla_X Z) - ([X,Y]f)Z - f\nabla_{[X,Y]}Z \\
&= (XYf)(Z) + (Yf)\nabla_X Z + (Xf)\nabla_Y Z + f\nabla_X\nabla_Y Z \\
&\quad - (YXf)(Z) - (Xf)\nabla_YZ - (Yf)\nabla_X Z - f\nabla_Y\nabla_X Z \\
&\quad - ([X,Y]f)Z - f\nabla_{[X,Y]}Z \\
&= f(\nabla_X\nabla_Y - \nabla_Y\nabla_X - \nabla_{[X,Y]})Z  + ((XY-YX)f)Z - ([X,Y]f)Z \\
&= f(\nabla_X\nabla_Y - \nabla_Y\nabla_X - \nabla_{[X,Y]})Z + ([X,Y]f)Z - ([X,Y]f)Z \\
&= f(\nabla_X\nabla_Y - \nabla_Y\nabla_X - \nabla_{[X,Y]})Z \\
&= fR(X,Y)Z.
\end{align*}
$$

which yields $C^\infty(M)$-linearity in $Z$. The <a href="https://anthonymakela.com/differential%20geometry/2023/09/07/tensor-characterization-lemma.html" style="color:#680530; text-decoration: underline;">Tensor Characterization Lemma</a> now implies that $R$ is indeed a $(1,3)$-tensor field.
</div>

As a $(1,3)$-tensor field, we can write $R$ in any local frame with one upper and three lower indices. In local coordinates $(x^i)$ we have: 

$$
R = R^l_{ijk} dx^i \otimes dx^j \otimes dx^k \otimes \partial_l.    
$$

---

[^1]: Being locally isometric to $\Bbb R^n$

[^2]: If $(M,g)$ and $(\widetilde{M}, \widetilde{g})$ are Riemannian manifolds with Levi-Civita connections $\nabla$ and $\widetilde{\nabla}$ an isometry between them $\varphi : M \to \widetilde{M}$ yields that $\varphi^\ast \widetilde{\nabla} = \nabla$.