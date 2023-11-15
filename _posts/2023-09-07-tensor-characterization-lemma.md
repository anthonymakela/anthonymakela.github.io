---
layout: post
title: "Tensor Characterization Lemma"
categories: [Differential Geometry]
published: false
mathjax: true
excerpt_separator: <!--more-->
---

Some of my classmates found it challenging to grasp the concept that the torsion tensor, defined as $T(X,Y) = \nabla_X Y - \nabla_Y X - [X,Y]$ is a $(1,2)$-tensor field. Therefore, the aim of this post is to elucidate this concept. I'll try to avoid abstract nonsense as much as possible to make things more concrete.

<!--more-->

Let's quickly recall few facts about tensors. For the remaining of this post $M$ will denote a smooth manifold of dimension $n$ and $V$ a finite-dimensional vector space of dimension $n$ as well.

A <b>covariant $k$-tensor</b> on $V$ is a multilinear map

$$
F : \underbrace{V \times \dots \times V}_{k \text{ times }} \to \Bbb R.
$$

Similarly a <b>contravariant $k$-tensor</b> on $V$ is a multilinear map

$$
F : \underbrace{V^\ast \times \dots \times V^\ast}_{k \text{ times }} \to \Bbb R.
$$

Often times we need to consider tensors of mixed valence so a mixed tensor of type $(k,l)$ i.e. <b>$k$-contravariant</b> and <b>$l$-covariant</b> is a multilinear map 

$$
F : \underbrace{V^\ast \times \dots \times V^\ast}_{k \text{ times }} \times  \underbrace{V \times \dots \times V}_{l \text{ times }} \to \Bbb R.
$$

If $(e_i)$ is a basis for $V$ and $(\varepsilon^j)$ the dual basis, a basis for the space tensors of type $(k,l)$ is given by the set of tensors of the form

$$
e_{i_1}\otimes\dots\otimes e_{i_k} \otimes \varepsilon^{j_1} \otimes \dots \otimes \varepsilon^{j_l}.
$$

It follows that any $(k,l)$-tensor $F$ can be written as

$$
F = F^{i_1,\dots,i_k}_{j_1,\dots,j_l}e_{i_1}\otimes\dots\otimes e_{i_k} \otimes \varepsilon^{j_1} \otimes \dots \otimes \varepsilon^{j_l}
$$

where 

$$
F^{i_1,\dots,i_k}_{j_1,\dots,j_l} = F(\varepsilon^{i_1},\dots,\varepsilon^{i_k}, e_{j_1},\dots,e_{j_l}).
$$

Notice the switching of the indices. The following calculation may or may not make this a bit more clear. Let $\omega^1,\dots,\omega^k \in V^\ast$ and $v_1,\dots,v_l \in V$. Then

$$
\begin{align*}
F(\omega^1,\dots,\omega^k, v_1,\dots,v_l) &= F\left(\sum_{i_1} \omega^1_{i_1}\varepsilon^{i_1}, \dots, \sum_{i_k}\omega^k_{i_k}\varepsilon^{i_k}, \sum_{j_1} v_1^{j_1}e_{j_1},\dots,\sum_{j_l} v_1^{j_l}e_{j_l} \right) \\
&= \sum_{i_1,\dots,i_k}\sum_{j_1,\dots,j_l} \omega^1_{i_1}\dots\omega^k_{i_k} v_1^{j_1}\dots\ v_l^{j_l}F(\varepsilon^{i_1}, \dots, \varepsilon^{i_k}, e_{j_1},\dots,e_{j_l}) \\
&= \sum_{i_1,\dots,i_k}\sum_{j_1,\dots,j_l} F(\varepsilon^{i_1}, \dots, \varepsilon^{i_k}, e_{j_1},\dots,e_{j_l})e_{i_1}\otimes\dots\otimes e_{i_k} \otimes \varepsilon^{j_1} \otimes \dots \otimes \varepsilon^{j_l}(\omega^1,\dots,\omega^k, v_1,\dots,v_l).
\end{align*}
$$

Note that here

$$
\begin{align*}
e_{i_1}\otimes\dots\otimes e_{i_k} \otimes \varepsilon^{j_1} \otimes \dots \otimes \varepsilon^{j_l}(\omega^1,\dots,\omega^k, v_1,\dots,v_l) &= \omega^1(e_{i_1})\dots\omega^k(e_{i_k})\varepsilon^{j_1}(v_1)\dots\varepsilon^{j_l}(v_l) \\
&= \omega^1_{i_1}\dots\omega^k_{i_k}v_1^{j_1}\dots v_l^{j_l}.
\end{align*}
$$

