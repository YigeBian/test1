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

From the output, we can observe that the variable `vec_random` and
`vec_logical` with numeric and logical form could be calculated the
mean, while the other two variables `vec_char` and `vec_factor` with
character and factor form got the result of NA and encounter the
warning: argument is not numeric or logical.

## Convert of variable types

``` r
# Define variables with different data type
samp_num = c(-1, 1, 0.4, -3, 4)
samp_logical = samp_num < 0
samp_char_str = c("1", "2", "3", "4", "5")
samp_char_num = c("a", "b", "c", "d", "e")
samp_fac_str = factor(c("high", "med", "samll", "high", "med", "med"))
samp_fac_num = factor(c("500", "400", "300", "200", "100", "600"))
samp_fac_mix = factor(c("500", "a", "*", "200", "z", "#"))

# use as.numeric() to convert type of variables
as.numeric(samp_logical)
as.numeric(samp_char_str)
as.numeric(samp_char_num)
as.numeric(samp_fac_str)
as.numeric(samp_fac_num)
as.numeric(samp_fac_mix)
as.numeric(as.character(samp_fac_num))
```

We have defined variables `samp_logical` with class `logical`,
`samp_char_str` with class `character`, `samp_char_num` with class
`character`, `samp_fac_str` with class `factor`, `samp_fac_num` with
class `factor` and `samp_fac_mix` with class `factor`.

1.  Logical variable: we observed that under the function
    `as.numeric()`, true value will be converted to 1 and false value
    will be converted to 0.
2.  Character variable: if the variable stored numbers in char type like
    `samp_char_num`, as.numeric() could convert it into numeric, while
    if the variable stored string in char type like `samp_char_str`,
    as.numeric() will fail to convert it to numeric.
3.  Factor variable: We observed that when use as.numeric() to convert
    factor to numeric, it will be converted to number from 1 to n
    follows some rules of rank, where n is the number of different
    values in the variable. If all values are numbers like
    `samp_fac_num`, the rank is the value of number from small to large.
    If all values are strings like `samp_fac_str`, the rank is the
    alphabetic sequence. If values in the variable are a mix of numbers,
    strings and symbols like `samp_fac_mix`, it follows the rank symbol,
    number and string. Moreover, if we want to obtian the number in
    `samp_fac_num` into numeric type, we should use `as.character()` to
    convert it to char first, and then use `as.numeric()` to convert it
    to numeric.
