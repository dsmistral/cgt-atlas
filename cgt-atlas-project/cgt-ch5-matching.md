---
name: "cgt-ch5-matching"
title: "Ch. 5 — Matching, Flows & Hall: A Lecture Course in the Feynman Style"
type: "text/markdown"
---

# Chapter 5 · Matching, Flows & Hall

*A lecture course in the spirit of the earlier chapters: the idea before the formula, the story before the proof, and the proof as a conversation. Every method of the reference canon is preserved inside the narrative. The chapter's spine is one algorithmic idea — **augment until stuck, then read the stuck state as a certificate** — and a family of theorems that all say the same thing: the best you can do equals the least you must pay.*

## How to read this chapter

Read it slowly, with a pencil. The problems look like personnel work — marry applicants to positions, send each committee its own delegate, push freight through a network — but they are secretly *accounting* problems. The proofs here rarely construct anything directly; instead they push a procedure until it can no longer move, then interrogate the obstruction. The obstruction always turns out to be a witness that nothing better was possible. That is the aesthetic of the whole subject: **the algorithm's failure mode is the theorem's tightness.**

**Notation.** A bipartite graph has parts X (applicants) and Y (positions), edge xy meaning "x is qualified for y". A **matching** is a set of edges no two of which share a vertex; it **saturates** X if every x ∈ X is matched. N(S) is the set of neighbors of S; ν(G) is the maximum matching size, τ(G) the minimum vertex cover size, α(G) the maximum independent set size. In networks: capacities c, a flow f with value |f|, an s–t cut (S, V∖S) with capacity c(S, V∖S).

**The exercises are graded:** ●○○ *easy* (a direct application of one lecture idea), ●●○ *moderate* (two ideas, or one tricky step), ●●● *tough* (several chapter ideas combined). Hints travel with the problems; worked answers sit at the very end of the chapter. Try honestly before reading a hint. Beyond the graded set, ◆ **pattern-unknown** problems name no method and carry no hint: diagnosing which tool fits is part of the problem. And ◐ **Explorations** at the end are open-ended investigations with no single right answer — research training, not test preparation.

## The pattern table for this chapter

| Pattern | Core move | First seen |
|---------|-----------|------------|
| **P4 Induction on one side** | Marry one pair (or peel one layer), reduce | L1.1 |
| **P16 Alternating paths** | Reachability from unsaturated vertices reorganizes the whole graph | L2.1 |
| **P17 Duality (min–max)** | Two differently-flavored quantities secretly coincide | L2, L3 |
| **P18 Algorithmic proof** | Augment until stuck; "stuck" produces a certificate | L2.1, L4.1 |
| **P2 Double counting** | The weak inequality is free; equality is the theorem | L2.1 |
| **P11 Padding construction** | Add dummies to force a hypothesis, then delete them | L1.2 |

---

## Lecture 1 · The Matchmaker's Theorem

A matchmaker has applicants X and positions Y. Each applicant is qualified for some subset of the positions. She wants to place **everyone** — each applicant in a distinct position they are qualified for. When can she?

The obvious obstruction: if k applicants are jointly qualified for fewer than k positions, they cannot all be placed — k people cannot sit in fewer than k chairs. Call S ⊆ X any set of applicants and N(S) the positions they are collectively qualified for. The obstruction says: some S with |N(S)| < |S|. **Hall's Marriage Theorem** (1935) says this obvious obstruction is the *only* one:

**Theorem.** A matching saturating X exists **if and only if** every S ⊆ X has |N(S)| ≥ |S|.

The necessity direction is the observation above (a matching pairs S into distinct members of N(S)). The miracle is sufficiency — and the proof below is worth memorizing not for the theorem but for the *architecture*: it is the master example of an induction that would naively die, and is saved by splitting into regimes.

### 1.1 The induction that almost works — and its two rescue regimes

Try induction on |X| the naive way: marry one applicant x to one position y, delete both, and appeal to induction on the rest. The catch: deleting y may *wound* someone else. Applicant x' might have been qualified only for y; the reduced graph no longer satisfies Hall's condition, and the induction hypothesis refuses to load.

✎ **Checkpoint.** Before reading on: find a tiny example where marrying x to y ruins the Hall condition for the survivors. (One applicant qualified only for y does it.) Then ask: what extra property would make the greedy marriage safe?

There are exactly two ways the greedy step can be safe, and together they cover everything.

**Regime 1 — slack everywhere.** Suppose every nonempty proper S ⊊ X has |N(S)| ≥ |S| + 1: there is a spare position in every neighborhood. Marry x to **any** neighbor y. For T ⊆ X − {x}, its neighborhood in the reduced graph is N(T) − {y} at worst: |N′(T)| ≥ |N(T)| − 1 ≥ |T| + 1 − 1 = |T|. Hall survives the deletion; induction finishes. ✓

**Regime 2 — a tight set exists.** Suppose some nonempty proper S has |N(S)| = |S| exactly — a perfectly tight block of applicants and positions. Then split the problem in two, and note that *the split is clean*:
- Match S into N(S) by induction. Hall's condition holds inside: for T ⊆ S, its neighborhood within N(S) is N(T) itself (T ⊆ S forces N(T) ⊆ N(S)), so |N(T) ∩ N(S)| = |N(T)| ≥ |T|. ✓
- Match X − S into Y − N(S) by induction. For T ⊆ X − S, use Hall for T ∪ S in the **original** graph: the neighbors of T outside N(S) number at least |N(T ∪ S)| − |N(S)| ≥ |T ∪ S| − |S| = |T|. ✓
- The two matchings use disjoint vertices (S ∪ N(S) versus its complement); their union saturates X. ∎

If neither regime holds — no nonempty proper S is tight and none has slack — the case cannot actually occur: Hall's inequalities are integer-valued, so for every nonempty proper S with |N(S)| ≥ |S|, exactly one of |N(S)| ≥ |S| + 1 (slack, Regime 1) or |N(S)| = |S| (tight, Regime 2) holds. The two regimes exhaust all cases (with |X| ≤ 1 as the trivial base). **Hall's theorem is proved.** (Pattern **P4**: the critical-set split — *tight somewhere ⇒ solve both halves recursively; slack everywhere ⇒ greed is safe* — reappears in matroid theory, in the Gallai–Edmonds structure theorem, and wherever a min–max theorem hides inside an induction.)

### 1.2 The deficiency form — how many *can* you place?

Hall is all-or-nothing. The refined question: if Hall fails, how many applicants can still be placed? Define the **deficiency** of S as |S| − |N(S)| and let d = max over all S of the deficiency (at least 0, achieved by S = ∅).

**Theorem (deficiency form).** The maximum number of X-vertices that can be simultaneously matched is exactly |X| − d.

*Two directions, and the hard one is sneaky-easy.* **No matching beats |X| − d:** take S* with deficiency d. Any matching places the members of S* into distinct members of N(S*) — at most |N(S*)| = |S*| − d of them — so at least d applicants of S* go unplaced. **Some matching achieves |X| − d:** add d **dummy positions**, each acceptable to *every* applicant. The padded graph satisfies Hall: for any S ⊆ X, its padded neighborhood has size |N(S)| + d ≥ |N(S)| + (|S| − |N(S)|) = |S|, since S's deficiency never exceeds d. So Hall places all of X; at most d of the placements use dummies (there are only d of them); the remaining ≥ |X| − d placements are real. Delete the dummy edges. ∎ (Pattern **P11** in a new costume: *when a hypothesis fails by d, pad with d universal options and it holds*.)

Check it on the lab's E2 (four applicants: x0 and x1 are both qualified only for y0; x2 is qualified only for y1; and x3 is qualified for nothing). The worst set is S* = {x0, x1, x3}: three applicants, one position — deficiency 2. The theorem promises |X| − d = 4 − 2 = **2**, and indeed a maximum matching marries two applicants (x1–y0, x2–y1, say). The lab confirms this by brute force.

**What you now own:** the two-regime induction (P4), the deficiency form and its padding proof (P11), and the reflex of asking *how far* a theorem's hypothesis can bend before it snaps.

---

## Lecture 2 · A Theorem You Can Run

Hall tells you *when* everyone can be placed. This lecture's theorem tells you the exact size of the best partial placement — and its proof is a machine: run the machine, and the machine's stopping point *is* the tightness witness.

**König–Egerváry Theorem** (1931). In a bipartite graph, the maximum matching size ν equals the minimum vertex cover size τ. (A **vertex cover** is a set of vertices touching every edge.)

### 2.1 The free inequality, then the engine

First the direction that costs nothing: **τ ≥ ν.** Take a minimum cover C and any matching M. The edges of M share no vertices, so each one needs its own member of C: an injection from M-edges into C. Counting the same world two ways (P2) gives |M| ≤ |C| for *every* matching and *every* cover. Equality is the theorem — and equality is where the work is.

Now the engine (**P16 + P18**). Take any matching M — we will improve it until it cannot be improved. Call an X-vertex **free** if M leaves it unmatched. An **M-alternating path** starts at a free X-vertex and alternates edges not-in-M, in-M, not-in-M, … Let Z be everything reachable from the free X-vertices by alternating paths. Two outcomes:

- **A free Y-vertex is reachable.** Then the alternating path to it has one more non-matching edge than matching edges: flip the path (non-M edges become M-edges and vice versa). The matching grows by exactly one edge. **Augment.** Repeat.
- **No free Y-vertex is reachable.** Then M is maximum, and Z is about to pay us for the trip. Define

**C = (X ∖ Z) ∪ (Y ∩ Z)**

and claim: *C is a vertex cover with |C| = |M|.* If true, we have exhibited a cover of the matching's size — the free inequality then forces ν = τ and certifies that M was maximum. Three verifications, each a line:

*Cover.* Could an edge xy go from x ∈ X ∩ Z to y ∈ Y ∖ Z? If xy ∈ M, then x (being matched and in Z) entered Z via the matching edge yx from y ∈ Z — contradicting y ∉ Z; if xy ∉ M, the path reaching x ends with a matching edge or has length 0, so x can traverse the non-matching edge xy, putting y in Z — contradiction again. Thus every edge either has its X-end in X ∖ Z ⊆ C, or crosses from X ∩ Z into Y ∩ Z ⊆ C and is covered by its Y-end. ✓

*Parity of the matching.* Every M-edge has exactly one end in C. Its Y-end y enters Z only via a non-matching edge; if y ∈ Z, the alternating rule immediately pulls y's partner x into Z — so y ∈ Z forces x ∈ Z. Conversely if x ∈ Z is matched, x entered Z via its matching edge from y — so x ∈ Z forces y ∈ Z. Matched pairs stand or fall **together** in Z; C keeps exactly one of each pair (X ∖ Z keeps x when both fall in Z; Y ∩ Z keeps y when both stay out). ✓

*Size.* Every C-vertex is matched: X ∖ Z contains no free vertex (free X-vertices all start in Z), and a Y-vertex of Z sits at the end of an alternating path from a free X-vertex — if it were unmatched, that path would be augmenting, and we are in the "stuck" case. Since each matched pair contributes exactly one C-vertex and matching pairs are disjoint, |C| = |M|. ✓

The machine halts (each augmentation grows |M|, which is bounded), and on halting it prints the cover C. **ν = τ, proved by an algorithm whose failure mode is the tightness certificate.** This is pattern **P18** in its purest form, and it is *constructive in both directions*: the matching you cannot improve and the cover you cannot shrink are the same information.

