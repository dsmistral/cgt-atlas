# The pattern layer - one file per pattern, grouped by similarity and interdependence

Added 2026-10-13 (work style v2, user-directed; charter amendment in ../README.md).

## What this layer is

An index and accumulator OVER the batch files - never a replacement. Each pattern file quotes the census rows and hypothesis-test notes from papers/BATCH-*.md, which remain the gather record and source of truth. Purposes:

1. Resume: a new chat reads ONE small pattern dossier instead of eleven batch files.
2. Synthesis: chunk 14 builds papers/ANALYSIS.md from these dossiers (load-bearing test, silent-registry evidence, P43+ proposals).
3. Incremental safety: every gather sub-chunk appends only to the pattern files it touched, then pushes.

## Families (grouped by move-similarity and engine interdependence)

| Folder | Patterns | The family's shared engine |
|--------|----------|----------------------------|
| 01-counting | P1, P2, P3, P6, P7, P9 | count it directly, two ways, by complement, by parity, by boxes |
| 02-induction-extremal | P4, P8, P15, P26 | climb the ladder or take the extremal object and force structure |
| 03-probability | P10, P12, P13, P14, P27, P28 | sample, average, prune; tails and correlations |
| 04-analytic-information | P5, P29 | generating functions; entropy as the counting currency |
| 05-construction-algorithms | P11, P18, P25 | build the object; the proof is a procedure; translate problems |
| 06-duality-optimization | P16, P17, P37 | augment toward the optimum; min = max; structural duals |
| 07-linear-algebra-polynomial | P19, P21, P22 | vectors, eigenvalues, polynomials - dimension bounds |
| 08-canonicalization | P20, P23, P24, P32 | push toward the extremal/canonical configuration; price it |
| 09-density-structure | P30, P31, P33 | regularity, removal, density increments - the modern density era |
| 10-graph-structure | P34, P35, P36, P38 | minors, decompositions, charges, replication |
| 11-symmetry-designs-codes | P39, P40, P41, P42 | symmetry averaging, Mobius inversion, divisibility, words-as-designs |
| candidates | CAND-A1..A4, B5, C1, G1 + six watch-items | pattern candidates outside P1-P42, with the load-bearing test in mind |

## Cross-family links that matter (interdependence recorded at gather time)

- P2 <-> P41: divisibility is double counting's arithmetic face.
- P10 <-> P20/P23: where symmetrization was expected, averaging or shifting did the work (the K-batch synthesis call).
- P23 <-> P24: compression vs pricing - two ways to canonicalize.
- P19/P21/P22 <-> slice-rank watch: a family face; synthesis call on naming.
- P32 <-> P30/P31: stability is the canonicalization face of the regularity era.
- P17 <-> P37 <-> P16: augmentation witnesses the min-max; structural duals carry it.
- P4 <-> P15; P5 <-> CAND-C1; P28 <- K1 (the Littlewood-Offord lineage arc); P29 -> CAND-A4 / spread watch.

## Update rule (standing)

At every sub-chunk close: append the sub-chunk's census rows and hypothesis-test notes to each touched pattern file (quoted, tagged by sub-chunk), refresh the pattern's status line and INDEX.md, and push together with the batch files and STATE.md. Extend, never rewrite; corrections to a quoted census row go into the pattern file as a dated correction note, never silent edits. All files under papers/ stay ASCII-only.
