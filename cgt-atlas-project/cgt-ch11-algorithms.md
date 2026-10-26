---
name: "cgt-ch11-algorithms"
title: "Ch. 11 — Algorithms & Complexity of Combinatorics: A Lecture Course in the Feynman Style"
type: "text/markdown"
---

# Chapter 11 · Algorithms & Complexity of Combinatorics

*Part of the Combinatorics & Graph Theory Atlas (the chapter map lives in the book basis).*

The Atlas has been running two engines since Chapter 2: proofs that things exist, and procedures that find them. This chapter asks the question both engines have been dodging: *how fast can the procedure go?* The answer splits combinatorics into three worlds, and the chapter walks all three. The **easy world**: greedy when the structure is a matroid (Kruskal is exact, and the chapter proves why), flows with costs (min-cost flow and the assignment problem, by successive shortest paths), and matching in general graphs — Edmonds' blossoms and Tutte's theorem, the backlog Chapter 5 honestly deferred, paid here in full. The **hard world**: NP-completeness, where the Atlas's favorite pattern — reduction — turns against us and proves that no fast algorithm exists at all, unless P = NP. The spine runs in full, 3-SAT through independent set, clique, and vertex cover, every step proved, every gadget machine-verified on its own body: the satisfiable instance's five assignments and twelve independent sets, the unsatisfiable instance's clean zero. The **surviving world**: what remains reachable when exactness is lost — approximation with guarantees. Greedy set cover within a harmonic number of optimal, and the proof that this is the best any polynomial algorithm can promise; the traveling salesman within 3/2 by Christofides, with the matching lemma machine-checked to exact tightness on a five-point instance; MaxCut within 0.878 by semidefinite programming, the exact constant computed, its optimality tied to the Unique Games Conjecture. And the final twist: hardness in n can coexist with tractability in k — vertex cover in O(2^k·(n+m)), the bounded search tree that this chapter runs on all 33,866 labeled graphs up to six vertices, its worst case hitting the theory's bound of 2^(k+1) − 1 nodes exactly. Every number in this chapter is machine-verified by the lab, proved in the text, or carries its source; the census counts are the chapter's own.

## How to read this chapter

**Notation.** Graphs have n vertices and m edges, vertices labeled 0 to n−1 in the lab (the code and the prose agree; [n] in prose means {1, …, n}, but every lab instance is 0-indexed and says so). α(G) is the independence number, ω(G) the clique number, τ(G) the minimum vertex cover, ν(G) the matching number — the Chapter 5 conventions. "Polytime" means time O(n^c) for a constant c. **P** is the class of problems decidable in polytime; **NP** is the class whose *yes*-answers have polytime-checkable certificates; a problem is **NP-complete** if it is in NP and every NP problem reduces to it in polytime (Lecture 1 makes all three definitions precise). A *reduction* from problem A to problem B is a polytime map turning instances of A into instances of B with the same answer — the Atlas's pattern P25, until now a proof tool, here promoted to a theorem about hardness. H_n = 1 + 1/2 + ⋯ + 1/n is the n-th harmonic number (H₂ = 1.5, H₁₀₀ ≈ 5.187). For approximation, the *ratio* of a minimization algorithm is cost(ALG)/OPT, always ≥ 1; guarantees are upper bounds on the ratio. In Lecture 5 the metric is Manhattan distance |x₁ − x₂| + |y₁ − y₂| unless stated. In Lecture 6, odd(G) is the number of odd-order components of G, and G − S means deleting S's vertices and all incident edges. Letters are re-stated locally where a lecture needs its own.

**The exercises are graded:** ●○○ *easy* (a direct application of one lecture idea), ●●○ *moderate* (two ideas, or one tricky step), ●●● *tough* (several chapter ideas combined). Hints travel with the problems and name the pattern; worked answers sit at the very end of the chapter. Try honestly before reading a hint. Beyond the graded set, ◆ **pattern-unknown** problems name no method and carry no hint: diagnosing which tool fits is part of the problem. And ◐ **Explorations** at the end are open-ended investigations with no single right answer — research training, not test preparation.

## The pattern table for this chapter

