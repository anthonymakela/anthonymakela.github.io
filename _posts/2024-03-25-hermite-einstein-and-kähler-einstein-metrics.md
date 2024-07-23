---
layout: post
title: "Hermite-Einstein Metrics and Stability"
categories: [Complex Geometry, Differential Geometry]
mathjax: true
published: true
excerpt_separator: <!--more-->
---

Last time we went over holomorphic connections and the Atiyah class on a holomorphic vector bundle. At the end of the post, we were looking at some of the properties of holomorphic vector bundles with vanishing Atiyah class and their correspondence with holomorphic bundles that admit flat connections. In one of the propositions, I mentioned something called a <i>Hermite-Einstein</i> metric, which we have not yet discussed. This, and the stability of vector bundles will be the topic for today.

<!--more-->

---

As the name might suggest, we are stepping a bit on the physicist's territory here. I'm by no means a physicist so I'm going to keep the actual physics to a minimum. That being said, let's kick this off with some physics and more specifically with the Einstein field equations. Suppose that $(X,g)$ is a Riemannian manifold. The Einstein field equations are given by 

$$
\operatorname{Ric} = \frac{1}{2}S + T,
$$

where $S$ is the scalar curvature of $g$ and $T$ the so-called stress-energy tensor. Now in our case $T \equiv 0$ and for the mathematician's version of this we state the following definition.

<div class="definition">
A Riemannian manifold $(X,g)$ is called <i>Einstein</i> if the Ricci tensor $\operatorname{Ric}$ is proportional to the metric $g$. That is

$$
\operatorname{Ric} = \lambda g,
$$

for $\lambda \in \Bbb R$.
</div>

Consider now a compact Hermitian manifold $(X,g)$ and the fundamental form $\omega = g(J(-), -)$. By definition, $(X,g)$ is Kähler if and only if $d\omega = 0$ or equivalently if $J$ is parallel with respect to the Levi-Civita connection of $g$. Now $g$ can be viewed as a Hermitian metric on the tangent bundle of $X$ and instead of asking if the Ricci curvature of the Levi-Civita connection on the tangent bundle of $X$ is proportional to $g$, we can ask the same question about the curvature $F_\nabla$ of a Chern connection $\nabla$ associated to a Hermitian metric on <i>any</i> holomorphic vector bundle $(E,h)$ over $(X,g)$.


Clearly, we are trying to generalize the definition above and since it depends on the Ricci curvature, we should probably start with the curvature tensor $F_\nabla$ of $E$. This is an $\operatorname{End}(E)$-valued $2$-form so locally on a framed open set we can write[^1]

$$
\begin{align*}
F_\nabla &= \sum \Omega^i_j \otimes \varepsilon^j \otimes e_i \\
&= \sum \left(\sum R^i_{j\alpha\bar{\beta}} dz^\alpha \wedge d\bar{z}^\beta\right) \otimes \varepsilon^j \otimes e_i.
\end{align*}
$$

Now, the Ricci tensor is given by tracing over the Levi-Civita connection on the tangent bundle of $X$. We'll do something similar here and consider the trace/contraction of $F_\nabla$​ with the fundamental form $\omega$. However, tracing with the form $\omega$ is not as straightforward as it sounds. What we'll do is consider the adjoint $\Lambda_\omega$ of the Lefschetz operator to define this. Recall that the Lefschetz operator $L_\omega : \Omega^{p,q}(X) \to \Omega^{p+1,q+1}(X)$ is given by 

$$
\alpha \mapsto \alpha \wedge \omega.
$$

Let $e_k:\Omega^{p,q}(X) \to \Omega^{p+1,q}(X)$ be the operator given by $\alpha \mapsto dz^k\wedge \alpha$ and define $\bar{e}_k:\Omega^{p,q}(X) \to \Omega^{p,q+1}(X)$ similarly. Recall now also that the wedge product has the interior product as its adjoint. Denote these by $\iota_k$ and $\bar{\iota}_k$ respectively. Now 

$$
\begin{align*}
L_\omega(\alpha) &= \alpha \wedge \omega \\
&= ig_{j\bar{k}}\alpha\wedge dz^j\wedge d\bar{z}^k \\
&= \sum_{j,k} ig_{j\bar{k}}e_j\bar{e}_k(\alpha).
\end{align*}
$$

