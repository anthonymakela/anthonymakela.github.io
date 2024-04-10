---
layout: post
title: "Hermite-Einstein and Kähler-Einstein Metrics"
categories: [Complex Geometry, Differential Geometry]
mathjax: true
published: false
excerpt_separator: <!--more-->
---

Last time we went over holomorphic connections and the Atiyah class on a holomorphic vector bundle. At the end of the post, we were looking at some of the properties of holomorphic vector bundles with vanishing Atiyah class and their correspondence with holomorphic bundles that admit flat connections. In one of the propositions, I mentioned something called a <i>Hermite-Einstein</i> metric, which we have not yet discussed. This, and the stability of vector bundles will be the topic for today.

<!--more-->

---

As the name might suggest, we are stepping a bit on the physicists territory here. I'm by no means a physicist so I'm going to keep the actual physics to a minimum. That being said, let's kick this off with some physics and more specifically with the Einstein field equations. Suppose that $(X,g)$ is a Riemannian manifold. The Einstein field equations are given by 

$$
\operatorname{Ric} = \frac{1}{2}S + T,
$$

where $S$ is the scalar curvature of $g$ and $T$ the so-called stress-energy tensor. Now in our case $T \equiv 0$ and for the mathematicians version of this we state the following definition.

<div class="definition">
A Riemannian manifold $(X,g)$ is called <i>Einstein</i> if the Ricci tensor $\operatorname{Ric}$ is proportional to the metric $g$. That is

$$
\operatorname{Ric} = \lambda g,
$$

for $\lambda \in \Bbb R$.
</div>

Consider now a compact Hermitian manifold $(X,g)$ and the fundamental form $\omega = g(J(-), -)$. By definition $(X,g)$ is Kähler if and only if $d\omega = 0$ or equivalently if $J$ is parallel with respect to the Levi-Civita connection of $g$. Now $g$ can be viewed as a Hermitian metric on the tangent bundle of $X$ and instead of asking if the Ricci curvature of the Levi-Civita connection on the tangent bundle of $X$ is proportional to $g$, we can ask the same question about the curvature $F_\nabla$ of a Chern connection $\nabla$ associated to a Hermitian metric on <i>any</i> holomorphic vector bundle $E$ over $X$,

Recall that $F_\nabla \in \Omega^{1,1}(X, \operatorname{End}(E))$, i.e. $F_\nabla$ is of type $(1,1)$.
