---
layout: post
title: "Chern Classes"
categories: [Differential Geometry]
mathjax: true
excerpt_separator: <!--more-->
---

The final topic in our discussions considering characteristic classes will be that of <b>Chern classes</b>. In the foreseeable future, I might write about characteristic classes from a different viewpoint. The way we have been doing this for now is based on the Chern-Weil Theory, but there is an alternative, more topological approach using something called <i>classifying spaces</i>.

<!--more-->

Since Chern classes are characteristic classes associated with complex vector bundles, we need to define what such bundles are and how we talk about connections and curvature of such bundles.

---

A complex vector bundle of rank $n$ is nothing more than a fiber bundle with fiber $\Bbb C^n$ and a structure group $\mathrm{GL}(n,\Bbb C)$. More concretely we have the following definition.

<div class="definition">
A complex vector bundle of rank $n$ on $M$ is a smooth manifold together with a smooth map $\pi : E \to M$ and the structure of an $n$-dimensional complex vector space on any fiber $E_p := \pi^{-1}(p)$ satisfying the following conditions:

<ul>
  <li>
    For every $p \in M$, there is a neighborhood $U \ni p$ and a diffeomorphism $\varphi : \pi^{-1}(U) \to U \times \Bbb C^n$ such that the following diagram:  
    $$
    \xymatrix{
        \pi^{-1}(U) \ar[rr]^{\varphi} \ar[dr]_{\pi} && U \times \mathbb{C}^n \ar[dl]^{\operatorname{pr}_1} \\
        & U
    }
    $$
    commutes. The map $\varphi$ is called a local trivialization of $E$ over $U$.
  </li>
  <li>
    For each $p \in M$, the map $\varphi\vert_p : E_p \to \{p\} \times \Bbb C^n$ is a linear isomorphism.
  </li>
</ul>
</div>

As you might see, the definition is pretty much identical to the one you met when you studied smooth manifolds and their vector bundles for the first time.

There are slight nuances we need to consider when we transition from the real case to the complex. For starters, the module $\Gamma(E)$ is no longer only a module over the ring $C^\infty(M)$ of smooth real-valued functions, but also a module over the set of all complex-valued smooth functions denoted by $C^\infty(M,\Bbb C)$[^1]. 

Similarly for differential forms we set 

$$
\Omega^k(M,\Bbb C) := \Omega^k(M) \otimes \Bbb C
$$

and call the elements of $\Omega^k(M,\Bbb C)$ complex $k$-forms. Exterior differentiation 

$$
\Omega^k(M,\Bbb C) \to \Omega^{k+1}(M,\Bbb C)
$$

is now defined by extending $d$ linearly over $\Bbb C$.


You might wonder what happens to our de Rham cohomology theory now as we've transitioned to consider forms in $\Omega^k(M,\Bbb C)$. We call the cochain complex $(\Omega^k(M,\Bbb C), d)$ the complex de Rham complex and denote the cohomology of this complex by $H^\ast_{dR}(M,\Bbb C)$ or simply $H^\ast(M,\Bbb C)$.

---

In the real case, we were able to consider the Riemannian metric on vector bundles $E \to M$ since the fibers were real vector spaces. The analog of this in the complex case is the <b>Hermitian metric</b> which I will define shortly.

On the complex vector space $\Bbb C^n$, the Hermitian inner product is given by

$$
\langle z, w\rangle = \sum_{j=1}^n z_j\bar{w}_j.
$$

Using this we can define a complex inner product on any complex vector space $V$.

<div class="definition">
A <b>complex inner product</b> on a complex vector space $V$ is a positive-definite, Hermitian-symmetric, sesquilinear form $\langle \ , \ \rangle : V \times V \to \Bbb C$. 
</div>

We now have the ingredients to define a Hermitian metric on a complex vector bundle $E \to M$.

<div class="definition">
A Hermitian metric on a complex vector bundle $E \to M$ assigns to each $p \in M$ a complex inner product $\langle \ , \ \rangle_p$ on the fiber $E_p$. This assignment is required to be smooth in the sense that if $s$ and $\sigma$ are sections of $E$, then $\langle s,  \sigma\rangle : M \to \Bbb C$ is a smooth complex-valued function on $M$.
</div>

It is not too difficult to see that a finite positive linear combination $\sum a^i \langle \ , \ \rangle_i$ of complex inner products on a complex vector space $V$ is again a complex inner product. This in turn yields that we can use partitions of unity to obtain the existence of a Hermitian metric on any complex vector bundle. 

