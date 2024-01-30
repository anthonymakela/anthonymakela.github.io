---
layout: post
title: "Sheaf Cohomology"
categories: [Algebraic Topology Category Theory]
mathjax: true
published: false
excerpt_separator: <!--more-->
---

We'll be continuing our journey on sheaves and their cohomology today. Last time we ended up in a situation where we considered a short exact sequence of sheaves 

$$
0 \longrightarrow \mathcal{F} \longrightarrow \mathcal{G} \longrightarrow \mathcal{H} \longrightarrow 0,
$$ 

on a topological space $X$. This gave us a short exact sequence of sections

$$
0 \longrightarrow \mathcal{F}(U) \longrightarrow \mathcal{G}(U) \longrightarrow \mathcal{H}(U),
$$

for every open set $U \subset X$. We noted that the map $\mathcal{G}(U) \longrightarrow \mathcal{H}(U)$ needed not be surjective[^1], which leads us to the question, how "far" is it from being surjective? The cohomology $H^1(U, \mathcal{F})$ turns out to measure exactly this. We are often interested in the case $U  =X$ and call the sections _global sections_. If the group $H^1(X, \mathcal{F})$ is zero, then the exact sequence implies that every global section of $\mathcal{H}$ lifts to a global section of $\mathcal{G}$.

The exactness of the first sequence is purely local property, whereas exactness of the second sequence is a global property.

More formally, sheaf cohomology is a theory which is used to compute and understand this defect in exactness via the use of invariants, namely the images under derived functors $R^i\Gamma$ usually written as $H^i(X,-)$.

---

Last time we went over the example using the exact sequence of sheaves on $\Bbb R^2 \setminus \\{0\\}$ given by

$$
0 \longrightarrow \underline{\Bbb R}\to \Omega^0 \longrightarrow \Omega^1 \longrightarrow 0. 
$$

We noted that even though this is exact, passing to global sections

$$
0 \longrightarrow \underline{\Bbb R}(\Bbb R^2 \setminus \\{0\\})\to \Omega^0(\Bbb R^2 \setminus \\{0\\}) \longrightarrow \Omega^1(\Bbb R^2 \setminus \\{0\\}),
$$

ended up causing an issue with the surjectivity of the last map as the differential form 
$$
d\theta = \frac{-ydx + xdy}{x^2+y^2} \in \Omega^1(\Bbb R^2 \setminus \\{0\\}),
$$

is closed, but not exact. As mentioned above, this failure of surjectivity is measured by the group $H^1(\Bbb R^2 \setminus \\{0\\}, \underline{\Bbb R}) = \Bbb R$. What this is saying is that, even though every closed form is locally exact[^2] (a local property) we cannot expect this to hold globally on all of $\Bbb R^2 \setminus \{0\}$ (a global property).

The way you should be thinking about this is captured by the following quote: "Suppose you have a topological space and a covering for that space such that you can do _something_ you want on each set of the covering. Can you do it on the whole space?"

<div class="exercise">
On any manifold $M$ of dimension $n$, prove that the sequence of sheaves
$$
0 \longrightarrow \underline{\Bbb R}\to \Omega^0 \longrightarrow \Omega^1\longrightarrow \dots \longrightarrow \Omega^n \longrightarrow 0
$$
is exact. 
</div>

---
We'll begin by quickly going over abelian categories. The motivation for this is that we mainly want to be able to do homological algebra on $\mathbf{Sh}(X)$ like we are able to do in $\mathbf{Ab}$ or $R\mathbf{-Mod}$.

An abelian category $\mathscr{C}$ is  a category satisfying the following conditions:

<li>
For every pair of objects $A, B \in \mathscr{C}$, 
</li>

---

[^1]: What this is saying is that the global sections functor $\Gamma(X,-) : \mathbf{Sh}(X) \to \mathbf{Ab}$ is not exact, but only left-exact.

[^2]: Poincaré Lemma!
