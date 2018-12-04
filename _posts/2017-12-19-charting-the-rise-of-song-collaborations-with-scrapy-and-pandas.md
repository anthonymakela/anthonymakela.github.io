---
title: "Charting the Rise of Song Collaborations with Scrapy and Pandas"
excerpt: "Taking a break from deep learning, this post explores the recent surge in song collaborations in the pop charts"
layout: single
header:
  overlay_image: studio-collab-overlay.jpg
  overlay_filter: 0.4
  caption: "Dropping some sick beatz"
  cta_label: "Switch to R version"
  cta_url: "https://dashee87.github.io/data%20science/r/charting-the-rise-of-song-collaborations/"
categories:
  - data science
  - python
tags:
  - music
  - collaboration
  - pandas
  - scrapy
  - python
author: "David Sheehan"
date: "19 December 2017"
---


Keen readers of this blog (hi Mom!) might have noticed my recent focus on neural networks and deep learning. It's good for popularity, as deep learning posts are automatically cool ([I'm really big in China now](https://jiasuhui.com/article/3855)). Well, I'm going to leave the AI alone this time. In fact, this post won't even really constitute data science. Instead, I'm going to explore a topic that has been on my mind and maybe produce a few graphs.

These days, my main interaction with modern music is through the radio at the gym. It wasn't always like this. I mean [I used to be with it](https://www.youtube.com/watch?v=ajmI1P3r1w4), but then they changed what it was. I wouldn't go so far as to say that modern music is weird and scary, but it's certainly getting harder to keep up. It doesn't help that songs now have about 5 people on them. Back in my day, you might include a [brief rapper cameo to appear more edgy](http://www.youtube.com/watch?v=kfVsfOSbJY0&t=2m30s). So I thought I'd explore how song collaborations have come to dominate the charts. 

Note that the accompanying Jupyter notebook can be viewed [here](https://github.com/dashee87/blogScripts/blob/master/Jupyter/2017-12-19-charting-the-rise-of-song-collaborations-with-scrapy-and-pandas.ipynb). Let's get started!

## Scrapy

In my research, I came across a similar [post](https://medium.com/fun-with-data-and-stats/visualizing-artist-collaborations-in-the-billboard-top-10-songs-ff6188a0f57b). That one looked at the top 10 of the Billboard charts going back to 1990. Just to be different, I'll primarily focus on the UK singles chart, though I'll also pull data from the Billboard chart. From what I can tell, there's no public API. But it's not too hard to scrape the data off [the official site](http://www.officialcharts.com/charts/singles-chart/). I'm going to use [Scrapy](https://scrapy.org/). We'll set up a spider to pull the relevant data and then navigate to the previous week's chart and repeat that process until it finally reaches the [first chart in November 1952](http://www.officialcharts.com/charts/singles-chart/19521114/7501/). This is actually the first time I've ever used Scrapy (hence the motivation for this post), so check out its extensive documentation if you have any issues. Scrapy isn't the only option for web scraping with Python (others reviewed [here](https://bigishdata.com/2017/06/06/web-scraping-with-python-part-two-library-overview-of-requests-urllib2-beautifulsoup-lxml-scrapy-and-more/), but I like how easy it is to [deploy and automate](https://doc.scrapy.org/en/latest/topics/deploy.html) your spiders for larger projects.

```python
import scrapy
import re # for text parsing
import logging

class ChartSpider(scrapy.Spider):
    name = 'ukChartSpider'
    # page to scrape
    start_urls = ['http://www.officialcharts.com/charts/']
    # if you want to impose a delay between sucessive scrapes
#    download_delay = 0.5

    def parse(self, response):
        self.logger.info('Scraping page: %s', response.url)
        chart_week = re.sub(' -.*', '', 
                        response.css('.article-heading+ .article-date::text').extract_first().strip())
        
        for (artist, chart_pos, artist_num, track, label, lastweek, peak_pos, weeks_on_chart) in \
                             zip(response.css('#main .artist a::text').extract(),
                                 response.css('.position::text').extract(),
                                 response.css('#main .artist a::attr(href)').extract(),
                                 response.css('.track .title a::text').extract(),
                                 response.css('.label-cat .label::text').extract(),
                                 response.css('.last-week::text').extract(),
                                 response.css('td:nth-child(4)::text').extract(),
                                 response.css('td:nth-child(5)::text').extract()):
            yield {'chart_week': chart_week, 'chart_pos':chart_pos, 'track': track, 'artist': artist, 
                   'artist_num':re.sub('/.*', '', re.sub('/artist/', '', artist_num)), 
                   'label':label, 'last_week':re.findall('\d+|$', lastweek)[0],
                  'peak_pos':re.findall('\d+|$', peak_pos)[0], 
                   'weeks_on_chart':re.findall('\d+|$', weeks_on_chart)[0]}

# move onto next page (if it exists)             
        for next_page in response.css('.charts-header-panel:nth-child(1) .chart-date-directions'):
            if next_page.css("a::text").extract_first()=='prev':
                yield response.follow(next_page, self.parse)
```

Briefly explaining what happened there: We create a class called `ChartSpider`, essentially our customised spider (called `ukChartSpider`). We specify the page we want to scrape (`start_urls`). The spider then selects specific CSS elements (`response.css()`) within the page that contain the information we want (e.g. `#main .artist a` represents the artist's name). These tags may seem complicated, but they're actually quite easy to retrieve with a tool like [Selector Gadget](http://selectorgadget.com/). Isolate the elements you want to extract and copy the css elements highlighted with the tool (see image below).

<div style="text-align:center" markdown="1">

![]({{ base_path }}/images/selector_gadget_.png)

</div>

Finally, we'll opt to write the spider output to a json file called `uk_charts.json`. Scrapy accepts [numerous file formats](https://doc.scrapy.org/en/latest/topics/feed-exports.html) (including CSV), but I went with JSON as it's easier to append to this file type, which may be useful if your spider unexpectedly terminates.  We're now ready to launch `ukChartSpider`. Note that the process for the US Billboard chart is very similar. That code can be found in the [accompanying Jupyter notebook](https://github.com/dashee87/blogScripts/blob/master/Jupyter/2017-12-19-charting-the-rise-of-song-collaborations-with-scrapy-and-pandas.ipynb).


```python
from scrapy.crawler import CrawlerProcess

process = CrawlerProcess({
'USER_AGENT': 'Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1)',
'FEED_FORMAT': 'json',
'FEED_URI': 'uk_charts.json'
})

# minimising the information presented on the scrapy log
logging.getLogger('scrapy').setLevel(logging.WARNING)
process.crawl(ChartSpider)
process.start()
```

    2017-12-18 23:26:29 [scrapy.utils.log] INFO: Scrapy 1.4.0 started (bot: scrapybot)
    2017-12-18 23:26:29 [scrapy.utils.log] INFO: Overridden settings: {'FEED_FORMAT': 'json', 'FEED_URI': 'uk_charts.json', 'USER_AGENT': 'Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1)'}
    2017-12-18 23:26:30 [ukChartSpider] INFO: Scraping page: http://www.officialcharts.com/charts/
    2017-12-18 23:26:30 [ukChartSpider] INFO: Scraping page: http://www.officialcharts.com/charts/singles-chart/20171208/7501/


## Pandas

If that all went to plan, we can now load in the json file as pandas dataframe (unless you changed the file path, it should be sitting in your working directory). If you can't wait for the spider to conclude, then you can import the file directly from github (you can also find the corresponding Billboard Hot 100 file [there](https://github.com/dashee87/blogScripts/tree/master/files)- you might prefer downloading the files and importing them locally).


```python
import pandas as pd
uk_charts = pd.read_json('uk_charts.json')
# convert the date column to the correct date format
uk_charts = uk_charts.assign(chart_week=pd.to_datetime(uk_charts['chart_week']))
uk_charts.head(5)
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
      <th>artist</th>
      <th>artist_num</th>
      <th>chart_pos</th>
      <th>chart_week</th>
      <th>label</th>
      <th>last_week</th>
      <th>peak_pos</th>
      <th>track</th>
      <th>weeks_on_chart</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>ED SHEERAN</td>
      <td>6692</td>
      <td>1</td>
      <td>2017-12-08</td>
      <td>ASYLUM</td>
      <td>3</td>
      <td>1</td>
      <td>PERFECT</td>
      <td>30</td>
    </tr>
    <tr>
      <th>1</th>
      <td>RAK-SU FT WYCLEF/NAUGHTY BOY</td>
      <td>52716</td>
      <td>2</td>
      <td>2017-12-08</td>
      <td>SYCO MUSIC</td>
      <td></td>
      <td>2</td>
      <td>DIMELO</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>RITA ORA</td>
      <td>7418</td>
      <td>3</td>
      <td>2017-12-08</td>
      <td>ATLANTIC</td>
      <td>2</td>
      <td>2</td>
      <td>ANYWHERE</td>
      <td>7</td>
    </tr>
    <tr>
      <th>3</th>
      <td>CAMILA CABELLO FT YOUNG THUG</td>
      <td>51993</td>
      <td>4</td>
      <td>2017-12-08</td>
      <td>EPIC/SYCO MUSIC</td>
      <td>1</td>
      <td>1</td>
      <td>HAVANA</td>
      <td>18</td>
    </tr>
    <tr>
      <th>4</th>
      <td>MARIAH CAREY</td>
      <td>25943</td>
      <td>5</td>
      <td>2017-12-08</td>
      <td>COLUMBIA</td>
      <td>22</td>
      <td>2</td>
      <td>ALL I WANT FOR CHRISTMAS IS YOU</td>
      <td>83</td>
    </tr>
  </tbody>
</table>
</div>



That table shows the top 5 singles in the UK for week starting 8st December 2017. I think I recognise two of those songs. As we're interested in collaborations, you'll notice that we have a few in this top 5 alone, which are marked with an 'FT' in the artist name. Unfortunately, there's [no consistent nomenclature to denote collaborations](https://music.stackexchange.com/questions/25532/whats-the-difference-between-feat-artist1-x-artist-2-artist1-vs-artist2) on the UK singles chart (the Billboard chart isn't as bad).

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
      <th>artist</th>
      <th>artist_num</th>
      <th>chart_pos</th>
      <th>chart_week</th>
      <th>label</th>
      <th>last_week</th>
      <th>peak_pos</th>
      <th>track</th>
      <th>weeks_on_chart</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>128157</th>
      <td>WEST END FEAT. SYBIL</td>
      <td>41240</td>
      <td>8</td>
      <td>1993-02-14</td>
      <td>PWL SANCTUARY</td>
      <td>4</td>
      <td>3</td>
      <td>THE LOVE I LOST</td>
      <td>6</td>
    </tr>
    <tr>
      <th>98974</th>
      <td>JODE FEATURING YO-HANS</td>
      <td>7134</td>
      <td>75</td>
      <td>1998-12-20</td>
      <td>LOGIC</td>
      <td>48</td>
      <td>48</td>
      <td>WALK... (THE DOG) LIKE AN EGYPTIAN</td>
      <td>2</td>
    </tr>
    <tr>
      <th>89799</th>
      <td>MUTINY FEAT D-EMPRESS</td>
      <td>9653</td>
      <td>100</td>
      <td>2000-09-24</td>
      <td>AZULI</td>
      <td></td>
      <td>100</td>
      <td>NEW HORIZONS</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>RAK-SU FT WYCLEF/NAUGHTY BOY</td>
      <td>52716</td>
      <td>2</td>
      <td>2017-12-08</td>
      <td>SYCO MUSIC</td>
      <td></td>
      <td>2</td>
      <td>DIMELO</td>
      <td>1</td>
    </tr>
    <tr>
      <th>69097</th>
      <td>DJ SAMMY AND YANOU FT DO</td>
      <td>3502</td>
      <td>98</td>
      <td>2004-09-12</td>
      <td>DATA/MOS</td>
      <td>100</td>
      <td>1</td>
      <td>HEAVEN</td>
      <td>28</td>
    </tr>
    <tr>
      <th>11</th>
      <td>SELENA GOMEZ &amp; MARSHMELLO</td>
      <td>52496</td>
      <td>12</td>
      <td>2017-12-08</td>
      <td>INTERSCOPE</td>
      <td>9</td>
      <td>9</td>
      <td>WOLVES</td>
      <td>6</td>
    </tr>
    <tr>
      <th>31974</th>
      <td>SOLDIERS WITH ROBIN GIBB</td>
      <td>25894</td>
      <td>75</td>
      <td>2011-10-30</td>
      <td>DMG TV</td>
      <td></td>
      <td>75</td>
      <td>I'VE GOTTA GET A MESSAGE TO YOU</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4595</th>
      <td>KUNGS VS COOKIN' ON 3 BURNERS</td>
      <td>49557</td>
      <td>96</td>
      <td>2017-01-27</td>
      <td>3 BEAT</td>
      <td>90</td>
      <td>2</td>
      <td>THIS GIRL</td>
      <td>33</td>
    </tr>
    <tr>
      <th>98596</th>
      <td>SLADE VS. FLUSH</td>
      <td>5538</td>
      <td>97</td>
      <td>1999-01-17</td>
      <td>POLYDOR</td>
      <td></td>
      <td>30</td>
      <td>MERRY XMAS EVERYBODY '98 REMIX</td>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div>



Okay, we've identified various terms that denote collaborations of some form. Not too bad. We just need to count the number of instances where the artist name includes one of these terms. Right? Maybe not.


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
      <th>artist</th>
      <th>artist_num</th>
      <th>chart_pos</th>
      <th>chart_week</th>
      <th>label</th>
      <th>last_week</th>
      <th>peak_pos</th>
      <th>track</th>
      <th>weeks_on_chart</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>196512</th>
      <td>AC/DC</td>
      <td>16970</td>
      <td>51</td>
      <td>1978-06-04</td>
      <td>ATLANTIC</td>
      <td></td>
      <td>51</td>
      <td>ROCK AND ROLL DAMNATION</td>
      <td>1</td>
    </tr>
    <tr>
      <th>129655</th>
      <td>BOB MARLEY AND THE WAILERS</td>
      <td>31532</td>
      <td>5</td>
      <td>1992-09-27</td>
      <td>TUFF GONG</td>
      <td>6</td>
      <td>5</td>
      <td>IRON LION ZION</td>
      <td>3</td>
    </tr>
    <tr>
      <th>203656</th>
      <td>BOB MARLEY &amp; THE WAILERS</td>
      <td>31532</td>
      <td>40</td>
      <td>1975-09-21</td>
      <td>ISLAND</td>
      <td></td>
      <td>40</td>
      <td>NO WOMAN NO CRY</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>



I'm a firm believer that [domain expertise is a fundamental component of data science](https://dashee87.github.io/football/python/predicting-football-results-with-statistical-modelling/), so good data scientists must always be mindful of AC/DC and Bob Marley. Obviously, these songs shouldn't be considered collaborations, so we need to exclude them from the analysis. Rather than manually evaluating each case, we'll discount artists that include  '&', 'AND', 'WITH', 'VS' that registered more than one song on the chart ('FT' and 'FEATURING' are pretty reliable- please let me know if I'm overlooking some brilliant 1980s post-punk new wave synth-pop group called 'THE FT FEATURING FT'). Obviously, we'll still have some one hit wonders mistaken as collaborations. For example, Derek and the Dominoes had only one hit single (Layla); though we're actually lucky in this instance, as the song was rereleased in 1982 under a slight different name.


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
      <th>artist</th>
      <th>artist_num</th>
      <th>chart_pos</th>
      <th>chart_week</th>
      <th>label</th>
      <th>last_week</th>
      <th>peak_pos</th>
      <th>track</th>
      <th>weeks_on_chart</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>181904</th>
      <td>DEREK AND THE DOMINOES</td>
      <td>14664</td>
      <td>68</td>
      <td>1982-02-28</td>
      <td>RSO</td>
      <td></td>
      <td>68</td>
      <td>LAYLA {1982}</td>
      <td>1</td>
    </tr>
    <tr>
      <th>211792</th>
      <td>DEREK AND THE DOMINOES</td>
      <td>14664</td>
      <td>25</td>
      <td>1972-08-06</td>
      <td>POLYDOR</td>
      <td></td>
      <td>25</td>
      <td>LAYLA</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
uk_charts = pd.merge(uk_charts,
         uk_charts.groupby('artist').track.nunique().reset_index().rename(
        columns={'track': 'one_hit'}).assign(one_hit = lambda x: x.one_hit==1)).sort_values(
        ['chart_week', 'chart_pos'], ascending=[0, 1]).reset_index(drop=True)
uk_charts.head()
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
      <th>artist</th>
      <th>artist_num</th>
      <th>chart_pos</th>
      <th>chart_week</th>
      <th>label</th>
      <th>last_week</th>
      <th>peak_pos</th>
      <th>track</th>
      <th>weeks_on_chart</th>
      <th>one_hit</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>ED SHEERAN</td>
      <td>6692</td>
      <td>1</td>
      <td>2017-12-08</td>
      <td>ASYLUM</td>
      <td>3</td>
      <td>1</td>
      <td>PERFECT</td>
      <td>30</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>RAK-SU FT WYCLEF/NAUGHTY BOY</td>
      <td>52716</td>
      <td>2</td>
      <td>2017-12-08</td>
      <td>SYCO MUSIC</td>
      <td></td>
      <td>2</td>
      <td>DIMELO</td>
      <td>1</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2</th>
      <td>RITA ORA</td>
      <td>7418</td>
      <td>3</td>
      <td>2017-12-08</td>
      <td>ATLANTIC</td>
      <td>2</td>
      <td>2</td>
      <td>ANYWHERE</td>
      <td>7</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>CAMILA CABELLO FT YOUNG THUG</td>
      <td>51993</td>
      <td>4</td>
      <td>2017-12-08</td>
      <td>EPIC/SYCO MUSIC</td>
      <td>1</td>
      <td>1</td>
      <td>HAVANA</td>
      <td>18</td>
      <td>True</td>
    </tr>
    <tr>
      <th>4</th>
      <td>MARIAH CAREY</td>
      <td>25943</td>
      <td>5</td>
      <td>2017-12-08</td>
      <td>COLUMBIA</td>
      <td>22</td>
      <td>2</td>
      <td>ALL I WANT FOR CHRISTMAS IS YOU</td>
      <td>83</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>




We've appended a column denoting whether that song represents that artist's only ever entry in the charts. We can use a few more tricks to weed out mislabelled collaborations. We'll ignore entries where the artist name contains 'AND THE' or '& THE'. Again, it's not perfect, but it should get us most of the way (data science in a nutshell). For example, 'Ariana Grande & The Weeknd' would be overlooked, so I'll crudely include a clause to allow The Weeknd related collaborations. With those caveats, let's plot the historical frequency of these various collaboration terms.


<div style="text-align:center" markdown="1">

![]({{ base_path }}/images/uk_us_collaboration_terms.png)

</div>

In the 1960s, 70s and 80s, colloborations were relatively rare (~5% of charted singles) and generally took the form of duets. Things changed in the mid 90s, when the number of colloborations increases significantly, with duets dying off and featured artists taking over. I blame rap music. Comparing the two charts, the UK and US prefer 'ft' and 'featuring', repsectively ([two nations divided by a common language](https://english.stackexchange.com/questions/74737/what-is-the-origin-of-the-phrase-two-nations-divided-by-a-common-language)). The Billboard chart doesn't seem to like the '/' notation, while the UK is generally much more eclectic. 

Finally, we can plot the proportion of songs that were collobarations (satisfied any of these conditions).

<div style="text-align:center" markdown="1">

![]({{ base_path }}/images/uk_us_collaboration_prop.png)

</div>


Clearly, collaborations are on the rise in both the US and UK, with nearly half of all charted songs now constituting collaborations of some form. I should say the Billboard chart has always consisted of 100 songs (hence the name), while the UK chart originally had 12 songs (gradually increasing to 50 in 1960 and 75 in 1978, finally settling on 100 in 1994). That may explain why the UK records high percentages in 1950s, as it would only require several colloborations. 

Broadly speaking, the number of collaborations is pretty similar across the two countries. I suppose this isn't surprising, as famous artists are commonly popular in both countries. Between 1995 and 2005, the proportion of collaborations runs slightly higher on the Billboard chart. Without any rigorous analysis to validate my speculations, I put this down to rap music. This genre tends to have more featured artists and I suspect it took longer for it to achieve mainstream popularity in the UK. Nevertheless, there's no denying that collaborations are well on their way to chart domination.

## Summary

Using [Scrapy](https://scrapy.org/), we pulled historical data for both the [UK Singles Chart](http://www.officialcharts.com/charts/singles-chart/) and the [Billboard Hot 100](https://www.billboard.com/charts/hot-100). We converted it into a Pandas dataframe, which allowed us to manipulate the artist names to distinguish collaborations and highlight of popularity of various collaboration types. Finally, we've illustrated the recent surge in song collaborations, which now account for nearly half of all songs on the chart.

So, that's it. I apologise for the speculations and lack of cool machine learning. In my next post, I'll return to artificial intelligence to predict future duets between current and now deceased artists (e.g. 'Bob Marley & The Weeknd'). While you wait a very long time for that, you can download the historical UK chart and Billboard Top 100 files [here](https://github.com/dashee87/blogScripts/tree/master/files) or play around with the [accompanying Jupyter notebook](https://github.com/dashee87/blogScripts/blob/master/Jupyter/2017-12-19-charting-the-rise-of-song-collaborations-with-scrapy-and-pandas.ipynb). Thanks for reading!
