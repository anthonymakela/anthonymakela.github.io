---
title: "Traffic Accident Analysis"
excerpt: "This post looks at road accidents in Finland between 2008 and 2017 and investigates whether we can forecast the number of accidents in 2018."
layout: single
author: "Anthony Makela"
date: "04 December 2018"
---



It's soon Winter again and the  $$ H_{0} $$  states that the accident severity and car accidents will rise. The objective of this analysis is to explore and gain a better understanding of this phenomena and figure out if it's actually the case. We will also explore and gain a better understanding of some of the factors that affect the likelihood of the crashes.

### Preprocessing

All of the data used in this analysis is from https://www.avoindata.fi. They have some really interesting data that they make available to public.

``` r
# Libraries
suppressWarnings(suppressMessages(library(ggplot2)))
suppressWarnings(suppressMessages(library(readr))) 
suppressWarnings(suppressMessages(library(data.table)))
suppressWarnings(suppressMessages(library(MASS)))
suppressWarnings(suppressMessages(library(DMwR)))
suppressWarnings(suppressMessages(library(dplyr)))
suppressWarnings(suppressMessages(library(lubridate)))
suppressWarnings(suppressMessages(library(zoo)))
suppressWarnings(suppressMessages(library(repr)))
suppressWarnings(suppressMessages(library(gridExtra)))
suppressWarnings(suppressMessages(library(memisc)))
suppressWarnings(suppressMessages(library(plotly)))
suppressWarnings(suppressMessages(library(forecast)))
suppressWarnings(suppressMessages(library(IRdisplay)))


# ggplot options
options(repr.plot.width = 6, repr.plot.height = 4)
```



``` r
# Read the data(2008-2017)
accidents_2017 <- data.table(read.csv("~/Downloads/Tieliikenne/onnettomuudet_2017.csv", sep = ','))
accidents_2016 <- data.table(read.csv("~/Downloads/Tieliikenne/onnettomuudet_2016.csv", sep = ','))
accidents_2015 <- data.table(read.csv("~/Downloads/Tieliikenne/onnettomuudet_2015.csv", sep = ','))
accidents_2014 <- data.table(read.csv("~/Downloads/Tieliikenne/onnettomuudet_2014.csv", sep = ','))
accidents_2013 <- data.table(read.csv("~/Downloads/Tieliikenne/onnettomuudet_2013.csv", sep = ','))
accidents_2012 <- data.table(read.csv("~/Downloads/Tieliikenne/onnettomuudet_2012.csv", sep = ','))
accidents_2011 <- data.table(read.csv("~/Downloads/Tieliikenne/onnettomuudet_2011.csv", sep = ','))
accidents_2010 <- data.table(read.csv("~/Downloads/Tieliikenne/onnettomuudet_2010.csv", sep = ','))
accidents_2009 <- data.table(read.csv("~/Downloads/Tieliikenne/onnettomuudet_2009.csv", sep = ','))
accidents_2008 <- data.table(read.csv("~/Downloads/Tieliikenne/onnettomuudet_2008.csv", sep = ','))
```

``` r 
# Row bind dataframes
accidents_ <- rbind(accidents_2017, accidents_2016, accidents_2015, accidents_2014, accidents_2013, accidents_2012, accidents_2011, accidents_2010, accidents_2009, accidents_2008)
```

Since in Finland we also have some special alphabetical characters, we have to do just a tiny bit of string manipulation here as well.

``` r
# Replace Finnish letters
names(accidents_2017) <- gsub(x = names(accidents_2017), pattern = "\\.", replacement = "a")
accidents_$Kuntasel <- gsub(x = accidents_$Kuntasel, pattern = "\\\344", replacement = "a")
accidents_$Kuntasel <- gsub(x = accidents_$Kuntasel, pattern = "\\\366", replacement = "o")
accidents_$Kuntasel <- gsub(x = accidents_$Kuntasel, pattern = "\\\304", replacement = "aa")
accidents_$Valsel <- gsub(x = accidents_$Valsel, pattern = "\\\344", replacement = "a")
```

