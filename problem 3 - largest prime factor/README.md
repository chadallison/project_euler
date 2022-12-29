project euler problem 3: largest prime factor
================
chad allison \| 28 december 2022

------------------------------------------------------------------------

### loading tidyverse

``` r
library(tidyverse)
options(digits = 22, scipen = 999)
```

### creating function for primes

``` r
sieve = function(n) {
  
    if (n == 1) return(NULL)
    if (n == 2) return(n)
    l = c(2, seq(from = 3, to = n, by = 2))
    i = 1
    p = 2
    
    while (p ^ 2 <= n) {
      
        l = l[l == p | l %% p != 0]
        i = i + 1
        p = l[i]
        
    }
    
    return(l)
    
}

head(sieve(13195))
```

    ## [1]  2  3  5  7 11 13

### creating function for prime factors

``` r
prime.factors = function (n) {
  
        factors = c()
        primes = sieve(floor(sqrt(n)))
        d = which(n %% primes == 0)
        
        if (length(d) == 0) return(n)
        for (q in primes[d]) {
            
          while (n %% q == 0) {
            
                factors = c(factors, q)
                n = n / q
                
          }
          
        }
        
        if (n > 1) factors = c(factors, n)
        return(factors)
        
}

prime.factors(13195)
```

    ## [1]  5  7 13 29

### solution

``` r
max(prime.factors(600851475143))
```

    ## [1] 6857
