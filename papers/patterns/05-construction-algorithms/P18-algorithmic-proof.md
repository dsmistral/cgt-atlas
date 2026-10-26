# P18 - Algorithmic proof

- Family: 05-construction-algorithms
- Atlas one-line: The proof is a procedure; termination = theorem
- Home chapters (Atlas): 2, 5
- Status (through chunk 22a): Atlas-named textbook-canon pattern; in-corpus firings recorded below. Batch M: the isomorphism column M1/M2 (proof = procedure at its largest scale), the property-testing column M5/M6 (the testers), and 13c the classic-algorithms column (M7 flagship, M8 genuine, M9 partial). Batch N 14b: N6 partial (the Gale-Shapley round traces). Batch O 17a (extension corpus): O2 genuine - the LLL's first algorithmization; 17b: O4, O5 genuine (the constructive arc); Batch T 22a (extension corpus): T2 genuine - the machine-verification face (proof-by-execution), T1/T3 partial. Batch T 22b (extension corpus): T6 genuine - the linear-time treewidth algorithm (proof-equals-procedure, the f(k) constant honestly recorded as enormous). Batch W 25a: W1 genuine (deferred acceptance - the algorithm IS the proof) + W3 genuine (the Gomory-Hu cut tree). Batch X 26b (extension corpus): X6 genuine (the zig-zag iteration - the construction procedure whose correctness proof IS the expansion analysis). Batch Y 27a (extension corpus): Y1 partial (the LOCAL model's birth - the distributed model itself the object of study; the paper's own theorems impossibility lower bounds, no proof-equals-procedure firing). Batch Y 27b (extension corpus): Y5 genuine unplanned (the Book Algorithm - the Erdos-Szekeres argument reframed as an explicit algorithm and upgraded; proof-equals-procedure at the Ramsey upper-bound frontier)
- Migration: this dossier was machine-migrated 2026-10-13 from the batch files (the gather record and source of truth); every census row and hypothesis-test note below is QUOTED, not rewritten.

## Census rows (quoted; source = papers/BATCH-*.md)

### Batch A (chunk 1)
- Fires in: A9
- Notes: the resampling proof IS the algorithm

### Batch D (chunk 4)
- Fires in: D1, D2, D3, D4, D5, D6, D9
- Notes: D3 is the founding citation for polynomial-time-as-efficiency

### Batch E (chunk 5)
- Fires in: E3 (constructive), E8 (lineage: Kierstead-Kostochka algorithms)
- Notes: 

### Batch G (chunk 7)
- Fires in: G7, G12
- Notes: P30 meeting P18 at G7

### Batch M, sub-chunk 13a (chunk 13)
- Fires in: M1, M2 (genuine)
- Notes: the isomorphism column: the proof IS the procedure - polynomial-time bounded-valence testing (M1) and the quasipolynomial general test (M2); correctness and complexity analysis are one; the pattern's first GI-batch exemplars.

### Batch M, sub-chunk 13b (chunk 13)
- Fires in: M5, M6 (genuine)
- Notes: the property-testing column: the randomized tester IS the procedure - constant queries decide the property; the theorem is the algorithm's correctness with a constant query bound.

### Batch M, sub-chunk 13c (chunk 13)
- Fires in: M7 (flagship), M8 (genuine), M9 (partial)
- Notes: the classic-algorithms column: M7 - the linear-time planarity test (the batch's classic proof = procedure paper); M8 - Kruskal's Constructions A and B ARE the proof; M9 partial - the tractability side is an algorithm, but the theorem is the classification.

### Batch N, sub-chunk 14b (chunk 14)
- Fires in: N6 (partial)
- Notes: Propositions 1, 2, 7 - the Gale-Shapley round traces (exactly n rounds under shared preferences; one round iff each woman is exactly one man's first choice; n-1 soulmate pairs force a unique matching reached in j rounds); the trace IS the proof, with the honest caveat that the algorithm is the object of study (mirror of the M9 caveat).

### Batch O, sub-chunk 17a (chunk 17; extension corpus - NEXT100 seeds)
- Fires in: O2 (genuine)
- Notes: Beck 1991 - the LLL's first algorithmization: the existence proof replaced by an explicit search procedure with a complexity analysis, under a stronger constant (the constant-loss datum that 17b's O4/O5 erase); the direct ancestor of A9's resampling proof.

### Batch O, sub-chunk 17b (chunk 17; extension corpus - NEXT100 seeds)
- Fires in: O4 (genuine), O5 (genuine)
- Notes: O4 Moser 2009 - the resampling loop's termination analysis IS the theorem (A9's "the resampling proof IS the algorithm" line extends to the solo debut); O5 Kolipaka-Szegedy 2011 - the efficiency analysis up to the abstract lemma's exact Shearer boundary.

### Batch T, sub-chunk 22a (chunk 22; extension corpus - NEXT100 seeds)
- Fires in: T2 (genuine), T1 (partial), T3 (partial)
- Notes: T2 - a NEW FACE of the pattern recorded honestly: PROOF-BY-EXECUTION (the first major theorem proved by use of a computer; the reducibility-verification program's execution IS the proof's core; the surveyability/trust debate, Tymoczko's non-surveyability line, as the epistemology datum); T1 - the unavoidable-set verification bookkeeping; T3 - the computer-checked second proof (the quadratic coloring algorithm is the STOC 1996 companion's, cross-noted per the companion precedent)

### Batch T, sub-chunk 22b (chunk 22; extension corpus - NEXT100 seeds)
- Fires in: T6 (genuine)
- Notes: the classic-proof-equals-procedure face at the structure-family scale: the linear-time construction path IS the correctness argument (the M1/M2 isomorphism-column precedent); the f(k) constant enormous and honestly recorded - the practical-infeasibility note the later approximation and single-exponential FPT lines answered

