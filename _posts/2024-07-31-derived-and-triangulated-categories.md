---
layout: post
title: "Derived and Triangulated Categories"
categories: [Category Theory]
mathjax: true
published: true
excerpt_separator: <!--more-->
---

In the near future, I will write a short series on homological mirror symmetry and hopefully get a chance to talk about something called Bridgeland stability. This ties in somewhat beautifully with the previous discussions we've had here since there is a connection between the theory we are going to develop and the deformed Hermitian-Yang-Mills equation. Since the Bridgeland stability condition is stated in terms of $D^b(X)$, the derived category of coherent sheaves on $X$, we'll need to go over some technical preliminaries first. I'll try to give proper motivations for the series in a later post so this time around, unfortunately, we'll be dealing with only technicalities.

<!--more-->

---

The motivation to consider $D^b(X) := D^b(\textbf{Coh}(X))$ seems to originate from a physics perspective. The objects of this category correspond to $B$-branes in the $B$-model in topological string theory. To get a handle on the complex geometry of $B$-branes, a good starting point is to think of them as complex vector bundles. From there, we can broaden our view naturally to the category of coherent sheaves $\textbf{Coh}(X)$ on $X$. However, not all $B$-branes can be described in terms of objects in $\textbf{Coh}(X)$. To capture the full range of $B$-branes, one needs to consider the "larger" category $D^b(X)$.  

Since I have not talked about derived or triangulated categories here before, we'll be starting from there. 


---

Let $\mathcal{A}$ be an abelian category. A <b>cochain complex</b> in $\mathcal{A}$ is a sequence of objects in $\mathcal{A}$ and morphisms

$$
\dots \longrightarrow A^{i-1} \xrightarrow{\quad d^{i-1} \quad } A^i  \xrightarrow{\quad d^{i} \quad} A^i \longrightarrow \dots,
$$

such that $d^i \circ d^{i-1} = 0$ for all $i$. Given an abelian category $\mathcal{A}$ we can form a new abelian category, the category of complexes $\operatorname{Kom}(\mathcal{A})$. The zero object in this category is given by the zero complex, and a morphism between complexes $f : A^\bullet \to B^\bullet$ is given by a sequence of morphisms $f^i : A^i \to B^i$ in $\mathcal{A}$ such that the following diagram commutes:

$$
\xymatrix{
\dots \ar@{->}[r] & A^{i-1} \ar@{->}[d]^{f^{i-1}} \ar@{->}[r]^{d^{i-1}} & A^i \ar@{->}[r]^{d^{i}} \ar@{->}[d]^{f^i} & A^{i+1} \ar@{->}[d]^{f^{i+1}} \ar@{->}[r] & \dots \\
\dots \ar@{->}[r] & B^{i-1} \ar@{->}[r]_{d^{i-1}} & B^i \ar@{->}[r]_{d^i} & B^{i+1} \ar@{->}[r] & \dots
}
$$

The commutativity of the above diagram says that $f^{i+1} \circ d^i = d^i \circ f^i$, hence we obtain two induced maps 

$$
f^{i+1} : \operatorname{Im}(d^i) \to \operatorname{Im}(d^i)
$$

and

$$
f^{i} : \ker(d^i) \to \ker(d^i).
$$

The existence of kernels and cokernels in $\operatorname{Kom}(\mathcal{A})$ follows from their existence on $\mathcal{A}$. The category $\operatorname{Kom}(\mathcal{A})$ also has something called a <b>shift functor</b>

$$
\Sigma: \operatorname{Kom}(\mathcal{A}) \to \operatorname{Kom}(\mathcal{A})
$$

given by $\Sigma A^{i} = A^{i+1}$ and $\Sigma d^i = -d^{i+1}$. What this does is that it shifts the sequence as


$$
\xymatrix{
\dots \ar@{->}[r] & A^{i-1} \ar@{->}[d]^{\Sigma} \ar@{->}[r]^{d^{i-1}} & A^i \ar@{->}[r]^{d^{i}} \ar@{->}[d]^{\Sigma} & A^{i+1} \ar@{->}[d]^{\Sigma} \ar@{->}[r] & \dots \\
\dots \ar@{->}[r] & A^{i} \ar@{->}[r]_{-d^{i}} & A^{i+1} \ar@{->}[r]_{-d^{i+1}} & A^{i+2} \ar@{->}[r] & \dots
}
$$

The shift is usually written as $A^\bullet[1] = \Sigma A^\bullet$, or more generally $A^\bullet[n] = \Sigma^n A^\bullet$. We'll discuss more about this shortly when we introduce triangulated categories. 

