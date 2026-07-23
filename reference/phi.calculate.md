# Update pheromone levels for each decision node

Compute pheromone increments (`delta_phi`) for each node in the ant
colony optimization search tree and update the global pheromone levels
(`phi`) based on the ants' paths in the current round.

## Usage

``` r
phi.calculate(
  r,
  search.space = "ivbase",
  fitness_history = NULL,
  nodeslst.hist = NULL,
  Q = 1,
  alpha = 1,
  rho = 0.5,
  diff_tol = 1,
  phi0 = 2,
  phi_min = 1,
  phi_max = Inf
)
```

## Arguments

- r:

  Integer. Current optimization round.

- search.space:

  Character, one of "ivbase" or "oralbase". Default is "ivbase".

- fitness_history:

  Data frame. History of ants' fitness values and decision variable
  selections across rounds.

- nodeslst.hist:

  Data frame. History of node-level pheromone values across previous
  rounds.

- Q:

  A positive numeric value. Pheromone scaling constant controlling the
  amount of pheromone deposited by high-quality solutions during each
  iteration. Defaults to 1.

- alpha:

  A non-negative numeric value. Exponent controlling the influence of
  pheromone values on the probability of selecting a component during
  solution construction. Defaults to 1.

- rho:

  Numeric in (0, 1). Pheromone evaporation rate. Higher values increase
  evaporation, encouraging exploration. Defaults to 0.5.

- diff_tol:

  Numeric. Tolerance threshold controlling when differences in fitness
  values are treated as meaningful during pheromone updates. Defaults to
  1.

- phi0:

  A non-negative numeric value. Initial pheromone value assigned to all
  nodes at the start of the search. Defaults to 2.

- phi_min:

  A non-negative numeric value. Lower bound for pheromone values,
  preventing premature convergence. Defaults to 1.

- phi_max:

  A non-negative numeric value. Upper bound for pheromone values,
  limiting excessive reinforcement. Defaults to Inf.

## Value

A data frame (node list) with updated `phi` and `delta_phi` for each
node.

## Details

The update proceeds as follows:

- Initialize the node list for the given search space with \\phi = 0\\.

- Subset the ants from the current round in `fitness_history`.

- Compute rank-based weights so better-performing ants contribute more:
  \$\$\Delta \phi \propto 1 / \mathrm{rank}^{\alpha}.\$\$

- Extract the decision columns and attach the computed weights to form a
  working table of ant paths and contributions.

- Map local decision indices to global node numbers using `node.no` and
  `local.edge.no` from the node list.

- For each node, sum contributions from ants that selected the node to
  obtain \\\Delta \phi\\, then update pheromone with evaporation:
  \$\$\phi\_{\mathrm{new}} = (1 - \rho)\\\phi\_{\mathrm{prev}} + \Delta
  \phi.\$\$

- Clamp updated \\\phi\\ to be between `phi_min` and `phi_max`.

## See also

[initNodeList](https://nlmixr2auto.org/reference/initNodeList.md),
[rank_new](https://nlmixr2auto.org/reference/rank_new.md)

## Author

Zhonghui Huang

## Examples

``` r
# Define search space
search.space <- "ivbase"
# Example fitness_history from round 1
fitness_history <- data.frame(
  round   = rep(1, 8),
  mod.no  = 1:8,
  no.cmpt = c(1, 1, 2, 2, 3, 3, 2, 2),
  eta.km  = c(0, 0, 0, 0, 0, 0, 0, 0),
  eta.vc  = c(0, 0, 0, 0, 0, 0, 1, 1),
  eta.vp  = c(0, 0, 0, 0, 0, 0, 0, 1),
  eta.vp2 = c(0, 0, 0, 0, 0, 0, 0, 0),
  eta.q   = c(0, 0, 0, 0, 0, 0, 0, 0),
  eta.q2  = c(0, 0, 0, 0, 0, 0, 0, 0),
  mm      = c(0, 0, 0, 0, 0, 0, 1, 0),
  mcorr   = c(0, 0, 0, 0, 0, 0, 0, 0),
  rv      = c(1, 2, 1, 2, 1, 2, 1, 1),
  fitness = c(1243.874, 1200.762, 31249.876, 31202.200,
              51259.286, 51204.839, 61032.572, 41031.825),
  allrank = c(2, 1, 4, 3, 7, 6, 8, 5)
)

# Example node list history
nodeslst.hist <- initNodeList(
  search.space = search.space,
  phi0 = 2
)

 phi.calculate(
  r = 1,
  search.space = search.space,
  fitness_history = fitness_history,
  nodeslst.hist = nodeslst.hist
)
#>    travel node.no    node.name edge.no local.edge.no   edge.name      phi
#> 1       1       1 compartments       1             1       1Cmpt 2.500000
#> 2       1       1 compartments       2             2       2Cmpt 1.908333
#> 3       1       1 compartments       3             3       3Cmpt 1.309524
#> 4       1       2      eta_vp2       4             0  eta.vp2.no 3.717857
#> 5       1       2      eta_vp2       5             1 eta.vp2.yes 1.000000
#> 6       1       3       eta_q2       6             0   eta.q2.no 3.717857
#> 7       1       3       eta_q2       7             1  eta.q2.yes 1.000000
#> 8       1       4       eta_vp       8             0   eta.vp.no 3.517857
#> 9       1       4       eta_vp       9             1  eta.vp.yes 1.200000
#> 10      1       5        eta_q      10             0    eta.q.no 3.717857
#> 11      1       5        eta_q      11             1   eta.q.yes 1.000000
#> 12      1       6       eta_vc      12             0   eta.vc.no 3.392857
#> 13      1       6       eta_vc      13             1  eta.vc.yes 1.325000
#> 14      1       7           mm      14             0       mm.no 3.592857
#> 15      1       7           mm      15             1      mm.yes 1.125000
#> 16      1       8       eta_km      16             0   eta.km.no 3.717857
#> 17      1       8       eta_km      17             1  eta.km.yes 1.000000
#> 18      1       9        mcorr      18             0    mcorr.no 3.717857
#> 19      1       9        mcorr      19             1   mcorr.yes 1.000000
#> 20      1      10     residual      20             1         add 2.217857
#> 21      1      10     residual      21             2        prop 2.500000
#> 22      1      10     residual      22             3        comb 1.000000
#>    delta_phi     p
#> 1  1.5000000 0.333
#> 2  0.9083333 0.333
#> 3  0.3095238 0.333
#> 4  2.7178571 0.500
#> 5  0.0000000 0.500
#> 6  2.7178571 0.500
#> 7  0.0000000 0.500
#> 8  2.5178571 0.500
#> 9  0.2000000 0.500
#> 10 2.7178571 0.500
#> 11 0.0000000 0.500
#> 12 2.3928571 0.500
#> 13 0.3250000 0.500
#> 14 2.5928571 0.500
#> 15 0.1250000 0.500
#> 16 2.7178571 0.500
#> 17 0.0000000 0.500
#> 18 2.7178571 0.500
#> 19 0.0000000 0.500
#> 20 1.2178571 0.333
#> 21 1.5000000 0.333
#> 22 0.0000000 0.333
```
