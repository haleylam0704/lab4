Lab 04 - La Quinta is Spanish for next to Denny’s, Pt. 1
================
Haley Lam
2/9/2025

### Load packages and data

``` r
library(tidyverse) 
library(dsbox) 
```

``` r
states <- read_csv("data/states.csv")
```

### Exercise 1

``` r
data(dennys)
dennys <- dennys

nrow(dennys)
```

    ## [1] 1643

``` r
ncol(dennys)
```

    ## [1] 6

There are 1643 rows and 6 columns.

Each row is a location of Dennys, and columns are the details of each
location.

### Exercise 2

``` r
data(laquinta)
laquinta <- laquinta

nrow(laquinta)
```

    ## [1] 909

``` r
ncol(laquinta)
```

    ## [1] 6

There are 909 rows and 6 columns.

Each row represents a location of La Quinta, and columns are details of
each location.

### Exercise 3

There are some La Quintas outside of the US: Canada, Mexico, China, New
Zealand, Georgia, Turkiye, UAE, Columbia, Ecuador

I don’t see any Denny’s outside of US on the website.

### Exercise 4

One idea is to count NA values for the “state” columns.

### Exercise 5

``` r
dennys %>%
  filter(!(state %in% states$abbreviation))
```

    ## # A tibble: 0 × 6
    ## # ℹ 6 variables: address <chr>, city <chr>, state <chr>, zip <chr>,
    ## #   longitude <dbl>, latitude <dbl>

There are no Dennys outside of the US

…

### Exercise 6

…

Add exercise headings as needed.

### Exercise 7

laquinta %\>% filter(!(state %in% states\$abbreviation))
