# D4 - Dinic (1970): Algorithm for solution of a problem of maximum flow in a network with power estimation

- Metadata (web-verified 2026-10-13): E. A. Dinic, "Algorithm for solution of a problem of maximum flow in a network with power estimation", Soviet Mathematics Doklady 11 (1970): 1277-1280; Russian original in Dokl. Akad. Nauk SSSR 194 (1970). TITLE VERIFIED - the seed's "(verify title)" marker resolved. Sources: Wikipedia (Dinic's algorithm) reference; SCIRP reference listing; Dinitz's historical account (Springer chapter).
- Summary (general-knowledge level, flagged sketch): max flow in O(V^2 E) by phases: each phase builds the layered (level) network by BFS from the source and pushes a blocking flow; the source-to-sink distance strictly increases from phase to phase, so there are at most V phases.
- Decisive moves: (1) [P18] algorithmic proof - the phase-count analysis; (2) [monovariant watch] the potential/monovariant argument - source-sink distance is the potential that strictly rises each phase, terminating the outer loop (same watch-item family as D6); (3) [P16] augmentation batched - the blocking flow exhausts all shortest augmenting paths at once; (4) [P25] encoding - the layered network compresses the residual graph into levels.
- Honest note: the algorithm known worldwide as "Dinic's" is the Even-Itai modification of Dinitz's original (per Dinitz's own historical account); both share the phase/monovariant structure.
- New-pattern candidates: none new; contributes to the monovariant/potential-termination watch-item.
- Full text: not fetched - the Dinitz historical chapter documents the algorithm in English.
- Corrections log: TITLE verified ("...with power estimation"); transliteration Dinitz recorded; pages 1277-1280.
