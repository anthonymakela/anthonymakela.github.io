---
layout: post
title: "Tensor Contraction"
categories: [Differential Geometry]
published: true
mathjax: true
excerpt_separator: <!--more-->
---

Today, we're keeping it brief and diving into tensor contraction, particularly its application in Riemannian geometry. Our motivating example will be the Ricci tensor, which, as we'll see, is actually a contraction of the curvature tensor.

<!--more-->

---

For the remaining of this post, suppose that $V_1,\dots, V_k$ and $W$ are all finite-dimensional vector spaces over the real numbers[^1], and $\alpha : V_i \times V_j \to W$ a bilinear map.

<div class="definition">
The $(i,j)$-<b>contraction</b> on $V_1 \otimes \dots \otimes V_k$ relative to $\alpha$ is the unique linear map

$$
\operatorname{tr}_{\alpha,i,j}:V_1\otimes\cdots\otimes V_k \to W\otimes V_1\otimes \cdots \widehat{V_i}\otimes\cdots\otimes \widehat{V_j}\otimes\cdots\otimes V_k,
$$

given by

$$
v_1\otimes\cdots\otimes v_k\mapsto\alpha(v_i,v_j)\otimes
v_1\otimes \cdots \widehat{v_i}\otimes\cdots\otimes \widehat{v_j}\otimes\cdots\otimes v_k.
$$

</div>


To see how this actually works, we'll go over some simpler cases and then afterwards see how the Ricci tensor arises as the contraction of the curvature tensor.

Let's start with $k = 2$ as this should be familiar to most of you who have taken linear algebra.

<div class="example">
For $k = 2$ we have $V_1, V_2$ and a bilinear map $\alpha : V_1 \times V_2 \to W$. The contraction in this case is simply the unique map 

$$
\begin{align*}
V_1 \otimes V_2 &\to W \\
v_1 \otimes v_2 &\mapsto \alpha(v_1,v_2)
\end{align*}
$$

given by the universal property of the tensor product.

</div>

Another important example is when we have a vector space $V$ and consider its dual space $V^\ast$. You might already guess what the map $\alpha$ is going to be in this case.

<div class="example">
Consider a finite-dimensional vector space $V$ and its dual $V^\ast$. Using the canonical pairing 

$$
\begin{align*}
\alpha : V^\ast \times V &\to \Bbb R \\
(\varphi, v) &\mapsto \varphi(v),
\end{align*}
$$

we obtain a unique linear map

$$
V^\ast \otimes V \to \Bbb R.
$$

Identifying $V^\ast \otimes V$ with $\operatorname{End}(V)$ this gives the familiar trace map $\operatorname{tr} : \operatorname{End}(V) \to \Bbb R$. This is one of the reasons why you might see contractions being called traces also.

</div>

<div class="example">
If $W = \Bbb R$, then $\alpha$ is a map $V_i \times V_j \to \Bbb R$ and the $(i,j)$-contraction is given by

$$
\operatorname{tr}_{\alpha,i,j}:V_1\otimes\cdots\otimes V_k \to V_1\otimes \cdots \widehat{V_i}\otimes\cdots\otimes \widehat{V_j}\otimes\cdots\otimes V_k,
$$

with

$$
v_1\otimes\cdots\otimes v_k\mapsto\alpha(v_i,v_j)\cdot 
v_1\otimes \cdots \widehat{v_i}\otimes\cdots\otimes \widehat{v_j}\otimes\cdots\otimes v_k
$$

</div>

---

Consider now the case with $k = 3$ and for example a $(1,2)$-tensor 

$$
T=T_{i\,\,k}^{\,\,j}\cdot \varepsilon^i\otimes e_j\otimes \varepsilon^k \in V^\ast \otimes V \otimes V^\ast,
$$

in a fixed bases $e_1,\dots,e_n$ and $\varepsilon^1,\dots,\varepsilon^n$ for $V$ and $V^\ast$ respectively.

There are a few different contractions we can perform here and since these depend on the bilinear map $\alpha$, some of them are a bit more difficult to construct. For a $(1,2)$-contraction we can always consider the canonical pairing $\alpha : V^\ast \times V \to \Bbb R$ which gives

$$
\begin{align*}
\operatorname{tr}_{\alpha,1,2}(T) &= T_{i\,\,k}^{\,\,j} \operatorname{tr}_{\alpha,1,2}(\varepsilon^i\otimes e_j\otimes \varepsilon^k) \\
&= T_{i\,\,k}^{\,\,j} \delta^i_j \varepsilon^k \\
&= T_{i\,\,k}^{\,\,i} \varepsilon^k.
\end{align*}
$$

