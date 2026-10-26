---
name: "cgt-ch16-symmetry-design"
title: "Ch. 16 — Symmetry, Inversion, and Design (A Lecture Course in the Feynman Style)"
type: "text/markdown"
---

# Chapter 16 · Symmetry, Inversion, and Design

*Part of the Combinatorics & Graph Theory Atlas (see the Atlas canvas for the chapter map and progress report).*

Chapter 2 planted a seed you have been carrying ever since. Cayley's formula says n^{n−2} trees grow on n labeled vertices — and then the exploration X1 asked: how many *shapes*? Not trees, tree *types* — two trees counted once if some relabeling carries one onto the other. The labeled count explodes; the shape count limps along as 1, 1, 1, 2, 3, 6, 11, 23. The exploration named the tool that answers such questions — **Pólya's machine** — and deferred it. This is the chapter where the debt is paid. **Symmetry** (Lectures 1–2) is the discipline of counting *orbits* — objects up to relabeling, colorings up to rotation, molecules up to the symmetries of their frame — and it comes in two acts: Burnside's lemma averages a group over its fixed points, and Möbius inversion runs the same averaging idea backwards, recovering the individual counts that a pile of sums has smeared together. **Design** (Lectures 3–4) is the second half: combinatorial objects — Steiner triple systems, projective planes, the schoolgirls' walking schedule — whose existence is governed by pure *arithmetic divisibility*. The through-line is a counting question asked three ways: when you average over symmetry, what are you really counting; when you invert an average, what survives; and when you demand that every pair of points sit in exactly one block, which universes of points are even possible? **Codes** (Lectures 5–6) close the circle: the error-correcting codes of Chapter 8 return with their Singleton and Plotkin bounds, and the Golay codes — the best single page in coding theory, Berlekamp called their 1949 announcement — turn out to *be* designs in disguise: their weight supports are the Witt systems S(4,5,11), S(5,6,12), and S(5,8,24), whose automorphism groups are the sporadic Mathieu groups.

The deal with the reader is the one the Atlas has enforced since Chapter 1: every number printed below was machine-verified before printing — exhaustive orbit censuses, complete Steiner-system searches (STS(13) = 2 proved by a machine run that visited all 41,621 search states), perfect-code partitions checked word by word — and where a statement is a conjecture, a proof is cited rather than given, or a count is beyond the chapter's computational reach, the text says so in those words.

## How to read this chapter

Nothing here needs beyond Chapter 2 (labeled versus unlabeled graphs, Cayley's formula, the tree-shape exploration X1), Chapter 6 (you met Fisher's inequality there, proved twice — the Gram-determinant route and Bose's dimension argument), and Chapter 8 (the Hamming cube, the [7,4] code, Delsarte's linear program). All group machinery is defined in place; the only group we ever enumerate in full is the rotation group of the cube. Lines marked **✎ Checkpoint** are the places to stop and predict — commit to a guess, in ink, before reading on. Exercises are graded ●○○ *easy* (one idea, applied directly), ●●○ *moderate* (two ideas, or one tricky step), ●●● *tough* (several ideas combined); ◆ **pattern unknown** problems come with no hint — diagnosing the tool is part of the problem; ◐ **Explorations** are open-ended investigations that state what you should find, not a number to match. Worked answers sit at the end; hints travel with the problems.

Notation. A **group action** of a group G on a set X is a map G × X → X, written g·x, with e·x = x and g·(h·x) = (gh)·x; the **orbit** of x is G·x = {g·x : g ∈ G}; X/G is the set of orbits, and Fix(g) = {x : g·x = x}. A **cycle type** is the multiset of cycle lengths in a permutation's disjoint-cycle decomposition; c(g) is its number of cycles. The **cycle index** of an action on n points is the polynomial Z_G(x₁,…,x_n) = (1/|G|)·Σ_{g∈G} x₁^{c₁(g)}···x_n^{c_n(g)}, where c_i(g) is the number of i-cycles in g. A **poset** (P, ≤) is a partially ordered set; μ(x,y) is its **Möbius function**, defined by μ(x,x) = 1 and Σ_{x≤z≤y} μ(x,z) = 0 for x < y. A **t-(v,k,λ) design** is a v-point set with a family of k-subsets (**blocks**) such that every t-subset of points lies in exactly λ blocks; **Steiner system** S(t,k,v) = a t-(v,k,1) design; b = number of blocks, r = number through a fixed point; a design is **resolvable** when its blocks partition into parallel classes, each class partitioning the point set. A **projective plane** of order q is a design with q²+q+1 points, q+1 points per line, any two points on exactly one line (so S(2, q+1, q²+q+1)). A **[n,k,d]_q code** is a q-ary code of length n with q^k codewords and minimum distance d; MDS = meeting the Singleton bound d = n−k+1; A_q(n,d) is the largest size of any q-ary (n,d)-code.

The chapter's machine runs follow the Atlas's standing rule: exhaustive where feasible (every orbit census cross-checked against a brute-force canonicalization; the S(2,3,6) non-existence verified over all 15,504 candidate block-sets; the Kirkman schedule checked line by line), and every search recorded so it can be replayed exactly.

## The pattern map for this chapter

