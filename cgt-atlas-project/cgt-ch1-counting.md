---
name: "cgt-ch1-counting"
title: "Ch. 1 — Counting: A Lecture Course in the Feynman Style"
type: "text/markdown"
---

# Chapter 1 · Counting

*A lecture course, in the spirit of Feynman's physics lectures: the idea before the formula, the story before the proof, and the proof as a conversation. A compact reference card follows the lectures; graded exercises, a computational lab and worked answers close the chapter.*

## How to read this chapter

Read it slowly, with a pencil. Whenever a small number appears in front of you — *compute it yourself before reading on*. This chapter is a conversation, and you must do your half. Nothing here requires genius; it requires only the patience to count carefully, which is the entire secret of combinatorics. Lines marked **✎ Checkpoint** are the places to stop and predict: commit to a guess — in ink — before reading on. A checked guess teaches; a passively read reveal only feels like learning.

**The exercises are graded:** ●○○ *easy* (a direct application of one lecture idea), ●●○ *moderate* (two ideas, or one tricky step), ●●● *tough* (several chapter ideas combined). Hints travel with the problems; worked answers sit at the very end of the chapter. Try honestly before reading a hint — the struggle is the part of learning that cannot be outsourced. Beyond the graded set, ◐ **Explorations** at the end are open-ended investigations with no single right answer — research training, not test preparation.

---

## Lecture 1 · Ten Letters, Ten Wrong Envelopes

Here is a problem posed around 1708 by Pierre Rémond de Montmort, and it caused a surprising amount of trouble: *You have n letters and n addressed envelopes. In how many ways can you put every letter into a **wrong** envelope?*

A permutation with no fixed point is called a **derangement**, and the count is written D_n. Before we know anything, let us feel the numbers. Take n = 2: the only way to get both wrong is to swap them — D₂ = 1. For n = 3, try it: the two 3-cycles (2,3,1) and (3,1,2) — each list (π(1),π(2),π(3)) says where letters 1, 2, 3 go — put every letter in a wrong envelope, and everything else leaves at least one letter at home (namely, the one-line list (1,2,3) leaves all three letters at home, while (1,3,2), (3,2,1), and (2,1,3) leave letters 1, 2, and 3 at home respectively), so D₃ = 2. For n = 4 you can grind it out: D₄ = 9 (every derangement of {1,2,3,4} has cycle lengths all at least 2, so written as a one-line list (π(1),π(2),π(3),π(4)) it is either one of the (4−1)! = 6 four-cycles — (2,3,4,1), (2,4,1,3), (3,1,4,2), (3,4,2,1), (4,1,2,3), (4,3,1,2) — or one of the ½·C(4,2) = 3 products of two disjoint transpositions — (2,1,4,3) swapping 1 ↔ 2, 3 ↔ 4; (3,4,1,2) swapping 1 ↔ 3, 2 ↔ 4; and (4,3,2,1) swapping 1 ↔ 4, 2 ↔ 3 — totaling 6 + 3 = 9). From n = 2 the sequence runs 1, 2, 9, 44, 265, 1854, … and it grows almost as fast as the factorial. Already something is strange: "get everything wrong" turns out to be *far from rare — a sizeable fraction of all the arrangements there are*.

Now — how would you attack this? Let me show you three attacks, and I promise each one is something you could have invented.

### 1.1 First attack: count the complement — but carefully

There are n! arrangements in all. The ones we want are the complement of "at least one letter lands home." Fine: count the arrangements where letter 1 is home, letter 2 is home, and so on, and subtract. Let's do n = 4 by hand, because the danger shows up immediately.

"Letter i is home" happens in 3! ways for each fixed i — that's 4 × 6 = 24. Subtract from 24 total: 24 − 24 = 0?? Already nonsense — the answer is 9, not 0. **What went wrong?** A permutation with *two* letters home was counted twice, once for each letter. The events overlap, and overlapping events must not be counted with a plain subtraction.

So we repair it, and the repair is the whole method: *add back the double overlaps, subtract the triple overlaps, add back the quadruple…* For n = 4: (4 × 3!) − (C(4,2) × 2!) + (C(4,3) × 1!) − (1 × 0!) = 24 − 12 + 4 − 1 = 15 arrangements with at least one letter home. The complement: 24 − 15 = **9** ✓.

Do you see the mechanism? Add, subtract, add, subtract — **alternate**. Counting the complement of a union of overlapping events is a zigzag. Let us prove that this zigzag gives the exact count D_n for every n, not just n = 4. For each subset S ⊆ {1, …, n} of size k, the number of arrangements that place at least the letters of S into their own envelopes is (n−k)!, because the k letters in S are fixed and the remaining n−k letters may be arranged in any order. Since there are C(n,k) ways to choose the k-element subset S, the k-th level sum across all k-tuples of letters is C(n,k)·(n−k)!. Now follow any single arrangement π through the alternating sum

Σ_{k=0}^{n} (−1)^k · C(n,k) · (n−k)!.

Suppose π puts exactly m letters into their correct envelopes. At level k, the arrangement π is counted once for every k-element subset S chosen from its m fixed letters — that is, C(m,k) times for k ≤ m, and 0 times for k > m. The total net weight contributed by π to the alternating sum is therefore

Σ_{k=0}^{m} (−1)^k · C(m,k).

If m = 0 (so π is a derangement), this sum consists of the single term (−1)⁰·C(0,0) = 1, so every derangement is counted with weight 1. If m ≥ 1 (so π puts at least one letter home), the binomial theorem (1 + x)^m = Σ_{k=0}^{m} C(m,k)·x^k evaluated at x = −1 gives

Σ_{k=0}^{m} (−1)^k · C(m,k) = (1 − 1)^m = 0,

so every arrangement with one or more fixed letters cancels out completely. Finally, expanding C(n,k) = n!/(k!·(n−k)!) cancels the (n−k)! factors: C(n,k)·(n−k)! = n!/k!. We have proved:

**D_n = Σ_{k=0}^{n} (−1)^k · C(n,k) · (n−k)! = n! · Σ_{k=0}^{n} (−1)^k/k!**  — *inclusion–exclusion* (pattern **P3**).

**✎ Checkpoint.** Own the zigzag before moving on. Compute D₅ by hand: 120 − 5·24 + 10·6 − 10·2 + 5·1 − 1. Then compute the two fractions D₅/5! = 44/120 and D₄/4! = 9/24 — and notice how close together they already sit. Pocket that observation; §1.4 will explain it. Explicitly, the alternating terms evaluate to 120 − 120 + 60 − 20 + 5 − 1 = 44, so D₅ = 44. In decimal form, D₄/4! = 9/24 = 0.375 and D₅/5! = 44/120 = 11/30 ≈ 0.3667, differing by only |9/24 − 44/120| = 1/120 = 1/5!.

### 1.2 Second attack: explain the objects to themselves

The formula above is an *answer*. But a recurrence is an *explanation*, and explanations are worth more. Follow letter number 1. It must land in some envelope i ≠ 1: there are n − 1 choices.

**✎ Checkpoint.** Try the rest yourself before reading on: what can you say about where letter *i* goes? Find the two possible situations — one is a plain swap, and one hides a relabeling that is the entire trick.

Now there are exactly two situations:

1. **Envelope 1 gets letter i back** — a swap. The remaining n − 2 letters must all go wrong among themselves: D_{n−2} ways. Formally, for every n ≥ 2 and fixed i ∈ {2, …, n}, let ℬ_i be the set of derangements π of {1, …, n} with π(1) = i and π(i) = 1. Since π maps {1, i} bijectively onto {1, i}, restricting π to the remaining (n−2)-element set U_i = {1, …, n} ∖ {1, i} gives a permutation π|_{U_i} of U_i with π(j) ≠ j for all j ∈ U_i. Conversely, extending any derangement τ of U_i by setting π(1) = i and π(i) = 1 yields a derangement in ℬ_i. Because relabeling U_i in increasing order by {1, …, n−2} preserves fixed points, |ℬ_i| = D_{n−2} (with D₀ = 1 when n = 2, corresponding to the single swap (2,1)).
2. **Envelope 1 does not get letter i.** Then **remove letter 1 and envelope i** — both are spent — and **relabel envelope 1 as i**. Now letter i is forbidden the relabelled envelope i, and every other remaining letter is forbidden its own envelope: *exactly the derangement problem one size down*, D_{n−1} ways. (Check the bookkeeping on n = 3: letter 1 → envelope 3, and letter 3 avoids envelope 1. Remove letter 1 and envelope 3; relabel envelope 1 as "3". Now letters {2, 3} must derange on envelopes {2, 3*} — D₂ = 1 way ✓, namely letter 2 → envelope 1 and letter 3 → envelope 2.) To verify formally that this relabeling is a bijection for every n ≥ 2 and fixed i ∈ {2, …, n}, let 𝒜_i be the set of derangements π of {1, …, n} with π(1) = i and π(i) ≠ 1, and let 𝒟′ be the set of all derangements σ of the (n−1)-element set {2, …, n}. When n = 2 (so i = 2), any permutation π of {1, 2} with π(1) = 2 must have π(2) = 1, so 𝒜₂ = ∅, and simultaneously {2} has no derangements (𝒟′ = ∅), so the empty map is vacuously a bijection between 𝒜₂ and 𝒟′ with |𝒜₂| = |𝒟′| = D₁ = 0. For n ≥ 3, define Φ_i : 𝒜_i → 𝒟′ by setting, for each j ∈ {2, …, n}, Φ_i(π)(j) = i if π(j) = 1, and Φ_i(π)(j) = π(j) if π(j) ≠ 1. Since π is a bijection from {2, …, n} onto {1, …, n} ∖ {i} and replacing the unique output value 1 = π(j₀) (achieved at a unique j₀ ∈ {2, …, n} ∖ {i} since π(i) ≠ 1) with i is a bijection from {1, …, n} ∖ {i} onto {2, …, n}, the map σ = Φ_i(π) is a permutation of {2, …, n}. Moreover, σ has no fixed points: for j ≠ i, we had π(j) ≠ j and j ≠ i, so σ(j) ≠ j; for j = i, the hypothesis π(i) ≠ 1 ensures σ(i) = π(i) ≠ i (because π(i) ≠ i as π is a derangement, and π(i) ≠ 1 so the replacement to i does not occur). Conversely, for n ≥ 3, given any derangement σ ∈ 𝒟′, define Ψ_i(σ) on {1, …, n} by setting Ψ_i(σ)(1) = i and, for j ∈ {2, …, n}, Ψ_i(σ)(j) = 1 if σ(j) = i and Ψ_i(σ)(j) = σ(j) if σ(j) ≠ i. Because σ is a derangement of {2, …, n}, the value i is achieved at a unique index j₁ ∈ {2, …, n} ∖ {i} (giving Ψ_i(σ)(j₁) = 1 ≠ j₁). Since σ(i) ≠ i, we have Ψ_i(σ)(i) = σ(i) ≠ 1, and for all j ∈ {2, …, n} we have Ψ_i(σ)(j) ≠ j, so Ψ_i(σ) ∈ 𝒜_i. Clearly Ψ_i(Φ_i(π)) = π and Φ_i(Ψ_i(σ)) = σ, proving |𝒜_i| = |𝒟′| = D_{n−1}.

**D_n = (n−1)(D_{n−1} + D_{n−2})** (since for every integer n ≥ 2, the set 𝒟_n of derangements of {1, …, n} partitions by the image i = π(1) ∈ {2, …, n} and whether π(i) = 1 or π(i) ≠ 1 into the 2(n−1) pairwise disjoint subsets 𝒟_n = ⨆_{i=2}^{n} (𝒜_i ⊔ ℬ_i), giving D_n = Σ_{i=2}^{n} (|𝒜_i| + |ℬ_i|) = Σ_{i=2}^{n} (D_{n−1} + D_{n−2}) = (n−1)(D_{n−1} + D_{n−2})). Check: D₄ = 3 × (2 + 1) = 9 ✓. (Two seeds power the machine: D₀ = 1 — the empty arrangement — and D₁ = 0 — a single letter cannot go wrong alone. The recurrence then produces D₂ = 1·(0 + 1) = 1, the swap, and the whole sequence is pinned.) This little machine *explains* why the numbers grow: each derangement is built from smaller derangements plus one honest choice. (Pattern **P4**: recurrence built by following a forced case analysis.)

### 1.3 Third attack: package the whole sequence into one object

Here is a thought that looks lazy and is secretly profound. Every permutation is: a **set** of letters left in their correct envelopes, glued to a derangement of the rest. Explicitly, for every integer n ≥ 0, any permutation π of {1, …, n} determines its fixed-point set S = Fix(π) = {j ∈ {1, …, n} : π(j) = j} of size k ∈ {0, …, n}, and restricting π to the complement {1, …, n} ∖ S yields a permutation with no fixed points — a derangement of the remaining n − k labels. Conversely, for any k-element subset S ⊆ {1, …, n} (chosen in C(n,k) ways, with a_k = 1 way to leave every element of S fixed) and any derangement σ of {1, …, n} ∖ S (chosen in b_{n−k} = D_{n−k} ways), gluing the identity map on S to σ on {1, …, n} ∖ S reconstructs a unique permutation π with Fix(π) = S, proving n! = Σ_{k=0}^{n} C(n,k)·1·D_{n−k} (for n = 3: C(3,0)·D₃ + C(3,1)·D₂ + C(3,2)·D₁ + C(3,3)·D₀ = 1·2 + 3·1 + 3·0 + 1·1 = 6 = 3! ✓). Sets of letters are counted by 1 + x + x²/2! + … = e^x. All permutations are counted by 1/(1−x) = Σ n! xⁿ/n!. So if D(x) = Σ D_n xⁿ/n! is the derangement bookkeeping machine:

e^x · D(x) = 1/(1−x), that is, **D(x) = e^{−x}/(1−x)**.

One line — but *why* may we multiply? Because gluing two structures built on disjoint label sets obeys a clean law, and the law is double counting in disguise. If structure A can be built on k of the n labels — chosen in C(n,k) ways — and structure B on the remaining n−k, then the number of glued structures is Σ_k C(n,k)·a_k·b_{n−k}: the binomial coefficient's whole job is to **choose which labels belong to A**. And multiplying the bookkeeping machines performs exactly this sum, term by term:

**(Σ a_n xⁿ/n!) · (Σ b_n xⁿ/n!) = Σ_n [Σ_k C(n,k)·a_k·b_{n−k}] xⁿ/n!**.

Indeed, multiplying the k-th term a_k x^k/k! of the first series by the (n−k)-th term b_{n−k} x^{n−k}/(n−k)! of the second series and inserting 1 = n!/n! yields

a_k/k! · b_{n−k}/(n−k)! · x^n = n!/(k!·(n−k)!) · a_k · b_{n−k} · xⁿ/n! = C(n,k) · a_k · b_{n−k} · xⁿ/n!,

and summing over 0 ≤ k ≤ n collects the entire coefficient of xⁿ/n!.

So the sentence "every permutation is a set of fixed letters glued to a derangement of the rest" translates *mechanically* into e^x · D(x) = 1/(1−x), or D(x) = e^{−x} · 1/(1−x). When you know the product law, the algebra writes itself. Now unpack the coefficient of x^n on both sides by multiplying the two Taylor series

e^{−x} = Σ_k (−1)^k/k! · x^k and 1/(1−x) = Σ_m x^m.

A term of degree n in the product arises by pairing the x^k term of e^{−x} with the x^{n−k} term of 1/(1−x), for each k ∈ {0, 1, …, n}, and the coefficient of x^n in the product is therefore

D_n/n! = Σ_{k=0}^{n} (−1)^k/k! · 1 = Σ_{k=0}^{n} (−1)^k/k!.

Multiplying through by n! recovers D_n = n! · Σ_{k=0}^{n} (−1)^k/k! — the alternating formula of §1.1 falls out of the algebra *by itself*, without our having to track a single overlap by hand. (Analytically, because 0 ≤ D_n ≤ n! for every integer n ≥ 0, the power series D(x) = Σ_{n=0}^{∞} D_n/n! · x^n and 1/(1−x) = Σ_{m=0}^{∞} x^m both converge absolutely for all x ∈ (−1, 1) while e^{±x} = Σ_{k=0}^{∞} (±x)^k/k! converges absolutely for all x ∈ ℝ, so the Cauchy product holds both as an identity of formal power series in ℚ[[x]] and as an equality of analytic functions on (−1, 1); for n = 2, pairing (k, 2−k) for k = 0, 1, 2 gives D₂/2! = 1/0!·1 + (−1)/1!·1 + 1/2!·1 = 1 − 1 + ½ = ½, so D₂ = 2!·½ = 1 ✓.) When a bookkeeping machine reproduces an answer without being told the zigzag, that is a sign you have found the true structure. (Pattern **P5**: generating functions — a whole sequence treated as a single object.)

### 1.4 The punchline: nature leaves a fingerprint

**✎ Checkpoint.** Predict before the reveal: D₇/7! = 1854/5040 and D₈/8! = 14833/40320. Compute both as decimals, commit in ink to a guess about where the fractions are heading, and only then read on. Carrying out the division gives D₇/7! = 1854/5040 = 103/280 ≈ 0.367857 and D₈/8! = 14833/40320 ≈ 0.367882, bracketing the limit 1/e ≈ 0.367879 within 1/8! = 1/40320 ≈ 0.000025.

Divide by n!: D_n/n! = Σ_{k=0}^{n} (−1)^k/k! → **1/e ≈ 0.3679** as n grows (since the Taylor series e^x = Σ_{k=0}^{∞} x^k/k! converges for all x ∈ ℝ and evaluating at x = −1 gives Σ_{k=0}^{∞} (−1)^k/k! = e^{−1} = 1/e, with alternating truncation error |D_n/n! − 1/e| < 1/(n+1)!). A random arrangement of a million letters has about a 36.8% chance of getting *every single one wrong* — essentially the same chance as for six letters (265/720 ≈ 36.8%, where 265/720 ≈ 0.368056 differs from 1/e ≈ 0.367879 by less than 1/7! = 1/5040 ≈ 0.000198). The number e, which you met in calculus as a limit of (1+1/n)ⁿ, shows up here as a *probability about universal mess-making*. Nature is economical with her ideas; she reuses them without telling you.

**What you now own:** count-the-complement with honest overlaps (P3); recurrence-as-explanation (P4); generating-function bookkeeping (P5); and the reflex — *when everything must avoid everything, count the complement, but respect the overlap.*

