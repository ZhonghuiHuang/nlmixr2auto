# Summarize parameter estimates and run information from an nlmixr2 fit

Extracts fixed effects, between-subject variability, residual
variability, estimation precision, confidence intervals, covariance
structure, shrinkage, and key runtime metrics from a fitted model
produced by nlmixr2.

## Usage

``` r
get.mod.lst(fit.s, modi)
```

## Arguments

- fit.s:

  A model object generated using nlmixr2.

- modi:

  A numeric identifier used to label the model results, for example when
  multiple models are evaluated in sequence.

## Value

A data.frame with parameter summaries, model fit criteria (AIC, BIC,
objective function value, log-likelihood, number of estimated
parameters) and computation timings extracted from the fitted object.

## Details

The function checks for the presence of each element before extraction
to ensure robust handling of incomplete estimation or missing covariance
results.

## Author

Zhonghui Huang

## Examples

``` r
# \donttest{
pheno <- function() {
  ini({
    tcl <- log(0.008) # typical value of clearance
    tv <-  log(0.6)   # typical value of volume
    eta.cl + eta.v ~ c(1,
                       0.01, 1) ## cov(eta.cl, eta.v), var(eta.v)
    add.err <- 0.1    # residual variability
  })
  model({
    cl <- exp(tcl + eta.cl) # individual value of clearance
    v <- exp(tv + eta.v)    # individual value of volume
    ke <- cl / v            # elimination rate constant
    d/dt(A1) = - ke * A1    # model differential equation
    cp = A1 / v             # concentration in plasma
    cp ~ add(add.err)       # define error model
  })
}

# Fit the model using nlmixr2
fit <- nlmixr2est::nlmixr2(pheno, pheno_sd, est="saem", nlmixr2est::saemControl(print=0))
#>  
#>  
#>  
#>  
#> ℹ parameter labels from comments are typically ignored in non-interactive mode
#> ℹ Need to run with the source intact to parse comments
#>  
#>  
#> → loading into symengine environment...
#> → pruning branches (`if`/`else`) of saem model...
#> ✔ done
#> → finding duplicate expressions in saem model...
#> ✔ done
#> ℹ calculate uninformed etas
#> ℹ done
#> Calculating covariance matrix
#> → loading into symengine environment...
#> → pruning branches (`if`/`else`) of saem model...
#> ✔ done
#> → finding duplicate expressions in saem predOnly model 0...
#> → finding duplicate expressions in saem predOnly model 1...
#> → finding duplicate expressions in saem predOnly model 2...
#> ✔ done
#>  
#>  
#> → Calculating residuals/tables
#> ✔ done
#> → compress origData in nlmixr2 object, save 34224
#> → compress parHistData in nlmixr2 object, save 7200
#> → compress phiM in nlmixr2 object, save 1021696

# Extract model results
model_results <- get.mod.lst(fit,1)
print(model_results)
#>   model.num        current.time AIC BIC OBJFV ll npar model.covMethod
#> 1         1 2026-07-23 00:01:01  NA  NA    NA NA   NA          linFim
#>   model.message model.time.setup model.time.covariance model.time.algorithm
#> 1                      0.0288852             0.0140033                9.879
#>   model.time.optimize model.time.table model.time.compress model.time.other
#> 1                  NA            0.087               0.114        0.7891115
#>   thetaka thetacl thetavc thetavp thetavp2 thetaq thetaq2 thetavmax thetakm
#> 1      NA      NA      NA      NA       NA     NA      NA        NA      NA
#>   thetaD2 thetaF1 thetaF2 thetatlag thetamtt thetan thetabio rseka rsecl rsevc
#> 1      NA      NA      NA        NA       NA     NA       NA    NA    NA    NA
#>   rsevp rsevp2 rseq rseq2 rsevmax rsekm rseD2 rseF1 rseF2 rsetlag rsemtt rsen
#> 1    NA     NA   NA    NA      NA    NA    NA    NA    NA      NA     NA   NA
#>   rsebio bsvka bsvcl bsvvc bsvvp bsvvp2 bsvq bsvq2 bsvvmax bsvkm bsvD2 bsvF1
#> 1     NA    NA    NA    NA    NA     NA   NA    NA      NA    NA    NA    NA
#>   bsvF2 bsvtlag bsvmtt bsvn bsvbio shrinkka shrinkcl shrinkvc shrinkvp
#> 1    NA      NA     NA   NA     NA       NA       NA       NA       NA
#>   shrinkvp2 shrinkq shrinkq2 shrinkvmax shrinkkm shrinkD2 shrinkF1 shrinkF2
#> 1        NA      NA       NA         NA       NA       NA       NA       NA
#>   shrinktlag shrinkmtt shrinkn shrinkbio CIlowerka CIlowercl CIlowervc
#> 1         NA        NA      NA        NA        NA        NA        NA
#>   CIlowervp CIlowervp2 CIlowerq CIlowerq2 CIlowervmax CIlowerkm CIlowerD2
#> 1        NA         NA       NA        NA          NA        NA        NA
#>   CIlowerF1 CIlowerF2 CIlowertlag CIlowermtt CIlowern CIlowerbio CIupperka
#> 1        NA        NA          NA         NA       NA         NA        NA
#>   CIuppercl CIuppervc CIuppervp CIuppervp2 CIupperq CIupperq2 CIuppervmax
#> 1        NA        NA        NA         NA       NA        NA          NA
#>   CIupperkm CIupperD2 CIupperF1 CIupperF2 CIuppertlag CIuppermtt CIuppern
#> 1        NA        NA        NA        NA          NA         NA       NA
#>   CIupperbio omegaka   omegacl omegavc omegavp omegavp2 omegaq omegaq2
#> 1         NA      NA 0.2376906      NA      NA       NA     NA      NA
#>   omegavmax omegakm omegaD2 omegaF1 omegaF2 omegatlag omegamtt omegan omegabio
#> 1        NA      NA      NA      NA      NA        NA       NA     NA       NA
#>   omega.vc.cl omega.vp.cl omega.q.cl omega.vp2.cl omega.q2.cl omega.vp.vc
#> 1          NA          NA         NA           NA          NA          NA
#>   omega.q.vc omega.vp2.vc omega.q2.vc omega.q.vp omega.vp2.vp omega.q2.vp
#> 1         NA           NA          NA         NA           NA          NA
#>   omega.vp2.q omega.q2.q omega.q2.vp2 omega.vmax.km cor.eta.vc.cl cor.eta.vp.cl
#> 1          NA         NA           NA            NA            NA            NA
#>   cor.eta.q.cl cor.eta.vp2.cl cor.eta.q2.cl cor.eta.vp.vc cor.eta.q.vc
#> 1           NA             NA            NA            NA           NA
#>   cor.eta.vp2.vc cor.eta.q2.vc cor.eta.q.vp cor.eta.vp2.vp cor.eta.q2.vp
#> 1             NA            NA           NA             NA            NA
#>   cor.eta.vp2.q cor.eta.q2.q cor.eta.q2.vp2 cor.eta.vmax.km add prop
#> 1            NA           NA             NA              NA  NA   NA
# }
```