---

A connection on a complex vector bundle $E \to M$ is defined exactly the same way as it is defined on a real vector bundle. It is an $\Bbb R$-bilinear map 

$$
\nabla : \Gamma(TM) \times \Gamma(E) \to \Gamma(E)
$$

that is $C^\infty(M)$-linear in the first argument, $\Bbb C$-linear in the second argument, and satisfies the Leibniz rule. Using partitions of unity, it is again not too difficult to show that every complex vector bundle has a connection.

If $E \to M$ is equipped with a Hermitian metric we call $\nabla$ a metric connection, and it is said to be compatible with the Hermitian metric if for all $X \in \Gamma(TM)$ and $s,\sigma \in \Gamma(E)$

$$
X\langle s,\sigma\rangle = \langle \nabla_X s, \sigma\rangle + \langle s, \nabla_X \sigma\rangle.
$$

If $e_1,\dots,e_n$ is a local frame over $U$, a connection $\nabla$ can be represented by a matrix $\omega = [\omega^i_j]$ of complex-valued $1$-forms:

$$
\nabla_X e_j = \sum_i \omega^i_j(X)e_i.
$$

The only difference to the real case is that the $1$-forms are now complex. The same story holds for the curvature tensor $R$. As for the curvature matrix $\Omega = [\Omega^i_j]$, the structural equation $\Omega = d\omega + \omega \wedge \omega$ holds also in the complex case.

---

It is probably no surprise that if $e = \begin{bmatrix} e_1 & \cdots & e_n\end{bmatrix}$ and $\bar{e} = \begin{bmatrix} \bar{e}_1 & \cdots & \bar{e}_n\end{bmatrix}$ are two local frames for which $\bar{e} = ea$ for $a \in \mathrm{GL}(n,\Bbb C)$, then the connection matrix and curvature matrix transform exactly the same as in the real case:

$$
\begin{align*}
\bar{\omega} &= a^{-1}\omega a + a^{-1}da \\
\bar{\Omega} &= a^{-1}\Omega a.
\end{align*}
$$

This yields that a complex polynomial $P$ on $\mathfrak{gl}(n,\Bbb C)$ that is invariant under conjugation by elements of $\mathrm{Gl}(n,\Bbb C)$ will define a global form $P(\Omega)$ on $M$. As we have shown previously, the form $P(\Omega)$ is closed and the cohomology class $[P(\Omega)]$ will be independent of the connection.

<div class="definition">
The Chern classes $c_i(E)$ on a complex vector bundle $E \to M$ are defined by

$$
c_k(E) = \left[f_k\left(\frac{i}{2\pi}\Omega\right)\right] \in H^{2k}(M, \Bbb C).
$$
</div>

Notice the similarity to the Pontryagin classes. The Pontryagin classes can be regarded as the Chern classes of a complexification $E \otimes_{\Bbb R} \Bbb C$ of a real vector bundle $E$. Indeed with our definition[^2] $p_k(E) = c_{2k}(E \otimes \Bbb C) \in H^{4k}(M)$.


As before, we'll define the <b>total Chern class</b> by

$$
c(E) := \left[\det\left(I + \frac{i}{2\pi} \Omega\right)\right] = 1 + c_1(E) + \dots + c_n(E).
$$

---

In addition to the Pontryagin classes being related to the Chern classes, the Euler classes are as well. However, you might remember from <a href="https://anthonymakela.com/differential%20geometry/2023/12/29/pontryagin-euler-chern.html" style="color:#680530; text-decoration: underline;">Pontryagin and Euler Classes
</a> that we needed the bundle to be orientable for Euler classes. Fortunately, we have the following lemma.


<div class="lemma">
Let $E$ be a complex vector bundle. Then the underlying real vector bundle $E_\Bbb R$ has a canonical orientation.
</div>

<div class="proof">
Let $V$ be a finite-dimensional complex vector space. Choosing a basis $v_1,\dots,v_n$ for $V$ over $\Bbb C,$ gives us a real basis of the underlying real vector space $V_\Bbb R$ as $v_1,iv_1,\dots,v_n,iv_n$. If $w_1,\dots,w_n$ is any other complex basis of $V$, then there exists a matrix $A \in \mathrm{GL}(n,\Bbb C)$ that transforms the first basis into the second. Since for the corresponding real matrix $A_\Bbb R \in \mathrm{GL}(2n,\Bbb R)$ we have

