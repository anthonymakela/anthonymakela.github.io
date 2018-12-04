---
title: "Home Advantage in Football Leagues Around the World"
excerpt: "This post investigates the universally known but poorly understood home advantage and how it varies in football leagues around the world"
layout: single
header:
  overlay_image: home_field_overlay.jpg
  overlay_filter: 0.5
  caption: "I guessed AEK Athens, but it's actually Columbus Crew of the MLS"
categories:
  - data science
  - python
tags:
  - football
  - soccer
  - python
  - scrapy
  - d3
author: "David Sheehan"
date: "10 January 2018"
---

Reflecting on 2017, I decided to return to my [most popular blog topic](https://dashee87.github.io/football/python/predicting-football-results-with-statistical-modelling/) (at least by the number of emails I get). Last time, I built a crude statistical model to predict the result of football matches. I even presented a webinar on the subject [here](https://www.brighttalk.com/webcast/9059/282915/predicting-football-results-with-statistical-modelling) (it's free to sign up). During the presentation, I described a coefficient in the model that accounts for the fact that the home team tends to score more goals than the away team. This is called the home advantage (or home field advantage) and can [probably be explained](https://www.theguardian.com/sport/2008/feb/03/features.sportmonthly16) by a combination of physcological (e.g. familiarity with surroundings) and physical factors (e.g. travel). [It occurs in various sports](https://www.researchgate.net/publication/7671541_Long-term_trends_in_home_advantage_in_professional_team_sports_in_North_America_and_England_1876-2003f), including American football, baseball, basketball and soccer. Sticking to soccer/football, I mentioned in my talk how it would be interesting to see how this effect varies around the world. In which countries do the home teams enjoy the greatest advantage?

We're going to use the [same statistcal model as last time](https://dashee87.github.io/football/python/predicting-football-results-with-statistical-modelling/), so there won't be any new statistical features developed in this post. Instead, it will focus on retrieving the appropriate goals data for even the most obscure leagues in the world (yes, even the Irish Premier Division) and then interactively visualising the results with D3. The full code can be found in the [accompanying Jupyter notebook](https://github.com/dashee87/blogScripts/blob/master/Jupyter/2018-01-10-home-advantage-in-football-leagues-around-the-world.ipynb).

## Calculating Home Field Advantage

The first consideration should probably be how to calculate home advantage. The [traditional approach](https://en.wikipedia.org/wiki/Home_advantage#Measuring_of_home-field_advantage) is to look at team matchups and check whether teams achieved better, equal or worse results at home than away. For example, let's imagine Chlesea beat Arsenal 2-0 at home and drew 1-1 away. That would be recored as a better home result (+2 goals versus 0). This process is repeated for every opponent and so [you can actually construct a trinomial distribution and test whether there was a statistically significant home field effect](https://www.researchgate.net/publication/318588534_Home_Team_Advantage_in_English_Premier_League). This works for balanced leagues, where team play each other an equal number of times home and away. While this holds for Europe's most famous leagues (e.g. EPL, La Liga), there are various leagues where teams play each other threes times (e.g. Ireland, Montenegro, Tajikistan aka The Big Leagues) or even just once (e.g Argetnina, Libya and to a lesser extent MLS (balanced for teams within the same conference)). There's also issues with postponements and abandonments rendering some leagues slightly unbalanced (e.g. Sri Lanka). For those reasons, we'll opt for a different (though not necessarily better) approach.

In the [previous post](https://dashee87.github.io/football/python/predicting-football-results-with-statistical-modelling/), we built a model for the EPL 2016/17 season, using the number of goals scored in the past to predict future results. Looking at the model coefficients again, you see the `home` coefficient has a value of approximately 0.3. By taking the exponent of this value ($$e^{0.3}=1.35$$), it tells us that the home team are generally 1.35 times more likely to score than the away team. In case you don't recall, the model accounts for team strength/weakness by including coefficients for each team (e.g  0.07890 and -0.96194 for Chelsea and Sunderland, respectively). 

Let's see how this value compares with the lower divisions in England over the past 10 years. We'll pull the data from [football-data.co.uk](football-data.co.uk), which can loaded in directly using the url link for each csv file. First, we'll design a function that will take a dataframe of match results as an input and return the home field advantage (plus confidence interval limits) for that league.


```python
# importing the tools required for the Poisson regression model
import statsmodels.api as sm
import statsmodels.formula.api as smf
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np
import seaborn

def get_home_team_advantage(goals_df, pval=0.05):
    
    # extract relevant columns
    model_goals_df = goals_df[['HomeTeam','AwayTeam','FTHG','FTAG']]
    # rename goal columns
    model_goals_df = model_goals_df.rename(columns={'FTHG': 'HomeGoals', 'FTAG': 'AwayGoals'})

    # reformat dataframe for the model
    goal_model_data = pd.concat([model_goals_df[['HomeTeam','AwayTeam','HomeGoals']].assign(home=1).rename(
                columns={'HomeTeam':'team', 'AwayTeam':'opponent','HomeGoals':'goals'}),
               model_goals_df[['AwayTeam','HomeTeam','AwayGoals']].assign(home=0).rename(
                columns={'AwayTeam':'team', 'HomeTeam':'opponent','AwayGoals':'goals'})])

    # build poisson model
    poisson_model = smf.glm(formula="goals ~ home + team + opponent", data=goal_model_data, 
                            family=sm.families.Poisson()).fit()
    # output model parameters
    poisson_model.summary()
    
    return np.concatenate((np.array([poisson_model.params['home']]), 
                    poisson_model.conf_int(alpha=pval).values[-1]))
```


I've essentially combined various parts of the previous post into one convenient function. If it looks a little strange, then I suggest you consult the original post. Okay, we're ready to start calculating some home advantage scores.


```python
# home field advantage for EPL 2016/17 season
get_home_team_advantage(pd.read_csv("http://www.football-data.co.uk/mmz4281/1617/E0.csv"))
```




    array([ 0.2838454,  0.16246  ,  0.4052308])



It's as easy as that. Feed a url from [football-data.co.uk](http://www.football-data.co.uk/data.php) into the function and it'll quickly tell you the statistical advantage enjoyed by home teams in that league. Note that the latter two values repesent the left and right limit of the 95% confidence interval around the mean value. The first value in the array is actually just the log of the number of goals scored by the home team divided by the total number of away goals.


```python
temp_goals_df = pd.read_csv("http://www.football-data.co.uk/mmz4281/1617/E0.csv")
[np.exp(get_home_team_advantage(temp_goals_df)[0]),
 np.sum(temp_goals_df['FTHG'])/float(np.sum(temp_goals_df['FTAG']))]
```




    [1.3282275711159723, 1.3282275711159737]



The goals ratio calculation is obviously much simpler and definitely more intuitive. But it doesn't allow me to reference [my previous post](https://dashee87.github.io/football/python/predicting-football-results-with-statistical-modelling/) as much ([link](https://dashee87.github.io/football/python/predicting-football-results-with-statistical-modelling/) [link](https://dashee87.github.io/football/python/predicting-football-results-with-statistical-modelling/) [link](https://dashee87.github.io/football/python/predicting-football-results-with-statistical-modelling/)) and it fails to provide any uncertainty around the headline figure. Let's plot the home advantage figure for the top 5 divisions of the English league pyramid for since 2005. You can remove those hugely informative confidence interval bars by switching the toggle.

<style>
.switch {
  position: relative;
  display: inline-block;
  width: 60px;
  height: 34px;
}

.switch input {display:none;}

.slider {
  position: absolute;
  cursor: pointer;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: #ccc;
  -webkit-transition: .4s;
  transition: .4s;
}

.slider:before {
  position: absolute;
  content: "";
  height: 26px;
  width: 26px;
  left: 4px;
  bottom: 4px;
  background-color: white;
  -webkit-transition: .4s;
  transition: .4s;
}

input:checked + .slider {
  background-color: #2196F3;
}

input:focus + .slider {
  box-shadow: 0 0 1px #2196F3;
}

input:checked + .slider:before {
  -webkit-transform: translateX(26px);
  -ms-transform: translateX(26px);
  transform: translateX(26px);
}

.slider.round {
  border-radius: 34px;
}

.slider.round:before {
  border-radius: 50%;
}
</style>

<div style="font-size:0.9em">Error Bars<br>
<label class="switch" style="text-align:left">
  <input type="checkbox" checked id="link_checkbox">
  <span class="slider round"></span>
</label>
</div>
<div class="result_img" style="text-align:center">
<img id="picture" src="https://github.com/dashee87/dashee87.github.io/raw/master/images/england_home_field_advantage_bars.png" alt="result.png" />
</div>

<script type="text/javascript">
$("#link_checkbox").click(function () {
    if ($(this).is(":checked")) {
        $('#picture').attr('src', 'https://github.com/dashee87/dashee87.github.io/raw/master/images/england_home_field_advantage_bars.png');
    } else {
        $('#picture').attr('src', 'https://github.com/dashee87/dashee87.github.io/raw/master/images/england_home_field_advantage.png');
    }
});
</script>


It's probably more apparent without those hugely informative confidence interval bars, but it seems that the home advantage score decreases slightly as you move down the pyramid ([analysis by Sky Sports produced something similar](http://www.skysports.com/football/news/11096/10955089/sky-sports-bust-common-football-myths-home-advantage)). This might make sense for two reasons. Firstly, bigger teams generally have larger stadiums and more supporters, which could strengthen the home field advantage. Secondly, as you go down the leagues, I suspect the quality gap between teams narrows. Taking it to an extreme, when I used to play Sunday league football, it didn't really matter where we played... we still lost. In that sense, one must be careful comparing the home advantage between leagues, as it will be affected by the relative team strengths within those leagues. For example, a league with a very dominant team (or teams) will record a lower home advantage score, as that dominant team will score goals home and away with little difference (Man Utd would probably beat Cork City 6-0 at Old Trafford and Turners Cross!).

Having warned about the dangers of comparing different leagues with this approach, let's now compare the top five leagues in Europe over the same time period as before.

<div style="font-size:0.9em">Error Bars<br>
<label class="switch" style="text-align:left">
  <input type="checkbox" id="europe_link_checkbox">
  <span class="slider round"></span>
</label>
</div>
<div class="result_img" style="text-align:center">
<img id="europe_picture" src="https://github.com/dashee87/dashee87.github.io/raw/master/images/europe_home_field_advantage.png" alt="result.png" />
</div>

<script type="text/javascript">
$("#europe_link_checkbox").click(function () {
    if ($(this).is(":checked")) {
        $('#europe_picture').attr('src', 'https://github.com/dashee87/dashee87.github.io/raw/master/images/europe_home_field_advantage_bars.png');
    } else {
        $('#europe_picture').attr('src', 'https://github.com/dashee87/dashee87.github.io/raw/master/images/europe_home_field_advantage.png');
    }
});
</script>


Honestly, there's not much going on there. With the poissble exception of the Spanish La Liga since 2010, the home field advantage enjoyed by the teams in each league is broadly similar (and that's before we bring in the idea of confidence intervals and hypothesis testing).

## Home Advantage Around the World

To find more interesting contrasts, we must venture to crappier and more corrupt leagues. My hunch is that home advantage would be negligible in countries where the overall quality (team, infastructure, etc.) is very low. And by low, I mean leagues worse than the Irish Premier Division (yes, they exist). Unfortunately, the historical results for such leagues are not available on football-data.co.uk. Instead, we'll scrape the data off [betexplorer](http://www.betexplorer.com). I'm extremely impressed by the breadth of this site. You can even retrieve past results for the French overseas department of [Réunion](http://www.betexplorer.com/soccer/reunion/regionale-1/results/). Fun fact: [Dimtri Payet](https://en.wikipedia.org/wiki/Dimitri_Payet#Early_career) spent the 2004 season at AS Excelsior of the Réunion Premier League.

We'll use [Scrapy](https://scrapy.org/) to pull the appropriate information off the website. If you've never used Scrapy before, then you should check out [this post](https://dashee87.github.io/data%20science/python/charting-the-rise-of-song-collaborations-with-scrapy-and-pandas/). I won't spend too long on this part, but you can find the full code [here](https://github.com/dashee87/blogScripts/blob/master/Jupyter/2018-01-10-home-advantage-in-football-leagues-around-the-world.ipynb).


You don't actually need to run your own spider, as I've shared the output to [my GitHub account](https://github.com/dashee87/blogScripts/tree/master/files). We can import the json file in directly using pandas.


```python
all_league_goals = pd.read_json(
    "https://raw.githubusercontent.com/dashee87/blogScripts/master/files/all_league_goals.json")
# reorder the columns to it a bit more logical
all_league_goals = all_league_goals[['country', 'league', 'date', 'HomeTeam', 
                                     'AwayTeam', 'FTHG', 'FTAG', 'awarded']]
all_league_goals.head()
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
      <th>country</th>
      <th>league</th>
      <th>date</th>
      <th>HomeTeam</th>
      <th>AwayTeam</th>
      <th>FTHG</th>
      <th>FTAG</th>
      <th>awarded</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Albania</td>
      <td>Super League 2016/2017</td>
      <td>2017-05-27</td>
      <td>Korabi Peshkopi</td>
      <td>Flamurtari</td>
      <td>0</td>
      <td>3</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Albania</td>
      <td>Super League 2016/2017</td>
      <td>2017-05-27</td>
      <td>Laci</td>
      <td>Teuta</td>
      <td>2</td>
      <td>1</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Albania</td>
      <td>Super League 2016/2017</td>
      <td>2017-05-27</td>
      <td>Luftetari Gjirokastra</td>
      <td>Kukesi</td>
      <td>1</td>
      <td>0</td>
      <td>False</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Albania</td>
      <td>Super League 2016/2017</td>
      <td>2017-05-27</td>
      <td>Skenderbeu</td>
      <td>Partizani</td>
      <td>2</td>
      <td>2</td>
      <td>False</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Albania</td>
      <td>Super League 2016/2017</td>
      <td>2017-05-27</td>
      <td>Vllaznia</td>
      <td>KF Tirana</td>
      <td>0</td>
      <td>0</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>



Hopefully, that's all relatively clear. You'll notice that it's very similar to the format used by football-data, which means that we can feed this dataframe into the `get_home_team_advantage` function. Sometimes, matches are awarded due to one team fielding an ineligible player or crowd trouble. We should probably exclude such matches from the home field advantage calculations.


```python
# little bit of data cleansing to remove fixtures that were abandoned/awarded/postponed
all_league_goals = all_league_goals[~all_league_goals['awarded']]
all_league_goals = all_league_goals[all_league_goals['FTAG']!='POSTP.']
all_league_goals = all_league_goals[all_league_goals['FTAG']!='CAN.']
all_league_goals[['FTAG', 'FTHG']] = all_league_goals[['FTAG', 'FTHG']].astype(int)
```

We're ready to put it all together. I'll omit the code (though it can be found here), but we'll loop through each country and league combination (just in case you decide to include multiple leagues from the same country) and calculate the home advantage score, plus its confidence limits as well as some other information for each league (number of teams, average number of goals in each match). I've converted the pandas output to a [datatables](https://datatables.net/) table that you can interactively filter and sort.

{% include league_goal_table.html %}

Focusing on the `home_adv score` column, teams in Nigeria by far enjoy the greatest benefit from playing at home (score = 1.195). In other words, home teams scored 3.3 (= $$e^{1.195}$$) times more goals than their opponents. This isn't new information and [can be attributed to a combination of corruption (e.g. bribing referees) and violent fans](https://www.theguardian.com/football/blog/2013/oct/29/nigeria-toughest-league-win-away). In fact, my motivation for this post was to identify more football corruption hotspots. Alas, when it comes to home turf invincibility, it seems Nigeria are the World Cup winners.

Fifteen leagues have a negative `home_advantage_score`, meaning that visiting teams actually scored more goals than their hosts- though none was statistically significant. By some distance, the Maldives records the most negative score. Luckily, I've twice researched this beautiful archipelago and I'm aware that [all matches in the Dhiveli Premier League are played at the national stadium in Malé](https://en.wikipedia.org/wiki/Dhivehi_Premier_League#Stadiums) (much like the [Gibraltar Premier League](https://en.wikipedia.org/wiki/2017%E2%80%9318_Gibraltar_Premier_Division#Teams)). So it would make sense that there's no particular advantage gained by the home team. Libya is another interesting example. Owing to security issues, [all matches in the Libyan Premier League are played in neutral venues with no spectators present](https://en.wikipedia.org/wiki/2017%E2%80%9318_Libyan_Premier_League#Stadiums). Quite fittingly, it returned a home advantage score just off zero. Generally speaking, the leagues with near zero home advantage come from small countries (minimal inconvenience for travelling teams) with a small number of teams and they tend to share stadiums.

If you sort the `avg_goals` column, you'll see the semi-pro Canadian Soccer League is the place to be for goals (average = 4.304). But rather than sifting through that table or explaining the results with words, the most intuitive way to illustrate this type of data is with a map of world. This might also help to clarify whether there's any geographical influence on the home advantage effect. Again, I won't go into the details (an appendix can be found in the [Jupyter notebook](https://github.com/dashee87/blogScripts/blob/master/Jupyter/2018-01-10-home-advantage-in-football-leagues-around-the-world.ipynb)), but I built a map using the JavaScript library, D3. And by built I mean I adapted the code from [this post](http://bl.ocks.org/micahstubbs/8e15870eb432a21f0bc4d3d527b2d14f) and [this post](https://bl.ocks.org/mbostock/2206590). Though a little outdated now, I found [this post](https://bost.ocks.org/mike/map/) quite useful too. Finally, I think [this post](https://codepen.io/sassquad/post/rough-guide-to-building-uk-election-maps-for-d3-js) shows off quite well what you can do with maps using D3.

And here it is! The country colour represents its `home_advantage_score`. You can zoom in and out and hover over a country to reveal a nice informative overlay; use the radio buttons to switch between home advantage and goals scored. I recommend viewing it on desktop (mobile's a bit jumpy) and on Chrome (sometimes have security issues with Firefox).

{% include world_map_d3.html %}

It's not scientifically rigorous (not in academia any more, baby!), but there's evidence for some geographical trends. For example, it appears that home advantage is stronger in Africa and South America compared to Western and Central Europe, with the unstable warzones of Libya, Somalia and Paraguay (?) being notable exceptions. As for average goals, Europe boasts stonger colours compared to Africa, though South East Asia seems to be the global hotspot for goals. North America is also quite dark, but you can debate whether Canada should be coloured grey, as the best Canadian teams belong to the American soccer system.

## Conclusion

Using a [previously described model](https://dashee87.github.io/football/python/predicting-football-results-with-statistical-modelling/) and some JavaScript, this post explored the so called home advantage in football leagues all over the world (including Réunion). I  don't think it uncovered anything particularly amazing: different leagues have different properties and don't bet on the away team in the Nigerian league. You can play around with the Python code [here](https://github.com/dashee87/blogScripts/blob/master/Jupyter/2018-01-10-home-advantage-in-football-leagues-around-the-world.ipynb). Thanks for reading!
