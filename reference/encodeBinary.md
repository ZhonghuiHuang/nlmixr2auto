# Encode categorical encoding to binary encoding

Converts a categorical parameter vector into a binary-encoded GA
chromosome.

## Usage

``` r
encodeBinary(categorical_string, search.space = "ivbase", custom_config)
```

## Arguments

- categorical_string:

  Numeric vector of categorical parameter values. Length must match the
  expected layout for the selected `search.space`.

- search.space:

  Character string specifying which search space to use. Options are
  "ivbase", "oralbase", or "custom". Default is "ivbase".

- custom_config:

  Optional named list defining a custom parameter structure. If
  provided, the parameter names are taken from the names of this list.
  If NULL, a default parameter structure is used based on the selected
  search space.

## Value

Numeric vector of bits (0/1).

## Details

This function converts a vector of categorical parameter values into a
0/1 bit string (a GA chromosome). The required input layout and the
encoding rules depend on the selected search space.

**Built-in search spaces: ivbase / oralbase**

- Expected input length:

  - ivbase: 10 categorical values

  - oralbase: 11 categorical values

- Structure: the first value is no.cmpt and the last value is rv. All
  middle values are copied as-is (they are expected to be 0/1 flags).
  Specifically, ivbase copies indices 2..9 and oralbase copies indices
  2..10.

- no.cmpt and rv use the legacy 3-level 2-bit encoding:

  - 1 -\> 01

  - 2 -\> 10

  - 3 -\> 11

  The code 00 is not used in this mapping.

- Output length:

  - ivbase: 12 bits (2 + 8 + 2)

  - oralbase: 13 bits (2 + 9 + 2)

**Custom search space: custom**

For search.space = "custom", the function reads categorical values in
the order given by params. If custom_config\$params is provided and
non-empty, that vector defines the parameter names and order; otherwise,
the default 24-parameter layout is used:


    no.cmpt, abs.type, abs.delay, abs.bio,
    eta.vmax, eta.km, eta.cl, eta.vc, eta.vp, eta.vp2, eta.q, eta.q2,
    eta.ka, eta.tlag, eta.D2, eta.F1, eta.Fr, eta.mtt, eta.n, eta.bio,
    mm, mcorr, rv, allometric_scaling

- Parameters encoded with 2 bits: no.cmpt, abs.type, abs.delay, rv, and
  allometric_scaling.

- All other parameters must be single-bit flags (0 or 1) and are
  appended directly to the chromosome.

**2-bit encoding rules**

- no.cmpt (1..3): 1-\>01, 2-\>10, 3-\>11 (00 unused)

- abs.type (1..4): 1-\>00, 2-\>01, 3-\>10, 4-\>11

- abs.delay (0..2): 0-\>00, 1-\>01, 2-\>10 (11 unused)

- rv (1..4): 1-\>00, 2-\>01, 3-\>10, 4-\>11

- allometric_scaling (0..3): 0-\>00, 1-\>01, 2-\>10, 3-\>11

## See also

[`.twoBitCode`](https://nlmixr2auto.org/reference/dot-twoBitCode.md),
[`decodeBinary`](https://nlmixr2auto.org/reference/decodeBinary.md)

## Author

Zhonghui Huang

## Examples

``` r
# ivbase: 10 categorical -> 12 bits
cat_iv <- c(1, rep(0, 8), 3)
encodeBinary(cat_iv, "ivbase")
#>  [1] 0 1 0 0 0 0 0 0 0 0 1 1

# Custom: 24 categorical -> 29 bits
cat_custom <- c(
  1, 2, 0, 1,
  rep(0, 16),
  0, 1, 3, 1
)
encodeBinary(cat_custom, "custom")
#>  [1] 0 1 0 1 0 0 1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 1 1 0 0 1
```