``` r
# Remove unnecessary columns
accidents_$Aet = NULL
accidents_$Liittyvtie = NULL
accidents_$Kvl = NULL
accidents_$Raskaskvl = NULL
accidents_$Tienlev = NULL
accidents_$X = NULL
accidents_$Y = NULL
accidents_$Lahliittie = NULL
accidents_$Suuntlkm = NULL
accidents_$Paallyslev = NULL
accidents_$Nakos150 = NULL
accidents_$Nakos300 = NULL
accidents_$Nakos460 = NULL
accidents_$Runkotie = NULL
```


``` r
# Remove explanations (could be done more efficiently)
accidents_$Tienpitsel = NULL
accidents_$Vakavuus = NULL
accidents_$Elynimi = NULL
accidents_$Piirinimi = NULL
accidents_$Ontyypsel = NULL
accidents_$Onlksel = NULL
accidents_$Taajamasel = NULL
accidents_$Pintasel = NULL
accidents_$Saasel = NULL
accidents_$Onnpaiksel = NULL
accidents_$Maakuntsel = NULL
accidents_$Noplajisel = NULL
accidents_$Mo_molsel = NULL
accidents_$Toimlksel = NULL
accidents_$Paallsel = NULL
accidents_$Risteyssel = NULL
accidents_$Rautatsel = NULL
accidents_$Talvhoitsel = NULL
accidents_$Tietyypsel = NULL
accidents_$Tienverkse = NULL
accidents_$Maankaytse = NULL
accidents_$Valoohjsel = NULL
accidents_$Lisakaisse = NULL
accidents_$Solmutyyps = NULL
accidents_$Liitlksel = NULL
accidents_$Toimpidsel = NULL
accidents_$Valomsel = NULL
accidents_$Poikleikse = NULL
accidents_$Paallksel = NULL
```

### Missing values

While analyzing the data some missing values were located. The missing values can be found in the variables "Tie", "Aosa", "Ajr" and "Lampatila". The first ones wont cause any problems since we're not going to use them however, the latter one caught my interest and there would be an opportunity to investigate it more. To do this we could use some imputation methods to fill the missing values, I'll quickly introduce here the KNN method which is found to be one of the most efficient methods.

``` r
# Count NA's
na_count <- sapply(accidents_, function(y) sum(length(which(is.na(y)))))
show(na_count)
```


    ##         Tie    Aosa   Ajr    
    ##       106274   106543 120955
    ##
    ##       Kuntasel Lampatila
    ##          6       6537


### KNN imputation for missing values

The assumption behind using KNN for missing values is that a point value can be approximated by the values of the  $$ {k} $$ points that are closest to it, based on other variables. Essentially, two vectors that are far apart based on the distance function are less likely than two closely situated vectors to have a similar output value. The most frequently used distance metrics are the Euclidean distance metric or the Pearson correlation metric. Let $$ {X}_{i}$$ , $$ {i} $$ = 1, …, $$ {n} $$ be independent and identically distributed (iid) with mean $$ {µ} $$ $$ {X} $$ and standard deviation $$ {σ} $$ $$ {X} $$, and $$ {Y}_{i} $$, $$ {i} $$ = 1, …, $$ {n} $$ be iid with mean $$ {µ} $$ $$ {Y} $$ and standard deviation $$ {σ} $$ $$ {Y} $$. The Euclidean distance between the two sample vectors $$ {x} $$ = $$ x_{i} $$ 1, …, $$ {x} $$ $$ {n} $$ and $$ {y} $$ = $$ {y} $$ 1, …, $$ {y} $$ $${n} $$ is defined as follows:

$$d_{E}(x, y) = {\sqrt{\sum_{i=1}^N (x_i-y_i)^2}}$$


``` r
# knnImputation()
```

### Let's first find out the number #1 cause of deaths.

The factors are defined at avoindata.fi, but i'll describe them here as well.

1 – Yksittäisonnettomuus

2 – Kääntymisonnettomuus

3 – Ohitusonnettomuus

4 – Risteämisonnettomuus

5 – Kohtaamisonnettomuus

6 – Peräänajo-onnettomuus

7 – Mopedionnettomuus

8 – Polkupyöräonnettomuus

9 – Jalankulkijaonnettomuus

10 – Hirvionnettomuus

11 – Peura- tai kaurisonnettomuus

12 – Muu eläinonnettomuus

13 – Muu onnettomuus

