# Fit univariate and multivariate GARCH-type models

Estimates the parameters of a univariate ARMA-GARCH/APARCH process, or —
experimentally — of a multivariate GO-GARCH process model. The latter
uses an algorithm based on `fastICA()`, inspired from Bernhard Pfaff's
package [gogarch](https://CRAN.R-project.org/package=gogarch).

## Usage

    garchFit(formula = ~ garch(1, 1), data,
        init.rec = c("mci", "uev"),
        delta = 2, skew = 1, shape = 4,
        cond.dist = c("norm", "snorm", "ged", "sged",
                          "std", "sstd", "snig", "QMLE"),
        include.mean = TRUE, include.delta = NULL, include.skew = NULL,
            include.shape = NULL,
            leverage = NULL, trace = TRUE,
        <!-- %recursion = c("internal", "filter", "testing"), -->
        algorithm = c("nlminb", "lbfgsb", "nlminb+nm", "lbfgsb+nm"),
        hessian = c("ropt", "rcd"),
            control = list(),
            title = NULL, description = NULL, ...)

    garchKappa(cond.dist = c("norm", "ged", "std", "snorm", "sged", "sstd", "snig"),
               gamma = 0, delta = 2, skew = NA, shape = NA)

    .gogarchFit(formula = ~garch(1, 1), data, init.rec = c("mci", "uev"),
                delta = 2, skew = 1, shape = 4,
                cond.dist = c("norm", "snorm", "ged", "sged",
                              "std", "sstd", "snig", "QMLE"),
                include.mean = TRUE, include.delta = NULL, include.skew = NULL,
                include.shape = NULL,
                leverage = NULL, trace = TRUE,
                algorithm = c("nlminb", "lbfgsb", "nlminb+nm", "lbfgsb+nm"),
                hessian = c("ropt", "rcd"),
                control = list(),
                title = NULL, description = NULL, ...)

## Arguments

- formula:

  [`formula`](https://geobosh.github.io/fGarchDoc/reference/methods-formula.md)
  object describing the mean and variance equation of the
  ARMA-GARCH/APARCH model. A pure GARCH(1,1) model is selected e.g., for
  `formula = ~garch(1,1)`. To specify an ARMA(2,1)-APARCH(1,1) process,
  use ` ~ arma(2,1) + aparch(1,1)`.

- data:

  an optional `"timeSeries"` or `"data.frame"` object containing the
  variables in the model. If not found in `data`, the variables are
  taken from `environment(formula)`, typically the environment from
  which `armaFit` is called. If `data` is an univariate series, then the
  series is converted into a numeric vector and the name of the response
  in the formula will be neglected.

- init.rec:

  a character string indicating the method how to initialize the mean
  and varaince recursion relation.

- delta:

  a numeric value, the exponent `delta` of the variance recursion. By
  default, this value will be fixed, otherwise the exponent will be
  estimated together with the other model parameters if
  `include.delta=FALSE`.

- skew:

  a numeric value, the skewness parameter of the conditional
  distribution.

- shape:

  a numeric value, the shape parameter of the conditional distribution.

- cond.dist:

  a character string naming the desired conditional distribution. Valid
  values are `"dnorm"`, `"dged"`, `"dstd"`, `"dsnorm"`, `"dsged"`,
  `"dsstd"` and `"QMLE"`. The default value is the normal distribution.
  See Details for more information.

- include.mean:

  this flag determines if the parameter for the mean will be estimated
  or not. If `include.mean=TRUE` this will be the case, otherwise the
  parameter will be kept fixed durcing the process of parameter
  optimization.

- include.delta:

  a [`logical`](https://rdrr.io/r/base/logical.html) determining if the
  parameter for the recursion equation `delta` will be estimated or not.
  If false, the shape parameter will be kept fixed during the process of
  parameter optimization.

- include.skew:

  a logical flag which determines if the parameter for the skewness of
  the conditional distribution will be estimated or not. If
  `include.skew=FALSE` then the skewness parameter will be kept fixed
  during the process of parameter optimization.

- include.shape:

  a logical flag which determines if the parameter for the shape of the
  conditional distribution will be estimated or not. If
  `include.shape=FALSE` then the shape parameter will be kept fixed
  during the process of parameter optimization.

- leverage:

  a logical flag for APARCH models. Should the model be leveraged? By
  default `leverage=TRUE`.

- trace:

  a logical flag. Should the optimization process of fitting the model
  parameters be printed? By default `trace=TRUE`.

- algorithm:

  a string parameter that determines the algorithm used for maximum
  likelihood estimation.

- hessian:

  a string denoting how the Hessian matrix should be evaluated, either
  `hessian ="rcd"`, or `"ropt"`. The default, `"rcd"` is a central
  difference approximation implemented in R and `"ropt"` uses the
  internal R function `optimhess`.

- control:

  control parameters, the same as used for the functions from `nlminb`,
  and 'bfgs' and 'Nelder-Mead' from `optim`.

- gamma:

  APARCH leverage parameter entering into the formula for calculating
  the expectation value.

- title:

  a character string which allows for a project title.

- description:

  optional character string with a brief description.

- ...:

  additional arguments to be passed.

## Details

`"QMLE"` stands for Quasi-Maximum Likelihood Estimation, which assumes
normal distribution and uses robust standard errors for inference.
Bollerslev and Wooldridge (1992) proved that if the mean and the
volatility equations are correctly specified, the QML estimates are
consistent and asymptotically normally distributed. However, the
estimates are not efficient and “the efficiency loss can be marked under
asymmetric ... distributions” (Bollerslev and Wooldridge (1992), p.
166). The robust variance-covariance matrix of the estimates equals the
(Eicker-White) sandwich estimator, i.e.

\$\$V = H^{-1} G^{\prime} G H^{-1},\$\$

where \\V\\ denotes the variance-covariance matrix, \\H\\ stands for the
Hessian and \\G\\ represents the matrix of contributions to the
gradient, the elements of which are defined as

\$\$G\_{t,i} = \frac{\partial l\_{t}}{\partial \zeta\_{i}},\$\$

where \\t\_{t}\\ is the log likelihood of the t-th observation and
\\\zeta\_{i}\\ is the i-th estimated parameter. See sections 10.3 and
10.4 in Davidson and MacKinnon (2004) for a more detailed description of
the robust variance-covariance matrix.

## Value

for `garchFit`, an S4 object of class
`"`[`fGARCH`](https://geobosh.github.io/fGarchDoc/reference/class-fGARCH.md)`"`.
Slot `@fit` contains the results from the optimization.

for `.gogarchFit()`: Similar definition for GO-GARCH modeling. Here,
`data` must be *multivariate*. Still “preliminary”, mostly undocumented,
and untested(!). At least mentioned here...

## References

ATT (1984); *PORT Library Documentation*,
http://netlib.bell-labs.com/netlib/port/.

Bera A.K., Higgins M.L. (1993); *ARCH Models: Properties, Estimation and
Testing*, J. Economic Surveys 7, 305–362.

Bollerslev T. (1986); *Generalized Autoregressive Conditional
Heteroscedasticity*, Journal of Econometrics 31, 307–327.

Bollerslev T., Wooldridge J.M. (1992); *Quasi-Maximum Likelihood
Estimation and Inference in Dynamic Models with Time-Varying
Covariance*, Econometric Reviews 11, 143–172.

Byrd R.H., Lu P., Nocedal J., Zhu C. (1995); *A Limited Memory Algorithm
for Bound Constrained Optimization*, SIAM Journal of Scientific
Computing 16, 1190–1208.

Davidson R., MacKinnon J.G. (2004); *Econometric Theory and Methods*,
Oxford University Press, New York.

Engle R.F. (1982); *Autoregressive Conditional Heteroscedasticity with
Estimates of the Variance of United Kingdom Inflation*, Econometrica 50,
987–1008.

Nash J.C. (1990); *Compact Numerical Methods for Computers*, Linear
Algebra and Function Minimisation, Adam Hilger.

Nelder J.A., Mead R. (1965); *A Simplex Algorithm for Function
Minimization*, Computer Journal 7, 308–313.

Nocedal J., Wright S.J. (1999); *Numerical Optimization*, Springer, New
York.

## Author

Diethelm Wuertz for the Rmetrics R-port,  
R Core Team for the 'optim' R-port,  
Douglas Bates and Deepayan Sarkar for the 'nlminb' R-port,  
Bell-Labs for the underlying PORT Library,  
Ladislav Luksan for the underlying Fortran SQP Routine,  
Zhu, Byrd, Lu-Chen and Nocedal for the underlying L-BFGS-B Routine.

Martin Maechler for cleaning up; *mentioning* `.gogarchFit()`.

## See also

[`garchSpec`](https://geobosh.github.io/fGarchDoc/reference/garchSpec.md),
[`garchFitControl`](https://geobosh.github.io/fGarchDoc/reference/garchFitControl.md),
class
`"`[`fGARCH`](https://geobosh.github.io/fGarchDoc/reference/class-fGARCH.md)`"`

## Examples

``` r
## UNIVARIATE TIME SERIES INPUT:
# In the univariate case the lhs formula has not to be specified ...

# A numeric Vector from default GARCH(1,1) - fix the seed:
N <- 200
x.vec <- as.vector(garchSim(garchSpec(rseed = 1985), n = N)[,1])
garchFit(~ garch(1,1), data = x.vec, trace = FALSE)
#> 
#> Title:
#>  GARCH Modelling 
#> 
#> Call:
#>  garchFit(formula = ~garch(1, 1), data = x.vec, trace = FALSE) 
#> 
#> Mean and Variance Equation:
#>  data ~ garch(1, 1)
#> <environment: 0x613d7ffdd660>
#>  [data = x.vec]
#> 
#> Conditional Distribution:
#>  norm 
#> 
#> Coefficient(s):
#>         mu       omega      alpha1       beta1  
#> 3.5418e-05  1.0819e-06  8.8855e-02  8.1200e-01  
#> 
#> Std. Errors:
#>  based on Hessian 
#> 
#> Error Analysis:
#>         Estimate  Std. Error  t value Pr(>|t|)    
#> mu     3.542e-05   2.183e-04    0.162    0.871    
#> omega  1.082e-06   1.051e-06    1.030    0.303    
#> alpha1 8.885e-02   5.450e-02    1.630    0.103    
#> beta1  8.120e-01   1.242e-01    6.538 6.25e-11 ***
#> ---
#> Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
#> 
#> Log Likelihood:
#>  861.9494    normalized:  4.309747 
#> 
#> Description:
#>  Thu Jan 29 21:01:06 2026 by user: georgi 
#> 

# An univariate timeSeries object with dummy dates:
stopifnot(require("timeSeries"))
#> Loading required package: timeSeries
#> Loading required package: timeDate
#> 
#> Attaching package: ‘timeSeries’
#> The following objects are masked from ‘package:graphics’:
#> 
#>     lines, points
x.timeSeries <- dummyDailySeries(matrix(x.vec), units = "GARCH11")
garchFit(~ garch(1,1), data = x.timeSeries, trace = FALSE)
#> 
#> Title:
#>  GARCH Modelling 
#> 
#> Call:
#>  garchFit(formula = ~garch(1, 1), data = x.timeSeries, trace = FALSE) 
#> 
#> Mean and Variance Equation:
#>  data ~ garch(1, 1)
#> <environment: 0x613d80d2e480>
#>  [data = x.timeSeries]
#> 
#> Conditional Distribution:
#>  norm 
#> 
#> Coefficient(s):
#>         mu       omega      alpha1       beta1  
#> 3.5418e-05  1.0819e-06  8.8855e-02  8.1200e-01  
#> 
#> Std. Errors:
#>  based on Hessian 
#> 
#> Error Analysis:
#>         Estimate  Std. Error  t value Pr(>|t|)    
#> mu     3.542e-05   2.183e-04    0.162    0.871    
#> omega  1.082e-06   1.051e-06    1.030    0.303    
#> alpha1 8.885e-02   5.450e-02    1.630    0.103    
#> beta1  8.120e-01   1.242e-01    6.538 6.25e-11 ***
#> ---
#> Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
#> 
#> Log Likelihood:
#>  861.9494    normalized:  4.309747 
#> 
#> Description:
#>  Thu Jan 29 21:01:06 2026 by user: georgi 
#> 

if (FALSE) { # \dontrun{
   # An univariate zoo object:
   require("zoo")
   x.zoo <- zoo(as.vector(x.vec), order.by = as.Date(rownames(x.timeSeries)))
   garchFit(~ garch(1,1), data = x.zoo, trace = FALSE)
} # }

# An univariate "ts" object:
x.ts <- as.ts(x.vec)
garchFit(~ garch(1,1), data = x.ts, trace = FALSE)
#> 
#> Title:
#>  GARCH Modelling 
#> 
#> Call:
#>  garchFit(formula = ~garch(1, 1), data = x.ts, trace = FALSE) 
#> 
#> Mean and Variance Equation:
#>  data ~ garch(1, 1)
#> <environment: 0x613d81807130>
#>  [data = x.ts]
#> 
#> Conditional Distribution:
#>  norm 
#> 
#> Coefficient(s):
#>         mu       omega      alpha1       beta1  
#> 3.5418e-05  1.0819e-06  8.8855e-02  8.1200e-01  
#> 
#> Std. Errors:
#>  based on Hessian 
#> 
#> Error Analysis:
#>         Estimate  Std. Error  t value Pr(>|t|)    
#> mu     3.542e-05   2.183e-04    0.162    0.871    
#> omega  1.082e-06   1.051e-06    1.030    0.303    
#> alpha1 8.885e-02   5.450e-02    1.630    0.103    
#> beta1  8.120e-01   1.242e-01    6.538 6.25e-11 ***
#> ---
#> Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
#> 
#> Log Likelihood:
#>  861.9494    normalized:  4.309747 
#> 
#> Description:
#>  Thu Jan 29 21:01:06 2026 by user: georgi 
#> 


## MULTIVARIATE TIME SERIES INPUT:
##
# For multivariate data inputs the lhs formula must be specified ...

# A numeric matrix binded with dummy random normal variates:
X.mat <- cbind(GARCH11 = x.vec, R = rnorm(N))
garchFit(GARCH11 ~ garch(1,1), data = X.mat)
#> 
#> Series Initialization:
#>  ARMA Model:                arma
#>  Formula Mean:              ~ arma(0, 0)
#>  GARCH Model:               garch
#>  Formula Variance:          ~ garch(1, 1)
#>  ARMA Order:                0 0
#>  Max ARMA Order:            0
#>  GARCH Order:               1 1
#>  Max GARCH Order:           1
#>  Maximum Order:             1
#>  Conditional Dist:          norm
#>  h.start:                   2
#>  llh.start:                 1
#>  Length of Series:          200
#>  Recursion Init:            mci
#>  Series Scale:              0.003308171
#> 
#> Parameter Initialization:
#>  Initial Parameters:          $params
#>  Limits of Transformations:   $U, $V
#>  Which Parameters are Fixed?  $includes
#>  Parameter Matrix:
#>                      U            V       params includes
#>     mu     -0.05516776   0.05516776 -0.005516776     TRUE
#>     omega   0.00000100 100.00000000  0.100000000     TRUE
#>     alpha1  0.00000001   0.99999999  0.100000000     TRUE
#>     gamma1 -0.99999999   0.99999999  0.100000000    FALSE
#>     beta1   0.00000001   0.99999999  0.800000000     TRUE
#>     delta   0.00000000   2.00000000  2.000000000    FALSE
#>     skew    0.10000000  10.00000000  1.000000000    FALSE
#>     shape   1.00000000  10.00000000  4.000000000    FALSE
#>  Index List of Parameters to be Optimized:
#>     mu  omega alpha1  beta1 
#>      1      2      3      5 
#>  Persistence:                  0.9 
#> 
#> 
#> --- START OF TRACE ---
#> Selected Algorithm: nlminb 
#> 
#> R coded nlminb Solver: 
#> 
#>   0:     280.37902: -0.00551678 0.100000 0.100000 0.800000
#>   1:     280.37507: -0.00551675 0.101085 0.0997614 0.800840
#>   2:     280.37172: -0.00551671 0.100985 0.0984074 0.800529
#>   3:     280.36889: -0.00551668 0.102056 0.0981374 0.801378
#>   4:     280.36553: -0.00551664 0.101972 0.0967732 0.801110
#>   5:     280.36291: -0.00551659 0.102982 0.0962621 0.801921
#>   6:     280.36028: -0.00551652 0.102987 0.0948733 0.801815
#>   7:     280.35812: -0.00551642 0.103857 0.0941985 0.802668
#>   8:     280.35640: -0.00551626 0.103796 0.0928284 0.802909
#>   9:     280.35510: -0.00551594 0.104079 0.0921544 0.804093
#>  10:     280.35429: -0.00551543 0.103412 0.0912751 0.804938
#>  11:     280.35380: -0.00551470 0.102925 0.0909305 0.806189
#>  12:     280.35345: -0.00551337 0.102118 0.0903861 0.807156
#>  13:     280.35308: -0.00550880 0.101958 0.0898304 0.808116
#>  14:     280.35296: -0.00550326 0.101305 0.0896346 0.808798
#>  15:     280.35287: -0.00549602 0.101693 0.0894169 0.808659
#>  16:     280.35280: -0.00548956 0.101338 0.0890255 0.809195
#>  17:     280.35270: -0.00548306 0.100990 0.0889425 0.809846
#>  18:     280.35261: -0.00546712 0.100295 0.0886753 0.810712
#>  19:     280.35191: -0.00526092 0.100384 0.0880880 0.811016
#>  20:     280.34947: -0.00443606 0.0998012 0.0868493 0.812628
#>  21:     280.34213: -0.00121747 0.0993041 0.0846804 0.814752
#>  22:     280.33288: 0.00415509 0.0983925 0.0835405 0.816652
#>  23:     280.32556: 0.00933509 0.0984673 0.0851411 0.815292
#>  24:     280.32295: 0.0112564 0.0984683 0.0875808 0.813418
#>  25:     280.32262: 0.0109708 0.0988384 0.0887005 0.812137
#>  26:     280.32261: 0.0107322 0.0988356 0.0888526 0.812038
#>  27:     280.32261: 0.0107066 0.0988719 0.0888596 0.811988
#>  28:     280.32261: 0.0107061 0.0988616 0.0888549 0.812004
#> 
#> Final Estimate of the Negative LLH:
#>  LLH:  -861.9494    norm LLH:  -4.309747 
#>           mu        omega       alpha1        beta1 
#> 3.541769e-05 1.081941e-06 8.885493e-02 8.120038e-01 
#> 
#> R-optimhess Difference Approximated Hessian Matrix:
#>                   mu         omega        alpha1         beta1
#> mu     -2.110947e+07 -4.842148e+08  2.852385e+03 -1.458198e+03
#> omega  -4.842148e+08 -2.671144e+13 -2.328641e+08 -2.747076e+08
#> alpha1  2.852385e+03 -2.328641e+08 -2.618403e+03 -2.563703e+03
#> beta1  -1.458198e+03 -2.747076e+08 -2.563703e+03 -2.938561e+03
#> attr(,"time")
#> Time difference of 0.001574039 secs
#> 
#> --- END OF TRACE ---
#> 
#> 
#> Time to Estimate Parameters:
#>  Time difference of 0.008285522 secs
#> 
#> Title:
#>  GARCH Modelling 
#> 
#> Call:
#>  garchFit(formula = GARCH11 ~ garch(1, 1), data = X.mat) 
#> 
#> Mean and Variance Equation:
#>  GARCH11 ~ garch(1, 1)
#> <environment: 0x613d7fb58dc8>
#>  [data = X.mat]
#> 
#> Conditional Distribution:
#>  norm 
#> 
#> Coefficient(s):
#>         mu       omega      alpha1       beta1  
#> 3.5418e-05  1.0819e-06  8.8855e-02  8.1200e-01  
#> 
#> Std. Errors:
#>  based on Hessian 
#> 
#> Error Analysis:
#>         Estimate  Std. Error  t value Pr(>|t|)    
#> mu     3.542e-05   2.183e-04    0.162    0.871    
#> omega  1.082e-06   1.051e-06    1.030    0.303    
#> alpha1 8.885e-02   5.450e-02    1.630    0.103    
#> beta1  8.120e-01   1.242e-01    6.538 6.25e-11 ***
#> ---
#> Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
#> 
#> Log Likelihood:
#>  861.9494    normalized:  4.309747 
#> 
#> Description:
#>  Thu Jan 29 21:01:06 2026 by user: georgi 
#> 

# A multivariate timeSeries object with dummy dates:
X.timeSeries <- dummyDailySeries(X.mat, units = c("GARCH11", "R"))
garchFit(GARCH11 ~ garch(1,1), data = X.timeSeries)
#> 
#> Series Initialization:
#>  ARMA Model:                arma
#>  Formula Mean:              ~ arma(0, 0)
#>  GARCH Model:               garch
#>  Formula Variance:          ~ garch(1, 1)
#>  ARMA Order:                0 0
#>  Max ARMA Order:            0
#>  GARCH Order:               1 1
#>  Max GARCH Order:           1
#>  Maximum Order:             1
#>  Conditional Dist:          norm
#>  h.start:                   2
#>  llh.start:                 1
#>  Length of Series:          200
#>  Recursion Init:            mci
#>  Series Scale:              0.003308171
#> 
#> Parameter Initialization:
#>  Initial Parameters:          $params
#>  Limits of Transformations:   $U, $V
#>  Which Parameters are Fixed?  $includes
#>  Parameter Matrix:
#>                      U            V       params includes
#>     mu     -0.05516776   0.05516776 -0.005516776     TRUE
#>     omega   0.00000100 100.00000000  0.100000000     TRUE
#>     alpha1  0.00000001   0.99999999  0.100000000     TRUE
#>     gamma1 -0.99999999   0.99999999  0.100000000    FALSE
#>     beta1   0.00000001   0.99999999  0.800000000     TRUE
#>     delta   0.00000000   2.00000000  2.000000000    FALSE
#>     skew    0.10000000  10.00000000  1.000000000    FALSE
#>     shape   1.00000000  10.00000000  4.000000000    FALSE
#>  Index List of Parameters to be Optimized:
#>     mu  omega alpha1  beta1 
#>      1      2      3      5 
#>  Persistence:                  0.9 
#> 
#> 
#> --- START OF TRACE ---
#> Selected Algorithm: nlminb 
#> 
#> R coded nlminb Solver: 
#> 
#>   0:     280.37902: -0.00551678 0.100000 0.100000 0.800000
#>   1:     280.37507: -0.00551675 0.101085 0.0997614 0.800840
#>   2:     280.37172: -0.00551671 0.100985 0.0984074 0.800529
#>   3:     280.36889: -0.00551668 0.102056 0.0981374 0.801378
#>   4:     280.36553: -0.00551664 0.101972 0.0967732 0.801110
#>   5:     280.36291: -0.00551659 0.102982 0.0962621 0.801921
#>   6:     280.36028: -0.00551652 0.102987 0.0948733 0.801815
#>   7:     280.35812: -0.00551642 0.103857 0.0941985 0.802668
#>   8:     280.35640: -0.00551626 0.103796 0.0928284 0.802909
#>   9:     280.35510: -0.00551594 0.104079 0.0921544 0.804093
#>  10:     280.35429: -0.00551543 0.103412 0.0912751 0.804938
#>  11:     280.35380: -0.00551470 0.102925 0.0909305 0.806189
#>  12:     280.35345: -0.00551337 0.102118 0.0903861 0.807156
#>  13:     280.35308: -0.00550880 0.101958 0.0898304 0.808116
#>  14:     280.35296: -0.00550326 0.101305 0.0896346 0.808798
#>  15:     280.35287: -0.00549602 0.101693 0.0894169 0.808659
#>  16:     280.35280: -0.00548956 0.101338 0.0890255 0.809195
#>  17:     280.35270: -0.00548306 0.100990 0.0889425 0.809846
#>  18:     280.35261: -0.00546712 0.100295 0.0886753 0.810712
#>  19:     280.35191: -0.00526092 0.100384 0.0880880 0.811016
#>  20:     280.34947: -0.00443606 0.0998012 0.0868493 0.812628
#>  21:     280.34213: -0.00121747 0.0993041 0.0846804 0.814752
#>  22:     280.33288: 0.00415509 0.0983925 0.0835405 0.816652
#>  23:     280.32556: 0.00933509 0.0984673 0.0851411 0.815292
#>  24:     280.32295: 0.0112564 0.0984683 0.0875808 0.813418
#>  25:     280.32262: 0.0109708 0.0988384 0.0887005 0.812137
#>  26:     280.32261: 0.0107322 0.0988356 0.0888526 0.812038
#>  27:     280.32261: 0.0107066 0.0988719 0.0888596 0.811988
#>  28:     280.32261: 0.0107061 0.0988616 0.0888549 0.812004
#> 
#> Final Estimate of the Negative LLH:
#>  LLH:  -861.9494    norm LLH:  -4.309747 
#>           mu        omega       alpha1        beta1 
#> 3.541769e-05 1.081941e-06 8.885493e-02 8.120038e-01 
#> 
#> R-optimhess Difference Approximated Hessian Matrix:
#>                   mu         omega        alpha1         beta1
#> mu     -2.110947e+07 -4.842148e+08  2.852385e+03 -1.458198e+03
#> omega  -4.842148e+08 -2.671144e+13 -2.328641e+08 -2.747076e+08
#> alpha1  2.852385e+03 -2.328641e+08 -2.618403e+03 -2.563703e+03
#> beta1  -1.458198e+03 -2.747076e+08 -2.563703e+03 -2.938561e+03
#> attr(,"time")
#> Time difference of 0.001563311 secs
#> 
#> --- END OF TRACE ---
#> 
#> 
#> Time to Estimate Parameters:
#>  Time difference of 0.008081436 secs
#> 
#> Title:
#>  GARCH Modelling 
#> 
#> Call:
#>  garchFit(formula = GARCH11 ~ garch(1, 1), data = X.timeSeries) 
#> 
#> Mean and Variance Equation:
#>  GARCH11 ~ garch(1, 1)
#> <environment: 0x613d7fb58dc8>
#>  [data = X.timeSeries]
#> 
#> Conditional Distribution:
#>  norm 
#> 
#> Coefficient(s):
#>         mu       omega      alpha1       beta1  
#> 3.5418e-05  1.0819e-06  8.8855e-02  8.1200e-01  
#> 
#> Std. Errors:
#>  based on Hessian 
#> 
#> Error Analysis:
#>         Estimate  Std. Error  t value Pr(>|t|)    
#> mu     3.542e-05   2.183e-04    0.162    0.871    
#> omega  1.082e-06   1.051e-06    1.030    0.303    
#> alpha1 8.885e-02   5.450e-02    1.630    0.103    
#> beta1  8.120e-01   1.242e-01    6.538 6.25e-11 ***
#> ---
#> Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
#> 
#> Log Likelihood:
#>  861.9494    normalized:  4.309747 
#> 
#> Description:
#>  Thu Jan 29 21:01:06 2026 by user: georgi 
#> 

if (FALSE) { # \dontrun{
   # A multivariate zoo object:
   X.zoo <- zoo(X.mat, order.by = as.Date(rownames(x.timeSeries)))
   garchFit(GARCH11 ~ garch(1,1), data = X.zoo)
} # }

# A multivariate "mts" object:
X.mts <- as.ts(X.mat)
garchFit(GARCH11 ~ garch(1,1), data = X.mts)
#> 
#> Series Initialization:
#>  ARMA Model:                arma
#>  Formula Mean:              ~ arma(0, 0)
#>  GARCH Model:               garch
#>  Formula Variance:          ~ garch(1, 1)
#>  ARMA Order:                0 0
#>  Max ARMA Order:            0
#>  GARCH Order:               1 1
#>  Max GARCH Order:           1
#>  Maximum Order:             1
#>  Conditional Dist:          norm
#>  h.start:                   2
#>  llh.start:                 1
#>  Length of Series:          200
#>  Recursion Init:            mci
#>  Series Scale:              0.003308171
#> 
#> Parameter Initialization:
#>  Initial Parameters:          $params
#>  Limits of Transformations:   $U, $V
#>  Which Parameters are Fixed?  $includes
#>  Parameter Matrix:
#>                      U            V       params includes
#>     mu     -0.05516776   0.05516776 -0.005516776     TRUE
#>     omega   0.00000100 100.00000000  0.100000000     TRUE
#>     alpha1  0.00000001   0.99999999  0.100000000     TRUE
#>     gamma1 -0.99999999   0.99999999  0.100000000    FALSE
#>     beta1   0.00000001   0.99999999  0.800000000     TRUE
#>     delta   0.00000000   2.00000000  2.000000000    FALSE
#>     skew    0.10000000  10.00000000  1.000000000    FALSE
#>     shape   1.00000000  10.00000000  4.000000000    FALSE
#>  Index List of Parameters to be Optimized:
#>     mu  omega alpha1  beta1 
#>      1      2      3      5 
#>  Persistence:                  0.9 
#> 
#> 
#> --- START OF TRACE ---
#> Selected Algorithm: nlminb 
#> 
#> R coded nlminb Solver: 
#> 
#>   0:     280.37902: -0.00551678 0.100000 0.100000 0.800000
#>   1:     280.37507: -0.00551675 0.101085 0.0997614 0.800840
#>   2:     280.37172: -0.00551671 0.100985 0.0984074 0.800529
#>   3:     280.36889: -0.00551668 0.102056 0.0981374 0.801378
#>   4:     280.36553: -0.00551664 0.101972 0.0967732 0.801110
#>   5:     280.36291: -0.00551659 0.102982 0.0962621 0.801921
#>   6:     280.36028: -0.00551652 0.102987 0.0948733 0.801815
#>   7:     280.35812: -0.00551642 0.103857 0.0941985 0.802668
#>   8:     280.35640: -0.00551626 0.103796 0.0928284 0.802909
#>   9:     280.35510: -0.00551594 0.104079 0.0921544 0.804093
#>  10:     280.35429: -0.00551543 0.103412 0.0912751 0.804938
#>  11:     280.35380: -0.00551470 0.102925 0.0909305 0.806189
#>  12:     280.35345: -0.00551337 0.102118 0.0903861 0.807156
#>  13:     280.35308: -0.00550880 0.101958 0.0898304 0.808116
#>  14:     280.35296: -0.00550326 0.101305 0.0896346 0.808798
#>  15:     280.35287: -0.00549602 0.101693 0.0894169 0.808659
#>  16:     280.35280: -0.00548956 0.101338 0.0890255 0.809195
#>  17:     280.35270: -0.00548306 0.100990 0.0889425 0.809846
#>  18:     280.35261: -0.00546712 0.100295 0.0886753 0.810712
#>  19:     280.35191: -0.00526092 0.100384 0.0880880 0.811016
#>  20:     280.34947: -0.00443606 0.0998012 0.0868493 0.812628
#>  21:     280.34213: -0.00121747 0.0993041 0.0846804 0.814752
#>  22:     280.33288: 0.00415509 0.0983925 0.0835405 0.816652
#>  23:     280.32556: 0.00933509 0.0984673 0.0851411 0.815292
#>  24:     280.32295: 0.0112564 0.0984683 0.0875808 0.813418
#>  25:     280.32262: 0.0109708 0.0988384 0.0887005 0.812137
#>  26:     280.32261: 0.0107322 0.0988356 0.0888526 0.812038
#>  27:     280.32261: 0.0107066 0.0988719 0.0888596 0.811988
#>  28:     280.32261: 0.0107061 0.0988616 0.0888549 0.812004
#> 
#> Final Estimate of the Negative LLH:
#>  LLH:  -861.9494    norm LLH:  -4.309747 
#>           mu        omega       alpha1        beta1 
#> 3.541769e-05 1.081941e-06 8.885493e-02 8.120038e-01 
#> 
#> R-optimhess Difference Approximated Hessian Matrix:
#>                   mu         omega        alpha1         beta1
#> mu     -2.110947e+07 -4.842148e+08  2.852385e+03 -1.458198e+03
#> omega  -4.842148e+08 -2.671144e+13 -2.328641e+08 -2.747076e+08
#> alpha1  2.852385e+03 -2.328641e+08 -2.618403e+03 -2.563703e+03
#> beta1  -1.458198e+03 -2.747076e+08 -2.563703e+03 -2.938561e+03
#> attr(,"time")
#> Time difference of 0.00154376 secs
#> 
#> --- END OF TRACE ---
#> 
#> 
#> Time to Estimate Parameters:
#>  Time difference of 0.008075953 secs
#> 
#> Title:
#>  GARCH Modelling 
#> 
#> Call:
#>  garchFit(formula = GARCH11 ~ garch(1, 1), data = X.mts) 
#> 
#> Mean and Variance Equation:
#>  GARCH11 ~ garch(1, 1)
#> <environment: 0x613d7fb58dc8>
#>  [data = X.mts]
#> 
#> Conditional Distribution:
#>  norm 
#> 
#> Coefficient(s):
#>         mu       omega      alpha1       beta1  
#> 3.5418e-05  1.0819e-06  8.8855e-02  8.1200e-01  
#> 
#> Std. Errors:
#>  based on Hessian 
#> 
#> Error Analysis:
#>         Estimate  Std. Error  t value Pr(>|t|)    
#> mu     3.542e-05   2.183e-04    0.162    0.871    
#> omega  1.082e-06   1.051e-06    1.030    0.303    
#> alpha1 8.885e-02   5.450e-02    1.630    0.103    
#> beta1  8.120e-01   1.242e-01    6.538 6.25e-11 ***
#> ---
#> Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
#> 
#> Log Likelihood:
#>  861.9494    normalized:  4.309747 
#> 
#> Description:
#>  Thu Jan 29 21:01:06 2026 by user: georgi 
#> 


## MODELING THE PERCENTUAL SPI/SBI SPREAD FROM LPP BENCHMARK:

stopifnot(require("timeSeries"))
X.timeSeries <- as.timeSeries(data(LPP2005REC))
X.mat <- as.matrix(X.timeSeries)
if (FALSE) X.zoo <- zoo(X.mat, order.by = as.Date(rownames(X.mat))) # \dontrun{}
X.mts <- ts(X.mat)
garchFit(100*(SPI - SBI) ~ garch(1,1), data = X.timeSeries)
#> 
#> Series Initialization:
#>  ARMA Model:                arma
#>  Formula Mean:              ~ arma(0, 0)
#>  GARCH Model:               garch
#>  Formula Variance:          ~ garch(1, 1)
#>  ARMA Order:                0 0
#>  Max ARMA Order:            0
#>  GARCH Order:               1 1
#>  Max GARCH Order:           1
#>  Maximum Order:             1
#>  Conditional Dist:          norm
#>  h.start:                   2
#>  llh.start:                 1
#>  Length of Series:          377
#>  Recursion Init:            mci
#>  Series Scale:              0.7911981
#> 
#> Parameter Initialization:
#>  Initial Parameters:          $params
#>  Limits of Transformations:   $U, $V
#>  Which Parameters are Fixed?  $includes
#>  Parameter Matrix:
#>                      U          V    params includes
#>     mu     -1.06338438   1.063384 0.1063384     TRUE
#>     omega   0.00000100 100.000000 0.1000000     TRUE
#>     alpha1  0.00000001   1.000000 0.1000000     TRUE
#>     gamma1 -0.99999999   1.000000 0.1000000    FALSE
#>     beta1   0.00000001   1.000000 0.8000000     TRUE
#>     delta   0.00000000   2.000000 2.0000000    FALSE
#>     skew    0.10000000  10.000000 1.0000000    FALSE
#>     shape   1.00000000  10.000000 4.0000000    FALSE
#>  Index List of Parameters to be Optimized:
#>     mu  omega alpha1  beta1 
#>      1      2      3      5 
#>  Persistence:                  0.9 
#> 
#> 
#> --- START OF TRACE ---
#> Selected Algorithm: nlminb 
#> 
#> R coded nlminb Solver: 
#> 
#>   0:     509.82704: 0.106338 0.100000 0.100000 0.800000
#>   1:     509.51991: 0.106356 0.0941456 0.0992929 0.796649
#>   2:     509.34861: 0.106401 0.0914068 0.105150 0.798661
#>   3:     509.31324: 0.106450 0.0850532 0.106653 0.796875
#>   4:     509.18616: 0.106664 0.0845871 0.109854 0.802489
#>   5:     509.13752: 0.107048 0.0796272 0.109273 0.805331
#>   6:     509.11455: 0.107636 0.0785584 0.109980 0.809041
#>   7:     509.09156: 0.108344 0.0773904 0.109886 0.808412
#>   8:     508.86157: 0.130216 0.0904027 0.123041 0.783222
#>   9:     508.76023: 0.151709 0.0685017 0.102923 0.822562
#>  10:     508.74002: 0.151708 0.0695354 0.103784 0.823131
#>  11:     508.73297: 0.151702 0.0694221 0.104546 0.821891
#>  12:     508.72844: 0.151608 0.0697581 0.105658 0.821808
#>  13:     508.72336: 0.151493 0.0696262 0.105848 0.820859
#>  14:     508.71847: 0.151405 0.0705829 0.106223 0.820227
#>  15:     508.71404: 0.151289 0.0705200 0.106456 0.819285
#>  16:     508.71023: 0.151174 0.0708824 0.107305 0.818955
#>  17:     508.70624: 0.151057 0.0709395 0.107483 0.818015
#>  18:     508.70241: 0.150956 0.0717984 0.107803 0.817387
#>  19:     508.69901: 0.150836 0.0716372 0.108257 0.816599
#>  20:     508.69619: 0.150718 0.0720058 0.109044 0.816221
#>  21:     508.68815: 0.150061 0.0750247 0.109122 0.812611
#>  22:     508.67779: 0.149315 0.0751932 0.111191 0.809976
#>  23:     508.67153: 0.148688 0.0766777 0.114346 0.806316
#>  24:     508.67090: 0.149243 0.0770851 0.115532 0.804599
#>  25:     508.67086: 0.148699 0.0770358 0.115443 0.804762
#>  26:     508.67085: 0.148859 0.0770391 0.115425 0.804785
#>  27:     508.67085: 0.148857 0.0770402 0.115430 0.804778
#> 
#> Final Estimate of the Negative LLH:
#>  LLH:  420.3749    norm LLH:  1.115053 
#>         mu      omega     alpha1      beta1 
#> 0.11777514 0.04822674 0.11543003 0.80477759 
#> 
#> R-optimhess Difference Approximated Hessian Matrix:
#>                mu        omega      alpha1        beta1
#> mu     -822.50417    -66.39566    44.87188    -46.12927
#> omega   -66.39566 -22459.56936 -7066.22458 -10357.90647
#> alpha1   44.87188  -7066.22458 -4084.55043  -4274.92985
#> beta1   -46.12927 -10357.90647 -4274.92985  -5674.92502
#> attr(,"time")
#> Time difference of 0.001900911 secs
#> 
#> --- END OF TRACE ---
#> 
#> 
#> Time to Estimate Parameters:
#>  Time difference of 0.009106398 secs
#> 
#> Title:
#>  GARCH Modelling 
#> 
#> Call:
#>  garchFit(formula = 100 * (SPI - SBI) ~ garch(1, 1), data = X.timeSeries) 
#> 
#> Mean and Variance Equation:
#>  100 * (SPI - SBI) ~ garch(1, 1)
#> <environment: 0x613d7fb58dc8>
#>  [data = X.timeSeries]
#> 
#> Conditional Distribution:
#>  norm 
#> 
#> Coefficient(s):
#>       mu     omega    alpha1     beta1  
#> 0.117775  0.048227  0.115430  0.804778  
#> 
#> Std. Errors:
#>  based on Hessian 
#> 
#> Error Analysis:
#>         Estimate  Std. Error  t value Pr(>|t|)    
#> mu       0.11778     0.03509    3.357 0.000789 ***
#> omega    0.04823     0.01851    2.605 0.009186 ** 
#> alpha1   0.11543     0.03771    3.061 0.002206 ** 
#> beta1    0.80478     0.05422   14.842  < 2e-16 ***
#> ---
#> Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
#> 
#> Log Likelihood:
#>  -420.3749    normalized:  -1.115053 
#> 
#> Description:
#>  Thu Jan 29 21:01:06 2026 by user: georgi 
#> 
# The remaining are not yet supported ...
# garchFit(100*(SPI - SBI) ~ garch(1,1), data = X.mat)
# garchFit(100*(SPI - SBI) ~ garch(1,1), data = X.zoo)
# garchFit(100*(SPI - SBI) ~ garch(1,1), data = X.mts)

## MODELING HIGH/LOW RETURN SPREADS FROM MSFT PRICE SERIES:

X.timeSeries <- MSFT
garchFit(Open ~ garch(1,1), data = returns(X.timeSeries))
#> 
#> Series Initialization:
#>  ARMA Model:                arma
#>  Formula Mean:              ~ arma(0, 0)
#>  GARCH Model:               garch
#>  Formula Variance:          ~ garch(1, 1)
#>  ARMA Order:                0 0
#>  Max ARMA Order:            0
#>  GARCH Order:               1 1
#>  Max GARCH Order:           1
#>  Maximum Order:             1
#>  Conditional Dist:          norm
#>  h.start:                   2
#>  llh.start:                 1
#>  Length of Series:          248
#>  Recursion Init:            mci
#>  Series Scale:              0.03467707
#> 
#> Parameter Initialization:
#>  Initial Parameters:          $params
#>  Limits of Transformations:   $U, $V
#>  Which Parameters are Fixed?  $includes
#>  Parameter Matrix:
#>                      U           V      params includes
#>     mu     -0.27446113   0.2744611 -0.02744611     TRUE
#>     omega   0.00000100 100.0000000  0.10000000     TRUE
#>     alpha1  0.00000001   1.0000000  0.10000000     TRUE
#>     gamma1 -0.99999999   1.0000000  0.10000000    FALSE
#>     beta1   0.00000001   1.0000000  0.80000000     TRUE
#>     delta   0.00000000   2.0000000  2.00000000    FALSE
#>     skew    0.10000000  10.0000000  1.00000000    FALSE
#>     shape   1.00000000  10.0000000  4.00000000    FALSE
#>  Index List of Parameters to be Optimized:
#>     mu  omega alpha1  beta1 
#>      1      2      3      5 
#>  Persistence:                  0.9 
#> 
#> 
#> --- START OF TRACE ---
#> Selected Algorithm: nlminb 
#> 
#> R coded nlminb Solver: 
#> 
#>   0:     342.27498: -0.0274461 0.100000 0.100000 0.800000
#>   1:     340.94425: -0.0274245 0.0415953 0.171831 0.810282
#>   2:     340.93440: -0.0274205 0.0422745 0.170657 0.808213
#>   3:     340.92348: -0.0274161 0.0447136 0.170835 0.807844
#>   4:     340.91370: -0.0274100 0.0453986 0.169929 0.805652
#>   5:     340.90869: -0.0274003 0.0476051 0.170026 0.804585
#>   6:     340.90521: -0.0273777 0.0482184 0.169865 0.802336
#>   7:     340.90248: -0.0273321 0.0489754 0.171281 0.801438
#>   8:     340.89717: -0.0270041 0.0480428 0.177299 0.797774
#>   9:     340.86736: -0.0231806 0.0537295 0.174808 0.789982
#>  10:     340.73004: -0.0101016 0.0439580 0.164309 0.806907
#>  11:     340.56766: 0.0160790 0.0439679 0.183551 0.801336
#>  12:     340.52900: 0.0197153 0.0459647 0.190266 0.789344
#>  13:     340.52544: 0.0172714 0.0457522 0.185566 0.793380
#>  14:     340.52539: 0.0175126 0.0455331 0.185311 0.793841
#>  15:     340.52539: 0.0175241 0.0455418 0.185276 0.793848
#>  16:     340.52539: 0.0175254 0.0455424 0.185274 0.793849
#> 
#> Final Estimate of the Negative LLH:
#>  LLH:  -493.1704    norm LLH:  -1.98859 
#>           mu        omega       alpha1        beta1 
#> 6.077311e-04 5.476465e-05 1.852739e-01 7.938490e-01 
#> 
#> R-optimhess Difference Approximated Hessian Matrix:
#>                  mu       omega       alpha1        beta1
#> mu      -323896.988    -3942880    -1274.877    -2692.172
#> omega  -3942880.327 -3716487012 -2283988.677 -3321697.132
#> alpha1    -1274.877    -2283989    -1841.165    -2492.527
#> beta1     -2692.172    -3321697    -2492.527    -3686.317
#> attr(,"time")
#> Time difference of 0.001632214 secs
#> 
#> --- END OF TRACE ---
#> 
#> 
#> Time to Estimate Parameters:
#>  Time difference of 0.006318092 secs
#> 
#> Title:
#>  GARCH Modelling 
#> 
#> Call:
#>  garchFit(formula = Open ~ garch(1, 1), data = returns(X.timeSeries)) 
#> 
#> Mean and Variance Equation:
#>  Open ~ garch(1, 1)
#> <environment: 0x613d7fb58dc8>
#>  [data = returns(X.timeSeries)]
#> 
#> Conditional Distribution:
#>  norm 
#> 
#> Coefficient(s):
#>         mu       omega      alpha1       beta1  
#> 6.0773e-04  5.4765e-05  1.8527e-01  7.9385e-01  
#> 
#> Std. Errors:
#>  based on Hessian 
#> 
#> Error Analysis:
#>         Estimate  Std. Error  t value Pr(>|t|)    
#> mu     6.077e-04   1.778e-03    0.342   0.7325    
#> omega  5.476e-05   3.765e-05    1.455   0.1458    
#> alpha1 1.853e-01   8.095e-02    2.289   0.0221 *  
#> beta1  7.938e-01   6.301e-02   12.599   <2e-16 ***
#> ---
#> Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
#> 
#> Log Likelihood:
#>  493.1704    normalized:  1.98859 
#> 
#> Description:
#>  Thu Jan 29 21:01:06 2026 by user: georgi 
#> 
garchFit(100*(High-Low) ~ garch(1,1), data = returns(X.timeSeries))
#> 
#> Series Initialization:
#>  ARMA Model:                arma
#>  Formula Mean:              ~ arma(0, 0)
#>  GARCH Model:               garch
#>  Formula Variance:          ~ garch(1, 1)
#>  ARMA Order:                0 0
#>  Max ARMA Order:            0
#>  GARCH Order:               1 1
#>  Max GARCH Order:           1
#>  Maximum Order:             1
#>  Conditional Dist:          norm
#>  h.start:                   2
#>  llh.start:                 1
#>  Length of Series:          248
#>  Recursion Init:            mci
#>  Series Scale:              1.759168
#> 
#> Parameter Initialization:
#>  Initial Parameters:          $params
#>  Limits of Transformations:   $U, $V
#>  Which Parameters are Fixed?  $includes
#>  Parameter Matrix:
#>                      U            V       params includes
#>     mu     -0.01484999   0.01484999 -0.001484999     TRUE
#>     omega   0.00000100 100.00000000  0.100000000     TRUE
#>     alpha1  0.00000001   0.99999999  0.100000000     TRUE
#>     gamma1 -0.99999999   0.99999999  0.100000000    FALSE
#>     beta1   0.00000001   0.99999999  0.800000000     TRUE
#>     delta   0.00000000   2.00000000  2.000000000    FALSE
#>     skew    0.10000000  10.00000000  1.000000000    FALSE
#>     shape   1.00000000  10.00000000  4.000000000    FALSE
#>  Index List of Parameters to be Optimized:
#>     mu  omega alpha1  beta1 
#>      1      2      3      5 
#>  Persistence:                  0.9 
#> 
#> 
#> --- START OF TRACE ---
#> Selected Algorithm: nlminb 
#> 
#> R coded nlminb Solver: 
#> 
#>   0:     338.79385: -0.00148500 0.100000 0.100000 0.800000
#>   1:     338.46090: -0.00148500 0.0930914 0.100064 0.793760
#>   2:     338.24428: -0.00148500 0.0927929 0.109355 0.793249
#>   3:     338.13232: -0.00148499 0.0865650 0.112004 0.786856
#>   4:     337.95165: -0.00148499 0.0903645 0.120451 0.785916
#>   5:     337.83363: -0.00148498 0.0880066 0.123980 0.777629
#>   6:     337.71984: -0.00148497 0.0934008 0.130363 0.773527
#>   7:     337.62836: -0.00148495 0.0936956 0.132882 0.764569
#>   8:     337.54525: -0.00148493 0.0995383 0.138251 0.759700
#>   9:     337.47146: -0.00148490 0.100375 0.140485 0.750701
#>  10:     337.40214: -0.00148486 0.106092 0.145870 0.745701
#>  11:     337.33811: -0.00148478 0.106731 0.148700 0.736855
#>  12:     337.27971: -0.00148466 0.112207 0.154164 0.731676
#>  13:     337.22953: -0.00148446 0.113576 0.156827 0.722862
#>  14:     337.17847: -0.00148403 0.118016 0.163018 0.717519
#>  15:     337.15010: -0.00148366 0.121418 0.163737 0.708886
#>  16:     337.12658: -0.00148293 0.117033 0.171770 0.710523
#>  17:     337.08704: -0.00148284 0.122915 0.178235 0.693051
#>  18:     337.03054: -0.00148210 0.136576 0.184775 0.680722
#>  19:     337.00277: -0.00148078 0.144688 0.188565 0.663381
#>  20:     336.98756: -0.00147267 0.154426 0.195482 0.648918
#>  21:     336.97675: -0.00144968 0.154594 0.204920 0.641641
#>  22:     336.97583: -0.00142340 0.157318 0.206707 0.637693
#>  23:     336.97552: -0.00139450 0.158213 0.207352 0.636343
#>  24:     336.97467: -0.00128837 0.159968 0.208616 0.633682
#>  25:     336.97264: -0.000975485 0.163087 0.210866 0.628926
#>  26:     336.96825: -0.000197740 0.167982 0.214399 0.621399
#>  27:     336.95854: 0.00166593 0.175778 0.220016 0.609263
#>  28:     336.93800: 0.00599522 0.188577 0.229193 0.588989
#>  29:     336.90456: 0.0144044 0.207806 0.242786 0.557755
#>  30:     336.89568: 0.0148500 0.204967 0.240403 0.561330
#>  31:     336.89184: 0.0148500 0.157893 0.205616 0.629260
#>  32:     336.86883: 0.0148500 0.184188 0.226104 0.592041
#>  33:     336.85962: 0.0148500 0.173554 0.219500 0.608290
#>  34:     336.85725: 0.0148500 0.155984 0.209335 0.635860
#>  35:     336.85498: 0.0148500 0.164112 0.214240 0.623640
#>  36:     336.85486: 0.0148500 0.163014 0.213762 0.625457
#>  37:     336.85485: 0.0148500 0.162753 0.213693 0.625907
#>  38:     336.85485: 0.0148500 0.162780 0.213714 0.625865
#>  39:     336.85485: 0.0148500 0.162785 0.213717 0.625858
#> 
#> Final Estimate of the Negative LLH:
#>  LLH:  476.9354    norm LLH:  1.923127 
#>         mu      omega     alpha1      beta1 
#> 0.02612363 0.50376670 0.21371740 0.62585764 
#> 
#> R-optimhess Difference Approximated Hessian Matrix:
#>                 mu      omega      alpha1       beta1
#> mu     -132.010667  -11.71868    6.265931   -31.66371
#> omega   -11.718680 -165.10094 -231.511196  -402.35533
#> alpha1    6.265931 -231.51120 -664.732441  -708.75592
#> beta1   -31.663715 -402.35533 -708.755923 -1073.12968
#> attr(,"time")
#> Time difference of 0.001746893 secs
#> 
#> --- END OF TRACE ---
#> 
#> 
#> Time to Estimate Parameters:
#>  Time difference of 0.00990963 secs
#> 
#> Title:
#>  GARCH Modelling 
#> 
#> Call:
#>  garchFit(formula = 100 * (High - Low) ~ garch(1, 1), data = returns(X.timeSeries)) 
#> 
#> Mean and Variance Equation:
#>  100 * (High - Low) ~ garch(1, 1)
#> <environment: 0x613d7fb58dc8>
#>  [data = returns(X.timeSeries)]
#> 
#> Conditional Distribution:
#>  norm 
#> 
#> Coefficient(s):
#>       mu     omega    alpha1     beta1  
#> 0.026124  0.503767  0.213717  0.625858  
#> 
#> Std. Errors:
#>  based on Hessian 
#> 
#> Error Analysis:
#>         Estimate  Std. Error  t value Pr(>|t|)    
#> mu       0.02612     0.08964    0.291 0.770733    
#> omega    0.50377     0.35141    1.434 0.151694    
#> alpha1   0.21372     0.09596    2.227 0.025941 *  
#> beta1    0.62586     0.18294    3.421 0.000623 ***
#> ---
#> Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
#> 
#> Log Likelihood:
#>  -476.9354    normalized:  -1.923127 
#> 
#> Description:
#>  Thu Jan 29 21:01:06 2026 by user: georgi 
#> 

## GO-GARCH Modelling  (not yet!!) % FIXME

## data(DowJones30, package="fEcofin") # no longer exists
## X <- returns(as.timeSeries(DowJones30)); head(X)
## N <- 5; ans <- .gogarchFit(data = X[, 1:N], trace = FALSE); ans
## ans@h.t
```
