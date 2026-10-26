---
name: "cgt-ch20-named-methods"
title: "Ch. 20 — Named Methods: Six Engines the Field Actually Uses (A Lecture Course in the Feynman Style)"
type: "text/markdown"
---

# Chapter 20 · Named Methods

*Part of the Combinatorics & Graph Theory Atlas (the chapter map lives in the book basis).*

The Atlas's pattern index (P1 through P45) catalogs proof *moves* — a double count, an involution, a monovariant, a window. This chapter is about a different species: methods with names. When a paper's abstract says "by the container method" or "using flag algebras" or "via iterative absorption," a referee knows exactly what machinery is coming, the way an engineer knows what "finite element analysis" means. A named method is a reusable engine plus a name the community has agreed to use. This chapter builds the six the survey record recommended for adoption: the **container method** (count a huge family by covering it with few small boxes), **analytic combinatorics** (read exact asymptotics off the singularities of a generating function), **flag algebras** (a calculus that turns Cauchy–Schwarz into computer-checkable extremal lower bounds), **absorption** (convert an approximate decomposition into an exact one by planning the cleanup in advance), **randomized algebraic construction** (algebraic templates plus randomized choices, the engine that proved the Existence Conjecture for designs), and the **strategy devices** of the contest canon (the pairing strategy, the adaptive adversary, the state-partition block — three engines that decide entire olympiad problems and carry no P-ID at all).

The honest arc behind this chapter is worth stating up front, because it is itself a datum. None of the six earned a pattern entry on the survey's planned corpus: hypergraph containers were *demoted* (the two origin papers sit in a single batch, and "the letter of the two-batch gate governs"), analytic combinatorics was demoted the same way, and flag algebras, absorption, and randomized algebraic construction each fired once in-corpus, at their origins. The survey's recommendation was adoption on *external evidence* — and its extension batches then crossed the two-batch gates in-survey, one by one (containers: batch B + batch P; analytic combinatorics: batch C + batch Q; flags: batch M + batch R; absorption: batch L + batch S), superseding the external-only route. This chapter is the adoption record: six lectures, one per method, each with its origin story, its honest statement (proved here only where the proof fits; cited with pin levels where it does not), and the receipts the lab could verify. The strategy devices join them by the container-method precedent — three contest canons, one datum each, engines the pattern index does not name.

The deal with the reader is the one the Atlas has enforced since Chapter 1: every number printed below was machine-verified before printing, and the receipts came first. The lab runs on the documented Lehmer/MINSTD engine x ← 48271·x mod (2³¹−1) with integer-exact draw rules; the randomized panels use seeds 20261090 (Part 4), 20261091 (Part 5's relabeling), 20261092–20261094 (Part 6's three panels), and the rest — the sum-free census, the exact-arithmetic asymptotics, the exhaustive flag panels, the strategy minimaxes — are deterministic. The printed Python lab reproduces every receipt value-for-value, and a post-compaction verification pass re-implemented every panel from the documented rules alone and re-verified all of them before a line of prose was installed. Where the lab's toy fails to reproduce a method's real power, the text says so in place: the container toy's prefix key alone leaves one box holding a third of everything; the absorption toy's post-hoc repair completes 200/200 but sacrifices 92% of what it repairs. The receipts govern; where the machine corrected the author, the prediction is printed as wrong.

## How to read this chapter

