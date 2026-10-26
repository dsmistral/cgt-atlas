---
name: "cgt-ch18-thresholds"
title: "Ch. 18 — Thresholds and Windows: The Phase Transition as a Theorem (A Lecture Course in the Feynman Style)"
type: "text/markdown"
---

# Chapter 18 · Thresholds and Windows

*Part of the Combinatorics & Graph Theory Atlas (the chapter map lives in the book basis).*

Chapter 13 followed a random graph through its evolution and watched structures appear one after another. This chapter is about the *shape* of each appearance. A monotone property — connectivity, say, or the appearance of a triangle — is off at p, off at p, off at p… and then, over a vanishingly short interval, it is on, on, on. The interval is the **window**. Erdős and Rényi saw the windows first (1959–1960); Bollobás and Thomason proved that every monotone property has one (1987); Friedgut and Kalai computed how narrow they must be for graph properties (1996); and Kahn and Kalai proposed — before anyone could prove it — the deepest structural statement in the subject: **a threshold is never more than a logarithmic factor away from the first-moment heuristic that a freshman can compute** (2006). Park and Pham proved it (2022, published 2024). That theorem, like Chapter 17's nibble, is one of the rare results that upgrades an entire culture of guesswork into theorems: it says that to *locate* a threshold you may count witnesses, and only the window's *width* needs deeper machinery.

The motto of the chapter, and of pattern **P44**: **the window is the theorem.** The location of a threshold is usually easy — a first moment, a union bound, an obstruction count. The theorem is what the probability *does inside the window*: whether the transition is coarse (a wide, gradual climb, like the triangle's) or sharp (a cliff, like connectivity's), and how wide the cliff is in units of its own location. This is a phenomenon-pattern in the manner of P26: the object of study is not a counting trick but a law of nature that every monotone system obeys.

The deal with the reader is the one the Atlas has enforced since Chapter 1: every number printed below was machine-verified before printing. All randomized receipts come from a single documented engine — the Lehmer generator x ← 48271·x mod (2³¹−1), seed 20261082, with integer-exact draw rules stated once per lab part — so the printed Python lab reproduces the receipts bit for bit. Where a theorem is cited rather than proved, the text says so; where a census is small enough that finite-size noise shows, the noise is printed, not hidden.

## How to read this chapter

Read with Chapters 4, 13 and 17 within reach: the probability space G(n,p) and the Poisson toolbox are Chapter 13's (Lecture 4 there is the evolution story this chapter rereads); the first-moment and union-bound instincts are Chapter 4's; and the semi-random philosophy of Chapter 17 supplies the contrast class — the nibble *builds* a structure bite by bite, while this chapter *measures* the cliff that one-shot randomness climbs. Lines marked **✎ Checkpoint** are the places to stop and predict — commit to a guess, in ink, before reading on. Exercises are graded ●○○ *easy* (one idea, applied directly), ●●○ *moderate* (two ideas, or one tricky step), ●●● *tough* (several ideas combined); ◆ **pattern unknown** problems come with no hint — diagnosing the tool is part of the problem; ◐ **Explorations** are open-ended investigations that state what you should find, not a number to match. Worked answers sit at the end; hints travel with the problems.

Notation. G(n,p) is the random graph on n labeled vertices with each edge present independently with probability p; G(n,m) is the uniform graph with exactly m edges; N = C(n,2) throughout. For a monotone (increasing) property A of graphs, **p_c** is its *critical probability*: any p with μ_p(A) = 1/2 (the choice of level 1/2 is a convention; any constant in (0,1) gives the same asymptotics). The **ε-window** T_ε(A) is the interval of p over which μ_p(A) climbs from ε to 1−ε. A property of n-vertex graphs has a **sharp threshold** if T_ε/p_c → 0 for every fixed ε, and a **coarse threshold** otherwise. Ω = {0,1}^E is the discrete cube over the edge set; for x ∈ Ω, x ∪ {e} and x ∖ {e} add or delete edge e. An edge e is **pivotal** for A at state x if x ∖ {e} ∉ A but x ∪ {e} ∈ A (for increasing A: absent, and its addition flips membership). **Inf_e(A, p)** is the **marginal influence**: the probability, over a random state y of the *other* N−1 edges (each present independently with probability p), that y ∖ {e} ∉ A while y ∪ {e} ∈ A — e's own bit is marginalized out. (This is the convention in which Russo's formula below reads dμ/dp = Σ_e Inf_e with no extra factor; the older boundary-measure convention differs by the factor p(1−p), and we use the marginal one throughout, matching the machine receipts.) Riemann p vs the process view: in the random graph process, edges arrive in a uniformly random order and **τ_A** is the hitting time of A. E_p[X] is expectation under μ_p; w.h.p. means with probability tending to 1; ln is the natural logarithm.

## The pattern map for this chapter