``` r
# Number #1 cause of deaths
cause_ <- accidents_ %>%
    group_by(Onluokka) %>%
    summarize(Kuolleet = sum(Kuolleet))

ggplot(cause_, aes(x = as.factor(Onluokka), y = Kuolleet)) +
  geom_bar(stat = "identity", color = "blue", fill = rgb(0.1,0.4,0.5,0.7)) + 
  labs(x = "Onnettomuusluokka", y = "Maara (Kuolleet)")
```

<div style="text-align:center" markdown="1">

![Differencing]({{ base_path }}/images/cause_.png)

</div>

### Number of deaths yearly

Here we can observe that the most of the deaths happened in 2011. What might be the cause of this?

``` r
# Number of deaths by year
death_y <- accidents_ %>%
    group_by(Vuosi) %>%
    summarize(Kuolleet = sum(Kuolleet))

ggplot(death_y, aes(x = as.factor(Vuosi), y = Kuolleet)) +
  geom_line(size = .5, alpha = 0.7, color = "mediumseagreen", group = 1) + 
  geom_point(size = 0.8) +
  labs(x = "Vuosi", y = "Maara (Kuolleet)")
```

<div style="text-align:center" markdown="1">

![Differencing]({{ base_path }}/images/death_y.png)

</div>

### Number of deaths by weekday

We can see that the deaths are more common on the weekends (Friday and Saturday). This doesn’t come as a surprise since on the weekends there’s more likely also alcohol involved. Too bad we don’t have access to that kind of data to investigate it. On the contrary, the amount of fatal accidents seems to be the lowest on Sundays.

``` r
# Number of deaths by weekday
death_weekday <- accidents_ %>%
    group_by(Vkpv) %>%
    summarize(Kuolleet = sum(Kuolleet))

death_weekday = death_weekday[-8, ]

ggplot(death_weekday, aes(x = as.factor(Vkpv), y = Kuolleet)) +
  geom_bar(stat="identity", color="blue", fill=rgb(0.1,0.4,0.5,0.7)) + 
  labs(x="Paivamaara", y="Maara (Kuolleet)")
```

<div style="text-align:center" markdown="1">

![Differencing]({{ base_path }}/images/death_weekday.png)

</div>

### Number of deaths hourly

Most of the deaths occur between 12-18 and the highest amount at 16. This might be due to the fact that a large number of people are leaving work around that time and the traffic periods are at their peak.

``` r
death_hour <- accidents_ %>%
  group_by(Tunti) %>%
  summarize(Kuolleet = sum(Kuolleet)) %>%
  arrange(desc(Kuolleet))

death_hour = death_hour[-nrow(death_hour), ]

ggplot(death_hour, aes(x = as.factor(Tunti), y = Kuolleet)) +
  geom_bar(stat = "identity", color = "blue", fill = rgb(0.1,0.4,0.5,0.7)) + 
  labs(x = "Tunti", y = "Maara (Kuolleet)")
```

<div style="text-align:center" markdown="1">

![Differencing]({{ base_path }}/images/death_hour.png)

</div>

### Number of deaths in largest cities of Finland

It looks like the most deaths occur in Helsinki and Oulu. Helsinki doesn’t come as a surprise since it’s the capital of Finland and has the most population. Oulu, on the other hand, is only the 4th most populated city and still, it has roughly about 45% difference compared to other cities.

``` r
# Number of deaths by largest cities in Finland
largest_cities <- c('Helsinki', 'Espoo', 'Vantaa', 'Tampere', 'Turku', 'Oulu', 'Jyvaskyla', 'Lahti')

death_c <- accidents_ %>%
  filter(Kuntasel %in% largest_cities)  %>%
  group_by(Kuntasel) %>%
  summarize(Kuolleet = sum(Kuolleet)) %>%
  arrange(desc(Kuolleet))

ggplot(death_c, aes(x = as.factor(Kuntasel), y = Kuolleet)) +
  geom_bar(stat = "identity", color = "blue", fill = rgb(0.1,0.4,0.5,0.7)) + 
  labs(x = "Kaupungit", y = "Maara (Kuolleet)")
```

<div style="text-align:center" markdown="1">

![Differencing]({{ base_path }}/images/death_city.png)

</div>

### Number of deaths by different weathers

