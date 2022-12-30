project euler problem 17: number letter counts
================
chad allison \| 29 december 2022

------------------------------------------------------------------------

### setup

``` r
library(tidyverse)
library(english)
options(digits = 22, scipen = 999)
```

### reproducing example

``` r
data.frame(num = 1:5) |>
  mutate(written = as.character(english(num)),
         chars = nchar(written))
```

    ##   num written chars
    ## 1   1     one     3
    ## 2   2     two     3
    ## 3   3   three     5
    ## 4   4    four     4
    ## 5   5    five     4

``` r
data.frame(num = 1:5) |>
  mutate(written = as.character(english(num)),
         chars = nchar(written)) |>
  summarise(letters = sum(chars)) |>
  pull(letters)
```

    ## [1] 19

### solution

``` r
data.frame(num = 1:1000) |>
  mutate(written = str_remove_all(as.character(english(num)), "[ -]"),
         written = ifelse(str_detect(written, "hundred") &
                          substr(written, nchar(written) - 6, nchar(written)) != "hundred",
                          str_replace_all(written, "hundred", "hundredand"), written),
         chars = nchar(written)) |>
  sample_n(10) |>
  arrange(num)
```

    ##    num                   written chars
    ## 1   51                  fiftyone     8
    ## 2  204         twohundredandfour    17
    ## 3  376 threehundredandseventysix    25
    ## 4  453  fourhundredandfiftythree    24
    ## 5  459   fourhundredandfiftynine    23
    ## 6  463  fourhundredandsixtythree    24
    ## 7  602          sixhundredandtwo    16
    ## 8  712     sevenhundredandtwelve    21
    ## 9  855  eighthundredandfiftyfive    24
    ## 10 990      ninehundredandninety    20

``` r
data.frame(num = 1:1000) |>
  mutate(written = str_remove_all(as.character(english(num)), "[ -]"),
         written = ifelse(str_detect(written, "hundred") &
                          substr(written, nchar(written) - 6, nchar(written)) != "hundred",
                          str_replace_all(written, "hundred", "hundredand"), written),
         chars = nchar(written)) |>
  summarise(n = sum(chars)) |>
  pull(n)
```

    ## [1] 21124
