---
name: "cgt-ch3-coloring"
title: "Ch. 3 — Coloring, Ramsey & Extremal: A Lecture Course in the Feynman Style"
type: "text/markdown"
---

# Chapter 3 · Coloring, Ramsey & Extremal Numbers

*A lecture course in the spirit of Chapters 1–2: the idea before the formula, the story before the proof, complete proofs inside the narrative. Graded exercises with hints and worked answers, gem and exploration problems, machine-verified labs, and three vector figures. Every theorem arrives with both halves — the forcing argument above, the construction below — and no proof is left as an honest flag: Brooks, the five-color theorem, Rademacher, and Turán's symmetrization *and* uniqueness are all complete on the page.*

## How to read this chapter

Three questions drive everything here, and they are secretly the same question asked three ways. *How many colors does a graph need?* (Coloring.) *How big must a party be before perfect disorder is impossible?* (Ramsey.) *How many edges can a graph hold before a forbidden shape must appear?* (Extremal.) In each case the answer has the same architecture: a **forcing argument** shows you cannot escape above some threshold, and a **construction** shows you can escape below it. Learn to hear that two-beat rhythm in every proof.

**Notation.** n vertices, m edges, Δ = max degree, χ = chromatic number, ω = clique number, α = independence number. **Exercises are graded ●○○ / ●●○ / ●●●**, with hints inline and worked answers at the end. **Two marks to know:** ◆ marks a **gem** — a self-contained jewel problem whose full worked answer is at the end (a triangle-free 4-chromatic graph, a sum-free coloring of K₁₆, a circulant dodge); ◐ marks an **exploration** — a stated question with recorded machine findings, deliberately left unsolved on the page. Take those as far as you can.

---

## Lecture 1 · Six People at a Party

Here is the theorem that gave Ramsey theory its name — prove it before reading any proof of it, then compare. *Among any 6 people, either 3 are mutual friends or 3 are mutual strangers.*

Model the party as a complete graph K₆: each pair joined by an edge, colored red for friendship, blue for strangeness. The claim: some triangle is all one color.

### 1.1 The forcing half: ask one person

Pick any person P. P stands in 5 relationships, each red or blue. Five objects, two boxes — so some box holds at least three: say P is red-joined to A, B, C. (Compute the pigeonhole yourself: 5 = 2+2+1 fails — one color must appear ≥ 3 times ✓.)

Now watch A, B, C. If *any* pair among them is red — say A–B — then P, A, B is a red triangle, and we are done. If *no* pair among them is red, then all three pairs are blue, and A, B, C is a blue triangle. Done. There is no third possibility; that is the whole proof. ∎ (Pattern **P9**: the pigeonhole, but note *where* it bit — at a single vertex, whose 5 edges could not stay balanced.)

### 1.2 The dodge: why five people are not enough

Is 6 forced, or could 5 escape? Never trust a threshold without testing its underside. On 5 vertices, color red the edges of a pentagon (the cycle C₅) and blue the remaining five edges — which happen to form another pentagon, the pentagram, the five-pointed star.

Now check honestly that no monochromatic triangle exists. Red triangles would be triangles in C₅ — a cycle of length 5 has none. Blue triangles would be triangles in the pentagram — but the pentagram is *also* a 5-cycle (trace it: 0–2–4–1–3–0), so it has none either. And any 3 vertices of the pentagon: at least one pair is adjacent (a red edge — the largest set with no two adjacent in C₅ has size 2) and at least one pair is a diagonal (a blue edge) — so no 3-subset is single-colored. ∎ (Pattern **P11**: beat the bound by *building*.)

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 880 330" font-family="system-ui, -apple-system, 'Segoe UI', sans-serif">
  <rect x="0" y="0" width="880" height="330" fill="#ffffff"/>
  <text x="40" y="34" font-size="17" font-weight="700" fill="#193e5c">Figure 1 &#183; The two halves of R(3,3) = 6 (&#167;1.1&#8211;1.2)</text>
  <text x="40" y="72" font-size="13" fill="#172333" font-weight="600">the dodge at n = 5: red pentagon, blue pentagram</text>
  <g stroke="#dc2626" stroke-width="3.5">
    <line x1="235" y1="105" x2="316" y2="164"/><line x1="316" y1="164" x2="285" y2="259"/>
    <line x1="285" y1="259" x2="185" y2="259"/><line x1="185" y1="259" x2="154" y2="164"/>
    <line x1="154" y1="164" x2="235" y2="105"/>
  </g>
  <g stroke="#2563eb" stroke-width="2.5">
    <line x1="235" y1="105" x2="285" y2="259"/><line x1="285" y1="259" x2="154" y2="164"/>
    <line x1="154" y1="164" x2="316" y2="164"/><line x1="316" y1="164" x2="185" y2="259"/>
    <line x1="185" y1="259" x2="235" y2="105"/>
  </g>
  <g fill="#ffffff" stroke="#193e5c" stroke-width="2.5">
    <circle cx="235" cy="105" r="12"/><circle cx="316" cy="164" r="12"/><circle cx="285" cy="259" r="12"/>
    <circle cx="185" cy="259" r="12"/><circle cx="154" cy="164" r="12"/>
  </g>
  <g font-size="13" font-weight="600" fill="#172333" text-anchor="middle">
    <text x="235" y="88">0</text><text x="334" y="162">1</text><text x="290" y="282">2</text>
    <text x="180" y="282">3</text><text x="138" y="162">4</text>
  </g>
  <text x="40" y="306" font-size="12" fill="#dc2626">red = the cycle 0&#8211;1&#8211;2&#8211;3&#8211;4: no triangle</text>
  <text x="40" y="322" font-size="12" fill="#2563eb">blue = the star 0&#8211;2&#8211;4&#8211;1&#8211;3: also a 5-cycle, no triangle</text>
  <text x="470" y="72" font-size="13" fill="#172333" font-weight="600">the forcing at n = 6: pigeonhole at one person P</text>
  <g stroke="#dc2626" stroke-width="4">
    <line x1="530" y1="190" x2="740" y2="115"/><line x1="530" y1="190" x2="760" y2="190"/>
    <line x1="530" y1="190" x2="740" y2="265"/>
  </g>
  <g stroke="#94a3b8" stroke-width="2.5" stroke-dasharray="6 5">
    <line x1="740" y1="115" x2="760" y2="190"/><line x1="760" y1="190" x2="740" y2="265"/>
    <line x1="740" y1="115" x2="740" y2="265"/>
  </g>
  <g fill="#ffffff" stroke="#193e5c" stroke-width="2.5">
    <circle cx="530" cy="190" r="13"/>
  </g>
  <circle cx="740" cy="115" r="12" fill="#ffffff" stroke="#dc2626" stroke-width="3"/>
  <circle cx="760" cy="190" r="12" fill="#ffffff" stroke="#dc2626" stroke-width="3"/>
  <circle cx="740" cy="265" r="12" fill="#ffffff" stroke="#dc2626" stroke-width="3"/>
  <g font-size="14" font-weight="700" fill="#172333" text-anchor="middle">
    <text x="530" y="196">P</text><text x="740" y="120">A</text><text x="760" y="195">B</text><text x="740" y="270">C</text>
  </g>
  <text x="470" y="306" font-size="12" fill="#64748b">P has 5 edges; one color appears &#8805; 3 times &#8212; say red to A, B, C.</text>
  <text x="470" y="322" font-size="12" fill="#64748b">Dashed pair red &#8594; red triangle; all dashed blue &#8594; blue triangle ABC.</text>
