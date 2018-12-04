---
title: "Analysing the Factors that Influence Cryptocurrency Prices with Cryptory"
excerpt: "Announcing my new Python package with a look at the forces involved in cryptocurrency prices"
layout: single
header:
  overlay_image: moonshot.jpg
  overlay_filter: 0.4
  caption: "Factors not considered: moon cycle"
categories:
  - data science
  - python
tags:
  - cryptos
  - cryptory
  - analysis
author: "David Sheehan"
date: "11 February 2018"
---

You may have seen [my previous post](https://dashee87.github.io/deep%20learning/python/predicting-cryptocurrency-prices-with-deep-learning/) that tried to predict bitcoin and ethereum prices with deep learning. To summarise, there was alot of hype but it wasn't very useful in practice (I'm referring to the model, of course). To improve the model, we have two options: carefully design an intricately more sophisticated model (i.e. [throw shit tons more layers in there](https://dashee87.github.io/data%20science/deep%20learning/python/another-keras-tutorial-for-neural-network-beginners/)) or identify more informative data sources that can be fed into the model. While it's tempting to focus on the former, the garbage-in-garbage-out principle remains. 

With that in mind, I created a new Python package called [cryptory](https://github.com/dashee87/cryptory). Not to be confused with the [obscure Go repo](https://github.com/mtamer/cryptory) (damn you, mtamer) or [that bitcoin scam](https://www.reddit.com/r/Scams/comments/2ao4aw/cryptorycom_scam_alert_stay_away/?st=jd3c7q9a&sh=9af44946) (you try to come up with a crypto package name that isn't associated with some scam), it integrates various packages and protocols so that you can get historical crypto (just daily... for now) and wider economic/social data in one place. Rather than making more crypto based jokes, I should probably just explain the package.

As always, the full code for this post can found on my [GitHub account](https://github.com/dashee87/blogScripts/blob/master/Jupyter/2018-02-11-analysing-the-factors-that-influence-cryptocurrency-prices-with-cryptory.ipynb).

## Installation

`cryptory` is available on [PyPi](https://pypi.python.org/pypi/cryptory/0.1.0) and [GitHub](https://github.com/dashee87/cryptory), so installing it is as easy as running `pip install cryptory` in your command line/shell.

<div style="text-align:center" markdown="1">

![]({{ base_path }}/images/install_cryptory.png)

</div>

It relies on pandas, numpy, BeautifulSoup and [pytrends](https://github.com/GeneralMills/pytrends), but, if necesssary, these packages should be automatically installed alongisde cryptory.

The next step is to load the package into the working environment. Specifically, we'll import the `Cryptory` class.


```python
# import package
from cryptory import Cryptory
```

Assuming that returned no errors, you're now ready to starting pulling some data. But before we do that, it's worth mentioning that you can retrieve information about each method by running the `help` function.


```python
help(Cryptory)
```

    Help on class Cryptory in module cryptory.cryptory:
    
    class Cryptory
     |  Methods defined here:
     |  
     |  __init__(self, from_date, to_date=None, ascending=False, fillgaps=True, timeout=10.0)
     |      Initialise cryptory class
     ...
    


We'll now create our own cryptory object, which we'll call `my_cryptory`. You need to define the start date of the data you want to retrieve, while there's also some optional arguments. For example, you can set the end date, otherwise it defaults to the current date- see `help(Cryptory.__init__)` for more information).


```python
# initialise object
my_cryptory = Cryptory(from_date="2017-01-01")
```

### Cryptocurrency Prices

We'll start by getting some historical bitcoin prices (starting from 1st Jan 2017). `cryptory` has a few options for this type of data, which I will now demonstrate.


```python
# get prices from coinmarketcap
my_cryptory.extract_coinmarketcap("bitcoin")
```




<div>
<style>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: left;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: middle;">
      <th></th>
      <th>date</th>
      <th>open</th>
      <th>high</th>
      <th>low</th>
      <th>close</th>
      <th>volume</th>
      <th>market cap</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2018-02-10</td>
      <td>8720.08</td>
      <td>9122.55</td>
      <td>8295.47</td>
      <td>8621.90</td>
      <td>7780960000</td>
      <td>146981000000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2018-02-09</td>
      <td>8271.84</td>
      <td>8736.98</td>
      <td>7884.71</td>
      <td>8736.98</td>
      <td>6784820000</td>
      <td>139412000000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2018-02-08</td>
      <td>7637.86</td>
      <td>8558.77</td>
      <td>7637.86</td>
      <td>8265.59</td>
      <td>9346750000</td>
      <td>128714000000</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>403</th>
      <td>2017-01-03</td>
      <td>1021.60</td>
      <td>1044.08</td>
      <td>1021.60</td>
      <td>1043.84</td>
      <td>185168000</td>
      <td>16426600000</td>
    </tr>
    <tr>
      <th>404</th>
      <td>2017-01-02</td>
      <td>998.62</td>
      <td>1031.39</td>
      <td>996.70</td>
      <td>1021.75</td>
      <td>222185000</td>
      <td>16055100000</td>
    </tr>
    <tr>
      <th>405</th>
      <td>2017-01-01</td>
      <td>963.66</td>
      <td>1003.08</td>
      <td>958.70</td>
      <td>998.33</td>
      <td>147775000</td>
      <td>15491200000</td>
    </tr>
  </tbody>
</table>
</div>




```python
# get prices from bitinfocharts
my_cryptory.extract_bitinfocharts("btc")
```




<div>
<table border="1" class="dataframe" style="width:50%">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>date</th>
      <th>btc_price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2018-02-10</td>
      <td>8691.000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2018-02-09</td>
      <td>8300.000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2018-02-08</td>
      <td>8256.000</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>403</th>
      <td>2017-01-03</td>
      <td>1017.000</td>
    </tr>
    <tr>
      <th>404</th>
      <td>2017-01-02</td>
      <td>1010.000</td>
    </tr>
    <tr>
      <th>405</th>
      <td>2017-01-01</td>
      <td>970.988</td>
    </tr>
  </tbody>
</table>
</div>



Those cells illustrate how to pull bitcoin prices from coinmarketcap and bitinfocharts. The discrepancy in prices returned by each can be explained by their different approaches to calculate daily prices (e.g. bitinfocharts represents the average prices across that day). For that reason, I wouldn't recommend combining different price sources.

You also pull non-price specific data with `extract_bitinfocharts` e.g. transactions fees. See `help(Cryptory.extract_bitinfocharts)` for more information.


```python
# average daily eth transaction fee
my_cryptory.extract_bitinfocharts("eth", metric='transactionfees')
```




<div>
<table border="1" class="dataframe" style="width:50%">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>date</th>
      <th>eth_transactionfees</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2018-02-10</td>
      <td>0.78300</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2018-02-09</td>
      <td>0.74000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2018-02-08</td>
      <td>0.78300</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>403</th>
      <td>2017-01-03</td>
      <td>0.00773</td>
    </tr>
    <tr>
      <th>404</th>
      <td>2017-01-02</td>
      <td>0.00580</td>
    </tr>
    <tr>
      <th>405</th>
      <td>2017-01-01</td>
      <td>0.00537</td>
    </tr>
  </tbody>
</table>
</div>



You may have noticed that each method returns a pandas dataframe. In fact, all `cryptory` methods return a pandas dataframe. This is convenient, as it allows you to slice and dice the output using common pandas techniques. For example, we can easily merge two `extract_bitinfocharts` calls to combine daily bitcoin and ethereum prices.


```python
my_cryptory.extract_bitinfocharts("btc").merge(
my_cryptory.extract_bitinfocharts("eth"), on='date', how='inner')
```




<div>
<table border="1" class="dataframe" style="width:50%">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>date</th>
      <th>btc_price</th>
      <th>eth_price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2018-02-10</td>
      <td>8691.000</td>
      <td>871.238</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2018-02-09</td>
      <td>8300.000</td>
      <td>832.564</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2018-02-08</td>
      <td>8256.000</td>
      <td>814.922</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>403</th>
      <td>2017-01-03</td>
      <td>1017.000</td>
      <td>8.811</td>
    </tr>
    <tr>
      <th>404</th>
      <td>2017-01-02</td>
      <td>1010.000</td>
      <td>8.182</td>
    </tr>
    <tr>
      <th>405</th>
      <td>2017-01-01</td>
      <td>970.988</td>
      <td>8.233</td>
    </tr>
  </tbody>
</table>
</div>



One further source of crypto prices is offered by `extract_poloniex`, which pulls data from the [public poloniex API](https://poloniex.com/support/api/). For example, we can retrieve the BTC/ETH exchange rate.


```python
# btc/eth price
my_cryptory.extract_poloniex(coin1="btc", coin2="eth")
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>date</th>
      <th>close</th>
      <th>open</th>
      <th>high</th>
      <th>low</th>
      <th>weightedAverage</th>
      <th>quoteVolume</th>
      <th>volume</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2018-02-10</td>
      <td>0.099700</td>
      <td>0.100961</td>
      <td>0.101308</td>
      <td>0.098791</td>
      <td>0.100194</td>
      <td>2.160824e+04</td>
      <td>2165.006520</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2018-02-09</td>
      <td>0.101173</td>
      <td>0.098898</td>
      <td>0.101603</td>
      <td>0.098682</td>
      <td>0.100488</td>
      <td>2.393343e+04</td>
      <td>2405.019824</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2018-02-08</td>
      <td>0.098896</td>
      <td>0.099224</td>
      <td>0.101196</td>
      <td>0.096295</td>
      <td>0.098194</td>
      <td>2.250954e+04</td>
      <td>2210.293015</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>403</th>
      <td>2017-01-03</td>
      <td>0.009280</td>
      <td>0.008218</td>
      <td>0.009750</td>
      <td>0.008033</td>
      <td>0.009084</td>
      <td>1.376059e+06</td>
      <td>12499.794908</td>
    </tr>
    <tr>
      <th>404</th>
      <td>2017-01-02</td>
      <td>0.008220</td>
      <td>0.008199</td>
      <td>0.008434</td>
      <td>0.007823</td>
      <td>0.008101</td>
      <td>6.372636e+05</td>
      <td>5162.784640</td>
    </tr>
    <tr>
      <th>405</th>
      <td>2017-01-01</td>
      <td>0.008200</td>
      <td>0.008335</td>
      <td>0.008931</td>
      <td>0.008001</td>
      <td>0.008471</td>
      <td>7.046517e+05</td>
      <td>5968.975870</td>
    </tr>
  </tbody>
</table>
</div>



We're now in a position to perform some basic analysis of cryptocurrencies prices.

<div style="text-align:center" markdown="1">

![]({{ base_path }}/images/crypto_price_2017.png)

</div>


Of course, that graph is meaningless. You can't just compare the price for single units of each coin. You need to consider the total supply and the market cap. It's like saying the dollar is undervalued compared to the Japanese Yen. But I probably shouldn't worry. It's not as if people are [buying cryptos based on them being superficially cheap](https://www.youtube.com/watch?v=SvMF10ZXVoQ). More relevant here is the relative change in price since the start of 2017, which we can plot quite easily with a little pandas magic ([pct_change](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.Series.pct_change.html)).

<div style="text-align:center" markdown="1">

![]({{ base_path }}/images/crypto_price_2017_norm.png)

</div>

Those coins are provided on [bitinfocharts](https://bitinfocharts.com/comparison/bitcoin-price.html) and they tend to represent older legacy coins. For example, the coin from this list that performed best over 2017 was Reddcoin. It started 2017 with a market cap of less than 1 million dollars, but finished it with a value of around $250m, reaching a peak of over 750m in early Jan 2018. You'll notice that each coin shows the same general behaviour- a sustained rise between March and June, followed by another spike in December and a noticeable sell-off in Jan 2018. 

With a little help from pandas, we can produce a crypto price correlation plot (use the dropdown menu to switch between [Pearson](https://en.wikipedia.org/wiki/Pearson_correlation_coefficient) and [Spearman](https://en.wikipedia.org/wiki/Spearman%27s_rank_correlation_coefficient) correlation).

<div>
<select id="corr_choice_price" style="font-size:0.8em">
  <option value="pearson">Pearson</option>
  <option value="spearman">Spearman</option>
</select>
</div>
<div class="result_img" style="text-align:center">
<img id="price_picture" src="https://github.com/dashee87/dashee87.github.io/raw/master/images/crypto_price_correlation.png" alt="result.png" />
</div>
<div><br></div>
 
<script type="text/javascript">
$("#corr_choice_price").change(function () {
   menu_val = $(this).val();
    if (menu_val=="pearson") {
        $('#price_picture').attr('src', 'https://github.com/dashee87/dashee87.github.io/raw/master/images/crypto_price_correlation.png');
    } else {
        $('#price_picture').attr('src', 'https://github.com/dashee87/dashee87.github.io/raw/master/images/crypto_price_correlation_spear.png');
    }
});
</script>



There's nothing too surprising ([or novel](https://blog.patricktriest.com/analyzing-cryptocurrencies-python/)) here. It's well known that cryptos are heavily correlated- they tend to [spike](https://imgur.com/a/UBQaw#KLDWEIG) and [crash](https://www.reddit.com/r/CryptoCurrency/comments/7it7zi/93_of_the_top_100_cryptos_are_down_today_most_of/?st=jd5sd4p0&sh=cea8d0f0) collectively. There's a few reasons for this: Most importantly, the vast majority of coins can only be exchanged with the few big coins (e.g. btc and eth). As they are priced relative to these big coins, a change in btc or eth will also change the value of those smaller coins. Secondly, it's not like the stock market. Ethereum and Bitcoin are not as different as, say, Facebook and General Motors. While stock prices are linked to hitting financial targets (i.e. quarterly earnings reports) and wider macroeconomic factors, most cryptos (maybe all) are currently powered by hope and aspirations (well, hype and speculation) around blockchain technology. That's not to say coins can't occasionally buck the market e.g. ripple (xrp) in early December. However, overperformance is often followed by market underperformance (e.g. ripple in January 2018).

I'll admit nothing I've presented so far is particularly ground breaking. You could get similar data from the [Quandl api](https://www.quandl.com/tools/python) (aside: I intend to integrate quandl API calls into `cryptory`). The real benefit of `cryptory` comes when you want to combine crypto prices with other data sources.

### Reddit Metrics

If you're familiar with cryptos, you're very likely to be aware of their associated reddit pages. It's where crypto investors come to discuss the merits of different blockchain implementations, dissect the day's main talking points and post amusing gifs- okay, [it's mostly just GIFs](https://www.reddit.com/r/Bitcoin/comments/7v438b/the_last_3_months_in_47_seconds/). With `cryptory` you can combine reddit metrics (total number of subscribers, new subscribers, rank -literally scraped from the [redditmetrics website](http://redditmetrics.com/)) and other crypto data.

Let's take a look at iota and eos; two coins that emerged in June 2017 and experienced strong growth towards the end of 2017. Their corresponding subreddits are [r/iota](https://www.reddit.com/r/Iota/) and [r/eos](https://www.reddit.com/r/eos/), respectively.


```python
my_cryptory.extract_reddit_metrics("iota", "subscriber-growth")
```




<div>
<table border="1" class="dataframe" style="width:50%">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>date</th>
      <th>subscriber_growth</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2018-02-10</td>
      <td>150</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2018-02-09</td>
      <td>161</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2018-02-08</td>
      <td>127</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>404</th>
      <td>2017-01-03</td>
      <td>0</td>
    </tr>
    <tr>
      <th>405</th>
      <td>2017-01-02</td>
      <td>0</td>
    </tr>
    <tr>
      <th>406</th>
      <td>2017-01-01</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>





Now we can investigate the relationship between price and subreddit growth.


<div style="text-align:center" markdown="1">

![]({{ base_path }}/images/crypto_reddit_price.png)

</div>


Visually speaking, there's clearly some correlation between price and subreddit member growth (the y-axis was normalised using the conventional [min-max scaling](https://stats.stackexchange.com/questions/70801/how-to-normalize-data-to-0-1-range)). While the Spearman rank correlation is similarly high for both coins, the Pearson correlation coefficient is significantly stronger for iota, highlighting the importance of not relying on one single measure. At the time of writing, iota and eos both had a marketcap of about \$5bn (11th and 9th  overall), though the number of subscribers to the iota subreddit was over 3 times more than the eos subreddit (105k and 30k, respectively). While this doesn't establish whether the relationship between price and reddit is predictive or reactive, it does suggest that reddit metrics could be useful model features for some coins.

### Google Trends

You'll notice an almost simultaneous spike in suscribers to the iota and eos subreddits in late November and early December. This was part of a wider crypto trend, where most coins experienced unprecendented gains. Leading the charge was Bitcoin, which tripled in price between November 15th and December 15th. As the most well known crypto to nocoiners, Bitcoin (and the wider blockchain industry) received considerable [mainstream attention](https://www.theguardian.com/business/live/2017/dec/07/pound-sterling-ftse-brexit-bitcoin-economics-business-live) during this bull run. Presumably, this attracted quite alot of new crypto investors (i.e [gamblers](https://www.cnbc.com/2017/12/11/people-are-taking-out-mortgages-to-buy-bitcoin-says-joseph-borg.html)), which propelled the price even higher. Well, what's the first thing you're [gonna do](https://www.youtube.com/watch?v=tpD00Q4N6Jk) after [reading an article about this fancy futuristic blockchain that's making people rich](https://www.nytimes.com/2018/01/13/style/bitcoin-millionaires.html)?. You'd google bitcoin, ethereum and obviously [bitconnect](https://www.youtube.com/watch?v=21kGmCsJ5ZM).

With `cryptory`, you can easily combine conventional crypto metrics with [Google Trends](https://trends.google.com/trends/) data. You just need to decide the terms you want to search. It's basically a small wrapper on top of the [pytrends](https://github.com/GeneralMills/pytrends) package. If you've used [Google Trends](https://trends.google.com/trends/) before, you'll be aware that you can only retrieve daily scores for max 90 day periods. The `get_google_trends` method stitches together overlapping searches, so that you can pull daily scores going back years. It's probably best to illustrate it with a few examples.


```python
my_cryptory.get_google_trends(kw_list=['bitcoin'])
```




<div>
<table border="1" class="dataframe" style="width:50%">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>date</th>
      <th>bitcoin</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2018-02-09</td>
      <td>22.000000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2018-02-08</td>
      <td>25.000000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2018-02-07</td>
      <td>30.000000</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>402</th>
      <td>2017-01-03</td>
      <td>3.974689</td>
    </tr>
    <tr>
      <th>403</th>
      <td>2017-01-02</td>
      <td>4.377918</td>
    </tr>
    <tr>
      <th>404</th>
      <td>2017-01-01</td>
      <td>2.707397</td>
    </tr>
  </tbody>
</table>
</div>



Now we can investigate the relationship between crypto price and google search popularity.



<div style="text-align:center" markdown="1">

![]({{ base_path }}/images/google_reddit_price.png)

</div>


As before, it's visually obvious and statisically clear that there's a strong correlation between google searches and coin prices. Again, this a well known observation ([here](http://uk.businessinsider.com/bitcoin-price-correlation-google-search-2017-9), [here](https://www.express.co.uk/finance/city/911979/Cryptocurrency-Google-search-bitcoin-boom-ethereum-price-warning-boost) and [here](https://www.reddit.com/r/dataisbeautiful/duplicates/7ldxy7/2017_bitcoin_value_versus_google_search_interest/)). What's not so apparent is whether google search drives or follows the price. That chicken and egg question question will be addressed in my next deep learning post. 

A few words on Verge (xvg): eccentric (i.e. [crazy](http://uk.businessinsider.com/the-crazy-life-of-john-mcafee)) crypto visionary [John McAfee](https://twitter.com/officialmcafee?ref_src=twsrc%5Egoogle%7Ctwcamp%5Eserp%7Ctwgr%5Eauthor) [recommended](https://twitter.com/officialmcafee/status/941003398215761922?lang=en) (i.e. [shilled](https://twitter.com/officialmcafee/status/946052577539579906)) the unheralded Verge to his twitter followers (i.e. fools), which triggered a huge surge in its price. As is usually the case with pump and dumps, the pump (from which [McAfee himself potentially profitted](https://www.financemagnates.com/cryptocurrency/news/john-mcafee-pumping-cryptocurrencies-cash/)) was followed by the dump. The sorry story is retold in both the price and google search popularity. Unlike bitcoin and ethereum though, you'd need to consider in your analysis that verge is also a common search term for popular online technology news site [The Verge](https://www.theverge.com/) ([tron](https://en.wikipedia.org/wiki/Tron) would be a similar case). 

Anyway, back to `cryptory`, you can supply more than one keyword at a time, allowing you to visualise the relative popularity of different terms. Let's go back to the early days and compare the historical popularity of Kim Kardashian and Bitcoin since 2013.


<div style="text-align:center" markdown="1">

![]({{ base_path }}/images/kim_k_bitcoin.png)

</div>


According to Google Trends, bitcoin became a more popular search term in June 2017 (a sure sign of a bubble if ever there was one- [just realised this isn't a unique insight either](http://uk.businessinsider.com/bitcoin-passes-beyonc-taylor-swift-and-kim-kardashians-popularity-2017-12?r=US&IR=T)). That said, Bitcoin has never reached the heights of Kim Kardashian on the 13th November 2014 (obviously, the day [Kim Kardashian broke the internet](https://www.theguardian.com/lifeandstyle/2014/dec/17/kim-kardashian-butt-break-the-internet-paper-magazine)).  The graph shows daily values, but you'll notice that it quite closely matches what you'd get for [the same weekly search on the Google Trends website](https://trends.google.com/trends/explore?date=2013-01-01%202018-02-03&q=kim%20kardashian,bitcoin).

While social metrics like reddit and google popularity can be powerful tools to study cryptocurrency prices, you may also want to incorporate data related to finance and the wider global economy.

### Stock Market Prices

With their market caps and closing prices, cryptocurrencies somewhat resemble traditional company stocks. Of course, the major difference is that you couldn't possibly pay for a lambo by investing in the stock market. Still, looking at the stock market may provide clues as to how the general economy is performing, or even how specific industries are responding to the blockchain revolution.

`cryptory` includes a `get_stock_prices` method, which scrapes yahoo finance and returns historical daily data. Just note that you'll need to find the relevant company/index code on the yahoo finance website.


```python
# %5EDJI = Dow Jones
my_cryptory.get_stock_prices("%5EDJI")
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>date</th>
      <th>adjclose</th>
      <th>close</th>
      <th>high</th>
      <th>low</th>
      <th>open</th>
      <th>volume</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2018-02-10</td>
      <td>24190.900391</td>
      <td>24190.900391</td>
      <td>24382.140625</td>
      <td>23360.289062</td>
      <td>23992.669922</td>
      <td>735030000.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2018-02-09</td>
      <td>24190.900391</td>
      <td>24190.900391</td>
      <td>24382.140625</td>
      <td>23360.289062</td>
      <td>23992.669922</td>
      <td>735030000.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2018-02-08</td>
      <td>23860.460938</td>
      <td>23860.460938</td>
      <td>24903.679688</td>
      <td>23849.230469</td>
      <td>24902.300781</td>
      <td>657500000.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>403</th>
      <td>2017-01-03</td>
      <td>19881.759766</td>
      <td>19881.759766</td>
      <td>19938.529297</td>
      <td>19775.929688</td>
      <td>19872.859375</td>
      <td>339180000.0</td>
    </tr>
    <tr>
      <th>404</th>
      <td>2017-01-02</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>405</th>
      <td>2017-01-01</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



You may notice the previous closing prices are carried over on days the stock market is closed (e.g. weekends). You can choose to turn off this feature when you initialise your cryptory class (see `help(Cryptort.__init__)`).

With a little help from pandas, we can visualise the performance of bitcoin relative to some specific stocks and [indices](http://business.nasdaq.com/marketinsite/2016/Indexes-or-Indices-Whats-the-deal.html).


<div style="text-align:center" markdown="1">

![]({{ base_path }}/images/bitcoin_stocks_price_norm.png)

</div>


This graph shows the return you would have received if you had invested on January 3rd. As Bitcoin went up the most (>10x returns), it was objectively the best investment. While the inclusion of some names is hopefully intuitive enough, AMD and NVIDIA (and Intel to some extent) are special cases, as these companies produce the [graphics cards](http://www.techradar.com/news/best-mining-gpu) that underpin the hugely energy intensive (i.e. [wasteful](https://www.theguardian.com/technology/2018/jan/17/bitcoin-electricity-usage-huge-climate-cryptocurrency)) process of [crypto mining](https://news.bitcoin.com/a-visit-to-a-bitcoin-mining-farm-in-sichuan-china-reveals-troubles-beyond-regulation/). Kodak (not to be confused with the pre 2012 bankruptcy Kodak) made the list, as they announced their intention in early Jan 2018 to [create their own "photo-centric cryptocurrency"](https://www.nytimes.com/2018/01/30/technology/kodak-blockchain-bitcoin.html) (yes, that's what caused that blip).

As before, with a little bit of pandas work, you can create a bitcoin stock market correlation plot.


<div>
<select id="corr_choice_stock" style="font-size:0.8em">
  <option value="pearson">Pearson</option>
  <option value="spearman">Spearman</option>
</select>
</div>
<div class="result_img" style="text-align:center">
<img id="stock_picture" src="https://github.com/dashee87/dashee87.github.io/raw/master/images/stock_bitcoin_corr.png" alt="result.png" />
</div>
<div><br></div>
 
<script type="text/javascript">
$("#corr_choice_stock").change(function () {
   menu_val = $(this).val();
    if (menu_val=="pearson") {
        $('#stock_picture').attr('src', 'https://github.com/dashee87/dashee87.github.io/raw/master/images/stock_bitcoin_corr.png');
    } else {
        $('#stock_picture').attr('src', 'https://github.com/dashee87/dashee87.github.io/raw/master/images/stock_bitcoin_corr_spear.png');
    }
});
</script>


The highest correlation recorded (0.75) is between Google and Nasdaq, which is not surprising, as the former is large component of the latter. As for Bitcoin, it was most correlated with Google (0.12), but its relationship with the stock market was generally quite weak.

### Commodity Prices

While Bitcoin was originally envisioned as alternative system of payments, [high transaction fees and rising value has discouraged its use as a legitimate currency](https://hackernoon.com/ten-years-in-nobody-has-come-up-with-a-use-case-for-blockchain-ee98c180100). This has meant that Bitcoin and its successors have morphed into an alternative store of value- a sort of [easily lost](http://uk.businessinsider.com/nearly-4-million-bitcoins-have-been-lost-forever-study-says-2017-11) internet gold. So, it may be interesting to investigate the relationship between Bitcoin and the more traditional stores of value.

`cryptory` includes a `get_metal_prices` method that retrieves historical daily prices of various precious metals.


```python
my_cryptory.get_metal_prices()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>date</th>
      <th>gold_am</th>
      <th>gold_pm</th>
      <th>silver</th>
      <th>platinum_am</th>
      <th>platinum_pm</th>
      <th>palladium_am</th>
      <th>palladium_pm</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2018-02-10</td>
      <td>1316.05</td>
      <td>1314.10</td>
      <td>16.345</td>
      <td>972.0</td>
      <td>969.0</td>
      <td>970.0</td>
      <td>969.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2018-02-09</td>
      <td>1316.05</td>
      <td>1314.10</td>
      <td>16.345</td>
      <td>972.0</td>
      <td>969.0</td>
      <td>970.0</td>
      <td>969.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2018-02-08</td>
      <td>1311.05</td>
      <td>1315.45</td>
      <td>16.345</td>
      <td>974.0</td>
      <td>975.0</td>
      <td>990.0</td>
      <td>985.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>403</th>
      <td>2017-01-03</td>
      <td>1148.65</td>
      <td>1151.00</td>
      <td>15.950</td>
      <td>906.0</td>
      <td>929.0</td>
      <td>684.0</td>
      <td>706.0</td>
    </tr>
    <tr>
      <th>404</th>
      <td>2017-01-02</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>405</th>
      <td>2017-01-01</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



Again, we can easily plot the change in commodity over 2017 and 2018.


<div style="text-align:center" markdown="1">

![]({{ base_path }}/images/bitcoin_commodity_price.png)

</div>


Look at silly old gold appreciating slowly over 2017 and 2018, thus representing a [stable store of wealth](https://www.bullionvault.com/gold-guide/why-gold). As before, we can plot a price correlation matrix.


<div>
<select id="corr_choice_metal" style="font-size:0.8em">
  <option value="pearson">Pearson</option>
  <option value="spearman">Spearman</option>
</select>
</div>
<div class="result_img" style="text-align:center">
<img id="metal_picture" src="https://github.com/dashee87/dashee87.github.io/raw/master/images/bitcoin_commodity_corr.png" alt="result.png" />
</div>
<div><br></div>
 
<script type="text/javascript">
$("#corr_choice_metal").change(function () {
   menu_val = $(this).val();
    if (menu_val=="pearson") {
        $('#metal_picture').attr('src', 'https://github.com/dashee87/dashee87.github.io/raw/master/images/bitcoin_commodity_corr.png');
    } else {
        $('#metal_picture').attr('src', 'https://github.com/dashee87/dashee87.github.io/raw/master/images/bitcoin_commodity_corr_spear.png');
    }
});
</script>



Unsurprisingly, the various precious metals exhibit significant correlation, while bitcoin value appears completely unconnected. I suppose negative correlation could have provided evidence that people are moving away from traditional stores of value, but there's little evidence to support this theory.

### Foreign Exchange Rates

One of the motivations behind Bitcoin was to create a currency that wasn't controlled by any central authority. There could be no [quantitative easing](https://en.wikipedia.org/wiki/Quantitative_easing)- when the US Central Bank devalued the dollar by essentially printing trillions of new dollars to prop up the faltering economy after the 2007 financial crisis. As such, there may be a relationship between USD exchange rate (which would be devalued by such policies) and money moving into cryptocurrencies.

`cryptory` includes a `get_exchange_rates` method that retrieves historical daily exchange rate between particular currency pairs.


```python
my_cryptory.get_exchange_rates(from_currency="USD", to_currency="EUR")
```




<div>
<table border="1" class="dataframe" style="width:50%">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>date</th>
      <th>exch_rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2018-02-10</td>
      <td>1.2273</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2018-02-09</td>
      <td>1.2273</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2018-02-08</td>
      <td>1.2252</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>403</th>
      <td>2017-01-03</td>
      <td>1.0385</td>
    </tr>
    <tr>
      <th>404</th>
      <td>2017-01-02</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>405</th>
      <td>2017-01-01</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



As you can see, the USD has lost ground to the Euro over the last year. We can easily add a few more USD exchange rates (spoiler alert:the USD has depreciated relative to most major currencies). As the results are similar to the precious metals, that code can be found in the [Jupyter notebook](https://github.com/dashee87/blogScripts/blob/master/Jupyter/2018-02-11-analysing-the-factors-that-influence-cryptocurrency-prices-with-cryptory.ipynb).

### Oil Prices

Oil prices are strongly affected by the strength of the global economy (e.g. demand in China) and geopolitical instability (e.g. Middle East, Venezuela). Of course, there's other factors at play (shale, moves towards renewables, etc.), but you might want to have oil prices in your crypto price model in order to include these forces.

`cryptory` includes a `get_oil_prices` method that retrieves historical daily oil ([London Brent Crude](https://en.wikipedia.org/wiki/Brent_Crude)) prices.


```python
my_cryptory.get_oil_prices()
```




<div>
<table border="1" class="dataframe" style="width:50%">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>date</th>
      <th>oil_price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2018-02-10</td>
      <td>64.18</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2018-02-09</td>
      <td>64.18</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2018-02-08</td>
      <td>64.18</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>403</th>
      <td>2017-01-03</td>
      <td>52.36</td>
    </tr>
    <tr>
      <th>404</th>
      <td>2017-01-02</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>405</th>
      <td>2017-01-01</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



As you can see, oil is up about 20% since the start of 2017. Of course, you can plot the price over a longer time period.


<div style="text-align:center" markdown="1">

![]({{ base_path }}/images/oil_price_2000s.png)

</div>


## Future

So what's the future of cryptos? Moon, obviously! As for the future of `cryptory`, it already includes numerous tools that could improve price models (particularly, reddit and google trend metrics). But it's certainly lacking features that would take it to the moon: 
-  twitter statistics (specifically John McAffee's!!!) 
-  media analysis (number of mainstream articles, sentiment, etc.- [example](https://github.com/mattlisiv/newsapi-python))
-  more Asian-centric data sources (Japan and South Korea are said to account for [40%](https://www.ft.com/content/384936ac-e70c-11e7-97e2-916d4fbac0da) and [20%](http://www.straitstimes.com/asia/south-korean-officials-grapple-with-bitcoin-mania) of global bitcoin volume, respectively)
- more financial/crypto data (integrate [Quandl api](https://www.quandl.com/tools/python))

In my next post, I'll use `cryptory` to (hopefully) improve the [previous LSTM crypto price prediction model](https://dashee87.github.io/deep%20learning/python/predicting-cryptocurrency-prices-with-deep-learning/). While you wait for that, you can perform your own cryptocurrency analysis with the [accompanying Jupyter notebook](https://github.com/dashee87/blogScripts/blob/master/Jupyter/2018-02-11-analysing-the-factors-that-influence-cryptocurrency-prices-with-cryptory.ipynb). Thanks for reading!
