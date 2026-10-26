# D2 - Ford-Fulkerson (1956): Maximal flow through a network

- Metadata (web-verified 2026-10-13): L. R. Ford Jr., D. R. Fulkerson, "Maximal flow through a network", Canadian Journal of Mathematics 8 (1956): 399-404. Sources: Cambridge Core; standard reference listings.
- Summary (general-knowledge level, flagged sketch): the max-flow min-cut theorem - the maximum value of an s-t flow equals the minimum capacity of an s-t cut. Repeatedly augment along an f-augmenting path; when none exists, the vertex set reachable in the residual network has a saturated boundary - a cut of capacity equal to the flow value.
- Decisive moves: (1) [P16] augmenting-path iteration - improve a partial flow along residual arcs until stuck; (2) [P17] min-max - the stuck state manufactures the cut, a matching certificate, so max = min; (3) [P18] algorithmic proof, with the integrality corollary (integer capacities give integer max flows - flows as carriers of combinatorial proofs); (4) [P25] cross-domain encoding - the network model carries transport and later countless graph problems.
- New-pattern candidates: none new - flagship evidence that P16+P17 is a load-bearing pairing (augmentation manufactures the dual certificate).
- Full text: not fetched.
- Corrections log: none - seed row confirmed.
