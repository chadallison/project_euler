project euler problem 11: largest product in a grid
================
chad allison \| 28 december 2022

------------------------------------------------------------------------

### setup

``` r
library(tidyverse)
options(digits = 22, scipen = 999)
```

### loading input as matrix

``` r
input = scan("input.txt", quiet = T)
mat = matrix(input, ncol = 20, byrow = T)

mat
```

    ##       [,1] [,2] [,3] [,4] [,5] [,6] [,7] [,8] [,9] [,10] [,11] [,12] [,13]
    ##  [1,]    8    2   22   97   38   15    0   40    0    75     4     5     7
    ##  [2,]   49   49   99   40   17   81   18   57   60    87    17    40    98
    ##  [3,]   81   49   31   73   55   79   14   29   93    71    40    67    53
    ##  [4,]   52   70   95   23    4   60   11   42   69    24    68    56     1
    ##  [5,]   22   31   16   71   51   67   63   89   41    92    36    54    22
    ##  [6,]   24   47   32   60   99    3   45    2   44    75    33    53    78
    ##  [7,]   32   98   81   28   64   23   67   10   26    38    40    67    59
    ##  [8,]   67   26   20   68    2   62   12   20   95    63    94    39    63
    ##  [9,]   24   55   58    5   66   73   99   26   97    17    78    78    96
    ## [10,]   21   36   23    9   75    0   76   44   20    45    35    14     0
    ## [11,]   78   17   53   28   22   75   31   67   15    94     3    80     4
    ## [12,]   16   39    5   42   96   35   31   47   55    58    88    24     0
    ## [13,]   86   56    0   48   35   71   89    7    5    44    44    37    44
    ## [14,]   19   80   81   68    5   94   47   69   28    73    92    13    86
    ## [15,]    4   52    8   83   97   35   99   16    7    97    57    32    16
    ## [16,]   88   36   68   87   57   62   20   72    3    46    33    67    46
    ## [17,]    4   42   16   73   38   25   39   11   24    94    72    18     8
    ## [18,]   20   69   36   41   72   30   23   88   34    62    99    69    82
    ## [19,]   20   73   35   29   78   31   90    1   74    31    49    71    48
    ## [20,]    1   70   54   71   83   51   54   69   16    92    33    48    61
    ##       [,14] [,15] [,16] [,17] [,18] [,19] [,20]
    ##  [1,]    78    52    12    50    77    91     8
    ##  [2,]    43    69    48     4    56    62     0
    ##  [3,]    88    30     3    49    13    36    65
    ##  [4,]    32    56    71    37     2    36    91
    ##  [5,]    40    40    28    66    33    13    80
    ##  [6,]    36    84    20    35    17    12    50
    ##  [7,]    54    70    66    18    38    64    70
    ##  [8,]     8    40    91    66    49    94    21
    ##  [9,]    83    14    88    34    89    63    72
    ## [10,]    61    33    97    34    31    33    95
    ## [11,]    62    16    14     9    53    56    92
    ## [12,]    17    54    24    36    29    85    57
    ## [13,]    60    21    58    51    54    17    58
    ## [14,]    52    17    77     4    89    55    40
    ## [15,]    26    26    79    33    27    98    66
    ## [16,]    55    12    32    63    93    53    69
    ## [17,]    46    29    32    40    62    76    36
    ## [18,]    67    59    85    74     4    36    16
    ## [19,]    86    81    16    23    57     5    54
    ## [20,]    43    52     1    89    19    67    48

### calculating left-right products

``` r
max_prod_lr = 0

for (i in 1:(nrow(mat) - 3)) {
  for (j in 1:(ncol(mat) - 3)) {
    prod = mat[i, j] * mat[i, j + 1] * mat[i, j + 2] * mat[i, j + 3]
    if (prod > max_prod_lr) max_prod_lr = prod
  }
}

paste("the maximum left-right product is", max_prod_lr)
```

    ## [1] "the maximum left-right product is 48477312"

### calculating up-down products

``` r
# read the matrix by column instead of row and implement above logic
mat2 = matrix(input, ncol = 20, byrow = F)
max_prod_ud = 0

for (i in 1:(nrow(mat2) - 3)) {
  for (j in 1:(ncol(mat2) - 3)) {
    prod = mat2[i, j] * mat2[i, j + 1] * mat2[i, j + 2] * mat2[i, j + 3]
    if (prod > max_prod_ud) max_prod_ud = prod
  }
}

paste("the maximum up-down product is", max_prod_ud)
```

    ## [1] "the maximum up-down product is 51267216"

### calculating diagonal left-right products

``` r
max_prod_diag_lr = 0

for (i in 1:(nrow(mat) - 3)) {
  for (j in 1:(ncol(mat) - 3)) {
    prod = mat[i, j] * mat[i + 1, j + 1] * mat[i + 2, j + 2] * mat[i + 3, j + 3]
    if (prod > max_prod_diag_lr) max_prod_diag_lr = prod
  }
}

paste("the maximum diagonal left-right product is", max_prod_diag_lr)
```

    ## [1] "the maximum diagonal left-right product is 40304286"

### calculating diagonal right-left products

``` r
# flip matrix to read right to left, implement above logic
mat3 = mat[1:20, 20:1]
max_prod_diag_rl = 0

for (i in 1:(nrow(mat3) - 3)) {
  for (j in 1:(ncol(mat3) - 3)) {
    prod = mat3[i, j] * mat3[i + 1, j + 1] * mat3[i + 2, j + 2] * mat3[i + 3, j + 3]
    if (prod > max_prod_diag_rl) max_prod_diag_rl = prod
  }
}

paste("the maximum diagonal right-left product is", max_prod_diag_rl)
```

    ## [1] "the maximum diagonal right-left product is 70600674"

### solution

``` r
max(max_prod_lr, max_prod_ud, max_prod_diag_lr, max_prod_diag_rl)
```

    ## [1] 70600674
