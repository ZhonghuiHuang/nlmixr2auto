# Add inter-individual variability to a parameter

Defines a model string for a parameter, optionally adding
inter-individual variability.

## Usage

``` r
add_variability(param_name, eta_flag, param_table, param.type = 1)
```

## Arguments

- param_name:

  Character. The name of the parameter.

- eta_flag:

  Integer. If 1, inter-individual variability is added; otherwise, it is
  not.

- param_table:

  Data frame. A table containing parameter details with columns `Name`,
  `init`, and optionally bounds like `lb` and `ub`.

- param.type:

  Integer. Transformation type: 1=Exponential, 2=Logistic. Defaults to
  1.

## Value

A list containing:

- mod:

  Character. The model string for the parameter.

- eta_init:

  Character. The initialization string for the variability parameter (if
  applicable).

## Author

Zhonghui Huang

## Examples

``` r
param_table <- initialize_param_table()
add_variability("cl", 1, param_table)
#> $mod
#> [1] "cl = exp(lcl+eta.cl)"
#> 
#> $eta_init
#> [1] "eta.cl ~ 0.1"
#> 
```
