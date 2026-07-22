# Apply parameter dependency rules

Applies dependency constraints among structural and statistical flags in
a model-code parameter list to produce a feasible combination.

## Usage

``` r
applyParamDeps(params)
```

## Arguments

- params:

  Named list of model-code parameters. Elements are typically scalar
  categorical values or 0/1 flags. Unknown elements are ignored.

## Value

A named list with corrected parameter values.

## Details

Corrections are applied in the following groups:

- Compartment rules: disable peripheral IIV terms when "no.cmpt" implies
  they are not used.

- Michaelis-Menten rules: enable or disable "eta.vmax", "eta.km", and
  "eta.cl" based on "mm".

- Oral absorption rules: enable or disable oral-related terms based on
  "abs.delay", "abs.type", and "abs.bio".

- Correlation rules: disable "mcorr" when too few IIV terms are present.

- IIV requirement: ensure at least one IIV term is present by enabling a
  default term consistent with "mm".

## Author

Zhonghui Huang

## Examples

``` r
params <- list(
  no.cmpt = 1, mm = 0, mcorr = 1,
  eta.vc = 1, eta.cl = 0, eta.vp = 1, eta.q = 1
)
applyParamDeps(params)
#> $no.cmpt
#> [1] 1
#> 
#> $mm
#> [1] 0
#> 
#> $mcorr
#> [1] 0
#> 
#> $eta.vc
#> [1] 1
#> 
#> $eta.cl
#> [1] 0
#> 
#> $eta.vp
#> [1] 0
#> 
#> $eta.q
#> [1] 0
#> 

params2 <- list(
  no.cmpt = 2, mm = 1,
  eta.vmax = 0, eta.km = 0, eta.cl = 1
)
applyParamDeps(params2)
#> $no.cmpt
#> [1] 2
#> 
#> $mm
#> [1] 1
#> 
#> $eta.vmax
#> [1] 1
#> 
#> $eta.km
#> [1] 0
#> 
#> $eta.cl
#> [1] 0
#> 
```
