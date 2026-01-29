# Package index

## Overview of package fGarch

- [`fGarch-package`](https://geobosh.github.io/fGarchDoc/reference/00fGarch-package.md)
  [`fGarch`](https://geobosh.github.io/fGarchDoc/reference/00fGarch-package.md)
  : Modelling heterskedasticity in financial time series
- [`fGarchData`](https://geobosh.github.io/fGarchDoc/reference/fGarchData.md)
  [`dem2gbp`](https://geobosh.github.io/fGarchDoc/reference/fGarchData.md)
  [`sp500dge`](https://geobosh.github.io/fGarchDoc/reference/fGarchData.md)
  : Time series datasets
- [`garchSim()`](https://geobosh.github.io/fGarchDoc/reference/garchSim.md)
  : Simulate univariate GARCH/APARCH time series

## Fit GARCH-type models

- [`garchFit()`](https://geobosh.github.io/fGarchDoc/reference/garchFit.md)
  [`garchKappa()`](https://geobosh.github.io/fGarchDoc/reference/garchFit.md)
  [`.gogarchFit()`](https://geobosh.github.io/fGarchDoc/reference/garchFit.md)
  : Fit univariate and multivariate GARCH-type models
- [`garchSpec()`](https://geobosh.github.io/fGarchDoc/reference/garchSpec.md)
  : Univariate GARCH/APARCH time series specification
- [`garchFitControl()`](https://geobosh.github.io/fGarchDoc/reference/garchFitControl.md)
  : Control GARCH fitting algorithms

## Classes

- [`fGARCH-class`](https://geobosh.github.io/fGarchDoc/reference/class-fGARCH.md)
  [`show,fGARCH-method`](https://geobosh.github.io/fGarchDoc/reference/class-fGARCH.md)
  [`update,fGARCH-method`](https://geobosh.github.io/fGarchDoc/reference/class-fGARCH.md)
  : Class "fGARCH" - fitted ARMA-GARCH/APARCH models
- [`fGARCHSPEC-class`](https://geobosh.github.io/fGarchDoc/reference/class-fGARCHSPEC.md)
  [`show,fGARCHSPEC-method`](https://geobosh.github.io/fGarchDoc/reference/class-fGARCHSPEC.md)
  [`update,fGARCHSPEC-method`](https://geobosh.github.io/fGarchDoc/reference/class-fGARCHSPEC.md)
  : Class "fGARCHSPEC"

## Exploring and computing on ‘fGARCH’ objects

- [`tsdiag(`*`<fGARCH>`*`)`](https://geobosh.github.io/fGarchDoc/reference/stats-tsdiag.md)
  : Diagnostic plots and statistics for fitted GARCH models
- [`plot(`*`<fGARCH>`*`,`*`<missing>`*`)`](https://geobosh.github.io/fGarchDoc/reference/methods-plot.md)
  : GARCH plot methods
- [`summary-methods`](https://geobosh.github.io/fGarchDoc/reference/methods-summary.md)
  [`summary`](https://geobosh.github.io/fGarchDoc/reference/methods-summary.md)
  [`summary,fGARCH-method`](https://geobosh.github.io/fGarchDoc/reference/methods-summary.md)
  : fGARCH method for the summary function
- [`coef-methods`](https://geobosh.github.io/fGarchDoc/reference/methods-coef.md)
  [`coef`](https://geobosh.github.io/fGarchDoc/reference/methods-coef.md)
  [`coef,fGARCH-method`](https://geobosh.github.io/fGarchDoc/reference/methods-coef.md)
  [`coef,fGARCHSPEC-method`](https://geobosh.github.io/fGarchDoc/reference/methods-coef.md)
  : GARCH coefficients methods
- [`fitted-methods`](https://geobosh.github.io/fGarchDoc/reference/methods-fitted.md)
  [`fitted`](https://geobosh.github.io/fGarchDoc/reference/methods-fitted.md)
  [`fitted,fGARCH-method`](https://geobosh.github.io/fGarchDoc/reference/methods-fitted.md)
  : Extract GARCH model fitted values
- [`formula-methods`](https://geobosh.github.io/fGarchDoc/reference/methods-formula.md)
  [`formula`](https://geobosh.github.io/fGarchDoc/reference/methods-formula.md)
  [`formula,fGARCH-method`](https://geobosh.github.io/fGarchDoc/reference/methods-formula.md)
  : Extract GARCH model formula
- [`predict(`*`<fGARCH>`*`)`](https://geobosh.github.io/fGarchDoc/reference/methods-predict.md)
  : GARCH prediction function
- [`residuals(`*`<fGARCH>`*`)`](https://geobosh.github.io/fGarchDoc/reference/methods-residuals.md)
  : Extract GARCH model residuals
- [`volatility(`*`<fGARCH>`*`)`](https://geobosh.github.io/fGarchDoc/reference/methods-volatility.md)
  : Extract GARCH model volatility
- [`VaR(`*`<fGARCH>`*`)`](https://geobosh.github.io/fGarchDoc/reference/VaR.md)
  [`ES(`*`<fGARCH>`*`)`](https://geobosh.github.io/fGarchDoc/reference/VaR.md)
  : Compute Value-at-Risk (VaR) and expected shortfall (ES)

## Standardized distributions

- [`absMoments()`](https://geobosh.github.io/fGarchDoc/reference/dist-absMoments.md)
  : Absolute moments of GARCH distributions
- [`dstd()`](https://geobosh.github.io/fGarchDoc/reference/dist-std.md)
  [`pstd()`](https://geobosh.github.io/fGarchDoc/reference/dist-std.md)
  [`qstd()`](https://geobosh.github.io/fGarchDoc/reference/dist-std.md)
  [`rstd()`](https://geobosh.github.io/fGarchDoc/reference/dist-std.md)
  : Standardized Student-t distribution
- [`dged()`](https://geobosh.github.io/fGarchDoc/reference/dist-ged.md)
  [`pged()`](https://geobosh.github.io/fGarchDoc/reference/dist-ged.md)
  [`qged()`](https://geobosh.github.io/fGarchDoc/reference/dist-ged.md)
  [`rged()`](https://geobosh.github.io/fGarchDoc/reference/dist-ged.md)
  : Standardized generalized error distribution

## Skewed standardized distributions

- [`dsnorm()`](https://geobosh.github.io/fGarchDoc/reference/dist-snorm.md)
  [`psnorm()`](https://geobosh.github.io/fGarchDoc/reference/dist-snorm.md)
  [`qsnorm()`](https://geobosh.github.io/fGarchDoc/reference/dist-snorm.md)
  [`rsnorm()`](https://geobosh.github.io/fGarchDoc/reference/dist-snorm.md)
  : Skew normal distribution
- [`dsstd()`](https://geobosh.github.io/fGarchDoc/reference/dist-sstd.md)
  [`psstd()`](https://geobosh.github.io/fGarchDoc/reference/dist-sstd.md)
  [`qsstd()`](https://geobosh.github.io/fGarchDoc/reference/dist-sstd.md)
  [`rsstd()`](https://geobosh.github.io/fGarchDoc/reference/dist-sstd.md)
  : Skew Student-t distribution
- [`dsged()`](https://geobosh.github.io/fGarchDoc/reference/dist-sged.md)
  [`psged()`](https://geobosh.github.io/fGarchDoc/reference/dist-sged.md)
  [`qsged()`](https://geobosh.github.io/fGarchDoc/reference/dist-sged.md)
  [`rsged()`](https://geobosh.github.io/fGarchDoc/reference/dist-sged.md)
  : Skew generalized error distribution

## Fit standardized distributions

- [`stdFit()`](https://geobosh.github.io/fGarchDoc/reference/dist-stdFit.md)
  : Student-t distribution parameter estimation
- [`gedFit()`](https://geobosh.github.io/fGarchDoc/reference/dist-gedFit.md)
  : Generalized error distribution parameter estimation
- [`snormFit()`](https://geobosh.github.io/fGarchDoc/reference/dist-snormFit.md)
  : Skew normal distribution parameter estimation
- [`sstdFit()`](https://geobosh.github.io/fGarchDoc/reference/dist-sstdFit.md)
  : Skew Student-t distribution parameter estimation
- [`sgedFit()`](https://geobosh.github.io/fGarchDoc/reference/dist-sgedFit.md)
  : Skew generalized error distribution parameter estimation

## Visualize standardized distributions

- [`stdSlider()`](https://geobosh.github.io/fGarchDoc/reference/dist-Slider.md)
  [`gedSlider()`](https://geobosh.github.io/fGarchDoc/reference/dist-Slider.md)
  [`snormSlider()`](https://geobosh.github.io/fGarchDoc/reference/dist-Slider.md)
  [`sstdSlider()`](https://geobosh.github.io/fGarchDoc/reference/dist-Slider.md)
  [`sgedSlider()`](https://geobosh.github.io/fGarchDoc/reference/dist-Slider.md)
  : Visualise skew normal, (skew) Student-t and (skew) GED distributions

## Internal functions and classes

- [`fUGARCHSPEC-class`](https://geobosh.github.io/fGarchDoc/reference/class-fUGARCHSPEC.md)
  [`.ugarchFit`](https://geobosh.github.io/fGarchDoc/reference/class-fUGARCHSPEC.md)
  [`.ugarchSpec`](https://geobosh.github.io/fGarchDoc/reference/class-fUGARCHSPEC.md)
  : Class 'fUGARCHSPEC'
