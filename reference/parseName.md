# Parse model coding vector to model name

Converts an ordinal model-coding vector into a single pharmacokinetic
model name string, using a search space configuration.

## Usage

``` r
parseName(modcode, search.space = NULL, custom_config = NULL)
```

## Arguments

- modcode:

  Numeric vector of model-coding flags/values in the order defined by
  the search space configuration.

- search.space:

  Character string specifying which search space to use. Options are
  "ivbase", "oralbase", or "custom". Default is "ivbase".

- custom_config:

  Optional named list defining a custom parameter structure. If
  provided, the parameter names are taken from the names of this list.
  If NULL, a default parameter structure is used based on the selected
  search space.

## Value

A character string representing the constructed model name.

## Details

The function selects a configuration (either a custom configuration when
search.space is "custom", or the predefined configuration from
spaceConfig(search.space) otherwise). It then decodes modcode with
parseParams() and assembles an underscore-separated model name.

The name is built from these blocks in order: prefix, compartments,
optional absorption, ETA block, elimination, correlation, residual
error, and optional allometric scaling.

Key rules:

- The prefix is taken from config\$prefix when available; otherwise from
  config\$route; otherwise from search.space.

- The absorption block is included when any absorption option is
  present. If abs.type, abs.delay, and abs.bio are all missing/NA, the
  absorption block is included only for oral or mixed routes using
  FO_abs; otherwise it is omitted.

- The ETA block includes all eta.\* terms equal to 1 (NA values are
  ignored), and also forces Vmax when mm equals 1; otherwise it forces
  CL.

- Elimination uses FO_elim when mm is 0 or NA, and MM_elim when mm is 1.
  Correlation uses uncorrelated when mcorr is 0 or NA, and correlated
  when mcorr is 1. Residual error uses add, prop, or combined.

- Allometric scaling is omitted when allometric_scaling is 0 or NA;
  otherwise it appends "asWT", "asBMI", or "asFFM".

## See also

[`spaceConfig()`](https://nlmixr2auto.org/reference/spaceConfig.md),
[`parseParams()`](https://nlmixr2auto.org/reference/parseParams.md)

## Author

Zhonghui Huang

## Examples

``` r
# Example 1: Parse IV base model name
parseName(c(1, 0, 0, 0, 0, 0, 0, 0, 0, 1), "ivbase")
#> [1] "bolus_1cmpt_etaCL_FOelim_uncorrelated_add"

# Example 2: Parse oral base model name
parseName(c(2, 1, 1, 0, 0, 1, 1, 1, 0, 1, 3), "oralbase")
#> [1] "oral_2cmpt_FO_abs_etaCLKMVCQQ2KA_FOelim_correlated_combined"

# Example 3: Parse custom configuration model name
custom_config <- list(
  prefix = "custom",
  route  = "oral",
  params = c("no.cmpt", "eta.cl", "eta.vc", "mm", "mcorr", "rv"),
  param_dependencies = list(),
  fixed_params = list()
)
parseName(c(2, 1, 0, 0, 1, 2), search.space = "custom",
custom_config = custom_config)
#> [1] "custom_2cmpt_FO_abs_etaCL_FOelim_correlated_prop"
```
