# Skew Student-t distribution parameter estimation

Fits the parameters of the skew Student-t distribution.

## Usage

``` r
sstdFit(x, ...)
```

## Arguments

- x:

  a numeric vector of quantiles.

- ...:

  parameters passed to the optimization function `nlm`.

## Value

a list with the following components:

- par:

  the best set of parameters found;

- objective:

  the value of objective corresponding to `par`;

- convergence:

  an integer code. 0 indicates successful convergence;

- message:

  a character string giving any additional information returned by the
  optimizer, or NULL. For details, see PORT documentation;

- iterations:

  number of iterations performed;

- evaluations:

  number of objective function and gradient function evaluations.

## References

Fernandez C., Steel M.F.J. (2000); *On Bayesian Modelling of Fat Tails
and Skewness*, Preprint, 31 pages.

## Author

Diethelm Wuertz for the Rmetrics R-port

## See also

[`sstd`](https://geobosh.github.io/fGarchDoc/reference/dist-sstd.md),
[`stdFit`](https://geobosh.github.io/fGarchDoc/reference/dist-stdFit.md)

## Examples

``` r
set.seed(1953)
r <- rsstd(n = 1000)

sstdFit(r)
#> $minimum
#> [1] 1306.033
#> 
#> $estimate
#>        mean          sd          nu          xi 
#> -0.01376393  1.00314970  4.21091035  1.37308787 
#> 
#> $gradient
#>          mean            sd            nu            xi 
#>  5.691163e-04  3.685488e-04  2.985997e-05 -1.288313e-04 
#> 
#> $code
#> [1] 1
#> 
#> $iterations
#> [1] 18
#> 
```
