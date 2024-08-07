---
layout: post
title: "Pontryagin and Euler Classes"
categories: [Differential Geometry]
mathjax: true
excerpt_separator: <!--more-->
---

Last time we finished with a quite general description of  <a href="https://anthonymakela.com/differential%20geometry/2023/12/28/characteristic-classes.html" style="color:#680530; text-decoration: underline;">Characteristic Classes</a>. In particular, we gave a construction for the Chern–Weil homomorphism $c_E : \mathrm{Inv}(\mathfrak{gl}(n,\Bbb R)) \to H^\ast(M)$. The goal today is to look at different types of characteristic classes. We'll begin with Pontryagin classes and look at Euler classes afterward. The next post will be about complex vector bundles and Chern classes.

<!--more-->

Recall that the algebra $\mathrm{Inv}(\mathfrak{gl}(n,\Bbb R))$ is generated by the coefficients $f_k(A)$ of the characteristic polynomials and by the trace polynomials $\operatorname{tr}(A^k)$. To determine all characteristic classes of a vector bundle $E \to M$, it is sufficient to compute the characteristic classes associated with either of these sets of polynomials. The characteristic classes we obtain from the polynomials $f_k(A)$ are called <b>Pontryagin Classes</b>.

---

Before diving into Pontryagin classes, let's try to figure out when characteristic classes vanish. I'll first remind you that whenever the bundle $E \to M$ is equipped with a Riemannian metric compatible with a connection $\nabla$, the curvature matrix $\Omega = [\Omega^i_j]$ relative to a local <i>orthonormal</i> frame $(e_i)$ over $U \subset M$ is skew-symmetric. Why is this? The second structural equation relates $\Omega$ to the connection matrix $\omega$ via $\Omega^i_j = d\omega^i_j + \omega^j_k \wedge \omega^k_i$. It would be therefore sufficient to show that $\omega = [\omega^i_j]$ is skew-symmetric as this would imply

$$
\begin{align*}
\Omega^i_j &= d\omega^i_j + \omega^i_k \wedge \omega^k_j \\
&= -d\omega^j_i + \omega^k_i \wedge \omega^j_k \\
&= -d\omega^i_j - \omega^j_k \wedge \omega^k_i \\
&= -\Omega^j_i.
\end{align*}
$$

To show that $\omega$ is skew-symmetric we'll use the compatibility of $\nabla$ with the metric. For any $X \in \Gamma(U, E)$ we have that

$$
\begin{align*}
0 &= X\langle e_i,e_j\rangle \\
&= \langle\nabla_X e_i, e_j\rangle +\langle e_i, \nabla_X e_j \rangle \\
&= \langle \omega^k_i(X)e_k, e_j\rangle + \langle e_i, \omega^k_j(X)e_k \rangle \\
&= \omega^j_i(X) + \omega^i_j(X)
\end{align*}
$$

which yields that $\omega^i_j = -\omega^j_i$ and therefore the skew-symmetry of $\Omega$. Okay, so we've shown that $\Omega$ is a skew-symmetric matrix, what does this have to do with vanishing characteristic classes? Well, notice that we now have

$$
\begin{align*}
f_1(\Omega) &= \operatorname{tr}(\Omega) \\
&= \operatorname{tr} \begin{pmatrix} 
    0 & \dots  & \Omega^1_n\\
    \vdots & \ddots & \vdots\\
    -\Omega^n_1 & \dots  & 0
    \end{pmatrix} \\
    &= 0
\end{align*}
$$

and so $[f_1(\Omega)] = [\operatorname{tr}(\Omega)] = 0$. It would be reasonable to ask, whether this happens for all odd $k$? Turns out that this holds. We will need the following lemma for the proof.

<div class="lemma">
If $A$ is a skew-symmetric matrix of $2$-forms on $M$, then $A^k$ is symmetric for even $k$ and skew-symmetric for odd $k$.
</div>

The proof of the above lemma is a simple induction and will be left for the reader as an exercise. Using this we can conclude that $\Omega^k$ is skew-symmetric for odd $k$. You might have noticed that we have been assuming the orthonormality of the frame and the compatibility of the connection with the metric in the above calculations. Neither of these will be a problem for us, since $\operatorname{tr}(\Omega^k)$ is invariant under conjugation and the cohomology class $[\operatorname{tr}(\Omega^k)]$ is independent of the connection. It is actually quite nice that we are able to use the Levi-Civita connection for example to calculate characteristic classes.

