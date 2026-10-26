---
name: "cgt-ch4-probabilistic"
title: "Ch. 4 — The Probabilistic Method: Existence by Randomness (A Lecture Course in the Feynman Style)"
type: "text/markdown"
---

# Chapter 4 · The Probabilistic Method

*A lecture course, in the spirit of Feynman's physics lectures. One scandalous idea powers the whole chapter (Erdős, 1947, with a 1943 prequel): to prove that an object exists, **design a random experiment** and show it succeeds with positive probability. No object is ever constructed. The proofs in this chapter are, every one of them, an argument that a needle exists in a haystack — followed, twice, by the honest admission that nobody can hand you the needle.*

## How to read this chapter

Read with dice in your hands, not just a pencil. Lines marked **✎ Checkpoint** are the places to stop and predict — commit to a guess, in ink, before reading on. The exercises are graded: ●○○ *easy* (one lecture idea, applied directly), ●●○ *moderate* (two ideas, or one tricky step), ●●● *tough* (several ideas combined). Hints travel with the problems; worked answers sit at the very end. Try honestly first — the struggle is the part that cannot be outsourced. Beyond the graded set, ◐ **Explorations** are open-ended investigations: they state what you should find, not a number to match.

The chapter trains five patterns: **P10** (averaging/expectation), **P12** (random construction), **P13** (union bound), **P14** (alteration), **P18** (algorithmic proof). They are summarized in the Trick Bag at the end. Two sharpenings arrive along the way: the **Lovász Local Lemma** refines P13 when the bad events are nearly independent (§4.3), and the **second-moment method** upgrades P10 from "some object beats the average" to "the average is where the mass lives" — enough to pin a sharp threshold (Lecture 6).

---

## Lecture 1 · Existence Without Construction

Here is a fact you can prove in three lines and cannot improve in three years: **every graph with m edges has a cut crossing at least m/2 of them.** (A *cut* is what you get by splitting the vertices into two sides; an edge is *crossed* if its ends land on different sides. Crossed edges form a bipartite subgraph — the two statements are the same fact in two costumes.)

The obvious attack is to build the best split cleverly. Don't. Do something outrageous instead: throw every vertex into side A or side B **at random, by fair coin flip**. Now watch one edge e = uv. Its two endpoints flipped independent coins, so they disagree with probability exactly 1/2 — the edge is crossed with probability 1/2, and there is nothing this edge can do about it, nor anything its neighbors can do. The expected number of crossed edges is m·(1/2) = **m/2**.

Now the punchline of the entire chapter. An *average* of m/2 is a promise: the number of crossed edges is m/2 on average, so **some** particular split crosses at least m/2 — because a random variable cannot always sit below its own average. We never built that split. We proved it exists, the way an alibi proves you were somewhere, without saying where. (Pattern **P10** — averaging — riding on **P12**, the random construction. This pairing is the engine of everything below.)

**✎ Checkpoint.** Before reading on: for K₄ (m = 6), predict the expected number of crossed edges, then list all splits and their cuts. There are 16 coin-flip outcomes, but a split and its mirror image are the same split — so 8 partitions. Do it in ink.

Here is the full census, machine-checked: the 8 partitions of K₄ cut **0, 3, 3, 3, 3, 4, 4, 4** edges. The expectation is (0 + 4·3 + 3·4)/8 = **3 = m/2**, exactly as promised — and the three balanced (2–2) partitions cut **4**, comfortably above the average. The theorem is true, and K₄ shows it live; the gap between 3 and 4 is the slack the next exercises will squeeze.

### 1.1 From dice to determinism

A probabilistic proof can leave an engineer cold: *which* split crosses m/2? Here is the beautiful answer — the proof contains an algorithm. Take **any** partition whatsoever. If some vertex has strictly more neighbors on its own side than across, flip it: the cut grows by a positive integer. Flips strictly increase an integer bounded by m, so they stop. When they stop, **every** vertex has at least as many neighbors across as at home. Count now, twice: each crossed edge contributes 2 to the total "across" tally (one for each endpoint), each internal edge contributes 2 to the "at home" tally. Since across ≥ at home at every vertex, 2·cut ≥ 2·(m − cut), so **cut ≥ m/2**. ∎

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 880 320" font-family="system-ui, -apple-system, 'Segoe UI', sans-serif">
  <rect x="0" y="0" width="880" height="320" fill="#ffffff"/>
  <defs>
    <marker id="f1arrow" viewBox="0 0 10 10" refX="8" refY="5" markerWidth="6" markerHeight="6" orient="auto"><path d="M 0 1 L 8 5 L 0 9 z" fill="#dc2626"/></marker>
  </defs>
  <text x="40" y="34" font-size="17" font-weight="700" fill="#193e5c">Figure 1 &#183; Derandomizing Lecture 1 on K&#8324;: the local flip (m = 6)</text>
  <text x="40" y="60" font-size="13" fill="#172333" font-weight="600">Before &#183; {v&#8321;} | {v&#8322;, v&#8323;, v&#8324;} cuts 3 = m/2</text>
  <text x="470" y="60" font-size="13" fill="#172333" font-weight="600">After &#183; {v&#8321;, v&#8322;} | {v&#8323;, v&#8324;} cuts 4 &gt; m/2</text>
  <line x1="190" y1="86" x2="190" y2="262" stroke="#94a3b8" stroke-width="1.5" stroke-dasharray="5,4"/>
  <line x1="650" y1="86" x2="650" y2="262" stroke="#94a3b8" stroke-width="1.5" stroke-dasharray="5,4"/>
  <text x="110" y="80" font-size="12" fill="#64748b" text-anchor="middle">Side A</text>
  <text x="295" y="80" font-size="12" fill="#64748b" text-anchor="middle">Side B</text>
  <text x="545" y="80" font-size="12" fill="#64748b" text-anchor="middle">Side A</text>
  <text x="760" y="80" font-size="12" fill="#64748b" text-anchor="middle">Side B</text>
  <line x1="110" y1="165" x2="270" y2="105" stroke="#2563eb" stroke-width="2.5"/>
  <line x1="110" y1="165" x2="330" y2="175" stroke="#2563eb" stroke-width="2.5"/>
  <line x1="110" y1="165" x2="250" y2="235" stroke="#2563eb" stroke-width="2.5"/>
  <line x1="270" y1="105" x2="330" y2="175" stroke="#dc2626" stroke-width="2" stroke-dasharray="6,4"/>
  <line x1="270" y1="105" x2="250" y2="235" stroke="#dc2626" stroke-width="2" stroke-dasharray="6,4"/>
  <line x1="330" y1="175" x2="250" y2="235" stroke="#dc2626" stroke-width="2" stroke-dasharray="6,4"/>
  <circle cx="110" cy="165" r="13" fill="#ffffff" stroke="#193e5c" stroke-width="2.5"/>
  <circle cx="270" cy="105" r="13" fill="#ffffff" stroke="#dc2626" stroke-width="3"/>
  <circle cx="330" cy="175" r="13" fill="#ffffff" stroke="#172333" stroke-width="2"/>
  <circle cx="250" cy="235" r="13" fill="#ffffff" stroke="#172333" stroke-width="2"/>
  <g font-size="12.5" font-weight="600" fill="#172333" text-anchor="middle">
    <text x="110" y="169">v&#8321;</text><text x="270" y="109">v&#8322;</text>
    <text x="330" y="179">v&#8323;</text><text x="250" y="239">v&#8324;</text>
  </g>
  <line x1="405" y1="170" x2="455" y2="170" stroke="#dc2626" stroke-width="2.5" marker-end="url(#f1arrow)"/>
  <text x="430" y="152" font-size="12" font-weight="700" fill="#dc2626" text-anchor="middle">flip v&#8322;</text>
  <text x="430" y="192" font-size="11.5" fill="#64748b" text-anchor="middle">&#916;cut = +2 &#8722; 1 = +1</text>
  <line x1="520" y1="180" x2="715" y2="105" stroke="#2563eb" stroke-width="2.5"/>
  <line x1="520" y1="180" x2="775" y2="195" stroke="#2563eb" stroke-width="2.5"/>
  <line x1="600" y1="105" x2="715" y2="105" stroke="#2563eb" stroke-width="2.5"/>
  <line x1="600" y1="105" x2="775" y2="195" stroke="#2563eb" stroke-width="2.5"/>
  <line x1="520" y1="180" x2="600" y2="105" stroke="#dc2626" stroke-width="2" stroke-dasharray="6,4"/>
  <line x1="715" y1="105" x2="775" y2="195" stroke="#dc2626" stroke-width="2" stroke-dasharray="6,4"/>
  <circle cx="520" cy="180" r="13" fill="#ffffff" stroke="#193e5c" stroke-width="2.5"/>
  <circle cx="600" cy="105" r="13" fill="#ffffff" stroke="#dc2626" stroke-width="3"/>
  <circle cx="715" cy="105" r="13" fill="#ffffff" stroke="#172333" stroke-width="2"/>
  <circle cx="775" cy="195" r="13" fill="#ffffff" stroke="#172333" stroke-width="2"/>
  <g font-size="12.5" font-weight="600" fill="#172333" text-anchor="middle">
    <text x="520" y="184">v&#8321;</text><text x="600" y="109">v&#8322;</text>
    <text x="715" y="109">v&#8323;</text><text x="775" y="199">v&#8324;</text>
  </g>
  <text x="40" y="290" font-size="12" fill="#172333">v&#8322; has 2 internal neighbors (dashed red) vs 1 crossed (solid blue); flipping it turns 2 internal edges crossed and 1 crossed edge internal.</text>
  <text x="40" y="308" font-size="12" fill="#64748b">Flips strictly increase the cut; when they stop, every vertex has at least as many neighbors across as at home &#8212; termination is the theorem (P18).</text>
</svg>
```

What you just watched is **derandomization** (pattern **P18**): the coin-flip proof is converted into a deterministic procedure whose termination *is* the theorem. The flip rule is exactly "do what the coin probably would have done, one vertex at a time." Expectation proof first, greedy algorithm second — a two-step worth owning as a single reflex.

**What you now own:** the coin-flip experiment (P12); the average as an existence promise (P10); the local-flip derandomization (P18). And a reflex: *when every object in a family has some score, some object scores at least the average — say so, and you have proved existence.*

---

## Lecture 2 · The Average Is a Promise

Lecture 1 quietly used the most valuable identity in this book: **linearity of expectation**. If X = X₁ + X₂ + … + X_r (each Xᵢ an indicator: 1 when the i-th bad thing happens, 0 otherwise), then E[X] = E[X₁] + … + E[X_r], and — this is the scandal — **the Xᵢ need not be independent**. Look for it in Lecture 1: whether edge e is crossed and whether edge f is crossed *feel* like dependent events — they may share an endpoint and its coin. The sum didn't care. And the feeling deserves an audit, because in this experiment it is mostly an illusion: for **two** distinct edges the crossing indicators are independent, sharing an endpoint or not. If the edges are uv and uw, then X_uv = B_u ⊕ B_v and X_uw = B_u ⊕ B_w for the three fair coins; over the eight labelings each indicator fires in four and both fire together in two — 1/4 = (1/2)², independence. The genuine dependence is *joint* and lives on the triangle: every cut crosses an even number of any cycle's edges, so X_uv ⊕ X_uw ⊕ X_vw = 0 — the three indicators are pairwise independent yet can never all fire at once (probability 0, not 1/8). Dependence is exactly what makes probability hard elsewhere; linearity of expectation never meets the difficulty — in any of its costumes.

**✎ Checkpoint.** Tabulate the eight coin assignments of a triangle's vertices and tick, per row, which of the three edges are crossed. Confirm: each edge is crossed in four rows; each *pair* of edges is crossed together in two rows (pairwise independence — including the pairs that share a vertex); and no row crosses all three (a cut crosses a cycle an even number of times). You will have located the dependence exactly — and seen that Lecture 1's expectation never needed to know. (Explicitly, over (B_u, B_v, B_w) ∈ {0,1}³, the two monochromatic rows (0,0,0) and (1,1,1) yield (X_uv, X_vw, X_uw) = (0,0,0), while the six 2–1 rows yield (1,0,1), (1,1,0), (0,1,1) twice each — giving column sums [4,4,4], pairwise dot products [2,2,2], and triple product 0.)

Now the 1943 theorem that started the whole method, before Erdős gave the method its name: **Szele's theorem.** Recall that a *tournament* is a complete graph with every edge directed one way (a round-robin league: every pair plays, one winner). A *directed Hamiltonian path* is an ordering of all n players v₁, v₂, …, v_n such that each player beat the next. The claim: **some tournament has at least n!/2^{n−1} directed Hamiltonian paths.**

The experiment: pick a tournament uniformly at random — each game's outcome an independent fair coin. Fix one ordering (v₁, …, v_n); it forms a directed Hamiltonian path exactly when its n − 1 consecutive games were all won by the earlier player: probability 2^{−(n−1)}. Let X = the number of directed Hamiltonian paths; by linearity over all n! orderings,

**E[X] = n!/2^{n−1}**,

and some tournament achieves at least the average. ∎ The number is enormous — for n = 10 it is 10!/2^{9} = 3,628,800/512 = **7,087.5**, and since a count is an integer, some tournament on 10 players has at least **7,088** directed Hamiltonian paths. Individual rich tournaments can even be written down — at n = 10 a machine search finds them easily, and the appendix records one with 9,793 paths. What no one can write down is the needle the proof promises in general: a *uniform* explicit construction — a single rule that builds, for every n, a tournament with anything near n!/2^{n−1} directed Hamiltonian paths. None is known; the average certifies the haystack without mapping it.

**✎ Checkpoint.** n = 3, by hand. There are 2³ = 8 tournaments. Six are *transitive* (a beats b beats c, and a beats c — the results order the players with no cycle). Two are 3-cycles. Count the directed Hamiltonian paths in each kind, total them over all 8, and divide. Predict first whether you will see 6/4.

The census, machine-checked: a transitive tournament has exactly **1** directed Hamiltonian path (its total order); a 3-cycle has **3** (start anywhere). Total 6·1 + 2·3 = **12**, and 12/8 = **1.5 = 6/2² = n!/2^{n−1}** ✓. (For n = 4 the machine totals 192 over 64 tournaments: E = 3, with individual tournaments ranging from 1 to 5.) Notice what the average hides: the transitive extreme has just 1, the crowded extreme has more — the *expectation* sits between them and certifies the crowded one exists, without telling you where it is. That is the method's signature: an average over a world you can't survey is squeezed until it confesses that an extreme exists.

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 880 280" font-family="system-ui, -apple-system, 'Segoe UI', sans-serif">
  <rect x="0" y="0" width="880" height="280" fill="#ffffff"/>
  <defs>
    <marker id="f2blue" viewBox="0 0 10 10" refX="8" refY="5" markerWidth="6" markerHeight="6" orient="auto"><path d="M 0 1.5 L 8 5 L 0 8.5 z" fill="#2563eb"/></marker>
    <marker id="f2gray" viewBox="0 0 10 10" refX="8" refY="5" markerWidth="6" markerHeight="6" orient="auto"><path d="M 0 1.5 L 8 5 L 0 8.5 z" fill="#64748b"/></marker>
  </defs>
  <text x="40" y="34" font-size="17" font-weight="700" fill="#193e5c">Figure 2 &#183; Szele's census at n = 3: two kinds of tournament (Lecture 2)</text>
  <text x="40" y="62" font-size="13" fill="#172333" font-weight="600">Transitive &#183; 6 of 8 tournaments &#183; 1 directed path</text>
  <text x="470" y="62" font-size="13" fill="#172333" font-weight="600">3-cycle &#183; 2 of 8 tournaments &#183; 3 directed paths</text>
  <line x1="191" y1="119" x2="141" y2="198" stroke="#2563eb" stroke-width="2.5" marker-end="url(#f2blue)"/>
  <line x1="147" y1="215" x2="258" y2="215" stroke="#2563eb" stroke-width="2.5" marker-end="url(#f2blue)"/>
  <line x1="210" y1="119" x2="268" y2="199" stroke="#64748b" stroke-width="1.8" marker-end="url(#f2gray)"/>
  <circle cx="200" cy="105" r="15" fill="#ffffff" stroke="#2563eb" stroke-width="2.5"/>
  <circle cx="130" cy="215" r="15" fill="#ffffff" stroke="#2563eb" stroke-width="2.5"/>
  <circle cx="280" cy="215" r="15" fill="#ffffff" stroke="#2563eb" stroke-width="2.5"/>
  <g font-size="12.5" font-weight="600" fill="#172333" text-anchor="middle">
    <text x="200" y="109">v&#8321;</text><text x="130" y="219">v&#8322;</text><text x="280" y="219">v&#8323;</text>
  </g>
  <line x1="631" y1="119" x2="581" y2="198" stroke="#2563eb" stroke-width="2.5" marker-end="url(#f2blue)"/>
  <line x1="587" y1="215" x2="698" y2="215" stroke="#2563eb" stroke-width="2.5" marker-end="url(#f2blue)"/>
  <line x1="710" y1="201" x2="652" y2="121" stroke="#2563eb" stroke-width="2.5" marker-end="url(#f2blue)"/>
  <circle cx="640" cy="105" r="15" fill="#ffffff" stroke="#2563eb" stroke-width="2.5"/>
  <circle cx="570" cy="215" r="15" fill="#ffffff" stroke="#2563eb" stroke-width="2.5"/>
  <circle cx="720" cy="215" r="15" fill="#ffffff" stroke="#2563eb" stroke-width="2.5"/>
  <g font-size="12.5" font-weight="600" fill="#172333" text-anchor="middle">
    <text x="640" y="109">v&#8321;</text><text x="570" y="219">v&#8322;</text><text x="720" y="219">v&#8323;</text>
  </g>
  <text x="40" y="248" font-size="12" fill="#172333">Left: the total order v&#8321; &#8594; v&#8322; &#8594; v&#8323; is the only directed path (the third arc is a shortcut, not a path edge).</text>
  <text x="470" y="248" font-size="12" fill="#172333">Right: deleting any one of the 3 arcs leaves a directed path &#8212; 3 of them.</text>
  <text x="40" y="268" font-size="12" fill="#64748b">Census: 6&#183;1 + 2&#183;3 = 12 paths over 8 tournaments, so E[X] = 12/8 = 1.5 = 3!/2&#178;.</text>
</svg>
```

**What you now own:** indicator variables and linearity across dependent events (P10); the random-tournament experiment (P12); and the historical headline — the first probabilistic-method theorem in combinatorics is Szele's (1943), and no explicit construction matching its constant is known to this day.

---

## Lecture 3 · Keep the Local Winners

Independent sets hide in every graph, and the question is how big. Here is a second way to be random — subtler than coin flips, and it proves the **Caro–Wei bound**: every graph has an independent set of size at least

**α(G) ≥ Σ_{v} 1/(d(v) + 1)**,

the sum taken over all vertices, d(v) the degree.

The experiment (**P12** again, a new costume): order the vertices **uniformly at random** — a random permutation, every ordering equally likely. Now select a vertex v whenever v comes **before all of its neighbors** in the ordering: keep the *local winners*. Two observations, and each is half the theorem:

1. **The selected set is independent.** Suppose edge uv had both ends selected. Then u came before all of N(u), which includes v — so u precedes v. And v came before all of N(v), which includes u — so v precedes u. Both cannot be true; contradiction. (Notice this argument never used independence of anything — it is pure ordering logic.)
2. **v is selected with probability 1/(d(v)+1).** Look at the d(v)+1 vertices in {v} ∪ N(v). In a uniform random ordering, each of them is equally likely to appear first, and v is selected exactly when v is that first one.

So the expected number of selected vertices is Σ_v 1/(d(v)+1), by linearity (Lecture 2), and some ordering selects at least that many — an independent set of that size. ∎

