# Skew normal distribution parameter estimation

Fits the parameters of the skew normal distribution.

## Usage

``` r
snormFit(x, ...)
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

[`snormSlider`](https://geobosh.github.io/fGarchDoc/reference/dist-Slider.md)
(visualize),
[`snorm`](https://geobosh.github.io/fGarchDoc/reference/dist-snorm.md),
[`absMoments`](https://geobosh.github.io/fGarchDoc/reference/dist-absMoments.md)

## Examples

``` r
set.seed(1953)
r <- rsnorm(n = 1000)

snormFit(r)
#> $par
#>       mean         sd         xi 
#> 0.06694004 1.03494430 1.57611278 
#> 
#> $objective
#> [1] 1413.746
#> 
#> $convergence
#> [1] 0
#> 
#> $iterations
#> [1] 24
#> 
#> $evaluations
#> function gradient 
#>       31       90 
#> 
#> $message
#> [1] "relative convergence (4)"
#> 
```