<div class="theorem">
Suppose that a homogeneous invariant polynomial $P(A)$ on $\mathfrak{gl}(n,\Bbb R)$ has odd degree $k$, then for any connection $\nabla$ on any vector bundle $E \to M$ with curvature matrix $\Omega$, the cohomology class $[P(\Omega)]$ is zero in $H^{2k}(M)$.
</div>

<div class="proof">
Equip $E$ with a Riemannian metric and let $\widetilde{\nabla}$ be the Levi-Civita connection on $E$, with curvature matrix $\widetilde{\Omega}$ on a framed open set. Since $P(A)$ is a linear combination with real coefficients in the trace polynomials and $k$ is odd, every monomial term of $P(A)$ has an odd degree i.e. must contain a trace polynomial $\Sigma_m$ of odd degree $m$ as a factor. Since $\Sigma_m(\widetilde{\Omega}) = 0$ implies $P(\widetilde{\Omega}) = 0$ for the trace polynomials with odd degrees, we conclude using the independence of the connection that if $\nabla$ is any connection on $E$ with curvature matrix $\Omega$, then $[P(\Omega)] = [P(\widetilde{\Omega}) ] = 0$.
</div>

---

From the theorem above we concluded that for odd $k$, the polynomials $\Sigma_k(\Omega)$ and $f_k(\Omega)$ are all zero. This tells us that the ring of characteristic classes of $E$ is generated by

<ol>
    <li>
    The trace polynomials of even degrees
    $$
    [\Sigma_2(\Omega)],[\Sigma_4(\Omega)], [\Sigma_6(\Omega)], \dots
    $$
    </li>
<li>
    The coefficients of the characteristic polynomial $\det(\lambda I + \Omega)$ of even degrees
    $$
    [f_2(\Omega)],[f_4(\Omega)], [f_6(\Omega)], \dots
    $$
    </li>    
</ol>

Using these we'll get the following definition.

<div class="definition">
The $k$'th Pontryagin class $p_k(E)$ of a vector bundle $E \to M$ is defined to be
$$
p_k(E) = \left[f_{2k}\left(\frac{i}{2\pi}\Omega\right)\right] \in H^{4k}(M).
$$
</div>

The factor of $i$ is there to make sure that other formulas will be sign-free and the factor of $1/2\pi$ is there to ensure that $p_k(E)$ is the class of an integral form[^1].

Note that we can collect the Pontryagin classes in a single formula[^2] given by

$$
\begin{align*}
    \left[\det\left(\lambda I + \frac{i}{2\pi} \Omega\right)\right] &= \lambda^n + p_1(E)\lambda^{n-2} + \dots + p_{\lfloor n/2\rfloor}(E)\lambda^{n-2\lfloor n/2\rfloor}
\end{align*}
$$

where $n$ is the rank of $E$. Using this we'll define the <b>total Pontryagin class</b> by setting $\lambda = 1$ to get

$$
p(E) := \left[\det\left(I + \frac{i}{2\pi} \Omega\right)\right] = 1 + p_1(E) + \dots + p_{\lfloor n/2\rfloor}(E).
$$

Now as $\Omega$ is a $\mathfrak{gl}(n,\Bbb R)$-valued $2$-form, $f_{2k}\left(\frac{i}{2\pi} \Omega\right)$ is a $4k$-form. It follows that $p_k(E)^{a_i}$ has degree $4ka_i$ and so the monomial $p_1(E)^{a_1}p_2(E)^{a_2}\cdots p_{\lfloor n/2\rfloor}(E)^{a_{\lfloor n/2\rfloor}}$ has degree

$$
4a_1 + 8a_2 + \dots + 4\lfloor \frac{n}{2}\rfloor a_{\lfloor n/2\rfloor} = 4\left(a_1 + a_2 + \dots + \lfloor \frac{n}{2}\rfloor a_{\lfloor n/2\rfloor}\right).
$$

When this equals, say $\dim M = 4m$, we can compute the integral

$$
\int_M p_1(E)^{a_1}p_2(E)^{a_2}\cdots p_{\lfloor n/2\rfloor}(E)^{a_{\lfloor n/2\rfloor}}
$$

