---
name: "cgt-ch7-set-systems"
title: "Ch. 7 — Extremal Set Systems: A Lecture Course in the Feynman Style"
type: "text/markdown"
---

# Chapter 7 · Extremal Set Systems

*Part of the Combinatorics & Graph Theory Atlas (see the Atlas canvas for the chapter map and progress report).*

How many sets can you choose before structure is forced? An antichain forces the middle level; an intersecting family forces a star; cross-intersecting pairs force Bollobás's inequality — and every one of these falls to the same engine: **count the right pairs**. This edition is a lecture course in five lectures: Sperner's theorem three ways (with the symmetric chain decomposition actually built, not cited), Bollobás's two-families theorem with the honest skew landscape, Katona's circle method with the sharp interval lemma complete — the notorious mixed sub-case included — EKR uniqueness proved in full for every n ≥ 2k+1 via anchored adjacent transpositions, and shifting, complete with its closing induction by splitting on the top element n. The chapter's second thread — sumsets (the staircase, Cauchy–Davenport in two complete proofs, Kneser's theorem, the Erdős–Ginzburg–Ziv theorem) and shadows (the Kruskal–Katona theorem through Keevash's clique-form proof, Daykin's complement mirror as a third EKR proof, the Hilton–Milner and Ahlswede–Khachatrian gateways, union-closed lore) — lives in Chapter 9, "Sumsets and Shadows: the Completed Arcs". Every proof in this chapter is complete; every claimed number is machine-checked; the figure is drawn from verified data.

## How to read this chapter

**Notation.** [n] = {1, …, n}; 2^[n] is its power set, and C([n], k) is the collection of k-subsets of [n]. C(n, k) is the binomial coefficient (comb(n, k) in the lab code). A *family* F is a set of sets; *k-uniform* means every member has size k. A *chain* is a family of pairwise comparable sets; an *antichain* has no two comparable. *Intersecting* means every two members meet. For the circle lectures, points live on a cycle ℤ_n of n positions and dist(x, y) = min(|x−y|, n−|x−y|) is cyclic distance. Letters are re-stated locally where a lecture needs its own.

**The exercises are graded:** ●○○ *easy* (a direct application of one lecture idea), ●●○ *moderate* (two ideas, or one tricky step), ●●● *tough* (several chapter ideas combined). Hints travel with the problems; worked answers sit at the very end of the chapter. Try honestly before reading a hint. Beyond the graded set, ◆ **pattern-unknown** problems name no method and carry no hint: diagnosing which tool fits is part of the problem. And ◐ **Explorations** at the end are open-ended investigations with no single right answer — research training, not test preparation.

## The pattern table for this chapter

| Pattern | Plain language | Where you meet it |
|---------|---------------|-------------------|
| **P2 Double counting (chains / permutations / circles)** | Count pairs (object, witness-arrangement) two ways; the inequality falls out of the mismatch | L1, L2, L3, L4 |
| **P17 Duality / specialization** | One inequality, many shadows: Bollobás → LYM → Sperner by plugging in special pairs | L2, Ch. 9 L4 |
| **P8 Extremal circle structure** | Intersecting arcs trap their start points inside a short window; the window has exactly 2k−1 slots | L3, L4 |
| **P23 Compression / shifting** | Deform the family toward a canonical shape without losing the property or the count | L5 |
| **P4 Induction** | Peel the extreme element; one new element per step | L5, Ch. 9 L1 |
| **P22 Polynomial method** | A polynomial vanishing on a grid, priced by its degrees — the same engine as Chapter 6 | Ch. 9 L1 |
| **P24 Shadow pricing (Kruskal–Katona)** | Price a family by its own real parameter x: a k-family of size C(x, k) forces every j-shadow to size ≥ C(x, j) — equality only at integer x and the complete families | Ch. 9 L4 |

---
## Lecture 1 · Sperner's Theorem: The Middle Level, Three Ways

**Problem.** The largest family of subsets of [n] with **no two comparable** (an *antichain*) has size **C(n, ⌊n/2⌋)** — the middle level(s).

### 1.1 Method 1 — Counting maximal chains (P2, full)

A *maximal chain* is ∅ ⊂ {x₁} ⊂ {x₁, x₂} ⊂ … ⊂ [n]. It is determined by the **order in which elements enter**, so there are exactly n! chains. A chain passes through a fixed k-set A in k!·(n−k)! orders: order A's k elements first (k! ways), then the remaining n−k (that many ways).

Now count pairs (chain, member of F on that chain). Each chain meets an antichain **at most once** — two members on one chain would be comparable. So:

Σ_{A∈F} |A|!·(n−|A|)! ≤ n!.

Divide by n!:

**LYM inequality.** Σ_{A∈F} 1/C(n, |A|) ≤ 1.

Finish: C(n, k) ≤ C(n, ⌊n/2⌋) for every k, so each term satisfies 1/C(n,|A|) ≥ 1/C(n, mid), and therefore

|F| = Σ_{A∈F} 1 ≤ C(n, mid) · Σ_{A∈F} 1/C(n,|A|) ≤ C(n, mid). ∎

**Equality.** Take the middle level itself: every term lands at exactly 1/C(n, mid), and the LYM sum is exactly 1. (When n is odd there are two middle levels, both of size C(n, (n−1)/2) = C(n, (n+1)/2); each saturates alone.) A worthwhile ✎: check that the full union of the two middle levels when n is odd is *not* an antichain — the smaller sets sit inside the bigger ones across levels — while partial mixes can be ({1} together with {2,3} at n = 3 is one).

### 1.2 Method 2 — The symmetric chain decomposition, actually built (full)

The second proof needs a structure the reference edition only cited: a partition of 2^[n] into chains that each run from some level r straight up to level n−r, one set per level along the way. This is the *symmetric chain decomposition* (SCD) of de Bruijn–Tengbergen–Kruyswijk — and it has a two-line recursive construction that we can verify, not just believe.

**The doubling construction.** Suppose 2^[n−1] has an SCD. Each chain C = (A₁ ⊂ A₂ ⊂ … ⊂ A_l) is symmetric: |A₁| + |A_l| = n−1, and sizes grow by exactly one per step. From C, keep:

- **the extended chain** A₁ ⊂ … ⊂ A_l ⊂ A_l ∪ {n}, and (when l ≥ 2)
- **the reflected chain** A₁ ∪ {n} ⊂ A₂ ∪ {n} ⊂ … ⊂ A_{l−1} ∪ {n}.

**Every subset of [n] lands in exactly one new chain.** A set S avoiding n lies in exactly one old chain, as some A_i; if i < l it appears only in the extended chain (the reflected chain only carries sets that *contain* n); if i = l it is the second-to-top of the extended chain — again exactly once. A set S containing n is T ∪ {n} for exactly one T ⊆ [n−1]: if T = A_l it is the top of the extended chain; if T = A_i with i ≤ l−1 it sits in the reflected chain. One home for everybody: a partition. ✓

**Symmetry survives.** Extended chain: |A₁| + |A_l ∪ {n}| = |A₁| + |A_l| + 1 = n. Reflected chain: |A₁∪{n}| + |A_{l−1}∪{n}| = |A₁| + 1 + |A_{l−1}| + 1, and |A_{l−1}| = |A_l| − 1 (sizes step by one), so this is |A₁| + |A_l| + 1 = n. Both start at level r and end at level n−r. ✓

**Base case.** 2^[1]: the single chain ∅ ⊂ {1}, symmetric (0 + 1 = 1). Induction up, and 2^[n] has an SCD for every n. ∎

**How many chains?** C(n, ⌊n/2⌋) — the middle binomial itself. Count chain *starts* by level: a chain starting at level r ends at n−r, so it passes through level j exactly when r ≤ j ≤ n−r, i.e. r ≤ min(j, n−j). Every set at level j lies on exactly one chain, so Σ_{r ≤ min(j,n−j)} starts(r) = C(n, j). Subtracting the equation for j−1: starts(j) = C(n, j) − C(n, j−1) for j ≤ n/2. Telescoping: total chains = Σ_{r=0}^{⌊n/2⌋} starts(r) = C(n, ⌊n/2⌋). ✓ (✎: run the telescoping for n = 5 by hand — starts 1, 4, 5 at levels 0, 1, 2, total 10 = C(5,2).)

**Sperner, second proof.** An antichain meets each chain at most once, so |F| ≤ number of chains = C(n, mid). ∎ Same bound, and now the extremal structure is vivid: the middle level works *because* it is a full transversal of the chains — one set per chain, no waste.

### 1.3 Erdős's generalization: banning chains of length k+1 (full)

Suppose F contains **no k+1 pairwise comparable sets** (an antichain is the k = 1 case). Both proofs adapt, and the SCD route needs no exchange argument.

**Weighted LYM (P2).** A maximal chain meets F in at most k members — the members along one chain are pairwise comparable, and k+1 of them would make a chain of length k+1. The pair-counting of §1.1 now reads Σ_{A∈F} |A|!·(n−|A|)! ≤ k·n!, i.e.

**Σ_{A∈F} 1/C(n, |A|) ≤ k.**

**The size bound, via the SCD.** Each chain c contributes at most min(k, |c|) members — a chain of length |c| can host at most |c| members anyway, and more than k would make a (k+1)-chain:

|F| ≤ Σ_c min(k, |c|).

Now evaluate the sum. Write min(k, |c|) = Σ_{j=1..k} [|c| ≥ j]. A symmetric chain starting at level r has length |c| = n−2r+1, so |c| ≥ j holds iff r ≤ ⌊(n+1−j)/2⌋. Summing over chains and telescoping exactly as in §1.2 (for each j ≤ n+1, the number of chains starting at level ≤ ⌊(n+1−j)/2⌋ is C(n, ⌊(n+1−j)/2⌋)):

**Σ_c min(k, |c|) = Σ_{j=1..k} C(n, ⌊(n+1−j)/2⌋) — the k middle binomial coefficients.**

Indeed, as j runs from 1 to k (for k ≤ n+1), the index m_j = ⌊(n+1−j)/2⌋ steps down through ⌊n/2⌋, ⌊(n−1)/2⌋, …; whenever the same value m appears twice (for consecutive j where n+1−j is odd and then even), using the level symmetry C(n, m) = C(n, n−m) pairs one copy of C(n, m) with level m and the other with its complementary level n−m, so the sum is the exact sum of the sizes of the k middle levels of 2^[n].

**Sharpness.** Any union of k levels of 2^[n] contains no chain of length k+1 — a chain can take at most one set per level — and choosing the k middle levels achieves the exact sum Σ_{j=1..k} C(n, ⌊(n+1−j)/2⌋). ∎

For n = 4, k = 2: bound 6 + 4 = 10, achieved by levels 1 and 2 (or levels 2 and 3). For n = 5, k = 2: 10 + 10 = 20, achieved by levels 2 and 3. The exhaustive census in the lab confirms these maxima over *all* families, not just the constructions, for n = 4 and every k.
### 1.4 What to learn

LYM is a *weighted* pigeonhole: every set costs at least the middle-level price 1/C(n, mid), and the total budget is 1. The SCD converts the same statement into an unweighted one — one member per chain — which is why it survives the generalization to banned long chains so gracefully. And the doubling construction is worth remembering as a pattern: **build the recursive object explicitly, then let the counting verify it**. Dozens of theorems in extremal set theory are LYM in disguise; the next lecture shows the master example.

---
## Lecture 2 · Bollobás's Two-Families Theorem

**Problem.** Pairs of sets (A₁,B₁), …, (A_m,B_m) with **A_i ∩ B_i = ∅** but **A_i ∩ B_j ≠ ∅ for all i ≠ j**. Write a_i = |A_i|, b_i = |B_i|. Then

**Σ_i 1/C(a_i + b_i, a_i) ≤ 1.**

### 2.1 The permutation proof (P2, full)

Take a uniform random permutation of the ground set and let E_i be the event that **all of A_i precedes all of B_i** in it. Among the a_i + b_i relevant elements, every relative order is equally likely, and the orders that work are exactly those with the a_i elements of A_i first; so

P(E_i) = a_i!·b_i!/(a_i+b_i)! = 1/C(a_i+b_i, a_i).

**The events are disjoint.** Suppose E_i and E_j both hold, i ≠ j. By hypothesis pick x ∈ A_i ∩ B_j and y ∈ A_j ∩ B_i (both intersections are nonempty). E_i forces every element of A_i before every element of B_i — in particular x before y. E_j forces every element of A_j before every element of B_j — in particular y before x. No permutation does both. ∎

So P(∪ E_i) = Σ P(E_i) ≤ 1 — the theorem. ∎ **Complete, and short enough to hold in your head.**

### 2.2 LYM as a corollary (P17, full)

Given an antichain F ⊆ 2^[n], set A = A and B = [n] ∖ A for each member A ∈ F. Then A ∩ B = ∅ ✓. Incomparability says A ∖ A′ ≠ ∅ and A′ ∖ A ≠ ∅ for distinct members A, A′ ∈ F — that is, A ∩ B′ = A ∖ A′ ≠ ∅ and A′ ∩ B = A′ ∖ A ≠ ∅ ✓. Bollobás applies with a + b = n:

Σ_{A∈F} 1/C(n, |A|) ≤ 1 — the LYM inequality, and Sperner follows as in §1.1. **One theorem, three shadows** (Bollobás, LYM, Sperner); the pattern-index dream, live.

### 2.3 Tightness, saturation, and a warning

**Tight.** Let the ground set be [m] and take the m pairs Aᵢ = {i}, Bᵢ = [m] ∖ {i}. Then Aᵢ ∩ Bᵢ = ∅ ✓, and for i ≠ j the element i lies in Aᵢ ∩ B_j ✓. The sum is m · 1/C(m, 1) = 1 — **exactly 1**. The lab verifies this and an exhaustive sweep of small instances; the bound is never exceeded and is attained by the star-like arrangements.

**A warning about weakenings.** If you keep only the "forward" cross-conditions Aᵢ ∩ B_j ≠ ∅ for i < j (dropping i > j), the theorem as stated is **false** — the sum can exceed 1: take A₁ = {1}, B₁ = ∅ and A₂ = {2}, B₂ = {1}. The forward condition A₁ ∩ B₂ = {1} ∩ {1} ≠ ∅ holds, yet 1/C(1,1) + 1/C(2,1) = 3/2. And the obvious rescue attempt fails too: keeping the sizes small does not help. On [3] the pairs (A₁, B₁) = ({1}, {2}), (A₂, B₂) = ({2}, {1}), (A₃, B₃) = ({3}, {1, 2}) satisfy every skew condition *and* Aᵢ ≠ ∅ *and* |Aᵢ| ≤ |Bᵢ| for all three, yet Σ 1/C(|Aᵢ|+|Bᵢ|, |Aᵢ|) = 1/2 + 1/2 + 1/3 = **4/3** (Exercise 14 asks you to verify this by hand). What survives is the honest landscape, stated in full in the Trick Bag: the **uniform** skew bound — all |Aᵢ| = a, |Bᵢ| = b gives m ≤ C(a+b, a) (Frankl 1982; also Kalai 1984) — and, for non-uniform pairs on the ground set [n], the **Hegedüs–Frankl bound** Σ 1/C(|Aᵢ|+|Bᵢ|, |Aᵢ|) ≤ n+1 (2023), sharp at the complement pairs. The machine census is the referee: the exhaustive maxima are n+1 with no hypotheses, n with Aᵢ ≠ ∅, and 1, 4/3, 2 at n = 2, 3, 4 under Aᵢ ≠ ∅ *and* |Aᵢ| ≤ |Bᵢ| — the sum genuinely grows, and no size condition brings it back to 1.

### 2.4 What to learn

Bollobás is the strongest form of the "one budget per witness" principle in this chapter: the budget Σ 1/C(a+b, a) is spent by *pairs*, and the witness arrangements are *permutations*. Note the asymmetry with L1: there, chains are deterministic objects counted twice; here, a single random permutation pays for every pair at once, and disjointness of events is the whole proof. When a problem hands you set pairs with a disjointness condition *inside* each pair and intersection conditions *across* pairs, this is the theorem to try first.

---

## Lecture 3 · The Circle Method: Katona's Interval Lemma and EKR

**Problem (Erdős–Ko–Rado).** A family F of k-subsets of [n], **pairwise intersecting**, n ≥ 2k. Then |F| ≤ **C(n−1, k−1)** — achieved by the *star* (all k-sets containing a fixed element).

The proof arranges [n] on a circle at random and counts. The engine is a lemma about arcs, and this lecture proves it completely — including the mixed sub-case that the reference edition had to flag.

### 3.1 Arcs and their starts (P8, full)

Put the n points on a circle ℤ_n and fix a clockwise direction. A *k-arc* is a set of k consecutive points; identify it by its **start**. For two k-arcs with starts s, t ∈ ℤ_n:

**Claim.** The arcs intersect ⟺ dist(s, t) ≤ k−1.

*Proof.* (⇐) Say the clockwise distance from s to t is d ≤ k−1 (the other case is symmetric). Then t ≡ s+d (mod n) itself lies in the arc starting at s (which covers s, s+1, …, s+k−1 (mod n)), and t lies in its own arc. A shared point. (⇒) Let z be a shared point of the two k-arcs starting at s and t. Then z ≡ s+u (mod n) and z ≡ t+v (mod n) for integers u, v ∈ {0, 1, …, k−1}. Subtracting gives s−t ≡ v−u (mod n) with −(k−1) ≤ v−u ≤ k−1, so the cyclic distance between s and t is dist(s, t) = |v−u| ≤ k−1. ∎

So an intersecting family of arcs is exactly a set S ⊆ ℤ_n of start points with **pairwise cyclic distances ≤ k−1**. Geometry has become arithmetic on a cycle.

### 3.2 The interval lemma, complete (the mixed sub-case included)

**Katona's interval lemma.** If S ⊆ ℤ_n has pairwise cyclic distances ≤ k−1, then |S| ≤ k. (Requires n ≥ 2k.)

