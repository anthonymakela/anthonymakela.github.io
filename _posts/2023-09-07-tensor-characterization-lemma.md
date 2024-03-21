---
layout: post
title: "Tensor Characterization Lemma"
categories: [Differential Geometry]
mathjax: true
excerpt_separator: <!--more-->
---

Some of my classmates found it challenging to grasp the concept that the torsion tensor, defined as $T(X,Y) = \nabla_X Y - \nabla_Y X - [X,Y]$ is a $(1,2)$-tensor field. Therefore, the aim of this post is to elucidate this concept. I apologize in advance for the notational overload.

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

Notice the switching of the indices in the basis vectors. The following calculation may or may not make this a bit more clear. Let $\omega^1,\dots,\omega^k \in V^\ast$ and $v_1,\dots,v_l \in V$. Then

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

The key thing to keep in mind is that we have a one-to-one correspondence between multilinear maps 

$$ 
\underbrace{V^\ast \times \dots \times V^\ast}_{k \text{ times }} \times  \underbrace{V \times \dots \times V}_{l \text{ times }} \to \Bbb R
$$

and elements in

$$
\underbrace{V \otimes \dots \otimes V}_{k \text{ times }} \otimes  \underbrace{V^\ast \otimes \dots \otimes V^\ast}_{l \text{ times }}.
$$

For example if $F = v \otimes \omega \in V \otimes V^\ast$, then $F$ "eats" a pair $(\alpha, u)$ in $ V^\ast \times V$ not in $ V \times V^\ast$ in order for $F(\alpha,u) = v\otimes \omega(\alpha,u) = \alpha(v)\omega(u)$ to make sense.

---

Now, let's discuss something related to the actual aim of this post.

<div class="proposition">
There is a natural basis independent isomorphism between the space $T^{(k+1,l)}(V)$ of $(k+1,l)$-tensors over $V$ and the space of multilinear maps
$$
\underbrace{V^\ast \times \dots \times V^\ast}_{k \text{ times }} \times  \underbrace{V \times \dots \times V}_{l \text{ times }} \to V.
$$
Note the target here is $V$ instead of the underlying field of $V$.
</div>

<div class="proof">
Consider a multilinear map 

$$
F : \underbrace{V^\ast \times \dots \times V^\ast}_{k \text{ times }} \times  \underbrace{V \times \dots \times V}_{l \text{ times }} \to V.
$$

By the universal property of tensor products this induces a unique linear map

$$
\widetilde{F} : \underbrace{V^\ast \otimes \dots \otimes V^\ast}_{k \text{ times }} \otimes  \underbrace{V \otimes \dots \otimes V}_{l \text{ times }} \to V.
$$

such that $\widetilde{F}(\omega^1\otimes\dots\otimes \omega^k \otimes v_1\otimes\dots\otimes v_l) = F(\omega^1,\dots,\omega^k, v_1,\dots,v_l)$ for any $\omega^1,\dots,\omega^k, v_1,\dots,v_l \in V^\ast \times \dots \times V^\ast \times V \times \dots \times V$.

It follows that $\widetilde{F} \in \operatorname{Hom}(V^\ast \otimes \dots \otimes V^\ast \otimes V \otimes \dots \otimes V, V)$, but

$$
\begin{align*}
\operatorname{Hom}(\underbrace{V^\ast \otimes \dots \otimes V^\ast}_{k \text{ times }} \otimes \underbrace{V \otimes \dots \otimes V}_{l \text{ times }}, V) &\cong \left(V^\ast \otimes \dots \otimes V^\ast \otimes V \otimes \dots \otimes V\right)^\ast \otimes V \\
&= \underbrace{V \otimes \dots \otimes V}_{k+1 \text{ times }} \otimes \underbrace{V^\ast \otimes \dots \otimes V^\ast}_{l \text{ times }}
\end{align*}
$$

which concludes the result.

</div>

Before we march onto tensor fields let's go over a lemma we are going to need soon. 

<div class="lemma">
Let $E, F$ and $G$ be vector bundles over $M$. If

$$
\Phi : \Gamma(E) \times \Gamma(G) \to \Gamma(F)
$$