Given a complex $A^\bullet \in \operatorname{Kom}(\mathcal{A})$, the ith cohomology object is defined as the quotient

$$
H^i(A^\bullet) = \ker(d^i)/\operatorname{Im}(d^{i-1}).
$$

Note that this defines a functor $H^i(-) : \operatorname{Kom}(\mathcal{A}) \to \mathcal{A}$, since a morphism of complexes induces corresponding morphisms on cohomology objects. To put this slightly differently, an object $\operatorname{Kom}(\mathcal{A})$ is a $\Bbb Z$-graded object

$$
A^\bullet = \bigoplus_{i \in \Bbb Z} A^i
$$

of $\mathcal{A}$, equipped with a differential $d : A^\bullet \to A^\bullet$ satisfying $d^2 = 0$.

Differential-graded objects frequently appear in both physics and mathematics. In topology, for example, one associates a complex of free abelian groups to a space $X$, where the cohomology of this complex corresponds to the cohomology groups of $X$. In algebra, it's often useful to replace a module over a ring with various types of resolutions. Our goal is to consider complexes only up to an equivalence relation. A single topological space $X$ can have multiple triangulations, each leading to a different chain complex. However, we aim to associate a unique equivalence class of complexes to $X$. Similarly, different resolutions of a fixed module of a given type are usually not unique, and we want to treat all these resolutions equivalently.

Suppose for example that $\mathcal{F}$ is a coherent sheaf over a projective variety $X$. Then there exists an resolution $\mathcal{E}^\bullet$

$$
0 \longrightarrow \mathcal{F} \xrightarrow{\quad f\quad} \mathcal{E}^0 \longrightarrow \mathcal{E}^1 \longrightarrow \mathcal{E}^2 \longrightarrow \dots \longrightarrow \mathcal{E}^n \longrightarrow 0        
$$

of $\mathcal{F}$ by locally free sheaves $\mathcal{E}^i$, i.e. vector bundles. One can now study $\mathcal{F}$ in terms of this resolution and we would not want to distinguish between

$$
0 \longrightarrow \mathcal{F} \longrightarrow 0
$$

and

$$
0 \longrightarrow \mathcal{E}^0 \longrightarrow \mathcal{E}^1 \longrightarrow \mathcal{E}^2 \longrightarrow \dots \longrightarrow \mathcal{E}^n \longrightarrow 0,
$$

since different resolutions of the same sheaf will generally lead to complexes that are not identical, but these complexes should be considered equivalent if they produce the same cohomology. The map $f$ above yields a quasi-isomorphism of the complexes. Indeed, consider

$$
\xymatrix{
0 \ar@{->}[r] & \mathcal{F} \ar@{->}[r] \ar@{->}[d]^{f} & 0 \ar@{->}[r] \ar@{->}[d] & \dots \ar@{->}[r] & 0 \ar@{->}[r] \ar@{->}[d] & 0 \\
0 \ar@{->}[r] & \mathcal{E}^0 \ar@{->}[r] & \mathcal{E}^1 \ar@{->}[r] & \dots \ar@{->}[r] & \mathcal{E}^n \ar@{->}[r] & 0.
}
$$

Since $H^i(\mathcal{E}^\bullet) = 0$ for all $i \ge 1$ we only need to consider the morphism $f$. We have that $H^0(\mathcal{F}) = \mathcal{F}$ and $H^0(\mathcal{E}^\bullet) = \operatorname{Im}f$. Since $\ker f$ we obtain $\operatorname{Im}f = \mathcal{F}$. Hence $H^0(f) : H^0(\mathcal{F}) \to H^0(\mathcal{E})$ is an isomorphism and $f$ a quasi-isomorphism.


<div class="definition">
A morphism of complexes $f : A^\bullet \to B^\bullet$ is called a quasi-isomorphism (qis) if the induced morphisms on cohomology
$$
H^i(f) : H^i(A^\bullet) \to H^i(B^\bullet)
$$
are isomorphisms for all $i$.
</div>

<div class="definition">
Two complexes $A^\bullet$ and $B^\bullet$ of $\operatorname{Kom}(\mathcal{A})$ are called quasi-isomorphic if there exists a complex $C^\bullet$ and morphisms $f : C^\bullet \to A^\bullet$, $g : C^\bullet \to B^\bullet$
$$
\xymatrix{
 & C^\bullet \ar@{->}[ld]^{f} \ar@{->}[rd]_{g} &  \\
A^\bullet &  & B^\bullet
} 
$$
such that $H^i(f)$ and $H^i(g)$ are isomorphisms for all $i$. That is, $f$ and $g$ are quasi-isomorphisms.
</div>

