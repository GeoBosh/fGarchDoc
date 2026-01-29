# Univariate GARCH/APARCH time series specification

Specifies an univariate ARMA-GARCH or ARMA-APARCH time series model.

## Usage

``` r
garchSpec(model = list(), presample = NULL, 
    cond.dist = c("norm", "ged", "std", "snorm", "sged", "sstd"), 
    rseed = NULL)
```

## Arguments

- model:

  a list of GARCH model parameters, see section ‘Details’. The default
  `model=list()` specifies Bollerslev's GARCH(1,1) model with normal
  conditional distributed innovations.

- presample:

  a numeric three column matrix with start values for the series, for
  the innovations, and for the conditional variances. For an
  ARMA(m,n)-GARCH(p,q) process the number of rows must be at least
  max(m,n,p,q)+1, longer presamples are truncated. Note, all presamples
  are initialized by a normal-GARCH(p,q) process.

- cond.dist:

  a character string naming the desired conditional distribution. Valid
  values are `"norm"`, `"ged"`, `"std"`, `"snorm"`, `"sged"`, `"sstd"`.
  The default value is `"norm"`, the standard normal distribution.

- rseed:

  single integer argument, the seed for the intitialization of the
  random number generator for the innovations. If `rseed=NULL`, the
  default, then the state of the random number generator is not touched
  by this function.

## Details

`garchSpec` specifies a GARCH or APARCH time series model which can be
used for simulating artificial GARCH and/or APARCH time series. This is
very useful for testing the GARCH parameter estimation results, since
the model parameters are known and well specified.

Argument `model` is a list of model parameters. For the GARCH part of
the model they are:

- `omega`:

  the constant coefficient of the variance equation, by default `1e-6`;

- `alpha`:

  the value or vector of autoregressive coefficients, by default 0.1,
  specifying a model of order 1;

- `beta`:

  the value or vector of variance coefficients, by default 0.8,
  specifying a model of order 1.

If the model is APARCH, then the following additional parameters are
available:

- delta:

  a positive number, the power of sigma in the volatility equation, it
  is 2 for GARCH models;

- gamma:

  the leverage parameters, a vector of length `alpha`, containing
  numbers in the interval \\(0,1)\\.

The values for the linear part (conditional mean) are:

- `mu`:

  the mean value, by default NULL;

- `ar`:

  the autoregressive ARMA coefficients, by default NULL;

- `ma`:

  the moving average ARMA coefficients, by default NULL.

The parameters for the conditional distributions are:

- `skew`:

  the skewness parameter (also named "xi"), by default 0.9, effective
  only for the `"dsnorm"`, the `"dsged"`, and the `"dsstd"` skewed
  conditional distributions;

- `shape`:

  the shape parameter (also named "nu"), by default 2 for the `"dged"`
  and `"dsged"`, and by default 4 for the `"dstd"` and `"dsstd"`
  conditional distributions.

For example, specifying a subset AR(5\[1,5\])-GARCH(2,1) model with a
standardized Student-t distribution with four degrees of freedom will
return the following printed output:

            garchSpec(model = list(ar = c(0.5,0,0,0,0.1), alpha =
                c(0.1, 0.1), beta = 0.75, shape = 4), cond.dist = "std")

            Formula:
             ~ ar(5) + garch(2, 1)
            Model:
             ar:    0.5 0 0 0 0.1
             omega: 1e-06
             alpha: 0.1 0.1
             beta:  0.75
            Distribution:
             std
            Distributional Parameter:
             nu = 4
            Presample:
               time          z     h y
            0     0 -0.3262334 2e-05 0
            -1   -1  1.3297993 2e-05 0
            -2   -2  1.2724293 2e-05 0
            -3   -3  0.4146414 2e-05 0
            -4   -4 -1.5399500 2e-05 0
            

Its interpretation is as follows. ‘Formula’ describes the formula
expression specifying the generating process, ‘Model’ lists the
associated model parameters, ‘Distribution’ the type of the conditional
distribution function in use, ‘Distributional Parameters’ lists the
distributional parameter (if any), and the ‘Presample’ shows the
presample input matrix.

If we have specified `presample = NULL` in the argument list, then the
presample is generated automatically by default as norm-AR()-GARCH()
process.