$$
\det(A_\Bbb R) = |\det(A)|^2 > 0
$$

i.e. $A_\Bbb R$ preserves the orientation of the underlying real vector space. Applying this to every fiber of $E$ yields the required orientation for $E_\Bbb R$ since overlapping trivializations determine a section in $\mathrm{GL}(n,\Bbb C)$.

</div>

As a consequence of the above lemma, every complex manifold is oriented, since an orientation of the tangent bundle of a manifold induces an orientation of the
manifold itself.

So, a complex vector bundle of rank $n$ is a real vector bundle of rank $2n$ with a canonical orientation. Hence it has both Chern classes as well as Euler classes. The following theorem summarizes the relationship between them. To emphasize the distinction between the complex and the underlying real vector bundle, I'll denote the latter by $E_\Bbb R$.


<div class="lemma">
Let $A \in \mathfrak{u}(n)$ be a skew-Hermitian matrix and $A_{\Bbb R} \in \mathfrak{so}(2n)$ the associated real matrix. Then
$$
\operatorname{Pf}(A_\Bbb R) = i^n\det(A).
$$
</div>

<div class="proof">
Note that since $A$ is normal, there exists a unitary matrix $U$ such that $U^{-1}AU$ is a diagonal matrix with, say $ia_1,\dots,ia_n$ as the diagonal entries. Now clearly

$$
\begin{align*}
\det(A) &= \det(U^{-1}AU) \\
&= i^na_1\cdots a_n.
\end{align*}
$$

On the other hand, if $U_{\Bbb R}$ is the orthogonal matrix induced by $U$, then since each $ia_k$ corresponds to a $2 \times 2$ block 

$$
\begin{pmatrix}0&-a_k\\ a_k&0\end{pmatrix}
$$

we have that 

$$
\begin{align*}
\operatorname{Pf}(A_\Bbb R) &= \operatorname{Pf}(U^{-1}_\Bbb R A_\Bbb RU_\Bbb R) \\
&= (-1)^n a_1\cdots a_n \\
&= i^{2n}a_1\cdots a_n \\
&= i^n \det(A)
\end{align*}
$$

which yields the result.

</div>


<div class="theorem">
Let $E \to M$ be a complex vector bundle of rank $n$. Then $c_n(E) = e(E_\Bbb R)$. In particular $c_n(E) \in H^{2n}(M, \Bbb R)$.
</div>

<div class="proof">
Equip $E$ with a Hermitian metric and a compatible connection $\nabla$. The curvature matrix $\Omega = [\Omega^j_k]$ relative to a local orthonormal frame is then skew-Hermitian. Let $\Omega_{\Bbb R}$ denote the corresponding real matrix. Using the above lemma, we get

$$
\begin{align*}
\operatorname{Pf}\left(\frac{1}{2\pi} \Omega_\Bbb R\right) &= \left(\frac{1}{2\pi} \right)^n\operatorname{Pf}(\Omega_\Bbb R) \\
&= \left(\frac{i}{2\pi} \right)^n \det(\Omega) \\
&= \left(\frac{i}{2\pi} \right)^n f_n(\Omega) \\
&= f_n\left(\frac{i}{2\pi} \Omega\right)
\end{align*}
$$
from where we conclude that $e(E_\Bbb R) = c_n(E)$.
</div>

---

Recall that if $E$ is a complex vector bundle, we define the <b>conjugate bundle</b> $\bar{E}$ as a complex vector bundle of the same rank. On each fiber $E_p$ with $p \in M$, we define multiplication by $z = a+bi \in \Bbb C$ by setting $zv = \bar{z}v$ for every $v \in E_p$. We denote this new complex vector space by $\bar{E}_p$ and define $\bar{E} = \bigcup \bar{E}_p$. Considering trivializations, if $E$ has local trivializations 

$$
\varphi_\alpha : \pi^{-1}(U_\alpha) \to U_\alpha \times \Bbb C^n,
$$

then the trivializations of $\bar{E}$ are given by

$$
\bar{\varphi}_\alpha : \pi^{-1}(U_\alpha) \to U_\alpha \times \Bbb C^n,
$$

which is composition of $\varphi_\alpha$ with the conjugation map. In terms of cocycles, if $\\{g_{\alpha\beta}\\}$ defines $E$, then $\\{\bar{g}_{\alpha\beta}\\}$ defines $\bar{E}$.