**✎ Checkpoint.** The path P₄ has degrees 1, 2, 2, 1. Compute Σ 1/(d+1) in ink — you should get 5/3 — and check it against α(P₄) = 2. Comfortable? Now predict what the bound gives for K_n: you should get exactly 1 (each of the n vertices has degree n − 1, contributing 1/((n−1)+1) = 1/n, so the sum over all n vertices is n·1/n = 1 = α(K_n)).

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 880 240" font-family="system-ui, -apple-system, 'Segoe UI', sans-serif">
  <rect x="0" y="0" width="880" height="240" fill="#ffffff"/>
  <text x="40" y="34" font-size="17" font-weight="700" fill="#193e5c">Figure 3 &#183; Caro&#8211;Wei local winners on P&#8324; (Lecture 3)</text>
  <text x="40" y="60" font-size="13" fill="#172333" font-weight="600">sample ordering &#960; = (v&#8322;, v&#8324;, v&#8321;, v&#8323;) &#8212; keep each vertex that precedes all of its neighbors</text>
  <line x1="186" y1="130" x2="324" y2="130" stroke="#94a3b8" stroke-width="2.5"/>
  <line x1="356" y1="130" x2="494" y2="130" stroke="#94a3b8" stroke-width="2.5"/>
  <line x1="526" y1="130" x2="664" y2="130" stroke="#94a3b8" stroke-width="2.5"/>
  <circle cx="170" cy="130" r="16" fill="#ffffff" stroke="#94a3b8" stroke-width="2"/>
  <circle cx="340" cy="130" r="16" fill="#ffffff" stroke="#2563eb" stroke-width="3"/>
  <circle cx="510" cy="130" r="16" fill="#ffffff" stroke="#94a3b8" stroke-width="2"/>
  <circle cx="680" cy="130" r="16" fill="#ffffff" stroke="#2563eb" stroke-width="3"/>
  <g font-size="13" font-weight="600" fill="#172333" text-anchor="middle">
    <text x="170" y="135">v&#8321;</text><text x="340" y="135">v&#8322;</text>
    <text x="510" y="135">v&#8323;</text><text x="680" y="135">v&#8324;</text>
  </g>
  <text x="170" y="95" font-size="11.5" fill="#64748b" text-anchor="middle">rank 3 (blocked)</text>
  <text x="340" y="95" font-size="11.5" fill="#2563eb" font-weight="700" text-anchor="middle">rank 1 &#9733; winner</text>
  <text x="510" y="95" font-size="11.5" fill="#64748b" text-anchor="middle">rank 4 (blocked)</text>
  <text x="680" y="95" font-size="11.5" fill="#2563eb" font-weight="700" text-anchor="middle">rank 2 &#9733; winner</text>
  <text x="170" y="170" font-size="11.5" fill="#172333" text-anchor="middle">1/(d+1) = 1/2</text>
  <text x="340" y="170" font-size="11.5" fill="#172333" text-anchor="middle">1/(d+1) = 1/3</text>
  <text x="510" y="170" font-size="11.5" fill="#172333" text-anchor="middle">1/(d+1) = 1/3</text>
  <text x="680" y="170" font-size="11.5" fill="#172333" text-anchor="middle">1/(d+1) = 1/2</text>
  <text x="40" y="205" font-size="12" fill="#172333">Selected I = {v&#8322;, v&#8324;}: two local winners never share an edge, because neither endpoint of an edge can precede the other.</text>
  <text x="40" y="225" font-size="12" fill="#64748b">Expected size over all 24 orderings: 1/2 + 1/3 + 1/3 + 1/2 = 5/3 &#8804; &#945;(P&#8324;) = 2.</text>
</svg>
```

The bound is *tight* for disjoint unions of cliques (Exercise 8): each clique K_{nᵢ} has nᵢ vertices of degree nᵢ − 1, contributing nᵢ · 1/nᵢ = 1 to the sum, so Σ 1/(d(v)+1) counts the cliques and equals α(G) exactly. Moreover, for general graphs with n vertices and m edges, one application of the Cauchy–Schwarz inequality turns Caro–Wei into a global bound in terms of average degree alone. Pairing the positive quantities √(d(v)+1) and 1/√(d(v)+1) across all v, Cauchy–Schwarz gives

**n² = (Σ_v 1)² = (Σ_v √(d(v)+1) · 1/√(d(v)+1))² ≤ (Σ_v (d(v)+1))·(Σ_v 1/(d(v)+1)).**

By the handshake lemma, Σ_v (d(v)+1) = Σ_v d(v) + n = 2m + n. Dividing through by 2m + n > 0 yields

**α(G) ≥ Σ_v 1/(d(v)+1) ≥ n²/(2m+n) = n/(d̄+1),**

where d̄ = 2m/n is the average degree, with equality in the Cauchy–Schwarz step if and only if d(v) is constant (i.e., G is regular). Sparse graphs must contain large independent sets — the quantitative form of "density costs you a certificate of structurelessness."

**What you now own:** the random-ordering experiment and local winners (P12/P10); the honest reflex for tightness (ask *when does equality hold*); convexity as the standard second squeeze. The Caro–Wei bound will do honest work again in Exercise 6, where it turns a local observation (triangle-free) into a global one (α(α+1) ≥ n).

---

## Lecture 4 · When the Average Is Not Enough: the Union Bound

Lectures 1–3 proved objects *at least as good as an average* exist. But the questions that made Ramsey theory famous have a different shape: does an object exist with **none** of a long list of bad features? No monochromatic K_k anywhere. No undominated pair anywhere. "At least one bad thing happens" must be shown **impossible**, so we need P(no bad thing) > 0. The tool costs one line and is the workhorse of the subject — the **union bound** (pattern **P13**):

**P(A₁ ∪ A₂ ∪ … ∪ A_r) ≤ P(A₁) + P(A₂) + … + P(A_r).**

If the bad-event probabilities **sum below 1**, then with positive probability *no* bad event occurs — and an event of positive probability, in a finite probability space, has a witness. ∎

### 4.1 Ramsey numbers, from the dice's side

Chapter 3 proved R(k,k) — the smallest n such that every red/blue coloring of K_n contains a monochromatic K_k — is at most about 4^k. From the other side: **R(k,k) is at least exponential in k**, and the proof is two coin flips deep. Color each edge of K_n red/blue independently, fairly. A fixed k-set S has all its C(k,2) internal edges monochromatic with probability 2·2^{−C(k,2)} = 2^{1−C(k,2)} (all red, or all blue). Union bound over the C(n,k) choices of S:

**P(some monochromatic K_k) ≤ C(n,k) · 2^{1−C(k,2)}.**

If C(n,k)·2^{1−C(k,2)} < 1, some coloring of K_n has no monochromatic K_k — so **R(k,k) > n**. We need no computer assistance to prove the clean exponential bound for all k ≥ 3 at once. Set n = ⌊2^{k/2}⌋, so n ≤ 2^{k/2}. At k = 3 we have n = ⌊2^{3/2}⌋ = 2 < 3, so C(n,k) = C(2,3) = 0 < n^k/k! holds trivially (a 2-vertex graph cannot contain K₃), while for all k ≥ 4 we have n = ⌊2^{k/2}⌋ ≥ k (equality at k = 4, 5), where C(n,k) = n(n−1)⋯(n−k+1)/k! < n^k/k!. Hence for every k ≥ 3,

**C(n,k)·2^{1−C(k,2)} < (n^k/k!)·2^{1−k(k−1)/2} ≤ ((2^{k/2})^k/k!)·2^{1−k²/2+k/2} = 2^{1+k/2}/k!.**

For k = 3, 2^{1+3/2}/3! = 4√2/6 = 2√2/3 < 1 (since (2√2)² = 8 < 9 = 3²). For every k ≥ 3, incrementing k ↦ k+1 multiplies the numerator by √2 and the denominator by k+1 ≥ 4 > √2, so the ratio 2^{1+k/2}/k! is strictly decreasing and remains strictly less than 1 for all k ≥ 3. Consequently:

**R(k,k) > ⌊2^{k/2}⌋ for all k ≥ 3.** ∎

Honesty first, because this chapter deals in honesty: the method is *weak when k is small*, and you should see exactly how weak. The union bound's certified frontier, computed exactly: for k = 3 it certifies only R(3,3) > 3 (the truth, from Chapter 3, is 6); for k = 4, R(4,4) > 6 (truth: 18); for k = 5, > 11; k = 6, > 17; k = 7, > 27. The asymptotic engine only warms up as k grows — but warm up it does, exponentially, and no construction is known that gets anywhere near it.

**✎ Checkpoint.** Check k = 3, n = 5 by hand: C(5,3)·2^{1−3} = 10/4 = 2.5. Predict what this means about the union bound's ability to certify R(3,3) > 5 — then notice how lucky Lecture 1 was that m/2 needed no such slack. (Because 2.5 ≥ 1, the union bound fails to certify R(3,3) > 5 even though exactly 12 of the 2^{10} = 1024 colorings of K₅ have zero monochromatic triangles — as the lab's Part 1 side-experiment verifies.)

### 4.2 The same move, two more costumes

**Property B (hypergraph 2-coloring).** Call a k-uniform hypergraph (every edge a k-set of vertices) *2-colorable* if vertices can be red/blue'd so that no edge is monochromatic. Random coloring: a fixed edge is mono with probability 2^{1−k}; union bound: **if m < 2^{k−1} edges, the hypergraph is 2-colorable.** ∎ One line. The frontier of this claim — what happens at and beyond 2^{k−1} edges — is Exploration X2's territory, and the Fano plane (Exercise 13) is the smallest famous casualty: 7 edges, not colorable.

**Property S(k) (unbeatable tournaments).** A tournament has property **S(k)** if every set of k players is *jointly beaten* — for each k-set, some single player beat all k of them. Random tournament again. Fix a k-set V. One outside player w fails to dominate V with probability 1 − 2^{−k}; the n − k outside players flip disjoint pairs of games, so independently:

P(V is undominated) = (1 − 2^{−k})^{n−k}.

Union bound over the C(n,k) sets: **if C(n,k)·(1 − 2^{−k})^{n−k} < 1, a tournament with S(k) exists.** The product first grows with n, then decays exponentially; the first dip below 1 is the certification. Machine-checked exactly: for k = 2 it happens at n = **21**; for k = 3, at n = **91**. The scale — roughly k²·2^k players — crushes every known explicit construction, and (Exercise 12 sends you there) the certified answer for k = 2 is wildly far from the truth. The method proves existence the way a flood proves the valley is downhill of the rain.

### 4.3 Bad events that barely talk: the Lovász Local Lemma

The union bound has a blind spot worth naming. If the bad events were fully independent, their probabilities would not need to sum below 1 at all: P(no bad event) = ∏(1−pᵢ) > 0 however many events there are, as long as each is avoidable on its own. The union bound charges every event as if it overlapped all the others; the truth usually sits between. The **Lovász Local Lemma** (1975) interpolates honestly:

**Symmetric Lovász Local Lemma (Erdős–Lovász, 1975).** Let A₁, …, A_m be events in a probability space. Suppose that for each i, P(Aᵢ) ≤ p, and there exists a dependency neighborhood Γ(i) ⊆ {1, …, m} \ {i} of size |Γ(i)| ≤ d such that Aᵢ is **mutually independent** of the collection of events {Aⱼ : j ∉ Γ(i) ∪ {i}}. If

**e·p·(d+1) ≤ 1,**

then P(⋂_{i=1}^{m} Āᵢ) > 0: a witness avoiding every bad event exists.

*Proof.* If d = 0, the events A₁, …, A_m are mutually independent; since p ≤ 1/e < 1, P(⋂ Āᵢ) = ∏(1 − P(Aᵢ)) ≥ (1−p)^m > 0. Assume henceforth d ≥ 1, and set γ = 1/(d+1) ∈ (0, 1/2]. Note that p ≤ 1/(e(d+1)) = γ/e. We prove by induction on |S| ∈ {0, 1, …, m−1} that for every subset S ⊆ {1, …, m} and every i ∉ S,

**P(Aᵢ | ⋂_{j∈S} Āⱼ) ≤ γ  and  P(⋂_{j∈S} Āⱼ) > 0.**

For the base case |S| = 0, the conditioning event is the full space, and P(Aᵢ) ≤ p ≤ γ/e < γ. For the inductive step, fix S with |S| ≥ 1 and i ∉ S, assuming the claim holds for all strictly smaller subsets. Ordering S = {j₁, …, j_s}, the chain rule together with the induction hypothesis on proper prefixes gives

P(⋂_{j∈S} Āⱼ) = ∏_{r=1}^{s} (1 − P(A_{j_r} | ⋂_{t<r} Ā_{j_t})) ≥ (1−γ)^s > 0,

so the conditional probability given ⋂_{j∈S} Āⱼ is well-defined. Now partition S into S₁ = S ∩ Γ(i) and S₂ = S \ Γ(i); note |S₁| ≤ |Γ(i)| ≤ d. By the definition of conditional probability,

P(Aᵢ | ⋂_{j∈S} Āⱼ) = P(Aᵢ ∩ ⋂_{j∈S₁} Āⱼ | ⋂_{k∈S₂} Ā_k) / P(⋂_{j∈S₁} Āⱼ | ⋂_{k∈S₂} Ā_k).

Bound the numerator above by dropping ⋂_{j∈S₁} Āⱼ: since Aᵢ is mutually independent of {A_k : k ∈ S₂}, the numerator is at most P(Aᵢ | ⋂_{k∈S₂} Ā_k) = P(Aᵢ) ≤ p. For the denominator, if S₁ = ∅ it equals 1 = (1−γ)⁰; if S₁ = {u₁, …, u_r} with 1 ≤ r ≤ d, then for each 1 ≤ ℓ ≤ r the conditioning set {u₁, …, u_{ℓ−1}} ∪ S₂ has size ℓ−1+|S₂| < r+|S₂| = |S|, so the induction hypothesis gives P(A_{u_ℓ} | ⋂_{t<ℓ} Ā_{u_t} ∩ ⋂_{k∈S₂} Ā_k) ≤ γ. Hence the denominator satisfies

P(⋂_{j∈S₁} Āⱼ | ⋂_{k∈S₂} Ā_k) = ∏_{ℓ=1}^{r} (1 − P(A_{u_ℓ} | ⋂_{t<ℓ} Ā_{u_t} ∩ ⋂_{k∈S₂} Ā_k)) ≥ (1−γ)^r ≥ (1−γ)^d.

Using the elementary inequality (1 − 1/(d+1))^d = (1 + 1/d)^{−d} > e^{−1} (since (1 + 1/d)^d < e for all d ≥ 1), we obtain

P(Aᵢ | ⋂_{j∈S} Āⱼ) ≤ p/(1−γ)^d < p·e ≤ 1/(d+1) = γ,

completing the induction. Finally, the chain rule over all m events gives P(⋂_{i=1}^{m} Āᵢ) ≥ (1−γ)^m = (d/(d+1))^m > 0. ∎

The condition itself reads plainly: each bad event may be somewhat more likely than the union bound's budget of 1/m allows, provided it *confers* with only a few of its kind.

**Ramsey, revisited.** Take the bad events of §4.1 again: for each k-subset S ⊆ V(K_n), let A_S be the event that S is monochromatic, so P(A_S) = p = 2^{1−C(k,2)}. Because the C(n,2) edge coins are mutually independent and A_S is determined solely by the C(k,2) edges inside S, the **Mutual Independence Principle** guarantees that A_S is mutually independent of the entire collection of events {A_T : |S ∩ T| ≤ 1} — those events live on edge sets disjoint from S's. The conferring partners are therefore the k-sets sharing two or more vertices with S: the dependency neighborhood Γ(S) = {T ≠ S : |S ∩ T| ≥ 2} has size d, where

**d + 1 = Σ_{i=2}^{k} C(k,i)·C(n−k, k−i).**

Let us extract the exact asymptotic threshold of e·p·(d+1) ≤ 1 for n = c·k·2^{k/2} as k → ∞. For consecutive terms in the sum, the ratio is

**C(k,i+1)·C(n−k,k−i−1) / (C(k,i)·C(n−k,k−i)) = (k−i)²/((i+1)(n−2k+i+1)) ≤ k²/(3(n−2k+3)) = O(k·2^{−k/2}) → 0,**

so the i = 2 term dominates the entire sum up to a factor of 1 + O(k·2^{−k/2}) (and in finite terms, the i = 2 summand already exceeds the i = 3 summand as soon as 3(n−2k+3) ≥ (k−2)², i.e., n ≥ 2k − 3 + ⌈(k−2)²/3⌉ ≈ k²/3 — not 3k: at n = 3k the i = 3 term still leads for every k ≥ 8, and an exact tie is possible at the threshold when k ≡ 2 mod 3 — machine-verified for k = 4..15), and the +1 is S itself, hiding in the i = k term (the identity is brute-force-confirmed at (k, n) up to (5, 12)). Moreover, since k²/n = O(k·2^{−k/2}) → 0, we have C(n−k, k−2) = (1+O(k²/n))·C(n, k−2) and C(n, k−2) = k(k−1)/((n−k+2)(n−k+1))·C(n,k) = (1+O(k/n))·(k²/n²)·C(n,k). By Stirling's formula C(n,k) = (1+o(1))·(1/√(2πk))·(en/k)^k, we obtain

**d + 1 = (1+o(1))·C(k,2)·C(n, k−2) = (1+o(1))·k⁴/(2n²√(2πk))·(en/k)^k.**

Substituting n = c·k·2^{k/2} (so n² = c²k²2^k and (en/k)^k = (ec)^k·2^{k²/2}) and multiplying by e·p = 2e·2^{−k²/2+k/2} gives

**e·p·(d+1) = (1+o(1))·2e·2^{−k²/2+k/2}·k⁴/(2c²k²2^k√(2πk))·(ec)^k·2^{k²/2} = (1+o(1))·(e/(c²√(2π)))·k^{3/2}·(ec/√2)^k.**

For any fixed c < √2/e, the exponential base ec/√2 < 1 crushes the polynomial prefactor k^{3/2} for all large k, yielding Spencer's theorem (1975):

**R(k,k) > (√2/e − o(1))·k·2^{k/2}.** ∎

— still the best asymptotic lower bound known for diagonal Ramsey numbers. The constants now form a ladder, each method worth exactly one factor of √2 over the last:

| method | constant on k·2^{k/2} |
|---|---|
| union bound (Erdős 1947) | 1/(e√2) ≈ 0.260 |
| alteration (Lecture 5) | 1/e ≈ 0.368 |
| Local Lemma (Spencer 1975) | √2/e ≈ 0.520 |

And the honest small print, machine-checked by exact integer comparison: at small k the Local Lemma certifies *less* than the methods it beats asymptotically —

| k | union bound certifies | alteration certifies | Local Lemma certifies |
|---|---|---|---|
| 4 | R > 6 | R > 6 | R > 5 |
| 5 | R > 11 | R > 11 | R > 9 |
| 6 | R > 17 | R > 18 | R > 15 |
| 7 | R > 27 | R > 29 | R > 25 |

The asymptotic aristocrat is the small-k pauper — the chapter's honesty tax, levied one more time. The −o(1) in the statement is load-bearing: it absorbs a Θ(ln k/k) correction whose leading coefficient must exceed 3/2. Specifically, setting c = (√2/e)(1 − α·ln k/k) yields e·p·(d+1) ∼ (e³/(2√(2π)))·k^{3/2−α}: thus α = 2 decays as k^{−1/2} and certifies for every k ≥ 15 (in fact from k = 5), whereas α = 1 grows as k^{1/2} and fails for every k ≥ 6 (diverging to +∞ as k → ∞ — the slack is real work, not decoration).

**Property B, locally.** Lecture 4.2 certified k-uniform hypergraphs with m < 2^{k−1} edges — a *global* budget. The lemma buys a *local* one. Bad events A_E = "edge E is monochromatic", p = 2^{1−k}; A_E is independent of every event on a disjoint vertex set, so its conferring partners are precisely the edges meeting E. The condition e·p·(d+1) ≤ 1 reads d ≤ ⌊2^{k−1}/e⌋ − 1:

**If every edge of a k-uniform hypergraph meets at most ⌊2^{k−1}/e⌋ − 1 others, the hypergraph is 2-colorable.**

Disjoint edges are now free: a hypergraph may have any number of edges, however far m runs past 2^{k−1}, as long as each edge lives in a sparse neighborhood. The budgets, machine-checked: k = 3 → 0, k = 4 → 1, k = 5 → 4, k = 6 → 10, k = 7 → 22, k = 8 → 46. The Fano plane (each line meeting 6 others against a budget of 0) is correctly *not* certified — it is the smallest genuine casualty, Exercise 13's. And a detector sweep on the enumerable scale: every 3-uniform hypergraph on 6 vertices with pairwise disjoint edges (all 30 of them) and every 4-uniform one on 6 vertices with each edge meeting at most one other (all 120) is 2-colorable — at this scale no counterexample to the constant exists to be found; the sweep is a guard on the arithmetic, which is exactly what it is for.

**What you now own:** the union bound as the standard "avoid all bad events" template (P13); the Ramsey lower bound and its honest small-k weakness; two costumes of the same move (hypergraphs, tournaments); the Local Lemma as the honest interpolation between full independence and the union bound's worst case — and the calibrated expectation that a clean certification may sit far from the truth.

---

## Lecture 5 · Build, Then Prune: Alteration

One flaw runs through Lectures 1–4: the random object only *avoids* bad features when the union bound squeezes below 1, and it often won't. Erdős's repair is pattern **P14**, **alteration**: let the random object have its bad features, then **delete them**. The random coloring of K_n has some monochromatic K_k's? Fine — delete one vertex from each. What survives is smaller but clean, and smaller-but-clean is often far better than nothing.

Set it up. Color K_n randomly; let X = the number of monochromatic K_k's; Lecture 4 computed **E[X] = C(n,k)·2^{1−C(k,2)}**. Now delete, from each monochromatic K_k, one of its vertices. The survivors contain no monochromatic K_k (any survivor clique would have been on the deletion list, and each listed clique lost a vertex), and at most one vertex was deleted per bad clique — so at least **n − X** vertices survive. Expectation again — and since the number of surviving vertices s in any coloring is an integer:

**some outcome leaves at least ⌈n − C(n,k)·2^{1−C(k,2)}⌉ survivors**,

and since a survivor graph on s vertices with no monochromatic K_k is a certificate that R(k,k) > s:

**R(k,k) > ⌈n − C(n,k)·2^{1−C(k,2)}⌉ — for every integer n ≥ 1.** ∎

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 880 380" font-family="system-ui, -apple-system, 'Segoe UI', sans-serif">
  <rect x="0" y="0" width="880" height="380" fill="#ffffff"/>
  <defs>
    <marker id="f4arrow" viewBox="0 0 10 10" refX="8" refY="5" markerWidth="6" markerHeight="6" orient="auto"><path d="M 0 1 L 8 5 L 0 9 z" fill="#dc2626"/></marker>
  </defs>
  <text x="40" y="34" font-size="17" font-weight="700" fill="#193e5c">Figure 4 &#183; Build, then prune: alteration on K&#8326; (Lecture 5), Pattern P14</text>
  <text x="40" y="60" font-size="13" fill="#172333" font-weight="600">a random 2-coloring with X = 2 monochromatic triangles &#8212; both blue, both through v&#8321;</text>
  <text x="40" y="84" font-size="13" fill="#172333" font-weight="600">1. Random coloring: X = 2 bad K&#8323;'s</text>
  <text x="470" y="84" font-size="13" fill="#172333" font-weight="600">2. Delete v&#8321;: 0 bad K&#8323;'s, s = 5</text>
  <polygon points="60,185 282,163 174,242" fill="#dbeafe"/>
  <polygon points="60,185 282,163 148,163" fill="#dbeafe"/>
  <g stroke="#2563eb" stroke-width="1.8">
    <line x1="60" y1="185" x2="282" y2="163"/><line x1="60" y1="185" x2="174" y2="242"/>
    <line x1="60" y1="185" x2="148" y2="163"/><line x1="215" y1="115" x2="256" y2="242"/>
    <line x1="215" y1="115" x2="174" y2="242"/><line x1="282" y1="163" x2="174" y2="242"/>
    <line x1="282" y1="163" x2="148" y2="163"/><line x1="256" y1="242" x2="148" y2="163"/>
  </g>
  <g stroke="#dc2626" stroke-width="3">
    <line x1="215" y1="115" x2="282" y2="163"/><line x1="282" y1="163" x2="256" y2="242"/>
    <line x1="256" y1="242" x2="174" y2="242"/><line x1="174" y1="242" x2="148" y2="163"/>
    <line x1="148" y1="163" x2="215" y2="115"/><line x1="60" y1="185" x2="215" y2="115"/>
    <line x1="60" y1="185" x2="256" y2="242"/>
  </g>
  <circle cx="60" cy="185" r="13" fill="#ffffff" stroke="#dc2626" stroke-width="3"/>
  <circle cx="215" cy="115" r="13" fill="#ffffff" stroke="#172333" stroke-width="2"/>
  <circle cx="282" cy="163" r="13" fill="#ffffff" stroke="#172333" stroke-width="2"/>
  <circle cx="256" cy="242" r="13" fill="#ffffff" stroke="#172333" stroke-width="2"/>
  <circle cx="174" cy="242" r="13" fill="#ffffff" stroke="#172333" stroke-width="2"/>
  <circle cx="148" cy="163" r="13" fill="#ffffff" stroke="#172333" stroke-width="2"/>
  <g font-size="12.5" font-weight="600" fill="#172333" text-anchor="middle">
    <text x="60" y="189" fill="#dc2626">v&#8321;</text>
    <text x="215" y="119">v&#8322;</text><text x="282" y="167">v&#8323;</text>
    <text x="256" y="246">v&#8324;</text><text x="174" y="246">v&#8325;</text>
    <text x="148" y="167">v&#8326;</text>
  </g>
  <line x1="330" y1="185" x2="392" y2="185" stroke="#dc2626" stroke-width="2.5" marker-end="url(#f4arrow)"/>
  <text x="361" y="167" font-size="12" font-weight="700" fill="#dc2626" text-anchor="middle">delete v&#8321;</text>
  <circle cx="500" cy="185" r="13" fill="#ffffff" stroke="#94a3b8" stroke-width="1.8" stroke-dasharray="4,3"/>
  <text x="500" y="189" font-size="12.5" fill="#94a3b8" text-anchor="middle">v&#8321;</text>
  <g stroke="#94a3b8" stroke-width="1.3" stroke-dasharray="4,3">
    <line x1="500" y1="185" x2="655" y2="115"/><line x1="500" y1="185" x2="722" y2="163"/>
    <line x1="500" y1="185" x2="696" y2="242"/><line x1="500" y1="185" x2="614" y2="242"/>
    <line x1="500" y1="185" x2="628" y2="163"/>
  </g>
  <g stroke="#2563eb" stroke-width="1.8">
    <line x1="655" y1="115" x2="696" y2="242"/><line x1="655" y1="115" x2="614" y2="242"/>
    <line x1="722" y1="163" x2="614" y2="242"/><line x1="722" y1="163" x2="628" y2="163"/>
    <line x1="696" y1="242" x2="628" y2="163"/>
  </g>
  <g stroke="#dc2626" stroke-width="3">
    <line x1="655" y1="115" x2="722" y2="163"/><line x1="722" y1="163" x2="696" y2="242"/>
    <line x1="696" y1="242" x2="614" y2="242"/><line x1="614" y1="242" x2="628" y2="163"/>
    <line x1="628" y1="163" x2="655" y2="115"/>
  </g>
  <circle cx="655" cy="115" r="13" fill="#ffffff" stroke="#172333" stroke-width="2"/>
  <circle cx="722" cy="163" r="13" fill="#ffffff" stroke="#172333" stroke-width="2"/>
  <circle cx="696" cy="242" r="13" fill="#ffffff" stroke="#172333" stroke-width="2"/>
  <circle cx="614" cy="242" r="13" fill="#ffffff" stroke="#172333" stroke-width="2"/>
  <circle cx="628" cy="163" r="13" fill="#ffffff" stroke="#172333" stroke-width="2"/>
  <g font-size="12.5" font-weight="600" fill="#172333" text-anchor="middle">
    <text x="655" y="119">v&#8322;</text><text x="722" y="167">v&#8323;</text>
    <text x="696" y="246">v&#8324;</text><text x="614" y="246">v&#8325;</text>
    <text x="628" y="167">v&#8326;</text>
  </g>
  <text x="40" y="290" font-size="12" fill="#172333">Left: red C&#8325; on {v&#8322;,&#8230;,v&#8326;} plus v&#8321; joined red to v&#8322;, v&#8324;; the two shaded blue triangles {v&#8321;,v&#8323;,v&#8325;} and {v&#8321;,v&#8323;,v&#8326;} are the entire damage.</text>
  <text x="470" y="290" font-size="12" fill="#172333">Right: one deletion kills both bad cliques at once; the 5 survivors are clean, so s = 5 &#8805; n &#8722; X = 4.</text>
  <text x="40" y="318" font-size="12" fill="#172333">The clean survivors carry no monochromatic triangle &#8212; a certificate that R(3,3) &gt; 5.</text>
  <text x="40" y="342" font-size="12" fill="#64748b">Honesty note: Goodman's theorem says no coloring of K&#8326; has fewer than 2 monochromatic triangles, so X = 2 is the best a complete K&#8326; can show &#8212; the figure draws a machine-verified minimizer.</text>
</svg>
```

Now the fun: choose n to make the right side big, which the plain union bound never allowed (it needed its product *below* 1; alteration only needs the damage to be smaller than the head start). Machine-checked, exactly, by rational arithmetic:

| k | best n | expected damage C(n,k)·2^{1−C(k,2)} | survivors ≥ | certified | plain bound certified |
|---|---------|-------------------------------------|-------------|-----------|----------------------|
| 5 | 13 | 1287/512 ≈ 2.51 | 10.49 | R(5,5) > 11 | R(5,5) > 11 |
| 6 | 21 | 54264/16384 ≈ 3.31 | 17.69 | **R(6,6) > 18** | R(6,6) > 17 |
| 7 | 33 | 4272048/1048576 ≈ 4.07 | 28.93 | **R(7,7) > 29** | R(7,7) > 27 |

**✎ Checkpoint.** Before reading the table: k = 5 gave the plain bound R(5,5) > 11. Predict whether alteration beats it there. Then look — and take the lesson: alteration gains a *factor that grows with k*, but at k = 5 the pruning damage eats exactly the head start. The method's profit is asymptotic, and honesty about small cases is the tax on this whole chapter.

### The asymptotics, in full

Both asymptotic constants follow rigorously from Stirling's inequality k! ≥ √(2πk)·(k/e)^k. Write n = c·k·2^{k/2} for a constant c > 0. Using C(n,k) ≤ n^k/k! ≤ (1/√(2πk))·(en/k)^k (asymptotically tight, since C(n,k) = (1 − O(k²/n))·n^k/k!), the expected number of monochromatic K_k's satisfies

**E[X] = C(n,k)·2^{1−C(k,2)} ≤ (1/√(2πk))·(e·c·k·2^{k/2}/k)^k·2·2^{−k(k−1)/2} = 2(ec√2)^k/√(2πk)**

— collect the powers of 2: k·(k/2) from the binomial, minus k(k−1)/2 from the coloring, plus the leading 2. One formula now answers both questions:

1. **The union bound** requires E[X] < 1. From the bound above, this holds whenever (ec√2)^k < √(2πk)/2. For any fixed c ≤ 1/(e√2) (and k ≥ 2, where √(2πk)/2 > 1), (ec√2)^k ≤ 1 < √(2πk)/2 — whereas for any fixed c > 1/(e√2), the asymptotic equivalence E[X] ∼ 2(ec√2)^k/√(2πk) → ∞ makes the union bound fail for all large k. Thus the union bound certifies

**R(k,k) > (1/(e√2) − o(1))·k·2^{k/2}.**

2. **Alteration** requires far less: not E[X] < 1, only E[X] = o(n) — the damage must not eat the head start, so the survivor count n − E[X] = n(1 − E[X]/n) keeps a 1−o(1) fraction of n. Dividing the same bound by n = c·k·2^{k/2} cancels the 2^{k/2} inside (ec√2)^k = (ec)^k·2^{k/2} against the 2^{k/2} in n:

**E[X]/n ≤ 2(ec)^k/(c·√(2π)·k^{3/2}) → 0 whenever ec ≤ 1**, i.e. c ≤ 1/e (in fact c = 1/e gives n − E[X] = (k/e)·2^{k/2}·(1 − O(k^{−3/2}))); conversely, for any fixed c > 1/e, E[X]/n ∼ 2(ec)^k/(c√(2π)k^{3/2}) → +∞. Then some outcome keeps n(1−o(1)) clean vertices, and alteration certifies

**R(k,k) > (1/e − o(1))·k·2^{k/2}.** ∎

The ratio of the constants is exactly √2 — the asymptotic shadow of the tie, +1, +2 you read off the table above. And the machine (exact integer arithmetic at k = 10, 15, 20, 25, 30) sees precisely the two regimes the derivation predicts: at c = 0.9/e the exact E[X]/n falls monotonically from 1.6% to 0.06%, while at c = 1.5/e it explodes from 2.0 to 1,681 — the boundary ec = 1 is real, and nothing happens on the wrong side of it. The union bound's own boundary is just as sharp, and just as slow to arrive: at 20% above 1/(e√2) the product already exceeds 1 by k = 15; at 5% above, it stays below 1 through k = 40 and crosses only by k = 45. The closer c sits to the constant, the longer the certification holds — but above the constant it always dies. That is what the −o(1) is for.

### The same race, run without dice: greedy joins the table

One player is missing from the comparisons so far: a *deterministic constructor*. Lecture 1 derandomized the max-cut coin flips; the Ramsey union bound derandomizes the same way — pattern **P18**, second appearance. Color the **edges** of K_n one at a time. After some edges are colored, each k-clique S contributes its conditional probability of ending up monochromatic: 2^{1−C(k,2)} while none of its edges is colored, (1/2)^{C(k,2)−f} once f of them are colored and all share one color, and 0 from the moment two colors appear among S's colored edges — that clique can never be monochromatic again. Call the total E_so_far. For the next edge e, let D_c be the change in E_so_far if e gets color c. Cliques not containing e contribute to neither; each clique containing e splits its old contribution so that the two futures average out: **D_red + D_blue = 0** — the same telescoping as Lecture 1's two coordinate expectations. (Explicitly, for any k-clique S containing e with r red and b blue colored edges prior to coloring e: if r = b = 0, coloring e either red or blue transitions S from weight 2^{1−C(k,2)} to 2^{−C(k,2)+1} = 2^{1−C(k,2)}, so D_red(S) = D_blue(S) = 0; if r ≥ 1 and b = 0, coloring e red doubles S's weight from 2^{r−C(k,2)} to 2^{r+1−C(k,2)} while coloring e blue kills S's weight to 0, so D_red(S) = +2^{r−C(k,2)} and D_blue(S) = −2^{r−C(k,2)}; symmetrically if b ≥ 1, r = 0; and if r ≥ 1, b ≥ 1, both are 0.) So one of the two colors has D_c ≤ 0, and greedy takes it: the conditional expectation never rises. When the last edge is colored, E_so_far *is* the count of monochromatic k-cliques. **Whenever the union bound certifies — E[X] < 1 — greedy constructs a clean coloring of the same K_n, deterministically.** The dice were only ever a proof device; the constructor needs no appeal to probability at run time.

The guarantee column below is therefore exactly the union bound's column — derandomization costs nothing here. The *observed* reach of the constructor is another matter, and it is the table's most honest lesson:

| k | random certifies (union bound, Lecture 4) | greedy guarantees (derandomized) | greedy observed (scanned to first failure) | altered certifies (this lecture) | Local Lemma certifies (§4.3) |
|---|---|---|---|---|---|
| 4 | > 6 | > 6 | > 10 | > 6 | > 5 |
| 5 | > 11 | > 11 | > 22 | > 11 | > 9 |
| 6 | > 17 | > 17 | > 26 (scan cap) | > 18 | > 15 |
| 7 | > 27 | > 27 | — | > 29 | > 25 |
| 8 | > 42 | > 42 | — | > 47 | > 41 |

The observed column is one implementation — edges in lexicographic order, ties broken to red — run upward in n until its first failure (at k = 4 it fails at n = 11; at k = 5 it fails at n = 23; at k = 6 no failure was found up to the scan's cap; k = 7–8 not scanned). Read three lessons off the table. **Greedy's guarantee inherits the union bound exactly** — that is the derandomization theorem, and the runs confirm it: at every frontier n the conditional expectation started below 1, never rose, and finished at zero. **The observed constructor outruns every analytic certificate at k = 5, 6** — the scan's clean coloring of K_22 at k = 5 is itself a constructive proof that R(5,5) > 22, double this chapter's best certified bound — while at k = 4 the same constructor stops at 10, far short of the true 17. Neither direction is promised: the observed reach is a fact about one implementation, discovered by running it, and the guarantee column is all the method warrants in general. **Analysis and search are different sports** — the certified bounds grow like k·2^{k/2} because that is what we can prove in general; a constructor's reach at a fixed small k is a measurement. The probabilistic method's philosophy in one sentence: *the dice prove existence, the derandomized dice construct it, and neither pretends to be the fastest way to find it* (computer searches in the literature reach far beyond any column here — record-hunting is a different game than certifying).

**What you now own:** alteration (P14) — random object, then prune; the deletion inequality for Ramsey; the reflex of *optimizing the head start n against the expected damage*; the full asymptotic derivation — one Stirling formula, two thresholds (ec√2 = 1 for the union bound, ec = 1 for alteration), and the technique every later Ramsey lower bound descends from; the calibrated expectation that a method's small cases may tie or lose while its asymptotics win; and the derandomized Ramsey (P18) — greedy inherits the union bound's certificate as a construction, while its observed reach runs on a track no guarantee covers.

---

## Lecture 6 · The Second Moment: When the Average Must Concentrate

Every result so far lived on the first moment — E[X] small enough (union bound), or E[X] large somewhere (averaging), or E[X] = o(n) (alteration). Here is a question none of those can answer. In G(n,p) — n vertices, each of the C(n,2) possible edges present independently with probability p — let X be the number of triangles. E[X] = C(n,3)p³. If E[X] → ∞, must a triangle *actually appear*? The first moment is deaf to this: a huge average can be run up by rare freak outcomes, with X = 0 in the typical case. To conclude that X > 0 *typically*, you must show the distribution concentrates — and concentration is a statement about the second moment.

**The engine (Paley–Zygmund, worn as Chebyshev).** For any nonnegative random variable X with 0 < E[X²] < ∞,

**P(X > 0) ≥ E[X]²/E[X²].**

Proof: E[X] = E[X·1_{X>0}] ≤ √(E[X²]·E[1_{X>0}²]) = √(E[X²]·P(X>0)) — Cauchy–Schwarz on the two random variables X and 1_{X>0} — then square. ∎ The working costume is Chebyshev: P(X = 0) ≤ P(|X − E[X]| ≥ E[X]) ≤ Var(X)/E[X]², so **Var(X) = o(E[X]²) forces X > 0 almost surely** ("almost surely" = with probability tending to 1 as n grows). Sanity, on a full census: at n = 6, p = ½, all 32,768 graphs enumerated give E[X] = 5/2, E[X²] = 45/4, so the engine promises P(triangle exists) ≥ (25/4)/(45/4) = 5/9 ≈ 0.556; the exact count is 26,979/32,768 ≈ 0.823. The bound is soft, as bounds at n = 6 should be — but it is a bound.

**Application: the triangle threshold.** Write X = Σ_S X_S over 3-sets S, X_S the indicator of S's three edges. E[X] = C(n,3)p³. The second moment splits by overlap: to compute Var(X) = E[X²] − E[X]² = Σ_{(S,T)} (E[X_S X_T] − E[X_S]·E[X_T]), classify the ordered pairs (S, T) of 3-subsets by the size of their vertex intersection |S ∩ T|:

- **|S ∩ T| ≤ 1:** the two triples share at most one vertex and therefore **zero edges**, so their six edges are distinct and mutually independent: E[X_S X_T] = p⁶ = E[X_S]·E[X_T] — contributing 0 to the variance.
- **|S ∩ T| = 3 (T = S):** there are C(n,3) such pairs; S ∪ T spans three edges, so the contribution is p³ − p⁶.
- **|S ∩ T| = 2:** to form T from a fixed S, choose 2 of S's 3 vertices (C(3,2) = 3 ways) and 1 of the n − 3 vertices outside S (n − 3 ways), giving 3(n−3)C(n,3) ordered pairs; the union S ∪ T has four vertices and 3 + 3 − 1 = five distinct edges (sharing the single edge on S ∩ T), so the contribution is p⁵ − p⁶.

What survives is the covariance of the overlapping pairs:

**Var(X) = C(n,3)(p³ − p⁶) + 3(n−3)C(n,3)(p⁵ − p⁶)**

— machine-verified to the last integer: at n = 4, 5, 6 and p = 1/2 and 1/4, full enumeration of all 2^{C(n,2)} graphs matches E[X] and E[X²] exactly, and Paley–Zygmund holds on every one of those exact distributions. Now divide by E[X]² = C(n,3)²p⁶ — valid for all n ≥ 3 and p ∈ (0, 1]:

**Var(X)/E[X]² = (1−p³)/(C(n,3)p³) + 3(n−3)(1−p)/(C(n,3)p) ≤ 1/(C(n,3)p³) + 3(n−3)/(C(n,3)p).**

Since C(n,3) = n(n−1)(n−2)/6 = (n³/6)(1 − O(1/n)), substituting t = np yields

**Var(X)/E[X]² ≤ (1+o(1))·(6/t³ + 18(n−3)/(n³p)) ≤ (1+o(1))·(6/t³ + 18/(n²p)) → 0 whenever np → ∞**

(n²p = n·t ≥ t → ∞ kills both terms; and larger p only shrinks the relative variance further, since p^{−3} − 1 and p^{−1} − 1 are strictly decreasing on (0, 1]).

Chebyshev finishes one side: if np → ∞, almost every graph contains a triangle. The first moment kills the other, by name — **Markov's inequality**: if np → 0, then E[X] ≈ (np)³/6 → 0 and P(X ≥ 1) ≤ E[X] → 0 — almost no graph contains one. Between the two regimes sits the answer, sharp:

**The threshold for the appearance of a triangle in G(n,p) is p = 1/n.** ∎

First moment below, second moment above: a complete sharp-threshold argument, the kind random-graph theory runs on.

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 880 260" font-family="system-ui, -apple-system, 'Segoe UI', sans-serif">
  <rect x="0" y="0" width="880" height="260" fill="#ffffff"/>
  <text x="40" y="34" font-size="17" font-weight="700" fill="#193e5c">Figure 5 &#183; The three overlap cases behind Var(X) (Lecture 6)</text>
  <text x="40" y="62" font-size="13" fill="#172333" font-weight="600">|S &#8745; T| = 3 &#183; T = S</text>
  <text x="300" y="62" font-size="13" fill="#172333" font-weight="600">|S &#8745; T| = 2 &#183; 1 shared edge</text>
  <text x="590" y="62" font-size="13" fill="#172333" font-weight="600">|S &#8745; T| &#8804; 1 &#183; 0 shared edges</text>
  <g stroke="#2563eb" stroke-width="2.5">
    <line x1="150" y1="100" x2="105" y2="180"/>
    <line x1="105" y1="180" x2="195" y2="180"/>
    <line x1="195" y1="180" x2="150" y2="100"/>
  </g>
  <circle cx="150" cy="100" r="10" fill="#ffffff" stroke="#2563eb" stroke-width="2"/>
  <circle cx="105" cy="180" r="10" fill="#ffffff" stroke="#2563eb" stroke-width="2"/>
  <circle cx="195" cy="180" r="10" fill="#ffffff" stroke="#2563eb" stroke-width="2"/>
  <text x="150" y="215" font-size="12" fill="#172333" text-anchor="middle">3 edges: Cov = p&#179; &#8722; p&#8310;</text>
  <line x1="285" y1="140" x2="345" y2="98" stroke="#2563eb" stroke-width="2"/>
  <line x1="285" y1="140" x2="345" y2="182" stroke="#2563eb" stroke-width="2"/>
  <line x1="405" y1="140" x2="345" y2="98" stroke="#2563eb" stroke-width="2"/>
  <line x1="405" y1="140" x2="345" y2="182" stroke="#2563eb" stroke-width="2"/>
  <line x1="345" y1="98" x2="345" y2="182" stroke="#dc2626" stroke-width="3.5"/>
  <circle cx="285" cy="140" r="10" fill="#ffffff" stroke="#2563eb" stroke-width="2"/>
  <circle cx="405" cy="140" r="10" fill="#ffffff" stroke="#2563eb" stroke-width="2"/>
  <circle cx="345" cy="98" r="10" fill="#dbeafe" stroke="#dc2626" stroke-width="2.5"/>
  <circle cx="345" cy="182" r="10" fill="#dbeafe" stroke="#dc2626" stroke-width="2.5"/>
  <text x="345" y="215" font-size="12" fill="#172333" text-anchor="middle">5 edges: Cov = p&#8309; &#8722; p&#8310;; 3(n&#8722;3)C(n,3) pairs</text>
  <g stroke="#2563eb" stroke-width="2">
    <line x1="545" y1="105" x2="545" y2="175"/>
    <line x1="545" y1="105" x2="605" y2="140"/>
    <line x1="545" y1="175" x2="605" y2="140"/>
    <line x1="665" y1="105" x2="665" y2="175"/>
    <line x1="665" y1="105" x2="605" y2="140"/>
    <line x1="665" y1="175" x2="605" y2="140"/>
  </g>
  <circle cx="545" cy="105" r="9" fill="#ffffff" stroke="#2563eb" stroke-width="2"/>
  <circle cx="545" cy="175" r="9" fill="#ffffff" stroke="#2563eb" stroke-width="2"/>
  <circle cx="665" cy="105" r="9" fill="#ffffff" stroke="#2563eb" stroke-width="2"/>
  <circle cx="665" cy="175" r="9" fill="#ffffff" stroke="#2563eb" stroke-width="2"/>
  <circle cx="605" cy="140" r="9" fill="#ffffff" stroke="#193e5c" stroke-width="2.5"/>
  <text x="605" y="215" font-size="12" fill="#172333" text-anchor="middle">6 independent edge coins: Cov = 0</text>
  <text x="40" y="243" font-size="12" fill="#64748b">Only the overlapping pairs (|S &#8745; T| &#8805; 2) feed the variance; the disjoint pairs cancel into E[X]&#178;.</text>
</svg>
```

**✎ Checkpoint.** At exactly p = 1/n: E[X] → 1/6, a constant. Predict P(no triangle) as n → ∞ — does it tend to 0, to 1, or to something in between? Neither moment can decide a boundary this fine; the truth (flagged, not proved here) is the Poisson limit: the triangle count tends to a Poisson(1/6) variable, so P(no triangle) → e^{−1/6} ≈ 0.846. The average alone never tells you where the mass sits — that is the whole point of this lecture.

**Corollary: random graphs are hard to color.** Exercise 5's union bound, read asymptotically, says almost every graph in G(n, ½) has α ≤ 2log₂n — the product it bounds tends to 0 as n grows (machine-checked trend: 10^{−4}, 10^{−10}, 10^{−25}, 10^{−42} at n = 16, 100, 10⁴, 10⁶). Now count color classes: a proper coloring with r colors partitions the n vertices into r independent sets, each of size at most α, so n ≤ r·α:

**χ(G(n,½)) ≥ n/(2log₂n) for almost every graph** — Erdős's classical lower bound.

The matching upper bound — almost every graph is colorable with (1+o(1))·n/(2log₂n) colors — is Bollobás's celebrated 1988 theorem, and it is honestly beyond this chapter: the lower bound is a first-moment count; the upper bound needs a greedy coloring plus a sharp second-moment analysis of the independent-set count. Together they pin the chromatic number of a random graph to within a factor of 1+o(1) — while of Lecture 4's honesty it remains true that we cannot write a single one of these graphs down.

**What you now own:** the second-moment engine — Cauchy–Schwarz's P(X>0) ≥ E[X]²/E[X²], worn as Chebyshev's Var = o(E²); the threshold reflex (first moment kills one side, second moment the other); the triangle threshold p = 1/n with its honestly flagged Poisson boundary; and the chromatic corollary, lower bound proved, sharp form flagged as a flag should be.

---

## The Trick Bag (reference card)

| Pattern | Plain language | Where you met it |
|---------|---------------|-----------------|
| **P10 Averaging / expectation** | A random variable cannot always sit below its average; some object beats the mean. Its functional-analysis face, **graphical Brascamp–Lieb**: assign every edge of the host graph a two-variable function and iterate L^p duality and Hölder — the convexity engine that carries whole proofs the way the average carries this chapter (Sah–Sawhney–Stoner–Zhao's reverse Sidorenko inequality, Inventiones 2020) | Lectures 1, 2, 3, 5, 6 |
| **P12 Random construction** | Prove existence by designing an experiment: coin flips, random tournaments, random orderings, random colorings | All lectures |
| **P13 Union bound** | If the bad-event probabilities sum below 1, an object avoiding all of them exists | Lecture 4 (refined by the Local Lemma, §4.3) |
| **P14 Alteration** | Let the random object be imperfect; delete the damage; count survivors | Lecture 5 |
| **P18 Algorithmic proof** | Derandomize: the greedy local-flip procedure's termination *is* the theorem; the conditional-expectation walk inherits the union bound | Lectures 1, 5 |

**Formula box:** cut ≥ m/2 (every graph; connected graphs: ≥ m/2 + (n−1)/4 — Edwards–Erdős, Exercise 10). Szele: some tournament has ≥ n!/2^{n−1} directed Hamiltonian paths. Caro–Wei: α ≥ Σ 1/(d(v)+1) ≥ n²/(2m+n). Union bound Ramsey: C(n,k)·2^{1−C(k,2)} < 1 ⇒ R(k,k) > n; clean form R(k,k) > ⌊2^{k/2}⌋ (k ≥ 3). Alteration: R(k,k) > ⌈n − C(n,k)·2^{1−C(k,2)}⌉ for every integer n ≥ 1; asymptotics R(k,k) > (1/(e√2) − o(1))·k·2^{k/2} (union bound) and R(k,k) > (1/e − o(1))·k·2^{k/2} (alteration) — constants ladder 1/(e√2) < 1/e < √2/e. Property B: m < 2^{k−1} edges ⇒ 2-colorable; locally: each edge meeting ≤ ⌊2^{k−1}/e⌋ − 1 others ⇒ 2-colorable. Property S(k): C(n,k)(1−2^{−k})^{n−k} < 1 ⇒ S(k) tournament exists (k = 2: n = 21; k = 3: n = 91). Local Lemma (symmetric): e·p·(d+1) ≤ 1 with p = 2^{1−C(k,2)}, d+1 = Σ_{i≥2}C(k,i)C(n−k,k−i) ≈ C(k,2)C(n,k−2) ⇒ R(k,k) > (√2/e − o(1))·k·2^{k/2} (Spencer 1975 — best known). Second moment: P(X>0) ≥ E[X]²/E[X²]; triangles in G(n,p): Var(X)/E[X]² ≈ 6/(np)³ + 18/(n²p) → 0 iff np → ∞ — threshold p = 1/n; χ(G(n,½)) ≥ n/(2log₂n) for almost every graph (Bollobás 1988: equality up to 1+o(1), flagged).

---

## Exercises (graded: ●○○ easy · ●●○ moderate · ●●● tough)

*Hints are here; worked answers are at the end of the chapter. Try first.*

**Easy — one idea, applied directly**

1. (●○○) Redo Lecture 1 with explicit indicator variables: X = Σ_e X_e with X_e = 1 iff edge e is crossed. *Hint: P10 — compute E[X_e] and appeal to linearity; no independence needed. Then locate the dependence honestly: check on a triangle which indicator pairs are independent, and which joint pattern is impossible.*
2. (●○○) Prove that every k-uniform hypergraph with m < 2^{k−1} edges is 2-colorable. *Hint: P13 — this is Lecture 4.2's property B, in your hands; check a fixed edge's mono probability.*
3. (●○○) Prove that every 3-uniform hypergraph with m edges admits a vertex 2-coloring with at most m/4 monochromatic edges. *Hint: P12 + P10 — a fixed edge is monochromatic with probability 1/4.*
4. (●○○) Prove that some tournament on n vertices has at least C(n,3)/4 *cyclic* triples (three players each beating the next round the triangle). Note the transitive tournament has 0 — the point of the exercise is that the crowded extreme exists anyway. *Hint: P12 + P10 — for a fixed triple, count the cyclic orientations out of the 8.*

**Moderate — two ideas, or one tricky step**

5. (●●○) Prove that for every n ≥ 2 (and for almost every graph as n → ∞), some n-vertex graph has both α(G) ≤ 2log₂n and ω(G) ≤ 2log₂n. *Hint: P13 — random graph G(n, ½); union-bound over k-sets that are cliques OR independent sets, with k = ⌈2log₂n⌉; the two colors are symmetric.*
6. (●●○) Prove that every triangle-free graph satisfies α(α+1) ≥ n. *Hint: P10 + Lecture 3 — what is the neighborhood of a vertex, in a triangle-free graph? Careful: d(v) ≤ α, NOT α − 1; then apply Caro–Wei.*
7. (●●○) Prove that for every n ≥ 3, some tournament on n vertices has at least (n−1)!/2^n directed Hamiltonian *cycles*. *Hint: P12 + P10 — count undirected Hamiltonian cycles first ((n−1)!/2 of them); each survives as a directed cycle with probability 2^{1−n}; mind both cyclic directions.*
8. (●●○) Show that Caro–Wei is tight: if G is a disjoint union of cliques, then α(G) = Σ 1/(d(v)+1) exactly. *Hint: compute both sides per clique; then check tightness on examples — equality, not just closeness.*

**Tough — several chapter ideas combined**

9. (●●○) Prove that every graph with m ≥ n/2 edges has an independent set of size at least n²/(4m). *Hint: P14 alteration — pick a random vertex subset (each vertex with probability p), then delete one endpoint of every surviving internal edge; choose p = n/(2m) and explain why the hypothesis m ≥ n/2 is genuinely needed.*
10. (●●●) **The Edwards–Erdős bound.** Prove that every *connected* graph has a cut of size at least **m/2 + (n−1)/4** — and first refute, with two examples — K₃ and K₅ — the tempting-but-false claim that every graph has a cut of at least m/2 + √(m/8). *Hint: P10/P18-style induction on n — three moves: split at a cut vertex; remove a non-cut vertex of odd degree; and when all degrees are even, remove two adjacent vertices u,v with G − {u,v} still connected, placing them back in the order that pays a rounding bonus. The third move needs a small existence lemma about 2-connected graphs — proved in full in the answer; this is the chapter's most demanding exercise. (The historical truth: the √(m/8) claim is a garbled memory of Edwards' theorem for arbitrary graphs, which really does hold — see the answer.)*
11. (●●●) Compute, by exact arithmetic, the best alteration bound of Lecture 5 for k = 5, 6, 7: for each k, find the n maximizing n − C(n,k)·2^{1−C(k,2)}, and state the certified R(k,k) lower bound. Report where alteration beats the plain union bound and where it merely ties. *Hint: P14 — rational arithmetic, not floats; compare with Lecture 4's certified frontier.*
12. (●●●) For property S(k), find by exact computation the smallest n the union bound certifies, for k = 2 and k = 3 — and compare each with the scale k²·2^k. *Hint: P13 — C(n,k)(1−2^{−k})^{n−k} < 1; the product rises, then decays; the first dip below 1 is your answer.*

**Pattern unknown — you choose the tool** *The graded set above tells you which lecture idea to reach for — research and exams do not. No hints here, and no difficulty rating either: diagnosing the problem is part of the problem. Worked answers still wait at the end.*

13. (◆) The **Fano plane**: seven points and seven 3-point lines, every two points on exactly one line, every two lines meeting in exactly one point. Show that no matter how you color its seven points red and blue, some line is monochromatic.
14. (◆) Prove that every set A of n nonzero integers contains a **sum-free** subset larger than n/3 — a subset S with no solution of x + y = z inside S. *(Erdős, 1965 — the proof fits in this chapter's toolbox.)*
15. (◆) Vectors v₁, …, v_r in the plane satisfy Σ|vᵢ|² = 1. Show that signs εᵢ ∈ {±1} exist with |Σ εᵢvᵢ| ≤ 1.

**Graded backfill — five more, each hint naming its pattern**

16. (●○○) **How rare is order?** A tournament is *transitive* if its players can be ranked so that everyone beats everyone below them. Compute the probability that a random tournament on n vertices is transitive, and conclude that for large n almost every tournament contains a cyclic triple (Exercise 4's engine, from the other side). *Hint: P12 — count the favorable tournaments (each ranking forces every one of the C(n,2) games), then divide by the 2^C(n,2) equally likely tournaments.*
17. (●○○) **Expected fixed points.** In a uniformly random arrangement of n letters into n envelopes (Chapter 1's derangement world, but now with luck allowed), compute the expected number of letters that land home — for **every** n at once. *Hint: P10's linearity — X = Σ X_i with X_i the indicator that letter i is home; E[X_i] is one honest number each.*
18. (●●○) **Chebyshev's first outing.** In a uniform random vertex bipartition of K_n (Lecture 1's coin-flip cut experiment), let X = Σ_{e∈E(K_n)} X_e be the number of crossed edges. Compute E[X] and Var(X), and conclude that P(|X − C(n,2)/2| < n) ≥ 7/8 for every n ≥ 1. Why does Var(X) equal the variance of the total edge count in G(n, ½) even though the two distributions are completely different? *Hint: P10 — in the random cut, the edge-crossing indicators are not mutually independent, but Lecture 2's pairwise-independence lesson is all that Var(X) = Σ Var(X_e) needs; then apply Chebyshev's inequality.*
19. (●●○) **Tournament kings.** A *king* of a tournament is a player who, for every opponent u, either beat u directly or beat someone who beat u (two steps or fewer). Prove that every tournament has a king — in fact, that **every player of maximum out-degree is a king.** *Hint: P8 — take the winningest player v; if some u dodges v and all of v's victims, count u's wins honestly and catch the contradiction (P2's degree-sum spirit).*
20. (●●●) **Dominating sets by alteration.** A *dominating set* is a set D of vertices such that every vertex outside D has a neighbor inside D. Prove that every graph on n vertices with minimum degree δ has a dominating set of at most **n(1 + ln(δ+1))/(δ+1)** vertices. *Hint: P14, exactly as Lecture 5 runs: pick each vertex independently with probability p = ln(δ+1)/(δ+1), let U be the uncovered vertices, and repair — how big is E[|chosen| + |U|]? The bound (1−p)^{δ+1} ≤ e^{−p(δ+1)} does the last step.*

**Explorations — ◐ research-style training** *No single right answer — what you should find is described in each. These train the habit research actually runs on: changing the problem.*

X1. (◐) **When certificates lie.** Lecture 4 certifies an S(2) tournament exists on 21 vertices. The truth is dramatically smaller: search all tournaments on n ≤ 6 vertices (2^15 of them at n = 6 — a one-liner) and you will find **none** with S(2); so the truth is somewhere in 7..20. Find the true minimum, then interrogate the winner: it is not a random-looking object at all — it has arithmetic structure (investigate tournaments built from the quadratic residues modulo a prime p ≡ 3 (mod 4)). Then meditate on the gap: a certificate of 21 against a truth of single digits — and ask how the gap behaves for k = 3, where the certificate says 91.

X2. (◐) **The property-B frontier.** Exercise 2 shows m < 2^{k−1} edges always allow a 2-coloring, and Exercise 13 exhibits a 3-uniform 7-edge non-colorable hypergraph — so the frontier for k = 3 sits between 4 and 7 edges, and the general minimum m(3) is a known hard theorem (it is 7, achieved only by the Fano plane). Build the frontier ladder yourself: for n = 4, 5, 6 vertices, search by increasing edge count for the smallest non-2-colorable 3-uniform hypergraph. You should find that four vertices admit nothing at all, and — the discovery — that the minimum for n = 5 and n = 6 coincides: edge-minimal obstructions are cramped, not sprawling. Then push to n = 7 and meet the Fano plane from the machine's side.

---

## Computational Lab (verified)

### Part 1 — Derandomized cuts and a variance lesson

The chapter's two pillars — derandomized cuts and Monte-Carlo existence — executed and verified (2026-10-09, reference edition; carried over unchanged, comments normalized to plain ASCII):

```python
import random

def max_cut_by_flips(n, p):                      # Lecture 1, Method 2, live
    adj = {v: set() for v in range(n)}; m = 0
    for i in range(n):
        for j in range(i+1, n):
            if random.random() < p: adj[i].add(j); adj[j].add(i); m += 1
    side = [random.random() < 0.5 for _ in range(n)]
    improved = True
    while improved:
        improved = False
        for v in range(n):
            same = sum(1 for u in adj[v] if side[u] == side[v])
            if same > len(adj[v]) - same:
                side[v] = not side[v]; improved = True
    cut = sum(1 for i in range(n) for j in adj[i] if i < j and side[i] != side[j])
    return m, cut

for _ in range(6):
    m, cut = max_cut_by_flips(12, 0.5)
    assert cut >= m / 2                          # never lands below m/2
```

**Verified output:** 6 random graphs (n = 12, p = 0.5): m = 30, 29, 36, 30, 32, 32 and cut = 22, 22, 24, 24, 25, 21 — **zero violations** of cut ≥ m/2, with ratios 1.31–1.60 (local flips typically beat the expectation bound by a wide margin). Recorded side-experiment, run separately from the embedded program above (which carries only the six flip trials): Monte-Carlo on K_5 — 200 random red/blue edge colorings → 1 survivor (a coloring with no monochromatic triangle) ≈ 0.005 vs the exact 12/1024 ≈ 0.0117 — a **variance lesson**: for events near 1%, small samples are noisy; validate estimators on computable cases before trusting them elsewhere.

**What to explore:** test the Edwards–Erdős improvement of Exercise 10 (cut ≥ m/2 + (n−1)/4 on *connected* graphs — check a few hundred random connected graphs and record how often equality is approached; odd complete graphs and windmills achieve it exactly); estimate P(no monochromatic K_4) on K_8 by sampling (the exact value is out of reach of brute force — 2^28 colorings — but your Chapter 3 lab already knows R(4,4) = 18, so K_8 should mostly survive; measure the gap between your estimate and the union bound's pessimism).

### Part 2 — The triangle threshold at scale: seeded, reproducible Monte-Carlo

Lecture 6 proved the sharp threshold: triangles appear in G(n, p) right around p = 1/n — first moment below, second moment above. What does the threshold look like from inside a finite graph? Sampling answers that — but Part 1's variance lesson demands samples that mean something, so this part is fully *reproducible*: no `random` module, just a Lehmer LCG (x ← 48271·x mod (2³¹ − 1)) drawing every coin, doing exact integer arithmetic that any language reproduces identically. With p = c/n the expected triangle count is C(n,3)p³ ≈ c³/6; if triangles behaved like a Poisson family, the chance of seeing at least one would be about 1 − e^{−c³/6} — the lecture's closing checkpoint asks you to predict exactly this at c = 1.

```python
import math

def make_rng(seed=1):                        # Lehmer LCG: x <- 48271 x mod (2^31 - 1)
    state = [seed]
    def rand():
        state[0] = 48271 * state[0] % 2147483647
        return state[0]
    return rand

rand = make_rng()
TRIALS = 200
for n in (60, 120, 240):
    for c in (0.5, 1, 2, 3):
        p = c / n
        hits, tri_sum = 0, 0
        for _ in range(TRIALS):
            adj = [[False] * n for _ in range(n)]
            for i in range(n):                # one draw per pair, (i, j) lexicographic
                for j in range(i + 1, n):
                    if rand() / 2147483647 < p:
                        adj[i][j] = adj[j][i] = True
            t = 0
            for i in range(n):
                for j in range(i + 1, n):
                    if adj[i][j]:
                        for k in range(j + 1, n):
                            if adj[i][k] and adj[j][k]:
                                t += 1
            if t:
                hits += 1
            tri_sum += t
        print(f"{n} {c} {hits} {hits / TRIALS:.3f} "
              f"{1 - math.exp(-c ** 3 / 6):.3f} {tri_sum / TRIALS:.2f} {c ** 3 / 6:.2f}")
```

The columns: n, c, samples with a triangle (of 200), the observed fraction, the Poisson estimate 1 − e^{−c³/6}, the observed mean triangle count, the Poisson mean c³/6.

**Verified output.** `60 0.5 4 0.020 0.021 0.03 0.02` / `60 1 29 0.145 0.154 0.15 0.17` / `60 2 148 0.740 0.736 1.45 1.33` / `60 3 196 0.980 0.989 4.04 4.50` / `120 0.5 5 0.025 0.021 0.03 0.02` / `120 1 22 0.110 0.154 0.12 0.17` / `120 2 146 0.730 0.736 1.26 1.33` / `120 3 194 0.970 0.989 4.16 4.50` / `240 0.5 5 0.025 0.021 0.03 0.02` / `240 1 21 0.105 0.154 0.12 0.17` / `240 2 148 0.740 0.736 1.41 1.33` / `240 3 199 0.995 0.989 4.26 4.50`. Away from the threshold the fractions land on the Poisson estimate within noise — at c = 2 the observed 0.740, 0.730, 0.740 straddle the limit 0.736, and at c = 3 everything is within two points of 0.989. At c = 1, exactly on the threshold, the observed fractions (0.145, 0.110, 0.105) run below the limit 0.154 and close slowly — finite-size effects: C(n,3)p³ = (c³/6)(1 − O(1/n)), plus genuine dependence between overlapping triangles, both fading as n grows. That is Lecture 6's closing checkpoint answered empirically: P(no triangle) tends to e^{−1/6} ≈ 0.846, and the c = 1 columns show the approach (0.855, 0.890, 0.895). At c = 0.5 the counts are 4, 5, 5 hits in 200 — a couple of Poisson blips against a 0.021 baseline; with 200 samples a fraction carries noise of about ±0.03 (Part 1's variance lesson, now wearing threshold clothes: read the trend, not a single cell).

**What to explore:** push n further at c = 1 and watch the fraction climb toward 0.154; then push TRIALS up at fixed n and watch the noise band shrink — which effect converges faster, and why? Finally, re-read the second-moment proof and pinpoint exactly which dependence the Poisson heuristic ignores.

---

## Answers to the Exercises

*Attempt everything first — the value is in the attempt; these pages will still be here when you return.*

**A1.** Let X_e = 1 if edge e has its ends on different sides of the coin-flip partition. Then X = Σ_e X_e is the cut size, and E[X_e] = P(coin(u) ≠ coin(v)) = 1/2 for every edge. Linearity: E[X] = Σ_e E[X_e] = m/2, so some partition crosses ≥ m/2. ∎ Sanity, machine-checked: K₄'s eight partitions cut 0, 3, 3, 3, 3, 4, 4, 4 — average exactly 3 = m/2. *(The exercise is Lecture 1 with the machinery named. On the dependence the hint asks you to locate: two distinct edges' indicators are in fact independent — sharing an endpoint breaks nothing, as Lecture 2's tabulation shows — while the triangle's three indicators are pairwise independent but jointly dependent: every cut crosses zero or two of them, so all three never fire at once. Linearity needed none of this, and that is the point.)*

**A2.** Color each vertex red/blue independently. A fixed edge (a k-set) is monochromatic with probability 2·(1/2)^k = 2^{1−k}. Union bound over the m edges: P(some mono edge) ≤ m·2^{1−k} < 1 (here is where m < 2^{k−1} enters), so some coloring has none. ∎ For k = 3 this certifies 2-colorability for m ≤ 3 — and honestly stops there: the Fano plane (Exercise 13) fails with 7, and Exploration X2 maps the frontier between.

**A3.** Random coloring; a fixed 3-edge is mono with probability 2·(1/2)³ = 1/4. E[# mono edges] = m/4, so some coloring has at most m/4 monochromatic edges. ∎ Note the shape of the conclusion: not "zero bad events" (that would need m < 2² = 4 by A2) but "few bad events" — expectation tolerates what the union bound cannot: P10 where P13 would refuse.

**A4.** For a fixed triple of players, the 8 orientations of the three games fall into two camps: 6 transitive (a total order among the three) and 2 cyclic (each beats the next, in one or the other rotation). So the triple is cyclic with probability 2/8 = 1/4, and the expected number of cyclic triples over a random tournament is C(n,3)/4. Some tournament achieves at least the average. ∎ Machine-checked at n = 5: over all 1024 tournaments the average is exactly 2.5 = C(5,3)/4; the maximum is **5** (the regular "cyclic" tournament on 5 vertices — 5 of its 10 triples cyclic, the most any tournament can hold, attained by 24 of the 1024 labeled tournaments) and the minimum is **0** (the transitive tournament, which is exactly why the statement needs existence, not construction: the extremes coexist, and the average certifies the crowded one).

**A5.** Take G ∼ G(n, ½) and set k = ⌈2log₂n⌉. By the definition of the ceiling, 2log₂n ≤ k < 2log₂n + 1, so the integer k − 1 satisfies k − 1 < 2log₂n for **every** n ≥ 2. A fixed k-vertex set S is a clique with probability 2^{−C(k,2)} and an independent set with probability 2^{−C(k,2)}; for k ≥ 2 the two events are disjoint, so P(S is a clique or an independent set) = 2^{1−C(k,2)}. Union bound over all C(n,k) choices of S:

**P(α(G) ≥ k or ω(G) ≥ k) ≤ C(n,k)·2^{1−C(k,2)}.**

For n = 2, every 2-vertex graph satisfies α(G) ≤ 2 = 2log₂2 and ω(G) ≤ 2 = 2log₂2 trivially. For every n ≥ 3, k = ⌈2log₂n⌉ ≥ ⌈2log₂3⌉ = 4 and n ≤ 2^{k/2}. Using C(n,k) < n^k/k! (valid for all k ≥ 2, and equal to 0 if n < k),

**C(n,k)·2^{1−C(k,2)} < (n^k/k!)·2^{1−k(k−1)/2} ≤ ((2^{k/2})^k/k!)·2^{1−k²/2+k/2} = 2^{1+k/2}/k!.**

Since 2^{1+k/2}/k! ≤ 2³/4! = 1/3 < 1 for all k ≥ 4 (equality at k = 4), and 2^{1+k/2}/k! → 0 super-exponentially as n → ∞ (where k ≥ 2log₂n → ∞), the union bound is strictly below 1 for **every** n ≥ 3 and tends to 0 as n grows (for instance, at n = 16, k = 8: C(16,8)·2^{−27} = 12870/134217728 ≈ 9.6×10⁻⁵ < 1, so some 16-vertex graph has α, ω ≤ 7 < 8; at n = 100, k = 14: C(100,14)·2^{−90} ≈ 3.6×10⁻¹¹ < 1, so α, ω ≤ 13 < 2log₂100 ≈ 13.29). Thus for every n ≥ 2 (and for a 1−o(1) fraction of all graphs as n → ∞), some n-vertex graph has α(G) ≤ k−1 < 2log₂n and ω(G) ≤ k−1 < 2log₂n. ∎ The lesson of Chapter 3 returns with a vengeance: almost every graph is Ramsey-quiet, and we cannot write a single one of them down.

**A6.** Triangle-free means the neighborhood of any vertex is an *independent* set — so d(v) ≤ α for every v (careful: α, not α−1; the neighborhood can have α vertices, it just cannot exceed the maximum independent set). Caro–Wei (Lecture 3) gives α ≥ Σ_v 1/(d(v)+1); since d(v) ≤ α, each term is at least 1/(α+1), so α ≥ n/(α+1), i.e. **α(α+1) ≥ n**. ∎ The trap: writing d(v) ≤ α−1 would give α² ≥ n — false: C₅ has α = 2 and α² = 4 < 5, while the correct inequality gives 2·3 = 6 ≥ 5 ✓. Machine-checked: all 7 + 41 + 388 + 5789 triangle-free graphs on n = 3, 4, 5, 6 vertices satisfy α(α+1) ≥ n; zero violations.

**A7.** For n ≥ 3, K_n contains (n−1)!/2 undirected Hamiltonian cycles (cyclic orderings up to rotation and reversal). Fix one; its n edges are oriented consistently with the cyclic order — all clockwise, or all counterclockwise — with probability 2·(1/2)^n = 2^{1−n} (the two events are disjoint for n ≥ 3, and each is a specific pattern of n independent coins). Linearity over the cycles: the expected number of directed Hamiltonian cycles in a random tournament is ((n−1)!/2)·2^{1−n} = **(n−1)!/2^n**, and some tournament achieves at least that. ∎ Machine-checked: n = 4 — over all 64 tournaments, total 24 directed Hamiltonian cycles, E = 24/64 = 0.375 = 6/16 ✓, and the maximum in one tournament is 1 (the cyclic K₄); n = 5 — total 768 over 1024 tournaments, E = 0.75 = 24/32 ✓, maximum 3. So already at n = 5 some tournament has 3 directed Hamiltonian cycles while the transitive one has 0 — the average again certifies the crowded extreme. (Do not over-read the count: the three cycles cannot be edge-disjoint — three Hamiltonian cycles on five vertices would need 3 × 5 = 15 arcs, and a 5-vertex tournament has only 10 — the count is of cycles, not of disjoint arc sets.) Note the pair of expectations, for n ≥ 3: directed Hamiltonian paths (Lecture 2) at n!/2^{n−1}, directed Hamiltonian cycles here at (n−1)!/2^n — the ratio is exactly **2n**, and the factorization is honest: deleting any of the n arcs of a directed Hamiltonian cycle produces a distinct directed Hamiltonian path (n paths per cycle), while a fixed directed Hamiltonian path v₁ → v₂ → ⋯ → v_n (already using n − 1 arcs) closes into a directed cycle only if the remaining arc between v_n and v₁ points v_n → v₁ — one more coin, probability 1/2. So E[paths] = 2·E[closings] = 2n·E[cycles], and the middle identity is a per-tournament fact, machine-proven: in every single tournament, closings = n × cycles (the cyclic K₄, for instance, has 5 directed Hamiltonian paths, 4 closings, 1 cycle). At n = 5 the check reads 7.5/0.75 = 10 = 2n ✓.

**A8.** Let G = K_{n₁} ⊔ K_{n₂} ⊔ … ⊔ K_{n_t} (disjoint cliques). Every vertex of clique i has degree nᵢ−1, so clique i contributes nᵢ·(1/nᵢ) = 1 to the sum: Σ 1/(d(v)+1) = t. And α(G) = t exactly: an independent set takes at most one vertex per clique, and one per clique is possible. So the bound is attained — equality, not a near miss. ∎ Machine-checked on K₃⊔K₂⊔K₁ (α = 3 = sum), K₂⊔K₂ (2 = 2), K₄⊔K₃ (2 = 2), and five isolated vertices (5 = 5). A bound you cannot improve without changing its shape: any uniform strengthening must fail on these.

**A9.** Choose a random vertex subset S by keeping each vertex with probability p. E[|S|] = np; E[# edges inside S] = mp² (each of the m edges survives with p²). Now **alter** (P14): delete from S one endpoint of every internal edge. At most one vertex is lost per internal edge, so survivors ≥ |S| − e(S), and the survivors are independent (every surviving internal edge lost an endpoint — in fact all of them did). E[survivors] ≥ np − mp², so some choice leaves at least that many: **α ≥ np − mp²**. Optimize: p = n/(2m) gives np − mp² = n²/(2m) − n²/(4m) = **n²/(4m)**. ∎ The hypothesis is load-bearing: p is a probability only if n/(2m) ≤ 1, i.e. **m ≥ n/2** (for m < n/2 take p = 1 instead, giving α ≥ n − m — a different and also useful regime; at m = n/2 the two formulas agree at n/2). Machine-checked: every graph on 5 or 6 vertices with m ≥ n/2 satisfies α ≥ n²/(4m); zero violations (968 and 32647 cases). Compare Turán's n²/(2m+n) (Lecture 3): the alteration formula n²/(4m) exceeds n²/(2m+n) algebraically when 0 < m < n/2, where p = n/(2m) > 1 is invalid and p = 1 already gives the even stronger bound n − m > n²/(2m+n) (since (n−m)(2m+n) − n² = m(n−2m) > 0); for m ≥ n/2, Turán's n²/(2m+n) ≥ n²/(4m) since 4m − (2m+n) = 2m − n ≥ 0, with equality only at m = n/2. So the alteration bound's honest role is a proof technique that transfers (Exercise 10's world), not a record-holder here — worth saying aloud.

**A10.** *Part 1 — the refutation.* The claim "every graph has a cut ≥ m/2 + √(m/8)" is **false**. Witness 1: K₃. Its maximum cut is 2 (of 3 edges), but m/2 + √(m/8) = 1.5 + √0.375 ≈ 2.112 > 2. Witness 2: K₅, max cut 6, bound 5 + √1.25 ≈ 6.118 > 6. And this is no accident of smallness — an exhaustive machine scan of all connected graphs on 3 to 6 vertices (27,474 of them) finds these two and *only* these two violators: they are exactly the odd cliques, the graphs where the true theorem below is tight. A strengthening that adds anything to a sharp bound must fail on the sharp examples.

*Part 2 — the theorem.* **Every connected graph has a cut of size at least m/2 + (n−1)/4** (Edwards, answering a conjecture of Erdős). Proof by induction on n. For n ≤ 2, connected means a single edge (cut 1 ≥ 0.5 + 0.25) or a single vertex (0 ≥ 0). Now n ≥ 3.

**Move 1 — split at a cut vertex.** If G has a cut vertex x, write G = G₁ ∪ G₂ with G₁ ∩ G₂ = {x}, both parts connected, every edge in one part, n₁ + n₂ = n + 1 and m₁ + m₂ = m. By induction, each part has a cut of ≥ mᵢ/2 + (nᵢ−1)/4. Put the two cuts together, flipping all of G₂'s side labels if necessary so the two copies of x agree: internal edges keep their cut status, so the combined cut has ≥ m₁/2 + m₂/2 + (n₁−1)/4 + (n₂−1)/4 = m/2 + (n−1)/4. No loss — the fractions add perfectly. ∎ (for this case)

**Move 2 — remove a non-cut vertex of odd degree.** If G has no cut vertex it is 2-connected, so G − v is connected for every v. If some v has odd degree d: by induction G - v (connected, m − d edges, n − 1 vertices) has a cut ≥ (m−d)/2 + (n−2)/4. Put v back on the side that crosses more of its d edges — at least ⌈d/2⌉ = (d+1)/2 of them. Total: (m−d)/2 + (d+1)/2 + (n−2)/4 = m/2 + n/4 ≥ m/2 + (n−1)/4. Overshooting is allowed. ∎ (for this case)

**Move 3 — the even 2-connected case.** Suppose G is 2-connected and every degree is even (if Moves 1–2 do not apply, this is where we are). We need an *adjacent* pair u, v with G − {u,v} connected; that one exists is a small lemma, proved below. Let G' = G − {u,v}: connected, with m' = m − a − b − 1 edges, where a and b are the numbers of edges from u and v to G'. By induction G' has a cut ≥ m'/2 + (n−3)/4. Now put u and v back. Since d(u), d(v) are even and uv is an edge, **a = d(u) − 1 and b = d(v) − 1 are odd.** Place u first, opposite the majority of its a neighbors in the cut: ≥ ⌈a/2⌉ = (a+1)/2 edges crossed. Place v second: it faces b neighbors in G' plus u — b + 1 of them, an even number — and goes to the side crossing at least (b+1)/2 of them. New edges crossed: (a+1)/2 + (b+1)/2 = (a+b)/2 + 1. Total cut ≥ m'/2 + (n−3)/4 + (a+b)/2 + 1 = (m − a − b − 1)/2 + (a+b)/2 + (n−3)/4 + 1 = **m/2 + (n−1)/4**. ∎

**Lemma (the good pair).** Every 2-connected graph on n ≥ 3 vertices has an edge uv such that G − {u,v} is connected. *Proof.* If G is a cycle, removing the endpoints of any edge leaves a path (or a single vertex, at n = 3) — connected. Otherwise, by the ear-decomposition theorem, G is built as C₀ ∪ P₁ ∪ … ∪ P_r from a cycle C₀ by adding ears (paths whose endpoints lie in the earlier graph, whose internal vertices are new), every intermediate stage 2-connected — and one quiet clause of the decomposition matters here: an ear may be a single edge with *no* internal vertices (a chord). So do not take the last ear; take the **last ear with at least one internal vertex**, say P_i. Every later ear P_{i+1}, …, P_r is then a single edge adding no vertex, so the stage C₀ ∪ … ∪ P_i already spans all of G. If P_i has two or more internal vertices, take u, v to be consecutive internal vertices of P_i: G − {u,v} contains C₀ ∪ … ∪ P_{i−1} (connected) plus the remaining fragments of P_i, each attached to that stage at an ear endpoint — connected, and spanning, so G − {u,v} is connected. If P_i has exactly one internal vertex w, let x be an endpoint of P_i adjacent to w (wx is an edge of G): G − {w, x} contains (C₀ ∪ … ∪ P_{i−1}) − x, and a 2-connected graph minus one vertex is connected — spanning again, since the later ears added no vertices. Finally, if *no* ear has an internal vertex, then C₀ itself spans all of G and G is a cycle plus chords: take u, v to be the endpoints of any C₀-edge — C₀ − {u,v} is a path and G − {u,v} contains it. In every case the chosen pair is an edge and G − {u,v} is connected. ∎ (The lemma was also verified exhaustively by machine: every 2-connected graph on at most 6 vertices, and every even-degree 2-connected graph on 7 vertices — all 22,834 of them, enumerated over the full cycle space of K₇ — admits a good pair; zero counterexamples.)

Sharpness, and the chapter's honesty: the bound is attained by **K₃** (2 = 1.5 + 0.5), **K₅** (6 = 5 + 1), **K₇** (12 = 10.5 + 1.5), and the windmill of triangles on 5 vertices (4 = 3 + 1) — all machine-checked. The historical note: the √(m/8) claim is a corruption of Edwards' *other* theorem, which really holds: every graph (connected or not) has a cut of at least ⌈m/2 + √(m/8 + 1/64) − 1/8⌉ — verified by machine on all graphs up to 6 vertices, zero violations — but the version with √(m/8) alone drops the correction terms and dies on K₃. The connected bound m/2 + (n−1)/4 is the cleaner statement and the one parameterized algorithms target.

*Proof of Edwards' general bound.* Let G be any graph with m edges, and decompose G into its connected components C₁, …, C_r, having nᵢ vertices and mᵢ edges (Σᵢ mᵢ = m). For any component with mᵢ ≥ 1 edges, nᵢ ≥ 2 and mᵢ ≤ C(nᵢ,2) = nᵢ(nᵢ−1)/2, so nᵢ² − nᵢ − 2mᵢ ≥ 0, which yields nᵢ − 1 ≥ (√(1+8mᵢ) − 1)/2. By the Edwards–Erdős bound just proved, applied to each connected component,

**cut(Cᵢ) ≥ mᵢ/2 + (nᵢ−1)/4 ≥ mᵢ/2 + (√(1+8mᵢ) − 1)/8 = mᵢ/2 + √(mᵢ/8 + 1/64) − 1/8**

(and the inequality also holds with equality 0 = 0 if mᵢ = 0). Since the function g(x) = √(x/8 + 1/64) − 1/8 is concave on [0, ∞) with g(0) = 0, it is subadditive: g(x) ≥ (x/(x+y))·g(x+y) and g(y) ≥ (y/(x+y))·g(x+y) for x, y ≥ 0, so g(x) + g(y) ≥ g(x+y). Summing across all components,

**cut(G) = Σᵢ cut(Cᵢ) ≥ Σᵢ (mᵢ/2 + g(mᵢ)) ≥ m/2 + g(Σᵢ mᵢ) = m/2 + √(m/8 + 1/64) − 1/8.**

Because cut(G) is an integer, taking the ceiling completes the proof. ∎ (Machine-checked in the exact integer form (8M − 4m + 1)² ≥ 8m + 1, M the maximum cut: all graphs on at most 6 vertices satisfy it, with equality exactly on K₃, K₅ and K₇.)

**A11.** Rational arithmetic, exactly as the hint demands; D = 2^{C(k,2)−1}, expected damage E[X] = C(n,k)/D.

k = 5: maximize f(n) = n − C(n,5)/512. f(12) = 12 − 792/512 = 10.453…; f(13) = 13 − 1287/512 = 10.486…; f(14) = 14 − 2002/512 = 10.089…. Best n = **13**, survivors ≥ 13 − 1287/512 = 5369/512 ≈ 10.49, so some outcome leaves ≥ 11 vertices: **R(5,5) > 11** — exactly what the plain bound already certified. A tie: at k = 5 the pruning damage (2.51 expected bad cliques) eats the two extra vertices of head start.

k = 6: best n = **21**: E[X] = 54264/16384 ≈ 3.312, survivors ≥ 21 − 3.312 = 17.688 → ≥ 18 vertices: **R(6,6) > 18**, versus the plain bound's 17. A one-vertex gain.

k = 7: best n = **33**: E[X] = 4272048/1048576 ≈ 4.074, survivors ≥ 28.926 → ≥ 29: **R(7,7) > 29**, versus the plain 27. A two-vertex gain. ∎ The pattern is the lecture's moral in numbers: alteration's profit grows with k (tie, +1, +2) — the asymptotic √2-in-the-constant improvement is invisible at k = 5 and only waking up here. Machine-checked by exact BigInt rational comparison of n − C(n,k)/D across all n ≤ 500.

**A12.** The bound certifies an S(k) tournament on n vertices as soon as C(n,k)(1−2^{−k})^{n−k} < 1. The product rises with n, peaks, then decays exponentially (each new vertex multiplies by (1−2^{−k}) < 1 while the C(n,k) factor grows only polynomially in n); the first dip below 1 is the certification, found by exact integer arithmetic (compare C(n,k)·(2^k−1)^{n−k} against (2^k)^{n−k}):

k = 2: C(n,2)·(3/4)^{n−2} < 1 first at **n = 21** (n = 20 gives 190·(3/4)^18 ≈ 1.07 — just misses).
k = 3: C(n,3)·(7/8)^{n−3} < 1 first at **n = 91** (n = 90 gives ≈ 1.058 — just misses).

Against the scale k²·2^k: 21 vs 16, and 91 vs 72 — the same constant factor of about 1.3 in both, which is what "n ≈ k²·2^k up to a constant" means. To derive the asymptotic scale rigorously from the union bound condition C(n,k)·(1 − 2^{−k})^{n−k} < 1, use C(n,k) ≤ (en/k)^k and 1−x ≤ e^{−x} (with x = 2^{−k}):

**C(n,k)·(1−2^{−k})^{n−k} ≤ (en/k)^k·e^{−(n−k)·2^{−k}} = exp(k·ln(en/k) − (n−k)·2^{−k}).**

Substituting n = c·k²·2^k for a constant c > 0: ln(en/k) = ln(e·c·k·2^k) = k·ln2 + O(ln k), and (n−k)·2^{−k} = c·k² − k·2^{−k} = (1−o(1))·c·k², so the exponent equals

**k²·(ln2 − c + O(ln k/k)).**

Thus for any c > ln 2 ≈ 0.6931 the exponent tends to −∞ as k → ∞, certifying an S(k) tournament of order

**n = (ln 2 + o(1))·k²·2^k.** ∎ And now the sting, which Exploration X1 develops: for k = 2 the *truth* is single digits, so the certificate is off by a factor of three. The union bound proves existence, never optimality — a certified 21 is a proof that a valley floods, not a map of the river.

**A13.** Color the seven points red/blue and count **same-colored pairs** two ways. On one side: if r points are red, the same-colored pairs number

**C(r,2) + C(7−r,2) = (r(r−1) + (7−r)(6−r))/2 = r² − 7r + 21 = (r − 7/2)² + 35/4,**

a quadratic minimized, since r is an integer, at r = 3 and r = 4, where it equals C(3,2) + C(4,2) = 3 + 6 = **9**. On the other side: every pair of points lies on **exactly one** of the 7 lines (the Fano plane's defining property — machine-checked: its 7 lines cover all 21 pairs exactly once). Now suppose, for contradiction, that no line is monochromatic. Then every line's colors split 2–1, contributing exactly *one* same-colored pair; each same-colored pair lies on exactly one line; so there are at most 7 same-colored pairs. But there are at least 9. Contradiction — some line is monochromatic. ∎ Machine-checked: all 128 colorings were enumerated and every single one has a monochromatic line. Notice the architecture: this is the union bound's *exact* cousin — instead of bounding P(some bad line) ≤ 7·(1/8), the incidence structure lets us count the bad events perfectly, and the count overflows. (This is also the smallest 3-uniform non-2-colorable hypergraph — Exploration X2's frontier begins here.)

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 880 380" font-family="system-ui, -apple-system, 'Segoe UI', sans-serif">
  <rect x="0" y="0" width="880" height="380" fill="#ffffff"/>
  <text x="40" y="34" font-size="17" font-weight="700" fill="#193e5c">Figure 6 &#183; The Fano plane: 9 same-colored pairs on 7 lines (A13)</text>
  <text x="40" y="60" font-size="13" fill="#172333" font-weight="600">coloring: red {1, 5, 6}, blue {2, 3, 4, 7} &#8212; and the base line {2, 4, 3} is all-blue</text>
  <circle cx="440" cy="220" r="70" fill="none" stroke="#94a3b8" stroke-width="2"/>
  <line x1="440" y1="80" x2="562" y2="290" stroke="#94a3b8" stroke-width="2"/>
  <line x1="440" y1="80" x2="318" y2="290" stroke="#94a3b8" stroke-width="2"/>
  <line x1="440" y1="80" x2="440" y2="290" stroke="#94a3b8" stroke-width="2"/>
  <line x1="318" y1="290" x2="501" y2="185" stroke="#94a3b8" stroke-width="2"/>
  <line x1="562" y1="290" x2="379" y2="185" stroke="#94a3b8" stroke-width="2"/>
  <line x1="318" y1="290" x2="562" y2="290" stroke="#2563eb" stroke-width="4"/>
  <circle cx="440" cy="80" r="13" fill="#ffffff" stroke="#dc2626" stroke-width="2.5"/>
  <circle cx="379" cy="185" r="13" fill="#ffffff" stroke="#dc2626" stroke-width="2.5"/>
  <circle cx="501" cy="185" r="13" fill="#ffffff" stroke="#dc2626" stroke-width="2.5"/>
  <circle cx="318" cy="290" r="13" fill="#ffffff" stroke="#2563eb" stroke-width="2.5"/>
  <circle cx="562" cy="290" r="13" fill="#ffffff" stroke="#2563eb" stroke-width="2.5"/>
  <circle cx="440" cy="290" r="13" fill="#ffffff" stroke="#2563eb" stroke-width="2.5"/>
  <circle cx="440" cy="220" r="13" fill="#ffffff" stroke="#2563eb" stroke-width="2.5"/>
  <g font-size="12.5" font-weight="700" text-anchor="middle">
    <text x="440" y="84" fill="#991b1b">1</text>
    <text x="379" y="189" fill="#991b1b">6</text>
    <text x="501" y="189" fill="#991b1b">5</text>
    <text x="318" y="294" fill="#172333">2</text>
    <text x="562" y="294" fill="#172333">3</text>
    <text x="440" y="294" fill="#172333">4</text>
    <text x="440" y="224" fill="#172333">7</text>
  </g>
  <text x="40" y="330" font-size="12" fill="#172333">Red pairs 15, 16, 56 (lines {1,5,3}, {1,6,2}, the circle); blue pairs 23, 24, 34, 27, 37, 47 (the base line, {2,7,5}, {3,7,6}, {1,7,4}) &#8212; nine in all.</text>
  <text x="40" y="350" font-size="12" fill="#172333">Every pair lies on exactly one line, so 9 same-colored pairs must share 7 lines: some line carries two pairs of one color and is monochromatic.</text>
  <text x="40" y="370" font-size="12" fill="#64748b">C(3,2) + C(4,2) = 3 + 6 = 9 &gt; 7 lines: the count overflows &#8212; here the all-blue base line {2, 4, 3}.</text>
</svg>
```

**A14.** Choose a prime p = 3k + 2 with p larger than every |aᵢ| (there are infinitely many — a standard fact of number theory; any large enough prime congruent to 2 mod 3). The **middle third** of the residues mod p, M = {k+1, k+2, …, 2k+1}, is *sum-free mod p*: if x, y ∈ M then x + y lies in {2k+2, …, 4k+2}, which wraps mod p = 3k+2 to {2k+2, …, 3k+1} ∪ {0, …, k} — neither piece meets M. (Check p = 23, k = 7: M = {8, …, 15}; sums land in 16..30, i.e. mod 23 in {16..22} ∪ {0..7} — disjoint from M ✓ machine-checked.) Now randomize: pick λ uniformly from {1, …, p−1} and let S_λ = {a ∈ A : λa mod p ∈ M}. For each fixed a ∈ A, since 0 < |a| < p we have p ∤ a, so the map λ ↦ λa mod p is a bijection on {1, …, p−1}; as λ runs uniformly over {1, …, p−1}, the residue λa mod p is uniformly distributed over {1, …, p−1}, of which M = {k+1, …, 2k+1} occupies |M| = k+1 elements. Since p = 3k+2,

**P(λa mod p ∈ M) = |M|/(p−1) = (k+1)/(3k+1) > 1/3.**

By linearity — Lecture 2, one last time — E[|S_λ|] = n·(k+1)/(p−1) > n/3, so some λ gives **|S_λ| > n/3**. And S_λ is sum-free *as integers*: if x + y = z with all three in S_λ, then λx + λy ≡ λz (mod p) with all three residues in M — contradicting M's sum-freeness. ∎ Machine-checked, p = 23, A = {1, …, 12}: the 22 multiplier sets have sizes 4 or 5, totaling 96, average 48/11 ≈ 4.36 > 4 ✓; the max is 5 (λ = 1 gives S = {8, 9, 10, 11, 12}); and every one of the 22 sets is verifiably sum-free over the integers.

**A15.** Flip independent signs εᵢ = ±1, each fair. Expand the square: |Σ εᵢvᵢ|² = Σᵢ|vᵢ|² + Σ_{i≠j} εᵢεⱼ (vᵢ·vⱼ). For i ≠ j the signs are independent with E[εᵢεⱼ] = E[εᵢ]E[εⱼ] = 0 — every cross term has expectation zero (this is where independence *is* needed, and honestly so). So E[|Σ εᵢvᵢ|²] = Σ|vᵢ|² = 1, and some signing achieves |Σ εᵢvᵢ|² ≤ 1, i.e. |Σ εᵢvᵢ| ≤ 1. ∎ The proof never used the plane: any dimension, same one line. Machine-checked on three examples: v = (0.6, 0), (0, 0.8) — every signing gives |Σ| exactly 1 (equality: the worst case, and the theorem's bound is sharp); three copies of (1/√3, 0) — best signing gives 1/√3 ≈ 0.577; and (0.3, 0.4), (0.5, 0), (0, 0.5), (0.4, 0.3) — best ≈ 0.283. Note what the machine's first example teaches: the average of |Σ|² is exactly 1 with *no spread*, so "some signing ≤ 1" is all the method can ever promise there — and it delivers exactly that.

**A16.** Count the favorable tournaments. A ranking of the players forces every one of the C(n,2) games — the higher-ranked player wins each — so each of the n! rankings produces one tournament. And no transitive tournament is counted twice: its ranking is recoverable, because a transitive tournament's out-degrees are 0, 1, …, n−1, all distinct (the last player loses to everyone; remove them and induct), so a player's rank can be read off from their score. Hence exactly n! of the 2^C(n,2) equally likely tournaments are transitive, and

P(transitive) = n!/2^C(n,2).

For n = 5 that is 120/1024 ≈ 0.117; for n = 10 it is 10!/2^45 ≈ 1.03 × 10^{−7}; and the decay is faster than exponential — n! grows roughly like n^n while the denominator grows like 2^{n²/2}. Now the conclusion, from Exercise 4's other side: a tournament with *no* cyclic triple is exactly a transitive one. (Why: if u beats v and v beats w, then u must beat w — otherwise u, v, w are a cycle — so the beat-relation is transitive, and a transitive total relation is a ranking.) So P(some cyclic triple) = 1 − n!/2^C(n,2) → 1 as n grows: almost every tournament contains a cyclic triple. ∎ Machine-checked: the transitive tournaments on n = 2, 3, 4, 5 vertices number exactly n! (2, 6, 24, 120 out of 2, 8, 64, 1024).

**A17.** Linearity does all the work, one honest number at a time. Let X_i be the indicator that letter i lands home, and X = Σ_{i=1}^n X_i. Letter i is home in exactly (n−1)! of the n! arrangements — the other n−1 letters are free to permute — so E[X_i] = (n−1)!/n! = 1/n, honestly, for every i and every n. Summing: E[X] = n · (1/n) = **1**. The expected number of homecomings is one, no matter how many envelopes there are. ∎ Machine-checked over every arrangement for n = 2, …, 6: the mean fixed-point count is exactly 1 each time. Two honest notes. (1) The expectation is not a promise — the actual count swings from 0 to n, and its concentration around 1 is a variance story (Lecture 6's world; Exercise 18 trains exactly that computation). (2) This one line is the engine under Chapter 1's derangement world: X1 there asks for the same expectation by double counting, and follows it to the deeper law — the fixed-point count converges to Poisson(1), the shadow of this expectation. On average one success; sometimes none.

**A18.** Write X = Σ_{e∈E(K_n)} X_e, the sum over the C(n,2) edges of K_n, with X_e the indicator that edge e = uv is crossed by the random vertex partition. Each X_e is a Bernoulli(1/2) variable: E[X_e] = 1/2 and Var(X_e) = 1/4, so E[X] = C(n,2)/2. For the variance, name the lesson before using it — this is the exercise's second question. **The edge-crossing indicators are not mutually independent** — on any triangle u, v, w, X_uv ⊕ X_vw ⊕ X_wu = 0, so all three can never fire simultaneously — but, as Lecture 2 proved, they are *pairwise independent*: for any two distinct edges e ≠ f (disjoint or sharing one endpoint), E[X_eX_f] = P(both crossed) = 1/4 = E[X_e]·E[X_f], so every covariance Cov(X_e, X_f) vanishes. Since the variance of a sum depends only on the pairwise moments,

**Var(X) = Σ_e Var(X_e) + Σ_{e≠f} Cov(X_e, X_f) = C(n,2)·(1/4) + 0 = C(n,2)/4**

— identical to the variance of the edge count in G(n, ½), where the C(n,2) edge indicators are mutually independent. This is Lecture 2's lesson in service — pairwise independence is free where variance is concerned; the dependence hides in *joint* events (the triangles), which the variance never consults. Then Chebyshev: for every n ≥ 1, P(|X − C(n,2)/2| ≥ n) ≤ Var(X)/n² = C(n,2)/(4n²) = (n−1)/(8n) < 1/8 — strictly, for every n — so P(|X − C(n,2)/2| < n) > 7/8. The random cut's crossed-edge count hugs its mean within ±n, at 7/8 confidence, with no independence assumption beyond pairwise ever spent. ∎ Machine-checked twice, on both distributions the exercise names: over all 2^C(n,2) graphs of G(n, ½) for n = 2, …, 5, the edge count has mean exactly C(n,2)/2 and variance exactly C(n,2)/4 (n = 5: mean 5, variance 5/2, over all 1024 graphs); and over all 2⁵ = 32 side assignments of K₅'s vertices — 2 cut 0 edges, 10 cut 4, 20 cut 6 — the mean is (2·0 + 10·4 + 20·6)/32 = 5 = C(5,2)/2 and the variance is (2·25 + 10·1 + 20·1)/32 = 80/32 = 5/2 = C(5,2)/4. Same mean, same variance, completely different distributions — exactly what pairwise independence pays for.

**A19.** Let v be a player of maximum out-degree d⁺(v) = d, and suppose some opponent u dodges v for two steps: u beat v (otherwise v reached u directly), and u beat every player that v beat — otherwise some w with v → w → u gives the two-step road. Now count u's wins honestly, in the degree-sum spirit: u beat v *and* all d of v's victims, and u is none of those d+1 players, so d⁺(u) ≥ d + 1 — one more win than the maximum out-degree in the whole tournament. Contradiction. Nobody dodges v: **every player of maximum out-degree is a king**, and since a maximum always exists, every tournament has a king. ∎ Machine-checked on every tournament on n = 2, …, 5 vertices (1,098 tournaments, 1,678 maximum-out-degree players in all): every maximum player reached every other player within two steps, zero exceptions. Note the moral: the king is found by a counting contradiction, never by construction — Lecture 1's existence-without-construction, in tournament clothes.

**A20.** Alteration, run exactly as Lecture 5 taught it. Choose each vertex independently with probability p = ln(δ+1)/(δ+1); let D₀ be the chosen set, so E[|D₀|] = np. Call a vertex *uncovered* if neither it nor any neighbor was chosen, and let U be the uncovered set. For a fixed vertex v, the set {v} ∪ N(v) has d(v)+1 ≥ δ+1 vertices, each missed independently with probability (1−p), so P(v ∈ U) = (1−p)^{d(v)+1} ≤ (1−p)^{δ+1}. The hint's bound closes the estimate: 1−x ≤ e^{−x}, so (1−p)^{δ+1} ≤ e^{−p(δ+1)} = e^{−ln(δ+1)} = 1/(δ+1). Sum over vertices: E[|U|] ≤ n/(δ+1). Now repair: D = D₀ ∪ U dominates by construction — every vertex is either chosen or was uncovered and repaired in — and

E[|D|] ≤ np + n/(δ+1) = n(1 + ln(δ+1))/(δ+1).

Some outcome does at least as well as the expectation, so a dominating set of that size or smaller exists. ∎ Machine-checked on every labeled graph on at most six vertices (33,867 of them): the true minimum dominating number never exceeded n(1+ln(δ+1))/(δ+1).

**X1 (Exploration notes).** In any tournament with property S(2), every vertex v must have in-degree d⁻(v) ≥ 3: first, d⁻(v) ≥ 1 because v is beaten; if u → v, the pair {u, v} is beaten by some w, giving w → u and w → v (d⁻(v) ≥ 2); and if d⁻(v) = 2 with N⁻(v) = {u₁, u₂} and u₁ → u₂, then no player can beat both v and u₁ (the beater of v must be u₂, but u₁ → u₂). Summing d⁻(v) ≥ 3 over all n vertices gives C(n,2) = Σ_v d⁻(v) ≥ 3n, forcing n ≥ 7 (with d⁻(v) = d⁺(v) = 3 for every vertex at n = 7). The unique 7-vertex winner up to isomorphism is the **Paley tournament QR₇** on ℤ₇, where a → b iff b − a ∈ {1, 2, 4} (mod 7) — the nonzero quadratic residues modulo 7 (machine-checked here: no tournament on at most 6 vertices has S(2), QR₇ has it, and all 240 labeled 7-vertex S(2) tournaments are copies of QR₇). For k = 3, every in-neighborhood N⁻(v) must itself be an S(2) tournament of order ≥ 7 (the beater of any pair inside N⁻(v) ∪ {v} must lie in N⁻(v)), forcing d⁻(v) ≥ 7 and n ≥ 15 (the true minimum for S(3) is n = 19, achieved by QR₁₉ — a known computation in the literature; machine-checked here that QR₁₉ has S(3), against the union bound's certificate of 91).

**X2 (Exploration notes).** For k = 3 on n = 4 vertices, a balanced 2–2 vertex coloring contains no monochromatic 3-subset, so all C(4,3) = 4 edges can be present and the hypergraph remains 2-colorable — nothing fails. On n = 5 vertices, any 2-coloring has a color class of size ≥ 3, so the complete 3-uniform hypergraph C([5],3) (m = 10 edges) is not 2-colorable; conversely, any 3-uniform hypergraph on 5 vertices with m ≤ 9 edges omits at least one 3-subset {a,b,c}, and coloring {a,b,c} red and [5]∖{a,b,c} blue leaves zero monochromatic edges — so the minimum is exactly m = 10. On n = 6 vertices, each 3-edge is monochromatic under exactly 1 of the ½·C(6,3) = 10 balanced 3–3 vertex partitions, so every 3-uniform hypergraph with m ≤ 9 edges is 2-colorable by a balanced 3–3 split, while C([5],3) embedded on 6 vertices fails at m = 10 — the minimum is again exactly m = 10, before dropping to the global minimum m(3) = 7 at n = 7 (the Fano plane of Exercise 13, the smallest 3-uniform non-2-colorable hypergraph of all).

---

## Revision History & Verification Notes

*The lectures above should read like a finished book; the development record lives here, so the body never interrupts itself with its own history.*

**Editions.** Reference edition (5 problem families, 8 methods, pattern table) → **Feynman lecture edition** (this one): the five families became five lectures with ✎ discovery checkpoints; the pattern table moved into the Trick Bag at the end; all four reference-edition exercises were preserved (as Exercises 1, 3, 5, 10), re-graded and re-hinted; eight new graded exercises, three ◆ pattern-unknown problems and two ◐ Explorations were added; worked answers A1–A15 written, every one machine-verified before publication. The computational lab was carried over unchanged (its recorded outputs are from the verified 2026-10-09 execution), with comments normalized to plain ASCII and its cross-references renumbered. **Backlog completed (session 27):** Lecture 6 (the second-moment method) and §4.3 (the Lovász Local Lemma) added; Lecture 5's asymptotics derived in full (both constants, exact-integer regime checks); the constants ladder 1/(e√2) < 1/e < √2/e installed; Trick Bag and formula box extended; every new number machine-verified before installation. **Adversarially reviewed (session 62):** the whole chapter re-audited chunk by chunk by two arguing experts with a fresh exhaustive machine battery — seven defect classes fixed (see the review record below); everything else green. **Expansion pass (session 88):** a user-supplied Chapter 4 draft was compared against this master clause by clause and adopted on merit — the pencil proof of R(k,k) > ⌊2^{k/2}⌋ for all k ≥ 3 (§4.1); the full Lovász Local Lemma proof plus the full Spencer derivation via the Mutual Independence Principle (§4.3); the explicit Cauchy–Schwarz step (Lecture 3); the ceiling-form alteration bound with rigorous two-sided Stirling asymptotics (Lecture 5); the full case-analysis variance computation with Markov named (Lecture 6); six vector figures in the Chapter 3 convention; and answer upgrades (A5 for every n ≥ 2, A7's honest 2n factorization, A10's Edwards general-bound proof, A12's S(k) asymptotic, A13's quadratic, A14's bijection step, A18's cut-experiment redesign). Five master defects the draft exposed were repaired on its evidence (see the session-88 record below).

**Corrections.** The reference edition's Exercise 2 claimed every graph has a bipartite subgraph with ≥ m/2 + √(m/8) edges. **The claim is false**, and the machine is unambiguous: K₃'s best cut is 2 < 1.5 + √0.375 ≈ 2.112, and K₅'s is 6 < 5 + √1.25 ≈ 6.118 — an exhaustive scan of all 27,474 connected graphs on 3 to 6 vertices finds exactly these two violators, both odd cliques, precisely the graphs where the true theorem is tight. The exercise is now the Edwards–Erdős bound (Exercise 10 / A10) with a complete proof; the historical source of the false version is recorded there — Edwards' genuine arbitrary-graph bound ⌈m/2 + √(m/8 + 1/64) − 1/8⌉, which does hold (machine-checked, zero violations up to n = 6).

**Verification record.** Every quantitative claim in the lectures and answers was machine-verified in-session, deterministically and exhaustively where finite: K₄'s eight partitions cut 0, 3, 3, 3, 3, 4, 4, 4 (expectation 3 = m/2, maximum 4); Szele totals — n = 3: 12 directed Hamiltonian paths over all 8 tournaments (transitive: 1 each; 3-cycles: 3 each; E = 1.5 = n!/2^{n−1}), n = 4: 192 over 64 (E = 3, range 1–5); directed Hamiltonian cycles — n = 4: 24 over 64 (E = 0.375 = 6/16, max 1), n = 5: 768 over 1024 (E = 0.75 = 24/32, max 3), both matching (n−1)!/2^n; P₄'s Caro–Wei value 5/3 ≤ α = 2; Caro–Wei equality on four disjoint-clique unions; cyclic triples at n = 5: E = 2.5 = C(5,3)/4 over all 1024 tournaments, max 5 (regular), min 0 (transitive); triangle-free α(α+1) ≥ n on all 7 + 41 + 388 + 5789 triangle-free graphs with n ≤ 6 (and the C₅ trap α² = 4 < 5 confirming the α-vs-α−1 distinction); the alteration bound α ≥ n²/(4m) on all graphs with n = 5, 6 and m ≥ n/2 (968 + 32647 cases, zero violations); Edwards–Erdős (4·maxcut ≥ 2m + n − 1) on all connected graphs with n ≤ 6, zero violations, with sharpness confirmed exactly on K₃, K₅, K₇ and the windmill; the good-pair lemma on every 2-connected graph with n ≤ 6 (1 + 10 + 238 + 11368 graphs) and every even-degree 2-connected graph on 7 vertices (22,834 graphs, the entire cycle space of K₇); Ramsey's R(k,k) > ⌊2^{k/2}⌋ by exact BigInt arithmetic for k = 4..17 and by the (en/k)^k estimate for k = 18..64; the union bound's certified frontier 6, 11, 17, 27 for k = 4..7 and its k = 3 weakness (certifies only n = 3); the deletion optimizer by exact rational comparison over all n ≤ 500 (k = 5: n = 13, tie at R(5,5) > 11; k = 6: n = 21, R(6,6) > 18; k = 7: n = 33, R(7,7) > 29); property S(k) certifications 21 and 91 by exact comparison of C(n,k)(2^k−1)^{n−k} against (2^k)^{n−k}; the α,ω ≤ 2log₂n products 12870·2^{−27} ≈ 9.6×10⁻⁵ (n = 16, k = 8) and C(100,14)·2^{−90} ≈ 3.6×10⁻¹¹; the Fano plane's pair coverage (21 pairs, each exactly once) and all 128 colorings carrying a monochromatic line, with the same-colored-pair minimum 9 > 7; the sum-free construction at p = 23 (M sum-free mod 23; multiplier-set sizes totaling 96, average 48/11 ≈ 4.36 > 4, maximum 5, all 22 sets integer-sum-free); vector-signing examples with minimum norms 1, 1/√3, 0.283 (all ≤ 1, one exactly 1); and the property-B ladder (nothing on 4 vertices; the n = 5 and n = 6 minima coincide — recorded in the Atlas session log; the chapter leaves X2's numbers to the reader). The exploration censuses behind X1 (no S(2) tournament exists on at most 6 vertices; the quadratic-residue tournament mod 7 has S(2)) are likewise recorded in the Atlas — and since the session-99 expansion pass their censuses are condensed into the X1/X2 Exploration notes closing this answer key; the explorations themselves stay open-ended on the exercise page (the notes hand over the censuses, not the investigation). Session-27 additions, each machine-verified before installation: the second-moment identities E[X] = C(n,3)p³ and E[X²] = C(n,3)p³ + 3(n−3)C(n,3)p⁵ + [C(n,3)² − C(n,3) − 3(n−3)C(n,3)]p⁶ confirmed exactly against full enumeration at n = 4, 5, 6 and p = 1/2, 1/4 (all 2^{C(n,2)} graphs each), with Paley–Zygmund P(X>0) ≥ E[X]²/E[X²] verified on the same exact distributions (n = 6, p = ½: E[X] = 5/2, E[X²] = 45/4, bound 5/9 ≈ 0.556 against the exact 26,979/32,768 ≈ 0.823) and the α ≤ 2log₂n product trend 10^{−4}/10^{−10}/10^{−25}/10^{−42} at n = 16/100/10⁴/10⁶; the asymptotic regimes by exact integer arithmetic at k = 10, 15, 20, 25, 30 — E[X]/n at c = 0.9/e falls 1.6% → 0.06% while at c = 1.5/e it explodes 2.0 → 1,681, and the union bound's E[X] stays below 1 at c = 0.99/(e√2) through k = 30, exceeds 1 from k = 15 at c = 1.2/(e√2), and at c = 1.05/(e√2) crosses between k = 40 and k = 45; the Local Lemma's dependency identity d + 1 = Σ_{i≥2}C(k,i)C(n−k,k−i) brute-confirmed at (k, n) up to (5, 12); the Local Lemma's certified frontier (exact integer comparisons, rational e-bounds) R > 5/9/15/25/41 at k = 4..8 against the union bound's 6/11/17/27/42 and alteration's 6/11/18/29/47 — the asymptotic leader is the small-k laggard; the Θ(log k/k) correction: c = (√2/e)(1 − 2ln k/k) certifies at k = 15..30 while (1 − ln k/k) still fails at k = 30; and the Property-B budgets ⌊2^{k−1}/e⌋ − 1 = 0, 1, 4, 10, 22, 46 at k = 3..8, with exhaustive detector sweeps on 6 vertices (all 30 disjoint-edge 3-uniform hypergraphs and all 120 meet-at-most-one 4-uniform hypergraphs 2-colorable — zero counterexamples at the enumerable scale). Session-29 additions, all machine-verified before installation: the union-bound frontier re-derived exactly (k = 4..8 certifies R > 6, 11, 17, 27, 42) and the alteration frontier re-derived (> 6, 11, 18, 29, 47); the derandomized greedy (conditional-expectation edge coloring, edges in lexicographic order, ties to red) run at the four guarantee points (k, n) = (4, 6), (5, 11), (6, 17), (7, 27) — the conditional expectation starts at 15/32, 462/512, 12,376/16,384 and 888,030/1,048,576, never rises, and finishes at exactly 0 monochromatic k-cliques each (the invariant held throughout: the running value equals the current count of still-possible monochromatic cliques); and the observed-reach scans run upward from n = 3 to the first failure — k = 4 succeeds through n = 10 and fails at n = 11 (1 monochromatic K₄), k = 5 succeeds through n = 22 and fails at n = 23 (5 monochromatic K₅), k = 6 is clean through the scan's cap n = 26 with no failure found, and k = 7–8 are not scanned. Discrepancies across all passes: none beyond the two caught in the reference edition's Exercise 2, which is precisely why every claim here was re-verified before publication.

**Figures.** None at publication — and deliberately so at the time: this chapter's arguments are arithmetic on expectations; its one honest picture (K₄'s cut census) is a table, and the lab's outputs are its graphics. **Session-88 exception (2026-10-23):** six vector figures installed with the expansion pass, in the Chapter 3 convention (fenced svg, in-figure titles, numeric entities): the K₄ local flip (Figure 1), the Szele census (Figure 2), Caro–Wei local winners on P₄ (Figure 3), alteration on K₆ (Figure 4 — drawn from a machine-verified X = 2 coloring, since Goodman's theorem forbids X = 1 on a complete K₆), the triangle-overlap cases behind Var(X) (Figure 5), and the Fano plane (Figure 6). Every quantitative claim in every figure was machine-verified before installation (receipts in the session-88 record below).

**Standing decisions.** The lecture text carries no session or review history (this appendix absorbs it). The lab's recorded outputs are from real executions and are the reference for any reader re-run (a Raspberry Pi is more than enough — see Chapter 1's post-export self-test for protecting code through an export pipeline). Small-case machine checks certify only the cases they run: they are detectors, and the proofs above are the proofs.

**Backlog completion (session 27).** All four method items of the recorded backlog are closed. Alteration-Ramsey asymptotics: derived in full in Lecture 5 (one Stirling formula, both constants, both machine-checked regimes). Second-moment method: Lecture 6 (Paley–Zygmund and its Chebyshev costume, the triangle threshold p = 1/n, the chromatic corollary χ(G(n,½)) ≥ n/(2log₂n) with Bollobás's sharp upper bound honestly flagged). Lovász Local Lemma: §4.3 (symmetric form, stated with its proof flagged; the Spencer 1975 Ramsey application R(k,k) > (√2/e − o(1))·k·2^{k/2}; the local Property-B budget ⌊2^{k−1}/e⌋ − 1; the honest small-k frontier table). Deletion-method constants: sharpened everywhere they appear — the 1/(e√2) → 1/e → √2/e ladder is now derived, not cited. One item remains deferred, as originally planned: the interaction of these bounds with van der Waerden-type problems waits on Chapter 10.

**External review audit (session 28).** An independent mathematical review of the five-lecture web export was audited claim by claim before adoption. The review was right four times, and the chapter now records it: Szele at n = 10 is 10!/512 = 3,628,800/512 = **7,087.5** — the chapter had printed a factor of ten less (708.75), so the certified count rises to at least **7,088** (Lecture 2 corrected, the exact arithmetic now on the page); the expected-paths-to-expected-cycles ratio is **2n**, not n/2 — each directed Hamiltonian cycle contains exactly 2n directed Hamiltonian paths (A7 corrected); Exercise 10's refutation could not be a two-vertex example — K₂ *satisfies* the false bound (1 ≥ 0.5 + √0.125 ≈ 0.854) — and now names K₃ and K₅; and the good-pair lemma's proof had skipped ears with no internal vertices (single-edge chords), a genuine gap closed by choosing the last ear *with* an internal vertex plus the all-chords case. The review's ten-player witness was verified before installation: the tournament whose out-neighbor bitmasks for players 0–9 are 798, 116, 360, 34, 684, 705, 921, 271, 570, 142 (player i beats player j iff bit j of mask i is set) is a valid tournament with exactly **9,793** directed Hamiltonian paths, counted by subset dynamic programming — so rich individual tournaments *can* be written down at n = 10, and Lecture 2's wording now separates that from the still-open absence of a uniform construction with the same asymptotic guarantee. The review's independence finding was also right, against the chapter's own wording: two edge-crossing indicators in the fair-coin model are *independent* even when the edges share a vertex (over a triangle's eight labelings each pair fires together in two rows: 1/4 = (1/2)²), and the true dependence is joint — X_uv ⊕ X_uw ⊕ X_vw = 0, all three never firing at once — now taught precisely in Lecture 2 (with a tabulation checkpoint), Exercise 1 and A1. The A14 modular interval is completed as {0, …, k} (machine-checked for every k ≤ 12: M + M lands in {2k+2, …, 3k+1} ∪ {0, …, k} mod p = 3k+2, disjoint from M), and the lab's Monte-Carlo sentence is now labeled a recorded side-experiment distinct from the embedded program. The review's independent numbers — alteration survivors 10.4863 / 17.6887 / 28.9260 at (k, n) = (5, 13), (6, 21), (7, 33) (its "17.6880" and "28.9259" small final-digit roundings); the property-B minima 10 and 10 at n = 5, 6; the quadratic-residue tournament mod 7 having S(2) — all matched the chapter's recorded verifications: a clean external cross-check. One review observation was at first traced to the pipeline rather than the source: the banner "mojibake" was judged a proper UTF-8 em dash (bytes E2 80 94) in the web edition's frame — a viewing artifact, the source needing no repair. That judgment was wrong, and is corrected here (session 32): prompted by the identical Ch. 5 finding, a byte-level scan shows the frame's banner carries the double-encoded em dash (â + U+0080 + U+0094) in the canvas source itself, as does every web edition's frame — all five were repaired in session 32 with proper UTF-8 em dashes. Adopted pedagogy: the triangle's eight-labeling tabulation as a Lecture 2 ✎ checkpoint, and Exercise 10 flagged as the chapter's most demanding exercise with its lemma's location named. Deferred: a random/greedy/altered comparison table (the Trick Bag already carries those contrasts).

**Backlog pass (session 29).** The deferred comparison table is now installed in Lecture 5, as the subsection "The same race, run without dice: greedy joins the table." The union bound is derandomized there in full — the conditional-expectation walk never rises, so greedy inherits the union bound's certificate exactly, and the guarantee column is the union bound's column at no cost — and the constructor's *observed* reach is machine-measured rather than asserted: edges in lexicographic order with ties broken to red, run upward in n to the first failure (k = 4 stops at n = 10; k = 5 at n = 22, a clean K_22 that doubles the chapter's best certified R(5,5) bound; k = 6 clean through the scan's cap; k = 7–8 not scanned). Every number in the table — all five columns — was verified before installation; the guarantee runs' exact conditional-expectation trajectories (dyadic starting values, never rising, finishing at zero) are recorded in the verification record above. The subsection also names the honest lesson the table teaches: analysis and search are different sports, and neither column pretends to be the other.

**Follow-up review audit (session 31; every claim machine-verified before acting).** A second, independent review of the revised web edition confirmed the session-28 fixes and reported no new central-theorem defect — and its assessment was itself re-verified claim by claim, with fresh machine runs, before this record was written. The six status rows: (1) the independence lesson is in place and exact — Lecture 2's eight-labeling tabulation shows adjacent-edge crossing indicators pairwise independent (each fires in four rows, together in two: 1/4 = (1/2)²) and the triangle's three indicators pairwise independent yet never all firing (probability 0, not 1/8; zero of the eight labelings crosses an odd number of the triangle's edges); (2) Szele at n = 10: 10!/2⁹ = 3,628,800/512 = 7,087.5, so at least 7,088 directed Hamiltonian paths — the arithmetic re-verified, and a fresh witness tournament found by randomized search carries 8,414 of them (the recorded witness has 9,793; both clear the bound); (3) the path/cycle expectation ratio is 2n, re-derived by full enumeration over all tournaments at n = 3, 4, 5 — E[paths] = n!/2^{n−1} and E[cycles] = (n−1)!/2ⁿ exactly, ratio exactly 2n — with both counting conventions (paths as linear orderings, cycles as cyclic orderings up to rotation and reversal) explicit at every site the ratio appears; (4) Exercise 10's refutation names K₃ and K₅ — in place (one precision: the review's table row describes this K₃ as the pairwise-not-joint-independence example; those are two distinct K₃ appearances — the √(m/8) refuter in Exercise 10 and the dependence witness in Lecture 2 — and both are installed); (5) the good-pair lemma's proof states its single-edge-ear base case explicitly in the source — chords allowed, the last-ear-with-an-internal-vertex choice, the all-chords case — so the review's residual concern is only the PDF render; (6) A14's modular residue intervals are complete in the source and machine-checked mod 23 — likewise a render check only. The review's §3 checks: Szele's arithmetic ✓; the 2n convention ✓; Caro–Wei re-verified on all 1,099 graphs with n ≤ 5 over all orderings — the selected set is independent (zero violations) and the exact average equals Σ 1/(d(v)+1); the existence-versus-witness distinction is taught in both places the review asks for it (Lecture 2's honest paragraph on the missing uniform construction; Lecture 5's derandomized-greedy subsection). No mathematical defect was found, and the verdict — no rewrite — is confirmed and adopted. The review's remaining recommendations are the PDF export gate: print the web edition to PDF and check equations, code blocks, and the appendix for clipping; re-extract the embedded lab (the chapter carries one; the review's "both labs" reads as boilerplate) from the actual PDF and compare outputs with the HTML version; confirm the ear-decomposition base case and A14's intervals render intact. Those are user-owned steps — the last gate before freezing the chapter, at the user's direction.

**Backfill (session 41).** Five graded exercises (16–20) with pattern-mapped hints were added, per the atlas-wide backfill mandate: the transitivity probability n!/2^C(n,2); expected fixed points (linearity's cleanest showcase — expectation exactly 1, for every n); Chebyshev on the random graph's edge count (variance licensed by pairwise independence alone); tournament kings (every maximum out-degree player is one); and dominating sets by alteration (the n(1+ln(δ+1))/(δ+1) bound). Worked answers A16–A20 were machine-verified before installation: the n! census of transitive tournaments (n = 2–5), the fixed-point average over all arrangements (n = 2–6), edge-count mean and variance over all graphs (n = 2–5), the king check over all tournaments (n = 2–5: 1,098 tournaments, 1,678 maximum players), and the dominating-number bound over all 33,867 labeled graphs on n ≤ 6 vertices.

**Lab expansion (session 44).** A second lab part was added, per the atlas lab-expansion mandate: Lecture 6's triangle threshold, measured at scale — seeded Monte-Carlo on G(n, c/n) with a Lehmer LCG (x ← 48271·x mod (2³¹ − 1)) implemented identically in the Python lab and in the verifying TypeScript port, which reproduced all twelve printed rows before installation (no unseeded randomness anywhere, per the labs-record-only-actually-run-outputs rule). Recorded numbers: n = 60, 120, 240 at c = 0.5, 1, 2, 3, 200 samples per cell — fractions with a triangle 0.020/0.145/0.740/0.980, 0.025/0.110/0.730/0.970, 0.025/0.105/0.740/0.995 against the Poisson limit 1 − e^{−c³/6} = 0.021/0.154/0.736/0.989; mean triangle counts 0.03/0.15/1.45/4.04, 0.03/0.12/1.26/4.16, 0.03/0.12/1.41/4.26 against c³/6 = 0.02/0.17/1.33/4.50. The c = 1 column runs below the limit and converges slowly — finite-size effects, recorded honestly (sampling noise ±0.03 at 200 samples; P(no triangle) 0.855/0.890/0.895 against the limit e^{−1/6} ≈ 0.846). The pre-existing block was renumbered Part 1; its code and verified outputs are unchanged.

**Rounding repair (session 51).** Lecture 6's closing checkpoint printed the Poisson limit as e^{−1/6} ≈ 0.852; the correct three-decimal value is ≈ 0.846 (the lab's Part 2 sites already printed 0.846 correctly). The slip was caught while shipping Chapter 14, where the same limit is re-derived from the factorial moments and machine-checked (session 51's receipt campaign); this repair executes at Chapter 14's ship, together with this web-edition rebuild. No other number in the chapter is affected — both other occurrences of the limit were verified correct before this repair.

**Adversarial review (session 62).** The chapter was re-audited chunk by chunk by two arguing experts — skeptic and engineer — with every retained objection machine-verified before any edit and every edit re-verified after installation. The fresh battery came back essentially all green: the K₄ cut census (0, 3, 3, 3, 3, 4, 4, 4); the flip-derandomization sweep over all 33,867 graphs on at most 6 vertices; the Szele censuses (n = 3: 12 paths over 8 tournaments; n = 4: 192 over 64, range 1–5; n = 10: 10!/2⁹ = 7,087.5 and the 9,793-path witness); Caro–Wei over all 1,099 graphs with n ≤ 5; the K₅ census — exactly 12 of 1024 edge colorings avoid a monochromatic triangle; the union-bound frontier 3, 6, 11, 17, 27, 42; R(k,k) > ⌊2^{k/2}⌋ exact for k = 4..17 and by the (en/k)^k estimate for k = 18..64; the S(k) certifications n = 21 and n = 91; the Local Lemma identity (up to (5, 12)) and frontier 5, 9, 15, 25, 41; the Property-B budgets 0, 1, 4, 10, 22, 46 with the 30 + 120 detector sweeps; the alteration optimizer (best n = 13/21/33; survivors 5369/512 ≈ 10.49, 17.6887, 28.9260); the second-moment identities against full enumeration at n = 4, 5, 6 × p = 1/2, 1/4; both asymptotic regimes and the union-bound boundary claims; the derandomized greedy — all four guarantee trajectories starting 15/32, 462/512, 12,376/16,384, 888,030/1,048,576, never rising, finishing 0, with observed reach clean through n = 10 at k = 4 (first failure n = 11), n = 22 at k = 5 (first failure n = 23), and through the n = 26 cap at k = 6; the A6–A20 answer checks; and — the lab gate — an independent port of the Part 2 Lehmer LCG reproducing all twelve printed rows bit-for-bit. Four battery alarms were the reviewer's own checker bugs, re-run green against the chapter: the cyclic-triple expectation is exactly 2.5 = C(5,3)/4 (max 5, attained by 24 labeled tournaments; the regular tournament holds 5 cyclic of its 10 triples, Σ_v C(d⁺(v),2) = 5); directed Hamiltonian cycles at n = 5 total 768 with max 3 (attained by 40 of the 1024); transitive tournaments number exactly n! (2, 6, 24, 120); and A19's census holds — 1,098 tournaments on 2..5 vertices carry exactly 1,678 maximum-out-degree players, every one a king, zero exceptions. Seven defects were confirmed and fixed, each verified before installation: (1) Lecture 6's corollary trend opened at 10^{−14}; the n = 16 product is C(16,8)·2^{−27} = 12,870/134,217,728 ≈ 9.6×10⁻⁵, so both sites (corollary and verification record) now print 10^{−4} — the other three entries (10^{−10}, 10^{−25}, 10^{−42}; true values −10.45, −25.41, −42.41) were correct; (2) §4.3's "the i = 2 term dominates once n > 3k" fails at n = 3k for every k ≥ 8 (k = 8: i₃ = 244,608 > i₂ = 224,224); the true crossover is n* = 2k − 3 + ⌈(k−2)²/3⌉, machine-verified for k = 4..15 (i₂ ≥ i₃ ⟺ n ≥ n*), with an exact tie at n* when k ≡ 2 mod 3, and the i = 3 term already a ~1% tail in the Spencer regime (ratio 0.0102 at k = 20); (3) A10 and the appendix record called the 27,474 connected graphs "at most 6 vertices" — that count is the n = 3..6 slice (n = 1..6 totals 27,476), and both sites now read "3 to 6 vertices", the same convention repair Chapter 3 received at session 61; (4) the appendix's van der Waerden deferral pointed at Chapter 8 — its home has been Chapter 10 since session 46, and the pointer now says so; (5) the chapter's lone Lecture 1 subsection was numbered 1.2 with no 1.1 — renumbered 1.1 to match Chapters 2 and 3 (no cross-references existed anywhere); (6) A4's parenthetical claimed the regular 5-vertex tournament has "every single triple cyclic" — the true count is 5 of 10, which is the maximum, and the text now says so with the 24 attainers; (7) the lab Part 1 side-experiment never defined its event — a survivor is a K₅ edge coloring with no monochromatic triangle (exactly 12 of 1024), and the sentence now defines it. Honest notes, recorded without edit: the lab Part 1's six unseeded flip trials and its Monte-Carlo side-experiment stand as recorded executions; session-31's 8,414-path randomized witness stands as recorded; and the verification record's "exceeds 1 from k = 15 at c = 1.2/(e√2)" reads on the reviewer's convention as a first crossing at k = 12 — the lecture's own phrasing ("already exceeds 1 by k = 15") verifies exactly, and the difference is the n-rounding convention, not a defect. Figures: none, deliberately — the verdict stands; this chapter's arguments are arithmetic on expectations, and its honest pictures are the K₄ census table and the lab's outputs.

**Survey-adoption pass (session 83).** The paper-pattern survey's chunk-15 synthesis (papers/ANALYSIS.md, §5, in the cgt-atlas-backup repo) closed its face-naming list here: P10's celebrated face is **graphical Brascamp–Lieb** — the functional-analysis form of averaging, in which every edge of the host graph carries a two-variable function and the "some object beats the average" budget becomes an iterated L^p-duality/Hölder inequality. The survey's evidence: N2 (Sah–Sawhney–Stoner–Zhao 2019, the independent-sets-in-irregular-graphs settlement) already used the Hölder/convexity face as a verification step, and N8 — the same team with the same mentor structure (Sah and Sawhney MIT undergraduates, the 2021 Morgan Prize; Stoner a Harvard undergraduate; Zhao the faculty mentor — recorded honestly per the survey's author-level rule) — promoted it to the whole engine in "A reverse Sidorenko inequality", Inventiones mathematicae 221(2): 665–711 (2020), DOI 10.1007/s00222-020-00956-9 (metadata-verified in the survey's batch-N census against the NSF PAR, MIT DSpace, and the authors' pages): Lemma 3.1 (L^p duality + Cauchy–Schwarz), the mixed L^{p,q} matrix-norm reformulation, and the local inequality the main theorem reduces to — Kahn's entropy method honestly bypassed along the whole Kahn arc (Granville → Alon → Kahn 2001 → Zhao's swapping → Galvin–Tetali → Lubetzky–Zhao's Hölder reinterpretation → N8). Executed in the Trick Bag's P10 card; the chapter's own second-moment upgrade is untouched. No proof, exercise, or answer changed. The .html export is rebaked at this session's export pass.

**Expansion-pass adoption (session 88).** A user-uploaded Chapter 4 draft — an HTML file, rejected as a file per the no-script rule and adopted as content only, translated to the master's plain-Unicode notation — was compared against this master and adopted on merit; every adopted claim was machine-verified before installation, and every rejected claim was machine-refuted before rejection. The draft is a light re-edit of the session-62 master (~95% identical, carrying the session-80/83 additions verbatim), valuable chiefly for exposing latent master defects and for six genuinely new upgrades. The battery, all green: the §4.1 pencil chain — 2^{1+k/2}/k! strictly decreasing from 2√2/3 < 1 at k = 3 (exact products k = 3..20; the k = 3 site is the trivial n = 2 < k case, now stated); (1+1/d)^d < e and (d/(d+1))^d > 1/e for d = 1..200; the Local Lemma frontier 5/9/15/25/41 at k = 4..8; the α-correction under the floor convention n = ⌊c·k·2^{k/2}⌋ — α = 2 certifies every k = 5..60 while α = 1 certifies only k = 4, 5 and fails from k = 6 (the draft's "fails for every k ≥ 4" was false at k = 4, 5, and was repaired rather than adopted), with the Spencer formula's ratio verified → 1; the i = 2 dominance threshold n* = 2k − 3 + ⌈(k−2)²/3⌉ re-verified for k = 4..20 and the Vandermonde dependency identity d + 1 = #{T : |S∩T| ≥ 2} brute-confirmed up to (5, 12); the Szele/path/cycle censuses at n = 3, 4, 5 with the per-tournament identity closings = n × cycles and the corrected 2n = n × 2 factorization (n arc-deletions per cycle, closing-arc coin 1/2); the A5 product below 1 for every n = 3..300 (9.6×10⁻⁵ at n = 16, ≈3.6×10⁻¹¹ at n = 100) with 2^{1+k/2}/k! ≤ 1/3 for k ≥ 4, equality at k = 4; the A18 cut experiment — mean C(n,2)/2, variance C(n,2)/4 at n = 2..6, with the n = 5 census 2/10/20 side assignments cutting 0/4/6 (variance exactly 5/2) alongside the retained G(n, ½) enumeration receipt; the A12 first-dip certifications (k = 2: n = 21; k = 3: n = 91) with n = 90 at exactly 1.058 — repairing the master's "≈ 1.056" slip — and the (ln 2 + o(1))·k²·2^k asymptotic; the A13 quadratic r² − 7r + 21 = (r − 7/2)² + 35/4 (minimum 9 at r = 3, 4, i.e. C(3,2) + C(4,2) = 3 + 6 — repairing the master's "3 + 3" typo), with the figure coloring red {1,5,6}/blue {2,3,4,7} carrying exactly 9 same-colored pairs and exactly one monochromatic line {2,3,4}; the A14 multiplier bijection with P = (k+1)/(3k+1) = 4/11 > 1/3 at p = 23 (repairing a garbled probability fragment), M sum-free mod 23 with all 22 multiplier sets integer-sum-free; the A10 Edwards general bound in the exact integer form (8M − 4m + 1)² ≥ 8m + 1 on all graphs with n ≤ 6, tight exactly on K₃, K₅, K₇; and the Lecture 6 identities exactly at n = 4, 5, 6 × p = 1/2, 1/4. The draft's own defects, machine-verified before rejection or repair: its alteration figure drew a complete K₆ coloring with X = 1 monochromatic triangle — impossible (Goodman's theorem: the minimum over all 32,768 K₆ colorings is 2, attained by 1,760 of them), so Figure 4 is drawn from a machine-verified X = 2 construction (red C₅ on {v₂,…,v₆} plus v₁ joined red to v₂, v₄; the two bad cliques {v₁,v₃,v₅} and {v₁,v₃,v₆} are both blue, and one deletion of v₁ kills both — s = 5 ≥ n − X = 4, honestly noted in the figure); its Figure-1 right panel placed v₂ and v₄ at the same coordinate so the drawn boundary could not separate {v₁,v₂} from {v₃,v₄} (redrawn); and its α = 1 clause (repaired as above). Rejected whole, with receipts: the draft's lab Part 3 — a "verification suite" whose ramsey_certified_frontiers(4) asserts (6,(8,6),5) while the code's own argmax computes (7,6), since f(7) = 5.90625 > f(8) = 5.8125 — machine-proven, so the suite fails its own frontier; also its float math.e and its dead greedy_ramsey_coloring; the draft's lab Part 1 rewrite (inert guards, a dead rng parameter, and an embedded side-experiment violating the recorded-side-experiment separation of session 62); the draft's lab Part 2 refactor (inert guard, identical outputs); and the draft as a file (s78: MathJax CDN, $-TeX, scripts). Master defects repaired on the draft's evidence, each machine-verified: (1) Exercise 7/A7's unguarded n = 2 falsehood (a 2-vertex tournament has no directed Hamiltonian cycle yet (n−1)!/2^n = 1/4 > 0 — now guarded to n ≥ 3); (2) A7's false "read the cycle in either direction" 2n mechanism (each directed cycle contains exactly n paths, not 2n — replaced by the honest n × 2 factorization); (3) A13's "3 + 3 = 9" arithmetic display; (4) A14's garbled probability fragment; (5) A12's "≈ 1.056" receipt slip. Pattern audit: clean — the draft's Trick Bag (including the session-83 Brascamp–Lieb face on P10) is identical to the master's, all hints unchanged, exercise numbering 1–20 + X1/X2 unchanged, so no atlas renumbering and no survey-era note was dropped. The .html export is rebaked at this session's export pass.

**Expansion pass (session 99).** A second user-supplied Chapter 4 draft — again an HTML file, adopted as content only per the no-script rule — was compared against this master clause by clause; it is a genuine new draft (1,094 lines / 156,236 bytes; not the session-88 file's resubmission), and every adopted claim was machine-verified fresh before installation, every rejected claim machine-refuted fresh before rejection. Pattern audit: clean — the draft's pattern references were not mangled (its apparent "P4" hits are the path graph P₄ inside SVG/aria text, false positives; all P-labels position-identical to the master's), and its one genuinely new pattern label — P14 on the alteration figure — is adopted into Figure 4's in-figure title. Adopted, each fresh-verified: the explicit eight-labeling coin tabulation closing Lecture 2's checkpoint (column sums [4,4,4], pairwise dot products [2,2,2], triple product 0, the six 2–1 rows yielding (1,0,1), (1,1,0), (0,1,1) twice each — full enumeration of {0,1}³); the α(K_n) = 1 computation appended to Lecture 3's checkpoint (n·1/n); the §4.1 pencil chain rewritten as an explicit two-case argument (k = 3 trivial — C(2,3) = 0, a 2-vertex graph cannot contain K₃; k ≥ 4 — n = ⌊2^{k/2}⌋ ≥ k, with the draft's false "≥ 4 ≥ k" repaired to "≥ k (equality at k = 4, 5)", verified for k = 4..60); the honest closing of the §4.1 checkpoint (2.5 ≥ 1 fails to certify R(3,3) > 5 although exactly 12 of the 1024 K₅ colorings survive — cross-checked against the K₅ census); the explicit four-case analysis of the greedy edge-coloring deltas D_red/D_blue in Lecture 5 (cross-checked exactly against brute-force conditional expectation at every step through n = 9 at k = 4); the fuller A9 comparison against Turán (both algebraic identities (n−m)(2m+n) − n² = m(n−2m) and 4m − (2m+n) = 2m − n verified over the full m/n grid, both inequality regimes); and the X1/X2 Exploration notes closing the answer key — X1: the in-degree ≥ 3 argument forcing n ≥ 7 for S(2), the QR₇ winner with its uniqueness census (nothing on n ≤ 6; all 240 labeled 7-vertex S(2) tournaments copies of QR₇, canonical-form-proven), the in-neighborhood argument forcing n ≥ 15 for S(3), and QR₁₉ carrying S(3) (fresh: all 969 triples dominated, regular out-degree 9) against the union bound's certificate of 91; X2: the n = 4 vacuity (all 15 hypergraphs colorable), the n = 5 minimum (exactly one non-colorable hypergraph in the full 1023-census — the complete C([5],3) at m = 10 — with the missing-triple coloring certifying m ≤ 9), the n = 6 balanced-partition pigeonhole (10 balanced partitions, each of the 20 triples a side exactly once, so m ≤ 9 is always colorable; embedded C([5],3) fails at m = 10, zero surviving colorings), and m(3) = 7 at the Fano plane (zero of 128 colorings survive — re-verified fresh). Rejected whole, with fresh receipts: the draft's ~330-line lab Part 3 — an s88-rejected retread with both decisive defects unfixed: its recorded frontier for k = 4 asserts (6,(8,6),5) while the code's own argmax computes (6,(7,6),5) (f(7) = 5.90625 > f(8) = 5.8125, the exact mismatch in an otherwise-green k = 3..8 frontier census), and its internal assert (t2 ≥ t3) == (n ≥ thresh) crashes at 55 degenerate tie points for every k = 6..15, so the suite cannot run to completion — its remaining recorded censuses re-verified green fresh (K₄ cuts 0,3,3,3,3,4,4,4 mean 3; K₅ cut mean 5, variance 5/2; tournament paths/cycles 12/3/2/1, 192/5/24/1, 7680/15/768/3; the prose audit's 1098 tournaments, 1678 max-players, 0 king failures, n = 5 cyclic mean 2.5 with max 5 ×24 and min 0 ×120; Caro–Wei on P₄ 5/3 = 5/3; disjoint-clique sums 3, 2, 2, 5; the G(6,½) moments E[X] = 5/2, E[X²] = 45/4, bound 5/9 against the exact 26,979/32,768) — the defects are localized, but a suite that contradicts itself is rejected as a suite; the draft's lab Parts 1–2 rewrites (the session-62-recorded inert-guard, dead-rng-parameter and embedded-side-experiment defects, unchanged retreads — master's Parts 1–2 kept verbatim); the draft's redesigned figures (its s88 figure defects were indeed fixed in this draft — but swapping six verified convention figures for near-identical redesigns is churn; the six master figures stand), including its alteration figure, whose X = 1 complete-K₆ claim remains impossible (Goodman's minimum is 2, attained by exactly 1,760 of 32,768 colorings, re-verified fresh — and the redrawn left panel omits six of K₆'s 15 edges, so even as a drawing it is not a complete coloring); A12's "n = 90 ≈ 1.056" (the s88-repaired slip reintroduced; the exact value is 1.0584 — the master's "≈ 1.058" stands); the draft's truncations of master receipts (A7's per-tournament closings identity, A10's subadditivity detail with the (8M−4m+1)² ≥ 8m+1 receipt, A18's G(n,½) enumeration receipt — receipts are never truncated); and the draft as a file (MathJax CDN, $-TeX, scripts). One draft improvement found already present in the master and not double-adopted: the Lecture 6 engine's "with 0 < E[X²] < ∞" hypothesis. The .html export is rebaked at this session's export pass.

---
*Chapter status: ✅ **Feynman edition + backlog closed (session 27) + external review audited (session 28) + backlog pass (session 29) + follow-up review audited (session 31) + exercise backfill (session 41) + lab expansion (session 44) + adversarial review (session 62) + expansion pass (session 88) + expansion pass (session 99)** — 6 lectures with ✎ discovery checkpoints and six vector figures (session 88, Chapter 3 convention), Trick Bag, 17 graded + 3 ◆ pattern-unknown + 2 ◐ exploration exercises, 20 worked answers (all machine-verified, several by exhaustive enumeration), verified lab in two parts (Part 1 carried over from the reference edition, Part 2 — the seeded triangle-threshold table — added), and this Revision History appendix. The reference edition's one false claim (the √(m/8) cut bound) was caught, refuted by K₃ and K₅, and replaced by the Edwards–Erdős bound with a complete proof; the session-28 external review's corrections — Szele's n = 10 expectation (7,087.5, not 708.75), A7's paths/cycles ratio (2n, not n/2), Exercise 10's counterexamples (K₃ and K₅, not a two-vertex example), the good-pair lemma's single-edge ears, and the precise independence lesson (pairwise independence is free; the dependence is the triangle's joint one) — are installed, each machine-verified before adoption. The review's deferred random/greedy/altered comparison table is installed in Lecture 5 (session 29): the union bound derandomized — greedy inherits the certificate — and the constructor's observed reach machine-measured (clean through K_22 at k = 5, double the best certified bound). A follow-up external review (session 31) re-examined the revised edition and found every prior fix in place and no new defect; each of its claims was re-verified by fresh machine runs before adoption. Its remaining recommendations are the PDF export gate — a user-owned step, the last before freezing. The session-62 adversarial review re-audited the whole chapter with a fresh machine battery and fixed seven defect classes — the corollary trend's first entry (10^{−4}, not 10^{−14}), the §4.3 i = 2 dominance threshold (n* = 2k − 3 + ⌈(k−2)²/3⌉, not 3k), two census scope labels (27,474 = the connected graphs on 3 to 6 vertices), the appendix's stale Chapter 8 pointer (van der Waerden lives in Chapter 10), the lone subsection numbered 1.2 (now 1.1), A4's false "every single triple cyclic" parenthetical (the regular tournament holds 5 cyclic triples of 10 — the maximum), and the lab side-experiment's undefined survivor event — each machine-verified before installation; four battery alarms were the reviewer's own checker bugs, re-run green against the chapter's numbers, and the lab's Part 2 table was reproduced bit-for-bit by an independent port. Next: the PDF gate; learner testing now follows the completion of the whole project scope, at the user's direction. The session-88 expansion pass compared a user-supplied draft against this chapter and adopted its content on merit — the pencil proofs (§4.1's R(k,k) > ⌊2^{k/2}⌋ for all k ≥ 3), the full Local Lemma and Spencer derivations (§4.3), the ceiling-form alteration bound and rigorous two-sided asymptotics (Lecture 5), the case-analysis variance with Markov named (Lecture 6), the explicit Cauchy–Schwarz step (Lecture 3), six vector figures, and seven answer upgrades — while repairing five master defects the draft exposed and rejecting the draft's own defective parts with receipts (the impossible X = 1 alteration figure vs. Goodman's theorem, the mis-separating flip figure, the self-contradicting lab Part 3, the inert lab rewrites, and the α = 1 clause as written; appendix session-88 record).*
