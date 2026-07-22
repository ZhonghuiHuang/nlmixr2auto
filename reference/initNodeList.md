# Initialize node list for ACO search space

Construct the initial edge list used in model structure search based on
ant colony optimization.

## Usage

``` r
initNodeList(search.space, phi0)
```

## Arguments

- search.space:

  Character, one of "ivbase" or "oralbase". Default is "ivbase".

- phi0:

  A non-negative numeric value. Initial pheromone value assigned to all
  nodes at the start of the search. Defaults to 2.

## Value

A data.frame in which each row represents an edge in the ACO
path-construction graph, with the following columns:

- travel:

  Integer. Travel counter associated with the edge, initialized to zero.

- node.no:

  Integer. Decision node identifier corresponding to a model feature.

- node.name:

  Character. Semantic label of the decision node.

- edge.no:

  Integer. Global edge index.

- local.edge.no:

  Integer. Index of the edge within the corresponding decision node.

- edge.name:

  Character. Semantic label of the edge (model component choice).

- phi:

  Numeric. Initial pheromone value associated with the edge.

- delta_phi:

  Numeric. Change in pheromone level, initialized to zero.

- p:

  Numeric. Initial selection probability of the edge.

## Author

Zhonghui Huang

## Examples

``` r
initNodeList(search.space = "ivbase", phi0 = 1)
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
#>        p
#> 1  0.333
#> 2  0.333
#> 3  0.333
#> 4  0.500
#> 5  0.500
#> 6  0.500
#> 7  0.500
#> 8  0.500
#> 9  0.500
#> 10 0.500
#> 11 0.500
#> 12 0.500
#> 13 0.500
#> 14 0.500
#> 15 0.500
#> 16 0.500
#> 17 0.500
#> 18 0.500
#> 19 0.500
#> 20 0.333
#> 21 0.333
#> 22 0.333
initNodeList(search.space = "oralbase", phi0 = 1)
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
#> 14      0       7       eta_ka      14             0   eta.ka.no   1         0
#> 15      0       7       eta_ka      15             1  eta.ka.yes   1         0
#> 16      0       8           mm      16             0       mm.no   1         0
#> 17      0       8           mm      17             1      mm.yes   1         0
#> 18      0       9       eta_km      18             0   eta.km.no   1         0
#> 19      0       9       eta_km      19             1  eta.km.yes   1         0
#> 20      0      10        mcorr      20             0    mcorr.no   1         0
#> 21      0      10        mcorr      21             1   mcorr.yes   1         0
#> 22      0      11     residual      22             1         add   1         0
#> 23      0      11     residual      23             2        prop   1         0
#> 24      0      11     residual      24             3        comb   1         0
#>        p
#> 1  0.333
#> 2  0.333
#> 3  0.333
#> 4  0.500
#> 5  0.500
#> 6  0.500
#> 7  0.500
#> 8  0.500
#> 9  0.500
#> 10 0.500
#> 11 0.500
#> 12 0.500
#> 13 0.500
#> 14 0.500
#> 15 0.500
#> 16 0.500
#> 17 0.500
#> 18 0.500
#> 19 0.500
#> 20 0.500
#> 21 0.500
#> 22 0.333
#> 23 0.333
#> 24 0.333
```
