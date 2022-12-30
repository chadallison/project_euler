project euler problem 20: factorial digit sum
================
chad allison \| 30 december 2022

------------------------------------------------------------------------

### setup

``` r
library(tidyverse)
library(gmp) # necessary for large numbers
options(digits = 22, scipen = 99999)
```

### computing 100!

``` r
factorialZ(100)
```

    ## Big Integer ('bigz') :
    ## [1] 93326215443944152681699238856266700490715968264381621468592963895217599993229915608941463976156518286253697920827223758251185210916864000000000000000000000000

### solution

``` r
num = factorialZ(100)
split = str_split(num, pattern = "")[[1]]
sum(as.numeric(split))
```

    ## [1] 648
