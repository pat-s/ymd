
<!-- README.md is generated from README.Rmd. Please edit that file -->
# ymd

<!-- badges: start -->
[![R-CMD-check](https://github.com/shrektan/ymd/workflows/R-CMD-check/badge.svg)](https://github.com/shrektan/ymd/actions) <!-- badges: end -->

Handle common ymd Date Operations in R using Rust. It converts ymd integers or strings to Date, e.g., `211225` to `as.Date("2021-12-25")` and it provides addition helper functions like bop or eop (quick finding the begining or ending of period, e.g., the 1st date of the year or month).

It's similar to the `lubridate` package but will be much lighter and focusing on Date objects.

``` r
x <- c("210101", "21/02/03", "89-1-03", "1989.03.05")
x <- rep(x, 100)
bench::mark(
  ymd::ymd(x),
  lubridate::ymd(x), time_unit = "us"
)
#> # A tibble: 2 × 6
#>   expression           min median `itr/sec` mem_alloc `gc/sec`
#>   <bch:expr>         <dbl>  <dbl>     <dbl> <bch:byt>    <dbl>
#> 1 ymd::ymd(x)         32.7   33.2    29782.   209.5KB      0  
#> 2 lubridate::ymd(x) 1833.  1878.       530.     8.2MB     19.9

x <- c(210101, 210224, 211231, 19890103)
x <- rep(x, 100)
bench::mark(
  ymd::ymd(x),
  lubridate::ymd(x), time_unit = "us"
)
#> # A tibble: 2 × 6
#>   expression           min median `itr/sec` mem_alloc `gc/sec`
#>   <bch:expr>         <dbl>  <dbl>     <dbl> <bch:byt>    <dbl>
#> 1 ymd::ymd(x)         12.1   12.7    77510.    3.17KB      0  
#> 2 lubridate::ymd(x) 1683.  1711.       583.  373.41KB     21.9
```
