# D3 - Edmonds (1965): Paths, trees, and flowers

- Metadata (web-verified 2026-10-13): J. Edmonds, "Paths, trees, and flowers", Canadian Journal of Mathematics 17(3) (1965): 449-467. Open PDF located: web.eecs.umich.edu/~pettie/matching/Edmonds-paths-trees-flowers.pdf. Sources: Cambridge Core; UMich mirror.
- Summary (general-knowledge level, flagged sketch): the first polynomial-time algorithm for maximum matching in general (non-bipartite) graphs. Odd cycles - blossoms - obstruct the bipartite alternating-path search; Edmonds shrinks them and proves the matching lifts back.
- Decisive moves: (1) [P16] alternating-path augmentation beyond bipartite - the alternating tree search, with the blossom-shrinking move that lets the search continue through odd cycles; (2) [P25] reduction - blossom contraction replaces the graph by a smaller one whose perfect matching lifts back to the original; (3) [P18] algorithmic proof - termination plus the optimality certificate (an odd-set cover certifying maximality, Tutte-Berge style); (4) historical note: the passage proposing a "good algorithm" / polynomial time as the efficiency criterion is here - the founding citation for P18's modern reading.
- New-pattern candidates: none new.
- Full text: not fetched - open PDF located (UMich).
- Corrections log: none - seed row confirmed.
