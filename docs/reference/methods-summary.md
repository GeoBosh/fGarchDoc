# fGARCH method for the summary function

Prints a summary of an object from class `"fGARCH"`. The summary
contains information about the parameters of the fitted model, its
specifications, and diagnostic statistics for inference and
goodness-of-fit. If you don't need the diagnostics, just print the
object (instead of calling `summary`).

## Methods

Methods for `summary` defined in package fGarch:

- object = "fGARCH":

  Summary function for objects of class `"fGARCH"`.

## Value

an object from class `"summary_fGARCH"`

## How to read a diagnostic summary report?

The first five sections give the title, the call, the mean and variance
formula, the conditional distribution and the type of standard errors:

            Title:
             GARCH Modelling

            Call:
             garchFit(~ garch(1, 1), data = garchSim(), trace = FALSE)

            Mean and Variance Equation:
             ~arch(0)

            Conditional Distribution:
             norm

            Std. Errors:
             based on Hessian
            

The next three sections return the estimated coefficients and an error
analysis including standard errors, t values, and probabilities, as well
as the log Likelihood values from optimization:

            Coefficient(s):
                      mu         omega        alpha1         beta1
            -5.79788e-05   7.93017e-06   1.59456e-01   2.30772e-01

            Error Analysis:
                     Estimate  Std. Error  t value Pr(>|t|)
            mu     -5.798e-05   2.582e-04   -0.225    0.822
            omega   7.930e-06   5.309e-06    1.494    0.135
            alpha1  1.595e-01   1.026e-01    1.554    0.120
            beta1   2.308e-01   4.203e-01    0.549    0.583

            Log Likelihood:
             -843.3991    normalized:  -Inf
            

The next section provides results on standardized residuals tests,
including statistic and p values, and on information criterion statistic
including AIC, BIC, SIC, and HQIC:

            Standardized Residuals Tests:
                                            Statistic p-Value
             Jarque-Bera Test   R    Chi^2  0.4172129 0.8117146
             Shapiro-Wilk Test  R    W      0.9957817 0.8566985
             Ljung-Box Test     R    Q(10)  13.05581  0.2205680
             Ljung-Box Test     R    Q(15)  14.40879  0.4947788
             Ljung-Box Test     R    Q(20)  38.15456  0.008478302
             Ljung-Box Test     R^2  Q(10)  7.619134  0.6659837
             Ljung-Box Test     R^2  Q(15)  13.89721  0.5333388
             Ljung-Box Test     R^2  Q(20)  15.61716  0.7400728
             LM Arch Test       R    TR^2   7.049963  0.8542942

            Information Criterion Statistics:
                     AIC      BIC      SIC     HQIC
                8.473991 8.539957 8.473212 8.500687
            

## Author

Diethelm Wuertz for the Rmetrics R-port

## See also

[`tsdiag`](https://geobosh.github.io/fGarchDoc/reference/stats-tsdiag.md)
and
[`plot`](https://geobosh.github.io/fGarchDoc/reference/methods-plot.md)
for further diagnostics and plots,

[`garchFit`](https://geobosh.github.io/fGarchDoc/reference/garchFit.md)
for fitting GARCH/APARCH models,

class
`"`[`fGARCH`](https://geobosh.github.io/fGarchDoc/reference/class-fGARCH.md)`"`
for details and further methods

## Examples

``` r
x <- garchSim(n = 200)
fit <- garchFit(formula = x ~ garch(1, 1), data = x, trace = FALSE)
summary(fit)
#> 
#> Title:
#>  GARCH Modelling 
#> 
#> Call:
#>  garchFit(formula = x ~ garch(1, 1), data = x, trace = FALSE) 
#> 
#> Mean and Variance Equation:
#>  data ~ garch(1, 1)
#> <environment: 0x613d7dbb1798>
#>  [data = x]
#> 
#> Conditional Distribution:
#>  norm 
#> 
#> Coefficient(s):
#>         mu       omega      alpha1       beta1  
#> 2.4457e-04  5.1170e-07  6.9308e-02  8.8130e-01  
#> 
#> Std. Errors:
#>  based on Hessian 
#> 
#> Error Analysis:
#>         Estimate  Std. Error  t value Pr(>|t|)    
#> mu     2.446e-04   2.063e-04    1.185    0.236    
#> omega  5.117e-07   3.983e-07    1.285    0.199    
#> alpha1 6.931e-02   3.906e-02    1.774    0.076 .  
#> beta1  8.813e-01   5.835e-02   15.104   <2e-16 ***
#> ---
#> Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
#> 
#> Log Likelihood:
#>  875.212    normalized:  4.37606 
#> 
#> Description:
#>  Thu Jan 29 21:01:08 2026 by user: georgi 
#> 
#> 
#> 
#> Standardised Residuals Tests:
#>                                 Statistic    p-Value
#>  Jarque-Bera Test   R    Chi^2   4.330425 0.11472556
#>  Shapiro-Wilk Test  R    W       0.990428 0.20618083
#>  Ljung-Box Test     R    Q(10)  13.455200 0.19932236
#>  Ljung-Box Test     R    Q(15)  27.766018 0.02308043
#>  Ljung-Box Test     R    Q(20)  31.358634 0.05063043
#>  Ljung-Box Test     R^2  Q(10)  13.832163 0.18078576
#>  Ljung-Box Test     R^2  Q(15)  29.464189 0.01400719
#>  Ljung-Box Test     R^2  Q(20)  31.448108 0.04954583
#>  LM Arch Test       R    TR^2   13.323871 0.34594640
#> 
#> Information Criterion Statistics:
#>       AIC       BIC       SIC      HQIC 
#> -8.712120 -8.646153 -8.712899 -8.685424 
#> 
```