is a $C^\infty(M)$-bilinear map, then for any $p \in M$ there exists a unique $\Bbb R$-linear map on the fibers

$$
\Phi_p : E_p \times G_p \to F_p
$$

such that for every $s \in \Gamma(E)$ and $t \in \Gamma(G)$ we have

$$
\Phi_p(s(p),t(p)) = \Phi(s,t)(p).
$$
</div>

<div class="proof">
Let $(v,u) \in E_p \times G_p$ and choose sections $s \in \Gamma(E)$ and $t \in \Gamma(G)$ with $s(p) = v$ and $t(p) = u$. Define 
$$
\Phi_p(v,u) = \Phi(s,t)(p).
$$
We will first argue that this choice is independent of the sections $s$ and $t$. Suppose that $s'$ and $t'$ are two sections with $s'(p) = v$ and $t'(p) = u$, then $(s-s')(p) = 0$ and $(t-t')(p) = 0$ and since we know by our previous results <a href="https://anthonymakela.com/differential%20geometry/2023/08/01/local-operators.html" style="color:#680530; text-decoration: underline;">here</a> that $\Phi$ is a point operator it follows that $\Phi(s-s',t-t')(p) = 0$ which yields that

$$
\Phi(s,t)(p) = \Phi(s',t')(p).
$$

I will show that it's linear in the first arguement and the argument carries over similarly to the second argument mutatis mutandis. Let $v_1,v_2 \in E_p, u \in G_p$ and $a_1,a_2 \in \Bbb R$ as well as $s_i \in \Gamma(E)$ be global sections such that $s_i(p) = v_i$ and lastly $t \in \Gamma(G)$ with $t(p) = u$. We have that

$$
\begin{align*}
\Phi_p(a_1v_1+a_2v_2, u) &= \Phi(a_1s_1 + a_2s_2, t)(p) \\
&= a_1\Phi(s_1,t)(p) + a_2\Phi(s_2,t)(p) \\
&= a_1\Phi_p(v_1,u) + a_2\Phi(v_2,u)
\end{align*}
$$
which concludes the proof.
</div>

---

So onto tensor fields then.

<div>
A $(k,l)$-tensor field on a manifold $M$ is a section of the vector bundle
$$
\left(\bigotimes^k TM\right) \otimes \left(\bigotimes^l T^\ast M \right)
$$
</div>

An example you might have already encountered is the metric tensor $g$ on a Riemannian manifold $M$. Infact $g$ is a smooth $(0,2)$-tensor field.

Similarly any differential $k$-form is a smooth section of the exterior bundle $\bigotimes^k(T^\ast M)$ that corresponds to an alternating $k$-linear and is thus a smooth $(0,k)$-tensor field. To be more specific a differential $k$-form is a section of the exterior bundle $\Lambda^k T^\ast M$.

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
F : \Gamma(T^\ast M) \times \dots \times \Gamma(T^\ast M) \times \Gamma(TM) \times \dots \times \Gamma(TM) \to C^\infty(M)
$$

is multilinear over $C^\infty(M)$. For each $p \in M$ there is a unique $\Bbb R$-multilinear map 

$$
F_p : T^\ast_p M \times \dots \times T^\ast_p M \times T_pM \times \dots \times T_pM \to \Bbb R
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

Now since $\widetilde{F}_p \in \operatorname{Hom}(T^\ast_p M \otimes \dots \otimes T^\ast_p M \otimes T_pM \otimes \dots \otimes T_pM, \Bbb R)$ and

$$
\begin{align*}
\operatorname{Hom}(\underbrace{T^\ast_p M \otimes \dots \otimes T^\ast_p M}_{k \text{ times }} \otimes \underbrace{T_pM \otimes \dots \otimes T_pM}_{l \text{ times }}, \Bbb R) &\cong \left(T^\ast_p M \otimes \dots \otimes T^\ast_p M \otimes T_pM \otimes \dots \otimes T_pM \right)^\ast \\
&= \underbrace{T_p M \otimes \dots \otimes T_p M}_{k \text{ times }} \otimes  \underbrace{T^\ast_pM \otimes \dots \otimes T^\ast_pM}_{l \text{ times }}. 
\end{align*}
$$

