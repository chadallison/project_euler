project euler problem 29: distinct powers
================
chad allison \| 03 january 2023

------------------------------------------------------------------------

### setup

``` r
library(tidyverse)
options(digits = 22, scipen = 999)
```

### solution

``` r
crossing(a = 2:100, b = 2:100) |>
  mutate(x = a ^ b) |>
  distinct(x) |>
  nrow()
```

    ## [1] 9183
