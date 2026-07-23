# Configure penalty settings for model evaluation

Defines rules governing penalty assignment during model adequacy
evaluation.

## Usage

``` r
penaltyControl(
  penalty.value = 10000,
  step.penalties = list(rse = c(10, 10000), shrinkage = c(10, 10000), bsv = c(10, 10000),
    sigma = list(add = c(10, 10000), prop = c(10, 10000)), correlation = c(10, 10000)),
  bounds = param.bounds(),
  thresholds = list(),
  penalty.terms = c("total")
)
```

## Arguments

- penalty.value:

  Numeric. Constant penalty assigned to binary violations and bound
  constraints.

- step.penalties:

  A named list defining penalty magnitudes used in step-wise procedures.
  Each element must contain a numeric vector of length two representing
  penalty levels for moderate and critical deviations.

- bounds:

  A list specifying lower and upper parameter limits, as returned by
  param.bounds(). The structure can include limits for theta, omega,
  sigma, and correlation terms.

- thresholds:

  A named list describing evaluation rules for RSE and shrinkage. Each
  component must include a field named method, with value binary or
  step, together with the corresponding limit definition:

  - If method = binary: a single cutoff value stored in threshold

  - If method = step: two deviation boundaries stored in step.levels

- penalty.terms:

  Character vector specifying which components are considered when
  penalties are reported. Recognized entries include: rse, shrinkage,
  theta, omega, sigma, correlation, covariance, and total. If total is
  included, penalties are aggregated across all components and any other
  entries are ignored.

## Value

A list containing the full penalty configuration for use in fitness().

## Details

Penalization may be triggered by exceeding predefined parameter bounds
(fixed-effect and variance-covariance elements) or by surpassing
thresholds for relative standard error (RSE) or shrinkage criteria.
Binary and step-wise penalty procedures are supported.

## See also