### Batch W, sub-chunk 25a (chunk 25; extension corpus - NEXT100 seeds)
- Fires in: W1 (genuine), W3 (genuine)
- Notes: W1 - deferred acceptance: the proposal dynamic with the rejection argument and the strict-descent termination count proves the stable-matching existence theorem (the man-optimality lattice the paper's own addition; the N-batch stable-matching papers the corpus descendants). W3 - the Gomory-Hu cut tree: n-1 max-flow computations determine every pairwise minimum cut (the non-crossing-cuts lemma + condensation); the multi-terminal program's founding algorithm

### Batch X, sub-chunk 26b (chunk 26; extension corpus - NEXT100 seeds)
- Fires in: X6 (genuine)
- Notes: the iterative construction procedure - start from one constant-size expander, iterate the zig-zag product to arbitrary sizes: the construction algorithm whose correctness proof IS the expansion analysis (proof-equals-procedure, the W1/W3 origin-era face at the expander program); the paper's second theme the derandomization applications (the conference companion's "and Extractors" title the datum, per the companion precedent no double credit)

### Batch Y, sub-chunk 27a (chunk 27; extension corpus - NEXT100 seeds)
- Fires in: Y1 (partial)
- Notes: the LOCAL model born as an object of study - the distributed complexity class defined (synchronous rounds, local views; the graph the network); partial honestly per the N6 object-of-study precedent: the paper's own theorems are impossibility lower bounds (the Omega(log* n) ring-coloring bound, the Cole-Vishkin upper bound met exactly), no proof-equals-procedure firing


### Batch Y, sub-chunk 27b (chunk 27; extension corpus - NEXT100 seeds)
- Fires in: Y5 (genuine)
- Notes: the Book Algorithm - the 1935 Erdos-Szekeres upper-bound argument reframed as an explicit algorithm and upgraded (the Zigzag Lemma the key step; the paper's sections organized around the algorithm); proof-equals-procedure at the Ramsey upper-bound frontier: the algorithm IS the argument, its termination the theorem (R(k) <= (4-eps)^k, two proofs; UNPLANNED by seed - the seed expected P12)


## Hypothesis-test notes (quoted; source = papers/BATCH-*.md)

### Batch M, sub-chunk 13a (chunk 13)
- M1/M2 P18 confirmed (unplanned by seed - the M1/M2 seed rows expected P25/P19 and P8/P30; the algorithmic character of the whole batch is the surprise the census records).

### Batch M, sub-chunk 13c (chunk 13)
- M7/M8 P18 CONFIRMED (both expected by seed; M7 the flagship); M9 P18 partial (unplanned).

### Batch N, sub-chunk 14b (chunk 14)
- N6 P18 partial confirmed UNPLANNED by seed (the seed expected P5/P2/P23).

### Batch O, sub-chunk 17a (chunk 17)
- O2 P18 CONFIRMED (expected by seed - "the first constructive version").

### Batch O, sub-chunk 17b (chunk 17)
- O4/O5 P18 CONFIRMED (expected by seed); the constructive arc's payoff datum: O2's constant loss erased at O4, closed at O5.

### Batch T, sub-chunk 22a (chunk 22)
- T2 P18 firing UNPLANNED by seed (the seed rows expected P18 only at T3): the machine-verification face is the extension corpus's surprise; T3 P18 partial CONFIRMED (seed-expected, credited at partial with the honest companion note)

### Batch T, sub-chunk 22b (chunk 22)
- T6 P18 CONFIRMED (expected by seed): the treewidth algorithm's proof-as-procedure firing closes the batch's P18 pair - the machine-verification face (T2, 22a) and the human construction face (T6, 22b)

### Batch W, sub-chunk 25a (chunk 25)
- W1 P18 GENUINE CONFIRMED (expected by seed as the algorithmic classic). W3 P18 GENUINE with the seed's P17 expectation an honest miss: the paper's own move is the algorithm + the encoding face (P25 partial), the max-flow min-cut duality the used black box (D-batch owns it), cross-noted no census row

### Batch X, sub-chunk 26b (chunk 26)
- X6 P18 GENUINE CONFIRMED (expected by seed): the composition-era construction procedure - the explicit-family iteration with the spectral analysis as the correctness argument

### Batch Y, sub-chunk 27a (chunk 27)
- Y1 P18 partial (the seed's "P18 (the LOCAL model; the M-batch algorithmic extension)" expectation met at PARTIAL honestly): the model births the pattern's distributed face, but the paper's own theorems are impossibility lower bounds (the Omega(log* n) ring-coloring bound via the indistinguishable-views argument) - the N6 object-of-study precedent (the Gale-Shapley round traces)


### Batch Y, sub-chunk 27b (chunk 27)
- Y5 P18 GENUINE UNPLANNED by seed (the seed expected P12 - the random-construction expectation inverted by the paper's own deterministic design): the Book Algorithm the proof-equals-procedure face at the Ramsey frontier - the W1/W3/T6 lineage's newest member, born by reframing the 1935 Erdos-Szekeres argument AS an algorithm


## Cross-links (interdependence)

X6's iteration pairs the algorithmic face with the P11 construction line (the product replaces the arithmetic: the W1/W3 algorithm-as-proof era meeting the expander program).
Y1's LOCAL model is the distributed face's object-of-study half - the impossibility lower bounds set the model's boundary; the proof-equals-procedure face's distributed descendants stay uncorpus'd lineage.
Y5's Book Algorithm is the same batch's complementary genuine firing - the object-of-study half at Y1 (the model's boundary) and the proof-equals-procedure half at Y5 (the algorithm upgraded from the 1935 Erdos-Szekeres argument): the algorithmic pattern's two faces gathered in one wildcard batch.
