---
layout: post
title: "Characteristic Classes"
categories: [Differential Geometry]
mathjax: true
excerpt_separator: <!--more-->
---

The previous post on <a href="https://anthonymakela.com/differential%20geometry/2023/12/27/connection-and-curvature-forms.html" style="color:#680530; text-decoration: underline;">Connection & Curvature Forms</a> recalled some basic notions on Cartan formalism and how these forms transform under a change of frame. This time, we are going to pick up from that and see where it leads us.

<!--more-->

Last time we saw that a connection on a vector bundle $E \to M$ of rank $n$ can be expressed locally by the matrix $\omega = [\omega^i_j]$ of connection $1$-forms. Likewise, the curvature could be represented locally by the matrix $\Omega = [\Omega^i_j]$ of curvature $2$-forms.

Under a change of frame these transformed as $\bar{\omega} = a^{-1}\omega a + a^{-1}da$ and $\bar{\Omega} = a^{-1}\Omega a$. Now while both of these equations are nice, the one considering the curvature is quite remarkable. Essentially it's saying that a change of frame acts on $\Omega$ by conjugation with $a$. If you now reflect back on our discussion about those <a href="https://anthonymakela.com/algebra/2023/12/17/invariant-polynomials.html" style="color:#680530; text-decoration: underline;">Invariant Polynomials</a> you may realize that, since $\Omega$ can be thought of as $\mathfrak{gl}(n,\Bbb R)$-valued two form, it fits exactly in our framework.

What this means is that if $P(A)$ is a polynomial in $n^2$ variables invariant under conjugation by elements of $\mathrm{GL}(n,\Bbb R)$, then the form $P(\Omega)$ will be <i>independent of the frame</i> and define a global form on $M$. Now, when you come across something like this, it's a good chance to get excited and see if we can uncover something interesting on cohomology. Turns out that $P(\Omega)$ is closed and independent of the connection and so $[P(\Omega)]$ is a well-defined element of $H^\ast(M)$ depending only on the invariant polynomial $P(A)$. This gives rise to the famous <b>Chern–Weil homomorphism</b> of algebras

$$
c_E : \mathrm{Inv}(\mathfrak{gl}(n,\Bbb R)) \to H^\ast(M).
$$

For each invariant polynomial $P(A)$ of degree $k$, the class $[P(\Omega)] \in H^{2k}(M)$ is an isomorphism invariant of the bundle $E$. We call $[P(\Omega)]$ a <b>characteristic class</b> of $E$. The form $P(\Omega)$ is called a <b>characteristic form</b>.

---

Let's try to make the above discussion a bit more formal. Let $E \to M$ be a vector bundle over a smooth manifold $M$ and suppose that $\nabla$ is a connection on $E$. Let $e = \begin{bmatrix} e_1 & \cdots & e_n\end{bmatrix}$ and $\bar e = \begin{bmatrix} \bar{e}_1 & \cdots & \bar{e}_n\end{bmatrix}$ be two local frames over an open set $U$. We know from our previous discussions that $\bar{e} = ea$ for some smooth function $a : U \to \mathrm{GL}(n,\Bbb R)$.

Let $P$ be a <i>homogeneous</i> invariant polynomial of degree $k$ on $\mathfrak{gl}(n,\Bbb R)$. If $\Omega = [\Omega^i_j]$ is the curvature matrix of $\nabla$ relative to $e$, then for each $p \in U$ we have that $\Omega_p \in \mathcal{A}^{n\times n}$ where $\mathcal{A}$ is the commutative $\Bbb R$-algebra given by $\mathcal{A} = \bigoplus_{i=0}^\infty \Lambda^{2i}\left(T^\ast_p M\right)$[^1]. Also 

$$
\bar{\Omega}_p = a^{-1}(p)\Omega_p a(p)
$$

for $a(p) \in \mathrm{GL}(n,\Bbb R)$. Since $P$ is invariant under conjugation this yields

$$
\begin{align*}
P(\bar{\Omega}_p) &= P(a^{-1}(p)\Omega_p a(p)) \\
&= P(\Omega_p) \in \Lambda^{2k}\left(T^\ast_p M\right).
\end{align*}
$$

