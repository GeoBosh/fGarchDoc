# Modelling heterskedasticity in financial time series

The Rmetrics package fGarch is a collection of functions to analyze and
model heteroskedastic behavior in financial time series. The website
<https://geobosh.github.io/fGarchDoc/> contains the documentation of the
package with a reference section in which the functions are grouped by
topic.

## Author

Diethelm Wuertz \[aut\] (original code), Yohan Chalabi \[aut\], Tobias
Setz \[aut\], Martin Maechler \[ctb\]
(\<https://orcid.org/0000-0002-8685-9910\>), Chris Boudt \[ctb\] Pierre
Chausse \[ctb\], Michal Miklovac \[ctb\], Georgi N. Boshnakov \[cre,
aut\]

Maintainer: Georgi N. Boshnakov \<georgi.boshnakov@manchester.ac.uk\>

## 1 Introduction

GARCH, Generalized Autoregressive Conditional Heteroskedastic, models
have become important in the analysis of time series data, particularly
in financial applications when the goal is to analyze and forecast
volatility.

For this purpose, the family of GARCH functions offers functions for
simulating, estimating and forecasting various univariate GARCH-type
time series models in the conditional variance and an ARMA specification
in the conditional mean. The function
[`garchFit`](https://geobosh.github.io/fGarchDoc/reference/garchFit.md)
is a numerical implementation of the maximum log-likelihood approach
under different assumptions, Normal, Student-t, GED errors or their
skewed versions. The parameter estimates are checked by several
diagnostic analysis tools including graphical features and hypothesis
tests. Functions to compute n-step ahead forecasts of both the
conditional mean and variance are also available.

The number of GARCH models is immense, but the most influential models
were the first. Beside the standard ARCH model introduced by Engle
\[1982\] and the GARCH model introduced by Bollerslev \[1986\], the
function `garchFit` also includes the more general class of asymmetric
power ARCH models, named APARCH, introduced by Ding, Granger and Engle
\[1993\]. The APARCH models include as special cases the TS-GARCH model
of Taylor \[1986\] and Schwert \[1989\], the GJR-GARCH model of Glosten,
Jaganathan, and Runkle \[1993\], the T-ARCH model of Zakoian \[1993\],
the N-ARCH model of Higgins and Bera \[1992\], and the Log-ARCH model of
Geweke \[1986\] and Pentula \[1986\].

There exist a collection of review articles by Bollerslev, Chou and
Kroner \[1992\], Bera and Higgins \[1993\], Bollerslev, Engle and Nelson
\[1994\], Engle \[2001\], Engle and Patton \[2001\], and Li, Ling and
McAleer \[2002\] which give a good overview of the scope of the
research.

## 2 Time series simulation

Functions to simulate artificial GARCH and APARCH time series processes.

|                                                                           |                                                 |
|---------------------------------------------------------------------------|-------------------------------------------------|
| [`garchSpec`](https://geobosh.github.io/fGarchDoc/reference/garchSpec.md) | specifies an univariate GARCH time series model |
| [`garchSim`](https://geobosh.github.io/fGarchDoc/reference/garchSim.md)   | simulates a GARCH/APARCH process                |

## 3 Parameter estimation

Functions to fit the parameters of GARCH and APARCH time series
processes.

|                                                                         |                                        |
|-------------------------------------------------------------------------|----------------------------------------|
| [`garchFit`](https://geobosh.github.io/fGarchDoc/reference/garchFit.md) | fits the parameters of a GARCH process |

### Extractor Functions:

|                                                                                     |                                                                 |
|-------------------------------------------------------------------------------------|-----------------------------------------------------------------|
| [`residuals`](https://geobosh.github.io/fGarchDoc/reference/methods-residuals.md)   | extracts residuals from a fitted `"fGARCH"` object              |
| [`fitted`](https://geobosh.github.io/fGarchDoc/reference/methods-fitted.md)         | extracts fitted values from a fitted `"fGARCH"` object          |
| [`volatility`](https://geobosh.github.io/fGarchDoc/reference/methods-volatility.md) | extracts conditional volatility from a fitted `"fGARCH"` object |
| [`coef`](https://geobosh.github.io/fGarchDoc/reference/methods-coef.md)             | extracts coefficients from a fitted `"fGARCH"` object           |
| [`formula`](https://geobosh.github.io/fGarchDoc/reference/methods-formula.md)       | extracts formula expression from a fitted `"fGARCH"` object     |

## 4 Forecasting

Functions to forecast mean and variance of GARCH and APARCH processes.

|                                                                               |                                              |
|-------------------------------------------------------------------------------|----------------------------------------------|
| [`predict`](https://geobosh.github.io/fGarchDoc/reference/methods-predict.md) | forecasts from an object of class `"fGARCH"` |

## 5 Standardized distributions

This section contains functions to model standardized distributions.

### Skew normal distribution:

|                                                                              |                                             |
|------------------------------------------------------------------------------|---------------------------------------------|
| [`[dpqr]norm`](https://rdrr.io/r/stats/Normal.html)                          | Normal distribution (base R)                |
| [`[dpqr]snorm`](https://geobosh.github.io/fGarchDoc/reference/dist-snorm.md) | Skew normal distribution                    |
| [`snormFit`](https://geobosh.github.io/fGarchDoc/reference/dist-snormFit.md) | fits parameters of Skew normal distribution |

### Skew generalized error distribution:

|                                                                            |                                                        |
|----------------------------------------------------------------------------|--------------------------------------------------------|
| [`[dpqr]ged`](https://geobosh.github.io/fGarchDoc/reference/dist-ged.md)   | Generalized error distribution                         |
| [`[dpqr]sged`](https://geobosh.github.io/fGarchDoc/reference/dist-sged.md) | Skew Generalized error distribution                    |
| [`gedFit`](https://geobosh.github.io/fGarchDoc/reference/dist-gedFit.md)   | fits parameters of Generalized error distribution      |
| [`sgedFit`](https://geobosh.github.io/fGarchDoc/reference/dist-sgedFit.md) | fits parameters of Skew generalized error distribution |

### Skew standardized Student-t distribution:

|                                                                            |                                                             |
|----------------------------------------------------------------------------|-------------------------------------------------------------|
| [`[dpqr]std`](https://geobosh.github.io/fGarchDoc/reference/dist-std.md)   | Standardized Student-t distribution                         |
| [`[dpqr]sstd`](https://geobosh.github.io/fGarchDoc/reference/dist-sstd.md) | Skew standardized Student-t distribution                    |
| [`stdFit`](https://geobosh.github.io/fGarchDoc/reference/dist-stdFit.md)   | fits parameters of Standardized Student-t distribution      |
| [`sstdFit`](https://geobosh.github.io/fGarchDoc/reference/dist-sstdFit.md) | fits parameters of Skew standardized Student-t distribution |

### Absolute moments:

|                                                                                  |                                                 |
|----------------------------------------------------------------------------------|-------------------------------------------------|
| [`absMoments`](https://geobosh.github.io/fGarchDoc/reference/dist-absMoments.md) | computes absolute moments of these distribution |

## About Rmetrics

The `fGarch` Rmetrics package is written for educational support in
teaching “Computational Finance and Financial Engineering” and licensed
under the GPL.
