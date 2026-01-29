# Control GARCH fitting algorithms

Control parameters for the GARCH fitting algorithms.

## Usage

``` r
garchFitControl(
    llh = c("filter", "internal", "testing"),
    nlminb.eval.max = 2000,
    nlminb.iter.max = 1500,
    nlminb.abs.tol = 1.0e-20,
    nlminb.rel.tol = 1.0e-14,
    nlminb.x.tol = 1.0e-14,
    nlminb.step.min = 2.2e-14,
    nlminb.scale = 1,
    nlminb.fscale = FALSE,
    nlminb.xscale = FALSE,
    sqp.mit = 200,
    sqp.mfv = 500,
    sqp.met = 2,
    sqp.mec = 2,
    sqp.mer = 1,
    sqp.mes = 4,
    sqp.xmax = 1.0e3,
    sqp.tolx = 1.0e-16,
    sqp.tolc = 1.0e-6,
    sqp.tolg = 1.0e-6,
    sqp.told = 1.0e-6,
    sqp.tols = 1.0e-4,
    sqp.rpf = 1.0e-4,
    lbfgsb.REPORT = 10,
    lbfgsb.lmm = 20,
    lbfgsb.pgtol = 1e-14,
    lbfgsb.factr = 1,
    lbfgsb.fnscale = FALSE,
    lbfgsb.parscale = FALSE,
    nm.ndeps = 1e-14,
    nm.maxit = 10000,
    nm.abstol = 1e-14,
    nm.reltol = 1e-14,
    nm.alpha = 1.0,
    nm.beta = 0.5,
    nm.gamma = 2.0,
    nm.fnscale = FALSE,
    nm.parscale = FALSE)
```

## Arguments

- llh:

  `llh = c("filter", "internal", "testing")[1]`, defaults to `"filter"`.

&nbsp;

- nlminb.eval.max:

  maximum number of evaluations of the objective function, defaults to
  200.

- nlminb.iter.max:

  maximum number of iterations, defaults to 150.

&nbsp;

- nlminb.abs.tol:

  absolute tolerance, defaults to 1e-20.

- nlminb.rel.tol:

  relative tolerance, defaults to 1e-10.

- nlminb.x.tol:

  X tolerance, defaults to 1.5e-8.

- nlminb.fscale:

  defaults to FALSE.

- nlminb.xscale:

  defaulkts to FALSE.

- nlminb.step.min:

  minimum step size, defaults to 2.2e-14.

- nlminb.scale:

  defaults to 1.

&nbsp;

- sqp.mit:

  maximum number of iterations, defaults to 200.

- sqp.mfv:

  maximum number of function evaluations, defaults to 500.

- sqp.met:

  specifies scaling strategy:  
  sqp.met=1 - no scaling,  
  sqp.met=2 - preliminary scaling in 1st iteration (default),  
  sqp.met=3 - controlled scaling,  
  sqp.met=4 - interval scaling,  
  sqp.met=5 - permanent scaling in all iterations.

- sqp.mec:

  correction for negative curvature:  
  sqp.mec=1 - no correction,  
  sqp.mec=2 - Powell correction (default).

- sqp.mer:

  restarts after unsuccessful variable metric updates:  
  sqp.mer=0 - no restarts,  
  sqp.mer=1 - standard restart.

- sqp.mes:

  interpolation method selection in a line search:  
  sqp.mes=1 - bisection,  
  sqp.mes=2 - two point quadratic interpolation,  
  sqp.mes=3 - three point quadratic interpolation,  
  sqp.mes=4 - three point cubic interpolation (default).

- sqp.xmax:

  maximum stepsize, defaults to 1.0e+3.

- sqp.tolx:

  tolerance for the change of the coordinate vector, defaults to
  1.0e-16.

- sqp.tolc:

  tolerance for the constraint violation, defaults to 1.0e-6.

- sqp.tolg:

  tolerance for the Lagrangian function gradient, defaults to 1.0e-6.

- sqp.told:

  defaults to 1.0e-6.

- sqp.tols:

  defaults to 1.0e-4.

- sqp.rpf:

  value of the penalty coefficient, default to1.0D-4. The default velue
  may be relatively small. Therefore, larger value, say one, can
  sometimes be more suitable.

&nbsp;

- lbfgsb.REPORT:

  the frequency of reports for the `"BFGS"` and `"L-BFGS-B"` methods if
  `control$trace` is positive. Defaults to every 10 iterations.

- lbfgsb.lmm:

  an integer giving the number of BFGS updates retained in the
  `"L-BFGS-B"` method, It defaults to 5.

- lbfgsb.factr:

  controls the convergence of the `"L-BFGS-B"` method. Convergence
  occurs when the reduction in the objective is within this factor of
  the machine tolerance. Default is 1e7, that is a tolerance of about
  1.0e-8.

- lbfgsb.pgtol:

  helps control the convergence of the `"L-BFGS-B"` method. It is a
  tolerance on the projected gradient in the current search direction.
  This defaults to zero, when the check is suppressed.

- lbfgsb.fnscale:

  defaults to FALSE.

- lbfgsb.parscale:

  defaults to FALSE.

&nbsp;

- nm.ndeps:

  a vector of step sizes for the finite-difference approximation to the
  gradient, on par/parscale scale. Defaults to 1e-3.

- nm.maxit:

  the maximum number of iterations. Defaults to 100 for the
  derivative-based methods, and 500 for `"Nelder-Mead"`. For `"SANN"`
  maxit gives the total number of function evaluations. There is no
  other stopping criterion. Defaults to 10000.

- nm.abstol:

  the absolute convergence tolerance. Only useful for non-negative
  functions, as a tolerance for reaching zero.

- nm.reltol:

  relative convergence tolerance. The algorithm stops if it is unable to
  reduce the value by a factor of `reltol * (abs(val) + reltol)` at a
  step. Defaults to `sqrt(.Machine$double.eps)`, typically about 1e-8.

- nm.alpha, nm.beta, nm.gamma:

  scaling parameters for the "Nelder-Mead" method. alpha is the
  reflection factor (default 1.0), beta the contraction factor (0.5),
  and gamma the expansion factor (2.0).

- nm.fnscale:

  an overall scaling to be applied to the value of fn and gr during
  optimization. If negative, turns the problem into a maximization
  problem. Optimization is performed on `fn(par) / nm.fnscale`.

- nm.parscale:

  a vector of scaling values for the parameters. Optimization is
  performed on par/parscale and these should be comparable in the sense
  that a unit change in any element produces about a unit change in the
  scaled value.

## Value

a list

## Author

Diethelm Wuertz for the Rmetrics R-port,  
R Core Team for the 'optim' R-port,  
Douglas Bates and Deepayan Sarkar for the 'nlminb' R-port,  
Bell-Labs for the underlying PORT Library,  
Ladislav Luksan for the underlying Fortran SQP Routine,  
Zhu, Byrd, Lu-Chen and Nocedal for the underlying L-BFGS-B Routine.

## See also

[`garchFit`](https://geobosh.github.io/fGarchDoc/reference/garchFit.md)

## Examples

``` r
##
```
