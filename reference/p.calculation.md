# Calculate selection probabilities for each node

Calculates the probability of selecting each node in an ant colony
optimization search, based on pheromone levels \\\phi\\.

## Usage

``` r
p.calculation(nodeslst, prob_min = NULL)
```

## Arguments

- nodeslst:

  A data frame of nodes, including columns:

  phi

  :   Current pheromone level \\\phi\\

  node.no

  :   Group ID for the decision step

  p

  :   Probability of selection (to be calculated)

- prob_min:

  Numeric scalar. Minimum probability each node is allowed to have
  within its decision group. Set to NULL or 0 to disable smoothing.

## Value

The updated node list with recalculated p values.

## Details

Within each decision group \\G\\, selection probabilities are computed
from pheromone levels \\\phi\\ as: \$\$p_i = \frac{\phi_i}{\sum\_{j \in
G} \phi_j}\$\$

If prob_min is enabled and any calculated probability falls below this
value, the algorithm:

1.  Sets all probabilities below prob_min to prob_min.

2.  Redistributes the remaining probability mass proportionally among
    the other nodes in the same group.

This acts as a probability smoothing mechanism, preventing premature
convergence by ensuring all nodes retain some chance of being explored.

## Author

Zhonghui Huang

## Examples

``` r
node.list <- initNodeList(search.space = "ivbase", phi0 = 1)
p.calculation(nodeslst = node.list, prob_min = 0.2)
#>    travel node.no    node.name edge.no local.edge.no   edge.name phi delta_phi
#> 1       0       1 compartments       1             1       1Cmpt   1         0
#> 2       0       1 compartments       2             2       2Cmpt   1         0
#> 3       0       1 compartments       3             3       3Cmpt   1         0
#> 4       0       2      eta_vp2       4             0  eta.vp2.no   1         0
#> 5       0       2      eta_vp2       5             1 eta.vp2.yes   1         0
#> 6       0       3       eta_q2       6             0   eta.q2.no   1         0
#> 7       0       3       eta_q2       7             1  eta.q2.yes   1         0
#> 8       0       4       eta_vp       8             0   eta.vp.no   1         0
#> 9       0       4       eta_vp       9             1  eta.vp.yes   1         0
#> 10      0       5        eta_q      10             0    eta.q.no   1         0
#> 11      0       5        eta_q      11             1   eta.q.yes   1         0
#> 12      0       6       eta_vc      12             0   eta.vc.no   1         0
#> 13      0       6       eta_vc      13             1  eta.vc.yes   1         0
#> 14      0       7           mm      14             0       mm.no   1         0
#> 15      0       7           mm      15             1      mm.yes   1         0
#> 16      0       8       eta_km      16             0   eta.km.no   1         0
#> 17      0       8       eta_km      17             1  eta.km.yes   1         0
#> 18      0       9        mcorr      18             0    mcorr.no   1         0
#> 19      0       9        mcorr      19             1   mcorr.yes   1         0
#> 20      0      10     residual      20             1         add   1         0
#> 21      0      10     residual      21             2        prop   1         0
#> 22      0      10     residual      22             3        comb   1         0
#>            p
#> 1  0.3333333
#> 2  0.3333333
#> 3  0.3333333
#> 4  0.5000000
#> 5  0.5000000
#> 6  0.5000000
#> 7  0.5000000
#> 8  0.5000000
#> 9  0.5000000
#> 10 0.5000000
#> 11 0.5000000
#> 12 0.5000000
#> 13 0.5000000
#> 14 0.5000000
#> 15 0.5000000
#> 16 0.5000000
#> 17 0.5000000
#> 18 0.5000000
#> 19 0.5000000
#> 20 0.3333333
#> 21 0.3333333
#> 22 0.3333333
```