<div class="lemma">
Let $E$ be a complex vector bundle. Then $\bar{E} \cong E^\ast = \operatorname{Hom}(E, \mathcal{O})$, where $\mathcal{O}$ denotes the trivial complex line bundle.
</div>

<div class="proof">
Equip $E$ with a Hermitian metric. We can then reduce the structure group of $E$ to the unitary group. Since unitary matrices $g_{\alpha\beta}$ satisfy 

$$
\bar{g}_{\alpha\beta} = \left(g^{T}_{\alpha\beta}\right)^{-1},
$$

we see that $\bar{E}$ and $E^\ast$ have the same transition functions, i.e. are isomorphic.

</div>

<div class="proposition">
The Chern classes of the conjugate bundle $\bar{E}$ of a complex vector bundle $E$ are given by

$$
c_k(\bar{E}) = (-1)^kc_k(E).
$$
</div>

<div class="proof">
Note first that any connection $\nabla$ on $E$ is also a connection on $\bar{E}$. If $\Omega$ is the curvature matrix for $\nabla$ on $E$, then $\bar{\Omega}$ is the curvature matrix for $\nabla$ on $\bar{E}$. Now, like we have done before, on a locally framed open set the curvature matrix is skew-symmetric. Since the Chern classes are real cohomology classes, $\bar{\Omega}$ ends up being skew-Hermitian i.e. $\bar{\Omega} = -\Omega^T$. It follows that 

$$
\begin{align*}
c_k(\bar{E}) &= \left[f_k\left(\frac{i}{2\pi}\left(-\Omega^T\right)\right)\right] \\
&=(-1)^k\left[f_k\left(\frac{i}{2\pi}\left(\Omega^T\right)\right)\right] \\
&= (-1)^k\left[f_k\left(\frac{i}{2\pi}\Omega\right)\right] \\
&= (-1)^kc_k(E)
\end{align*} 
$$

as $\Omega^T = -\Omega$.
</div>

It's an immediate consequence that the Chern class of the dual bundle $E^\ast$ is given by $c_k(E^\ast) = (-1)^kc_k(E)$ also.
 
---

For the sake of concreteness, let's calculate the Chern classes of the complex projective space $\Bbb CP^n.$ Recall that the cohomology ring of $\Bbb CP^n$ is given by 

$$
H^\ast(\Bbb CP^n, \Bbb Z) \cong \Bbb Z[x]/(x^{n+1}).
$$

Let $x$ be a generator of $H^2(\Bbb CP^1, \Bbb Z)$. Now, before we go any further, we are going to need the following proposition for the calculation.

<div class="proposition">
Let $\mathcal{O}(-1)$ be the tautological line bundle over $\Bbb CP^n$ and $\mathcal{O}$ the trivial complex line bundle. Then

$$
T\Bbb CP^n \oplus \mathcal{O} \cong \underbrace{\mathcal{O}(1) \oplus \dots \oplus \mathcal{O}(1)}_{n+1}
$$

where $\mathcal{O}(1)$ is the dual bundle of $\mathcal{O}(-1)$.
</div>

<div class="proof">
This follows directly from the Euler sequence

$$
0\longrightarrow \mathcal{O} \longrightarrow {\mathcal {O}}(1)^{\oplus (n+1)}\longrightarrow {T\Bbb CP^n}\longrightarrow 0
$$

being split in the smooth category.

</div>


We are also going to need that for $\mathcal{O}(-1)$ the first Chern class is $c_1(\mathcal{O}(-1)) = -x$. To see this, note that if $\iota : \Bbb CP^1 \hookrightarrow \Bbb CP^n$ is the inclusion map, then $\iota^\ast(\mathcal{O}(-1)) = \mathcal{O}(-1)$. It suffices thus to prove the case with $n = 1$. As $c_1(\mathcal{O}(1)) = -c_1(\mathcal{O}(-1))$, its sufficient to show that $c_1(\mathcal{O}(1)) = x$. Since $H^2(\Bbb CP^1, \Bbb Z) = \Bbb Z$, we have $c_1(\mathcal{O}(1)) = kx$ for $k \in \Bbb Z$. Now

$$
T\Bbb CP^1 \oplus \mathcal{O} \cong \mathcal{O}(1) \oplus \mathcal{O}(1)
$$

and so by the Whitney product formula

$$
\begin{align*}
c_1(\Bbb CP^1) &= c_1(T\Bbb CP^1) \\
&= c_1(T\Bbb CP^1 \oplus \mathcal{O}) \\
&= c_1(\mathcal{O}(1) \oplus \mathcal{O}(1)) \\
&= 2c_1(\mathcal{O}(1)) \\
&= 2kx.
\end{align*}
$$

