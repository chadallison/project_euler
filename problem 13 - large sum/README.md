project euler problem 13: large sum
================
chad allison \| 28 december 2022

------------------------------------------------------------------------

### setup

``` r
library(tidyverse)
options(digits = 22, scipen = 999)
```

### solution

``` r
data.frame(x = readLines("input.txt")) |>
  mutate(x = as.numeric(x)) |>
  summarise(sum = sum(x)) |>
  pull(sum) |>
  substr(1, 10)
```

    ## [1] "5537376230"
