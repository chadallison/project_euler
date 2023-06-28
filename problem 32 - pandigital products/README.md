<<<<<<< HEAD
project euler problem 32: pandigital products
================
chad allison \| 23 january 2023

------------------------------------------------------------------------

### setup

``` r
library(tidyverse)
options(digits = 22, scipen = 999)
```

### creating function to find if number is pandigital

``` r
is_pandigital = function(x) {
  digits = as.numeric(strsplit(as.character(x), "")[[1]])
  length(digits) == 9 & all(1:9 %in% digits)
}
```

### solution

``` r
pandigital_products = c()

max_int = 2500
for (i in 1:max_int) {
  for (j in 1:max_int) {
    product = i * j
    pandigital_identity = paste0(i, j, product)
    if (is_pandigital(pandigital_identity)) {
      pandigital_products = c(pandigital_products, product)
    }
  }
}

sum(unique(pandigital_products))
```

    ## [1] 45228
=======
project euler problem 32: pandigital products
================
chad allison \| 23 january 2023

------------------------------------------------------------------------

### setup

``` r
library(tidyverse)
options(digits = 22, scipen = 999)
```

### creating function to find if number is pandigital

``` r
is_pandigital = function(x) {
  digits = as.numeric(strsplit(as.character(x), "")[[1]])
  length(digits) == 9 & all(1:9 %in% digits)
}
```

### solution

``` r
pandigital_products = c()

max_int = 2500
for (i in 1:max_int) {
  for (j in 1:max_int) {
    product = i * j
    pandigital_identity = paste0(i, j, product)
    if (is_pandigital(pandigital_identity)) {
      pandigital_products = c(pandigital_products, product)
    }
  }
}

sum(unique(pandigital_products))
```

    ## [1] 45228
>>>>>>> f1222a78a7a34ae61e1902ab8e4bede3dfa4665f
