---
layout: post
title: "Connections"
categories: [Differential Geometry]
mathjax: true
---

The notion of a connection seems to be a source of confusion for many students seeing it for the first time. Questions such as "What is the geometric intuition?" are usually present in discussions with students going through connections and I don't blame them, the definition is rather abstract.

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
  <li>$\nabla_X s$ is $C^\infty(M)$-linear in $X$ and $\Bbb R$-linear in $s$.</li>
  <li>
  (Leibniz rule) if $f$ is a smooth function on $M$, then 
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

Note that we are implicitly using the isomorphism[^2] $T^\ast M \otimes E \cong \operatorname{Hom}(TM,E)$ in the above calculation to justify this "dropping $X$". The map $X \longmapsto df(X)s \in \operatorname{Hom}(TM,E)$ corresponds exactly to the element $df \otimes s \in T^\ast M \otimes E$.

This isn't very informative considering the fact that we are essentially looking for a way to generalize the notion of differentiating vector fields to differentiating sections of arbitrary vector bundles over $M$. 

You might have heard the usual story that if we naively try to define a way to differentiate vector fields on a smooth manifold we run into the issue of needing to compare vectors living in different tangent spaces. The is indeed not defined on a general manifold which might or might not be a surprise since we do this kind of thing in the familiar $\Bbb R^n$ constantly, but we are actually exploiting the fact that at any point $p \in \Bbb R^n$ we have a canonical isomorphism $T_p\Bbb R^n \cong \Bbb R^n$ that allows us to compare vectors living in different tangent spaces.

So maybe at this point you are convinced that we need a tool to give us the possibility to compare tangent vectors living in different tangent spaces. Indeed, once you have a connection, it comes equipped with something called a parallel transport that is relatively intuitive to understand.

It's tempting to ask why don't we just use the Lie derivative, but this is troublesome for a multitude of reasons. Consider for example the vector fields $X=\frac{\partial}{\partial x}$ and $Y=e^y\frac{\partial}{\partial x}$ in $\Bbb R^2$. On the $x$-axis, these two are equal so one would expect that

$$
\mathcal{L}_X\left(\frac{\partial}{\partial y}\right) = \mathcal{L}_Y\left(\frac{\partial}{\partial y}\right),
$$

but it turns out that $\mathcal{L}_X\left(\frac{\partial}{\partial y}\right) = 0$ and $\mathcal{L}_Y\left(\frac{\partial}{\partial y}\right) = -e^y\frac{\partial}{\partial x}$, so what gives? The issue here is that $\mathcal{L}$ is missing a property that $\nabla$ enjoys. Namely the $C^\infty(M)$-linearity[^3]. More explicitly a connection $\nabla$ satisfies

$$
\nabla_{fX}s = f\nabla_X s,
$$

for $X \in \Gamma(TM)$ and $s \in \Gamma(E)$. Comparing this with the Lie derivative, the above example illustrates that generally

$$
\mathcal{L}_{fX}Y \ne f\mathcal{L}_XY.
$$
 
In <a href="https://anthonymakela.com/differential%20geometry/2023/12/27/connection-and-curvature-forms.html" style="color:#680530; text-decoration: underline;">Connection and Curvature Forms</a> I gave a proof for the fact that $\nabla$ is a local operator[^4] and it was exactly this tensoriality that was the key ingredient we needed. It follows that the Lie derivative is _not_ a local operator, which is a property we would like to have for an operator we are going to be using to "differentiate" things.

It's worth noting that the Lie derivative is canonically defined using the smooth structure of a manifold, but on the other hand for the connection, we need some extra geometric structure on the manifold.

So about parallel transports. In general, if we have a vector field $Y \in \Gamma(TM)$ we say that $X$ is parallel if $\nabla_X Y \equiv 0$ for all $X \in \Gamma(TM)$. Now given a tangent vector $Y_p \in T_pM$ and a curve $\gamma : [0,1] \to M$ starting at $p$ with $\gamma'(0) = Y_p$ there exists a unique parallel vector field $Y$ along $\gamma$ with $Y(0) = Y_p$. We then say that $Y(t) = Y_{\gamma(t)}$ is the parallel transport of $Y_p$ from $p$ to $\gamma(t)$ along $\gamma$.

Effectively we have obtained a well-defined linear map

$$
P^\gamma_{p,q} : T_pM \to T_qM
$$

which turns out to be an isomorphism with inverse $P^\gamma_{q,p}$.

---

More generally, given a vector bundle $E \to M$, we would like to have a notion on how to differentiate sections of $E$. A connection on $E$ gives us exactly this. Let's go over some examples of this to get more familiar with the idea.

<div class="example">
The directional derivative in Eucliden space defines a connection. If $Y = \sum a^i \partial/\partial x^i$ is a vector field on $\Bbb R^n$, then the directional derivative of $Y$ in the direction $X_p$ is defined to be