Varying $p$ gives $P(\bar{\Omega}) = P(\Omega) \in \Gamma\left(\Lambda^{2k}T^\ast U\right)$. This means that the $2k$-form[^2] $P(\Omega)$ on $U$ is independent of the frame.

Using this if we consider a trivializing open cover $\\{U_\alpha\\}$ of $E$, frames $e_\alpha$ for each $U_\alpha$ and curvature matrices $\Omega_\alpha$, we can patch[^3] together the collection $\\{P(\Omega_\alpha)\\}$ to get a global $2k$-form on $M$ denoted by $P(\Omega)$.

---

Our main objective today is to prove the following theorem.

<div class="theorem" text="1">
Let $E \to M$ be a rank $n$ vector bundle, $\nabla$ a connection on $E$ and $P$ a homogeneous invariant polynomial of degree $k$ on $\mathfrak{gl}(n,\Bbb R)$. Then

<ol type="i">
    <li>The global $2k$-form $P(\Omega)$ on $M$ is closed.</li>
    <li>The cohomology class $[P(\Omega)] \in H^{2k}(M)$ is independent of the connection.</li>
</ol>
</div>

In order to prove the above theorem recall that the ring $\mathrm{Inv}(\mathfrak{gl}(n,\Bbb R))$ of invariant polynomials on $\mathfrak{gl}(n,\Bbb R)$ is generated either by the coefficients $f_k(A)$ of the characteristic polynomial or by the trace polynomials $\Sigma_k(A) := \operatorname{tr}(A^k)$. It is therefore sufficient to prove the theorem for the trace polynomials.

Currently, defining $\Omega$ requires choosing a connection $\nabla$, which appears to make the cohomology class $[P(\Omega)]$ reliant on $\nabla$. This limitation is problematic as it restricts these specific cohomology classes to vector bundles with predetermined connections, instead of allowing for their application to arbitrary vector bundles.

Thankfully any finite convex linear combination of connections yields a connection again. so if $\nabla^0$ and $\nabla^1$ are two connections on $E$, then for each $t \in [0,1]$ 

$$
\nabla^t = (1-t)\nabla^0 + t\nabla^1
$$

is again a connection on $E$. Also, for each $t \in [0,1]$ the connection $\nabla^t$ yields the connection and curvature matrices $\omega_t$ and $\Omega_t$. It's easy to see that $\omega_t = (1-t)\omega_0 + t\omega_1$, which means that $\omega_t$ depends smoothly on $t$. By the second structural equation, the curvature matrix $\Omega_t$ also depends smoothly on $t$.

Our strategy is to show that, if somehow $\frac{d}{dt}\operatorname{tr}(\Omega^k_t) = d\eta_t$ for some global form $\eta_t$, then integrating this with respect to $t$ yields

$$
\begin{align*}
\operatorname{tr}(\Omega^k_1) - \operatorname{tr}(\Omega^k_0) &= \int_{0}^1\frac{d}{dt}\operatorname{tr}(\Omega^k_t) \ dt \\
&= \int_{0}^1 d\eta_t \ dt \\
&= d \int_{0}^1 \eta_t \ dt
\end{align*}
$$

where $d\int_{0}^1 \eta_t \ dt$ is a global <i>exact</i> form[^4]. Passing to cohomology classes yields that $[\operatorname{tr}(\Omega^k_1)] = [\operatorname{tr}(\Omega^k_0)]$ which would be enough to show that the class $[P(\Omega)]$ doesn't depend on the connection.

---

Before marching onto the proof, we need a couple more auxiliary results. First off, if $A = [\alpha^i_j]$ and $B = [\beta^i_j]$ are matrices of forms of degree $a$ and $b$, then 

<ol type="i">
    <li>
    If $A \wedge B$ and $B \wedge A$ are both defined, then 
    $$
    \operatorname{tr}(A \wedge B) = (-1)^{ab}\operatorname{tr}(B \wedge A).
    $$
    </li>
    <li>
    If $A = [\alpha^i_j]$ is a square matrix of differential forms on $M$, then
    $$
    d\operatorname{tr}(A) = \operatorname{tr}(dA).
    $$
    </li>
