---
name: "cgt-lean-track"
title: "The Lean Formal Track — A Living Companion to the Whole Atlas"
type: "text/markdown"
---

# The Lean Formal Track

*Not a chapter of the book — an unnumbered companion that shadows the whole book (its Ch. 17 number was cancelled at session 80; the track is touched at the very end, after every numbered chapter). As each chapter is written (or rewritten), its key statements get Lean 4 drafts here. One track, updated forever, covering everything before and after it.*

## 0. Why this track exists

The book you are reading is a human proof. A human proof is an argument designed to make another human say "ah, yes." A machine proof is an argument designed to leave a machine *no room to disagree*. Both are mathematics, but they are different crafts, and this century rewards the people who can speak both — because the communication channel between humans and provers is exactly the place where claims become checkable and errors become impossible to hide.

The honest position, stated once and then enforced by the conventions below: **nobody knows whether an AI system "understands" a proof, and nobody knows what understanding even is in a human head. What we can have is verifiable communication** — formal artifacts that compile or don't. That is what this chapter produces. A lemma is *done* here only when it has compiled on a reader's machine; everything else is honestly labeled a draft.

## 1. The contract (verification level 4 of the Atlas ladder)

1. **The Atlas drafts** Lean 4 + Mathlib code for a theorem, with the human proof (and its home chapter) referenced beside it.
2. **A reader compiles** the draft on their own machine — Lean needs a real toolchain and Mathlib, which cannot run in the authoring sandbox.
3. **The reader reports back** the exact errors (copy-paste, not paraphrase).
4. **The Atlas repairs** the draft; repeat until `lake build` is silent.
5. Only then is the lemma stamped **machine-verified (reader build X)** here and cross-referenced in its home chapter. Until then, every block below carries the label: **DRAFT — NOT YET COMPILED.**

The corollary to keep in mind: a wrong-but-compiling proof is impossible here (the kernel checks it), but a *draft that fails to compile* is routine and is not a failure of the method — it is the method working, one loop at a time. Expect names of Mathlib lemmas to drift between versions; that is the most common repair.

