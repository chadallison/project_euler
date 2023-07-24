project euler problem 37: truncatable primes
================
chad allison \| 23 july 2023

------------------------------------------------------------------------

### setup

``` r
library(tidyverse)
options(digits = 22, scipen = 999)
```

### solution

``` r
# setting limit to one million
limit = 1e6

# function to generate primes up to a given n
sieve = function(n) {
   n = as.integer(n)
   if (n > 1e8) stop("n too large")
   primes = rep(T, n)
   primes[1] = F
   last.prime = 2L
   fsqr = floor(sqrt(n))
   while (last.prime <= fsqr) {
     primes[seq.int(2L * last.prime, n, last.prime)] = F
     sel = which(primes[(last.prime + 1):(fsqr + 1)])
     if (any(sel)) {
       last.prime = last.prime + min(sel)
     } else last.prime = fsqr + 1
   }
   return(which(primes))
}

# generating all primes up to the given limit
all_primes = sieve(limit)

# function to determine if a number is left-truncatable
is_left_truncatable = function(num) {
  char = nchar(num)
  if (char == 1) return(F)
  for (i in 1:char) {
    if (!as.numeric(substr(num, i, char)) %in% all_primes) return(F)
  }
  return(T)
}

# function to determine if a number is right-truncatable
is_right_truncatable = function(num) {
  char = nchar(num)
  if (char == 1) return(F)
  for (i in char:1) {
    if (!as.numeric(substr(num, 1, i)) %in% all_primes) return(F)
  }
  return(T)
}

# getting all left-truncatable primes
left_truncatables = data.frame(x = all_primes) |>
  mutate(y = sapply(x, is_left_truncatable)) |>
  filter(y) |>
  pull(x)

# getting all left-and-right-truncatable primes
truncatables = data.frame(x = left_truncatables) |>
  mutate(y = sapply(x, is_right_truncatable)) |>
  filter(y) |>
  pull(x)

# summing all left-and-right-truncatable primes
if (length(truncatables) == 11) {
  print(sum(truncatables))
} else {
  print("wrong number of left-and-right-truncatable primes")
}
```

    ## [1] 748317
