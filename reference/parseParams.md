# Parse string vector to model parameters

Converts a numeric vector of parameter values into a named list of model
parameters based on the search space configuration.

## Usage

``` r
parseParams(string, config)
```

## Arguments

- string:

  Numeric vector containing parameter values in the order specified by
  the search space configuration

- config:

  List object returned by
  [`spaceConfig()`](https://zhonghuihuang.github.io/nlmixr2auto/reference/spaceConfig.md),
  containing parameter definitions and dependencies

## Value

A named list containing:

- All parameters specified in config\$params with their values

- Computed dependent parameters based on param_dependencies

- Fixed parameters from `fixed_params`

- Administration route from config\$route

## Details

This function performs three main operations:

1.  Maps the input vector to named parameters

2.  Computes dependent parameter values using defined functions

3.  Adds fixed parameters and route information

## See also

[`spaceConfig()`](https://zhonghuihuang.github.io/nlmixr2auto/reference/spaceConfig.md),
[`mod.run()`](https://zhonghuihuang.github.io/nlmixr2auto/reference/mod.run.md)

## Author

Zhonghui Huang

## Examples

``` r
# Example 1: Parse IV base model parameters
config_iv <- spaceConfig("ivbase")
parseParams(c(2, 1, 1, 0, 0, 1, 1, 0, 1, 1), config_iv)
#> $no.cmpt
#> [1] 2
#> 
#> $eta.vmax
#> [1] 0
#> 
#> $eta.km
#> [1] 1
#> 
#> $eta.cl
#> [1] 1
#> 
#> $eta.vc
#> [1] 1
#> 
#> $eta.vp
#> [1] 0
#> 
#> $eta.vp2
#> [1] 0
#> 
#> $eta.q
#> [1] 1
#> 
#> $eta.q2
#> [1] 1
#> 
#> $mm
#> [1] 0
#> 
#> $mcorr
#> [1] 1
#> 
#> $rv
#> [1] 1
#> 
#> $route
#> [1] "bolus"
#> 

# Example 2: Parse oral base model parameters
config_oral <- spaceConfig("oralbase")
parseParams(c(2, 1, 1, 0, 0, 1, 1, 1, 0, 1, 1), config_oral)
#> $no.cmpt
#> [1] 2
#> 
#> $eta.vmax
#> [1] 0
#> 
#> $eta.km
#> [1] 1
#> 
#> $eta.cl
#> [1] 1
#> 
#> $eta.vc
#> [1] 1
#> 
#> $eta.vp
#> [1] 0
#> 
#> $eta.vp2
#> [1] 0
#> 
#> $eta.q
#> [1] 1
#> 
#> $eta.q2
#> [1] 1
#> 
#> $eta.ka
#> [1] 1
#> 
#> $mm
#> [1] 0
#> 
#> $mcorr
#> [1] 1
#> 
#> $rv
#> [1] 1
#> 
#> $route
#> [1] "oral"
#> 

# Example 3: Parse custom configuration parameters
custom_config <- list(route = "oral", params = c("no.cmpt", "eta.cl", "eta.vc"),
                      param_dependencies = list(), fixed_params = list(mm = 0))
parseParams(c(1, 1, 1), custom_config)
#> $no.cmpt
#> [1] 1
#> 
#> $eta.cl
#> [1] 1
#> 
#> $eta.vc
#> [1] 1
#> 
#> $mm
#> [1] 0
#> 
#> $route
#> [1] "oral"
#> 
```
