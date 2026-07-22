# Create a base model code for single-start model search algorithms

Constructs a named numeric vector defining the initial structural and
inter-individual variability model configuration used in single-start
automated PK model search algorithms.

## Usage

``` r
base_model(search.space = "ivbase")
```

## Arguments

- search.space:

  Character, one of "ivbase" or "oralbase". Default is "ivbase".

## Value

For search.space = "ivbase": a named integer vector of length 9
containing:

- no.cmpt - Number of compartments

- eta.km - IIV flag for \\K_m\\

- eta.vc - IIV flag for \\V_c\\

- eta.vp - IIV flag for \\V_p\\

- eta.vp2 - IIV flag for \\V\_{p2}\\

- eta.q - IIV flag for \\Q\\

- eta.q2 - IIV flag for \\Q_2\\

- mm - Michaelis–Menten term flag

- mcorr - Correlation flag among ETAs

- rv - Residual error model code

For search.space = "oralbase": a named integer vector of length 11,
including all fields above plus:

- eta.ka - IIV flag for \\k_a\\ (oral absorption rate constant)

## Details

Two search spaces are supported: "ivbase" and "oralbase". A
user-specified initial model code can be provided via the custom_base
argument. The input is validated for numerical type and expected length,
and standardized element names are applied before returning. The
function is currently used in stepwise selection and tabu search
routines, where a single starting model is iteratively updated.

## Author

Zhonghui Huang

## Examples

``` r
base_model("ivbase")
#> no.cmpt  eta.km  eta.vc  eta.vp eta.vp2   eta.q  eta.q2      mm   mcorr      rv 
#>       1       0       0       0       0       0       0       0       0       3 
base_model("oralbase")
#> no.cmpt  eta.km  eta.vc  eta.vp eta.vp2   eta.q  eta.q2  eta.ka      mm   mcorr 
#>       1       0       0       0       0       0       0       0       0       0 
#>      rv 
#>       3 
```
