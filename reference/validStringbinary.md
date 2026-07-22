# Validate and correct model string for GA

Validates model parameter strings from genetic algorithms.

## Usage

``` r
validStringbinary(string, search.space = "ivbase", custom_config = NULL)
```

## Arguments

- string:

  Numeric vector representing binary model encoding (0/1).

- search.space:

  Character string specifying which search space to use. Options are
  "ivbase", "oralbase", or "custom". Default is "ivbase".

- custom_config:

  List, configuration for custom search spaces. Required when
  search.space is "custom".

## Value

Numeric vector of validated and corrected parameters (binary encoding).

## Details

The input string is a binary chromosome (0/1). The function:

1.  Decodes the binary chromosome to a categorical parameter vector
    using `decodeBinary`.

2.  Applies model constraints in categorical space by calling
    `validStringcat`.

3.  Encodes the corrected categorical vector back to binary using
    `encodeBinary`.

This design keeps all correction rules in `validStringcat` and makes the
GA version a thin wrapper around the categorical validator.

## See also

[`validStringcat`](https://zhonghuihuang.github.io/nlmixr2auto/reference/validStringcat.md)
for categorical validation used by ACO/TS.
[`decodeBinary`](https://zhonghuihuang.github.io/nlmixr2auto/reference/decodeBinary.md)
and
[`encodeBinary`](https://zhonghuihuang.github.io/nlmixr2auto/reference/encodeBinary.md)
for encoding conversions.

## Author

Zhonghui Huang

## Examples

``` r
# Example 1: ivbase, 1 compartment disables peripheral terms.
# Bits 1-2 encode no.cmpt; here 00 maps to 1.
invalid_iv <- c(0, 0, 1, 1, 0, 1, 0, 0, 0, 1, 0, 1)
validStringbinary(invalid_iv, "ivbase")
#>  [1] 0 1 0 1 0 0 0 0 0 1 0 1

# Example 2: oralbase, mm = 0 forces eta.km to 0.
# Bits 12-13 encode rv for oralbase.
invalid_oral <- c(1, 0, 1, 1, 0, 0, 0, 0, 1, 0, 0, 0, 1)
validStringbinary(invalid_oral, "oralbase")
#>  [1] 1 0 0 1 0 0 0 0 1 0 0 0 1

# Example 3: custom, mcorr is cleared when there are not enough IIV terms.
simple_config <- list(
  route = "bolus",
  params = c("eta.vc", "mcorr", "rv"),
  param_dependencies = list(),
  fixed_params = list(no.cmpt = 1, eta.cl = 1, allometric_scaling = 1)
)
# custom encoding: eta.vc (1 bit), mcorr (1 bit), rv (2 bits)
invalid_custom <- c(0, 1, 1, 1)  # eta.vc=0, mcorr=1, rv=4
validStringbinary(invalid_custom, "custom", custom_config = simple_config)
#> [1] 0 0 1 1
```
