project euler problem 6: sum square difference
================
chad allison \| 28 december 2022

------------------------------------------------------------------------

### loading tidyverse

``` r
library(tidyverse)
options(digits = 22, scipen = 999)
```

### creating sum squares function

``` r
sum_squares = function(x) {
  sum = data.frame(x = 1:x) |>
    mutate(x2 = x ^ 2) |>
    pull(x2) |>
    sum()
  
  return(sum)
}

sum_squares(10)
```

    ## [1] 385

### creating sqaure of sum function

``` r
square_sum = function(x) {
  return(sum(1:x) ^ 2)
}

square_sum(10)
```

    ## [1] 3025

### reproducing example

``` r
square_sum(10) - sum_squares(10)
```

    ## [1] 2640

### solution

``` r
square_sum(100) - sum_squares(100)
```

    ## [1] 25164150
