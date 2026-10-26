# P25 - Reduction / encoding

- Family: 05-construction-algorithms
- Atlas one-line: Translate one problem into another language; the target structure carries the proof or the hardness
- Home chapters (Atlas): 3, 10, 11
- Status (through chunk 22b): Atlas-named textbook-canon pattern; in-corpus firings recorded below. Batch M: the isomorphism column fires it twice (M1/M2 genuine), M3 the flagship encoding, M4 the second framework firing (genuine), M5/M6 the property-testing partials, and 13c M7 partial (DFS/path encoding) + M9 genuine (the CSP classification). Batch N 14a: N2 genuine - Zhao's bipartite-swapping reduction reused as the Kahn-conjecture settlement's step 1 - see the census rows. Batch N 14b: N5 flagship genuine (the SMP <-> Sudoku translation) + N4 partial (the base-k digit encoding). Batch N 14c: N8 genuine (the homomorphism encoding) + N7 partial (the orbit reduction). Batch O 17b (extension corpus): O4 partial (the witness-tree encoding). Batch P 18a (extension corpus): P1 partial (the KW certificate encoding) + P2 partial (the container algorithm's profile encoding). Batch R 20a (extension corpus): R1 genuine + R2 genuine - the flag-algebra translation move at the extremal level (the K_r density problem in the algebra's positivity language) and the meta level (inequalities as quantum-graph positivity statements); Batch R 20b (extension corpus): R3 genuine (the pentagons line's flag encoding) + R4 genuine (the homomorphism-counting framework encoding - the N8/M9 cross-notes); Batch T 22b (extension corpus): T5 partial (the graph-as-term encoding, unplanned by seed - standard-tool credit per the M9 precedent). Batch V 24b (extension corpus): V10 partial (the de Bruijn sequence - the encoding IS the object: all 2^n words of length n packed into one cyclic word of length 2^n; the object-vs-engine split, honestly partial). Batch V 24c: V13 partial (the forbidden-subdivision reduction) + V14 partial (the confusability-graph encoding - the zero-error origin). Batch W 25a: W3 partial (the cut-tree encoding - n-1 tree edges carrying every pairwise cut value). Batch X 26a (extension corpus): X2 + X3 partial (the concentrator/superconcentrator encodings - the objects ARE the translations). Batch Y 27a (extension corpus): Y4 genuine (the long-code encoding + gap-preserving reductions - the PCP program's optimization boundary). Batch Y 27b (extension corpus): Y5 partial unplanned (the book reduction - "to bound R(k) it suffices to find a large book", the inherited framing traced to Ramsey's original paper)
- Migration: this dossier was machine-migrated 2026-10-13 from the batch files (the gather record and source of truth); every census row and hypothesis-test note below is QUOTED, not rewritten.

## Census rows (quoted; source = papers/BATCH-*.md)

### Batch B (chunk 2)
- Fires in: B7
- Notes: classical theorems rephrased as hypergraph independence

### Batch D (chunk 4)
- Fires in: D1, D3, D5, D7, D8, D9, D10
- Notes: D7 is the whole-paper exemplar; D5 classifies optimizers by encoding; D9's lossless metric encoding

### Batch E (chunk 5)
- Fires in: E4 (Tait), E5/E6 (group products), E7 (hypergraph correspondence), E11 (kernels)
- Notes: E7's bipartite-hypergraph correspondence is two-way

### Batch F (chunk 6)
- Fires in: F4 (partition -> density), F7 (2D -> 1D), F8 (ergodic transference), F10 (structural/hereditary)
- Notes: 

### Batch G (chunk 7)
- Fires in: G1 (reduced graph), G3 (chromatic-number reduction), G12 (analytic recasting)
- Notes: 

### Batch H (chunk 8)
- Fires in: H2 (block decomposition), H8 (tree decomposition), H9 (basic classes + 2-joins), H10 (hypergraph formulation), H12 (cell decomposition)
- Notes: 

### Batch L, sub-chunk 12a (chunk 12)
- Fires in: L1 (partial)
- Notes: the Mathieu groups constructed as the design automorphism groups - combinatorics and group theory carried together; the successive transitive extensions mirror the design extensions.

### Batch M, sub-chunk 13a (chunk 13)
- Fires in: M1 (genuine), M2 (genuine), M3 (flagship)
- Notes: the isomorphism column carries the pattern twice - M1: GI encoded as the color-automorphism problem for permutation groups with bounded simple sections (the reduction IS the title move); M2: GI reduced to String Isomorphism / Coset Intersection under group action (the Luks-framework vehicle, quasipolynomial in the largest orbit); M3: asymptotic extremal questions encoded as elements of the flag algebra with positivity constraints - the model-theoretic translation is the whole framework.

### Batch M, sub-chunk 13b (chunk 13)
- Fires in: M4 (genuine), M5 (partial), M6 (partial)
- Notes: M4: the flag-algebra encoding again (the density problem translated into the algebra's positivity constraints - the framework's second in-corpus firing). M5 partial: a monotone property reduced to a finite set of forbidden colorings of reduced graphs. M6 partial: a property encoded by its regularity profile - the characterization is an encoding statement.

### Batch M, sub-chunk 13c (chunk 13)
- Fires in: M7 (partial), M9 (genuine)
- Notes: M7 partial (unplanned): the graph encoded into DFS/path structures - the path decomposition makes the iterative path-addition embedding tractable (the paper's own Auslander-Parter framing). M9 (expected by seed): homomorphism <-> CSP <-> conjunctive-query evaluation as one problem in three languages, with the complexity encoded as a structural invariant (bounded tree-width of cores) - the "other side" perspective is itself a translation.

### Batch N, sub-chunk 14a (chunk 14)
- Fires in: N2 (genuine)
- Notes: Zhao's bipartite-swapping trick (the double cover G x K2: i(G)^2 <= i(G x K2) via the explicit injection, and j(G)^2 = j(G x K2)) reduces the general theorem to the bipartite case - inherited machinery doing load-bearing work at the youth-research frontier.

### Batch N, sub-chunk 14b (chunk 14)
- Fires in: N5 (flagship), N4 (partial)
- Notes: N5 - the whole-paper move: the bidirectional SMP <-> Sudoku translation (preference profiles drawn in Sudoku grids; blocking pairs and the Gale-Shapley algorithm in Sudoku language; mutually Latin / disjoint / joint profiles; the new joint-groups Sudoku invented to carry the correspondence). N4 - the base-k digit encoding of the stable configuration (Prop 3.2: chips per layer = 1 + the k-ary digits of N - (k^n-1)/(k-1)), the representation that carries the fire-count section.

### Batch N, sub-chunk 14c (chunk 14)
- Fires in: N8 (genuine), N7 (partial)
- Notes: N8 - the whole-problem move: i(G) = hom(G, H_ind), c_q(G) = hom(G, K_q), the Ising/Potts partition functions as hom counts into looped/weighted H; Question 1.3 (maximize hom(G,H)^{1/|V(G)|} among d-regular G) unifies Questions 1.1-1.2. N7 - the Klein-four orbit reduction (composing every pattern with the reversal and the value-complement preserves the class structure - one representative per orbit counted) + the section-4 pattern-avoidance connection (avoiders are trivial classes; when all non-avoiders merge, class counting reduces to avoidance counting).

### Batch O, sub-chunk 17b (chunk 17; extension corpus - NEXT100 seeds)
- Fires in: O4 (partial)
- Notes: Moser's witness trees - execution logs encoded as labeled rooted trees, the counted object that makes the entropy-compression contradiction quantitative (the encoding face of the CAND-A4 origin).

### Batch P, sub-chunk 18a (chunk 18; extension corpus - NEXT100 seeds)
- Fires in: P1 (partial), P2 (partial)
- Notes: the certificate/profile encoding of the container ancestor - P1: the C4-free graphs compressed into few degree-ordered profiles, each counted by binomial bounds (flagged-sketch, survey level); P2: the same encoding as the survey algorithm's core (the KW algorithm of the survey's Section 2).

### Batch R, sub-chunk 20a (chunk 20; extension corpus - NEXT100 seeds)
- Fires in: R1 (genuine), R2 (genuine)
- Notes: the flag-algebra framework's translation move at two levels - R1: the clique-density extremal question encoded in the algebra's positivity language (the M3/M4 face at the program's capstone); R2: extremal inequalities encoded as quantum-graph positivity statements, the encoding applied to the decidability question itself

### Batch R, sub-chunk 20b (chunk 20; extension corpus - NEXT100 seeds)
- Fires in: R3 (genuine), R4 (genuine)
- Notes: the encoding at the two faces of the flag-algebras arc's close - R3: the C5-density extremal question encoded in the algebra's positivity language (the M3/M4/R1 translation move, the pentagons line); R4: the homomorphism-counting encoding as the chapter's whole framework move (homomorphism densities as the unification language) - cross-noted to N8 (the homomorphism encoding's youth-lineage firing) and M9 (homomorphism classification by structure)

### Batch T, sub-chunk 22b (chunk 22; extension corpus - NEXT100 seeds)
- Fires in: T5 (partial)
- Notes: the graph-as-term encoding: the graph's parse-tree (algebraic-term) representation is what the MSO automaton consumes - standard-tool credit, unplanned by seed, per the M9 precedent; the definability framework's encoding face

### Batch V, sub-chunk 24b (chunk 24; extension corpus - NEXT100 seeds)
- Fires in: V10 (partial)
- Notes: the encoding IS the object: the maximal cyclic sequence packing all 2^n binary words of length n into one cyclic word of length 2^n (the count 2^(2^(n-1)-n)); the shift-register/de Bruijn-graph frame retrospective; partial credit for the object-vs-engine reason (the encoding is studied, not deployed as a proof device) - the same-author continuation of C7 resolved at gather: distinct papers, distinct engines (P25 here vs P39's averaging at C7)

### Batch V, sub-chunk 24c (chunk 24; extension corpus - NEXT100 seeds)
- Fires in: V13 (partial), V14 (partial)
- Notes: V13 - the forbidden-subdivision reduction: planarity reduced to two canonical obstructions (K5, K3,3) - the object-vs-engine datum again (the V10 precedent), the M7 planarity test's theorem-level ancestor. V14 - the confusability-graph encoding IS the theory: zero-error codes -> independent sets in strong powers, capacity -> asymptotic independence - the zero-error origin and the J2 lineage's birthplace (the pentagon problem born open here, solved by the corpus's J2 Lovasz 1979)

### Batch W, sub-chunk 25a (chunk 25; extension corpus - NEXT100 seeds)
- Fires in: W3 (partial)
- Notes: the flow-equivalent tree IS the object: exponentially many pairwise cut values compressed into n-1 tree edges (the V10 de Bruijn precedent - the encoding as the contribution, the P18 algorithm its construction; the P17 duality the used black box, cross-noted no census row)

### Batch X, sub-chunk 26a (chunk 26; extension corpus - NEXT100 seeds)
- Fires in: X2 (partial), X3 (partial)
- Notes: the encoding faces at the expansion origins: the network problems translated into graph theory - the concentrator (arbitrary input patterns through a bounded-degree network) and the superconcentrator (the linear-size routing extremum) ARE the translations; partial honestly per the V10 object-vs-engine precedent: the papers construct the objects, the P25 framing is the abstraction, not a load-bearing reduction

### Batch Y, sub-chunk 27a (chunk 27; extension corpus - NEXT100 seeds)
- Fires in: Y4 (genuine)
- Notes: the long-code encoding + the gap-preserving reductions - the constraint instance translated into the long-code/dictatorship language, the verifier's test the decoding, the inapproximability factor the preserved gap (the optimal 1/2 and 7/8 ratios closed at the matching algorithmic bounds; the seed's "PCP reductions; the optimization boundary" expectation met)


### Batch Y, sub-chunk 27b (chunk 27; extension corpus - NEXT100 seeds)
- Fires in: Y5 (partial)
- Notes: the book reduction - "to bound R(k) it suffices to find a large book" - the translation inherited from Ramsey's original paper (the paper's own framing of the reduction); partial honestly per the V10 object-vs-engine precedent: the framing inherited, not a deployed encoding; UNPLANNED by seed (the seed expected P12)


## Hypothesis-test notes (quoted; source = papers/BATCH-*.md)

### Batch M, sub-chunk 13a (chunk 13)
- M1 P25 CONFIRMED (expected by seed); M3 P25 CONFIRMED (expected, flagship); M2 P25 confirmed UNPLANNED by seed (the M2 seed row expected P8/P30, both missed) - the reduction chain GI -> String Isomorphism -> Coset Intersection is the abstract's own framing.

### Batch M, sub-chunk 13b (chunk 13)
- M4 P25 CONFIRMED (expected by seed); M5/M6 P25 partials confirmed (unplanned - the seeds expected only P30).

### Batch M, sub-chunk 13c (chunk 13)
- M9 P25 CONFIRMED (expected by seed, genuine); M7 P25 partial confirmed (unplanned - the DFS/path encoding).

### Batch N, sub-chunk 14a (chunk 14)
- N2 P25 CONFIRMED (expected by seed): the swapping reduction is step 1 of the Kahn-conjecture settlement.

### Batch N, sub-chunk 14b (chunk 14)
- N5 P25 CONFIRMED (expected by seed; the flagship encoding); N4 P25 partial confirmed UNPLANNED (the seed expected P5/P7/P4): the digit translation as the representation move.

### Batch N, sub-chunk 14c (chunk 14)
- N8 P25 CONFIRMED (expected by seed): the homomorphism encoding is the problem-unification move (independent sets, colorings, and statistical-mechanics partition functions as one object). N7 P25 partial confirmed UNPLANNED (the seed expected P1/P5/P23): the orbit reduction + the avoidance connection.

### Batch O, sub-chunk 17b (chunk 17)
- O4 P25 partial confirmed UNPLANNED by seed (the O4 seed row expected the CAND-A4/P13/P18 family only).

### Batch P, sub-chunk 18a (chunk 18)
- P1/P2 P25 partials confirmed UNPLANNED by seed (the P rows expected the container datum only): the encoding is the ancestor method's counting mechanism.

### Batch R, sub-chunk 20a (chunk 20)
- R1/R2 P25 FIRES GENUINELY (expected by seed): the R rows' own target ("WATCH flag algebras; P25") met - the flag-algebra encoding is the framework's translation move, and batch R runs it at both the extremal level (R1) and the meta level (R2).

### Batch R, sub-chunk 20b (chunk 20)
- R3/R4 P25 FIRES GENUINELY: R3 the flag-encoding face of the pentagons line (the seed rows' target met at the third flag-algebra paper); R4 the homomorphism-counting framework itself - the honest unplanned datum, with flag algebras NOT firing there (the language, not the calculus; the N8/M9 cross-notes).

### Batch T, sub-chunk 22b (chunk 22)
- T5 P25 partial UNPLANNED by seed (the seed rows expected only P35 at T5): the graph-as-term encoding is the definability framework's reduction move - partial credit, the M9 precedent (the pattern's 13c co-touch at the same paper line)

### Batch V, sub-chunk 24b (chunk 24)
- V10 P25 partial CONFIRMED (expected by seed as "P25 encoding"): the object-vs-engine datum - the paper studies encodings rather than deploying one; partial, honestly

### Batch V, sub-chunk 24c (chunk 24)
- V13 P25 partial UNPLANNED by seed (the NEXT100 row targeted the M7-ancestor role, not a P-ID census); V14 P25 partial CONFIRMED (expected by seed as the J2-lineage origin): the encoding-as-object at the planarity and information-theory origins

### Batch W, sub-chunk 25a (chunk 25)
- W3 P25 partial (UNPLANNED by seed - the seed expected P17): the encoding face fires at the cut tree - the survey's encoding family gains its optimization-era member (V10, M7-adjacent, and now W3 faces distinct)

### Batch X, sub-chunk 26a (chunk 26)
- X2/X3 P25 partial (the seed's expected-pattern columns named no P-ID - the encoding faces UNPLANNED): the concentrator and superconcentrator abstractions ARE the translations - partial per the V10 object-vs-engine precedent

### Batch Y, sub-chunk 27a (chunk 27)
- Y4 P25 CONFIRMED (expected by seed as "PCP reductions; the optimization boundary"): the long-code/dictatorship translation at the optimization boundary - the PCP program's approximation-era flagship encoding


### Batch Y, sub-chunk 27b (chunk 27)
- Y5 P25 partial UNPLANNED by seed (the seed expected P12): the book reduction the inherited framing's translation face - partial per the V10 object-vs-engine precedent (the reduction Ramsey's own, the Book Algorithm the paper's contribution)


## Cross-links (interdependence)

(none recorded)