Likewise for a $(2,3)$-contraction we can use the canonical pairing to obtain

$$
\begin{align*}
\operatorname{tr}_{\alpha,2,3}(T) &= T_{i\,\,k}^{\,\,j} \operatorname{tr}_{\alpha,2,3}(\varepsilon^i\otimes e_j\otimes \varepsilon^k) \\
&= T_{i\,\,k}^{\,\,j} \delta^k_j \varepsilon^i \\
&= T_{i\,\,k}^{\,\,k}\varepsilon^i.
\end{align*}
$$

What about a $(1,3)$-contraction? For such a contraction we would need a bilinear map $\alpha : V^\ast \times V^\ast \to W$ for some vector space $W$. In general there is no such a map, but suppose we have the additional datum of an inner product $g$ on $V$. This yields an isomorphism $g^\flat : V \to V^\ast$ with inverse $g^\sharp : V^\ast \to V$. Using this we can define a bilinear map

$$
\begin{align*}
h : V^\ast \times V^\ast &\to \Bbb R \\
(\varphi,\psi) &\mapsto g\left(g^\sharp(\varphi),g^\sharp(\psi)\right).
\end{align*}
$$
 
This in turn gives us a way to perform the $(1,3)$-contraction with $\alpha = h$. We obtain

$$
\begin{align*}
\operatorname{tr}_{\alpha,1,3}(T) &= T_{i\,\,k}^{\,\,j} \operatorname{tr}_{\alpha,1,3}(\varepsilon^i\otimes e_j\otimes \varepsilon^k) \\
&= T_{i\,\,k}^{\,\,j} h(\varepsilon^i, \varepsilon^k) e_j  \\
&= T_{i\,\,k}^{\,\,j} g^{ik}e_j,
\end{align*}
$$

where $g^{ij}$ are the components of the inverse metric $h$. In practice you'll see this being called <i>lowering an index</i>. Traditionally we can only contract a tensor with one upper index and one lower index, but like above, when we have two upper indices we ought to lower on of them with the metric.

---

Consider now a Riemannian manifold $(M,g)$ and the curvature tensor 

$$
R : \Gamma(TM) \times \Gamma(TM) \times \Gamma(TM) \to \Gamma(TM).
$$
 
In local coordinates we have

$$
R = R^{\,\,\,\,\,\,l}_{ijk} dx^i \otimes dx^j \otimes dx^k \otimes \partial_l.
$$

The Ricci tensor is now simply the contraction $\operatorname{tr}_{\alpha,1,4}$, where $\alpha$ is the evaluation pairing $\alpha : T^\ast M \times TM \to \Bbb R$. We obtain

$$
\begin{align*}
\operatorname{Ric} &= \operatorname{tr}_{\alpha,1,4}(R) \\
&= R^{\,\,\,\,\,\,l}_{ijk} \operatorname{tr}_{\alpha,1,4}(dx^i \otimes dx^j \otimes dx^k \otimes \partial_l) \\
&= R^{\,\,\,\,\,\,l}_{ijk} \alpha(dx^i, \partial_l)dx^j \otimes dx^k \\
&= R^{\,\,\,\,\,\,l}_{ijk} \delta^i_l dx^j \otimes dx^k \\
&= R^{\,\,\,\,\,\,i}_{ijk} dx^j \otimes dx^k \\
&= R_{jk} dx^j \otimes dx^k, 
\end{align*}
$$

where[^2] $R_{jk} = R^{\,\,\,\,\,\,i}_{ijk}$.

While we are at it, the Scalar curvature $S$ is defined by taking the $(1,2)$-contraction of $\operatorname{Ric}$ relative to the inner product $h$ on the cotangent space induced by the Riemannian metric. In this instance, we obtain

$$
\begin{align*}
S &= \operatorname{tr}_{h,1,2}(\operatorname{Ric}) \\
&= R^{\,\,\,\,\,\,i}_{ijk} \operatorname{tr}_{h,1,4}(dx^j \otimes dx^k) \\
&= g^{jk}R^{\,\,\,\,\,\,i}_{ijk} \\
&= g^{jk}R_{jk}.
\end{align*}
$$

That's all this time around.

---

[^1]: Could be any field, but we will stick with $\Bbb R$ for simplicity.

[^2]: It is a usual convention to denote the components of $\operatorname{Ric}$ by $R_{ij}$. See Introduction to Riemannian Manifolds by John M. Lee for more details on this.