The adjoint $\Lambda_\omega$ is thus given by 

$$
\Lambda_\omega = -i\sum_{j,k}g^{j\bar{k}}\bar{\iota}_k\iota_j.
$$

Applying this yields

$$
\begin{align*}
\Lambda_\omega F_\nabla &= \Lambda_\omega\left(\sum \Omega^i_j \otimes \varepsilon^j \otimes e_i\right) \\
&= \Lambda_\omega\left(\sum \left(\sum R^i_{j\alpha\bar{\beta}} dz^\alpha \wedge d\bar{z}^\beta\right) \otimes \varepsilon^j \otimes e_i\right) \\
&= \sum \left(\sum R^i_{j\alpha\bar{\beta}} \Lambda_\omega(dz^\alpha \wedge d\bar{z}^\beta)\right) \otimes  \varepsilon^j \otimes e_i \\
&= -i\sum \left(\sum g^{\alpha\bar{\beta}}R^i_{j\alpha\bar{\beta}} \right) \otimes  \varepsilon^j \otimes e_i. 
\end{align*}
$$

Note that multiplying by $i$ gives $i\Lambda_\omega F_\nabla = \sum \left(\sum g^{\alpha\bar{\beta}}R^i_{j\alpha\bar{\beta}} \right) \otimes  \varepsilon^j \otimes e_i$. In literature[^2] you might see $\Lambda_\omega F_\nabla$ being denoted by $K$ and called the <b>mean curvature</b>. This is defined by setting $K^i_j = g^{\alpha\bar{\beta}}R^i_{j\alpha\bar{\beta}}$ and $K(\xi) = K^i_j\xi^je_i$, for a section $\xi = \xi^ie_i$. There is also the <b>mean curvature form</b> obtained by setting $K_{j\bar{k}} = h_{i\bar{k}}K^i_j$ and $\hat{K}(\xi,\eta) = K_{j\bar{k}}\xi^j\bar{\eta}^k$.

Using this we'll define the Hermite-Einstein condition as follows:

<div class="definition">
An Hermitian metric $h$ on a holomorphic vector bundle $E$ is called <i>weakly Hermite-Einstein</i> if
$$
i\Lambda_\omega F_\nabla = \lambda\operatorname{id}_E
$$  
for some real function $\lambda$. If $\lambda$ is a constant, we say that $h$ is <i>Hermite-Einstein</i>. Here $\Lambda_\omega$ is the contraction by $\omega$.
</div>

When $E = TX$, we can regard $\Lambda_\omega F_\nabla$ as the Ricci tensor of $g$ after lowering an index.
<div class="proposition">
<ol>
    <li>
    Every Hermitian line bundle $(L, h)$ over a complex manifold $X$ satisfies the weak Einstein condition (with respect to any Hermitian metric $g$ on $X$).
    </li>
    <li>
    If $(E, h)$ over $(X, g)$ satisfies the (weak) Einstein condition with factor $\lambda$, then the dual bundle $(E^\ast, h^\ast)$ satisfies (weak) Einstein condition with factor $-\lambda$.
    </li>
    <li>
    If $(E_1, h_1)$ and $(E_2, h_2)$ over $(X, g)$ satisfy the (weak) Einstein condition with factor $\lambda_1$ and $\lambda_2$, respectively, then their tensor product $(E_1 \otimes E_2, h_1 \otimes h_2)$ satisfies the (weak) Einstein condition with factor $\lambda_1 + \lambda_2$.
    </li>
    <li>
    The Whitney sum $(E_1\oplus E_2, h_1 \oplus h_2)$ satisfies the (weak) Einstein condition with factor $\lambda$ if and only if both summands $(E_1, h_1)$ and $(E_2, h_2)$ satisfy the (weak) Einstein condition with the same factor $\lambda$.
    </li>
</ol>
</div>

