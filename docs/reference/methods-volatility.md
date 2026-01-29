# Extract GARCH model volatility

Extracts volatility from a fitted GARCH object.

## Usage

``` r
# S3 method for class 'fGARCH'
volatility(object, type = c("sigma", "h"), ...)
```

## Arguments

- object:

  an object of class `"fGARCH"` as returned by
  [`garchFit()`](https://geobosh.github.io/fGarchDoc/reference/garchFit.md).

- type:

  a character string denoting if the conditional standard deviations
  `"sigma"` or the variances `"h"` should be returned.

- ...:

  currently not used.

## Details

`volatility` is an S3 generic function for computation of volatility,
see
[`volatility`](https://geobosh.github.io/fBasicsDoc/reference/volatility.html)
for the default method.

The method for `"fGARCH"` objects, described here, extracts the
volatility from slot `@sigma.t` or `@h.t` of an `"fGARCH"` object
usually obtained from the function
[`garchFit()`](https://geobosh.github.io/fGarchDoc/reference/garchFit.md).

The class of the returned value depends on the input to the function
`garchFit` who created the object. The returned value is always of the
same class as the input object to the argument `data` in the function
`garchFit`, i.e. if you fit a `"timeSeries"` object, you will get back
from the function `fitted` also a `"timeSeries"` object, if you fit an
object of class `"zoo"`, you will get back again a `"zoo"` object. The
same holds for a `"numeric"` vector, for a `"data.frame"`, and for
objects of class `"ts", "mts"`.

In contrast, the slot itself always contains a numeric vector,
independently of the class of the input data input, i.e. the function
call `slot(object, "fitted")` will return a numeric vector.

## Author

Diethelm Wuertz for the Rmetrics R-port

## Note

(GNB) Contrary to the description of the returned value of the
`"fGARCH"` method, it is always `"numeric"`.

TODO: either implement the documented behaviour or fix the
documentation.

## Methods

Methods for `volatility` defined in package fGarch:

- object = "fGARCH":

  Extractor function for volatility or standard deviation from an object
  of class `"fGARCH"`.

## See also

[`garchFit`](https://geobosh.github.io/fGarchDoc/reference/garchFit.md),
class
[`fGARCH`](https://geobosh.github.io/fGarchDoc/reference/class-fGARCH.md)

## Examples

``` r
## Swiss Pension fund Index -
stopifnot(require("timeSeries")) # need package 'timeSeries'
x <- as.timeSeries(data(LPP2005REC, package = "timeSeries"))

fit <- garchFit(LPP40 ~ garch(1, 1), data = 100*x, trace = FALSE)
fit
#> 
#> Title:
#>  GARCH Modelling 
#> 
#> Call:
#>  garchFit(formula = LPP40 ~ garch(1, 1), data = 100 * x, trace = FALSE) 
#> 
#> Mean and Variance Equation:
#>  LPP40 ~ garch(1, 1)
#> <environment: 0x613d798b87a8>
#>  [data = 100 * x]
#> 
#> Conditional Distribution:
#>  norm 
#> 
#> Coefficient(s):
#>        mu      omega     alpha1      beta1  
#> 0.0491045  0.0083931  0.0881843  0.8016409  
#> 
#> Std. Errors:
#>  based on Hessian 
#> 
#> Error Analysis:
#>         Estimate  Std. Error  t value Pr(>|t|)    
#> mu      0.049104    0.013478    3.643 0.000269 ***
#> omega   0.008393    0.003493    2.403 0.016268 *  
#> alpha1  0.088184    0.035316    2.497 0.012524 *  
#> beta1   0.801641    0.071544   11.205  < 2e-16 ***
#> ---
#> Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
#> 
#> Log Likelihood:
#>  -38.61265    normalized:  -0.1024208 
#> 
#> Description:
#>  Thu Jan 29 21:01:08 2026 by user: georgi 
#> 

## volatility
## Standard Deviation:
vola <- volatility(fit, type = "sigma")
head(vola)
#> [1] 0.2805121 0.2674818 0.2608402 0.2645372 0.2603407 0.2558202
class(vola)
#> [1] "numeric"
## Variance:
vola <- volatility(fit, type = "h")
head(vola)
#> [1] 0.07868705 0.07154652 0.06803761 0.06997993 0.06777730 0.06544396
class(vola)
#> [1] "numeric"

## slot
vola <- slot(fit, "sigma.t")
head(vola)
#> [1] 0.2805121 0.2674818 0.2608402 0.2645372 0.2603407 0.2558202
class(vola)
#> [1] "numeric"
vola <- slot(fit, "h.t")
head(vola)
#> [1] 0.07868705 0.07154652 0.06803761 0.06997993 0.06777730 0.06544396
class(vola)
#> [1] "numeric"
```
