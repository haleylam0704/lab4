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

``` r
dennys <- dennys %>%
  mutate(country = "United States")
```

### Exercise 7

``` r
laquinta %>%
  filter(!(state %in% states$abbreviation))
```

    ## # A tibble: 14 × 6
    ##    address                                  city  state zip   longitude latitude
    ##    <chr>                                    <chr> <chr> <chr>     <dbl>    <dbl>
    ##  1 Carretera Panamericana Sur KM 12         "\nA… AG    20345    -102.     21.8 
    ##  2 Av. Tulum Mza. 14 S.M. 4 Lote 2          "\nC… QR    77500     -86.8    21.2 
    ##  3 Ejercito Nacional 8211                   "Col… CH    32528    -106.     31.7 
    ##  4 Blvd. Aeropuerto 4001                    "Par… NL    66600    -100.     25.8 
    ##  5 Carrera 38 # 26-13 Avenida las Palmas c… "\nM… ANT   0500…     -75.6     6.22
    ##  6 AV. PINO SUAREZ No. 1001                 "Col… NL    64000    -100.     25.7 
    ##  7 Av. Fidel Velazquez #3000 Col. Central   "\nM… NL    64190    -100.     25.7 
    ##  8 63 King Street East                      "\nO… ON    L1H1…     -78.9    43.9 
    ##  9 Calle Las Torres-1 Colonia Reforma       "\nP… VE    93210     -97.4    20.6 
    ## 10 Blvd. Audi N. 3 Ciudad Modelo            "\nS… PU    75010     -97.8    19.2 
    ## 11 Ave. Zeta del Cochero No 407             "Col… PU    72810     -98.2    19.0 
    ## 12 Av. Benito Juarez 1230 B (Carretera 57)… "\nS… SL    78399    -101.     22.1 
    ## 13 Blvd. Fuerza Armadas                     "con… FM    11101     -87.2    14.1 
    ## 14 8640 Alexandra Rd                        "\nR… BC    V6X1…    -123.     49.2

Peru, Mexico, Columbia, Canada, Honduras

### Exercise 8

``` r
laquinta <- laquinta %>%
  mutate(country = case_when(
    state %in% state.abb ~ "United States",
    state %in% c("ON", "BC") ~ "Canada",
    state == "ANT" ~ "Colombia",
    state == "AG" ~ "Peru",
    state %in% c("QR", "CH", "NL", "VE", "PU") ~ "Mexico",
    state == "FM" ~ "Hondorus")
  )
```

``` r
laquinta <- laquinta %>%
  filter(country == "United States")
```

### Exercise 9

``` r
dennys %>%
  count(state, sort = TRUE)
```

    ## # A tibble: 51 × 2
    ##    state     n
    ##    <chr> <int>
    ##  1 CA      403
    ##  2 TX      200
    ##  3 FL      140
    ##  4 AZ       83
    ##  5 IL       56
    ##  6 NY       56
    ##  7 WA       49
    ##  8 OH       44
    ##  9 MO       42
    ## 10 PA       40
    ## # ℹ 41 more rows

``` r
laquinta %>%
  count(state, sort = TRUE)
```

    ## # A tibble: 48 × 2
    ##    state     n
    ##    <chr> <int>
    ##  1 TX      237
    ##  2 FL       74
    ##  3 CA       56
    ##  4 GA       41
    ##  5 TN       30
    ##  6 OK       29
    ##  7 LA       28
    ##  8 CO       27
    ##  9 NM       19
    ## 10 NY       19
    ## # ℹ 38 more rows

California, Texas, and Florida have the most Dennys. Delaware, Vermont,
and DC (District of Columbia?) have the least.

This is not surprising, because TX, CA, and FL are huge with many
people!

``` r
new_dn <- dennys %>%
  count(state) %>%
  inner_join(states, by = c("state" = "abbreviation"))

new_lq <- laquinta %>%
  count(state) %>%
  inner_join(states, by = c("state" = "abbreviation"))
```

### Exercise 10

``` r
new_dn %>%
  mutate(ratio = n / area) %>%
  arrange(desc(ratio))
```

    ## # A tibble: 51 × 5
    ##    state     n name                     area    ratio
    ##    <chr> <int> <chr>                   <dbl>    <dbl>
    ##  1 DC        2 District of Columbia     68.3 0.0293  
    ##  2 RI        5 Rhode Island           1545.  0.00324 
    ##  3 CA      403 California           163695.  0.00246 
    ##  4 CT       12 Connecticut            5543.  0.00216 
    ##  5 FL      140 Florida               65758.  0.00213 
    ##  6 MD       26 Maryland              12406.  0.00210 
    ##  7 NJ       10 New Jersey             8723.  0.00115 
    ##  8 NY       56 New York              54555.  0.00103 
    ##  9 IN       37 Indiana               36420.  0.00102 
    ## 10 OH       44 Ohio                  44826.  0.000982
    ## # ℹ 41 more rows

``` r
new_lq %>%
  mutate(ratio = n / area) %>%
  arrange(desc(ratio))
```

    ## # A tibble: 48 × 5
    ##    state     n name             area    ratio
    ##    <chr> <int> <chr>           <dbl>    <dbl>
    ##  1 RI        2 Rhode Island    1545. 0.00129 
    ##  2 FL       74 Florida        65758. 0.00113 
    ##  3 CT        6 Connecticut     5543. 0.00108 
    ##  4 MD       13 Maryland       12406. 0.00105 
    ##  5 TX      237 Texas         268596. 0.000882
    ##  6 TN       30 Tennessee      42144. 0.000712
    ##  7 GA       41 Georgia        59425. 0.000690
    ##  8 NJ        5 New Jersey      8723. 0.000573
    ##  9 MA        6 Massachusetts  10554. 0.000568
    ## 10 LA       28 Louisiana      52378. 0.000535
    ## # ℹ 38 more rows

DoC, Rhode Island, and Calirfornia are the states with the most Dennys
per sq mile.

Rhode Island, Florida, and Connecticut are states with the most La
Quintas per sq mile.

``` r
dennys <- dennys %>%
  mutate(establishment = "Denny's")
laquinta <- laquinta %>%
  mutate(establishment = "La Quinta")

dn_lq <- bind_rows(dennys, laquinta)
```

``` r
ggplot(dn_lq, mapping = aes(
  x = longitude,
  y = latitude,
  color = establishment
)) +
  geom_point()
```

![](lab-04_files/figure-gfm/unnamed-chunk-13-1.png)<!-- -->

### Exercise 11

``` r
dn_lq %>% 
  filter(state == "NC") %>%
  ggplot(dn_lq, mapping = aes(
  x = longitude,
  y = latitude,
  color = establishment
)) +
  geom_point()
```

![](lab-04_files/figure-gfm/unnamed-chunk-14-1.png)<!-- --> I think it
looks mostly true when looking at where there exist La Quintas (i.e.,
whenever there’s a La Quinta, right next to it there is also usually a
Denny’s).

### Exercise 12

``` r
dn_lq %>% 
  filter(state == "TX") %>%
  ggplot(dn_lq, mapping = aes(
  x = longitude,
  y = latitude,
  color = establishment
)) +
  geom_point()
```

![](lab-04_files/figure-gfm/unnamed-chunk-15-1.png)<!-- --> It does seem
like a lot of Denny’s are right next to La Quintas, but there are also
many La Quinta locations that don’t have Denny’s next to them (unless
they’re right on top of each other!). There are odd clusters of La
Quintas and Denny’s, though.
