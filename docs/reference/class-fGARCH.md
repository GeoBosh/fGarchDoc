# Class "fGARCH" - fitted ARMA-GARCH/APARCH models

Class 'fGARCH' represents models fitted to heteroskedastic time series,
including ARCH, GARCH, APARCH, ARMA-GARCH and ARMA-APARCH models.

## Objects from the Class

Objects from class `"fGARCH"` can be created by calls of the function
[`garchFit`](https://geobosh.github.io/fGarchDoc/reference/garchFit.md).

## Slots

- `call`::

  Object of class `"call"`, the call used to fit the model and create
  the object.

- `formula`::

  Object of class `"formula"`, a formula object representing the mean
  and variance equations.

- `method`::

  Object of class `"character"`, a string denoting the optimization
  method, by default `"Max Log-Likelihood Estimation"`.

- `data`::

  Object of class `"list"`, a list with one entry, `x`, containing the
  data of the time series to which the model is fitted.

- `fit`::

  Object of class `"list"`, a list with the results from the parameter
  estimation. The entries of the list depend on the selected algorithm,
  see below.

- `residuals`::

  Object of class `"numeric"`, the raw, unstandardized residuals.

- `fitted`::

  Object of class `"numeric"`, the fitted values.

- `h.t`::

  Object of class `"numeric"`, the conditional variances (\\h_t =
  \sigma_t^\delta\\).

- `sigma.t`::

  Object of class `"numeric"`, the conditional standard deviations.

- `title`::

  Object of class `"character"`, a title string.

- `description`::

  Object of class `"character"`, a string with a brief description.

## Methods

Besides the S4 methods described below, the are `"fGARCH"` methods (S3)
for `tsdiag`
([`tsdiag`](https://geobosh.github.io/fGarchDoc/reference/stats-tsdiag.md)),
VaR ([`VaR`](https://geobosh.github.io/fGarchDoc/reference/VaR.md)),
expected shortfall
([`ES`](https://geobosh.github.io/fGarchDoc/reference/VaR.md)),
volatility
([`volatility`](https://geobosh.github.io/fGarchDoc/reference/methods-volatility.md)),
and maybe others.

- plot:

  `signature(x = "fGARCH", y = "missing")`: plots an object of class
  `"fGARCH"`, see the
  [`help page`](https://geobosh.github.io/fGarchDoc/reference/methods-plot.md)
  of the method for details and options.

- show:

  `signature(object = "fGARCH")`: prints the object.

- summary:

  `signature(object = "fGARCH")`: summarizes the object. The
  [`help page`](https://geobosh.github.io/fGarchDoc/reference/methods-summary.md)
  of the `"fGARCH"` method gives details on the output, as well as
  interpretation of the results.

- predict:

  `signature(object = "fGARCH")`: Computes forecasts of the mean and
  some measures of risk (such as volatility, value-at-risk and expected
  shortfall), see the method's
  [`help page`](https://geobosh.github.io/fGarchDoc/reference/methods-predict.md)
  for full details.

- fitted:

  `signature(object = "fGARCH")`: extracts fitted values from the object
  ([`help page`](https://geobosh.github.io/fGarchDoc/reference/methods-fitted.md)).

- residuals:

  `signature(object = "fGARCH")`: returns residuals from the fitted
  model
  ([`help page`](https://geobosh.github.io/fGarchDoc/reference/methods-residuals.md)).

- coef:

  `signature(object = "fGARCH")`: extracts the estimated coefficients
  ([`help page`](https://geobosh.github.io/fGarchDoc/reference/methods-coef.md)).

- formula:

  `signature(x = "fGARCH")`: extracts the formula expression, see the
  method's
  [`help page`](https://geobosh.github.io/fGarchDoc/reference/methods-formula.md).

- update:

  `signature(object = "fGARCH")`: ...

## Author

Diethelm Wuertz and Rmetrics Core Team

## See also

[`garchFit`](https://geobosh.github.io/fGarchDoc/reference/garchFit.md),
[`garchSpec`](https://geobosh.github.io/fGarchDoc/reference/garchSpec.md),
[`garchFitControl`](https://geobosh.github.io/fGarchDoc/reference/garchFitControl.md)

## Examples

``` r
## simulate a time series, fit a GARCH(1,1) model, and show it:
x <- garchSim( garchSpec(), n = 500)
fit <- garchFit(~ garch(1, 1), data = x, trace = FALSE)
coef(fit)
#>            mu         omega        alpha1         beta1 
#> -1.311144e-04  1.288087e-06  8.792572e-02  7.803781e-01 
summary(fit)
#> 
#> Title:
#>  GARCH Modelling 
#> 
#> Call:
#>  garchFit(formula = ~garch(1, 1), data = x, trace = FALSE) 
#> 
#> Mean and Variance Equation:
#>  data ~ garch(1, 1)
#> <environment: 0x613d7bc7d178>
#>  [data = x]
#> 
#> Conditional Distribution:
#>  norm 
#> 
#> Coefficient(s):
#>          mu        omega       alpha1        beta1  
#> -1.3111e-04   1.2881e-06   8.7926e-02   7.8038e-01  
#> 
#> Std. Errors:
#>  based on Hessian 
#> 
#> Error Analysis:
#>          Estimate  Std. Error  t value Pr(>|t|)    
#> mu     -1.311e-04   1.338e-04   -0.980   0.3272    
#> omega   1.288e-06   8.186e-07    1.573   0.1156    
#> alpha1  8.793e-02   3.955e-02    2.223   0.0262 *  
#> beta1   7.804e-01   1.038e-01    7.518 5.57e-14 ***
#> ---
#> Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
#> 
#> Log Likelihood:
#>  2183.772    normalized:  4.367544 
#> 
#> Description:
#>  Thu Jan 29 21:01:04 2026 by user: georgi 
#> 
#> 
#> 
#> Standardised Residuals Tests:
#>                                  Statistic    p-Value
#>  Jarque-Bera Test   R    Chi^2   0.8749564 0.64566259
#>  Shapiro-Wilk Test  R    W       0.9978536 0.78316127
#>  Ljung-Box Test     R    Q(10)  17.8536807 0.05748257
#>  Ljung-Box Test     R    Q(15)  24.2180027 0.06148270
#>  Ljung-Box Test     R    Q(20)  25.8442849 0.17101649
#>  Ljung-Box Test     R^2  Q(10)  13.1441777 0.21572205
#>  Ljung-Box Test     R^2  Q(15)  14.9334373 0.45622242
#>  Ljung-Box Test     R^2  Q(20)  19.3320156 0.50034833
#>  LM Arch Test       R    TR^2   13.9249937 0.30552369
#> 
#> Information Criterion Statistics:
#>       AIC       BIC       SIC      HQIC 
#> -8.719089 -8.685372 -8.719216 -8.705859 
#> 
fit # == print(fit) and also == show(fit)
#> 
#> Title:
#>  GARCH Modelling 
#> 
#> Call:
#>  garchFit(formula = ~garch(1, 1), data = x, trace = FALSE) 
#> 
#> Mean and Variance Equation:
#>  data ~ garch(1, 1)
#> <environment: 0x613d7bc7d178>
#>  [data = x]
#> 
#> Conditional Distribution:
#>  norm 
#> 
#> Coefficient(s):
#>          mu        omega       alpha1        beta1  
#> -1.3111e-04   1.2881e-06   8.7926e-02   7.8038e-01  
#> 
#> Std. Errors:
#>  based on Hessian 
#> 
#> Error Analysis:
#>          Estimate  Std. Error  t value Pr(>|t|)    
#> mu     -1.311e-04   1.338e-04   -0.980   0.3272    
#> omega   1.288e-06   8.186e-07    1.573   0.1156    
#> alpha1  8.793e-02   3.955e-02    2.223   0.0262 *  
#> beta1   7.804e-01   1.038e-01    7.518 5.57e-14 ***
#> ---
#> Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
#> 
#> Log Likelihood:
#>  2183.772    normalized:  4.367544 
#> 
#> Description:
#>  Thu Jan 29 21:01:04 2026 by user: georgi 
#> 
```
