project euler problem 23: non-abundant sums
================
chad allison \| 31 december 2022

------------------------------------------------------------------------

### setup

``` r
library(tidyverse)
options(digits = 22, scipen = 999)
```

### creating function to determine if number is abundant

``` r
abundant = function(n) {
  if (n == 1) return(F)
  div = which(n %% seq(1, n - 1) == 0)
  return(sum(div) > n)
}

abundant(12)
```

    ## [1] TRUE

### getting all abundant integers up to 28123

``` r
abundant_ints = data.frame(num = 12:28123) |>
  mutate(isAbundant = sapply(num, abundant)) |>
  filter(isAbundant)

sample_n(abundant_ints, 10)
```

    ##      num isAbundant
    ## 1  15036       TRUE
    ## 2  26110       TRUE
    ## 3  15384       TRUE
    ## 4  24042       TRUE
    ## 5  13332       TRUE
    ## 6  19500       TRUE
    ## 7  25780       TRUE
    ## 8  21808       TRUE
    ## 9   4180       TRUE
    ## 10 14538       TRUE

### getting all integers than can be expressed as sum of two abundant numbers

``` r
all_abundant = abundant_ints |>
  pull(num)

abundant_sum_nums = crossing(x = all_abundant, y = all_abundant) |>
  mutate(sum = x + y) |>
  pull(sum) |>
  unique()

sample(abundant_sum_nums, 25)
```

    ##  [1] 42975 44587 36635 44318 10848 17961 47195  3105 29721 49765 24969 26230
    ## [13] 50641 16372 26320 31921 38655 20943 17897 47582 13816 49652 53542 16101
    ## [25] 46862

### solution

``` r
integers = 1:28123
sum(integers[!integers %in% abundant_sum_nums])
```

    ## [1] 4179871