Read with Chapter 13 (the probabilistic toolkit) and Chapter 17 (designs — where Keevash's template machinery and the n = 9 exhibit already live) within reach, and Chapter 19 (the Lovász Local Lemma) as the sibling chapter: it too was adopted from the survey's named-methods ledger, and it got its own chapter because its pattern entry (P45) is a proof *move* with a certificate and a boundary theorem; the six methods here are bigger machines that *deploy* moves. Lines marked **✎ Checkpoint** are the places to stop and predict — commit to a guess, in ink, before reading on. Exercises are graded ●○○ *easy* (one idea, applied directly), ●●○ *moderate* (two ideas, or one tricky step), ●●● *tough* (several ideas combined); ◆ **pattern unknown** problems come with no hint — diagnosing the tool is part of the problem; ◐ **Explorations** are open-ended investigations that state what you should find, not a number to match. Worked answers sit at the end; hints travel with the problems.

Notation. [n] = {1,…,n}; a set A ⊆ [n] is **sum-free** if x + y ∉ A for all x, y ∈ A; **SF(n)** counts sum-free subsets of [n] (the empty set included), **fmax(n)** counts *maximal* ones; for a sum-free A, **s** = #{x ∈ A : x ≤ n/2} and **v** = #{even x ∈ A}. Generating functions: C_n = Catalan, binom(2n,n) the central binomial, H_n harmonic; r_n the number of rooted trees on n vertices, t_n the number of unrooted trees, α = 2.95576528… Otter's constant; [z^n] extracts coefficients. Graphs: A the adjacency matrix, T the triangle count, m the edge count; tr(A³) = 6T, tr(A²) = 2m, and each C5 contributes exactly 10 closed 5-walks, so #C5 = tr(A⁵)/10 in triangle-free graphs. Designs: an **STS(v)** is a Steiner triple system — triples covering every pair of v points exactly once (v ≡ 1, 3 mod 6 necessary); the lab's template lives in F₂⁴: the 15 nonzero vectors, triples {x, y, x ⊕ y}; GL(4,2) is the invertible 4×4 group of order (16−1)(16−2)(16−4)(16−8) = 20160. Games: {0,1,2}^n the digit cube, φ the pairing map; the snail's **route** is its vector of descent columns (a₁,…,a_{R−1}); the grid game's **states** are its 2×2 blocks. The lab engine: *nxt()* advances x ← 48271·x mod (2³¹−1); a uniform choice among m items is floor(nxt()·m/(2³¹−1)); Fisher–Yates steps draw one index each. e = 2.71828…

## The pattern map for this chapter

| Pattern | Plain language | Where it fires here |
|---------|---------------|--------------------|
| **P4 Recurrence + induction** | Relate case n to smaller cases | L2 (Otter's recurrences, exact to n = 256); Ex 7 (reading the ratio convergence); Ex 12 (the repair loop's termination is an induction on a monotone template set) |
| **P5 Generating functions** | Encode a family's counts in one function and read them off | L2 — the parent pattern: analytic combinatorics is P5 grown into a whole discipline |
| **P10 Averaging / expectation** | Some object beats the average | L1 (balanced supersaturation — the container algorithm's required input, an averaging statement); L3 (the flag calculus is systematic Cauchy–Schwarz; the spectral receipt tr(A³)² ≤ tr(A²)³) |
| **P11 Explicit construction** | Build the object and check it | L4 (absorbing structures are *built*, not repaired into existence); L6 (the blob-growth strategy, B's half of the grid game) |
| **P12 Random construction** | Prove existence by sampling | L4 (the random greedy packing and its leftovers); L5 (the randomized half of randomized algebraic construction) |
| **P1 Sign-reversing involution (partial)** | Pair things up; survivors carry information | L6 (φ, the fixed-point-free edge-matching — the census grades it P1 PARTIAL: it pairs without summing signs); Ex 5 |
| **P25 Reduction / encoding** | Translate the problem; the target structure carries the proof | L6 (the digit-string game IS a graph game in disguise — P25 GENUINE at Putnam 2025 A3); L1 (a container is an encoding: a small certificate standing for many sets) |
| **P41 Divisibility (cameo)** | Necessary arithmetic conditions shape what can exist | L4 (the STS receipts: leftovers are multiples of 3, uncovered degrees even — divisibility and parity governing the repair landscape); ◆15 |
| **— the game-strategy cluster (no Atlas P-ID)** | Pairing, adaptive adversary, state partition: named devices of contest mathematics | L6 — the survey's honest finding: three contest canons, one datum each, engines outside the pattern index; adopted here by the container-method precedent |

---
## Lecture 1 · The Container Method: Counting Without Listing

**Encounter.** Call a set A ⊆ [n] **sum-free** if no two of its elements add to a third: x + y ∉ A for all x, y ∈ A. Two families come for free. All the odd numbers: odd + odd = even, never odd. All the large numbers, everything above n/2: two of them add past n. Each family lives in a space of 2^{⌈n/2⌉} subsets, so there are at least 2^{⌈n/2⌉} sum-free sets — but how many are there in total? Cameron and Erdős conjectured (1990) that the answer stays at that scale: the number of sum-free subsets of [n] is O(2^{n/2}) — no more than constant times the odd numbers alone. The conjecture's pull is structural: it says the two trivial families somehow *explain* almost everything, that a sum-free set is not an arbitrary scatter but a thin variation on one of two themes.

Why is this hard? Because counting means understanding, and there are 2^n subsets to understand. What you would love is a *fingerprint*: a small piece of information that pins each sum-free set down, so that counting fingerprints plus counting what a fingerprint allows does the whole job. The container method is that fingerprinting discipline, grown into a general machine.

**✎ Checkpoint.** Suppose you had to file all 94,498 nonempty sum-free subsets of [26] into boxes, where each box is *described* by a small key and *contains* only sets the key allows. What is the smallest key you could reach for? Before reading on, guess both the key and what could possibly keep the boxes small. (The lab runs this exact toy below, and the honest answer is not the one a first guess wants.)

**Experiment — the lab first (Part 1, deterministic).** The receipts, three panels.

*Panel 1: the count.* SF(n) for n = 4..34, by exhaustive depth-first search over sum-free sets (every leaf of the search tree is a sum-free set, and the search is the enumeration — no O(N²) materialization, the search tree itself is the census). The honest scale reading, straight from the receipts:

| n | SF(n) | SF/2^⌈n/2⌉ | fmax(n) | log₂fmax/n |
|----|--------|-----------|---------|------------|
| 4 | 9 | 2.2500 | 4 | 0.5000 |
| 8 | 61 | 3.8125 | 13 | 0.4626 |
| 12 | 369 | 5.7656 | 37 | 0.4341 |
| 16 | 1954 | 7.6328 | 118 | 0.4302 |
| 20 | 9583 | 9.3584 | 359 | 0.4244 |
| 24 | 45417 | 11.0881 | 1043 | 0.4178 |
| 26 | 94499 | 11.5355 | 1765 | 0.4148 |
| 28 | 200768 | 12.2539 | 3064 | 0.4136 |
| 30 | 415543 | 12.6814 | 5017 | 0.4098 |
| 34 | 1739022 | 13.2677 | 14007 | 0.4051 |

(The full 16-row table is in the lab.) SF/2^{⌈n/2⌉} grows — 2.25 to 13.27 — but *decelerating* (the increments over n = 26..34 are 0.72, 0.43, 0.29, 0.30), consistent with the Cameron–Erdős O(2^{n/2}) scale, with the constant honestly not pinned at lab scale. The maximal count fmax(n) tells the BLST story: log₂fmax/n decreases monotonically 0.4302 → 0.4051 over n = 16..34 and fits 1/4 + 0.79/log₂n (at n = 34 the fit reads 0.4051 against the measured 0.4051) — the 2^{(1/4+o(1))n} scale of the sharp theorem, visible at lab scale *as a drift*, not a flat constant. An honest display: the lab sees the polylogarithmic correction, not the limit.

*Panel 2: the dichotomy datum.* For each sum-free A ⊆ [26] (94,498 nonempty ones), compute min(s, v) — the smaller of "how many small elements (≤ n/2)" and "how many even elements." Histogram: min = 0: 16,319 (17.27%); 1: 26,925 (cum 45.76%); 2: 29,787 (cum 77.28%); 3: 17,833 (cum 96.15%); 4: 3,493; 5: 141 (cum 100.00%); ≥ 6: zero. **Three quarters of all sum-free sets are within two elements of the all-odd or all-large theme** — the conjecture's structural intuition, as a machine-checked histogram. The pure theme sets: 8,191 pure all-odd, 8,191 pure all-large, 63 in both (the odd numbers above 13: exactly the six elements {15,17,19,21,23,25}, so 2⁶ − 1 nonempty — Exercise 10 makes you reconcile this with the receipt). And Exploration 17 pushes to n = 30 and finds the tail *thickening*: the maximum min(s,v) grows from 5 (141 sets at n = 26) to 6 (52 sets) — no hard cap, a slowly spreading tail. Both readings are receipts, and both are printed.

*Panel 3: the container toy, honest.* Take the smallest honest fingerprint: the prefix key A ∩ [1..7] — 128 possible keys, filing every sum-free set of [26] by its first-seven elements. Receipts: 42 nonempty containers; mean size 2,249.98; and the box that hurts: the *empty prefix* container holds 30,645 of the 94,499 sets — **32.4%** of everything in one box (top five: 30645, 4779, 4756, 4631, 4262). The prefix key alone does NOT make containers small. A fingerprint with no size control is just a filing cabinet with one bulging drawer.

**Conjecture.** So what does the real method add? A container must do two jobs at once: *describe* many objects (few containers) and *constrain* them (each container small and sparse). The insight the real theorems build on: an object family with a supersaturation property — every medium-sized piece of the ground set *extends* to a forbidden configuration — forces any container holding many objects to be structurally sparse, and the sparsity caps how much the container can hold; the fingerprint's fewness comes from the same property. The container method's bargain: give me supersaturation, and I will give you a census without a listing.

**Explain — the theorem, stated at flag level.** The general machine arrived twice in 2015, independently: Balogh–Morris–Samotij ("Independent sets in hypergraphs", J. Amer. Math. Soc. 28(3) 669–709) and Saxton–Thomason ("Hypergraph containers", Invent. math. 201 (2015) 925–992 — a venue pin that corrects a common misattribution to JEMS, recorded in this Atlas's canon pins). The shape, in one honest sentence (the proofs are long and are cited, not reproduced):

> **(Containers, flag level.)** For a suitable hypergraph H — small codegrees, and supersaturation: every small vertex subset extends to an edge — the independent sets of H are contained in a small family of *containers*, each determined by a short certificate, with each container itself nearly independent. The number of containers is roughly 2^{εv} for an ε you may choose small; counting independent sets then reduces to counting containers and, inside each, a thin arithmetic allowance.

Read it against the toy: the prefix key is the *certificate* idea, and the missing input is supersaturation — the toy filed sets but never forced the big drawer to be sparse. In the real applications the deep work is the supersaturation input. For sum-free sets the modern sharp line is arithmetic: Green solved the Cameron–Erdős conjecture by *discrete Fourier analysis* (not containers — Bull. London Math. Soc. 36(6) 2004 769–778, a contrasting-engine datum the survey recorded deliberately), and Balogh–Liu–Sharifzadeh–Treglown closed the maximal question sharply — fmax(n) = (C_i + o(1))·2^{n/4} — via Green's arithmetic container lemma (J. Eur. Math. Soc. 20(8) 2018 1885–1911, with the Proc. Amer. Math. Soc. 143(11) 4713–4721 companion whose Lemma 2.1 is explicitly derivable from the general hypergraph theorems: the two faces of the method — arithmetic and hypergraph — in one two-paper unit).

**The origin story, with its honest label.** The general theorems of 2015 had an implicit ancestor thirty-three years earlier: Kleitman–Winston, "On the number of graphs without 4-cycles" (Discrete Math. 41(2) 1982 167–172 — the venue corrected by the survey's gather from a wrong seed; every C4-free graph sealed into a small family via a bounded degree-ordered certificate, 2^{O(ex(n,C4))} of them). The attribution is the surveys' own — Samotij's expository bridge ("Counting independent sets in graphs", European J. Combin. 48 2015 5–18, a self-described short survey presenting the Kleitman–Winston/Sapozhenko algorithm with derived bounds) writes that the method was "first employed more than three decades ago by Kleitman and Winston," and the ICM-level surveys say "introduced (implicitly)." Between the ancestor and the general theorems sits Sapozhenko's independent line (independent sets in regular graphs, the Russian tradition, uncorpus'd by the survey — recorded here as survey-level attribution). Then the flagship applications: Morris–Saxton, "The number of C_{2l}-free graphs" (Adv. Math. 298 2016 534–580) — Erdős's even-cycle counting conjecture confirmed for the whole family, via the general containers *plus a new balanced supersaturation theorem* (supersaturation refined to a roughly uniformly spread subcollection: the averaging engine P10 modernized into the exact input form the container algorithm needs — the survey graded it P10 genuine). The pattern's arc, receipt-grade at every station: the implicit origin (1982) → the general theorems (2015) → the bridge (2015) → the flagships (2016, 2018).

**Generalize — and the honest usage ledger.** The survey record's verdict on the container method is the template for this whole chapter, so read it carefully. In the planned corpus the method *fired* — twice, genuinely, in its two origin papers — and was **demoted anyway**: B7 and B8 sit in a single batch, and "the letter of the two-batch gate governs." The external-evidence recommendation followed ("a modern field workhorse and deserves an Atlas home on external evidence"), and the extension batch P (the ancestor, the bridge, and both flagships) then crossed the gate in-survey, superseding the external-only route. Adopted here per the survey's recommendation 4. What the ledger teaches: a method can be field practice of the first rank and still be *countable* — the census discipline does not rank methods by fame; it records where they fired and when the gate crossed. The container method is the precedent the other five lectures cite.

**What to learn:** the container method converts "count every object" into "count few certificates, then thin arithmetic inside each" — and the fewness is never free. The certificate idea is visible at toy scale (the prefix key); the size control is the supersaturation input the real theorems pay for, and the toy's bulging drawer (32.4% in one box) is the receipt that proves the point.

---

## Lecture 2 · Analytic Combinatorics: The Asymptotics Machine

**Encounter.** The Catalan numbers are the most counted sequence in combinatorics — C_n = 1/(n+1)·binom(2n,n): the triangulations, the balanced parentheses, the binary trees. Ask the working question: *how big is C_n?* The exact formula is a closed book; the shape is what a combinatorialist needs: 4^n divided by a polynomial. The discipline that answers such questions mechanically is analytic combinatorics, and its whole philosophy fits in one sentence: **a generating function is a function — its coefficients' asymptotics are governed by its singularities.** The book of the discipline is Flajolet–Sedgewick, *Analytic Combinatorics* (Cambridge University Press, 2009). The discipline's proof engine, the transfer theorems, is Flajolet–Odlyzko 1990 (SIAM J. Discrete Math. 3(2) 216–240); its pre-history toolbox is Bender 1974 (SIAM Rev. 16(4) 485–515).

The move, stated at flag level: if F(z) = Σ f_n z^n has nonnegative coefficients and near its dominant singularity ρ behaves like F(z) ~ C·(1 − z/ρ)^{−α}, then f_n ~ C·ρ^{−n}·n^{α−1}/Γ(α). The singularity's *type* (a square root, a logarithm, a pole) dictates the polynomial correction; the location dictates the exponential. Read C(z) = 1 + zC(z)²: the discriminant 1 − 4z says the singularity is at ρ = 1/4 and is a square root, so C_n lives at 4^n/n^{3/2}. The entire lecture is what the machine does to four classical families — and the receipts discipline what the chapter is allowed to claim.

**✎ Checkpoint.** Before the table: the normalized ratio r_n = C_n/(4^n/(√π·n^{3/2})) approaches 1 as n → ∞ — from which side, and at what rate in 1/n? The leading relative correction term is a rational multiple of 1/n; commit to a guess for its sign and order before reading on. (The lab answers to ten digits.)

**Experiment (Part 2, deterministic, exact arithmetic).** Four families, four singularity shapes, and every ratio a receipt computed in exact integer arithmetic (the printed Python uses native big integers; the receipts' ten-digit ratios are scaled-big-integer quotients — C₁₀₂₄ overflows IEEE doubles a hundred times over, and the lab does not fake its way past that).

*(a) Catalan, the square root.* r_n = C_n / (4^n/(√π·n^{3/2})):

| n | r_n | n(1−r_n) |
|---|-----|----------|
| 2 | 0.6266570687 | 0.7467 |
| 16 | 0.9338533633 | 1.0583 |
| 64 | 0.9826942040 | 1.1076 |
| 256 | 0.9956226871 | 1.1206 |
| 1024 | 0.9989024465 | 1.1239 |

n(1−r_n) → 1.125 = **9/8** — the first correction term 9/(8n), confirmed to three-plus digits from below. *(b) Central binomial, the same square root, one power lower:* s_n = binom(2n,n)/(4^n/√(πn)) → 1 with n(1−s_n) → 0.125 = **1/8** (receipts: 0.9399856030 at n = 2 … 0.9998779371 at n = 1024, last product 0.124992). *(c) Harmonic numbers, the logarithm:* H_n vs ln n + γ + 1/(2n) — n²·(residual) → **−0.083333 = −1/12** (receipts: −0.082827 at n = 4, −0.083301 at 16, −0.083331 at 64, −0.083333 at both 256 and 1024): the Euler–Maclaurin correction, machine-confirmed to six digits. *(d) Otter's trees, the square root of a logarithm:* rooted trees r_n via the divisor recurrence s_k = Σ_{d|k} d·r_d and r_n = (1/(n−1))·Σ s_k·r_{n−k} (divisions exact); unrooted trees t_n via Otter's dissimilarity identity T(z) = R(z) − (R(z)² − R(z²))/2, verified digit-by-digit: t_1..t_16 = 1, 1, 1, 2, 3, 6, 11, 23, 47, 106, 235, 551, 1301, 3159, 7741, 19320. Then the ratio t_n/t_{n−1}: 2.090909091 (n = 8), 2.495801576 (16), 2.726757988 (32), 2.840912744 (64), 2.898199479 (128), 2.926942754 (256) — converging to Otter's constant α = 2.95576528… (Otter, "The number of trees", Ann. of Math. 49(3) 1948 583–599), honestly slowly: the correction is 1/n-scale, and the receipts show it. And the constant itself: C_n = t_n·n^{5/2}/α^n = 0.7146498 (8), 0.5828919 (16), 0.5529941 (32), 0.5431738 (64), 0.5388940 (128), 0.5368831 (256) — the n^{−5/2} scale confirmed, with a constant still converging at n = 256 (toward the textbook value ≈ 0.535; cited, not re-derived — the receipts do not pin it, and neither does the prose).

**Explain — why the machine works, and where the receipts stop it from lying.** The four panels are the four shapes in the transfer-theorem zoo: (1 − z/ρ)^{−1/2} twice (the Catalan and binomial square roots — differing only in the subexponential power), the logarithm (harmonic numbers: the singularity is a log, the corrections are the Euler–Maclaurin constants), and the tree function's square-root-of-log — the hardest classical singularity, and the reason Otter's 1948 paper is the discipline's first triumph (the ratio's slow 1/n convergence is *the* receipt that the next correction term is large: the machine is honest about its own error terms, and so is this chapter). The discipline's deeper faces, each a paper in the survey's batch Q: the Mellin transform (Flajolet–Gourdon–Dumas, "Mellin transforms and asymptotics: harmonic sums", Theoret. Comput. Sci. 144(1–2) 1995 3–58) and de-Poissonization (Jacquet–Szpankowski, "Analytical de-Poissonization and its applications", Theoret. Comput. Sci. 201(1–2) 1998 1–62) — three faces in one batch: singularity analysis, Mellin, Poissonization; and the flagship application face, the kernel method for lattice paths (Banderier–Flajolet, "Basic analytic combinatorics of directed lattice paths", Theoret. Comput. Sci. 281(1–2) 2002 37–80). The survey recorded the three-faces datum as a structural finding: the method is one discipline, but its faces are separable engines.

**Generalize — counting without exact formulas.** The parent pattern is P5 (generating functions); the method is what P5 becomes when you stop asking for closed forms and start asking for *shapes*. The practical cycle the receipts model: (1) derive the functional equation; (2) locate the dominant singularity (for the Catalan equation, the discriminant; for trees, the radius where z = 1/R — a fixed point); (3) apply the transfer theorem at flag level; (4) *verify numerically at a scale where exact arithmetic is possible* — and read the correction terms as receipts. Step (4) is the Atlas's addition, and it bit twice in this lab's own design history: the first pass's float arithmetic died at C₁₀₂₄ (overflow — fixed with scaled big-integer quotients) and Otter's divisor sum was first computed with the divisor d = k missing (the recurrence is s_k = Σ_{d|k} d·r_d *including* k, so s_n can only be completed after r_n lands — the ordering is part of the receipts, recorded in the Verification Notes).

**The usage ledger, honestly.** The survey demoted analytic combinatorics in the planned corpus: three firings — Otter's classic among them — all inside a single batch; the cross-batch test "cannot be satisfied in-corpus." The external-canon recommendation followed (Flajolet–Sedgewick), with P5 named as the parent; the extension batch Q (the toolbox pre-history, the transfer-theorem origin, the Mellin and de-Poissonization faces, the lattice-path flagship) crossed the two-batch gate in-survey, with zero seed corrections — the cleanest gather of the survey record. Adopted here per recommendation 4, as a named method on top of its parent pattern.

**What to learn:** asymptotics are a *reading* skill — read the singularity, and the polynomial correction follows; but every printed digit must survive a receipts check, and the correction terms (9/(8n), 1/(8n), −1/(12n²), Otter's slow ratio) are where the honesty lives. A wrong asymptotic can agree with the data for fifty values; the lab's job is to make it confess early.

---
## Lecture 3 · Flag Algebras: The Extremal Lower-Bound Machine

**Encounter.** Mantel's theorem — a triangle-free graph on n vertices has at most ⌊n²/4⌋ edges — is where extremal graph theory starts, and Chapter 3's Ramsey scandal (R(3,3) = 6) is its shadow side. The lab opens by re-verifying the baseline exhaustively (Part 3): on n = 4, 5, 6 vertices, over *all* 64, 1024, 32768 graphs, the maximum triangle-free edge counts are exactly 4, 6, 9 = ⌊n²/4⌋, achieved by 3, 10, 10 labeled copies of K_{2,2}, K_{2,3}, K_{3,3}. So far, a sanity check. The modern question runs the other way: if a graph *must* contain triangles — its edge density is above 1/2, say — *how few* can it contain? Turán's construction gives one answer; the truth needed a machine.

The person who built the machine is Alexander Razborov, and the framework's home is a surprise the canon pins correct: **"Flag algebras", J. Symbolic Logic 72(4) (2007) 1239–1282** — a logic journal, a fact this Atlas's pin explicitly recorded because the framework paper is routinely misattributed to a combinatorics journal. The idea in one sentence: densities of substructures (triangles, paths, stars — "flags") satisfy *all* the inequalities that averaging forces, systematically; a computer can search that inequality system for the strongest consequence, and the consequence is a proof. Every application of Cauchy–Schwarz in an extremal paper is one point in a space the flag calculus parameterizes *all* of.

**Experiment — the minuscule version, exhaustively (Part 3, deterministic).** What the flag calculus would impose, the lab verifies by brute force at n ≤ 6, over every graph:

- **MANTEL:** max edges among triangle-free graphs = ⌊n²/4⌋ exactly, at all three sizes (achievers 3/10/10 — the complete bipartite balance).
- **DENSITY:** the inequality tr(A³)² ≤ tr(A²)³ — the spectral shadow of "triangle density cannot beat edge density to the 3/2" — has **0 violations** in all 2^{15} graphs at n = 6 (and all smaller sizes), with equality achieved *only by the empty graph* (1 equality each size). This is the flag calculus's raw material witnessed at census scale: an inequality that holds everywhere, tightly only in degeneracy.
- **PENTAGONS:** the maximum number of C5's in a triangle-free graph: 0 (n = 4), **1 = (5/5)⁵** (n = 5 — the only triangle-free graph on 5 vertices containing a C5 is C5 itself: any chord closes a triangle; 12 labeled achievers = 5!/10, and the total C5 count over *all* triangle-free 5-vertex graphs is 12), and **2 ≤ (6/5)⁵ = 2.48832** (n = 6, with 180 labeled achievers, hand-identified in the receipts as the (2,1,1,1,1)-blowups of C5: Aut order 4, so 720/4 = 180). The (n/5)⁵ shape is no accident — it is the leading form of a theorem this lecture culminates in.
- The counting device underneath: **#C5 = tr(A⁵)/10** in triangle-free graphs (a closed 5-walk's edge multiset must contain an odd cycle; C3 is excluded, so each C5 contributes exactly its 10 rooted directed walks) — divisibility by 10 machine-checked on every triangle-free graph in the census.

**✎ Checkpoint.** Here is the exercise the machinery exists for: prove tr(A³)² ≤ tr(A²)³ for every graph, and find every equality case, *before* looking at Exercise 11's worked answer. (Hint only: eigenvalues; the receipts say the empty graph is the only equality at n ≤ 6, and the lab checked all 33,856 graphs.)

**Explain — the calculus, honestly scaffolded.** The framework, at flag level with its load-bearing steps named: (1) fix a type (a small rooted graph); the "flags" are its extensions; (2) the flag algebra's products make averaging statements into algebra — a Cauchy–Schwarz that would appear in a paper as one line becomes a *family* of inequalities indexed by how you average; (3) the extremal problem becomes a semidefinite program over that inequality family; (4) the computer solves the SDP and returns coefficients; (5) a human-readable proof is extracted — Razborov's own triangle paper does exactly this. The survey's census graded the framework firing (M3) and the triangle-density landmark (M4) — both inside one batch, so the cross-batch gate could not be tested in-corpus; the external descendants decided, and they are strong:

- **Razborov, "On the minimal density of triangles in graphs", Combin. Probab. Comput. 17(4) (2008) 603–618** — the r = 3 case of the clique density problem: the exact minimum triangle density at every edge density, an explicit piecewise function. (Another venue pin this Atlas recorded against a common misattribution to Annals.)
- **Reiher, "The clique density theorem", Ann. of Math. 184(3) 683–707** — the full conjecture for all r, the flagship descendant whose weight carried the survey's recommendation.
- **Grzesik, "On the maximum number of five-cycles in a triangle-free graph", J. Combin. Theory Ser. B 102(5) 1061–1066** — the pentagons line, the theorem the lab's PENTAGONS panel rehearses at toy scale: the maximum is the balanced blowup of C5, (n/5)⁵ at the divisible sizes; the companion (Hatami–Hatami–Hladký–Kráľ–Norine–Razborov, J. Combin. Theory Ser. A 120(3) 722–732) landed four days apart on the arXiv — an independent-arrival datum the survey logged.
- **Hatami–Norine, "On the decidability of the theory of the reals with a generic predicate and flag algebras", J. Amer. Math. Soc. 24(2) 547–565** — the boundary result: the *whole* flag-algebra consequence problem is undecidable; with **Zhao's companion (SIAM J. Discrete Math. 25(2) 660–680)**. The survey's structural contrast, recorded for teaching: the *practical* fragment — sum-of-squares and SDP searches over bounded, human-chosen inequality families — is exactly the computable island the field lives on; the undecidability is the ocean around it. (The R2 gather itself carried a logged seed-swap: a conflated Hatami–Hatami row resolved at gather — recorded, never silent.)
- The pre-history node: homomorphism counting (Borgs–Chayes–Lovász–Sós–Vesztergombi, the Springer AoC 26 chapter (2006) 315–371) — flag densities are homomorphism densities renormalized; the survey filed it as the framework's ancestry.

**Generalize — why a calculus beats a lemma.** A lemma proves one inequality; a calculus *generates* them, and the computer searches the space for the binding ones. The trade, stated honestly: the proofs the machine returns are long coefficient lists whose *shape* is meaningful (which flags enter, which terms cancel) but whose *verification* is bookkeeping — exactly the kind of statement the Atlas's receipts discipline was built for. What the human still owns: the choice of types (which flags to average over), the conjecture, and the reading of the equality cases. The lab's minuscule census is the method in miniature — a space of objects exhaustively searched, an inequality holding everywhere with equality exactly at the degenerate point, and a sharp construction (the blowups) identified as the extremizer.

**What to learn:** when an extremal problem's answer is an *inequality with an optimizer* (a density question), the flag calculus is the assembly line for the lower bound; the SDP is the search; the equality case is still yours to imagine. And the boundary result is part of the method's honest spec: outside the practical fragment, the theory is undecidable — a named method with a *proven* limit.

---

## Lecture 4 · Absorption: From Almost to Exact

**Encounter.** A Steiner triple system covers every pair exactly once; Kirkman's 1847 existence theory (textbook canon: v ≡ 1, 3 mod 6) tells us exact covering is delicate. Now the modern question: prove that a *given, uncooperative* host — a random graph, a typical large structure — decomposes *exactly* into copies of your target. The probabilistic toolbox (Chapter 13) has an easy first half: the nibble, the semi-random method, covers all but a vanishing fraction. And then you are stuck with leftovers — a handful of uncovered pairs that are mutually incompatible, precisely because they are what randomness left over. Post-hoc, they cannot be repaired locally. **Absorption is the discipline of planning the cleanup before the mess exists**: build a small auxiliary structure first — an *absorber* — designed so that it can trade its own triples against *any* small leftover, then run the approximate phase, then let the absorber swallow what remains.

The lab makes the honest point with a toy (Part 4, seed 20261090): on the F₂⁴ STS(15) template — 35 triples {x, y, x ⊕ y} covering all 105 pairs exactly once — a random greedy packing (draw an uncovered pair, draw a valid third point, ≤ 20 draw attempts then a deterministic fallback, one continuous engine over 200 trials) leaves leftovers of 9, 12, 15, 18, 21, 24, 27 pairs (histogram 9:9, 12:24, 15:61, 18:73, 21:22, 24:10, 27:1; mean 29.455 triples packed). The leftovers are orderly — always a multiple of 3 (105 ≡ 0 mod 3 and each packed triple covers exactly 3 — Exercise 6), every uncovered vertex degree even — but orderly is not *closed*. Then the receipt that teaches the lesson: the naive **template-fixpoint repair** (add the template's triple for each uncovered pair, delete packing triples that clash with what you added, iterate) *does* complete — 200/200 systems, every pair exactly once — but the price is brutal: mean sacrifice d = 27.185 of the mean 29.455 packed triples (**92.3% of the packing deleted**), the template taking over with mean 32.73 of the 35 final triples. And the minimal-sacrifice search — delete only d = 0, 1, or 2 greedy triples and close the remainder by *any* fresh triples via exact-cover search (node cap 30,000, cover routine unit-tested on the template, K4, C8, bowties, disjoint pairs) — fails **0/50 trials, zero cap hits**: with d ≤ 2 there is genuinely nothing, and the receipts say so without flinching.

**✎ Checkpoint.** Before the receipts' column: if the greedy leaves only 9–27 pairs, how many of the 29-ish packed triples would you guess a template repair must delete? Commit in ink. (The author's own hand-run guessed single digits; the machine printed a mean of 27.185. The receipts govern, and the guess is recorded here as wrong.)

**Explain — what the real methods do differently.** The toy's failure *is* the pedagogy: post-hoc repair is expensive because the absorber's job — closing *arbitrary* compatible leftovers — was never designed in. The named methods all plan:

- **Keevash's template-first construction** (designs I, arXiv:1401.3665 — accepted by Annals of Mathematics on 10 July 2026, a pin this Atlas records with its date) builds the algebraic template (Lecture 5) *first*, so the exact-covering structure exists before the random choices scatter; nothing is left to repair. The absorption face fires at this origin — the survey's single in-corpus firing, at the L8 node.
- **Glock–Kühn–Lo–Osthus, iterative absorption** (Mem. Amer. Math. Soc. 284(1406) 2023, 1–144 — the monograph combining the two arXiv manuscripts 1611.06827 and 1706.01800; the venue/year/published form was corrected by the survey's gather from a wrong seed): the Existence Conjecture's *second* proof, "purely probabilistic and combinatorial" in the citing literature's own framing — an iterated cascade of absorbers, each layer cleaning up what the previous layer could not. The pre-history the survey recorded at survey level: the method's introducing moves trace to Kühn–Osthus and coauthors in Hamilton-type decomposition work, before the designs application — the origin *firing* stays at Keevash's designs paper (the absorption face), with the lineage noted honestly.
- **Montgomery, distributive absorption** (Adv. Math. 356 2019, Article 106793): the method's random-graphs face — spanning trees embedded in G(n, C log n/n) via distributive reservoirs; the threshold confirmed at the anticipated optimal order (Kahn's conjecture), a P44-family datum the survey cross-noted.
- **Glock–Joos–Kim–Kühn–Osthus** ("Resolution of the Oberwolfach problem", J. Eur. Math. Soc. 23(8) 2021 2511–2547 — title and venue corrected at gather from a mis-seeded "existence of resolvable designs"): the decomposition-application flagship — Oberwolfach resolved for all large n, via approximate decomposition (the nibble) *then* an absorption procedure keyed on a very special case of Keevash's resolvable-designs framework.
- **Kwan** ("Almost all Steiner triple systems have perfect matchings", Proc. London Math. Soc. 121(5) 2020 1468–1495 — title, venue, and year all corrected at gather): the random-structure downstream — an absorbing structure with a flexible set in the proof, and the almost-all statement as existence-by-sampling at measure one (P12 genuine).

**Generalize — the shape of the method.** Absorption is the compositional trick that reconciles randomness with exactness: the random phase gets you *near* the target with probability 1 (P12), and the pre-built absorber converts *near* into *exact* deterministically (P11's spirit: the absorber is explicitly constructed). The divisibility cameo (P41) is not decoration: leftover sets must satisfy the necessary arithmetic conditions (v ≡ 1, 3 mod 6 for the whole system; the toy's multiples-of-3 and even-degree invariants are the same physics at packing scale) — the absorber can only swallow what arithmetic permits, and the receipts' leftover structure (Exercise 6) is exactly the admissibility boundary at toy scale. Cross-reference Chapter 17, where Keevash's Existence Conjecture and the n = 9 exhibit already live; this lecture's contribution is the *method* extracted, with its honest lab-scale price tag.

**The usage ledger.** The survey's watch verdict: absorption fired once in-corpus (the Keevash origin) — not promotable as a pattern on that evidence; recommended on the external line (the iterative-absorption monograph and the design-existence proofs it powers); the extension batch S then crossed the two-batch gate in-survey (batches L + S), with the family's faces plural and recorded: L8 the randomized-algebraic template, S1 the iterative cascade, S2 the distributive reservoirs, S3 the decomposition flagship, S4 the random-structure downstream — "the WATCH's shape line holds, the faces differ per engine." Adopted per recommendation 6.

**What to learn:** approximate-then-absorb, with the absorber built *first* and designed for the leftovers you can actually get; the toy's 92% sacrifice is the receipt for what happens when you skip the planning. When a proof's last lemma is a repair, the repair was a design decision that got deferred.

---

## Lecture 5 · Randomized Algebraic Construction: Templates From Algebra, Flexibility From Chance

**Encounter.** The 15 nonzero vectors of F₂⁴ carry a miracle: the triples {x, y, x ⊕ y} — for each pair, the third point that completes the line through the origin — form a Steiner triple system on 15 points. The lab verifies the miracle before doing anything with it (Part 5(a)): 35 triples, every one of the 105 pairs covered exactly once. This is PG(3,2), the projective geometry, arriving as a design for free — *algebra is exactness on rails*. But exactness on rails is also brittleness: one algebraic system, one shape. Keevash's Existence Conjecture needed designs inside *arbitrary* large hosts, where no algebra hands you the system. The engine he named — **randomized algebraic construction** (the designs I paper's own method name; arXiv:1401.3665, the Annals acceptance recorded above) — is the productive tension of this chapter: take an algebraic template for the exactness, randomize *over* it for the flexibility, and prove the randomized object still lands where the algebra promised.

**Experiment (Part 5, deterministic + seed 20261091).** The lab verifies the two halves at the scale where they can be verified whole:

- **The algebra half.** (b) A census over all 65,536 4×4 F₂ matrices: exactly **20,160 invertible** — and the column-counting formula explains the number completely: (16−1)(16−2)(16−4)(16−8) (Exercise 4). Each invertible M acts on the 15 points; the census machine-checks that **every one of the 20,160 preserves the triple system** (M(x ⊕ y) = Mx ⊕ My — the algebra *is* the design's symmetry), and all 20,160 induced permutations are distinct: at least 20,160 automorphisms exhibited, and the exact order 20,160 = |PGL(4,2)| is textbook canon (cited, not re-derived). This panel is the chapter's cleanest "algebraicity is checkable" receipt: the machine walked the whole group and the template never bent.
- **The randomized half — honestly bounded.** (c) A Fisher–Yates relabeling of the 15 points (seed 20261091, floor-rule draws, i from 15 down, one continuous engine, 10 permutations): all 10 image systems are valid STS(15)s (35 triples, 105 pairs once — 10/10). The receipts pin the honesty: a point bijection *trivially* preserves STS-ness — the panel verifies the bookkeeping, not a deep fact; the algebraicity is panel (b); and the *real* method's randomization — random functions and orderings over the template, the randomized embeddability machinery — is beyond lab scale. What the toy shows instead is the *division of labor*: the template guarantees the exact-covering skeleton, the randomness moves it into position.

**Explain — the method, at flag level.** The real construction (cited, not reproduced — its home is Chapter 17, which carries Keevash's theorem with the template machinery in full): build a template with the algebraic exactness (a "typical" copy of the design structure, distributed through the host), randomize the signs/orderings over it so it flexes to cover the host's local features, then run the absorption face (Lecture 4) on the remains. The survey's ledger: randomized algebraic construction fired once in-corpus (the L8 origin), like absorption; recommended on the external line — "the subspace-designs line reuses the engine outside the corpus" — and adopted per recommendation 6. The companion paper, designs II (arXiv:1802.05900 — the subset-sums-in-lattices framework, whose Baranyai-type generalizations carry the resolvable-designs results Lecture 4's Oberwolfach proof consumes as a special case), **remains a preprint per the author's own publication list, checked 2026-10-13** — recorded honestly: this Atlas cites it as the framework's second half, with its unpublished status pinned, not hidden.

**Generalize — when to reach for the engine.** The pattern to internalize: *randomness cannot create exact global structure, and algebra cannot adapt to local constraints — so spend algebra on the skeleton and randomness on the skin.* The lab's group census is the receipt that the skeleton holds its symmetry under every admissible transformation; the relabeling panel is the receipt that moving the skeleton does not break it. Between them they model, at toy scale, why the hybrid works. The failure mode is equally instructive and equally lab-scale: randomize *inside* the algebra (Part 4's greedy packing ignored the template and paid 92% to get back to it — the two randomized panels of this chapter are a matched pair, the unplanned packing and the planned template, and the receipts price the difference at 27.185 triples).

**What to learn:** when exactness is the requirement and randomness is the tool, do not randomize the structure — randomize the *placement* of a structure that is already exact. And verify the algebraicity the way the lab did: exhaustively, over the whole symmetry group, with the count checked against the column-counting formula.

---

## Lecture 6 · The Strategy Devices: Pairing, Adaptive Adversary, State Partition

**Encounter.** Three problems from three different contest traditions, three devices with no Atlas P-ID between them — the survey's honest finding that a whole cluster of decisive engines lives outside the pattern index, three contest canons with one datum each. This lecture installs the devices as named methods (the container-method precedent: adoption on evidence, with the census verdict printed), and the lab (Part 6) verifies each device's mechanism at toy scale — with two receipts where the machine overruled the author's hand analysis, kept on display.

**Device 1 — the pairing strategy (Putnam 2025 A3).** The problem: a token starts at 0^n in the cube {0,1,2}^n; Alice and Bob alternately move it (a move changes one digit by ±1, staying in range), never revisiting a vertex; the player first unable to move loses. Bob — the second player — wins, for every n. The device: *see the game as a graph game and hand the second player a perfect matching*. The encoding is the census's P25 GENUINE datum (the game-to-graph reading, the survey's third-most-fired pattern doing its usual work), and the matching is explicit: **φ = swap 1 ↔ 2 at the first nonzero coordinate.** Bob answers every Alice move to x by moving to φ(x). The lab (Part 6(a), deterministic) machine-verifies φ on the whole cube for n = 1..12: involutive ✓, fixed-point-free ✓, every {x, φ(x)} an edge (the pair differs by ±1 in exactly one digit — the certificate |y − x| = 3^i in the ternary reading) ✓ — 531,440 vertices at n = 12 — and then plays the game *exhaustively*: full minimax with memoization on (vertex, visited set): Bob wins at n = 1 (Alice loses; 2 memo states) and n = 2 (28 memo states), the matching's promise confirmed by search independent of the proof (Exercise 5 builds the invariant argument: after each Bob reply the visited set is a union of complete pairs, so Alice always faces a fresh pair and Bob always has his half of it). The census graded the involution face P1 PARTIAL — φ pairs vertices without summing signs; the pattern's dynamic face is Chapter 19's neighbor P25, and the pairing *device* is the named method. Kin recorded by the census: Putnam 2023 A6 (the permutation fixed-point reading, P25 genuine) and the copycat device (Putnam 2022 A5) — the pairing family's nearest contest relatives.

**Device 2 — the adaptive adversary (IMO 2024 P5 = shortlist C4).** The problem: a snail crosses a 2024 × 2023 grid in which 2022 monsters hide — one in each interior row, at most one per column; the snail moves only right and down, restarting after any hit; find the least number of attempts guaranteed to reach the far side. The answer is **3**, and the device is the *lazy adaptive adversary*: commit a row's monster at the first-reached cell of that row with a free column, as the snail arrives — two attempts always die (row 2, then row 3), and the three-attempt strategy threads the monsters' taken columns. The lab (Part 6(b), deterministic minimax + seed 20261092 for the naive panel) builds the honest monotone-route subgame — route = the non-decreasing column profile (a₁,…,a_{R−1}); the walk visits each row's span; the adversary commits lazily at a fresh row's entry if the column is free, *defers* if the column is already taken (a monster cannot share a column). Receipts, both toys: (R,C) = (4,3) minimum attempts **3** — [1,1,1] dies at row 2 col 1, [2,2,2] dies at row 3 col 2, [2,3,3] survives; (R,C) = (5,4) minimum **3** — [2,2,2,2] dies r2c2, [3,3,3,3] dies r3c3, and [1,1,2,2] **survives by entering fresh row 4 at column 2 — the very column monster 2 took: the lazy commit is impossible there, the monster stays deferred** (its legal placements, columns 1 and 4, machine-verified — an illusory win would be a win leaving a deferred monster with no legal home, and the lab checks for exactly that). And the receipt that keeps this lecture honest: the author's hand-prediction for (5,4) was **4** — wrong; the machine found the taken-column threading. The prediction is recorded in the scars, the receipts govern. Exploration 18 scales to (6,5): still 3, now a *double* deferral (rows 4 and 5 both deferred, each placeable at three columns). The naive-snail panel (seed 20261092, sequential conditional route draws, a fresh engine per toy) shows what unengineered play does against the lazy adversary: (4,3) dies r2c2 five times then r3c1; (5,4) dies r2c2, r3c4, r4c3, then r2c2 again and again — repeated deaths at known commits, the mechanism on display. The grand-scale relative, recorded at statement level only, engines unpinned: IMO 2021 C6, the hunter/rabbit game on the infinite grid — the cluster's grandest scale, cited as genre, never as route (the census's route-pinning discipline, kept here).

**Device 3 — state-partition blocking (USAJMO 2023 P4).** The problem: on an infinite grid, Blue claims 1 white square per turn, Red claims 2; Blue's score is the largest simple polygon of blue squares; the largest score Blue can *guarantee* is **4**. Both halves are devices. Blue's guarantee — *blob growth*: at each of the first four rounds at least one neighboring white square survives Red's two removals (neighbor-availability counting — the census graded it P9 PARTIAL); Red's obstruction — *state partition*: tile the grid into 2×2 states and answer each Blue move by claiming the two squares bordering Blue's pick across state lines, so no blue polygon ever spans two states (score capped at one state's four cells). The lab (Part 6(c), seeds 20261093/20261094) verifies both halves at full toy strength: (c1) 200 plays × 48 rounds on the 12×12 board (2×2 states, Red's strategy exact, Blue's moves drawn): **zero** cross-border blue-blue adjacencies in 9,600 rounds, zero Red shortfalls, and the maximum within-state blue component = **4** — Red's cap, machine-witnessed, exactly the contest answer; (c2) Blue's growth on the infinite grid (8-directional frontier; Blue claims one drawn frontier cell per round, Red claims two): **100/100 trials reach blob size 4 in exactly 4 rounds** (histogram 4:100, mean 4.00, failures 0) — Red's two removals per round can never fence a blob this small, the neighbor-availability counting at full strength. The census graded the row P9 PARTIAL + P11 PARTIAL with no P-ID for the strategy design itself — the third datum of the cluster.

**Explain — why these are named methods and not tricks.** Each device is a *reusable mechanism with a proof obligation*: the pairing must exhibit a fixed-point-free involutive edge-matching covering everything but the start; the adaptive adversary must commit lazily (never early) and must leave every deferred monster a legal home; the state partition must be locally exact (the answerer's claims must always be available). The lab's receipts are the proof obligations in executable form: φ's three properties checked on 531,440 vertices; the deferred-placement consistency check; the zero-violation, zero-shortfall census. What elevates them to methods: they *compose with problems* — the pairing answers any "second player wins" question shaped like a graph minus a start; the lazy adversary answers any hidden-information race where the hider's constraints (one per row, one per column) can be threaded; the state partition answers any "opponent spans too much" cap. The survey's recommendation 11 recorded exactly this: the game-strategy cluster as a named method on the three-canon datum, by the container-method precedent.

**Generalize — the honest boundary.** The strategy devices are the contest canon's contribution to the Atlas's method ledger, and their census rows are unusual: no genuine P-pattern firings (2025 A3's P25 is the encoding, not the device; USAJMO P4's P9 is a lemma inside the device; IMO 2024 P5 has no P-ID at all). The survey's recommendation 14 drew the general moral: the obstruction halves of contest extremal problems live disproportionately outside the pattern index — modular residues, pairing, blocking, chip-firing, max-plus — and the Atlas teaches them as methods, here and in the pattern sections where they fire. This lecture is that teaching, with the receipts the machine signed.

**What to learn:** when a problem says "guaranteed," someone owns a strategy — and strategies are checkable objects. Build the strategy explicit enough that a machine can try to break it (the minimax, the census, the consistency check), and let the receipts, not the intuition, decide whether it holds. Twice in this lecture's own lab the machine corrected the author. That is the discipline working.

---

## The Trick Bag (reference card)

| # | Tool | Statement | Watch out |
|---|------|-----------|-----------|
| 1 | Container method (BMS / Saxton–Thomason 2015) | Cover all independent sets by few small containers; count = containers × thin arithmetic | Fewness needs supersaturation — a bare prefix key leaves one box holding 32.4% (Part 1's toy) |
| 2 | Balanced supersaturation (Morris–Saxton 2016) | The averaging input the container algorithm needs: forbidden configurations spread roughly uniformly | It is a theorem, not an assumption — someone must prove it per problem |
| 3 | Transfer theorems (Flajolet–Odlyzko 1990) | F(z) ~ C(1−z/ρ)^{−α} ⇒ f_n ~ C·ρ^{−n}·n^{α−1}/Γ(α) | Corrections are receipts: 9/(8n), 1/(8n), −1/(12n²) all machine-confirmed (Part 2) |
| 4 | Otter's machinery (1948) | s_k = Σ_{d\|k} d·r_d; T(z) = R(z) − (R(z)² − R(z²))/2; t_n/t_{n−1} → α = 2.95576528… | Exact arithmetic only (big integers); the divisor d = n completes only after r_n lands; ratio converges at honest 1/n speed |
| 5 | Flag calculus (Razborov 2007) | Averaging inequalities among substructure densities, searched by SDP | The whole-space problem is undecidable (Hatami–Norine) — live on the SOS/SDP island |
| 6 | Spectral density | tr(A³)² ≤ tr(A²)³; equality only the empty graph (n ≤ 6 census) | Translations: T = tr(A³)/6, m = tr(A²)/2, #C5 = tr(A⁵)/10 in triangle-free graphs |
| 7 | Absorption (Keevash origin; GKLO iterative) | Approximate decomposition + a pre-built absorber ⇒ exact | Post-hoc repair costs 92.3% (Part 4); the absorber is built BEFORE the random phase |
| 8 | Randomized algebraic construction (Keevash designs I) | Algebraic template for exactness, randomized placement for flexibility | Algebraicity is checkable: the whole GL(4,2) census preserves the template (Part 5); designs II is still a preprint — cite with status |
| 9 | Pairing strategy (Putnam 2025 A3) | A fixed-point-free involutive edge-matching covering the graph minus the start wins for the second player | The matching must cover EVERYTHING but the start; the visited-set invariant is the proof (Ex 5) |
| 10 | Adaptive adversary (IMO 2024 P5) / state partition (USAJMO 2023 P4) | Commit lazily at first entry; defer at taken columns — or partition the board into states and cap the opponent's span | Verify deferred placements are legal (illusory wins); the adversary never commits early — early commits are throwable |

**Scars (recorded so you skip them).** (1) The container toy's bulging drawer: a fingerprint with no supersaturation input is not a container method — it is a filing cabinet (Part 1's honest 32.4%). (2) Float arithmetic past 2^1024: the asymptotics panels overflow IEEE-754 doubles at C₁₀₂₄; exact big-integer arithmetic with scaled quotients is the only honest way to print ten digits (Part 2). (3) The author's wrong snail prediction (4 vs. the machine's 3 at (R,C) = (5,4)): the taken-column threading is invisible to hand analysis that assumes fresh-row commits always fire — deferral is the mechanism, and the receipts govern (Part 6(b), scar on display in the Verification Notes). (4) Repair-as-method confusion: the 92.3% sacrifice receipt exists to be misread by nobody — completion is not absorption; planning is (Part 4). The full campaign record — seven design scars from the receipts pass, the post-compaction verification pass with its two re-implementation bugs caught and fixed, the seed corrections, and every pin level — is in the Verification Notes.

**Reading list (pin levels as verified this session).** Web-pinned 2026-10-14: Balogh–Morris–Samotij, J. Amer. Math. Soc. 28(3) 669–709; Saxton–Thomason, Invent. math. 201 925–992 (venue pin correcting a JEMS misattribution); Razborov, J. Symbolic Logic 72(4) 1239–1282 (correcting a JCTB misattribution); Razborov, Combin. Probab. Comput. 17(4) 603–618 (correcting an Annals misattribution); Otter, Ann. of Math. 49(3) 583–599; Green, Bull. London Math. Soc. 36(6) 769–778; Flajolet–Sedgewick, *Analytic Combinatorics*, Cambridge UP (2009). Survey-provenance (repo commit bec3ce15, fetched and web-verified at gather): Kleitman–Winston, Discrete Math. 41(2) 167–172 (venue corrected from seed); Samotij, European J. Combin. 48 5–18; Morris–Saxton, Adv. Math. 298 534–580; BLST, J. Eur. Math. Soc. 20(8) 1885–1911 + the PAMS 143(11) 4713–4721 companion; Flajolet–Odlyzko, SIAM J. Discrete Math. 3(2) 216–240; Bender, SIAM Rev. 16(4) 485–515; Banderier–Flajolet, Theoret. Comput. Sci. 281 37–80; Flajolet–Gourdon–Dumas, Theoret. Comput. Sci. 144 3–58; Jacquet–Szpankowski, Theoret. Comput. Sci. 201 1–62; Reiher, Ann. of Math. 184(3) 683–707; Hatami–Norine, J. Amer. Math. Soc. 24(2) 547–565 (seed-swap logged at gather); Zhao, SIAM J. Discrete Math. 25(2) 660–680; Grzesik, J. Combin. Theory Ser. B 102(5) 1061–1066; HHKNR companion, J. Combin. Theory Ser. A 120(3) 722–732; BCLSV, Springer AoC 26 (2006) 315–371; GKLO, Mem. Amer. Math. Soc. 284(1406) 1–144 (published form corrected from seed); Montgomery, Adv. Math. 356 106793; GJKKO, J. Eur. Math. Soc. 23(8) 2511–2547; Kwan, Proc. London Math. Soc. 121(5) 1468–1495. Ch. 17 canon reused (web-verified session 80): Keevash designs I arXiv:1401.3665 (accepted by Ann. of Math., 10 July 2026); designs II arXiv:1802.05900 (still a preprint, checked 2026-10-13); Rödl 1985. Contest statements (census provenance, chunk 29): Putnam 2025 A3 (routes pinned, MAA-permitted archive); IMO 2024 P5 = shortlist C4 (route pinned, official UK host booklet); USAJMO 2023 P4 (routes pinned, open author-version reports); IMO 2021 C6 (statement-level only, engines unpinned — genre, never route).

---
## Exercises (graded: ●○○ easy · ●●○ moderate · ●●● tough)

Hints travel with the problems. ◆ **pattern unknown** problems come with no hint — diagnosing the tool is part of the problem; ◐ **Explorations** state what you should find, not a number to match. Machine-verified answers sit at the end of the chapter.

### Easy (●○○)

**Exercise 1 · Maximality, by hand and by machine.** A sum-free A ⊆ [n] is maximal if no element e′ ∉ A can be added (staying sum-free). (a) Show {2,3} is a maximal sum-free subset of [6]. (b) The receipts count fmax(6) = 6, and the verification pass listed the six maximal sets: {2,3}, {1,3,5}, {3,4,5}, {1,4,6}, {2,5,6}, {4,5,6}. Verify two of the other five by hand, using the three addability conditions from the lab: e′ is addable iff (i) no x, y ∈ A have x + y = e′, (ii) 2e′ ∉ A, (iii) no x ∈ A has x + e′ ∈ A. (c) The brute-force cross-check at n ≤ 12 confirms SF(6) = 24: reconcile — the 24 includes the empty set, the 6 maximal sets among them, and both all-odd and all-large sets. *Hint: condition (i) is the one naive checks forget — e′ = x + y with both x, y in A.*

**Exercise 2 · Reading the Catalan receipts.** The lab prints r_n = C_n/(4^n/(√π n^{3/2})) rising from 0.6266570687 (n = 2) to 0.9989024465 (n = 1024), with n(1 − r_n) → 1.125. (a) Explain, from the transfer-theorem shape, why the correction is 1/n-scale (the singularity is a square root; each correction term of C(z) near ρ = 1/4 multiplies the asymptotic by 1 + O(1/n)). (b) Why must the ratios approach from *below* — i.e., why is n(1 − r_n) positive and decreasing toward 9/8? (c) Check the central binomial panel's parallel: n(1 − s_n) → 0.125, and explain why the two limits differ by a factor of exactly 9 (the square root's subexponential power differs by one; the leading constants differ by the √π normalization). *Hint: 9/8 vs 1/8 — the Catalan's extra n in the denominator is the whole difference.*

**Exercise 3 · Mantel and the pentagon at n = 5.** (a) From the receipts: the maximum edge count among triangle-free graphs on 6 vertices is 9 with 10 labeled achievers. Verify both halves by exhibiting K_{3,3} and counting its labelings: 6!/(3!·3!) = 20, halved because the two sides are unordered — 10. (b) The receipts say the total number of C5's over ALL triangle-free graphs on 5 vertices is exactly 12 — every one of them inside the 12 labeled copies of C5 itself. Prove the chord fact that forces this: the only triangle-free graph on 5 vertices containing a C5 is C5 itself. (c) Combine: why does this make "max C5 = (5/5)⁵ = 1" a two-line receipt at n = 5, while n = 6 needs the blowup analysis (max 2, 180 achievers)? *Hint for (b): a chord of a 5-cycle splits it into a triangle and a quadrilateral.*

### Moderate (●●○)

**Exercise 4 · Counting GL(4,2) by columns.** (a) Show the number of invertible 4×4 matrices over F₂ is (16 − 1)(16 − 2)(16 − 4)(16 − 8) = 20,160, by building the matrix column by column: the first column is any nonzero vector (15 choices), the second avoids the first's span (14 choices: 16 − 2), the third avoids the span of two (12: 16 − 4), the fourth avoids the span of three (8: 16 − 8). (b) The census receipt: exactly 20,160 of the 65,536 matrices are invertible — reconcile 65,536 = 2^{16}. (c) Generalize to GL(k, 2): ∏_{i=0}^{k−1}(2^k − 2^i), and check k = 3 gives 168 (Exploration 16's Fano census). *Hint: at each step the forbidden set is exactly the span of the columns already chosen.*

**Exercise 5 · Bob's invariant, proved.** The pairing map φ swaps 1 ↔ 2 at the first nonzero coordinate of x ∈ {0,1,2}^n ∖ {0^n}. (a) Prove φ is an involution (φ(φ(x)) = x) with no fixed points. (b) Prove every {x, φ(x)} is an edge of the game graph: exactly one digit changes, by exactly 1 (in the ternary reading, |φ(x) − x| = 3^i where i is the first nonzero coordinate). (c) Prove Bob's strategy — answer Alice's move to x with φ(x) — is winning: show by induction that after every Bob move, the visited set is a union of complete pairs, and conclude Alice always moves to a fresh vertex whose mate is also fresh, so Bob always has a legal reply and Alice eventually does not. (d) The receipts' minimax confirms at n = 1, 2 (Alice loses; 2 and 28 memo states): explain why the exhaustive search is even feasible — the memo key is (vertex, visited set), and count the states the search actually visits at n = 2. *Hint for (c): if x is fresh but φ(x) were visited, the pair {x, φ(x)} would already be complete — containing x.*

**Exercise 6 · The leftovers' arithmetic.** After the lab's greedy packing on the STS(15) template (105 pairs, triples of 3), the receipts record leftover pair counts that are always multiples of 3 (9, 12, 15, 18, 21, 24, 27 — never anything else), and every uncovered vertex has even uncovered degree. (a) Prove the multiples of 3: each packed triple covers exactly 3 pairs, and 105 ≡ 0 (mod 3), so the uncovered count is 105 − 3·(#packed). (b) Prove the even degrees: every packed triple through a vertex v consumes exactly 2 of v's uncovered pairs (the two other members of the triple), so v's uncovered degree drops by 0 or 2 at each step. (c) Why does (b) imply the leftover pairs form a union of cycles and doubled edges — structures the repair phase must handle — and why did the min-sacrifice search still fail 0/50? (Because *compatible closure* is the stronger requirement: the leftover pairs must decompose into triples, which even-degree structure does not guarantee — the receipts' honest answer.) *Hint: divisibility (P41's cameo) sets the *necessary* stage; existence of the decomposition is another matter.*

**Exercise 7 · Reading Otter's receipts.** The lab computes t_n exactly to n = 256 and prints t_n/t_{n−1} = 2.090909091 (n = 8), 2.726757988 (32), 2.898199479 (128), 2.926942754 (256), against Otter's constant α = 2.95576528…. (a) Show the convergence's honest speed: the residuals α − ratio are approximately proportional to 1/n across the printed range (compute the four products n·(α − ratio_n) and observe near-constancy). (b) The receipts print C_n = t_n·n^{5/2}/α^n = 0.7146498 (8) → 0.5368831 (256): explain why the convergence of C_n is *faster* than the ratio's (the n^{5/2} prefactor absorbs exactly the correction that makes the ratio slow). (c) Why does the lab's parity check — t_n integral, from the dissymilarity identity T(z) = R(z) − (R(z)² − R(z²))/2 — need exact arithmetic rather than floats? *Hint for (b): the ratio's next correction is 1/n-scale; folding 1/n corrections into the prefactor is what n^{5/2} does.*

**Exercise 8 · The blob's arithmetic.** In the grid game, Blue grows an 8-connected blob B ⊆ ℤ² — b₁ = (0,0) on round 1, then one unclaimed 8-directional frontier cell per round; Red claims two unclaimed frontier cells per round (the Part 6(c2) engine exactly). The receipts (Part 6(c2)): 100/100 trials reach blob size 4 in exactly 4 rounds. (a) Prove the neighbor-availability lemma at the relevant scale: for every 8-connected blob of size ≤ 3 on the infinite grid, the 8-directional frontier contains at least 5 cells — in fact |F(B)| ≥ 2|B| + 6 (check the cases: 1 cell — 8 neighbors; 2 adjacent cells — at least 10; 3 cells in a path or an L — at least 12). (b) Conclude: since Red removes at most 2 frontier cells per round, Blue can always grow on rounds 1–4 regardless of Red's play — the exactly-4-rounds receipt, proved. (c) The other half of the contest answer: explain how Red's state partition caps Blue's score at 4 *despite* the frontier argument — which assumption of the blob growth does the partition attack? (The frontier argument protects *growth*; the partition attacks *span*: Blue can fill one 2×2 state but never connect across states, so the largest simple polygon stays at 4.) *Hint for (a): cells of the blob itself do not count; only white neighbors.*

**Exercise 9 · The snail's two-attempt lower bound.** In the (5,4) subgame, prove the lazy adversary kills any two attempts. (a) Show attempt 1 dies: whatever route the snail walks, it enters row 2 at some cell; if column c is free the monster commits there and the snail dies at that entry (a monotone route cannot skip row 2's entry span); if c is taken — impossible on attempt 1 (nothing is committed yet). (b) Attempt 2 dies: the adversary still has every interior row except row 2 available with fresh columns; commit at the first entry of row 3 with a free column. (c) The receipts' three-attempt line for (5,4) is [2,2,2,2], [3,3,3,3], [1,1,2,2]: trace all three walks and verify the deferral mechanism — the third route enters fresh row 4 at column 2, monster 2's *taken* column, so the lazy commit cannot fire and the monster stays deferred with legal homes (columns 1 and 4, machine-checked). (d) State the lesson in one sentence: why does the adversary's laziness (never committing early) *create* the threading resource? *Hint: a committed monster costs the adversary a column forever; deferral preserves it.*

### Tough (●●●)

**Exercise 10 · The trivial families, counted exactly.** (a) Prove the odd numbers of [n] are sum-free, and so are all subsets of {⌊n/2⌋+1, …, n}: conclude SF(n) ≥ 2^{⌈n/2⌉} + 2^{⌈n/2⌉} − (overlap). (b) Count the overlap at n = 26: the all-odd ∩ all-large family is the subsets of the odd numbers above 13 — the six elements {15, 17, 19, 21, 23, 25} — so 2⁶ = 64 sets including the empty one; reconcile with the receipts' 63 nonempty. (c) The receipts' scale reading is SF(26) = 94,499 against the two families' 2^{13} + 2^{13} − 64 = 16,320: explain what the Cameron–Erdős conjecture claims about the ratio (it stays bounded by a constant as n → ∞), what the lab's drift (11.54 → 13.27 over n = 26..34) does and does not establish, and why the receipts refuse to print a bound. *Hint for (c): monotone-decelerating growth at lab scale is consistent with O(2^{n/2}) and with slow divergence — only the theorem (Green 2004) decides, and it is cited, not re-derived.*

**Exercise 11 · The spectral density inequality, completely.** Prove: for every graph with adjacency matrix A, **tr(A³)² ≤ tr(A²)³**, with equality characterization. (a) Let λ₁,…,λ_n be the eigenvalues, ρ = max|λᵢ|. Show tr(A³) = Σλᵢ³ ≤ Σ|λᵢ|³ ≤ ρ·Σλᵢ² = ρ·tr(A²). (b) Show ρ² ≤ tr(A²), and conclude tr(A³)² ≤ tr(A²)³. (c) Translate to graph language: T = tr(A³)/6 and m = tr(A²)/2 give 36T² ≤ 8m³, i.e., T ≤ (√2/3)·m^{3/2} — triangles are capped by edges to the 3/2. (d) Equality: trace through (a) and (b)'s inequalities to show equality forces every eigenvalue to have |λᵢ| ∈ {0, ρ} *and* all nonzero eigenvalues positive — and the trace of A (0 on the diagonal... careful: what does the diagonal of A³ count?) — reconcile with the receipts: at n = 4, 5, 6 the ONLY equality case in all 33,856 graphs is the empty graph. (e) Why is this inequality "flag algebra's raw material" (Lecture 3): it is an averaging statement about substructure densities — the calculus's systematic generalization of exactly this Cauchy–Schwarz shape. *Hint for (d): each step's equality condition, composed.*

**Exercise 12 · The repair loop, proved and priced.** The template-fixpoint repair (Part 4) iterates: add the template triple {a, b, a ⊕ b} for each currently uncovered pair; delete every packing triple sharing a pair (two or more points) with an added triple; repeat to fixpoint. (a) Termination in at most 35 rounds: show the set of template triples in use grows strictly monotone whenever the loop has not finished, and the template has only 35 triples. (b) The invariant: template triples pairwise share at most one point (they form an STS), so added triples never conflict with each other; and every pair stays covered at most once throughout — verify the deletion rule is exactly what preserves this. (c) The price, from the receipts: mean sacrifice d = 27.185 deleted packing triples against mean 29.455 packed, and mean |S| = 32.73 template triples in the final system — reconcile all three numbers (survivors = 29.455 − 27.185 = 2.27; added template = 35 − 2.27 = 32.73; the final system has exactly 35 triples), and explain why d ≈ 27 is the honest receipt for "post-hoc repair is not absorption." *Hint for (a): an uncovered pair always has a template triple; if that triple is already in use, the pair is covered — contradiction.*

### ◆ Pattern unknown (no hints — diagnosing the tool is the problem)

**◆ 13.** Alice and Bob play the digit-string game of Lecture 6 on {0,1,2}^n (token at 0^n, moves change one digit by ±1, no vertex revisited, the player unable to move loses; Alice moves first). Prove that Bob wins for every n ≥ 1.

**◆ 14.** Determine the maximum number of 5-cycles in a triangle-free graph on 6 vertices, and count the labeled extremal graphs. (The lab's receipts hold the answer; the diagnosis of how to find it is the problem.)

**◆ 15.** Prove that every Steiner triple system on v points contains exactly v(v−1)/6 triples. (Equivalently: an STS(v) exists only if v(v−1) is divisible by 6 — the divisibility necessity of Lecture 4, as a count.)

### ◐ Explorations (state what you should find)

**◐ 16 · The Fano sibling.** Drop to F₂³: the 7 nonzero vectors, triples {a, b, a ⊕ b} — the Fano plane STS(7), with 21 pairs. Census all 512 3×3 F₂ matrices for the analog of Part 5: you should find 168 = (8−1)(8−2)(8−4) invertible matrices, every one preserving the triple system, and 168 distinct induced permutations — the textbook order |PGL(3,2)| = 168, exhibited by exhaustive search.

**◐ 17 · The dichotomy at n = 30.** Rerun Part 1's min(s, v) histogram at n = 30 (415,542 nonempty sum-free sets). You should find the max growing from 5 to 6 — 52 sets with min(s, v) = 6 — with the cumulative share of min ≤ 2 falling to 70.32%. The honest finding to state: the dichotomy tail thickens slowly with n; there is no hard cap at 5, and the lab shows the drift rather than the limit.

**◐ 18 · The snail at (6,5).** Extend the monotone-route subgame to R = 6, C = 5. You should find the minimum still 3, with a winning line whose first two attempts die at r2c2 and r3c3 and whose third route survives with rows 4 AND 5 both deferred — a double taken-column threading, each deferred monster still having legal homes. State the pattern the three toys (4,3), (5,4), (6,5) jointly suggest, and the honest caveat (three data points are a suggestion, not a theorem — the contest's answer 3 holds at 2024×2023 scale by a different, case-split argument).

---
## Computational Lab (verified)

*Every run below uses the chapter's documented engine: the Lehmer/MINSTD generator x ← 48271·x mod (2³¹−1), and a uniform choice among m items is floor(nxt()·m/(2³¹−1)) — integer-exact in IEEE doubles throughout. Fresh engines start at seeds **20261090** (Part 4's greedy packing, one continuous stream over all 200 trials), **20261091** (Part 5's relabelings, one stream over the 10 permutations), **20261092** (Part 6's naive snail — a FRESH engine per toy), **20261093** (Part 6's grid-game census, one stream over the 200 plays), and **20261094** (Part 6's blob growth, one stream over the 100 trials). Parts 1, 2, 3, 5(a),(b) and Part 6(a),(b)'s minimaxes are deterministic — no draws. The printed Python reproduces every receipt value-for-value; a close-out pass re-verified the draw-dependent panels end-to-end against this receipts file before printing, re-pinning the two bookkeeping conventions the receipts now record (the minimax memo and the blob start). The engine's own bug history — seven design scars, two verification-pass scars, the two re-pinned conventions, and an assembly self-review that caught and fixed three printing defects in the code below before installation — is in the Verification Notes.*

### Part 1 — The sum-free censuses (Lecture 1)

Three deterministic panels: the SF/fmax table by depth-first enumeration (the search tree IS the census — every node a sum-free set, nothing O(N²) materialized), the brute-force cross-check at n ≤ 12, and the honest container toy.

```python
import math
def sum_free_sets(n):
    """Every sum-free subset of [n], exactly once. DFS over elements
    n..1: adding e (all current elements exceed e) is valid iff
    2e not in S and no x+e in S — the x+y=e case is impossible.
    The yield is at the LEAVES (e == 0): every leaf of the search
    tree is a sum-free set, and the search is the enumeration."""
    if n <= 0:
        yield frozenset()
        return
    def rec(e, S):
        if e == 0:
            yield S
            return
        yield from rec(e - 1, S)
        if 2 * e not in S and all(x + e not in S for x in S):
            yield from rec(e - 1, S | {e})
    yield from rec(n, frozenset())

def maximal(S, n):
    """No e' outside S addable — the three-condition test:
    (i) no x,y in S with x+y=e', (ii) 2e' not in S, (iii) no x+e' in S."""
    for e in range(1, n + 1):
        if e in S:
            continue
        if (2 * e not in S
                and all(x + e not in S for x in S)
                and not any(x + y == e for x in S for y in S)):
            return False
    return True

def brute_census(n):                      # independent check, all 2^n masks
    if n <= 0:
        return 1, 1
    sf = fmax = 0
    for mask in range(1 << n):
        S = frozenset(i + 1 for i in range(n) if mask >> i & 1)
        if all(x + y not in S for x in S for y in S):
            sf += 1
            if maximal(S, n):
                fmax += 1
    return sf, fmax

# cross-check, n = 1..12 — ALL MATCH:
#   SF:   2, 3, 6, 9, 16, 24, 42, 61, 108, 151, 253, 369
#   fmax: 1, 2, 2, 4,  5,  6,  8, 13,  17,  23,  29,  37
for n in range(1, 13):
    a = brute_census(n)
    b = (sum(1 for _ in sum_free_sets(n)),
         sum(1 for S in sum_free_sets(n) if maximal(S, n)))
    assert a == b, n

for n in range(4, 35, 2):                 # the SF/fmax table
    SF = FM = 0
    for S in sum_free_sets(n):
        SF += 1
        if maximal(S, n):
            FM += 1
    h = (n + 1) // 2
    print(n, SF, SF / 2**h, FM, FM / 2**(n/4), FM / 2**h, math.log2(FM) / n)

def dichotomy(n):                          # the min(s,v) histogram
    if n < 0:
        return [0], 0, 0, 0
    hist = [0] * (n + 2); pure_odd = pure_large = both = 0
    for S in sum_free_sets(n):
        if not S:
            continue
        s = sum(1 for x in S if 2 * x <= n)
        v = sum(1 for x in S if x % 2 == 0)
        hist[min(s, v)] += 1
        if all(x % 2 for x in S):
            pure_odd += 1
        if all(2 * x > n for x in S):
            pure_large += 1
            if all(x % 2 for x in S):
                both += 1
    return hist, pure_odd, pure_large, both

def container_toy(n=26, k=7):              # the honest prefix-key filing
    if n < 0 or not isinstance(k, int):
        return 0, 0, 0.0, 0.0, []
    boxes = {}
    for S in sum_free_sets(n):
        key = tuple(sorted(x for x in S if x <= k))
        boxes[key] = boxes.get(key, 0) + 1
    if not boxes:
        return 0, 0, 0.0, 0.0, []
    sizes = sorted(boxes.values(), reverse=True)
    return len(sizes), sizes[0], sizes[0] / sum(sizes), \
           sum(sizes) / len(sizes), sizes[:5]
print(container_toy(26, 7))
print(dichotomy(26)[0][:7], dichotomy(26)[1:])   # the receipts below
```

Receipts — the SF/fmax table (deterministic; SF counts include the empty set; fmax counts maximal sets; the ratios against the two trivial families and the 2^{n/4} scale):

| n | SF(n) | SF/2^⌈n/2⌉ | fmax(n) | fmax/2^(n/4) | fmax/2^⌈n/2⌉ | log₂fmax/n |
|----|--------|-----------|---------|-------------|---------------|------------|
| 4 | 9 | 2.2500 | 4 | 2.000 | 1.0000 | 0.5000 |
| 6 | 24 | 3.0000 | 6 | 2.121 | 0.7500 | 0.4308 |
| 8 | 61 | 3.8125 | 13 | 3.250 | 0.8125 | 0.4626 |
| 10 | 151 | 4.7188 | 23 | 4.066 | 0.7188 | 0.4524 |
| 12 | 369 | 5.7656 | 37 | 4.625 | 0.5781 | 0.4341 |
| 14 | 847 | 6.6172 | 66 | 5.834 | 0.5156 | 0.4317 |
| 16 | 1954 | 7.6328 | 118 | 7.375 | 0.4609 | 0.4302 |
| 18 | 4398 | 8.5898 | 201 | 8.883 | 0.3926 | 0.4251 |
| 20 | 9583 | 9.3584 | 359 | 11.219 | 0.3506 | 0.4244 |
| 22 | 20982 | 10.2451 | 598 | 13.214 | 0.2920 | 0.4193 |
| 24 | 45417 | 11.0881 | 1043 | 16.297 | 0.2546 | 0.4178 |
| 26 | 94499 | 11.5355 | 1765 | 19.501 | 0.2155 | 0.4148 |
| 28 | 200768 | 12.2539 | 3064 | 23.938 | 0.1870 | 0.4136 |
| 30 | 415543 | 12.6814 | 5017 | 27.715 | 0.1531 | 0.4098 |
| 32 | 849877 | 12.9681 | 8547 | 33.387 | 0.1304 | 0.4082 |
| 34 | 1739022 | 13.2677 | 14007 | 38.689 | 0.1069 | 0.4051 |

Receipts — the dichotomy datum (n = 26; 94,498 nonempty sum-free sets; s = #elements ≤ 13, v = #even elements): min(s,v) = 0: 16,319 (17.27%); 1: 26,925 (28.49%, cum 45.76%); 2: 29,787 (31.52%, cum 77.28%); 3: 17,833 (18.87%, cum 96.15%); 4: 3,493 (3.70%, cum 99.85%); 5: 141 (0.15%, cum 100.00%); ≥ 6: 0. Pure all-odd sets: 8,191; all-large: 8,191; both: 63.

Receipts — the container toy (n = 26, prefix key A ∩ [1..7], 128 possible keys): nonempty containers 42; sets filed 94,499 (empty set included, key = empty prefix); **max container 30,645 = 32.4% of everything in one box**; mean container size 2,249.98; top five 30645, 4779, 4756, 4631, 4262. The honest reading, printed as run: the prefix key alone does not make containers small — the empty-prefix drawer holds a third of the family, and the fewness the real method delivers must come from the supersaturation input the toy does not have.

### Part 2 — Four singularity shapes, exactly (Lecture 2)

Deterministic, exact arithmetic: big-integer recurrences with scaled quotients for the two square-root panels (C₁₀₂₄ overflows IEEE doubles — the ratios are computed as C_n·10⁴⁰/4ⁿ big-integer quotients, then floated), Kahan summation for the harmonic panel, and exact rational arithmetic (Python `Fraction`) for Otter's trees, with the integrality of every t_n asserted.

```python
import math
from fractions import Fraction
from math import comb

SQRT_PI = math.sqrt(math.pi)
GAMMA = 0.5772156649015329

def catalan_ratios():                       # (a) Catalan vs 4^n/(sqrt(pi) n^1.5)
    C = 1                                   # c_0; c_n = c_{n-1} 2(2n-1)/(n+1)
    for n in range(1, 1025):
        if n > 1:
            C = C * 2 * (2 * n - 1) // (n + 1)          # exact
        if n >= 2 and n & (n - 1) == 0:                 # n = 2,4,...,1024
            q = C * 10**40 // 4**n                     # scaled quotient
            r = q * SQRT_PI * n**1.5 / 10**40
            print(n, f"{r:.10f}", f"{n * (1 - r):.6f}")

def binomial_ratios():                      # (b) binom(2n,n) vs 4^n/sqrt(pi n)
    for n in (2, 4, 8, 16, 32, 64, 128, 256, 512, 1024):
        q = comb(2 * n, n) * 10**40 // 4**n
        s = q * SQRT_PI * math.sqrt(n) / 10**40
        print(n, f"{s:.10f}", f"{n * (1 - s):.6f}")

def kahan(n):                               # (c) harmonic, compensated
    if n <= 0:
        return 0.0
    s = c = 0.0
    for k in range(1, n + 1):
        y = 1.0 / k - c
        t = s + y
        c = (t - s) - y
        s = t
    return s

catalan_ratios()                           # panels (a) and (b) printed
binomial_ratios()
for n in (4, 16, 64, 256, 1024):
    res = kahan(n) - math.log(n) - GAMMA - 1 / (2 * n)
    print(n, f"{n * n * res:.6f}")

def otter(N=256):                           # (d) Otter, exact rationals
    if N < 1:
        return [Fraction(0)], [Fraction(0)]
    r = [Fraction(0), Fraction(1)]
    s = [Fraction(0)] * (N + 1)
    s[1] = Fraction(1)
    for n in range(2, N + 1):
        # r_n = (1/(n-1)) sum_{k=1}^{n-1} s_k r_{n-k}  (division exact)
        r.append(sum(s[k] * r[n - k] for k in range(1, n)) / (n - 1))
        # s_n = sum_{d|n} d r_d — the divisor d = n completes ONLY NOW
        s[n] = (sum(d * r[d] for d in range(1, n) if n % d == 0)
                + n * r[n])
    t = [Fraction(0), Fraction(1)]
    for n in range(2, N + 1):               # T(z) = R - (R^2 - R(z^2))/2
        cross = sum(r[k] * r[n - k] for k in range(1, n))
        val = r[n] - cross / 2
        if n % 2 == 0:
            val += r[n // 2] / 2
        assert val.denominator == 1         # t_n integral, machine-checked
        t.append(val)
    return r, t

r, t = otter()
print([int(x) for x in t[1:17]])           # the receipt list below
for n in (8, 16, 32, 64, 128, 256):
    print(n, f"{float(t[n] / t[n-1]):.9f}") # ratios to Otter's alpha
ALPHA = 2.95576528
for n in (8, 16, 32, 64, 128, 256):
    print(n, f"{float(t[n]) * n**2.5 / ALPHA**n:.7f}")   # the constant
```

Receipts — (a) Catalan r_n = C_n/(4^n/(√π n^{3/2})): 0.6266570687 (n = 2), 0.7754485598 (4), 0.8751168049 (8), 0.9338533633 (16), 0.9659166330 (32), 0.9826942040 (64), 0.9912795452 (128), 0.9956226871 (256), 0.9978070473 (512), 0.9989024465 (1024); n(1−r_n) → 1.125 = **9/8** (last 1.123895) — the 9/(8n) correction confirmed. (b) Central binomial s_n = binom(2n,n)/(4^n/√(πn)): 0.9399856030 (2), 0.9693106997 (4), 0.9845064055 (8), 0.9922191985 (16), 0.9961015277 (32), 0.9980488009 (64), 0.9990239167 (128), 0.9995118383 (256), 0.9997558892 (512), 0.9998779371 (1024); n(1−s_n) → 0.125 = **1/8** (last 0.124992). (c) Harmonic residual n²·(H_n − ln n − γ − 1/(2n)): −0.082827 (4), −0.083301 (16), −0.083331 (64), −0.083333 (256), −0.083333 (1024) → **−1/12** — the Euler–Maclaurin correction confirmed to six digits. (d) Otter: t₁..t₁₆ = 1, 1, 1, 2, 3, 6, 11, 23, 47, 106, 235, 551, 1301, 3159, 7741, 19320 (every t_n integral, asserted in code); ratios t_n/t_{n−1} = 2.090909091 (8), 2.495801576 (16), 2.726757988 (32), 2.840912744 (64), 2.898199479 (128), 2.926942754 (256) → converging to α = 2.95576528… at honest 1/n speed; the constant C_n = t_n·n^{5/2}/α^n = 0.7146498 (8), 0.5828919 (16), 0.5529941 (32), 0.5431738 (64), 0.5388940 (128), 0.5368831 (256) — the n^{−5/2} scale confirmed with the constant still converging at lab scale (Exercise 7 reads all of this).

### Part 3 — Flag inequalities at census scale (Lecture 3)

Deterministic: every graph on n = 4, 5, 6 vertices (64, 1,024, 32,768 of them), exhaustively.

```python
def graphs(n):
    if n <= 0:
        yield []
        return
    pairs = [(i, j) for i in range(n) for j in range(i + 1, n)]
    for mask in range(1 << len(pairs)):
        A = [[0] * n for _ in range(n)]
        for b, (i, j) in enumerate(pairs):
            if mask >> b & 1:
                A[i][j] = A[j][i] = 1
        yield A

def matmul(A, B):
    n = len(A)
    if n == 0:
        return []
    return [[sum(A[i][k] * B[k][j] for k in range(n))
             for j in range(n)] for i in range(n)]

def trace(M):
    return sum(M[i][i] for i in range(len(M)))

for n in (4, 5, 6):
    total = tfree = mantel_ach = dens_viol = dens_eq = pent_ach = 0
    mantel_max = pent_max = pent_total = 0
    for A in graphs(n):
        total += 1
        A2 = matmul(A, A)
        A3 = matmul(A2, A)
        A5 = matmul(A2, A3)
        T = trace(A3)                      # 6T = tr(A^3)
        m = trace(A2) // 2
        if trace(A3) ** 2 > trace(A2) ** 3:
            dens_viol += 1                 # DENSITY violations
        if trace(A3) ** 2 == trace(A2) ** 3:
            dens_eq += 1
        if T == 0:                         # triangle-free
            tfree += 1
            if m > mantel_max:
                mantel_max, mantel_ach = m, 1
            elif m == mantel_max:
                mantel_ach += 1
            assert trace(A5) % 10 == 0     # #C5 = tr(A^5)/10, exact
            C5 = trace(A5) // 10
            pent_total += C5
            if C5 > pent_max:
                pent_max, pent_ach = C5, 1
            elif C5 == pent_max and C5 > 0:  # no "achievers" of a zero max
                pent_ach += 1
    print(n, total, tfree, mantel_max, mantel_ach,
          dens_viol, dens_eq, pent_max, pent_ach, pent_total)
```

Receipts — the exhaustive panels:

| n | graphs | triangle-free | MANTEL max e | achievers | DENSITY viol / eq | PENTAGONS max C5 | achievers |
|---|--------|---------------|--------------|-----------|-------------------|-------------------|-----------|
| 4 | 64 | 41 | 4 = ⌊16/4⌋ | 3 (labeled K_{2,2}) | 0 / 1 | 0 ≤ (4/5)⁵ | — |
| 5 | 1,024 | 388 | 6 = ⌊25/4⌋ | 10 (labeled K_{2,3}) | 0 / 1 | 1 = (5/5)⁵ | 12 |
| 6 | 32,768 | 5,789 | 9 = ⌊36/4⌋ | 10 (labeled K_{3,3}) | 0 / 1 | 2 ≤ (6/5)⁵ = 2.48832 | 180 |

Three readings, all machine-witnessed. **MANTEL**: the extremal balance ⌊n²/4⌋ achieved only by the complete bipartite splits, at every size. **DENSITY**: tr(A³)² ≤ tr(A²)³ has zero violations in all 33,856 graphs, with equality *only the empty graph* (Exercise 11 proves this in general — the receipts are the census-scale witness). **PENTAGONS**: at n = 5 the only triangle-free C5-carrier is C5 itself (the chord fact, Exercise 3 — any chord closes a triangle), so max C5 = 1 with 12 labeled achievers and total C5 = 12 over all triangle-free graphs; at n = 6 the maximum is 2 with 180 labeled achievers, hand-identified as the (2,1,1,1,1)-blowups of C5 (Aut order 4, 720/4 = 180) — the balanced-blowup leading form (n/5)⁵ that Grzesik's theorem makes exact, witnessed at the sizes a machine can check whole. And the counting device underneath: #C5 = tr(A⁵)/10 in triangle-free graphs (each C5 contributes exactly 10 closed walks; any other closed 5-walk would carry an odd cycle shorter than 5), divisibility by 10 asserted on every graph in the census.

### Part 4 — Absorption exhibited at STS(15) (Lecture 4)

One seeded engine (20261090), one continuous stream through the 200 greedy trials; the repair and the min-sacrifice search are deterministic given the packings.

```python
M31 = 2147483647
def engine(seed):
    x = [seed]
    def nxt():
        x[0] = 48271 * x[0] % M31
        return x[0]
    return nxt
unif = lambda nxt, m: nxt() * m // M31      # floor rule

PAIRS = [(a, b) for a in range(1, 16) for b in range(a + 1, 16)]  # lex 105
pm = lambda x, y: (x, y) if x < y else (y, x)
def pairs_of(t):
    return {pm(t[0], t[1]), pm(t[0], t[2]), pm(t[1], t[2])}

TEMPLATE = [tuple(sorted((a, b, a ^ b)))             # F_2^4: 35 triples
            for a in range(1, 16) for b in range(a + 1, 16)
            if (a ^ b) > b]
assert len(TEMPLATE) == 35
assert set().union(*map(pairs_of, TEMPLATE)) == set(PAIRS)   # each pair once

def pack(nxt):                              # random greedy, seed 20261090
    covered, triples = set(), []
    for step in range(500):                  # cap
        unc = [p for p in PAIRS if p not in covered]
        if not unc:
            break
        placed = False
        for _ in range(20):                 # <= 20 pair-draw attempts
            p = unc[unif(nxt, len(unc))]
            thirds = [c for c in range(1, 16)
                      if c not in p and pm(p[0], c) not in covered
                      and pm(p[1], c) not in covered]
            if thirds:
                c = thirds[unif(nxt, len(thirds))]
                t = tuple(sorted((p[0], p[1], c)))
                triples.append(t); covered |= pairs_of(t)
                placed = True; break
        if placed:
            continue
        for p in unc:                       # first-valid scan fallback
            thirds = [c for c in range(1, 16)
                      if c not in p and pm(p[0], c) not in covered
                      and pm(p[1], c) not in covered]
            if thirds:
                t = tuple(sorted((p[0], p[1], thirds[0])))
                triples.append(t); covered |= pairs_of(t)
                placed = True; break
        if not placed:
            break
    return triples

def repair(packing):                        # template-fixpoint, deterministic
    P, S, deleted = list(packing), [], 0    # P: packing, S: template triples
    for _ in range(40):                     # terminates in <= 35 (Ex 12)
        covered = set()
        for t in P + S:
            covered |= pairs_of(t)
        unc = [p for p in PAIRS if p not in covered]
        if not unc:
            break
        add = sorted({next(tr for tr in TEMPLATE
                            if p in pairs_of(tr)) for p in unc})
        for t in list(P):                   # sacrifice: clash = shared pair
            if any(len(set(t) & set(a)) >= 2 for a in add):
                P.remove(t); deleted += 1
        S.extend(add)
    return P, S, deleted

def exact_cover(pairs, cap=30000):           # triangle exact cover, lex-first
    P = set(pairs); nodes = 0
    def rec():
        nonlocal nodes
        nodes += 1                          # nodes = recursion calls
        if nodes > cap:
            raise RuntimeError("cap")
        if not P:
            return True
        p = min(P)
        a, b = p
        for c in range(1, 16):
            if c in (a, b):
                continue
            q1, q2 = pm(a, c), pm(b, c)
            if q1 in P and q2 in P:
                P.difference_update((p, q1, q2))
                if rec():
                    return True
                P.update((p, q1, q2))
        return False
    return rec(), nodes

# cover-routine unit tests (nodes = recursion calls):
assert exact_cover(set().union(*map(pairs_of, TEMPLATE)))[1] == 36
assert exact_cover({(1,2),(1,3),(1,4),(2,3),(2,4),(3,4)}) == (False, 3)
assert exact_cover({(1,2),(2,3),(3,4),(4,5),(5,6),(6,7),(7,8),(1,8)}) == (False, 1)
assert exact_cover({(1,2),(1,3),(2,3),(1,4),(1,5),(4,5)}) == (True, 3)
assert exact_cover({(1,2),(1,3),(2,3),(4,5),(4,6),(5,6)}) == (True, 3)

nxt = engine(20261090)                      # ONE continuous engine, 200 trials
packings, hist, packed_sum = [], {}, 0
for _ in range(200):
    t = pack(nxt)
    packings.append(t)
    left = 105 - 3 * len(t)                 # leftovers: multiples of 3 (Ex 6)
    hist[left] = hist.get(left, 0) + 1
    packed_sum += len(t)
print(sorted(hist.items()), packed_sum / 200)

d_hist, ext, d_sum, S_sum, done = {}, 0, 0, 0, 0
for t in packings:                          # repair all 200
    P, S, deleted = repair(t)
    cov = set()
    for x in P + S:
        cov |= pairs_of(x)
    assert len(cov) == 105 and len(P) + len(S) == 35   # complete: 35, all once
    d_hist[deleted] = d_hist.get(deleted, 0) + 1
    d_sum += deleted; S_sum += len(S); done += 1
print(sorted(d_hist.items()), d_sum / 200, S_sum / 200)
# receipts: the d histogram, mean d = 27.185, mean |S| = 32.73

from itertools import combinations
for t in packings[:50]:                     # min-sacrifice: first 50, d <= 2
    found = False
    for d in (0, 1, 2):
        for drop in combinations(t, d):
            keep = [x for x in t if x not in drop]
            cov = set()
            for x in keep:
                cov |= pairs_of(x)
            unc = [p for p in PAIRS if p not in cov]
            try:
                ok, _ = exact_cover(unc)
            except RuntimeError:
                pass
            else:
                if ok:
                    found = True; break
        if found:
            break
    ext += found
print(ext, "/50")
```

Receipts — Part 4 (seed 20261090, one continuous stream):

- **Greedy packing, 200 trials:** leftover-pairs histogram **9:9, 12:24, 15:61, 18:73, 21:22, 24:10, 27:1**; mean packed triples **29.455**. Leftover counts are multiples of 3 and all uncovered vertex degrees are even — the arithmetic of Exercise 6, visible in every trial.
- **Template-fixpoint repair: 200/200 completions** (each final system: 35 triples, every pair exactly once — asserted in code). Sacrifice histogram (deleted packing triples): **22:3, 23:7, 24:8, 25:19, 26:35, 27:37, 28:38, 29:28, 30:17, 31:8**; mean d = **27.185**, mean template triples in the final system |S| = **32.73**. The reconciliation (Exercise 12(c)): survivors = 29.455 − 27.185 = 2.27; template = 35 − 2.27 = 32.73 — the repair deletes **92.3% of the packing** (the session-113 battery re-measured both statistics: per-trial fraction mean 92.28%, ratio of the rounded means 92.29% — both print 92.3%; the earlier 92.2% was a rounding slip, caught and corrected). Honest receipt: post-hoc template repair *works* but is not the absorption method's small-sacrifice regime.
- **Minimal-sacrifice extension, 50 trials, d ≤ 2: 0/50 extend, zero cap hits** — deleting up to two greedy triples never leaves a triangle-decomposable remainder, at any of the hundreds of subsets tried per trial. The cover routine's unit tests: the template's 105 pairs decompose in **36 nodes**; K4 fails in **3**; C8 fails in **1**; the bowtie {123, 145} succeeds in **3**; two disjoint triples succeed in **3** (nodes = recursion calls).
- **The lesson the receipts license** (and only this): the greedy leaves only 3–9 pairs' worth of leftovers, but post-hoc completion is expensive (naive fixpoint d ≈ 27; minimal extension with d ≤ 2 nonexistent) — the named methods get small sacrifices by *planning* (GKLO's pre-built absorbing structures; Keevash's template-first construction leaves nothing to repair), never by repair. Cross-reference Chapter 17's Part 6, the n = 9 exhibit.

### Part 5 — The algebraic template and its symmetry (Lecture 5)

Deterministic census plus one seeded relabeling panel (20261091, one stream, 10 permutations).

```python
M31 = 2147483647
def engine(seed):                          # the lab engine, self-contained
    x = [seed]
    def nxt():
        x[0] = 48271 * x[0] % M31
        return x[0]
    return nxt
unif = lambda nxt, m: nxt() * m // M31     # floor rule
pm = lambda x, y: (x, y) if x < y else (y, x)
def pairs_of(t):
    return {pm(t[0], t[1]), pm(t[0], t[2]), pm(t[1], t[2])}
TEMPLATE = [tuple(sorted((a, b, a ^ b)))
            for a in range(1, 16) for b in range(a + 1, 16)
            if (a ^ b) > b]                 # (a) 35 triples, 105 pairs once

def invertible(M):                          # Gaussian elimination over F_2
    M = [row[:] for row in M]
    k = len(M)
    if k == 0:
        return True
    for col in range(k):
        piv = next((r for r in range(col, k) if M[r][col]), None)
        if piv is None:
            return False
        M[col], M[piv] = M[piv], M[col]
        for r in range(k):
            if r != col and M[r][col]:
                M[r] = [x ^ y for x, y in zip(M[r], M[col])]
    return True

def apply_M(M, x):                          # image of a k-bit label
    k = len(M)
    bits = [(x >> i) & 1 for i in range(k)]
    out = 0
    for i in range(k):
        v = sum(M[i][j] & bits[j] for j in range(k)) % 2
        out |= v << i
    return out

count_inv, perms, preserve = 0, set(), True
for mask in range(1 << 16):                 # (b) the GL(4,2) census
    M = [[(mask >> (4 * i + j)) & 1 for j in range(4)] for i in range(4)]
    if not invertible(M):
        continue
    count_inv += 1
    img = tuple(apply_M(M, x) for x in range(16))  # img[label]; img[0] = 0
    if any(img[a ^ b] != img[a] ^ img[b]          # triple preservation
           for a in range(1, 16) for b in range(a + 1, 16)):
        preserve = False
    perms.add(img)
print(count_inv, preserve, len(perms))

nxt = engine(20261091)                      # (c) FY relabeling, 10 permutations
valid = 0
for _ in range(10):
    arr = list(range(16))                   # 16-entry array indexed by label
    for i in range(15, 1, -1):              # Fisher-Yates, one draw per index
        j = unif(nxt, i) + 1                # j uniform in [1, i]
        arr[i], arr[j] = arr[j], arr[i]
    sys = {tuple(sorted((arr[a], arr[b], arr[c])))  # each triple's image
           for (a, b, c) in TEMPLATE}
    cov = set()
    for t in sys:
        cov |= pairs_of(t)
    if len(sys) == 35 and len(cov) == 105:  # the image system is an STS(15)
        valid += 1
print(valid, "/ 10")                        # receipt: 10 / 10
```

Receipts — Part 5: (a) the template verified: **35 triples, every one of the 105 pairs covered exactly once**. (b) The GL(4,2) census over all 65,536 matrices: **20,160 invertible** = (16−1)(16−2)(16−4)(16−8) (Exercise 4's column count, machine-witnessed); **every invertible map preserves the triple system** (M(x ⊕ y) = Mx ⊕ My checked on all pairs, all 20,160 matrices); **20,160 distinct induced permutations** — at least 20,160 automorphisms exhibited, and the exact order 20,160 = |PGL(4,2)| is textbook canon, cited, not re-derived. (c) The FY-relabeling (seed 20261091, floor rule, i from 15 down, 16-entry array indexed by label): **10/10 image systems valid**. The receipts' honesty note stands: a point bijection trivially preserves STS-ness — the panel verifies the bookkeeping; the algebraicity is panel (b); the real method's randomization (random functions and orderings over the template) is beyond lab scale, and Part 4 shows the template's role instead.

### Part 6 — The strategy devices, exhaustively (Lecture 6)

Deterministic verification and minimaxes; three seeded panels: 20261092 (naive snail, fresh engine per toy), 20261093 (the grid census), 20261094 (blob growth).

```python
from itertools import product
from functools import lru_cache
M31 = 2147483647
def engine(seed):                          # the lab engine, self-contained
    x = [seed]
    def nxt():
        x[0] = 48271 * x[0] % M31
        return x[0]
    return nxt
unif = lambda nxt, m: nxt() * m // M31     # floor rule

def phi(x):                                 # (a) swap 1<->2 at first nonzero
    y = list(x)
    for i, d in enumerate(y):
        if d:
            y[i] = 3 - d
            break
    return tuple(y)

for n in range(1, 13):                      # the pairing device, verified
    verts = [x for x in product((0, 1, 2), repeat=n) if any(x)]
    assert all(phi(phi(x)) == x for x in verts)        # involution
    assert all(phi(x) != x for x in verts)             # fixed-point-free
    assert all(sum(abs(a - b) for a, b in zip(x, phi(x))) == 1
               for x in verts)                          # edge certificate
    # n = 12: 531,440 vertices, all pass

def minimax(n):                             # full game search, memoized
    if n <= 0:
        return False, 0
    V = list(product((0, 1, 2), repeat=n))
    idx = {v: i for i, v in enumerate(V)}
    nbr = [[j for j in range(len(V))
            if sum(abs(a - b) for a, b in zip(V[i], V[j])) == 1]
           for i in range(len(V))]
    memo = {}
    def wins(v, mask, root=False):
        moves = [w for w in nbr[v] if not mask >> w & 1]
        if not moves:                        # terminal states ARE stored
            if not root:
                memo[(v, mask)] = False
            return False
        if (v, mask) in memo:
            return memo[(v, mask)]
        res = any(not wins(w, mask | 1 << w) for w in moves)
        if not root:                        # the root state is NOT stored
            memo[(v, mask)] = res
        return res
    start = idx[(0,) * n]                   # start visited, unusable
    return wins(start, 1 << start, root=True), len(memo)

for n in (1, 2):
    print(n, minimax(n))    # (False, 2), (False, 28) — Bob wins both

def spans(R, C, route):                     # (b) the snail subgame
    if R < 2 or C < 1:
        return [(1, max(1, C))]
    sp = [(1, route[0])]
    for r in range(2, R):                   # rows 2..R-1
        sp.append((route[r - 2], route[r - 1]))
    sp.append((route[R - 2], C))            # row R
    return sp

def walk(R, C, route, monsters):            # lazy first-entry adversary
    if R < 2 or C < 1:
        return ("survive", None, None, None)
    sp = spans(R, C, route)
    committed = dict(monsters)
    for r in range(1, R + 1):
        lo, hi = sp[r - 1]
        if 1 < r < R:
            if r in committed:             # existing monster hits in-span
                m = committed[r]
                if lo <= m <= hi:
                    return ("die", r, m, None)
            else:                           # fresh row: first free cell commits
                taken = set(committed.values())
                for c in range(lo, hi + 1):
                    if c not in taken:
                        committed[r] = c
                        return ("die", r, c, (r, c))
                # else: deferred (no commit; the walk continues)
    return ("survive", None, None, None)

def deferred_homes(R, C, route, monsters):  # legal columns for deferred rows
    sp = spans(R, C, route)
    taken = set(monsters.values())
    return {r: [c for c in range(1, C + 1)
                if c not in taken and not (sp[r - 1][0] <= c <= sp[r - 1][1])]
            for r in range(2, R) if r not in monsters}

def minimax_snail(R, C):                    # f(state) = min attempts
    if R < 2 or C < 1:
        return lambda state=(): 1
    def key(mon):
        return tuple(sorted(mon.items()))
    @lru_cache(maxsize=None)
    def f(state):
        mon = dict(state)
        best = None
        def routes(route):                  # lex order, non-decreasing
            nonlocal best
            if len(route) == R - 1:
                out = walk(R, C, route, mon)
                if out[0] == "survive":
                    cand = 1
                elif out[3] is not None:    # commit-death: progress
                    m2 = dict(mon); m2[out[3][0]] = out[3][1]
                    cand = 1 + f(key(m2))
                else:
                    return                  # no-commit death: a cycle, skipped
                if best is None or cand < best:
                    best = cand
                return
            lo = route[-1] if route else 1
            for a in range(lo, C + 1):
                routes(route + (a,))
                if best == 1:               # sound: 1 is optimal — the
                    return                  # poisoned variant broke at 2
        routes(())
        return best
    return f

def naive_snail(R, C, seed, attempts=6):     # sequential conditional draws
    if R < 2 or C < 1:
        return ["SURVIVE"]
    nxt = engine(seed)                      # FRESH engine per toy
    mon, out = {}, []
    for _ in range(attempts):
        route, prev = (), unif(nxt, C) + 1
        route += (prev,)
        for _ in range(R - 2):
            prev += unif(nxt, C - prev + 1)
            route += (prev,)
        res = walk(R, C, route, mon)
        if res[0] == "survive":
            out.append("SURVIVE"); break
        if res[3]:
            mon[res[3][0]] = res[3][1]
        out.append(f"r{res[1]}c{res[2]}")
    return out

def grid_census(seed, plays=200, rounds=48):  # (c1) the state-partition census
    nxt = engine(seed)
    violations = shortfalls = 0
    max_comp = 0
    DIRS = ((-1, 0), (1, 0), (0, -1), (0, 1))
    for _ in range(plays):
        owner = {}                             # (r, c) -> 'B' or 'R'
        state = lambda r, c: (r // 2, c // 2)  # the 2x2 states
        for _ in range(rounds):                # 48 rounds x 3 claims = 144
            whites = [(r, c) for r in range(12) for c in range(12)
                     if (r, c) not in owner]   # row-major
            b = whites[unif(nxt, len(whites))]  # B draws one white
            owner[b] = 'B'
            r_count = 0
            for dr, dc in DIRS:                # R: B's pick's cross-border
                nb = (b[0] + dr, b[1] + dc)    # white 4-neighbors, exact
                if (0 <= nb[0] < 12 and 0 <= nb[1] < 12
                        and state(*nb) != state(*b) and nb not in owner):
                    owner[nb] = 'R'; r_count += 1
            while r_count < 2:                 # fill to 2 with drawn whites
                whites = [w for w in whites if w not in owner]
                if not whites:
                    shortfalls += 1; break
                w = whites[unif(nxt, len(whites))]
                owner[w] = 'R'; r_count += 1
            for dr, dc in DIRS:                # the cap, checked live
                nb = (b[0] + dr, b[1] + dc)
                if (0 <= nb[0] < 12 and 0 <= nb[1] < 12
                        and state(*nb) != state(*b) and owner.get(nb) == 'B'):
                    violations += 1
        seen, best = set(), 0                  # end of play: B's components
        for cell in owner:
            if owner[cell] == 'B' and cell not in seen:
                comp, stack = 0, [cell]; seen.add(cell)
                while stack:
                    r, c = stack.pop(); comp += 1
                    for dr, dc in DIRS:
                        nb = (r + dr, c + dc)
                        if (0 <= nb[0] < 12 and 0 <= nb[1] < 12
                                and owner.get(nb) == 'B' and nb not in seen):
                            seen.add(nb); stack.append(nb)
                best = max(best, comp)
        max_comp = max(max_comp, best)
    return violations, shortfalls, max_comp

def blob_growth(seed, trials=100):             # (c2) B's half: the blob
    nxt = engine(seed)
    hist = {}
    for _ in range(trials):
        blob, red = set(), set()               # the blob starts EMPTY
        rounds = 0
        def frontier():                        # 8-directional (king moves)
            f = {(r + dr, c + dc) for (r, c) in blob
                 for dr in (-1, 0, 1) for dc in (-1, 0, 1)
                 if (dr, dc) != (0, 0) and (r + dr, c + dc) not in blob}
            return sorted(f)
        while len(blob) < 4:
            rounds += 1
            if blob:                           # rounds 2+: a drawn frontier cell
                f = [x for x in frontier() if x not in red]
                blob.add(f[unif(nxt, len(f))])
            else:
                blob.add((0, 0))              # round 1: B claims the origin
            for _ in range(2):                # R claims 2, every round
                f = [x for x in frontier() if x not in red]
                red.add(f[unif(nxt, len(f))])
        hist[rounds] = hist.get(rounds, 0) + 1
    return hist

print(minimax_snail(4, 3)(()), minimax_snail(5, 4)(()))      # 3, 3
print(deferred_homes(5, 4, (1, 1, 2, 2), {2: 2, 3: 3}))      # {4: [1, 4]}
print(naive_snail(4, 3, 20261092), naive_snail(5, 4, 20261092))
print(grid_census(20261093))   # receipt: (0, 0, 4) — 9,600 rounds
print(blob_growth(20261094))   # receipt: {4: 100} — mean 4.00, failures 0
```

Receipts — Part 6(a): **φ verified for n = 1..12** — involutive ✓, fixed-point-free ✓, every {x, φ(x)} an edge ✓, all three properties on every vertex of every cube (n = 12: **531,440** vertices). **Full minimax** (token starts at 0^n, visited and unusable; Alice moves first; the player without a move loses; memo on (vertex, visitedMask) — terminal states stored, the root state not, the search short-circuiting): **n = 1: AliceWins = false, 2 memo states; n = 2: AliceWins = false, 28 memo states** — Bob wins both, and the matching IS the strategy (Exercise 5's invariant is the proof; the search is the independent witness).

Receipts — Part 6(b), the monotone-route subgames (route = non-decreasing descent columns; monsters one per interior row, at most one per column; the lazy adversary commits a fresh row's monster at the first-reached cell with a free column, and *defers* when the entered column is taken):

- **(R,C) = (4,3): minimum attempts = 3.** Lex-first optimal line: [1,1,1] dies row 2 col 1 (m₂ = 1); [2,2,2] dies row 3 col 2 (m₃ = 2); [2,3,3] **survives** (row-2 span [2,3] avoids m₂ = 1; row-3 span [3,3] avoids m₃ = 2).
- **(R,C) = (5,4): minimum attempts = 3.** Line: [2,2,2,2] dies row 2 col 2 (m₂ = 2); [3,3,3,3] dies row 3 col 3 (m₃ = 3); [1,1,2,2] **survives** — entering fresh row 4 at column 2, monster 2's TAKEN column: the lazy commit cannot fire there, the monster stays **deferred**. Deferred-placement consistency machine-verified: row 4 deferred with legal homes (m₄ placeable at column 1 or 4) — an illusory win (a deferred monster with no legal home) would have been caught. Both toys reproduce the full problem's answer, 3.
- **Naive snail (seed 20261092, fresh engine per toy, 6 attempts):** (4,3) dies r2c2, r2c2, r2c2, r2c2, r2c2, r3c1; (5,4) dies r2c2, r3c4, r4c3, then repeats r2c2. Honest display: unengineered play dies repeatedly at known commits — the mechanism (fresh-row commits defeat unplanned attempts) is what the receipts show, not a strategy.

Receipts — Part 6(c1), the state-partition census (12×12 board, 2×2 states, B draws one white per round from the row-major list, R claims B's pick's cross-border white 4-neighbors then fills to 2 with drawn whites; seed 20261093, 200 plays × 48 rounds): **9,600 rounds: cross-border B-B adjacency violations = 0; R-shortfall rounds = 0; maximum within-state B component = 4** — B's score capped at exactly 4, the contest answer, machine-witnessed at full census strength.

Receipts — Part 6(c2), blob growth (infinite grid, 8-directional frontier; round = B claims one drawn frontier cell, then R claims two; the blob starts empty and B's first claim is the origin; seed 20261094, 100 trials): **100/100 trials reach blob size 4 in exactly 4 rounds** (histogram 4:100, mean 4.00, failures 0) — Exercise 8's neighbor-availability lemma at full strength: Red's two removals per round can never fence a blob this small. (Two rejected designs from the verification pass are recorded in the Notes: a bounded board fails at the edges 5/100; R moving first fails 33/100 — the infinite grid and B-first are load-bearing.)

## Answers to the Exercises

*Worked answers for the twelve graded problems and the three ◆ pattern-unknown ones. The three ◐ Explorations state what you should find and get no worked answer — that is their point. Where an answer cites a machine receipt, the receipt exists: the lab above, from the chapter's documented engine (seeds 20261090–20261094 as mapped there).*

**Answer 1 (maximality, by hand and by machine).** (a) For S = {2,3} ⊆ [6], test each e′ ∈ [6] ∖ S = {1,4,5,6} against the three addability conditions: (i) no x, y ∈ S satisfy x + y = e′, (ii) 2e′ ∉ S, (iii) no x ∈ S satisfies x + e′ ∈ S. Candidate e′ = 1 fails (ii), since 2·1 = 2 ∈ S (and also fails (iii), since 2 + 1 = 3 ∈ S). Candidates 4, 5, 6 fail (i), since 2 + 2 = 4, 2 + 3 = 5, and 3 + 3 = 6 with both summands in S. Thus no element of [6] ∖ {2,3} can be added, so {2,3} is maximal. (b) The five remaining maximal sum-free subsets of [6], verified the same way: {1,3,5}: e′ = 2 fails (i) (1 + 1 = 2); e′ = 4 fails (i) (1 + 3 = 4); e′ = 6 fails (i) (1 + 5 = 6 and 3 + 3 = 6). {3,4,5}: e′ = 1 fails (iii) (3 + 1 = 4 ∈ S); e′ = 2 fails (ii) (2·2 = 4 ∈ S) and (iii) (3 + 2 = 5 ∈ S); e′ = 6 fails (i) (3 + 3 = 6). {1,4,6}: e′ = 2 fails (i) (1 + 1 = 2) and (ii) (2·2 = 4 ∈ S); e′ = 3 fails (ii) (2·3 = 6 ∈ S) and (iii) (1 + 3 = 4 ∈ S); e′ = 5 fails (i) (1 + 4 = 5) and (iii) (1 + 5 = 6 ∈ S). {2,5,6}: e′ = 1 fails (ii) (2·1 = 2 ∈ S) and (iii) (5 + 1 = 6 ∈ S); e′ = 3 fails (ii) (2·3 = 6 ∈ S) and (iii) (2 + 3 = 5 ∈ S); e′ = 4 fails (i) (2 + 2 = 4) and (iii) (2 + 4 = 6 ∈ S). {4,5,6}: e′ = 1 fails (iii) (4 + 1 = 5 ∈ S); e′ = 2 fails (ii) (2·2 = 4 ∈ S) and (iii) (4 + 2 = 6 ∈ S); e′ = 3 fails (ii) (2·3 = 6 ∈ S). (c) The 24 sum-free subsets of [6] partition by cardinality: 1 empty set; 6 singletons; 12 two-element sets — all binom(6,2) = 15 pairs except the three {x, 2x} pairs {1,2}, {2,4}, {3,6}; and 5 three-element sets ({1,3,5}, {3,4,5}, {1,4,6}, {2,5,6}, {4,5,6}) — giving 1 + 6 + 12 + 5 = 24 in total, and every sum-free subset sits inside at least one of the six maximal sets {2,3}, {1,3,5}, {3,4,5}, {1,4,6}, {2,5,6}, {4,5,6}. Condition (i) — the one naive checks forget — is exactly what kills the middle candidates.

**Answer 2 (reading the Catalan receipts).** (a) From C(z) = 1 + zC(z)² and C(0) = 1, the quadratic formula gives C(z) = (1 − √(1−4z))/(2z). By the binomial series (1−4z)^{1/2} = 1 − Σ_{m≥1} (2/m)·binom(2m−2, m−1)·z^m, extracting [zⁿ]C(z) = −(1/2)·[z^{n+1}](1−4z)^{1/2} yields C_n = (1/(n+1))·binom(2n,n). Singularity analysis of (1−4z)^{1/2} = Σ_k (−1)^k·binom(1/2, k)·(4z)^k at the dominant square-root singularity ρ = 1/4 transfers to an asymptotic expansion in descending powers of n: binom(2n,n) = (4^n/√(πn))·(1 − 1/(8n) + 1/(128n²) + O(n⁻³)). Dividing by n+1 = n(1 + 1/n), i.e. multiplying by (1/n)(1 − 1/n + 1/n² + O(n⁻³)), gives C_n = (4^n/(√π·n^{3/2}))·(1 − 1/(8n) + 1/(128n²) + O(n⁻³))·(1 − 1/n + 1/n² + O(n⁻³)) = (4^n/(√π·n^{3/2}))·(1 − 9/(8n) + 145/(128n²) + O(n⁻³)) — the 145/128 = 1 + 1/8 + 1/128 collecting the three 1/n² contributions. (b) Thus r_n = C_n/(4^n/(√π·n^{3/2})) = 1 − 9/(8n) + 145/(128n²) + O(n⁻³). The first correction is negative (−9/(8n)), so r_n approaches from below; the second correction enters as O(1/n²), so n(1−r_n) approaches 9/8 from below with its own 1/n drift — the receipts read 0.7467 (n = 2) rising to 1.123895 (n = 1024), still short of 1.125, honestly. (c) For the binomial, n(1−s_n) → 1/8 by the same analysis one power of n lower. The Catalan is the binomial divided by (n+1): (1/(n+1))·(1 − 1/(8n)) ≈ (1/n)(1 − 1/n)(1 − 1/(8n)) ≈ (1/n)(1 − 9/(8n)) — the extra factor of n shifts the correction from 1/8 to 9/8; the two limits differ by exactly 9.

**Answer 3 (Mantel and the pentagon at n = 5).** (a) K_{3,3}: choose which 3 of 6 labels sit on the left — 20 ways — but the two sides are unordered, so 10 labeled graphs. (b) A 5-vertex graph containing a C5 has at least the cycle's 5 edges; any sixth edge joins two cycle vertices, and in C5 every pair of non-adjacent vertices is at cyclic distance 2 — the chord plus the two cycle edges between its endpoints closes a triangle (the short way around is a 2-path). So a triangle-free C5-carrier is exactly C5. (c) At n = 5 the census is then one line: the only carrier is C5, it contains one C5, and there are 5!/(2·5) = 12 labelings — max C5 = 1 = (5/5)⁵, total 12. At n = 6 there is room to blow up: doubling one vertex of C5 gives the (2,1,1,1,1)-blowup with 2 ≤ (6/5)⁵ = 2.48832 C5s, and the receipts' exhaustive search confirms no triangle-free 6-vertex graph reaches 3 (180 labeled achievers, all blowups — the complete proof that 2 is the maximum and 180 the exact achiever count is Answer ◆14) — the structural analysis is genuinely larger, which is why the (n/5)⁵ leading form is a theorem (Grzesik), not a glance.

**Answer 4 (counting GL(4,2) by columns).** (a) Column 1: any nonzero vector, 15. Column 2: avoid the span of column 1 ({0, v₁} — 2 vectors), 14 = 16 − 2. Column 3: avoid the span of the two prior columns (a 2-dimensional span, 4 vectors), 12 = 16 − 4. Column 4: avoid the 3-dimensional span (8 vectors), 8 = 16 − 8. Product 15·14·12·8 = 20,160 — every choice sequence extends to a unique invertible matrix, and invertibility is exactly column-independence. (b) A 4×4 F₂ matrix has 16 entries: 2¹⁶ = 65,536 total, the census denominator. (c) GL(k,2) = ∏_{i=0}^{k−1}(2^k − 2^i); k = 3: 7·6·4 = 168 — Exploration 16's Fano census, the same column count one dimension down.

**Answer 5 (Bob's invariant, proved).** (a) φ acts on the first nonzero coordinate; swapping 1 ↔ 2 preserves nonzero-ness and position, so φ(φ(x)) = x, and since the swapped digit changes (1 → 2 or 2 → 1), φ(x) ≠ x. (b) All coordinates outside i are unchanged; at i the digit moves by ±1; so x and φ(x) differ by exactly 1 in exactly one digit — in the ternary reading |φ(x) − x| = 3^i, the edge certificate the lab checks. (c) Invariant: after each of Bob's replies the visited set is {0^n} ∪ ⋃_{j≤k} {x_j, φ(x_j)} — a start plus complete pairs. Alice's (k+1)-th move lands on a fresh y. If φ(y) were visited: φ(y) ≠ 0^n (φ(y) has a nonzero digit), so φ(y) ∈ some complete pair {x_j, φ(x_j)}; applying φ, y = x_j or y = φ(x_j) — either way y is visited, contradiction. So φ(y) is fresh and Bob's reply is legal. The game is finite, Bob always has a reply after every Alice move, so it is Alice who eventually cannot move. (d) At n = 2 the board has 9 vertices and 2⁹ = 512 possible masks — 4,608 conceivable (vertex, mask) states — but the reachable set from the start is tiny: the memo stores exactly 28 states, the search's own census of what is actually attainable (and at n = 1, just 2).

**Answer 6 (the leftovers' arithmetic).** (a) A Steiner triple system on 15 points has C(15,2) = 105 pairs, and each packed triple covers 3 distinct pairs, disjoint from all previously covered pairs. After packing t triples, 105 − 3t = 3(35 − t) pairs remain uncovered — always a multiple of 3 (the receipts' leftover columns are 9, 12, …, 27, never anything else). (b) In K₁₅ every vertex v initially has degree 14 (even). Each packed triple containing v uses exactly 2 edges incident to v, and each packed triple not containing v uses 0 edges incident to v. Thus the leftover degree deg_L(v) = 14 − 2·(#packed triples through v) is even for every v ∈ [15]. (c) Because the leftover graph L ⊆ K₁₅ is a simple graph in which every vertex has even degree, Veblen's theorem guarantees that E(L) decomposes into edge-disjoint simple cycles. However, a Steiner completion requires that E(L) decompose into edge-disjoint *triangles* (C₃), whereas an even-degree simple graph with 3 | E(L) may consist of cycles of length ≥ 4 and contain no triangle decomposition at all (or even zero triangles, e.g. when L is bipartite). Deleting d ≤ 2 packed triples returns only 3d ≤ 6 edges to L — enough to modify the cycle structure on at most those 6 edges, not enough to conjure the missing structure: the receipts say so with data, 0/50 trials admit closure after deleting d ≤ 2 packing triples, with zero cap hits — the searches exhausted honestly. Divisibility (P41's cameo) is the necessary stage; the decomposition is the missing structure, and that is the whole absorption lesson in one receipt.

**Answer 7 (reading Otter's receipts).** (a) Otter's asymptotic formula for unrooted trees is t_n = C·α^n·n^{−5/2}·(1 + O(1/n)) with α = 2.95576528…. Taking consecutive ratios gives t_n/t_{n−1} = α·((n−1)/n)^{5/2}·(1 + O(n⁻²)) = α·(1 − 5/(2n) + O(n⁻²)), so n·(α − t_n/t_{n−1}) → (5/2)·α ≈ 7.3894132. Evaluating on the lab receipts gives 8(2.95576528 − 2.090909091) = 6.9188, 16(2.95576528 − 2.495801576) = 7.3594, 32(2.95576528 − 2.726757988) = 7.3282, 64(2.95576528 − 2.840912744) = 7.3506, 128(2.95576528 − 2.898199479) = 7.3684, and 256(2.95576528 − 2.926942754) = 7.3786, approaching (5/2)α as predicted — near-constant, with the small non-monotone dip at n = 32 honestly in the ladder. (b) In C_n = t_n·n^{5/2}/α^n the n^{−5/2} factor is multiplied out explicitly, canceling the first-order 5/(2n) drift of the ratio and leaving only the O(1/n) series correction to C itself — so its residual drift is the next order: the receipts show C_n moving by ~0.002 per doubling at n = 256 against the ratio's ~0.029, an order of magnitude faster convergence. (c) By Otter's dissimilarity theorem for trees: for any unrooted tree T, let p(T) be the number of orbits of vertices under Aut(T), q(T) the number of orbits of edges, and s(T) ∈ {0,1} the number of symmetry edges (edges whose endpoints are swapped by an automorphism of T). Then p(T) − q(T) + s(T) = 1. Summing over all unrooted trees on n vertices gives Σp(T) = r_n (each vertex-orbit of each tree, rooted once, is a rooted tree), Σq(T) = [zⁿ]½R(z)² (an edge joining two rooted trees; symmetric pairs with s(T) = 1 need R(z²)), and Σ(q(T) − s(T)) = [zⁿ]½(R(z)² − R(z²)) — yielding T(z) = R(z) − ½(R(z)² − R(z²)), the identity the lab verifies digit-by-digit. Because t₂₅₆ ≈ 1.59×10¹¹⁴ (a 115-digit integer, computed exactly in the session-113 battery) exceeds the 53-bit significand of IEEE-754 doubles (2⁵³ ≈ 9×10¹⁵) by nearly a hundred orders of magnitude, verifying the exact integrality of t_n requires arbitrary-precision rational arithmetic — the lab's scaled big-integer route.

**Answer 8 (the blob's arithmetic).** (a) For a finite nonempty subset B ⊆ ℤ², let N∞[B] = B ∪ F(B) be its closed L∞-unit-ball neighborhood. If |B| = 1, say B = {(0,0)}, then |N∞[B]| = 3×3 = 9, so |F(B)| = 9 − 1 = 8. If |B| = 2 and the two cells are 8-adjacent, their bounding box has dimensions 2×1 (orthogonal) or 2×2 (diagonal); expanding by 1 in all four directions gives a 4×3 box of 12 cells (orthogonal case, |F(B)| = 12 − 2 = 10) or a 4×4 box minus two opposite corners = 14 cells (diagonal case, |F(B)| = 14 − 2 = 12) — so |F(B)| ≥ 10. If |B| = 3 and B is 8-connected, N∞[B] is the union of three 3×3 squares centered at B's cells: the minimum area occurs when two centers share a row or column (an L-tromino in a 2×2 bounding box, whose dilate is a 4×4 square minus at most one corner ≥ 15 cells; or a straight 1×3 tromino, whose dilate is a 3×5 rectangle of exactly 15), so |N∞[B]| ≥ 15 and |F(B)| = |N∞[B]| − 3 ≥ 12. In all cases |F(B)| ≥ 2|B| + 6 for 1 ≤ |B| ≤ 3. (b) On round 1, Blue claims (0,0) (|B| = 1). Before Blue's turn on round k+1 (k ∈ {1, 2, 3}), Blue's blob has size |B| = k with |F(B)| ≥ 2k + 6, while Red has claimed a total of 2k cells across the preceding k rounds. Thus at least (2k + 6) − 2k = 6 > 0 frontier cells of B are unclaimed by Red — Blue grows on rounds 1–4 no matter what Red does, ending at size 4: the receipt's 100/100 in exactly 4 rounds is the lemma in executable form. (c) The state partition attacks *span*, not growth. Red answers each Blue pick by taking the cross-border squares: each Blue cell b in a 2×2 block has exactly two orthogonal neighbors outside that block, and Red immediately claims both of them (if still white) — so Blue's cells never connect orthogonally across state lines, confining every 4-connected Blue component to a single 2×2 state, whose cells number 4. The frontier argument guarantees Blue can always add a *neighbor*; every neighbor Red permits lies inside one state. Growth is unlimited; span is capped — the two halves of the contest answer (guarantee 4, cap 4) are two different counting facts, and the receipts witness both (c2's 4:100 and c1's max component 4).

**Answer 9 (the snail's two-attempt lower bound).** (a) Attempt 1: nothing is committed; the route enters row 2 at the first cell of its span, column a₁; the column is free (nothing taken), so the lazy adversary commits m₂ = a₁ and the snail dies there — every first attempt dies, no matter the route. (b) On Attempt 2 the committed state is {m₂ = c}. Any route that survives row 2 must have its row-2 span [a₁, a₂] disjoint from {c}; in particular a₂ ≠ c. When this route enters fresh row 3 with span [a₂, a₃], its entry column a₂ is therefore guaranteed to be outside the taken column set {c}, so the lazy adversary immediately commits m₃ = a₂ at row 3's entry cell (3, a₂) and kills Attempt 2. (The same conclusion survives the one corner the argument must close: to defer row 3, every cell of its span would have to be taken — span ⊆ {c} — forcing a row-2 span containing c, dead already.) Every second attempt dies too. (c) Third attempt against {m₂ = 2, m₃ = 3}: [1,1,2,2] walks row 2's span [1,1] (avoids 2), row 3's span [1,2] (avoids 3), and enters fresh row 4 at column 2 — taken: the commit cannot fire, the monster defers with legal homes {1, 4} (machine-checked), and the snail crosses. (d) Laziness never spends a column before the snail arrives — so the taken columns accumulate exactly where the snail has already been, and a route that re-enters a taken column at a fresh row converts the adversary's own bookkeeping into a shield. Deferral is not a loophole; it is the mechanism the answer runs on.

**Answer 10 (the trivial families, counted exactly).** (a) Odd + odd = even, so any all-odd set is sum-free; two elements above n/2 sum above n, so any subset of {⌊n/2⌋+1, …, n} is sum-free. Each family has 2^{⌈n/2⌉} members. (b) At n = 26 the overlap is the subsets of {15, 17, 19, 21, 23, 25} — six odd elements above 13 — so 2⁶ = 64 sets including the empty one, 63 nonempty: exactly the receipt's "both" count. (c) The Cameron–Erdős conjecture says SF(n)/2^{⌈n/2⌉} stays bounded by a constant as n → ∞. The lab's drift — 11.54 at n = 26 to 13.27 at n = 34, monotone but decelerating (increments 0.72, 0.43, 0.29, 0.30) — is consistent with a bounded limit and with slow growth alike; thirty-four vertices cannot distinguish the two, and the receipts refuse to print a bound the data does not force. Green's theorem (cited, not re-derived) decides it: the ratio is bounded.

**Answer 11 (the spectral density inequality, completely).** (a) Since A is a real symmetric n×n matrix, it has real eigenvalues λ₁, …, λ_n, and tr(A^k) = Σλᵢ^k for every integer k ≥ 1. Setting ρ = max |λᵢ|, the triangle inequality and the termwise bound |λᵢ|³ ≤ ρ·λᵢ² give |tr(A³)| = |Σλᵢ³| ≤ Σ|λᵢ|³ ≤ ρ·Σλᵢ² = ρ·tr(A²) (moreover, since A has nonnegative entries, tr(A³) = 6T ≥ 0, so |tr(A³)| = tr(A³)). (b) Since ρ² = max λᵢ² ≤ Σλᵢ² = tr(A²) (the largest square does not exceed the sum of squares), ρ ≤ tr(A²)^{1/2}. Substituting into |tr(A³)| ≤ ρ·tr(A²) gives 0 ≤ |tr(A³)| ≤ tr(A²)^{3/2}, and squaring both nonnegative sides yields tr(A³)² ≤ tr(A²)³. (c) With T = tr(A³)/6 and m = tr(A²)/2: 36T² ≤ 8m³, i.e. T ≤ (√2/3)·m^{3/2} ≈ 0.471·m^{3/2} — triangle density capped by edge density to the 3/2. (d) Equality needs all steps tight: Σλᵢ³ = Σ|λᵢ|³ (every nonzero eigenvalue positive), |λᵢ| = ρ for every nonzero eigenvalue, and exactly one nonzero eigenvalue (ρ² = Σλᵢ²). A rank-one symmetric 0/1 matrix with zero diagonal would be A = vv^T with A_ii = v_i² — nonzero wherever v_i = 1, contradicting the zero diagonal; so v = 0 and A = 0: only the empty graph, exactly the receipts' census (equalities 1 at each n ≤ 6). (e) The inequality is a valid relation among substructure densities (triangles vs edges) proved by an averaging argument on the spectrum — precisely the kind of statement the flag calculus generates systematically; the lab's panel is the calculus's raw material at a scale where "all graphs" is checkable.

**Answer 12 (the repair loop, proved and priced).** (a) In any uncompleted round some pair is uncovered; its template triple is not yet in use (else the pair would be covered); so each round adds at least one new template triple, the set in use grows strictly, and it is bounded by 35 — at most 35 rounds (the code caps at 40 and never reaches it). (b) Template triples pairwise share at most one point (they are the lines of PG(3,2), an STS), so the added triples never double-cover a pair among themselves; the deletion rule removes every packing triple sharing a pair with any added triple, so no pair is ever covered twice across the two sets; and the packing itself was pair-disjoint. The final system's completeness (asserted per trial) is the fixpoint: every pair exactly once. (c) Survivors = 29.455 − 27.185 = 2.27 packing triples; template triples = 35 − 2.27 = 32.73 — the receipts' |S|, exact to the digit. The deleted fraction is 27.185/29.455 = 92.29% ≈ **92.3%** (the per-trial fraction mean agrees: 92.28% — the session-113 battery measured both): the repair completes by *replacing* the packing with the template, which is why d ≈ 27 is the honest receipt for "post-hoc repair is not absorption" — the real methods buy their small sacrifices by building the absorbing structure before the random phase, when it costs O(1) instead of 92.3%.

**Answer ◆13 (Bob wins the digit-string game).** Encode the game as a token-avoidance game on the graph {0,1,2}^n minus the start (P25: the game-to-graph encoding): vertices are the strings, edges join strings differing by ±1 in one digit, the token starts at 0^n (visited, unusable), and the player unable to move loses. Define φ: swap 1 ↔ 2 at the first nonzero coordinate — a fixed-point-free involution whose pairs are edges (the lab verifies all three properties on every vertex for n ≤ 12, 531,440 vertices at n = 12). Bob answers every Alice move to x with φ(x); the visited set stays a union of complete pairs plus the start (Answer 5's invariant), so Bob always has a legal reply and Alice eventually does not. Bob wins for every n — the pairing device, machine-witnessed by the exhaustive minimax at n = 1, 2.

**Answer ◆14 (five-cycles in triangle-free 6-vertex graphs).** First, in any simple triangle-free graph G, tr(A⁵) = 10·#C₅(G): any closed walk w = (v₀, v₁, v₂, v₃, v₄, v₀) of length 5 in a loopless graph has odd length, so the subgraph spanned by its edges cannot be bipartite and therefore contains an odd cycle; since G is triangle-free, that odd cycle must have length 5, which uses all 5 steps of w and forces v₀, v₁, v₂, v₃, v₄ to be 5 distinct vertices forming a 5-cycle in G. Conversely, each 5-cycle in G is traversed by exactly 5×2 = 10 closed directed walks of length 5 (5 starting vertices × 2 orientations). Second, let G be a triangle-free graph on 6 vertices containing at least one 5-cycle C = v₁v₂v₃v₄v₅v₁, and let u be the sixth vertex. By Answer 3(b), the induced subgraph G[V(C)] has no chords and is exactly C. Moreover, u cannot be adjacent to two consecutive vertices v_i, v_{i+1} of C, as u·v_i·v_{i+1} would be a triangle. Since C₅'s largest independent set has size α(C₅) = 2, u has at most 2 neighbors on C — and if deg_C(u) = 2, those two neighbors must be at distance 2 along C, say v₁ and v₃. Any 5-cycle in G other than C must pass through u and therefore use two edges incident to u; when N_C(u) = {v₁, v₃}, the unique length-3 path in C between v₁ and v₃ is v₁v₅v₄v₃, giving exactly one additional 5-cycle, u·v₁v₅v₄v₃·u. Thus G contains at most 1 + 1 = **2** five-cycles, with equality if and only if G is the (2,1,1,1,1)-blowup of C₅ (where u and v₂ are false twins sharing neighbors {v₁, v₃}). Finally, the automorphism group of this blowup has order 4 (generated by swapping the twins {u, v₂} and reflecting the 5-cycle across the axis through v₂), so the number of labeled extremal graphs on 6 vertices is 6!/4 = 720/4 = **180** — the receipts' exhaustive search over all 32,768 graphs confirms the maximum, its achievers, and their count. The diagnosis: spectral counting plus the balanced-blowup construction — the flag-algebra lecture's leading form (n/5)⁵ made concrete at census scale.

**Answer ◆15 (every STS(v) has v(v−1)/6 triples).** Double count the incidences (p, t) with p a 2-subset of the v points and t a triple containing p. Each of the C(v,2) = v(v−1)/2 pairs lies in *exactly one* triple (the STS axiom); each triple contains exactly 3 pairs. So 3·(#triples) = v(v−1)/2, giving #triples = v(v−1)/6. As a corollary the divisibility necessity of Lecture 4: v(v−1) ≡ 0 (mod 6) — with each point's (v−1)/2 neighbors requiring v odd, this forces v ≡ 1, 3 (mod 6), Kirkman's condition (textbook canon, cited). The tool: P2's double count — one line, the whole design arithmetic.
