
This post explores a powerful method with the general problem of optimization, an area where Bayesian statistics can have a big impact.

It is the year 2900, Elon Musk has lead humanity to become a space-faring civilization. Bayesians and Frequentists still argue about who's methods are more efficient. You are a Data Scientist at SpaceX, a company that sends humans to the moon and Mars. You are given a task to  manage the supply chain to keep the rockets running.


```python
import pandas as pd
import numpy as np
import pymc3 as pm
from scipy import stats
import seaborn as sns
import arviz as az
import matplotlib.pyplot as plt

sns.set_style("whitegrid")
sns.set_palette(sns.color_palette("Blues_d"))

%matplotlib inline
```

The rockets themselves are reusable, and we need a new rocket engine for every launch we have. There are three different suppliers from whom we can order the engines from. All of the suppliers have different prices, quality, and different maximum amounts they can ship to us within a specific timeframe. We know the prices and order sizes, but the true yield distribution is unobservable. Here, we include the unobservable parameters P_YIELD and P_YIELD_SD to simulate data, but we will assume we don't know them.


```python
P_YIELD = np.array([.9, .5, .8])
P_YIELD_SD = np.array([.1, .2, .2])
PRICES = [220.0, 100.0, 120.0]
MAX_ORDER_SIZE = [100, 80, 100]
```

The yield represents the percentage of engines that passes our stress tests. Due to different manufacturing techniques, the yield varies depending on the supplier, which is also reflected in the price. As we assume that we can't directly observe the true yield, we will have to estimate it from previous batches we ordered. Let's assume we have ordered different times from different suppliers. For example, as supplier 2 (third list item) only opened up recently, we only ordered twice from there:


```python
OBSERVATIONS = [30, 20, 2]
```


```python
np.random.seed(100)
data = []
for p_yield, p_yield_sd, observations in zip(P_YIELD, P_YIELD_SD, OBSERVATIONS):
    data.append(pm.Beta.dist(mu = p_yield, sd = p_yield_sd, shape = observations).random())
```


```python
df = pd.DataFrame(data).T
tidy = df.unstack().to_frame('yield')
tidy.index = tidy.index.set_names(['supplier', 'obs'])
g = sns.FacetGrid(data = tidy.reset_index().dropna(), col = 'supplier')
g.map(sns.distplot, 'yield', kde = False);
```


![png](/images/output_8_0.png)


This is the data we have in our use to estimate the true yield of every one of the suppliers.

In order to find out how many engines we need, we first need to know how many launches we can sell. If we buy too few we are leaving money on the table and if we buy too many we will have to hold them in a storage which costs money (HOLD_COST). Let's assume we can sell a rocket for 500 bitcoins (BTC) and it costs us 100 BTC in holding cost.


```python
SALES_PRICE = 500 # BTC
HOLD_COST = 100 # BTC
```

## Loss function

Let's define our loss function which takes as inputs how many engines we currently have in stock, how many launches our customers want, what was price that we bought the engine, at what price we can sell the launch, and what the holding costs are per engine:


```python
@np.vectorize
def loss(in_stock, demand, buy_price, sales_price = SALES_PRICE, holding_cost = HOLD_COST):
    # How much do we make per launch(Margin)
    margin = sales_price - buy_price
    
    if in_stock > demand:
        total_profit = demand * margin
        # Everything left over after the demand was met, goes into holding
        total_holding_cost = (in_stock - demand) * holding_cost
        reward = total_profit - total_holding_cost
    else:
        # We can only sell what we have in stock, no storage required
        reward = in_stock * margin
    
    # We need to invert in the case of minimizing
    return -reward
```


```python
in_stock = np.arange(0, 100)
plt.scatter(in_stock, -loss(in_stock, 50, 50), marker = "|"); plt.axvline(50, c = 'k', ls = '-', label = 'Assumed demand');
plt.xlabel('In stock'); plt.ylabel('Profit (neg loss)'); sns.despine(); plt.legend();
```


![png](/images/output_14_0.png)


We can observe that, if the customer demand is 50 launches, we maximize our profit if we have 50 engines in stock. Having fewer engines eats our profits at a greater rate than ordering excess engines because in this setup our margins are larger than the holding cost.

Next, we need our estimate of demand. As we have a history of launches we have a pretty solid idea of what the distribution looks like, but we will also assume that we don't know the true underlying parameters and only have access to the samples:


```python
demand_est = stats.poisson(60, 40).rvs(1000)
sns.distplot(demand_est);
```


![png](/images/output_17_0.png)


We can evaluate our objective function over every demand we observed historically (setting engines in stock to 100):