It is worth emphasizing here that quasi-isomorphic complexes have isomorphic cohomology groups, but the converse does not hold generally.

The derived category $D(\mathcal{A})$ is the category where the quasi-isomorphisms in $\operatorname{Kom}(\mathcal{A})$ are isomorphisms. In fact, we can formally invert all the quasi-isomorphisms in $\operatorname{Kom}(\mathcal{A})$ as follows.

<div class="lemma">
There exists a category $D(\mathcal{A})$ and a functor
$$
Q : \operatorname{Kom}(\mathcal{A}) \to D(\mathcal{A})
$$
such that:
<ol>
    <li>
 $Q$ inverts all the quasi-isomorphisms
    </li>
    <li>
 $Q$ is universal with this property. If $Q' : \operatorname{Kom}(\mathcal{A}) \to \mathcal{D}$ is another functor that inverts quasi-isomorphisms, then there exists a functor $F : D(\mathcal{A}) \to \mathcal{D}$ and an isomorphism of functors $Q' \cong F \circ Q$.
    </li>
</ol>
</div>
<div class="proof">
Consider $\operatorname{Kom}(\mathcal{A})$ as an oriented graph $\Gamma$, with the objects lying at the vertices and the morphisms being directed edges. Let $\Gamma_\ast$ be the graph obtained from $\Gamma$ by adding one extra edge $s^{-1} : b \to a$ for each quasi-isomorphism $s : a \to b$. It follows that a finite path in $\Gamma_\ast$ is a sequence of the form $f_1\cdot f_2 \cdots f_{r-1}\cdot f_r$ where each $f_i$ is either a morphism of $\operatorname{Kom}(\mathcal{A})$, or is of the form $s^{-1}$ for some quasi-isomorphism $s$. There is a unique minimal equivalence relation $\sim$ on the set of finite paths in $\Gamma_\ast$ generated by the relations:
<ol>
    <li>
 $s \cdot s^{-1} \sim \operatorname{id}_b$ and $s^{-1} \cdot s \sim \operatorname{id}_a$ for each quasi-isomorphism $s : a \to b$ in $\operatorname{Kom}(\mathcal{A})$.
    </li>
    <li>
 $g \cdot f \sim g \circ f$ for composable morphisms $f : a \to b$ and $g : b \to c$ of $\operatorname{Kom}(\mathcal{A})$.
    </li>
</ol>
Define now $D(\mathcal{A})$ to be the category whose objects are the vertices of $\Gamma_\ast$ and whose morphisms are given by equivalence classes of paths in $\Gamma_\ast$. Define $Q : \operatorname{Kom}(\mathcal{A}) \to D(\mathcal{A})$ by using the identity morphism on objects, and by sending a morphism $f$ of $\operatorname{Kom}(\mathcal{A})$ to the length one path in $\Gamma_\ast$ defined by $f$. Then $Q$ satisfies the two conditions of the lemma.
</div>
The second condition ensures that $D(\mathcal{A})$ is unique up to the equivalence of categories. The functor $Q$ is called the localization functor. Note that there is also a fully faithful functor

$$
J : \mathcal{A} \to \operatorname{Kom}(\mathcal{A})
$$

sending an object of $A$ to the trivial complex $A^\bullet$. Composing this with $Q$ we obtain a functor $\mathcal{A} \to D(\mathcal{A})$. It turns out that this functor is also fully faithful and therefore defines an embedding of $\mathcal{A}$ to $D(\mathcal{A})$. Also by definition, $H^i(-) : \operatorname{Kom}(\mathcal{A}) \to \mathcal{A}$ inverts quasi-isomorphisms and hence descends to functor $D(\mathcal{A}) \to \mathcal{A}$.


---

The construction of the derived category $D(\mathcal{A})$ given above works well for abstract purposes, but unfortunately, it does not tell us much about $D(\mathcal{A})$. For example, it does not immediately tell us what kind of structure the category has. Fortunately for us, there is a way to get a better handle of $D(\mathcal{A})$.

Suppose again that $\mathcal{A}$ is an abelian category and $f,g : A^\bullet \to B^\bullet$ morphisms of complexes. We say that $f$ and $g$ are <b>homotopic</b> if there exists morphisms $h^i : A^i \to B^{i-1}$ such that

$$
g^i - f^i  = d^{i-1} \circ h^i + h^{i+1} \circ d^i.
$$

The following commutative diagram expresses this:

