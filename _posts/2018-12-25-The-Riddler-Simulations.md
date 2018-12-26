---
title: "Monte Carlo Simulation Examples for 'The Riddler' Puzzles "
excerpt: "The Riddler offers problems related to: math, logic and probability. In this post we take a look at 2 of those problems and try to solve them using Monte Carlo simulation "
layout: single
author: "Anthony Makela"
date: "26 December 2018"
---



There are two types of problems: Riddler Express and Riddler Classic. We're going to start with the Riddler Express and then move onto the second one. Also here is a link for the post at https://fivethirtyeight.com/features/the-riddler-just-had-to-go-and-reinvent-beer-pong/

# Riddler Express
	
So the first problem seems to be related with chess. 

Disclaimer: The Championships were already and Magnus Carlsen won!

"The World Chess Championship is underway. It is a 12-game match between the world’s top two grandmasters. Many chess fans feel that 12 games is far too short for a biennial world championship match, allowing too much variance.

Say **one of the players is better than his opponent to the degree that he wins 20 percent of all games, loses 15 percent of games and that 65 percent of games are drawn.** Wins at this match are worth 1 point, draws a half-point for each player, and losses 0 points. In a 12-game match, the first player to 6.5 points wins.

What are the chances the better player wins a 12-game match? How many games would a match have to be in order to give the better player a 75 chance of winning the match outright? A 90 percent chance? A 99 percent chance?"



``` r
# Tidyverse
library(tidyverse)
```

### What are the chances the better player wins a 12-game match?

We are sampling from 3 options here(1 = win, 0 = lose, .5 = draw). The respective weighted probabilities are in the vector c(.2, .15, .65). Then we're getting the players score in every "match" and plotting an histogram from them.

``` r
scores <- crossing(trials = 1:1e5,
         game = 1:12) %>%
  mutate(result = sample(c(1, 0, .5), n(), replace = TRUE, prob = c(.2, .15, .65))) %>%
  group_by(trials) %>%
  summarize(score = sum(result))
```

``` r 
scores %>%
  ggplot(aes(score)) +
  geom_histogram(binwidth = .25, color="blue", fill=rgb(0.1,0.4,0.5,0.7)) +
  geom_vline(color = 'red', xintercept = 6.5)
```

<div style="text-align:center" markdown="1">

![Differencing]({{ base_path }}/images/Rplot.png)

</div>

We can also simply find out how often it's above 6.5. And we see that the player wins 52% of the time.

``` r
scores %>%
  summarize(mean(score >= 6.5))
```

```
# A tibble: 1 x 1
#  `mean(scores >= 6.5)`
#                  <dbl>
# 1                 0.520

```

### How many games would a match have to be in order to give the better player a 75 chance of winning the match outright? A 90 percent chance? A 99 percent chance?

Here we are simulating 50,000 trials with logarithmically increasing ngames to try and get solid estimates. Then we will create an line plot and scale x to be on a logarithmic scale because that usually helps to detect the trend more thoroughly.

``` r
ngames_ <- crossing(trials = 1:5e4,
         ngames = round(12 * 2 ^ seq(0, 7, .5))) %>%
  unnest(game = map(ngames, seq_len)) %>%
  mutate(result = sample(c(1, 0, .5), n(), replace= TRUE, prob = c(.2, .15, .65))) %>%
  group_by(ngames, trials) %>%
  summarize(score = sum(result)) %>%
  summarize(win = mean(score > ngames / 2))
```


``` r
ngames_ %>%
  ggplot(aes(ngames, win)) +
  geom_line(color = rgb(0.1,0.4,0.5,0.7)) +
  geom_point() +
  scale_x_log10() +
  scale_y_continuous(labels = scales::percent_format()) +
  labs(x = 'Number of games',
       y = 'Probability for the better player to win')
```

<div style="text-align:center" markdown="1">

![Differencing]({{ base_path }}/images/logplot.png)

</div>

Let's find out if we were right. Here we can find the solutions: https://fivethirtyeight.com/features/alice-and-bob-fall-in-love/

" That better player wins a 12-game match about 52 percent of the time. The number of games required for those larger thresholds are, in order, 82, 248 and 773. (Call me crazy, but I’m totally game for a two-year-long World Chess Championship.) "

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


# Riddler Classic

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

![Differencing]({{ base_path }}/images/Rplot1.png)

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

We used several datasets containing information about traffic accidents in Finland between 2008 and 2017. After some EDA and time series theory, we built an ARIMA model to forecast the number of accidents in 2018. The most interesting part of any predictive model is determining how well it performed against the actual data. Sadly, we cannot do this until the 2018 data becomes available. Also when data from 2018 is released we can start forecasting 2019.
