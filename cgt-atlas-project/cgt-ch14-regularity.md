---
name: "cgt-ch14-regularity"
title: "Ch. 14 — Regularity and Density: The Structure Hiding in Every Large Graph (A Lecture Course in the Feynman Style)"
type: "text/markdown"
---

# Chapter 14 · Regularity and Density

*Part of the Combinatorics & Graph Theory Atlas (the chapter map lives in the book basis).*

Turán's theorem (Chapter 2) and Erdős–Stone (this chapter, Lecture 3) say the same scandalous thing: the extremal question "how many edges before H must appear" is governed by one number, the chromatic number of H — a single integer steering an n²-scale question. Why should that be true? What is it about large dense graphs that makes one parameter so powerful? The answer is the Szemerédi regularity lemma, and it is the engine room of this chapter. **Regularity** (Lecture 1): every large graph, however adversarial, is a bounded blow-up of a small pattern graph, draped in quasirandom noise. **Counting and removal** (Lecture 2): within that structure, copies of any fixed H are counted by multiplying densities — and a graph with few copies of H can be cleaned of them all for the price of few edge deletions. **Stability** (Lecture 3): near-extremal H-free graphs are not just few in edges — they are *close to the Turán graph itself*. **Roth** (Lecture 4): triangle removal + a layered construction ⟹ every positive-density set of integers holds a 3-term arithmetic progression — combinatorics proving number theory. **Density Ramsey** (Lecture 5): Szemerédi's theorem for all k, the density Hales–Jewett theorem, and the honest hierarchy between them. **The cap set theorem** (Lecture 6): the 2016 surprise — the polynomial method of Chapter 6 returning with slice rank, and the constant 2.7551046130^n.

The deal with the reader is the one the Atlas has enforced since Chapter 1: every number printed below was machine-verified before printing — exhaustive censuses, exact optima, seeded searches — and where a bound is vacuous, a proof is cited rather than given, or an optimality is beyond the chapter's computational reach, the text says so in those words.

## How to read this chapter

Nothing here needs Chapter 2 beyond Turán's theorem and Chapter 6 beyond the polynomial method's calling card; both are re-derivable from the statements given in place. Lines marked **✎ Checkpoint** are the places to stop and predict — commit to a guess, in ink, before reading on. Exercises are graded ●○○ *easy* (one idea, applied directly), ●●○ *moderate* (two ideas, or one tricky step), ●●● *tough* (several ideas combined); ◆ **pattern unknown** problems come with no hint — diagnosing the tool is part of the problem; ◐ **Explorations** are open-ended investigations that state what you should find, not a number to match. Worked answers sit at the end; hints travel with the problems.

Notation. For vertex sets X, Y in a graph G, e(X, Y) counts the ordered pairs (x, y) ∈ X × Y with xy ∈ E(G) (so e(X, Y) is the number of cross-edges when X, Y are disjoint, and e(X, X) = 2|E(G[X])| when X = Y), and d(X, Y) = e(X, Y)/(|X||Y|) is the *density* between them. A pair (X, Y) is **ε-regular** if |d(A, B) − d(X, Y)| ≤ ε for every A ⊆ X, B ⊆ Y with |A| ≥ ε|X|, |B| ≥ ε|Y|. A partition V = V₁ ∪ … ∪ V_k is *equitable* if the parts differ in size by at most one, and *ε-regular* if all but at most εk² of the pairs (V_i, V_j) are ε-regular. The *index* (or *energy*) of a partition P is q(P) = Σ_{i,j} |V_i||V_j|/n² · d(V_i, V_j)², diagonal included — the weighted average of squared densities. ex(n, H) is the maximum number of edges of an n-vertex H-free graph; χ(H) its chromatic number; π(H) = 1 − 1/(χ(H) − 1) its Turán density. Z_n is the integers mod n (n odd throughout, so 2 is invertible); F₃ⁿ is the n-dimensional vector space over {0, 1, 2}. o(·) is as n → ∞.

The chapter's machine runs follow the Atlas's standing rule: exhaustive where feasible, and where randomness is used, a Lehmer generator (x ← 48271·x mod 2³¹−1), seeded and recorded, so every sample is reproducible bit for bit.

## The pattern map for this chapter

