# Control Parameters for Tabu Search

Creates a list of control settings for the `tabu.operator` function.

## Usage

``` r
tabuControl(tenure = 3, niter = 20, nsize = NULL, policy = "move")
```

## Arguments

- tenure:

  Integer. Number of iterations a move remains tabu.

- niter:

  Integer. Maximum number of search iterations.

- nsize:

  Optional integer. If not NULL, restricts neighborhood sear to a random
  subset of this size (candidate list strategy).

- policy:

  Character. Type of tabu restriction:

  - `"attribute"` — forbid revisiting a variable value .

  - `"move"` — forbid only specific from–to transitions (default).

## Value

A named list containing all tabu control parameters.

## Author

Zhonghui Huang

## Examples

``` r
tabuControl()
#> $tenure
#> [1] 3
#> 
#> $niter
#> [1] 20
#> 
#> $nsize
#> NULL
#> 
#> $policy
#> [1] "move"
#> 
```