```python
plt.scatter(demand_est, -loss(in_stock = 100, demand = demand_est, buy_price = 10),  marker = "|")
plt.xlabel('Demand'); plt.ylabel('Profit (neg loss)'); plt.axvline(100, c = 'k', ls = '-', label = 'Assumed in stock');
plt.legend();
```


![png](/images/output_19_0.png)


In response to demand, the loss-function behaves differently. With less demand than what we have in stock, we earn less (because we sell less launches, but also have to pay the holding costs), but we can observe that when demand exceeds the number of engines we have in stock our profit stays flat because we can't sell more than what we have.

## Bayesian model

We will use PyMC3000 to build a model to estimate the yield of every engine supplier:


```python
with pm.Model() as model:
    # Priors on alpha and beta params for each supplier
    α = pm.HalfNormal('α', sd = 10., shape = 3)
    β = pm.HalfNormal('β', sd = 10., shape = 3)
    
    # Different likelihood for every supplier because we have different n of data points
    for i, d in enumerate(data):
        pm.Beta(f'p_yield_obs_{i}', 
            alpha = α[i], beta = β[i],
            observed = d)
    
    trace = pm.sample()
```

    Auto-assigning NUTS sampler...
    Initializing NUTS using jitter+adapt_diag...
    Multiprocess sampling (2 chains in 2 jobs)
    NUTS: [β, α]
    Sampling 2 chains: 100%|██████████| 2000/2000 [00:03<00:00, 573.50draws/s]



```python
# Convergence
az.plot_energy(trace);
```


![png](/images/output_23_0.png)


## Possible future scenarios

In order to make good assumptions and decision making with Bayesian Statistics, we need an estimate of what the future might look like. As we are in a generative framework this is trivial: we just need to sample from the posterior predictive distribution of our model which generates new data based on our estimated posteriors.


```python
with model:
    posterior_pred = pm.sample_posterior_predictive(trace, 1000)
```

    100%|██████████| 1000/1000 [00:02<00:00, 449.37it/s]



```python
p_yield_post_pred = pd.DataFrame({k: v[:, 1] for k, v in posterior_pred.items()})
tidy = p_yield_post_pred.unstack().to_frame('yield')
tidy.index = tidy.index.set_names(['supplier', 'obs'])
g = sns.FacetGrid(data = tidy.reset_index().dropna(), col = 'supplier')
g.map(sns.distplot, 'yield', kde = False);
```


![png](/images/output_26_0.png)


This plot shows, given the data and our model, what we can expect to observe. Note that these predictions take the uncertainty into account. For supplier 2 we have a lot of uncertainty because we only had very few data points.

Given these estimates we can write a function that converts the orders we place to each supplier, the yield we assume for each one, and what their prices are.


```python
def yield_and_price(orders, 
                         p_yield = np.array([.9, .5, .8]),
                         prices = PRICES
                        ):
    orders = np.asarray(orders)
    
    full_yield = np.sum(p_yield * orders)
    price_per_item = np.sum(orders * prices) / np.sum(orders)
    
    return full_yield, price_per_item

yield_and_price([100, 60, 60])
```




    (168.0, 160.0)



So given these (randomly picked) order amounts to each supplier and some deterministic yield, we would receive 168 functioning engines at an effective price of 160 BTC each.

##  Decision Making & Optimization

Now we have to actually do the optimization. First, we need to specify our objective function which will compute the total yield and effective price given a posterior predictive sample. Once we have that and our demand (also a sample from that distribution), we can compute our loss. As we have a distribution over possible scenarios, we compute the loss for each one and return the distribution.


```python
def objective(orders, p_yield = p_yield_post_pred,
              demand_est = demand_est, max_order_size = MAX_ORDER_SIZE):
    orders = np.asarray(orders)
    losses = []
    
    # Negative orders are impossible
    if np.any(orders < 0):
        return np.inf
    # Also ordering more than the supplier can ship is also impossible
    if np.any(orders > MAX_ORDER_SIZE):
        return np.inf
    
    for i, p_yield_sample in p_yield.iterrows():
        full_yield, price_per_item = yield_and_price(
            orders,
            p_yield = p_yield_sample
        )
        
        # Evaluate loss over each sample with one sample from the demand distribution
        loss_i = loss(full_yield, demand_est[i], price_per_item)
        
        losses.append(loss_i)
        
    return np.asarray(losses)
```

Let's run the optimization and see what will the results look like


```python
from scipy import optimize
```


```python
# Parameters for optimization
bounds = [(0, max_order) for max_order in MAX_ORDER_SIZE]
starting_value = [50., 50., 50.]
```


```python
opt_stoch = optimize.minimize(lambda *args: np.mean(objective(*args)), 
                                                      starting_value, 
                                                      bounds = bounds)
```


```python
print('Optimal order amount from the suppliers = {}'.format(np.ceil(opt_stoch.x)))
```

    Optimal order amount from the suppliers = [ 0. 80. 92.]



