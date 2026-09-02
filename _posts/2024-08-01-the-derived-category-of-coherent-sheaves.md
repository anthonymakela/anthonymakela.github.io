---
layout: post
title: "The Derived Category of Coherent Sheaves and Fourier-Mukai Theory"
categories: [Category Theory]
mathjax: true
published: true
excerpt_separator: <!--more-->
---

Last time we went through a brief overview of derived and triangulated categories. This time, our aim is to study the bounded derived category $D^b(X)$ of coherent sheaves on an algebraic variety $X$. We'll also look at something called Fourier-Mukai theory or more concretely derived correspondences.

<!--more-->

---


<div class="definition">
Let $X$ be a complex manifold or a variety. Its derived category $D^b(X)$ is by definition the bounded derived category of the abelian category $\textbf{Coh}(X)$, i.e.
$$
D^b(X) := D^b(\textbf{Coh}(X)).
$$
</div>

Recall that the objects in this category are chain complexes of coherent sheaves, and we formally invert all quasi-isomorphisms. Also, recall that this category is generally not abelian even though it is constructed from an abelian category. It is a triangulated category where the distinguished triangles serve as a substitute for short exact sequences.

It's worth mentioning here that in literature you usually see $\textbf{Coh}(X)$ replaced with $\textbf{Qcoh}(X)$, the category of quasi-coherent sheaves. The reason being that $\textbf{Coh}(X)$ usually does not contain any non-trivial injective objects so in order to compute derived functors one needs to consider a larger abelian category.

If $\mathcal{E}$ and $\mathcal{F}$ are coherent sheaves, we can think of them as being complexes concentrated in degree zero. We thus have a full and faithful embedding

$$
\textbf{Coh}(X) \to D^b(X),
$$

and in particular

$$
\operatorname{Hom}_{D^b(X)}(\mathcal{E}, \mathcal{F}) \cong \operatorname{Hom}_{\mathcal{O}_X}(\mathcal{E}, \mathcal{F}).
$$

Recall that $D^b(X)$ is also equipped with the translation functor, thus we can define

$$
\operatorname{Ext}^i(\mathcal{E}, \mathcal{F}) = \operatorname{Hom}_{D^b(X)}(\mathcal{E}, \mathcal{F}[i]).
$$

These vanish in negative degrees and $\operatorname{Ext}^0$ is just given as the sheaf morphisms due to the previous isomorphism and $\operatorname{Ext}^1(\mathcal{E}, \mathcal{F})$ classifies extensions

$$
0 \longrightarrow \mathcal{F} \longrightarrow \mathcal{G} \longrightarrow \mathcal{E} \longrightarrow 0
$$

as usual. 

The following proposition describes some basic results regarding these $\operatorname{Ext}$-groups.

<div class="proposition">
<ol>
    <li>
 If $X$ is a smooth variety of dimenison $n$, then for coherent sheaves $\mathcal{E}, \mathcal{F}$,
 $$
    \operatorname{Ext}^i(\mathcal{E}, \mathcal{F}) = 0
    $$
 unless $0 \le i \le n$.
    </li>
    <li>
 If $X$ is a projective variety, then $\operatorname{Ext}^i(\mathcal{E}, \mathcal{F})$ is a finite-dimensional complex vector space.
    </li>
    <li>
 If $X$ is an affine variety and $\mathcal{E}$ is locally free, then $\operatorname{Ext}^i(\mathcal{E}, \mathcal{F}) = 0$ for $i \ne 0$.
    </li>
</ol>
</div>

The next thing we need to assess are the derived operations. Before we do this, let's quickly go over what these are when we consider only sheaves of $\mathcal{O}_X$-modules. Let $\mathcal{F}$ and $\mathcal{G}$ be sheaves of $\mathcal{O}_X$-modules. Then we can define the following standard operations.

<ol>
    <li>
    <b>Direct sum</b>: The direct sum $\mathcal{F} \oplus \mathcal{G}$ is defined by taking the collection of direct sums of local sections fitting into a trivial split extension of $\mathcal{O}_X$-modules
 $$
    0 \longrightarrow \mathcal{F} \longrightarrow \mathcal{F} \oplus \mathcal{G} \longrightarrow \mathcal{G} \longrightarrow 0.
    $$
    </li>
    <li>
    <b>Tensor product</b>: The tensor product of $\mathcal{F} \otimes_{\mathcal{O}_X} \mathcal{G}$ to be the sheafification of the assignment
 $$
 U \mapsto \mathcal{F}(U) \otimes_{\mathcal{O}_X(U)} \otimes \mathcal{G}(U).
    $$
    </li>
    <li>
    <b>Internal Hom</b>: The internal hom $\mathcal{Hom}(\mathcal{F}, \mathcal{G})$ is defined by 
 $$
    \mathcal{Hom}(\mathcal{F}, \mathcal{G})(U) = \operatorname{Hom}(\mathcal{F}(U),\mathcal{G}(U)).
    $$
    </li>
    <li>
    <b>Dual</b>: Using the internal hom we can define the dual of a sheaf $\mathcal{F}$ by 
 $$
    \mathcal{F}^\ast = \mathcal{Hom}(\mathcal{F}, \mathcal{O}_X).
    $$
    </li>
</ol>

Given a morphism $f : X \to Y$, we also have the direct and inverse image functors. 

