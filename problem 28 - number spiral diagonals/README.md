project euler problem 28: number spiral diagonals
================
chad allison \| 05 january 2023

------------------------------------------------------------------------

### setup

``` r
library(tidyverse)
options(digits = 22, scipen = 999)
```

### creating function to solve

``` r
diag_sum = function(size) {
  ans = 1
  for (i in 3:size) {
    if (i %% 2 == 1) ans = ans + sum(4 * i ^ 2 - 6 * (i - 1))
  }
  return(as.character(ans))
}

diag_sum(5)
```

    ## [1] "101"

### solution

``` r
diag_sum(1001)
```

    ## [1] "669171001"
