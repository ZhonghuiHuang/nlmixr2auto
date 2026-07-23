# Evaluate residual error model structure

Evaluates alternative residual error model structures by modifying the
residual variability setting in the model code.

## Usage

``` r
step_rv(
  dat,
  start.mod = NULL,
  search.space = "ivbase",
  no.cores = NULL,
  param_table = NULL,
  penalty.control = NULL,
  precomputed_results_file = NULL,
  filename = "test",
  foldername = NULL,
  .modEnv = NULL,
  verbose = TRUE,
  ...
)
```

## Arguments

- dat:

  A data frame containing pharmacokinetic data in standard nlmixr2
  format, including "ID", "TIME", "EVID", and "DV", and may include
  additional columns.

- start.mod:

  A named integer vector specifying the starting model code. If NULL, a
  base model is generated using
  [`base_model()`](https://nlmixr2auto.org/reference/base_model.md).

- search.space:

  Character, one of `ivbase` or `oralbase`. Default is `ivbase`.

- no.cores:

  Integer. Number of CPU cores to use. If NULL, uses
  [`rxode2::getRxThreads()`](https://nlmixr2.github.io/rxode2/reference/getRxThreads.html).

- param_table:

  Optional parameter table used during model estimation.

- penalty.control:

  Optional penalty control object used for reporting penalty terms in
  the results table.

- precomputed_results_file:

  Optional path to a CSV file of previously computed model results used
  for caching.

- filename:

  Optional character string used as a prefix for output files. Defaults
  to "test".

- foldername:

  Character string specifying the name of the folder to be created in
  the current working directory to store intermediate results. If NULL,
  a name is generated automatically.

- .modEnv:

  Optional environment used to store model indices and cached results
  across steps.

- verbose:

  Logical. If TRUE, print progress messages.

- ...:

  Additional arguments passed to the model estimation function.

## Value

A list with the following elements:

- results_table: A data frame summarizing the evaluated residual error
  models and their fit statistics,

- best_code: A named integer vector corresponding to the selected model
  code,

- best_row: A one-row data frame containing the summary of the selected
  model.

## Details

Candidate models are constructed by assigning different residual error
types to the model code. Each candidate differs only in the residual
variability specification, and all other structural and statistical
components are kept unchanged. Model selection is based on comparison of
Fitness values obtained during estimation.

## See also

[`mod.run`](https://nlmixr2auto.org/reference/mod.run.md),
[`base_model`](https://nlmixr2auto.org/reference/base_model.md),
[`penaltyControl`](https://nlmixr2auto.org/reference/penaltyControl.md)

## Author

Zhonghui Huang

## Examples

``` r
# \donttest{
  dat <- pheno_sd
  param_table <- initialize_param_table()
  param_table$init[param_table$Name == "lcl"] <- log(0.008)
  param_table$init[param_table$Name == "lvc"] <- log(0.6)
  penalty.control <- penaltyControl()
  penalty.control$penalty.terms <-
    c("rse","theta", "covariance","shrinkage","omega","correlation","sigma")
  step_rv(
    dat = dat,
    search.space = "ivbase",
    param_table = param_table,
    filename = "step_rv_test",
    penalty.control = penalty.control,
    saem.control = nlmixr2est::saemControl(logLik = TRUE,nBurn=15,nEm=15)
  )
#> [Success] Model file created:
#> /tmp/RtmpzBHrsN/mod1.txt
#> SAEM control (core) = niter=15|15; nBurn=15; nEm=15; seed=99; print=1
#> [Success] Model file created:
#> /tmp/RtmpzBHrsN/mod2.txt
#> [Success] Model file created:
#> /tmp/RtmpzBHrsN/mod3.txt
#> $results_table
#>                   Step
#> 1 Residual error types
#> 2 Residual error types
#> 3 Residual error types
#>                                                  Penalty.terms
#> 1 rse, theta, covariance, shrinkage, omega, correlation, sigma
#> 2 rse, theta, covariance, shrinkage, omega, correlation, sigma
#> 3 rse, theta, covariance, shrinkage, omega, correlation, sigma
#>                                       Model.name          Model.code  Fitness
#> 1      bolus_1cmpt_etaCL_FOelim_uncorrelated_add 1,0,0,0,0,0,0,0,0,1 3068.941
#> 2     bolus_1cmpt_etaCL_FOelim_uncorrelated_prop 1,0,0,0,0,0,0,0,0,2 1934.261
#> 3 bolus_1cmpt_etaCL_FOelim_uncorrelated_combined 1,0,0,0,0,0,0,0,0,3 1330.987
#>        AIC      BIC      OFV
#> 1 3056.767 3068.941 2763.896
#> 2 1922.087 1934.261 1629.216
#> 3 1305.770 1320.987 1010.899
#> 
#> $best_code
#> no.cmpt  eta.km  eta.vc  eta.vp eta.vp2   eta.q  eta.q2      mm   mcorr      rv 
#>       1       0       0       0       0       0       0       0       0       3 
#> 
#> $best_row
#>                   Step
#> 3 Residual error types
#>                                                  Penalty.terms
#> 3 rse, theta, covariance, shrinkage, omega, correlation, sigma
#>                                       Model.name          Model.code  Fitness
#> 3 bolus_1cmpt_etaCL_FOelim_uncorrelated_combined 1,0,0,0,0,0,0,0,0,3 1330.987
#>       AIC      BIC      OFV
#> 3 1305.77 1320.987 1010.899
#> 
# }
```
