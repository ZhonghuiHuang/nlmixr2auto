# Create an initial GA population

Generates an initial population for a genetic algorithm (GA). Each
individual is a binary chromosome represented by a numeric vector
containing 0 and 1.

## Usage

``` r
create.pop(npop, nbits)
```

## Arguments

- npop:

  Integer. Number of individuals (chromosomes) in the population.

- nbits:

  Integer. Number of bits in each chromosome.

## Value

A numeric matrix with npop rows and nbits columns containing only 0
and 1. Each row corresponds to one chromosome.

## Details

Bits are sampled independently. Each bit takes the value 0 or 1 with
equal probability.

## Author

Zhonghui Huang

## Examples

``` r
create.pop(npop = 10, nbits = 12)
#>       [,1] [,2] [,3] [,4] [,5] [,6] [,7] [,8] [,9] [,10] [,11] [,12]
#>  [1,]    1    1    0    0    1    1    1    1    0     0     0     1
#>  [2,]    1    0    1    0    1    0    0    1    1     0     0     0
#>  [3,]    0    0    0    1    1    0    1    0    0     1     1     1
#>  [4,]    0    0    1    0    0    0    0    1    1     0     1     1
#>  [5,]    1    1    0    0    1    1    0    0    0     1     1     1
#>  [6,]    1    1    1    1    1    0    1    0    1     1     1     1
#>  [7,]    0    1    0    1    1    0    0    0    0     1     1     1
#>  [8,]    0    0    0    1    0    0    1    0    1     0     0     1
#>  [9,]    0    0    1    1    1    0    1    1    1     1     1     1
#> [10,]    1    1    0    0    0    0    0    0    0     1     0     1
```