```python
print('Total order amount from all suppliers = {}'.format(np.ceil(np.sum(opt_stoch.x))))
```

    Total order amount from all suppliers = 172.0


Great, we did it! Excitedly you go to Musk and tell him about the amazing model you built and the optimal order amounts. Unfortunately, he is not impressed and asks "that's some fancy technique, but I'm not convinced this is actually better than what we currently use which is to just take the means of the yield distribution for each supplier."

## Evaluation

Slightly discouraged you go back to your desk and wonder why life is so unfair and you actually have to prove that things work and why "but it's Bayesian!" is not as convincing an argument as you hoped for. After some deep reflection you come to the conclusion that Musk might have a point and that additional complexity must be warranted and demonstrably better. To build a more compelling case, you decide to compare the naive method of just using the means to your fancy method in terms of expected profit in a simulation study.

Instead of samples from the posterior predictive, we can just pass a single sample -- the mean -- into our objective function.


```python
p_yield_mean = pd.DataFrame([np.mean(d) for d in data]).T
p_yield_mean
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.918735</td>
      <td>0.558903</td>
      <td>0.896244</td>
    </tr>
  </tbody>
</table>
</div>



As well as the demand we expect on average (100). This way we can still use the above objective function but the loop will just run once.


```python
opt_non_stoch = optimize.minimize(lambda *args: objective(*args, 
                                                          p_yield = p_yield_mean, 
                                                          demand_est = [100]),
                                                          starting_value, 
                                                          bounds = bounds)
```


```python
print('Optimal order amount from every supplier = {}'.format(np.ceil(opt_non_stoch.x)))
```

    Optimal order amount from every supplier = [42. 46. 42.]



```python
print('Total order amount from all suppliers = {}'.format(np.ceil(np.sum(opt_non_stoch.x))))
```

    Total order amount from all suppliers = 128.0


The results are certainly different. The full Bayesian treatment seems to dislike our high-cost but high-quality supplier. It also orders more in total (probably to account for the lower yield of the other two suppliers). But which one is actually better in terms of our profit?

To answer that question, we will generate new data from our true generative model and compute the profit in each new scenario given the order amounts from the two optimizations.


```python
np.random.seed(123)
new_data = []
for p_yield, p_yield_sd, observations in zip(P_YIELD, P_YIELD_SD, OBSERVATIONS):
    new_data.append(pm.Beta.dist(mu = p_yield, sd = p_yield_sd, shape = 1000).random())
new_data = pd.DataFrame(new_data).T
new_data.head().add_prefix("Supplier ")
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Supplier 0</th>
      <th>Supplier 1</th>
      <th>Supplier 2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.880298</td>
      <td>0.752686</td>
      <td>0.997934</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.698046</td>
      <td>0.307304</td>
      <td>0.971085</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.676807</td>
      <td>0.534287</td>
      <td>0.891209</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0.943773</td>
      <td>0.666368</td>
      <td>0.975907</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.911538</td>
      <td>0.457898</td>
      <td>0.556483</td>
    </tr>
  </tbody>
</table>
</div>




```python
neg_loss_stoch = -objective(opt_stoch.x, p_yield = new_data) / demand_est
neg_loss_non_stoch = -objective(opt_non_stoch.x, p_yield = new_data) / demand_est
sns.distplot(neg_loss_stoch, label = 'Stochastic', kde = False)
plt.axvline(np.mean(neg_loss_stoch), label = 'Expected stochastic')
sns.distplot(neg_loss_non_stoch, label = 'Non-stochastic', kde = False)
plt.axvline(np.mean(neg_loss_non_stoch), color = 'Orange', label = 'Expected non-stochastic')
plt.legend(); plt.xlabel('Profit (negative loss)'); plt.ylabel('Occurances');
```


![png](/images/output_49_0.png)



```python
print('Expected profit of Bayesian model = %.2f BTC' % np.mean(neg_loss_stoch))
```

    Expected profit of Bayesian model = 349.98 BTC



```python
print('Expected profit of naive model = %.2f BTC' % np.mean(neg_loss_non_stoch))
```

    Expected profit of naive model = 317.01 BTC


Musk is very pleased that you finally spoke his language and demonstrated an expected 10% increase in profit, which translates to millions of additional profit over a year at the scale the spaceport operates on. For your demonstrated ability to understand business requirements you get promoted to Chief Bayesian Officer.

## Summary

As you can see, once we have a Bayesian model and an objective function we can apply Bayesian Decision Theory to make better decisions. Why better? While there is a mathematical proof that shows this to be optimal, there are also more practical and intuitive reasons. The first major reason is that we do not just optimize over the most likely future scenario, but all possible future scenarios.