$$
\xymatrix@C=6em{
\dots \ar@{->}[r]^{d^{i-2}} & A^{i-1} \ar@{->}[r]^{d^{i-1}} \ar@{->}[ld] \ar@{->}[d]^{f^{i-1},g^{i-1}} & A^i \ar@{->}[r]^{d^{i}} \ar@{->}[ld]^{h^i} \ar@{->}[d]^{f^{i},g^i} & A^{i+1} \ar@{->}[r]^{d^{i+1}} \ar@{->}[ld]^{h^{i+1}} \ar@{->}[d]^{f^{i+1},g^{i+1}} & \dots \ar@{->}[ld]^{h^{i+2}} \\
\dots \ar@{->}[r]_{d^{i-2}} & B^{i-1} \ar@{->}[r]_{d^{i-1}} & B^i \ar@{->}[r]_{d^{i}} & B^{i+1} \ar@{->}[r]_{d^{i+1}} & \dots
}
$$

The homotopy category $K(\mathcal{A})$ is obtained from the category of complexes by identifying homotopic morphisms. The objects of $K(\mathcal{A})$ are thus the same as $\operatorname{Kom}(\mathcal{A})$, but the morphisms are homotopy equivalence classes of morphisms.

<div class="lemma">
Let $\mathcal{A}$ be an abelian category and $Q : \operatorname{Kom}(\mathcal{A}) \to D(\mathcal{A})$ the localization functor. If $f,g : A^\bullet \to B^\bullet$ are homotopic, then $Q(f) = Q(g)$.
</div>

The process of defining the derived category is similar to the problem of localizing rings. This is because an additive category is essentially a generalized version of a ring. To illustrate, let’s consider the concept of localization in the context of rings.

Suppose $A$ is a ring (not necessarily commutative), and let $S$ be a subset of $A$ containing non-zero elements such that $1 \in S$ and if $s, t \in S$, then $st \in S$. Our goal is to construct a new ring $B$ and a homomorphism $Q : A \to B$ such that every element $Q(s)$ for $s \in S$ becomes invertible in $B$. Additionally, if there is another ring $B'$ and a homomorphism $Q' : A \to B'$ with the same property, then $Q'$ should factor through $Q$.

To achieve this, we can create a set $B$ by introducing symbols $s^{-1}$ for each $s \in S$ into $A$. We then define the relations $ss^{-1} = s^{-1}s = 1$ for all $s \in S$ and $(st)^{-1} = t^{-1}s^{-1}$ for all $s, t \in S$. This ensures that every element of $B$ can be expressed in terms of elements from $A$ and their inverses from $S$.

However, in the general non-commutative case, expressions in $B$ can become complicated. Elements of $B$ look like $r_1s_1^{-1}r_2s_2^{-1}\cdots r_ns_n^{-1}$, where $r_i \in A$ and $s_i \in S$. Determining when two such expressions represent the same element in $B$ is not straightforward, and there is no simple method to add these expressions directly.

If $A$ is commutative, the situation simplifies significantly. In this case, since $fs = sf$, we have $s^{-1}f = fs^{-1}$. This commutativity allows us to combine "denominators," so every element in $B$ can be written as $fs^{-1}$ for $f \in A$ and $s \in S$. The addition of fractions can then be handled as follows:

$$
fs^{-1} + gt^{-1} = (tf + sg)(st)^{-1}.
$$

This familiar method of adding fractions addresses the problem effectively in the commutative case. In the non-commutative case, this trick still works sometimes. What we need is the following conditions on the set $S$, usually called the Ore conditions:
<ol>
    <li>
 For every $s \in S$ and $r \in A$ there exists a $t \in S$ and $g \in A$ such that $rt = sg$.
    </li>
    <li>
 Given $r \in A$ there exists an $s \in S$ with $fs = 0$ if and only if there exists a $t \in S$ with $tr = 0$ 
    </li>
</ol>
We can now write $s^{-1}r = gt^{-1}$ and collect denominators ad before. Also, every element of $B$ can be written in the form $rs^{-1}$ for $r \in A$ and $s \in S$, and two such expressions $r_is^{-1}_i$ for $i = 1,2$ define the same element of $B$ if there are elements $t_1,t_2 \in S$ such that $s_1t_1 = s_2t_2$ and $r_1t_1 = r_2t_2$. Lastly, any two elements $b_1$ and $b_2$ of $B$ can be "put over a common denominator", which is to say that they can be written in the form $b_i = f_is^{-1}$ for a fixed $s \in S$. These can then be added by setting

$$
b_1 + b_2 = (f_1+f_2)s^{-1}.
$$

This operation makes $B$ into a ring as required. Now remarkably, Verdier discovered that inside $K(\mathcal{A})$ the set of quasi-isomorphisms satisfy the following analog of the Ore conditions:

