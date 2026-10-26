# P4 - Recurrence + induction

- Family: 02-induction-extremal
- Atlas one-line: Relate case n to smaller cases
- Home chapters (Atlas): 1, 2, 3
- Status (through chunk 14c): Atlas-named textbook-canon pattern; in-corpus firings recorded below. Batch M 13a: the isomorphism column's recursions (M1 partial composition-series divide-and-conquer; M2 genuine aggregate-consumption). Batch N 14a: N2 genuine - the freshman-level independent-set recursion at a maximum-degree vertex is the Kahn-conjecture proof's skeleton (the accessibility datum). Batch N 14b: N4 genuine (the chip-firing paper's spine) + N5 genuine (the soulmate-removal induction). Batch N 14c: N7 genuine (the class-count recurrences) + N8 genuine (the strengthened list-coloring induction on |V(G)|). Batch V 24a: V2 partial (the minimal-counterexample induction frame) + V5 partial (the reducibility concept institutionalizing it). Batch V 24c: V12 genuine (the tournament insertion induction - the parity classic's spine)
- Migration: this dossier was machine-migrated 2026-10-13 from the batch files (the gather record and source of truth); every census row and hypothesis-test note below is QUOTED, not rewritten.

## Census rows (quoted; source = papers/BATCH-*.md)

### Batch A (chunk 1)
- Fires in: A5, A7, A8 (process bookkeeping)
- Notes: 

### Batch C (chunk 3)
- Fires in: C2 (functional equation), C3 (map decomposition)
- Notes: 

### Batch D (chunk 4)
- Fires in: D5 (exchange argument), D7 (reduction transitivity)
- Notes: 

### Batch F (chunk 6)
- Fires in: F2 (double induction), F3 (cups-caps), F6 (master induction), F8 (PET induction), F9 (Ramsey recursion)
- Notes: the batch's workhorse - five genuinely different induction schemes

### Batch G (chunk 7)
- Fires in: G1, G7 (refinement loops), G9 (uniformity induction), G10 (iterative purification)
- Notes: 

### Batch H (chunk 8)
- Fires in: H1, H2, H5, H13 (+ H8 through the decomposition)
- Notes: 

### Batch I (chunk 9)
- Fires in: I2, I12
- Notes: I2's original induction/case engine; I12's critical-matrix induction (the whole proof, remarkably elementary)

### Batch L, sub-chunk 12a (chunk 12)
- Fires in: L3, L1 (partial)
- Notes: L3 Hanani: the whole existence proof is an induction on v via recursive PBD/hole constructions. L1 Witt partial: stepwise extension S(5,6,12) from S(4,5,11) - the recursive skeleton is present but the blocks are placed by hand.

### Batch L, sub-chunk 12c (chunk 12)
- Fires in: L7 (partial)
- Notes: Teirlinck's construction reduces t to t-1 recursively (large-set-style machinery), but the placement is explicit handwork - partial, as at L1.

### Batch M, sub-chunk 13a (chunk 13)
- Fires in: M1 (partial), M2 (genuine)
- Notes: M1: divide-and-conquer down the composition series (the trivalent case P = G with elementary analysis; higher valence via primitive-group observations). M2: the aggregate-consumption recursion over the permutation domain is load-bearing in the quasipolynomial bound.

