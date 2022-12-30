project euler problem 15: lattice paths
================
chad allison \| 29 december 2022

------------------------------------------------------------------------

### setup

``` r
library(tidyverse)
options(digits = 22, scipen = 999)
```

### solution

``` r
lattice = function(x) return(choose(2 * x, x))
lattice(20)
```

    ## [1] 137846528820
