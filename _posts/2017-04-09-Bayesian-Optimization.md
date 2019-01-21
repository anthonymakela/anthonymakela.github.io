---
title: "Bayesian Optimization"
excerpt: "Strategy for optimizing black-box functions. Generally, Bayesian optimization is useful when the function you want to optimize is not differentiable. As such, it is a natural candidate for hyperparameter tuning."
layout: single
author: "Anthony Makela"
date: "09 April 2017"
---



The process of fitting a single classifier isn't a long process but, fitting hundreds takes a while. To find the best hyperparameters you need to fit a lot of classifiers. Here we explore an way to achieve this.

This post explores the inner workings of an algorithm you can use to reduce the number of hyperparameter sets you need to try before finding the best set. The algorithm goes under the name of Bayesian optimisation.

Bayesian optimization is an approach to optimizing objective functions that take a long time (minutes or hours) to evaluate. It builds a surrogate for the objective
and quantifies the uncertainty in that surrogate using a Bayesian machine learning technique, Gaussian
process regression, and then uses an acquisition function defined from this surrogate to decide where to
sample


```python
from bayes_opt import BayesianOptimization
from bayes_opt import UtilityFunction
import numpy as np

import matplotlib.pyplot as plt
from matplotlib import gridspec

import seaborn as sns
sns.set_style('whitegrid')
sns.set_context("talk")
```


```python
%matplotlib inline
plt.rc("font", family="serif", size=17)
```

## Target function

One-dimensional function with multiple local maxima.

$$f(x) = e^{-(x - 2)^2} + e^{-\frac{(x - 6)^2}{10}} + \frac{1}{x^2 + 1}, $$

its maximum is at $x = 2$ and we will restrict the interval of interest to $x \in (-2, 10)$.

In practice, this function is unknown, the only information we have is obtained by sequentialy probing it at different points. Bayesian Optimization works by contructing a posterior distribution of functions that best fit the data observed and chosing the next probing point by balancing exploration and exploitation.


```python
def target(x):
    """
    Target function we want to find the maximum of
    """
    return np.exp(-(x - 2)**2) + np.exp(-(x - 6)**2/10) + 1/ (x**2 + 1)
```


```python
x = np.linspace(-2, 10, 10000).reshape(-1, 1)
y = target(x)

plt.figure(figsize=(20,10))
plt.plot(x, y, color = 'teal')
```




    [<matplotlib.lines.Line2D at 0x7fd1284116a0>]


<div style="text-align:center" markdown="1">

![Differencing]({{ base_path }}/images/output_5_1.png)

</div>



### Optimizer object

Enter the target function to be maximized, its variables and their corresponding ranges. A minimum number of 2 initial guesses is crucial to kick start the algorithms, these can either be random or user-defined.


```python
opt = BayesianOptimization(target, {'x': (-2, 10)}, random_state=27)
```