If we now consider a functor of $F : \mathcal{A} \to \mathcal{B}$ between abelian categories, a natural question to pose is that can we define a canonical functor between the derived categories $D(\mathcal{A})$ and $D(\mathcal{B})$. One would naively consider applying to a complex $A^\bullet$ in $D(\mathcal{A})$ the functor $F$ just componentwise, but this only makes sense if $F$ is exact due to the following proposition.

<div class="proposition">
Let $F : \mathcal{A} \to \mathcal{B}$ be an additive functor between abelian categories. Then $F$ is exact if and only if the image $F(A^\bullet)$ of any acyclic complex $A^\bullet$ in $\mathcal{A}$ is an acyclic complex in $\mathcal{B}.$
</div>

<div class="proof">
Suppose that $F$ is exact and 

$$
A^\bullet = \cdots \longrightarrow A^{i-1} \longrightarrow A^i \longrightarrow A^{i+1} \longrightarrow \cdots
$$

an acyclic complex in $\mathcal{A}$. That is $H^i(A^\bullet) = 0$ for every $i$. Since $F$ is exact the complex 

$$
F(A^\bullet) = \cdots \longrightarrow F(A^{i-1}) \longrightarrow F(A^i) \longrightarrow F(A^{i+1}) \longrightarrow \cdots
$$

is exact at each $F(A^i)$ and hence $F(A^\bullet)$ is acyclic in $\mathcal{B}$. Suppose then that $F(A^\bullet)$ is an acyclic complex in $\mathcal{B}$ for any acyclic complex $A^\bullet$ in $\mathcal{A}$. Note that for any $A,B,C \in \mathcal{A}$, the complex

$$
\cdots \longrightarrow 0 \longrightarrow A \longrightarrow B \longrightarrow C \longrightarrow 0 \longrightarrow \cdots
$$


where $A$ is in degree $0$, $B$ in degree $1$ and $C$ in degree $2$ obtained from the short exact sequence

$$
0 \longrightarrow A \longrightarrow B \longrightarrow C \longrightarrow 0 
$$

is acyclic. Hence

$$
\cdots \longrightarrow 0 \longrightarrow F(A) \longrightarrow F(B) \longrightarrow F(C) \longrightarrow 0 \longrightarrow \cdots
$$

is acyclic in $\mathcal{B}$ by assumption. Thus $0 \longrightarrow F(A) \longrightarrow F(B) \longrightarrow F(C) \longrightarrow 0 $ is a short exact sequence and $F$ is exact.
</div>

Using the above proposition, if $F$ is not exact, the image of any acyclic complex $A^\bullet$ in $\mathcal{A}$, i.e. a complex that is zero in $D(\mathcal{A})$, is not generally acyclic. This is problematic since, in derived categories, we want to identify complexes that are quasi-isomorphic (i.e., have isomorphic cohomology). To remedy this, we introduce the concepts of left and right-derived functors. These derived functors provide a way to extend $F$ to a functor between the derived categories, $D(\mathcal{A})$ and $D(\mathcal{B})$.

To ensure the existence of such a derived functor, some kind of exactness condition must be assumed. Suppose in addition that the category $\mathcal{A}$ has enough injectives. Let $F : \mathcal{A} \to \mathcal{B}$ be a left-exact functor of abelian categories.

<div class="lemma">
Suppose that $\mathcal{A}$ is an abelian category that has enough injectives. That is, any object can be embedded into an injective one. Then the natural functor
$$
\iota : K^+(\mathcal{I}_{\mathcal{A}}) \to D^+(\mathcal{A})
$$
is an equivalence.
</div>


Consider the equivalence $\iota : K^+(\mathcal{I}\_{\mathcal{A}}) \to D^+(\mathcal{A})$ induced by the localization functor $Q_{\mathcal{A}} : K^+(\mathcal{A}) \to D^+(\mathcal{A})$. If we denote the quasi-inverse of $\iota$ by $\iota^{-1}$ we obtain a commutative diagram

$$
\xymatrix{
K^+(\mathcal{I}_{\mathcal{A}}) \ar@{->}[r] \ar@{->}[rd]^{\iota} & K^+(\mathcal{A}) \ar@{->}[r]^{K(F)} \ar@{->}[d]^{Q_\mathcal{A}} & K^+(\mathcal{B}) \ar@{->}[d]^{Q_\mathcal{B}} \\
 & D^+(\mathcal{A}) \ar@/^/@{->}[lu]^{\iota^{-1}} & D^+(\mathcal{B}),
}
$$

where $K(F)$ is the functor that maps 

$$
\cdots \longrightarrow A^{i-1} \longrightarrow A^i \longrightarrow A^{i+1} \longrightarrow \cdots
$$

to

$$
\cdots \longrightarrow F(A^{i-1}) \longrightarrow F(A^i) \longrightarrow F(A^{i+1}) \longrightarrow \cdots
$$

which is well-defined in the case of the homotopy category.

<div class="definition">
The right derived functor of a functor $F : \mathcal{A} \to \mathcal{B}$ between abelian categories is the functor 
$$
RF := Q_{\mathcal{B}} \circ K(F) \circ \iota^{-1} : D^+(\mathcal{A}) \to D^+(\mathcal{B}).
$$
</div>

The properties illustrated in the following proposition determine the right derived functor $RF$ of a left exact functor $F$ up to unique isomorphism.

