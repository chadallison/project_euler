project euler problem 19: counting sundays
================
chad allison \| 30 december 2022

------------------------------------------------------------------------

### setup

``` r
library(tidyverse)
library(lubridate)
options(digits = 22, scipen = 999)
```

### creating data

``` r
df = data.frame(date = as_date(as_date("1901-01-01"):as_date("2000-12-31")))
sample_n(df, 10)
```

    ##          date
    ## 1  1914-11-16
    ## 2  1968-02-08
    ## 3  1954-09-07
    ## 4  1976-11-08
    ## 5  1990-01-12
    ## 6  1945-02-25
    ## 7  1995-03-21
    ## 8  1950-02-03
    ## 9  1956-03-10
    ## 10 1910-05-03

### creating day variable

``` r
df = df |>
  mutate(day_num = day(date))

sample_n(df, 10)
```

    ##          date day_num
    ## 1  1978-11-21      21
    ## 2  1932-04-21      21
    ## 3  1936-10-29      29
    ## 4  1977-05-22      22
    ## 5  1923-10-03       3
    ## 6  1969-01-25      25
    ## 7  1952-11-06       6
    ## 8  1952-09-14      14
    ## 9  1944-06-30      30
    ## 10 1930-05-04       4

### creating weekday variable

``` r
df = df |>
  mutate(weekday = wday(date, label = T, abbr = F))

sample_n(df, 10)
```

    ##          date day_num   weekday
    ## 1  1985-05-26      26    Sunday
    ## 2  1992-01-24      24    Friday
    ## 3  1996-01-22      22    Monday
    ## 4  1957-11-20      20 Wednesday
    ## 5  1935-04-27      27  Saturday
    ## 6  1912-02-24      24  Saturday
    ## 7  1957-01-23      23 Wednesday
    ## 8  1942-04-06       6    Monday
    ## 9  1955-07-01       1    Friday
    ## 10 1901-07-26      26    Friday

### solution

``` r
n = df |>
  filter(day_num == 1 & weekday == "Sunday") |>
  nrow()

paste0("during the twentieth centurty, there were ", n, " sundays that fell on the first of the month")
```

    ## [1] "during the twentieth centurty, there were 171 sundays that fell on the first of the month"
