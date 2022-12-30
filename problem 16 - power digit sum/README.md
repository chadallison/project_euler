project euler problem 16: power digit sum
================
chad allison \| 29 december 2022

------------------------------------------------------------------------

### setup

``` r
library(tidyverse)
library(gmp)
options(digits = 22, scipen = 999)
```

### reproducing example

``` r
power_digit_sum = function(x) sum(as.numeric(str_split(2 ^ x, pattern = "")[[1]]))
power_digit_sum(15)
```

    ## [1] 26

### solution

``` r
num = as.bigz(2 ^ 1000)
sum(as.numeric(unlist(strsplit(as.character(num), ""))))
```

    ## [1] 1366
