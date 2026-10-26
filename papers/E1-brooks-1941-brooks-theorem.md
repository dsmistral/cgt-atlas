# E1 - Brooks (1941): On colouring the nodes of a network

- Metadata (web-verified 2026-10-13): R. L. Brooks, "On colouring the nodes of a network", Proceedings of the Cambridge Philosophical Society 37 (1941): 194-197. Sources: Cambridge Core (journal page); the Baetz-Wood citation listing (Proc. Cambridge Philos. Soc. 37:194-197, 1941).
- Summary (general-knowledge level, flagged sketch): Brooks' theorem - a connected graph of maximum degree Delta is Delta-colourable unless it is a complete graph or an odd cycle. The proof orders the vertices so each vertex has at most Delta - 1 later neighbours, then colors greedily in reverse order.
- Decisive moves: (1) [P15] induction/ordering - a spanning-tree (BFS-style) ordering from a suitable root realizes the "at most Delta - 1 later neighbours" property; (2) [P8] extremal characterization - the exceptions (complete graphs, odd cycles) are exactly the connected graphs where every subgraph has minimum degree >= Delta, forced by local structure; (3) greedy extension: the ordering converts a global claim into Delta - 1 local slack per vertex.
- New-pattern candidates: none new.
- Full text: not fetched - short note; textbook proofs (including Lovasz's 3-line version) are abundant.
- Corrections log: none - seed row confirmed.
