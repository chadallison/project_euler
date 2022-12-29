project euler problem 10: summation of primes
================
chad allison \| 28 december 2022

------------------------------------------------------------------------

### setup

``` r
library(tidyverse)
options(digits = 22, scipen = 999)
```

### creating function for primes

``` r
sieve = function(n) {
  
    if (n == 1) return(NULL)
    if (n == 2) return(n)
    list = c(2, seq(from = 3, to = n, by = 2))
    i = 1
    p = 2
    
    while (p ^ 2 <= n) {
        list = list[list == p | list %% p != 0]
        i = i+1
        p = list[i]
    }
    
    return(list)
    
}

sieve(100)
```

    ##  [1]  2  3  5  7 11 13 17 19 23 29 31 37 41 43 47 53 59 61 67 71 73 79 83 89 97

### solution

``` r
sum(sieve(2000000))
```

    ## [1] 142913828922