| Pattern | Plain language | Where you meet it |
|---------|---------------|-------------------|
| **P25 Reduction / encoding** | Translate one problem into another's language — and the translation carries more than the answer: it can carry optimality, hardness, or a guarantee | L1 (the entire NP-completeness spine), L4 (assignment → min-cost flow), L2 (greedy priced against an unknown optimum) |
| **P18 Algorithmic proof** | The proof *is* a procedure; termination is the theorem; the running time is part of the statement | L2 (greedy's guarantee lives in its own execution), L4 (successive shortest paths), L6 (the blossom engine) |
| **P17 Duality (min–max)** | Two problems are the same number; a certificate for one is a solution of the other | L1 (α + τ = n), L4 (potentials price the residual; no negative cycle = optimal), L6 (Tutte's condition is the obstruction, exactly) |
| **P16 Alternating paths / augmentation** | Improve a partial solution along a path; the residual network remembers what you can undo | L4 (residuals and cancellation), L6 (the engine that stalls on odd cycles, and the blossom repair) |
| **P10 Averaging / expectation** | Some object beats the average; some random choice does no worse in expectation | L2 (the charging argument), L5 (random MaxCut at 1/2; the random hyperplane at 0.878) |
| **P9 Pigeonhole** | n+1 objects, n boxes — here mostly as parity: odd sets, odd components, distinct representatives | L5 (the optimal tour's odd vertices split into two matchings), L6 (odd components eat distinct vertices of S) |
| **P4 Recurrence + induction** | Relate case k to smaller cases, on purpose and in the exponent | L1 (the 2^k search tree), L6 (Tutte's induction on vertex count) |
| **Hardness is structure (lore)** | An NP-completeness proof is not a defeat — it is the theorem that the *structure* two problems share is exactly the structure that resists speed | L1, L2 (the ln n ceiling), L5 (0.878's conjectured finality) |
| **The guarantee is the theorem (lore)** | When exactness is impossible, the honest objects are provable ratios — and the proof of a ratio is still a proof | L2, L4, L5, and the 2^k light of L1 |

---

## Lecture 1 · P, NP, and the Reduction Spine

Chapter 2 drew Euler circuits and Hamilton cycles side by side and promised (§5.3) that a later chapter would make their difference precise. Chapter 5 built matching and flow engines that always terminate, always certifiably. This lecture is the reckoning: a framework in which "no good algorithm exists" is a *theorem*, proved the same way as any other — by reduction, pattern P25 turned inside out. The spine runs from 3-SAT through independent set to clique to vertex cover, every reduction proved in full and every gadget run on the lab's two witness instances before being trusted. Then the twist that saves the chapter from despair: the same vertex cover that is NP-hard in n is solvable in time O(2^k·(n+m)) when you only care about solutions of size at most k — and the census says the bound is honest, because the worst tree the lab ever grew hits it exactly.

### 1.1 What "hard" means

A *decision problem* is a question with a yes/no answer on each instance: does this graph have a Hamilton cycle, does this formula have a satisfying assignment. An algorithm is *polynomial-time* (polytime) if on instances of size n it halts within O(n^c) steps for a fixed constant c. **P** is the class of decision problems solvable in polytime: the Euler test (parity and connectivity), shortest paths, maximum flow, matching — Chapters 2 and 5 built these.

**NP** is defined by certificates. A problem is in NP if every *yes*-instance has a proof, checkable in polytime, that convinces a skeptic. A Hamilton cycle instance answers "yes" exactly when someone can hand you the cycle — checking that the handed-over list visits every vertex once and uses only real edges is O(n²). A satisfying assignment checks in O(m). A claimed perfect matching checks in O(m). Note what this definition does *not* say: it says nothing about *finding* the certificate, only about checking one. That asymmetry — verification seems easy, discovery seems hard — is the entire subject.

A problem is **NP-complete** if (i) it is in NP, and (ii) every problem in NP reduces to it: for every NP problem A there is a polytime map carrying instances of A to instances of our problem, preserving the answer. If any NP-complete problem has a polytime algorithm, then every NP problem does — P = NP.

**Theorem (Cook–Levin; statement).** Satisfiability of Boolean formulas is NP-complete. Every problem in NP reduces to satisfiability in polynomial time. (Cook 1971, independently Levin; the reduction encodes the verifier's entire computation as a Boolean formula.)

Karp (1972) then showed that twenty-one natural problems — including clique, vertex cover, Hamilton cycle, and set cover — are NP-complete by direct reduction, and the industry was born: thousands of problems since, each hardness claim a reduction, each reduction a combinatorial construction you can check by hand. The Atlas's stance: a reduction is a proof like any other, and we run its gadgets through the machine before printing them. Whether P = NP is *open* — the Clay Mathematics Institute prices it at one million dollars — and nothing in this chapter depends on the answer being either way. The theorems have the honest form: *unless P = NP, no polytime algorithm does X*.

### 1.2 The spine, in full: 3-SAT → Independent Set → Clique → Vertex Cover

The spine deserves to be walked once with every joint visible. **3-SAT**: given a formula in conjunctive normal form, m clauses, each a disjunction of exactly three literals (a variable or its negation), decide whether some assignment makes every clause true.

**Theorem.** 3-SAT reduces to Independent Set: there is a polytime map from 3-clause formulas to graphs such that the formula is satisfiable if and only if the graph has an independent set of size m.

**Construction.** For each clause, create a triangle: three fresh vertices, one per literal *occurrence*, all three edges present. Then connect every pair of complementary literal occurrences across the whole graph: every vertex labeled x is adjacent to every vertex labeled ¬x, wherever they sit. The graph has 3m vertices.

**(⇐) From an assignment to an independent set.** Suppose the assignment satisfies the formula. From each clause pick one literal true under the assignment. The chosen vertices, one per clause, are m in number; no two sit in one triangle (one per clause, and within a clause all pairs are adjacent), and no two are complementary (both would have to be true, impossible). So they form an independent set of size m.

**(⇒) From an independent set to an assignment.** An independent set of size m contains at most one vertex per triangle (within a triangle everything is adjacent), and there are m triangles, so it contains *exactly* one per clause. No complementary pair sits in the set, so reading the chosen labels gives a consistent partial assignment — set each variable true or false as its chosen occurrence demands. The chosen occurrence in each clause is true under this assignment, so every clause is satisfied. ∎

The lab runs both directions on two witness instances before this chapter believed them. The satisfiable instance (x ∨ y ∨ ¬z)(¬x ∨ y ∨ z)(x ∨ ¬y ∨ z) has exactly **5 satisfying assignments** (000, 011, 101, 110, 111 — every one of which yields an independent set by the construction) and exactly **12 independent sets of size 3** in its 9-vertex gadget — and all twelve pick one literal per clause, as the proof says they must: same-clause vertices are adjacent, so the shape is automatic. The unsatisfiable instance (x ∨ y)(¬x ∨ y)(x ∨ ¬y)(¬x ∨ ¬y) — four 2-literal clauses, its gadget built the same way with edges in place of triangles — has **0** satisfying assignments and **0** independent sets of size 4. Two clean zeros: the equivalence is not a coincidence of small numbers.

**✎ Checkpoint 1.** Verify the unsatisfiable instance by hand first — four clauses, two cases: x true forces y true (from ¬x ∨ y) and y false (from ¬x ∨ ¬y): contradiction; x false forces y true (from x ∨ y) and y false (from x ∨ ¬y): contradiction again. Eight assignments, none surviving. Then convince yourself the gadget's 8 vertices cannot host an independent set of size 4 *without* the theorem: the four 2-literal clauses form four disjoint edges, so any independent set of size 4 must pick exactly one vertex from each clause-edge. Because complementary literals are joined by edges across the gadget, the chosen vertices can include at most one sign of x (either x or ¬x, never both) and at most one sign of y (either y or ¬y, never both) — at most two allowed literal labels in total. Since the four clauses exhaust all four sign pairs (±x ∨ ±y), the unique clause whose two literals are the negations of the two allowed labels has neither of its vertices available, so at most three clauses can contribute a vertex and α(G) ≤ 3 < 4.

**From Independent Set to Clique** is one word: complement. An independent set in G is a clique in the complement Ḡ, edge for non-edge. So a polytime algorithm for clique would solve independent set.

**From Clique to Vertex Cover** is one identity, and the identity deserves its own line. Recall τ(G) is the minimum size of a vertex cover — a set touching every edge — and α(G) the maximum independent set.

**Theorem (Gallai).** α(G) + τ(G) = n for every graph.

**Proof.** If S is independent, every edge has at least one endpoint outside S (both endpoints inside would be an edge inside S), so V ∖ S is a vertex cover: τ ≤ n − α. Conversely if C is a vertex cover, no edge lies entirely inside V ∖ C, so V ∖ C is independent: α ≥ n − τ. Chain the two inequalities and the sandwich closes: α + τ = n. ∎

So G has a clique of size k iff Ḡ has an independent set of size k iff Ḡ has a vertex cover of size n − k: a polytime algorithm for vertex cover would solve clique, hence independent set, hence 3-SAT. The spine is closed, and the lab verified Gallai's identity by brute force on **all 33,866 labeled graphs on 2 to 6 vertices: zero violations**. Three problems — one structure. That is the lesson of the spine, and it is P25 promoted from proof technique to worldview: the reduction does not just transport the answer, it declares the two problems *the same problem wearing different signs*.

### 1.3 Two more doors, and a census

Two NP-completeness statements complete the map this chapter needs; both are cited, not re-proved — their constructions are longer than the spine's and teach no new idea. **3-coloring** (deciding whether a graph's vertices can be colored with three colors, adjacent vertices differently) is NP-complete: Stockmeyer 1973, with the now-standard simplified construction of Garey–Johnson–Stockmeyer 1976. **Hamiltonian cycle** is NP-complete (Karp 1972). Here is the Chapter 2 promise paid: *no local, checkable criterion like Euler's parity condition can characterize Hamiltonicity, unless P = NP* — because a polytime characterization would be a polytime algorithm for an NP-complete problem. The twins of §5.3 are twins no more.

Yet the news is not all subtraction, and one census puts the border on a map. Dirac's theorem (Chapter 2's Lecture 6) guarantees a Hamilton cycle whenever n ≥ 3 and every degree is at least n/2, and the guarantee is *certifiable*: the tour is its own certificate, which is exactly why Hamiltonicity is in NP while non-Hamiltonicity has no known short certificate. The lab's census of all labeled graphs on five and six vertices: at n = 5, **26** Dirac graphs, all Hamiltonian, alongside **192** non-Dirac graphs that are Hamiltonian anyway and **806** that are not; at n = 6, **1,858** Dirac graphs, all Hamiltonian (zero exceptions, as the theorem demands), **8,220** non-Dirac Hamiltonian, **22,690** not. The hardness lives entirely in the wilderness below the Dirac line — the theorem is sufficient, genuinely not necessary, and NP-completeness is a statement about the wilderness, not about the guaranteed zone. Hardness theorems and sufficient conditions are not rivals; they are two answers to different questions, and the census shows the space between them is almost the whole space.

### 1.4 The twist: exponential in k, polynomial in n

Here is the paragraph that keeps this chapter from being a story about walls. Vertex cover is NP-hard in n — and *easy in a different parameter*. Suppose we only need to know whether τ(G) ≤ k for a small k, and want the cover if so.

**The bounded search tree.** If any edge uv is uncovered, every vertex cover contains u or v — there is no third option. So: pick any uncovered edge uv, and *branch*: either u is in the cover (delete u, solve for k − 1) or v is (delete v, solve for k − 1). At a branch both children carry k − 1; when k reaches 0 with edges still uncovered, that leaf dies. The tree has depth at most k, branching factor 2, so at most 2^(k+1) − 1 nodes, each doing O(m) work: total time O(2^k·(n + m)) plus the same to verify the result. Recurrence T(k) ≤ 2T(k − 1) + O(m), unrolled — pattern P4 with the induction sitting in the exponent.

The lab ran this exact procedure on all 33,866 labeled graphs on 2 to 6 vertices, k set to the true cover size. Every run returned a valid cover of optimal size. The census's worst tree: **31 nodes — exactly 2^(k+1) − 1 at k = 4, attained by K₆ with one edge deleted** (cover size 4; the missing edge creates a "wrong branch" that must be explored to exhaustion before the right one wins). The bound is not slack; the machine found its tight case on its own. This is the **fixed-parameter tractability** paradigm of Downey and Fellows: exponential in the parameter k, polynomial in the data n — a different contract than NP-hardness forbids, and for many atlas problems the honest one. The chapter's last lecture returns to what survives; the exercise set builds the tree by hand.

**What to learn.** Definitions that bite: NP is about checking, not finding. The spine is one structure seen three ways — the reductions are easy because the problems share a skeleton, and that shared skeleton is what resists speed. Gallai's α + τ = n is the hinge. Hardness is a theorem with a proof you can audit, not an opinion. And the parameter world is real: 2^k·n is a *kind* of polynomial, whenever k is small. One question runs the chapter: *what exactly is the price of this problem, and in which currency?*

---
## Lecture 2 · Set Cover and the Harmonic Ceiling

Vertex cover's twin name haunts this lecture, but the problem is different and older than the spine: given a universe U of u elements and a family of sets, choose the fewest sets whose union is U. Set cover is NP-complete (Karp's original twenty-one), so we ask the surviving question: how well does the obvious algorithm do? The obvious algorithm is *greedy*: repeatedly take the set covering the most still-uncovered elements. This lecture proves the answer — greedy is within a factor H_u = 1 + 1/2 + ⋯ + 1/u of optimal — and then proves the darker half: no polynomial algorithm can do substantially better, unless P = NP. The pair of theorems is the chapter's cleanest specimen of *an approximation ceiling* — a problem where the reachable guarantee is known exactly, and where the natural greedy turns out to be essentially the best possible.

### 2.1 The problem, the algorithm, and a census to keep us honest

An instance is a universe U with |U| = u and sets S₁, …, S_t ⊆ U whose union is U. A *cover* is a subfamily with union U; OPT is the minimum cover size. Greedy: while uncovered elements remain, take the set adding the most new ones. Nothing could be more natural — and nothing about it promises anything. So the lab ran a census first: every covering system of at most three distinct nonempty sets over universes of size u = 1 to 5 — all **3,093** of them (1 + 5 + 45 + 361 + 2,681 by universe size) — computing greedy's picks against the true optimum, with ties broken toward the earliest set in the family's printed order. Result: **zero violations** of the bound this lecture is about to prove, and a maximum observed ratio of exactly **1.5** — witnessed by the family {[0,1], [0,2], [1,3]} on the universe {0,1,2,3}: greedy takes [0,1] (two new), then [0,2] (one new), then [1,3] (the last element) — three sets, while {[0,2], [1,3]} covers everything in two. Ratio 3/2, and 3/2 = H₂ exactly. The census says the bound is already tight at its floor; the theory to come will say the census never had a chance to violate it — and Exercise 4's ladder will show that the same census never had a chance to see the true ceiling either.

### 2.2 The harmonic bound, proved

**Theorem (Chvátal 1979; Lovász 1975).** Greedy set cover uses at most H_d · OPT sets, where d is the size of the largest set — in particular at most H_u · OPT.

**Proof (charging).** Run greedy. When a greedy move covers c new elements, charge each of them cost 1/c; each greedy move then contributes exactly 1 to the total cost, so the total charge over all elements equals the number of sets greedy used.

Now fix an optimal cover O₁, …, O_OPT, and *prune it into a partition*: assign every element of U to exactly one O_i containing it, and let O_i′ be the elements assigned to O_i. The O_i′ are disjoint, their union is U, and |O_i′| ≤ |O_i| ≤ d. Claim: the total charge landing on O_i′ is at most H_{|O_i′|}.

Order O_i′'s elements e₁, e₂, …, e_s by the time greedy covers them (every element gets covered — greedy ends with the universe covered). When greedy covers e_j, look at that moment: the elements of O_i′ not yet covered are e_j, e_{j+1}, …, e_s — exactly s − j + 1 of them, all currently uncovered, all sitting in one set O_i. Greedy covers the most uncovered elements of *any* set, so its move covers at least s − j + 1 new elements: c ≥ s − j + 1, and the charge to e_j is at most 1/(s − j + 1). Summing over j = 1, …, s: the charge on O_i′ is at most Σ_{j=1}^{s} 1/(s − j + 1) = H_s. ∎ (One line of averaging, pattern P10 — every element is priced by the crowd it arrived with.)

So greedy's count = total charge = Σ_i (charge on O_i′) ≤ OPT · H_d ≤ OPT · H_u. For the record and the lab: H₂ = 1.5, H₄ ≈ 2.0833, H₈ ≈ 2.7179, H₁₆ ≈ 3.3807, H₃₂ ≈ 4.0585, H₁₀₀ ≈ 5.1874 — the harmonic numbers grow like ln u, so the honest slogan is **greedy ≤ ln u + 1**.

**✎ Checkpoint 1.** Run the charging proof on the census's witness by hand: {[0,1], [0,2], [1,3]} on {0,1,2,3}, greedy order [0,1], [0,2], [1,3]. Charges: 1/2 each to elements 0 and 1 on the first move, then 1 to element 2 on the second move, then 1 to element 3 on the third move (total charge 1/2 + 1/2 + 1 + 1 = 3 = greedy's count). Under the optimal partition O₁′ = {0, 2} and O₂′ = {1, 3}, each optimal piece has size d = 2 and receives charge 1/2 + 1 = 3/2 = H₂, so the sharper bound H_d · OPT = H₂ · 2 = 3 is tight with zero slack; the looser bound H_u · OPT = H₄ · 2 ≈ 2.0833 × 2 ≈ 4.17 loses the extra 1.17 entirely when weakening H_d = H₂ to H_u = H₄.

### 2.3 The ceiling is real

Two results convert the bound from a comfort into a complete answer.

First, the bound describes *greedy* exactly: Slavík (1996) pinned greedy's worst-case ratio at **ln n − ln ln n + Θ(1)** — asymptotically tight for the algorithm itself, not just for the proof. The H_u ≈ ln u shape is not slack in the analysis; it is the algorithm's true face.

Second, no polynomial algorithm can pass substantially below it: Dinur and Steurer (2014) proved that approximating set cover within **(1 − ε) ln n is NP-hard for every ε > 0** — improving on the breakthrough threshold of Feige (1998), which reached the same barrier under the weaker assumption that NP has no quasi-polynomial algorithms. Read the two together: greedy achieves ln n + 1; the barrier says (1 − ε) ln n is unreachable; the additive gap is the constant 1 (and Slavík's −ln ln n correction). Unless P = NP, no polynomial algorithm — however clever, however ungreedy — beats the natural heuristic by more than a lower-order term. This is the theorem form of the lore that hard problems have *prices*, and the price is sometimes posted exactly.

The census's H₂ witness shows the ceiling at its smallest scale: inside that tiny world — at most three sets, universes of at most five elements — greedy never beat 1.5 on any of the 2,166 opt-2 systems. Read that scope honestly: it is the small census's ceiling, not a bound in OPT. Exercise 4's ladder baits greedy to five sets at OPT = 2 on a sixteen-element universe (ratio 2.5), and it telescopes without end — the ceiling that is *real* is the harmonic one, priced in set sizes, which §2.2 proved. For contrast, keep vertex cover in mind from Lecture 1: there the best ratio is 2 (maximal matching's cover — the Chapter 5 backfill proved it), and improving to 2 − ε is impossible *assuming the Unique Games Conjecture* (Khot–Regev 2008) — a hardness claim one confidence level softer than set cover's, which Lecture 5 revisits.

### 2.4 What to learn

Greedy is an *algorithm with a theorem attached*: the charging argument is the whole proof, and it turns a heuristic into a guarantee. The harmonic number is the exact shape of the price. And the Dinur–Steurer barrier is the modern face of NP-hardness: hardness not of solving, but of approximating — proved, as always, by a reduction (P25 again, this time constructing instances whose optimums encode constraint satisfaction). The pattern to keep: *when exactness dies, demand a ratio; when a ratio is achieved, ask whether the ceiling is lower*.

---

## Lecture 3 · Matroids: Where Greedy Is Exact

Set cover's greedy is a 1.5-factor sometimes-loser. Kruskal's greedy — sort edges by weight, take an edge if it does not close a cycle — is *never* wrong: it always returns a minimum spanning tree. Same algorithmic shape, opposite reliability. What exactly separates them? The answer is one of the most beautiful structures in combinatorics, and this lecture builds it: the matroid, the environment where greedy is provably exact, with a theorem (Rado–Edmonds) that closes the question in *both* directions.

### 3.1 Kruskal, and the question his algorithm begs

The lab's census first: all **770 connected labeled graphs** on 3, 4, and 5 vertices (4 + 38 + 728 by size), each with seeded integer weights (1 to 100, drawn in edge order by the lab's Lehmer generator — Part 3 reproduces them bit-for-bit). For every graph, Kruskal's total weight was compared against an exhaustive minimum spanning tree. Agreements: **770 of 770**. Zero mismatches. Kruskal's greedy is exact, always, and the census is the ritual before the theorem. The question: what property of "forests" makes greed infallible here and fallible for set cover?

### 3.2 The exchange axiom

An *independence system* on a ground set E is a family I of "independent" subsets with (I1) ∅ ∈ I and (I2) heredity: subsets of independent sets are independent. Forests of a graph (edge sets with no cycle) are the running example. A *matroid* adds the axiom that gives the lecture its title:

> **(I3) Exchange.** If A, B ∈ I with |A| < |B|, then some e ∈ B ∖ A has A ∪ {e} ∈ I.

Forests satisfy it — the lab verified the graphic matroid of K₄ exhaustively: **38 forests** among the 64 edge subsets, **463 ordered pairs A, B with |A| < |B|**, and every single pair admits an augmenting edge — zero counterexamples. The hand-sized instance to feel it: A = the 2-edge path 0–1–2, B = the 3-edge star at 0. B ∖ A = {0–2, 0–3}. Adding 0–2 to A closes the triangle 0–1–2 — not independent. But 0–3 does not: the star's second option saves the axiom. The proof that forests on V always satisfy (I3) is an exact component count: a forest F on n = |V| vertices has exactly c(F) = n − |F| connected components. Since |A| < |B|, the forest (V, A) has strictly more connected components than (V, B): c(A) = n − |A| > n − |B| = c(B). If every edge e ∈ B ∖ A had both endpoints inside the same connected component of (V, A), then every edge of B would lie inside a single A-component, so every B-component would be contained in a single A-component, forcing c(B) ≥ c(A) — a contradiction. Therefore at least one edge e ∈ B ∖ A joins two distinct connected components of (V, A), and adding e to A merges those two components without closing a cycle, so A ∪ {e} ∈ I. The exercise set revisits this count from the vertex side.

The non-example earns its place in the lab too: the family **{∅, {a}, {b}, {c}, {b, c}}** is hereditary but fails exchange — A = {a}, B = {b, c}: neither b nor c augments {a}. One missing edge of the axiom; watch what it does to greedy in §3.3.

Two more examples to keep the concept honest: the *uniform matroid* (independent = all sets of size ≤ k, every k-element set exchangeable); the *partition matroid* (a ground set split into blocks, independent = at most one element per block — matching's natural habitat, and Lecture 4's currency).

### 3.3 Rado–Edmonds: greedy optimal if and only if matroid

**Theorem (Rado 1957; Edmonds).** Let (E, I) be an independence system and consider weights w: E → ℝ. Greedy (sort descending, take an element if it keeps the set independent) maximizes total weight over all independent sets **for every nonnegative weight function** if and only if (E, I) is a matroid. (Nonnegativity is the honest domain, and it is load-bearing: on the uniform matroid U₂,₃ — independent = size ≤ 2 — with weights (1, −5, −5), greedy takes the 1, then a −5 that keeps the set independent: total −4 against the optimum +1, the single weight-1 element. With negative weights in play, greedy fails *on a genuine matroid* — take-if-independent never refuses — and the theorem's domain is w ≥ 0.)

**The "if" direction, proved.** First, greedy's output G is *maximal* — it stops only when nothing augments — and in a matroid all maximal independent sets have the same size (the standard consequence of exchange: if |A| < |B| both maximal, some e ∈ B∖A augments A, contradicting maximality). Fix r = |G| and let O be any independent set with |O| = r — an optimal solution, which exists because with weights nonnegative an optimum may be taken *maximal* (extending an independent set never lowers the total), and in a matroid all maximal independent sets share the size r = |G|; take O of maximum weight among size-r independent sets.

Claim: for every k ≤ r, the sum of greedy's first k weights is at least the weight of *any* independent k-set. Induction on k. k = 1: greedy's first pick g₁ has maximum weight among all elements (any single element is independent by heredity from ∅). Step: let A be any independent set with |A| = k; greedy's prefix is B = {g₁, …, g_{k−1}}, |B| = k − 1 < k = |A|. Exchange (I3) hands us an element a ∈ A ∖ B with B ∪ {a} independent. By heredity (I2), every earlier prefix B′ ⊆ B also had B′ ∪ {a} ∈ I, so a could not have been inspected and rejected before step k; thus at step k, a was still *available* to greedy, and greedy chose the heaviest available: w(g_k) ≥ w(a). By induction, Σ_{i≤k−1} w(g_i) ≥ w(A ∖ {a}) (an independent (k−1)-set), hence Σ_{i≤k} w(g_i) ≥ w(A ∖ {a}) + w(a) = w(A). At k = r this reads Σ_{i≤r} w(g_i) ≥ w(O): greedy is optimal. ∎

The proof is the exchange axiom *running forward in time* — every greedy choice is certified against the eventual optimum at the moment it is made. That is what "greedy is exact" means mechanically, and why the axiom is exactly the right statement: P18 in its purest form, an algorithmic proof where the invariant is future-proof.

**The "only if" direction, constructed.** Suppose exchange fails: A, B ∈ I, |A| < |B|, no element of B ∖ A augments A. Choose weights with 1 < c/c′ < |B|/|A|: weight c on A's elements, c′ on B ∖ A's elements, and 0 on E ∖ (A ∪ B). Greedy — which prefers the heavier class — takes all of A (every subset of A is independent by heredity), then tries B ∖ A element by element: every attempt fails, by the failed exchange, and weight-0 elements add nothing. Greedy's total is therefore c|A| < c′|B| ≤ c|B ∩ A| + c′|B ∖ A| = w(B), the weight of the independent set B. Greedy is suboptimal for these weights. ∎

The lab's witness is this construction with |A| = 1, |B| = 2, c/c′ = 3/2: the family {∅, {a}, {b}, {c}, {b,c}} with weights **a = 3, b = c = 2**. Greedy takes a (weight 3); b fails ({a, b} is not in the family); c fails; total 3. Optimal: {b, c}, total 4. Machine-verified — and now understood: *the failure of greedy is exactly the failure of the axiom, element for element*. Set cover sits on the far side of this boundary: its greedy optimizes a *moving* target — elements newly covered, a different objective after every step — not a fixed weight function over an independence system, and no exchange-style structure survives to rescue it; the census's 3/2 witness is the smallest symptom of the difference.

One theorem more, stated: **matroid intersection** — the common independent sets of two matroids — is solvable in polynomial time (Edmonds), and bipartite matching is the intersection of two partition matroids (one per side of the bipartition, "at most one edge at each left vertex" ∩ "at most one at each right vertex"). The assignment problem of Lecture 4 is *weighted* bipartite matching — a hint of how far this theory reaches.

### 3.4 What to learn

The matroid axioms are not abstract decoration; they are the exact boundary of greedy's reliability, in both directions, with proofs that construct the correspondence edge by edge. Kruskal is exact because forests exchange; set cover is a 3/2-loser at OPT = 2 because its structure does not. When you meet a greedy algorithm in the wild, the honest first question is now: *what is the independence system, and does it satisfy exchange?* The answer decides whether you owe the world a proof of optimality or an apology with a ratio attached.

---
## Lecture 4 · Flows with Costs: Successive Shortest Paths and the Assignment Problem

Chapter 5 moved flow: the maximum volume from s to t, with the min-cut theorem pricing the ceiling. This lecture adds a currency. Each arc now has a capacity *and* a cost per unit of flow, and the question becomes: send a prescribed value v from s to t as *cheaply* as possible. The engine is Chapter 5's residual network wearing a price tag, and the algorithm — successive shortest paths — is the cleanest example in the Atlas of a proof-carrying algorithm: at every moment it maintains a certificate that no cheaper flow of the same value exists.

### 4.1 The problem, and the engine

An instance is a directed network with arc capacities c(e) ≥ 0 and costs w(e) (possibly negative — discounts are legal), a source s, a sink t, and a demand v. A *feasible flow* of value v respects conservation at every internal vertex and every capacity; the *cost* is Σ f(e)·w(e) over arcs. Min-cost flow: minimize cost.

The engine, **successive shortest paths (SSP)**: start at the zero flow; while the value is below v, find a cheapest s–t path in the *residual network* — forward along each arc with unused capacity, at cost w(e); *backward* along each arc carrying flow, at cost −w(e), representing the right to change your mind and take a refund — and push as much as the path allows, capped by the remaining demand. Backward arcs are pattern P16's whole point: augmentation is not accumulation but *correction*, and the residual network keeps every correction available at its honest price.

The lab's witness network has nine arcs on five vertices (Part 4 prints them all): among them 0→1 (capacity 1, cost 1), two parallel arcs 0→2 (costs 3 and 1), two parallel 2→3 (costs 9 and 3), 1→4 (cost 4), 3→4 (capacity 1, cost 2), and a return arc 3→0. Demand 2. SSP's run, machine-verified end to end: the first shortest path is 0→1→4 at cost 5, pushing the single unit of arc 0→1; the second is 0→2 (the cost-1 parallel) → 2→3 (the cost-3 parallel) → 3→4 at cost 6. Two iterations, total cost **11**, final arc flows **[1, 1, 0, 0, 1, 0, 1, 0, 1]** — the two expensive-looking parallel arcs (costs 9 and 8) untouched, their cheap siblings used to capacity. Note what the greedy eye would have missed: the *first* unit's cheapest route costs 5, but the second unit's costs 6 — prices rise as the cheap capacity fills, and the algorithm that grabs shortest paths in the *residual* network is pricing exactly this changing market.

### 4.2 Why SSP is safe: integrality, termination, and the certificate

Three facts, each visible in the witness run.

**Integrality.** Every push moves the minimum of integer capacities along a path, so every arc flow stays an integer: min-cost flow with integer capacities has an integer optimum. (The Chapter 5 lesson, inherited wholesale — and the reason Lecture 4.3's assignment problem becomes a flow problem at all.)

**Termination.** Each iteration pushes at least 1 unit (integrality again, assuming integer capacities and demand), so at most v iterations: polynomial.

**The optimality certificate (pattern P17).** A feasible flow f of value v is minimum-cost *if and only if* its residual network G_f contains no negative-cost directed cycle. The constructive half: if vertex potentials d(·) exist such that every residual arc (u, v) of G_f has nonnegative *reduced cost* w_f(u, v) + d(u) − d(v) ≥ 0, then no residual cycle is negative (potentials telescope to zero around any cycle), and f is minimum-cost. To prove the optimality claim, let f′ be any other feasible flow of the same value v. The difference Δf = f′ − f has net flow zero at every vertex (including s and t, since both flows have value v) and respects the residual capacities of G_f: put Δf(u, v) = f′(u, v) − f(u, v) > 0 on forward residual arcs where f′ > f, and Δf(v, u) = f(u, v) − f′(u, v) > 0 on backward residual arcs where f′ < f. Thus Δf is a nonnegative circulation in G_f, and its cost in G_f is exactly cost(f′) − cost(f). Because every vertex has net inflow equal to net outflow under Δf, the telescoping sum Σ Δf(u, v) · (d(u) − d(v)) over G_f's arcs vanishes identically, so cost(f′) − cost(f) = Σ Δf(u, v) · w_f(u, v) = Σ Δf(u, v) · (w_f(u, v) + d(u) − d(v)) ≥ 0, since Δf ≥ 0 and every reduced cost is ≥ 0 on every residual arc. Hence cost(f′) ≥ cost(f): the potentials are a certificate the skeptic can check arc by arc — the same min–max spine as Chapter 5's, now with prices. The witness's final flow carries potentials **d = (−6, −4, −5, −2, 0)** on vertices 0 through 4: every unsaturated forward arc has nonnegative reduced cost (the cost-1 arc 0→2 gets reduced cost exactly 0, as do the used cost-4 and cost-3 arcs — the arcs a *tight* optimum must use), and every arc carrying flow has nonpositive reduced cost in the forward direction — the complementary-slackness picture in miniature, machine-checked arc by arc. SSP maintains such potentials *by construction*: it augments along shortest paths, so the shortest-path distances themselves serve as the next round's potentials — which is why the search must be Bellman–Ford and not Dijkstra whenever reduced costs go negative.

The chapter's appendix records the wider census: forty designed feasible five-vertex networks, SSP against an exhaustive minimum on every one — **40 of 40 agreements**, every final residual negative-cycle-free, on average 1.68 iterations.

### 4.3 The assignment problem, paid in flow

The assignment problem: n rows, n columns, a cost matrix; choose one cell per row and per column, minimizing the total. It is the oldest scheduled problem in optimization and the cleanest demonstration that a combinatorial question becomes a flow question the moment you draw the right picture.

The flow model: a source joined to each row (capacity 1, cost 0), each row joined to each column by an arc of capacity 1 and cost c(row, column), each column joined to the sink (capacity 1, cost 0). Flows of value n are exactly the legal assignments — integrality makes the 0/1 structure automatic — and min-cost flow of value n is the optimum assignment. The lab's worked witness is the matrix

```
10  11   2   8
15  12  10   3
 8  19  14   9
15  12   2  12
```

whose optimum is **24**, achieved by the permutation **[1, 3, 0, 2]** — row 0 takes column 1 (cost 11), row 1 takes column 3 (cost 3), row 2 takes column 0 (cost 8), row 3 takes column 2 (cost 2). SSP on the flow model found exactly this assignment in four augmentations, one per row, and the brute-force sweep over all 24 permutations agrees: 24 is optimal. The lab's census extends the check: **eight seeded 4×4 matrices, SSP versus brute force, 8 of 8 agreements** (optima 74, 72, 51, 33, 30, 47, 28, 50 — each reached in four iterations).

The classical direct algorithm — the Hungarian method (Kuhn 1955) — solves the same problem by exactly these potentials, maintained by hand a decade before flow theory explained what they were. And the matroid lens of Lecture 3 explains the boundary: assignment is weighted bipartite matching, the intersection of two partition matroids, polynomial by Edmonds' intersection theory — the non-bipartite version is Lecture 6's mountain.

### 4.4 The frontier, honestly

Two statements record where the asymptotics stand, so the chapter does not teach its students a museum piece as if it were the news. For maximum flow: the preflow-push algorithm of Goldberg and Tarjan runs in O(V²E) — the standard text bound, with faster special-purpose results known. And the genuine news: min-cost flow is solvable in *almost-linear* time — the 2022 breakthrough of Chen, Kyng, Liu, Peng, Probst Gutenberg, and Sachdeva (FOCS 2022), with a deterministic version in 2023 — "almost-linear" meaning within subpolynomial factors of the input size. The chapter still teaches SSP, and says why: SSP is the algorithm whose every run carries a checkable certificate (integrality, potentials, no negative cycle), whose proof is four paragraphs, and whose structure — the residual network as a market in past mistakes — is the idea that generalizes. The frontier algorithms trade that transparency for asymptotics; an Atlas reader should know both prices. **What to learn.** Costs ride the residual network; backward arcs price regret; potentials are duality made computable; integrality is the bridge between continuous-looking optimization and combinatorial objects; and the assignment problem was a flow problem all along, waiting for its picture to be drawn.

---

## Lecture 5 · The Traveling Salesman, Priced: Approximation with Guarantees

Hardness, met honestly, changes the question rather than ending the conversation: *if the exact optimum is out of reach, what can be guaranteed?* This lecture builds the two classical guarantees for the metric traveling salesman — the factor 2 of the doubled tree and the factor 3/2 of Christofides, each proved in full — and then the modern cautionary tale: MaxCut's 0.878, the one approximation constant in this chapter you can compute to five decimals yourself, and the conjecture that says it cannot be beaten.

### 5.1 The doubling argument, and the factor 2

The traveling salesman problem: given n points with distances, find the cheapest tour visiting each once. It is NP-hard in brutal generality — set every distance to 1 and a cost-n tour exists exactly when the graph has a Hamilton cycle, so the spine of Lecture 1 already covers it — but the *metric* case (distances obeying the triangle inequality) is a different country, and its guarantees start from one observation:

**Theorem.** In the metric TSP, the minimum spanning tree has weight at most OPT.

**Proof.** Delete one edge from the optimal tour: what remains is a spanning path — connected, acyclic, visiting everything — hence a spanning tree, of weight OPT − (a nonnegative edge). The minimum spanning tree weighs no more. ∎

**The 2-approximation.** Take a minimum spanning tree T, *double* every edge: all degrees become even, so the multigraph has an Euler circuit (the lab's Hierholzer walk — Chapter 2's splicing, upgraded to carry weights). Walk the circuit, and shortcut past revisited vertices: the triangle inequality makes each shortcut no dearer than the segment it replaces. The resulting tour costs at most the walk, which costs 2·w(T) ≤ 2·OPT. ∎

The lab's census (Part 5): twelve instances — the witness plus eleven seeded, n = 5 to 8, lattice points drawn by the lab's Lehmer generator, Manhattan distances, exact optima by exhaustive permutation search. Every instance: 2-approx ratio ≤ 2, worst observed **1.5** — practice runs far inside the guarantee, and the exercise set asks you to think about why. The chapter's witness instance — the five points (4,2), (5,0), (1,1), (0,5), (0,6) — has MST weight **13** and optimum **22**, and the doubled-tree tour lands on cost **22**: the ratio is exactly 1 here, the shortcutting luckiest possible. The guarantee is 2; the instance says do not confuse the worst case with the case.

### 5.2 Christofides: the odd vertices, matched

The doubling argument wastes half its material — every tree edge walked twice. Christofides' repair uses the matching theory of Chapter 5 at exactly one point.

**The parity fact.** The set of *odd-degree* vertices of any tree is even in size (the degree sum 2(n − 1) is even, so odd degrees pair off — pattern P9 as bookkeeping).

**The matching lemma, proved.** Let T be a minimum spanning tree, O its odd-degree vertex set, and let M be a minimum perfect matching on O. Then w(M) ≤ OPT/2.

**Proof.** Take the optimal tour and read off the order in which it visits the vertices of O: o₁, o₂, …, o_{2k}, cyclically. The tour segments between consecutive O-vertices — the stretches of tour between o₁ and o₂, o₂ and o₃, and so on — number 2k, and they partition the tour's edges. Now alternate: the odd-numbered segments form one perfect matching on O (each o_i reached by exactly one odd segment and left by one — the cyclic alternation guarantees the pairing is a genuine perfect matching), the even-numbered segments a second. By the triangle inequality, each matching's cost is at most the cost of its own segments — the matching edge o_i o_j is priced by the sum of the tour edges along its segment, which is exactly what the metric licenses; together the two matchings cost at most OPT; so the *cheaper* one costs at most OPT/2 — and the minimum matching M costs no more. ∎

**The 3/2-approximation (Christofides 1976; Serdyukov 1978).** Union T with the minimum perfect matching M on its odd vertices: connected, all degrees even — an Euler circuit exists. Walk it, shortcut: cost ≤ w(T) + w(M) ≤ OPT + OPT/2 = 3/2 · OPT. ∎

The lemma is *exactly* tight, and the lab's witness is the proof: the five-point instance above has odd set **{1, 4}** (vertices (5,0) and (0,6)), whose single-pair perfect matching costs |5 − 0| + |0 − 6| = **11 = OPT/2 exactly** — the tour's two O-segments both cost 11, both matchings tie, and there is no slack anywhere. Yet the resulting Christofides tour costs **24** (ratio 24/22 ≈ **1.091**): the tight lemma, the comfortable final guarantee. Across the twelve-instance census: perfect matching ≤ OPT/2 with **12 of 12** holding, worst Christofides ratio **1.125**, odd sets even every time. For forty-five years 3/2 stood as the final word; in 2021 Karlin, Klein, and Oveis Gharan crossed it — a *randomized* algorithm with expected ratio 3/2 − ε for an ε > 10⁻³⁶ (yes, thirty-six zeros: the first improvement, and a hair's width). Deterministically, 3/2 is still the frontier.

**✎ Checkpoint 1.** Compute the witness instance's MST by hand (Prim from (4,2) works; the answer is 13 with odd vertices (5,0) and (0,6)) and verify the matching arithmetic: |5−0| + |0−6| = 11, twice 11 = 22 = OPT. The lemma's proof needs the *cyclic* order of O along the tour because the 2k vertices o₁, o₂, …, o_{2k} divide a closed cycle into 2k edge-disjoint segments (including the wrap-around segment from o_{2k} back to o₁), which split into two complete matchings of k pairs each: {o₁o₂, …, o_{2k−1}o_{2k}} and {o₂o₃, …, o_{2k}o₁}. A merely linear path from o₁ to o_{2k} has only 2k − 1 segments, so its even-numbered segments leave o₁ and o_{2k} unpaired and fail to form a second perfect matching on O.

### 5.3 MaxCut and the exact constant 0.878

One more problem, the modern emblem of approximation theory. **MaxCut**: split a graph's vertices into two camps to maximize the number of edges crossing. NP-hard (statement). The trivial floor: cut each vertex by independent fair coin flips — every edge crosses with probability 1/2, so the expected cut is at least half the optimum (pattern P10 in its cheapest form).

**The Goemans–Williamson algorithm (1995), statement.** Relax to a semidefinite program: place a unit vector per vertex, maximize the sum over edges of (1 − ⟨u_i, u_j⟩)/2; solve the SDP; round by a uniformly random hyperplane through the origin. The guarantee: the expected cut is at least **0.87857** times the optimum, and the constant is *computable*, not mysterious: for an edge whose SDP unit vectors make angle θ ∈ (0, π], the hyperplane separates its endpoints with probability θ/π, while the SDP objective prices the edge at (1 − cos θ)/2 = sin²(θ/2) — so the per-edge ratio is **θ/(π sin²(θ/2))**, whose minimum over 0 < θ ≤ π the lab locates at θ ≈ **2.3311**, value **0.87857** (Exercise 11 makes you derive every piece; the machine only checks the calculus).

And the optimality half, one confidence level softer than set cover's: assuming the **Unique Games Conjecture** (Khot 2002 — a hardness conjecture about a certain constraint system, still open), no polynomial algorithm approximates MaxCut within any factor above 0.878 (Khot–Regev 2008). Set cover's ceiling is unconditional (unless P = NP); MaxCut's is conditional (unless UGC fails); the honest atlas prints both with their price tags. If the conjecture falls, 0.878 may yet be beaten — the watermark tells you exactly what to watch.

### 5.4 What to learn

Approximation is not consolation; it is a different contract with the same rigor: a ratio, proved. The doubling argument converts a spanning structure into a tour and pays a factor of 2 for the conversion; Christofides pays only 1/2 more by repairing parity with matching — the whole chapter's cast (trees, parity, matching, shortcuts) assembled in one bound. The tight witness teaches the difference between a tight *lemma* and a tight *guarantee*. And MaxCut shows the modern endgame: exact constants, computed not looked up, with optimality conjectured on record. The meta-pattern, worth more than any single bound: *when a problem's exact solution is provably unreachable, the mathematics does not stop — it changes currency, and the exchange rate becomes the theorem.*

---
## Lecture 6 · Matching in General Graphs: the Search That Stops Lying

Chapter 5 built the bipartite matching engine and then told the truth about its frontier (§3.3): beyond bipartite graphs, Berge's lemma still guarantees that every nonmaximum matching has an augmenting path — but the parity-labeled *search* can falsely report that none exists, and Exploration X2 sent you hunting the lie. This lecture is the promised payment in full. First the lie, caught in the act, with its exact labels on the table. Then Edmonds' blossoms — the contraction that repairs the search, the first polynomial-time algorithm for a problem that had resisted every attempt, and the birth of polyhedral combinatorics. Then Tutte's 1-factor theorem, the min–max obstruction to a perfect matching, proved in full — the chapter's last long proof, and the one that turns "no augmenting path" from an algorithm's report into a structural theorem with a certificate you can check by hand. The lecture closes the chapter's books: what the matching story now covers, and what the Atlas still owes.

### 6.1 The search that lies, caught in the act

Recall the engine (Chapter 5's Lecture 2). Given a matching M and an exposed vertex r, grow the *alternating tree*: label r **A**; repeatedly, from every A-vertex cross every *unmatched* edge to label a new vertex **B**; from every B-vertex cross its *matched* edge to label the partner **A**. Two exits: an unmatched edge from an A-vertex to an exposed vertex reads off an M-augmenting path — augment and restart — or the tree stops growing and the search reports "no augmenting path from r". In a bipartite graph the second exit is honest, and Chapter 5 built the certificate that proves it. In a general graph it can be a lie — and Berge's lemma (Chapter 5, L3.3) is what makes the lie detectable: if M is not maximum, an augmenting path *does* exist, so a "not found" report is a failure of the search, not a fact about the graph.

Figure 1 shows the smallest lying state. The **paw** — the triangle 0-1-2 with a pendant vertex 3 at 0 — with M = {0–1} and root 2: the labels run 2A, then 1B and 0B (the unmatched edges 2–1 and 2–0), and there is the tell: 0's matched partner is 1 — the matched edge 0–1 lies *inside* side B, the B→A step cannot fire, and the tree dies with A = {2}. No unmatched edge from 2 reaches an exposed vertex, so the search reports stuck. The report is false: 2-1-0-3 alternates (unmatched 2–1, matched 1–0, unmatched 0–3) and ends at the exposed 3 — an M-augmenting path three edges long, sitting in plain sight. The mirror state (M = {0–2}, root 1) lies identically.

```svg
<svg xmlns="http://www.w3.org/2000/svg" width="520" height="300" viewBox="0 0 520 300">
  <line x1="130" y1="90" x2="390" y2="90" stroke="#333" stroke-width="2"/>
  <line x1="130" y1="90" x2="260" y2="190" stroke="#333" stroke-width="2"/>
  <line x1="390" y1="90" x2="260" y2="190" stroke="#333" stroke-width="5"/>
  <line x1="260" y1="190" x2="260" y2="252" stroke="#333" stroke-width="2"/>
  <path d="M148 82 L 372 82" fill="none" stroke="#b03030" stroke-width="3" stroke-dasharray="7,5"/>
  <path d="M378 104 L 276 176" fill="none" stroke="#b03030" stroke-width="3" stroke-dasharray="7,5"/>
  <path d="M260 196 L 260 244" fill="none" stroke="#b03030" stroke-width="3" stroke-dasharray="7,5"/>
  <circle cx="130" cy="90" r="7" fill="#333"/>
  <circle cx="390" cy="90" r="7" fill="#333"/>
  <circle cx="260" cy="190" r="7" fill="#333"/>
  <circle cx="260" cy="252" r="7" fill="#b03030"/>
  <g font-family="monospace" font-size="14" fill="#333" text-anchor="middle">
    <text x="92" y="76">2 A</text>
    <text x="428" y="76">1 B</text>
    <text x="204" y="214">0 B</text>
    <text x="292" y="268">3 (exposed)</text>
  </g>
  <g font-family="monospace" font-size="13" fill="#333" text-anchor="middle">
    <text x="325" y="128">matched 0&#8211;1, inside side B</text>
    <text x="260" y="294">the search reports stuck; the red dashes are the real augmenting path 2-1-0-3</text>
  </g>
</svg>
```

*Figure 1. The paw's lying state: M = {0–1}, root 2. The matched edge 0–1 joins two B-labeled vertices, the tree cannot grow, the search reports "no augmenting path" — and the alternating path 2-1-0-3 (dashed) augments the matching anyway.*

One edge up, the **pendant C₅** — the cycle 0-1-2-3-4-0 plus pendant 5 at 0 — supplies the second kind of tell. With M = {2–3, 4–0} and root 1: labels 1A; 0 and 2 become B (unmatched edges from 1); 4 becomes A (0's matched partner) and 3 becomes A (2's matched partner). Now side A contains the unmatched edge 3–4 — *an unmatched edge inside side A*, the second tell — and no A-vertex touches the exposed 5, whose only edge goes to 0, a B-vertex. Stuck, says the search; stuck it is not: 1-2-3-4-0-5 alternates (unmatched, matched, unmatched, matched, unmatched) and augments. The mirror state (M = {0–1, 2–3}, root 4) lies the same way.

The lab enumerated every state exhaustively on both graphs — every nonmaximum matching, every root — and there are exactly **four lying states**, two per graph, one per symmetry class each: the paw's two (matched edge inside B) and the pendant C₅'s two (unmatched edge inside A). Both tells are the same event: an **odd alternating cycle** closing inside the tree. Around an odd cycle the alternating structure runs out of room — parity cannot be assigned consistently around an odd loop — and the labels the tree hands out stop meaning what they mean in bipartite graphs. That is the entire wall Chapter 5's bipartite proofs lean on, seen at zero distance.

### 6.2 Edmonds' blossoms: contraction as the repair

The repair is Edmonds' (1965), and it is one move. A **blossom** is an odd alternating cycle found by the search — in the pendant C₅ state above, the cycle 1-2-3-4-0-1 (three unmatched edges, two matched, odd length, based at the root). Edmonds' move: *contract the blossom to a single pseudovertex and keep searching in the contracted graph; when an augmenting path turns up there, lift it back through the blossom.* The mathematical content of the repair is a two-line parity fact, worth stating as a lemma because it is the whole engine.

**Lemma (parity switching).** Let C be an odd alternating cycle in G with respect to M. For any two vertices u, v of C there is an alternating u–v path along C starting with an unmatched edge, and another starting with a matched edge: walk one way around C or the other, and the odd length is exactly what makes the two walks' parities differ.

**Proof.** The two u–v arcs of the cycle partition it into walks of opposite parity sum (their lengths add to |C|, which is odd). Alternation is preserved along the cycle because the cycle alternates: each arc, read from u, is an alternating walk, and its first edge is the cycle edge at u on one arc and the other cycle edge at u on the other arc — opposite types, since the cycle alternates at every vertex, u included. ∎

So whatever parity the rest of an augmenting path demands at the point where it enters a contracted blossom, the inside can supply it: the blossom is a parity switcher, and contraction plugs it in. More precisely, a blossom C discovered during the alternating-tree search has a unique base b (the unique vertex of C not incident to any matched edge of C) connected to the tree's exposed root by an even-length alternating stem P₀; if we first switch M along P₀ to reduce to the case where b itself is exposed, then M has an augmenting path in G if and only if the contracted matching M/C has one in G/C — any augmenting path in G/C visiting the pseudovertex v_C leaves v_C along an unmatched edge incident to some vertex w ∈ C, and the parity-switching lemma supplies the even-length alternating path inside C from the exposed base b to w that lifts the path back to G. Consequently, the search may contract C and continue without losing or inventing augmentability. The remaining bookkeeping (that a completed Hungarian forest with no further blossoms or augmenting steps certifies maximality, the certificate machinery now known as the Tutte–Berge–Edmonds theory) is a careful induction that this chapter cites to Edmonds' two 1965 papers — "Paths, Trees, and Flowers" and the matching polyhedron paper, the birth of polyhedral combinatorics — rather than re-proving; the perfect-matching case of the certificate is §6.3's theorem, proved in full below. What this chapter proves is the parity core, and what the lab does is check the implementation against the truth.

The lab's engine (a faithful port of the classical algorithm, adjacency scanned in ascending order) runs the repair on the chapter's specimens. The paw from the empty matching: the first search finds the single-edge augmenting path 0–1 at once; the second search, rooted at 2, meets the blossom 2-0-1 (unmatched 2–0, matched 0–1, unmatched 1–2 — labels 2A, 0B, 1B with the matched edge inside B), contracts it, finds the pseudovertex joined to the exposed 3, and lifts back through the cycle to the true path 2-1-0-3 — augmenting to the perfect matching **{0–3, 1–2}**. The pendant C₅ from the empty matching returns the perfect matching **{0–5, 1–2, 3–4}**, the last augmentation through a contraction. The Petersen graph — the outer 5-cycle on 0–4, the inner star joining i+5 to ((i+2) mod 5)+5, spokes i–(i+5) — returns the perfect matching **{0–1, 2–3, 4–9, 5–7, 6–8}**: the star's 5-cycle of inner vertices is one big blossom in the middle of the run, and the engine steps through it. And the census: against an exact bitmask dynamic program on **all 33,866 labeled graphs on 2 to 6 vertices, zero mismatches and zero invalid matchings** — plus thirty seeded instances on 10 and 12 vertices, all agreeing. Implementation reality matches the cited theory everywhere the machine can see. For practice, tuned implementations have made the engine fast — Blossom V (Kolmogorov 2009) is the standard modern one — and the algorithm's polynomial running time, unremarkable now, was the shock of 1965: a problem that looked irreducibly exponential fell to parity bookkeeping, and the lesson (clever certificates can beat brute force *provably*) is the founding document of this chapter's entire worldview.

### 6.3 Tutte's 1-factor theorem, proved in full

Blossoms find matchings; Tutte's theorem says when a perfect matching — a *1-factor* — exists at all, and the statement is the perfect instance of pattern P17: an obstruction that is exactly tight, every failing graph failing for a visible structural reason.

**Theorem (Tutte 1947).** A graph G has a perfect matching if and only if for every set S of vertices, the number odd(G − S) of odd-order components of G − S is at most |S|.

The lab census first: every labeled graph on 4 and on 6 vertices — 32,832 of them (64 + 32,768). On 4 vertices, **37** have a perfect matching and **27** do not; on 6, **24,823** and **7,945**. The census checked the equivalence both ways on every graph: zero violations. Now the proof.

**(⇒) Necessity, by pigeonhole.** Let M be a perfect matching and S any vertex set. Take any odd component C of G − S: the edges of M that lie completely inside C pair up an even number of vertices of C, and because |C| is odd, at least one vertex of C must be matched by M to a vertex outside C. Since components of G − S have no edges between them in G, any edge leaving V(C) has its other endpoint in S; thus at least one vertex of C is matched to a partner in S. Because M is a matching, two distinct odd components cannot share the same partner in S, so the odd components of G − S inject into S: odd(G − S) ≤ |S|. ∎

**(⇐) Sufficiency, by induction on n = |V|.** Suppose the condition holds throughout. The base n = 0 is the empty matching, perfect. For the induction, three moves and an assembly.

*Move 1: the vertex count is even.* S = ∅ gives odd(G) ≤ 0: G has no odd-order components, so n is even. In particular ∅ is a set with odd(G − ∅) = |∅| = 0, so *equality sets exist*. Choose S maximal by inclusion among the sets with odd(G − S) = |S|.

*Move 2: every component of G − S is odd.* Suppose not: let C be an even-order component and x any vertex of C. In G − (S ∪ {x}), everything outside C is untouched, so its odd components are exactly the |S| odd components of G − S other than C (C contributed none, being even); and C − x has odd order, so it has at least one odd component. Hence odd(G − (S ∪ {x})) ≥ |S| + 1 = |S ∪ {x}|, while the hypothesis caps it at |S ∪ {x}|: equality — contradicting the maximality of S, since S ∪ {x} is a strictly larger equality set. So all components of G − S are odd, and there are exactly |S| of them.

*Move 3: every component of G − S is factor-critical* (deleting any one of its vertices leaves a graph with a perfect matching). Let C be a component and x ∈ C; suppose C − x has no perfect matching. The graph C − x has fewer than n vertices, so the induction hypothesis applies to it, and its failure gives a set T with odd((C − x) − T) > |T|. Parity sharpens this: |C − x| is even, so odd((C − x) − T) has the same parity as |T|, and the strict inequality forces odd((C − x) − T) ≥ |T| + 2. Now set W = S ∪ T ∪ {x} and count G − W: the components of G − S other than C survive untouched (odd, |S| − 1 of them), and the components of (C − x) − T appear inside; so odd(G − W) ≥ (|S| − 1) + (|T| + 2) = |S| + |T| + 1 = |W|. The hypothesis caps it at |W|: equality again — and W ⊋ S contradicts maximality. So C − x has a perfect matching for every x, which is factor-criticality.

*The assembly: a matching saturating S, then the pieces.* Build the auxiliary bipartite graph H: left side S, right side the odd components of G − S, and s adjacent to component C iff s has a neighbor in C. Hall's condition holds: for any nonempty T ⊆ S, let U = S ∖ T and look at G − U. Every component of G − S with no neighbor in T survives intact as an odd component of G − U (it has no edges to T, and deleting U cannot connect anything to it), and there are |S| − |N(T)| of them, where N(T) is T's neighborhood in H. If |N(T)| < |T|, then odd(G − U) ≥ |S| − |N(T)| > |S| − |T| = |U| — violating the hypothesis. So |N(T)| ≥ |T| throughout, Hall gives a matching of H saturating S, and since the components number exactly |S| (Move 2), the matching pairs every s ∈ S with a distinct component C_s. For each s pick a neighbor v_s ∈ C_s (one exists, by adjacency), delete v_s from C_s, and take the perfect matching of C_s − v_s that factor-criticality provides (Move 3). The union — the edges s–v_s together with the internal perfect matchings — covers every vertex exactly once: a perfect matching of G. ∎

Two remarks the proof begs to make. First, the proof is *constructive in structure*: the equality set S, the factor-critical components, and the auxiliary bipartite matching are exactly what the blossom algorithm's terminated forest computes — Tutte's theorem is the certificate the engine's silence reports. Second, maximality of S is load-bearing, and the lab's worked instance shows where.

**The worked instance.** Take two 5-cycles — 0-1-2-3-4-0 and 5-6-7-8-9-5 — bridged by the single edge 0–5: ten vertices, and the theorem's anatomy is visible end to end. The graph has perfect matchings ({1–2, 3–4, 0–5, 6–7, 8–9} is one), and the machine finds the maximal equality sets: **{0,1,3}, {0,2,3}, {0,2,4}, {5,6,8}, {5,7,8}, {5,7,9}** — six of them, all with odd(G − S) = |S| = 3. Run the proof on S = {0,1,3}: G − S has components {2}, {4}, and the second C₅ on {5,…,9} — all odd, three of them (Moves 1–2 hold with equality, maximality confirmed: adding any vertex collapses the count below the size, since it splits or shrinks odd components into even remainders). Each component is factor-critical (Move 3): the singletons trivially, the C₅ machine-verified — delete any vertex and the remaining four form a path with a perfect matching. The auxiliary bipartite graph: 0 is adjacent to the {4}-component (edge 0–4) and to the C₅ (edge 0–5); 1 to {2} (edge 1–2); 3 to {2} (edge 3–2) and to {4} (edge 3–4). The matching saturating S pairs 1 → {2}, 3 → {4}, 0 → C₅; the assembly picks neighbors 1–2, 3–4, 0–5, deletes 2, 4, 5 from their components, and matches the C₅'s remainder: {6–7, 8–9}. The result is the perfect matching {1–2, 3–4, 0–5, 6–7, 8–9} — built by the proof, not found by search. Now the trap: {0,1} is *also* an equality set (G − {0,1} has the path 2-3-4 and the C₅, both odd: 2 = |{0,1}|), but it is not maximal, and its component 2-3-4 — the three-vertex path — is **not factor-critical**: delete the middle vertex 3 and two isolated vertices remain, no perfect matching. Move 3's contradiction is unavailable there, and that is precisely why the proof takes S maximal: the non-maximal equality set is where factor-criticality goes to die.

**✎ Checkpoint 1.** Run necessity by hand on the worked instance's perfect matching: with S = {0,1,3}, check that each of the three odd components sends exactly one matched edge across to S — {2} sends 2–1, {4} sends 4–3, the C₅ sends 5–0 — three distinct partners in S, exactly as the pigeonhole proof demands. Then find the second C₅'s *own* equality set structure: what are the components of G − {5,7,9}, and why does the bridge edge 0–5 make 0 the vertex that saturates the far component?

### 6.4 The consolidation, and what the Atlas still owes

The matching chapter of the Atlas is now a complete story, and it deserves its map stated in one place:

| The question | The engine | The guarantee | Where |
|---|---|---|---|
| Bipartite: can all of X be matched? | Alternating paths; Hall | Exact, with a certificate (the deficient set) | Ch. 5 |
| Bipartite, cheapest assignment | Kuhn's potentials — or Lecture 4's SSP | Exact, with a certificate (potentials, no negative residual cycle) | L4 |
| General: a maximum matching | Blossoms: contract odd alternating cycles, lift back | Exact, polynomial (Edmonds 1965) | L6.1–6.2 |
| General: a perfect matching? | Tutte's condition | Min–max: a failing S is a checkable certificate; a passing one builds the matching | L6.3 |

And the chapter's own map — the three worlds this book set out to separate — closes with its full cast:

| World | The question | This chapter's specimens |
|---|---|---|
| Easy (P) | Exact, certified, polynomial | Matroid greedy (Kruskal exact), SSP with potentials, blossoms, the 2^k search tree |
| Hard (NP-complete) | No exact polytime algorithm, unless P = NP | The spine: independent set, clique, vertex cover; 3-coloring; Hamiltonicity; set cover; the TSP |
| Surviving | Ratios and parameters, with proofs | Set cover within H_u and the ln n ceiling; the TSP within 3/2; MaxCut within 0.878; vertex cover in 2^k |

One ledger entry remains, recorded honestly. Chapter 5's appendix carries a standing backlog of three items: "Edmonds' blossom algorithm and Tutte's theorem as a full section (the general-graph matching theory); Hopcroft–Karp analysis in full; stable marriage as an application section." The first item is **paid, here, in full** — the lying search caught and repaired, Tutte's theorem proved to the last line. The other two remain open on the Atlas's books: Hopcroft–Karp runs as Chapter 5's verified lab engine (phases against the √V ceiling, an exhaustive census) but its full analysis has not been written as a lecture, and stable marriage is installed nowhere in the book. This chapter records the state of the ledger and does not edit Chapter 5's.

**What to learn.** The bipartite engine failed in general graphs for exactly one reason — odd alternating cycles break parity bookkeeping — and the repair was not to abandon the engine but to make the obstruction a first-class object and contract it. That is the deepest algorithmic move in the Atlas: when a search lies, do not trust it harder or discard it; find what it cannot say, name it, and build the saying into the machine. Tutte's theorem is the same lesson at the level of structure: the obstruction to a perfect matching is not a mystery but a set S with too many odd components, a certificate a skeptic can check with a pencil — the min–max pattern's final form in this book. And the consolidation table is the chapter's thesis in one glance: *the same combinatorial objects — paths, matchings, covers — live in all three worlds at once; the world is decided by the question you ask, and every border crossing has a proof at the gate.*

---

## The Trick Bag (reference card)

| Pattern | Plain language | Where you met it |
|---------|---------------|------------------|
| **P25 Reduction / encoding** | Translate one problem into another's language; the translation carries the answer — and, run backwards, it carries hardness: one fast algorithm would solve everything downstream | L1 (the entire spine, every joint proved), L4 (assignment → min-cost flow), L2 (the ceiling's reduction-built hardness) |
| **P18 Algorithmic proof** | The proof is the procedure; the invariant is future-proof; termination is the theorem | L3 (Rado–Edmonds' greedy certified against the eventual optimum at every step), L4 (SSP carries its optimality certificate through every iteration), L6 (the blossom engine) |
| **P17 Duality (min–max)** | Two problems are the same number; each solution certifies the other's optimality | L1 (α + τ = n), L4 (potentials price the residual; no negative cycle = optimal), L6 (Tutte: the failing S is exactly the obstruction) |
| **P16 Alternating paths / augmentation** | Improve along a path; the residual network keeps every correction available at its honest price | L4 (backward arcs and cancellation), L6 (the engine that stalls on odd cycles — and the blossom repair) |
| **P10 Averaging / expectation** | Charge by the crowd you arrived with; the average prices the greedy | L2 (the charging argument: each element pays 1/c), L5 (the coin-flip floor at 1/2; the random hyperplane at θ/π) |
| **P9 Pigeonhole** | n+1 objects, n boxes — here mostly as parity: odd components, odd cycles, distinct partners | L5 (the odd-degree set is even; the tour splits into two matchings), L6 (Tutte's necessity: odd components eat distinct vertices of S) |
| **P4 Recurrence + induction** | Relate case k to smaller cases — on purpose, and in the exponent | L1 (the search tree T(k) ≤ 2T(k−1) + O(m)), L6 (Tutte's induction, with maximality doing the heavy lifting) |
| **Hardness is structure (lore)** | An NP-completeness proof is the theorem that two problems share the exact structure that resists speed — the reduction is the proof | L1 (the spine), L2 (the ln n ceiling), L5 (0.878's conjectured finality) |
| **The guarantee is the theorem (lore)** | When exactness dies, demand a ratio; when a ratio is achieved, ask whether the ceiling is lower — some ceilings are posted exactly | L2 (H_u achieved, ln n the barrier), L4 (certificates over asymptotics), L5 (2, 3/2, 0.878), L1 (2^k: hardness in n, tractability in k) |

**Formula box:** P and NP: certificates define NP (checking, not finding); a reduction is a polytime answer-preserving map; NP-complete = in NP + everything reduces in. The spine: 3-SAT → independent set (clause triangles, complement edges across, size m; 3m vertices) → clique (complement) → vertex cover (Gallai α + τ = n, both inequalities one line each); cite Cook–Levin, Karp's twenty-one, Stockmeyer/GJS for 3-coloring. FPT: branch on any uncovered edge uv, T(k) ≤ 2T(k−1) + O(m), tree ≤ 2^(k+1) − 1 nodes, time O(2^k·(n+m)); the census's worst tree hits 31 = 2⁵ − 1 exactly at K₆ minus an edge, τ = 4. Set cover: greedy ≤ H_d·OPT ≤ (ln u + 1)·OPT by charging (each covered element pays 1/c to its move; each optimal set's share ≤ H of its size — prune the optimum into a partition first); H₂ = 1.5, H₄ ≈ 2.0833, H₈ ≈ 2.7179, H₁₆ ≈ 3.3807, H₃₂ ≈ 4.0585, H₁₀₀ ≈ 5.1874; greedy's true worst is ln n − ln ln n + Θ(1) (Slavík); (1 − ε)·ln n is NP-hard to beat (Dinur–Steurer 2014, past Feige 1998); vertex cover's 2 is unbeatable by 2 − ε only assuming UGC (Khot–Regev). No bound in OPT alone: the ladder drives greedy to (log₂ u)+1 sets at OPT = 2. Matroids: heredity + exchange (I3); Rado–Edmonds: greedy optimal for every nonnegative weight function ⟺ exchange holds — forward by induction on greedy's prefix vs any independent k-set, backward by weights c on A, c′ on B∖A with 1 < c/c′ < |B|/|A|; Kruskal is the graphic case (forests exchange by component counting). Min-cost flow: SSP augments along a cheapest residual path (backward arcs at −w: refunds); integrality free with integer data; optimal ⟺ no negative residual cycle, certified by potentials with w(u,v) + d(u) − d(v) ≥ 0 on every residual arc; assignment = source → rows → columns → sink with unit capacities, optimum a permutation; the 2022 almost-linear frontier (Chen–Kyng–Liu–Peng–Probst Gutenberg–Sachdeva) trades SSP's transparency for asymptotics. TSP: MST ≤ OPT (delete one tour edge); double the tree, Euler, shortcut: ≤ 2·OPT (triangle inequality is the shortcut's license — without it the same steps cost 2,005 against an optimum of 8); Christofides: the odd-degree set is even (degree-sum parity), the minimum perfect matching on it costs ≤ OPT/2 (alternate the tour's O-segments into two matchings; the cheaper is under half), total 3/2 — tight as a lemma (PM = OPT/2 exactly on the five-point witness), 3/2 − ε crossed randomized in 2021 (Karlin–Klein–Oveis Gharan, ε > 10⁻³⁶). MaxCut: coin flips give 1/2; GW's hyperplane separates SDP vectors at angle θ with probability θ/π while the SDP prices the edge at sin²(θ/2) = (1 − cos θ)/2; the ratio θ/(π sin²(θ/2)) is minimized where tan(θ/2) = θ, at θ ≈ 2.3311, value 0.87857 — UGC-optimal (Khot 2002; Khot–Regev 2008). Tutte: PM ⟺ odd(G − S) ≤ |S| for every S — necessity by pigeonhole, sufficiency by maximal equality set → all components odd → all factor-critical (induction) → Hall on the auxiliary bipartite → assemble; factor-critical = delete-anyone-keeps-a-PM; blossoms: odd alternating cycles are parity switchers (two ways around, opposite parities) — contract, search, lift back.

---
## Exercises (graded: ●○○ easy · ●●○ moderate · ●●● tough)

**Easy — one idea, applied directly**

1. ●○○ **The gadget, by hand.** Build the reduction of §1.2 on the satisfiable witness (x ∨ y ∨ ¬z)(¬x ∨ y ∨ z)(x ∨ ¬y ∨ z): three triangles, one per clause, then every complementary pair joined across. (a) Verify by truth table that exactly five assignments satisfy the formula: 000, 011, 101, 110, 111. (b) Count the gadget: nine vertices and fifteen edges — where do the six non-triangle edges come from? (c) Read off the independent set the assignment 000 yields (one true literal per clause), and check directly that no two of its vertices are adjacent. (d) Run the converse on the assignment 111: pick true literals, get an independent set, and check that reading its labels back gives a consistent assignment. *Hint: P25 — the construction is the proof; every edge of the gadget is a reason.*

2. ●○○ **The paw, its complement, and Gallai.** The paw is the triangle 0-1-2 with pendant 3 at 0. (a) Compute α(G) and τ(G) by hand. (b) Draw the complement: show it is the path 1-3-2 plus an isolated vertex, and compute α(Ḡ) and τ(Ḡ). (c) Verify Gallai's identity α + τ = n in both graphs, and verify the spine's chain on this instance: G's triangle is a clique of 3, Ḡ has an independent set of 3, and Ḡ has a vertex cover of size 4 − 3 = 1. *Hint: P6 — compute in the complement; the identity is one line per direction.*

**Moderate — two ideas, or one tricky step**

3. ●●○ **The tree that hits the bound.** Run the bounded search tree of §1.4 by hand on K₆ with the edge (0,1) deleted, k = 4: branch always on the first uncovered edge in the order (0,2), (0,3), (0,4), (0,5), (1,2), …, (4,5), trying the smaller endpoint first, and stop at the first success. (a) Show τ = 4 and α = 2. (b) Show the first branch (delete 0) wanders a complete K₅ with budget 3 — fifteen nodes, every one doomed. (c) Show the second branch finds its first — and the search's only — success at its very last leaf. Total: 31 = 2^(k+1) − 1 nodes, the worst-case bound hit exactly. (d) The same search on K₆ with edge (2,3) deleted finishes in nine nodes. What does the contrast teach about worst-case bounds? *Hint: P4 + P18 — unroll the recurrence; count the nodes as the procedure experiences them.*

4. ●●○ **The ladder — no bound in OPT alone.** The census never caught greedy set cover using more than 1.5·OPT sets, but its families had at most three sets each. Consider a 16-element universe with six sets, listed in this order: S₁ = {0,…,7}, S₂ = {8,…,11}, S₃ = {12,13}, S₄ = {14}, A = {0,1,2,3,8,9,12,14}, B = {4,5,6,7,10,11,13,15}. Greedy takes the set covering the most new elements, ties to the earliest. (a) Verify A ∪ B is the whole universe — so OPT = 2 — and run greedy: it uses five sets. Compute the ratio. (b) Show each bait Sᵢ wins its stage only by tying A and B, so the earliest-first rule is doing all the work. (c) Extend the ladder: on a universe of 2^t elements, how many sets can greedy be forced to use at OPT = 2? (d) Reconcile with Chvátal's theorem — why is five sets no contradiction to greedy ≤ H_d·OPT — and state the honest moral about bounds of the form f(OPT). *Hint: P11 + P10 — the construction is the proof; price each stage with the charging argument's own logic.*

5. ●●○ **Exchange, by hand and in general.** In the graphic matroid of K₄ let A = {0–1, 1–2} (the 2-edge path) and B = {0–1, 0–2, 0–3} (the 3-edge star). (a) Check B ∖ A = {0–2, 0–3}: adding 0–2 closes the triangle 0-1-2, but 0–3 augments — the axiom survives on its smallest nontrivial case. (b) Prove the graphic matroid always satisfies exchange: if A, B are forests with |A| < |B| and *no* edge of B ∖ A augments A, derive a contradiction by counting A's connected components. (c) The census: K₄ has 38 forests among its 64 edge sets, and all 463 ordered pairs |A| < |B| admit an augmenting edge. Explain why (b) makes the census inevitable. *Hint: P8 — take the extremal failure; if nothing augments, every edge of B lives inside one of A's components, and forests cannot overfill a component.*

6. ●●○ **The non-matroid, both directions of the theorem.** The family M = {∅, {a}, {b}, {c}, {b, c}} is an independence system (hereditary — check it) but not a matroid. (a) Exhibit the exchange failure. (b) Build the weights that break greedy: a = 3, b = c = 2 (the ratio 3/2 sits strictly between 1 and |B|/|A| = 2). Run greedy: it takes a, then can add nothing — total 3 against the optimal {b, c} at 4. (c) Now weight b = c = 10, a = 0: greedy finds the optimum. Explain carefully why (c) is no alibi — quote the exact quantifier in Rado–Edmonds that (b) violates and (c) does not repair. *Hint: P18 — the algorithm is the theorem's subject; one failing input condemns it, for the theorem says "every."*

7. ●●○ **Successive shortest paths, by hand, with the certificate.** The lab's nine-arc network (Part 4 prints the arcs): demand 2 from source 0 to sink 4. (a) Find the first shortest path (cost 5) and the second (cost 6); write the final arc flows and the total cost 11. (b) The optimality certificate: with potentials d = (−6, −4, −5, −2, 0) on vertices 0 through 4, compute the reduced cost w(u, v) + d(u) − d(v) of every residual arc — forward on unsaturated arcs, backward on arcs carrying flow — and check all twelve are ≥ 0. (c) Prove the certificate works: potentials telescope around any cycle, so no residual cycle is negative; and if a cheaper flow of the same value existed, their difference would decompose into residual cycles, at least one negative — contradiction. *Hint: P16 + P17 — the residual network prices regret; the potentials are the dual solution made computable.*

**Tough — several chapter ideas combined**

8. ●●● **The 3/2 chain, tight at exactly one link.** (a) Reprove the matching lemma of §5.2: the minimum perfect matching on the MST's odd-degree set costs at most OPT/2. (b) Pinpoint the exact step where the triangle inequality enters the proof — which sentence is false without it? (c) Run the whole chain by hand on the witness instance (4,2), (5,0), (1,1), (0,5), (0,6): the MST (weight 13, edges 3–4, 0–1, 0–2, 2–3), the odd set {1, 4}, the matching cost 11 = OPT/2 exactly, the optimal tour 0-1-2-3-4-0 at 22, the Christofides walk 0, 1, 4, 3, 2, 0 shortcutting to cost 24 — ratio 24/22 ≈ 1.091. Where does the chain lose its slack on this instance, and where is it exactly tight? (d) The 2021 randomized algorithm promises 3/2 − ε in expectation. Explain why this violates nothing you proved in (a)–(c). *Hint: P9 — the odd set is even; the tour splits into two matchings; the cheaper one is under half.*

9. ●●● **Factor-criticality, and the worked instance.** (a) Prove C₅ is factor-critical and the 3-vertex path P₃ is not. (b) Prove every factor-critical graph is connected and has odd order. (c) On the worked instance of §6.3 — two 5-cycles bridged by 0–5 — verify the proof's anatomy end to end for S = {0, 1, 3}: the three odd components {2}, {4}, the second C₅; factor-criticality; the auxiliary bipartite graph and its matching 1 → {2}, 3 → {4}, 0 → C₅; the assembled perfect matching {1–2, 3–4, 0–5, 6–7, 8–9}. (d) Now the trap: {0, 1} is also an equality set, but its components are the path 2-3-4 and the C₅, and the path is not factor-critical. Locate exactly which step of the proof fails there, and explain why maximality of S is the load-bearing choice. *Hint: P9 + P4 — odd counts first; the induction's maximality contradiction second.*

10. ●●● **The search that lies, resolved.** (a) Run the naive parity search on the paw with M = {0–1}, root 2: write the labels, exhibit the tell (the matched edge inside side B), and find the real augmenting path. (b) Same on the pendant C₅ with M = {2–3, 4–0}, root 1: labels 1A, 0B, 2B, 4A, 3A — the tell is now an unmatched edge inside side A — and the real path 1-2-3-4-0-5. (c) Resolve both with Edmonds' move: contract the blossom, find the augmenting path in the contracted graph, lift it back — and say explicitly which of the two ways around each odd cycle the lift takes. (d) The naive search could, in principle, "try both parities" everywhere. Why is that not a fix — and what exactly does contraction buy over it? *Hint: P16 — the alternating structure is the engine; the odd cycle is the one place it can be repaired locally.*

11. ●●● **The 0.878, computed.** (a) Derive the separation probability: for two unit vectors at angle θ, a uniformly random hyperplane through the origin separates them with probability θ/π (great-circle lunes: the two separating lunes have total area 4θ on a sphere of area 4π). (b) Derive the SDP price: the vector program pays the edge (1 − cos θ)/2 = sin²(θ/2). (c) Minimize the ratio f(θ) = θ/(π sin²(θ/2)): show f′(θ) = 0 exactly when tan(θ/2) = θ, solve (θ ≈ 2.3311), and evaluate f there (0.87857). (d) Check the boundaries — f explodes as θ → 0 and f(π) = 1 — and explain why the guarantee is the *minimum* over θ, not the average: the worst edge in the graph is the one that prices the round. *Hint: P10 + P21 — the ratio function is an average-price argument in disguise; the calculus is routine and the lab checks it.*

12. ●●● **Direct 3-SAT → vertex cover, without the detour.** §1.2 reaches vertex cover through independent set; there is also a direct reduction. For each variable make an edge (x, ¬x); for each clause make a clique on fresh occurrence-vertices, one per literal occurrence, and join each occurrence-vertex to the variable-vertex of the *opposite* sign; set k = (number of variables) + Σ(clause size − 1). (a) Prove both directions: a satisfying assignment builds a k-cover, and a k-cover reads off a satisfying assignment (budget forces exactly one endpoint per variable edge and exactly s − 1 per clause clique). (b) Run it on the satisfiable witness: 15 vertices, k = 9 — and the machine confirms the minimum cover is exactly 9 (eighteen covers of size 9 exist, one per satisfying-choice structure). (c) Run it on the unsatisfiable witness (x ∨ y)(¬x ∨ y)(x ∨ ¬y)(¬x ∨ ¬y): 12 vertices, k = 6 — and the minimum cover is 7, so no cover of size 6 exists: unsatisfiability, certified by a cover number. *Hint: P25 — the budget k is the assignment plus one omission per clause; the clique is a choice gadget.*

**◆ Pattern-unknown — no hints; diagnosing the tool is the assignment**

13. ◆ **Count the independent sets of size m.** In the gadget of Exercise 1, count exactly the independent sets of size 3 (one per clause, as the theorem's shape demands). Your answer should end in a number and a description of the structure you counted.

14. ◆ **When the metric dies.** Six cities; the cheap edges are (0,1), (0,5), (0,3), (2,3), (3,4) at cost 1 each, (1,2) and (4,5) at cost 2, every other pair at cost 1000. Run the double-tree algorithm: MST, doubled, Euler walk, shortcut. Compare the tour's cost with the true optimum, count the triangle-inequality violations, and diagnose exactly which sentence of the factor-2 proof the instance breaks.

15. ◆ **The greedy assignment, diagnosed.** The 2×2 cost matrix [[1, 2], [2, 4]]: assign each row to a distinct column, minimizing total cost. The row-greedy (each row takes its cheapest free column) totals 5; the optimum is 4. Diagnose the failure with Lecture 3's machinery — what is the independence system, does it exchange, and which engine should have been used instead?

**◐ Explorations — no single right answer**

16. ◐ **Design the next census.** The Dirac census stopped at n = 6; at n = 7 there are 2^21 = 2,097,152 labeled graphs. Design the n = 7 run: what exactly do you count, what is the falsifier (a Dirac graph without a Hamilton cycle would refute a theorem — say precisely what the machine would have to print), how would you make Hamiltonicity testing fast enough (2^21 graphs times what per-graph test?), and what would the result add that the n = 5, 6 numbers do not? Then the deeper question: what can no census at any n ever establish about Dirac's theorem, and what, concretely, is a census *for*?

17. ◐ **The parameterized frontier.** The chapter's search tree is the first word of FPT, not the last. Investigate: how much can tuned branching rules (deciding more cleverly which vertex to branch on, or branching on whole structures at once) shrink the 2^k? What is kernelization, and why does it pair naturally with a bounded search tree — what does each do to the exponent and to the input size? Hunt the current literature for the best known FPT algorithms for vertex cover and for one problem of your choosing, and read enough of Downey–Fellows to say what W[1]-hardness is the parameterized analogue of. What would a proof of W[1]-hardness for a problem you care about change in practice?

18. ◐ **Approximation in practice.** The lab's twelve-instance family runs the 2-approximation at worst 1.5 — far inside its guarantee — while Exercise 4's ladder and ◆14's broken metric show the guarantees are honest. Investigate the gap: what do worst-case instances for TSP approximation look like, and can you design a family that pushes Christofides close to 3/2? When the optimum is computable (small instances, or problems with exact algorithms that are merely slow), measure *how often* the guarantees are nearly tight on random instances versus structured ones. Then the engineering question the chapter deliberately leaves open: given a 2-approximation that runs in milliseconds and a 3/2-approximation that runs in minutes, what does a real instance distribution do to that trade-off, and how would you decide?

---

## Answers to the Exercises

**A1.** (a) Evaluating the three clauses at all eight assignments: 000 satisfies via (¬z), (¬x), (¬y); 001 fails clause 1 (x, y, ¬z all false); 010 fails clause 3 (x, ¬y, z all false with y = 1, z = 0); 011 satisfies; 100 fails clause 2 (¬x, y, z all false); 101 satisfies; 110 satisfies; 111 satisfies — exactly **{000, 011, 101, 110, 111}**. (b) Three triangles contribute 9 edges; the complementary pairs: x occurs in clauses 1 and 3, ¬x in clause 2 — two x/¬x edges; y in clauses 1 and 2, ¬y in clause 3 — two y/¬y edges; z in clauses 2 and 3, ¬z in clause 1 — two z/¬z edges: **6 complement edges**, 15 in all, on 9 vertices. (c) Assignment 000 makes exactly one literal true per clause: ¬z in clause 1, ¬x in clause 2, ¬y in clause 3. The three chosen vertices sit in different triangles (no triangle edge between them) and no pair is complementary (three different variables) — independent ✓. (d) 111 makes several literals true per clause; pick (x from clause 1, y from clause 2, z from clause 3): pairwise non-adjacent for the same reasons; reading the labels gives x = y = z = true — consistent, and it satisfies. The two directions of the proof of §1.2, run on one body each. ∎ (The machine census: 5 satisfying assignments, every one yielding independent sets; Exercise ◆13 counts them all.)

**A2.** (a) The paw's edges: 0–1, 1–2, 0–2, 0–3. Independent sets: {1, 3} and {2, 3} (1 and 3 share no edge; 2 and 3 share none; vertex 0 is adjacent to everyone) — α(G) = 2. Vertex covers: {0, 1} covers all four edges (0–1 ✓, 0–2 via 0, 1–2 via 1, 0–3 via 0); no single vertex does (0 misses 1–2; 1 misses 0–2 and 0–3; 2 misses 0–1 and 0–3; 3 misses three) — τ(G) = 2. Gallai: 2 + 2 = 4 ✓. (b) The complement's edges are exactly the non-edges of the paw: 1–3 and 2–3 — the path 1-3-2, with 0 isolated. α(Ḡ) = 3 ({0, 1, 2}: no complement edge among them — they are G's triangle) = ω(G) ✓. τ(Ḡ) = 1 (vertex 3 covers both complement edges) = n − α(Ḡ) ✓, Gallai again. (c) The chain: clique {0,1,2} in G ⟺ independent set {0,1,2} in Ḡ ⟺ vertex cover {3} in Ḡ of size 4 − 3 = 1 ✓ — three problems, one number, on four vertices. ∎ (machine-checked)

**A3.** (a) In K₆ − (0,1) the only non-edge is 0–1, so {0,1} is the largest independent set: α = 2, and Gallai gives τ = 6 − 2 = 4. (b) The first uncovered edge at the root is (0,2); the u-branch deletes 0, leaving the complete K₅ on {1,…,5} with budget 3. Since τ(K₅) = 4, no set of ≤ 3 vertices covers it: every node with budget ≥ 1 still sees an uncovered edge, so the subtree branches to the full depth-3 binary tree — 1 + 2 + 4 + 8 = 15 nodes, every leaf a failure, the success structurally impossible. (c) The v-branch deletes 2, leaving {0,1,3,4,5} minus 0–1 with budget 3 (τ = 3, so success is possible but only at depth 3). Inside: the first edge (0,3) — the u-side deletes 0 (a complete K₄, budget 2 < τ(K₄) = 3: 7 doomed nodes), the v-side deletes 3; then (0,4): u deletes 0 (K₃, budget 1 < τ(K₃) = 2: 3 doomed), v deletes 4; then (0,5): u deletes 0 (the edge 1–5 remains, budget 0: fails), v deletes 5 — no edges remain: **success, the cover {2, 3, 4, 5}**, the subtree's very last leaf. The subtree cost 15 nodes; with the root and the doomed 15: **31 = 2⁵ − 1 = 2^(k+1) − 1 exactly** — the bound attained because every wrong turn is walkable to its grave before the right one appears. (d) On K₆ − (2,3) the first branch's deletions happen to leave covers early: the search succeeds at its fourth leaf (cover {0,1,4,5}), nine nodes total. The lesson: the bound 2^(k+1) − 1 counts the *unlucky* tree — no early success anywhere below the last leaf — and the short-circuit makes typical trees far smaller; tightness is the statement that the unlucky tree exists. ∎ (machine-verified, both instances and the full census: max 31 across all 33,866 graphs)

**A4.** (a) A ∪ B = {0,…,15} ✓; no single set is the universe, so OPT = 2. Greedy, ties to earliest: stage 1: S₁, A, B each cover 8 → **S₁**. Stage 2 (remaining 8–15): S₂ covers 4, A covers 4 ({8,9,12,14}), B covers 4 ({10,11,13,15}) → **S₂**. Stage 3 (remaining 12–15): S₃ covers 2, A 2, B 2 → **S₃**. Stage 4 (remaining 14, 15): S₄ covers 1, A 1 ({14}), B 1 ({15}) → **S₄**. Stage 5: {15} — only B covers it → **B**. Five sets: ratio **2.5**. (b) Every stage is a three-way (or two-way) tie that the earliest-first rule resolves toward the bait — the baits never win by covering more, only by being listed first. (c) Double the universe: baits of sizes 16, 8, 4, 2, 1 on 32 elements with the same tie bookkeeping drive greedy to **six** sets (the lab runs it); in general u = 2^t elements give t baits plus one finishing set: t + 1, ratio (t + 1)/2 — unbounded at OPT = 2. (d) Chvátal: the largest set has size 8, and H₈ · 2 ≈ 2.7179 × 2 = 5.4357 ≥ 5 ✓ — no contradiction, because the harmonic bound is priced in the *set sizes*, not in OPT. The moral: no bound of the form f(OPT) exists for greedy; its true worst-case shape is Slavík's ln u − ln ln u + Θ(1), and the census's 1.5 was the ceiling of the *small* world only — three-set families on tiny universes. The ladder is that theorem in miniature. ∎ (machine-verified at u = 16 and u = 32)

**A5.** (a) A = {0–1, 1–2}: the independent 2-edge path. B = {0–1, 0–2, 0–3}: the star at 0, three independent edges. B ∖ A = {0–2, 0–3}: 0–2 joins 0 and 2, which A already connects (0–1–2) — adding it closes the triangle ✗; 0–3 reaches vertex 3, which A does not touch — A ∪ {0–3} is the 3-edge tree ✓. Exchange survives, and the star's *second* option is what saves it. (b) Suppose A, B forests, |A| < |B|, and no e ∈ B ∖ A augments A. Adding e to A closes a cycle exactly when e's endpoints lie in one connected component of (V, A) — so *every* edge of B (including B ∩ A, trivially) has both endpoints within a single A-component. B restricted to each A-component C is then a forest on C's vertex set: at most |V(C)| − 1 edges. Summing over components: |B| ≤ Σ(|V(C)| − 1) = n − c(A) = |A| (the forest identity, |A| = n − components) — contradicting |A| < |B|. So some edge augments. ∎ (c) The census was a formality: (b) proves the axiom for *every* pair; the machine's 463-for-463 is the theorem counted on one body. ∎

**A6.** (a) Hereditary: every subset of a member is a member ✓ (∅; singletons; {b, c}'s subsets are singletons and ∅). Exchange: A = {a}, B = {b, c}: |A| < |B|, but A ∪ {b} = {a, b} ∉ M and A ∪ {c} = {a, c} ∉ M — no augmenting element. (b) Weights a = 3, b = c = 2, greedy descending: take a (3, independent); b fails ({a, b} ∉ M); c fails; done — greedy's total 3. Optimal: {b, c}, total 4. Greedy loses, and the weight ratio 3/2 is exactly the construction's demand: strictly between 1 and |B|/|A| = 2, so greedy prefers the doomed singleton while the optimum hides in the pair. (c) Weights b = c = 10, a = 0: greedy takes b, then c ({b, c} ✓), then fails on a: total 20 — optimal. No alibi: Rado–Edmonds says greedy is optimal **for every nonnegative weight function if and only if exchange holds**; the "only if" direction needs just one failing weight function, (b) supplies it, and the system stands condemned — that (c) succeeds only shows greedy is *sometimes* lucky, which no one disputed. ∎

**A7.** (a) Iteration 1: the cheapest 0→4 path is 0→1→4 at cost 1 + 4 = 5; push 1 (arc 0→1 saturates). Iteration 2: in the residual network the cheapest path is 0→2 (the cost-1 parallel) → 2→3 (the cost-3 parallel) → 3→4 at cost 1 + 3 + 2 = 6; push 1. Final flows [1, 1, 0, 0, 1, 0, 1, 0, 1], total cost 1 + 4 + 2 + 3 + 1 = **11**. (b) Residual arcs and reduced costs w + d(u) − d(v) with d = (−6, −4, −5, −2, 0): forward unsaturated — 1→4: 4 − 4 − 0 = 0; 0→2 (cost 3): 3 − 6 + 5 = 2; 2→3 (cost 9): 9 − 5 + 2 = 6; 1→4 (cost 8): 8 − 4 = 4; 2→3 (cost 3): 3 − 5 + 2 = 0; 3→0: 4 − 2 + 6 = 8; 0→2 (cost 1): 1 − 6 + 5 = 0; backward on flow-carrying arcs — 1→0: −1 − 4 + 6 = 1; 4→1: −4 + 0 + 4 = 0; 4→3: −2 + 0 + 2 = 0; 3→2: −3 − 2 + 5 = 0; 2→0: −1 − 5 + 6 = 0. **Twelve arcs, all ≥ 0** ✓ — and note the used arcs (0→1's refund, the cost-4, cost-3, cost-1 arcs) all sit at reduced cost 0: a *tight* optimum, exactly as complementary slackness wants. (c) Around any closed walk the d-terms cancel (each +d(v) meets a −d(v)), so a residual cycle's reduced-cost sum equals its true cost; all reduced costs ≥ 0 makes every residual cycle nonnegative. And if some flow f′ of value 2 cost less than 11, the difference f′ − f would be a circulation in the residual network of negative total cost; a circulation decomposes into cycles (walk it off its cycles), each residual, and at least one must carry negative cost — contradiction. No cheaper flow exists: the certificate closes. ∎ (all twelve values machine-checked)

**A8.** (a) As in §5.2: read the tour's visits to the odd set O = {o₁, …, o_{2k}} cyclically; the odd-numbered tour segments pair the O-vertices one way, the even ones the other way; each pairing is a perfect matching on O; the two matchings' costs sum to at most the tour's; the cheaper is ≤ OPT/2; the minimum matching M costs no more. (b) The metric enters at "each matching's cost is at most the cost of its own segments": the matching edge oᵢoⱼ is priced by the *sum of the tour edges along the segment* — precisely the triangle inequality. Without it a segment can cost 10 while its shortcut costs 1000 (that is ◆14, at scale). (c) The chain on the witness: distances (Manhattan): d(0,1) = 3, d(0,2) = 4, d(0,3) = 7, d(0,4) = 8, d(1,2) = 5, d(2,3) = 5, d(3,4) = 1, d(2,4) = 6, d(1,3) = 10, d(1,4) = 11. MST: 3–4 (1), 0–1 (3), 0–2 (4), 2–3 (5) — weight 13 ✓; degrees (2, 1, 2, 2, 1): odd set {1, 4} ✓; its matching costs d(1,4) = 11 = OPT/2 with OPT = 22 — the lemma's tight case (both tour segments between 1 and 4 cost 11, so *both* alternating matchings tie at exactly half). The optimal tour 0-1-2-3-4-0 costs 3 + 5 + 5 + 1 + 8 = 22 ✓ (the lab's exhaustive check confirms 22 is the minimum). Christofides: T ∪ {1–4} has all degrees even; the Euler walk 0, 1, 4, 3, 2, 0 shortcuts to the tour 0-1-4-3-2-0 costing 3 + 11 + 1 + 5 + 4 = 24, ratio 24/22 ≈ **1.091**. The chain is exactly tight at the *matching* link (11 = OPT/2) and slack at the tree link (w(T) = 13 < 22 = OPT): the final guarantee 3/2 · 22 = 33 sits far above the actual 24 because both links are never simultaneously tight. (d) KKOG violates nothing: the lemma bounds a particular ingredient (the minimum matching on the odd set) of a particular algorithm; a *different, randomized* algorithm can choose its matching from a cleverer distribution and win in expectation without the minimum matching ever costing less than OPT/2. Tight lemmas constrain algorithms that must use them; they do not fence the whole landscape. ∎ (all arithmetic machine-checked)

**A9.** (a) C₅: delete any vertex; the remainder is a path on 4 vertices (the cycle opens), which has the perfect matching of its two edges — the same for all five deletions by symmetry ✓ (machine-verified). P₃ (2-3-4 say): delete the center 3 — two isolated vertices, no perfect matching ✗. (b) Odd order: G − v has a perfect matching for any v, so |V| − 1 is even, so |V| is odd. Connected: if G fell into parts A ⊎ B, pick v ∈ A; then B survives intact in G − v, so |B| must be even (else G − v has no perfect matching); swapping roles, |A| is even too — making |V| even, contradicting odd order. So one part only. ∎ (c) G − {0,1,3}: vertex 2 loses neighbors 1 and 3 — isolated ✓ odd; vertex 4 loses 3 and 0 — isolated ✓ odd; the second cycle 5-6-7-8-9-5 survives whole — odd ✓; three odd components = |S| ✓. Factor-criticality: the singletons trivially; C₅ by (a) ✓. The auxiliary bipartite graph: 0–{4} (edge 0–4), 0–C₅ (edge 0–5), 1–{2} (edge 1–2), 3–{2} (edge 3–2), 3–{4} (edge 3–4); the matching 1 → {2}, 3 → {4}, 0 → C₅ saturates S ✓. Assembly: pick 1–2, 3–4, 0–5; delete 2, 4, 5; the C₅ minus 5 is the path 6-7-8-9 with matching {6–7, 8–9}; the union {1–2, 3–4, 0–5, 6–7, 8–9} is a perfect matching — the proof *builds* it. (d) At S = {0, 1}: components are the path 2-3-4 and the C₅, both odd: an equality set, but not maximal. Move 3 fails exactly here: for the component P₃ and its center x = 3, the subgraph P₃ − 3 = two isolated vertices has no perfect matching, and the maximality contradiction that Move 3 needs — a larger equality set W = S ∪ T ∪ {x} — is unavailable because {0,1} was never maximal in the first place. Maximality is what guarantees every component *must* be factor-critical; without it the proof's induction has nothing to grab. ∎

**A10.** (a) Paw, M = {0–1}, root 2: 2 → A; unmatched edges 2–1, 2–0 → 1, 0 → B; 0's matched partner is 1 — already B: the matched edge 0–1 lies inside side B, the B→A step cannot fire, A = {2} is final, and no unmatched edge from 2 reaches an exposed vertex: the search reports stuck. The lie: 2-1-0-3 (unmatched, matched, unmatched) ends at exposed 3. (b) Pendant C₅, M = {2–3, 4–0}, root 1: 1 → A; 0, 2 → B; 4 → A (0's partner), 3 → A (2's partner); the unmatched edge 3–4 now lies inside A — second tell — and 5 hangs off 0 ∈ B, out of the A-side's reach: stuck again, and again falsely: 1-2-3-4-0-5 alternates to the exposed 5. (c) Paw: the blossom is the odd cycle 2-0-1 (unmatched 2–0, matched 0–1, unmatched 1–2, based at the root 2). Contract to a pseudovertex: its one outside edge is 0–3, unmatched, to the exposed 3 — an augmenting path immediately. Lift: the path leaves the blossom from vertex 0 along the unmatched edge 0–3, so inside the blossom we must walk from the base 2 to 0 along the even-length alternating arc ending in a matched edge — namely 2-1-0 (unmatched 2–1, then matched 1–0) — and splice to obtain 2-1-0-3. The parity-switching lemma guarantees that exactly one of the two arcs around the triangle has even length and ends with a matched edge at 0, and 2-1-0 is that arc. C₅: the blossom is 1-2-3-4-0 (three unmatched, two matched edges, based at 1). Contract; the pseudovertex's outside edge 0–5 reaches exposed 5; lift by leaving from 0 and walking the even-length alternating arc 1-2-3-4-0 (unmatched, matched, unmatched, matched) from the base 1 to 0, giving 1-2-3-4-0-5. (d) "Trying both parities everywhere" is exponential: parity assignments interact across the whole graph, and only those consistent with *some* augmenting path matter. Contraction buys exactly the needed ambiguity at exactly the places it arises — each blossom resolved by one contraction, one local parity switch — keeping the search polynomial while restoring completeness. The genius is not exploring both worlds; it is proving the two worlds say the same thing. ∎ (all four lying states and both lifts machine-verified)

**A11.** (a) The separating region: sign⟨w, u⟩ ≠ sign⟨w, v⟩ changes only across the great circles w ⊥ u and w ⊥ v, which cut the unit sphere into four lunes; the two separating lunes (dihedral angle θ between the circles' planes) have combined area 2 · 2θ = 4θ on the sphere of area 4π: probability θ/π. (b) The vector program's per-edge term: (1 − ⟨u, v⟩)/2; with ⟨u, v⟩ = cos θ that is (1 − cos θ)/2 = sin²(θ/2). (c) For f(θ) = θ/(π sin²(θ/2)), the quotient rule gives f′(θ) = (sin²(θ/2) − θ sin(θ/2)cos(θ/2))/(π sin⁴(θ/2)). For θ ∈ (0, π), sin(θ/2) > 0 and cos(θ/2) > 0, so dividing the numerator by sin(θ/2)cos(θ/2) shows f′(θ) = 0 if and only if tan(θ/2) = θ. The unique solution in (0, π) is **θ ≈ 2.3311** (tan(1.16555) ≈ 2.3311 ✓), and f(2.3311) = 0.74201/0.84457 ≈ **0.87857** — the constant, computed not looked up. (d) As θ → 0: f ~ θ/(πθ²/4) = 4/(πθ) → ∞ (nearly parallel vectors: the SDP pays almost nothing, the hyperplane separates almost never); at θ = π: f = π/(π·1) = 1 (antipodal vectors: separation certain). So the minimum is interior — and it is the *minimum* that matters because the rounding analysis pays every edge its own ratio θ_e/π against its own SDP price sin²(θ_e/2): E[cut] ≥ (min_e f(θ_e)) · SDP ≥ 0.87857 · OPT. The worst edge sets the exchange rate. ∎ (the calculus machine-checked: argmin 2.3311, value 0.87857)

**A12.** (a) *Assignment → cover.* Given a satisfying assignment, cover each variable edge at the *false* literal's vertex (one per variable: #vars picks). In each clause pick a true literal's occurrence-vertex and cover all other occurrence-vertices of that clause (s − 1 picks for a clause of size s). Check the uncovered occurrence-vertex: its external edge runs to the *opposite-sign* variable vertex, which is the false side — already covered ✓; its clique edges are covered by its siblings ✓. Total: #vars + Σ(s − 1) = k ✓. *Cover → assignment.* A k-cover exists: the variable edges need ≥ one endpoint each (≥ #vars vertex-picks), each clause clique K_s needs ≥ s − 1 (≥ Σ(s−1)); the total budget is exactly k, so equality holds everywhere: exactly one endpoint per variable edge, exactly s − 1 per clique, so each clause has exactly one uncovered occurrence-vertex o*, and its external edge (to the opposite-sign variable vertex) forces that vertex into the cover. The same-sign variable vertex is therefore *out* (one per edge). Read the assignment: the literal carried by o* is true. Consistency: if clause i demands x true and clause j demands x false, then clause i's o* forces ¬x into the cover and clause j's forces x in — both endpoints of one variable edge, impossible at equality. Every clause has a true literal: the formula is satisfied. ∎ (b) The satisfiable witness: 3 variables, three 3-clauses: k = 3 + 6 = 9; 15 vertices (6 variable + 9 occurrence); the machine confirms min vertex cover = 9 exactly — and finds eighteen 9-covers, one per way the clauses' true literals can be chosen consistently. (c) The unsatisfiable witness: 2 variables, four 2-clauses: k = 2 + 4 = 6; 12 vertices (4 + 8); the machine: min cover = 7 > 6 — no cover of size k exists, so the formula is unsatisfiable, certified by a number the skeptic can verify with a pencil and 2¹² masks. ∎

**A13.** Twelve. Structure: an independent set of size 3 takes exactly one vertex per triangle (within a triangle everything is adjacent), and the three chosen literals must contain no complementary pair — same variable twice with the same sign is allowed (no edge joins them), opposite signs never. Count: 27 one-per-clause triples total; subtract the ones containing a complementary pair — (x from clause 1, ¬x from clause 2): 3; (x from clause 3, ¬x from clause 2): 3; (y from clause 1, ¬y from clause 3): 3; (y from clause 2, ¬y from clause 3): 3; (¬z from clause 1, z from clause 2): 3; (¬z from clause 1, z from clause 3): 3 — that sum 18 double-counts exactly three triples violating two pairs at once ((x, ¬x, x), (y, y, ¬y), (¬z, z, z)): 27 − (18 − 3) = **12**. The list: (x,y,x) (x,y,z) (x,z,x) (x,z,¬y) (x,z,z) (y,¬x,z) (y,y,x) (y,y,z) (y,z,x) (y,z,z) (¬z,¬x,¬y) (¬z,y,x). Note (y,¬x,z) is the triple the assignment 011 reads; (¬z,¬x,¬y) is 000's; the others mix partial assignments — an independent set need not settle every variable. ∎ (machine-enumerated, exactly these twelve)

**A14.** The MST is the five cheap edges (0,1), (0,3), (0,5), (2,3), (3,4) — weight 5. Doubled and walked: 0, 1, 0, 3, 2, 3, 4, 3, 0, 5, 0 — an Euler circuit of the ten traversals. Shortcutting first visits: 0-1-3-2-4-5-0. Its cost: d(0,1) = 1, then d(1,3) = 1000, d(3,2) = 1, d(2,4) = 1000, d(4,5) = 2, d(5,0) = 1: total **2005**. The optimum: 0-1-2-3-4-5-0 = 1 + 2 + 1 + 1 + 2 + 1 = **8**. Ratio 2005/8 ≈ **250.6** — the "2-approximation" off by two and a half orders of magnitude. Triangle violations: 20 ordered triples (a, b, c) with d(a,c) > d(a,b) + d(b,c) — e.g., d(1,3) = 1000 > d(1,2) + d(2,3) = 3. The broken sentence is the shortcut step: "the triangle inequality makes each shortcut no dearer than the segment it replaces" — with shortcuts priced at 1000, the walk's cost explodes at exactly the two places the proof stopped guarding. Note what *survives*: MST ≤ OPT (5 ≤ 8) needs only nonnegative costs — the doubling argument's collapse is entirely the shortcut's. ∎ (machine-verified: walk, tour, optimum, violation count)

**A15.** Greedy: row 0 takes column 0 (cost 1); row 1 takes the cheapest free column, column 1 (cost 4): total 5. The optimum: row 0 → column 1 (2), row 1 → column 0 (2): total 4. Diagnosis: the legal partial assignments — cell sets with no two in one row or column — form an independence system (hereditary ✓). Exchange fails: A = {(0,0)}, B = {(0,1), (1,0)} — |A| < |B|, but A ∪ {(0,1)} repeats row 0 and A ∪ {(1,0)} repeats column 0: neither augments. By Rado–Edmonds' contrapositive, some weight function breaks greedy, and this matrix is one: greedy's per-row myopia is *the* greedy on a non-matroid. The correct engines: the problem is weighted bipartite matching — the intersection of the two partition matroids "at most one cell per row" and "at most one per column" — polynomial by Edmonds' intersection theorem, solved exactly by Lecture 4's successive shortest paths (the flow model of §4.3 finds 4) or Kuhn's potentials. The failure is not the greedy idea but the greedy *contract*: on a matroid it comes with a proof, and this system never signed. ∎ (greedy 5, optimum 4, and the exchange failure machine-verified)

---
## Computational Lab (verified)

Every recorded output below was produced by the chapter's verification runs — a TypeScript port whose logic the Python mirrors exactly; the seeded parts use the Lehmer linear congruential generator x ← 48271·x mod (2³¹ − 1), implemented identically in both languages, so every printed number is exactly reproducible. Two tie-breaking conventions run through everything: adjacencies and candidate vertices are scanned in ascending order, and greedy set cover breaks ties toward the earliest set in the family's printed order — the lab says so wherever it matters.

### Part 1 — The spine on real bodies: two gadgets, Gallai, Dirac, and the search tree

```python
from itertools import combinations

def comp(l):                          # literal negation
    return l[1:] if l[0] == '~' else '~' + l

def gadget(clauses):                  # clause cliques + complement pairs across
    vs = [(l, c) for c, cl in enumerate(clauses) for l in cl]
    E = []
    for i in range(len(vs)):
        for j in range(i + 1, len(vs)):
            if vs[i][1] == vs[j][1] or comp(vs[i][0]) == vs[j][0]:
                E.append((i, j))
    return len(vs), E

def sat_assigns(clauses, variables):
    out = []; m = len(variables)
    for bits in range(2 ** m):
        v = {variables[k]: (bits >> (m - 1 - k)) & 1 == 1 for k in range(m)}
        for x in variables: v[comp(x)] = not v[x]
        if all(any(v[l] for l in cl) for cl in clauses):
            out.append(''.join(str((bits >> (m - 1 - k)) & 1) for k in range(m)))
    return out

def indep(n, E, k):
    if k <= 0 or n < k: return [()] if k == 0 else []
    adj = [[False] * n for _ in range(n)]
    for i, j in E: adj[i][j] = adj[j][i] = True
    return [c for c in combinations(range(n), k)
            if all(not adj[a][b] for a, b in combinations(c, 2))]

sat_cl = [['x', 'y', '~z'], ['~x', 'y', 'z'], ['x', '~y', 'z']]
uns_cl = [['x', 'y'], ['~x', 'y'], ['x', '~y'], ['~x', '~y']]
n1, E1 = gadget(sat_cl); n2, E2 = gadget(uns_cl)
print(sat_assigns(sat_cl, 'xyz'), len(E1), len(indep(n1, E1, 3)))
print(sat_assigns(uns_cl, 'xy'), len(E2), len(indep(n2, E2, 4)))

def nbrs_of(n, pairs, mask):
    nb = [set() for _ in range(n)]
    for i, (a, b) in enumerate(pairs):
        if mask >> i & 1: nb[a].add(b); nb[b].add(a)
    return nb

def alpha(nb):                        # largest independent set, sizes descending
    n = len(nb)
    for k in range(n, -1, -1):
        for s in combinations(range(n), k):
            if all(b not in nb[a] for a, b in combinations(s, 2)):
                return k
    return 0

def tau(nb):                           # smallest vertex cover, sizes ascending
    n = len(nb)
    for k in range(n + 1):
        for s in combinations(range(n), k):
            if all(a in s or b in s for a in range(n) for b in nb[a]):
                return k
    return n

viol = total = 0
for n in range(2, 7):
    pairs = list(combinations(range(n), 2))
    for mask in range(2 ** len(pairs)):
        nb = nbrs_of(n, pairs, mask)
        total += 1
        if alpha(nb) + tau(nb) != n: viol += 1
print(total, viol)                    # Gallai's identity, all labeled graphs

def hamiltonian(nb):
    n = len(nb)
    if n < 3: return False
    full = (1 << n) - 1
    ends = [set() for _ in range(1 << n)]
    ends[1] = {0}                      # DP over paths starting at vertex 0
    for mask in range(1, 1 << n):
        for v in ends[mask]:
            for w in nb[v]:
                if not mask >> w & 1: ends[mask | 1 << w].add(w)
    return any(0 in nb[v] for v in ends[full])

for n in (5, 6):
    pairs = list(combinations(range(n), 2))
    counts = [0, 0, 0, 0]             # !Dirac!Ham, !DiracHam, Dirac!Ham, DiracHam
    for mask in range(2 ** len(pairs)):
        nb = nbrs_of(n, pairs, mask)
        d = min(len(nb[v]) for v in range(n)) >= n / 2
        counts[2 * d + hamiltonian(nb)] += 1
    print(n, counts)

def fpt(nb, k):                       # first uncovered edge (lex order), u then v
    nodes = [0]; n = len(nb)
    def dfs(del_, k):
        nodes[0] += 1
        for a in range(n):
            if a in del_: continue
            for b in sorted(nb[a]):
                if b > a and b not in del_:
                    if k <= 0: return None      # budget gone, edge remains
                    r = dfs(del_ | {a}, k - 1)  # try u, short-circuit on success
                    return r if r is not None else dfs(del_ | {b}, k - 1)
        return del_                             # no uncovered edge: success
    return dfs(frozenset(), k), nodes[0]

worst, att, bad = 0, [], 0
for n in range(2, 7):
    pairs = list(combinations(range(n), 2))
    for mask in range(2 ** len(pairs)):
        nb = nbrs_of(n, pairs, mask)
        cover, nodes = fpt(nb, tau(nb))
        ok = cover is not None and len(cover) == tau(nb) and \
             all(a in cover or b in cover for a in range(n) for b in nb[a])
        if not ok: bad += 1
        if nodes > worst: worst, att = nodes, [(n, mask)]
        elif nodes == worst: att.append((n, mask))
print(worst, len(att), bad)

pairs6 = list(combinations(range(6), 2))
def k6minus(a, b):
    mask = (1 << 15) - 1 & ~(1 << pairs6.index((a, b)))
    return nbrs_of(6, pairs6, mask)
for a, b in [(0, 1), (2, 3)]:
    nb = k6minus(a, b)
    print(tau(nb), fpt(nb, tau(nb)))

def direct_vc(variables, clauses):    # Exercise 12's reduction, run on its bodies
    idx = {}
    for i, l in enumerate(variables):
        idx[l], idx[comp(l)] = 2 * i, 2 * i + 1
    occ = [(l, c) for c, cl in enumerate(clauses) for l in cl]
    def oid(j): return 2 * len(variables) + j
    E = {(idx[variables[i]], idx[comp(variables[i])]) for i in range(len(variables))}
    for c in range(len(clauses)):
        for a, b in combinations([oid(j) for j, o in enumerate(occ) if o[1] == c], 2):
            E.add((a, b))
    for j, o in enumerate(occ): E.add((oid(j), idx[comp(o[0])]))
    k = len(variables) + sum(len(cl) - 1 for cl in clauses)
    covers = [s for size in range(len(E) + 1) for s in combinations(range(2 * len(variables) + len(occ)), size)
              if all(a in s or b in s for a, b in E)]
    return (2 * len(variables) + len(occ), len(E), k,
            min(map(len, covers)), sum(1 for s in covers if len(s) == k))
print(direct_vc('xyz', sat_cl))
print(direct_vc('xy', uns_cl))
```

**Verified output.** The satisfiable witness prints `['000', '011', '101', '110', '111'] 15 12` — five satisfying assignments, a fifteen-edge gadget on nine vertices, and exactly **12 independent sets of size 3** (the list is A13's). The unsatisfiable witness prints `[] 12 0`: **zero** satisfying assignments and **zero** independent sets of size 4 — the equivalence holding through both clean zeros. Gallai prints `33866 0`: every labeled graph on 2 to 6 vertices satisfies α + τ = n. Dirac prints `5 [806, 192, 0, 26]` and `6 [22690, 8220, 0, 1858]`: at n = 5, **26** Dirac graphs all Hamiltonian, 192 non-Dirac Hamiltonian, 806 non-Dirac not; at n = 6, **1,858** Dirac all Hamiltonian (zero exceptions), 8,220 and 22,690 on the far side — the wilderness below the Dirac line is almost the whole space. The search-tree census prints `31 5 0`: every one of the 33,866 graphs returns a valid cover of optimal size, and the worst tree is **31 = 2⁵ − 1 nodes, attained by exactly five graphs** — precisely K₆ with the missing edge incident to vertex 0, under the lab's lexicographic pair order. The two K₆ prints: `4 (frozenset({2, 3, 4, 5}), 31)` — K₆ − (0,1): τ = 4, the full unlucky tree — and `4 (frozenset({0, 1, 4, 5}), 9)` — K₆ − (2,3): τ = 4, success at the fourth leaf in **nine** nodes, cover {0, 1, 4, 5}: the bound counts the unlucky tree, and typical trees are far smaller. The direct construction prints `(15, 21, 9, 9, 18)` on the satisfiable witness — 15 vertices, 21 edges, k = 9, minimum cover exactly 9, **eighteen** covers of size 9 — and `(12, 14, 6, 7, 0)` on the unsatisfiable one: k = 6, minimum cover **7**, no cover of size 6 anywhere: unsatisfiability certified by a cover number.

### Part 2 — Greedy set cover against the optimum: the census, the ladder, the seeded family

```python
from itertools import combinations

def greedy_cover(u, fam):             # ties -> earliest set in printed order
    if u <= 0: return 0
    covered = [False] * u; ncov = picks = 0
    while ncov < u:
        best, bg = -1, 0
        for i, s in enumerate(fam):
            g = sum(1 for e in s if 0 <= e < u and not covered[e])
            if g > bg: bg, best = g, i
        if best < 0: break
        picks += 1
        for e in fam[best]:
            if 0 <= e < u and not covered[e]: covered[e] = True; ncov += 1
    return picks

def opt_cover(u, fam):
    if u <= 0: return 0
    full = set(range(u))
    for size in range(1, len(fam) + 1):
        for comb in combinations(fam, size):
            if set().union(*comb) == full: return size
    return len(fam)

def census(u):                        # families of <= 3 distinct nonempty sets,
    subs = [frozenset(e for e in range(u) if mask >> e & 1)  # ascending bitmask order
            for mask in range(1, 2 ** u)]
    full = set(range(u)); fams = []
    for i in range(len(subs)):
        if subs[i] == full: fams.append([subs[i]])
        for j in range(i + 1, len(subs)):
            if subs[i] | subs[j] == full: fams.append([subs[i], subs[j]])
            for k in range(j + 1, len(subs)):
                if subs[i] | subs[j] | subs[k] == full:
                    fams.append([subs[i], subs[j], subs[k]])
    return fams

counts, viol, maxr, opt2, opt2max, wit = [], 0, 0, 0, 0, None
for u in range(1, 6):
    fams = census(u)
    H = sum(1 / (e + 1) for e in range(u))
    counts.append(len(fams))
    for fam in fams:
        gr, op = greedy_cover(u, fam), opt_cover(u, fam)
        viol += gr > H * op + 1e-12
        maxr = max(maxr, gr / op)
        if op == 2: opt2 += 1; opt2max = max(opt2max, gr / op)
        if wit is None and u == 4 and gr / op == 1.5: wit = fam
print(counts, sum(counts), viol, maxr, opt2, opt2max, [sorted(s) for s in wit])

print([round(sum(1 / (i + 1) for i in range(n)), 4)
       for n in (2, 4, 8, 16, 32, 100)])

def ladder(t):                        # baits halving; A = first halves; B = rest + leftover
    u = 2 ** t; fam = []; A, B = [], []
    off, sz = 0, u // 2
    for _ in range(t):
        block = list(range(off, off + sz))
        fam.append(block)
        half = (sz + 1) // 2
        A += block[:half]; B += block[half:]
        off += sz; sz //= 2
    B.append(u - 1)
    fam += [A, B]
    return fam
for t in (4, 5):
    print(greedy_cover(2 ** t, ladder(t)), opt_cover(2 ** t, ladder(t)))

def seeded(s):                        # 4 blocks + 8 extras of 3 + dr()%7 elements
    x = s
    def dr():
        nonlocal x
        x = 48271 * x % 2147483647
        return x
    fam = [list(range(4 * b, 4 * b + 4)) for b in range(4)]
    for _ in range(8):
        want = 3 + dr() % 7
        s_ = set()
        while len(s_) < want: s_.add(dr() % 16)
        fam.append(sorted(s_))
    return fam
runs = [(greedy_cover(16, seeded(s)), opt_cover(16, seeded(s))) for s in range(1, 13)]
print(runs, max(g / o for g, o in runs))
```

**Verified output.** The census prints `[1, 5, 45, 361, 2681] 3093 0 1.5 2166 1.5 [[0, 1], [0, 2], [1, 3]]`: **3,093** covering systems (1 + 5 + 45 + 361 + 2,681 by universe size), **zero** violations of greedy ≤ H_u·OPT, maximum observed ratio exactly **1.5 = H₂** — first witnessed by the family {[0,1], [0,2], [1,3]} — and among the **2,166** opt-2 systems none exceeded 1.5: the small census's ceiling, exactly as §2.3 scopes it. The harmonic run prints `[1.5, 2.0833, 2.7179, 3.3807, 4.0585, 5.1874]`. The ladder prints `5 2` at u = 16 and `6 2` at u = 32: greedy driven to **five** sets at OPT = 2, six on the doubled universe — unbounded in OPT, priced in set sizes (H₈·2 ≈ 5.44 ≥ 5), Exercise 4's construction run by the machine. The seeded family prints twelve pairs — `(4,4) (5,4) (3,3) (3,3) (3,3) (5,4) (4,4) (4,4) (5,4) (4,4) (4,4) (3,3)` — with max ratio **1.25**: three seeds (2, 6, 9) bait greedy one set past the planted 4-block optimum, and nothing in the family comes near the harmonic ceiling the census and the ladder bracket it with.

### Part 3 — Greedy exact: the graphic matroid, Kruskal's census, the non-matroid

```python
from itertools import combinations

pc = lambda m: bin(m).count('1')
pairs4 = list(combinations(range(4), 2))

def forest(mask):                     # acyclic check via union-find
    parent = list(range(4))
    def find(x):
        while parent[x] != x: parent[x] = parent[parent[x]]; x = parent[x]
        return x
    for i in range(6):
        if mask >> i & 1:
            ra, rb = find(pairs4[i][0]), find(pairs4[i][1])
            if ra == rb: return False
            parent[ra] = rb
    return True

forests = [m for m in range(64) if forest(m)]
ab = [(A, B) for A in forests for B in forests if pc(A) < pc(B)]
fails = [(A, B) for A, B in ab
         if not any(forest(A | 1 << i) for i in range(6) if B >> i & 1 and not A >> i & 1)]
print(len(forests), len(ab), len(fails))

x = 1
def dr():
    global x
    x = 48271 * x % 2147483647
    return x

def connected(nb):
    if not nb: return True
    seen = {0}; q = [0]
    while q:
        v = q.pop()
        for w in nb[v]:
            if w not in seen: seen.add(w); q.append(w)
    return len(seen) == len(nb)

def kruskal(n, pairs, present, ws):
    order = sorted((i for i in range(len(pairs)) if present >> i & 1),
                   key=lambda i: (ws[i], i))
    parent = list(range(n))
    def find(a):
        while parent[a] != a: parent[a] = parent[parent[a]]; a = parent[a]
        return a
    tot = 0
    for i in order:
        ra, rb = find(pairs[i][0]), find(pairs[i][1])
        if ra != rb: parent[ra] = rb; tot += ws[i]
    return tot

def brute_mst(n, pairs, present, ws):
    best = None
    for sub in range(2 ** len(pairs)):
        if pc(sub) != n - 1 or sub & ~present: continue
        parent = list(range(n))
        def find(a):
            while parent[a] != a: parent[a] = parent[parent[a]]; a = parent[a]
            return a
        ok, tot = True, 0
        for i in range(len(pairs)):
            if sub >> i & 1:
                ra, rb = find(pairs[i][0]), find(pairs[i][1])
                if ra == rb: ok = False; break
                parent[ra] = rb; tot += ws[i]
        if ok and (best is None or tot < best): best = tot
    return best

agree = tested = 0
for n in (3, 4, 5):
    pairs = list(combinations(range(n), 2))
    for mask in range(2 ** len(pairs)):
        nb = [set() for _ in range(n)]
        for i, (a, b) in enumerate(pairs):
            if mask >> i & 1: nb[a].add(b); nb[b].add(a)
        if not connected(nb): continue
        ws = [1 + dr() % 100 for _ in pairs]      # one stream, edges in lex order
        tested += 1
        agree += kruskal(n, pairs, mask, ws) == brute_mst(n, pairs, mask, ws)
print(tested, agree)

FAM = [frozenset(s) for s in ([], ['a'], ['b'], ['c'], ['b', 'c'])]
def greedy_max(w):                    # descending, add if independent
    tot, cur = 0, frozenset()
    for e in sorted('abc', key=lambda v: -w[v]):
        if cur | {e} in FAM: cur = cur | {e}; tot += w[e]
    return tot
w1 = {'a': 3, 'b': 2, 'c': 2}
print(greedy_max(w1),
      max(sum(w1[e] for e in s) for s in FAM),
      greedy_max({'a': 0, 'b': 10, 'c': 10}))
```

**Verified output.** K₄ prints `38 463 0`: **38 forests** among the 64 edge subsets, **463 ordered pairs** A, B with |A| < |B|, and every single pair admits an augmenting edge — the exchange axiom counted on one body, exactly as Exercise 5(c) says the census must read. Kruskal prints `770 770`: all **770 connected labeled graphs** on 3, 4, and 5 vertices (4 + 38 + 728), each with seeded weights 1–100 drawn from the single Lehmer stream in edge order — greedy's tree equals the exhaustive minimum every time; the census was a formality, and that is the point. The non-matroid prints `3 4 20`: weights a = 3, b = c = 2 send greedy to 3 against the optimum {b, c} at 4 — the failing exchange, priced — while weights (0, 10, 10) let greedy find the optimum at 20: one failing weight function condemns, as Rado–Edmonds quantifies.

### Part 4 — Successive shortest paths: the witness network, the certificate, the assignment problem

```python
from itertools import permutations

ARCS = [  # (u, v, capacity, cost) in printed order
    (0, 1, 1, 1), (1, 4, 2, 4), (0, 2, 2, 3), (2, 3, 2, 9), (3, 4, 1, 2),
    (1, 4, 2, 8), (2, 3, 2, 3), (3, 0, 2, 4), (0, 2, 2, 1)]

def ssp(arcs, demand, s, t):          # Bellman-Ford on the residual network
    if not arcs or demand <= 0: return [0] * len(arcs), 0, 0, []
    n = max(max(u, v) for u, v, _, _ in arcs) + 1
    flow = [0] * len(arcs); val = iters = 0; log = []
    while val < demand:
        iters += 1
        INF = float('inf')
        dist = [INF] * n; dist[s] = 0
        par = [None] * n
        for _ in range(n):
            for i, (u, v, cap, c) in enumerate(arcs):
                if flow[i] < cap and dist[u] + c < dist[v]:
                    dist[v] = dist[u] + c; par[v] = (i, 1)
                if flow[i] > 0 and dist[v] - c < dist[u]:
                    dist[u] = dist[v] - c; par[u] = (i, -1)  # refund arc
        if par[t] is None: break
        path, cur = [], t
        while cur != s:
            i, d = par[cur]; path.append((i, d))
            cur = arcs[i][0] if d == 1 else arcs[i][1]
        path.reverse()
        push = demand - val
        for i, d in path:
            if d == 1: push = min(push, arcs[i][2] - flow[i])
            else:      push = min(push, flow[i])   # a refund cannot exceed the arc's flow
        for i, d in path: flow[i] += d * push
        val += push
        log.append((dist[t], push, [(arcs[i][0], arcs[i][1], arcs[i][3]) for i, d in path]))
    return flow, sum(f * a[3] for f, a in zip(flow, arcs)), iters, log

flow, cost, iters, log = ssp(ARCS, 2, 0, 4)
print(iters, log)
print(flow, cost)

d = (-6, -4, -5, -2, 0)              # the optimality certificate's potentials
res = []
for i, (u, v, cap, c) in enumerate(ARCS):
    if flow[i] < cap: res.append(('fwd', i, c + d[u] - d[v]))
    if flow[i] > 0:  res.append(('bwd', i, -c + d[v] - d[u]))
print(res, all(r[2] >= 0 for r in res))

def brute_assign(c):
    n = len(c)
    if n == 0: return 0, []
    best = min((sum(c[i][p[i]] for i in range(n)), list(p))
               for p in permutations(range(n)))
    return best

def asg_model(mat):                   # source -> rows -> columns -> sink, unit caps
    n = len(mat)
    if n == 0: return 0, [], 0
    arcs = []
    for i in range(n): arcs.append((0, 1 + i, 1, 0))
    for i in range(n):
        for j in range(n): arcs.append((1 + i, n + 1 + j, 1, mat[i][j]))
    for j in range(n): arcs.append((n + 1 + j, 2 * n + 1, 1, 0))
    flow, cost, iters, _ = ssp(arcs, n, 0, 2 * n + 1)
    perm = [-1] * n
    for i in range(n):
        for j in range(n):
            if flow[n + i * n + j] > 0: perm[i] = j
    return cost, perm, iters

W4 = [[10, 11, 2, 8], [15, 12, 10, 3], [8, 19, 14, 9], [15, 12, 2, 12]]
print(brute_assign(W4), asg_model(W4))

x = 0
def dr2():
    global x
    x = 48271 * x % 2147483647
    return x
for s in range(1, 9):
    x = s
    mat = [[1 + dr2() % 50 for _ in range(4)] for _ in range(4)]
    print(asg_model(mat), brute_assign(mat))

c22 = [[1, 2], [2, 4]]                # the row-greedy of Exercise 15
used = [False, False]; tot = 0; perm = []
for i in range(2):
    b = min((j for j in range(2) if not used[j]), key=lambda j: c22[i][j])
    used[b] = True; perm.append(b); tot += c22[i][b]
print(tot, perm, brute_assign(c22))
```

**Verified output.** The witness run prints two iterations — `(5, 1, [(0, 1, 1), (1, 4, 4)])` then `(6, 1, [(0, 2, 1), (2, 3, 3), (3, 4, 2)])` — the first unit along 0→1→4 at cost 5, the second along the cost-1 and cost-3 parallel arcs at cost 6 — then flows `[1, 1, 0, 0, 1, 0, 1, 0, 1]` and total cost **11**: the expensive parallels (9 and 8) untouched, prices rising as the cheap capacity fills, exactly as §4.1 reads the market. The certificate prints **twelve** residual arcs — forward `a1:0 a2:2 a3:6 a5:4 a6:0 a7:8 a8:0`, backward `a0:1 a1:0 a4:0 a6:0 a8:0` — all reduced costs ≥ 0, every arc with flow strictly between 0 and capacity at reduced cost exactly 0, and every arc carrying flow at a nonpositive reduced cost in the forward direction — the complementary-slackness picture of §4.1, arc by arc: a tight optimum. The assignment witness prints brute force `(24, [1, 3, 0, 2])` and SSP `(24, [1, 3, 0, 2], 4)`: the same optimum, found in **four** augmentations, one per row. The seeded run prints eight pairs, SSP equal to brute force each time — optima **74, 72, 51, 33, 30, 47, 28, 50**, every one in four iterations: 8 of 8. And the 2×2 epilogue prints `5 [0, 1] (4, [1, 0])`: the row-greedy's 5 against the optimum's 4 — ◆15's diagnosis (a greedy on a non-matroid, the exchange failure A15 exhibits) on the machine's record.

### Part 5 — TSP: the tight witness, the twelve-instance family, the 0.878, the broken metric

```python
import math
from itertools import combinations, permutations

def manhattan(p, q): return abs(p[0] - q[0]) + abs(p[1] - q[1])

def table(pts):
    n = len(pts)
    return [[manhattan(pts[i], pts[j]) for j in range(n)] for i in range(n)]

def mst(n, D):                        # Kruskal; ties -> lexicographic pair
    if n <= 1: return [], 0
    order = sorted(combinations(range(n), 2), key=lambda e: (D[e[0]][e[1]], e))
    parent = list(range(n))
    def find(a):
        while parent[a] != a: parent[a] = parent[parent[a]]; a = parent[a]
        return a
    edges, w = [], 0
    for a, b in order:
        ra, rb = find(a), find(b)
        if ra != rb: parent[ra] = rb; edges.append((a, b)); w += D[a][b]
    return edges, w

def euler(n, mult):                   # greedy Hierholzer from 0, ascending neighbor
    if n == 0: return []
    stack, walk = [0], []
    while stack:
        v = stack[-1]
        for w in range(n):
            if mult[v][w]:
                mult[v][w] -= 1; mult[w][v] -= 1; stack.append(w); break
        else: walk.append(stack.pop())
    return walk[::-1]

def shortcut(walk, D):
    if not walk: return 0, []
    seen, tour = set(), []
    for v in walk:
        if v not in seen: seen.add(v); tour.append(v)
    return sum(D[tour[i]][tour[(i + 1) % len(tour)]] for i in range(len(tour))), tour

def opt_tour(n, D):
    if n == 0: return 0, []
    best = min((sum(D[p[i]][p[(i + 1) % n]] for i in range(n)), list(p))
               for p in permutations(range(n)) if p[0] == 0)
    return best

def tsp(pts):
    n = len(pts); D = table(pts)
    edges, w = mst(n, D)
    deg = [0] * n
    for a, b in edges: deg[a] += 1; deg[b] += 1
    odds = [v for v in range(n) if deg[v] % 2]
    best = [None, float('inf')]
    def pairup(left, c, es):          # minimum perfect matching on the odd set
        if not left:
            if c < best[1]: best[0], best[1] = es, c
            return
        a = left[0]
        for k in range(1, len(left)):
            b = left[k]
            pairup(left[1:k] + left[k + 1:], c + D[a][b], es + [(a, b)])
    pairup(odds, 0, [])
    m1 = [[0] * n for _ in range(n)]   # the 2-approximation: doubled tree
    for a, b in edges: m1[a][b] += 2; m1[b][a] += 2
    walk1 = euler(n, m1); c1, t1 = shortcut(walk1, D)
    m2 = [[0] * n for _ in range(n)]   # Christofides: tree + matching
    for a, b in edges: m2[a][b] += 1; m2[b][a] += 1
    for a, b in best[0]: m2[a][b] += 1; m2[b][a] += 1
    walk2 = euler(n, m2); c2, t2 = shortcut(walk2, D)
    return (edges, w, deg, odds, best[1], walk1, c1, walk2, c2) + opt_tour(n, D)

WIT = [[4, 2], [5, 0], [1, 1], [0, 5], [0, 6]]
print(tsp(WIT))

def dr(seed):
    x = seed
    def nxt():
        nonlocal x
        x = 48271 * x % 2147483647
        return x
    return nxt

worst2 = worstc = 0; pmok = oddok = True
for j in range(1, 13):                # instance 1 = the witness; seeds 2..12
    n = 5 + (j - 1) % 4
    if j == 1: pts = WIT
    else:
        g = dr(j)
        pts = [[g() % 6, g() % 7] for _ in range(n)]
    r = tsp(pts)
    pmok &= r[4] <= r[9] / 2 + 1e-9
    oddok &= len(r[3]) % 2 == 0
    worst2 = max(worst2, r[6] / r[9]); worstc = max(worstc, r[8] / r[9])
print(round(worst2, 4), round(worstc, 4), pmok, oddok)

f = lambda t: t / (math.pi * math.sin(t / 2) ** 2)
lo, hi = 0.01, math.pi - 0.01
for _ in range(200):                  # bisection on tan(theta/2) = theta
    mid = (lo + hi) / 2
    if math.tan(mid / 2) - mid < 0: lo = mid
    else: hi = mid
theta = (lo + hi) / 2
print(round(theta, 4), round(f(theta), 5),
      round(2.3311 / math.pi, 5), round(math.sin(2.3311 / 2) ** 2, 5),
      round(f(2.3311), 5))

n = 6; D = [[1000] * n for _ in range(n)]
for a, b, c in [(0, 1, 1), (0, 5, 1), (0, 3, 1), (2, 3, 1), (3, 4, 1), (1, 2, 2), (4, 5, 2)]:
    D[a][b] = D[b][a] = c
edges, w = mst(n, D)
m = [[0] * n for _ in range(n)]
for a, b in edges: m[a][b] += 2; m[b][a] += 2
walk = euler(n, m); c, t = shortcut(walk, D)
viol = sum(1 for a in range(n) for b in range(n) for c_ in range(n)
           if a != b != c_ != a and D[a][c_] > D[a][b] + D[b][c_])
print(w, edges, walk, t, c, opt_tour(n, D), round(c / opt_tour(n, D)[0], 3), viol)
```

**Verified output.** The witness prints the whole chain: MST weight **13** on edges (3,4), (0,1), (0,2), (2,3); degrees (2, 1, 2, 2, 1); odd set **{1, 4}**; its perfect matching costs **11 = OPT/2 exactly** — the lemma tight, both alternating matchings tying at half the optimal tour's **22**; the doubled-tree walk `0 1 0 2 3 4 3 2 0` shortcutting to cost **22** (ratio 1 — the luckiest case); the Christofides walk `0 1 4 3 2 0` giving **24**, ratio 24/22 ≈ **1.091**: the tight link (the matching) and the slack link (the tree at 13 < 22) never tight together. The family run prints `1.5 1.125 True True`: across all twelve instances (the witness plus eleven seeded, n cycling 5 to 8, lattice coordinates from the Lehmer generator at % 6 and % 7) the 2-approximation stays ≤ 2 with worst ratio **1.5** (instance 5), Christofides stays ≤ 1.5 with worst **1.125** (instance 8), the matching lemma holds **12 of 12**, and every odd-degree set is even — practice far inside the guarantees, Exploration 18's gap on the record. The constant prints `2.3311 0.87857 0.74201 0.84457 0.87857`: the ratio θ/(π sin²(θ/2)) minimized where tan(θ/2) = θ, at θ ≈ **2.3311**, value **0.87857** — and the hand-check at the printed θ: θ/π = 0.74201, sin²(θ/2) = 0.84457, their quotient 0.87857 — every digit of Exercise 11's calculus, computed not looked up. The broken metric prints MST **5** on the five cheap edges, walk `0 1 0 3 2 3 4 3 0 5 0`, tour 0-1-3-2-4-5-0 at **2005** against optimum **8** (tour 0-1-2-3-4-5-0) — ratio **250.625** — with exactly **20** ordered triangle violations: the sentence the instance breaks is the shortcut's, and MST ≤ OPT (5 ≤ 8) survives on nonnegativity alone, exactly as A14 says.

### Part 6 — Tutte and the blossoms: the census, the worked instance, the lying states, the engine

```python
from itertools import combinations

def has_pm(n, em):                    # exact perfect-matching DP, bitmask recursion
    if n % 2 or n < 0: return False
    def rec(mask):
        if mask == 0: return True
        v = (mask & -mask).bit_length() - 1
        rest = mask & ~(1 << v)
        for w in range(n):
            if rest >> w & 1 and em[v] >> w & 1 and rec(rest & ~(1 << w)):
                return True
        return False
    return rec((1 << n) - 1)

def tutte_census(n):
    pairs = list(combinations(range(n), 2))
    withpm = without = viol = 0
    for mask in range(2 ** len(pairs)):
        em = [0] * n
        for i, (a, b) in enumerate(pairs):
            if mask >> i & 1: em[a] |= 1 << b; em[b] |= 1 << a
        pm = has_pm(n, em)
        withpm += pm; without += not pm
        bad = False
        for S in range(1 << n):       # Tutte: odd(G - S) <= |S| for every S
            seen = set(); odd = 0
            for v in range(n):
                if S >> v & 1 or v in seen: continue
                comp = [v]; seen.add(v); sz = 1
                while comp:
                    u = comp.pop()
                    for w in range(n):
                        if em[u] >> w & 1 and not S >> w & 1 and w not in seen:
                            seen.add(w); sz += 1; comp.append(w)
                odd += sz % 2
            if odd > bin(S).count('1'): bad = True; break
        viol += pm == bad             # a disagreement with the equivalence, either direction
    return withpm, without, viol
print(tutte_census(4), tutte_census(6))

n = 10; em = [0] * n                  # the worked instance: two C5s bridged at 0-5
def add(a, b): em[a] |= 1 << b; em[b] |= 1 << a
for i in range(5): add(i, (i + 1) % 5); add(5 + i, 5 + (i + 1) % 5)
add(0, 5)
def oddcomps(S):
    seen = set(); odd = 0; comps = []
    for v in range(n):
        if S >> v & 1 or v in seen: continue
        comp = [v]; seen.add(v); mem = []
        while comp:
            u = comp.pop(); mem.append(u)
            for w in range(n):
                if em[u] >> w & 1 and not S >> w & 1 and w not in seen:
                    seen.add(w); comp.append(w)
        odd += len(mem) % 2; comps.append(sorted(mem))
    return odd, comps
eq = [S for S in range(1, 1 << n) if oddcomps(S)[0] == bin(S).count('1')]
maximal = [S for S in eq if not any(T != S and T & S == S for T in eq)]
print([[i for i in range(n) if S >> i & 1] for S in maximal])
print(oddcomps(0b1011), oddcomps(0b11))

def lying_states(n, em):              # naive parity search vs brute-force truth
    edges = [(a, b) for a in range(n) for b in range(a + 1, n) if em[a] >> b & 1]
    lying = []
    def run(match, root):             # returns found?
        lab = [0] * n; lab[root] = 1
        mwith = lambda v: next((e[0] if e[1] == v else e[1] for e in match if v in e), -1)
        ism = lambda a, b: (a, b) in match or (b, a) in match
        found = False; grew = True
        while grew and not found:
            grew = False
            for v in range(n):
                if lab[v] == 2:
                    p = mwith(v)
                    if p >= 0 and lab[p] == 0: lab[p] = 1; grew = True
            for u in range(n):
                if lab[u] != 1: continue
                for w in range(n):
                    if not em[u] >> w & 1 or ism(u, w): continue
                    if mwith(w) < 0 and w != root: found = True; break
                    if lab[w] == 0: lab[w] = 2; grew = True
                if found: break
        return found, lab
    def truth(match, root):           # alternating-path search keyed by parity
        mwith = lambda v: next((e[0] if e[1] == v else e[1] for e in match if v in e), -1)
        ism = lambda a, b: (a, b) in match or (b, a) in match
        seen = set()
        def dfs(v, want_un):
            if (v, want_un) in seen: return False
            seen.add((v, want_un))
            for w in range(n):
                if not em[v] >> w & 1 or ism(v, w) == want_un: continue
                if want_un and mwith(w) < 0 and w != root: return True
                if dfs(w, not want_un): return True
            return False
        return dfs(root, True)
    def all_matchings(i, cur, used):
        if i == len(edges): yield cur; return
        yield from all_matchings(i + 1, cur, used)
        a, b = edges[i]
        if not used >> a & 1 and not used >> b & 1:
            yield from all_matchings(i + 1, cur + [(a, b)], used | 1 << a | 1 << b)
    for match in all_matchings(0, [], 0):
        for r in range(n):
            if any(r in e for e in match): continue
            found, lab = run(match, r)
            if not found and truth(match, r):
                lying.append((match, r, [f'{i}{"AB"[lab[i]-1]}' for i in range(n) if lab[i]]))
    return lying
paw = [0b1110, 0b0101, 0b0011, 0b0001]
c5p = [0] * 6
for i in range(5): c5p[i] |= 1 << (i + 1) % 5; c5p[(i + 1) % 5] |= 1 << i
c5p[0] |= 1 << 5; c5p[5] |= 1
print(lying_states(4, paw))
print(lying_states(6, c5p))

def max_matching(n, em):              # Edmonds' blossom, classical port
    if n <= 1: return []
    adj = [[bool(em[i] >> j & 1) for j in range(n)] for i in range(n)]
    match = [-1] * n; p = [-1] * n; base = list(range(n))
    used = [False] * n; bl = [False] * n; q = []
    def lca(a, b):
        vis = [False] * n
        while True:
            a = base[a]; vis[a] = True
            if match[a] == -1: break
            a = p[match[a]]
        while True:
            b = base[b]
            if vis[b]: return b
            b = p[match[b]]
    def mark(v, b, child):
        while base[v] != b:
            bl[base[v]] = bl[base[match[v]]] = True
            p[v] = child; child = match[v]; v = p[match[v]]
    def find_path(root):
        for i in range(n): used[i] = False; p[i] = -1; base[i] = i
        used[root] = True; q.append(root); qh = 0
        while qh < len(q):
            v = q[qh]; qh += 1
            for to in range(n):       # adjacency scanned in ascending order
                if not adj[v][to] or base[v] == base[to]: continue
                if to == root or (match[to] != -1 and p[match[to]] != -1):
                    cb = lca(v, to)
                    for i in range(n): bl[i] = False
                    mark(v, cb, to); mark(to, cb, v)
                    for i in range(n):
                        if bl[base[i]]:
                            base[i] = cb
                            if not used[i]: used[i] = True; q.append(i)
                elif p[to] == -1:
                    p[to] = v
                    if match[to] == -1:
                        u = to          # augment back to the root
                        while u != -1:
                            pv = p[u]; ppv = match[pv]
                            match[u] = pv; match[pv] = u; u = ppv
                        return True
                    else: q.append(match[to]); used[match[to]] = True
        return False
    for i in range(n):
        if match[i] == -1: find_path(i)
        q.clear()
    return sorted((i, v) for i, v in enumerate(match) if i < v)

print(max_matching(4, paw))
print(max_matching(6, c5p))
pet = [0] * 10
def addp(a, b): pet[a] |= 1 << b; pet[b] |= 1 << a
for i in range(5): addp(i, (i + 1) % 5); addp(5 + i, 5 + (i + 2) % 5); addp(i, 5 + i)
print(max_matching(10, pet))

def max_match_dp(n, em):              # exact bitmask DP for the census
    if n <= 1: return 0
    memo = [-1] * (1 << n)
    def rec(mask):
        if mask == 0: return 0
        if memo[mask] >= 0: return memo[mask]
        v = (mask & -mask).bit_length() - 1
        rest = mask & ~(1 << v)
        best = rec(rest)
        for w in range(n):
            if rest >> w & 1 and em[v] >> w & 1:
                best = max(best, 1 + rec(rest & ~(1 << w)))
        memo[mask] = best
        return best
    return rec((1 << n) - 1)

mism = total = 0
for n_ in range(2, 7):
    pairs = list(combinations(range(n_), 2))
    for mask in range(2 ** len(pairs)):
        em_ = [0] * n_
        for i, (a, b) in enumerate(pairs):
            if mask >> i & 1: em_[a] |= 1 << b; em_[b] |= 1 << a
        mm = max_matching(n_, em_)
        total += 1
        mism += len(mm) != max_match_dp(n_, em_)
print(total, mism)

smism = 0
for s in range(1, 31):                # 30 seeded: 15 on 10 vertices, 15 on 12
    n_ = 10 if s <= 15 else 12
    x = s
    em_ = [0] * n_
    for a in range(n_):
        for b in range(a + 1, n_):
            x = 48271 * x % 2147483647
            if x % 2: em_[a] |= 1 << b; em_[b] |= 1 << a
    smism += len(max_matching(n_, em_)) != max_match_dp(n_, em_)
print(smism)
```

**Verified output.** The Tutte census prints `(37, 27, 0)` and `(24823, 7945, 0)`: on 4 vertices **37** graphs have a perfect matching and **27** do not; on 6, **24,823** and **7,945** — 32,832 graphs, and the equivalence PM ⟺ odd(G − S) ≤ |S| holds with **zero** violations in both directions on every one. The worked instance prints the six maximal equality sets exactly — **{0,1,3}, {0,2,3}, {0,2,4}, {5,6,8}, {5,7,8}, {5,7,9}** — then `(3, [[2], [4], [5, 6, 7, 8, 9]])` for S = {0,1,3}: three odd components, the singletons and the second C₅, and `(2, [[2, 3, 4], [5, 6, 7, 8, 9]])` for the trap S = {0,1}: an equality set, but its path component 2-3-4 is the one that is not factor-critical (delete the center and two isolated vertices remain — the machine checks all three deletions), so the proof's maximality is load-bearing, exactly as §6.3 and Exercise 9(d) argue. The lying-state enumeration prints, for the paw, `[((0, 2), 1, ['0B', '1A', '2B']), ((0, 1), 2, ['0B', '1B', '2A'])]` — the two mirror states, matched edge inside B, the labels in vertex order exactly as the enumeration prints them (§6.1 narrates the same labels in discovery order) — and for the pendant C₅ `[((0, 4), (2, 3), 1, ['0B', '1A', '2B', '3A', '4A']), ((0, 1), (2, 3), 4, ['0B', '1A', '2A', '3B', '4A'])]` — the two states with the unmatched edge inside A: **exactly four lying states**, two per graph, one per symmetry class each, and no others among all matchings and all exposed roots. The engine prints the paw's perfect matching `[(0, 3), (1, 2)]` — the second augmentation contracting the triangle 2-0-1 and lifting the path 2-1-0-3, as §6.2 narrates — the pendant C₅'s `[(0, 5), (1, 2), (3, 4)]`, and the Petersen graph's `[(0, 1), (2, 3), (4, 9), (5, 7), (6, 8)]`. The census prints `33866 0`: the blossom engine agrees with the exact bitmask DP on **every** labeled graph on 2 to 6 vertices, zero mismatches — and the seeded run prints `0`: thirty instances (fifteen on 10 vertices, fifteen on 12, edges drawn from the Lehmer generator), all agreeing. Implementation reality matches the cited theory everywhere the machine can see.
