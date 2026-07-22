# Detect the primary move between two model codes

Compares a previous model code with a new one and identifies the primary
intended change. If an `original_neighbor` is provided, this is used to
determine the intended change, ignoring any secondary modifications
introduced by validation.

## Usage

``` r
detect_move(prev_string, new_string, original_neighbor = NULL)
```

## Arguments

- prev_string:

  A named numeric vector: the starting model code.

- new_string:

  A named numeric vector: the validated model code.

- original_neighbor:

  Optional named numeric vector: the original neighbor before
  validation. If provided, this is used to identify the primary change.

## Value

A list with `element`, `from`, and `to` describing the primary change.

## Author

Zhonghui Huang

## Examples

``` r
prev <- c(no.cmpt = 2, eta.vc = 1)
orig <- c(no.cmpt = 3, eta.vc = 1)  # original neighbor
new  <- c(no.cmpt = 3, eta.vc = 0)  # validated neighbor (extra fix)
detect_move(prev, new, original_neighbor = orig)
#> $element
#> [1] "no.cmpt"
#> 
#> $from
#> [1] 2
#> 
#> $to
#> [1] 3
#> 
```