</svg>
```

So R(3,3) — the least n forcing a red or blue triangle in every 2-coloring of K_n — is exactly **6**. Memorize the shape of what we did, not the numbers: *forcing above (pigeonhole at a vertex), construction below (a symmetric dodge).* Every Ramsey result in existence has these two halves, and neither half is optional — the "=" is the teamwork.

**What you now own:** the vertex-pigeonhole (P9), the construction-dodge (P11), and the reflex of testing a threshold from both sides.

---

## Lecture 2 · The Engine: Why It Never Stops

The party problem was one cell of an infinite table: R(s,t) = the least n such that every red/blue coloring of K_n contains a red K_s or a blue K_t. Does the whole table even exist — is R(s,t) finite for all s, t? The answer is the engine that makes Ramsey theory a theory.

**The recursion.** R(s,t) ≤ R(s−1, t) + R(s, t−1) for all s, t ≥ 2.

*Proof.* Let n = R(s−1,t) + R(s,t−1), take any coloring of K_n, and stand at a vertex v. Its n−1 = R(s−1,t) + R(s,t−1) − 1 edges split into red and blue. If at least R(s−1,t) are red, then v's red neighborhood spans (by definition of R) either a red K_{s−1} — which with v makes a red K_s, done — or a blue K_t, done. If fewer than R(s−1,t) are red, then at least R(s,t−1) are blue, and the same sentence with colors swapped finishes it. ∎ (P9 + P4 — the pigeonhole at v feeds an induction.)

**Finiteness** now falls out by induction on s+t: R(1,t) = R(s,1) = 1 (a single vertex is both a red K₁ and a blue K₁), and every cell of the table with s, t ≥ 2 sits above two smaller-sum cells, so the whole table is finite — every uniform-enough disorder is *impossible*, at some finite population. Ramsey's theorem is the mathematical statement that **perfect disorder cannot be maintained forever**.

**The binomial bound.** Unrolling the recursion: R(s,t) ≤ C(s+t−2, s−1). *Proof:* R(1,t) = 1 = C(t−1, 0) ✓ and R(s,1) = 1 = C(s−1, s−1) ✓; and for s, t ≥ 2, the recursion plus Pascal's identity C(a,b) + C(a,b+1) = C(a+1,b+1) gives R(s,t) ≤ C(s+t−3, s−2) + C(s+t−3, s−1) = C(s+t−2, s−1) ∎. In particular R(k,k) ≤ C(2k−2, k−1) ~ 4^{k−1}/√(πk) — large, but *finite*.

**And now the honest embarrassment.** The basic probabilistic *lower* frontier is 2^{k/2}: random colorings avoid monochromatic K_k that long (Chapter 4 builds the machine). So the truth of R(k,k) is trapped between 2^{k/2} below and C(2k−2, k−1) ~ 4^{k−1}/√(πk) above (the binomial bound with its polynomial factor kept) — an *exponential gap*: the upper estimate exceeds the lower by a factor of about 2^{3k/2} (4^k ÷ 2^{k/2} = 2^{3k/2}, the √k barely denting it), one of the most famous open problems in mathematics. Known exact values: R(3,3)=6, R(3,4)=9, R(3,5)=14, R(4,4)=18; even R(5,5) is unknown (known to lie between 43 and 46 as of recent work). Sixty-plus years of work has moved that interval by almost nothing. Some doors need a new idea, not more effort.

---

## Lecture 3 · Coloring Cheaply

New problem family, same chapter, because it is the same rhythm. A **proper coloring** assigns colors to vertices so adjacent vertices differ; χ(G) is the fewest colors that work. Scheduling conflicts, register allocation in a compiler, radio frequencies for neighboring towers — all are χ in costume.

**The greedy guarantee: χ ≤ Δ + 1.** *Method 1 — the algorithm (P15).* Order the vertices v₁,…,v_n arbitrarily; color them in order, always giving vᵢ a color unused by its already-colored neighbors. When vᵢ's turn comes, at most Δ neighbors have been colored, forbidding at most Δ colors — among Δ+1 colors one is always free. The procedure never fails; the procedure *is* the proof. ∎ *Method 2 — the induction (P4).* Delete a vertex, color the rest (Δ can only shrink), put the vertex back: at most Δ neighbor colors are forbidden among Δ+1 available. ∎

Two engines, one line of substance. But *look at what the proof did not do*: it never planned ahead. So the guarantee is a ceiling, not a value — and the ceiling is met exactly where you'd expect structure: K_n needs n = Δ+1 colors (every pair clashes). Run the lab's exhaustion: over all 32,768 graphs on 6 vertices, greedy (in one fixed order) *never* exceeds Δ+1 — but it *equals* Δ+1 in only 1,155 of them and does better in 31,613. Order matters (Exercise 9 makes this vivid).

**Two lower bounds to keep in your pocket** (a χ-user needs both walls): **χ ≥ ω** — the vertices of a clique pairwise clash, so each needs its own color. And **χ ≥ n/α** — the color classes are independent sets, each of size ≤ α, so n vertices need ≥ n/α classes. ∎ (Both one-liners; do not memorize — *see* them.)

### Brooks' theorem, in full (Lovász's construction)

The greedy ceiling χ ≤ Δ + 1 is met exactly where you would expect structure: complete graphs (every pair clashes) and odd cycles (any order walks around the cycle and arrives home to find all Δ colors taken). **Brooks' theorem** says that for connected graphs these are the *only* failures: every connected graph that is neither complete nor an odd cycle has **χ ≤ Δ**. (Connectedness is a real hypothesis, not decoration — apply the theorem componentwise, and one exceptional component can force the ceiling for the whole graph: K₄ ⊔ K₂ is neither complete nor an odd cycle, yet χ = 4 = Δ + 1.)

*Proof.* First Δ ≤ 2: a connected graph with Δ ≤ 1 is K₁ or K₂ (complete), and a connected graph with Δ = 2 is a path or a cycle; paths and even cycles color with 2 = Δ colors, and odd cycles are the exception, done. So let Δ ≥ 3, G connected and not complete. The engine is greedy coloring with a **smart order**: if the vertices can be lined up v₁, …, v_n so that every vᵢ (i < n) has a neighbor *later* in the line, then greedy uses at most Δ colors — when vᵢ's turn comes, that later neighbor is still uncolored, so at most d(vᵢ) − 1 ≤ Δ − 1 colors are forbidden. (The arbitrary-order proof of the ceiling was exactly this count, minus the free neighbor.)

**Case 1 — G is not Δ-regular.** Some vertex r has d(r) < Δ. Line the vertices up by decreasing distance from r in a breadth-first tree: every v ≠ r has its tree-parent later in the line, and r comes last, seeing at most d(r) < Δ colored neighbors. Greedy never runs out. ∎

**Case 2 — G is Δ-regular with a cut vertex x.** Let C₁, …, C_k (k ≥ 2) be the components of G − x, and Gᵢ the piece induced by Cᵢ ∪ {x}. Every vertex of Cᵢ keeps its neighbors inside its own piece (components cannot share edges), so each Gᵢ still has maximum degree Δ — but x, whose Δ neighbors are split among the k pieces, has degree at most Δ − 1 in each. So each piece is a Case-1 graph: color it with at most Δ colors, then permute each piece's palette so that x takes color 1 throughout. The pieces share only x, so the union is a proper coloring of G with at most Δ colors. ∎

**Case 3 — G is Δ-regular and 2-connected.** Regular and not complete means no vertex is adjacent to all others (a universal vertex in a regular graph forces Δ = n − 1, the complete graph) — every vertex has a non-neighbor. It is enough to find a **Lovász triple**: vertices v₁ ≁ v₂, both adjacent to u, with G − {v₁, v₂} connected. Given the triple: color v₁ and v₂ both with color 1 (they do not clash), line up the remaining vertices by decreasing distance from u in a breadth-first tree of G − {v₁, v₂} — u comes last. Every other vertex w has its tree-parent later in line, so it sees at most d(w) − 1 ≤ Δ − 1 colors; and u, colored last, sees at most Δ − 2 colors on its other neighbors plus the single color 1 shared by v₁ and v₂ — at most Δ − 1 distinct. Greedy completes with Δ colors. ∎ It remains to produce the triple; pick any vertex x (it has a non-neighbor) and split in two.

*Case 3a — G − x is 2-connected.* Set v₁ = x and let v₂ be a vertex at distance exactly 2 from x — one exists, because the shortest path from x to any non-neighbor passes through such a vertex — and let u be a common neighbor on that path (v₁ ≁ v₂, both adjacent to u ✓). Then G − {v₁, v₂} = (G − x) − v₂ is a 2-connected graph minus a single vertex: still connected. ∎

*Case 3b — G − x has a cut vertex.* Set u = x. A connected graph with a cut vertex has **end blocks** — maximal 2-connected pieces (or bridges) attached to the rest through a single cut vertex — and at least two of them. Let B₁ ≠ B₂ be two end blocks of H = G − x, with attachment vertices a₁, a₂. **x must have a neighbor inside each end block** Bᵢ ∖ {aᵢ}: the vertices of Bᵢ∖{aᵢ} reach the rest of H only through aᵢ, so if x had no neighbor there, deleting aᵢ would detach them from G entirely — a cut vertex of G, forbidden by 2-connectedness. Choose such neighbors v₁ ∈ B₁∖{a₁} and v₂ ∈ B₂∖{a₂}. They are non-adjacent: two blocks share at most their cut vertices, and v₁, v₂ are not cut vertices of H (the only cut vertex inside an end block is its attachment), so no edge reaches from one to the other. Finally G − {v₁, v₂} is connected: deleting a non-cut vertex from its own block leaves every block connected and every cut vertex in place, so H − {v₁, v₂} stays connected — and x, whose Δ ≥ 3 neighbors all lie in H, keeps at least one neighbor other than v₁, v₂ and stays attached. ∎

That is the whole theorem. (Machine-checked: on all 26,283 connected non-complete graphs with Δ ≥ 3 on 6 vertices, a vertex with two non-adjacent neighbors always exists; on the 11,307 that are 2-connected, the Lovász triple exists and the breadth-first line-up yields a valid ≤ Δ-coloring every single time. A separate census over all connected graphs on n ≤ 6 vertices — 1, 1, 4, 38, 728, 26,704 of them for n = 1, …, 6 — finds χ = Δ + 1 attained *exactly* by complete graphs and odd cycles: zero violations.)

A different repair tool — **Kempe chains**, recoloring along two-colored paths — waits in Lecture 6, where it proves the five-color theorem.

**What you now own:** greedy + delete-and-extend (P15/P4), the two χ-walls, the smart-order greedy (Brooks' engine — a good *order* is worth a color), and the habit of asking *when is a bound tight?*

---

## Lecture 4 · Mantel: The First Density Theorem

Now the third question, and the birth of extremal graph theory. How many edges can a graph on n vertices hold before a triangle becomes *unavoidable*? Try it on n = 4, 5 by hand; guess the shape of the extremal graph. The answer — the complete bipartite graph K_{⌊n/2⌋,⌈n/2⌉}, with two camps and all cross-edges — is exactly the "split the party into two rooms" idea wearing a new costume. It holds ⌊n²/4⌋ edges and not one triangle (triangles need a within-room edge). 

**Mantel's theorem.** A triangle-free graph on n vertices has at most ⌊n²/4⌋ edges; for even n, equality holds only for K_{n/2,n/2} (and Method 3's equality analysis below proves the same uniqueness at every n: only K_{⌊n/2⌋,⌈n/2⌉}).

### Method 1 — the flagship: degree identity + Cauchy–Schwarz (P2)

Triangle-free means: *no edge lies in a triangle*, i.e. for every edge uv, the neighborhoods N(u), N(v) are **disjoint** (a shared neighbor would complete the triangle). Since N(u) ∪ N(v) ⊆ V, every edge satisfies

**d(u) + d(v) ≤ n.**

Sum this over all edges. Each vertex v contributes d(v) once per incident edge — that is, it contributes d(v) · d(v) times in total. So Σ_{uv∈E}(d(u)+d(v)) = Σ_v d(v)², and the inequality reads Σ_v d(v)² ≤ mn. Now the averaging device (P10 in algebraic form): Σ_v d(v)² ≥ (Σ_v d(v))²/n = (2m)²/n by Cauchy–Schwarz. Chain them: 4m²/n ≤ mn, so **m ≤ n²/4**. ∎ *Equality (even n):* forces all degrees equal to 2m/n = n/2 and d(u)+d(v) = n on every edge; picking any edge uv, the disjoint independent sets N(u) and N(v) of size n/2 partition V, and all (n/2)² = n²/4 cross-edges must be present — the graph is exactly K_{n/2,n/2}.

Learn this chain cold — *local constraint → sum over edges → degree-squared identity → Cauchy–Schwarz → bound on m*. It reappears in dozens of extremal problems, and it is the engine behind several results in Chapters 6 and 7.

### Method 2 — induction, peeling a light vertex (P4)

First a reusable lemma: *every triangle-free graph has a vertex of degree ≤ ⌊n/2⌋.* If all degrees exceeded n/2, then any edge uv would have disjoint neighborhoods of total size > n — impossible. Now induct: delete v (degree ≤ ⌊n/2⌋); the rest is triangle-free on n−1 vertices, so by induction it has ≤ ⌊(n−1)²/4⌋ edges; adding back v's ≤ ⌊n/2⌋ edges: ⌊(n−1)²/4⌋ + ⌊n/2⌋ = ⌊n²/4⌋ (check both parities yourself — this floor identity is worth doing once by hand). ∎

### Method 3 — the largest independent set as a measuring rod (P8 + P10)

*(A confession that is also a lesson: in the reference edition this third proof was an honest sketch — a maximum-cut bookkeeping that actually yields only the weaker m ≤ n²/2. This edition replaces it with a complete argument of a different kind.)*

Let A be a **largest independent set**, α = |A|. Three observations, each one line:
1. Every vertex outside A has a neighbor in A — otherwise A ∪ {v} would be a larger independent set.
2. **Δ ≤ α** — because G is triangle-free, every neighborhood N(v) is an independent set, so |N(v)| ≤ α.
3. Every edge touches a vertex outside A (A has no internal edges), so m ≤ Σ_{v∉A} d(v) ≤ (n−α)·Δ ≤ (n−α)·α.

And (n−α)·α ≤ ((n−α+α)/2)² = n²/4 by the arithmetic–geometric mean. **m ≤ n²/4** (and since m and α are integers, m ≤ (n−α)·α ≤ ⌊n²/4⌋). ∎

**The equality case, in full.** Equality m = ⌊n²/4⌋ forces every inequality in the chain to be tight: for n = 1, m = 0 and the graph is K₀,₁; for n ≥ 2, no edge can have both endpoints in V ∖ A (else m = Σ_{v∉A} d(v) − e(V∖A) < Σ_{v∉A} d(v) ≤ (n−α)·α), so V ∖ A is also an independent set, and maximality of A gives α ≥ n − α; since the chain is tight, (n−α)·α = ⌊n²/4⌋, which pins the exact ordered sizes α = ⌈n/2⌉ and n − α = ⌊n/2⌋ ≥ 1; and Σ_{v∉A} d(v) = (n−α)·α with each d(v) ≤ α forces d(v) = α for every v ∉ A — every vertex outside A is joined to all of A, yielding K_{⌊n/2⌋,⌈n/2⌉}. The maximum is attained by one graph only, for every n. (Machine-checked: for each n ≤ 7, the triangle-free graphs with ⌊n²/4⌋ edges are exactly the labeled copies of K_{⌊n/2⌋,⌈n/2⌉} — 1, 1, 3, 3, 10, 10, 35 of them for n = 1…7, and none else.)

The extremal instinct — *take the largest object of its kind and use both what it contains and what it excludes* — is the same cornering move as the longest path (Chapter 2), aimed at a set instead of a path.

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 880 350" font-family="system-ui, -apple-system, 'Segoe UI', sans-serif">
  <rect x="0" y="0" width="880" height="350" fill="#ffffff"/>
  <text x="40" y="34" font-size="17" font-weight="700" fill="#193e5c">Figure 2 &#183; Mantel three ways, one graph: K&#8323;,&#8323; (&#167;4)</text>
  <text x="50" y="72" font-size="13" fill="#172333" font-weight="600">Method 1 &#183; per-edge, then CS</text>
  <text x="340" y="72" font-size="13" fill="#172333" font-weight="600">Method 2 &#183; light vertex, induction</text>
  <text x="630" y="72" font-size="13" fill="#172333" font-weight="600">Method 3 &#183; independent-set rod</text>
  <g stroke="#94a3b8" stroke-width="2.5">
    <line x1="135" y1="130" x2="265" y2="195"/><line x1="135" y1="130" x2="265" y2="260"/>
    <line x1="135" y1="195" x2="265" y2="130"/><line x1="135" y1="195" x2="265" y2="195"/><line x1="135" y1="195" x2="265" y2="260"/>
    <line x1="135" y1="260" x2="265" y2="130"/><line x1="135" y1="260" x2="265" y2="195"/><line x1="135" y1="260" x2="265" y2="260"/>
    <line x1="425" y1="195" x2="555" y2="130"/><line x1="425" y1="195" x2="555" y2="195"/><line x1="425" y1="195" x2="555" y2="260"/>
    <line x1="425" y1="260" x2="555" y2="130"/><line x1="425" y1="260" x2="555" y2="195"/><line x1="425" y1="260" x2="555" y2="260"/>
    <line x1="715" y1="130" x2="845" y2="130"/><line x1="715" y1="130" x2="845" y2="195"/><line x1="715" y1="130" x2="845" y2="260"/>
    <line x1="715" y1="195" x2="845" y2="130"/><line x1="715" y1="195" x2="845" y2="195"/><line x1="715" y1="195" x2="845" y2="260"/>
    <line x1="715" y1="260" x2="845" y2="130"/><line x1="715" y1="260" x2="845" y2="195"/><line x1="715" y1="260" x2="845" y2="260"/>
  </g>
  <line x1="135" y1="130" x2="265" y2="130" stroke="#dc2626" stroke-width="4"/>
  <g stroke="#2563eb" stroke-width="4">
    <line x1="135" y1="130" x2="265" y2="195"/><line x1="135" y1="130" x2="265" y2="260"/>
    <line x1="135" y1="195" x2="265" y2="130"/><line x1="135" y1="260" x2="265" y2="130"/>
  </g>
  <g stroke="#94a3b8" stroke-width="2.5" stroke-dasharray="5 5">
    <line x1="425" y1="130" x2="555" y2="130"/><line x1="425" y1="130" x2="555" y2="195"/>
    <line x1="425" y1="130" x2="555" y2="260"/>
  </g>
  <g fill="#ffffff" stroke="#2563eb" stroke-width="3">
    <circle cx="135" cy="130" r="12"/><circle cx="135" cy="195" r="12"/><circle cx="135" cy="260" r="12"/>
    <circle cx="265" cy="195" r="12"/><circle cx="265" cy="260" r="12"/>
    <circle cx="425" cy="195" r="12"/><circle cx="425" cy="260" r="12"/>
    <circle cx="555" cy="130" r="12"/><circle cx="555" cy="195" r="12"/><circle cx="555" cy="260" r="12"/>
    <circle cx="715" cy="195" r="12"/><circle cx="715" cy="260" r="12"/>
  </g>
  <circle cx="265" cy="130" r="12" fill="#ffffff" stroke="#2563eb" stroke-width="3"/>
  <circle cx="425" cy="130" r="12" fill="#ffffff" stroke="#94a3b8" stroke-width="2.5" stroke-dasharray="4 4"/>
  <g fill="#2563eb" stroke="#ffffff" stroke-width="2.5">
    <circle cx="715" cy="130" r="13"/><circle cx="715" cy="195" r="13"/><circle cx="715" cy="260" r="13"/>
  </g>
  <circle cx="845" cy="130" r="12" fill="#ffffff" stroke="#2563eb" stroke-width="3"/>
  <circle cx="845" cy="195" r="12" fill="#ffffff" stroke="#2563eb" stroke-width="3"/>
  <circle cx="845" cy="260" r="12" fill="#ffffff" stroke="#2563eb" stroke-width="3"/>
  <g font-size="12.5" font-weight="600" fill="#172333" text-anchor="middle">
    <text x="135" y="135">a&#8321;</text><text x="135" y="200">a&#8322;</text><text x="135" y="265">a&#8323;</text>
    <text x="265" y="135">b&#8321;</text><text x="265" y="200">b&#8322;</text><text x="265" y="265">b&#8323;</text>
    <text x="425" y="135">a&#8321;</text><text x="425" y="200">a&#8322;</text><text x="425" y="265">a&#8323;</text>
    <text x="555" y="135">b&#8321;</text><text x="555" y="200">b&#8322;</text><text x="555" y="265">b&#8323;</text>
    <text x="715" y="135" fill="#ffffff">a&#8321;</text><text x="715" y="200" fill="#ffffff">a&#8322;</text><text x="715" y="265" fill="#ffffff">a&#8323;</text>
    <text x="845" y="135">b&#8321;</text><text x="845" y="200">b&#8322;</text><text x="845" y="265">b&#8323;</text>
  </g>
  <text x="40" y="302" font-size="12" fill="#172333">N(a&#8321;), N(b&#8321;) disjoint: d(a&#8321;)+d(b&#8321;) = 6 = n on the red edge;</text>
  <text x="40" y="318" font-size="12" fill="#172333">sum over edges, then Cauchy&#8211;Schwarz: m &#8804; n&#178;/4.</text>
  <text x="330" y="302" font-size="12" fill="#172333">a light vertex (d &#8804; &#8970;n/2&#8971; = 3) always exists;</text>
  <text x="330" y="318" font-size="12" fill="#172333">delete it, induct, put it back.</text>
  <text x="620" y="302" font-size="12" fill="#172333">A = biggest independent set (&#945; = 3): every outside</text>
  <text x="620" y="318" font-size="12" fill="#172333">vertex sees A, &#916; &#8804; &#945;: m &#8804; (n&#8722;&#945;)&#945; = 9.</text>
  <text x="40" y="342" font-size="12" fill="#64748b">Three independent proofs of m &#8804; &#8970;n&#178;/4&#8971; &#8212; and K&#8323;,&#8323; is the even-n equality case, unique up to labeling.</text>
</svg>
```

**Lab tie-in (all verified this session):** on 6 vertices, exhaustive search over all 32,768 graphs finds the triangle-free edge maximum is **9 = ⌊36/4⌋** ✓; exactly **10** graphs achieve it, and every one is a labeled K_{3,3} — Mantel's equality case, confirmed as *unique* up to labeling ✓; and all 3,003 graphs with 10 edges contain a triangle ✓. The theorem's two halves, executed by machine.

### Rademacher's theorem: one edge over the top forces many triangles

Mantel says a graph with ⌊n²/4⌋ edges can be triangle-free. Add *one* edge — and the triangle you now own turns out not to be lonely. **Rademacher's theorem:** every graph on n ≥ 3 vertices with ⌊n²/4⌋ + 1 edges contains at least **⌊n/2⌋** triangles — sharp, by the construction of Exercise 13 (T₂(n) plus one edge inside the larger part).

The proof needs a device worth owning on its own — a second helping of the flagship chain (P2 + CS):

**Lemma (per-edge count).** *Every edge uv lies in at least d(u) + d(v) − n triangles.* The third vertices of triangles on uv are exactly the common neighbors N(u) ∩ N(v), and by inclusion–exclusion |N(u) ∩ N(v)| = d(u) + d(v) − |N(u) ∪ N(v)| ≥ d(u) + d(v) − n. ∎

**Chained (the second-moment bound).** Sum the lemma over all m edges. The left side counts every triangle exactly three times (once per edge): 3T. The right side is Σ_{uv∈E}(d(u) + d(v)) = Σ_v d(v)² — vertex v contributes d(v) to each of its d(v) incident edges — and Cauchy–Schwarz gives Σ d(v)² ≥ (Σ d(v))²/n = 4m²/n. Together: **3T ≥ 4m²/n − mn, that is, T ≥ m(4m − n²)/(3n).** ∎ Two sanity checks: at the Mantel threshold m = n²/4 the bound reads zero (consistent — bipartite graphs have no triangles), and at the complete graph it equals C(n,3) exactly. Machine-checked on all 33,864 graphs with 3 ≤ n ≤ 6: zero violations.

*Proof of Rademacher's theorem*, induction on n; v is throughout a vertex of minimum degree δ. *Base* n = 3: ⌊9/4⌋+1 = 3 edges is all of K₃ — one triangle = ⌊3/2⌋ ✓.

