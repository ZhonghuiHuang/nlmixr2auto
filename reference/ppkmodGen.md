# Generate a Pharmacokinetic (PK) Model for nlmixr2

Constructs a PK model based on specified parameters, absorption
characteristics, variability components, and residual error models. The
model is generated as a text file compatible with nlmixr syntax. The
function handles various absorption types, multi-compartment models,
Michaelis-Menten kinetics, and different residual variability
structures.

## Usage

``` r
ppkmodGen(
  modi = 1,
  route = "bolus",
  no.cmpt = 1,
  abs.bio = 0,
  abs.type = 1,
  abs.delay = 0,
  eta.ka = 0,
  eta.cl = 0,
  eta.vc = 0,
  eta.vp = 0,
  eta.vp2 = 0,
  eta.q = 0,
  eta.q2 = 0,
  mm = 0,
  eta.vmax = 0,
  eta.km = 0,
  eta.tlag = 0,
  eta.n = 0,
  eta.mtt = 0,
  eta.bio = 0,
  eta.D2 = 0,
  eta.F1 = 0,
  eta.Fr = 0,
  mcorr = 0,
  rv = 1,
  allometric_scaling = 0,
  param_table = NULL,
  return.func = FALSE,
  out.dir = NULL,
  verbose = TRUE
)
```

## Arguments

- modi:

  Model identification number (default: 1). Used for generating unique
  model filenames.

- route:

  Administration route. Valid options: "bolus", "oral", "mixed_iv_oral"
  (default: "bolus").

- no.cmpt:

  Number of compartments in the model (1, 2, or 3) (default: 1).

- abs.bio:

  Bioavailability flag (0 = no bioavailability, 1 = with
  bioavailability) (default: 0).

- abs.type:

  Absorption type (1 = first-order, 2 = zero-order, 3 = sequential
  first-order and zero-order absorption, 4 = dual first-order and
  zero-order absorption) (default: 1).

- abs.delay:

  Absorption delay type (0 = none, 1 = lag time, 2 = transit
  compartments) (default: 0).

- eta.ka:

  Variability flag for absorption rate (ka) (0 = no variability, 1 =
  include variability).

- eta.cl:

  Variability flag for clearance (CL) (0 = no variability, 1 = include
  variability).

- eta.vc:

  Variability flag for central volume (Vc) (0 = no variability, 1 =
  include variability).

- eta.vp:

  Variability flag for peripheral volume (Vp) in multi-compartment
  models.

- eta.vp2:

  Variability flag for second peripheral volume (Vp2) in 3-compartment
  models.

- eta.q:

  Variability flag for intercompartmental clearance (Q) in
  multi-compartment models.

- eta.q2:

  Variability flag for second intercompartmental clearance (Q2) in
  3-compartment models.

- mm:

  Michaelis-Menten kinetics flag (0 = linear kinetics, 1 =
  Michaelis-Menten kinetics).

- eta.vmax:

  Variability flag for Vmax when using Michaelis-Menten kinetics.

- eta.km:

  Variability flag for Km when using Michaelis-Menten kinetics.

- eta.tlag:

  Variability flag for lag time (tlag) when abs.delay=1.

- eta.n:

  Variability flag for number of transit compartments when abs.delay=2.

- eta.mtt:

  Variability flag for mean transit time when abs.delay=2.

- eta.bio:

  Variability flag for bioavailability when abs.delay=2.

- eta.D2:

  Variability flag for zero-order duration (D2) when abs.type=2 or 3.

- eta.F1:

  Variability flag for bioavailability fraction (F1) when abs.bio=1.

- eta.Fr:

  Variability flag for absorption fraction (Fr) when abs.type=4.

- mcorr:

  Correlation flag for omega blocks (0 = no correlation, 1 = include
  correlations).

- rv:

  Residual variability type (1 = additive, 2 = proportional, 3 =
  combined, 4 = log-normal).

- allometric_scaling:

  Allometric scaling type (0 = none, 1 = weight, 2 = BMI, 3 = FFM).

- param_table:

  Data frame containing parameter initial values and variability
  components. Should contain columns: Name (parameter name), init
  (initial value), eta (TRUE/FALSE for variability inclusion), cov
  (covariate relationships).

- return.func:

  Logical, whether to return a compiled function (default `FALSE`
  returns model code as text).

- out.dir:

  Directory where model files and results are written. Defaults to the
  current working directory when not provided.

- verbose:

  Logical; if `TRUE`, progress messages are printed.

## Value

Generates a text file ('modX.txt' where X = modi) containing the
nlmixr-compatible model code. The file is written to the current working
directory. No explicit return value. If `return.func = TRUE`, returns a
compiled model function object.

## Author

Zhonghui Huang

## Examples

``` r
withr::with_dir(tempdir(), {
#' # Create a 1-compartment oral model with first-order absorption
 ppkmodGen( no.cmpt = 1, abs.type = 1,return.func = TRUE,param_table = initialize_param_table())
})
#> [Success] Model file created:
#> /tmp/RtmpzBHrsN/mod1.txt
#> function () 
#> {
#>     ini({
#>         lcl <- 1
#>         lvc <- 1
#>         sigma_add <- 1
#>     })
#>     model({
#>         cl = exp(lcl)
#>         vc = exp(lvc)
#>         d/dt(central) <- -cl/vc * central
#>         cp <- central/vc
#>         cp ~ add(sigma_add)
#>     })
#> }
#> <environment: 0x56155e369848>
```