Here we compare the deaths to different weather conditions. This plot doesn't seem to be that informative since the weather is usually either 1 or 2.

1 – Kirkas

2 – Pilvipouta

3 – Sumu

4 – Vesisade

5 – Lumisade

6 – Räntäsade

``` r
# Number of deaths by different weathers
death_w <- accidents_ %>%
  group_by(Saa) %>%
  summarize(Kuolleet = sum(Kuolleet)) %>%
  arrange(desc(Kuolleet))

death_w = death_w[-4, ]

ggplot(death_w, aes(x = as.factor(Saa), y = Kuolleet)) +
  geom_bar(stat = "identity", color = "blue", fill = rgb(0.1,0.4,0.5,0.7)) + 
  labs(x = "Saa", y = "Maara (Kuolleet)")
```

<div style="text-align:center" markdown="1">

![Differencing]({{ base_path }}/images/death_w.png)

</div>

### Number of deaths depending on Winter maintenance

This was rather alarming. There seems to be a bit too many deaths with the factor #2. Im not sure how they measure " tingitään öisin " but they probably should do something about it.

-1 - Ei arvoa

0 - Liukkaudentorjunta ilman toimenpideaikaa

1 - Normaalisti aina paljaana

2 - Normaalisti paljaana (tingitään öisin)

3 - Osan talvea lumipintaisena

4 - Taajamaassa

5 - 2-luokka, pääosin lumipintainen

6 - Hiekoitus vain pahimmissa tilanteissa

7 - Hyvin hoidettu kevyen liikenteen väylä

8 - Merkitykseltään vähäisempi kev. liik. v

``` r
# Winter maintenance
death_wc <- accidents_ %>%
  group_by(Talvhoitlk) %>%
  summarize(Kuolleet = sum(Kuolleet)) %>%
  arrange(desc(Kuolleet))

death_wc = death_wc[-1, ]

ggplot(death_wc, aes(x = as.factor(Talvhoitlk), y = Kuolleet)) +
  geom_bar(stat = "identity", color = "blue", fill = rgb(0.1,0.4,0.5,0.7)) + 
  labs(x = "Talvihoitoluokka", y = "Maara (Kuolleet)")
```

<div style="text-align:center" markdown="1">

![Differencing]({{ base_path }}/images/death_wc.png)

</div>

### Number of injuries depending on Winter maintenance

The plot above was something that really caught my attention. I find it pretty disturbing that we’re losing lives due to “ bargaining “. Here I'm plotting the same graph but instead of all outcomes that lead dead, we’re looking at all the accidents that lead to injuries. Again we can see that the roads that aren’t maintained are causing lots of potential harm and have a substantial risk of fatality.

``` r
acc_wc <- accidents_ %>%
  group_by(Talvhoitlk) %>%
  summarize(acc = sum(Loukkaant))

acc_wc = acc_wc[-1, ]

ggplot(acc_wc, aes(x = as.factor(Talvhoitlk), y = acc)) +
  geom_bar(stat = "identity", color = "blue", fill = rgb(0.1,0.4,0.5,0.7)) + 
  labs(x = "Talvihoitoluokka", y = "Maara (Loukkaantuneet)")
```

<div style="text-align:center" markdown="1">

![Differencing]({{ base_path }}/images/acc_wc.png)

</div>

### Number of deaths monthly

Although the common assumption would be that most of the accidents that lead to death would occur in the Winter season, however, this doesn't seem to be the case. The graph displays that most of the deaths actually happen during summer time. Perhaps the accidents are more serious in the summer and that’s why the consequences are worse.