**Case A — δ ≥ ⌊n/2⌋ + 1.** Every edge lies in at least 2δ − n triangles (the lemma), so 3T ≥ m(2δ − n). For n = 2k: 2δ − n ≥ 2, so T ≥ 2m/3 ≥ 2(k²+1)/3 ≥ k, since 2k² − 3k + 2 > 0. For n = 2k+1: 2δ − n ≥ 1, so T ≥ m/3 ≥ (k²+k+1)/3 ≥ k, since (k−1)² ≥ 0. Both give T ≥ ⌊n/2⌋ ✓.

**Induction cases — δ ≤ ⌊n/2⌋.** Delete v and apply the induction hypothesis to the rest.

*n odd, n = 2k+1.* The rest has m′ ≥ m − δ ≥ (k²+k+1) − k = k² + 1 > k² = ⌊(2k)²/4⌋ edges, so the hypothesis applies: T ≥ T(G−v) ≥ k = ⌊n/2⌋ ✓.

*n even, n = 2k, δ ≤ k − 1.* The rest has m′ ≥ (k²+1) − (k−1) = k² − k + 2 > k² − k = ⌊(2k−1)²/4⌋ edges, so T(G−v) ≥ k − 1. If v lies on a triangle, the deletion destroys it: T ≥ (k−1) + 1 = k ✓. If v lies on no triangle, T(G) = T(G−v), and the second-moment bound on the rest (n′ = 2k−1 vertices, m′ ≥ k²−k+2 edges) finishes: 4m′ − n′² ≥ 4(k²−k+2) − (4k²−4k+1) = 7, so T ≥ 7m′/(3n′) ≥ 7(k²−k+2)/(3(2k−1)) ≥ k — the last step being exactly k² − 4k + 14 ≥ 0, that is, (k−2)² + 10 ≥ 0, always true ✓.

*n even, n = 2k, δ = k, v on a triangle.* The rest has m′ ≥ (k²+1) − k = k² − k + 1 = ⌊(2k−1)²/4⌋ + 1 edges — the threshold exactly — so T(G−v) ≥ k − 1, plus the destroyed triangle: T ≥ k ✓.

*n even, n = 2k, δ = k, v on no triangle.* The delicate corner has a clean answer. Let I = N(v): an **independent set** of k vertices (an edge inside I would make a triangle with v). Let R be the remaining k − 1 vertices. Every x ∈ I has degree ≥ δ = k, no neighbors inside I, and only v outside R ∪ I — so x has ≥ k − 1 neighbors in R, and |R| = k − 1: **x is adjacent to every vertex of R.** And R contains an edge — otherwise m ≤ e(v) + e(I) + e(I,R) ≤ k + 0 + k(k−1) = k² < k² + 1, too few. Now every edge of R together with every x ∈ I is a triangle — k choices per R-edge: **T ≥ k · e(R) ≥ k** ✓.

