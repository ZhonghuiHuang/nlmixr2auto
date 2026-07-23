# Get search space configuration

Retrieve the configuration for a specified search space.

## Usage

``` r
spaceConfig(search.space = c("ivbase", "oralbase"))
```

## Arguments

- search.space:

  Character, one of "ivbase" or "oralbase". Default is "ivbase".

## Value

A list with four elements:

- route: Administration route ("bolus", "oral", or NULL).

- params: Character vector of parameter names expected in the string
  vector.

- param_dependencies: Named list of functions that compute dependent
  parameters.

- fixed_params: Named list of fixed parameter values.

## Details

Pre-defined search spaces:

- "ivbase": IV bolus model, 11 parameters, supports 1 to 3 compartments.

- "oralbase": Oral model, 12 parameters (adds eta.ka), supports 1 to 3
  compartments.

For "ivbase" and "oralbase", param_dependencies handle the relationship
between Michaelis-Menten elimination (mm) and the associated variability
parameters (eta.vmax, eta.cl).

## See also

[mod.run](https://nlmixr2auto.org/reference/mod.run.md) for the main
function that uses these configurations.
[parseParams](https://nlmixr2auto.org/reference/parseParams.md) for
parameter parsing using configurations.

## Author

Zhonghui Huang

## Examples

``` r
# Get IV base configuration
config <- spaceConfig("ivbase")
config$params
#>  [1] "no.cmpt" "eta.km"  "eta.vc"  "eta.vp"  "eta.vp2" "eta.q"   "eta.q2" 
#>  [8] "mm"      "mcorr"   "rv"     

# Get oral base configuration
config <- spaceConfig("oralbase")
config$params
#>  [1] "no.cmpt" "eta.km"  "eta.vc"  "eta.vp"  "eta.vp2" "eta.q"   "eta.q2" 
#>  [8] "eta.ka"  "mm"      "mcorr"   "rv"     
```