**Setting up (reader's machine, e.g. a Raspberry Pi 5 with ≥ 4 GB RAM — expect the first Mathlib build to take a long while; use the pre-built cache via `lake exe cache get`):**
```
curl -L https://raw.githubusercontent.com/leanprover/elan/master/elan-init.sh | sh
lake +leanprover-community/mathlib4:lean-toolchain new Atlas math   # creates a project depending on Mathlib
cd Atlas
lake update && lake exe cache get   # fetches prebuilt Mathlib
# paste a draft into Atlas.lean, then:
lake build
```
(Toolchain invocations evolve; the leanprover community's "Getting Started" pages are canonical when this drifts.)

---

## 2. Warm-up 1 · The Handshaking Lemma *(Atlas Ch. 2, Lecture 1)*

**The math.** For every graph: Σ_{v} d(v) = 2m; consequently the number of odd-degree vertices is even. The human proof counts the ends-table two ways (P2) and peels parity (P7).

**Lean 4 + Mathlib draft.** In Mathlib a simple graph on vertex type `V` is `SimpleGraph V`; adjacency is `G.Adj x y`; the degree is `G.degree v = (G.neighborFinset v).card`; the edge set finset is `G.edgeFinset`.

```lean
import Mathlib

/-! ## Atlas Warm-up 1 — the Handshaking Lemma
    Home chapter: Ch. 2, Lecture 1.  DRAFT — NOT YET COMPILED. -/

variable {V : Type*} [Fintype V] [DecidableEq V]

namespace Atlas.Handshaking

/-- **Handshaking.** The degrees sum to twice the number of edges.
    Tier A: Mathlib already ships this fact; the exact name drifts
    between Mathlib versions. Try the line below; if it fails, ask
    Lean to search for the right name and substitute. -/
theorem handshaking (G : SimpleGraph V) [DecidableRel G.Adj] :
    ∑ v : V, G.degree v = 2 * G.edgeFinset.card := by
  exact G.sum_degrees_eq_twice_card_edges
  -- If the name above has drifted, replace with:
  --   exact?     (after `import Mathlib`), or search the docs for
  --   `sum_degrees_eq`.

/-- Corollary: an even number of vertices have odd degree.
    Tier A: Mathlib already ships this too — `SimpleGraph.even_card_odd_degree_vertices`
    (the DegreeSum file's own handshaking corollary); the `sorry` below stays
    deliberately open as the first repair target for the reader loop.
    DRAFT — plan: split the sum over odd/even-degree vertices using
    `Finset.sum_filter` (or sum over `Finset.filter (fun v => ¬Even (G.degree v))`)
    and apply `handshaking`; the odd part's parity is forced. -/
theorem even_number_of_odd_degrees (G : SimpleGraph V) [DecidableRel G.Adj] :
    Even (Finset.univ.filter (fun v => ¬Even (G.degree v))).card := by
  sorry   -- deliberately open: first repair target for the reader loop

end Atlas.Handshaking
```

**Tier B — prove it from first principles (for the reader who wants the real exercise).** The human proof counts incidences I = {(v, e) : v is an endpoint of e} two ways: by vertices (row sums = degrees) and by edges (column sums = 2 each). The Lean plan, commented, maps each human step to a tactic move:

```lean
/-- Tier B plan (human proof ↦ Lean moves). DRAFT — NOT YET COMPILED.
(1) Expand each degree as a sum over edges incident to v:
      `G.degree v = ∑ e ∈ G.edgeFinset, if v ∈ (e : Sym2 V) then 1 else 0`
    (via `Finset.card_eq_sum` / `Finset.sum_ite` machinery;
     `Sym2` membership for edges).
(2) Swap the order of summation: `Finset.sum_comm` — the ends-table flip.
(3) Inner sum is 2 for every edge (an edge has exactly two ends;
    `Sym2` two-ends lemma) — each column has two ✓'s.
(4) Collect: ∑_v d(v) = ∑_e 2 = 2 * card. ∎ -/
```

**What the warm-up teaches even before it compiles:** the *shape* of formalization — a bijection-free double count becomes a `Finset.sum_comm`; "obviously each edge has two ends" is the only genuinely mathematical content and must be a named Sym2 lemma. Formalization is an X-ray of the human proof: it shows you which steps were load-bearing and which were decoration.

**Status: awaiting first reader build.** Report output/errors verbatim; the Atlas repairs.

---

## 3. Warm-up 2 · Sperner's theorem *(planned; home: Ch. 7)*

Statement target: an antichain of subsets of a finite type has size at most the middle binomial coefficient; ideally prove the LYM inequality on the way (the human proof of Ch. 7 §7.1 chains through it). Mathlib's `Finset α` and `Equiv.Perm` (the symmetric group, for the chain-counting) are the natural setting; the cyclic-permutation counting of the LYM proof will need a `Finset.card_image_le`-style argument. Tier A, stated now for honesty as with Warm-up 1: Mathlib already ships Sperner's theorem and both LYM inequalities (`Mathlib.Combinatorics.SetFamily.LYM`) — the Atlas target is the Tier-B exercise of rebuilding them via the cyclic-permutation proof. Draft lands after Warm-up 1's loop closes — one warm-up in the air at a time.

## 4. The statement bank (grows as chapters are written/rewritten)

| # | Statement | Home | Status |
|---|-----------|------|--------|
| 1 | Handshaking + odd-degree corollary | Ch. 2 (Lecture 1) | 📝 draft above, awaiting build |
| 2 | Sperner / LYM | Ch. 7 | 📋 planned |
| 3 | δ ≥ 2 ⇒ contains a cycle (P8 engine) | Ch. 2 (Lecture 2) | 📋 planned — natural `SimpleGraph` exercise |
| 4 | Tree characterizations (the three-way door) | Ch. 2 (Lecture 3) | 📋 planned — large; may become three lemmas |
| 5 | Cayley via Prüfer (P1) | Ch. 2 (Lecture 4) | 📋 ambitious; state `Enc`/`Dec` first |
| 6 | Euler-tour iff even degrees | Ch. 2 (Lecture 5) | 📋 planned |
| 7 | Dirac / Ore | Ch. 2 (Lecture 6) | 📋 planned — the Ch. 6 spectral friends will follow |
| 8 | Oddtown (F₂ rank bound) | Ch. 6 | 📋 planned — needs a matrix-rank detour |
| 9 | Derangement recurrence D_n = (n−1)(D_{n−1}+D_{n−2}) | Ch. 1 (Lecture 1) | 📋 planned |

Ordering principle: one warm-up loop open at a time; each closed loop stamps its home chapter and trains the next.

## 5. Conventions for this track

- Lean 4 + current Mathlib, nothing exotic; every draft self-contained in one file.
- Every proof block labeled: **DRAFT — NOT YET COMPILED** → *(reader build: pending)* → **machine-verified (reader build N)** with date and reporter.
- `sorry` is allowed in *open* drafts (it marks the frontier of the loop honestly) but a machine-verified stamp requires zero sorries and `#print axioms` free of sorryAx.
- Human proof and formal draft always cite each other's section numbers.
---
*Chapter status: 🌱 seeded (session 6). Warm-up 1 drafted, awaiting first reader build. This chapter is updated as every other chapter is written or rewritten — never one Lean chapter per math chapter.*
