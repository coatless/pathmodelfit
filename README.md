
<!-- README.md is generated from README.Rmd. Please edit that file -->

# pathmodelfit

<!-- badges: start -->

[![R build
status](https://github.com/tmsalab/pathmodelfit/workflows/R-CMD-check/badge.svg)](https://github.com/tmsalab/pathmodelfit/actions)
[![Package-License](http://img.shields.io/badge/license-GPL%20\(%3E=2\)-brightgreen.svg?style=flat)](http://www.gnu.org/licenses/gpl-2.0.html)
<!-- badges: end -->

The goal of `pathmodelfit` is to provide fit indices for the path
components of latent variable Structural Equation Models (SEM).

## Installation

You can install the released version of pathmodelfit from
[CRAN](https://CRAN.R-project.org) with:

``` r
install.packages("pathmodelfit")
```

Or, you can be on the cutting-edge development version on
[GitHub](https://github.com/) using:

``` r
if(!requireNamespace("remotes")) { install.packages("remotes") }
remotes::install_github("tmsalab/pathmodelfit")
```

## Usage

To use `pathmodelfit`, load the package using:

``` r
library("pathmodelfit")
```

From there, load the data, setup the path and obtain a lavaan model.

``` r
# Load example data
data(mediationVC, package = "pathmodelfit")

# Define path model for lavaan
model4 <- "
Ldrrew =~ LdrrewI1 + LdrrewI2 + LdrrewI3
Jobcom =~ JobcomI1 + JobcomI2 + JobcomI3
Jobsat =~ JobsatI1 + JobsatI2 + JobsatI3
Orgcom =~ OrgcomI1 + OrgcomI2 + OrgcomI3
Jobsat ~ Ldrrew + Jobcom
Orgcom ~ Jobsat"

# Fit the pathmodel with lavaan's sem() function
fit <- lavaan::sem(model4, sample.cov = mediationVC, sample.nobs = 232)
```

Then, the fit indices can be estimated using:

``` r
# Compute the fit indices
pathmodelfit_info = pathmodelfit(fit)

# View results
pathmodelfit_info
#>                             Est
#> RMSEA-P                 0.14685
#> RMSEA-P 90% lower bound 0.04543
#> RMSEA-P 90% upper bound 0.21931
#> NSCI-P                  0.95587
#> srmr.s                  0.05526
#> rmsea.s                 0.17376
#> tli.s                   0.88764
#> cfi.s                   0.95506
```

## Authors

Steven Andrew Culpepper and Larry Williams

## Citing the `pathmodelfit` package

To ensure future development of the package, please cite `pathmodelfit`
package if used during an analysis or simulation study. Citation
information for the package may be acquired by using in *R*:

``` r
citation("pathmodelfit")
```

## License

GPL (\>= 2)
