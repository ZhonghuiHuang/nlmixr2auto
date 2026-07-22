# Generate omega block Code for nlmixr2 model

Generates the code for the omega block matrix in nlmixr2 syntax,
supporting both independent variance terms and correlated covariance
structures.

## Usage

``` r
omega_block(param_list, mcorr, eta_table)
```

## Arguments

- param_list:

  A character vector of parameter names requiring inter-individual
  variability (IIV) terms.

- mcorr:

  Integer flag indicating covariance structure:

  - `0`: Generate independent variance terms only

  - `1`: Generate full block covariance structure

- eta_table:

  A data frame containing eta initialization values and correlation
  coefficients. Must contain columns:

  - `Name`: Parameter names (format "eta.X" for variances, "cor.eta_X_Y"
    for correlations)

  - `init`: Initialization values for variance/covariance terms

## Value

A character string containing nlmixr2 omega matrix specification code.

- When `mcorr = 0`: Returns individual variance terms in formula syntax

- When `mcorr = 1`: Returns covariance block structure in matrix syntax

## Author

Zhonghui Huang

## Examples

``` r
# Example eta table structure
eta_table <- initialize_param_table()

# Generate independent terms
omega_block(c("eta.cl", "eta.vc"), mcorr = 0, eta_table)
#> [1] "eta.cl ~ 0.1\neta.vc ~ 0.1"

# Generate covariance block
omega_block(c("eta.cl", "eta.vc"), mcorr = 1, eta_table)
#> [1] "eta.cl + eta.vc ~ c(\n  0.1,\n  0.01, 0.1\n)"
```
