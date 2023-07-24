project euler problem 38: pandigital multiples
================
chad allison \| 24 july 2023

------------------------------------------------------------------------

### setup

``` r
library(tidyverse)
options(digits = 22, scipen = 999)
```

### solution

``` r
# setting limit
limit = 100000

# function to determine if a number is 1 to 9 pandigital
is_pandigital = function(x) {
  if (nchar(x) != 9) return(F)
  split = as.numeric(str_split(x, "")[[1]])
  return(sum(sort(split) == 1:9) == 9)
}

# function to generate concatenated product
concatenated_product = function(x, y) {
  prod = ""
  for (i in 1:y) {
    prod = paste0(prod, x * i)
  }
  return(as.numeric(prod))
}

# function to find largest concatenated product for a given n
find_largest = function(n) {
  max = 0
  for (i in 1:limit) {
    if (is_pandigital(concatenated_product(i, n)) & concatenated_product(i, n) > max) {
      max = concatenated_product(i, n)
    }
  }
  return(max)
}

# generating vector of NAs to populated
prod_vec = rep(NA, 9)

# generating largest concatenated product for n = 1, 2, ..., 9
for (i in 1:9) {
  prod_vec[i] = find_largest(i)
}

# solution
max(prod_vec)
```

    ## [1] 932718654