``` r
accidents_$Paiva = as.yearmon(accidents_$Paiva, format = "%d.%m.%Y")

death_yearlymon <- accidents_ %>%
  group_by(as.yearmon(Paiva, format = "%d/%m/%Y")) %>%
  summarize(Kuolleet = sum(Kuolleet))
  colnames(death_yearlymon)[1]="YearMonth"

format_axis <- function(plottitle,size=18,colour="black"){
  list(
    title = plottitle,
    titlefont = list(
      size = size,
      color = colour))}

line_list <- list()
for(i in 1:length(unique(year(accidents_$Paiva)))){
  line_list[[i]]=list(type      = "line",
                      line      = list(color = "black", dash="dashdot"),
                      opacity   = 0.3,
                      x0        = unique(year(accidents_$Paiva))[i],
                      x1        = unique(year(accidents_$Paiva))[i],
                      xref      = "x",
                      y0        = min(death_yearlymon$Kuolleet),
                      y1        = max(death_yearlymon$Kuolleet),
                      yref      = "y")
}

plot_ly(death_yearlymon, x = ~ YearMonth, y = ~ Kuolleet, type = "scatter", 
        mode = "lines", text = sapply(death_yearlymon$YearMonth, toString),
        hoverinfo = "text+y") %>% layout(shapes = line_list) %>%  
  layout(xaxis = format_axis("Vuosi"), yaxis = format_axis("Maara (Kuolleet)"),
         title = "Kuolleiden maara kuukausittain (2008-2017)")
```

<iframe  src="https://plot.ly/~anthonymakela/6/#/.embed?link=false" width="100%" height="500" frameborder="no" scrolling="no"></iframe>

### Number of injuries monthly

We can observe that also the accidents that lead to injuries are more likely to happen during the summer time. 

``` r
inj_yearlymon <- accidents_ %>%
  group_by(as.yearmon(Paiva, format="%d/%m/%Y")) %>%
  summarize(Loukkaant = sum(Loukkaant))
  colnames(inj_yearlymon)[1]="YearMonth"

format_axis <- function(plottitle,size=18,colour="black"){
  list(
    title = plottitle,
    titlefont = list(
      size = size,
      color = colour))}

line_list_inj <- list()
for(i in 1:length(unique(year(accidents_$Paiva)))){
  line_list_inj[[i]]=list(type      = "line",
                      line      = list(color = "black", dash="dashdot"),
                      opacity   = 0.3,
                      x0        = unique(year(accidents_$Paiva))[i],
                      x1        = unique(year(accidents_$Paiva))[i],
                      xref      = "x",
                      y0        = min(inj_yearlymon$Loukkaant),
                      y1        = max(inj_yearlymon$Loukkaant),
                      yref      = "y")
}

plot_ly(inj_yearlymon, x = ~ YearMonth, y = ~ Loukkaant, type = "scatter", 
        mode = "lines", text = sapply(inj_yearlymon$YearMonth, toString),
        hoverinfo = "text+y") %>% layout(shapes = line_list_inj) %>%  
  layout(xaxis = format_axis("Vuosi"),yaxis = format_axis("Maara (Loukkaantuneet)"),
         title = "Loukkaantuneiden maara kuukausittain (2008-2017)")
```

<iframe  src="https://plot.ly/~anthonymakela/8/#/.embed?link=false" width="100%" height="500" frameborder="no" scrolling="no"></iframe>

### Number of accidents monthly

The good news is that it seems that the number of accidents has been slowly declining. You might also detect seasonal behavior within the numbers. April typically has the least number of accidents, while November and December is the worst month for accidents. This is rather different from the previous plot where we looked at the number of actual fatalities/deaths. The deaths were more common in the summertime. So the time series appears to be composed of a trend and cyclical/seasonal component.

``` r
acc_yearlymon <- accidents_ %>%
  group_by(as.yearmon(Paiva, format="%d/%m/%Y")) %>%
  summarize(acc = n())
  colnames(acc_yearlymon)[1]="YearMonth"

line_list_mon <- list()
for(i in 1:length(unique(year(accidents_$Paiva)))){
  line_list_mon[[i]]=list(type      = "line",
                      line      = list(color = "black", dash = "dashdot"),
                      opacity   = 0.3,
                      x0        = unique(year(accidents_$Paiva))[i],
                      x1        = unique(year(accidents_$Paiva))[i],
                      xref      = "x",
                      y0        = min(acc_yearlymon$acc),
                      y1        = max(acc_yearlymon$acc),
                      yref      = "y")
}

plot_ly(acc_yearlymon, x = ~ YearMonth, y = ~ acc, type = "scatter", 
        mode = "lines", text = sapply(acc_yearlymon$YearMonth, toString),
        hoverinfo = "text+y") %>% layout(shapes = line_list_mon) %>%  
  layout(xaxis = format_axis("Vuosi"),yaxis = format_axis("Maara (Onnettomuudet)"),
         title = "Onnettomuuksien maara kuukausittain (2008-2017)")
```

