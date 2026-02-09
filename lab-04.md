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

…

### Exercise 4

…

### Exercise 5

…

### Exercise 6

…

Add exercise headings as needed.
