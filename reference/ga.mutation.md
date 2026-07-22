# Mutation operator for binary genetic algorithms

Mutate a binary population by flipping bits with probability pmut.

## Usage

``` r
ga.mutation(children.cross, pmut)
```

## Arguments

- children.cross:

  Numeric matrix containing the child population. Rows are individuals
  and columns are bits. Values are expected to be 0/1.

- pmut:

  Single numeric value in \\\[0, 1\]\\ giving the per-bit mutation
  probability.

## Value

Numeric matrix containing the mutated population.

## Details

Mutation is applied independently to each bit (gene). For each position,
a Bernoulli trial with success probability pmut determines whether the
bit is flipped (0 becomes 1, 1 becomes 0).

## Author

Zhonghui Huang

## Examples

``` r
children.cross <- matrix(sample(0:1, 120, replace = TRUE), nrow = 10)
ga.mutation(children.cross, pmut = 0.1)
#>       [,1] [,2] [,3] [,4] [,5] [,6] [,7] [,8] [,9] [,10] [,11] [,12]
#>  [1,]    0    1    1    0    0    0    1    1    1     1     0     1
#>  [2,]    1    1    1    0    1    0    0    0    1     0     1     1
#>  [3,]    1    0    0    1    0    0    0    0    0     0     1     1
#>  [4,]    1    1    0    1    1    1    1    0    1     0     1     0
#>  [5,]    1    1    1    1    0    0    1    1    0     0     0     0
#>  [6,]    1    1    1    1    1    0    0    0    1     1     0     1
#>  [7,]    0    0    1    1    1    0    1    0    0     0     1     0
#>  [8,]    0    1    0    0    1    1    0    1    1     1     1     0
#>  [9,]    1    1    1    1    1    1    1    1    0     1     1     1
#> [10,]    1    1    1    1    1    1    0    0    1     1     0     0
```
