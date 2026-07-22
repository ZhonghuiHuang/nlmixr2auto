# Generate initial parameter table for pharmacometric model estimation

Creates a structured parameter table containing initial estimates with
constraints for base parameters, inter-individual variability (ETA),
residual errors (SIGMA), and correlation terms (OMEGA) to initialize
nonlinear mixed-effects model fitting.

## Usage

``` r
initialize_param_table()
```

## Value

A data.frame with 29 columns containing parameter specifications. The
structure includes:

- Name:

  Parameter name (e.g., "lcl", "eta.vc", "cor.eta_cl_vc")

- init:

  Numeric initial value for parameter estimation

- lb:

  Lower bound constraint (use -Inf for unconstrained)

- ub:

  Upper bound constraint (use Inf for unconstrained)

- fixed:

  Integer flag indicating whether parameter should be fixed (1) or
  estimated (0)

- Description:

  Text description of parameter's biological/pharmacometric meaning

## Details

This table includes:

- Base PK parameters (absorption, clearance, volumes, etc.) in log-scale

- Michaelis-Menten kinetics parameters (vmax, km)

- Absorption parameters including zero-order, mixed-order, and transit
  compartment models

- Residual variability components (additive and proportional error)

- Inter-individual variability (ETA) terms with variance parameters

- Correlation parameters between ETA terms in two blocks:

  - Block 1: vmax and km parameters

  - Block 2: clearance, volumes, and inter-compartmental clearance

Parameters are organized with:

- Name: Parameter name following standard nomenclature

- init: Initial estimate for model fitting

- lb/ub: Lower/upper bounds for parameter estimation

- fixed: Flag indicating fixed parameters (1) vs estimated (0)

- Description: Plain-text explanation of parameter meaning

## Author

Zhonghui Huang

## Examples

