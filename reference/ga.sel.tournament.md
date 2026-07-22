# Tournament selection

Select individuals for the next generation using tournament selection.

## Usage

``` r
ga.sel.tournament(data.pop, npop, nbits)
```

## Arguments

- data.pop:

  A data.frame containing the current population. The first nbits
  columns must be the chromosome (typically coded as 0/1). The data
  frame must also contain a column named `rank`, where smaller values
  indicate better individuals (e.g., rank 1 is best).

- npop:

  Integer. Number of individuals to select for the next generation.

- nbits:

  Integer. Number of bits (genes) per chromosome; i.e., the number of
  columns taken from `data.pop` to form the chromosome matrix.

## Value

A matrix of dimension npop x nbits containing the selected chromosomes
for the next generation.

## Author

Zhonghui Huang

## Examples

``` r
data.pop <- data.frame(fitness = stats::runif(10), rank = rank(stats::runif(10)))
population <- matrix(sample(0:1, 100, replace = TRUE), nrow = 10)
ga.sel.tournament(data.pop=cbind(as.data.frame(population), data.pop), npop=10, nbits=10)
#>       V1 V2 V3 V4 V5 V6 V7 V8 V9 V10
#>  [1,]  1  1  0  0  1  1  0  1  1   1
#>  [2,]  0  0  1  0  1  1  0  0  1   1
#>  [3,]  0  0  1  0  1  0  1  0  1   0
#>  [4,]  1  1  0  1  0  1  1  0  1   1
#>  [5,]  1  0  0  1  1  0  0  0  0   1
#>  [6,]  1  0  1  1  1  0  1  1  1   1
#>  [7,]  1  1  0  0  1  1  0  1  1   1
#>  [8,]  0  0  1  0  1  1  0  0  1   1
#>  [9,]  0  0  1  0  1  0  1  0  1   0
#> [10,]  1  0  0  1  0  0  1  0  0   1
```