<div class="lemma">
Let $\mathcal{A}$ be an abelian category and $K(\mathcal{A})$ the homotopy category of complexes and homotopy classes of morphisms of complexes.
<ol>
    <li>
 If $f : A^\bullet \to B^\bullet$ and $s : C^\bullet \to B^\bullet$ are morphisms in $K(\mathcal{A})$, with $s$ a quasi-isomorphism, then there exists a complex $D^\bullet$ and morphisms of complexes $g : D^\bullet \to C^\bullet$ and $t : D^\bullet \to A^\bullet$ with $t$ a quasi-isomorphism such that the diagram:
 $$
    \xymatrix{
 D^\bullet \ar@{->}[d]_{t} \ar@{->}[r]^{g} & C^\bullet \ar@{->}[d]^{s} \\
 A^\bullet \ar@{->}[r]_{f} & B^\bullet
 }
    $$
 commutes.
    </li>
    <li>
 If $f : A^\bullet \to B^\bullet$ is a morphism in $K(\mathcal{A})$, then there is a quasi-isomorphism $s : C^\bullet \to A^\bullet$ with $f \circ s = 0$ in $K(\mathcal{A})$ precisely if there exists a quasi-isomorphism $t : B^\bullet \to D^\bullet$ with $t \circ f = 0$ in $K(\mathcal{A})$.
    </li>
</ol>
</div>
Using this, we can conclude that the localization functor

$$
Q_K : K(\mathcal{A}) \to D(\mathcal{A})
$$

has properties analogous to the ones described earlier. Any morphism $f : A^\bullet \to B^\bullet$ in $D(\mathcal{A})$ can be represented by a "fraction" or a "roof" in $K(\mathcal{A})$, which is to say by a diagram

$$
\xymatrix{
 & C^\bullet \ar@{->}[rd]^{f} \ar@{->}[ld]_{s} &  \\
A^\bullet &  & B^\bullet,
}
$$

where $s : C^\bullet \to A^\bullet$ is a quasi-isomorphism. Two roofs 

$$
\xymatrix{
 & C^\bullet_1 \ar@{->}[ld]_{s_1} \ar@{->}[rd]^{f_1} &  \\
A^\bullet &  & B^\bullet
}
$$

and

$$
\xymatrix{
 & C^\bullet_2 \ar@{->}[ld]_{s_2} \ar@{->}[rd]^{f_2} &  \\
A^\bullet &  & B^\bullet
}
$$

are said to be equivalent if they are dominated in the homotopy category $K(\mathcal{A})$ by a third roof, i.e. there exists a commutative diagram in $K(\mathcal{A})$ of the form:

$$
\xymatrix{
 &  & C^\bullet \ar@{->}[rd] \ar@{->}[ld]_{s} &  &  \\
 & C_1^\bullet \ar@{->}[ld]_{s_1} \ar@{->}[rrrd]^{f_1} &  & C_2^\bullet \ar@{->}[rd]^{f_2} \ar@{->}[llld]^{s_2} &  \\
A^\bullet &  &  &  & B^\bullet.
}
$$

The next thing we need to consider are compositions of morphisms. Suppose that we are given two morphisms represented by roofs

$$
\xymatrix{
 & C^\bullet_1 \ar@{->}[ld]_{s_1} \ar@{->}[rd]^{f_1} &  \\
A^\bullet &  & B^\bullet
}
$$

and

$$
\xymatrix{
 & C^\bullet_2 \ar@{->}[ld]_{s_2} \ar@{->}[rd]^{f_2} &  \\
B^\bullet &  & C^\bullet.
}
$$

The composition is then represented by the commutative diagram given by:

$$
\xymatrix{
 &  & C^\bullet_0 \ar@{->}[rd] \ar@{->}[ld]_{s} &  &  \\
 & C_1^\bullet \ar@{->}[ld]_{s_1} \ar@{->}[rd]^{f_1} &  & C_2^\bullet \ar@{->}[rd]^{f_2} \ar@{->}[ld]_{s_2} &  \\
A^\bullet &  & B^\bullet &  & C^\bullet.
}
$$

To show that this diagram actually exists and is defined uniquely in $D(\mathcal{A})$, we need to introduce something called the mapping cone. Introducing this will give us means also to consider $D(\mathcal{A})$ as a triangulated category.

---