which we will call a <b>Pontryagin number</b> of $E$. The following theorem gives us a neat way to calculate total Pontryagin classes for direct sums of vector bundles.

<div class="theorem" text="(Whitney)">
Let $E$ and $F$ be vector bundles over $M$, then

$$
p(E \oplus F) = p(E) \smile p(F).
$$

</div>

<div class="proof">
Let $\nabla$ and $\widetilde{\nabla}$ be connections on $E$ and $F$ respectively. Then there is a natural direct sum connection $\nabla \oplus \widetilde{\nabla}$ on $E \oplus F$. If $\Omega$ and $\widetilde{\Omega}$ are the curvature matrices of $E$ and $F$, then the curvature matrix of the sum $E \oplus F$ is given by

$$
\Omega' = \begin{pmatrix}\Omega &0\\ 0&\widetilde{\Omega}\end{pmatrix}.
$$

It follows that the total Pontryagin class of the sum $E \oplus F$ is given by

$$
\begin{align*}
p(E \oplus F) &= \left[\det\left(I + \frac{i}{2\pi} \Omega'\right)\right] \\
&= \left[\det\begin{pmatrix}I + \frac{i}{2\pi}\Omega &0\\ 0&I + \frac{i}{2\pi}\widetilde{\Omega}\end{pmatrix}\right] \\
&= \left[\det\left(I + \frac{i}{2\pi} \Omega\right) \wedge \det\left(I + \frac{i}{2\pi} \widetilde{\Omega}\right)\right] \\
&= p(E)\smile p(F)
\end{align*}
$$

which yields our desired result.

</div>

Here $[\alpha] \smile [\beta]$ is the cup product which in the case of de Rham cohomology is represented by $[\alpha \wedge \beta]$. I might occasionally drop the $\smile$ and just write $[\alpha][\beta]$.

---

Since we can characterize reasonably well Riemannian manifolds with constant curvature, suppose $M$ is such with constant curvature $K$. What can we say about the Pontryagin classes of $M$?

Recall that if $U$ is a framed open set and $(e_i)$ the local frame, then given the dual coframe $(\varepsilon^i)$ we have that

$$
\begin{align*}

\Omega^j_i &= \sum \Omega^j_i(e_k,e_l) \varepsilon^k \wedge \varepsilon^l \\
&= \sum \varepsilon^j(R(e_k,e_l)e_i) \varepsilon^k \wedge \varepsilon^l \\
&= \sum \langle R(e_k,e_l)e_i, e_j\rangle \varepsilon^k \wedge \varepsilon^l \\
&= \sum R_{klij} \varepsilon^k \wedge \varepsilon^l \\
&= -\sum K (\delta_{ki}\delta_{lj} - \delta_{kj}\delta_{li})\varepsilon^k \wedge \varepsilon^l \\
&= -K \varepsilon^i \wedge \varepsilon^j.

\end{align*}
$$

Also the matrix $\Omega$ is skew-symmetric and hence takes the form

$$
\begin{pmatrix}
0 & -K\varepsilon^1 \wedge \varepsilon^2 & -K\varepsilon^1 \wedge \varepsilon^3 & \cdots & -K\varepsilon^1 \wedge \varepsilon^n \\
K\varepsilon^1 \wedge \varepsilon^2 & 0 & -K\varepsilon^2 \wedge \varepsilon^3 & \cdots & -K\varepsilon^2 \wedge \varepsilon^n \\
K\varepsilon^1 \wedge \varepsilon^3 & K\varepsilon^2 \wedge \varepsilon^3 & 0 & \cdots & -K\varepsilon^3 \wedge \varepsilon^n \\
\vdots & \vdots & \vdots & \ddots & \vdots \\
K\varepsilon^1 \wedge \varepsilon^n & K\varepsilon^2 \wedge \varepsilon^n & K\varepsilon^3 \wedge \varepsilon^n & \cdots & 0
\end{pmatrix}.
$$

Observe now that the polynomials $f_{2k}\left(\frac{i}{2\pi}\Omega\right)$ are the sums of the principal $2k \times 2k$ minors of $\Omega$. More explicitly[^3]

$$
\begin{align*}
f_{2k}\left(\frac{i}{2\pi}\Omega\right) &= \frac{(-1)^k}{(2\pi)^{2k}(2k)!}\sum \delta^{i_1,\dots,i_{2k}}_{j_1,\dots,j_{2k}}\Omega^{i_1}_{j_1}\wedge\dots\wedge\Omega^{i_{2k}}_{j_{2k}} \\
&= \frac{(-1)^kK^{2k}}{(2\pi)^{2k}(2k)!}\sum \delta^{i_1,\dots,i_{2k}}_{j_1,\dots,j_{2k}}\varepsilon^{i_1}\wedge \varepsilon^{j_1}\wedge\dots\wedge\varepsilon^{i_k}\wedge \varepsilon^{j_k}.
\end{align*}
$$

Now, notice that the $\delta$'s vanish unless $j_1,\dots,j_{2k}$ is a permutation of $i_1,\dots,i_{2k}$, but if that's the case, then the wedge product of these $\varepsilon$'s has repeated factors yielding that $f_{2k}\left(\frac{i}{2\pi}\Omega\right)$ will vanish no matter what.

There is actually an even stronger result by Chern and Simons stating conformal invariance for Pontryagin classes. This means that for a locally conformally flat manifold the Pontryagin classes vanish.

---

The <b>Euler class</b> can be defined in a few different ways. One way to do this is to use something called a <b>Thom class</b> which you can find in the book "Differential Forms in Algebraic Topology" by Bott & Tu. Instead of this, we will be using the <b>Pfaffian</b> which we can use later on to prove the Generalized Gauss–Bonnet Theorem. 

The key idea with the Euler class is that it is an obstruction to the existence of a nowhere-vanishing section. To get an intuition for the Euler class the following might be a good way to think about it: Whenever you attempt to create a nowhere-vanishing section on a manifold, you'll end up with difficulties in getting the section to function properly on a submanifold. Different approaches might lead to issues on different submanifolds, but interestingly, all these problematic submanifolds represent the same homology class. If this homology class is non-zero, it will be impossible to construct the nowhere-vanishing section successfully.

The following picture illustrates this with $\Bbb S^2$. Trying to construct a nowhere-vanishing section of the tangent bundle i.e. a vector field is not possible due to the Hairy Ball Theorem.

<p align="center">
    <img src="/assets/images/hb.png" alt="image" width="400" height="auto">
</p>

The caveat of Euler classes is that they are only defined for orientable vector bundles. Let's quickly recall how we define an orientation on a vector bundle.

<div class="definition">
An <b>orientation</b> on a vector bundle $E \to M$ of rank $n$ is an equivalence class of nowhere-vanishing sections of the determinant line bundle $\Lambda^n E$, two such sections $s$ and $\sigma$ being equivalent if and only if they are related by multiplication with a positive function on $M$. That is $\sigma = fs$ for $f >0$.
</div>

Nowhere-vanishing sections and line bundles play together quite nicely giving us the following proposition.

<div class="proposition">
A vector bundle $E \to M$ of rank $n$ has an orientation if and only if the determinant line bundle is trivial.
</div>

<div class="proof">
It suffices to show that $\Lambda^n E$ is trivial if and only if it has a nowhere-vanishing section. Suppose that $\varphi : \Lambda^n E \to M \times \Bbb R$ is an isomorphism. Define 

$$
\begin{align*}
s : M &\to \Lambda^n E \\
p &\longmapsto \varphi^{-1}(p, 1).
\end{align*}
$$

The map $s$ is now a nowhere-vanishing section. Conversely, if $\sigma : M \to \Lambda^n E$ is a nowhere-vanishing section, we can define

$$
\begin{align*}
\psi : M \times \Bbb R &\to \Lambda^n E \\
(p,\lambda) &\longmapsto \lambda \sigma(p).
\end{align*}
$$

To show that $\psi$ is an isomorphism we need to show that the maps $\psi_p : \{p\} \times \Bbb R \to \Lambda^n E_p$ are isomorphisms. Note that $\psi_p$ is injective as $\psi_p(p,\lambda) = \lambda\sigma(p) = 0 \implies \lambda = 0$ since $\sigma$ is a nowhere-vanishing section. Finally, notice that $\psi_p$ is an injective linear map of vector spaces with the same dimension and therefore an isomorphism. I should probably point out that there is nothing special about the bundle $\Lambda^n E$ here. The proof generalizes to any line bundle.

</div>

Since we gave more structure to the bundle $E \to M$ by introducing orientation we can consider local frames $e = \begin{bmatrix} e_1 & \cdots & e_n\end{bmatrix}$ of $E$ over an open set $U$ which are positively oriented[^4] and orthonormal. If $\nabla$ is a connection on $E$ we recall that relative to $e$ the matrices $\omega$ and $\Omega$ are both skew-symmetric. For another positively oriented orthonormal local frame $\bar{e}$ over $U$ the frame $e$ transforms as 

$$
\bar{e} = ea
$$

for a smooth function $a : U \to \mathrm{SO}(n)$. Similarly the matrix $\Omega$ transforms via

$$
\bar{\Omega} = a^{-1}\Omega a.
$$

The important thing now is that $a$ is a special orthogonal matrix at each point. This means that, in order to get a global form $P(\Omega)$ on $M$ we do not need $P(\Omega)$ to be invariant under conjugation by all of $\mathrm{GL}(n,\Bbb R)$, but only for elements in $\mathrm{SO}(n)$. Evidently, every $\mathrm{GL}(n,\Bbb R)$-invariant polynomial is also $\mathrm{SO}(n)$-invariant, but could there be an $\mathrm{SO}(n)$-invariant polynomial which isn't $\mathrm{GL}(n,\Bbb R)$-invariant? This would give us a new characteristic class. Turns out that for odd $n$ the only $\mathrm{SO}(n)$-invariant polynomials are the trace polynomials and the coefficients of the characteristic polynomial, but for even $n$ the ring of $\mathrm{SO}(n)$-invariant polynomials has an additional generator, namely the Pfaffian which I mentioned earlier. You might now guess how we are going to define the Euler class.

Let's take a quick excursion to understand the Pfaffian before defining the Euler class. There is a neat fact from linear algebra that if $A$ is a skew-symmetric $n \times n$ matrix with entries in a field $F$, then $\det(A)$ is a perfect square in $F$. Using this it is not too difficult to show that if $A= [a^i_j]$ is an $2m \times 2m$ skew-symmetric matrix of indeterminates, then $\det(A)$ is a perfect square in the ring $\Bbb Z[a^i_j]$. This leads us to the definition of the Pfaffian.

<div class="definition">
The Pfaffian of a $2m \times 2m$ skew-symmetric matrix $A$ is defined to be a polynomial $\operatorname{Pf}(A)$ such that

$$
\det(A) = \left(\operatorname{Pf}(A)\right)^2.
$$
</div>

More explicitly the Pfaffian of $A$ could be defined as

$$
\operatorname{Pf} (A)={\frac {1}{2^{m}m!}}\sum _{\sigma \in S_{2m}}\operatorname {sgn} (\sigma )\prod _{i=1}^{m}a^{\sigma (2i-1)}_{\sigma (2i)}.
$$

<div class="proposition">
Let $A = [a^i_j]$ be a $2m \times 2m$ skew-symmetric matrix and $X = [x^i_j]$ a $2m \times 2m$ matrix of indeterminates. Then

$$
\operatorname{Pf}(X^TAX) = \det(X) \operatorname{Pf}(A) \in \Bbb Z[a^i_j, x^i_j].
$$

</div>

<div class="proof">
Note that

$$
\begin{align*}
\det(X^TAX) &= \det\left(X^T\right)\det(A)\det(X) \\
&= \det(X)^2\det(A).
\end{align*}
$$

Since $A$ is skew-symmetric the matrix $X^TAX$ is also skew-symmetric so

$$
\left(\operatorname{Pf}(X^TAX)\right)^2 = \det(X)^2\left(\operatorname{Pf}(A)\right)^2.
$$

This yields that

$$
\operatorname{Pf}(X^TAX) = \pm \det(X)\operatorname{Pf}(A).
$$

To get the sign correctly, note that if $\operatorname{Pf}(A) = 0$ we win. If $\operatorname{Pf}(A) \ne 0$ and we had $\operatorname{Pf}(X^TAX) = -\det(X)\operatorname{Pf}(A)$, then taking $X = I$ would give $\operatorname{Pf}(A) = - \operatorname{Pf}(A)$ which would result in a contradiction.
</div>

From the above proposition it follows that if $A$ is a $n \times n$ skew-symmetric matrix and $X \in \mathrm{SO}(n)$, then

$$
\begin{align*}
\operatorname{Pf}(X^{-1}AX) &= \operatorname{Pf}(X^{T}AX) \\
&= \det(X)\operatorname{Pf}(A) \\
&= \operatorname{Pf}(A)
\end{align*}
$$

yielding that $\operatorname{Pf}(A)$ is an $\mathrm{SO}(n)$-invariant polynomial on $n \times n$ skew-symmetric matrices.

All in all we see that if $a \in \mathrm{SO}(2m)$, then $\det(a) = 1$ and if $\bar{\Omega}$ is the curvature matrix of a connection $\nabla$ on a vector bundle $E \to M$ with respect to a positively oriented local orthonormal frame $\bar{e}$, then

$$
\begin{align*}
\operatorname{Pf}(\bar{\Omega}) &= \operatorname{Pf}(a^{-1}\Omega a) \\
&= \operatorname{Pf}(a^{T}\Omega a) \\
&= \det(a)\operatorname{Pf}(\Omega) \\
&= \operatorname{Pf}(\Omega).
\end{align*}
$$

So $\operatorname{Pf}(\Omega)$ is independent of the frame and therefore defines a global form on $M$. This form is also closed and independent of the connection[^5], hence it gives a well-defined cohomology class $[\operatorname{Pf}(\Omega)] \in H^{2m}(M)$. 

<div class="definition">
The Euler class $e(E)$ of the real oriented vector bundle $E \to M$ equipped with a Riemannian metric is defined to be

$$
e(E) = \left[\operatorname{Pf}\left(\frac{1}{2\pi}\Omega\right)\right] \in H^{2n}(M).
$$

</div>

---

Before I wrap this up, I want to show you how calculating the Euler class $e\left(T\Bbb S^2\right)$ will hint us towards the Generalized Gauss–Bonnet Theorem.

A Riemannian metric on $\Bbb S^2$ with coordinates $(\theta,\varphi)$ given by the inverse of the parametrization $X(\theta,\varphi) = (\cos\theta\sin\varphi,\sin\theta\sin\varphi,\cos\varphi)$ is given by 

$$
g = d\varphi \otimes d\varphi + \sin^2(\varphi)d\theta \otimes d\theta.
$$

An orthonormal frame is given by $e_1 = \frac{\partial}{\partial \varphi}, e_1 = \frac{1}{\sin(\varphi)}\frac{\partial}{\partial \theta}$, with the corresponding dual coframe $\varepsilon^1 = d\varphi, \varepsilon^2 = \sin(\varphi)d\theta$. Now, in an orthonormal frame the matrix $\omega = [\omega^i_j]$ of connection $1$-forms is skew-symmetric i.e.

$$
\omega = \begin{bmatrix} 0 & \omega^1_2 \\ -\omega^1_2 & 0 \end{bmatrix}
$$

so let's first find $\omega^1_2$. Note that 

$$
\begin{gather*} 
d\varepsilon^1 = 0 \\ 
d\varepsilon^2 = \cos(\varphi)d\varphi \wedge d\theta.
\end{gather*}
$$

Since the form $\omega^1_2$ is a linear combination $\omega^1_2 = ad\varphi + bd\theta$ we can solve for $a$ and $b$ using the first structural equation[^6]:

$$
\begin{align*} 
d\varepsilon^1 &= -\omega^1_2 \wedge \varepsilon^2 \\ 
d\varepsilon^2 &= -\omega^2_1 \wedge \varepsilon^1 = \omega^1_2 \wedge \varepsilon^1.
\end{align*}
$$

The first equation yields

$$
\begin{align*} 
0 &= -(ad\varphi + bd\theta)\wedge \sin(\varphi)d\theta \\
&= -a\sin(\varphi)d\varphi \wedge d\theta\\
&\implies a = 0.
\end{align*} 
$$

From the second equation

$$
\begin{align*} 
\cos(\varphi)d\varphi \wedge d\theta &= (ad\varphi + bd\theta)\wedge d\varphi \\
&= bd\theta \wedge d\varphi \\
&\implies b = -\cos(\varphi).
\end{align*} 
$$

The connection matrix thus reads as

$$
\omega = \begin{bmatrix} 0 & -\cos(\varphi)d\theta \\ \cos(\varphi)d\theta & 0 \end{bmatrix}.
$$

Now note that 

$$
\begin{align*}
\omega \wedge \omega &= \begin{bmatrix} 0 & \omega^1_2 \\ -\omega^1_2 & 0 \end{bmatrix} \wedge \begin{bmatrix} 0 & \omega^1_2 \\ -\omega^1_2 & 0 \end{bmatrix} \\
&= \begin{bmatrix} -\omega^1_2 \wedge \omega^1_2 & 0 \\ 0 & -\omega^1_2 \wedge \omega^1_2 \end{bmatrix} \\
&= \begin{bmatrix} 0 & 0 \\ 0 & 0 \end{bmatrix}.
\end{align*}
$$

This is nice as the second structural equation $\Omega = d\omega + \omega \wedge \omega$ simplifies to $\Omega = d\omega$. We obtain

$$
\Omega = \begin{bmatrix} 0 & \sin(\varphi)d\varphi \wedge d\theta \\ -\sin(\varphi)d\varphi \wedge d\theta & 0 \end{bmatrix}.
$$

The Pfaffian of a $2\times 2$ skew-symmetric matrix is just the $(1,2)$'th entry and so

$$
\operatorname{Pf}(\Omega) = \sin(\varphi)d\varphi \wedge d\theta.
$$

The Euler class is thus given by $e\left(T\Bbb S^2\right) = \left[\frac{1}{2\pi}\sin(\varphi)d\varphi \wedge d\theta\right]$. Now if you are bored enough you might think that since the form $1/2\pi\sin(\varphi)d\varphi \wedge d\theta$ is so simple, let's just see what happens when we integrate it over the manifold. You'll find that

$$
\begin{align*}
\frac{1}{2\pi}\int_{\Bbb S^2} \sin(\varphi)\ d\varphi \wedge d\theta &= \frac{1}{2\pi}\int_{0}^\pi \int_{0}^{2\pi} \sin(\varphi)\ d\varphi \ d\theta \\
&= \frac{1}{2\pi} 4\pi \\
&= 2 \\
&= \chi(\Bbb S^2).
\end{align*}
$$

That is, we've recovered the Euler characteristic of the sphere. This is not a coincidence and is an instance of a generalization of the Gauss-Bonnet theorem. Next time we'll look at complex vector bundles and Chern classes.

---

[^1]: A closed $p$-form is said to be <b>integral</b> if it results in an integer when integrated over any compact oriented submanifold of $M$ with dimension $p$.

[^2]: A quick explanation for the floor function here. Note that for each even integer $2k \le n$ we get a Pontryagin class $p_k(E) = \left[f_{2k}\left(\frac{i}{2\pi}\Omega\right)\right]$. If $n$ is even, then $2\lfloor n/2\rfloor = n$ and if $n$ is odd, then $2\lfloor n/2\rfloor = n-1$. In other words $2\lfloor n/2\rfloor$ is the smallest even integer less than or equal to $n$ and hence $p_{\lfloor n/2\rfloor}(E) = \left[f_{2\lfloor n/2\rfloor}\left(\frac{i}{2\pi}\Omega\right)\right]$ is the last term of our sum. It is also worth mentioning that a bunch of the summands here could potentially be zero depending on the dimension of $M$. To get the last potentially non-zero class one should consider $\min\\{\lfloor n/2\rfloor, \dim M\\}$.

[^3]: See the end of the post <a href="https://anthonymakela.com/algebra/2023/12/18/coefficients-of-the-characteristic-polynomial.html" style="color:#680530; text-decoration: underline;">Coefficients and Characteristic Polynomials</a> 

[^4]: Positively oriented meaning that at each point $p$ in $M$ it agrees with the orientation on $E$.

[^5]: The proof for this follows from a more general result proven in Milnor & Stasheff's book "Characteristic Classes".

[^6]: Given an orthonormal frame $(e_i)$ and a dual coframe $(\varepsilon^j)$, we have that $d\varepsilon^i + \sum_{j}\omega^i_j \wedge \varepsilon^j = 0$ for all $i$.

