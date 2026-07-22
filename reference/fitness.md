# Evaluate fitness of a population pharmacokinetic model

Evaluates the quality of a fitted model based on parameter bounds and
diagnostic thresholds.

## Usage

``` r
fitness(
  search.space = "ivbase",
  fit = NULL,
  dat = NULL,
  penalty.control = penaltyControl(),
  objf = "BIC"
)
```

## Arguments

- search.space:

  Character, one of "ivbase" or "oralbase". Default is "ivbase".

- fit:

  Data frame. Model summary from tools such as
  [`get.mod.lst()`](https://zhonghuihuang.github.io/nlmixr2auto/reference/get.mod.lst.md),
  with parameter estimates and diagnostics.

- dat:

  A data frame containing pharmacokinetic data in standard nlmixr2
  format, including "ID", "TIME", "EVID", and "DV", and may include
  additional columns.

- penalty.control:

  List created using
  [`penaltyControl()`](https://zhonghuihuang.github.io/nlmixr2auto/reference/penaltyControl.md),
  including:

  penalty.value

  :   Numeric. Default penalty multiplier used in binary violations.

  step.penalties

  :   Numeric vector or list. Penalties applied to step violations
      (mild, severe).

  bounds

  :   List of parameter lower/upper bounds, typically from
      [`param.bounds()`](https://zhonghuihuang.github.io/nlmixr2auto/reference/param.bounds.md).

  thresholds

  :   Named list of diagnostic constraints (e.g., RSE, shrinkage). Each
      contains a method ("binary" or "step") and the corresponding
      threshold or step levels.

  penalty.terms

  :   Character vector of constraint categories to penalize. Valid terms
      include "theta", "rse", "omega", "shrinkage", "sigma",
      "correlation", "covariance", and "total".

- objf:

  Character. Column name in fit used as the base objective function
  (e.g., "AIC", "BIC", "OBJFV").

## Value

A data frame extending fit with the following:

- flag.\* columns: indicators of constraint violations (0 = no
  violation, 1 = mild, 2 = severe).

- count.constraint.\* columns: number of violations per constraint type.

- fitness: penalized objective function value, computed from the
  specified objf plus applicable penalties.

## See also

[`penaltyControl()`](https://zhonghuihuang.github.io/nlmixr2auto/reference/penaltyControl.md),
[`param.bounds()`](https://zhonghuihuang.github.io/nlmixr2auto/reference/param.bounds.md).

## Author

Zhonghui Huang

## Examples

``` r
# \donttest{
# Fit a model (using nlmixr2)
pheno <- function() {
  ini({
    tcl <- log(0.008)
    tv <-  log(0.6)
    eta.cl + eta.v ~ c(1,
                       0.01, 1)
    add.err <- 0.1
  })
  model({
    cl <- exp(tcl + eta.cl)
    v <- exp(tv + eta.v)
    ke <- cl / v
    d/dt(A1) = - ke * A1
    cp = A1 / v
    cp ~ add(add.err)
  })
}
fit <- nlmixr2est::nlmixr2(pheno, pheno_sd, "saem", control = list(print = 0),
              table = list(cwres = TRUE, npde = TRUE))
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
#> rxode2 5.1.4 using 2 threads (see ?getRxThreads)
#>   no cache: create with `rxCreateCache()`
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
#> → loading into symengine environment...
#> → pruning branches (`if`/`else`) of full model...
#> ✔ done
#> → calculate sensitivities
#> → calculate ∂(f)/∂(η)
#> → calculate ∂(R²)/∂(η)
#> → finding duplicate expressions in inner model...
#> → optimizing duplicate expressions in inner model...
#> → finding duplicate expressions in EBE model...
#> → optimizing duplicate expressions in EBE model...
#> → compiling inner model...
#>  
#>  
#> ✔ done
#> → finding duplicate expressions in FD model...
#> → optimizing duplicate expressions in FD model...
#> → compiling EBE model...
#>  
#>  
#> ✔ done
#> → compiling events FD model...
#>  
#>  
#> ✔ done
#>  
#>  
#> ✔ done
#> → compress origData in nlmixr2 object, save 34224
#> → compress parHistData in nlmixr2 object, save 7136
#> → compress phiM in nlmixr2 object, save 1021696
#>  
#>  
#> → loading into symengine environment...
#> → pruning branches (`if`/`else`) of full model...
#> ✔ done
#> → calculate sensitivities
#> → calculate ∂(f)/∂(η)
#> → calculate ∂(R²)/∂(η)
#> → finding duplicate expressions in inner model...
#> → optimizing duplicate expressions in inner model...
#> → finding duplicate expressions in EBE model...
#> → optimizing duplicate expressions in EBE model...
#> → compiling inner model...
#>  
#>  
#> ✔ done
#> → finding duplicate expressions in FD model...
#> → optimizing duplicate expressions in FD model...
#> → compiling EBE model...
#>  
#>  
#> ✔ done
#> → compiling events FD model...
#>  
#>  
#> ✔ done
Store. <- get.mod.lst(fit.s = fit, 1)
 fitness(fit = Store.,dat = pheno_sd)
#>   model.num        current.time      AIC      BIC    OBJFV        ll npar
#> 1         1 2026-07-22 22:05:53 986.1912 1004.452 689.3203 -487.0956    6
#>   model.covMethod model.message model.time.setup model.time.covariance
#> 1          linFim                     0.03599741             0.0150114
#>   model.time.algorithm model.time.optimize model.time.table model.time.compress
#> 1                8.983          4.5399e-05            3.268               0.119
#>   model.time.other thetaka thetacl thetavc thetavp thetavp2 thetaq thetaq2
#> 1               NA      NA      NA      NA      NA       NA     NA      NA
#>   thetavmax thetakm thetaD2 thetaF1 thetaF2 thetatlag thetamtt thetan thetabio
#> 1        NA      NA      NA      NA      NA        NA       NA     NA       NA
#>   rseka rsecl rsevc rsevp rsevp2 rseq rseq2 rsevmax rsekm rseD2 rseF1 rseF2
#> 1    NA    NA    NA    NA     NA   NA    NA      NA    NA    NA    NA    NA
#>   rsetlag rsemtt rsen rsebio bsvka bsvcl bsvvc bsvvp bsvvp2 bsvq bsvq2 bsvvmax
#> 1      NA     NA   NA     NA    NA    NA    NA    NA     NA   NA    NA      NA
#>   bsvkm bsvD2 bsvF1 bsvF2 bsvtlag bsvmtt bsvn bsvbio shrinkka shrinkcl shrinkvc
#> 1    NA    NA    NA    NA      NA     NA   NA     NA       NA       NA       NA
#>   shrinkvp shrinkvp2 shrinkq shrinkq2 shrinkvmax shrinkkm shrinkD2 shrinkF1
#> 1       NA        NA      NA       NA         NA       NA       NA       NA
#>   shrinkF2 shrinktlag shrinkmtt shrinkn shrinkbio CIlowerka CIlowercl CIlowervc
#> 1       NA         NA        NA      NA        NA        NA        NA        NA
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
#>   flag.thetacl flag.thetavc flag.thetavp flag.thetavp2 flag.thetaq flag.thetaq2
#> 1            0            0            0             0           0            0
#>   flag.thetavmax flag.thetakm flag.rsecl flag.rsevc flag.rsevp flag.rsevp2
#> 1              0            0          0          0          0           0
#>   flag.rseq flag.rseq2 flag.rsevmax flag.rsekm flag.bsvvc flag.bsvcl flag.bsvvp
#> 1         0          0            0          0          0          0          0
#>   flag.bsvvp2 flag.bsvq flag.bsvq2 flag.bsvtlag flag.bsvvmax flag.bsvkm
#> 1           0         0          0            0            0          0
#>   flag.add flag.prop flag.shrinkcl flag.shrinkvc flag.shrinkvp flag.shrinkvp2
#> 1        0         0             0             0             0              0
#>   flag.shrinkq flag.shrinkq2 flag.shrinkvmax flag.shrinkkm flag.cor.eta.vc.cl
#> 1            0             0               0             0                  0
#>   flag.cor.eta.vp.cl flag.cor.eta.q.cl flag.cor.eta.vp2.cl flag.cor.eta.q2.cl
#> 1                  0                 0                   0                  0
#>   flag.cor.eta.vp.vc flag.cor.eta.q.vc flag.cor.eta.vp2.vc flag.cor.eta.q2.vc
#> 1                  0                 0                   0                  0
#>   flag.cor.eta.q.vp flag.cor.eta.vp2.vp flag.cor.eta.q2.vp flag.cor.eta.vp2.q
#> 1                 0                   0                  0                  0
#>   flag.cor.eta.q2.q flag.cor.eta.q2.vp2 flag.cor.eta.vmax.km flag.covariance
#> 1                 0                   0                    0               0
#>   count.constraint.theta count.constraint.rse count.constraint.omega
#> 1                      0                    0                      0
#>   count.constraint.shrinkage count.constraint.correlation
#> 1                          0                            0
#>   count.constraint.sigma count.constraint.total  fitness
#> 1                      0                      0 1004.452
# }
```
