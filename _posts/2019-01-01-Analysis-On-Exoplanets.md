---
title: "Analysis On Exoplanets"
excerpt: "Analysis of NASA data on confirmed exoplanets. Explored how the planets are discovered and the solar systems they inhabit."
layout: single
author: "Anthony Makela"
date: "01 January 2019"
---




# NASA Exoplanet Archive
	
(http://exoplanetarchive.ipac.caltech.edu/index.html)

This research has made use of the NASA Exoplanet Archive, which is operated by the California Institute of Technology, under contract with the National Aeronautics and Space Administration under the Exoplanet Exploration Program.

This source has the most current official NASA information available. Becuase the data is in flux, some other sources may be out of date, and thus they may disagree with this information. It's also possible that other sources may disagree with NASA's definitions in vague situations, and thus have slightly different data for edge cases.



``` r
# Libraries
library(dplyr)
library(ggplot2)
library(readr)
library(jsonlite)
library(scales)
```

``` r
# Data
url <- 'https://exoplanetarchive.ipac.caltech.edu/cgi-bin/nstedAPI/nph-nstedAPI?format=json&table=exoplanets&select=pl_discmethod,pl_disc,pl_facility,pl_locale,pl_rade,pl_orbper'
exo <- jsonlite::fromJSON(url, simplifyDataFrame = TRUE, flatten = TRUE)
```

### How many planets have we found orbiting other stars so far?

``` r 
exo %>%
  count()
```

``` 
[1] 3869
```

### When was the earliest discovery?

``` r 
exo %>%
  summarize(min(pl_disc))
```

``` 
[1] 1989
```

``` r
exo %>%
  group_by(pl_disc) %>%
  count() %>%
  ggplot(aes(pl_disc, n)) +
  geom_line() +
  geom_point() +
  labs(x = 'Year', y = 'Number of Exoplanets Discovered', title = 'Exoplanets Discovered yearly')
```


<div style="text-align:center" markdown="1">

![Differencing]({{ base_path }}/images/discov.png)

</div>

Having confirmation that exoplanets even exist is a relatively new idea. The first one wasn't discovered until 1989, but in the time since, the number of exoplanets we know of has exploded.

### Discovery methods

``` r
exo %>%
  group_by(pl_discmethod) %>%
  count() %>%
  ggplot(aes(pl_discmethod, n, label = n)) +
  geom_col() +
  coord_flip() +
  geom_text(hjust = -0.23, size = 4,
            position = position_dodge(width = 1)) +
  labs(x = 'Number of Planets Discovered', y = 'Planet Discovery Method', title = 'Planets Discovered by Method')
```

<div style="text-align:center" markdown="1">

![Differencing]({{ base_path }}/images/methods_disc.png)

</div>


Many methods have been proposed to find exoplanets, but only 10 have ever been successfully used (by NASA's definitions).

What the methods are:

* **Transit:** Analyzing how the star dims when the planet passes between us and the star.
* **Radial Velocity:** Using the Doppler effect to measure how much the planet's gravity makes the star wobble. Used to discover the first exoplanet in 1989.
* **Imaging:** Taking a picture of the planet.
* **Microlensing:** Detecting planet's gravity's effect on the star's light.
* **Transit Timing Variations:** Finding additional planets in a solar system through variations in an already-detected planet's transit timing.
* **Eclipse Timing Variations:** When one star in a binary star system eclipses the other, there are certain predictable points of minimum brightness. This method tracks variations from what's expected to find a planet affecting the stars' orbits and thus causing the variations.
* **Orbital Brightness Modulation:** I had difficulty finding a concrete definition for this method, but my best guess is it's similar to the radial velocity method, tracking brightness variations instead of frequency variations.
* **Pulsar Timing:** Watching for variations in pulsar pulse timing to measure how much the planet's gravity makes the star wobble. Second method to ever be successfully used.
* **Pulsation Timing Variations:** Same as the pulsar method, but for other types of pulsating variable stars.
* **Astrometry:** Observing the star physically move because of a planet's gravitational influence.


``` r
exo %>%
  ggplot(aes(pl_discmethod)) +
  geom_bar(aes(y = (..count..)/sum(..count..))) +
  geom_text(aes(y = ((..count..)/sum(..count..)), label = scales::percent((..count..)/sum(..count..))), stat = "count", vjust = -0.25) +
  scale_y_continuous(labels = percent) +
  labs(x = 'Planet Discovery Method', y = 'Percentage')
```

<div style="text-align:center" markdown="1">

![Differencing]({{ base_path }}/images/percentagge.png)

</div>

Of the 10 methods that have successfully been used to find planets, 96.5% of discoveries have been made using just two methods: transit and radial velocity.

### Who has discovered the majority of the planets?

``` r
# Number of exoplanet-discovering facilities
exo %>%
  summarize(facilities = n_distinct(pl_facility))
```

```
[1] 56
```

``` r
# Number which have discovered more than 5 planets
exo %>%
  count(pl_facility) %>%
  filter(n > 5) %>%
  summarize(facilities_5 = n_distinct(n))
```

```
[1] 22
```

``` r
# Graph facilities which have found at least 15 exoplanets
exo %>%
  group_by(pl_facility) %>%
  count(sort = TRUE) %>%
  filter(n >= 15) %>%
  ggplot(aes(reorder(pl_facility, n), n, label = n)) +
  geom_col() +
  coord_flip() +
  labs(x = 'Facility', y = 'Number of Planets Discovered', title = 'Planets Discovered by Facility (at least 15 Discovered)') +
  geom_text(hjust = -0.25, size = 4,
            position = position_dodge(width = 1))
```


<div style="text-align:center" markdown="1">

![Differencing]({{ base_path }}/images/facilities.png)

</div>

The large majority of exoplanets so far have been discovered by the Kepler space telescope, almost 13x what was discovered by the next most accomplished facility.

### Where would we be without Kepler?

The Kepler Space Telescope is the 800-pound gorilla in the room, but there's more to exoplanet discovery than just Kepler. It wasn't even launched until 2009, and there are almost 50 other facilities that have found confirmed exoplanets.

What happens if we ignore Kepler?

Note: We'll also ignore K2, the second mission of the Kepler Space Telescope, as we want to remove the influence of the entire telescope.

``` r
exo %>%
  filter(pl_facility != 'Kepler' & pl_facility != 'K2') %>%
  group_by(pl_discmethod) %>%
  ggplot(aes(pl_discmethod)) +
  geom_bar(aes(y = (..count..)/sum(..count..))) +
  geom_text(aes(y = ((..count..)/sum(..count..)), label = scales::percent((..count..)/sum(..count..))), stat = "count", vjust = -0.25) +
  scale_y_continuous(labels = percent)
```

<div style="text-align:center" markdown="1">

![Differencing]({{ base_path }}/images/woutkepler.png)

</div>

Let's find out if we were right. Here we can find the solutions: https://fivethirtyeight.com/features/alice-and-bob-fall-in-love/

" That better player wins a 12-game match about 52 percent of the time. The number of games required for those larger thresholds are, in order, **82, 248 and 773.** (Call me crazy, but I’m totally game for a two-year-long World Chess Championship.) "

And it seems that our simulation did a pretty good job.

We got the first question(What are the chances the better player wins a 12-game match?) right as you can see from above.

And here is our results for the second question, they seem to be almost exactly the same.

``` r
exp(approx(ngames_$win, log(ngames_$ngames), xout = .75)$y)
exp(approx(ngames_$win, log(ngames_$ngames), xout = .9)$y)
exp(approx(ngames_$win, log(ngames_$ngames), xout = .99)$y)
```


```
# > exp(approx(ngames_$win, log(ngames_$ngames), xout = .75)$y)
# [1] 82.17202
# > exp(approx(ngames_$win, log(ngames_$ngames), xout = .9)$y)
# [1] 249.4356
# > exp(approx(ngames_$win, log(ngames_$ngames), xout = .99)$y)
# [1] 772.3506
```


# Second

The second problem seems to be related with ping-pong balls. 

"You’re going to play a game. Like many probability games, this one involves an infinite supply of ping-pong balls. No, this game is not quite beer pong.

The balls are numbered 1 through N. There is also a group of N cups, labeled 1 through N, each of which can hold an unlimited number of ping-pong balls. The game is played in rounds. A round is composed of two phases: throwing and pruning.

During the throwing phase, the player takes balls randomly, one at a time, from the infinite supply and tosses them at the cups. The throwing phase is over when every cup contains at least one ping-pong ball.
Next comes the pruning phase. During this phase the player goes through all the balls in each cup and removes any ball whose number does not match the containing cup.
Every ball drawn has a uniformly random number, every ball lands in a uniformly random cup, and every throw lands in some cup. The game is over when, after a round is completed, there are no empty cups.

How many rounds would you expect to need to play to finish this game? How many balls would you expect to need to draw and throw to finish this game?"

Let's first create an function to simulate a game.


``` r
simulate_game <- function(N) {
  
  # Row = ball, Col = cup
  m <- matrix(0L, nrow = N, ncol = N)
  
  rounds <- 0L
  balls <- 0L
  
  while (any(colSums(m) == 0)) {
    rounds <- rounds + 1L
    while (any(colSums(m) == 0)) {
      balls <- balls + 1L
      ball <- sample.int(N, 1)
      cup <- sample.int(N, 1)
      
      m[ball, cup] <- m[ball, cup] + 1L
    }
    
    # Empty non diagonal cups 
    m[lower.tri(m)] <- 0L
    m[upper.tri(m)] <- 0L
  }
  
  list(rounds, balls)
}
```

Now we can generate all the games and create an graph. The results should be so that while the number of throws required grows roughly quadratically, the number of rounds required grows roughly linearly.

``` r
games <- crossing(N = seq(3, 25, 3),
                   game = 1:1e3) %>%
  mutate(result = map(N, simulate_game),
         rounds = map_int(result, 1),
         balls = map_int(result, 2))
```

Here we can see that the number of throws required grows quadratically. 

``` r
games %>%
  group_by(N) %>%
  summarize(rounds = mean(rounds),
            balls = mean(balls)) %>%
  ggplot(aes(N, balls)) +
  geom_line()
```

<div style="text-align:center" markdown="1">

![Differencing]({{ base_path }}/images/Rplot01.png)

</div>

And this plot illustrates how the expected number of rounds increases as the number of cups (and the number of numbers on the balls) increases — **roughly linearly**

``` r
games %>%
  group_by(N) %>%
  summarize(rounds = mean(rounds),
            balls = mean(balls)) %>%
  ggplot(aes(N, rounds)) +
  geom_line()
```

<div style="text-align:center" markdown="1">

![Differencing]({{ base_path }}/images/linear.png)

</div>


### Summary

We used programmatic, simulation-based approaches and managed to get pretty good results. Although we could have used mathematical approaches and get the same results, the objective of this post was to illustrate an Monte Carlo Simulation examples in R and see if we can solve the puzzles with that approach. Here is an mathematical approach from Laurent Lessard https://laurentlessard.com/bookproofs/beer-pong/ 

Lessard uses a Markov chain, a stochastic model describing a sequence of events that depend on the current state of events — such as the balls currently in our cups. And from there he invokes a holy Riddler trinity: absorbing states and limiting distributions and nilpotent matrices.