<div class="proposition">
Let $F : \mathcal{A} \to \mathcal{B}$ be a functor between abelian categories. Then 
<ol>
    <li>
 There exists a natural morphism of functors
 $$
 Q_\mathcal{B} \circ K(F) \to RF \circ Q_{\mathcal{A}}.
    $$
    </li>
    <li>
 The right-derived functor $RF : D^+(\mathcal{A}) \to D^+(\mathcal{B})$ is an exact functor of triangulated categories.
    </li>
    <li>
 Suppose that $G : D^+(\mathcal{A}) \to D^+(\mathcal{B})$ is an exact functor. Then any functor morphism $Q_\mathcal{B} \circ K(F) \to G \circ Q_\mathcal{A}$ factorizes through a unique functor morphism $RF \to G$.
    </li>
</ol>
</div>

<div class="proof">
<ol>
    <li>
 Let $A^\bullet \in D^+(\mathcal{A})$ and $I^\bullet = \iota^{-1}(A^\bullet)$. The natural transformation $\operatorname{id} \to \iota \circ \iota^{-1}$ gives a functorial morphism $A^\bullet \to I^\bullet$ in $D^+(\mathcal{A})$, which is itself given by a roof
 $$
    \xymatrix{
 & C^\bullet \ar@{->}[ld]_{\operatorname{qis}} \ar@{->}[rd] &  \\
 A^\bullet &  & I^\bullet.
 }
    $$
 The injectivity of $I^j$ for each $j$ yields a unique morphism $A^\bullet \to I^\bullet$ in $K(\mathcal{A})$, which is independent of the choice of $C^\bullet$. All in all, we obtain a functorial morphism 
 $$
 K(F)(A^\bullet) \to K(F)(I^\bullet) = RF(A^\bullet).
    $$
    </li>
    <li>
 The category $K^+(\mathcal{I}_\mathcal{A})$ is triangulated and $\iota : K^+(\mathcal{I}_\mathcal{A}) \to D^+(\mathcal{A})$ is clearly exact. It follows that $\iota^{-1}$ is also exact and so $RF$ is the composition of three exact functors and therefore itself exact.
    </li>
    <li>
 For the proof of this, see S. Gelfand, Y. Manin Methods of Homological Algebra III.6.11.
    </li>
</ol>
</div>

For a right exact functor $F : \mathcal{A} \to \mathcal{B}$ we have an analogous definition of the left derived functor

$$
LF : D^{-}(\mathcal{A}) \to D^{-}(\mathcal{B}).
$$

The following summarizes some of the important results we are going to need in the future.

<div class="theorem">
Let $X$ be a smooth variety. 
<ol>
    <li>
 For $\mathcal{E}, \mathcal{F}$ and $\mathcal{G}$ in $D^b(X)$, we have that
 $$
    \mathcal{E} \overset{L}{\otimes} (\mathcal{F} \overset{L}{\otimes} \mathcal{G}) \cong (\mathcal{E} \overset{L}{\otimes} \mathcal{F}) \overset{L}{\otimes} \mathcal{G} \in D^b(X).
    $$
    </li>
    <li>
 For $\mathcal{E}$ and $\mathcal{F}$ in $D^b(X)$, we have that
 $$
 Lf^\ast(\mathcal{E}) \overset{L}{\otimes} Lf^\ast(\mathcal{F}) \cong Lf^\ast(\mathcal{E} \overset{L}{\otimes} \mathcal{F}) \in D^b(X).
    $$
    </li>
    <li>
    <b>Adjunction</b>: Let $\mathcal{E} \in D^b(Y)$ and $\mathcal{F} \in D^b(X)$. Then
 $$
    \operatorname{Hom}_{D^b(X)}(Lf^\ast \mathcal{E},\mathcal{F}) \cong \operatorname{Hom}_{D^b(Y)}(\mathcal{E},Rf_\ast\mathcal{F}).
    $$
    </li>
    <li>
    <b>The Projection Formula</b>: Let $\mathcal{E} \in D^b(Y)$, $\mathcal{F} \in D^b(X)$ and assume that $f$ is proper. Then
 $$
 Rf_\ast \left(Lf^\ast(\mathcal{E}) \overset{L}{\otimes} \mathcal{F}\right) \cong \mathcal{E} \overset{L}{\otimes} Rf_\ast(\mathcal{F}) \in D^b(Y).
    $$
    </li>
    <li>
    <b>Smooth Base Change</b>: Let $X,Y$ and $Z$ be smooth varieties, and $f : Z \to Y$ a morphism. From the diagram
 $$
    \xymatrix{
 X \times Z \ar@{->}[d]_{q} \ar@{->}[r]^{F} & X \times Y \ar@{->}[d]^{p} \\
 Z \ar@{->}[r]_{f} & Y
 }
    $$
 where $F$ is the map induced by $f$, and $p,q$ the natural projections. Then there is a natural isomorphism of functors
 $$
 Lf^\ast \circ Rp_\ast \cong Rq_\ast \circ LF^\ast : D^b(X\times Y) \to D^b(Z).
    $$
    </li>
</ol>
</div>

---

We'll now turn into derived correspondences. Let's begin by considering correspondences in a classical sense in algebraic geometry. A <i>correspondence</i> from a variety $X$ to a variety $Y$ is essentially a relation between the points of these two varieties. Formally a correspondence from $X$ to $Y$ is defined as a subvariety $Z \subset X \times Y$. The idea behind this is that it generalizes the notion of a function or a morphism between varieties to a "multi-valued
function".

