# Changelog

## CHANGES in fGarch VERSION 4052.93 (2025-12-12, svn r6482–r6544)

CRAN release: 2025-12-12

- emphasised that the skew normal distribution in fGarch is different
  from what is usually called skew normal distribution. Similarly for
  the other skew distributions.

- replaced a call to ‘warnings’ (plural) with ‘warning’ (singular) in
  `garchSpec`. The old one was clearly a typo and was not issuing the
  intended warning about the violation of the stationarity condition for
  GARCH models.

- improved the layout of the reference section of the pkgdown site.

- edited the help page of class `"fGARCH"`. In particular, added
  cross-references to the help pages of the individual methods.

## CHANGES in fGarch VERSION 4033.92 (2024-03-26, svn r6481–r6481)

CRAN release: 2024-03-26

- added VaR and ES plots to the `plot` method for fitted GARCH models.

- documented with examples that argument `which` of the plot method for
  fitted GARCH objects can be of length greater than one.

- added a link to the website created with pkgdown to file
  ‘DESCRIPTION’.

## CHANGES in fGarch VERSION 4032.91 (2024-02-02, svn r6436–r6479)

CRAN release: 2024-02-01

- added computation of Value-at-Risk (VaR) and expected shortfall (ES)
  for fitted GARCH and APARCH models (in-sample and in the predict
  method). Just use something like `Var(fitted_object)`,
  `ES(fitted_object)` or `predict(fitted_object, ..., p_loss = 0.05)`.

## CHANGES in fGarch VERSION 4031.90 (2023-10-15, svn r6333–r6435)

CRAN release: 2023-10-15

