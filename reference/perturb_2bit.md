# Apply 2-bit perturbation to escape local optimum

Randomly flips two parameters ("2-bit change") in the current model
string to generate a perturbed candidate.

## Usage

``` r
perturb_2bit(prev_string, search.space, max.try = 1000)
```

## Arguments

- prev_string:

  A named numeric vector representing the current model.

- search.space:

  Character, one of "ivbase" or "oralbase". Default is "ivbase".

- max.try:

  Maximum number of attempts to generate a valid perturbed model.

## Value

A `list` with two named numeric vectors:

- original_neighbor:

  raw 2-bit flip (may be invalid)

- validated_neighbor:

  validated and usable model code

## Details

The function returns both:

- `original_neighbor`: the raw 2-bit flip before validation

- `validated_neighbor`: the corrected version after validation

This allows downstream functions (e.g.
[`detect_move()`](https://nlmixr2auto.org/reference/detect_move.md)) to
identify which parameters were intentionally changed (primary moves),
while still using a valid model code for evaluation.

## Author

Zhonghui Huang

## Examples

``` r
prev <- c(no.cmpt = 2, eta.km = 0, eta.vc = 1,
          eta.vp = 0, eta.vp2 = 0, eta.q = 1,
          eta.q2 = 0, mm = 0, mcorr = 1, rv = 2)
perturb <- perturb_2bit(prev, search.space = "ivbase")
perturb$original_neighbor   # original 2-bit flip
#> no.cmpt  eta.km  eta.vc  eta.vp eta.vp2   eta.q  eta.q2      mm   mcorr      rv 
#>       3       0       1       0       0       1       1       0       1       2 
perturb$validated_neighbor  # validated model
#> no.cmpt  eta.km  eta.vc  eta.vp eta.vp2   eta.q  eta.q2      mm   mcorr      rv 
#>       3       0       1       0       0       1       1       0       1       2 
```