In the simplest case, if $f : X \to Y$ is a morphism of varieties, then the graph $\Gamma_f \subset X \times Y$ is a special kind of correspondence where every $x \in Y$ corresponds to exactly one point $y \in Y$. In a sense, all the information about $f$ is contained in the graph $\Gamma_f \subset X \times Y$. If we now consider the projections $p_X$ and $p_Y$ from $X \times Y$ to the corresponding factors, restricted to the subvariety $\Gamma_f$, the projection $p_X$ is an isomorphism. The map $p_Y$ acts just like $f$. The fibers of $p_Y$ restricted to $\Gamma_f$ are just the fibers of $f$, so for example $f$ is proper if and only if $p_Y\vert_{\Gamma_f}$ is.

If $H$ is any reasonable homology, then we have a natural push forward

$$
f_\ast : H(X) \to H(Y).
$$

It's not too difficult to see that this map can be expressed in terms of $\Gamma_f$ and the projections as the map

$$
f_\ast(\alpha) = p_{Y\ast}(p^\ast_X(\alpha) \smile [\Gamma_f]).
$$

To understand this formula, the homology class $\alpha$ is first pulled back to a class in $X \times Y$ and then intersected with the fundamental class $[\Gamma_f]$ after which we push it forward via $p_{Y\ast}$.

In the more general case, we replace the graph of a morphism with a general subvariety $Z \subset X \times Y$ and relax the condition for $p_X$ to be an isomorphism to something weaker like finite or proper. Under some suitable assumptions the right-hand side of the above formula still makes sense and yields a generalized pushforward.

Now any subvariety $Z \subset X \times Y$ can be represented by its structure sheaf $\mathcal{O}_Z$ and we have the usual direct and inverse image functors $f\_\ast$ and $f^\ast$ for which we can consider the respective derived functors. Generalizing this to not only just structure sheaves we obtain the following definition.

<div class="definition">
A <i>derived correspondence</i> $\mathcal{F}$ between varieties $X$ and $Y$ is an object of $D^b(X \times Y)$ with proper support over both factors. A derived correspondence defines a functor
$$
\begin{align*}
\Phi_\mathcal{F} : D^b(X) &\to D^b(Y) \\
(-) &\mapsto Rp_{Y\ast}(Lp^\ast_X(-) \overset{L}{\otimes} \mathcal{F}),
\end{align*}
$$
where $(-)$ is could be either an object or a morphism.
</div>

A worthy remark here is that $\Phi_\mathcal{F}$ is an exact functor as it is defined as the composition of exact functors. Also, one must resort to the derived tensor product $\overset{L}{\otimes}$ when we allow for arbitrary objects of $D^b(X \times Y)$. In the case of $Y$-flat sheaves, this is not necessary. Given two derived correspondences $\mathcal{F} \in D^b(X \times Y)$ and $\mathcal{G} \in D^b(Y \times Z)$, we can consider the composite 

$$
\Phi_\mathcal{G} \circ \Phi_\mathcal{F} : D^b(X) \to D^b(Z),
$$

of the respective functors defined by the correspondences.

<div class="proposition">
The composite $\Phi_\mathcal{G} \circ \Phi_\mathcal{F}$ is isomorphic to the functor $\Phi_\mathcal{E}$, where
$$
\mathcal{E} = Rp_{XZ\ast}(Lp^\ast_{YZ}(\mathcal{G}) \overset{L}{\otimes} Lp^\ast_{XY}(\mathcal{F})) \in D^b(X \times Z).
$$
Here $p_{XY} : X \times Y \times Z \to X \times Y$ and $p_{YZ}$ and $p_{XZ}$ are defined similarly.
</div>