| Pattern | Plain language | Where it fires here |
|---------|---------------|--------------------|
| **P44 Threshold/window (this chapter's home)** | Every monotone property has a critical probability, and the *window* — where the probability actually climbs — is the real theorem: coarse or sharp, its width in units of p_c is the invariant worth knowing | All six lectures — the spine of the chapter |
| **P10 Averaging / expectation** | Some object beats the average; count and set E = 1 | L1 (the first-moment heuristic: E[#triangles] = 1 pins p = Θ(1/n) exactly); L5 (the expectation threshold q_G is the heuristic institutionalized — Kahn–Kalai–Park–Pham proves the heuristic is never off by more than a log) |
| **P13 Union bound** | P(anything bad) ≤ Σ P(one bad thing) | L1 (the obstruction side: P(not connected) ≥ P(isolated vertex) — the lower bound that makes the union bound a *threshold locator*); L3 (isolated vertices are the last obstruction standing) |
| **P4 Recurrence + induction** | Relate case n to smaller cases; evolve step by step | L2–L4 (the window obeys a differential equation in p: Russo's formula turns threshold analysis into solving dμ/dp = total influence); L6 (k-core peeling: a deletion cascade analyzed round by round) |
| **P25 Encoding** | Rename the structure so it becomes computable | L4 (a graph property becomes a monotone Boolean function on {0,1}^N — the encoding that makes influence, Fourier analysis, and the whole Boolean-functions view possible) |
| **The phase-transition kinship** (no registry ID; the survey's synthesis calls P44 "a phenomenon-pattern in the manner of P26") | Look for the moment a system changes character | Ch. 13's giant component is the *phenomenon*; P44 is the *law* (windows exist and have a width worth stating as a theorem) — the kinship this chapter rereads |
| **The Poisson paradigm** (no registry ID of its own; Ch. 13's map files it under P12) | Poisson-type approximation for rare dependent events | L1, L3, L6 (the isolated-vertex count converges to Poisson(e^{−c}) — Chapter 13 Lecture 2's paradigm, reprised as the *engine* of a threshold statement); Ex 3 |
| **P12 Random construction** | Prove existence by sampling | The backdrop: G(n,p) itself is P12's space; this chapter asks what *else* the experiment knows how to tell you |

## Lecture 1 · The Evolution, Reread as a Theorem

**The story.** Erdős and Rényi began with a question that looks like a pastime: take n vertices, flip a coin of bias p for each of the N = C(n,2) pairs, and watch what happens as p climbs from 0 to 1. Their 1959 note "On random graphs I" and the 1960 memoir "On the evolution of random graphs" report the discovery that made random graph theory a subject: structures do not appear gradually. For each structure — first edge, first triangle, first cycle, the giant component, connectivity — there is a *specific* p at which it switches from almost-never to almost-always, and the switch is fast. Erdős and Rényi wrote thresholds as *threshold functions* t(n): a property holds w.h.p. once p/t(n) → ∞ and fails w.h.p. once p/t(n) → 0. Sixty years of sharpening have replaced the two-ended function by today's cleaner objects: a **critical probability** p_c and a **window** around it.

**The setting.** A property A of graphs is **monotone increasing** if adding edges can only help: G ∈ A and G ⊆ G′ implies G′ ∈ A. ("Contains a triangle," "connected," and "has a Hamilton cycle" are monotone increasing; by contrast, "3-colorable" is monotone *decreasing*, so *non*-3-colorability is the monotone increasing side of that fence, and choosing the increasing orientation is the standard first move.) On the probability space G(n,p), monotonicity makes μ_p(A) = P(G(n,p) ∈ A) a strictly increasing polynomial in p of degree at most N for any nontrivial property (with nonnegative counts a_m = |A ∩ C(E,m)| in the Bernstein expansion Σ a_m p^m(1−p)^{N−m} and nondecreasing slice densities a_m/C(N,m), hence dμ_p(A)/dp > 0 throughout (0,1)).

**The first-moment heuristic (P10), stated precisely.** Let X count the *witnesses* of A — the small structures whose presence certifies membership. ("Contains a triangle": X = #triangles.) Then

> **First-moment threshold heuristic.** If E_p[X] → 0 then μ_p(A) → 0; if E_p[X] → ∞ **and the witnesses rarely overlap**, μ_p(A) → 1. The scale p where E_p[X] ≈ 1 is the heuristic location of the threshold.

The first half is Chapter 4's union bound (P13): P(X ≥ 1) ≤ E[X]. The second half is honest only when overlap is negligible — that is exactly the caveat this whole chapter learns to manage, and Lecture 5 will turn it into a theorem.

**✎ Checkpoint.** Before computing: for the property "contains a triangle," do you expect the transition to be *narrower* or *wider* than the transition for "connected"? Commit to a guess and a reason. (Both thresholds are computable by first moments; the surprise is that the two *windows* live on different scales. The receipts below settle it, and Lecture 2 names the scales.)

**The triangle, completely.** E[#triangles] = C(n,3)p³. Setting the count to 1 gives p³ ≈ 6/n³, i.e. **p = Θ(1/n)**, and the refined parametrization p = c/n gives

E[X] = C(n,3)(c/n)³ = (c³/6)(1 − 1/n)(1 − 2/n) → c³/6.

For fixed small c this is the whole story: P(no triangle) ≈ e^{−c³/6} when triangles are rare and nearly independent (Poisson paradigm — Chapter 13 Lecture 2's machinery; Exercise 3 does the analogous computation for isolated vertices in complete detail). So the climb of μ_p is the climb of 1 − e^{−c³/6}: from 10% to 90% as c runs from (6 ln(10/9))^{1/3} ≈ **0.858** to (6 ln 10)^{1/3} ≈ **2.400** — a c-window width of Δc ≈ 1.541 in units of 1/n (or T_0.1/p_c ≈ 1.541/1.608 ≈ 0.958 in units of p_c itself). That is a **coarse** window: it never narrows.

**Receipt (lab Part 1).** The census at n = 200 and n = 400 (100 runs per point, engine seed 20261082):

| c | 0.6 | 0.8 | 1.0 | 1.2 | 1.5 | 2.0 |
|---|-----|-----|-----|-----|-----|-----|
| P(≥1 triangle), n = 200 | 0.06 | 0.05 | 0.13 | 0.21 | 0.39 | 0.75 |
| P(≥1 triangle), n = 400 | 0.04 | 0.08 | 0.15 | 0.28 | 0.38 | 0.75 |
| theory 1 − e^{−c³/6} | 0.035 | 0.082 | 0.154 | 0.250 | 0.430 | 0.736 |

The two rows *overlay each other* — the transition curve in the variable c = np is the same at n = 200 and n = 400 (and remains so as n → ∞). The mean triangle counts (0.06…1.59 and 0.04…1.32 against the exact expectations c³/6·(1−1/n)(1−2/n), within census noise of 100 runs) confirm the Poisson scale. **A coarse window is n-independent in units of p_c.** Hold that against Part 2's cliff.

**The obstruction side (P13).** For "connected," the useful witnesses live on the *other* side: A's complement is witnessed by cuts. The cheapest cut is the isolated vertex. E[#isolated vertices] = n(1−p)^{n−1}; setting this to 1:

n(1−p)^{n−1} ≈ n·e^{−(n−1)p} ≈ 1 ⟹ **p ≈ (ln n)/n**.

The union bound's shadow — P(not A) ≥ P(one specific obstruction) — is the *lower-bound* half of a threshold argument, and it is exact here in the strongest sense: at p = (ln n + c)/n, the number of isolated vertices converges to Poisson(e^{−c}) (Exercise 3 proves it from factorial moments), and the classical Erdős–Rényi theorem — hardened by decades of sharpening, with the hitting-time form due to Bollobás and Thomason (1985) — says that at this scale, *whp the isolated vertices are the only obstruction left*: μ_p(connected) → e^{−e^{−c}}. The heuristic and the theorem agree to the additive constant in p.

**The lecture's takeaway.** Both thresholds were located by a one-line expectation count (P10) plus a one-line obstruction count (P13). What the heuristics cannot say is how *fast* the probability climbs — and that is not a detail. It is the subject of the book's newest pattern, P44: the window is the theorem.

## Lecture 2 · Windows: Coarse versus Sharp

**The definition.** For a monotone property A and 0 < ε < 1/2, let p₁ = p₁(ε) be the p with μ_p(A) = ε and p₂ the p with μ_p(A) = 1−ε. The **ε-window** is T_ε(A) = p₂ − p₁: the length of the interval across which the probability actually climbs. A sequence A_n of properties has a **sharp threshold** if T_ε(A_n)/min(p_c, 1−p_c) → 0 for every fixed ε, and a **coarse threshold** if the ratio stays bounded away from 0. (For thresholds with p_c → 0 — the random-graph case — min(p_c, 1−p_c) is just p_c: sharpness means the window is *negligible in units of the threshold's own location*.) This is the definition used by the Kalai–Safra survey of the subject, and it is the right one: it makes "sharp vs coarse" a statement about what an experimenter *sees*.

**Bollobás–Thomason (1987): windows exist.** Before 1987, "threshold function" was a property-by-property affair. Bollobás and Thomason proved the universal statement:

> **Theorem (Bollobás–Thomason).** Every nontrivial monotone property of subsets of a finite set has a threshold: the ε-window is bounded — T_ε = O(min(p_c, 1−p_c)·log(1/ε)) (the window bound as normalized in the Kalai–Safra survey; the structural content is what we use) — so for every fixed ε the window is at most a constant multiple of the threshold's scale.

*Proof (the replication-coupling half complete; the Kruskal–Katona shadow machinery cited).* First, to see why every monotone increasing property A has a bounded ε-window T_ε(A) = O(p_c) for every fixed ε ∈ (0, 1/2), take k independent draws S_1, …, S_k ∼ μ_p and form their union S = S_1 ∪ … ∪ S_k. Each ground-set element fails to appear in S with probability (1−p)^k, so S ∼ μ_q with q = 1−(1−p)^k ≤ kp. Because A is monotone increasing, if S_i ∈ A for at least one i, then S ∈ A; taking complements gives

1 − μ_{kp}(A) ≤ 1 − μ_q(A) = P(S ∉ A) ≤ P(∀i, S_i ∉ A) = (1 − μ_p(A))^k.

Applying this first with p = p₁(ε) (where μ_{p₁}(A) = ε) and k₁ = ⌈(ln 2)/ε⌉ yields 1 − μ_{k₁p₁}(A) ≤ (1−ε)^{k₁} ≤ e^{−εk₁} ≤ 1/2, so p_c ≤ k₁p₁(ε). Applying it again with p = p_c (where μ_{p_c}(A) = 1/2) and k₂ = ⌈log₂(1/ε)⌉ gives 1 − μ_{k₂p_c}(A) ≤ 2^{−k₂} ≤ ε, so p₂(ε) ≤ k₂p_c. To upgrade the lower tail from p₁(ε) ≥ (ε/ln 2)·p_c to the symmetric O(min(p_c, 1−p_c)·log(1/ε)) bound, Bollobás and Thomason invoke the Kruskal–Katona theorem on the uniform slices A_m = A ∩ C(E,m): if |A_m|/C(N,m) = C(x,m)/C(N,m), then by monotonicity the upper shadow keeps |A_{m'}|/C(N,m') ≥ C(x,m')/C(N,m') for all m' ≥ m, which makes (1 − μ_p(A))^{1/p} nonincreasing in p and yields p₂(ε) − p₁(ε) = O(min(p_c, 1−p_c)·log(1/ε)). Thus a threshold is not a folk tale; it is a universal theorem that applies to *every* monotone property at once — which is the structural foundation that the Kahn–Kalai conjecture (Lecture 5) later strengthens. ∎

**The warm-up: majority.** Before graph properties, the cleanest sharp threshold in mathematics is majority voting. Let f be majority on n bits: A = "more than half the bits are 1." An individual bit is pivotal when the other n−1 bits split exactly evenly, so (for n odd)

Inf_bit(1/2) = C(n−1, (n−1)/2)/2^{n−1} ≈ √(2/(πn)),

and the total influence is ≈ √(2n/π) — machine-checked numbers: at n = 101 the exact pivotal probability is 0.079589 per bit, total influence 8.0385 (against the approximation 8.019); at n = 1001, 0.025225 per bit, total 25.2502 (approximation 25.244). By Lecture 4's Russo formula the climb rate dμ/dp equals the total influence, so majority's window is Θ(1/√n) — sharp in units of p_c = 1/2, and *radically* sharper than any counting heuristic would suggest: no freshman expectation count produces a 1/√n. Windows are made of influence, not of expectation.

**Receipt (lab Part 2).** Connectivity, parametrized on the exact theorem curve p = (ln n + c)/n — sampled in the G(n,m) process form with m = ⌊(n/2)(ln n + c)⌋, 200 runs per point:

| c | −3 | −2 | −1 | 0 | 1 | 2 | 3 |
|----|----|----|----|----|----|----|----|
| P(connected), n = 400 | 0.000 | 0.010 | 0.050 | 0.375 | 0.695 | 0.880 | 0.945 |
| P(δ ≥ 1), n = 400 | 0.000 | 0.010 | 0.050 | 0.380 | 0.695 | 0.880 | 0.945 |
| P(connected), n = 800 | 0.000 | 0.000 | 0.055 | 0.390 | 0.660 | 0.855 | 0.940 |
| theory e^{−e^{−c}} | 0.000 | 0.001 | 0.066 | 0.368 | 0.692 | 0.873 | 0.951 |

Read the table twice. First: the census overlays e^{−e^{−c}}, and the two properties — *connected* and *minimum degree ≥ 1* — are statistically the *same event* at this scale (they agree cell for cell at n = 800; at n = 400 they differ by a single run at c = 0: one graph with no isolated vertex and a small cut — the honest finite-n residue, printed as it happened). Second, the width: theory says the 10%–90% climb happens as c runs from −ln ln 10 ≈ **−0.834** to −ln ln(10/9) ≈ **2.250**, a c-window of 3.084. Normalized by ln n/n: at n = 400 that is a relative width 3.084/ln 400 ≈ **0.515**; at n = 800, 3.084/ln 800 ≈ **0.461**. The relative width is shrinking, like 1/ln n — the same absolute window, inside a threshold that itself grows.

**The two receipts side by side.** Triangle: c-window 1.54, *relative* width Θ(1) at every n — coarse forever. Connectivity: c-window 3.08 (twice as wide in c!), yet *relative* width ~3.08/ln n → 0 — sharp. **A window can be absolutely wider and relatively narrower.** The theorem-statement worth memorizing is the relative one, and it is why this chapter exists as a chapter rather than a curiosity: P44's content is that "where does it turn on" (first moment, easy) and "how fast does it turn on" (influence machinery, a real theory) are *different questions with different answers* — and both answers are theorems.

**✎ Checkpoint.** "Contains a triangle" is coarse and "connected" is sharp. Predict before computing: is "every vertex has degree ≥ 1" (no isolated vertices) coarse or sharp? You know the receipt already — it is hiding in Part 2's table — but predict the *reason* before you check. (Answer at Lecture 4: the number of pivotal edges near p_c is what sets the width, and the isolated-vertex obstruction makes almost every edge incident to a low-degree vertex pivotal at once.)

## Lecture 3 · Hitting Times: The Process View

**The process.** Instead of fixing p, run the *random graph process*: put all N = C(n,2) possible edges in a uniformly random order and add them one at a time. G(n,m) — the m-th snapshot — is exactly the uniform graph with m edges, so the process is a way of seeing *all* the p's at once, in their natural coupling. For a monotone property A, the **hitting time** τ_A is the first m at which the snapshot lies in A. Hitting times restate every threshold question: G(n,p) is essentially G(n,m) at m ≈ pN, so a threshold location p_c ↔ m_c = p_c·N, and *two properties with the same threshold can still have different hitting-time behavior*.

**The coincidences.** The classical results here are so clean they read like accidents:

> **Theorem (Bollobás–Thomason, 1985; the k = 1 case is the Erdős–Rényi phenomenon).** In the random graph process, w.h.p. the hitting time of "minimum degree ≥ k" *equals* the hitting time of "k-connected" — for every fixed k. The last isolated vertex disappears and the graph is connected *in the same instant*; the last degree-1 vertex disappears and the graph is 2-connected in the same instant.

> **Theorem (Bollobás, 1984).** The Hamiltonicity analogue: w.h.p. the first Hamilton cycle appears at exactly the hitting time of "minimum degree ≥ 2." (The companion edge-count statement — Hamiltonicity once m ≈ (n/2)(ln n + ln ln n) — has its sharp threshold in the same paper's circle of results, with the path versions due to Ajtai–Komlós–Szemerédi (1981) and Komlós–Szemerédi (1983).)

These are *much* sharper than threshold statements. A threshold says "around p_c, connectivity turns on." A hitting-time coincidence says: at the very moment the graph loses its last isolated vertex, it is, right then, already connected — the union of the two events' windows collapses to a point. There is no interval where the graph is "no longer obstructed but not yet connected." The proofs work the ER way: show that at the window, the *only* possible obstructions are the small-degree vertices (all other cut structures have already been outrun), and that the arrival of the last few edges is oblivious to the boundary. We state the theorems and prove the k = 1 case's engine in Exercise 12 (given the Poisson tool from Exercise 3); the full-strength k ≥ 2 arguments are cited, not reproduced.

**Receipt (lab Part 3).** The process census, 200 runs per n (full Fisher–Yates shuffle of the N pairs — one draw per index, j = x mod (i+1), engine seed 20261082):

| n | τ(conn) = τ(δ≥1) | mean gap | max gap | gap census |
|---|------------------|----------|---------|------------|
| 30 | 184/200 = 92.0% | 0.52 edges | 19 | 0×184, 1×2, 2×1, 3×2, 4×3, 5×1, 7×1, 8×2, 10×2, 15×1, 19×1 |
| 50 | 177/200 = 88.5% | 1.22 edges | 24 | 0×177, 1×2, 4×2, 6×1, 7×3, 9×4, 10×2, 11×2, 13×1, 14×1, 17×2, 20×1, 24×2 |

And in all 400 runs, δ ≥ 2 arrived *strictly after* connected (400/400) — no run ever built two richly-connected halves before joining them. Read honestly: at these small n the coincidence holds ~90% of the time, not w.h.p. — the theorem is asymptotic, and the finite-n residue is exactly the rare cuts of Part 2's c = 0 cell (a graph with no isolated vertex can still fail to be connected; it just becomes vanishingly unlikely as n grows, because every non-isolated obstruction is a *cut* and cuts are outrun by the window's own width). The gap distribution's shape — 90% at exactly 0, a thin tail out to 19–24 edges — is what "the two events' windows collapse to a point" looks like on a laptop.

**Why the process view matters for P44.** The window of a property is an artifact of *re-randomizing* the experiment at each p. The process view shows the windows of several properties *stacked on one run of Nature*: nothing (edges are isolated), trees (components join), the giant component (Ch. 13's phase transition, at m = N/n), then — crowded together at the far end — δ ≥ 1, connectivity, and (a hair later) the Hamilton era. The theorem that the last two hair-thin windows coincide exactly is the sharpest statement the theory owns, and it is the natural closing image of the chapter: **thresholds are cliffs; hitting times are the cliff-edges; the theory's pride is that some cliff-edges coincide to the edge of the last edge.**

## Lecture 4 · Influences: Russo's Formula and KKL

This lecture builds the machine that measures window width. The idea is the encoding move of **P25**: a monotone graph property A on n vertices is a monotone Boolean function f: {0,1}^N → {0,1} (the input bits say which edges are present), invariant under the n! vertex relabelings. Study f with the tools of the discrete cube.

**Pivotality.** Edge e is **pivotal** at state x if flipping just e changes the verdict: x ∖ {e} ∉ A, x ∪ {e} ∈ A. The **influence** of e at p is Inf_e(p) = P_p(e pivotal) — the probability, at edge-density p, that this particular edge is the one currently holding the door shut.

> **Russo's formula (Margulis 1974; Russo 1981).** For monotone A and 0 < p < 1:
>
> dμ_p(A)/dp = Σ_e Inf_e(p) =: I_p(A), the **total influence**.

*Proof (complete).* Write μ_p(x) = Π_e μ_p(x_e), where μ_p(1) = p and μ_p(0) = 1−p for each edge's bit. Differentiate under the product:

dμ_p(A)/dp = d/dp Σ_x 1[x ∈ A] Π_e μ_p(x_e) = Σ_e Σ_x 1[x∈A]·μ_p(x)·(1[x_e=1]/p − 1[x_e=0]/(1−p)).

The inner sum factors: Σ_{x: x_e=1} 1[x∈A]μ_p(x)/p = P_p(A | e present), and likewise the subtracted term is P_p(A | e absent). So

dμ_p(A)/dp = Σ_e [ P_p(A | e present) − P_p(A | e absent) ].

Now fix e and condition on the other N−1 edges, drawn as a random y on the remaining bits. By monotonicity, the indicator 1[x ∈ A] is nondecreasing in the bit of e, so the two conditional probabilities differ exactly when y∪{e} ∈ A and y∖{e} ∉ A — the pivotal event. Hence P_p(A|e present) − P_p(A|e absent) = P_p(e pivotal) = Inf_e(p), and summing over e gives the formula. ∎ (Exercise 6 makes you run the whole computation on a 3-bit example by hand; the 10-edge machine check below certifies it exactly, including the integer identity at p = 1/2.)

The cleanest way to *feel* the formula: dμ/dp is the climb rate; the only states where raising p locally does anything are the pivotal ones; each pivotal configuration of the *other* edges contributes its own probability. The window width is then read off: μ climbs from ε to 1−ε while dp · (total influence) accumulates, so **T_ε ≈ (1−2ε)/I_{p_c}** up to constants — wide windows mean small total influence, sharp windows mean large total influence.

**Receipt (lab Part 4).** The machine check is exact, not statistical: all 2^10 = 1024 subgraphs of K₅, no randomness anywhere. For each of three monotone properties — *connected*, *contains a triangle*, *δ ≥ 1*:

| property | # states in A | Σ_e #pivotal states | Σ_{x∈A}(2|x|−10) | identity |
|----------|--------------|--------------------|------------------|----------|
| connected | 728 | 1000 | 1000 | **exact-equal** |
| triangle | 636 | 1060 | 1060 | **exact-equal** |
| δ ≥ 1 | 768 | 860 | 860 | **exact-equal** |

The third column counts the pivotal pairs (e, y) — Russo's left side at p = 1/2, where each of the nine *other* bits carries weight 2^{−9}, is pivSum·2^{−9}. The fourth column is the direct polynomial derivative: at p = 1/2 each state x ∈ A contributes 2^{−10}·2·(2|x|−10) to dμ/dp, so dμ/dp = polyDerivSum·2^{−9}. Two a priori different computations agreeing as *integers* is the receipt. At general p (0.1, 0.3, 0.5, 0.7, 0.9) the marginal influence sum matches the centered finite difference of μ_p to within 1.35×10⁻⁹ on all three properties. (Sanity bonus: 728 is the number of connected spanning subgraphs of K₅ — a classical count, now also a lab receipt.) Majority calibration: n = 101 → 0.079589 per bit, total 8.0385 (approximation 8.019); n = 1001 → 0.025225, total 25.2502 (approximation 25.244) — matching Lecture 2 and Trick Bag #8 exactly.

**KKL: not all influences can be small.** Russo turns window width into a question about total influence. The theorem that powers the entire sharp-threshold culture:

> **Theorem (Kahn–Kalai–Linial, 1988).** For any Boolean function f on m bits with μ_{1/2}(f) = 1/2, some variable has influence at least K·(log m)/m — a constant K > 0 independent of everything. (Stated in its uniform-measure form; the p-biased extension is due to Bourgain, Kahn, Kalai, Katznelson and Linial.)

The proof uses hypercontractive Fourier analysis on the discrete cube (the Bonami–Beckner inequality on the Walsh–Fourier expansion of ∂_e f) — the spectral method of Chapter 8 applied to {0,1}^m — and is outside this chapter's line of sight (flagged: cited, not proved). What the Atlas proves completely is the consequence that matters for graphs:

**Equal influences (complete).** If A is a *graph property* (invariant under vertex relabeling), then all N edge-influences are equal: the group S_n acts on vertices, hence on edges, and transitively (any edge maps to any edge); membership in A is invariant; pivotality is preserved by the action; so Inf_e(p) is constant in e. ∎ (Three lines — Exercise 7.)

> **Theorem (Friedgut–Kalai, 1996).** Every monotone graph property has a sharp threshold at any critical probability bounded away from 0 and 1: T_ε(A) ≤ C·log(1/ε)/log n.

*The derivation, complete given KKL (Exercise 8 makes you run it).* By equal influences and Russo, dμ/dp = N·Inf_e(p). KKL's p-biased form at density p ∈ [a, 1−a] gives Inf_e(p) ≥ K·μ(1−μ)·log N/N with N = C(n,2) — so dμ/dp ≥ K′·log n·μ(1−μ). Solve the differential equation: dμ/(μ(1−μ)) ≥ K′ log n dp, so log(μ/(1−μ)) climbs at rate ≥ K′ log n; the log-odds must travel from log(ε/(1−ε)) to its negative, a total of 2 log((1−ε)/ε), which costs at most (2/K′)·log((1−ε)/ε)/log n of dp. Hence T_ε ≤ C log(1/ε)/log n. ∎

The theorem is strikingly strong: at p bounded away from 0 and 1, *no* monotone graph property can dawdle — 3-colorability's failure, chromatic number crossing k, any symmetric question: the window is O(1/log n) wide, period. Its hypotheses matter and the next paragraph says what happens without them.

**The wider landscape (statements, with sources).** Margulis (1974) had already given a sharpness criterion for random subgraphs of highly connected graphs, and had the Russo formula early. Talagrand (1994) strengthened KKL to a sum-of-influences bound: under the marginal influence convention, Σ_e Inf_e(p)·log(e/(p(1−p)·Inf_e(p))) ≥ K·μ_p(A)(1−μ_p(A))/(p(1−p)·log(2/[p(1−p)])), so for p ∈ [a, 1−a], Σ_e Inf_e(p) ≥ K′·μ_p(A)(1−μ_p(A))/log(e/max_e Inf_e(p)). Friedgut (1999) — the paper with Bourgain's appendix — proved the *dichotomy*: at p bounded away from the endpoints, a monotone function with a coarse threshold is close to a **junta** — it genuinely depends on only a bounded number of coordinates (the property is approximable by a local rule). For graph properties, which are symmetric, "local rule" is a devastating restriction — hence the sharpness. This is the machinery behind the k-SAT sharpness in Lecture 6.

**✎ Checkpoint.** Now answer Lecture 2's question honestly: why is "δ ≥ 1" sharp? Compute the exact edge influence and total influence at the window p = (ln n + c)/n. A specific edge e = {u,v} is pivotal for A = {δ ≥ 1} at state y of the other N−1 edges if and only if no vertex in V ∖ {u,v} is isolated in y, and at least one of u, v has zero incident edges in y while neither remains isolated once e is added — that is, either u is isolated in y, or v is isolated in y, or both. Since u and v each have n−2 other potential incident edges, the probability that at least one of u, v has no edges in y is 2(1−p)^{n−2} − (1−p)^{2n−4} = (2+o(1))e^{−c}/n, while the conditional probability that no vertex in V ∖ {u,v} is isolated is (1+o(1))e^{−e^{−c}}. Therefore each individual edge has marginal influence Inf_e(p) = (2+o(1))·e^{−c}·e^{−e^{−c}}/n, and summing across all N = C(n,2) = (1+o(1))n²/2 edges gives the total influence I_p(A) = N·Inf_e(p) = (1+o(1))·n·e^{−c}·e^{−e^{−c}} = Θ(n), matching Russo's derivative d/dp(e^{−e^{−c}}) = n·d/dc(e^{−e^{−c}}) = n·e^{−c}·e^{−e^{−c}} — *far more* than majority's Θ(√n), handing us the window width Θ(1/n). (Equal influences makes this the per-edge scale for *every* edge, not just the lucky ones near low-degree vertices: by Exercise 7 all N edges share the same Θ(1/n) influence at the window, and the Part 2 census is the curve that fixes the constant.) Two concrete exercises sit behind the curtain: Exercise 5 derives majority's window by Chebyshev alone, and Exploration 17 connects influence spread to coarse vs. sharp voting rules.

## Lecture 5 · The Expectation Threshold: Kahn–Kalai to Park–Pham

**The heuristic, institutionalized.** Lecture 1's first-moment heuristic says: count witnesses, set E = 1, and that is where the threshold should be. It fails in both directions, and the failure modes are the story of the subject. When witnesses overlap heavily the heuristic *undershoots* (connectivity: witnesses are spanning trees, and E[#spanning trees] = 1 already at p ≈ 1/n — a factor ln n below the truth). When the witness structure is self-reinforcing it *overshoots* in spirit (the 3-core of Lecture 6: no witness count predicts it at all). Kahn and Kalai (2006) proposed the statement that tames the first failure mode forever:

> **Definitions (Kahn–Kalai).** For an increasing family A of subsets of a finite ground set, let H be the family of *minimal witnesses* (inclusion-minimal members of A), ℓ = max{|W| : W ∈ H}, and define the **expectation threshold** q = q_A by E_p[#(W ∈ H : W ⊆ S_p)] = 1, where S_p is the p-random subset. (E[#minimal witnesses contained] = 1.)
>
> **The Kahn–Kalai conjecture (2006; the Park–Pham theorem, 2022/2024).** There is a universal constant K such that for every increasing family, **p_c ≤ K·q·log ℓ.**

Note what this says: *whatever* the true threshold is, the freshman heuristic is off by at most a logarithmic factor, and the logarithm is of the *witness size* — a quantity you can read off the problem statement. Proving it took sixteen years. Jinyoung Park and Huy Tuan Pham announced the proof in April 2022 (the IAS announcement and a Quanta piece, "Elegant Six-Page Proof," appeared that week); it is published in the Journal of the American Mathematical Society 37 (2024) 235–243, arXiv:2203.17207. Their proof proceeds by downward induction on the maximum witness size ℓ in at most ⌈log₂ ℓ⌉ fragmentation rounds: instead of asking whether a single p-random set covers an entire witness S ∈ H, one samples a sprinkle W₁ ∼ μ_{Cq} and looks for the smallest uncovered residual fragment S ∖ W₁ as S ranges over H. When H is q-spread (every nonempty edge subset I is contained in at most q^{|I|} hyperedges of H, connected to the expectation threshold by Talagrand's fractional-expectation duality), a double-counting and second-moment argument on pairs (S, W₁) shows that either W₁ already leaves a witness fragment of size < ℓ/2 with probability 1 − o(1), or one can pass to a new q-spread hypergraph H′ of residual fragments whose maximum size is at most ℓ/2. Repeating this halving step ⌈log₂ ℓ⌉ times with independent sprinkles W_t ∼ μ_{Cq} uses total edge probability at most 1 − (1 − Cq)^{⌈log₂ ℓ⌉} ≤ K·q·log ℓ and reduces the residual witness size to 1, completing the proof. (Flagged sketch — the fragmentation bookkeeping and the optimization of K are the paper's.) What the theorem changed is quotable in one line: **locating a threshold is now, universally, a first-moment calculation up to a log factor; the *only* thing that can be hard about it is the window.**

**The showcase: connectivity, completely.** Minimal witnesses of connectivity are the spanning trees (Ch. 2's Prüfer world: a minimal connected spanning subgraph is a tree), so ℓ = n−1 and — by Cayley's formula and the independence of edges under μ_p — E_p[#spanning trees] = n^{n−2}p^{n−1}. Setting the count to 1:

q = n^{−(n−2)/(n−1)} = n^{−1}·n^{1/(n−1)} = (1/n)·e^{(ln n)/(n−1)} ≈ (1/n)(1 + (ln n)/n) ≈ **1/n**.

The true threshold (Exercise 3 + the ER theorem): p_c = (ln n + c*)/n with c* = −ln ln 2 ≈ **0.3665** the point where e^{−e^{−c}} = 1/2. So

p_c/q ≈ ln n — and ln ℓ = ln(n−1) ≈ ln n: **the ratio p_c/(q·log ℓ) tends to 1.** The conjecture's log factor is not an artifact; it is exactly what the simplest example needs.

**Receipt (lab Part 5).** The bisection census (400 runs per probe, G(n,m) process form, smallest m with ≥ half the runs connected):

| n | m* (median) | p̂_c = m*/N | q (spanning trees) | p̂_c/q | ln ℓ = ln(n−1) | p̂_c/(q·ln ℓ) |
|---|------------|------------|--------------------|--------|----------------|----------------|
| 12 | 15 | 0.22727 | 0.10445 | 2.176 | 2.398 | **0.907** |
| 18 | 27 | 0.17647 | 0.06585 | 2.680 | 2.833 | **0.946** |
| 24 | 41 | 0.14855 | 0.04784 | 3.105 | 3.135 | **0.990** |
| 32 | 58 | 0.11694 | 0.03495 | 3.346 | 3.434 | **0.974** |

The gap grows like ln n across a *fourfold* range of n on a laptop, and the normalized ratio sits within a few percent of 1 — the asymptotic theorem (ratio → 1) visible at n ≤ 32, with honest finite-n wobble. (For the triangle, by contrast, Exercise 11 shows p_c/q → (ln 2)^{1/3} ≈ 0.885 with ln ℓ = ln 3 ≈ 1.099 — no gap at all: when witnesses barely overlap, the first moment is *already* the answer.)

**What the conjecture does not say — the honest boundary.** Park–Pham bounds p_c *above* by K·q·log ℓ. It does not say p_c ≥ q (indeed q can exceed p_c, as the triangle shows, though p_c ≥ q/2 always holds). It does not locate *windows* — a threshold can be log-far from q and still coarse. And it does not apply to properties whose witness structure is not the point at all: the 3-core's threshold (Lecture 6) is governed by a *self-reinforcing bootstrap*, not by minimal witnesses — the Kahn–Kalai bound still holds there (witnesses exist, after all), but it is loose: the lesson of the catalog is that **there are two kinds of thresholds — witness-countable and bootstrap — and the second kind needs its own theory.**

## Lecture 6 · The Catalog: Where the Windows Are

The chapter closes with the table the whole theory exists to fill in — the threshold locations, window types, and the right tool for each. Locations are first-moment or obstruction counts (P10/P13) unless marked; window types are the theorems of Lectures 2–5; the "tool" column names the pattern that does the work.

| Property | Threshold location | Window | Tool |
|----------|--------------------|-------|------|
| contains a fixed small H (e.g. triangle, p = c/n) | n^{−1/ρ(H)}, ρ(H) = max_{F⊆H} e(F)/v(F) (the balanced density, Ch. 13 L4; triangle: ρ = 1, so p = 1/n) | **coarse** (relative width Θ(1); Part 1: c from 0.86 to 2.40 at both n) | P10 — and the Poisson paradigm (Ch. 13's L2) for the curve |
| some vertex has degree ≥ k (a k-star) | ≈ (k!/n)^{1/k}·n^{−1} (Ex 4) | **coarse** — unbalanced witness, one vertex can win alone | P10 + P13 |
| giant component emerges | p = 1/n | coarse for the *existence* question (Ch. 13 L4; the *structural* critical window p − 1/n ~ ±n^{−4/3} is the deepest object in the field — a pointer to Chapter 13's phase-transition lecture, not a P44 theorem) | the component process (Ch. 13) |
| minimum degree ≥ 1 | (ln n + c)/n | **sharp**: width 1/n (relative 1/ln n; Part 2) | P13 + the Poisson paradigm (Poisson e^{−c}) |
| connected | (ln n + c)/n — same window, same curve | **sharp** — and the hitting time *coincides* with δ ≥ 1 (L3) | obstruction count + hitting-time theorem |
| Hamilton cycle | (ln n + ln ln n)/n | sharp; hitting time coincides with δ ≥ 2 (Bollobás 1984) | the ER machinery, one level up |
| non-3-colorability (χ > 3) | at constant p — p_c(χ > 3) ∈ (0,1) | **sharp** by Friedgut–Kalai (p bounded away from 0,1 ⇒ window O(1/log n)); the *location* is not known exactly — the honest frontier | FK96 + Achlioptas–Naor: χ(G(n,d/n)) ∈ {k_d, k_d+1}, k_d = min{k : d < 2k ln k}, Ann. Math. 162 (2005) |
| k-core nonempty (k = 3) | c ≈ 3.35 in G(n, c/n) — Pittel–Spencer–Wormald 1996: an explicit constant from a fixed-point equation, not a witness count | **sharp and discontinuous in size** — the core either does not exist or is linear-sized (Part 6) | bootstrap/peeling (P4's cascade) — the second kind of threshold |
| k-SAT satisfiable (clause density α) | α_k exists; sharp for each fixed k (Friedgut 1999); α_k pinned for large k (Ding–Sly–Sun 2022); k = 2 classical (α₂ = 1) | sharp | Friedgut's junta dichotomy + the survey/the second moment |

**Receipt (lab Part 6).** The 3-core census, n = 400, 120 runs per point (engine seed 20261082, one continuous stream through the c-grid):

| c | 3.0 | 3.2 | 3.4 | 3.6 | 3.8 | 4.2 |
|---|-----|-----|-----|-----|-----|-----|
| P(3-core nonempty) | 0.033 | 0.283 | 0.725 | 0.983 | 0.992 | 1.000 |
| mean core size | 3.8 | 37.6 | 121.2 | 195.3 | 232.0 | 286.2 |

The transition sits between 3.2 and 3.6 at this n, consistent with the asymptotic PSW constant λ₃ ≈ 3.3509 (recorded from the literature, not re-derived here; the finite-n census is printed with its shift and noise). Now read the *sizes*: 3.8 → 37.6 → 121.2. There is no era of "small but nonzero" cores. When the 3-core exists it already holds a positive fraction of the vertices — the *emergence is a jump in size*, which is why no expectation count can see it: the witnesses of "3-core exists" are minimal 3-cores of every size, and their expectations conspire to be uninformative (every subgraph of minimum degree at least 3 on v vertices has at least ⌈3v/2⌉ edges, so the expected number of minimal 3-core witnesses of order v at p = c/n is bounded by C(n,v)·C(C(v,2), ⌈3v/2⌉)·p^{⌈3v/2⌉} ≤ (en/v)^v·(evc/(3n))^{3v/2} = ((e^{5/2}·c^{3/2}/3^{3/2})·√(v/n))^v, which is super-exponentially small for every v = o(n) and explodes for v = Θ(n) already at c = 3e^{−5/3} ≈ 0.567 — missing the true cascade threshold c₃ ≈ 3.3509 entirely). Peeling is a *dynamical* proof (P4): delete what fails, iterate, and track the fixed point — the threshold is where the fixed point turns nonzero, and the turn is a fold bifurcation, not a crossing.

**The phenomenon-pattern, reflected.** Chapter 13's phase transition names what one *sees* in the evolution; P44 names the law every monotone system *obeys*. The catalog shows the law's reach: coarse when witnesses are local and unbalanced (small subgraphs, stars), sharp when a global constraint fails all at once (connectivity, coloring, k-cores, SAT), bounded by first moments up to one logarithm (Park–Pham), and — the frontier — *understood at exactly the scale where the window, not the location, is the hard part*. The chapter's last word is the same as its first: the window is the theorem.

## The Trick Bag (reference card)

**The 12-row formula box.**

1. **First-moment location (P10).** Count minimal witnesses W ∈ H; the expectation-threshold scale is where E_p[#witnesses] = Σ_{W∈H} p^{|W|} ≈ 1 (for a single isomorphism type H, (#copies of H)·p^{e(H)} = 1). Triangle: C(n,3)p³ = 1 ⇒ p = 6^{1/3}/n ≈ 1.817/n.
2. **Obstruction location (P13).** For the *failure* side, count the cheapest obstruction. Isolated vertices: n(1−p)^{n−1} = 1 ⇒ p = (ln n)/n. The obstruction count is a *lower bound* on p_c; the witness count an *upper bound proxy*; when they agree up to constants you have located the threshold.
3. **Poisson curve (the Ch. 13 L2 paradigm).** At the window, rare weakly-dependent witnesses go to Poisson(λ): P(≥1 triangle) → 1 − e^{−c³/6}; P(≥1 isolated vertex) → 1 − e^{−e^{−c}}; so P(connected) → e^{−e^{−c}} — the *whole transition curve*, not just its location.
4. **Window definition.** T_ε = p₂(ε) − p₁(ε); sharp ⟺ T_ε/p_c → 0; coarse otherwise. Bollobás–Thomason: T_ε = O(min(p_c,1−p_c)·log(1/ε)) — windows exist, universally.
5. **Russo's formula.** dμ_p/dp = Σ_e Inf_e(p) (marginal influences) — the climb rate is the total influence. Proof: product rule + monotonicity turns conditional differences into pivotal events. Window ≈ (1−2ε)/I_{p_c}.
6. **KKL.** Some variable has influence ≥ K·μ(1−μ)·log m/m. Symmetric property ⇒ all influences equal ⇒ total influence ≥ K·μ(1−μ)·log m.
7. **Friedgut–Kalai window.** Graph property, p ∈ [a, 1−a]: T_ε ≤ C·log(1/ε)/log n. Derivation: Russo + KKL + solve dμ/dp ≥ K log n μ(1−μ) (the logit travels at rate ≥ K log n).
8. **Majority calibration.** Inf_bit(1/2) = C(n−1,(n−1)/2)/2^{n−1} ≈ √(2/πn); total ≈ √(2n/π) (n = 101: 8.0385 exact); window Θ(1/√n). The influence scale sets the window scale.
9. **Expectation threshold (Kahn–Kalai).** q = where E[#minimal witnesses] = 1; ℓ = max minimal-witness size. Connectivity: q = n^{−(n−2)/(n−1)} ≈ 1/n via Cayley, p_c ≈ (ln n + 0.3665)/n, ratio ≈ ln ℓ.
10. **Park–Pham.** p_c ≤ K·q·log ℓ, universally (JAMS 37 (2024) 235–243). Locating a threshold = a first-moment calculation up to one logarithm; only the window can be hard.
11. **Bootstrap thresholds (P4 cascade).** k-cores: peel (delete degree < k, iterate); threshold = fixed point of the survival curve, c₃ ≈ 3.3509 (PSW); emergence jumps in *size* (nonempty ⇒ linear-size). No witness count sees it.
12. **Hitting times.** τ(δ ≥ k) = τ(k-connected) w.h.p. (Bollobás–Thomason 1985); τ(Hamilton) = τ(δ ≥ 2) w.h.p. (Bollobás 1984). Windows that coincide to the edge.

**The scars, kept on display.** (i) The engine survived two platform memory-limit aborts and one process-deadline abort *before a single receipt existed* — the campaign's lesson, re-learned: run each lab part as its own small block, materialize no O(N²) object, and treat any abort as a full re-run (the session-81 rule); (ii) Part 6's first implementation carried an aborted half-pass that consumed engine draws — caught before printing, because the printed Python must reproduce receipts *bit for bit from a clean documented stream*; the part was re-run clean, and the stray receipts were discarded; (iii) the Part 5 bisection's first printed table carried a mis-normalized "K estimate" column (p_c/(q²·ln ℓ) — dimensionally wrong); the chapter prints the corrected p_c/(q·ln ℓ) ≈ 0.91–0.99; (iv) finite-size honesty: Part 1's mean-triangle counts at n = 200, c = 2 run +0.26 above the exact expectation (census noise of 100 runs, σ ≈ 0.12) — printed, not trimmed; Part 2's c = −2 cell shows 0.010 against theory 0.001 (two lucky graphs in 200) — the left tail is exactly where finite-n lives.

**The reading list for this chapter (all web-verified at authoring; the session-111 expansion re-verified and completed every pin below).** Erdős–Rényi, "On random graphs I," Publ. Math. Debrecen 6 (1959) 290–297, and "On the evolution of random graphs," Publ. Math. Inst. Hung. Acad. Sci. 5 (1960) 17–61. Bollobás–Thomason, "Threshold functions," Combinatorica 7 (1987) 35–38, DOI 10.1007/BF02579198. Friedgut–Kalai, "Every monotone graph property has a sharp threshold," Proc. Amer. Math. Soc. 124 (1996), no. 10, 2993–3002. Friedgut (with an appendix by Jean Bourgain), "Sharp thresholds of graph properties, and the k-sat problem," J. Amer. Math. Soc. 12 (1999) 1017–1054. Kahn–Kalai, "Thresholds and expectation thresholds," Combin. Probab. Comput. 16 (2007), no. 3, 495–502 (arXiv:math/0603218, 2006; DOI 10.1017/S0963548307008474). Park–Pham, "A proof of the Kahn–Kalai conjecture," J. Amer. Math. Soc. 37 (2024) 235–243, arXiv:2203.17207, DOI 10.1090/jams/1028 (announced April 2022). Bollobás, "The evolution of random graphs," Trans. Amer. Math. Soc. 286 (1984) 257–274. Bollobás–Thomason, "Random graphs of small order," in Random Graphs '83 (Poznań, 1983), North-Holland Math. Stud. 118 (North-Holland, 1985) 47–97. Ajtai–Komlós–Szemerédi, "The longest path in a random graph," Combinatorica 1 (1981) 1–12, DOI 10.1007/BF02579172. Margulis, "Probabilistic characteristics of graphs with large connectivity," Probl. Peredachi Inf. 10:2 (1974) 101–108. Kahn–Kalai–Linial, "The influence of variables on Boolean functions," Proc. 29th FOCS (1988) 68–80. Talagrand, "On Russo's approximate zero-one law," Ann. Probab. 22 (1994), no. 3, 1576–1587. Bourgain–Kahn–Kalai–Katznelson–Linial, "The influence of variables in product spaces," Israel J. Math. 77 (1992) 55–64. Kalai–Safra, "Threshold phenomena and influence: perspectives from mathematics, computer science, and economics," in Computational Complexity and Statistical Physics (Oxford Univ. Press, 2006) 25–60. Achlioptas–Naor, "The two possible values of the chromatic number of a random graph," Ann. Math. 162 (2005) 1335–1351. Ding–Sly–Sun, "Proof of the satisfiability conjecture for large k," Ann. Math. 196 (2022), no. 1, 1–388. Pittel–Spencer–Wormald, "Sudden emergence of a giant k-core in a random graph," J. Combin. Theory Ser. B 67 (1996), no. 1, 111–151, DOI 10.1006/jctb.1996.0036. Russo, "On the critical percolation probabilities," Z. Wahrsch. Verw. Gebiete 56 (1981) 229–237. O'Donnell, *Analysis of Boolean Functions* (Cambridge Univ. Press, 2014), Lecture 24 (the Russo–Margulis lemma).

## Exercises (graded: ●○○ easy · ●●○ moderate · ●●● tough)

**1. ●○○** A *cherry* (path of length 2) is a pair of edges sharing a vertex. Find the threshold scale for "G(n,p) contains a cherry," decide coarse vs sharp, and give the Poisson curve in the natural parametrization. *(Hint: P10 — count witnesses; then look at how many vertices can each carry one.)*

**2. ●○○** For the property "the specific edge e₀ = {1,2} is present": compute μ_p, Inf_{e₀}(p) under the marginal convention, and every other edge's influence. What is the exact ε-window, is the threshold coarse or sharp, and why does the answer *not* contradict Bollobás–Thomason? *(Hint: T_ε = (1−ε) − ε exactly; check it against the BT bound — the theorem promises existence of a window, never sharpness.)*

**3. ●●○** Let X = the number of isolated vertices in G(n, (ln n + c)/n). Show E[(X)_k] → e^{−kc} for each fixed k (factorial moments; the Poisson paradigm, Chapter 13 Lecture 2), conclude X → Poisson(e^{−c}), and derive P(δ ≥ 1) → e^{−e^{−c}}. Then explain in one sentence why this computation, plus the statement "w.h.p. no other obstruction exists at this window," yields the connectivity curve of Lecture 1. *(Hint: for the k-th factorial moment, choose the k vertices and count incident edges: k(n−k) + C(k,2) of them.)*

**4. ●●○** Find the threshold scale for "some vertex has degree ≥ 3" in G(n,p) — and compare it with the *minimum degree ≥ 3* threshold (ln n + 2 ln ln n)/n. Verify that the balanced-density prediction (with the max over subgraphs!) gives the star's location exactly, and explain why the same 3-edge local structure has two such different thresholds and windows. *(Hint: witnesses are 3-stars: n·C(n−1,3)p³ = 1. Then reread ρ(H) = max_{F⊆H} e(F)/v(F), and ask who has to win: one vertex, or all of them.)*

**5. ●●○** Majority on n bits, p = 1/2 ± t/√n. Using only Chebyshev's inequality, show that the window is O(1/√n) (both sides). Where does Chebyshev stop, and what does the central limit theorem add? *(Hint: X = #ones is Bin(n,p); bound P(X ≥ n/2) when p = 1/2 − t/√n and P(X < n/2) when p = 1/2 + t/√n.)*

**6. ●●●** Prove Russo's formula by hand on the 3-edge cube: A = "at least 2 of the 3 edges are present." Compute μ_p explicitly as a polynomial, its derivative, each edge's pivotal set, Σ Inf_e(p), and check the identity. Then reconcile with the general proof's conditioning argument. *(Hint: only 8 states; the derivative of 3p²(1−p) + p³ is the whole exercise.)*

**7. ●●○** Prove the equal-influence lemma: if A is a monotone graph property (invariant under vertex relabeling), then Inf_e(p) is the same for every edge e. Where exactly is transitivity of the edge action used? *(Hint: an explicit relabeling carries edge e to edge f; pivotality commutes with relabeling.)*

**8. ●●●** Derive the Friedgut–Kalai window from scratch, given only (i) Russo's formula, (ii) equal influences, (iii) the p-biased KKL bound Inf_e ≥ K·μ(1−μ)·log N/N at p ∈ [a, 1−a]: show T_ε ≤ C·log(1/ε)/log n. *(Hint: dμ/dp ≥ K′ log n · μ(1−μ); integrate dμ/(μ(1−μ)); the logit is the coordinate that climbs linearly.)*

**9. ●●○** Compute the expectation threshold q for connectivity from Cayley's formula, show q = n^{−(n−2)/(n−1)} ≈ (1/n)(1 + (ln n)/n), and prove the matching lower bound p_c ≥ q·2^{−1/(n−1)} — hence p_c ≈ q from below is *false* by a factor ln n, but p_c is never ≪ q. *(Hint: connectivity implies at least one spanning tree, so the indicator sits below the count: μ_p(A) ≤ E_p[#spanning trees]. Then note in one sentence why the same argument has no chance of pinning the triangle — see Ex 11.)*

**10. ●●●** Combine Exercises 3 and 9 with the Erdős–Rényi curve: show p_c = (ln n + c* + o(1))/n with c* = −ln ln 2, and conclude p_c/(q·ln ℓ) → 1 — the Kahn–Kalai log factor is *tight*: no universal bound p_c ≤ K·q·log^{1−ε} ℓ can hold. *(Hint: μ = 1/2 ⟺ e^{−e^{−c}} = 1/2; ℓ = n−1.)*

**11. ●○○** For "contains a triangle": compute q (E[#triangles] = 1), ℓ, and p_c (the 1/2-point of 1 − e^{−c³/6}), and show p_c/q → (ln 2)^{1/3} ≈ 0.885. Why is there no log gap here? *(Hint: witnesses are edge-disjoint with high probability at the window — the overlap caveat of the first-moment heuristic is vacuous.)*

**12. ●●○** The k = 1 hitting-time coincidence, with tools given. Assume (a) Exercise 3's Poisson law at m = ⌊(n/2)(ln n + c)⌋; (b) the ER component census: for every fixed c ∈ R, the number of vertices lying in components of order k with 2 ≤ k ≤ n/2 at p = (ln n + c)/n tends to 0 in probability as n → ∞ (Chapter 13's machinery — and verify it directly by bounding Σ_{k=2}^{⌊n/2⌋} C(n,k)k^{k−2}p^{k−1}(1−p)^{k(n−k)}). Prove P(τ(conn) = τ(δ ≥ 1)) → 1. *(Hint: show the two hitting times can differ only if some component of order between 2 and n/2 is present at the moment the last isolated vertex disappears, and bracket τ(δ ≥ 1) inside a window [(n/2)(ln n − ω), (n/2)(ln n + ω)].)*

**◆ 13–15. Pattern unknown — no hints, no ratings.** **13.** You are handed a monotone property by an oracle: it tells you only ℓ (the largest minimal witness) and q (the expectation threshold). What can and cannot be concluded about p_c, and about the window? Organize the answer as a table of "guaranteed / possible / impossible." **14.** A property A is decreasing (closed under edge deletion). Define its window. What does Russo's formula say, and how are the windows of A and its complement related? Work it out on "triangle-free." **15.** Without computing anything: rank the following by expected window width *in units of p_c*, and defend the ranking — then check against the receipts: "contains a triangle," "δ ≥ 1," "connected," and "E[#spanning trees] ≥ 1" (a subgraph-multiplicity question).

**◐ 16–18. Explorations — state what you should find, not a number to match.** **16.** Measure the 3-core constant yourself: run the peeling census at increasing n and watch both the crossing point and the emergence-size jump. What should happen to the crossing as n grows, and why does the *size* jump not narrow with n? (You should find the threshold pinning toward λ₃ ≈ 3.35 with the size-jump intact — and a clean explanation of why no first-moment count predicted either.) **17.** The voting analogy: an electorate of n voters, a monotone voting rule, p = each voter's probability of voting yes. When is an election "sharp"? Compute the influence scales for majority and for "the first voter decides" (a dictatorship), and find a rule whose window is *wider* than majority's. (You should find that sharpness is exactly the concentration of influence — and a pointer to the Kalai–Safra survey's opening example, Condorcet's jury theorem.) **18.** Hunt a window *wider* than the Bollobás–Thomason guarantee allows relative to p_c — or prove your hunt cannot succeed at fixed ε. Then reread T_ε's definition with ε = ε(n) shrinking: what changes? (You should find the guarantee's log(1/ε) becoming the binding constraint, and the first hint of why threshold-window questions at *moving* ε are the modern frontier.)

## Answers to the Exercises

**A1.** A cherry is witnessed by its 2 edges at a common vertex: E[#cherries] = n·C(n−1,2)·p² ~ n³p²/2, so the threshold scale is **p = √2·n^{−3/2}**, and with p = c·n^{−3/2} we get E → c²/2. The Poisson paradigm gives the full curve P(≥1 cherry) → 1 − e^{−c²/2}: from 10% to 90% as c runs from √(2 ln(10/9)) ≈ 0.459 to √(2 ln 10) ≈ 2.146 — a relative window of O(1): **coarse**. The location is exactly the balanced-density prediction n^{−1/ρ}, ρ(K₁,₂) = max(1/2, 2/3) = 2/3.

**A2.** μ_p = p, so p_c = 1/2 and T_ε = (1−ε) − ε = **1 − 2ε**: the window is a constant fraction of p_c — **coarse**, the widest a window can be relative to its location. Marginal influence of e₀: whatever the other edges do, y ∪ {e₀} ∈ A and y ∖ {e₀} ∉ A, so Inf_{e₀}(p) = 1 at every p (and Russo reads dμ/dp = 1 ✓); every other edge has influence 0. No contradiction with Bollobás–Thomason: the bound T_ε = O(min(p_c,1−p_c)·log(1/ε)) = O((1/2)log(1/ε)) is satisfied with room to spare — the theorem promises every monotone property a *window*, never a narrow one. The example is the calibration point: one edge's influence concentrated entirely in one bit is the *coarse* extreme; majority (influence spread across n bits) is the sharp one.

**A3.** Choose the k isolated vertices: (n)_k ways; the event kills all k(n−k) + C(k,2) incident edges, so E[(X)_k] = (n)_k(1−p)^{k(n−k)+C(k,2)}. At p = (ln n + c)/n: (1−p)^{k(n−k)+C(k,2)} = exp(−p·k(n−k) + O(pn·p·k)) = exp(−k(ln n + c)(1 − k/n) + o(1)), and (n)_k ~ n^k, so E[(X)_k] → n^k·n^{−k(1−k/n)}·e^{−kc(1+o(1))} → **e^{−kc}**. Poisson is determined by its factorial moments (Chapter 13 Lecture 2), so X → Poisson(e^{−c}) and P(δ ≥ 1) = P(X = 0) → **e^{−e^{−c}}**. One sentence for the upgrade: connectivity fails only through components, the Erdős–Rényi/Bollobás–Thomason component census says that at this window every non-giant component is w.h.p. a single isolated vertex, and the Poisson curve for the isolated vertices therefore *is* the connectivity curve — μ_p(connected) → e^{−e^{−c}}.

**A4.** E[#3-stars] = n·C(n−1,3)p³ ~ n⁴p³/6 = 1 gives **p = 6^{1/3}·n^{−4/3} ≈ 1.817·n^{−4/3}**. The balanced density ρ(K₁,₃) = max(1/2, 2/3, 3/4) = 3/4 gives n^{−4/3} — exactly this: the star does *not* ignore the theory; the theory's max-over-subgraphs already knows a star is internally balanced at its full 3-edge, 4-vertex scale, which makes its threshold earlier than the triangle's. The contrast: "every vertex has degree ≥ 3" lives at p = (ln n + 2 ln ln n)/n — logarithmically later still — and is sharp, because now all n vertices must succeed together: the failure probability near the threshold is governed by the count of vertices of degree ≤ 2 (E[#{v : deg(v) = 2}] ~ n·(np)²/2·e^{−np} = (1/2)e^{−c}(1+o(1)) at np = ln n + 2 ln ln n + c), and the climb happens as these rare local failures vanish within a window of width Θ(1/n). Existence thresholds (∃ a vertex) are first-moment and coarse; universality thresholds (∀ vertices) are obstruction-counted and sharp. Same 3 edges, opposite quantifier, different universe.

**A5.** Let X ~ Bin(n,p) count the number of ones. Since Var(X) = np(1−p) ≤ n/4, if p = 1/2 − t/√n with t > 0, then E[X] = n/2 − t√n and Chebyshev's inequality gives μ_p(A) = P(X ≥ n/2) = P(X − E[X] ≥ t√n) ≤ Var(X)/(t²n) ≤ (n/4)/(t²n) = 1/(4t²). Symmetrically, at p = 1/2 + t/√n, P(X < n/2) ≤ 1/(4t²). So for any ε, taking t = 1/(2√ε): at p = 1/2 − t/√n, μ ≤ ε; at p = 1/2 + t/√n, μ ≥ 1 − ε — a window of width T_ε(A) ≤ 1/√(εn) = O(1/√n) **by Chebyshev alone.** Where Chebyshev stops: it provides no matching Ω(1/√n) lower bound on the window width and does not determine the transition profile. The central limit theorem supplies both: since √Var(X) = (√n/2)(1+o(1)), at p = 1/2 + t/√n the standardized threshold sits at −2t, so μ_p(A) = P(X > n/2) → Φ(2t), pinning the exact window width at Θ(1/√n) and revealing the Gaussian error-function profile inside it. (For finite-n error bounds one invokes Berry–Esseen; the lab's Part 4 machinery is the exact finite analogue of this computation.)

**A6.** μ_p = C(3,2)p²(1−p) + p³ = 3p² − 2p³, so dμ/dp = 6p − 6p² = 6p(1−p). Edge e is pivotal exactly when the other two bits split — one present, one absent: two pivotal configurations y, each of measure p(1−p), so Inf_e(p) = 2p(1−p) (marginal convention: e's own bit integrated out), and Σ_e Inf_e = 6p(1−p) — **equal to dμ/dp, as Russo promises.** Reconciliation with the conditioning proof: P(A | e = 1) = P(the other two are not both absent) = 1 − (1−p)² = 2p − p²; P(A | e = 0) = P(both others present) = p²; the difference is 2p(1−p) = Inf_e — the conditional-difference *is* the marginal pivotal probability, which is the whole proof of Russo in one example.

**A7.** Let π be a vertex relabeling with π(e) = f (exists for every pair e, f because S_n acts transitively on edges — *that* is where transitivity enters, and only there). Since π permutes edges and A is relabeling-invariant: x ∈ A ⟺ π(x) ∈ A; moreover (x ∪ {e}) ↦ π(x) ∪ {f} and (x ∖ {e}) ↦ π(x) ∖ {f}. So e pivotal at x ⟺ f pivotal at π(x). The pushforward of μ_p under π is μ_p (the product measure is exchangeable under edge permutations), so P(e pivotal) = P(f pivotal). ∎ Three lines, one hypothesis: symmetry. It is worth saying what breaks without symmetry — Exercise 2's single-edge property has one influence equal to 1 and the rest 0, and its window is correspondingly as coarse as windows get.

**A8.** By Russo's formula (marginal convention) and equal influences (Exercise 7), dμ_p/dp = Σ_e Inf_e(p) = N·Inf_e(p). For n ≥ 3, N = C(n,2) ≥ n, so the p-biased KKL bound at p ∈ [a, 1−a] gives Inf_e(p) ≥ K·μ_p(1−μ_p)·log N/N and hence dμ_p/dp ≥ K·μ_p(1−μ_p)·log N ≥ K·μ_p(1−μ_p)·log n. Divide by μ_p(1−μ_p) and integrate p from p₁(ε) to p₂(ε) (where μ_p climbs from ε to 1−ε): the left side is ∫_ε^{1−ε} dμ/(μ(1−μ)) = [ln(μ/(1−μ))]_ε^{1−ε} = 2 ln((1−ε)/ε) < 2 ln(1/ε). Hence T_ε(A) = p₂(ε) − p₁(ε) ≤ (2/K)·ln(1/ε)/log n = **C·log(1/ε)/log n.** ∎ The coordinate that climbs at least linearly in p·log n is the logit ln(μ/(1−μ)) — which is why sharp-threshold proofs via influence always end with a logit integration, and why the constant C is honestly whatever KKL's constant hides.

**A9.** Each labeled spanning tree is present with probability p^{n−1}, independently of the others, and there are n^{n−2} of them (Cayley, Ch. 2), so E_p[#spanning trees] = n^{n−2}p^{n−1}. Setting it to 1: q = n^{−(n−2)/(n−1)} = n^{−1}·n^{1/(n−1)} = (1/n)e^{(ln n)/(n−1)} ≈ **(1/n)(1 + (ln n)/n)**. Lower bound: a connected graph contains at least one spanning tree, so the indicator of connectivity is ≤ the count of spanning trees as random variables: μ_p(A) ≤ E_p[#ST]. At p = q·2^{−1/(n−1)} the expectation is exactly 1/2, so μ ≤ 1/2 there, giving **p_c ≥ q·2^{−1/(n−1)} ≈ q** — but the *upper* comparison fails by ln n, which is the whole Kahn–Kalai phenomenon. For the triangle (Exercise 11) the indicator-below-count gives μ(triangle) ≤ E[#triangles], and both are ≈ E — the count is already the answer there; no lower-bound gap ever appears, and none is needed.

**A10.** The 1/2-point of e^{−e^{−c}} sits at e^{−c} = ln 2, i.e. c* = −ln ln 2 ≈ **0.36651** — so p_c = (ln n + c* + o(1))/n by Exercise 3's curve plus the ER component census. Meanwhile q·ln ℓ = n^{−(n−2)/(n−1)}·ln(n−1) = (ln(n−1)/n)(1 + (ln n)/(n−1) + O((ln n)²/n²)), and p_c/(q·ln ℓ) = (ln n + c* + o(1))/ln(n−1)·(1 + o(1)) → **1.** Tightness: any universal bound p_c ≤ K·q·(log ℓ)^{1−ε} would give, for this one family, ln n ≤ K(ln n)^{1−ε} — false for large n. So the exponent 1 on the logarithm cannot be improved: **the Kahn–Kalai log factor is exactly what the simplest example in the book demands.** (The receipts of lab Part 5 watch this ratio settle at 0.91–0.99 for n = 12…32.)

**A11.** For q: C(n,3)q³ = 1 ⟹ q = 6^{1/3}/n·(1+o(1)) ≈ 1.817/n, with witness size ℓ = 3. For p_c: 1 − e^{−c³/6} = 1/2 ⟹ c³ = 6 ln 2 ⟹ p_c = (6 ln 2)^{1/3}/n·(1+o(1)) ≈ 1.608/n. So **p_c/q → (ln 2)^{1/3} ≈ 0.8850** — the true threshold sits strictly below the expectation threshold. No log gap appears because the overlap caveat of the first-moment heuristic is vacuous here: two distinct triangles share an edge if and only if their union is a 4-vertex diamond K₄⁻ (5 edges), and at p = c/n the expected number of such overlapping pairs is 6·C(n,4)·p⁵ = Θ(n⁴·n^{−5}) = Θ(1/n) → 0. Thus the witness indicators are asymptotically uncorrelated, and P(X ≥ 1) → 1 − e^{−E[X]} is already exact to leading order. Where witnesses overlap heavily (spanning trees, where any two can share up to n−2 edges), the heuristic needs the ln ℓ correction. The pair Ex 9 + Ex 11 *is* the Kahn–Kalai philosophy in two worked examples.

**A12.** First, verify the component-census bound (b) at p = (ln n + c)/n: any connected component of order k (2 ≤ k ≤ n/2) contains a spanning tree (k^{k−2} choices by Cayley's formula) and has no edges to the remaining n−k vertices. By the union bound, the expected number of such components is at most Σ_{k=2}^{⌊n/2⌋} C(n,k)k^{k−2}p^{k−1}(1−p)^{k(n−k)} ≤ Σ_{k=2}^{⌊n/2⌋} (en/k)^k·k^{k−2}·((ln n + c)/n)^{k−1}·e^{−k(n−k)(ln n + c)/n}. For 2 ≤ k ≤ (ln n)², (n−k)/n = 1 − O((ln n)²/n), so the k = 2 term is O(n²·(ln n/n)·n^{−2}) = O(ln n/n) and the sum over 2 ≤ k ≤ (ln n)² is O(ln n/n). For (ln n)² < k ≤ n/2, since n−k ≥ n/2, each term is at most n·(e(ln n + c)·n^{−1/2}·e^{−c/2})^k = o(n^{−2}). Hence the expected number of components of order 2 ≤ k ≤ n/2 is O(ln n/n) → 0. Now choose ω = ω(n) → ∞ slowly (say ω = ln ln n) and set m₋ = ⌊(n/2)(ln n − ω)⌋ and m₊ = ⌈(n/2)(ln n + ω)⌉. By Exercise 3's Poisson law, P(m₋ ≤ τ(δ ≥ 1) ≤ m₊) → 1, and at m₋ the graph G(n, m₋) already consists w.h.p. of one giant component of order > n/2 together with isolated vertices (no components of order 2 ≤ k ≤ n/2). At m₋, the number of isolated vertices is I ~ Poisson(e^ω), so w.h.p. I ≤ 2e^ω = 2 ln ln n. Each subsequent edge that touches an isolated vertex chooses its other endpoint uniformly from the n−1 remaining vertices, so the conditional probability that it joins two isolated vertices rather than hitting the giant component of size n − I is at most (I−1)/(n−1) ≤ 2 ln ln n/(n−1). Across the at most I ≤ 2 ln ln n absorptions needed to eliminate all isolated vertices, the union bound shows the probability that any two isolated vertices ever merge with each other is at most (2 ln ln n)²/(n−1) → 0. Thus every isolated vertex surviving at m₋ attaches directly to the giant component, and at m* = τ(δ ≥ 1) the graph is a single connected component: P(τ(conn) = τ(δ ≥ 1)) → 1. ∎ The full Bollobás–Thomason theorem upgrades this to every fixed k and to the 2-connected/δ≥2 pairing by running the same argument one obstruction level deeper; the Hamiltonicity version (Bollobás 1984) is the same philosophy with a much harder "no other obstruction" census — the Pósa rotation machinery of Ch. 2 doing its random-graph side job.

**A13 (◆).** An oracle supplying only the maximum minimal-witness size ℓ and the expectation threshold q pins down the upper and lower scale of p_c up to a factor of O(log ℓ), and nothing about the window:

| Category | About the critical probability p_c | About the ε-window T_ε(A) |
|---|---|---|
| **Guaranteed** | (1/2)·q ≤ p_c ≤ K·q·log ℓ for a universal constant K > 0 (upper bound by Park–Pham; lower bound since μ_{q/2}(A) ≤ Σ_{W∈H}(q/2)^{|W|} ≤ (1/2)Σ_{W∈H}q^{|W|} = 1/2, strengthened to p_c ≥ q·2^{−1/ℓ} when H is ℓ-uniform). | T_ε(A) = O(min(p_c, 1−p_c)·log(1/ε)) (Bollobás–Thomason universal window bound). |
| **Possible** | p_c/q = Θ(1) with p_c < q (triangle: ℓ = 3, p_c/q → (ln 2)^{1/3} ≈ 0.8850), or p_c/q = Θ(log ℓ) achieving the full logarithmic gap (connectivity: ℓ = n−1, p_c/q ~ ln n). | Either a coarse window (T_ε/p_c = Θ(1), e.g. triangle or single-edge dictatorship) or a sharp window (T_ε/p_c → 0, e.g. connectivity, majority, or δ ≥ 1). |
| **Impossible** | p_c < q/2, or p_c/(q·log ℓ) → ∞ along any sequence of nontrivial monotone properties, or determining p_c/q up to a constant factor from (q, ℓ) alone. | Determining whether the threshold is coarse or sharp from (q, ℓ) alone: window width is governed by influence concentration across coordinates (Russo + KKL/Friedgut), whereas both the 3-star (coarse) and δ ≥ 1 (sharp, with minimal witnesses ranging from matchings of size ⌈n/2⌉ to spanning stars of size ℓ = n−1) cannot be separated in window width by (q, ℓ) alone. |

**A14 (◆).** For decreasing A, μ_p falls; define the window on the fall (p₁ = the 1−ε level, p₂ = ε). Russo: dμ/dp = −Σ_e Inf_e(p) with the same marginal pivotality (now the flip 1→0 is the damaging one). Duality, twice over. Event-complement: A increasing ⟺ A^c decreasing, so μ_p(A^c) = 1 − μ_p(A) — the two curves are vertical reflections, consequently **the windows of A and A^c have exactly equal width**, and the sharpness of one is the sharpness of the other. Cube-duality: x ↦ E ∖ x maps μ_p to μ_{1−p}, a *different* map; under it, the increasing property {x : E ∖ x is triangle-free} transitions near p = 1 − c/n (where min(p_c, 1−p_c) = 1−p_c = Θ(1/n)). For "triangle-free": μ_p(A^c) = e^{−c³/6} + o(1) at p = c/n, so its window is the exact vertical mirror of the triangle's — coarse, with the same Δc ≈ 1.541 width (T_0.1/p_c ≈ 0.958) — but the *hitting-time* picture is asymmetric in a way neither duality can see (the process destroys triangle-freeness for good, while it creates and destroys triangles for a while before one survives), which is why the process view (L3) carries strictly more information than any fixed-p statement.

**A15 (◆).** Ranking by relative window width, widest first: **"contains a triangle" (Δc ≈ 1.54, T_0.1/p_c ≈ 0.96) ≫ "δ ≥ 1" ≈ "connected" ≈ "contains a spanning tree"** — because the last two *are the same property* (a graph contains a spanning tree iff it is connected), and both are sharp with window 1/n relative-to-location 1/ln n. The defense: the triangle's witnesses are local and unbalanced (one vertex-triple can win alone) — few pivotal edges, coarse; δ ≥ 1 demands a global constraint (all vertices covered) — nearly every edge incident to the last few low-degree vertices is pivotal at once, total influence Θ(n), window 1/n. The trap in the ranking was the fourth item: "contains a spanning tree" sounds like a witness-counting property with threshold q ≈ 1/n (Ex 9), but its *true* window lives at (ln n)/n — the ranking question quietly re-derives the Kahn–Kalai gap, which is why it earned its ◆.

**A16 (◐).** What you should find: the crossing point drifts *down* toward λ₃ ≈ 3.3509 as n grows (finite-n shifts the apparent crossing up at small n — the PSW constant is an n → ∞ fixed-point statement), while the emergence-size jump does *not* soften: whenever the 3-core exists at moderate c it already holds a positive fraction of the vertices. The explanation to reach for: peeling is a *bootstrap* — the deletion cascade is self-reinforcing below threshold (each deletion triggers more) and self-limiting above it; thresholds of bootstrap type are sharp in the location *and* discontinuous in the size, and no expectation count sees either, because minimal witnesses of every size v contribute expectations at incompatible scales. Contrast the lab's Part 5: connectivity's threshold *was* first-moment-correctable up to one log; the 3-core's is not even that.

**A17 (◐).** Majority: window Θ(1/√n) — sharp, and the sharpest a symmetric rule can be at p = 1/2, because its influence is maximally spread (KKL is tight for it). Dictatorship ("voter 1 decides"): μ = p — window 1 − 2ε, constant: the *coarse* extreme; all influence concentrated in one bit. A rule wider than majority: the dictatorship is the clean example (any junta works — a rule depending on few voters has a window of constant order; Friedgut's junta theorem is the converse statement: *only* juntas have coarse windows at p away from 0 and 1). The general law to state: **an election is sharp exactly when influence is spread** — and Condorcet's jury theorem is majority's window statement avant la lettre: competence p > 1/2 fixed, error probability e^{−Ω(n)}: not a window statement but its infinite-sharpness limit. The Kalai–Safra survey opens with exactly this table and is the right next read.

**A18 (◐).** The hunt fails at fixed ε, and that failure is the lesson: for any fixed ε ∈ (0, 1/2), Bollobás–Thomason caps the window at T_ε(A) = O(min(p_c, 1−p_c)·log(1/ε)) for every monotone property, and Friedgut–Kalai sharpens this for symmetric graph properties at p_c ∈ [a, 1−a] to T_ε(A) ≤ C·log(1/ε)/log n. Thus no monotone property can have a window wider than its threshold scale at fixed ε. What changes when ε = ε(n) → 0: the log(1/ε(n)) factor grows with n and the cap loosens — for ε(n) = e^{−√n}, the Bollobás–Thomason bound permits a window of width O(min(p_c, 1−p_c)·√n) — and the *meaning* of the window at vanishing ε becomes the modern structural question. For the giant component, the structural critical window p − 1/n = Θ(n^{−4/3}), inside which the largest components have order Θ(n^{2/3}), is precisely a statement about a moving scale where the macroscopic emergence is still undecided. That marks the boundary of P44: the fixed-ε window theory is governed by Bollobás–Thomason (existence), Friedgut–Kalai (sharpness), and Kahn–Kalai/Park–Pham (location), while scaling windows at n-dependent tails belong to the fine phase-transition theory of Chapter 13.

## Computational Lab (verified)

**The engine (all parts).** A single documented generator, the Lehmer/MINSTD linear congruential engine, ported to whatever machine is at hand:

```python
M31 = 2147483647            # 2^31 - 1 (a Lehmer prime)
x = 20261082                 # session seed
def nxt():
    """One engine draw: x <- 48271*x mod (2^31-1)."""
    global x
    x = (48271 * x) % M31
    return x
```

Every randomized decision below is **integer-exact** — no floating-point draw ever gates an edge — so the receipts reproduce bit for bit: an edge at density p = k/(10n) is present iff `nxt()*(10*n) < k*M31`; a uniform index in range(N) is `nxt() % N`; the Fisher–Yates shuffle draws exactly one index per loop position. Each randomized lab part (part1, part2, part3, part5, part6) resets the engine to the seed 20261082 at the start of the function and runs one continuous stream through its grid. Part 4 uses no randomness at all — it is an exhaustive enumeration. The receipts printed under each part are the actual verified outputs of the campaign that authored this chapter; your machine reproduces them exactly.

### Part 1 — The triangle window: a coarse threshold (Lectures 1–2)

```python
import math
def part1():
    global x
    x = 20261082
    for n in (200, 400):
        if n < 3:
            raise ValueError("n must be >= 3")
        for c in (0.6, 0.8, 1.0, 1.2, 1.5, 2.0):
            k = round(10*c); den = 10*n; thr = k*M31   # p = k/(10n) = c/n
            with_tri = 0; tri_sum = 0
            for r in range(100):
                adj = [set() for _ in range(n)]; tri = 0
                for i in range(n):
                    for j in range(i+1, n):
                        if nxt()*den < thr:
                            tri += len(adj[i] & adj[j])
                            adj[i].add(j); adj[j].add(i)
                if tri: with_tri += 1
                tri_sum += tri
            print(n, c, with_tri/100, round(tri_sum/100, 2),
                  round(1 - math.exp(-c*c*c/6), 3))
```

**Receipts** (frac with ≥1 triangle · mean triangles · theory 1 − e^{−c³/6}): n = 200: c = 0.6 → **0.06 · 0.06 · 0.035**; 0.8 → 0.05 · 0.05 · 0.082; 1.0 → 0.13 · 0.14 · 0.154; 1.2 → 0.21 · 0.24 · 0.250; 1.5 → 0.39 · 0.53 · 0.430; 2.0 → 0.75 · 1.59 · 0.736. n = 400: 0.04 · 0.04; 0.08 · 0.08; 0.15 · 0.15; 0.28 · 0.33; 0.38 · 0.48; 0.75 · 1.32. The two c-curves overlay each other and the Poisson theory (mean expectation exact: c³/6·(1−1/n)(1−2/n)) — the transition in the variable c = np does not narrow with n. Theory window: 10% at c = 0.8582, 90% at c = 2.3995: c-width **1.5413** (T_0.1/p_c ≈ 0.9584), coarse at every n.

### Part 2 — The connectivity window: a sharp threshold (Lectures 1–3)

Sampled in the G(n,m) process form; m = ⌊(n/2)(ln n + c)⌋ (the printed m values are the canonical integers: n = 400 → 598, 798, 998, 1198, 1398, 1598, 1798; n = 800 → 1473, 1873, 2273, 2673, 3073, 3473, 3873).

```python
def part2():
    global x
    x = 20261082
    for n in (400, 800):
        if n < 3:
            raise ValueError("n must be >= 3")
        N = n*(n-1)//2
        rowstart = [i*(2*n-i-1)//2 for i in range(n)]
        def decode(e):                    # edge index -> (i, j)
            lo, hi = 0, n-1
            while lo < hi:
                mid = (lo + hi + 1)//2
                if rowstart[mid] <= e: lo = mid
                else: hi = mid - 1
            return lo, e - rowstart[lo] + lo + 1
        for c in (-3, -2, -1, 0, 1, 2, 3):
            m = int(0.5*n*(math.log(n) + c))
            conn = 0; deg1 = 0
            for r in range(200):
                seen = [False]*N; es = []
                while len(es) < m:         # rejection sampler: draw j = x mod N
                    j = nxt() % N         # until unseen; rejected draws consumed
                    if not seen[j]:
                        seen[j] = True; es.append(j)
                par = list(range(n)); deg = [0]*n
                def find(a):
                    while par[a] != a:
                        par[a] = par[par[a]]; a = par[a]
                    return a
                for e in es:
                    i, j = decode(e); deg[i] += 1; deg[j] += 1
                    ri, rj = find(i), find(j)
                    if ri != rj: par[ri] = rj
                comps = sum(1 for v in range(n) if find(v) == v)
                if comps == 1: conn += 1
                if min(deg) >= 1: deg1 += 1
            print(n, m, c, conn/200, deg1/200, round(math.exp(-math.exp(-c)), 3))
```

**Receipts** (frac connected · frac δ≥1 · theory e^{−e^{−c}}): n = 400: c = −3 → **0.000 · 0.000 · 0.000**; −2 → 0.010 · 0.010 · 0.001; −1 → 0.050 · 0.050 · 0.066; 0 → 0.375 · 0.380 · 0.368; 1 → 0.695 · 0.695 · 0.692; 2 → 0.880 · 0.880 · 0.873; 3 → 0.945 · 0.945 · 0.951. n = 800: 0.000·0.000; 0.000·0.000; 0.055·0.055; 0.390·0.390; 0.660·0.660; 0.855·0.855; 0.940·0.940 (same theory row). Connected and δ≥1 agree cell for cell at n = 800; at n = 400 exactly one run (at c = 0) separates them — a graph with no isolated vertex and a small cut, the honest finite-n residue. Theory window: 10% at c = −0.8340, 90% at 2.2504: c-width 3.0844 — but *relative* width 3.0844/ln n = **0.515** (n = 400), **0.461** (n = 800): sharp, and shrinking like 1/ln n.

### Part 3 — Hitting times: the coincidences, censused (Lecture 3)

```python
def part3():
    global x
    x = 20261082
    for n in (30, 50):
        if n < 3:
            raise ValueError("n must be >= 3")
        N = n*(n-1)//2
        rowstart = [i*(2*n-i-1)//2 for i in range(n)]
        equal = 0; gap_census = {}; d2_after = 0
        for r in range(200):
            ord_ = list(range(N))
            for i in range(N-1, 0, -1):   # Fisher-Yates: one draw per index,
                j = nxt() % (i+1)          # j = x mod (i+1)
                ord_[i], ord_[j] = ord_[j], ord_[i]
            par = list(range(n)); deg = [0]*n
            def find(a):
                while par[a] != a:
                    par[a] = par[par[a]]; a = par[a]
                return a
            comps = n; t1 = tc = t2 = -1
            for t in range(N):
                e = ord_[t]
                lo, hi = 0, n-1
                while lo < hi:
                    mid = (lo + hi + 1)//2
                    if rowstart[mid] <= e: lo = mid
                    else: hi = mid - 1
                i = lo; j = e - rowstart[lo] + lo + 1
                deg[i] += 1; deg[j] += 1
                ri, rj = find(i), find(j)
                if ri != rj: par[ri] = rj; comps -= 1
                if t1 < 0 and min(deg) >= 1: t1 = t
                if t2 < 0 and min(deg) >= 2: t2 = t
                if tc < 0 and comps == 1:   tc = t
            gap = tc - t1
            equal += (gap == 0)
            gap_census[gap] = gap_census.get(gap, 0) + 1
            d2_after += (t2 > tc)
        mean_gap = round(sum(k*v for k, v in gap_census.items())/200, 2)
        print(n, equal/200, mean_gap, max(gap_census),
              sorted(gap_census.items()), d2_after/200)
```

**Receipts:** n = 30: equal **184/200 = 0.920**, mean gap **0.52**, max gap 19, census {0: 184, 1: 2, 2: 1, 3: 2, 4: 3, 5: 1, 7: 1, 8: 2, 10: 2, 15: 1, 19: 1}, δ≥2 strictly after connected **200/200**. n = 50: equal **177/200 = 0.885**, mean gap **1.22**, max gap 24, census {0: 177, 1: 2, 4: 2, 6: 1, 7: 3, 9: 4, 10: 2, 11: 2, 13: 1, 14: 1, 17: 2, 20: 1, 24: 2}, δ≥2 after connected **200/200**. The coincidence holds ~90% at laptop scale — the theorem is asymptotic, and the thin tail of positive gaps is the finite-n cut residue of Part 2's c = 0 cell.

### Part 4 — Russo's formula, exactly (Lecture 4)

No randomness: all 1024 subgraphs of K₅ enumerated, plus exact majority-voting influence calibration at n = 101 and n = 1001.

```python
import math
from itertools import product
def part4(n=5):
    if n < 3:
        raise ValueError("n must be >= 3")
    edges = [(i, j) for i in range(n) for j in range(i+1, n)]
    m = len(edges)                          # 10
    def inA(s, prop):
        deg = [0]*n; par = list(range(n))
        def find(a):
            while par[a] != a:
                par[a] = par[par[a]]; a = par[a]
            return a
        for e in range(m):
            if (s >> e) & 1:
                i, j = edges[e]; deg[i] += 1; deg[j] += 1
                ri, rj = find(i), find(j)
                if ri != rj: par[ri] = rj
        if prop == 'tri':
            for (a, b) in edges:
                if (s >> edges.index((a, b))) & 1:
                    for w in range(n):
                        if w not in (a, b):
                            ea = edges.index((min(a,w), max(a,w)))
                            eb = edges.index((min(b,w), max(b,w)))
                            if ((s >> ea) & 1) and ((s >> eb) & 1):
                                return True
            return False
        if prop == 'd1': return min(deg) >= 1
        return len([v for v in range(n) if find(v) == v]) == 1
    for prop in ('conn', 'tri', 'd1'):
        A = [inA(s, prop) for s in range(1 << m)]
        piv = sum(1 for s in range(1 << m) for e in range(m)
                  if not ((s >> e) & 1) and not A[s] and A[s | (1 << e)])
        card = sum(A)
        polyd = sum(2*bin(s).count('1') - m for s in range(1 << m) if A[s])
        # Russo check at general p: marginal influence vs centered difference
        def mu(p):  return sum(p**bin(s).count('1') *
                               (1-p)**(m-bin(s).count('1')) for s in range(1<<m) if A[s])
        def infl(p):
            return sum(p**bin(s).count('1') *
                       (1-p)**(m-1-bin(s).count('1'))
                       for s in range(1 << m) for e in range(m)
                       if not ((s >> e) & 1) and not A[s] and A[s | (1 << e)])
        h = 1e-5
        print(prop, card, piv, polyd, piv == polyd,
              [round(infl(p) - (mu(p+h)-mu(p-h))/(2*h), 12)
               for p in (0.1, 0.3, 0.5, 0.7, 0.9)])
    # Majority voting influence calibration (Lecture 2)
    for nb in (101, 1001):
        piv_b = math.comb(nb - 1, (nb - 1)//2) / (2**(nb - 1))
        print("maj", nb, round(piv_b, 6), round(nb*piv_b, 4),
              round(math.sqrt(2*nb/math.pi), 3))
```

**Receipts:** connected: |A| = **728**, pivotal pairs **1000**, polynomial-derivative sum **1000** — exact-equal integers (Russo at p = 1/2 says both sides equal pivSum·2^{−9}). Triangle: |A| = 636, **1060 = 1060**. δ≥1: |A| = 768, **860 = 860**. At p = 0.1/0.3/0.5/0.7/0.9 the marginal influence sum minus the centered derivative is ≤ **1.35×10⁻⁹** in absolute value on all three properties (finite-difference truncation O(h²), not engine error — this part has no engine). Sanity: 728 = the number of connected spanning subgraphs of K₅, the classical count.

### Part 5 — Expectation threshold vs true threshold (Lecture 5)

```python
def part5():
    global x
    x = 20261082
    for n in (12, 18, 24, 32):
        if n < 3:
            raise ValueError("n must be >= 3")
        N = n*(n-1)//2
        rowstart = [i*(2*n-i-1)//2 for i in range(n)]
        def connected(mm):
            seen = [False]*N; cnt = 0
            par = list(range(n))
            def find(a):
                while par[a] != a:
                    par[a] = par[par[a]]; a = par[a]
                return a
            while cnt < mm:
                j = nxt() % N
                if not seen[j]:
                    seen[j] = True; cnt += 1
                    lo, hi = 0, n-1
                    while lo < hi:
                        mid = (lo + hi + 1)//2
                        if rowstart[mid] <= j: lo = mid
                        else: hi = mid - 1
                    i = lo; jj = j - rowstart[lo] + lo + 1
                    ri, rj = find(i), find(jj)
                    if ri != rj: par[ri] = rj
            return len([v for v in range(n) if find(v) == v]) == 1
        lo, hi = 1, N                    # bisection: smallest m with >= 200/400
        while lo < hi:
            mid = (lo + hi)//2
            c = sum(connected(mid) for _ in range(400))
            if c >= 200: hi = mid
            else: lo = mid + 1
        q = n**(-(n-2)/(n-1))
        print(n, lo, round(lo/N, 5), round(q, 5), round(lo/N/q, 3),
              round(lo/N/q/math.log(n-1), 3))
```

**Receipts:** n = 12: m* = **15**, p̂_c = 0.22727, q = 0.10445, ratio 2.176, p̂_c/(q·ln ℓ) = **0.907**; n = 18: m* = 27, 0.17647, 0.06585, 2.680, **0.946**; n = 24: m* = 41, 0.14855, 0.04784, 3.105, **0.990**; n = 32: m* = 58, 0.11694, 0.03495, 3.346, **0.974**. The Kahn–Kalai gap grows like ln n across the table, and the normalized ratio sits near 1 — the asymptotic tightness of Lecture 5 visible at n ≤ 32, with honest quantization wobble (N is as small as 66 at n = 12; one unit of m moves p̂_c by 1.5%).

### Part 6 — The 3-core: a bootstrap threshold (Lecture 6)

One continuous engine stream through the c-grid, started fresh at the seed *before the grid begins*; p = k/(100n) with k = round(100c).

```python
def part6(n=400):
    global x
    x = 20261082
    if n < 3:
        raise ValueError("n must be >= 3")
    N = n*(n-1)//2
    den = 100*n
    for c in (3.0, 3.2, 3.4, 3.6, 3.8, 4.2):
        k = round(100*c); thr = k*M31
        nonempty = 0; size_sum = 0; m_sum = 0
        for r in range(120):
            eu = []; ev = []
            for i in range(n):
                for j in range(i+1, n):
                    if nxt()*den < thr:
                        eu.append(i); ev.append(j)
            m = len(eu); m_sum += m
            off = [0]*(n+1)
            for e in range(m):
                off[eu[e]+1] += 1; off[ev[e]+1] += 1
            for v in range(n): off[v+1] += off[v]
            adj = [0]*(2*m); pos = off[:]
            for e in range(m):
                adj[pos[eu[e]]] = ev[e]; pos[eu[e]] += 1
                adj[pos[ev[e]]] = eu[e]; pos[ev[e]] += 1
            alive = [True]*n; deg = [off[v+1]-off[v] for v in range(n)]
            queue = [v for v in range(n) if deg[v] < 3]
            inq = [False]*n
            for v in queue: inq[v] = True
            head = 0
            while head < len(queue):
                v = queue[head]; head += 1
                if not alive[v]: continue
                alive[v] = False
                for t in range(off[v], off[v+1]):
                    w = adj[t]
                    if alive[w]:
                        deg[w] -= 1
                        if deg[w] < 3 and not inq[w]:
                            queue.append(w); inq[w] = True
            size = sum(alive)
            if size: nonempty += 1
            size_sum += size
        print(c, round(nonempty/120, 3), round(size_sum/120, 1), round(m_sum/120, 1))
```

**Receipts** (frac with 3-core · mean core size · mean edges): c = 3.0 → **0.033 · 3.8 · 595.2**; 3.2 → 0.283 · 37.6 · 639.8; 3.4 → 0.725 · 121.2 · 680.1; 3.6 → 0.983 · 195.3 · 717.9; 3.8 → 0.992 · 232.0 · 754.0; 4.2 → 1.000 · 286.2 · 837.7 (edge-count sanity: c·n/2 = 600, 640, 680, 720, 760, 840). The transition sits between c = 3.2 and 3.6 at n = 400, consistent with the asymptotic Pittel–Spencer–Wormald constant λ₃ ≈ 3.3509 (recorded from the literature; this census does not re-derive it). The lesson is the size row: 3.8 → 37.6 → 121.2 — when the core exists it is *large*; emergence is a jump in size, not a growth process, and that is why no first-moment count can see this threshold coming.

---