On the other hand, $\Bbb CP^1$ is homeomorphic to the sphere $\Bbb S^2$ so we have that

$$
\begin{align*}
c_1(\Bbb CP^1) &= e(T \Bbb S^2) \\
&= \chi(\Bbb S^2)x \\
&= 2x.
\end{align*}
$$

It follows that $k = 1$, as desired.

<div class="theorem">
The Chern classes of $\Bbb CP^n$ are given by $c(\Bbb CP^n) = (1+x)^{n+1}$ and $c_k(\Bbb CP^n) = \binom{n+1}{k}x^k$.
</div>

<div class="proof">
Using the above proposition we obtain

$$
\begin{align*}
c(\Bbb CP^n) &= c(T\Bbb CP^n \oplus \mathcal{O}) \\
&= c(\mathcal{O}(1)^{n+1}) \\
&= (1+x)^{n+1}.
\end{align*}
$$

Now $(1+x)^{n+1} = \sum_{k=0}^{n+1} \binom{n+1}{k}x^k$ from where we see that the term $\binom{n+1}{k}x^k$ corresponds to Chern class $c_k(\Bbb CP^n)$.
</div>

---

Here is a trick that turns out to be useful occasionally. Suppose that a manifold $N$ is embedded in a manifold $M$ with a normal bundle $\nu$. Then the exact sequence 

$$
0 \longrightarrow TN \longrightarrow TM\vert_N \longrightarrow \nu \longrightarrow 0,
$$

splits and so we have

$$
TM\vert_N = TN \oplus \nu.
$$

The Whitney product formula yields

$$
c(TM\vert_N) = c(TN)c(\nu).
$$

Consider the problem of deciding whether or not $\Bbb CP^4$ can be embedded in $\Bbb R^{11}$. Suppose that this can be done. Then there is an exact sequence

$$
0 \longrightarrow (T\Bbb CP^4)_\Bbb R \longrightarrow T\Bbb R^{11}\vert_{\Bbb CP^4} \longrightarrow \nu \longrightarrow 0,
$$

where $\nu$ is the normal bundle of $\Bbb CP^4$ in $\Bbb R^{11}$. If $x \in H^2(\Bbb CP^4, \Bbb Z)$ is the first Chern class of the line bundle $\mathcal{O}(1)$, then the total Chern class of $\Bbb CP^4$ is given by $(1+x)^5$. It follows that the total Pontryagin class is given by[^3]

$$
\begin{align*}
p(\Bbb CP^4) &= c((T\Bbb CP^4)_\Bbb R \otimes \Bbb C) \\
&= c(T\Bbb CP^4 \oplus \overline{T\Bbb CP^4}) \\
&= c(T\Bbb CP^4)c(\overline{T\Bbb CP^4}) \\
&= (1+x)^5(1-x)^5 \\
&= (1-x^2)^5.
\end{align*}
$$

The normal bundle trick now gives 

$$
p(T\Bbb R^{11}\vert_{\Bbb CP^{4}}) = p((T\Bbb CP^4)_\Bbb R)p(\nu).
$$

For $T\Bbb R^{11}\vert_{\Bbb CP^{4}}$, notice that this is exactly the pullback of $T\Bbb R^{11}$ to $\Bbb CP^4$ under the embedding $i : \Bbb CP^4 \to \Bbb R^{11}$ and so

$$
p(T\Bbb R^{11}\vert_{\Bbb CP^{4}}) = i^\ast(p(T\Bbb R^{11})) = 1.
$$

It follows that

$$
\begin{align*}
p(\nu) &= \frac{1}{p((T\Bbb CP^4)_\Bbb R)}  \\
&= \frac{1}{(1-x^2)^5} \\
&= 1 + 5x^2 + 15x^4,
\end{align*}
$$

since the higher-order terms vanish. Now as $\nu$ is a real line bundle, the top component of $p(\nu)$ should be in $H^2(\Bbb CP^4)$, but we have the nonzero classes $5x^2 \in H^4(\Bbb CP^4)$ and $15x^4 \in H^8(\Bbb CP^4)$ giving us a contradiction. 

---

One more thing before we'll split[^4] our ways. Typically, computing characteristic classes can be challenging. However, for complex vector bundles, this process can be simplified. The calculation of Chern classes for these bundles can be reduced to determining the Chern classes of direct sums of complex line bundles. The way to do this is by utilizing something called the <b>splitting principle</b>.