</ol>

Each of these is a simple matter to prove and is left as an exercise. Also, for matrices of differential forms we define the wedge product $A \wedge B$ to be the matrix whose $(i,j)$-entry is $(A\wedge B)^i_j = \sum_k \alpha^i_k \wedge \beta^k_j$. That is $A \wedge B$ is the usual matrix product, but instead of multiplying the entries, we take the wedge product. Lastly, $dA$ is defined to be the matrix $[d\alpha^i_j]$.

We also need the following proposition.

<div class="proposition" text="(Generalized second Bianchi identity)">
Let $\nabla$ be a connection on a vector bundle $E$. Suppose $\omega$ and $\Omega$ are the connection and curvature matrices of $\nabla$ relative to a local frame on $U$. Then for any integer $k \ge 1$
$$
d(\Omega^k) = \Omega^k \wedge \omega - \omega \wedge \Omega^k.
$$
</div>

<div class="proof">
For $k = 1$, using the second structural equation yields
$$
\begin{align*}
d\Omega &= d(d\omega) + (d\omega) \wedge \omega - \omega \wedge d\omega \\
&= (\Omega - \omega \wedge \omega) \wedge \omega - \omega \wedge(\Omega - \omega \wedge \omega) \\
&= \Omega \wedge \omega - \omega \wedge \Omega.
\end{align*}
$$
Suppose then that the equation holds for $k = n$. We have that
$$
\begin{align*}
d\Omega^{n+1} &= d(\Omega^n \wedge \Omega) \\
&= d\Omega^n \wedge \Omega + \Omega^n \wedge d\Omega \\
&= (\Omega^n \wedge \omega - \omega \wedge \Omega^n) \wedge \Omega + \Omega^n \wedge d\Omega \\
&= (\Omega^n \wedge \omega - \omega \wedge \Omega^n) \wedge \Omega + \Omega^n \wedge (\Omega \wedge \omega - \omega \wedge \Omega) \\
&= \Omega^n \wedge \omega \wedge \Omega - \omega \wedge \Omega^{n+1} + \Omega^{n+1} \wedge \omega - \Omega^n \wedge \omega \wedge \Omega \\
&= \Omega^{n+1} \wedge \omega - \omega \wedge \Omega^{n+1}.
\end{align*}
$$
The proof follows by induction.
</div>

---

Let's now see how we can construct the global exact form $\eta_t$ we were seeking above. We'll state this as the following proposition.

<div class="proposition">
If $\nabla^t$ is a family of connections on $E$ with connection and curvature matrices $\omega_t$ and $\Omega_t$ relative to a local frame on an open set $U$ depending smoothly on $t \in \Bbb R$, then
$$
\frac{d}{dt}\left(\operatorname{tr}\Omega^k_t\right) = d\left(k\operatorname{tr}(\Omega^{k-1}_t\dot{\omega}_t)\right).
$$
Moreover, the $d\left(k\operatorname{tr}(\Omega^{k-1}_t\dot{\omega}_t)\right)$ can be patched together to obtain a global form on $M$.
</div>

<div class="proof">
Note that for a square matrix of forms, the trace commutes with $\frac{d}{dt}$. This yields

$$
\begin{align*}
\frac{d}{dt}\left(\operatorname{tr}\Omega^k_t\right) &= \operatorname{tr}\left(\frac{d}{dt}\Omega^k_t\right) \\
&= \operatorname{tr}\left(\dot{\Omega}_t\wedge\Omega^{k-1}_t + \Omega_t\wedge\dot{\Omega}_t\wedge\Omega^{k-2}_t + \dots + \Omega^{k-1}_t\wedge\dot{\Omega}_t\right) \\
&=\operatorname{tr}\left(\dot{\Omega}_t\wedge\Omega^{k-1}_t\right) + \operatorname{tr}\left(\Omega_t\wedge\dot{\Omega}_t\wedge\Omega^{k-2}_t\right) + \dots + \operatorname{tr}\left(\Omega^{k-1}_t\wedge\dot{\Omega}_t\right) \\
&= \operatorname{tr}\left(\Omega^{k-1}_t\wedge\dot{\Omega}_t\right) + \operatorname{tr}\left(\Omega^{k-1}_t\wedge\dot{\Omega}_t\right) + \dots + \operatorname{tr}\left(\Omega^{k-1}_t\wedge\dot{\Omega}_t\right) \\
&= k \operatorname{tr}\left(\Omega^{k-1}_t\wedge\dot{\Omega}_t\right).
\end{align*}
$$

