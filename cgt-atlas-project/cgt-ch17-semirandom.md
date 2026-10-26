---
name: "cgt-ch17-semirandom"
title: "Ch. 17 — The Semi-Random Method: Nibble, Track, Absorb (A Lecture Course in the Feynman Style)"
type: "text/markdown"
---

# Chapter 17 · The Semi-Random Method

*Part of the Combinatorics & Graph Theory Atlas (the chapter map lives in the book basis).*

Chapter 4 taught the scandal: to prove an object exists, design a random experiment and show it succeeds with positive probability. Chapter 13 gave the method its grown-up ammunition — correlation, concentration, entropy. This chapter is about the last and subtlest upgrade: **stop letting randomness run wild and repairing the damage afterward. Expose the randomness in small bites, and after each bite, measure where the process stands.** A nibble eats a tiny random slice of the remaining structure; the tracked parameter — the uncovered-pair density, the list size, the residual degree — moves by its honest conditional expectation each round; the error stays small forever; the process converges on the full structure. Rödl invented the nibble to settle the Erdős–Hanani packing conjecture (1985). Pippenger and Spencer turned it into a lemma with hypotheses you can check (1989). Kahn turned the lemma into a coloring engine that decides the list-chromatic index asymptotically (1996). Keevash added a template and an absorber and proved that designs exist (2014). The ancestors — Ajtai, Komlós and Szemerédi, then Shearer, then Kim — ran the same engine on Ramsey numbers a decade earlier, and Kim's R(3,t) bound remains the method's most celebrated single result.

The deal with the reader is the one the Atlas has enforced since Chapter 1: every number printed below was machine-verified before printing. All randomized receipts come from a single documented engine — the Lehmer generator x ← 48271·x mod (2³¹−1), seed 20261081, Fisher–Yates with one draw per index — so the printed Python lab reproduces the receipts bit for bit. Where a theorem is cited rather than proved, the text says so; where a bound is vacuous at the machine's scale, the text says that too.

## How to read this chapter

Read with Chapters 4, 13 and 16 within reach: the nibble is what P12 (random construction) becomes when the experiment must *converge* rather than merely succeed once, and Keevash's design theorem is Chapter 16's divisibility ledger (P41) finally cashed for every large admissible order. Lines marked **✎ Checkpoint** are the places to stop and predict — commit to a guess, in ink, before reading on. Exercises are graded ●○○ *easy* (one idea, applied directly), ●●○ *moderate* (two ideas, or one tricky step), ●●● *tough* (several ideas combined); ◆ **pattern unknown** problems come with no hint — diagnosing the tool is part of the problem; ◐ **Explorations** are open-ended investigations that state what you should find, not a number to match. Worked answers sit at the end; hints travel with the problems.

Notation. A *packing* of a v-point set is a set of triples in which no pair of points lies in two blocks; the *leave* is the graph of pairs no block covers. D(v) is the maximum size of a triple packing on v points (the classical packing number, sometimes written D(v,3,2)); the counting bound is ⌊C(v,2)/3⌋. For a hypergraph H: D is the (maximum) vertex degree, the *codegree* of a pair is the number of edges containing it, and a *matching* is a set of pairwise disjoint edges. α(G), χ, Δ, d̄ are the independence number, chromatic number, maximum and average degree of a graph; R(3,t) is the Ramsey number. In the nibble, a_s is the *availability* — the fraction of pairs still uncovered at the start of round s — and λ_s is the round's empirical decay coefficient. AG(2,3) is the affine plane of order 3, the unique STS(9), whose 840 labeled copies populate Lecture 6. Convergence is as n → ∞; w.h.p. means with probability tending to 1.

## The pattern map for this chapter

