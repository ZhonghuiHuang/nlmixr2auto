# Validate and correct model string for ACO/TS

Validates model parameter strings from ACO or tabu search algorithms.

## Usage

``` r
validStringcat(string, search.space = "ivbase", custom_config = NULL)
```

## Arguments

- string:

  Numeric vector representing categorical model encoding.

- search.space:

  Character string specifying which search space to use. Options are
  "ivbase", "oralbase", or "custom". Default is "ivbase".

- custom_config:

  List, configuration for custom search spaces. Required when
  search.space is "custom".

## Value

Numeric vector of validated and corrected parameters (categorical).

## Details

The input string is interpreted using the parameter order defined by the
selected search space configuration (for "custom", this is
custom_config\$params). The function:

1.  Maps the input vector to named parameters via parseParams().

2.  Enforces model constraints via applyParamDeps().

3.  Returns only the parameters that belong to the search space, using
    the same order as space_cfg\$params.

This design ensures the returned vector is compatible with downstream
model generation and with binary encoding wrappers (for example,
validStringbinary()).

## See also

[`validStringbinary`](https://zhonghuihuang.github.io/nlmixr2auto/reference/validStringbinary.md)
for the GA wrapper using binary encoding.
[`parseParams`](https://zhonghuihuang.github.io/nlmixr2auto/reference/parseParams.md)
for mapping vectors to named parameters.
[`applyParamDeps`](https://zhonghuihuang.github.io/nlmixr2auto/reference/applyParamDeps.md)
for constraint enforcement rules.

## Author

Zhonghui Huang

## Examples

``` r
# Example 1: ivbase, 1 compartment disables peripheral terms.
invalid_iv <- c(1, 1, 1, 1, 0, 1, 0, 0, 0, 1)
validStringcat(invalid_iv, "ivbase")
#>  [1] 1 0 1 0 0 0 0 0 0 1

# Example 2: oralbase, mm = 0 forces eta.km to 0.
invalid_oral <- c(2, 1, 1, 0, 0, 0, 0, 1, 0, 0, 1)
validStringcat(invalid_oral, "oralbase")
#>  [1] 2 0 1 0 0 0 0 1 0 0 1

# Example 3: custom, mcorr is cleared when there are not enough IIV terms.
simple_config <- list(
  route = "bolus",
  params = c("eta.vc", "mcorr", "rv"),
  param_dependencies = list(),
  fixed_params = list(no.cmpt = 1, eta.cl = 1, allometric_scaling = 1)
)
invalid_custom <- c(0, 1, 4)
validStringcat(invalid_custom, "custom", custom_config = simple_config)
#> [1] 0 0 4
```