Differentiating the structural equation $\Omega_t = d\omega_t + \omega_t \wedge \omega_t$ with respect to $t$ gives us

$$
\begin{align*}
\dot{\Omega}_t &= \frac{d}{dt} d\omega_t + \frac{d}{dt}\left(\omega_t \wedge \omega_t\right) \\
&= d\dot{\omega}_t + \dot{\omega}_t \wedge \omega_t + \omega_t \wedge \dot{\omega}_t
\end{align*}
$$

and so

$$
\begin{align*}
\operatorname{tr}\left(\Omega^{k-1}_t\wedge\dot{\Omega}_t\right) &= \operatorname{tr}\left(\Omega^{k-1}_t\wedge(d\dot{\omega}_t + \dot{\omega}_t \wedge \omega_t + \omega_t \wedge \dot{\omega}_t)\right) \\
&= \operatorname{tr}\left(\Omega^{k-1}_t\wedge d\dot{\omega}_t + \Omega^{k-1}_t\wedge \dot{\omega}_t \wedge \omega_t + \Omega^{k-1}_t\wedge \omega_t \wedge \dot{\omega}_t\right) \\
&= \operatorname{tr}\left(\Omega^{k-1}_t\wedge d\dot{\omega}_t - \omega_t \wedge \Omega^{k-1}_t\wedge \dot{\omega}_t  + \Omega^{k-1}_t\wedge \omega_t \wedge \dot{\omega}_t\right) \\
&= \operatorname{tr}\left(\Omega^{k-1}_t\wedge d\dot{\omega}_t + (-\omega_t \wedge \Omega^{k-1}_t  + \Omega^{k-1}_t\wedge \omega_t) \wedge \dot{\omega}_t\right) \\
&= \operatorname{tr}\left(\Omega^{k-1}_t\wedge d\dot{\omega}_t + (\Omega^{k-1}_t\wedge \omega_t -\omega_t \wedge \Omega^{k-1}_t) \wedge \dot{\omega}_t\right) \\
&= \operatorname{tr}\left(\Omega^{k-1}_t\wedge d\dot{\omega}_t + d\Omega^{k-1}_t \wedge \dot{\omega}_t\right) \\
&= \operatorname{tr}\left(d(\Omega^{k-1}_t \wedge \dot{\omega}_t)\right) \\
&= d\operatorname{tr}\left(\Omega^{k-1}_t \wedge \dot{\omega}_t\right).
\end{align*}
$$

Last thing to note here is that we can actually patch these $\operatorname{tr}\left(\Omega^{k-1}_t \wedge \dot{\omega}_t\right)$ together to obtain a global <i>exact</i> form on $M$. Let $e$ and $\bar{e}$ be two frames such that $\bar{e} = ea$ for $a : U \to \mathrm{GL}(n,\Bbb R)$. The connection matrix transforms by

$$
\bar{\omega}_t = a^{-1}\omega_t a + a^{-1}da.
$$

Notice now that $\dot{\bar{\omega}}_t = \frac{d}{dt}\bar{\omega}_t = a^{-1}\dot{\omega}_ta$ since $a^{-1}da$ does not depend on $t$. We get that 

$$
\begin{align*}
\operatorname{tr}\left(\bar{\Omega}^{k-1}_t \wedge \dot{\bar{\omega}}_t\right) &=  \operatorname{tr}\left(a^{-1}\Omega^{k-1}_ta \wedge a^{-1}\dot{\omega}_ta\right).
\end{align*}
$$