<div class="proof">
<ol>
    <li>
    The curvature $F_\nabla$ of the Chern connection $\nabla$ is an imaginary $(1,1)$-form. It follows that $i\Lambda_\omega F_\nabla = \Lambda_\omega iF_\nabla$ is a real-valued function on $X$ and hence satisfies the weak Einstein condition.
    </li>
    <li>
    Suppose that $\nabla$ is the Chern connection on $E$ and $i\Lambda_\omega F_\nabla = \lambda\operatorname{id}_E$. Then the induced connection $\nabla^\ast$ on $E^\ast$ has curvature $F_{\nabla^\ast} = -F^T_\nabla$. Thus 
    $$
    i\Lambda_\omega F_{\nabla^\ast} = i\Lambda_\omega(-F^T_\nabla) = i\Lambda_\omega(F^T_\nabla) = -\lambda\operatorname{id}_E,
    $$
    i.e. the dual bundle $(E^\ast, h^\ast)$ satisfies (weak) Einstein condition with factor $-\lambda$.
    </li>
    <li>
    Recall that on $E_1 \otimes E_2$, the curvature is given by $F_{\nabla_1 \otimes \nabla_2} = F_{\nabla_1} \otimes \operatorname{id}_{E_2} + \operatorname{id}_{E_1} \otimes F_{\nabla_2}$. We obtain
    $$
    \begin{align*}
    i\Lambda_\omega F_{\nabla_1 \otimes \nabla_2} &= i\Lambda_\omega(F_{\nabla_1} \otimes \operatorname{id}_{E_2} + \operatorname{id}_{E_1} \otimes F_{\nabla_2}) \\
    &= i\Lambda_\omega(F_{\nabla_1})\otimes \operatorname{id}_{E_2} + \operatorname{id}_{E_2} \otimes  i\Lambda_\omega(F_{\nabla_2}) \\
    &= \lambda_1 \operatorname{id}_{E_1} \otimes \operatorname{id}_{E_2} + \operatorname{id}_{E_1} \otimes \lambda_2\operatorname{id}_{E_2} \\
    &= (\lambda_1+\lambda_2)\operatorname{id}_{E_1 \otimes E_2}.
    \end{align*}
    $$
    </li>
    <li>
    If $(E_1\oplus E_2, h_1 \oplus h_2)$ satisfies the (weak) Einstein condition with factor $\lambda$, then given the connection $\nabla = \nabla_1 + \nabla_2$ on $E_1\oplus E_2$, the curvature is given by $F_\nabla = F_{\nabla_1} + F_{\nabla_2}$. This gives
    $$
    \begin{align*}
    \lambda\operatorname{id}_{E_1 \oplus E_2} &= i\Lambda_\omega F_\nabla \\
    &= i\Lambda_\omega(F_{\nabla_1} + F_{\nabla_2}) \\
    &= i\Lambda_\omega F_{\nabla_1} + i\Lambda_\omega F_{\nabla_2}.
    \end{align*}
    $$
    It follows that $i\Lambda_\omega F_{\nabla_j} = \lambda\operatorname{id}_{E_j}$. Conversely, if both summands $(E_1, h_1)$ and $(E_2, h_2)$ satisfy the (weak) Einstein condition with the same factor $\lambda$, then 
    $$
    \begin{align*}
    i\Lambda_\omega F_\nabla &= i\Lambda_\omega(F_{\nabla_1} + F_{\nabla_2}) \\
    &= i\Lambda_\omega F_{\nabla_1} + i\Lambda_\omega F_{\nabla_2} \\
    &= \lambda\operatorname{id}_{E_1} +  \lambda\operatorname{id}_{E_2} \\
    &= \lambda\operatorname{id}_{E_1 \oplus E_2}.
    \end{align*}    
    $$
    </li>
</ol>
</div>

The Einstein condition imposes a strong restriction to possible sheaf morphisms. To see this we'll state the following useful result which is mostly based on the maximum principle by E. Hopf.

<div class="theorem">
Let $(E,h)$ be a Hermitian vector bundle over a compact Hermitian manifold $(X,g)$. Let $\nabla$ be the Chern connection of $E$, $F_\nabla$ its curvature, and $\hat{K}$ the mean curvature.
<ol>
    <li>
    If $\hat{K}$ is negative semi-definite everywhere on $X$, then $\nabla \xi = 0$ for any holomorphic section $\xi$ of $E$ and $\hat{K}(\xi,\xi) = 0$.
    </li>
    <li>
    If $\hat{K}$ negative semi-definite everywhere on $X$ and negative definite at some point of $X$, then $E$ admits no non-zero holomorphic sections.
    </li>
</ol>
</div>

