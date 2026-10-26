---
name: "cgt-ch19-lll"
title: "Ch. 19 — The Lovász Local Lemma: Rare, Local, Survivable (A Lecture Course in the Feynman Style)"
type: "text/markdown"
---

# Chapter 19 · The Lovász Local Lemma

*Part of the Combinatorics & Graph Theory Atlas (see the Atlas canvas for the chapter map and progress report).*

Chapter 4 taught the union bound's honest arithmetic: if the failure probabilities sum below one, something survives. This chapter is about what to do when they don't — when there are ten billion bad events, each vanishingly rare, each touching only a handful of the others. **The union bound charges every bad event against a single global budget. The Lovász Local Lemma discovers that the budget is local: an event only needs to defend against its own neighborhood, and rare events with sparse overlap cannot gang up.** The lemma was born at the Keszthely conference of 1973, in a problem list Erdős and Lovász wrote on 3-chromatic hypergraphs (published 1975): they needed to 2-color hypergraphs whose edges were far too many for the union bound, and proved, in passing, the survival principle that has carried the probabilistic method ever since. Spencer made it asymmetric and sharpenable (1977). Shearer found the exact boundary of what any such lemma can say (1985). Erdős and Spencer made it *lopsided* to handle random permutations and Latin transversals (1991). And in 2009–10, Moser and Tardos did what nobody expected: they made the lemma *run* — a trivial-sounding resampling algorithm whose termination proof is the lemma, constructive at last.

The deal with the reader is the one the Atlas has enforced since Chapter 1: every number printed below was machine-verified before printing. All randomized receipts come from documented engines — the Lehmer generator x ← 48271·x mod (2³¹−1), seed 20261083 on one continuous stream through lab Parts 1–3, and seeds 20261084–20261088 for Parts 1b, 3b, 4, 5B and 6 — with integer-exact draw rules only, so the printed Python lab reproduces the receipts bit for bit. Where a theorem is cited rather than proved, the text says so; where a certificate is vacuous or a bound non-tight at the machine's scale, the text says that too — including one honest place where the plain union bound beats the lemma's symmetric certificate, recorded rather than smoothed.

## How to read this chapter

Read with Chapters 4 and 13 within reach: the lemma is what P13 (union bound) becomes when the bad events are *rare* and *locally dependent* — and the probabilistic toolkit of Chapter 13 is what its grown-up applications lean on. Lines marked **✎ Checkpoint** are the places to stop and predict — commit to a guess, in ink, before reading on. Exercises are graded ●○○ *easy* (one idea, applied directly), ●●○ *moderate* (two ideas, or one tricky step), ●●● *tough* (several ideas combined); ◆ **pattern unknown** problems come with no hint — diagnosing the tool is part of the problem; ◐ **Explorations** are open-ended investigations that state what you should find, not a number to match. Worked answers sit at the end; hints travel with the problems.

Notation. Events A₁,…,A_n live in a probability space; **p_i = Pr[A_i]**. A **dependency graph** Γ is a graph on the events such that A_i is mutually independent of all A_j with j ∉ {i} ∪ Γ(i); **d = d(Γ)** is its maximum degree, and D in the lab means the realized maximum number of clauses/edges any one shares variables with. The **certificate variables** are x₁,…,x_n ∈ (0,1); the general certificate reads p_i ≤ x_i·∏_{j∈Γ(i)}(1−x_j). For the variable model, S_i is the variable set of A_i (i ~ j iff S_i ∩ S_j ≠ ∅). P_m is the path with m vertices; μ(G,p) is Shearer's independence polynomial Σ_k (−1)^k·I_k(G)·p^k with I_k = the number of independent k-sets. k-SAT instances have n variables and m clauses of width k, each clause violated with probability 2^{−k}. The lab engine: *nxt()* advances x ← 48271·x mod (2³¹−1); *idx(N) = nxt() mod N*; a biased bit with Pr[1] = k/m fires iff nxt()·m < k·M₃₁; partial Fisher–Yates draws one index per position. e = 2.71828…

## The pattern map for this chapter

