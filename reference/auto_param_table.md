# Automatically generate a parameter table with initial estimates

Constructs a parameter table for nlmixr2 model fitting. It supports:

- Direct use of a user-provided parameter table.

- Automatic initialization of parameters from data using
  [`getPPKinits()`](https://rdrr.io/pkg/nlmixr2autoinit/man/getPPKinits.html).

- Fallback to a default parameter table created by
  [`initialize_param_table()`](https://zhonghuihuang.github.io/nlmixr2auto/reference/initialize_param_table.md).

## Usage

``` r
auto_param_table(
  dat = NULL,
  param_table = NULL,
  nlmixr2autoinits = TRUE,
  foldername = NULL,
  filename = "test",
  out.inits = TRUE,
  ...
)
```

## Arguments

- dat:

  A data frame containing observed data (required if
  `nlmixr2autoinits = TRUE`).

- param_table:

  Optional. A user-provided parameter table (if provided, all other
  logic is skipped).

- nlmixr2autoinits:

  Logical. Whether to automatically estimate initial values using
  [`getPPKinits()`](https://rdrr.io/pkg/nlmixr2autoinit/man/getPPKinits.html).
  Default is `TRUE`.

- foldername:

  Character string specifying the folder name for storing
  `nlmixr2autoinits` outputs. If `NULL` (default),
  [`tempdir()`](https://rdrr.io/r/base/tempfile.html) is used for
  temporary storage. If specified, a cache directory is created in the
  current working directory.

- filename:

  Character string specifying the base name for model output files
  generated during evaluation.

- out.inits:

  Logical flag indicating whether the results returned by the automated
  initialization procedure should be saved to an RDS file. When TRUE,
  the output of the initialization step is written to disk for
  reproducibility or debugging purposes.

- ...:

  Additional arguments passed to
  [`getPPKinits()`](https://rdrr.io/pkg/nlmixr2autoinit/man/getPPKinits.html).

## Value

A `data.frame` representing the parameter table with initial estimates,
ready for use in `nlmixr2()`.

## Details

When `nlmixr2autoinits = TRUE`, this function estimates initial values
from data, applies a name mapping to internal model parameters, performs
log transformations where appropriate, and replaces problematic log
values (e.g. log(0) or `NA`) with `log(0.01)` for numerical stability.

## See also

[`getPPKinits`](https://rdrr.io/pkg/nlmixr2autoinit/man/getPPKinits.html),
[`initialize_param_table`](https://zhonghuihuang.github.io/nlmixr2auto/reference/initialize_param_table.md)

## Author

Zhonghui Huang

## Examples

``` r
# \donttest{
auto_param_table(dat = pheno_sd)
#> 
#> 
#> Infometrics                               Value          
#> ----------------------------------------  ---------------
#> Dose Route                                bolus          
#> Dose Type                                 combined_doses 
#> Number of Subjects                        59             
#> Number of Observations                    155            
#> Subjects with First-Dose Interval Data    35             
#> Observations in the First-Dose Interval   35             
#> Subjects with Multiple-Dose Data          56             
#> Observations after Multiple Doses         120            
#> ----------------------------------------  ------
#> Estimating half-life....................
#> Half-life estimation complete: Estimated t1/2 = 16.44 h
#> Evaluating the predictive performance of calculated one-compartment model parameters....................
#> Error in loadNamespace(x): there is no package called ‘progress’
# }
```