### Batch N, sub-chunk 14a (chunk 14)
- Fires in: N2 (genuine)
- Notes: induction on the vertex count via i(G) = i(G-w) + i(G-w-N(w)) at a maximum-degree vertex w - the recursion reduces the theorem to the local inequality j(G-w) + j(G-w-N(w)) <= j(G); the recursion itself is freshman-level (Batch N's accessibility datum).

### Batch N, sub-chunk 14b (chunk 14)
- Fires in: N4 (genuine), N5 (genuine)
- Notes: N4 - the paper's spine: induction on n for the stable configurations (Prop 3.1, the parallel firing strategy + subtree-isomorphism reduction), backward induction for the fire counts (Thm 4.1), the d0 recurrence (Prop 4.1) + the double induction of Thm 4.2, the recursive root-fire formula (Cor 4.3), the partial-sums recurrence (Prop 5.3). N5 - Prop 1: the forced soulmate pair removed, recursion on n (unique stable matching under shared preferences).

### Batch N, sub-chunk 14c (chunk 14)
- Fires in: N7 (genuine), N8 (genuine)
- Notes: N7 - the class-count recurrences for the cases with no clean closed form: f(n) = f(n-1) + (n-2) f(n-2) + 1 ({123,132,312}), f(n) = f(n-1) + (n-1) f(n-2) ({123,132}{213,312}), and the two-parameter recursion g(n,k) (a three-fold case analysis with a binomial double-sum interior) summed as f(n) = sum_k g(n+1,k) + n - 2 ({123,231}{213,312}). N8 - induction on the number of vertices of G under a STRENGTHENED hypothesis (the list-coloring form, Theorem 4.1; the C6/K3 toy calculation conditioning on the leftmost vertex's color; the dimension-reduction step) - the strengthening is the load-bearing move (the P15 induction-on-vertices form noted, no double credit).

### Batch V, sub-chunk 24a (chunk 24; extension corpus - NEXT100 seeds)
- Fires in: V2 (partial), V5 (partial)
- Notes: V2 - the minimal-counterexample frame: remove a low-degree region from a smallest five-chromatic map and extend the colouring (the extension step fails - Heawood's two-chain interference - but the frame survives into every later proof of the saga). V5 - reducibility institutionalized: a configuration is reducible if no minimal counterexample can contain it, proved by ring analysis - the minimal-counterexample frame made into the reducibility half of the eventual computer proofs (unavoidability the other half)

### Batch V, sub-chunk 24c (chunk 24; extension corpus - NEXT100 seeds)
- Fires in: V12 (genuine)
- Notes: the insertion induction - a new vertex slots into a Hamiltonian path of the preceding subtournament; the parity refinement's spine and the proof every standard treatment of Redei's theorem runs (the odd-count statement: every tournament has an ODD number of directed Hamiltonian paths)

## Hypothesis-test notes (quoted; source = papers/BATCH-*.md)

### Batch I (chunk 9)
- I12 P23 MISSED (expected): the Stanley-Wilf bound is pure structural induction; no compression appears. P4 confirmed.

### Batch L, sub-chunk 12a (chunk 12)
- L3 P11 AND P4 CONFIRMED (both expected).

### Batch L, sub-chunk 12b (chunk 12)
- L4 P4 partial only (not credited): the recursive hole/PBD machinery is inherited from Hanani (L3) and lives inside Wilson's composition theorems; the headline existence-conjecture proof runs on elementary number theory (finite basis for PBD-closed sets), not induction on v.

### Batch L, sub-chunk 12c (chunk 12)
- L7 P4 partial confirmed: the recursive skeleton carries the construction; no new genuine firing.

### Batch M, sub-chunk 13a (chunk 13)
- M2 P4 confirmed (unplanned by seed); M1 P4 partial - the recursion is the vehicle, but the analysis's novel content is group-theoretic (bounded simple sections), matching no Atlas pattern.

### Batch N, sub-chunk 14a (chunk 14)
- N2 P4 confirmed (UNPLANNED by seed; the seed expected P29/P25/P10/P9): the accessible skeleton of the Kahn-conjecture settlement.

### Batch N, sub-chunk 14b (chunk 14)
- N4 P4 CONFIRMED (expected by seed); N5 P4 confirmed UNPLANNED (the seed expected P25/P9/P16): induction is the middle-school engine after the encoding.

### Batch N, sub-chunk 14c (chunk 14)
- N7 P4 confirmed UNPLANNED (the seed expected P1/P5/P23); N8 P4 confirmed UNPLANNED (the seed expected P10/P25/P30/P31): the strengthened-induction move carries the reverse-Sidorenko proof's skeleton.

### Batch V, sub-chunk 24a (chunk 24)
- V2/V5 P4 partials UNPLANNED by seed (the NEXT100 rows targeted the Kempe-watch and reducibility lineage, not a P-ID census): the induction frame is the four-colour saga's skeleton from its 1879 origin

### Batch V, sub-chunk 24c (chunk 24)
- V12 P4 genuine CONFIRMED (expected by seed as "an induction classic"): the founding-century induction classic - the tournament insertion argument at its 1934 origin

## Cross-links (interdependence)

P15 is the same ladder one rung down; the monovariant/potential watch-item overlaps this pattern (synthesis call on distinctness).