I'm just going to take a moment to elaborate on this "switching" between the vector space and it's dual since it might result in some confusion. Effectively what is happening is that we are identifying a multilinear map 

$$ 
\underbrace{V^\ast \times \dots \times V^\ast}_{k \text{ times }} \times  \underbrace{V \times \dots \times V}_{l \text{ times }} \to \Bbb R
$$

with an element in

$$
\underbrace{V \otimes \dots \otimes V}_{k \text{ times }} \otimes  \underbrace{V^\ast \otimes \dots \otimes V^\ast}_{l \text{ times }}.
$$

For example if $F = v \otimes \omega \in V \otimes V^\ast$, then $F$ "eats" a pair $(\alpha, u)$ in $ V^\ast \times V$ not in $ V \times V^\ast$ in order for $F(\alpha,u) = v\otimes \omega(\alpha,u) = \alpha(v)\omega(u)$ to make sense.

Now something related to the actual aim of this post.

<div class="proposition">
There is a natural basis independent isomorphism between the space $T^{(k+1,l)}(V)$ of $(k+1,l)$-tensors over $V$ and the space of multilinear maps
$$
\underbrace{V^\ast \times \dots \times V^\ast}_{k \text{ times }} \times  \underbrace{V \times \dots \times V}_{l \text{ times }} \to V.
$$
Note the target here is $V$ instead of the underlying field of $V$.
</div>

<div class="proof">
Let's first go over the case with $k = 0$ and $l = 1$ as it will be quite informative. In this case the space of multilinear maps $V \to V$ is just $\operatorname{End}(V)$. Define $\Phi : \operatorname{End}(V) \to T^{(1,1)}(V)$ by
$$
\Phi(f)(\omega,v) = \omega(f(v)).
$$
Linearity of this map is straightforward and to see that it is injective, if $f \in \ker(\Phi)$, then 

$$
\Phi(f)(\omega,v) = 0 \implies \omega(f(v)) = 0
$$
and since this holds for all $\omega \in V^\ast$ we have $f(v) = 0$ for every $v \in V$ which means that $f = 0$. Surjectivity follows since $\dim \operatorname{End}(V) = n^2$ and likewise $\dim T^{(1,1)}(V) = n^2$.

For the general case define $\Phi$ as

$$
\Phi(f)(\omega^1,\dots,\omega^{k+1}, v_1,\dots,v_l) = \omega^{k+1}(f(\omega^1,\dots,\omega^k,v_1,\dots,v_l))
$$

The proof that this is an isomorphism is the same as for the case $k=0$ and $l = 1$.
</div>

Now onto tensor fields. 

<div>
A $(k,l)$-tensor field on a manifold $M$ is a section of the vector bundle
$$
\left(\bigotimes^k TM\right) \otimes \left(\bigotimes^l T^\ast M \right)
$$
</div>

An example you might have already encountered is the metric tensor $g$ on a Riemannian manifold $M$. Infact $g$ is a smooth $(0,2)$-tensor field.

Similarly any differential $k$-form is a smooth section of the exterior bundle $\bigotimes^k(T^\ast M)$ that corresponds to an alternating $k$-linear and is thus a smooth $(0,k)$-tensor field. To be more specific a differential $k$-form is a section of the exterior bundle $\bigwedge^k T^\ast M$.

An important property that tensor fields have is that they are multilinear over $C^\infty(M)$. If $F$ is a $(k,l)$-tensor field, then for $1$-forms $\omega^1,\dots,\omega^k$ and vector fields $X_1,\dots,X_l$ the <i>function</i> $F(\omega^1,\dots,\omega^k, X_1,\dots,X_l)$ from $M$ to $\Bbb R$ is smooth.

All in all we see that $F$ induces a map multilinear map 

$$
\widetilde{F} : \underbrace{\Gamma(T^\ast M) \times \dots \times \Gamma(T^\ast M)}_{k \text{ times }} \times \underbrace{\Gamma(TM) \times \dots \times \Gamma(TM)}_{l \text{ times }} \to C^\infty(M)
$$

over $C^\infty(M)$. The gist of this post is that the converse is true as well. 

<div class="lemma">
(<b>Tensor Characterization Lemma</b>) A map

$$
F : \underbrace{\Gamma(T^\ast M) \times \dots \times \Gamma(T^\ast M)}_{k \text{ times }} \times \underbrace{\Gamma(TM) \times \dots \times \Gamma(TM)}_{l \text{ times }} \to C^\infty(M)
$$

