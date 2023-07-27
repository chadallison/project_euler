project euler problem 42: coded triangle numbers
================
chad allison \| 27 july 2023

------------------------------------------------------------------------

### setup

``` r
library(tidyverse)
options(digits = 22, scipen = 999)
```

### solution

``` r
# loading in words.txt and getting into vector format
words = str_to_lower(str_remove_all(unlist(str_split(read_file("words.txt"), ",")), "[\"\\\\]"))

# creating data frame with all words
words = data.frame(word = words)

# function to generate nth triangle number
triangle_n = function(n) {
  return(0.5 * n * (n + 1))
}

# generating first 100 triangle numbers
for (i in 1:100) {
  if (i == 1) {
    triangle_nums = triangle_n(i)
  } else {
    triangle_nums = append(triangle_nums, triangle_n(i))
  }
}

# vector of alphabet letters
alphabet = c("a", "b", "c", "d", "e", "f", "g", "h", "i", "j", "k", "l", "m",
             "n", "o", "p", "q", "r", "s", "t", "u", "v", "w", "x", "y", "z")

# function to generate a word's value
get_word_value = function(word) {
  split = unlist(str_split(word, ""))
  value = 0
  for (i in 1:length(split)) {
    value = value + which(alphabet == split[i])
  }
  return(value)
}

# function to determine if a word is a triangle word
is_triangle_word = function(word) {
  return(get_word_value(word) %in% triangle_nums)
}

# solution
words |>
  mutate(is_triangle = sapply(word, is_triangle_word)) |>
  filter(is_triangle) |>
  nrow()
```

    ## [1] 162
