project euler problem 33: digit cancelling fractions
================
chad allison \| 19 july 2023

------------------------------------------------------------------------

### setup

``` r
library(tidyverse)
library(FRACTION)
options(digits = 22, scipen = 999)
```

### logic

``` r
# function to determine if two numbers share a digit
has_shared_digit = function(x, y) {
  xd = as.numeric(str_split(x, "")[[1]])
  yd = as.numeric(str_split(y, "")[[1]])
  if (length(intersect(xd, yd) > 0)) return(T) else return(F)
}

# if x and y share a digit, returns x with the shared digit removed
remove_shared_digit_x = function(x, y) {
  if (substr(x, 1, 1) == substr(y, 1, 1)) return(as.numeric(substr(x, 2, 2)))
  if (substr(x, 1, 1) == substr(y, 2, 2)) return(as.numeric(substr(x, 2, 2)))
  if (substr(x, 2, 2) == substr(y, 1, 1)) return(as.numeric(substr(x, 1, 1)))
  if (substr(x, 2, 2) == substr(y, 2, 2)) return(as.numeric(substr(x, 1, 1)))
}

# if x and y share a digit, returns y with the shared digit removed
remove_shared_digit_y = function(x, y) {
  if (substr(x, 1, 1) == substr(y, 1, 1)) return(as.numeric(substr(y, 2, 2)))
  if (substr(x, 1, 1) == substr(y, 2, 2)) return(as.numeric(substr(y, 1, 1)))
  if (substr(x, 2, 2) == substr(y, 1, 1)) return(as.numeric(substr(y, 2, 2)))
  if (substr(x, 2, 2) == substr(y, 2, 2)) return(as.numeric(substr(y, 1, 1)))
}

# implementing functions on all possible combinations
crossing(x = 10:99, y = 10:99) |>
  filter(x < y & !(substr(x, 2, 2) == 0 & substr(y, 2, 2) == 0)) |>
  rowwise() |>
  mutate(shared = has_shared_digit(x, y)) |>
  ungroup() |>
  filter(shared) |>
  select(-shared) |>
  rowwise() |>
  mutate(new_x = remove_shared_digit_x(x, y),
         new_y = remove_shared_digit_y(x, y)) |>
  ungroup() |>
  filter(x / y == new_x / new_y)
```

    ## # A tibble: 4 × 4
    ##       x     y new_x new_y
    ##   <int> <int> <dbl> <dbl>
    ## 1    16    64     1     4
    ## 2    19    95     1     5
    ## 3    26    65     2     5
    ## 4    49    98     4     8

### solution

``` r
paste0("final simplified fraction: ", fra((16 / 64) * (19 / 95) * (26 / 65) * (49 / 98)))
```

    ## [1] "final simplified fraction: 1 / 100"
