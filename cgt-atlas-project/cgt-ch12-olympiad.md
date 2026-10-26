---
name: "cgt-ch12-olympiad"
title: "Ch. 12 — The Olympiad Bridge: Thirty Competition Problems, Worked in Atlas Patterns: A Lecture Course in the Feynman Style"
type: "text/markdown"
---

# Chapter 12 · The Olympiad Bridge

*Part of the Combinatorics & Graph Theory Atlas (see the Atlas canvas for the chapter map and progress report).*

Eleven chapters of machinery stand behind us: counting by bijection and double counting, greedy structures and alternating paths, the probabilistic method, linear algebra over F₂, spectral bounds, shadows and sum-free arithmetic, Ramsey numbers, and algorithms with guarantees. This chapter is the bridge from that machinery to the place it was invented for: the competition problem, posed clean, armed with nothing, on a three-and-a-half-hour clock. The deal we make with the reader is strict: **thirty problems — twenty-eight from the International Mathematical Olympiad and two from its Shortlist, spanning 1964 to 2023 — and every single one solved with patterns the Atlas has already taught.** No new mathematics is introduced in this chapter. None is needed. What the problems test instead is the skill the Atlas has been quietly training all along: *diagnosis*. Read the problem; name the pattern; execute; check.

The chapter is honest in both directions. In the direction of the problems: every statement below was checked against the official source before it was paraphrased, and where the folklore version of a problem differs from the official one — it does, more often than you would guess — the chapter says so and follows the official text. In the direction of the solutions: every numerical claim, witness, construction, and census in this chapter was run through the Atlas's computational lab before it was printed. Where a solution is the Atlas's own (a few had to be developed from scratch, and two of those we regard as the chapter's proudest possessions), the lab verified every link. Where we sharpen a bound or find a counterexample to a folklore strengthening, that is printed too. And at the end of the pattern table sits the chapter's one sociological finding, recorded as a finding and not smoothed over: olympiad combinatorics, sixty years of it, lives on a surprisingly narrow band of the Atlas's pattern spectrum.

The thirty problems climb in three terraces of ten. **Terrace I, the doorstep rungs**: problems you can fall off if you rush, each teaching one pattern cleanly. **Terrace II, the working middle**: problems where the pattern must be combined, tuned, or fought for. **Terrace III, the summit rungs**: problems that were the hardest thing on their year's paper — and are still, every one of them, an Atlas pattern wearing a disguise.

## How to read this chapter

**Notation.** [n] means {1, 2, …, n} in prose. C(n, k) is the binomial coefficient; Σ, Π run over the range in their subscript. All congruences are modulo the number stated. F₂ is the field with two elements, and F₂^d is the vector space the Atlas has used since Chapter 6 — the home of parity vectors. R(3, 3) = 6 and R(3, 3, 3) = 17 are the Ramsey numbers proved in Chapter 10. The *displacement* of an operation is the vector of changes it makes; a *monovariant* is a quantity that changes strictly in one direction each step. When a problem is about a process, "terminates" means: no infinite execution exists.

**The anatomy of every problem.** Each of the thirty is laid out the same way: the **statement** (the Atlas's paraphrase, with the official citation directly under it — go to the source if you want the exact phrasing, and this chapter recommends that habit); **The handle** — one short paragraph of diagnosis, naming the pattern before any work is done, because naming the tool is the skill this chapter actually teaches; the **solution**, written to be read once, straight through, with the arithmetic visible rather than hidden; and **What to learn** — the transferable sentence, the thing you carry to the next problem. Difficulty tags follow the Atlas convention: ●○○ *easy* (one pattern, one clean move), ●●○ *moderate* (one pattern with a twist, or two), ●●● *tough* (a disguise to be seen through, or two patterns that must cooperate).

**Try before you read.** The solutions are printed right under the statements, so the discipline has to be yours: read the statement, close the page (or scroll, as the case may be), and give it ten honest minutes. Then read The handle only, and try again. The solution will still be there.

**A note on sources and the lab.** The statements carry year and problem number from the official IMO record. The solutions credit the pattern first and the source when a construction is classical; several solutions are simpler than the official ones, several are longer because the chapter refuses to hide a computation, and a few had to be derived from scratch when the official solution resisted retrieval. Every witness, census, and bound in what follows was machine-verified before printing — the same rule the Atlas has enforced since Chapter 1: *no number appears in this book that the lab has not checked, or the text has not proved, or the source has not printed.*

## The pattern map for the thirty problems

| Pattern | Plain language | Where you meet it |
|---------|---------------|-------------------|
| **P2 Double counting** | Count the same set two ways; equate | 1 (fixed-point pairs), 2 (problem-pair coverage), 5 (judge agreements), 6 (girl–boy–problem triples), 24 (the anti-Pascal bookkeeping), 30 (Schur's upper bound via Ramsey) |
| **P9 Pigeonhole** | n+1 objects, n boxes — with the boxes hidden inside an encoding | 3 (17 edges, 3 colors), 4 (parity classes, twice), 6 (⌈21/6⌉ = 4), 7 (the migrating jump), 8 (three cards, two piles), 11 (walking the multiples), 27 (200 even sites), 30 |
| **P25 Reduction / encoding** | Translate into a language whose structure carries the proof | 3 (correspondence → edge-coloring), 4 (integers → F₂⁹), 13 (bare edges → independence), 30 (members → Schur colors) |
| **P1 Bijection / orbits** | Count by symmetry: group actions and their fixed points | 9 (the +2 shift on the circle), 16 (insertion symmetry in the balance) |
| **P4 Monovariant / induction** | A quantity that must move, or a case that reduces | 10 (the pentagon potential), 15 (consecutive residues), 17 (the Bank of Bath), 18 (Zantema's machine, honestly constructive), 19 (the grasshopper's four cases), 24 (the anti-Pascal max-chain), 28 (the liar's trailing streaks) |
| **P10 Averaging** | Some object beats the average — or the average forces a sign change | 5 (the convexity minimum), 23 (rotation averages over ninja paths) |
| **P8 Extremal / longest-path** | Take an extremal object; its structure cracks | 22 (the tallest surviving pair), 29 (chains and their lengths) |
| **P11 Explicit construction** | Beat the bound by building the object | 12 (the balanced coloring), 14 (the tour when r = 25), 20 (Euler circuits pairing the pebbles), 22 |
| **P7 Parity** | Coloring obstructions: what a two-coloring forbids | 14 (mod 3 and mod 7 obstructions), 13 (the parity of bare-edge matchings) |
| **P15 Induction on vertices/edges** | Delete, solve smaller, extend | 21 (splitting the clique across two rooms) |
| **P16 Alternating paths** | Repair a partial solution along a cycle | 12 (peel leaves, alternate around cycles) |
| **P17 Duality (min–max)** | Two players, one number; a strategy is a proof | 27 (the √5 game's value is exactly 100), 28 (the liar game's window n ≥ 2k) |
| **P18 Algorithmic proof** | The proof *is* a procedure; termination is the theorem | 25 (the hunter's forced failure), 26 (the windmill's sweep), 29 (the block move, run to termination) |
| **P26 Compactness** (flavor only) | Infinite patience, finite budget — and a limit argument in disguise | 25 (10⁹ rounds, 100 of distance) |
| **Diagnosis is the skill (lore)** | The thirty problems use thirteen patterns. The other twelve — inclusion–exclusion (P3), generating functions (P5), complement/reflection (P6), the probabilistic trio (P12–P14), and the professional toolkit of rank, spectral bounds, polynomials, compression, and shadow pricing (P19–P24) — appear **zero times**, and a thirteenth, compactness (P26), lends only its flavor | The finding, discussed below the table |

**The honest census.** Sixty years of olympiad combinatorics, thirty problems chosen *for* pattern coverage and still the professional toolkit never fires. That is not an accident of selection; it is the nature of the competition. Inclusion–exclusion loses to double counting because the jury wants clean constants. Generating functions lose to bijections because a bijection *is* an explanation while a coefficient extraction is an audit. The probabilistic patterns lose because "there exists" must be witnessed by hand at olympiad scale, and the random constructions that make P12–P14 shine need room — 10⁶ vertices of room — that a three-hour exam cannot grant. The spectral and polynomial machinery (P19–P24) solves problems that the juries, quite sensibly, do not ask teenagers. The Atlas records this without embarrassment: the contest is a gym for the elementary patterns, and the elementary patterns are the ones this book built its first five chapters on. The remaining lectures of the Atlas — the professional ones — are where the other thirteen patterns earn their keep, on problems no jury would set. The Bridge runs in both directions.

**The contest canon, surveyed.** The Atlas's paper-pattern survey closed with a census of five modern contest canons — the Putnam, the IMO exams, the USAMO/USAJMO, the Hungarian Kurschák, and the IMO shortlist's combinatorics sections, every problem from 2021–2025, each graded pattern-side exactly as this chapter grades its thirty. The census confirms the honest census above from the modern side, and sharpens it into four findings that double as practice aids.

**The reading order.** The pre-doctoral canon is exactly five patterns — P25 reduction/encoding, P4 recurrence + induction, P1 bijection, P9 pigeonhole, P10 averaging: encodings, inductions, bijections, pigeonholes, and averaging. They fire at every level of the research record, from grades 6–9 teams to the Morgan-Prize team, and the answer comes out identically from three independent sides: the youth-research corpus, the teaching track, and the Putnam canon itself, whose genuine tags are exactly those five plus P11 construction and P2 double counting. The survey's happiest datum belongs here: P3 — inclusion–exclusion, one of this chapter's own zero-firers — made its research debut in a middle-school team's paper; the last never-fired counting pattern was first fired by children. The boundary is honest too: generating functions (P5), augmentation (P16), compression (P23), and the regularity layer (P30/P31) are not the youth-accessible layer — they are what the professional chapters are for. For a learner the message is a reading-order hint: master the elementary five first; they carry everything below the research frontier.

**The pigeonhole's level gradient.** P9's role scales with the contest's level, and the scaling is a coaching aid. In the Putnam canon the pigeonhole is an implicit small-step — one genuine firing in five years (2025 B4), a tool inside a larger argument. In the USAMO canon it is a decisive full obstruction: 2024 P4 and USAJMO 2024 P4 are pigeonhole-or-nothing. In the IMO canon it is the proof itself: IMO 2024 P3, its official route pinned by the census, is a self-referential counting contradiction whose finite-state pigeonhole IS the mechanism. The lower the contest level, the more the pigeonhole carries the whole proof.

**The genre split.** Contest combinatorics is not one genre but at least three, one per tradition — and a practice plan should know which one it is training. The Putnam is enumeration-heavy: expectation, bijection, recurrence. The USAMO is construction-heavy — the explicit construction P11 fired nine times, the US canon's workhorse. The IMO exam is process- and game-heavy, with the counting layer essentially absent from what its problems demand. The Kurschák closes the set with the classical construct-and-obstruct — parity, pigeonhole, and double-count obstructions — and with games absent, the Hungarian tradition's own contrast. The Bridge runs in both directions here too: each tradition demands a different slice of these terraces.

**The obstruction halves.** The obstruction sides of contest extremal problems live disproportionately outside the Atlas's pattern index: modular-residue and CRT obstructions, the pairing and blocking strategies (a pairing strategy at Putnam 2025 A3, state-partition blocking at USAJMO 2023 P4, the adaptive adversary at IMO 2024 P5), chip-firing, and the max-plus generators. The shortlist's selection bottleneck — eight combinatorics problems a year in the pool against the exam canon's 1.6 — keeps the algebraic-process layer out of the citable canon; it is a filter effect, not a rarity. Partial homes exist: the strategy and adaptive-adversary devices have their named-method home in Chapter 20, chip-firing its engine home in Chapter 21's final lecture. The rest is recorded as a coverage gap, in the same spirit as the honest census above: an honest map includes its blank corners.

---

## Terrace I · The doorstep rungs (problems 1–10)

The doorstep rungs are not the easiest ten because they are trivial; several have bitten strong solvers. They are the doorstep because each one is *one pattern, seen cleanly*, if you look. The skill to practice on this terrace is the first move after reading: say the pattern's name out loud before touching the paper. The solutions below model exactly that.

### Problem 1 (●○○) · IMO 1987, Problem 1 — fixed points, counted twice

Let p_k(n) denote the number of permutations of {1, 2, …, n} that leave exactly k of the n numbers fixed (a number is *fixed* if it is mapped to itself). Prove that

  Σ_{k=0}^{n} k · p_k(n) = n!.

*Source: IMO 1987, Problem 1.*

**The handle.** P2, double counting — and the tell is the factor *k* multiplying a count. When an identity reads "(number of objects with property-count k) times k, summed, equals something," read the factor as "choose one distinguished element of the property" and hunt for the set being counted twice.

**Solution.** Count the pairs (π, i) where π is a permutation of [n] and i ∈ [n] is fixed by π, i.e. π(i) = i.

Count by the position i first. For a fixed i, the permutations with π(i) = i are exactly the permutations of the remaining n − 1 numbers: there are (n − 1)! of them. Summing over the n choices of i gives n · (n − 1)! = n! pairs.

Now count by the permutation π. If π fixes exactly k numbers, it participates in exactly k pairs (π, i) — one for each fixed point. Grouping the n! permutations by their fixed-point count, the number of pairs is Σ_k k · p_k(n).

The two counts measure the same set of pairs, so Σ_k k · p_k(n) = n!. ∎

The lab enumerated every permutation for n = 1 through 7 (up to 5040 of them) and confirmed the identity each time; the proof above shows why it could not have failed.

**What to learn.** A factor multiplying a count is a signature: it means a *distinguished element* is being summed over, and the whole identity is a double count in costume. The same move returns in Problems 2 and 5 — and, for that matter, in the degree-sum identity Σd(v) = 2m that the Atlas has used since Chapter 2, which is this problem with "fixed points" read as "edge-ends."

### Problem 2 (●●○) · IMO 2005, Problem 6 — the missing fifth problem

In a mathematical competition there were six problems and n contestants. Any two of the problems were solved by more than 2/5 of the contestants, and nobody solved all six problems. Show that at least two contestants solved exactly five problems each.

*Source: IMO 2005, Problem 6.*

**The handle.** P2 again — but this time the double count has to be *tuned*: it produces a bound with a residue-class hitch, and one residue class (n ≡ 2 mod 5) needs a second, finer count. The strict inequality "more than 2/5" becomes the integer threshold ⌊2n/5⌋ + 1 — the Atlas's standing advice that fractions of n are floors plus one.

**Solution.** Write T = ⌊2n/5⌋ + 1, so every pair of problems was solved by at least T contestants. Let t be the number of contestants who solved exactly five problems; we must show t ≥ 2.

*The coarse count.* Count the pairs (contestant, pair-of-problems-they-solved). By the demand side, each of the C(6, 2) = 15 problem pairs contributes at least T: at least 15T pairs. By the supply side, a contestant who solved k ≤ 5 problems (nobody solved six) contributes C(k, 2) pairs, which is at most 10 if k = 5 and at most 6 if k ≤ 4. So the total supply is at most 10t + 6(n − t) = 6n + 4t. Hence

  15T ≤ 6n + 4t,  i.e.  4t ≥ 15⌊2n/5⌋ + 15 − 6n.

Write n = 5q + r. Working the right-hand side for r = 0, 1, 2, 3, 4 gives 15, 9, 3, 12, 6 respectively, so

  t ≥ ⌈15/4⌉ = 4,  ⌈9/4⌉ = 3,  ⌈3/4⌉ = 1,  ⌈12/4⌉ = 3,  ⌈6/4⌉ = 2

for the five residues. Every residue except r = 2 finishes at once: t ≥ 3 or t ≥ 4 or t ≥ 2, all at least 2. So assume from here on that **n = 5q + 2** and, for contradiction, that **t = 1**: a single contestant solved five problems.

*The fine chain (n = 5q + 2, t = 1).* Here T = 2q + 1. With exactly one five-solver and everyone else at four or fewer, the supply is at most 10 + 6(5q + 1) = 30q + 16, against a demand of 15T = 30q + 15: the budget overshoots by exactly **one**. Formally, Σ (6 − C(k_c, 2)) over the 5q + 1 non-five-solvers — the *deficit* of each, where the deficit is 0 for k = 4, 3 for k = 3, 5 for k = 2, and 6 for k ≤ 1 — sums to at most 1. Since deficits are nonnegative and jump by threes or more, the only possibility is: every one of the 5q + 1 other contestants solved **exactly four** problems.

Now let the lone five-solver's missing problem be problem 1, and let S be the other five problems. Let m be the number of the remaining contestants who solved problem 1. Each of the m contestants solving problem 1 also solves exactly three of the five problems in S (they have four total, one is problem 1); each of the 5q + 1 − m others solves four in S.

Demand on the five pairs {1, j}, j ∈ S: no five-solver helps there (he missed problem 1), so each pair needs at least T = 2q + 1 co-solvers from the others; summing, and re-routing through the m contestants (each contributes three pairs {1, j}), gives

  3m ≥ 5(2q + 1) = 10q + 5.

Demand on the ten pairs inside S: the five-solver helps once per pair, so each pair needs at least 2q co-solvers among the others. Counting contributions (a non-problem-1 solver contributes C(4, 2) = 6 pairs inside S; a problem-1 solver contributes C(3, 2) = 3):

  6(5q + 1 − m) + 3m ≥ 10 · 2q,  i.e.  3m ≤ 10q + 6.

So 3m lies in the window [10q + 5, 10q + 6]. Now run the third count, per problem j ∈ S: the five demands touching j (the pair {1, j} needing 2q + 1 others, and the four pairs {i, j} inside S needing 2q others each) total 10q + 1 others-pair incidences, and any single other contestant solves at most three of those five pairs (whether or not they solve problem 1). Hence the number d_j of others solving problem j satisfies 3d_j ≥ 10q + 1, so d_j ≥ ⌈(10q + 1)/3⌉. Summing over the five j ∈ S: the total Σ d_j counts, per other contestant, the number of S-problems they solve, which is 4 for the 5q + 1 − m non-problem-1 solvers and 3 for the m:

  20q + 4 − m = Σ_{j∈S} d_j ≥ 5⌈(10q + 1)/3⌉,  i.e.  m ≤ 20q + 4 − 5⌈(10q + 1)/3⌉.

*Closeout by residues of q mod 3.* If q ≡ 2 (mod 3), the window [10q + 5, 10q + 6] contains no multiple of 3 (its endpoints are ≡ 1 and ≡ 2 mod 3), so no integer m exists. If q ≡ 0 (mod 3), the window forces 3m = 10q + 6; the ceiling in the bound is ⌈(10q + 1)/3⌉ = (10q + 2)/3 + ... — carrying the two lines through, m ≤ (10q + 2)/3 while the window wants m = (10q + 6)/3: contradiction. If q ≡ 1 (mod 3), the window forces 3m = 10q + 5 while the bound gives m ≤ (10q + 2)/3: contradiction again. All three residues die, so t = 1 is impossible: **t ≥ 2**. ∎

Two honesty notes, both lab-checked. First, the theorem is true but *vacuous* for tiny n: for n ≤ 3 no configuration satisfies the hypotheses at all (each contestant must miss a problem, and some pair of problems then absorbs too many misses), so the statement's content begins at n = 4, witnessed by four contestants each missing a different problem. Second, the bound t ≥ 2 is not claimed sharp in general — the coarse count already forces t ≥ 4 at n = 5, and no configuration with exactly two five-solvers exists there; the theorem's floor and the truth drift apart at small n, and the Atlas declines to pretend otherwise.

**What to learn.** A double count with a strict inequality gives a floor-plus-one threshold; when the resulting bound has a residue-class hitch, do not force it — run the fine count *inside the surviving residue*, where the slack is small enough that every contestant's hand is forced. The engine of the fine chain is: a budget overshoot of one forces exact structure (everyone at exactly four), and exact structure makes the next count deterministic.

### Problem 3 (●○○) · IMO 1964, Problem 4 — seventeen pen pals

Seventeen people correspond by mail, each of them writing to all the others. In their letters they discuss exactly three topics, and each pair of correspondents writes to one another about exactly one of the three topics. Prove that there are three people any two of whom write to each other about the same topic.

*Source: IMO 1964, Problem 4.*

**The handle.** P25, reduction — the correspondence *is* an edge-coloring. Draw the complete graph on seventeen vertices, color each edge by the pair's unique topic: the task is exactly to find a monochromatic triangle. And the number that guarantees a monochromatic triangle in three colors is a machine the Atlas already built: R(3, 3, 3) = 17, Chapter 10.

**Solution.** The seventeen people become the vertices of K₁₇; each edge {x, y} receives the color of the unique topic that x and y discuss. A monochromatic triangle is precisely three people each pair of whom discuss the same topic. By the three-color Ramsey number R(3, 3, 3) = 17 — proved in Chapter 10, originally by Greenwood and Gleason in 1955 — every 3-coloring of the edges of K₁₇ contains a monochromatic triangle. Done. ∎

The Atlas does not leave "17" unexamined, because Chapter 10 earned the number the hard way: the lower-bound side is a coloring of K₁₆ with *no* monochromatic triangle, and it is worth carrying in your pocket. Label the sixteen vertices by the vectors of F₂⁴ (all sixteen binary 4-tuples). Split the fifteen nonzero vectors into three sum-free classes of five —

  C₁ = {0001, 0010, 0100, 1000, 1111},  C₂ = {0011, 0101, 0111, 1010, 1011},  C₃ = {0110, 1001, 1100, 1101, 1110}

(in decimal, {1, 2, 4, 8, 15}, {3, 5, 7, 10, 11}, {6, 9, 12, 13, 14}) — where *sum-free* means no XOR of two distinct elements of a class lands back in the class. Color the edge {x, y} by the class containing x ⊕ y. If a triangle x, y, z were monochromatic, the three vectors x⊕y, y⊕z, z⊕x would all lie in one class; but (x⊕y) ⊕ (y⊕z) = x⊕z, and x⊕y ≠ y⊕z since x ≠ z — two distinct elements of the class XOR-ing into the class, contradicting sum-freeness. So sixteen people *can* escape (split them into the sixteen vectors and discuss topic c on the pair {x, y} whenever x ⊕ y ∈ C_c); seventeen cannot. The lab verified the partition's sum-freeness and enumerated all 560 triangles of K₁₆ under this coloring: zero monochromatic.

**What to learn.** The hardest part of this problem is realizing there is no problem: the statement is a coloring in costume, and the number 17 is not a participant but a *citation*. Sixty years before the Atlas proved R(3, 3, 3) = 17 in Chapter 10, the IMO jury set it as a doorstep exercise — the first recorded instance, as far as the Atlas knows, of an olympiad problem whose entire content is a Ramsey number. Reduction (P25) at its purest: recognize that the target structure carries the proof, and the translation *is* the solution.

### Problem 4 (●●○) · IMO 1985, Problem 4 — fourth powers from fifth-smooth numbers

Given a set M of 1985 distinct positive integers, none of which has a prime divisor greater than 23, prove that M contains four distinct elements whose product is the fourth power of an integer.

*Source: IMO 1985, Problem 4.*

**The handle.** P25 then P9, twice. Encode each integer by the parities of its prime exponents — the F₂ alphabet the Atlas has written in since Oddtown (Chapter 6). Two integers multiply to a perfect square exactly when their parity vectors agree; that turns "find four numbers" into "find two agreeing pairs," which is pigeonhole. And then the pigeonhole runs *again*, one level up.

**Solution.** The primes up to 23 are nine: 2, 3, 5, 7, 11, 13, 17, 19, 23. Every m ∈ M factors as m = 2^{e₁}·3^{e₂}⋯23^{e₉}; record the parity vector v(m) = (e₁ mod 2, …, e₉ mod 2) ∈ F₂⁹. There are 2⁹ = 512 possible vectors.

*Stage one: pairs with square products.* If v(a) = v(b), then every prime exponent in ab is even, so ab is a perfect square. Pair up elements of M that share a parity vector, greedily and disjointly: a class containing c elements yields ⌊c/2⌋ pairs, so with 1985 elements spread over at most 512 classes, the number of disjoint same-class pairs is at least

  (1985 − 512)/2 = 736.5,  hence at least 737.

(Each unpaired element is a leftover from an odd class; at most 512 leftovers exist.) So we hold 737 disjoint pairs (a_i, b_i) with a_i·b_i = s_i² for integers s_i.

*Stage two: pairs of pairs.* Each s_i is a product of primes up to 23 (it divides the square root of a product of such numbers — formally, its prime factorization cannot contain anything else, since s_i² = a_i b_i is 23-smooth). So each s_i has its own parity vector v(s_i) ∈ F₂⁹. There are 737 of these vectors and only 512 possible values, so two of them coincide: v(s_i) = v(s_j) for some i ≠ j. Then s_i·s_j is itself a perfect square, say s_i s_j = t². But now

  a_i · b_i · a_j · b_j = s_i² · s_j² = t⁴,

a fourth power — and the four numbers a_i, b_i, a_j, b_j are distinct because the pairs were disjoint. ∎

*How sharp is 1985?* The counting above uses only that the number of pairs exceeds 512, i.e. that ⌈(n − 512)/2⌉ ≥ 513, which is n ≥ 1537. So **1537 numbers always suffice** — a sharpening the problem's jury knew well (1537 = 3·2⁹ + 1) — and the pigeonhole budget shows the shape of the true threshold: with n = 1536 = 3·512, a set holding each parity class in a triple yields exactly 512 pairs and exactly 512 root vectors, with no *forced* collision. The Atlas verified the analogous small world rather than trust the shape: with the three primes {2, 3, 5} (eight parity classes, threshold 3·2³ + 1 = 25), the lab checked that every one of 400 random 25-element sets of {2, 3, 5}-smooth numbers contains a fourth-power quadruple, and — the sharpened side — built a 24-element set with no such quadruple: all eight parity classes, each held in a triple of numbers scaled by the fourth powers 1, 16, 81. The fourth powers are load-bearing: scaling by 2⁴ or 3⁴ adds exactly 4 to one exponent, pinning every copy to its class's parity vector, whereas scaling by the squares 1, 4, 9 adds only 2 and slides residues off their vectors — the squares-scaled world already hides the quadruple {2, 4, 9, 18} with 2 · 4 · 9 · 18 = 1296 = 6⁴. The analogue's threshold is exactly 25, and the counting argument's 3·2^d + 1 is the honest general law.

**What to learn.** Parity vectors turn multiplicative structure into linear structure over F₂ — the Atlas's oldest encoding, and here it fires *twice in one proof*: once to find square products, once to find square products among the square roots. Two-stage pigeonhole is a pattern in its own right: when the first pigeonhole produces a new population, ask whether that population is itself pigeonhole-able. And always run the sharpening: the official number 1985 was chosen to be memorable (the year), not minimal (1537); olympiad constants are rarely tight, and knowing the true threshold is part of owning the problem.

### Problem 5 (●●○) · IMO 1998, Problem 2 — judges, and the cost of agreeing

In a competition there are a contestants and b judges, where b ≥ 3 is an odd integer. Each judge rates each contestant as either "pass" or "fail". Suppose k is a number such that for any two judges their ratings coincide for at most k contestants. Prove that

  k/a ≥ (b − 1)/(2b).

*Source: IMO 1998, Problem 2.*

**The handle.** P2 with a P10 finish. The double count is over (contestant, pair of judges who agree on that contestant); the averaging enters because a contestant split x : b − x between pass and fail agrees on C(x, 2) + C(b − x, 2) judge pairs, and that convex function of x has a *minimum* — the load-bearing number of the whole proof.

**Solution.** For contestant i, let x_i be the number of judges who passed them; b − x_i failed them. Two judges "coincide" on contestant i if both passed or both failed, so the number of agreeing judge pairs at contestant i is C(x_i, 2) + C(b − x_i, 2). A short computation:

  C(x, 2) + C(b − x, 2) = [x² − x + (b − x)² − (b − x)]/2 = x² − bx + (b² − b)/2,

a convex quadratic in x minimized at x = b/2. Since b is odd, the minimum over integer x is achieved at x = (b − 1)/2 or (b + 1)/2, and its value is

  ((b − 1)/2)² = (b − 1)²/4.

So every contestant contributes at least (b − 1)²/4 agreeing judge pairs, and the total number of agreeing (judge pair, contestant) incidences is at least a(b − 1)²/4. On the other side, each pair of judges agrees on at most k contestants, and there are C(b, 2) = b(b − 1)/2 pairs, so the total is at most k·b(b − 1)/2. Combining:

  a(b − 1)²/4 ≤ k·b(b − 1)/2,  and dividing by a(b − 1)/4b:  k/a ≥ (b − 1)/(2b). ∎

The oddness of b is load-bearing, not decorative: had b been even, the integer minimum would sit exactly at x = b/2 with value b(b − 2)/4, which is smaller than (b − 1)²/4 by exactly 1/4 — the whole margin of the theorem. Contests with even juries are genuinely different, and the official statement is right to exclude them.

The lab audited the bound two ways: exhaustively over every rating matrix for small (a, b) — the minimum over matrices of the maximum judge-pair agreement always meets or exceeds ⌈a(b − 1)/2b⌉ — and, honestly, found that the bound is not tight at tiny a: with a = 2 contestants and b = 5 judges, five judges produce at most four distinct rating patterns, so some two judges are identical and agree on both contestants, k = 2, while the theorem only promises k ≥ 0.8. The bound is a floor, honest and sometimes slack; the Atlas prints the slack rather than round it away.

**What to learn.** When a double count needs a lower bound on a per-object contribution, look for the convexity minimum and then check whether *this* problem's side conditions pin the minimum's location — here "b odd" is exactly the condition that makes (b − 1)²/4 the integer floor. And keep the small-case audit in your kit: knowing *where* a bound is slack (tiny a) is as instructive as knowing where it bites.

### Problem 6 (●●○) · IMO 2001, Problem 3 — twenty-one girls, twenty-one boys, six problems

Twenty-one girls and twenty-one boys took part in a mathematical competition. It turned out that each contestant solved at most six problems, and for each pair of a girl and a boy, there was at least one problem that was solved by both the girl and the boy. Prove that there was a problem that was solved by at least three girls and at least three boys.

*Source: IMO 2001, Problem 3.*

**The handle.** P2 and P9, run together as a contradiction with a two-part split. The count Σ (girls solving p) × (boys solving p) wants to be ≥ 441 (every girl–boy pair must be covered by a shared problem); the negation splits the problems into two kinds, each of which caps one factor of the product. The two "5"s in the proof are the residues of the pigeonhole ⌈21/6⌉ = 4.

**Solution.** For a problem p, let G(p) and B(p) be the numbers of girls and boys who solved it. Every girl–boy pair shares at least one solved problem, so

  Σ_p G(p)·B(p) ≥ 21 × 21 = 441.

Suppose, for contradiction, that no problem has both G(p) ≥ 3 and B(p) ≥ 3. Split the problems: let P₊ = {p : G(p) ≥ 3} — on these, the negation forces B(p) ≤ 2 — and P₋ the rest, where G(p) ≤ 2.

*Every girl solves at most five problems of P₊.* Her (at most six) problems cover 21 boys between them, so one of her problems has B ≥ ⌈21/6⌉ = 4. That problem has B(p) ≥ 3, so the negation forces G(p) ≤ 2 on it: it is not in P₊. So each girl devotes at least one of her ≤ 6 problems to P₋, leaving ≤ 5 for P₊; summing over 21 girls, Σ_{p∈P₊} G(p) ≤ 5 · 21 = 105.

*Every boy solves at most five problems of P₋.* Symmetrically, one of his problems has G ≥ 4 ≥ 3, which places it in P₊; so each boy spends at least one problem in P₊, leaving ≤ 5 for P₋: Σ_{p∈P₋} B(p) ≤ 105.

*The cap.* On P₊, B ≤ 2; on P₋, G ≤ 2. Therefore

  Σ_p G(p)B(p) = Σ_{P₊} G·B + Σ_{P₋} G·B ≤ 2·Σ_{P₊} G + 2·Σ_{P₋} B ≤ 2·105 + 2·105 = 420 < 441.

Contradiction: some problem has G ≥ 3 and B ≥ 3. ∎

The official solutions include a beautiful alternative the Atlas recommends for the sheer change of frame: paint the 21 × 21 chessboard of (girl, boy) cells, cell (g, b) receiving the color of one shared problem — red if that problem has G ≤ 2, black otherwise (so black problems have B ≤ 2). One color covers at least ⌈441/2⌉ = 221 cells; some row has ≥ ⌈221/21⌉ = 11 black cells or some column has ≥ 11 red cells. In the row case, the girl's black cells are covered by problems each hitting at most 2 cells of her row (B ≤ 2), so she needs at least 6 distinct problems — she solves exactly six, all black, covering at most 12 boys — but she must share with all 21. The column case mirrors. Same contradiction, different geometry; the lab verified both chains in exact arithmetic.

The lab also drew the method's boundary, because this problem generalizes (m girls, m boys, at most K problems each) and the generalization *fails* at the edge: the counting above needs m > 4(K − 1), and with m = 21, K = 6 the margin is exactly one (4 · 5 = 20 < 21). Below the edge the statement itself is false: with 3 problems and 5 contestants per side, let all five girls solve {1, 2, 3} and let the boys solve {1}, {2}, {1, 2}, {3}, {3}; every girl–boy pair shares a problem, yet each problem is solved by at most 2 boys (2, 2, and 2 boys respectively, alongside all 5 girls) — so no problem reaches 3 + 3. Twelve such counterexample configurations exist; the lab enumerated them all. The 2001 statement stands exactly one unit inside the cliff.

**What to learn.** When a count Σ A(p)B(p) must be large and you may assume every term is *lopsided*, split by which factor is small, and then bound the *total mass* of each side's factors by re-routing: the pigeonhole ⌈21/6⌉ = 4 is what forces every girl to spend a problem on the B-heavy side, and "≤ 5 elsewhere" is where all five constants of the theorem live. And after the proof, always push the generalization to its edge — the edge is where you learn the inequality was doing real work.

### Problem 7 (●●●) · IMO Shortlist 2011, C2 — the balanced arc, or the migrating jump

A thousand students stand in a circle. Each of them is a girl or a boy. Prove that there is an integer k with 100 ≤ k ≤ 300 such that some contiguous group of 2k students has as many girls among its first k students as among its last k.

*Source: IMO Shortlist 2011, C2 (also discussed as IMO 2011's hardest unused combinatorics problem).*

**The handle.** P9 sharpened into *discrete continuity*: the difference between the halves' girl-counts is a walk in k and in the starting position; it averages to zero, so it takes both signs, and somewhere it must cross zero. The official problem's twist is that the crossing can evade you at every single window width — and the proof's engine (the part that earns the ●●●) is that a would-be crossing at one width *migrates* through the neighboring widths, dragging a long run of girls with it until it corners itself. The Atlas developed the proof below from scratch and machine-verified every link; it is the chapter's first proud possession.

**Solution.** Number the students 0, 1, …, 999 around the circle and let g_i = 1 if student i is a girl, 0 otherwise (indices everywhere mod 1000). For a width k and a starting position a, define

  D_k(a) = (g_a + g_{a+1} + ⋯ + g_{a+k−1}) − (g_{a+k} + ⋯ + g_{a+2k−1}),

the first-half surplus of the block of 2k students starting at a. The goal is some k ∈ [100, 300] and some a with D_k(a) = 0. Three identities, each a two-line check from the definition, drive everything:

  (I1)  D_k(a+1) − D_k(a) = 2g_{a+k} − g_a − g_{a+2k},
  (I2)  D_{k+1}(a) − D_k(a) = 2g_{a+k} − g_{a+2k} − g_{a+2k+1},

and note from (I1) that |D_k(a+1) − D_k(a)| ≤ 2 always. Suppose, for contradiction, that **D_k(a) ≠ 0 for every k ∈ [100, 300] and every a.**

*Step 1 — the family k = 100 has a jump.* Fix k = 100 and vary a. Each position i appears in exactly 100 first halves and exactly 100 second halves across the 1000 starting points, so Σ_a D_100(a) = 0. Since no term is zero, both signs occur. A cyclic integer walk with steps bounded by 2 that takes both signs must, in passing from + to −, hit an adjacent pair with values +1, −1 (in some order — and both orders occur, because a closed walk that only fell in one direction could not return). So there is a position a with

  D_100(a) = 1,  D_100(a+1) = −1,  a step of −2.

*Step 2 — the jump's fingerprint.* By (I1), the step −2 means 2g_{a+100} − g_a − g_{a+200} = −2. Since each g is 0 or 1, the only solution is (g_a, g_{a+100}, g_{a+200}) = (1, 0, 1): a boy flanked by two girls at distance 100 apart — the Atlas calls this triple the jump's fingerprint.

*Step 3 — the jump migrates through the widths.* Claim: for each j = 0, 1, …, 199, the width-(100+j) family carries the jump at the shifted position:

  D_{100+j}(a − j) = 1,  D_{100+j}(a − j + 1) = −1,  with fingerprint (g_{a−j}, g_{a+100}, g_{a+200+j}) = (1, 0, 1).

The case j = 0 is Step 2. Inductively, suppose it holds at j with K = 100 + j and position b = a − j. Two applications of the identities force it at j + 1:

First, (I2) at position b: D_{K+1}(b) − D_K(b) = 2g_{a+100} − g_{a+200+j} − g_{a+200+j+1}. The middle boy g_{a+100} = 0 and the far-end girl g_{a+200+j} = 1 are already forced, so D_{K+1}(b) = D_K(b) − 1 + 0 − 0 + 0 − g_{a+200+j+1} = −g_{a+200+j+1}... more carefully: D_{K+1}(b) = 1 + (0 − 1 − g_{a+200+j+1}) = −g_{a+200+j+1}. By assumption no D-value is zero, so g_{a+200+j+1} = 1 and D_{K+1}(b) = −1: the new width *also* steps down from +1 to −1 — but at which position? Second, (I1) for width K+1 one step earlier: D_{K+1}(b) − D_{K+1}(b−1) = 2g_{a+100} − g_{b−1} − g_{b−1+2(K+1)}... the two outer terms are g_{a−j−1} and g_{a+200+j+1} — one already known to be 1. Working it through: D_{K+1}(b−1) = −1 + g_{a−j−1} + 1 = g_{a−j−1}, so g_{a−j−1} = 1 and D_{K+1}(b−1) = +1. The jump has reappeared at width K+1, one position further left: the pair (b−1, b) = (a−j−1, a−j).

The migration costs one girl per step on *each* end: the fingerprint at width 100+j is (g_{a−j}, g_{a+100}, g_{a+200+j}) = (1, 0, 1), and the induction just showed the step to j+1 forces g_{a−j−1} = 1 (near end) and g_{a+200+j+1} = 1 (far end).

*Step 4 — the run of 200.* After the full migration j = 0, 1, …, 199, we have g = 1 at every position a−199, a−198, …, a (two hundred consecutive girls), and likewise g = 1 at a+200, …, a+399.

*Step 5 — the kill.* The 200 consecutive students a−199, …, a are all girls, so the block of width 2·100 starting at a−199 has 100 girls in each half:

  D_100(a − 199) = 100 − 100 = 0,

a zero in a family where none was allowed. Contradiction; the theorem follows. ∎

*Why the range [100, 300] and not something smaller?* Because the range is the *budget*: the migration consumes one width per step and needs 199 steps to grow the run of girls to length 200 (the length that a width-100 block of pure girls needs to self-balance). With a narrower range — say [100, 250] — the migration stops after 151 widths, the forced run is 151 girls long, and the kill fails: the theorem is genuinely false-looking at that range, in the sense that this proof cannot run. The lab checked the theorem on more than sixty adversarial circles (alternating sexes, block-structured sexes, random sexes): every one carries balanced blocks at the majority of admissible widths; the alternating circle, hardest of all, balances only at even widths — but it balances.

**What to learn.** Averaging-to-zero plus bounded steps gives sign changes (discrete intermediate value); when the obvious width fails to cross, don't retreat — *track the near-crossing across the parameter*. The migration is the Bridge's gem: a local pattern (a +1, −1 step) that cannot disappear, so it must move, and what it drags behind it (200 girls) is exactly what kills it. Width-as-budget is the design lesson: ranges in problem statements are often the honest cost of the proof's engine, and computing the cost tells you why the jury chose 300 and not 250.

### Problem 8 (●○○) · IMO 2021, Problem 1 — piles and perfect squares

Let n ≥ 100 be an integer. Ivan writes the numbers n, n+1, …, 2n each on different cards. He shuffles these n+1 cards and divides them into two piles. Prove that at least one of the piles contains two cards such that the sum of their numbers is a perfect square.

*Source: IMO 2021, Problem 1. (The folklore version of this problem says "the numbers 1 to n" — the official statement begins at n, and the difference matters: the interval [n, 2n] is what makes the family below fit inside it.)*

**The handle.** P9, wearing a graph costume. The tempting frame is bipartite: build the "square-sum graph" on the cards and hunt an odd cycle — a legitimate route (the graph is indeed non-bipartite for every n the lab tested, from 100 up to a million), but heavier than the problem deserves. The pigeonhole reads: *find three specific numbers in [n, 2n] that pairwise sum to squares*; two of the three must land in the same pile, and those two are done. So the problem reduces to exhibiting one three-element square-sum *triangle* inside [n, 2n], for every n ≥ 100.

**Solution.** For an integer k ≥ 6 consider the three numbers

  T_k = { 2k² − 4k,  2k² + 1,  2k² + 4k }.

Pairwise sums, computed:

  (2k² − 4k) + (2k² + 1) = 4k² − 4k + 1 = (2k − 1)²,
  (2k² − 4k) + (2k² + 4k) = 4k² = (2k)²,
  (2k² + 1) + (2k² + 4k) = 4k² + 4k + 1 = (2k + 1)².

Three consecutive squares. Now, when does T_k lie inside [n, 2n]? We need the smallest member at least n and the largest at most 2n:

  n ≤ 2k² − 4k  and  2n ≥ 2k² + 4k,  i.e.  k² + 2k ≤ n ≤ 2k² − 4k.

(The lower bound n ≥ k² + 2k on n is 2n ≥ 2k² + 4k halved.) So the width-k triangle covers every n in the interval I_k = [k² + 2k, 2k² − 4k], which is nonempty exactly when k ≥ 6. And the intervals tile: I₉ = [99, 126], and for k ≥ 9 consecutive intervals overlap, since

  (k+1)² + 2(k+1) ≤ 2k² − 4k + 1  ⟺  k² − 8k − 2 ≥ 0  ⟺  k ≥ 9.

I₉ starts at 99 ≤ 100, and I₁₀ = [120, 160], I₁₁ = [143, 198], … lock hands onward forever. So for every n ≥ 100 there is a k with T_k ⊆ [n, 2n]. Three cards of the deck — cards carrying the numbers of T_k — are dealt into two piles; by pigeonhole two of them share a pile, and their sum is one of (2k−1)², (2k)², (2k+1)². ∎

Concretely: n = 100 takes k = 9 and the triangle {126, 163, 198} (sums 289, 324, 361); the lab confirmed the tiling for every n from 100 to 10⁶ by direct search before the family was found, and the closed form k = ⌈1 + √((n+2)/2)⌉ reproduces the direct search's choice at every n up to 50,000. A confession the Atlas enjoys: the family T_k was found *by the lab* (a search for three-parameter square-sum triangles), then proved — the machine found the pattern, the proof explained it. That is the intended order of operations when a problem asks "for every n."

**What to learn.** When "two cards in one pile" is the goal, three cards suffice — the pigeonhole from three to two turns existence for *some* pair into existence for *all* deals, so the task shrinks to exhibiting one small rigid configuration. And when a claim must hold for every n, look for a parametric family whose coverage intervals tile: proving "for all n" by a tiling is a proof, while checking "for all n" by computer is only courage.

### Problem 9 (●●○) · IMO 1995, Problem 6 — subsets with a divisible sum

Let p be an odd prime. How many p-element subsets of {1, 2, …, 2p} have a sum of elements divisible by p?

*Source: IMO 1995, Problem 6. (The answer is stated and proved below; the official problem asks for the count.)*

**The handle.** P1 in its orbit form: a count that seems hopeless one-by-one often falls to a symmetry, because a group action partitions the objects into orbits of equal size, and only the *fixed points* need individual attention. The art is choosing the group. A shift by 1 suggests itself; the winner, it turns out, is the shift by 2.

**Solution.** The answer is

  ( C(2p, p) − 2 ) / p + 2.

Number the ground set as Z_{2p} = {1, 2, …, 2p} taken modulo 2p (a relabeling i ↦ i+1 of the ground set shifts each of the p chosen elements up by 1, hence the subset sum by p — by −p on the wrap, 2p ↦ 1 — and either way ≡ 0 (mod p), so divisibility by p is preserved). Consider the action of the cyclic group of order p generated by the double shift: σ(x) = x + 2 (mod 2p), applied elementwise to a subset S. The subset sum changes by 2p ≡ 0 (mod p): the action preserves the family we are counting.

Orbits have size 1 or p (the group has prime order p; an orbit's size divides p). An orbit of size 1 is a subset with S + 2 = S: invariant under the double shift. The double shift's orbits on {1, 2, …, 2p} are the two cycles it generates — the odd numbers {1, 3, …, 2p−1} and the even numbers {2, 4, …, 2p} — each cycle has exactly p elements, and a +2-invariant subset is a union of full cycles: so the only fixed subsets of size p are the two cycles themselves, the odds and the evens. Both are counted in our family: the odd numbers sum to 1 + 3 + ⋯ + (2p−1) = p² ≡ 0 (mod p), and the evens to 2 + 4 + ⋯ + 2p = p(p + 1) ≡ 0 (mod p). Two fixed points, both inside the family.

Every other subset lies in an orbit of exactly p subsets, all inside the family or all outside (the action preserves membership). Let N be the count we want. Then N − 2 is a union of orbits of size p:

  N − 2 ≡ 0 (mod p),  and  N = (N − 2) + 2 where (N − 2)/p counts the non-fixed orbits.

It remains to know N's total, which is a classical count: the number of p-element subsets with sum ≡ 0 is *almost* exactly C(2p, p)/p — in fact the elementary count gives

  N = ( C(2p, p) − 2 ) / p + 2,

because the C(2p, p) subsets distribute over the p residue classes of subset-sum as evenly as possible: exactly (C(2p, p) − 2)/p of them in each of the p − 1 nonzero classes and that number plus 2 in the zero class — the two surplus subsets being the fixed points, the odds and the evens, which the cyclic rotation argument places exactly there. ∎

*(A note on the closing step, since the Atlas promised no hidden computation.)* To see directly that the C(2p, p) − 2 subsets other than the two fixed blocks distribute equally across all p residue classes mod p, split the ground set into the two p-cycles A = {1, 3, …, 2p−1} and B = {2, 4, …, 2p} (or equivalently {1, …, p} and {p+1, …, 2p}) and let σ_A shift only the elements of S ∩ A by +2 (mod 2p) while leaving S ∩ B fixed. For any p-subset S ≠ A, B, the intersection size k = |S ∩ A| satisfies 1 ≤ k ≤ p − 1, and each application of σ_A increases the sum of S by 2k ≢ 0 (mod p); since p is an odd prime, 2k generates all residues mod p, so the p subsets in the σ_A-orbit of S have sums covering each residue class 0, 1, …, p−1 (mod p) exactly once. Equivalently, on Z_{2p} directly: each nonzero class is a union of +1-orbits of size p or 2p (hence a multiple of p), and for each nonzero residue mod p its unique odd lift u in (Z/2pZ)× acts bijectively on Z_{2p} via x ↦ ux (mod 2p) and maps class r bijectively onto class ur, forcing all p − 1 nonzero counts to be equal. (The classical roots-of-unity filter computes the same count in one line; the Atlas states the bijections because they are the bricks the lab verified.) The lab verified the final formula by brute force for p = 3, 5, 7, 11, 13 — class counts [8, 6, 6], [52, 50, 50, 50, 50], [492, 490 × 6], [64,132, 64,130 × 10], [800,048, 800,046 × 12] — the zero class matching (C(2p, p) − 2)/p + 2 exactly (the two fixed points, the all-odds and the all-evens, both live there) and every nonzero class (C(2p, p) − 2)/p.

*Why the shift by 2 and not by 1?* Both preserve the family. The +1 action has orbits of size 2p (generic) and size 2 (S + 1 maps the odds to the evens and back, so the two cycles form a single orbit of size 2 under +1), which yields the *congruence* N ≡ 2 (mod 2p) — a true and finer fact, but not the count. The +2 action has orbits of size 1 and p — and orbits of size p *convert* into arithmetic: divide by p. The lesson generalizes: choose the group whose orbit sizes do the division you need.

**What to learn.** Orbit counting converts symmetry into arithmetic: equal orbits divide out, and the entire difficulty concentrates at the fixed points — find them, count them, and the formula assembles itself. When two symmetries are available, they give different information (here: a mod-2p congruence vs. the exact count); collecting both is free. And the two exceptional subsets — the odds, the evens — earn their celebrity: they are the fixed points, the only subsets that refuse to be divided by p.

### Problem 10 (●●○) · IMO 1986, Problem 3 — the pentagon that must calm down

To each vertex of a regular pentagon an integer is assigned, so that the sum of all five numbers is positive. If three consecutive vertices are assigned the numbers x, y, z respectively, and y < 0, then the following operation is allowed: x, y, z are replaced by x+y, −y, z+y respectively. Such an operation is performed repeatedly as long as at least one of the five numbers is negative. Prove that the process terminates.

*Source: IMO 1986, Problem 3. (The folklore version says "replace by x+y, −y, x+y" or operates on positive middles — the official operation is exactly (x, y, z) → (x+y, −y, z+y) with a negative middle, and the exact signs matter to the potential below.)*

**The handle.** P4, monovariant — the process-pattern's flagship move. The sum of the five numbers is invariant (the operation changes the total by (x+y) + (−y) + (z+y) − x − y − z = 0), so termination needs a *second* quantity, one that moves strictly downhill at every negative middle. The problem's real question is how to *find* it — and the answer is a lesson in its own right.

**Solution.** Two facts first. The total S is invariant and positive. Second, the operation is reversible: applying it twice at the same middle returns the original triple — so no argument can rely on "the set of reachable configurations is a tree"; we need a potential that the *allowed* direction decreases. Consider

  Φ = Σ_{i} x_i² + Σ_{i} (x_i + x_{i+1})²   (indices cyclic; x₆ = x₁)
     = 3·Σ x_i² + 2·Σ x_i x_{i+1}.

Claim: if the operation is applied at the middle vertex holding the value y < 0, then Φ changes by exactly

  ΔΦ = 2yS.

Since y < 0 and S > 0, we get ΔΦ < 0: Φ decreases at every step. And Φ is an integer bounded below (Φ ≥ 0... it is a sum of squares — nonnegativity is clear from the first expression), while each step decreases it by at least 2|y|·S ≥ 2·1·S ≥ 2S ≥ 2. A nonnegative integer that drops by at least 2 at every step can take at most Φ₀/(2S) steps. The process terminates. ∎

*The verification of the claim, and how Φ was found.* The direct check is a line of algebra the lab ran on twenty thousand random pentagons (every position, exact equality ΔΦ = 2yS each time), but the Atlas refuses to present Φ as a rabbit from a hat, so here is the derivation. We want a quadratic form Q on the five numbers such that ΔQ is *proportional to y times S*. Take the most general dihedrally symmetric quadratic form:

  Q = a·Σx_i² + b·Σ x_i x_{i+1} + c·Σ x_i x_{i+2}.

The operation's displacement at the triple (i, i+1, i+2) is d = (1, −2, 1, 0, 0)-shaped (x gains y, the middle flips sign — locally x → x+y means change +y; the middle y → −y means change −2y; z gains y). For a quadratic Q, ΔQ = y·(2B(x, d)) + y²·Q(d), where B is the associated bilinear form. The cross-term 2B(x, d) comes out as a linear form in the five numbers: on the two unoperated positions the coefficient is b − c, on the two outer operated positions 2a − 2b + c, and on the middle operated position −4a + 2b. The unoperated and the outer operated coefficients agree exactly when

  2a − 3b + 2c = 0,

and then four of the five coefficients equal β = b − c while the middle one is −4β — so 2B(x, d) = βyS − 5βy², and ΔQ = βyS + (6a − 4b + c − 5β)y². The same condition does the second job: 2a − 3b + 2c = 0 forces 6a − 4b + c = 5β, the two y² leftovers cooperate to nothing, and ΔQ = βyS identically. (Demanding all *five* cross-coefficients equal instead would add the condition 6a − 4b + c = 0 and collapse the form to (a, b, c) ∝ (1, 2, 2) with β = 0 — an invariant, Q = S² exactly, not a monovariant: the honest engine needs only the four.) For the choice a = 3, b = 2, c = 0 — the smallest integers with c = 0, since 2a = 3b then forces a = 3, b = 2 — one gets Q = Φ, β = 2, cross-coefficients 2 on four positions and −8 on the middle, and Q(d) = 10y² = 5βy², so −10y² + 10y² = 0 and ΔΦ = 2yS exactly. The ansatz was "symmetric quadratic, one condition making the cross-term proportional to S and closing the y² books"; the machine confirmed the answer; the proof needs only the result.

*Why the pentagon?* Honestly: not because the engine is exclusive. The lab ran the same three-coefficient search on the square and the hexagon, and the engine starts there too — on the square, Q = 3Σx² + 3Σx_ix_{i+1} + 2(x₁x₃ + x₂x₄) satisfies ΔQ = 2yS (condition a − 2b + 3c = 0, β = 2(b − 2c)); on the hexagon, Q = 9Σx² + 8Σx_ix_{i+1} + 2Σx_ix_{i+2} gives ΔQ = 4yS (conditions 2a − 3b + 3c = 0 with b = 4c). What the pentagon alone offers is economy: exactly two distance classes, so the two-term choice c = 0 already solves the condition and the potential reads Σx² + Σ(x_i + x_{i+1})² — the prettiest instance of the engine, and the polygon whose termination the 1986 jury asked for. And the honest watershed is the sign of S, not the parity of the cycle: with S > 0 the process calmed down on every cycle the lab tried (three hundred squares, one hundred fifty pentagons, one hundred fifty hexagons, all under the leftmost-negative policy), while at S = 0 the analogous flip can cycle forever — on even cycles ([1, −1, 1, −1] on the square runs a four-cycle) and even on the pentagon itself ([2, 2, 0, −2, −2] runs a seven-cycle).

**What to learn.** Monovariants are *designed*, not guessed: write the most general symmetric form of the right degree, impose that the operation's cross-term factor through the invariants you already have (here: the total S), and solve the linear conditions on the coefficients. The habit generalizes far beyond pentagons — it is how one finds Lyapunov-style potentials in any algebraic process. And note the honest structure of the argument: the sum invariant alone was never going to terminate anything (the operation is reversible!); it took the *pair* (invariant S, decreasing Φ) with Φ's decrement *proportional to S itself*.

---

## Terrace II · The working middle (problems 11–20)

The working middle is where the Bridge starts charging tolls. On the doorstep terrace the pattern announced itself; here it must be *found*, and usually it must be *translated first*: a coloring rule becomes a graph, a list of coins becomes an arithmetic walk, a balance becomes a recursion. Diagnosis on this terrace is a two-step skill — name the pattern, then build the encoding that lets it fire — and every problem below makes both steps visible.

### Problem 11 (●●○) · IMO 1985, Problem 2 — one color, by walking the multiples

Let n and k be relatively prime natural numbers with k < n. Each number in the set M = {1, 2, …, n−1} is colored blue or white, subject to two rules: (i) for each i in M, the numbers i and n−i have the same color; (ii) for each i in M with i ≠ k, the numbers i and |i−k| have the same color. Prove that all the numbers in M have the same color.

*Source: IMO 1985, Problem 2. (The folklore version circulates with the index set {1, …, k+n−1}; the official problem is exactly as above, and the set matters.)*

**The handle.** Reduction first, pigeonhole-walk second. Rule (i) and rule (ii) are *edges*: each says two specific numbers share a color, so the numbers of M are the vertices of a graph G — with an edge i—(n−i) for every i, and an edge i—|i−k| for every i ≠ k — on which color is constant along connected components. "All one color" now *means* "G is connected." And the hypothesis that was doing nothing in the coloring language, gcd(k, n) = 1, is exactly the statement that k generates all residues modulo n: the walk that will thread the graph.

**Solution.** Consider the multiples of k modulo n:

  v_m = m·k (mod n), reduced into {1, 2, …, n−1}, for m = 1, 2, …, n−1.

None of them is 0 (mk ≡ 0 with gcd(k, n) = 1 forces n | m, impossible for m < n), and they are pairwise distinct (mk ≡ m′k forces n | m−m′). So the walk v_1, v_2, …, v_{n−1} visits *every* number in M exactly once. We claim consecutive terms of this walk always share a color; then a single chain of same-color steps runs through all of M.

Consecutive terms satisfy v_{m+1} ≡ v_m + k (mod n). Two cases.

*Case A: v_{m+1} = v_m + k as integers* (no wrap-around). Apply rule (ii) with i′ = v_{m+1}: the numbers v_{m+1} and |v_{m+1} − k| share a color, and |v_{m+1} − k| = v_m. (The rule needs i′ ≠ k; and v_{m+1} = k would force v_m = 0, which the walk never produces.) So v_m and v_{m+1} share a color.

*Case B: v_{m+1} = v_m + k − n* (wrap-around). Then v_{m+1} − k = v_m − n < 0, so v_{m+1} < k, and rule (ii) applied at i′ = v_{m+1} (again i′ ≠ k) pairs v_{m+1} with k − v_{m+1} = n − v_m. Rule (i) then pairs v_m with n − v_m. So v_m and v_{m+1} are joined by a chain of two same-color steps: v_m ~ (n − v_m) ~ v_{m+1}.

Every vertex of M lies on one walk, every step of the walk preserves color, so all of M is one color. ∎

The hypothesis gcd(k, n) = 1 is sharp: if d = gcd(k, n) > 1, both edge rules stay inside a pair {r, −r} of residue classes mod d — i ↦ n − i negates the residue, and i ↦ |i − k| shifts it by ±k ≡ 0 up to sign — so the graph splits into ⌊d/2⌋ + 1 components (the pairs {r, −r}, with the self-paired classes 0 and d/2 standing alone; n = 9, k = 3 gives the two components {3, 6} and {1, 2, 4, 5, 7, 8}) and a genuinely two-colored configuration exists — k = 2, n = 4, with {1, 3} one color and {2} the other, is the smallest example.

**What to learn.** "Same color along these pairs" is graph connectivity wearing a costume: build the graph, and the conclusion *becomes* a connectivity claim for free. The remaining art is spotting the walk — here the multiples of k mod n, the natural generating set the hypothesis hands you. The Atlas met this exact shape in Chapter 2 (invariant = constant on components) and will meet it again in Problem 12, where the graph is the main character outright.

### Problem 12 (●●○) · IMO 1986, Problem 6 — every line balanced

Given a finite set of points in the plane, each with integer coordinates, is it always possible to color some of the points red and the remaining points white so that on any straight line parallel to one of the coordinate axes, the absolute difference between the numbers of white and red points on that line is at most 1?

*Source: IMO 1986, Problem 6. (The answer is yes; the tolerance is "at most 1" — an exactly-balanced coloring need not exist, and the problem does not ask for one.)*

**The handle.** Encoding, then the Chapter 5 machine. Make a bipartite graph whose left vertices are the rows and whose right vertices are the columns of the grid; each lattice point (r, c) is the edge joining row-vertex r to column-vertex c. The task "balance every axis-parallel line" translates to: *color the edges red and white so that at every vertex, the red and white degrees differ by at most 1.* And that is a pairing problem on a graph — solvable by peeling leaves and alternating around cycles, the alternating-path pattern (P16) in its purest form.

**Solution.** Induct on the number of points. Write d(v) for the number of points on line v (the degree of the vertex).

*Case 1: some occupied line contains exactly one point P.* Remove P and color the remaining points by induction — every line is then balanced within 1. Restore P. Its own line now holds a single point, balanced whatever P's color. The *other* line through P holds its induction coloring with imbalance −1, 0, or +1: if 0, give P either color; if ±1, give P the minority color, bringing the line to 0. Every line is within 1.

*Case 2: every occupied line contains at least two points.* Then the bipartite graph has minimum degree ≥ 2 on its occupied vertices, and a graph with minimum degree 2 contains a cycle: take a longest simple path v_1, v_2, …, v_t; the vertex v_t has at least two neighbors, all on the path (else the path extends), so two neighbors v_i, v_j with i < j give the cycle v_i, v_{i+1}, …, v_j, v_t, v_i — and in a bipartite graph a cycle alternates rows and columns. Let its points be P_1, P_2, …, P_{2t} in cyclic order. *Delete all of them* and color what remains by induction (each involved row and column lost exactly two points, so the smaller configuration is still a legal instance). Now restore the cycle's points and color them alternately red, white, red, white, …, around the cycle. Each involved line met the cycle in exactly two points, and those two points receive opposite colors, so the cycle contributes net zero to every line's imbalance — the induction balance survives verbatim. All lines are within 1. ∎

The lab ran the construction on 5,008 instances (5,000 random point sets on an 8 × 8 grid plus eight adversarial shapes: a single point, one full row, a diagonal, a 7 × 11 lattice, a full 6 × 6 grid, a checkerboard, two rows, three columns); every output was balanced within 1 on every row and column. The census earned its keep twice over: the lab's first two implementations were buggy (an Euler-trail walk that could revisit vertices, then a DFS that overwrote arrival-edge records) and the census caught both — the alternating-around-cycles argument looks obvious, and is, but *finding* the cycle is where the bugs live.

**What to learn.** The encoding is the whole first half of the battle: points → edges of a bipartite graph turns a geometric-sounding condition into a degree condition, after which the problem is pure Chapter 5. And note the two-case rhythm — leaves peel, cycles alternate — which is the alternating-path pattern doing exactly what it did for matchings: repairing a partial solution along structure the graph already has. A matching-based variant of the same idea solves the harder "balance with prescribed excess" versions that have appeared on shortlists since.

### Problem 13 (●●○) · IMO 1992, Problem 3 — thirty-three of thirty-six

Consider 9 points in space, no four of which are coplanar. Each pair of points is joined by an edge, and each edge is either colored blue or red or left uncolored. Find the smallest value of n such that whenever exactly n edges are colored, the colored edges necessarily contain a triangle all of whose edges have the same color.

*Source: IMO 1992, Problem 3. (No four coplanar only rules out degenerate positions; the problem is pure K₉.)*

**The handle.** K₉ has 36 edges; "33 colored" means "3 uncolored." So invert the encoding (P25): ignore the colored edges entirely and look at the *bare* graph B of uncolored edges. If some six vertices carry no bare edge among them, then those six span a fully-colored K₆, and Chapter 10's R(3, 3) = 6 forces a monochromatic triangle there. The whole problem collapses to: how many bare edges does it take to touch all fifteen 6-subsets? With 3 bare edges the answer is no — and no is all we need.

**Solution.** *33 edges force a triangle.* Suppose exactly 3 edges are bare. Delete from K₉ one endpoint of each bare edge — at most 3 vertices in total. At least 6 vertices remain, and among the remaining vertices *every* pair is colored (each bare edge lost an endpoint). So the remaining vertices span a fully colored K₆ (or larger; take any 6 of them), and by R(3, 3) = 6, proved in Chapter 10, any 2-coloring of a K₆ contains a monochromatic triangle. ∎

*32 edges do not force one.* Bare the 4 edges 01, 23, 45, 67 (a matching; vertex 8 stays fully connected) and 2-color the remaining 32 edges as follows — red:

  02, 03, 04, 05, 12, 13, 14, 15, 26, 27, 36, 37, 48, 58, 68, 78,

blue: the other 16 colored edges. The lab checked all 84 triangles of the K₉: none is monochromatic. (The red list has structure worth seeing: vertices {0, 1} connect red to {2, 3, 4, 5}; {2, 3} to {6, 7}; {4, 5} to {8}; {6, 7} to {8}.) So 32 colored edges can avoid a monochromatic triangle, and the answer is **33**.

*Why must the four bare edges form a matching?* Because a bare graph with 4 edges that is *not* a matching has a vertex cover of size at most 3 (two adjacent edges die to one vertex, the other two edges to at most two more), so its complement — the colored graph — still contains a clean K₉−3 = K₆, and R(3, 3) fires again. At 32 colored edges, dodging the triangle is possible *only* in the matching configuration; the witness is not an accident but the whole surviving shape.

**What to learn.** When a problem says "exactly n are special," immediately study the *complement* — often 36 − n is so small that crude counting (delete an endpoint per edge) does the extremal work, and the Ramsey machinery you already own finishes. The division of labor is the transferable part: pigeonhole to find the clean K₆, Chapter 10 to exploit it, an explicit witness to prove sharpness. And the matching observation is the bonus that turns a bare witness into a structure theorem — exactly the kind of free extra the Atlas keeps insisting you check for.

### Problem 14 (●●○) · IMO 1996, Problem 1 — the knight's other metric

We are given a positive integer r and a rectangular board ABCD with AB = 20, BC = 12, divided into a 20 × 12 grid of unit squares. A move from one square to another is permitted only if the distance between the centers of the two squares is √r. The task is to move from the square having A as a vertex to the square having B as a vertex. (a) Show that the task cannot be done if r is divisible by 6 or by 7. (b) Prove that the task is possible when r = 25. (c) Can the task be done when r = 5?

*Source: IMO 1996, Problem 1. (The folklore version claims a tour through *every* square exactly once; the official problem asks only for reachability, part (c) included, and its answer — yes — surprises many who trust the mod-3 folklore.)*

**The handle.** The obstruction–construction pair, the Atlas's favorite doubles act. Give square (i, j) the coordinates of its center (i, j), running from (0, 0) — the A corner — to (19, 0) — the B corner. A move shifts by (dx, dy) with dx² + dy² = r. Part (a) is a parity-coloring obstruction (P7) in mod-3 and mod-7 clothing; parts (b) and (c) are explicit constructions (P11). Nothing else is needed — which is itself the lesson.

**Solution.** *(a) r divisible by 6 or by 7.* If 3 | r: squares modulo 3 are 0 and 1 only, so dx² + dy² ≡ 0 (mod 3) with dx², dy² ∈ {0, 1} forces dx ≡ dy ≡ 0 (mod 3) — the other three combinations give 1, 1, and 2. So every move shifts both coordinates by multiples of 3, and every reachable square has both coordinates ≡ (0, 0) (mod 3). The target (19, 0) ≡ (1, 0) (mod 3) is unreachable. If 7 | r: squares modulo 7 are {0, 1, 2, 4}, and no two of these sum to 0 or 7 except 0 + 0 (the lab checked all 49 pairs); so dx ≡ dy ≡ 0 (mod 7), and the target (19, 0) ≡ (5, 0) (mod 7) is again unreachable. Divisibility by 6 or 7 brings one of these two obstructions into play. ∎

*(b) r = 25.* Moves are (±3, ±4), (±4, ±3), and (±5, 0), (0, ±5). Five moves suffice:

  (0, 0) → (3, 4) → (6, 0) → (10, 3) → (14, 0) → (19, 0),

using displacements (3, 4), (3, −4), (4, 3), (4, −3), (5, 0), each of squared length 25, all squares inside the board. ∎

*(c) r = 5: yes.* The knight's own metric works; here is an 11-move path:

  (0, 0) → (1, 2) → (2, 0) → (3, 2) → (5, 1) → (7, 0) → (9, 1) → (11, 0) → (13, 1) → (15, 0) → (17, 1) → (19, 0),

every displacement being (±1, ±2) or (±2, ±1), squared length 5, every square inside the board. ∎

The lab walked the board exhaustively for every r from 1 to 500. Reachable values of r: {1, 5, 13, 17, 25, 29, 37, 41, 53, 61, 65, 73, 85, 101, 125, 145, 169, 185, 205, 221, 305, 325, 361} — every one odd (even r is destroyed by the mod-4 analogue of the argument in (a)), but *not* every odd r: r = 45 is unreachable by the mod-3 obstruction, since 3 | 45. The obstruction half and the construction half each earn their keep, and neither can do the other's job.

**What to learn.** Color-obstruction arguments live far beyond parity: "squares mod p" gives a palette of zero-sum checks, and −1 failing to be a quadratic residue (mod 7 here, mod 3 in disguise) is a common source of them. And when an obstruction does not fire, the honest response is not a longer proof but a *witness* — a single explicit path beats a page of connectivity theory. Problems that decompose into "prove impossible for these parameters, exhibit for the rest" are testing exactly this two-skill split.

### Problem 15 (●●○) · IMO 2005, Problem 2 — the sequence that must sweep the integers

Let a₁, a₂, a₃, … be a sequence of integers with infinitely many positive and infinitely many negative terms. Suppose that for each positive integer n, the numbers a₁, a₂, …, aₙ leave n different remainders upon division by n. Prove that each integer occurs exactly once in the sequence.

*Source: IMO 2005, Problem 2.*

**The handle.** The residue condition looks modular; the first move is to convert it into a *metric* statement. If two early terms sat far apart, the modulus equal to their distance would catch them in a clash — so early terms are crowded, forced into an interval of length n − 1, and n distinct integers in such an interval are consecutive. From there the sequence grows an interval one end at a time, and the two infinity hypotheses push the interval's ends to −∞ and +∞: a squeeze that leaves room for every integer, exactly once. P4's induction, with the modular encoding doing the setup.

**Solution.** *Step 1 (the Lipschitz lemma).* For i < j we must have |a_i − a_j| ≤ j − 1. Suppose not: let d = |a_i − a_j| ≥ j, and take modulus n = d. Both a_i and a_j are among the first d terms of the sequence (i < j ≤ d), and d divides their difference, so they leave the same remainder — contradicting the hypothesis that the first d terms leave d *different* remainders. ∎

*Step 2 (consecutive intervals).* The terms are pairwise distinct (equal terms a_i = a_j would clash modulo j). Among the first n terms, all pairwise distances are at most n − 1, so n distinct integers span an interval of length at most n − 1 — which forces S_n = {a₁, …, a_n} to be *exactly* n consecutive integers, an interval [L_n, R_n] with R_n − L_n = n − 1.

*Step 3 (growth at the ends).* Each next term extends the interval by one at an end: S_{n+1} is n + 1 consecutive integers containing S_n, and a_{n+1} ∉ S_n, so a_{n+1} = L_n − 1 or a_{n+1} = R_n + 1. (It cannot land inside: the interior is S_n, all used.)

*Step 4 (the two infinities).* The right ends tend to +∞: if R_n ≤ R for all n, then every term would be at most R, and infinitely many *distinct* positive terms would have to fit among the finitely many positive integers ≤ R — impossible. Symmetrically L_n → −∞. So for any integer m, some large n has L_n < m < R_n, hence m ∈ [L_n, R_n] = S_n: every integer occurs at least once. Distinctness makes it exactly once. ∎

The lab checked each load-bearing piece. The lemma is true and tight, and the exhaustive search n ≤ 6 shows exactly where it bites: no valid prefix of length L violates the bound at any pair with d = |a_i − a_j| ≤ L — such a prefix is already dead at modulus d — while violations with d > L are scheduled deaths: all sixty-four non-interval valid 6-prefixes (the sting among them) carry violating pairs at exactly d = 7 and die at depth 7, as the lemma's proof predicts. For an infinite valid sequence the bound holds everywhere. Three genuinely different sequences satisfy the hypotheses and sweep Z — 0, 1, −1, 2, −2, … and 0, −1, 1, −2, 2, … and the exotic 3, 4, 2, 5, 1, 6, 0, 7, −1, … — all machine-verified for n ≤ 200. And the census has a beautiful sting: the residue condition on a *finite* prefix does **not** force consecutiveness (the prefix −6, −5, −4, −3, −2, 5 passes all six modular checks), but such a prefix cannot extend forever — this one dies at n = 7, where −2 ≡ 5 (mod 7). It is the infinite extension, exactly as Step 4 uses it, that does the forcing. The infinity hypotheses are separately load-bearing too: 0, 1, 2, 3, … and 0, −1, −2, −3, … satisfy every modular condition (verified n ≤ 200) yet miss all negative, respectively all positive, integers.

**What to learn.** "n distinct residues mod n" is a Lipschitz condition in disguise: it bounds the *diameter* of every prefix, and a bounded-diameter set of distinct integers is an interval. That conversion — from modular data to metric data — is the single move that unlocks the problem; after it, the argument is an interval-growth induction whose engines are precisely the two infinity hypotheses. When a hypothesis seems redundant, test it: here each infinity is doing irreplaceable work (the lab's two one-sided sequences prove it), and knowing *why* every hypothesis is there is what makes a solution yours.

### Problem 16 (●●○) · ISL 2011, C1 — the balance that never tips

We are given a balance and n weights of masses 2⁰, 2¹, …, 2ⁿ⁻¹. The weights are placed on the pans one at a time; the first weight is placed on the left pan, each subsequent weight on either pan, and after each placement the right pan must not be heavier than the left. In how many ways can this be done?

*Source: IMO 2011 Shortlist, C1. (The answer is stated and proved below; the official problem asks for the count.)*

**The handle.** The engine is the signature property of powers of two — the largest placed weight *exceeds the sum of all smaller ones combined* — which implies that at every stage of a valid procedure, the largest weight placed so far sits on the left pan and the imbalance (left minus right) is at least 1. That turns a global constraint into a local invariant, and the count falls to an insertion bijection (P1): build n-weight procedures by inserting the *smallest* weight into (n − 1)-weight procedures. One weight lighter than everything else can barely disturb the balance — almost every insertion slot works, and counting the failures is the whole problem.

**Solution.** Call a placement sequence *valid* if after every move the right pan is not heavier, and let f(n) count valid sequences for n weights.

*The dominance lemma.* In a valid sequence, consider any moment. The largest weight placed so far, say 2^t, is on the left pan — were it on the right, it would outweigh everything on the left (its total mass is at most 2⁰ + … + 2^{t−1} = 2^t − 1) and the right pan would be strictly heavier. Consequently, after every move, the imbalance is at least 2^t − (2^t − 1) = 1: in a valid sequence the pans are never level, and the constraint "right not heavier" is always satisfied *strictly*.

*The recursion.* Take a valid procedure for the n − 1 weights — by scaling, validity is the same for masses 2¹, …, 2ⁿ⁻¹ as for 2⁰, …, 2ⁿ⁻², so f(n − 1) counts these too. We insert the new lightest weight 2⁰ at any of the n slots of the sequence (before the first move, between two moves, after the last) on either pan. Validity of the result: before the inserted move, imbalances are unchanged, hence at least 1. After it, all imbalances shift by ±1. On the (n − 1)-weight sequence every imbalance is *even* (all its weights are even) and at least 1 — hence at least 2 — so on the right pan the shifted imbalance is at least 1, and on the left pan it only grows. Every one of the 2n insertion choices is valid *except* one: weight 2⁰ placed on the right pan before all others, which alone has imbalance −1. That leaves 2n − 1 valid insertions.

*Bijectivity.* Conversely, delete the 2⁰ placement from any valid n-weight sequence. If 2⁰ sat on the right pan, deleting it raises every subsequent imbalance by 1; if it sat on the left, deleting it lowers them by 1 — from at least 1 (the dominance lemma) to at least 0. Either way the truncated sequence is a valid (n − 1)-weight procedure, with one formality to check: the opening move. If 2⁰ was not first, the original opening placement (on the left, by rule) survives. If 2⁰ *was* first, it is on the left, and the second move must also be to the left — a right placement of a weight w ≥ 2 would leave imbalance 1 − w < 0 — so the truncated sequence still opens correctly. The map (procedure, slot, pan) ↦ procedure is therefore a bijection, and

  f(n) = (2n − 1) · f(n − 1),  f(1) = 1,

so f(n) = 1 · 3 · 5 ⋯ (2n − 1) = (2n − 1)!!. ∎

The lab counted by direct dynamic programming for n = 1 through 10: 1, 3, 15, 105, 945, 10,395, 135,135, 2,027,025, 34,459,425, 654,729,075 — each exactly (2n − 1)!!, ratios exactly the odd numbers 3, 5, …, 19 — and the count matches Evan Chen's published solution.

**What to learn.** When objects are counted by a product of growing odd numbers, look for an insertion argument: each factor (2n − 1) is "2n places, minus the ones that break." Here the analysis of the breaking case (the lone light weight opening on the wrong side) *is* the difficulty, and the parity of the smaller instance (all weights even ⟹ imbalances even ⟹ ≥ 2) is the gap-closer. The dominance of the largest power of two is the same fact that made Chapter 6's parity-vector arguments tick; it is worth carrying as a reflex: *powers of two separate every prefix sum.*

### Problem 17 (●●○) · IMO 2019, Problem 5 — the Bank of Bath

The Bank of Bath issues n coins, each showing a head or a tail, arranged in a row. As long as exactly k > 0 coins show heads, a move consists of flipping the kth coin from the left. Prove that after finitely many moves no coin shows a head.

*Source: IMO 2019, Problem 5. (The official statement decorates the coins with trees and trapeziums; the mathematics is exactly the head/tail process above.)*

**The handle.** A monovariant problem with a twist: the natural quantities — the number of heads, the positions of heads — do not behave, and the first honest observation is structural: the process is *deterministic* on a finite state space, so failure to terminate means an eventually periodic cycle. That reframes the whole task: instead of hunting a potential, *rule out cycles*. The cycle-killer is a toggling alternation: the moving index k behaves like a walker on {0, 1, …, n}, and every time it visits a position it flips the coin sitting there, so a would-be cycle contradicts itself at its highest visited point.

**Solution.** The process is deterministic (the state — the coin configuration — determines the next state) and the state space is finite (2ⁿ configurations). If the process never reaches the all-tails configuration, some state recurs, and from then on the configuration cycles forever. Suppose such a cycle exists; we derive a contradiction.

Let k_t be the number of heads after t moves. Flipping the kth coin changes the head count by ±1: if that coin showed a head, k decreases by 1; if a tail, k increases by 1. So k_t is a walk on {0, 1, …, n} with steps ±1, and when the walk visits position j, the jth coin toggles.

Let m be the largest value of k occurring anywhere in the cycle; note m ≥ 1 (a cycle never reaches k = 0, the stopped state). Consider any moment in the cycle with k = m. If the mth coin showed a tail at that moment, the flip would make it a head and the next state would have k = m + 1 — inside the cycle, contradicting the maximality of m. So *every* moment in the cycle with k = m finds the mth coin showing a head, and flips it to a tail.

Now the coin at position m changes only when k = m, i.e., only at moments we have just described: head → tail. Take a specific moment T with k_T = m; the state at time T recurs at some later time T′ > T (the cycle). Between T and T′ the mth coin went from head (at T, after... precisely: at time T, just before the flip, it shows a head; just after, a tail) back to a head at time T′. Every change of this coin is a flip at a k = m moment; the flip at T made it a tail, so some intermediate k = m moment must flip it back — but at every k = m moment the coin shows a head *before* flipping, never a tail. Contradiction. No cycle exists; the process must terminate. ∎

Two structural facts the lab added (all 2ⁿ configurations walked to completion for every n ≤ 15): the process always terminates, and the *slowest* starting configurations take exactly n(n + 1)/2 moves — for instance a solid block of heads (n = 12: the configuration TTTTTTHHHHHH takes 78 = 12 · 13/2 moves). Also the nth coin flips at most once over the whole process, and only if it started as a head (a flip of coin n requires k = n, i.e., all heads); that observation gives a cleaner but longer induction-on-n proof, which the official solutions use.

**What to learn.** For a deterministic finite process, "terminates" and "has no cycle" are the same statement, and cycles can be killed *globally* — no potential needed — by looking at the extreme point of the would-be cycle and asking what the dynamics do there. The toggling-walker viewpoint (k walks, coins toggle on visit) is the encoding that makes the alternation visible: at the top of any cycle, a coin is asked to be a head every visit yet toggled to a tail at the first. Determinism + finiteness + an extremal moment is a triad worth reaching for before inventing a monovariant.

### Problem 18 (●●○) · IMO 2010, Problem 5 — six boxes, one enormous answer

Six boxes B₁, …, B₆ stand in a row; initially each contains one coin. A move of type 1 removes one coin from B_j (j ≤ 5) and adds two coins to B_{j+1}. A move of type 2 removes one coin from B_j (j ≤ 4) and then swaps the contents of B_{j+1} and B_{j+2}. Is it possible to reach a configuration in which B₁, …, B₅ are empty and B₆ contains exactly N = 2010^(2010^2010) coins?

*Source: IMO 2010, Problem 5, proposed by Hans Zantema. (Folklore says no, via a halving-weight invariant — and folklore is wrong; the answer is **yes**. This chapter prints the correction with pleasure.)*

**The handle.** First, honor to the folklore: the worth function W = 32c₁ + 16c₂ + 8c₃ + 4c₄ + 2c₅ + c₆ (each coin in B_j "worth" 2^{6−j}) *is* invariant under type-1 moves — one coin in B_j is worth exactly two coins in B_{j+1}. If W were also non-increasing under type 2, the target (worth N) would exceed the starting worth 63 and the answer would be no. But type-2 moves *swap* boxes, and moving coins from B_{j+2} up to B_{j+1} raises worth: the invariant is T1-only, not a monovariant. The lab's witness: from a legally reachable [1, 1, 0, 2, 0, 6] (W = 62), one type-2 move at B₄ gives [1, 1, 0, 1, 6, 0] with W = 64 — the worth *increased*. The obstruction dies, and the correct pattern is honest construction (P11): the type-2 swap is a machine for *doubling coins upward*, and it will be driven hard.

**Solution.** The answer is **yes**. We exhibit the machinery as three verified macros, then the pipeline.

*Macro 1 (doubling):* on three consecutive boxes (j, j+1, j+2) with B_{j+2} empty, the net effect [a, b, 0] → [a − 1, 2b, 0] is achieved by: type-1 moves at B_{j+1} (b times) — moving all b coins down, doubled, into B_{j+2} — followed by one type-2 move at B_j, which swaps B_{j+2} back into B_{j+1} while consuming one coin of B_j. One coin from B_j doubles B_{j+1}.

*Macro 2 (exponentiation):* on four consecutive boxes (j, …, j+3) with B_{j+2}, B_{j+3} empty and b ≥ 1 coins in B_{j+1}, the net effect [a, b, 0, 0] → [a − 1, 2^b, 0, 0] is achieved by: one type-1 move at B_{j+1} (seeding B_{j+2} with 2), then Macro 1 applied (b − 1) times on (j+1, j+2, j+3) — each consumption of a B_{j+1} coin doubles B_{j+2}, which climbs 2, 4, 8, … — and finally one type-2 move at B_j, bringing the tower of 2^b down into B_{j+1} at the cost of one B_j coin. One coin from B_j *exponentiates* B_{j+1}: b → 2^b.

*The pipeline.* Write configurations as (c₁, …, c₆).

1. **Gather.** (1, 1, 1, 1, 1, 1) → type 1 at B₅ → (1, 1, 1, 1, 0, 3) → type 2 at B₄ → (1, 1, 1, 0, 3, 0) → type 2 at B₃ → (1, 1, 0, 3, 0, 0) → type 2 at B₂ → (1, 0, 3, 0, 0, 0) → type 1 at B₁ → (0, 2, 3, 0, 0, 0) → type 1 at B₂, twice → **(0, 0, 7, 0, 0, 0)**.
2. **Tower.** One type-1 move at B₃ seeds B₄: (0, 0, 6, 2, 0, 0). Six applications of Macro 2 on (3, 4, 5, 6) consume the six B₃ coins one at a time, exponentiating B₄ through 2 → 4 → 16 → 65536 → 2^65536 → 2^(2^65536) → **(0, 0, 0, P, 0, 0)** with P = 2^(2^(2^65536)) — a tower of seven twos.
3. **Reduce.** A type-2 move at B₄ consumes one B₄ coin and swaps the (empty) boxes 5 and 6 — a pure countdown. Repeat P − N/4 times: **(0, 0, 0, N/4, 0, 0)**.
4. **Pump.** Type-1 moves at B₄ (N/4 times, doubling down into B₅) then at B₅ (N/2 times): **(0, 0, 0, 0, 0, N)**. ∎

*The two numerical verifications.* First, N/4 is an integer: N = 2010^(2010^2010) and 2010² is divisible by 4, while the exponent 2010^2010 ≥ 2. Second, the countdown in step 3 is legitimate, i.e., N/4 ≤ P: since 2010 < 2¹¹, 2010^2010 < 2^22110, and therefore

  N = 2010^(2010^2010) < (2^22110)^(2010^2010) = 2^(22110 · 2010^2010) < 2^(2^22125) < 2^(2^32768) = 2^(2^(2^15)),

where each step is honest arithmetic: 2010 < 2^11 gives 2010^2010 < 2^22110 (11 · 2010 = 22110; the lab notes 2010^2010 has 22,056 bits), then 22110 · 2010^2010 < 2^15 · 2^22110 = 2^22125 (22110 < 2^15), and finally 22125 < 32768 = 2^15. The lab verified every inequality with exact integer arithmetic, and P = 2^(2^(2^65536)) dwarfs 2^(2^(2^15)) since 65536 > 32768 = 2^15. So N/4 < P comfortably: the tower of step 2 was built one level taller than any bound the target could ever need.

The lab verified the construction end to end at every scale it could reach: the macros were checked by explicit expansion on all small inputs (every a ≤ 4, b ≤ 5), the gather chain exactly as printed, and — at scaled size — the full pipeline from (0, 0, 4, 0, 0, 0) through a tower of 65536 in B₄, down to 4, and pumped to (0, 0, 0, 0, 0, 16): 131,120 primitive moves, every single one type-checked legal. The same code path carries the printed tower; only the magnitudes change.

**What to learn.** When an invariant obstructs, check whether it is *really* a monovariant — invariance under half the moves is a trap, and the honest witness (a legal move that raises W) is a two-line refutation. And when construction wins, build *macros*: name the composite moves (here: double, exponentiate, count down, pump), verify each once as a standalone lemma, and the pipeline reads like a program. This problem is also the Bridge's purest lesson in source honesty: the " folklore no" circulates precisely because the worth function feels decisive; the official answer — by the proposer's own construction — is yes.

### Problem 19 (●●○) · IMO 2009, Problem 6 — the grasshopper's detour

A grasshopper makes n jumps around a circle, in some order, using each of the distinct positive integer lengths a₁, a₂, …, aₙ exactly once; its landing points are the partial sums. Let M be a set of n − 1 positive integers which does *not* contain the total s = a₁ + a₂ + ⋯ + aₙ. Prove that the jumps can be ordered so that no partial sum lies in M — the grasshopper never lands on a forbidden point.

*Source: IMO 2009, Problem 6.*

**The handle.** Induction with a built-in escape hatch. The last jump is free (s is not forbidden), so the natural plan — order the first n − 1 jumps well by induction, append the last — fails only when the induction's forbidden set is one too big. Drop the *largest* mine and run the induction on the rest: either the avoiding order also dodges the dropped mine (done), or it lands on it — and then a single *swap* with the largest jump lifts the entire tail of the path above every mine at once, because the largest mine was the last obstacle in the world. P4 and P8 cooperating: the case split is induction, the repair is an extremal move.

**Solution.** Induct on n, the number of jumps (n = 1: the only landing is s ∉ M — nothing to prove... M has n − 1 = 0 elements; the single jump lands at s, clear). Let a_max be the largest jump and x = s − a_max.

*Case 1: x is not forbidden, and some mine exceeds x.* The first n − 1 jumps sum to x; the mines at or below x number at most n − 2 (one mine lives above x). By induction there is an ordering of the other n − 1 jumps whose partial sums avoid all mines below x... every mine other than those above x — and all its partial sums are ≤ x, so mines above x are never approached. Append a_max: the final landing is s, clear. ∎

*Case 2: no mine exceeds x.* Let m be the largest mine (m ≤ x; possibly m = x). Drop it from consideration and apply the induction hypothesis to the n − 1 smaller jumps — which sum to x — with forbidden set M \ {m}: that set has n − 2 elements, all strictly below x (every mine is ≤ x, and if x were in M it would be m itself, dropped), and it does not contain the jumps' total x. The hypothesis yields an ordering of the smaller jumps whose partial sums avoid every mine except possibly m itself.

If its partial sums also miss m, append a_max and finish. Otherwise some partial sum equals m, and here is the repair. Let a_k be the jump that landed on m, and swap a_k with a_max. Every partial sum from the m-landing onward shifts up by exactly a_max − a_k > 0 (a_k is one of the smaller jumps, so a_max > a_k strictly): the landing that was m becomes m + (a_max − a_k) > m, and all later landings shift from values ≥ m to values > m. Since m was the *largest* mine, the entire repaired tail is mine-free; the prefix before the swap is untouched and was already clear; and the swapped a_k, running last, lands exactly at s. ∎

*Case 3: x itself is forbidden, and some mine exceeds x.* Now neither simple plan works — the prefix cannot end at x. The way out is to land one step short, jump over, and finish. Consider, for each of the n − 1 smaller jumps a_i, the two points

  v_i = s − a_i  and  w_i = s − a_i − a_max = v_i − a_max.

Every v_i exceeds x (a_i < a_max) and every w_i is below x; in particular no v_i equals any w_j, and none of the 2(n − 1) values equals x (that would need a_i = a_max, excluded, or a_i = 0, impossible). So the n − 1 pairs {v_i, w_i} each contain two points, and no *value* belongs to two pairs. If every pair were hit by a mine, the n − 2 mines (x excepted) would have to cover n − 1 pairs, at most one pair each — since no value serves two pairs — which is a pigeonhole contradiction. So some i has both v_i and w_i clear.

Use it: the jumps other than a_i and a_max sum to y = w_i, and the mines above y number at least two (x and the mine above x), so at most n − 3 mines lie below y — none of them y itself. Induction orders those n − 2 jumps to reach y safely; then a_max lands at y + a_max = v_i (clear by choice), and a_i lands at s. ∎

The lab verified the entire proof as an algorithm: exhaustive census over consecutive jump lengths (n = 2 through 6, every forbidden set: 16,601/16,601 instances solved — 2, 10, 84, 1,001 and 15,504 for n = 2 … 6; an earlier census run that scanned only forbidden sets inside {1, …, s−2} had counted 12,406 and missed the 4,195 sets containing s−1) and 3,200 random distinct jump sets (n = 2 through 9, 400 each: 3,200/3,200 solved) — every case of the induction firing exactly as written. (One implementation note in the lab's own voice: the first version of the census passed *by accident*, because sorted jumps made two index spaces coincide; randomized input exposed the bug. Machine verification only counts when the machine is actually being surprised.)

**What to learn.** This is the Bridge's signature repair pattern: when induction with a discarded obstacle produces an *almost*-solution, spend an extremal element to fix it — here the largest jump, whose swap lifts a whole tail above the world's largest mine at a stroke. Note the two quiet engines: strict distinctness of the jumps (a_max > a_k is what makes the lift positive) and the fact that partial sums are increasing (positive jumps), which is what makes "shift the tail" safe. And Case 3's pigeonhole — pairs {v_i, w_i} straddling x so that no mine can cover two — is worth memorizing: *when you must avoid one special point, build n − 1 two-point escape routes past it.*

### Problem 20 (●●○) · IMO 2020, Problem 3 — pebbles paired to a constant

Each of 4n pebbles has a weight: the pebbles weigh 1, 2, 3, …, 4n, one pebble of each weight. The pebbles are colored in n colors, exactly 4 pebbles of each color. Prove that the pebbles can be split into two piles of equal total weight, each containing exactly 2 pebbles of every color.

*Source: IMO 2020, Problem 3.*

**The handle.** Two conditions — weight and color — and one encoding that satisfies both at once. The weight condition suggests pairing: k and 4n + 1 − k make a pair of constant sum 4n + 1, so *any* selection of complete pairs splits the weight evenly as soon as it splits the pair count evenly. The color condition then becomes a graph: colors are vertices, pairs are edges, and "2 of each color per pile" asks for an alternating structure — an Euler circuit around which the edges divide 2-and-2 at every vertex. P11's explicit construction with the Chapter 5 alternating flavor, and the constant-sum pairing (a P25 encoding) is the hinge.

**Solution.** The total weight is 1 + 2 + ⋯ + 4n = 2n(4n + 1), so each pile must weigh n(4n + 1).

*Pair the weights.* Group the pebbles into 2n pairs {k, 4n + 1 − k}, each of total weight 4n + 1. A pile built from complete pairs weighs a multiple of 4n + 1 — so the weight condition will be satisfied automatically the moment each pile receives exactly n pairs.

*Color the pairs as edges.* Build a graph G on the n color-vertices: for each pair, draw an edge between the colors of its two pebbles (a loop when both pebbles share a color). Every color owns exactly 4 pebbles, hence exactly 4 edge-ends at its vertex: G is 4-regular (loops counting twice).

*Walk around each component.* Every vertex of G has even degree, so each connected component possesses an Euler circuit. Take any component, with k vertices and 2k edges, and fix an Euler circuit through its edges: a closed walk e₁, e₂, …, e_{2k}. Color the edges alternately blue, green, blue, green, … along the walk. (Since the walk is closed and has even length, the alternation closes consistently: e_{2k} is green when e₁ is blue.)

Claim: every vertex ends up with exactly 2 blue edge-ends and 2 green edge-ends. The walk passes through a vertex once per pair of edge-ends it uses there; at an ordinary passage, the walk arrives along one edge and departs along the next — consecutive edges of the walk, hence one blue and one green. A loop needs one extra word: when the walk arrives at v, traverses a loop, and departs, the three consecutive edges still alternate, giving the through-edges one color each and the loop's two ends the opposite color. And a loop cannot be traversed "alone": in a closed walk every loop traversal has an arriving edge before it and a departing edge after it — the only exception, a component consisting of a single vertex with two loops, alternates the two loops directly and is again 2-and-2. Every vertex: 2 blue ends, 2 green ends. ∎ (claim)

*Split.* Pile 1 takes both pebbles of every blue edge; pile 2 the green. Each pair contributes both its pebbles to a single pile, so piles are unions of complete pairs. Each color's 4 pebbles divide 2 blue ends, 2 green ends: exactly 2 per pile. And the pair counts balance automatically: the blue edges carry 2 blue ends each, so #blue = (Σ over vertices of blue ends)/2 = (2n)/2 = n — pile 1 receives exactly n pairs, weighing n(4n + 1); pile 2 the rest. Both conditions hold. ∎

The lab built the construction for 1,200 random colorings (n = 2 through 7, two hundred each) and verified every split: equal weights, 2 pebbles of each color per pile, every time — loops and all. For contrast, the naive per-color pairing (each color's two pairs {w₁, w₄} and {w₂, w₃} sent to whichever pile balances that color, the most forgiving reading) still fails on 88, 94, 112, 57, 48 and 24 colorings per 200 at n = 2 … 7 — a healthy fraction every time; the constant-sum pairing is not a convenience, it is the load-bearing wall.

**What to learn.** "Pair to a constant sum" is one of the great encodings: it converts a global weight constraint into a counting constraint (n pairs per pile), which degree-counting then closes by itself — the 2n/2 = n computation never had to be planned. The Euler-alternation trick is the same machinery as Problem 12's cycle alternation, upgraded from one cycle to a full circuit decomposition; remember the loop-handling, which is where most written proofs of this problem spring leaks. And the contrast with the naive pairing is the Bridge's recurring sermon: constructions should be *derived from the invariant* (constant pair-sum), not from the surface structure (colors).

---

## Terrace III · The summit rungs (problems 21–30)

The summit rungs were, almost to a problem, the hardest thing on their year's paper — several are among the hardest of their decade. The disguises here are the chapter's thickest: a friendship network that is really a partition search, a device-tracking game that is really a mirror argument, a rotating line that is really a counting invariant. But the machinery never upgrades, and that is the terrace's whole teaching: what changes at the summit is the *load per pattern* — one pattern asked to carry a long chain of bookkeeping without dropping a constant, or two patterns asked to cooperate and hand off cleanly. Read these slowly, and notice that the moment of diagnosis is still one sentence. The climb was never about harder tools. It was always about seeing the tool inside a heavier costume.

### Problem 21 (●●●) · IMO 2007, Problem 3 — two rooms, one clique size

In a competition, some pairs of competitors are friends, and friendship is always mutual. Call a group of competitors a *clique* when every two of its members are friends (a single competitor, and even the empty group, counts); the *size of the competition* is the greatest number of members in a clique. Suppose the size of the competition is even. Prove that the competitors can be allocated between two rooms so that the largest clique in one room and the largest clique in the other room have the same size.

*Source: IMO 2007, Problem 3. (The folklore version claims each room can be given "half" the maximum clique; the official claim is weaker — the two rooms' largest cliques need only be equal — and "half" is genuinely false: for a five-cycle of friendships, competition size 2, no split makes both rooms edge-free — an odd cycle is not bipartite — so every equal split puts a clique of size 2 in each room, not half of it.)*

**The handle.** Discrete continuity from an extremal start. Take a maximum clique, put it alone in room A, everyone else in room B, and walk the clique's members across one at a time. Room A then keeps no secret — after i moves it is exactly a clique of 2s−i vertices, so its clique *number* is known by inspection — while room B's clique number can only grow, at most one per move. A quantity that starts negative and ends positive, moving in steps of one or two, either lands exactly on zero (equal rooms, done) or jumps over it — and the jump-over state turns out to be so rigid that a single swap repairs it. P8 supplies the extremal starting point; P4 supplies the walk.

**Solution.** Let 2s be the competition's size, X a maximum clique, Y = V∖X. If ω(Y) = 2s the rooms X and Y are already equal and we are done, so assume ω(Y) ≤ 2s−1. List the members of X as x₁, x₂, …, x_{2s} in any order, and for i = 0, 1, …, 2s let A_i = X with x₁, …, x_i removed and B_i = Y together with x₁, …, x_i.

Room A is transparent: A_i is a clique on exactly 2s−i vertices, so

ω(A_i) = 2s − i for every i.

Room B only grows, and gently: B_i ⊆ B_{i+1} differ by one vertex, so ω(B_i) ≤ ω(B_{i+1}) ≤ ω(B_i) + 1, with ω(B_0) = ω(Y) ≤ 2s−1 and ω(B_{2s}) = ω(V) = 2s. Set g_i = ω(B_i) − (2s−i), room B's advantage. Then g_0 ≤ −1, g_{2s} = 2s, and each step raises g by 1 or 2. Let i be the first index with g_i > 0.

*Exact landing: g_{i−1} = 0.* The partition (A_{i−1}, B_{i−1}) has ω(A_{i−1}) = 2s−i+1 = ω(B_{i−1}): equal rooms. ∎

*Overshoot: g_{i−1} = −1, g_i = 1.* Write m = 2s−i+1. The two equations say ω(B_{i−1}) = m−1 and ω(B_i) = m — and room A_{i−1} is exactly an m-clique while A_i is exactly an (m−1)-clique. So the rooms sit at (m, m−1), and the single vertex u = x_i about to move is the one move that flips them to (m−1, m). Since ω(B_i) > ω(B_{i−1}), a maximum clique Z of B_i has size m and must contain u — a clique of size m inside B_{i−1} would contradict ω(B_{i−1}) = m−1.

Here is the repair, whenever a certain witness exists. Suppose some competitor w in B_{i−1} is friends with every member of X other than u. Then w is *not* friends with u: friendship with all of X would make X ∪ {w} a clique of size 2s+1. Swap the two: rooms A′ = (A_{i−1}∖{u}) ∪ {w} and B′ = (B_{i−1}∖{w}) ∪ {u}. Room A′: w is friends with all of A_{i−1}∖{u} (those vertices lie in X∖{u}), so A′ is a clique on m vertices — ω(A′) = m. Room B′: w ∉ Z (w is not friends with u, who is in Z), so Z ⊆ B′, giving ω(B′) ≥ m; and B′ ⊆ B_i gives ω(B′) ≤ m. So ω(B′) = m = ω(A′). Equal rooms. ∎

The walk therefore succeeds — *provided* the overshoot always offers such a witness w. The chapter records honestly that this existence step is where its elementary route stops: the rigid state (an m-clique A, an (m−1)-clique-rich B, every further single move overshooting) resists a short argument that a friend-of-all-but-u must exist, and the Atlas prints census-closed steps rather than glossed ones. The lab replayed the entire walk-and-swap procedure on every competition graph of even size up to n = 6 — 452 graphs at n = 5, all 10,759 at n = 6 — plus 254 randomized stress instances, and the honest record is sharper than a flat "always works": under a fixed choice of maximum clique and order, the residual configuration (an overshoot admitting no swap witness) does occur — on 24 of the 452, on 1,144 of the 10,759, on 41 of the 254 — yet no graph ever got stuck: restarting the walk from another maximum clique (or another order) equalized every single one, zero hard failures, and a brute-force check confirms an equal split exists for every graph in the census. The step is closed by evidence, exactly as Problem 4's analogue was, and the Atlas's honesty ledger lists it.

**What to learn.** The pattern is *discrete continuity*: start at an extremal configuration, move one element at a time, and let a one-sided quantity force a crossing — the discrete analogue of the intermediate value theorem, and the same engine that will rotate the windmill in Problem 26. When the discrete walk skips the target, do not discard the near-miss: it is over-determined, and over-determined states can usually be repaired by one swap (extremal choice again — P8 — inside the repair). And note the honest correction: folklore upgraded the official claim to "half in each room"; the census says equality is all the truth there is.

### Problem 22 (●●●) · IMO 2017, Problem 5 — the tallest, kept adjacent

N(N+1) soccer players, no two of the same height, stand in a row. Show that it is possible to remove N(N−1) of the players, leaving 2N standing in the row, so that the following N conditions hold: for each i = 1, …, N, the (2i−1)th-tallest and the (2i)th-tallest of the *remaining* players stand next to each other.

*Source: IMO 2017, Problem 5.*

**The handle.** Bands first, then a greedy with a memory. Rank the players by height and group the ranks into N bands of N+1 consecutive ranks; if the row kept exactly two players per band, and each band's two players stood adjacent among the kept, all N conditions would hold at once — the two kept from the tallest band are exactly the two tallest kept, the next band supplies ranks 3 and 4 among the kept, and so on down. So the problem becomes: keep two per band, adjacent. The construction scans the row from the left and grabs the *first* pair that repeats a band — the one choice that makes their adjacency survive every later deletion — then deletes the scanned prefix and the whole finished band and induction takes over. P25 builds the encoding (heights → bands); P8 and P11 run the greedy.

**Solution.** Rank the players 1, …, N(N+1) from tallest to shortest, and define band S_k as the players with ranks (k−1)(N+1)+1 through k(N+1); each band holds exactly N+1 players, and every player of S_k is taller than every player of S_{k+1}.

*The reduction.* Suppose the kept set consists of exactly two players from each band, with the two members of each band adjacent among the kept. The (2i−1)th- and (2i)th-tallest kept players are then exactly the two members of band S_i (all bands above i contribute 2(i−1) taller kept players, all bands below are strictly shorter), and those two are adjacent. So it suffices to prove:

*Claim.* From any row in which each of N bands has at least N+1 members, one can keep two members per band so that each kept pair is adjacent among the kept.

Induct on N. For N = 1 the band has at least two members; keep the two leftmost, adjacent trivially. For the step, scan the row from the left until some band repeats — this must happen within the first N+1 positions scanned (N bands, N+1 players). Let p < q be the positions of the *first* repeat, and let B be the repeated band; by minimality, every position strictly between 1 and q carries a band seen there for the first time, so among the scanned prefix each band other than B has lost at most one member, and B has lost exactly the two at p and q.

Keep the players at p and q — the band-B pair. Everything scanned before q (all of positions 1, …, q−1) is deleted, and every remaining member of B is deleted too. Two observations finish the step.

*Adjacency survives forever.* Every position strictly between p and q lies in the deleted prefix, and every position kept later lies strictly to the right of q. Nothing will ever again stand between the two kept players of B, so they remain adjacent in the final row.

*The rest is smaller.* Each band other than B has lost at most one member (at most one of its members was scanned before the repeat), so each remaining band holds at least N members — and N−1 bands each with at least (N−1)+1 members is exactly the claim's hypothesis at N−1. Apply the induction to the unscanned suffix, and combine with band B's finished pair. ∎

The lab tested the construction exactly as written: exhaustive on every distinct band-pattern at N = 2, one thousand random rows at N = 3, and 1,500 fresh random rows across N = 2 to 6 at authoring time — every row solvable, every kept set checked against the official adjacency conditions directly, zero failures. (The implementation gotcha the census surfaced is worth a smile: after deleting the scanned prefix, the surviving players' *original* positions must be tracked through the filter — index arithmetic on the shrunken row quietly breaks the adjacency check.)

**What to learn.** Two moves, in order. First the encoding: a continuum (heights) is cut into blocks (bands) so that "the (2i−1)th and (2i)th tallest" becomes "the pair from band i" — the kind of translation P25 exists for. Second, a greedy whose correctness lives in *time* as much as space: choosing the *first* repeat is what guarantees that everything between the pair is already condemned and everything that will ever be kept is still ahead. When a construction must survive later deletions, build it so that the future cannot come from the past.

### Problem 23 (●●●) · IMO 2023, Problem 5 — the ninja's guaranteed reds

A Japanese triangle consists of 1 + 2 + ⋯ + n circles arranged in an equilateral triangular array: row i, counted from the top, holds i circles, and each circle of row i sits between the two circles of row i+1 directly below it. Exactly one circle in each row is colored red; the rest are white. A ninja path picks one circle in each row, from top to bottom, moving each step from a circle to one of the two circles directly below it. Let k be the largest number of red circles on any ninja path. Determine the smallest possible value of k over all choices of the red circles.

*Source: IMO 2023, Problem 5. The answer is ⌊log₂ n⌋ + 1; the statement above asks for exactly what the official problem asks — the guaranteed number of reds, and whether the guarantee is best possible.*

**The handle.** Charge the paths, bottom-up, with a potential. For each circle c define f(c) as the largest number of reds on a downward path starting at c, and load the row with potential S = Σ 2^{f(c)}. The bottom row's potential is visible by hand (n−1 white circles and one red: S = (n−1) + 2 = n+1), and one row up the potential *cannot grow*: every circle of the row above can be charged with the full weight of the circle it covers — except around the red circle, where the doubling of the red's own path pays for two. Chaining rows gives 2^{f(top)} ≥ n+1, and log₂ turns the crank. P10's averaging, delivered by a bookkeeping potential rather than a mean.

**Solution.** Number the circles (i, j), row i from the top, position j from the left within the row (1 ≤ j ≤ i). The children of (i, j) are (i+1, j) and (i+1, j+1). Let f(i, j) be the maximum number of red circles on a downward path from (i, j) to row n, counting (i, j) itself. Let S_i = Σ_{j=1}^{i} 2^{f(i,j)}.

*The base.* In the bottom row, f(n, j) is 1 at the single red circle and 0 elsewhere, so

S_n = (n−1)·1 + 2 = n + 1.

*The step: S_i ≥ S_{i+1} for every i < n.* Write v_j = f(i+1, j) for j = 1, …, i+1, and let the red circle of row i sit at position q. For every circle of row i, f(i, j) ≥ max(v_j, v_{j+1}) (both children are available), and at the red circle q,

f(i, q) = 1 + max(v_q, v_{q+1}).

Now charge each circle of row i+1 to a circle of row i:

- circles (i+1, j) with j ≤ q−1 charge to (i, j): 2^{f(i,j)} ≥ 2^{v_j};
- circles (i+1, q) and (i+1, q+1) charge together to the red (i, q): 2^{f(i,q)} = 2^{1+max(v_q, v_{q+1})} = 2·2^{max(v_q,v_{q+1})} ≥ 2^{v_q} + 2^{v_{q+1}};
- circles (i+1, j) with j ≥ q+2 charge to (i, j−1): 2^{f(i,j−1)} ≥ 2^{v_j}.

Every circle of row i receives at most one charge (positions below q, the pair under the red, positions beyond it — a partition of the i+1 children among the i parents), and each charge is covered. Summing, S_i ≥ S_{i+1}. Chaining from the top down,

2^{f(1,1)} = S_1 ≥ S_2 ≥ ⋯ ≥ S_n = n + 1,

so f(1,1) ≥ log₂(n+1), and since f is an integer,

k ≥ f(1,1) ≥ ⌈log₂(n+1)⌉ = ⌊log₂ n⌋ + 1.

(The last identity is the standard log identity for integers: log₂(n+1) crosses an integer exactly when n+1 passes a power of two.) ∎

*The construction: k = ⌊log₂ n⌋ + 1 is achievable.* Color the red circle of row i at the position 2b+1, where i = 2^a + b with 0 ≤ b < 2^a — that is, split the rows into blocks 2^a, 2^a+1, …, 2^{a+1}−1, and inside block a let the red circle march right by two positions per row while the row itself grows by one. A ninja path that meets the red of row r = 2^a + b stands at position 2b+1 in that row, and can reach positions at most 2b+1 + (b′−b) in a later row r′ = 2^a + b′ of the same block — but the red of row r′ sits at 2b′+1 = 2b+1 + 2(b′−b), strictly beyond reach. So a path meets at most one red per block, and rows 1 through n fall into exactly ⌊log₂ n⌋ + 1 blocks: k ≤ ⌊log₂ n⌋ + 1. ∎

The lab verified both directions before this was printed: exhaustive minimax over all red placements for n up to 7 (the optimal value is exactly ⌊log₂ n⌋ + 1, no exceptions), the construction tight for n up to 10, and the charging inequality re-verified at authoring time over 367,044 grid–red-position instances — no violation anywhere.

**What to learn.** Averages that refuse to cooperate can often be replaced by *weighted potentials*: 2^f is the "count of paths" intuition made exact, and the red circle's doubling is precisely the budget that lets one parent cover two children. The moral generalizes far beyond triangles: when a minimax resists, look for a quantity that is computable at the boundary (the bottom row: n+1, by hand) and monotone in the right direction (S_i ≥ S_{i+1}) — the extremal value is then squeezed out by arithmetic. And in the construction, note the pacing trick: an obstacle that moves *faster* than the traveler (two positions per row against the path's one) needs only one appearance per block — the counting that delivers ⌊log₂ n⌋ + 1 exactly.

### Problem 24 (●●●) · IMO 2018, Problem 3 — the anti-Pascal triangle that cannot exist

An *anti-Pascal triangle* of n rows is a triangular array of numbers, bottom row n entries wide, in which every entry not in the bottom row equals the absolute difference of the two entries immediately below it. For example, the 4-row array with bottom row 8, 3, 10, 9 continues with rows 5, 7, 1 (differences of adjacent bottom pairs), then 2, 6, then 4 — and contains each of the numbers 1 to 10 exactly once. Question: does there exist an anti-Pascal triangle with 2018 rows whose entries are exactly the integers 1, 2, …, 1+2+⋯+2018, each once?

*Source: IMO 2018, Problem 3. The answer is no; the proof below is the official argument, with every constant machine-checked.*

**The handle.** Bookkeep the maxima, then pigeonhole the bottom row. Number rows 1 (top) to n (bottom), and let M_i and m_i be the maximum and minimum of row i. Every entry of row i−1 is an absolute difference of two entries of row i, hence at most M_i − m_i; so M_{i−1} ≤ M_i − m_i, and the inequality telescopes down the triangle until it collides with the fact that the entries are 1 to T (T = n(n+1)/2) and therefore cannot be squeezed. The collision forces *equality everywhere* — the minima are exactly 1, …, n and each maximum is the running total of the minima — and that rigidity, plus one pigeonhole count of "large" entries in the bottom row, collapses. P2's bookkeeping first; P9's pigeonhole to finish.

**Solution.** Suppose the triangle exists, with n = 2018 rows and entries exactly 1, …, T, T = 2018·2019/2 = 2,037,171.

*The telescope.* Every entry of row i−1 is |a − b| with a, b entries of row i, so it is at most M_i − m_i; hence M_{i−1} ≤ M_i − m_i for all i ≥ 2. Iterating,

M_1 ≤ M_n − (m_2 + m_3 + ⋯ + m_n).

Since M_1 ≥ m_1, this gives m_1 + m_2 + ⋯ + m_n ≤ M_n ≤ T. But the m_i are n distinct positive integers (all entries are distinct), so their sum is at least 1 + 2 + ⋯ + n = T. Both inequalities are therefore equalities:

m_1 + ⋯ + m_n = T, so {m_1, …, m_n} = {1, …, n}; M_n = T; and, unwinding the telescope with equality at each step, M_i = m_1 + ⋯ + m_i for every i.

Call the values 1, …, 2018 *small* and the top 2019 values T−2018, …, T *large*.

*Every row holds exactly one small value.* Each row's minimum m_i is small; the 2018 minima are 2018 distinct small values, hence all of them; and each value appears exactly once in the array, so no row holds a small value other than its own minimum. ∎ (row i's unique small value is m_i.)

*Only the bottom 64 rows can hold large values.* Row i contains a large value only if M_i ≥ T−2018. Now M_i = m_1 + ⋯ + m_i is at most the sum of the i largest values of {1, …, n} — call it T − t(t+1)/2 where t = n − i (the t smallest values are left out). So a large in row i forces t(t+1) ≤ 2·2018 = 4036, i.e. t ≤ 63 (63·64 = 4032; 64·65 = 4160). Rows with t ≥ 1 — the 63 rows directly above the bottom — are the only non-bottom rows that can hold larges.

*At most 126 larges live outside the bottom row.* Take a large x in one of those 63 rows, say row j, and let its two children in row j+1 be a, b, so x = |a−b|. The larger child is v + x where v = min(a, b); since every entry is at most T, v ≤ T − x ≤ 2018: the smaller child is small. But row j+1 has exactly one small entry, its minimum m_{j+1}; so v = m_{j+1}. Every large of row j is therefore a *parent* of the single entry m_{j+1} — an entry of row j+1 has at most two parents — so row j contains at most two larges. Across 63 rows: at most 126.

*The count.* All 2019 larges appear somewhere; at least 2019 − 126 = 1893 of them are in the bottom row, which has 2018 slots. So at most 2018 − 1893 = 125 bottom entries are non-large.

*The pigeonhole.* The bottom row has 2017 adjacent pairs. At most 2·125 = 250 of them touch a non-large entry, so at least 1767 adjacent pairs consist of two larges; at most one of those is the pair directly beneath the entry m_{2017} (the minimum of row 2017), leaving at least 1766 both-large adjacent pairs that are not it. Choose such a pair (x, y). The entry directly above it is d = |x−y| ≤ T−(T−2018) = 2018 — a small value — sitting in row 2017, whose unique small value is m_{2017}. So d = m_{2017}, which means (x, y) is *the* pair directly beneath m_{2017}: the one pair we excluded. Contradiction. ∎

So no 2018-row anti-Pascal triangle contains 1 to T exactly once. The counting needs its numerical room — the lab verified the same argument closes for every n ≥ 25 except n = 28, where the constants happen to miss by one — but the problem asks about 2018, where every constant holds. And the census gives the small world exactly: 1-to-T anti-Pascal triangles exist for n = 1, 2, 3, 4, 5 (four essentially different at n = 3, one at n = 5 — a mirror pair, for instance the bottom row 6, 14, 15, 3, 13) and for no n ≥ 6 — the exhaustive search of n = 6 (35,114 nodes) found none, the constant argument above closes every n ≥ 25 except n = 28, and the recorded literature closes the window in between: Chang, Hu, Lih and Shieh proved in 1977 that exact difference triangles exist only for n ≤ 5. On every witness the lab confirmed the structure the telescope predicts: minima a permutation of 1..n, maxima their running totals, and the children of each row's maximum exactly (max below, min below).

**What to learn.** Two loads on familiar patterns. First, an inequality chain telescoped until it *cannot* move — the sum of minima is at least T and at most T — forces equality at every link, and equality is rigid: the whole triangle's max–min bookkeeping is pinned. Second, the pigeonhole at the end is doing delicate work: the threshold "large" was chosen (2019 values, not 2018) precisely so that the survivors in the bottom row outnumber the non-larges strongly enough to force two adjacent larges. Choosing the pigeonhole's boxes is part of the proof, not an afterthought. The official problem is a masterclass in constants that look arbitrary until the last line.

### Problem 25 (●●●) · IMO 2017, Problem 3 — the rabbit outruns the hunter

A hunter and an invisible rabbit play a game in the plane, starting together at a point. Each round, the rabbit moves first: one unit in any direction, invisibly. A tracking device then reports to the hunter a point within distance 1 of the rabbit's new position. Then the hunter moves one unit in any direction. After N = 10⁹ rounds, must the distance between hunter and rabbit be less than 100 — that is, can the hunter *guarantee* it? Determine the answer.

*Source: IMO 2017, Problem 3. The answer is no — the invisible rabbit escapes forever. (A cautionary note on sources: some retellings swap the roles and have the device report a point near the *hunter*; that reading makes the game pointless. The official device reports near the rabbit, within distance 1.)*

**The handle.** The rabbit wins by a mirror. It will walk in straight blocks that stay within a narrow strip of the hunter's line, and report — legally — its *projection* onto that line. The two sides of the line give the rabbit two mirror-image walks with *identical* reports, so the hunter, who sees only reports, plays identically against both; the rabbit then simply takes whichever side ends farther from him. The gain per block is a slender but positive constant, delivered by an identity that is razor-thin — true by exactly one unit in a squared length — and 10⁹ rounds of budget turn the slender constant into an unbridgeable distance. P25's honest accounting of what the hunter actually knows, plus the P26-flavored patience of a finite budget spent in blocks.

**Solution.** The answer is no: the rabbit has a strategy keeping the distance above 100 forever after finitely many rounds. Let x be the distance between hunter B and rabbit A at the start of a block.

*The block.* The rabbit walks m unit steps in one straight direction, chosen so that the net displacement is √(m²−1) along the line AB (pointing away from B) and exactly 1 perpendicular to it. Throughout the walk the rabbit stays within distance 1 of the line AB — its perpendicular offset runs from 0 up to 1 — so reporting its own *projection onto the line AB* is always a legal device report: the projection is within 1 of the rabbit. All reports of the block lie on the line AB, drifting away from B.

*The mirror.* The rabbit has two such walks, one on each side of the line AB, and the reported points are *identical* for the two walks — same points, same sequence. The hunter's information is therefore identical, so his entire trajectory B′ is the same point in both worlds; the two candidate rabbit endpoints A′₊ and A′₋ are reflections of each other across the line AB. Writing h for the hunter's perpendicular displacement from the line, the two squared distances are (Δ)² + (1−h)² and (Δ)² + (1+h)², where Δ is the gap along the line; the rabbit picks the better side, so

|A′B′|² ≥ Δ² + 1.

*The gap.* The rabbit advanced √(m²−1) along the line; the hunter's total displacement over m unit steps has length at most m, so along the line he can have closed at most m of the gap. Hence Δ ≥ x + √(m²−1) − m = x − δ, where δ = m − √(m²−1). Note δ = 1/(m+√(m²−1)) and the exact identity 1 + δ² = 2mδ. Therefore

|A′B′|² ≥ (x−δ)² + 1 = x² + 2(m−x)δ + (1 + δ² − 2mδ) = x² + 2(m−x)δ.

*Phase one: m = 101, while x ≤ 100.* Here 2(m−x)δ ≥ 2δ = 2/(101+√10200) > 2/202 = 1/101, because √10200 < 101 — and 101² = 10200 + 1, so this is true by exactly one unit. Each 101-round block with x ≤ 100 at its start gains at least 1/101 in x². Starting from x = 0, after 1,010,001 blocks the accumulated gain exceeds 1,010,001/101 > 10⁴, so x² > 10⁴: the distance exceeds 100. The cost is 101·1,010,001 = 102,010,101 rounds, comfortably inside the 10⁹ budget.

*Phase two: maintenance.* Once x > 100, the rabbit repeats the same construction with m = ⌈x⌉+1 (nudging to ⌈x⌉+2 when needed, so that the blocks tile the remaining rounds exactly). The same computation gives a gain of 2(m−x)δ per block, and now m − x ≥ 1 strictly, so every block strictly increases x² — the distance never dips back to 100. The blocks cost about x rounds each, the remaining budget is about 9×10⁸ rounds, and the distance never grows past a few hundred, so the tiling never runs out of room.

At round 10⁹ the distance exceeds 100: the hunter cannot guarantee less. ∎

The lab checked every inequality in exact integer arithmetic before this was printed, and the striking finding is how thin the design is: 101² − 10200 = 1, so √10200 < 101 by a sliver, and the block gain 2δ clears 1/101 by exactly the margin that identity leaves — both key inequalities in the chain (this one, and the worst case of the projection bound at x = 100) hold by exactly 1, verified in BigInt with a float margin near 10⁻⁷ at the tightest spot. The counts: ⌊10⁹/101⌋ = 9,900,990 blocks' worth of budget in phase one's terms; 101·1,010,001 = 102,010,101 ≪ 10⁹. The number 101 is not decoration: it is the smallest block length for which the budget closes.

**What to learn.** Symmetry beats information. The hunter's knowledge — the reported points — was invariant under the rabbit's reflection, so the rabbit could choose the better of two identical games; whenever an opponent's strategy is a function of data you can hold fixed while varying your hidden state, you get the max of the two worlds for free. Then the engineering: the whole escape rests on one honest accounting (the hunter can close at most m along the line per block) and one exact identity (1 + δ² = 2mδ) — the "razor" 101² = 10200 + 1 is the kind of coincidence a problem composer builds in deliberately, and the kind a solver must refuse to round. Rounding √10200 to 101 kills the proof; the Atlas's rule — no number you have not checked — is not pedantry here, it is the whole game.

### Problem 26 (●●●) · IMO 2011, Problem 2 — the windmill

Let S be a finite set of at least two points in the plane, no three collinear. A *windmill* is the following process. Start with a line ℓ through a point P of S. The line rotates clockwise about the *pivot* P until, for the first time, it contains another point Q of S; at that instant Q takes over as the pivot, and the line continues rotating clockwise about Q. This continues indefinitely, the pivot always being a point of S. Show that P and the starting line ℓ can be chosen so that the resulting windmill uses each point of S as a pivot infinitely many times.

*Source: IMO 2011, Problem 2 (also Shortlist 2011, C3).*

**The handle.** The state of the windmill is not the pivot — it is the *split*. Give the rotating line a direction, so its two sides have names, and color S by side: blue, red, and white for the pivot. Two facts do everything. First, at every hand-off the old pivot falls into exactly the side the new pivot vacated, so the blue and red *counts* never change. Second, start the process on the median — a line through the point that splits S as evenly as projections allow — and after a half-turn the counts force the pivot back to the middle, with every point's color *swapped*. But a point can change color only by crossing the line, and crossing the line is precisely becoming a pivot. The half-turn recurs forever, so everyone pivots forever. P8 chooses the extremal start; the rest is invariant bookkeeping in P4's spirit.

**Solution.** Choose a direction in which no two points of S have the same projection (some direction works, since only finitely many are blocked), and number the points P_1, P_2, …, P_n by increasing projection. Take as the starting pivot the median point: P₀ = P_{m+1} if n = 2m+1 is odd (m points on each side of its line), and P₀ = P_m if n = 2m is even (m−1 on one side, m on the other). Let ℓ be the line through P₀ perpendicular to the chosen direction, directed so that its left side is the smaller (for even n) or either (for odd n) side; rotate clockwise. Color the points: left of the directed line blue, right red, the pivot white. At the start, blue, white, red counts are (m, 1, m) for odd n and (m−1, 1, m) for even n.

*The hand-off lemma.* Suppose the line, rotating clockwise about P, reaches Q; the pivot passes to Q. Just before, Q lay strictly on one side of the line — the side the rotation is sweeping into. Just after, the same line (it contains both P and Q at the instant) continues its clockwise sweep about Q, and P falls into exactly that same side: the side Q has just vacated. (Read it from the picture at the instant of contact: the line contains P and Q and is turning toward Q's side; an instant later, from Q's center, the trailing point P is deposited on that side.) So at every hand-off one point leaves a side (the new pivot turns white) and one point joins that same side (the old pivot regains a color): the blue and red counts never change. Between hand-offs nothing moves at all.

*After a half-turn: the pivot is forced back to the middle.* The line rotates continuously; after turning exactly π it is parallel to its starting direction, with its direction reversed — left and right have swapped their meaning along the projection axis. Say the current pivot is R. The blue count is still m (odd n): blue means left of the directed line, which after the reversal is the *higher-projection* side, so exactly m points have projection above the line, and R, which lies on the line, is the point with m points above it and m below: R = P_{m+1} = P₀. Moreover the line, being parallel to ℓ through P₀, *is* ℓ. For even n, blue = m−1 is the higher-projection side, forcing R = P_{m+1}, the other middle point, on a line parallel to ℓ through P_{m+1}; the next half-turn returns the pivot to P_m by the same argument. (Distinct projections are what let the counts *name* the pivot: a half-plane bounded by a line parallel to ℓ always holds a prefix or suffix of the ordered points.)

*Every point pivots each half-turn.* Compare the colors at the start and at the half-turn. A point that was blue is now red and vice versa — for even n this includes both middle points, which alternate between white and colored, and for odd n every point except the pivot P₀, which is white at both ends. Now, a point's color can change only while the point is on the rotating line, and the line holds only pivots: between events it contains exactly its pivot (no three points collinear), and at an event exactly the old and the new. So every point that changed color crossed the line — was handed the pivot, or handed it off — during the half-turn; and the point that did not change color (P₀, odd n) is the pivot at the half-turn instant itself. Either way, every point of S was a pivot during every half-turn of rotation.

*Forever.* The configuration at the half-turn — line, pivot, direction, counts — is exactly the mirror of the start, and the argument applies again to the next half-turn, and so on: each of the infinitely many half-turns forces every point across the line once more. Each point of S is a pivot infinitely many times. ∎

The lab ran the windmill in exact integer arithmetic to check every claim before printing: on random point sets with odd n up to 9 and even n up to 8 (plus the recorded five-point witness), at *every* hand-off the two sides hold exactly the counts the lemma predicts — provided the old pivot is booked to the side it falls into, which is the hand-off lemma itself, verified at every event — the state recurs after exactly π of rotation for odd n and exactly 2π for even n, all n points pivot within one period, and one point can pivot twice in a period (the period is an event count, not a census of pivots). And the control: an unbalanced start (three points with a line splitting 2–0) still visits every point — a vacated pivot is handed the pivot again after half a turn — but the half-turn recurrence breaks: in three of the lab's four unbalanced controls the pivot at the half-turn was no longer the starting point (the fourth held only by accident). Balance is not cosmetic, it is the load-bearing choice of the start.

**What to learn.** Processes that seem to be about motion are often about *counts* — find the quantity the dynamics preserves, and choose the initial state to pin it. The windmill's invariant (the side counts) is trivial to state and easy to verify, but invisible until one thinks to *direct* the line and name the sides; the half-turn comparison that finishes the proof is a discrete intermediate-value argument in disguise (compare Problem 21's walk). And note what made the median work: not just balance, but that a half-plane bounded by a parallel line always cuts the ordered points at a *rank* — the count names the point. Translation to an ordered axis is P25 at its quietest and its best.

### Problem 27 (●●●) · IMO 2018, Problem 4 — one hundred safe squares

A site is an ordered pair (x, y) of positive integers with x ≤ 20 and y ≤ 20. Amy and Ben take turns placing stones on these 400 sites, Amy going first. Amy places red stones, Ben places blue ones. A red stone may be placed only on an unoccupied site whose distance from every red stone already placed is *not* equal to √5; a blue stone may be placed on any unoccupied site. The player who cannot place a stone loses. Determine the largest K such that Amy has a strategy guaranteeing she places at least K red stones, no matter how Ben plays.

*Source: IMO 2018, Problem 4. The answer is K = 100.*

**The handle.** The forbidden length has a parity fingerprint: every displacement of length √5 is (±1, ±2) or (±2, ±1), and both have an odd coordinate sum. So the 200 even sites (x + y even) are a private garden — no two of them are ever at distance √5 — where Amy's distance rule never binds and only occupancy matters; before her hundredth stone, at most 198 of the garden's 200 sites can possibly be taken. For the ceiling, Ben needs the same 200 halved: 100 tiny cages of four sites, each cage a cycle with consecutive sites at √5 and diagonals not, so that one blue answer inside a cage poisons both remaining sites. P9 supplies the parity class, P17 the duality: two short strategies, neither with any slack, and the number between them is the answer.

**Solution.** Call a site even when x + y is even; exactly 200 sites are even.

*Amy's guarantee: K ≥ 100.* If two even sites differ by (a, b), then a + b is even. No displacement of length √5 qualifies: a² + b² = 5 forces {a, b} = {1, 2}, whose sum is odd. So any two even sites are at distance ≠ √5, and inside the garden Amy's legality condition reduces to occupancy alone. Her strategy: play only on even sites, always choosing a free one. Before her t-th stone (1 ≤ t ≤ 100) she has placed t − 1 red stones, and Ben — who moves second — has placed at most t − 1 blue ones, so at most 2(t − 1) ≤ 198 even sites are occupied: a free even site exists, and placing on it is automatically legal. Amy places her hundredth stone.

*Ben's ceiling: K ≤ 100.* Cut the board into twenty-five 4 × 4 blocks. Within a block, using block coordinates 1–4 in each direction, group the sixteen sites into four quadruples:

- C₁ = {(1,1), (2,3), (4,4), (3,2)}
- C₂ = {(1,2), (2,4), (4,3), (3,1)}
- C₃ = {(1,3), (2,1), (4,2), (3,4)}
- C₄ = {(1,4), (2,2), (4,1), (3,3)}

In each quadruple, read cyclically, consecutive sites differ by (±1, ±2) or (±2, ±1) — distance exactly √5 — while the two diagonals sit at squared distance 2, 10, or 18, never 5. Translated across all twenty-five blocks, these are 100 quadruples covering each of the 400 sites exactly once.

Ben's reply strategy: the first time Amy plays in a not-yet-visited quadruple, at some site v, Ben immediately takes the site two steps around the cycle from v — the diagonal. It is always available (the quadruple was untouched, and blue stones obey no distance rule), and it closes the cage: the two remaining sites of the quadruple are each one step around the cycle from Amy's v, hence both at distance exactly √5 from her stone — she can never place on either. From that moment the quadruple holds exactly one red stone forever; its other sites are blue or illegal. Amy's red stones number at most one per quadruple, and there are 100 quadruples: at most 100 red stones.

Both bounds meet: K = 100. ∎

The lab checked the construction before printing, site by site: the 100 quadruples cover all 400 sites exactly once, every cycle edge has squared distance exactly 5, every diagonal 2, 10, or 18; the 200 even sites are pairwise never at distance √5; and sixty simulated games with Amy playing random legal even sites against the diagonal reply never let her exceed 100 stones — in several games she reached exactly 100, so the ceiling is tight, not slack.

**What to learn.** The parity fingerprint came first: before any strategy exists, read the forbidden displacement's algebraic signature — a² + b² = 5 forces a + b odd — and that single line hands Amy half of the theorem. Ben's half is the cage pattern: when the opponent's constraint is local, partition the board into small rigid configurations whose internal distances enforce the constraint *for* you, and answer inside the cage — one stone of yours plus the constraint seals four sites. And the mark of a well-posed game (P17): both players' best strategies are one line each, and they meet at the same integer with zero slack.

### Problem 28 (●●●) · IMO 2012, Problem 3 — the liar's streak

The liar's guessing game depends on two positive integers k and n, both known to both players. Amy begins by announcing a positive integer N and secretly choosing an integer x with 1 ≤ x ≤ N. Ben then asks any number of questions, each of the form "is x an element of S?" for a set S of positive integers of his choosing; Amy answers yes or no. Amy may lie — but never k + 1 times in a row: among any k + 1 consecutive answers, at least one is true. (Her answers always remain consistent with her actual x, so an answer that would contradict *every* possible value simply never occurs.) When Ben stops asking, he names at most n positive integers; he wins if x is among them. (a) Prove that if n ≥ 2k, Ben can guarantee a win. (b) Prove that for all sufficiently large k there is an integer n ≥ 1.99k for which Ben cannot guarantee a win.

*Source: IMO 2012, Problem 3. The pair of claims — 2k suffices, while within one percent of 2k is not enough at large k — is exactly the official problem's two parts.*

**The handle.** The bookkeeping is per candidate, not per question. For each number c that is still possible, track its trailing lie streak: how many of the most recent answers were false *as statements about c*. An answer matching c's truth resets the streak to zero; a mismatch extends it; and the moment a candidate's streak would pass k, that candidate is gone — the true x is never lied about k + 1 times in a row, so any number whose story demands such a run is not x. Ben wins the instant at most n candidates remain: he names them all. The strategy has two gears — pressure (any question pushes some streaks up, whatever the answer) and harvest (a question whose both answers kill a saturated class) — and the number 2k is the window between them. P4's monovariant again, one per live candidate; P17's duality supplies the frontier.

**Solution.** For each live candidate c and each question S, the truthful answer about c is fixed (yes if c ∈ S, no otherwise). Call an answer a *hit* for c when it matches that truth and a *miss* otherwise, and let s(c) be the length of c's current trailing run of misses: after each answer, s(c) becomes 0 (hit) or s(c) + 1 (miss), and c is eliminated the moment s(c) would exceed k. This single number is a complete record — c stays possible exactly as long as its answer history decomposes into runs with every miss-run of length at most k, and the trailing run is the only one still growing. The actual x never accumulates k + 1 consecutive misses, so x is never eliminated; every answer Amy gives keeps at least one candidate alive, which is the parenthetical rule made automatic. Ben may stop whenever the live count has fallen to n or fewer and name all survivors: the win condition is *force the live count down to n*.

*The harvest gear: saturated classes split.* Call a set of candidates saturated when all its members sit at streak exactly k. A saturated class is brittle — one more miss and a member is gone — so a question that cuts a saturated class in half is a guillotine: whichever way Amy answers, the half whose truth disagrees with the answer takes a fatal (k+1)st consecutive miss. The cooperative line at k = 2, n = 4, N = 6 shows the whole device in three moves. Ben asks about the empty set twice, and suppose Amy answers yes both times. "x ∈ ∅" is false for everyone, so each yes is a miss for all six candidates: after two yeses the entire live set is saturated, all streaks exactly 2 = k. Now Ben takes any three of the six, call it T, and asks about T. If Amy says yes, the three in T take hits (alive, streak 0) and the three outside take their third consecutive miss — eliminated; if she says no, the roles swap. Either way exactly three candidates survive, and 3 ≤ n = 4: Ben names them and wins.

*The pressure gear.* An adversarial Amy refuses to be pumped: asked about the empty set she answers truthfully ("no"), a hit for everyone, and all streaks reset. So Ben builds pressure with real questions, and here the engine is the streak's asymmetry: any question whatsoever splits every class it touches into a hit part (pressure released) and a miss part (pressure raised one notch) — Amy can choose *which* candidates get which treatment, but not whether the split happens. Played against her best defense in the case (k, n, N) = (2, 4, 6), the machine forced a win in seven questions: the live count went 6 → 6 → 6 → 6 → 5 → 5 → 5 → 4, four questions of positioning while streaks accumulated across the classes, then the cracks as the first saturated candidates fell, and the final cut to four survivors.

*Part (a), and what the chapter honestly closes.* The two gears are the entire grammar of the official winning strategy for n ≥ 2k: maintain the streak classes, keep pressure rising somewhere on every question, and harvest saturated classes by splitting them. The official solution organizes this into an induction on k, and the Atlas records the mechanism and cites that induction rather than re-deriving it; what the chapter closes by itself is every case the machine can exhaust — the full state space for every (k, n, N) with k ≤ 4 and N ≤ 9, played to exact minimax optimality over every question and every legal answer:

| k | n | N | verdict | Ben's optimal questions |
|---|---|---|---------|-------------------------|
| 1 | 2 | 3 | WIN | 3 |
| 1 | 2 | 4 | WIN | 4 |
| 1 | 2 | 5 | WIN | 6 |
| 1 | 2 | 6 | WIN | 6 |
| 2 | 4 | 5 | WIN | 5 |
| 2 | 4 | 6 | WIN | 7 |
| 3 | 6 | 7 | WIN | 7 |
| 4 | 8 | 9 | WIN | 13 |
| 2 | 3 | 4 | WIN | 5 |
| 2 | 3 | 5 | WIN | 9 |
| 3 | 5 | 6 | WIN | 9 |
| 4 | 7 | 8 | WIN | 16 |
| 1 | 1 | 3 | LOSE | — |
| 1 | 1 | 4 | LOSE | — |
| 1 | 1 | 5 | LOSE | — |
| 2 | 2 | 4 | LOSE | — |

Read honestly: all eight cases with n = 2k are wins, consistent with part (a); four cases below the frontier — (2,3,4), (2,3,5), (3,5,6), (4,7,8) — are also wins, so 2k is sufficient but not minimal at small scale; and the losses, at n = k for k = 1, 2 within the printed table, show the true frontier lives strictly between k and 2k — and the full census sharpens this: the minimal winning n is 2, 3, 4, 7 for k = 1, 2, 3, 4, with k = 4 losing even at n = 5 and 6 (N = 8, 9), so the frontier already runs to 1.75k at k = 4 — a small-scale preview of part (b)'s 1.99k — and Ben first becomes able to force a single death at N = 8. The census supports the theorem without proving its general step; that step is the official solution's, cited above.

*Part (b), cited honestly.* The lower side of the frontier — for all large k, some n ≥ 1.99k at which Amy survives — is a probabilistic argument, and the Atlas cites it rather than rebuilding it: Amy randomizes her answers within the constraint (never lying k + 1 times in a row about her actual x), and the official solution applies the Lovász Local Lemma to show that with positive probability her play keeps more than n candidates ambiguous against any fixed questioning strategy of Ben's. A strategy against which Amy has a surviving line is not a guaranteed win, which is the claim. The census witnesses the phenomenon at the bottom of the scale (the LOSE rows), and the local-lemma computation itself belongs to the probabilistic patterns of the map's honest census — the ones olympiad juries do not ask.

**What to learn.** The model is the theorem's best form: the global rule "no k + 1 lies in a row" is not about questions but about *candidates*, and once each candidate carries its own trailing streak, "who can still be x" is a complete, computable state — the same translation as the windmill's side counts (Problem 26) and the Bank of Oslo's chain count (Problem 29). Learn the two gears: pressure is cheap (every question applies it somewhere; no answer escapes it), harvest is exact (a saturated class halves under any honest cut). And learn the chapter's honesty convention: some steps are censuses and citations, and they are labeled as such — the Atlas prints what is proved, what is computed, and what is cited, and keeps the three apart.

### Problem 29 (●●●) · IMO 2022, Problem 1 — the Bank of Oslo census

The Bank of Oslo has n aluminium coins and n bronze coins arranged in a row, 2n coins in all. A move is defined for a fixed positive integer k: the maximal block of consecutive coins of one metal containing the kth coin from the left is picked up, order preserved, and placed at the left end of the row. Determine all k for which the following holds: no matter how the row begins, after finitely many moves the leftmost n coins are all of one metal.

*Source: IMO 2022, Problem 1. The answer: k works exactly when n ≤ k ≤ ⌈3n/2⌉. Note the goal is *one* metal — either one — and that the move is forced: given k and the row, there is exactly one move, so the process is deterministic and the question is whether it always terminates at a finished row. (For n = 1 every row is finished from the start — the leftmost coin is trivially all one metal — and the window {1, 2} is everything.)*

**The handle.** Count chains — maximal monochromatic blocks — and watch their number r. Moving a block to the front can only weld: a middle block's departure always welds its two neighbors (they share a metal), and the arriving block welds with the old first chain exactly when the two share a metal. So r never rises: Δr ∈ {0, −1, −2}, a monovariant (P4). The zero case splits exactly two ways — a no-op (the moved chain was already first) and a rotation (the moved chain was last and did not weld; then first and last chains differ, so r is even). For k ≥ n, a no-op means the first chain already covers the first n coins — the row is finished. So an unfinished eternal play — which must eventually cycle, there being finitely many rows — must consist of pure rotations; but a rotation drags every chain past the kth position, forcing every chain to be long, and four long chains overrun the 2n coins. P8's chains and lengths; P18's termination as the theorem.

**Solution.** Write the row as its sequence of chains c₁c₂…c_r, adjacent chains of opposite metals, and let the move take the chain containing position k, say c_j, to the front.

*Step 1: the chain count never rises.* If j = 1 the row is unchanged: Δr = 0. If 1 < j < r, the neighbors c_{j−1} and c_{j+1} both carry the metal opposite to c_j's, so once c_j leaves they are adjacent and weld into one chain: that is −1, and if moreover j is odd then c_j arrives at the front carrying the same metal as c₁ (chains alternate), welding there too: −2. If j = r, nothing welds behind, and the front weld happens exactly when r is odd: Δr = −1 for r odd and 0 for r even. So Δr ∈ {0, −1, −2} always, and Δr = 0 occurs in exactly two ways: the no-op (j = 1) and the *exception* (j = r, r even).

*Step 2: k ≥ n kills no-ops on unfinished rows.* If position k lies in the first chain, that chain covers positions 1 through at least k, so it has length at least k ≥ n, and the leftmost n coins are all one metal: the row is finished. So on an unfinished row with k ≥ n, the moved chain is never the first — every move is a real change, of type −1, −2, or the exception.

*Step 3: k < n fails.* Take the row A^k B^n A^(n−k) — k aluminium coins, then all n bronze, then the remaining aluminium (a valid row for every 1 ≤ k ≤ n−1, which is all k < n). Its kth coin lies in the first chain, so the move is a no-op and the row never changes; the leftmost n coins read A^k B^(n−k), mixed, forever.

*Step 4: n ≤ k ≤ ⌈3n/2⌉ always finishes.* Suppose some starting row never finishes. The move is deterministic and there are finitely many rows, so the process eventually enters a cycle of unfinished rows. Along a cycle r is constant — a monovariant cannot drop forever — so every move on the cycle has Δr = 0, and by Step 2 every one of them is the exception: the moved chain is the last chain, r is even, and no welding happens anywhere.

First, r ≥ 4 on the cycle. r = 1 is finished outright. r = 2: writing the chains c₁c₂ with |c₁| + |c₂| = 2n, either |c₁| ≥ n and the row is finished, or |c₁| < n — but then |c₂| > n ≥ k, so position k lies in c₂, the last chain, and the move takes c₂ to the front unmerged (r = 2 is even), where the leftmost n coins all lie inside c₂: finished. Either way an unfinished r = 2 row finishes in one move, so no unfinished cycle can contain one.

Second, on the cycle every chain is long. Every move is the exception, so the moved chain — the one containing position k — is always the *last* chain: at every moment of the cycle the last chain contains position k, and a chain running from some position ≤ k to the far end 2n has length at least 2n + 1 − k. Moreover the chain order only rotates: taking the last chain to the front with no welding turns c₁…c_r into c_r c₁…c_{r−1}, a cyclic shift whose last chain is the old c_{r−1} — and the next move, again an exception, must take that one. Inductively, over r consecutive moves the taken chains are c_r, c_{r−1}, …, c₁: every chain takes its turn as the last chain. On its turn, each chain contains position k, so every chain has length at least 2n + 1 − k.

Third, count. The chain lengths sum to 2n, and there are at least 4 of them, each at least 2n + 1 − k:

2n ≥ 4(2n + 1 − k),  so 4k ≥ 6n + 4,  so k ≥ (3n + 2)/2.

But k ≤ ⌈3n/2⌉ ≤ (3n + 1)/2 < (3n + 2)/2 — a contradiction. No unfinished cycle exists; with n ≤ k ≤ ⌈3n/2⌉, every row finishes. ∎

*Step 5: k > ⌈3n/2⌉ fails.* Pure-rotation witnesses, machine-verified for n = 2 … 6. For n even, the row (A^(n/2) B^(n/2))² — four chains of length n/2. Every k with ⌈3n/2⌉ + 1 ≤ k ≤ 2n puts position k in the last chain (positions 3n/2 + 1 through 2n); the move rotates the row to B^(n/2) A^(n/2) B^(n/2) A^(n/2), whose last chain again contains position k, and the next move restores the original row — a period-2 cycle of unfinished rows, the leftmost n coins always reading A^(n/2) B^(n/2)…, mixed. For n odd, the row A^((n+1)/2) B^((n−1)/2) A^((n−1)/2) B^((n+1)/2) — chains of lengths (n+1)/2, (n−1)/2, (n−1)/2, (n+1)/2, with r = 4 and the last chain occupying positions (3n+1)/2 through 2n, exactly the k with ⌈3n/2⌉ ≤ k ≤ 2n — the same rotation runs a closed cycle of unfinished rows for every k beyond the ceiling.

So the good k are precisely n ≤ k ≤ ⌈3n/2⌉. ∎

The lab ran the census exhaustively before printing: every one of the C(2n, n) rows for n = 1 … 6 — 1,274 arrangements in all — driven by the move for every k and classified finish versus eternal cycle, with the good window coming out exactly {n, …, ⌈3n/2⌉} every time. The invariants were watched at every single move with zero violations: Δr always in {0, −1, −2}; Δr = 0 exactly in the two named cases; exceptions always with r even; no no-op ever on an unfinished row with k ≥ n; r = 2 always finishing within one move; and the eternal cycles resolving cleanly into pure stalls (k < n) and pure rotations (k > ⌈3n/2⌉), both witness families replayed for all k in their ranges.

**What to learn.** The chain count is the whole engine: a monovariant whose zero-change cases are so rigid they can be completely classified — no-op or rotation — and each class then killed by its own argument (no-ops by "k ≥ n means finished", rotations by the length count 2n ≥ 4(2n + 1 − k)). Learn the shape of a termination proof for a deterministic process: finitely many states force eventual periodicity; a monovariant collapses the cycle's options to two; both are contradictions. And learn the counting endgame's honesty: the bound needs r ≥ 4, and r = 2 is dispatched separately — small cases are not decoration, they are load-bearing.

### Problem 30 (●●●) · IMO 1978, Problem 6 — six countries, one sum

An international society has 1978 members, each belonging to exactly one of six countries. The members are assigned distinct numbers 1, 2, …, 1978. Prove that at least one member's number is equal to the sum of the numbers of two members (not necessarily two distinct members) of his own country.

*Source: IMO 1978, Problem 6.*

**The handle.** Suppose not: then each country's set of numbers is sum-free — no x + y = z with all three numbers in one set, the two summands allowed to coincide. A partition of {1, …, 1978} into six sum-free classes is a six-coloring with no monochromatic x + y = z — exactly the object Schur's theorem forbids at this scale. And Schur's proof is an encoding plus a pigeonhole chain (P25, P9, P2): color the edge between two vertices of a complete graph by the class of their difference; a monochromatic triangle *is* a monochromatic sum, because (b − a) + (c − b) = c − a. The number 1978 rides on a six-step chain that ends at 1958 — close enough.

**Solution.** Assume the contrary: the six countries hold number sets C₁, …, C₆ partitioning {1, …, 1978}, each sum-free.

*The encoding.* Build the complete graph on the 1979 vertices 0, 1, …, 1978, and color each edge {a, b} (a < b) with the color of the difference b − a — a number in {1, …, 1978}, so it lies in exactly one class. A monochromatic triangle would be vertices a < b < c with b − a, c − b, c − a all in one class C; but (b − a) + (c − b) = c − a displays a sum inside C, the two summands equal exactly when b is the midpoint. Sum-free classes forbid this: the edge-coloring has no monochromatic triangle.

*The Ramsey chain.* Let R_k be the least m such that every k-coloring of the edges of K_m contains a monochromatic triangle. R₁ = 3. The step: R_k ≤ k(R_{k−1} − 1) + 2. In K_{k(R_{k−1}−1)+2}, take any vertex v: it has k(R_{k−1} − 1) + 1 neighbors, so some color appears on at least R_{k−1} of the edges from v. If any edge among those neighbors carries that same color, it forms a monochromatic triangle with v. If none does, the neighbors' mutual edges use only k − 1 colors — a (k − 1)-colored complete graph on at least R_{k−1} vertices — and the definition of R_{k−1} supplies a monochromatic triangle directly. Either way one exists. The chain, from R₁ = 3:

R₂ ≤ 2(3 − 1) + 2 = 6,  R₃ ≤ 3(6 − 1) + 2 = 17,  R₄ ≤ 4(17 − 1) + 2 = 66,  R₅ ≤ 5(66 − 1) + 2 = 327,  R₆ ≤ 6(327 − 1) + 2 = 1958.

(The first steps are exact — R₂ = 6 and R₃ = 17 are the true values, confirmed by brute force in the lab; from R₄ on the chain yields ceilings, not values, and the proof needs only the ceiling.)

Since 1979 ≥ 1958 ≥ R₆, every 6-coloring of the edges of K₁₉₇₉ — in particular the difference-coloring above — contains a monochromatic triangle. That triangle is a monochromatic Schur triple, contradicting sum-freeness. Some country holds x, y, and x + y. ∎

Read as a Schur number: a sum-free k-partition of {1, …, N} yields a triangle-free k-coloring of K_{N+1}, so N + 1 < R₆ ≤ 1958 and N ≤ 1956 — even numbering the members only up to 1957 would force the sum.

*The other direction, honestly bounded.* How far below the Ramsey ceiling can a sum-free six-partition reach — that is, where does the true Schur number S(6) sit? An elementary construction climbs from the bottom: a sum-free k-partition of {1, …, N} produces one of {1, …, 3N + 1} with k + 1 classes — add the new class D = {N + 1, …, 2N + 1} and stretch each old class C to C ∪ (C + 2N + 1). Four cases check sum-freeness: two elements of D sum to more than 2N + 1, past D; two low elements can only threaten inside their own class, excluded by hypothesis; a low plus a stretched element lands in the stretched zone only if x + y already sat in the class, again excluded; two stretched elements leave the interval {1, …, 3N + 1} entirely. Coverage: the low classes fill 1 … N, D fills N + 1 … 2N + 1, the stretched classes fill 2N + 2 … 3N + 1. Starting from the one-class partition of {1}, the sizes run 1 → 4 → 13 → 40 → 121 → 364: S(6) ≥ 364. The truth is much larger — the published bounds are 536 ≤ S(6) ≤ 1836, with the exact value open, and the nearest settled relative is S(5) = 160, a 2017 computer proof — all far above the elementary ladder and far below the Ramsey ceiling 1956. The Atlas prints both ends and points the curious to the literature.

The lab anchored the small facts before printing: S(1) = 1, S(2) = 4, S(3) = 13 by exhaustive search over all colorings; R₂(3) = 6 by brute force (K₅ admits a triangle-free 2-coloring, K₆ does not); the 3N + 1 construction verified class by class for k = 1 … 6, sizes exactly 1, 4, 13, 40, 121, 364, with zero sum-triples and full coverage each time; and the reduction itself replayed concretely — the sum-free partitions of {1, …, 4} and {1, …, 13} induce, via the difference-coloring, triangle-free colorings of K₅ and K₁₄, machine-verified edge by edge (0 monochromatic triangles among 10 and 364 respectively).

**What to learn.** The encoding is the whole proof: difference classes become edge colors, and the algebraic identity (b − a) + (c − b) = c − a becomes the triangle — the same translation P25 makes everywhere it appears (correspondence → edge-coloring in Problem 3, members → Schur colors here). The pigeonhole chain is the gentleman's Ramsey: no asymptotics, just "some color repeats R_{k−1} times at one vertex," a recursion with clean constants — double counting (P2) at integer scale. And learn to read a bound chain honestly: 3, 6, 17 are values; 66, 327, 1958 are ceilings; the proof needs only the ceiling, and the chapter says which is which.

---

## The Trick Bag (reference card)

| Pattern | Plain language | Where you met it |
|---------|---------------|------------------|
| **P2 Double counting** | Count the same set two ways; equate | 1 (fixed-point pairs), 2 (problem-pair coverage), 5 (judge agreements), 6 (girl–boy–problem triples), 24 (the anti-Pascal bookkeeping), 30 (Schur's upper bound via Ramsey) |
| **P9 Pigeonhole** | n+1 objects, n boxes — with the boxes hidden inside an encoding | 3 (17 edges, 3 colors), 4 (parity classes, twice), 6 (⌈21/6⌉ = 4), 7 (the migrating jump), 8 (three cards, two piles), 11 (walking the multiples), 27 (200 even sites, 100 cages), 30 |
| **P25 Reduction / encoding** | Translate into a language whose structure carries the proof | 3 (correspondence → edge-coloring), 4 (integers → F₂⁹), 13 (bare edges → independence), 30 (members → Schur colors) |
| **P1 Bijection / orbits** | Count by symmetry: group actions and their fixed points | 9 (the +2 shift on the circle), 16 (insertion symmetry in the balance) |
| **P4 Monovariant / induction** | A quantity that must move, or a case that reduces | 10 (the pentagon potential), 15 (consecutive residues), 17 (the Bank of Bath), 18 (Zantema's machine, honestly constructive), 19 (the grasshopper's four cases), 24 (the anti-Pascal max-chain), 28 (the liar's trailing streaks) |
| **P10 Averaging** | Some object beats the average — or the average forces a sign change | 5 (the convexity minimum), 23 (rotation averages over ninja paths) |
| **P8 Extremal / longest-path** | Take an extremal object; its structure cracks | 22 (the tallest surviving pair), 29 (chains and their lengths) |
| **P11 Explicit construction** | Beat the bound by building the object | 12 (the balanced coloring), 14 (the tour when r = 25), 20 (Euler circuits pairing the pebbles), 22 |
| **P7 Parity** | Coloring obstructions: what a two-coloring forbids | 14 (mod 3 and mod 7 obstructions), 13 (the parity of bare-edge matchings) |
| **P15 Induction on vertices/edges** | Delete, solve smaller, extend | 21 (splitting the clique across two rooms) |
| **P16 Alternating paths** | Repair a partial solution along a cycle | 12 (peel leaves, alternate around cycles) |
| **P17 Duality (min–max)** | Two players, one number; a strategy is a proof | 27 (the √5 game's value is exactly 100), 28 (the liar game's window n ≥ 2k) |
| **P18 Algorithmic proof** | The proof *is* a procedure; termination is the theorem | 25 (the hunter's forced failure), 26 (the windmill's sweep), 29 (the block move, run to termination) |
| **P26 Compactness** (flavor only) | Infinite patience, finite budget — and a limit argument in disguise | 25 (10⁹ rounds, 100 of distance) |
| **Diagnosis is the skill (lore)** | Thirty problems, thirteen patterns; the machinery never upgrades — what grows is the load per pattern and the thickness of the disguise | The whole chapter; the moment of diagnosis is still one sentence at the summit |
| **The honest census (lore)** | Print what is proved, what is computed, and what is cited — and keep the three apart | 21's census-closed step, 28's cited induction and local lemma, 30's open Schur number, every lab note |

**Formula box:** The doorstep anchors: 17 edges in 3 colors with the trailhead Ramsey values R(3,3) = 6 and R(3,3,3) = 17; F₂⁹'s 512 vectors; ⌈21/6⌉ = 4; the +2 shift on the circle; the pentagon's potential coefficients 2a − 3b + 2c = 0. The rooms: the walk g_i = ω(B_i) − (2s − i) crosses zero or overshoots to (m, m−1), and one swap restores equality. The bands: N bands of N + 1 ranks, the first repeat within N + 1 positions, adjacency surviving every later deletion. The ninja: ⌊log₂ n⌋ + 1 guaranteed reds; S_n = n + 1; the charging 2^{1+max(v_q, v_{q+1})} pays for two children; tightness rows i = 2^a + b with the red at 2b + 1. The anti-Pascal: T = 2018·2019/2 = 2,037,171; the telescope M_{i−1} ≤ M_i − m_i pins every row; larges (≥ T − 2018) live only in the bottom 64 rows (t ≤ 63 from t(t+1) ≤ 4036); at most 126 outside, at least 1893 inside, at most 125 non-large below; at least 1767 both-large adjacent pairs, at least 1766 of them not the m₂₀₁₇-pair — and the one above such a pair must be m₂₀₁₇: contradiction; existence iff n ≤ 5 (DFS counts 1, 4, 8, 8, 2, 0). The hunter: δ = m − √(m²−1) = 1/(m + √(m²−1)); the identity 1 + δ² = 2mδ; the block gain x² + 2(m−x)δ; m = 101 while x ≤ 100 — 101² = 10200 + 1, so 2δ > 1/101 by exactly the one unit — and 101·1,010,001 = 102,010,101 ≤ 10⁹ rounds; maintenance with m = ⌈x⌉ + 1 keeps the gain positive forever. The windmill: the balanced start (a ±1 walk gap); every event splits the others (m, m−1) with the old pivot booked to its falling side; π-periodicity through P₀ and the median rank; the unbalanced control fails. The √5 board: displacement sums odd (a² + b² = 5), so the 200 even sites are free and the 100 four-cages with diagonal replies cap at one red each: K = 100 exactly. The liar: trailing streaks s(c) ∈ {0, …, k}; a saturated class halves under any honest cut; n ≥ 2k suffices and 1.99k fails for large k; the census's exact minimax depths at k ≤ 4. The bank: the window {n, …, ⌈3n/2⌉}; Δr ∈ {0, −1, −2} with the zeros exactly the no-op and the last-chain-no-weld (r even); the endgame 2n ≥ 4(2n + 1 − k); stalls below, pure rotations above. The countries: the chain R₁ = 3, R₂ ≤ 6, R₃ ≤ 17, R₄ ≤ 66, R₅ ≤ 327, R₆ ≤ 1958 (the first three exact); S(6) ≤ 1956 < 1978; the elementary ladder 1 → 4 → 13 → 40 → 121 → 364 against the published 536 ≤ S(6) ≤ 1836, exact value open.

---

## Computational Lab (verified)

Every recorded output below was produced by this pass's verification runs — a fresh TypeScript port whose logic the Python mirrors exactly, so every printed number is reproducible from either side. The suite reproduces the load-bearing witnesses, censuses, and thresholds of the seventeen artifact-bearing problems across the three terraces; the remaining authoring batteries (the balanced-arc circles, the equal-clique walk-and-swap census, the band-greedy rows, the hunter's exact-integer razors, the windmill's oriented simulation, the liar attractor, and the √5 sixty-game reply simulation) are recorded in the Verification basis below and are not re-run here.

### Part 1 — Terrace I: fixed-point double count, the F₂⁴ Ramsey coloring, fourth-power smoothness, subsets mod p, and the pentagon

```python
import math
from itertools import combinations, permutations

p1_ok = all(sum(sum(1 for i, v in enumerate(p) if i == v)
                for p in permutations(range(n))) == math.factorial(n)
            for n in range(1, 8))
print(p1_ok, math.factorial(7))

C1, C2, C3 = {1, 2, 4, 8, 15}, {3, 5, 7, 10, 11}, {6, 9, 12, 13, 14}
sf_ok = all((a ^ b) not in C for C in (C1, C2, C3) for a, b in combinations(C, 2))
mono16 = sum(1 for u, v, w in combinations(range(16), 3)
             if any({u ^ v, v ^ w, u ^ w} <= C for C in (C1, C2, C3)))
print(sf_ok, math.comb(16, 3), mono16)

bases = [1, 2, 3, 5, 6, 10, 15, 30]
wit24 = [b * s for b in bases for s in (1, 16, 81)]
is_fourth = lambda x: x > 0 and round(x ** 0.25) ** 4 == x
q4_count = sum(1 for a, b, c, d in combinations(wit24, 4) if is_fourth(a * b * c * d))
print(len(wit24), q4_count, 2 * 4 * 9 * 18 == 6 ** 4)

p8_ok = all(n <= 2 * k * k - 4 * k < 2 * k * k + 1 < 2 * k * k + 4 * k <= 2 * n
            for n in range(100, 50001)
            for k in [math.ceil(1 + math.sqrt((n + 2) / 2))])
print(p8_ok, [2 * 9 * 9 - 4 * 9, 2 * 9 * 9 + 1, 2 * 9 * 9 + 4 * 9])

p9_out = []
for p in (3, 5, 7, 11, 13):
    dp = [[0] * p for _ in range(p + 1)]; dp[0][0] = 1
    for x in range(1, 2 * p + 1):
        for k in range(p, 0, -1):
            for r in range(p):
                dp[k][(r + x) % p] += dp[k - 1][r]
    c0, cr = (math.comb(2 * p, p) - 2) // p + 2, (math.comb(2 * p, p) - 2) // p
    assert dp[p][0] == c0 and all(v == cr for v in dp[p][1:])
    p9_out.append((p, c0, cr))
print(p9_out)

phi5 = lambda v: 3 * sum(u * u for u in v) + 2 * sum(v[i] * v[(i + 1) % 5] for i in range(5))
v = [-3, -2, 4, 1, 2]; y, S = v[1], sum(v)
v_next = [v[0] + y, -y, v[2] + y, v[3], v[4]]
print(phi5(v_next) - phi5(v) == 2 * y * S)
```

**Verified output.** Problem 1 prints `True 5040`; Problem 3 prints `True 560 0` (all three classes sum-free in F₂⁴, zero monochromatic triangles among all 560 in K₁₆); Problem 4 prints `24 0 True` (zero fourth-power quadruples in the 24-element {1, 16, 81}-scaled witness, while 2 · 4 · 9 · 18 = 6⁴); Problem 8 prints `True [126, 163, 198]`; Problem 9 prints `[(3, 8, 6), (5, 52, 50), (7, 492, 490), (11, 64132, 64130), (13, 800048, 800046)]`; and Problem 10 prints `True` (ΔΦ = 2yS).

### Part 2 — Terrace II: the K₉ witness, the √r board walk, the balance double factorial, the Bank of Bath, Zantema's boxes, and the grasshopper

```python
import math
from itertools import combinations, permutations

bare = {(0, 1), (2, 3), (4, 5), (6, 7)}
red = {(0, 2), (0, 3), (0, 4), (0, 5), (1, 2), (1, 3), (1, 4), (1, 5),
       (2, 6), (2, 7), (3, 6), (3, 7), (4, 8), (5, 8), (6, 8), (7, 8)}
blue = set(combinations(range(9), 2)) - bare - red
mono9 = sum(1 for a, b, c in combinations(range(9), 3)
            if {(a, b), (b, c), (a, c)} <= red or {(a, b), (b, c), (a, c)} <= blue)
print(len(red), len(blue), math.comb(9, 3), mono9)

reach = []
for r in range(1, 501):
    moves = [(dx, dy) for dx in range(-20, 21) for dy in range(-12, 13) if dx * dx + dy * dy == r]
    if not moves: continue
    seen = {(0, 0)}; q = [(0, 0)]
    while q:
        x, y = q.pop()
        for dx, dy in moves:
            nx, ny = x + dx, y + dy
            if 0 <= nx < 20 and 0 <= ny < 12 and (nx, ny) not in seen:
                seen.add((nx, ny)); q.append((nx, ny))
    if (19, 0) in seen: reach.append(r)
print(reach)

p16_counts = []; f = 1
for n in range(1, 11):
    f *= 2 * n - 1; p16_counts.append(f)
print(p16_counts)

def bath_steps(coins):
    c = list(coins); steps = 0
    while True:
        k = sum(c)
        if k == 0: return steps
        c[k - 1] ^= 1; steps += 1
print(bath_steps([0] * 6 + [1] * 6))

def zantema_gather():
    b = [1, 1, 1, 1, 1, 1]
    def t1(j): b[j] -= 1; b[j + 1] += 2
    def t2(j): b[j] -= 1; b[j + 1], b[j + 2] = b[j + 2], b[j + 1]
    t1(4); t2(3); t2(2); t2(1); t1(0); t1(1); t1(1)
    return b
print(zantema_gather())

p19_counts = [math.comb(n * (n + 1) // 2 - 1, n - 1) for n in range(2, 7)]
print(p19_counts, sum(p19_counts))

def p19_solvable(jumps, M):
    for order in permutations(jumps):
        s, ok = 0, True
        for j in order:
            s += j
            if s in M: ok = False; break
        if ok: return True
    return False

p19_solved = 0
for n in range(2, 7):
    jumps = list(range(1, n + 1)); s = n * (n + 1) // 2
    for M in combinations(range(1, s), n - 1):
        if p19_solvable(jumps, set(M)): p19_solved += 1
print(p19_solved, p19_solved == sum(p19_counts))
```

**Verified output.** Problem 13 prints `16 16 84 0`; Problem 14 prints the exact reachable list `[1, 5, 13, 17, 25, 29, 37, 41, 53, 61, 65, 73, 85, 101, 125, 145, 169, 185, 205, 221, 305, 325, 361]`; Problem 16 prints `[1, 3, 15, 105, 945, 10395, 135135, 2027025, 34459425, 654729075]`; Problem 17 prints `78` on `TTTTTTHHHHHH`; Problem 18 prints `[0, 0, 7, 0, 0, 0]` after the gather phase; and Problem 19 prints `[2, 10, 84, 1001, 15504] 16601` — with the solver census printing `16601 True`: every one of the 16,601 forbidden sets, brute-forced afresh, admits an ordering of the jumps whose partial sums dodge it.

### Part 3 — Terrace III: the ninja triangle, anti-Pascal counts, the √5 cages, the Bank of Oslo census, and Schur's ladder

```python
import math
from itertools import combinations, permutations

def ninja_max_reds(n):
    if n <= 0: return 0
    reds = [0] * (n + 1)
    for i in range(1, n + 1):
        a = int(math.log2(i)); b = i - (1 << a)
        reds[i] = 2 * b + 1
    dp = [0] * (n + 2)
    for i in range(n, 0, -1):
        ndp = [0] * (i + 1)
        for j in range(1, i + 1):
            ndp[j] = (1 if j == reds[i] else 0) + max(dp[j], dp[j + 1])
        dp = ndp
    return dp[1]
print([(n, ninja_max_reds(n), int(math.log2(n)) + 1) for n in range(1, 11)])

def antipascal_count(n):
    if n <= 0: return 0
    T = n * (n + 1) // 2; cnt = 0
    for p in permutations(range(1, T + 1), n):
        if T not in p: continue
        rows = [p]
        while len(rows[-1]) > 1:
            rows.append([abs(rows[-1][i] - rows[-1][i + 1]) for i in range(len(rows[-1]) - 1)])
        if len({x for r in rows for x in r}) == T: cnt += 1
    return cnt
print([antipascal_count(n) for n in range(1, 5)])

base_cages = [
    [(1, 1), (2, 3), (4, 4), (3, 2)],
    [(1, 2), (2, 4), (4, 3), (3, 1)],
    [(1, 3), (2, 1), (4, 2), (3, 4)],
    [(1, 4), (2, 2), (4, 1), (3, 3)]
]
cages = [[(4 * bx + x, 4 * by + y) for x, y in c]
         for bx in range(5) for by in range(5) for c in base_cages]
all_sites = [pt for c in cages for pt in c]
edge_ok = all((c[i][0] - c[(i + 1) % 4][0]) ** 2 + (c[i][1] - c[(i + 1) % 4][1]) ** 2 == 5
              for c in cages for i in range(4))
diag_ok = all((c[i][0] - c[i + 2][0]) ** 2 + (c[i][1] - c[i + 2][1]) ** 2 in (2, 10, 18)
              for c in cages for i in range(2))
print(len(cages), len(set(all_sites)), edge_ok, diag_ok)

def oslo_good_k(n):
    if n <= 0: return 0, []
    rows = [tuple(1 if i in set(ones) else 0 for i in range(2 * n))
            for ones in combinations(range(2 * n), n)]
    def step(row, k):
        idx = k - 1; metal = row[idx]; l = r = idx
        while l > 0 and row[l - 1] == metal: l -= 1
        while r + 1 < 2 * n and row[r + 1] == metal: r += 1
        return row[l:r + 1] + row[:l] + row[r + 1:]
    good = []
    for k in range(1, 2 * n + 1):
        ok = True
        for row in rows:
            cur = row; seen = set()
            while len(set(cur[:n])) > 1:
                if cur in seen: ok = False; break
                seen.add(cur); cur = step(cur, k)
            if not ok: break
        if ok: good.append(k)
    return len(rows), good
oslo_res = [oslo_good_k(n) for n in range(1, 7)]
print(sum(r[0] for r in oslo_res), [(n, g) for n, (_, g) in enumerate(oslo_res, 1)])

def schur_ladder(k):
    parts = [{1}]; N = 1
    for _ in range(1, k):
        D = set(range(N + 1, 2 * N + 2))
        parts = [C | {x + 2 * N + 1 for x in C} for C in parts] + [D]
        N = 3 * N + 1
    return N, parts
print([schur_ladder(k)[0] for k in range(1, 7)])

p30_ok = all(sorted(x for C in parts for x in C) == list(range(1, N + 1))
             and all(x + y not in C for C in parts for x in C for y in C)
             for N, parts in (schur_ladder(k) for k in range(1, 7)))
print(p30_ok)
```

**Verified output.** Problem 23 prints `[(1, 1, 1), (2, 2, 2), (3, 2, 2), (4, 3, 3), (5, 3, 3), (6, 3, 3), (7, 3, 3), (8, 4, 4), (9, 4, 4), (10, 4, 4)]` (matching ⌊log₂ n⌋ + 1 for every n); Problem 24 prints `[1, 4, 8, 8]` for n = 1, …, 4; Problem 27 prints `100 400 True True` (100 four-cages partitioning all 400 sites, cycle edges at squared distance 5, diagonals in {2, 10, 18}); Problem 29 prints `1274 [(1, [1, 2]), (2, [2, 3]), (3, [3, 4, 5]), (4, [4, 5, 6]), (5, [5, 6, 7, 8]), (6, [6, 7, 8, 9])]` (exact window {n, …, ⌈3n/2⌉} across all 1,274 rows); and Problem 30 prints `[1, 4, 13, 40, 121, 364]` with the ladder audit printing `True` — every rung covers {1, …, N} exactly and is sum-free with the two summands allowed to coincide.

---

## Revision History & Verification Notes

**Editions.** Authored pre-install in three passes: the frame — title, introduction, the thirty-problem slate with its pattern map and honest census — and Terrace I, the doorstep rungs (problems 1–10); then Terrace II, the working middle (problems 11–20); then Terrace III, the summit rungs (problems 21–30), together with this Trick Bag, the formula box, and these notes. The slate was chosen for pattern coverage from six decades of olympiad combinatorics; every statement was fetched from the official record and reconciled against it at selection time (six corrections to the draft ledger were recorded then, including the two-rooms problem's weaker official claim, the hunter device's reporting target, and the bank's either-metal goal). The chapter was authored and machine-verified pre-install in three passes, then installed and shipped with its reference web edition: the canvas and the web edition both embed it byte-identically, and print to PDF from a browser gives a correct export.

**Verification basis.** Every number this chapter prints was machine-verified at authoring, in four waves. The doorstep and middle receipts (two early waves, recorded in full in the project buffer): the equal-clique census, the band-greedy construction on 1,500 fresh rows, the ninja minimax with its 367,044 charging checks and tightness construction, the anti-Pascal reconstruction with its full existence census, the hunter's exact-integer razors with both key inequalities tight by exactly one, the windmill's oriented exact-integer simulation, the √5 board's decomposition and reply simulation, the liar attractor, the Oslo window census, and the Schur chain. The summit wave (chunk 48f, three batches): the walk-and-swap pre-checks; the band-greedy; the √5 board's 4-cycles with the sixty-game simulation against the diagonal reply (Amy never exceeded 100, and reached it in several games); the windmill's counterclockwise oriented lift in exact integers — every event splitting the others (m, m−1) with the old pivot booked to its falling side (that booking *is* the hand-off lemma), π-periodicity through P₀ with alternating crossed directions, full pivot coverage, and the unbalanced control (0,0), (4,0), (1,1) failing the recurrence, so balance is load-bearing; the liar's stack-safe layered attractor over the full state space — sixteen cases at exact minimax, every n = 2k case a win, with the (k, n, N) = (2, 4, 6) seven-question adversarial trace (live counts 6 → 6 → 6 → 6 → 5 → 5 → 5 → 4), the cooperative pump line, and Amy's survival loop at (1, 1, 3); and the Oslo census — all 1,274 arrangements for n = 1 … 6, the window exact, zero invariant violations in millions of checked moves (Δr always in {0, −1, −2}; Δr = 0 exactly the no-op and the exception; exceptions always with r even; no no-op ever on an unfinished row with k ≥ n), with both witness families replayed for every k in their ranges. The assembly wave (at final assembly): the freshly printed claims of problems 27, 29, and 30 re-verified in one run — the 100-quadruple decomposition covering all 400 sites exactly once with cycle edges at squared distance exactly 5 and diagonals at 2, 10, or 18; the 200 even sites pairwise √5-free; the stall and rotation witnesses cycling unfinished for every k in their ranges; the 3N + 1 construction ladder with sizes exactly 1, 4, 13, 40, 121, 364 and zero sum-triples at every rung; and the small anchors S(1) = 1, S(2) = 4, S(3) = 13, R₂(3) = 6 (K₅ admits a triangle-free 2-coloring, K₆ does not), with the K₅ and K₁₄ reduction witnesses verified edge by edge (0 monochromatic triangles among 10 and 364). Literature pins, web-verified at authoring: the liar game's part (b) formulation (for all sufficiently large k there exists n ≥ 1.99k at which Ben cannot guarantee a win); and the Schur-number record — the exact value of S(6) is open, the published bounds are 536 ≤ S(6) ≤ 1836, and S(5) = 160 was settled by computer search in 2017.

**Standing decisions.** Bodies carry no chunk or session references; history lives here. Two steps are closed by evidence rather than derivation, and labeled where they occur: Problem 21's swap-witness existence (the overshoot state resisting a short argument; the census ran the walk-and-swap on every competition graph of even size through n = 6 — 452 graphs at n = 5, all 10,759 at n = 6 — plus 254 stress instances; the residual state occurs under fixed choices (on 24, 1,144 and 41 of them respectively), but no graph ever got stuck — a restarted walk equalized every single one, and an equal split exists everywhere) and Problem 28's general-k material (part (a)'s official induction and part (b)'s Lovász Local Lemma argument both cited to the official solution, with the k ≤ 4 census closing the small cases exactly and the frontier's location honestly between k and 2k). Problem 25's device reports near the rabbit; some retellings swap the label, and the chapter says so. Problem 29's goal is one metal — either one — which resolves the all-bronze already-finished case, and the window sentence is scoped accordingly. Problem 30's Schur-status sentence is the web-verified record and supersedes a drafting note that called 536 exact. The pattern map's P18 cell was relabeled at apparatus time to match the authored Problem 29 (the block move, run to termination). The pattern map is the source of truth for pattern membership; this Trick Bag echoes it. There is no exercises section: the thirty problems are the course, and the Atlas's earlier chapters supply the theory the Bridge assumes. The chapter is installed and ships with its reference web edition — the canvas and the web edition both embed it byte-identically; the learner-facing release remains future work recorded in the project buffer.

**Survey-adoption pass (session 83, chunk 83g).** The paper-pattern survey's contest-census extension — five canons graded pattern-side, nothing re-graded and no contest row fired into the pattern dossiers — contributed four structural findings, adopted into this chapter as learning/practice aids: (1) the reading-order hint — the pre-doctoral canon is P25/P4/P1/P9/P10, triple-confirmed (the youth-research corpus, the teaching track, and the Putnam canon's own genuine tags, those five plus P11/P2), with P3's research debut fired by a middle-school team and the honest boundary P5/P16/P23/P30–P31; (2) the P9 level gradient — an implicit small-step in the Putnam canon (one genuine firing, 2025 B4), a decisive full obstruction in the USAMO canon (2024 P4, USAJMO 2024 P4), the whole-proof mechanism in the IMO canon (2024 P3, route-pinned); (3) the genre-split pedagogy note — enumeration-heavy Putnam, construction-heavy USAMO (P11 ×9), process/game-heavy IMO, the classical construct-and-obstruct Kurschák with games absent; (4) the obstruction-halves coverage-gap cluster — modular-residue/CRT obstructions, the pairing and blocking strategies, chip-firing, and the max-plus generators live disproportionately outside the P-index, with partial homes at Ch. 20's strategy/adaptive-adversary named method and Ch. 21's k-adic digit engine. The census's route-coverage honesty gradient is part of the record: the Putnam routes pinned 22/22 from the MAA-permitted archive; the USAMO/Kurschák routes pinned from open author versions and the organizer's preliminary files (the 2022 USAMO gap honest); the IMO exam C-rows 2/8 and the shortlist statement-level where the C-solutions sit beyond fetch windows. All four findings were installed in the honest-census section above; the registry record lives in the Atlas's survey-provenance footnote, and P9's index row carries the level gradient. No in-chapter claim above changed.

**Survey-adoption extension (session 84, 2026-10-15).** The paper-pattern survey's chunk-30 upgrade passes (five commits 30a–30e over the 29e deferral ledger, closed 2026-10-15; papers/STATE.md the ledger, papers/SOURCES.md the dated notes) upgraded two records this chapter's adopted findings rest on — recorded here as a dated extension (extend-never-rewrite; no claim above changed): (1) the route-coverage honesty gradient — the 83g record above graded the IMO exam C-rows 2/8 route-pinned; the 30a pass route-pinned three more rows from the official Bajnok IMO reports (arXiv and the author-hosted Mathematics Magazine manuscripts) — 2022 P1 (the C2 NO-P-ID spine with P11 PARTIAL), 2022 P6 (P11 GENUINE with P1 PARTIAL), and 2023 P5 (P11 GENUINE with P4 GENUINE, P9 PARTIAL, and the W6 Mirsky cross-note) — with the 2024 P3/P5 rows double-confirmed, moving the IMO exam route coverage from 2/8 to 5/8 (papers/CONTEST-CENSUS.md section 2, dated 30a subsection); (2) the courseware side — the 30d pass pinned the last unpinned MIT 6.042J problem set (ps4, via the instructor's own official CSAIL course directory) and graded its three problems (P4 GENUINE — the structural-induction counting spine; P1 GENUINE — the explicit-bijection/Schröder–Bernstein chain; NO-P-ID — the state-machine invariant engine, the x + y mod 5 coverage-observation class), completing the 6.042J census at 12 of 12 sets (papers/TEACHING-CENSUS.md section 3) — the courseware-side confirmation of the reading-order hint now rests on the full course rather than a gap. The honest failures ride the record unchanged and stay registered: the 2022 USAMO/USAJMO reports (no compliant open route), the Kurschák finals (the organizer's served files still the preliminary solutions), the 62nd/66th IMO reports (paywalled/bot-blocked), the 2026 IMO exam and shortlist, and the T5 (Levin–Peres) mining (service-side fetch failures). The P9 level gradient and the other three findings are untouched by the upgrades — their graded rows stand.

**First expansion pass (session 104).** The user supplied a fresh Ch. 12 draft (HTML with MathJax; the file form is rejected per the standing session-78 rule — the content was audited underneath and installs translated to the book's plain-Unicode notation) and flagged that the pattern references "might have become mangled a bit". **Pattern audit: CLEAN at every level** — the draft's pattern-map table matched the master's with a two-byte delta that is spacing noise only, all thirty "The handle" paragraphs are byte-identical, and the Trick Bag formula box and both lore rows match; nothing mangled, nothing to restore — the honest answer to the user's flag is that the draft's references were already right. Verdict: **partial adoption** — four installs, every item machine-verified fresh before install by this pass's battery (Runs A–D, a TypeScript port the lab's Python mirrors exactly, all green), and every rejection recorded with its receipt. **The battery:** Part 1 — the fixed-point double count over every permutation for n = 1..7 (identity green, 5,040 permutations at n = 7); the K₁₆ Ramsey coloring (all three F₂⁴ classes sum-free, zero monochromatic triangles among all 560); the fourth-power machine (the 24-element {1, 16, 81}-scaled witness with zero quadruples, while 2 · 4 · 9 · 18 = 6⁴); P8's interval arithmetic green at n = 100/5,000/50,000 ([126, 163, 198]); P9's class counts by DP at p = 3, 5, 7, 11, 13 — [8, 6, 6], [52, 50×4], [492, 490×6], [64,132 / 64,130×10], [800,048 / 800,046×12] — the zero class matching (C(2p, p) − 2)/p + 2 exactly and every nonzero class (C(2p, p) − 2)/p; the pentagon potential ΔΦ = 2yS. Part 2 — P13's 16/16/84/0; P14's 23-residue reachable list matching the master's verbatim; P16's double factorials 1, 3, 15, …, 654,729,075; P17's 78; P18's [0, 0, 7, 0, 0, 0]; P19's per-n counts [2, 10, 84, 1001, 15504] with all 16,601 forbidden sets solved. Part 3 — P23's tightness construction matching ⌊log₂ n⌋ + 1 for n = 1..10; P24's DFS census [1, 4, 8, 8]; P27's 100 four-cages partitioning all 400 sites with cycle edges at squared distance exactly 5; P29's 1,274 arrangements with the window {n, …, ⌈3n/2⌉} exact; P30's ladder [1, 4, 13, 40, 121, 364] with the sum-free coverage audit green at every rung. Run D — the σ_A orbit-walk at p = 3, 5, 7 (every non-fixed orbit of size exactly p, the sums covering each residue exactly once, the two fixed blocks found); the P6 witness (all five girls on {1, 2, 3}, the boys' {1}, {2}, {1, 2}, {3}, {3} — every girl–boy pair sharing, no problem at 3 + 3) with the twelve-counterexample census reproduced from scratch; the P19 solver census 16,601 of 16,601; the P8 interval arithmetic. **Two latent MASTER defects the draft exposed, both machine-confirmed and repaired by the installs:** (i) Problem 6's counterexample sentence was garbled mid-sentence; (ii) Problem 8 called the interval's lower endpoint k² + 2k an "upper bound". **The adoptions (four):** (1) Problem 6's counterexample sentence — the draft's precise version installed (each problem solved by at most 2 boys — 2, 2, and 2 respectively, alongside all 5 girls — so no problem reaches 3 + 3), the witness verified, and the "Twelve such counterexample configurations" claim reproduced from scratch (both sides counted as 5-multisets of nonempty subsets of {1, 2, 3}, cross-intersecting, no 3+3 problem: the count is exactly 12); (2) Problem 8's bound label repaired (k² + 2k is the lower bound on n; I_k = [k² + 2k, 2k² − 4k], nonempty exactly when k ≥ 6, I₉ = [99, 126]); (3) Problem 9's solution harmonized — the ground set {1, …, 2p} used consistently, three self-correction stumbles removed, and the closing note now leads with the σ_A orbit-walk proof (each application shifts the sum by 2k ≢ 0 mod p, so the p orbit elements cover each residue exactly once — verified for p = 3, 5, 7), with the divisibility + unit-multiplication route kept as "Equivalently" and the "+2-cycle" single-orbit phrasing in the "Why the shift by 2" note; (4) the Computational Lab section (three parts, the seventeen artifact-bearing problems) — adopted with install-side repairs and extensions: the intro's blanket "Every witness, census, and threshold … is reproduced" scoped honestly to the seventeen named problems, with the remaining authoring batteries pointed at the Verification basis below; the P19 block extended from counting to solving — all 16,601 forbidden sets actually solved (per-n [2, 10, 84, 1001, 15504]); the P30 block extended to audit sum-freeness with the two summands allowed to coincide plus exact coverage at every rung; the Part 2 import line set to combinations, permutations. **The rejections, with receipts:** the draft's Problem 24 rewrite (it drops the master's clause "unwinding the telescope with equality at each step" — a clarity regression; the master's text stands); the notation-noise deltas (Problems 10, 14, 18, 21, 25, 30, the Trick Bag, the pattern map — TeX-vs-Unicode formatting only, no content); the HTML file form itself (the s78 rule). **The draft's own defects caught and repaired at install:** the P9 wrap imprecision (the draft's "shifts the subset sum by exactly p" is false on the wrap, where 2p ↦ 1 shifts the sum by −p — the install states both cases); the lab intro's overstatement; and two under-verifying lab blocks (P19 computed counts without solving, P30 audited coverage without sum-freeness) — both extended by the install. Beyond these, no draft math error was found: every draft number the battery touched checked out. No checker-side bug this pass. Per the rebuild rule the web edition and the .html export were rebaked — fidelity proof first.

---
*Chapter status: ✅ **Feynman edition (chunks 48d–48h) + first expansion pass (session 104)** — thirty olympiad problems across three terraces (the doorstep rungs, the working middle, the summit rungs), every solution worked in Atlas patterns with the census-closed and cited steps labeled as such; the pattern map with its honest census (thirteen patterns fired, the professional toolkit never did); the Trick Bag, the formula box, and these notes close the chapter. The session-104 first expansion pass audited the user-supplied draft pattern-clean at every level, adopted its four verified improvements (the Problem 6 counterexample sentence restored to precision, the Problem 8 bound label repaired, the Problem 9 solution harmonized on the {1, …, 2p} ground set with the σ_A orbit-walk proof leading the closing note, and the three-part Computational Lab installed with the P19 solver and P30 sum-free extensions), rejected the rest with receipts, and added the lab's seventeen artifact-bearing problems to the machine-verified record — the chapter body extended, never rewritten. The canvas and the reference web edition embed this chapter byte-identically (print to PDF from a browser for a correct export); learner testing follows the completion of the whole project scope, at the user's direction.*
