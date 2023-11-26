---
layout: post
title: "Curvature"
categories: [Differential Geometry, Riemannian Geometry]
published: false
mathjax: true
---

Today will be all about curvature. Specifically we will be looking at the <b>Riemann curvature tensor</b> and something called  <b>Ricci curvature</b>.

Let's begin with the heuristic approach before we dive into the formal definitions. What is curvature? You might have some sort of an idea about what it is for example it might not be too difficult for you to convince yourself that the following surface has some <i>curvature</i>.

{:refdef: style="text-align: center;"}
![saddle](/assets/images/ddg_saddle.png)
{: refdef}

You might even know a method to quantify curvature from your background in vector analysis. Indeed the <i>Frenet frame</i> gives you a way to quantify curvature, but we are now in the realm of Riemannian Geometry and have moved on from the extrinsic geometry which is required for the Frenet frame.

So how can we come up with a method to capture this curviness of a manifold in an intrinsic way? Here is an idea, if $(M,g)$ is a Riemannian manifold, then we know that there exists a unique connection $\nabla$ which is compatible with $g$ i.e. the Levi-Civita connection. Given the connection we have the ability to transport vectors since we can define the so called <i>parallel transport</i> which we have discussed before.




