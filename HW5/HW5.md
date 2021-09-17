HW 5
================

``` r
library(tidyverse)

# Count the diamonds in each cut
count(diamonds, cut)
```

    ## # A tibble: 5 × 2
    ##   cut           n
    ##   <ord>     <int>
    ## 1 Fair       1610
    ## 2 Good       4906
    ## 3 Very Good 12082
    ## 4 Premium   13791
    ## 5 Ideal     21551

``` r
# Randomly select 1% of the diamond data
reduced_diamonds <- sample_frac(diamonds, .01)
reduced_diamonds
```

    ## # A tibble: 539 × 10
    ##    carat cut       color clarity depth table price     x     y     z
    ##    <dbl> <ord>     <ord> <ord>   <dbl> <dbl> <int> <dbl> <dbl> <dbl>
    ##  1  1.5  Premium   I     VVS1     62.4    60 11155  7.32  7.29  4.56
    ##  2  0.31 Ideal     J     SI1      61.3    56   418  4.37  4.4   2.69
    ##  3  0.31 Ideal     G     VS2      61.7    55   562  4.37  4.39  2.7 
    ##  4  1.26 Very Good H     SI1      62.1    57  6320  6.88  6.94  4.29
    ##  5  0.25 Ideal     E     VVS1     62.3    53   783  4.08  4.11  2.55
    ##  6  1    Good      G     VVS2     60.9    56  7492  6.49  6.52  3.96
    ##  7  1.56 Good      F     SI2      57.5    58  9784  7.82  7.67  4.45
    ##  8  1.51 Premium   G     VS2      62.7    58 12872  7.31  7.2   4.55
    ##  9  0.6  Good      G     VS1      60.1    61  1757  5.44  5.5   3.29
    ## 10  0.33 Premium   G     VS2      60      58   579  4.47  4.49  2.69
    ## # … with 529 more rows

``` r
# Find average size of top 100 diamonds of each clarity category
top_hundred_size <- diamonds %>%
  group_by(clarity) %>%
  mutate(area.xyz = x*y*z) %>%
  arrange(area.xyz)
  
top_hundred_size %>%
  dplyr::top_n(100, area.xyz) %>%
  summarize(average.area = mean(area.xyz))
```

    ## # A tibble: 8 × 2
    ##   clarity average.area
    ##   <ord>          <dbl>
    ## 1 I1              400.
    ## 2 SI2             456.
    ## 3 SI1             375.
    ## 4 VS2             365.
    ## 5 VS1             351.
    ## 6 VVS2            270.
    ## 7 VVS1            246.
    ## 8 IF              229.

``` r
# plot x vs y, x vs z
ggplot(diamonds) +
  geom_point(aes(y = x, x = y))
```

![](HW5_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

``` r
ggplot(diamonds) +
  geom_point(aes(y = x, x = z))
```

![](HW5_files/figure-gfm/unnamed-chunk-4-2.png)<!-- -->

``` r
# Remove outliers
rm_outliers <- diamonds %>%
  filter(x > 0, y > 0 , z > 0) %>%
  filter( y/x < 4, z/x < 4)
  
ggplot(rm_outliers) +
  geom_point(aes(y = x, x = y))
```

![](HW5_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->

``` r
ggplot(rm_outliers) +
  geom_point(aes(y = x, x = z))
```

![](HW5_files/figure-gfm/unnamed-chunk-5-2.png)<!-- -->