---

## Lecture 2 · The Mirror World: the Catalan Numbers

Now a problem that looks like a children's game and hides one of the deepest numbers in mathematics. A walker starts at the corner of a square city grid, at (0,0), and wants to reach the opposite corner (n,n), taking only steps East and North. Nothing special so far: C(2n,n) paths. But this walker is superstitious — she refuses ever to be *above* the diagonal line y = x. At every moment, "north so far" must not exceed "east so far." How many paths?

For n = 3: of the 20 total paths, exactly **5** survive — namely EEENNN, EENENN, EENNEN, ENEENN, and ENENEN. Five — the Catalan number **C₃**. (Mind your fingers: our sequence counts from C₀ = 1, so C₃ is the fourth *term*; "the fifth Catalan number" is exactly the off-by-one this course is training out of you. Compute n = 2 yourself; you should find 2. Do it — with a pencil — before reading on. This is not optional; the pencil is where the understanding happens. Explicitly, for n = 2 there are C(4,2) = 6 paths of two E's and two N's from (0,0) to (2,2): the two paths EENN and ENEN stay weakly below y = x throughout, whereas ENNE, NENE, NNEE, NEEN all rise above the diagonal, giving C₂ = 2.)

### 2.1 The mirror trick

Count the good paths directly? Hard. Count the **bad** paths — and this is the move to learn (pattern **P6**) — by finding a mirror image of them in a world we can count.

A bad path touches the line y = x + 1 at some first moment. Take the path up to that moment and reflect it across the line y = x + 1 — every East step becomes a North step and vice versa, and the path is reborn in the mirror world. Let me show you one, n = 2: the bad path **E, N, N, E** first touches the forbidden line at its third step. Reflect those three steps: E,N,N → N,E,E. The mirror path is N,E,E,E — a path that now ends at (3,1) instead of (2,2).

