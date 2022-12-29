project euler problem 8: largest product in a series
================
chad allison \| 28 december 2022

------------------------------------------------------------------------

### loading tidyverse

``` r
library(tidyverse)
options(digits = 22, scipen = 999)
```

### getting all thirteen digit chunks

``` r
input = readLines("input.txt")
chunk = NULL

for (i in 13:nchar(input) - 12) {
  chunk[length(chunk) + 1] = substr(input, i, i + 12)
}

head(chunk)
```

    ## [1] "7316717653133" "3167176531330" "1671765313306" "6717653133062"
    ## [5] "7176531330624" "1765313306249"

### creating function for product of each digit

``` r
digit_prod = function(num) {
  
  digits = as.numeric(strsplit(num, split = "")[[1]])
  
  prod = digits[1] * digits[2] * digits[3] * digits[4] * digits[5] * digits[6] * digits[7] *
   digits[8] * digits[9] * digits[10] * digits[11] * digits[12] * digits[13]
  
  return(prod)
  
}

digit_prod = Vectorize(digit_prod)
```

### solution

``` r
ans = data.frame(chunk) |>
  mutate(prod = digit_prod(chunk)) |>
  arrange(desc(prod)) |>
  head(1) |>
  pull(prod)

ans[[1]]
```

    ## [1] 23514624000
