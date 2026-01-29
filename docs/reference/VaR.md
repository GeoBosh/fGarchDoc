# Compute Value-at-Risk (VaR) and expected shortfall (ES)

Compute Value-at-Risk (VaR) and Expected Shortfall (ES) for a fitted
GARCH-APARCH model.

## Usage

``` r
# S3 method for class 'fGARCH'
VaR(dist, p_loss = 0.05, ..., tol)

# S3 method for class 'fGARCH'
ES(dist, p_loss = 0.05, ...)
```

## Arguments

- dist:

  an object from class `"fGARCH"`, obtained from
  [`garchFit()`](https://geobosh.github.io/fGarchDoc/reference/garchFit.md).

- p_loss:

  level, default is 0.05.

- ...:

  not used.

- tol:

  tollerance

## Details

We provide methods for the generic functions
[`cvar::VaR`](https://geobosh.github.io/cvar/reference/VaR.html) and
[`cvar::ES`](https://geobosh.github.io/cvar/reference/ES.html).

## Note

We use the traditional definition of VaR as the negated lower quantile.
For example, if \\X\\ are returns on an asset, VAR\\{}\_\alpha\\ =
\\-q\_\alpha\\, where \\q\_\alpha\\ is the lower \\\alpha\\ quantile of
\\X\\. Equivalently, VAR\\{}\_\alpha\\ is equal to the lower
\\1-\alpha\\ quantile of \\-X\\ (the loss series). For details see the
vignette in package cvar availalble at
<https://cran.r-project.org/package=cvar/vignettes/Guide_cvar.pdf> (or
by calling
[`vignette("Guide_cvar", package = "cvar")`](https://geobosh.github.io/cvar/articles/Guide_cvar.pdf)).

If you wish to overlay the VaR or ES over returns, just negate the
VaR/ES, see the examples.

## See also

[`VaR`](https://geobosh.github.io/cvar/reference/VaR.html) and
[`ES`](https://geobosh.github.io/cvar/reference/ES.html) in package cvar

## Examples

``` r
## simulate a time series of returns
x <- garchSim( garchSpec(), n = 500)
class(x)
#> [1] "timeSeries"
#> attr(,"package")
#> [1] "timeSeries"
## fit a GARCH model
fit <- garchFit(~ garch(1, 1), data = x, trace = FALSE)

head(VaR(fit))
#>  2024-09-16  2024-09-17  2024-09-18  2024-09-19  2024-09-20  2024-09-21 
#> 0.005205758 0.005190033 0.005114265 0.005391635 0.005264419 0.005132978 
head(ES(fit))
#>  2024-09-16  2024-09-17  2024-09-18  2024-09-19  2024-09-20  2024-09-21 
#> 0.006534349 0.006514630 0.006419614 0.006767447 0.006607913 0.006443081 

## use plot method for fitted GARCH models
plot(fit, which = 14) # VaR

plot(fit, which = 15) # ES

plot(fit, which = 16) # VaR & ES

## plot(fit) # choose the plot interactively

## diy plots

## overlay VaR and ES over returns
## here x is from class 'timeSeries', so we convert VaR/ES to timeSeries
## don't forget to negate the result of VaR()/ES(),
plot(x)
lines(timeSeries(-VaR(fit)), col = "red")
lines(timeSeries(-ES(fit)), col = "blue")


## alternatively, plot losses (rather than returns) and don't negate VaR()/ES()
plot(-x)
lines(timeSeries(VaR(fit)), col = "red")
lines(timeSeries(ES(fit)), col = "blue")
```
