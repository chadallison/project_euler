project euler problem 22: names scores
================
chad allison \| 30 december 2022

------------------------------------------------------------------------

### setup

``` r
library(tidyverse)
options(digits = 22, scipen = 999)
```

### loading input data

``` r
input = readLines("input.txt") |>
  str_split(pattern = ",") |>
  unlist() |>
  str_remove_all("\"")

sample(input, 10)
```

    ##  [1] "FLORA"    "TANDY"    "JEANNE"   "KIMBERLI" "CARLEE"   "MARGRET" 
    ##  [7] "ALEIDA"   "LIANA"    "CAITLYN"  "ILEANA"

### formatting input as data frame and putting into alphabetical order

``` r
df = data.frame(name = input) |>
  arrange(name) |>
  mutate(id = 1:length(input))

sample_n(df, 10)
```

    ##         name   id
    ## 1     MONROE 3591
    ## 2       IVAN 2091
    ## 3   SHANTELL 4346
    ## 4      CHERE  812
    ## 5  ANJANETTE  240
    ## 6     JANENE 2168
    ## 7    EMERALD 1491
    ## 8      JORGE 2381
    ## 9      FLOYD 1682
    ## 10      KRIS 2670

### creating data frame for letter values

``` r
letter_vals = data.frame(letter = c("A", "B", "C", "D", "E", "F", "G", "H", "I", "J", "K", "L", "M",
                                    "N", "O", "P", "Q", "R", "S", "T", "U", "V", "W", "X", "Y", "Z"),
                         value = 1:26)

sample_n(letter_vals, 10)
```

    ##    letter value
    ## 1       G     7
    ## 2       L    12
    ## 3       Q    17
    ## 4       R    18
    ## 5       C     3
    ## 6       E     5
    ## 7       W    23
    ## 8       T    20
    ## 9       Z    26
    ## 10      N    14

### creating function to calculate name score

``` r
name_score = function(name) {
  score = 0
  for (i in 1:nchar(name)) {
    letter = substr(name, i, i)
    value = letter_vals$value[which(letter_vals$letter == letter)]
    score = score + value
  }
  return(score)
}

name_score = Vectorize(name_score)
name_score("CHAD")
```

    ## CHAD 
    ##   16

### applying function and computing overall score

``` r
df = df |>
  mutate(score = name_score(name),
         ovr = id * score)

sample_n(df, 10)
```

    ##       name   id score    ovr
    ## 1    MABLE 3143    33 103719
    ## 2  KAYLENE 2564    73 187172
    ## 3    JOHNA 2345    48 112560
    ## 4  ROLLAND 4115    76 312740
    ## 5    RANDY 3977    62 246574
    ## 6  ANGELIC  216    51  11016
    ## 7  CHERLYN  821    85  69785
    ## 8    MARRY 3346    75 250950
    ## 9  LATICIA 2788    55 153340
    ## 10  REGENA 4012    50 200600

### solution

``` r
sum(df$ovr)
```

    ## [1] 871198282
