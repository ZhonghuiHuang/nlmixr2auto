# Ranking with significance difference threshold

Performs a custom ranking of a numeric vector,and ajusts the ranks of
values that differ by less than a specified threshold, ensuring they
receive the same rank.

## Usage

``` r
rank_new(x1, diff_tol)
```

## Arguments

- x1:

  A numeric vector to be ranked.

- diff_tol:

  A numeric value specifying the significance difference threshold.
  Values within this threshold are considered equal and receive the same
  rank.

## Value

A numeric vector representing the adjusted ranks of the input values.

## Author

Zhonghui Huang

## Examples

``` r
x1 <- c(10, 20, 20.5, 30)
diff_tol <- 1
ranked_list <- rank_new(x1, diff_tol)
print(ranked_list)
#> [1] 1 2 2 4
```
