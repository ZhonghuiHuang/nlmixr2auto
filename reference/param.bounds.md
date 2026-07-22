# Define Parameter Bounds for PK Models

Utility function to generate lower and upper bounds for pharmacokinetic
model parameters, including fixed effects (theta), random effects
variances (omega), residual error (sigma), and correlation constraints.

## Usage

``` r
param.bounds(
  theta = list(lower = NULL, upper = NULL),
  omega = list(lower = NULL, upper = NULL),
  sigma = list(add = list(lower = 0.001, upper = Inf), prop = list(lower = 0.001, upper =
    Inf)),
  correlation = list(lower = 0.1, upper = 0.8)
)
```

## Arguments

- theta:

  A list with optional elements:

  lower

  :   Named list of lower bounds for fixed effects. Defaults to -Inf for
      all parameters.

  upper

  :   Named list of upper bounds for fixed effects. Defaults to 10^9 for
      all parameters.

- omega:

  A list with optional elements:

  lower

  :   Named list of lower bounds for variance terms. Defaults to 10 for
      all parameters.

  upper

  :   Named list of upper bounds for variance terms. Defaults to Inf for
      all parameters.

- sigma:

  A list with two elements (each itself a list of bounds):

  add

  :   Lower and upper bounds for additive error component. Defaults to
      0.001 and Inf.

  prop

  :   Lower and upper bounds for proportional error component. Defaults
      to 0.001 and Inf.

- correlation:

  A list with elements lower and upper giving the bounds for correlation
  terms. Defaults to 0.1 and 0.8.

## Value

A named list with four components:

- theta:

  List of parameter-specific lower and upper bounds for fixed effects.

- omega:

  List of lower and upper bounds for variance terms.

- sigma:

  List with additive (add) and proportional (prop) error bounds.

- correlation:

  List with lower and upper correlation bounds.

## Details

Default theta bounds use -Inf for lower limits and 10^9 for upper limits
to avoid allowing unrealistically large fixed effect estimates while
still providing flexibility during model estimation.

## Author

Zhonghui Huang

## Examples

