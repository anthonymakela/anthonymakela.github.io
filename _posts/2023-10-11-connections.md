---
layout: post
title: "Connections"
categories: [Differential Geometry, Riemannian Geometry]
mathjax: true
---

The notion of a connection seems to be a source of confusion for many students seeing it the first time. Questions such as "what is the geometric intuition?" are usually present in discussions with students going through connections and I don't blame them, the definition is rather abstract.

Given a smooth manifold $M$ and a vector bundle $E \to M$ a connection is by definition an $\Bbb R$-linear map 

$$
\begin{align*}
\nabla : \Gamma(E) \to \Gamma(T^\ast M \otimes E)
\end{align*}
$$

such that $\nabla (fs) = df \otimes s + f\nabla s$. Alternatively[^1] we can define $\nabla$ as a map

$$
\begin{align*}
\nabla : \Gamma(TM) \times \Gamma(E) \to \Gamma(E)
\end{align*}
$$

such that for $X \in \Gamma(TM)$ and $s \in \Gamma(E)$ the following two conditions hold:

<ol>
  <li>$\nabla_X s$ is $C^\infty$-linear in $X$ and $\Bbb R$-linear in $s$.</li>
  <li>
  (Leibniz rule) if $f$ is a $C^\infty$ function on $M$, then 
  $$
  \nabla_X(fs) = (Xf)s + f\nabla_X s.
  $$
  </li>
</ol>

Since $Xf = (df)(X)$ we may rewrite the above equation as

$$
  \nabla_X(fs) = (df)(X)s + f\nabla_X s.
$$

Dropping $X$ we have

$$
  \nabla(fs) = df\otimes s + f\nabla s.
$$

This isn't very informative considering the fact that we are essentially looking for a way to generalize the notion of differentiating vector fields to differentiating sections of arbitrary vector bundles over $M$. 

You might have heard the usual story that if we naively try to define a way to differentiate vector fields on a smooth manifold we run into the issue of needing to compare vectors living in different tangent spaces. The is indeed not defined on a general manifold which might or might not be a surprise since we do this kind of things in the familiar $\Bbb R^n$ constantly, but we are actually exploiting the fact that at any point $p \in \Bbb R^n$ we have a canonical isomorphism $T_p\Bbb R^n \cong \Bbb R^n$ that allows us to compare vectors living in different tangent spaces.

So maybe at this point you are convinced that we need a tool to give us the possibility to compare tangent vectors living in different tangent spaces. Indeed, once you have a connection, it comes equipped with something called a parallel transport that is relatively intuitive to understand.

It's tempting to ask why don't we just use the Lie derivative, but this is troublesome for a multitude of reasons. Consider for example the vector fields $X=\frac{\partial}{\partial x}$ and $Y=e^y\frac{\partial}{\partial y}$ in $\Bbb R^2$. On the $x$-axis, these two are equal so one would expect that

$$
\mathcal{L}_X\left(\frac{\partial}{\partial y}\right) = \mathcal{L}_Y\left(\frac{\partial}{\partial y}\right)
$$

but it turns out that $\mathcal{L}_X\left(\frac{\partial}{\partial y}\right) = 0$ and $\mathcal{L}_Y\left(\frac{\partial}{\partial y}\right) = -e^y\frac{\partial}{\partial y}$, so what gives? The issue here is that $\mathcal{L}$ is missing a property that $\nabla$ enjoys. Namely the $C^\infty$-linearity. It's worth noting that the Lie derivative is canonically defined using the smooth structure of a manifold, but on the other hand for the connection we need some extra geometric structure on the manifold.

So about parallel transports. In general if we have a vector field $Y \in \Gamma(TM)$ we say that $X$ is parallel if $\nabla_X Y \equiv 0$ for all $X \in \Gamma(TM)$. Now given a tangent vector $Y_p \in T_pM$ and a curve $\gamma : [0,1] \to M$ starting at $p$ with $\gamma'(0) = Y_p$ there exists a unique parallel vector field $Y$ along $\gamma$ with $Y(0) = Y_p$. We then say that $Y(t) = Y_{\gamma(t)}$ is the parallel transport of $Y_p$ from $p$ to $\gamma(t)$ along $\gamma$.

Effectively we have obtained a well-defined linear map

$$
P^\gamma_{p,q} : T_pM \to T_qM
$$

which turns out to be an isomorphism with inverse $P^\gamma_{q,p}$.

---

[^1]: We actually have $\Gamma(T^\ast M \otimes E) \cong \Gamma(TM)^\ast \otimes_{C^\infty(M)} \Gamma(E)$ and $\Gamma(TM)^\ast \otimes_{C^\infty(M)} \Gamma(E) \cong \operatorname{Hom}_{C^\infty(M)}(\Gamma(TM), \Gamma(E))$ so the first definition is just a curried version of the second one.

