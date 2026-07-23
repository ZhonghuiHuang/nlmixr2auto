# 2-bit code helper

Internal utility used by decodeBinary() and encodeBinary() to convert
between a 2-bit representation and categorical values via lookup tables.

## Usage

``` r
.twoBitCode(
  mode = c("decode", "encode"),
  value,
  bit2 = NULL,
  decode_map = NULL,
  encode_map = NULL,
  param_name = "param"
)
```

## Arguments

- mode:

  Character, either "decode" or "encode".

- value:

  For decode: the first bit (0/1). For encode: the categorical value to
  encode.

- bit2:

  For decode: the second bit (0/1). Ignored for encode.

- decode_map:

  Numeric vector of length 4 used for decoding, in the order
  corresponding to 00, 01, 10, 11. Use NA for illegal codes.

- encode_map:

  Named integer/numeric vector mapping categorical values (as names) to
  integer codes 0..3 (corresponding to 00..11).

- param_name:

  Character, parameter name used in error messages.

## Value

For decode: a single numeric categorical value. For encode: an integer
vector length 2 containing bits c(bit1, bit2).

## Details

The helper supports two modes:

- decode: converts (bit1, bit2) to a categorical value using a length-4
  lookup table decode_map corresponding to 00, 01, 10, 11.

- encode: converts a categorical value to a 2-bit code using a named
  lookup table encode_map mapping values to integer codes 0..3
  (corresponding to 00..11).

## See also

[`decodeBinary`](https://nlmixr2auto.org/reference/decodeBinary.md),
[`encodeBinary`](https://nlmixr2auto.org/reference/encodeBinary.md)

## Author

Zhonghui Huang

## Examples

``` r
# Decode example (00/01 map to level 1).
.twoBitCode("decode", 0, 0, decode_map = c(1, 1, 2, 3))  # 1
#> [1] 1
.twoBitCode("decode", 0, 1, decode_map = c(1, 1, 2, 3))  # 1
#> [1] 1
.twoBitCode("decode", 1, 0, decode_map = c(1, 1, 2, 3))  # 2
#> [1] 2
.twoBitCode("decode", 1, 1, decode_map = c(1, 1, 2, 3))  # 3
#> [1] 3

# Encode example (level 1 emits 01).
encode_map <- stats::setNames(c(1, 2, 3), c(1, 2, 3))
.twoBitCode("encode", 1, encode_map = encode_map)  # c(0, 1)
#> [1] 0 1
.twoBitCode("encode", 2, encode_map = encode_map)  # c(1, 0)
#> [1] 1 0
.twoBitCode("encode", 3, encode_map = encode_map)  # c(1, 1)
#> [1] 1 1

# Decode 4-level example (00..11 map to 1..4).
.twoBitCode("decode", 0, 0, decode_map = c(1, 2, 3, 4))  # 1
#> [1] 1
```
