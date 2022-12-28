project euler problem 5: smallest multiple
================
chad allison \| 28 december 2022

------------------------------------------------------------------------

### loading tidyverse

``` r
library(tidyverse)
options(digits = 22, scipen = 999)
```

### reproducing example

``` r
div_by_10 = function(x) {
  bool = T
  
  for (i in 1:10) {
    if (x %% i != 0) bool = F
  }
  
  return(bool)
}

match = F
i = 10

while(!match) {
  res = div_by_10(i)
  if (res) print(i)
  if (res) match = T
  i = i + 10
}
```

    ## [1] 2520

### solution

``` r
div_by_20 = function(x) {
  bool = T
  
  for (i in 1:20) {
    if (x %% i != 0) bool = F
  }
  
  return(bool)
}

match = F
i = 20

while(!match) {
  res = div_by_20(i)
  if (res) print(i)
  if (res) match = T
  i = i + 20
}
```

    ## [1] 232792560
