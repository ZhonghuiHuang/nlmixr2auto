# Control parameters for genetic algorithm

Creates a list of control settings for the
[`ga.operator()`](https://zhonghuihuang.github.io/nlmixr2auto/reference/ga.operator.md)
function.

## Usage

``` r
gaControl(
  npop = 20,
  niter = 20,
  pcross = 0.7,
  pmut = 0.1,
  diff_tol = 1,
  nls = 3
)
```

## Arguments

- npop:

  Integer. The number of individuals (chromosomes) in the population for
  each generation.

- niter:

  Integer. The maximum number of generations to run the GA.

- pcross:

  Numeric in \\\[0, 1\]\\. Probability of performing crossover between
  two selected parents.

- pmut:

  Numeric in \\\[0, 1\]\\. Probability of mutating each bit in a
  chromosome.

- diff_tol:

  A numeric value specifying the significance difference threshold.
  Values within this threshold are considered equal and receive the same
  rank. Default is 1.

- nls:

  Integer. Frequency (in generations) of running local exhaustive search
  around the best current model.

## Value

A named list containing all GA control parameters.

## See also

[`ga.operator`](https://zhonghuihuang.github.io/nlmixr2auto/reference/ga.operator.md),
[`rank_new`](https://zhonghuihuang.github.io/nlmixr2auto/reference/rank_new.md),
[`runlocal`](https://zhonghuihuang.github.io/nlmixr2auto/reference/runlocal.md)

## Author

Zhonghui Huang

## Examples

``` r
# Default settings
gaControl()
#> $npop
#> [1] 20
#> 
#> $niter
#> [1] 20
#> 
#> $pcross
#> [1] 0.7
#> 
#> $pmut
#> [1] 0.1
#> 
#> $diff_tol
#> [1] 1
#> 
#> $nls
#> [1] 3
#> 
```
