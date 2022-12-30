project euler problem 18: maximum path sum i
================
chad allison \| 30 december 2022

------------------------------------------------------------------------

### setup

``` r
library(tidyverse)
library(english)
options(digits = 22, scipen = 999)
```

### loading input data

``` r
input = readLines("input.txt")
input
```

    ##  [1] "75"                                          
    ##  [2] "95 64"                                       
    ##  [3] "17 47 82"                                    
    ##  [4] "18 35 87 10"                                 
    ##  [5] "20 04 82 47 65"                              
    ##  [6] "19 01 23 75 03 34"                           
    ##  [7] "88 02 77 73 07 63 67"                        
    ##  [8] "99 65 04 28 06 16 70 92"                     
    ##  [9] "41 41 26 56 83 40 80 70 33"                  
    ## [10] "41 48 72 33 47 32 37 16 94 29"               
    ## [11] "53 71 44 65 25 43 91 52 97 51 14"            
    ## [12] "70 11 33 28 77 73 17 78 39 68 17 57"         
    ## [13] "91 71 52 38 17 14 91 43 58 50 27 29 48"      
    ## [14] "63 66 04 68 89 53 67 30 73 16 69 87 40 31"   
    ## [15] "04 62 98 27 23 09 70 98 73 93 38 53 60 04 23"

### formatting input data as matrix

``` r
triangle = str_split(input, pattern = " ")

for (i in 1:length(triangle)) {
  triangle[[i]] = as.numeric(triangle[[i]])
  vec = triangle[[i]]
  while (length(vec) < 15) vec[length(vec) + 1] = NA
  triangle[[i]] = vec
}

mat = matrix(NA, nrow = 15, ncol = 15)
for (i in 1:length(triangle)) mat[i, ] = triangle[[i]]

mat
```

    ##       [,1] [,2] [,3] [,4] [,5] [,6] [,7] [,8] [,9] [,10] [,11] [,12] [,13]
    ##  [1,]   75   NA   NA   NA   NA   NA   NA   NA   NA    NA    NA    NA    NA
    ##  [2,]   95   64   NA   NA   NA   NA   NA   NA   NA    NA    NA    NA    NA
    ##  [3,]   17   47   82   NA   NA   NA   NA   NA   NA    NA    NA    NA    NA
    ##  [4,]   18   35   87   10   NA   NA   NA   NA   NA    NA    NA    NA    NA
    ##  [5,]   20    4   82   47   65   NA   NA   NA   NA    NA    NA    NA    NA
    ##  [6,]   19    1   23   75    3   34   NA   NA   NA    NA    NA    NA    NA
    ##  [7,]   88    2   77   73    7   63   67   NA   NA    NA    NA    NA    NA
    ##  [8,]   99   65    4   28    6   16   70   92   NA    NA    NA    NA    NA
    ##  [9,]   41   41   26   56   83   40   80   70   33    NA    NA    NA    NA
    ## [10,]   41   48   72   33   47   32   37   16   94    29    NA    NA    NA
    ## [11,]   53   71   44   65   25   43   91   52   97    51    14    NA    NA
    ## [12,]   70   11   33   28   77   73   17   78   39    68    17    57    NA
    ## [13,]   91   71   52   38   17   14   91   43   58    50    27    29    48
    ## [14,]   63   66    4   68   89   53   67   30   73    16    69    87    40
    ## [15,]    4   62   98   27   23    9   70   98   73    93    38    53    60
    ##       [,14] [,15]
    ##  [1,]    NA    NA
    ##  [2,]    NA    NA
    ##  [3,]    NA    NA
    ##  [4,]    NA    NA
    ##  [5,]    NA    NA
    ##  [6,]    NA    NA
    ##  [7,]    NA    NA
    ##  [8,]    NA    NA
    ##  [9,]    NA    NA
    ## [10,]    NA    NA
    ## [11,]    NA    NA
    ## [12,]    NA    NA
    ## [13,]    NA    NA
    ## [14,]    31    NA
    ## [15,]     4    23

### solution

``` r
path.sum = function(x) {
  for (i in nrow(x):2) {
    for (j in 1:(ncol(x)-1)) x[i - 1, j] = max(x[i, j:(j + 1)]) + x[i - 1, j]
    x[i, ] = NA
  }
  return(max(x, na.rm = T))
}

path.sum(mat)
```

    ## [1] 1074
