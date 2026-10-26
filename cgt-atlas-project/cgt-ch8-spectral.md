---
name: "cgt-ch8-spectral"
title: "Ch. 8 — Spectral Methods and the Modern Toolkit: A Lecture Course in the Feynman Style"
type: "text/markdown"
---

# Chapter 8 · Spectral Methods and the Modern Toolkit

*Part of the Combinatorics & Graph Theory Atlas (see the Atlas canvas for the chapter map and progress report).*

The spectrum of a graph knows its extremal answers before the witnesses are found: the largest eigenvalue averages the edges and caps them by the clique number, dimension-priced polynomials cap a point configuration's distances, and the smallest eigenvalue — read through interlacing, semidefinite duality, and linear programming — prices independence, chromatic number, zero-error capacity, and code size. This edition is a lecture course in four lectures: eigenvalues as averaging machines (Mantel proved a fourth way, and the expander-mixing lemma in its sharp form), Motzkin–Straus and spectral Turán (the clique polynomial, and Turán's theorem arriving by way of optimization), two-distance sets (a capstone that weaves together every pattern in the course), and the modern toolkit — interlacing, the Hoffman bounds, Lovász theta with θ(C₅) = √5 and Θ(C₅) = √5, and Delsarte's linear program with hand-checkable Krawtchouk certificates. Chapter 6 built the vector-and-dimension machine and closed exactly where this chapter opens; every proof here is complete or honestly cited, every claimed number is machine-checked, and the figures are drawn from verified data.

## How to read this chapter

**Notation.** G = (V, E) is a graph on n vertices with m edges; A is its adjacency matrix with eigenvalues λ1 ≥ … ≥ λn, and d-regular means every degree d. μ = max(|λ2|, |λn|) is the second-eigenvalue constant of the mixing lemma. J is the all-ones matrix, I the identity, 𝟙 the all-ones vector, 𝟙⊥ the zero-sum hyperplane; xᵀ is the transpose and ||x|| the Euclidean norm. ω, α, χ are the clique, independence, and chromatic numbers; Ḡ is the complement; A_S the principal submatrix on S; M ⪰ 0 means positive semidefinite, and ⟨x, y⟩_M = xᵀMy. For the geometry lecture: points live in R^d, D is the set of realized pairwise distances, m(d) the maximum size of a two-distance set in R^d. For the coding section: A(n, d) is the largest binary code of length n with minimum distance d, and K_k(i) the Krawtchouk polynomial. C(a, b) is the binomial coefficient. Letters are re-stated locally where a lecture needs its own.

**The exercises are graded:** ●○○ *easy* (a direct application of one lecture idea), ●●○ *moderate* (two ideas, or one tricky step), ●●● *tough* (several chapter ideas combined). Hints travel with the problems; worked answers sit at the very end of the chapter. Try honestly before reading a hint. Beyond the graded set, ◆ **pattern-unknown** problems name no method and carry no hint: diagnosing which tool fits is part of the problem. And ◐ **Explorations** at the end are open-ended investigations with no single right answer — research training, not test preparation.

## The pattern table for this chapter

| Pattern | Plain language | Where you meet it |
|---------|---------------|-------------------|
| **P21 Spectral / Rayleigh** | Eigenvalues as averaging devices: the Rayleigh lower bound from the average, structure upper bounds, and the operator norm on 𝟙⊥ | L1, L2, L4 |
| **P20 Weight shifting / symmetrization** | Move weight toward the extremal configuration without losing the objective | L2 |
| **P19 Rank / dimension** | Build a matrix whose rank you can bound two ways; dimension is a counting bound in disguise | L3 |
| **P22 Polynomial method** | One polynomial per point, vanishing on all the others; the dimension of a polynomial space caps the configuration | L3, L4 |
| **Compress before you bound (lore)** | Restrict the matrix to a subspace or partition first: interlacing makes every such restriction honest | L4 |
| **Distribute, then average (lore)** | Sum a quantity over all pairs before bounding it: character sums come out as squares | L4 |

---

## Lecture 1 · Eigenvalues as Averaging Machines: Mantel, and the Expander-Mixing Lemma

Henceforth G has n vertices, m edges, adjacency matrix A with eigenvalues λ1 ≥ … ≥ λn. Because A is real symmetric and entrywise nonnegative, Perron–Frobenius applied to the connected components gives λ1 = max_i |λi| ≥ 0, with an entrywise nonnegative unit eigenvector x ≥ 0 — every lemma below only needs that.

### 1.1 The two-lemma sandwich (P21)

**Lemma 1 (Rayleigh = averaging).** λ1 ≥ 2m/n.
*Proof.* λ1 = max_{||x||=1} xᵀAx ≥ (𝟙/√n)ᵀA(𝟙/√n) = (Σ_v d(v))/n = 2m/n. ∎

**Lemma 2 (triangle-free ⇒ λ1 ≤ √m).**
*Proof.* Let x be a unit eigenvector for λ1 (||x|| = 1). For each vertex u: λ1x_u = Σ_{v~u} x_v, so by Cauchy–Schwarz λ1²x_u² ≤ d(u) Σ_{v~u} x_v². Sum over u:
λ1² ≤ Σ_u d(u) Σ_{v~u} x_v² = Σ_v x_v² · (Σ_{u~v} d(u)) ≤ max_v e(N(v)),
where e(N(v)) = Σ_{u~v} d(u) counts, with multiplicity, the edges incident to the neighborhood of v. Triangle-free ⇒ N(v) is independent ⇒ every edge has at most one endpoint in N(v) ⇒ e(N(v)) ≤ m. Hence λ1² ≤ m. ∎

**Mantel, spectrally.** (2m/n)² ≤ λ1² ≤ m ⟹ 4m² ≤ mn² ⟹ **m ≤ n²/4** — and integrality gives m ≤ ⌊n²/4⌋, the fourth proof of Chapter 3's §3.4. ∎

**Equality, and the extremal graph found twice.** For K_{a,b}: λ1 = √(ab) (Exercise 1 — eigenvector √b on one side, √a on the other) and m = ab, so Lemma 2 is tight for *every* complete bipartite graph; Lemma 1 is tight only when a = b, since 2ab/(a+b) = √(ab) ⟺ (a−b)² = 0. The sandwich *finds* the unique even-n extremal graph K_{n/2,n/2} directly, and for odd n integrality m ≤ ⌊n²/4⌋ = ⌊n/2⌋⌈n/2⌉ pins the balanced K_{⌊n/2⌋,⌈n/2⌉}. Machine check: on every triangle-free graph on 5 or 6 vertices (full census), both lemmas and m ≤ ⌊n²/4⌋ hold; the two-lemma sandwich is a theorem about all of them, not a lucky example.

### 1.2 The expander-mixing lemma — pseudorandomness, quantified

**Problem.** G is d-regular on n vertices, μ = max(|λ2|, |λn|). Show that for all disjoint S, T ⊆ V:

| e(S,T) − d·|S||T|/n | ≤ μ · √( |S||T| (1 − |S|/n)(1 − |T|/n) ).

("A graph with small μ behaves randomly: every two large vertex sets carry about the expected number of edges between them.")

*Proof.* Decompose against the all-ones vector: 1_S = (|S|/n)𝟙 + z_S with z_S ⊥ 𝟙, so ||z_S||² = |S| − |S|²/n = |S|(1 − |S|/n) — and likewise for T. Count edges through the adjacency matrix: e(S,T) = 1_SᵀA1_T = (|S||T|/n²)·𝟙ᵀA𝟙 + z_SᵀAz_T, the two cross terms vanishing because A𝟙 = d𝟙 and z ⊥ 𝟙. Now A𝟙: 𝟙ᵀA𝟙 = dn, so the first term is exactly d|S||T|/n. On 𝟙⊥ the symmetric matrix A has eigenvalues λ2, …, λn, so its operator norm there is μ: |z_SᵀAz_T| ≤ μ||z_S||·||z_T||. Combine. ∎

The √(1 − |S|/n)(1 − |T|/n) factors are the sharp form of the classical statement (which reads ≤ μ√|S||T|); they matter exactly when S or T is a large fraction of V.

**Tightness, machine-checked over all disjoint pairs.** On the Petersen graph (d = 3, spectrum {3, 1⁵, −2⁴}, μ = 2) the ratio of violation to bound attains μ exactly — the lemma cannot be improved there. On K_{3,3} the eigenvalue −d = −3 is present, so μ = 3 and the bound is again tight — the bipartite degeneracy: any connected d-regular bipartite graph carries −d, and the lemma degenerates with it. On C₅ the largest ratio is 4/3, short of μ = φ ≈ 1.618: some instances are rigid, some have slack. (Jacobi eigenvalues and maximum mixing ratios for all three: computed and validated in the lab, Part 1.)

**What these names buy.** (1) Quasi-randomness (Chung–Graham–Wilson): several "looks random" properties are equivalent to μ = o(n). (2) Expanders: the spectral gap d − λ2 measures connectivity strong enough to power derandomization, codes, and communication complexity. (3) Discrepancy control: with μ small, no two large vertex sets are unusually tightly connected — a deterministic randomness statement. The two-lemma sandwich of §1.1 — Rayleigh lower bound from the average, upper bound from local structure — is the template of spectral extremal graph theory.

---

## Lecture 2 · Motzkin–Straus: The Clique Polynomial, and Spectral Turán

Both lemmas of Lecture 1 bound λ1 on triangle-free graphs. Capping λ1 in terms of the clique number is a general game — and its engine, the Motzkin–Straus theorem, is a pure optimization statement with a beautiful weight-shifting proof (P20).

### 2.1 The Motzkin–Straus theorem

**Theorem.** For a graph G with clique number ω, max over the simplex Σx_v = 1, x ≥ 0 of

f(x) = Σ_{uv ∈ E} x_u x_v

is exactly **(1 − 1/ω)/2**.

*Proof.* The value (1−1/ω)/2 is attained: put weight 1/ω on each vertex of a maximum clique — f = C(ω,2)/ω² = (1 − 1/ω)/2.

For the upper bound, take a maximizer x with **smallest possible support**, and suppose the support contains two non-adjacent vertices u ≁ v. Write d_x(w) = Σ_{z~w} x_z. Merge v into u: x'_u = x_u + x_v, x'_v = 0, all else unchanged. Only edges at u and v change, and (u ≁ v, so the pair itself contributes nothing) the change is

