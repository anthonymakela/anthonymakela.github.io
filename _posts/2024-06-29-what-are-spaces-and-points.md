---
layout: post
title: "What Are Spaces and Points?"
categories: [Abstract Algebra]
mathjax: true
published: false
excerpt_separator: <!--more-->
---


This discussion will be more philosophical than my previous writings. If you have studied modern algebraic geometry, you are likely familiar with the concepts of locally ringed spaces and, more specifically, schemes. Upon first encountering these ideas, you may find it perplexing that the "points" of your space are represented by the prime ideals of a commutative ring $R$. Initially, I struggled to accept this as the proper way to define geometric objects. However, over time, I have come to appreciate and accept this definition more and more and today, I'll try to write out my thoughts on this. 

<!--more-->

---

I would like to first point out that there is a notion of a _topos_ by Grothendieck, which ended up being the ne plus ultra of what is considered a space. However, that is a topic we will reserve for another time since I think its better to start from the beginning to understand what lead to the current understanding.

We'll start with Grothendieck's first approach on defining what a space is. As a general rule, I would like to think of _space_ $X$ as something for which _localization_ makes sense. What I mean by localization here is that in order to define, say a continuous function $f : X \to \Bbb R$, it would suffice to define it on open subsets $U_i$ covering $X$ and check agreements on two-by-two intersections. So essentially I would like to have a sheaf $\mathcal{O}\_X$ on $X$. Following this path, one ends up defining a _ringed space_ $(X,\mathcal{O}\_X)$, where $\mathcal{O}_X$ is a sheaf of rings. This definition, however, is a bit problematic. Ideally one would like the definition to force the topology on $X$ to have something to do with the ring structure. For example, any ring can be viewed as a ringed space on a one-element topological space.

We'll end up defining locally ringed spaces, but before that we need our theory to be in a proper framework. The framework I'm referring to here is that one would like to understand a space $X$ by looking at functions on this space.


---

The story starts with the following observation due to Marshall H. Stone in the $1930$s.

<div class="theorem">
Let $X$ be a compact topological space. For every non-zero $\Bbb R$-algebra homomorphism $\varphi : C(X) \to \Bbb R$, there exists a unique $x \in X$ such that 
$$
\varphi(f) = f(x),
$$
for all $f \in C(X)$.
</div>

<div class="proof">
First of all, $\varphi(1) = 1$. Indeed, $\varphi(1) = \varphi(1 \cdot 1) = \varphi(1)\cdot\varphi(1)$ and $\varphi \ne 0$, thus $\varphi(1) = 1$. This entails that $\varphi(\lambda) = \lambda$ for every $\lambda \in \Bbb R$.
</div>