---
name: "cgt-book-basis"
title: "The CGT Atlas — Book Basis (what the book is, what it was built from, how to rebuild it)"
type: "text/markdown"
---

# 📘 The CGT Atlas — Book Basis

*The durable, history-free basis of the book: what it is, its chapter structure, its pattern index, the editorial and verification conventions it was built under, the build pipeline, and the sources it was mined from. Written at the great cleanup (2026-10-26) by extracting the load-bearing parts of the old master plan; all session history was deliberately purged. The chapters themselves (`cgt-ch*.md`) remain the source of truth — this file is the map, not the territory.*

## What the book is

**The Combinatorics & Graph Theory Atlas** — a lecture-course textbook in 21 chapters (five volumes), written as *Feynman-style* lecture courses: intuition and story before formalism, complete proofs inside the narrative, "how you could have found this" reconstructions, dialogue with the reader, a compact reference card at the end of each chapter. Problems are grouped not by topic but by the *move that solves them* — the Master Pattern Index below is the book's organizing spine. Every chapter carries a machine-verified computational lab, a graded exercise set with worked answers, and ◆ pattern-unknown exercises; an unnumbered Lean Formal Track companion (`cgt-lean-track.md`) shadows the whole book.

## Chapter map

| Ch. | Title | Volume | Contents |
|-----|-------|--------|----------|
| 1 | Counting & Enumeration | I — the canon | bijections, inclusion–exclusion, recurrences, generating functions |
| 2 | Graph Theory Core | I | degrees, trees, cycles, Euler tours, Cayley, **Dirac, Pósa/Chvátal, Gallai–Milgram** |
| 3 | Coloring, Ramsey & Extremal | I | pigeonhole, Ramsey bounds, Mantel/Turán, planarity |
| 4 | The Probabilistic Method | I | expectation, union bound, alteration, **second moment, Local Lemma** |
| 5 | Matching, Flows & Hall | I | augmenting paths, König duality, max-flow min-cut |
| 6 | Linear-Algebraic Methods | I | Fisher, de Bruijn–Erdős, Oddtown/Eventown (+ mod-p, △-parity), RCW/Frankl–Wilson + Ramsey graphs, friendship theorem, the linear-algebra canon |
| 7 | Extremal Set Systems | I | Sperner/LYM + SCD, Erdős–Ko–Rado + uniqueness, Bollobás two-families, shifting, the skew Bollobás landscape, Hilton–Milner/AK gateway, union-closed lore |
| 8 | Spectral Methods and the Modern Toolkit | II — planned expansions | spectral averaging + expander-mixing; Motzkin–Straus + spectral Turán; two-distance sets; interlacing/Hoffman/theta/Delsarte — four advanced lectures exported from Ch. 6 |
| 9 | Sumsets and Shadows: the Completed Arcs | II | the staircase + Cauchy–Davenport; Kneser + EGZ; the aperiodic assembly; shadows/Kruskal–Katona; the EKR thin range — the sumsets/shadows lectures exported from Ch. 7 + two closure lectures |
| 10 | Ramsey Theory in Depth | II | infinite Ramsey, van der Waerden, Schur, Hales–Jewett statement, lower-bound techniques |
| 11 | Algorithms & Complexity of Combinatorics | II | the NP-completeness spine (3-SAT → IS → clique → vertex cover; 3-coloring + Hamiltonian cycle cited), greedy set cover + the harmonic ceiling, matroids + Rado–Edmonds, min-cost flow + assignment, TSP 2-approx + Christofides 3/2 + GW 0.878, blossoms |
| 12 | The Olympiad Bridge | II | 30 competition problems (IMO/ISL, verifiable citations) mapped onto the Atlas patterns P1–P26, difficulty ladder, no new machinery |
| 13 | The Probabilistic Method, Act II | III — approved extensions | correlation/FKG + Kleitman; Janson + the Poisson paradigm; martingales + Azuma–Hoeffding (+ Talagrand st.); random-graph evolution — G(n,p), thresholds, the giant component; discrepancy (Spencer's six standard deviations); the entropy method (Brégman, Moser) |
| 14 | Regularity and Density | III | the Szemerédi regularity lemma + counting/removal; Erdős–Stone + stability; triangle removal + Roth; density Ramsey (Szemerédi's AP theorem + density HJ); cap set (Croot–Lev–Pach / Ellenberg–Gijswijt slice rank) |
| 15 | Graph Structure: Minors, Perfect Graphs, and the Limits of Coloring | III | treewidth + minors (Robertson–Seymour + grid, statements; DP on decompositions); Hadwiger (k = 4 proved; k = 5 ↔ 4CT st.); list coloring (Thomassen, Galvin, Voigt); discharging; nowhere-zero flows (Tutte 5-flow; the 4-flow conjecture st.) |
| 16 | Symmetry, Inversion, and Design | III | Pólya/Burnside; Möbius inversion on posets; designs I (Steiner, Fisher, projective planes, S(2,3,6)); designs II (Wilson + Keevash st.); coding beyond Hamming (Singleton/MDS, Plotkin, Gilbert–Varshamov; codes ↔ designs; Ch. 8 Delsarte) |
| 17 | The Semi-Random Method | IV — survey-proposed | the nibble paradigm as its own subject: expose a little randomness at a time and track a parameter through each nibble — Rödl 1985 (the Erdős–Hanani conjecture), Pippenger–Spencer 1989 (the formalization), Kahn's application, the Ajtai–Komlós–Szemerédi and Kim ancestry |
| 18 | Thresholds and Windows | IV | the threshold phenomenon as its own subject, beyond Ch. 13 L4's evolution lecture: Erdős–Rényi thresholds and scaling windows, coarse vs sharp, Friedgut–Kalai sharp thresholds, the Kahn–Kalai expectation-threshold conjecture and its Park–Pham 2022 proof, the Boolean-function machinery |
| 19 | The Lovász Local Lemma | V — second survey-adoption wave | the local lemma as its own subject: the 1975 origin and the union bound's incomparability, the symmetric form, Spencer's general asymmetric form with the seat calculus and printed floors, the lopsided variant (Erdős–Spencer 1991) and Latin transversals, the Moser–Tardos constructive proof |
| 20 | Named Methods | V | the survey's named methods with details and usage, one lecture each: the container method (Balogh–Morris–Samotij, Saxton–Thomason), analytic combinatorics (Flajolet–Sedgewick), flag algebras (Razborov; the Reiher clique-density and Hatami descendants), absorption (Keevash), and the rest |
| 21 | The Engines | V | the engine layer behind the patterns, one lecture each: Wilson's elementary-number-theory PBD existence engine, Gleason's invariant theory, the Luks permutation-group framework, Kruskal's greedy-exchange/cut property, the N4 k-adic digit engine |

**The Lean Formal Track** (`cgt-lean-track.md`) — the unnumbered living companion that shadows the whole book: as each chapter is written or rewritten, its key statements get Lean 4 drafts there. Touched at the very end, after every numbered chapter; never claimed verified until the reader reports a successful build (Lean cannot run in the authoring sandbox).

## The Master Pattern Index (P1–P45)

The central idea: problems are grouped by the *move that solves them*. The canonical registry — every pattern's canonical name, gloss, home chapters, plus every alias the book has used and a machine-readable JSON payload (P-ID = the join key, IDs immutable) — is `cgt-pattern-map.html`. The index:

| ID | Pattern | One-line description | Home chapters |
|----|---------|----------------------|---------------|
| P1 | **Bijection** | Count A by matching it 1-to-1 with a set B you can count | 1, 2 |
| P2 | **Double counting** | Count the same set two ways; equate | 1, 2, 3 |
| P3 | **Inclusion–exclusion** | Add, subtract overlaps back | 1 |
| P4 | **Recurrence + induction** | Relate case n to smaller cases | 1, 2, 3 |
| P5 | **Generating function** | Turn a sequence into a function; let algebra work | 1 |
| P6 | **Complement / reflection** | Count the complement or reflect the bad objects | 1 |
| P7 | **Parity & handshaking** | Degree-sum is even; ends of arguments | 2 |
| P8 | **Longest-path / extremal** | Take an extremal object; its structure forces a cycle, leaf, etc. | 2, 3 |
| P9 | **Pigeonhole** | n+1 objects, n boxes — and the lower the contest level, the more it carries the whole proof (the survey's level gradient: Putnam small-step, USAMO obstruction, IMO whole-proof engine) | 3 |
| P10 | **Averaging / expectation** | Some object beats the average | 3, 4 |
| P11 | **Explicit construction** | Beat the bound by *building* the object | 3 |
| P12 | **Random construction** | Prove existence by sampling | 4 |
| P13 | **Union bound** | If failure probabilities sum below 1, success exists | 4 |
| P14 | **Alteration** | Random object + pruning | 4 |
| P15 | **Induction on vertices/edges** | Delete a vertex, extend the solution | 2, 3 |
| P16 | **Alternating paths / augmentation** | Improve a partial solution along a path | 5 |
| P17 | **Duality (min–max)** | Two problems are the same number | 5 |
| P18 | **Algorithmic proof** | The proof *is* a procedure; termination = theorem | 2, 5 |
| P19 | **Rank / linear algebra** | Encode sets as vectors; dimension bounds | 6 |
| P20 | **Weight shifting / symmetrization** | Push weight to the extremal configuration | 3, 6 |
| P21 | **Spectral / Rayleigh** | Eigenvalues as averaging devices; operator norm on 1⊥ | 6 |
| P22 | **Polynomial method** | Encode sets as polynomials; dimension counting | 6 |
| P23 | **Compression / shifting** | Replace sets by canonical "heavier" ones without losing the property | 7 |
| P24 | **Shadow pricing (Kruskal–Katona)** | Price a family by its own real parameter x: a k-family of size C(x, k) forces every j-shadow to size ≥ C(x, j) — equality only at integer x and the complete families | 7, 9 |
| P25 | **Reduction / encoding** | Translate one problem into another’s language; the target structure carries the proof or the hardness | 3, 10, 11 |
| P26 | **Compactness (finite ↔ infinite)** | Prove the infinite statement, pull the finite one back via König’s lemma — or push the finite one to a limit | 2, 10 |
| P27 | **Correlation** | Up-sets lean together: P(∩ good) ≥ ∏P(good) is a floor — FKG beyond product measure | 13 |
| P28 | **Concentration** | Bounded exposure cannot stray far from its mean — Azuma, Talagrand | 13 |
| P29 | **Entropy counting** | Count by description cost: H ≤ log support + the chain rule | 13 |
| P30 | **Regularity partitioning** | Every large graph is a bounded quasirandom blow-up; refine until the noise is uniform | 14 |
| P31 | **Counting–removal** | Regular structure multiplies densities; few copies ⟹ few deletions | 14 |
| P32 | **Stability** | Near-extremal objects sit near the extremal configuration, not merely near its count | 14 |
| P33 | **Density increment** | If the structure you want is nowhere, refine: some cell gains density | 14 |
| P34 | **Minor chasing** | Build a shadow-clique from disjoint connected branch sets; deletion and contraction are the moves | 15 |
| P35 | **Dynamic programming on structure** | Tree decompositions turn global problems into bag-local recurrences | 15 |
| P36 | **Discharging** | Give every local object a charge; Euler’s formula fixes the total; some local configuration must go into deficit | 15 |
| P37 | **Duality** | Two theories, one object: plane duals exchange vertex-coloring with edge-flowing | 15 |
| P38 | **Replication** | Duplicate a vertex to force structure; twins inherit and transmit perfection | 15 |
| P39 | **Symmetry averaging** | To count what symmetry identifies, average fixed points over the group; the cycle index prices each symmetry’s orbit structure | 16 |
| P40 | **Möbius inversion** | Invert summatory functions on a poset: the μ function strips double-counted weight back to the primitive layer | 16 |
| P41 | **Double-counting & divisibility** | Integrality of the replication numbers r and λ is a design’s birth certificate: non-integral parameters forbid existence before any search | 16 |
| P42 | **Words-as-designs** | A code’s weight classes can carry Steiner structure: Assmus–Mattson turns distance into t-designs (Golay → Witt) | 16 |
| P43 | **Semi-random nibble** | Reveal a tiny random slice of the structure at a time and track one parameter through every nibble: the tracked quantity moves by honest conditional expectation each round, so the process converges on the full structure (Rödl's nibble; Pippenger–Spencer) | 17 |
| P44 | **Threshold / window** | The window is the theorem: a random structure's property turns on inside a scaling window whose position and width carry the information (Erdős–Rényi evolution; Friedgut–Kalai sharpness; the Kahn–Kalai expectation threshold, proved Park–Pham) | 18 |
| P45 | **Local lemma** | Rare, sparsely dependent bad events can be simultaneously avoided: certify survival seat by seat — p_i ≤ x_i·∏_{j∈Γ(i)}(1−x_j) — when no union bound can total them (Erdős–Lovász 1975; Spencer's asymmetric form; the lopsided variant; Moser–Tardos's resampling algorithm; Shearer's boundary) | 19 |

## Editorial & verification conventions (the basis the book was built under)

- **Notation.** n = number of vertices, m = number of edges, d(v) = degree, Δ = max degree, χ = chromatic number, α = independence number, ω = clique number, C(n,k) = binomial "n choose k".
- **"Complete proof"** = every logical step present. **"Sketch"** = the architecture is given; the missing steps are named.
- **Sources of truth for statements** — classic texts to verify against when extending: van Lint & Wilson *A Course in Combinatorics*; Diestel *Graph Theory*; Alon & Spencer *The Probabilistic Method*; Bollobás *Extremal Graph Theory*; Lovász *Combinatorial Problems and Exercises*; Stanley *Enumerative Combinatorics I*; West *Introduction to Graph Theory*; Engel *Problem-Solving Strategies*.
- **Computational labs.** Every chapter carries a lab: the algorithm is executed and verified in-session (the sandbox has an operation budget, so labs use small n / few trials), embedded as portable Python 3 for the reader's machine, with the actual verified outputs recorded — never invented. The reader's own machine (e.g., a Raspberry Pi) has no budget: scale n up there.
- **Verification levels (strongest → weakest).** (1) *Executed lab* — algorithm ran in-session, outputs recorded. (2) *Complete human proof* — every logical step present. (3) *Flagged sketch* — architecture given, missing steps named. (4) *Formal track* — Lean 4 code written for the reader to compile; **never claimed verified until the reader reports a successful build** (Lean cannot run in the authoring sandbox).
- **Editorial standard — the Feynman rule.** Chapters are written as *lecture courses*: intuition and story before formalism; complete proofs inside the narrative; "how you could have found this" reconstructions; dialogue with the reader ("compute it yourself before reading on"); a compact reference card at the end. Chapter 1 is the model (session 5). Reference-edition chapters are re-issued lecture-style one per session; new chapters ship lecture-style from the start. The Lean formal track (Ch. 17) stays a single living cross-cutting companion, updated as chapters are written or rewritten — never one Lean chapter per math chapter.
- **Editorial standard — the web edition** (adopted session 21, on the user's request): every chapter ships alongside its markdown canvas a **web edition** — a standalone HTML page embedding the chapter source byte-identically (base64 payload) and rendering it client-side with the export-safe CSS (`white-space: pre`, `break-inside: avoid`, A4 `@page` print rules). Print-to-PDF from any browser is the Atlas's standard PDF route while the platform's export pipeline is broken. Feynman rewrites and new chapters get their web edition at delivery time (Ch. 1–4 have theirs). **The rebuild rule:** a chapter edit invalidates its web edition — rebuild and re-verify byte-exact on every source change; a stale embed is a defect. The markdown canvas stays the authoritative source. **Web-frame retirement (session 78, user-directed):** the per-chapter web-edition canvases are retired from the durable master copy — every frame's payload is its chapter master and the renderMd v2 engine is byte-identical (md5 d5eaa031…) across all sixteen, so only one frame survives: `cgt-render-engine.md`, the canonical frame/engine master (the session-77 canary). A chapter edit no longer builds a web edition; it rebakes the .html export directly from the chapter master via the canonical frame (see the HTML export format convention).
- **Editorial standard — the exercise system** (adopted session 7, on the user's request): every chapter carries a graded exercise set — ●○○ easy (direct application of one lecture idea), ●●○ moderate (two ideas or one tricky step), ●●● tough (several chapter ideas combined) — with hints inline and complete worked answers at the end of the chapter, so the learner tries first and checks later. Chapters 1 and 3 are the models.
- **Editorial standard — the discovery cycle** (adopted session 8, from the external review of Ch. 1): every lecture aims to place the reader in the discoverer's seat — **Encounter** (surprising concrete problem) → **Experiment** (small cases, by hand or code) → **Conjecture** (predict before the formula) → **Struggle** (try a method, including a plausible wrong one — show the wrong turn that teaches) → **Explain** (the rigorous argument, verified) → **Generalize** (change the problem; see what survives). The sixth stage is where research begins. Discovery checkpoints (short "try it yourself before reading on" moments) are being retrofitted into existing lectures via the improvement trackers.
- **Explorations category** (adopted session 8): beyond the graded set, each chapter may carry ◐ **Explorations** — open-ended investigations with no single right answer. Each states *what you should find* (the law, the pattern, the shape of the answer) rather than a number to match. These are research-style training, not test preparation.
- **Labs test mappings, not just totals** (adopted session 8 — learned the hard way when a wrong reflection-bijection inverse survived because the totals happened to match): when a chapter claims a bijection, the lab implements the map **and its inverse** and round-trips them over *all* small inputs. Matching totals certify a count; only round-trips certify a correspondence.
- **Pattern-unknown ◆ exercises** (adopted session 10, from the second external review of Ch. 1): every chapter's exercise set ends with a few problems that name *no* method and carry no hint — the reader must diagnose which tool fits (inclusion–exclusion, bijection, recurrence, double counting…). Difficulty ratings are withheld too: sizing an unseen problem is part of the problem. Worked answers still go at the end. Ch. 1's three (subsets-without-consecutives → Fibonacci; even/odd subset involution; line-arrangement regions) are the models.
- **Small-case tests are detectors, not proofs** (adopted session 10): labs and round-trip checks certify the cases they run; general claims are settled by arguments. A chapter may never say or imply that computation replaces proof — and every lab should state what it does *not* establish.
- **Revision history lives in an appendix, not in the lectures** (adopted session 11, from the third external review of Ch. 1): chapters never interrupt the lecture body with session numbers, review stories, or correction history. Each chapter closes with a *Revision History & Verification Notes* appendix (editions, verification record, lab/rendering notes, standing decisions). Ch. 1 is the model.
- **Publishing and pipeline material lives in the publishing toolkit, not in chapter appendices** (adopted session 17, from the seventh external review of Ch. 1): chapters keep at most a one-paragraph rendering note in their revision appendix; export configuration, verification scripts, and standalone code distributions belong to the publishing toolkit canvas. Chapters are mathematics; the toolkit is plumbing.
- **Chapter numbering (session 56, user-directed).** The Lean Formal Track moved from Ch. 13 to the end as Ch. 17 (the last chapter); the four Volume III chapters shifted one step ahead — Probabilistic Act II 14 → 13, Regularity 15 → 14, Graph Structure 16 → 15, Symmetry & Design 17 → 16 — so Volume III is now Ch. 13–16. Historical session-log rows and completed-ledger lines keep the numbering of their time; every current-facing surface (chapter texts, web editions, .html exports, the chapter map, the pattern indexes, the project KNOWLEDGE) carries the new numbers. Chapter references are context-anchored tokens (Ch. N / Chapter N / chN) — never bare numbers.
- **Chapter numbering, second pass (session 80, user-directed).** The Lean Formal Track's Ch. 17 number was CANCELLED — the track is an unnumbered project idea, touched at the very end, after every numbered chapter; the two survey-proposed chapters take the freed numbers as Ch. 17 (The Semi-Random Method, P43's home) and Ch. 18 (Thresholds and Windows, P44's home) in the new Volume IV. Historical session-log rows and completed-ledger lines keep the numbering of their time (a pre-session-80 row that says Ch. 17 = the Lean track remains honest); every current-facing surface carries the new state. Chapter references stay context-anchored tokens (Ch. N / Chapter N / chN) — never bare numbers.

### Quality checklist (apply to every chapter)

- Every problem has ≥ 2 genuinely different solution methods
- Every method names its pattern ID from the master index
- Every proof is complete or explicitly labelled "sketch" with what's missing
- Every chapter carries a verified Computational Lab (the algorithm executed and outputs recorded — never invented)
- Graded exercises ●○○/●●○/●●● with inline hints + complete worked answers; ◆ pattern-unknown exercises at the end (no method named, no hint, difficulty withheld); ◐ Explorations (open-ended, state what you should find)

## The build pipeline (how the book is physically built)

- **Masters are the source of truth:** each chapter is a standalone Markdown master (`cgt-ch*.md`), written and extended extend-never-rewrite; revision history lives in an appendix at the end of each master, never in the lecture body.
- **The render engine:** `cgt-render-engine.md` carries the canonical `renderMd` engine. Each chapter's **web edition** is a standalone, script-free, pre-rendered plain-HTML page (`cgt-ch*-web.html`): head + rendered body + tail, built by rendering the master's payload through the engine — no MathJax, no CDN, no script; plain-Unicode mathematics only ($-TeX is banned from the book by standing decision). Exports carry no appendices: the payload runs from the chapter title to the last lecture content, stopping before the Revision History section.
- **The publishing toolkit:** `cgt-publishing.md` holds export configuration, the post-export verification scripts, and standalone runnable copies of chapter lab code. Chapters are mathematics; the toolkit is plumbing.
- **Verification discipline:** every claim adopted into a master is machine-verified before installation; labs test mappings, not just totals (a bijection claim requires implementing the map AND its inverse and round-tripping them); small-case tests are detectors, not proofs; a chapter may never imply that computation replaces proof.

## The sources (what the book was built from)

- **`papers/`** — the mined primary literature: `SOURCES.md` (the source list), ~160 per-paper notes (`A1–Y7`: one note per paper — claim, proof idea, pattern read), `CORPUS.md` + `ANALYSIS.md` (the corpus and its pattern analysis), `TEACHING.md`/`TEACHING-CENSUS.md` + `CONTEST.md`/`CONTEST-CENSUS.md` (the teaching-textbook and competition censuses), and `patterns/` (the per-pattern census over the corpus). The pattern index above was tested against actual field practice through this corpus; the Volume IV–V chapters were proposed by it.
- **Classic texts** (the sources of truth for statements, per the conventions above): van Lint & Wilson *A Course in Combinatorics*; Diestel *Graph Theory*; Alon & Spencer *The Probabilistic Method*; Bollobás *Extremal Graph Theory*; Lovász *Combinatorial Problems and Exercises*; Stanley *Enumerative Combinatorics I*; West *Introduction to Graph Theory*; Engel *Problem-Solving Strategies*.
- **Competition corpus:** Ch. 12's 30 problems (IMO/ISL 1964–2023, verifiable citations) + the contest census above.

## How to rebuild / extend the book

1. The chapters, this basis file, the pattern registry, and `papers/` are the complete durable state — that is the point of this file.
2. To extend or revise: work extend-never-rewrite on the master, machine-verify every adopted claim (labs re-run exactly as printed), re-render the web edition through the engine, and keep the revision appendix current.
3. To rebuild editions (print, PDF, other formats): start from the masters; the pipeline conventions above (pre-rendered script-free HTML, plain Unicode, no appendix leakage) are the standard.
4. A book-building skill pipeline (chunked authoring, machine-verified labs, adversarial review, expansion passes driven by fresh drafts) is the authoring model the book was actually built with — follow it for new material rather than rewriting wholesale.
