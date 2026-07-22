# Crossover operator (one- or two-point) for binary chromosomes

Apply one- or two-point crossover to a selected population of binary
chromosomes.

## Usage

``` r
ga.crossover(sel.population, pcross, npop, nbits)
```

## Arguments

- sel.population:

  Numeric matrix of dimension npop by nbits. Each row is a chromosome
  and is expected to contain binary values (0/1).

- pcross:

  Single numeric value in \\\[0, 1\]\\ giving the probability of
  applying crossover to each parent pair.

- npop:

  Single positive even integer giving the population size.

- nbits:

  Single positive integer giving the chromosome length.

## Value

Numeric matrix containing the children population after crossover.

## Details

Parents are paired sequentially (1 with 2, 3 with 4, etc.). For each
pair, crossover is applied with probability `pcross`; otherwise the
parents are copied unchanged. Crossover points are sampled from
0:`nbits`. If the sampled points do not yield a valid crossover, no
crossover is performed for that pair.

## Author

Zhonghui Huang

## Examples

``` r
sel.population <- matrix(sample(0:1, 100, replace = TRUE), nrow = 10)
ga.crossover(sel.population = sel.population, pcross = 0.7, npop = 10, nbits = 10)
#>       [,1] [,2] [,3] [,4] [,5] [,6] [,7] [,8] [,9] [,10]
#>  [1,]    1    1    1    0    0    1    0    0    1     0
#>  [2,]    0    1    0    1    0    0    1    0    1     1
#>  [3,]    0    1    0    0    1    1    0    1    0     0
#>  [4,]    0    1    0    1    0    0    0    0    1     1
#>  [5,]    0    1    1    0    1    1    0    0    1     1
#>  [6,]    0    1    1    0    0    0    1    1    0     1
#>  [7,]    0    1    1    0    1    1    1    0    1     0
#>  [8,]    1    0    0    0    1    1    0    0    1     1
#>  [9,]    0    0    0    0    1    0    1    0    1     0
#> [10,]    0    0    1    0    1    0    0    0    1     1
```