<div class="theorem" text="(Splitting Principle)">
Let $E \to M$ be a complex vector bundle of rank $n$ over a manifold $M$. Then there exists a space $F(E)$ called a flag bundle associated to $E$ and a map $\sigma : F(E) \to M$ such that
<ol>
  <li>The pullback bundle $\sigma^\ast(E)$ splits into a direct sum of line bundles: $\sigma^\ast(E) =  L_1 \oplus \dots \oplus L_n$.</li>
  <li>$\sigma^\ast$ embeds $H^\ast(M)$ in $H^\ast(F(E))$.</li>
</ol>
</div>

The proof is rather technical and long so I won't be going into it here. You can find it in “Differential Forms in Algebraic Topology” by Bott & Tu.

As an application let's compute the total Chern class of a tensor product of bundles $E \otimes E'$. Note that for line bundles $L$ and $L'$ we have

$$
c_1(L \otimes L') = c_1(L) + c_1(L').
$$

This follows from the Euler class of a rank $2$ vector bundle $E$ being expressable as $e(E) = \frac{i}{2\pi}\sum_k d(\rho_k d(\log g_{ki}))$ where $\\{\rho_k\\}$ is a partition of unity subordinate to an open cover $\\{U_k\\}$ and $\\{g_{ki}\\}$ the transition functions. If $L$ and $L'$ are now both complex line bundles given by the transition functions $\\{g_{ij}\\}$ and $\\{g_{ij}'\\}$, then the tensor product $L \otimes L'$ has transition functions $\\{g_{ij}g_{ij}'\\}$. Since $d(\log(g_{ij}g_{ij}')) = d\log(g_{ij}) + d\log(g_{ij}')$, the claim follows.

Using the splitting principle, suppose now that $E = \bigoplus_i L_i$ and $E' = \bigoplus_i L'_i$. Then

$$
E \otimes E' = \bigoplus_{i,j} L_i \otimes L'_j
$$

and so

$$
\begin{align*}
c(E \otimes E') &= c\left(\bigoplus_{i,j} L_i \otimes L'_j\right) \\
&= \prod_{ij}(1+c_1(L_i) + c_1(L'_j)).
\end{align*}
$$

Similarly for the exterior power $\Lambda^k E$ we have that, if $E$ splits as $E = \bigoplus_i L_i$, then 

$$
\Lambda^k E = \bigoplus_{1 \le i_1 \le \dots \le i_k \le n} L_{i_1} \otimes \dots \otimes L_{i_k}.
$$

Again it follows that

$$
\begin{align*}
c\left(\Lambda^k E\right) &= c\left(\bigoplus_{1 \le i_1 \le \dots \le i_k \le n} L_{i_1} \otimes \dots \otimes L_{i_k}\right) \\
&= \prod_{1 \le i_1 \le \dots \le i_k \le n}(1+ c_1(L_{i_1}) + \dots + c_1(L_{i_k})).
\end{align*}
$$


That's all for this time around. In the near future, I'm planning to write about a neat correspondence between vector bundles and maps to Grassmannians. Before that though, I'll continue with the posts considering sheaves and their cohomology.


---


[^1]: Note that $C^\infty(M,\Bbb C) = C^\infty(M) \otimes \Bbb C$.

[^2]: The definition here follows the practices from Bott & Tu. The usual way to define Pontryagin classes in terms of the Chern classes is to set $p_k(E) = (-1)^kc_{2k}(E \otimes \Bbb C)$ to ignore the odd Chern classes. Had we defined $p_k(E) = \left[f_{2k}\left(\frac{1}{2\pi}\Omega\right)\right]$, we would indeed have ended up with $p_k(E) =  \left[f_{2k}\left(\frac{1}{2\pi}\Omega\right)\right] =  \left[\left(\frac{1}{2\pi}\right)^{2k}f_{2k}\left(\Omega\right)\right]$. If you're careful enough with the coefficient $\left(1/2\pi\right)^{2k}$, you'll see that it equals $(-1)^k\left(i/2\pi\right)^{2k}$ and hence $p_k(E) = (-1)^kc_{2k}(E \otimes \Bbb C)$.

[^3]: Again, be careful here with the sign conventions if you are reading this from different sources. Milnor and Stasheff would tell you that the total Pontryagin class here would be $(1+x^2)^5$.

[^4]: No pun intended.