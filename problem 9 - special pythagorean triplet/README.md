project euler problem 9: special pythagorean triplet
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
crossing(a = 1:200, b = 2:375, c = 3:425) |>
  filter(a + b + c == 1000 &
         a < b & b < c &
         a ^ 2 + b ^ 2 == c ^ 2) |>
  summarise(prod = a * b * c) |>
  pull(prod)
```

    ## [1] 31875000
