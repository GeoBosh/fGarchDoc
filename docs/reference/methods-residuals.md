# Extract GARCH model residuals

Extracts residuals from a fitted GARCH object.

## Usage

``` r
# S4 method for class 'fGARCH'
residuals(object, standardize = FALSE)
```

## Arguments

- object:

  an object of class `"fGARCH"` as returned by
  [`garchFit`](https://geobosh.github.io/fGarchDoc/reference/garchFit.md).

- standardize:

  a logical, indicating if the residuals should be standardized.

## Details

The `"fGARCH"` method extracts the `@residuals` slot from an object of
class `"fGARCH"` as returned by the function `garchFit` and optionally
standardizes them, using conditional standard deviations.

## Author

Diethelm Wuertz for the Rmetrics R-port

## See also

[`fitted`](https://geobosh.github.io/fGarchDoc/reference/methods-fitted.md),
[`predict`](https://geobosh.github.io/fGarchDoc/reference/methods-predict.md),
[`garchFit`](https://geobosh.github.io/fGarchDoc/reference/garchFit.md),
class
[`fGARCH`](https://geobosh.github.io/fGarchDoc/reference/class-fGARCH.md),

## Examples

``` r
stopifnot(require("timeSeries"))
## Swiss Pension fund Index
data(LPP2005REC, package = "timeSeries")
x <- as.timeSeries(LPP2005REC)

## Fit LPP40 Bechmark:
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
#> <environment: 0x613d7e75d118>
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

fitted <- fitted(fit)
head(fitted)
#> 2005-11-01 2005-11-02 2005-11-03 2005-11-04 2005-11-07 2005-11-08 
#> 0.04910447 0.04910447 0.04910447 0.04910447 0.04910447 0.04910447 
class(fitted)
#> [1] "numeric"

res <- residuals(fit)
head(res)
#> [1] -0.02910647 -0.16114487  0.28265033  0.19302033  0.17555663  0.04716633
class(res)
#> [1] "numeric"
```