[`param.bounds()`](https://nlmixr2auto.org/reference/param.bounds.md),
[`fitness()`](https://nlmixr2auto.org/reference/fitness.md).

## Author

Zhonghui Huang

## Examples

``` r
# Default configuration
penaltyControl()
#> $penalty.value
#> [1] 10000
#> 
#> $step.penalties
#> $step.penalties$rse
#> [1]    10 10000
#> 
#> $step.penalties$shrinkage
#> [1]    10 10000
#> 
#> $step.penalties$bsv
#> [1]    10 10000
#> 
#> $step.penalties$sigma
#> $step.penalties$sigma$add
#> [1]    10 10000
#> 
#> $step.penalties$sigma$prop
#> [1]    10 10000
#> 
#> 
#> $step.penalties$correlation
#> [1]    10 10000
#> 
#> 
#> $bounds
#> $bounds$theta
#> $bounds$theta$lower
#> $bounds$theta$lower$ka
#> [1] -Inf
#> 
#> $bounds$theta$lower$vc
#> [1] -Inf
#> 
#> $bounds$theta$lower$cl
#> [1] -Inf
#> 
#> $bounds$theta$lower$vp
#> [1] -Inf
#> 
#> $bounds$theta$lower$vp2
#> [1] -Inf
#> 
#> $bounds$theta$lower$q
#> [1] -Inf
#> 
#> $bounds$theta$lower$q2
#> [1] -Inf
#> 
#> $bounds$theta$lower$tlag
#> [1] -Inf
#> 
#> $bounds$theta$lower$vmax
#> [1] -Inf
#> 
#> $bounds$theta$lower$km
#> [1] -Inf
#> 
#> 
#> $bounds$theta$upper
#> $bounds$theta$upper$ka
#> [1] 1e+09
#> 
#> $bounds$theta$upper$vc
#> [1] 1e+09
#> 
#> $bounds$theta$upper$cl
#> [1] 1e+09
#> 
#> $bounds$theta$upper$vp
#> [1] 1e+09
#> 
#> $bounds$theta$upper$vp2
#> [1] 1e+09
#> 
#> $bounds$theta$upper$q
#> [1] 1e+09
#> 
#> $bounds$theta$upper$q2
#> [1] 1e+09
#> 
#> $bounds$theta$upper$tlag
#> [1] 1e+09
#> 
#> $bounds$theta$upper$vmax
#> [1] 1e+09
#> 
#> $bounds$theta$upper$km
#> [1] 1e+09
#> 
#> 
#> 
#> $bounds$omega
#> $bounds$omega$lower
#> $bounds$omega$lower$ka
#> [1] 10
#> 
#> $bounds$omega$lower$vc
#> [1] 10
#> 
#> $bounds$omega$lower$cl
#> [1] 10
#> 
#> $bounds$omega$lower$vp
#> [1] 10
#> 
#> $bounds$omega$lower$vp2
#> [1] 10
#> 
#> $bounds$omega$lower$q
#> [1] 10
#> 
#> $bounds$omega$lower$q2
#> [1] 10
#> 
#> $bounds$omega$lower$tlag
#> [1] 10
#> 
#> $bounds$omega$lower$vmax
#> [1] 10
#> 
#> $bounds$omega$lower$km
#> [1] 10
#> 
#> 
#> $bounds$omega$upper
#> $bounds$omega$upper$ka
#> [1] Inf
#> 
#> $bounds$omega$upper$vc
#> [1] Inf
#> 
#> $bounds$omega$upper$cl
#> [1] Inf
#> 
#> $bounds$omega$upper$vp
#> [1] Inf
#> 
#> $bounds$omega$upper$vp2
#> [1] Inf
#> 
#> $bounds$omega$upper$q
#> [1] Inf
#> 
#> $bounds$omega$upper$q2
#> [1] Inf
#> 
#> $bounds$omega$upper$tlag
#> [1] Inf
#> 
#> $bounds$omega$upper$vmax
#> [1] Inf
#> 
#> $bounds$omega$upper$km
#> [1] Inf
#> 
#> 
#> 
#> $bounds$sigma
#> $bounds$sigma$add
#> $bounds$sigma$add$lower
#> [1] 0.001
#> 
#> $bounds$sigma$add$upper
#> [1] Inf
#> 
#> 
#> $bounds$sigma$prop
#> $bounds$sigma$prop$lower
#> [1] 0.001
#> 
#> $bounds$sigma$prop$upper
#> [1] Inf
#> 
#> 
#> 
#> $bounds$correlation
#> $bounds$correlation$lower
#> [1] 0.1
#> 
#> $bounds$correlation$upper
#> [1] 0.8
#> 
#> 
#> 
#> $thresholds
#> $thresholds$rse
#> $thresholds$rse$method
#> [1] "step"
#> 
#> $thresholds$rse$threshold
#> [1] 20
#> 
#> $thresholds$rse$step.levels
#> [1] 20 40
#> 
#> 
#> $thresholds$shrinkage
#> $thresholds$shrinkage$method
#> [1] "step"
#> 
#> $thresholds$shrinkage$threshold
#> [1] 30
#> 
#> $thresholds$shrinkage$step.levels
#> [1] 30 50
#> 
#> 
#> $thresholds$bsv
#> $thresholds$bsv$method
#> [1] "step"
#> 
#> $thresholds$bsv$step.levels
#> [1] 10 10
#> 
#> 
#> $thresholds$sigma
#> $thresholds$sigma$add
#> $thresholds$sigma$add$method
#> [1] "step"
#> 
#> $thresholds$sigma$add$step.levels
#> [1] 0.001 0.000
#> 
#> 
#> $thresholds$sigma$prop
#> $thresholds$sigma$prop$method
#> [1] "step"
#> 
#> $thresholds$sigma$prop$step.levels
#> [1] 0.001 0.000
#> 
#> 
#> 
#> $thresholds$correlation
#> $thresholds$correlation$method
#> [1] "step"
#> 
#> $thresholds$correlation$step.levels
#> $thresholds$correlation$step.levels$lower
#> [1] 0.10 0.05
#> 
#> $thresholds$correlation$step.levels$upper
#> [1] 0.80 0.95
#> 
#> 
#> 
#> 
#> $penalty.terms
#> [1] "total"
#> 

# Custom bounds for selected fixed-effect parameters
penaltyControl(bounds = param.bounds(
  theta = list(lower = list(cl = 0.01, vc = 0.01))
))
#> $penalty.value
#> [1] 10000
#> 
#> $step.penalties
#> $step.penalties$rse
#> [1]    10 10000
#> 
#> $step.penalties$shrinkage
#> [1]    10 10000
#> 
#> $step.penalties$bsv
#> [1]    10 10000
#> 
#> $step.penalties$sigma
#> $step.penalties$sigma$add
#> [1]    10 10000
#> 
#> $step.penalties$sigma$prop
#> [1]    10 10000
#> 
#> 
#> $step.penalties$correlation
#> [1]    10 10000
#> 
#> 
#> $bounds
#> $bounds$theta
#> $bounds$theta$lower
#> $bounds$theta$lower$ka
#> [1] -Inf
#> 
#> $bounds$theta$lower$vc
#> [1] 0.01
#> 
#> $bounds$theta$lower$cl
#> [1] 0.01
#> 
#> $bounds$theta$lower$vp
#> [1] -Inf
#> 
#> $bounds$theta$lower$vp2
#> [1] -Inf
#> 
#> $bounds$theta$lower$q
#> [1] -Inf
#> 
#> $bounds$theta$lower$q2
#> [1] -Inf
#> 
#> $bounds$theta$lower$tlag
#> [1] -Inf
#> 
#> $bounds$theta$lower$vmax
#> [1] -Inf
#> 
#> $bounds$theta$lower$km
#> [1] -Inf
#> 
#> 
#> $bounds$theta$upper
#> $bounds$theta$upper$ka
#> [1] 1e+09
#> 
#> $bounds$theta$upper$vc
#> [1] 1e+09
#> 
#> $bounds$theta$upper$cl
#> [1] 1e+09
#> 
#> $bounds$theta$upper$vp
#> [1] 1e+09
#> 
#> $bounds$theta$upper$vp2
#> [1] 1e+09
#> 
#> $bounds$theta$upper$q
#> [1] 1e+09
#> 
#> $bounds$theta$upper$q2
#> [1] 1e+09
#> 
#> $bounds$theta$upper$tlag
#> [1] 1e+09
#> 
#> $bounds$theta$upper$vmax
#> [1] 1e+09
#> 
#> $bounds$theta$upper$km
#> [1] 1e+09
#> 
#> 
#> 
#> $bounds$omega
#> $bounds$omega$lower
#> $bounds$omega$lower$ka
#> [1] 10
#> 
#> $bounds$omega$lower$vc
#> [1] 10
#> 
#> $bounds$omega$lower$cl
#> [1] 10
#> 
#> $bounds$omega$lower$vp
#> [1] 10
#> 
#> $bounds$omega$lower$vp2
#> [1] 10
#> 
#> $bounds$omega$lower$q
#> [1] 10
#> 
#> $bounds$omega$lower$q2
#> [1] 10
#> 
#> $bounds$omega$lower$tlag
#> [1] 10
#> 
#> $bounds$omega$lower$vmax
#> [1] 10
#> 
#> $bounds$omega$lower$km
#> [1] 10
#> 
#> 
#> $bounds$omega$upper
#> $bounds$omega$upper$ka
#> [1] Inf
#> 
#> $bounds$omega$upper$vc
#> [1] Inf
#> 
#> $bounds$omega$upper$cl
#> [1] Inf
#> 
#> $bounds$omega$upper$vp
#> [1] Inf
#> 
#> $bounds$omega$upper$vp2
#> [1] Inf
#> 
#> $bounds$omega$upper$q
#> [1] Inf
#> 
#> $bounds$omega$upper$q2
#> [1] Inf
#> 
#> $bounds$omega$upper$tlag
#> [1] Inf
#> 
#> $bounds$omega$upper$vmax
#> [1] Inf
#> 
#> $bounds$omega$upper$km
#> [1] Inf
#> 
#> 
#> 
#> $bounds$sigma
#> $bounds$sigma$add
#> $bounds$sigma$add$lower
#> [1] 0.001
#> 
#> $bounds$sigma$add$upper
#> [1] Inf
#> 
#> 
#> $bounds$sigma$prop
#> $bounds$sigma$prop$lower
#> [1] 0.001
#> 
#> $bounds$sigma$prop$upper
#> [1] Inf
#> 
#> 
#> 
#> $bounds$correlation
#> $bounds$correlation$lower
#> [1] 0.1
#> 
#> $bounds$correlation$upper
#> [1] 0.8
#> 
#> 
#> 
#> $thresholds
#> $thresholds$rse
#> $thresholds$rse$method
#> [1] "step"
#> 
#> $thresholds$rse$threshold
#> [1] 20
#> 
#> $thresholds$rse$step.levels
#> [1] 20 40
#> 
#> 
#> $thresholds$shrinkage
#> $thresholds$shrinkage$method
#> [1] "step"
#> 
#> $thresholds$shrinkage$threshold
#> [1] 30
#> 
#> $thresholds$shrinkage$step.levels
#> [1] 30 50
#> 
#> 
#> $thresholds$bsv
#> $thresholds$bsv$method
#> [1] "step"
#> 
#> $thresholds$bsv$step.levels
#> [1] 10 10
#> 
#> 
#> $thresholds$sigma
#> $thresholds$sigma$add
#> $thresholds$sigma$add$method
#> [1] "step"
#> 
#> $thresholds$sigma$add$step.levels
#> [1] 0.001 0.000
#> 
#> 
#> $thresholds$sigma$prop
#> $thresholds$sigma$prop$method
#> [1] "step"
#> 
#> $thresholds$sigma$prop$step.levels
#> [1] 0.001 0.000
#> 
#> 
#> 
#> $thresholds$correlation
#> $thresholds$correlation$method
#> [1] "step"
#> 
#> $thresholds$correlation$step.levels
#> $thresholds$correlation$step.levels$lower
#> [1] 0.10 0.05
#> 
#> $thresholds$correlation$step.levels$upper
#> [1] 0.80 0.95
#> 
#> 
#> 
#> 
#> $penalty.terms
#> [1] "total"
#> 

# Binary penalty method for RSE
penaltyControl(thresholds = list(
  rse = list(method = "binary", threshold = 40)
))
#> $penalty.value
#> [1] 10000
#> 
#> $step.penalties
#> $step.penalties$rse
#> [1]    10 10000
#> 
#> $step.penalties$shrinkage
#> [1]    10 10000
#> 
#> $step.penalties$bsv
#> [1]    10 10000
#> 
#> $step.penalties$sigma
#> $step.penalties$sigma$add
#> [1]    10 10000
#> 
#> $step.penalties$sigma$prop
#> [1]    10 10000
#> 
#> 
#> $step.penalties$correlation
#> [1]    10 10000
#> 
#> 
#> $bounds
#> $bounds$theta
#> $bounds$theta$lower
#> $bounds$theta$lower$ka
#> [1] -Inf
#> 
#> $bounds$theta$lower$vc
#> [1] -Inf
#> 
#> $bounds$theta$lower$cl
#> [1] -Inf
#> 
#> $bounds$theta$lower$vp
#> [1] -Inf
#> 
#> $bounds$theta$lower$vp2
#> [1] -Inf
#> 
#> $bounds$theta$lower$q
#> [1] -Inf
#> 
#> $bounds$theta$lower$q2
#> [1] -Inf
#> 
#> $bounds$theta$lower$tlag
#> [1] -Inf
#> 
#> $bounds$theta$lower$vmax
#> [1] -Inf
#> 
#> $bounds$theta$lower$km
#> [1] -Inf
#> 
#> 
#> $bounds$theta$upper
#> $bounds$theta$upper$ka
#> [1] 1e+09
#> 
#> $bounds$theta$upper$vc
#> [1] 1e+09
#> 
#> $bounds$theta$upper$cl
#> [1] 1e+09
#> 
#> $bounds$theta$upper$vp
#> [1] 1e+09
#> 
#> $bounds$theta$upper$vp2
#> [1] 1e+09
#> 
#> $bounds$theta$upper$q
#> [1] 1e+09
#> 
#> $bounds$theta$upper$q2
#> [1] 1e+09
#> 
#> $bounds$theta$upper$tlag
#> [1] 1e+09
#> 
#> $bounds$theta$upper$vmax
#> [1] 1e+09
#> 
#> $bounds$theta$upper$km
#> [1] 1e+09
#> 
#> 
#> 
#> $bounds$omega
#> $bounds$omega$lower
#> $bounds$omega$lower$ka
#> [1] 10
#> 
#> $bounds$omega$lower$vc
#> [1] 10
#> 
#> $bounds$omega$lower$cl
#> [1] 10
#> 
#> $bounds$omega$lower$vp
#> [1] 10
#> 
#> $bounds$omega$lower$vp2
#> [1] 10
#> 
#> $bounds$omega$lower$q
#> [1] 10
#> 
#> $bounds$omega$lower$q2
#> [1] 10
#> 
#> $bounds$omega$lower$tlag
#> [1] 10
#> 
#> $bounds$omega$lower$vmax
#> [1] 10
#> 
#> $bounds$omega$lower$km
#> [1] 10
#> 
#> 
#> $bounds$omega$upper
#> $bounds$omega$upper$ka
#> [1] Inf
#> 
#> $bounds$omega$upper$vc
#> [1] Inf
#> 
#> $bounds$omega$upper$cl
#> [1] Inf
#> 
#> $bounds$omega$upper$vp
#> [1] Inf
#> 
#> $bounds$omega$upper$vp2
#> [1] Inf
#> 
#> $bounds$omega$upper$q
#> [1] Inf
#> 
#> $bounds$omega$upper$q2
#> [1] Inf
#> 
#> $bounds$omega$upper$tlag
#> [1] Inf
#> 
#> $bounds$omega$upper$vmax
#> [1] Inf
#> 
#> $bounds$omega$upper$km
#> [1] Inf
#> 
#> 
#> 
#> $bounds$sigma
#> $bounds$sigma$add
#> $bounds$sigma$add$lower
#> [1] 0.001
#> 
#> $bounds$sigma$add$upper
#> [1] Inf
#> 
#> 
#> $bounds$sigma$prop
#> $bounds$sigma$prop$lower
#> [1] 0.001
#> 
#> $bounds$sigma$prop$upper
#> [1] Inf
#> 
#> 
#> 
#> $bounds$correlation
#> $bounds$correlation$lower
#> [1] 0.1
#> 
#> $bounds$correlation$upper
#> [1] 0.8
#> 
#> 
#> 
#> $thresholds
#> $thresholds$rse
#> $thresholds$rse$method
#> [1] "binary"
#> 
#> $thresholds$rse$threshold
#> [1] 40
#> 
#> $thresholds$rse$step.levels
#> [1] 20 40
#> 
#> 
#> $thresholds$shrinkage
#> $thresholds$shrinkage$method
#> [1] "step"
#> 
#> $thresholds$shrinkage$threshold
#> [1] 30
#> 
#> $thresholds$shrinkage$step.levels
#> [1] 30 50
#> 
#> 
#> $thresholds$bsv
#> $thresholds$bsv$method
#> [1] "step"
#> 
#> $thresholds$bsv$step.levels
#> [1] 10 10
#> 
#> 
#> $thresholds$sigma
#> $thresholds$sigma$add
#> $thresholds$sigma$add$method
#> [1] "step"
#> 
#> $thresholds$sigma$add$step.levels
#> [1] 0.001 0.000
#> 
#> 
#> $thresholds$sigma$prop
#> $thresholds$sigma$prop$method
#> [1] "step"
#> 
#> $thresholds$sigma$prop$step.levels
#> [1] 0.001 0.000
#> 
#> 
#> 
#> $thresholds$correlation
#> $thresholds$correlation$method
#> [1] "step"
#> 
#> $thresholds$correlation$step.levels
#> $thresholds$correlation$step.levels$lower
#> [1] 0.10 0.05
#> 
#> $thresholds$correlation$step.levels$upper
#> [1] 0.80 0.95
#> 
#> 
#> 
#> 
#> $penalty.terms
#> [1] "total"
#> 
```
