project euler problem 24: lexicographic permutations
================
chad allison \| 01 january 2023

------------------------------------------------------------------------

### setup

``` r
library(tidyverse)
library(gtools) # for permutations
options(digits = 22, scipen = 999)
```

### reproducing example

``` r
vec = 0:2
permutations(n = 3, r = 3, v = vec)
```

    ##      [,1] [,2] [,3]
    ## [1,]    0    1    2
    ## [2,]    0    2    1
    ## [3,]    1    0    2
    ## [4,]    1    2    0
    ## [5,]    2    0    1
    ## [6,]    2    1    0

### getting all permutations of 0123456789

``` r
vec = 0:9
permutations_df = permutations(n = 10, r = 10, v = vec)
permutations_df[1:10, ]
```

    ##       [,1] [,2] [,3] [,4] [,5] [,6] [,7] [,8] [,9] [,10]
    ##  [1,]    0    1    2    3    4    5    6    7    8     9
    ##  [2,]    0    1    2    3    4    5    6    7    9     8
    ##  [3,]    0    1    2    3    4    5    6    8    7     9
    ##  [4,]    0    1    2    3    4    5    6    8    9     7
    ##  [5,]    0    1    2    3    4    5    6    9    7     8
    ##  [6,]    0    1    2    3    4    5    6    9    8     7
    ##  [7,]    0    1    2    3    4    5    7    6    8     9
    ##  [8,]    0    1    2    3    4    5    7    6    9     8
    ##  [9,]    0    1    2    3    4    5    7    8    6     9
    ## [10,]    0    1    2    3    4    5    7    8    9     6

### solution

``` r
data.frame(permutations_df) |>
  arrange(X1, X2, X3, X4, X5, X6, X7, X8, X9, X10) |>
  mutate(id = 1:nrow(permutations_df)) |>
  filter(id == 1000000) |>
  transmute(permutation = as.numeric(paste0(X1, X2, X3, X4, X5, X6, X7, X8, X9, X10))) |>
  pull(permutation)
```

    ## [1] 2783915460
