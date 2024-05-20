---
layout: post
title: "Chern Classes of Hermite-Einstein Bundles"
categories: [Complex Geometry, Differential Geometry]
mathjax: true
published: false
excerpt_separator: <!--more-->
---

I'm planning on writing about Calabi-Yau manifolds in the upcoming future, but before I do that there is a loose end I would like to tie up. Last time we discussed vector bundles admitting Hermite-Einstein metrics. Today we'll be looking at the Chern classes of such bundles. This is going to be a relatively short one, but since they impose certain conditions on the flatness of the manifold—and that is mainly the question I'm interested in at the moment—I want to go over this.

<!--more-->

---

Recall that last time we proved the so-called Kobayashi-Lübke inequality given by

$$
\int_X (2kc_2(E) - (k-1)c^2_1(E)) \wedge \omega^{n-2} \ge 0,
$$

where $E$ is a holomorphic vector bundle of rank $k$ over a compact Hermitian manifold $(X,g)$. The main result I want to prove today is the following:

<div class="theorem" text="1">
Let $(E,h)$ be an Hermitian vector bundle over a compact Kähler manifold $(X,g)$ of dimension $n$. If it satisfies the Hermite-Einstein condition and if $c_1(E) = 0$, then
$$
\int_X c_2(E) \wedge \omega^{n-2} \ge 0,
$$
and the equality holds if and only if $(E,h)$ is flat.
</div>

The first part clearly follows from the Kobayashi-Lübke inequality, but for the latter part we need to do some work. Recall that a connection $\nabla$ on a complex vector bundle $E$ over $M$ is <i>projectively flat</i> if and only if its curvat