Since $a^{-1}\Omega^{k-1}_ta \wedge a^{-1}\dot{\omega}_ta$ is given by the matrix where the $(i,j)$-entry is 

$$
\begin{align*}
(a^{-1}\Omega^{k-1}_ta \wedge a^{-1}\dot{\omega}_ta)^i_j &= \sum_l a^{-1}(\Omega_t)^i_l a \wedge a^{-1}(\dot{\omega}_t)^l_j a \\
&= \sum_l a^{-1}(\Omega_t)^i_l \wedge (\dot{\omega}_t)^l_j a \\
&= \sum_l (\Omega_t)^i_l \wedge (\dot{\omega}_t)^l_j
\end{align*}
$$

we see that $a^{-1}\Omega^{k-1}_ta \wedge a^{-1}\dot{\omega}_ta=\Omega^{k-1}_t\wedge\dot{\omega}_t$.

Notice that here I'm abusing notation by referring to the entries of the $k-1$'th power $\Omega^{k-1}$ by $(\Omega_t)^i_l$ since adding more indices to the mix would be just stupid at this point.

It follows that

$$
\begin{align*}
\operatorname{tr}\left(\bar{\Omega}^{k-1}_t \wedge \dot{\bar{\omega}}_t\right) &= \operatorname{tr}\left(\Omega^{k-1}_t\wedge\dot{\omega}_t\right)
\end{align*}
$$

and so $\operatorname{tr}\left(\Omega^{k-1}_t\wedge\dot{\omega}_t\right)$ is independent of the frame, yielding our result.

</div>

<div class="proof" text="of Theorem 1.">
<ol type="i">
    <li>
    Let $\omega = [\omega^i_j]$ and $\Omega = [\Omega^i_j]$ be the connection and curvature forms relative to a local frame $e$ over $U$. We have that
    $$
    \begin{align*}
    d\Sigma_k(\Omega) &= d\operatorname{tr}(\Omega^k) \\
    &= \operatorname{tr}(d\Omega^k) \\
    &= \operatorname{tr}(\Omega^k \wedge \omega - \omega \wedge \Omega^k) \\
    &= \operatorname{tr}(\Omega^k \wedge \omega) - \operatorname{tr}(\omega \wedge \Omega^k) \\
    &= (-1)^{2k}\operatorname{tr}(\omega \wedge \Omega^k) - \operatorname{tr}(\omega \wedge \Omega^k) \\
    &= \operatorname{tr}(\omega \wedge \Omega^k) - \operatorname{tr}(\omega \wedge \Omega^k) \\
    &= 0.
    \end{align*}
    $$
    </li>
    <li>
    Suppose that $\nabla^0$ and $\nabla^1$ are two connections on $E$. Then the convex combination $\nabla^t = (1-t)\nabla^0 + t\nabla^1$ for $t \in \Bbb R$ is also a connection on $E$ with connection and curvature matrices $\omega_t$ and $\Omega_t$ over a trivialized open set. Now
    $$
    \frac{d}{dt}\left(\operatorname{tr}(\Omega^k_t)\right) = d(k\operatorname{tr}(\Omega^{k-1}_t\dot{\omega}_t))
    $$
    and so

    $$
    \int^1_0 \frac{d}{dt}\left(\operatorname{tr}(\Omega^k_t)\right) \ dt = \operatorname{tr}(\Omega^k_1) - \operatorname{tr}(\Omega^k_0)
    $$

    as well as

    $$
    \int^1_0 d(k\operatorname{tr}(\Omega^{k-1}_t\dot{\omega}_t)) \ dt = d \int^1_0 k \operatorname{tr}(\Omega^{k-1}_t\dot{\omega}_t) \ dt.
    $$

    It follows that

    $$
    \operatorname{tr}(\Omega^k_1) - \operatorname{tr}(\Omega^k_0) = d \int^1_0 k \operatorname{tr}(\Omega^{k-1}_t\dot{\omega}_t) \ dt.
    $$

    The right-hand side is now a global exact form so passing to cohomology yields that $[\operatorname{tr}(\Omega^k_1)] = [\operatorname{tr}(\Omega^k_0)]$ which proves that the cohomology class of $\operatorname{tr}(\Omega^k)$ is independent of the connection.

    </li>
