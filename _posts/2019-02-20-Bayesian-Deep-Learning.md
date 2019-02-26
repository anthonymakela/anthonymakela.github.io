---
title: "Bayesian Deep Learning"
excerpt: "Bayesian way to construct and utilize deep learning methods. Why they are so widely applicable and must be applied when we want to solve more complex tasks."
layout: single
author: "Anthony Makela"
date: "2019-02-20"
---


## Uncertainty and deep learning

Understanding where the model lacks and what it doesn't know is a crucial part of many deep learning systems. Unfortunately, current deep learning algorithms are usually incapable to understand their **uncertainty**. These models are often taken too blindly and assumed to be accurate, which is not always the case.

In my opinion finding out and understanding uncertainty is crucial. So why isn't it a standard procedure? The main issue is that traditional machine learning approaches to understanding uncertainty, such as __[Gaussian processes](https://en.wikipedia.org/wiki/Gaussian_process)__, do not scale to high dimensional inputs. To effectively understand this kind of data, we need deep learning. But deep learning struggles to model uncertainty.

In this post I’m going to introduce a field known as Bayesian deep learning. Bayesian deep learning informs us about the uncertainty in its predictions. I think uncertainty is an underappreciated concept in Machine Learning as it's clearly important for real-world applications. But it could also be useful in training. For example, we could train the model specifically on samples it is most uncertain about. I’m going to explain the different types of uncertainty and show how to model them.

## Different types of uncertainties

Let's first go through uncertainty and understand the fundamental concept of it. There are different types of uncertainty and we need to understand which types are required for different applications. I’m going to discuss the two most important types – **Epistemic** and **Aleatoric** uncertainty.

### Epistemic uncertainty

Epistemic uncertainty captures our ignorance about which model generated our collected data. This uncertainty can be explained away given enough data, and is often referred to as model uncertainty. Example of this might be:

