---
title: "Visualising Activation Functions in Neural Networks"
excerpt: "Using D3, this post visually explores activation functions, a fundamental component of neural networks."
layout: single
categories:
- deep learning
tags:
- machine learning
- deep learning
- activation function
author: "David Sheehan"
redirect_from: /data%20science/deep%20learning/visualising-activation-functions-in-neural-networks/
date: "08 October 2017"
---

{% include base_path %}

In neural networks, activation functions determine the output of a node
from a given set of inputs, where non-linear activation functions allow
the network to replicate complex non-linear behaviours. As most neural
networks are optimised using some form of gradient descent, activation
functions need to be differentiable (or at least, almost entirely
differentiable- see ReLU). Furthermore, complicated activation functions
may produce issues around vanishing and exploding gradients. As such,
neural networks tend to employ a select few activation functions
(identity, sigmoid, ReLU and their variants).

Select an activation function from the menu below to plot it and its
first derivative. Some properties relevant for neural networks are
provided in the boxes on the right.

{% include activation_functions_d3.html %}

If you spot any errors or want your fancy activation function included, then please get in touch! Thanks for reading!!!