| Pattern | Plain language | Where it fires here |
|---------|---------------|--------------------|
| **P45 Local lemma (this chapter's home)** | Bad events with local dependence can all be avoided if each is rare relative to its neighborhood's sparsity — survival is a *local* certificate, and the union bound's global ledger is only its densest special case | All six lectures — the spine of the chapter |
| **P4 Recurrence + induction** | Relate case n to smaller cases | L2 (the lemma's proof is a nested induction on conditioning sets); Ex 7 (the Shearer-boundary identity, proved by induction) |
| **P10 Averaging / expectation** | Some object beats the average | L5 (the Moser–Tardos bound on expected resamplings of A_i is an expectation statement; the lab measures it) |
| **P12 Random construction** | Prove existence by sampling | L1 (the random assignment is the experiment; the lemma certifies it succeeds with positive probability — a *conditional* P12) |
| **P13 Union bound** | If failure probabilities sum below 1, success exists | L1 (the parent, and the honest incomparability: the lab shows instances where the global certificate beats the local one); L6 (the practice menu: Σp < 1 ⇒ use P13, it is cheaper) |
| **P25 Reduction / encoding** | Translate the problem; the target structure carries the proof | L3 (choosing the dependency graph is an encoding act — fewer edges, stronger certificate); L4 (permutations: the lopsidependency graph keys on shared rows and columns, and the lab shows the graph is load-bearing) |
| **P29 Entropy counting** | Count by description cost | L5 (the witness trees are counted by description length — entropy compression, the algorithmic face's counting parent) |

---
## Lecture 1 · Ten Billion Bad Events: the Problem That Made the Lemma

**Encounter.** Color the edges of a complete graph red and blue and you are guaranteed a monochromatic triangle — that is R(3,3) = 6, Chapter 3's opening scandal. Turn the question inside out and you get the problem that created this chapter: color the *edges* of a sparse hypergraph — each edge a set of k vertices — with two colors so that **no edge is monochromatic**. Erdős had been circling such questions for a decade. The random experiment is the obvious one: flip a fair coin for every vertex. Any one edge comes out monochromatic with probability 2·2^{−k} = 2^{1−k} — hopelessly rare when k is, say, 40. And an m-edge hypergraph has m chances to go wrong.

The union bound (P13) adds the ledger: probability of *some* failure ≤ m·2^{1−k}. If that is below 1, a good coloring exists. So a hypergraph with m < 2^{k−1} edges is 2-colorable — and that is all the union bound will ever say. Read the ceiling carefully: **2^{k−1} is a cap on the total number of edges, with no regard for how many vertices the hypergraph has.** A 40-uniform hypergraph on a million vertices with a million edges sails far over the cap — even though each edge's collisions with the rest of the world might be a few dozen.

**✎ Checkpoint.** Before reading on: what *should* the right criterion care about, if not the total count of bad events? Write down a guess about the shape of the condition. (Prediction first — the formula lands in half a page.)

**Experiment.** Take the k-SAT cousin of the coloring problem, because it is the easiest to count with. Three variables per clause, m clauses on n variables, a random assignment of the n bits. Each clause is violated with probability 2^{−3} = 1/8. Two clauses are *independent* when they share no variable; they can be checked separately, and their failures have nothing to do with each other. Now watch what happens in the lab (Part 1 runs this, 100 instances per size, n = 12):

| m | mean dependency degree D | brute-force satisfiable | symmetric LLL certificate |
|---|---|---|---|
| 3 | 1.62 | 100/100 | 36/100 |
| 5 | 3.31 | 100/100 | 0/100 |
| 10 | 7.42 | 100/100 | 0/100 |

Two observations, one comfortable and one that should sting. Comfortable: every instance the certificate approves is satisfiable — 800 census instances, each brute-checked (all 4,096 assignments) and certificate-checked, zero conflicts, the certificate never lies. Stinging: at these sizes the *certificate* is far weaker than the *truth* (everything is satisfiable), and the union bound — which approves every instance with m ≤ 7 — actually out-certificates the local lemma's symmetric form. The local certificate is not a uniformly better union bound. It is a *differently shaped* one, and the shape is the whole point.

**Conjecture.** The union bound's ledger is global: every bad event, however remote from the others, charges the same single budget. But two events that share no variables are independent — the failure of one says *nothing* about the other. The global ledger overcharges hopelessly. What a rare event should actually have to defend against is only its *neighborhood*: the handful of bad events entangled with its variables. If each event is rare *relative to how sparse that entanglement is*, the whole system should survive. Erdős and Lovász, writing up the problem list of the 1973 Keszthely conference (published 1975), proved the survival principle in one paragraph and used it to 2-color hypergraphs far beyond the union bound's reach.

**Explain.** Say it as a theorem. Events A₁,…,A_n with **p_i = Pr[A_i]**, and a **dependency graph** Γ: connect i to j when the two are *not* provably independent — formally, A_i must be mutually independent of every A_j with j ∉ {i} ∪ Γ(i). Fewer edges is a stronger statement; you choose Γ, and Chapter 3's art of choosing is Exercise 11's subject. Write d for the maximum degree of Γ.

> **The Lovász Local Lemma (symmetric form; Erdős–Lovász 1975).** If each p_i ≤ p and each event depends on at most d others, and
> **e·p·(d+1) ≤ 1**,
> then Pr[no A_i occurs] > 0. In particular a point avoiding all bad events exists.

The 1/e is the price of the induction that proves it (Lecture 2) — and the +1 inside is easy to misplace; d+1, not d, because the gang of an event is its d neighbors plus itself. The lemma's shape is exactly the checkpoint guess: **rarity compared against local crowding**, with e as the exchange rate.

✎ *Micro-proof read-through, the two-clause case.* Two clauses sharing no variables: p = 1/8 each, d = 0, e·(1/8)·1 = 0.34 ≤ 1 — certified, as it must be, since the events are literally independent. Two clauses sharing a variable: d = 1, e·(1/8)·2 = 0.68 ≤ 1 — still certified, though the union bound would have been just as happy. Three clauses all mutually entangled: d = 2, e·(1/8)·3 = 1.02 > 1 — the certificate shuts off. The lab's Part 1 measures exactly this collapse: mean D 1.62 at m = 3 (36% certified), 3.31 at m = 5 (none).

**Generalize.** The dice circle. Stand 100 fair dice in a circle and call A_i the event *die i and die i+1 both show six* — p = 1/36 each, and A_i shares outcomes only with A_{i−1} and A_{i+1}: a dependency *cycle*, d = 2. The certificate: e·(1/36)·3 = 0.226 ≤ 1 — **survival certified**. The union bound: Σp_i = 100/36 ≈ 2.8 — dead. Here is the lemma's signature move in one line: a hundred events whose *total* failure mass is nearly three full probability budgets, surviving because no local gang can form. (Of course, for dice you could shortcut — the all-ones... the no-six assignment avoids everything, and it is a product event. The shortcut is exactly what k-SAT and hypergraph coloring do not offer: there, "avoid all bad events" is not the complement of a product event, and no shortcut is known. The lemma is the uniform argument that works when shortcuts die — that is its job description.)

And now the honest generalization, the one the receipts force: certificates are incomparable, not ranked. The lab's Part 1 table records instances (m ≤ 7, small n) where the union bound certifies and the symmetric lemma cannot — the global ledger wins whenever events are few and probabilities tiny, because the e·p·(d+1) shape is tuned for *many* events with *sparse* overlap. Part 1's second panel (n = 48, m ≥ 8: total failure mass ≥ 1, union dead) is where the local certificate earns its keep: 13% and 2% of instances certified at m = 8 and 10, against union's flat zero. **What to learn:** when failure probabilities sum below one, take the union bound and go home (P13, cheaper). When they don't, count the *degree of entanglement* — if each event's gang is small next to 1/(e·p), survival is still provable (P45). Diagnosing which regime you are in is the chapter's first skill.

---

## Lecture 2 · The General Form, and the Induction That Proves It

The symmetric form hides the lemma's real engine. The sharpened statement — due in this shape to Spencer (1977), the paper whose Ramsey applications we meet in Lecture 6 — gives every event its own exchange rate:

> **The Local Lemma (general asymmetric form).** Suppose there exist numbers x₁,…,x_n ∈ (0,1) with
> **p_i ≤ x_i · ∏_{j ∈ Γ(i)} (1 − x_j)** for every i.
> Then Pr[no A_i occurs] ≥ ∏_i (1 − x_i) > 0.

Read the certificate as a bargaining table: event i may claim budget x_i, but every neighbor j must *simultaneously* survive with probability 1−x_j, and the neighbors' survival discounts i's allowance. The symmetric form is the special case where every seat bargains identically.

**✎ Checkpoint.** Derive the symmetric constant yourself before looking: set every x_i = x and every degree = d. For which x is x(1−x)^d largest, and how does e·p·(d+1) ≤ 1 fall out? (This derivation is complete in the text below and again as Exercise 3 — it is the chapter's most reused computation.)

**From general to symmetric, completely.** Maximize f(x) = x(1−x)^d over x ∈ (0,1). Differentiate: f′(x) = (1−x)^d − dx(1−x)^{d−1} = (1−x)^{d−1}·(1 − x − dx) = (1−x)^{d−1}·(1 − (d+1)x). Zero at x = 1/(d+1); f there is (1/(d+1))·(d/(d+1))^d = d^d/(d+1)^{d+1}. So the uniform certificate exists exactly when **p ≤ d^d/(d+1)^{d+1}**, and the classical loose form e·p·(d+1) ≤ 1 follows because (1+1/d)^d < e: d^d/(d+1)^{d+1} = 1/((d+1)·(1+1/d)^d) > 1/(e(d+1)). The 1/e lost in the last step is pure slack — real proofs keep d^d/(d+1)^{d+1}. (d = 2: the exact uniform ceiling is 4/27 ≈ 0.1481 against the loose 1/(3e) ≈ 0.1226 — Lecture 5's lab measures this gap from the inside.)

**The floor.** The general form pays a bonus the symmetric statement doesn't mention: the theorem's conclusion is not merely *positive* probability but the explicit floor **Pr[all survive] ≥ ∏(1−x_i)**. A survival probability you can compute, print, and compare — the lab's Part 5 ranks three such floors against the exact truth on a line of events, and the floors' ordering is the chapter's sharpest practical lesson: a certificate is also a *quantitative guarantee*, and different certificates give wildly different floors to the same process.

**The proof, complete by nested induction.** The theorem is proved by strong induction on the size |S| of a conditioning set S ⊆ {1,…,n} ∖ {i}, establishing both that Pr[⋀_{j∈S} Ā_j] > 0 and the conditional bound:

> **Claim (Spencer 1977).** For every subset S ⊆ {1,…,n} and every i ∉ S, if Pr[⋀_{j∈S} Ā_j] > 0 then Pr[A_i | ⋀_{j∈S} Ā_j] ≤ x_i.

*Base case and Case A (S contains no neighbor of i).* When S ∩ Γ(i) = ∅ (which includes |S| = 0), A_i is mutually independent of {A_j : j ∈ S} by the definition of the dependency graph Γ. Hence conditioning on ⋀_{j∈S} Ā_j leaves the probability of A_i unchanged: Pr[A_i | ⋀_{j∈S} Ā_j] = Pr[A_i] = p_i ≤ x_i·∏_{j∈Γ(i)}(1−x_j) ≤ x_i, since each factor (1−x_j) lies in (0,1).

*Inductive step, Case B (S contains neighbors of i).* Fix |S| ≥ 1 and assume the Claim holds for all conditioning sets of size strictly smaller than |S|. Note first that by the induction hypothesis applied sequentially to the elements of S = {s₁,…,s_r}, we have Pr[⋀_{j∈S} Ā_j] = ∏_{t=1}^{r}(1 − Pr[A_{s_t} | ⋀_{u<t} Ā_{s_u}]) ≥ ∏_{j∈S}(1−x_j) > 0, so the conditioning event has strictly positive probability. Now partition S into neighbors S₁ = S ∩ Γ(i) = {j₁, j₂, …, j_k} (with k ≥ 1) and non-neighbors S₂ = S ∖ Γ(i). By the definition of conditional probability, keeping S₂ in the background conditioning throughout,

Pr[A_i | ⋀_{j∈S} Ā_j] = Pr[A_i ∧ ⋀_{j∈S₁} Ā_j | ⋀_{ℓ∈S₂} Ā_ℓ] / Pr[⋀_{j∈S₁} Ā_j | ⋀_{ℓ∈S₂} Ā_ℓ].

We bound the numerator from above and the denominator from below. For the **numerator**, dropping the events ⋀_{j∈S₁} Ā_j can only increase the probability, and since S₂ contains no neighbors of i, Case A applies directly to give

Pr[A_i ∧ ⋀_{j∈S₁} Ā_j | ⋀_{ℓ∈S₂} Ā_ℓ] ≤ Pr[A_i | ⋀_{ℓ∈S₂} Ā_ℓ] = Pr[A_i] = p_i ≤ x_i·∏_{j∈Γ(i)}(1−x_j).

For the **denominator**, telescope the conjunction over S₁ = {j₁,…,j_k} via the chain rule:

Pr[⋀_{j∈S₁} Ā_j | ⋀_{ℓ∈S₂} Ā_ℓ] = ∏_{r=1}^{k}(1 − Pr[A_{j_r} | ⋀_{t=1}^{r−1} Ā_{j_t} ∧ ⋀_{ℓ∈S₂} Ā_ℓ]).

Each conditioning set S^{(r)} = {j₁,…,j_{r−1}} ∪ S₂ avoids j_r and has cardinality |S^{(r)}| = r−1+|S₂| ≤ (k−1)+(|S|−k) = |S|−1 < |S|. By the strong induction hypothesis applied to event j_r and conditioning set S^{(r)}, we have Pr[A_{j_r} | ⋀_{m∈S^{(r)}} Ā_m] ≤ x_{j_r}. Therefore the denominator is at least ∏_{r=1}^{k}(1−x_{j_r}) = ∏_{j∈S₁}(1−x_j). Dividing the numerator bound by the denominator bound and canceling ∏_{j∈S₁}(1−x_j) > 0 yields

Pr[A_i | ⋀_{j∈S} Ā_j] ≤ x_i·∏_{j∈Γ(i)}(1−x_j) / ∏_{j∈S₁}(1−x_j) = x_i·∏_{j∈Γ(i)∖S₁}(1−x_j) ≤ x_i.

This completes the induction. Finally, chaining the Claim across T = {1,…,n} one event at a time gives the explicit survival floor: Pr[⋀_{i=1}^{n} Ā_i] = ∏_{i=1}^{n}(1 − Pr[A_i | ⋀_{j=1}^{i−1} Ā_j]) ≥ ∏_{i=1}^{n}(1−x_i) > 0. Every step of the bargaining table is accounted for: each neighbor j ∈ Γ(i) charges its survival factor (1−x_j) against i's allowance x_i so that when the denominator telescopes over any subset of neighbors S₁ ⊆ Γ(i), the exact factors needed to cancel the denominator are waiting in the numerator.

**Why asymmetric earns its keep — the star, previewed.** The general certificate's strength is that *rare events may sit in crowded neighborhoods, and crowded common events may lean on rare ones*. Build the lab's Part 6 instance: one hub clause of width 4 (p_h = 1/16) and eight satellite clauses of width 3 (p_s = 1/8), each satellite sharing exactly one variable with the hub and none with each other. Three certificates, three verdicts:

- **Union bound:** Σp = 1/16 + 8·(1/8) = 1.0625 > 1 — fails.
- **Symmetric lemma:** the hub has d = 8, so e·(1/8)·9 = 3.06 > 1 — fails.
- **General form:** solve the two-variable bargaining system x_h = (1/16)/(1−x_s)^8, x_s = (1/8)/(1−x_h). The iteration from zero converges (monotone increasing, the map is increasing in each coordinate): **x_h = 0.3064, x_s = 0.1802** — both below 1, the certificate holds, a satisfying assignment exists. The brute-force census agrees: 373,729 of 1,048,576 assignments satisfy all nine clauses.

The star and its three-verdict ledger, drawn as **Figure 1** — the hub in blue, its eight satellites in amber, and every certificate's arithmetic at the right:

```svg
<svg viewBox="0 0 640 290" width="640" height="290" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="The nine-clause star dependency graph K_{1,8} from Lecture 2 and Lab Part 6">
  <style>
    .st-edge { stroke: #64748b; stroke-width: 1.8; }
    .st-hub { fill: #dbeafe; stroke: #1d4ed8; stroke-width: 2.2; }
    .st-sat { fill: #fef3c7; stroke: #b45309; stroke-width: 1.8; }
    .st-txt { font-family: Georgia, serif; font-size: 12px; fill: #1a1a1a; text-anchor: middle; dominant-baseline: middle; }
    .st-sub { font-family: Georgia, serif; font-size: 11px; fill: #334155; text-anchor: start; }
    .st-cap { font-family: Georgia, serif; font-size: 12.5px; font-weight: bold; fill: #0f172a; }
  </style>
  <line class="st-edge" x1="175" y1="145" x2="175" y2="43"/>
  <line class="st-edge" x1="175" y1="145" x2="247" y2="73"/>
  <line class="st-edge" x1="175" y1="145" x2="277" y2="145"/>
  <line class="st-edge" x1="175" y1="145" x2="247" y2="217"/>
  <line class="st-edge" x1="175" y1="145" x2="175" y2="247"/>
  <line class="st-edge" x1="175" y1="145" x2="103" y2="217"/>
  <line class="st-edge" x1="175" y1="145" x2="73"  y2="145"/>
  <line class="st-edge" x1="175" y1="145" x2="103" y2="73"/>
  <circle class="st-sat" cx="175" cy="43"  r="20"/><text class="st-txt" x="175" y="43">S₀</text>
  <circle class="st-sat" cx="247" cy="73"  r="20"/><text class="st-txt" x="247" y="73">S₁</text>
  <circle class="st-sat" cx="277" cy="145" r="20"/><text class="st-txt" x="277" y="145">S₂</text>
  <circle class="st-sat" cx="247" cy="217" r="20"/><text class="st-txt" x="247" y="217">S₃</text>
  <circle class="st-sat" cx="175" cy="247" r="20"/><text class="st-txt" x="175" y="247">S₄</text>
  <circle class="st-sat" cx="103" cy="217" r="20"/><text class="st-txt" x="103" y="217">S₅</text>
  <circle class="st-sat" cx="73"  cy="145" r="20"/><text class="st-txt" x="73"  y="145">S₆</text>
  <circle class="st-sat" cx="103" cy="73"  r="20"/><text class="st-txt" x="103" y="73">S₇</text>
  <circle class="st-hub" cx="175" cy="145" r="30"/>
  <text class="st-txt" x="175" y="138" font-weight="bold">Hub H</text>
  <text class="st-txt" x="175" y="154" font-size="10.5">p = 1/16</text>
  <rect x="335" y="32" width="288" height="226" rx="6" fill="#f8fafc" stroke="#cbd5e1" stroke-width="1.4"/>
  <text class="st-cap" x="350" y="56">Part 6 Star Certificate Ledger (K₁,₈)</text>
  <text class="st-sub" x="350" y="82">• Hub H (width 4): p_h = 1/16, degree d_h = 8</text>
  <text class="st-sub" x="350" y="104">• 8 Satellites S_i (width 3): p_s = 1/8, degree d_s = 1</text>
  <text class="st-sub" x="350" y="132" fill="#991b1b">✗ Union bound: Σ p_i = 1/16 + 8(1/8) = 1.0625 > 1</text>
  <text class="st-sub" x="350" y="154" fill="#991b1b">✗ Symmetric LLL: e·(1/8)·(8+1) = 3.0581 > 1</text>
  <text class="st-sub" x="350" y="182" fill="#166534" font-weight="bold">✓ Asymmetric LLL (Jacobi fixed point):</text>
  <text class="st-sub" x="362" y="204" fill="#166534">x_h = (1/16)/(1 − x_s)⁸ = 0.3064 < 1</text>
  <text class="st-sub" x="362" y="224" fill="#166534">x_s = (1/8)/(1 − x_h)   = 0.1802 < 1</text>
  <text class="st-sub" x="350" y="246">• Exact truth: 373,729 / 2²⁰ = 35.64% satisfying</text>
</svg>
```

The satellite crowd is *individually cheap to forgive* (each rare-ish, each only leaning on the hub), and the hub is *rare enough to absorb eight leanings*. No uniform exchange rate can say that; the bargaining table can. **What to learn:** the general form is not a technicality — it is the lemma learning to price heterogeneous neighborhoods. When a symmetric check fails, do not abandon the Lemma: retune the x's (Exercise 5 hands you a second star to price). When the general form fails too, the crowd is genuinely dangerous — Lecture 4's lopsidedness or Lecture 5's algorithm may still save you.

---
## Lecture 3 · Two Ceilings: Hypergraph Coloring, k-SAT, and the Shape That Separates Them

**Encounter.** Return to the problem that created the lemma. A k-uniform hypergraph — every edge a set of k vertices — should have its vertices colored red and blue so that **no edge is monochromatic**. The random experiment: fair coin per vertex. One edge goes wrong with probability 2·(1/2)^k = **2^{1−k}**. The lemma wants a dependency graph: A_e and A_f are entangled exactly when the edges share a vertex (given all other vertices' colors, the two events still interact through the shared ones); disjoint edges are independent. So the degree d of the dependency graph is bounded by the number of edges that *collide* with a given edge — call the realized maximum D.

**Explain, completely.** The symmetric certificate for the coloring experiment reads

> **e · 2^{1−k} · (D+1) ≤ 1.**

For k = 4 that is p = 1/8 and **D ≤ 1**: each edge may collide with at most one other edge of the whole hypergraph. The general form sharpens it, and for once the sharpening can be finished by hand: with uniform exchange rate x, an edge with D neighbors is certifiable exactly when x(1−x)^D ≥ 1/8. For D = 2, x = 1/3 gives (1/3)(2/3)² = 4/27 = 0.1481 ≥ 0.125 — **certified**. For D = 3, the best uniform x is 1/4, giving (1/4)(3/4)³ = 27/256 = 0.1055 < 0.125 — and on any 3-regular (or minimum-degree ≥ 3) dependency graph, no asymmetric assignment can rescue p = 1/8 either: at whichever event i* attains the minimum seat value x_{i*} = min_i x_i, every neighbor j ∈ Γ(i*) has 1 − x_j ≤ 1 − x_{i*}, so the seat condition forces 1/8 ≤ x_{i*}·∏_{j∈Γ(i*)}(1−x_j) ≤ x_{i*}(1−x_{i*})^{d(i*)} ≤ x_{i*}(1−x_{i*})³ ≤ 27/256 < 1/8, a contradiction. (If a degree-3 edge instead sits only on degree-1 leaf neighbors, as on K_{1,3}, an asymmetric assignment *can* certify it — e.g. x_hub = 0.34, x_leaf = 0.19, machine-checked — so the uniform-seat ceiling D ≤ 2 is the exact threshold for regular graphs and for any degree-only test.) The lab's Part 3 runs the census on exactly these three verdicts: symmetric (D ≤ 1), general (D ≤ 2), and the union bound (m·2^{1−k} < 1, i.e. m ≤ 7).

**Experiment.** v = 14 vertices, k = 4, m edges, 100 instances per size, every instance brute-checked over all 2^{14} colorings:

| m | mean D | cert sym (D≤1) | cert gen (D≤2) | union (m≤7) | brute colorable |
|---|---|---|---|---|---|
| 4 | 2.83 | 1 | 16 | 100 | 100 |
| 6 | 4.84 | 0 | 0 | 100 | 100 |
| 8 | 6.62 | 0 | 0 | 0 | 100 |
| 10 | 8.63 | 0 | 0 | 0 | 100 |
| 12 | 10.55 | 0 | 0 | 0 | 100 |
| 14 | 12.31 | 0 | 0 | 0 | 100 |
| 16 | 14.17 | 0 | 0 | 0 | 100 |

Read it in three layers. *Soundness:* 700 instances, 700 colorable, and the one instance any certificate approved was colorable — the certificate never lies (cert∧¬col = 0, exactly as in Part 1's k-SAT census). *The bargaining table earns its keep:* at m = 4, the general form certifies 16 of 100 instances against the symmetric form's 1 — heterogeneous exchange rates are not decoration. *The honest gap:* from m = 6 on, both local certificates fall silent, the union bound dies at m = 8, and yet every instance remains colorable. The certificates are keyed to local crowding, and on 14 vertices everything is crowded: two random 4-edges intersect with probability 1 − C(10,4)/C(14,4) = 0.790, so by m = 16 each edge collides with all but two of the others. The v = 70 panel (Part 3b: m = 16, 18; mean D 5.82, 6.73) pushes the same honest negative further — there the collision probability is still 0.214, every certificate stays silent, and the union bound is nowhere.

**✎ Checkpoint.** The census says the certificates die of crowding while the truth stays easy. Before reading on: what does the union bound cap, what does the lemma cap, and which one can grow with the number of *vertices*?

**Generalize — the two ceilings, the chapter's centerpiece.** The union bound's ceiling: m·2^{1−k} < 1, so a k-uniform hypergraph with fewer than **2^{k−1} edges** is 2-colorable — a cap on the *total*, with no regard for v. The lemma's ceiling: e·2^{1−k}·(D+1) ≤ 1, so each edge may collide with up to **2^{k−1}/e − 1 others** — a cap on local *crowding*. Now translate: if each vertex sits in at most Δ edges, an edge's k vertices drag in at most k(Δ−1) colliding edges, and counting vertex-edge incidences gives m ≤ vΔ/k. Run k = 20: the union bound certifies up to 524,288 edges, ever, on any number of vertices. The lemma certifies when each edge collides with at most 192,873 others — which a hypergraph of max vertex degree Δ = 9,643 amply satisfies — and on v = 10^{9} vertices that allows up to 482,150,000,000 edges. **Nine hundred twenty thousand times the union bound's ceiling** — and the ratio doubles with every increment of k, because the lemma's ceiling is a degree and the union's is a count. This is the shape lesson of Lecture 1 made quantitative: *rarity priced against local crowding* lets a system of many events survive when a global ledger would call it hopeless. The lab cannot print a 2^{19}-edge example; the census instead shows the mechanism honestly at the scale it can verify — the certificates sit silent exactly where crowding is high, which is the same sensitivity, read from the other side.

The k-SAT cousin works identically (it is the lab Part 1 experiment): a clause of width k is violated with probability exactly **2^{−k}**, two clauses are entangled iff they share a variable, and if each variable appears in at most L clauses then any clause collides with at most k(L−1) others. The certificate e·2^{−k}(k(L−1)+1) ≤ 1 holds with L roughly 2^{k}/(ek) — so an instance on n variables may carry up to ~n·2^{k}/(ek²) clauses and still be certified satisfiable, against the union bound's fixed cap of 2^{k} − 1 total clauses. Part 1's n = 48 panel is this story at reachable scale: at m = 8 and 10 the union bound is dead (total failure mass ≥ 1) while the local certificate approves 13 and 2 instances per hundred — the slice where the lemma earns its keep, honestly recorded as *rare*, because at n = 48 even sparse overlap is hard to come by.

**What to learn:** for coloring and satisfiability, the union bound caps the *number* of bad events and the local lemma caps their *entanglement*. At small scale both certificates are conservative and the gap between certificate and truth is wide; the lemma's wins are asymptotic, where sparse events can number far beyond any global budget.

---

## Lecture 4 · The Lopsided Lemma: Permutations, and a Graph You Must Earn

**Encounter.** Random permutations break the beautiful variable model of Lecture 2. Take an n×n array and ask for a **Latin transversal**: a choice of one cell in each row and each column holding all n symbols distinct — the permutation σ (row i picks column σ(i)) must avoid every "two chosen cells share a symbol" accident. The natural experiment — a uniformly random permutation — has no independent coordinates to resample: forbid column 3 for row 1 and every other row's options shift. The dependency-graph calculus of the variable model is gone; worse, the *obvious* graph is far too crowded: two accident-events that name a common row or column can interact — but interact *how*? The discovery of Erdős and Spencer (1991) is that for permutations, conditioning on other events being *avoided* tends to help you, not hurt you — and a lemma that only charges you for what can genuinely hurt is strictly stronger.

**Explain.** The lopsided local lemma replaces the mutual-independence hypothesis by a one-sided one. Call Γ a **lopsidependency graph** for events A₁,…,A_n if for every i and every set S of *non-neighbors* of i:

> **Pr[A_i | all events of S are avoided] ≤ p_i.**

Then the same x-certificate p_i ≤ x_i·∏_{j∈Γ(i)}(1−x_j) implies Pr[no A_i] ≥ ∏_i(1−x_i) > 0. The proof is identical to Lecture 2's nested induction on |S|, with one surgical substitution in the numerator of Case B: when S is partitioned into neighbors S₁ = S ∩ Γ(i) and non-neighbors S₂ = S ∖ Γ(i), we no longer need A_i to be mutually independent of S₂; instead, the lopsided hypothesis directly bounds the numerator via Pr[A_i ∧ ⋀_{j∈S₁} Ā_j | ⋀_{ℓ∈S₂} Ā_ℓ] ≤ Pr[A_i | ⋀_{ℓ∈S₂} Ā_ℓ] ≤ p_i ≤ x_i·∏_{j∈Γ(i)}(1−x_j). The denominator still telescopes over S₁ using the induction hypothesis to give at least ∏_{j∈S₁}(1−x_j), and the ratio still cancels to at most x_i. Nothing else in the proof touches independence — which is why a one-sided inequality on non-neighbors does the entire job of mutual independence.

Why "one-sided" is the right idea — the two-event case, completely. Conditioning on Ā₂ not hurting is a correlation statement:

Pr[A₁ | Ā₂] ≤ Pr[A₁] ⟺ Pr[A₁]−Pr[A₁∧A₂] ≤ Pr[A₁]−Pr[A₁]Pr[A₂] ⟺ **Pr[A₁∧A₂] ≥ Pr[A₁]·Pr[A₂]**.

The lopsided hypothesis asks exactly that avoiding a non-neighbor makes your failure no *likelier* — i.e. that bad events are **positively correlated** across non-edges of the graph. Positive correlation is the friend; the enemy is negative correlation, where someone else's survival taxes you. (For independent coordinates, both correlations vanish and lopsided degenerates to the ordinary lemma — the variable model is the special case where all the hard work is free.)

**Experiment.** So measure the correlation. The lab's Part 4 puts two 3-cell forbidden boards in a 6×6 array — board 1 on rows {0,1,2}, board 2 on rows {3,4,5} — and asks the exact question over all T = 720 permutations: a₁ = 426 permutations miss every cell of board 1 (so the *hit* event has probability 294/720 = 0.4083), a₂ likewise 426, and ab permutations miss both. Two panels:

- **Panel a — disjoint columns** (lopsidependency non-neighbors): ab = 265, and the hit events' correlation is 265/720 − (426/720)² = **+0.01799 ≥ 0**. Six random boards, six identical verdicts (boards differ only by relabeling) — avoiding one board genuinely *helps* avoid the other: the conditioning discount is sound, and the lopsided graph need not draw this edge.
- **Panel b — shared column set** (neighbors): ab = 240, correlation **−0.01674 < 0** — negative, six for six. Here conditioning on the other board's survival makes yours *harder*, exactly the taxing that the lopsided hypothesis forbids — so the graph *must* draw the edge, and the certificate must pay for it.

(A quiet exactness note the receipts force on us: 265 is the derangement number D₆ — when both boards forbid a full set of columns the joint count is literally the derangement count, and panel c's 14833 is D₈. The enumeration is exact, not sampled.)

**Generalize.** With the lopsided graph keyed on shared rows and columns, the Latin transversal theorem lands: if no symbol appears in more than ~n/(4e) cells of the array, a transversal exists (Erdős–Spencer 1991; we state the theorem at flag level and do not reproduce the proof — the constant is quoted as in the standard exposition). Lu and Székely generalized the machinery from permutations to random injections (cited at flag level, venue not web-verified this session — the appendix records the pin level honestly). The reusable lesson is not the transversal: it is that **the graph is a claim, not a given**. Every edge you decline to draw is a promise that conditioning across that gap cannot hurt you — a promise the variable model underwrites for free and that permutation models make you measure. Exercise 10 sends you back to the lab numbers to check the bookkeeping yourself.

**What to learn:** when the underlying experiment is not a product of independent coordinates, ask which pairs of bad events are *negatively* entangled — those, and only those, belong in the graph. Lopsidedness is the local lemma's way of paying only for genuine danger.

---

## Lecture 5 · The Lemma Learns to Run: Moser–Tardos

**Encounter.** For thirty-five years the lemma was a pure existence statement — it promised that a good assignment existed with positive probability, but a lottery with a 10^{−100} win rate is a strange kind of algorithm. Then Moser and Tardos (2010) found the resampling algorithm hiding inside the proof, and it is almost embarrassingly simple:

> **While some bad event A_i holds: pick one (the lab picks the lowest index), and resample its variables fresh, independently.**

That is the whole algorithm. No restarts, no priority scheme, no memory. If the x-certificate of Lecture 2 holds, this loop terminates with probability 1 and its final assignment avoids every bad event — the lemma, made constructive, with the *same* hypotheses. And it comes with a quantitative runtime guarantee: Moser and Tardos (2010, Theorem 1.2) prove that **E[number of resamplings of A_i] ≤ x_i/(1−x_i)**. Whenever x_i ≤ 1−p_i (so 1−x_i ≥ p_i), this is further bounded above by the probability-ratio meter **x_i/p_i** tracked in the lab's Part 2 code (indeed, at a degree-1 seat where x₁(1−x₁) = p, we have x₁/p = 1/(1−x₁) = 1 + x₁/(1−x₁), i.e. the expected total number of *evaluations* including the initial draw; note that neither bound is simply x_i itself).

**Explain — the witness-tree proof, complete.** Why can the loop not run forever? Let the execution log be C₁, C₂, …, C_t, … where C_t ∈ {1,…,n} is the index of the bad event resampled at step t. For the t-th step (which resamples A_{C_t}), we build a rooted, vertex-labeled **witness tree** τ_t as follows: start with a single root vertex labeled C_t at depth 0; working backwards for s = t−1, t−2, …, 1, if C_s shares variables with the label of at least one vertex already in τ_t (so C_s ∈ {label(v)} ∪ Γ(label(v)) for some vertex v ∈ τ_t), attach a new vertex labeled C_s as a child of the *deepest* such vertex v in τ_t (breaking ties among deepest vertices by choosing the one with the largest label); if C_s shares no variables with any vertex currently in τ_t, discard s and continue.

> **Lemma 1 (distinct steps produce distinct witness trees).** In any execution log, the witness trees τ₁, τ₂, … are pairwise non-isomorphic as rooted labeled trees: specifically, if a given proper witness tree T (where sibling vertices always have distinct labels) appears in the log at step t, the total number of vertices of T labeled j equals the exact number of times A_j was resampled up to step t along the causal chain, so T can occur at most once in the entire run.
> *Proof.* Suppose τ_t = τ_{t'} = T with t < t'. Both trees have the same root label C_t = C_{t'}, so step t itself would have been encountered when scanning backwards from t' and attached as a child of the root or a deeper compatible descendant (since C_t shares variables with C_{t'} = C_t), giving τ_{t'} strictly more vertices labeled C_t than τ_t — a contradiction. Thus each tree shape T occurs in the log at most once.
>
> **Lemma 2 (coupling a witness tree to fresh independent samples).** For any fixed proper witness tree T, the probability that T appears as τ_t for some step t in the Moser–Tardos execution log is at most w(T) = ∏_{v∈V(T)} p_{label(v)}.
> *Proof.* Order the vertices of T in reverse breadth-first order (deepest vertices first). When the algorithm runs, each vertex v ∈ V(T) corresponds to an event A_{label(v)} that held at its resampling step. Because children in τ_t were chosen at the deepest possible level during the backward scan, before the event at v is checked at its step in the log, every variable in S_{label(v)} is either in its initial random state or was most recently resampled by a child of v in T. Consequently, traversing T from deepest level to the root presents each vertex v with a completely fresh, independent sample of the underlying variables in S_{label(v)}. The probability that A_{label(v)} holds on its fresh sample is exactly p_{label(v)}, and independence across the |V(T)| fresh evaluations gives Pr[T appears in the log] ≤ ∏_{v∈V(T)} p_{label(v)}.
>
> **Lemma 3 (the Galton–Watson branching bound).** Define a multi-type Galton–Watson branching process that builds a random tree rooted at i: a vertex with label u independently spawns a child with label w for each w ∈ {u} ∪ Γ(u) with probability x_w (and no child with probability 1−x_w). Then summing w(T) over all proper witness trees T_i rooted at i satisfies **E[resamplings of A_i] ≤ Σ_{T_i} w(T_i) ≤ x_i/(1−x_i)**.
> *Proof.* In the branching process, the probability of generating a specific proper tree T_i rooted at i is the parent-charged slot accounting — every vertex v spawns each actual child u ∈ Children(v) with probability x_u and fails to spawn each non-occurring label u ∈ ({ℓ_v} ∪ Γ(ℓ_v)) ∖ Children(v) with probability 1−x_u:
>
> P(T_i) = ∏_{v∈V(T_i)} [ ∏_{u∈Children(v)} x_u · ∏_{u∈({ℓ_v}∪Γ(ℓ_v))∖Children(v)} (1−x_u) ] = ((1−x_i)/x_i) · ∏_{v∈V(T_i)} [ x_{ℓ_v} · ∏_{u∈Γ(ℓ_v)} (1−x_u) ].
>
> (The regrouping: every non-root vertex is spawned exactly once, so the x-factors telescope to (∏_v x_{ℓ_v})/x_i, and the non-spawn slots restore, at every vertex v, the full neighborhood product ∏_{u∈Γ(ℓ_v)}(1−x_u) with exactly one global factor (1−x_i) left over — this slot accounting is what prices a same-label parent–child edge correctly, shifting the (1−x) charge by one seat instead of paying it twice; the naive unconditional per-vertex form x_ℓ(1−x_ℓ)·∏_{u∈Γ(ℓ)∖Children}(1−x_u) double-charges exactly there.) By the Local Lemma certificate, p_ℓ ≤ x_ℓ·∏_{u∈Γ(ℓ)}(1−x_u) for every label ℓ. Substituting this inequality at every vertex v ∈ V(T_i) gives w(T_i) = ∏_{v∈V(T_i)} p_{ℓ_v} ≤ (x_i/(1−x_i))·P(T_i). Summing over all proper trees T_i rooted at i, since the events {the branching process produces T_i} are mutually exclusive across distinct trees, we have Σ_{T_i} P(T_i) ≤ 1. Therefore E[resamplings of A_i] = Σ_{T_i} Pr[T_i appears in log] ≤ Σ_{T_i} w(T_i) ≤ x_i/(1−x_i) — the equality holds because Lemma 1's injectivity makes the appearance-events disjoint across trees, one per resampling of A_i.

**Experiment.** Four receipts panels, four honest readings.

*Certified vs uncertified (Part 2).* On 40 certified instances (n = 20, m = 5, rejection until D ≤ 1; 554 tries for 40 instances), MT terminated on 40 of 40 with **mean 0.65 resampling events, max 4**. The theory meters: with x₁ = (1−√(1/2))/2 ≈ 0.146447 for a degree-1 clause and x₀ = 1/8 for an isolated one, the exact Moser–Tardos Theorem 1.2 bound Σ x_i/(1−x_i) uses x₁/(1−x₁) = 3−2√2 ≈ 0.17157 and x₀/(1−x₀) = 1/7 ≈ 0.14286 (averaging **0.8134** across the 40 instances), while the lab code's coarser probability-ratio meter Σ x_i/p_i uses x₁/p = 1/(1−x₁) = 1.17157 and x₀/p = 1 and averages **5.592** — the sample mean 0.65 sits below both, and the reason is the meter's fine print: the bound is worst-case over *all* distributions sharing the dependency graph, while the lab samples the easiest one, the honest product measure. (The certificate's other output, the survival floor ∏(1−x_i), averaged 0.4709.) The control panel ran 30 brute-verified satisfiable instances with entanglement degree ≥ 5 — *uncertifiable* by any form of the lemma — and MT still terminated on 30 of 30, at **mean 2.23, max 10**: about 3.4× the resamplings of the certified set. **Sufficient, not necessary** — the algorithm patrols well beyond the certificate's fence, exactly as Part 1's census hinted it might.

*Beyond Shearer's wall (Part 5B).* On the line process (events A_i = "b_i and b_{i+1} both fire", q = Pr[b = 1] ranging 2/5 to 3/5, well past Shearer's exact boundary q = 1/2), MT ran with a 50,000-round cap and **never touched it**: medians 2–6 at m = 16, 5–14 at m = 32, roughly doubling with m, no caps in 700 trials. Kolipaka and Szegedy's efficiency theorem (cited at flag level) says MT can be *forced* to be slow right up to Shearer's boundary — worst-case over configurations sharing the dependency graph. This process is not that configuration; the receipts say so, and the chapter says so with them.

*The star (Part 6).* The nine-clause star that only the asymmetric form could certify: 20 trials, 20 terminations, **mean 1.10, max 4**. Recall 35.64% of all assignments already satisfy the instance — MT's first round is free more often than not, and its expected total effort is barely above one resampling. The certificate's promise and the algorithm's reality agree comfortably.

**Generalize — the counting parent.** Moser's original termination argument (with Tardos's simplification) is known as **entropy compression**: if the loop ran too long, its resampling log would be an incompressible string of too much description cost — counting by description length, P29's counting idea, turned into an algorithmic stop sign. The Atlas's pattern survey recorded honestly that entropy compression never fires *standalone* in the survey corpus — it lives here, as the engine inside P45's constructive face, with P29 as its counting parent. Its grown-up descendant is field practice: the same description-length discipline underlies the modern sharpenings of Johansson's coloring bound (Lecture 6).

**What to learn:** the lemma and the algorithm are one object — the x-certificate is simultaneously an existence proof, a termination proof, and a runtime meter. Trust the meter as a worst-case ceiling, not an estimate; and remember the algorithm is more generous than the theorem that licenses it.

---

## Lecture 6 · The Field, the Boundary, and the Practice Menu

**Encounter.** Where does the lemma carry real weight — not as a textbook cameo but as the spine of a theorem people use? The emblem is a coloring question of a different flavor: the **list chromatic number**. Give every vertex of a graph its own list of available colors and ask for a proper coloring from lists. For triangle-free graphs of maximum degree Δ, the answer is about Δ/ln Δ — dramatically better than the Δ+1 a greedy argument needs — because triangle-freeness makes each vertex's neighborhood locally sparse, and *locally sparse + globally many* is precisely the local lemma's regime. Johansson proved the bound around 1996; the honest publishing story is an odd one the Atlas records as it stands: the proof lives in a DIMACS technical report (91-5) that was never journal-published, and the LLL step it is famous for survives through the Molloy–Reed book's exposition. The result was sharpened to the exact leading constant by Molloy (2019, J. Combin. Theory Ser. B 134:264–284, arXiv:1701.09133): every triangle-free graph of maximum degree Δ has list chromatic number at most (1+o(1))Δ/ln Δ — a modern landmark whose load-bearing beam is a carefully tuned asymmetric application of the lemma (the general form, pricing heterogeneous neighborhoods — Lecture 2's bargaining table doing real work, not decoration). We cite the applications at flag level; the chapter has proven and verified what sits below them.

**The boundary.** How far can any such lemma go? Shearer (1985) found the exact frontier: for uniform p on a dependency graph G, the best possible certificate criterion is the positivity of the **independence polynomial** μ(G, p) = Σ_k (−1)^k·I_k(G)·p^k (I_k = number of independent k-sets) on G and every induced subgraph. Neither the symmetric nor the general form reaches it — on the path P_m the three ceilings stack like a ladder, and the lab's Part 5A measures every rung:

- symmetric LLL: p ≤ **1/(3e) = 0.12263** (the loose e-shape; q ≤ 0.3502)
- uniform-x general form: p ≤ **4/27 = 0.14815** (the exact uniform exchange rate; q ≤ 0.3849)
- Shearer: p ≤ **1/4 = 0.25** (exact for the path; q ≤ 1/2 — and at exactly p = 1/4 the finite paths stay marginally inside: μ(P_m, 1/4) = (m+2)/2^{m+1} > 0, the identity of Exercise 7, machine-checked at m = 8, 16, 32: 10/512 = 0.01953, 18/131072 = 0.000137, 34/2^{33} = 3.96·10^{−9}).

The ladder and a witness tree, drawn as **Figure 2** — the three thresholds as zones on the p-line of the path P_m, and a two-level witness tree whose left branch carries the same-label A_j → A_i edge that Lemma 3's slot accounting prices:

```svg
<svg viewBox="0 0 640 210" width="640" height="210" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="The three certificate thresholds on the path P_m and a Moser-Tardos witness tree">
  <style>
    .ld-axis { stroke: #1e293b; stroke-width: 2; }
    .ld-tick { stroke: #1e293b; stroke-width: 1.6; }
    .ld-txt { font-family: Georgia, serif; font-size: 11.5px; fill: #1e293b; text-anchor: middle; }
    .ld-title { font-family: Georgia, serif; font-size: 12.5px; font-weight: bold; fill: #0f172a; }
    .wt-node { fill: #f1f5f9; stroke: #334155; stroke-width: 1.8; }
    .wt-edge { stroke: #475569; stroke-width: 1.6; }
  </style>
  <!-- Left Panel: Threshold Ladder on P_m (d = 2) -->
  <text class="ld-title" x="25" y="28">Threshold Ladder on Path P_m (d = 2)</text>
  <!-- Zones along p in [0, 0.30], mapped to x in [30, 390] (1200 px per unit p) -->
  <rect x="30"  y="68" width="147" height="26" fill="#dcfce7" stroke="#16a34a" stroke-width="1"/>
  <rect x="177" y="68" width="31"  height="26" fill="#fef9c3" stroke="#ca8a04" stroke-width="1"/>
  <rect x="208" y="68" width="122" height="26" fill="#dbeafe" stroke="#2563eb" stroke-width="1"/>
  <rect x="330" y="68" width="65"  height="26" fill="#fee2e2" stroke="#dc2626" stroke-width="1"/>
  <line class="ld-axis" x1="30" y1="94" x2="395" y2="94"/>
  <!-- Ticks at p = 0, 1/(3e)=0.1226, 4/27=0.1481, 1/4=0.25 -->
  <line class="ld-tick" x1="30"  y1="90" x2="30"  y2="100"/><text class="ld-txt" x="30"  y="115">0</text>
  <line class="ld-tick" x1="177" y1="64" x2="177" y2="100"/><text class="ld-txt" x="158" y="56">1/(3e) ≈ 0.123</text>
  <line class="ld-tick" x1="208" y1="64" x2="208" y2="104"/><text class="ld-txt" x="226" y="122">4/27 ≈ 0.148</text>
  <line class="ld-tick" x1="330" y1="64" x2="330" y2="100"/><text class="ld-txt" x="330" y="56">1/4 = 0.250</text>
  <text class="ld-txt" x="103" y="85" font-size="10.5">Sym LLL</text>
  <text class="ld-txt" x="269" y="85" font-size="10.5">Shearer Region</text>
  <text class="ld-txt" x="362" y="85" font-size="10.5">Wall</text>
  <text class="ld-txt" x="210" y="152" font-size="11">Uniform General LLL adds +21% window (4/27 vs. 1/3e);</text>
  <text class="ld-txt" x="210" y="170" font-size="11">Shearer reaches p = 1/4 where μ(P_m, 1/4) = (m+2)/2^(m+1) > 0.</text>
  <!-- Right Panel: Witness Tree τ_t -->
  <rect x="425" y="16" width="198" height="178" rx="6" fill="#f8fafc" stroke="#cbd5e1" stroke-width="1.3"/>
  <text class="ld-title" x="442" y="38">Witness Tree τ_t (Lemma 2)</text>
  <line class="wt-edge" x1="524" y1="66" x2="484" y2="112"/>
  <line class="wt-edge" x1="524" y1="66" x2="564" y2="112"/>
  <line class="wt-edge" x1="484" y1="112" x2="484" y2="158"/>
  <circle class="wt-node" cx="524" cy="66"  r="16"/><text class="ld-txt" x="524" y="70">A_i</text>
  <circle class="wt-node" cx="484" cy="112" r="16"/><text class="ld-txt" x="484" y="116">A_j</text>
  <circle class="wt-node" cx="564" cy="112" r="16"/><text class="ld-txt" x="564" y="116">A_k</text>
  <circle class="wt-node" cx="484" cy="158" r="16"/><text class="ld-txt" x="484" y="162">A_i</text>
  <text class="ld-txt" x="556" y="162" font-size="10.5">w(T) = ∏ p_v</text>
</svg>
```

And the floors table turns the ladder into a quantitative lesson: at q = 1/3, m = 32, the three certified floors for the survival probability are 0.0044 (LLL floor (1−x)^m), 0.01308 (Shearer floor μ), against an exact truth of 0.04915 — **every floor below the truth, every floor above the last** — a certificate is not a verdict, it is a *guarantee with a number on it*, and different certificates give wildly different numbers for the same process. At q ≥ 2/5 the LLL floors cease to exist (no certificate) while Shearer's keeps working to the wall — and Part 5B's receipts show the *algorithm* strolling even past the wall, with the worst-case caveat recorded honestly.

**The practice menu — P13 and P45, one diagnosis.** The union bound is the local lemma's densest special case, and the two are *incomparable*, not ranked — the lab made you watch the union bound win Part 1's small panels. So the last skill is triage:

1. **Sum the failure probabilities.** Σp_i < 1? Take the union bound and go home — it is cheaper, and at small scale it certifies *more* (Part 1a: every m ≤ 7 instance).
2. **Count entanglement.** Many events, sparse overlap: symmetric check e·p·(d+1) ≤ 1. Crowded: it fails — retune before abandoning.
3. **Retune the exchange rates** (the general form): solve x_i ← p_i/∏_{j∈Γ(i)}(1−x_j) from zero; the star passed only here. Convergence with all x_i < 1 is the certificate — and for uniform p on regular graphs it is provably equivalent to the degree calculus (Lecture 3 proved the k = 4 case outright).
4. **Not a product space?** Ask which pairs are *negatively* correlated — the lopsided graph pays only for those (Lecture 4).
5. **Need the object, not just its existence?** Run MT — the same certificate is the termination proof, and the algorithm works well beyond it (Part 2's control, Part 5B's line).
6. **Near Shearer's wall?** The bound is tight *somewhere* with that dependency graph — if your instance is close to the boundary, no certificate shape will save you; look for structure (lopsidedness, a better graph) or accept the truth gap.

**Where this chapter came from.** The Atlas's pattern survey recorded the lemma's in-corpus usage honestly: the load-bearing firings sit in a single survey batch, and the celebrated Johansson application is exposition-level — the survey could not promote the lemma on that corpus evidence alone, and left a decision open: a pattern of its own, or a strengthening of P13? The Atlas resolved the question by *structure*, not by census: the union bound (P13) is a one-line global ledger, while this chapter's object — rarity priced against local dependence, with its own certificate, its own boundary theorem, and its own algorithm — is a different kind of mathematics, not a scaled-up version of the same trick. The lemma therefore takes its own entry (P45) with the union bound as its parent and densest special case; the survey's open question is closed, and the survey's honest negatives (entropy compression's zero standalone firings, recorded in Lecture 5) are taught where they live. A chapter earns its place the same way a certificate does: by what it lets you verify, not by how often it was cited.

---

## The Trick Bag (reference card)

| # | Tool | Statement | Watch out |
|---|------|-----------|-----------|
| 1 | Symmetric LLL (Erdős–Lovász 1975) | e·p·(d+1) ≤ 1 ⇒ Pr[no bad event] > 0 | d+1, not d; the 1/e is slack — keep d^d/(d+1)^{d+1} in real work |
| 2 | Uniform-x general form | p ≤ d^d/(d+1)^{d+1}; optimal x = 1/(d+1) | Only for uniform p and uniform degree; otherwise bargain per seat |
| 3 | General certificate (Spencer 1977) | p_i ≤ x_i·∏_{j∈Γ(i)}(1−x_j) ⇒ survival ≥ ∏(1−x_i) | The floor is a *number you can print* — use it (Part 5A) |
| 4 | Jacobi tuning | x_i ← p_i/∏_{j∈Γ(i)}(1−x_j) from 0; converges with all x_i < 1 ⟺ certificate | For uniform p on regular graphs it reduces to the degree calculus (L3's k = 4 proof) |
| 5 | Hypergraph 2-coloring | p = 2^{1−k}; cert e·2^{1−k}(D+1) ≤ 1; m ≤ vΔ/k linear-in-v ceiling | On few vertices everything collides — the census goes silent (Part 3) |
| 6 | k-SAT | p = 2^{−k}; variable load L ≲ 2^{k}/(ek) ⇒ satisfiable | Union's fixed cap is 2^{k}−1 clauses total — the contrast that created the lemma |
| 7 | Lopsided LLL (Erdős–Spencer 1991) | Pr[A_i \| non-neighbors avoided] ≤ p_i suffices | Every declined edge is a promise of non-negative correlation — measure it (Part 4) |
| 8 | Moser–Tardos (2010) | Resample violated events; certificate ⇒ termination; E[res_i] ≤ x_i/(1−x_i) (and ≤ x_i/p_i when x_i ≤ 1−p_i) | The bound is worst-case over distributions; the algorithm out-patrols the certificate |
| 9 | Shearer's boundary (1985) | μ(G,p) > 0 on all induced subgraphs; path: p < 1/4 exact; μ(P_m,1/4) = (m+2)/2^{m+1} | No LLL shape crosses it; near the wall the truth gap is real (Part 5A) |
| 10 | Triage | Σp < 1 → P13; sparse many events → P45; heterogeneous → asymmetric; permutations → lopsided; constructive → MT | Certificates are incomparable — diagnose before you choose |

**Scars (recorded so you skip them).** (1) The e-slack: e·p·(d+1) ≤ 1 loses a factor (1+1/d)^d < e; real proofs keep d^d/(d+1)^{d+1} — the lab's 1/(3e) vs 4/27 ladder exists to make the loss visible. (2) The +1: the gang is d neighbors *plus the event itself*; d = 0 still charges the seat. (3) Choosing Γ greedily-sparse: an edge you don't draw needs independence *or* a measured lopsided discount — the neighbor panel's −0.01674 is what an unearned discount costs. (4) Expecting Σx to be the expectation bound: the MT Theorem 1.2 bound is Σ x_i/(1−x_i) (bounded above in the lab's coarse meter by Σ x_i/p_i when x_i ≤ 1−p_i); Σx_i itself is not the theorem's bound (independent events already show why: x = p, while the true expected resampling cost is p/(1−p) = x/(1−x) > x). (5) Reading a certificate as an estimate: at lab scale certificates sit far below the truth — they are guarantees, not predictions. (6) The lab's own design iterations — v = 50 to v = 70, the retired runtime-transition design, the single-run to 20-trial fix, and this session's criterion corrections — are all recorded in the appendix, because how the receipts changed is part of what they certify.

**Reading list (pin levels as verified this session).** Erdős–Lovász 1975, *Problems and results on 3-chromatic hypergraphs and some related questions*, in Infinite and Finite Sets Vol. II, pp. 609–627 (pinned). Spencer 1977, Discrete Math. 20:69–76 (pinned). Shearer 1985, Combinatorica 5(3):241–245 (pinned). Erdős–Spencer 1991, Discrete Appl. Math. 28 (volume pinned; pages not web-verified this session). Moser–Tardos 2010, J. ACM 57(2), Article 11 (pinned). Molloy 2019, JCTB 134:264–284 (pinned). Alon–Spencer, *The Probabilistic Method*, Chapter 5 (exposition, book level). Beck 1991, Random Structures & Algorithms 2(4):343–358 (flag level, not web-verified). Kolipaka–Szegedy 2011 (efficiency theorem; flag level, not web-verified). Lu–Székely, random injections lopsidedness (flag level, not web-verified).

---
## Exercises (graded: ●○○ easy · ●●○ moderate · ●●● tough)

Hints travel with the problems. ◆ **pattern unknown** problems come with no hint — diagnosing the tool is part of the problem; ◐ **Explorations** state what you should find, not a number to match. Machine-verified answers sit at the end of the chapter.

### Easy (●○○)

**Exercise 1 · The one-event audit.** A probability space with a single bad event A, p = 0.9. (a) Show the union bound certifies survival. (b) Show the symmetric local lemma does *not* (d = 0: e·p·1 = 2.45 > 1). (c) Show the general form certifies it anyway, with floor exactly 1 − x₁, and identify the best x₁. (d) Conclude: for a single event the general form is *exact* and the symmetric form's 1/e is pure loss — the first glimpse that the forms are incomparable in both directions. *Hint: with d = 0 the certificate p₁ ≤ x₁ is asking almost nothing.*

**Exercise 2 · A 10-SAT certificate.** An instance has clauses of width k = 10 over n variables, and every variable appears in at most L = 4 clauses. (a) Show each clause is violated with probability exactly 2^{−10}. (b) Show any clause shares variables with at most D ≤ 30 others. (c) Verify the symmetric certificate e·(1/1024)·31 ≈ 0.082 ≤ 1, and conclude the instance is satisfiable — with no assumption on the number of clauses beyond counting incidences (m ≤ 2n/5). *Hint: a clause's 10 variables each sit in at most 3 other clauses.*

**Exercise 7 · The Shearer identity on the path.** Let μ(P_m, p) = Σ_k (−1)^k·I_k(P_m)·p^k with I_k the number of independent k-sets of the path. The receipts use the recursion μ(P_m, p) = μ(P_{m−1}, p) − p·μ(P_{m−2}, p) with μ(P_0, p) = μ(P_1, p) = 1. Prove by induction that **μ(P_m, 1/4) = (m+2)/2^{m+1}**, and check m = 8, 16, 32 against the lab's printed values (10/512, 18/131072, 34/2^{33}). *Hint: the induction step is two lines of algebra on the recursion — this is P4's cameo in this chapter.*

**Exercise 9 · The exact ceiling for 5-uniform coloring.** For 5-uniform hypergraph 2-coloring the bad events have p = 2^{1−5} = 1/16. (a) Show the symmetric certificate reads e·(1/16)·(D+1) ≤ 1, i.e. D ≤ 4. (b) Show the *exact* uniform-x ceiling is D ≤ 5: verify x(1−x)^D ≥ 1/16 holds at D = 5 (5^5/6^6 = 0.0670 ≥ 0.0625) and fails at D = 6 (6^6/7^7 = 0.0567 < 0.0625). (c) Conclude that the general form certifies strictly more than the symmetric form here, and explain why no asymmetric assignment can rescue D = 6. *Hint: the same maximization as Exercise 3; the event-graph translation itself is the P25 cameo.*

### Moderate (●●○)

**Exercise 3 · The optimal symmetric bound, completely.** Maximize f(x) = x(1−x)^d over x ∈ (0,1). (a) Show the maximum is d^d/(d+1)^{d+1} at x = 1/(d+1). (b) Derive the loose form e·p·(d+1) ≤ 1 from (1+1/d)^d < e, and show the loss is real: at d = 2 the exact ceiling 4/27 = 0.1481 against the loose 1/(3e) = 0.1226 — a 21% window surrendered to a two-line shortcut. (c) Where exactly in Lecture 2's proof does the 1/e enter, and why does the exact form avoid it? *This is the chapter's most reused computation — Lecture 2, Exercise 9, and the Part 5A ladder all run on it.*

**Exercise 4 · The dice circle, three floors deep.** Lecture 1's 100 fair dice in a circle, A_i = "die i and die i+1 both show six" (indices cyclic). (a) Certify with the symmetric form: e·(1/36)·3 ≈ 0.227 ≤ 1. (b) Certify with the uniform general form and *print the floor*: (1−x)^{100} = (2/3)^{100} = 2.46·10^{−18} — positive, verified, and astronomically small. (c) Explain why the wraparound pair (die 100, die 1) does not change d. (d) For the 3-dice circle, compute the exact survival probability by enumeration (216 outcomes): 200/216 ≈ 0.926, and compare with the LLL floor (2/3)³ ≈ 0.296 — the floor is honest, not tight. *Hint for (d): inclusion–exclusion over three events.*

**Exercise 8 · Reading the meter.** Moser–Tardos (Theorem 1.2) gives E[resamplings of A_i] ≤ x_i/(1−x_i), and when x_i ≤ 1−p_i the lab's coarse ratio x_i/p_i bounds this above (with x₁/p = 1/(1−x₁) = 1 + x₁/(1−x₁) at D = 1). (a) Show E[total resamplings] ≤ Σ_i x_i/(1−x_i) ≤ Σ_i x_i/p_i (for x_i ≤ 1−p_i). (b) For the lab's Part 2a instances (p = 1/8, degrees 0 or 1), show the coarse per-instance meter Σ_i x_i/p_i is (#degree-0)·1 + (#degree-1)·1.172 (while the tight Theorem 1.2 bound Σ_i x_i/(1−x_i) is (#degree-0)·(1/7) + (#degree-1)·0.1716), and quote the panel's mean coarse bound 5.592 (and mean tight bound 0.8134) against the measured mean 0.65. (c) Explain the gap: the bound is worst-case over *all* distributions with this dependency graph, the lab samples the product measure — the easiest one. This is P10's cameo: an expectation statement is only as good as the distribution it prices. *Hint: x(D=1) = 0.1464, so x/(1−x) = 0.1716 and x/p = 1.172; x(D=0) = p, so x/(1−x) = 1/7 and x/p = 1.*

**Exercise 10 · The neighbor's tax, in numbers.** The lab's Part 4, panel b: two 3-cell boards sharing their column set; over all 720 permutations, a₁ = a₂ = 426 miss their board (so each hit event has probability 294/720), and ab = 240 miss both. (a) Compute P(A₁∧A₂) = 108/720 = 0.15. (b) Compute P(A₁ | Ā₂) = 0.4366 and compare with P(A₁) = 0.4083. (c) Conclude: conditioning on the neighbor's survival makes failure *more* likely — the lopsided hypothesis fails across this edge, so the graph must draw it and the certificate must pay for it. (d) Contrast with panel a (ab = 265): show the conditional there *drops* below the unconditional, which is exactly what a declined edge promises. *Hint: the two-event equivalence of Lecture 4 turns this into one subtraction.*

**Exercise 11 · Certificates are incomparable, and the graph is a claim.** (a) *Union wins:* let A₁ = A₂ be the same event with p = 0.49 (so they are neighbors, d = 1). Show the union bound certifies survival (Σp = 0.98 < 1) while *every* form of the lemma refuses — even asymmetrically, x(1−x) ≤ 1/4 < 0.49 at both seats. (b) *Lemma wins:* the 100-dice circle of Exercise 4, where the union bound's ledger reads 100/36 ≈ 2.8. (c) *Choosing Γ is an act:* a cycle of events each of probability 0.1, each interacting only with its two cyclic neighbors. Show the honest graph (the cycle, d = 2) certifies — e·0.1·3 = 0.816 ≤ 1 — while the "lazy" graph connecting all pairs within distance 2 (defensible only if you cannot prove the missing independence) destroys the certificate: e·0.1·5 = 1.36 > 1. Every edge you cannot justify is a tax. *Hint for (a): the two seats bargain over the same single x each round.*

**Exercise 12 · The 4/27 window on the line.** For events of degree d = 2 (the line process of Part 5A, p = q²): (a) show the uniform-x certificate threshold is exactly p ≤ 4/27 with x = 1/3; (b) show this window is 21% wider than the symmetric form's 1/(3e) — the ratio 4/27 ÷ 1/(3e) ≈ 1.21; (c) translate to the lab's ladder: q ≤ 0.3849 against the symmetric q ≤ 0.3502, both still short of Shearer's q = 1/2. (d) Why does the general form not simply *replace* the symmetric form everywhere? (Think about what you must compute.)

### Tough (●●●)

**Exercise 5 · Price the second star.** One hub clause of width 5 (p = 1/32) and ten satellite clauses of width 3 (p = 1/8), each satellite sharing exactly one variable with the hub and none with each other. (a) Show the union bound fails: Σp = 1.28125 > 1. (b) Show the symmetric form fails: e·(1/8)·11 = 3.74 > 1. (c) Solve the two-seat bargaining system x_c = (1/32)/(1−x_s)^{10}, x_s = (1/8)/(1−x_c) by Jacobi iteration from zero; verify convergence to **x_c = 0.1549, x_s = 0.1479** with both below 1 — the certificate holds, and the instance is satisfiable. (d) Σx = 1.634: reconcile this with Exercise 8's meters (Σx_i/(1−x_i) = 1.919 and Σx_i/p_i = 16.79 are the runtime bounds, Σx_i is not). *Hint: ten leanings is past the k = 4 hub's capacity (Exploration 16) — the width-5 hub absorbs what the width-4 one cannot.*

**Exercise 6 · Count the witness trees.** (a) A single event with p = 1/8: show directly that the resampling algorithm's expected number of resamplings is p/(1−p) = 0.1429 (a geometric series — each resampling restarts the experiment fresh). (b) Two clauses sharing one variable (d = 1, p = 1/8 each): enumerate the consistent neighbor-alternating witness chains rooted at clause 1 — they are the alternating chains A→B→A→… of sizes 1, 2, 3, …, one shape per size, each demanding probability p per node — and sum: Σ_k p^k = 0.1429 again, an upper bound on E[resamplings of A]. (c) Compare with the theorem's coarse meter x/p = 1.1716 (and tight Theorem 1.2 bound x/(1−x) = 0.1716): the chain sum is 8.2× tighter than x/p here. (d) Sanity-check against the lab: Part 2a's 40 five-clause instances averaged 0.65 total resamplings — about 0.13 per clause, comfortably inside your bound. Explain why the bound is an overestimate even for the easiest process. *Hint for (b): because {A, B} forms a single shared-variable clique, every earlier step in the backward scan attaches to the unique deepest leaf, making every witness tree a unary chain.*

### ◆ Pattern unknown (no hints — diagnosing the tool is the problem)

**◆ 13.** Show that some outcome of the 100-dice circle has no adjacent pair of sixes.

**◆ 14.** Each of 100 events has probability 0.03, and each is independent of all but at most 4 of the others. Prove that some point of the probability space avoids all hundred.

**◆ 15.** Prove that every 3-uniform hypergraph with at most 3 edges is 2-colorable (no edge monochromatic).

### ◐ Explorations (state what you should find)

**◐ 16 · The hub's capacity.** Fix the width-4 hub (p = 1/16) and grow the crowd: s satellites of width 3 (p = 1/8), each sharing one variable with the hub and none with each other. Solve the fixed-point system for s = 1, 2, …, 12 and find the exact s where the certificate dies. You should find that s = 8 certifies (the lab's Part 6 star) and that s = 9 already diverges — a sharp capacity, set by the hub's width.

**◐ 17 · Floors near the wall.** On the path with m = 32 events (p = q²), take q = 0.49. You should find: no LLL certificate of any shape (p = 0.2401 > 4/27), a Shearer floor that is *positive but microscopic* (μ(P_32, 0.2401) ≈ 1.4·10^{−7} by the recursion), and an exact truth around 1.4·10^{−3} — four orders above the best certified floor. Reflect: what does a certificate buy when the wall is this close?

**◐ 18 · The algorithm beyond the wall.** Run the Part 5B engine (the same biased-bit line process) at q = 9/10, m = 16, 100 trials. You should find medians in the tens (our check run, seed 20261089: median 45, mean 46.9, max 94, no caps at 50,000) — the wall is real for the *algorithm* too, just far beyond the certificate's fence. Watch how the round distribution spreads compared to Part 5B's q = 3/5 panel.

---
## Computational Lab (verified)

*Every run below uses the chapter's documented engine: the Lehmer/MINSTD generator x ← 48271·x mod (2³¹−1). One continuous stream — **stream A, seed 20261083** — carries Parts 1a → 2a → 2b → 3a in exactly that order; fresh engines start at seeds 20261084 (Part 1b), 20261085 (Part 3b), 20261086 (Part 4), 20261087 (Part 5B), 20261088 (Part 6's resampling panel). Parts 5A and 6's certificate panels are deterministic — no draws. All draws are integer-exact: an index in range N is `nxt() % N`; a fair bit is `nxt() % 2`; a biased bit with P(1) = k/d happens iff `nxt()*d < k*M31`; a clause's k distinct variables come from a partial Fisher–Yates (one draw per index, i from n−1 down to n−k), and its k sign bits are drawn AFTER the Fisher–Yates; hypergraph edges draw no sign bits; the Part 4 board permutations are full Fisher–Yates (one draw per index, i from n−1 down to 0). The printed Python reproduces every receipt value-for-value; the resampling panels pick the lowest-index violated event and resample its variables in listed order. The engine's own bug history — a p-slip, a one-index slip, two unreproducible rounds lists, and a color convention — is in the Verification Notes.*

### Part 1 — The k-SAT dependency censuses (Lectures 1–2)

The census asks Lecture 1's question with a machine: how often does the symmetric certificate (here D ≤ 1, since e·(1/8)·(D+1) ≤ 1 exactly at D = 1) approve a random instance, and does it ever lie? Every instance is brute-checked against all 4,096 assignments. The n = 48 panel is the lemma's payoff slice: from m = 8 the union bound's ledger Σp = m/8 is ≥ 1 and dies, while the local certificate — blind to m, pricing only the degree — still fires.

```python
M31 = 2147483647
def engine(seed):
    x = [seed]
    def nxt():
        x[0] = 48271 * x[0] % M31
        return x[0]
    return nxt

def draw_clause(nxt, n, k, signs=True):
    if k <= 0 or k > n:
        return []
    arr = list(range(n))
    for i in range(n-1, n-k-1, -1):        # partial Fisher-Yates, one draw per index
        j = nxt() % (i+1)
        arr[i], arr[j] = arr[j], arr[i]
    vs = arr[n-k:]
    if not signs:                          # hypergraph edge: no sign draws
        return [(v, 1) for v in vs]
    return [(v, nxt() % 2) for v in vs]    # k sign bits, AFTER the FY draws

def degrees(clauses):                     # D_i = # other clauses sharing a variable
    m = len(clauses)
    if m == 0:
        return [0]
    return [sum(1 for e in range(m)
                if e != c and any(l1[0] == l2[0]
                                  for l1 in clauses[c] for l2 in clauses[e]))
            for c in range(m)]

def violated(clauses, bits):               # lowest-index clause, all literals false
    for c, cl in enumerate(clauses):
        if all(bits[v] != s for v, s in cl):
            return c
    return -1

def brute_sat(clauses, n):                 # some assignment satisfies every clause
    for mask in range(1 << n):
        if all(any((mask >> v) & 1 == s for v, s in cl) for cl in clauses):
            return True
    return False

def mt(nxt, clauses, n, cap=5000):        # resampling; rounds = resampled events
    bits = [nxt() % 2 for _ in range(n)]   # init: n fair bits in variable order
    r = 0
    while r < cap:
        c = violated(clauses, bits)
        if c < 0:
            return r
        for v, _ in clauses[c]:            # resample listed order, fair bits
            bits[v] = nxt() % 2
        r += 1
    return r

def census_1a(nxt):                        # n=12, k=3, m=3..10, 100 instances each
    for m in range(3, 11):
        sD = cert = sat = cbad = 0
        for _ in range(100):
            cl = [draw_clause(nxt, 12, 3) for _ in range(m)]
            Dmax = max(degrees(cl))
            ok = brute_sat(cl, 12)
            sD += Dmax; sat += ok
            if Dmax <= 1:                  # the sound symmetric certificate
                cert += 1
                if not ok: cbad += 1
        print(m, sD/100, cert, sat, cbad)

def census_1b():                           # n=48, all-positive, fresh engine
    nxt = engine(20261084)
    for m in (8, 10, 12):
        sD = cert = 0
        for _ in range(100):
            cl = [draw_clause(nxt, 48, 3, signs=False) for _ in range(m)]
            Dmax = max(degrees(cl))
            sD += Dmax
            if Dmax <= 1: cert += 1
        print(m, sD/100, cert, m <= 7)     # union certifies iff m <= 7
```

The stream-A driver — the four panels share one engine, in this exact order:

```python
nxt = engine(20261083)         # stream A
census_1a(nxt)                 # Part 1a (receipts below)
panel_2a(nxt); panel_2b(nxt)   # Part 2 (next section) — stream continues
census_3a(nxt)                 # Part 3a — stream continues
census_1b()                    # fresh engine, seed 20261084
```

Receipts — Part 1a (n = 12, k = 3, m = 3..10, 100 instances each, stream A; certificate = symmetric D ≤ 1; union approves iff m ≤ 7):

| m | meanD | LLLcert | bruteSAT | cert∧SAT | cert∧¬SAT |
|---|-------|---------|----------|----------|-----------|
| 3 | 1.62 | 36 | 100 | 36 | 0 |
| 4 | 2.43 | 8 | 100 | 8 | 0 |
| 5 | 3.31 | 0 | 100 | 0 | 0 |
| 6 | 4.15 | 0 | 100 | 0 | 0 |
| 7 | 4.94 | 0 | 100 | 0 | 0 |
| 8 | 5.84 | 0 | 100 | 0 | 0 |
| 9 | 6.52 | 0 | 100 | 0 | 0 |
| 10 | 7.42 | 0 | 100 | 0 | 0 |

800 census instances, each brute-checked (all 4,096 assignments) and certificate-checked, zero conflicts — the certificate never approves an unsatisfiable instance. And the honest counterpoint: the union bound approves *every* instance with m ≤ 7, out-certifying the local form at these sizes. The two certificates are incomparable — Lecture 1's stinging observation, machine-recorded.

Receipts — Part 1b (n = 48, all-positive clauses, no sign draws, seed 20261084):

| m | meanD | LLLcert (D ≤ 1) | union (m ≤ 7) |
|---|-------|---------|-------|
| 8 | 2.37 | 13/100 | 0 |
| 10 | 3.23 | 2/100 | 0 |
| 12 | 3.84 | 0/100 | 0 |

The payoff slice: from m = 8 the union bound is dead everywhere, and the local certificate still fires 13 times in a hundred — the shape (degree, not total) buying what the ledger cannot.

### Part 2 — Moser–Tardos: certified vs. entangled (Lecture 5)

Two panels on the continuing stream. Panel (a) rejects until the instance is certified (D ≤ 1) and runs the resampling algorithm; panel (b) rejects until the instance is *satisfiable but uncertified* (brute-SAT ∧ D ≥ 5) — deliberately entangled — and runs the same algorithm. The theorem promises nothing for panel (b)'s instances; the machine reports what actually happens. The tight Moser–Tardos Theorem 1.2 bound is E[resamplings of A_i] ≤ x_i/(1−x_i), bounded above here by the probability-ratio meter x_i/p_i (so E[total] ≤ Σ x_i/(1−x_i) ≤ Σ x_i/p_i) with x_i the small root of x(1−x)^{D_i} = p.

```python
def panel_2a(nxt):                        # n=20, m=5, reject until D <= 1
    x1 = (1 - 0.5 ** 0.5) / 2             # root of x(1-x) = 1/8   (D = 1)
    x0 = 0.125                            # root of x = 1/8        (D = 0)
    rounds, bounds, tight, floors, tries = [], [], [], [], 0
    while len(rounds) < 40:
        tries += 1
        cl = [draw_clause(nxt, 20, 3) for _ in range(5)]
        D = degrees(cl)
        if max(D) > 1:
            continue
        rounds.append(mt(nxt, cl, 20))
        bnd, tbnd, flr = 0.0, 0.0, 1.0
        for d in D:
            x = x0 if d == 0 else x1
            bnd += x / 0.125              # coarse ratio meter: x_i/p_i
            tbnd += x / (1 - x)            # MT Theorem 1.2 bound: x_i/(1-x_i)
            flr *= (1 - x)                # general-form survival floor
        bounds.append(bnd); tight.append(tbnd); floors.append(flr)
    print('tries', tries)
    print('rounds', rounds)
    print('mean', sum(rounds)/40, 'max', max(rounds))
    print('mean bound', sum(bounds)/40, 'mean tight', sum(tight)/40, 'mean floor', sum(floors)/40)

def panel_2b(nxt):                        # n=12, m=9, reject until SAT and D >= 5
    rounds, tries = [], 0
    while len(rounds) < 30:
        tries += 1
        cl = [draw_clause(nxt, 12, 3) for _ in range(9)]
        if max(degrees(cl)) < 5 or not brute_sat(cl, 12):
            continue
        rounds.append(mt(nxt, cl, 12))
    print('tries', tries)
    print('rounds', rounds)
    print('mean', sum(rounds)/30, 'max', max(rounds))
```

Receipts — panel (a), certified (n = 20, m = 5, k = 3, rejection until D ≤ 1): **554 tries for 40 instances**; rounds per instance

[0,0,2,0,0,2,2,1,0,4,1,1,1,1,0,1,0,0,0,0,1,0,0,1,0,0,0,1,1,2,0,0,0,0,0,1,2,0,1,0]

40/40 terminated; **mean 0.65, max 4**. Theory anchors (deterministic): x(D=1) = (1−√(1/2))/2 = 0.146447, x/(1−x) = 0.17157, x/p = 1.17157; x(D=0) = 0.125, x/(1−x) = 1/7 ≈ 0.14286, x/p = 1. The panel's instances give **mean coarse bound Σ x_i/p_i = 5.592** (and **mean tight Theorem 1.2 bound Σ x_i/(1−x_i) = 0.8134**) — worst-case bounds over all distributions sharing the dependency graph; the sampled product-measure process sits below both (the same honest caveat as Part 5B). The general-form survival floor ∏(1−x_i) has **mean 0.4709** over the 40 instances.

Receipts — panel (b), uncertified control (n = 12, m = 9, rejection until brute-SAT ∧ D ≥ 5): **31 tries for 30 instances**; rounds

[4,2,3,1,2,2,3,1,2,1,0,10,1,3,1,2,0,3,3,0,2,1,1,0,9,1,4,1,0,4]

30/30 terminated; **mean 2.23, max 10**. The certificate is sufficient, not necessary: the algorithm patrols far beyond its fence, and the entangled instances cost about 3.4× the resamplings of the certified ones at these sizes.

### Part 3 — Hypergraph Property B, two censuses (Lecture 3)

The same census in the coloring world: k = 4 edges on v vertices, a random 2-coloring makes each edge monochromatic with p = 2^{1−k} = 1/8 exactly. The sound certificates: symmetric D ≤ 1, uniform-general D ≤ 2 — and D ≤ 2 is also the exact asymmetric criterion, since max x(1−x)³ = 27/256 < 1/8. The brute check is two-sided (an edge is monochromatic in *either* color).

```python
def brute_col(edges, v):                  # Property B: some 2-coloring, no mono edge
    for mask in range(1 << v):
        if all(len({(mask >> w) & 1 for w, _ in e}) == 2 for e in edges):
            return True
    return False

def census_3a(nxt):                        # v=14, k=4, m=4,6,...,16, 100 each
    for m in (4, 6, 8, 10, 12, 14, 16):
        sD = sym = gen = col = scol = sbad = gcol = 0
        for _ in range(100):
            edges = [draw_clause(nxt, 14, 4, signs=False) for _ in range(m)]
            Dmax = max(degrees(edges))
            ok = brute_col(edges, 14)
            sD += Dmax; col += ok
            if Dmax <= 1:
                sym += 1; scol += ok; sbad += (not ok)
            if Dmax <= 2:
                gen += 1; gcol += ok
        print(m, sD/100, sym, gen, m <= 7, col, scol, sbad, gcol)

def census_3b():                           # v=70, fresh engine
    nxt = engine(20261085)
    for m in (16, 18):
        sD = sym = gen = v1 = 0
        for _ in range(100):
            edges = [draw_clause(nxt, 70, 4, signs=False) for _ in range(m)]
            Dmax = max(degrees(edges))
            sD += Dmax
            if Dmax <= 1: sym += 1
            if Dmax <= 2: gen += 1
            if Dmax <= 4: v1 += 1          # superseded criterion, kept for the record
        print(m, sD/100, sym, gen, v1)
```

Receipts — Part 3a (v = 14, k = 4, stream A; union approves iff m ≤ 7):

| m | meanD | cert_sym (D≤1) | cert_gen (D≤2) | union (m≤7) | bruteCol | sym∧col | sym∧¬col | gen∧col |
|---|-------|------|------|-------|------|------|------|------|
| 4 | 2.83 | 1 | 16 | 100 | 100 | 1 | 0 | 16 |
| 6 | 4.84 | 0 | 0 | 100 | 100 | 0 | 0 | 0 |
| 8 | 6.62 | 0 | 0 | 0 | 100 | 0 | 0 | 0 |
| 10 | 8.63 | 0 | 0 | 0 | 100 | 0 | 0 | 0 |
| 12 | 10.55 | 0 | 0 | 0 | 100 | 0 | 0 | 0 |
| 14 | 12.31 | 0 | 0 | 0 | 100 | 0 | 0 | 0 |
| 16 | 14.17 | 0 | 0 | 0 | 100 | 0 | 0 | 0 |

700/700 brute-colorable (soundness: sym∧¬col = 0); at lab scale both local certificates fall nearly silent while the union bound also dies at m = 8 — the honest certificate-truth gap, with one glimpse of the general form's power: at m = 4 it certifies 16× what the symmetric form does.

Receipts — Part 3b (v = 70, seed 20261085; the v = 50 design was retired — its certificate regions did not overlap at that size):

| m | meanD | cert_sym (D≤1) | cert_gen (D≤2) | union | v1 criterion (D≤4, superseded) |
|---|-------|------|------|-------|------|
| 16 | 5.82 | 0/100 | 0/100 | 0 | 13/100 |
| 18 | 6.73 | 0/100 | 0/100 | 0 | 1/100 |

An honest negative, printed as run: with the corrected certificate every certificate is silent on this panel (at lab scale the k = 4 censuses never met an uncolorable instance). The "LLL-beats-union" story lives in the k-SAT panel 1b, whose D ≤ 1 certificate is sound because a clause is violated with p = 2^{−k} exactly; the v1 "D ≤ 4" column is the p-slip's fossil, kept for the record.

### Part 4 — Lopsidedness: measuring the neighbor's tax (Lecture 4)

Two 3-cell boards inside the 6×6 grid; a permutation σ (rows → columns) *hits* a board if it touches any of its cells; the bad events are the hits. The lopsided hypothesis asks: does conditioning on a *declined* edge's survival lower the failure chance? The machine counts misses over all 720 permutations exactly. Boards are drawn by full Fisher–Yates; the counts are isomorphism-invariant, so every sample prints the same numbers — that invariance is itself the derangement cameo below.

```python
def full_fy(nxt, cols):                    # full Fisher-Yates, one draw per index
    p = list(cols)
    for i in range(len(p)-1, -1, -1):
        j = nxt() % (i+1)
        p[i], p[j] = p[j], p[i]
    return p

def board(nxt, rows, cols):                # one forbidden cell per row
    p = full_fy(nxt, cols)
    return [(r, p[i]) for i, r in enumerate(rows)]

def miss_counts(n, B1, B2):                # over ALL n! permutations: rows -> cols
    T = [0, 0, 0, 0]                       # total, miss1, miss2, miss both
    used, cur = [False]*n, [0]*n
    def rec(r):
        if r == n:
            T[0] += 1
            m1 = all(cur[r] != c for r, c in B1)
            m2 = all(cur[r] != c for r, c in B2)
            T[1] += m1; T[2] += m2; T[3] += (m1 and m2)
            return
        for c in range(n):
            if not used[c]:
                used[c] = True; cur[r] = c
                rec(r+1)
                used[c] = False
    rec(0)
    return T[1], T[2], T[3], T[0]

nxt = engine(20261086)
for _ in range(6):                         # (a) NON-neighbors: disjoint rows AND cols
    B1 = board(nxt, [0,1,2], [0,1,2])
    B2 = board(nxt, [3,4,5], [3,4,5])
    a1, a2, ab, T = miss_counts(6, B1, B2)
    print('a', a1, a2, ab, ab/T - (a1/T)**2)
for _ in range(6):                         # (b) shares the column set: NEIGHBORS
    B1 = board(nxt, [0,1,2], [0,1,2])
    B2 = board(nxt, [3,4,5], [0,1,2])
    a1, a2, ab, T = miss_counts(6, B1, B2)
    print('b', a1, a2, ab, ab/T - (a1/T)**2)
for _ in range(3):                         # (c) n=8, 4+4 split non-neighbors
    B1 = board(nxt, [0,1,2,3], [0,1,2,3])
    B2 = board(nxt, [4,5,6,7], [4,5,6,7])
    a1, a2, ab, T = miss_counts(8, B1, B2)
    print('c', a1, a2, ab, ab/T - (a1/T)**2)
```

Receipts (seed 20261086; gap = covariance of the miss events = covariance of the hit events, complement-invariant):

- **(a) non-neighbors, 6 samples, all identical:** a₁ = a₂ = 426, ab = 265, gap = 265/720 − (426/720)² = **+0.01799** ≥ 0. 6/6 positive — the declined edge's promise holds.
- **(b) column-sharing neighbors, 6 samples, all identical:** a₁ = a₂ = 426, ab = 240, gap = **−0.01674** < 0. 6/6 NEGATIVE — the lopsided discount FAILS across the neighbor relation; the graph is load-bearing, and the certificate must pay for this edge.
- **(c) n = 8, 4+4 non-neighbors, 3 samples identical:** a₁ = a₂ = 24024, ab = 14833, gap = **+0.01286** ≥ 0.

The cameo: ab = 265 = D₆ and 14833 = D₈, the derangement numbers — the two boards jointly forbid the diagonal, which is why the counts are isomorphism-invariant (any board shape with distinct rows and columns is a relabeling of the diagonal's complement). Exercise 10 turns panels (a) and (b) into the conditional probabilities by hand.

### Part 5 — The three floors, and the algorithm at the fence (Lectures 2, 5–6)

**5A — deterministic.** The path P_m with m events A_i = (b_i ∧ b_{i+1}) on m+1 independent bits, each 1 w.p. q, p = q². Three floors on the survival probability: the certificate floor (1−x)^m (uniform seat, the small root of x(1−x)² = p), the Shearer floor μ(P_m, p), and the exact truth — a two-term DP over the m+1 bits. No draws anywhere.

```python
import math

def she_mu(m, p):                          # mu(P_m,p) = a_{m+1}, a_n = a_{n-1} - p*a_{n-2}
    a0 = a1 = 1.0
    for _ in range(m):
        a0, a1 = a1, a1 - p * a0
    return a1

def truth(m, q):                           # P(no adjacent 1-1) over m+1 iid bits
    t0 = t1 = 1.0
    for _ in range(m):
        t0, t1 = t1, (1-q)*t1 + q*(1-q)*t0
    return t1

def small_root(p):                         # x(1-x)^2 = p, the small root in [0, 1/3]
    lo, hi = 0.0, 1/3
    for _ in range(200):
        mid = (lo+hi)/2
        if mid*(1-mid)**2 < p: lo = mid
        else: hi = mid
    return (lo+hi)/2

for q in (1/3, 2/5, 9/20, 1/2):
    p = q*q
    for m in (8, 16, 32):
        row = [q, m, p <= 1/(3*math.e), p <= 4/27,
               all(she_mu(j, p) > 0 for j in range(1, m+1))]
        if p <= 4/27:
            row.append((1 - small_root(p))**m)     # certificate floor
        row.append(she_mu(m, p))                    # Shearer floor
        row.append(truth(m, q))                     # exact truth
        print(row)
print(she_mu(8, 0.25), (8+2)/2**9)          # the Exercise 7 identity
print(she_mu(16, 0.25), (16+2)/2**17)
print(she_mu(32, 0.25), (32+2)/2**33)
```

Receipts — 5A (symCert: p ≤ 1/(3e) = 0.12263; genCert: p ≤ 4/27 = 0.14815; sheCert: μ(P_j, p) > 0 for all j ≤ m):

| q | p | m | symCert | genCert | sheCert | lllFloor | sheFloor | exact truth |
|---|---|---|---|---|---|---|---|---|
| 1/3 | 0.1111 | 8 | yes | yes | yes | 0.25755 | 0.3437 | 0.4642 |
| 1/3 | 0.1111 | 16 | yes | yes | yes | 0.06633 | 0.11561 | 0.2196 |
| 1/3 | 0.1111 | 32 | yes | yes | yes | 0.0044 | 0.01308 | 0.04915 |
| 2/5 | 0.16 | 8 | no | no | yes | — | 0.17896 | 0.3317 |
| 2/5 | 0.16 | 16 | no | no | yes | — | 0.03002 | 0.1134 |
| 2/5 | 0.16 | 32 | no | no | yes | — | 0.00085 | 0.01326 |
| 9/20 | 0.2025 | 8 | no | no | yes | — | 0.08346 | 0.2458 |
| 9/20 | 0.2025 | 16 | no | no | yes | — | 0.00589 | 0.06294 |
| 9/20 | 0.2025 | 32 | no | no | yes | — | 0.00003 | 0.004129 |
| 1/2 | 0.25 | 8 | no | no | yes* | — | 0.01953 | 0.1738 |
| 1/2 | 0.25 | 16 | no | no | yes* | — | 0.00014 | 0.03190 |
| 1/2 | 0.25 | 32 | no | no | yes* | — | 3.96·10⁻⁹ | 0.001074 |

*The identity (Exercise 7): μ(P_m, 1/4) = (m+2)/2^{m+1} > 0 for every finite m — the finite paths stay marginally inside Shearer's region at exactly p = 1/4; the 1/4 wall is the m → ∞ limit. Checks: m = 8: 10/512 = 0.01953; m = 16: 18/131072 = 0.000137; m = 32: 34/2³³ = 3.96·10⁻⁹ (the last prints 0 at four decimals). Threshold ladder: symmetric p ≤ 1/(3e) (q ≤ 0.3502), uniform-general p ≤ 4/27 (q ≤ 0.3849), Shearer p ≤ 1/4 (q ≤ 1/2, with finite-m margin).

**5B — the algorithm at the fence (seed 20261087).** The same line process, now *run*: biased bits with P(1) = k/d, m events on m+1 bits, lowest-index violated event resampled (its two bits, in listed order). For each q: 100 trials at m = 16, then 40 trials at m = 32, one continuous stream; cap 50,000, never hit; the median is the upper median.

```python
def line_mt(nxt, k, d, m, trials, cap=50000):
    if m <= 0 or trials <= 0:
        return
    rs = []
    for _ in range(trials):
        bits = [1 if nxt()*d < k*M31 else 0 for _ in range(m+1)]
        r = 0
        while r < cap:
            v = next((i for i in range(m)
                      if bits[i] == 1 and bits[i+1] == 1), -1)
            if v < 0: break
            bits[v] = 1 if nxt()*d < k*M31 else 0     # listed order
            bits[v+1] = 1 if nxt()*d < k*M31 else 0
            r += 1
        rs.append(r)
    rs.sort()
    print(k, d, m, rs[len(rs)//2], sum(rs)/len(rs), rs[-1])

nxt = engine(20261087)
for k, d in ((2, 5), (9, 20), (1, 2), (11, 20), (3, 5)):
    line_mt(nxt, k, d, 16, 100)
    line_mt(nxt, k, d, 32, 40)
```

Receipts — 5B (q = k/d; med/mean/max/caps per cell):

| q | p | m=16 med/mean/max/caps | m=32 med/mean/max/caps |
|---|---|---|---|
| 2/5 | 0.16 | 2 / 2.4 / 7 / 0 | 5 / 4.9 / 11 / 0 |
| 9/20 | 0.203 | 3 / 3.3 / 9 / 0 | 7 / 7.3 / 16 / 0 |
| 1/2 | 0.25 | 3 / 3.8 / 11 / 0 | 8 / 8.1 / 16 / 0 |
| 11/20 | 0.303 | 5 / 5.0 / 18 / 0 | 10 / 10.1 / 21 / 0 |
| 3/5 | 0.36 | 6 / 6.4 / 13 / 0 | 14 / 13.8 / 21 / 0 |

The honest observation: THIS process stays easy well beyond Shearer's boundary — no caps anywhere, medians roughly doubling with m. The Kolipaka–Szegedy efficiency theorem (flag level, not web-verified) is a worst-case over configurations sharing the dependency graph, not a claim about every such process; this panel is the counterexample-shaped datum, and the chapter says so. The wall is real for the algorithm too — Exploration 18 pushes q to 9/10 and watches the medians hit the tens.

### Part 6 — The star, priced three ways (Lecture 2)

The nine-clause star that only the asymmetric form could certify: hub H = (v₀, v₁, v₂, v₃), width 4, p_H = 1/16; eight satellites S_i = (v_i, v_{4+2i}, v_{5+2i}), width 3, p_s = 1/8, each sharing exactly one variable with the hub and none with each other; 20 variables. The certificate panels are deterministic; then the resampling algorithm runs on it.

```python
import math
clauses = [[0,1,2,3]] + [[i, 4+2*i, 5+2*i] for i in range(8)]

print(1/16 + 8/8)                          # union: 1.0625 — FAILS
print(math.e * (1/8) * 9)                  # symmetric: 3.0581 — FAILS
xc = xs = 0.0                              # Jacobi from zero
for _ in range(10000):
    xc, xs = (1/16)/(1-xs)**8, (1/8)/(1-xc)
print(xc, xs, xc + 8*xs)                   # 0.3064 0.1802 1.748 — CERTIFIES
sat = sum(1 for mask in range(1 << 20)
          if all(any((mask >> v) & 1 for v in cl) for cl in clauses))
print(sat, sat / 2**20)                    # 373729 0.3564 — the truth

nxt = engine(20261088)
rounds = []
for _ in range(20):
    bits = [nxt() % 2 for _ in range(20)]            # init: 20 fair bits, var order
    r = 0
    while r < 5000:
        v = next((c for c, cl in enumerate(clauses)
                  if all(bits[w] == 1 for w in cl)), -1)
        if v < 0: break
        for w in clauses[v]:                         # resample listed order
            bits[w] = nxt() % 2
        r += 1
    rounds.append(r)
print(rounds, sum(rounds)/20, max(rounds))
```

The star's clauses are stored with sign bit 0 — a violated clause reads all-ones. The color convention is a coin flip (the flipped reading, all-zeros, gives a distributionally identical process on the same instance; its 20-trial list is recorded in the Verification Notes); the receipts follow the all-ones reading printed above.

Receipts — Part 6: **union Σp = 1.0625 > 1 — FAILS. Symmetric e·(1/8)·9 = 3.0581 > 1 — FAILS. General (asymmetric) form:** Jacobi fixed point x_c = p_H/(1−x_s)⁸, x_s = p_s/(1−x_c) from zero: **x_c = 0.3064, x_s = 0.1802**, both < 1 — CERTIFIES; Σx = x_c + 8·x_s = **1.748**. **Brute force: 373,729 satisfying assignments of 2²⁰ = 1,048,576 (35.64%)**. **MT (seed 20261088, 20 trials, cap 5000, never hit):** rounds = [2,1,0,0,1,0,0,2,1,2,0,2,1,1,4,1,0,0,1,3]; 20/20 terminated; **mean 1.10, max 4**. Recall 35.64% of all assignments already satisfy the star — MT's first round is free more often than not, and the certificate's promise and the algorithm's reality agree comfortably.

## Answers to the Exercises

*Worked answers for the twelve graded problems and the three ◆ pattern-unknown ones. The three ◐ Explorations state what you should find and get no worked answer — that is their point. Where an answer cites a machine receipt, the receipt exists: the lab above, from the chapter's documented engine (stream A seed 20261083 and the per-part seeds 20261084–20261089 as mapped there).*

**Answer 1 (the one-event audit).** (a) Union: Σp = 0.9 < 1, so P(Ā₁) ≥ 1 − 0.9 = 0.1 > 0 — and in fact exactly 0.1. (b) Symmetric with d = 0: e·p·(d+1) = e·0.9 ≈ 2.446 > 1 — the form demands p ≤ 1/e ≈ 0.368 and refuses. (c) General: Γ(1) is empty, so the seat condition is just p₁ ≤ x₁ — any x₁ ≥ 0.9 works. The floor 1 − x₁ is best (largest) at the smallest seat x₁ = 0.9: floor 0.1. (d) The truth is Pr[Ā₁] = 0.1: for a single event the general form is *exact* — its floor equals the survival probability. The symmetric form's 1/e is pure loss here, the first glimpse that the forms are incomparable in both directions: Part 1a's union wins (m ≤ 7) and Part 1b's lemma wins (m ≥ 8) are the same lesson at census scale.

**Answer 2 (a 10-SAT certificate).** (a) A width-10 clause is violated by exactly one of the 2¹⁰ literal patterns: p = 2⁻¹⁰ = 1/1024. (b) Each of the clause's 10 variables sits in at most L − 1 = 3 other clauses, so at most 30 other clauses share a variable with it: D ≤ 30. (c) e·(1/1024)·31 = 0.0823 ≤ 1 — every such instance is satisfiable. What the certificate never asked for: the number of clauses. Counting incidences bounds it (10m ≤ 4n, i.e. m ≤ 2n/5), but the proof runs without it — degree, not total, is the lemma's currency (Lecture 3's contrast in one line).

**Answer 3 (the optimal symmetric bound, completely).** (a) f′(x) = (1−x)^d − dx(1−x)^{d−1} = (1−x)^{d−1}(1 − (d+1)x), zero at x = 1/(d+1); f(1/(d+1)) = (1/(d+1))·(d/(d+1))^d = d^d/(d+1)^{d+1}. (b) Since (1+1/d)^d < e, we get d^d/(d+1)^{d+1} > 1/(e(d+1)); replacing the exact ceiling by the loose one gives e·p·(d+1) ≤ 1. At d = 2: exact 4/27 = 0.1481 against loose 1/(3e) = 0.1226 — a 21% window surrendered (0.1481/0.1226 = 1.208) to a one-line shortcut. (c) The 1/e enters Lecture 2's derivation exactly at the step (1 − 1/(d+1))^d ≥ 1/e — a lower bound on (d/(d+1))^d, tight only as d → ∞. The exact form never takes that step: it keeps the maximized value as is. The same computation returns in Exercise 9 and in the Part 5A ladder (q ≤ 0.3849 vs. q ≤ 0.3502).

**Answer 4 (the dice circle, three floors deep).** (a) p = 1/36, d = 2: e·(1/36)·3 = 0.2265 ≤ 1 — certified. (b) The chapter's uniform seat x = 1/(d+1) = 1/3: p = 1/36 ≤ (1/3)(2/3)² = 4/27, and the printed floor is (1−x)¹⁰⁰ = (2/3)¹⁰⁰ = 2.46·10⁻¹⁸ — positive, verified, astronomically small. Honest reading: the floor is a function of the seat. The smallest valid seat x ≈ 0.0295 (the small root of x(1−x)² = 1/36) would print floor ≈ 0.050 — the slack seat certifies the same survival but prints a vastly weaker guarantee; "print the floor" cuts both ways. (c) The wraparound pair is A₁₀₀'s second neighbor: d counts *distinct* neighbors, the cycle is 2-regular, wrap or not. (d) Inclusion–exclusion over the three events of the 3-dice circle: P(∪A_i) = 3·(6/216) − 3·(1/216) + 1/216 = 16/216, so survival = 200/216 = 0.9259 — against the slack-seat floor (2/3)³ ≈ 0.296. The floor is honest, not tight: it prices the seat, not the truth.

**Answer 5 (pricing the second star).** (a) Σp = 1/32 + 10·(1/8) = 1.28125 > 1. (b) The hub meets all ten satellites (D = 10 for the hub; each satellite meets only the hub): e·p_max·(D+1) = e·(1/8)·11 = 3.74 > 1. (c) Jacobi from zero: x_c = (1/32)/(1−x_s)¹⁰, x_s = (1/8)/(1−x_c) converges to **x_c = 0.1549, x_s = 0.1479**, both < 1 — the certificate holds and the instance is satisfiable. Machine-checked extras: Σx = x_c + 10·x_s = **1.634**; the general-form floor ∏(1−x_i) = (1−x_c)(1−x_s)¹⁰ = **0.1705**; the tight Moser–Tardos Theorem 1.2 bound Σ x_i/(1−x_i) = 0.1549/0.8451 + 10·(0.1479/0.8521) = **1.919**, and the coarse probability-ratio meter Σ x_i/p_i = x_c·32 + 10·x_s·8 = **16.79**. (d) Σx = 1.634 is *not* the runtime bound — Exercise 8's bounds are Σx_i/(1−x_i) and Σx_i/p_i, and independent events already break the Σx reading (x = p there, while the true expected cost is p/(1−p) = x/(1−x) > p). Ten leanings is past the width-4 hub's capacity (Exploration 16: s = 9 diverges) — the width-5 hub absorbs what the width-4 one cannot, and the two-seat bargain is where that capacity is priced.

**Answer 6 (counting the witness trees).** (a) One event, p = 1/8: every resampling is a fresh independent trial, so the count is geometric — E = p + p² + … = p/(1−p) = 1/7 = 0.1429, exact. (b) Two clauses sharing one variable: because {A, B} is a single shared-variable clique, every earlier step in the backward scan is compatible with the deepest leaf, making every witness tree a unary chain; in the neighbor-alternating witness family rooted at clause 1, the chains are A, AB, ABA, ABAB, …, one per size k, each carrying weight p^k. The sum: Σ_{k≥1} p^k = 0.1429, an upper bound on E[resamplings of A] by the witness-tree lemma. (c) The lab's coarse meter at the same seat is x/p = 0.146447/0.125 = 1.1716 (and the tight Theorem 1.2 bound is x/(1−x) = 3−2√2 = 0.1716) — the chain sum is 8.2× tighter than x/p on this instance (1.1716/0.1429 ≈ 8.2). (d) Part 2a's 40 five-clause instances averaged 0.65 total resamplings ≈ 0.13 per clause — comfortably inside 0.1429 per clause, and far inside the coarse meter's 1.17. The tree sum still overestimates *even for the easiest process*: it prices every consistent genealogy at p per node, while a single run realizes exactly one genealogy — the bound totals the whole forest of possible histories, the run walks one path.

**Answer 7 (the Shearer identity on the path).** Base: μ(P₀, 1/4) = 1 = 2/2¹ and μ(P₁, 1/4) = 1 − 1/4 = 3/4 = 3/2². Step: with μ(P_{m−1}) = (m+1)/2^m and μ(P_{m−2}) = m/2^{m−1}, the recursion gives μ(P_m) = (m+1)/2^m − (1/4)·m/2^{m−1} = (2(m+1) − m)/2^{m+1} = **(m+2)/2^{m+1}**. Checks against the lab (Part 5A prints all three): m = 8: 10/512 = 0.01953; m = 16: 18/131072 = 0.000137; m = 32: 34/2³³ = 3.96·10⁻⁹ — positive for every finite m, so the finite paths sit marginally inside Shearer's region at exactly p = 1/4, and the wall is the m → ∞ limit. (This is P4's cameo: a two-line induction on a recursion — the monovariant habit, applied to a boundary.)

**Answer 8 (reading the meter).** (a) By linearity of expectation, E[total] = Σᵢ E[resᵢ] ≤ Σᵢ xᵢ/(1−xᵢ), and whenever 1−xᵢ ≥ pᵢ (i.e. xᵢ ≤ 1−pᵢ) each term is bounded above by xᵢ/pᵢ. (b) Degrees 0 or 1 at p = 1/8 = 0.125: we have x₀ = 0.125 and x₁ = (1−√(1/2))/2 = 0.146447, so the coarse per-instance bound Σᵢ xᵢ/pᵢ is (#D=0)·(0.125/0.125) + (#D=1)·(0.146447/0.125) = #D0 + 1.17157·#D1; the panel's 40 instances give **mean 5.592** (receipt) — and the tight Theorem 1.2 bound Σᵢ xᵢ/(1−xᵢ) = (1/7)·#D0 + 0.17157·#D1 gives **mean 0.8134** — against the measured mean 0.65. (c) The gap: the theorem's bound is worst-case over *all* distributions sharing this dependency graph — the events could be coupled adversarially within the graph's permission — while the lab samples the product measure, the easiest distribution, where violations are near-independent and repair is cheap. An expectation statement is only as good as the distribution it prices: P10's cameo, the same caveat Part 5B prints at the fence.

**Answer 9 (the exact ceiling for 5-uniform coloring).** (a) p = 2^{1−5} = 1/16: e·(1/16)·(D+1) ≤ 1 ⟺ D+1 ≤ 16/e ≈ 5.887 ⟺ D ≤ 4. (b) The uniform-x ceiling: max x(1−x)^D at x = 1/(D+1) is D^D/(D+1)^{D+1}; at D = 5: 5⁵/6⁶ = 0.0670 ≥ 0.0625 ✓; at D = 6: 6⁶/7⁷ = 0.0567 < 0.0625 ✗ — the exact ceiling is D = 5. (c) The general form certifies one degree more than the symmetric form, free. No asymmetric assignment rescues a 6-regular (or minimum-degree ≥ 6) dependency graph at p = 1/16: in any valid assignment x₁,…,x_m ∈ (0,1), choose an event i* attaining the minimum seat value x_{i*} = min_i x_i. Since every neighbor j ∈ Γ(i*) has x_j ≥ x_{i*}, we have 1−x_j ≤ 1−x_{i*}, and therefore the certificate inequality at seat i* forces 1/16 = p ≤ x_{i*}·∏_{j∈Γ(i*)}(1−x_j) ≤ x_{i*}(1−x_{i*})^{d(i*)} ≤ x_{i*}(1−x_{i*})⁶ ≤ 6⁶/7⁷ = 46656/823543 ≈ 0.05665 < 0.0625, a contradiction. Thus the uniform test is exact for regular uniform instances, and it says no. (The event-graph translation — bad event per edge, p = 2^{1−k}, Γ = vertex-sharing — is the P25 cameo.)

**Answer 10 (the neighbor's tax, in numbers).** (a) P(A₁∧A₂) = (720 − 426 − 426 + 240)/720 = 108/720 = 0.15. (b) P(A₁ | Ā₂) = (P(A₁) − P(A₁∧A₂))/(1 − P(A₂)) = (0.40833 − 0.15)/0.59167 = 0.4366 > P(A₁) = 0.40833. (c) Conditioning on the neighbor's survival makes failure *more* likely — the lopsided hypothesis (the conditional over a declined edge must not exceed p_i) fails across this edge, so the graph must draw it and the certificate must pay for it. (d) Panel (a), ab = 265: P(A₁∧A₂) = 133/720 = 0.18472, and P(A₁ | Ā₂) = (0.40833 − 0.18472)/0.59167 = 0.3779 < 0.40833 — the conditional *drops* below the unconditional, exactly what a declined edge promises (machine receipts, both panels). Lecture 4's two-event equivalence turns each of these into one subtraction; the covariance gaps +0.01799 / −0.01674 are the same two statements in miss-count dress.

**Answer 11 (certificates are incomparable, and the graph is a claim).** (a) *Union wins:* A₁ = A₂ with p = 0.49. Union: Σp = 0.98 < 1 — survival ≥ 0.02 (truth: 0.51). The lemma in every form: the event is its own neighbor; symmetric e·0.49·2 = 2.66 > 1; general (and asymmetric — the two seats bargain over the same event) needs x₁(1−x₂) ≥ 0.49 and x₂(1−x₁) ≥ 0.49; multiplying, x₁(1−x₁)·x₂(1−x₂) ≥ 0.49² = 0.2401 — but each factor is ≤ 1/4, so the product is ≤ 1/16 < 0.2401. Impossible: no seats exist. (b) *Lemma wins:* the 100-dice circle, where the union ledger reads 100/36 = 2.78 and the local lemma certifies with room (Exercise 4). (c) *Choosing Γ is an act:* the honest cycle graph gives d = 2 and e·0.1·3 = 0.8155 ≤ 1 — certified. The lazy graph, all pairs within distance 2 (defensible only if you cannot prove the missing independence), gives d = 4 and e·0.1·5 = 1.359 > 1 — destroyed. Every edge you cannot justify is a tax; Part 4's −0.01674 is what an unearned discount costs in the permutation world.

**Answer 12 (the 4/27 window on the line).** (a) d = 2: the uniform seat x = 1/3 has x(1−x)² = 4/27, so the certificate reads p ≤ 4/27 (Exercise 3's maximization at d = 2). (b) 4/27 against 1/(3e): the ratio is (4/27)·3e = 12e/27 ≈ 1.208 — the window is 21% wider. (c) In the lab's ladder (p = q²): q ≤ √(4/27) = 0.3849 against the symmetric q ≤ √(1/(3e)) = 0.3502 — and both still short of Shearer's q = 1/2 (Part 5A prints the whole ladder). (d) The general form does not replace the symmetric form because it demands more of you: the dependency graph's degree structure and, in the worst case, a seat-finding computation (a fixed point — Part 6's Jacobi loop). The symmetric form is one glance at two numbers. Diagnosis before algebra: the Trick Bag's triage row exists because the forms are incomparable and the price of the stronger one is real.

**Answer ◆13 (some outcome avoids every adjacent pair of sixes).** The events A_i = "dice i, i+1 both show six" have p = 1/36 and each meets only its two cyclic neighbors: d = 2. The symmetric local lemma applies in one glance — e·(1/36)·3 = 0.2265 ≤ 1 — so Pr[no bad event] > 0 and some outcome avoids all hundred. The union bound refuses (100/36 = 2.78 > 1); the general form certifies too and prints the floor (2/3)¹⁰⁰ (Exercise 4). The tool was P45 — the local lemma — against a global ledger too big for P13.

**Answer ◆14 (a hundred rare events, sparsely entangled).** p = 0.03, each event independent of all but four others: d = 4, and e·0.03·5 = 0.4077 ≤ 1 — the symmetric lemma certifies that some point avoids all hundred. The union bound's ledger reads 3 > 1 and refuses. Diagnosis: P45 again — many rare events, sparse overlap; the same shape as the k-SAT census, where the degree certificate fires precisely where the total dies.

**Answer ◆15 (three edges, two colors).** Color the vertices uniformly at random: each edge is monochromatic with p = 2^{1−3} = 1/4, so Σp = 3/4 < 1 — the *union bound* certifies survival: some coloring has no monochromatic edge, and every 3-uniform hypergraph with at most 3 edges is 2-colorable. The local lemma cannot take this instance: with ≤ 3 edges d ≤ 2, and e·(1/4)·3 = 2.04 > 1; the general form needs x(1−x)² ≥ 1/4 > 4/27 — impossible; asymmetric seats fail the same product test as Exercise 11(a) (each seat's budget is capped by x(1−x)^D ≤ 4/27 < 1/4 at D = 2). Diagnosis: P13, not P45 — three bad events make the global ledger small enough to pay in full, and Lecture 1's incomparability (the union bound's *total* vs. the lemma's *degree*) is the whole lesson. The local lemma earns its keep only when the total is too big — which is exactly the regime its certificate is shaped for.

## Revision History & Verification Notes

**Machine-verification campaign (before a line of prose was installed).** Six recorded lab parts, every quantitative claim in this chapter traceable to one. The campaign ran in two passes: a first receipts pass, then a verification pass that caught two numerical errors and two unreproducible panels — the receipts were rewritten as canonical v2, and the affected panels re-run with the printed code as the canonical procedure. A final printed-code reproduction pass re-implemented every panel from the documented draw rules and re-verified each receipt value-for-value before the lab was printed; the engine is the Lehmer/MINSTD generator x ← 48271·x mod (2³¹−1), one continuous stream A (seed 20261083) through Parts 1a → 2a → 2b → 3a, fresh engines at 20261084–20261088, deterministic panels in Part 5A and Part 6's certificate half, and Exploration 18's check run at 20261089. The printed Python above reproduces every table bit-for-bit.

1. **The k-SAT censuses (Part 1).** n = 12: meanD 1.62, 2.43, 3.31, 4.15, 4.94, 5.84, 6.52, 7.42 across m = 3..10; certificate (D ≤ 1) fires 36, 8, then 0; 800/800 instances brute-checked, zero certificate-truth conflicts; the union bound out-certifies at m ≤ 7 — incomparability, machine-recorded. n = 48: 2.37/13, 3.23/2, 3.84/0 with the union bound dead at every m — the lemma's payoff slice.
2. **Moser–Tardos, certified vs. entangled (Part 2).** 554 rejection tries for 40 certified instances; rounds mean 0.65, max 4, 40/40 terminated; the coarse meter (Σ x_i/p_i) averages 5.592, the tight Theorem 1.2 bound (Σ x_i/(1−x_i)) averages 0.8134, the survival floor 0.4709. Control: 31 tries for 30 satisfiable-but-uncertified instances (brute-SAT ∧ D ≥ 5); rounds mean 2.23, max 10, 30/30 terminated — the algorithm patrols beyond its fence at ~3.4× the cost.
3. **The hypergraph censuses (Part 3).** v = 14, k = 4: 700/700 brute-colorable; certificates nearly silent (sym 1, gen 16 at m = 4, then 0) — the corrected certificate after the p-slip (below). v = 70: meanD 5.82/6.73, every sound certificate silent — an honest negative, printed as run.
4. **Lopsidedness, exact enumeration (Part 4).** Non-neighbors: 426/426/265, gap +0.01799, 6/6 positive; column-sharing neighbors: ab = 240, gap −0.01674, 6/6 negative — the declined edge's promise measured on one side of the neighbor relation and broken on the other; n = 8 panel: 24024/24024/14833, gap +0.01286. The derangement cameo: ab = D₆ and D₈.
5. **The three floors and the fence (Part 5).** 5A: the full 12-row ladder (certificate floor, Shearer floor, exact truth) at q ∈ {1/3, 2/5, 9/20, 1/2} × m ∈ {8, 16, 32}, with the identity μ(P_m, 1/4) = (m+2)/2^{m+1} machine-checked at 10/512, 18/131072, 34/2³³. 5B: all ten runtime cells reproduce (medians 2–14, no caps at 50,000) — the process stays easy beyond Shearer's boundary, and the Kolipaka–Szegedy caveat is printed with it.
6. **The star (Part 6).** Union 1.0625 fails; symmetric 3.0581 fails; the asymmetric fixed point x_c = 0.3064, x_s = 0.1802, Σx = 1.748 certifies; brute force 373,729/1,048,576 = 35.64%; MT 20/20 terminated, mean 1.10, max 4. Exploration check runs: the second star (0.1549/0.1479, Σx 1.634, floor 0.1705, meter 16.79), the hub capacity (s = 8 certifies, s = 9 diverges), the near-wall floors (μ = 1.399·10⁻⁷ vs. truth 1.428·10⁻³), and the beyond-the-wall run (q = 9/10: median 45, mean 46.9, max 94, no caps).

**The scars, kept on display.** (i) *The p-slip (Part 3, corrected):* the first receipts recorded "cert = D ≤ 4 (p = 2^{1−4} = 1/16)" — an arithmetic slip; for k = 4 the monochromatic-edge probability is p = 2^{1−k} = 1/8, so the sound symmetric certificate is D ≤ 1 and the sound uniform-general certificate is D ≤ 2 (D ≤ 2 is also the exact asymmetric criterion: x(1−x)³ ≤ 27/256 < 1/8). Part 3b's stream was verified bit-for-bit and its certificates recomputed on the same instances (0/0 both; the v1 "D ≤ 4" column 13/1 is kept as the fossil), and Part 3a was re-run on the corrected stream. The hypergraph "LLL-beats-union" slice was retired honestly — the k-SAT panel 1b carries that story with a sound certificate. (ii) *The one-index slip (Part 5A, corrected):* the first truth column was computed over m bits (m − 1 events) while the floors use the m-event convention; the truth was recomputed over m+1 bits, consistent with the floors and the Exercise 7 identity. (iii) *The unreproducible rounds lists (Parts 2 and 6-MT, re-run):* the first pass's rounds lists could not be reproduced from the documented engine by any reconstruction tried (offset scans, generation variants, pick/init/resample variants); both panels were re-run with clean code as canonical. The reproduction pass then pinned the Part 6 difference precisely: the canonical list follows the all-ones violated reading (the star's clauses stored with sign bit 0), and the earlier list was the all-zeros reading of the same star on the same seed — a pure color convention, distributionally identical, both 20/20 terminated (means 1.10 vs. 1.00); the printed lab uses the canonical all-ones reading. (iv) *The meter mis-attribution (corrected twice, honestly):* the first pass compared the sample mean to Σx_i, but Moser–Tardos's Theorem 1.2 bounds E[resamplings of A_i] by x_i/(1−x_i) — bounded above by x_i/p_i whenever x_i ≤ 1−p_i — and independent events already break the Σx reading (x = p, true cost p/(1−p) = x/(1−x) > p). The chapter prices the meter correctly everywhere. The first expansion pass (session 112) then caught the session-83 citation itself: the meter had been attributed to "Theorem 1.3", whose actual content is the parallel algorithm — the sequential bound is Theorem 1.2, web-verified against the paper's numbering (arXiv 0903.0544 = J. ACM 57(2), Article 11). (v) *The design iterations, honestly:* v = 50 → v = 70 in Part 3b (the certificate regions did not overlap at the smaller size); Part 4's first design placed both boards on the shared diagonal — every pair was a *neighbor*, which taught the wrong lesson; the v2 panels contrast non-neighbors against column-sharing neighbors, and the iteration itself became the teaching point; Part 5's runtime-transition design was retired (this line process stays easy beyond Shearer — no transition to find at these sizes) and replaced by the three-floors panel plus the honest runtime panel; Part 6's single-run MT receipt (rounds = 0 — 35.6% of assignments already satisfy) was replaced by the 20-trial distribution. (vi) *One author-level slip, caught at assembly:* Exercise 2's first draft bounded the clause count by m ≤ 4n — the incidences are 4n but each clause consumes ten of them, so the honest bound is m ≤ 2n/5; the hint is repaired in place. (vii) *The engine rules are part of the receipts:* every draw is integer-exact, one draw per Fisher–Yates index, sign bits strictly after the variable draws, and the resampling panels pick the lowest-index violated event and resample in listed order — the reproduction pass confirmed that the printed tables demand exactly these rules and no others that were tried.

**Canon pins (web-verified before authoring, 2026-10-14).** Erdős–Lovász 1975, *Problems and results on 3-chromatic hypergraphs and some related questions*, in Hajnal–Radó–Sós (eds.), Infinite and Finite Sets, Vol. II, pp. 609–627, Colloq. Math. Soc. János Bolyai 10, North-Holland — pinned via three independent web sources. Spencer 1977, Discrete Math. 20:69–76 — pinned. Shearer 1985, *On a problem of Spencer*, Combinatorica 5(3):241–245, DOI 10.1007/BF02579368 — pinned. Erdős–Spencer 1991, Discrete Appl. Math. 28 — volume pinned; **pages not web-verified this session, recorded honestly**. Moser–Tardos 2010, J. ACM 57(2), Article 11, DOI 10.1145/1667053.1667060 — pinned; the algorithmic Theorem 1.2 form E[resamplings of A_i] ≤ x_i/(1−x_i) web-verified against the paper's theorem numbering at session 112 (the earlier "Theorem 1.3" attribution — the parallel version — was wrong, corrected in the expansion pass). Molloy 2019, *The list chromatic number of graphs with small clique number*, JCTB 134:264–284, arXiv:1701.09133 — pinned; every triangle-free graph of max degree Δ has list chromatic number at most (1+o(1))Δ/ln Δ. Johansson's DIMACS Tech. Report 91-5 was never journal-published; the LLL step lives on in the Molloy–Reed expositions — recorded honestly, no pin claimed. Flag level, not web-verified: Beck 1991 (Random Structures & Algorithms 2(4):343–358, from the standard literature), Kolipaka–Szegedy 2011 (the efficiency theorem), Lu–Székely (random-injection lopsidedness). Alon–Spencer, *The Probabilistic Method*, Chapter 5 — book level, the home of the Case B bookkeeping and the uniform-seat averaging argument.

**The honest ledger.** Proved in the text: the symmetric and general forms' complete nested-induction proof — Case A and Case B both (Lecture 2) — and the derivation of the optimal symmetric bound d^d/(d+1)^{d+1} (Exercise 3); the k-SAT and hypergraph certificates with their exact ceilings, including the minimum-seat argument that closes the degree-3 and degree-6 cases (Lecture 3, Exercises 2, 9); the complete lopsided substitution proof, the two-event lopsidedness equivalence and its measurement (Lecture 4, Exercise 10, Part 4); the witness-tree proof of Moser–Tardos — the τ_t construction, Lemmas 1 and 2, and the Galton–Watson Lemma 3 with its parent-charged slot accounting — with the single-event and two-clause cases computed exactly (Lecture 5, Exercise 6); the Shearer identity on the path (Exercise 7); the certificate incomparability constructions (Exercise 11); the union-bound coloring argument for three edges (Exercise ◆15). Stated with proof cited, not given — the chapter's flagged sketches, each with its missing steps named: the Latin transversal theorem (Erdős–Spencer 1991), and Johansson's theorem as used (via Molloy–Reed's exposition; Molloy 2019's triangle-free statement is the pinned descendant). Computed, not proved: every census, enumeration, fixed point, and simulation in the lab — reproducible value-for-value from the documented engine. The pattern P45 (the local lemma) finds its home in this chapter; its registry pin is filed at ship. The chapter itself was commissioned by the survey record's open question — one entry or a P13 strengthening? — resolved at user direction: P45, its own pattern.

**Expansion pass (session 112, the first for this chapter).** The user flagged a possible mangling of pattern references; the audit compared the master's map, Trick Bag, and in-text P-tokens against the draft's and returned **NOT MANGLED** — the same seven-ID set in both files, every delta accounted for by the appendix (an honest negative; the campaign's one genuine mangling remains Chapter 18's, session 111). One convention repair landed anyway: the Trick Bag's triage row cited a bare "45" where every other site says P45. Master defects found and fixed: the Lecture 3 degree-3 overclaim ("no asymmetric assignment can certify a degree-3 edge" is false on K_{1,3} — seats x_hub = 0.34, x_leaf = 0.19, machine-checked — replaced by the complete minimum-seat argument with its regular-graph scope, and the same technique now closes Answer 9's degree-6 case, retiring its cited averaging argument); the P10 map row's wrong "E[resamplings of A_i] ≤ x_i"; the meter mis-attribution's theorem number and form (Theorem 1.3 → 1.2, tight x_i/(1−x_i) with x_i/p_i as its coarse corollary); ◐17's "three orders" (the gap is four orders); the shared 0.12261 typo for 1/(3e) = 0.12263 (two sites); and the missing engine guards (draw_clause k-range, degrees m = 0, line_mt m/trials) plus the small_root bracket [0, 0.5] → [0, 1/3] (output-neutral, verified). Draft adoptions: the complete nested-induction proof of the general form (the chapter's one flagged proof sketch, now proved); the complete lopsided substitution proof; the complete witness-tree machinery — the τ_t construction, Lemmas 1 and 2, and the Galton–Watson Lemma 3; two figures (the K_{1,8} star ledger; the threshold ladder with a same-label witness-tree edge); the tight-meter receipts (mean 0.8134; anchors x₁/(1−x₁) = 3−2√2 and x₀/(1−x₀) = 1/7) across Lecture 5, Part 2, Exercises 5–8 and their answers; ◐18's check-run seed; and the practice menu's "regular graphs" precision. Three draft defects caught and **not** installed as printed: Lemma 3's first displayed form double-charges at self-spawning vertices (the unconditional (1−x_ℓ) factor is wrong exactly there — on the check instance, 0.10368 against the true 0.12960; the parent-charged slot accounting replaces it); the draft's theorem number "Theorem 1.1" for the meter (right form, wrong number — 1.1 is the LLL statement itself); and the draft's kept 0.12261. Battery: all six lab parts re-run from the printed code as installed — every receipt reproduced bit-for-bit, including the new tight-tracker output; every new printed constant verified numerically. Checker scars, recorded honestly: one battery run inverted the violated predicate (the all-true reading — distributionally identical statistics, caught by the rounds-list receipt mismatch 389 vs. 554 tries, fixed and re-run); the session's first triage asserted "Theorem 1.1" from memory without a web check — wrong, as corrected above; and one triage note claimed the Part 6 fence lacked `import math` — it was wrong, the fence already had it.

---

**Status:** 🟩 Feynman edition — installed (session 83, chunks 83a–83b: session open and survey-evidence capture; receipts verification campaign with the v2 rewrite; printed-code reproduction pass; authoring, assembly, install); first expansion pass installed (session 112). The web edition `cgt-ch19-web` was built at session 83 and rebaked at 112. No claim in this chapter predates its receipt.
