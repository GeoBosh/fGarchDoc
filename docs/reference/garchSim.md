# Simulate univariate GARCH/APARCH time series

Simulates univariate GARCH/APARCH time series.

## Usage

``` r
garchSim(spec = garchSpec(), n = 100, n.start = 100, extended = FALSE)
```

## Arguments

- spec:

  a specification object of class
  `"`[`fGARCHSPEC`](https://geobosh.github.io/fGarchDoc/reference/class-fGARCHSPEC.md)`"`
  as returned by
  [`garchSpec`](https://geobosh.github.io/fGarchDoc/reference/garchSpec.md).
  See also below for further details.

- n:

  length of the output series, an integer value, by default `n=100`.

- n.start:

  length of ‘burn-in’ period, by default 100.

- extended:

  logical parameter specifying what to return. If `FALSE`, return the
  univariate GARCH/APARCH time series. If `TRUE`, return a multivariate
  time series containing also the volatility and conditional innovations
  time series.

## Details

`garchSim` simulates an univariate GARCH or APARCH time series process
as specified by argument `spec`. The default model specifies
Bollerslev's GARCH(1,1) model with normally distributed innovations.

`spec` is an object of class `"fGARCHSPEC"` as returned by the function
[`garchSpec`](https://geobosh.github.io/fGarchDoc/reference/garchSpec.md).
It comes with a slot `@model` which is a list of just the numeric
parameter entries. These are recognized and extracted for use by the
function `garchSim`.

One can estimate the parameters of a GARCH process from empirical data
using the function `garchFit` and then simulate statistically equivalent
GARCH processes with the same set of model parameters using the function
`garchSim`.

## Value

the simulated time series as an objects of class `"timeSeries"` with
attribute `"spec"` containing the specification of the model.

If `extended` is `TRUE`, then the time series is multivariate and
contains also the volatility, `sigma`, and the conditional innovations,
`eps`.

## Note

An undocumented feature (so, it should not be relied on) is that the
returned time series is timed so that the last observation is the day
before the date when the function is executed. This probably should be
controlled by an additional argument in `garchSim`.

## Author

Diethelm Wuertz for the Rmetrics R-port

## See also

[`garchSpec`](https://geobosh.github.io/fGarchDoc/reference/garchSpec.md),
[`garchFit`](https://geobosh.github.io/fGarchDoc/reference/garchFit.md)

## Examples

``` r
## default garch model
spec <- garchSpec()
spec
#> 
#> Formula: 
#>  ~ garch(1, 1)
#> Model:
#>  omega: 1e-06
#>  alpha: 0.1
#>  beta:  0.8
#> Distribution: 
#>  norm
#> Presample: 
#>   time          z     h y
#> 1    0 -0.2367119 1e-05 0

x <- garchSim(spec, n = 50)
class(x)
#> [1] "timeSeries"
#> attr(,"package")
#> [1] "timeSeries"
print(x) 
#> GMT 
#>                    garch
#> 2025-12-10  2.293456e-03
#> 2025-12-11 -5.724565e-03
#> 2025-12-12 -5.579291e-03
#> 2025-12-13 -3.053226e-03
#> 2025-12-14 -5.901105e-03
#> 2025-12-15  1.982991e-03
#> 2025-12-16  2.311325e-04
#> 2025-12-17  1.591034e-03
#> 2025-12-18 -1.844241e-03
#> 2025-12-19  2.327274e-03
#> 2025-12-20 -2.810580e-03
#> 2025-12-21  4.083680e-03
#> 2025-12-22 -1.981109e-03
#> 2025-12-23 -2.736583e-03
#> 2025-12-24 -3.197632e-03
#> 2025-12-25 -2.687409e-03
#> 2025-12-26 -4.503116e-04
#> 2025-12-27 -9.716605e-04
#> 2025-12-28  1.665777e-03
#> 2025-12-29 -2.800591e-03
#> 2025-12-30  1.205845e-03
#> 2025-12-31  8.911127e-04
#> 2026-01-01 -3.355606e-03
#> 2026-01-02  6.375045e-04
#> 2026-01-03  6.992215e-03
#> 2026-01-04  2.302708e-03
#> 2026-01-05 -2.773734e-05
#> 2026-01-06 -6.103605e-03
#> 2026-01-07 -2.646679e-03
#> 2026-01-08  9.828453e-04
#> 2026-01-09  2.199372e-03
#> 2026-01-10 -1.669151e-03
#> 2026-01-11  4.976765e-04
#> 2026-01-12  1.773448e-03
#> 2026-01-13  4.240135e-04
#> 2026-01-14  2.872468e-03
#> 2026-01-15 -4.483632e-03
#> 2026-01-16  4.522951e-03
#> 2026-01-17 -5.253080e-03
#> 2026-01-18  1.227027e-03
#> 2026-01-19  5.491889e-03
#> 2026-01-20 -2.600418e-03
#> 2026-01-21  2.780861e-03
#> 2026-01-22  3.701203e-03
#> 2026-01-23  6.088748e-03
#> 2026-01-24 -1.635551e-03
#> 2026-01-25  1.800426e-03
#> 2026-01-26  5.328106e-03
#> 2026-01-27  1.903535e-03
#> 2026-01-28 -3.040495e-03
   
## More simulations ...

## Default GARCH(1,1) - uses default parameter settings
spec <- garchSpec(model = list())
garchSim(spec, n = 10)
#> GMT 
#>                    garch
#> 2026-01-19 -4.830059e-03
#> 2026-01-20 -1.673998e-03
#> 2026-01-21  4.252527e-03
#> 2026-01-22  1.028559e-03
#> 2026-01-23 -1.439446e-03
#> 2026-01-24  6.829775e-05
#> 2026-01-25  5.870646e-03
#> 2026-01-26  3.393152e-03
#> 2026-01-27  3.205573e-03
#> 2026-01-28 -2.040141e-03

## ARCH(2) - use default omega and specify alpha, set beta=0!
spec <- garchSpec(model = list(alpha = c(0.2, 0.4), beta = 0))
garchSim(spec, n = 10)
#> GMT 
#>                    garch
#> 2026-01-19  0.0017927422
#> 2026-01-20 -0.0008625608
#> 2026-01-21  0.0010001187
#> 2026-01-22  0.0030832726
#> 2026-01-23 -0.0018462440
#> 2026-01-24 -0.0023798962
#> 2026-01-25  0.0008704696
#> 2026-01-26  0.0007833472
#> 2026-01-27 -0.0003016249
#> 2026-01-28 -0.0005002815

## AR(1)-ARCH(2) - use default mu, omega
spec <- garchSpec(model = list(ar = 0.5, alpha = c(0.3, 0.4), beta = 0))
garchSim(spec, n = 10)
#> GMT 
#>                    garch
#> 2026-01-19 -0.0007531555
#> 2026-01-20 -0.0022603821
#> 2026-01-21 -0.0018410996
#> 2026-01-22 -0.0006229702
#> 2026-01-23 -0.0003279921
#> 2026-01-24  0.0012915726
#> 2026-01-25  0.0019140520
#> 2026-01-26  0.0005515873
#> 2026-01-27  0.0004785214
#> 2026-01-28  0.0002537728

## AR([1,5])-GARCH(1,1) - use default garch values and subset ar[.]
spec <- garchSpec(model = list(mu = 0.001, ar = c(0.5,0,0,0,0.1)))
garchSim(spec, n = 10)
#> GMT 
#>                    garch
#> 2026-01-19 -0.0002870178
#> 2026-01-20 -0.0011077595
#> 2026-01-21 -0.0031293703
#> 2026-01-22 -0.0017970960
#> 2026-01-23  0.0037490015
#> 2026-01-24  0.0057034834
#> 2026-01-25  0.0036035560
#> 2026-01-26  0.0039249403
#> 2026-01-27  0.0025426208
#> 2026-01-28  0.0014967001

## ARMA(1,2)-GARCH(1,1) - use default garch values
spec <- garchSpec(model = list(ar = 0.5, ma = c(0.3, -0.3)))  
garchSim(spec, n = 10)
#> GMT 
#>                    garch
#> 2026-01-19 -0.0001591027
#> 2026-01-20  0.0019475104
#> 2026-01-21 -0.0010304485
#> 2026-01-22 -0.0030496416
#> 2026-01-23  0.0052197237
#> 2026-01-24  0.0022934952
#> 2026-01-25  0.0044816955
#> 2026-01-26  0.0024859770
#> 2026-01-27  0.0005256349
#> 2026-01-28  0.0007577916

## GARCH(1,1) - use default omega and specify alpha/beta
spec <- garchSpec(model = list(alpha = 0.2, beta = 0.7))
garchSim(spec, n = 10)
#> GMT 
#>                    garch
#> 2026-01-19 -0.0030764300
#> 2026-01-20 -0.0037004645
#> 2026-01-21  0.0004573765
#> 2026-01-22  0.0018448485
#> 2026-01-23 -0.0021326538
#> 2026-01-24  0.0010830056
#> 2026-01-25 -0.0026793968
#> 2026-01-26  0.0014976261
#> 2026-01-27 -0.0023784895
#> 2026-01-28  0.0007910640

## GARCH(1,1) - specify omega/alpha/beta
spec <- garchSpec(model = list(omega = 1e-6, alpha = 0.1, beta = 0.8))
garchSim(spec, n = 10)
#> GMT 
#>                    garch
#> 2026-01-19  0.0032089890
#> 2026-01-20  0.0038018266
#> 2026-01-21  0.0022089174
#> 2026-01-22 -0.0007191505
#> 2026-01-23 -0.0004469077
#> 2026-01-24  0.0006013886
#> 2026-01-25 -0.0019554474
#> 2026-01-26 -0.0010905869
#> 2026-01-27  0.0007800873
#> 2026-01-28 -0.0034663114

## GARCH(1,2) - use default omega and specify alpha[1]/beta[2]
spec <- garchSpec(model = list(alpha = 0.1, beta = c(0.4, 0.4)))
garchSim(spec, n = 10)
#> GMT 
#>                    garch
#> 2026-01-19  0.0010577379
#> 2026-01-20 -0.0016142721
#> 2026-01-21  0.0006535505
#> 2026-01-22  0.0008639670
#> 2026-01-23  0.0026345611
#> 2026-01-24 -0.0010614903
#> 2026-01-25 -0.0011161837
#> 2026-01-26  0.0004583592
#> 2026-01-27  0.0023333481
#> 2026-01-28 -0.0037440396

## GARCH(2,1) - use default omega and specify alpha[2]/beta[1]
spec <- garchSpec(model = list(alpha = c(0.12, 0.04), beta = 0.08))
garchSim(spec, n = 10)
#> GMT 
#>                    garch
#> 2026-01-19 -0.0009540200
#> 2026-01-20  0.0003912605
#> 2026-01-21 -0.0018874914
#> 2026-01-22 -0.0001231150
#> 2026-01-23  0.0013522007
#> 2026-01-24  0.0007294251
#> 2026-01-25  0.0025261514
#> 2026-01-26  0.0004799199
#> 2026-01-27 -0.0020227883
#> 2026-01-28 -0.0008739593

## snorm-ARCH(1) - use defaults with skew Normal
spec <- garchSpec(model = list(beta = 0, skew = 0.8), cond.dist = "snorm")
garchSim(spec, n = 10)
#> GMT 
#>                    garch
#> 2026-01-19 -0.0005238778
#> 2026-01-20  0.0004031428
#> 2026-01-21  0.0009646549
#> 2026-01-22  0.0010711402
#> 2026-01-23  0.0001962504
#> 2026-01-24 -0.0007422212
#> 2026-01-25 -0.0005590742
#> 2026-01-26  0.0006256405
#> 2026-01-27 -0.0002550782
#> 2026-01-28  0.0003393966

## sged-GARCH(1,1) - using defaults with skew GED
model = garchSpec(model = list(skew = 0.93, shape = 3), cond.dist = "sged")
garchSim(model, n = 10)
#> GMT 
#>                    garch
#> 2026-01-19  0.0013291707
#> 2026-01-20  0.0016032978
#> 2026-01-21  0.0020813099
#> 2026-01-22 -0.0029451222
#> 2026-01-23 -0.0016848480
#> 2026-01-24 -0.0020145022
#> 2026-01-25 -0.0002782589
#> 2026-01-26  0.0015856048
#> 2026-01-27  0.0029872444
#> 2026-01-28  0.0033366976

## Taylor Schwert GARCH(1,1) - this belongs to the family of APARCH Models
spec <- garchSpec(model = list(delta = 1))
garchSim(spec, n = 10)
#> GMT 
#>                    garch
#> 2026-01-19 -1.575025e-06
#> 2026-01-20 -7.708141e-06
#> 2026-01-21 -1.477750e-06
#> 2026-01-22 -8.557501e-06
#> 2026-01-23 -5.101197e-06
#> 2026-01-24  9.565472e-06
#> 2026-01-25 -8.507530e-07
#> 2026-01-26  4.646833e-06
#> 2026-01-27 -5.793243e-06
#> 2026-01-28  6.106456e-06

## AR(1)-t-APARCH(2, 1) - a little bit more complex specification ...
spec <- garchSpec(model = list(mu = 1.0e-4, ar = 0.5, omega = 1.0e-6, 
    alpha = c(0.10, 0.05), gamma = c(0, 0), beta = 0.8, delta = 1.8, 
    shape = 4, skew = 0.85), cond.dist = "sstd")
garchSim(spec, n = 10)
#> GMT 
#>                  garch
#> 2026-01-19 0.001434469
#> 2026-01-20 0.002922677
#> 2026-01-21 0.002206212
#> 2026-01-22 0.002961086
#> 2026-01-23 0.004310860
#> 2026-01-24 0.001242425
#> 2026-01-25 0.001137885
#> 2026-01-26 0.002214825
#> 2026-01-27 0.008865429
#> 2026-01-28 0.015609584

garchSim(spec, n = 10, extended = TRUE)
#> GMT 
#>                    garch       sigma         eps
#> 2026-01-19  0.0023363781 0.001656053  1.10505200
#> 2026-01-20  0.0009580534 0.001676312 -0.18501074
#> 2026-01-21 -0.0017466545 0.001641064 -1.41717868
#> 2026-01-22 -0.0008666182 0.001723989 -0.05411341
#> 2026-01-23 -0.0005399831 0.001705201 -0.12120216
#> 2026-01-24 -0.0019883909 0.001606889 -1.13162697
#> 2026-01-25 -0.0037203874 0.001636257 -1.72722977
#> 2026-01-26 -0.0007738262 0.001836876  0.53698088
#> 2026-01-27 -0.0052309638 0.001862567 -2.65442772
#> 2026-01-28 -0.0007040583 0.002313670  0.78292205
```