$$
\nabla_{X_p}Y = \sum (Xa^i)\frac{\partial}{\partial x^i}\Bigg\rvert_p.
$$

</div>

<div class="example">
Suppose that $E = M \times \Bbb R^k$ is the trivial bundle of rank $k$ over $M$. Then there exists a global frame $e = (e_1,\dots, e_k)$ and any global section $s \in \Gamma(E)$ can be written as $s = \sum s^ie_i$ with $s^i : M \to \Bbb R$. For $X \in \Gamma(TM)$, the Leibniz rule yields

$$
\begin{align*}
\nabla_X s &= \sum ds^i(X)e_i + s^i\nabla_X e_i.
\end{align*}
$$

Declaring the sections $e_i$ to be flat, we obtain a connection by setting

$$
\nabla s = ds,
$$

where $ds$ is understood to be the exterior derivative of a $E$-valued differential form. That is, $ds = \sum_i ds^i \otimes e_i \in \Gamma(T^\ast M \otimes E)$.

</div>

Notice that if we have two connections $\nabla_1$ and $\nabla_2$ on a vector bundle $E$, then for all smooth functions $f$ on $M$ and sections $s$ of $E$ we have

$$
\begin{align*}
(\nabla_1 - \nabla_2)(fs) &= \nabla_1(fs) - \nabla_2(fs) \\
&= (df \otimes s + f\nabla_1 s) - (df \otimes s + f\nabla_2 s) \\
&= f(\nabla_1 s -\nabla_2 s),
\end{align*}
$$

i.e. the difference of two connections is $C^\infty(M)$-linear. Recall from <a href="https://anthonymakela.com/differential%20geometry/2023/07/01/local-operators.html" style="color:#680530; text-decoration: underline;">Local Operators</a> that given a $C^\infty(M)$-linear map of sections $\Gamma(E) \to \Gamma(F)$ for two bundles $E$ and $F$, we obtain a unique map $E_p \to F_p$ for each $p \in M$. In particular, since $\nabla_1 - \nabla_2 : \Gamma(E) \to \Gamma(T^\ast M \otimes E)$ is $C^\infty(M)$-linear, we obtain a map $E_p \to T^\ast_p M \otimes E_p$ which is the same as a map $T_pM \to \operatorname{End}(E_p)$ i.e. $\nabla_1 - \nabla_2$ gives an $\operatorname{End}(E)$-valued $1$-form.

Given a connection $\nabla$ on $E$ and a $\operatorname{End}(E)$-valued $1$-form $A$, we have that

$$
\begin{align*}
(\nabla + A)(fs) &= \nabla(fs) + A(fs) \\
&= df \otimes s + f\nabla s + fA(s) \\
&= df \otimes s + f(\nabla + A)(s).
\end{align*}
$$

Thus $\nabla + A$ satisfies the Leibniz rule and is, therefore, a connection. Since connections always exist we obtain the following proposition.

<div class="proposition">
The set of all connections on a vector bundle $E$ is an affine space over the space of $\operatorname{End}(E)$-valued $1$-forms.
</div>

The above proposition gives us a neat way to describe connections locally since any connection can be obtained from fixed "basepoint connection". If $U \subset M$ is a trivializing open set, then $E\vert_U \cong U \times \Bbb R^k$. Hence we can take $d$ as our "basepoint connection". It follows that any connection on $U$ can be written as 

$$
\nabla = d + A,
$$

where $A$ is a matrix-valued $1$-form. In an upcoming post on connection $1$-forms and curvature $2$-forms, I’ll go more in depth on how we describe these things locally on a framed open set.

---

[^1]: We actually have $\Gamma(T^\ast M \otimes E) \cong \Gamma(TM)^\ast \otimes_{C^\infty(M)} \Gamma(E)$ and $\Gamma(TM)^\ast \otimes_{C^\infty(M)} \Gamma(E) \cong \operatorname{Hom}_{C^\infty(M)}(\Gamma(TM), \Gamma(E))$ so the first definition is just a curried version of the second one.

[^2]: If this is the first time you are seeing this, then here is a quick justification. In the realm of finite-dimensional vector spaces, we have an isomorphism $V^\ast \otimes W \cong \operatorname{Hom}(V,W)$ and the map is given by $(\alpha \otimes w) \mapsto \alpha(-)w$. That is for $v \in V$ we have $(\alpha\otimes w)(v) = \alpha(v)w$.

[^3]: This property is often called tensoriality.

[^4]: The idea here is that $(\nabla_X s)(p)$ depends only on the values of $X$ and $s$ in an arbitarily small neighborhood of $p$. Just like derivative of a function $f : \Bbb R \to \Bbb R$ at $p \in \Bbb R$ depends only on the values of $f$ in a neighborhood of $p$.