| Pattern | Plain language | Where it fires |
|---------|---------------|----------------|
| **P10 Averaging / expectation** | The average is a promise; some object beats it | L1 (Burnside: the average of fixed points IS the orbit count — averaging as an exact identity, not an estimate) |
| **Symmetry averaging (new this chapter)** | To count objects up to symmetry, average the fixed points of the symmetry | L1 (necklaces, the colored cube, tree shapes — the debt to Chapter 2's X1 paid); proposed to the Atlas pattern registry at ship |
| **Möbius inversion (new this chapter)** | Sums hide individuals; run the sieve backwards to recover them | L2 (τ, φ, the partition lattice; Rota's incidence algebra); proposed at ship |
| **Double-counting / divisibility (new this chapter)** | Count one thing two ways; integrality is existence's admission fee | L3–L4 (Fisher's inequality b ≥ v; the v ≡ 1, 3 mod 6 gate; S(2,3,6) impossible at r = 5/2; Keevash's divisibility conditions); proposed at ship |
| **Words-as-designs (new this chapter)** | A code's constant-weight words carry a t-design on their supports | L6 (759 octads = S(5,8,24); 132 weight-6 supports of the extended ternary Golay = S(5,6,12); Assmus–Mattson); proposed at ship |

---

## Lecture 1 · The Orbit-Counting Machine: Burnside, Pólya, and the Shapes of Trees

### 1.1 The question Chapter 2 left open

Cayley's formula counts trees on *labeled* vertices: 16 of them at n = 4, 125 at n = 5, 1,296 at n = 6, 16,807 at n = 7. But the number of *shapes* — unlabeled trees, isomorphism classes — is 2, 3, 6, 11 at those sizes. The labeled count is a pile of copies: every shape on n vertices contributes exactly n!/|Aut(shape)| labelings (its automorphisms fold labelings onto each other), so the labeled world and the shape world are related by a sum you cannot read backwards:

n^{n−2} = Σ_{shapes S} n!/|Aut(S)|.

Two shapes with different automorphism groups contribute differently, and nothing about the equation lets you pull the shape count out. What is missing is a machine that counts *orbits* — equivalence classes under a group action — directly. Burnside's lemma is that machine, and it is almost embarrassingly simple once you see the double counting that powers it.

### 1.2 Burnside: averaging as an exact identity

**Lemma (Burnside — actually Cauchy 1845, Frobenius 1887; Burnside popularized it in his 1897 textbook, always with credit to Frobenius).** For a finite group G acting on a finite set X, the number of orbits is the average number of fixed points:

|X/G| = (1/|G|) · Σ_{g∈G} |Fix(g)|.

**Proof.** Count pairs (g, x) with g·x = x, two ways. Summing over group elements gives Σ_g |Fix(g)|. Summing over points gives Σ_x |Stab(x)|, and each point's orbit has size |G|/|Stab(x)| — the cosets of its stabilizer — so the points of one orbit contribute |G| in total. Orbits therefore each contribute exactly |G| to the second sum, and dividing by |G| counts orbits. Both sums equal, divide, done. ∎

This is Stigler's law in its purest form — the lemma that is not Burnside's — and the proof shows why the averaging works: it is not an estimate, it is bookkeeping. The orbit count falls out of a double count of pairs.

**✎ Checkpoint.** Before computing anything: 2-color necklaces of length 4, beads on a loop up to rotation. Predict how many there are, then check that the naive guess "2⁴/4 = 4" is close but has the wrong denominator. Where does the rotation group of a 4-loop fail to have every orbit of size 4?

The machine: the rotation group C₄ acts on the 16 colorings. The identity fixes 16; the rotations by one and three beads fix only the 2 constant colorings; rotation by two fixes 4. Burnside: (16 + 2 + 4 + 2)/4 = 6. The answer 6 — not 4 — is the orbit count, and the all-white and all-black necklaces are exactly the orbits whose small stabilizers made the division naive. Run the same computation for n = 1..12 and the census is **2, 3, 4, 6, 8, 14, 20, 36, 60, 108, 188, 352** — each value machine-checked two ways in this chapter's lab: brute-force canonicalization of every one of the 2^n strings against the same formula (1/n)·Σ_k 2^gcd(n,k), agreement at every n.

### 1.3 Pólya: the cycle index turns the lemma into a polynomial

Burnside's sum demands |Fix(g)| for each group element, and for coloring problems that is a one-liner: a coloring is fixed by g exactly when it is constant on each cycle of g, so a k-coloring has k^{c(g)} fixed colorings, c(g) the cycle count. Substitute and you have **Pólya's enumeration theorem**:

# orbits of k-colorings = Z_G(k, k, …, k), where Z_G(x₁,…,x_n) = (1/|G|)·Σ_{g∈G} ∏_i x_i^{c_i(g)}.

The polynomial Z_G — the **cycle index** — is worth computing once and keeping: it answers the coloring question for every k at the same time. (History's honest note: J. H. Redfield published the essence of this in 1927, in a paper so obscure that Pólya's 1937 independent rediscovery — motivated by counting chemical isomers — gave the theorem its name; "Redfield–Pólya" is the fair hyphenation.)

**The cube.** Color the six faces of a cube with k colors, up to rotation. The rotation group of the cube has 24 elements — machine-verified in this chapter's lab by generating the closure of two quarter-turns — with five cycle types on faces, machine-tallied as 1⁶:1, 2²1²:3, 2³:6, 3²:8, 4·1²:6 (identity; 180° turns about face axes; 180° turns about edge axes; 120° turns about vertex axes; quarter-turns about face axes — the counts sum to 24). A coloring fixed by a rotation is constant on each cycle, so each type contributes k^{#cycles}: k⁶, k⁴, k³, k², k³ respectively, and the cycle index collapses to

(k⁶ + 3k⁴ + 12k³ + 8k²)/24,

and for k = 1, 2, 3, 4, 5 the counts are **1, 10, 57, 240, 800** — every value machine-verified against brute-force canonicalization of all k⁶ labeled colorings under all 24 rotations. Pólya's original motivation was exactly this kind of question — counting chemical isomers, where a molecule's mirror-symmetric carbon framework turns equivalent labelings into one compound — and the closed form explains at a glance why the count at k = 2 is 10 rather than anything near the naive 2⁶/24: the two constant colorings ride through all 24 rotations fixed, inflating their orbits' share of the average.

### 1.4 Paying Chapter 2's debt: tree shapes by multiset closure

The tree-shape sequence — the X1 counts 1, 1, 1, 2, 3, 6 extended to n = 8 — is not a Pólya application in the direct sense (the "group" would act on an infinite set), but it is the same philosophy: count orbits by building each *exactly once*. The engine that does it is recursive and canonical. A rooted tree of size n is a multiset of rooted trees of sizes summing to n−1, so rooted shapes are generated by multisets of smaller ones, deduplicated by generating multisets in sorted order — every shape produced exactly once, no isomorphism test needed. The unrooted version splits by centroid: a tree has either one centroid (count: rooted multisets of total size n−1 with every branch at most ⌊(n−1)/2⌋) or two (n even: an unordered pair of rooted trees of size n/2), and the two cases are disjoint.

The census, machine-run twice (multiset generation, and full Prüfer-sequence enumeration over all n^{n−2} labeled trees with canonical-form dedup — the two agree at every n): unrooted shapes n = 1..8 are **1, 1, 1, 2, 3, 6, 11, 23**; rooted, **1, 1, 2, 4, 9, 20, 48, 115**. Chapter 2's first six values are exactly the opening of these sequences, and the automorphism-group subtlety that broke the naive division — why 1,296 labeled 6-vertex trees do not divide by 720 into an integer count of shapes — is now visible in the machine: the shapes' |Aut| values range from 2 to 120 and the sum Σ n!/|Aut(S)| = n^{n−2} balances term by term.

### 1.5 What to learn

Symmetry counting is double counting in disguise. Burnside's lemma is proved in two lines by counting pairs; Pólya's theorem packages the fixed-point counts into a polynomial that answers a whole family of questions at once; and the way to generate orbits directly — never produce two representatives of the same orbit, rather than produce and deduplicate — scales to the tree-shape census where the group is too wild to enumerate. The averaging pattern (P10) here upgrades from "some object beats the average" to "the average *is* the answer."

## Lecture 2 · Möbius Inversion: Running the Sieve Backwards

### 2.1 The averaging problem, inverted

Burnside computes one aggregate (the orbit count) from many local counts (the fixed points). Averaging has a mirror problem, and number theory lived in it for a century: every positive integer n carries the divisor sum

Σ_{d|n} 1 = τ(n), the number of divisors of n.

Fine — but suppose you know τ and want something *behind* it. The classic behind-the-scenes function is the Möbius function μ(n), the number-theoretic bellows: μ(n) = (−1)^k if n is a product of k distinct primes, μ(n) = 0 if any prime divides n twice, μ(1) = 1. Its whole job is the inversion formula:

if g(n) = Σ_{d|n} f(d) for all n, then f(n) = Σ_{d|n} μ(d)·g(n/d).

Read it as recovering the individual from the pile of sums. Why does μ do this? Because Σ_{d|n} μ(d) = 0 unless n = 1, when it is 1 — the Möbius function sums to an *identity* over the divisors of any n > 1, which is exactly what an inverse needs. Specifically, first verify the divisor sum Σ_{d|n} μ(d) = [n = 1]: for n = 1, μ(1) = 1; for n > 1 with prime factorization n = p₁^{a₁}···p_r^{a_r} (r ≥ 1), only the squarefree divisors d = ∏_{i∈S} p_i (S ⊆ {1,…,r}) have μ(d) ≠ 0, so Σ_{d|n} μ(d) = Σ_{k=0}^{r} C(r,k)·(−1)^k = (1−1)^r = 0. Then the inversion formula itself is a change of order of summation: substituting g(n/d) = Σ_{c|(n/d)} f(c) and re-indexing the pairs by m = cd (so c | n and d | (n/c)) gives

Σ_{d|n} μ(d)·g(n/d) = Σ_{d|n} μ(d)·Σ_{c|(n/d)} f(c) = Σ_{c|n} f(c)·Σ_{d|(n/c)} μ(d) = Σ_{c|n} f(c)·[n/c = 1] = f(n).

— the whole proof in two displays, machine-checked identity by identity in the lab.

The identity Σ_{d|n} μ(d) = [n = 1] and the sibling identities Σ_{d|n} φ(d) = n and Σ_{d|n} d·μ(n/d) = φ(n) are all machine-verified in this chapter's lab over every n ≤ 10,000 — zero mismatches; spot values: τ(60) = 12, φ(60) = 16, φ(100) = 40.

### 2.2 Rota's move: the poset is the thing

In 1964 Gian-Carlo Rota asked the question that turned a number-theory trick into a combinatorial theory: *where does μ really live?* Answer: on the divisor lattice — the poset of divisors of n ordered by divisibility, where d ≤ e means d | e. Number-theoretic μ(d) is a value attached to the *pair* (1, n) of that poset, filtered through the pairs (d, e) with n/d squarefree. And the definition that generalizes is this:

**Poset Möbius function.** On a finite poset P, define μ(x, y) for x ≤ y by μ(x, x) = 1 and, for x < y,

μ(x, y) = −Σ_{x ≤ z < y} μ(x, z).

The recursion runs upward: to know μ(x, y) you need μ on the interval strictly below y. (Two traps for the implementer, both caught by the lab's own consistency checks: the sum excludes z = y — including it makes the recursion self-referential and silently wrong; and the recursion accumulates from x *upward*, not from y downward.) The inversion theorem is then pure algebra:

**Theorem (Möbius inversion on posets).** Let P be a locally finite poset with minimum element 0̂ (or fix any lower bound x₀ ∈ P). If g(y) = Σ_{x₀ ≤ z ≤ y} f(z) for all y ≥ x₀, then f(y) = Σ_{x₀ ≤ z ≤ y} g(z)·μ(z, y). Dually, if P is finite and h(x) = Σ_{z ≥ x} f(z) for all x ∈ P, then f(x) = Σ_{z ≥ x} μ(x, z)·h(z).

*Proof.* In the **incidence algebra** of P, where convolution of two interval functions α, β is defined by (α ∗ β)(x, y) = Σ_{x ≤ z ≤ y} α(x, z)·β(z, y), the identity element is the Kronecker delta δ(x, y) = [x = y] and the zeta function is ζ(x, y) = [x ≤ y]. By the defining recursion of μ, for any x ≤ y the sum telescopes: (μ ∗ ζ)(x, y) = Σ_{x ≤ z ≤ y} μ(x, z) = [x = y] = δ(x, y) — so μ is the left inverse of ζ, and hence its two-sided inverse in the associative incidence algebra (the same telescoping run downward gives (ζ ∗ μ)(w, y) = Σ_{w ≤ z ≤ y} μ(z, y) = δ(w, y)). Substituting g(z) = Σ_{x₀ ≤ w ≤ z} f(w) and re-indexing the pairs (w, z) with x₀ ≤ w ≤ z ≤ y yields

Σ_{x₀ ≤ z ≤ y} g(z)·μ(z, y) = Σ_{x₀ ≤ w ≤ y} f(w)·Σ_{w ≤ z ≤ y} μ(z, y) = Σ_{x₀ ≤ w ≤ y} f(w)·δ(w, y) = f(y). ∎

ζ is the algebra's identity-shaped zeta function; μ is its inverse, exactly as the Riemann zeta and the classical μ are inverse under Dirichlet convolution. Rota's 1964 paper ("On the foundations of combinatorial theory I. Theory of Möbius functions") made this the founding observation of modern enumerative combinatorics: choose the poset, get a μ, get an inversion.

**✎ Checkpoint.** Before computing: on the Boolean lattice B_k of subsets of a k-set (ordered by inclusion), predict μ(∅, S). Hint: what does inclusion-exclusion look like from inside the incidence algebra?

### 2.3 Three posets, three μ's

- **The divisor lattice** of n. μ(1, n) is the classical Möbius μ(n); μ(d, e) = μ(e/d) filtered as above. The whole of elementary number-theory sieving is one poset.
- **The Boolean lattice B_k.** Every proper extension of the empty set flips sign: μ(∅, S) = (−1)^{|S|} — and more generally μ(T, S) = (−1)^{|S∖T|} for T ⊆ S, proved by induction on m = |S∖T| using Σ_{j=0}^{m} C(m,j)(−1)^j = [m = 0], machine-verified for k ≤ 6 in the lab (all 64 intervals [∅, S] of B_6 checked against the recursion, and the expansion pass's fresh battery re-walked every one of the 4,096 interval pairs (T, S) — zero mismatches). Inclusion-exclusion — the oldest trick in the counting book — is Möbius inversion on B_k; the pattern map's averaging entry and this lecture are the two faces of one coin.
- **The partition lattice Π_n** (set partitions ordered by *reverse refinement*: the single-block whole set is the bottom 0̂, singletons-only is the top 1̂; under dualization to the standard refinement order — singletons at 0̂, the whole set at 1̂ — the value μ(0̂, 1̂) is identical, so the convention costs nothing). This one is genuinely nontrivial: |Π_n| = 1, 2, 5, 15, 52 for n = 1..5, and the machine census of μ(0̂, 1̂) — the Möbius value of the whole lattice, bottom to top — is **1, −1, 2, −6, 24**: that is, μ(0̂, 1̂) = (−1)^{n−1}(n−1)!. To see why, for every n at once: fix a positive integer λ and let g(π) = λ^{|π|} count the λ-colorings constant on each block of π, while f(σ) counts the colorings whose *exact* color-class partition is σ — that is λ(λ−1)···(λ−|σ|+1), since the |σ| classes need distinct colors. A coloring is constant on each block of π exactly when its color-class partition σ is coarser than π (σ ≤ π in our order), so g(π) = Σ_{0̂ ≤ σ ≤ π} f(σ), and Möbius inversion at π = 1̂ reads

λ(λ−1)···(λ−n+1) = Σ_{0̂ ≤ σ ≤ 1̂} λ^{|σ|}·μ(σ, 1̂).

Both sides are polynomials in λ agreeing for every positive integer λ, so their coefficients agree: the coefficient of λ¹ on the left is (−1)^{n−1}(n−1)!, and on the right only the one-block partition σ = 0̂ contributes to λ¹ — so μ(0̂, 1̂) = (−1)^{n−1}(n−1)!, proved. (The classic argument, reproducible from the lab's recursion; the census above is its shadow.)

### 2.4 What to learn

Averaging hides individuals; inversion buys them back. The structure that makes inversion possible is a poset with a μ attached — and once the incidence algebra is in hand, inclusion-exclusion, the divisor identities, and the partition-lattice sign pattern all become one theorem read off three lattices. The "recover what was averaged" pattern is the proposed registry entry; Burnside and Möbius, Lectures 1 and 2, are the two directions of the same coin.

---

## Lecture 3 · Designs I: Steiner's Question, Fisher's Inequality, and the Planes That Cannot Exist

### 3.1 The schoolgirl's diary and Steiner's question

In 1844 Woolhouse posed, in the Lady's and Gentleman's Diary, the problem of arranging triples so that no pair repeats; Kirkman solved the existence question for triples in 1846 (the paper sits in the journal's 1847 volume — cite Kirkman 1846/47), and in 1850 posed his famous walking problem: fifteen schoolgirls, seven days, rows of three, every pair together exactly once *per week*. Steiner asked the abstract version for k-subsets in 1853, unaware of Kirkman, and the objects carry Steiner's name. Definitions:

A **t-(v, k, λ) design** is a v-point set X and a family B of k-subsets (blocks) such that every t-subset of X lies in exactly λ blocks. λ = 1 gives a **Steiner system S(t, k, v)**. For t = 2, k = 3: a **Steiner triple system STS(v)**. Counting constants: a t-design with v points, b blocks, r blocks through a fixed point, satisfies λ·C(v, t) = b·C(k, t) and r·C(k−1, t−1) = λ·C(v−1, t−1) (which for t = 2 gives r = λ(v−1)/(k−1)) — double counting the (block, t-subset) pairs two ways. For an STS: b = v(v−1)/6 and r = (v−1)/2.

**✎ Checkpoint.** Before reading on: v(v−1)/6 and (v−1)/2 must be integers. Which v survive? Predict the congruence class before checking the next paragraph.

### 3.2 The arithmetic gate: v ≡ 1, 3 (mod 6), and the exhibit that cannot exist

Integrality of b and r forces v ≡ 1 or 3 (mod 6). The gate has two leaves, both machine-walked in the lab: r = (v−1)/2 integer says v is odd, leaving v ≡ 1, 3, 5 (mod 6); then b = v(v−1)/6 needs 3 | v(v−1), which fails exactly when v ≡ 2 (mod 3) — that is, at v ≡ 5 (mod 6) — leaving **v ≡ 1 or 3 (mod 6)**. The remarkable theorem (Kirkman's constructions, completed by Bose 1939 and Skolem 1958): **STS(v) exists if and only if v ≡ 1 or 3 (mod 6)** (v ≥ 3) — the arithmetic gate is the *whole* story.

And here is the chapter's worked non-existence exhibit, the one the scope sheet nearly fumbled: **S(2,3,6) does not exist.** The formula gives r = (6−1)/2 = 5/2 — not an integer, so no system. The lab makes this a *machine proof*, not an algebra shrug: over all C(20, 5) = 15,504 candidate 5-block families from the 20 triples on 6 points, exactly **zero** exact covers exist. Divisibility is not a technicality; it is the admission fee, and v = 6 cannot pay.

### 3.3 Fisher's inequality: b ≥ v

For nontrivial 2-designs, block count can never duck below point count:

**Theorem (Fisher 1940).** In a 2-(v, k, λ) design with 2 ≤ k < v and λ ≥ 1, b ≥ v.

Chapter 6 proved this two ways — the Gram determinant of the block incidence vectors (a square v × v Gram matrix NN^T whenever b = v, with det(NN^T) = (r−λ)^{v−1}·(r+(v−1)λ); the Fano-plane instance prints (3−1)^6·9 = 576 = 24²) and Bose's linear-algebra argument. What this chapter adds is the *census view*: Fisher is tight at the bottom and slack immediately above. The Fano plane STS(7): b = v = 7, tight. STS(9) — the machine census finds exactly 840 labeled systems, all isomorphic (one orbit; the affine plane AG(2,3)): b = 12 > 9. The projective plane of order 3 (next section): b = v = 13, tight again — and this is no accident: **the equality case b = v of Fisher is precisely the symmetric designs**, where any two distinct blocks also meet in exactly λ points, duality everywhere.

### 3.4 Projective planes, and the orders that cannot exist

A **projective plane of order q** is a design with v = q²+q+1 points, blocks (lines) of size q+1, every pair of points on exactly one line — that is, S(2, q+1, q²+q+1). Finite field arithmetic builds one for every prime power q: points = 1-dimensional subspaces of F_q³, lines = 2-dimensional ones. The machine instance this chapter carries everywhere is **PG(2,3)**: 13 points, 13 lines of 4 points, every pair on exactly one line (all 78 pairs machine-checked) — an S(2,4,13), Fisher-tight with b = v = 13. The affine plane AG(2, q) — STS(9) at q = 3 — is the projective plane minus a line and its points.

Do planes exist at every order? Here the story becomes one of combinatorics' great campaigns. The order-2 plane (the Fano plane, v = 7) is unique; order 3 unique; and then:

**Theorem (Bruck–Ryser 1949; generalized to symmetric designs by Bruck–Ryser–Chowla 1950).** If a projective plane of order q ≡ 1 or 2 (mod 4) exists, then q is a sum of two integer squares.

The lab runs the census: q = 6 and q = 14 are 2 (mod 4) and not sums of two squares — **no plane of order 6, none of order 14**. q = 10 is 2 (mod 4) but 10 = 1² + 3², so Bruck–Ryser is silent; the true obstruction took until 1989, when Lam, Thiel and Swiercz closed order 10 by coding theory plus one of the largest computer searches of its era. And q = 12 — 0 (mod 4), outside Bruck–Ryser entirely — is **the smallest open order today**. The chapter says this in those words: nobody knows whether a plane of order 12 exists.

### 3.5 How many systems? The census ladder

Uniqueness at 7 and 9, then a fork: the lab's orderly-generation search — branching on the lowest uncovered pair, canonicalizing candidates under the stabilizer of the partial system, and discarding nothing — visits **41,621 search states and 560 leaves, all valid**, collapses them to isomorphism classes, and returns **STS(13) = 2**: one system with 8 Pasch configurations (four triples on six points, the "quadrilateral" {a,b,c},{a,d,e},{f,b,d},{f,c,e} up to labels), one with 13 — automorphism groups of order 6 and 39, labeled counts 1,037,836,800 + 159,667,200 = 1,197,504,000 = 13!/6 + 13!/39, as it must. The Fano plane has 7 Pasches, STS(9) has 0; the two STS(13)s split the difference, and the lab's leaves sort cleanly into buckets 468 (8-Pasch) + 92 (13-Pasch). Beyond reach of this chapter's machines and honest to say so: STS(15) = 80 systems; STS(19) = 11,084,874,829 (the Kaski–Östergård classification of 2004).

### 3.6 What to learn

Designs live or die by double counting. The two counting constants (b, r) are forced by λ·C(v, t) = b·C(k, t) before any construction begins; divisibility is the gate; Fisher's b ≥ v is the global shadow of linear independence; and the equality cases — Fano, PG(2,3) — are exactly the symmetric, self-dual worlds where the design looks the same from the block side. The census ladder (1, 1, 2, 80, eleven billion) shows how fast "count the objects" outruns "prove the theorems."

---

## Lecture 4 · Designs II: The Existence Theorems — Wilson, Keevash, and the Schoolgirls

### 4.1 Resolvability: Kirkman's problem, solved on the smallest stage

Kirkman's walking problem asks for more than an STS(15): the 35 triples must partition into **7 parallel classes of 5 disjoint triples each**, every class a partition of the 15 girls, so no two girls walk together twice across the week. A design with such a class structure is **resolvable**. The lab constructs the answer on the smallest geometric stage — PG(3,2), the projective 3-space over F₂: its 15 points are the nonzero 4-bit vectors, its lines the triples {a, b, a XOR b}, and its **35 lines are precisely an STS(15)** (every one of the 105 pairs lies in exactly one line — machine-checked). A **spread** is a set of 5 lines partitioning the points; the space has exactly **56 spreads** (machine census). The parallelism the schoolgirls need is a set of 7 spreads sharing no line; the search finds it, and the schedule is printed in the lab verbatim — Monday through Sunday, every class a clean partition, all 35 lines used exactly once. The full record: STS(15) has 80 isomorphism classes and exactly how many resolvable ones was settled only in the computer era; the lab's resolvable witness is the classical one and its verification is line-by-line.

(Sylvester's harder 1850 question — partition all C(15,3) = 455 triples of the 15 schoolgirls into 13 disjoint weekly Kirkman schedules of 35 triples each, so that every pair walks together exactly once per week and every three girls walk together exactly once across the entire 13-week term — a *large set* of resolvable STS(15)s; 455 = 13·35, so the term has exactly enough triples — was settled by Denniston in 1974, seven hours of Elliott 4130 time; whether his solution is unique up to isomorphism remains open. The chapter cites and moves on.)

### 4.2 Wilson: existence up to finitely many exceptions

For a fixed k, does a 2-(v, k, 1) design (a pairwise balanced design, PBD) exist for all large admissible v? Wilson's theorem chain of the early 1970s ("An existence theory for pairwise balanced designs" I–III) answers **yes**: for each k, all but finitely many v satisfying the divisibility conditions — **v − 1 ≡ 0 (mod k−1) and v(v−1) ≡ 0 (mod k(k−1))**, the two integrality leaves of r and b at λ = 1 — actually carry a design. The proof engine — pairwise balanced designs with one block size at a time, glued via Wilson's fundamental construction — is beyond this chapter's scope to prove; what the chapter keeps is the *shape* of the answer: divisibility is a finite check, non-existence is confined to a finite exceptional set, and the exceptional set is computable in principle for every fixed k.

### 4.3 Keevash: divisibility is the only obstruction, at last

The finishing theorem is recent and is one of the great results of modern combinatorics:

**Theorem (Keevash 2014, "The existence of designs," arXiv 1401.3665).** For every t and k, there is n₀ such that for all n ≥ n₀ satisfying the divisibility conditions — C(n−i, t−i)/C(k−i, t−i) ∈ ℤ for every 0 ≤ i < t — a Steiner system S(t, k, n) exists.

Steiner's 1853 question, open for 160 years, closes: for large systems, the arithmetic gate that blocked S(2,3,6) at a glance is the *only* obstruction. The proof is non-constructive (randomized algebra — a subtle blend of the probabilistic method of Chapter 4 with algebraic structure), and it further settled the existence of nontrivial Steiner systems for t ≥ 6 and infinitely many t = 4, 5.

The lab runs the divisibility check where the chapter can hold it in its hands, on quadruple systems S(3,4,n): the conditions are C(n,3)/4, C(n−1,2)/3, and (n−2)/2 all integral. n = 10: 30, 12, 4 — SQS(10) exists (the lab builds it: 2,520 labeled systems, one orbit, uniqueness — Barrau's 1908 theorem machine-confirmed; |Aut| = 1,440). n = 12: fails at C(11,2)/3 = 55/3 — no SQS(12), arithmetic gate closed before any search. And the census over n = 4..60: divisibility holds exactly when n ≡ 2 or 4 (mod 6) — Hanani's iff theorem (1960/1963), with the machine checking the arithmetic half.

### 4.4 The small-quadruple ladder, honestly

S(3,4,8): the lab finds 30 labeled systems, one orbit — unique, with |Aut| = 1,344 = AGL(3,2) (the 30 labeled copies each with 1,344 automorphisms exactly partition 8! = 30·1,344). S(3,4,10): unique as above. SQS(16): **1,054,163** systems (cited; the honest lab note says why: at v = 16 even a single system's labeled orbit census is an industrial computation, and the count belongs to the classification literature, not to this chapter's machines). S(4,5,v): unique at v = 11 (the Witt small system — Lecture 6's ternary Golay will *be* it), nonexistent at 15 and 17, known at 23, 35, 47, 71, …, and the smallest open order is **21**. The ladder's shape: after the first two rungs, counting collapses from "uniqueness" to "census by industrial machine," and by the third rung into open problems — the design universe thickens as fast as the existence theory thins.

### 4.5 What to learn

Existence at scale is the divisibility conditions *plus* one theorem. Kirkman's resolvable STS(15) shows constructions can be pure geometry (PG(3,2)); Wilson confines exceptions to finite sets; Keevash erases them entirely for large v. The pattern entry proposed: **double-counting/divisibility** — integrality as the admission fee, existence as the theorem that the fee is sufficient.

---

## Lecture 5 · Coding Beyond the Sphere: Singleton, Plotkin, and Gilbert–Varshamov

### 5.1 Where Chapter 8 left the cube

Chapter 8 built the Hamming theory: the [7,4,3] code — 16 words, minimum distance 3, the weight distribution A = [1, 0, 0, 7, 7, 0, 0, 1] (one zero word, seven of weight 3, seven of weight 4, one all-ones) — and Delsarte's linear program on the cube. This lecture takes the three bounds that shape every code family: Singleton from the outside, Plotkin from the outside when distances are dense, Gilbert–Varshamov from the inside. The lab re-derives the Hamming [7,4,3] from the parity-check view (columns = the seven nonzero 3-bit vectors) and machine-verifies its **perfectness**: 16 radius-1 balls of size 8 tile F₂⁷, 16·8 = 128 = 2⁷ — every word within distance 1 of exactly one codeword, the sphere-packing identity made literal.

### 5.2 Singleton and MDS

**Theorem (Singleton bound; standard citation Singleton 1964 — though proven earlier by Joshi in 1958 and Komamiya in 1953, a priority the chapter records honestly).** Any q-ary code of length n, size M, minimum distance d (1 ≤ d ≤ n) satisfies M ≤ q^{n−d+1}. *Proof in one move:* puncture d−1 coordinates; surviving words remain distinct, and there are only q^{n−d+1} of them. ∎

Linear codes meeting the bound with equality — [n, k, n−k+1]_q — are **MDS** (maximum distance separable). The binary census is a desert: the lab enumerates every binary linear code up to n = 7 by canonical subspace enumeration (Gaussian cross-checks on the row-reduced keys) and finds *no* nontrivial binary MDS — the only [n, k, n−k+1]₂ codes are the trivial three families (whole space k = n, repetition k = 1, and even-weight parity k = n−1). Over larger alphabets the desert blooms: **Reed–Solomon codes** take the messages (a, b) ∈ F_q² and evaluate a + bx at n distinct field points. The lab's witnesses over F₅: evaluations at 4 points give **[4,2,3]₅** (25 words, all distinct, machine minimum pairwise distance exactly 3 = Singleton) and at all 5 points **[5,2,4]₅** (distance 4 = Singleton). A degree-1 polynomial has at most 1 root, so two distinct messages differ in at least n−1 positions — Singleton tight for every n ≤ q (and n ≤ q+1 with the point at infinity, where the extra coordinate carries the leading coefficient; the lab's [6,2,5]₅ — evaluations at all five points plus b — is the machine witness), and the whole family rides one polynomial fact.

How far can MDS go? The **MDS conjecture** (posed as a question by Segre in 1955): a nontrivial [n,k]_q MDS code (2 ≤ k ≤ q−1) has n ≤ q+1, except when q is even with k = 3 or k = q−1, where n ≤ q+2. The prime-field case is now a theorem — **Ball 2012**, with Ball–De Beule 2012 giving k ≤ 2p−2 for q = p^h — and the general case is **open**. Another honest frontier entry.

### 5.3 Plotkin: dense distance caps size

**Theorem (Plotkin 1960).** A binary code of length n and minimum distance d with 2d > n has at most ⌊2d/(2d−n)⌋ codewords, and at most 2⌊d/(2d−n)⌋ when d is even; in the boundary case n = 2d, A(2d, d) ≤ 4d.

*Proof (by averaging — the pattern map's P10 in its purest code-theoretic use):* sum the pairwise distances two ways. On one hand, every pair is ≥ d apart, contributing at least d·C(M,2). On the other, column by column: if a column has z zeros and M−z ones it contributes z(M−z) ≤ M²/4 (and ≤ (M²−1)/4 when M is odd), so the total is ≤ M²n/4. Comparing: d·M(M−1)/2 ≤ M²n/4, which rearranges (M ≥ 2) to M ≤ 2d/(2d−n), hence M ≤ ⌊2d/(2d−n)⌋. Two refinements squeeze out the integers. When M = 2m is even, the comparison reads d·m(2m−1) ≤ m²n, i.e. m(2d−n) ≤ d, so m ≤ ⌊d/(2d−n)⌋ and M ≤ 2⌊d/(2d−n)⌋. When M is odd and d is even, the sharper column bound (M²−1)/4 gives M(2d−n) ≤ n, i.e. M ≤ n/(2d−n) = 2d/(2d−n) − 1, and an odd integer strictly below 2d/(2d−n) never exceeds the even integer 2⌊d/(2d−n)⌋. So M ≤ ⌊2d/(2d−n)⌋ always, and M ≤ 2⌊d/(2d−n)⌋ when d is even. ∎

The boundary case n = 2d is beyond averaging's reach — both displayed bounds go vacuous exactly there — but one line of *shortening* proves it: split any code by its first coordinate into the words with a 0 there and the words with a 1, puncture that coordinate from each half (agreement on it means distances survive intact), and each half is a code of length 2d−1 and distance d — so A(2d, d) ≤ 2·A(2d−1, d), and the theorem just proved caps the half at ⌊2d/1⌋ = 2d. Hence **A(2d, d) ≤ 4d, with no parity guard needed**. The expansion pass's fresh battery certifies the small instances exhaustively: A(2,1) = 4, A(4,2) = 8, A(6,3) = 8, A(8,4) = 16 — each within 4d, tight at d = 1, 2, 4 — and Best's famous 20-word code is a length-*nine* code (A(9,4)), nowhere near this boundary; the Paley–Hadamard (12, 24, 6) code witnesses d = 6 at exactly 4d. (Chapter 8 already owns the Delsarte-certificate form of Plotkin — the certificate F = 1 + K₁/(2d−n) — the two routes agree and the cross-reference stands.)

The bound is tight in the dense corner where Singleton is slack: the lab exhibits **A(6,4) = 4** (Plotkin bound 2·⌊4/2⌋ = 4, met by a machine-constructed code of 4 words) and **A(7,4) = 8** (bound 2·⌊4/(8−7)⌋ = 8, met by the **[7,3,4] simplex code** — the dual of the Hamming code: all seven nonzero codewords have weight exactly 4, so every pair sits at distance 4, machine-verified). Two more tightness exhibits from the fresh battery: **A(8,6) = 2** is the even-d refinement biting — the general form allows 3, the parity form caps it at 2⌊6/4⌋ = 2 — and **A(7,5) = 2** shows the odd-M column bound at work, explaining why the general form's ⌊10/3⌋ = 3 is never achieved there. Simplex structure saturates Plotkin exactly as polynomial structure saturates Singleton: **the extremal witness teaches the bound**.

### 5.4 Gilbert–Varshamov: existence from greed

**Theorem (Gilbert 1952; the linear-code version Varshamov 1957).** A_q(n, d) ≥ q^n / Σ_{j=0}^{d−1} C(n,j)(q−1)^j.

*Proof:* greed. Throw balls of radius d−1 around a maximal code; maximality says they cover the whole cube, so M·(ball volume) ≥ q^n. ∎ The lab runs the greedy construction itself and prints honest witnesses at four points — (7,3): 16 ≥ ⌈128/29⌉ = 5; (8,3): 16 ≥ 7; (10,4): 32 ≥ 6; (12,4): 128 ≥ 14 — each a machine-constructed code and a count that clears the bound with room, because the ball-volume denominator over-counts overlaps near the covering boundary.

### 5.5 What to learn

The three bounds are three geometries of the Hamming cube: Singleton slices coordinates away (algebra), Plotkin averages distances (geometry), Gilbert–Varshamov covers (volume). MDS codes live where algebra is richest (polynomials over fields); Plotkin-tight codes where combinatorial designs are (the simplex); and the GV bound is the guarantee that good codes are *easy to find* — greed suffices. The frontier ledger: binary MDS trivial (census), general MDS bounded by a conjecture with the prime case proved, Plotkin's corner exactly charted by simplex witnesses.

---

## Lecture 6 · The Golay Bridge: Codes as Designs

### 6.1 The best single published page

Marcel Golay's 1949 note "Notes on Digital Coding" (Proceedings of the IRE, vol. 37, page 657 — half a column, one table) announced two codes: a binary [23,12,7] and a ternary [11,6,5]. Berlekamp's verdict is the standard quip: it is the best single published page in coding theory. (The ternary code had been printed even earlier — Virtakallio, 1947, in the Finnish football-pool magazine Veikkaaja; priority is recorded.) Both codes are **perfect**: their radius-t error balls tile their cubes exactly, the sphere-packing identity holding with equality — the [7,4,3] Hamming code of Chapter 8 has exactly two nontrivial siblings in the perfect family, and Golay's page contains both. Perfectness here is machine-verified in this chapter's lab, word by word: 729 ternary balls of radius 2 partition F₃¹¹ (729·243 = 177,147 = 3¹¹), and 4,096 binary balls of radius 3 partition F₂²³ (4,096·2,048 = 8,388,608 = 2²³).

### 6.2 The ternary Golay code and the Witt system S(4,5,11)

Take Φ₁₁ = 1 + x + x² + … + x¹⁰, the cyclotomic factor of x¹¹ − 1 over F₃. It splits into two monic quintics, and the lab factors it by machine:

Φ₁₁ = (x⁵ + x⁴ + 2x³ + x² + 2)·(x⁵ + 2x³ + x² + 2x + 2)

(verify the coefficient arithmetic mod 3 — the product is 1 + x + … + x¹⁰ with zero remainder, machine-checked). Either factor generates a cyclic code of length 11, dimension 6, and the machine census prints, for both: **729 codewords, minimum distance 5** — the [11,6,5]₃. The weight distribution (identical for both factors):

A₀ = 1, A₅ = 132, A₆ = 132, A₈ = 330, A₉ = 110, A₁₁ = 24.

Now the bridge: look only at the *supports* of the 132 weight-5 words. Two ternary words can share a support (the sign flip c ↦ 2c = −c changes the word, not the support), and here the 132 words pair up onto **66 supports**, every 4-subset of the 11 coordinates lying in exactly one of them — the supports form the Steiner system **S(4,5,11)**, the small Witt design. Extend the code by an overall-parity coordinate to [12,6,6]₃ (machine-verified self-dual, weights A = 1, 264, 440, 24 at 0, 6, 9, 12): now the 264 weight-6 words pair up onto **132 weight-6 supports** forming **S(5,6,12)** — the 5-design of the small Witt pair — with automorphism group M₁₂.

### 6.3 The binary Golay code and S(5,8,24)

The binary twin: over F₂, (x²³+1)/(x+1) factors into exactly two monic degree-11 polynomials (machine-found, not remembered):

g₀ = x¹¹ + x⁹ + x⁷ + x⁶ + x⁵ + x + 1, g₁ = x¹¹ + x¹⁰ + x⁶ + x⁵ + x⁴ + x² + 1.

Either generates the **[23,12,7]₂**: 4,096 words, minimum distance 7 — verified by the machine over all 8,386,560 codeword pairs, with the weight distribution

A₀ = 1, A₇ = 253, A₈ = 506, A₁₁ = 1288, A₁₂ = 1288, A₁₅ = 506, A₁₆ = 253, A₂₃ = 1 — the all-ones word included, the eight values summing to 4,096.

Extend by parity to the **[24,12,8]₂** — self-dual, and the weight enumerator is the famous five-term line

A₀ = 1, A₈ = 759, A₁₂ = 2576, A₁₆ = 759, A₂₄ = 1.

The 759 weight-8 words — **octads** — are the blocks of S(5,8,24): the lab machine-verifies that each of the C(24,5) = 42,504 five-subsets of coordinates lies in **exactly one** octad. The octad arithmetic that makes the count inevitable is the exercise: every octad carries C(8,5) = 56 of the five-subsets, so 759·56 = 42,504 = C(24,5) — the design's defining property *is* the weight enumerator's arithmetic shadow.

### 6.4 Assmus–Mattson: how a code hands you a design

Why do the weight supports of these codes suddenly satisfy t-design conditions? The Assmus–Mattson theorem (1969) is the machine behind the bridge: for a linear code with few distinct weights and a dual with few weights, the words of any given weight carry a t-design on their supports. The theorem is stated (its proof — an incidence-counting argument via the dual code — is cited, and the chapter does not pretend otherwise); the Golay instances are the classic application, and Assmus–Mattson's own paper mined exactly these: the 5-designs on 12 and 24 points. The general pattern — **words-as-designs** — is the proposed registry entry: pick a code with rigid weight structure, read a design off its supports, and the code's automorphism group acts on the design's block set.

### 6.5 The Mathieu groups, and the chapter in one table

The automorphism group of S(5,8,24) is **M₂₄**, of order

24·23·22·21·20·48 = 244,823,040 = 2¹⁰·3³·5·7·11·23,

machine-multiplied and machine-factored; the point stabilizer is M₂₃ = 10,200,960 (= M₂₄/24), whose point stabilizer is M₂₂ = 443,520, and the octad stabilizer has order |M₂₄|/759 = 322,560 — the ladder the lab prints exactly. The S(5,6,12) system carries M₁₂ = 95,040 (its stabilizer arithmetic: |M₁₂|/132 hexads = 720), point stabilizer M₁₁ = 7,920. M₂₄ and M₁₂ are 5-transitive — M₁₂ sharply so — and by the classification of finite simple groups the Mathieu groups are the *only* 4-transitive permutation groups beyond the symmetric and alternating ones. They are the first five sporadic simple groups ever found (Mathieu, 1861 and 1873), and the honest historical arrow runs backwards: the *designs* were constructed first as abstract systems, and the *codes* — Golay 1949 — gave them their most usable incarnation.

**The consolidation table:**

| Object | The symmetry | The inversion | The design |
|--------|--------------|---------------|-----------|
| Necklaces / cube / trees (L1) | Burnside average over C_n, the 24 rotations, canonical generation | — | — |
| Divisors / subsets / partitions (L2) | — | μ recovers τ, φ, the (−1)^k and (−1)^{n−1}(n−1)! patterns | — |
| Fano / STS(9) / STS(13) (L3) | — | — | b = v(v−1)/6 forced by double counting; Fisher b ≥ v; census 1, 1, 2 |
| PG(2,3) (L3) | 13-point self-dual symmetric design | — | S(2,4,13), Bruck–Ryser's survivors |
| Schoolgirls (L4) | 7 parallel classes of PG(3,2) | — | resolvable STS(15); divisibility gate v ≡ 1,3 (mod 6) → S(3,4,n): n ≡ 2,4 (mod 6) |
| RS / simplex / greedy (L5) | Singleton by puncturing; Plotkin by averaging | — | — |
| Golay ↔ Witt (L6) | Aut groups M₂₄, M₁₂ | — | 66 supports = S(4,5,11); 759 octads = S(5,8,24) |

### 6.6 What to learn

The three threads of the chapter knit into one object: the Golay codes are perfect by *volume* (sphere-packing — Lecture 5's cube geometry), their supports are designs by *counting* (Assmus–Mattson — Lecture 3–4's double counting), and their automorphism groups are symmetry groups (Lecture 1's orbit machines, run at full size). The words-as-designs bridge is the proposed pattern entry, and the Mathieu groups are the proof that the bridge can carry traffic: five sporadic simple groups live at the far end of it.

---

## The Trick Bag (reference card)

| Tool | Statement | Where proved / cited |
|------|-----------|---------------------|
| **Burnside's lemma** | # orbits = (1/\|G\|)·Σ_g \|Fix(g)\| | L1 (proved in full; Cauchy 1845/Frobenius 1887 priority) |
| **Pólya's theorem** | k-coloring orbits = Z_G(k,…,k); Z_G the cycle index | L1 (proved from the fixed-point form; Redfield 1927 priority noted) |
| **Cube cycle index** | (k⁶+3k⁴+12k³+8k²)/24; k = 1..5: 1, 10, 57, 240, 800 | L1 (machine census 1⁶:1, 2²1²:3, 2³:6, 3²:8, 4·1²:6) |
| **Shape generation** | Rooted = multiset closure; unrooted = centroid split; 1,1,1,2,3,6,11,23 | L1 (Prüfer cross-check) |
| **Möbius inversion (classical)** | g = Σ_{d\|n} f(d) ⟹ f(n) = Σ_{d\|n} μ(d)·g(n/d); Σ_{d\|n} μ(d) = [n=1] | L2 (proved) |
| **Poset μ + incidence algebra** | μ ζ = identity under convolution; μ(0̂,1̂) on Π_n = (−1)^{n−1}(n−1)! | L2 (proved; Rota 1964) |
| **Design counting constants** | λ·C(v,t) = b·C(k,t); r·C(k−1,t−1) = λ·C(v−1,t−1) (so r = λ(v−1)/(k−1) for t = 2) | L3 (double counting) |
| **STS gate** | STS(v) exists iff v ≡ 1, 3 (mod 6) (v ≥ 3); S(2,3,6) impossible at r = 5/2 | L3 (cited; machine exhibit) |
| **Fisher's inequality** | 2-(v,k,λ) with 2 ≤ k < v, λ ≥ 1 ⟹ b ≥ v; equality ⟺ symmetric designs | L3 (Ch. 6 proofs cited; census view here) |
| **Bruck–Ryser–Chowla** | q ≡ 1,2 (mod 4) plane ⟹ q a sum of two squares; orders 6, 14 out; 10 out by Lam et al. 1989; 12 open | L3 (cited; arithmetic census) |
| **STS census ladder** | 1 (v=7), 1 (v=9), 2 (v=13, machine-proved), 80 (v=15), 11,084,874,829 (v=19) | L3 (first three machine; the rest cited) |
| **Wilson / Keevash** | PBDs: all but finitely many admissible v; designs for all large admissible n — divisibility the only obstruction | L4 (cited) |
| **Kirkman resolvability** | PG(3,2): 35 lines = STS(15), 56 spreads, 7 disjoint = the schoolgirl schedule | L4 (machine-verified) |
| **SQS ladder** | SQS iff v ≡ 2, 4 (mod 6) (Hanani); unique at 8 (Aut 1344) and 10 (Aut 1440 = PΓL(2,9)); 1,054,163 at 16; S(4,5,v) unique at 11, smallest open 21 | L4 (8/10 machine; rest cited) |
| **Singleton / MDS** | M ≤ q^{n−d+1}; binary MDS trivial; RS over F₅: [4,2,3]₅, [5,2,4]₅; MDS conjecture (Segre 1955), prime case Ball 2012 | L5 (bound proved; census + witnesses machine) |
| **Plotkin bound** | 2d > n ⟹ M ≤ ⌊2d/(2d−n)⌋ (and M ≤ 2⌊d/(2d−n)⌋ for even d); boundary A₂(2d,d) ≤ 4d by shortening; tight at (6,4) = 4, (7,4) = 8 simplex, (2,1) = 4, (4,2) = 8, (8,4) = 16 Hadamard, (8,6) = 2 | L5 (proved by averaging + shortening; witnesses machine) |
| **Gilbert–Varshamov** | A_q(n,d) ≥ q^n/Σ_{j<d} C(n,j)(q−1)^j | L5 (proved; greedy witnesses machine) |
| **Perfect codes** | Hamming [7,4,3]: A = [1,0,0,7,7,0,0,1], 16·8 = 128; ternary [11,6,5]: 729·243 = 3¹¹; binary [23,12,7]: 4096·2048 = 2²³ | L5–L6 (machine; Ch. 8 cross-ref) |
| **Golay ↔ Witt** | 132 w₅ words → 66 supports = S(4,5,11); [12,6,6] → 264 w₆ words → 132 supports = S(5,6,12); 759 octads = S(5,8,24), each 5-subset in exactly one; Assmus–Mattson 1969 the bridge | L6 (machine) |
| **Mathieu ladder** | M₂₄ = 244,823,040 = 2¹⁰·3³·5·7·11·23; M₂₃ = 10,200,960; M₂₂ = 443,520; M₁₂ = 95,040; M₁₁ = 7,920; 5-transitive M₂₄, M₁₂ | L6 (machine arithmetic; transitivity cited) |

**Formula box:** Burnside |X/G| = (1/|G|)Σ_g |Fix(g)|; Pólya Z_G(x) = (1/|G|)Σ_g ∏_i x_i^{c_i(g)}, cube (k⁶+3k⁴+12k³+8k²)/24, 2-color necklace (1/n)Σ_{k=0}^{n−1} 2^gcd(n,k). Möbius: Σ_{d|n} μ(d) = [n=1]; inversion f(n) = Σ_{d|n} μ(d)g(n/d); poset μ(x,y) = −Σ_{x≤z<y} μ(x,z); Boolean μ(T,S) = (−1)^{|S∖T|}; partition μ(0̂,1̂) = (−1)^{n−1}(n−1)!. Designs: λC(v,t) = bC(k,t), rC(k−1,t−1) = λC(v−1,t−1) (r = λ(v−1)/(k−1) for t=2); STS: b = v(v−1)/6, r = (v−1)/2, exists iff v ≡ 1,3 (mod 6); Fisher b ≥ v; projective plane S(2,q+1,q²+q+1), affine S(2,q,q²); BR: q ≡ 1,2 (mod 4) ⟹ q = a²+b². Codes: Singleton A_q(n,d) ≤ q^{n−d+1}; Plotkin 2d > n ⟹ A_2(n,d) ≤ ⌊2d/(2d−n)⌋ (2⌊d/(2d−n)⌋ when d is even), A_2(2d,d) ≤ 4d; GV A_q(n,d) ≥ q^n/Σ_{j=0}^{d−1}C(n,j)(q−1)^j; Hamming ball V_q(n,t) = Σ_{j≤t} C(n,j)(q−1)^j; perfect: M·V_q(n,t) = q^n. Golay: ternary [11,6,5] A = 1,132,132,330,110,24; binary [24,12,8] A = 1,759,2576,759,1; octad arithmetic 759·56 = 42,504 = C(24,5); |M₂₄| = 244,823,040.

---

## Exercises (graded: ●○○ easy · ●●○ moderate · ●●● tough)

**1. (●●○) The twelfth necklace.** Compute the number of 2-color necklaces of length 12 by Burnside, then explain in one sentence why the answer is *not* 2¹²/12. *(Hint: gcd is doing the work — tabulate 2^gcd(12, k) for k = 0..11 before averaging.)*

**2. (●●○) The three-color cube.** Using the cycle-type census 1⁶:1, 2²1²:3, 2³:6, 3²:8, 4·1²:6, compute the number of rotationally distinct 3-colorings of the cube's faces, and verify your answer against the closed form (k⁶+3k⁴+12k³+8k²)/24.

**3. (●○○) Bracelets vs necklaces, at six beads.** A bracelet may be picked up and flipped; a necklace may only be spun. Compute both counts for 2 colors at n = 6 and explain the difference of exactly one orbit: which coloring class merges under the flip?

**4. (●○○) The divisor battery.** Compute τ(60) and φ(60); then prove the identity φ(n) = Σ_{d|n} d·μ(n/d) by Möbius inversion from Σ_{d|n} φ(d) = n. *(All three values are machine-verified in the lab.)*

**5. (●○○) The exhibit that cannot exist.** Show that S(2,3,6) cannot exist by integrality of r; then state the exact congruence gate for STS(v) and where v = 6 fails it. *(The lab's machine proof searched all 15,504 candidate block families and found zero — your job is the two-line reason.)*

**6. (●●○) Fisher at nine.** The lab's census finds exactly 840 labeled STS(9)s, all isomorphic. Compute b and r for STS(9), verify Fisher's inequality b ≥ v with the actual slack, and explain what the slack measures geometrically (the affine plane AG(2,3) has a distinguished line at infinity that the Fano plane does not).

**7. (●●○) A symmetric design.** For PG(2,3): verify from the construction (points = 1-dim subspaces of F₃³) that b = v = 13, and prove that in any projective plane any two *lines* meet in exactly one point — so the design is symmetric: the block-versus-point incidence matrix is square and the dual design is another plane of the same order.

**8. (●●○) Quadruple witnesses.** The lab finds SQS(8) and SQS(10) each unique (one orbit; 30 and 2,520 labeled systems). Compute the pair-multiplicity λ₂ for S(3,4,v) at v = 8 and v = 10 from the counting constants alone, and check your values against the lab's witnesses.

**9. (●●●) The schoolgirls' schedule, verified.** The lab prints a resolvable STS(15): 7 parallel classes of 5 disjoint triples. Prove from the parameters alone that any resolvable STS(15) must have exactly 7 classes of exactly 5 triples each (count block-slots two ways), then verify the lab's printed schedule satisfies: every class partitions all 15 girls; the 35 triples are distinct and each is a line of PG(3,2).

**10. (●●○) Reed–Solomon is MDS.** Prove that the code of evaluations of a + bx at n distinct points of F_q has minimum distance exactly n−1 (hence [n,2,n−1]_q, Singleton-tight), and exhibit the lab's witnesses [4,2,3]₅ and [5,2,4]₅.

**11. (●●○) Two bounds, two witnesses.** Run the Plotkin arithmetic at (7,4): the bound gives 2⌊4/(8−7)⌋ = 8, met by the [7,3,4] simplex (all seven nonzero words weight 4). Then run the Gilbert–Varshamov arithmetic at (10,4): the bound gives 32 ≥ ⌈1024/176⌉ = 6. Verify both denominators (the ball volume 1+10+... at d−1 = 3; the Plotkin floor) and explain why one bound is met *exactly* and the other with a factor of 5 to spare.

**12. (●●○) Octad arithmetic.** The extended binary Golay code has 759 weight-8 words. Show that if their supports form an S(5,8,24), then the count 759 is forced by pure arithmetic: C(24,5)/C(8,5). Compute the number, and verify it equals the weight enumerator's A₈.

### ◆ Pattern-unknown problems (no hints; the diagnosis is the point)

**◆ Problem 1.** Chapter 2's exploration X1 counted 1, 1, 1, 2, 3, 6 tree shapes at n = 6 and deferred the machine. Extend the census to n = 8 — by any method that never produces the same shape twice — and also report the *rooted* count at n = 8.

**◆ Problem 2.** On the partition lattice Π₅ (52 elements), compute μ(0̂, 1̂) directly from the recursion — no formula assumed. Then guess the general pattern for Π_n and check it against Π₄.

**◆ Problem 3.** Chapter 8's [7,4,3] Hamming code has 16 words. Verify the weight distribution [1,0,0,7,7,0,0,1] and prove the perfectness identity 16·8 = 128 = 2⁷ from the distribution — counting, not construction, is the tool the problem wants.

### ◐ Explorations (what you should find, not a number to match)

**◐ Exploration 1 (Bruck–Ryser table).** For each order q = 2..16, classify: ruled out by Bruck–Ryser (and why, via the sum-of-two-squares test), silent to it, or (where the answer is known) resolved by other means. You should find exactly two ruled-out orders in this range, one famously silent-then-killed order (q = 10), and the smallest open order.

**◐ Exploration 2 (Keevash's gate, by hand).** Write the three divisibility conditions for S(3,4,n) explicitly as three fractions in n. Evaluate them at n = 10 and n = 12; determine which condition is the binding one at each, and run the census: for which residues mod 6 do all three hold? (The lab's machine census over n = 4..60 confirms the pattern; your job is the hand derivation plus the machine agreement.)

**◐ Exploration 3 (The Mathieu ladder).** Verify by machine arithmetic: M₂₄ = 24·23·22·21·20·48 and its prime factorization; the stabilizer ladder M₂₃ = M₂₄/24, M₂₂ = M₂₃/23, M₁₂ = 12·11·10·9·8, M₁₁ = M₁₂/12; and the block-stabilizer arithmetic |M₂₄|/759 (octads) and |M₁₂|/132 (hexads). Explain why each quotient is an integer, using the design whose blocks are being stabilized.

## Answers to the Exercises

**1.** Burnside over C₁₂: tabulate gcd(12, k) for k = 0..11 — 12, 1, 2, 3, 4, 1, 6, 1, 4, 3, 2, 1 — so the fixed-coloring counts are 4096, 2, 4, 8, 16, 2, 64, 2, 16, 8, 4, 2, summing to 4224, and 4224/12 = **352**. And it is *not* 2¹²/12 = 341.33 because orbits are not the same size: the two constant colorings ride all 12 rotations fixed, and every orbit of size s contributes |G|/s to the sum Σ|Fix| — Burnside's average repairs exactly what naive division breaks. *(Receipt 54runs-1: brute-force canonicalization of all 4096 strings agrees at n = 12, and at every n = 1..12.)*

**2.** k = 3: (729 + 3·81 + 12·27 + 8·9)/24 = (729 + 243 + 324 + 72)/24 = 1368/24 = **57** ✓, matching the machine's brute-force canonicalization (54runs-1).

**3.** Necklaces: Burnside over C₆, rotations k = 0..5 fix 2^gcd(6,k) = 64, 2, 4, 8, 4, 2 — sum 84, and 84/6 = **14**. Bracelets: add the 6 reflections of the dihedral group; n even splits them — 3 axes through opposite bead-pairs (2 fixed beads + 2 swapped pairs = 4 cycles → 16 fixed colorings each) and 3 axes through opposite gaps (3 swapped pairs = 3 cycles → 8 each), reflection total 3·16 + 3·8 = 72; (84 + 72)/12 = **13** ✓ (54runs-9). The merged orbit: the two mirror-image necklaces with no rotational symmetry — e.g. 001011 and its reversal — become a single bracelet under the flip.

**4.** 60 = 2²·3·5 → τ(60) = 3·2·2 = **12**; φ(60) = 60·(1/2)(2/3)(4/5) = **16**. Proof of the identity: first Σ_{d|n} φ(d) = n, by partitioning the n integers m ∈ {1,…,n} according to g = gcd(m, n); writing d = n/g, we have gcd(m/g, d) = 1 with 1 ≤ m/g ≤ d, so exactly φ(d) integers belong to each divisor d | n. Then apply Möbius inversion to g(n) = n = Σ_{d|n} f(d) with f = φ: φ(n) = Σ_{d|n} μ(d)·(n/d) = Σ_{d|n} d·μ(n/d) ✓ (all identities machine-verified n ≤ 10⁴, zero mismatches; receipt 54runs-2).

**5.** r = (v−1)/(k−1) = 5/2 — not an integer, so no S(2,3,6) exists. The gate is v ≡ 1 or 3 (mod 6), and v = 6 fails at exactly one leaf: b = 6·5/6 = 5 is an integer, so it is r = 5/2 that kills it — which is precisely why the exhibit is instructive: checking *one* counting constant is not enough to certify existence, but one non-integer is enough to certify non-existence. The lab's exhaustive search over all 15,504 candidate block families returns zero systems — the machine echo of the two-line reason. *(Receipt 54runs-3.)*

**6.** STS(9): b = 9·8/6 = **12** > v = 9 (Fisher slack 3); r = 8/2 = 4. The geometric reading: STS(9) is the affine plane AG(2,3) — PG(2,3) with a line at infinity deleted — so 13 − 1 = 12 lines remain on 13 − 4 = 9 points. Fisher's tight case b = v needed the full symmetric plane; deleting the line at infinity destroys the symmetry and leaves the inequality strict. (The machine census: 840 labeled systems, one isomorphism orbit — receipt 54runs-3.)

**7.** Any two 1-dim subspaces of F₃³ span a unique 2-dim subspace (their sum), so any two points lie on exactly one line; dually, any two 2-dim subspaces intersect in a 1-dim subspace (dimension formula: 2+2−3 = 1), so any two lines meet in exactly one point. The incidence matrix is square (13 = 13) and N^T is the incidence matrix of another S(2,4,13) — the dual plane. Fisher is tight exactly because the blocks, like the points, are pairwise "incident-constant" (any two blocks meet in λ' = 1 points). *(Receipt 54runs-9: all 78 pairs in exactly one of the 13 lines, machine-verified.)*

**8.** Fix a pair P in S(3,4,v). Every triple P ∪ {x} lies in a unique block, whose fourth point is a partner y(x); the partner map x ↦ y is a fixed-point-free involution on the remaining v − 2 points (y(y(x)) = x, since P ∪ {y} ∪ {x} is the same block), so the points pair up and the blocks through P number (v−2)/2: **λ₂ = 3 at v = 8** (three pairs from six points) and **λ₂ = 4 at v = 10** — both confirmed on the lab's witnesses, where every pair lies in exactly 3 (resp. 4) blocks. The same count is the i = 2 case of the design constant λ_i = λ·C(v−i, t−i)/C(k−i, t−i): C(6,1)/C(2,1) = 3 and C(8,1)/C(2,1) = 4. *(Receipts 54runs-5.)*

**9.** Any resolvable STS(15): 35 blocks total (15·14/6); each parallel class partitions 15 points into 15/3 = 5 triples; so the number of classes is 35/5 = **7** — both counts forced, no freedom anywhere. The lab's schedule verifies: each class's 5 triples are pairwise disjoint and cover {1..15}; the 35 triples are distinct; each is {a, b, a XOR b} in the bitmask labeling, i.e., a line of PG(3,2). *(Receipt 54runs-10; the schedule prints Monday..Sunday verbatim.)*

**10.** Two distinct messages (a,b) ≠ (a′,b′) give a nonzero linear polynomial c₀ + c₁x with at most one root among the n evaluation points, so the evaluations agree in at most one position and differ in at least n−1: d ≥ n−1; Singleton gives d ≤ n−1; equality. Witnesses: [4,2,3]₅ (25 words, machine min distance 3) and [5,2,4]₅ (min distance 4) — receipt 54runs-11.

**11.** Plotkin at (7,4): 2d > n (8 > 7) so M ≤ 2⌊d/(2d−n)⌋ = 2·4 = 8; the simplex meets it (7 nonzero words of weight 4; distance between any two = 4 by linearity). GV at (10,4): ball volume Σ_{j=0}^{3} C(10,j) = 1+10+45+120 = 176; A ≥ 1024/176 → 32 ≥ 5.82, so ≥ 6; the greedy construction actually finds 32 words. Why the difference in tightness: Plotkin's averaging argument is *exact* for its witnesses (the simplex saturates the double count), while GV's greedy leaves slack because balls near the packing boundary overlap less than the volume bound pretends. *(Receipts 54runs-6, 54runs-11.)*

**12.** If the 759 octads form S(5,8,24), each octad contains C(8,5) = 56 five-subsets and each of the C(24,5) = 42,504 five-subsets lies in exactly one octad, so 759·56 = 42,504 — and 42,504/56 = **759** ✓ = A₈, the machine's weight-enumerator entry. The arithmetic is airtight in both directions: the design property forces the weight enumerator's A₈, and the lab verifies the design property independently (each of the 42,504 five-subsets in exactly one octad, machine-checked; receipt 54runs-8).

### Answers to the ◆ problems (receipt-backed)

**◆ 1.** Unrooted shapes at n = 8: **23** (multiset closure via the centroid split; independent Prüfer-sequence enumeration of all 8⁶ = 262,144 labeled trees with canonical-form dedup agrees exactly). Rooted shapes at n = 8: **115**. The diagnosis: this is orbit counting where the "group" is all relabelings — Burnside in spirit, canonical-generation in practice. *(Receipt 54runs-1; the machine cross-check is the whole point: two independent engines, one answer.)*

**◆ 2.** μ(0̂, 1̂) on Π₅ = **+24**, computed from the recursion alone — the lab walks the 52-element lattice (|Π₅| = 52, machine-tallied) and the alternating accumulation returns +24. The general pattern it suggests: μ(0̂,1̂) on Π_n = (−1)^{n−1}(n−1)!, and the machine agrees — n = 3: +2, n = 4: −6, n = 5: +24. The diagnosis: Möbius inversion on a genuinely non-numeric poset — the pattern is the incidence algebra, not the numbers. *(Receipt 54runs-2.)*

**◆ 3.** Weight distribution [1,0,0,7,7,0,0,1]: 16 words, weights 0,3,4,7. Perfectness from the distribution: count pairs (c, x) with x within distance 1 of codeword c — equivalently Σ_c (1 + 7) = 16·8 = 128 = 2⁷; a perfect code must satisfy M·(1+n) = 2^n at radius 1, and the [7,4,3] does, exactly. The diagnosis: sphere-packing as a *counting* identity on the weight enumerator — Chapter 8's Delsarte machinery in miniature. *(Receipt 54runs-11.)*

### Findings for the ◐ explorations (receipt-backed)

**◐ 1.** Ruled out by Bruck–Ryser in 2..16: q = 6 and q = 14 (both ≡ 2 mod 4, neither a sum of two squares: 6 = a²+b² has no solution; 14's prime factor 7 ≡ 3 mod 4 appears to an odd power). The silent-then-killed: q = 10 ≡ 2 mod 4 but 10 = 1²+3², so Bruck–Ryser says nothing — non-existence is Lam–Thiel–Swiercz 1989 (coding theory + search). Smallest open: **q = 12** (≡ 0 mod 4, outside Bruck–Ryser entirely; q = 15 ≡ 3 mod 4 is also not a prime power, silent to Bruck–Ryser, and open). The prime-power orders in 2..16 all exist as Desarguesian planes PG(2,q): 2, 5, 9, 13 pass Bruck–Ryser's two-squares test (2 = 1²+1², 5 = 1²+2², 9 = 0²+3², 13 = 2²+3²), while 3, 7, 11 (≡ 3 mod 4) and 4, 8, 16 (≡ 0 mod 4) are silent to Bruck–Ryser. *(Receipt 54runs-9.)*

**◐ 2.** S(3,4,n) conditions: C(n,3)/4, C(n−1,2)/3, (n−2)/2. At n = 10: 120/4 = 30 ✓, 36/3 = 12 ✓, 8/2 = 4 ✓ — admissible (SQS(10) exists and is unique). At n = 12: 220/4 = 55 ✓, but 55/3 ∉ ℤ — inadmissible; the binding condition is the second (pairs through a point). Census n = 4..60: all three hold iff n ≡ 2 or 4 (mod 6) — zero mismatches with Hanani's iff theorem. *(Receipt 54runs-11.)*

**◐ 3.** M₂₄ = 244,823,040 = 2¹⁰·3³·5·7·11·23 (product and factorization both machine-verified); M₂₃ = M₂₄/24 = 10,200,960; M₂₂ = M₂₃/23 = 443,520; M₁₂ = 95,040; M₁₁ = M₁₂/12 = 7,920; |M₂₄|/759 = 322,560; |M₁₂|/132 = 720. Integrality: each quotient counts a stabilizer (point stabilizers by transitivity; octad/hexad stabilizers because the group acts on the block set of the Witt design — 759 octads, 132 hexads — transitively by design automorphism). *(Receipt 54runs-11.)*

---

## Computational Lab (verified)

Every run below was executed before a line of the chapter's prose was written; the printed numbers are byte-exact outputs of the recorded runs (receipts 54runs-1..11, kept in the session buffer). Where a code sketch is shown, it is the essence of the engine that produced the receipt — compacted to fit the page, faithful to the algorithm, with the receipt carrying the full record.

### Part 1 — Orbit censuses: necklaces, bracelets, the cube, the trees (Lecture 1)

```typescript
// Necklaces: brute force = canonicalize every 2^n string over all n rotations,
// collect lex-min representatives; Burnside = (1/n)·Σ_{k=0..n−1} 2^gcd(n,k).
// Bracelets: same + the n reflections of the dihedral group; Burnside side:
//   n odd:  reflections fix 2^((n+1)/2) each;  n even: (n/2)·2^(n/2+1) + (n/2)·2^(n/2).
// Cube: the rotation group = closure of the two quarter-turns (F L B R) and
// (U R D L); 24 elements machine-tallied by cycle type on faces:
//   1⁶:1, 2²1²:3, 2³:6, 3²:8, 4·1²:6; orbit count = Σ k^{cycles}/24 both ways.
// Trees: rooted = sorted-multiset closure; unrooted = centroid/bicentroid split;
// cross-check = full Prüfer enumeration n^{n−2} with canonical-form dedup.
```

**Verified output.** Necklaces n = 1..12, brute = Burnside at every n: **2, 3, 4, 6, 8, 14, 20, 36, 60, 108, 188, 352**. Bracelets n = 1..12, brute dihedral = Burnside over D_n at every n: **2, 3, 4, 6, 8, 13, 18, 30, 46, 78, 126, 224**; the necklace/bracelet contrast prints 14 vs 13 at n = 6 and 352 vs 224 at n = 12. Cube: |G| = 24 verified; k = 1..5 face-coloring orbits **1, 10, 57, 240, 800**, brute canonicalization = the closed form (k⁶+3k⁴+12k³+8k²)/24 at every k. Tree shapes n = 1..8: unrooted **1, 1, 1, 2, 3, 6, 11, 23**, rooted **1, 1, 2, 4, 9, 20, 48, 115**; the Prüfer cross-check agrees at every n. *(Receipt 54runs-1, extended by 54runs-9 K1.)*

### Part 2 — The Möbius battery (Lecture 2)

```typescript
// Divisor lattice, every n ≤ 10⁴: Σ_{d|n} 1 = τ(n); Σ_{d|n} μ(d) = [n=1];
// Σ_{d|n} d·μ(n/d) = φ(n); Σ_{d|n} φ(d) = n. Boolean B_k, k ≤ 6: μ(∅,S) = (−1)^{|S|}.
// Partition lattice Π_n, n ≤ 5: full element tally + μ(0̂,1̂) by the recursion
//   μ(x,y) = −Σ_{x≤z<y} μ(x,z)   // exclude z = y; accumulate from x upward
```

**Verified output.** All four divisor identities: **zero mismatches over every n ≤ 10,000** (spot values τ(60) = 12, φ(60) = 16, φ(100) = 40). Boolean: μ(∅, S) = (−1)^{|S|} on all intervals of B_6 (all 64 subsets walked). Partition lattices: **|Π_n| = 1, 2, 5, 15, 52** and **μ(0̂,1̂) = 1, −1, 2, −6, 24** = (−1)^{n−1}(n−1)! at every n. Implementation scars on the receipt: the recursion direction (μ(x,y) = −Σ_{x≤z<y} μ(x,z), accumulated upward from x — the first draft ran it downward and produced garbage the identity checks caught), the z = y self-inclusion trap, and the φ-sieve initialization (φ[m] = m before the sieve starts). *(Receipt 54runs-2.)*

### Part 3 — Steiner triple systems: the small census, the exhibit, the fork (Lectures 3–4)

```typescript
// STS(v) labeled census: exact cover of all C(v,2) pairs by triples, with
// propagation + undo; isomorphism by canonical relabeling.
// S(2,3,6): exhaustive over all C(20,5) = 15,504 candidate block families.
// STS(13): orderly generation — branch on the lowest uncovered pair; candidates
// canonicalized under Stab(partial) ∩ the pair-stabilizer; every leaf valid.
// Pasch counter: the four-triple quadrilateral, counted per system.
```

**Verified output.** STS(7): **30 labeled systems**, one isomorphism class — the Fano plane unique (7 Pasches). STS(9): **840 labeled**, one orbit (0 Pasches — AG(2,3)). S(2,3,6): **0 of 15,504** — the non-existence machine proof (r = 5/2 the obstruction). STS(13): the orderly search visits **41,621 nodes and 560 leaves, all valid**; leaves sort into Pasch buckets **468 (8 Pasches) + 92 (13 Pasches)**; two isomorphism classes with **|Aut| = 6 and 39**; labeled counts **1,037,836,800 + 159,667,200 = 1,197,504,000**. Fisher on every found system: b ≥ v, tight at 7, slack at 9, 13. *(Receipts 54runs-3, 54runs-4.)*

### Part 4 — Quadruple systems and the schoolgirls (Lecture 4)

```typescript
// SQS(v) labeled census: exact cover of all C(v,3) triples by quadruples,
// propagation + undo; uniqueness = one orbit under the full symmetric group;
// |Aut| counted per representative (labeled total = v!/|Aut| when unique).
// PG(3,2): points = nonzero 4-bit vectors 1..15; lines {a,b,a XOR b}; spreads =
// 5 disjoint lines covering all 15 points (masks ≤ 15 bits — the 32-bit lesson:
// 35-bit line masks wrapped in the first draft and printed 52 spreads, an
// impossibility its own arithmetic exposed; fixed masks → 56).
// Parallelism: 7 spreads pairwise disjoint as line sets, covering all 35 lines.
```

**Verified output.** SQS(8): **30 labeled systems, one orbit — unique; |Aut| = 1,344 = AGL(3,2)** (30·1,344 = 8! exactly). SQS(10): **2,520 labeled, one orbit — Barrau's 1908 uniqueness machine-confirmed; |Aut| = 1,440 = PΓL(2,9)** (2,520·1,440 = 10! exactly; the remembered "15,120 labeled / |Aut| 240" was WRONG and the machine overruled it — recorded on the receipt). PG(3,2): 35 lines form STS(15) — all 105 pairs in exactly one line; **56 spreads**; the resolvable parallelism FOUND: 7 parallel classes × 5 disjoint triples, all 35 lines used once, every class a partition of the 15 points — the schoolgirl schedule:

- Mon: {1,2,3} {4,8,12} {5,10,15} {6,11,13} {7,9,14}
- Tue: {1,4,5} {2,8,10} {3,13,14} {6,9,15} {7,11,12}
- Wed: {1,6,7} {2,9,11} {3,12,15} {4,10,14} {5,8,13}
- Thu: {1,8,9} {2,12,14} {3,5,6} {4,11,15} {7,10,13}
- Fri: {1,10,11} {2,13,15} {3,4,7} {5,9,12} {6,8,14}
- Sat: {1,12,13} {2,4,6} {3,9,10} {5,11,14} {7,8,15}
- Sun: {1,14,15} {2,5,7} {3,8,11} {4,9,13} {6,10,12}

*(Receipts 54runs-5, 54runs-10.)*

### Part 5 — Code bounds: greedy, simplex, puncturing (Lecture 5)

```typescript
// GV greedy: start from any word, repeatedly add any word at distance ≥ d from
// all chosen; halt when the radius-(d−1) balls cover the cube.
// Plotkin witnesses: (6,4) = 4 and (7,4) = 8 — the simplex built as the dual of
// the Hamming code (all 7 nonzero codewords weight 4).
// Binary MDS census n ≤ 7: canonical subspace enumeration with RREF keys
// (post-elimination rows — a pre-elimination key bug was caught by a Gaussian
// cross-check on the recorded first version).
// RS over F₅: evaluate a+bx at 4 and at 5 field points; pairwise distances.
// Hamming [7,4,3]: parity-check columns = the 7 nonzero 3-bit vectors;
// syndrome s_j = XOR_i (w_i AND column_i[j]) — the first draft ANDed instead
// of XOR-accumulating and returned 64 bogus codewords (its own perfectness
// check, 64/128, exposed it).
```

**Verified output.** GV greedy: (7,3): **16 ≥ ⌈128/29⌉ = 5**; (8,3): **16 ≥ 7**; (10,4): **32 ≥ ⌈1024/176⌉ = 6**; (12,4): **128 ≥ ⌈4096/299⌉ = 14**. Plotkin: **(6,4) = 4** and **(7,4) = 8** met exactly, the simplex saturating. Binary MDS census n ≤ 7: subspace counts = the Gaussian binomials **35, 155, 651, 1,395, 2,667, 11,811** (the nontrivial pairs (n, k) = (4,2), (5,2), (6,2), (6,3), (7,2), (7,3)), maximum distance strictly below Singleton for every nontrivial dimension; only the three trivial families reach equality. RS over F₅: **[4,2,3]₅** — 25 words, machine minimum pairwise distance exactly 3 = Singleton; **[5,2,4]₅** — distance 4 = Singleton. Hamming [7,4,3]: **16 codewords, d = 3, A = [1, 0, 0, 7, 7, 0, 0, 1], perfect — 16 radius-1 balls of size 8 partition F₂⁷ (16·8 = 128 = 2⁷)**. Keevash arithmetic: S(3,4,10) admissible (30, 12, 4 all integers), S(3,4,12) fails at 55/3; census n = 4..60 matches n ≡ 2, 4 (mod 6) exactly. *(Receipts 54runs-6, 54runs-11.)*

### Part 6 — The Golay codes and their designs (Lecture 6)

```typescript
// Ternary: Φ₁₁ = 1+x+…+x¹⁰ over F₃ factors into two monic quintics
//   (x⁵+x⁴+2x³+x²+2)(x⁵+2x³+x²+2x+2) — machine-factored, not remembered;
// either generates [11,6,5]: 729 words, perfect (729 balls of radius 2,
// volume 1+2·11+4·55 = 243, partition F₃¹¹: 729·243 = 3¹¹).
// Extension: one overall-parity coordinate → [12,6,6], self-dual.
// Binary: (x²³+1)/(x+1) over F₂ factors into exactly two monic degree-11
// polynomials g₀, g₁ (machine-found); either generates [23,12,7]: 4,096 words,
// min pairwise distance 7 verified over all 8,386,560 pairs; perfect
// (4096·V(23,3) = 4096·2048 = 2²³). Extension → [24,12,8], self-dual.
// Design extraction: supports of constant-weight words; coverage test = every
// 5-subset of 24 coordinates in exactly one octad support.
```

**Verified output.** Ternary [11,6,5]₃ (both factors): **A = 1, 132, 132, 330, 110, 24** at weights 0, 5, 6, 8, 9, 11; **132 weight-5 words on 66 supports = S(4,5,11)** (every 4-subset in exactly one support); the [12,6,6]₃ extension: **A = 1, 264, 440, 24**, self-dual, **132 weight-6 supports = S(5,6,12)**. Binary [23,12,7]₂ (both factors g₀ = x¹¹+x⁹+x⁷+x⁶+x⁵+x+1, g₁ = x¹¹+x¹⁰+x⁶+x⁵+x⁴+x²+1): **A = 1, 253, 506, 1288, 1288, 506, 253, 1** at weights 0, 7, 8, 11, 12, 15, 16, 23, perfect; the [24,12,8]₂ extension: **A = 1, 759, 2576, 759, 1** at 0, 8, 12, 16, 24, self-dual; **759 octads, and each of the C(24,5) = 42,504 coordinate 5-subsets lies in exactly one octad = S(5,8,24)**. Mathieu arithmetic: **M₂₄ = 244,823,040 = 2¹⁰·3³·5·7·11·23**; M₂₃ = 10,200,960 = M₂₄/24; M₂₂ = 443,520 = M₂₃/23; M₁₂ = 95,040; M₁₁ = 7,920 = M₁₂/12; |M₂₄|/759 = 322,560; |M₁₂|/132 = 720. *(Receipts 54runs-7, 54runs-8, 54runs-11.)*

## Revision History & Verification Notes

**Machine-verification campaign (before a line of prose was installed).** Eleven recorded batches — receipts 54runs-1..11, kept in the session buffer — with every quantitative claim in this chapter traceable to one:

1. **Orbit censuses** (runs 1, 9): necklaces and bracelets n = 1..12 brute-versus-Burnside agreement at every n; the cube's 24 rotations, cycle-type census, and the k = 1..5 orbit counts 1, 10, 57, 240, 800; tree shapes 1, 1, 1, 2, 3, 6, 11, 23 with the Prüfer cross-check (rooted 115 at n = 8).
2. **Möbius battery** (run 2): the four divisor identities over all n ≤ 10⁴ (zero mismatches); Boolean μ on B_6; the partition lattices to Π₅ with μ(0̂,1̂) = 1, −1, 2, −6, 24.
3. **Small designs** (runs 3, 4): STS(7) 30/1, STS(9) 840/1; S(2,3,6) = 0 of 15,504 — the machine non-existence proof; STS(13) = 2 by orderly generation over 41,621 nodes / 560 leaves with the Pasch buckets 468 + 92, |Aut| 6 and 39, labeled total 1,197,504,000; Fisher on every system.
4. **Quadruple systems + schoolgirls** (runs 5, 10): SQS(8) 30 labeled / unique / |Aut| = 1,344; SQS(10) 2,520 / unique / |Aut| = 1,440; PG(3,2): 35 lines = STS(15), 56 spreads, the full 7-class resolvable parallelism verified class by class.
5. **Code bounds** (runs 6, 11): GV greedy witnesses at four parameter points; Plotkin tight at (6,4) = 4 and (7,4) = 8 simplex; the binary MDS census n ≤ 7 (Gaussian cross-checked); Reed–Solomon [4,2,3]₅ and [5,2,4]₅ Singleton-tight; Hamming [7,4,3] with distribution [1,0,0,7,7,0,0,1] and perfectness 128/128.
6. **The Golay bridge** (runs 7, 8, 11): both Φ₁₁ factors → [11,6,5]₃ perfect with A = 1, 132, 132, 330, 110, 24, 66 supports = S(4,5,11), extension [12,6,6]₃ self-dual with 132 supports = S(5,6,12); both degree-11 binary factors → [23,12,7]₂ perfect (A₇ = 253, A₈ = 506, A₁₁ = A₁₂ = 1288, A₁₅ = 506, A₁₆ = 253, A₂₃ = 1), extension [24,12,8]₂ self-dual with A = 1, 759, 2576, 759, 1, 759 octads = S(5,8,24) with all 42,504 five-subsets covered exactly once; the Mathieu order ladder.
7. **The BRC arithmetic** (run 9): PG(2,3) = S(2,4,13) with all 78 pairs machine-checked and b = v = 13; the sum-of-two-squares census q = 2..16.

**The scars, kept on display.** The campaign's own oracles caught, before any number reached prose: the μ-recursion direction and the z = y self-inclusion (run 2's identity checks); the RREF key bug in the MDS census (a Gaussian cross-check on recorded subspaces); the ternary synthetic-division sign error — a negacyclic twin that passed the [11,6,5] test but whose extension failed self-duality, and the run refused to proceed past the failed check (run 7); the hand-transcribed binary factor that dropped its leading x¹¹ — the machine-found factorization was right and the transcription wrong (run 8); the SQS(10) remembered figures (15,120 labeled / 240) that the machine overruled with 2,520 / 1,440 (run 5) — receipts, not memory; the 32-bit bitwise mask trap, hit for the third time in the Atlas at the PG(3,2) spread census — 35-bit line masks wrapped at bit 32 and printed 52 spreads, and the tell was arithmetic, not visual: line-transitivity forces every line into equally many spreads, so 5·(#spreads) = 35·(per-line count) and the spread count must be a multiple of 7; 52 is not; fixed with short masks → 56 (run 10); the PG(2,3) collinearity test — the det≡0 shortcut and the affine-proportionality shortcut were both wrong (projective points live on representatives up to scaling; the rank-2 test is the correct one) (run 9); the Hamming syndrome AND-for-XOR wiring bug, exposed by its own perfectness counter (run 11); and the Mathieu M₂₃ product with a stray factor of 4, exposed by the M₂₄/24 cross-check line (run 11).

**Canon pins (verified before authoring).** Burnside's lemma: Cauchy 1845 / Frobenius 1887; Burnside's 1897 textbook (Stigler's law recorded). Pólya: Redfield 1927 (priority), Pólya 1937 ("Kombinatorische Anzahlbestimmungen für Gruppen, Graphen und chemische Verbindungen"). Rota, "On the foundations of combinatorial theory I. Theory of Möbius functions", *Z. Wahrscheinlichkeitstheorie verw. Gebiete* 2 (1964), 340–368. Kirkman 1846 (solving Woolhouse 1844; the journal volume is 1847 — cited "Kirkman 1846/47"); Steiner 1853; STS existence iff v ≡ 1, 3 (mod 6) (Bose 1939, Skolem 1958); Kirkman's schoolgirl problem 1850; Sylvester's extension — Denniston, *Discrete Math.* 9 (1974), 229–233. Fisher, "An examination of the different possible solutions of a problem in incomplete blocks", *Annals of Eugenics* 10 (1940), 52–75; Bose's alternative proof (Chapter 6's dual presentation). Bruck–Ryser 1949; Chowla–Ryser 1950; order 10: Lam–Thiel–Swiercz 1989; order 12 open. STS(19) = 11,084,874,829: Kaski–Östergård 2004 (Stinson–Ferch 1985 the forerunner). Wilson, "An existence theory for pairwise balanced designs" I–III (early 1970s); Keevash, "The existence of designs", arXiv:1401.3665 (2014). Hanani 1960 (*Canad. J. Math.* 12, 145–157) and 1963 (15, 702–722); Barrau 1908 (uniqueness of S(3,4,8) and S(3,4,10)); SQS(16) = 1,054,163; S(4,5,v) unique at 11, smallest open 21. Singleton 1964 (*IEEE Trans. Inf. Theory* 10(2), 116–118; earlier proofs Joshi 1958, Komamiya 1953 — priority recorded); MDS conjecture: Segre 1955; prime case Ball 2012 (*J. Eur. Math. Soc.* 14, 733–748); Ball–De Beule 2012 (*Des. Codes Cryptogr.* 65, 5–14). Plotkin 1960 (*IRE Trans. Inf. Theory* 6(4), 445–450; Chapter 8 owns the Delsarte-certificate form — cross-referenced, not re-proved). Gilbert 1952 (*Bell System Tech. J.* 31(3), 504–522); Varshamov 1957 (*Dokl. Akad. Nauk SSSR* 117, 739–741). Golay 1949 ("Notes on Digital Coding", *Proc. IRE* 37, 657); Virtakallio 1947 (the football-pool magazine Veikkaaja — priority recorded); Berlekamp's "best single published page" verdict. Assmus–Mattson, "New 5-designs", *J. Combin. Theory* 6 (1969), 122–151. Mathieu M₂₄/M₁₂ 5-transitivity and the CFSG uniqueness of the Mathieu groups among 4-transitive groups — cited. Cross-references: Chapter 2 (Cayley's formula, the X1 tree-shape exploration, "Pólya's machine" named there), Chapter 6 (Fisher's inequality two ways — the Gram determinant route and Bose's argument), Chapter 8 (the Hamming cube, the [7,4,3] distribution, Delsarte's program).

**The honest ledger.** Proved in the text: Burnside's lemma; Pólya's theorem (from the fixed-point form); the divisor Möbius inversion formula and the poset version via the incidence algebra; the design counting constants (double counting); the v ≡ 1, 3 (mod 6) necessity and the S(2,3,6) non-existence; the projective-plane duality argument (dimension formula); the resolvability parameter count (7 classes of 5); the Singleton bound (puncturing); the Plotkin bound (averaging with the two parity refinements; the boundary case n = 2d by shortening, as of session 109); the Gilbert–Varshamov bound (greedy covering); the RS distance argument; the octad arithmetic (759·56 = 42,504). Stated with proof cited, not given: the STS existence theorem (Bose/Skolem); Fisher's inequality (Chapter 6); Bruck–Ryser–Chowla; the Lam–Thiel–Swiercz order-10 result; Wilson's and Keevash's theorems; Hanani's iff theorem; Barrau's uniqueness; the MDS conjecture and Ball's prime-case theorem; the Assmus–Mattson theorem; the CFSG 4-transitivity classification. Computed, not proved: every census, witness, factorization, and schedule in the lab — reproducible bit for bit from the receipts. The four proposed pattern-registry entries (Symmetry averaging, Möbius inversion, Double-counting/divisibility, Words-as-designs) are filed at ship.

**Expansion pass (session 109, the first for this chapter).** The user-supplied expansion draft was audited against this master section by section; every adoptable claim re-verified by a fresh machine battery before install. Installed: the full divisor-sum proof of Σ_{d|n} μ(d) = [n=1] and the inversion re-indexing (L2.1, previously deferred to an exercise); the restated poset-inversion theorem with lower bound and dual, with the explicit incidence-algebra proof μ∗ζ = δ (L2.2); the Boolean generalization μ(T,S) = (−1)^{|S∖T|} (L2.3 — battery-verified on all 4,096 interval pairs of B₆); the full λ-coloring proof of μ(0̂,1̂) = (−1)^{n−1}(n−1)! on Π_n (L2.3, previously cited only); Fisher's guards (2 ≤ k < v, λ ≥ 1) and the explicit det(NN^T) (L3.3); the Bruck–Ryser attribution precision (planes 1949, the symmetric-design generalization 1950, L3.4); Sylvester's 13-week large-set statement spelled out (455 = C(15,3) = 13·35, L4.1); Wilson's divisibility conditions explicit (L4.2); Singleton's guard and the RS point-at-infinity witness [6,2,5]₅ (L5.2, machine-verified); the two-tier Plotkin theorem with the parity proof and the boundary case proved by shortening (L5.3 — the master's boundary claim was true but unproven in the text; A(8,4) = 16 certified exhaustively, killing the misremembered "Best ≈ 20 at (8,4)" worry: Best's 20-word code has length nine); the S(5,6,12) mechanism (264 weight-6 words pair onto 132 supports) and the "5-design of the small Witt pair" phrasing (L6.2 — repairing the garbled "large small-Witt design"). Repairs the draft exposed in the master: the transposed design-constant equation in L3.1 (r·C(v−1,t−1) = λ·C(k−1,t−1) → r·C(k−1,t−1) = λ·C(v−1,t−1), which at t = 2 gives the r the Trick Bag always carried); the pattern map's "132 weight-6 words of the ternary Golay" → supports of the extended code. Pattern-reference audit verdict, honestly recorded: the pattern references were never mangled — P10 appears at exactly its three sites, the four unlabeled "(new this chapter)" rows are the registry's P39–P42 by the Ch. 15/16 ship convention, and "Pólya's machine" fires once in the preface; the unlabeled convention is kept (the registry's forward-rows and the reverse index's "none yet" state are keyed to it). Fresh battery (all green, receipts in the session record): exact A(2,1) = 4, A(4,2) = 8, A(5,3) = 4, A(6,3) = 8, A(6,4) = 4, A(7,4) = 8, A(7,5) = 2, A(8,5) = 4, A(8,6) = 2, A(8,4) = 16, A(9,5) = 6 (exhaustive branch-and-bound, 0 in every code by translation); ternary Φ₁₁ factorization re-verified, [11,6,5] and its [12,6,6] extension (self-dual, 1/264/440/24), S(4,5,11) and S(5,6,12) full coverage censuses; binary [23,12,7]/[24,12,8] weight enumerators and the S(5,8,24) census; the Möbius battery re-run (zero mismatches n ≤ 10,000; Π_n sizes and μ values); the Paley–Hadamard (12,24,6) witness; RS [4,2,3]₅/[5,2,4]₅/[6,2,5]₅; the Wilson/Keevash/Sylvester/GV/Mathieu arithmetic. Two checker scars on the battery, caught and fixed before any install was trusted: a popcount table sized 2¹⁴ fed 23-bit codewords (weights read as undefined), and an OR where XOR belonged in a witness builder.

---

**Status:** 🟩 Feynman edition — installed (session 54, chunks 54a–54h: session open, canon pins, verification campaign batches 1–11, design lock, authoring, assembly + install, web edition build, closeout + pattern-registry installs); first expansion pass installed (session 109). The web edition `cgt-ch16-web` and the .html export were built at 54g and rebaked at 109. No claim in this chapter predates its receipt.