Every case is covered. ∎ (Machine-checked in full: exhaustive search at n = 3..7 finds minima 1, 2, 2, 3, 3 — ⌊n/2⌋ every time — with 1, 6, 30, 60, 210 witnesses, matching the construction's labeled counts. At n = 8, all 21,474,180 seventeen-edge graphs were enumerated: minimum 4, exactly 420 witnesses, every one ≅ K₄,₄ plus one within-part edge — the construction set exactly — and curiously *no* seventeen-edge graph on 8 vertices has exactly 5 triangles. The census even probes further: 2 and 3 edges over the top force minima 8 and 12 — exactly q·⌊n/2⌋ — the thread Exploration X1 sends you down.)

**Why denser graphs are free — the deletion note.** Rademacher's theorem is stated at the exact threshold, but the induction above applied its hypothesis to G−v carrying m′ *above* the threshold for n−1 vertices (two of the cases) as well as at it (the third). So the statement must cover denser graphs — and it does, for free: given more than ⌊n²/4⌋ + 1 edges, delete edges until exactly ⌊n²/4⌋ + 1 remain — deleting edges cannot create triangles, so the count only drops — and every triangle the threshold result finds in the remainder was present in the original graph. The guarantee therefore holds for *every* graph with at least ⌊n²/4⌋ + 1 edges, which is exactly what the induction's above-threshold cases need. (Machine-checked: at n = 5, all 176 graphs with ≥ 7 edges carry at least 2 triangles, and at n = 6, all 4,944 with ≥ 10 edges carry at least 3 — ⌊n/2⌋ throughout, with the sharp examples already sitting at the threshold: 30 labeled K_{2,3} plus one within-part edge, 60 labeled K_{3,3} plus one within-part edge.)

**What you now own:** the flagship chain (P2+CS), the light-vertex lemma (P4), the independent-set rod (P8+P10), the second-moment bound T ≥ m(4m−n²)/(3n), and the bipartite-split instinct for extremal constructions.

---

## Lecture 5 · Turán: The General Ceiling

Mantel forbids triangles. Forbid K_{r+1} instead — a clique of r+1 — and the same story should hold with the complete bipartite graph replaced by a complete **r**-partite one, camps as equal as possible. That is **Turán's theorem** (1941), the first theorem of extremal graph theory: a K_{r+1}-free graph on n vertices has at most the number of edges of the Turán graph T_r(n) — the complete r-partite graph with parts as equal as possible — which is (1 − 1/r)·n²/2 up to rounding. Two complete proofs follow — symmetrization, which rebuilds any K_{r+1}-free graph into a clean multipartite shape without losing edges, and induction, the light-vertex engine again — and then the equality analysis pins the extremal graph down exactly: **T_r(n), unique up to labeling.**

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 880 330" font-family="system-ui, -apple-system, 'Segoe UI', sans-serif">
  <rect x="0" y="0" width="880" height="330" fill="#ffffff"/>
  <text x="40" y="34" font-size="17" font-weight="700" fill="#193e5c">Figure 3 &#183; T&#8323;(6) = K&#8322;,&#8322;,&#8322;: balanced complete tripartite (&#167;5)</text>
  <g stroke="#cbd5e1" stroke-width="2" stroke-dasharray="6 6">
    <line x1="440" y1="95" x2="440" y2="265"/>
    <line x1="280" y1="150" x2="600" y2="210"/>
    <line x1="600" y1="150" x2="280" y2="210"/>
  </g>
  <g stroke="#94a3b8" stroke-width="3">
    <line x1="440" y1="95" x2="280" y2="150"/><line x1="440" y1="95" x2="600" y2="150"/>
    <line x1="440" y1="95" x2="280" y2="210"/><line x1="440" y1="95" x2="600" y2="210"/>
    <line x1="440" y1="265" x2="280" y2="150"/><line x1="440" y1="265" x2="600" y2="150"/>
    <line x1="440" y1="265" x2="280" y2="210"/><line x1="440" y1="265" x2="600" y2="210"/>
    <line x1="280" y1="150" x2="600" y2="150"/><line x1="280" y1="210" x2="600" y2="210"/>
    <line x1="280" y1="150" x2="280" y2="210"/><line x1="600" y1="150" x2="600" y2="210"/>
  </g>
  <circle cx="440" cy="95" r="13" fill="#2563eb" stroke="#ffffff" stroke-width="2.5"/>
  <circle cx="440" cy="265" r="13" fill="#2563eb" stroke="#ffffff" stroke-width="2.5"/>
  <circle cx="280" cy="150" r="13" fill="#dc2626" stroke="#ffffff" stroke-width="2.5"/>
  <circle cx="600" cy="210" r="13" fill="#dc2626" stroke="#ffffff" stroke-width="2.5"/>
  <circle cx="600" cy="150" r="13" fill="#14766d" stroke="#ffffff" stroke-width="2.5"/>
  <circle cx="280" cy="210" r="13" fill="#14766d" stroke="#ffffff" stroke-width="2.5"/>
  <g font-size="13" font-weight="700" fill="#ffffff" text-anchor="middle">
    <text x="440" y="100">u&#8321;</text><text x="440" y="270">u&#8322;</text>
    <text x="280" y="155">v&#8321;</text><text x="600" y="215">v&#8322;</text>
    <text x="600" y="155">w&#8321;</text><text x="280" y="215">w&#8322;</text>
  </g>
  <g font-size="12.5" fill="#172333">
    <circle cx="52" cy="116" r="9" fill="#2563eb"/>
    <text x="70" y="120">part 1 &#183; u&#8321;, u&#8322; (top &amp; bottom)</text>
    <circle cx="52" cy="142" r="9" fill="#dc2626"/>
    <text x="70" y="146">part 2 &#183; v&#8321;, v&#8322; (opposite corners)</text>
    <circle cx="52" cy="168" r="9" fill="#14766d"/>
    <text x="70" y="172">part 3 &#183; w&#8321;, w&#8322; (opposite corners)</text>
    <text x="40" y="204" font-size="12" fill="#94a3b8" font-style="italic">dashed = the three within-part</text>
    <text x="40" y="220" font-size="12" fill="#94a3b8" font-style="italic">non-edges</text>
  </g>
  <text x="440" y="300" font-size="12" fill="#172333" text-anchor="middle">All 12 cross-edges present, none within: e = (1 &#8722; 1/3)&#183;n&#178;/2 = 12, and no K&#8324; anywhere.</text>
  <text x="440" y="318" font-size="12" fill="#64748b" text-anchor="middle">Uniqueness (&#167;5): every K&#8324;-free graph on 6 vertices with 12 edges is this shape up to labeling &#8212; the octahedron.</text>
</svg>
```

### Method 1 — Symmetrization by cloning (P20)

Here is the key device, proven in full so you can hold it: **the cloning lemma.** If u ≁ w and d(w) ≥ d(u), replace u's neighborhood by a copy of w's (delete u's edges; join u to every neighbor of w). Then: (i) the graph stays K_{r+1}-free — any new K_{r+1} using u would contain a K_r inside N(w), and that K_r together with *w* was already a K_{r+1}, contradiction ∎; (ii) the edge count does not decrease (it grows by d(w) − d(u) ≥ 0).

Now fire the device in one **batch**. Let v be a vertex of maximum degree Δ, let N = N(v), and let B be the set of v's non-neighbors. Clone *every* b ∈ B onto v, one clone at a time. Each clone keeps the graph K_{r+1}-free and loses no edges (since v's edges are untouched, d(v) = Δ stays fixed while the degree of any remaining b′ ∈ B can only drop if an edge inside B is deleted, so d(v) ≥ d(b′) holds at every step), and no clone ever disturbs the setup: v's own edges are never touched (only the edges of the vertex being cloned change), and b's new neighborhood N contains neither v nor any other member of B (they are all non-adjacent to v, so none of them sits in N) — so the vertices being cloned stay non-adjacent to v and to each other throughout. When the dust settles:

**S = B ∪ {v} is an independent set, every vertex of S is adjacent to exactly the vertices of N, and the edges inside N are untouched.** The edge count now reads e(G) ≤ e(G′) = |S|·|N| + e(G′[N]) = (n − Δ)Δ + e(G′[N]).

One more forcing step: **G′[N] is K_r-free.** A K_r inside N, plus any vertex of S — which is adjacent to all of N — would be a K_{r+1} in G′. Forbidden. So the Δ vertices of N carry a K_r-free graph, and the *theorem at r − 1* applies to them: e(G′[N]) ≤ t_{r−1}(Δ). (The base of this induction on r is r = 1: a K₂-free graph has no edges at all, and t_1(n) = 0.) Chaining:

**e(G) ≤ (n − Δ)Δ + t_{r−1}(Δ) =: f(Δ).**

**The convexity brick.** What *is* f(Δ)? Exactly the edge count of a complete r-partite graph: split Δ vertices into r − 1 parts as equally as possible (that is T_{r−1}(Δ), worth t_{r−1}(Δ) edges) and add one more part of n − Δ vertices joined to everything before (worth (n − Δ)Δ edges). So maximizing f(Δ) is the question "how many edges can a complete r-partite graph on n vertices have?" — and that has a clean answer. With part sizes s₁, …, s_r, every cross-pair is joined and no inside-pair is: e = ½(n² − Σsᵢ²), so maximizing edges means minimizing Σsᵢ². If two parts differ by two or more, sᵢ ≥ sⱼ + 2, move one vertex from the bigger to the smaller: Σsᵢ² changes by (sᵢ−1)² + (sⱼ+1)² − sᵢ² − sⱼ² = 2(sⱼ − sᵢ) + 2 ≤ −2, a strict improvement. So Σsᵢ² is minimized exactly when the parts are as equal as possible — and therefore **f(Δ) ≤ t_r(n) for every Δ, with equality exactly when the f(Δ)-configuration is balanced.** And a balanced configuration can occur at *two* values of Δ: Δ = n − ⌈n/r⌉ always works, and when r does not divide n so does Δ = n − ⌊n/r⌋ (n = 5, r = 3: Δ = 3 gives parts (2, 2, 1), Δ = 4 gives parts (1, 2, 2), and both are worth 8 = t₃(5); when r divides n the two values coincide and the maximizer is unique). Turán's bound is proved. ∎ (Machine-checked: the batch construction preserves K_{r+1}-freeness and never loses edges — and it is a no-op on every extremal graph, but not only on them (the star K_{1,4} at r = 2 has nothing to clone: four edges, six needed); extremality is the bound's conclusion, not the clone's behavior. The inequality f(Δ) ≤ t_r(n) holds for every Δ, with the maximum attained exactly at Δ = n − ⌈n/r⌉ and Δ = n − ⌊n/r⌋ — one value when r divides n, two otherwise — verified on all n ≤ 100, r ≤ 8.)

### Method 2 — Induction (P4) — the edge bound in full

Three steps: a light-vertex lemma with the *right* bound, the exact increment of the Turán numbers, and the induction itself.

**The light-vertex lemma.** Every K_{r+1}-free graph on n vertices has a vertex of degree at most **n − ⌈n/r⌉ = ⌊(1 − 1/r)n⌋**. *Proof.* Suppose not — every degree is strictly greater than n − ⌈n/r⌉, and since degrees are integers, every vertex satisfies d(v) ≥ n − ⌈n/r⌉ + 1 > (1 − 1/r)n. (If n ≤ r this is already absurd: it demands a degree above n − 1.) Build a clique greedily: pick any v₁; having picked a clique v₁, …, v_k with k ≤ r, take the next vertex from the common neighborhood N(v₁) ∩ ⋯ ∩ N(v_k). A vertex outside N(vᵢ) is one of the n − d(vᵢ) non-neighbors of vᵢ (vᵢ included — nothing is its own neighbor), so by the union bound the common neighborhood still holds at least n − Σᵢ (n − d(vᵢ)) > n(1 − k/r) vertices — at least one for every k ≤ r (and the chosen vertices themselves are never candidates: vᵢ is not its own neighbor). The clique grows to size r, and its common neighborhood still holds a fresh vertex — the (r+1)-th member. A forbidden K_{r+1}: contradiction. ∎ (At r = 2 this is Mantel's light-vertex lemma in its sharp form: a triangle-free graph has a vertex of degree ≤ ⌊n/2⌋. The bound is honest — K_{3,3} has δ = 3 = 6 − ⌈6/2⌉ exactly.)

**The exact increment.** Let t_r(n) be the edge count of T_r(n). The n-th vertex of the Turán graph joins its largest part (of size ⌈n/r⌉ in T_r(n), having grown from a part of size ⌈n/r⌉ − 1 in T_r(n−1)) and is adjacent to exactly the n − ⌈n/r⌉ vertices outside it: **t_r(n) − t_r(n−1) = n − ⌈n/r⌉.** (Algebraically: write n − 1 = qr + s′ with 0 ≤ s′ < r, so ⌈n/r⌉ = q + 1; passing from T_r(n−1) — which has s′ parts of size q+1 and r − s′ parts of size q — to T_r(n) replaces one part of size q by a part of size q+1, raising Σsᵢ² by (q+1)² − q² = 2q + 1 and raising t_r by ½((n² − (n−1)²) − (2q+1)) = ½((2n−1) − (2⌈n/r⌉ − 1)) = n − ⌈n/r⌉.)

**The induction.** Delete a vertex of degree ≤ n − ⌈n/r⌉ — the lemma supplies one. The remainder is K_{r+1}-free on n − 1 vertices, so by induction it carries at most t_r(n−1) edges; restore the vertex and count: e(G) ≤ t_r(n−1) + n − ⌈n/r⌉ = **t_r(n).** ∎ (Base: n ≤ r — no clique of r+1 vertices fits, and t_r(n) = C(n,2) is all the edges there are.)

The induction above delivers the edge bound; Method 1's convexity brick already shows that among complete multipartite graphs only the balanced ones are maximizers. The remaining gap is that a wild, non-multipartite extremal graph might exist. The next section closes it.

### The extremal graph is unique (equality analysis)

**Claim.** If G is K_{r+1}-free on n vertices with e(G) = t_r(n), then G ≅ T_r(n).

*Proof*, induction on n. *Base* n ≤ r: t_r(n) = C(n,2) — every pair is an edge, so G = K_n, which is exactly T_r(n) with its n one-vertex parts. *Step*, n > r. Take a light vertex v — the light-vertex lemma supplies one with d(v) ≤ n − ⌈n/r⌉ — and delete it. Then e(G−v) = t_r(n) − d(v) ≥ t_r(n) − (n − ⌈n/r⌉) = t_r(n−1) by the exact increment, while G−v, being K_{r+1}-free on n−1 vertices, carries at most t_r(n−1) edges. Both inequalities are therefore equalities: **d(v) = n − ⌈n/r⌉ exactly**, and e(G−v) = t_r(n−1), so by induction **G−v ≅ T_r(n−1)** — complete multipartite, parts as equal as possible.

Where are v's missing edges? Let X be the non-neighbors of v inside G−v; the count is forced: |X| = (n−1) − d(v) = ⌈n/r⌉ − 1.

**X must swallow an entire part.** If not, every part of the Turán structure on G−v keeps a vertex outside X — that is, adjacent to v. One such vertex from each of the r parts: r pairwise-adjacent vertices (different parts are fully joined), all adjacent to v — a K_{r+1}. Forbidden.

**And the size arithmetic forces X to be exactly one part.** Write n = qr + s with 0 ≤ s < r. If s ≥ 1, the parts of T_r(n−1) come in sizes q+1 (when s ≥ 2) and q, and |X| = ⌈n/r⌉ − 1 = q; if s = 0 they come in sizes q and q−1, and |X| = q−1. In both cases the *smallest* part size equals |X| exactly. A part contained in X has size ≤ |X|, hence at most the smallest part size, hence exactly it — and since it fills X, **X is precisely one part P₀ of G−v.**

Complete the picture: v is adjacent to everything outside X ∪ {v} — that is, fully joined to every other part — and X ∪ {v} = P₀ ∪ {v} is independent (P₀ is a part; v is non-adjacent to all of it). So G is complete r-partite with parts P₀ ∪ {v} and the r−1 untouched parts of G−v. Count sizes: for s ≥ 1, that is s parts of q+1 and r−s parts of q; for s = 0, it is r parts of q. Those are exactly the part sizes of T_r(n) — and a complete r-partite graph with those sizes **is** T_r(n). ∎

(Machine-checked: exhaustive census over all K_{r+1}-free graphs on n ≤ 6 vertices, every r — every graph attaining the extremal count is isomorphic to T_r(n), and the labeled counts 3, 3, 6, 10, 15, 10, 10, 15, 45, 15 match n! / (∏sᵢ! · ∏m_a!) — the count of labeled copies of T_r(n), where m_a is the number of parts of size a and the equal-sized parts' permutations are divided out — exactly: for K_{3,3} on six labeled vertices, 6!/(3!·3!·2!) = 10, not 40.)

**Where this leads.** Turán is the tip of an iceberg: the Erdős–Stone theorem extends it to any forbidden subgraph H — asymptotically (1 − 1/(χ(H)−1))·n²/2 edges — and exact results for specific H are a thriving industry. Chapter 4 will return with the probabilistic method's own contribution to these numbers.

---

## Lecture 6 · Flatland: Planar Graphs

Can a graph be drawn in the plane with no crossings? A **planar** graph can. The land of the flat has three theorems, each an application of something you already own.

### 6.1 Euler's formula: v − e + f = 2 (P4)

For a connected planar graph with v vertices, e edges, f faces (including the unbounded face): **v − e + f = 2.** *Proof:* build the graph up from one vertex (v=1, e=0, f=1: invariant 2 ✓). Each new edge either (a) hangs from one existing vertex (a tree edge): v and e both grow — invariant preserved; or (b) attaches at both ends, splitting a face into two: e and f both grow — invariant preserved. At the end, all additions preserved 2. ∎ (The same build-it-edge-by-edge engine as Chapter 2's handshaking proof.)

### 6.2 Flat graphs are thin: e ≤ 3v − 6 (P2)

Count face–edge incidences. Work in a **connected** simple plane graph with v ≥ 3. Each face's boundary *walk* has length at least 3 — counting edge-sides, so that a bridge (an edge with the same face on both sides) is walked twice, once along each side; summing over all faces counts every edge-side exactly once, so 3f ≤ 2e. Substitute f = e − v + 2 (Euler's formula, which needs the connectedness): 3(e − v + 2) ≤ 2e ⟹ **e ≤ 3v − 6.** ∎ A disconnected planar graph with v ≥ 3 is handled componentwise — or by first adding noncrossing edges to join its components, which raises e without changing v and can only help the inequality. Two one-line corollaries, both worth saying aloud: K₅ has 10 > 3·5−6 = 9 edges — **not planar**; and K_{3,3}, being bipartite, has all facial walks of ≥ 4 sides, so 4f ≤ 2e gives **e ≤ 2v − 4** (Exercise 8), and 9 > 8 — **not planar** either. (These two graphs are, remarkably, the *only* obstacles: Kuratowski's theorem, stated with one direction proved in §6.5.)

### 6.3 Six colors suffice (P10 + P4)

Planar graphs always have a vertex of degree ≤ 5: for v < 3 this is immediate, and for v ≥ 3 all degrees ≥ 6 would give Σd = 2e ≥ 6v against e ≤ 3v − 6 < 3v — contradiction. Now induct: delete such a vertex, color the rest (still planar), put it back — at most 5 neighbor colors are forbidden among 6. ∎ Averaging says a thin graph has a cheap corner; induction exploits it.

### 6.4 Five colors suffice: repair instead of delete (P4 + Kempe chains)

Six colors came from pure deletion. Five takes repair. Induct as before: delete the low-degree vertex v (§6.3 supplies one with d(v) ≤ 5), 5-color the rest, put v back. If d(v) ≤ 4, or if two neighbors share a color, some color among the five is missing at v's neighborhood — done. The only hard case: **d(v) = 5 and the five neighbors carry five different colors.** Name the neighbors v₁, …, v₅ in their cyclic order around v in the plane drawing, vᵢ wearing color i.

**Kempe chains.** The subgraph induced by the vertices of colors {1, 3} — the (1,3)-subgraph — splits into connected components, its *Kempe components*: each is bipartite with colors 1 and 3 alternating across every edge, and swapping 1 ↔ 3 throughout any single component is again a proper coloring — the swap never leaves the component. Two vertices of colors 1 and 3 in the same component are joined by an alternating 1,3,1,3,… path inside it. A component need not be a path or a cycle — a color-1 vertex with three color-3 neighbors branches it — but only the component facts are used below. v₁ and v₃ each sit in one component (their *Kempe chains*). Two cases:

*Case 1 — v₁ and v₃ lie in different components.* Swap colors 1 ↔ 3 throughout v₁'s component only: still a proper coloring (the swap is an involution inside a component), but now *no* neighbor of v has color 1 — v₃ is in the other component, untouched. Color v with 1. Done.

*Case 2 — v₁ and v₃ lie in the same component.* Then a path of colors 1,3,1,3,… joins v₁ to v₃, and together with the two edges v–v₁, v–v₃ it closes a curve in the plane — with v₂ on one side and v₄ on the other. Any path of colors {2,4} from v₂ to v₄ would have to cross that curve; but the curve is made of graph edges, edges do not cross in a plane drawing, and the curve's vertices carry only colors 1, 3, and v's (missing) color — never 2 or 4. So no such path exists: **v₂ and v₄ lie in different components of the (2,4)-subgraph.** Swap 2 ↔ 4 in v₂'s component; now no neighbor of v has color 2. Color v with 2. Done.

Either way v gets its color: **every planar graph is 5-colorable.** ∎ (Heawood, 1890 — who found the flaw in Kempe's 1879 "proof" of four colors and salvaged this much.) The machine census confirms the shape of the argument: among all 32,647 graphs on 6 vertices satisfying the planar edge bound, every one is 5-colorable; and on 7 vertices, where 232 graphs satisfy δ ≥ 5 and 21 of them need 6 colors, *not one* is 6-critical — the only 6-critical graph on ≤ 7 vertices is K₆, which is not planar (15 edges > 3·6−6). The minimal counterexample the proof dismantles never actually materializes below the non-planar K₆.

### 6.5 Kuratowski's theorem: the only two obstacles

A **subdivision** of a graph is what you get by replacing edges with internally disjoint paths — stretching edges into threads, planting extra vertices along them. **Kuratowski's theorem (1930):** a graph is planar if and only if it contains no subgraph that is a subdivision of K₅ or of K_{3,3}. The hard direction (planarity can always be certified by avoiding just these two shapes) is a longer journey — a minimal counterexample dismantled into 3-connected pieces — honestly left beyond this chapter's scope. But the **easy direction is yours already:** any graph containing a subdivision of K₅ or K_{3,3} is *not* planar. *Proof.* Contracting an edge preserves planarity: in a plane drawing, slide one endpoint along the edge into the other — every other edge merely deforms, nothing crosses. Now suppose G were planar and contained a subdivided K₅. Contract each subdivision path back to an edge: planarity survives every contraction, so K₅ itself would be planar — against §6.2 (10 > 9 edges). Same for K_{3,3} against the bipartite bound (9 > 8). ∎ So the two graphs of §6.2 are not merely non-planar; they are *contagiously* non-planar — every graph that threads them into itself inherits it.

**The rest of the story.** The four-color theorem took a century: Appel–Haken 1976, by computer, checking 1,936 configurations — and in 2005 Georges Gonthier *formally verified* it, machine-checked end to end, in a proof assistant. Hold that thought: the most famous theorem of this chapter is now known precisely because it was formalized — the philosophy of the Lean formal track (the Atlas's unnumbered companion), vindicated at full scale.

**What you now own:** Euler's build-proof, the incidence-counting habit (3f ≤ 2e), low-degree corners from averaging, the Kempe-chain repair (recolor along a two-colored chain; separation wins when chains collide), contraction preserving planarity, and the flat-land bounds.

---

## The Trick Bag (reference card)

| Pattern | Plain language | Where you met it |
|---------|---------------|-----------------|
| **P9 Pigeonhole** | Majority at a vertex; n+1 objects, n boxes | L1.1, L2 |
| **P11 Explicit construction** | The dodge: beat a bound by building | L1.2, L4, Ex 14–17 |
| **P15 Greedy / P18 algorithmic** | The procedure is the proof | L3 |
| **P4 Delete & extend** | Remove a vertex, color/induct, put back | L2, L3, L4, L6.3–6.4 |
| **P2 + Cauchy–Schwarz** | Local constraint → sum over edges → Σd² → CS → bound | L4.1, L4 Rademacher, §6.2 |
| **P8 + P10 Extremal rod** | Largest independent set as a measuring stick | L4.3 |
| **P20 Cloning/symmetrization** | Replace a vertex by a copy of a better one — in one batch. Usage-evidence note: genuinely under-used in the field — the survey's classics reach for shifting (P23) or averaging (P10) when they symmetrize (Katona's circle method is P10 partial work) | L5.1, L5 uniqueness |
| **Smart order (Lovász)** | A good vertex order is worth a color: keep a later neighbor uncolored | L3 (Brooks), L6.4 |
| **Kempe chains** | Recolor along a two-colored chain; colliding chains separate the plane | L6.4 |
| **The two-beat doctrine** | Forcing above, construction below — both halves, always | L1, L2, L4, L5 |

**Formula box:** R(3,3) = 6; R(s,t) ≤ R(s−1,t) + R(s,t−1) ≤ C(s+t−2, s−1); R(k,k) between ~2^{k/2} and ~4^{k−1}/√(πk); known: R(3,4) = 9 (Exercise 14), R(3,5) = 14 (Exercise 17's dodge), R(4,4) = 18; R(3,3,3) = 17 (Exercises 12 + 16). χ ≤ Δ+1; **Brooks: χ ≤ Δ for connected graphs, except complete graphs and odd cycles**; χ ≥ ω; χ ≥ n/α; α ≥ Σ 1/(d+1) (Caro–Wei). Mantel: triangle-free ⟹ m ≤ ⌊n²/4⌋, equality K_{⌊n/2⌋,⌈n/2⌉}; **Rademacher: ⌊n²/4⌋+1 edges ⟹ ≥ ⌊n/2⌋ triangles**; second-moment: T ≥ m(4m−n²)/(3n). Turán: K_{r+1}-free ⟹ m ≤ edges of T_r(n) ≈ (1−1/r)n²/2, **equality only for T_r(n) itself**. Planar: v−e+f = 2; e ≤ 3v−6; bipartite e ≤ 2v−4; δ ≤ 5 somewhere; χ ≤ 6, **χ ≤ 5 with Kempe chains**; Kuratowski: planar ⟺ no subdivision of K₅ or K₃,₃ (easy direction proved).

---

## Exercises (graded: ●○○ easy · ●●○ moderate · ●●● tough)

*Hints are here; worked answers are at the end of the chapter. Try first.*

**Easy — one idea, applied directly**

1. (●○○) Compute R(1,t) and R(2,t) for t ≥ 2. *Hint: how little does it take to force a single red edge?*
2. (●○○) For C₅, K₄, K_{2,3}: compute χ, ω, Δ, α and check χ ≤ Δ+1, χ ≥ ω, χ ≥ n/α on each. *Hint: Lecture 3's two walls, held side by side.*
3. (●○○) Use the edge bounds of Lecture 6.2 to prove K₅ and K_{3,3} are non-planar.
4. (●○○) On 6 vertices: the most edges a triangle-free graph can have? The least number of edges that *guarantees* a triangle? *Hint: Lecture 4 + the lab.*
5. (●○○) A graph has 10 vertices and 26 edges — must it contain a triangle? What about exactly 25 edges? *Hint: Mantel, and check the boundary carefully.*

**Moderate — two ideas, or one tricky step**

6. (●●○) Prove R(2,4) = 4, then conclude R(3,4) ≤ 10 from the recursion. *(The recursion is off by exactly one — Exercise 14 closes the gap and proves R(3,4) = 9.)*
7. (●●○) Prove every graph has an independent set of size ≥ n/(Δ+1). *Hint: greedy color with Δ+1 colors (Lecture 3), then find the big color class (Lecture 1's pigeonhole).*
8. (●●○) Prove a bipartite planar graph with v ≥ 3 has e ≤ 2v − 4. *Hint: what is the shortest possible face in a graph with no odd cycles?*
9. (●●○) Build a bipartite graph (χ = 2!) and a vertex order in which greedy coloring uses *n* colors on 2n vertices. *Hint: the "crown" — aᵢ–bⱼ joined for i ≠ j; order a₁, b₁, a₂, b₂, …*
10. (●●○) Prove the Petersen graph is non-planar. *Hint: girth 5 ⇒ every face has ≥ 5 sides; combine with Euler's formula.*

**Tough — several chapter ideas combined**

11. (●●●) **Caro–Wei.** Prove α(G) ≥ Σ_v 1/(d(v)+1). *Hint: take a uniformly random ordering of the vertices; call v a "winner" if it comes before all its neighbors. Who do the winners form? What is the expected number of winners?*
12. (●●●) Prove R(3,3,3) ≤ 17: any 3-coloring of K₁₇'s edges contains a monochromatic triangle. *Hint: pigeonhole at a vertex (16 = 3·5+1), then Lecture 1 inside the majority color class.*
13. (●●●) **A Rademacher warm-up.** (a) Construct, for every n ≥ 3, a graph with ⌊n²/4⌋+1 edges and only ⌊n/2⌋ triangles — the fewest Rademacher's theorem allows. (b) For n = 6, the lab verified that no 10-edge graph has fewer than 3 triangles, with 60 extremal examples — reconstruct all 60 by hand from your construction. *(The general theorem — ⌊n²/4⌋+1 edges force at least ⌊n/2⌋ triangles — is Rademacher's, proved in full in Lecture 4's Rademacher section. At n = 3 the construction is simply K₃.)*
14. (●●●) **R(3,4) = 9, both walls.** (a) Show that every red/blue coloring of K₉ contains a red triangle or a blue K₄. *Hint: look at the red graph alone — neighborhoods there are independent sets; rule out red degree ≥ 4, then rule out red degree ≤ 2 with R(3,3) = 6, and count what is left.* (b) Exhibit a red/blue coloring of K₈ with neither, and verify it. *Hint: ten red edges; show each red edge's two endpoint-neighborhoods are disjoint, and chase how any four vertices must span a red edge.*

**Gems ◆ — worked jewels (full answers at the end)**

15. (◆) **Four colors, no triangles: the Grötzsch graph.** The Mycielskian M(G) keeps G's vertices v₁,…,v_n, adds a *shadow* mᵢ for each vᵢ (adjacent exactly to vᵢ's neighbors), and an apex adjacent to every shadow. (a) Show χ(M(G)) ≤ χ(G)+1 with an explicit coloring. (b) Apply this to G = C₅ and verify the result: 11 vertices, 20 edges, triangle-free — and χ = 4. *Hint for the hard half: up to rotation and renaming, a 3-coloring of the outer C₅ reads 1,2,3,1,2; now hunt the shadows' colors.*
16. (◆) **Sum-free colorings: R(3,3,3) > 16.** Put the 16 vertices of K₁₆ in one-to-one correspondence with the vectors of Z₂⁴ and color the edge xy with the class of the difference x+y in a partition of the 15 nonzero vectors into three **sum-free** classes (no a + b = c inside a class). Exhibit the classes and prove the coloring is triangle-free. *Hint: what do the three edge-differences of a triangle sum to? Combined with Exercise 12, this pins R(3,3,3) = 17 exactly.*
17. (◆) **A circulant dodge: R(3,5) > 13.** Around a 13-cycle (vertices Z₁₃), color x–y red when the cyclic distance is 1 or 5, blue otherwise. Prove: no red triangle (a finite sum check) and no blue K₅ (a gap argument: 5 points around the clock cut it into 5 gaps summing to 13). *Hint: gaps of 1 or 5 are already red pairs; what gap patterns remain?*

**Further Graded Problems — each hint naming its pattern**

18. (●○○) **Wheels.** The wheel W_n is a rim cycle C_{n−1} plus one hub vertex adjacent to every rim vertex (n ≥ 4 vertices). Determine χ(W_n) for every n — when is it 3, when 4 — and prove your answer. *Hint: the hub needs its own color (P9); the rim needs two when even, so count parities — and for the 4 case, show three really do suffice on the rim by coloring from any fixed starting vertex.*
19. (●●○) **The Ramsey recursion, and Pascal's ceiling.** Prove R(s,t) ≤ R(s−1,t) + R(s,t−1), then conclude by induction that R(s,t) ≤ C(s+t−2, s−1). *Hint: P9 at a vertex of the complete graph — its incident edges split into two classes, so one class is large; then P4 — the binomial recursion is exactly Pascal's.*
20. (●●○) **Half of every graph is bipartite.** Prove that every graph with m edges has a bipartite subgraph with at least m/2 edges. *Hint: P10/P12 in miniature — throw the vertices left/right uniformly at random and compute the expected number of edges that cross; or derandomize greedily, moving any vertex that sees more of its neighbors on its own side than across.*
21. (●●●) **Chromatic number prices edges.** Prove that χ(G) = k forces m ≥ C(k,2), and classify equality: m = C(k,2) exactly when G is a K_k plus isolated vertices. *Hint: P8 — pass to a k-critical subgraph (minimal with χ = k; every proper subgraph is (k−1)-colorable); a critical graph has minimum degree ≥ k−1 (else delete the light vertex, color, put it back); now count.*
22. (●●●) **Sums of one color (Schur's theorem for two colors).** Call a coloring of {1,…,n} *sum-free* if no monochromatic x, y, z with x + y = z (x = y allowed). Prove: **every 2-coloring of {1,…,5} fails**, and exhibit a sum-free 2-coloring of {1,…,4}. *Hint: P1 (and P25 Reduction / encoding in the companion Pattern Map) — encode as Ramsey: give the edges of K₆ the color of their difference, coloring the edge between i < j with the color of the number j − i, then run Lecture 1 on the resulting coloring of K₆.*

**Explorations ◐ — stated, not solved (machine findings recorded in the lab)**

X1. (◐) **How far does q·⌊n/2⌋ go?** Rademacher is q = 1 edge over the top. Enumerate every graph on 8 vertices with 16 + q edges, for q = 1, 2, 3, and find the minimum triangle count each time. (Recorded: minima 4, 8, 12 — exactly q·4; at q = 1, the 420 minimizers are *exactly* the construction set K₄,₄ plus one within-part edge, and no 17-edge graph has exactly 5 triangles; at q = 2, the 2,310 minimizers are exactly K₄,₄ plus any two of the 12 within-part edges — three genuinely different shapes: 1,260 with one within-part edge in each part, 210 with two disjoint edges in one part, and 840 with a 2-edge path P₃ in one part. What breaks at q = 4?)
X2. (◐) **The 6-critical census.** A graph is k-critical if χ = k but every proper subgraph is (k−1)-colorable. Enumerate all 6-critical graphs on at most 7 vertices. (Recorded: exactly one, K₆ — on 7 vertices there are 232 graphs of minimum degree ≥ 5 and 21 of them have χ = 6, yet every one has a vertex whose deletion drops the count to 5. Why must a 6-critical graph have minimum degree ≥ 5? — that is §6.4's minimal-counterexample logic in reverse.)

---

## Answers to the Exercises

**A1.** R(1,t) = 1: a single vertex is a red K₁. R(2,t) = t: a red K₂ is just a red edge; if any edge is red, done — so to dodge, color *all* edges blue, which forces a blue K_t exactly when n = t (at n = t−1, all-blue dodges both). So R(2,t) = **t**.

**A2.** C₅: χ=3, ω=2, Δ=2, α=2 → 3 ≤ 3 ✓, 3 ≥ 2 ✓, 3 ≥ 5/2 ✓. K₄: χ=4, ω=4, Δ=3, α=1 → 4 ≤ 4 ✓, 4 ≥ 4 ✓, 4 ≥ 4 ✓ (a wall-tight case: every bound is equality). K_{2,3}: χ=2, ω=2, Δ=3, α=3 → 2 ≤ 4 ✓, 2 ≥ 2 ✓, 2 ≥ 5/3 ✓.

**A3.** K₅ has v = 5 ≥ 3 and e = C(5,2) = 10; if K₅ were planar, Lecture 6.2 would force e ≤ 3v − 6 = 3·5 − 6 = 9, against e = 10 > 9 ✗. K₃,₃ has v = 6 ≥ 3, e = 3·3 = 9, and is bipartite, so if it were planar the bipartite bound e ≤ 2v − 4 (Exercise A8) would force e ≤ 2·6 − 4 = 8, against e = 9 > 8 ✗. Neither fits in the plane. ∎

**A4.** Most edges triangle-free: **9** (attained by K_{3,3}; the lab found it unique up to labeling). Guarantee threshold: **10** — Mantel says triangle-free ≤ ⌊36/4⌋ = 9, and the lab confirms all 3,003 ten-edge graphs contain a triangle.

**A5.** 26 edges: yes — Mantel caps triangle-free at 10²/4 = 25, and 26 > 25. Exactly 25: **no** — K₅,₅ has 25 edges and no triangle. The boundary case is exactly the extremal graph; always test a threshold at its edge.

**A6.** R(2,4): a red K₂ is any red edge; to dodge red entirely, color all blue, which forces a blue K₄ exactly at n = 4 (n = 3: all-blue K₃ dodges both). So R(2,4) = 4. Recursion: R(3,4) ≤ R(2,4) + R(3,3) = 4 + 6 = **10**. (The recursion is off by exactly one: the sharp value is 9 — Exercise 14 proves it, both walls.)

**A7.** Greedy uses at most Δ+1 colors (Lecture 3), producing a proper coloring in which every color class is an independent set. Since n vertices are distributed among ≤ Δ+1 classes, the largest class has ≥ n/(Δ+1) vertices (pigeonhole), and it is independent. **α ≥ n/(Δ+1).** ∎

**A8.** Bipartite ⟹ no odd cycle ⟹ every closed walk has even length, so each facial boundary *walk* has length ≥ 4 (in a connected plane graph with v ≥ 3, every face boundary walk has length ≥ 2, and no simple graph can have a closed walk of length 2 bounding a face unless the whole connected graph is a single bridge K₂ with v = 2; since a bridge contributes its two sides to the same face's walk, the walk length stays even and is therefore ≥ 4). Counting face–edge incidences in a **connected** plane bipartite graph: 4f ≤ 2e. Euler: f = 2 − v + e, so 4(2 − v + e) ≤ 2e ⟹ **e ≤ 2v − 4.** ∎ (A disconnected bipartite planar graph: join the components with noncrossing edges — choosing the bipartition sides compatibly: if G has c ≥ 2 components in a plane embedding, some face F of one component C₁ contains another component C₂, so a vertex u ∈ C₁ on the boundary of F can be joined by a curve inside F to a vertex w ∈ C₂ on the outer boundary of C₂, flipping the 2-coloring of C₂ if needed so u and w lie in opposite parts; repeating c − 1 times produces a connected bipartite plane graph on the same v ≥ 3 vertices with e + (c − 1) ≤ 2v − 4, whence e ≤ 2v − 4 − (c − 1) < 2v − 4 — or argue componentwise.)

**A9.** The crown on {a₁,…,a_n, b₁,…,b_n}: join aᵢ–bⱼ iff i ≠ j. It is bipartite (χ = 2). Order a₁, b₁, a₂, b₂, …: by induction on i ∈ {1,…,n}, both aᵢ and bᵢ receive color i. For i = 1, a₁ gets 1, and b₁ is *not* adjacent to a₁, so b₁ gets 1. For i > 1, when aᵢ is colored, its already-colored neighbors are b₁,…,b_{i−1}, which by the induction hypothesis carry colors 1,…,i−1, so aᵢ gets i; when bᵢ is colored, its already-colored neighbors are a₁,…,a_{i−1} (since bᵢ ≁ aᵢ), which carry colors 1,…,i−1, so bᵢ also gets i. Greedy uses **n colors** on a 2-colorable graph. The moral: greedy is order-blind, and orders can be adversarial.

**A10.** The Petersen graph is connected and has v = 10, e = 15, girth 5 (no triangles, no 4-cycles — check the standard drawing: outer 5-cycle, inner star, spokes: the outer rim and inner star are 5-cycles with no chords; a cycle using spokes must cross between rim and star an even number of times, and two spokes between adjacent rim vertices i, i+1 lead to inner vertices at star-distance 2 from each other, closing a cycle of length 1 + 1 + 2 + 1 = 5). Since the graph is connected and 2-edge-connected (bridgeless) with girth 5, every facial boundary walk in any plane embedding contains a cycle and therefore has length ≥ 5. Every face would be bounded by ≥ 5 edges, so 5f ≤ 2e = 30, f ≤ 6. But Euler demands f = 2 − v + e = 7. Contradiction — **non-planar.** ∎ (Equivalently: 5(2−10+15) = 35 > 2·15 = 30.)

**A11.** Order the vertices uniformly at random and call v a **winner** if it precedes all its neighbors. Winners form an independent set: if u ~ v both won, one of them precedes the other — say u before v — but then v has a neighbor (u) before it, so v lost. Contradiction. Now E[#winners]: v wins iff v is first among its closed neighborhood of d(v)+1 vertices; by symmetry each of the d(v)+1 orderings of that little set is equally likely, so P(v wins) = 1/(d(v)+1). Linearity of expectation: E = Σ_v 1/(d(v)+1). Some ordering achieves at least the expectation. **α ≥ Σ_v 1/(d(v)+1).** ∎ This is Chapter 4's probabilistic method in miniature — existence by expectation — and (by the AM–HM inequality, Σ1/x ≥ n²/Σx) it implies the handy α ≥ n²/(2m+n).

**A12.** In any 3-coloring of K₁₇, stand at a vertex v: 16 incident edges, 3 colors, and 16 > 3·5, so some color — say red — appears on ≥ 6 of them. Let S be v's red neighborhood, |S| ≥ 6. If any edge inside S is red, it completes a red triangle with v ✓. If not, S spans a 2-colored (blue/green) complete subgraph on at least 6 vertices — and R(3,3) = 6 (Lecture 1) forces a monochromatic triangle inside S ✓. Either way a monochromatic triangle exists in the original coloring. **R(3,3,3) ≤ 17.** ∎ (The value is exactly 17; the 16-vertex dodge is Exercise 16 — the sum-free coloring of Z₂⁴.)

**A13.** (a) Start from K_{a,b}, a = ⌊n/2⌋, b = ⌈n/2⌉, with ab = ⌊n²/4⌋ edges, and add one edge inside the **larger** part (of b vertices), between u and v. New triangles: exactly u–v–x for x in the other part — any other triangle would use the within-part edge, and there is only one. Count: **a = ⌊n/2⌋ triangles**, on ⌊n²/4⌋+1 edges — exactly Rademacher's guaranteed minimum, so the construction is sharp for every n ≥ 3. (The larger class is the right target: for even n the two classes are the same size and either works, but for odd n adding inside the *smaller* class would create ⌈n/2⌉ triangles — one too many — and at n = 3 the smaller class has a single vertex and no edge to add. For n = 3 the construction is simply K₃: three edges, one triangle; for n = 5, adding within the class of three gives exactly 2 = ⌊5/2⌋ triangles.) (b) For n = 6: parts of 3 and 3; the extremal graphs are labeled K_{3,3} plus one within-part edge. Count them: 10 labeled K_{3,3} (choose which 3 vertices form a part — C(6,3) = 20, halved since the two parts are unordered) × 2 choices of part × 3 choices of within-part edge = **10 × 2 × 3 = 60** ✓ — exactly the 60 witnesses the lab found, and the machine's minimum (3 triangles) matches the construction ✓. (c) Lecture 4's Rademacher section shows ⌊n/2⌋ is the true minimum for every n — your construction is sharp by proof, not just by census. And look where it sits in the proof: for even n, a min-degree vertex of your graph that is not an endpoint of the extra edge has degree k, lies on *no* triangle — exactly the delicate corner — and the proof's I–R structure is your two parts, with the extra edge inside R (e(R) = 1, giving T = k·1 = k).

**A14.** (a) Read the coloring as a single graph: let R be the red graph of K₉. No red triangle says R is triangle-free; a blue K₄ is exactly an independent 4-set of R. *No vertex has red degree ≥ 4:* its red neighborhood would be an independent set (R is triangle-free) of size ≥ 4 — a blue K₄. Forbidden. *No vertex has red degree ≤ 2:* then at least 9 − 3 = 6 vertices lie outside v's closed red neighborhood, and v has no red edges to any of them. Among any 6 of those vertices, R is still triangle-free — so R(3,3) = 6 (Lecture 1) forces an independent 3-set among them, and together with v that is an independent 4-set again. Forbidden. So every vertex has red degree exactly 3: a 3-regular graph on 9 vertices would have degree-sum 27 — odd, against the handshaking lemma. Contradiction: **R(3,4) ≤ 9.** ∎ (The machine agrees: exhaustive search finds zero triangle-free graphs with α ≤ 3 on 9 vertices.) (b) The dodge on 8 vertices — red edges: 0–3, 0–5, 1–4, 1–6, 2–5, 2–6, 2–7, 3–6, 3–7, 4–7. *No red triangle:* the red neighborhoods are N(0) = {3,5}, N(1) = {4,6}, N(2) = {5,6,7}, N(3) = {0,6,7}, N(4) = {1,7}, N(5) = {0,2}, N(6) = {1,2,3}, N(7) = {2,3,4}, and for each of the ten red edges uv the intersection N(u) ∩ N(v) is empty — e.g. edge 2–7: N(2)∖{7} = {5,6} and N(7)∖{2} = {3,4}. *No blue K₄ (= every 4 vertices span a red edge):* split the vertices into L = {0,1,4,5} (red degree 2 each) and H = {2,3,6,7} (red degree 3 each). Inside L, the only red edges are 0–5 and 1–4; if 3 vertices are chosen from L, by pigeonhole they contain one of the pairs {0,5} or {1,4}, a red edge, so an independent set meets L in at most 2 vertices. Inside H, the red edges form K_{2,2} between {2,3} and {6,7}, so the only non-edges are 2–3 and 6–7, and an independent set meets H in at most 2 vertices — an independent 4-set would need exactly 2 + 2. The L-to-H red edges form a perfect matching: 0–3, 1–6, 4–7, 5–2. If the H-pair is {2,3}, the L-pair must avoid the matched vertices 5 and 0, so it comes from {1,4} — but 1–4 is red. If the H-pair is {6,7}, the L-pair must avoid 1 and 4, so it comes from {0,5} — but 0–5 is red. No independent 4-set exists: **R(3,4) ≥ 9**, and with (a), R(3,4) = **9.** ∎

**A15.** (a) Color each old vertex vᵢ with its old color c(vᵢ), each shadow mᵢ with the *same* color c(vᵢ), and the apex with the fresh color χ(G)+1. Check the three new edge types: mᵢ is adjacent only to vᵢ's neighbors, which carry colors ≠ c(vᵢ) (the old coloring was proper); shadows are pairwise non-adjacent; the apex meets only shadows, all colored ≤ χ(G). Proper with χ(G)+1 colors: **χ(M(G)) ≤ χ(G)+1.** ∎ (b) For G = C₅: 5 old + 5 shadows + apex = 11 vertices; edges: 5 (cycle) + 10 (each shadow to two cycle-neighbors) + 5 (apex) = 20. Triangle-free: the cycle has none, and any other triangle must use a shadow mᵢ or the apex. A shadow mᵢ has exactly three neighbors — v_{i−1}, v_{i+1}, and the apex — and no two of them are adjacent: v_{i−1} ≁ v_{i+1} (C₅ has no chords), and the apex meets only shadows, never cycle vertices. A triangle through the apex would need two adjacent shadows — but shadows are pairwise non-adjacent. No triangle anywhere. (Machine-checked: 11 vertices, 20 edges, 0 triangles, α = 5, Δ = 5.) For χ ≥ 4, suppose a 3-coloring exists. Up to rotation, reflection, and renaming colors, every proper 3-coloring of the outer C₅ reads 1,2,3,1,2 (some color appears twice — twice only, since α(C₅) = 2 — and at cyclic distance 2; the rest is forced). Now the shadows: m₀ sees v₄, v₁ (colors 2,2); m₁ sees v₀, v₂ (1,3); m₂ sees v₁, v₃ (2,1); m₃ sees v₂, v₄ (3,2); m₄ sees v₃, v₀ (1,1). So m₁ = 2, m₂ = 3, m₃ = 1 are forced — the shadows already carry all three colors. The apex, adjacent to every shadow, has nothing left: no 3-coloring exists. With (a), **χ = 4.** ∎ This is the Grötzsch graph — the smallest triangle-free graph needing 4 colors. χ can outrun ω by an unbounded distance, one Mycielski step at a time.

**A16.** The vertices are the 16 vectors of Z₂⁴; the edge xy (x ≠ y) carries the difference x+y ∈ Z₂⁴∖{0̄} (x+y ≠ 0̄ exactly because x ≠ y). Partition the 15 nonzero vectors into three classes, each **sum-free** — no a + b = c inside a class: C₁ = {0001, 0010, 0100, 1000, 1111}, C₂ = {0011, 0101, 0111, 1010, 1011}, C₃ = {0110, 1001, 1100, 1101, 1110} (5 + 5 + 5 = 15 ✓) — and color edge xy by the class of x+y. (Sum-freeness is a finite check per class: in C₁ every element has Hamming weight 1 or 4, so any sum of two distinct elements has weight 2 or 3 ∉ {1,4}; in C₂ and C₃, all 10 pairwise sums inside each class land in the other two classes — machine-verified across all pairs; the three classes cover all 15 nonzero vectors.) Now the key step: in a triangle x, y, z, the three edge-differences are d₁ = x+y, d₂ = y+z, d₃ = z+x; they are *distinct* (d₁ = d₂ would give x = z) and they sum to d₁ + d₂ + d₃ = 0̄. In Z₂⁴, three distinct elements summing to 0̄ always split as a + b = c (add a to both sides of a+b+c = 0̄). So a monochromatic triangle would put three distinct elements a, b, a+b inside one class — against sum-freeness. No monochromatic triangle in K₁₆: **R(3,3,3) > 16**, and with Exercise 12, R(3,3,3) = **17** exactly. ∎

**A17.** Red = cyclic distance 1 or 5 on Z₁₃. *No red triangle:* a red triangle needs differences a, b, a+b all in {±1, ±5} (mod 13); check the pairs — 1+1 = 2, 1+5 = 6, 1−1 = 0, 1−5 = −4, 5+5 = −3, 5−1 = 4, 5−5 = 0, and the negated cases — none of the sums lands in {±1, ±5}. (Machine-checked: the circulant is triangle-free.) *No blue K₅:* take any 5 points and read the 5 gaps between consecutive chosen points around the clock — positive integers summing to 13. A gap of 1 or 5 is itself a red pair, so all gaps avoid {1, 5}; a gap ≥ 6 forces the other four gaps to sum to ≤ 7, impossible since each is ≥ 2. So the gaps come from {2, 3, 4} and sum to 13: the only multisets are {2,2,2,3,4} and {2,2,3,3,3}. In {2,2,2,3,4}, the gap 3 sits next to some 2 (its two cyclic neighbors cannot both be the single 4): consecutive gaps 2+3 = 5 mean two chosen points at cyclic distance 5 — a red pair. In {2,2,3,3,3}, the two 2s are either separated — then each has a 3 as a neighbor, again 2+3 = 5 — or adjacent, and then the block [2,2] has a 3 beside it: same conclusion. Every 5-point set contains a red pair: **no blue K₅, so R(3,5) > 13.** ∎ (The 4-set {0, 3, 6, 9} — gaps 3,3,3,4 — is red-free: the machine puts the red independence number at exactly 4. The true value is R(3,5) = 14; the K₁₃ dodge is as far as this construction goes.)

**A18.** The hub touches everything, so it spends one color alone (P9: its neighbors take the other colors). What is left is the rim, a cycle: C_{n−1} needs 2 colors when n−1 is even and 3 when odd (an odd cycle is not 2-colorable — chase the parity around the loop). So: **χ(W_n) = 3 when the rim is even, 4 when odd** — W_n with n−1 odd (W₄, W₆, W₈, …) needs the hub color plus three rim colors. For the upper bound on the odd rim, fix any rim vertex v₀, alternate two colors around the rim from v₀ until the alternation fails at the last edge, and repaint v₀ with the third rim color: its two neighbors keep the other two. Machine check: χ computed by brute force on every wheel W₄…W₉ — 4, 3, 4, 3, 4, 3 exactly as predicted, zero exceptions ✓. (The odd wheels are 4-*critical* — remove anything and three colors return — which is X2's census family in miniature.)

**A19.** Pigeonhole at a vertex (P9): in a red/blue coloring of K_N with N = R(s−1,t) + R(s,t−1) vertices, fix v. Its N − 1 = R(s−1,t) + R(s,t−1) − 1 incident edges split into red and blue: if v has at least R(s−1,t) red neighbors, the red graph on them contains either a red K_{s−1} — which with v makes a red K_s — or a blue K_t, done. Otherwise v has fewer than R(s−1,t) red neighbors, so at least (N−1) − (R(s−1,t) − 1) = R(s,t−1) blue neighbors, and the blue argument runs the same way: a blue K_{t−1} grows to a blue K_t with v, or a red K_s appears. Either way a monochromatic K_s or K_t exists, so **R(s,t) ≤ R(s−1,t) + R(s,t−1)**. For the ceiling, induct on s + t (P4): R(s,2) = s = C(s, s−1) and R(2,t) = t = C(t,1) anchor the base for s, t ≥ 2 (and R(1,t) = R(s,1) = 1), and the recursion is Pascal's identity — R(s,t) ≤ C(s+t−3, s−2) + C(s+t−3, s−1) = C(s+t−2, s−1) ✓. Numbers: R(3,3) = 6 = C(4,2) (the ceiling is *tight* there); R(3,4) = 9 ≤ 10; R(3,5) = 14 ≤ 15; R(4,4) = 18 ≤ 20 — the machine-checked table agrees everywhere ✓. Notice Exercise 6's "off by exactly one": the recursion gives 10 for R(3,4), the truth is 9 — ceilings are honest but not always tight, which is exactly why Exercise 14 had to close the gap by hand.

**A20.** Throw every vertex independently left or right with probability ½ (P12's coin). An edge crosses the cut exactly when its ends landed on opposite sides — probability ½ — so the expected number of crossing edges is m/2 (P10: expectation adds over edges). An expectation is a promise: *some* partition has at least m/2 edges crossing it, and the crossing edges form a bipartite subgraph (the two sides are the parts). ∎ The derandomized version (P18) is a greedy repair: start anywhere; a vertex whose own-side neighbors outnumber its across-side neighbors switches sides, gaining the cut at least one edge each move — the process must stop (the cut is bounded above by m), and it stops only when every vertex sees at least as many across as home, so at least m/2 edges cross. Machine check: over all 33,866 graphs on n = 2..6 vertices, the exact maximum cut is ≥ m/2 in every single one; equality m/2 happens only for the five edgeless graphs (m = 0), every graph with edges cuts strictly more than m/2, and 70 of those sit tight at the ceiling ⌈m/2⌉ — the triangle among them, its best split keeping exactly two of its three edges ✓. The moral for the chapter: bipartiteness is 2-colorability, and *half of every graph's edges can always be 2-colored* — a first hint that χ is not just about cliques (Lecture 3's second wall).

**A21.** The extremal reflex (P8): pass to a subgraph H ⊆ G that is *k-critical* — χ(H) = k but every proper subgraph is (k−1)-colorable (keep deleting edges and vertices; χ never rises, so stop at the last subgraph still needing k). H has minimum degree ≥ k−1: delete a lighter vertex v, (k−1)-color H − v, then put v back with a free color (it has fewer than k−1 neighbors, so some color is unused among them) — contradicting criticality. Also H has at least k vertices (χ(H) ≤ |V(H)|). Now the degree-sum machine (Lecture 1 of Chapter 2, P2/P7): m(H) ≥ ½(k−1)|V(H)| ≥ k(k−1)/2 = C(k,2), and m(G) ≥ m(H). ∎ **Equality:** retrace — |V(H)| = k and δ(H) = k−1 force H = K_k (every vertex adjacent to every other); and G may add only isolated vertices (any extra edge would push m past C(k,2)). So m = C(χ,2) exactly on K_k-plus-isolated-vertices. Machine check: over all 33,867 graphs on n ≤ 6 vertices, no graph violates m ≥ C(χ,2), and all 105 equality cases are exactly K_χ plus isolated vertices (the edgeless graph is the χ = 1 case) ✓. The honest lesson: the machine found the equality *classification* first — a bare "equality iff complete" is false (a single edge on three vertices is not complete), and the repair is the family above.

**A22.** The encoding (P1, and P25 Reduction / encoding in the companion Pattern Map): vertices 1, …, 6; give the edge between i < j the color of the integer j − i. Lecture 1's theorem says the resulting coloring of K₆ contains a monochromatic triangle, on vertices i < j < l. Monochromatic means the three differences j − i, l − j, l − i all carry one color — and the first two *sum to the third*. So the integers x = j − i, y = l − j, z = l − i = x + y all share a color, all lie in {1,…,5}: **every 2-coloring of {1,…,5} contains a monochromatic solution of x + y = z.** ∎ The dodge at n = 4: color {1, 4} red and {2, 3} blue — every solution x + y = z inside {1,…,4} (namely 1+1 = 2, 1+2 = 3, 1+3 = 4, 2+2 = 4) mixes colors ✓ (machine check: the census of all 32 colorings confirms {1,…,4} is the last sum-free zone and every one of the 32 colorings of {1,…,5} fails ✓). The encoding is a *pattern for a whole world*: arithmetic statements (sums, progressions) hide inside Ramsey statements about complete graphs; Volume II's Ramsey chapter reuses this bridge for van der Waerden and Schur's general theorem, and it is the same bridge ◆16 crossed in the other direction (Z₂⁴'s vector sums built the R(3,3,3) > 16 dodge).

---

## Computational Lab (verified)

### Part 1 — R(3,3) = 6 by total search (verified 2026-10-09)

```python
from itertools import combinations

def triangle_free_colorings(n):
    edges = list(combinations(range(n), 2))
    eidx = {e: i for i, e in enumerate(edges)}
    tris = [(eidx[(a,b)], eidx[(a,c)], eidx[(b,c)])
            for a, b, c in combinations(range(n), 3)]
    good = 0
    for mask in range(1 << len(edges)):
        ok = True
        for x, y, z in tris:
            if ((mask >> x) & 1) == ((mask >> y) & 1) == ((mask >> z) & 1):
                ok = False; break
        good += ok
    return good, 1 << len(edges)

print(triangle_free_colorings(5))   # (12, 1024)
print(triangle_free_colorings(6))   # (0, 32768)
```

**Verified output (2026-10-09):** K₅ — exactly **12 of 1024** colorings avoid a monochromatic triangle (12 = labeled 5-cycles: the C₅ dodge of Lecture 1.2, relabeled); K₆ — **0 of 32768** survive. **R(3,3) = 6, confirmed by total search.** Scaling lesson: each extra vertex doubles the work — the exponential wall is *why* Chapter 4's nonconstructive existence proofs matter.

### Part 2 — Mantel, greedy, and Rademacher by exhaustion on all graphs on 6 vertices (verified 2026-10-10)

```python
def greedy_color_count(adj, n):
    if n == 0:
        return 0
    color = [-1] * n
    for v in range(n):
        used = {color[u] for u in range(v) if adj[u][v]}
        c = 0
        while c in used: c += 1
        color[v] = c
    return max(color) + 1

n = 6
pairs = [(a, b) for a in range(n) for b in range(a + 1, n)]
max_tf_edges = 0; tf_at_max = 0; k33_witnesses = 0
e10 = 0; e10_trianglefree = 0
min_tri = 99; min_tri_count = 0
greedy_equal = 0; greedy_less = 0
for mask in range(1 << len(pairs)):
    adj = [[False]*n for _ in range(n)]
    deg = [0]*n; m = 0
    for i, (a, b) in enumerate(pairs):
        if mask >> i & 1:
            adj[a][b] = adj[b][a] = True; deg[a] += 1; deg[b] += 1; m += 1
    tri = sum(adj[a][b] and adj[a][c] and adj[b][c]
              for a in range(n) for b in range(a+1, n) for c in range(b+1, n))
    if tri == 0:
        if m > max_tf_edges: max_tf_edges = m; tf_at_max = 1
        elif m == max_tf_edges: tf_at_max += 1
        if m == 9:   # check the extremal ones really are K_{3,3}
            cdeg = [sum(1 for b in range(n) if b != a and not adj[a][b]) for a in range(n)]
            has_complement_triangle = any(
                (not adj[a][b]) and (not adj[a][c]) and (not adj[b][c])
                for a in range(n) for b in range(a+1, n) for c in range(b+1, n))
            if all(d == 2 for d in cdeg) and has_complement_triangle:
                k33_witnesses += 1
    if m == 10:
        e10 += 1
        if tri == 0: e10_trianglefree += 1
        if tri < min_tri: min_tri = tri; min_tri_count = 1
        elif tri == min_tri: min_tri_count += 1
    g = greedy_color_count(adj, n)
    if g == max(deg) + 1: greedy_equal += 1
    elif g < max(deg) + 1: greedy_less += 1
print(max_tf_edges, tf_at_max, k33_witnesses)
print(e10, e10_trianglefree, min_tri, min_tri_count)
print(greedy_equal, greedy_less)
```

**Verified output (2026-10-10):**
- **Mantel:** maximum edges of a triangle-free graph on 6 vertices = **9** = ⌊36/4⌋ ✓; exactly **10** extremal graphs, and **all 10 verified to be labeled K_{3,3}** (complement = two disjoint triangles) — the equality case is unique up to labeling ✓. All **3,003** graphs with 10 edges (C(15,10) = 3003 ✓) contain a triangle: **0** triangle-free ✓.
- **Rademacher instance:** among the 3,003 ten-edge graphs, the minimum triangle count is **3** (= ⌊6/2⌋), attained by exactly **60** graphs — matching the hand count 10 labeled K_{3,3} × 2 parts × 3 within-part edges (Exercise A13) exactly ✓.
- **Greedy:** over all 32,768 graphs, greedy (vertices in natural order) *never* exceeds Δ+1 — **0 violations**; it equals Δ+1 in **1,155** graphs and does strictly better in **31,613** — the ceiling is honest but usually slack, and order matters (Exercise A9).

**What to explore:** re-run Part 2 for n = 7 (2²¹ ≈ 2M graphs — minutes on a Raspberry Pi). The recorded answers: the triangle-free maximum is ⌊49/4⌋ = 12, the extremal graphs are the 35 labeled K_{3,4}; the greedy ceiling holds again; and at 13 edges the Rademacher minimum ⌊7/2⌋ = 3 is attained by exactly 210 graphs — all ≅ K_{3,4} plus one edge inside the 4-class (35 × 6, matching the construction). Then push to n = 8 at 17 edges — all 21,474,180 of them (hours, not minutes; the trick is a two-phase incremental build): minimum 4, exactly 420 witnesses, every one ≅ K₄,₄ plus one within-part edge, and *zero* graphs with exactly 5 triangles. That is Exploration X1's territory: at q = 2 edges over the top the minimum is 8 with 2,310 witnesses (K₄,₄ plus any two of the 12 within-part edges — three different shapes: 1,260 with one within-part edge in each part, 210 with two disjoint same-part edges, 840 with a same-part 2-edge path), at q = 3 it is 12.

---
## Revision History & Verification Notes

**Editions.** Reference edition → Feynman lecture edition (session 7, replacing the reference edition; Mantel's broken max-cut sketch replaced by the independent-set rod, three complete proofs) → first external review audited (session 26): five error fixes, recorded below → **backlog closed (session 27): every remaining honest flag and backlog item completed** — the full record follows → **adversarial review passed (session 61)**, recorded below → **Ch. 3 expansion pass adopted (session 87)**, recorded below.

**Backlog completion (session 27; every claim machine-verified before publication).** (1) **Turán completed both ways:** Method 1 (symmetrization) is now a complete proof — batch cloning onto a maximum-degree vertex, the induced K_r-free neighborhood, induction on r, and the convexity brick — with machine support: 161,874 batch tests on all (graph, r) with n ≤ 6, r ≤ 5 (K_{r+1}-freeness preserved every time, edge count never down, a no-op on every extremal graph — though not only on them; corrected in the follow-up audit below) and f(Δ) = (n−Δ)Δ + t_{r−1}(Δ) ≤ t_r(n) verified for all n ≤ 100, r ≤ 8, with the maximum exactly at Δ = n − ⌈n/r⌉ and, when r does not divide n, also at Δ = n − ⌊n/r⌋. A new **uniqueness section** proves the extremal graph is T_r(n) up to labeling (equality analysis by light-vertex deletion); the labeled-extremal census over all (n, r) with n ≤ 6 was re-run for publication: every extremal graph ≅ T_r(n), labeled counts 3, 3, 6, 10, 15, 10, 10, 15, 45, 15 = n!/(∏ part sizes! · ∏(multiplicities of equal parts)!) exactly. (2) **Brooks' theorem in full** (Lovász's construction): smart order for non-regular graphs, palette-matched pieces at a cut vertex, and the Lovász triple (both construction sub-cases proved); machine support: a vertex with two non-adjacent neighbors exists in all 26,283 connected non-complete Δ ≥ 3 graphs with n = 6, the triple plus breadth-first line-up gives a valid ≤ Δ-coloring on the 11,307 two-connected ones, and the χ = Δ+1 census over all connected graphs with n ≤ 6 (1, 1, 4, 38, 728, 26,704 by size) finds the ceiling attained exactly by complete graphs and odd cycles — zero violations. (3) **Rademacher's theorem in full:** per-edge triangle count + Cauchy–Schwarz give the second-moment bound T ≥ m(4m−n²)/(3n) (zero violations on all 33,864 graphs with 3 ≤ n ≤ 6), and a deletion induction closes every case, including the delicate δ = k corner (Lemma L′; 60-case census at n = 4, 6, zero violations). Censuses: n = 3..7 minima 1, 2, 2, 3, 3 (witnesses 1, 6, 30, 60, 210, matching the construction's labeled counts); at n = 8, all 21,474,180 seventeen-edge graphs: minimum 4, exactly 420 witnesses, all ≅ K₄,₄ plus one within-part edge, zero graphs with exactly 5 triangles; two and three edges over the top force minima 8 (2,310 witnesses) and 12. (4) **Five-color theorem** (§6.4): Kempe chains + the separation argument; census: all 32,647 planar-bound graphs on 6 vertices are 5-colorable, and at n = 7 the 232 graphs with δ ≥ 5 include 21 with χ = 6 but not one 6-critical graph (the only 6-critical graph on ≤ 7 vertices is K₆, which is not planar). (5) **Kuratowski** (§6.5): statement with the easy direction proved (contraction preserves planarity); the hard direction is honestly scoped out. (6) **R(3,4) = 9** as Exercise 14, both walls: machine search finds zero triangle-free graphs with α ≤ 3 on 9 vertices; the 8-vertex witness re-verified (triangle-free via disjoint endpoint neighborhoods, α = 3 via the L/H case analysis). (7) **The ◆/◐ retrofit:** gems 15–17 (Grötzsch graph re-verified — 11 vertices, 20 edges, 0 triangles, χ = 4, α = 5, Δ = 5; the Z₂⁴ sum-free partition re-verified, giving R(3,3,3) > 16, hence with Exercise 12 the exact value 17; the Z₁₃ circulant re-verified: triangle-free, red independence exactly 4, giving R(3,5) > 13) and explorations X1–X2 with recorded machine findings, stated not solved. The reviewer's three suggested figures are installed as Figures 1–3, and the web edition was rebuilt and verified byte-exact after all edits.

**First external review (audited session 26; every claim machine-verified before acting).** The reviewer confirmed the lab counts by independent extraction and execution (R(3,3): 12 of 1024 and 0 of 32,768; Mantel at n = 6: maximum 9 triangle-free edges, 10 extremal graphs all labeled K_{3,3}; 3,003 ten-edge graphs, minimum 3 triangles, 60 witnesses; greedy equal to Δ+1 in 1,155 of 32,768 graphs), endorsed the three Mantel proofs and the chapter architecture, and recommended targeted corrections, not a rewrite. Five fixes: (1) **Turán Method 2's induction premise was false** — a K_{r+1}-free graph need not contain a vertex of degree ≤ (1−1/r)(n−1): K_{3,3} has minimum degree 3 > 2.5 (machine-confirmed). Replaced by a complete edge-bound induction: the light-vertex lemma **δ ≤ n − ⌈n/r⌉ = ⌊(1−1/r)n⌋**, proved by clique-building (if every degree exceeded (1−1/r)n, the union bound on common neighborhoods grows a clique to K_{r+1} — verified on all 102,354 (graph, r) pairs with n ≤ 6, zero violations); the exact increment **t_r(n) − t_r(n−1) = n − ⌈n/r⌉** (verified for r = 2..5, n ≤ 40); and the deletion induction (base n ≤ r: t_r(n) = C(n,2)). The **uniqueness of the extremal graph is explicitly not claimed** — a separate equality analysis, on the backlog. (2) **The Ramsey gap ratio was miscalculated** — the chapter divided 4^k by 2^{k/2} and got 2^{k/2}; the correct ratio is 2^{3k/2}, and the passage now says so, keeping the binomial bound's √k factor honestly. (3) **Brooks' theorem lacked its connectedness hypothesis** — added, with the witness K₄ ⊔ K₂ (χ = 4 = Δ+1, neither complete nor an odd cycle). The connected form was machine-checked on all 27,475 connected graphs with n = 2..6 — zero violations — while 404 disconnected graphs with n ≤ 6 violate the unqualified form. (4) **Planar face counting qualified** — §6.2 and A8 now state the bounds for connected plane graphs via boundary *walks* (a bridge walked twice, once per side), with the componentwise / connect-with-noncrossing-edges route for disconnected graphs; the deductions for K₅, K_{3,3}, and Petersen were confirmed correct and stand; a stale "Exercise M3" reference (pre-retrofit numbering) repaired to Exercise 8. (5) **Exercise 13/A13's Rademacher construction corrected** — the domain is now n ≥ 3 (at n = 1, 2 the edge count ⌊n²/4⌋+1 exceeds C(n,2) and no such graph exists); the added edge goes inside the **larger** class (inside the smaller class is impossible at n = 3 and non-sharp for odd n, creating ⌈n/2⌉ triangles against Rademacher's ⌊n/2⌋); the exercise now asks for the sharp ⌊n/2⌋. Verified by total enumeration for n = 3..7 — minima 1, 2, 2, 3, 3, exactly ⌊n/2⌋ every time, with witness counts 1, 6, 30, 60, 210; the n = 5 and n = 7 counts match the corrected construction's labeled count exactly (10 × 3 = 30 labeled K_{2,3} with an edge inside the 3-class; 35 × 6 = 210 labeled K_{3,4} with an edge inside the 4-class). **Reviewer recommendations recorded:** the preserved strengths (three independent Mantel proofs, the two-beat threshold habit, the labs) stay; suggested figures (a two-panel red/blue K₅ Ramsey construction, a three-way Mantel proof comparison, Turán's balanced partite structure) go to the Atlas backlog per the figures-at-rewrite-time convention; the recommended next step is learner testing.

**Follow-up review audit (session 30; every claim machine-verified before acting).** A second, independent review of the rebuilt web-edition export confirmed the session-26 corrections and the completed proofs, re-executed the embedded labs — every count matched the records (R(3,3): 12 of 1,024 and 0 of 32,768; Mantel at n = 6: maximum 9 triangle-free edges, ten extremal graphs; 3,003 ten-edge graphs, minimum 3 triangles, 60 witnesses; greedy at Δ+1 on 1,155 of 32,768 graphs; the Z₂⁴ sum-free classes, the Z₁₃ circulant with zero red triangles and zero independent 5-sets, and the Grötzsch colorings' orbit of 30) — and recommended four localized corrections, not a rewrite. All four verified genuine and are installed: (1) **the Turán f(Δ) equality is two-valued when r ∤ n** — the maximum of f(Δ) = (n−Δ)Δ + t_{r−1}(Δ) is attained at Δ = n − ⌈n/r⌉ *and* at Δ = n − ⌊n/r⌋ (scan of all 672 pairs with n ≤ 100, r ≤ 8: the bound holds always, the maximum always equals t_r(n), the argmax set is exactly the two values, merging to one when r | n; n = 5, r = 3: both Δ = 3 and Δ = 4 worth 8): corrected in §5's convexity brick and in the session-27 record above; (2) **the labeled-extremal formula multiplied where it must divide** — the correct count is n! / (∏sᵢ! · ∏m_a!), with permutations of equal-sized parts divided out (K_{3,3} on six labeled vertices: 6!/(3!·3!·2!) = 10, not 40; the recorded census values were right all along): corrected in §5's uniqueness note and in the session-27 record; (3) **batch cloning is not a no-op only on the extremal graphs** — corrected census, 102,354 (graph, r) cases with n ≤ 6, r ≤ 5: K_{r+1}-freeness preserved and the edge count never down in every case, all 135 extremal cases no-ops for every maximum-degree choice, but 15,324 non-extremal no-op cases besides (the star K_{1,4}: nothing to clone, four edges against t₂(5) = 6): qualified in §5 and in the session-27 record; (4) **Kempe components are not always paths or cycles** — among 3,245 connected bipartite graphs on 4–6 labeled vertices only 63 are paths or cycles: §6.4 now describes components (bipartite, componentwise swap, alternating paths within a component), and the five-color proof, which uses only those facts, stands unchanged. The reviewer's optional fifth recommendation — an explicit note that Rademacher's guarantee extends to denser graphs by edge deletion, making the induction's above-threshold cases self-contained — was verified load-bearing (n = 5: all 176 graphs with ≥ 7 edges carry at least 2 triangles; n = 6: all 4,944 with ≥ 10 edges carry at least 3, ⌊n/2⌋ throughout, sharp examples at the threshold) and installed in the Rademacher lecture. The session-27 record's three over-claims are corrected in place above. Verdict adopted: no rewrite — the chapter is ready for learner testing, at the user's direction.

**Adversarial review (session 61; every retained objection machine-verified before acting; extend, never rewrite).** Two arguing experts (a skeptic and an engineer) walked the chapter chunk by chunk against a fresh exhaustive machine battery. Verdict: the mathematics is clean — every construction, proof skeleton, and recorded count re-verified green, including the wheels, Schur, Grötzsch, the Z₂⁴ and Z₁₃ colorings, the K₈ R(3,4) witness, R(3,3) over all 1,024 and 32,768 colorings, the Mantel/Rademacher/Turán/Brooks/five-color/max-cut/m ≥ C(χ,2)/Caro–Wei censuses at n ≤ 6, Rademacher at n = 3..8 including all 21,474,180 seventeen-edge graphs and the q = 2, 3 extensions, and the n = 7 battery. Six defect classes, all machine-confirmed and fixed in place: (1) **A19's value table said R(3,5) = 13 ≤ 15** — the true value is 14 (Lecture 2 and the formula box already said so; A17's dodge proves only > 13); corrected. (2) **A stray unbalanced parenthesis** closed §6.4's machine-census note; removed. (3) **§6.5's four-color coda credited "the philosophy of Chapter 11"** — stale; the Lean formal track has been Chapter 17 since session 56; corrected. (4) **Figure 2's panels drew 7, 7, and 6 of K₃,₃'s 9 edges** (a₂b₂ and a₃b₃ never drawn; panel 3 also missing a₁b₁, against its caption "every outside vertex sees A"); all nine edges now drawn in every panel, panel 3's A-side vertices filled dark with white labels, panel 2's three missing b-side vertex circles restored (15 of 18 were drawn), and panel 2's base layer no longer underlies the dashed light-vertex edges (the dashes were rendering solid). (5) **A20's max-cut note claimed exactly-m/2 for "5 cases, e.g. the triangle"** — false: the five exact-m/2 graphs are the five edgeless ones (m = 0), every graph with edges cuts strictly more, and the triangle is one of 70 edge-holding graphs tight at the ceiling ⌈m/2⌉ (75 counting the edgeless); rewritten. (6) **Scope labels**: the census counts 26,283 (connected non-complete Δ ≥ 3), 11,307 (2-connected), and 32,647 (planar-bound) are 6-vertex slices but were labeled "at most 6 vertices"/"n ≤ 6" — corrected in Lecture 3, §6.4, and the records above (the corresponding n ≤ 6 totals, 26,960 and 11,538, also verify green), together with two more count/scope mismatches of the same class (the 27,475 connected Brooks census is n = 2..6; the 33,866 max-cut census is n = 2..6). Honest notes: the session-27 record's 161,874 batch-test count does not reproduce under twelve natural conventions (the batch-clone census itself re-verified green under the r ≤ n convention, 102,354 pairs) — the qualitative claim stands and the text is unchanged, as with the session-30 audit's 15,324 non-extremal no-op figure (not reproducible under five conventions); the fresh n = 8, q = 3 census found 20,020 twelve-triangle minimizers, 12,600 of them outside the K₄,₄-plus-within-part-edges family — a genuine new finding recorded for Exploration X1; R(5,5)'s bounds 43–46 could not be re-verified this session (the search returned no usable snippets) and stand as recorded; and two checker-side false alarms during the battery (a component-edge counter bug at q = 1, a shape-tally reset bug at q = 2) were found, fixed, and re-run green before any edit. The web edition was rebuilt and verified byte-exact after all edits.

**Standing decisions.** Lecture text beyond the five review fixes, the seven backlog completions, and the four follow-up corrections above is unchanged; the lab code and its recorded outputs are unchanged by the **session-41 graded backfill (a user-directed exception, recorded here): exercises 18–22 + answers A18–A22 added, every number machine-verified before installation** — wheels χ-census W₄…W₉ (4,3,4,3,4,3); the Pascal ceiling R(s,t) ≤ C(s+t−2, s−1) checked against the known values (tight at R(3,3) = 6); the max-cut census over all 33,866 graphs on n = 2..6 (every cut ≥ m/2, five exactly-m/2 graphs); the m ≥ C(χ,2) census over all 33,867 graphs on n ≤ 6 with the machine-discovered equality family (K_χ plus isolated vertices, 105 cases, no others); the Schur census (S(2) = 4 — every 2-coloring of {1,…,5} fails, {1,4}/{2,3} dodges at {1,…,4}). The lab code and its recorded outputs are unchanged (the review reproduced them independently) — with one exception recorded here: the session-87 expansion pass added a two-line n == 0 guard to Part 2's greedy_color_count (a latent max([]) crash; the recorded outputs are untouched). The chapter's Atlas backlog is now **empty**. The recommended next step for the Ch. 2–5 feedback loop remains learner testing; the Ch. 4 external review follows at user direction.

**Survey-adoption pass (session 80).** One cross-reference repair: §6.5's four-color coda pointed at "the philosophy of Chapter 17" — the Lean formal track, whose chapter number was cancelled at user direction this session (it becomes the unnumbered companion, a project idea touched at the very end, and Ch. 17 becomes the semi-random method's planned chapter). The pointer now reads "the philosophy of the Lean formal track (the Atlas's unnumbered companion)". No mathematics changed. The .html export was rebaked per the rebuild rule, fidelity-first.

**Usage-evidence note (session 83).** The paper-pattern survey's usage ledger (papers/ANALYSIS.md, §4, in the cgt-atlas-backup repo) records the honest negative for this chapter's symmetrization card: P20 is genuinely under-used — the symmetrization work the field's classics actually do is performed by P23 shifting or P10 averaging (the survey's K7, Katona's circle method, is P10 partial work). Installed in the Trick Bag's P20 row; the entry stays canonical (cloning is this chapter's L5 engine), the note says honestly that the field reaches for other tools. The same datum is installed in Chapter 6's P20 card, the entry's other home. No proof, exercise, or answer changed. The .html export is rebaked at this session's export pass.

**Ch. 3 expansion pass (session 87; every claim machine-verified before installation; extend, never rewrite).** A user-supplied updated Chapter 3 draft (uploaded HTML, 104,613 B) was compared line by line against the standing master and adopted on merit — the third expansion-pass session, after Ch. 1 (session 85) and Ch. 2 (session 86). KEY FINDING, recorded honestly: the draft is NOT a large expansion like the Ch. 1/2 drafts — it is a light re-edit of the current master (it carries the session-80 Lean-track pointer and the session-83 P20 usage-evidence note verbatim), ~95% identical in content. Its real value: the draft exposes **six latent master defects, all repaired in place**: (1) Lecture 3's stale "**Exercise M4**" reference — pre-retrofit numbering; Exercise 9 (the crown) is the order-matters exercise, and the draft's "Exercise 9" is correct; (2) A19's garbled opener "…R(s−1,t) + R(s,t−1) − 1 < N − 1 + 1... count honestly:" — an abandoned-edit fragment, replaced by the clean count; (3) Lecture 2's garbled "trapped somewhere between roughly √2^k... precisely" fragment, replaced by the draft's clean statement; (4) A12's "|S| = 6" — the red neighborhood has **≥ 6** vertices, and R(3,3) = 6 applies to any 6 of them; (5) the second-moment receipt's scope label — 33,864 graphs are those on **3 ≤ n ≤ 6** (graphs on n ≤ 6 number 33,867), the session-61 scope-label class, fixed in the lecture and in the session-27 record above; (6) Figure 3's "= 12 up to rounding" — at n = 6, r = 3 the value (1 − 1/3)·n²/2 = 12 is exact. Adopted beyond the repairs: the recursion's explicit "for all s, t ≥ 2" domain and both induction bases, stated twice (Lecture 2: R(1,t) = R(s,1) = 1 with both binomial anchors; A19: R(s,2) = s = C(s, s−1), R(2,t) = t = C(t,1), plus the R(1,t)/R(s,1) parenthetical); the precise binomial asymptotic C(2k−2, k−1) ~ 4^{k−1}/√(πk), replacing "≈ 4^k/√k" in Lecture 2 and "~4^k" in the formula box; Brooks' Δ ≤ 2 case made airtight (a connected graph with Δ ≤ 1 is K₁ or K₂, both complete; Δ = 2 gives paths and cycles, colored with 2 = Δ colors); Mantel's Method-1 equality analysis completed (picking any edge uv, the disjoint independent sets N(u) and N(v) of size n/2 partition V, forcing all n²/4 cross-edges); the batch-clone paragraph's explicit degree bookkeeping (v's edges are untouched so d(v) = Δ stays fixed while any remaining b′'s degree can only drop, hence d(v) ≥ d(b′) at every step); the light-vertex lemma's integer step (d(v) ≥ n − ⌈n/r⌉ + 1 > (1 − 1/r)n); the exact-increment sentence made precise (the n-th vertex joins T_r(n)'s **largest** part, of size ⌈n/r⌉, grown from size ⌈n/r⌉ − 1 in T_r(n−1) — the old "joins its smallest part" read against the wrong graph); the uniqueness arithmetic's "(when s ≥ 2)" qualifier on the q+1 part sizes; §6.2's "with v ≥ 3" on the disconnected route; §6.3's v < 3 guard; Exercise 18's hint aligned with A18's rim-parity convention ("the rim needs two when **even**"); the graded-backfill block retitled "Further Graded Problems — each hint naming its pattern" (the session-85/86 precedent — "backfill" is project jargon); A7's cleanup (the "of size ≤ α... no —" stumble removed); A9's explicit induction (replacing "colors {1,…,i−1} possibly plus; work it through"); A14(b)'s explicit red-neighborhood table N(0)–N(7) with the L-pigeonhole step and the H-K_{2,2} structure; A16's human-readable C₁ argument (weights 1 and 4, so distinct sums have weight 2 or 3) with the C₂/C₃ note that all 10 pairwise sums per class land in the other two classes; and lab Part 2's greedy_color_count n == 0 guard (a latent max([]) crash — the session-86 guard precedent; recorded outputs unchanged). REJECTED, recorded honestly: the draft AS A FILE (MathJax CDN + $-TeX — violates the s78 no-script export rule; content only; identical ground to sessions 85/86); the draft's Exploration-X1 and lab-"What to explore" **K₃,₅ clause** — DEFECTIVE as written: the literal construction (K₃,₅ plus one edge inside the 5-part minus one incident cross-edge) has 15 edges, not the 18 a q = 2 minimizer on 8 vertices needs, and 2,310 = 35 labeled K₄,₄ × C(12,2) exactly exhausts the minimizer count (machine-checked: the K₄,₄-plus-two-within-edges family has exactly 2,310 distinct members; the 18-edge "star" K₃,₅ variant carrying 8 triangles is canonically isomorphic to K₄,₄ plus two adjacent within-part edges — no separate family exists); the draft's lab Part 2 main-code rewrite (the "m == e_rad_target if False else m == rad_edge" ternary is dead-code obfuscation with an undefined-name trap, against the s65 no-dead-clause discipline; its is_complete_bipartite_balanced is equivalent to the recorded complement check; outputs identical, so the master's recorded code stands); the draft's lab Part 1 n < 3 guard (semantically inert for all n ≥ 0 — dead code, s65); the draft's Mantel Method-2 lemma rewording (equivalent; the master's negation proof is complete); and the draft's Figure 1–3 redesigns (cosmetic variants — node radii, label placement, caption phrasings; the master's figures are the session-61-reviewed artifacts; only the Figure 3 "up to rounding" wording defect was adopted). Pattern-reference audit: **NO pattern ID misassigned anywhere in the draft** — the user's "mangled" concern resolves, as at sessions 85/86, to the stale M-numbering and the garbled fragments, all repaired; NO survey-era note dropped (the 83f P20 usage-evidence note is present in the draft — nothing needed restoring, unlike Ch. 1); exercise numbering UNCHANGED (1–22 + ◆15–17 + ◐X1–X2) → no Atlas reverse-index renumbering. Verification battery (TS ports, all GREEN before installation): the asymptotic ratio C(2k−2, k−1)·√(πk)/4^{k−1} → 1 over k = 5..40 (1.084 → 1.010); the second-moment census — all 33,864 graphs on 3..6 vertices, zero violations of 3nT ≥ m(4m − n²); the exact increment t_r(n) − t_r(n−1) = n − ⌈n/r⌉ for r = 2..5, n ≤ 40; the uniqueness arithmetic — min part of T_r(n−1) = ⌈n/r⌉ − 1 and a (q+1)-part present exactly when n mod r ≥ 2, same ranges; the A14(b) K₈ witness re-verified in full (10 red edges, triangle-free, the N-table exact, disjoint endpoint neighborhoods on all ten red edges, α = 3, every 3-subset of L containing a red pair, the H-K_{2,2} with non-edges 2–3 and 6–7, red degrees 2/3, the perfect matching 0–3/1–6/4–7/5–2); the A16 classes (C₁ weights 1 and 4 with distinct sums of weight 2 or 3; C₂/C₃ sums landing in the other two classes; the 15-vector partition; zero monochromatic triangles in K₁₆); the A9 crown induction (n = 2..6: exactly n colors, aᵢ and bᵢ both colored i); the greedy n = 0 guard; the 2,310-distinct-graphs count; the wheels census W₄..W₉ = 4, 3, 4, 3, 4, 3; and R(3,3) (12 of 1,024 at K₅, 0 of 32,768 at K₆). The .html export was rebaked per the rebuild rule, fidelity-first; the changed tree pushed under blob-sha gates.

**Ch. 3 expansion pass, second draft (session 98; every claim machine-verified before installation; extend, never rewrite).** A second user-supplied Chapter 3 draft (uploaded HTML, 128,964 B — a genuine new draft, +24 KB over the s87 draft, not a resubmission) was compared line by line against the standing master and adopted on merit — the fourth expansion-pass session. Adopted: the P25 "Reduction / encoding" labels on the Schur exercise's hint and A22 (the companion Pattern Map already registers Ch. 3 as P25's home; the master said only P1); three fuller worked answers — A3 (both non-planarity bounds spelled out), A8 (the face-walk length-≥-2-vs-K₂ justification and the disconnected case in full: components joined with compatibly flipped bipartitions, e ≤ 2v − 4 − (c − 1)), A10 (the Petersen girth-5 spoke-parity argument and the bridgeless facial-walk point); Mantel's Method 3 completed with the integer floor and the equality case in full — equality m = ⌊n²/4⌋ forces K_{⌊n/2⌋,⌈n/2⌉} at every n (machine-checked n ≤ 7: the triangle-free graphs attaining the bound are exactly the labeled balanced complete bipartite graphs — 1, 1, 3, 3, 10, 10, 35 of them, none else), with the theorem statement's even-n uniqueness clause extended accordingly; the Turán exact increment's algebraic verification clause (Σsᵢ² rises by 2q+1; identity machine-checked for n ≤ 60, r ≤ 8); and the X1 q = 2 shape census recorded exactly — 1,260 with one within-part edge in each part, 210 with two disjoint same-part edges, 840 with a same-part 2-edge path (machine-checked over the K₄,₄-plus-two-within family: exactly 2,310 distinct labeled graphs, decomposition unique). REJECTED, recorded honestly: the draft's ~400-line lab Part 3 census suite wholesale — its headline recorded output ("n=8 X1: … (630, 420, 1260)") is provably not the output of its own printed code (which computes (630, 210, 840)), and neither matches the combinatorial truth (1,260/210/840, machine-checked); its kempe_five_color function is defined but never invoked (advertised in the section title, never run anywhere); and its remaining recorded outputs re-derive counts already recorded in the lectures (connected graphs 1, 1, 4, 38, 728, 26,704; Brooks 26,283/11,307; second-moment 33,864/0; Rademacher minima and witnesses; the denser-graph 176/4,944; the Turán uniqueness census; the planar 32,647; X2 232/21/0; the A14(b)–A22 checks); the lab Part 1 n < 3 guard (rejected at session 87 already — inert); the lab Part 2 main-code rewrite (renames e10 → e_rad and k33 → k_ab, a bipartite-BFS witness check equivalent to the recorded complement check, inline output comments, a preserved-scratch comment — the s87 verdict stands); and the figures' tspan re-encodings (cosmetic; the s87 verdict stands). Pattern-reference audit (user-flagged again): CLEAN — the draft's pattern census equals the export's token for token (P10 = 9, P20 = 2, P23 = 1, …), the master's extra tokens are appendix-only (dropped from exports by design), the draft's "P3" is a lab-code subgraph-count false positive, and the P25 additions are correct canonical labels. Verification battery (all GREEN before installation): the Mantel equality census n = 1…7; the X1 family census (2,310 distinct labeled graphs, unique decomposition, shapes 1,260/210/840); the Turán increment identity t_r(n) − t_r(n−1) = n − ⌈n/r⌉ for n ≤ 60, r ≤ 8; the A3/A8/A10 arithmetic. The .html export was rebaked per the rebuild rule, fidelity-first; the changed tree pushed under blob-sha gates.

---

*Chapter status: ✅ **Feynman edition + backlog closed (session 27) + two external reviews audited (sessions 26, 30) + adversarial review passed (session 61) + expansion passes adopted (sessions 87, 98)** — 6 lectures, 6 problem families. Mantel with three complete proofs; Turán with two complete proofs **and the uniqueness of the extremal graph**; Brooks in full (Lovász); Rademacher in full (with the second-moment bound); five-color with Kempe chains; Kuratowski stated, easy direction proved. R(3,4) = 9 as a worked tough exercise; R(3,3,3) = 17 and R(3,5) > 13 as worked gems. 19 graded exercises (●○○–●●●, incl. the session-41 backfill 18–22: wheels, the Ramsey recursion + Pascal ceiling, half-bipartite max cut, chromatic edge pricing, Schur for two colors) + 3 gems (◆15–17) + 2 explorations (◐X1–X2), all with worked answers or recorded findings; verified labs ×2; three vector figures; web edition rebuilt and verified byte-exact. Every claim machine-verified before publication. Two external reviews and one adversarial review audited (session 26: five error fixes; session 30: four localized corrections — the Turán f(Δ) two-value equality, the labeled-count formula's divisor, the batch-clone no-op qualification, the Kempe component wording — plus the Rademacher deletion note; session 61 adversarial: six defect classes fixed — the A19 R(3,5) value, a stray parenthesis, the stale Chapter 11/17 pointer, Figure 2's missing edges and vertex circles, A20's max-cut equality cases, and mislabeled census scopes — fresh exhaustive battery otherwise green); session 87 expansion pass: the draft's six latent master defects repaired (the stale Exercise-M4 reference, two garbled fragments, A12's |S| = 6, the 33,864 scope label, Figure 3's "up to rounding") and its micro-upgrades adopted (explicit induction bases, the 4^{k−1}/√(πk) asymptotic, the batch-clone bookkeeping, the exact-increment precision, A9/A12/A14(b)/A16/A19 upgrades, the n == 0 lab guard), with five rejections recorded honestly — every claim machine-verified before installation; session 98 second expansion pass: the P25 Schur labels, fuller A3/A8/A10, Method 3's all-n equality case (K_{⌊n/2⌋,⌈n/2⌉} uniqueness machine-checked to n = 7), the Turán increment algebra clause, and the corrected X1 q = 2 shape census (1,260/210/840) adopted; the draft's defective lab Part 3 (a recorded output line that its own code cannot produce, an unused Kempe function) rejected with machine proof. Backlog: empty. Learner testing now runs at the end of the whole project scope (user direction, session 41).*