- added `"fGARCH"` method for
  [`stats::tsdiag`](https://rdrr.io/r/stats/tsdiag.html). The method
  produces diagnostic plot for fitted GARCH/APARCH models and computes
  some diagnostic tests. The plots can be chosen interactively and/or
  via arguments. The test results are in the returned value. The method
  is in development in that more plots may be made available and
  additional tests included in the returned value.

- refactored the `"fGARCH"` method for ‘summary’ to return an object
  from S3 class ‘summary_fGARCH’ equipped with a ‘print’ method. The
  printout is the same as before, except that now the numbers in the
  statistics column for the residual diagnostics are aligned on the
  decimal point (previously they were left-aligned due to a buglet).

- the `"fGARCH"` method for `fitted` was returning the data, not the
  fitted values. Fixes issue 6789, reported by Kouhei Hashinokuchi
  (hakoshie).

- the help pages for the `"fGARCH"` methods for
  [`fitted()`](https://geobosh.github.io/fGarchDoc/reference/methods-fitted.md)
  and
  [`residuals()`](https://geobosh.github.io/fGarchDoc/reference/methods-residuals.md)
  were stating that the returned results have the same class as the
  input time series. Actually, they return numeric vectors. (todo?: to
  make the returned values as previously documented,
  [`garchFit()`](https://geobosh.github.io/fGarchDoc/reference/garchFit.md)
  would need to put the original data or the necessary information in
  the fitted object, e.g., `object@fit$data`.

- some tests were using deprecated
  [`fBasics::.distCheck()`](https://geobosh.github.io/fBasicsDoc/reference/fBasics-deprecated.html)
  (notice the leading dot). Replaced such calls with the equivalent
  [`fBasics::distCheck()`](https://geobosh.github.io/fBasicsDoc/reference/dist-distCheck.html).

## CHANGES in fGarch VERSION 4022.89 (2022-11-05, from svn r6316–r6326)

CRAN release: 2022-11-05

- in `absMoments`, the absolute moments for the standardized Student-t
  distribution were wrong.

- in README, linked to the paper by Wuertz et al.

- substantially revised the documentation and filled gaps in it.

- removed the functions with suffix ‘\_orig’ which were kept
  temporarilly after the bug fix in v4021.87 since there were no
  reported problems with the fix.

## CHANGES in fGarch VERSION 4021.88 (2022-09-28, svn r6276)

CRAN release: 2022-09-29

- require Matrix (\>= 1.5-0) to avoid problems for users who have
  earlier versions of Matrix on their devices (thanks to Mikael Jagan
  for checking for not strict enough dependency on Matrix and alerting
  the maintainer).

## CHANGES in fGarch VERSION 4021.87 (2022-08-06, svn r6215–r6265)

CRAN release: 2022-08-06

### NEW MAINTAINER

- Georgi N. Boshnakov

### VERSION NUMBERS

- We continue to use the traditional Rmetrics scheme for numbering the
  versions of the package as Mmmr.n, where ‘M’ is the current major R
  version at the time of submission of the package to CRAN, ‘mm’ is the
  minor one and ‘r’ is the revision. ‘n’ is the sequential number of the
  CRAN submission of the package. For example, this release has version
  4021.87 since it was released when R 4.2.1 was current and ‘n’ in the
  previous version was 86.

### BUG FIXES

Fixed issue 6061 raised by William Scott, who also supplied examples.

- The quantile function, `qsnorm`, was wrong around 0.5. The error was
  in `.qsnorm`. For now its version before the fix is kept as
  `.qsnorm_orig`. Basically, branching was done w.r.t. `p = 0.5`, which
  is correct only for the symmetric case, `\xi = 1`, and should be
  `1/(1+\xi^2)` instead. More details in the source code. The error was
  affecting the central part of the distrbution with the interval
  becoming larger for `\xi` further away from 1.

- The cdf, `psnorm`, had an error at a single point, coinciding with the
  wrong value for `p = 0.5` returned by `qsnorm(0.5)` before the fix.
  The result was that `psnorm(qsnorm(0.5))` was returning 0.5, falsely
  giving reassurance that `qsnorm(0.5)` was correct.

- Not mentioned in issue 6061 but the same problems held for the other
  skewed distributions: `qsstd`, `psstd`, `qsged`, `psged`. The original
  versions of the relevant internal functions are kept for now with a
  suffix `_orig`, as above: `qsstd_orig`, `psstd_orig`, `qsged_orig`,
  `psged_orig`.

### Documentation

- Edited the documentation of `"garchSpec"` and `garchSim`. It was
  somewhat incomplete and contained leftovers, apparently from old
  versions of the functions.

- Documented the datasets. Previously the help page for them was a
  placeholder, without the names of the available datasets. There is no
  information about the time span of the data or how the returns were
  calculated.

## CHANGES in fGarch VERSION 4021.86 (2022-06-23, svn r6188)

CRAN release: 2022-07-16

### NEW MAINTAINER

- Tobias Setz

### Notes

- This is a CRAN release of version 4001.1, with trivial changes in
  ‘DESCRIPTION’.

## CHANGES in fGarch VERSION 4001.1 (2022-06-23, svn r6184–r6185)

### NEW MAINTAINER

- ad interim: Martin Maechler

### NEW FEATURES

- Packages [timeSeries](https://CRAN.R-project.org/package=timeSeries),
  [timeDate](https://CRAN.R-project.org/package=timeDate) and
  [fBasics](https://CRAN.R-project.org/package=fBasics) are no longer in
  `Depends`, but only in `Imports` and hence no longer automatically
  attached to the [`search()`](https://rdrr.io/r/base/search.html) path
  whenever fGarch is.

  This may require updates in your code, e.g., adding

  ``` R
     stopifnot(require("timeSeries"))
  ```

  as it has been done in our own fGarch’s examples and tests.

- [`.gogarchFit()`](https://geobosh.github.io/fGarchDoc/reference/garchFit.md)
  is at least *mentioned* in the documentation.

### BUG FIXES

- Added registration of compiled functionality for speed up and as good
  practice.

- Removed all `Depends:` entries and checked exactly which parts of
  packages, notably fBasics, timeDate, and timeSeries, are needed and
  imported only these.

- Eliminated warning about ‘length \> 1’ character formula in
  [`garchFit()`](https://geobosh.github.io/fGarchDoc/reference/garchFit.md),
  i.e., `.garchFit()`.

- Replaced the error-prone checking for ‘class()’ equality by
  ‘inherits(\*, \<class\>)’.

### Misc

- Exporting practically everything seems “wrong” (according to MM):
  Several `.<some>` functions have *no* documentation and hence should
  either be (renamed and) documented or no longer be exported.

- a `data` argument should never have a default: hence removed from
  [`garchFit()`](https://geobosh.github.io/fGarchDoc/reference/garchFit.md).

## CHANGES in fGarch, VERSION 3042.83.2 (2020-03-07, CRAN team)

CRAN release: 2020-03-07

### Misc

- in ‘dist-norm.Rd’, removed the description of argument `...`, which is
  not in the argument list of any function described there.

## CHANGES in fGarch, VERSION 3042.83.1 (2019-01-31, CRAN team)

CRAN release: 2019-01-31

### Misc

- in ‘NAMESPACE’ and ‘R/methods-plot.R’ renamed functions
  `.plot.garch.1`, …, `.plot.garch.13` to `.plot.garch_1`, …,
  `.plot.garch_13`.

- compressed datasets ‘data/dem2gbp.csv’ and ‘data/sp500dge.csv’ to
  ‘data/dem2gbp.csv.bz2’ ‘data/sp500dge.csv.bz2’, respectively.

## CHANGES in fGarch, VERSION 3042.83 (2017-11-16, svn r…)

CRAN release: 2017-11-16

### Misc

- Startup message removed

- Incorporate fixes by CRAN team (Brian Ripley?)

- Checks and adaptions for R 3.4.2, e.g., ‘DESCRIPTION’, …

## CHANGES in fGarch, VERSION 3010.82.1 (2016-08-14, CRAN team.)

CRAN release: 2016-08-15

### Misc

- in ‘NAMESPACE’, import (selectively) from utils.

- changed a couple of calls to `Matrix()` from package Matrix and
  `fastICA()` from fastICA to the fully qualified forms
  [`Matrix::Matrix()`](https://rdrr.io/pkg/Matrix/man/Matrix.html) and
  [`fastICA::fastICA`](https://rdrr.io/pkg/fastICA/man/fastICA.html).

- removed some flag settings in ‘Makevars’.

- in ‘math.f’, move a `DATA` command out of the body of an `"if"` block
  putting it towards the beginning of the file.

## CHANGES in fGarch, VERSION 3010.82 (2013-04-30, svn r5509) – and earlier

CRAN release: 2013-05-01

### ChangeLog

- Changes up to April 2013, by Yohan Chalabi, Diethelm Wuertz, Pierre
  Chausse and Martin Maechler are all in file ‘ChangeLog’.
