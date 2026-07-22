# Create control parameters for the ACO algorithm

Creates a list of control settings for the `aco.operator` function.

## Usage

``` r
acoControl(
  nants = 15,
  niter = 20,
  Q = 1,
  rho = 0.5,
  phi0 = 2,
  phi_min = 1,
  phi_max = Inf,
  alpha = 1,
  elite = 0,
  prob_min = 0.2,
  diff_tol = 1
)
```

## Arguments

- nants:

  Integer. Number of ants (candidate solutions) generated at each
  iteration. Defaults to 15.

- niter:

  Integer. Maximum number of ACO iterations. Defaults to 20.

- Q:

  A positive numeric value. Pheromone scaling constant controlling the
  amount of pheromone deposited by high-quality solutions during each
  iteration. Defaults to 1.

- rho:

  Numeric in (0, 1). Pheromone evaporation rate. Higher values increase
  evaporation, encouraging exploration. Defaults to 0.5.

- phi0:

  A non-negative numeric value. Initial pheromone value assigned to all
  nodes at the start of the search. Defaults to 2.

- phi_min:

  A non-negative numeric value. Lower bound for pheromone values,
  preventing premature convergence. Defaults to 1.

- phi_max:

  A non-negative numeric value. Upper bound for pheromone values,
  limiting excessive reinforcement. Defaults to Inf.

- alpha:

  A non-negative numeric value. Exponent controlling the influence of
  pheromone values on the probability of selecting a component during
  solution construction. Defaults to 1.

- elite:

  Numeric. Elitism rate between 0 and 1. Specifies the proportion of
  elite ants whose solutions are preserved and directly propagated to
  the next iteration. Defaults to 0.

- prob_min:

  Numeric. Minimum probability floor between 0 and 1. Applied during
  solution construction to avoid zero-probability choices. Defaults to
  0.2.

- diff_tol:

  Numeric. Significance difference threshold used for ranking. Values
  within this threshold are considered equal and receive the same rank.
  Default is 1.

## Value

A named list containing all ACO control parameters.

## Author

Zhonghui Huang

## Examples

``` r
acoControl()
#> $nants
#> [1] 15
#> 
#> $niter
#> [1] 20
#> 
#> $Q
#> [1] 1
#> 
#> $rho
#> [1] 0.5
#> 
#> $phi0
#> [1] 2
#> 
#> $phi_min
#> [1] 1
#> 
#> $phi_max
#> [1] Inf
#> 
#> $alpha
#> [1] 1
#> 
#> $elite
#> [1] 0
#> 
#> $prob_min
#> [1] 0.2
#> 
#> $diff_tol
#> [1] 1
#> 
```
