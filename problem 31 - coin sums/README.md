<<<<<<< HEAD
project euler problem 31: coin sums
================
chad allison \| 22 january 2023

------------------------------------------------------------------------

### setup

``` r
library(tidyverse)
options(digits = 22, scipen = 999)
```

### solution

``` r
ways = c(1, rep(0, times = 200))

for (i in c(1, 2, 5, 10, 20, 50, 100, 200)) {
  for (j in i:200) {
    ways[j + 1] = ways[j + 1] + ways[j + 1 - i]
  }
}

ways[length(ways)]
```

    ## [1] 73682
=======
project euler problem 31: coin sums
================
chad allison \| 22 january 2023

------------------------------------------------------------------------

### setup

``` r
library(tidyverse)
options(digits = 22, scipen = 999)
```

### solution

``` r
ways = c(1, rep(0, times = 200))

for (i in c(1, 2, 5, 10, 20, 50, 100, 200)) {
  for (j in i:200) {
    ways[j + 1] = ways[j + 1] + ways[j + 1 - i]
  }
}

ways[length(ways)]
```

    ## [1] 73682
>>>>>>> f1222a78a7a34ae61e1902ab8e4bede3dfa4665f
