# Skew generalized error distribution parameter estimation

Function to fit the parameters of the skew generalized error
distribution.

## Usage

``` r
sgedFit(x, ...)
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

Nelson D.B. (1991); *Conditional Heteroscedasticity in Asset Returns: A
New Approach*, Econometrica, 59, 347–370.

Fernandez C., Steel M.F.J. (2000); *On Bayesian Modelling of Fat Tails
and Skewness*, Preprint, 31 pages.

## Author

Diethelm Wuertz for the Rmetrics R-port

## See also

[`sged`](https://geobosh.github.io/fGarchDoc/reference/dist-sged.md),
[`sgedSlider`](https://geobosh.github.io/fGarchDoc/reference/dist-Slider.md)

## Examples

``` r
set.seed(1953)
r <- rsged(n = 1000)
       
sgedFit(r)
#> $par
#>       mean         sd         nu         xi 
#> 0.01115429 1.00416120 1.92236744 1.48742248 
#> 
#> $objective
#> [1] 1390.069
#> 
#> $convergence
#> [1] 0
#> 
#> $iterations
#> [1] 24
#> 
#> $evaluations
#> function gradient 
#>       33      147 
#> 
#> $message
#> [1] "relative convergence (4)"
#> 
```