``` r
# Use all default bounds
 param.bounds()
#> $theta
#> $theta$lower
#> $theta$lower$ka
#> [1] -Inf
#> 
#> $theta$lower$vc
#> [1] -Inf
#> 
#> $theta$lower$cl
#> [1] -Inf
#> 
#> $theta$lower$vp
#> [1] -Inf
#> 
#> $theta$lower$vp2
#> [1] -Inf
#> 
#> $theta$lower$q
#> [1] -Inf
#> 
#> $theta$lower$q2
#> [1] -Inf
#> 
#> $theta$lower$tlag
#> [1] -Inf
#> 
#> $theta$lower$vmax
#> [1] -Inf
#> 
#> $theta$lower$km
#> [1] -Inf
#> 
#> 
#> $theta$upper
#> $theta$upper$ka
#> [1] 1e+09
#> 
#> $theta$upper$vc
#> [1] 1e+09
#> 
#> $theta$upper$cl
#> [1] 1e+09
#> 
#> $theta$upper$vp
#> [1] 1e+09
#> 
#> $theta$upper$vp2
#> [1] 1e+09
#> 
#> $theta$upper$q
#> [1] 1e+09
#> 
#> $theta$upper$q2
#> [1] 1e+09
#> 
#> $theta$upper$tlag
#> [1] 1e+09
#> 
#> $theta$upper$vmax
#> [1] 1e+09
#> 
#> $theta$upper$km
#> [1] 1e+09
#> 
#> 
#> 
#> $omega
#> $omega$lower
#> $omega$lower$ka
#> [1] 10
#> 
#> $omega$lower$vc
#> [1] 10
#> 
#> $omega$lower$cl
#> [1] 10
#> 
#> $omega$lower$vp
#> [1] 10
#> 
#> $omega$lower$vp2
#> [1] 10
#> 
#> $omega$lower$q
#> [1] 10
#> 
#> $omega$lower$q2
#> [1] 10
#> 
#> $omega$lower$tlag
#> [1] 10
#> 
#> $omega$lower$vmax
#> [1] 10
#> 
#> $omega$lower$km
#> [1] 10
#> 
#> 
#> $omega$upper
#> $omega$upper$ka
#> [1] Inf
#> 
#> $omega$upper$vc
#> [1] Inf
#> 
#> $omega$upper$cl
#> [1] Inf
#> 
#> $omega$upper$vp
#> [1] Inf
#> 
#> $omega$upper$vp2
#> [1] Inf
#> 
#> $omega$upper$q
#> [1] Inf
#> 
#> $omega$upper$q2
#> [1] Inf
#> 
#> $omega$upper$tlag
#> [1] Inf
#> 
#> $omega$upper$vmax
#> [1] Inf
#> 
#> $omega$upper$km
#> [1] Inf
#> 
#> 
#> 
#> $sigma
#> $sigma$add
#> $sigma$add$lower
#> [1] 0.001
#> 
#> $sigma$add$upper
#> [1] Inf
#> 
#> 
#> $sigma$prop
#> $sigma$prop$lower
#> [1] 0.001
#> 
#> $sigma$prop$upper
#> [1] Inf
#> 
#> 
#> 
#> $correlation
#> $correlation$lower
#> [1] 0.1
#> 
#> $correlation$upper
#> [1] 0.8
#> 
#> 

# Customize only omega lower bounds
param.bounds(omega = list(lower = list(cl = 5, vc = 2)))
#> $theta
#> $theta$lower
#> $theta$lower$ka
#> [1] -Inf
#> 
#> $theta$lower$vc
#> [1] -Inf
#> 
#> $theta$lower$cl
#> [1] -Inf
#> 
#> $theta$lower$vp
#> [1] -Inf
#> 
#> $theta$lower$vp2
#> [1] -Inf
#> 
#> $theta$lower$q
#> [1] -Inf
#> 
#> $theta$lower$q2
#> [1] -Inf
#> 
#> $theta$lower$tlag
#> [1] -Inf
#> 
#> $theta$lower$vmax
#> [1] -Inf
#> 
#> $theta$lower$km
#> [1] -Inf
#> 
#> 
#> $theta$upper
#> $theta$upper$ka
#> [1] 1e+09
#> 
#> $theta$upper$vc
#> [1] 1e+09
#> 
#> $theta$upper$cl
#> [1] 1e+09
#> 
#> $theta$upper$vp
#> [1] 1e+09
#> 
#> $theta$upper$vp2
#> [1] 1e+09
#> 
#> $theta$upper$q
#> [1] 1e+09
#> 
#> $theta$upper$q2
#> [1] 1e+09
#> 
#> $theta$upper$tlag
#> [1] 1e+09
#> 
#> $theta$upper$vmax
#> [1] 1e+09
#> 
#> $theta$upper$km
#> [1] 1e+09
#> 
#> 
#> 
#> $omega
#> $omega$lower
#> $omega$lower$ka
#> [1] 10
#> 
#> $omega$lower$vc
#> [1] 2
#> 
#> $omega$lower$cl
#> [1] 5
#> 
#> $omega$lower$vp
#> [1] 10
#> 
#> $omega$lower$vp2
#> [1] 10
#> 
#> $omega$lower$q
#> [1] 10
#> 
#> $omega$lower$q2
#> [1] 10
#> 
#> $omega$lower$tlag
#> [1] 10
#> 
#> $omega$lower$vmax
#> [1] 10
#> 
#> $omega$lower$km
#> [1] 10
#> 
#> 
#> $omega$upper
#> $omega$upper$ka
#> [1] Inf
#> 
#> $omega$upper$vc
#> [1] Inf
#> 
#> $omega$upper$cl
#> [1] Inf
#> 
#> $omega$upper$vp
#> [1] Inf
#> 
#> $omega$upper$vp2
#> [1] Inf
#> 
#> $omega$upper$q
#> [1] Inf
#> 
#> $omega$upper$q2
#> [1] Inf
#> 
#> $omega$upper$tlag
#> [1] Inf
#> 
#> $omega$upper$vmax
#> [1] Inf
#> 
#> $omega$upper$km
#> [1] Inf
#> 
#> 
#> 
#> $sigma
#> $sigma$add
#> $sigma$add$lower
#> [1] 0.001
#> 
#> $sigma$add$upper
#> [1] Inf
#> 
#> 
#> $sigma$prop
#> $sigma$prop$lower
#> [1] 0.001
#> 
#> $sigma$prop$upper
#> [1] Inf
#> 
#> 
#> 
#> $correlation
#> $correlation$lower
#> [1] 0.1
#> 
#> $correlation$upper
#> [1] 0.8
#> 
#> 

# Adjust sigma proportional error bounds
param.bounds(
  sigma = list(
    add = list(lower = 0.001, upper = 1),
    prop = list(lower = 0.01, upper = 0.05)
  )
)
#> $theta
#> $theta$lower
#> $theta$lower$ka
#> [1] -Inf
#> 
#> $theta$lower$vc
#> [1] -Inf
#> 
#> $theta$lower$cl
#> [1] -Inf
#> 
#> $theta$lower$vp
#> [1] -Inf
#> 
#> $theta$lower$vp2
#> [1] -Inf
#> 
#> $theta$lower$q
#> [1] -Inf
#> 
#> $theta$lower$q2
#> [1] -Inf
#> 
#> $theta$lower$tlag
#> [1] -Inf
#> 
#> $theta$lower$vmax
#> [1] -Inf
#> 
#> $theta$lower$km
#> [1] -Inf
#> 
#> 
#> $theta$upper
#> $theta$upper$ka
#> [1] 1e+09
#> 
#> $theta$upper$vc
#> [1] 1e+09
#> 
#> $theta$upper$cl
#> [1] 1e+09
#> 
#> $theta$upper$vp
#> [1] 1e+09
#> 
#> $theta$upper$vp2
#> [1] 1e+09
#> 
#> $theta$upper$q
#> [1] 1e+09
#> 
#> $theta$upper$q2
#> [1] 1e+09
#> 
#> $theta$upper$tlag
#> [1] 1e+09
#> 
#> $theta$upper$vmax
#> [1] 1e+09
#> 
#> $theta$upper$km
#> [1] 1e+09
#> 
#> 
#> 
#> $omega
#> $omega$lower
#> $omega$lower$ka
#> [1] 10
#> 
#> $omega$lower$vc
#> [1] 10
#> 
#> $omega$lower$cl
#> [1] 10
#> 
#> $omega$lower$vp
#> [1] 10
#> 
#> $omega$lower$vp2
#> [1] 10
#> 
#> $omega$lower$q
#> [1] 10
#> 
#> $omega$lower$q2
#> [1] 10
#> 
#> $omega$lower$tlag
#> [1] 10
#> 
#> $omega$lower$vmax
#> [1] 10
#> 
#> $omega$lower$km
#> [1] 10
#> 
#> 
#> $omega$upper
#> $omega$upper$ka
#> [1] Inf
#> 
#> $omega$upper$vc
#> [1] Inf
#> 
#> $omega$upper$cl
#> [1] Inf
#> 
#> $omega$upper$vp
#> [1] Inf
#> 
#> $omega$upper$vp2
#> [1] Inf
#> 
#> $omega$upper$q
#> [1] Inf
#> 
#> $omega$upper$q2
#> [1] Inf
#> 
#> $omega$upper$tlag
#> [1] Inf
#> 
#> $omega$upper$vmax
#> [1] Inf
#> 
#> $omega$upper$km
#> [1] Inf
#> 
#> 
#> 
#> $sigma
#> $sigma$add
#> $sigma$add$lower
#> [1] 0.001
#> 
#> $sigma$add$upper
#> [1] 1
#> 
#> 
#> $sigma$prop
#> $sigma$prop$lower
#> [1] 0.01
#> 
#> $sigma$prop$upper
#> [1] 0.05
#> 
#> 
#> 
#> $correlation
#> $correlation$lower
#> [1] 0.1
#> 
#> $correlation$upper
#> [1] 0.8
#> 
#> 
```
