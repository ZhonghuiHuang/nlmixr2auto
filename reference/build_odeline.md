# Build ODE model lines for pharmacokinetic modeling

Constructs a system of ordinary differential equations (ODEs) for
pharmacokinetic modeling with various configurations including different
absorption models, compartmental structures, and elimination kinetics.

## Usage

``` r
build_odeline(
  mm = 0,
  no.cmpt = 1,
  route = "bolus",
  abs.bio = 0,
  abs.type = 1,
  abs.delay = 0
)
```

## Arguments

- mm:

  Michaelis-Menten elimination flag. 0 = linear elimination (default), 1
  = Michaelis-Menten elimination.

- no.cmpt:

  Number of compartments. Supported values: 1 (central only), 2
  (central + peripheral), or 3 (central + 2 peripheral).

- route:

  Administration route. Options: "bolus" (IV), "oral", or
  "mixed_iv_oral".

- abs.bio:

  Bioavailability estimation flag. 0 = no bioavailability estimation
  (default), 1 = include bioavailability parameter (F1).

- abs.type:

  Absorption type for oral route:

  - 1 = First-order absorption (default)

  - 2 = Zero-order absorption

  - 3 = Sequential zero-first order absorption

  - 4 = Dual zero-first order absorption

- abs.delay:

  Absorption delay type:

  - 0 = No delay (default)

  - 1 = Lag time (tlag)

  - 2 = Transit compartment model

## Value

A character vector containing ODE equations for the specified
configuration. Includes differential equations for drug compartments,
absorption models, and derived parameters.

## Details

Parameter Constraints: The function includes error checking for
incompatible parameter combinations:

- abs.bio=1 cannot be used with abs.type=4 or abs.delay=3

- Dual absorption (abs.type=4) not supported for mixed routes

## Author

Zhonghui Huang

## Examples

``` r
# Two-compartment model with first-order absorption
build_odeline(no.cmpt = 2, route = "oral")
#> [1] "d/dt(depot) <- - ka * depot"                                                         
#> [2] "d/dt(central) <- - cl / vc * central - q / vc * central + q / vp * peri + ka * depot"
#> [3] "d/dt(peri) <- q / vc * central - q / vp * peri"                                      
#> [4] "cp <- central/vc"                                                                    

# One-compartment IV model with Michaelis-Menten elimination
build_odeline(mm = 1, route = "bolus")
#> [1] "d/dt(central) <- - (vmax / (km + central / vc)) / vc * central"
#> [2] "cp <- central/vc"                                              
```
