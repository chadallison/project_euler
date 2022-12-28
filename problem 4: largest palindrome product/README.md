project euler problem 4: largest palindrome product
================
chad allison \| 28 december 2022

------------------------------------------------------------------------

### loading tidyverse

``` r
library(tidyverse)
options(digits = 22, scipen = 999)
```

### creating palindrome function

``` r
isPalindrome = function(x) {
  
  forward = as.character(x)
  rev = ""
  
  for (i in nchar(x):1) {
    rev = paste0(rev, substr(x, i, i))
  }
  
  return(forward == rev)
  
}

isPalindrome = Vectorize(isPalindrome)
isPalindrome(9009)
```

    ## [1] TRUE

### reproducing example

``` r
crossing(x = 1:99, y = 1:99) |>
  mutate(prod = x * y) |>
  filter(nchar(prod) >= 4) |>
  mutate(palin = isPalindrome(prod)) |>
  filter(palin == T) |>
  arrange(desc(prod)) |>
  head(1) |>
  pull(prod)
```

    ## [1] 9009

### solution

``` r
crossing(x = 1:999, y = 1:999) |>
  mutate(prod = x * y) |>
  filter(nchar(prod) >= 4) |>
  mutate(palin = isPalindrome(prod)) |>
  filter(palin == T) |>
  arrange(desc(prod)) |>
  head(1) |>
  pull(prod)
```

    ## [1] 906609
