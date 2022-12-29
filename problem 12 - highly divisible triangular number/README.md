project euler problem 11: largest product in a grid
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
tau = function(num) {
  
  n = num
  i = 2
  p = 1

  if (num == 1) return(1)

  while (i ^ 2 <= n) {
    c = 1
    while (n %% i == 0) {
      n = n / i
      c = c + 1
    }
    
    i = i + 1
    p = p * c
  
  }

  if (n == num | n > 1)
    p = p * (2)

  return(p)
  
}

solution = function(x) {
  
  n = 1
  d = 1

  while (tau(d) <= x) {
    n = n + 1
    d = d + n
  }
  
  return(d)
  
}

solution(500)
```

    ## [1] 76576500
