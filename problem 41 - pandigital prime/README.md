project euler problem 41: pandigital prime
================
chad allison \| 26 july 2023

------------------------------------------------------------------------

### setup

``` r
library(tidyverse)
library(gtools)
options(digits = 22, scipen = 999)
```

### solution

``` r
# function to check if a number is prime
is_prime = function(n) {
  if (n <= 1) return(F)
  for (i in 2:sqrt(n)) {
    if (n %% i == 0) return(F)
  }
  return(T)
}

# function to find the largest n-digit pandigital prime
find_largest_pandigital_prime = function(n) {
  if (n <= 0 | n > 9) {
    print("invalid input - n must be in the range [1, 9]")
    return(NULL)
  }
  digits = 1:n
  permutations = permutations(n, n, digits)
  largest_pandigital_prime = NULL
  for (i in n:1) {
    pandigital_numbers = apply(permutations, 1, function(x) as.numeric(paste0(x, collapse = "")))
    pandigital_numbers = sort(pandigital_numbers, decreasing = T)
    for (num in pandigital_numbers) {
      if (is_prime(num)) {
        largest_pandigital_prime = num
        break
      }
    }
    if (!is.null(largest_pandigital_prime)) {
      break
    }
  }
  return(largest_pandigital_prime)
}

# finding the largest 7-digit pandigital prime number (i know it's 7-digit from trial and error)
find_largest_pandigital_prime(7)
```

    ## [1] 7652413