<div class="proposition">
Let $(E_1, h_1)$ and $(E_2, h_2)$ be Hermitian vector bundles over a compact Hermitian manifold $(X, g)$ satisfying the (weak) Einstein condition
with factors $\lambda_1$ and $\lambda_2$, respectively. If $\lambda_2 < \lambda_1$, then there are no non-zero sheaf homomorphisms $f : E_1 \to E_2$.
</div>

<div class="proof">
Let $f : E_1 \to E_2$ be a morphism of sheaves. The map $f$ is a global holomorphic section of $E^\ast_1 \otimes E_2$, which satisfies the weak Einstein condition with factor $\lambda_2-\lambda_1$. Now Since $\lambda_2-\lambda_1 < 0$ we have that

$$
\begin{align*}
\Lambda_\omega F_{\nabla_1 \otimes \nabla_2} &= (\lambda_2-\lambda_1)\operatorname{id}_{E_1 \otimes E_2} \\
&<0,
\end{align*}
$$ 
i.e. $\Lambda_\omega F_{\nabla_1 \otimes \nabla_2}$ is negative definite and hence $f = 0$.
</div>

Generally speaking, these kinds of Hermite-Einstein metrics are not easy to describe, but they exist relatively frequently and the benefit is that those holomorphic bundles that admit such a metric can be described algebraically as we will see later on.

We'll now state and prove the Kobayashi-Lübke inequality and derive some interesting corollaries from it.

<div class="proposition">
Let $E$ be a holomorphic vector bundle of rank $k$ over a compact Hermitian manifold $(X,g)$. If $E$ admits a Hermite-Einstein metric, then
$$
\int_X (2kc_2(E) - (k-1)c^2_1(E)) \wedge \omega^{n-2} \ge 0.
$$
</div>


<div class="proof">
Since $E$ admits a Hermite-Einstein metric, the bundle $\operatorname{End}(E)$ with the naturally induced connection $\nabla'$ does so as well. Note that $\operatorname{End}(E) = E^\ast \otimes E$ and given the connection $\nabla$ on $E$ and $\nabla^\ast$ on $E^\ast$ the curvature on $E^\ast$ is given by $F_{\nabla^\ast} = F^T_\nabla$. It follows that

$$
\operatorname{tr}(F_\nabla) = -\operatorname{tr}(F_{\nabla^\ast}),
$$

and so 

