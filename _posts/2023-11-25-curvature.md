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

Consider first the manifold $\Bbb R^2$ with the usual Riemannian metric. Again heuristically speaking, we would expect this space to be flat even though we don't yet know how to address this properly. Fix a point $p$ in $\Bbb R^2$ and consider a vector $X_p = \partial_2\vert_p$. Observe now the following: transporting this vector first along the $\partial_2$-direction and then along the $\partial_1$-direction back to the point $p$, yields the same vector as the one we started with. The following illustration depicts this.

<p align="center">
    <img src="/assets/images/r2.png" alt="image" width="350" height="auto">
</p>

This innocent idea that you might even consider obvious turns out to be of utmost importance. Let's now consider a manifold like $\Bbb S^2$ which you probably expect to have some sort of curvature. Fix again a point $p$ on the equator, and pick a vector $X_p$ emanating from $p$ and start transporting it around a closed spherical triangle. We see that the resulting vector is different than the vector we started with. Again the following illustration depicts this phenomenon.

<p align="center">
    <img src="/assets/images/sphere.png" alt="image" width="400" height="auto">
</p>

Aha! Seems like we are onto something. It's exactly this curviness that $\Bbb S^2$ has and $\Bbb R^2$ doesn't which is causing the transported vectors to be different. Motivated by this we can define curvature such that it measures in some sense how far away the connection is from being the standard connection on the Euclidean space. Said differently it should measure the deviation from local flatness[^1].

---

[^1]: Being locally isometric to $\Bbb R^n$