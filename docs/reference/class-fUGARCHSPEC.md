# Class 'fUGARCHSPEC'

Class 'fUGARCHSPEC'.

## Objects from the Class

Objects can be created by calls of the form `new("fUGARCHSPEC", ...)`.

## Slots

- `model`::

  Object of class `"list"` \~~

- `distribution`::

  Object of class `"list"` \~~

- `optimization`::

  Object of class `"list"` \~~

- `documentation`::

  Object of class `"list"` \~~

## Methods

No methods defined with class `"fUGARCHSPEC"` in the signature.

## Note

Was this class meant to replace `"fGARCHSPEC"`?

(GNB) This class seems to be meant for internal use by the package.

(GNB) Amendment: no, functions `.ugarchSpec` and `.ugarchFit` are
exported. `.ugarchFit` fits the model from a spec, unlike `garchFit`.

TODO: There is something unfinished here. Check and sort out. See also
`fUGARCHSPEC-class`

## See also

class
`"`[`fGARCH`](https://geobosh.github.io/fGarchDoc/reference/class-fGARCH.md)`"`

## Examples

``` r
showClass("fUGARCHSPEC")
#> Class "fUGARCHSPEC" [package "fGarch"]
#> 
#> Slots:
#>                                                               
#> Name:          model  distribution  optimization documentation
#> Class:          list          list          list          list
```
