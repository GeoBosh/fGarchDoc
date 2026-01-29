# Extract GARCH model formula

Extracts formula from a formula GARCH object.

## Methods

Methods for `formula` defined in package fGarch:

- object = "fGARCH":

  Extractor function for formula expression.

## Details

`formula` is a generic function which extracts the formula expression
from objects returned by modeling functions.

The `"fGARCH"` method extracts the `@formula` expression slot from an
object of class `"fGARCH"` as returned by the function `garchFit`.

The returned formula has always a left hand side. If the argument `data`
was an univariate time series and no name was specified to the series,
then the left hand side is assigned the name of the data.set. In the
multivariate case the rectangular `data` object must always have column
names, otherwise the fitting will be stopped with an error message

The class of the returned value depends on the input to the function
`garchFit` who created the object. The returned value is always of the
same class as the input object to the argument `data` in the function
`garchFit`, i.e. if you fit a `"timeSeries"` object, you will get back
from the function `fitted` also a `"timeSeries"` object, if you fit an
object of class `"zoo"`, you will get back again a `"zoo"` object. The
same holds for a `"numeric"` vector, for a `"data.frame"`, and for
objects of class `"ts", "mts"`.

In contrast, the slot itself returns independent of the class of the
data input always a numeric vector, i.e. the function call
r`slot(object, "fitted")` will return a numeric vector.

## Note

(GNB) Contrary to the description of the returned value of the
`"fGARCH"` method, it is always `"numeric"`.

TODO: either implement the documented behaviour or fix the
documentation.

## Author

Diethelm Wuertz for the Rmetrics R-port

## See also

[`garchFit`](https://geobosh.github.io/fGarchDoc/reference/garchFit.md),
class
[`fGARCH`](https://geobosh.github.io/fGarchDoc/reference/class-fGARCH.md)

## Examples

``` r
set.seed(2024)
fit <- garchFit(~garch(1, 1), data = garchSim(), trace = FALSE)
   
formula(fit)
#> data ~ garch(1, 1)
#> attr(,"data")
#> [1] "data = garchSim()"
#> <environment: 0x613d7eb668f0>

## A Bivariate series and mis-specified formula:
x <- garchSim(n = 500)
y <- garchSim(n = 500)
z <- cbind(x, y)
colnames(z)
#> [1] "garch.1" "garch.2"
class(z)
#> [1] "timeSeries"
#> attr(,"package")
#> [1] "timeSeries"
if (FALSE) { # \dontrun{
garchFit(z ~garch(1, 1), data = z, trace = FALSE)
} # }
# Returns:
# Error in .garchArgsParser(formula = formula, data = data, trace = FALSE) :  
#   Formula and data units do not match.
   
## Doubled column names in data set - formula can't fit:
colnames(z) <- c("x", "x")
z[1:6,]
#> GMT 
#>                        x             x
#> 2024-09-16 -0.0009479484  7.362291e-04
#> 2024-09-17  0.0030573851  3.241022e-03
#> 2024-09-18  0.0046413667  3.294819e-07
#> 2024-09-19  0.0014175724 -2.040258e-03
#> 2024-09-20 -0.0003273780 -7.098226e-04
#> 2024-09-21  0.0020663036  1.077096e-04
if (FALSE) { # \dontrun{
garchFit(x ~garch(1, 1), data = z, trace = FALSE)
} # }
# Again the error will be noticed:
# Error in garchFit(x ~ garch(1, 1), data = z) : 
#   Column names of data are not unique.

## Missing column names in data set - formula can't fit:
z.mat <- as.matrix(z)
colnames(z.mat) <- NULL
z.mat[1:6,]
#>                     [,1]          [,2]
#> 2024-09-16 -0.0009479484  7.362291e-04
#> 2024-09-17  0.0030573851  3.241022e-03
#> 2024-09-18  0.0046413667  3.294819e-07
#> 2024-09-19  0.0014175724 -2.040258e-03
#> 2024-09-20 -0.0003273780 -7.098226e-04
#> 2024-09-21  0.0020663036  1.077096e-04
if (FALSE) { # \dontrun{
garchFit(x ~ garch(1, 1), data = z.mat, trace = FALSE)
} # }
# Again the error will be noticed:
# Error in .garchArgsParser(formula = formula, data = data, trace = FALSE) : 
#   Formula and data units do not match
```
