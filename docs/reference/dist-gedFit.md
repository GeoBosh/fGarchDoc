# Generalized error distribution parameter estimation

Function to fit the parameters of the generalized error distribution.

## Usage

``` r
gedFit(x, ...)
```

## Arguments

- x:

  a numeric vector of quantiles.

- ...:

  parameters parsed to the optimization function `nlm`.

## Value

`gedFit` returns a list with the following components:

- par:

  The best set of parameters found.

- objective:

  The value of objective corresponding to `par`.

- convergence:

  An integer code, 0 indicates successful convergence.

- message:

  A character string giving any additional information returned by the
  optimizer, or NULL. For details, see PORT documentation.

- iterations:

  Number of iterations performed.

- evaluations:

  Number of objective function and gradient function evaluations.

## References

Nelson D.B. (1991); *Conditional Heteroscedasticity in Asset Returns: A
New Approach*, Econometrica, 59, 347–370.

Fernandez C., Steel M.F.J. (2000); *On Bayesian Modelling of Fat Tails
and Skewness*, Preprint, 31 pages.

## Author

Diethelm Wuertz for the Rmetrics R-port

## See also

[`ged`](https://geobosh.github.io/fGarchDoc/reference/dist-ged.md),
[`sgedFit`](https://geobosh.github.io/fGarchDoc/reference/dist-sgedFit.md)

## Examples

``` r
set.seed(1953)
r <- rged(n = 1000)

gedFit(r)
#> $par
#>        mean          sd          nu 
#> -0.01416477  1.00755265  1.85747923 
#> 
#> $objective
#> [1] 1425.889
#> 
#> $convergence
#> [1] 0
#> 
#> $iterations
#> [1] 19
#> 
#> $evaluations
#> function gradient 
#>       27       91 
#> 
#> $message
#> [1] "relative convergence (4)"
#> 
```
