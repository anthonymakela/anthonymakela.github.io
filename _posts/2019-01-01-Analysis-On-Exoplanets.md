---
title: "Analysis On Exoplanets"
excerpt: "Analysis of NASA data on confirmed exoplanets. Explored how the planets are discovered and the solar systems they inhabit."
layout: single
author: "Anthony Makela"
date: "01 January 2019"
---




# NASA Exoplanet Archive
	
(http://exoplanetarchive.ipac.caltech.edu/index.html)

This research has made use of the NASA Exoplanet Archive, which is operated by the California Institute of Technology.

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
url <- 'https://exoplanetarchive.ipac.caltech.edu/cgi-bin/nstedAPI/nph-nstedAPI?format=json&table=exoplanets&select=pl_discmethod,pl_disc,pl_facility,pl_locale,pl_rade,pl_orbper,pl_bmassj,pl_radj,pl_orbsmax'
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

![Differencing]({{ base_path }}/images/num_discoveries.png)

</div>

Having evidence that exoplanets even exist is a relatively new idea. The first one wasn’t discovered until 1989, but in the time since the number of exoplanets we know of has exploded.

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


Numerous methods have been suggested to find exoplanets, but only 10 have ever been successfully used (by NASA’s definitions).

The methods are described here:

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

Of the 10 methods that have successfully been used to find planets, 96% of discoveries are made using just two methods: transit and radial velocity.

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

The Kepler Space Telescope is the top of its class, but there's more to exoplanet discovery than just Kepler. It wasn't even launched until 2009, and there are almost 50 other facilities that have found confirmed exoplanets.

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

Turns out Kepler is a massive leader for the transit method. Without Kepler in the picture, transit is no longer the most successful method of planetary discovery by a long shot. Radial velocity is now the most productive, with fully twice the success record of transit.

This could be because radial velocity is the oldest successful method, and thus has had the most time to rack up confirmed finds. Radial velocity has been used successfully since 1989, whereas transit didn't complete its first find until 2002.

``` r
exo %>%
  filter(pl_facility != 'Kepler' & pl_facility != 'K2') %>%
  group_by(pl_discmethod) %>%
  count(sort = TRUE) %>%
  ggplot(aes(reorder(pl_discmethod, n), n, label = n)) +
  geom_col() +
  coord_flip() +
  labs(x = 'Planet Discovery Method', y = 'Number of Planets Discovered', title = 'Planets Discovered by Method - Without Kepler') +
  geom_text(hjust = -0.5, size = 4,
                position = position_dodge(width = 1))
```

<div style="text-align:center" markdown="1">

![Differencing]({{ base_path }}/images/keplerw.png)

</div>

Since two methods are now completely missing, it appears Kepler is the only facility to have ever successfully used the transit timing variations or orbital brightness modulation methods to discover a planet.

### Are certain methods more successful at discovering particular types of planets?

``` r
exo %>%
  filter(!is.na(pl_rade)) %>%
  group_by(pl_discmethod) %>%
  summarize(mean_rad = mean(pl_rade)) %>%
  ggplot(aes(reorder(pl_discmethod, mean_rad), mean_rad, label = round(mean_rad, 2))) +
  geom_col() +
  coord_flip() +
  geom_text(hjust = -0.2, size = 3.5,
            position = position_dodge(width = 1)) +
  labs(x = 'Average Radius of Discovered Planets (Number of Earths)', y = 'Planet Discovery Method', title = 'Planet Radius by Discovery Method')
```

<div style="text-align:center" markdown="1">

![Differencing]({{ base_path }}/images/avg_rad.png)

</div>


As expected, imaging is best at discovering larger planets.

Interestingly, transit generally discovers larger planets than transit timing variations. It's possible that once the first planet is discovered helping find smaller planets.

Note: Some methods are missing because no radius data is available for the planets they've discovered.

``` r
exo %>%
  filter(!is.na(pl_rade)) %>%
  group_by(pl_locale) %>%
  summarize(mean_rad = mean(pl_rade)) %>%
  ggplot(aes(reorder(pl_locale, mean_rad), mean_rad, label = round(mean_rad, 2))) +
  geom_col() +
  coord_flip() +
  geom_text(hjust = -0.2, size = 3.5,
            position = position_dodge(width = 1)) +
  labs(x = 'Average Radius of Discovered Planets (Number of Earths)', y = 'Facility Locale', title = 'Planet Radius by Locale')
```

<div style="text-align:center" markdown="1">

![Differencing]({{ base_path }}/images/plot_locale.png)

</div>

Also not surprisingly, space telescopes are better at discovering smaller planets than ground-based telescopes. Because space telescopes avoid atmosphere-induced errors, they're more precise, accurate, and consistent than ground-based telescopes.

### Mass of the Exoplanets

There is plenty of extremely large planets! But still, the largest amount has approximately the same mass as Earth.

``` r
exo %>%
  filter(pl_bmassj < 10) %>%
  ggplot(aes(pl_bmassj*317.83)) +
  geom_histogram(binwidth = 60) +
  geom_vline(aes(xintercept = 1), linetype="dashed", size=.5, color = '#80cdc1') +
  geom_vline(aes(xintercept = 317.83), linetype = 'dashed', size = .5, color = '#80cdc1') +
  geom_text(aes(x = 1, label = "Earth", y = 300), color = '#80cdc1', vjust = 2.2) +
  geom_text(aes(x = 317.83, label = "Jupiter", y = 250), color = '#80cdc1', vjust = 3.0) +
  labs(x = expression(Earth~mass~(M['\u2295'])), title = 'Mass of the Exoplanets')
```

<div style="text-align:center" markdown="1">

![Differencing]({{ base_path }}/images/mass_plot.png)

</div>

I would like to approximate the gravity of these planets. Gravity depends on the mass and density of the planet, unfortunately, we don’t have density available at our dataset. But if we assume that the planets are perfectly spherical, we can derive their density from their radius and mass.

### Density

$ p = {m \over V} $

``` r
exo$density = (1.898*10^27*1000*exo$pl_bmassj)/((4/3)*pi*(exo$pl_radj*69911*100000)^3)

exo %>%
  filter(density < 90) %>%
  ggplot(aes(density)) +
  geom_histogram(binwidth = 3) +
  geom_vline(aes(xintercept = 5.51), linetype = 'dashed', size = .5, color = '#80cdc1') +
  geom_vline(aes(xintercept = 1.33), linetype = 'dashed', size = .5, color = '#80cdc1') +
  geom_text(aes(x = 5.51, label = "Earth", y = 300), color = '#80cdc1', vjust = 2.2) +
  geom_text(aes(x = 1.33, label = "Jupiter", y = 350), color = '#80cdc1', vjust = 2.2) +
  labs(x = expression(Planet~Density~(g/cm^{3})), title = 'Density of the Exoplanets')
```

<div style="text-align:center" markdown="1">

![Differencing]({{ base_path }}/images/planet_density.png)

</div>

# Solar Systems

``` r
url_solar <- 'https://exoplanetarchive.ipac.caltech.edu/cgi-bin/nstedAPI/nph-nstedAPI?format=json&&table=exoplanets&select=pl_cbflag,pl_pnum,pl_masse'
solar <- jsonlite::fromJSON(url_solar, simplifyDataFrame = TRUE, flatten = TRUE)
```

### How many planets orbit multiple stars?

In a binary star system, two stars orbit each other. A circumbinary planet is a planet orbiting around both stars in a binary star system.

``` r
solar %>%
  group_by(pl_cbflag) %>%
  mutate(pl_cbflag_recode = recode(pl_cbflag, 
                    "0" = "Not Tatooine", 
                    "1" = "Circumbinary")) %>%
  ggplot(aes(pl_cbflag_recode)) +
  geom_bar(aes(y = (..count..)/sum(..count..))) +
  geom_text(aes(y = ((..count..)/sum(..count..)), label = scales::percent((..count..)/sum(..count..))), stat = "count", vjust = -0.25) +
  scale_y_continuous(labels = percent) +
  labs(x = 'Circumbinary Flag', y = 'Percentage')
```

<div style="text-align:center" markdown="1">

![Differencing]({{ base_path }}/images/cbflag.png)

</div>

Due to a lack of granularity in the data set, it's unclear whether the non-circumbinary planets orbit a single star, are in a binary star system that isn't circumbinary, or orbit even more than 2 stars.

Less than 1% of planets discovered so far are circumbinary. That is, we know of 23 planets currently orbiting binary star systems, and one could potentially be Tatooine. It remains to be seen how many have pod racing.

All jokes aside, it's pretty amazing that examples of this even exist in our galaxy!

``` r
# How many planets are in each solar system?
solar %>%
  summarize(mean_num_planets = mean(pl_pnum))
```

```
[1] 1.77
```

``` r
# Percentage of solar systems with multiple planets
solar %>%
  filter(pl_pnum > 1) %>%
  count(pl_pnum) %>%
  summarize(multiple_planets_perc = sum(n) / nrow(solar) * 100)
```

```
[1] 42.1
```

``` r
solar %>%
  group_by(pl_pnum) %>%
  count(pl_pnum) %>%
  ggplot(aes(as.factor(pl_pnum), n, label = n)) +
  geom_col() +
  geom_text(vjust = -0.25, size = 3.5,
            position = position_dodge(width = 1)) +
  labs(x = 'Number of Planets', y = 'Frequency', title = 'Number of Planets in Solar Systems')
```

<div style="text-align:center" markdown="1">

![Differencing]({{ base_path }}/images/numsolsys.png)

</div>

Almost half of solar systems have multiple planets!

The most we've found in another solar system so far is 8, which is still fewer than the number in our own system. It's likely that this number is low, considering our ability to detect small planets is still limited, and many of the planets in our own system would be too small to discover yet in those distant systems.

Because new planets are constantly being discovered, it's likely that there are many planets yet undiscovered in these solar systems. If true, this would skew the data even more in favor of multiple planets. Considering so many solar systems have numerous planets already, it's likely the majority of systems had multiple planets.

### Summary