Let $\mathcal{A}$ be an abelian category. The above discussions imply that $D(\mathcal{A})$ is an additive category, but generally speaking, the morphisms in $D(\mathcal{A})$ do not have kernels or cokernels. That is, $D(\mathcal{A})$ is generally not abelian and we do not have a notion of short exact sequences in $D(\mathcal{A})$. Fortunately, there is a weaker substitute called a <b>distinguished triangle</b>. Before we dive into these, let's go over some basics related to triangulated categories.

A triangulated category $\mathcal{C}$ is a special type of additive category. Such a category needs to have a shift functor, a set of distinguished triangles, and satisfy a certain set of special axioms called the TR axioms.

<div class="definition">
Let $\mathcal{C}$ be an additive category. $\mathcal{C}$ is called triangulated if there exists an additive equivalence
$$
\Sigma : \mathcal{C} \to \mathcal{C}
$$
called the shift functor, and a set of distinguished triangles 
$$
A \longrightarrow B \longrightarrow C  \longrightarrow  \Sigma A
$$
subject to the TR axioms.
</div>

As before, we'll adopt the notation 

$$
A[1] := \Sigma A
$$

for any object $A \in \mathcal{C}$ and $f[1]:= \Sigma f \in \operatorname{Hom}(A[1],B[1])$ for any morphism $f \in \operatorname{Hom}(A,B)$. For any $n \in \Bbb Z$, we'll write $A[n] = \Sigma^n A$ and $f[n] = \Sigma^n f$. A morphism between two triangles

$$
A \longrightarrow B \longrightarrow C  \longrightarrow A[1]
$$

and

$$
A' \longrightarrow B' \longrightarrow C'  \longrightarrow A'[1]
$$

is given by a commutative diagram

$$
\xymatrix{
A \ar[r] \ar[d]_{f} & B \ar[r] \ar[d]_{g} & C \ar[r] \ar[d]_{h} & A[1] \ar[d]^{f[1]} \\
A' \ar[r] & B' \ar[r] & C' \ar[r] & A'[1].
}
$$

A morphism like this is called an isomorphism if $f,g$, and $h$ are isomorphisms. Let's now go over the TR axioms.

**TR1**
<ol>
    <li>
 Any triangle of the form 
 $$
 A \longrightarrow A \longrightarrow 0  \longrightarrow A[1]
    $$
 is distinguished.
    </li>
    <li>
 Any triangle isomorphic to a distinguished triangle is distinguished
    </li>
    <li>
 Any morphism $f: A \to B$ can be completed to a distinguished triangle
 $$
 A \longrightarrow B \longrightarrow C  \longrightarrow A[1].
    $$
    </li>
</ol>

**TR2** The triangle 

$$
\xymatrix{
A \ar@{->}[r]^{f} & B \ar@{->}[r]^{g} & C \ar@{->}[r]^{h} & A[1]
}
$$

is distinguished if and only if 

$$
\xymatrix{
B \ar@{->}[r]^{g} & C \ar@{->}[r]^{h} & A[1] \ar@{->}[r]^{-f{[1]}} & A
}
$$

is distinguished.

**TR3** Suppose that there exists a commutative diagram of distinguished triangles with vertical arrows $f$ and $g$:

$$
\xymatrix{
A \ar[r] \ar[d]_{f} & B \ar[r] \ar[d]_{g} & C \ar[r] \ar@{-->}[d]_{h} & A[1] \ar[d]^{f[1]} \\
A' \ar[r] & B' \ar[r] & C' \ar[r] & A'[1].
}
$$

Then the diagram can be completed to a commutative diagram, i.e. to a morphism of triangles, by a morphism $h : C \to C'$.

**TR4** This is called <i>the octahedral axiom</i>. It states that given $A,B,C,D$ and $E$ and the solid arrows in the octahedron:

$$
\xymatrix{
 & B \ar[rd] \ar[ldd] &  \\
D \ar[ru]^{[1]} \ar@{-->}[d]_{[1]} &  & E \ar[ll] \ar@{-->}[ldd] \\
C \ar[rr]^{[1]} \ar@{-->}[rd] &  & A \ar[luu] \ar@{-->}[u] \\
 & F \ar@{-->}[luu] \ar@{-->}[ru]_{[1]} &
}
$$

there is an object $F$ such that the octahedron may be completed with the dotted arrows. The pairs of maps that combine to form maps between $B$ and $F$ also commute.

Next, recall the notion of a mapping cone.

<div class="definition">
Let $f : A^\bullet \to B^\bullet$ be a morphism in $\operatorname{Kom}(\mathcal{A})$. The mapping cone $C(f)$ is defined to be the complex
$$
C(f)=A^\bullet[1]\oplus B^\bullet=\dots \longrightarrow A^{n}\oplus B^{n-1}\longrightarrow A^{n+1}\oplus B^{n}\longrightarrow A^{n+2}\oplus B^{n+1}\longrightarrow \cdots
$$
with differential 
$$
d={\begin{pmatrix}d_{A[1]}&0\\f[1]&d_{B}\end{pmatrix}}.
$$
</div>