</ol>
Note that we did most of the heavy lifting for the first item in the Generalized second Bianchi identity and for the second item by coming up with the form $d(k\operatorname{tr}(\Omega^{k-1}_t\dot{\omega}_t))$.
</div>

The above proof shows that for $P(A) \in \mathrm{Inv}(\mathfrak{gl}(n,\Bbb R))$, since $P(\Omega)$ is a polynomial in $\operatorname{tr}(\Omega),\operatorname{tr}(\Omega^2),\dots,\operatorname{tr}(\Omega^k)$, the characteristic form $P(\Omega)$ is closed and the cohomology class $[P(\Omega)]$ independent of the connection.

---

This is a good place to stop for a moment and appreciate what we have done:

<ol>
  <li>We started off with a smooth manifold $M$ and a rank $n$ vector bundle $E \to M$.</li>
  <li>We equipped $E$ with a connection $\nabla$ which gave us a notion of curvature.</li>
  <li>We expressed this curvature locally by the curvature matrix $\Omega$.</li>
  <li>We observed that the curvature matrix transformed by conjugation under a change of frame.</li>
  <li>We used our knowledge about invariant polynomials to come up with a global differential form $P(\Omega)$ that's independent of the local frame.</li>
  <li>We showed that the form $P(\Omega)$ is closed and hence gives us a well-defined cohomology class.</li>
  <li>We finally showed that the obtained class $[P(\Omega)]$ is independent of the connection.</li>
</ol>

All in all, we've managed to come up with <i>diffeomorphism invariants</i> of the vector bundle $E$.

---

Before I'll wrap this up, here is an interpretation of characteristic classes for the categorically inclined. Let's denote the set of all isomorphism classes of vector bundles of rank $k$ over $M$ by $\mathrm{Vect}_k(M)$. Note that $\mathrm{Vect}_k(-)$ and $H^\ast(-)$ are both contravariant functors on $\textbf{Man}^\infty$.

A characteristic class associates to each manifold $M$ a map $c_M : \mathrm{Vect}_k(M) \to H^\ast(M)$ such that if $f : N \to M$ is a smooth map between manifolds and $E \to M$ a vector bundle over $M$, then the following diagram commutes

$$
\xymatrix{
  \mathrm{Vect}_k(M) \ar[r]^{c_M} \ar[d]_{f^\ast} & H^\ast(M) \ar[d]^{f^\ast} \\
  \mathrm{Vect}_k(N) \ar[r]_{c_N} & H^\ast(N).
}
$$

This is means precisely that a characteristic class is a natural transformation

$$
c : \mathrm{Vect}_k \implies H^\ast.
$$

---

[^1]: If this is confusing, you can think of it as follows: $\Omega$ is a matrix consisting of sections of the bundle $\Lambda^2(T^\ast M)$ i.e. $2$-forms. Evaluating at $p$, a section of this bundle (a $2$-form) gives an alternating map $T_pM \times T_pM \to \Bbb R$. $\mathcal{A}$ is now the commutative $\Bbb R$-algebra of such things. There is an unfortunate coincidence in notation as usually, we denote by $\Omega^k(M) := \Gamma\left(\Lambda^k T^\ast M\right)$ the global $k$-forms on a manifold $M$, but we reserve the symbol $\Omega$ now for the curvature matrix.

[^2]: Make sure you understand why this is a $2k$-form. It clarifies the intuition for considering $\mathcal{A}$ also.

[^3]: On the intersections $U_\alpha \cap U_\beta$ the $2k$-forms $P(\Omega_\alpha)$ and $P(\Omega_\beta)$ agree due to $P$ being invariant under conjugation.

[^4]: The commutativity $\int_a^b d\eta_t \ dt = d\left(\int_a^b \eta_t \ dt\right)$ follows from expressing $\eta_t$ locally, comparing $\int_a^b d\eta_t \ dt$ and $d \int_a^b \eta_t \ dt$ and concluding using the Leibniz integral rule.