```python
opt.maximize(init_points=2, n_iter=0, kappa=5)
```

    |   iter    |  target   |     x     |
    -------------------------------------
    | [0m 1       [0m | [0m 0.8198  [0m | [0m 3.109   [0m |
    | [0m 2       [0m | [0m 0.746   [0m | [0m 7.775   [0m |
    =====================================



```python
def posterior(opt, x_obs, y_obs, grid):
    opt._gp.fit(x_obs, y_obs)

    mu, sigma = opt._gp.predict(grid, return_std=True)
    return mu, sigma


def plot_gp(opt, x, y):
    fig = plt.figure(figsize=(16, 10))
    steps = len(opt.space)
    fig.suptitle(
        'Gaussian Process and Utility Function After {} Steps'.format(steps)
    )
    
    gs = gridspec.GridSpec(2, 1, height_ratios=[3, 1]) 
    axis = plt.subplot(gs[0])
    acq = plt.subplot(gs[1])
    
    x_obs = np.array([[res["params"]["x"]] for res in opt.res])
    y_obs = np.array([res["target"] for res in opt.res])
    
    mu, sigma = posterior(opt, x_obs, y_obs, x)
    axis.plot(x, y, linewidth=3, label='Target function', color = 'teal')
    axis.plot(x_obs.flatten(), y_obs, 'D', markersize=8, label=u'Samples', color='black')
    axis.plot(x, mu, '--', color='k', label='Prediction')

    axis.fill(np.concatenate([x, x[::-1]]), 
              np.concatenate([mu - 1.9600 * sigma, (mu + 1.9600 * sigma)[::-1]]),
        alpha=.6, fc='skyblue', ec='None', label='95% confidence interval')
    
    axis.set_xlim((-2, 10))
    axis.set_ylim((None, None))
    axis.set_ylabel('f(x)', fontdict={'size':20})
    axis.set_xlabel('x', fontdict={'size':20})
    
    utility_function = UtilityFunction(kind="ucb", kappa=5, xi=0)
    utility = utility_function.utility(x, opt._gp, 0)
    acq.plot(x, utility, label='Utility Function', color='maroon')
    acq.plot(x[np.argmax(utility)], np.max(utility), '.', markersize=15, 
             label=u'Next Best Guess', markerfacecolor='black', markeredgecolor='k', markeredgewidth=1)
    acq.set_xlim((-2, 10))
    acq.set_ylim((0, np.max(utility) + 0.5))
    acq.set_ylabel('Utility', fontdict={'size':20})
    acq.set_xlabel('x', fontdict={'size':20})
    
    axis.legend(loc=2, bbox_to_anchor=(1.01, 1), borderaxespad=0.)
    acq.legend(loc=2, bbox_to_anchor=(1.01, 1), borderaxespad=0.)
```

## Random points

After we probe two points at random, we can fit a Gaussian Process and start the bayesian optimization procedure. Two points should give us a uneventful posterior with the uncertainty growing as we go further from the observations


```python
plot_gp(opt, x, y)
```

<div style="text-align:center" markdown="1">

![Differencing]({{ base_path }}/images/output_11_0.png)

</div>



The green line represents the true value of the target function as a function of our hypothetical hyper-parameter X. The black dots represent our two random points. The dashed line is our regression model trying to predict the value of the target function. Shaded area around the dashed line represents the 95% CI.

## Let's take one step 


```python
opt.maximize(init_points=0, n_iter=1, kappa=5)
plot_gp(opt, x, y)
```

    |   iter    |  target   |     x     |
    -------------------------------------
    | [0m 3       [0m | [0m 0.2017  [0m | [0m-2.0     [0m |
    =====================================

<div style="text-align:center" markdown="1">

![Differencing]({{ base_path }}/images/output_14_1.png)

</div>


## 10 iterations

Let's do 10 iterations here for the sake of not wasting time on plotting every single time we take a step.


```python
opt.maximize(init_points=0, n_iter=10, kappa=5)
plot_gp(opt, x, y)
```

    |   iter    |  target   |     x     |
    -------------------------------------
    | [0m 4       [0m | [0m 0.2118  [0m | [0m 10.0    [0m |
    | [95m 5       [0m | [95m 0.9898  [0m | [95m 5.327   [0m |
    | [95m 6       [0m | [95m 1.024   [0m | [95m 6.141   [0m |
    | [0m 7       [0m | [0m 0.9227  [0m | [0m 0.6438  [0m |
    | [95m 8       [0m | [95m 1.32    [0m | [95m 1.682   [0m |
    | [95m 9       [0m | [95m 1.367   [0m | [95m 2.203   [0m |
    | [0m 10      [0m | [0m 0.7036  [0m | [0m-0.6686  [0m |
    | [0m 11      [0m | [0m 0.4608  [0m | [0m 8.833   [0m |
    | [0m 12      [0m | [0m 0.827   [0m | [0m 4.403   [0m |
    | [95m 13      [0m | [95m 1.401   [0m | [95m 1.975   [0m |
    =====================================

<div style="text-align:center" markdown="1">

![Differencing]({{ base_path }}/images/output_16_1.png)

</div>


## Conclusions

After just a few points the algorithm was able to get pretty close to the true maximum. It is important to notice that the trade off between exploration (exploring the parameter space) and exploitation (probing points near the current known maximum) is fundamental to a succesful bayesian optimization procedure. The utility function being used here (Upper Confidence Bound - UCB) has a free parameter $\kappa$ that allows the user to make the algorithm more or less conservative. Additionally, a the larger the initial set of random points explored, the less likely the algorithm is to get stuck in local minima due to being too conservative.


```python

```