The following definition will now be the key in turning $D(\mathcal{A})$ and $K(\mathcal{A})$ into triangulated categories.

<div class="definition">
Let $\mathcal{A}$ be an abelian category. In $D(\mathcal{A})$ or $K(\mathcal{A})$, we define a distinguished triangle to be a triangle isomorphic to one of the form

$$
\xymatrix{
A^\bullet \ar@{->}[rr]^{f} &  & B^\bullet \ar@{->}[ld] \\
 & C(f). \ar@{-->}[lu] & 
}
$$
</div>

Now, because we have defined distinguished triangles in $D(\mathcal{A})$ to be isomorphic to the distinguished triangles coming from mapping cones, we immediately get the following result:

<div class="proposition">
Every distinguished triangle $A^\bullet \longrightarrow B^\bullet \longrightarrow C^\bullet \longrightarrow A^\bullet[1]$ results in a long exact sequence in cohomology
$$
\dots \longrightarrow H^i(A^\bullet) \longrightarrow H^i(B^\bullet) \longrightarrow H^i(C^\bullet) \longrightarrow H^{i+1}(A^\bullet) \longrightarrow \dots
$$
</div> 

---

The concept of derived equivalences leads to the intriguing result that a fixed derived category $\mathcal{D}$ can correspond to various seemingly unrelated algebraic and geometric objects. For instance, $\mathcal{D}$ can simultaneously represent the derived category of sheaves on a projective space and the derived category of modules over a finite-dimensional algebra. These different manifestations of $\mathcal{D}$ can be viewed as different geometric or algebraic "phases" of the same underlying theory. The key to handling these different phases concurrently lies in the notion of a $t$-structure.

A brief overview of $t$-structures is necessary before delving into the derived categories of coherent sheaves on $X$. An abelian category $\mathcal{A}$ is embedded in its derived category $D(\mathcal{A})$ as the subcategory of complexes whose cohomology is concentrated in degree zero. Specifically, a complex $A^\bullet$ is said to be concentrated in degree $k$ if $H^i(A^\bullet) = 0$ for $i \ne k$. Numerous interesting algebraic and geometric relationships can be captured by an equivalence of derived categories

$$
F : D(\mathcal{A}) \to D(\mathcal{B}),
$$

although such equivalences typically do not stem from an equivalence of the underlying abelian categories $\mathcal{A}$ and $\mathcal{B}$. Therefore, the use of derived categories is essential. Shifting perspectives slightly, one can think of a derived equivalence $D(\mathcal{A}) \cong D(\mathcal{B})$ as a single triangulated category containing two different abelian categories. The theory of $t$-structures enables one to discern these distinct abelian categories within the triangulated category. In essence we would like to understand the image of $\mathcal{A} = \mathcal{A}[0]$ in $D(\mathcal{B})$.

<div class="definition">
Let $\mathcal{D}$ be a triangulated category. A <b>t-structure</b> on $\mathcal{D}$ is a pair $(\mathcal{D}^{\le 0},\mathcal{D}^{\ge 0})$ of full subcategories satisfying the following axioms:
<ol>
    <li>
 $\mathcal{D}^{\le 0} \subset \mathcal{D}^{\le 1}$ and $\mathcal{D}^{\ge 0} \supset \mathcal{D}^{\le 1}$.
    </li>
    <li>
 If $X$ is an object of $\mathcal{D}^{\le 0}$ and $Y$ is an object of $\mathcal{D}^{\le 1}$, then $\operatorname{Hom}_{\mathcal{D}}(X,Y) = 0$.
    </li>
    <li>
 If $A$ is an object of $\mathcal{D}$, then there exists a distinguished triangle
 $$
 X \longrightarrow A \longrightarrow Y \longrightarrow X[1]
    $$
 such that $X$ is an object of $\mathcal{D}^{\le 0}$ and $Y$ an object of $\mathcal{D}^{\ge 1}$.
    </li>
</ol>
</div>

The <b>heart</b> of a $t$-structure on $\mathcal{D}$ is the full subcategory defined by

$$
\mathcal{D}^\heartsuit = \mathcal{D}^{\le 0} \cap \mathcal{D}^{\ge 0}.
$$

There is a sort of a canonical $t$-structure on any derived category $D(\mathcal{A})$ of an abelian category $\mathcal{A}$. One defines