## Value

an object of class
`"`[`fGARCHSPEC`](https://geobosh.github.io/fGarchDoc/reference/class-fGARCHSPEC.md)`"`

## Author

Diethelm Wuertz for the Rmetrics R-port

## See also

[`garchSim`](https://geobosh.github.io/fGarchDoc/reference/garchSim.md),
[`garchFit`](https://geobosh.github.io/fGarchDoc/reference/garchFit.md)

## Examples

``` r
# Normal Conditional Distribution:
spec = garchSpec()
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
#>   time        z     h y
#> 1    0 1.114986 1e-05 0

# Skewed Normal Conditional Distribution:
spec = garchSpec(model = list(skew = 0.8), cond.dist = "snorm")
spec
#> 
#> Formula: 
#>  ~ garch(1, 1)
#> Model:
#>  omega: 1e-06
#>  alpha: 0.1
#>  beta:  0.8
#> Distribution: 
#>  snorm
#> Distributional Parameters: 
#>  xi = 0.8
#> Presample: 
#>   time        z     h y
#> 1    0 1.779133 1e-05 0

# Skewed GED Conditional Distribution:
spec = garchSpec(model = list(skew = 0.9, shape = 4.8), cond.dist = "sged")
spec
#> 
#> Formula: 
#>  ~ garch(1, 1)
#> Model:
#>  omega: 1e-06
#>  alpha: 0.1
#>  beta:  0.8
#> Distribution: 
#>  sged
#> Distributional Parameters: 
#>  nu = 4.8  xi = 0.9
#> Presample: 
#>   time        z     h y
#> 1    0 1.122071 1e-05 0
   
## More specifications ...

# Default GARCH(1,1) - uses default parameter settings
garchSpec(model = list())
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
#>   time         z     h y
#> 1    0 0.2432528 1e-05 0

# ARCH(2) - use default omega and specify alpha, set beta=0!
garchSpec(model = list(alpha = c(0.2, 0.4), beta = 0))
#> 
#> Formula: 
#>  ~ arch(2)
#> Model:
#>  omega: 1e-06
#>  alpha: 0.2 0.4
#> Distribution: 
#>  norm
#> Presample: 
#>   time         z       h y
#> 1   -1 0.2340239 2.5e-06 0
#> 2    0 0.8722562 2.5e-06 0

# AR(1)-ARCH(2) - use default mu, omega
garchSpec(model = list(ar = 0.5, alpha = c(0.3, 0.4), beta = 0))
#> 
#> Formula: 
#>  ~ ar(1) + arch(2)
#> Model:
#>  ar:    0.5
#>  omega: 1e-06
#>  alpha: 0.3 0.4
#> Distribution: 
#>  norm
#> Presample: 
#>   time          z            h y
#> 1   -1  0.6428043 3.333333e-06 0
#> 2    0 -0.3326850 3.333333e-06 0

# AR([1,5])-GARCH(1,1) - use default garch values and subset ar[.]
garchSpec(model = list(mu = 0.001, ar = c(0.5,0,0,0,0.1)))
#> 
#> Formula: 
#>  ~ ar(5) + garch(1, 1)
#> Model:
#>  ar:    0.5 0 0 0 0.1
#>  mu:    0.001
#>  omega: 1e-06
#>  alpha: 0.1
#>  beta:  0.8
#> Distribution: 
#>  norm
#> Presample: 
#>   time          z     h      y
#> 1   -4 -0.6641954 1e-05 0.0025
#> 2   -3  0.6353050 1e-05 0.0025
#> 3   -2  0.8513766 1e-05 0.0025
#> 4   -1  1.2776275 1e-05 0.0025
#> 5    0  0.1459210 1e-05 0.0025

# ARMA(1,2)-GARCH(1,1) - use default garch values
garchSpec(model = list(ar = 0.5, ma = c(0.3, -0.3)))  
#> 
#> Formula: 
#>  ~ arma(1, 2) + garch(1, 1)
#> Model:
#>  ar:    0.5
#>  ma:    0.3 -0.3
#>  omega: 1e-06
#>  alpha: 0.1
#>  beta:  0.8
#> Distribution: 
#>  norm
#> Presample: 
#>   time         z     h y
#> 1   -1 0.8914155 1e-05 0
#> 2    0 3.6295605 1e-05 0

# GARCH(1,1) - use default omega and specify alpha/beta
garchSpec(model = list(alpha = 0.2, beta = 0.7))
#> 
#> Formula: 
#>  ~ garch(1, 1)
#> Model:
#>  omega: 1e-06
#>  alpha: 0.2
#>  beta:  0.7
#> Distribution: 
#>  norm
#> Presample: 
#>   time          z     h y
#> 1    0 -0.4065891 1e-05 0

# GARCH(1,1) - specify omega/alpha/beta
garchSpec(model = list(omega = 1e-6, alpha = 0.1, beta = 0.8))
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
#>   time        z     h y
#> 1    0 1.739747 1e-05 0

# GARCH(1,2) - use default omega and specify alpha[1]/beta[2]
garchSpec(model = list(alpha = 0.1, beta = c(0.4, 0.4)))
#> 
#> Formula: 
#>  ~ garch(1, 2)
#> Model:
#>  omega: 1e-06
#>  alpha: 0.1
#>  beta:  0.4 0.4
#> Distribution: 
#>  norm
#> Presample: 
#>   time          z     h y
#> 1   -1 -1.9194209 1e-05 0
#> 2    0  0.8253429 1e-05 0

# GARCH(2,1) - use default omega and specify alpha[2]/beta[1]
garchSpec(model = list(alpha = c(0.12, 0.04), beta = 0.08))
#> 
#> Formula: 
#>  ~ garch(2, 1)
#> Model:
#>  omega: 1e-06
#>  alpha: 0.12 0.04
#>  beta:  0.08
#> Distribution: 
#>  norm
#> Presample: 
#>   time          z            h y
#> 1   -1  0.5432452 1.315789e-06 0
#> 2    0 -1.5046706 1.315789e-06 0

# snorm-ARCH(1) - use defaults with skew Normal
garchSpec(model = list(beta = 0, skew = 0.8), cond.dist = "snorm")
#> 
#> Formula: 
#>  ~ arch(1)
#> Model:
#>  omega: 1e-06
#>  alpha: 0.1
#> Distribution: 
#>  snorm
#> Distributional Parameters: 
#>  xi = 0.8
#> Presample: 
#>   time          z            h y
#> 1    0 -0.4931206 1.111111e-06 0

# sged-GARCH(1,1) - using defaults with skew GED
garchSpec(model = list(skew = 0.93, shape = 3), cond.dist = "sged")
#> 
#> Formula: 
#>  ~ garch(1, 1)
#> Model:
#>  omega: 1e-06
#>  alpha: 0.1
#>  beta:  0.8
#> Distribution: 
#>  sged
#> Distributional Parameters: 
#>  nu = 3  xi = 0.93
#> Presample: 
#>   time         z     h y
#> 1    0 0.2931894 1e-05 0

# Taylor Schwert GARCH(1,1) - this belongs to the family of APARCH Models
garchSpec(model = list(delta = 1))
#> 
#> Formula: 
#>  ~ aparch(1, 1)
#> Model:
#>  omega: 1e-06
#>  alpha: 0.1
#>  beta:  0.8
#>  delta: 1
#> Distribution: 
#>  norm
#> Presample: 
#>   time          z     h y
#> 1    0 -0.6985515 1e-05 0

# AR(1)-t-APARCH(2, 1) - a little bit more complex specification ...
garchSpec(model = list(mu = 1.0e-4, ar = 0.5, omega = 1.0e-6, 
    alpha = c(0.10, 0.05), gamma = c(0, 0), beta = 0.8, delta = 1.8, 
    shape = 4, skew = 0.85), cond.dist = "sstd")
#> 
#> Formula: 
#>  ~ ar(1) + aparch(2, 1)
#> Model:
#>  ar:    0.5
#>  mu:    1e-04
#>  omega: 1e-06
#>  alpha: 0.1 0.05
#>  beta:  0.8
#>  delta: 1.8
#> Distribution: 
#>  sstd
#> Distributional Parameters: 
#>  nu = 4  xi = 0.85
#> Presample: 
#>   time           z     h     y
#> 1   -1 -1.31068201 2e-05 2e-04
#> 2    0 -0.08895085 2e-05 2e-04
```
