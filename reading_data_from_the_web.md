Data Wrangling II: Reading Data from the Web
================
Diana Hernandez
2023-10-12

Load necessary libraries

``` r
library(tidyverse)
```

    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ dplyr     1.1.3     ✔ readr     2.1.4
    ## ✔ forcats   1.0.0     ✔ stringr   1.5.0
    ## ✔ ggplot2   3.4.3     ✔ tibble    3.2.1
    ## ✔ lubridate 1.9.2     ✔ tidyr     1.3.0
    ## ✔ purrr     1.0.2     
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

``` r
library(rvest)
```

    ## 
    ## Attaching package: 'rvest'
    ## 
    ## The following object is masked from 'package:readr':
    ## 
    ##     guess_encoding

``` r
library(httr)
```

``` r
nsduh_url = "http://samhda.s3-us-gov-west-1.amazonaws.com/s3fs-public/field-uploads/2k15StateFiles/NSDUHsaeShortTermCHG2015.htm"

nsduh_html = 
  read_html(nsduh_url)
```

`first()` gives us first one in a list. `slice()` can remove rows.

``` r
marj_use_df =
nsduh_html |>
  html_table() |>
  first() |>
  slice(-1)
```

CSS Selectors: Import Star Wars

``` r
swm_html = 
  read_html("https://www.imdb.com/list/ls070150896/")
```

Use Selector Gadget on the website…

``` r
swm_title_vec = 
  swm_html|>
    html_elements(".lister-item-header a") |>
    html_text()

swm_gross_vec = 
  swm_html|>
  html_elements(".text-muted .ghost~ .text-muted+ span") |>
    html_text()

swm_df = tibble(
  title = swm_title_vec,
  gross = swm_gross_vec
)
```

Using an API