$$
D(\mathcal{A})^{\le 0} := \{ A^\bullet \mid \forall i > 0, H^i(A^\bullet) = 0 \}
$$

and

$$
D(\mathcal{A})^{\ge 0} := \{ A^\bullet \mid \forall i < 0, H^i(A^\bullet) = 0 \}.
$$

The heart is then given by

$$
\begin{align*}
D(\mathcal{A})^\heartsuit &= D(\mathcal{A})^{\le 0} \cap D(\mathcal{A})^{\ge 0} \\
&= \{ A^\bullet \mid \forall i \ne 0, H^i(A^\bullet) = 0 \} \\
&\cong \mathcal{A}
\end{align*}
$$

since a complex $A^\bullet$ in $D(\mathcal{A})$ with $H^i(A^\bullet) = 0$ for all $i \ne 0$ is quasi-isomorphic to the complex that has the object $A$ in degree $0$ and zeros elsewhere.

As we are mostly interested in the <i>bounded</i> derived category $D^b(\mathcal{A})$, the notion of a bounded $t$-structure is also worth mentioning here. We say that a $t$-structure on a triangulated category $\mathcal{D}$ is bounded if $\mathcal{D} = \bigcup_{i,j} \mathcal{D}^{\le 0}[i] \cap \mathcal{D}^{\ge 0}[j]$.

<div class="theorem">
A bounded $t$-structure on a triangulated category $\mathcal{D}$ is determined by its heart $\mathcal{D}^\heartsuit$.
</div>

---

Let's now take time to contemplate why we want to work with these categories in the first place. There is a saying: "chain complexes are good and (co)homology is bad." To understand this, let's first acknowledge that cohomology is an incredibly useful tool in various branches of mathematics. However, the point here is that while cohomology provides valuable information, it is derived from a complex, and the complex itself contains more information than its cohomology. This may seem obvious since cohomology is obtained by taking quotients of subspaces within the complex, but the implications are significant.

Consider again the example with a topological space $X$ and its triangulation $T(X)$. This triangulation gives us a complex of simplicial chains $C_\bullet(T(X), \mathbb{Z})$, which inherently contains more information than the cohomology groups. However, the complex is not uniquely associated with $X$ because different choices of triangulation can lead to different chain complexes. Despite this, these different chain complexes will have isomorphic (co)homology groups.

For instance, if $X_1$ and $X_2$ are simply connected, a theorem by Whitehead states that $X_1 \cong X_2$ if and only if there exists a simplicial complex $Y$ and simplicial maps $f_i : Y \to X_i$ inducing quasi-isomorphisms on the simplicial complexes. This implies that while different triangulations lead to different chain complexes, the essential topological information is preserved in their (co)homology.

Thus, if we are interested in studying objects up to homotopy equivalence, the correct notion at the level of homological algebra is quasi-isomorphism. By considering different triangulations of a (simply connected) manifold, we obtain quasi-isomorphic chain complexes. Therefore, to make the chain complex a true topological invariant, we invert quasi-isomorphisms, which leads us to the derived category.

The takeaway here is summarized in the following:
<ol>
    <li>
 The derived category $D(\mathcal{A})$ is the right setting in which to do homological algebra. It retains more information and yields the correct notion of isomorphisms.
    </li>
    <li>
 Short exact sequences of complexes give long exact sequences in (co)homology, which lift to distinguished triangles in the derived category. Every distinguished triangle comes from a short exact sequence.
    </li>
    <li>
 If 
 $$
    0 \longrightarrow A^\bullet \longrightarrow B^\bullet \longrightarrow C^\bullet \longrightarrow 0
    $$
 is a short exact sequence in $\operatorname{Kom}(\mathcal{A})$, then there is a corresponding distinguished triangle
 $$
 A^\bullet \longrightarrow B^\bullet \longrightarrow C^\bullet \longrightarrow A^\bullet[1]
    $$
 in $D(\mathcal{A})$. If
 $$
 A^\bullet \longrightarrow B^\bullet \longrightarrow C(f) \longrightarrow A^\bullet[1]
    $$
 is a distinguished triangle in $D(\mathcal{A})$, then there is a corresponding short exact sequence
 $$
    0 \longrightarrow B^\bullet \longrightarrow C(f) \longrightarrow A^\bullet[-1] \longrightarrow 0
    $$
 in $\operatorname{Kom}(\mathcal{A})$ and their long exact sequences in (co)homology will be isomorphic.
    </li>
</ol>

Next time, we'll specialize into the bounded derived category $D^b(X)$ in a bit more detail.