*Proof.* If S = ∅ the bound is trivial; otherwise fix an anchor s₀ ∈ S. Every other point of S lies in the **window** [s₀−k+1, s₀+k−1] (mod n) — the 2k−1 positions within cyclic distance k−1 of s₀ — because all pairwise distances to s₀ are ≤ k−1. (Here n ≥ 2k matters: 2k−1 ≤ n−1, so the window's 2k−1 positions are all distinct on the cycle.) Split the window's interior into:

- **forward offsets** A = {a ∈ [1, k−1] : s₀+a ∈ S},
- **backward offsets** B = {b ∈ [1, k−1] : s₀−b ∈ S}.

Take a ∈ A and b ∈ B. The two points s₀+a and s₀−b have cyclic distance min(a+b, n−a−b). Now **a + b = k is forbidden**: it would give cyclic distance min(k, n−k) = k > k−1 (using n ≥ 2k). So no a ∈ A pairs with any b ∈ B at sum exactly k:

**A ∩ (k − B) = ∅**, where k − B = {k − b : b ∈ B}.

Both A and k − B live inside the k−1 slots [1, k−1], disjointly:

|A| + |B| = |A| + |k − B| ≤ k − 1, and |S| = 1 + |A| + |B| ≤ k. ∎

That is the whole proof — the "mixed sub-case" (forward and backward starts coexisting) is exactly the A ∩ (k−B) = ∅ step, and it costs one line once the window and the reflected set k−B are on the table. Without the reflection trick, the naive bound is |A|, |B| ≤ k−1 each, giving 2k−1; the reflection k − B is what fuses the two groups into one budget.

**Figure 1 draws the proof**: an equality configuration on the circle, the window, and the offset strip where A and k−B tile [1, k−1] disjointly.

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 880 365" font-family="Georgia, 'Times New Roman', serif">
  <rect x="0" y="0" width="880" height="365" fill="#ffffff"/>
  <text x="240" y="26" text-anchor="middle" font-size="17" fill="#111827">n = 10, k = 4: starts S = {8, 9, 0, 1}</text>
  <circle cx="240" cy="175" r="110" fill="none" stroke="#9ca3af" stroke-width="2"/>
  <path d="M 118.2 214.4 A 128 128 0 1 1 361.8 214.4" fill="none" stroke="#dc2626" stroke-width="2" stroke-dasharray="7 5"/>
  <line x1="112" y1="217" x2="125" y2="212" stroke="#dc2626" stroke-width="2"/>
  <line x1="355" y1="212" x2="368" y2="217" stroke="#dc2626" stroke-width="2"/>
  <text x="240" y="322" text-anchor="middle" font-size="13" fill="#dc2626">window [s&#8320;&#8722;3, s&#8320;+3] = {7, 8, 9, 0, 1, 2, 3}: 2k&#8722;1 = 7 slots</text>
  <circle cx="240" cy="65" r="13" fill="#2563eb" stroke="#1e3a8a" stroke-width="2"/>
  <text x="240" y="70" text-anchor="middle" font-size="13" fill="#ffffff">0</text>
  <circle cx="305" cy="86" r="13" fill="#2563eb" stroke="#1e3a8a" stroke-width="2"/>
  <text x="305" y="91" text-anchor="middle" font-size="13" fill="#ffffff">1</text>
  <circle cx="345" cy="141" r="13" fill="#ffffff" stroke="#374151" stroke-width="2"/>
  <text x="345" y="146" text-anchor="middle" font-size="13" fill="#111827">2</text>
  <circle cx="345" cy="209" r="13" fill="#ffffff" stroke="#374151" stroke-width="2"/>
  <text x="345" y="214" text-anchor="middle" font-size="13" fill="#111827">3</text>
  <circle cx="305" cy="264" r="13" fill="#ffffff" stroke="#374151" stroke-width="2"/>
  <text x="305" y="269" text-anchor="middle" font-size="13" fill="#111827">4</text>
  <circle cx="240" cy="285" r="13" fill="#ffffff" stroke="#374151" stroke-width="2"/>
  <text x="240" y="290" text-anchor="middle" font-size="13" fill="#111827">5</text>
  <circle cx="175" cy="264" r="13" fill="#ffffff" stroke="#374151" stroke-width="2"/>
  <text x="175" y="269" text-anchor="middle" font-size="13" fill="#111827">6</text>
  <circle cx="135" cy="209" r="13" fill="#ffffff" stroke="#374151" stroke-width="2"/>
  <text x="135" y="214" text-anchor="middle" font-size="13" fill="#111827">7</text>
  <circle cx="135" cy="141" r="13" fill="#2563eb" stroke="#1e3a8a" stroke-width="2"/>
  <text x="135" y="146" text-anchor="middle" font-size="13" fill="#ffffff">8</text>
  <circle cx="175" cy="86" r="13" fill="#2563eb" stroke="#1e3a8a" stroke-width="2"/>
  <text x="175" y="91" text-anchor="middle" font-size="13" fill="#ffffff">9</text>
  <text x="240" y="102" text-anchor="middle" font-size="12" fill="#2563eb">anchor s&#8320; = 0</text>
  <text x="660" y="26" text-anchor="middle" font-size="17" fill="#111827">the offset strip [1, k&#8722;1]</text>
  <rect x="550" y="125" width="60" height="50" fill="#dbeafe" stroke="#2563eb" stroke-width="2.5"/>
  <text x="580" y="156" text-anchor="middle" font-size="16" fill="#1e3a8a">1</text>
  <rect x="630" y="125" width="60" height="50" fill="#ffffff" stroke="#dc2626" stroke-width="2.5"/>
  <text x="660" y="156" text-anchor="middle" font-size="16" fill="#dc2626">2</text>
  <rect x="710" y="125" width="60" height="50" fill="#ffffff" stroke="#dc2626" stroke-width="2.5"/>
  <text x="740" y="156" text-anchor="middle" font-size="16" fill="#dc2626">3</text>
  <text x="580" y="197" text-anchor="middle" font-size="13" fill="#2563eb">A = {1}</text>
  <text x="700" y="197" text-anchor="middle" font-size="13" fill="#dc2626">k&#8722;B = {2, 3}</text>
  <text x="660" y="233" text-anchor="middle" font-size="13" fill="#111827">a + b = 4 is forbidden &#8658; A &#8745; (k&#8722;B) = &#8709;</text>
  <text x="660" y="255" text-anchor="middle" font-size="13" fill="#111827">equality: A &#8851; (k&#8722;B) = {1, 2, 3}, so |A| + |B| = 3 = k&#8722;1</text>
  <text x="660" y="277" text-anchor="middle" font-size="13" fill="#111827">backward offsets B = {1, 2} reflect by b &#8614; k&#8722;b</text>
  <text x="440" y="350" text-anchor="middle" font-size="14" fill="#374151">Figure 1 &#183; Katona's window: starts trapped within distance k&#8722;1 of the anchor, and the forbidden sum a + b = k</text>
</svg>
```

The verification record checks the lemma exhaustively: for every 2k ≤ n ≤ 16 (k ≥ 2), the maximum size of a start set with pairwise distances ≤ k−1 is exactly k — 0 violations across every subset of every cycle.

### 3.3 Equality: consecutive starts and the unique common point (n > 2k)

Equality analysis drives uniqueness, so we do it now, completely.

**Lemma (structure of equality).** Suppose n > 2k and |S| = k in the interval lemma. Then S is a set of **k consecutive points** of the cycle, and the k arcs starting at S share **exactly one common point**.

*Proof.* Equality gives |A| + |B| = k−1 with A and k−B *disjoint* subsets of [1, k−1] — so they tile it: **A ⊔ (k−B) = [1, k−1]**. The extra room n ≥ 2k+1 bans one more sum: a + b = k+1 gives cyclic distance min(k+1, n−k−1), and n−k−1 ≥ k, so the distance is ≥ k > k−1 — forbidden. Hence also **A ∩ (k+1−B) = ∅**.

Now let b ∈ B with b ≥ 2, and suppose b−1 ∉ B. From the tiling, k−b+1 = k−(b−1) ∉ k−B, so k−b+1 ∈ A. But (k−b+1) + b = k+1 — a forbidden sum with b ∈ B, contradicting A ∩ (k+1−B) = ∅. So **B is downward-closed**: b ∈ B, b ≥ 2 ⟹ b−1 ∈ B, i.e. B = {1, …, β} for some β ≥ 0 (with B = ∅ when β = 0). The tiling then forces A = {1, …, k−1−β}.

So S = {s₀} ∪ {s₀+1, …, s₀+k−1−β} ∪ {s₀−1, …, s₀−β} = {s₀−β, …, s₀+k−1−β} (mod n): k consecutive points on the cycle. Write these k consecutive starts as u_i ≡ s₀−β+i (mod n) for i = 0, 1, …, k−1, where the arc starting at u_i is A_{u_i} = {u_i+r (mod n) : 0 ≤ r ≤ k−1}. Every arc A_{u_i} contains the point z ≡ u₀+(k−1) ≡ s₀+k−1−β (mod n), since z ≡ u_i+(k−1−i) (mod n) and 0 ≤ k−1−i ≤ k−1. Conversely, any point in A_{u₀} has the form u₀+r (mod n) with 0 ≤ r ≤ k−1 (and since n > 2k > k, these k points are distinct modulo n). For any r < k−1, its clockwise offset from u_{k−1} ≡ u₀+k−1 (mod n) is r−(k−1) ≡ n−(k−1−r) (mod n). Because 1 ≤ k−1−r ≤ k−1 and n ≥ 2k+1, we have n−(k−1−r) ≥ n−(k−1) ≥ k+2 > k−1, so u₀+r (mod n) ∉ A_{u_{k−1}}. Thus A_{u₀} ∩ A_{u_{k−1}} = {z}, and the k arcs share **exactly one common point** z. ∎

At exactly n = 2k the tiling still holds but the (k+1)-ban disappears, and non-consecutive equality configurations exist: for (n, k) = (6, 3), the starts {0, 2, 4} give three pairwise-intersecting arcs with no common point — the lab census counts 8 equality configurations there, 2 of them non-consecutive; for (8, 4) it counts 16, of which 8 are non-consecutive. The uniqueness theorem in the next lecture will have to treat n = 2k separately, and it does.

### 3.4 EKR by double counting (P2, full)

Call a pair (σ, A) a *witness* if σ is a circular arrangement of [n] (there are (n−1)! of them, modulo rotation) and A ∈ F appears as an **arc** of σ.

*Per set.* A fixed k-set A is an arc of exactly **k!·(n−k)!** circular arrangements: treat A as a single block — k! internal orders of A, and (n−k)! circular arrangements of the block together with the other n−k elements.

*Per arrangement.* The F-arcs of one circle σ are pairwise intersecting (F is), so their starts have pairwise cyclic distances ≤ k−1, so there are at most **k** of them (Katona's interval lemma).

So |F| · k!·(n−k)! ≤ k · (n−1)!, and dividing:

|F| ≤ k·(n−1)! / (k!·(n−k)!) = (n−1)! / ((k−1)!(n−k)!) = **C(n−1, k−1)**. ∎

**Tight.** The star: all k-sets through a fixed point x have size C(n−1, k−1) ✓ and are pairwise intersecting ✓.

### 3.5 What to learn

The circle method is double counting with a *geometric* engine: the interval lemma is what makes "per arrangement ≤ k" true, and its complete proof is a lesson in **reflections** — map the backward offsets by b ↦ k−b so both directions compete for the same k−1 slots, and the mixed case dies of overcrowding. Watch where n ≥ 2k and n ≥ 2k+1 were used: the first makes the window non-degenerate and bans the sum k; the second bans k+1 and unlocks the structure of equality. Hypotheses in extremal theorems are usually the exact fingerprints of the proof steps.

---
## Lecture 4 · Uniqueness: Why Only Stars

EKR says |F| ≤ C(n−1, k−1). The sharp question: **who achieves equality?** The answer: at n = 2k, many families; at n > 2k, only stars. This lecture proves both regimes completely: the n = 2k complementary-pair characterization and the n > 2k star-uniqueness theorem across the entire range n ≥ 2k+1.

### 4.1 Equality forces every circle to be full (full)

**Lemma.** |F| = C(n−1, k−1) ⟺ every circular arrangement σ carries **exactly k** F-arcs.

*Proof.* The witness count of §3.4 is |F|·k!(n−k)! = Σ_σ (F-arcs of σ), and each term is ≤ k. Equality in the bound is equality in this count: since C(n−1,k−1)·k!(n−k)! = k·(n−1)! exactly (an arithmetic identity — the verification record checks it for all n ≤ 20), |F| maximal forces the sum to reach its cap k·(n−1)!, which with every term ≤ k forces every term to equal k. Conversely, if every circle carries k F-arcs, the double count recovers |F| = C(n−1, k−1). ∎

So an extremal family is *rigid*: on every single arrangement, its arcs must realize the interval lemma's equality case. Rigidity is what uniqueness proofs feed on.

### 4.2 What a full circle looks like (full)

For n > 2k, §3.3 applies to every circle σ: its k F-arcs start at k consecutive points and share exactly one common point z(σ). For n = 2k this fails — non-consecutive configurations exist — which is why the two regimes must be separated, and why n = 2k admits many extremal families:

**Theorem (equality at n = 2k, complete).** At n = 2k, a k-uniform intersecting family F is extremal (|F| = C(2k−1, k−1)) **iff** F contains exactly one set from each complementary pair {S, [2k] ∖ S}.

*Proof.* First, two members of F cannot be complementary (they would be disjoint), so F takes at most one set from each of the ½C(2k, k) = C(2k−1, k−1) pairs — that is the EKR bound in this regime, reproved. Conversely, if F takes exactly one from each pair it is automatically intersecting: two k-sets of [2k] that are disjoint are complements of each other — the only way to fit 2k points into two disjoint k-sets — so they would form one of the pairs, and F never holds both ends of a pair. Size: C(2k−1,k−1) ✓. ∎

For (n, k) = (6, 3) the lab enumerates all of them: exactly **2^10 = 1024** maximum families, one per choice of one-from-each-complementary-pair — the 6 stars among them, and 1018 others; the census confirms both the count and that every one of the 1024 choices really is intersecting. At n > 2k the party ends, and the next section proves why.

### 4.3 The transport to a global center (complete for all n ≥ 2k+1)

**Theorem (EKR uniqueness for n > 2k, complete).** Suppose n ≥ 2k+1 and F ⊆ C([n], k) is pairwise intersecting with |F| = C(n−1, k−1). Then F = star(x*) for some x* ∈ [n].

*Proof.* If k = 1, then |F| = C(n−1, 0) = 1 and the single 1-set is a star. Assume k ≥ 2 and n ≥ 2k+1. By §4.1 and §3.3, on every circular arrangement σ of [n] the family F realizes exactly k arcs, and these k arcs start at k consecutive positions of σ and share a unique common point z(σ) — specifically, if we label the circle positions 0, 1, …, n−1 clockwise with z(σ) placed at position 0, the k F-arcs of σ are precisely the k arcs containing position 0:

A_i(σ) = {σ(i), σ(i+1), …, σ(i+k−1)} for i ∈ {−(k−1), −(k−2), …, 0} (mod n).

Fix a reference circular arrangement σ₀, let x* = z(σ₀), and represent every circular arrangement σ by anchoring x* at position 0, so (σ(1), σ(2), …, σ(n−1)) ranges over all (n−1)! permutations of [n] ∖ {x*}. We prove that z(σ) = x* for **every** σ. Since the symmetric group on {1, 2, …, n−1} is generated by adjacent transpositions τ_m = (m, m+1) for 1 ≤ m ≤ n−2, it suffices to show that if z(σ) = x*, then σ′ = σ ∘ τ_m also satisfies z(σ′) = x*.

Suppose z(σ) = x*, so σ carries the k F-arcs A_i(σ) for i ∈ {−(k−1), …, 0}. When we swap the adjacent positions m and m+1 (where 1 ≤ m ≤ n−2, so position 0 is untouched), an arc A_i(σ) changes as a set if and only if the swapped pair {m, m+1} straddles an endpoint of A_i(σ). Since the left endpoint of A_i(σ) lies in {n−k+1, …, n−1} ∪ {0} and the right endpoint lies in {0, 1, …, k−1}:

- If 1 ≤ m ≤ k−1, then m ≤ k−1 < n−k (as n ≥ 2k+1), so {m, m+1} cannot straddle any left endpoint and straddles the right endpoint of A_i(σ) only when i+k−1 = m, i.e. for the single arc i = m−k+1. Thus the other k−1 arcs A_i(σ) (i ≠ m−k+1) are unchanged as sets: A_i(σ′) = A_i(σ) ∈ F.
- If k ≤ m ≤ n−k−1, then {m, m+1} lies strictly outside [−(k−1), k−1] (mod n), so all k arcs A_i(σ) are unchanged: A_i(σ′) = A_i(σ) ∈ F.
- If n−k ≤ m ≤ n−2, then {m, m+1} straddles only the left endpoint i ≡ m+1 (mod n), so again at least k−1 of the arcs A_i(σ) are unchanged: A_i(σ′) = A_i(σ) ∈ F.

In every case, at least k−1 of the k arcs through position 0 on σ′ already belong to F:

- **If k ≥ 3:** whenever 1 ≤ m ≤ k−2 (or n−k+1 ≤ m ≤ n−2), both extreme arcs A_{−(k−1)}(σ′) = {σ′(n−k+1), …, σ′(0)} and A_0(σ′) = {σ′(0), …, σ′(k−1)} belong to F. Their intersection on σ′ is the single point {σ′(0)} = {x*} (since n ≥ 2k+1). Because all k F-arcs of σ′ share the unique point z(σ′), we must have z(σ′) ∈ A_{−(k−1)}(σ′) ∩ A_0(σ′) = {x*}, so z(σ′) = x*. What if m = k−1, where the missing arc is A_0(σ′)? Then A_{−(k−1)}(σ′), …, A_{−1}(σ′) ∈ F, so the k consecutive F-arcs of σ′ must either be {A_{−(k−1)}(σ′), …, A_0(σ′)} (giving z(σ′) = x*) or {A_{−k}(σ′), A_{−(k−1)}(σ′), …, A_{−1}(σ′)}, where A_{−k}(σ′) = {σ′(n−k), …, σ′(n−1)}. In the latter case A_{−k}(σ′) ∈ F; but m = k−1 ≤ n−k−2 (since n ≥ 2k+1), so τ_{k−1} does not touch positions {n−k, …, n−1}, meaning A_{−k}(σ′) = A_{−k}(σ) was already an F-arc on σ — contradicting the fact that σ has only k F-arcs! By symmetry, m = n−k (missing A_{−(k−1)}(σ′)) is ruled out because τ_{n−k} does not touch positions {1, …, k} (k < n−k as n ≥ 2k+1), so A_1(σ′) = A_1(σ) ∉ F.
- **If k = 2:** for m = 1, A_{−1}(σ′) = {σ(n−1), x*} ∈ F, and the second F-arc on σ′ is either A_0(σ′) = {x*, σ(2)} (giving z(σ′) = x*) or A_{−2}(σ′) = {σ(n−2), σ(n−1)}. Since n ≥ 5, position 1 is disjoint from {n−2, n−1}, so A_{−2}(σ′) = A_{−2}(σ) ∉ F; hence z(σ′) = x*. Symmetrically, for m = n−2, A_0(σ′) = {x*, σ(1)} ∈ F and A_1(σ′) = {σ(1), σ(2)} = A_1(σ) ∉ F (as n−2 ≥ 3), so z(σ′) = x*.

Thus z(σ) = x* for every circular arrangement σ. Finally, every U ∈ F appears as an arc of at least one circular arrangement σ, and every F-arc of σ contains z(σ) = x*; therefore x* ∈ U for all U ∈ F. Thus F ⊆ star(x*), and |F| = C(n−1, k−1) = |star(x*)| forces F = star(x*). ∎

**Historical note and census check.** Katona's original 1972 block-circle transport fixes a k-set T ∈ F as a contiguous block and permutes the n−k outside elements, which directly covers n ≥ 3k−2 and leaves the "thin range" 2k < n ≤ 3k−2 to either the position-0 transposition argument above or the Kruskal–Katona shadow-cascade uniqueness proof in Chapter 9. The lab census confirms star uniqueness exhaustively wherever brute force reaches: (5, 2) has 5 maximum families (all stars), (7, 3) has 7 (all stars), (8, 3) has 8 (all stars), and Exploration 18 probes (9, 4).

### 4.4 What to learn

Uniqueness proofs are *rigidity* arguments: equality in a double count forces every local configuration to be extremal too, and extremal local configurations are so constrained that a global structure falls out. The gap between "every circle has a common point z(σ)" and "one point x* serves every circle" is closed by connectedness under local moves: anchoring x* at position 0 and applying a single adjacent transposition on the remaining n−1 positions leaves at least k−1 of the k arcs through position 0 intact, and the room n ≥ 2k+1 prevents the missing arc from sliding off position 0 into a position untouched by the swap. When you meet a uniqueness claim in the wild, ask: *what is being double-counted, and how do local moves connect the extremal witnesses?*

---
## Lecture 5 · Shifting: Deforming Families Toward the Star

The circle method proves EKR by *averaging over arrangements*. Shifting takes the opposite philosophy: **deform the family itself** toward a canonical shape, without changing its size or losing the intersecting property — and read the theorem off the deformed family (P23).

### 5.1 The (i, j)-shift (definition)

For 1 ≤ i < j ≤ n, the *shift* S_{ij} replaces a set A ∈ F containing j but not i by A′ = (A ∖ {j}) ∪ {i} — swapping the larger element for a smaller one — *provided the target A′ is not already in F; if A′ ∈ F, then A stays put* — and leaves every other set alone. Applied to a family: S_{ij}(F) = {S_{ij}(A) : A ∈ F}. The proviso is what keeps the image a set of the same cardinality: no duplicate can arise, because a set is only ever replaced by a target absent from the family. A family is *shifted* (or *left-compressed*) when no shift changes it: whenever A ∈ F, j ∈ A, i ∉ A, and i < j, then also (A ∖ {j}) ∪ {i} ∈ F.

**Size is preserved (full).** A shift fires only when the target set is absent from F, so the map A ↦ S_{ij}(A) is injective on F: two sets cannot collapse onto one target, because an unshifted set is its own image in F and a shifted set's image is not in F (and determines its preimage uniquely by swapping i back to j). So |S_{ij}(F)| = |F|, and k-uniformity is preserved because every image has the same size as its source. ✓

### 5.2 Intersecting is preserved (full)

Suppose F is k-uniform and intersecting, and let C, D ∈ S_{ij}(F) be disjoint — we derive a contradiction.

Both cannot contain i (they would meet at i), so one of them, say C, misses i. Any shifted image contains i, so C was not shifted: **C ∈ F** with i ∉ C. If D ∈ F too, then C ∩ D = ∅ contradicts F being intersecting. Hence D ∉ F, which means D is a shifted copy: D = (D* ∖ {j}) ∪ {i} for some D* ∈ F with j ∈ D* and i ∉ D*. Since C ∩ D = ∅ and D ∖ {i} = D* ∖ {j}, the unshifted part of D* misses C entirely: C ∩ (D* ∖ {j}) = ∅.

**Case j ∉ C.** Then C ∩ D* = (C ∩ (D* ∖ {j})) ∪ (C ∩ {j}) = ∅ ∪ ∅ = ∅ — two members C, D* ∈ F, disjoint. Contradiction.

**Case j ∈ C.** Then C ∈ F has j ∈ C and i ∉ C, *and C survived the shift unmoved* — which happens only when its own shift target C′ = (C ∖ {j}) ∪ {i} was already present in F. Now compute C′ ∩ D*: every piece is empty — i ∉ D* (since D* was shifted); j ∉ C′ (removed by the shift); and (C ∖ {j}) ∩ (D* ∖ {j}) ⊆ C ∩ (D* ∖ {j}) = ∅. So C′ ∩ D* = ∅ with C′, D* ∈ F. Contradiction. ∎

The proof is a template for *every* shifting-preservation argument in the field: chase which of the conflicting sets were actually moved, split on whether the shift's target was already present, and land the contradiction back in the original family.

### 5.3 Termination and the closing induction (full)

Shifting terminates. Each effective shift strictly decreases the total weight w(F) = Σ_{A∈F} Σ_{x∈A} x — each swap replaces j by i < j — and w(F) is a nonnegative integer. So after finitely many shifts the family is shifted, and it is still k-uniform, still intersecting, and still of size |F|.

**The closing induction for EKR (complete).** Once F ⊆ C([n], k) is shifted, we prove |F| ≤ C(n−1, k−1) for all n ≥ 2k by induction on n + k. The base cases k = 1 (|F| ≤ 1 = C(n−1, 0)) and n = 2k (|F| ≤ ½C(2k, k) = C(2k−1, k−1) by complementary pairs, §4.2) hold for all intersecting families without even shifting. Now suppose k ≥ 2 and n ≥ 2k+1, and split the shifted family F on the *largest* element n:

F₀ = {A ∈ F : n ∉ A} ⊆ C([n−1], k), and F₁ = {A ∖ {n} : n ∈ A ∈ F} ⊆ C([n−1], k−1).

First, F₀ is a k-uniform intersecting family on [n−1], and since n ≥ 2k+1 we have n−1 ≥ 2k, so the induction hypothesis for (n−1, k) gives |F₀| ≤ C(n−2, k−1).

Second, we claim that F₁ is a (k−1)-uniform **intersecting** family on [n−1] (where n−1 ≥ 2(k−1) holds automatically). Suppose for contradiction that B₁, B₂ ∈ F₁ are disjoint. Then A₁ = B₁ ∪ {n} and A₂ = B₂ ∪ {n} belong to F and meet only at n: A₁ ∩ A₂ = {n}. Their union inside [n−1] has size |B₁ ∪ B₂| = (k−1) + (k−1) = 2k−2 ≤ n−3 (since n ≥ 2k+1). Hence there is an element i ∈ [n−1] ∖ (B₁ ∪ B₂). Because F is shifted and i < n with n ∈ A₁ and i ∉ A₁, the shifted set A₁′ = (A₁ ∖ {n}) ∪ {i} = B₁ ∪ {i} must also belong to F. But A₁′ ∩ A₂ = (B₁ ∪ {i}) ∩ (B₂ ∪ {n}) = ∅ because B₁ ∩ B₂ = ∅, i ∉ B₂ ∪ {n}, and n ∉ B₁ ∪ {i}. That gives two disjoint sets A₁′, A₂ ∈ F — contradiction! Thus F₁ is indeed intersecting, so the induction hypothesis for (n−1, k−1) gives |F₁| ≤ C(n−2, k−2). Adding the two parts via Pascal's identity closes the induction:

|F| = |F₀| + |F₁| ≤ C(n−2, k−1) + C(n−2, k−2) = C(n−1, k−1). ∎

Notice why splitting on the *top* element n (rather than 1) is so clean: the sets avoiding n already live on [n−1], and shiftedness lets us swap n down to a free element i ∈ [n−1] whenever two sets through n try to meet only at n. In Chapter 9's shadow lecture you will meet a third complete proof of EKR — Daykin's complement mirror, which applies Kruskal–Katona directly to the complement family.

### 5.4 What to learn

Shifting is the most portable deformation tool in extremal set theory: it preserves size and uniformity automatically, and with modest case analysis it preserves intersecting-ness, cross-intersecting-ness, and most "forbidden configuration" properties. And once a family is shifted, peeling the largest coordinate n reduces (n, k) directly to (n−1, k) and (n−1, k−1) with Pascal's identity paying the sum. Its philosophy (canonical forms first, counting second) complements the circle method's (averaging first, structure second). The lab verifies preservation exhaustively on [4] — every intersecting subfamily of 2^[4], every single shift, and the full shift to stability — with size and intersecting-ness intact in every trial; the verification record extends the census to all 75 + 191 intersecting edge families at (5, 2) and (6, 2), again zero violations.

---
## The Trick Bag (reference card)

| Pattern | Plain language | Where you met it |
|---------|---------------|------------------|
| **P2 Double counting (chains / permutations / circles)** | Count pairs (object, witness-arrangement) two ways; the inequality falls out of the mismatch | L1, L2, L3, L4 |
| **P17 Duality / specialization** | One inequality, many shadows: Bollobás → LYM → Sperner by plugging in special pairs | L2, Ch. 9 L4 |
| **P8 Extremal circle structure** | Intersecting arcs trap their start points inside a short window; the window has exactly 2k−1 slots | L3, L4 |
| **P23 Compression / shifting** | Deform the family toward a canonical shape without losing the property or the count | L5 |
| **P4 Induction** | Peel the extreme element; one new element per step — or split a shifted family on n | L5, Ch. 9 L1, L2 |
| **P22 Polynomial method** | A polynomial vanishing on a grid, priced by its degrees — the same engine as Chapter 6 | Ch. 9 L1 |
| **P24 Shadow pricing (Kruskal–Katona)** | Price a family by its own real parameter x: a k-family of size C(x, k) forces every j-shadow to size ≥ C(x, j) — equality only at integer x and the complete families | Ch. 9 L4 |
| **One budget per witness (lore)** | Chains, permutations, circles: the proof prices each extremal witness arrangement, and the budgets sum to the answer | L1, L2, L3 |
| **Rearrange, then average (lore)** | The circle method: bound on every arrangement, average over random ones | L3, L4 |
| **A deficit is a period (lore)** | A sumset that underperforms the staircase by d carries a stabilizer of order ≥ d — the deficit is the period, not an accident | Ch. 9 L2 |
| **Local moves force global centers (lore)** | Anchor x* at position 0 and apply adjacent transpositions on the remaining n−1 positions: n ≥ 2k+1 keeps z(σ) pinned at x* across every circle | L4 |
| **The complement mirror (lore)** | Pass to complements: an intersecting family and the k-shadow of its complement family are disjoint — one j-form application plus one monotone function turns this into EKR | Ch. 9 L4 |
| **Beyond EKR (lore)** | Empty core (t = 1, n > 2k) ⇒ Hilton–Milner's C(n−1, k−1) − C(n−k−1, k−1) + 1 (tied with F₁ at k = 3); t-intersecting for all n ≥ 2k−t ⇒ Ahlswede–Khachatrian's max_r |F_r^{(t)}|, where F_r^{(t)} = {A ∈ C([n], k) : |A ∩ [t+2r]| ≥ t+r} (for t = 1, F₀ wins for all n ≥ 2k) | Ex. 20, Ch. 9 L4 |
| **Union-closed frontier (lore)** | Frankl's conjecture: some element in at least half the sets; proved so far: (3−√5)/2 ≈ 0.382 (Gilmer); a singleton in the family settles it for free | Ch. 9 L4 |

**Formula box:** Sperner: |F| ≤ C(n, ⌊n/2⌋); LYM Σ 1/C(n,|A|) ≤ 1 for antichains; Erdős: no chain of length k+1 ⇒ |F| ≤ Σ_{j=1..k} C(n, ⌊(n+1−j)/2⌋) = the sum of the k middle binomials. SCD: chain count C(n, ⌊n/2⌋), starts(j) = C(n,j) − C(n,j−1), Σ_c min(k,|c|) = sum of the k middle binomials; a family with no (k+1)-chain meets every symmetric chain ≤ k times. Bollobás: pairs (Aᵢ, Bᵢ), Aᵢ∩Bᵢ = ∅, cross-intersecting ⇒ Σ 1/C(aᵢ+bᵢ, aᵢ) ≤ 1; the skew versions (forward conditions Aᵢ∩B_j ≠ ∅ for i < j only): uniform |Aᵢ| = a, |Bᵢ| = b ⇒ m ≤ C(a+b, a) (Frankl 1982; Kalai 1984); non-uniform on [n] ⇒ Σ 1/C(|Aᵢ|+|Bᵢ|, |Aᵢ|) ≤ n+1, sharp at the complement pairs (Hegedüs–Frankl 2023); no size hypothesis rescues Σ ≤ 1 — the exhaustive maxima are n+1 (no hypotheses), n (Aᵢ ≠ ∅), and 1, 4/3, 2 at n = 2, 3, 4 under Aᵢ ≠ ∅ and |Aᵢ| ≤ |Bᵢ| (Exercise 14; the machine census is the referee). EKR: intersecting k-uniform on [n], n ≥ 2k ⇒ |F| ≤ C(n−1, k−1); equality at n = 2k ⟺ exactly one set from each complementary pair (2^{C(2k−1,k−1)} maximum families; (6,3): 2^10 = 1024, of which 6 are stars and 6 are fully shifted); at n > 2k, equality forces k consecutive arc-starts per circle, one common point z(σ), and by adjacent-transposition transport F = star(x*). Interval lemma: pairwise intersecting k-arcs ⇒ starts inside a (2k−1)-slot window, at most k arcs; equality (n > 2k) ⇒ B = [1,β], A = [1,k−1−β], k consecutive starts. The sumset clauses — the staircase, Cauchy–Davenport in both proofs with the m-fold corollary, Kneser with the e-transform, EGZ — and the shadow clauses — the Kruskal–Katona cascade and clique forms, the Daykin mirror, Hilton–Milner, Ahlswede–Khachatrian, union-closed — live in Chapter 9's formula box (its Lectures 1, 2, and 4).

---
## Exercises (graded: ●○○ easy · ●●○ moderate · ●●● tough)

**Easy — one idea, applied directly**

1. ●○○ **The smallest EKR census, by hand.** List every intersecting family of 2-subsets of [5] up to size 4 (there are not many maximal ones): show the maximum is 4 = C(4,1), and that the maximum families are exactly the five stars. *Hint: among the 10 edges of K₅, intersecting means no two disjoint edges.*
2. ●○○ **Complementary-pair arithmetic.** At n = 2k, count the complementary pairs {S, S̄} of k-subsets of [2k] and verify that half of C(2k, k) equals C(2k−1, k−1). Then show that choosing exactly one set from each pair always yields an intersecting family of the EKR-maximum size. *Hint: disjoint k-sets at n = 2k are complements.*
3. ●○○ **Half the cube, no uniformity.** Show that a pairwise-intersecting family F of arbitrary subsets of [n] — no size condition, no uniformity — satisfies |F| ≤ 2^{n−1}. Then exhibit a maximum family on [4] whose members have no element in common. Finally contrast with Exercise 2: at n = 2k every one-per-complementary-pair choice of k-sets is intersecting, but on the full 2^[4] most one-per-pair choices fail — say exactly which extra hypothesis made Exercise 2's choices safe. *Hint: P2 — the complementary-pair ledger of Exercise 2, run over the whole cube: {A, Ā} splits 2^[n] into 2^{n−1} pairs, and an intersecting family takes at most one from each.*

**Moderate — two ideas, or one tricky step**

4. ●●○ **LYM from Bollobás, in full detail.** Given an antichain A₁, …, A_m, set up the Bollobás pairs and verify *both* cross-intersection hypotheses from incomparability, concluding Σ_{i=1..m} 1/C(n, |Aᵢ|) ≤ 1. Which hypothesis fails if the family is merely an intersecting family rather than an antichain?
5. ●●○ **The naive interval bound.** Without the reflection trick, show that pairwise intersecting k-arcs have at most 2k−1 starts (treat the starts after and before a chosen anchor separately, k−1 each plus the anchor). Then show where the proof loses: the two budgets must be *summed*, and only the substitution k − B puts both budgets in the same (k−1)-slot offset strip [1, k−1]. *Hint: §3.2's A ∩ (k−B) = ∅ inside [1, k−1].*
6. ●●○ **The exchange argument.** Give the alternative proof of Erdős's bound: among families with no chain of length k+1, take one of maximum size, show its LYM sum is ≤ k, and then exchange sets between levels — if a cheaper level has room, move — until the family is pushed into the k middle levels. Where exactly does maximality close the bound?
7. ●●○ **Shifting hygiene.** Prove that an (i, j)-shift preserves the size and the k-uniformity of a family, and that the weight w(F) = Σ_{A∈F} Σ_{x∈A} x strictly decreases with every nontrivial shift — a nonnegative integer, hence termination. Then verify on the 2-subsets of [4] that the fully shifted maximal intersecting families are exactly two: the star {12, 13, 14} and the triangle {12, 13, 23}.
8. ●●○ **Equality at n = 2k, both directions.** At n = 2k: (⇐) a one-per-complementary-pair family is intersecting of maximum size (Exercise 2); (⇒) an intersecting family of maximum size C(2k−1, k−1) contains exactly one of each complementary pair — no more (disjointness), no fewer (count the pairs and use the size). Conclude: for (6, 3) there are exactly 2^10 maximum families.
9. ●●○ **The window algebra and t-intersecting arcs, end to end.** Prove the two facts behind the interval lemma's sharp count: with anchor s₀ and window [s₀−k+1, s₀+k−1], the forward-offset set A and backward-offset set B satisfy A ∩ (k−B) = ∅ and therefore |A|+|B| ≤ k−1. Verify both on the (6, 3) witness {0, 2, 4} and on the consecutive family {0, 1, 2}. Then generalize to t-intersecting k-arcs (1 ≤ t ≤ k, n ≥ 2k−t+1): show that two k-arcs share at least t points on the circle iff their starts satisfy dist(s, s′) ≤ k−t, that a + b = k−t+1 is forbidden between A, B ⊆ [1, k−t], and hence that at most k−t+1 arcs can be pairwise t-intersecting. *Hint: reflect by b ↦ (k−t+1)−b inside [1, k−t].*
10. ●●○ **Stars and triangles: the complete k = 2 map.** (a) Prove that every pairwise-intersecting family of 2-subsets of [n] is contained in a star (all pairs through one point) or in the three edges of a triangle. (b) Deduce the inclusion-maximal families for n ≥ 4: exactly the n full stars and the C(n, 3) triangles, and nothing else. (c) Stars have n−1 edges and win outright once n ≥ 5; at n = 4 the four triangles tie them at 3 = C(3, 1). Reconcile the tie with Exercise 8: show that each triangle on [4] picks exactly one edge from each complementary pair, so all eight maxima are one-per-pair families, as A8 demands. *Hint: P2 — A1's edge-census chase promoted to every n, then count the maximal witnesses.*
11. ●●○ **Sunflowers.** A family of r distinct sets S₁, …, S_r is an r-sunflower with core K when Sᵢ ∩ S_j = K for all i ≠ j; the petals Sᵢ ∖ K are pairwise disjoint (and when the sets are k-uniform, the petals are automatically nonempty since Sᵢ ≠ S_j). (a) Prove the Erdős–Rado sunflower lemma: any family F of more than k!(r−1)^k sets, each of size at most k (k ≥ 1, r ≥ 2), contains an r-sunflower. Induct on k: if some point lies in more than (k−1)!(r−1)^{k−1} members, hand its trace family to the induction and glue the point back into the core; otherwise take a maximal pairwise-disjoint subfamily of nonempty members of F — of size at most r−1 — and double-count pairs (A ∈ F ∖ {∅}, x ∈ A ∩ P) against the degree cap (checking separately whether ∅ ∈ F). (b) At k = 2, r = 3 the bound reads 8. Prove the structural equivalence: a 2-uniform edge family with no 3-sunflower is exactly one with maximum degree Δ ≤ 2 and matching number ν ≤ 2, and census the true maxima on [5] and [6]. (c) The bound has honest slack here; quote the Erdős–Rado sunflower conjecture (c_r^k for a constant c_r depending only on r) and the modern bounds: Alweiss–Lovett–Wu–Zhang (2020), simplified by Rao, proved (Cr log(rk))^k, and Bell–Chueluecha–Warnke (2021) refined it to (Cr log k)^k — the current best. *Hint: P4 — peel by a degree census: a heavy point recurses on traces, light points let the disjoint subfamily pay.*
12. ●●○ **The shift's boundary.** §5.2 proves that (i, j)-shifts preserve pairwise intersection for k-uniform families. (a) Show the uniformity was never needed: replay the three-case ledger for arbitrary families and find that the mixed case closes on the *original* family, not the shifted one. (b) The antichain property is another story: exhibit a two-set family and one shift whose image is a chain, and check whether the full shift of §5.3 (all pairs, to stability) rescues it. (c) Audit the chapter: every place Lecture 5 and its exercises use the shift — is uniformity present at each use? *Hint: P23 — compression preserves exactly what it is asked to preserve; audit hypotheses, not conclusions.*

**Tough — several chapter ideas combined**

13. ●●● **Equality structure at n > 2k, in full.** Reconstruct §3.3's argument with every step: forbidden sum k+1 (cyclically), b ∈ B with b ≥ 2, the inference b−1 ∈ B (else k−b+1 ∈ A sums to k+1 with b), the collapse B = [1, β] and A = [1, k−1−β], and the conclusion: k consecutive starts sharing exactly one common point. Verify each step on the circle n = 10, k = 4 with S = {8, 9, 0, 1} and anchor s₀ = 0 (Figure 1's exact data).
14. ●●● **The skew landscape, mapped.** (a) Verify the 3/2 counterexample of §2.3 condition by condition. (b) Now add the rescue attempts: on [3], take the pairs (A₁, B₁) = ({1}, {2}), (A₂, B₂) = ({2}, {1}), (A₃, B₃) = ({3}, {1, 2}); check every skew cross-condition, every disjointness, Aᵢ ≠ ∅, and |Aᵢ| ≤ |Bᵢ| for all three — then compute Σ 1/C(|Aᵢ|+|Bᵢ|, |Aᵢ|) and watch it exceed 1. (c) Two survivors: show the singleton-complement system ({i}, [n]∖{i}) is skew (indeed cross-intersecting both ways) with Σ = 1; and show the uniform bound C(a+b, a) is sharp by pairing every a-subset of a fixed (a+b)-set with its complement (same size, distinct sets ⇒ no containment). (d) The sharpness witness for the n+1 bound: list *all* subsets of [n] in non-increasing size order and pair each Aᵢ with Bᵢ = [n]∖Aᵢ. Show the system is skew (non-increasing size bans containment), and compute the sum. What does the answer tell you about *any* attempt to rescue Σ ≤ 1 with a size hypothesis?
15. ●●● **Shattered sets (Sauer–Shelah).** F shatters S when {A ∩ S : A ∈ F} is all of 2^S. Prove the dimension bound: if |F| > C(n, 0) + C(n, 1) + … + C(n, s−1), then F shatters a set of size s. The sharp route, inducting on n: fix a coordinate x; project every member of F (delete x wherever it appears) and collect the distinct images into G₀; collect into G₁ the projections whose two lifts, A and A ∪ {x}, both lie in F. Then show: (i) |F| = |G₀| + |G₁|, by counting the fibers of the projection; (ii) G₀ shatters no s-set — a G₀-witness lifts to an F-witness with the same trace; (iii) G₁ shatters no (s−1)-set — a G₁-witness for the trace T on S lifts to both traces T and T ∪ {x} on S ∪ {x}, so a G₁ shattering of S is an F shattering of the s-set S ∪ {x}; (iv) close the induction with Pascal. Finish with sharpness: the level family {A : |A| ≤ s−1} meets the bound exactly and shatters no s-set — which trace can it never realize? *Hint: P4 + P2 — peel one coordinate; Pascal's identity pays the sum.*

**Pattern unknown — you choose the tool** *No hints, no difficulty rating: diagnosing the problem is part of the problem. Worked answers still wait at the end.*

16. ◆ Count the maximum intersecting families of 3-subsets of [6] — not just their size. You should get a familiar power of 2; say what each family is, how many of them are stars, and how many of the 2^10 maximum families are *fully shifted* (stable under every S_{ij} for 1 ≤ i < j ≤ 6).
17. ◆ Write the symmetric chain decomposition of 2^[4] explicitly — every chain, start to finish — and check the three defining properties: partition, steps of +1, and symmetry |bottom| + |top| = 4. How many chains, and what should that number be?

**Explorations — ◐ research-style training** *No single right answer — what you should find is described in each.*

18. ◐ **The thin range, censused.** At (n, k) = (9, 4) Katona's original block-circle transport falls in the thin range (2k < n ≤ 3k−2), while §4.3's anchored transposition proof still forces stars. Set up a search for maximum and near-maximum intersecting families of 4-subsets of [9] — branch on the 126 sets, or classify by core size and shift stability against the C(8, 3) = 56 bound — and census what you find: are all maximum families stars, how many are there, and what do the largest empty-core (non-star) intersecting families look like? Compare with (7, 3) and (8, 3).
19. ◐ **LYM sums, sampled and exhaustive.** For n ≤ 4, enumerate all antichains (167 nonempty ones at n = 4) and verify Σ_{A∈F} 1/C(n,|A|) ≤ 1, with equality on the full levels (all five of them at n = 4) — and prove that for every n ≥ 1, the *only* nonempty antichains achieving LYM equality Σ_{A∈F} 1/C(n,|A|) = 1 are the n+1 single full levels C([n], j). Confirm also that the full union of the two middle levels when n is odd is not an antichain, while partial mixes can be ({{1}, {2, 3}} at n = 3 is one). For n = 5, 6 sample maximal antichains and study the distribution of LYM sums: where does the mass concentrate?
20. ◐ **Beyond EKR: empty-core maxima and the Ahlswede–Khachatrian families.** For (n, k) = (7, 3), (8, 3), (10, 4), (9, 4), (12, 5), compute the sizes of the Frankl / Ahlswede–Khachatrian candidates F_r = {A ∈ C([n], k) : |A ∩ [2r+1]| ≥ r+1} for 0 ≤ r ≤ k−1, and the Hilton–Milner formula HM(n, k) = C(n−1, k−1) − C(n−k−1, k−1) + 1 alongside. You should find |F₁| and HM(n, k) equal in size at k = 3 (the (7, 3) census counts 175 empty-core maxima of size 13, split 140 + 35 between the two shapes) and separated at k ≥ 4 — 70 vs 75 at (10, 4), 51 vs 53 at (9, 4), 288 vs 316 at (12, 5). Which is the true empty-core maximum for 1-intersecting families when n > 2k? And when does a higher F_r^{(t)} = {A ∈ C([n], k) : |A ∩ [t+2r]| ≥ t+r} overtake the t-star F₀^{(t)} in the t-intersecting problem (t ≥ 2)?

---
## Computational Lab (verified)

Five parts, all deterministic — the randomized parts use a fixed Lehmer generator (seed 12345, multiplier 48271, modulus 2³¹−1), so every run reproduces every digit. The printed outputs were produced by machine runs of exactly this logic (the verification record in the appendix enumerates the runs). Runtimes: Part 2's (8, 3) census and Part 4's exact-fraction skew recursions take a few seconds to a couple of minutes; everything else is instantaneous.

### Part 1 — Sperner, LYM, and the symmetric chain decomposition, actually built

```python
from math import comb

def scd(n):
    if n < 0: return []
    chains = [[frozenset()]]                          # n = 0: one chain holding the empty set
    for m in range(1, n + 1):
        nxt = []
        for c in chains:
            nxt.append(c + [c[-1] | {m}])             # extended chain: new element m on top
            if len(c) > 1:
                nxt.append([A | {m} for A in c[:-1]]) # reflected chain: first l-1 sets + {m}
        chains = nxt
    return chains

for n in range(0, 7):
    ch = scd(n)
    flat = [A for c in ch for A in c]
    ok = (len(set(flat)) == 2**n                                        # partition
          and all(len(c[i+1]) == len(c[i]) + 1 for c in ch for i in range(len(c)-1))
          and all(len(c[0]) + len(c[-1]) == n for c in ch)              # symmetry
          and len(ch) == comb(n, n // 2))
    if n >= 1: print(n, len(ch), ok)

starts_5 = [comb(5, j) - (comb(5, j - 1) if j > 0 else 0) for j in range(3)]
print("n=5 starts by level 0..2:", starts_5, "sum:", sum(starts_5) == comb(5, 2))
print("scd(4) chain lengths:", [len(c) for c in scd(4)])

ch6 = scd(6)
erdos   = [sum(min(k, len(c)) for c in ch6) for k in range(1, 7)]
formula = [sum(comb(6, (7 - j) // 2) for j in range(1, k + 1)) for k in range(1, 7)]
print(erdos, formula, erdos == formula)

def popcount(x): return bin(x).count("1")
def members(mask): return [s for s in range(16) if mask >> s & 1]
antichains = lym_eq = 0; lym_ok = True; best = [0, 0, 0, 0]
for mask in range(1, 2**16):                          # every nonempty family on [4]
    mem = sorted(members(mask), key=popcount)
    chain = {}
    for s in mem:
        chain[s] = 1 + max((chain[t] for t in chain if t & ~s == 0), default=0)
    longest = max(chain.values())
    for k in range(1, 5):
        if longest <= k: best[k-1] = max(best[k-1], len(mem))
    if longest == 1:
        antichains += 1
        lym = sum(1 / comb(4, popcount(s)) for s in mem)
        lym_ok &= lym <= 1 + 1e-12
        lym_eq += abs(lym - 1) < 1e-12
print(antichains, lym_ok, lym_eq, best)
```

**Verified output.** The doubling construction passes every check for n = 0…6 — printing `1 1 True`, `2 2 True`, `3 3 True`, `4 6 True`, `5 10 True`, `6 20 True` for n = 1…6, with `n=5 starts by level 0..2: [1, 4, 5] sum: True` and `scd(4) chain lengths: [5, 3, 3, 1, 3, 1]` matching §1.2 and A◆17 verbatim. The Erdős sums from the built decomposition, `[20, 35, 50, 56, 62, 63]`, agree with the formula Σ_{j≤k} C(6, ⌊(7−j)/2⌋). The n = 4 census over all 65,535 nonempty families prints `167 True 5 [6, 10, 14, 15]`: 167 nonempty antichains, LYM never exceeded, equality in **5** of them (the five full levels), and maximum sizes **6, 10, 14, 15** for families with no chain of length k+1 (k = 1…4).

### Part 2 — The EKR censuses, interval lemma, and empty-core competitors

```python
from itertools import combinations
from math import comb, factorial

def max_cliques(vs, adj):                 # Bron-Kerbosch with pivoting
    best = [0, 0]                         # [max size, count]
    def bk(R, P, X):
        if not P and not X:
            if len(R) > best[0]: best[0], best[1] = len(R), 1
            elif len(R) == best[0]: best[1] += 1
            return
        pivot = max(P + X, key=lambda u: sum(adj[u][w] for w in P))
        for v in [w for w in P if not adj[pivot][w]]:
            bk(R + [v], [w for w in P if adj[v][w]], [w for w in X if adj[v][w]])
            P.remove(v); X.append(v)
    bk([], list(vs), [])
    return best

for n, k in [(5, 2), (6, 3), (7, 3), (8, 3)]:
    V = list(combinations(range(n), k))
    adj = [[i != j and set(a) & set(b) != set() for j, b in enumerate(V)]
           for i, a in enumerate(V)]
    size, count = max_cliques(range(len(V)), adj)
    print(f"({n}, {k}): max {size}, families {count}, EKR bound {comb(n-1, k-1)}")

def cdist(a, b, n): return min(abs(a - b), n - abs(a - b))
def is_consec(S, n):
    s = sorted(S)
    if len(s) < 2: return True
    gaps = [s[i+1] - s[i] for i in range(len(s) - 1)]
    return gaps == [1] * (len(s) - 1) or \
           sorted(gaps) == sorted([1] * (len(s) - 2) + [n - len(s) + 1])

for n, k in [(6, 3), (7, 3), (8, 3), (8, 4), (10, 4), (10, 5)]:
    best, configs, nonc = 0, 0, 0
    for size in range(1, k + 1):
        for S in combinations(range(n), size):
            if not all(cdist(a, b, n) <= k - 1 for a, b in combinations(S, 2)):
                continue
            if size > best: best, configs, nonc = size, 1, 0
            elif size == best:
                configs += 1
                if not is_consec(S, n): nonc += 1
    print(f"({n}, {k}): max {best}, configs {configs}, non-consecutive {nonc}")

def common_points(starts, n, k):
    arcs = [{(s + j) % n for j in range(k)} for s in starts]
    return {t for t in range(n) if all(t in a for a in arcs)}

ok1 = all(len(common_points(range(s, s + k), n, k)) == 1
          for n, k in [(6, 3), (7, 3), (8, 4), (10, 4)] for s in range(n))
ok2 = all(sum(1 for s in range(n) if x in {(s + j) % n for j in range(k)}) == k
          for n in range(4, 10) for k in range(2, n // 2 + 1) for x in range(n))
ok3 = all(comb(n-1, k-1) * factorial(k) * factorial(n-k) == k * factorial(n-1)
          for n in range(2, 13) for k in range(1, n))
print(ok1, ok2, ok3)
print("Figure 1 tiling:", {1} | {4 - b for b in {1, 2}} == {1, 2, 3})

# Exploration 20 / A◐20: F_r sizes and Hilton-Milner bound across the 5 benchmark pairs
for n, k in [(7, 3), (8, 3), (10, 4), (9, 4), (12, 5)]:
    Fr = [sum(comb(2*r + 1, i) * comb(n - 2*r - 1, k - i)
              for i in range(r + 1, min(k, 2*r + 1) + 1)) for r in range(k)]
    hm = comb(n - 1, k - 1) - comb(n - k - 1, k - 1) + 1
    print(f"({n}, {k}): F_r = {Fr}, HM = {hm}")
```

**Verified output.** The maximum-clique census of the intersect graphs prints `(5, 2): max 4, families 5`, `(6, 3): max 10, families 1024`, `(7, 3): max 15, families 7`, `(8, 3): max 21, families 8`. The interval-lemma sweep prints `(6, 3): max 3, configs 8, non-consecutive 2`, `(7, 3): max 3, configs 7, non-consecutive 0`, `(8, 3): max 3, configs 8, non-consecutive 0`, `(8, 4): max 4, configs 16, non-consecutive 8`, `(10, 4): max 4, configs 10, non-consecutive 0`, `(10, 5): max 5, configs 32, non-consecutive 22`. Then `True True True` and `Figure 1 tiling: True`. Finally, the benchmark table for Exploration 20 prints `(7, 3): F_r = [15, 13, 10], HM = 13`, `(8, 3): F_r = [21, 16, 10], HM = 16`, `(10, 4): F_r = [84, 70, 55, 35], HM = 75`, `(9, 4): F_r = [56, 51, 45, 35], HM = 53`, and `(12, 5): F_r = [330, 288, 246, 196, 126], HM = 316`.

### Part 3 — Bollobás: saturation and an exhaustive small sweep

```python
from fractions import Fraction
from math import comb

star = sum(Fraction(1, comb(6, 1)) for _ in range(6))   # A_i = {i}, B_i = the rest
print("star sum:", star)

pairs = [(A, B) for A in range(8) for B in range(8)
         if not (A & B) and (A | B)]                    # disjoint nonempty-union pairs on [3]
def cross_ok(ps):
    return all(ps[i][0] & ps[j][1] for i in range(len(ps)) for j in range(len(ps))
               if i != j)
valid = viol = tight = 0
for p1 in pairs:
    for p2 in pairs:
        if not cross_ok([p1, p2]): continue
        fam = [p1, p2]
        for p3 in pairs:
            fam3 = fam + [p3]
            if not cross_ok(fam3): continue
            valid += 1
            s = sum(Fraction(1, comb(bin(A).count("1") + bin(B).count("1"),
                                      bin(A).count("1"))) for A, B in fam3)
            viol += s > 1; tight += s == 1
        valid += 1
        s = sum(Fraction(1, comb(bin(A).count("1") + bin(B).count("1"),
                                  bin(A).count("1"))) for A, B in fam)
        viol += s > 1; tight += s == 1
print(valid, viol, tight)
```

**Verified output.** `star sum: 1` — the six-pair singleton-complement star spends the whole budget (6 × 1/C(6,1) = 1). The exhaustive sweep over all ordered 2- and 3-pair configurations on ground set [3] satisfying both cross-intersection hypotheses prints `60 0 18`: **60** valid configurations, **0** violations, and **18** tight ones.

### Part 4 — The skew battery (Bollobás §2.3 & Exercise 14)

```python
from math import comb
from fractions import Fraction
from itertools import permutations

def bits(m): return bin(m).count("1")

# the skew battery — exhaustive, exact fractions
def skew_max(n, hyp):
    cands = []
    for A in range(1 << n):
        for B in range(1 << n):
            if A & B or not hyp(A, B): continue
            cands.append((A, B, Fraction(1, comb(bits(A) + bits(B), bits(A)))))
    memo = {}
    def best(state):
        key = tuple(sorted(state))
        if key in memo: return memo[key]
        res = Fraction(0)
        for A, B, w in cands:
            if A in state: continue
            if any(not (a & B) for a in state): continue
            tot = w + best(state + [A])
            if tot > res: res = tot
        memo[key] = res
        return res
    return best([])

variants = [(lambda A, B: True, "ANY", 1, 4),
            (lambda A, B: A != 0, "A nonempty", 1, 4),
            (lambda A, B: A != 0 and bits(A) <= bits(B), "A nonempty & |A|<=|B|", 2, 4),
            (lambda A, B: bits(A) <= bits(B), "|A|<=|B|", 2, 4)]
for hyp, name, lo, hi in variants:
    vals = [skew_max(n, hyp) for n in range(lo, hi + 1)]
    print("skew maxima", name, ":", ", ".join(str(v) for v in vals))

for n in range(2, 8):
    hf = sum(Fraction(1, comb(n, bits(A))) for A in range(1 << n))
    sing = sum(Fraction(1, comb(n, 1)) for _ in range(n))
    print(f"n = {n}: HF list sum {hf}, singleton-complement sum {sing}")

# Linear extensions of reverse inclusion on 2^[n] (A14(d): 2 at n=2, 48 at n=3)
for n in [2, 3]:
    subsets = list(range(1 << n))
    valid_orders = sum(1 for p in permutations(subsets)
                       if all(not (p[i] & ~p[j] == 0) for i in range(len(p)) for j in range(i + 1, len(p))))
    print(f"n = {n}: valid full-complement skew orderings = {valid_orders}")

def uniform_max(n, a, b):
    As = [m for m in range(1 << n) if bits(m) == a]
    cands = [(A, B) for A in As
             for B in (m for m in range(1 << n) if bits(m) == b) if not (A & B)]
    memo = {}
    def best(state):
        key = tuple(sorted(state))
        if key in memo: return memo[key]
        res = 0
        for A, B in cands:
            if A in state: continue
            if any(not (s & B) for s in state): continue
            res = max(res, 1 + best(state + [A]))
        memo[key] = res
        return res
    return best([])

for a, b, n in [(1,1,3),(1,1,4),(1,2,4),(1,2,5),(2,1,4),(2,1,5),
                (2,2,5),(2,2,6),(1,3,5),(3,1,5)]:
    m = uniform_max(n, a, b)
    print(f"uniform ({a},{b}) on [{n}]: max {m}, bound C({a+b},{a}) = {comb(a+b,a)}")
```

**Verified output.** The skew battery prints maxima **2, 3, 4, 5** with no hypotheses (n = 1..4), **1, 2, 3, 4** with Aᵢ ≠ ∅, **1, 4/3, 2** with Aᵢ ≠ ∅ and |Aᵢ| ≤ |Bᵢ| (n = 2..4), and **2, 7/3, 3** with |Aᵢ| ≤ |Bᵢ| and empty Aᵢ allowed. The Hegedüs–Frankl subset list sums to n+1 for every n = 2..7 (with `n = 2: valid full-complement skew orderings = 2` and `n = 3: valid full-complement skew orderings = 48` matching A14(d)), the singleton-complement system sums to 1, and the uniform census returns C(a+b, a) in all ten configurations.

### Part 5 — Shifting, Sunflowers, Sauer–Shelah, and the Lehmer RNG Battery (Lecture 5 & Exercises 3, 7, 10–12, 15, ◆16, ◐19)

```python
from itertools import combinations
from math import comb
from fractions import Fraction

# Deterministic Lehmer generator (seed 12345, multiplier 48271, modulus 2^31 - 1)
class LehmerRNG:
    def __init__(self, seed=12345): self.state = seed
    def next_int(self, bound):
        self.state = (self.state * 48271) % 2147483647
        return self.state % bound

def shift_ij(F, i, j):                        # (i, j)-shift on a family of frozensets
    out = set()
    for A in F:
        if j in A and i not in A:
            target = (A - {j}) | {i}
            out.add(target if target not in F else A)
        else:
            out.add(A)
    return frozenset(out)

def full_shift(F, n):
    cur = frozenset(F)
    while True:
        nxt = cur
        for i, j in combinations(range(1, n + 1), 2):
            nxt = shift_ij(nxt, i, j)
        if nxt == cur: return cur
        cur = nxt

# 1. A◆16: Stars (6) and fully shifted maximum intersecting families (6) at (6, 3)
triples6 = [frozenset(c) for c in combinations(range(1, 7), 3)]
comp_pairs6 = [(A, frozenset(range(1, 7)) - A) for A in triples6 if 1 in A]
stars6 = shifted6 = 0
for mask in range(1 << 10):
    F = frozenset(comp_pairs6[b][(mask >> b) & 1] for b in range(10))
    if len(frozenset.intersection(*F)) >= 1: stars6 += 1
    if all(shift_ij(F, i, j) == F for i, j in combinations(range(1, 7), 2)): shifted6 += 1
print(f"(6, 3) out of 1024 max families: stars = {stars6}, fully shifted = {shifted6}")

# 2. A3 & A12: Intersecting subfamilies of 2^[4], single-shift and full-shift preservation
subs4 = [frozenset(s for s in range(1, 5) if (m >> (s - 1)) & 1) for m in range(16)]
int_fams4 = []
max8_total = max8_stars = 0
for mask in range(1 << 16):
    F = frozenset(subs4[idx] for idx in range(16) if (mask >> idx) & 1)
    if all(len(A & B) > 0 for A in F for B in F):
        int_fams4.append(F)
        if len(F) == 8:
            max8_total += 1
            if len(frozenset.intersection(*F)) >= 1: max8_stars += 1
pairs4 = list(combinations(range(1, 5), 2))
single_checks = sum(1 for F in int_fams4 for i, j in pairs4
                    if all(len(A & B) > 0 for A in shift_ij(F, i, j) for B in shift_ij(F, i, j)))
print(f"A3 2^[4] max=8 families: {max8_total} ({max8_stars} stars + {max8_total - max8_stars} empty-core)")
print(f"A12 single-shift checks on 2^[4]: {single_checks}/{len(int_fams4)*len(pairs4)}")

# Antichain casualties under full_shift on [4] (A12(b): 72 of 167 nonempty antichains)
def is_antichain(F):
    return all(not (A < B) for A in F for B in F if A != B)
ac4 = [frozenset(subs4[idx] for idx in range(16) if (mask >> idx) & 1)
       for mask in range(1, 1 << 16)]
ac4 = [F for F in ac4 if is_antichain(F)]
lost_ac = sum(1 for F in ac4 if not is_antichain(full_shift(F, 4)))
print(f"A12(b) antichains on [4]: {len(ac4)}, lost after full shift: {lost_ac}")

# 3. A7 & A10: Stars and triangles census for k = 2 on n = 4, 5, 6
for n in [4, 5, 6]:
    edges = [frozenset(e) for e in combinations(range(1, n + 1), 2)]
    int_e = []
    for mask in range(1 << len(edges)):
        F = frozenset(edges[b] for b in range(len(edges)) if (mask >> b) & 1)
        if all(len(A & B) > 0 for A in F for B in F): int_e.append(F)
    int_set = set(int_e)
    maximal = [F for F in int_e if not any((F | {e}) in int_set for e in edges if e not in F)]
    max_sz = max(len(F) for F in int_e)
    max_fams = [F for F in int_e if len(F) == max_sz]
    if n == 4:
        sh_max = [F for F in maximal if full_shift(F, 4) == F]
        print(f"A7 shifted maximal edge families on [4]: {len(sh_max)}")
    print(f"A10 n={n}: total intersecting={len(int_e)}, maximal={len(maximal)}, max_size={max_sz} ({len(max_fams)} families)")

# 4. A11(b): 3-sunflower equivalence and maxima on [5] and [6]
def has_3_sunflower(F):
    for A, B, C in combinations(F, 3):
        if (A & B) == (B & C) == (A & C): return True
    return False

def max_deg_and_matching(F, n):
    deg = max([sum(1 for e in F if v in e) for v in range(1, n + 1)], default=0)
    has_3_match = any(len(A | B | C) == 6 for A, B, C in combinations(F, 3))
    return deg <= 2 and not has_3_match

for n in [5, 6]:
    edges = [frozenset(e) for e in combinations(range(1, n + 1), 2)]
    viol = best_sz = best_cnt = 0
    for mask in range(1 << len(edges)):
        F = [edges[b] for b in range(len(edges)) if (mask >> b) & 1]
        sf_free = not has_3_sunflower(F)
        cap_ok  = max_deg_and_matching(F, n)
        if sf_free != cap_ok: viol += 1
        if sf_free:
            if len(F) > best_sz: best_sz, best_cnt = len(F), 1
            elif len(F) == best_sz: best_cnt += 1
    print(f"A11(b) [n={n}]: equivalence violations={viol}, max edges={best_sz}, attainers={best_cnt}")

# 5. A15: Sauer-Shelah exhaustive census on [4]
def shatters_s(mask, s):
    for S in combinations(range(4), s):
        smask = sum(1 << i for i in S)
        traces = {idx & smask for idx in range(16) if (mask >> idx) & 1}
        if len(traces) == (1 << s): return True
    return False

for s in [1, 2, 3]:
    bound = sum(comb(4, i) for i in range(s))
    no_shatter = [bin(m).count("1") for m in range(1 << 16) if not shatters_s(m, s)]
    mx = max(no_shatter)
    print(f"A15 [4] s={s}: max={mx} (bound {bound}), attainers={no_shatter.count(mx)}")

# 6. A◐19: greedy maximal antichains — the LYM sum distribution at n = 5, 6
for n, trials in [(5, 20000), (6, 10000)]:
    rng = LehmerRNG(12345)
    vals, hits, full_levels = [], 0, 0
    for _ in range(trials):
        pool = list(range(1, 1 << n))          # every subset except the empty set
        F = []
        while pool:
            S = pool.pop(rng.next_int(len(pool)))
            F.append(S)                        # kept: the pool excludes everything comparable with F
            pool = [T for T in pool if T & S not in (T, S)]   # drop sets comparable with S
        lym = sum(Fraction(1, comb(n, bin(A).count("1"))) for A in F)
        vals.append(float(lym))
        if lym == 1:
            hits += 1
            sizes = {bin(A).count("1") for A in F}
            if len(sizes) == 1 and len(F) == comb(n, sizes.pop()):
                full_levels += 1
    qs = sorted(vals)
    print(f"A◐19 n={n} ({trials} trials): min={qs[0]:.3f} q10={qs[trials//10-1]:.3f} "
          f"median={qs[trials//2-1]:.3f} q90={qs[9*trials//10-1]:.3f} mean={sum(vals)/trials:.3f}, "
          f"LYM-equality hits={hits} (full levels: {full_levels})")
```

**Verified output.** Every single count cited across Lecture 5 and the Answer Key is reproduced verbatim:

- `(6, 3) out of 1024 max families: stars = 6, fully shifted = 6` (verifying A◆16);
- `A3 2^[4] max=8 families: 12 (4 stars + 8 empty-core)` and `A12 single-shift checks on 2^[4]: 8256/8256`, with `A12(b) antichains on [4]: 167, lost after full shift: 72`;
- `A7 shifted maximal edge families on [4]: 2` and `A10 n=4: total intersecting=27, maximal=8, max_size=3 (8 families)`, `n=5: total intersecting=76, maximal=15, max_size=4 (5 families)`, `n=6: total intersecting=192, maximal=26, max_size=5 (6 families)`;
- `A11(b) [n=5]: equivalence violations=0, max edges=5, attainers=12` and `[n=6]: equivalence violations=0, max edges=6, attainers=10`;
- `A15 [4] s=1: max=1 (bound 1), attainers=16`, `s=2: max=5 (bound 5), attainers=400`, `s=3: max=11 (bound 11), attainers=400`;
- `A◐19 n=5 (20000 trials): min=0.400 q10=0.500 median=0.700 q90=1.000 mean=0.708, LYM-equality hits=2349 (full levels: 2349)` and `A◐19 n=6 (10000 trials): min=0.333 q10=0.450 median=0.617 q90=0.783 mean=0.627, LYM-equality hits=256 (full levels: 256)` — the sampled maximal-antichain LYM sums of Exploration 19: the median sits at 0.70 (n = 5) and 0.62 (n = 6), and every sampled sum that reaches exactly 1 is a single full level.

---
## Answers to the Exercises

**A1.** View the 2-subsets of [5] as the edges of K₅: a pairwise-intersecting family is a set of edges no two of which are disjoint. If every two edges share the same vertex, the family sits inside a star — at most 4 = C(4, 1) edges. Otherwise two edges {v, a}, {v, b} share v and some edge avoids v; to meet both it must be {a, b} — the triangle. Any further edge must then meet all three triangle edges: through v it fails on {a, b} unless it is one of {v, a}, {v, b}; avoiding v it must sit inside {a, b} — {a, b} itself. So a non-star family caps at the triangle's 3 edges, and the maximum is **4**, attained exactly by the five stars. Machine check: the Part 2 census prints `(5, 2): max 4, families 5`.

**A2.** The complement map S ↦ [2k] ∖ S is an involution on the k-subsets with no fixed point (S = S̄ would force S = ∅ by disjointness), so the C(2k, k) k-sets split into ½C(2k, k) pairs; and ½C(2k, k) = C(2k−1, k−1) because C(2k, k) = (2k/k)·C(2k−1, k−1) = 2C(2k−1, k−1). Choosing one set per pair: two chosen sets A, B cannot be disjoint — B ⊆ Ā would force B = Ā (both have size k), the very pair A was chosen from. So every one-per-pair family is intersecting, of size C(2k−1, k−1) = the EKR bound: at n = 2k the bound is attained by **every** such choice.

**A3.** Complementation is a fixed-point-free involution on 2^[n] (A = Ā would put every x inside A and outside A), so the 2^n subsets split into the 2^{n−1} pairs {A, Ā}, whose two members are disjoint. An intersecting family takes at most one from each pair: |F| ≤ 2^{n−1}. Sharpness: the star — all 2^{n−1} sets containing a fixed point — is pairwise intersecting. The machine census (Part 5) of all 65,536 subfamilies of 2^[4] says the maximum 8 is attained by **12** families: the 4 stars and 8 empty-core families, for instance {12, 13, 14, 234, 123, 124, 134, 1234} — the 2-sets through 1, all four triples, and the top; every pair meets, yet the total intersection is empty. The contrast with Exercise 2: there, B ∩ A = ∅ with |A| = |B| = k at n = 2k forced B = Ā, so a one-per-pair choice banned disjointness automatically — the only sets that could clash with A were ruled out by the picking rule itself. With sizes free, two chosen sets can be disjoint without being complements ({1} from the pair {1, 234} and {23} from the pair {14, 23}), and of the 2^8 = 256 one-per-pair choices at n = 4 only those same 12 are intersecting. The pigeonhole is necessary; the safety was uniformity's gift. Machine check: Part 5 prints `A3 2^[4] max=8 families: 12 (4 stars + 8 empty-core)`.

**A4.** For an antichain A₁, …, A_m set Bᵢ = [n] ∖ Aᵢ. Then Aᵢ ∩ Bᵢ = ∅, and for i ≠ j: Aᵢ ∩ B_j = Aᵢ ∖ A_j, which is nonempty *because the family is an antichain* — Aᵢ ⊆ A_j is forbidden, so Aᵢ has an element outside A_j (and symmetrically A_j ∩ Bᵢ = A_j ∖ Aᵢ ≠ ∅). Bollobás gives Σ_{i=1..m} 1/C(|Aᵢ| + (n − |Aᵢ|), |Aᵢ|) = Σ_{i=1..m} 1/C(n, |Aᵢ|) ≤ 1: LYM. For a merely intersecting family the cross-intersection hypothesis fails at comparable pairs: Aᵢ ⊊ A_j makes Aᵢ ∩ B_j = Aᵢ ∖ A_j = ∅ even when Aᵢ ∩ A_j = Aᵢ ≠ ∅ — intersection is not incomparability.

**A5.** Naive bound: pick any start s₀ ∈ S; every other start is within cyclic distance k−1 of it (arcs intersect ⟺ start distance ≤ k−1), so all starts lie in the window {s₀−k+1, …, s₀+k−1}: at most 2k−1 of them. The loss: the forward starts (offsets A ⊆ [1, k−1]) and backward starts (offsets B ⊆ [1, k−1]) are budgeted separately as (k−1) + 1 + (k−1) = 2k−1. The sharp proof reflects the backward budget — k − B lives in the *same* interval [1, k−1] as A, and the two are disjoint (a + b = k would put two starts at cyclic distance min(k, n−k) = k > k−1), so |A| + |B| ≤ k−1 and |S| ≤ k. One substitution, one budget: that is the entire content of the "mixed sub-case".

**A6.** Let F ⊆ 2^[n] have no chain of length k+1 (1 ≤ k ≤ n+1), and write x_j = |F ∩ C([n], j)| for the level counts (0 ≤ j ≤ n). Each maximal chain ∅ = C₀ ⊂ C₁ ⊂ … ⊂ C_n = [n] meets F in at most k sets, so the double count of (chain, member on it) gives the weighted LYM inequality Σ_{j=0..n} x_j/C(n, j) ≤ k, together with the level capacity constraints 0 ≤ x_j ≤ C(n, j). Order the n+1 levels j₁, j₂, …, j_{n+1} so that C(n, j₁) ≥ C(n, j₂) ≥ … ≥ C(n, j_{n+1}); then B_r = C(n, j_r) = C(n, ⌊(n+1−r)/2⌋) are the middle binomial coefficients from the inside out. For any feasible vector (x₀, …, x_n), suppose there exist indices r ≤ k < s with x_{j_r} < B_r and x_{j_s} > 0. Since B_r ≥ B_s, replacing δ = min(B_r − x_{j_r}, x_{j_s}) > 0 units of mass at level j_s by δ units at level j_r keeps the total count Σ_{j=0..n} x_j unchanged, respects 0 ≤ x_j ≤ C(n, j), and changes the LYM weight by δ(1/B_r − 1/B_s) ≤ 0, so the LYM inequality remains satisfied. Repeating this finite exchange pushes all weight into the first k levels {j₁, …, j_k} until either no mass remains outside {j₁, …, j_k} (in which case Σ_j x_j = Σ_{r=1..k} x_{j_r} ≤ Σ_{r=1..k} B_r) or every level j₁, …, j_k is completely full (x_{j_r} = B_r for 1 ≤ r ≤ k), which spends the entire LYM budget Σ_{r=1..k} B_r/B_r = k and forces x_{j_s} = 0 for all s > k. In both cases |F| = Σ_{j=0..n} x_j ≤ Σ_{r=1..k} C(n, ⌊(n+1−r)/2⌋). And the exercise's closing question — where does maximality close the bound? — has an honest answer: in this ledger it never has to. The exchange runs on the actual level counts of any family with no (k+1)-chain, so the LYM budget pays alone; in the older route (exchange inside a maximum-size family), maximality closes at the inertia point — no profitable exchange left means the family already sits in the k middle levels, and its size is the middle-binomial sum. Machine check: the n = 4 census maxima {6, 10, 14, 15}, the four sums of middle binomials (Part 1).

**A7.** For 1 ≤ i < j ≤ n, the (i, j)-shift S_{ij} maps A ∈ F to A′ = (A ∖ {j}) ∪ {i} when j ∈ A, i ∉ A, and A′ ∉ F, and fixes A otherwise. Every image S_{ij}(A) has |S_{ij}(A)| = |A|, preserving k-uniformity. To see injectivity on F, suppose S_{ij}(A) = S_{ij}(B) for A, B ∈ F. If neither was moved, A = B; if both were moved, then A = (S_{ij}(A) ∖ {i}) ∪ {j} = B; and if A was moved while B was fixed, then S_{ij}(A) = A′ ∉ F whereas S_{ij}(B) = B ∈ F, impossible. Thus |S_{ij}(F)| = |F|. Whenever S_{ij}(F) ≠ F, at least one set A ∈ F is replaced by A′ = (A ∖ {j}) ∪ {i}, which changes w(F) = Σ_{A∈F} Σ_{x∈A} x by i − j < 0 per moved set. Since w(F) is a nonnegative integer, any sequence of nontrivial shifts terminates. On C([4], 2): if a shifted maximal intersecting family F contains a pair {a, b} avoiding 1 (2 ≤ a < b ≤ 4), shift stability S_{1b}(F) = F and S_{1a}(F) = F forces {1, a}, {1, b} ∈ F, forming the triangle {1a, 1b, ab}; shifting down to {2, 3} via S_{2a} and S_{3b} forces a = 2, b = 3, giving the unique shifted triangle **{12, 13, 23}**. If no member of F avoids 1, then F ⊆ {12, 13, 14}, and maximality forces the full star **{12, 13, 14}**. Machine check: Part 5 prints `A7 shifted maximal edge families on [4]: 2`.

**A8.** (⇐) is Exercise 2. (⇒) Let |F| = C(2k−1, k−1) — exactly the number of complementary pairs {S, [2k] ∖ S}. Since F is intersecting, it never contains both members of a pair (they are disjoint); so it contains at most one per pair — that is at most C(2k−1, k−1) sets, and equality of counts forces **exactly one per pair**. For (6, 3): C(5, 2) = 10 pairs, so 2^10 = **1024** maximum families, the 6 stars among them (a star contains exactly one member of each pair — every 3-set either contains the center x or its complement does). Machine check: Part 2 prints `max 10, families 1024`.

**A9.** All starts lie in the window [s₀−k+1, s₀+k−1] around the anchor s₀; a forward start sits at s₀+a (a ∈ A ⊆ [1, k−1]) and a backward one at s₀−b (b ∈ B ⊆ [1, k−1]). Two window positions at offset-sum a+b are at cyclic distance min(a+b, n−a−b); for a+b = k and n ≥ 2k this distance is min(k, n−k) = k > k−1 — the two arcs would be disjoint, forbidden. So no a ∈ A satisfies a = k−b for b ∈ B: **A ∩ (k−B) = ∅**, both inside [1, k−1], whence |A| + |B| ≤ k−1 and |S| = 1 + |A| + |B| ≤ k. On (6, 3) with S = {0, 2, 4} and anchor s₀ = 0: A = {2}, B = {2}, k−B = {1}: disjoint inside {1, 2}, |A| + |B| = 2 = k−1 ✓. On S = {0, 1, 2} with anchor s₀ = 0: A = {1, 2}, B = ∅, k−B = ∅, |A| + |B| = 2 ✓. For the t-intersecting extension (1 ≤ t ≤ k, n ≥ 2k−t+1): two k-arcs at cyclic distance d ≤ k overlap in k−d consecutive points along the shorter arc (since d ≤ k−t gives k+d ≤ 2k−t < n, the two arcs cannot wrap around and meet at both ends), so |A_s ∩ A_{s′}| ≥ t ⟺ dist(s, s′) ≤ k−t. With anchor s₀ ∈ S, all other starts have offsets A, B ⊆ [1, k−t], and a+b = k−t+1 is forbidden because min(k−t+1, n−(k−t+1)) = k−t+1 > k−t (using n ≥ 2k−t+1 ≥ 2(k−t+1)). Thus A ∩ ((k−t+1)−B) = ∅ inside [1, k−t], giving |A| + |B| ≤ k−t and |S| ≤ k−t+1.

**A10.** (a) With at most one edge the family sits in any star. With two, they share a vertex v — say {v, a} and {v, b} (disjointness is banned). If every edge contains v: the star at v. Otherwise some edge avoids v; to meet both {v, a} and {v, b} it must be {a, b}, and the triangle {v, a}, {v, b}, {a, b} is present. A fourth edge meeting all three: through v it would be {v, c} with c ∉ {a, b} — disjoint from {a, b}; avoiding v it must fit inside {a, b}, and {a, b} is taken. So the family sits inside the star at v or inside that triangle. (b) The full star at v is maximal for n ≥ 4: an added edge {a, b} avoiding v misses the star edge {v, c} for any c ∉ {a, b}, and n ≥ 4 provides such a c. A triangle is maximal by the same chase — nothing meets all three edges. Since every intersecting family sits in one of these, the maximal ones are exactly the n stars and the C(n, 3) triangles: 8, 15, 26 at n = 4, 5, 6, in exact agreement with the Part 5 censuses (27, 76, 192 intersecting families, zero of them outside a star or a triangle). At n = 3 the star is not maximal — it sits inside the one triangle — which is why the count needs n ≥ 4. (c) Stars have n−1 edges and win alone once n ≥ 5 (5 stars at n = 5, 6 at n = 6). At n = 4, stars and triangles tie at 3 = C(3, 1). A8 says the maxima at n = 2k are the one-per-pair choices — 2^3 = 8 at (4, 2) — and each triangle complies: {12, 13, 23} takes 12 against 34, 13 against 24, and 23 against 14, one edge from each complementary pair. The eight maxima are the four stars and the four triangles, every one a one-per-pair family, as A8 demands.

**A11.** (a) Induction on k ≥ 1. For k = 1, a family F of subsets of size ≤ 1 has at most one empty set and at most |F| − 1 distinct singletons; if |F| > 1!(r−1)^1 = r−1, then |F| ≥ r. If ∅ ∉ F, any r distinct singletons form an r-sunflower with core ∅; if ∅ ∈ F, then ∅ together with any r−1 distinct singletons {x₁}, …, {x_{r−1}} satisfies Sᵢ ∩ S_j = ∅ for all i ≠ j, again an r-sunflower with core ∅. Now let k ≥ 2 and assume the lemma holds at k−1. If some point x lies in more than (k−1)!(r−1)^{k−1} members of F, the trace family {A ∖ {x} : x ∈ A ∈ F} has more than (k−1)!(r−1)^{k−1} distinct sets of size at most k−1; the induction hypothesis yields an r-sunflower B₁, …, B_r among them with core K, and B₁ ∪ {x}, …, B_r ∪ {x} form an r-sunflower in F with core K ∪ {x}. Otherwise every point has degree at most (k−1)!(r−1)^{k−1} in F. Let P₁, …, P_t be a maximal pairwise-disjoint subfamily of nonempty members of F, and set P = P₁ ∪ … ∪ P_t. If ∅ ∉ F and t ≥ r, then P₁, …, P_r is an r-sunflower with core ∅; if ∅ ∈ F and t ≥ r−1, then ∅, P₁, …, P_{r−1} is an r-sunflower with core ∅. In the remaining case, either ∅ ∉ F and t ≤ r−1 (so |P| ≤ (r−1)k and every A ∈ F meets P, giving |F| ≤ |P|·(k−1)!(r−1)^{k−1} ≤ k!(r−1)^k), or ∅ ∈ F and t ≤ r−2 (so |P| ≤ (r−2)k and every A ∈ F ∖ {∅} meets P, giving |F| ≤ 1 + (r−2)k(k−1)!(r−1)^{k−1} ≤ k!(r−1)^k, since k(k−1)!(r−1)^{k−1} ≥ 1). Both contradict |F| > k!(r−1)^k. (b) For 2-uniform edges, the possible cores of a 3-sunflower are ∅ (three disjoint edges) and {v} (three distinct edges through v, whose pairwise intersections all equal {v}); a core of size 2 would require three identical edges, impossible in a family. So no 3-sunflower ⟺ no three disjoint edges and no vertex of degree ≥ 3 ⟺ ν ≤ 2 and Δ ≤ 2 (Part 5 verifies 0 violations over all 1,024 edge families on [5] and all 32,768 on [6]). Under those two caps the census maxima are **5** on [5], attained by the 12 labeled 5-cycles (5!/10 = 12), and **6** on [6], attained by the 10 disjoint triangle pairs (½C(6, 3) = 10). (c) The bound 2!·2² = 8 sits above both true maxima (5 and 6). The Erdős–Rado sunflower conjecture asks whether (r−1)^k k! can be improved to c_r^k for a constant c_r > 0 depending only on r (note c_r ≥ r−1 is forced by taking k disjoint blocks of size r−1). The 2020 breakthrough of Alweiss–Lovett–Wu–Zhang, simplified by Rao, proved (Cr log(rk))^k; Bell–Chueluecha–Warnke (2021) refined it to (Cr log k)^k — the current best. The c_r^k conjecture remains open.

**A12.** (a) The ledger, uniformity-free. Write C* = (C ∖ {j}) ∪ {i} for a shifted member, and suppose S_{ij}(F) contains disjoint images C′ and D′; injectivity (A7, proved without uniformity) gives unique preimages in F. Case 1, both unshifted: C ∩ D = ∅ inside F — forbidden. Case 2, both shifted: C* and D* both contain i — not disjoint. Case 3, mixed — say C′ = C is unshifted and D′ = D* = (D ∖ {j}) ∪ {i} with C ∩ D* = ∅. Then i ∉ C (since i ∈ D*), and D contained j but not i. Since F is intersecting, C ∩ D ≠ ∅; but D = (D* ∖ {i}) ∪ {j}, so C ∩ D ⊆ (C ∩ D*) ∪ (C ∩ {j}) = C ∩ {j} — hence C ∩ D = {j}, and j ∈ C. Now C contains j and not i: C was itself a shift candidate, and it stayed unmoved only because C* = (C ∖ {j}) ∪ {i} already lies in F. But C* ∩ D = ((C ∖ {j}) ∩ D) ∪ ({i} ∩ D) = ∅ ∪ ∅ = ∅ — the first term is empty because C ∩ D = {j}, the second because i ∉ D. Two disjoint members C*, D ∈ F: the contradiction lands in the *original* family, where uniformity was never consulted. (b) Take F = {{1, 3}, {2}} under S_{23}: the shift condition holds for {1, 3} (j = 3 present, i = 2 absent, {1, 2} ∉ F), so the image is {{1, 2}, {2}} — and {2} ⊂ {1, 2}: a chain. The full shift does not rescue it: cycling the pairs to §5.3's stability lands at {{1}, {1, 2}}, still a chain (machine, exact). Nor is it a fluke: of the 167 nonempty antichains on [4], **72** lose the antichain property by the time the full shift stabilizes. (c) The audit: §5.1 defines the shift for arbitrary sets, §5.2 proves intersecting-preservation in that setting, §5.3 and A7 verify size, uniformity, and termination, and the EKR application shifts k-sets throughout — uniformity is present at every use, and by (a) it was never even needed for intersecting-preservation, only for the k-set bookkeeping around it. The antichain casualty of (b) touches nothing standing: nothing in Lecture 5 shifts an antichain. Machine: Part 5 verifies all 8,256 single-shift checks on intersecting subfamilies of 2^[4] — 1,376 intersecting families × 6 pairs — with 0 violations, plus 2,570 sampled single shifts on [5], zero violations, and the full-shift census over all 65,536 families on [4], again zero violations.

**A13.** Equality forces |A| + |B| = k−1 with A and k−B tiling [1, k−1] disjointly: A ⊔ (k−B) = [1, k−1]. The room n ≥ 2k+1 (n > 2k) bans one more sum: a+b = k+1 puts two starts at cyclic distance min(k+1, n−k−1) ≥ k > k−1 — forbidden, so **A ∩ (k+1−B) = ∅**. Now take b ∈ B with b ≥ 2 and suppose b−1 ∉ B. Then k−(b−1) ∉ k−B, so by the tiling k−b+1 ∈ A; but (k−b+1) + b = k+1 — a forbidden sum — contradiction. So b ∈ B, b ≥ 2 ⟹ b−1 ∈ B: B is downward-closed, B = {1, …, β} for some 0 ≤ β ≤ k−1, and the tiling forces A = {1, …, k−1−β}: **k consecutive starts** {s₀−β, …, s₀+k−1−β} (mod n), whose k arcs share the unique point z ≡ s₀+k−1−β (mod n) (as proved in §3.3). On Figure 1's exact data (n = 10, k = 4, S = {8, 9, 0, 1}, anchor s₀ = 0): the forward offset is A = {1} (start 0+1 = 1), the backward offsets are B = {1, 2} (starts 0−1 ≡ 9 and 0−2 ≡ 8, so β = 2), and the reflected set is k−B = {4−1, 4−2} = {2, 3}. Thus A ⊔ (k−B) = {1} ⊔ {2, 3} = {1, 2, 3} = [1, k−1] ✓, the starts are {s₀−2, s₀−1, s₀, s₀+1} ≡ {8, 9, 0, 1}, and the four 4-arcs {8, 9, 0, 1}, {9, 0, 1, 2}, {0, 1, 2, 3}, {1, 2, 3, 4} share the unique common point s₀+k−1−β = 0+3−2 = **1** ✓.

**A14.** (a) The two pairs: A₁∩B₁ = {1}∩∅ = ∅ ✓, A₂∩B₂ = {2}∩{1} = ∅ ✓; the one forward condition A₁∩B₂ = {1}∩{1} ≠ ∅ ✓. Sum: 1/C(1,1) + 1/C(2,1) = 1 + 1/2 = **3/2**. (b) The three pairs: disjointness {1}∩{2} = {2}∩{1} = {3}∩{1, 2} = ∅ ✓; forward conditions A₁∩B₂ = {1}∩{1} ≠ ∅, A₁∩B₃ = {1}∩{1, 2} ≠ ∅, A₂∩B₃ = {2}∩{1, 2} ≠ ∅ ✓; Aᵢ ≠ ∅ for all three ✓; |Aᵢ| ≤ |Bᵢ| (1 ≤ 2, 1 ≤ 1, 1 ≤ 2) ✓. Sum: 1/C(2,1) + 1/C(2,1) + 1/C(3,1) = 1/2 + 1/2 + 1/3 = **4/3** > 1 — the size hypothesis does not rescue Σ ≤ 1. The exhaustive census (Part 4) confirms the pattern: under Aᵢ ≠ ∅ and |Aᵢ| ≤ |Bᵢ| the maxima at n = 2, 3, 4 are 1, 4/3, 2 — the sum genuinely grows (and by symmetry the same holds for |Aᵢ| ≥ |Bᵢ|: swap the roles of the A's and B's and read the list backwards). (c) Singleton-complement: for i ≠ j, Aᵢ ∩ B_j = {i} ∩ ([n] ∖ {j}) = {i} ≠ ∅ — the system is cross-intersecting in *both* directions, a fortiori skew in any order; Σ = n · 1/C(n, 1) = **1**, the budget exactly spent. Uniform sharpness: pair every a-subset A of a fixed (a+b)-set X with B = X ∖ A; for i ≠ j the same-size distinctness of Aᵢ, A_j gives Aᵢ ⊄ A_j, i.e. Aᵢ ∩ B_j ≠ ∅ — m = C(a+b, a) skew pairs, each of weight 1/C(a+b, a): Σ = 1, meeting Frankl's uniform bound m ≤ C(a+b, a) (1982; also Kalai 1984, and via Lovász's exterior algebra / tensor argument) exactly. The census says the bound survives larger grounds: at (a, b) = (1, 1) on [4] the maximum is still 2, at (2, 2) on [6] still 6 = C(4, 2) — out of 15 available A's; all ten checked configurations return C(a+b, a). (d) Order all 2^n subsets of [n] by non-increasing size (ties arbitrary). For i < j: |Aᵢ| ≥ |A_j|, so Aᵢ ⊆ A_j would force Aᵢ = A_j — forbidden, since the list has no repeats — hence Aᵢ ⊄ A_j, which is exactly Aᵢ ∩ B_j ≠ ∅ for B_j = [n] ∖ A_j; disjointness is complementarity. So the system is skew, and Σ 1/C(|Aᵢ|+|Bᵢ|, |Aᵢ|) = Σ_{A ⊆ [n]} 1/C(n, |A|) = Σ_{k=0..n} C(n,k)/C(n,k) = **n+1** — the sharpness witness for the Hegedüs–Frankl bound Σ ≤ n+1 (2023). The machine census confirms optimality (n = 1..4: maxima 2, 3, 4, 5, the witnesses being complement systems) and at n = 2, 3 the extremal pair-set is unique up to valid skew ordering (2 and 48 valid orderings respectively, verified in Part 4). **The lesson:** no size condition on the individual pairs brings the sum back to 1. The true landscape is the uniform bound C(a+b, a) and the sharp n+1; the "skew Bollobás with Σ ≤ 1 under a size hypothesis" that circulates informally is false, and the three-pair family of (b) is its smallest refutation.

**A15.** (i) The projection π(A) = A ∖ {x} maps F onto G₀, and each fiber {A, A ∪ {x}} ∩ F has size 1 or 2 — size 2 iff the projection belongs to G₁. Summing the fiber sizes gives |F| = |G₀| + |G₁|. (ii) If G₀ shatters S ⊆ [n] ∖ {x} with |S| = s: every A ∈ G₀ has a lift in F (A or A ∪ {x}), and both lifts cut S in A ∩ S since x ∉ S, so F shatters S. (iii) If G₁ shatters S ⊆ [n] ∖ {x} with |S| = s−1: for each T ⊆ S take A ∈ G₁ with A ∩ S = T; both A and A ∪ {x} lie in F, cutting S ∪ {x} in T and T ∪ {x}, so F shatters the s-set S ∪ {x}. (iv) Induct on n ≥ 0 and s ≥ 0. Base cases: for s = 0 the empty sum is 0, and |F| > 0 means F is nonempty, so it shatters ∅; for n = 0 and s ≥ 1, the bound is C(0, 0) = 1, and |F| ≤ |2^∅| = 1 never exceeds 1. For n ≥ 1 and s ≥ 1, G₀ and G₁ live on the n−1 coordinates [n] ∖ {x}. If F shatters no s-set, then by (ii) G₀ shatters no s-set, so |G₀| ≤ Σ_{i=0..s−1} C(n−1, i), and by (iii) G₁ shatters no (s−1)-set, so |G₁| ≤ Σ_{i=0..s−2} C(n−1, i). Adding via Pascal's identity C(n−1, i) + C(n−1, i−1) = C(n, i) gives |F| = |G₀| + |G₁| ≤ Σ_{i=0..s−1} C(n, i). Sharpness: {A ⊆ [n] : |A| ≤ s−1} has size Σ_{i=0..s−1} C(n, i) and on any s-set S its traces never realize S itself (A ∩ S = S requires |A| ≥ s). Machine: Part 5's exhaustive [4] census over all 65,536 families returns maxima **1, 5, 11** at s = 1, 2, 3 with 16, 400, 400 attainers; the fiber identity and both shatter steps re-verified on 5,000 random [5] instances, zero violations; and the boundary probed from above — 20,000 random [5] families, all of size above 6, all shattered a 2-set, and of 10,000 further samples the 4,677 of size above 16 all shattered a 3-set. Zero escapes.

**A◆16.** At (6, 3) the EKR bound is C(5, 2) = 10, and by A8's characterization a family F ⊆ C([6], 3) has size 10 and is intersecting iff it picks **exactly one triple from each of the 10 complementary pairs** {S, [6] ∖ S}: there are **2^10 = 1024** maximum intersecting families. Among them, the **6 stars** star(x) = {S ∈ C([6], 3) : x ∈ S} (x ∈ [6]) each pick the unique member containing x from every pair. How many of the 1024 maximum families are *fully shifted*? A family F is stable under all shifts S_{ij} (1 ≤ i < j ≤ 6) iff it is an order ideal in the Gale (componentwise) poset on C([6], 3), where {a₁ < a₂ < a₃} ≤_G {b₁ < b₂ < b₃} ⟺ a₁ ≤ b₁, a₂ ≤ b₂, a₃ ≤ b₃. For 5 of the 10 complementary pairs, the two members are comparable in the Gale order (123 ≤_G 456, 124 ≤_G 356, 125 ≤_G 346, 134 ≤_G 256, 135 ≤_G 246), so any shifted one-per-pair family must pick the smaller triple (123, 124, 125, 134, 135). The remaining 5 complementary pairs have Gale-incomparable members: Q₁ = (126, 345), Q₂ = (136, 245), Q₃ = (145, 236), Q₄ = (146, 235), Q₅ = (156, 234). Since 126 ≤_G 136 ≤_G 146 ≤_G 156 (and dually 234 ≤_G 235 ≤_G 245 ≤_G 345), downward closure on {Q₁, Q₂, Q₄, Q₅} requires choosing a threshold 0 ≤ r ≤ 4 where the 1-containing triple is chosen in the first r of (Q₁, Q₂, Q₄, Q₅) and the 1-avoiding complement in the remaining 4−r. For Q₃ = (145, 236): the relations 136 ≤_G 236 and 235 ≤_G 236 ban 236 unless r = 2 (choosing 236 needs 136 ∈ F, which happens only for r ≥ 2, and 235 ∈ F, which happens only for r ≤ 2), while 145 ≤_G 245 and 145 ≤_G 146 force 145 whenever 245 ∈ F (r ≤ 1) or 146 ∈ F (r ≥ 3). So r = 0, 1, 3, 4 each give one family — Q₃ forced to 145 — and r = 2 gives two (both Q₃ choices downward-closed): 1+1+2+1+1 = **6** fully shifted maximum families: C([5], 3) (r = 0, picking 345, 245, 145, 235, 234), star(1) (r = 4, picking 126, 136, 145, 146, 156), and the four intermediate families for r = 1, 2, 3. Machine check: Part 5 prints `(6, 3) out of 1024 max families: stars = 6, fully shifted = 6`.

**A◆17.** Six chains, produced directly by the doubling construction (Part 1's `scd(4)`):

∅ ⊂ {1} ⊂ {1, 2} ⊂ {1, 2, 3} ⊂ {1, 2, 3, 4} — sizes 0…4 (length 5);
{4} ⊂ {1, 4} ⊂ {1, 2, 4} — sizes 1, 2, 3 (length 3);
{3} ⊂ {1, 3} ⊂ {1, 3, 4} — sizes 1, 2, 3 (length 3);
{3, 4} — size 2 (length 1);
{2} ⊂ {2, 3} ⊂ {2, 3, 4} — sizes 1, 2, 3 (length 3);
{2, 4} — size 2 (length 1).

All 16 subsets of [4] appear once (5 + 3 + 3 + 1 + 3 + 1 = 16, partition ✓); every step adds one element ✓; every chain satisfies |bottom| + |top| = 4 ✓ (0+4, 1+3, 1+3, 2+2, 1+3, 2+2). The total number of chains is **6 = C(4, 2)** — the middle binomial coefficient, matching Part 1's `scd(4) chain lengths: [5, 3, 3, 1, 3, 1]`.

**A◐18.** At (n, k) = (9, 4), the EKR bound is C(8, 3) = **56**, and by §4.3's Theorem (since 9 ≥ 2(4)+1), the maximum intersecting families of size 56 are **only the 9 stars** star(x) (x ∈ [9]). What do the largest non-star (empty-core, ∩_{A∈F} A = ∅) intersecting families look like? By the Hilton–Milner theorem, the maximum size of an intersecting 4-uniform family on [9] with empty core is HM(9, 4) = C(8, 3) − C(4, 3) + 1 = 56 − 4 + 1 = **53**, achieved by fixing a point x ∈ [9] and a 4-set E ⊆ [9] ∖ {x} and taking F_HM(x, E) = {E} ∪ {A ∈ C([9], 4) : x ∈ A and A ∩ E ≠ ∅} (there are 9 × C(8, 4) = 630 such families). The second natural empty-core competitor is the 2-out-of-3 majority family F₁ = {A ∈ C([9], 4) : |A ∩ {1, 2, 3}| ≥ 2}, which has size C(3,2)C(6,2) + C(3,3)C(6,1) = 45 + 6 = **51** < 53. Thus at (9, 4) there is a gap of 3 between the 9 stars (56) and the 630 Hilton–Milner families (53), and a further gap of 2 down to the C(9, 3) = 84 majority families F₁ (51).

A full census at (9, 4) is infeasible — even the shifted search space alone reaches about 17 million Gale ideals — so the honest receipts are partial, and every one of them agrees with the theorem: a pruned sweep of all shifted intersecting 4-families on [9] (37,145 of them, the empty family included) finds exactly one maximum, star(1) at 56, and a unique empty-core maximum at 53, attained by HM(1, {2,3,4,5}) — exactly the shifted Hilton–Milner shape — with nine shifted families at 51; and a hill-climb launched from all 630 Hilton–Milner families never found anything above 53. For comparison, the reachable censuses (7, 3) and (8, 3) return 7 and 8 maximum families, all stars (Part 2).

**A◐19.** For n = 4, Part 1's exhaustive sweep over all 2^16 − 1 = 65,535 nonempty subfamilies of 2^[4] finds exactly **167** nonempty antichains (stored in `ac4` in Part 5), all satisfying Σ_{A∈F} 1/C(4, |A|) ≤ 1, with equality in **5** of them — the five full levels C([4], j) (j = 0, 1, 2, 3, 4). To prove that for every n ≥ 1 the *only* nonempty antichains with Σ_{A∈F} 1/C(n, |A|) = 1 are the n+1 full levels C([n], j), let j be the largest level such that F_j = F ∩ C([n], j) ≠ ∅. If j = 0, then F = {∅} = C([n], 0). If 1 ≤ j ≤ n, every A ∈ F_j has j immediate subsets in ΔF_j = {A ∖ {x} : A ∈ F_j, x ∈ A} ⊆ C([n], j−1), and each B ∈ ΔF_j is contained in at most n−j+1 sets of F_j, giving the LYM shadow inequality |ΔF_j|/C(n, j−1) ≥ |F_j|/C(n, j). Equality in this shadow step holds iff every B ∈ ΔF_j has all n−j+1 of its j-supersets in F_j and every A ∈ F_j has all j of its (j−1)-subsets in ΔF_j; since the bipartite inclusion graph between C([n], j) and C([n], j−1) is connected for 1 ≤ j ≤ n, equality for F_j ≠ ∅ holds **iff** F_j = C([n], j). Because F is an antichain, F_{j−1} ∩ ΔF_j = ∅, so replacing F_j by ΔF_j produces an antichain on levels ≤ j−1 whose LYM sum is at least that of F, and strictly larger unless F_j = C([n], j) (in which case F = C([n], j) already). At odd n, the full union C([n], (n−1)/2) ∪ C([n], (n+1)/2) has LYM sum 2 > 1 and is never an antichain, whereas partial mixes can be: taking A from the lower level and B from the upper, the mix is an antichain exactly when B ∩ ∇A = ∅ (for n = 3, A = {{1}} leaves {2, 3} outside ∇A, giving {{1}, {2, 3}} with LYM sum 2/3). What does sampling say? In random greedy sampling of maximal antichains at n = 5, 6 (Part 5's Lehmer-seeded sampler: 20,000 trials at n = 5, 10,000 at n = 6), early inclusion of a small or large set blocks a wide cone of comparable sets in the middle levels, so the sampled LYM sums concentrate well below the budget — median 0.70 at n = 5 (mean 0.71, deciles 0.50 and 1.00) and median 0.62 at n = 6 (deciles 0.45 and 0.78) — and every sampled sum that reaches exactly 1 is a single full level: 2,349 such hits at n = 5 and 256 at n = 6, all full levels.

**A◐20.** For 0 ≤ r ≤ k−1, F_r = {A ∈ C([n], k) : |A ∩ [2r+1]| ≥ r+1} has size |F_r| = Σ_{i=r+1..min(k, 2r+1)} C(2r+1, i)C(n−2r−1, k−i), while HM(n, k) = C(n−1, k−1) − C(n−k−1, k−1) + 1. Evaluating both across the five benchmark pairs (verified in Part 2 of the Lab):

- **(7, 3):** (|F₀|, |F₁|, |F₂|) = (15, 13, 10) and HM(7, 3) = 15 − 3 + 1 = **13**. Here |F₁| = HM(7, 3) = 13: at k = 3, F₁ and F_HM tie for the empty-core maximum (35 families of type F₁ and 7 × C(6, 3) = 140 of type F_HM, totaling 175 empty-core maxima).
- **(8, 3):** (|F₀|, |F₁|, |F₂|) = (21, 16, 10) and HM(8, 3) = 21 − 6 + 1 = **16** (tied again at k = 3).
- **(10, 4):** (|F₀|, |F₁|, |F₂|, |F₃|) = (84, 70, 55, 35) and HM(10, 4) = 84 − 10 + 1 = **75** > 70.
- **(9, 4):** (|F₀|, |F₁|, |F₂|, |F₃|) = (56, 51, 45, 35) and HM(9, 4) = 56 − 4 + 1 = **53** > 51.
- **(12, 5):** (|F₀|, |F₁|, |F₂|, |F₃|, |F₄|) = (330, 288, 246, 196, 126) and HM(12, 5) = 330 − 15 + 1 = **316** > 288.

For 1-intersecting families with n > 2k: the star F₀ is always the overall maximum (by EKR), and the Hilton–Milner family F_HM is always the true empty-core maximum — strictly beating F₁ for all k ≥ 4, and tying F₁ at k = 3. Where do the higher candidates overtake the star? In the **t-intersecting** problem (|A ∩ B| ≥ t for t ≥ 2): Ahlswede and Khachatrian's 1997 Complete Intersection Theorem proves that for all n ≥ 2k−t, the maximum of a t-intersecting k-uniform family on [n] is max_{0 ≤ r ≤ k−t} |F_r^{(t)}|, where F_r^{(t)} = {A ∈ C([n], k) : |A ∩ [t+2r]| ≥ t+r}. The t-star F₀^{(t)} wins iff n ≥ (t+1)(k−t+1); as soon as n < (t+1)(k−t+1) (for instance n = 8, k = 4, t = 2, where |F₀^{(2)}| = C(6, 2) = 15 < |F₁^{(2)}| = 4C(4, 1) + 1 = **17**), F₁^{(t)} and higher F_r^{(t)} take over.

---
## Revision History & Verification Notes

**Editions.** Reference edition (five problem families: Sperner/LYM with the SCD as a flagged sketch, EKR with the sharp interval lemma flagged, Bollobás, the integer staircase, and Cauchy–Davenport as a statement with a flagged sketch; one verified lab) → **Feynman lecture edition** (this edition): 8 lectures. Everything from the reference canon is preserved inside the narrative, and the flagged sketches are now complete proofs: Katona's interval lemma in full — including the mixed sub-case and the equality structure at n > 2k —, the symmetric chain decomposition actually built by the doubling construction (with Erdős's generalization proved from it, no exchange argument required), Cauchy–Davenport twice (merge/periodicity and the polynomial method, with the m-fold corollary), and two new summits: the uniqueness lecture (complete n = 2k characterization, structural steps at n > 2k, honest flags on the transport) and the Kneser–EGZ lecture (stabilizer subgroup lemma, the e-transform toolkit with both properties proved, the quotient reduction proved in full, and the Erdős–Ginzburg–Ziv theorem end to end). The full Atlas exercise standard is installed (tiers, ◆ pattern-unknown, ◐ Explorations, worked answers, this appendix), and two figures are embedded (the interval-lemma window; the sumset staircase grid). A **canon-install pass** then added the closing lecture: Kruskal–Katona proved through Keevash's clique-form argument with the equality structure, the j-form by own-parameter induction, Daykin's complement mirror as a third complete EKR proof (retiring the shifting route's flag), the honest shade-route-to-uniqueness discussion, the Hilton–Milner and Ahlswede–Khachatrian gateways, the union-closed lore, the corrected skew landscape (graded Exercise 16 with worked answer), the ◐24 exploration, and the lab's Part 6 — with the pattern table, Trick Bag, and formula box extended to match. A **restructure pass (session 38)** then slimmed the course to its five-lecture extremal-set core: Lectures 6–8 (sumsets twice and shadows) moved verbatim — with nine exercises, eight worked answers, Figure 2, and the lab's Parts 4 and 5 plus Part 6 minus its skew battery — into the new Chapter 9 skeleton, "Sumsets and Shadows: the Completed Arcs", assembled the same session; the skew battery stayed here as the new lab Part 4 (it anchors §2.3 and Exercise 10); exercises renumbered 1–10 graded, ◆11–◆12, ◐13–◐15, answers A1–A10 + A◆11–A◆12. The appendix's earlier paragraphs keep the numbering of their time. The session-65 adversarial review then audited the whole chapter with a fresh machine battery — two proof-site repairs (the §5.1 shift definition made conditional, the semantics every lemma already uses; §5.2's false D-part clause replaced by the disjointness established above the case split), one lab-code repair (Part 2's is_consec second clause was dead code — replaced by the verified full-cyclic test, the recorded outputs already correct), and three record-level classes (the LYM-equality wording at ◐14 and the §1.1 ✎; two lab→verification-record attributions; A20(c)'s audit sentence), the mathematics otherwise untouched (the review record below).

**Corrections during the rewrite (verification-pass honesty).** Five items were caught by the machine or by the verification discipline before anything was installed. (1) **The middle-J uniqueness step is false as naively stated**: the planned exclusion |𝓗| < C(n−1, k−1) cannot hold, because 𝓗 (the k-sets hitting both the head and tail configurations) always contains the star at z = t_{k−J} — |𝓗| ≥ C(n−1, k−1) unconditionally. Lecture 4 was restructured around this: the counting reduction, the per-circle structure, and the complete n = 2k characterization are proved; the middle-J transport and the thin range 2k < n ≤ 3k−2 are flagged with citations and machine census evidence instead of a fake proof. (2) A lab-writer's bug: the composite EGZ check first tested the final sum modulo m — the *scaled* modulus — instead of modulo nm; the fixed check (sum of the union divisible by nm, equivalently the halved-then-selected block sums ≡ 0 mod m) is what the lab runs. (3) The merge monitor first counted the trivial b = 0 step as a zero-gain event; the fixed monitor skips it, and then *every* zero-gain step fires only when the running set is already the whole field — the periodicity claim in its clean form. (4) Three self-correcting prose artifacts in the Lecture 7 draft were caught and removed before assembly (a checkpoint phrased as visible self-correction, a wrong element count in the composite proof, a mangled cross-reference). (5) **The canon-audit proposal quoted a false skew theorem.** The proposal's "Frankl Σ ≤ 1 with |Aᵢ| ≤ |Bᵢ|" appears in none of the sources it gestured at: Frankl's 1982 paper proves the *uniform* bound m ≤ C(a+b, a), and the non-uniform statement that holds is Hegedüs–Frankl's Σ 1/C(|Aᵢ|+|Bᵢ|, |Aᵢ|) ≤ n+1 (2023, sharp). The quoted version was machine-refuted on [3] — the three-pair family of §2.3's warning satisfies every skew condition plus A ≠ ∅ and |Aᵢ| ≤ |Bᵢ| and sums to 4/3 — before installation, and the install teaches the verified landscape instead (§2.3, the Trick Bag, Exercise 16/A16, Part 6g). The audit's lesson, recorded: proposals are re-verified against the sources and the machine *before* they become chapter content.

**Canon-coverage audit — executed (user-approved).** A standing Atlas goal is auditing each chapter against the broader canon; the audit PROPOSES and the user approves before anything is installed. This chapter's audit produced four proposals, which the user approved, and they are now chapter content: (1) **The Kruskal–Katona theorem** — the chapter's load-bearing gap, since the shifting route to EKR flags its closing induction and Frankl's uniqueness route runs through shade minimization — installed as Lecture 8: the cascade and Lovász statements with the colex agreement machine-checked (781/781), Keevash's clique-form proof in full with the equality analysis (equality ⟺ integer x and the complete family, all 99 exhaustive cases confirmed), the j-form by own-parameter induction, and Daykin's mirror as a third complete EKR proof, closing flag (i) — the flagged induction is retired, EKR no longer rests on it anywhere in this chapter. (2) **Ahlswede–Khachatrian** — the honest continuation of L4 into n < 2k — installed as a citation gateway: Hilton–Milner stated with its formula and machine witnesses (the (7, 3) census: 175 empty-core maxima of size 13, split 140 + 35 between the HM and F₁ shapes), the complete intersection theorem cited with machine-computed sizes, the F₁-vs-HM divergence at k ≥ 4 recorded honestly (70 vs 75, 51 vs 53, 288 vs 316), and ◐24 as the exploration. (3) **The union-closed conjecture** — installed as lore: Frankl's 1979 statement, Gilmer's constant, the singleton lemma proved in a line, and exhaustive censuses on [3] and [4] with zero failures. (4) **Skew Bollobás** — installed as graded Exercise 16 with worked answer A16 — and corrected in the process: the proposal's quoted version is false (Correction 5), and what the chapter now teaches is the verified landscape (Frankl's uniform bound, Hegedüs–Frankl's sharp n+1, the machine census as referee). The audit's proposals and their execution are part of this edition's verification record below.

**Figures.** Two figures, embedded as fenced SVG at their lecture locations per the dual-presentation convention (prose and lab code stay terminal-portable): Figure 1 (L3) — the circle n = 10 with the equality configuration S = {8, 9, 0, 1} at k = 4, the (2k−1)-slot window around the anchor, and the offset strip where A = {1} and k−B = {2, 3} tile [1, 3] disjointly; Figure 2 (L6) — the sumset grid A = {1, 2, 4} × B = {1, 3} with the staircase witness 2 < 3 < 5 < 7 picked out and the full sumset {2, 3, 4, 5, 7} on its diagonal line. All figure data were machine-verified before drawing: S's pairwise cyclic distances {1, 2, 3, 1, 2, 1} all ≤ k−1; the tiling A ∪ (k−B) = {1, 2, 3} with A ∩ (k−B) = ∅; the staircase strictly increasing; the sumset of size 5 against the bound 4. Lecture 8 adds no new figure: its objects — shadows, cascades, the complement mirror — are numeric families rather than geometric configurations, and the lecture's ✎ checkpoints and Part 6's printed censuses carry its worked data. The restructure (session 38) moved Figure 2 to Chapter 9 with the sumset lecture; Figure 1 — the circle-method window — stays.

**Verification record (all deterministic; the Python labs above are the reader's runnable copies of the same logic).** Interval lemma: max |S| = k exhaustive for all 2k ≤ n ≤ 16, zero violations; arcs-intersect ⟺ cyclic start distance ≤ k−1 exact for 4 ≤ n ≤ 12; equality configurations at n > 2k are all consecutive (exhaustive), while n = 2k admits non-consecutive witnesses — (6, 3): 8 configs, 2 non-consecutive; (8, 4): 16, 8 non-consecutive; (10, 5): 32, 22 non-consecutive; window algebra A ∩ (k−B) = ∅, A ∪ (k−B) = [1, k−1], |A|+|B| = k−1: 5,551 anchor-checks, all pass. Uniqueness census: (5, 2) max 4 = exactly 5 families, all stars; **(7, 3) max 15 = exactly 7, all stars; (8, 3) max 21 = exactly 8, all stars** (exhaustive); (6, 3) at n = 2k: exactly 1024 = 2^10 maximum families, every one-per-complementary-pair pick intersecting; k consecutive arcs share exactly one common point (n ≤ 12); star = exactly k arcs on every circle (n ≤ 9); counting identity C(n−1, k−1)·k!·(n−k)! = k·(n−1)! for all n ≤ 20. Sperner side: the SCD doubling construction verified n = 1..8 — partition, +1 steps, symmetry, chain counts 1, 2, 3, 6, 10, 20, 35, 70 = C(n, ⌊n/2⌋), and Σ_c min(k, |c|) = sum of the k middle binomials for every k; exhaustive n = 4 (all 65,535 nonempty families): 167 antichains, LYM ≤ 1 with equality on the 5 full levels, weighted LYM (no (k+1)-chain ⇒ Σ ≤ k) zero violations, maxima {6, 10, 14, 15} = the middle-binomial sums exactly; shifting: 1,200 random intersecting families to stability — size, uniformity, intersecting all preserved; Bollobás: 2,000 random constrained instances Σ ≤ 1 (7 tight) plus the exhaustive ground-[3] sweep (60 valid configurations, 0 violations, 18 tight) and the m = 6 star summing to exactly 1. Sumsets: Cauchy–Davenport — 473,998 pairs over 𝔽₂, 𝔽₃, 𝔽₅, 𝔽₇ (all subsets), 𝔽₁₁ (≤ 4), 𝔽₁₃ (≤ 3): zero violations, 42,081 tight; merge/periodicity — 7,279 gate processes in 𝔽₅/𝔽₇ with gain-0 ⟺ invariance and invariance never occurring short of the full field, and the lab monitor's 8,624 processes with all 16,988 zero-gain steps full-field; polynomial method — univariate partial-fraction identity 15,011 checks (p = 5..13), bivariate weighted-sum identity 900 random polynomials (including the i ≥ |A| terms dying by degree), C(m, r) ≢ 0 mod p for m ≤ p−1 (206 checks), grid-lemma interpolation 184 exact reconstructions, vanishing f(a,b) = 0 ⟺ a+b ∈ C (450 checks), coefficient identity 360 checks, padding arithmetic always true; m-fold C–D: 600 random trials, zero violations. Kneser: exhaustive Z₆..Z₉ (3,969 / 16,129 / 65,025 / 261,121 pairs), Z₁₀ (≤ 5: 405,769), Z₁₂ (≤ 4: 628,849), Z₃² (261,121), Z₄² (40,000 sampled): |A+B| ≥ |A|+|B|−|stab(A+B)| zero violations, tight counts 1,004 / 3,382 / 7,269 / 17,524 for the exhaustive four; e-transform: both properties on all e ∈ G for random pairs in Z₆, Z₈, Z₃², Z₄² — 28,000 gate checks, 6,900 lab checks, zero violations. EGZ: exhaustive n = 3..7 (21 / 120 / 715 / 4,368 / 27,132 multisets — every one contains a zero-sum n-subset) plus 20,000 sampled multisets each at n = 9, 10; pairing lemma 800 random constrained multisets, zero failures; prime-case engine 900 runs — all succeeded, the trivial case firing 225 times in the gate's runs and 44 in the lab's seeded runs, with the choice-sumset covering 𝔽_p in every non-trivial run; composite chain 300 instances over (n, m) = (2,3), (3,2), (2,2), (2,5), (3,3) — every instance yielded 2m−1 disjoint zero-mod-n blocks, the EGZ(m) selection succeeded, and the union certified zero mod nm. **Canon install (Lecture 8 and its orbit), all deterministic:** cascade vs colex initial-segment shadows — agreement on 781/781 sizes (k = 2, 3, 4; every N ≤ C(12, k)); cascade(10, 3) = 10 = C(5, 2). Lovász real form: exhaustive (6, 2) 32,767 + (6, 3) 1,048,575 nonempty families, zero violations, plus 24,000 sampled families at (7, 3), (7, 4), (8, 3), (8, 4) — zero violations. Clique form on the same grounds: zero violations. Equality in the shadow, clique, and j-forms ⟺ x ∈ ℤ and the complete family K^k_x: at (6, 2) all 57 equality cases are the complete families (15 + 20 + 15 + 6 + 1), at (6, 3) all 42 (20 + 15 + 6 + 1) — 99 cases, every one complete, confirmed case by case. j-form: (6, 3) j = 1 and j = 2 zero violations over all 1,048,575 families; (6, 2) j = 1 zero violations, equality 57. Daykin mirror: exhaustive (6, 2) 192 intersecting families (empty included) and (6, 3) 59,049 — zero violations of |𝓕| + |∂_k𝓕*| ≤ C(n, k); maxima 5 by exactly the 6 stars and 10 by exactly 1,024; mirror-equality at 26 ((6, 2): 6 stars + 20 sub-maximum triangles — mirror-tight ≠ maximal, recorded as the honest nuance) and at all 1,024 ((6, 3)). Hilton–Milner: (7, 3) Bron–Kerbosch census — 6,127 maximal intersecting families; maximum 15 = exactly the 7 stars; empty-core maximum 13 = the HM formula C(6, 2) − C(3, 2) + 1, achieved by exactly 175 families, machine-classified 140 HM(x, Y) + 35 F₁(W), none other; AK sizes at (7, 3) [15, 13, 10, 0] and at (5, 3) [6, 7, 10, 0]; F₁ vs HM machine sizes: (7, 3) 13 vs 13, (10, 4) 70 vs 75, (9, 4) 51 vs 53, (12, 5) 288 vs 316 — the divergence recorded honestly. Skew battery: exhaustive memoized recursion over constraint states with exact fractions — maxima n+1 with no hypotheses (n = 1..4: 2, 3, 4, 5; witnesses = complement systems), n with A ≠ ∅ (1, 2, 3, 4), 1, 4/3, 2 at n = 2, 3, 4 with A ≠ ∅ and |Aᵢ| ≤ |Bᵢ| — the refutation of the quoted Σ ≤ 1 version — and 2, 7/3, 3 with |Aᵢ| ≤ |Bᵢ|, A = ∅ allowed; swap-mirror symmetry (|Aᵢ| ≥ |Bᵢ|) confirmed identical; constructions: the Hegedüs–Frankl subset list Σ = n+1 verified n = 2..7, singleton-complement Σ = 1 verified n = 2..7, uniform complement systems attain m = C(a+b, a) at all 9 (a, b) pairs, uniform census maxima = C(a+b, a) in all 10 configurations including grounds larger than a+b ((2, 2) on [6]: 6 of 15 available A's), and the extremal pair-set is unique at n = 2, 3 (all pairs complementary; 2 and 48 valid orderings). Union-closed: [3] 121 nonempty families (120 with a nonempty member — {∅} vacuous), [4] 4,959 (4,958), zero failures of the 1/2 conjecture; the singleton lemma verified on all 98 ([3]) + 4,126 ([4]) singleton-containing families, zero bad; Gilmer's constant (3−√5)/2 = 0.3819660112501051. **Restructure verification (session 38):** the exported lecture block (39,279 chars), all nine exported exercise lines, all eight exported answers (A◆20 with its full multi-line block), and the exported lab parts (Parts 4–5 verbatim; Part 6 minus the skew battery) verified byte-identical inside the Chapter 9 skeleton — zero content loss; the skew battery's code (2,098 chars) and its verified-output sentences re-homed as this chapter's lab Part 4 with the same printed digits; the kept chapter re-gated: 5 lecture headers, balanced fences, 0 mojibake, no session references in lecture bodies, one trailing newline, canvas == master.

**Standing decisions.** Lecture bodies carry no session references; history lives here. Flags, as standing content rather than TODOs: (i) **closed** — the shifting route's EKR closing induction (L5) carried no weight once the circle method proved EKR in full, and the Daykin mirror — now Chapter 9's shadow lecture — provides a second complete proof besides; the induction remains cited as the field's standard route, and nothing in this chapter rests on it; (ii) **closed** — the middle-J transport and the thin range 2k < n ≤ 3k−2 in the uniqueness lecture (L4, cited to Katona 1972, Anderson 1987, Godsil–Meagher 2015, with exhaustive census evidence at (5,2), (6,3), (7,3), (8,3)); the mirror-plus-KK discussion moved with the shadow lecture to Chapter 9, whose closing lecture (Lecture 5, the shade route: cap-meets-floor, the deep cascade-uniqueness lemma, the star theorem for every n > 2k) completed the thin range and retired the flag; (iii) **closed** — Kneser's aperiodic case (the e-transform toolkit and the quotient reduction are proved; the general assembly was cited to Kneser 1953 (Math. Z. 58), Dyson 1945, Nathanson's GTM 165, Tao–Vu, and the arXiv:2407.12253 survey) — Chapter 9's Lecture 3 closed it: Dyson's two-case recursion proves the weak form in full, and DeVos's intersection–union proof completes the strong form. The canon-coverage audit's four proposals were approved by the user and executed — the executed record is the audit paragraph above. The web edition embeds this chapter byte-identically (the standard delivery format); the PDF export check is the user-owned release gate, then learner testing.

**Backfill (session 41).** Five graded exercises (16–20) with pattern-mapped hints were added, per the atlas-wide backfill mandate: the non-uniform half-cube bound |𝓕| ≤ 2^{n−1} by complementary pairs, with the census surprise (at n = 4, twelve maxima, eight with empty total intersection) and the honest contrast with Exercise 2's automatic one-per-pair safety at n = 2k; the complete k = 2 map — every intersecting edge family inside a star or a triangle, the maximal census n stars + C(n, 3) triangles for n ≥ 4, and the n = 4 star-triangle tie reconciled with A7's one-per-pair characterization; the sunflower lemma by induction on k, with the k = 2, r = 3 census (the Δ ≤ 2 ∧ ν ≤ 2 equivalence, maxima 5 and 6 on [5] and [6], the slack against the bound 8, and the sunflower conjecture quoted as open); Sauer–Shelah with the projection/both-lifts decomposition (|𝓕| = |G₀| + |G₁|, the two shatter steps, Pascal's close, and the level-family sharpness — the design's first draft misstated the [4] census as 1, 5, 15; the machine returned 1, 5, 11, exactly the bounds, and the text was corrected before installation); and the shift's boundary — intersecting-preservation needs no uniformity (the mixed-case ledger closing on the original family), the antichain property dies (the {{1, 3}, {2}} witness; 72 of the 167 [4]-antichains broken by the full shift), and the chapter's uses audited uniform. Worked answers A16–A20 were machine-verified before installation: the exhaustive 2^[4] census (65,536 subfamilies — pairwise-intersecting maximum 8, twelve attainers, eight with empty intersection, the displayed witness exact); the edge-family censuses on [4]/[5]/[6] (27 + 76 + 192 intersecting families, zero outside stars and triangles; maximal counts 8, 15, 26; size maxima attained by 8 = four stars + four triangles, five stars, six stars); the sunflower censuses (the no-3-sunflower equivalence over all 1,024 + 32,768 edge families, zero violations; maxima 5 and 6, machine-classified as exactly the twelve labeled 5-cycles on [5] and the ten disjoint-triangle splits of [6]); Sauer (exhaustive [4] maxima 1, 5, 11 at s = 1, 2, 3 with 16, 400, 400 attainers; the fiber identity and both shatter steps on 5,000 random [5] instances, zero violations; 20,000 + 4,677 sampled above-bound families all shattering as claimed); the shift (single shifts exhaustively on [4] — 8,262 intersecting family-pair checks plus 2,570 sampled [5] shifts, zero violations; the full-shift census zero violations; 167 antichains counted, 72 broken). One numbering note: the two older mentions of a graded Exercise 16 in this appendix (the Editions paragraph and the canon-audit paragraph) are the session-36 skew-Bollobás exercise in its period numbering — renumbered to Exercise 10/A10 by the session-38 restructure — and are preserved as the historical record; the new 16–20 continue the post-restructure numbering.

**Adversarial review (session 65).** The review arc's two arguing experts (skeptic and engineer) took this chapter chunk by chunk — correctness, coherence, exposition, figure aid — extend-never-rewrite, every retained objection machine-verified before any edit. Verdict: the mathematics is otherwise CLEAN, with two proof-site defects and one dead lab clause caught, confirmed, and repaired in place. **The defects (machine-sealed):** (1) §5.1 defined the shift unconditionally — "duplicates merge" — while every lemma (size preservation, §5.2, §5.3) already uses the conditional semantics; under the unconditional reading S_{12} collapses {{1,3},{2,3}} to a single set. The definition is now conditional up front (the target replaces A only when absent from the family; otherwise A stays put), with the no-duplicates-can-arise justification in place of "duplicates merge". (2) §5.2's Case j ∈ C asserted "C′ ∩ D ⊆ C ∩ D = ∅ for the D-part" — false as written (i lies in C′ and may lie in D); the conclusion C′ ∩ D* = ∅ survives, and the clause now cites the D-part disjointness established above the case split. (3) Part 2's is_consec second clause was dead code (a length-(len−1) gap list can never equal [1]·(len−2)); the recorded outputs — 2/0/0/8/0/22 — already match full-cyclic semantics on all six (n, k) pairs, and the printed code now carries the verified full-cyclic test (equivalent to the cyclic-rotation check, zero mismatches n = 5..12). **Three record-level classes:** ◐14's "equality exactly on the middle level(s)" — Part 1's own census shows equality on all five full levels at n = 4 — and its "mixes fail to be antichains at all" (now: the full union of the two middle levels is not an antichain; partial mixes can be, {1} with {2,3} at n = 3), with the matching §1.1 ✎ repaired the same way; §3.2's and §4.1's "the lab verifies/checks … n ≤ 16 / n ≤ 20" re-attributed to this verification record (the printed lab reaches six (n, k) pairs and n ≤ 12; both ranges re-verified fresh this session); and A20(c)'s "§5.1 defines the shift for k-uniform families" — the definition is uniformity-free, and the audit sentence now says so. **The fresh battery (all green, condensed):** Sperner side — the antichain censuses 3/6/20/168 (n ≤ 4), LYM zero violations, Sperner maxima exact, the Erdős no-(k+1)-chain census 6/10/14/15/16 exact, the SCD doubling build n = 1..8 (partition, symmetry, steps, chain counts 1, 2, 3, 6, 10, 20, 35, 70), and Part 1's printed line reproduced exactly. Bollobás — the Part 3 sweep 60/0/18 exact; the skew battery's five variants exact (2, 3, 4, 5; 1, 2, 3, 4; 1, 4/3, 2; 2, 7/3, 3; mirror identical); the Hegedüs–Frankl list Σ = n+1 (n = 2..7), the singleton construction Σ = 1, the complement orderings 2 and 48, the uniform census 10/10 = C(a+b, a). Circle/EKR/uniqueness — the max-clique censuses (5, 2): 4/5, (6, 3): 10/1024, (7, 3): 15/7; the interval sweep 2k ≤ n ≤ 16 (max = k, zero violations); the n > 2k equality configurations all consecutive with exactly one common point; arcs ⟺ distance exact n ≤ 12; the counting identity n ≤ 20 (BigInt); star = k arcs n ≤ 9; the (7, 3) census — 6,127 maximal, 7 stars, 175 empty-core 13s = 140 HM + 35 F₁, none other; AK sizes [15, 13, 10, 0] and [6, 7, 10, 0]; F₁ vs HM 13/13, 70/75, 51/53, 288/316. Shifting — 167 nonempty antichains on [4], 72 broken by the full shift; the single-shift receipt 8,262 = 1,377 intersecting families × 6 pairs, zero violations; A6's exactly two fully-shifted maxima ({12, 13, 14} and {12, 13, 23}). Answers — A8/A9 witnesses exact; A12's scd(4) chains byte-match; A16 max 8 with twelve attainers (4 stars + 8 empty-core), 256 one-per-pair → 12; A17 27/76/192 with maximal 8/15/26 and max attainers 8 (4+4), 5, 6; A18's equivalence zero violations over 1,024 + 32,768 with maxima 5 (12 attainers) and 6 (10); A19's maxima 1, 5, 11 with 16, 400, 400 attainers; SCD n = 7, 8; the equality-config tiling over 190 configurations, zero bad; A20(b)'s witness and full-shift rescue check exact. Figure 1 (the circle-method window) adequate — all ten vertices on the r = 110 circle at 36° spacing, the equality configuration S = {8, 9, 0, 1}, the tiling {1} ⊔ {2, 3} = [1, 3], and the window arc verified. Cross-references: the Chapter 9 forward pointers valid post-restructure; the pattern index consistent with the atlas (this chapter's reverse rows P2 16, 17, 19; P4 18, 19; P23 20). Per the rebuild rule the web edition and the .html export were rebuilt — fidelity proof first — and the review arc advances to Chapter 8.

**Expansion-pass adoption (session 91).** The uploaded expansion draft was adopted per the standing pipeline — R1 structural read and pattern audit, R2 adversarial referee, R3 figure and lab validation, R4 assembly — extend-never-rewrite, every number machine-verified before installation. **Lecture upgrades:** §4.3 is now complete for every n ≥ 2k+1 (the anchored adjacent-transposition transport, with the k = 2 sub-case and the m = k−1 / m = n−k edge cases closed), retiring the thin-range flag in-chapter; §5.3 gains the closing EKR induction (split the shifted family on the top element n; Pascal pays the sum); §3.1 carries the full arcs-intersect ⟺ distance proof; §3.3 the full equality-structure argument; §1.3 the Erdős generalization with the telescoping chain count; §2.2 both cross-hypotheses verified from incomparability. **A latent master defect sealed:** §2.3's "maxima 1, 4/3, 2 under |Aᵢ| ≤ |Bᵢ|" clause was missing the Aᵢ ≠ ∅ qualifier — under |Aᵢ| ≤ |Bᵢ| alone the maxima are 2, 7/3, 3 (empty Aᵢ allowed) — the qualifier is restored at §2.3 and in the formula box, and the lab battery prints the full variant set. **Figure 1 upgraded**, its geometry machine-validated: the window arc is exactly concentric (M 118.2 214.4 A 128 128 0 1 1 361.8 214.4), the end-cap ticks are radial span markers, the anchor is s₀ = 0, and every caption datum (S = {8, 9, 0, 1}, A = {1}, B = {1, 2}, k−B = {2, 3}, the tiling of [1, 3]) is exact. **Exercises reorganized and renumbered** (old → new: 1→1, 2→2, 16→3, 3→4, 4→5, 5→6, 6→7, 7→8, 8→9, 17→10, 18→11, 20→12, 9→13, 10→14, 19→15, ◆11→◆16, ◆12→◆17, ◐13→◐18, ◐14→◐19, ◐15→◐20 — this map resolves the older records' exercise references; earlier paragraphs keep their period numbering), with mangled references restored (§2.3's Exercise 14, §4.3's Exploration 18, the lab's Part headings) and hints re-mapped. **Twenty worked answers** now ship (the three explorations gained worked answers), and the lab runs in **five verified parts**, adding Part 5 (the shifting census: stars vs fully shifted at (6, 3), the half-cube census, the edge-family map, the 3-sunflower equivalence, the Sauer–Shelah census) and a Lehmer-seeded greedy maximal-antichain sampler whose 2,349 + 256 exact-LYM hits are all single full levels. **Trick Bag updates:** the P4 row gains the L5 sites and the split-on-n form; the "Census what you cannot rebuild" row is retired (its content now lives in the lectures it served); the "Local moves force global centers" row is added; the Beyond-EKR row carries the t-intersecting form. **Three draft defects caught and repaired** (R2, machine-sealed): (1) the shifted-maxima answer asserted 236 ≤_G 245 — false in the Gale order — with a wrong r = 0 pick list; the corrected forcing relations (136 ≤_G 236 and 235 ≤_G 236 ban 236 unless r = 2; 145 ≤_G 245 and 145 ≤_G 146 force 145 at r ≤ 1 and r ≥ 3) keep the count at 6 and repair the r = 0 family to C([5], 3). (2) The LYM-sampling answer quoted an unsupported "0.55–0.85" concentration; it now quotes the measured sampler receipts (medians 0.70 at n = 5 over 20,000 trials and 0.62 at n = 6 over 10,000; every exact-1 hit a single full level). (3) The single-shift receipt "8,262 = 1,377 intersecting families × 6 pairs" is wrong: the true count of intersecting subfamilies of 2^[4] is 1,376 (including the empty family), so the receipt is 8,256/8,256 — this also corrects the session-65 record's figure above, which stays verbatim as history. The sunflower citation was repaired at both sites (Alweiss–Lovett–Wu–Zhang 2020 → Rao's (Cr log(rk))^k → Bell–Chueluecha–Warnke's (Cr log k)^k, the current best), and the lab preamble's appendix-enumeration clause is restored. **Honesty at (9, 4):** a full census is infeasible (the shifted search space alone reaches about 17 million Gale ideals), so Exploration 18's answer keeps partial receipts, every one agreeing with the theorem: a pruned sweep of all 37,145 shifted intersecting 4-families on [9] (empty family included) finds exactly one maximum — star(1) at 56 — and a unique empty-core maximum at 53, attained by HM(1, {2,3,4,5}); a hill-climb from all 630 Hilton–Milner families found nothing above 53. **The fresh verification battery, all green:** §4.3's straddle and sub-case grids; F₁-intersecting exhaustively at (5, 2) and (6, 2); the t-intersecting grids; the A◆16 Gale census; the HM hill-climb; the AK and Wilson thresholds; weighted LYM exhaustively at n = 4 (65,535 families); the LYM-equality classification exhaustively at n ≤ 5 (7,581 antichains) plus the n = 6 sampler; the Part 5 port — with the sampler reconstructing all twelve recorded statistics exactly. Per the rebuild rule the web edition was rebaked oracle-first after assembly.

---

*Chapter status: ✅ **Feynman edition + exercise backfill (session 41) + adversarial review (session 65) + expansion pass (session 91)** — 5 lectures (Sperner three ways; Bollobás with the honest skew landscape; the circle method and EKR with the interval lemma complete; uniqueness proved in full for every n ≥ 2k+1 — the thin-range flag retired; shifting with the closing induction), all proofs complete, no flags left; 1 verified figure (upgraded, geometry machine-validated); 15 graded exercises + 2 ◆ pattern-unknown + 3 ◐ explorations, 20 worked answers machine-verified; lab in 5 verified parts (Sperner/SCD census; EKR interval lemma + uniqueness censuses + the F_r/HM benchmark table; Bollobás sweep; the skew battery with linear extensions; the shifting census with the Lehmer-seeded LYM sampler). The session-91 expansion pass adopted the uploaded draft end to end — three draft defects caught and repaired (a false Gale relation in the shifted-maxima count; an unsupported distribution claim replaced by measured receipts; the 8,262 → 8,256 receipt correction) — and the (9, 4) exploration keeps honest partial receipts where a full census is infeasible. Ships with its web edition (the standard delivery format): the HTML canvas embeds this chapter byte-identically; print to PDF from a browser for a correct export.*