``` r
# Generate default parameter table
initialize_param_table()
#>               Name init   lb  ub fixed
#> 1              lka 1.00 -Inf Inf     0
#> 2              lcl 1.00 -Inf Inf     0
#> 3         lvc1cmpt 1.00 -Inf Inf     0
#> 4         lvc2cmpt 1.00 -Inf Inf     0
#> 5         lvc3cmpt 1.00 -Inf Inf     0
#> 6         lvp2cmpt 1.00 -Inf Inf     0
#> 7         lvp3cmpt 1.00 -Inf Inf     0
#> 8          lq2cmpt 1.00 -Inf Inf     0
#> 9          lq3cmpt 1.00 -Inf Inf     0
#> 10            lvp2 1.00 -Inf Inf     0
#> 11             lq2 1.00 -Inf Inf     0
#> 12           lvmax 1.00 -Inf Inf     0
#> 13             lkm 1.00 -Inf Inf     0
#> 14             lD2 1.00 -Inf Inf     0
#> 15             lF1 0.01 -Inf Inf     0
#> 16             lFr 0.01 -Inf Inf     0
#> 17           ltlag 1.00 -Inf Inf     0
#> 18            lmtt 1.00 -Inf Inf     0
#> 19              ln 0.01 -Inf Inf     0
#> 20            lbio 0.01 -Inf Inf     0
#> 21       sigma_add 1.00    0 Inf     0
#> 22      sigma_prop 0.10    0   1     0
#> 23          eta.ka 0.10    0   1     0
#> 24          eta.cl 0.10    0   1     0
#> 25          eta.vc 0.10    0   1     0
#> 26          eta.vp 0.10    0   1     0
#> 27           eta.q 0.10    0   1     0
#> 28         eta.vp2 0.10    0   1     0
#> 29          eta.q2 0.10    0   1     0
#> 30        eta.vmax 0.10    0   1     0
#> 31          eta.km 0.10    0   1     0
#> 32        eta.tlag 0.10    0   1     0
#> 33          eta.D2 0.10    0   1     0
#> 34         eta.mtt 0.10    0   1     0
#> 35           eta.n 0.10    0   1     0
#> 36         eta.bio 0.10    0   1     0
#> 37          eta.F1 0.10    0   1     0
#> 38          eta.Fr 0.10    0   1     0
#> 39 cor.eta_vmax_km 0.10    0   1     0
#> 40   cor.eta_cl_vc 0.10    0   1     0
#> 41   cor.eta_cl_vp 0.10    0   1     0
#> 42  cor.eta_cl_vp2 0.10    0   1     0
#> 43    cor.eta_cl_q 0.10    0   1     0
#> 44   cor.eta_cl_q2 0.10    0   1     0
#> 45   cor.eta_vc_vp 0.10    0   1     0
#> 46  cor.eta_vc_vp2 0.10    0   1     0
#> 47    cor.eta_vc_q 0.10    0   1     0
#> 48   cor.eta_vc_q2 0.10    0   1     0
#> 49  cor.eta_vp_vp2 0.10    0   1     0
#> 50    cor.eta_vp_q 0.10    0   1     0
#> 51   cor.eta_vp_q2 0.10    0   1     0
#> 52   cor.eta_vp2_q 0.10    0   1     0
#> 53  cor.eta_vp2_q2 0.10    0   1     0
#> 54    cor.eta_q_q2 0.10    0   1     0
#>                                                                                                      Description
#> 1                                                                            Log of the absorption rate constant
#> 2                                                                                               Log of clearance
#> 3                                                  Log of central volume of distribution for 1-compartment model
#> 4                                                  Log of central volume of distribution for 2-compartment model
#> 5                                                  Log of central volume of distribution for 3-compartment model
#> 6                                                               Log of peripheral volume for 2-compartment model
#> 7                                                               Log of peripheral volume for 3-compartment model
#> 8  Log of intercompartmental clearance between central and first peripheral compartments for 2-compartment model
#> 9  Log of intercompartmental clearance between central and first peripheral compartments for 3-compartment model
#> 10                                                           Log of volume for the second peripheral compartment
#> 11                        Log of intercompartmental clearance between central and second peripheral compartments
#> 12                                                                           Log of the maximum elimination rate
#> 13                                                    Log of the concentration at which the rate is half of Vmax
#> 14                                                                         Log of zero-order absorption duration
#> 15                                   Log of absolute bioavailability, typically used in IV and oral mixed dosing
#> 16                         Log of the fraction absorbed through first-order kinetics in a mixed absorption model
#> 17                                                                      Log of lag time before absorption begins
#> 18                                                                                      Log of mean transit time
#> 19                                                                     Log of the number of transit compartments
#> 20                                                       Log of the bioavailability of transit compartment model
#> 21                                        Additive residual error component, constant across all concentrations.
#> 22                                        Proportional residual error component, scales with drug concentration.
#> 23                              Inter-individual variability inka, modeled with variance as the initial estimate
#> 24                              Inter-individual variability incl, modeled with variance as the initial estimate
#> 25                              Inter-individual variability invc, modeled with variance as the initial estimate
#> 26                              Inter-individual variability invp, modeled with variance as the initial estimate
#> 27                               Inter-individual variability inq, modeled with variance as the initial estimate
#> 28                             Inter-individual variability invp2, modeled with variance as the initial estimate
#> 29                              Inter-individual variability inq2, modeled with variance as the initial estimate
#> 30                            Inter-individual variability invmax, modeled with variance as the initial estimate
#> 31                              Inter-individual variability inkm, modeled with variance as the initial estimate
#> 32                            Inter-individual variability intlag, modeled with variance as the initial estimate
#> 33                              Inter-individual variability inD2, modeled with variance as the initial estimate
#> 34                             Inter-individual variability inmtt, modeled with variance as the initial estimate
#> 35                               Inter-individual variability inn, modeled with variance as the initial estimate
#> 36                             Inter-individual variability inbio, modeled with variance as the initial estimate
#> 37                              Inter-individual variability inF1, modeled with variance as the initial estimate
#> 38                              Inter-individual variability inFr, modeled with variance as the initial estimate
#> 39                                                                       Correlation between eta.vmax and eta.km
#> 40                                                                         Correlation between eta.cl and eta.vc
#> 41                                                                         Correlation between eta.cl and eta.vp
#> 42                                                                        Correlation between eta.cl and eta.vp2
#> 43                                                                          Correlation between eta.cl and eta.q
#> 44                                                                         Correlation between eta.cl and eta.q2
#> 45                                                                         Correlation between eta.vc and eta.vp
#> 46                                                                        Correlation between eta.vc and eta.vp2
#> 47                                                                          Correlation between eta.vc and eta.q
#> 48                                                                         Correlation between eta.vc and eta.q2
#> 49                                                                        Correlation between eta.vp and eta.vp2
#> 50                                                                          Correlation between eta.vp and eta.q
#> 51                                                                         Correlation between eta.vp and eta.q2
#> 52                                                                         Correlation between eta.vp2 and eta.q
#> 53                                                                        Correlation between eta.vp2 and eta.q2
#> 54                                                                          Correlation between eta.q and eta.q2
```
