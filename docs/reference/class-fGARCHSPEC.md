# Class "fGARCHSPEC"

Specification structure for an univariate GARCH time series model.

## Objects from the Class

Objects can be created by calls of the function `garchSpec`. This object
specifies the parameters of an empirical GARCH process.

## Slots

- `call`::

  Object of class `"call"`: the call of the `garch` function.

- `formula`::

  Object of class `"formula"`: a list with two formula entries for the
  mean and variance equation.

- `model`::

  Object of class `"list"`: a list with the model parameters.

- `presample`::

  Object of class `"matrix"`: a numeric matrix with presample values.

- `distribution`::

  Object of class `"character"`: a character string with the name of the
  conditional distribution.

- `rseed`::

  Object of class `"numeric"`: an integer with the random number
  generator seed.

## Methods

- show:

  `signature(object = "fGARCHSPEC")`: prints an object of class
  'fGARCHSPEC'.

## Note

With Rmetrics Version 2.6.1 the class has been renamed from
`"garchSpec"` to `"fGARCHSPEC"`.

## Author

Diethelm Wuertz for the Rmetrics R-port

## Examples

``` r
spec = garchSpec()
spec
#> 
#> Formula: 
#>  ~ garch(1, 1)
#> Model:
#>  omega: 1e-06
#>  alpha: 0.1
#>  beta:  0.8
#> Distribution: 
#>  norm
#> Presample: 
#>   time         z     h y
#> 1    0 0.7436201 1e-05 0
```