$$
\begin{align*}
\operatorname{tr}(F_{\nabla'}) &= \operatorname{tr}(F_{\nabla^\ast} \otimes \operatorname{id}_E + \operatorname{id}_E \otimes F_{\nabla}) \\
&= \operatorname{tr}(F_{\nabla^\ast})k + k\operatorname{tr}(F_{\nabla}) \\
&= k(\operatorname{tr}(F_{\nabla^\ast}) - \operatorname{tr}(F_{\nabla^\ast})) \\
&= 0.
\end{align*}
$$

That is $c_1(\operatorname{End}(E), \nabla') = 0$. In particular $\Lambda_\omega F_{\nabla'} = 0$ since the Hermite-Einstein constant $\lambda$ is defined in terms of $c_1(\operatorname{End}(E), \nabla')$ as we will see shortly. It suffices to show that $ch_2(\operatorname{End}(E), \nabla')\wedge\omega^{n-2} \le 0$ pointwise, since 

$$
ch_2(\operatorname{End}(E), \nabla') = -(2kc_2(E,\nabla) - (k-1)c^2_1(E,\nabla)).
$$

Now

$$
\begin{align*}
ch_2(\operatorname{End}(E), \nabla') &= \frac{1}{2}(\underbrace{c^2_1(\operatorname{End}(E), \nabla')}_{0} - 2c_2(\operatorname{End}(E),\nabla')) \\
&= -c_2(\operatorname{End}(E),\nabla')) \\
&= -\frac{1}{8\pi^2} \operatorname{tr}(F^2_{\nabla'}) \\
&= \frac{1}{2} \left(\operatorname{tr}\left(\frac{i}{2\pi} F_{\nabla'} \wedge \left(\overline{\frac{i}{2\pi} F_{\nabla'}}\right)^T \right)\right)
\end{align*}
$$

and since $\Lambda_\omega F_{\nabla'} = 0$, we know that $F_{\nabla'}$ is a primitive real $(1,1)$-form. the Hodge-Riemann bilinear relation now yields

$$
\begin{align*}
ch_2(\operatorname{End}(E), \nabla') \wedge \omega^{n-2} &= \frac{1}{2} \left(\operatorname{tr}\left(\frac{i}{2\pi} F_{\nabla'} \wedge \left(\overline{\frac{i}{2\pi} F_{\nabla'}}\right)^T \right)\right) \wedge \omega^{n-2} \\
&\le 0
\end{align*}
$$

since for any matrix $A = [\alpha^i_j]$ of primitive $(1,1)$-forms the relation gives

$$
\operatorname{tr}\left(A \wedge \bar{A}^T\right )\wedge \omega^{n-2} = \sum_j \sum_k \alpha^j_k \wedge \bar{\alpha}^j_k \wedge \omega^{n-2} \le 0.
$$

</div>

What about the converse? If $E$ satisfies the above inequality, does it automatically admit a Hermite-Einstein metric? Due to Donaldson, Uhlenbeck, and
Yau, this question can be answered by studying the algebraic geometry of $E$. However, before we go into this we need to introduce the concept of <i>stability</i>.

---

On any bundle $E$ equipped with the Chern connection, one can express the curvature as

$$
F_\nabla = \frac{\operatorname{tr}(F_\nabla)}{\operatorname{rank}(E)}\operatorname{id} + F^\circ_\nabla,
$$

where $F^\circ_\nabla$ is the trace-free part of $F_\nabla$. Suppose now that $g$ is a Kähler metric, that is $\omega$ is closed. Note that $\omega$ is in this case also harmonic.

<div class="lemma">
A closed $(1,1)$-form $\xi$ is harmonic if and only if $\Lambda_\omega \xi$ is locally constant.
</div>

<div class="proof">
Suppose that $\xi$ is harmonic. Recall that $\omega$ is parallel and hence $\xi \wedge \omega^{n-1}$ is harmonic. Since the only harmonic form of top degree up to a constant factor is $\omega^n$, we conclude that $\xi \wedge \omega^{n-1} = c\omega^n$ for some constant $c$. It follows that $\Lambda_\omega \xi$ is constant. Conversely if $\Lambda_\omega \xi$ is constant, then the Kähler identity $[\Lambda, \partial] = i\bar{\partial}^\ast$ gives

$$
\begin{align*}
0 &= -\partial \Lambda\xi \\
&= [\Lambda, \partial]\xi - \Lambda\partial \xi \\
&= i\bar{\partial}^\ast \xi,
\end{align*}
$$

and so $\bar{\partial}^\ast \xi = 0$ yields that $\xi$ is harmonic.
</div>

Using the above lemma, we conclude that $(E,h)$ is Hermite-Einstein if and only if $\Lambda_\omega F^\circ_\nabla = 0$ and $\operatorname{tr}(F_\nabla)$ is harmonic. Indeed, if $(E,h)$ is Hermite-Einstein, then since $\Lambda_\omega F_\nabla = \lambda\operatorname{id}$ we have from

$$
\Lambda_\omega F_\nabla = \left(\frac{1}{\operatorname{rank}(E)} \Lambda_\omega\operatorname{tr}(F_\nabla)\right)\operatorname{id} + \Lambda_\omega F^\circ_\nabla,
$$

that $\Lambda_\omega F^\circ_\nabla = 0$. This also implies that $\Lambda_\omega(\operatorname{tr}(F_\nabla))$ is constant, which by the above lemma gives harmonicity for $\operatorname{tr}(F_\nabla)$. Conversely, if $\Lambda_\omega F^\circ_\nabla = 0$ and $\operatorname{tr}(F_\nabla)$ is harmonic,

$$
\Lambda_\omega F^\circ_\nabla = \Lambda_\omega F_\nabla - \left(\frac{1}{\operatorname{rank}(E)} \Lambda_\omega \operatorname{tr}(F_\nabla)\right)\operatorname{id}
$$

gives $ \Lambda_\omega F_\nabla = \lambda \operatorname{id}$ when we set $\frac{1}{\operatorname{rank}(E)} \Lambda_\omega\operatorname{tr}( F_\nabla) = \lambda$. The harmonicity of $\operatorname{tr}(F_\nabla)$ yields that $\frac{1}{\operatorname{rank}(E)} \Lambda_\omega \operatorname{tr}(F_\nabla)$ is constant. 

It's not too difficult to see[^3] that the metric $h$ is Hermite-Einstein if and only if

$$
iF_\nabla \wedge \omega^{n-1} = i\frac{\lambda}{n} \omega^n \operatorname{id}_E.
$$

Taking traces gives

$$
2\pi ic_1(E) \wedge \omega^{n-1} = i\frac{\operatorname{rank}(E)\cdot \lambda}{n}\omega^n,
$$

and furthermore

$$
\lambda  = 2\pi n \cdot \left(\int_X [\omega]^n\right)^{-1}\cdot \frac{\int_X c_1(E)\wedge [\omega]^{n-1}}{\operatorname{rank}(E)}.
$$

<div class="definition">
The <b>slope</b> of a vector bundle $E$ with respect to the Kähler form $\omega$ is defined by
$$
\mu(E) := \frac{\int_X c_1(E)\wedge [\omega]^{n-1}}{\operatorname{rank}(E)}.
$$
</div>

The number $\int_X c_1(E)\wedge [\omega]^{n-1}$ is often called the degree of $E$ and denoted by $\deg(E)$. Having defined the slope of a vector bundle, we are ready to define stability. The origins of this trace back to David Mumford's work on Geometric Invariant Theory.

<div class="definition">
A holomorphic vector bundle $E$ over a compact Kähler manifold $X$ is <b>stable</b> if and only if
$$
\mu(F) < \mu(E)
$$
for any proper non-trivial $\mathcal{O}_X$-subsheaf $F \subset E$.
</div>

Few remarks are in place here. Note that the definition depends on the class $[\omega]$ of the chosen Kähler form on $X$. Secondly, we've only defined this for vector bundles and not arbitrary $\mathcal{O}_X$-sheaves. It is not difficult to correct the definition in this case, but I won't be diving on to that here.

There are also notions of <i>polystability</i> and <i>semi-stability</i>. A holomorphic vector bundle $E$ is called polystable if 

$$
E = \bigoplus E_i,
$$

where $E_i$'s satisfy $\mu(E) = \mu(E_i)$. The following result shows that the algebraic geometry of a vector bundle determines whether or not a Hermite-Einstein metric exists.

<div class="theorem" text="(Donaldson, Uhlenbeck, Yau)">
A holomorphic vector bundle $E$ on a compact Kähler manifold $X$ admits a Hermite-Einstein metric if and only if $E$ is polystable.
</div>

---

To get some feel for stable vector bundles, let's consider Riemann surfaces. Actually, in higher dimensional cases, studying these becomes relatively difficult. For the remaining of this post, $X$ denotes a compact Riemann surface. Our aim is to show that every holomorphic vector bundle $E$ over a compact Riemann surface has a unique maximal semi-stable subbundle.

<div class="lemma">
Given a holomorphic vector bundle $E$ over a compact Riemann surface $X$, there is a positive integer $q$ such that if $L$ is a line bundle over $X$ with $\deg(L) \ge q$, then $\operatorname{Hom}(L,E)$ has no non-zero holomorphic sections.
</div>

<div class="proof">
When $X$ is a Riemann surface, $\deg(L) = c_1(L)$. Let $H$ be an ample line bundle over $X$ with a Hermitian structure whose curvature is positive. Fix also a Hermitian structure on $E$ and choose a positive integer $p$ such that the mean curvature $K$ of $H^{-m} \otimes E$ is negative for $m \ge p$. Recall now that in this case $H^{-m} \otimes E = \operatorname{Hom}(H^m, E)$ admits no non-zero sections, i.e.

$$
H^0(X,\operatorname{Hom}(H^m, E)) = H^0(X, H^{-m} \otimes E) = 0.
$$

By the Riemann-Roch formula, for any line bundle $L$ we have

$$
\dim H^0(X, H^{-p} \otimes L) \ge \deg(L) -p\deg(H)+1-g,
$$

where $g$ is the genus of $X$. Hence

$$
H^0(X, \operatorname{Hom}(H^p,L)) \ne 0,
$$

if $\deg(L) \ge g + p\deg(H)$. It follows that

$$
H^0(X,\operatorname{Hom}(L,E)) = 0,
$$

if $\deg(L) \ge g + p\deg(H)$.

</div>

<div class="lemma">
Given a holomorphic vector bundle $E$ over a compact Riemann surface $X$, there is an integer $m$ such that
$$
\mu(F) \le m
$$
for all holomorphic subbundles $F$ of $E$.
</div>

<div class="proof">
Applying the previous lemma to $\bigwedge^s E$, let $q(s)$ be the integer given by the lemma. Let $F$ be a subbundle of rank $s$. The injection $F \to E$ induces an injection $\bigwedge^s F \to \bigwedge^s E$. We have that $\deg\left(\bigwedge^s F\right) < q(s)$. Letting $m = \max_{s=1,\dots,k}\{q(s)/s\}$ we conclude the result.
</div>


<div class="proposition">
Given a holomorphic vector bundle $E$ over a compact Riemann surface $X$, there is a unique subbundle $E_1$ such that for every subbundle
$F$ of $E$ we have
<ol>
    <li>
    $\mu(F) \le \mu(E_1)$
    </li>
    <li>
    $\operatorname{rank}(F) \le \operatorname{rank}(E_1)$ if $\mu(F) = \mu(E_1)$.
    </li>
</ol>
We call $E_1$ the maximal semi-stable subbundle of $E$. 
</div>

<div class="proof">
The existence follows from the above lemma. From the characterizing properties of $E_1$ it is also clear that $E_1$ is semi-stable. To prove the uniqueness, let $E'_1$ be another subbundle satisfying 1. and 2. Let $p : E \to E/E'_1$ be the projection. Then $p(E_1) \ne 0$. Since $p(E_1)$ itself may not be a subbundle of $E/E'_1$, we consider the subbundle $G$ of $E/E'_1$ generated by $p(E_1)$. To be a bit more elaborate, let $e_1,\dots,e_m$ be a local holomorphic frame for $E_1$. Let $k$ be the rank of $p(E_1)$. Consider
$$
p(e_{i_1}) \wedge \dots \wedge p(e_{i_k}),
$$
for $i_1<\dots< i_k $. These holomorphic sections of $\bigwedge^k(E/E'_1)$ define a rank $k$ subbundle of $E/E'_1$ except where they all vanish. Wherever they all vanish, we factor out their common zeros, this is possible since $\dim X = 1$. Then they define a rank $k$ subbundle $G$ of $E/E'_1$. Define the subbundle $F$ of $E_1$ by the “locally defined” exact sequence 
$$
0 \longrightarrow F \longrightarrow E_1 \longrightarrow G \longrightarrow 0.
$$
Since $E_1$ is semi-stable, $\mu(F) \le \mu(E_1)$, or equivalently $\mu(E_1) \le \mu(G)$. On the other hand, we have an exact sequence
$$
0 \longrightarrow E'_1 \longrightarrow p^{-1}(G) \longrightarrow G \longrightarrow 0.
$$
From the properties 1. and 2. for $E'_1$, we have $\mu(p^{-1}(G)) < \mu(E'_1)$, i.e. 
$$
\frac{\deg(G) + \deg(E'_1)}{\operatorname{rank}(G) + \operatorname{rank}(E'_1)} < \frac{\deg(E'_1)}{\operatorname{rank}(E'_1)}.
$$
This gives $\mu(G) < \mu(E'_1) = \mu(E_1)$, a contradiction.
</div>

---

Before we part ways, let's discuss bundles admitting a Hermite-Einstein metric over Riemann surfaces. Let $(E,h)$ be a Hermitian vector bundle over a Riemann surface $X$. Let $g = g_{1\bar{1}}dz^1 \otimes d\bar{z}^1$ be any Hermitian metric on $X$. The mean curvature of $E$ is given, in terms of its components by

$$
K^i_j = g^{1\bar{1}}R^i_{j1\bar{1}}.
$$

The weak Hermite-Einstein condition is in this case equivalent to

$$
R^i_{j1\bar{1}} = g_{1\bar{1}}\lambda\delta^i_j,
$$

where $\lambda$ is a real function. Any two Hermitian metrics on $X$ are conformal to each other and hence the weak Hermite-Einstein condition is independent of the choice of $g$. This yields the following.

<div class="proposition">
A Hermitian vector bundle $(E,h)$ over a Riemann surface $(X,g)$ satisfies the weak Hermite-Einstein condition if and only if it is projectively flat.
</div>

Let $F$ be a holomorphic subbundle of a Hermite-Einstein bundle $(E,h)$ over a compact Riemann surface $(X,g)$. If we denote the curvature forms of $(E,h)$ and $(F,h\vert_{F})$ by $\Omega$ and $\widetilde{\Omega}$, then the vector bundle analogue of the Gauss-Codazzi equation gives

$$
\widetilde{\Omega}^i_j = \Omega^i_j - \sum \omega^k_j \wedge \omega^k_i
$$

for $1\le i,j\le p < k \le r$, where $r$ is the rank of $E$ and $p$ the rank of $F$. The first Chern classes of $E$ and $F$ are given by

$$
c_1(E,h) = \frac{i}{2\pi} \sum_{j=1}^r \Omega^j_j, \quad c_1(F,h) = \frac{i}{2\pi} \sum_{j=1}^p \widetilde{\Omega}^j_j.
$$

Now $\Omega^i_j = \alpha\delta^i_j$ for a suitable $(1,1)$-form $\alpha$ and hence,

$$
\begin{align*}
&\deg(E) = \int_X c_1(E) = \frac{i}{2\pi}\int_X r\alpha, \\
&\deg(F) = \int_X c_1(F) = \frac{i}{2\pi}\int_X \left(p\alpha-\sum \omega^k_j \wedge \bar{\omega}^k_i\right) \\
&\mu(E) = \frac{i}{2\pi}\int_X \alpha \\
&\mu(F) = \frac{i}{2\pi}\int_X \alpha - \frac{i}{2p\pi}\int_X \sum \omega^k_j \wedge \bar{\omega}^k_i.
\end{align*}
$$

It follows that $\mu(F) \le \mu(E)$, and the equality holds if $\omega^k_j = 0$. If $\mu(F) = \mu(E)$, then

$$
E = F \oplus F^\perp,
$$

where $F^\perp$ is orthogonal to $F$. Both $F$ and $F^\perp$ satisfy the Einstein condition with the same factor as $E$. In particular,

$$
\mu(E) = \mu(F) = \mu(F^\perp).
$$

We obtain the following proposition.

<div class="proposition">
If $(E, h)$ is an Hermite-Einstein vector bundle over a compact Riemann surface $(X, g)$, then $E$ is semi-stable and decomposes into a direct
sum 
$$
E = E_1 \oplus \dots \oplus E_k
$$
of stable Einstein-Hermitian vector bundles $E_1, \dots , E_k$ such that $\mu(E) = \mu(E_1) = \dots = \mu(E_k)$.
</div>

To end this, I'll present some results related to the famous Narasimhan–Seshadri theorem. first and foremost,

<div class="theorem">
A holomorphic vector bundle $E$ over a compact Riemann surface $X$ is stable if and only if the associated projective bundle $P(E)$ comes from
an irreducible representation of the fundamental group $\pi_1(X)$ into the projective unitary group $PU(r)$, that is, if and only if $E$ admits a projectively flat Hermitian structure.
</div>

As a corollary, we obtain the following neat result.

<div class="theorem">
If $E$ is a stable vector bundle over a compact Riemann surface $(X, g)$, there is a Hermite-Einstein structure $h$ in $E$.
</div>

---

[^1]: The indices here might be a bit unusual. I'm denoting $R^{j}_{ik\bar{l}}\partial_j = R(\partial_k,\bar{\partial}_l)\partial_i$ when we consider the curvature on the tangent bundle and $R^{j}\_{i\alpha\bar{\beta}}e\_j = R(\partial\_\alpha,\bar{\partial}\_\beta)e\_i$ when $R$ is the curvature of on a general vector bundle with a local frame $e_1,\dots,e_k$.

[^2]: Especially in Kobayashi's texts.

[^3]: Recall that for a $(1,1)$-form $\alpha = i \sum \alpha_{j\bar{k}}dz^j \wedge d\bar{z}^k$ we have $\alpha \wedge \omega^{n-1} = \frac{1}{n}\left(\sum \alpha_{k\bar{k}}\right)\omega^n$.