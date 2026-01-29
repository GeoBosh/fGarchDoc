# Absolute moments of GARCH distributions

Computes absolute moments of the standard normal, standardized GED, and
standardized skew Student-t distributions.

## Usage

``` r
absMoments(n, density = c("dnorm", "dged", "dstd"), ...)
```

## Arguments

- n:

  the order of the absolute moment, can be a vector to compute several
  absolute moments at once.

- density:

  a character string naming a symmetric density function.

- ...:

  parameters passed to the density function.

## Details

`absMoments` returns a numeric vector of length `n` with the values of
the absolute moments, as specified by `n`, of the selected probability
density function (pdf).

If `density` names one of the densities in the signature of
`absMoments`, the moments are calculated from known formulas.

Otherwise, numerical integration is used and an attribute is attached to
the results to report an estimate of the error. Note that the density is
assumed symmetric wihtout a check.

## Value

a numeric vector

## References

Fernandez C., Steel M.F.J. (2000); *On Bayesian Modelling of Fat Tails
and Skewness*, Preprint, 31 pages.

## Author

Diethelm Wuertz for the Rmetrics R-port

## See also

[`ged`](https://geobosh.github.io/fGarchDoc/reference/dist-ged.md),
[`std`](https://geobosh.github.io/fGarchDoc/reference/dist-std.md)

## Examples

``` r
absMoments(1, "dstd", nu = 6)
#> [1] 0.75
absMoments(1, "dstd", nu = 600)
#> [1] 0.7975511
absMoments(1, "dstd", nu = 60000)
#> [1] 0.7978812
absMoments(1, "dstd", nu = 600000)
#> [1] 0.7978842

absMoments(1, "dnorm")
#> [1] 0.7978846

## excess kurtosis of t_nu is  6/(nu - 4)
nu <- 6
absMoments(2*2, "dstd", nu = nu) / absMoments(2*1, "dstd", nu = nu)^2 - 3
#> [1] 3
6/(nu-4)
#> [1] 3

## 4th moment for t_4 is infinite
absMoments(4, "dstd", nu = 4)
#> [1] Inf

absMoments(1, "dged", nu = 4)
#> [1] 0.8408964
```