✎ **Checkpoint.** Run the engine by hand on E2 with M = {x1–y0, x2–y1}: the free applicants are x0 and x3; the alternating reachability set is Z = {x0, x3, y0, x1}; the certificate is C = (X ∖ Z) ∪ (Y ∩ Z) = {x2} ∪ {y0} = **{x2, y0}** — a cover of size 2 = |M|. The machine, run on three edges, just told you exactly which two vertices witness the optimum.

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 880 330" font-family="system-ui, -apple-system, 'Segoe UI', sans-serif">
  <rect x="0" y="0" width="880" height="330" fill="#ffffff"/>
  <text x="40" y="34" font-size="17" font-weight="700" fill="#193e5c">Figure 1 &#183; Augment-or-certify on E2: the reachable set Z and the cover C = (X&#8726;Z) &#8746; (Y&#8745;Z) (&#167;2.1)</text>
  <text x="40" y="72" font-size="13" fill="#172333" font-weight="600">the search: alternating reachability from the free applicants x0, x3</text>
  <line x1="210" y1="110" x2="430" y2="145" stroke="#64748b" stroke-width="2"/>
  <g stroke="#2563eb" stroke-width="4"><line x1="210" y1="170" x2="430" y2="145"/><line x1="210" y1="230" x2="430" y2="255"/></g>
  <line x1="249.6" y1="116.3" x2="368.4" y2="135.2" stroke="#dc2626" stroke-width="2.5" stroke-dasharray="7 5"/>
  <polygon points="368.4,135.2 359.8,138.3 361.2,129.6" fill="#dc2626"/>
  <line x1="381.6" y1="150.5" x2="262.8" y2="164" stroke="#dc2626" stroke-width="2.5" stroke-dasharray="7 5"/>
  <polygon points="262.8,164 270.3,158.7 271.2,167.5" fill="#dc2626"/>
  <circle cx="210" cy="110" r="13" fill="#dbeafe" stroke="#2563eb" stroke-width="2.5"/>
  <text x="210" y="114.5" font-size="13" font-weight="700" fill="#172333" text-anchor="middle">x0</text>
  <circle cx="210" cy="170" r="13" fill="#dbeafe" stroke="#2563eb" stroke-width="2.5"/>
  <text x="210" y="174.5" font-size="13" font-weight="700" fill="#172333" text-anchor="middle">x1</text>
  <circle cx="210" cy="230" r="13" fill="#ffffff" stroke="#193e5c" stroke-width="2.5"/>
  <text x="210" y="234.5" font-size="13" font-weight="700" fill="#172333" text-anchor="middle">x2</text>
  <circle cx="210" cy="290" r="13" fill="#dbeafe" stroke="#2563eb" stroke-width="2.5"/>
  <text x="210" y="294.5" font-size="13" font-weight="700" fill="#172333" text-anchor="middle">x3</text>
  <circle cx="430" cy="145" r="13" fill="#dbeafe" stroke="#2563eb" stroke-width="2.5"/>
  <text x="430" y="149.5" font-size="13" font-weight="700" fill="#172333" text-anchor="middle">y0</text>
  <circle cx="430" cy="255" r="13" fill="#ffffff" stroke="#193e5c" stroke-width="2.5"/>
  <text x="430" y="259.5" font-size="13" font-weight="700" fill="#172333" text-anchor="middle">y1</text>
  <text x="40" y="115" font-size="12" fill="#64748b">X (applicants)</text>
  <text x="40" y="295" font-size="12" fill="#64748b">free: x0, x3</text>
  <text x="445" y="150" font-size="12" fill="#64748b">Y (positions)</text>
  <text x="470" y="72" font-size="13" fill="#172333" font-weight="600">the certificate: C = (X&#8726;Z) &#8746; (Y&#8745;Z) = {x2} &#8746; {y0}, size 2 = |M|</text>
  <line x1="650" y1="110" x2="850" y2="145" stroke="#64748b" stroke-width="2"/>
  <g stroke="#2563eb" stroke-width="4"><line x1="650" y1="170" x2="850" y2="145"/><line x1="650" y1="230" x2="850" y2="255"/></g>
  <circle cx="814" cy="138.7" r="4.5" fill="#dc2626"/>
  <circle cx="814" cy="149.5" r="4.5" fill="#dc2626"/>
  <circle cx="686" cy="234.5" r="4.5" fill="#dc2626"/>
  <circle cx="650" cy="230" r="19" fill="none" stroke="#dc2626" stroke-width="3"/>
  <circle cx="850" cy="145" r="19" fill="none" stroke="#dc2626" stroke-width="3"/>
  <circle cx="650" cy="110" r="13" fill="#dbeafe" stroke="#2563eb" stroke-width="2.5"/>
  <text x="650" y="114.5" font-size="13" font-weight="700" fill="#172333" text-anchor="middle">x0</text>
  <circle cx="650" cy="170" r="13" fill="#dbeafe" stroke="#2563eb" stroke-width="2.5"/>
  <text x="650" y="174.5" font-size="13" font-weight="700" fill="#172333" text-anchor="middle">x1</text>
  <circle cx="650" cy="230" r="13" fill="#ffffff" stroke="#193e5c" stroke-width="2.5"/>
  <text x="650" y="234.5" font-size="13" font-weight="700" fill="#172333" text-anchor="middle">x2</text>
  <circle cx="650" cy="290" r="13" fill="#dbeafe" stroke="#2563eb" stroke-width="2.5"/>
  <text x="650" y="294.5" font-size="13" font-weight="700" fill="#172333" text-anchor="middle">x3</text>
  <circle cx="850" cy="145" r="13" fill="#dbeafe" stroke="#2563eb" stroke-width="2.5"/>
  <text x="850" y="149.5" font-size="13" font-weight="700" fill="#172333" text-anchor="middle">y0</text>
  <circle cx="850" cy="255" r="13" fill="#ffffff" stroke="#193e5c" stroke-width="2.5"/>
  <text x="850" y="259.5" font-size="13" font-weight="700" fill="#172333" text-anchor="middle">y1</text>
  <text x="620" y="240" font-size="12" fill="#dc2626" text-anchor="end">ringed: in C</text>
  <text x="40" y="312" font-size="12" fill="#64748b">Blue tint = Z = {x0, x3, y0, x1}, reached from the free applicants; red dashes = the alternating walk (out on a non-matching edge, back on a matching one).</text>
  <text x="470" y="312" font-size="12" fill="#64748b">C keeps the X-vertices outside Z and the Y-vertices inside it; the ringed vertices cover every edge. Stuck search &#8594; C, |C| = |M|: K&#246;nig.</text>
</svg>
```

**A remark for later.** The set C came in a strange dress: X-vertices *outside* the reachable set, Y-vertices *inside* it. File that shape; Lecture 3 will produce the same cover by pure thought, and Lecture 4 will produce it as a *cut*. Three costumes, one theorem — that is the next lecture's whole point.

**What you now own:** alternating reachability (P16), augment-or-certify (P18), the free-inequality reflex (P2), and the shape (X∖Z) ∪ (Y∩Z).

---

## Lecture 3 · Three Costumes, One Theorem

Sit back from the proofs and look at what was actually proved. Three theorems that look like different subjects:

| Costume | Quantity maximized | Quantity minimized | Weak inequality |
|---------|--------------------|-------------------|-----------------|
| **Hall** (L1) | applicants placed ν_X | deficiency d | any deficient set blocks ≥ d placements |
| **König** (L2) | matching size ν | cover size τ | τ ≥ ν is a line |
| **Max-flow** (L4) | flow value | s–t cut capacity | value ≤ every cut's capacity |

In the König and max-flow rows the two quantities are equal; in the Hall row they *sum* — placed + deficiency = |X|, i.e. ν_X = |X| − d, which is exactly the deficiency form of L1.2 — and each row is *equivalent* to the other rows. This is pattern **P17** at full power: whenever you suspect a min–max theorem, first secure the trivial weak inequality, then hunt the alternating-path (or reachability) certificate for equality. The certificate is never far from the greedy procedure's stuck state.

Let us close the dictionary explicitly, because the translations are theorems in their own right.

### 3.1 König ⇒ Hall

Assume König. Given Hall's condition, show τ ≥ |X|: then ν ≥ |X| means a matching saturating X exists. Take any vertex cover C and let S = X ∖ C. Every edge from S must be covered by its Y-end, so N(S) ⊆ C ∩ Y: |C ∩ Y| ≥ |N(S)| ≥ |S| = |X| − |C ∩ X|. Rearranged, |C| = |C ∩ X| + |C ∩ Y| ≥ |X|. Every cover has size ≥ |X|, so ν = τ ≥ |X|: a maximum matching saturates X. ∎

### 3.2 Hall ⇒ König

Assume Hall — hence (by L1.2's padding proof, which used nothing but Hall) the deficiency form. Let d be the maximum deficiency and S* a worst set; the deficiency form gives ν = |X| − d. Now build a cover of exactly that size:

**C = (X ∖ S*) ∪ N(S*)**.

It covers every edge (edges out of S* land in N(S*); every other edge is covered by its X-end), and |C| = |X| − |S*| + |N(S*)| = |X| − d = ν. With the free inequality τ ≥ ν, this cover is minimum: τ = ν. ∎

Look at the shape of C once more: X-vertices *outside* a special set, Y-vertices *inside* its neighborhood. It is the (X∖Z) ∪ (Y∩Z) of Lecture 2 with Z replaced by S* — the same cover wearing its static (worst-set) and dynamic (reachable-set) costumes. When two proofs of one fact produce the same object by different routes, you have found the theorem's true face.

### 3.3 What the dictionary cannot do

The honest frontier. Hall and König live in bipartite graphs because alternating paths there have a rigid side-structure. In a general graph, an alternating path can wander back to its own side — an odd cycle — and the Lecture-2 *search* stalls: the parity-labeled alternating walk can report "no augmenting path" while one exists. It is worth being precise about what does and does not survive the crossing. **Berge's lemma** (all graphs): a matching M is maximum **if and only if** no M-augmenting path exists — bipartiteness plays no role. (If a larger matching M′ exists, the components of M △ M′ are alternating cycles and alternating paths; since |M′| > |M|, some path component carries one more M′-edge than M-edge — and that is an M-augmenting path.) What genuinely fails beyond bipartite graphs is the *bookkeeping*: a search that permanently labels vertices "X-side" or "Y-side" can miss an augmenting path hiding behind an odd alternating cycle, and then falsely reports failure. The repairs exist and are deep:

- **Tutte's theorem** (1947, statement): G has a perfect matching iff for every U ⊆ V, the number of odd components of G − U is at most |U|.
- **Edmonds' blossom algorithm** (1965, statement): contract odd alternating cycles ("blossoms") and the alternating-path engine works again — the first polynomial-time matching algorithm and the birth of polyhedral combinatorics.

Both are beyond this chapter's scope; the ◐ exploration at the end sends you to the exact wall the bipartite proofs lean on.

**What you now own:** the dictionary (Hall ⇄ König ⇄ max-flow), the two translation proofs, and a named reason the bipartite world is special.

---

## Lecture 4 · The Freeway Theorem

Now the third costume in full: flows. A network is a directed graph with a source s, a sink t, and a capacity c(e) ≥ 0 on each edge. A **flow** assigns each edge a value f(e) with **0 ≤ f(e) ≤ c(e)** so that at every vertex except s and t, inflow = outflow (**conservation**). Its **value** |f| is the net flow leaving s. An **s–t cut** is a partition (S, V∖S) with s ∈ S, t ∉ S; its capacity is the total capacity of edges from S to V∖S.

**Max-flow min-cut theorem.** The maximum flow value equals the minimum cut capacity.

### 4.1 The free inequality, then the engine

**Value ≤ every cut's capacity.** By conservation, the value of f equals the net flow across any s–t cut: |f| = Σ_{u∈S, v∉S} f(u,v) − Σ_{u∉S, v∈S} f(u,v) (telescope the vertex-by-vertex conservation over S — P2 again). The first sum is at most the cut's capacity; the second is *subtracted*, and it is ≥ 0 since f ≥ 0. So |f| ≤ c(S, V∖S). ∎ Equality for *some* flow and *some* cut simultaneously is the theorem.

The engine (P18, third appearance): push flow greedily along s–t paths that still have room, and when no path has room, the **stuck state is the minimum cut**. To say "room" properly, work in the **residual network**: for each edge u→v with capacity c and current flow f, the residual capacity forward is c − f, and — this is the twist that makes everything work — the residual capacity of the *reverse* edge v→u is f (pushing flow backward is how the algorithm *changes its mind*, rerouting earlier greedy choices). If the residual network has an s–t path, push its bottleneck amount (the minimum residual capacity along it): the flow value rises. If it has none:

**Stuck ⇒ the reachable set is a saturated cut.** Let Z be the residual-reachable vertices from s; t ∉ Z. Every edge u→v from Z to V∖Z has residual 0 (else v would be reachable): f(u,v) = c(u,v) — *saturated*. And every edge v→u from V∖Z into Z carries f(v,u) = 0: if it carried flow, the residual reverse edge u→v would have positive capacity and pull v into Z. So in the net-flow-across-the-cut formula, the first sum is the full cut capacity and the second sum vanishes: **|f| = c(Z, V∖Z)**. The stuck flow equals the cut it exposes; the free inequality says nothing beats that cut and no flow beats this one. Both are optimal. ∎

**Termination, honestly.** With *integer* capacities, each augmentation pushes at least 1 (the bottleneck is a positive integer, and residuals stay integers), and the value is bounded above by, say, the capacity of the cut {s} alone. So the engine halts after finitely many augmentations — ≤ the min-cut value of them, in fact. With arbitrary real capacities the greedy engine can chase an infinite sequence of shrinking bottlenecks and never finish (a famous four-vertex example with capacities built from the golden ratio does exactly that — a literature landmark, stated here without proof). The **Edmonds–Karp** refinement — always augment along a *shortest* residual path — terminates in polynomial time for all capacities (statement). The lab runs the greedy engine and counts its augmentations: on small networks it stops in 2–3 rounds.

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 880 350" font-family="system-ui, -apple-system, 'Segoe UI', sans-serif">
  <rect x="0" y="0" width="880" height="350" fill="#ffffff"/>
  <text x="40" y="34" font-size="17" font-weight="700" fill="#193e5c">Figure 2 &#183; The right to un-decide: an augmenting path that cancels an earlier flow (&#167;4.1)</text>
  <text x="40" y="72" font-size="13" fill="#172333" font-weight="600">round 1 &#8212; greedy: push 1 along s &#8594; a &#8594; b &#8594; t (value 1)</text>
  <line x1="130" y1="170" x2="280" y2="95" stroke="#2563eb" stroke-width="4"/>
  <polygon points="262,104 257.5,110.6 254,103.7" fill="#2563eb"/>
  <line x1="280" y1="95" x2="280" y2="245" stroke="#2563eb" stroke-width="4"/>
  <polygon points="280,227 276.2,220 283.9,220" fill="#2563eb"/>
  <line x1="280" y1="245" x2="430" y2="170" stroke="#2563eb" stroke-width="4"/>
  <polygon points="412,179 407.5,185.6 404,178.7" fill="#2563eb"/>
  <line x1="130" y1="170" x2="280" y2="245" stroke="#94a3b8" stroke-width="2"/>
  <polygon points="262,236 255.2,236.3 258.1,230.4" fill="#94a3b8"/>
  <line x1="280" y1="95" x2="430" y2="170" stroke="#94a3b8" stroke-width="2"/>
  <polygon points="412,161 405.2,161.3 408.1,155.4" fill="#94a3b8"/>
  <text x="199.2" y="124.9" font-size="12" fill="#172333" text-anchor="middle">1</text>
  <text x="199.2" y="223.1" font-size="12" fill="#172333" text-anchor="middle">1</text>
  <text x="267" y="174" font-size="12" fill="#172333" text-anchor="middle">1</text>
  <text x="360.8" y="124.9" font-size="12" fill="#172333" text-anchor="middle">1</text>
  <text x="360.8" y="223.1" font-size="12" fill="#172333" text-anchor="middle">1</text>
  <circle cx="130" cy="170" r="13" fill="#ffffff" stroke="#193e5c" stroke-width="2.5"/>
  <text x="130" y="174.5" font-size="14" font-weight="700" fill="#172333" text-anchor="middle">s</text>
  <circle cx="280" cy="95" r="13" fill="#ffffff" stroke="#193e5c" stroke-width="2.5"/>
  <text x="280" y="99.5" font-size="14" font-weight="700" fill="#172333" text-anchor="middle">a</text>
  <circle cx="280" cy="245" r="13" fill="#ffffff" stroke="#193e5c" stroke-width="2.5"/>
  <text x="280" y="249.5" font-size="14" font-weight="700" fill="#172333" text-anchor="middle">b</text>
  <circle cx="430" cy="170" r="13" fill="#ffffff" stroke="#193e5c" stroke-width="2.5"/>
  <text x="430" y="174.5" font-size="14" font-weight="700" fill="#172333" text-anchor="middle">t</text>
  <text x="40" y="318" font-size="12" fill="#64748b">All capacities 1. Round 1 saturates s&#8594;a, a&#8594;b and b&#8594;t; the direct edges s&#8594;b and a&#8594;t still have room.</text>
  <text x="470" y="72" font-size="13" fill="#172333" font-weight="600">round 2 &#8212; the only residual s&#8211;t path: s &#8594; b &#8594; a &#8594; t, undoing a&#8594;b</text>
  <line x1="540" y1="170" x2="690" y2="95" stroke="#64748b" stroke-width="2.5"/>
  <polygon points="672,104 668.1,109.6 665.2,103.7" fill="#64748b"/>
  <text x="609.2" y="124.9" font-size="12" fill="#64748b" text-anchor="middle">f = 1</text>
  <line x1="690" y1="245" x2="840" y2="170" stroke="#64748b" stroke-width="2.5"/>
  <polygon points="822,179 818.1,184.6 815.2,178.7" fill="#64748b"/>
  <text x="770.8" y="223.1" font-size="12" fill="#64748b" text-anchor="middle">f = 1</text>
  <line x1="690" y1="95" x2="690" y2="245" stroke="#94a3b8" stroke-width="1.5"/>
  <polygon points="690,227 687.3,222 692.8,222" fill="#94a3b8"/>
  <text x="675" y="174" font-size="12" fill="#94a3b8" text-anchor="end">a&#8594;b: 1 &#8594; 0</text>
  <line x1="690" y1="245" x2="690" y2="95" stroke="#dc2626" stroke-width="3" stroke-dasharray="7 5"/>
  <polygon points="690,113 694.4,121 685.6,121" fill="#dc2626"/>
  <line x1="540" y1="170" x2="690" y2="245" stroke="#2563eb" stroke-width="4"/>
  <polygon points="672,236 664,236.3 667.5,229.4" fill="#2563eb"/>
  <line x1="690" y1="95" x2="840" y2="170" stroke="#2563eb" stroke-width="4"/>
  <polygon points="822,161 814,161.3 817.5,154.4" fill="#2563eb"/>
  <text x="609.2" y="223.1" font-size="12" fill="#2563eb" text-anchor="middle">room 1</text>
  <text x="770.8" y="124.9" font-size="12" fill="#2563eb" text-anchor="middle">room 1</text>
  <circle cx="540" cy="170" r="13" fill="#ffffff" stroke="#193e5c" stroke-width="2.5"/>
  <text x="540" y="174.5" font-size="14" font-weight="700" fill="#172333" text-anchor="middle">s</text>
  <circle cx="690" cy="95" r="13" fill="#ffffff" stroke="#193e5c" stroke-width="2.5"/>
  <text x="690" y="99.5" font-size="14" font-weight="700" fill="#172333" text-anchor="middle">a</text>
  <circle cx="690" cy="245" r="13" fill="#ffffff" stroke="#193e5c" stroke-width="2.5"/>
  <text x="690" y="249.5" font-size="14" font-weight="700" fill="#172333" text-anchor="middle">b</text>
  <circle cx="840" cy="170" r="13" fill="#ffffff" stroke="#193e5c" stroke-width="2.5"/>
  <text x="840" y="174.5" font-size="14" font-weight="700" fill="#172333" text-anchor="middle">t</text>
  <text x="470" y="318" font-size="12" fill="#64748b">The red hop is the reverse edge of a&#8594;b (capacity = its flow, the refund). Pushing 1 along the path takes a&#8594;b back to 0;</text>
  <text x="470" y="334" font-size="12" fill="#64748b">a now ships straight to t and b keeps its own outlet: value 2 = the cut {s}. The greedy choice was undone, not regretted.</text>
  <text x="40" y="334" font-size="12" fill="#94a3b8">(Exercise 12(b): a shortest-first order &#8212; s&#8594;a&#8594;t first &#8212; never touches the middle edge.)</text>
</svg>
```

**Integrality, and König falls out.** Integer capacities ⇒ the final flow is integral (it was built by integer pushes). Specialize: bipartite G, capacity 1 on every s→x and every y→t edge, capacity ∞ on every x→y edge. Integral flows ↔ matchings (each x receives ≤ 1 from s, each y ships ≤ 1 to t, so the x→y edges used form a matching; value = size). Finite cuts ↔ vertex covers: for a cut (S, V∖S) of finite capacity, no ∞ edge x→y can cross from S to V∖S, so every edge xy either has x ∉ S (paying 1 for s→x) or y ∈ S (paying 1 for y→t). Thus C = (X∖S) ∪ (Y∩S) is a vertex cover of size at most the cut capacity, and conversely any vertex cover C defines the cut S = {s} ∪ (X∖C) ∪ (Y∩C) of capacity exactly |C|. Max-flow min-cut *is* König–Egerváry, and Hall follows by L3.1. The dictionary closes. ∎

✎ **Checkpoint.** The lab's network N1 is a diamond: s → a (3), s → b (2), a → b (1), a → t (2), b → t (3). Predict the min cut before running: there are four cuts to price — {s}, {s,a}, {s,b}, {s,a,b}. The lab says the value is 5; find all three cuts that achieve it.

**What you now own:** residual thinking (the right to *un-decide*), stuck-state certificates, integrality by construction, and the flow compiler — the reflex of writing a small network first whenever a matching, covering, or dispatch question appears.

---

## Lecture 5 · Delegates, Dispatchers, and the Flow Compiler

The machinery is built; this lecture cashes it in across three classic applications — and states honestly where the open problems begin.

### 5.1 Committees and delegates: SDR

n committees, each a subset A_i of a pool of people; each committee must send **its own** delegate, and no person delegates twice. A **system of distinct representatives** (SDR) is exactly a matching saturating the index side of the bipartite graph i ↔ (people in A_i). Hall translates verbatim:

**Theorem.** An SDR exists iff every subcollection of the committees has a union at least as large as the subcollection itself.

*Warm-up, by hand:* committees {a,b}, {b,c}, {a,c} — every pair's union has size 3 ≥ 2, the triple's union has 3 ≥ 3; an SDR exists: a, b, c respectively. *Failure, by hand:* four committees all equal to {a,b}: the full collection has union 2 < 4 — no SDR, and at most two committees can be served (L1.2's deficiency form says exactly two, d = 4 − 2).

This innocuous translation is load-bearing: **Latin squares** are built row by row out of SDRs (the ◆ exercise 13 asks you to prove it), and **Dilworth's theorem** for partially ordered sets is König in a mirror (exercise 11).

### 5.2 Schedules: k-regular bipartite graphs decompose

A **k-regular bipartite graph** — equivalently, a 0-1 matrix with exactly k ones in every row and every column — models a schedule between two equal-sized sets in which every vertex has exactly k commitments. Such a graph splits into k perfect matchings:

**Theorem.** Every k-regular bipartite graph is the disjoint union of k perfect matchings.

*Proof.* For k = 0 there is nothing to decompose, so assume k ≥ 1. A k-regular bipartite graph satisfies Hall by double counting (P2): k|S| edges leave S, each Y-vertex absorbs at most k of them, so |N(S)| ≥ |S|; and k|X| = k|Y| — divide by k ≥ 1 — gives |X| = |Y|, so Hall's matching saturates both sides — a **perfect matching**. Delete it: the remainder is (k−1)-regular. Induct on k (P4). ∎

Three lines, and every scheduling problem that reduces to "k ones per row and column" falls with it — exam timetables, round robins, parallel-processor assignment. The lab's cousin verification enumerated every k-regular bipartite graph on small sides and split each into k perfect matchings, zero failures.

### 5.3 Where the frontier begins

Two statements to carry as flags, honestly labeled:

- **Dilworth's theorem** (1950, proved in the exercise): in a finite poset, the maximum antichain equals the minimum chain cover. It is König's theorem on the "comparability split graph" — exercise 11 builds the translation.
- **Menger's theorem** (1927, exercised): the maximum number of internally vertex-disjoint s–t paths equals the minimum s–t vertex separator. It is max-flow min-cut with vertices split into in/out copies of unit capacity — exercise 9.

And one genuinely open problem, stated so you know the ground is not all paved: a full **transversal** of a Latin square — n cells, no two in one row or column, holding all n symbols — need not exist (already at order 2 both squares fail: each diagonal repeats a symbol), so the honest question is partial. The **Brualdi–Stein conjecture** — the standing form — asks whether every Latin square of order n has a *partial* transversal of size at least n − 1 (n − 1 cells in distinct rows, distinct columns, holding distinct symbols); even this is open in general. The SDR pattern you just learned is the engine of every partial result.

**The flow compiler, stated as a reflex.** When a problem says *matching, covering, dispatch, scheduling, representatives, disjoint paths* — write the small network first. Hall, König, Menger, Dilworth, and the k-regular decomposition are each one network away; the art is choosing vertices and capacities so that *conservation means what you want it to mean*.

**What you now own:** SDR as matching-in-disguise, the k-regular decomposition and its double-counting seed, the Dilworth/Menger flags, and the compiler reflex.

---

## The Trick Bag (reference card)

| Pattern | Plain language | Where you met it |
|---------|---------------|------------------|
| **P4 Critical-set split** | Slack everywhere ⇒ greed is safe; tight set ⇒ split and recurse | L1.1, L5.2 |
| **P11 Padding** | Hypothesis fails by d ⇒ add d universal options, apply, delete | L1.2 |
| **P16 Alternating paths** | Reachability from unsaturated vertices reorganizes the graph | L2.1 |
| **P18 Augment-or-certify** | Improve until stuck; the stuck state *is* the tightness witness | L2.1, L4.1 |
| **P2 Free inequality** | Count two ways: cover ≥ matching, cut ≥ flow; equality is the theorem | L2.1, L4.1 |
| **P17 Duality dictionary** | Hall ⇄ König ⇄ max-flow; translate before you re-prove | L3 |
| **Residual thinking (lore)** | The right to un-decide: reverse edges carry "refund" capacity | L4.1 |
| **The flow compiler (lore)** | Matching/covering/dispatch question ⇒ write the network first | L4, L5 |

**Formula box:** Hall: saturating matching ⇔ |N(S)| ≥ |S| for all S. Deficiency form: max matchable = |X| − max_S(|S| − |N(S)|). König: ν = τ in bipartite graphs; corollaries α = n − ν and min edge cover = n − ν (no isolated vertices). k-regular bipartite ⇒ k disjoint perfect matchings. Max-flow = min-cut; integer capacities ⇒ integral optimum. Dilworth: max antichain = min chain cover. Menger: max internally-disjoint s–t paths = min s–t separator (s, t distinct and nonadjacent).

---

## Exercises (graded: ●○○ easy · ●●○ moderate · ●●● tough)

*Hints are here; worked answers are at the end of the chapter. Try first.*

**Easy — one idea, applied directly**

1. (●○○) **Hall by hand.** Check Hall's condition on the lab's E1 (x0: {y0,y1}, x1: {y0,y1,y2}, x2: {y2,y3}, x3: {y3}) — all 15 nonempty subsets — and find a matching saturating X. *Hint: L1; the three tight subsets you should find are the checkpoints.*
2. (●○○) **Committees.** Which of these have SDRs? (a) {a,b}, {b,c}, {a,c}, {a,b,c}; (b) {a,b}, {a,b}, {a,b}; (c) {a}, {a,b}, {b,c}, {c}. *Hint: L5.1 — Hall on the committee graph; find the deficient subcollection when it fails.*
3. (●○○) **Everyone knows a position is not enough.** Show that "every applicant is qualified for at least one position" does not imply Hall's condition, and find the smallest example where it fails. What is its deficiency d, and what does the deficiency form promise? *Hint: L1.2.*
4. (●○○) **The compiler, by hand.** Build the flow network for E2 (L4's reduction: source → applicants → positions → sink, all capacities 1). Run one augmentation by hand, then read the minimum cut the stuck state exposes — which vertices does it correspond to as a *cover*? *Hint: L4.1 and the ✎ checkpoint of L2.*

**Moderate — two ideas, or one tricky step**

5. (●●○) **The deficiency form.** Prove both inequalities of L1.2's theorem yourself: no matching beats |X| − d, and padding achieves it. Where exactly does the padding proof need dummies adjacent to *all* of X? *Hint: L1.2; be careful why |N′(S)| = |N(S)| + d.*
6. (●●○) **Schedules.** Prove that every k-regular bipartite graph splits into k perfect matchings, from the double-counting seed up. Where does the proof need the graph to be *bipartite*? *Hint: L5.2; the seed is k|S| ≤ k|N(S)|.*
7. (●●○) **Two König corollaries.** Prove that in a bipartite graph on n vertices: (a) the maximum independent set has size α = n − ν; (b) if no vertex is isolated, the minimum edge cover (edges covering all vertices) has size n − ν. *Hint: L2 — a cover's complement is an independent set; for (b), build an edge cover from a maximum matching and prove optimality.*
8. (●●○) **Half is not enough.** Prove: if each of n sets has size at least n/2, an SDR of size at least ⌈n/2⌉ always exists — but an SDR of size n need not. *Hint: L1.2 — the sets' sizes are integers, so round up; bound the worst deficiency by ⌊n/2⌋ for the promise, and take all sets equal for the counterexample.*
9. (●●○) **Menger from flows.** Prove the vertex version of Menger's theorem, for distinct *nonadjacent* vertices s and t: the maximum number of internally vertex-disjoint s–t paths equals the minimum number of vertices whose deletion separates s from t. (The nonadjacency is needed as stated: if s and t are adjacent, the edge st survives the deletion of every *internal* vertex, so no deletion of internal vertices can separate them.) *Hint: P18 + L4 — split each vertex v into v_in → v_out with capacity 1 (s and t get capacity ∞), and read integral flows as paths; the unit-capacity vertices are exactly what a cut must pay for.*

**Tough — several chapter ideas combined**

10. (●●●) **The dictionary, both ways, in writing.** Prove König ⇒ Hall and Hall ⇒ König as full proofs (not citations): the first via the cover-size bound of L3.1, the second via the deficiency form and the cover (X ∖ S*) ∪ N(S*) of L3.2. Then explain in one paragraph why the two covers — (X∖Z) ∪ (Y∩Z) and (X∖S*) ∪ N(S*) — are the same shape in different clothes. *Hint: L3, all of it.*
11. (●●●) **Dilworth.** (a) Warm-up: if {a, b} is a maximum antichain of a poset, show every element is comparable to a or to b. (b) Prove Dilworth's theorem via König on the **split graph**: elements x on the left, copies x⁺ on the right, an edge x → y⁺ whenever x < y. *Hint: two constructions — a maximum matching of size m links elements into n − m chains; a minimum vertex cover C yields an antichain of size ≥ n − |C| (take elements whose *neither* copy is in C). Combine with König and the trivial bound width ≤ every chain cover.*
12. (●●●) **When does the greedy freeway engine halt?** (a) Prove: with integer capacities, the augmenting-path engine terminates, in at most (min cut value) augmentations. (b) Exhibit a network and an augmentation *order* in which the engine requires more rounds to terminate than a shortest-first order on the same network. *Hint: L4.1's termination analysis; for (b) the lab's diamond plus one cross edge is enough to see orders diverge.*

**Pattern unknown — you choose the tool** *No hints, no difficulty rating: diagnosing the problem is part of the problem. Worked answers still wait at the end.*

13. (◆) A **Latin rectangle** is an r × n array, each row a permutation of {1,…,n}, no symbol repeated in a column. Prove every Latin rectangle can be extended to a full Latin square.
14. (◆) A bipartite graph needs its edges partitioned into as few matchings as possible. Prove the answer is exactly Δ, the maximum degree — and find the engine inside this chapter.
15. (◆) A doubly stochastic matrix has nonnegative entries with every row and column summing to 1. Prove it is a convex combination of permutation matrices.

**Graded backfill — five more, each hint naming its pattern**

16. (●●○) **Mutilated chessboards.** (a) Prove that an 8×8 board with two diagonally opposite corners removed cannot be tiled by dominoes. (b) Prove the companion theorem: a rectangle with both sides at least 2 and even area, minus any ONE black and any ONE white square, can always be tiled. Where does (a)'s counting argument break down in (b)? *Hint: (a) is P2 — count the two colors. (b) is P18 — build a Hamiltonian cycle through every square (the snake: down one column, then weave back row by row), delete the two squares, and read dominoes off the two broken paths.*
17. (●●○) **Committees with quotas.** Each of n committees A_i must send **d_i** distinct delegates, and no person may serve two committees. Prove: an assignment exists if and only if for every subcollection I, the total demand Σ_{i∈I} d_i is at most the size of the union ∪_{i∈I} A_i. *Hint: P11 — clone each committee d_i times with identical membership; Hall (L5.1) does the rest. Count the necessity direction directly (P2).*
18. (●○○) **Greedy's guarantee.** Call a matching *maximal* when no further edge can be added to it. Prove, in ANY graph (not just bipartite): (a) every maximal matching M has at least ν/2 edges; (b) the endpoints of a maximal matching cover every edge, so they form a vertex cover of size at most 2τ. Compare with König's exact answer (L2–L3): what does greedy lose, and what does it keep? *Hint: P18 + P2 — maximality is the certificate: block the maximum matching's edges endpoint by endpoint, and ask what an uncovered edge would do to maximality.*
19. (●●●) **Uniquely matched, fragile.** Prove: if a bipartite graph has exactly one perfect matching M, then some edge of M is a bridge (its removal disconnects the graph). *Hint: P16 — first show an M-alternating cycle would produce a second matching; then orient every M-edge from X to Y and every other edge from Y to X, and find a sink of the orientation.*
20. (●○○) **Half the room, both sides.** Prove: a bipartite graph with |X| = |Y| = n in which EVERY vertex on BOTH sides has degree at least n/2 has a perfect matching. Compare with Exercise 8: why does the same threshold buy the full matching here, but only ⌈n/2⌉ delegates there? Then show the threshold is sharp: exhibit, for n = 4 and for n = 3, a graph with all degrees at least ⌈n/2⌉ − 1 and no perfect matching. *Hint: P2 — run Hall and split on |S| ≤ n/2 versus |S| > n/2; in the second case count the neighbors of a vertex OUTSIDE N(S).*

**Explorations — ◐ research-style training** *No single right answer — what you should find is described in each.*

X1. (◐) **Making the engine sweat.** Implement naive augmentation (any augmenting path) and Hopcroft–Karp (shortest paths, in phases). Build bipartite graphs on which naive takes Θ(n) augmentations where Hopcroft–Karp takes a handful of phases — chains of tightly-coupled pairs are the classic torture test. Measure both on random graphs and on your torture tests; record how augmentation counts and phase counts grow with n.

X2. (◐) **The wall the bipartite proofs lean on.** By Berge's lemma (L3.3) a nonmaximum matching *always* has an augmenting path — so in general graphs the danger is not that augmentation stops working, but that the *search* lies. Take the parity-labeled alternating search of Lecture 2 into general graphs. On the "paw" (a triangle with a pendant vertex) and on C₅ plus a pendant edge, start from specific small nonmaximum matchings and run the search: find a state where it reports "stuck — no augmenting path" although one exists. Pinpoint the odd alternating cycle that breaks the X-side/Y-side bookkeeping — you have found the need for **blossom contraction** (L3.3). Describe what the augmenting path "wants to do" on an odd cycle, why contraction is the repair, and confirm experimentally (brute force over the small graphs) that whenever a matching is not maximum, an augmenting path truly exists.

---

## Computational Lab (verified)

### Part 1 — Hall, matching, cover: exhaustive checks (code unchanged from the reference edition)

```python
from itertools import combinations
X = 4

def nbrs(E, S): return {y for x, y in E if x in S}

def hall_ok(E):
    for k in range(1, X + 1):
        for S in combinations(range(X), k):
            if len(nbrs(E, S)) < k: return False, S
    return True, None

def max_matching(E):                    # brute force over matchings
    best = 0
    def rec(i, used, cnt):
        nonlocal best
        if i == X: best = max(best, cnt); return
        rec(i + 1, used, cnt)          # leave x_i unmatched
        for x, y in E:
            if x == i and y not in used:
                used.add(y); rec(i + 1, used, cnt + 1); used.remove(y)
    rec(0, set(), 0)
    return best

def min_cover(E):                       # brute force over vertex subsets
    verts = list(range(8))              # x0..x3 = 0..3, y0..y3 = 4..7
    for k in range(9):
        if any(all((x in C) or (4 + y in C) for x, y in E)
               for C in combinations(verts, k)):
            return k
```

**Verified output.** E1 = {x0:{y0,y1}, x1:{y0,y1,y2}, x2:{y2,y3}, x3:{y3}}: Hall ✓ (all 15 subsets pass; the three tight ones — where |N(S)| = |S| — are {x3}, {x2,x3}, and {x0,x1,x2,x3}); maximum matching **4**; minimum cover **4** — König's equality on a saturated instance. E2 = {x0:{y0}, x1:{y0}, x2:{y1}} (x3 unqualified): Hall **fails** — the brute force returns S = {x3} first (an applicant with no positions at all), and {x0, x1} fails next (two applicants, one shared position); the worst deficiency is **2** at S = {x0, x1, x3}; maximum matching **2** = minimum cover **2**, and the deficiency form predicts |X| − d = 4 − 2 = **2** exactly. (Honest correction, recorded in the appendix: the reference edition's lab note claimed Hall "fails at S = {x0,x1}" and wrote the prediction as 3 − 1; the machine's ledger shows the first failure is the isolated applicant {x3}, the worst deficiency is 2, and the honest prediction is 4 − 2. The answer 2 was right; the bookkeeping was not.)

**What to explore:** modify `hall_ok` to return the *maximally* deficient set; count deficient sets of E2 (there are ten: eight of deficiency 1 and two of deficiency 2 — the full census is in the appendix).

### Part 2 — The flow compiler, run by hand-sized brute force

```python
def edmonds_karp(cap, s, t):
    n = len(cap)
    if n == 0 or s == t:
        return 0, 0, set(), []
    r = [row[:] for row in cap]
    flow, augs = 0, 0
    while True:
        parent = [-1] * n
        parent[s] = s
        q = [s]
        while q and parent[t] == -1:
            u = q.pop(0)
            for v in range(n):
                if parent[v] == -1 and r[u][v] > 0:
                    parent[v] = u
                    q.append(v)
        if parent[t] == -1:
            Z = {u for u in range(n) if parent[u] != -1}
            sat = [(u, v) for u in Z for v in range(n)
                   if v not in Z and cap[u][v] > 0]
            return flow, augs, Z, sat
        aug = float("inf")
        v = t
        while v != s:
            u = parent[v]
            aug = min(aug, r[u][v])
            v = u
        v = t
        while v != s:
            u = parent[v]
            r[u][v] -= aug
            r[v][u] += aug
            v = u
        flow += aug
        augs += 1

def min_cut_brute(cap, s, t):
    n = len(cap)
    if n == 0 or s == t:
        return 0, 0
    best, cuts = float("inf"), []
    for U in range(1 << n):
        if not (U >> s & 1) or (U >> t & 1):
            continue
        c = sum(cap[u][v] for u in range(n) if U >> u & 1
                          for v in range(n) if not (U >> v & 1))
        if c < best:
            best, cuts = c, [U]
        elif c == best:
            cuts.append(U)
    return best, len(cuts)

N1 = [[0, 3, 2, 0],      # s -> a (3), s -> b (2)
      [0, 0, 1, 2],      # a -> b (1), a -> t (2)
      [0, 0, 0, 3],      # b -> t (3)
      [0, 0, 0, 0]]
print("N1:", edmonds_karp(N1, 0, 3)[:2], min_cut_brute(N1, 0, 3))

N2 = [[0] * 10 for _ in range(10)]      # E2 as a network
for i in range(1, 5):
    N2[0][i] = 1                        # s -> each applicant, cap 1
for x, y in [(0, 0), (1, 0), (2, 1)]:
    N2[1 + x][5 + y] = 1                # qualification edges, cap 1
for j in range(5, 9):
    N2[j][9] = 1                        # each position -> t, cap 1
flow, augs, Z, sat = edmonds_karp(N2, 0, 9)
print("N2:", (flow, augs), min_cut_brute(N2, 0, 9)[0], "Z:", sorted(Z), "sat:", sat)
```

**Verified output.** N1 (the diamond): `(5, 3) (5, 3)` — maximum flow 5, reached in 3 augmentations, and the brute force prices the minimum cut at 5 too (three of the four cuts tie at 5; only {s, b} is worse, at 6). N2 (E2 compiled to a network): `(2, 2) 2 Z: [0, 1, 2, 4, 5] sat: [(0, 3), (5, 9)]` — flow 2 in 2 augmentations, cut 2: the network says what the matching said. The integral flow on N2 uses exactly the qualification edges of a maximum matching, and the exposed cut is the saturated pair {s → x2, y0 → t}, which reads as the vertex cover {x2, y0} — the same certificate Lecture 2's engine prints, the compiler at work. (The full census behind these numbers — every network of each topology with small integer capacities, the stuck-cut saturation property, and the augmenting-path counts — is in the appendix.)

**What to explore:** run E1 through the compiler (expect flow 4 and a cut of 4); build a network where a naive longest-path-first augmentation order takes noticeably more rounds than shortest-first; then read the Edmonds–Karp bound.

### Part 3 — Hopcroft–Karp: shortest augmenting paths, in phases

Part 2's compiler pays one full search per augmenting edge — ν searches in the worst case. **Hopcroft–Karp** (1973) batches the work: each phase runs *one* BFS that layers the alternating forest by distance, then one DFS sweep commits a maximal set of vertex-disjoint *shortest* augmenting paths. Each phase strictly lengthens the shortest augmenting path, and once that length passes √V, vertex-disjointness caps how many augmentations can remain — O(√V) phases in total, the engine behind the O(E√V) bound. The lab returns (ν, phases):

```python
def hopcroft_karp(adj, nX, nY):
    """One BFS per phase layers the alternating forest; the phase's
    DFS then commits a maximal set of vertex-disjoint shortest paths."""
    matchX, matchY = [-1] * nX, [-1] * nY
    dist = [-1] * nX
    dist_nil = [-1]                      # BFS level of a free Y vertex
    def dfs(u):
        if u == -1:                      # NIL reached: a free Y vertex
            return True
        need = dist[u] + 1
        for v in adj[u]:
            w = matchY[v]
            if ((dist_nil[0] if w == -1 else dist[w]) == need
                    and dfs(w)):
                matchX[u], matchY[v] = v, u
                return True
        dist[u] = -1                     # dead end: pruned for this phase
        return False
    phases = 0
    while True:
        for x in range(nX):
            dist[x] = -1
        dist_nil[0] = -1
        queue = [x for x in range(nX) if matchX[x] == -1]
        for x in queue:
            dist[x] = 0
        qi = 0
        while qi < len(queue):
            u = queue[qi]; qi += 1
            if dist_nil[0] != -1 and dist[u] >= dist_nil[0]:
                continue                 # stop layering past the free level
            for v in adj[u]:
                w = matchY[v]
                if w == -1:
                    if dist_nil[0] == -1:
                        dist_nil[0] = dist[u] + 1
                elif dist[w] == -1:
                    dist[w] = dist[u] + 1
                    queue.append(w)
        if dist_nil[0] == -1:            # stuck: the matching is maximum
            break
        phases += 1
        for x in range(nX):
            if matchX[x] == -1:
                dfs(x)
    return sum(1 for x in matchX if x != -1), phases

E1 = [[0, 1], [0, 1, 2], [2, 3], [3]]    # the chapter's own graphs
E2 = [[0], [0], [1], []]                 # x3 qualified for nothing
print(hopcroft_karp(E1, 4, 4), hopcroft_karp(E2, 4, 2))

def seeded_bipartite(n, p, seed=1):      # Lehmer LCG: x <- 48271 x mod (2^31 - 1)
    x = seed                             # fixed seed: byte-identical reruns
    adj = [[] for _ in range(n)]
    for i in range(n):
        for j in range(n):
            x = 48271 * x % 2147483647
            if x / 2147483647 < p:
                adj[i].append(j)
    return adj

for n in (30, 60, 100):
    for p in (0.2, 3 / n):
        nu, phases = hopcroft_karp(seeded_bipartite(n, p), n, n)
        print(n, round(p, 4), nu, phases, round((2 * n) ** 0.5, 2))
```

**Verified output.** `(4, 1) (2, 1)` — E1 saturates all four applicants (x0–y0, x1–y1, x2–y2, x3–y3); E2 places exactly the two its structure permits (x1 and x3 stay unplaced — no algorithm can beat the graph). One phase each: the very first layered search already sees a maximal disjoint set. The seeded instances, rebuilt from the same seed on every run, so your output matches exactly: n = 30 → `(30, 3)` at p = 0.2 and `(27, 2)` at p = 0.1; n = 60 → `(60, 2)` and `(56, 5)`; n = 100 → `(100, 2)` and `(97, 4)`.

At p = 0.2 all three instances admit perfect matchings and the engine needs 2–3 phases, n notwithstanding. The sparse regime p = 3/n is the interesting one: vertices stay exposed (ν < n) and the searches dig deeper — five phases at n = 60 — yet every count sits far below both the √V ceiling (7.75, 10.95, 14.14) and the ν single-path searches a naive engine would pay. Behind these outputs stands an exhaustive check: on *all* 74,954 bipartite graphs with |X|, |Y| ≤ 4 the engine agreed with a brute-force maximum-matching DP everywhere — zero mismatches — and the phase census ran 16 graphs at zero phases (exactly the edgeless ones), 51,657 at one, 23,179 at two, and 102 at three (appendix).

**What to explore:** wire the phase counter into X1's torture chains and watch it stay flat while naive augmentation's search count climbs; then feed Part 2's networks to both engines — same maximum, and count the difference in searches.

---

## Answers to the Exercises

*Attempt everything first — the value is in the attempt; these pages will still be here when you return.*

**A1.** The 15 nonempty subsets of X: the singletons all pass (each x has ≥ 1 neighbor). The census — {x0} → 2, {x1} → 3, {x2} → 2, {x3} → 1, {x0,x1} → 3, {x0,x2} → 4, {x0,x3} → 3, {x1,x2} → 4, {x1,x3} → 3, {x2,x3} → 2, {x0,x1,x2} → 4, {x0,x1,x3} → 4, {x0,x2,x3} → 4, {x1,x2,x3} → 4, X → 4 — has slack everywhere except the three *tight* subsets, where |N(S)| = |S| exactly: **{x3}, {x2,x3}, and X**. Hall holds. A saturating matching: x0–y0, x1–y1, x2–y2, x3–y3. Machine check: the brute force confirms Hall, matching 4, cover 4 on E1.

**A2.** All three fail Hall's condition, with maximum deficiency d = 1 in each case; the deficiency form therefore promises exactly 3, 2, and 3 committees served, respectively. (a) The full collection has union {a,b,c}, of size 3 < 4, so no SDR exists; a maximum matching serves three committees, e.g. 1 → a, 2 → b, 3 → c. (b) The full collection has union {a,b}, of size 2 < 3, so no SDR exists; at most two committees can be served. (c) The full collection has union {a,b,c}, of size 3 < 4, so no SDR exists; a maximum matching serves three committees, e.g. 1 → a, 2 → b, 4 → c. In each case no subcollection has deficiency larger than the displayed full-collection deficiency 1: singleton unions are nonempty (deficiency ≤ 0), unions of two committees have size at least 2, and unions of three have size at least 2 or 3, so |S| − |N(S)| ≤ 1 throughout. The honest lesson of this exercise: (a), (b), and (c) all fail — hand-verify with the deficiency form before trusting any "obvious" SDR. Machine check: all three compiled to bipartite graphs and brute-forced — maximum matchings 3, 2, 3 respectively, each exactly |X| − d with d = 1.

**A3.** Smallest failure: two applicants, both qualified for the same single position. X = {x0, x1}, Y = {y0}, E = {x0y0, x1y0}: every applicant is qualified for ≥ 1 position, but |N(X)| = 1 < 2 — Hall fails at S = X, deficiency d = 1; the deficiency form promises 2 − 1 = 1 placed applicant, which is exactly right. (E2's x3 is the same phenomenon wearing an isolated vertex.) Machine check: on all 512 bipartite graphs with parts 3+3, the deficiency form agrees with the brute-force maximum matching on every single one — the promise is never wrong.

**A4.** Network: s → x0..x3 (cap 1), x_i → y_j for E2's edges, y_j → t (cap 1) — the lab's convention. (The cover correspondence of L4.1 would prefer capacity ∞ — in practice anything > |X| — on the qualification edges; the *value* is unaffected either way because the source already caps each applicant at 1, but with capacity 1 a minimum cut could in principle slice a qualification edge instead of exposing a cover — a caution whenever the correspondence, not just the value, is the point.) First augmentation: s → x0 → y0 → t, pushing 1. Second: the trail s → x1 → y0 dies at the saturated y0 → t, and the residual reverse edge y0 → x0 leads nowhere new (x0 has no other outlet) — the engine instead finds s → x2 → y1 → t. Final: flow 2, 2 augmentations. The stuck state, honestly: residual reachability from s is Z = {s, x0, x1, x3, y0} — x2 is unreachable (s → x2 is saturated), and so is y1 (its only inlet x2 → y1 is saturated, and y0's reverse edges dead-end at x0). The exposed cut is the saturated pair **s → x2 and y0 → t**, capacity 1 + 1 = 2 — read as a vertex cover: **{x2, y0}**, size 2 = ν: exactly the certificate of L2's ✎ checkpoint. ({y0, y1} is also a minimum cover — but it is not the cover this particular residual network exposes.) The certificate engine of L2 and the cut engine of L4 name the same optimum.

**A5.** Upper bound: S* with |S*| − |N(S*)| = d forces ≥ d unmatched vertices in every matching (L1.2's argument verbatim). Padding: dummies z1..zd adjacent to all of X. For nonempty S: |N′(S)| = |N(S)| + d — this is where "adjacent to *all* of X" is needed: every dummy is a neighbor of every applicant, so all d dummies enter N′(S) regardless of which S we test — and then |N′(S)| ≥ |N(S)| + |S| − |N(S)| = |S| because S's deficiency is at most d. Hall holds in the padded graph; a saturating matching uses at most d dummy positions (there are only d), so ≥ |X| − d edges are real. The subtle point: the same d must dominate *every* S's deficiency at once — which is exactly why we defined d as the maximum.

**A6.** The seed: for S ⊆ X, count the edges incident to S two ways — k|S| leave S, each Y-vertex absorbs ≤ k, so |N(S)| ≥ |S| (bipartite is used here: *all* edges from S land in Y; in a general graph, edges can stay inside S and the count collapses). Regularity also forces |X| = |Y| (count all edges by the two sides and divide by k ≥ 1; the k = 0 case is the empty decomposition, nothing to prove). Hall's matching saturates X, hence all of Y: a perfect matching. Deleting it leaves (k−1)-regular; induction down to k = 0. Machine check: every k-regular bipartite graph on 3+3 (census: 6 with k = 1, 6 with k = 2, 1 with k = 3) and on 4+4 (24, 90, 24) decomposes into k perfect matchings — zero failures.

**A7.** (a) A vertex cover's complement is an independent set (an edge inside the complement would be uncovered): α = n − τ; König gives τ = ν, so α = n − ν. (b) From a maximum matching M (size ν), cover the ν matched vertices with M's own edges and each unmatched vertex with any one incident edge (no isolated vertices!): total ν + (n − 2ν) = n − ν edges — the upper bound. For the lower bound, take any edge cover F and shrink it to an inclusion-minimal one: now every component of the spanning graph (V, F) is a **star** (a single edge counts as a two-vertex star) — if a component contained a path of three edges, the middle edge's endpoints would each be covered by another of its edges and it could be dropped; if it contained a cycle, any edge could be dropped. A star forest on n vertices with c components has |F| = n − c edges, and one edge chosen from each star is a matching of size c = n − |F|. So ν ≥ n − |F|, i.e. |F| ≥ n − ν. (Bipartiteness was never used: this holds in any graph without isolated vertices.) With König available (a) stands on its own. Machine check: on all 512 (3+3) and 4096 (3+4) graphs, α = n − ν with zero violations; min edge cover = n − ν on every graph without isolated vertices, zero violations.

**A8.** Promise: set sizes are integers, so "at least n/2" forces |A_x| ≥ ⌈n/2⌉. For any nonempty S, N(S) ⊇ A_x for any x ∈ S, so |N(S)| ≥ ⌈n/2⌉ and deficiency(S) = |S| − |N(S)| ≤ |S| − ⌈n/2⌉ ≤ n − ⌈n/2⌉ = ⌊n/2⌋; the deficiency form (L1.2) then promises n − ⌊n/2⌋ = **⌈n/2⌉** committees served — for odd n the honest guarantee is (n+1)/2, not (n−1)/2. Sharpness, both parities: take all n sets identical to one fixed set of size ⌈n/2⌉ (legal: ⌈n/2⌉ ≥ n/2); the full collection's union has ⌈n/2⌉ < n elements (n ≥ 2), so at most ⌈n/2⌉ committees can be served — exactly the promise, never more. Machine check: on 3+3 graphs where every applicant has degree ≥ 2, every single one has a matching of size ≥ 2; the all-equal instances (4 sets, all {1,2}) serve exactly 2 of 4 committees and (5 sets, all {1,2,3}) exactly 3 of 5 — the bound is tight on both parities.

**A9.** Assume s and t are distinct and nonadjacent (as the exercise states; if st were an edge, it would survive the deletion of every internal vertex and no deletion could separate the pair). Replace each undirected edge by two opposite directed arcs of capacity ∞. Split every vertex v into v_in → v_out: capacity 1 for internal v, capacity ∞ for s and t; take source s_out and sink t_in (the unused copies s_in and t_out may be omitted). An integral flow of value k decomposes into k s–t paths plus cycles; discard the cycles. Since every internal gadget v_in → v_out has capacity 1, at most one path uses v, so the paths are internally vertex-disjoint. Conversely, k internally vertex-disjoint paths give an integral flow of value k. Thus max flow = max number of internally vertex-disjoint s–t paths. Now finite cuts and separators correspond. If U is a set of internal vertices whose deletion separates s from t, let R be the vertices reachable from s in G − U, and define A = {s_out} ∪ {v_in, v_out : v ∈ R} ∪ {u_in : u ∈ U and u has a neighbor in R}. No ∞ arc leaves A: from v_out with v ∈ R, an edge to w either has w ∉ U, hence w ∈ R and w_in ∈ A, or w ∈ U, hence w_in ∈ A by definition. The only arcs leaving A are u_in → u_out for u ∈ U with u_in ∈ A, so the cut has capacity at most |U|. Hence min cut ≤ min separator. Conversely, for a finite cut (A, V∖A), no ∞ arc leaves A. Put U = {v internal : v_in ∈ A, v_out ∉ A}. The cut capacity is exactly |U|, since only these unit-capacity vertex gadgets cross. If some s–t path avoided U, then along that path from s_out ∈ A to t_in ∉ A there would be a first arc leaving A; it cannot be an ∞ original arc, and it cannot be a gadget v_in → v_out with v ∉ U by definition, while v ∈ U is forbidden. So U separates s from t. Thus min separator ≤ min cut. Therefore max internally vertex-disjoint paths = max flow = min cut = min separator. ∎ Machine check: on all 1024 graphs on 5 vertices, over all 5,120 unordered (graph, non-adjacent pair) cases — 10,240 ordered — the split-network flow equaled the brute-force minimum separator every single time.

**A10.** König ⇒ Hall: for any cover C, S = X ∖ C has N(S) ⊆ C ∩ Y (edges out of S must be covered at their Y-end), so |C| ≥ |C ∩ X| + |N(S)| ≥ |C ∩ X| + |X| − |C ∩ X| = |X|; König then forces ν ≥ |X|, a saturating matching. Hall ⇒ König: the deficiency form (Hall alone, via padding) gives ν = |X| − d; the cover C = (X ∖ S*) ∪ N(S*) has size |X| − d and covers everything. The shapes rhyme: the dynamic certificate keeps X-vertices *unreachable* from the free set and Y-vertices *reachable*; the static certificate keeps X-vertices *outside the worst deficient set* and Y-vertices *inside its neighborhood*. In both, the kept Y-side is a neighborhood and the kept X-side is a complement — and in both, |C| = ν falls out of matched pairs crossing the boundary exactly once. One theorem, two shadows.

**A11.** (a) If x were comparable to neither a nor b, then x is incomparable to both members of the antichain {a, b}; since a and b are incomparable, {x, a, b} would be an antichain of size 3, contradicting maximality. Hence every element is comparable to a or to b. (b) Build the split graph: left = elements, right = copies x⁺, an edge x → y⁺ iff x < y. It is bipartite, so König applies. Let m be a maximum matching. Each matched edge x → y⁺ means x < y; each element has at most one matched successor and at most one matched predecessor. Hence the matched edges form a directed forest of paths (a directed cycle would force x₁ < x₂ < … < x₁, impossible), and a forest on n vertices with m edges has n − m components; each component is a *chain*. Thus the minimum chain cover is at most n − m. Conversely, let C be a minimum vertex cover, |C| = m by König. Put A = {x : x ∉ C and x⁺ ∉ C}. If x, y ∈ A and x < y, then the edge x → y⁺ is uncovered — contradiction; so A is an antichain. Since the m cover vertices knock out at most m elements (two copies of one element knock out only that element), |A| ≥ n − m; therefore width ≥ |A| ≥ n − m. Every chain cover has size at least width (a chain meets an antichain at most once), so min chain cover ≥ width. Combining min chain cover ≤ n − m ≤ |A| ≤ width ≤ min chain cover gives equality: width = n − m = min chain cover. ∎ Machine check: on all 219 labeled posets on 4 elements and all 4,231 on 5 (the known censuses, matched exactly), width = minimum chain cover = n − maximum split-graph matching, zero violations.

**A12.** (a) With integer capacities, every augmentation pushes the bottleneck amount — a positive integer, so at least 1 — and the flow value is bounded above by the capacity of the fixed cut ({s}, V∖{s}), namely the sum of capacities out of s. Hence the engine halts after at most that many augmentations; in particular it terminates. (b) Take the diamond-plus-cross network with capacities s → a = 2, s → b = 2, a → b = 1, a → t = 1, b → t = 2 (minimum cut 3). Shortest-first: augment s → a → t by 1, then s → b → t by 2 — value 3 in 2 augmentations. Bad order: first augment the longer path s → a → b → t by 1 (bottleneck min(2, 1, 2) = 1); this saturates a → b and leaves b → t with residual 1. Then augment s → a → t by 1, and finally s → b → t by 1 — value 3 again, but in 3 augmentations. The bad order pays an extra round because it spends b → t on a longer path and later cannot send the full s → b → t amount; the number of augmentations is order-dependent, which is exactly why Edmonds–Karp *pins* the order (shortest first) to guarantee the polynomial bound. The machine record: over 1,024 diamond-topology networks (capacities 0–3) and 6,561 layered networks (capacities 0–2), the greedy engine always matched the brute-force minimum cut, never exceeding 3 and 4 augmentations respectively — but the counts per network vary with the search order.

**A13.** The tool is Hall/SDR — but seeing it is the problem. Given an r × n Latin rectangle with r < n, extend by one row. For each column j, let A_j be the set of symbols not yet used in that column: exactly n − r of them, since the column holds r distinct symbols. Each symbol occurs exactly once in each of the r rows, hence in exactly r distinct columns — so it is missing from exactly n − r columns. Hall for the columns: take any k columns and let U be the union of their missing-symbol sets. Count the pairs (chosen column, symbol it misses): each of our k columns misses exactly n − r symbols, so there are k(n − r) pairs. Every symbol of U is missed by at most n − r columns *in the entire rectangle*, so it accounts for at most n − r of these pairs: k(n − r) ≤ |U|(n − r), and since n − r > 0, **|U| ≥ k**. Hall's condition holds, so the columns can be assigned distinct missing symbols — and that assignment *is* the next row: each column receives one new symbol, and distinctness across columns makes the row a permutation. Repeat, r → r + 1, until r = n. ∎ The double count (P2) is the entire proof — no regimes, no case split; the symmetry of "each column misses n − r, each symbol is missed by n − r" is exactly what makes Hall automatic. Machine check: every Latin rectangle with n = 3 (30, of which 12 are full squares — the known count) and n = 4 (1,392, of which 576 are full squares — the known count) extends by this procedure with Hall's condition holding at every stage, zero failures.

**A14.** The engine inside is Exercise 6's k-regular decomposition — but the graph need not be regular. Make it regular by **padding (P11)**. Suppose Δ ≥ 1 (for Δ = 0 there are no edges to color). Add isolated dummy vertices to the smaller side until both sides have the same number N of vertices; every degree stays ≤ Δ. Now give each vertex v exactly Δ − d(v) unfilled **degree slots**. The two sides own equally many unfilled slots — each side has NΔ target slots, and the m real edges fill the same number on each — so pair the left slots with the right slots arbitrarily, adding one edge per pair (parallel added edges are permitted). The result is a **Δ-regular bipartite multigraph** H containing G. Exercise 6's proof runs unchanged in a multigraph: k|S| edges leave S (counted with multiplicity), each Y-vertex absorbs at most k of them, so |N(S)| ≥ |S|; and k|X| = k|Y| with k = Δ ≥ 1 gives |X| = |Y|, so Hall's matching is **perfect**. Delete it — the remainder is (Δ−1)-regular — and repeat: peeling Δ perfect matchings partitions all of H's edges, and restricting each to G's real edges partitions E(G) into exactly Δ matchings. Δ is also necessary (the Δ edges at a vertex of degree Δ need Δ distinct matchings), so the answer is exactly Δ. ∎ Machine check: the slot-pairing construction was verified directly on all 511 nonzero 3+3 and 4,095 nonzero 3+4 graphs — H comes out Δ-regular, decomposes into Δ perfect matchings, and the restriction partitions E(G): zero failures.

**A15.** Birkhoff–von Neumann. First: the support graph of a doubly stochastic matrix (rows × columns, positive entries as edges) has a perfect matching *by Hall*: if S rows had |N(S)| < |S| positive-neighbor columns, then the rows of S sum to |S| while all their positive entries live in N(S)'s columns, whose column sums total |N(S)| < |S| — impossible. So: choose a permutation matrix P supported on such a perfect matching (all entries of M on P's support are positive), and let λ be the minimum positive entry of M on P's support. If λ = 1, then every entry of M on P's support is 1; since each row and column of M sums to 1, all off-support entries are 0, so M = P — a permutation matrix, and the decomposition is finished. Otherwise 1 − λ > 0 and M′ = (M − λP)/(1 − λ) is again doubly stochastic — the numerator is entrywise nonnegative with row and column sums 1 − λ — and M′ has fewer positive entries than M (at least one positive entry of M, where λ is attained, has become zero). Induct on the number of positive entries: eventually M′ is a permutation matrix itself. Unrolling: M = λ₁P₁ + λ₂P₂ + … with λᵢ > 0 and Σλᵢ = 1. Machine check: the peel run to ground on fixed 3×3 and two 4×4 instances — 3, 4, and 5 rounds respectively, weight sums exactly 1, reconstruction error at machine zero.

**A16.** *Part (a) — the obstruction.* Color the board like a chessboard; a domino covers one square of each color, so any tiling pairs every square with a differently-colored partner. The two removed corners share a color (their row and column offsets add to the same parity) — say black — so the mutilated board has 30 black squares against 32 white: the 32 white squares would need 32 distinct black partners among the 30 available. No tiling exists; the count alone is the proof (P2). *Part (b) — the companion theorem.* An m×n rectangle with m, n ≥ 2 and mn even has a Hamiltonian cycle through its squares: run down the first column, then weave back up row by row across the remaining columns (when m is even this closes directly; when m is odd, n is even — weave column by column instead). The cycle alternates colors, because the grid is bipartite. Now delete one black square b and one white square w: the cycle breaks into two paths, one from b's successor to w's predecessor, the other from w's successor to b's predecessor. b's cycle-neighbors are white and w's are black, so each path starts at one color and ends at the other — each path alternates and has an EVEN number of vertices (if b and w are adjacent on the cycle, one path is empty and the other has mn − 2 vertices). Pair consecutive squares along each path into dominoes: a tiling exists. This is exactly where (a)'s argument breaks: the count is necessary for a tiling, and on a rectangle with one removal of each color, the snake shows the count is also sufficient — the obstruction in (a) is not "a count is close to balanced" but "the count is off by two." ∎ Machine-checked: every one-of-each-color removal tiles — all 64 cases on 4×4, 324 on 6×6, and 1,024 on 8×8, zero exceptions (and the mutilated board of (a): 30 black, 32 white, maximum matching 30 — two whites must go unpaired).

**A17.** Necessity is honest counting (P2): the subcollection I sends Σ_{i∈I} d_i distinct delegates, no person serving twice, all drawn from ∪_{i∈I} A_i. Sufficiency is the padding move (P11), run on demands instead of dummies: replace committee i by d_i identical clones, each with membership A_i. The cloned family satisfies Hall — any set S of clones spanning the committee set I = {i : S contains a clone of i} has |S| ≤ Σ_{i∈I} d_i ≤ |∪_{i∈I} A_i| = |N(S)| — so (Lecture 1, in L5.1's committee costume) the clones have an SDR. Read it back: committee i's clones received d_i people, distinct because the SDR is, and no person serves two committees, because the SDR is injective. ∎ Machine-checked: for three committees over a four-person pool, all 4,096 membership patterns × all 8 demand triples in {1,2}³ — 32,768 instances — brute-force feasibility agreed with the condition on every single one. Micro-cases: A = {0,1,2}, B = {2,3}, C = {0,1,3} with demands (2,1,1) is feasible — A sends 0 and 1, B sends 2, C sends 3; but A = {0,1}, B = {0,1}, C = {2} with the same demands fails at the subcollection {A,B}: demand 3 from a two-person union, exactly as the condition records.

**A18.** (a) Let M* be a maximum matching and M a maximal one. Every edge e of M* touches an endpoint of some edge of M — otherwise M ∪ {e} is a strictly larger matching, contradicting maximality. Assign each edge of M* to one edge of M that it touches; an edge (a, b) of M receives at most two assignments, one through a and one through b, because M* has at most one edge at each vertex. So ν = |M*| ≤ 2|M| (P2's ledger, run twice). (b) If some edge had neither endpoint in M's endpoint set, it could be added to M — maximality again — so the endpoint set, of size 2|M| ≤ 2ν ≤ 2τ, covers every edge. What greedy keeps, in ANY graph, is a certified cover and a certified half-optimal matching — the same "stuck state = certificate" reflex as L2's engine (P18); what it loses, outside König's bipartite world, is exactness. The matching bound is tight on the path P₄: the middle edge is a maximal matching of size 1, while ν = 2. The cover bound is tight on the star K_{1,3}: any single edge is a maximal matching, so its endpoint set has two vertices, while τ = 1 = ν; on the path P₃, ν = τ = 1 but the endpoint set of either edge has two vertices. ∎ Machine-checked over all 33,861 nonempty graphs on at most six vertices: every maximal matching M satisfied 2|M| ≥ ν and its endpoint set covered every edge — zero violations.

**A19.** Suppose M is the unique perfect matching (with |X| = |Y| ≥ 1). Step 1 — no M-alternating cycle: if C were one, flipping along C (replace M-edges of C by the non-M edges of C) yields a second perfect matching — vertices on C keep exactly one matched edge, vertices off C keep theirs. Step 2 — orient: direct each M-edge from X to Y, every other edge from Y to X. An M-alternating cycle is precisely a directed cycle in this orientation, so the digraph is acyclic (P16's alternating bookkeeping, re-cast as directions). An acyclic digraph has a sink — a vertex with no outgoing edge. No x ∈ X can be a sink (its M-edge points out), so the sink is some y ∈ Y; and any non-M edge at y would point out of y, so ALL of y's edges are M-edges — but y is matched to exactly one x, so y has degree 1, its only edge being its M-edge xy. Step 3 — the bridge: deleting xy isolates y, so G − xy is disconnected: an edge of the unique matching is a bridge. Uniqueness cannot survive two-edge-connectivity. ∎ Machine-checked: all 13,188 bipartite graphs with |X| = |Y| = 2, 3, 4 having exactly one perfect matching — every single one has a matching edge whose removal disconnects it, zero exceptions; and on every perfect-matching-bearing graph of those sizes, "unique perfect matching" coincided exactly with "the orientation above is acyclic."

**A20.** Hall, with the case split doing all the work. Suppose S ⊆ X witnesses a failure: |N(S)| ≤ |S| − 1 < |S|. If |S| ≤ n/2, pick s ∈ S: |N(S)| ≥ d(s) ≥ ⌈n/2⌉ ≥ |S| — contradiction. If |S| > n/2, first note S ≠ X, since |N(X)| < n would leave some y ∈ Y with no neighbor, impossible when d(y) ≥ ⌈n/2⌉ ≥ 1; so pick y ∈ Y ∖ N(S): all of y's ≥ ⌈n/2⌉ neighbors lie in X ∖ S, forcing n − |S| ≥ ⌈n/2⌉, i.e., |S| ≤ ⌊n/2⌋ ≤ n/2 — contradiction again. Hall holds, and the perfect matching exists (P2's ledger run from both sides: once from s, once from y — Exercise 8 runs it from one side only, which is exactly why it buys only ⌈n/2⌉ delegates while the both-sides threshold buys the whole matching). Sharpness, machine-confirmed: on n = 4, the graph x₀:{y₀,y₁}, x₁:{y₂}, x₂:{y₂}, x₃:{y₃} has all degrees ≥ 1 = n/2 − 1 but S = {x₁, x₂} sees only {y₂} — maximum matching 3, no perfect matching; on n = 3, x₀:{y₀}, x₁:{y₀}, x₂:{y₁,y₂} has all degrees ≥ 1 = ⌈3/2⌉ − 1 but S = {x₀, x₁} sees only {y₀} — maximum matching 2. ∎ Machine-checked: all 7,384 bipartite graphs with |X| = |Y| = 2, 3, 4 and both-side degrees ≥ ⌈n/2⌉ have a perfect matching — zero violations.

---

## Revision History & Verification Notes

**Editions.** Reference edition (matching/flows/Hall reference treatment, one verified lab) → **Feynman lecture edition** (this edition): 5 lectures; all reference-edition methods preserved inside the narrative — Hall by the critical-set split and via König, König by alternating paths and via max-flow, the duality dictionary, max-flow min-cut with the augmenting-path proof, SDR via Hall — plus the deficiency form proved in full (the reference edition stated it only as an exercise), the k-regular decomposition promoted to a worked lecture, and the full Atlas exercise standard installed (tiers, ◆ pattern-unknown, ◐ Explorations, worked answers, this appendix). An adversarial review (session 63) then audited the entire chapter with a fresh machine battery — see the review record below; the mathematics survived otherwise untouched.

**Corrections during the rewrite.** The reference edition's lab record for E2 claimed Hall "fails at S = {x0,x1}" and predicted the maximum matching as "3 − 1 = 2". The machine's honest ledger: with X = {x0,…,x3} as the code defines it, the first failing subset is {x3} (the isolated applicant), the worst deficiency is 2 (at {x0,x1,x3}), and the correct prediction is 4 − 2 = 2. The numerical answer was right; the bookkeeping was wrong; both are now corrected in the lab record. E2's full deficient-set census: eight subsets of deficiency 1 ({x0,x1}, {x0,x1,x2}, {x3}, {x0,x3}, {x1,x3}, {x2,x3}, {x0,x2,x3}, {x1,x2,x3}) and two of deficiency 2 ({x0,x1,x3} and the full set {x0,x1,x2,x3}).

**External review audit (session 28).** An independent review of this chapter's web edition flagged fifteen findings; each was machine-re-verified here before adoption, and all were incorporated. Critical: Lecture 3.3 claimed the alternating-path engine can stall at a nonmaximum matching with *no* augmenting path — false in all graphs (Berge's lemma); the lecture now teaches the true failure (the naive parity-labeled search can *falsely report* failure), and Exploration X2 was rewritten to hunt that false negative. A13 and A14, previously stopped short, were replaced with complete proofs (see Standing decisions). A4's residual narrative was corrected against a verbatim re-run of the lab's Edmonds–Karp on N2: the terminating reachable set is {s, x0, x1, x3, y0}, the exposed cut is {s → x2, y0 → t}, and the cover it names is {x2, y0}; the earlier text's Z = everything-but-t and cover {y0, y1} was wrong ({y0, y1} is minimum but is not this residual's certificate), and the lab Part 2 record's cover "{x3, y0} ∪ dummies' worth" was wrong the same way (x3 is reachable). Exercise 1 and the lab Part 1 record promised four tight subsets of E1; the honest census is three — {x3}, {x2,x3}, X (A1 already said so; hint and record now agree). Exercise 8 / A8 now state the sharp ⌈n/2⌉ guarantee, with sharpness examples on both parities. Exercise 9 / A9 / the formula box now require s, t distinct and nonadjacent, with the reason stated. A7(b) carries the clean star-forest proof of |F| ≥ n − ν (valid in any graph without isolated vertices). A15 stops when λ = 1. Lecture 1's "neither regime" paragraph is now honest (integer Hall inequalities make the two regimes exhaustive), Lecture 4 states 0 ≤ f(e) ≤ c(e) and computes the stuck cut as c(Z, V∖Z), the k-regular proof (L5.2, A6) handles k = 0 explicitly, the min–max dictionary's Hall row now reads ν_X with placed + deficiency = |X|, and the Latin-transversal research pointer states the real Brualdi–Stein question (full transversals already fail at order 2 — both squares checked). The reviewer's independent numbers — N1 (flow 5, 3 augmentations), N2 (flow 2, 2 augmentations), the 512 + 4,096 bipartite censuses with Hall holding on 247 / 3,125 — all match this appendix's recorded runs. Deferred to the backlog: the reviewer's two proposed proof figures — both installed in the next pass (see Figures below).

**Figures (session 29).** The two review figures are embedded as fenced SVG blocks at their lecture locations, per the dual-presentation convention of the earlier chapters (prose and lab code stay terminal-portable; the figures are the paginated-export pictures). Figure 1 (§2.1) draws the ✎ checkpoint's run on E2: the alternating reachability from the free applicants x0 and x3, the reachable set Z = {x0, x3, y0, x1}, and the cover C = (X∖Z) ∪ (Y∩Z) = {x2, y0} with |C| = |M| = 2. Figure 2 (§4.1) shows the residual network's signature move on a unit-capacity diamond (s→a, s→b, a→b, a→t, b→t, all capacity 1): after the greedy first push s→a→b→t, the residual network's only simple s–t path is s→b→a→t through the *reverse* edge of a→b — pushing 1 refunds a→b to 0, and the final flow 2 equals the brute-force minimum cut, while a shortest-first order never touches the middle edge (Exercise 12(b)'s lesson, drawn). Both figures' data are machine-verified; the runs are recorded in the verification record below.

**Verification record (all deterministic, exhaustive where feasible; run in-sandbox as TypeScript computations — the Python labs are the reader's runnable copies of the same logic).** Hall ⇔ saturating matching: agreement on all 512 bipartite graphs with parts 3+3 (Hall holds on 247) and all 4096 with parts 3+4 (Hall holds on 3125). Deficiency form: zero violations on both censuses. König–Egerváry: max matching = min vertex cover, zero violations on both censuses; the alternating-path certificate C = (X∖Z) ∪ (Y∩Z) verified on every graph for the algorithm's matching, and for **every** maximum matching of every 3+3 graph (cover, parity, matched-ness, size). Corollaries: α = n − ν zero violations on both censuses; min edge cover = n − ν zero violations on every graph without isolated vertices. k-regular decomposition: zero failures on every k-regular graph of the 3+3 census (6, 6, 1 for k = 1, 2, 3) and the 4+4 census (24, 90, 24); every 4+4 graph with minimum degree ≥ 2 (7,343 of them) has matching ≥ 2. Max-flow min-cut: 1,024 diamond-topology networks (capacities 0–3) and 6,561 layered networks (capacities 0–2) — Edmonds–Karp value = brute-force minimum cut, conservation, and the full stuck-cut property (crossing edges saturated, reverse-crossing edges at zero flow, exposed cut capacity = flow value) with zero violations; at most 3 and 4 augmentations respectively. Menger (vertex version, via splitting): zero violations over all 10,240 (graph, pair) cases on all 1,024 five-vertex graphs, non-adjacent pairs. Latin rectangles: every Latin rectangle with n = 3 (30, of which 12 are full squares — the known count) and n = 4 (1,392, of which 576 are full squares — the known count) extends to a Latin square by the SDR row-extension, with Hall's condition holding at every stage, zero failures. Dilworth: all 219 labeled posets on 4 elements and all 4,231 on 5 (exactly the known censuses) satisfy width = minimum chain cover = n − maximum split-graph matching, zero violations. Δ-round edge partition (A14's slot-pairing regularization): the constructed multigraph is Δ-regular and its Δ perfect matchings restrict to a partition of E(G) — zero failures on all 511 nonzero 3+3 and 4,095 nonzero 3+4 graphs; the maximum-degree covering lemma (a maximum matching saturating every Δ-degree vertex exists) also verified on the same censuses. Birkhoff–von Neumann: exact decompositions on fixed instances (3, 4, and 5 permutation matrices; weight sums exactly 1; reconstruction at machine zero). The two labs' recorded outputs derive from these runs: E1 (Hall ✓, matching 4, cover 4), E2 (first failure {x3}, worst deficiency 2 at {x0,x1,x3}, matching 2 = cover 2), N1 (flow 5, 3 augmentations, cut 5), N2 (flow 2, 2 augmentations, cut 2). Figures 1–2 (session 29): Figure 1's data is the §2.1 checkpoint run itself — free X = {x0, x3}; alternating reachability gives Z ∩ X = {x0, x1, x3} and Z ∩ Y = {y0}; the cover C = (X∖Z) ∪ (Y∩Z) = {x2, y0} is verified a vertex cover with |C| = |M| = ν = 2. Figure 2's diamond (unit capacities on s→a, s→b, a→b, a→t, b→t): the brute-force minimum cut is 2; after the greedy round s→a→b→t (value 1), an exhaustive enumeration of the residual network's simple s–t paths finds exactly one — s→b→a→t, through the reverse edge of a→b; pushing 1 along it cancels a→b (flow 1 → 0), conserves at a and b, respects every capacity, and lands at value 2 = the minimum cut; a shortest-first order (s→a→t, then s→b→t) reaches the same value with the middle edge never touched.

**Standing decisions.** The lecture text carries no inline history; revisions are recorded here. New chapters inherit the full standard from the start. Backlog: Edmonds' blossom algorithm and Tutte's theorem as a full section (the general-graph matching theory); Hopcroft–Karp analysis in full; stable marriage as an application section. The two session-28 review figures are installed as Figures 1–2 (session 29; see Figures above — Figure 2's cancellation diamond is a new verified example, recorded in the verification record). Answers A13 and A14 are complete proofs as of the session-28 audit: an earlier edition deliberately handed their final counting lines to the reader, and the review's replacements — the A13 missing-symbol double count and the A14 slot-pairing regularization — were machine-verified (the A14 construction checked on all 511 nonzero 3+3 and 4,095 nonzero 3+4 graphs, zero failures) and adopted.

**Follow-up review audit (session 32; every claim machine-verified before acting).** A second, independent review of the revised web edition confirmed the session-28 repairs and reported no new central-theorem error — and its assessment was re-verified claim by claim, with fresh machine runs, before this record was written. The eight confirmed repairs: (1) the Berge lesson — Lecture 3 teaches Berge's lemma for all graphs (nonmaximum ⇒ an augmenting path always exists) and locates the genuine failure in the parity-labeled search's bookkeeping, with X2 framed on the search lying, not on augmentation failing; (2) Exercise 1 — E1 has exactly three tight subsets ({x3}, {x2,x3}, X; machine-enumerated over all 15, zero deficient), prompt and hint in agreement; (3) the deficiency form and E2 — {x0,x1,x3} has deficiency 2 (machine census: exactly ten deficient sets — eight of deficiency 1, two of deficiency 2, the maximum at {x0,x1,x3} and X), maximum matching 4 − 2 = 2, first-failing versus maximally-deficient explicitly distinguished; (4) A4's flow certificate — reproduced exactly by an independent Edmonds–Karp implementation: flow 2 in 2 augmentations, stuck reachable set {s, x0, x1, x3, y0}, exposed cut the saturated pair s → x2 and y0 → t (value 2), read as the cover {x2, y0}; (5) Exercises 8 and 9 — the ⌈n/2⌉ guarantee machine-checked exhaustively at n = 3 (64 families) and n = 4 (14,641) with zero violations, sharpness exact on both parities (the all-equal families serve exactly ⌈n/2⌉), and vertex-Menger stated for distinct nonadjacent terminals; (6) A13 — the Latin-rectangle double count re-verified by full enumeration: n = 3 gives 30 rectangles (12 full squares), n = 4 gives 1,392 (576 full squares) — the known counts — with Hall's condition holding at every extension stage, zero failures; (7) A14 — the padding argument re-verified on all 511 nonzero 3+3 and 4,095 nonzero 3+4 bipartite graphs: the slot-pairing construction yields a Δ-regular multigraph every time, the Δ perfect matchings peel cleanly, and the restriction partitions E(G) — zero failures; (8) the flow lab — the printed results reproduce exactly (N1: flow 5 in 3 augmentations, minimum cut 5, three of the four cuts tying at 5 with {s, b} alone at 6; N2: flow 2 in 2 augmentations, cut 2), verified by a faithful in-sandbox reimplementation (the standing convention: the Python labs are the reader's runnable copies of the same logic). The review's one remaining issue — mojibake in the visible no-print banner — was **genuine** and is now repaired: a byte-level scan showed the frame's banner carrying double-encoded em dashes (â + U+0080 + U+0094, the Latin-1 ghost of bytes E2 80 94), three occurrences per web edition (the title line and two in the banner paragraph) — and not only here: the same corrupted sequences sat in every web edition's frame, and all five are now repaired with proper UTF-8 em dashes (see also the session-32 correction to the Ch. 4 record, whose session-28 audit had wrongly dismissed the identical banner finding as a viewing artifact). The banner still does not print, exactly as designed. The review's final recommendations — print to PDF and visually inspect the two SVG figures, long equations, tables, and code-block pagination, then re-extract the Python blocks from the exported PDF and compile them as the independent release gate — are user-owned steps, the last before release. Verdict adopted: no structural rewrite; the chapter is release-ready pending the PDF gate.

**Backfill (session 41).** Five graded exercises (16–20) with pattern-mapped hints were added, per the atlas-wide backfill mandate: mutilated chessboards (the two-color counting obstruction, and the Hamiltonian snake that proves one-of-each-color removals always tile); committees with quotas (the capacitated Hall theorem, proved by cloning); greedy's maximal-matching 2-approximation (valid in all graphs, where König's exactness is bipartite-only); uniquely matchable bipartite graphs (some matching edge is a bridge — alternating cycles, an orientation, and a sink); and the both-sides half-degree threshold for perfect matchings (with sharpness on both parities, and the explicit contrast with Exercise 8's one-sided bound). Worked answers A16–A20 were machine-verified before installation: the mutilated board's color census (30/32, maximum matching 30); exhaustive one-of-each-color removal tilings on 4×4 (64 cases), 6×6 (324), and 8×8 (1,024) — every one tileable; the capacitated Hall condition against brute-force feasibility on 32,768 instances (zero mismatches, plus the two micro-cases); the 2-approximation properties over all 33,861 nonempty graphs on at most six vertices (zero violations); the bridge theorem on all 13,188 bipartite graphs on 2–4 + 2 vertices with a unique perfect matching (zero exceptions), with the orientation acyclicity cross-check confirmed on every perfect-matching-bearing graph of those sizes; and the half-degree theorem on all 7,384 bipartite graphs with both-side degrees ≥ ⌈n/2⌉ (zero violations), both sharpness instances machine-confirmed (maximum matchings 3 and 2).

**Lab expansion (session 44).** A third lab part was added, per the atlas lab-expansion mandate: Hopcroft–Karp — one BFS per phase layers the alternating forest, one DFS commits a maximal set of vertex-disjoint shortest augmenting paths — run on the chapter's own E1 and E2 and on seeded larger instances (a Lehmer LCG, x ← 48271·x mod (2³¹ − 1), implemented identically in the Python lab and in the verifying TypeScript port, so the printed outputs are exactly reproducible). Every recorded number was machine-verified before installation: E1 → (4, 1) and E2 → (2, 1); the seeded instances (n = 30, 60, 100 at p = 0.2 and p = 3/n — matching sizes 30, 60, 100 and 27, 56, 97; phase counts 3, 2, 2 and 2, 5, 4 against the √V ceilings 7.75, 10.95, 14.14); and the exhaustive census — all 74,954 bipartite graphs with |X|, |Y| ≤ 4, the engine against a brute-force DP, zero mismatches, phase histogram 16 / 51,657 / 23,179 / 102 (the zero-phase graphs are exactly the 16 edgeless ones). A first TypeScript draft that blocked Y vertices per phase failed its own census — a zero-augmentation phase, caught by a phase-progress guard before any installation; the installed engine is the standard layered-forest version.

**Adversarial review (session 63).** The atlas-wide skeptic-versus-engineer arc reached this chapter: the text was audited chunk by chunk, every retained objection machine-verified before any edit, extend-only. One defect was confirmed and fixed: Figure 2's panel-1 caption omitted a→b from the round-1 saturation — an omission that matters, because a→b being saturated is exactly what leaves the residual network with a *single* simple s–t path (the caption now reads "Round 1 saturates s→a, a→b and b→t; the direct edges s→b and a→t still have room"). The fresh battery otherwise came back green: Hall on 247 / 3,125 graphs plus the deficiency form, zero violations; König–Egerváry, α = n − ν, and edge covers zero violations, with the alternating-path certificate checked on every one of the 1,024 maximum matchings of the 3+3 census; E1's tight sets exactly {x3}, {x2,x3}, X; E2's deficient-set census exactly ten (eight of deficiency 1, two of deficiency 2, worst 2 at {x0,x1,x3}), cover {x2,y0} from both engine and checkpoint; k-regular decompositions 6, 6, 1 / 24, 90, 24 with zero failures; all 7,343 minimum-degree-≥-2 graphs of the 4+4 census matching ≥ 2; A20's 7,384 both-side-threshold graphs with the sharpness pair 3 and 2; A8's 64 + 14,641 families; the flow censuses 1,024 + 6,561 networks, zero violations, ≤ 3 / ≤ 4 augmentations; Menger over all 10,240 ordered non-adjacent (graph, pair) cases of the 1,024 five-vertex graphs; Latin rectangles 30 / 12 and 1,392 / 576 — the known counts — with zero extension failures; Dilworth on 219 + 4,231 posets; A14's 4,606 graphs plus the covering lemma; A16–A19's censuses (the mutilated board 30/32; one-of-each-color removals tiling in all 64 / 324 / 1,024 cases; capacitated Hall on 32,768 instances; the 2-approximation on 33,861 graphs; 13,188 unique-perfect-matching graphs, all bridged); Birkhoff–von Neumann at 3, 4, 5 permutation rounds with Σλ = 1 and reconstruction at machine zero; Hopcroft–Karp reproduced bit-for-bit on the seeded LCG — E1 (4, 1), E2 (2, 1), phase counts 3, 2, 2 and 2, 5, 4 against the √V ceilings 7.75, 10.95, 14.14, and the 74,954-graph census with zero mismatches, histogram 16 / 51,657 / 23,179 / 102. Six reviewer-side checker alarms were re-run and resolved as checker bugs (a bit-index off-by-one, missing dummy slots, unlabeled parallel copies, a micro-case clone list, a raw-λ weight-accounting slip, and a bitmask-DP memory blowup replaced by Kuhn augmenting paths) — none implicate the chapter. Two honest notes recorded without edit: Menger's 10,240 counts *ordered* non-adjacent pairs; and A15's "fixed instances" are not printed in the chapter — verified as 3 and 4 permutation rounds on uniform matrices and 5 rounds on a recorded 4×4 combo instance (2,120 / 20,000 structured combos reach 5). Both figures were judged adequate as-is — their data and coordinates check against the recorded runs. The web edition was rebuilt per the rebuild rule; the arc advances to Chapter 6.

**Expansion-pass adoption (session 89).** A user-supplied corrected draft of the web edition was compared against this master, change by change; every adoption was machine-verified fresh before installation, and every rejection was recorded. The draft's bulk — a wholesale conversion of the master's plain Unicode to $-delimited TeX plus a MathJax CDN — was rejected outright (the standing no-script export rule; the master's notation is plain Unicode by design), as were its exercise renumbering (backfill 16–20 → 13–17, ◆ 13–15 → 18–20: pure churn with reverse-index cost and no content gain), its renaming of the "Graded backfill" heading, its deletion of the lab's inline honest-correction parenthetical, and its new end-of-chapter appendix restating the L1.2 correction (this Revision History and the inline lab record already carry it). Adopted, all translated to plain Unicode: the L1.2 fix of the E2 sentence (the old text said "three applicants" while listing four — the E2 census re-verified: four applicants, worst deficiency 2 at {x0,x1,x3} and X, first lab-order failure {x3}, ten deficient subsets); the L5.1 warm-up repair (the old text claimed "every pair's union has size 2 ≥ 2" — a genuine numerical error; the pair unions of {a,b}, {b,c}, {a,c} all have size 3, machine-confirmed); the L5.2 intro rewrite (the old "players vs. days?" parenthesis was garbled; the new opening states the 0-1-matrix equivalence cleanly); the Figure 1 consistency fix (caption "every edge is caught at its red end" → "the ringed vertices cover every edge", matching the ring legend, plus the ring-label repositioning) and the Figure 2 label re-anchoring; the sharpened Exercise 12(b) (the old requirement — "an order in which the engine terminates" — was vacuous, since every order terminates; the new one asks for an order requiring more rounds than a shortest-first order); the A2 cleanup (the old answer narrated a false start — "an SDR exists … Wait — recount" — before concluding that all three parts fail; the new answer states d = 1 and the promises 3, 2, 3 directly, with the draft's subcollection-verification sentence corrected during adoption: its claim that "unions of one or two committees have size at least 2" was false for (c)'s singleton committees {a} and {c}, whose unions have size 1 — the corrected text splits singletons (deficiency ≤ 0) from pairs (≥ 2); machine check re-run: matchings 3, 2, 3, each = |X| − d); the full A9 proof (the old answer was a three-sentence sketch; the new one proves both directions — the A-construction giving min cut ≤ min separator and the U-construction giving min separator ≤ min cut — over the two-∞-arcs, s_out/t_in split network; the receipt now states the census honestly as 5,120 unordered non-adjacent pairs — 10,240 ordered — on all 1,024 five-vertex graphs, split-network flow = brute-force minimum separator, zero violations, re-run fresh this session); the A11 rewrite (the old (a) carried a "wait" self-dialogue; the new proof adds the explicit acyclicity argument — a directed cycle would force x₁ < x₂ < … < x₁ — and the forest-components chain count, with the antichain accounting tightened; censuses re-run: 219 labeled posets on 4 elements, 4,231 on 5 — the known counts — width = min chain cover = n − max split matching, zero violations); the A12(b) concrete example (diamond-plus-cross, capacities s→a = 2, s→b = 2, a→b = 1, a→t = 1, b→t = 2; machine-verified: min cut 3, shortest-first 2 augmentations, bad order 3, value 3 both ways) merged with — not replacing — the standing machine record (1,024 diamond + 6,561 layered networks); the A20 threshold sharpening (d(s) ≥ ⌈n/2⌉ and n − |S| ≥ ⌈n/2⌉, i.e. |S| ≤ ⌊n/2⌋, replacing the coarser n/2 bounds — valid since degrees and |S| are integers; the 7,384-graph both-side-threshold census re-run, zero violations); and the A15 precision fixes (λ defined as the minimum positive entry on P's support; the λ = 1 case now justified — row sums 1 force the off-support entries to 0, so M = P; and the induction metric corrected from "one more zero" — false when λ is attained several times — to "fewer positive entries"; the λ = 1 ⇒ M = P implication machine-checked over 5,369 scaled-integer Birkhoff combinations, 11,034 permutation-support checks, zero counterexamples). The pattern-reference audit requested with the draft came back clean: every pattern ID in the draft (P2, P4, P11, P16, P17, P18) matches this master's assignment and the atlas registry — no restoration needed. The web edition was rebaked from this master.

**Repeat expansion pass (session 100).** A second user-supplied draft of the web edition was compared against this master, item by item; every adoption was machine-verified fresh before installation, and every rejection was recorded with its receipt. The pattern-reference audit requested with the draft came back clean at every level: the draft's pattern census (P2 ×15, P4 ×5, P11 ×7, P16 ×6, P17 ×3, P18 ×10) matches this master's exactly, the pattern tables are byte-equivalent, and no restoration was needed. Adopted, eight installs: the §2.1 cover verification's explicit two-case split (xy ∈ M / xy ∉ M — the master had treated every edge as non-matching; the 512-graph certificate census re-run green, E2's certificate {x2, y0} reproduced); the §4.1 free-inequality stumble removed ("at most 0 — well, it is subtracted" → the clean clause); the §4.1 cut↔cover dictionary made explicit in both directions (any finite-capacity cut yields the cover C = (X∖S) ∪ (Y∩S) with |C| at most the cut's capacity, and any cover C defines the cut S = {s} ∪ (X∖C) ∪ (Y∩C) of capacity exactly |C|; 512/512 census, zero violations); the A20 clone-family Hall chain made explicit (|S| ≤ Σ d_i ≤ |∪ A_i| = |N(S)|; the 32,768-instance quota census and both micro-cases re-run green); the A18 stumble repaired ("... wait," → the matching bound's tightness on P₄ and the cover bound's tightness on K₁,₃ and P₃, all three machine-confirmed: P₄'s maximal matchings {middle} and {ends} with ν = 2, K₁,₃ and P₃ each with ν = τ = 1); the A16 snake-cycle precision ("EVEN length" → "an EVEN number of vertices," with the adjacent-case parenthetical — the master's "length" counted edges and was genuinely odd; 64/64 path decompositions even, the adjacent case 0 + 14 vertices, 64/64 tilings re-verified); the A19 guard "(with |X| = |Y| ≥ 1)" (the empty graph has the unique perfect matching ∅ and no edge that could be a bridge — the statement is false without the guard); and the Part-2 lab upgrade (edmonds_karp now returns the flow, the augmentation count, the terminating reachable set and the saturated cut; min_cut_brute now returns the count of tied minimum cuts; the empty-graph guards normalized; the verified-output sentence updated to the fresh runs: N1 (5, 3) with three tied cuts of value 5 and {s, b} = 6, N2 (2, 2) with Z = [0, 1, 2, 4, 5] and the saturated cut [(0, 3), (5, 9)], the stuck property zero violations on both networks). Rejected, with receipts: the exercise renumbering and the "Graded backfill" heading rename (session-89 retreads); the Part-1 lab additions (their outputs were never recorded in the draft) and the honest-correction parenthetical's deletion (another retread); the Part-3 nX/nY guard (trivial); the A2 rewording (drops the honest-lesson sentence); the A9 nonadjacency-reason deletion; the A12(a) rewording and its (b) deletion of the standing machine record (1,024 diamond + 6,561 layered networks); the A11 copy-labels; the A20 redundant guards; the §1.2 empty-set parenthetical (the master was already correct); the figure redraws (content-identical churn); and the TeX/MathJax conversion (the standing no-script rule). Two rejections deserve their own lines. The draft's A15 receipt claims "3, 4, and 4 rounds" for its own Birkhoff–von Neumann suite, but its own printed instances peel in 5, 4, and 5 rounds — machine-confirmed, with two of the three instances contradicting the draft's own text; this master's session-63 record (3, 4, 5 on its own instances) stands. And the draft's appendix re-derivation suite ships code defects rather than new knowledge: the §5 "tiling census" prints only |B|·|W| pair counts, the §8 bridge check is a degree-1 proxy, ec_ok is accumulated but never returned, and the promised "C₅ + pendant" run never happens; its X2 paw demonstration is correct (the naive parity search does falsely report failure on the paw with M = {(1,2)}, ν = 2 — machine-confirmed) but that investigation is exactly what this master's X2 brief already assigns. The web edition was rebaked from this master, oracle-first: the renderer was revalidated byte-identical against the previous export before the bake, and the export grew 88,553 → 89,353 B (448 → 459 lines), no script, the write round-trip verified.

---
*Chapter status: ✅ **Feynman edition + two external reviews audited (sessions 28, 32) + exercise backfill (session 41) + lab expansion (session 44) + adversarial review (session 63) + expansion-pass adoption (session 89) + repeat expansion pass (session 100)** — 5 lectures, 6 problem families, 9 methods preserved from the reference canon, a three-part verified lab (exhaustive Hall/cover checks, the flow compiler, Hopcroft–Karp in phases); 17 graded exercises + 3 ◆ pattern-unknown + 2 ◐ explorations, 20 worked answers machine-verified. Two external reviews audited and incorporated (session 28: fifteen findings, all fixed; session 32: follow-up — all eight repairs confirmed, the web frame's banner encoding repaired across all five web editions, no new mathematical defect; the PDF export gate remains, user-owned). Two vector proof figures embedded (session 29). Adversarially reviewed (session 63): one figure-caption defect fixed, the mathematics otherwise confirmed by a fresh machine battery — see the review record above. Expansion-pass adoption (session 89): a user-supplied draft audited item by item — six defect repairs and five rigor upgrades adopted (each machine-verified fresh before install), the draft's format regressions and exercise renumbering rejected, pattern references audited clean — see the adoption record above. Repeat expansion pass (session 100): a second draft audited the same way — eight adoptions installed (each machine-verified fresh), the retreads and the draft's new defects rejected with receipts, pattern references audited clean again — see the record above. Ships with its web edition (the standard delivery format): the HTML canvas embeds this chapter byte-identically; print to PDF from a browser for a correct export.*