In other words $\widetilde{F}$ is a section of $\left(\bigotimes^k TM\right) \otimes \left(\bigotimes^l T^\ast M \right)$ i.e. a $(k,l)$-tensor field.

Similarly if

$$
F : \Gamma(T^\ast M) \times \dots \times \Gamma(T^\ast M) \times \Gamma(TM) \times \dots \times \Gamma(TM) \to \Gamma(TM)
$$

is multilinear over $C^\infty(M)$, then for each $p \in M$ we get a unique $\Bbb R$-multilinear map on the fibers

$$
F_p : T_p^\ast M \times \dots \times T^\ast_p M \times T_pM \times \dots \times T_pM \to T_pM.
$$

Again the universality of the tensor product yields a unique map 

$$
\widetilde{F}_p : \underbrace{T_p^\ast M \otimes \dots \otimes T^\ast_p M}_{k \text{ times }} \otimes \underbrace{T_pM \otimes \dots \otimes T_pM}_{l \text{ times }} \to T_pM
$$

i.e. $\widetilde{F}_p \in \operatorname{Hom}(T_p^\ast M \otimes \dots \otimes T^\ast_p M \otimes T_pM \otimes \dots \otimes T_pM, T_pM)$, but

$$
\begin{align*}
\operatorname{Hom}(\underbrace{T_p^\ast M \otimes \dots \otimes T^\ast_p M}_{k \text{ times }} \otimes \underbrace{T_pM \otimes \dots \otimes T_pM}_{l \text{ times }}, T_pM) &\cong \left(T_p^\ast M \otimes \dots \otimes T^\ast_p M \otimes T_pM \otimes \dots \otimes T_pM \right)^\ast \otimes T_pM \\
&= \underbrace{T_p M \otimes \dots \otimes T_p M}_{k+1 \text{ times }} \otimes \underbrace{T^\ast_pM \otimes \dots \otimes T^\ast_pM}_{l \text{ times }}
\end{align*}
$$

and so $\widetilde{F}$ is a $(k+1,l)$-tensor field. We could have just as easily deduced this from the proposition above since we reduced this to the realm of vector spaces.
</div>

So after all this trouble it should be quite clear now why the torsion $T : \Gamma(TM) \times \Gamma(TM) \to \Gamma(TM)$ is a $(1,2)$-tensor field. We just identify it with the induced map we get from the Tensor Characterization Lemma.

Before I end this there might be a question on your mind that's bugging you (at least it was bugging me), what if we consider for example the curvature tensor $R$ of a vector bundle $E$ over $M$? We know that, for $X,Y \in \Gamma(TM)$ and $s \in \Gamma(E)$

$$
R(X,Y)s = \nabla_X\nabla_Y s - \nabla_Y\nabla_X s - \nabla_{[X,Y]}s \in \Gamma(E)
$$

So $R$ is a map $\Gamma(TM) \times \Gamma(TM) \times \Gamma(E) \to \Gamma(E)$. The issue now is that our lemma doesn't say anything about maps with target space something else than $\Gamma(TM)$ or $C^\infty(M)$. What can we do here? Looking at this on the fibers we have a map $R_p : T_pM \times T_pM \times E_p \to E_p$ which we can curry to get an alternating bilinear map $R_p : T_pM \times T_pM \to \operatorname{Hom}(E_p,E_p)$. So it would seem that $R$ is a section of the bundle $\left(\bigotimes^2 T^\ast M \right) \otimes \operatorname{End}(E)$. We call such a thing an $\operatorname{End}(E)$-valued $(0,2)$-tensor field.

In general if $E$ is a vector bundle over $M$, then an $E$-<b>valued</b> tensor field of type $(k,l)$ is a section of the bundle

$$
\left(\bigotimes^k TM \right) \otimes \left(\bigotimes^l T^\ast M \right) \otimes E.
$$

This post ended up being quite a bit longer than I expected, but hopefully you'll be able to gain some insights from this.