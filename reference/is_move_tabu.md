# Check if a move is tabu

Given a move (variable, from-value, to-value) and a tabu list, this
function checks whether the move is currently forbidden by the tabu
list.

## Usage

``` r
is_move_tabu(move, tabu_list, policy = c("attribute", "move"))
```

## Arguments

- move:

  A list as returned by
  [`detect_move`](https://nlmixr2auto.org/reference/detect_move.md),
  containing `element`, `from`, and `to`.

- tabu_list:

  Data frame of tabu elements, with columns: `elements` (variable name),
  `elements.value` (forbidden value), and `tabu.iteration.left`
  (remaining tabu tenure).

- policy:

  Character scalar. Tabu restriction type: `"attribute"` (default) or
  `"move"`.

## Value

Logical scalar: TRUE if the move is tabu, FALSE otherwise.

## Author

Zhonghui Huang

## Examples

``` r
move <- list(element = "no.cmpt", from = 2, to = 3)
tabu_list <- data.frame(
  elements = c("no.cmpt", "eta.vc"),
  elements.value = c(3, 1),
  tabu.iteration.left = c(2, 1)
)
is_move_tabu(move, tabu_list)
#> [1] FALSE
```
