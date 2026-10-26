---
name: "cgt-ch13-probabilistic-ii"
title: "Ch. 13 — The Probabilistic Method, Act II: Correlation, Concentration, and the Entropy Ledger (A Lecture Course in the Feynman Style)"
type: "text/markdown"
---

# Chapter 13 · The Probabilistic Method, Act II

*Part of the Combinatorics & Graph Theory Atlas (the chapter map lives in the book basis).*

Chapter 4 taught the scandal: to prove an object exists, design a random experiment and show it succeeds with positive probability. This chapter is what the method grew into when the questions got serious. Four upgrades, one per pair of lectures: **correlation** (Lecture 1: events in a product space are not neutral toward each other — increasing events lean together, and the lean can be quantified); **the Poisson paradigm** (Lecture 2: Janson's inequality turns "mostly independent" into a usable bound, and pays a debt Chapter 4 left openly flagged — the exact value of P(no triangle) at the threshold); **concentration** (Lectures 3 and 4: martingales and exposure, Azuma's inequality, and the random graph's full life story from empty to giant); and **counting by entropy** (Lectures 5 and 6: Spencer's six standard deviations, Brégman's permanent bound, and Moser–Tardos's resampler — where the Local Lemma of Chapter 4 §4.3 stops being an existence argument and becomes an algorithm).

The deal with the reader is the one the Atlas has enforced since Chapter 1: every number printed below was machine-verified before printing — censuses, exact optima, seeded Monte-Carlo — and where a bound is vacuous, a statement is beyond the chapter, or a proof is cited rather than given, the text says so. Act I promised existence; Act II delivers structure.

## How to read this chapter

Read with Chapter 4 within reach: its patterns (P10 averaging, P12 random construction, P13 union bound, P14 alteration) all fire again here, now with sharper ammunition. Lines marked **✎ Checkpoint** are the places to stop and predict — commit to a guess, in ink, before reading on. Exercises are graded ●○○ *easy* (one idea, applied directly), ●●○ *moderate* (two ideas, or one tricky step), ●●● *tough* (several ideas combined); ◆ **pattern unknown** problems come with no hint — diagnosing the tool is part of the problem; ◐ **Explorations** are open-ended investigations that state what you should find, not a number to match. Worked answers sit at the end; hints travel with the problems.

Notation. G(n, p) is the random graph on vertex set {0, …, n−1}, each of the C(n,2) possible edges present independently with probability p. For a fixed graph H, m(H) = max e(F)/v(F) over subgraphs F ⊆ H with v(F) ≥ 3 — the *density* that governs H's appearance threshold n^{−1/m(H)}. A *up-set* is a family A of sets with S ∈ A, S ⊆ T ⟹ T ∈ A. χ, α, ω are the chromatic number, independence number, clique number. P(△) is the probability a random graph contains a triangle. Convergence is as n → ∞; "almost surely" (a.a.s.) means with probability tending to 1. e is the base of natural logarithms — it will be doing real work in Lecture 6, where it arrives on the side of the *count* rather than the probability.

The chapter's Monte-Carlo runs on the Atlas's standing rule: a Lehmer generator (x ← 48271·x mod 2³¹−1), seeded and recorded, so every sample is reproducible bit for bit — the same rule Chapter 4's lab Part 2 already enforces.

## The pattern map for this chapter