| Pattern | Plain language | Where it fires |
|---------|---------------|----------------|
| **P10 Averaging / expectation** | The average is a promise; some object beats it | L1 (the energy index is averaging with a spotlight on the partition), L6 (the slice-rank bound is an averaged monomial count) |
| **P30 Regularity partitioning** | Every large graph is a bounded quasirandom blow-up; refine until the noise is uniform | L1–L4 (the lemma and its three payoffs: counting, removal, stability) |
| **P31 Counting–removal** | Regular structure multiplies densities; few copies ⟹ few deletions | L2 (the counting lemma), L4 (triangle removal ⟹ Roth) |
| **P32 Stability** | Near-extremal objects are near the extremal *configuration*, not merely near its count | L3 (Simonovits: near-extremal H-free graphs are near-Turán after few deletions) |
| **P33 Density increment** | If the structure you want is nowhere, refine: some cell gains density | L4 (Roth's own proof route, and the Meshulam prior in L6), L1 (the index increment is the same move on graphs) |
| **Transference — the face of P30/P31** | The engine deployed on *relative* versions: find a dense model inside the sparse host and the regularity/removal argument carries across unchanged (the transference principle; Green–Tao's relative Szemerédi is the flagship). One face, two entries: the relative argument needs P30's partition to build the dense model AND P31's counting–removal to run inside it — the survey's census fired both patterns together (G11 the flagship), so the face names both, no double credit | Beyond this chapter — named here at the survey's recommendation |
| **Polynomial method (Chapter 6's card)** | Wrap the configuration space in a polynomial; dimension is your budget | L6 (CLP/EG slice rank — the direct descendant of Chapter 6's Lecture 3) |

---

## Lecture 1 · The Regularity Lemma: Every Graph Wants to Be Simple

Here is a fact it took combinatorics until 1975 to notice. Take any graph on a million vertices — the most adversarial construction you can imagine, edges placed by an enemy to defeat every theorem. The regularity lemma says: at the right magnification, your enemy's graph is *boring*. Its vertices split into a bounded number of parts, the edges between any two parts behave like a coin flip, and the only thing your enemy actually chose is the small pattern of densities between the parts. Structure at the macro level, noise at the micro level — whether the graph is a Turán graph, a Paley graph, or pseudorandom garbage, this description is forced.

The notion that makes "behaves like a coin flip" precise is ε-regularity. Say it once more, slowly: a pair (X, Y) is **ε-regular** if *no pair of large test sets can detect a bias* — for every A ⊆ X and B ⊆ Y with |A| ≥ ε|X| and |B| ≥ ε|Y|, the density d(A, B) stays within ε of the overall density d(X, Y).

**✎ Checkpoint.** Before reading on: at ε = 1/4, among all 65,536 bipartite graphs on 4 + 4 labeled vertices, how many do you expect to be ε-regular — most of them, about half, or almost none? Commit to a number.

The machine answer was run as an exhaustive census (every graph, every test pair — no sampling): at ε = 1/4 exactly **2** of the 65,536 graphs are ε-regular. Regularity at a meaningful tolerance is *rare*, a genuine structural property and not a formality — which is the point: the lemma will *force* it. At ε = 1/2 the count rises to 46,408 (about 71%), and at ε = 3/4 it reaches 65,536 — the property has gone vacuous, as every bound in this chapter does when its tolerance is loosened far enough. The census also fixes the worst a witness can be forced to show: some non-regular pair at ε = 1/4 has a test pair (A, B) with |d(A, B) − d(X, Y)| = 0.9375, nearly the full range — non-regularity is not always subtle.

> **The Szemerédi regularity lemma.** For every ε > 0 and every integer m there is M(ε, m) such that every graph on n ≥ m vertices admits an equitable partition into k parts with m ≤ k ≤ M(ε, m), all but at most εk² of the pairs ε-regular. (E. Szemerédi, "Regular partitions of graphs", *Problèmes Combinatoires et Théorie des Graphes*, Orsay 1976, Colloq. Internat. CNRS 260, 399–401.)

The proof is an energy argument — averaging with a spotlight, P10 upgraded. For a partition P define the index q(P) = Σ_{i,j} |V_i||V_j|/n² · d(V_i, V_j)² (the diagonal terms i = j included; with them the weights sum to exactly 1, so 0 ≤ q ≤ 1 with both ends honest: q = 0 for the empty graph, q → 1 for the complete graph partitioned into singletons). Two monotonicity facts drive everything:

1. **Refinement raises the index.** If P′ refines P, then q(P′) ≥ q(P). *Proof.* Let X = X₁ ∪ … ∪ X_r and Y = Y₁ ∪ … ∪ Y_s be decomposed into subparts of P′. Because e(X, Y) = Σ_{a,b} e(X_a, Y_b) = Σ_{a,b} |X_a||Y_b| d(X_a, Y_b), the overall density d(X, Y) is the weighted average Σ_{a,b} p_{a,b} d(X_a, Y_b) with weights p_{a,b} = |X_a||Y_b|/(|X||Y|) summing to 1. By the elementary variance identity Σ_{a,b} p_{a,b} d(X_a, Y_b)² − d(X, Y)² = Σ_{a,b} p_{a,b}(d(X_a, Y_b) − d(X, Y))² ≥ 0, multiplying by |X||Y|/n² gives Σ_{a,b} (|X_a||Y_b|/n²) d(X_a, Y_b)² − (|X||Y|/n²) d(X, Y)² = Σ_{a,b} (|X_a||Y_b|/n²)(d(X_a, Y_b) − d(X, Y))² ≥ 0. Summing over all pairs (X, Y) of P yields q(P′) ≥ q(P). The Atlas ran this as an exhaustive machine check: for *every* graph and partition on small vertex sets, the inequality held without exception — 106,496 checks at n = 5 (all 1,024 graphs × all 52 partitions × both ladder bounds) and 1,638,400 at n = 6 (all 32,768 graphs × the 25 equitable (2,2,2) and (3,3) partitions × both bounds), **zero violations** — pinning the ladder q(trivial) ≤ q(P) ≤ q(singletons) that the proof climbs.
2. **Defects pay rent.** Suppose (X, Y) is *not* ε-regular, witnessed by X₁ ⊆ X, Y₁ ⊆ Y with |X₁| ≥ ε|X|, |Y₁| ≥ ε|Y|, and |d(X₁, Y₁) − d(X, Y)| > ε. Partition X = X₁ ∪ X₂ and Y = Y₁ ∪ Y₂; by the variance identity above, the single sub-block (X₁, Y₁) alone contributes at least (|X₁||Y₁|/n²)(d(X₁, Y₁) − d(X, Y))² > ε|X|·ε|Y|·ε²/n² = ε⁴|X||Y|/n² to the index increment. When more than εk² ordered pairs (V_i, V_j) of an equitable k-partition P are irregular (with |V_i| = n/k), simultaneously refining every part V_i by the common intersection of all witness cuts (producing at most k·2^{k−1} subparts, then re-equitabilizing into k′ ≤ k·4^k parts at an index loss of at most ε⁵/2) yields a net energy gain of at least εk²·ε⁴·(n/k)²/n² − ε⁵/2 = ε⁵/2, so **q(P′) ≥ q(P) + ε⁵/2** (the core variance identity was machine-checked over 1,125,000 instances, zero violations). A defect is not free: exposing it deposits energy.

Now iterate. Start from an equitable partition into m parts. If it is ε-regular, stop. If not, refine by the witnesses; the index rises by at least ε⁵/2, and since it is capped at 1, there are at most 2ε⁻⁵ refinement rounds before the partition must be ε-regular. The catch — the famous, honest catch — is the *size* of the partitions along the way: each refinement multiplies the number of parts by roughly 4 per defective pair, and the part count grows like a tower of exponentials in the number of rounds. The standard bound makes M(ε) a **tower of 2's of height O(ε⁻⁵)**.

Do not nod past that tower; look at it. The Atlas ran the toy iteration k ↦ k·2^k (the same shape as the refinement blow-up) from k₀ = 2: after one step k = 8, after two k = 2048, after three k = 2048·2^2048 ≈ 10^619.8 — already past the number of atoms in the observable universe (10^80) and past a googol (10^100) at the *third* step — and the fourth step overflows 64-bit floating point arithmetic entirely. A true tower of 2's of height 5 is 2^65536 ≈ 10^19728. At the sample tolerances, the regularity proof's tower carries about 100,000 levels at ε = 0.1, 3.2 million at ε = 0.05, and ten billion at ε = 0.01. And the tower is *not an artifact of the proof*: Gowers proved partitions exist for which any regular partition genuinely needs tower height Ω(ε^{−1/16}) — a proof later simplified by Moshkovitz–Shapira — and Fox–Lovász pinned the tight order of the tower height, about ε^{−2}, for a version of the lemma — the regularity lemma is, in a precise sense, *about towers*. The honest gap between the proven upper height (ε⁻⁵) and the lower one (ε^{−1/16}), for the standard form of the lemma, is stated here as a gap, not smoothed over.

What the lemma does *not* say is as important as what it says. It is vacuous for sparse graphs (densities shrink with the noise). Its constants are galactic — no algorithm can afford M(ε) — which is why the algorithmic regularity literature (finding the partition, not just proving it exists) is a separate subject the chapter only names. And the ε-regularity of a pair is a *for-all* condition over test sets: checking it naively costs exponential time, which is why the Lab's Part 1 brute-forces it only at census scale.

**✎ Checkpoint.** You know q ≤ 1 and each defect-refinement adds ≥ ε⁵/2. Estimate how many rounds the proof can possibly need at ε = 1/2. Then explain to yourself why this *still* produces a tower — the rounds are few, but the *parts* are what explode.

The next two lectures cash the lemma in: counting (Lecture 2) turns the macro pattern into copy counts, and removal turns copy counts into the deletion theorem that Lecture 4 will point at the integers.

---

## Lecture 2 · Counting and Removal: Densities Multiply, Copies Yield

The regularity lemma described the *macro* graph: parts, densities, uniform noise. This lecture turns the description into arithmetic. The counting lemma says that in an ε-regular world, the number of triangles is what the densities predict — the product d₁₂·d₁₃·d₂₃ times the volume. Its philosophical punchline is a dichotomy: in a regular setting, a graph's triangle count is *either zero or enormous* — there is no in-between, no "seven triangles hiding in a dense sea of edges". Then, run in reverse with the regularity lemma's refining power, the counting lemma proves the **graph removal lemma**: a graph with few copies of H can be made H-free by deleting few edges. Few in, few out — the deletion theorem that Lecture 4 will fire at the integers.

First, the trap. Why is ε-regularity needed at all — aren't densities enough?

**✎ Checkpoint.** A tripartite graph has parts X, Y, Z of size 16, with *every* pairwise density exactly 1/2: d(X,Y) = d(X,Z) = d(Y,Z) = 1/2. The product 1/8 would predict (16)³/8 = 512 triangles. Guess: can such a graph have *zero* triangles?

It can, and the Atlas built the witness: a hi/lo split. Label each part's 16 vertices 0…15 and let hi(v) record whether v ≥ 8. Put an X–Y edge when hi(x) = hi(y), a Y–Z edge when hi(y) = hi(z), and a Z–X edge when hi(z) ≠ hi(x). Each pair carries exactly 128 of its 256 possible edges — every pairwise density is exactly 1/2 — and a machine sweep confirms the triangle count is **zero**: a triangle needs hi(x) = hi(y) = hi(z) from the first two pairs, and then hi(z) ≠ hi(x) from the third — a flat contradiction. The pairs are maximally irregular: the test sets X = {0,1,2,3} (all low) and Y = {8,9,10,11} (all high) see density 0 where the pair as a whole says 1/2 — witness discrepancy exactly 1/2, the maximum over 2,000 seeded test pairs as well. Densities *lie* when the pairs are not regular — and that is the point: the counting lemma's hypothesis is not decoration; it is the engine.

> **The counting lemma (triangles, ε-tolerant form).** Let (X, Y), (X, Z), (Y, Z) be ε-regular pairs with densities d₁₂, d₁₃, d₂₃ ≥ 2ε. Then the number of triangles xyz is within a factor (1 ± Cε) — on the C = 3 form used here — of d₁₂·d₁₃·d₂₃·|X||Y||Z|; in particular, it is at least (1 − 2ε)(d₁₂−ε)(d₁₃−ε)(d₂₃−ε)·|X||Y||Z|, with per-vertex degree-floor product window (d₁₂−ε)(d₁₃−ε)(d₂₃−ε)·|X||Y||Z|.

*Proof (greedy embedding — the chapter gives it in full).* For each x ∈ X let d_Y(x), d_Z(x) be its degrees into Y and Z. Regularity of (X, Y) forces all but at most ε|X| vertices x to satisfy d_Y(x) ≥ (d₁₂ − ε)|Y| — otherwise the set A of low-degree vertices would have |A| ≥ ε|X| and d(A, Y) < d₁₂ − ε, violating ε-regularity. Likewise at most ε|X| vertices fail d_Z(x) ≥ (d₁₃ − ε)|Z|. Fix any of the at least (1 − 2ε)|X| *good* vertices x ∈ X satisfying both degree floors: its neighborhoods N_Y(x) ⊆ Y and N_Z(x) ⊆ Z have sizes |N_Y(x)| ≥ (d₁₂−ε)|Y| ≥ ε|Y| and |N_Z(x)| ≥ (d₁₃−ε)|Z| ≥ ε|Z|. Applying ε-regularity of (Y, Z) directly to the admissible test pair (N_Y(x), N_Z(x)) gives at least (d₂₃ − ε)|N_Y(x)||N_Z(x)| ≥ (d₁₂−ε)(d₁₃−ε)(d₂₃−ε)|Y||Z| edges between N_Y(x) and N_Z(x) — the degree-floor product window per x ∈ X. Summing over the ≥ (1 − 2ε)|X| good vertices x yields at least (1 − 2ε)(d₁₂−ε)(d₁₃−ε)(d₂₃−ε)|X||Y||Z| triangles, and the matching upper bound is the same walk with inequalities flipped. ∎

The Atlas ran the honest numeric test: tripartite graphs on parts of size 30, each pair a uniform random bipartite graph at planted densities (Lehmer seed 20261052, recorded) — density triples (1/2, 1/2, 1/2) and (0.7, 0.4, 0.55): the machine counted **3,307 triangles against a product prediction of 3,285 (100.7%)** and **4,202 against 4,215 (99.7%)**, both comfortably inside the (d−0.1)³ lower window the lemma promises at ε = 0.1. Two thousand seeded samples per configuration, zero runs outside the window. When the pairs are regular, densities multiply — end of story.

The same greedy walk, run vertex by vertex on a fixed H whose edges' pairs are all ε-regular, counts copies of H in a regular partition as the product of the relevant densities times n^{|H|}, up to the same ε-slack: **regular structure is transparent to counting**.

Now run the machinery in reverse.

> **The graph removal lemma.** For every fixed graph H and every δ > 0 there is ε > 0 such that every n-vertex graph with at most εn^{|H|} copies of H can be made H-free by deleting at most δn² edges.

*Proof of the graph removal lemma (Komlós–Simonovits cleaning argument).* Let h = |V(H)|. Given δ > 0, set the minimum density threshold γ = δ/2, the regularity tolerance ε = min(δ/4, γ/3h), and the minimum cluster count m = ⌈2/δ⌉. By the Szemerédi regularity lemma, G has an equitable ε-regular partition V(G) = V₁ ∪ … ∪ V_k with m ≤ k ≤ M(ε, m).

Form a cleaned subgraph G′ ⊆ G by deleting three classes of edges:

1. **Intra-cluster edges** (both endpoints inside the same V_i): at most k·C(⌈n/k⌉, 2) ≤ n²/(2k) ≤ (δ/4)n² edges.
2. **Irregular-pair edges** (between pairs (V_i, V_j) that are not ε-regular): since at most εk² ordered pairs {i, j} are irregular, this deletes at most (1/2)·εk²·(n/k)² = (ε/2)n² ≤ (δ/8)n² edges.
3. **Low-density-pair edges** (between pairs (V_i, V_j) with density d(V_i, V_j) < γ): at most C(k, 2)·γ·(n/k)² ≤ (γ/2)n² = (δ/4)n² edges.

In total, at most (δ/4 + δ/8 + δ/4)n² < δn² edges have been deleted. Suppose for contradiction that the cleaned graph G′ still contains a copy of H, with vertices u₁, …, u_h lying in clusters V_{i₁}, …, V_{i_h}. Because every edge of G′ connects two distinct clusters whose pair (V_{i_a}, V_{i_b}) is ε-regular with density d(V_{i_a}, V_{i_b}) ≥ γ ≥ 3hε (even if some non-adjacent vertices of H fall into the same cluster V_{i_a}, we may split each cluster into h equal subclusters while preserving hε-regularity and density ≥ γ − ε ≥ 2hε), the general counting lemma applied to the h subclusters hosting u₁, …, u_h guarantees at least (γ − hε)^{|E(H)|}·∏_a |V_{i_a}| ≥ (γ/2)^{|E(H)|}·(n/(h·M(ε, m)))^h copies of H in G. Choosing the theorem's hypothesis parameter ε₀(δ) < (γ/2)^{|E(H)|}·(h·M(ε, m))^{−h} contradicts the assumption that G had at most ε₀n^h copies of H. Thus G′ is H-free. ∎ (The quantitative price: the tolerance ε₀ must be a tower-inverse of δ, since it is chosen *after* the regularity lemma's M — this is where tower-type bounds in removal lemmas come from; Fox's regularity-free proof, "A new proof of the graph removal lemma", *Annals of Mathematics* 174(1), 2011, DOI 10.4007/annals.2011.174.1.17, cuts this bond and yields better quantitative forms for the directed and multicolored analogues. The chapter cites it; it does not reprove it.)

The removal lemma has a mirror-image extremal question — the **Ruzsa–Szemerédi (6,3)-problem**: how many edges can a graph have if *every edge lies in exactly one triangle*? At first glance such graphs look rich (triangle-covered), and small cases say little: on 6 vertices, the Atlas ran the exhaustive census — all 32,768 labeled graphs — and found the maximum is exactly **6 edges**: the 100 labeled extremals are 90 "bowties" (two triangles sharing one vertex) and 10 disjoint triangle pairs, and in total only 121 graphs on 6 vertices have the property at all (including the empty graph, vacuously). Compare the Roth construction of Lecture 4: there, a 3-AP-free set A ⊆ Z_n yields exactly such a graph with n|A| edges on 3n vertices — *linearly* many. The Ruzsa–Szemerédi theorem says that is essentially the ceiling: such graphs have o(n²) edges. Equivalently (the matching formulation — its small end is ◆ Problem 3's classification; the general equivalence is standard, cited rather than re-derived here): if the edges of a bipartite graph partition into induced matchings, each of size at least δ times its side, then the graph has o(n²) edges.

The machine census gives that equivalence's *threshold behavior* honestly at brute-force scale: for m + m bipartite graphs, partition the edges into induced matchings each of size at least k. At k = 2 (a constant), the maximum is still quadratic — m² − m edges, and the extremal graphs are *exactly* the complements of perfect matchings (6 labeled at m = 3, 24 = m! at m = 4; blocks = the transposition pairs). Raise the bar to k = 3 of 4 — matchings of size at least 3n/4 — and the maximum collapses to n (a single induced perfect matching; no 5- or 6-edge example exists at m = 4, exhaustively confirmed). The δn matching-size hypothesis of the theorem is not a technicality; it is the cliff edge between n² and n, and the small censuses display it exactly.

**✎ Checkpoint.** Every edge in exactly one triangle, 6 vertices, 6 edges: the bowtie and the triangle pair tie. Predict: on 8 vertices, can any such graph beat 8 edges? (Part 6 of the Lab runs the 6-vertex census in seconds; 8 vertices means 2^28 graphs, and brute force itself collapses — which is the point: the honest answer for general n is the Ruzsa–Szemerédi o(n²), whose *proof* needs the full regularity apparatus. The small cases are Structure, the theorem is Law.)

What you should carry forward: densities multiply *under regularity*; few copies *mean* few deletions; and the unique-triangle world is thin — all three facts are the regularity lemma wearing different clothes. Lecture 3 turns the machine on the oldest extremal question there is.

---

## Lecture 3 · Erdős–Stone and Stability: One Number Rules Them All

Turán's theorem solved one case with a beautiful exact answer: ex(n, K_r) = (1 − 1/(r−1))·C(n,2), with equality exactly at the complete (r−1)-partite Turán graph. In 1946 Erdős and Stone answered the general case in a single stroke, and the answer is the scandal of the subject: for any fixed graph H with at least one edge (χ(H) ≥ 2),

> **Erdős–Stone.** ex(n, H) = (1 − 1/(χ(H)−1) + o(1))·C(n,2).

The chromatic number. Nothing about H's edges, its triangles, its paths — only how many colors it demands. A 3-chromatic H of any shape (the triangle, an odd cycle, K₃ plus a million dangling vertices) has the same extremal asymptotics to first order. Every extra part-level of uncolorability costs exactly a 1/(r−1) fraction of the edges. (Erdős–Stone, "On the structure of linear graphs", *Bull. Amer. Math. Soc.* 52(12), 1946, 1087–1091; the compact form used today is due to Erdős–Simonovits, "A limit theorem in graph theory", *Studia Sci. Math. Hungar.* 1, 1966, 51–57.)

The modern proof is the regularity lemma with the counting lemma bolted on — worth writing in full because it is the template for everything in the rest of the chapter. Let G be H-free with χ(H) = r ≥ 2 and |V(H)| = h, so H is a subgraph of the complete r-partite blow-up K_r(t) with part size t ≤ h. Fix any target slack δ > 0. Set the pair-density threshold γ = δ/2, choose ε > 0 small enough that ε ≤ (γ/2)^{rt} and ε ≤ δ/4, and apply the regularity lemma to G with tolerance ε and m ≥ 2/δ, obtaining an equitable partition V₁ ∪ … ∪ V_k with m ≤ k ≤ M(ε, m).

Clean G just as in Lecture 2: delete all edges inside clusters (≤ n²/(2k) ≤ (δ/4)n²), inside irregular pairs (≤ (ε/2)n² ≤ (δ/8)n²), and inside pairs of density below γ = δ/2 (≤ (γ/2)n² = (δ/4)n²) — a total escrow sacrifice of at most (5/8)δn² edges. Now form the *reduced graph* R on the k cluster indices {1, …, k}, joining i and j whenever (V_i, V_j) is ε-regular with density d(V_i, V_j) ≥ γ. If R contained a copy of K_r, say on clusters V₁, …, V_r, the blow-up counting lemma would embed K_r(t) (and therefore H ⊆ K_r(t)) into V₁ ∪ … ∪ V_r as soon as |V_i| = n/k ≥ t/(γ/2)^{rt}: each new vertex embedded into V_a needs to lie in the common neighborhood of at most (r−1)t already-embedded vertices from the other r−1 clusters, and by ε-regularity each step shrinks the candidate pool in V_a by a factor of at least γ − ε ≥ γ/2. Because G is H-free, R must be K_r-free! Applying Turán's theorem (Chapter 2) to the macro graph R gives |E(R)| ≤ (1 − 1/(r−1))·C(k,2). Even if every edge of R represents a completely full cluster pair of size (n/k)², the surviving edges of G number at most |E(R)|·(n/k)² ≤ (1 − 1/(r−1))·(k(k−1)/2)·(n²/k²) ≤ (1 − 1/(r−1))·C(n,2). Adding back the escrow of at most (5/8)δn² ≤ 2δ·C(n,2) edges proves e(G) ≤ (1 − 1/(r−1) + 2δ)·C(n,2) for all sufficiently large n. ∎

Notice what happened, because it is the chapter's signature move: the question about G was transferred by regularity to a question about a graph R on k vertices — a *small* graph, where Turán's theorem from Chapter 2 applies exactly. Extremal questions at scale n reduce to exact answers at bounded scale, plus noise. The machine census pins the exact small end of the same story — for K₄ at n = 5 and K₃, K₄ at n = 6, the Atlas enumerated every labeled graph: **ex(5, K₄) = 8, ex(6, K₃) = 9, ex(6, K₄) = 12**, and the extremal graphs are *exactly* the Turán graphs — all 15 labeled copies of T₃(5) (parts 2,2,1), all 10 of K₃,₃, all 15 of K₂,₂,₂ (parts 2,2,2). Structure and count both machine-exact: Turán's equality case is rigid even before the asymptotics begin.

**✎ Checkpoint.** Erdős–Stone predicts ex(6, C₅) ≈ (1 − 1/1)·C(6,2) = 0?? Read the formula's small print: χ(C₅) = 3, so the first-order term is (1 − 1/2)·15 = 7.5. The machine-exhaustive answer is **ex(6, C₅) = 9**, with 85 labeled extremal graphs (the Atlas census, run because recall guessed 12 and was wrong: K₂,₂,₂ *looks* like a candidate at 12 edges, but it is tripartite, not bipartite, and hosts the 5-cycle a₁–b₁–c₁–a₂–b₂–a₁). The missing 1.5 edges live in the o(n²) — the correction is lower-order but not zero, and it separates C₅ from K₃ only at scale (at n = 6 both maxima are exactly 9, though with wildly different extremal censuses: 85 labeled graphs vs. the 10 rigid K₃,₃ copies). The full story is the Erdős–Simonovits compact form, which the exercises unpack.

Erdős–Stone is a *counting* theorem: it says near-extremal H-free graphs have nearly (1 − 1/(χ−1))C(n,2) edges. The stability phenomenon is the structural upgrade:

> **Simonovits stability.** For every fixed graph H with χ(H) ≥ 2 and every ε > 0 there exist δ > 0 and n₀ such that if an H-free graph on n ≥ n₀ vertices has at least (1 − 1/(χ(H)−1) − δ)·C(n,2) edges, then it can be made (χ(H)−1)-partite by deleting at most ε·C(n,2) edges. (Simonovits, "A Method for Solving Extremal Problems in Graph Theory", Proc. Colloq. Tihany 1966, 1968, 279–319.)

In words: a graph within ε of the extremal *count* is within ε of the extremal *configuration*.

*Proof of Simonovits stability from reduced-graph Turán stability.* Apply the Erdős–Stone regularity reduction to an H-free graph G with e(G) ≥ (1 − 1/(r−1) − η)·C(n,2) (r = χ(H)), using density threshold γ ≪ ε and regularity tolerance ε₁ ≪ γ. Because R is K_r-free and the cleaning escrow removes at most γn² edges, the surviving edge count in G forces the reduced graph R on k vertices to satisfy |E(R)| ≥ (1 − 1/(r−1) − (η + 2γ))·C(k,2). By the exact stability of Turán's theorem for K_r-free graphs (proved by induction or Zykov symmetrization: any K_r-free graph on k vertices within δ′k² edges of T_{r−1}(k) can be made (r−1)-partite by deleting at most O(δ′)k² edges), R can be made (r−1)-partite by deleting at most C·(η + 2γ)k² edges of R. Lift this (r−1)-coloring of V(R) back to V(G) by assigning every vertex in cluster V_i the color of i in R. Any monochromatic edge of G under this (r−1)-partition either lies in the cleaning escrow (≤ γn² edges) or comes from one of the ≤ C·(η + 2γ)k² deleted edges of R (≤ C·(η + 2γ)k²·(n/k)² = C·(η + 2γ)n² edges). Choosing η, γ small enough that γ + C·(η + 2γ) ≤ ε/2 leaves at most ε·C(n,2) monochromatic edges to delete. ∎

The Atlas ran stability as a brute-force census at n = 6, one edge below the K₄-extremal 12 — and the small end is *sharper than the theorem promises*: all **240** labeled 11-edge K₄-free graphs on 6 vertices are *already 3-partite* — the deletion distance to the 3-partite class is zero, not merely small, for every single one (checked against all 90 partitions of 6 vertices into 3 nonempty blocks). The finer distance to the *specific* Turán graph K₂,₂,₂ — the minimum number of edge changes (delete plus add) to reach some labeled copy — splits the 240 into exactly two structural types: **180 graphs at edit distance 1** (K₂,₂,₂ minus one edge; note 15 copies × 12 choices = 180, every labeled instance accounted) and **60 at edit distance 3** (the complete 3-partite K₃,₂,₁; 6!/(3!2!1!) = 60 labeled copies), mean edit distance 1.5, maximum 3. One edge below extremal, the K₄-free universe consists of the Turán graph's immediate neighborhood and nothing else — the Simonovits tableau at census scale.

**✎ Checkpoint.** Before the census was run, the plausible guesses were "mostly 3-partite, a few exotics at deletion distance 1 or 2". The machine found *zero* exotic deletion distance. Predict the analogous answer at 10 edges (two below extremal) before you run Part 6 of the Lab — and be prepared to be surprised: structure decays fast, but where exactly it breaks is census territory, not intuition territory.

Carry forward: regularity transfers scale-n questions to bounded-scale exact ones; near-extremal rigidity is real and census-checkable. Lecture 4 now aims the whole machine at a target that is not a graph at all: the integers.

---

## Lecture 4 · Roth's Theorem: Combinatorics Fires at the Integers

Here is the payoff of the whole machine, and it aims outside graph theory entirely. Say a set A ⊆ {1, …, N} is *3-AP-free* if it contains no three distinct terms in arithmetic progression. How large can A be? In 1946 Behrend built such sets with N·e^{−O(√(log N))} elements — density decaying to zero, but barely. In 1953 Roth proved that *any* set of positive density must contain a 3-AP: the Behrend scale is close to the truth. (Roth, "On certain sets of integers", *J. London Math. Soc.* s1-28(1), 1953, 104–109, DOI 10.1112/jlms/s1-28.1.104.)

> **Roth's theorem.** For every δ > 0 there is N₀(δ) such that every A ⊆ {1, …, N} with |A| ≥ δN and N ≥ N₀ contains x, y, z distinct with x + z = 2y.

Roth's own proof was Fourier analysis — a density-increment argument. The proof below is the later, purely combinatorial route: triangle removal. It is the chapter's centerpiece construction, so the Atlas machine-verified every structural claim in it before a word was printed.

**The construction.** Let A ⊆ Z_n, n odd (2 invertible). Build a tripartite graph G(A) on parts V₁, V₂, V₃, each a copy of Z_n, with edges:

- E₁₂: x ∈ V₁ to x + s ∈ V₂, for every s ∈ A and every x;
- E₂₃: x ∈ V₂ to x + s ∈ V₃, for every s ∈ A and every x;
- E₃₁: z ∈ V₃ to x ∈ V₁, for every s ∈ A and every x with z − x = 2s.

Walk around a triangle x, y, z: its edge differences are s₁ = y − x ∈ A, s₂ = z − y ∈ A, and (z − x)/2 = s₃ ∈ A. But s₁ + s₂ = 2s₃ — the three differences are *themselves a 3-term arithmetic progression of A*, in order (s₁, s₃, s₂). Two regimes:

- **Genuine triangles** (s₁ ≠ s₂): a *nontrivial* 3-AP inside A.
- **Degenerate triangles** (s₁ = s₂ = s₃): the "progression" is trivial; these triangles exist always, one per (x, s) pair.

So: **A is 3-AP-free if and only if every edge of G(A) lies in exactly one triangle** (the degenerate one). The Atlas verified this equivalence *exhaustively* — every subset A of Z_n, for n = 5, 7, 9: all 32, 128, 512 subsets respectively, **zero mismatches** in either direction; 16, 43, 127 AP-free sets respectively; largest AP-free sets of sizes 2, 3, 4 (for instance {0, 1, 3, 4} in Z₉). And in the AP-free regime the census pins the bookkeeping exactly: #triangles = n·|A| (only the degenerate survive), #edges = 3n·|A|, and — brute-forced over all deletion subsets at n = 5 — the minimum number of edges whose deletion kills all triangles is **exactly the number of triangles**, forced by the edge-disjointness: every edge belongs to its own private triangle, so no deletion serves two masters. Five singleton sets tested, five answers, all 5 = #triangles.

**✎ Checkpoint.** In G(A) with A AP-free, each edge sits in exactly one triangle. Before reading on: what is the *fewest* edges you must delete to destroy all triangles — could a clever deletion ever kill two birds? (The census says no: edge-disjoint triangles pay one deletion each, always.)

**The proof of Roth.** Let A ⊆ {1, …, N} be 3-AP-free, |A| = δN. Choose a prime p with 2N < p < 4N (Bertrand's postulate — a prime lies strictly between m and 2m for m > 1, applied with m = 2N — so the window is never empty for N ≥ 1). Regard A as a subset of Z_p: since p > 2N, no mod-p progression inside A can wrap: if x, y, z ∈ A with x + z ≡ 2y (mod p), then x + z and 2y both lie in [0, 2N], a range shorter than p, so the congruence forces equality x + z = 2y — a genuine three-term progression, which A forbids (machine-checked: 554 congruence-forcing triples across the 27 pairs (N, p) with N ≤ 9 and p prime in (2N, 4N), zero counterexamples). So A is 3-AP-free in Z_p too. Form G(A) on the tripartite skeleton with n = p. Then:

1. **Triangles are few.** Every triangle is degenerate (AP-freeness), so #triangles = p|A| ≤ pN < p²/2. The graph has n = 3p vertices, so the triangle count is O(p²) = o(n³).
2. **Edges are many.** #edges = 3p|A| ≥ 3p·δN ≥ 3p·δ(p/4) = (3/4)δp² = Θ(p²), since p ≤ 4N gives N ≥ p/4.
3. **Apply triangle removal.** The graph can be made triangle-free by deleting at most εp² edges for any fixed ε, once p is large — o(p²) deletions.
4. **But edge-disjointness demands more.** Because A is 3-AP-free in Z_p, the p|A| degenerate triangles (x, x+s, x+2s) are pairwise *edge-disjoint*: an edge between V₁ and V₂ fixes x and x+s (hence s), an edge between V₂ and V₃ fixes x+s and x+2s (hence s and x), and an edge between V₃ and V₁ fixes x and x+2s (hence s, since 2 is invertible mod p). Because no single edge belongs to two triangles, destroying all p|A| triangles requires deleting at least one edge from each — so at least p|A| = pδN > (δ/4)p² edge deletions (using p < 4N). Choosing the removal parameter δ_rem = δ/36 in Step 3 guarantees that all triangles can be destroyed by deleting at most δ_rem·(3p)² = (δ/4)p² edges once p is large enough that p|A| < p²/2 ≤ ε(δ_rem)·(3p)³ — a direct contradiction. ∎

Sit with step 4, because it is the whole trick dressed in one line: *removal promises few deletions suffice; the construction's rigid, edge-disjoint triangle cover forbids it.* The machine census verified the rigidity exhaustively at small scale; the proof lifts it to every scale. Note honestly what the proof costs: triangle removal's ε–δ dependence runs through the regularity lemma (even under Fox's 2011 regularity-free improvement, a tower of height O(log(1/δ))), whereas Roth's 1953 Fourier density-increment proof gives N₀(δ) ≤ exp(exp(O(1/δ))), Bourgain (1999, 2008) and Sanders (2011) pushed the Fourier/quasi-polynomial method down to δ ≥ (log N)^{−1+o(1)}, and Kelley–Meka (2023) achieved the Behrend-like quasi-polynomial bound δ ≥ exp(−O((log N)^{1/12})).

**✎ Checkpoint.** Behrend says AP-free sets of size N·e^{−O(√(log N))} exist; Roth says density δ needs N₀(δ). Why is Behrend *not* a counterexample to Roth? (Answer: e^{−O(√(log N))} → 0 — Behrend's density is not positive; both statements live happily together, and the true shape of the extremal scale — polynomial? barely-exponential? — is *the* open problem of the area, recently sharpened by Kelley–Meka 2023, statement-level here.)

The same template — encode forbidden arithmetic structure as triangles in a layered graph, quote removal, cash the contradiction — generalizes: 4-term progressions need *hypergraph* removal (Nagle–Rödl–Schacht, and Gowers, independently — the honest boundary of this chapter: stated, not proved), and full Szemerédi (all progression lengths) follows. That is Lecture 5's map. And the density-increment idea Roth used by hand — *if the structure is nowhere, some refinement gains density* — returns in Lecture 6 as the Meshulam prior that the cap set theorem demolished.

---

## Lecture 5 · Density Ramsey: From Coloring to Counting

Van der Waerden's theorem (Chapter 10) is a *coloring* statement: finitely many colors, one monochromatic progression, forced. Its density upgrade asks the sharper question — how *few* points can a set keep while dodging all k-term progressions? Roth answered k = 3 last lecture; the general case is the theorem the whole field is named for:

> **Szemerédi's theorem.** For every k ≥ 3 and δ > 0 there is N₀(k, δ) such that every A ⊆ {1, …, N} with |A| ≥ δN, N ≥ N₀, contains k distinct terms in arithmetic progression. (Szemerédi, "On sets of integers containing k elements in arithmetic progression", *Acta Arith.* 27(1), 1975, 199–245; k = 3 is Roth 1953; k = 4 was Szemerédi's combinatorial proof with a second proof by Roth in 1972.)

The small scale shows the rigidity the machine census already met in Lecture 4: in Z₅, Z₇, Z₉ the largest 3-AP-free sets have sizes 2, 3, 4 — e.g. {0, 1, 3, 4} in Z₉ — and *every* AP-free set is exactly the degenerate-triangle rigidity profile in its G(A) graph. Density is a promise that scale eventually collects on.

The honest map of proofs — four routes, and the chapter's boundary stated plainly:

1. **The original (1975).** A combinatorial density-increment argument of legendary complexity; the 4-term case alone had taken years. Not given here.
2. **Fourier (Roth, k = 3; extended by others).** The density-increment route: if A has no 3-AP, the balanced indicator's Fourier coefficients reveal a refinement on which density strictly increases; reiterate; density cannot exceed 1. This is the pattern row "Density increment" firing on the integers.
3. **Ergodic (Furstenberg, 1977).** A correspondence transferring the statement to recurrence in measure-preserving systems; it re-proves Szemerédi and generalizes furthest — named, not given.
4. **Hypergraph removal (Nagle–Rödl–Schacht; and Gowers — independent).** The Lecture-4 template, one level up: k-APs in dense sets correspond to edges in a (k−1)-uniform hypergraph, and the *hypergraph* removal lemma (a statement the chapter cites, honestly, without proof — its regularity prerequisites are a book of their own) cashes the same contradiction. This is the route that makes "removal ⟹ density Ramsey" a machine.

One floor above sits the density Hales–Jewett theorem — the combinatorial-lines statement:

> **Density Hales–Jewett.** For every δ > 0 and alphabet size k there is n₀(δ, k) such that every A ⊆ [k]^n with |A| ≥ δ·k^n, n ≥ n₀, contains a combinatorial line — k points differing in one coordinate block. (D. H. J. Polymath, "A new proof of the density Hales–Jewett theorem", *Annals of Mathematics* 175(3), 2012, 1283–1327; arXiv:0910.3926.)

The hierarchy is strict, and each arrow is a genuine theorem: van der Waerden (coloring HJ) is implied by Szemerédi's theorem (a dense one-color set is denser than any of k color classes), and Szemerédi's theorem follows from density HJ — a k-term progression embeds as a combinatorial line in [k]^n restricted to a suitable slice of constant coordinate-sum. The chapter states each implication at the level of "what embeds in what" and proves none of them; that honesty is deliberate — the implications are standard but their proofs are transfers, not one-liners.

**✎ Checkpoint.** Density HJ at k = 2: subsets of the binary cube {0,1}^n of density δ contain a combinatorial line — which in [2]^n is a pair of points a, b ∈ {0,1}^n obtained by setting a non-empty wildcard coordinate set W ⊆ [n] to all 0s vs. all 1s while holding [n]∖W fixed, i.e., a pair of comparable subsets A ⊊ B ⊆ [n]. What famous theorem is the k = 2 case? (Answer: Sperner's theorem, Chapter 7's opening result — an antichain in the Boolean lattice has size at most C(n,⌊n/2⌋) = Θ(2ⁿ/√n) = o(2ⁿ), so density o(1). The whole density-Ramsey tower stands on the case you already know.)

The machine side of this lecture is deliberately thin — the content is statements and hierarchy, not computation — but the tower table of Lecture 1 is the honest reason: every quantitative window in this chapter (removal tolerances, hence Szemerédi's N₀ via the removal route) is tower-infested, and the Polymath proof of density HJ, a fully combinatorial argument discovered by mass collaboration, was celebrated precisely for dodging the regularity machinery.

## Lecture 6 · The Cap Set Theorem: The Polynomial Method Returns

Back to F₃ⁿ — the n-dimensional vector space over {0, 1, 2} — for the chapter's closing theorem, and the one with the youngest proof. A *cap* is a set containing no three distinct points x, y, z with x + y + z = 0 — no three points collinear, since in F₃ a line is exactly such a triple. How large can a cap be?

**✎ Checkpoint.** Guess the sequence of maximum caps in F₃ⁿ for n = 1, 2, 3, 4, 5 before reading on — and guess whether the ratio between consecutive terms stays near 3, or decays.

The machine answers, run to the chapter's standing rule (exhaustive where feasible, flagged where not): n = 1: **2** (exhaustive over all 8 subsets); n = 2: **4** (exhaustive, 512 subsets); n = 3: **9** — proved exact by a full-tree search over all 27 points (647,644 nodes, no pruning shortcuts, an exhibit verified pairwise); n = 4: **20** — a 20-cap found and pairwise-verified by seeded search (Lehmer seed 20261053), *optimality cited from the literature, not machine-proved here* (the proof-by-search attempt exceeded the recorded compute budget — the receipt says so); n = 5: **45** — found and verified by plateau-accepting iterated local search (seed 20261055; the naive variant stalled at 39, an honest search-difficulty note), again optimality cited. The ratios 2, 2, 2.25, 2.22, 2.25 already whisper the theorem: caps are exponentially smaller than 3ⁿ.

The known bound landscape, honestly dated: for decades the best upper bound was Meshulam's (2001) C·3ⁿ/n — a Fourier/density-increment argument, the Roth pattern in vector spaces — improved to 3ⁿ/n^{1+ε} by Bateman–Katz (2012). Then in 2016 two papers landed on the arXiv, published together in the same volume of the *Annals* — 185 (2017) — ending the game in one stroke:

> **The cap set theorem (CLP/EG).** A cap in F₃ⁿ has size at most cⁿ with c = 2.7551046130… — explicitly, |A| ≤ 3·M(n, 2n/3), where M(n, d) counts the monomials in n variables with every exponent at most 2 and total degree at most d. (Croot–Lev–Pach, "Progression-free sets in Z₄ⁿ are exponentially small", and Ellenberg–Gijswijt, "On large subsets of F_q^n with no three-term arithmetic progression", *Annals of Mathematics* 185, 2017.)

The constant is *exactly* computable, and the chapter computes it. The exponential growth of M(n, 2n/3) is governed by c = min_{0<x<1} (1 + x + x²)/x^{2/3}: the calculus is one line — the minimizer satisfies 4x² + x − 2 = 0, so x* = (√33 − 1)/8 = 0.593070330817 — and the Atlas verified it by an independent dense-scan plus golden-section minimization agreeing to all twelve printed decimals: **c = 2.755104613024**. (The literature's headline "2.756" is this same value rounded; the chapter prints the exact one.)

*The proof, in its EG slice-rank form — the direct descendant of Chapter 6's polynomial method (Lecture 3 there), with the same two beats: wrap the structure in a polynomial, count monomials.*

**Beat 1 — the polynomial 3-tensor on A × A × A.** In F₃ⁿ, three points x, y, z ∈ A form a 3-term arithmetic progression (or collinear triple) if and only if x + y + z = 0 (since x + z = 2y ⟺ x + y + z = 3y = 0 in F₃ⁿ, and if any two of x, y, z are equal, x + y + z = 0 forces all three to be equal). Thus A ⊆ F₃ⁿ is a cap if and only if for all x, y, z ∈ A: x + y + z = 0 ⟺ x = y = z. Consider the polynomial P : F₃ⁿ × F₃ⁿ × F₃ⁿ → F₃ defined by P(x, y, z) = Π_{i=1}^n (1 − (xᵢ + yᵢ + zᵢ)²). By Fermat's little theorem in F₃, u² = 1 for every u ∈ F₃∖{0} and 0² = 0. Hence P(x, y, z) = 1 if x + y + z = 0 in F₃ⁿ, and P(x, y, z) = 0 otherwise. Restricted to A × A × A, the cap property implies that P is the Kronecker delta tensor: T(x, y, z) = P(x, y, z)|_{A×A×A} equals 1 if x = y = z ∈ A, and 0 otherwise.

**Beat 2 — Tao's slice-rank formulation.** A 3-tensor T : A × A × A → F has *slice rank* 1 if it can be written in one of the three forms f(x)g(y, z), f(y)g(x, z), or f(z)g(x, y), and the *slice rank* sr(T) is the minimum number of slice-rank-1 tensors that sum to T. Two exact lemmas finish the theorem:

1. **Lower bound (sr(T) = |A| for the diagonal tensor, valid over any field F).** Let T(x, y, z) = Σ_{a∈A} c_a·δ_{x=a}δ_{y=a}δ_{z=a} with c_a ∈ F∖{0}, and suppose T(x, y, z) = Σ_{i=1}^{r₁} f_i(x)g_i(y, z) + Σ_{j=1}^{r₂} h_j(y)k_j(x, z) + Σ_{ℓ=1}^{r₃} u_ℓ(z)v_ℓ(x, y). The subspace V₁ = span{f₁, …, f_{r₁}} ⊆ F^A has dimension d₁ ≤ r₁. By Gaussian elimination, there exists a coordinate subset S₁ ⊆ A of size |S₁| = d₁ ≤ r₁ such that restriction to S₁ is an isomorphism on V₁; hence for every x ∈ A∖S₁ there exist scalars λ_{x,s} ∈ F (s ∈ S₁) such that f(x) = Σ_{s∈S₁} λ_{x,s}·f(s) for all f ∈ V₁. For x, y, z ∈ A∖S₁, define T̃(x, y, z) = T(x, y, z) − Σ_{s∈S₁} λ_{x,s}·T(s, y, z). Because s ∈ S₁ and y, z ∈ A∖S₁ are disjoint (s ≠ y), T(s, y, z) = 0 on (A∖S₁)², so T̃ coincides with the diagonal tensor Σ_{a∈A∖S₁} c_a·δ_{x=a}δ_{y=a}δ_{z=a} on (A∖S₁)³. On the other hand, applying the linear operation f(x) ↦ f(x) − Σ_{s∈S₁} λ_{x,s}·f(s) to the slice decomposition annihilates every f_i(x)g_i(y, z) term while preserving the r₂ mode-2 terms h_j(y)k′_j(x, z) and the r₃ mode-3 terms u_ℓ(z)v′_ℓ(x, y). Repeating the same elimination on mode 2 deletes a subset S₂ ⊆ A∖S₁ of size d₂ ≤ r₂, leaving the diagonal tensor on A″ = A∖(S₁ ∪ S₂) of size |A″| ≥ |A| − r₁ − r₂ expressed purely as Σ_{ℓ=1}^{r₃} u_ℓ(z)v″_ℓ(x, y). Since the |A″| diagonal z-slices {c_z·δ_{x=z}δ_{y=z}}_{z∈A″} are linearly independent and lie in span{v″₁, …, v″_{r₃}}, we must have r₃ ≥ |A″| ≥ |A| − r₁ − r₂, and therefore r₁ + r₂ + r₃ ≥ |A|.
2. **Upper bound (sr(T) ≤ 3·M(n, ⌊2n/3⌋) via monomial degree splitting).** Expand P(x, y, z) = Π_{i=1}^n (1 − (xᵢ + yᵢ + zᵢ)²) into a linear combination of monomials x^α·y^β·z^γ where α, β, γ ∈ {0, 1, 2}ⁿ and the total degree satisfies |α| + |β| + |γ| ≤ 2n. In every monomial with |α| + |β| + |γ| ≤ 2n, at least one of the three degree sums |α|, |β|, |γ| is at most ⌊2n/3⌋ (otherwise |α| + |β| + |γ| > 3·(2n/3) = 2n). Partition the monomials into three sets S₁, S₂, S₃ according to whether |α| ≤ 2n/3, |β| ≤ 2n/3 (and |α| > 2n/3), or |γ| ≤ 2n/3 (and |α|, |β| > 2n/3). Grouping the terms in S₁ by their x-monomial x^α expresses the S₁-sum as Σ_{|α| ≤ 2n/3} x^α·F_α(y, z), which is a sum of at most M(n, ⌊2n/3⌋) slice-rank-1 tensors. Doing the same for S₂ (grouped by y^β) and S₃ (grouped by z^γ) shows sr(T) ≤ 3·M(n, ⌊2n/3⌋).

Chaining the lower and upper bounds yields **|A| = sr(T) ≤ 3·M(n, ⌊2n/3⌋) ≤ 3·cⁿ with c = 2.7551046130.** ∎

The monomial census — machine-run to display the bound's honest texture — counts M(n, ⌊2n/3⌋) exactly: 1, 3, 10, 15, 51, 168, 274, 927 for n = 1..8, so the bounds 3·M read 3, 9, 30, 45, 153, 504, 822, 2781 — against true maxima 2, 4, 9, 20, 45, 112, ... The bound is *slack at small n* (at n = 3 it says 30 where the truth is 9) and tightens only in the exponential rate — the slice-rank weapon is asymptotic, exactly like the Chernoff and entropy bounds of Chapter 13 that lose all constant factors and win the exponent. The chapter's Lab Part 5 hunts caps by seeded search and reproduces the exact small ladder.

**✎ Checkpoint.** The gap 3 → 2.755 is about 8%. Estimate how many extra dimensions it takes for 2.7551ⁿ to beat 3ⁿ by a factor of 100 — and then reconcile with the fact that at n = 5 the bound (153) is 3.4× the truth (45): why both facts can hold at once.

The closing circle: Behrend's 1946 construction — the lower bound for Roth's theorem — is itself a cap in a suitable F₃-like slice of the integers; the cap set theorem is, in a precise sense, Roth's question moved to the cleanest ambient group; and the polynomial method that closed it is Chapter 6's machine, grown up. Density increment (Roth, Meshulam) held the problem for fifty years; the polynomial method ended it in six pages. That alternation — analytic averaging against algebraic structure — is the Atlas's running theme, and this chapter is where it stood up and announced itself.

---

## The Trick Bag (reference card)

| Pattern | Plain language | Where you met it |
|---------|---------------|------------------|
| **P10 Averaging / expectation** | The average is a promise; some object beats it — and a weighted average of squares only grows under refinement | L1 (the index q is averaging with a spotlight; monotonicity is nonnegative variance), L3 (Turán on the reduced graph R), L6 (the monomial count M is an averaged degree budget) |
| **P30 Regularity partitioning** | Every large graph is a bounded quasirandom blow-up of a small pattern graph; refine until the noise is uniform — defects pay rent | L1 (the lemma + the tower), L3 (the escrow-and-reduce proof of Erdős–Stone) |
| **P31 Counting–removal** | Under regularity, copies multiply as density products; few copies therefore mean few deletions | L2 (the counting lemma + the removal lemma), L4 (triangle removal ⟹ Roth) |
| **P32 Stability** | Near the extremal count, objects sit near the extremal *configuration* | L3 (Simonovits; the 240-graph tableau; the 10-edge census where it breaks) |
| **P33 Density increment** | If the structure you want is nowhere, some refinement gains density; iterate to the ceiling | L1 (the index increment), L4 (Roth's Fourier route), L6 (Meshulam's prior) |
| **Polynomial method (Chapter 6's card)** | Wrap the configuration space in a polynomial; the monomial budget is your dimension | L6 (CLP/EG slice rank — Chapter 6's Lecture 3, grown up) |
| **The honest ledger (lore)** | Print what is proved, what is computed, and what is cited — and keep the three apart | The L1 tower-gap table; the cited-not-proved flags of L2, L4, L5; every machine note in this chapter |

**Formula box:** d(X, Y) = e(X, Y)/(|X||Y|); (X, Y) is ε-regular when |d(A, B) − d(X, Y)| ≤ ε for all A ⊆ X, B ⊆ Y with |A| ≥ ε|X|, |B| ≥ ε|Y| (4×4 census at ε = 1/4, 1/2, 3/4: 2 / 46,408 / 65,536 of 65,536; worst witness discrepancy 0.9375). Index q(P) = Σ_{i,j} |V_i||V_j|/n² · d_{ij}², diagonal included, 0 ≤ q ≤ 1; refinement monotone (q(P′) ≥ q(P): 106,496 + 1,638,400 machine checks, zero violations); a defect-refinement pays q(P′) ≥ q(P) + ε⁵/2 (the variance identity: 1,125,000 checks, zero violations), so at most 2ε⁻⁵ rounds and M(ε) a tower of height O(ε⁻⁵) — Gowers' lower bound Ω(ε^{−1/16}); the Fox–Lovász tight order — tower height about ε^{−2} for a version of the lemma — pins the truth. Counting lemma: ε-regular triples with densities ≥ 2ε carry at least (1 − 2ε)(d₁₂−ε)(d₁₃−ε)(d₂₃−ε)|X||Y||Z| triangles, with per-vertex degree-floor product window (d₁₂−ε)(d₁₃−ε)(d₂₃−ε)|X||Y||Z|; without regularity densities lie (hi/lo: all pair densities 1/2, zero triangles, witness discrepancy 1/2). Removal: at most εn^{|H|} copies of H ⟹ at most δn² deletions (δ a tower-inverse of ε; Fox 2011 cuts the tower). Erdős–Stone (χ(H) ≥ 2): ex(n, H) = (1 − 1/(χ(H)−1) + o(1))·C(n,2), π(H) = 1 − 1/(χ(H)−1); Simonovits stability: within δ of the extremal count ⟹ (χ(H)−1)-partite after ε-deletions; census: ex(5, K₄) = 8 (15 labeled), ex(6, K₃) = 9 (10), ex(6, K₄) = 12 (15), ex(6, C₅) = 9 (85); one edge below extremal all 240 K₄-free graphs are 3-partite (180 at edit distance 1, 60 at 3, mean 1.5). Roth: G(A) on three copies of Z_p, p ∈ (2N, 4N) prime; AP-free ⟺ every edge in exactly one triangle (zero mismatches over all subsets, n = 5/7/9); #triangles = p|A|, #edges = 3p|A|; forced deletions ≥ #triangles ≥ (1/4)δp² against removal's o(p²). Ruzsa–Szemerédi (6,3): every edge in exactly one triangle ⟹ o(n²) edges; bipartite form: an edge set partitioning into induced matchings of size ≥ δn ⟹ o(n²); the census cliff: blocks of size ≥ 2 still allow m² − m (extremals = complements of perfect matchings), blocks ≥ 3m/4 collapse to m. Szemerédi: positive density ⟹ k-term progressions, all k ≥ 3 (k = 3 Roth 1953, general 1975); density HJ ⟹ Szemerédi ⟹ van der Waerden. Cap set: |A| ≤ 3·M(n, 2n/3) ≤ 3·cⁿ with c = min_{0<x<1}(1+x+x²)/x^{2/3} = 2.755104613024 at x* = (√33−1)/8; M(n, ⌊2n/3⌋) = 1, 3, 10, 15, 51, 168, 274, 927 (n = 1..8), bounds 3M = 3, 9, 30, 45, 153, 504, 822, 2781, against true maxima 2, 4, 9, 20, 45.

---

## Exercises (graded: ●○○ easy · ●●○ moderate · ●●● tough)

**Exercise 1 (●○○, L1).** A bipartite pair on 4 + 4 vertices. (a) Show that the complete pair K₄,₄ is ε-regular for every ε > 0. (b) Show that the diagonal matching M = {(x_i, y_i)} is *not* ε-regular at ε = 1/4, with an explicit witness. (c) The exhaustive census says exactly 2 of the 65,536 bipartite graphs on 4 + 4 vertices are ε-regular at ε = 1/4 — which two, and why is that the honest reading of the count? [Hint: ε-regularity is a for-all condition; think about what every test set sees when the answer is forced.]

**Exercise 2 (●○○, L1).** Let G be the bowtie: vertices 0…5, edges 01, 04, 14 (triangle {0,1,4}) and 02, 03, 23 (triangle {0,2,3}). Compute the index q for the trivial partition, for P = {0,1,4} ∪ {2,3,5}, and for the singleton partition (diagonal-inclusive convention), and verify the ladder. [Hint: q(P) is a weighted average of squared densities; the within-block density of {0,1,4} is not what your eye guesses first.]

**Exercise 3 (●●○, L1).** (a) Prove: if every defect-refinement raises the index by at least ε⁵/2, the regularity proof needs at most 2ε⁻⁵ rounds. (b) Compute the worst-case round counts at ε = 1/2 and ε = 1/4. (c) The round counts are small — so where does the tower come from? Reconcile with the Lecture 1 exhibit (k ↦ k·2^k reaches 10^619.8 at height 3). [Hint: rounds count refinements; the *part count* is what compounds.]

**Exercise 4 (●●○, L2).** The counting window, numerically. For the machine's config 1 (realized pair densities 0.4911, 0.4911, 0.5044 on parts of size 30; observed triangles 3,307) and config 2 (0.7033, 0.4011, 0.5533; observed 4,202): compute the density-product prediction and the (d − ε)³ lower window at ε = 0.1, and check both observations sit above the window. [Hint: the window is the *product* of the per-pair floors — three factors, not one.]

**Exercise 5 (●○○, L2).** In the hi/lo exhibit of Lecture 2, identify precisely which hypothesis of the counting lemma fails, and exhibit a witness pair proving the failure. [Hint: it is not the densities.]

**Exercise 6 (●●●, L3).** Prove ex(6, K₃) = 9 — by hand, from the triangle-free condition alone — then reconcile with the machine census: exactly 10 labeled extremal graphs, all isomorphic to K₃,₃. [Hint: Mantel's route; equality analysis.]

**Exercise 7 (●●○, L3).** Erdős–Stone arithmetic: compute the Turán density π(H) and the first-order asymptotic of ex(n, H) for H = C₄, K₅, and K₅ with one edge deleted. Which pair does the theorem refuse to distinguish, and what resolves them at lower order? [Hint: what does the theorem actually see of H?]

**Exercise 8 (●●○, L3).** The stability tableau. Given: all 240 labeled 11-edge K₄-free graphs on 6 vertices are already 3-partite; 180 sit at edit distance 1 from K₂,₂,₂ and 60 at distance 3. Reconstruct both structural types and verify the counts 180 and 60 arithmetically. [Hint: count labeled copies of each type.]

**Exercise 9 (●●○, L4).** Hands on the Roth construction with A = {0, 1, 3} ⊆ Z₇: (a) verify A is 3-AP-free; (b) compute #edges and #triangles of G(A); (c) confirm every edge lies in exactly one triangle. [Hint: midpoints, mod 7 — there are only three pairs to check in (a).]

**Exercise 10 (●●●, L4).** Assemble the full Roth contradiction: given triangle removal (o(n³) triangles ⟹ o(n²) deletions suffice) and the G(A) bookkeeping (AP-free A of size δN inside Z_p, p ∈ (2N, 4N) prime), show the two bounds collide for large N. Work the numeric skeleton at δ = 0.1. [Hint: deletions needed ≥ #triangles; count both sides as multiples of p².]

**Exercise 11 (●●○, L5).** The density ladder: (a) verify the maximum 3-AP-free sizes 2, 3, 4 in Z₅, Z₇, Z₉ (exhibit sets; argue no larger set works in Z₅); (b) justify each arrow of van der Waerden ⟸ Szemerédi ⟸ density HJ in one line. [Hint for (a): in Z₅ every 3-subset has a pair whose midpoint lands in the set — count pairs.]

**Exercise 12 (●●○, L6).** The EG constant: (a) derive the minimizer condition 4x² + x − 2 = 0 for f(x) = (1 + x + x²)/x^{2/3}; (b) compute c to six decimals; (c) compute M(3, 2) by listing every monomial, and compare 3M with the true maximum cap in F₃³. [Hint: logarithmic differentiation tames x^{−2/3}.]

### ◆ Pattern-unknown problems (no hints; the diagnosis is the point)

**◆ Problem 1.** Prove that the largest cap in F₃³ has exactly 9 points.

**◆ Problem 2.** Classify, up to isomorphism, every graph on 6 vertices in which every edge lies in exactly one triangle.

**◆ Problem 3.** Prove: a 3 + 3 bipartite graph whose edges partition into induced matchings of size at least 2 has at most 6 edges; and if it has exactly 6, its missing cells form a perfect matching and the blocks are the transposition pairs.

### ◐ Explorations (what you should find, not a number to match)

**◐ Exploration 1.** The tower gap: upper height O(ε⁻⁵), lower Ω(ε^{−1/16}) — the order pinned by Fox–Lovász for a version of the lemma. Find the ε at which the *upper* bound's tower first exceeds height 5, and work out which quantitative statements of Lectures 2 and 4 would collapse to usable bounds if the true height were the lower one.

**◐ Exploration 2.** Hypergraph removal ⟹ Szemerédi: sketch the correspondence between 4-term progressions and edges of a 3-uniform hypergraph on a layered vertex set, and identify precisely where hypergraph regularity is needed where the graph proof used ordinary regularity. (Statement-level; the Atlas boundary is Chapter 14's Lecture 5.)

**◐ Exploration 3.** Behrend (1946) vs. Kelley–Meka (2023): find both bounds' exact forms, and quantify the gap — in orders of magnitude of N — between Behrend's e^{−O(√(log N))} and the 2023 improvement. What kind of proof does Kelley–Meka add to the toolbox?

---

## Answers to the Exercises

**Answer 1.** (a) In K₄,₄ every test density is 1 = d(X, Y) — the for-all condition holds vacuously at every tolerance. (b) The matching has d(X, Y) = 4/16 = 1/4; the test sets A = {x₁}, B = {y₁} are admissible at ε = 1/4 (|A| = 1 = ε·4) and see d(A, B) = 1, discrepancy 3/4 > ε. Not ε-regular. (c) The two are the **empty and the complete graph** — machine-verified (census masks 0 and 65,535): at a meaningful tolerance, ε-regularity is a genuine structural property that *only trivial densities force for all test sets*. That is why the regularity lemma is a theorem and not a formality: it manufactures this rare property from nothing.

**Answer 2.** Bowtie: within {0,1,4} all three edges are present (01, 04, 14 — the eye drops 04), so d = 6/9 = 2/3; cross-density d({0,1,4}, {2,3,5}) = 2/9 (edges 02, 03); within {2,3,5}: d = 2/9 (edge 23). Then q(trivial) = (12/36)² = 1/9 ≈ 0.1111; q(P) = (9/36)(2/3)² + (9/36)(2/9)² + 2·(9/36)(2/9)² = 4/27 ≈ 0.1481; q(singletons) = 12·(1/36)·1 = 1/3 (twelve ordered adjacent singleton pairs, each contributing weight 1/36). The ladder 1/9 ≤ 4/27 ≤ 1/3 — machine-verified exhaustively at n = 5, 6 with zero violations (receipt 52runs-1).

**Answer 3.** (a) 0 ≤ q ≤ 1 and each defect round adds ≥ ε⁵/2: at most 2ε⁻⁵ rounds before the partition is ε-regular (else q would pass 1). (b) ε = 1/2: 2·2⁵ = **64 rounds**; ε = 1/4: 2·4⁵ = **2,048 rounds**. (c) The rounds are few but each multiplies the *part count* by up to 4 per defective pair — part growth compounds like k ↦ 4^k per round, and compounding is where towers come from: the Lecture 1 exhibit's iteration k ↦ k·2^k passes 10^80 and 10^100 at height 3 with only three doublings of doubling. Few rounds, galactic parts.

**Answer 4.** Config 1: product = 0.4911·0.4911·0.5044·30³ = **3,285** (observed 3,307, 100.7%); window = (0.3911)(0.3911)(0.4044)·27,000 = **1,670** ≤ 3,307 ✓. Config 2: product = 0.7033·0.4011·0.5533·27,000 = **4,215** (observed 4,202, 99.7%); window = (0.6033)(0.3011)(0.4533)·27,000 = **2,224** ≤ 4,202 ✓. Both runs sit above the floor the lemma promises, within 0.7% of the product prediction — regularity, where it holds, is quantitative honesty itself.

**Answer 5.** The failed hypothesis is pairwise **ε-regularity** (the densities are honest 1/2). Witness: X = {0,1,2,3} ⊆ X-part, Y = {8,9,10,11} ⊆ Y-part — all-low against all-high sees d(X, Y) = 0 against the pair's 1/2, discrepancy exactly 1/2 = the maximum possible (machine: also the max over 2,000 seeded test pairs).

**Answer 6.** The sharp route is a degree sum with Cauchy–Schwarz behind it. For any edge xy of a triangle-free graph, the neighborhoods N(x) and N(y) are *disjoint* (a shared neighbor z would close the triangle xyz), so d(x) + d(y) ≤ n. Summing over all m edges: Σ_{xy∈E}(d(x) + d(y)) = Σ_v d(v)² ≤ mn. Cauchy–Schwarz turns this into an edge budget: (Σ_v d(v))² ≤ n·Σ_v d(v)², i.e. (2m)² ≤ n·mn = mn², so **m ≤ n²/4 = 9**. Equality forces every inequality tight: d(x) + d(y) = n for every edge and all degrees equal n/2 = 3 — each edge's endpoint neighborhoods partition the vertex set, and following any vertex across an edge shows the graph is bipartite with parts of size 3 and all cross edges present: exactly K₃,₃. Labeled copies = C(6,3)/2 = **10** — every labeled extremal is a K₃,₃, matching the machine census (receipt 52runs-5: exhaustive over all 32,768 graphs, 10 extremals, all complete bipartite 3+3).

**Answer 7.** π(C₄) = 1 − 1/(2−1) = 0: ex(n, C₄) = o(n²) — the true scale is Θ(n^{3/2}), a fact Erdős–Stone is *blind to* (χ(C₄) = 2 collapses the first-order term to 0; the honest note: bipartite H live entirely in the o(n²)). π(K₅) = 1 − 1/4 = 3/4; π(K₅ − e) = 1 − 1/4 = 3/4 as well, since χ(K₅ − e) = 4 (the two non-adjacent vertices share a color). The theorem cannot distinguish them: both are (3/8 + o(1))n² at first order. The resolution at lower order: the exact large-n extremal values differ (K₅ − e is *easier* to host — ex(n, K₅ − e) > ex(n, K₅) for all large n), a Simonovits-method fact the chapter flags rather than proves.

**Answer 8.** Type 1: K₂,₂,₂ minus one edge — labeled copies: 15 labeled K₂,₂,₂ (partitions into three pairs) × 12 deletable edges = **180** ✓. Type 2: K₃,₂,₁ — the complete 3-partite graph with parts of sizes 3, 2, 1: labeled copies = 6!/(3!·2!·1!) = **60** ✓. 180 + 60 = 240: the census found *nothing else* — every 11-edge K₄-free graph on 6 vertices is one of these two (all 240 already 3-partite; the K₃,₂,₁ type is 3-partite but not a subgraph of any K₂,₂,₂ — hence its edit distance 3: 1 deletion to sever the moved vertex from the singleton part, plus 2 additions to join it to its two former part-mates, reaching the 12-edge Turán shape K₂,₂,₂ — machine-verified symmetric differences).

**Answer 9.** (a) Midpoints of the three pairs: (0,1) → 4, (0,3) → 5, (1,3) → 2 — none in A ✓ (all mod 7, inv2 = 4). (b) #edges = 3·7·3 = **63**; #triangles = 7·3 = **21** (all degenerate: only (x, x+s, x+2s) survive). (c) Machine census: every edge in exactly one triangle — the AP-free ⟺ unique-triangle equivalence holds with zero mismatches over all 128 subsets of Z₇.

**Answer 10.** With |A| = δN and N ≥ p/4 (p ≤ 4N): edges = 3p|A| ≥ 3p·δ(p/4) = (3/4)δp², and the forced deletions — one per triangle, since the triangles are edge-disjoint — are at least #triangles = p|A| ≥ (1/4)δp². Triangle removal supplies o(p²) deletions. For p large, o(p²) < (1/4)δp²; at δ = 0.1 the construction demands ≥ 0.025p² deletions while removal allows εp² for any fixed ε once p is large enough that ε < 0.025 — contradiction. The machine pins the floor honestly at brute-force scale: at n = 5, all five singleton constructions need exactly #triangles = 5 deletions (exhaustive over all 2^15 deletion sets — no clever sharing exists).

**Answer 11.** (a) Exhibits: {0,1} in Z₅, {0,1,3} in Z₇, {0,1,3,4} in Z₉. No larger set in Z₅: any 3-subset of Z₅ contains a 3-AP (concretely, machine-checked on all ten 3-subsets: the midpoints of the pairs of any 3-subset cover the two elements outside it). The machine's exhaustive census: 16, 43, 127 AP-free subsets and maxima exactly 2, 3, 4 (receipt 52runs-3). (b) Sz ⟹ vdW: in any k-coloring some color class has density ≥ 1/k (pigeonhole), and Szemerédi finds progressions in positive-density sets — the density hypothesis is *weaker*, so the conclusion is stronger. dHJ ⟹ Sz: embed {1,…,N} into the slice of [k]^n of constant coordinate sum; k-term progressions surface as combinatorial lines, so a dense AP-free set would be a dense line-free set — forbidden by dHJ. (Each implication is a theorem the chapter states; the small print is at Lecture 5.)

**Answer 12.** (a) f'(x) = x^{−2/3}(1 + 2x) − (2/3)x^{−5/3}(1 + x + x²) = 0 ⟺ 3x(1 + 2x) = 2(1 + x + x²) ⟺ **4x² + x − 2 = 0**; the root in (0, 1) is x* = (√33 − 1)/8 ≈ 0.593070. (b) c = f(x*) = **2.755105** to six decimals (machine: 2.755104613024, with an independent numeric minimization agreeing to all twelve printed decimals). (c) M(3, 2) = **10**: 1, x, y, z, x², y², z², xy, xz, yz. The bound 3M = 30 against the true maximum 9 — the slice-rank weapon is asymptotic: it concedes a factor of 3+ at n = 3 and wins the exponential rate as n grows (30 vs 9 at n = 3; 153 vs 45 at n = 5; the ratio decays toward 1 in *rate*, never in constant).

### Answers to the ◆ problems (receipt-backed)

**◆ 1.** The machine's proof is a full-tree search over the 27 points with bound-pruning (647,644 nodes, no shortcuts — receipt 52runs-4); first, a 9-cap in F₃³ exists: the exhibit A₉ = {(0,0,0), (1,0,0), (0,1,0), (1,1,0), (0,0,1), (1,0,1), (2,1,1), (2,2,1), (2,1,2)} has 9 points and is pairwise-verified to contain no collinear triple. The hand proof that no 10-cap exists:

1. **Step 1 (max cap in F₃² is 4).** The affine plane F₃² can be partitioned into 3 parallel lines of 3 points each; a cap can contain at most 2 points per line, so at most 6 points. If a cap B ⊆ F₃² had 5 points, pick any point p ∈ B: the 4 lines through p in F₃² (one in each of the 4 directions) partition F₃²∖{p} into 4 pairs, and B∖{p} can contain at most 1 point from each of these 4 lines, so |B∖{p}| ≤ 4, i.e., |B| ≤ 5. Moreover, if |B| = 5, then for *every* p ∈ B, each of the 4 lines through p contains a second point of B, so every line in F₃² meets B in 0 or 2 points. Counting the C(5,2) = 10 pairs of points in B: each pair determines a distinct line of F₃² (since no 3 points of B are collinear), so B determines 10 distinct 2-secant lines. Thus out of the 12 lines in F₃², 10 meet B in 2 points and 2 meet B in 0 points. Those 2 zero-secant lines have a union of 6 points (if parallel) or 5 (if intersecting) — either way at most 9 − 5 = 4 points of the plane remain for B, contradicting |B| = 5. Thus every cap in F₃² has size at most 4.
2. **Step 2 (plane slicing in F₃³).** Suppose A ⊆ F₃³ is a cap of size |A| = 10. Any parallel family of 3 affine planes H₀, H₁, H₂ partitions A, and by Step 1 each plane contains at most 4 points of A. Since 10 = 4 + 4 + 2 = 4 + 3 + 3, no plane can contain 0 or 1 point of A: **every affine plane in F₃³ meets A in 2, 3, or 4 points!**
3. **Step 3 (plane pencil around a 2-secant line).** For any line L ⊆ F₃³ containing 2 points of A (|A ∩ L| = 2), the 4 affine planes P₁, P₂, P₃, P₄ containing L partition F₃³∖L, so their intersections with A∖L partition the 10 − 2 = 8 points of A∖L. By Step 1, each plane Pᵢ satisfies |A ∩ Pᵢ| ≤ 4, so |(A∖L) ∩ Pᵢ| ≤ 4 − 2 = 2. Because Σ_{i=1}^{4} |(A∖L) ∩ Pᵢ| = 8 and each summand is at most 2, equality |(A∖L) ∩ Pᵢ| = 2 — and hence |A ∩ Pᵢ| = 4 — must hold for all four planes Pᵢ! Thus **every affine plane in F₃³ that contains at least two points of A (and hence contains the 2-secant line through them) must contain exactly 4 points of A.** Combine this with Step 2 (every affine plane meets A in at least 2 points): it follows that *every* affine plane in F₃³ must contain 4 points of A, which is impossible since 3 parallel planes would then contain 4 + 4 + 4 = 12 ≠ 10 points of A. Contradiction! Thus |A| ≤ 9. ∎

The receipt stands as the oracle; the census confirms 2, 4, 9 for n = 1, 2, 3 exactly.

**◆ 2.** Four isomorphism types: the **empty graph** (1 labeled copy — vacuous), the **single triangle** (C(6,3) = 20 labeled), the **bowtie** — two triangles sharing one vertex (6 choices of center × 15 ways to pair four of the remaining five into two pairs = 90 labeled), and the **disjoint triangle pair** (10 labeled: partitions of 6 into two triples). Total **121** labeled graphs; maximum edges **6**, achieved exactly by the bowtie and the disjoint pair (100 labeled at the maximum — receipt 52runs-6, exhaustive over all 32,768 graphs).

**◆ 3.** Six edges on 9 cells means 3 missing cells. Each 2-block {(a,b),(c,d)} of an induced-matching partition forces its two cross cells (a,d) and (c,b) to be *absent*. With three blocks and only three absent cells, every absent cell must serve as the cross cell of exactly two blocks; chasing the incidence structure (block₁'s cross cell is block₂'s, etc., around the cycle of three) forces the three absent cells to share no row or column — a perfect matching — and the blocks to be exactly the transposition pairs {(i,j),(j,i)} around it. The census confirms: exactly **6** labeled 6-edge examples = the 3! perfect matchings of K₃,₃ (receipt 52runs-6, v3).

---

## Computational Lab (verified)

*Six parts, one per lecture. Exhaustive where the chapter's receipts are exhaustive; seeded where they are sampled — no `random` module anywhere: a Lehmer generator (x ← 48271·x mod 2³¹−1) draws every coin, and each part records its seeds and draw rules. The printed outputs are the recorded run outputs (receipts 52runs-1..7): the exhaustive parts re-verify exactly, and every seeded part states its rule — change a seed and you get different samples, never different theorems.*

### Part 1 — The ε-regular pair checker (Lecture 1)

```python
from math import ceil
from itertools import combinations

def density(mask, m, A, B):               # cell (a, b) -> bit a*m + b
    e = sum((mask >> (a*m + b)) & 1 for a in A for b in B)
    return e / (len(A) * len(B))

def max_disc(mask, m, eps):               # worst admissible test pair
    d = density(mask, m, range(m), range(m))
    t = ceil(eps * m)
    subs = [S for k in range(t, m + 1) for S in combinations(range(m), k)]
    return max(abs(density(mask, m, A, B) - d) for A in subs for B in subs)

for eps in (0.25, 0.5, 0.75):
    reg, worst = 0, 0.0
    for mask in range(1 << 16):           # all 65,536 bipartite 4x4 pairs
        disc = max_disc(mask, 4, eps)
        reg += disc <= eps
        if eps == 0.25: worst = max(worst, disc)
    extra = f", worst witness {worst}" if eps == 0.25 else ""
    print(f"eps={eps}: {reg} regular of 65536{extra}")
```

**Verified output.** `eps=0.25: 2 regular of 65536, worst witness 0.9375` / `eps=0.5: 46408 regular of 65536` / `eps=0.75: 65536 regular of 65536`. The two survivors at ε = 1/4 are masks 0 and 65,535 — the empty and the complete pair: at a meaningful tolerance, ε-regularity is a rare, forced-trivial property, exactly Lecture 1's point (the receipt's engine is Gray-code incremental; this naive mirror is minutes slower and prints the same four numbers). Recorded side-run, seeded 8×8 pairs (Lehmer seed 20261056, 100 graphs, cells drawn (a, b)-lexicographic, edge when the draw is even): at ε = 1/4, 0 of 100 regular (worst witness discrepancy 0.671875); at ε = 1/2, 100 of 100 (worst 0.484375) — the tolerance, not the graph, decides.

**What to explore:** seed 8×8 pairs at edge probability 1/2 and watch the ε = 1/4 survivor count stay at zero; then relax ε until the property goes vacuous and find your own personal "galactic constant" — the regularity lemma manufactures for free what randomness cannot give you at any price.

### Part 2 — The energy ladder (Lecture 1)

```python
def partitions(els):                      # all set partitions of els
    if not els:
        yield []
        return
    first, rest = els[0], els[1:]
    for p in partitions(rest):
        yield [[first]] + p
        for i in range(len(p)):
            yield p[:i] + [[first] + p[i]] + p[i+1:]

def q_index(adj, P, n):                   # diagonal-INCLUSIVE Szemeredi index
    q = 0.0
    for Bi in P:
        for Bj in P:                       # ordered block pairs, i = j included
            e = sum(adj[a][b] for a in Bi for b in Bj)
            d = e / (len(Bi) * len(Bj))
            q += len(Bi) * len(Bj) / (n*n) * d * d
    return q

viol = checks = 0
for n, fams in ((5, None), (6, ((2,2,2), (3,3)))):
    allP = list(partitions(list(range(n))))
    if fams:                               # n = 6: the two equitable families
        allP = [P for P in allP if tuple(sorted(map(len, P))) in fams]
    for mask in range(1 << (n*(n-1)//2)):
        adj = [[0]*n for _ in range(n)]
        bit = 0
        for i in range(n):
            for j in range(i+1, n):
                if (mask >> bit) & 1:
                    adj[i][j] = adj[j][i] = 1
                bit += 1
        q0 = q_index(adj, [list(range(n))], n)
        q1 = q_index(adj, [[v] for v in range(n)], n)
        for P in allP:
            checks += 2
            if not (q0 <= q_index(adj, P, n) <= q1):
                viol += 1
print(f"ladder: {checks} checks, {viol} violations")
```

**Verified output.** `ladder: 106496 checks, 0 violations` (n = 5: all 1,024 graphs × all 52 partitions, both inequalities) and `ladder: 1638400 checks, 0 violations` appended (n = 6: all 32,768 graphs × the 15 (2,2,2) + 10 (3,3) partitions) — the ladder q(trivial) ≤ q(P) ≤ q(singletons) is machine-exact, and the proof's defect-refinement deposit has its own receipt: the variance identity increment = Σ p_b(d_b − d)² ≥ p_XY(d_XY − d)² was verified on 1,125,000 seeded (graph, witness) pairs (Lehmer seed 20261012), zero violations of either statement.

**What to explore:** recompute Answer 2's bowtie ladder by hand, then let this code check you; then delete the diagonal terms from `q_index` and watch the ladder break — v1 of the very receipt behind this part made exactly that mistake, and the census refused to confirm it.

### Part 3 — Counting-lemma sampler (Lecture 2)

```python
def lehmer(seed):
    x = seed
    while True:
        x = x * 48271 % 2147483647
        yield x

def tripartite(seed, n, targets):         # targets: ((0,1), t12), ((1,2), t23), ((2,0), t20)
    rng = lehmer(seed)
    E, dens = set(), []
    for (i, j), t in targets:             # one draw per cell, pairs in listed order
        e = 0
        for a in range(n):                 # a in part i, b in part j
            for b in range(n):
                if (next(rng) % 10**6) / 10**6 < t:
                    E.add((i, a, j, b)); e += 1
        dens.append(e / (n*n))
    tri = sum(1 for a in range(n) for b in range(n) for c in range(n)
              if (0,a,1,b) in E and (1,b,2,c) in E and (2,c,0,a) in E)
    return dens, tri

def report(seed, targets, label):
    dens, tri = tripartite(seed, 30, targets)
    prod = dens[0]*dens[1]*dens[2] * 30**3
    window = (dens[0]-0.1)*(dens[1]-0.1)*(dens[2]-0.1) * 30**3
    print(f"{label}: densities {dens[0]:.4f}/{dens[1]:.4f}/{dens[2]:.4f}, "
          f"triangles {tri} vs product {prod:.0f} ({100*tri/prod:.1f}%), "
          f"window {window:.0f}")

report(20261057, [((0,1), 0.5), ((1,2), 0.5), ((2,0), 0.5)], "config 1")
report(20261057, [((0,1), 0.7), ((1,2), 0.4), ((2,0), 0.55)], "config 2")

hi = lambda v: v >= 8                     # the lying-densities exhibit (deterministic)
Eab = lambda a, b: hi(a) == hi(b)
Ebc = lambda b, c: hi(b) == hi(c)
Eca = lambda c, a: hi(c) != hi(a)
counts = [sum(Eab(a,b) for a in range(16) for b in range(16)),
          sum(Ebc(b,c) for b in range(16) for c in range(16)),
          sum(Eca(c,a) for c in range(16) for a in range(16))]
tri = sum(1 for a in range(16) for b in range(16) for c in range(16)
          if Eab(a,b) and Ebc(b,c) and Eca(c,a))
print("hi/lo exhibit: pair counts", counts, "of 256, triangles", tri)
```

**Verified output.** `config 1: densities 0.4911/0.4911/0.4867, triangles 3176 vs product 3169 (100.2%), window 1597` / `config 2: densities 0.7033/0.3889/0.5456, triangles 4011 vs product 4029 (99.6%), window 2097` / `hi/lo exhibit: pair counts [128, 128, 128] of 256, triangles 0`. Both samples sit above the (d − 0.1)³ floor the counting lemma promises, within 0.4% of the product prediction; the exhibit shows what happens when regularity is withheld — all three densities exactly 1/2, zero triangles, and the all-low against all-high test sets see density 0 where the pair says 1/2 (witness discrepancy exactly 1/2, also the maximum over 2,000 seeded test pairs in the receipt). The Lecture 2 rows — 3,307 vs 3,285 (window 1,670) and 4,202 vs 4,215 (window 2,224) at seed 20261052 — are the receipt's original recorded rows (receipt 52runs-2 B2, whose draw rule went unrecorded — the standing scar; re-running the printed rule above at that seed gives 3,883 vs 3,852 and 4,731 vs 4,648, the same story in different digits); this part's rows are the port sample whose draw rule is printed in full above (receipt 52runs-7 C7), so every digit here follows from the code and the seed.

### Part 4 — The Roth reduction explorer (Lecture 4)

```python
def build_G(A, n):                        # the tripartite construction on Z_n (n odd)
    E = set()
    for x in range(n):
        for s in A:
            E.add(((0, x), (1, (x + s) % n)))     # E12
            E.add(((1, x), (2, (x + s) % n)))     # E23
            E.add(((2, (x + 2*s) % n), (0, x)))   # E31: z - x = 2s
    return E

def ap_free(A, n):                        # no 3 distinct terms in arithmetic progression
    return not any(x != y and (x + y) * pow(2, -1, n) % n in A
                   for x in A for y in A)

def profile(A, n):                       # edges, triangle list, per-edge triangle count
    E = build_G(A, n)
    T = []
    for x in range(n):
        for y in range(n):
            for z in range(n):
                t = (((0, x), (1, y)), ((1, y), (2, z)), ((2, z), (0, x)))
                if set(t) <= E:
                    T.append(t)
    cnt = {}
    for t in T:
        for e in t:
            cnt[e] = cnt.get(e, 0) + 1
    return E, T, cnt

for n in (5, 7, 9):
    mism = apfree = uniq = 0
    best = 0
    for mask in range(1 << n):            # EVERY subset A of Z_n
        A = [x for x in range(n) if (mask >> x) & 1]
        E, T, cnt = profile(A, n)
        unique = len(cnt) == len(E) and all(v == 1 for v in cnt.values())
        if ap_free(A, n):
            apfree += 1
            best = max(best, len(A))
        if unique:
            uniq += 1
        if ap_free(A, n) != unique:
            mism += 1
    print(f"n={n}: {mism} mismatches, {apfree} AP-free, "
          f"{uniq} unique-triangle, max {best}")

from itertools import combinations

def min_deletions(A, n):                  # brute force: fewest edges killing all triangles
    E, T, _ = profile(A, n)
    edges = list(E)
    for k in range(len(edges) + 1):
        for D in combinations(range(len(edges)), k):
            s = set(D)
            if all(s & {edges.index(e) for e in t} for t in T):
                return k

for s in range(5):
    E, T, _ = profile([s], 5)
    print(f"A={{{s}}}: edges {len(E)}, triangles {len(T)}, "
          f"min deletions {min_deletions([s], 5)}")
```

**Verified output.** `n=5: 0 mismatches, 16 AP-free, 16 unique-triangle, max 2` / `n=7: 0 mismatches, 43 AP-free, 43 unique-triangle, max 3` / `n=9: 0 mismatches, 127 AP-free, 127 unique-triangle, max 4` — the equivalence A is AP-free ⟺ every edge of G(A) lies in exactly one triangle is machine-exact, in both directions, over *all* subsets; the bookkeeping holds too (#triangles = n|A|, #edges = 3n|A|, asserted clean in the receipt for every AP-free A). Then the deletion floor: `A={0}: edges 15, triangles 5, min deletions 5` — and the same line for all five singletons of Z₅ (exhaustive over all 2^15 deletion sets): the minimum is exactly #triangles, forced by edge-disjointness. No clever deletion ever kills two triangles; removal's o(n²) promise collides with the construction's δn² demand, and Roth's theorem falls out.

**What to explore:** find the largest AP-free sets by hand ({0,1} ⊂ Z₅, {0,1,3} ⊂ Z₇, {0,1,3,4} ⊂ Z₉) and confirm the census counts them; then feed an AP-*containing* A and watch the unique-triangle property die with it — the equivalence cuts both ways.

### Part 5 — The cap-set hunter (Lecture 6)

```python
from itertools import product

def is_cap(pts):                          # no three distinct points with x + y + z = 0
    S = set(map(tuple, pts))
    for x in S:
        for y in S:
            if x == y:
                continue
            z = tuple((3 - (xi + yi) % 3) % 3 for xi, yi in zip(x, y))
            if z in S and z != x and z != y:
                return False
    return True

def max_cap_exhaustive(n):               # n = 1, 2: every subset of F_3^n
    pts = list(product(range(3), repeat=n))
    best = 0
    for m in range(1 << len(pts)):
        A = [pts[i] for i in range(len(pts)) if (m >> i) & 1]
        if is_cap(A):
            best = max(best, len(A))
    return best

def max_cap_dfs(n):                      # n = 3: include/exclude, bound pruning, full tree
    pts = list(product(range(3), repeat=n))
    best = 0
    def dfs(i, chosen):
        nonlocal best
        best = max(best, len(chosen))
        if i == len(pts) or len(chosen) + (len(pts) - i) <= best:
            return
        if is_cap(chosen + [pts[i]]):
            dfs(i + 1, chosen + [pts[i]])
        dfs(i + 1, chosen)
    dfs(0, [])
    return best

def seeded_greedy(seed, n, restarts):   # random orders; greedily keep cap points
    x = seed
    pts = list(product(range(3), repeat=n))
    best = []
    for _ in range(restarts):
        order = pts[:]
        for i in range(len(order) - 1, 0, -1):    # seeded Fisher-Yates
            x = x * 48271 % 2147483647
            j = x % (i + 1)
            order[i], order[j] = order[j], order[i]
        A = []
        for p in order:
            if is_cap(A + [p]):
                A.append(p)
        if len(A) > len(best):
            best = A
    return best

cap4 = [(1,0,1,2), (2,2,0,2), (1,0,2,0), (2,0,1,2), (2,2,1,1), (2,1,0,1),
        (1,1,2,2), (0,2,1,0), (2,0,1,1), (0,2,2,1), (2,2,1,0), (2,1,0,2),
        (0,1,0,1), (0,0,2,1), (0,1,2,0), (1,2,2,2), (1,1,2,0), (0,0,2,0),
        (1,2,0,0), (2,2,0,0)]             # the recorded seed-20261053 exhibit

print("exhaustive max caps (n=1,2):", max_cap_exhaustive(1), max_cap_exhaustive(2))
print("exact DFS max cap in F_3^3:", max_cap_dfs(3))
print("recorded exhibit: F_3^4 cap", len(cap4), "pairwise-verified:", is_cap(cap4))
# the recorded hunts: seeded_greedy(20261053, 4, 2000) -> a 20-cap;
# at n = 5, plateau-accepting iterated local search (seed 20261055,
# 80,000 iterations) -> a 45-cap; plain kicks (seed 20261054) stalled at 39.
```

**Verified output.** `exhaustive max caps (n=1,2): 2 4` / `exact DFS max cap in F_3^3: 9` / `recorded exhibit: F_3^4 cap 20 pairwise-verified: True`. The deterministic parts re-verify exactly; the recorded TypeScript DFS explored the FULL tree — 647,644 nodes, no pruning shortcuts, no abort — so 9 is *proved*, and ◆ Problem 1 asks you to make the machine's argument human. The n = 4 and n = 5 rungs are honest search results, not proofs: r₃(F₃⁴) = 20 and r₃(F₃⁵) = 45 are cited from the literature (the receipt's optimality-proof attempts exceeded the session's compute budget — it says so), the 45-cap needed plateau-accepting kicks where plain kicks stalled at 39, and both exhibits are pairwise-verified caps (re-certified in batch 7).

**What to explore:** the ratios 2, 2, 2.25, 2.22, 2.25 against 2.7551046130 — the bound's constant is *above* every observed ratio, and the gap is the slice-rank slack: 3M = 30 against the truth 9 at n = 3. Watch the slack tighten by computing M(n, ⌊2n/3⌋) for larger n (the DP is six lines) while the truth stalls — asymptotic weapons concede constants and win exponents.

### Part 6 — Extremal, stability, Ruzsa–Szemerédi, and tower tables (Lectures 1, 2, 3)

```python
from itertools import combinations, permutations
import math

def pc(m):
    return bin(m).count("1")

PAIRS = [(i, j) for i in range(6) for j in range(i + 1, 6)]
EIDX = {p: k for k, p in enumerate(PAIRS)}
def emask(edges):
    return sum(1 << EIDX[(min(u,v), max(u,v))] for u, v in edges)
K4S  = [emask(combinations(V, 2)) for V in combinations(range(6), 4)]
TRIS = [emask(combinations(V, 2)) for V in combinations(range(6), 3)]
P5 = [(i, j) for i in range(5) for j in range(i + 1, 5)]
E5 = {p: k for k, p in enumerate(P5)}
def emask5(edges):
    return sum(1 << E5[(min(u,v), max(u,v))] for u, v in edges)
K4S5 = [emask5(combinations(V, 2)) for V in combinations(range(5), 4)]

C5S = []
for V in combinations(range(6), 5):        # the 12 five-cycles on each 5-subset
    seen = set()
    for p in permutations(V[1:]):
        cyc = (V[0],) + p
        m = 0
        for k in range(5):
            u, v = cyc[k], cyc[(k + 1) % 5]
            m |= 1 << EIDX[(min(u, v), max(u, v))]
        seen.add(m)
    C5S += list(seen)

def extremal(pairs, subs):                 # (max edges, labeled extremal count)
    best, cnt = -1, 0
    for m in range(1 << len(pairs)):
        if any(m & s == s for s in subs):
            continue
        if pc(m) > best:
            best, cnt = pc(m), 1
        elif pc(m) == best:
            cnt += 1
    return best, cnt

print("ex(5,K4):", extremal(P5, K4S5), "ex(6,K3):", extremal(PAIRS, TRIS),
      "ex(6,K4):", extremal(PAIRS, K4S), "ex(6,C5):", extremal(PAIRS, C5S))

PARTS3 = []
def partitions3(els, blocks):
    if not els:
        if len(blocks) == 3:
            PARTS3.append([b[:] for b in blocks])
        return
    f, rest = els[0], els[1:]
    for i in range(len(blocks)):
        blocks[i].append(f); partitions3(rest, blocks); blocks[i].pop()
    blocks.append([f]); partitions3(rest, blocks); blocks.pop()
partitions3(list(range(6)), [])

K222 = []
for pp in combinations(PAIRS, 3):          # only perfect pair-partitions of 6
    if sorted(v for p in pp for v in p) != list(range(6)):
        continue
    K222.append(emask([(u, v) for (P, Q) in combinations(pp, 2)
                       for u in P for v in Q]))
print(len(K222), "labeled K2,2,2")

def dels_to_3partite(m):
    return min(sum(1 for B in P for u, v in combinations(B, 2)
                   if m >> EIDX[(u, v)] & 1) for P in PARTS3)

def edit_to_K222(m, e):
    return min((e - pc(m & T)) + (12 - pc(m & T)) for T in K222)

for E in (11, 10):
    G = [m for m in range(1 << 15)
         if pc(m) == E and not any(m & s == s for s in K4S)]
    dd = [dels_to_3partite(m) for m in G]
    ed = [edit_to_K222(m, E) for m in G]
    print(f"{E}-edge K4-free: {len(G)} graphs, deletion distances "
          f"{ {d: dd.count(d) for d in set(dd)} }, edit distances "
          f"{ {d: ed.count(d) for d in set(ed)} }")

W5 = emask([(0, b) for b in range(1, 6)]
           + [(1, 2), (2, 3), (3, 4), (4, 5), (5, 1)])
print("wheel W5:", pc(W5), "edges, K4-free:", not any(W5 & s == s for s in K4S),
      "deletion distance to 3-partite:", dels_to_3partite(W5))

def unique_triangle_census(n=6):          # parameterized; n = 6 is the printed census
    pairs = [(i, j) for i in range(n) for j in range(i + 1, n)]
    tris = []
    for V in combinations(range(n), 3):
        t = 0
        for u, v in combinations(V, 2):
            t |= 1 << pairs.index((min(u, v), max(u, v)))
        tris.append(t)
    total = at_max = max_e = 0
    for m in range(1 << len(pairs)):
        tri = [t for t in tris if m & t == t]
        cnt = {}
        for t in tri:
            for k in range(len(pairs)):
                if t >> k & 1:
                    cnt[k] = cnt.get(k, 0) + 1
        if all(v == 1 for v in cnt.values()) and pc(m) == len(cnt):
            total += 1
            if pc(m) > max_e:
                max_e, at_max = pc(m), 1
            elif pc(m) == max_e:
                at_max += 1
    return total, max_e, at_max

print("(6,3) census:", unique_triangle_census(6))

def im_census(m, kmin):                   # bipartite m + m; blocks of size >= kmin
    cells = tuple((a, b) for a in range(m) for b in range(m))
    def induced_matching(B, E0):          # cross-pairs checked against the ORIGINAL set
        if len({a for a, _ in B}) != len(B):
            return False
        if len({b for _, b in B}) != len(B):
            return False
        return not any((a1, b2) in E0 or (a2, b1) in E0
                       for (a1, b1) in B for (a2, b2) in B
                       if (a1, b1) != (a2, b2))
    def ok(E, E0):                         # E: remaining edges; E0: the original graph
        if not E:
            return True
        e0 = min(E)
        rest = [c for c in E if c != e0]
        for r in range(kmin - 1, len(rest) + 1):
            for extra in combinations(rest, r):
                B = (e0,) + extra
                if induced_matching(B, E0) and ok(E - set(B), E0):
                    return True
        return False
    best = cnt = 0
    for mask in range(1 << len(cells)):
        E = frozenset(c for i, c in enumerate(cells) if mask >> i & 1)
        if ok(E, E):
            if len(E) > best:
                best, cnt = len(E), 1
            elif len(E) == best:
                cnt += 1
    return best, cnt

print("m=3 induced matching: k>=2 ->", im_census(3, 2),
      " k>=3 ->", im_census(3, 3))

lg = math.log10(2)                        # k0 = 2; the refinement shape k -> k*2^k
for h in range(1, 5):
    if lg > 300:
        print(f"height {h}: overflow - the number has 10^{lg:.1f} digits and counting")
        break
    lg = lg + 10 ** lg * math.log10(2)
    print(f"height {h}: log10(k) = {lg:.4f}")
print("true tower of height 5: 2^65536 = 10^%.4f" % (65536 * math.log10(2)))
for eps in (0.1, 0.05, 0.01):
    print(f"eps={eps}: regularity-proof height {eps**-5:.0f}, "
          f"Gowers lower {(1/eps)**(1/16):.4f}")
```

**Verified output.** `ex(5,K4): (8, 15) ex(6,K3): (9, 10) ex(6,K4): (12, 15) ex(6,C5): (9, 85)` — the extremals are *exactly* the Turán graphs (15 labeled T₃(5) with parts 2,2,1; 10 labeled K₃,₃; 15 labeled K₂,₂,₂), machine-exact in structure and in labeled count; the 85 is the census that killed the recall guess "12" (K₂,₂,₂ is tripartite and hosts the 5-cycle 0–2–4–1–3–0). `15 labeled K2,2,2`. `11-edge K4-free: 240 graphs, deletion distances {0: 240}, edit distances {1: 180, 3: 60}` / `10-edge K4-free: 1437 graphs, deletion distances {0: 1365, 1: 72}, edit distances {2: 945, 4: 492}` — one edge below extremal the whole universe is 3-partite (mean edit distance 1.5); two below, 72 exotics appear, and the wheel is the printed witness: `wheel W5: 10 edges, K4-free: True, deletion distance to 3-partite: 1` (mean edit distance 2.68). Structure decays fast — and *where* it breaks is census territory, exactly as Lecture 3's Checkpoint promised. `(6,3) census: (121, 6, 100)` — 121 unique-triangle graphs in total (the empty one vacuously), max 6 edges, 100 at the max (90 bowties + 10 disjoint triangle pairs; ◆ Problem 2 asks for the classification). `m=3 induced matching: k>=2 -> (6, 6) k>=3 -> (3, 6)`; the recorded m = 4 rows: k ≥ 2 → 12 edges with exactly 24 = m! labeled extremals (the complements of perfect matchings), k ≥ 3 → 4, k ≥ 4 → 4 — the δn cliff between m² − m and m, the separator the Ruzsa–Szemerédi hypothesis draws. And the tower: `height 1: log10(k) = 0.9031` / `height 2: log10(k) = 3.3113` / `height 3: log10(k) = 619.8208` / `height 4: overflow - the number has 10^619.8 digits and counting` / `true tower of height 5: 2^65536 = 10^19728.3018` / `eps=0.1: regularity-proof height 100000, Gowers lower 1.1548` / `eps=0.05: regularity-proof height 3200000, Gowers lower 1.2059` / `eps=0.01: regularity-proof height 10000000000, Gowers lower 1.3335` — the honest gap of Lecture 1, in digits.

**What to explore:** run the stability census one floor down (9 edges: how much of the K₄-free universe is still 3-partite?); point `unique_triangle_census` at n = 7 (2^21 graphs — a patient run; the receipt stops at 6, and the maximum you meet is yours to report, not the chapter's); and try to break the induced-matching cliff by hand at m = 4 — ◆ Problem 3 is the m = 3 case, and the general proof is the Ruzsa–Szemerédi theorem itself.

---