-  The __[drag](https://en.wikipedia.org/wiki/Drag_(physics))__ in an experiment designed to measure the acceleration of gravity near the earth's surface. The commonly used gravitational acceleration of 9.8 m/s^2 ignores the effects of air resistance, but the air resistance for the object could be measured and incorporated into the experiment to reduce the resulting uncertainty in the calculation of the gravitational acceleration.
   

## Aleatoric uncertainty

Aleatoric uncertainty is also known as statistical uncertainty, and is representative of unknowns that differ each time we run the same experiment. For example, aleatoric uncertainty in images can be attributed to occlusions (because cameras can’t see through objects) or lack of visual features or over-exposed regions of an image, etc. Example of this might be:

- Real-time applications, because we can form aleatoric models as a deterministic function of the input data, without expensive Monte Carlo sampling.

Next, I’m going to show how to form models to capture this uncertainty using Bayesian deep learning.

## Bayesian neural network

Data we're going to use in this example is the make_moons dataset from sklearn datasets. It's a simple binary classification problem that's not linearly separable.


```python
%matplotlib inline
import numpy as np
import matplotlib.pyplot as plt
import theano
import pymc3 as pm
import seaborn as sns

sns.set_style('white')
import sklearn
from sklearn import datasets
from sklearn.preprocessing import scale
from sklearn.model_selection import train_test_split
from sklearn.datasets import make_moons
```


```python
X, Y = make_moons(noise = 0.2, random_state = 0, n_samples = 1000)
X = scale(X)
X = X.astype(float)
Y = Y.astype(float)
X_train, X_test, Y_train, Y_test = train_test_split(X, Y, test_size=.5)
```


```python
fig, ax = plt.subplots(figsize = (12, 8))
ax.scatter(X[Y == 0, 0], X[Y == 0, 1], label = 'Class 0')
ax.scatter(X[Y == 1, 0], X[Y == 1, 1], color = 'r', label = 'Class 1')
sns.despine(); ax.legend()
ax.set(xlabel = 'X', ylabel = 'Y', title = 'Example dataset');
```

<div style="text-align:center" markdown="1">

![Differencing]({{ base_path }}/images/output_35_0.png)

</div>


## Model specification

Here we will use 2 hidden layers with 5 neurons each which is enough for such a simple problem. The Normal priors help regularize the weights.


```python
def construct_nn(ann_input, ann_output):
    n_hidden = 5
    
    # Initialize random weights between each layer
    init_1 = np.random.randn(X.shape[1], n_hidden).astype(float)
    init_2 = np.random.randn(n_hidden, n_hidden).astype(float)
    init_out = np.random.randn(n_hidden).astype(float)
        
    with pm.Model() as neural_network:
        # Weights from input to hidden layer
        weights_in_1 = pm.Normal('w_in_1', 0, sd = 1, 
                                 shape = (X.shape[1], n_hidden), 
                                 testval = init_1)
        
        # Weights from 1st to 2nd layer
        weights_1_2 = pm.Normal('w_1_2', 0, sd = 1, 
                                shape = (n_hidden, n_hidden), 
                                testval = init_2)
        
        # Weights from hidden layer to output
        weights_2_out = pm.Normal('w_2_out', 0, sd = 1, 
                                  shape = (n_hidden,), 
                                  testval = init_out)
        
        # Build neural-network using tanh activation function
        act_1 = pm.math.tanh(pm.math.dot(ann_input, 
                                         weights_in_1))
        act_2 = pm.math.tanh(pm.math.dot(act_1, 
                                         weights_1_2))
        act_out = pm.math.sigmoid(pm.math.dot(act_2, 
                                              weights_2_out))
        
        # Binary classification -> Bernoulli likelihood
        out = pm.Bernoulli('out', 
                           act_out,
                           observed = ann_output,
                           total_size = Y_train.shape[0]
                          )
    return neural_network


ann_input = theano.shared(X_train)
ann_output = theano.shared(Y_train)
neural_network = construct_nn(ann_input, ann_output)
```

## Variational Inference: Scaling model complexity

We will use ADVI variational inference. Note, that this is a mean-field approximation so we ignore correlations in the posterior.


```python
from pymc3.theanof import set_tt_rng, MRG_RandomStreams
set_tt_rng(MRG_RandomStreams(42))
```


```python
%%time

with neural_network:
    inference = pm.ADVI()
    approx = pm.fit(n=50000, method=inference)
```

    Average Loss = 120.37: 100%|██████████| 50000/50000 [01:04<00:00, 771.95it/s]
    Finished [100%]: Average Loss = 120.37


    CPU times: user 1min 42s, sys: 5.66 s, total: 1min 47s
    Wall time: 1min 12s


As samples are more convenient to work with, we can very quickly draw samples from the variational approximation using the sample method (this is just sampling from Normal distributions):


```python
trace = approx.sample(draws=5000)
```

Plotting the objective function **evidence lower bound (ELBO)** we can see that the optimization slowly improves the fit over time.


```python
plt.plot(-inference.hist, color = 'black')
plt.ylabel('ELBO')
plt.xlabel('Iteration');
```


<div style="text-align:center" markdown="1">

![Differencing]({{ base_path }}/images/output_20_0.png)

</div>


Now that we have trained the model, lets predict on the holdout set using a posterior predictive check.


```python
# Replace arrays our NN references with the test data
ann_input.set_value(X_test)
ann_output.set_value(Y_test)

with neural_network:
    ppc = pm.sample_posterior_predictive(trace, samples=500, progressbar=False)

# Use probability of > 0.5 to assume prediction of class 1
pred = ppc['out'].mean(axis=0) > 0.5
```

Predictions:


```python
fig, ax = plt.subplots()
ax.scatter(X_test[pred == 0, 0], X_test[pred == 0, 1])
ax.scatter(X_test[pred == 1, 0], X_test[pred == 1, 1], color = 'r')
sns.despine()
ax.set(title = 'Predicted labels (testing set)', xlabel = 'X', ylabel = 'Y');
```


<div style="text-align:center" markdown="1">

![Differencing]({{ base_path }}/images/output_24_0.png)

</div>



```python
print('Accuracy = {}%'.format((Y_test == pred).mean() * 100))
```

    Accuracy = 94.8%


## Lets look at what the classifier has learned

For this, we evaluate the class probability predictions on a grid over the whole input space.


```python
grid = pm.floatX(np.mgrid[-3:3:100j,-3:3:100j])
grid_2d = grid.reshape(2, -1).T
dummy_out = np.ones(grid.shape[1], dtype = np.int8)
```


```python
ann_input.set_value(grid_2d)
ann_output.set_value(dummy_out)

with neural_network:
    ppc = pm.sample_posterior_predictive(trace, samples = 500, progressbar = False)
```

## Probability surface


```python
cmap = sns.diverging_palette(250, 12, s = 85, l = 25, as_cmap = True)
fig, ax = plt.subplots(figsize = (14, 8))
contour = ax.contourf(grid[0], grid[1], ppc['out'].mean(axis = 0).reshape(100, 100), cmap = cmap)
ax.scatter(X_test[pred == 0, 0], X_test[pred == 0, 1])
ax.scatter(X_test[pred == 1, 0], X_test[pred == 1, 1], color = 'r')
cbar = plt.colorbar(contour, ax = ax)
_ = ax.set(xlim = (-3, 3), ylim = (-3, 3), xlabel = 'X', ylabel = 'Y');
cbar.ax.set_ylabel('Posterior predictive mean probability of class label = 0');
```


<div style="text-align:center" markdown="1">

![Differencing]({{ base_path }}/images/output_30_0.png)

</div>


## Uncertainty

Now let's get to the good stuff. So far, everything I showed we could have done with a non-Bayesian Neural Network. The mean of the posterior predictive for each class-label should be identical to maximum likelihood predicted values. However, we can also look at the standard deviation of the posterior predictive to get a sense for the uncertainty in our predictions. Here is what that looks like:


```python
cmap = sns.cubehelix_palette(light = 1, as_cmap = True)
fig, ax = plt.subplots(figsize = (14, 8))
contour = ax.contourf(grid[0], grid[1], ppc['out'].std(axis = 0).reshape(100, 100), cmap = cmap)
ax.scatter(X_test[pred == 0, 0], X_test[pred == 0, 1])
ax.scatter(X_test[pred == 1, 0], X_test[pred == 1, 1], color = 'r')
cbar = plt.colorbar(contour, ax = ax)
_ = ax.set(xlim = (-3, 3), ylim = (-3, 3), xlabel = 'X', ylabel = 'Y');
cbar.ax.set_ylabel('Uncertainty (posterior predictive standard deviation)');
```


<div style="text-align:center" markdown="1">

![Differencing]({{ base_path }}/images/output_32_0.png)

</div>


We can see that very close to the decision boundary, our uncertainty as to which label to predict is highest. You can imagine that associating predictions with uncertainty is a critical property for many applications like health care. To further maximize accuracy, we might want to train the model primarily on samples from that high-uncertainty region.

## Summary

This post explored the Bayesian way to construct and utilize deep learning methods. Altough the example was very simple, the main point i wanted to get through with this post was the concept of uncertainty. It is a crucial part and should be always considered when starting a new project in deep learning.