(What, geometrically, is this swap? Reflection across **any** line of slope +1 exchanges East and North steps; what the line's position decides is only *where the picture must be translated afterwards*. Two honest descriptions of one map. **Mirror in the boundary:** reflect the head across the forbidden line y = x + 1 — the touch point (t, t+1) stays where it is and the tail stays where it was, but the head now begins at (−1, 1), so the whole path is lifted by (1, −1) to start at the origin again. **Mirror in the main diagonal:** reflect the head across y = x — the origin stays fixed, but the touch point slides to (t+1, t), and now it is the *tail* that must shift by (1, −1) to rejoin it. Either way the very same path comes out, ending at (n+1, n−1): in coordinates, if a bad path has vertices (x_j, y_j)_{j=0}^{2n} with first touch (x_m, y_m) = (t, t+1) at step m = 2t+1, reflecting the prefix 0 ≤ j ≤ m across y = x + 1 sends (x_j, y_j) ↦ (y_j − 1, x_j + 1) and translating the entire path by (+1, −1) yields (y_j, x_j) for 0 ≤ j ≤ m and (x_j + 1, y_j − 1) for m ≤ j ≤ 2n, which is identical to reflecting the prefix across y = x via (x_j, y_j) ↦ (y_j, x_j) and shifting the tail by (+1, −1) — for ENNE at n = 2, m = 3, both produce (0,0) → (0,1) → (1,1) → (2,1) → (3,1), the path NEEE. The step-swap is the primitive; the two mirrors are costumes for it — and when this chapter says "reflect across y = x + 1," it means the first description, translation included.)

Drawn, the pair looks like this (x runs right, y runs up; **⊗** marks the relevant first touch, ╱ the relevant line):

```
   The bad path  E N N E  (ends at (2,2)):

     y=2  ·    ⊗————●
             ╱ │          ╱ = the forbidden line y = x + 1
     y=1  ·    ●    ·     │ = the walker's steps
        ╱      │
     y=0  ●————●    ·
          0    1    2   (x)

   Its mirror  N E E E  (ends at (3,1)):

     y=2  ·    ·    ·    ·
                       ╱       ╱ = the line x = y + 1
     y=1  ●————●————⊗————●
          │       ╱
     y=0  ●    ·    ·    ·
          0    1    2    3   (x)
```

Read the left panel: East along the ground, North twice at x = 1, then East into (2,2) — the walker first sets foot on the line y = x+1 at ⊗. Swap the head up to ⊗ (E,N,N → N,E,E) and the path is reborn as the right panel, ending at (3,1) instead. To *return*, swap the right panel's head up to its own ⊗ — a first touch of **x = y + 1** — and E,N,N,E comes back. **The two ⊗'s lie on different lines.** That is the whole trap: hunt the wrong line and some partners (like E,E,E,N) offer no touch to find — the lab below rings exactly that alarm.

The same pair, drawn as **Figure 1** — labelled axes, the swapped head in amber and the kept tail in blue, both mirror lines dashed, and the two ⊗'s visibly on their different lines:

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 880 530" font-family="system-ui, -apple-system, 'Segoe UI', sans-serif">
  <rect x="0" y="0" width="880" height="530" fill="#ffffff"/>
  <!-- ================= FIGURE 1 · The reflection pair ================= -->
  <text x="40" y="34" font-size="17" font-weight="700" fill="#193e5c">Figure 1 &#183; The reflection pair &#8212; a bad path and its mirror</text>

  <!-- Panel A : bad path E N N E -->
  <text x="110" y="62" font-size="13" fill="#172333" font-weight="600">the bad path E N N E (ends at (2,2))</text>
  <g fill="#cbd5e1">
    <circle cx="110" cy="380" r="2.5"/><circle cx="160" cy="380" r="2.5"/><circle cx="210" cy="380" r="2.5"/><circle cx="260" cy="380" r="2.5"/>
    <circle cx="110" cy="330" r="2.5"/><circle cx="160" cy="330" r="2.5"/><circle cx="210" cy="330" r="2.5"/><circle cx="260" cy="330" r="2.5"/>
    <circle cx="110" cy="280" r="2.5"/><circle cx="160" cy="280" r="2.5"/><circle cx="210" cy="280" r="2.5"/><circle cx="260" cy="280" r="2.5"/>
    <circle cx="110" cy="230" r="2.5"/><circle cx="160" cy="230" r="2.5"/><circle cx="210" cy="230" r="2.5"/><circle cx="260" cy="230" r="2.5"/>
  </g>
  <line x1="110" y1="230" x2="110" y2="385" stroke="#94a3b8" stroke-width="1.2"/>
  <line x1="105" y1="380" x2="265" y2="380" stroke="#94a3b8" stroke-width="1.2"/>
  <g font-size="11" fill="#64748b" text-anchor="middle">
    <text x="110" y="398">0</text><text x="160" y="398">1</text><text x="210" y="398">2</text><text x="260" y="398">3</text>
    <text x="98" y="384">0</text><text x="98" y="334">1</text><text x="98" y="284">2</text><text x="98" y="234">3</text>
  </g>
  <!-- the forbidden line y = x + 1 (passes through (0,1)=(110,330), (1,2)=(160,280), (2,3)=(210,230)) -->
  <line x1="104" y1="336" x2="235" y2="205" stroke="#dc2626" stroke-width="2" stroke-dasharray="6,4"/>
  <text x="239" y="207" font-size="11.5" fill="#dc2626" font-style="italic">y = x + 1</text>
  <!-- path: head (amber) = steps 1-3, tail (blue) = step 4 -->
  <polyline points="110,380 160,380 160,330 160,280" fill="none" stroke="#d97706" stroke-width="4" stroke-linecap="round" stroke-linejoin="round"/>
  <polyline points="160,280 210,280" fill="none" stroke="#2563eb" stroke-width="4" stroke-linecap="round"/>
  <circle cx="210" cy="280" r="4" fill="#2563eb"/>
  <text x="220" y="272" font-size="11.5" fill="#2563eb">(2,2)</text>
  <!-- step labels -->
  <g font-size="11" font-weight="600">
    <text x="135" y="372" fill="#d97706" text-anchor="middle">1 E</text>
    <text x="168" y="358" fill="#d97706">2 N</text>
    <text x="168" y="316" fill="#d97706">3 N</text>
    <text x="195" y="294" fill="#2563eb" text-anchor="middle">4 E</text>
  </g>
  <!-- first-touch mark -->
  <circle cx="160" cy="280" r="8" fill="#ffffff" stroke="#dc2626" stroke-width="2.5"/>
  <line x1="154.5" y1="274.5" x2="165.5" y2="285.5" stroke="#dc2626" stroke-width="2"/>
  <line x1="165.5" y1="274.5" x2="154.5" y2="285.5" stroke="#dc2626" stroke-width="2"/>
  <g font-size="12" fill="#172333">
    <text x="110" y="428">swap the head up to &#8855;: E,N,N &#8594; N,E,E</text>
    <text x="110" y="448" font-size="11.5" fill="#64748b">the path is reborn in the mirror world</text>
  </g>

  <!-- Panel B : the mirror N E E E -->
  <text x="500" y="62" font-size="13" fill="#172333" font-weight="600">its mirror N E E E (ends at (3,1))</text>
  <g fill="#cbd5e1">
    <circle cx="500" cy="380" r="2.5"/><circle cx="550" cy="380" r="2.5"/><circle cx="600" cy="380" r="2.5"/><circle cx="650" cy="380" r="2.5"/>
    <circle cx="500" cy="330" r="2.5"/><circle cx="550" cy="330" r="2.5"/><circle cx="600" cy="330" r="2.5"/><circle cx="650" cy="330" r="2.5"/>
    <circle cx="500" cy="280" r="2.5"/><circle cx="550" cy="280" r="2.5"/><circle cx="600" cy="280" r="2.5"/><circle cx="650" cy="280" r="2.5"/>
    <circle cx="500" cy="230" r="2.5"/><circle cx="550" cy="230" r="2.5"/><circle cx="600" cy="230" r="2.5"/><circle cx="650" cy="230" r="2.5"/>
  </g>
  <line x1="500" y1="230" x2="500" y2="385" stroke="#94a3b8" stroke-width="1.2"/>
  <line x1="495" y1="380" x2="655" y2="380" stroke="#94a3b8" stroke-width="1.2"/>
  <g font-size="11" fill="#64748b" text-anchor="middle">
    <text x="500" y="398">0</text><text x="550" y="398">1</text><text x="600" y="398">2</text><text x="650" y="398">3</text>
    <text x="488" y="384">0</text><text x="488" y="334">1</text><text x="488" y="284">2</text><text x="488" y="234">3</text>
  </g>
  <!-- the line x = y + 1 (passes through (1,0)=(550,380), (2,1)=(600,330), (3,2)=(650,280)) -->
  <line x1="544" y1="386" x2="675" y2="255" stroke="#16a34a" stroke-width="2" stroke-dasharray="6,4"/>
  <text x="679" y="257" font-size="11.5" fill="#16a34a" font-style="italic">x = y + 1</text>
  <!-- path: head (amber) = steps 1-3, tail (blue) = step 4 -->
  <polyline points="500,380 500,330 550,330 600,330" fill="none" stroke="#d97706" stroke-width="4" stroke-linecap="round" stroke-linejoin="round"/>
  <polyline points="600,330 650,330" fill="none" stroke="#2563eb" stroke-width="4" stroke-linecap="round"/>
  <circle cx="650" cy="330" r="4" fill="#2563eb"/>
  <text x="660" y="322" font-size="11.5" fill="#2563eb">(3,1)</text>
  <!-- step labels -->
  <g font-size="11" font-weight="600">
    <text x="492" y="358" fill="#d97706" text-anchor="end">1 N</text>
    <text x="525" y="318" fill="#d97706" text-anchor="middle">2 E</text>
    <text x="575" y="318" fill="#d97706" text-anchor="middle">3 E</text>
    <text x="628" y="346" fill="#2563eb" text-anchor="middle">4 E</text>
  </g>
  <!-- first-touch mark -->
  <circle cx="600" cy="330" r="8" fill="#ffffff" stroke="#16a34a" stroke-width="2.5"/>
  <line x1="594.5" y1="324.5" x2="605.5" y2="335.5" stroke="#16a34a" stroke-width="2"/>
  <line x1="605.5" y1="324.5" x2="594.5" y2="335.5" stroke="#16a34a" stroke-width="2"/>
  <g font-size="12" fill="#172333">
    <text x="500" y="428">swap back up to &#8855;: N,E,E &#8594; E,N,N</text>
    <text x="500" y="448" font-size="11.5" fill="#64748b">the bad path returns &#8212; the bijection is two-way</text>
  </g>

  <!-- legend + note -->
  <g font-size="11.5">
    <line x1="40" y1="472" x2="70" y2="472" stroke="#d97706" stroke-width="4"/>
    <text x="78" y="476" fill="#172333">the head (what gets swapped)</text>
    <line x1="270" y1="472" x2="300" y2="472" stroke="#2563eb" stroke-width="4"/>
    <text x="308" y="476" fill="#172333">the tail (kept as it is)</text>
  </g>
  <text x="40" y="498" font-size="12" fill="#172333">The two &#8855; marks lie on different lines &#8212; y = x + 1 (left, red) and x = y + 1 (right, green).</text>
  <text x="40" y="516" font-size="12" fill="#64748b">Hunt the wrong line and some partners (like E, E, E, N) offer no touch to find.</text>
</svg>

```

The miracle: this map is a **bijection** for every n ≥ 1 — and the way to *know* that is to verify both the endpoint step counts and the preservation of the first-touch index. Along any lattice path starting at (x₀, y₀) = (0,0), the quantity y_j − x_j starts at 0 and changes by ±1 at each step j. A path P from (0,0) to (n,n) is bad if and only if y_j − x_j ≥ 1 for some j, so by unit-step continuity there is a unique earliest step m = 2t + 1 at which y_m − x_m = 1 — namely, the first vertex (x_m, y_m) = (t, t+1) on the forbidden line y = x + 1, while y_j − x_j ≤ 0 for all 0 ≤ j < m. The prefix of P of length m has t East steps and t + 1 North steps, and the remaining suffix has n − t East steps and n − (t + 1) North steps. Define Φ(P) by swapping East and North in the prefix of length m. The reflected path Φ(P) has

(t + 1) + (n − t) = n + 1 East steps and t + (n − t − 1) = n − 1 North steps,

so it is an unrestricted lattice path from (0,0) to (n+1, n−1). Crucially, at every vertex (x′_j, y′_j) = (y_j, x_j) of the swapped prefix (0 ≤ j ≤ m), we have x′_j − y′_j = y_j − x_j. Therefore x′_j − y′_j ≤ 0 for all 0 ≤ j < m and x′_m − y′_m = 1, which means (x′_m, y′_m) = (t+1, t) is the **unique first vertex** of Φ(P) on the line x = y + 1.

Conversely, along any unrestricted path Q from (0,0) to (n+1, n−1), the difference x_j − y_j starts at 0, ends at (n+1) − (n−1) = 2 ≥ 1, and changes by ±1 per step, so Q has a unique first vertex (t+1, t) at step m = 2t + 1 where x_m − y_m = 1 (with x_j − y_j ≤ 0 for all 0 ≤ j < m). Defining Ψ(Q) by swapping East and North in the prefix up to step m produces a path to (n,n) whose vertices satisfy y″_j − x″_j = x_j − y_j ≤ 0 for 0 ≤ j < m and y″_m − x″_m = 1, so (t, t+1) at step m is its first touch of y = x + 1. Because Φ and Ψ reflect at the exact same first-touch index m in both directions and swapping East and North twice is the identity, Ψ(Φ(P)) = P and Φ(Ψ(Q)) = Q. (Careful: the inverse looks for the first touch of x = y + 1, *not* y = x + 1 — the path E, E, E, N to (3,1) never touches y = x + 1 at all. The lab below machine-tests this inverse in both directions.) Two worlds, perfectly translated, with the translation specified both ways.

Unrestricted paths of length 2n to (n+1, n−1) are easy to count for n ≥ 1: choose which n − 1 of the 2n steps are North, in C(2n, n−1) ways. Subtracting the bad paths from all C(2n,n) paths to (n,n) and simplifying the factorials for every integer n ≥ 1 gives:

**C_n = C(2n,n) − C(2n,n−1) = (2n)!/(n!·n!) − (2n)!/((n−1)!·(n+1)!) = (2n)!/(n!·n!) · (1 − n/(n+1)) = (1/(n+1)) · C(2n,n)**.

(At n = 0, the single empty path from (0,0) to (0,0) never touches y = x + 1, so C₀ = 1, which also matches (1/(0+1))·C(0,0) = 1.) The ugly answer "5 out of 20" is now *explained*: for n = 3, 1/(3+1) = 1/4, so exactly 1 in every 4 paths behaves. When a strange fraction becomes obvious, you have found the right idea.

### 2.2 The equation the paths obey

Look at any nonempty good path. It starts with an **East** step (a North step would put her above the diagonal immediately) and, at some point, first returns to the diagonal — closing the first "excursion." A good path is:

> **empty**, or **E** [a good path] **N** [a good path]

Read that aloud: a path is nothing, or a matched pair wrapping a smaller path and followed by another. That is *self-similarity* — the object is made of copies of itself. Here is a good path of size 3 cut at its first return (⊗ marks the first return to the diagonal):

```
   The path  E E N N E N:

     y=3  ·    ·    ·    ●
                         │
     y=2  ·    ·    ⊗————●
                    │
     y=1  ·    ·    ●    ·
                    │
     y=0  ●————●————●    ·
          0    1    2    3   (x)
```

Read the shape: the opening E starts the first excursion; the closing N of that excursion lands on ⊗. Inside the pair sat **A = E N** (a good path of size 1, translated); after it marches **B = E N** (another). The path is E [A] N [B] with |A| = 1, |B| = 1 — and summing over the splits 0+2, 1+1, 2+0 gives C₃ = 1·2 + 1·1 + 2·1 = 5 ✓.

The same cut, drawn as **Figure 2** — the wrapping pair E…N in purple, A in amber, B in blue, all six steps labelled and the split arithmetic at the foot:

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 548 880 350" font-family="system-ui, -apple-system, 'Segoe UI', sans-serif">
  <rect x="0" y="548" width="880" height="350" fill="#ffffff"/>
  <!-- ================= FIGURE 2 · The first-return cut ================= -->
  <text x="40" y="568" font-size="17" font-weight="700" fill="#193e5c">Figure 2 &#183; The first-return cut &#8212; E [A] N [B]</text>
  <text x="40" y="590" font-size="12.5" fill="#64748b">the good path E E N N E N of size 3, cut at its first return to the diagonal</text>

  <g fill="#cbd5e1">
    <circle cx="120" cy="780" r="2.5"/><circle cx="172" cy="780" r="2.5"/><circle cx="224" cy="780" r="2.5"/><circle cx="276" cy="780" r="2.5"/>
    <circle cx="120" cy="728" r="2.5"/><circle cx="172" cy="728" r="2.5"/><circle cx="224" cy="728" r="2.5"/><circle cx="276" cy="728" r="2.5"/>
    <circle cx="120" cy="676" r="2.5"/><circle cx="172" cy="676" r="2.5"/><circle cx="224" cy="676" r="2.5"/><circle cx="276" cy="676" r="2.5"/>
    <circle cx="120" cy="624" r="2.5"/><circle cx="172" cy="624" r="2.5"/><circle cx="224" cy="624" r="2.5"/><circle cx="276" cy="624" r="2.5"/>
  </g>
  <line x1="120" y1="624" x2="120" y2="785" stroke="#94a3b8" stroke-width="1.2"/>
  <line x1="115" y1="780" x2="281" y2="780" stroke="#94a3b8" stroke-width="1.2"/>
  <g font-size="11" fill="#64748b" text-anchor="middle">
    <text x="120" y="812">0</text><text x="172" y="812">1</text><text x="224" y="812">2</text><text x="276" y="812">3</text>
    <text x="108" y="784">0</text><text x="108" y="732">1</text><text x="108" y="680">2</text><text x="108" y="628">3</text>
  </g>
  <!-- the diagonal y = x -->
  <line x1="120" y1="780" x2="276" y2="624" stroke="#94a3b8" stroke-width="1.5" stroke-dasharray="4,4"/>
  <text x="262" y="612" font-size="11.5" fill="#64748b" font-style="italic">y = x</text>
  <!-- path segments -->
  <polyline points="120,780 172,780" fill="none" stroke="#7c3aed" stroke-width="4" stroke-linecap="round"/>
  <polyline points="172,780 224,780 224,728" fill="none" stroke="#d97706" stroke-width="4" stroke-linecap="round" stroke-linejoin="round"/>
  <polyline points="224,728 224,676" fill="none" stroke="#7c3aed" stroke-width="4" stroke-linecap="round"/>
  <polyline points="224,676 276,676 276,624" fill="none" stroke="#2563eb" stroke-width="4" stroke-linecap="round" stroke-linejoin="round"/>
  <circle cx="276" cy="624" r="4" fill="#2563eb"/>
  <text x="286" y="628" font-size="11.5" fill="#172333">(3,3)</text>
  <!-- step labels -->
  <g font-size="11" font-weight="600">
    <text x="146" y="795" fill="#7c3aed" text-anchor="middle">1 E</text>
    <text x="198" y="795" fill="#d97706" text-anchor="middle">2 E</text>
    <text x="232" y="758" fill="#d97706">3 N</text>
    <text x="232" y="714" fill="#7c3aed">4 N</text>
    <text x="256" y="691" fill="#2563eb" text-anchor="middle">5 E</text>
    <text x="286" y="654" fill="#2563eb">6 N</text>
  </g>
  <!-- first-return mark -->
  <circle cx="224" cy="676" r="8" fill="#ffffff" stroke="#dc2626" stroke-width="2.5"/>
  <line x1="218.5" y1="670.5" x2="229.5" y2="681.5" stroke="#dc2626" stroke-width="2"/>
  <line x1="229.5" y1="670.5" x2="218.5" y2="681.5" stroke="#dc2626" stroke-width="2"/>
  <!-- bracket reading -->
  <text x="40" y="838" font-size="15" font-weight="600"><tspan fill="#7c3aed">E</tspan><tspan fill="#172333"> [ </tspan><tspan fill="#d97706">A = E N</tspan><tspan fill="#172333"> ] </tspan><tspan fill="#7c3aed">N</tspan><tspan fill="#172333"> [ </tspan><tspan fill="#2563eb">B = E N</tspan><tspan fill="#172333"> ]</tspan></text>
  <text x="40" y="862" font-size="12.5" fill="#172333">|A| = 1, |B| = 1 &#8212; over the splits 0+2, 1+1, 2+0:  C&#8323; = 1&#183;2 + 1&#183;1 + 2&#183;1 = 5 &#10003;</text>
  <text x="40" y="886" font-size="11.5" fill="#64748b">&#8855; = first return to diagonal &#183; purple = wrapping pair E &#8230; N &#183; amber = A (inside) &#183; blue = B (the rest)</text>
</svg>

```

**✎ Checkpoint.** Now try the translation yourself before seeing it done. If C(x) is the bookkeeping machine for good paths, what should the sentence "a path is *empty*, or **E** [path] **N** [path]" say about C(x)? (Decide first what one wrapped pair E…N should *cost* — there is exactly one natural choice: the empty path has size 0 and contributes x⁰ = 1, while a nonempty path E[A]N[B] has size |A| + |B| + 1, so the wrapping pair E…N contributes x¹ = x and the independent choices of A and B contribute C(x)·C(x) = C(x)², giving C(x) = 1 + x·C(x)².)

Now the physicist's move. First, why is the decomposition E[A]N[B] an exact bijection between nonempty good paths of size n ≥ 1 and ordered pairs (A, B) of good paths whose sizes k and n−1−k sum to n−1? Take any good path P from (0,0) to (n,n) with n ≥ 1. Since P stays in the region y ≤ x and ends at (n,n) with n ≥ 1, the set of positive steps j > 0 at which y_j = x_j is nonempty (it contains j = 2n), so there is a unique smallest even step 2k+2 ∈ {2, 4, …, 2n} at which P first returns to the diagonal, landing at (k+1, k+1) for some k ∈ {0, …, n−1}. At every intermediate step 1 ≤ j ≤ 2k+1, the path has not yet returned to y = x, so y_j ≤ x_j − 1. In particular, at j = 1 we have x₁ + y₁ = 1 and y₁ ≤ x₁ − 1, forcing (x₁, y₁) = (1,0) (an opening E step); and at j = 2k+1 we have x_{2k+1} + y_{2k+1} = 2k+1, y_{2k+1} ≤ x_{2k+1} − 1, and x_{2k+1} ≤ x_{2k+2} = k+1, which together give k+1 = (2k+1) − k ≤ (x_{2k+1} + y_{2k+1}) − y_{2k+1} = x_{2k+1} ≤ k+1, forcing (x_{2k+1}, y_{2k+1}) = (k+1, k) and thus a closing N step into (k+1, k+1). Shifting the intermediate segment from (1,0) to (k+1, k) by (−1,0) gives a path A from (0,0) to (k,k) whose vertices (x′_r, y′_r) = (x_{r+1} − 1, y_{r+1}) satisfy y′_r − x′_r = y_{r+1} − (x_{r+1} − 1) ≤ 0 for all 0 ≤ r ≤ 2k, so A is a good path of size k. Shifting the remaining suffix from (k+1, k+1) to (n,n) by (−k−1, −k−1) gives a good path B of size n−1−k. Conversely, for any k ∈ {0, …, n−1}, any good path A of size k, and any good path B of size n−1−k, concatenating E[A]N[B] produces a good path of size n whose first return to y = x occurs at step 2k+2. Define the bookkeeping machine **C(x) = Σ_{n≥0} C_n xⁿ** — the *ordinary* generating function: a path of size n contributes one unit of xⁿ. Notice what is *absent* here compared with Lecture 1.3, where D(x) = Σ D_n xⁿ/n! carried a factorial in every term. That factorial was load-bearing: derangements live on *labeled* letters, and gluing two labeled structures forces a choose-which-labels binomial — the 1/n! factors are exactly what tames it. A path carries no labels: its decomposition splits it by *position* — first excursion, then the rest — and the sizes of the pieces are read off the path itself, with nothing to choose. No binomial appears, so no factorial is needed. **Exponential bookkeeping for labeled worlds; ordinary bookkeeping for unlabeled ones** — a distinction that will earn its own lecture the next time it matters. The sentence above, translated into bookkeeping (one wrapped pair costs a factor x), is an *equation*:

**C(x) = 1 + x·C(x)²**.

That equation **is** the Catalan structure: x·C(x)² − C(x) + 1 = 0. Comparing coefficients of xⁿ directly in C(x) = 1 + x·C(x)² gives the convolution recurrence C_n = Σ_{k=0}^{n−1} C_k·C_{n−1−k} for n ≥ 1 with C₀ = 1 (check C_3 = 1·2 + 1·1 + 2·1 = 5 ✓). Better still, we can solve the quadratic for C(x) and extract the closed form without touching a mirror. For x ≠ 0, the quadratic formula gives

C(x) = (1 ± √(1−4x))/(2x).

Which sign does nature choose? Because every good path of size n ≥ 0 is a word of length 2n over {E, N}, we have the crude a priori bound 0 ≤ C_n ≤ C(2n,n) ≤ 2^{2n} = 4ⁿ for all n ≥ 0 (for n = 2, C₂ = 2 ≤ C(4,2) = 6 ≤ 4² = 16), so by comparison with the geometric series Σ_{n=0}^{∞} (4|x|)ⁿ the power series C(x) = Σ_{n=0}^{∞} C_n xⁿ converges absolutely and defines a continuous function on (−1/4, 1/4). Since C(x) = Σ C_n·xⁿ is continuous near x = 0 with C(0) = C₀ = 1, we must have lim_{x→0} C(x) = 1. Because √(1−4x) = 1 − 2x + O(x²) as x → 0, the plus branch diverges like 1/x, whereas the minus branch satisfies lim_{x→0} (1 − (1 − 2x + O(x²)))/(2x) = 1. Thus C(x) = (1 − (1−4x)^{1/2})/(2x) for |x| < 1/4. Now expand (1−4x)^{1/2} by Newton's generalized binomial theorem:

(1−4x)^{1/2} = 1 + Σ_{m=1}^{∞} C(1/2, m)·(−4)^m·x^m.

For m = 1, the term is C(1/2, 1)·(−4)·x = −2x = −(2/1)·C(0,0)·x. For every integer m ≥ 2, the numerator of C(1/2, m) has m factors — namely 1/2 followed by the m − 1 negative half-integers −1/2, −3/2, …, −(2m−3)/2:

C(1/2, m) = (1/2)(−1/2)(−3/2)···(−(2m−3)/2) / m! = ((−1)^{m−1})/(2^m·m!) · ∏_{j=1}^{m−1} (2j − 1).

Multiply numerator and denominator of this (m−1)-factor odd product by the (m−1)-factor even product ∏_{j=1}^{m−1} (2j) = 2^{m−1}·(m−1)! to complete the factorial (2m−2)!:

C(1/2, m)·(−4)^m = ((−1)^{m−1})/(2^m·m!) · (2m−2)!/(2^{m−1}·(m−1)!) · (−1)^m·2^{2m} = −(2/m)·(2m−2)!/((m−1)!·(m−1)!) = −(2/m)·C(2m−2, m−1).

Since −(2/m)·C(2m−2, m−1) also equals −2 at m = 1, the formula holds for all m ≥ 1. Substituting it into C(x) = (1 − (1−4x)^{1/2})/(2x) and shifting the summation index via n = m − 1 (so m = n + 1) yields

C(x) = (1/(2x)) · Σ_{m=1}^{∞} (2/m)·C(2m−2, m−1)·x^m = Σ_{n=0}^{∞} (1/(n+1))·C(2n,n)·xⁿ.

The coefficient of xⁿ on the right is C_n = (1/(n+1))·C(2n,n) for all n ≥ 0 — streaming out of pure algebra, and matching the mirror world of §2.1. Pattern **P4/P5** again: *decompose at the first return; write the self-similarity as an equation.*

### 2.3 One number, many costumes

**✎ Checkpoint.** Pause the book. You now own the sequence 1, 2, 5, 14, 42, 132. Write down every mathematical object you have *ever* seen counted by these numbers — guess boldly, in ink — then compare with the list below. Every hit you score is a costume you can hunt a bijection for.

Here is the part that would make you suspicious if you met it in fiction: the numbers 1, 2, 5, 14, 42… count *all* of these — good lattice paths to (n,n); balanced parenthesis strings with n pairs; triangulations of an (n+2)-gon; full binary trees with n+1 leaves; permutations of n things sortable by one stack. Five costumes, one number. Each pair of costumes is connected by an explicit **bijection** (pattern **P1**), and finding those translations is the best training I know: when the same numbers appear twice, do not shrug — *hunt the map between the two worlds.* The decomposition "E [path] N [path]" is the true content; every costume is the same creature wearing different clothes. Exercises 4 and 18 work out the explicit bijections for balanced parenthesis strings (worked in A4) and polygon triangulations (worked in A18); let us verify the remaining two costumes right here against the same E[A]N[B] structure for every integer n ≥ 0:
- **Full plane binary trees with n+1 leaves (equivalently, n internal nodes):** For n = 0, a tree with 1 leaf has no internal nodes, matching the single empty path (C₀ = 1). For n ≥ 1, every full binary tree T with n+1 leaves has a root internal node whose left child roots a full binary subtree T_L with k+1 leaves (k internal nodes, for a unique k ∈ {0, …, n−1}) and whose right child roots a full binary subtree T_R with (n−1−k)+1 leaves (n−1−k internal nodes), since the total number of leaves is (k+1) + (n−k) = n+1. Define Φ(T) recursively by mapping the single-leaf tree to the empty path and setting Φ(T) = E[Φ(T_L)]N[Φ(T_R)]. Because the first-return decomposition of §2.2 uniquely recovers Φ(T_L) and Φ(T_R) from Φ(T), induction on n shows Φ is a bijection onto good paths of size n (for n = 3, the leaf-splits (k+1, 3−k) ∈ {(1,3), (2,2), (3,1)} yield C₀C₂ + C₁C₁ + C₂C₀ = 1·2 + 1·1 + 2·1 = 5 = C₃ trees ✓).

- **Permutations of {1, …, n} sortable by one stack (producing 1, 2, …, n):** A stack processes an input permutation π of {1, …, n} by a sequence of n pushes (E) from the input onto the stack and n pops (N) from the top of the stack to the output; because one cannot pop from an empty stack, a sequence of n pushes and n pops is legal if and only if in every prefix the number of pops (y_j) is at most the number of pushes (x_j), with the stack empty precisely at the diagonal returns x_j = y_j. Moreover, any two elements x < y on the stack at the same time must have x above y (otherwise y would be popped before x), so a stack-sortable permutation π admits a *unique* sorting push-pop sequence Ψ_stack(π) (namely: pop the top of the stack whenever it equals the next required output integer, and push the next input element otherwise). Thus legal push-pop sequences of length 2n are in bijection with good lattice paths from (0,0) to (n,n), and each good path P produces a unique output permutation when applied to the identity input — or equivalently, sorts a unique input permutation π_P into the increasing output 1, 2, …, n. Under the first-return decomposition P = E[A]N[B] of §2.2 (where |A| = k ∈ {0, …, n−1} and |B| = n−1−k), the opening step E pushes the first input element π(1) onto the empty stack, and the matching first-return step N (at step 2k+2) is the exact moment π(1) is finally popped to the output; during the intermediate sub-path A, the next k input elements L′ are pushed and completely popped above π(1) before π(1) leaves the stack, and during B the final n−1−k input elements R′ are pushed and popped after π(1) is output. For the total output to be 1, 2, …, n in increasing order, L′ must be a stack-sortable permutation of {1, …, k} sorted by A, the first element must be π(1) = k+1, and R′ must be a stack-sortable permutation of {k+2, …, n} sorted by B; thus π = (k+1) L′ R′ ↦ E[A]N[B] is a bijection between stack-sortable permutations of {1, …, n} and good lattice paths of size n (check n = 2: π = 12 = 1 ∅ 2 has k = 0 and is sorted by E[ε]N[EN] = ENEN, while π = 21 = 2 1 ∅ has k = 1 and is sorted by E[EN]N[ε] = EENN ✓). Equivalently, decomposing π = L n R at the maximum element n (with |L| = k and |R| = n−1−k, and Ψ_stack(∅) = ε), because n must be output last of all, every element of L must be pushed and completely popped before n is pushed (otherwise an element of L would be trapped beneath n on the stack and forced out after n), and every element of L is output before every element of R, so π is stack-sortable if and only if L is a stack-sortable permutation of {1, …, k} and R is a stack-sortable permutation of {k+1, …, n−1} — which by induction holds if and only if π avoids the pattern 231 (no i₁ < i₂ < i₃ have π(i₃) < π(i₁) < π(i₂), since any 231 triple not lying entirely inside L or R cannot have π(i₁) = n or π(i₃) = n and thus forces π(i₁) ∈ L and π(i₃) ∈ R with π(i₃) < π(i₁), and conversely any such pair π(i₁) ∈ L, π(i₃) ∈ R with π(i₃) < π(i₁) yields the 231 triple (π(i₁), n, π(i₃)) with middle element n, occurring if and only if L fails to consist of {1, …, k} and R of {k+1, …, n−1}) — with unique sorting push-pop sequence Ψ_stack(π) = [Ψ_stack(L)] E [Ψ_stack(R)] N (for n = 3, five of the 3! = 6 permutations — 123, 132, 213, 312, 321 — are stack-sortable, and only 231 fails because 2 must be popped before 3 is pushed, putting 2 ahead of 1 ✓).

**What you now own:** count-the-bad by reflection (P6); decompose-at-first-return and write self-similarity as an equation (P4/P5); bijection-hunting (P1).

---

## Lecture 3 · Count It Twice

The single most productive trick in this entire book fits in one sentence: **count the same set two different ways and set the answers equal.**

### 3.1 The committee

From m women and n men (m, n, r ≥ 0, with C(a,b) = 0 whenever b < 0 or b > a), choose a committee of r. Obvious answer: C(m+n, r) (if W is the set of m women and M is the disjoint set of n men, then |W ⊔ M| = m + n, so the family 𝒞 of all r-person committees from W ⊔ M has size |𝒞| = C(m+n, r)). But classify the same committees by composition — k women (0 ≤ k ≤ r) and r−k men: Σ_{k=0}^{r} C(m,k)·C(n, r−k) (since every committee S ∈ 𝒞 has a unique number of women k = |S ∩ W| ∈ {0, …, r} and therefore |S ∩ M| = r − k men, partitioning 𝒞 = ⨆_{k=0}^{r} 𝒞_k where 𝒞_k = {S ∈ 𝒞 : |S ∩ W| = k}, and the map S ↦ (S ∩ W, S ∩ M) is a bijection from 𝒞_k onto the set of ordered pairs (A, B) with A ⊆ W, |A| = k and B ⊆ M, |B| = r−k, with inverse (A, B) ↦ A ⊔ B, so |𝒞_k| = C(m,k)·C(n, r−k)). The two bookkeepings count one world, so:

**C(m+n, r) = Σ_{k=0}^{r} C(m,k)·C(n, r−k)** — Vandermonde.

Notice what happened: the identity was *not* algebra; it was an **observation about the world dressed in symbols**. Two ways to prove it anyway: (i) multiply (1+x)^m(1+x)^n = (1+x)^{m+n} and compare the coefficient of x^r — the bookkeeping machine again: by the binomial theorem, (1+x)^m = Σ_{k=0}^{m} C(m,k)·x^k and (1+x)^n = Σ_{j=0}^{n} C(n,j)·x^j, so the coefficient of x^r in their product is obtained by summing over all index pairs (k, j) with k + j = r, namely Σ_{k=0}^{r} C(m,k)·C(n, r−k), which must equal the coefficient C(m+n, r) of x^r in (1+x)^{m+n} (with C(a,b) = 0 for b > a); (ii) lattice paths (for 0 ≤ r ≤ m+n): paths from (0,0) to (m+n−r, r) take m+n steps, r of them North, so there are C(m+n, r) such paths in total; classify them by k, the height y = k at which a path crosses the step-m antidiagonal boundary x + y = m after step m, at the unique vertex (m−k, k) — the first m steps form a path from (0,0) to (m−k, k) and place their k Norths in C(m,k) ways, while the last n steps form a translated path from (m−k, k) to (m+n−r, r) and place their r−k Norths in C(n, r−k) ways. Since the crossing height k ∈ {0, …, r} is uniquely determined by the path, the sets of paths for different k partition the full set of paths (check m = 2, n = 2, r = 2: C(2,0)·C(2,2) + C(2,1)·C(2,1) + C(2,2)·C(2,0) = 1 + 4 + 1 = 6 = C(4,2) ✓). Sum over k: same identity, third costume. *Multiple proofs are not decoration; each proof is a different door into the idea.*

### 3.2 The handshake among subsets

Now the deepest two-line argument in elementary combinatorics.

**✎ Checkpoint.** Warm the engine by hand first: list all 8 subsets of {1,2,3} and total their sizes — you should get 12. Now predict, in ink, the average size of a subset of {1,…,100} before reading the two bookkeepings. Explicitly, the 8 subsets of {1,2,3} have sizes |∅| = 0, |{1}| = |{2}| = |{3}| = 1, |{1,2}| = |{1,3}| = |{2,3}| = 2, and |{1,2,3}| = 3, totaling 0 + 3(1) + 3(2) + 1(3) = 12, for an average size of 12/8 = 1.5 = 3/2; for {1, …, 100}, the average subset size is 100/2 = 50.

For n ≥ 1, count pairs (x, S) in the incidence set 𝓘 = {(x, S) : S ⊆ {1,…,n}, x ∈ S} where x is an element of the subset S of {1,…,n}:

- **Choose S first:** grouping the incidence set by the second coordinate — 𝓘 = ⨆_{S ⊆ {1,…,n}} {(x, S) : x ∈ S}, one block per subset S — every k-element set contributes a fiber of size |{(x, S) : x ∈ S}| = |S| = k pairs; total Σ_{k=0}^{n} k·C(n,k).
- **Choose x first:** grouping by the first coordinate — 𝓘 = ⨆_{x=1}^{n} {(x, S) : S ⊆ {1,…,n}, x ∈ S} — each of the n elements sits in exactly half of all subsets — 2^{n−1} of them (since the map S ↦ S ∖ {x} is a bijection between subsets S ⊆ {1, …, n} containing x and all 2^{n−1} subsets of the (n−1)-element set {1, …, n} ∖ {x}, with inverse T ↦ T ∪ {x}); total n·2^{n−1}.

So **Σ_k k·C(n,k) = n·2^{n−1}** for all n ≥ 1 (and trivially at n = 0, where both sides equal 0). And a third costume: differentiate (1+x)^n at x = 1. Differentiating (1+x)^n = Σ_{k=0}^{n} C(n,k)·x^k with respect to x gives n(1+x)^{n−1} = Σ_{k=1}^{n} k·C(n,k)·x^{k−1}, and evaluating at x = 1 yields Σ_{k=0}^{n} k·C(n,k) = n·2^{n−1}. Three engines, one truth.

**The corollary to remember forever:** the *average* subset has n/2 elements. Dividing the total number of elements Σ_{k=0}^{n} k·C(n,k) = n·2^{n−1} across all 2^n subsets gives an average size of (n·2^{n−1})/2^n = n/2. Averaging is the baby form of probability, and probability grows into an entire method — one that will later prove things *exist* without ever constructing them. Plant that seed now; Chapter 4 waters it.

---

## Lecture 4 · The Bit Machine: 2^n

Shortest lecture of the course. A subset of {1,…,n} is a row of n switches, each up or down. Switches: 2 × 2 × … × 2 = **2^n** (explicitly, for every integer n ≥ 0, the indicator map S ↦ (b₁, …, b_n) ∈ {0,1}^n defined by b_i = 1 if i ∈ S and b_i = 0 if i ∉ S, with inverse (b₁, …, b_n) ↦ {i ∈ {1, …, n} : b_i = 1}, is a bijection between the power set 𝒫({1, …, n}) and the 2^n binary strings of length n).

**✎ Checkpoint.** Before classifying: what must Σ_k C(n,k) equal — and *why*, using nothing but the switch picture? Say the reason aloud, then check it against the n = 3 row of Pascal's triangle. Every subset corresponds to one of the 2^n switch settings, and grouping those settings by the number k of "up" switches partitions all 2^n settings into the C(n,k) subsets of size k, so Σ_{k=0}^{n} C(n,k) = 2^n; for n = 3, row 3 of Pascal's triangle sums to 1 + 3 + 3 + 1 = 8 = 2³.

Classify by the number of "up" switches and you get Σ_k C(n,k) = 2^n — the same world counted by type and by total. The binomial theorem at x = 1 says the same thing in formal dress: setting x = 1 in (1+x)^n = Σ_{k=0}^{n} C(n,k)·x^k gives (1+1)^n = 2^n = Σ_{k=0}^{n} C(n,k) — this is the machine from Lecture 3 with both bookkeepings visible at once.

The switch picture is worth keeping for one reason: it converts statements about sets into statements about *strings*, where arithmetic is easy. Half the tricks in coding theory and combinatorics start by putting a string costume on a set.

---

## The Trick Bag (reference card)

| Pattern | Plain language | Where you met it |
|---------|---------------|-----------------|
| **P1 Bijection** | Two worlds, one map: translate the count. Its dynamic face, the **sign-reversing involution**: pair the unwanted objects with a sign-flipping swap and they cancel from an alternating sum (Gessel–Viennot) | Lecture 2.3, A18 |
| **P2 Double counting** | Count one world two ways; setting the answers equal is the theorem | Lecture 3 |
| **P3 Inclusion–exclusion** | Complement of overlapping events = zigzag add/subtract | Lecture 1.1 |
| **P4 Recurrence** | Follow a forced case; explain n by smaller n. Its termination face, the **monovariant**: a quantity that strictly improves at each step certifies the process bottoms out | Lecture 1.2, 2.2 |
| **P5 Generating function** | A whole sequence packaged as one object; algebra works for you | Lectures 1.3, 2.2 |
| **P6 Complement / reflection** | Can't count the good? Count the bad — maybe in a mirror world. Usage-evidence note: zero genuine firings in the survey's census of 133 papers across 14 batches — the only textbook-canon pattern with none; this card is textbook canon (a proof-shape every counter should own — Exercise 11 runs it), not field-visible practice | Lecture 2.1, A11 |

**Formula box:** For integers n, m, r ≥ 0 (with the convention C(a,b) = 0 whenever b < 0 or b > a): D_n = n!·Σ_{k=0}^{n}(−1)^k/k! (n ≥ 0); D_n = (n−1)(D_{n−1}+D_{n−2}) (n ≥ 2, with D₀ = 1, D₁ = 0); D(x) = e^{−x}/(1−x); D_n/n! → 1/e. C_n = (1/(n+1))·C(2n,n) (n ≥ 0); C(x) = 1 + xC(x)². Vandermonde: C(m+n,r) = Σ_{k=0}^{r} C(m,k)·C(n,r−k). Σ_{k=0}^{n} C(n,k) = 2^n; Σ_{k=0}^{n} k·C(n,k) = n·2^{n−1} (n ≥ 1).

---

## Exercises (graded: ●○○ easy · ●●○ moderate · ●●● tough)

*Hints travel with the graded tiers; worked answers are at the end of the chapter (numbered A1–A22 to match). Try first.*

**Easy — one idea, applied directly**

1. (●○○) Compute D₁₀ with the recurrence engine of Lecture 1.2 (no closed formulas allowed), then check D₁₀/10! against 1/e.
2. (●○○) Count the lattice paths from (0,0) to (5,5) staying weakly below the diagonal — *using the mirror trick of Lecture 2.1 by naming the reflected endpoint and inverse boundary explicitly, not plugging into the closed formula*.
3. (●○○) From 5 women and 4 men, count the 3-person committees directly; then classify by composition (k women, 3−k men) and check the bookkeepings agree. *(This is Lecture 3 in your hands.)*
4. (●○○) List all balanced parenthesis strings of length 6. Then prove why balanced parenthesis strings of length 2n are counted by C_n, and predict the count for length 8.
5. (●○○) How many length-4 strings over {a,b,c} contain at least one of each letter? — *inclusion–exclusion, and mind the overlaps.*
6. (●○○) **Anagrams.** How many distinct rearrangements does the word BANANA have? And MISSISSIPPI? *Hint: P1 — temporarily label the identical letters so everything is distinguishable, count, then ask how many labelings collapse onto one printed arrangement.*

**Moderate — two ideas, or one tricky step**

7. (●●○) For every integer n ≥ 0, prove Σ_{k=0}^{n} C(n,k)² = C(2n,n). *Hint: P2 — choose n people from two rooms of n; or specialize Vandermonde.*
8. (●●○) Prove the derangements' second engine: **D_n = n·D_{n−1} + (−1)ⁿ** for every integer n ≥ 1. *Hint: P5 — start from D(x) = e^{−x}/(1−x), multiply both sides by (1−x), and extract the coefficient of xⁿ.*
9. (●●○) Show that D_n is the nearest integer to n!/e for every n ≥ 1. *Hint: P3 — bound the discarded alternating tail strictly below 1/(n+1).*
10. (●●○) Count the arrangements of n ≥ 1 letters in which *exactly one* letter lands in its correct envelope. *Hint: choose the lucky letter — n ways — then derange the rest (P3/P4).*
11. (●●○) **The ballot problem.** Candidate A scores a votes, B scores b, with a > b ≥ 0. In how many orderings of the ballots is A strictly ahead after every single ballot? (Paths (0,0)→(a,b) touching the diagonal only at the start.) *Hint: P6 — first reduce to the weak version by deleting A's forced first ballot, then run Lecture 2.1's reflection through the line y = x+1.*
12. (●●○) **The couples' banquet.** From 7 married couples (14 people), count the 5-person delegations that contain no married couple. *Hint: P3 — the zigzag of Lecture 1, with "a couple both chosen" playing the role of "a letter home." Mind where the zigzag honestly stops: how many couples fit in a 5-person delegation at all?*
13. (●●○) **Compositions.** For n ≥ 1, in how many ways can n be written as an *ordered* sum of positive integers? (For n = 4: 4, 3+1, 1+3, 2+2, 2+1+1, 1+2+1, 1+1+2, 1+1+1+1 — eight.) Prove your answer **two ways**: one bijection, one recurrence. *Hint: P1 on the n−1 gaps between n unit tokens — cut or glue; then P4, conditioning on the first summand.*
14. (●●○) **Committee, then subcommittee.** Prove that Σ_k C(n,k)·C(k,m) = C(n,m)·2^{n−m} for 0 ≤ m ≤ n. *Hint: P2 — count the pairs (committee S, subcommittee T) with T ⊆ S ⊆ {1,…,n} and |T| = m in two orders: choose S first, or choose T first and let S grow around it.*

**Tough — several chapter ideas combined**

15. (●●●) For n ≥ 1, count the paths from (0,0) to (n,n), on either side of the diagonal, that touch the diagonal **only at their two endpoints**. *Hint: once the side is chosen, the first and last steps are forced; strip them off, translate, and recognize what remains (Lecture 2.2's decomposition).*
16. (●●●) For every integer n ≥ 1, prove Σ_{k=0}^{n} (k − n/2)²·C(n,k) = n·2ⁿ⁻². *In words: the average subset has n/2 elements (Lecture 3.2) — this says how far it typically strays. Hint: differentiate (1+x)ⁿ twice at x = 1, then combine with Lecture 3.2's identity.*
17. (●●●) 2n people (n ≥ 1) sit at a round table. In how many ways can they split into n disjoint handshake pairs with **no two handshakes crossing**? *Hint: P1/P4 — fix person 1's partner; the handshake cuts the circle into two independent smaller circles; write the self-similarity (Lecture 2.2 style).*
18. (●●●) For n ≥ 1, find an explicit bijection between the triangulations of a convex (n+2)-gon and the balanced parenthesis strings of length 2n, and prove it is invertible. *Hint: P1 — distinguish one base edge of the polygon; the unique triangle sitting on that edge splits the polygon into two smaller polygons; recurse. Verify on the pentagon (n = 3) by listing all 5 triangulations and their 5 strings.*

19. (●●●) **Onto functions.** Count the functions from a 6-element set onto a 3-element set (every value must be hit at least once); then find the general formula for onto functions from an n-element set to a k-element set (n, k ≥ 1). *Hint: P3 again, but the bad events are now *misses* — a function avoiding a fixed set of j target values can land anywhere in the remaining k−j values. What is the derangement lesson's zigzag, transplanted?*

**Pattern unknown — you choose the tool** *The graded sets above tell you which lecture idea to reach for — research and exams do not. No hints here, and no difficulty rating either: diagnosing the problem is part of the problem. Worked answers still wait at the end.*

20. (◆) For n ≥ 0, how many subsets of {1, …, n} contain no two consecutive integers?
21. (◆) Show that for n ≥ 1, the subsets of {1, …, n} of even size are exactly as many as those of odd size.
22. (◆) n ≥ 0 straight lines are drawn in the plane, no two parallel and no three through a point. Into how many regions do they cut the plane?

**Explorations — ◐ research-style training** *No single right answer — what you should find is described in each. These train the habit research actually runs on: changing the problem.*

X1. (◐) **When letters may be correct.** Count the arrangements with *exactly r* letters home (choose the r lucky letters, derange the rest — these are the **rencontres numbers**). Then compute, for every n, the *expected* number of home letters in a random arrangement — count the pairs (letter, arrangement where it is home) two ways, Lecture 3's engine. You should find a strikingly clean answer independent of n; meditate on why. Then code it: for n = 5, 10, 20, tally the number of home letters over many random arrangements and watch the distribution settle — you should recognize Lecture 1.4's 1/e grown into a whole law (the count of home letters converges to a Poisson(1) distribution). Explain to yourself why the events "letter i is home" are rare, approximately independent events — each occurring with probability 1/n — and where the dependence hides.

X2. (◐) **Catalan paths in a band.** Restrict the walker to the band x − 2 ≤ y ≤ x (she may fall at most two behind): count paths to (n,n) for n = 1..6 by hand and by code, and find the recurrence they satisfy — it is unusually simple; find the *reason* for its simplicity. One boundary alone still surrenders to the mirror trick of Lecture 2.1; with two, the mirrored images overlap, and the honest repair is Lecture 1's zigzag (P3) applied to whole reflected worlds. No answer is provided here: hitting the edge of a method — and repairing it — is the exercise.

---

## Computational Lab (verified)

Both engines of Lecture 1 and Lecture 2 — with their boundary cases — cross-checked by execution (2026-10-09; re-run 2026-10-13; re-run 2026-10-23 as a line-for-line TypeScript port, all assertions and prints reproduced):

```python
from fractions import Fraction
from itertools import combinations, permutations, product
from math import comb, e, factorial

def D_rec(n):                       # recurrence engine (Lecture 1.2)
    if n < 0:
        raise ValueError("n must be >= 0")
    if n == 0:
        return 1
    if n == 1:
        return 0
    D = [1, 0]
    for i in range(2, n + 1):
        D.append((i - 1) * (D[i-1] + D[i-2]))
    return D[n]

def D_one_step(n):                  # one-step engine (Exercise 8: D_n = n*D_{n-1} + (-1)**n)
    if n < 0:
        raise ValueError("n must be >= 0")
    d = 1
    for i in range(1, n + 1):
        d = i * d + (-1)**i
    return d

def D_ie(n):                        # inclusion-exclusion engine (Lecture 1.1)
    if n < 0:
        raise ValueError("n must be >= 0")
    return sum((-1)**k * comb(n, k) * factorial(n - k) for k in range(n + 1))

def C_rec(n):                       # Catalan first-return recurrence (Lecture 2.2)
    if n < 0:
        raise ValueError("n must be >= 0")
    C = [1]
    for i in range(1, n + 1):
        C.append(sum(C[k] * C[i-1-k] for k in range(i)))
    return C[n]

def C_mirror(n):                    # reflection-difference engine (Lecture 2.1)
    if n < 0:
        raise ValueError("n must be >= 0")
    bad = comb(2*n, n - 1) if n >= 1 else 0
    return comb(2*n, n) - bad

def C_newton_coeff(m):              # Newton half-integer binomial coefficient (Lecture 2.2)
    if m < 1:
        raise ValueError("m must be >= 1")
    c = Fraction(1, 1)
    for j in range(m):
        c *= Fraction(1, 2) - j
    c /= factorial(m)
    return int(c * (-4)**m)

assert all(0 <= D_rec(n) == D_one_step(n) == D_ie(n) <= factorial(n) for n in range(11))
assert all(sum(comb(n, k) * D_rec(n - k) for k in range(n + 1)) == factorial(n)
           for n in range(11))      # EGF convolution e^x * D(x) = 1/(1-x) (Lecture 1.3)
assert all(abs(D_rec(n) - factorial(n) / e) < 1 / (n + 1) for n in range(1, 11))
assert all(0 <= C_rec(n) == C_mirror(n) == comb(2*n, n) // (n + 1) <= comb(2*n, n) <= 4**n
           for n in range(11))
assert all(C_newton_coeff(m) == -2 * comb(2*m - 2, m - 1) // m
           for m in range(1, 12))   # Newton series identity (Lecture 2.2)
assert all(sum(comb(m, k) * comb(n, r - k) for k in range(r + 1)) == comb(m + n, r)
           for m in range(6) for n in range(6) for r in range(m + n + 1))
assert all(sum(comb(n, k) for k in range(n + 1)) == 2**n for n in range(11))
assert all(sum(k * comb(n, k) for k in range(n + 1))
           == (n * 2**(n - 1) if n >= 1 else 0) for n in range(11))

# Lecture 1, 1.1, 1.3, 1.4, 2.2, 3.1, 3.2, and 4 Checkpoint & prose witnesses
assert [p for p in permutations((1, 2)) if all(p[j] != j + 1 for j in range(2))] == [(2, 1)]
assert [p for p in permutations((1, 2, 3)) if all(p[j] != j + 1 for j in range(3))] == [(2, 3, 1), (3, 1, 2)]
assert sorted(p for p in permutations((1, 2, 3))
              if any(p[j] == j + 1 for j in range(3))) == [(1, 2, 3), (1, 3, 2), (2, 1, 3), (3, 2, 1)]
four_cycles_4 = [(2, 3, 4, 1), (2, 4, 1, 3), (3, 1, 4, 2), (3, 4, 2, 1), (4, 1, 2, 3), (4, 3, 1, 2)]
double_trans_4 = [(2, 1, 4, 3), (3, 4, 1, 2), (4, 3, 2, 1)]
assert len(four_cycles_4) == 6 and len(double_trans_4) == 3
assert sorted(p for p in permutations((1, 2, 3, 4))
              if all(p[j] != j + 1 for j in range(4))) == sorted(four_cycles_4 + double_trans_4)
assert 24 - 12 + 4 - 1 == 15 and 24 - 15 == D_rec(4) == 9
assert 120 - 120 + 60 - 20 + 5 - 1 == D_rec(5) == 44
assert sum(Fraction((-1)**k, factorial(k)) for k in range(3)) == Fraction(1, 2) == Fraction(D_rec(2), factorial(2))
assert [comb(3, k) * D_rec(3 - k) for k in range(4)] == [2, 3, 0, 1] and sum([2, 3, 0, 1]) == factorial(3) == 6
assert Fraction(D_rec(4), factorial(4)) - Fraction(D_rec(5), factorial(5)) == Fraction(1, factorial(5))
assert D_rec(6) == 265 and factorial(6) == 720 and abs(265 / 720 - 1 / e) < 1 / factorial(7)
assert Fraction(D_rec(7), factorial(7)) == Fraction(1854, 5040) == Fraction(103, 280)
assert Fraction(D_rec(8), factorial(8)) == Fraction(14833, 40320)
assert (C_rec(2), comb(4, 2), 4**2) == (2, 6, 16)
assert [comb(2, k) * comb(2, 2 - k) for k in range(3)] == [1, 4, 1] and comb(4, 2) == 6
assert sum(len(s) for r in range(4) for s in combinations(range(1, 4), r)) == 12
assert [comb(3, k) for k in range(4)] == [1, 3, 3, 1] and sum([1, 3, 3, 1]) == 2**3 == 8

print("D_n, n = 2..9:", [D_rec(n) for n in range(2, 10)])
print("D_9/9! =", round(D_rec(9) / factorial(9), 5))
print("Catalan, n = 0..10:", [C_rec(n) for n in range(11)])
```

**Verified output (printed by the block above; the assertions passed on the same runs — 2026-10-09, re-run 2026-10-13, TypeScript port 2026-10-23):** D_n for n = 2..9 = 1, 2, 9, 44, 265, 1854, 14833, 133496 — three engines agree everywhere (n = 0..10, boundary cases D₀ = 1 and D₁ = 0 included), and the EGF convolution Σ_{k=0}^{n} C(n,k)·D_{n−k} = n! of Lecture 1.3 holds for n = 0..10; D₉/9! = 0.36788 ≈ 1/e (Lecture 1.4, live). Catalan n = 0..10 = 1, 1, 2, 5, 14, 42, 132, 429, 1430, 4862, 16796 — recurrence, reflection difference, Newton half-integer series C(1/2,m)·(−4)^m = −(2/m)·C(2m−2, m−1), and closed form agree. The assertions certify more than the prints show: the nearest-integer bound |D_n − n!/e| < 1/(n+1) holds for n = 1..10 (Exercise 9's bound, live), and the Lecture 3/4 identities hold at every size tested — Vandermonde for all m, n ≤ 5 and r ≤ m+n, Σ C(n,k) = 2^n and Σ k·C(n,k) = n·2^{n−1} for n = 0..10, with the n = 0 case reading 0 = 0 as §3.2 records.

### Part 2 — the reflection bijection, machine-tested (verified 2026-10-10; re-run 2026-10-13; re-run 2026-10-23 as a TypeScript port, boundary sizes and answer-key suite added)

A formula can lie about being a bijection — and, in fairness, so can code: a small-case test is an error *detector*, not a proof (the nearest-integer property of Exercise 9 (worked in A9) is settled by an argument, not by a tally, and no finite run of code replaces that). What code adds is a check the eye cannot fake. Lecture 2.1's map, together with its inverse (first touch of x = y+1), round-tripped over **all** small paths — the test that separates a bijection from a coincidence of totals — followed by machine verification of Lecture 2.2's first-return cut and the worked answers A1–A22:

```python
from itertools import combinations, permutations, product
from math import comb, e, factorial

def all_paths(a, b):
    if a < 0 or b < 0:
        return set()
    steps = a + b
    return {''.join('E' if i in east else 'N' for i in range(steps))
            for east in combinations(range(steps), a)}

def path_coords(p):                 # vertex sequence [(x_0, y_0), ..., (x_m, y_m)]
    x = y = 0
    pts = [(0, 0)]
    for s in p:
        x += (s == 'E'); y += (s == 'N')
        pts.append((x, y))
    return pts

def first_touch_index(p, target):   # earliest step k where (y - x) == target
    x = y = 0
    for k, s in enumerate(p):
        x += (s == 'E'); y += (s == 'N')
        if y - x == target:
            return k
    return None

def forward(p):    # bad path to (n,n): swap head at first touch of y - x = +1
    k = first_touch_index(p, +1)
    if k is None:
        return None                  # no touch: map undefined -- bug alarm
    return p[:k+1].translate(str.maketrans('EN','NE')) + p[k+1:]

def inverse(q):    # any path to (n+1, n-1): swap head at first touch of y - x = -1
    k = first_touch_index(q, -1)
    if k is None:
        return None
    return q[:k+1].translate(str.maketrans('EN','NE')) + q[k+1:]

def mirror_boundary_coords(p):      # Lecture 2.1: reflect head across y = x+1, then shift all by (1, -1)
    k = first_touch_index(p, +1)
    if k is None:
        return None
    pts = path_coords(p)
    reflected = [(y - 1, x + 1) if j <= k + 1 else (x, y) for j, (x, y) in enumerate(pts)]
    return [(x + 1, y - 1) for x, y in reflected]

def mirror_diagonal_coords(p):      # Lecture 2.1: reflect head across y = x, then shift tail by (1, -1)
    k = first_touch_index(p, +1)
    if k is None:
        return None
    pts = path_coords(p)
    return [(y, x) if j <= k + 1 else (x + 1, y - 1) for j, (x, y) in enumerate(pts)]

def first_return_split(p):          # Lecture 2.2: good path P -> (A, B) via P = E[A]N[B]
    if not p:
        raise ValueError("path must be nonempty")
    x = y = 0
    for j, s in enumerate(p):
        x += (s == 'E'); y += (s == 'N')
        if x == y:
            assert p[0] == 'E' and p[j] == 'N'
            return p[1:j], p[j+1:]
    raise ValueError("path never returns to diagonal")

# Lecture 1.2: Formal bijection & disjoint partition check for B_i (D_{n-2}) and A_i <-> D' (D_{n-1})
for n in range(2, 7):
    der_n = [p for p in permutations(range(1, n + 1))
             if all(p[j - 1] != j for j in range(1, n + 1))]
    der_sub = {p for p in permutations(range(2, n + 1))
               if all(p[j - 2] != j for j in range(2, n + 1))}
    part_union = []
    for i in range(2, n + 1):
        B_i = [p for p in der_n if p[0] == i and p[i - 1] == 1]
        A_i = [p for p in der_n if p[0] == i and p[i - 1] != 1]
        part_union.extend(B_i); part_union.extend(A_i)
        assert len(B_i) == D_rec(n - 2) and len(A_i) == D_rec(n - 1)
        phi_A = {tuple(i if p[j - 1] == 1 else p[j - 1] for j in range(2, n + 1)) for p in A_i}
        assert phi_A == der_sub
        for sigma in der_sub:
            psi = (i,) + tuple(1 if sigma[j - 2] == i else sigma[j - 2] for j in range(2, n + 1))
            assert psi in A_i
        if n == 2 and i == 2:
            assert B_i == [(2, 1)] and A_i == [] and der_sub == set()
        if n == 3 and i == 3:
            assert A_i == [(3, 1, 2)] and phi_A == {(3, 2)}
    assert len(part_union) == len(set(part_union)) == len(der_n) and set(part_union) == set(der_n)

for n in range(5):                   # includes the boundary sizes n = 0 and 1
    total = all_paths(n, n)
    bads = [p for p in total if forward(p) is not None]
    goods = [p for p in total if forward(p) is None]
    images = [forward(p) for p in bads]
    mirror = all_paths(n+1, n-1)
    assert len(bads) == len(set(images)) == len(mirror) == (comb(2*n, n-1) if n >= 1 else 0)
    assert len(goods) == comb(2*n, n) // (n + 1)           # the good count is C_n
    assert set(images) == mirror                          # bijection onto the mirror world
    assert all(inverse(forward(p)) == p for p in bads)    # round trip, bad side
    assert all(forward(inverse(q)) == q for q in mirror)  # round trip, mirror side
    assert all(first_touch_index(p, +1) == first_touch_index(forward(p), -1)
               for p in bads)                             # first-touch index preserved
    assert all(mirror_boundary_coords(p) == mirror_diagonal_coords(p) == path_coords(forward(p))
               for p in bads)                             # both geometric mirror descriptions match
    if n == 2:
        assert sorted(goods) == ['EENN', 'ENEN']
        assert sorted(bads) == ['ENNE', 'NEEN', 'NENE', 'NNEE']
        assert mirror_boundary_coords('ENNE') == [(0, 0), (0, 1), (1, 1), (2, 1), (3, 1)]
    if n == 3:
        assert sorted(goods) == ['EEENNN', 'EENENN', 'EENNEN', 'ENEENN', 'ENENEN']
        assert first_return_split('EENNEN') == ('EN', 'EN')
    if n >= 1:
        splits = [first_return_split(p) for p in goods]
        assert all('E' + A + 'N' + B == p for p, (A, B) in zip(goods, splits))
    if n in (2, 3):
        print("n =", n, "|", len(bads), "bad of", len(total))
        print("      ", len(set(images)), "images,", len(mirror), "mirror paths")

assert forward('EEEN') is None   # the WRONG inverse hunts y = x+1 here: nothing to find

# Lecture 2.3: Full binary trees with n+1 leaves and stack-sortable permutations
def binary_trees(n):                # n internal nodes (n+1 leaves)
    if n < 0:
        raise ValueError("n must be >= 0")
    if n == 0:
        return ['L']
    return [('N', L, R) for k in range(n)
            for L in binary_trees(k) for R in binary_trees(n - 1 - k)]

def tree_to_path(T):
    return '' if T == 'L' else 'E' + tree_to_path(T[1]) + 'N' + tree_to_path(T[2])

def stack_sort_path(perm):          # returns push-pop path sorting perm to 1..n, or None
    stack, out, path, nxt = [], [], [], 1
    for x in perm:
        while stack and stack[-1] == nxt:
            out.append(stack.pop()); path.append('N'); nxt += 1
        stack.append(x); path.append('E')
    while stack:
        out.append(stack.pop()); path.append('N')
    return ''.join(path) if out == list(range(1, len(perm) + 1)) else None

def avoids_231(perm):
    return not any(perm[k] < perm[i] < perm[j]
                   for i, j, k in combinations(range(len(perm)), 3))

def stack_first_return_decomp(perm): # Lecture 2.3: pi = (k+1) L' R' -> E [A] N [B]
    if not perm:
        return ''
    k = perm[0] - 1
    L_prime = perm[1:k+1]
    R_prime = tuple(x - k - 1 for x in perm[k+1:])
    return 'E' + stack_first_return_decomp(L_prime) + 'N' + stack_first_return_decomp(R_prime)

def psi_max_decomp(perm):           # Lecture 2.3: pi = L n R -> [Psi(L)] E [Psi(R)] N
    if not perm:
        return ''
    m = max(perm)
    idx = perm.index(m)
    return psi_max_decomp(perm[:idx]) + 'E' + psi_max_decomp(perm[idx+1:]) + 'N'

for n in range(5):
    trees = binary_trees(n)
    tree_paths = {tree_to_path(T) for T in trees}
    good_paths = {p for p in all_paths(n, n) if forward(p) is None}
    assert len(trees) == C_rec(n) and tree_paths == good_paths
    sortable = [p for p in permutations(range(1, n + 1)) if stack_sort_path(p) is not None]
    assert sortable == [p for p in permutations(range(1, n + 1)) if avoids_231(p)]
    assert {stack_sort_path(p) for p in sortable} == good_paths
    for p in permutations(range(1, n + 1)):
        if n >= 1:
            idx = p.index(n)
            L, R = p[:idx], p[idx+1:]
            assert avoids_231(p) == (avoids_231(L) and avoids_231(R)
                                     and set(L) == set(range(1, idx + 1)))
        if avoids_231(p):
            assert stack_sort_path(p) == stack_first_return_decomp(p) == psi_max_decomp(p)
assert stack_sort_path((1, 2)) == 'ENEN' and stack_sort_path((2, 1)) == 'EENN'
assert [p for p in permutations((1, 2, 3)) if stack_sort_path(p) is None] == [(2, 3, 1)]

# Lecture 3.1, 3.2, and Lecture 4: Committee partition, antidiagonal path partition, incidence fibers, bit-switch bijection
for m in range(4):
    W = {f'w{i}' for i in range(m)}
    for n in range(4):
        M = {f'm{j}' for j in range(n)}
        for r in range(m + n + 1):
            all_comm = [frozenset(c) for c in combinations(W | M, r)]
            assert len(all_comm) == comb(m + n, r)
            paths_mnr = all_paths(m + n - r, r)
            for k in range(r + 1):
                comm_k = [c for c in all_comm if len(c & W) == k]
                assert len(comm_k) == comb(m, k) * comb(n, r - k)
                at_height_k = [p for p in paths_mnr if p[:m].count('N') == k]
                assert len(at_height_k) == comb(m, k) * comb(n, r - k)
for n in range(5):
    powerset = [frozenset(s) for r in range(n + 1) for s in combinations(range(1, n + 1), r)]
    incidence = [(x, s) for s in powerset for x in s]
    assert len(incidence) == sum(len(s) for s in powerset) == (n * 2**(n - 1) if n >= 1 else 0)
    bits = {tuple(1 if i in s else 0 for i in range(1, n + 1)) for s in powerset}
    assert bits == set(product((0, 1), repeat=n))
    for x in range(1, n + 1):
        with_x = [s for s in powerset if x in s]
        without_x = [s for s in powerset if x not in s]
        assert {s - {x} for s in with_x} == set(without_x) and len(with_x) == 2**(n - 1)

# --- Answer-Key & Exploration Verification Suite (A1-A22) ---
# A1: D_10 and 1/e error bound
assert [D_rec(k) for k in range(11)] == [1, 0, 1, 2, 9, 44, 265, 1854, 14833, 133496, 1334961]
assert D_rec(10) == 9 * (133496 + 14833) == 1334961 and factorial(10) == 3628800 and factorial(11) == 39916800
assert abs(D_rec(10) / factorial(10) - 1 / e) < 1 / factorial(11)

# A2 & A3: C_5 via mirror difference & bijection at n=5; committee double count
bads_5 = [p for p in all_paths(5, 5) if forward(p) is not None]
mirror_5 = all_paths(6, 4)
assert comb(10, 5) == 252 and len(bads_5) == len(mirror_5) == comb(10, 4) == 210 and 252 - 210 == 42
assert {forward(p) for p in bads_5} == mirror_5
assert [comb(5, k) * comb(4, 3 - k) for k in range(4)] == [4, 30, 40, 10]
assert comb(9, 3) == sum(comb(5, k) * comb(4, 3 - k) for k in range(4)) == 84

# A4: Balanced parenthesis strings of length 6 and 8
def is_balanced(s):
    bal = 0
    for ch in s:
        bal += 1 if ch == '(' else -1
        if bal < 0:
            return False
    return bal == 0
bal_6 = sorted(s for s in (''.join(p) for p in product('()', repeat=6)) if is_balanced(s))
bal_8 = sorted(s for s in (''.join(p) for p in product('()', repeat=8)) if is_balanced(s))
assert bal_6 == ['((()))', '(()())', '(())()', '()(())', '()()()']
assert len(bal_6) == 5 and len(bal_8) == C_rec(4) == 14
assert [sum(1 for s in bal_8
            if len(first_return_split(s.translate(str.maketrans('()', 'EN')))[0]) == a_len)
        for a_len in (0, 2, 4, 6)] == [5, 2, 2, 5]
assert {a_len: sorted(s for s in bal_8
                      if len(first_return_split(s.translate(str.maketrans('()', 'EN')))[0]) == a_len)
        for a_len in (0, 2, 4, 6)} == {
    0: ['()((()))', '()(()())', '()(())()', '()()(())', '()()()()'],
    2: ['(())(())', '(())()()'],
    4: ['((()))()', '(()())()'],
    6: ['(((())))', '((()()))', '((())())', '(()(()))', '(()()())'],
}

# A5 & A6: Surjective length-4 strings over {a,b,c}; anagrams of BANANA and MISSISSIPPI
assert 3**4 - 3 * 2**4 + 3 * 1**4 - 0 == 81 - 48 + 3 == 3 * comb(4, 2) * factorial(2) == 36
assert sum(1 for s in product('abc', repeat=4) if set(s) == {'a', 'b', 'c'}) == 36
assert len(set(permutations('BANANA'))) == factorial(6) // (factorial(3) * factorial(2)) == 720 // 12 == 60
assert factorial(11) == 39916800 and factorial(4) * factorial(4) * factorial(2) == 1152
assert factorial(11) // (factorial(4) * factorial(4) * factorial(2)) == 330 * 35 * 3 == 34650

# A7, A8, A9, A10: Vandermonde squares, 1-step derangement, nearest integer, 1 fixed point
assert all(sum(comb(n, k)**2 for k in range(n + 1)) == comb(2*n, n) for n in range(11))
assert D_rec(5) == 5 * D_rec(4) - 1 == 44
assert all(D_rec(n) - n * D_rec(n - 1) == (-1)**n for n in range(1, 11))
assert all(0 < (-1)**(n + 1) * (factorial(n) / e - D_rec(n)) < 1 / (n + 1) for n in range(1, 11))
assert all(D_rec(n) == round(factorial(n) / e) for n in range(1, 11))
for n in range(1, 7):
    fixed_one = sum(1 for p in permutations(range(n))
                    if sum(p[i] == i for i in range(n)) == 1)
    assert fixed_one == n * D_rec(n - 1)
assert [n * D_rec(n - 1) for n in range(1, 5)] == [1, 0, 3, 8]

# A11: Ballot problem (weak and strict versions, including q=0 and b=0 edge cases)
for p in range(6):
    for q in range(p + 1):
        weak_paths = [w for w in all_paths(p, q)
                      if all(w[:k].count('E') >= w[:k].count('N') for k in range(1, p + q + 1))]
        assert len(weak_paths) == (p - q + 1) * comb(p + q, q) // (p + 1)
for a in range(1, 6):
    for b in range(a):
        strict_paths = [w for w in all_paths(a, b)
                        if all(w[:k].count('E') > w[:k].count('N') for k in range(1, a + b + 1))]
        assert len(strict_paths) == (a - b) * comb(a + b, b) // (a + b)
        if a == 2 and b == 1:
            assert strict_paths == ['EEN']

# A12: Couples' banquet (Machine check cited in A12)
couples = [{2*i, 2*i + 1} for i in range(7)]
delegations = list(combinations(range(14), 5))
no_couple = [d for d in delegations if not any(c.issubset(d) for c in couples)]
assert comb(14, 5) == 2002 and comb(12, 3) == 220 and comb(10, 1) == 10
assert len(delegations) == 2002 and len(no_couple) == 2002 - 7*220 + 21*10 == 672

# A13: Compositions of n for n = 1..12 (Machine check cited in A13)
def count_compositions(n):
    if n < 0:
        raise ValueError("n must be >= 0")
    C_comp = [1]
    for i in range(1, n + 1):
        C_comp.append(sum(C_comp[i - m] for m in range(1, i + 1)))
    return C_comp[n]
comp_1_to_12 = [count_compositions(n) for n in range(1, 13)]
assert comp_1_to_12 == [2**(n - 1) for n in range(1, 13)]

# A14: Committee-subcommittee identity for all n <= 12 (Machine check cited in A14)
for n in range(13):
    for m in range(n + 1):
        lhs = sum(comb(n, k) * comb(k, m) for k in range(m, n + 1))
        rhs = comb(n, m) * 2**(n - m)
        assert lhs == rhs
assert comb(8, 3) * 2**(8 - 3) == 1792

# A15, A16, A17: Endpoint-only diagonal paths; variance identity; non-crossing pairings
for n in range(1, 6):
    endpoint_only = sorted(p for p in all_paths(n, n)
                           if all(p[:k].count('E') != p[:k].count('N') for k in range(1, 2*n)))
    assert len(endpoint_only) == 2 * C_rec(n - 1)
    if n == 1:
        assert endpoint_only == ['EN', 'NE']
    if n == 2:
        assert endpoint_only == ['EENN', 'NNEE']
    if n == 3:
        assert endpoint_only == ['EEENNN', 'EENENN', 'NNENEE', 'NNNEEE']
assert all(sum(k * (k - 1) * comb(n, k) for k in range(n + 1)) == n * (n - 1) * 2**(n - 2)
           for n in range(1, 11))
assert all(sum(k**2 * comb(n, k) for k in range(n + 1)) == n * (n + 1) * 2**(n - 2)
           for n in range(1, 11))
assert all(sum((k - n / 2)**2 * comb(n, k) for k in range(n + 1)) == n * 2**(n - 2)
           for n in range(1, 11))

def non_crossing_pairings(verts):   # A17: explicit enumeration of non-crossing pairings
    if not verts:
        return [frozenset()]
    v0 = verts[0]
    res = []
    for idx in range(1, len(verts), 2):
        partner = verts[idx]
        for L in non_crossing_pairings(verts[1:idx]):
            for R in non_crossing_pairings(verts[idx+1:]):
                res.append(frozenset({(v0, partner)}) | L | R)
    return res
assert [len(non_crossing_pairings(list(range(1, 2*n + 1)))) for n in range(5)] == [C_rec(n) for n in range(5)]
assert set(non_crossing_pairings([1, 2, 3, 4])) == {
    frozenset({(1, 2), (3, 4)}),
    frozenset({(1, 4), (2, 3)}),
}

# A18: Recursive triangulation-to-parenthesis bijection and inverse on n = 0..4
def tri_to_parens(lo, hi, diags):
    if hi - lo < 1:
        raise ValueError("Invalid polygon interval")
    if hi - lo == 1:
        return ""
    for k in range(lo + 1, hi):
        e1 = (lo, k) if k - lo > 1 else None
        e2 = (k, hi) if hi - k > 1 else None
        if (e1 is None or e1 in diags) and (e2 is None or e2 in diags):
            return "(" + tri_to_parens(lo, k, diags) + ")" + tri_to_parens(k, hi, diags)
    raise ValueError("Invalid triangulation")

def parens_to_tri(lo, hi, s):
    if hi - lo < 1:
        raise ValueError("Invalid polygon interval")
    if not s:
        assert hi - lo == 1
        return set()
    bal = 0
    for idx, ch in enumerate(s):
        bal += 1 if ch == '(' else -1
        if bal == 0:
            k = lo + 1 + (idx - 1) // 2
            diags = set()
            if k - lo > 1:
                diags.add((lo, k))
            if hi - k > 1:
                diags.add((k, hi))
            return diags | parens_to_tri(lo, k, s[1:idx]) | parens_to_tri(k, hi, s[idx+1:])
    raise ValueError("Unbalanced string")

pentagon_table = [
    ({(1, 4), (2, 4)}, "()()()"),
    ({(1, 4), (1, 3)}, "()(())"),
    ({(0, 2), (2, 4)}, "(())()"),
    ({(0, 3), (1, 3)}, "(()())"),
    ({(0, 3), (0, 2)}, "((()))"),
]
assert tri_to_parens(0, 1, set()) == "" and parens_to_tri(0, 1, "") == set()
assert [tri_to_parens(0, 4, d) for d, _ in pentagon_table] == [s for _, s in pentagon_table]
assert [parens_to_tri(0, 4, s) for _, s in pentagon_table] == [d for d, _ in pentagon_table]
assert all(tri_to_parens(0, 5, parens_to_tri(0, 5, s)) == s for s in bal_8)

# A19: Onto functions [6]->[3], [5]->[5], [n]->[1], and pigeonhole n < k (Machine check cited in A19)
onto_6_3 = sum(1 for f in product(range(3), repeat=6) if len(set(f)) == 3)
S_6_3_parts = (comb(6, 4) * comb(2, 1) * comb(1, 1) // factorial(2),
               comb(6, 3) * comb(3, 2) * comb(1, 1),
               comb(6, 2) * comb(4, 2) * comb(2, 2) // factorial(3))
assert S_6_3_parts == (15, 60, 15) and sum(S_6_3_parts) == 90
assert onto_6_3 == 3**6 - 3 * 2**6 + 3 * 1**6 == factorial(3) * sum(S_6_3_parts) == 540
assert [(-1)**j * comb(5, j) * (5 - j)**5 for j in range(6)] == [3125, -5120, 2430, -320, 5, 0]
assert sum((-1)**j * comb(5, j) * (5 - j)**5 for j in range(6)) == factorial(5) == 120
assert all(sum((-1)**j * comb(1, j) * (1 - j)**n for j in range(2)) == 1 for n in range(1, 7))
assert sum((-1)**j * comb(3, j) * (3 - j)**2 for j in range(4)) == 9 - 12 + 3 == 0

# A20, A21, A22: No-consecutive subsets (Fibonacci), even/odd subsets, plane regions
fib_counts = [1, 2, 3, 5, 8, 13, 21]
for n in range(7):
    no_consec = [s for r in range(n + 1) for s in combinations(range(1, n + 1), r)
                 if all(s[i+1] - s[i] > 1 for i in range(len(s) - 1))]
    even_subs = [set(s) for r in range(0, n + 1, 2) for s in combinations(range(1, n + 1), r)]
    odd_subs = [set(s) for r in range(1, n + 1, 2) for s in combinations(range(1, n + 1), r)]
    assert len(no_consec) == fib_counts[n]
    if n == 3:
        assert no_consec == [(), (1,), (2,), (3,), (1, 3)]
    if n >= 1:
        assert len(even_subs) == len(odd_subs) == 2**(n - 1)
        assert {frozenset(s ^ {1}) for s in even_subs} == {frozenset(s) for s in odd_subs}
        assert sum((-1)**k * comb(n, k) for k in range(n + 1)) == 0
assert [1 + n * (n + 1) // 2 for n in range(6)] == [1, 2, 4, 7, 11, 16]

print("A12, A13, A14, A19 checks:", len(no_couple), comp_1_to_12[:4], 1792, onto_6_3)
```

**Verified output (2026-10-10; the block prints the counts and asserts the rest; re-run 2026-10-23 as a TypeScript port, with the boundary sizes and answer-key suite added):** n = 2 — 4 bad paths (of 6 total), 4 distinct images, all 4 paths to (3,1) covered, both round trips exact. n = 3 — 15 bad paths (of 20; 20 − C₃ = 20 − 5 = 15 ✓), 15 distinct images, all 15 paths to (4,2) covered, both round trips exact. At the boundary sizes the same assertions hold: n = 0 (one path, the empty one, trivially good — no bad paths, no mirror), n = 1 (two paths; the single bad path NE ↔ its mirror EE, and good = 1 = C₁), and at every size n = 0..4 the counts match the closed forms — bad = C(2n, n−1), good = C_n, mirror total = bad — with the **first-touch index m preserved under the map in both directions** (m for y = x+1 forward, m for x = y+1 back), the §2.1 proof's key invariant witnessed by machine, and with Lecture 2.2's first-return decomposition E[A]N[B] round-tripping every nonempty good path. Moreover, `forward('EEEN')` returns **None**: a path to (3,1) never touches y = x+1 — the alarm that proves the inverse must search for **x = y+1**. Finally, the answer-key verification suite reproduces every cited count in A1–A22 (672 [1, 2, 4, 8] 1792 540). *The lesson: when a chapter claims a bijection, the lab implements the map **and its inverse** and round-trips everything — matching totals certify a count, never a correspondence.*

**What to explore:** plot D_n·e/n! for n = 1..15 approaching 1 — and note that A9 proves the nearest-integer property *never* fails, so do not hunt a counterexample; instead watch the true rounding residual |D_n − n!/e| against its proven bound 1/(n+1) — the first omitted term of the alternating series — and measure how tightly it tracks the true error.

---

## Answers to the Exercises

*Attempt everything first — the value is in the attempt; these pages will still be here when you return.*

**A1.** Starting from the seeds D₀ = 1 and D₁ = 0, the recurrence D_n = (n−1)(D_{n−1} + D_{n−2}) produces step by step: D₂ = 1(0+1) = 1, D₃ = 2(1+0) = 2, D₄ = 3(2+1) = 9, D₅ = 4(9+2) = 44, D₆ = 5(44+9) = 265, D₇ = 6(265+44) = 1854, D₈ = 7(1854+265) = 14833, D₉ = 8(14833+1854) = 133496, and D₁₀ = 9·(D₉ + D₈) = 9·(133496 + 14833) = **1,334,961**. Then D₁₀/10! = 1334961/3628800 ≈ **0.367879464**, whereas 1/e ≈ 0.367879441 (differing by less than 1/11! = 1/39916800 ≈ 2.5 × 10⁻⁸) ≈ 1/e ✓ — Lecture 1.4, live at n = 10.

**A2.** Total paths to (5,5): C(10,5) = 252. A bad path first touches y = x+1 at some earliest vertex (t, t+1) after 2t+1 steps (0 ≤ t ≤ 4), so its prefix has t East steps and t+1 North steps while its suffix has 5−t East steps and 4−t North steps; reflect its head through that line by swapping E ↔ N in the prefix — a path with (t+1) + (5−t) = 6 East steps and t + (4−t) = 4 North steps, ending at (6,4) instead, of which there are C(10,4) = 210. Good: 252 − 210 = **42** = C₅ ✓ (the map inverts honestly: a path to (6,4) has x − y travelling from 0 up to 6 − 4 = 2 by unit steps ±1, so it touches the inverse boundary x = y + 1 somewhere, and swapping the head at the *first* such touch (t+1, t) returns the bad path with first touch at (t, t+1) on y = x + 1 — the same two-sided check as Lecture 2.1).

**A3.** Direct: C(9,3) = (9·8·7)/(3·2·1) = 84. By composition (k women from 5, 3−k men from 4, counted by C(5,k)·C(4,3−k)): k=0: C(5,0)·C(4,3) = 1·4 = 4; k=1: C(5,1)·C(4,2) = 5·6 = 30; k=2: C(5,2)·C(4,1) = 10·4 = 40; k=3: C(5,3)·C(4,0) = 10·1 = 10. Sum 4+30+40+10 = **84** ✓. One world, two bookkeepings.

**A4.** Length 6: **()()(), ()(()), (())(), (()()), ((()))** — five strings = C₃ ✓. Why does C_n count balanced strings of length 2n in general? Replace every ( with an East step E and every ) with a North step N: a string of length 2n over {(, )} is balanced if and only if (i) the total number of ( equals the total number of ) (so there are n of each, meaning the corresponding lattice path ends at (n,n)), and (ii) in every prefix of length j ∈ {1, …, 2n}, the number of ('s is at least the number of )'s — which says x_j ≥ y_j at every vertex (x_j, y_j) along the path. Because the letter-by-letter replacement ( ↔ E, ) ↔ N is a bijection on words of length 2n that preserves both conditions (i) and (ii) in both directions, it restricts to a bijection onto the good Catalan paths of Lecture 2. For length 8, then: **C₄ = 14** (from the recurrence C₄ = C₀C₃ + C₁C₂ + C₂C₁ + C₃C₀ = 5+2+2+5, or the closed form (1/5)·C(8,4) = 70/5 = 14; explicitly, grouping by the first-return decomposition (A)B produces the 5 strings ()()()(), ()()(()), ()(())(), ()(()()), ()((())) for |A| = 0, the 2 strings (())()(), (())(()) for |A| = 2, the 2 strings (()())(), ((()))() for |A| = 4, and the 5 strings (()()()), (()(())), ((())()), ((()())), (((()))) for |A| = 6).

**A5.** Let U be the set of all length-4 strings over {a,b,c}, so |U| = 3⁴ = 81. For each letter ℓ ∈ {a,b,c}, let E_ℓ ⊆ U be the set of strings in which letter ℓ does not appear. A string in E_ℓ uses only the remaining 2 letters, so |E_a| = |E_b| = |E_c| = 2⁴ = 16 (×3). A string in the pairwise intersection E_{ℓ₁} ∩ E_{ℓ₂} (for ℓ₁ ≠ ℓ₂) uses only the single remaining letter, so |E_a ∩ E_b| = |E_a ∩ E_c| = |E_b ∩ E_c| = 1⁴ = 1 (×3). A string in the triple intersection E_a ∩ E_b ∩ E_c has 0 available letters, so |E_a ∩ E_b ∩ E_c| = 0⁴ = 0. By inclusion–exclusion (P3), the number of strings avoiding none of the sets E_ℓ is |U ∖ (E_a ∪ E_b ∪ E_c)| = 81 − C(3,1)·16 + C(3,2)·1 − C(3,3)·0 = 81 − 48 + 3 − 0 = **36**. (Note the overlap repair — plain subtraction would give nonsense, 81 − 48 = 33, because the 3 monochromatic strings aaaa, bbbb, cccc each miss two letters and were subtracted twice, exactly as in Lecture 1.1; as a second-engine check, any length-4 string containing all three letters has one letter twice and the other two once each, giving 3·C(4,2)·2! = 3·6·2 = 36 ✓.)

**A6.** Make the identical letters distinguishable, then divide the collapse away (P1). BANANA has six letters — one B, three A's, two N's — so the labeled word B A₁ N₁ A₂ N₂ A₃ has 6! = 720 labelings. Each printed arrangement comes from exactly 3! · 2! = 12 of them (relabel the A's, relabel the N's), so the count is 720/12 = **60**. MISSISSIPPI: 11!/(4!·4!·2!) = 39,916,800/1,152 = **34,650**. Second engine, as a check: choose the 4 positions holding S (C(11,4) = 330), then the 4 positions holding I among the rest (C(7,4) = 35), then the 2 positions holding P (C(3,2) = 3), and the M's fill what remains: 330·35·3 = 34,650 ✓. Two engines agreeing is Lecture 3's habit wearing a different coat. The general law: a word of n letters with multiplicities n₁,…,n_r (where n₁ + … + n_r = n) has n!/(n₁!·…·n_r!) distinct arrangements, because the forget-the-subscripts map from the n! permutations of the subscripted letters to printed words is surjective, and the fiber over every printed word has size n₁!·…·n_r! (generated by independently permuting the n_i subscripts of the i-th letter type for each i = 1, …, r).

**A7.** For every integer n ≥ 0, choose n people from two disjoint rooms R₁, R₂ holding n people each (|R₁| = |R₂| = n, |R₁ ⊔ R₂| = 2n). Directly: the family 𝒮 of n-person selections from R₁ ⊔ R₂ has size C(2n,n). By composition (k from room 1, n−k from room 2): 𝒮 partitions into the n+1 disjoint blocks 𝒮_k = {S ∈ 𝒮 : |S ∩ R₁| = k, |S ∩ R₂| = n−k} for 0 ≤ k ≤ n of size |𝒮_k| = C(n,k)·C(n,n−k), giving Σ_{k=0}^{n} C(n,k)·C(n,n−k) = Σ_{k=0}^{n} C(n,k)², since the complement map B ↦ R₂ ∖ B is a bijection from the (n−k)-person subsets of R₂ onto the k-person subsets of R₂ — choosing n−k people to include from room 2 is in bijection with choosing the k people to leave behind, so C(n,n−k) = n!/((n−k)!·k!) = C(n,k) (equivalently, specialize Vandermonde's identity C(m+n,r) = Σ_{k=0}^{r} C(m,k)·C(n,r−k) at m = n and r = n; check n = 3: 1² + 3² + 3² + 1² = 1 + 9 + 9 + 1 = 20 = C(6,3) ✓). Equate: |𝒮| = Σ_{k=0}^{n} |𝒮_k| yields C(2n,n) = Σ_{k=0}^{n} C(n,k)². ∎ *(Third costume: lattice paths from (0,0) to (n,n), sorted by where they cross the antidiagonal x + y = n — every path of 2n steps reaches x + y = n at step n at a unique point (k, n−k) for some k ∈ {0, …, n}; there are C(n,k) paths from (0,0) to (k, n−k) and C(n,n−k) = C(n,k) paths from (k, n−k) to (n,n), giving C(n,k)² paths through (k, n−k) and Σ_{k=0}^{n} C(n,k)² = C(2n,n) in total.)*

**A8.** From D(x) = e^{−x}/(1−x), multiply both sides by (1−x): **(1−x)·D(x) = e^{−x}**. Now match the coefficients of the *plain power* xⁿ for any integer n ≥ 1 — and mind the bookkeeping, because with plain powers the factorial machinery stays visible. Left side: D(x) contributes D_n/n! (its xⁿ term), and x·D(x) contributes its own xⁿ term, which is the xⁿ⁻¹ term of D(x) shifted up one place: D_{n−1}/(n−1)! — the same number as n·D_{n−1}/n!. Right side: e^{−x} contributes (−1)ⁿ/n!. So **D_n/n! − D_{n−1}/(n−1)! = (−1)ⁿ/n!**, and multiplying through by n!: **D_n − n·D_{n−1} = (−1)ⁿ** for all n ≥ 1. ∎ Check: D₅ = 44 = 5·9 − 1 ✓. (Second engine, directly from Lecture 1.2's recurrence D_n = (n−1)(D_{n−1} + D_{n−2}) for n ≥ 2: rearranging gives D_n − n·D_{n−1} = −(D_{n−1} − (n−1)·D_{n−2}), so the difference d_n = D_n − n·D_{n−1} simply flips sign at every step; since d₁ = D₁ − 1·D₀ = 0 − 1 = −1 = (−1)¹, induction gives d_n = (−1)^{n−1}·d₁ = (−1)ⁿ for every n ≥ 1. You can instead stay in the normalized EGF basis the whole way: there x·D(x) = Σ_{n=1}^{∞} n·D_{n−1}·xⁿ/n! — the one-power shift costs exactly a factor n — and matching the coefficients of xⁿ/n! on both sides for n ≥ 1 gives D_n − n·D_{n−1} = (−1)ⁿ directly, with no final multiplication. Both bookkeepings are honest and equivalent; the one error to avoid is writing one convention's numbers under the other convention's label.)

**A9.** D_n/n! = Σ_{k=0}^n (−1)^k/k!, so the difference is exactly **minus** the discarded tail: D_n/n! − 1/e = −Σ_{k=n+1}^∞ (−1)^k/k!. Multiplying by n! and setting R_n = (−1)^{n+1}(n!/e − D_n) = (−1)^{n+1}·Σ_{k=n+1}^{∞} (−1)^k·n!/k! = Σ_{j=1}^{∞} (−1)^{j−1}·n!/(n+j)! (whose terms a_j = n!/(n+j)! satisfy a₁ > a₂ > a₃ > ⋯ > 0) gives both consecutive-term groupings:

R_n = (1/(n+1) − 1/((n+1)(n+2))) + (1/((n+1)(n+2)(n+3)) − 1/((n+1)(n+2)(n+3)(n+4))) + ⋯ > 0,

R_n = 1/(n+1) − (1/((n+1)(n+2)) − 1/((n+1)(n+2)(n+3))) − ⋯ < 1/(n+1).

Because each grouped pair in parentheses is strictly positive, 0 < R_n < 1/(n+1) (so the alternating series tail n!/e − D_n = (−1)^{n+1}·R_n has sign (−1)^{n+1} and is strictly smaller in magnitude than its first omitted term): |D_n − n!/e| = n!·|tail| = R_n < n!/(n+1)! = 1/(n+1) ≤ 1/2 for every integer n ≥ 1. Since the distance from n!/e to the integer D_n is strictly less than 1/2, any other integer m ≠ D_n satisfies |m − n!/e| ≥ |m − D_n| − |D_n − n!/e| > 1 − 1/2 = 1/2, so an integer within 1/2 of n!/e is unique, and D_n is it — the nearest-integer property *never* fails. ∎ (Check: D₄ = 9, 4!/e ≈ 8.83 ✓.)

**A10.** Let ℱ be the set of permutations of {1, …, n} with exactly one fixed point, and for each i ∈ {1, …, n}, let ℱ_i ⊆ ℱ be the subset in which i is the unique fixed letter (π(i) = i and π(j) ≠ j for all j ≠ i). Since a permutation in ℱ fixes a unique element, ℱ = ⨆_{i=1}^{n} ℱ_i is a disjoint union of n sets. Choosing which letter i is fixed gives n choices, and restricting π ∈ ℱ_i to {1, …, n} ∖ {i} is a bijection onto the derangements of the remaining n−1 letters, of which there are D_{n−1}. Total **n·D_{n−1}** for all n ≥ 1. Check n=1: 1·D₀ = 1 (the identity permutation on {1} fixes 1 letter ✓); n=2: 2·D₁ = 0 (fixing one letter forces the second letter home too ✓); n=3: 3·D₂ = 3 = the three transpositions ✓; n=4: 4·D₃ = 8 (the eight 3-cycles ✓).

**A11.** Fix the geometry first — this is where it is easy to slip. With p ≥ q ≥ 0, the endpoint (p,q) is *on or below* the diagonal, so the right weak version is: paths (0,0)→(p,q) staying **weakly below** (y ≤ x). For q ≥ 1, bad paths first touch y = x+1 — Lecture 2.1's own forbidden line. Swap the head up to that first touch: a prefix with t East-steps and t+1 North-steps (for some 0 ≤ t ≤ q−1) becomes t+1 E's and t N's, re-aiming the whole path from (p,q) at **(p+1, q−1)**. Every path to (p+1, q−1) inverts this — its x − y climbs from 0 to (p+1) − (q−1) = p − q + 2 ≥ 2 in steps of ±1, so it first touches x = y+1, and swapping its head returns the bad path — a genuine two-way bijection, the bad side counted by C(p+q, q−1). Expanding the factorials, the weak count for p ≥ q ≥ 1 is

C(p+q, q) − C(p+q, q−1) = (p+q)!/(p!·q!) − (p+q)!/((p+1)!·(q−1)!) = (p+q)!/(p!·q!)·(1 − q/(p+1)) = **(p−q+1)/(p+1) · C(p+q, q)**.

(At q = 0 and any p ≥ 0, there are no North steps and thus C(p, q−1) = 0 bad paths, so the unique path of p East steps stays weakly below y = x and the weak count is 1 = (p−0+1)/(p+1)·C(p, 0); thus the weak formula holds for all integers p ≥ q ≥ 0.) *Now the strict version:* for a > b ≥ 0, A is strictly ahead after every ballot ⇔ the first step is East (from (0,0) to (1,0)), and after deleting it the translated path (0,0)→(a−1, b) stays weakly below y = x (since x − y ≥ 1 on the original path after step 1 is equivalent to x′ − y′ = (x−1) − y ≥ 0 on the shifted path). Since a > b implies p = a − 1 ≥ b = q ≥ 0, we may apply the weak formula with p = a−1, q = b:

((a−1)−b+1)/((a−1)+1)·C(a+b−1, b) = (a−b)/a·C(a+b−1, b) = (a−b)/a · a/(a+b)·C(a+b, b) = **(a−b)/(a+b) · C(a+b, b)**. ∎

Check a=2, b=1: 1/3·3 = 1 — and indeed AAB is the only ordering with A strictly ahead after every ballot (after 1: 1–0 ✓; after 2: 2–0 ✓; after 3: 2–1 ✓), while ABA ties at ballot 2 ✗ and BAA is behind at ballot 1 ✗. (Edge cases: at b = 0 the strict formula reads (a−0)/(a+0)·C(a, 0) = 1 — the all-A ordering, correct; and at q = 0 the weak count is 1 — the single all-East path — exactly as the weak formula says: (p−0+1)/(p+1)·C(p, 0) = 1.)

**A12.** Total delegations: C(14,5) = 2,002. Let E_c be the delegations containing couple c (both spouses), for c ∈ {1, …, 7}. Zigzag (P3): |E_c| = C(12,3) = 220 (the couple is in, choose the other 3 from the remaining 12 people); any two couples fit together, so |E_c ∩ E_{c′}| = C(10,1) = 10 (4 people fixed, choose the fifth from the remaining 10); and *three* or more couples need 2k ≥ 6 people, which a 5-person delegation cannot hold, so ∩_{c ∈ J} E_c = ∅ and C(7,k)·C(14−2k, 5−2k) = 0 for all 3 ≤ k ≤ 7 — the zigzag honestly stops at k = 2, which is exactly the point the hint nudges you to notice. So the answer is Σ_{k=0}^{2} (−1)^k·C(7,k)·C(14−2k, 5−2k) = 2,002 − C(7,1)·220 + C(7,2)·10 = 2,002 − 1,540 + 210 = **672**. Machine check: enumerating all 2,002 five-person subsets, exactly 672 contain no married couple ✓ — the transplant of Lecture 1 is sound, and the early-stopping observation is what made the zigzag finite *and* obviously finite.

**A13.** Bijection (P1): for any integer n ≥ 1, write n as a row of n unit tokens with n − 1 gaps between them. Every composition n = a₁ + a₂ + ⋯ + a_r (a_i ≥ 1) is determined by the set of partial sums {a₁, a₁ + a₂, …, a₁ + ⋯ + a_{r−1}} ⊆ {1, …, n−1}, which specifies *which of the n−1 gaps to cut* — cut gaps split the row into r contiguous blocks, the block lengths a_i are the summands, and cutting no gaps (∅) gives the one-summand composition n itself. Conversely, any subset S = {s₁ < s₂ < ⋯ < s_{r−1}} ⊆ {1, …, n−1} recovers a unique composition a₁ = s₁, a₂ = s₂ − s₁, …, a_r = n − s_{r−1} of positive integers summing to n. There are 2^{n−1} subsets of gaps, so c_n = **2^{n−1}** for every integer n ≥ 1 (with the empty convention c₀ = 1). Recurrence (P4): for n ≥ 1, condition on the first summand m (1 ≤ m ≤ n); what follows is a composition of n − m, so c_n = Σ_{m=1}^{n} c_{n−m} with c₀ = 1. For n ≥ 2, the same equation read at n − 1 says c_{n−1} = Σ_{i=0}^{n−2} c_i, so c_n = c_{n−1} + Σ_{i=0}^{n−2} c_i = 2·c_{n−1} — and c₁ = c₀ = 1 gives c_n = 2^{n−1} for all n ≥ 1 by induction. Machine check: n = 1, …, 12 gives 1, 2, 4, 8, 16, 32, 64, 128, 256, 512, 1024, 2048, no exceptions ✓. The honest boundary: *order matters here* — 3+1 and 1+3 are different compositions. If you decide order *doesn't* matter (partitions), the count collapses (4 has 5 partitions, not 8) and no gap-bijection exists; that harder world is a different book's chapter.

**A14.** Count the pairs (S, T) with T ⊆ S ⊆ {1,…,n} and |T| = m. Way 1: pick the committee S first — if |S| = k, there are C(n,k) choices — then the subcommittee T ⊆ S: C(k,m) choices (which is 0 for k < m). Total: Σ_{k=m}^{n} C(n,k)·C(k,m). Way 2: pick the subcommittee T first (C(n,m) choices), then let the committee grow around it: since T ⊆ S ⊆ {1,…,n} if and only if S = T ⊔ U for a unique subset U = S ∖ T ⊆ {1,…,n} ∖ T, every subset of the n − m outsiders may join S, giving 2^{n−m} choices. Total: C(n,m)·2^{n−m}. (Algebraic check: for 0 ≤ m ≤ k ≤ n, C(n,k)·C(k,m) = n!/(k!·(n−k)!) · k!/(m!·(k−m)!) = n!/(m!·(n−m)!) · (n−m)!/((k−m)!·(n−k)!) = C(n,m)·C(n−m, k−m), and summing over j = k − m ∈ {0, …, n−m} gives C(n,m)·Σ_{j=0}^{n−m} C(n−m, j) = C(n,m)·2^{n−m}.) One set of pairs, two books (P2): **Σ_k C(n,k)·C(k,m) = C(n,m)·2^{n−m}**. ∎ Machine check: all n ≤ 12, all m — e.g. n = 8, m = 3 gives 1,792 both ways ✓. Notice the formula box's identities are the bottom rungs: m = 0 recovers Σ C(n,k) = 2^n, and m = 1 recovers Σ k·C(n,k) = n·2^{n−1}. The pattern generalizes: when an identity feels isolated, ask what two-order count produced it.

**A15.** Because y_j − x_j changes by ±1 at each step, a path cannot pass from y − x > 0 to y − x < 0 without hitting y − x = 0 at an intermediate vertex. Thus a path from (0,0) to (n,n) that touches the diagonal y = x only at its endpoints (0,0) and (n,n) must satisfy either y_j − x_j ≥ 1 for all 1 ≤ j ≤ 2n−1 (strictly above) or x_j − y_j ≥ 1 for all 1 ≤ j ≤ 2n−1 (strictly below). For n = 1, the single vertex in between is (0,1) (above, path NE) or (1,0) (below, path EN), giving 2 = 2·C₀ paths. For n ≥ 2, take the above side: since (x₁, y₁) has x₁ + y₁ = 1 and y₁ − x₁ ≥ 1, the first step must be N to (0,1); similarly, since (x_{2n−1}, y_{2n−1}) has x_{2n−1} + y_{2n−1} = 2n−1, y_{2n−1} − x_{2n−1} ≥ 1, and y_{2n−1} ≤ n, we must have (x_{2n−1}, y_{2n−1}) = (n−1, n), so the last step must be E. Strip the forced pair: N [inner] E, where the inner path, translated down by (0,−1), runs (0,0)→(n−1, n−1) with vertices (x′_r, y′_r) = (x_{r+1}, y_{r+1}−1) satisfying y′_r − x′_r = (y_{r+1} − x_{r+1}) − 1 ≥ 0 for all 0 ≤ r ≤ 2n−2, staying weakly above y = x (which, under the diagonal reflection (x′, y′) ↦ (y′, x′) swapping E ↔ N, is in bijection with paths from (0,0) to (n−1, n−1) staying weakly below y = x) — count C_{n−1} by A11's weak formula (or Lecture 2.1: p = q = n−1 gives (1/n)·C(2n−2, n−1) = C_{n−1}). Reflecting across y = x (swapping E ↔ N) gives a bijection onto the strictly-below paths E [inner] N, contributing another C_{n−1}. Total **2·C_{n−1}** for all n ≥ 1. ∎ Check n=2: 2·C₁ = 2 ✓ (NNEE, EENN); n=3: 2·C₂ = 4 ✓ (NNNEEE, NNENEE, EENENN, EEENNN).

**A16.** For n ≥ 2, differentiating (1+x)^n = Σ_{k=0}^{n} C(n,k)·x^k twice with respect to x gives n(n−1)(1+x)^{n−2} = Σ_{k=2}^{n} k(k−1)·C(n,k)·x^{k−2}, and evaluating at x=1 yields Σ_{k=0}^{n} k(k−1)·C(n,k) = n(n−1)·2^{n−2} (which also holds at n = 1, where both sides equal 0 = 1(0)·2⁻¹); adding Lecture 3.2's Σ_{k=0}^{n} k·C(n,k) = n·2^{n−1} = 2n·2^{n−2} gives

Σ_{k=0}^{n} k²·C(n,k) = Σ_{k=0}^{n} (k(k−1) + k)·C(n,k) = n(n−1)·2^{n−2} + 2n·2^{n−2} = n(n+1)·2^{n−2}.

Expanding (k − n/2)² = k² − nk + n²/4 and summing over 0 ≤ k ≤ n for every n ≥ 1 then gives

Σ_{k=0}^{n} (k − n/2)²·C(n,k) = n(n+1)·2^{n−2} − n·(n·2^{n−1}) + (n²/4)·2^n = 2^{n−2}·(n² + n − 2n² + n²) = **n·2^{n−2}**. ∎

Sanity: n=1: ¼·1 + ¼·1 = ½ = 1·2⁻¹ ✓; n=2: 1·1 + 0·2 + 1·1 = 2 = 2·2⁰ ✓; n=3: (9/4)(1) + (1/4)(3) + (1/4)(3) + (9/4)(1) = 6 = 3·2¹ ✓.

**A17.** Let person 1 shake hands with person j ∈ {2, …, 2n}. By the Jordan curve theorem on the circle, the straight chord 1–j divides the circle into two open arcs holding the clockwise sets L_j = {2, …, j−1} of size j−2 and R_j = {j+1, …, 2n} of size 2n−j, and any chord between a person in L_j and a person in R_j must intersect the chord 1–j. Therefore, a pairing containing 1–j is non-crossing if and only if L_j and R_j are paired internally without crossings; for such pairings to exist, **both arc sizes j−2 and 2n−j must be even — so j must be even**, j = 2i+2 (i = 0, …, n−1). Drawn for 8 people, with person 1 shaking person 4:

```
              8           1
            ·             ┃
          ·               ┃
        7                 ┃     2
        |                 ┃     |
        6                 ┃     3
          ·               ┃
            ·             ┃
              5           4
```

Clockwise from 1 to 4 the arc holds {2, 3} — 2 people, who must pair among themselves; clockwise from 4 back to 1 it holds {5, 6, 7, 8} — 4 people, pairing internally without crossing. And why must j be even? Try the chord 1–5 instead: the arcs become {2, 3, 4} and {6, 7, 8} — both *odd*, so someone would be forced to cross the chord.

The same table, drawn to scale as **Figure 3** — a true circle, the chord 1–4, and both arcs colour-coded with their counts and pairing counts:

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 925 880 372" font-family="system-ui, -apple-system, 'Segoe UI', sans-serif">
  <rect x="0" y="925" width="880" height="372" fill="#ffffff"/>
  <!-- ================= FIGURE 3 · The chord-split ================= -->
  <text x="40" y="950" font-size="17" font-weight="700" fill="#193e5c">Figure 3 &#183; The chord-split &#8212; handshakes around the table (exercise 17)</text>

  <circle cx="200" cy="1130" r="130" fill="none" stroke="#cbd5e1" stroke-width="1.5"/>
  <!-- arcs -->
  <path d="M 200,1000 A 130,130 0 0 1 292,1222" fill="none" stroke="#d97706" stroke-width="5"/>
  <path d="M 292,1222 A 130,130 0 1 1 200,1000" fill="none" stroke="#2563eb" stroke-width="5"/>
  <!-- chord 1-4 -->
  <line x1="200" y1="1000" x2="292" y2="1222" stroke="#dc2626" stroke-width="4"/>
  <text x="228" y="1120" font-size="11.5" fill="#dc2626" text-anchor="end">chord 1&#8211;4</text>
  <!-- people -->
  <g>
    <circle cx="200" cy="1000" r="7" fill="#ffffff" stroke="#172333" stroke-width="2"/><text x="200" y="982" font-size="13" font-weight="700" fill="#172333" text-anchor="middle">1</text>
    <circle cx="292" cy="1038" r="7" fill="#ffffff" stroke="#172333" stroke-width="2"/><text x="312" y="1034" font-size="13" font-weight="700" fill="#172333">2</text>
    <circle cx="330" cy="1130" r="7" fill="#ffffff" stroke="#172333" stroke-width="2"/><text x="348" y="1134" font-size="13" font-weight="700" fill="#172333">3</text>
    <circle cx="292" cy="1222" r="7" fill="#ffffff" stroke="#172333" stroke-width="2"/><text x="312" y="1240" font-size="13" font-weight="700" fill="#172333">4</text>
    <circle cx="200" cy="1260" r="7" fill="#ffffff" stroke="#172333" stroke-width="2"/><text x="200" y="1284" font-size="13" font-weight="700" fill="#172333" text-anchor="middle">5</text>
    <circle cx="108" cy="1222" r="7" fill="#ffffff" stroke="#172333" stroke-width="2"/><text x="88" y="1240" font-size="13" font-weight="700" fill="#172333" text-anchor="end">6</text>
    <circle cx="70" cy="1130" r="7" fill="#ffffff" stroke="#172333" stroke-width="2"/><text x="52" y="1134" font-size="13" font-weight="700" fill="#172333" text-anchor="end">7</text>
    <circle cx="108" cy="1038" r="7" fill="#ffffff" stroke="#172333" stroke-width="2"/><text x="88" y="1034" font-size="13" font-weight="700" fill="#172333" text-anchor="end">8</text>
  </g>
  <!-- annotations -->
  <g font-size="12.5" fill="#172333">
    <line x1="405" y1="1006" x2="435" y2="1006" stroke="#d97706" stroke-width="5"/>
    <text x="445" y="1010">arc {2, 3} &#8212; clockwise from 1 to 4</text>
    <text x="445" y="1032" fill="#64748b">2 people: they must pair among themselves &#8594; C&#8321; = 1 way</text>
    <line x1="405" y1="1066" x2="435" y2="1066" stroke="#2563eb" stroke-width="5"/>
    <text x="445" y="1070">arc {5, 6, 7, 8} &#8212; clockwise from 4 to 1</text>
    <text x="445" y="1092" fill="#64748b">4 people: pairing internally, no crossings &#8594; C&#8322; = 2 ways</text>
    <line x1="405" y1="1126" x2="435" y2="1126" stroke="#dc2626" stroke-width="5"/>
    <text x="445" y="1130">the chord 1&#8211;4 contributes a&#8321; &#183; a&#8322; = 1 &#215; 2 pairings</text>
    <text x="445" y="1170" fill="#64748b">j must be even: a chord 1&#8211;5 would strand the arcs</text>
    <text x="445" y="1190" fill="#64748b">{2, 3, 4} and {6, 7, 8} &#8212; both odd, forcing a crossing.</text>
  </g>
</svg>
```

The arcs then hold 2i and 2n−j = 2(n−1−i) people, pairable internally in a_i and a_{n−1−i} ways (since the straight line through 1 and j divides the plane into two disjoint open half-planes containing the open circular arcs L_j = {2, …, j−1} and R_j = {j+1, …, 2n} respectively, and open half-planes are convex, the convex hulls of L_j and R_j are disjoint, so no chord with both endpoints in L_j can intersect a chord with both endpoints in R_j; and because two disjoint chords {u₁, v₁} and {u₂, v₂} written with u₁ < v₁ and u₂ < v₂ in clockwise order along an arc cross if and only if u₁ < u₂ < v₁ < v₂ or u₂ < u₁ < v₂ < v₁, relabeling L_j as {1, …, 2i} and R_j as {1, …, 2(n−1−i)} in strictly increasing clockwise order preserves the crossing relation and gives a bijection with non-crossing pairings on 2i and 2(n−1−i) people around a smaller table). Summing over i ∈ {0, …, n−1} gives a_n = Σ_{i=0}^{n−1} a_i·a_{n−1−i} for n ≥ 1 with a₀ = 1 (and a₁ = a₀² = 1) — exactly the Catalan recurrence of Lecture 2.2, in the same "cut at the first return" costume. By induction on n, **a_n = C_n.** ∎ (Check 4 people: person 1 must pair with j = 2 or j = 4 — an odd j = 3 would strand one person on each side of the chord — giving (1,2)(3,4) and (1,4)(2,3): C₂ = 2 ✓.)

**A18.** Label the (n+2)-gon's vertices 0,…,n+1 in clockwise order and distinguish the base edge (0, n+1). In any triangulation T, the base edge (0, n+1) belongs to a unique triangle (0, k, n+1) whose third vertex is some k ∈ {1, …, n}; its edges (0,k) and (k, n+1) (which are diagonals or boundary edges of the polygon) split the (n+2)-gon into a left (k+1)-gon P_L on vertices (0, 1, …, k) with distinguished base edge (0,k) and a right (n−k+2)-gon P_R on vertices (k, k+1, …, n+1) with distinguished base edge (k, n+1) (where a 2-gon for k = 1 or k = n is a single boundary edge with the empty triangulation; because the chords (0,k) and (k, n+1) connect k to 0 and n+1 across the convex (n+2)-gon, any diagonal linking an interior vertex of P_L in {1, …, k−1} to an interior vertex of P_R in {k+1, …, n} would cross (0,k) or (k, n+1) in its interior, so every remaining diagonal of T lies either wholly in P_L or wholly in P_R, decomposing T uniquely into a pair of triangulations (T_L, T_R) of P_L and P_R). Map Φ_n: define Φ₀(∅) = ε (the empty string), and for n ≥ 1, map the triangulation T with apex k to

**Φ_n(T) = ( Φ_{k−1}(T_L) ) Φ_{n−k}(T_R),**

where T_L and T_R are the induced triangulations of P_L and P_R: the triangle (0, k, n+1) ↔ the first-return wrapping pair **( … )**, the left polygon ↔ what is inside the pair, the right polygon ↔ what follows it. To prove Φ_n is a bijection with explicit inverse Ψ_n by induction on n ≥ 0: for n = 0, Ψ₀(ε) = ∅. For n ≥ 1, any balanced parenthesis string w of length 2n has a unique first-return decomposition w = ( u ) v where u is a balanced string of length 2(k−1) for a unique k ∈ {1, …, n} and v is a balanced string of length 2(n−k) (Lecture 2.2 and A4). Define Ψ_n(w) by placing the triangle (0, k, n+1) on the base edge (0, n+1), triangulating the left (k+1)-gon on (0, …, k) via Ψ_{k−1}(u), and triangulating the right (n−k+2)-gon on (k, …, n+1) via Ψ_{n−k}(v) (relabelling vertices 0, …, n+1−k by +k). Because the apex k of the triangle (0, k, n+1) in Ψ_n(w) is 1 + |u|/2 and the first-return cut of Φ_n(T) occurs after 2k characters, induction gives Ψ_n(Φ_n(T)) = T and Φ_n(Ψ_n(w)) = w. Both sides satisfy the same recurrence (Σ_{k=1}^{n} C_{k−1}C_{n−k} = C_n). Pentagon (n = 3, vertices 0,1,2,3,4 with base edge (0,4)): all 5 triangulations = C₃ ✓, listed explicitly by apex k ∈ {1, 2, 3} and internal diagonals:

- k = 1, diagonals {(1,4), (2,4)} (T_L = ∅, T_R on (1,2,3,4) has apex 2, then (2,3,4) has apex 3): Φ₃(T) = ()()().
- k = 1, diagonals {(1,4), (1,3)} (T_L = ∅, T_R on (1,2,3,4) has apex 3, with left triangle (1,2,3)): Φ₃(T) = ()(()).
- k = 2, diagonals {(0,2), (2,4)} (T_L is triangle (0,1,2), T_R is triangle (2,3,4)): Φ₃(T) = (())().
- k = 3, diagonals {(0,3), (1,3)} (T_R = ∅, T_L on (0,1,2,3) has apex 1, then (1,2,3) has apex 2): Φ₃(T) = (()()).
- k = 3, diagonals {(0,3), (0,2)} (T_R = ∅, T_L on (0,1,2,3) has apex 2, with left triangle (0,1,2)): Φ₃(T) = ((())).

**A19.** Let U be the set of all k^n functions f : [n] → [k]. The bad events are misses: for each i ∈ {1, …, k}, let E_i = {f ∈ U : i ∉ im(f)} be the set of functions where value i is never hit. For any subset J ⊆ {1, …, k} of size j, a function belongs to ∩_{i∈J} E_i if and only if im(f) ⊆ {1, …, k} ∖ J, so each of the n domain elements has k − j possible target values, giving |∩_{i∈J} E_i| = (k−j)^n possibilities (with 0^n = 0 at j = k since n ≥ 1). Any function f whose image misses exactly m values of {1, …, k} is counted C(m,j) times at level j, contributing net weight Σ_{j=0}^{m} (−1)^j C(m,j) = (1−1)^m = 0 if m ≥ 1 and 1 if m = 0 (onto). So the zigzag (P3) over which values are missed gives the onto count: **Σ_{j=0}^{k} (−1)^j · C(k,j) · (k−j)^n**. For a 6-element set onto a 3-element set: 3⁶ − C(3,1)·2⁶ + C(3,2)·1⁶ = 729 − 192 + 3 = **540**. Machine check: of all 729 functions, exactly 540 hit every value ✓. Second engine, as a calibration: an onto function f : [n] → [k] is uniquely determined by partitioning the domain [n] into k nonempty unordered blocks {f⁻¹(1), …, f⁻¹(k)} (counted by the Stirling number of the second kind, S(n,k)) and then assigning those k distinct blocks bijectively to the k target values in [k] (k! ways). For n = 6, k = 3, the nonempty block sizes must sum to 6 according to one of three integer partitions: 4+1+1 (giving ½·C(6,4)·C(2,1)·C(1,1) = 15 set partitions), 3+2+1 (giving C(6,3)·C(3,2)·C(1,1) = 60 set partitions), or 2+2+2 (giving 1/3!·C(6,2)·C(4,2)·C(2,2) = 15 set partitions), so S(6,3) = 15 + 60 + 15 = 90 and k!·S(n,k) = 6·90 = 540 ✓. Sanity rungs: onto [5]→[5] gives 5⁵ − C(5,1)·4⁵ + C(5,2)·3⁵ − C(5,3)·2⁵ + C(5,4)·1⁵ − 0 = 3125 − 5120 + 2430 − 320 + 5 = 120 = 5! (when n = k ≥ 1, a function f : [n] → [n] has |im(f)| = n if and only if f is a bijection — the n! permutations of Lecture 1), onto [n]→[1] gives C(1,0)·1^n − C(1,1)·0^n = 1, and when 1 ≤ n < k every function f : [n] → [k] has |im(f)| ≤ n < k so the set of onto functions is empty by the pigeonhole principle and the inclusion–exclusion formula evaluates to 0 (e.g. for n = 2, k = 3: 3² − 3·2² + 3·1² − 0 = 9 − 12 + 3 = 0 ✓). The derangement lesson transplanted: D_n comes from the same inclusion–exclusion, with the bad events "letter i lands home" — any j of them together leave (n−j)! arrangements, where the misses above leave (k−j)^n functions — and the rencontres numbers of X1 sit one step further along the same road.

**A20.** The graded exercises above hand you the pattern; here you must *find* it. So do what a researcher does: compute small cases. n = 0: 1 (the empty set). n = 1: 2. n = 2: 3 (∅, {1}, {2}). n = 3: 5. n = 4: 8. That sequence — 1, 2, 3, 5, 8 — is Fibonacci wearing a disguise, and now it must be *explained*, not just recognized. Let 𝒮_n be the family of subsets of {1,…,n} with no two consecutive integers, and let a_n = |𝒮_n|. For n ≥ 2, partition 𝒮_n = 𝒮_n^{(0)} ⊔ 𝒮_n^{(1)} according to whether n ∉ S or n ∈ S. A subset S ∈ 𝒮_n^{(0)} avoids n and is simply a valid subset of {1, …, n−1} — a_{n−1} choices. A subset S ∈ 𝒮_n^{(1)} contains n, and then it cannot contain n−1, so the map S ↦ S ∖ {n} is a bijection from 𝒮_n^{(1)} onto 𝒮_{n−2} (with inverse T ↦ T ∪ {n}, since T ⊆ {1, …, n−2} ensures every element of T is at most n−2 and thus not consecutive with n): a_{n−2} choices. So **a_n = a_{n−1} + a_{n−2}** for all n ≥ 2 with a₀ = 1, a₁ = 2 — the Fibonacci recurrence with shifted seeds; since a₀ = 1 = F₂ and a₁ = 2 = F₃, induction gives **a_n = F_{n+2}** for all n ≥ 0 (counting F₁ = F₂ = 1). ∎ Check n = 3 by listing: ∅, {1}, {2}, {3}, {1,3} — 5 ✓. (The tool was P4, the recurrence — but the *diagnosis* was the exercise: experiment first, then the forced case analysis on element n.)

**A21.** The move is a **bijection** (P1), and it is one line: for n ≥ 1, pair every subset S ⊆ {1, …, n} with the set τ(S) = S △ {1} obtained by toggling the membership of the element 1 (τ(S) = S ∖ {1} if 1 ∈ S, and τ(S) = S ∪ {1} if 1 ∉ S). Because ||τ(S)| − |S|| = 1, toggling one element flips the parity of the size, so τ maps the family ℰ_n of even-sized subsets into the family 𝒪_n of odd-sized subsets and vice versa; applying τ twice returns τ(τ(S)) = (S △ {1}) △ {1} = S, so τ is its own inverse (an involution with no fixed points) — and neither side can outnumber the other. Since |ℰ_n| + |𝒪_n| = 2^n and |ℰ_n| = |𝒪_n|, both counts are **2ⁿ⁻¹** for every n ≥ 1. ∎ Check n = 2: even ∅, {1,2}; odd {1}, {2} ✓ — and watch the pairing do the work: ∅ ↔ {1} and {2} ↔ {1,2}. (Second costume: Σ_k (−1)^k C(n,k) = (1−1)ⁿ = 0 for n ≥ 1 — Lecture 1.1's zigzag collapsing to zero precisely because every even-sized subset (a +1 in the sum) has an odd-sized partner (a −1). One engine is a map; the other is a sum; the truth is the same.)

**A22.** No chapter formula covers this — which is the point. Experiment first: one line cuts the plane into 2 regions; two into 4; three into 7; four into 11. The *differences* are 2, 3, 4 — each new line adds one more region than the last one did. Now explain the pattern, because a conjecture without a reason is a rumor. Suppose n − 1 lines are already in the plane forming R_{n−1} convex regions (n ≥ 1, with R₀ = 1 for the undivided plane). Because the n-th line L_n is not parallel to any of the n − 1 earlier lines, it intersects each of them; and because no three lines pass through a common point, those n − 1 intersection points along L_n are all distinct. Ordering those n − 1 points along L_n slices L_n into (n−1) + 1 = n open pieces (for n = 1, the single undivided line L₁ itself with 0 intersection points; for n ≥ 2, two unbounded rays at the ends and n − 2 bounded open segments between consecutive intersection points). Each existing region formed by L₁, …, L_{n−1} is a non-empty open intersection of half-planes bounded by L₁, …, L_{n−1} (hence convex), and any two distinct open pieces of L_n are separated along L_n by at least one intersection point p = L_n ∩ L_i (1 ≤ i ≤ n−1), placing the two pieces on opposite open sides of L_i so they cannot belong to the same existing region. Each of these n pieces contains no intersection points in its interior, so it lies entirely inside the interior of a single existing convex region and cuts that region into two non-empty open convex subregions (one on each open side of L_n), adding exactly one new region per piece: **R_n = R_{n−1} + n** for all n ≥ 1, with R₀ = 1. Telescoping: **R_n = R₀ + Σ_{k=1}^{n} (R_k − R_{k−1}) = 1 + (1 + 2 + … + n) = 1 + n(n+1)/2** for all n ≥ 0. ∎ Check: n = 2 gives 1 + 3 = 4 ✓ (L₂ meets L₁ at 1 point, splitting L₂ into 2 open rays on opposite sides of L₁ that bisect the 2 half-planes into 4 quadrants), n = 4 gives 11 ✓, n = 5 gives 16 — draw five lines and count. (The tool was again P4, but its *seed* was the experiment — the discovery cycle, running.)

---