<div class="proof">
Consider
$$
\xymatrix{
X \times Y \times Z \ar@{->}[r]^{p_{XY}} \ar@{->}[d]_{p_{YZ}} & X \times Y \ar@{->}[d]^{p_Y} \\
Y \times Z \ar@{->}[r]_{p_Y} & Y.
}
$$
The key idea here is to use the projection formula and apply base change using the above diagram. Let $\mathcal{A} \in D^b(X)$, then
$$
\begin{align*}
\Phi_{\mathcal{E}}(\mathcal{A}) &= Rp_{Z\ast}(Lp^\ast_X(\mathcal{A}) \overset{L}{\otimes} \mathcal{E}) \\
&= Rp_{Z\ast}(Lp^\ast_X(\mathcal{A}) \overset{L}{\otimes} Rp_{XZ\ast}(Lp^\ast_{YZ}(\mathcal{G}) \overset{L}{\otimes} Lp^\ast_{XY}(\mathcal{F}))) \\
&\cong Rp_{Z\ast}(Rp_{XZ_\ast}(Lp^\ast_{XZ}(Lp^\ast_X(\mathcal{A})) \overset{L}{\otimes} Lp^\ast_{YZ}(\mathcal{G}) \overset{L}{\otimes} Lp^\ast_{XY}(\mathcal{F})) && \text{(The projection formula)} \\
&= Rp_{Z\ast}(Rp_{XZ_\ast}(Lp^\ast_X(\mathcal{A}) \overset{L}{\otimes} Lp^\ast_{YZ}(\mathcal{G}) \overset{L}{\otimes} Lp^\ast_{XY}(\mathcal{F})) && \text{($p^\ast_{XZ} \circ p^\ast_X = p^\ast_X$)} \\
&=  Rp_{Z\ast}(Lp^\ast_X(\mathcal{A}) \overset{L}{\otimes} Lp^\ast_{YZ}(\mathcal{G}) \overset{L}{\otimes} Lp^\ast_{XY}(\mathcal{F})) && \text{($p_{Z\ast} \circ p_{XZ\ast} = p_{Z\ast}$)} \\
&= Rp_{Z\ast}(Lp^\ast_{XY}(Lp^\ast_X(\mathcal{A})\overset{L}{\otimes} \mathcal{F})\overset{L}{\otimes} Lp^\ast_{YZ}(\mathcal{G})) && \text{($p^\ast_{XY} \circ p^\ast_X = p^\ast_X$)} \\
&= Rp_{Z\ast}(Rp_{YZ\ast}(Lp^\ast_{XY}(Lp^\ast_X(\mathcal{A})\overset{L}{\otimes} \mathcal{F})\overset{L}{\otimes} Lp^\ast_{YZ}(\mathcal{G}))) && \text{($p_{Z\ast} \circ p_{YZ\ast} = p_{Z\ast}$)}  \\
&\cong Rp_{Z\ast}(Rp_{YZ\ast}(Lp^\ast_{XY}(Lp^\ast_X(\mathcal{A})\overset{L}{\otimes} \mathcal{F})) \overset{L}{\otimes} \mathcal{G}) && \text{(The projection formula)} \\
&\cong Rp_{Z\ast}(Lp^\ast_Y(Rp_{Y\ast}(Lp^\ast_X(\mathcal{A})\overset{L}{\otimes} \mathcal{F})) \overset{L}{\otimes} \mathcal{G})  && \text{(Base change)} \\
&= \Phi_\mathcal{G}(\Phi_\mathcal{F}(\mathcal{A})).
\end{align*}
$$
</div>

In literature the functor $\Phi_\mathcal{F}$ is also sometimes called an <i>integral functor</i>. We call $\Phi_\mathcal{F}$ an <i>Fourier-Mukai transform</i> if it is an equivalence and $X$ and $Y$ Fourier-Mukai partners, if there exists a Fourier-Mukai transform $\Phi_\mathcal{F} : D^b(X) \to D^b(Y) $.

The first occurrence of a derived equivalence seems to originate from a set of lecture notes called "Microfunctions and pseudodifferential equations" by  Sato, Kawai, and Kashiwara in $1971$. What they did was show that there is such an equivalence between the derived categories of sheaves on a sphere bundle and its dual bundle. Since then this framework has been utilized in multiple different places. Mukai showed that analogously for a real vector space $V$, Fourier transformations yielding an isometry between $L^2(V)$ and $L^2(V^\ast)$, an abelian variety $X$ and its dual $\hat{X}$ have equivalent derived categories of coherent sheaves. In $1983$ Beilinson showed that $D^b(\mathbf{Coh}(\Bbb P^n))$ is equivalent to a non-commutative finite dimensional algebra which yielded some insight on earlier results of Barth and Hulek on the relation between vector bundles and linear algebra. 

There is also the famous Riemann-Hilbert correspondence that yields a derived equivalence between sheaves of vector spaces and regular holonomic $D$-modules
on a complex manifold or a smooth algebraic variety.

Most notably we have homological mirror symmetry conjectured by Kontsevich stating that for mirror pair $X$ and $Y$ of Calabi-Yau manifolds, the bounded derived category of coherent sheaves on $X$ is equivalent to the Fukaya category of $Y$. In $2003$, Seidel proved this to hold for quartic surfaces.

A reasonable question one might ask now is: Why would one expect a derived equivalence of categories to hold? This might be not the easiest question to answer, but one way to think about this is that while any equivalence of abelian categories is exact, there are lots of exact functors that are not equivalences. Derived functors fix this problem and thus in a sense tell us that occasionally the "only" thing preventing a functor between abelian categories from being an equivalence is the lack of exactness.

Considering the identity map $\operatorname{id} : D^b(X) \to D^b(X)$ provides us with the simplest of an equivalence that is actually a Fourier-Mukai transformation.

<div class="example">
The identity map $\operatorname{id} : D^b(X) \to D^b(X)$ is naturally equivalent to the Fourier-Mukai transformation $\Phi_{\mathcal{O}_\Delta}$ with the kernel given by the structure sheaf $\mathcal{O}_\Delta$ of the diagonal $\Delta \subset X \times X$. Indeed, if $\iota : X \to \Delta$ denotes the embedding we obtain
$$
\begin{align*}
\Phi_{\mathcal{O}_\Delta}(\mathcal{A}) &= Rp_{X\ast}(Lp^\ast_X(\mathcal{A})\overset{L}{\otimes}\mathcal{O}_\Delta) \\
&=  Rp_{X\ast}(Lp^\ast_X(\mathcal{A})\overset{L}{\otimes}\iota_\ast(\mathcal{O}_X)) \\
&\cong Rp_{X\ast}(\iota_\ast(\iota^\ast(Lp^\ast_X(\mathcal{A}))\overset{L}{\otimes}\mathcal{O}_X)) \\
&= \mathcal{A}
\end{align*}
$$
since $p_X \circ \iota = \operatorname{id} = \iota \circ p_X$.
</div>

A quick digression on Serre functors and then we can proceed to go over some elementary properties of Fourier-Mukai transforms and state a celebrated result due to Orlov. Let $X$ be a smooth projective variety over a field $k$ and $\omega_X$ its canonical bundle. The bundle $\omega_X$ is often called the <i>dualizing sheaf</i> of $X$ for reasons that become apparent soon. Note that for any locally free sheaf $\mathcal{E}$, the functor

$$
\begin{align*}
\mathbf{Coh}(X) &\to \mathbf{Coh}(X) \\
\mathcal{F} &\mapsto \mathcal{F} \otimes \mathcal{E}
\end{align*}
$$

is exact. It follows that this descends to an exact functor $\mathcal{E} \otimes -$ on the derived categories $D^b(X) \to D^b(X)$. 

<div class="definition">
Let $X$ be a smooth projective variety of dimension $n$. Define the exact functor $S_X$ as the composition

$$
\xymatrix{
D^b(X) \ar@{->}[r]^{\omega_X\otimes -} & D^b(X) \ar@{->}[r]^{[n]} & D^b(X)
}
$$

</div>

In a $k$-linear category[^1] $\mathcal{A}$, a Serre functor is a $k$-linear equivalence $S : \mathcal{A} \to \mathcal{A}$ such that for any two objects $A,B \in \mathcal{A}$, there exists an isomorphism

$$
\eta_{A,B} : \operatorname{Hom}(A,B) \to \operatorname{Hom}(B,S(A))^\ast 
$$

of $k$-vector spaces which is functorial in $A$ and $B$.

<div class="theorem">
Let $X$ be a smooth projective variety over a field $k$. Then 
$$
S_X : D^b(X) \to D^b(X)
$$
is a Serre functor.
</div>

<div class="lemma">
Let $\mathcal{A}$ and $\mathcal{B}$ be $k$-linear categories over a field $k$ with finite-dimensional hom-sets. If $\mathcal{A}$ and $\mathcal{B}$ are endowed with Serre functors $S_{\mathcal{A}}$ and $S_{\mathcal{B}}$, then any $k$-linear equivalence
$$
F : \mathcal{A} \to \mathcal{B}
$$
commutes with Serre duality, i.e. there exists an isomorphism
$$
F \circ S_{\mathcal{A}} \cong S_{\mathcal{B}} \circ F.
$$
</div>

<div class="proof">
For any $A,B \in \mathcal{A}$, since $F$ is fully faithful we have that
$$
\operatorname{Hom}(A,S_{\mathcal{A}}(B)) \cong \operatorname{Hom}(F(A),F(S_{\mathcal{A}}(B))),
$$
and
$$
\operatorname{Hom}(B,A) \cong \operatorname{Hom}(F(B),F(A)).
$$
Additionally
$$
\operatorname{Hom}(A,S_{\mathcal{A}}(B)) \cong \operatorname{Hom}(B,A)^\ast,
$$
and
$$
\operatorname{Hom}(F(B),F(A)) \cong \operatorname{Hom}(F(A),S_{\mathcal{B}}(F(B)))^\ast.
$$
These yield a functorial isomorphism 
$$
\operatorname{Hom}(F(B),F(S_{\mathcal{A}}(B))) \cong \operatorname{Hom}(F(A),S_{\mathcal{B}}(F(B)))^\ast
$$
and using the fact that any object in $\mathcal{B}$ is isomorphic to some $F(A)$ the conclusion follows from Yoneda's lemma.
</div>

So for equivalences, we obtain compatibility with Serre functors. Unfortunately, this no longer holds in the case of Fourier-Mukai transformations. If we consider a morphism $f : X \to Y$, then if $\iota : \Gamma_f \to X \times Y$ denotes the inclusion, we obtain 

$$
p^\ast_X(-) \otimes_{\mathcal{O}_{X \times Y}} \mathcal{O}_{\Gamma_f} \cong \iota_\ast \circ p^\ast_X(-).
$$

This gives $f\_\ast \cong \Phi_{\mathcal{O}\_{\Gamma_f}} : D^b(X) \to D^b(Y)$. As a special case, one may consider cohomology $H^\ast(X,-)$ as the Fourier–
Mukai transform $\Phi_{\mathcal{O}_X} : D^b(X) \to D^b(\textbf{Vec}_k)$, where $X \subset X \times \operatorname{Spec}(k)$ is considered as the graph of the projection $X \to \operatorname{Spec}(k)$. The projection maps a sheaf $\mathcal{F}$ to its cohomology $H^\ast(X,\mathcal{F})$ and in general

$$
\begin{align*}
S_{\mathrm{pt}}H^0(X,\mathcal{F}) &= H^0(X,\mathcal{F}) \\
&\not\cong H^n(X,\mathcal{F} \otimes \omega_X) \\
&\cong H^0(X,\mathcal{F} \otimes \omega_X[\dim(X)]) \\
&= H^0(X,S_X(\mathcal{F})).
\end{align*}
$$

Any exact equivalence has a left and a right adjoint and this is in fact true also for any Fourier-Mukai transform. More concretely, the left and the right adjoint of a Fourier–Mukai transform are again Fourier–Mukai transforms.

<div class="definition">
For any $\mathcal{A} \in D^b(X \times Y)$, define
$$
\mathcal{A}_L := \mathcal{A}^\lor \otimes Lp^\ast_Y \omega_Y[\dim(Y)]
$$
and
$$
\mathcal{A}_R := \mathcal{A}^\lor \otimes Lp^\ast_X \omega_X[\dim(X)].
$$
</div>

<div class="proposition" text="(Mukai)">
Let $\Phi_{\mathcal{A}} : D^b(X) \to D^b(Y)$ be the Fourier-Mukai transform with kernel $\mathcal{A}$. Then
$$
\Phi_{\mathcal{A}_L} : D^b(Y) \to D^b(X)
$$
and
$$
\Phi_{\mathcal{A}_R} : D^b(Y) \to D^b(X)
$$
are left and right adjoints for $\Phi_{\mathcal{A}}$ respectively.
</div>

<div class="proof">
This is mostly an application of the Grothendieck-Verdier duality. For any $\mathcal{E} \in D^b(X)$ and $\mathcal{F} \in D^b(Y)$ we have
$$
\begin{align*}
\operatorname{Hom}_{D^b(X)}(\Phi_{\mathcal{A}_L}(\mathcal{F}),\mathcal{E}) &= \operatorname{Hom}_{D^b(X)}(Rp_{X\ast}(\mathcal{A}_L \overset{L}{\otimes} Lp^\ast_Y(\mathcal{F})),\mathcal{E}) \\
&\cong \operatorname{Hom}_{D^b(X\times Y)}(\mathcal{A}_L \overset{L}{\otimes} Lp^\ast_Y(\mathcal{F}),Lp^\ast_X(\mathcal{E}) \overset{L}{\otimes}Lp^\ast_Y \omega_Y[\dim(Y)]) \\
&\cong \operatorname{Hom}_{D^b(X\times Y)}(\mathcal{A}^\lor \overset{L}{\otimes} Lp^\ast_Y(\mathcal{F}), Lp^\ast_X(\mathcal{E})) \\
&\cong \operatorname{Hom}_{D^b(X\times Y)}(Lp^\ast_Y(\mathcal{F}), \mathcal{A}\overset{L}{\otimes} Lp^\ast_X(\mathcal{E})) \\
&\cong \operatorname{Hom}_{D^b(Y)}(\mathcal{F}, Rp_{Y\ast}(\mathcal{A}\overset{L}{\otimes} Lp^\ast_X(\mathcal{E}))) \\
&= \operatorname{Hom}_{D^b(Y)}(\mathcal{F}, \Phi_{\mathcal{A}}(\mathcal{E})),
\end{align*}
$$
and hence $\Phi_{\mathcal{A}_L}\dashv \Phi_{\mathcal{A}}$. A similar calculation shows that $\Phi_{\mathcal{A}} \dashv \Phi_{\mathcal{A}_R}$.
</div>

The proposition above is neat since it allows us to use techniques we know for functors on triangulated categories admitting adjoints to be applied to Fourier-Mukai transforms. There is a result of Bondal and van den Bergh stating that any exact functor

$$
F : D^b(X) \to D^b(Y),
$$

whether or not it's a Fourier-Mukai transform, admits left and right adjoints. The relationship between arbitrary functors and those of Fourier-Mukai type is given by the following remarkable result of Orlov.

<div class="theorem" text="(Orlov)">
Let $X$ and $Y$ be smooth projective varieties and let
$$
F : D^b(X) \to D^b(Y)
$$
be a fully faithful exact functor. If $F$ admits right and left adjoint functors, then there exists an object $\mathcal{E} \in D^b(X\times Y)$ unique up to isomorphism such that 
$$
F \cong \Phi_{\mathcal{E}}.
$$
</div>

Let's go over a few corollaries of this result.

<div class="corollary">
Let $F : D^b(X) \to D^b(Y)$ be an equivalence of derived categories of smooth projective varieties. Then $F$ is isomorphic to a Fourier-Mukai transform $\Phi_{\mathcal{E}}$ associated with a certain object $\mathcal{E} \in D^b(X \times Y)$, which is unique up to isomorphism. 
</div>

The following shows that the derived categories contain most of the important data of the varieties in question.

<div class="corollary">
Let $X$ and $Y$ be smooth projective varieties with equivalent derived categories $D^b(X)$ and $D^b(Y)$. Then
$$
\dim(X) = \dim(Y).
$$
</div>

<div class="proof">
Let $F : D^b(X) \to D^b(Y)$ be the equivalence. Orlov's theorem states that $F$ is of the form $\Phi_{\mathcal{E}}$ for some $\mathcal{E} \in D^b(X \times Y)$. Moreover, $F$ has left and right adjoints given by the Fourier-Mukai transforms $D^b(Y) \to D^b(X)$ with kernels $\mathcal{E}_L = \mathcal{E}^\lor \otimes Lp^\ast_Y \omega_Y[\dim(Y)]$ and $\mathcal{E}_R = \mathcal{E}^\lor \otimes Lp^\ast_X \omega_Y[\dim(X)]$. Since $F$ is an equivalence, both of these adjoints are quasi-inverses of $F$. The uniqueness of Fourier-Mukai kernels yields that $\mathcal{E}_L$ and $\mathcal{E}_R$ are isomorphic objects in $D^b(X\times Y)$. It follows that

$$
\mathcal{E}^\lor \cong \mathcal{E}^\lor \overset{L}{\otimes}(Lp^\ast_Y\omega_X \overset{L}{\otimes} Lp^\ast_X\omega^\ast_Y[\dim(X)-\dim(Y)]).
$$

Since $\mathcal{E}^\lor$ is an object of a bounded derived category this yields $\dim(X) = \dim(Y)$.

</div>

Orlov's result can also be used to prove a result of Gabriel's stating that the abelian category of coherent sheaves on a scheme determines the scheme.

<div class="corollary" text="Gabriel">
Let $X$ and $Y$ be smooth projective varieties. If there exists an equivalence

$$
\textbf{Coh}(X) \cong \textbf{Coh}(Y),
$$

then $X \cong Y$.
</div>

<div class="proof">
Note that any equivalence 

$$
F : \textbf{Coh}(X) \to \textbf{Coh}(Y)
$$

can be extended to an equivalence

$$
\Phi : D^b(X) \to D^b(Y).
$$

A sheaf $\mathcal{F} \in \textbf{Coh}(X)$ is called indecomposable if any non-trivial surjection $\mathcal{F} \to \mathcal{G}$ with $\mathcal{G} \in \textbf{Coh}(X)$ is an isomorphism. Recall also that any indecomposable sheaf is of the form $k(x)$ with $x \in X$ being a closed point. As the equivalence $F$ preserves indecomposable objects, it follows that for any closed point $x \in X$ there is a closed point $y \in Y$ such that

$$
F(k(x)) \cong k(y).
$$

As this holds also for the extension $\Phi$, this implies that $\Phi$ is of the form

$$
\mathcal{F}^\bullet \mapsto L \otimes f_\ast\mathcal{F}^\bullet
$$

for some isomorphism $f : X \to Y$ and some line bundle $L$ on $Y$.

</div>

---

To conclude this, let's go over a characterization for $\Phi_{\mathcal{F}}$ to be an equivalence.

<div class="proposition">
Let $X$ be a smooth projective variety. The set $\{\mathcal{O}_x \mid x \in X \}$ of objects in $D(X)$ consisting of the structure sheaves of points satisfies the following properties:
<ol>
    <li>
 For all $x \in X$, 
 $$
    \operatorname{Hom}_{D(X)}(\mathcal{O}_x,\mathcal{O}_x) \cong \Bbb C.
    $$
    </li>
    <li>
 For all $x \ne y$ and $i \in \Bbb Z$,
 $$
    \operatorname{Hom}_{D(X)}(\mathcal{O}_x,\mathcal{O}_y[i]) = 0.
    $$
    </li>
    <li>
 If $C \in D(X)$ is an object such that for all $x \in X$ and $i \in \Bbb Z$,
 $$
    \operatorname{Hom}_{D(X)}(\mathcal{O}_x,C[i]) = 0,
    $$  
 then $C = 0$ in $D(X)$.
    </li>
</ol>
</div>

If one denotes $\iota_x : \{x\} \to X$ the inclusion and notes that $\mathcal{O}\_x$ is just a shorthand for $\iota_{x\ast}\mathcal{O}_x$, then by adjunction

$$
\operatorname{Hom}_{D(X)}(\iota_{x\ast}\mathcal{O}_x, \iota_{y\ast}\mathcal{O}_y[i]) \cong \operatorname{Hom}_{D(X)}(L\iota^\ast_{q}(\iota_{x\ast}\mathcal{O}_x), \mathcal{O}_y[i]).
$$

The first item follows from the Koszul resolution of $\iota\_{y\ast}\mathcal{O}\_y$ on $X$ and the second item follows from the fact that the support of $\iota_{x\ast}\mathcal{O}_x$ is disjoint from $y$. The last one is a bit more involved. For any $\mathcal{A} \in D(X)$ and $x \in X$ you look at the spectral sequence

$$
E^{p,q}_2 = \operatorname{Ext}^p_X(H^{-q}(A),\mathcal{O}_x) \implies \operatorname{Hom}_{D(X)}^{p+q}(A, \mathcal{O}_x)
$$

and then utilize Serre duality. The idea here is that the set $\\{\mathcal{O}_x \mid x \in X\\}$ can be loosely interpreted as an "orthonormal basis" of the derived category. The first and second items express "normalization" and "orthogonality" and the last one states that the set $\\{\mathcal{O}_x \mid x \in X\\}$ is a so-called <i>spanning class</i>.

The following theorem by Bondal-Orlov and Bridgeland provides an analogy of the linear algebra principle that the behavior of a linear map between inner product spaces can be fully described by its action on an orthonormal basis.

<div class="theorem">
Let $\mathcal{F} \in D(X \times Y)$ be a derived correspondence between smooth projective varieties $X$ and $Y$. For $x \in X$, let

$$
\iota_x : Y = \{x\} \times Y \to X \times Y
$$

denote the inclusion of a fibre of the projection $p_X$, and let $\mathcal{F}_x := L\iota^\ast_x \mathcal{F}$ be the derived pullback (restriction) of $\mathcal{F}$ to the fibre. Then $\Phi_{\mathcal{F}}$ is fully faithful if and only if:

<ol>
    <li>
 For every $x \in X$,
 $$
    \operatorname{Hom}_{D(Y)}(\mathcal{F}_x,\mathcal{F}_x) \cong \Bbb C.
    $$
    </li>
    <li>
 For every $x \ne y$ and $i \in \Bbb Z$,
 $$
    \operatorname{Hom}_{D(Y)}(\mathcal{F}_x,\mathcal{F}_q[i]) = 0.
    $$
    </li>
</ol>
Moreover, $\Phi_{\mathcal{F}}$ is an equivalence if and only if $\dim(X) = \dim(Y)$ and for every $x \in X$

$$
\mathcal{F}_x \otimes \omega_Y \cong \mathcal{F}_x.
$$

</div>

Next time, I'll be discussing the McKay correspondence.


---

[^1]: An additive category in which the hom-sets are $k$-vector spaces and all compositions are $k$-bilinear.