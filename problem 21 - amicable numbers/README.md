project euler problem 21: amicable numbers
================
chad allison \| 30 december 2022

------------------------------------------------------------------------

### setup

``` r
library(tidyverse)
options(digits = 22, scipen = 999)
```

### creating function for sum of proper divisors

``` r
d = function(x) {
  vec = NULL
  if (x == 1) return(0)
  for (i in 2:x - 1) if (x %% i == 0) vec[length(vec) + 1] = i
  return(sum(vec))
}

d(220)
```

    ## [1] 284

### creating function to determine if number is amicable

``` r
amicable = function(n) {
  if (n == 1) return(F)
  x = d(n)
  if (n == x) return(F)
  y = d(x)
  return(n == y)
}

amicable(220)
```

    ## [1] TRUE

### finding all amicable numbers under 10000

``` r
amicable_numbers = NULL
for (i in 1:9999) if (amicable(i)) amicable_numbers[length(amicable_numbers) + 1] = i

amicable_numbers
```

    ##  [1]  220  284 1184 1210 2620 2924 5020 5564 6232 6368

### solution

``` r
sum(amicable_numbers)
```

    ## [1] 31626