<iframe  src="https://plot.ly/~anthonymakela/10/#/.embed?link=false" width="100%" height="500" frameborder="no" scrolling="no"></iframe>

### Decompose

We should be able to decompose this time series, if we include a noise term to account for random monthly variations.
We’ll opt for a multiplicative model (number deaths is the product of its seasonal/trend/noise components) and use Seasonal and Trend decomposition using Loess (STL) The theory behind time series decomposition is well described here.

``` r
decomp_accs_ts <- stl(ts(log(acc_yearlymon$acc), frequency = 12, start = 2008), s.window = "periodic")
decomp_accs_ts$time.series <- exp(decomp_accs_ts$time.series)

plot_ly_decomp <- function(time_series){
  ts_df <- as.data.frame(time_series$time.series) %>% 
    mutate(date = as.yearmon(time(time_series$time.series))) %>% 
    tidyr::gather(variable, value, -date) %>% transform(id = as.integer(factor(variable)))
  seas_plotly <- plot_ly(filter(ts_df, variable == "seasonal"),
                         x = ~ date, y = ~ value, colors = "Dark2", name = "seasonal", 
                         type = "scatter", mode = "lines",
                         text = unique(sapply(ts_df$date,toString)),hoverinfo = "text + y") %>%
    layout(xaxis = list(title = "", showticklabels = FALSE))
  remain_plotly <- plot_ly(filter(ts_df, variable == "remainder"),
                           x = ~ date, y = ~ value, colors = "Dark2", name = "noise", 
                           type = "scatter", mode = "lines",
                           text = unique(sapply(ts_df$date,toString)),hoverinfo = "text + y") %>%
    add_trace(x = ~date, y = 1, mode = "lines", showlegend = FALSE, line = list(
      color = "gray",
      dash = "dashed"                                
    )) %>%
    layout(xaxis = list(title = ""))
  trend_plotly <- plot_ly(filter(ts_df, variable == "trend"),
                          x = ~ date, y = ~ value, colors = "Dark2", name = "trend", 
                          type = "scatter", mode = "lines",
                          text = unique(sapply(ts_df$date,toString)), hoverinfo = "text + y") %>%
    layout(xaxis = list(title = "", showticklabels = FALSE))
  data_plotly <- plot_ly(group_by(ts_df,date) %>% summarize(value = prod(value)),
                         x = ~ date, y = ~ value, colors = "Dark2", name = "data", 
                         type = "scatter", mode = "lines",
                         text = unique(sapply(ts_df$date,toString)), hoverinfo = "text + y") %>%
    layout(title = "Finland Traffic Accidents Multiplicative Model",
           xaxis = list(title = "", showticklabels = FALSE))
  subplot(list(data_plotly, seas_plotly, trend_plotly, remain_plotly), nrows = 4) 
}

plot_ly_decomp(decomp_accs_ts) %>% 
  layout(legend = list(font = list(size = 14)))
```

<iframe  src="https://plot.ly/~anthonymakela/12/#/.embed?link=false" width="100%" height="500" frameborder="no" scrolling="no"></iframe>

### ARIMA

While the plot illustrates the seasonal behavior and trend within the data, if we want to forecast the number of accidents in 2019, we’ll apply another form of time series decomposition called Autoregressive Integrated Moving Average (ARIMA).

Key concepts behind ARIMA.

### Stationary Processes

A stationary time series is one whose statistical properties such as mean, variance, autocorrelation, etc. are all constant over time. Stationary process is quite useful for forecasting: as it contains no trends or longer term changes, knowing its value today is sufficient to predict its future values.

### Autoregressive Models

Autoregressive models and processes operate under the assumption that past values have an effect on current values. In autoregressive models, the output is a linear combination of its p previous (or lagged) values, together with a stochastic term (e.g. white noise).

$$ 
y_{t} = \phi_{1} y_{t-1} + ... + \phi_{p} y_{t-p} + \epsilon_{t}
$$

where $$\epsilon_t$$ denotes the stochastic component in the series.

### Moving Average Models

Rather than using past values of the forecast variable in a regression, a moving average model uses past forecast errors in a regression-like model.

In mathematical terms, a moving average model of order q __(MA(q))__ is written

