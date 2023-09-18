test for hw1
================
Yige Bian
2023-9-18

# Problem 1

## Data description

``` r
# Load the moderndive library and load the early_january_weather datase
library(moderndive)
data("early_january_weather")
```

- Variables in the dataset ‘early_january_weather’ are origin, year,
  month, day, hour, temp, dewp, humid, wind_dir, wind_speed, wind_gust,
  precip, pressure, visib, time_hour.
  - The variable `origin` has class character
  - The variable `year` has class integer
  - The variable `month` has class integer
  - The variable `day` has class integer
  - The variable `hour` has class integer
  - The variable `temp` has class numeric
  - The variable `dewp` has class numeric
  - The variable `humid` has class numeric
  - The variable `wind_dir` has class numeric
  - The variable `wind_speed` has class numeric
  - The variable `wind_gust` has class numeric
  - The variable `precip` has class numeric
  - The variable `pressure` has class numeric
  - The variable `visib` has class numeric
  - The variable `time_hour` has class POSIXct, POSIXt.
- The dataset ‘early_january_weather’ has 358 rows and 15 columns.
- The mean temperature is 39.5821229

## Data plot

``` r
# Scatterplot of temp (y) vs time_hour (x), color points using the humid
ggplot(early_january_weather, aes(x = time_hour, y = temp, color=humid)) + geom_point()
```

![](test1_hw1_files/figure-gfm/scatter%20plot%20for%20time%20and%20temp-1.png)<!-- -->

The scatter plot illustrates that, from January 1st to January 15th, a
noticeable upward trend in temperature fluctuations can be observed. The
temperature during different times of the day follows a similar pattern
of change, and overall, the average temperature continues to rise. In
the first few days of January, the humidity is relatively low. Starting
from January 6th, there are intermittent periods of increased humidity.
It’s worth noting that from January 11th to January 14th, the humidity
is particularly high, and during these days, the daily temperature
fluctuations are relatively small.

``` r
# Export scatterplot to project directory
ggsave("scatter_plot.pdf", height = 4, width = 6)
```

# Problem 2

## Dataframe initialization

``` r
set.seed(1)

samp_df = tibble(
  vec_random = rnorm(10),
  vec_logical = vec_random > 0,
  vec_char = c("1", "2", "3", "4", "5", "6", "7", "8", "9", "10"),
  vec_factor = factor(c("high", "med", "samll", "high", "med", "med", "samll", "samll", "high", "med"))
)
```

## Mean of variables

``` r
mean(pull(samp_df,vec_random))
```

    ## [1] 0.1322028

``` r
mean(pull(samp_df,vec_logical))
```

    ## [1] 0.6

``` r
mean(pull(samp_df,vec_char))
```

    ## Warning in mean.default(pull(samp_df, vec_char)): argument is not numeric or
    ## logical: returning NA

    ## [1] NA

``` r
mean(pull(samp_df,vec_factor))
```

    ## Warning in mean.default(pull(samp_df, vec_factor)): argument is not numeric or
    ## logical: returning NA

    ## [1] NA

## Convert of variable types

``` r
mean(as.numeric(pull(samp_df,vec_char)))
as.numeric(pull(samp_df,vec_factor))
```