is induced by a smooth $(k,l)$-tensor field if and only if it is multilinear over $C^\infty(M)$. Likewise a map 

$$
F : \underbrace{\Gamma(T^\ast M) \times \dots \times \Gamma(T^\ast M)}_{k \text{ times }} \times \underbrace{\Gamma(TM) \times \dots \times \Gamma(TM)}_{l \text{ times }} \to \Gamma(TM)
$$

is induced by a smooth $(k+1,l)$-tensor field if and only if it is multilinear over $C^\infty(M)$.
</div>

<div class="proof">
Suppose that 

$$
F : \underbrace{\Gamma(T^\ast M) \times \dots \times \Gamma(T^\ast M)}_{k \text{ times }} \times \underbrace{\Gamma(TM) \times \dots \times \Gamma(TM)}_{l \text{ times }} \to C^\infty(M)
$$

is multilinear over $C^\infty(M)$. For each $p \in M$ there is a unique $\Bbb R$-multilinear map 

$$
F_p : \underbrace{T^\ast_p M \times \dots \times T^\ast_p M}_{k \text{ times }} \times \underbrace{T_pM \times \dots \times T_pM}_{l \text{ times }} \to \Bbb R
$$

such that for all $\omega^1,\dots,\omega^k \in \Gamma(T^\ast M) \times \dots \times \Gamma(T^\ast M)$ and $X_1,\dots,X_l \in \Gamma(TM) \times \dots \times \Gamma(TM)$

$$
F_p(\omega^1_p,\dots,\omega^k_p, X_{1,p},\dots,X_{l,p}) = F(\omega^1,\dots,\omega^k, X_{1},\dots,X_{l})(p).
$$

Now the universal property of tensor products yields that the multilinear map $F_p$ corresponds to a unique multilinear map 
$$
\widetilde{F}_p : \underbrace{T^\ast_p M \otimes \dots \otimes T^\ast_p M}_{k \text{ times }} \otimes \underbrace{T_pM \otimes \dots \otimes T_pM}_{l \text{ times }} \to \Bbb R
$$
such that $\widetilde{F}_p(\omega^1_p \otimes \dots \otimes \omega^k_p, X_{1,p} \otimes \dots \otimes X_{l,p}) = F(\omega^1,\dots,\omega^k, X_{1},\dots,X_{l})(p)$.

Now since $\widetilde{F}_p \in \operatorname{Hom}(\underbrace{T^\ast_p M \otimes \dots \otimes T^\ast_p M}_{k \text{ times }} \otimes \underbrace{T_pM \otimes \dots \otimes T_pM}_{l \text{ times }}, \Bbb R)$ and

$$
\begin{align*}
\operatorname{Hom}(\underbrace{T^\ast_p M \otimes \dots \otimes T^\ast_p M}_{k \text{ times }} \otimes \underbrace{T_pM \otimes \dots \otimes T_pM}_{l \text{ times }}, \Bbb R) &\cong \left(T^\ast_p M \otimes \dots \otimes T^\ast_p M \otimes T_pM \otimes \dots \otimes T_pM \right)^\ast \\
&= \underbrace{T_p M \otimes \dots \otimes T_p M}_{k \text{ times }} \otimes  \underbrace{T^\ast_pM \otimes \dots \otimes T^\ast_pM}_{l \text{ times }}. 
\end{align*}
$$

In other words $\widetilde{F}_p$ is a section of $\left(\bigotimes^k TM\right) \otimes \left(\bigotimes^l T^\ast M \right)$ i.e. a $(k,l)$-tensor field.

Similarly if

$$
F : \underbrace{\Gamma(T^\ast M) \times \dots \times \Gamma(T^\ast M)}_{k \text{ times }} \times \underbrace{\Gamma(TM) \times \dots \times \Gamma(TM)}_{l \text{ times }} \to \Gamma(TM)
$$

is multilinear over $C^\infty(M)$, then for each $p \in M$ we get a unique $\Bbb R$-multilinear map on the fibers

$$
F_p : \underbrace{T_p^\ast M \times \dots \times T^\ast_p M}_{k \text{ times }} \times \underbrace{T_pM \times \dots \times T_pM}_{l \text{ times }} \to T_pM.
$$

Again the universality of the tensor product yields a unique map 

$$
\widetilde{F}_p : \underbrace{T_p^\ast M \otimes \dots \otimes T^\ast_p M}_{k \text{ times }} \otimes \underbrace{T_pM \otimes \dots \otimes T_pM}_{l \text{ times }} \to T_pM
$$


</div>


