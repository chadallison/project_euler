project euler problem 2: even fibonacci numbers
================
chad allison \| 27 december 2022

------------------------------------------------------------------------

### loading tidyverse

``` r
library(tidyverse)
options(digits = 22, scipen = 999)
```

### solution

``` r
fibo = function(x) {
  nums = 1:2
  i = 1
  while (i <= x) {
    nums[length(nums) + 1] = nums[length(nums) - 1] + nums[length(nums)]
    i = i + 1
  }
  return(nums)
}

vec = fibo(40)
sum(vec[vec <= 4000000 & vec %% 2 == 0])
```

    ## [1] 4613732
