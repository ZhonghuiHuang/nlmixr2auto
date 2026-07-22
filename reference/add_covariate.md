# Add a covariate effect to a parameter model

Automates the creation of covariate effects in pharmacometric models by
generating appropriate beta coefficients and modifying model
expressions. Supports both standard allometric scaling rules and custom
covariate effects.

## Usage

``` r
add_covariate(
  param_name,
  covariate_var,
  param_model,
  beta_value = NULL,
  existing_betas = c(),
  use_fix = TRUE
)
```

## Arguments

- param_name:

  Character. Target parameter name (e.g., "cl", "vc").

- covariate_var:

  Character. Covariate variable name (e.g., "WT", "BMI").

- param_model:

  Character. Current parameter model expression (e.g., "cl = exp(tcl)").

- beta_value:

  Numeric. Optional fixed beta value. If NULL, uses built-in rules.

- existing_betas:

  Character vector. Existing beta definitions to append to.

- use_fix:

  Logical. Use [`fix()`](https://rdrr.io/r/utils/fix.html) for beta
  values? Default TRUE.

## Value

List with two elements:

- betas - Updated character vector of beta definitions

- mod - Modified model expression with covariate term

## Details

Automatic beta selection rules:

- Standard covariates ("wt"/"ffm"/"bmi"/"bsa"):

  - 0.75 for clearance parameters (cl/q/q2)

  - 1.0 for volume parameters (vc/vp/vp2)

- Other covariates: Default beta = -0.1 with message

## Author

Zhonghui Huang

## Examples

``` r
# Add weight effect to clearance
 add_covariate( "cl", "WT", "cl = exp(tcl)")
#> $betas
#> [1] "beta.wt.cl <- fix(0.75)"
#> 
#> $mod
#> [1] "cl = exp(tcl + beta.wt.cl*LOGWT)"
#> 

# Custom beta value for BMI effect
add_covariate(
  "vc", "BMI", "vc = exp(tvc)",
  beta_value = -0.2, use_fix = FALSE
)
#> $betas
#> [1] "beta.bmi.vc <- -0.2"
#> 
#> $mod
#> [1] "vc = exp(tvc + beta.bmi.vc*LOGBMI)"
#> 
```