| Pattern | Plain language | Where it fires in Act II |
|---------|---------------|--------------------------|
| **P10 Averaging / expectation** | The average is a promise; some object beats it | L2 (Janson's μ is Chapter 4's E[X], upgraded), L4 (expected cycle counts c^k/2k), L6 (entropy is averaging on the log scale) |
| **P12 Random construction** | Prove existence by designing an experiment | L2 (the Poisson paradigm's experiments), L5 (random colorings vs. optimal discrepancy), L6 (random assignments, resampled) |
| **P13 Union bound** | If the bad-event probabilities sum below 1, an object avoiding all exists | L1 (its mirror image: FKG *floors* the probability of the good intersection), L2 (Janson repairs it where events overlap), L6 (the Local Lemma's budget e·p·(d+1) ≤ 1, back from Chapter 4 §4.3) |
| **P14 Alteration** | Let the random object be imperfect; delete the damage | L5 (partial coloring: color half the elements, recurse on the remainder) |
| **P18 Algorithmic proof** | The proof *is* a procedure; termination is the theorem | L6 (Moser–Tardos: the resampler's termination *is* the LLL's conclusion) |
| **P27 Correlation (new this chapter)** | Increasing events in a product space are positively correlated — the union bound's pessimism has a floor. Usage-evidence note: fully silent in the survey's corpus — no firing, partial or genuine, in 133 papers; the registry entry (P27) stays open, waiting for its first genuine use | L1 (Harris–Kleitman, FKG, Ahlswede–Daykin), L2 (Janson's conditional lower bound); proposed to the Atlas pattern registry at ship |
| **P28 Concentration (new this chapter)** | A martingale that moves in bounded steps cannot stray far from its mean | L3 (Azuma–Hoeffding, Talagrand), L4 (the evolution's phases are concentration statements); proposed to the registry at ship |
| **P29 Entropy counting (new this chapter)** | Count objects by the information needed to describe them; the chain rule does the bookkeeping | L5 (Spencer's partial coloring), L6 (Brégman, Moser–Tardos's entropy compression); proposed to the registry at ship |

---

## Lecture 1 · Correlation: Knowing One Thing Teaches You Another

Chapter 4's coins were honest but cold: each bad event was charged at face value by the union bound, and when events overlapped too much, the Local Lemma stepped in with a budget (e·p·(d+1) ≤ 1). But something obvious was missing from that whole account. In a random graph, "contains a triangle" and "contains a four-cycle" are both increasing events — more edges can only help them. Intuition says they should lean *together*: a graph generous enough to host a triangle is a graph hosting other things too. The union bound can never say this (it only bounds intersections from above, pessimistically). This lecture builds the tool that says it precisely, in three increasing levels of generality: Harris–Kleitman for the cube, FKG for lattices with non-product measures, and the Ahlswede–Daykin four-functions theorem that contains both.

**The Harris–Kleitman lemma.** Let A and B be up-sets of subsets of [n] = {1, …, n}. Then

**|A ∩ B| · 2ⁿ ≥ |A| · |B|.**

In probability language (a uniformly random subset S of [n]): **P(S ∈ A and S ∈ B) ≥ P(S ∈ A) · P(S ∈ B)** — increasing events are positively correlated. Kleitman's proof (1966) is an induction the Atlas will hand to you as Exercise 1, because the final line is a two-factor product worth doing in ink; the engine is that an up-set's two coordinate slices satisfy A₀ ⊆ A₁ (adding the last element can only help membership), so both slice-differences are nonnegative and their product finishes the induction. ∎ (A forerunner for decreasing families appears in Harris's 1960 percolation work; Kleitman's paper is the sharp combinatorial version.)

**✎ Checkpoint.** Before the machine speaks: in G(5, ½) — every graph on 5 vertices equally likely, 1024 of them — predict the sign of the gap P(△ and C₄) − P(△)·P(C₄). Positive (correlation), zero (independence), or negative? Commit in ink, and also guess the size: a few percent, or a tenth?

The machine's answer, by exhaustive census of all 1024 graphs: P(△) = 636/1024 ≈ 0.621, P(C₄) = 476/1024 ≈ 0.465, P(both) = 391/1024 ≈ 0.3818 — against the product 0.2887. The gap is **+0.0931**: nearly a third of the product, added back by correlation. (And with both events increasing, the lemma predicted the sign before any counting: positive, always.)

The census underneath the lemma itself: all up-set pairs on the 3-cube — 20 up-sets (the Dedekind number D(3) = 20, machine-verified), hence 400 ordered pairs — and all up-set pairs on the 4-cube — 168 up-sets (D(4) = 168), hence 28,224 ordered pairs: **zero violations** of |A∩B|·2ⁿ ≥ |A||B| in either census. Reversed for one-up-one-down pairs (A increasing, B decreasing), the inequality flips, and the census confirmed the flip with zero exceptions there too. Kleitman's lemma is the kind of statement that is true everywhere it applies — and the machine has now checked every place it applies, twice.

**FKG: the lattice upgrade.** The cube {0,1}ⁿ is a special lattice — meet ∧ = intersection, join ∨ = union — with a *product* measure. Fortuin, Kasteleyn and Ginibre (1971) saw that both conditions can be relaxed. **FKG inequality:** let L be a finite distributive lattice and μ a probability measure on it satisfying the **lattice condition**

**μ(x ∧ y) · μ(x ∨ y) ≥ μ(x) · μ(y) for all x, y**

(μ is *log-supermodular*). Then for increasing functions f, g: **E[fg] ≥ E[f] · E[g]** under μ. Increasing events are the 0–1 case, and the conclusion reads P(A ∩ B) ≥ P(A)P(B): positive correlation survives far from product measure. Product measures satisfy the lattice condition with equality (each factor splits across the coordinates where x, y agree); the theorem's value is that other measures do too.

The Atlas's machine-checked example of a genuinely non-product FKG measure is the **rank-flattened measure** on the cube: fix N and 0 < q < 1, and set μ(A) = q^{|A|} / C(N, |A|) — weight ∝ q^{rank}, spread *evenly within a rank*. Log-supermodularity is then a binomial identity in disguise: for sets A, B with |A| = a, |B| = b, |A ∪ B| = u, |A ∩ B| = i (so a + b = u + i), the lattice condition reads

  C(N, a)·C(N, b) ≥ C(N, i)·C(N, u),

which is a classical log-concavity fact about binomial coefficients. The machine verified it directly — all 87,380 ordered pairs of subsets for N = 1 through 8 (every pair, diagonals included), q = 0.37: **zero violations**. An honesty note the Atlas records because it cost a design iteration: the first draft flattened the *other* way, μ(A) = C(N, |A|)·q^{|A|} (weight by the count of same-rank peers) — and that measure is log-*sub*modular, 68,210 violations, the inequality runs the wrong way. Flattening must divide by the rank size, not multiply. The machine caught the error before any prose was written; the chapter keeps the scar as a checkpoint of its own process.

**The four-functions theorem.** The engine room is Ahlswede and Daykin's 1978 theorem, which subsumes Harris–Kleitman, FKG, and Holley's 1974 comparison theorem in one statement. Call it the **AD inequality**: for nonnegative functions α, β, γ, δ on a finite distributive lattice L satisfying

  α(x) · β(y) ≤ γ(x ∧ y) · δ(x ∨ y) for all x, y ∈ L,

it follows that the same inequality holds *after summation*: for all subsets A, B ⊆ L,

  α(A) · β(B) ≤ γ(A ∧ B) · δ(A ∨ B),

where α(A) = Σ_{x∈A} α(x) and A ∧ B = {x ∧ y : x ∈ A, y ∈ B}, A ∨ B likewise. (A pointwise hypothesis upgrades to a statement about sums — that is the whole miracle, and the proof is an induction on the lattice's join-irreducible decomposition once you see the gluing lemma; the Atlas states it and points to the literature.) The chapter's use of AD is as a *theorem factory*: Harris–Kleitman falls out by taking α, β, γ, δ all equal to the product-measure weights; FKG falls out by taking α = μ·f, β = μ·g, γ = δ = μ. The machine ran the factory floor: 3,000 constructed hypothesis-holding quadruples on a 2×3 grid lattice — zero conclusion violations — and FKG's conclusion under the non-product rank-flattened measure on the 4-cube, all 28,224 up-set pairs, zero violations.

**Why a probabilist cares.** The union bound caps P(∪ bad) from above; FKG floors P(∩ good) from below — for increasing good events A₁, …, A_r in a product space, iterating the lemma gives **P(∩Aᵢ) ≥ ∏P(Aᵢ)**. When a proof needs "the random graph simultaneously avoids every one of several decreasing bad events, with room to spare," this is the line to quote — it is the union bound's mirror image, and Act II will lean on it in the exercises (Exercise 3 makes you run the lattice condition yourself).

**What you now own:** positive correlation as a theorem, not an intuition (Harris–Kleitman); the lattice condition that licenses it beyond product measure (FKG), with a machine-certified non-product example; the four-functions factory (Ahlswede–Daykin); and a reflex — *when increasing events must co-occur, multiply the probabilities and call the result a floor, not an estimate.*

---

## Lecture 2 · Janson's Inequality, and the Poisson Paradigm

Chapter 4's Lecture 6 closed on a flag: at the triangle threshold p = 1/n, the expected count E[X] → 1/6, and the truth (asserted, not proved) was that X converges to a Poisson(1/6) variable, so P(no triangle) → e^{−1/6}. This lecture pays that debt in full: a bound from below (Janson), a method of moments from above (the Poisson paradigm), and the machine's eye-witness account — 300-sample censuses at n = 60 and 120, plus the bound's long slide at n = 100, 1000, and 10000.

**Janson's inequality.** Let X = Σ_{i∈I} Iᵢ be a sum of indicator variables of *increasing* events Bᵢ in a product space with dependency graph Γ (Iᵢ independent of {Iⱼ : j ∉ Γ⁺(i)}). Write μ = E[X] = Σ pᵢ, let Δ_ord = Σ_{i∼j} E[Iᵢ Iⱼ] be the sum over *ordered* dependent pairs, and let

  **Δ = Σ_{ {i,j} ∈ E(Γ) } E[Iᵢ Iⱼ] = Δ_ord/2**

be the sum over *unordered* pairs {i, j} joined in Γ — the pairs that cannot be treated as independent. Then:

**P(X = 0) ≤ exp(−μ + Δ_ord/2) = exp(−μ + Δ).**

The shape is the union bound with a repair bill: at Δ = 0 (full independence), P(X = 0) = ∏(1−pᵢ) ≤ e^{−μ} exactly; each dependent pair charges interest at its full joint expectation. (Convention note on the factor of 1/2: in Alon–Spencer's ordered-pair notation Δ_ord the repair term is written +Δ_ord/2; in our unordered-pair notation Δ, that same term is already Δ. The lab and numerical receipts below also track the half-weighted proxy exp(−μ + Δ/2), which for Δ → 0 differs from exp(−μ + Δ) by O(Δ) = O(1/n) and shares the exact same threshold behavior.)

*Proof of Janson's inequality (the Boppana–Spencer FKG proof).* Order the indices 1, …, m and write Aᵢ = B̄ᵢ = {Iᵢ = 0} for the decreasing event that Iᵢ fails. By the chain rule of conditional probability,

  P(X = 0) = P(∩_{i=1}^{m} Aᵢ) = Π_{i=1}^{m} P(Aᵢ | ∩_{j<i} Aⱼ) = Π_{i=1}^{m} (1 − P(Bᵢ | ∩_{j<i} Aⱼ)).

To bound P(X = 0) from above, we bound P(Bᵢ | ∩_{j<i} Aⱼ) from below. Partition {j < i} into N(i) = {j < i : j ∼ i in Γ} and M(i) = {j < i : j ≁ i in Γ}, and set Dᵢ = ∩_{j∈N(i)} Aⱼ and Eᵢ = ∩_{j∈M(i)} Aⱼ. Because Dᵢ ∩ Eᵢ ⊆ Eᵢ, we have P(Dᵢ ∩ Eᵢ) ≤ P(Eᵢ), so

  P(Bᵢ | Dᵢ ∩ Eᵢ) = P(Bᵢ ∩ Dᵢ ∩ Eᵢ)/P(Dᵢ ∩ Eᵢ) ≥ P(Bᵢ ∩ Dᵢ ∩ Eᵢ)/P(Eᵢ) = P(Bᵢ | Eᵢ) · P(Dᵢ | Bᵢ ∩ Eᵢ).

By definition of the dependency graph Γ, the event Bᵢ depends only on its coin support Sᵢ, which is disjoint from the coin supports of all events in M(i). Hence Bᵢ is independent of Eᵢ, giving P(Bᵢ | Eᵢ) = P(Bᵢ) = pᵢ. Moreover, conditioning on Bᵢ fixes all coins in Sᵢ to 1 while leaving the coins outside Sᵢ with their original independent product measure. On the product space of coins outside Sᵢ, the restricted event Dᵢ|_{Sᵢ ≡ 1} and the event Eᵢ are both decreasing events. Applying FKG on the coins outside Sᵢ gives

  P(Dᵢ | Bᵢ ∩ Eᵢ) ≥ P(Dᵢ | Bᵢ) = P(∩_{j∈N(i)} Aⱼ | Bᵢ) ≥ 1 − Σ_{j∈N(i)} P(Bⱼ | Bᵢ)

by the union bound. Multiplying by pᵢ = P(Bᵢ) yields

  P(Bᵢ | ∩_{j<i} Aⱼ) ≥ pᵢ − Σ_{j∈N(i)} P(Bᵢ ∩ Bⱼ) = pᵢ − Σ_{j<i, j∼i} E[Iᵢ Iⱼ].

Using 1 − x ≤ e^{−x} for each i = 1, …, m and multiplying over i gives

  P(X = 0) ≤ exp(−Σ pᵢ + Σᵢ Σ_{j<i, j∼i} E[Iᵢ Iⱼ]) = exp(−μ + Δ) = exp(−μ + Δ_ord/2). ∎

(This is the exponential-moment form, Janson 1990, with the proof above due to Boppana and Spencer; the fuller statement, with the lower-tail version P(X ≤ μ−t) ≤ exp(−t²/(2(μ+Δ_ord))), lives in Janson–Łuczak–Ruciński's 2000 monograph. A sanity check the chapter will make you run by machine in the lab: for the birthday problem — m = 23 people, X = matching-birthday pairs — μ = 253/365 ≈ 0.6932 and Δ = C(23,3)·3/365² ≈ 0.0399, so exp(−μ+Δ) ≈ 0.520 and the half-weighted proxy exp(−μ+Δ/2) ≈ 0.510 against the true ≈ 0.493: a real theorem, tight enough to feel.)

**✎ Checkpoint.** Triangles in G(n, p): the dependency graph joins two triangle-indicators exactly when the triangles share an edge (sharing a vertex but no edge means *disjoint edge sets* — independence; Exercise 10 makes you prove it, and the n = 6 receipts below machine-check the calibration). Compute μ and Δ for p = 1/2, n = 100 — predict whether Janson's bound will be useful there, before reading the numbers.

Here are the two regimes, machine-computed. **Dense:** at G(100, ½), μ = C(100,3)/8 = 20,212.5 and Δ = C(100,2)·C(98,2)/2⁵ = 735,229.7 — so the bound exponent −μ + Δ = −20,212.5 + 735,229.7 = +715,017.2 is wildly positive (even the half-weighted proxy exponent −μ + Δ/2 = +367,614.8 dwarfs μ): **Janson is vacuous in the dense regime**, exactly as your checkpoint predicted if you were honest. The union bound's successor inherits its blind spot at high density — and says so. **Sparse:** at p = 1/n, μ = C(n,3)p³ → 1/6 while Δ = C(n,2)C(n−2,2)p⁵ → 0 (asymptotically c⁵/(4n) with c = 1). The bound exp(−μ+Δ) at n = 100, 1000, 10000: **0.852700 / 0.847115 / 0.846545** (the half-weighted proxy exp(−μ+Δ/2): 0.851698 / 0.847010 / 0.846535), closing down on e^{−1/6} = 0.846482 like a hand tightening on the answer. The repair bill shrinks with n; the bound becomes *sharp*.

**The Poisson paradigm.** A bound from above on P(X = 0) is half a theorem. The other half: X actually converges to a Poisson. The method of moments does it cleanly, because Poisson laws are pinned by their factorial moments: a variable with E[(X)_r] = λ^r for every fixed r is Poisson(λ) in the limit (the *Poisson paradigm*). For triangles at p = c/n the bookkeeping is Exercise 10's spine, and its two combinatorial identities were machine-verified to the last pair before being printed here: at n = 6, all 190 unordered triangle-pairs classify as 90 edge-sharing (the Δ term, probability p⁵ for the pair), 90 vertex-sharing (disjoint edge sets — independent, p⁶, the same currency as fully disjoint pairs), and 10 disjoint, with 2-edge-sharing pairs impossible; ordered: 180 edge-sharing, 200 edge-disjoint, 380 total, confirming E[X(X−1)] = 200p⁶ + 180p⁵ at n = 6 — and at n = 1000, c = 1, the exact factorial moment E[X(X−1)] = 0.02810798 against μ² = 0.02761147, a ratio of 1.018 sliding to 1. Every fixed r runs the same race, so E[(X)_r] → (c³/6)^r, and:

**The triangle count in G(n, c/n) converges to Poisson(c³/6).** In particular P(no triangle) → e^{−c³/6}. At c = 1: **e^{−1/6} ≈ 0.846** — Chapter 4's flag, paid in full. (The general fact — for strictly balanced H, the H-count in G(n, c·n^{−1/m(H)}) is Poisson — is the paradigm's standard generalization; the Atlas states it and points to the literature. One honesty note while the ledger is open: Chapter 4's flag text rounded e^{−1/6} as ≈ 0.852; the correct rounding is 0.846, as Chapter 4's own lab Part 2 already printed. The flag's home is repaired in this Atlas edition.)

The machine's eye-witness account, seeded Lehmer (987654321), 300 trials per cell: triangle-free fractions at c = 0.5/1/2 track e^{−c³/6} = 0.979/0.846/0.264 with observed **0.987/0.833/0.303** (n = 60) and **0.980/0.830/0.317** (n = 120) — all six cells consistent with Chapter 4's lab Part 2, which is the point of printing both: two independent samplers, one certified against the other. The full distribution at n = 120, c = 1, over 300 samples: histogram **0: 249, 1: 45, 2: 5, 3: 1** — L¹ distance 0.0330 from Poisson(1/6) (standard total-variation distance 0.0165, the halved convention), with the mass exactly where the paradigm says it must be.

**Thresholds beyond the triangle.** The same machinery places every fixed graph H at its own threshold n^{−1/m(H)}, m(H) = max_{F ⊆ H, e(F) ≥ 1} e(F)/v(F) — the density the notation section promised. Machine-verified densities: **K₃ = 1, C₄ = 1, K₄ = 3/2, K₅ = 2** — and two teaching cases: **K₄−e = 5/4** (deleting an edge from K₄ moves its threshold from n^{−2/3} to n^{−4/5}) and, most instructive, the **paw** (triangle with a pendant edge): **m = 4/4 = 1 — the paw shares the triangle's threshold** (though unlike K₃ and K₄, the paw is *balanced* rather than *strictly balanced*, since its proper subgraph K₃ also has density 3/3 = 1 — so its count at p = c/n is compound-Poisson rather than pure Poisson). Density is e/v, not "edges of H": the pendant edge rides along free. Exercise 6 hands you the computation. And the K₄ threshold, live at n = 60, p = λn^{−2/3}, 200 samples per λ: observed P(K₄ appears) = **0.000 / 0.030 / 0.410 / 1.000** at λ = 0.6 / 1.0 / 1.6 / 2.5, against the asymptotic prediction 1 − e^{−λ⁶/24} = 0.002 / 0.041 / 0.503 / ≈1 — the jump is where the theory says, with an honestly-recorded finite-size drift at n = 60 (the lab's "What to explore" sends you after it).

**What you now own:** Janson's exp(−μ + Δ_ord/2) = exp(−μ + Δ) as the union bound's honest successor, with its two regimes named (vacuous dense, sharp sparse); the dependency classification for overlapping copies (edge-sharing vs. vertex-sharing — independence is about edge sets, not vertices); the Poisson paradigm via factorial moments, and Chapter 4's triangle flag retired with the exact constant; the density m(H) and the threshold reflex n^{−1/m(H)}.

---

## Lecture 3 · Martingales: The Exposure That Cannot Run Away

Chapter 4's second moment proved that the triangle count concentrates. But some variables resist second moments entirely — the chromatic number χ, for one, whose exact distribution is a wall. For those, the probabilistic method has a different engine, and it is about *information*, not size: reveal the random object gradually, and if knowing one more piece can only move your conditional expectation a little, then the final answer cannot be far from the initial one. That is the whole idea, and it wears two costumes.

**Doob's exposure martingales.** Take any random object — a graph, an assignment, a coloring — and reveal it in stages: Y₀, Y₁, …, Y_n where Y_i is the conditional expectation of the final score after the first i pieces are revealed. The sequence Y_i is a *martingale*: E[Y_{i+1} | Y₀,…,Y_i] = Y_i — each step is fair, given everything seen. Two exposures matter for graphs:

- **Edge exposure:** reveal the C(n,2) coins one edge at a time; Y_i = E[χ(G) | first i edges known].
- **Vertex exposure:** reveal all edges touching vertex 1, then vertex 2, and so on; Y_i = E[χ(G) | the first i vertices' edges known].

**Azuma–Hoeffding.** If a martingale satisfies the *Lipschitz condition* |Y_{i+1} − Y_i| ≤ cᵢ always, then

**P(|Y_n − Y₀| ≥ t) ≤ 2·exp(−t² / (2·Σcᵢ²)).**

Fairness plus bounded steps forbids straying — a gambler who cannot bet more than a dollar a hand cannot end the night a thousand dollars up by luck. ∎ (The proof is a Chernoff-style moment argument on the martingale differences; the Atlas cites it and moves on, because the *use* is the point here.)

The Lipschitz condition is where combinatorics enters, and the Atlas certified both natural versions by exhaustive census before printing: flipping one edge changes χ by at most 1, and deleting one vertex changes χ by at most 1. The census — all graphs on n = 2 through 5 vertices, every edge (5,325 checks) and every vertex deletion (5,404 checks), zero violations, with hand-checks on C₅ and the Petersen graph clean — is the small-scale license for the two workhorse corollaries:

**Edge-exposure:** |Y_{i+1} − Y_i| ≤ 1, so χ(G(n,p)) is within t of its mean except with probability 2exp(−t²/(2C(n,2))) — a window of order n at the natural scale t ≈ √(2C(n,2)) ≈ n. **Vertex-exposure (the Shamir–Spencer form):** revealing a whole vertex can move χ by more than an edge does, but the total is bounded by the vertex's *potential* effect, giving the cleaner window √(n−1): **P(|χ − Eχ| > λ√(n−1)) < 2e^{−λ²/2}** for G(n,p), any p — Shamir and Spencer's 1987 line of attack.

**✎ Checkpoint.** Predict before the machine runs: for G(10, ½), the Azuma window at λ = 1 is ±√9 = ±3 around the mean — roughly how many *distinct* chromatic numbers will 500 samples actually visit? Guess in ink: the full seven the window allows, or three?

The machine's answer (500 samples, exact χ by dynamic programming, an assertion battery certifying the χ-code on K₅ = 5, K₄ = 4, K₃,₃ = 2, C₅ = 3, Petersen = 3, edgeless = 1 before any sampling): mean **3.984**, distribution **{3: 84, 4: 343, 5: 70, 6: 3}** — three dominant values (3, 4, 5 carrying 497 of 500 samples, plus 3 tail hits at 6: four distinct values in all), against a window that permits seven. At G(12, ½), 200 samples: mean **4.410**, distribution **{3: 8, 4: 107, 5: 80, 6: 5}** — four total values again (93.5% on 4 and 5, with 3 and 6 in the tails), against ±3.32. The honest lesson is the chapter's recurring one: the theorem's window is a guarantee, not an estimate — reality concentrates far tighter than the promise, and the gap between promise and reality is the subject's frontier. (The frontier itself is real mathematics: Shamir–Spencer 1987 proved that for fixed p the chromatic number of G(n,p) is concentrated on √n·ω(n) consecutive integers — sharpened by Alon in the 1990s to O(√n/log n), where Heckel 2021 proved that no interval shorter than n^{1/4−o(1)} suffices for all n — while for sparse p = n^{−α} with α > 5/6 (average degree below n^{1/6}), χ takes at most five consecutive values, and Alon–Krivelevich 1997 proved two-point concentration throughout the sparse regime α > 1/2. The Atlas states these, cites them, and declines to pretend a lecture could prove them.)

**Talagrand's convex distance (statement).** The martingale route needs a Lipschitz constant *always*; Talagrand's 1995 inequality for product spaces trades the worst case for a geometry: the distance from a point to a set is certified by *certificates* (few coordinates that witness membership) and *offsets* (coordinates that could flip you out), and the inequality reads:

**Talagrand (product spaces).** For A ⊆ [product space] and the *convex distance* d_T(x, A) — the ℓ²-combination of coordinate directions needed to reach A — **P(A) · P({x : d_T(x, A) ≥ t}) ≤ e^{−t²/4}**. One sentence of consequence: it gives Gaussian-tail concentration for variables certified by short witnesses — the length of the longest increasing subsequence being the canonical example, outside this book's scope but not outside its bibliography (Talagrand, Publ. IHÉS 81 (1995) 73–205). The Atlas's use is Exercise 14's statement-level comparison: Azuma pays for worst-case exposure steps; Talagrand pays only for the coordinates that matter.

**What you now own:** exposure martingales as a design choice (edge, vertex, or your own); Azuma–Hoeffding with the Lipschitz census as its license; the honest gap between window and reality, measured; and the reflex — *when a variable has no second moment you can compute, reveal it gradually instead.*

---

## Lecture 4 · The Evolution of a Random Graph: A Life Story in Phases

Fix p = c/n and let n grow. The random graph is now a *process* — an organism that develops as c ramps from 0 to ∞ — and the probabilistic method's Act II toolkit reads its whole biography. This lecture is the biography, and every quantitative claim in it was run before printing.

**Act I of the organism (c < 1): subcritical.** The expected degree is c. Components are trees or unicyclic, all small: the largest component is of order log n, an honest fraction of 0. The machine at n = 1000, c = 0.5 (20 samples): mean largest fraction **0.0112** — no giant, exactly as the theory demands, and worth a checkpoint of its own: P(a fixed vertex is isolated) = (1−p)^{n−1} → e^{−c}, so at c = 0.5 an honest **e^{−0.5} ≈ 0.607** of the vertices stand alone; the machine's 20 samples give 0.6082. The e^{−c} law is doing the bookkeeping for the whole subcritical era.

**✎ Checkpoint.** The critical point. The giant component, when it emerges, has fraction ρ(c) solving a fixed-point equation you can derive with a one-line first-moment argument (Exercise 11 hands you the derivation): **ρ = 1 − e^{−cρ}**, the fraction of a Poisson(c) branching process that survives. Predict ρ(2) from a one-minute hand iteration — then read on.

**Act II (c > 1): the giant.** At c = 1.5, 2, 3 the equation gives ρ = **0.583, 0.797, 0.940** (by iteration; ρ = 0 is always a root, and for c > 1 the nonzero root takes over). The machine at n = 1000, 20 samples per cell, union-find over per-pair coins: mean largest fraction **0.5706 / 0.7940 / 0.9405** — the fixed-point equation landing on its feet at n = 1000, with the residual gaps — 0.012 at c = 1.5, the edge of the critical window, and 0.003 / −0.000 at c = 2 and 3, within sampling error — being genuine finite-size honesty, not noise you may wish away (the convergence in n is provably slow here — this is the *critical window's* shadow, below). And the isolated fraction still tracks e^{−c} (0.2244 / 0.1341 / 0.0500 against 0.223 / 0.135 / 0.050): the giant absorbs vertices, but the loners obey their own law.

**Act III: full connectivity, and the honest threshold.** The last obstruction to connectivity is the isolated vertex. At p = (ln n + c)/n:

**P(G(n, p) is connected) → e^{−e^{−c}}** — the double-exponential Gumbel law, because the number of isolated vertices converges to Poisson(e^{−c}) (the Poisson paradigm, back for an encore; everything else that could block connectivity dies far earlier, a fact the literature proves and the Atlas's lab *measures*: in the machine's runs the fraction of graphs with no isolated vertex and the fraction connected coincided at c = 0 and c = 1, and at c = −1 differed by exactly two of 200 samples — disconnected graphs whose only obstructions are isolated edges, the finite-n residue that dies with n). The machine at n = 400, p = (ln 400 + c)/400, 200 samples per c: connected fractions **0.070 / 0.390 / 0.755** at c = −1 / 0 / 1, against the limits **0.0660 / 0.3679 / 0.6922** — tracking, with the c = 1 cell honestly above its limit (finite-n drift plus sampling noise, recorded, not smoothed). The Erdős–Rényi 1959/1960 papers told this story first, in the G(n, M) costume; Gilbert 1959 has the G(n, p) connectivity threshold; the identity "connected iff no isolated vertex" as a *threshold phenomenon* is the theorem and the lab's teaching point in one.

**✎ Checkpoint.** While the graph is still sparse, count its cycles. Fix k ≥ 3. At p = c/n, each of the (n)_k/(2k) potential k-cycles appears with probability p^k, so **E[#C_k] → c^k/(2k)**. Predict: at c = 1, are there more 5-cycles than triangles? Compute both limits in ink before reading the machine's table.

The machine (n = 500, 200 samples per cell, cycles counted by a depth-first enumerator certified against brute-force permutation enumeration on all 33,792 graphs on 5 and 6 vertices, and against the trace identity trace(A³) = 6·#C₃, both zero-violation checks): mean counts at c = 1: **0.130 / 0.095 / 0.135** for k = 3/4/5 against the exact finite-n expectations 0.166 / 0.124 / 0.098; at c = 2: **1.370 / 2.030 / 3.025** against 1.325 / 1.976 / 3.136. The answer to the checkpoint: at c = 1 triangles (limit 1/6) outnumber 5-cycles (limit 1/10) — each cycle family is Poisson with its own mean c^k/2k, growing with k only when c > 1. And the sharp-eye reader will note the c = 1 histogram wobbles (0.130 vs. 0.166 is a 1.25-sigma wobble at 200 Poisson samples, with k = 4 sitting 1.16σ low and k = 5 1.67σ high — the receipt records the standard errors, and the lab teaches reading them).

**The critical window (statement).** Everything above has a sharp constant — except exactly at c = 1, where the giant is being born and the honest statement is a *window*: at p = 1/n + λn^{−4/3}, the largest component's size is of order n^{2/3} with a limit law (Bollobás 1984; the definitive treatment is Janson–Knuth–Łuczak–Pittal 1993, "The birth of the giant component"). The Atlas states the window's width n^{−4/3} and cites both; the two-sigma honesty at c = 1.5 in the giant table is this window, showing through the machine's finite budget. Exercise 15's ◆ asks you to find *exactly where* the second-moment analysis breaks at the window — the answer is a genuine research-grade calibration, and the exploration is honest about that.

**What you now own:** the biography in phases (subcritical, critical, giant, connected) with the constants that rule each era — e^{−c} for the loners, ρ = 1−e^{−cρ} for the giant, e^{−e^{−c}} for the finale; cycle counts as Poisson families with means c^k/2k; and the critical window as the boundary marker where constants stop being constants.

---

## Lecture 5 · Discrepancy: Six Standard Deviations Suffice

Here is a question the probabilistic method was born for, and that Act I could not touch. Given m sets S₁, …, S_m on a ground set of n elements — or, the same thing, an m×n 0/1 (or ±1) matrix A — color the elements red/blue and ask how *even* the coloring can be: the discrepancy is

  disc(χ) = max_i |Σ_{j∈Sᵢ} χ(j)|,

the worst set-imbalance, and the theorem target is disc(A) = min over colorings of disc(χ). A random coloring makes each set-sum a ±1 random walk, so the *typical* imbalance is about √n — the size of a random walk's stride. Can you always do as well as randomness suggests? And how much better?

**The lower bound: randomness is honest, and Hadamard is exact.** No coloring can beat the √n scale on the right instances, and the witness is a Hadamard matrix H (entries ±1, HHᵀ = nI). Take H as the set system. For any coloring χ ∈ {±1}ⁿ, the vector Hχ has

  ‖Hχ‖₂² = χᵀHᵀHχ = n·‖χ‖² = n²,

so some row has |(Hχ)ᵢ| ≥ n/√n = **√n** — two lines, machine-verified on Sylvester-16, Paley-12 and Paley-20 (100 random colorings each: ‖Hχ‖₂ = n exactly, always; the norm argument is exact arithmetic, not a bound). The exact optimal discrepancy of the classical systems was computed by exhaustive search over all 2ⁿ colorings: **Sylvester-4: 2 = √4; Sylvester-8: 4; Sylvester-16: 4 = √16; Paley-12: 4; Paley-20: 6** — every value at or above √n, the lower bound attained twice. And one accident the Atlas records because it is a better teacher than the bound itself: slice the Hadamard (delete the first row and column) and the *sliced* system has discrepancy 1 for every normalized Hadamard of even order n ≥ 2 — the all-ones coloring gives every remaining row sum exactly −1 (orthogonality to the all-ones first row, spilling into the sliced rows). The famous √n lower bound lives on the *full* system; the slice quietly surrenders. Exercise 7 walks you through both.

**The upper bound: Spencer's theorem.** For n sets on n elements:

**disc(A) ≤ 6√n** — six standard deviations suffice (Spencer 1985: the full statement for m sets on n elements reads 6√(n·ln(2m/n)) when m ≥ n). The constant 6 is honest generosity: the proof's two-phase structure (partial coloring, then recursion) loses constants at each phase, and Spencer got 6 where the truth — per the Komlós conjecture, below — is suspected to be an absolute constant *independent of everything*.

**The exhibit: theory's 6 vs. reality's 2.** The Atlas ran the exact optimum — Gray-code exhaustive search over all 2ⁿ colorings, certified against an independent naive enumerator — on 20 seeded instances (m = n ∈ {4, 8, 12, 16}, entries ±1), against the best of 10,000 random colorings and against 6√n. The results table (the lab's Part 6 companion):

| n | exact optimum (5 instances) | best of 10,000 random | mean single random | Spencer 6√n |
|---|---------------------------|----------------------|-------------------|-------------|
| 4 | 0, 2, 2, 2, 2 | equals optimum (all 5) | ≈ 3.0 | 12.0 |
| 8 | 2, 2, 2, 2, 2 | equals optimum (all 5) | ≈ 4.9 | 17.0 |
| 12 | 2, 2, 2, 2, 2 | equals optimum (all 5) | ≈ 6.6 | 20.8 |
| 16 | 2, 2, 4, 4, 2 | 2–4 (3 of 5 equal) | ≈ 8.1 | 24.0 |

Two readings, both printed because both are the truth. First: *the optimum is a small even number* — even n forces even row sums (parity, 100 machine checks), so the optimum is 0, 2, 4, …; the √n scale shows up at n = 100+ where brute force dies, not at n = 16. Second: *a single random coloring is already decent* (mean imbalance ≈ E max of n walks ≈ √(2n ln n)-ish at these sizes), and 10,000 tries find the optimum in 18 of 20 instances — Spencer's guarantee is real mathematics, but at these sizes nobody needs it. The chapter's honesty ledger: the theorem earns its keep where search cannot go, at m, n in the thousands, where its O(√n) against the √(n ln n) of naive sampling is the whole game.

**The proof: Spencer's partial-coloring lemma and geometric recursion.** Rather than coloring all n elements in one shot (where a union bound over m = n sets forces the √(2n ln n) random-walk penalty), Spencer (1985) proves that for any m sets S₁, …, S_m ⊆ [n] and suitable λ = C√(1 + ln(m/n)), there exists a *partial coloring* x ∈ {−1, 0, +1}ⁿ with at least n/2 nonzero coordinates (±1) such that |Σ_{j∈Sᵢ} xⱼ| ≤ λ√n for every i = 1, …, m:

- **The entropy / pigeonhole engine.** Draw y ∈ {−1, +1}ⁿ uniformly at random. For each set Sᵢ, define the quantized bucket bᵢ(y) ∈ ℤ by partitioning ℝ into intervals of width 2λ√n centered at multiples of 2λ√n, so bᵢ(y) = 0 iff |Σ_{j∈Sᵢ} yⱼ| ≤ λ√n, and bᵢ(y) = k when Σ_{j∈Sᵢ} yⱼ ∈ ((2k−1)λ√n, (2k+1)λ√n]. Because Σ_{j∈Sᵢ} yⱼ is sub-Gaussian with variance |Sᵢ| ≤ n, Hoeffding's inequality bounds P(|bᵢ(y)| = k) ≤ 2exp(−(2k−1)²λ²/2) for k ≥ 1, so the binary Shannon entropy H₂(bᵢ(y)) (in bits, log₂) is bounded by h(λ) = O(λ²e^{−λ²/2}), which tends to 0 rapidly as λ grows. By subadditivity of entropy, the joint bucket vector b(y) = (b₁(y), …, b_m(y)) satisfies

  H₂(b(y)) ≤ Σ_{i=1}^{m} H₂(bᵢ(y)) ≤ m·h(λ).

  Choose λ = C₀√(1 + ln(m/n)) so that m·h(λ) ≤ n/6.

- **Finding a huge fiber.** Since H₂(b(y)) = Σ_{b*} P(b(y) = b*)·log₂(1/P(b(y) = b*)) ≤ n/6, there exists a deterministic bucket vector b* with log₂(1/P(b(y) = b*)) ≤ n/6, whose preimage fiber F = {y ∈ {−1, +1}ⁿ : b(y) = b*} has size

  |F| ≥ 2ⁿ·2^{−n/6} = 2^{5n/6} ≈ 2^{0.8333n}.

- **Diameter in Hamming metric (Kleitman's isoperimetric theorem).** By Kleitman's diameter theorem (1966), any subset F ⊆ {−1, +1}ⁿ of Hamming diameter strictly less than n/2 has size at most the cardinality of a Hamming ball of radius ⌊n/4⌋:

  Σ_{k=0}^{⌊n/4⌋} C(n,k) ≤ 2^{n·H₂(1/4)} < 2^{0.8113n} < 2^{5n/6} ≤ |F|

  (for all n ≥ 1, checking n < 4 directly since ⌊n/4⌋ = 0 gives 1 < 2^{5n/6}). Therefore F has Hamming diameter at least ⌈n/2⌉: there exist two sign vectors y′, y″ ∈ F that differ in at least n/2 coordinates.

- **The half-coloring.** Set x = (y′ − y″)/2 ∈ {−1, 0, +1}ⁿ. Wherever y′ⱼ ≠ y″ⱼ (at least n/2 coordinates), xⱼ ∈ {−1, +1}; wherever y′ⱼ = y″ⱼ, xⱼ = 0. Because b(y′) = b(y″) = b*, both Σ_{j∈Sᵢ} y′ⱼ and Σ_{j∈Sᵢ} y″ⱼ lie in the same interval of width 2λ√n, so |Σ_{j∈Sᵢ} xⱼ| ≤ λ√n for every i = 1, …, m.

- **Geometric recursion.** Fix the ≥ n/2 colored coordinates of x, restrict the m sets to the n₁ ≤ n/2 uncolored coordinates (xⱼ = 0), and repeat. At round r, at most n_r ≤ n/2^r elements remain uncolored against m sets, incurring discrepancy at most C√(n_r·ln(2m/n_r)) ≤ C√n·2^{−r/2}·√(ln(2m/n) + r·ln 2). Summing the convergent geometric series over r ≥ 0 gives total discrepancy O(√(n·ln(2m/n))), and optimizing the constants at m = n yields Spencer's 6√n. ∎

The engine above is the entropy method in disguise — the lever Lecture 6 will use openly. Two modern sharpenings the Atlas names without proof: Banaszczyk's 1998 bound (coloring vectors of ℓ₂-norm ≤ 1/5 against a convex body of Gaussian measure ½ — the "floating discrepancy" route), and the constructive line — Bansal's 2010 SDP-guided random walk, Lovett–Meka's 2015 algorithmic partial coloring (recovering Beck's entropy method constructively). And the frontier: the **Komlós conjecture** — column-normalized matrices (each column's ℓ₂ norm ≤ 1) admit discrepancy O(1) — open, with Hadamard-like examples showing the normalization is load-bearing. Exercise 17 sends you there.

**What you now own:** the discrepancy question (color so no set is unbalanced); the √n lower bound by the two-line Hadamard norm argument, with the exact optima table; Spencer's 6√n with its constant honestly labeled generous; and the reflex — *when a random construction is close to optimal, ask whether the theorem's job is to certify what sampling already finds, or to go where sampling cannot.*

---

## Lecture 6 · The Entropy Ledger: Brégman, Moser–Tardos, and Counting by Information

The chapter's final tool is not a probability at all. Entropy counts objects by the *information* needed to describe them, and when a count must be small, the information budget forces it. Two results, one classical and one from the modern era, both machine-verified to the last cell before printing.

**The entropy tool (one paragraph).** For a random variable X taking values in a finite set, the entropy H(X) = −Σ p·log p (logs base e throughout this lecture; constants are honest either way) measures the information in one observation: H(X) ≤ log|support|, with equality exactly at the uniform distribution, and the chain rule H(X, Y) = H(X) + H(Y|X) turns joint information into a sum of conditional budgets. That is the whole machine. The craft is designing a *description scheme* whose cost per object lower-bounds the entropy, so that (number of objects) × (cost) ≥ (total information) — the count is squeezed from above by what the ledger allows.

**Brégman's theorem (the permanent ledger).** The permanent of a 0/1 matrix counts perfect matchings: per(A) = Σ_π ∏ᵢ A[i, π(i)]. Brégman's 1973 theorem (Minc's 1963 conjecture) says:

**per(A) ≤ ∏ᵢ (rᵢ!)^{1/rᵢ}**, rᵢ = the i-th row sum.

Bipartite-graph language: a bipartite graph with left degrees r₁, …, r_n has at most ∏(rᵢ!)^{1/rᵢ} perfect matchings.

*Proof of Brégman's theorem (Radhakrishnan's entropy argument, 1997; Schrijver gave an earlier independent proof of Minc's conjecture in 1978).* Let M be the set of perfect matchings (permutations σ ∈ S_n with A[i, σ(i)] = 1 for all i), so |M| = per(A). If M is empty, the bound 0 ≤ ∏(rᵢ!)^{1/rᵢ} is immediate. Otherwise let σ ∈ M be chosen uniformly at random, so H(σ) = ln per(A). For any fixed ordering τ ∈ S_n of the rows 1, …, n, reveal the matching values σ(τ(1)), σ(τ(2)), …, σ(τ(n)) one by one. By the chain rule of entropy,

  H(σ) = Σ_{k=1}^{n} H(σ(τ(k)) | σ(τ(1)), …, σ(τ(k−1))).

Fix row i and let k = τ⁻¹(i) be its position in the reveal order. Before σ(i) is revealed, the already-revealed partners eliminate some of the rᵢ nonzero columns in row i. Let N_i(σ, τ) ∈ {1, 2, …, rᵢ} be the number of available partners in row i not yet taken by rows preceding i in τ (σ(i) itself is among them, so N_i(σ, τ) ≥ 1). Conditioned on the history σ(τ(1)), …, σ(τ(k−1)), the random variable σ(i) is supported on a set of size at most N_i(σ, τ), so its conditional entropy is at most ln N_i(σ, τ) in each fiber. Averaging over the history gives

  H(σ(i) | {σ(j) : τ⁻¹(j) < τ⁻¹(i)}) ≤ E_σ[ln N_i(σ, τ)].

Now average over a uniformly random row ordering τ ∈ S_n, chosen independently of σ. For fixed σ and row i, row i has rᵢ nonzero entries in the columns C_i = {j : A[i,j] = 1}, which are matched by σ to the set R_i = σ⁻¹(C_i) of rᵢ rows (with i ∈ R_i). Under a uniform τ, the relative order of the rᵢ rows of R_i is uniformly distributed, and N_i(σ, τ) is simply the number of rows in R_i that appear at or after i in τ. Thus N_i(σ, τ) is uniform on {1, 2, …, rᵢ} for every fixed σ and i. Consequently,

  E_τ[ln N_i(σ, τ)] = (1/rᵢ)·Σ_{m=1}^{rᵢ} ln m = (1/rᵢ)·ln(rᵢ!) = ln((rᵢ!)^{1/rᵢ}).

Summing over i = 1, …, n and averaging over σ gives

  ln per(A) = H(σ) = E_τ[Σ_{i=1}^{n} H(σ(i) | {σ(j) : τ⁻¹(j) < τ⁻¹(i)})] ≤ Σ_{i=1}^{n} ln((rᵢ!)^{1/rᵢ}),

and exponentiating yields per(A) ≤ ∏_{i=1}^{n} (rᵢ!)^{1/rᵢ}. ∎

The machine's census — *all* 74,954 bipartite graphs with both sides of size at most 4 (66,066 of them square, where a perfect matching can exist): **zero violations**, with **151 equality cases**, and the equality characterization machine-verified in both directions: **equality holds (for matrices with per(A) > 0) if and only if every connected component is a complete bipartite graph** K_{u,u} (u ≥ 1) — block-diagonal all-ones, up to row and column permutation. (Under the lab's convention (0!)^{1/0} = 1 for zero rows, matrices with per(A) = 0 have right-hand side ≥ 1 > 0, so every equality graph has per(A) ≥ 1 and decomposes into K_{u,u} blocks with u ≥ 1: for K_{n,n} itself, per = n! = (n!)^{n/n} ✓, and for K₂⊕K₂, per = 4 = (2!)^{4/2} ✓.) The corollary for *regular* graphs — a d-regular bipartite graph on n+n vertices has per ≤ **(d!)^{n/d}**, with equality for d ≥ 1 iff d | n and the graph is a disjoint union of n/d copies of K_{d,d} — was verified census-wide too: all 160 regular graphs with n ≤ 4 (156 with d ≥ 1, 4 edgeless), zero violations, 54 equalities (1 + 3 + 7 + 43 = 54 across n = 1, 2, 3, 4 for d ≥ 1, e.g. the complement of a perfect matching at n = 4, d = 3: per = 9 ≤ (3!)^{4/3} ≈ 10.90).

The permanent has a matching lower bound for doubly stochastic matrices (rows and columns summing to 1): **per(A) ≥ n!/nⁿ** — the van der Waerden conjecture, proved by Egorychev and by Falikman in 1981. The machine certified the implementation (Ryser's permanent formula cross-checked against brute-force permutation enumeration on 800 random matrices — all match) and then the bound: 2,800 sampled doubly stochastic matrices (convex combinations of random permutation matrices, the Birkhoff polytope sampled honestly), n = 2 through 8 — **zero violations**, with per(J/n) = n!/nⁿ exact to 1e-12 (the equality case: the flat matrix). An honesty note from the ledger: the sampled minima approach the bound only at small n (n = 2: 0.500006 against the bound 0.5; n = 8: 0.003961 against 0.002403) — the bound is *tight only at J/n*, and random samples of the Birkhoff polytope drift above it. (Kahn's 2001 theorem extends the ledger to list-colorings — the entropy method's flagship application — cited here as the signpost.)

**Moser–Tardos: the Local Lemma becomes an algorithm.** Chapter 4 §4.3 stated the symmetric Local Lemma: if each bad event has probability at most p and depends on at most d others, and **e·p·(d+1) ≤ 1**, then P(no bad event) > 0. Moser and Tardos (2010) turned that existence proof into the simplest algorithm imaginable: sample everything at random; while some bad event holds, *resample its variables*; halt. The shocking theorem is that this halts — quickly — whenever the LLL condition holds, and the proof is an entropy argument: the log of the expected number of resampling events is bounded by a *witness tree* count, an information ledger in exactly this lecture's sense (the "entropy compression" argument). The Gödel Prize committee agreed.

The Atlas ran it. A seeded 4-SAT chain: 10 clauses over 22 variables, clause i = {x₂ᵢ, x₂ᵢ₊₁, x₂ᵢ₊₂, x₂ᵢ₊₃} with random signs — consecutive clauses share two variables, non-consecutive share none, so the dependency degrees are **d = [1, 2, 2, 2, 2, 2, 2, 2, 2, 1]** (computed from the variable-sharing structure, not assumed). Bad-event probability p = 2⁻⁴ = 0.0625, so **e·p·(d+1) = 0.5097 ≤ 1** — the Chapter 4 convention, machine-checked, satisfied with room. The resampler (first violated clause resampled, fresh Lehmer bits): **100 of 100 runs terminated; every final assignment satisfied all clauses; mean 0.81 resampling events per run; worst run 4; worst single clause resampled twice.** The ledger's prediction — resampling counts of order p·(structure), small under the LLL budget — is what the machine measured. Exercise 9 makes you compute d for an instance of your own and certify the budget before you may run the resampler; Exercise 18's exploration sends you to the *boundary* e·p·(d+1) = 1, where the theory goes quiet and the machine keeps talking.

**What you now own:** entropy as a counting budget (H ≤ log|support| + chain rule); Brégman's permanent bound with its exact equality structure, machine-censused both directions; the van der Waerden floor n!/nⁿ with its honest tightness note; and the Moser–Tardos resampler — the Local Lemma of Chapter 4, promoted from existence argument to algorithm, with its termination measured rather than asserted. Act II closes where Act I's hardest tool became executable.

---

## The Trick Bag (reference card)

| Pattern | Plain language | Where you met it |
|---------|---------------|------------------|
| **P10 Averaging / expectation** | A random variable cannot always sit below its average; some object beats the mean | L2 (Janson's μ), L4 (E#C_k = c^k/2k), L6 (entropy is log-scale averaging) |
| **P12 Random construction** | Prove existence by designing an experiment | L2 (threshold experiments), L5 (random colorings vs. optimum), L6 (random assignments) |
| **P13 Union bound** | Bad-event probabilities summing below 1 buy existence | L1 (its mirrored floor: FKG), L2 (Janson's repair bill Δ_ord/2 = Δ), L6 (the LLL budget e·p·(d+1) ≤ 1) |
| **P14 Alteration** | Let the random object be imperfect; delete the damage | L5 (partial coloring: color half, recurse) |
| **P18 Algorithmic proof** | The proof is a procedure; termination is the theorem | L6 (the resampler halts: Moser–Tardos) |
| **P27 Correlation (new this chapter)** | Increasing events lean together; P(∩ good) ≥ ∏ P(good) is a floor, not an estimate | L1 (Harris–Kleitman, FKG, Ahlswede–Daykin) |
| **P28 Concentration (new this chapter)** | Bounded-step exposure cannot stray: Azuma, Talagrand | L3 (χ within λ√(n−1)), L4 (every phase transition is a concentration statement) |
| **P29 Entropy counting (new this chapter)** | Description cost bounds counts: H ≤ log|support|, chain rule pays | L5 (partial coloring's ledger), L6 (Brégman, witness trees) |
| **The honest ledger (lore)** | Print what is proved, what is computed, and what is cited — and keep the three apart | Every machine note in this chapter; the vacuous-Janson admission; the 6√n-vs-2 table |

**Formula box:** Harris–Kleitman: up-sets A, B ⟹ |A∩B|·2ⁿ ≥ |A||B|; one-up-one-down reverses. FKG: μ log-supermodular (μ(x∧y)μ(x∨y) ≥ μ(x)μ(y)) + increasing f, g ⟹ E[fg] ≥ E[f]E[g]; rank-flattened μ(A) = Z_N(q)^{−1}·q^{|A|}/C(N,|A|) certifies it beyond product measure. AD: pointwise α(x)β(y) ≤ γ(x∧y)δ(x∨y) upgrades to sums. Janson: P(X=0) ≤ exp(−μ + Δ_ord/2) = exp(−μ + Δ), Δ over unordered dependent pairs (the receipts also track the half-weighted proxy exp(−μ + Δ/2)); triangles G(n,c/n): μ → c³/6, Δ → c⁵/(4n); lower tail P(X ≤ μ−t) ≤ exp(−t²/(2(μ+Δ_ord))). Poisson paradigm: E[(X)_r] → λ^r ⟹ X → Poisson(λ); P(no triangle) → e^{−c³/6}; c = 1: e^{−1/6} ≈ 0.846. Thresholds: H appears at n^{−1/m(H)}, m(H) = max_{e(F) ≥ 1} e(F)/v(F): K₃ = C₄ = paw = 1, K₄−e = 5/4, K₄ = 3/2, K₅ = 2. Azuma: |Y_{i+1}−Y_i| ≤ cᵢ ⟹ P(|Y_n−Y₀| ≥ t) ≤ 2exp(−t²/2Σcᵢ²); vertex exposure: P(|χ−Eχ| > λ√(n−1)) < 2e^{−λ²/2}; Talagrand: P(A)·P(d_T(x,A) ≥ t) ≤ e^{−t²/4}. Evolution: isolated fraction → e^{−c}; giant ρ = 1−e^{−cρ} (ρ(1.5), ρ(2), ρ(3) = 0.583, 0.797, 0.940); connectivity P → e^{−e^{−c}}; E#C_k → c^k/2k; critical window p = 1/n + λn^{−4/3} (Bollobás 1984). Discrepancy: Hadamard ⟹ disc ≥ √n (norm argument ‖Hχ‖₂ = n); Spencer: disc ≤ 6√n (n sets, n elements); m sets: 6√(n·ln(2m/n)); Komlós conjecture: O(1) for column-normalized — open. Entropy: H(X) ≤ log|support|; chain rule H(X,Y) = H(X) + H(Y|X). Brégman: per ≤ ∏(rᵢ!)^{1/rᵢ}, equality ⟺ K_{u,u} blocks; d-regular: per ≤ (d!)^{n/d}. Van der Waerden (Egorychev–Falikman): doubly stochastic ⟹ per ≥ n!/nⁿ, equality at J/n. Moser–Tardos: e·p·(d+1) ≤ 1 ⟹ resample-until-halt terminates; witness trees are the entropy ledger.

---

## Exercises (graded: ●○○ easy · ●●○ moderate · ●●● tough)

*Hints are here; worked answers are at the end of the chapter. Try first.*

**Easy — one idea, applied directly**

1. (●○○) **Kleitman's induction.** Prove that up-sets A, B of subsets of [n] satisfy |A ∩ B| · 2ⁿ ≥ |A| · |B|. *Hint: induct on n, slicing on the last coordinate: as families over [n−1], set A₀ = {S ⊆ [n−1] : S ∈ A} and A₁ = {S ⊆ [n−1] : S ∪ {n} ∈ A}; use the up-set property to see A₀ ⊆ A₁ (and B₀ ⊆ B₁), apply the induction hypothesis to the (A₀, B₀) and (A₁, B₁) pairs, and finish with (|A₁|−|A₀|)(|B₁|−|B₀|) ≥ 0. The machine has checked every up-set pair on the 3- and 4-cubes: 400 + 28,224 ordered pairs, zero violations — you are proving the census's theorem.*
2. (●○○) **The Janson ledger for triangles.** For triangles in G(n, p), compute μ = C(n,3)p³ and Δ = C(n,2)·C(n−2,2)·p⁵ (edge-sharing pairs only), and evaluate both at p = c/n. *Hint: show Δ → c⁵/4n → 0 while μ → c³/6; then read Janson's exp(−μ + Δ) and the half-weighted proxy exp(−μ + Δ/2) in the sparse regime and say what they converge to — the machine receipts: at n = 1000, c = 1, μ = 0.166167 and Δ = 0.000249.*

**Moderate — two ideas, or one tricky step**

3. (●●○) **FKG beyond product measure.** Prove that the rank-flattened measure μ(A) = Z_N(q)^{−1}·q^{|A|}/C(N,|A|) (where Z_N(q) = Σ_{k=0}^{N} q^k normalizes) on subsets of [N] satisfies the lattice condition. *Hint: for sets A, B with intersection i and union u (so |A|+|B| = i+u), the condition reduces to C(N,|A|)·C(N,|B|) ≥ C(N,i)·C(N,u) — a log-concavity fact about binomial coefficients; the machine verified all 87,380 pairs at N ≤ 8, q = 0.37, and you may verify your key step at N = 4 by hand. Also explain (one sentence) why the first-draft μ(A) = C(N,|A|)·q^{|A|} fails — 68,210 violations, the wrong log-modularity.*
4. (●●○) **Two Lipschitz costumes.** Prove |χ(G) − χ(G−e)| ≤ 1 and |χ(G) − χ(G−v)| ≤ 1, and write Azuma's conclusion for χ(G(n,p)) in the edge-exposure and vertex-exposure costumes. *Hint: colorings restrict and extend; for the deletions, add the missing piece back with one fresh color. The census: 5,325 edge checks and 5,404 vertex-deletion checks over all graphs n ≤ 5, zero violations — your proof is the census's theorem.*
5. (●●○) **The Shamir–Spencer window.** Prove the vertex-exposure form: for G(n, p), P(|χ − Eχ| > λ√(n−1)) < 2e^{−λ²/2}. *Hint: vertex exposure gives |Y_{i+1} − Y_i| ≤ 1 with n−1 steps whose squares sum to n−1 — but care: a revealed vertex can move χ by 1, so the honest bound needs the *conditional* Lipschitz argument; the machine exhibits (G(10,½): four visited values, three dominant, against a window of seven; G(12,½): four against ±3.32) are the reality check on your theorem's generosity.*
6. (●●○) **Densities and thresholds.** Verify m(K₄) = 3/2, m(K₄−e) = 5/4, m(paw) = 1, and state the appearance threshold n^{−1/m(H)} for each. *Hint: m(H) = max_{F ⊆ H, e(F) ≥ 1} e(F)/v(F); for the paw (triangle plus pendant edge) the maximum is 4/4 — the pendant edge rides free, and the paw shares the triangle's threshold.*
7. (●●○) **The Hadamard bound, both directions of the accident.** (a) Prove that a normalized Hadamard matrix H (HHᵀ = nI, first row all ones) as a set system has disc ≥ √n for every coloring, via ‖Hχ‖₂. (b) Show that for even Hadamard order n ≥ 2, the *sliced* system (delete row and column 1) has discrepancy exactly 1. *Hint: (a) ‖Hχ‖₂² = n², so the max row beats the average n/√n; (b) the all-ones coloring gives every sliced row sum −1 — and no coloring can beat 1: the slice has odd size n − 1, so every row sum is an odd number of ±1s and cannot vanish. Note the norm argument of (a) is honestly unavailable here — the sliced rows are no longer orthogonal (the deleted column held a 1 in every row, so their pairwise inner products are −1), which is exactly why the accident can happen. Machine receipts: exact optima 2/4/4/4/6 for Sylvester-4/8/16, Paley-12/20.*
8. (●●○) **Brégman's regular corollary.** Deduce per ≤ (d!)^{n/d} for d-regular bipartite graphs from Brégman's theorem, and verify equality for disjoint unions of K_{d,d} (d ≥ 1). *Hint: all row sums equal d, so ∏(d!)^{1/d} = (d!)^{n/d}; for equality, K_{d,d} itself has per = d! = (d!)^{d/d} and the product multiplies over blocks. Census: 160 regular graphs at n ≤ 4, zero violations, 54 equalities.*
9. (●●○) **Certify the budget.** For the 10-clause 4-SAT chain of Lecture 6 (clause i = {x₂ᵢ, x₂ᵢ₊₁, x₂ᵢ₊₂, x₂ᵢ₊₃}), compute the dependency degree d_i of every clause from the variable-sharing structure, verify max e·p·(d+1) = 0.5097 ≤ 1 with p = 2⁻⁴, and predict how many resampling events a run should need. *Hint: two clauses are dependent iff they share a variable — compute, do not assume; the receipts say mean 0.81, max 4 over 100 runs.*

**Tough — several chapter ideas combined**

10. (●●●) **The flag, paid in full.** Let X be the triangle count in G(n, c/n). Show E[(X)_r] → (c³/6)^r for every fixed r, and conclude X → Poisson(c³/6), so P(no triangle) → e^{−c³/6} — at c = 1, the constant e^{−1/6} ≈ 0.846 that Chapter 4 flagged without proof. *Hint: classify ordered r-tuples of distinct triangles by their overlap components; each component with v vertices and e edges contributes p^e, and everything except the singletons is O(1/n) — the n=6 receipts (90 edge-sharing, 90 vertex-sharing, 10 disjoint pairs; E[X(X−1)] = 200p⁶ + 180p⁵) are your calibration.*
11. (●●●) **The giant's equation.** Derive ρ = 1 − e^{−cρ}: show that the fraction of vertices in the giant component of G(n, c/n) solves this fixed-point equation, and solve it for c = 1.5, 2, 3. *Hint: expose a vertex's component as a Poisson(c) branching process — a vertex is in the giant iff its exploration tree survives, and survival probability x satisfies x = 1 − e^{−cx}; by duality x = ρ. (Machine: 0.583, 0.797, 0.940; the MC at n = 1000 landed 0.5706, 0.7940, 0.9405.)*
12. (●●●) **The Gumbel law.** At p = (ln n + c)/n, show the number of isolated vertices converges to Poisson(e^{−c}) — factorial moments again — and conclude P(G(n,p) connected) → e^{−e^{−c}}. *Hint: E[#isolated] = n(1−p)^{n−1} → e^{−c}; for the r-th factorial moment, count ordered r-tuples of distinct vertices and the edges their joint isolation forbids — r(n−1) incident edges, less the C(r,2) edges among them that were counted twice — giving E[(#isolated)_r] = (n)_r·(1−p)^{r(n−1)−C(r,2)} → e^{−cr}; then argue connectivity fails only via isolated vertices (the hard direction is a theorem the lab measures: in 600 machine runs, "no isolated vertex" and "connected" coincided in every run at c = 0 and c = 1, and at c = −1 in 198 of 200 — the two exceptions disconnected graphs whose only obstructions were isolated edges, the finite-n residue that dies with n).*

**Pattern unknown — you choose the tool** *No hints here, and no difficulty rating: diagnosing the problem is part of the problem. Worked answers still wait at the end.*

13. (◆) **The budget's slack.** The symmetric Local Lemma demands e·p·(d+1) ≤ 1. Shearer's 1985 criterion (the optimal one for dependency graphs) shows this loses a factor in both p and d. Statement-level task: find the gap concretely — for the triangle as dependency graph (each event dependent on exactly the other two, p uniform), compute the largest p the symmetric condition allows, and the largest Shearer's allows (via his independence polynomial criterion at the triangle), and measure the factor between them.
14. (◆) **Azuma pays worst-case; Talagrand pays for what matters.** Statement-level task: for the longest increasing subroutine you know — the longest increasing subsequence of a random permutation (length ≈ 2√n, Baik–Deift–Johansson territory) — explain in one paragraph each why Azuma's exposure bound gives a window of the wrong order (O(√n) too wide? check: what is the exposure Lipschitz constant here?) while Talagrand's convex distance certificate argument gives the right one.
15. (◆) **Where the second moment breaks.** At the critical window p = 1/n + λn^{−4/3}, explain precisely why Chapter 4's second-moment engine (Var = o(E²)) cannot resolve the largest component's law, and why the Janson analysis of Lecture 2 also stalls — the window's width n^{−4/3} is exactly the scale at which both break; Bollobás 1984 is the citation for what replaces them.

**Explorations — ◐ research-style training** *No single right answer — what you should find is described in each.*

16. (◐) **Run the evolution.** With the lab's seeded generator, chart the giant component at n = 1000 across a fine grid of c from 0.2 to 3, and overlay the curve ρ(c) = 1 − e^{−cρ}. What you should find: agreement within a couple of points for c ≥ 1.5, a hard-to-resolve blur exactly at c = 1 (this is the critical window n^{−4/3}, showing through — push n to 2000 or 4000 and watch the blur narrow), and below c = 1 no giant at any budget — the largest component grows like log n.
17. (◐) **The Komlós landscape.** Investigate the state of the Komlós conjecture (column-normalized matrices have O(1) discrepancy): the Banaszczyk 1998 bound for the vector-balancing cousin, the Lovett–Meka 2015 algorithmic partial coloring, and what stands between those and the conjecture itself. What you should find: a precise statement of what O(1) would mean, the best current bounds (O(√log n) territory), and a clear explanation of why Hadamard examples do *not* refute it — normalization is the whole game.
18. (◐) **The boundary of the budget.** Take the Moser–Tardos lab and push the chain to the exact boundary e·p·(d+1) = 1 (adjust clause length or overlap to sit on the line), then just past it. What you should find: termination is still quick *on average* at the boundary (the LLL condition is sufficient, not necessary — the resampler is more robust than the theorem), but the variance of resampling counts explodes as you cross; construct an instance where the symmetric condition fails badly yet the resampler still halts, and one where it genuinely runs long.

---

## Computational Lab (verified)

*Six parts, one per lecture pair. Every part is seeded and reproducible: no `random` module — a Lehmer LCG (x ← 48271·x mod 2³¹−1) draws every coin, in the same pair-lexicographic order as the verifying TypeScript port that reproduced all printed rows before installation. The printed outputs are the recorded port outputs; change a seed and you get different samples, never different theorems.*

### Part 1 — The correlation census (Lecture 1)

```python
def upsets(n):                              # all up-set families on [n]
    subs = range(1 << n)
    out = []
    for fam in range(1 << (1 << n)):        # membership bitmask over subsets
        F = {s for s in subs if fam >> s & 1}
        if all((s | t) in F                 # up-closure, machine-checked
               for s in F for t in subs if (s & t) == s):
            out.append(F)
    return out

def violates(A, B, n):                     # Kleitman: |A∩B|·2ⁿ ≥ |A||B|
    return len(A & B) * (1 << n) < len(A) * len(B)

for n in (3, 4):
    U = upsets(n)
    bad = sum(violates(A, B, n) for A in U for B in U)
    print(f"n={n}: {len(U)} up-sets, {len(U)**2} pairs, violations={bad}")
```

**Verified output.** `n=3: 20 up-sets, 400 pairs, violations=0` / `n=4: 168 up-sets, 28224 pairs, violations=0`. (The Dedekind numbers 20 and 168 fall out as a by-product — the machine re-proves a sequence whose general term is famously intractable, in the only places it can.) Recorded side-run, G(5, ½): exhaustive over all 1024 graphs — P(△) = 636/1024 ≈ 0.621, P(C₄) = 476/1024 ≈ 0.465 (a C₄ is four vertices in a cyclic pattern of 4 present edges, diagonals free — the first draft accidentally required the diagonals and found K₄s instead; the lab records the scar), P(both) = 391/1024 ≈ 0.3818 against the product 0.2887: **gap +0.0931**.

**What to explore:** reverse one family's direction (A increasing, B decreasing) and watch the inequality flip, zero exceptions; then weight the graph edges (p ≠ ½) and check the gap's sign stays put — FKG says it must.

### Part 2 — FKG beyond product measure (Lecture 1)

```python
from math import comb

def lattice_ok(N, q):                      # rank-flattened mu(A) = q^|A| / C(N,|A|)
    subs = range(1 << N)
    mu = lambda S: q ** bin(S).count("1") / comb(N, bin(S).count("1"))
    bad = 0
    for A in subs:
        for B in subs:                     # mu(A^B)mu(AvB) >= mu(A)mu(B)
            i, u = A & B, A | B
            if mu(i) * mu(u) < mu(A) * mu(B) - 1e-15:
                bad += 1
    return bad

for N in (5, 6):
    print(f"N={N}: violations={lattice_ok(N, 0.37)}")
```

**Verified output.** `N=5: violations=0` / `N=6: violations=0` (1,024 and 4,096 ordered pairs in the printed loop; the receipt census covers N = 1..8, all 87,380 ordered pairs, zero violations). The first-draft measure μ(A) = C(N,|A|)·q^{|A|} — dividing by the rank size is *required*, and the census of that draft found 68,210 violations, the wrong log-modularity; the lab keeps both lines so you can watch the sign flip.

**What to explore:** push q toward 1 (the flat limit) and toward 0 (the rank-0 limit) — where does the inequality get tight? (Answer to find: at q = 1, μ is uniform and equality holds everywhere; the interesting middle is where the theorem works for free.)

### Part 3 — Janson's two regimes and the Poisson paradigm (Lecture 2)

```python
def make_rng(seed):
    state = [seed]
    def rand():
        state[0] = 48271 * state[0] % 2147483647
        return state[0] / 2147483647
    return rand

rand = make_rng(987654321)
TRIALS = 300
for n in (60, 120):
    for c in (0.5, 1, 2):
        p = c / n
        hist = [0] * 4
        for _ in range(TRIALS):
            adj = [[False]*n for _ in range(n)]
            for i in range(n):
                for j in range(i+1, n):     # one draw per pair, lexicographic
                    if rand() < p: adj[i][j] = adj[j][i] = True
            t = sum(adj[i][j] and adj[i][k] and adj[j][k]
                    for i in range(n) for j in range(i+1, n)
                    for k in range(j+1, n))
            hist[min(t, 3)] += 1
        print(n, c, hist)
```

**Verified output.** `60 0.5 [296, 4, 0, 0]` / `60 1 [250, 48, 2, 0]` / `60 2 [91, 106, 56, 47]` / `120 0.5 [294, 6, 0, 0]` / `120 1 [249, 45, 5, 1]` / `120 2 [95, 85, 68, 52]` — the tri-free columns (296/300 = 0.987, 250/300 = 0.833, 91/300 = 0.303; 294/300 = 0.980, 249/300 = 0.830, 95/300 = 0.317) against the Poisson limits e^{−c³/6} = 0.979 / 0.846 / 0.264. At n = 120, c = 1 the histogram is **0: 249, 1: 45, 2: 5, 3: 1** — L¹ distance 0.0330 from Poisson(1/6) (standard total-variation 0.0165). The Janson ledger, machine-audited: μ and Δ at G(100, ½) give the bound exponent −20212.5 + 735229.7 = +715017.2 > 0 (the half-weighted proxy exponent −20212.5 + 367614.8 just as positive) — **vacuous**; at p = 1/n, n = 100/1000/10000 the half-weighted proxy reads 0.851698/0.847010/0.846535 (and the bound exp(−μ+Δ) reads 0.852700/0.847115/0.846545), closing on e^{−1/6} = 0.846482.

**What to explore:** the c = 1 columns of Chapter 4's lab Part 2 run *below* the limit and climb; these columns (300 trials vs. that lab's 200) climb the same way. Sample the boundary c = 1 at n = 500 and watch the tri-free fraction tighten toward 0.846 from above.

### Part 4 — Exposure and the honest window (Lecture 3)

```python
def chromatic(adj, n):                     # exact chi: subset DP over color classes
    chi = [0] * (1 << n)
    for S in range(1, 1 << n):
        v = (S & -S).bit_length() - 1      # lowest vertex: its class is independent
        best = n
        stack = [(1 << v, S & ~(1 << v))]  # (independent I so far, rest)
        while stack:
            I, rest = stack.pop()
            best = min(best, chi[rest])    # stop growing: drop I, pay one color
            for u in range(v + 1, n):
                if rest >> u & 1 and not any(adj[u][t]
                        for t in range(n) if I >> t & 1):
                    stack.append((I | 1 << u, rest & ~(1 << u)))
        chi[S] = best + 1                  # chi(S) = 1 + min chi(S \ I)
    return chi[-1]
```

*(The engine above is the complete recurrence the port runs — χ(S) = 1 + min χ(S \ I) over independent I containing S's lowest vertex, memoized over the 2ⁿ subsets; at n = 12 the table is 4,096 entries and each sample colors from it. The stack may reach the same class in several growth orders — harmless under a min, and one line shorter; what the port adds is only the harness: the assertion battery, the two Lipschitz censuses, and the sampling loop.)*

**Verified output.** The census: 5,325 edge-flip checks and 5,404 vertex-deletion checks over all graphs on n = 2..5 vertices — **zero violations** of the Lipschitz property (the port's full version; the snippet above shows the engine). The concentration exhibits, 500 and 200 samples with exact χ by subset DP (assertion battery first: K₅ = 5, K₄ = 4, K₃,₃ = 2, C₅ = 3, Petersen = 3, edgeless = 1): G(10, ½) mean **3.984**, distribution **{3: 84, 4: 343, 5: 70, 6: 3}**; G(12, ½) mean **4.410**, distribution **{3: 8, 4: 107, 5: 80, 6: 5}** — four visited values in both (497/500 on 3, 4, 5 at n = 10; 187/200 on 4, 5 at n = 12), against Azuma windows of ±3.00 and ±3.32.

**What to explore:** at n = 12 run 2000 samples instead of 200 and watch the 3 and the 6 fade — then compute the window the *observed* standard deviation would certify, and compare it with Azuma's. The ratio (about a factor of 4) is the gap between worst-case exposure and reality.

### Part 5 — The evolution, live (Lecture 4)

```python
def giant(n, c, trials, seed):
    rand = make_rng(seed); p = c / n
    largest = isolated = 0.0
    for _ in range(trials):
        par, sz = list(range(n)), [1]*n     # union-find
        def find(v):
            while par[v] != v: par[v] = par[par[v]]; v = par[v]
            return v
        for i in range(n):
            for j in range(i+1, n):          # one Lehmer coin per pair
                if rand() < p:
                    a, b = find(i), find(j)
                    if a != b:
                        if sz[a] < sz[b]: a, b = b, a   # union by size
                        par[b] = a; sz[a] += sz[b]
        largest += max(sz[find(v)] for v in range(n)) / n
        isolated += sum(sz[find(v)] == 1 for v in range(n)) / n
    return largest / trials, isolated / trials
```

*(The engine above is complete — per-pair Lehmer coins, union by size, no bitmasks anywhere. What the port adds is only the separate seeded runs: connectivity at p = (ln n + c)/n, seed 20261013, and the k-cycle census at n = 500, seeds 20261015/16 — each run as its own process, a habit the receipts record.)*

**Verified output.** Giant at n = 1000, 20 samples per cell, seed 20261012: mean largest fraction **0.0112 / 0.5706 / 0.7940 / 0.9405** at c = 0.5/1.5/2/3 against ρ = 0/0.583/0.797/0.940; mean isolated fractions **0.6082 / 0.2244 / 0.1341 / 0.0500** against e^{−c} = 0.607/0.223/0.135/0.050. Connectivity at n = 400, p = (ln 400 + c)/400, 200 samples per cell, seed 20261013: connected fractions **0.070 / 0.390 / 0.755** at c = −1/0/1 against the Gumbel limits 0.0660/0.3679/0.6922 — and the no-isolated fractions (0.080/0.390/0.755) coincide with connected at c = 0 and c = 1; at c = −1 they differ by exactly two of 200 samples (0.080 vs. 0.070), both exceptions disconnected graphs whose only obstructions are isolated edges — the finite-n residue that dies with n. Cycle counts at n = 500, 200 samples, seeds 20261015/16: means **0.130/0.095/0.135** (c = 1) and **1.370/2.030/3.025** (c = 2) for k = 3/4/5, against exact finite-n 0.166/0.124/0.098 and 1.325/1.976/3.136 — the counter is the DFS enumerator certified against brute-force permutation enumeration on all 33,792 graphs on five and six vertices, and against trace(A³) = 6·#C₃, both zero-violation checks.

**What to explore:** Exploration 16 is this part's continuation — chart c from 0.2 to 3 finely and find the blur at c = 1; then push n and watch the window narrow.

### Part 6 — The ledger: discrepancy, permanents, and the resampler (Lectures 5–6)

```python
from math import factorial as fact, prod

def exact_disc(A, n):                       # Gray code over all 2^n colorings
    s = [-sum(row) for row in A]            # all-eps-minus-one start
    best = max(abs(v) for v in s)
    for g in range(1, 1 << n):
        b = (g & -g).bit_length() - 1       # the flipped coordinate
        sign = 2 if (g ^ (g >> 1)) >> b & 1 else -2
        for i in range(n): s[i] += sign * A[i][b]
        best = min(best, max(abs(v) for v in s))
    return best

def permanent(mask, n):                     # Ryser's formula via Gray code
    rows = [[(mask >> (i*n + j)) & 1 for j in range(n)] for i in range(n)]
    col_sums = [0] * n
    total = 0
    for g in range(1, 1 << n):
        b = (g & -g).bit_length() - 1
        gray = g ^ (g >> 1)
        sgn = 1 if (gray >> b) & 1 else -1
        for j in range(n):
            col_sums[j] += sgn * rows[b][j]
        term = prod(col_sums)
        total += -term if (n - bin(gray).count("1")) & 1 else term
    return total

def bregman_ok(n):                          # census: per <= prod (r_i!)^(1/r_i)
    for mask in range(1 << (n*n)):          # permanent via Ryser, defined above
        r = [bin(mask >> (i*n) & ((1 << n)-1)).count("1") for i in range(n)]
        bound = prod(fact(ri) ** (1/ri) if ri else 1 for ri in r)
        if permanent(mask, n) > bound + 1e-9:
            return False
    return True

def clause_vars(c):                        # clause c on variables 2c..2c+3
    return [2*c + l for l in range(4)]

def resample(seed, trials=100):             # the Moser-Tardos chain of Lecture 6
    rand = make_rng(seed)
    signs = [[1 if rand() < 0.5 else -1 for _ in range(4)]   # forty coins first
             for _ in range(10)]
    total = 0
    for _ in range(trials):
        val = [rand() < 0.5 for _ in range(22)]
        events = 0
        while True:
            viol = next((c for c in range(10)
                         if all(val[v] != (signs[c][l] > 0)
                                for l, v in enumerate(clause_vars(c)))), None)
            if viol is None: break
            for v in clause_vars(viol): val[v] = rand() < 0.5
            events += 1
        total += events
    return total / trials
```

**Verified output.** Discrepancy: 20 seeded instances (m = n ∈ {4, 8, 12, 16}), Gray-code exact optima **0, 2, 2, 2, 2 / 2×5 / 2×5 / 2, 2, 4, 4, 2**, all even (parity: even n forces even row sums), against Spencer's 6√n = 12.0/17.0/20.8/24.0 and a mean single-random-coloring imbalance of 3.0/4.9/6.6/8.1; the best of 10,000 random colorings equals the optimum in 18 of 20 instances. Independent re-verification: five instances (including both opt-4 outliers) re-enumerated with a naive full-recompute checker — all match; the Sylvester-4/8/16 Hadamard systems re-verified at 2/4/4. Brégman census: all **74,954** bipartite graphs with sides ≤ 4 (66,066 square) — **zero violations, 151 equality cases**, the equality set (for per(A) > 0) identical to the disjoint-K_{u,u}-components set in both directions; the regular corollary: all 160 d-regular square graphs at n ≤ 4, zero violations, 54 equalities; van der Waerden: 2,800 doubly stochastic samples (n = 2..8, Ryser permanents cross-checked against brute force on 800 random 0/1 matrices), zero violations of per ≥ n!/nⁿ, per(J/n) exact to 1e-12. The resampler, seed 20261040: **100/100 runs terminate, mean 0.81 resampling events, max 4, every final assignment satisfying all ten clauses**, under the certified budget e·p·(d+1) = 0.5097 ≤ 1 with d = [1, 2, 2, 2, 2, 2, 2, 2, 2, 1].

**What to explore:** Exploration 18 lives here — grow the chain to the boundary e·p·(d+1) = 1 and past it; the resampler keeps terminating (the condition is sufficient, not necessary) while the resampling-count variance climbs. Then break the budget honestly: a dense dependency structure with p large, and watch a genuine long run.

---

## Answers to the Exercises

*Worked answers for the twelve graded problems and the three ◆ pattern-unknown ones. The three ◐ Explorations state what you should find and get no worked answer — that is their point. Where an answer cites a machine receipt, the receipt exists: rerun the printed lab and the printed outputs match.*

**Answer 1 (Kleitman's induction).** Induct on n; the case n = 0 is one subset and equality. For an up-set A of subsets of [n], slice on the last coordinate: A₀ = {S ⊆ [n−1] : S ∈ A} and A₁ = {S ⊆ [n−1] : S ∪ {n} ∈ A}. The up-set property gives A₀ ⊆ A₁ (if S ∈ A₀ then S ∈ A, so S ∪ {n} ∈ A, so S ∈ A₁) — and likewise B₀ ⊆ B₁. Slicing commutes with intersection, ((A∩B)₀ = A₀∩B₀ and (A∩B)₁ = A₁∩B₁), and |A| = |A₀| + |A₁| because every member of A is counted by exactly one slice. Apply the hypothesis on [n−1] to both slice-pairs and add:

  |A∩B| · 2^{n−1} = (|A₀∩B₀| + |A₁∩B₁|) · 2^{n−1} ≥ |A₀||B₀| + |A₁||B₁|.

It remains to check |A₀||B₀| + |A₁||B₁| ≥ |A||B|/2 = (|A₀|+|A₁|)(|B₀|+|B₁|)/2, which after multiplying out is exactly

  (|A₁| − |A₀|)(|B₁| − |B₀|) ≥ 0,

true because both differences are nonnegative. Both factors are honest slice-growths — that is the whole proof, and the reason it deserves ink. ∎ (The machine's census — 400 + 28,224 ordered up-set pairs, zero violations — checked every instance of the theorem where it can be checked; this proof is the census's explanation.)

**Answer 2 (The Janson ledger).** μ = C(n,3)p³ counts the triangles; Δ counts the unordered *edge-sharing* pairs: choose the shared edge (C(n,2) ways) and the two remaining vertices (C(n−2,2) ways), each pair present with probability p⁵ — so Δ = C(n,2)·C(n−2,2)·p⁵ (and Δ_ord = 2Δ). At p = c/n: μ = C(n,3)c³/n³ → c³/6, while Δ = [n(n−1)/2][(n−2)(n−3)/2]·c⁵/n⁵ → c⁵/(4n) → 0. Both exp(−μ + Δ) and the half-weighted proxy exp(−μ + Δ/2) therefore converge to e^{−c³/6} — the repair bill shrinks a full order of n faster than the main term, and Janson's inequality becomes sharp in the sparse regime (receipt: at n = 1000, c = 1, μ = 0.166167, Δ = 0.000249, exp(−μ + Δ/2) = 0.847010 and exp(−μ + Δ) = 0.847115, closing on e^{−1/6} = 0.846482 by n = 10000). Contrast the dense regime of the lecture: at G(100, ½), the bound exponent −μ + Δ = +715,017.2 (the half-weighted proxy exponent −μ + Δ/2 = +367,614.8 against μ = 20,212.5) — vacuous either way. Same theorem, two worlds.

**Answer 3 (FKG beyond product measure).** For sets A, B ⊆ [N] write a = |A|, b = |B|, i = |A∩B|, u = |A∪B|, so a + b = i + u and i ≤ a, b ≤ u. The lattice condition for μ(A) = Z_N(q)^{−1}·q^{|A|}/C(N,|A|) reads

  q^{i}/C(N,i) · q^{u}/C(N,u) ≥ q^{a}/C(N,a) · q^{b}/C(N,b) ⟺ C(N,a)·C(N,b) ≥ C(N,i)·C(N,u).

The q's and Z_N(q)'s cancel (i + u = a + b) — the condition is pure binomial. Now log C(N,k) is concave in k (the standard log-concavity C(N,k)² ≥ C(N,k−1)C(N,k+1), proved by cross-cancelling factorials), and the pair (i, u) is a spreading of (a, b) with the same sum (i ≤ min(a,b), max(a,b) ≤ u). A concave function loses value under spreading: log C(N,i) + log C(N,u) ≤ log C(N,a) + log C(N,b). Exponentiate. ∎ The failure note: the first-draft μ′(A) = C(N,|A|)·q^{|A|} inverts every ratio C(N,·) in this computation — log-*sub*modular, 68,210 machine violations — because weighting by the rank size rewards exactly the spreading that concavity punishes. Flattening must divide, not multiply.

**Answer 4 (Two Lipschitz costumes).** For the edge e = uv: χ(G−e) ≤ χ(G) because a coloring of G is a coloring of G−e; and χ(G) ≤ χ(G−e)+1 because given a coloring of G−e, if u, v already differ you are done, and if not, repaint u with one fresh color. So χ(G) and χ(G−e) are within 1 either way. For the vertex: χ(G−v) ≤ χ(G) ≤ χ(G−v)+1 — restrict a coloring, or extend one by giving v a fresh color. Edge exposure: C(n,2) reveal-steps with |Y_{i+1}−Y_i| ≤ 1 (the conditional version of the edge bound) gives Azuma's

  P(|χ − Eχ| ≥ t) ≤ 2exp(−t²/(2C(n,2))),

window of order n. Vertex exposure: n − 1 live steps (the last vertex adds no information), window √(n−1) — strictly better, and the reason Shamir–Spencer wore that costume. The census (5,325 edge checks, 5,404 vertex-deletion checks, all graphs n ≤ 5, zero violations) is the small-scale license for both.

**Answer 5 (The Shamir–Spencer window).** At step i (i = 1, …, n), reveal all edges between vertex i and the higher-indexed vertices {i+1, …, n}, and let Y_i = E[χ | first i steps revealed]. The honest Lipschitz step: condition on the first i steps and compare two realizations E₀, E₁ of vertex (i+1)'s edges to {i+2, …, n}. Let G′ be the graph with all edges between vertex i+1 and {i+2, …, n} deleted (and any fixed realization on the remaining pairs); every completion E satisfies χ(G′ ∪ E) ∈ [χ(G′), χ(G′)+1] (color G′ and, if needed, give vertex i+1 one fresh color). Averaging over the still-unexposed edges among {i+2, …, n} preserves this interval of length 1, so all possible values of Y_{i+1} given the first i steps lie in an interval of length 1, and since Y_i = E[Y_{i+1} | the first i steps] is their average, |Y_{i+1} − Y_i| ≤ 1. The last step (i = n) reveals no new edges ({n+1, …, n} = ∅) and moves nothing (Y_n = Y_{n−1}), so Azuma with Σ_{i=1}^{n−1} cᵢ² = n − 1 gives

  P(|χ − Eχ| > λ√(n−1)) < 2e^{−λ²/2} — for G(n,p), every p.

The machine exhibits are the generosity report: G(10,½) visits four values in total (497/500 samples on three values 3, 4, 5) against the window's seven; G(12,½) visits four values (187/200 on 4 and 5) against ±3.32.

**Answer 6 (Densities and thresholds).** For any graph H with at least one edge, m(H) = max_{F ⊆ H, e(F) ≥ 1} e(F)/v(F) (and when H contains a cycle, m(H) ≥ 1 > 1/2, so the maximum is achieved on a subgraph with v(F) ≥ 3). K₄: the whole graph gives 6/4 = 3/2, triangles give 1 — m(K₄) = 3/2, threshold n^{−2/3}. K₄−e: 5/4 (the whole graph; its two triangles give 1), threshold n^{−4/5} — deleting one edge retards the threshold from n^{−2/3} to n^{−4/5}. The paw: the whole graph has e = 4, v = 4, ratio 1 — equal to the triangle's; the pendant edge adds edges and vertices in exactly the balancing proportion, so m(paw) = 1 and the paw rides the triangle's threshold n^{−1}. The moral: density is e/v of the *densest subgraph*, not of H — compute, never assume; and the receipt (K₃ = C₄ = paw = 1, K₄−e = 5/4, K₄ = 3/2, K₅ = 2) is machine-verified.

**Answer 7 (The Hadamard bound, both directions).** (a) For any χ ∈ {±1}ⁿ: ‖Hχ‖₂² = χᵀ(HᵀH)χ = n·χᵀχ = n². The maximum row beats the root-mean-square: max_i |(Hχ)ᵢ| ≥ ‖Hχ‖₂/√n = √n. Two lines; and since this holds for every χ, disc(full system) ≥ √n — with equality achieved by Sylvester-4 and Sylvester-16 among the classical systems (exact optima 2/4/4/4/6 for Sylvester-4/8/16, Paley-12/20, all ≥ √n, machine-exhausted over all 2ⁿ colorings). (b) Assume H has even Hadamard order n ≥ 2 (i.e., n = 2 or 4 | n; the trivial case n = 1 leaves an empty 0×0 slice). Slice off the first row and column. The all-ones coloring gives every sliced row sum −1: each remaining row is orthogonal to the all-ones first row, hence sums to 0 over all n entries, and its deleted first entry was +1. For the floor: since n ≥ 2 is even, the slice has n − 1 columns — an odd positive integer — so every sliced row sum is a sum of an odd number of ±1s: odd, in particular nonzero, so |row sum| ≥ 1 for every coloring. Floor 1, ceiling 1: disc(sliced) = 1 exactly. And the honest footnote the exercise demanded: the norm argument of (a) is *unavailable* here — the sliced rows are no longer orthogonal (the deleted column held a 1 in every row, so sliced pairwise inner products are −1; machine-checked on Sylvester-4/8/16). The accident happens precisely where the proof technique dies, and knowing which tool fails where is the actual skill.

**Answer 8 (Brégman's regular corollary).** In a d-regular bipartite graph (d ≥ 1) every row sum is d, so Brégman's ∏(rᵢ!)^{1/rᵢ} = ∏(d!)^{1/d} = (d!)^{n/d} — the product telescopes into a pure power. Equality for disjoint K_{d,d} unions (d ≥ 1, d | n): per is multiplicative over blocks, per(K_{d,d}) = d! = (d!)^{d/d}, so a union of n/d blocks has per = (d!)^{n/d} — exactly the bound. (The census's equality structure says this is the *only* shape: all 54 regular-graph equalities at n ≤ 4 are K_{d,d} unions with d ≥ 1, per the both-directions verification of Lecture 6.) Numbers from the census: 160 regular graphs n ≤ 4, zero violations; e.g. the complement of a perfect matching at n = 4, d = 3: per = 9 ≤ (3!)^{4/3} ≈ 10.90, and C₄⊕C₄: per = 4 = (2!)^{4/2}, equality.

**Answer 9 (Certify the budget).** Clause i sits on variables {x₂ᵢ, x₂ᵢ₊₁, x₂ᵢ₊₂, x₂ᵢ₊₃}. Clauses i and j share a variable iff their windows overlap: |i−j| = 1 shares exactly two variables ({x₂ᵢ₊₂, x₂ᵢ₊₃} for the forward neighbor), |i−j| ≥ 2 shares none. So clause 0 depends only on clause 1 (d₀ = 1), clause 9 only on clause 8 (d₉ = 1), and the eight interior clauses depend on two neighbors each: **d = [1, 2, 2, 2, 2, 2, 2, 2, 2, 1]**, max 2. With p = 2⁻⁴ = 0.0625: **e·p·(d+1) = e·0.0625·3 = 0.5097 ≤ 1** — the budget holds with almost a factor 2 in reserve. Prediction before running: the resampler should touch a handful of clauses per run and rarely revisit one — the ledger's expected event count under the LLL machinery is O(1), p·(number of clauses)-scale. The machine's measurement: mean 0.81 resampling events per run over 100 runs, worst run 4, no clause resampled more than twice — the prediction's shape, with honest numbers attached.

**Answer 10 (The flag, paid in full).** E[(X)_r] sums, over ordered r-tuples of distinct triangles, the probability that all are present. Group each tuple into *overlap components* (maximal groups of its triangles connected by vertex-sharing). A component of t ≥ 2 triangles on v vertices spans e edges with e ≥ v + 1 — check the cases: two triangles sharing a vertex (v = 5, e = 6), sharing an edge (v = 4, e = 5), and larger components only increase the surplus, by induction on adding a triangle that shares something. A singleton component (one triangle) has v = 3, e = 3. Now split the sum: tuples of r vertex-disjoint triangles number ≈ (n³/6)^r and contribute (n³/6)^r·(c/n)^{3r} → (c³/6)^r. Every other tuple has a non-singleton component; if its components span V vertices in total, the tuple count is O(n^V) and its probability is at most p^{V+1} (each component charges e ≥ v + 1 edges, singletons v = e), so its total contribution is O(n^V·n^{−(V+1)}) = O(1/n) → 0. Hence E[(X)_r] → (c³/6)^r for every fixed r. Factorial moments converging to λ^r force X → Poisson(λ) (the Poisson paradigm — the method of moments, valid because Poisson laws are moment-determinate): **X → Poisson(c³/6), P(no triangle) → e^{−c³/6}.** At c = 1: e^{−1/6} ≈ 0.846 — Chapter 4's flag, retired. Calibration receipts: at n = 6, ordered pairs classify as 180 edge-sharing + 200 edge-disjoint = 380, giving E[X(X−1)] = 200p⁶ + 180p⁵ (the first draft missed the 90 vertex-sharing/edge-disjoint unordered pairs, and the brute enumeration refused to confirm it — the gate at work); at n = 1000, c = 1, E[X(X−1)] = 0.02810798 against μ² = 0.02761147, ratio 1.018 → 1. One repair this answer pays for: Chapter 4's flag text rounded e^{−1/6} as ≈ 0.852; the correct rounding is 0.846 (as Chapter 4's own lab printed), and the flag's home is repaired in this edition.

**Answer 11 (The giant's equation).** Expose the component of a fixed vertex by breadth-first exploration: each reached vertex offers Bin(n−1, c/n) ≈ Poisson(c) new neighbors, and in the n → ∞ limit the exploration is a Galton–Watson branching process with Poisson(c) offspring. The process survives with probability x satisfying the fixed-point equation for extinction: q = P(extinction) = e^{−c(1−q)} (each of the Poisson(c) children must itself die out), i.e. survival x = 1 − e^{−cx}. For c ≤ 1 the survival probability is 0 — subcritical, no giant, the largest component of order log n. For c > 1, x > 0, and the fraction of vertices in the giant is the survival probability of their explorations: ρ = x, so **ρ = 1 − e^{−cρ}** (ρ = 0 is always a root; for c > 1 the positive root takes over — the equation's two roots are the phase transition, made algebraic). Solving by iteration: **ρ(1.5) = 0.583, ρ(2) = 0.797, ρ(3) = 0.940**. The machine at n = 1000, 20 samples per cell: 0.5706 / 0.7940 / 0.9405 — the equation landing on its feet, with the residuals being the critical window's honest shadow (the convergence is provably slow near c = 1).

**Answer 12 (The Gumbel law).** The r-th factorial moment of the isolated-vertex count X counts ordered r-tuples of distinct vertices, all isolated: choose them in (n)_r ways; their joint isolation forbids every edge touching any of them — r(n−1) incident edges, minus the C(r,2) edges *among* the chosen vertices that were counted twice:

  E[(X)_r] = (n)_r · (1−p)^{r(n−1) − C(r,2)}.

At p = (ln n + c)/n: (n)_r ~ n^r, and the exponent r(n−1) − C(r,2) = rn − O(1) gives (1−p)^{rn−O(1)} → e^{−cr}, the C(r,2)·p correction vanishing. So E[(X)_r] → e^{−cr} = (e^{−c})^r for every fixed r: **X → Poisson(e^{−c})**, and P(no isolated vertex) → e^{−e^{−c}}. For the finale: at this p every obstruction to connectivity other than an isolated vertex dies with probability → 1 (the theorem — Erdős–Rényi 1959/1960, Gilbert 1959; the Atlas's lab *measures* it: no-isolated and connected coincided in 598 of 600 runs across three cells — the two exceptions (c = −1, n = 400) were disconnected graphs whose only obstructions were isolated edges, the finite-n residue that dies with n), so

  **P(G(n,p) connected) → e^{−e^{−c}}** — the Gumbel law.

The machine at n = 400: 0.070 / 0.390 / 0.755 at c = −1/0/1, against the limits 0.0660 / 0.3679 / 0.6922.

**Answer 13 (◆ The budget's slack).** The triangle as dependency graph: three events, each dependent on the other two (d = 2). The symmetric condition: e·p·(d+1) ≤ 1 ⟹ p ≤ 1/(3e) ≈ **0.1226**. Shearer's criterion: the multivariate independence polynomial must stay positive on every induced subgraph; for K₃ the independent sets are ∅ and the three singletons, so the criterion reads 1 − p > 0, 1 − 2p > 0, 1 − 3p > 0 — the binding constraint is p < 1/3 ≈ **0.3333**. Tightness: on a uniform 3-point space take Aᵢ = {point i} — three mutually dependent events of probability exactly 1/3 with P(all avoided) = 0. So the gap at the triangle is a factor of **exactly e** (0.3333/0.1226 = e to machine precision), and the same computation at K₄ (d = 3: 1/4 vs 1/(4e)) shows it is no accident of small numbers: for the complete dependency graph, Shearer's optimal threshold is 1/(d+1) while the symmetric condition pays 1/(e(d+1)) — the budget's built-in e is the price of a proof that works for *every* dependency graph at once. Shearer's 1985 criterion is the exact price list; the symmetric lemma is the flat rate.

**Answer 14 (◆ Azuma vs. Talagrand on LIS).** Azuma's costume: reveal the permutation element by element; exposing one element changes the longest increasing subsequence by at most 1 (delete the element from the subsequence, or insert it — one step either way), so with n reveal-steps the window is 2exp(−t²/(2n)): order **√n**. Honest, and wrong by a power of n: the true fluctuation of LIS around its mean 2√n is of order **n^{1/6}** (Baik–Deift–Johansson 1999 — the normalized fluctuation follows the Tracy–Widom GUE law). Why Azuma cannot see this: it charges every exposure step at its worst-case cost 1, and the worst case (a revealed element moving through the *entire* optimal subsequence) is astronomically untypical — Azuma pays for exposure that almost never matters. Talagrand's convex-distance inequality pays for what is certified instead: membership in {LIS ≥ k} is witnessed by a *short certificate* — the k coordinates of one increasing subsequence — and the inequality's ℓ² bookkeeping turns that witness structure into a Gaussian tail at scale √k: applied with k ≈ 2√n, the window becomes order **n^{1/4}**. Still not n^{1/6} — Talagrand's certificate counting is not the truth either, but it is a full power of n closer, because it prices witnesses rather than exposures. The numbers at n = 10⁶: mean ≈ 2000, Azuma window ≈ 1000, Talagrand window ≈ 32, truth ≈ 10. Statement-level throughout: the Tracy–Widom theorem is far beyond this Atlas's altitude, and the answer says so.

**Answer 15 (◆ Where the second moment breaks).** Inside the window p = 1/n + λn^{−4/3}, the component structure has no scale separation. Below the window (p = c/n with fixed c < 1 — more precisely n(1−c) ≫ n^{2/3}, equivalently 1 − c ≫ n^{−1/3}), the expected number of tree components of size k is

  E[T_k] = C(n,k)·k^{k−2}·p^{k−1}·(1−p)^{k(n−k) + C(k,2) − (k−1)} ~ (n/c)·(ce^{−c})^k·k^{k−2}/k!.

Writing 1 − p = 1 − 1/n − λn^{−4/3}: the exponential decay rate per vertex k is governed by c − 1 − ln c ≈ (c−1)²/2. When c = 1 + λn^{−1/3}, this quadratic damping factor is ½λ²n^{−2/3}, which stays bounded of order O(1) for component sizes up to k ≍ n^{2/3}. Furthermore, for two candidate tree components S₁, S₂ of size k, their indicators I_{S₁}, I_{S₂} are not independent even when S₁ ∩ S₂ = ∅: knowing S₁ is an isolated component forbids all k² cross-edges between S₁ and S₂, dividing the unconditional probability by (1−p)^{k²} ≈ exp(−k²/n). As long as k ≪ n^{1/2}, (1−p)^{−k²} = 1 + o(1) and Var(T_k) = o((E[T_k])²) — the second-moment engine runs cleanly, relative fluctuations die, and E pins the truth. Inside the critical window p = 1/n + λn^{−4/3}, however, the largest components live at scale k ≍ n^{2/3}, where k²p ≍ n^{1/3} → ∞ and the covariance discount (1−p)^{−k²} ≈ e^{k²/n} explodes (even the expected count of cycles of length ℓ = tn^{1/3} carries the window's λ-dependence: E[C_ℓ] = (np)^ℓ/(2ℓ) → e^{λt}/(2ℓ), vanishing only at order n^{−1/3}), so Var(X)/(E[X])² converges to a strictly positive constant κ(λ) > 0 rather than 0. No constant is asymptotically pinned by an expectation whose relative error does not vanish — the second moment is not merely weak here, it is structurally unusable. Janson's repair stalls for the twin reason: Janson's inequality needs the dependency bill Δ to be a lower-order correction to μ (Δ ≪ μ was the sparse regime's whole gift), but at the window the component-structure events are correlated at the same scale as their means — Δ grows to μ's order, exp(−μ + Δ) degenerates, and no exponential-moment argument separates the scales, because there is no separation to exploit. What replaces them is genuinely different mathematics: Bollobás 1984 established that the window exists and has width exactly n^{−4/3}; Janson–Knuth–Łuczak–Pittal 1993 derived the limit laws inside it (component sizes rescaled by n^{−2/3}, the excursions of a Brownian motion with parabolic drift). The Atlas cites both and proves neither — the honest answer is that the window is where this chapter's two engines stop, and knowing precisely where and why they stop is the calibration the exercise asked for.

---
