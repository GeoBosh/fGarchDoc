# Visualise skew normal, (skew) Student-t and (skew) GED distributions

Displays interactively the dependence of distributions on their
parameters. Package 'fGarch' provides sliders for the Student-t, GED,
skew normal, skew Student-t and skew GED distributions,

## Usage

``` r
stdSlider(type = c("dist", "rand"))
gedSlider(type = c("dist", "rand"))

snormSlider(type = c("dist", "rand"))
sstdSlider(type = c("dist", "rand"))
sgedSlider(type = c("dist", "rand"))
```

## Arguments

- type:

  a character string denoting which interactive plot should be
  displayed. Either a distribution plot `type = "dist"`, the default
  value, or a random variates plot, `type = "rand"`.

## Value

a Tcl object

## References

Nelson D.B. (1991); *Conditional Heteroscedasticity in Asset Returns: A
New Approach*, Econometrica, 59, 347–370.

Fernandez C., Steel M.F.J. (2000); *On Bayesian Modelling of Fat Tails
and Skewness*, Preprint, 31 pages.

## Author

Diethelm Wuertz for the Rmetrics R-port

## See also

[`snorm`](https://geobosh.github.io/fGarchDoc/reference/dist-snorm.md),
[`std`](https://geobosh.github.io/fGarchDoc/reference/dist-std.md),
[`sstd`](https://geobosh.github.io/fGarchDoc/reference/dist-sstd.md),
[`ged`](https://geobosh.github.io/fGarchDoc/reference/dist-ged.md),
[`sged`](https://geobosh.github.io/fGarchDoc/reference/dist-sged.md)

## Examples

``` r
if (FALSE) { # \dontrun{  
require(tcltk)

snormSlider("dist")
snormSlider("rand")

stdSlider("dist")
stdSlider("rand")

sstdSlider("dist")
sstdSlider("rand")

gedSlider("dist")
gedSlider("rand")

sgedSlider("dist")
sgedSlider("rand")
} # }
```