$$y_{t} = c + \epsilon_{t} + \theta_{1} \epsilon_{t-1} + ... + \theta_{q} \epsilon_{t-q} $$ 

``` r
arima_fit <- auto.arima(ts(acc_yearlymon$acc, frequency = 12, start=2008),
                        allowdrift = TRUE, approximation=FALSE)
arima_fit
```

    ## Series: ts(acc_yearlymon$acc, frequency = 12, start = 2008)  
    ## ARIMA(1,1,1)(0,1,1)[12]                    
    ## 
    ## Coefficients:
    ##          ar1      ma1    smal  
    ##       0.3339  -0.7191  -0.3553
    ## s.e.  0.1566   0.1035   0.1483
    ## 
    ## sigma^2 estimated as 66631:  log likelihood=-745.49
    ## AIC=1498.98   AICc=1499.37   BIC=1509.67


### Forecast

The grey line shows how the ARIMA model compares to the observed 2008-2017 data, while the coloured regions represent the predicted number of accidents in 2018 to varying degrees of certainty. For example, monthly road accidents in 2018 are 80 % and 95 % likely to fall within the green and orange lines, respectively. A monthly value outside of the orange lines would signify an unusually high/low month for road accidents and suggest further investigation for the underlying cause.

``` r
forecast_ <- forecast(arima_fit, h=12)

plot_ly(acc_yearlymon, x = ~ YearMonth, y = ~ acc, type = "scatter", mode = "lines", name = "Observed",
        text = ~ sapply(YearMonth, toString), hoverinfo = "text+y+name") %>% 
  add_trace(x = c(max(acc_yearlymon$YearMonth) + seq(1/12,1,1/12), 
                max(acc_yearlymon$YearMonth) + seq(1,1/12,-1/12)),
            y = c(forecast_$lower[,2], rev(forecast_$upper[,2])), name = "95% Confidence",
            fill = "toself", hoveron = "points",
            text=c(sapply(max(acc_yearlymon$YearMonth) + seq(1/12,1,1/12), toString),
                   sapply(max(acc_yearlymon$YearMonth) + seq(1,1/12,-1/12), toString)), 
            hoverinfo = "text+y+name", hoveron = "points") %>%
  add_trace(x = c(max(acc_yearlymon$YearMonth) + seq(1/12,1,1/12), 
                max(acc_yearlymon$YearMonth) + seq(1,1/12,-1/12)),
            y = c(forecast_$lower[,1], rev(forecast_$upper[,1])), name="80% Confidence",
            fill = "toself", hoveron = "points",
            text = c(sapply(max(acc_yearlymon$YearMonth) + seq(1/12,1,1/12), toString),
                   sapply(max(acc_yearlymon$YearMonth) + seq(1,1/12,-1/12), toString)), 
            hoverinfo = "text+y+name", hoveron = "points")  %>%
  add_trace(x = c(max(acc_yearlymon$YearMonth) + seq(1/12,1,1/12)),
            y = as.vector(forecast_ $mean), name = "Mean Prediction",
            text = sapply(max(acc_yearlymon$YearMonth) + seq(1/12,1,1/12), toString), 
            hoverinfo = "text+y+name", hoveron = "points") %>%
  add_trace(x = ~ YearMonth,
            y = as.vector(forecast_$fitted), name = "Model",
            text = ~ sapply(YearMonth, toString), hoverinfo = "text+y+name",
            line = list(color = "#A9A9A9", dash = "dashed")) %>%
  layout(xaxis = format_axis("Vuosi"), yaxis = format_axis("Maara (Onnettomuudet)"), 
         title = "Onnettomuuksien maara kuukausittain (2008-2018)") %>%
  layout(legend = list(x = 0.8, y = 0.99, font = list(size = 14)))
```


<iframe  src="https://plot.ly/~anthonymakela/4/#/.embed?link=false" width="100%" height="500" frameborder="no" scrolling="no"></iframe>



### Summary

We used several datasets containing information about traffic accidents in Finland between 2008 and 2017. After some EDA and time series theory, we built an ARIMA model to forecast the number of accidents in 2018. The most interesting part of any predictive model is determining how well it performed against the actual data. Sadly, we cannot do this until the 2018 data becomes available.
