# Student-t distribution parameter estimation

Fits the parameters of the standardized Student-t distribution.

## Usage

``` r
stdFit(x, ...)
```

## Arguments

- x:

  a numeric vector of quantiles.

- ...:

  parameters parsed to the optimization function `nlm`.

## Value

`stdFit` returns a list with the following components:

- par:

  The best set of parameters found.

- objective:

  The value of objective corresponding to `par`.

- convergence:

  An integer code. 0 indicates successful convergence.

- message:

  A character string giving any additional information returned by the
  optimizer, or NULL. For details, see PORT documentation.

- iterations:

  Number of iterations performed.

- evaluations:

  Number of objective function and gradient function evaluations.

## References

Fernandez C., Steel M.F.J. (2000); *On Bayesian Modelling of Fat Tails
and Skewness*, Preprint, 31 pages.

## Author

Diethelm Wuertz for the Rmetrics R-port

## See also

[`std`](https://geobosh.github.io/fGarchDoc/reference/dist-std.md),
[`stdSlider`](https://geobosh.github.io/fGarchDoc/reference/dist-Slider.md)

## Examples

``` r
set.seed(1953)
r <- rstd(n = 1000)

stdFit(r)
#> $par
#>        mean          sd          nu 
#> -0.04913403  1.02055890  3.96747983 
#> 
#> $objective
#> [1] 1353.659
#> 
#> $convergence
#> [1] 0
#> 
#> $iterations
#> [1] 15
#> 
#> $evaluations
#> function gradient 
#>       28       75 
#> 
#> $message
#> [1] "relative convergence (4)"
#> 
```