| Pattern | Plain language | Where it fires here |
|---------|---------------|--------------------|
| **P43 Semi-random nibble (this chapter's home)** | Reveal a tiny random slice of the structure at a time and track one parameter through every nibble: the tracked quantity moves by honest conditional expectation each round, so the process converges on the full structure | All six lectures — the spine of the chapter |
| **P2 Double counting** | Count the same set two ways; equate | L1 (the counting bound C(v,2)/3 and the leave-divisibility \|L\| ≡ C(v,2) mod 3) |
| **P4 Recurrence + induction** | Relate case n to smaller cases | L2–L3 (the round-by-round evolution of a_s; the nibble loop is a recurrence you can analyze) |
| **P10 Averaging / expectation** | Some object beats the average | L3 (the mean-field predictor (v−2)a² is an expectation; the tracking is averaging conditionalized) |
| **P11 Explicit construction** | Beat the bound by *building* the object | L4 (the blow-up hosts; the exhibited 5-point independent set in the Clebsch graph) |
| **P12 Random construction** | Prove existence by sampling | L1 (the probabilistic instinct behind Erdős–Hanani); L4 (the one-shot random lower bound for R(3,t) that alteration could only push to t²/log² t) |
| **P13 Union bound** | If failure probabilities sum below 1, success exists | L4 (concentration replaces union bounds as the workhorse); L3 (the conflict-culling step is where the union bound's pessimism shows up as the conflict toll) |
| **P14 Alteration** | Random object + pruning | L4 (AKS's random-plus-delete lower bound); L6 (the *sacrifice* step — drop the mismatch and regrow) |
| **P25 Reduction / encoding** | Translate the problem; the target structure carries the proof | L5 (coloring → matching on an auxiliary structure); L6 (design existence → matching in an auxiliary hypergraph) |
| **P29 Entropy counting** | Count by description cost | L5 (the entropy-weighted nibble in Kahn's later work — flagged, not used) |
| **P41 Double-counting & divisibility** | Integrality is a design's birth certificate | L1 (the leave's degree parity and residue close every packing optimum at v ≤ 10); L6 (Keevash's divisibility conditions are Chapter 16's, met by nibble-plus-absorption) |

---

## Lecture 1 · The Nibble Is Born: Erdős–Hanani to Rödl

**The question.** Pack triples on a v-point set so that no pair of points sits in two triples. How many triples can you pack? This is the packing number D(v) = D(v,3,2); the covering twin C(v) asks for triples so that every pair sits in *at least* one. The two questions meet at the counting bound. Each triple consumes 3 pairs, and there are C(v,2) pairs in all, so

  **D(v) ≤ ⌊C(v,2)/3⌋ — the counting bound (P2, double counting).**

When v ≡ 1, 3 mod 6 the bound is achieved exactly: a Steiner triple system exists (Chapter 16), every pair consumed once, leave empty. For other orders something must be left over — a *leave*: the graph of pairs no block covers. The machine's small-scale table, every row an exhaustive fact (optimum proved by the bound arguments of Exercises 1–2 plus machine exhibits; receipts in the lab, Part 1):

| v | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
|---|---|---|---|---|---|---|----|
| counting bound ⌊C(v,2)/3⌋ | 2 | 3 | 5 | 7 | 9 | 12 | 15 |
| **optimum D(v)** | **1** | **2** | **4** | **7** | **8** | **12** | **13** |
| leave (pairs) | 3 | 4 | 3 | 0 | 4 | 0 | 6 |
| leave shape | star K₁,₃ | 4-cycle | perfect matching | — | perfect matching | — | K₁,₃ ⊔ 3K₂ (one deg-3 + nine deg-1) |

Two orders (7 and 9) are perfect — the Fano plane and AG(2,3). Every other order pays a leave, and the leave is not waste but *structure*: its degrees are all ≡ v−1 mod 2 (Exercise 1) and its size is ≡ C(v,2) mod 3. Those two parity facts close every optimum in the table (Exercise 2 does it by hand): at v = 6, all six leave-degrees must be odd, so the leave needs at least 3 edges, so D(6) ≤ (15−3)/3 = 4; at v = 10, ten odd degrees and |L| ≡ 0 mod 3 force |L| ≥ 6, so D(10) ≤ 13. The counting bound alone never does this — divisibility does (P41, the design-theoretic birth certificate, in miniature).

**The conjecture.** Erdős and Hanani asked the asymptotic question in 1963: for fixed block size k and t, as n → ∞, does the packing number P(n,k,t) meet its counting bound C(n,t)/C(k,t) up to a vanishing fraction? In the triple case: is the leave o(n²)? A greedy look at the table's last row says the gap is real — 13 against 15 at v = 10 — but the *fraction* 13/15 already hints which way it goes. Erdős and Hanani conjectured yes; proving it resisted the era's tools, because the obvious attacks fail in instructive ways.

**Why greedy starves.** Pack triples one at a time, anywhere you can. Late in the process the remaining uncovered pairs form isolated islands — a pair {a,b} whose every completion c has {a,c} or {b,c} already used — and the process dies with a positive fraction of pairs stranded. A *maximal* packing can be terrible: the windmill W₁₀ of Lecture 3's table takes all v − 2 triples through a fixed core pair {0,1}, covering 2v − 3 pairs, and is already maximal as soon as the remaining v − 2 points are fewer than 3 (or if one greedily extends on those v − 2 points, a bad maximal choice on the rest still strands a positive fraction of pairs). Greedy is maximal by construction; nothing about greed promises near-optimality. The random greedy of Lecture 2 does far better — but for thirty years after 1963, the only proofs of Erdős–Hanani-type statements were partial.

**Rödl's nibble (1985).** The idea that broke the conjecture is almost insultingly simple to state: *don't pack everything at once; pack a tiny slice, chosen at random, and repeat.* In one round, each still-available triple is selected with a small probability p. Selected triples conflict — two may share a pair — so you keep only the conflict-free survivors. Then you look at where you stand: the fraction a of pairs still uncovered has dropped by roughly p(v−2)a² per pair (the chance one of a pair's ≈ (v−2)a² available completions got selected and survived). The drop is *proportional to the state*: dense rounds eat lots, sparse rounds eat little. That self-scaling is the whole trick. Each round is nearly independent of the last, every vertex loses almost exactly its expected share, the profile stays near-uniform, and the error — the deviation from the mean-field prediction — accumulates slower than the signal. Iterated, the process leaves o(n²) pairs: the Erdős–Hanani conjecture, proved.

  **Rödl's theorem (1985, cited).*:** For fixed k and t, P(n,k,t) = (1+o(1))·C(n,t)/C(k,t) as n → ∞. The proof is the semi-random nibble: repeatedly consume a small random slice of the available blocks, tracking the t-subset availability; the leave is o(nᵗ) t-subsets (in the t = 2 case, o(n²) pairs).

(Yes, the asterisk is doing honest work: the full proof controls a hierarchy of error terms across Θ(log n)-many phases, and this chapter states, cites, and simulates — it does not re-derive. Frankl and Rödl's companion 1985 paper, *Near perfect coverings in graphs and hypergraphs* (EJC 6:317–326), developed the related uniform-covering machinery that later proofs — including Kim's — absorb as a tool.)

**✎ Checkpoint.** Before the machine speaks: the random greedy (Lecture 2) at v = 39 packs triples until stuck, ten seeded runs. Predict the leave fraction — is it closer to 1/2 (greedy starves badly), 1/4, or 1/10? Commit in ink; the receipt is 0.1045, and the surprise to predict next is that the *nibble* (Part 3) at v = 33 — a much smaller instance! — gets within a hair of it. Nibble scale beats greedy scale.

**What you now own.** The packing problem and its counting bound; the leave as structure (parity, divisibility); the small-order optima table, every entry proved; the greedy starvation phenomenon; Erdős–Hanani's conjecture; and the nibble idea — small random bites, self-scaling consumption, tracked errors — in its original habitat.

## Lecture 2 · The Random Greedy, and the Parameter That Steers It

Rödl's process selects each available triple with probability p each *round*. Before we simulate that, warm up on its p = 1 cousin: the **random greedy** — repeatedly pick a *uniformly random* available triple and keep it, until no triple is available. This is the process a programmer writes first, and its behavior is the first evidence that tracking matters.

**The receipts (lab Part 2).** Ten seeded runs at each v ∈ {15, 21, 27, 33, 39}, uniform available pick:

| v | 15 | 21 | 27 | 33 | 39 |
|---|----|----|----|----|----|
| mean leave fraction | 0.1714 | 0.1329 | 0.1333 | 0.1142 | 0.1045 |
| parity lemma holds (50/50 runs) | ✓ | ✓ | ✓ | ✓ | ✓ |

Three facts to notice. First, the fractions fall roughly like v^(−1/2)-scale at these toy sizes (v = 15 → 39 halves the fraction; n^(−1/2) falls by 0.62 over that range — the receipts are consistent with a subquadratic leave, and the honest caveat is that nothing at v ≤ 39 proves an asymptotic; this chapter pins no exponent). Second, the v = 21 → 27 *inversion* (0.1329 → 0.1333) is sampling noise — ten runs, per-run standard deviation ≈ 0.06 — and the text says so rather than smoothing it away. Third, the parity lemma — leave degrees ≡ v−1 mod 2 — held in 50 of 50 runs, which is what a *theorem* looks like on a machine (Exercise 1 proves it).

**✎ Checkpoint.** Predict the *shape* of the greedy leave at odd v (say v = 15, or the v = 9 miniature of Lecture 6 with C(9,2) = 36 total pairs) before you look: by the parity lemma, every vertex in the leave has even degree — so is the leave one big cycle, a union of edge-disjoint cycles, or an arbitrary subgraph? The v = 9 receipts (Lecture 6) show leaves of 6 or 9 pairs with all degrees even; the honest answer at odd v is that the leave is an *Eulerian* graph (a union of edge-disjoint cycles on its active vertices) — every vertex has even degree — which is exactly why the greedy can get stuck: a pair {a,b} in an Eulerian leave can still have all v − 2 of its third-point completions killed off because each candidate c has at least one of {a,c} or {b,c} already covered.

**Why the nibble is analyzable and the greedy is (mostly) not.** The random greedy makes *large* moves: each accepted triple changes the availability profile by a visible step, and the steps are strongly correlated with the state (the process over-eats exactly where it just ate). The nibble makes *tiny* moves: in one round the availability drops by a factor 1 − Θ(a²p·v) across the board, every vertex's residual degree falls by nearly the same fraction, and the profile *re-uniformizes* as it shrinks. That is what lets you write a recurrence — Lecture 3's subject — and why Pippenger and Spencer, Kahn, and Keevash all nibble rather than feast. The formal tracking tool — write the expected drift of each parameter as a differential equation and prove the process follows it w.h.p. — is the **differential-equation method** (Wormald's 1999 survey is the standard reference; cited, not proved here). Chapter 13's martingale lectures are the concentration engine underneath; P43 is the bookkeeping discipline on top.

**The nibble in miniature (a preview of the lab, Part 3).** At v = 33 with p = 1/33, seed 20261081: the process runs **65 rounds** and strands a leave of **60 pairs — fraction 0.1136** — already beating the random greedy's v = 33 mean (0.1142). The tracked parameter is a_s, the availability (fraction of the 528 pairs uncovered at round s's start), and the mean-field prediction says each uncovered pair should see about (v−2)a_s² available completions. The census, observed against predicted:

| round s | 1 | 2 | 3 | 4 | 5 | 14 | 20 | 30 |
|---------|---|---|---|---|---|----|----|----|
| availability a_s | 1.0000 | 0.6136 | 0.4716 | 0.4148 | 0.3580 | 0.1989 | 0.1761 | 0.1591 |
| completions obs. | 31.00 | 11.72 | 6.95 | 5.36 | 3.79 | 1.31 | 0.81 | 0.57 |
| mean-field (v−2)a² | 31.00 | 11.67 | 6.89 | 5.33 | 3.97 | 1.23 | 0.96 | 0.78 |

Five rounds of agreement to within 2–5% — the mean-field tracking *works* while the profile is uniform. Then look at rounds 20 and 30: observed completions fall *below* the mean-field line (0.81 vs 0.96; 0.57 vs 0.78). That is the endgame: the surviving uncovered pairs are not a random sample but the correlated residue of the culling — their lost completions cluster. The naive model says the decay coefficient λ_s (defined by a_{s+1} = a_s·e^(−λ_s a_s²)) should sit at λ₀ = (v−2)/v = 0.939 every round if selections never conflicted; the observed first ten λ_s are 0.488, 0.699, 0.577, 0.856, 0.512, 0.464, 0.924, 0.973, 0.610, 1.424 — oscillating across the naive line, sometimes half of it, sometimes 1.5× it. That oscillation is the **conflict toll**: pairs die not one at a time but in little bursts when a selected triple culls several completions at once. Exercise 8 makes you compute these by hand from the a_s list; Lecture 3 explains why a lemma, not a simulation, is needed to bound the toll.

**What you now own.** The random greedy and its receipts; the parity lemma in machine form; the difference between big correlated steps (greedy) and tiny re-uniformizing ones (nibble); the tracked parameter a_s and its mean-field predictor; the conflict toll made visible; and the differential-equation method as the tracking discipline's formal name.

## Lecture 3 · The Pippenger–Spencer Nibble Lemma

Rödl's argument was a proof *of a process*; what the field needed was a theorem *about a class of hypergraphs*, with hypotheses you can check on the structure in front of you. Pippenger and Spencer supplied it in 1989, and it is the engine room of everything in the rest of this chapter.

  **The nibble lemma (Pippenger–Spencer 1989, cited).** Let H be an r-uniform hypergraph on n vertices, r fixed. Suppose (i) every vertex has degree (1+o(1))D — *near-regularity* — and (ii) every pair of distinct vertices has codegree at most o(D) — the codegrees are negligible against the degrees (a precise rate is part of the theorem). Then H contains a matching covering (1−o(1)) of its vertices: all but o(n) points are consumed by disjoint edges.**

Read the hypotheses as a checklist — they are exactly the two ways a nibble can fail, and the machine's census (lab Part 4) turns each into a specimen. For each structure: D the maximum degree, the largest codegree, their ratio, and the exact maximum matching (by exhaustive search), as a fraction of points covered:

| structure | D | max codegree | ratio | max matching covers | which hypothesis dies |
|-----------|---|--------------|-------|---------------------|----------------------|
| W₁₀ windmill (10 triples {0,1,2+i} on 12 points) | 10 | 10 | **1.000** | 3/12 = **25%** | near-regularity (degrees 10,10,1,…,1) |
| 3 × K₄³ (three disjoint complete 3-graphs on 4 points) | 3 | 2 | **0.667** | 9/12 = **75%** | both: codegree, and 4 ∤ 3 — components can't tile |
| Fano plane (7 points, 7 lines) | 3 | 1 | **0.333** | 3/7 = **43%** | codegree (ratio fixed: no o(D)) — any two lines meet |
| Fano blow-up, m = 3 (21 points, 189 triples) | 27 | 3 | **0.111** | 21/21 = **100%** | neither — a perfect matching exists |
| AG(2,3) (9 points, 12 lines) | 4 | 1 | **0.250** | 9/9 = **100%** | neither — parallel classes supply disjoint lines |

```svg
<svg viewBox="0 0 680 265" width="680" height="265" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="Comparison of maximum matchings in the Fano plane PG(2,2) and the affine plane AG(2,3)">
  <style>
    .f-title { font-family: Georgia, serif; font-size: 13px; font-weight: bold; fill: #1a1a1a; text-anchor: middle; }
    .f-sub { font-family: Georgia, serif; font-size: 11.5px; fill: #444; text-anchor: middle; }
    .f-lbl { font-family: 'Courier New', monospace; font-size: 11px; font-weight: bold; fill: #1a1a1a; text-anchor: middle; dominant-baseline: central; }
    .f-edge-bg { stroke: #bbb; stroke-width: 1.4; fill: none; }
    .f-edge-hi { stroke: #1b5e20; stroke-width: 3.2; fill: none; stroke-linecap: round; }
    .f-edge-F { stroke: #b71c1c; stroke-width: 3.2; fill: none; stroke-linecap: round; }
    .f-node-cov { fill: #e8f5e9; stroke: #1b5e20; stroke-width: 1.8; }
    .f-node-fano { fill: #ffebee; stroke: #b71c1c; stroke-width: 1.8; }
    .f-node-unc { fill: #f5f5f5; stroke: #777; stroke-width: 1.4; stroke-dasharray: 3,2; }
  </style>
  <text x="165" y="20" class="f-title">Fano Plane PG(2,2) — Max Matching: 1 Line (3/7 = 43%)</text>
  <text x="165" y="37" class="f-sub">D = 3, max codegree = 1 (ratio 0.333): every pair of lines intersects</text>
  <circle cx="165" cy="148" r="46" class="f-edge-bg"/>
  <line x1="165" y1="56" x2="165" y2="194" class="f-edge-bg"/>
  <line x1="245" y1="194" x2="125" y2="125" class="f-edge-bg"/>
  <line x1="85" y1="194" x2="205" y2="125" class="f-edge-bg"/>
  <line x1="165" y1="56" x2="85" y2="194" class="f-edge-bg"/>
  <line x1="85" y1="194" x2="245" y2="194" class="f-edge-bg"/>
  <line x1="165" y1="56" x2="245" y2="194" class="f-edge-F"/>
  <circle cx="165" cy="56" r="11" class="f-node-fano"/><text x="165" y="56" class="f-lbl">0</text>
  <circle cx="205" cy="125" r="11" class="f-node-fano"/><text x="205" y="125" class="f-lbl">1</text>
  <circle cx="245" cy="194" r="11" class="f-node-fano"/><text x="245" y="194" class="f-lbl">2</text>
  <circle cx="85" cy="194" r="11" class="f-node-unc"/><text x="85" y="194" class="f-lbl">3</text>
  <circle cx="125" cy="125" r="11" class="f-node-unc"/><text x="125" y="125" class="f-lbl">4</text>
  <circle cx="165" cy="194" r="11" class="f-node-unc"/><text x="165" y="194" class="f-lbl">5</text>
  <circle cx="165" cy="148" r="11" class="f-node-unc"/><text x="165" y="148" class="f-lbl">6</text>
  <text x="165" y="232" class="f-sub">Matched triple {0,1,2} (solid red); vertices {3,4,5,6} (dashed) stranded</text>
  <line x1="340" y1="15" x2="340" y2="245" stroke="#ddd" stroke-width="1"/>
  <text x="510" y="20" class="f-title">Affine Plane AG(2,3) — Max Matching: 3 Lines (9/9 = 100%)</text>
  <text x="510" y="37" class="f-sub">D = 4, max codegree = 1 (ratio 0.250): parallel class tiles all 9 points</text>
  <line x1="440" y1="68" x2="440" y2="196" class="f-edge-bg"/>
  <line x1="510" y1="68" x2="510" y2="196" class="f-edge-bg"/>
  <line x1="580" y1="68" x2="580" y2="196" class="f-edge-bg"/>
  <line x1="440" y1="68" x2="580" y2="196" class="f-edge-bg"/>
  <line x1="580" y1="68" x2="440" y2="196" class="f-edge-bg"/>
  <line x1="440" y1="68" x2="580" y2="68" class="f-edge-hi"/>
  <line x1="440" y1="132" x2="580" y2="132" class="f-edge-hi"/>
  <line x1="440" y1="196" x2="580" y2="196" class="f-edge-hi"/>
  <circle cx="440" cy="68" r="11" class="f-node-cov"/><text x="440" y="68" class="f-lbl">0</text>
  <circle cx="510" cy="68" r="11" class="f-node-cov"/><text x="510" y="68" class="f-lbl">1</text>
  <circle cx="580" cy="68" r="11" class="f-node-cov"/><text x="580" y="68" class="f-lbl">2</text>
  <circle cx="440" cy="132" r="11" class="f-node-cov"/><text x="440" y="132" class="f-lbl">3</text>
  <circle cx="510" cy="132" r="11" class="f-node-cov"/><text x="510" y="132" class="f-lbl">4</text>
  <circle cx="580" cy="132" r="11" class="f-node-cov"/><text x="580" y="132" class="f-lbl">5</text>
  <circle cx="440" cy="196" r="11" class="f-node-cov"/><text x="440" y="196" class="f-lbl">6</text>
  <circle cx="510" cy="196" r="11" class="f-node-cov"/><text x="510" y="196" class="f-lbl">7</text>
  <circle cx="580" cy="196" r="11" class="f-node-cov"/><text x="580" y="196" class="f-lbl">8</text>
  <text x="510" y="232" class="f-sub">Parallel class {012, 345, 678} (solid green) covers every point once</text>
</svg>
```

The Fano plane is the census's moral center: its maximum matching covers 3 of 7 points because *any two lines intersect* — the codegree obstruction in the flesh. Blow it up (each point → 3 twins, each line → all 27 triples) and the ratio falls from 1/3 to 1/9 while D grows from 3 to 27: **blow-ups wash out fixed codegrees** (Exercise 3 computes the ratio 1/(3m) by hand). That washing-out is why Rödl's Erdős–Hanani application works: the auxiliary hypergraph whose vertices are the t-subsets inherits fixed-bounded codegrees against a growing D — the o(D) hypothesis for free. The windmill dies the *other* death — its degrees are 10, 10, then ten 1s — a warning that regularity is a separate hypothesis, not a bonus of sparseness. And 3 × K₄³ fails for the third, silent reason: each 4-point component can host only one disjoint triple, so 9 of 12 points is the *divisibility* ceiling (4 ≡ 1 mod 3) — P41 hiding inside a matching problem.

**✎ Checkpoint.** Before reading on: the Fano blow-up at m = 3 covers 100%. Predict the *un-blown* AG(2,3)'s matching coverage from its ratio 0.250 — does a ratio of 1/4 at toy scale obstruct anything? (Receipt: 100% — three mutually parallel lines cover all 9 points. The lesson: the lemma's hypotheses are *asymptotic*; at D = 4 the census is a morality table, not a counterexample.)

Pippenger and Spencer's own application was chromatic: a hypergraph satisfying the hypotheses has its edges colorable with (1+o(1))D colors — edge colorings are iterated near-perfect matchings, one nibble per color class. The nibble loop, abstracted from everything so far, is now small enough to carry in your pocket:

1. **Slice:** expose a small random piece of the remaining structure (select each available edge with probability p).
2. **Cull:** discard conflicts (the union bound's pessimism becomes the *conflict toll*, Lecture 2's λ-oscillation).
3. **Track:** update the parameter (availability, residual degree, list size) by its conditional expectation; prove the deviation stays small (martingale concentration, Chapter 13).
4. **Re-uniformize and repeat:** the profile after the bite is the profile before, scaled; recurse.

Steps 3–4 are the pattern P43; steps 1–2 alone are merely P12 with extra steps. The difference is the *theorem-shaped guarantee* that the parameter stays on its predicted trajectory — which is what the next three lectures cash into coloring (L5), Ramsey numbers (L4), and design existence (L6).

## Lecture 4 · The Ancestors: AKS, Shearer, Kim, and R(3,t)

The nibble's official birth is 1985, but its *spirit* — guided randomness with tracked parameters — decides the most famous off-diagonal Ramsey number a decade early. Chapter 10 introduced R(3,t): the least n such that every triangle-free graph on n vertices has an independent set of size t. Cross back there for the problem's biography; what matters here is the method's.

**The upper side (1980).** Ajtai, Komlós and Szemerédi proved that a triangle-free graph on n vertices with average degree d̄ has independence

  **α ≥ c·(n/d̄)·log d̄ — the AKS bound,**

with c an absolute constant. The consequence is immediate: R(3,t) ≤ c'·t²/log t. The proof's engine is a *degree-cleaning induction* — repeatedly discard low-degree vertices, applying the bound to the surviving core — and the triangle-free hypothesis enters exactly once: **every neighborhood is an independent set** (a vertex's neighbors are pairwise non-adjacent, or there'd be a triangle). That single structural fact, iterated with tracked degrees, is worth a logarithm over the trivial α ≥ n/(d̄+1) (Chapter 4's greedy bound). It is P43 avant la lettre: an averaging argument conditioned on a tracked degree profile.

**Shearer's sharpening (1983).** The constant c was never the issue; the *shape* was. Shearer proved the optimal-in-shape bound for triangle-free graphs:

  **α ≥ n·(d̄ ln d̄ − d̄ + 1)/(d̄−1)² — Shearer's bound.**

For large d̄ this is (n/d̄)(ln d̄ − 1 + o(1)) — the AKS bound with the log term made exact. Combined with the degree-cleaning scheme, it pins the upper bound at its asymptotic form R(3,t) ≤ (1+o(1))·t²/log t (cited; Kim's 1995 paper records exactly this as "the known upper bound"). The machine receipts (lab Part 5) calibrate the bound at honest-to-goodness scales — and show it is a *lower* bound with a real gap, tightening only as d grows:

| host graph | n | d | α (exact, machine) | Shearer bound | ratio |
|------------|---|---|--------------------|---------------|-------|
| balanced blow-up of C₅, m = 2 | 10 | 4 | 4 | 2.828 | 0.71 |
| balanced blow-up of C₅, m = 3 | 15 | 6 | 6 | 3.450 | 0.58 |
| balanced blow-up of C₅, m = 4 | 20 | 8 | 8 | 3.933 | 0.49 |
| balanced blow-up of C₅, m = 5 | 25 | 10 | 10 | 4.329 | 0.43 |
| Clebsch graph (F₂⁴, distances 1 and 4) | 16 | 5 | 5 | 4.047 | 0.81 |

The blow-up hosts (P11: built explicitly, twins of the 5-cycle) have α = 2m exactly — take both twin-classes of two non-adjacent cycle vertices. Watch the ratio column fall as d grows: 0.71 → 0.43. That fall is not the bound failing — it is the bound's shape. Shearer's guarantee is a Θ((ln d̄ − 1)/d̄) fraction of n, tuned for sparse random-like graphs; these hosts are dense twins with α proportional to n, so the honest asymptotic bound undershoots by a growing factor — the gap is the *bound's* coarseness at fixed d, not the graph's exceptionality. The Clebsch graph is the census's jewel: 5-regular, triangle-free (machine-checked), α = 5 with the exhibited independent set {0010, 0100, 0111, 1001, 1110} (binary labels; pairwise distances 2 or 3), Shearer guaranteeing 4.047 — within one of perfect at d = 5.

**The lower side: from alteration to process.** For the lower bound R(3,t) ≥ (big), you must *build* a triangle-free graph on n vertices with α < t — many vertices, few independent sets. The one-shot probabilistic method (P12) plus alteration (P14) — sample G(n,p), delete one endpoint of every triangle — reaches only n ~ t²/log² t: a log off. The triangle-free *process* closes the gap: start with n vertices and no edges; repeatedly add a uniformly random edge that creates no triangle, until stuck. Erdős, Suen and Winkler (1995) analyzed exactly this kind of random maximal graph — for the triangle-free property the process ends with only Θ(n^{3/2}) edges, and their paper already noted the Ramsey payoff; along the way, this is the process that makes the constraint *do work*: every added edge is chosen from the still-safe candidates, so the graph stays triangle-free by construction, not by deletion. The machine's seeded runs (lab Part 5):

| n | edges (receipt) | (1/(2√2))·n^{3/2}·√(ln n) | Δ (receipt) | √(n ln n) | α exact | ⇒ |
|---|-----------------|------------------------------|------------|-----------|---------|---|
| 30 | 124 | 107.1 | 11 | 10.1 | 11 | R(3,12) > 30 |
| 60 | 402 | 332.5 | 16 | 15.7 | 17 | R(3,18) > 60 |

Triangle-free by construction, machine-verified; α exactly computed (11 and 17 — each within one of the max degree, the process's signature). The receipts sit 16% and 21% above the asymptotic edge curve — honest small-n overshoot, the same direction at both scales. Kim (1995) proved what the receipts gesture at: the triangle-free process, run to its end and analyzed with full nibble-grade tracking, yields a graph with α ≤ t on n = (1/4−o(1))·t²/log t vertices:

  **R(3,t) ≥ (1/4−o(1))·t²/log t — Kim's theorem (1995, cited; a Fulkerson Prize).**

With the (1+o(1)) upper bound, this nails R(3,t) = Θ(t²/log t). Bohman (2009) re-ran the process with nibble-grade concentration and pinned its final edge count at (1/(2√2)+o(1))·n^{3/2}√(log n); Bohman and Keevash's dynamic concentration (2021) recovered Kim's 1/4 constant through the process itself — the same result found independently and simultaneously by Fiz Pontiveros, Griffiths and Morris. The lesson this chapter exists to teach: **alteration threw away a log because it repaired damage after the fact; the process never created the damage.** Guided randomness with tracked parameters — P43 — is worth exactly one logarithm here, and the constant 1/4 versus alteration's crude residue is what "semi-random" buys.

**✎ Checkpoint.** Predict before computing: in the n = 30 receipt graph (124 edges, α = 11), what does Shearer's bound guarantee? Guess the integer — then check: d̄ = 8.2667, bound = 5.792, truth 11. The graph is *better than Shearer promises* — its degrees are too uniform for its independence to be minimal — which is precisely the process's design goal.

**What you now own.** The AKS degree-cleaning idea; Shearer's sharp bound and its honest gap at fixed d; the triangle-free process as constraint-respecting greedy; Kim's theorem and the alteration-vs-process log gap; the receipts table; and the moral: tracking beats repairing.

## Lecture 5 · Kahn's Guided Randomness: Coloring by Nibble

Color the edges of a graph so that incident edges differ. Vizing's theorem (Chapter 3) says Δ+1 colors always suffice and Δ sometimes doesn't; the list version asks more — each edge e arrives with its own palette L(e), and edge e must receive a color from L(e). The *list-chromatic index* χ'ₗ(G) is the least k such that every assignment of k-element lists admits a proper edge coloring from the lists. Since one can assign the same k lists everywhere, χ'ₗ ≥ χ' ≥ Δ; the hard question is the reverse gap, and for the nibble it is the perfect workout: coloring *is* matching, iterated.

**The engine.** Kahn's algorithm (the 1996 papers; cited, not proved here) nibbles the edge set:

1. Each uncolored edge picks, with probability p, one random color from its current list.
2. Conflicts — two incident edges that picked the same color — are *all* returned to the pool (the conflict-cull of Lecture 3, now in color).
3. Every color used by a newly colored edge is deleted from the lists of all neighboring edges.
4. Track: after the round, each list has shrunk by nearly the same factor, and the number of colors available to each edge stays a near-uniform (1−o(1)) multiple of the number of colors *not yet used in its neighborhood* — the tracked parameter, exactly a_s in a new costume.

The punchline, the analogue of Pippenger–Spencer's chromatic application with lists in play:

  **Kahn's theorem (1996, cited).** The list-chromatic index of every multigraph of maximum degree Δ satisfies χ'ₗ ≤ Δ + o(Δ) as Δ → ∞; for simple graphs the statement reads χ'ₗ(G) = (1+o(1))Δ. Since χ'ₗ ≥ χ' ≥ Δ always, the list-chromatic index is asymptotically decided: Δ + o(Δ).

The reduction doing the quiet work (P25): edge coloring from lists is a *matching problem in an auxiliary bipartite graph* — edges of G on one side, color slots on the other, each edge needing a disjoint set of "its colors' slots." A nibble-matching in the auxiliary structure, tracked so that every edge retains a near-equal share of live colors, is a coloring. Kahn's own view of the field's toolkit later added the entropy weights of Chapter 13's ledger (P29) — flagged here as a door, not opened.

**Why tracking is load-bearing here.** The naive one-shot attempt — color each edge a random color from its list, then repair — drowns in conflicts: an edge with Δ neighbors needs its color to avoid up to Δ others, and the union bound's cost (P13's pessimism) is a multiplicative constant one cannot afford when the palette is exactly Δ + o(Δ). The nibble colors a p-slice per round; the *conditional* expectation of each list's survival is computable because the slice is small; the deviation concentrates (Chapter 13's Azuma); the parameters stay on trajectory for the Θ(log Δ) rounds needed. The receipts of Lecture 2 are this story in miniature: the λ-oscillation across the naive line 0.939 is exactly the cull's sting, and the point of the lemma-grade tracking is that the sting stays bounded — the process never enters a state where some edge's list dies before the edges are done.

**✎ Checkpoint.** Before the receipts: in a graph of maximum degree Δ = 100, Kahn colors with 100 + o(100) lists. Guess the order of the o(100) correction from the nibble's mechanics — is it closer to 1, to √Δ = 10, or to Δ/log Δ? (The theorem's proof gives o(Δ) with a polylog-scale saving at best in the original — the honest answer is "some vanishing fraction, far smaller than alteration would need": alteration-style repair costs a *constant fraction*, and that is precisely the gap between 1+o(1) and what greedy repair achieves.)

**What you now own.** List coloring as nibble-matching; the tracked list-size parameter; Kahn's asymptotic determination of χ'ₗ; and the transfer principle: *any* problem whose feasible solutions are matchings in an auxiliary structure inherits the nibble — which is the door to Lecture 6.

## Lecture 6 · Designs Exist: Nibble + Template + Absorption

Chapter 16 ended with the design-theoretic ledger (P41): a Steiner system S(t,k,n) can exist only if the divisibility conditions hold — C(n−i, t−i)/C(k−i, t−i) integral for 0 ≤ i < t (the i = 0 term: C(n,t)/C(k,t) blocks exactly) — and Wilson's theorem proved that for fixed t, k, every sufficiently large *admissible* order carries a design. What Wilson's iterative constructions did not give was a *random-like* existence theory; what the subject lacked was any method for large t. Keevash (2014) closed both gaps at once:

  **Keevash's theorem (2014, cited; arXiv:1401.3665).** For fixed t and k and all sufficiently large n satisfying the divisibility conditions, the design S(t,k,n) exists — and in abundance: all sufficiently large admissible orders carry exponentially many designs. The first Steiner systems with t ≥ 6 ever constructed come out of this theorem.

The architecture is the chapter's whole story assembled, plus one new organ. **(1) The nibble** (Rödl, Pippenger–Spencer grade): cover all but a small, *random-looking* leave with a tracked semi-random process — on an auxiliary hypergraph whose vertices record not just t-subsets but small anchored configurations, so that what survives is guaranteed typical. **(2) The template:** a small reservoir design-like structure, set aside *in advance*, that can absorb configurations on demand. **(3) Absorption:** the absorber is a pre-built pool with a closure property — for every leave the nibble might strand (within the typical family), the pool contains a small structure that, swapped in, completes the design. Glock, Kühn, Lo and Osthus later gave a parallel proof by *iterative absorption* (the memoir-length 2023 version is the standard reference; cited) — the same three-organ architecture with the absorber applied layer by layer.

**The miniature that proves the architecture is not decorative (lab Part 6).** Take the smallest interesting design world: STS(9), the affine plane AG(2,3) and its 840 labeled copies (Exercise 10 proves 840 = 9!/432). The machine enumerated all 840 systems and audited them: **every one is anti-Pasch** — no system contains four triples on six points with each point in exactly two of them (the Pasch configuration {012, 034, 135, 245}). The F₃ case analysis of Exercise 7 shows why: in the affine plane of order 3, any four pairwise non-parallel lines repeat an intersection point. Now run the chapter's greedy on 9 points — twenty seeded passes, each pair order random, each uncovered pair completed by a random available third point — and ask the design-theory question: *can the packing be repaired into a complete system?*

- **Direct completion: 0 of 20.** No greedy packing extends to a full STS(9) by adding triples. Mean packed 9.50 triples (of 12), leave 6 or 9 pairs, leave degrees all even (parity lemma, 20/20).
- **Trade repair: provably impossible.** A *trade* swaps one set of triples for another covering exactly the same pairs. The classical volume-4 trade is the Pasch swap {012, 034, 135, 245} ↔ {013, 024, 125, 345} (twelve pairs, identical on both sides — machine-checked). But Exercise 5 proves the classification: *every* volume-4 trade is Pasch-shaped, and Exercise 6 draws the conclusion — a trade's new side must live inside the target system, a Pasch inside an anti-Pasch system is a contradiction, so **no sequence of volume-4 trades, of any length, ever lands a greedy packing inside any of the 840 systems.** The machine's census of inter-system trade volumes confirms the shape of the wall: distinct STS(9)s differ by trades of volumes 6, 8, 9, 10, 11, 12 (15,120 pairs at volume 6; none at 4, 5, or 7) — volume 4 is not merely rare, it is *absent*.
- **Absorption, honestly: sacrifice, then regrow.** Drop the packing's mismatched triples — at most 2 in all twenty runs (mean 1.65) — and what survives, 7 to 9 triples (mean 7.85), sits inside one of the 840 systems: 20 of 20 packings complete. The escape from the trade-impossibility wall is exactly the architectural move: not repair-in-place (P12 thinking) but *sacrifice and regrow inside a template* — Keevash's template+absorber, automated. Since every packing sits within 2 sacrificed triples of some system, and the minimum trade volume is 4, the toy makes the general point brutally: **when repair is impossible, pre-built flexibility is not optional.**

```svg
<svg viewBox="0 0 680 250" width="680" height="250" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="The volume-4 Pasch trade T and T-prime on 6 vertices">
  <style>
    .p-title { font-family: Georgia, serif; font-size: 13px; font-weight: bold; fill: #1a1a1a; text-anchor: middle; }
    .p-sub { font-family: Georgia, serif; font-size: 11.5px; fill: #444; text-anchor: middle; }
    .p-lbl { font-family: 'Courier New', monospace; font-size: 11px; font-weight: bold; fill: #1a1a1a; text-anchor: middle; dominant-baseline: central; }
    .p-line-A { stroke: #1565c0; stroke-width: 2.4; fill: none; stroke-linecap: round; }
    .p-line-B { stroke: #6a1b9a; stroke-width: 2.4; fill: none; stroke-dasharray: 6,3; stroke-linecap: round; }
    .p-node { fill: #fff; stroke: #222; stroke-width: 1.8; }
  </style>
  <text x="155" y="20" class="p-title">Pasch Side T = {012, 034, 135, 245}</text>
  <text x="155" y="37" class="p-sub">4 triples, 6 points (each degree 2), 12 covered pairs</text>
  <line x1="155" y1="58" x2="75" y2="194" class="p-line-A"/>
  <line x1="155" y1="58" x2="235" y2="194" class="p-line-A"/>
  <path d="M 115 126 Q 155 202 195 126" class="p-line-A"/>
  <path d="M 75 194 Q 155 134 235 194" class="p-line-A"/>
  <circle cx="155" cy="58" r="11" class="p-node"/><text x="155" y="58" class="p-lbl">0</text>
  <circle cx="115" cy="126" r="11" class="p-node"/><text x="115" y="126" class="p-lbl">1</text>
  <circle cx="75" cy="194" r="11" class="p-node"/><text x="75" y="194" class="p-lbl">2</text>
  <circle cx="195" cy="126" r="11" class="p-node"/><text x="195" y="126" class="p-lbl">3</text>
  <circle cx="235" cy="194" r="11" class="p-node"/><text x="235" y="194" class="p-lbl">4</text>
  <circle cx="155" cy="164" r="11" class="p-node"/><text x="155" y="164" class="p-lbl">5</text>
  <text x="155" y="228" class="p-sub">Lines: {0,1,2}, {0,3,4}, {1,3,5}, {2,4,5}</text>
  <text x="340" y="118" class="p-title">Volume-4 Trade</text>
  <line x1="305" y1="132" x2="375" y2="132" stroke="#333" stroke-width="2"/>
  <polygon points="375,132 367,127 367,137" fill="#333"/>
  <polygon points="305,132 313,127 313,137" fill="#333"/>
  <text x="340" y="152" class="p-sub">same 12 pairs</text>
  <text x="340" y="168" class="p-sub">T ∩ T′ = ∅</text>
  <text x="525" y="20" class="p-title">Mate T′ = {013, 024, 125, 345}</text>
  <text x="525" y="37" class="p-sub">Re-organizes the same 12 pairs into 4 new triples</text>
  <polygon points="525,58 485,126 565,126" class="p-line-B"/>
  <polygon points="485,126 445,194 525,164" class="p-line-B"/>
  <polygon points="565,126 605,194 525,164" class="p-line-B"/>
  <polygon points="525,58 445,194 605,194" class="p-line-B"/>
  <circle cx="525" cy="58" r="11" class="p-node"/><text x="525" y="58" class="p-lbl">0</text>
  <circle cx="485" cy="126" r="11" class="p-node"/><text x="485" y="126" class="p-lbl">1</text>
  <circle cx="445" cy="194" r="11" class="p-node"/><text x="445" y="194" class="p-lbl">2</text>
  <circle cx="565" cy="126" r="11" class="p-node"/><text x="565" y="126" class="p-lbl">3</text>
  <circle cx="605" cy="194" r="11" class="p-node"/><text x="605" y="194" class="p-lbl">4</text>
  <circle cx="525" cy="164" r="11" class="p-node"/><text x="525" y="164" class="p-lbl">5</text>
  <text x="525" y="228" class="p-sub">Absent in all 840 STS(9)s (anti-Pasch wall)</text>
</svg>
```

**✎ Checkpoint.** Before the census: predict the trade-volume histogram between distinct STS(9)s. Two random labeled systems — is their symmetric difference more like 4 triples (one Pasch), 6, or 12 (disjoint)? Commit, then read: the answer is "6 at minimum, and 4 is *structurally absent*" — the anti-Pasch property reaches across the whole 840-system family, which is why the greedy's failures cannot be traded away.

**What you now own.** The three-organ architecture — nibble, template, absorber; the anti-Pasch obstruction as a machine-verified wall; the trade-volume census; the sacrifice-distance receipts; and the chapter's thesis in its final form: the semi-random method converges *when it is allowed to plan ahead* — the absorber is the tracked parameter's last payment, made in advance.

## The Trick Bag (reference card)

**The nibble loop (P43, the pattern).** *Slice* — expose a small random piece (probability p per available item). *Cull* — discard all conflicts. *Track* — update the parameter by conditional expectation; prove concentration (Azuma/Chernoff, Chapter 13). *Re-uniformize* — the post-bite profile is the pre-bite profile, scaled; recurse Θ(log n) times. The theorem-shaped guarantee — the parameter stays on trajectory — is what separates P43 from P12+P14.

**When to reach for it.** The one-shot random object fails by *local collapse* (greedy starvation, list death, stranded pairs) or needs *global uniformity* (near-regular profiles, equal list sizes). If the object can be repaired after the fact at cost o(1) — use P14 alteration (Chapter 4). If the repair costs a constant (R(3,t)'s lost log), the nibble is the difference between 1+o(1) and the crude constant.

**The two death-hypotheses (Pippenger–Spencer checklist).** Near-regularity: degrees (1+o(1))D. Codegree: pairs in o(D) edges. The windmill dies the first, the Fano plane the second, blow-ups survive both (codegree ratio → 0 as m grows: 1/(3m)). Divisibility kills silently afterward (3 × K₄³: 4 ≢ 0 mod 3 caps matchings at 75%).

**The formula box.**

| # | formula | where |
|---|---------|-------|
| 1 | D(v) ≤ ⌊C(v,2)/3⌋; leave \|L\| ≡ C(v,2) mod 3; leave degrees ≡ v−1 mod 2 | L1, Ex 1–2 |
| 2 | optima D(v), v = 4..10: **1, 2, 4, 7, 8, 12, 13** (leaves 3, 4, 3, 0, 4, 0, 6) | L1, lab Part 1 |
| 3 | Erdős–Hanani/Rödl: P(n,k,t) = (1+o(1))·C(n,t)/C(k,t) | L1 |
| 4 | Pippenger–Spencer: near-regular + codegrees o(D) ⇒ matching covers (1−o(1)) of vertices | L3 |
| 5 | nibble mean-field: available completions ≈ (v−2)a²; naive decay λ₀ = (v−2)/v | L2–L3, Ex 8 |
| 6 | Shearer: α ≥ n(d̄ ln d̄ − d̄ + 1)/(d̄−1)² (triangle-free) | L4, Ex 4, 9 |
| 7 | AKS: α ≥ c(n/d̄)·log d̄; upper R(3,t) ≤ (1+o(1))t²/log t | L4 |
| 8 | Kim: R(3,t) ≥ (1/4−o(1))·t²/log t; TFP edges (1/(2√2))·n^{3/2}·√(ln n), Δ ~ √(n ln n) | L4, Ex 9 |
| 9 | Kahn: χ'ₗ = Δ + o(Δ) (multigraphs) | L5 |
| 10 | Keevash: divisibility C(n−i,t−i)/C(k−i,t−i) ∈ ℤ (0 ≤ i < t) + large n ⇒ S(t,k,n) exists | L6 |
| 11 | volume-4 trades are Pasch-shaped; anti-Pasch ⇒ no volume-4 trade repair; min trade volume between STS(9)s = 6 | L6, Ex 5–6, 12 |
| 12 | sacrifice distance: every greedy packing of AG(2,3) sits ≤ 2 dropped triples from a complete system (20/20, kept 7–9, mean 7.85) | L6, lab Part 6 |

**The scar list (read before re-implementing anything).** (i) A B&B that only branches on *covering* the first uncovered element silently forbids leaving it — it returns wrong optima (the 2/3/4 class); the leave-branch is not optional. (ii) Update the incumbent only when the count *exceeds* best; a `best = count` leaf assignment overwrites downward. (iii) A greedy-coloring count bounds cliques, *not* independent sets — for exact α, search maximum cliques in the complement. (iv) Stop the nibble on exhaustion (no available item), never on an empty selection — empty rounds are the endgame's rhythm. (v) JavaScript bitwise masks wrap at 32 bits; at n = 36 pair-bits the enumeration returns nonsense — use arrays. (vi) A hypergraph-matching B&B needs the *free-vertex* bound ⌊unused/3⌋ on remaining capacity, never ⌊used/3⌋.

## Exercises (graded: ●○○ easy · ●●○ moderate · ●●● tough)

*Hints are here; worked answers are at the end of the chapter. Try first.*

**Easy — one idea, applied directly**

1. (●○○) **The parity of the leave.** Prove that in any packing on v points, every leave degree is ≡ v−1 mod 2. *Hint: each packed triple through a vertex x removes exactly two of x's pairs; the leave degree is (v−1) minus twice the number of packed triples through x. The machine: 50/50 random-greedy runs at Lecture 2's scales, and 20/20 at v = 9 (leave degrees all even) — the census of a theorem.*
2. (●○○) **The leave is divisible.** Prove that the leave of a packing on v points has \|L\| ≡ C(v,2) mod 3, and combine with Exercise 1 to close every optimum in Lecture 1's table by hand: show D(4) = 1, D(5) = 2, D(6) = 4, D(8) = 8, D(10) = 13. *Hint: \|L\| = C(v,2) − 3·(packed); at v = 5 the leave cannot have 1 edge (parity: degrees would be 1,1,0,0,0, but v−1 = 4 demands even degrees), and \|L\| ≡ 10 ≡ 1 mod 3, so \|L\| ≥ 4; at v = 10, ten odd degrees force \|L\| ≥ 5 and the residue forces \|L\| ≥ 6. The exhibits exist — lab Part 1 prints one per order, so each upper bound is tight.*
3. (●○○) **Codegree ratios by hand.** Compute the maximum codegree, the maximum degree D, and their ratio for: the Fano plane; AG(2,3); the balanced blow-up of the Fano plane with m twins per point (m = 3 gives the lab's 3/27 = 1/9). *Hint: in a Steiner system every pair has codegree exactly 1, so the ratio is 1/D; in the blow-up, a pair of twins-of-adjacent-points lies in m triples while each point's degree is 3m². The receipts: 1/3, 1/4, 1/(3m).*
4. (●○○) **Evaluating Shearer.** Evaluate Shearer's bound on the balanced blow-up of C₅ at m = 2 and m = 5 (n = 10, 25; d = 4, 10) and on the Clebsch graph (n = 16, d = 5), and check each against the exact α. *Hint: substitute into n(d ln d − d + 1)/(d−1)²; the receipts are 2.828, 4.329, 4.047 against truths 4, 10, 5. Then say in one sentence why the *ratio* bound/truth shrinks as d grows — the bound's (ln d − 1)/d shape against hosts whose α grows linearly in d.*

**Moderate — two ideas, or one tricky step**

5. (●●○) **Volume-4 trades are Pasch-shaped.** Call (T, T′) a *trade* if T ≠ T′ are sets of triples, each pair-disjoint (no pair in two triples of the same side), covering exactly the same pairs, with T ∩ T′ = ∅. Prove: if \|T\| = \|T′\| = 4, then both sides are Pasch configurations — four triples on six points, each point in exactly two. *Hint: sum of degrees is 12 on each side. A point of degree 1 in T lies in a triple {x,y,z}; the pairs xy, xz must be covered in T′, and any T′-triple through x covers two of x's pairs — so it covers both, hence contains y and z, hence equals xyz ∈ T ∩ T′, a contradiction. So all degrees ≥ 2, forcing all = 2 and exactly six points.*
6. (●●○) **The repair-impossibility theorem.** Deduce: in an anti-Pasch Steiner triple system S, no four triples of S can form one side of a volume-4 trade; conclude that no sequence of volume-4 trades of any length transforms a packing P (not already in S) into a subset of S, and that if \|P ∖ S\| ≤ 2 (as in all twenty receipts), no trade of any volume on the mismatched triples P ∖ S can repair P into S. *Hint: the last volume-4 trade in any successful sequence inserts only triples of S (everything later stays in S), and its new side is four triples of S covering twelve pairs — Exercise 5 makes it a Pasch in S, contradiction; moreover, any non-empty trade has volume ≥ 4, whereas \|P ∖ S\| ≤ 2 < 4.*
7. (●●○) **AG(2,3) is anti-Pasch.** Prove that four pairwise non-parallel lines of the affine plane F₃² always repeat an intersection point — so no Pasch configuration exists in AG(2,3), and (since STS(9) is unique up to isomorphism) none exists in any of the 840 systems. *Hint: three pairwise non-parallel lines are either concurrent or form a triangle. If they are concurrent at p, the three lines already repeat p, leaving at most 1 + 3 = 4 distinct pairwise intersection points among the four lines rather than the 6 required for a Pasch configuration. If they form a triangle, work the F₃ arithmetic: up to affine transformation, take the three lines to be x = 0, y = 0, and y = x + 1, whose vertices are (0,0), (0,1), and (2,0); a fourth line non-parallel to all three must have slope 2, i.e., y = 2x + b with b ∈ {0,1,2}, and each choice of b ∈ F₃ passes through one of those three triangle vertices. The machine verified all 840 systems Pasch-free, so your proof and the census agree.*
8. (●●○) **The conflict toll, by hand.** From Lecture 2's census (a₁..a₅ = 1.0000, 0.6136, 0.4716, 0.4148, 0.3580), compute λ_s = −ln(a_{s+1}/a_s)/a_s² for s = 1..4 and check against the receipts 0.488, 0.699, 0.577, 0.856; then verify the naive conflict-free value λ₀ = (v−2)/v = 0.9394 and explain in two sentences why the observed values oscillate across it. *Hint: a burst-kill — one selected triple culls several of a pair's completions at once — makes some rounds cheap (λ < λ₀) and others expensive; the naive model assumes independent single kills.*
9. (●●●) **The process envelope.** (a) Prove: a triangle-free graph on n vertices with α < t certifies R(3,t) > n. (b) Verify the receipts against the asymptotics: edges 124 and 402 against (1/(2√2))n^{3/2}√(ln n) = 107.1 and 332.5; Δ = 11 and 16 against √(n ln n) = 10.1 and 15.7 — and note the honest 16%/21% overshoot. (c) Apply Shearer to the n = 60 receipt graph (d̄ = 13.4: bound 8.732 against α = 17) and derive the constant-free conclusion: the triangle-free process yields α = Ω(√(n ln n)), hence R(3,t) = Ω(t²/log t). *Hint for (c): d̄ = 2E/n = (1/√2+o(1))√(n ln n) — compute n·(ln d̄)/d̄ with E = (1/(2√2))n^{3/2}√(ln n); the constant is not Kim's 1/4 — the delicate min-degree tracking Kim adds is exactly the gap between your Ω and his 1/4.*

**Tough — several ideas combined**

10. (●●●) **840 = 9!/432.** (a) Exhibit 432 automorphisms of AG(2,3): the affine maps x ↦ Ax + b with A ∈ GL(2,3), b ∈ F₃² — count \|GL(2,3)\| = (9−1)(9−3) = 48 and multiply by 9. (b) Explain why 9!/432 = 840 counts the labeled systems if all labeled systems are isomorphic (the orbit-stabilizer theorem; STS(9)'s uniqueness is the classical input, cited). (c) The receipt: the machine's exhaustive enumeration found exactly 840 — and 362880/840 = 432, so the census is consistent both ways. *The honest division of labor: exhibiting 432 automorphisms is the exercise; proving no more exist is delegated to the enumeration plus the classical isomorphism type.*
11. (●●●) **Packing tetrahedra.** A block of size 4 covers 4 triples; pack 4-blocks on v points so no triple sits in two blocks. Optima for v = 4..8: **1, 1, 3, 7, 14** (covered 4, 4, 12, 28, 56 triples; totals 4, 10, 20, 35, 56). (a) v = 5: prove two blocks always share a triple (pigeonhole: two 4-subsets of a 5-set meet in ≥ 3 points). (b) v = 6: prove 4 blocks are impossible — each point's leave-count is ≡ C(5,2) = 10 ≡ 1 mod 3 and at most 4, so the leave's 12 incidences force two points at 4 and four points at 1, meaning all four leave triples contain the same pair {e,f}; thus no block can contain {e,f}, forcing every block to take ≥ 3 points from the remaining 4-set (or equivalently, by complementation, 4-blocks sharing ≤ 2 points have pairwise-disjoint 2-element complements in the 6-set, of which at most 3 exist). (c) v = 7: prove 8 blocks impossible the same way (the leave would be 3 triples; every point's leave-count ≡ 0 mod 3 and ≤ 3 forces three points at 3 and four at 0, forcing all three leave triples to lie inside a 3-point set — but three points support only C(3,3) = 1 triple, not three). (d) v = 8: exhibit the SQS(8) (lab Part 1 prints one — 14 blocks, 56/56 triples) and note the counting bound ⌊56/4⌋ = 14 is tight. *This is Keevash's divisibility in miniature: the residues, not the bounds, do the work.*
12. (●●●) **Symmetric differences are trades.** Prove: if S₁ ≠ S₂ are Steiner triple systems on the same point set, then S₁ ∖ S₂ and S₂ ∖ S₁ cover exactly the same pairs (so they form a trade of volume \|S₁ ∖ S₂\|). *Hint: a pair whose S₁-triple lies in S₁ ∩ S₂ has its S₂-triple there too — uniqueness of the triple through a pair. Then read the census: volumes 6, 8, 9, 10, 11, 12 occur (15,120 pairs of systems at volume 6), while 4 is absent (Exercise 5 + anti-Pasch), 5 is classically impossible (trade theory), and 7's absence at n = 9 is an instance-level curiosity — ◐17 sends you hunting for a volume-7 trade at n = 13.*

**◆ Pattern unknown — no hint; diagnosing the tool is the problem**

◆13. The census table of Lecture 3 lists five structures with their codegree ratios and matching coverages: the windmill 1.000 → 25%, the three K₄³'s 0.667 → 75%, the Fano plane 0.333 → 43%, the Fano blow-up 0.111 → 100%, AG(2,3) 0.250 → 100%. Diagnose each structure's obstruction — or lack of one. (Which hypothesis of the nibble lemma dies, and where divisibility hides?)
◆14. On 9 points, no greedy packing extends to a complete system (0/20), no sequence of volume-4 trades can put one inside a system, and yet every packing completes after dropping at most 2 of its triples (20/20). Name the method class of the rescue, and say what it shares with Keevash's architecture.
◆15. Two lower-bound strategies for R(3,t): sample a random graph and delete one endpoint of every triangle; or grow a triangle-free graph edge by edge, always choosing among still-safe pairs. One reaches n ~ t²/log² t, the other (1/4)·t²/log t. Explain the gap as a pattern-level statement about where the randomness is exposed.

**◐ Explorations — state what you should find, not a number**

◐16. **Scale the nibble.** Run Part 3's nibble at v = 33, 51, 69 with p = 1/v. Watch three things: the leave fraction (does it keep falling — and how fast?), the round at which the observed census decouples from (v−2)a² (it should drift *later* as v grows), and the early λ_s range (narrowing toward the naive line?). You should find all three drifts; predicting their sizes is the real exploration.
◐17. **Hunt a volume-7 trade.** At n = 9 the inter-system trade volumes are {6, 8, 9, 10, 11, 12} — no 7. First exhibit a volume-6 trade between two labeled STS(9)s (the machine census says 15,120 pairs of systems realize one; find a pair and describe the shape — how many points does the 6-trade sit on?). Then move to n = 13: the cyclic system on Z₁₃ and a second, non-isomorphic copy — does a volume-7 trade exist between STS(13)s? (Trade theory says volume 7 exists in the abstract; the question is whether it fits at these small orders.)
◐18. **Sacrifice distance at n = 13.** Sample random greedy packings on 13 points and measure how many triples must be dropped before the remainder sits inside a fixed STS(13) (use the cyclic system as the template). At n = 9 the answer was ≤ 2, always. You should find the distance grows with n — and the growth is the quantitative shadow of why Keevash needs a genuine absorber rather than a fixed template.

## Computational Lab (verified)

*Every run below uses the chapter's documented engine: the Lehmer generator x ← 48271·x mod (2³¹−1), seed 20261081 (run i of a family uses seed 20261081+i), Fisher–Yates with one draw per index, candidate scans in lexicographic order. The printed Python reproduces every receipt bit for bit. The engine's own bug history — the receipts caught two search bugs and one unsound bound this session — is in the Trick Bag's scar list and the Verification Notes.*

### Part 1 — The packing optima, proved and exhibited (Lecture 1)

The optima below are *proved* by the counting bound plus the leave's parity and residue (Exercises 1–2 do the arithmetic per order); the machine's job is to exhibit packings achieving them and to verify every invariant. The finder is a branch-and-bound that branches cover-first, then on leaving the first uncovered pair (the scar list explains why the leave-branch is not optional), stopping at the proven target.

```python
def find_packing(v, target):          # exhibit search, early stop at the target
    if v < 3: return [] if target <= 0 else None
    pairs = [(a, b) for a in range(v) for b in range(a+1, v)]
    pid = {p: i for i, p in enumerate(pairs)}
    def PI(a, b): return pid[(min(a,b), max(a,b))]
    np = len(pairs)
    cov, deg, cur, hit = [0]*np, [v-1]*v, [], [None]
    def ub():                          # parity-aware capacity: sum floor(r_x/2)/3
        return sum(r//2 for r in deg)//3
    def rec(cnt, start):
        if hit[0] is not None: return
        free = next((i for i in range(start, np) if not cov[i]), None)
        if free is None:                 # scanned past every pair
            if cnt == target: hit[0] = cur[:]   # leave allowed — that's the point
            return
        if cnt + min(ub(), (np - 3*cnt)//3) < target: return
        a, b = pairs[free]
        for c in range(v-1, -1, -1):   # cover branches first (dive)
            if c in (a, b): continue
            q1, q2 = PI(a, c), PI(b, c)
            if cov[q1] or cov[q2]: continue
            for q in (free, q1, q2): cov[q] = 1
            deg[a] -= 2; deg[b] -= 2; deg[c] -= 2; cur.append((a, b, c))
            rec(cnt+1, free+1)
            for q in (free, q1, q2): cov[q] = 0
            deg[a] += 2; deg[b] += 2; deg[c] += 2; cur.pop()
        rec(cnt, free+1)               # the LEAVE branch
    rec(0, 0)
    return hit[0]

def verify(v, triples):               # pair-disjointness + leave invariants
    pairs = [(a, b) for a in range(v) for b in range(a+1, v)]
    pid = {p: i for i, p in enumerate(pairs)}
    cov = [0]*len(pairs)
    for a, b, c in triples:
        a, b, c = sorted((a, b, c))
        for q in (pid[(a,b)], pid[(a,c)], pid[(b,c)]):
            assert not cov[q], "pair clash"; cov[q] = 1
    ld = [0]*v
    for i, (a, b) in enumerate(pairs):
        if not cov[i]: ld[a] += 1; ld[b] += 1
    assert all(d % 2 == (v-1) % 2 for d in ld), "parity"
    return len(pairs) - 3*len(triples), sorted((d for d in ld if d), reverse=True)

def find_tetra_packing(v, target):    # t = 3, k = 4 block search (Exercise 11)
    if v < 4: return [] if target <= 0 else None
    tri = [(a,b,c) for a in range(v) for b in range(a+1,v) for c in range(b+1,v)]
    tid = {t: i for i, t in enumerate(tri)}
    blocks = [(a,b,c,d) for a in range(v) for b in range(a+1,v)
              for c in range(b+1,v) for d in range(c+1,v)]
    bt = [(tid[(a,b,c)], tid[(a,b,d)], tid[(a,c,d)], tid[(b,c,d)])
          for a,b,c,d in blocks]
    nt = len(tri); cov = [0]*nt; cur = []; hit = [None]
    through = [[] for _ in range(nt)]
    for b_idx, ts in enumerate(bt):
        for t_idx in ts: through[t_idx].append(b_idx)
    def rec(cnt, start):
        if hit[0] is not None: return
        free = next((i for i in range(start, nt) if not cov[i]), None)
        if free is None:
            if cnt == target: hit[0] = [blocks[b] for b in cur]
            return
        if cnt + (nt - 4*cnt)//4 < target: return
        for b_idx in through[free]:
            ts = bt[b_idx]
            if any(cov[t_idx] for t_idx in ts): continue
            for t_idx in ts: cov[t_idx] = 1
            cur.append(b_idx); rec(cnt+1, free+1); cur.pop()
            for t_idx in ts: cov[t_idx] = 0
        rec(cnt, free+1)
    rec(0, 0)
    return hit[0]
```

Receipts (targets from the proved bounds; exhibits found and verified; block-search for the tetrahedra of Exercise 11, t = 3, k = 4):

- **Triple packings, v = 4..10: optima 1, 2, 4, 7, 8, 12, 13** (leaves 3, 4, 3, 0, 4, 0, 6; bound floors ⌊C(v,2)/3⌋ = 2, 3, 5, 7, 9, 12, 15). Leave degree sequences: v = 4 [3,1,1,1] (star); v = 5 [2,2,2,2] (4-cycle); v = 6 [1,1,1,1,1,1] (perfect matching); v = 8 [1×8] (matching); v = 10 [3,1,1,1,1,1,1,1,1,1] — exactly the shapes the parity-plus-residue analysis demands. Exhibits (v = 10, 13 triples): 019, 028, 037, 046, 127, 138, 145, 236, 249, 359, 478, 568, 679.
- **Tetrahedra (t = 3, k = 4), v = 4..8: optima 1, 1, 3, 7, 14** (triples covered 4, 4, 12, 28, 56 of totals 4, 10, 20, 35, 56; bound floors 1, 2, 5, 8, 14 — tight only at v = 4 and 8). v = 8 is the SQS(8): 14 blocks covering 56/56 — 0123, 0145, 0167, 0246, 0257, 0347, 0356, 1247, 1256, 1346, 1357, 2345, 2367, 4567. v = 6 exhibit: 0123, 0145, 2345; v = 7 exhibit: 0123, 0145, 0246, 0356, 1256, 1346, 2345.

### Part 2 — The random greedy (Lecture 2)

```python
def rng(seed):                          # the engine: Lehmer MINSTD
    x = [seed]
    def nxt():
        x[0] = 48271 * x[0] % 2147483647
        return x[0] / 2147483647
    return nxt

def greedy_run(v, seed):                # uniform pick among available triples
    R, pairs = rng(seed), [(a,b) for a in range(v) for b in range(a+1,v)]
    pid = {p: i for i, p in enumerate(pairs)}
    trip = [(a,b,c) for a in range(v) for b in range(a+1,v) for c in range(b+1,v)]
    tp = [(pid[(a,b)], pid[(a,c)], pid[(b,c)]) for a,b,c in trip]
    cov = [0]*len(pairs)
    while True:
        cand = [t for t in range(len(trip))
                if not cov[tp[t][0]] and not cov[tp[t][1]] and not cov[tp[t][2]]]
        if not cand: break
        t = cand[int(R()*len(cand))]    # one draw, uniform
        for q in tp[t]: cov[q] = 1
    ld = [0]*v; unc = 0
    for i,(a,b) in enumerate(pairs):
        if not cov[i]: unc += 1; ld[a] += 1; ld[b] += 1
    assert all(d % 2 == (v-1) % 2 for d in ld)   # parity lemma, every run
    return unc/len(pairs)

for v in (15, 21, 27, 33, 39):
    fr = [greedy_run(v, 20261081+i) for i in range(10)]
    print(v, sum(fr)/10)
```

Receipts — mean leave fraction over ten runs each, parity lemma 50/50 runs: **v = 15: 0.1714 · v = 21: 0.1329 · v = 27: 0.1333 · v = 33: 0.1142 · v = 39: 0.1045.** (The v = 21 → 27 inversion is sampling noise, ten runs, per-run sd ≈ 0.06 — printed as run, not smoothed.)

### Part 3 — The nibble, tracked (Lectures 2–3)

```python
import math

def nibble(v, p, seed):                 # select w.p. p, shuffle, cull, accept
    if v < 3: return 0, 0, [], []
    R, pairs = rng(seed), [(a,b) for a in range(v) for b in range(a+1,v)]
    pid = {p_: i for i, p_ in enumerate(pairs)}
    trip = [(a,b,c) for a in range(v) for b in range(a+1,v) for c in range(b+1,v)]
    tp = [(pid[(a,b)], pid[(a,c)], pid[(b,c)]) for a,b,c in trip]
    cov, rows, a_hist, r = [0]*len(pairs), [], [], 0
    while True:
        avail = [t for t in range(len(trip))
                 if not cov[tp[t][0]] and not cov[tp[t][1]] and not cov[tp[t][2]]]
        if not avail: break             # exhaustion — NOT the empty selection
        a = sum(1 for q in cov if not q)/len(pairs)
        a_hist.append(a)
        obs = 0; nun = 0                # census: completions per uncovered pair
        for i,(x,y) in enumerate(pairs):
            if cov[i]: continue
            nun += 1
            obs += sum(1 for c in range(v) if c not in (x,y)
                       and not cov[pid[(min(x,c),max(x,c))]]
                       and not cov[pid[(min(y,c),max(y,c))]])
        obs /= nun
        if r+1 in (1,2,3,4,5,14,20,30):
            rows.append((r+1, round(a,4), round(obs,2), round((v-2)*a*a,2)))
        sel = [t for t in avail if R() < p]          # one draw per available
        for k in range(len(sel)-1, 0, -1):           # Fisher–Yates
            j = int(R()*(k+1)); sel[k], sel[j] = sel[j], sel[k]
        for t in sel:                               # cull conflicts, accept
            if not cov[tp[t][0]] and not cov[tp[t][1]] and not cov[tp[t][2]]:
                for q in tp[t]: cov[q] = 1
        r += 1
    lams = [round(-math.log(a_hist[s+1]/a_hist[s])/(a_hist[s]**2), 3)
            for s in range(min(10, len(a_hist)-1))]
    return r, sum(1 for q in cov if not q), rows, lams
```

Receipts (v = 33, p = 1/33, seed 20261081): **65 rounds, leave 60 pairs (0.1136)** — beating the random greedy's v = 33 mean (0.1142). The census (round, availability a, observed completions, mean-field (v−2)a²): **(1, 1.0000, 31.00, 31.00) · (2, 0.6136, 11.72, 11.67) · (3, 0.4716, 6.95, 6.89) · (4, 0.4148, 5.36, 5.33) · (5, 0.3580, 3.79, 3.97) · (14, 0.1989, 1.31, 1.23) · (20, 0.1761, 0.81, 0.96) · (30, 0.1591, 0.57, 0.78)** — mean-field exact while the profile is uniform, decoupling *below* the line in the endgame. The decay coefficients λ_s = −ln(a_{s+1}/a_s)/a_s², first ten: **0.488, 0.699, 0.577, 0.856, 0.512, 0.464, 0.924, 0.973, 0.610, 1.424**, oscillating across the naive conflict-free λ₀ = (v−2)/v = 0.9394 — the conflict toll made visible.

### Part 4 — The codegree census (Lecture 3)

```python
def census(name, pts, tri):             # degrees, codegrees, exact max matching
    if pts < 3 or not tri: return
    deg = [0]*pts
    for a, b, c in tri: deg[a] += 1; deg[b] += 1; deg[c] += 1
    codeg = {}
    for a, b, c in tri:
        for x, y in ((a,b),(a,c),(b,c)):
            k = (min(x,y), max(x,y)); codeg[k] = codeg.get(k, 0) + 1
    used, best = [0]*pts, [0]
    def rec(cnt, start):
        best[0] = max(best[0], cnt)      # incumbent only ever moves up
        if cnt + sum(1 for u in used if not u)//3 <= best[0]: return
        for t in range(start, len(tri)):
            a, b, c = tri[t]
            if used[a] or used[b] or used[c]: continue
            used[a] = used[b] = used[c] = 1
            rec(cnt+1, t+1)
            used[a] = used[b] = used[c] = 0
    rec(0, 0)
    D, C = max(deg), max(codeg.values())
    print(name, "D =", D, "codeg =", C, "ratio", round(C/D, 3),
          "match covers", round(3*best[0]/pts, 4))

fano = sorted((i%7, (i+1)%7, (i+3)%7) for i in range(7))
census("W10 windmill", 12, [(0, 1, i+2) for i in range(10)])
census("3xK4^3", 12, [tuple(p for p in range(4*g, 4*g+4) if p != 4*g+i)
                     for g in range(3) for i in range(4)])
census("Fano", 7, fano)
census("Fano blow-up m=3", 21, [(3*x+i, 3*y+j, 3*z+k)
                                for x,y,z in fano for i in range(3)
                                for j in range(3) for k in range(3)])
ag = ([(3*s, 3*s+1, 3*s+2) for s in range(3)]             # vertical
    + [(s, 3+s, 6+s) for s in range(3)]                  # horizontal
    + [(s, 3+(s+m)%3, 6+(s+2*m)%3) for m in (1, 2) for s in range(3)])
census("AG(2,3)", 9, ag)
```

Receipts — the morality table, exact: **W₁₀: D = 10, codeg 10, ratio 1.000, matching covers 25% · 3 × K₄³: D = 3, codeg 2, ratio 0.667, 75% · Fano: D = 3, codeg 1, ratio 0.333, 43% (3/7) · Fano blow-up m = 3: D = 27, codeg 3, ratio 0.111, 100% · AG(2,3): D = 4, codeg 1, ratio 0.250, 100%.** The windmill dies regularity, the Fano plane codegree, the blow-up survives both, and AG(2,3)'s parallel classes tile perfectly despite a toy-scale ratio of 1/4.

### Part 5 — The ancestors: hosts and the triangle-free process (Lecture 4)

```python
import math

def shearer(n, d):
    if d <= 1: return float(n)
    return n*(d*math.log(d) - d + 1)/(d-1)**2

def alpha_exact(n, adj):                # max clique on the complement
    if n <= 0: return 0
    comp = [[b for b in range(n) if b != a and b not in adj[a]]
            for a in range(n)]
    best = [0]
    def cliq(cand, cnt):
        best[0] = max(best[0], cnt)
        if not cand or cnt + len(cand) <= best[0]: return
        cols, colof = [], [-1]*n
        for x in cand:                  # greedy coloring: sound bound FOR CLIQUES
            used = {colof[y] for y in comp[x] if colof[y] >= 0}
            c = 0
            while c in used: c += 1
            colof[x] = c
            if c == len(cols): cols.append([x])
            else: cols[c].append(x)
        if cnt + len(cols) <= best[0]: return
        for ci in range(len(cols)-1, -1, -1):
            if cnt + ci + 1 <= best[0]: return
            for v in cols[ci]:
                cliq([x for x in cand if x != v and x in comp[v]], cnt+1)
                cand = [x for x in cand if x != v]
                if not cand: return
    cliq(list(range(n)), 0)
    return best[0]

for m in (2, 3, 4, 5):                  # balanced blow-up of C5: twins
    n = 5*m
    adj = [[] for _ in range(n)]
    for i in range(5):
        for j in range(m):
            for nb in ((i+4) % 5, (i+1) % 5):
                adj[i*m+j] += [nb*m+k for k in range(m)]
    print("C5 blow-up m=%d: alpha = %d, Shearer %.3f"
          % (m, alpha_exact(n, adj), shearer(n, 2*m)))

clebsch_adj = [[y for y in range(16) if bin(x ^ y).count("1") in (1, 4)]
              for x in range(16)]
print("Clebsch: alpha = %d, Shearer %.3f"
      % (alpha_exact(16, clebsch_adj), shearer(16, 5)))

def tfp(n, seed):                       # the triangle-free process
    if n < 2: return set(), [[] for _ in range(n)]
    R = rng(seed); adj = [[] for _ in range(n)]; E = set()
    while True:
        cand = []
        for a in range(n):
            for b in range(a+1, n):
                if (a, b) in E or set(adj[a]) & set(adj[b]): continue
                cand.append((a, b))
        if not cand: break
        a, b = cand[int(R()*len(cand))]
        E.add((a, b)); adj[a].append(b); adj[b].append(a)
    return E, adj
```

Receipts: **blow-up hosts α = 4, 6, 8, 10 at m = 2..5 (Shearer 2.828, 3.450, 3.933, 4.329 — the ratio bound/truth falls 0.71 → 0.43, the asymptotic bound's honest shape); Clebsch (F₂⁴, adjacency at distances 1 and 4): 5-regular, triangle-free, α = 5, Shearer 4.047, witness {0010, 0100, 0111, 1001, 1110}.** The process (seed 20261081): **n = 30: 124 edges, Δ = 11, d̄ = 8.2667, α = 11 ⇒ R(3,12) > 30 (Shearer guarantees 5.792; asymptotic curves: edges 107.1, Δ 10.1); n = 60: 402 edges, Δ = 16, d̄ = 13.4, α = 17 ⇒ R(3,18) > 60 (Shearer 8.732; curves: 332.5, 15.7)** — the receipts sit 16% and 21% above the edge asymptotics, the honest small-n overshoot; the exact-α sanity check for the search itself is the Petersen graph (α = 4).

### Part 6 — Designs in miniature: the absorption wall (Lecture 6)

```python
def systems9():                          # all labeled STS(9), exact cover
    trip = [(a,b,c) for a in range(9) for b in range(a+1,9) for c in range(b+1,9)]
    tid = {t: i for i, t in enumerate(trip)}
    tp = [tuple(sorted(((a,b),(a,c),(b,c)))) for a,b,c in trip]
    pid = {p: i for i, p in enumerate((a,b) for a in range(9) for b in range(a+1,9))}
    tp = [tuple(pid[p] for p in t) for t in tp]
    cov, cur, out = [0]*36, [], []
    through = [[] for _ in range(36)]
    for t, qs in enumerate(tp):
        for q in qs: through[q].append(t)
    def rec():
        q = next((i for i in range(36) if not cov[i]), None)
        if q is None: out.append(cur[:]); return
        for t in through[q]:
            if any(cov[x] for x in tp[t]): continue
            for x in tp[t]: cov[x] = 1
            cur.append(t); rec(); cur.pop()
            for x in tp[t]: cov[x] = 0
    rec(); return out, trip, tp

def pasch_free(S, trip):                 # any 4 triples on 6 points, all deg 2?
    for i in range(12):
        for j in range(i+1, 12):
            for k in range(j+1, 12):
                for l in range(k+1, 12):
                    deg = {}
                    for t in (S[i], S[j], S[k], S[l]):
                        for p in trip[t]: deg[p] = deg.get(p, 0) + 1
                    if len(deg) == 6 and all(d == 2 for d in deg.values()):
                        return False
    return True

def trade_volumes(systems):              # |S1 \ S2| histogram, all pairs
    hist = {}
    for i in range(len(systems)):
        for j in range(i+1, len(systems)):
            t = 12 - len(set(systems[i]) & set(systems[j]))
            hist[t] = hist.get(t, 0) + 1
    return hist

def greedy9(seed):                       # variant C: random pair order,
    R = rng(seed)                        # random available completion each
    pairs = [(a,b) for a in range(9) for b in range(a+1,9)]
    order = list(range(36))
    for k in range(35, 0, -1):           # Fisher–Yates
        j = int(R()*(k+1)); order[k], order[j] = order[j], order[k]
    pid = {p: i for i, p in enumerate(pairs)}
    cov, packed = [0]*36, []
    for q in order:
        if cov[q]: continue
        a, b = pairs[q]
        cand = [c for c in range(9) if c not in (a, b)
                and not cov[pid[(min(a,c),max(a,c))]]
                and not cov[pid[(min(b,c),max(b,c))]]]
        if not cand: continue            # the pair is stranded
        c = cand[int(R()*len(cand))]
        for p in ((a,b),(min(a,c),max(a,c)),(min(b,c),max(b,c))): cov[pid[p]] = 1
        packed.append(tuple(sorted((a, b, c))))
    return packed
```

Receipts (seed 20261081+i, i = 0..19):

- **The census: 840 labeled systems = 9!/432 exactly** (Exercise 10); **all 840 are anti-Pasch** (0 systems contain a Pasch configuration — Exercise 7's F₃ case analysis, machine-confirmed); **the volume-4 trade {012, 034, 135, 245} ↔ {013, 024, 125, 345} covers the same 12 pairs** (identity verified).
- **Inter-system trade volumes:** histogram over all 352,380 pairs of systems — **volume 6: 15,120 · 8: 11,340 · 9: 63,840 · 10: 90,720 · 11: 90,720 · 12: 80,640; volumes 4, 5, 7 absent.** Four is the anti-Pasch wall (Exercise 5); five is classical trade theory; seven's absence is the instance-level curiosity of ◐17.
- **Greedy (variant C), 20 runs: packed ∈ {9, 10}, mean 9.50; leave ∈ {6, 9}, mean 7.5; leave degrees all even, 20/20 (parity lemma).**
- **Direct completion: 0/20** — no run's packing extends to a full system.
- **Template absorption: 20/20 within ≤ 2 sacrifices** — the maximum overlap between a run's packing and some single system is kept ∈ {7, 8, 9} (mean 7.85), so the sacrifice distance packed − kept ∈ {1, 2} (mean 1.65, seven runs at 1, thirteen at 2). Since the minimum trade volume is 4 (Exercise 5) and every packing sits within 2 triples of a system, **no trade of any volume on the mismatched triples completes these packings — sacrifice is provably the only route** (Exercise 6): Keevash's template+absorber, in miniature.

## Answers to the Exercises

*Worked answers for the twelve graded problems and the three ◆ pattern-unknown ones. The three ◐ Explorations state what you should find and get no worked answer — that is their point. Where an answer cites a machine receipt, the receipt exists: the lab above, from the chapter's single documented engine (seed 20261081).*

**Answer 1 (parity of the leave).** Fix a vertex x. Of the v−1 pairs through x, each packed triple {x, y, z} consumes exactly two — (x,y) and (x,z) — and any triple not through x consumes none. So the leave degree of x is (v−1) − 2·(#packed triples through x) ≡ v−1 mod 2. The odd orders v = 15, 21, 27, 33, 39 give v−1 even: every leave is an even-degree (Eulerian) graph, which is why a stranded pair still cannot be completed greedily — its completions were consumed pairwise. Receipts: 50/50 greedy runs; 20/20 at v = 9.

**Answer 2 (the leave is divisible).** Write P for the packing and L for the leave: C(v,2) = 3|P| + |L|, so |L| ≡ C(v,2) mod 3. Combined with Answer 1:
- **v = 4:** C(4,2) = 6, so |L| ≡ 0 mod 3; |L| = 0 would mean two edge-disjoint triangles covering K₄, impossible (any two triangles in K₄ share an edge); |L| = 3 is admissible (the star K₁,₃, degrees 3,1,1,1 all odd ✓). So D(4) = (6−3)/3 = **1**.
- **v = 5:** |L| ≡ 10 ≡ 1 mod 3. |L| = 1 needs degree-1 endpoints — even degrees demanded, contradiction. So |L| ≥ 4: D(5) ≤ 2, and the 4-cycle leave is realized by two triples (lab exhibit: 014, 023): D(5) = **2**.
- **v = 6:** |L| ≡ 0 mod 3; all degrees odd ⇒ all six ≥ 1 ⇒ |L| ≥ 3: D(6) ≤ 4; the perfect-matching leave is realized (exhibit 015, 024, 123, 345): D(6) = **4**.
- **v = 8:** |L| ≡ 1 mod 3; eight odd degrees ⇒ |L| ≥ 4: D(8) ≤ 8; realized by the matching-leave exhibit: D(8) = **8**.
- **v = 10:** |L| ≡ 0 mod 3; ten odd degrees ⇒ |L| ≥ 5, so |L| ≥ 6: D(10) ≤ 13; realized (the 13-triple exhibit, leave degree sequence [3,1,1,1,1,1,1,1,1,1]): D(10) = **13**.
The counting bound alone gives 2, 3, 5, 9, 15 — parity and residue shave exactly the difference every time: divisibility is doing the work (P41).

**Answer 3 (codegree ratios).** Fano: each pair lies in exactly one line (Steiner), so max codegree = 1, D = 3, ratio 1/3. AG(2,3): Steiner again; D = 4 (each point on 4 lines), ratio 1/4. Fano blow-up with m twins: a pair of twins (x_i, y_j) whose base points share a line {x, y, z} lies in exactly the m triples {x_i, y_j, z_k} — max codegree m; each point lies on 3 base lines, each blown up to m² triples through the point, so D = 3m²; ratio 1/(3m) → 0. The receipts: m = 3 gives D = 27, codegree 3, ratio 0.111 — the census's survivor.

**Answer 4 (evaluating Shearer).** Substituting n(d ln d − d + 1)/(d−1)²: blow-up m = 2: 10(4 ln 4 − 3)/9 = 2.828 against α = 4; m = 5: 25(10 ln 10 − 9)/81 = 4.329 against α = 10; Clebsch: 16(5 ln 5 − 4)/16 = 4.047 against α = 5. The bound holds everywhere (as it must — it is a theorem) and the ratio bound/truth shrinks as d grows because Shearer's guarantee has the (ln d − 1)/d *shape* — designed for sparse random-like graphs whose α is a small fraction of n — while the blow-up hosts' α = 2m grows linearly in d = 2m, i.e., as a constant fraction of n. The bound is honest, not tight: its tightness lives at the Ramsey-critical sparsity of Lecture 4's process graphs.

**Answer 5 (volume-4 trades are Pasch-shaped).** Let (T, T′) be a trade, |T| = |T′| = 4, sides pair-disjoint, pair sets equal, T ∩ T′ = ∅. The 12 pair-slots of T distribute over its point set; write d(x) for x's T-degree; Σd(x) = 12. Suppose some d(x) = 1, say x's only T-triple is {x,y,z}. The pairs (x,y), (x,z) are covered in T′, and since x occurs in T′-triples covering exactly the pairs (x,y), (x,z) (pair sets are equal), some T′-triple contains x and covers two of x's pairs — it must contain both y and z, hence is {x,y,z} ∈ T ∩ T′: contradiction. So all degrees ≥ 2; Σ = 12 forces all exactly 2, on exactly 6 points — the Pasch configuration; by symmetry the same holds for T′. ∎ (The classical trade-theory fact — volume 4 is Pasch, volume 5 impossible — is the cited general form; this exercise proves the instance needed for Answer 6.)

**Answer 6 (repair impossibility).** Suppose a non-empty sequence of volume-4 trades transforms P into P_final ⊆ S, and consider the last effective trade (T_old → T_new): T_new ⊆ P_final ⊆ S (any T_new-triple outside S would have to be removed by a later trade — there is none), and T_old covers the same 12 pairs as T_new with T_old ∩ T_new = ∅. Thus T_new is a set of 4 pair-disjoint triples of S covering the same 12 pairs as T_old; by Answer 5, T_new is a Pasch configuration *inside S* — contradicting S anti-Pasch (Answer 7). So the last volume-4 trade cannot exist, and no sequence of volume-4 trades completes P into S. Furthermore, any non-empty trade (T, T′) with T ∩ T′ = ∅ has volume |T| = |T′| ≥ 4: by Answer 5's degree argument, every point in V(T) has degree ≥ 2 in T, and since two triples of T share at most one point, any triple {x,y,z} ∈ T requires at least two further triples through y and z plus a fourth to close their degrees (3 pair-disjoint triples on ≥ 6 vertices have only 9 < 12 incidences). In the receipts, every greedy packing satisfies |P ∖ S| ≤ 2 < 4 = the minimum possible trade volume, so no trade of any volume on the mismatched triples P ∖ S can exist, and the 20/20 completions all go through sacrifice: drop the ≤ 2 mismatched triples and regrow inside the template system. ∎

**Answer 7 (AG(2,3) is anti-Pasch).** A Pasch configuration consists of 4 triples on 6 points such that every point has degree 2 (lies in 2 of the 4 triples). Consequently, no two of the 4 triples can be disjoint: the 4 triples have 4 × 3 = 12 point-incidences, and by inclusion-exclusion on 6 points of degree 2, there are 6 pairwise intersections among the 4 triples, which equals C(4,2) = 6, so every pair of the 4 triples intersects in exactly 1 point, and no point lies in 3 of the triples. In the affine plane AG(2,3) = F₃², two lines intersect in 1 point if and only if they have distinct slopes (are non-parallel). Since F₃² has 4 parallel classes (slopes m ∈ {0, 1, 2, ∞}), any 4 pairwise intersecting lines L₁, L₂, L₃, L₄ must represent all 4 distinct slope classes. Consider the first three lines L₁, L₂, L₃. Because their slopes are pairwise distinct, L₁ ∩ L₂ = {A}, L₁ ∩ L₃ = {B}, and L₂ ∩ L₃ = {C}. If L₁, L₂, L₃ are concurrent (A = B = C), then three lines already share a point of degree 3, so they cannot form part of a Pasch configuration. If A, B, C are distinct, the affine group AGL(2,3) acts transitively on non-collinear ordered triples of points (since GL(2,3) acts transitively on bases of F₃²), so up to an affine automorphism we may take A = (0,0), B = (0,1), and C = (2,0). Then L₁ = AB is the line x = 0 (slope ∞, points {(0,0),(0,1),(0,2)}), L₂ = AC is y = 0 (slope 0, points {(0,0),(1,0),(2,0)}), and L₃ = BC is y = x + 1 (slope 1, points {(0,1),(1,2),(2,0)}). The fourth line L₄ must belong to the remaining slope class m = 2, so L₄ has equation y = 2x + b for some b ∈ F₃ = {0, 1, 2}. Evaluating the three choices of b over F₃: for b = 0, (0,0) = A ∈ L₄; for b = 1, (0,1) = B ∈ L₄; for b = 2, setting x = 2 gives y = 2(2) + 2 = 6 ≡ 0 mod 3, so (2,0) = C ∈ L₄. In every case, L₄ passes through one of the triangle vertices A, B, or C, creating a point of degree 3 among {L₁, L₂, L₃, L₄} and leaving only 5 distinct points on the union of the 4 lines instead of 6. Thus AG(2,3) contains no Pasch configuration, and since every STS(9) is isomorphic to AG(2,3), all 840 labeled STS(9)s are anti-Pasch. ∎

**Answer 8 (the conflict toll).** λ₁ = −ln(0.6136)/1² = 0.488; λ₂ = −ln(0.4716/0.6136)/0.6136² = 0.699; λ₃ = −ln(0.4148/0.4716)/0.4716² = 0.577; λ₄ = −ln(0.3580/0.4148)/0.4148² = 0.856 — matching the receipts to three places. The naive model treats a pair's survival as 1 − p·(v−2)a², i.e., each completion dies independently: a_{s+1} = a_s(1 − p(v−2)a_s²), giving λ ≈ p(v−2) = (v−2)/v = 0.9394. The observed values oscillate across 0.9394 because deaths are not independent: one *accepted* triple kills three pairs at once (a burst — some rounds overshoot), while heavy selection rounds cull each other into mutual conflicts (some rounds undershoot). The mean-field (v−2)a² census tracks the *average* availability well (Lecture 2's table) precisely because bursts and duds average out — it is the *variance*, the λ-oscillation, that a real proof must bound (Lecture 3's lemma).

**Answer 9 (the process envelope).** (a) A triangle-free graph on n vertices with α < t is, by definition, a graph avoiding both K₃ and an independent t-set, so R(3,t) exceeds n. (b) (1/(2√2))·30^{3/2}·√(ln 30) = 0.35355·164.32·1.8442 = 107.1 against 124 (ratio 1.16); √(30 ln 30) = 10.1 against 11 (1.09). At n = 60: 332.5 against 402 (1.21); 15.7 against 16 (1.02). The receipts overshoot the asymptotic edge count by 16–21% at these tiny scales — the finite-n process is *denser* than its limit curve predicts; the Δ receipts close to within 2–9%. (c) For the n = 60 graph: d̄ = 2·402/60 = 13.4, Shearer gives α ≥ 60(13.4 ln 13.4 − 12.4)/12.4² = 8.732 (receipt; truth 17 — the receipt graph is far from Shearer-tight). Asymptotically, the process ends with E = (1/(2√2)+o(1))n^{3/2}√(ln n) edges, so d̄ = 2E/n = (1/√2+o(1))·n^{1/2}√(ln n), and Shearer's bound gives

  α ≥ n·(ln d̄)/d̄ = (√2 + o(1))·√(n/ln n)·(½ ln n + O(ln ln n)) = (1/√2 + o(1))·√(n ln n),

so the process graph has α ≥ (1/√2 + o(1))·√(n ln n) — Shearer's floor on the process's own degree profile. The certificate direction: R(3,t) > n demands a triangle-free graph with α < t, and Shearer *lower-bounds* α, so the floor blocks the certificate once (1/√2)√(n ln n) ≥ t; treating the floor as if it were the graph's true independence, the usable range is n with (1/√2)√(n ln n) < t, i.e., n < 2t²/ln t: the constant-free conclusion R(3,t) = Ω(t²/log t). (The constant is deliberately untracked: the receipts show the graph's true α sits above the Shearer floor, and turning the Ω into the explicit (1/4−o(1)) is exactly the delicate minimum-degree tracking Kim's theorem adds; the Ω is all this exercise claims, honestly.) ∎

**Answer 10 (840 = 9!/432).** (a) An affine map x ↦ Ax + b (A invertible over F₃) permutes points and carries lines to lines (affine images of {p, p+u, p+2u} are {Ap+b, Ap+Au+b, Ap+2Au+b} — again a line), so AGL(2,3) ⊆ Aut(AG(2,3)). Count: b is free (9 choices); A ∈ GL(2,3): first column any nonzero vector (8), second column any vector not in the first's span (6): |GL(2,3)| = 48. Total 9·48 = 432. (b) STS(9) is unique up to isomorphism (classical; cited), so the 9! labeled systems form one orbit under relabeling; each system's stabilizer is its automorphism group, of order 432, giving 9!/432 = 840 labeled systems. (c) The exhaustive enumeration found exactly 840 systems — and independently 362880/840 = 432, so the census and the group theory agree twice. The honest division of labor stands: the exercise exhibits 432 automorphisms; the *nonexistence of more* is the enumeration's verdict plus the classical isomorphism type, not proved here. ∎

**Answer 11 (packing tetrahedra).** A 4-block covers C(4,3) = 4 triples; two blocks conflict if and only if they share at least 3 points (a triple). (a) v = 5: two 4-subsets of a 5-set intersect in ≥ 4 + 4 − 5 = 3 points, i.e., share a triple. So one block is optimal — and one exists: D(5,4,3) = 1 (the counting bound ⌊10/4⌋ = 2 is not achieved). (b) v = 6: suppose 4 blocks existed on V = {0,1,2,3,4,5}, covering 16 of the 20 triples; the leave L has |L| = 4 triples carrying 12 point-incidences. Each point x lies in C(5,2) = 10 triples in total, and each block through x covers C(3,2) = 3 of them, so x's leave-count l(x) satisfies l(x) ≡ 10 ≡ 1 mod 3 and l(x) ≤ |L| = 4. Thus every leave-count is 1 or 4; summing Σl(x) = 12 forces two points e, f at l(e) = l(f) = 4 and four points a, b, c, d at 1. Since |L| = 4 and l(e) = l(f) = 4, every leave triple contains both e and f, so L is the set of all four triples through {e,f}: {efa, efb, efc, efd}. Consequently, no packed block can contain both e and f (any such block would cover two triples through {e,f}), so each of the 4 blocks takes at most one point from {e,f} and at least 3 points from {a,b,c,d}. By the pigeonhole principle, among 4 blocks each taking ≥ 3 points from {a,b,c,d}, either two share the same 3-subset of {a,b,c,d}, or at least two contain the same element of {e,f} (say e) and their 3-subsets of {a,b,c,d} — any two of which meet in ≥ 3 + 3 − 4 = 2 points {u,w} — share the triple {e,u,w}. (Equivalently, two 4-blocks on 6 points intersect in ≤ 2 points iff their 2-element complements are disjoint, and a 6-set holds at most ⌊6/2⌋ = 3 disjoint pairs.) Contradiction: D(6,4,3) = 3, as the exhibit {0123, 0145, 2345} attests. (c) v = 7: 8 blocks would cover 32 of 35 triples, leaving |L| = 3 triples = 9 incidences; each point's leave-count is ≡ C(6,2) = 15 ≡ 0 mod 3 and at most 3 (only three leave triples exist), so exactly three points sit at 3 and four at 0, forcing all three leave triples to lie inside a 3-point set — but three points support only C(3,3) = 1 triple, not three. Contradiction: D(7,4,3) = 7 (the lab's exhibit). (d) v = 8: the SQS(8) exhibit covers 56/56, matching the counting bound ⌊56/4⌋ = 14. ∎ (This answer's scar history is two-deep, kept honestly: the first-draft hint claimed "a point in 3 leave-triples needs 7 points" — false, since leave triples may share pairs with each other; the session-81 repair then replaced it with an incidence analysis that silently used v = 7's residue — 15 ≡ 0 mod 3 — at v = 6, where the correct count is 10 ≡ 1 mod 3. Session 110 caught the residue slip and installed the 1-or-4 analysis above; both scars are recorded in the Verification Notes.)

**Answer 12 (symmetric differences are trades).** Let Π be a pair. Its S₁-triple T₁ and S₂-triple T₂ are unique (Steiner). If T₁ ∈ S₁ ∩ S₂ then T₂ = T₁ (uniqueness in S₂), so Π is covered by S₁ ∖ S₂ iff its S₁-triple is outside the intersection iff its S₂-triple is too — and then T₂ ≠ T₁ covers Π on the S₂ side. So S₁ ∖ S₂ and S₂ ∖ S₁ cover exactly the same pairs, with equal sizes |S₁ ∖ S₂| = |S₂ ∖ S₁| = 12 − |S₁ ∩ S₂|: a trade. The census: volumes 6 (15,120 pairs), 8 (11,340), 9 (63,840), 10 (90,720), 11 (90,720), 12 (80,640) — 4 absent (Answers 5–7), 5 classically impossible, 7 an instance-level curiosity at n = 9. ∎

**Answer ◆13 (the morality table).** Windmill: near-regularity — degrees 10, 10, then ten 1s; its codegree ratio 1.000 is a *symptom* (all triples share pair {0,1}), but even a re-weighted version fails the degree profile. 3 × K₄³: codegree 0.667 within components — but the deeper obstruction is divisibility: a 4-point component cannot be covered by disjoint triples (4 ≡ 1 mod 3), so 75% is a ceiling regardless of codegrees. Fano: codegree — ratio 1/3 fixed forever (blowing up is the cure; the blow-up row shows it). Fano blow-up: no obstruction — ratio 1/(3m) → 0, degrees uniform, and the perfect matching exists. AG(2,3): no obstruction *at its scale* (parallel classes tile), though its ratio 1/4 is not o(D) — the lemma's hypotheses are asymptotic, and this row is the census's reminder. The diagnosis pattern: P43's hypotheses (regularity, codegree) are checkable *before* running anything; divisibility (P41) is the silent third.

**Answer ◆14 (the rescue's method class).** The rescue is *template absorption*: fix a family of complete systems in advance (the 840), measure the packing's overlap with the best template, sacrifice the mismatch (≤ 2 triples), and regrow inside the template. It shares with Keevash's architecture exactly the two organs the greedy lacks: a **template** (the reservoir of systems) and an **absorption** step (the sacrifice-and-complete move) — and the receipts add the negative result that makes them non-negotiable: volume-4 trade repair (in-place fixing, P12/P14 thinking) is *provably impossible* here. When repair is impossible, pre-built flexibility is the only mathematics left.

**Answer ◆15 (where the randomness is exposed).** Alteration exposes all the randomness at once (one sample of G(n,p)), then pays for violations with deletions — and the deleted mass carries a whole logarithm: n ~ t²/log² t. The process exposes randomness *incrementally under the constraint*: each edge is chosen among still-safe pairs, so no violation is ever created, and the tracked degree profile (what the process's analysis actually reads) concentrates around its predicted trajectory. The gap — t²/log² t versus (1/4)t²/log t — is exactly the price of "repair after" versus "never damage": P14's ledger debt versus P43's clean book. That is the pattern-level statement: the later the randomness is exposed against the constraint, the less it costs.
