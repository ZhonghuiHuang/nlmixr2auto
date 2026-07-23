# Decode binary encoding to categorical encoding

Converts a binary-encoded GA chromosome (0/1 vector) into a categorical
parameter vector.

## Usage

``` r
decodeBinary(binary_string, search.space = "ivbase", custom_config)
```

## Arguments

- binary_string:

  Numeric vector of bits (0/1). Length must match the expected layout
  for the selected search.space.

- search.space:

  Character string specifying which search space to use. Options are
  "ivbase", "oralbase", or "custom". Default is "ivbase".

- custom_config:

  Optional named list defining a custom parameter structure. If
  provided, the parameter names are taken from the names of this list.
  If NULL, a default parameter structure is used based on the selected
  search space.

## Value

Numeric vector of categorical parameter values.

## Details

Supported search spaces:

- "ivbase": binary string has 12 bits and decodes to 10 values.

- "oralbase": binary string has 13 bits and decodes to 11 values.

- "custom": binary string has 29 bits and decodes to 24 values.

Legacy layout ("ivbase" and "oralbase"):

- The first two bits encode the number of compartments (no.cmpt) as 00
  or 01 for 1, 10 for 2, and 11 for 3.

- The middle parameters are copied directly and preserve values such as
  0, 1, and -1.

- The last two bits encode the residual error model (rv) as 00 or 01 for
  1, 10 for 2, and 11 for 3.

Custom layout ("custom"):

- Multi-level parameters are stored as 2-bit fields (for example,
  no.cmpt, absorption type, absorption delay, residual error model, and
  allometric scaling).

- Binary flags are stored as single bits, including absolute
  bioavailability (abs.bio), the Michaelis-Menten indicator (mm), and
  the correlation indicator (mcorr).

- Inter-individual variability indicators (eta.\*) are stored as 16
  single-bit flags in a fixed order.

For "custom", the categorical output order is:


    no.cmpt, abs.type, abs.delay, abs.bio,
    eta.vmax, eta.km, eta.cl, eta.vc, eta.vp, eta.vp2, eta.q, eta.q2,
    eta.ka, eta.tlag, eta.D2, eta.F1, eta.Fr, eta.mtt, eta.n, eta.bio,
    mm, mcorr, rv, allometric_scaling

## See also

[`.twoBitCode`](https://nlmixr2auto.org/reference/dot-twoBitCode.md),
[`encodeBinary`](https://nlmixr2auto.org/reference/encodeBinary.md)

## Author

Zhonghui Huang

## Examples

``` r
binary_iv <- c(0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 1, 1)
decodeBinary(binary_iv, "ivbase")
#>  [1] 1 0 1 0 0 0 0 0 0 3

binary_oral <- c(0, 1, rep(0, 9), 1, 1)
decodeBinary(binary_oral, "oralbase")
#>  [1] 1 0 0 0 0 0 0 0 0 0 3

binary_custom <- c(
  0, 0, 0, 1, 1, 1, 1, rep(0, 16), 0, 1, 1, 0, 0, 1
)
decodeBinary(binary_custom, "custom")
#>  [1] 1 2 0 1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 1 3 1
```
