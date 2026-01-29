# GARCH coefficients methods

Coefficients methods `coef()` for GARCH Models.

## Methods

Methods for `coef` defined in package fGarch:

- object = "fGARCH":

  Extractor function for coefficients from a fitted GARCH model.

- object = "fGARCHSPEC":

  Extractor function for coefficients from a GARCH specification
  structure.

## Note

`coef` is a generic function which extracts coefficients from objects
returned by modeling functions.

## Author

Diethelm Wuertz for the Rmetrics R-port

## Examples

``` r
# Use default parameters beside alpha:
spec <- garchSpec(model = list(alpha = c(0.05, 0.05)))
spec
#> 
#> Formula: 
#>  ~ garch(2, 1)
#> Model:
#>  omega: 1e-06
#>  alpha: 0.05 0.05
#>  beta:  0.8
#> Distribution: 
#>  norm
#> Presample: 
#>   time          z     h y
#> 1   -1 -0.3853194 1e-05 0
#> 2    0 -0.3488880 1e-05 0
coef(spec)
#>  omega alpha1 alpha2 gamma1 gamma2   beta     mu     ar     ma  delta 
#>  1e-06  5e-02  5e-02  0e+00  0e+00  8e-01  0e+00  0e+00  0e+00  2e+00 
#> attr(,"distribution")
#> [1] "norm"

## Simulate an univariate "timeSeries" series from specification 'spec':
x <- garchSim(spec, n = 2000)
x <- x[,1]

fit <- garchFit( ~ garch(1, 1), data = x, trace = FALSE)
coef(fit)
#>           mu        omega       alpha1        beta1 
#> 2.291034e-05 1.051494e-06 9.538329e-02 8.000716e-01 
```