f(x') − f(x) = x_v ( d_x(u) − d_x(v) ).

If d_x(u) ≥ d_x(v), merge v into u; otherwise merge u into v (same formula, roles swapped). Either way f does not decrease, x' is still a maximizer — and its support is strictly smaller. Contradiction to the minimal-support choice. So the support of x is a **clique** — every pair of support vertices adjacent.

On a clique of size t, f(x) = Σ_{i<j} x_i x_j = ((Σx_i)² − Σx_i²)/2 = (1 − Σx_i²)/2 ≤ (1 − 1/t)/2 by Cauchy–Schwarz on the support, with t ≤ ω. ∎

Note what the merge lemma really says: *weight should live on tightly connected vertices* — shifting a small vertex's weight to a better-connected non-neighbor never hurts. That is P20 in its purest form.

For the record, the merge formula has an honest general form: if u ~ v (adjacent merge), the lost edge uv adds a correction — f(x') − f(x) = x_v(d_x(u) − d_x(v)) − x_v² — used in Figure 1's first move.

### 2.2 The merge, drawn: the paw graph

The paw (triangle a, b, c plus pendant d on a) has ω = 3, so the theorem promises max f = 1/3. The merge walk from the uniform point, with all arithmetic done:

start x⁰ = (1/4, 1/4, 1/4, 1/4): f = 4 edges · 1/16 = **1/4**. Weighted degrees: d_x(a) = 3/4, d_x(d) = 1/4. Merge d into a (adjacent merge — pay the x_v² correction): change = (1/4)(3/4 − 1/4) − 1/16 = 1/16, so x¹ = (1/2, 1/4, 1/4, 0) and f = **5/16**. The support {a, b, c} is now a clique; f depends only on the weights there, f = (1 − Σx_i²)/2, maximized at the uniform point: x² = (1/3, 1/3, 1/3, 0), f = **1/3** = (1 − 1/ω)/2. ∎

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 880 340" font-family="system-ui, -apple-system, 'Segoe UI', sans-serif">
  <rect x="0" y="0" width="880" height="340" fill="#ffffff"/>
  <text x="40" y="32" font-size="17" font-weight="700" fill="#193e5c">Figure 1 &#183; Motzkin&#8211;Straus on the paw: 1/4 &#8594; 5/16 &#8594; 1/3, two moves (Lecture 2)</text>

  <!-- Panel 1: Start -->
  <text x="35" y="62" font-size="13" fill="#172333" font-weight="600">start: x = (1/4, 1/4, 1/4, 1/4), f = 1/4</text>
  <path d="M 268 106 Q 220 72 172 106" fill="none" stroke="#dc2626" stroke-width="2.2" stroke-dasharray="6 4"/>
  <polygon points="172,106 181,103 177,96" fill="#dc2626"/>
  <text x="220" y="82" font-size="12" fill="#dc2626" text-anchor="middle">merge d into a</text>
  <g stroke="#2563eb" stroke-width="3">
    <line x1="120" y1="190" x2="200" y2="190"/>
    <line x1="120" y1="190" x2="160" y2="125"/>
    <line x1="200" y1="190" x2="160" y2="125"/>
    <line x1="160" y1="125" x2="270" y2="125"/>
  </g>
  <circle cx="160" cy="125" r="13" fill="#dbeafe" stroke="#2563eb" stroke-width="2.5"/>
  <text x="142" y="112" font-size="13" font-weight="700" fill="#172333" text-anchor="end">a</text>
  <text x="160" y="154" font-size="12" fill="#64748b" text-anchor="middle">1/4</text>
  <circle cx="120" cy="190" r="13" fill="#dbeafe" stroke="#2563eb" stroke-width="2.5"/>
  <text x="100" y="195" font-size="13" font-weight="700" fill="#172333" text-anchor="end">b</text>
  <text x="120" y="216" font-size="12" fill="#64748b" text-anchor="middle">1/4</text>
  <circle cx="200" cy="190" r="13" fill="#dbeafe" stroke="#2563eb" stroke-width="2.5"/>
  <text x="220" y="195" font-size="13" font-weight="700" fill="#172333" text-anchor="start">c</text>
  <text x="200" y="216" font-size="12" fill="#64748b" text-anchor="middle">1/4</text>
  <circle cx="270" cy="125" r="13" fill="#dbeafe" stroke="#2563eb" stroke-width="2.5"/>
  <text x="288" y="112" font-size="13" font-weight="700" fill="#172333" text-anchor="start">d</text>
  <text x="270" y="154" font-size="12" fill="#64748b" text-anchor="middle">1/4</text>
  <text x="160" y="244" font-size="12" fill="#64748b" text-anchor="middle">d_x(a) = 3/4, d_x(d) = 1/4</text>

  <!-- Panel 2: After adjacent merge -->
  <text x="325" y="62" font-size="13" fill="#172333" font-weight="600">merge d &#8594; a: pay x_d&#178; ; f = 5/16</text>
  <line x1="450" y1="125" x2="560" y2="125" stroke="#94a3b8" stroke-width="2" stroke-dasharray="4 3"/>
  <g stroke="#2563eb" stroke-width="3">
    <line x1="410" y1="190" x2="490" y2="190"/>
    <line x1="410" y1="190" x2="450" y2="125"/>
    <line x1="490" y1="190" x2="450" y2="125"/>
  </g>
  <circle cx="450" cy="125" r="13" fill="#dbeafe" stroke="#2563eb" stroke-width="2.5"/>
  <text x="450" y="104" font-size="13" font-weight="700" fill="#172333" text-anchor="middle">a</text>
  <text x="450" y="154" font-size="12" fill="#64748b" text-anchor="middle">1/2</text>
  <circle cx="410" cy="190" r="13" fill="#dbeafe" stroke="#2563eb" stroke-width="2.5"/>
  <text x="390" y="195" font-size="13" font-weight="700" fill="#172333" text-anchor="end">b</text>
  <text x="410" y="216" font-size="12" fill="#64748b" text-anchor="middle">1/4</text>
  <circle cx="490" cy="190" r="13" fill="#dbeafe" stroke="#2563eb" stroke-width="2.5"/>
  <text x="510" y="195" font-size="13" font-weight="700" fill="#172333" text-anchor="start">c</text>
  <text x="490" y="216" font-size="12" fill="#64748b" text-anchor="middle">1/4</text>
  <circle cx="560" cy="125" r="13" fill="#ffffff" stroke="#64748b" stroke-width="2" stroke-dasharray="4 3"/>
  <text x="560" y="104" font-size="13" font-weight="700" fill="#64748b" text-anchor="middle">d</text>
  <text x="560" y="154" font-size="12" fill="#64748b" text-anchor="middle">0</text>
  <text x="455" y="244" font-size="12" fill="#64748b" text-anchor="middle">change = (1/4)(3/4 &#8722; 1/4) &#8722; (1/4)&#178; = 1/16</text>
  <text x="455" y="264" font-size="12" fill="#64748b" text-anchor="middle">support {a, b, c} is now a clique</text>

  <!-- Panel 3: Symmetrize clique -->
  <text x="615" y="62" font-size="13" fill="#172333" font-weight="600">symmetrize the clique: f = 1/3</text>
  <line x1="740" y1="125" x2="845" y2="125" stroke="#94a3b8" stroke-width="2" stroke-dasharray="4 3"/>
  <g stroke="#2563eb" stroke-width="3">
    <line x1="700" y1="190" x2="780" y2="190"/>
    <line x1="700" y1="190" x2="740" y2="125"/>
    <line x1="780" y1="190" x2="740" y2="125"/>
  </g>
  <circle cx="740" cy="125" r="13" fill="#dbeafe" stroke="#2563eb" stroke-width="2.5"/>
  <text x="740" y="104" font-size="13" font-weight="700" fill="#172333" text-anchor="middle">a</text>
  <text x="740" y="154" font-size="12" fill="#64748b" text-anchor="middle">1/3</text>
  <circle cx="700" cy="190" r="13" fill="#dbeafe" stroke="#2563eb" stroke-width="2.5"/>
  <text x="680" y="195" font-size="13" font-weight="700" fill="#172333" text-anchor="end">b</text>
  <text x="700" y="216" font-size="12" fill="#64748b" text-anchor="middle">1/3</text>
  <circle cx="780" cy="190" r="13" fill="#dbeafe" stroke="#2563eb" stroke-width="2.5"/>
  <text x="800" y="195" font-size="13" font-weight="700" fill="#172333" text-anchor="start">c</text>
  <text x="780" y="216" font-size="12" fill="#64748b" text-anchor="middle">1/3</text>
  <circle cx="845" cy="125" r="13" fill="#ffffff" stroke="#64748b" stroke-width="2" stroke-dasharray="4 3"/>
  <text x="845" y="104" font-size="13" font-weight="700" fill="#64748b" text-anchor="middle">d</text>
  <text x="845" y="154" font-size="12" fill="#64748b" text-anchor="middle">0</text>
  <text x="745" y="244" font-size="12" fill="#64748b" text-anchor="middle">on a clique f = (1 &#8722; &#931;x_i&#178;)/2,</text>
  <text x="745" y="264" font-size="12" fill="#64748b" text-anchor="middle">max at uniform: (1 &#8722; 1/3)/2 = 1/3</text>

  <text x="40" y="318" font-size="12" fill="#64748b">The pendant cannot join a clique, so its weight migrates to the triangle; once the support is a clique, only the weight distribution matters. Two moves, one theorem.</text>
</svg>
```

**A mesh check (machine).** On all 64 graphs on 4 vertices, evaluating f on the 1/40 mesh of the simplex (all 12,341 lattice points x with 40·x ≥ 0 integral and Σ 40·x_i = 40) never exceeds (1 − 1/ω)/2, and **42 graphs attain it exactly**: the empty graph, the 40 triangle-free graphs with at least one edge (ω = 2, max 1/4), and K₄ (max 3/8). Why exactly those 42: on this mesh f takes values that are multiples of 1/1600, and 1600·(1−1/ω)/2 is an integer precisely for ω = 1, 2, 4 — for ω = 3 it is 800/3, unattainable. The same census at n = 5 (all 1,024 graphs, mesh 1/10 plus random points) never exceeds the bound either.

### 2.3 Spectral Turán — the clique number caps λ1

**Theorem.** λ1 ≤ (1 − 1/ω)·n.
*Proof.* If E = ∅, then ω = 1 and λ1 = 0 = (1 − 1/1)n. Otherwise let x be a unit Perron eigenvector of a connected G (entrywise ≥ 0 — this is where Perron–Frobenius earns its keep, since Motzkin–Straus needs x in the simplex; for disconnected G apply the argument to a component achieving λ1). Let s = Σ_v x_v > 0. Then

λ1 = xᵀAx = 2 Σ_{uv∈E} x_u x_v = 2 s² f(x/s) ≤ 2 s² · (1 − 1/ω)/2 = s²(1 − 1/ω),

by Motzkin–Straus applied to the normalized vector x/s; and Cauchy–Schwarz gives s² ≤ n·||x||² = n. So λ1 ≤ (1 − 1/ω)n. ∎

**Turán recovered.** Combine with Rayleigh (Lemma 1): m ≤ nλ1/2 ≤ (1 − 1/ω)n²/2 — the Turán bound m ≤ (1 − 1/r)n²/2 for K_{r+1}-free graphs, arriving by way of optimization. Machine check: on all 33,792 graphs on 5 and 6 vertices (the full censuses), λ1 ≤ (1 − 1/ω)n holds without exception, and K_{3,3} attains equality: λ1 = 3 = (1 − 1/2)·6.

**What you now own:** weight shifting as an optimization engine (P20), the merge lemma with its adjacent-merge correction, and the chain *Perron → simplex → Motzkin–Straus → Cauchy–Schwarz → spectral Turán → Turán* — five ideas, one line of inequality.

---

## Lecture 3 · Two-Distance Sets: A Capstone in Three Bounds

**Problem.** How many points can fit in R^d if all pairwise distances take at most **s** distinct values? The two-distance case (s = 2) is the classic; the answer weaves together every pattern of the chapter — Gram matrices, polynomials, and a sharp dichotomy between spherical and unrestricted configurations.

### 3.1 Warm-up: equidistant points — the centered Gram

**Lemma.** At most d + 1 points in R^d can be pairwise equidistant.
*Proof.* Let p_1, …, p_k be pairwise at distance δ > 0, and **center them**: c = (1/k)Σp_i, w_i = p_i − c, so Σw_i = 0. On the centered configuration two facts hold: first, summing ||w_i − w_j||² over all j gives (k−1)δ² = Σ_{j=1}^k ||w_i − w_j||² = k||w_i||² + Σ_{j=1}^k ||w_j||², and summing that over i gives k(k−1)δ² = 2k Σ_{j=1}^k ||w_j||², whence ||w_i||² = (k−1)δ²/(2k) for every i; second, w_i·w_j = (||w_i||² + ||w_j||² − δ²)/2 = −δ²/(2k) for i ≠ j. The Gram matrix of the w_i is then

G = (δ²/2)(I − J/k),

whose spectrum is δ²/2 on 𝟙⊥ (multiplicity k − 1) and 0 on 𝟙 — in particular G kills 𝟙 and has **rank k − 1**. But G = WWᵀ for the k×d matrix W whose rows are the centered vectors w_iᵀ, so k − 1 = rank G = rank W ≤ d: **k ≤ d + 1**. ∎

Tight: the standard simplex, w_i = e_i − 𝟙/k, has pairwise distance² = 2 and ||w_i||² = (k−1)/k — k = d + 1 points in the hyperplane Σx = 0 ⊂ R^{d+1} (isometric to R^d). (Machine: the centered Gram's spectrum {1 × (k−1), 0} verified for k = 2 … 9; the simplex vectors' distances and norms verified exactly.)

✎ **Checkpoint — the tempting shortcut.** Why not skip the centering and call (δ²/2)(J + I) "the Gram matrix"? It is positive definite — det(J_k + I_k) = k + 1 (checked for k = 2 … 9) — and full rank k, which would suggest k ≤ d, even better! The catch: those entries are the inner products of vectors of **norm δ from the origin**, and nothing in the hypothesis says the points are equidistant from anywhere. The uncentered configuration the shortcut secretly assumes does not exist in general; the centered Gram, rank k − 1, is the honest one, and the theorem it proves — k ≤ d + 1 — is tight.

### 3.2 The general bound: polynomials on the paraboloid

**Theorem.** A set of k points in R^d with at most s distinct pairwise distances satisfies k ≤ C(d + s + 1, s).
*Proof.* Let D be the realized squared-distance values (|D| ≤ s) and p_1, …, p_k the points. To each point assign the polynomial in y ∈ R^d:

f_i(y) = Π_{ℓ ∈ D}(||y − p_i||² − ℓ).

Then f_i(p_j) = 0 for j ≠ i (some distance factor vanishes — note 0 ∉ D, distances between distinct points are positive) and f_i(p_i) = Π_ℓ(−ℓ) ≠ 0. The evaluation matrix is diagonal: the f_i are linearly independent **as functions on the point set**. Now count the room they live in. Write ||y − p_i||² = ||y||² − 2p_i·y + ||p_i||²: each f_i is a polynomial of degree ≤ s in the d + 1 "variables" (y_1, …, y_d, ||y||²) — a function on the **paraboloid** t = ||y||² in R^{d+1}. The space of such functions Σ_{q=0}^s ||y||^{2q} g_q(y) with deg g_q ≤ s − q has dimension at most Σ_{q=0}^{s} C(d + s − q, s − q) = C(d + s + 1, s) (hockey-stick identity — machine-checked for d ≤ 6, s ≤ 4). Independent functions, finite room: k ≤ C(d+s+1, s). ∎

### 3.3 The spherical bound — Delsarte–Goethals–Seidel

If all points lie on a sphere of radius r, the paraboloid collapses: ||y − p_i||² = 2r² − 2p_i·y there, so each f_i agrees on the sphere with an ordinary polynomial of degree ≤ s in y — and distinct polynomials can agree **on the sphere**, an ambiguity that is exactly computable:

**Theorem (DGS).** A set of k points on a sphere in R^d with at most s ≥ 1 pairwise distances satisfies k ≤ C(d+s, s) − C(d+s−2, s−2) = C(d+s−1, s) + C(d+s−2, s−1) (with C(n,m) = 0 for m < 0).
*Proof.* The restriction map Π_≤s (polynomials of degree ≤ s in y, dimension C(d+s, s)) → functions on the sphere has a kernel containing every polynomial (r² − ||y||²)·h(y) with deg h ≤ s − 2 — these vanish identically on the sphere ||y||² = r², and multiplication by (r² − ||y||²) is injective on polynomials (a product of nonzero polynomials over R is nonzero). So the image has dimension ≤ C(d+s, s) − C(d+s−2, s−2); the independent f_i live in that image. For s = 2 the bound is d(d+3)/2. ∎

For s = 2 the honest comparison: general C(d+3, 2) versus spherical d(d+3)/2 — e.g. d = 2: 10 versus 5; d = 3: 15 versus 9. The **sharp** general bound is in fact C(d+s, s) (Bannai–Bannai–Stanton 1983; a short proof by Petrov–Pohoata 2019) — tighter than the paraboloid bound and cited here, not re-proved: the chapter's own proved bound is C(d+s+1, s).

### 3.4 Witnesses, drawn and machine-checked

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 880 370" font-family="system-ui, -apple-system, 'Segoe UI', sans-serif">
  <rect x="0" y="0" width="880" height="370" fill="#ffffff"/>
  <text x="40" y="34" font-size="17" font-weight="700" fill="#193e5c">Figure 2 &#183; Two spherical witnesses: the pentagon in R&#178; and the octahedron in R&#179; (Lecture 3)</text>

  <!-- Left: Pentagon on unit circle -->
  <circle cx="220" cy="170" r="105" fill="none" stroke="#64748b" stroke-width="1.5" stroke-dasharray="6 5"/>
  <polygon points="220,65 120,138 158,255 282,255 320,138" fill="none" stroke="#2563eb" stroke-width="3"/>
  <g stroke="#2563eb" stroke-width="1.5" stroke-dasharray="5 4">
    <line x1="220" y1="65" x2="158" y2="255"/>
    <line x1="220" y1="65" x2="282" y2="255"/>
    <line x1="120" y1="138" x2="320" y2="138"/>
    <line x1="120" y1="138" x2="282" y2="255"/>
    <line x1="320" y1="138" x2="158" y2="255"/>
  </g>
  <circle cx="220" cy="65" r="11" fill="#dbeafe" stroke="#2563eb" stroke-width="2.5"/>
  <circle cx="120" cy="138" r="11" fill="#dbeafe" stroke="#2563eb" stroke-width="2.5"/>
  <circle cx="158" cy="255" r="11" fill="#dbeafe" stroke="#2563eb" stroke-width="2.5"/>
  <circle cx="282" cy="255" r="11" fill="#dbeafe" stroke="#2563eb" stroke-width="2.5"/>
  <circle cx="320" cy="138" r="11" fill="#dbeafe" stroke="#2563eb" stroke-width="2.5"/>
  <text x="40" y="298" font-size="13" fill="#172333" font-weight="600">pentagon on the unit circle (r = 1):</text>
  <text x="40" y="318" font-size="12" fill="#64748b">side 1.1756, diagonal 1.9021; squared distances {4sin&#178;36&#176;, 4sin&#178;72&#176;} = {1.38197, 3.61803}</text>
  <text x="40" y="338" font-size="12" fill="#64748b">k = 5 = d(d+3)/2 = 2&#183;5/2 &#8212; spherical bound tight at d = 2</text>

  <!-- Right: Octahedron in R^3 -->
  <g stroke="#2563eb" stroke-width="2.5">
    <line x1="620" y1="80" x2="700" y2="165"/>
    <line x1="620" y1="80" x2="540" y2="165"/>
    <line x1="620" y1="80" x2="665" y2="205"/>
    <line x1="620" y1="80" x2="575" y2="125"/>
    <line x1="620" y1="250" x2="700" y2="165"/>
    <line x1="620" y1="250" x2="540" y2="165"/>
    <line x1="620" y1="250" x2="665" y2="205"/>
    <line x1="620" y1="250" x2="575" y2="125"/>
    <line x1="700" y1="165" x2="665" y2="205"/>
    <line x1="665" y1="205" x2="540" y2="165"/>
    <line x1="540" y1="165" x2="575" y2="125"/>
    <line x1="575" y1="125" x2="700" y2="165"/>
  </g>
  <g stroke="#dc2626" stroke-width="1.5" stroke-dasharray="5 4">
    <line x1="620" y1="80" x2="620" y2="250"/>
    <line x1="540" y1="165" x2="700" y2="165"/>
    <line x1="575" y1="125" x2="665" y2="205"/>
  </g>
  <circle cx="620" cy="80" r="11" fill="#dbeafe" stroke="#2563eb" stroke-width="2.5"/>
  <circle cx="620" cy="250" r="11" fill="#dbeafe" stroke="#2563eb" stroke-width="2.5"/>
  <circle cx="700" cy="165" r="11" fill="#dbeafe" stroke="#2563eb" stroke-width="2.5"/>
  <circle cx="540" cy="165" r="11" fill="#dbeafe" stroke="#2563eb" stroke-width="2.5"/>
  <circle cx="665" cy="205" r="11" fill="#dbeafe" stroke="#2563eb" stroke-width="2.5"/>
  <circle cx="575" cy="125" r="11" fill="#dbeafe" stroke="#2563eb" stroke-width="2.5"/>
  <text x="465" y="298" font-size="13" fill="#172333" font-weight="600">octahedron in R&#179;: 6 points, red dashes = antipodal pairs</text>
  <text x="465" y="318" font-size="12" fill="#64748b">squared distances {2, 4}; spherical bound 9, general 15.</text>
  <text x="465" y="338" font-size="12" fill="#64748b">Non-spherical witness: {0, 1, 2} on R&#185; &#8212; {1, 4}, m(1) = 3.</text>
</svg>
```

The three canonical witnesses, with their machine-checked data. **Pentagon** (unit circle): squared distances {4sin²36°, 4sin²72°} = {1.38197, 3.61803}; its f_i evaluation matrix has rank 5 in the spherical quotient of dimension exactly 5 — the spherical bound d(d+3)/2 = 5 is **tight** at d = 2. **Octahedron** (R³): squared distances {2, 4}, 6 points — rank 6 against spherical dimension 9 and paraboloid dimension C(6,2) = 15 (slack both ways). **{0, 1, 2}** (R¹): squared distances {1, 4}, 3 points = m(1) — and non-spherical: no point of the line is equidistant from all three.

### 3.5 The landscape: known maxima and arithmetic rigidity

The known maxima for two-distance sets in small dimensions (research literature; cited, not derived here):

| d | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 |
|---|---|---|---|---|---|---|---|---|
| m(d) | 3 | 5 | 6 | 10 | 16 | 27 | 29 | 45 |

Two entries deserve their names: m(2) = 5 (the pentagon) and m(6) = 27 (the Schläfli-graph construction) attain the spherical bound d(d+3)/2 exactly; m(8) = 45 is **non-spherical** and tight for the sharp general bound C(d+2, 2) = C(10,2) = 45. Beyond the bounds, the Larman–Rogers–Seidel phenomenon (cited): once a spherical two-distance set has more than 2d + 3 points, strong integrality conditions fall on the distance data — large two-distance sets are arithmetically rigid, which is one reason the table above is so sparse and so hard to extend.

### 3.6 Grids: two-distance sets under lattice discipline

How much of this geometry survives on the integer lattice? Machine censuses, exhaustive:

- The 9-point line {0, …, 8}: maximum two-distance subset has **3** points ({0,1,2}-type — and any 4 collinear lattice points already span 3 distances).
- The 7×7 grid [−3..3]²: **no** 5-point two-distance subset exists (all C(49,5) = 1,906,884 five-subsets checked); 4 is attained by the square (±1, ±1) with squared distances {4, 8}. The pentagon, in particular, is **not lattice-realizable** — the plane's 2-distance optimum cannot be drawn on the integer grid, even in a 7×7 window.
- The 3×3×3 grid [−1..1]³: **no** 7-point two-distance subset (all C(27,7) = 888,030 checked); 6 is attained by the octahedron {±e_1, ±e_2, ±e_3} with squared distances {2, 4} — the octahedron *is* lattice-realizable, where the pentagon is not.

**What you now own:** the centered-Gram reflex (center before you count — the equidistant lemma's rank k − 1 is the whole theorem), the paraboloid lift for unrestricted configurations, the sphere-relation discount for spherical ones, and the habit of asking not just "what is the maximum" but "what arithmetic does the configuration force".

---

## Lecture 4 · The Modern Toolkit: Interlacing, Hoffman, Theta, and Delsarte's Program

Chapter 6's four lectures and Lectures 1–3 here built one machine — encode combinatorics as vectors, then let dimension and spectrum do the counting — and pointed it at seven problem families. This lecture upgrades the machine to its modern form, in an order that is almost a story. **Interlacing** says that substructures inherit eigenvalues, and it explains retroactively why the spectral moves of Chapter 6's Lecture 4 and Lectures 1–2 here were legal at all. **Hoffman's bound** turns the smallest eigenvalue into a quantitative cap on independent sets and a lower bound on the chromatic number. **Lovász theta** is a single number sandwiched between α and χ(Ḡ); computing it exactly for the five-cycle — θ(C₅) = √5 — is the theorem that carried semidefinite programming into combinatorics. And **Delsarte's linear program** runs the polynomial method of Chapter 6's Lecture 3 on the Hamming cube, where hand-checkable polynomials certify exact code sizes. Every number below is machine-checked; the lab's Part 3 reproduces every run.

### 4.1 Interlacing: submatrices inherit the spectrum

Everything rests on one lemma about symmetric matrices, proved once and reused three ways.

**Lemma (min–max).** For a real symmetric matrix A with eigenvalues λ1 ≥ … ≥ λn and Rayleigh quotient R(x) = (xᵀAx)/(xᵀx):

λ_k = max_{dim T = k} min_{x ∈ T∖{0}} R(x) = min_{dim S = n−k+1} max_{x ∈ S∖{0}} R(x).

*Proof.* For the max–min: any k-dimensional T meets the span of the eigenvectors v_k, …, v_n (dimensions add to n + 1), and on that span R never exceeds λ_k — so min_T R ≤ λ_k. Equality: on T = span(v_1, …, v_k) the quotient never drops below λ_k. The min–max is the mirror argument: any (n−k+1)-dimensional S meets span(v_1, …, v_k), where R is at least λ_k; equality on span(v_k, …, v_n). ∎

**Theorem (Cauchy interlacing).** Let B be the m × m principal submatrix of the symmetric A (delete some rows and the same columns), with eigenvalues μ1 ≥ … ≥ μm. Then for every i:

λ_i ≥ μ_i ≥ λ_{i+n−m}.

*Proof.* B is the quadratic form of A restricted to a coordinate subspace U of dimension m — padded vectors preserve Rayleigh quotients. Upper: μ_k = max over k-dimensional T ⊆ U of min R_B = max over those T of min R_A ≤ max over all k-dimensional T of min R_A = λ_k. Lower: apply the upper bound to −A and −B, whose k-th largest eigenvalues are −μ_{m+1−k} and −λ_{n+1−k}: −μ_{m+1−k} ≤ −λ_{n+1−k}, i.e. μ_i ≥ λ_{i+n−m} for i = m+1−k. ∎

Two remarks make the theorem usable. First, the proof never used that U is a *coordinate* subspace: the same interlacing holds for the matrix of the form restricted to **any** m-dimensional subspace W — this is *compression*, and it is how partitions enter. Second, taking induced subgraphs is exactly taking principal submatrices of the adjacency matrix, so graph-theoretic conclusions fall out immediately.

**Corollary (monotonicity).** Adding an edge cannot decrease λ1: the unit Perron vector x ≥ 0 of the smaller graph, tested against both adjacency matrices, gives λ1(A + E) ≥ xᵀ(A + E)x ≥ xᵀAx = λ1(A).

**Corollary (the inertia bound).** α(G) ≤ n − p(A) and α(G) ≤ n − q(A), where p, q are the counts of positive and negative eigenvalues of A.

*Proof.* An independent set S makes A_S — the principal submatrix on S — the zero matrix, whose |S| eigenvalues are all 0. Interlacing reads this twice: μ_α = 0 forces λ_α ≥ 0 (at least α eigenvalues are nonnegative: α ≤ p + z), and μ_1 = 0 forces λ_{1+n−α} ≤ 0 (at least α are nonpositive: α ≤ q + z); z is the zero count, and p + z = n − q, q + z = n − p. ∎

✎ **Checkpoint.** Petersen: spectrum {3, 1⁵, −2⁴} — p = 6, so n − p = 4 = α, tight. C₅: spectrum {2, 0.618², −1.618²} — p = 3, q = 2, and n − p = 2 = α, also tight. The lab (Part 3) runs the bound over **all 1,099 graphs with n ≤ 5**: never violated, tight 633 times on n − p (954 on n − q, and 966 on min(n − p, n − q)).

**Partitions: compression and quotients.** Let V = C_1 ∪ … ∪ C_m be a partition of the vertex set into nonempty cells, U its indicator matrix (column j is 𝟙_{C_j}), and Q = U(UᵀU)^{−1/2} the orthonormalized version. Then B = QᵀAQ is the compressed matrix, and its eigenvalues interlace A's by the remark above. When the partition is *equitable* — every vertex of C_i has exactly b_ij neighbors in C_j — something stronger happens:

**Theorem (equitable quotients).** For an equitable partition, the quotient matrix B_quot = (b_ij) has its entire spectrum inside A's: every eigenvalue of B_quot is an eigenvalue of A.

*Proof.* If B_quot w = μw with w ≠ 0, lift w to the nonzero vector x with x_v = w_{cell(v)}. Then (Ax)_v = Σ_j b_{cell(v),j}·w_j = μ·w_{cell(v)} = μ·x_v: an eigenvector. ∎

This is Chapter 6's Exercise 6 computation, licensed. The windmill W_t with the partition {hub} ∪ {everything else} is equitable (the hub has 2t neighbors in the second class; every blade vertex has one neighbor in each), and its 2×2 quotient [[0, 2t], [1, 1]] has eigenvalues (1 ± √(1+8t))/2 — exactly the two exotic eigenvalues that Chapter 6's A6 hunted down. ✎ The lab verifies both quotients inside the full Jacobi spectra of W₂ and W₃.

**The unification.** Look back with new eyes: Chapter 6's Lecture 4 spectral lemma diagonalized on invariant subspaces; L1's Rayleigh tools *are* the min–max lemma; L2's s² ≤ n bounded a linear form via Cauchy–Schwarz. Each spectral restriction — to a coordinate block, an invariant subspace, or a partition span — is a compression: restrict the matrix to a well-chosen subspace, then bound. Interlacing is the general theorem that makes every such restriction honest, and it is the tool the next two sections use.

### 4.2 Hoffman's bound: the smallest eigenvalue prices independence

The inertia bound of §4.1 counts eigenvalues — how many sit on each side of zero. Hoffman's bound makes the *sizes* of the eigenvalues do the work, and its engine is a construction the next section will reuse at full power: a degenerate inner product.

**Lemma (PSD semi-inner products).** If M is a real symmetric positive semidefinite matrix, then ⟨x, y⟩_M = xᵀMy is a symmetric bilinear form with ⟨x, x⟩_M ≥ 0 for all x, and it satisfies Cauchy–Schwarz: ⟨x, y⟩_M² ≤ ⟨x, x⟩_M⟨y, y⟩_M.

*Proof.* Symmetry and nonnegativity are the definition of PSD. For Cauchy–Schwarz, complete the square: for any real t, 0 ≤ ⟨x − ty, x − ty⟩_M = ⟨x, x⟩_M − 2t⟨x, y⟩_M + t²⟨y, y⟩_M. If ⟨y, y⟩_M > 0, take t = ⟨x, y⟩_M/⟨y, y⟩_M and read off the discriminant. If ⟨y, y⟩_M = 0, then ⟨x − ty, x − ty⟩_M = ⟨x, x⟩_M − 2t⟨x, y⟩_M is nonnegative for *every* t, forcing ⟨x, y⟩_M = 0, and the inequality reads 0 ≤ 0. ∎

Degeneracy — the possibility ⟨x, x⟩_M = 0 with x ≠ 0 — is not a bug but the mechanism: the null directions of M are exactly what an extremal independent set exploits.

**Theorem (Hoffman's bound).** Let G be d-regular on n vertices with smallest eigenvalue λ_n < 0. Then

α(G) ≤ n·(−λ_n)/(d − λ_n).

*Proof.* Set M = A − λ_n·I; it is PSD, since every eigenvalue of M is λ_i − λ_n ≥ 0. Take the semi-inner product ⟨·,·⟩_M and let S be a nonempty independent set of size s, with x = 𝟙_S. Three inner products:

- ⟨x, x⟩_M = 𝟙_SᵀA𝟙_S − λ_n·s = 2e(S) − λ_n·s = −λ_n·s, because S independent means 𝟙_SᵀA𝟙_S = 2e(S) = 0;
- ⟨x, 𝟙⟩_M = 𝟙_SᵀA𝟙 − λ_n·s = ds − λ_n·s = s(d − λ_n), because d-regularity counts every edge leaving S;
- ⟨𝟙, 𝟙⟩_M = 2m − λ_n·n = n(d − λ_n).

Cauchy–Schwarz gives s²(d − λ_n)² ≤ (−λ_n·s)·n(d − λ_n); divide by s(d − λ_n) > 0. ∎

**Theorem (Hoffman's chromatic bound).** With the same hypotheses, χ(G) ≥ 1 + d/|λ_n|.

*Proof 1 (through α).* The color classes of a χ-coloring partition V into χ independent sets, so χ·α ≥ n. Feeding in Hoffman's bound: χ ≥ n/α ≥ (d + |λ_n|)/|λ_n| = 1 + d/|λ_n|. ∎

*Proof 2 (compression, no α needed).* Let C_1, …, C_k be the nonempty classes of any proper k-coloring, Q the orthonormalized indicator matrix of §4.1, and B = QᵀAQ the compression. Three facts, in order. (i) Each diagonal entry B_ii = q_iᵀAq_i = 2e(C_i)/|C_i| = 0 — the classes are independent — so tr B = 0. (ii) For w = (√|C_1|, …, √|C_k|) we have Qw = 𝟙, so wᵀBw = 𝟙ᵀA𝟙 = nd and wᵀw = n: the Rayleigh quotient is d, giving μ_1 ≥ d; interlacing gives μ_1 ≤ λ_1 = d, so μ_1 = d exactly. (iii) The remaining k − 1 eigenvalues sum to tr B − μ_1 = −d, and each satisfies μ_i ≥ λ_n by interlacing. Hence −d = Σ_{i≥2} μ_i ≥ (k − 1)λ_n, i.e. k ≥ 1 + d/|λ_n|. ∎

Proof 2 is worth the detour: it never mentions independent sets, it runs entirely on the compression machine of §4.1, and its chain — tr B = 0, μ_1 = d, then Σ_{i≥2}μ_i = −d pinned below by (k−1)λ_n — is exactly the kind of bookkeeping the lab can check on real colorings.

**Petersen (d = 3, λ_n = −2).** The bound reads α ≤ 10·2/(3+2) = 4 — tight, and the five witnesses are the stars of Chapter 6's Exercise ◆12 census. Each star S attains equality in Cauchy–Schwarz: ⟨𝟙_S, 𝟙_S⟩_M = 8, ⟨𝟙_S, 𝟙⟩_M = 20, ⟨𝟙, 𝟙⟩_M = 50, and 8·50 = 400 = 20². Equality is explained by direct computation: M𝟙_S = 2𝟙 and M𝟙 = 5𝟙, so M(𝟙_S − (2/5)𝟙) = 0 — the difference vector is null for M, which is precisely what equality in a *degenerate* Cauchy–Schwarz demands. The chromatic bound: χ ≥ 1 + 3/2 = 2.5, so χ ≥ 3, and 3 it is.

**C₅ (d = 2, λ_n = −φ, φ = (1+√5)/2).** The bound is 5φ/(2 + φ), and this simplifies *exactly*: φ√5 = (5+√5)/2 = 2 + φ, so 5φ/(2+φ) = √5. Thus α ≤ √5 ≈ 2.236 against the true α = 2. Hold that number: the next section computes θ(C₅) = √5 exactly — Hoffman and theta agree on the pentagon, from opposite directions.

**Three calibrations.** K_n: d = n−1, λ_n = −1, α ≤ 1 and χ ≥ n — both exact. Bipartite d-regular: λ_n = −d, so α ≤ n/2 (structural equality: each side of the bipartition is independent) and χ ≥ 1 + 1 = 2 — the bound reads bipartiteness straight off the spectrum. The cocktail party K₆ minus a perfect matching (d = 4, spectrum {4, 0³, −2²}): α ≤ 6·2/6 = 2, tight — the three deleted pairs — and χ ≥ 3, exact again.

✎ **Checkpoint.** The lab sweeps the bound over **all 1,122 d-regular graphs on n = 4…7 vertices with λ_n < 0**: not once is it violated, and it is tight 225 times (7 of 7 at n = 4, 1 of 13 at n = 5, 111 of 171 at n = 6, 106 of 931 at n = 7). The chromatic bound was checked on all 191 regular graphs with n = 4…6 — zero violations — with Proof 2's chain verified coloring by coloring.

### 4.3 Lovász theta: one number between α and χ(Ḡ)

Hoffman caps α from above with the spectrum, but the cap is one-sided: α can fall well short of it (C₅: cap √5, truth 2). Lovász's theta is a different kind of object — a single number that always sits between α(G) and χ(Ḡ), computable in polynomial time by semidefinite programming, and on the pentagon *exactly computable by hand*: θ(C₅) = √5.

**Definition (orthogonal representation).** An orthogonal representation (OR) of G assigns unit vectors u_1, …, u_n to the vertices so that u_i ⊥ u_j whenever v_i and v_j are **non-adjacent** — orthogonality on non-edges, the reverse of the graph's own logic. For a unit *handle* c, the value of the pair ({u_i}, c) is max_i 1/(c·u_i)², and

θ(G) = min over all ORs and handles of that value.

**Calibrations.** θ(K_n) = 1: no non-edges means no constraints; take all u_i = c for value 1, and nothing can beat 1 since |c·u_i| ≤ 1 for unit vectors always. θ(E_n) = n: the empty graph forces the u_i pairwise orthogonal, so Bessel gives 1 = ||c||² ≥ Σ_i (c·u_i)², and some i has (c·u_i)² ≤ 1/n — every representation has value at least n. An orthonormal basis with handle c = 𝟙/√n attains it: c·u_i = 1/√n for all i.

**Theorem (the sandwich).** α(G) ≤ θ(G) ≤ χ(Ḡ).

*Proof, lower bound.* An independent set S is pairwise non-adjacent, so in any OR the vectors {u_i : i ∈ S} are pairwise orthogonal and Bessel gives Σ_{i∈S}(c·u_i)² ≤ 1. Some i ∈ S has (c·u_i)² ≤ 1/|S|, so *every* representation has value ≥ |S|; the minimum over representations is at least α. ∎

*Proof, upper bound.* A k-coloring of the complement Ḡ is a partition of V into k cliques of G. Set u_i = e_{color(i)} ∈ R^k and c = 𝟙/√k. Non-adjacent vertices of G are adjacent in Ḡ, so they carry different colors — different standard basis vectors, orthogonal. And c·u_i = 1/√k for every i, so the value is exactly k. Minimizing over k = χ(Ḡ). ∎

Both ends of the sandwich are NP-hard to compute; θ itself is not — that is the point (semidefinite programming, cited). On *perfect* graphs the sandwich collapses to θ = α = χ(Ḡ) (cited), which is what makes the pentagon — the smallest imperfect graph — the interesting case: all three numbers differ.

**The umbrella.** Label C₅'s vertices 0, …, 4 cyclically; the non-edges are the five distance-2 pairs. Take an umbrella: five unit vectors at azimuths 2πi/5 around an axis, all tilted by the same angle ψ from it,

u_i = (sin ψ·cos(2πi/5), sin ψ·sin(2πi/5), cos ψ), so u_i·u_j = sin²ψ·cos(2π(i−j)/5) + cos²ψ.

Demand orthogonality on the distance-2 pairs: sin²ψ·cos(4π/5) + cos²ψ = 0, i.e. cos²ψ = cos(π/5)/(1 + cos(π/5)). Now the golden ratio φ = (1+√5)/2 — which already owned λ_n = −φ in §4.2 — enters twice: cos(π/5) = φ/2, and φ√5 = 2 + φ. So

cos²ψ = (φ/2)/(1 + φ/2) = φ/(2 + φ) = **1/√5, exactly**.

The machine check confirms it: distance-2 products vanish (to 1.7 × 10⁻¹⁶ in floating point). What the umbrella buys is a constant handle price: c·u_i = cos ψ = 5^(−1/4) for every i, so the value is 1/cos²ψ:

**θ(C₅) ≤ √5.**

The adjacent pairs come along for free: u_i·u_{i+1} = sin²ψ·cos(2π/5) + cos²ψ = (√5−1)/2 = 1/φ. The inner products draw a golden pentagon — 1/φ on edges, 0 on non-edges — echoing L3's pentagon, whose squared distances {4sin²36°, 4sin²72°} = {1.38197, 3.61803} were φ-fractions too.

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 880 340" font-family="system-ui, -apple-system, 'Segoe UI', sans-serif">
  <rect x="0" y="0" width="880" height="340" fill="#ffffff"/>
  <text x="40" y="34" font-size="17" font-weight="700" fill="#193e5c">Figure 3 &#183; Lov&#225;sz's umbrella for C&#8325;: cos&#178;&#968; = 1/&#8730;5 makes distance-2 pairs orthogonal (Lecture 4)</text>

  <!-- Left: Umbrella -->
  <text x="230" y="64" font-size="13" fill="#172333" font-weight="600" text-anchor="middle">the umbrella: five spokes, one tilt &#968;</text>
  <ellipse cx="230" cy="235" rx="150" ry="48" fill="none" stroke="#64748b" stroke-width="2" stroke-dasharray="4 3"/>
  <line x1="230" y1="85" x2="230" y2="295" stroke="#64748b" stroke-width="2" stroke-dasharray="4 3"/>
  <text x="242" y="252" font-size="13" font-weight="700" fill="#172333">c</text>
  <g stroke="#2563eb" stroke-width="3">
    <line x1="230" y1="85" x2="380" y2="235"/>
    <line x1="230" y1="85" x2="276" y2="189"/>
    <line x1="230" y1="85" x2="109" y2="207"/>
    <line x1="230" y1="85" x2="109" y2="263"/>
    <line x1="230" y1="85" x2="276" y2="281"/>
  </g>
  <path d="M 237 92 L 230 99 L 223 92" fill="none" stroke="#dc2626" stroke-width="2"/>
  <text x="195" y="88" font-size="12" fill="#dc2626" text-anchor="end">u&#8320; &#8869; u&#8322;</text>
  <circle cx="380" cy="235" r="12" fill="#dbeafe" stroke="#2563eb" stroke-width="2.5"/>
  <text x="398" y="240" font-size="13" font-weight="700" fill="#172333">u&#8320;</text>
  <circle cx="276" cy="189" r="12" fill="#dbeafe" stroke="#2563eb" stroke-width="2.5"/>
  <text x="294" y="186" font-size="13" font-weight="700" fill="#172333" text-anchor="start">u&#8321;</text>
  <circle cx="109" cy="207" r="12" fill="#dbeafe" stroke="#2563eb" stroke-width="2.5"/>
  <text x="90" y="211" font-size="13" font-weight="700" fill="#172333" text-anchor="end">u&#8322;</text>
  <circle cx="109" cy="263" r="12" fill="#dbeafe" stroke="#2563eb" stroke-width="2.5"/>
  <text x="90" y="267" font-size="13" font-weight="700" fill="#172333" text-anchor="end">u&#8323;</text>
  <circle cx="276" cy="281" r="12" fill="#dbeafe" stroke="#2563eb" stroke-width="2.5"/>
  <text x="296" y="286" font-size="13" font-weight="700" fill="#172333" text-anchor="start">u&#8324;</text>
  <text x="230" y="310" font-size="12" fill="#64748b" text-anchor="middle">cos&#178;&#968; = cos(&#960;/5)/(1 + cos(&#960;/5)) = 1/&#8730;5 &#8658; 1/cos&#178;&#968; = &#8730;5</text>
  <text x="230" y="328" font-size="12" fill="#64748b" text-anchor="middle">u_i &#183; u_(i+2) = 0 on all five distance-2 pairs</text>

  <!-- Right: Dot-product pentagon -->
  <text x="650" y="64" font-size="13" fill="#172333" font-weight="600" text-anchor="middle">the pentagon it draws: the dot products</text>
  <g stroke="#dc2626" stroke-width="2" stroke-dasharray="7 5">
    <line x1="650" y1="75" x2="706" y2="247"/>
    <line x1="740" y1="141" x2="594" y2="247"/>
    <line x1="706" y1="247" x2="560" y2="141"/>
    <line x1="594" y1="247" x2="650" y2="75"/>
    <line x1="560" y1="141" x2="740" y2="141"/>
  </g>
  <g stroke="#2563eb" stroke-width="3">
    <line x1="650" y1="75" x2="740" y2="141"/>
    <line x1="740" y1="141" x2="706" y2="247"/>
    <line x1="706" y1="247" x2="594" y2="247"/>
    <line x1="594" y1="247" x2="560" y2="141"/>
    <line x1="560" y1="141" x2="650" y2="75"/>
  </g>
  <circle cx="650" cy="75" r="13" fill="#dbeafe" stroke="#2563eb" stroke-width="2.5"/>
  <text x="650" y="80" font-size="13" font-weight="700" fill="#172333" text-anchor="middle">0</text>
  <circle cx="740" cy="141" r="13" fill="#dbeafe" stroke="#2563eb" stroke-width="2.5"/>
  <text x="740" y="146" font-size="13" font-weight="700" fill="#172333" text-anchor="middle">1</text>
  <circle cx="706" cy="247" r="13" fill="#dbeafe" stroke="#2563eb" stroke-width="2.5"/>
  <text x="706" y="252" font-size="13" font-weight="700" fill="#172333" text-anchor="middle">2</text>
  <circle cx="594" cy="247" r="13" fill="#dbeafe" stroke="#2563eb" stroke-width="2.5"/>
  <text x="594" y="252" font-size="13" font-weight="700" fill="#172333" text-anchor="middle">3</text>
  <circle cx="560" cy="141" r="13" fill="#dbeafe" stroke="#2563eb" stroke-width="2.5"/>
  <text x="560" y="146" font-size="13" font-weight="700" fill="#172333" text-anchor="middle">4</text>
  <text x="650" y="310" font-size="12" fill="#64748b" text-anchor="middle">solid: u_i &#183; u_(i+1) = 1/&#966; &#8776; 0.618 &#183; dashed: u_i &#183; u_(i+2) = 0</text>
  <text x="650" y="328" font-size="12" fill="#64748b" text-anchor="middle">handle c meets every spoke at angle &#968; &#8212; value &#952;(C&#8325;) &#8804; &#8730;5</text>
</svg>
```

**Certificates: the dual side.** The umbrella bounds θ from above. For the reverse direction, dual feasible points are matrices one can check by hand.

**Lemma (certificate lemma).** Let X be a real symmetric n × n matrix with (i) X ⪰ 0, (ii) X_ij ≥ 0 entrywise, (iii) X_ij = 0 on every edge of G, (iv) tr X = 1. Then J•X ≤ θ(G), where J is the all-ones matrix and • is the entrywise inner product Σ_{i,j} A_ij·B_ij.

*Proof.* Fix any OR {u_i} with handle c and value t, so (c·u_i)² ≥ 1/t for every i. Let M be the Gram matrix (M_ij = u_i·u_j) and v the vector (c·u_i)_i.

*Step 1: X•M = tr X.* Expand X•M = Σ_ij X_ij(u_i·u_j). The off-diagonal terms die two ways: on *edges* X_ij = 0, and on *non-edges* u_i ⊥ u_j. The diagonal terms are X_ii·||u_i||² = X_ii (the u_i are unit). So X•M = Σ_i X_ii = 1.

*Step 2: M ⪰ vvᵀ.* M − vvᵀ is the Gram matrix of the residual vectors u_i − (c·u_i)c — hence PSD. Since the Frobenius inner product of two PSD matrices is nonnegative, 0 ≤ X•(M − vvᵀ) = 1 − vᵀXv, so vᵀXv ≤ 1.

*Step 3: an entrywise Cauchy–Schwarz.* Every c·u_i is nonzero (it squares to at least 1/t), and flipping the sign of any u_i preserves both the OR property and all |c·u_i| — so WLOG v_i > 0. Then

(J•X)² = (Σ_ij X_ij)² = (Σ_ij √(X_ij/(v_iv_j))·√(X_ij·v_iv_j))² ≤ (Σ_ij X_ij/(v_iv_j))·(vᵀXv),

and since 1/(v_iv_j) ≤ max_i(1/v_i²) by AM–GM while X_ij ≥ 0, the first factor is at most max_i(1/v_i²)·(J•X). Dividing by J•X > 0 (it is at least tr X = 1):

J•X ≤ (vᵀXv)·max_i(1/v_i²) ≤ 1·t. ∎

**The circulant certificate, and θ(C₅) = √5.** On C₅ set X_ii = 1/5, X_ij = b = (√5−1)/10 on the five distance-2 pairs, and X_ij = 0 on the five edges. The four conditions, checked: entrywise nonnegative ✓; zero on edges ✓; tr X = 5·(1/5) = 1 ✓; and PSD because X is a circulant whose five eigenvalues are

**{√5/5, (5−√5)/10, (5−√5)/10, 0, 0}** — all nonnegative.

(The trace reads √5/5 + 2(5−√5)/10 = 1, as it must.) The payoff: J•X = 1 + 10b = 1 + (√5−1) = **√5**. Machine check: the five eigenvalues, the trace, and J•X = √5 verify to 10⁻¹². So the lemma gives θ(C₅) ≥ √5, and with the umbrella:

**θ(C₅) = √5 — exactly.** The sandwich on the pentagon is strict on both sides: α = 2 < θ = √5 ≈ 2.236 < χ(C̄₅) = 3. Note the echo: Hoffman's cap (§4.2) produced the *same* √5 on C₅ — the smallest eigenvalue and the semidefinite dual agree on the pentagon, and the truth 2 sits strictly below both.

**The capacity of the pentagon.** Shannon's zero-error capacity of G is Θ(G) = sup_k α(G^⊠k)^(1/k), where ⊠ is the strong product — (u, v) adjacent to (u′, v′) when each coordinate is equal-or-adjacent and at least one is adjacent. Lovász proved θ *multiplicative* under the strong product, θ(G⊠H) = θ(G)·θ(H) (cited); since α ≤ θ always, α(G^⊠k) ≤ θ(G)^k, and taking roots:

**Θ(G) ≤ θ(G)** — theta caps capacity.

For C₅ the interesting floor is the *square*: α(C₅ ⊠ C₅) = 5, not 4 = α² — machine-checked exhaustively. None of the C(25,6) = 177,100 six-subsets is independent, and exactly ten five-subsets are; a clean witness is the diagonal {(i, 2i mod 5) : i = 0..4}, independent because doubling turns adjacent pairs into distance-2 pairs and vice versa, so every pair fails adjacency in at least one coordinate. So √5 ≤ Θ(C₅) ≤ θ(C₅) = √5, and

**Θ(C₅) = √5** — the exact value Shannon's own bounds could not reach; the umbrella and the certificate met it from both sides.

✎ **Checkpoint.** Part 3 of the lab recomputes every ingredient: the umbrella's dot products (vanishing on distance-2 pairs, 1/φ on edges), the circulant certificate's eigenvalues, trace, and J•X, and the strong-product census (0 of 177,100 six-sets independent; ten independent five-sets).

### 4.4 Delsarte's program: the polynomial method on the Hamming cube

Theta ran Chapter 6's Lecture 3 polynomial thinking through semidefinite geometry; Delsarte's linear program runs it through the Hamming cube — and on the cube, hand-checkable polynomials certify exact code sizes.

**Problem.** A (binary) code is a subset C ⊆ {0,1}^n in which any two distinct words differ in at least d positions (minimum distance d); A(n,d) is the largest possible size. Same forbidden-configuration shape as Chapter 6's Lectures 1–3, new ambient space.

**The distance distribution.** For a nonempty code of size M set A_i = (1/M)·#{ordered pairs (c, c′) with d(c, c′) = i}, i = 0..n. Then A_0 = 1, A_i = 0 for 1 ≤ i < d, all A_i ≥ 0, and Σ_i A_i = M. The whole game is to bound Σ_i A_i.

**Krawtchouk polynomials, two faces.** For 0 ≤ k ≤ n,

K_k(i) = Σ_{j=0}^k (−1)^j·C(i, j)·C(n−i, k−j).

Polynomial face: a degree-k polynomial in i. Character face: if x ∈ {0,1}^n has |x| = i, then K_k(i) = Σ_{|y| = k} (−1)^{x·y} — the character χ_y(x) = (−1)^{x·y}, summed over all y of weight k. The two faces agree; the lab checks the identity for n = 5..8, every (i, k).

**Theorem (Delsarte inequalities).** For every code and every k: Σ_i A_i·K_k(i) ≥ 0.

*Proof.* Multiply by M and use the character face:

M·Σ_i A_iK_k(i) = Σ_{c,c′} K_k(d(c, c′)) = Σ_{c,c′} Σ_{|y|=k} (−1)^{(c⊕c′)·y}.

Now the parity move: |y ∩ (c⊕c′)| ≡ |y ∩ c| + |y ∩ c′| (mod 2), so (−1)^{(c⊕c′)·y} = (−1)^{c·y}·(−1)^{c′·y}, and every term factors:

Σ_{c,c′} K_k(d(c,c′)) = Σ_{|y|=k} (Σ_c (−1)^{c·y})² ≥ 0. ∎

A sum of *squares* — the polynomial method of Chapter 6's Lecture 3, with "vanishes on the other sets" replaced by "is a square when summed".

**Lemma (certificates).** Let F = Σ_k f_k·K_k with f_0 = 1, f_k ≥ 0, and suppose F(i) ≤ 0 for d ≤ i ≤ n. Then A(n,d) ≤ F(0).

*Proof.* Sum F over all ordered pairs of a code of size M. Lower bound — only the k = 0 square, using Delsarte's proof:

Σ_{c,c′} F(d(c,c′)) = Σ_k f_k·Σ_{|y|=k} (Σ_c (−1)^{c·y})² ≥ f_0·(Σ_c 1)² = M².

Upper bound — split the pairs: c = c′ contributes M·F(0), and c ≠ c′ contributes F(d(c,c′)) ≤ 0 since d(c,c′) ≥ d. Together M² ≤ M·F(0), i.e. M ≤ F(0). ∎

**Plotkin, one line.** F = 1 + K₁/(2d−n) (when 2d > n): since K₁(i) = n − 2i, F(i) = 2(d−i)/(2d−n) ≤ 0 for i ≥ d, so

A(n,d) ≤ F(0) = 2d/(2d−n) — Plotkin's bound as a single certificate. Machine check: all 29 parameter pairs with 2d > n and 2 ≤ n ≤ 10, valid.

**Four exact values.** Each certificate below was checked as an exact fraction, value by value:

| value | certificate F | sign check on [d, n] |
|-------|----------------|----------------------|
| **A(7,3) = 16** | 1 + K₁ + ⅓K₂ + K₇ | F(3) = F(4) = F(6) = F(7) = 0, F(5) = −8/3 |
| **A(7,4) = 8** | 1 + K₁ | F(i) = 8 − 2i: F(4) = 0, then −2, −4, −6 |
| **A(8,4) = 16** | 1 + K₁ + ¼K₂ | F(4) = F(8) = 0, F(5) = F(7) = −3/2, F(6) = −2 |
| **A(8,5) = 4** | 1 + ⅓K₁ + ⅓K₈ | F(5) = F(6) = 0, F(7) = F(8) = −4/3 |

And each is *attained*: the [7,4] Hamming code (16 words, min 3); the [7,3] simplex code — 8 words, every nonzero word of weight exactly 4, so all pairwise distances are 4; the [8,4] extended Hamming code (16 words, min 4); and for (8,5) the four-word code {00000000, 00011111, 11100011, 11111100}, pairwise distances 5, 5, 6, 6, 5, 5 — no third certificate needed, but note that the 4 here beats Plotkin's 5: the K₈ term earns a full code word.

**The [7,4] Hamming code, in full.** Distance distribution A = [1, 0, 0, 7, 7, 0, 0, 1] (ordered pair counts [16, 0, 0, 112, 112, 0, 0, 16]). Its eight Delsarte sums Σ_{c,c′}K_k(d):

**[256, 0, 0, 0, 1792, 0, 0, 0]** — six of the eight rows vanish.

Three of the six are demanded: the (7,3) certificate carries dual weight exactly on k = 1, 2, 7, so the squares Σ_c(−1)^{c·y} must vanish for every y of weight 1, 2, or 7 — complementary slackness, and the sums confirm it. The other three (k = 3, 5, 6) vanish unasked: the distribution is that rigid. And F vanishes at every realized distance (3, 4, 7), so equality M = F(0) = 16 holds with all slack closed.

**The linear program, solved exactly.** A code's distance distribution is a feasible point of: maximize Σ_{i≥d} x_i subject to x_0 = 1, x_i = 0 for 1 ≤ i ≤ d−1, x_i ≥ 0, and Σ_i x_iK_k(i) ≥ 0 for all k. So A(n,d) ≤ 1 + LP maximum. The lab solves all sixteen instances (n, d) below in exact rational arithmetic — vertex enumeration with BigInt fractions, primal and dual both, 16 of 16 matching:

| n \ d | 2 | 3 | 4 | 5 |
|:------|:--|:--|:--|:--|
| **4** | 8 | 8/3 | 2 | — |
| **5** | 16 | 4 | 8/3 | 2 |
| **6** | 32 | 8 | 4 | 12/5 |
| **7** | — | 16 | 8 | — |
| **8** | — | 128/5 | 16 | 4 |

**Honesty: (8,3).** The LP bound is 128/5 = 25.6, and here the program is genuinely loose: the truth is A(8,3) = 20 (shortened Hamming code; cited). The LP optimum is what it is — no certificate in this framework can say more — and the gap is the honest signature of what the method cannot do.

**The brute table, certified.** For n ≤ 6, exhaustive search closes every gap the LP leaves: A(4,2)=8, A(4,3)=2, A(4,4)=2, A(5,2)=16, A(5,3)=4, A(5,4)=2, A(5,5)=2, A(6,2)=32, A(6,3)=8, A(6,4)=4, A(6,5)=2. Eight match the LP bound exactly; the three where the LP is fractional — (4,3), (5,4), (6,5) with bounds 8/3, 8/3, 12/5 — come out at 2, with attaining pairs and no third word.

**What you now own:** the polynomial method's third face — Chapter 6's Lectures 1–3 made polynomials *vanish*; Delsarte makes them *sum to squares*. The certificate habit (guess a short Krawtchouk combination, check signs, read off F(0)) and its dual, the attaining code; the LP that automates the guessing; and the Atlas's arc closed — Fisher's dimension counting, Oddtown's field arithmetic, the polynomial method, the spectrum, and now the semidefinite and linear programs, all one machine pointed at different cubes.

---

## The Trick Bag (reference card)

| Pattern | Plain language | Where you met it |
|---------|---------------|------------------|
| **P21 Spectral / Rayleigh** | λ1 ≥ 2m/n from the average; structure caps λ1; operator norm μ on 𝟙⊥ prices pseudorandomness; the smallest eigenvalue prices independence and chromatic number | L1, L2, L4 |
| **P20 Weight shifting** | Merge weight into better-connected vertices; the support shrinks to a clique at no cost, and adjacent merges pay their x_v² correction | L2 |
| **P19 Rank / dimension** | Centered Gram and evaluation matrices; rank bounded above by ambient dimension and below by independence | L3 |
| **P22 Polynomial method** | One polynomial per point, vanishing on the others; the paraboloid lift, the sphere discount, and Krawtchouk combinations as certificates | L3, L4 |
| **Center before counting (lore)** | Subtract the mean; the centered Gram carries the true rank (k − 1, not k) | L3 |
| **Test parameters for degeneracy (lore)** | A construction whose forbidden values never occur proves nothing (the K₂₁ non-example) | Ch. 6 (its L3) |
| **Compress before you bound (lore)** | Restrict the matrix to a subspace or partition first: interlacing makes every such restriction honest, and equitable quotients give exact eigenvalues | L4 |
| **Distribute, then average (lore)** | Sum a quantity over all pairs before bounding it: character sums come out as squares, distance distributions as feasible points | L4 |

**Formula box:** Rayleigh: λ1 ≥ 2m/n; triangle-free λ1 ≤ √m; Mantel m ≤ ⌊n²/4⌋ spectrally. Expander-mixing: |e(S,T) − d·|S||T|/n| ≤ μ·√(|S||T|(1 − |S|/n)(1 − |T|/n)) — Petersen μ = 2, K_{3,3} μ = 3 (the −d bipartite degeneracy). Motzkin–Straus: simplex max = (1 − 1/ω)/2; adjacent merges pay x_v²; spectral Turán λ1 ≤ (1 − 1/ω)n, Turán m ≤ (1 − 1/r)n²/2. Two-distance: equidistant k ≤ d + 1 (centered Gram rank k − 1); s-distance k ≤ C(d+s+1, s) proved, C(d+s, s) sharp (cited); spherical DGS d(d+3)/2 at s = 2; witnesses — pentagon {1.38197, 3.61803} (spherical tight at d = 2), octahedron {2, 4}, {0, 1, 2} non-spherical; Larman–Rogers–Seidel integrality beyond 2d + 3 points (cited, flagged). Interlacing: λ_i ≥ μ_i ≥ λ_{i+n−m}; inertia α ≤ n − p(A) and α ≤ n − q(A); equitable quotient spectra sit inside the full spectrum; Hoffman α ≤ n(−λ_n)/(d − λ_n) and χ ≥ 1 + d/|λ_n|. Theta: sandwich α ≤ θ(G) ≤ χ(Ḡ), θ(C₅) = √5, Θ(C₅) = √5 (multiplicativity cited). Delsarte: M² ≤ Σ_{c,c′} F ≤ M·F(0) for certificates with f_0 = 1; Plotkin A(n,d) ≤ 2d/(2d−n); LP-exact A(7,3) = 16, A(7,4) = 8, A(8,4) = 16, A(8,5) = 4; the honest (8,3): LP 128/5 against the cited truth A(8,3) = 20.

---

## Exercises (graded: ●○○ easy · ●●○ moderate · ●●● tough)

**Easy — one idea, applied directly**

1. ●○○ **The bipartite eigenvalue.** Prove λ1(K_{a,b}) = √(ab) by exhibiting the eigenvector, and verify the tightness discussion of L1.1: which of the two sandwich lemmas does it make tight, and exactly when? *Hint: √b on one side, √a on the other; compare 2ab/(a+b) with √(ab).*

**Moderate — two ideas, or one tricky step**

2. ●●○ **Equidistant points.** Prove that at most d + 1 points of R^d can be pairwise equidistant, and exhibit d + 1 that are. *Hint: P19 — center first; the spectrum of (δ²/2)(I − J/k).*

**Tough — several chapter ideas combined**

3. ●●● **The spectral Turán chain.** Prove λ1 ≤ (1 − 1/ω)n, then recover Turán's theorem m ≤ (1 − 1/r)n²/2 from it. *Hint: Perron vector → simplex → Motzkin–Straus → Cauchy–Schwarz; then Rayleigh.*

**From Lecture 4 — the modern toolkit**

4. ●●○ **The inertia bound, both sides.** Prove α(G) ≤ n − p(A) and α(G) ≤ n − q(A), and evaluate both on the Petersen graph and on C₅ — each is tight on one side. Then read the census: over all 1,099 graphs with n ≤ 5, the bound is never violated; which side is tight more often, and can you see why? *Hint: §4.1 — interlacing reads the all-zero principal block twice.*

5. ●●○ **Hoffman's tight cases.** Verify Hoffman's bound and its equality conditions on the Petersen graph (α = 4; the five stars), the cocktail party K₆ ∖ 3K₂ (α = 2), and K_{a,a} (α = a). For a Petersen star S, compute the three inner products ⟨𝟙_S, 𝟙_S⟩_M = 8, ⟨𝟙_S, 𝟙⟩_M = 20, ⟨𝟙, 𝟙⟩_M = 50 and confirm 8·50 = 20²; then explain the equality via M𝟙_S = 2𝟙 and M𝟙 = 5𝟙. *Hint: M = A − λ_n·I = A + 2I.*

6. ●●● **Two proofs of the chromatic bound.** Prove χ ≥ 1 + d/|λ_n| twice: through the n/α chain, and directly, by compressing to the color-class span (tr B = 0, then μ_1 = d, then Σ_{i≥2}μ_i = −d ≥ (k−1)λ_n). Which proof assumes less, and where exactly does each spend the hypothesis d-regular? *Hint: §4.2 — the direct proof never mentions an independent set.*

**Pattern unknown — you choose the tool** *No hints, no difficulty rating: diagnosing the problem is part of the problem. Worked answers still wait at the end.*

7. ◆ Codes and their certificates: show A(5,3) = 4 and A(8,5) = 4, each with a Krawtchouk combination certifying the upper bound *and* a code attaining it.

**Explorations — ◐ research-style training** *No single right answer — what you should find is described in each.*

8. ◐ **Two-distance sets under lattice discipline.** Extend the lab's grid censuses: larger square grids, rectangular windows, the 4×4×4 cube. Is any 2D lattice two-distance set larger than 4 ever found? Where exactly does the pentagon fail — try the triangular lattice too, and formulate a conjecture about which optimal configurations are lattice-realizable (the octahedron is; the pentagon is not).

9. ◐ **The capacity of the pentagon, pushed.** The lab checks α(C₅ ⊠ C₅) = 5 exhaustively; with theta's multiplicativity (cited), Θ(C₅) = √5 follows. Push on to C₅ ⊠ C₅ ⊠ C₅, where the sandwich pins 10 ≤ α ≤ 11 — which is it? Find a certificate or a smarter search than brute force. Then try the umbrella on C₇: what goes wrong, and what *is* θ(C₇)?

**Graded backfill — five more, each hint naming its pattern**

10. ●○○ **Triangles from the spectrum.** Prove that the number of triangles t(G) equals tr(A³)/6, and then — since tr(A³) = Σᵢλᵢ³ — that the triangle count is a function of the spectrum alone. Compute t both ways for K₄, the paw, the diamond K₄ ∖ e, C₅, K_{3,3}, and the Petersen graph. Then the lesson K_{3,3} teaches: λ1 = 3 is as large as six vertices allow, yet t = 0 — what cancels, and why can no single eigenvalue see triangles? *Hint: P2 — count closed walks of length 3 through their middle vertex; then expand A³ in the eigenbasis (P21).*

11. ●●○ **The spectral triangle threshold.** Prove: a d-regular triangle-free graph on n vertices with at least one edge has μ ≥ d²/(n−d), with equality for every K_{d,d}. Restated: a triangle-free graph cannot be too pseudorandom — and if μ < d²/(n−d), triangles must exist. Run the census: every d-regular triangle-free graph with n ≤ 6, plus C₇ and the Petersen graph; zero violations, and which graphs attain equality? *Hint: P21 + P2 — set tr(A³) = 0, bound Σ_{i≥2}λ_i³ from below by λ_n·Σ_{i≥2}λ_i², and spend the identity Σ_{i≥2}λ_i² = d(n−d).*

12. ●●○ **Wilf's bound: the other end of the chromatic sandwich.** Hoffman bounds χ from below (Exercise 6); Wilf bounds it from above: χ(G) ≤ 1 + ⌊λ1⌋. Prove it — every induced subgraph has a vertex of degree at most λ1(G) — and then run the census: all 33,866 graphs with n ≤ 6, zero violations, 23,887 tight. On the Petersen graph, Wilf says only 4; on C₅, show that Hoffman and Wilf together pin χ = 3 exactly. Among the regular graphs of the census, how many does the sandwich pin? *Hint: P21 — the average degree of any induced H is a Rayleigh quotient of A_H, and λ1(H) ≤ λ1(G) by interlacing (§4.1); the greedy spends the rest.*

13. ●●○ **When Plotkin is attained.** Analyze equality in the certificate lemma's proof, for Plotkin's certificate F = 1 + K₁/(2d−n): show that a code attaining A(n,d) = 2d/(2d−n) must be *equidistant* — every pair at distance exactly d — and balanced on every coordinate (Σ_c(−1)^{c_j} = 0 for each position j). Then: build a four-word code attaining A(6,4) = 4 (the brute table's row, closed by construction); check the [7,3] simplex code against the same analysis at A(7,4) = 8; and confirm that the chapter's (8,5) code, which *beats* Plotkin, is not equidistant — exactly as the analysis demands. *Hint: P22 — re-read the lemma's proof and name the slack budgets: the k ≥ 1 squares, the cross terms F(d(c,c′)), and where F vanishes.*

14. ●●● **The Petersen graph is the Kneser graph K(5,2).** Take the ten 2-subsets of [5] as vertices, joining two when they are *disjoint*. (i) Count the edges two ways and check the graph is 3-regular. (ii) Exhibit an explicit isomorphism with the Petersen graph — outer cycle {01, 23, 40, 12, 34}, inner pentagram {24, 14, 13, 03, 02}, spokes included — and verify all 15 edges and all 30 non-edges. (iii) The independent sets of size 4 are exactly the stars: prove α = 4 by the EKR argument at (5,2) — the range n > 2k where Chapter 7 proved uniqueness — and confirm the five stars are the only maximum independent sets. (iv) Color the ten pairs with three intersecting classes — star, star, triangle — and conclude χ = 3 = n − 2k + 2 (the case k = 1 is the complete graph; Lovász's Kneser theorem for general (n, k) is cited, not proved here). (v) Where does Hoffman's bound land (Exercise 5), and which extremal fact does it certify? *Hint: P9 — two disjoint 2-subsets miss exactly one point of [5]; then P21's certificate; Chapter 7's Lecture 3 owns the stars.*

---

## Answers to the Exercises

**A1.** The vector x with x_u = √b on the A-side and x_v = √a on the B-side is an eigenvector: for u ∈ A, (Ax)_u = Σ_{v~u} x_v = b√a = √(ab)·√b = √(ab)·x_u, and symmetrically on B. So λ1 = √(ab) (Perron–Frobenius: entrywise-nonnegative eigenvectors belong to λ1). Against L1: m = ab, so Lemma 2 (λ1 ≤ √m) is tight for **every** complete bipartite graph; Lemma 1 (λ1 ≥ 2m/n) is tight iff 2ab/(a+b) = √(ab) ⟺ (a−b)² = 0, i.e. a = b. The sandwich thus singles out the balanced case a = b = n/2 for even n directly, and for odd n integrality m ≤ ⌊n²/4⌋ selects K_{⌊n/2⌋,⌈n/2⌉}.

**A2.** Center: w_i = p_i − mean, Σw_i = 0. Summing ||w_i − w_j||² over j gives (k−1)δ² = k||w_i||² + Σ_j||w_j||², and summing over i gives k(k−1)δ² = 2kΣ_j||w_j||², whence ||w_i||² = (k−1)δ²/(2k), w_i·w_j = −δ²/(2k) for i ≠ j, and G = (δ²/2)(I − J/k) — spectrum {δ²/2 × (k−1), 0}, rank k − 1 (the 𝟙 direction is killed by centering). Since G = WWᵀ with W of k rows in R^d: k − 1 = rank G = rank W ≤ d, so k ≤ d + 1. Attainment: the standard simplex w_i = e_i − 𝟙/k in the hyperplane Σx = 0 ⊂ R^k (dimension k − 1 = d): pairwise distance² = 2, norms² = (k−1)/k — d + 1 equidistant points in R^d. Machine check: the centered Gram's spectrum {1 × (k−1), 0} and the simplex data verified for k = 2 … 9.

**A3.** Let x be a unit Perron vector of a component carrying λ1 (entrywise ≥ 0; for disconnected G the component argument applies verbatim, and if E = ∅ then λ1 = 0 = (1−1/1)n). With s = Σx_v > 0: λ1 = xᵀAx = 2Σ_{uv∈E}x_ux_v = 2s²·f(x/s), and Motzkin–Straus caps f(x/s) at (1−1/ω)/2; Cauchy–Schwarz caps s² ≤ n||x||² = n. Chained: λ1 ≤ (1 − 1/ω)n. Rayleigh (L1.1) then gives m ≤ nλ1/2 ≤ (1 − 1/ω)n²/2; for K_{r+1}-free graphs ω ≤ r, so m ≤ (1 − 1/r)n²/2: Turán. Machine check: all 33,792 graphs on 5 and 6 vertices satisfy λ1 ≤ (1−1/ω)n; K_{3,3} has λ1 = 3 = (1 − 1/2)·6 — equality.

**A4.** An independent S of size α makes the principal submatrix A_S the zero matrix: α eigenvalues μ, all equal 0. Interlacing reads this twice: μ_α = 0 with μ_i ≤ λ_i gives λ_α ≥ 0 — at least α eigenvalues are nonnegative, α ≤ p + z; and μ_1 = 0 with μ_i ≥ λ_{i+n−α} gives λ_{1+n−α} ≤ 0 — at least α are nonpositive, α ≤ q + z (z = zero count). Since p + z = n − q and q + z = n − p: **α ≤ n − q and α ≤ n − p**. Petersen {3, 1⁵, −2⁴}: p = 6, q = 4 — n − p = 4 = α, tight (the n − q side says 6, slack). C₅ {2, 0.618², −1.618²}: p = 3, q = 2 — n − p = 2 = α, tight. Census (all 1,099 graphs with n ≤ 5, Part 3(a)): **zero violations on either side**; the n − p reading is tight 633 times, the n − q reading 954 — the weaker of the two bounds is met more often, as it should be — and the honest combined bound α ≤ min(n−p, n−q) is tight 966 times. The two sides agree exactly when p = q, in particular for every graph whose components are all bipartite.

**A5.** Petersen (d = 3, λ_n = −2): the bound is 10·2/5 = 4 = α — tight, witnesses the five stars. With M = A + 2I, each star S gives ⟨𝟙_S, 𝟙_S⟩_M = 8, ⟨𝟙_S, 𝟙⟩_M = 20, ⟨𝟙, 𝟙⟩_M = 50, and 8·50 = 400 = 20² — equality in Cauchy–Schwarz, explained by M𝟙_S = 2𝟙 and M𝟙 = 5𝟙 (so 𝟙_S − (2/5)𝟙 is M-null, exactly what equality in a degenerate Cauchy–Schwarz demands). Cocktail party K₆ ∖ 3K₂ (d = 4, spectrum {4, 0³, −2²}): bound 6·2/6 = 2 = α, tight — the three deleted pairs — and χ ≥ 1 + 4/2 = 3, exact. K_{a,a} (spectrum {a, 0^{2a−2}, −a}): bound 2a·a/(a+a) = a = α — structural equality: Hoffman certifies exactly the bipartition. Machine check: Part 3(b) — 1,122 d-regular graphs with λ_n < 0, zero violations, 225 tight; the star inner products print `8 20 50 True` five times.

**A6.** *Proof 1.* The χ color classes partition V into independent sets, so χα ≥ n; feeding in Hoffman's α ≤ n|λ_n|/(d+|λ_n|): χ ≥ n/α ≥ (d+|λ_n|)/|λ_n| = 1 + d/|λ_n|. *Proof 2.* Compress A to the span of the orthonormalized class indicators: tr B = 0 (each class independent), Rayleigh on w = (√|C_i|)_i gives μ_1 ≥ d while interlacing gives μ_1 ≤ λ_1 = d — so μ_1 = d — and the remaining k − 1 eigenvalues sum to −d with each ≥ λ_n: −d ≥ (k−1)λ_n, i.e. k ≥ 1 + d/|λ_n|. The hypotheses are the same (d-regular, λ_n < 0), but the spending differs: Proof 1 routes through α and inherits regularity from Hoffman's proof; Proof 2 spends regularity directly (𝟙ᵀA𝟙 = nd and λ_1 = d) and never mentions an independent set. Machine check: Part 3(e) — all 191 d-regular graphs with n = 4..6, zero violations, and Proof 2's chain (tr B = 0, μ_1 = d, Σ_{i≥2}μ_i = −d ≥ (k−1)λ_n) verified coloring by coloring.

**A◆7.** *A(5,3) = 4.* Certificate F = 1 + ½K₁ + ½K₅ (f_0 = 1, f_1 = f_5 = ½, all ≥ 0): F(0) = 1 + 5/2 + 1/2 = **4**; on [3, 5]: F(3) = 1 + ½(5−6) + ½(−1) = 0, F(4) = 1 + ½(−3) + ½(+1) = 0, F(5) = 1 + ½(−5) + ½(−1) = −2. So A(5,3) ≤ 4, and the code {00000, 11100, 10011, 01111} attains it: closed under xor (11100 ⊕ 10011 = 01111), weights 3, 3, 4, pairwise distances 3, 3, 4 — minimum 3. *A(8,5) = 4.* Certificate F = 1 + ⅓K₁ + ⅓K₈: F(0) = 1 + 8/3 + 1/3 = **4**; on [5, 8]: F(5) = 1 + ⅓(−2) + ⅓(−1) = 0, F(6) = 1 + ⅓(−4) + ⅓(+1) = 0, F(7) = 1 + ⅓(−6) + ⅓(−1) = −4/3, F(8) = 1 + ⅓(−8) + ⅓(+1) = −4/3. The code {00000000, 00011111, 11100011, 11111100} attains it — pairwise distances 5, 5, 6, 6, 5, 5, minimum 5. Note Plotkin alone caps A(8,5) at 2d/(2d−n) = 5: the K₈ term is what closes 5 to 4. Machine check: both certificates verified as exact fractions, and both values agree with the LP optima (Part 3(f) prints `(5,3) 4` and `(8,5) 4`).

**A10.** A closed walk of length 3 is a triangle traversed from a chosen start vertex in a chosen direction: every triangle contributes 3 · 2 = 6 walks, and (A³)_{vv} counts the length-3 closed walks starting at v. So tr(A³) = Σ_v(A³)_{vv} = 6t. And tr(A³) = Σᵢλᵢ³, since A = QΛQᵀ makes A³ = QΛ³Qᵀ — the triangle count is a symmetric function of the spectrum, readable without ever looking at the edges. Machine check, three engines agreeing on all six graphs: K₄ → 4, the paw → 1, the diamond → 2, C₅ → 0, K_{3,3} → 0, Petersen → 0; direct triangle count, tr(A³)/6, and Σᵢλᵢ³/6 identical throughout. K_{3,3}'s spectrum is {3, 0⁴, −3}: Σᵢλᵢ³ = 27 − 27 = 0. The cube is an odd function, so the +3 and the −3 cancel — bipartiteness pairs every eigenvalue with its negation, and the pairing kills the count. That is the moral: no single eigenvalue sees triangles; the sum of cubes does. Exercise 11 spends exactly this identity.

**A11.** First λ_n < 0: if all eigenvalues were ≥ 0, then tr(A³) ≥ d³ > 0 would force a triangle. For i ≥ 2: if λ_i ≥ 0 then λ_i³ ≥ 0 ≥ λ_n·λ_i²; if λ_i < 0 then λ_i ≥ λ_n gives λ_i³ = λ_i·λ_i² ≥ λ_n·λ_i². Either way λ_i³ ≥ λ_n·λ_i², so 0 = tr(A³) = d³ + Σ_{i≥2}λ_i³ ≥ d³ + λ_n·Σ_{i≥2}λ_i² — and Σ_{i≥2}λ_i² = tr(A²) − d² = 2m − d² = d(n−d), the same bookkeeping that priced K_{3,3}'s degeneracy in the formula box. Hence 0 ≥ d³ + λ_n·d(n−d), i.e. |λ_n| ≥ d²/(n−d), and μ ≥ |λ_n| closes the claim. Equality: K_{d,d} has spectrum {d, 0^{2d−2}, −d}, so μ = d = d²/(2d−d) — attained for every d, and these are the only attainers the census finds. Machine check: all 104 d-regular triangle-free graphs with n ≤ 6 (by class — n = 2, d = 1: one; n = 4: three at d = 1, three at d = 2; n = 5, d = 2: twelve; n = 6: fifteen at d = 1, sixty at d = 2, ten at d = 3), zero violations; equality μ = d²/(n−d) exactly on the 14 complete bipartite labelings (K₂ once, the three labeled C₄ = K₂,₂, the ten labeled K₃,₃). The strict witnesses: C₅ (μ = 2cos(π/5) = φ ≈ 1.618 against 4/3), C₆ (μ = 2 against 1), C₇ (μ = 2cos(π/7) ≈ 1.802 against 4/5), the Petersen graph (μ = 2 against 9/7). Read inversely, the theorem is a triangle detector: μ < d²/(n−d) certifies triangles without exhibiting one.

**A12.** For any nonempty induced H: its average degree is a Rayleigh quotient, avgdeg(H) = 𝟙ᵀA_H𝟙/|H| ≤ λ1(H), and λ1(H) ≤ λ1(G) because A_H is a principal submatrix of A_G — interlacing, §4.1. Since H was arbitrary, every induced subgraph has a vertex of degree ≤ ⌊λ1(G)⌋. Peel: repeatedly delete such a vertex; the deletion order leaves every vertex adjacent to at most ⌊λ1(G)⌋ later vertices, so coloring in reverse order uses at most 1 + ⌊λ1(G)⌋ colors — Wilf's bound, the greedy made spectral. Machine check: all 33,866 graphs with n = 2..6, exact eigenvalues — zero violations, 23,887 tight (2 + 8 + 61 + 909 + 22,907 by n), including every complete graph and every odd cycle (λ1(C₅) = 2, χ = 1 + ⌊2⌋ = 3) and non-integer cases like the paw (χ = 3, λ1 ≈ 2.17). The Petersen graph: λ1 = 3 gives χ ≤ 4 — honest slack against χ = 3, and Hoffman's end says only χ ≥ 3: the spectrum leaves [3, 4], the sandwich does not pin Petersen. On C₅ the two ends meet: Hoffman gives χ ≥ 1 + 2/1.618… = 2.236 → 3, Wilf gives χ ≤ 3 — χ = 3 from the spectrum alone. Census of the pinch: of the 193 regular graphs with n ≤ 6 (d ≥ 1, λ_n < 0), Hoffman and Wilf pin χ exactly on 45. (Honesty note, recorded in the appendix: a first census pass using an iterative eigenvalue estimate produced 81 spurious violations at integer boundaries; the exact computation removes all of them.)

**A13.** The lemma's ledger: M² ≤ Σ_{c,c′}F(d(c,c′)) = M·F(0) + Σ_{c≠c′}F(d(c,c′)). If M = F(0) — Plotkin attained — then Σ_{c≠c′}F(d(c,c′)) = 0 with every term ≤ 0, so every term vanishes. For F = 1 + K₁/(2d−n), F(i) = 2(d−i)/(2d−n), which vanishes only at i = d: every pair of codewords sits at distance exactly d — the code is equidistant. The second budget: the proof's lower bound kept only the k = 0 square, so at equality every k ≥ 1 square with f_k > 0 must vanish; Plotkin has f_1 = 1/(2d−n) > 0, so Σ_c(−1)^{c·y} = 0 for every y of weight 1: each coordinate carries as many 0s as 1s — balanced. The (6,4) code: {000000, 111100, 110011, 001111} — all six pairwise distances exactly 4, every coordinate balanced (two 0s, two 1s), so A(6,4) = 4 = 2·4/(8−6): the brute table's row, attained, with both equality signatures present. The [7,3] simplex code: all 28 pairwise distances exactly 4, every nonzero word of weight 4, all seven coordinates balanced — A(7,4) = 8 = 2·4/(8−7) with the same signatures. And the chapter's (8,5) code — distances 5, 5, 6, 6, 5, 5 — beats Plotkin (4 < 5) precisely by not being equidistant; likewise the (5,3) code (distances 3, 3, 4) needed the K₅ term beyond Plotkin's 6. The analysis is one-directional on purpose: attainment forces equidistance; slack is where irregular distance profiles live. Machine check: all pairwise distances and all coordinate balances computed for all four codes; Plotkin's arithmetic 4, 8, 5, 6 exact.

**A14.** (i) Each 2-subset is disjoint from exactly the C(3,2) = 3 pairs inside its 3-point complement: 10 · 3 directed counts, 15 edges — and the same count per vertex says 3-regular. (ii) The labeling, in the Petersen's conventions (outer cycle u_0…u_4, inner pentagram v_0…v_4 with v_i ~ v_{i+2}, spokes u_i ~ v_i): u = ({0,1}, {2,3}, {4,0}, {1,2}, {3,4}), v = ({2,4}, {1,4}, {1,3}, {0,3}, {0,2}). Spot checks: outer edge {0,1}–{2,3} (disjoint); pentagram edge {2,4}–{1,3} (disjoint); spoke {0,1}–{2,4} (disjoint); non-edge {0,1}–{0,2} (they share 0, and indeed u_0's only inner neighbor is v_0). Machine check: all 15 edges and all 30 non-edges verified under this single bijection, zero mismatches — K(5,2) is the Petersen graph, spectrum {3, 1⁵, −2⁴} and all. (iii) Independent = intersecting, since adjacency is disjointness. If all members share a point x, the family sits inside the star at x — at most the four pairs through x, with equality exactly at the star. If not, pick A = {p,q}, B = {p,r} sharing only p; every further member must meet both, so it contains p, or is {q,r}; the members containing p are A, B and the two pairs {p,s} beyond them, and any three of them would share p — while {q,r} excludes every {p,s}. A common-point-free family therefore has at most three members, {A, B, {q,r}}. So α = 4, with the five stars the only attainers — Chapter 7's EKR with its uniqueness theorem, at (5,2) in the proved range n > 2k. Machine census: all 1,023 nonempty families — maximum 4, exactly five attainers, each a star. (iv) The classes {12, 13, 14, 15} (star at 1), {23, 24, 25} (star at 2 without 12), {34, 35, 45} (triangle on {3,4,5}) — each pairwise intersecting, so independent in K(5,2), and together all ten pairs: χ ≤ 3. And χ ≥ 3, because {01, 23, 40, 12, 34} is a 5-cycle. So χ(K(5,2)) = 3 = 5 − 2·2 + 2; k = 1 gives the complete graph, and Lovász's Kneser theorem χ(K(n,k)) = n − 2k + 2 in general is cited, not proved here. (v) Hoffman: α ≤ 10·2/5 = 4 — the spectral bound certifies the EKR number exactly, with equality through the degenerate Cauchy–Schwarz that Exercise 5 walked. One number, three witnesses: the combinatorial count, the spectral certificate, and the census.

---

## Computational Lab (verified)

### Part 1 — Jacobi eigenvalues, expander-mixing ratios, the spectral censuses, and the Motzkin–Straus detector

```python
from itertools import combinations
from math import sqrt

def jacobi(A, sweeps=100):            # cyclic Jacobi: eigenvalues, descending
    n = len(A)
    if n == 0: return []
    A = [row[:] for row in A]
    for _ in range(sweeps):
        off = sqrt(sum(A[i][j]**2 for i in range(n) for j in range(n) if i != j))
        if off < 1e-11: break
        for p in range(n-1):
            for q in range(p+1, n):
                if abs(A[p][q]) < 1e-13: continue
                th = (A[q][q] - A[p][p]) / (2*A[p][q])
                t = (1 if th >= 0 else -1) / (abs(th) + sqrt(th*th + 1))
                c = 1/sqrt(t*t + 1); s = t*c
                for k in range(n):
                    akp, akq = A[k][p], A[k][q]
                    A[k][p], A[k][q] = c*akp - s*akq, s*akp + c*akq
                for k in range(n):
                    apk, aqk = A[p][k], A[q][k]
                    A[p][k], A[q][k] = c*apk - s*aqk, s*apk + c*aqk
    return sorted((A[i][i] for i in range(n)), reverse=True)

def adjacency(n, edges):
    adj = [0]*n
    for u, v in edges:
        adj[u] |= 1 << v; adj[v] |= 1 << u
    return [[1 if adj[u] >> v & 1 else 0 for v in range(n)] for u in range(n)]

petersen = adjacency(10, [(i, (i+1) % 5) for i in range(5)] +
                          [(5+i, 5 + (i+2) % 5) for i in range(5)] +
                          [(i, i+5) for i in range(5)])
c5_mat = adjacency(5, [(i, (i+1) % 5) for i in range(5)])
k33_mat = adjacency(6, [(a, 3+b) for a in range(3) for b in range(3)])
for name, A in [("K23", adjacency(5, [(a, 2+b) for a in range(2) for b in range(3)])),
               ("C5", c5_mat), ("Petersen", petersen), ("K33", k33_mat),
               ("W2", adjacency(5, [(0,1),(0,2),(0,3),(0,4),(1,2),(3,4)])),
               ("W3", adjacency(7, [(0,i) for i in range(1,7)] +
                                    [(1,2),(3,4),(5,6)]))]:
    print(name, [round(x, 4) for x in jacobi(A)])

def max_eml_ratio(A):                 # max expander-mixing ratio over disjoint S, T
    n = len(A); d = sum(A[0]); best = 0.0
    for s_mask in range(1, (1 << n) - 1):
        s = bin(s_mask).count("1")
        comp = ((1 << n) - 1) ^ s_mask
        t_mask = comp
        while t_mask:
            t = bin(t_mask).count("1")
            e_st = sum(A[u][v] for u in range(n) if s_mask >> u & 1
                               for v in range(n) if t_mask >> v & 1)
            denom = sqrt(s * t * (1 - s/n) * (1 - t/n))
            best = max(best, abs(e_st - d*s*t/n) / denom)
            t_mask = (t_mask - 1) & comp
    return round(best, 4)

print("EML max ratios:", max_eml_ratio(petersen), max_eml_ratio(k33_mat), max_eml_ratio(c5_mat))
# EML max ratios: 2.0 3.0 1.3333

def clique_num(adj, n):
    for k in range(n, 0, -1):
        if any(all(adj[u] >> v & 1 for u, v in combinations(C, 2))
               for C in combinations(range(n), k)):
            return k
    return 0

tot_56 = viol_mantel = viol_turan = 0
for n in (5, 6):
    pairs = list(combinations(range(n), 2))
    for mask in range(1 << len(pairs)):
        adj = [0]*n; m = mask.bit_count()
        for k, (u, v) in enumerate(pairs):
            if mask >> k & 1: adj[u] |= 1 << v; adj[v] |= 1 << u
        A = [[1 if adj[i] >> j & 1 else 0 for j in range(n)] for i in range(n)]
        lam1 = jacobi(A)[0]; om = clique_num(adj, n)
        tot_56 += 1
        viol_turan += (lam1 < 2*m/n - 1e-7) or (lam1 > (1 - 1/om)*n + 1e-7)
        if om <= 2:
            viol_mantel += (lam1 > sqrt(m) + 1e-7) or (m > (n*n)//4)
print("census n=5,6:", tot_56, viol_mantel, viol_turan)
# census n=5,6: 33792 0 0
```

**Verified output (eigenvalues, mixing ratios, and censuses).** K_{2,3}: {√6, 0, 0, 0, −√6} = {2.4495, 0, 0, 0, −2.4495}. C₅: {2, 0.618, 0.618, −1.618, −1.618}. Petersen: {3, 1, 1, 1, 1, 1, −2, −2, −2, −2}. K_{3,3}: {3, 0, 0, 0, 0, −3} — the −d eigenvalue of L1.2's bipartite degeneracy. W₂: {(1+√17)/2, 1, −1, −1, (1−√17)/2} ≈ {2.5616, 1, −1, −1, −1.5616}. W₃: {3, 1, 1, −1, −1, −1, −2} — all six match Chapter 6's §4.5, L1, and the lab's theory lines. `EML max ratios: 2.0 3.0 1.3333` — tight on Petersen (μ = 2) and K_{3,3} (μ = 3), and 4/3 < φ on C₅. `census n=5,6: 33792 0 0` — zero violations of Rayleigh, spectral Mantel, or spectral Turán across all 33,792 graphs on 5 and 6 vertices.

The same Jacobi routine drives the two censuses. **Spectral Mantel and Turán sweep** (all graphs on 5 and 6 vertices — 1,024 + 32,768 = 33,792 of them): triangle-free graphs satisfy λ1 ≤ √m and every graph satisfies λ1 ≥ 2m/n, λ1 ≤ (1 − 1/ω)n and m ≤ ⌊n²/4⌋ — zero violations; K_{3,3} attains spectral Turán equality, λ1 = 3. **Motzkin–Straus detector** (all 64 graphs on 4 vertices, f evaluated on the 1/40 simplex mesh — all 12,341 lattice points; then all 1,024 graphs on 5 vertices on a 1/10 mesh plus 200 random points each): the simplex maximum never exceeds (1 − 1/ω)/2 on any graph, and exactly **42** of the 64 attain it (empty graph, the 40 triangle-free graphs with an edge, and K₄ — the integrality explanation is in §2.2). Detector:

```python
def ms_max(edges, grid):              # grid: list of simplex lattice points
    return max((sum(x[u]*x[v] for u, v in edges) for x in grid), default=0.0)

mesh40 = [(a/40, b/40, c/40, 1 - (a+b+c)/40)
          for a in range(41) for b in range(41 - a) for c in range(41 - a - b)]
pairs4 = list(combinations(range(4), 2))
ms_viol = ms_tight = 0
for mask in range(1 << 6):
    edges = [pairs4[k] for k in range(6) if mask >> k & 1]
    adj = [0]*4
    for u, v in edges: adj[u] |= 1 << v; adj[v] |= 1 << u
    om = clique_num(adj, 4)
    val = ms_max(edges, mesh40); bound = (1 - 1/om)/2
    ms_viol += val > bound + 1e-9
    ms_tight += abs(val - bound) < 1e-9
print("MS n=4:", len(mesh40), ms_viol, ms_tight)
# MS n=4: 12341 0 42
```

### Part 2 — Two-distance sets: Gram spectra, polynomial dimensions, and exhaustive grid censuses

```python
from itertools import combinations
from math import comb, cos, sin, pi
from fractions import Fraction as Fr

def sqdist(p, q): return sum((a - b)**2 for a, b in zip(p, q))

def det_frac(M):                      # exact rational determinant
    n = len(M)
    if n == 0: return Fr(1)
    A = [[Fr(x) for x in row] for row in M]
    sign = Fr(1)
    for c in range(n):
        p = next((r for r in range(c, n) if A[r][c] != 0), None)
        if p is None: return Fr(0)
        if p != c: A[c], A[p] = A[p], A[c]; sign = -sign
        for r in range(c+1, n):
            factor = A[r][c] / A[c][c]
            for j in range(c, n): A[r][j] -= factor * A[c][j]
    ans = sign
    for i in range(n): ans *= A[i][i]
    return ans

# Centered Gram spectrum & simplex norms, plus det(J_k + I_k) = k + 1 for k = 2..9
gram_ok = det_ok = True
for k in range(2, 10):
    W = [[(1 if j == i else 0) - Fr(1, k) for j in range(k)] for i in range(k)]
    G = [[sum(W[i][r]*W[j][r] for r in range(k)) for j in range(k)] for i in range(k)]
    gram_ok &= all(G[i][i] == Fr(k-1, k) for i in range(k))
    gram_ok &= all(G[i][j] == Fr(-1, k) for i in range(k) for j in range(k) if i != j)
    JkIk = [[Fr(2 if i == j else 1) for j in range(k)] for i in range(k)]
    det_ok &= (det_frac(JkIk) == k + 1)
hockey_ok = all(sum(comb(d + s - q, s - q) for q in range(s + 1)) == comb(d + s + 1, s)
                for d in range(1, 7) for s in range(1, 5))
print("L3 checks (Gram, det(J+I)=k+1, hockey-stick):", gram_ok, det_ok, hockey_ok)
# L3 checks (Gram, det(J+I)=k+1, hockey-stick): True True True

# Canonical witnesses: pentagon (d=2), octahedron (d=3), and {0,1,2} (d=1)
pent = [(cos(2*pi*i/5), sin(2*pi*i/5)) for i in range(5)]
pent_d = sorted({round(sqdist(p, q), 5) for p, q in combinations(pent, 2)})
octa = [(1,0,0),(-1,0,0),(0,1,0),(0,-1,0),(0,0,1),(0,0,-1)]
octa_d = sorted({sqdist(p, q) for p, q in combinations(octa, 2)})
line3_d = sorted({sqdist((i,), (j,)) for i, j in combinations(range(3), 2)})
print("witnesses:", pent_d, octa_d, line3_d)
# witnesses: [1.38197, 3.61803] [2, 4] [1, 4]

def two_distance(pts):                # at most two distinct pairwise distances
    return len({sqdist(p, q) for p, q in combinations(pts, 2)}) <= 2

line = [(i,) for i in range(9)]
for k in range(9, 0, -1):
    if any(two_distance(s) for s in combinations(line, k)):
        print("1D {0..8}: max", k); break          # 1D {0..8}: max 3

grid2 = [(i, j) for i in range(-3, 4) for j in range(-3, 4)]
for k in range(7, 0, -1):               # C(49,5) = 1906884 five-subsets checked
    if any(two_distance(s) for s in combinations(grid2, k)):
        print("7x7: max", k); break               # 7x7: max 4

grid3 = [(i, j, l) for i in (-1,0,1) for j in (-1,0,1) for l in (-1,0,1)]
for k in range(9, 0, -1):               # C(27,7) = 888030 seven-subsets checked
    if any(two_distance(s) for s in combinations(grid3, k)):
        print("3x3x3: max", k); break             # 3x3x3: max 6
```

**Verified output.** `L3 checks (Gram, det(J+I)=k+1, hockey-stick): True True True` / `witnesses: [1.38197, 3.61803] [2, 4] [1, 4]` / `1D {0..8}: max 3` / `7x7: max 4` / `3x3x3: max 6`. The maxima are attained by {0,1,2}-type triples, the square (±1, ±1) with squared distances {4, 8}, and the octahedron {±e_1, ±e_2, ±e_3} with {2, 4}; the two exhaustive searches confirm **no** 5-subset of the 7×7 grid and **no** 7-subset of the 3×3×3 grid is two-distance — the pentagon is not lattice-realizable, the octahedron is. **What to explore:** the ◐ Exploration (Exercise 8) sends this part's machinery further — bigger grids, rectangular windows, and the 4×4×4 cube for the lattice-discipline question.

### Part 3 — The Lecture 4 toolkit and Exercise Answer Verifications (A4–A14)

```python
from itertools import combinations
from math import sqrt, cos, sin, pi, comb, floor, ceil
from fractions import Fraction as Fr

def jacobi(A, sweeps=100):            # cyclic Jacobi: eigenvalues, descending
    n = len(A)
    if n == 0: return []
    A = [row[:] for row in A]
    for _ in range(sweeps):
        off = sqrt(sum(A[i][j]**2 for i in range(n) for j in range(n) if i != j))
        if off < 1e-11: break
        for p in range(n-1):
            for q in range(p+1, n):
                if abs(A[p][q]) < 1e-13: continue
                th = (A[q][q] - A[p][p]) / (2*A[p][q])
                t = (1 if th >= 0 else -1) / (abs(th) + sqrt(th*th + 1))
                c = 1/sqrt(t*t + 1); s = t*c
                for k in range(n):
                    akp, akq = A[k][p], A[k][q]
                    A[k][p], A[k][q] = c*akp - s*akq, s*akp + c*akq
                for k in range(n):
                    apk, aqk = A[p][k], A[q][k]
                    A[p][k], A[q][k] = c*apk - s*aqk, s*apk + c*aqk
    return sorted((A[i][i] for i in range(n)), reverse=True)

def adjacency(n, edges):
    adj = [0]*n
    for u, v in edges:
        adj[u] |= 1 << v; adj[v] |= 1 << u
    return [[1 if adj[u] >> v & 1 else 0 for v in range(n)] for u in range(n)]

def graphs(n):                         # every labeled graph, rows as bitmasks
    pairs = list(combinations(range(n), 2))
    for mask in range(1 << len(pairs)):
        adj = [0]*n
        for k, (u, v) in enumerate(pairs):
            if mask >> k & 1: adj[u] |= 1 << v; adj[v] |= 1 << u
        yield adj

def mat(adj, n):
    return [[1 if adj[i] >> j & 1 else 0 for j in range(n)] for i in range(n)]

def alpha_of(adj, n):                  # independence number, brute force
    def ok(S):
        return all(not adj[i] >> j & 1 for i in range(n) for j in range(i+1, n)
                   if S >> i & 1 and S >> j & 1)
    return max((bin(S).count("1") for S in range(1 << n) if ok(S)), default=0)

# (a) the inertia bound on every graph with n <= 5 (both sides and combined)
viol = tight_p = tight_q = tight_min = tot = 0
for n in range(1, 6):
    for adj in graphs(n):
        eigs = jacobi(mat(adj, n))
        p = sum(e > 1e-9 for e in eigs)
        q = sum(e < -1e-9 for e in eigs)
        al = alpha_of(adj, n)
        tot += 1
        viol += (al > n - p + 1e-9) or (al > n - q + 1e-9)
        tight_p += (al == n - p)
        tight_q += (al == n - q)
        tight_min += (al == min(n - p, n - q))
print("inertia:", tot, viol, tight_p, tight_q, tight_min)
# inertia: 1099 0 633 954 966

# (b) Hoffman on every d-regular graph, n = 4..7, lambda_n < 0
per_n, ht_n, hv, ht = {}, {}, 0, 0
for n in range(4, 8):
    for adj in graphs(n):
        deg = [bin(adj[i]).count("1") for i in range(n)]
        if len(set(deg)) > 1: continue
        eigs = jacobi(mat(adj, n))
        if eigs[-1] >= -1e-9: continue
        per_n[n] = per_n.get(n, 0) + 1
        b = n*(-eigs[-1])/(deg[0] - eigs[-1])
        al = alpha_of(adj, n)
        hv += al > b + 1e-9
        if abs(al - b) < 1e-9:
            ht += 1; ht_n[n] = ht_n.get(n, 0) + 1
print("hoffman:", per_n, ht_n, hv, ht)
# hoffman: {4: 7, 5: 13, 6: 171, 7: 931} {4: 7, 5: 1, 6: 111, 7: 106} 0 225

pet = adjacency(10, [(i, (i+1) % 5) for i in range(5)] +
                    [(5+i, 5 + (i+2) % 5) for i in range(5)] + [(i, i+5) for i in range(5)])
M = [[pet[i][j] + (2 if i == j else 0) for j in range(10)] for i in range(10)]
ipM = lambda x, y: sum(x[i]*sum(M[i][j]*y[j] for j in range(10)) for i in range(10))
one = [1]*10
for S in combinations(range(10), 4):            # exactly five survive
    if any(pet[a][b] for a, b in combinations(S, 2)): continue
    x = [1 if i in S else 0 for i in range(10)]
    print("star:", ipM(x, x), ipM(x, one), ipM(one, one),
          ipM(x, x)*ipM(one, one) == ipM(x, one)**2)   # star: 8 20 50 True (x5)

# (c) compression: 23 random subspaces, then the windmill quotients
seed = 987654321
def rnd():                            # deterministic LCG in [0, 1)
    global seed
    seed = (1103515245*seed + 12345) % (1 << 31)
    return seed/(1 << 31)

def orth(V):                           # Gram-Schmidt on the columns of V
    n, m, cols = len(V), len(V[0]), []
    for j in range(m):
        w = [V[i][j] for i in range(n)]
        for q in cols:
            d = sum(a*b for a, b in zip(w, q))
            w = [a - d*b for a, b in zip(w, q)]
        ln = sqrt(sum(a*a for a in w))
        cols.append([a/ln for a in w])
    return cols

ok23 = 0
for t in range(23):
    n, m = 5 + t % 4, 2 + t % 3        # m < n always
    A = [[rnd()*2 - 1 for _ in range(n)] for _ in range(n)]
    A = [[(A[i][j] + A[j][i])/2 for j in range(n)] for i in range(n)]
    Q = orth([[rnd()*2 - 1 for _ in range(m)] for _ in range(n)])
    B = [[sum(Q[j][a]*A[a][b]*Q[k][b] for a in range(n) for b in range(n))
          for k in range(m)] for j in range(m)]
    la, mu = jacobi(A), jacobi(B)
    ok23 += all(la[i] >= mu[i] - 1e-6 and mu[i] >= la[i + n - m] - 1e-6
                for i in range(m))
print("compression:", ok23, "of 23")            # compression: 23 of 23

for t, name in [(2, "W2"), (3, "W3")]:
    W = adjacency(1 + 2*t, [(0, i) for i in range(1, 2*t+1)] +
                            [(2*i-1, 2*i) for i in range(1, t+1)])
    spec, q = jacobi(W), jacobi([[0, 2*t], [1, 1]])
    print(name, all(min(abs(qv - sv) for sv in spec) < 1e-6 for qv in q))
    # W2 True / W3 True: (1 +- sqrt(17))/2 and {3, -2} inside the spectra

# (d) the umbrella, the circulant certificate, the strong product
c, s = (1/sqrt(5))**0.5, sqrt(1 - 1/sqrt(5))     # cos psi = 5^(-1/4)
u = [(s*cos(2*pi*i/5), s*sin(2*pi*i/5), c) for i in range(5)]
d2 = max(abs(sum(u[i][k]*u[(i+2) % 5][k] for k in range(3))) for i in range(5))
d1 = max(abs(sum(u[i][k]*u[(i+1) % 5][k] for k in range(3)) - (sqrt(5) - 1)/2)
         for i in range(5))
print("umbrella:", d2, d1, 1/c**2)              # umbrella: 1.67e-16 4.4e-17 2.2360679...

b = (sqrt(5) - 1)/10
X = [[0]*5 for _ in range(5)]
for i in range(5):
    X[i][i] = 0.2; X[i][(i+2) % 5] = X[i][(i+3) % 5] = b
print("certificate:", jacobi(X), sum(X[i][i] for i in range(5)),
      sum(sum(r) for r in X))
# certificate: [0.4472, 0.2764, 0.2764, ~0, ~0] 1.0 2.2360679...

c5 = adjacency(5, [(i, (i+1) % 5) for i in range(5)])
near = lambda a, b: a != b and c5[a][b] == 1
free = lambda P, Q: not ((P[0] == Q[0] or near(P[0], Q[0])) and
                         (P[1] == Q[1] or near(P[1], Q[1])))
V = [(i, j) for i in range(5) for j in range(5)]
print("strong 6:", sum(all(free(P, Q) for P, Q in combinations(T, 2))
                       for T in combinations(V, 6)))    # strong 6: 0 of 177100
print("strong 5:", sum(all(free(P, Q) for P, Q in combinations(T, 2))
                       for T in combinations(V, 5)))    # strong 5: 10
print("diagonal:", all(free((i, 2*i % 5), (j, 2*j % 5))
                       for i, j in combinations(range(5), 2)))  # diagonal: True

# (e) the chromatic bound and Proof 2's chain, coloring by coloring
def chi_color(adj, n):
    for k in range(1, n+1):
        color = [-1]*n
        def bt(v):
            if v == n: return True
            used = {color[w] for w in range(n) if adj[v] >> w & 1 and color[w] >= 0}
            for c in range(k):
                if c not in used:
                    color[v] = c
                    if bt(v+1): return True
                    color[v] = -1
            return False
        if bt(0): return k, color

nviol = nchk = 0
for n in range(4, 7):
    for adj in graphs(n):
        deg = [bin(adj[i]).count("1") for i in range(n)]
        if len(set(deg)) > 1: continue
        A = mat(adj, n); eigs = jacobi(A)
        if eigs[-1] >= -1e-9: continue
        k, color = chi_color(adj, n)
        nviol += k < 1 + deg[0]/abs(eigs[-1]) - 1e-9
        cls = sorted(set(color))
        q = [[(1 if color[v] == cl else 0)/sqrt(sum(1 for v in range(n)
                                                    if color[v] == cl))
              for v in range(n)] for cl in cls]
        B = [[sum(q[j][a]*A[a][w]*q[l][w] for a in range(n) for w in range(n))
              for l in range(k)] for j in range(k)]
        mu = jacobi(B)
        nchk += (abs(sum(B[i][i] for i in range(k))) < 1e-6 and
                 abs(mu[0] - deg[0]) < 1e-6 and
                 abs(sum(mu[1:]) + deg[0]) < 1e-6 and
                 sum(mu[1:]) >= (k-1)*eigs[-1] - 1e-6)
print("chi:", nviol, "violations of 191;", nchk, "chains verified")
# chi: 0 violations of 191; 191 chains verified

# (f) Krawtchouk, the [7,4] Hamming code, certificates, Plotkin, the exact LPs
K = lambda k, i, n: sum((-1)**j*comb(i, j)*comb(n-i, k-j) for j in range(k+1))
agree = all(K(k, i, n) == sum((-1)**len({*range(i)} & {*y})
                              for y in combinations(range(n), k))
            for n in range(5, 9) for i in range(n+1) for k in range(n+1))
print("krawtchouk faces agree:", agree)          # krawtchouk faces agree: True

ham = []
for m in range(128):
    w = [(m >> j) & 1 for j in range(7)]
    if (w[0]^w[2]^w[4]^w[6], w[1]^w[2]^w[5]^w[6],
        w[3]^w[4]^w[5]^w[6]) == (0, 0, 0): ham.append(w)
dist = lambda a, b: sum(x != y for x, y in zip(a, b))
pairs = [0]*8
for a in ham:
    for b in ham: pairs[dist(a, b)] += 1
print("hamming:", len(ham), pairs,
      [sum(pairs[i]*K(k, i, 7) for i in range(8)) for k in range(8)])
# hamming: 16 [16, 0, 0, 112, 112, 0, 0, 16] [256, 0, 0, 0, 1792, 0, 0, 0]

def F(f, i, n): return sum(c*Fr(K(k, i, n)) for k, c in f.items())
certs = [("(5,3)", 5, 3, {0: Fr(1), 1: Fr(1, 2), 5: Fr(1, 2)}, Fr(4)),
         ("(6,3)", 6, 3, {0: Fr(1), 1: Fr(1), 6: Fr(1)}, Fr(8)),
         ("(7,3)", 7, 3, {0: Fr(1), 1: Fr(1), 2: Fr(1, 3), 7: Fr(1)}, Fr(16)),
         ("(7,4)", 7, 4, {0: Fr(1), 1: Fr(1)}, Fr(8)),
         ("(8,4)", 8, 4, {0: Fr(1), 1: Fr(1), 2: Fr(1, 4)}, Fr(16)),
         ("(8,5)", 8, 5, {0: Fr(1), 1: Fr(1, 3), 8: Fr(1, 3)}, Fr(4)),
         ("(6,4)", 6, 4, {0: Fr(1), 1: Fr(1, 2)}, Fr(4)),
         ("(4,4)", 4, 4, {0: Fr(1), 1: Fr(1, 4)}, Fr(2)),
         ("(5,5)", 5, 5, {0: Fr(1), 1: Fr(1, 5)}, Fr(2)),
         ("(6,5)", 6, 5, {0: Fr(1), 1: Fr(1, 4)}, Fr(5, 2))]
assert all(F(f, 0, n) == v and all(F(f, i, n) <= 0 for i in range(d, n+1))
           for _, n, d, f, v in certs)
print("certificates: 10 of 10 valid")            # certificates: 10 of 10 valid

plotkin = [(n, d) for n in range(2, 11) for d in range(1, n+1) if 2*d > n]
assert all(F({0: Fr(1), 1: Fr(1, 2*d - n)}, 0, n) == Fr(2*d, 2*d - n) and
           all(F({0: Fr(1), 1: Fr(1, 2*d - n)}, i, n) <= 0
               for i in range(d, n+1)) for n, d in plotkin)
print("plotkin:", len(plotkin), "of 29 valid")   # plotkin: 29 of 29 valid

def solve(Mo, b):                     # exact solution of a square system
    n = len(Mo); A = [r[:] + [b[i]] for i, r in enumerate(Mo)]
    for c in range(n):
        p = next((r for r in range(c, n) if A[r][c] != 0), None)
        if p is None: return None
        A[c], A[p] = A[p], A[c]
        pv = A[c][c]; A[c] = [v/pv for v in A[c]]
        for r in range(n):
            if r != c and A[r][c] != 0:
                A[r] = [v - A[r][c]*w for v, w in zip(A[r], A[c])]
    return [A[i][n] for i in range(n)]

def lp_extreme(rows, rhs, obj, maximize):
    nv = len(rows[0])
    cons = [(row, r) for row, r in zip(rows, rhs)]
    cons += [([Fr(int(i == t)) for i in range(nv)], Fr(0)) for t in range(nv)]
    best = None
    for basis in combinations(range(len(cons)), nv):
        sol = solve([cons[k][0] for k in basis], [cons[k][1] for k in basis])
        if sol is None or any(x < 0 for x in sol): continue
        if any(sum(a*b for a, b in zip(row, sol)) < r for row, r in cons): continue
        val = sum(a*b for a, b in zip(obj, sol))
        if best is None or (maximize and val > best) or (not maximize and val < best):
            best = val
    return best

for n, d in [(4, 2), (4, 3), (4, 4), (5, 2), (5, 3), (5, 4), (5, 5), (6, 2),
             (6, 3), (6, 4), (6, 5), (7, 3), (7, 4), (8, 3), (8, 4), (8, 5)]:
    rows = [[Fr(K(k, i, n)) for i in range(d, n+1)] for k in range(n+1)]
    rhs = [-Fr(K(k, 0, n)) for k in range(n+1)]
    pm = lp_extreme(rows, rhs, [Fr(1)]*(n-d+1), True)
    drows = [[-Fr(K(k, i, n)) for k in range(n+1)] for i in range(d, n+1)]
    dm = lp_extreme(drows, [Fr(1)]*(n-d+1),
                    [Fr(K(k, 0, n)) for k in range(n+1)], False)
    assert 1 + pm == 1 + dm
    print("lp", (n, d), 1 + pm)
# lp (4,2) 8 / (4,3) 8/3 / (4,4) 2 / (5,2) 16 / (5,3) 4 / (5,4) 8/3 / (5,5) 2 /
# lp (6,2) 32 / (6,3) 8 / (6,4) 4 / (6,5) 12/5 / (7,3) 16 / (7,4) 8 /
# lp (8,3) 128/5 / (8,4) 16 / (8,5) 4   — primal == dual, 16 of 16

simplex = [[bin(m & (j+1)).count("1") % 2 for j in range(7)] for m in range(8)]
ext = [w + [sum(w) % 2] for w in ham]
punct = [w[:6] for w in simplex]
for name, C in [("[7,3]", simplex), ("[8,4]", ext), ("[6,3]", punct)]:
    print(name, len(C), min(dist(a, b) for a, b in combinations(C, 2)))
# [7,3] 8 4 / [8,4] 16 4 / [6,3] 8 3
for name, ws in [("(5,3)", ["00000", "11100", "10011", "01111"]),
                 ("(6,4)", ["000000", "111100", "110011", "001111"]),
                 ("(8,5)", ["00000000", "00011111", "11100011", "11111100"])]:
    C = [[int(ch) for ch in w] for w in ws]
    print(name, len(C), min(dist(a, b) for a, b in combinations(C, 2)))
# (5,3) 4 3 / (6,4) 4 4 / (8,5) 4 5
for n in (4, 5, 6):
    E = [[(m >> j) & 1 for j in range(n)] for m in range(1 << n)
         if bin(m).count("1") % 2 == 0]
    print("even", n, len(E), min(dist(a, b) for a, b in combinations(E, 2)))
# even 4 8 2 / even 5 16 2 / even 6 32 2

def brute(n, d):                       # A(n, d) by backtracking
    far = lambda a, b: bin(a ^ b).count("1") >= d
    best = 0
    def extend(code, cand):
        nonlocal best
        if len(code) + len(cand) <= best: return
        if not cand: best = max(best, len(code)); return
        w = cand[0]
        extend(code + [w], [c for c in cand[1:] if far(w, c)])
        extend(code, cand[1:])
    extend([], list(range(1 << n)))
    return best
print("brute:", [(n, d, brute(n, d)) for n, d in
                 [(4, 3), (5, 4), (6, 5)]])
# brute: [(4, 3, 2), (5, 4, 2), (6, 5, 2)]

# (g) Exercise Answer Verifications (A10, A11, A12, A13, A14)
# A10: triangles via direct count, tr(A^3)/6, and sum(lambda_i^3)/6
k4 = adjacency(4, list(combinations(range(4), 2)))
paw = adjacency(4, [(0,1),(1,2),(0,2),(0,3)])
dia = adjacency(4, [(0,1),(1,2),(0,2),(0,3),(1,3)])
k33 = adjacency(6, [(a, 3+b) for a in range(3) for b in range(3)])
tri_out = []
for A in (k4, paw, dia, c5, k33, pet):
    n = len(A)
    t_dir = sum(A[i][j]*A[j][k]*A[k][i] for i, j, k in combinations(range(n), 3))
    tr_a3 = sum(A[i][j]*A[j][k]*A[k][i] for i in range(n) for j in range(n) for k in range(n)) // 6
    t_eig = round(sum(e**3 for e in jacobi(A)) / 6)
    assert t_dir == tr_a3 == t_eig
    tri_out.append(t_dir)
print("A10 triangles:", tri_out)                 # A10 triangles: [4, 1, 2, 0, 0, 0]

# A11: spectral triangle threshold mu >= d^2/(n-d) on d-regular triangle-free graphs (n <= 6)
tf_tot = tf_viol = tf_eq = 0
for n in range(2, 7):
    for adj in graphs(n):
        deg = [bin(adj[i]).count("1") for i in range(n)]
        if len(set(deg)) > 1 or deg[0] == 0: continue
        A = mat(adj, n)
        if any(A[i][j]*A[j][k]*A[k][i] for i, j, k in combinations(range(n), 3)): continue
        eigs = jacobi(A); d = deg[0]
        mu = max(abs(eigs[1]), abs(eigs[-1]))
        tf_tot += 1
        tf_viol += mu < d*d/(n - d) - 1e-7
        tf_eq += abs(mu - d*d/(n - d)) < 1e-7
print("A11 threshold:", tf_tot, tf_viol, tf_eq)  # A11 threshold: 104 0 14

# A12: Wilf's bound chi <= 1 + floor(lambda_1) on all 33,866 graphs (2 <= n <= 6) & regular pinch
w_tot = w_viol = w_tight = reg_tot = reg_pinch = 0
w_by_n = []
for n in range(2, 7):
    nt = 0
    for adj in graphs(n):
        A = mat(adj, n); eigs = jacobi(A)
        chi, _ = chi_color(adj, n)
        ub = 1 + int(floor(eigs[0] + 1e-9))      # +1e-9 guards exact integer eigenvalues
        w_tot += 1; w_viol += (chi > ub)
        if chi == ub: w_tight += 1; nt += 1
        deg = [bin(adj[i]).count("1") for i in range(n)]
        if len(set(deg)) == 1 and deg[0] >= 1 and eigs[-1] < -1e-9:
            reg_tot += 1
            lb = int(ceil(1 + deg[0]/abs(eigs[-1]) - 1e-9))
            reg_pinch += (lb == ub)
    w_by_n.append(nt)
print("A12 Wilf:", w_tot, w_viol, w_tight, w_by_n, reg_tot, reg_pinch)
# A12 Wilf: 33866 0 23887 [2, 8, 61, 909, 22907] 193 45

# A14: Petersen = K(5,2) isomorphism (15 edges, 30 non-edges) and 1,023-family EKR census
kneser_lbl = [(0,1),(2,3),(0,4),(1,2),(3,4),(2,4),(1,4),(1,3),(0,3),(0,2)]
iso_edges = sum(pet[i][j] == 1 and not (set(kneser_lbl[i]) & set(kneser_lbl[j]))
                for i, j in combinations(range(10), 2))
iso_non = sum(pet[i][j] == 0 and bool(set(kneser_lbl[i]) & set(kneser_lbl[j]))
              for i, j in combinations(range(10), 2))
ekr_max = max(bin(S).count("1") for S in range(1, 1 << 10)
              if all(not pet[i][j] for i, j in combinations(range(10), 2)
                     if (S >> i & 1) and (S >> j & 1)))
ekr_att = sum(bin(S).count("1") == 4 and
              all(not pet[i][j] for i, j in combinations(range(10), 2)
                  if (S >> i & 1) and (S >> j & 1))
              for S in range(1, 1 << 10))
print("A14 K(5,2):", iso_edges, iso_non, ekr_max, ekr_att)
# A14 K(5,2): 15 30 4 5
```

**Verified output.** (a) `inertia: 1099 0 633 954 966` — neither side of the inertia bound is ever violated on any graph with n ≤ 5; n − p is tight 633 times, n − q is tight 954 times, and min(n − p, n − q) is tight 966 times. (b) `hoffman: {4: 7, 5: 13, 6: 171, 7: 931} {4: 7, 5: 1, 6: 111, 7: 106} 0 225` — 1,122 d-regular graphs with λ_n < 0, zero violations, 225 tight (7 of 7 at n = 4, 1 of 13 at n = 5, 111 of 171 at n = 6, 106 of 931 at n = 7); the five Petersen stars each print `8 20 50 True` — equality in Cauchy–Schwarz, 8·50 = 400 = 20². (c) `compression: 23 of 23` — every random subspace interlaces; `W2 True` / `W3 True` — the quotient spectra {(1±√17)/2} and {3, −2} sit inside the full windmill spectra. (d) `umbrella: 1.67e-16 4.4e-17 2.2360679…` — distance-2 products vanish, edge products are 1/φ, the value is √5; `certificate: [0.4472, 0.2764, 0.2764, 0, 0] 1.0 2.2360679…` — PSD, trace 1, J•X = √5; `strong 6: 0` of the 177,100 six-sets, `strong 5: 10`, `diagonal: True`. (e) `chi: 0 violations of 191; 191 chains verified` — every color-class quotient has tr B = 0, μ_1 = d, Σ_{i≥2}μ_i = −d ≥ (k−1)λ_n. (f) `krawtchouk faces agree: True` for n = 5..8; `hamming: 16 [16, 0, 0, 112, 112, 0, 0, 16] [256, 0, 0, 0, 1792, 0, 0, 0]`; `certificates: 10 of 10 valid`; `plotkin: 29 of 29 valid`; the sixteen LPs print `(4,2) 8`, `(4,3) 8/3`, `(4,4) 2`, `(5,2) 16`, `(5,3) 4`, `(5,4) 8/3`, `(5,5) 2`, `(6,2) 32`, `(6,3) 8`, `(6,4) 4`, `(6,5) 12/5`, `(7,3) 16`, `(7,4) 8`, `(8,3) 128/5`, `(8,4) 16`, `(8,5) 4` — exact fractions, primal == dual every time; the attaining codes print `[7,3] 8 4`, `[8,4] 16 4`, `[6,3] 8 3`, `(5,3) 4 3`, `(6,4) 4 4`, `(8,5) 4 5`, and the even-weight codes `8 2`, `16 2`, `32 2`; the three LP-loose gaps close by brute force: `(4, 3, 2)`, `(5, 4, 2)`, `(6, 5, 2)`. (g) `A10 triangles: [4, 1, 2, 0, 0, 0]`; `A11 threshold: 104 0 14`; `A12 Wilf: 33866 0 23887 [2, 8, 61, 909, 22907] 193 45`; `A14 K(5,2): 15 30 4 5`.

---

## Revision History & Verification Notes

**Editions.** Born inside Chapter 6: the averaging, Motzkin–Straus, and two-distance lectures date from that chapter's Feynman lecture edition, and the toolkit lecture (interlacing, the Hoffman bounds, Lovász theta, Delsarte's program) was its canon-audit addition. The **session-37 restructure** moved the four lectures verbatim out of the slimmed Chapter 6 and into this file, with the old numbering deliberately inherited (sections 5.x–8.x; nine exercises and seven answers in Chapter 6's numbering; lab Parts 3–5; Figures 2–4). This edition — the restructure's planned polish, executed as task B3c — completes the authoring: the chapter gets its own introduction, notation, pattern table, Trick Bag, and formula box; the lectures become 1–4 and every cross-reference is re-aimed, at Chapter 6's retained lectures where the material's history lies and at this chapter's own sections, exercises, answers, lab parts, and figures; exercises are renumbered 1–6 graded plus ◆7 and ◐8–9, answers A1–A6 and A◆7, the lab becomes Parts 1–3, the figures 1–3; and this appendix, the status footer, and the web edition are added. One bookkeeping correction to the restructure's own record: it counted ten exported exercises, but the authoritative count is nine (2, 5, 11, 13, 14, 15, 19, 21, 22), exactly as Chapter 6's verification paragraph lists them. The polish touched numbering and framing only: outside the renumbering and re-aiming tokens, the lecture bodies, exercises, answers, and lab are byte-identical to the export, save one typographic repair: the stray double-struck 𝔸 before 𝟙 in §1.2’s expander-mixing proof — a glyph that appears nowhere else in the Atlas and denotes no symbol — restored to the plain A the same sentence already uses. The session-66 adversarial review then audited the chapter end to end — one lecture-wording repair (§4.4's LP objective), one answer-formula repair (A11's C₇ witness), one typographic repair (§2.2's bold mis-close), and four lab-code repairs (Part 3's compression indexing, umbrella literal, and LP dual signs, plus the pentagram offset in both Petersen constructions) — the mathematics otherwise clean. The session-92 expansion pass then adopted the user-supplied draft on merit — five latent master defects sealed and the lab extended; the record lives in the appendix below.

**Verification basis.** The machine runs behind this chapter's numbers — the Jacobi validation, the spectral and Motzkin–Straus censuses, the two-distance grid searches, the interlacing, Hoffman, and chromatic sweeps, the theta computations, and the Delsarte certificates, Plotkin checks, and sixteen exact LPs — were all executed and recorded during Chapter 6's life; the record lives in Chapter 6's verification paragraph, and the lab parts here are the reader's runnable copies of exactly that logic, moved verbatim and renumbered only. This edition's transform was verified the standard way: an exact-token replacement pipeline, every replacement anchored at a unique string with its occurrence count asserted before the swap; a residual scan for every stale-reference shape (old lecture, section, exercise, lab-part, and figure numbers); and a hygiene gate — four lecture headers, fifteen subsection headers, balanced fences, zero mojibake, zero session references in lecture bodies, one trailing newline — before the master and its canvas were written from the same string and read back equal.

**Standing decisions.** Lecture bodies carry no session references; history lives here. The chapter proves what it uses and cites what it does not: the sharp general s-distance bound C(d+s, s) is cited (Bannai–Bannai–Stanton 1983, with Petrov–Pohoata's 2019 short proof) while the elementary C(d+s+1, s) is proved; the m(d) table of known two-distance maxima is cited, and the Larman–Rogers–Seidel integrality phenomenon beyond 2d + 3 points is cited and flagged, not derived; theta's multiplicativity under the strong product, Θ(C₅) = √5, the perfect-graph collapse, and theta's semidefinite computability are cited to Lovász 1979; A(8,3) = 20 by the shortened Hamming code is cited literature held honestly against the LP's 128/5 — the gap stays visible as the method's signature. The windmill spectra and the friendship census that produced them are Chapter 6's (its Lecture 4 and its lab); this chapter reuses the quotient computation, re-aimed. Volume II backlog attached to this chapter: the SDP lifts of the Delsarte LP (the first level of the hierarchy), the (8,3) gap beyond the LP, the Borsuk conjecture's two-distance connection, and the 27-point Schläfli construction written out. The web edition embeds this chapter byte-identically (the standard delivery format); the PDF export check is the user-owned release gate; learner testing now follows the completion of the whole project scope, at the user's direction.

**Figures.** Three figures, embedded as fenced SVG at their lecture locations per the dual-presentation convention (prose and lab code stay terminal-portable), renumbered 1–3 in this edition: Figure 1 (L2) — the Motzkin–Straus merge walk on the paw, 1/4 → 5/16 → 1/3 in two moves with the adjacent merge paying its x_v² correction; Figure 2 (L3) — the two spherical witnesses, the pentagon on the unit circle (squared distances {1.38197, 3.61803}; the spherical bound tight at d = 2) and the octahedron in R³ ({2, 4}), with the non-spherical line witness {0, 1, 2} recorded; Figure 3 (L4) — Lovász's umbrella for C₅: cos²ψ = 1/√5 makes the distance-2 pairs orthogonal, the value is √5, and the golden pentagon of dot products it draws (1/φ on edges, 0 on non-edges). All figure data were machine-verified before drawing and moved verified; the captions now carry this chapter's numbering.

**Backfill (session 41).** Five graded exercises (10–14) with pattern-mapped hints were added, per the atlas-wide backfill mandate, with worked answers A10–A14 continuing the exercise numbering (8–9 are explorations and carry no answers): triangles from the spectrum (tr(A³) = Σᵢλᵢ³ = 6t, with the bipartite-cancellation lesson — K_{3,3}'s 27 − 27); the spectral triangle threshold μ ≥ d²/(n−d) for d-regular triangle-free graphs via the tr(A³) = 0 ledger with λ_n·Σλ_i² bookkeeping, tight exactly on the complete bipartite family, with the inverse reading as a triangle detector; Wilf's chromatic upper bound χ ≤ 1 + ⌊λ1⌋ (induced Rayleigh + §4.1 interlacing + the greedy), with the Hoffman–Wilf sandwich pinning C₅ at 3; the equality analysis of Plotkin's certificate (attainment forces equidistance and coordinate balance — the (6,4) four-word code closes the brute table's row by construction, the [7,3] simplex passes the same analysis at (7,4), and the (8,5) slack is consistent by not being equidistant); and the Petersen–Kneser identification K(5,2) — the explicit isomorphism (outer {01, 23, 40, 12, 34}, inner pentagram {24, 14, 13, 03, 02}), α = 4 as Chapter 7's EKR at (5,2) with exactly the five stars attaining, the star/star/triangle 3-coloring giving χ = 3 = n − 2k + 2 (Lovász cited), and Hoffman certifying the EKR number. Every answer was machine-verified before installation: the tr(A³)/triangle/spectral triple agreement on the six named graphs (4, 1, 2, 0, 0, 0); the 104-graph d-regular triangle-free census, zero violations, equality exactly on the complete bipartite labelings (K₂ once, C₄ three times, K₃,₃ ten times), plus the C₇/Petersen strict checks (μ 1.802 against 0.8; 2 against 9/7) and K_{d,d} equality for d = 1, 2, 3; the Wilf census over all 33,866 graphs with n = 2..6 using exact eigenvalues — zero violations, 23,887 tight, the sandwich pinning 45 of the 193 regular graphs — with an honesty note: a first pass using an iterative eigenvalue estimate produced 81 spurious violations at integer boundaries, all removed by the exact computation; the code checks (all six (6,4) distances = 4 with balanced coordinates, all 28 simplex distances = 4 with weights {0, 4}, the (8,5) and (5,3) distance profiles non-equidistant, Plotkin's arithmetic 4, 8, 5, 6); and the K(5,2) checks (15 edges, 3-regular, spectrum {3, 1⁵, −2⁴}, the bijection with zero edge and non-edge mismatches, the 1,023-family census — maximum 4, exactly five attainers, all stars — and the three coloring classes independent and covering).

**Adversarial review (session 66).** The review arc's two arguing experts (skeptic and engineer) took this chapter chunk by chunk — correctness, coherence, exposition, figure aid — extend-never-rewrite, every retained objection machine-verified before any edit. Verdict: the mathematics is otherwise CLEAN, with one lecture-wording defect, one answer-formula defect, one typographic defect, and four lab-code defects caught, confirmed, and repaired in place. **The defects (machine-sealed):** (1) §4.4's LP sentence set up "maximize Σ_i x_i subject to x_0 = 1" and concluded "A(n,d) ≤ 1 + LP maximum" — under the literal reading the optimum already includes x_0's 1 and the prefix double-counts it; the lab maximizes the tail with x_0 = 1 as a constraint and prints 1 + pm, and all sixteen table values equal 1 + tail-maximum, so the objective now reads Σ_{i≥d}. (2) A11's C₇ witness read "μ = 2cos(2π/7) ≈ 1.802" — 2cos(2π/7) ≈ 1.247 is λ₂, while μ = 2cos(π/7) ≈ 1.801938 (the C₇ spectrum recomputed: {2, 1.247 twice, −0.445 twice, −1.802 twice}); the witness now carries the correct formula. (3) §2.2's mesh-check paragraph opened a bold marker and closed it with a lone asterisk — repaired to the sibling paragraphs' period-plus-double-asterisk close. **The lab-code class (recorded outputs correct, printed code repaired, outputs unchanged):** (4) Part 3(c)'s compression printed the contraction Q[a][j]·A[a][b]·Q[b][k] with a, b running over range(n) — orth returns only m orthonormal columns, so the printed loop crashes; the correct Q[j][a]·A[a][b]·Q[k][b] reproduces "23 of 23" on the lab's own LCG. (5) Part 3(d)'s umbrella check printed the ten-digit literal 0.6180339887, which forces d1 ≈ 5·10⁻¹¹ in any environment against the recorded 4.4e-17; the printed code now evaluates (√5 − 1)/2. (6) Part 3(f)'s dual block printed a sign-flipped LP — all-positive Krawtchouk rows with the negated objective minimized over z ≥ 0 is unbounded below, its vertex minima (−17, −5, −1, …) never equal to the primal — and the corrected dual (negated constraint rows, positive objective) matches the primal on all sixteen instances in exact fraction arithmetic. (7) Both Petersen constructions (Part 1's petersen, Part 3's pet) printed the pentagram term with an outer endpoint, (i, 5+(i+2)%5), building a graph of degrees 4,4,4,4,4,2,2,2,2,2 whose spectrum and star census contradict the chapter's own recorded lines; the corrected (5+i, 5+(i+2)%5) restores the Petersen graph — 3-regular, spectrum {3, 1⁵, −2⁴}, exactly five stars printing 8 20 50 True. **The fresh battery (all green, condensed):** averaging — the 33,792-graph Rayleigh/Turán census zero violations, triangle-free λ1 ≤ √m and Mantel zero violations, spectral Turán equality on K₃,₃, expander-mixing tight on Petersen and K₃,₃, C₅'s normalization 4/3 exact; Motzkin–Straus — mesh40 = 12,341 lattice points, the 64-graph census zero exceed with exactly 42 attainers (the empty graph, the 40 triangle-free-with-edge, K₄) and the integrality explanation, the n = 5 census zero exceed; two-distance grids — the centered Gram k = 2..9, the simplex witness, the pentagon {1.38197, 3.61803}, the octahedron {2, 4}, the 7×7 and 3×3×3 censuses zero exceed with the recorded attainers; the toolkit — the inertia census 1,099/0/633, the Hoffman census 1,122/0/225 with the Petersen star algebra (M𝟙_S = 2𝟙 via the K(5,2) model), the χ census 191/0/191 with Proof 2's chain verified coloring by coloring, the W₂/W₃ quotients inside the spectra, the umbrella d2 = 1.67e-16, the circulant certificate (trace 1, J•X = √5), the strong product zero of 177,100 with ten 5-sets and the diagonal free; Delsarte — the Krawtchouk faces n = 5..8, the Hamming line exact, the certificates 10/10, Plotkin 29/29, all sixteen LP optima matching the table in exact fractions; answers — A10's triple engine agreeing on all six graphs (4, 1, 2, 0, 0, 0), A11's 104-graph d-regular triangle-free census with equality exactly on the fourteen complete-bipartite labelings plus the strict witnesses (φ against 4/3, 2 against 1, 2cos(π/7) against 4/5, 2 against 9/7), A12's Wilf census over all 33,866 graphs with n = 2..6 — zero violations, 23,887 tight (2 + 8 + 61 + 909 + 22,907), the Hoffman–Wilf sandwich pinning exactly 45 of the 193 regular graphs — A13's equidistance and coordinate-balance signatures on all four codes with Plotkin's 4, 8, 5, 6, and A14's K(5,2) checks (the bijection with zero edge and non-edge mismatches, the 1,023-family census with exactly five star attainers, the coloring classes independent and covering, the 5-cycle witness). Figures 1–3 verified as SVG geometry. Cross-references: the Chapter 6 pointers valid, the pattern index consistent with the atlas (P19: exercise 2; P21: 10, 11, 12, 14; P22: 13). Per the rebuild rule the web edition and the .html export were rebuilt — fidelity proof first — and the review arc advances to Chapter 9.

**Expansion-pass adoption (session 92).** The uploaded expansion draft was adopted per the standing pipeline — R1 structural read and pattern audit, R2 adversarial referee, R3 figure and lab validation, R4 assembly — extend-never-rewrite, every number machine-verified before installation. The pattern references were audited against the atlas registry and found not mangled: the P21/P20/P19/P22 table, every exercise hint, and the Trick Bag all match, and no reverse-index ripple was needed. **Five latent master defects sealed:** (1) §2's intro claimed "both lemmas bound λ1 from below" — Lemma 2 bounds from above; the draft's "on triangle-free graphs" is correct. (2) §3.1's Gram factorization read G = WᵀW — it is G = WWᵀ for the k×d row matrix whose rows are the centered vectors (the session-90 Chapter 6 transpose class). (3) §3.1's simplex witness placed the hyperplane Σx = 0 ⊂ R^d — it sits in R^{d+1}, isometric to R^d. (4) §4.1's monotonicity corollary tested "the Perron vector of the larger graph", a chain that never closes (Rayleigh_A(x) ≤ λ1(A) runs the wrong way); the smaller graph's unit Perron vector gives λ1(A + E) ≥ xᵀ(A + E)x ≥ xᵀAx = λ1(A) — verified over all 5,120 edge-addition pairs on n = 5, zero decreases. (5) §4.1's unification credited "L2's σ² ≤ n" as a quadratic form on 𝟙⊥ — a symbol L2 never introduces; it is s² ≤ n, Cauchy–Schwarz on the linear form. Plus A4's stale cross-ref ("Part 1(a)" → Part 3(a), where the inertia census lives) and the precision repairs adopted from the draft: the Perron–Frobenius preamble (λ1 = max_i|λi| ≥ 0 with an entrywise nonnegative unit eigenvector), the even/odd Mantel equality split, the E = ∅ edge case and s > 0 in §2.3 and A3, δ > 0 with the explicit two-step summing in §3.1 and A2, D as the realized squared-distance values with 0 ∉ D in §3.2, s ≥ 1 and C(n,m) = 0 for m < 0 in §3.3, the nonempty guards (partition cells, the independent set, the coloring classes, the code), the entrywise inner product definition with the Frobenius justification in §4.3, the explicit Krawtchouk bounds in §4.4, and A1's odd-n integrality extension. **Lab extended:** Part 1 gains the max_eml_ratio expander-mixing receipt (`2.0 3.0 1.3333` — tight on Petersen and K_{3,3}, 4/3 short of φ on C₅), the clique_num helper, and the full 33,792-graph census code; Part 2 gains the exact-fraction block (centered Gram k = 2..9, det(J_k + I_k) = k + 1, the hockey-stick identity) and the three canonical witnesses (pentagon {1.38197, 3.61803}, octahedron {2, 4}, {0, 1, 2} {1, 4}); Part 3 prints both inertia sides (`1099 0 633 954 966`), per-n Hoffman totals and tight counts (`{4: 7, 5: 13, 6: 171, 7: 931} {4: 7, 5: 1, 6: 111, 7: 106} 0 225`), and the new (g) answer-verification receipts (A10 `[4, 1, 2, 0, 0, 0]`; A11 `104 0 14` — equality exactly the fourteen complete-bipartite labelings; A12 `33866 0 23887 [2, 8, 61, 909, 22907] 193 45`; A14 `15 30 4 5`); the Jacobi tolerances tightened (1e-9 → 1e-11, 1e-12 → 1e-13, with the n = 0 guard). **Figures 1–3 are redesigns with identical captions**, geometry machine-validated: Figure 1 walks the paw in three panels (the four-weight start, the adjacent merge paying the x_d² correction, the symmetrized clique at 1/3); Figure 2's pentagon vertices sit on its drawn circle within 1.5 px and the octahedron's three antipodal pairs share a midpoint, its twelve blue edges exactly the non-antipodal pairs; Figure 3's umbrella rim lies on its drawn ellipse and the dot-product pentagon's solid cycle is exactly the 1/φ edges. **The fresh verification battery, all green:** every standing and new receipt reproduced in independent ports — the six spectra, the EML ratios, both inertia sides, the Hoffman census through the full n = 7 enumeration (2,097,152 masks), the Wilf census, the threshold census, the MS meshes (12,341 points, 42 attainers, the n = 5 census zero exceed), the grid censuses (zero 5-subsets of C(49,5) = 1,906,884; zero 7- and 8-subsets of the 3×3×3), the exact-fraction Gram/determinant/hockey-stick checks, the theta and Delsarte batteries with all sixteen LP optima primal == dual, and the three brute-force closures. **Checker-side test bugs (the session's own, honestly recorded):** the R1 tag-stripper's raw-"<" false alarms (three passages re-verified intact on disk), a Gram-check port bug, a compression indexing crash, a Krawtchouk faces bitmask bug, a Plotkin fraction-normalization bug, an even-code pc(sum) bug, and two figure-filter artifacts — every one caught by its own gate and fixed before any finding was recorded. **Honest scope notes:** the (g) A11 block is scoped to n ≤ 6 (its comment says so), with Exercise 11's prose witnesses C₇ and Petersen verified fresh (μ(C₇) = 1.8019 ≥ 4/5; Petersen μ = 2 ≥ 9/7); Part 2's printed 7×7 loop starts at k = 7, so its k = 6, 7 layers rest on the cited m(2) = 5 (unchanged from the session-66 state — the k = 5 census, 1,906,884 subsets, is the printed receipt). Per the rebuild rule the web edition was rebaked oracle-first after assembly.

---
*Chapter status: ✅ **Feynman edition + exercise backfill (session 41) + adversarial review (session 66) + expansion pass (session 92)** — 4 lectures (eigenvalues as averaging machines; Motzkin–Straus and spectral Turán; two-distance sets, a capstone in three bounds; the modern toolkit: interlacing, Hoffman, theta, Delsarte), all proofs complete with citations kept honest; 3 verified figures (redesigns, geometry machine-validated); 11 graded exercises + 1 ◆ pattern-unknown + 2 ◐ explorations, 12 worked answers machine-verified; lab in 3 verified parts (Jacobi eigenvalues, expander-mixing ratios, and the spectral and Motzkin–Straus censuses; two-distance Gram spectra, polynomial dimensions, and exhaustive grid censuses; the toolkit with the exercise-answer verifications). Born in Chapter 6, exported by the restructure, completed here as a standalone course: the Atlas's linear-algebraic arc runs from Chapter 6 into this chapter and closes. The session-66 adversarial review audited the chapter end to end — one lecture-wording repair (§4.4's LP objective), one answer-formula repair (A11's C₇ witness), one typographic repair (§2.2's bold mis-close), and four lab-code repairs (Part 3's compression indexing, umbrella literal, LP dual signs, and the Petersen constructions' pentagram offset), the mathematics otherwise clean. The session-92 expansion pass sealed five latent master defects (§2's "from below", §3.1's G = WᵀW and simplex tail, §4.1's monotonicity corollary and unification σ²), adopted the draft's precision repairs, and extended the lab with fresh receipts. Ships with its web edition (the standard delivery format): the HTML canvas embeds this chapter byte-identically; print to PDF from a browser for a correct export.*
