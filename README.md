# The Combinatorics & Graph Theory Atlas

A 21-chapter lecture-course textbook in combinatorics and graph theory, written Feynman-style: intuition and story before formalism, complete proofs inside the narrative, machine-verified computational labs, graded exercises with worked answers, and a Master Pattern Index (P1–P45) that organizes problems by *the move that solves them*.

## Layout

- **`cgt-atlas-project/`** — the book itself.
  - `cgt-ch1-counting.md` … `cgt-ch21-engines.md` — the 21 chapter masters (the source of truth).
  - `cgt-ch1-web.html` … `cgt-ch21-web.html` — the 21 pre-rendered, script-free web editions (print-ready).
  - `cgt-pattern-map.html` — the pattern registry (canonical names, aliases, machine-readable JSON).
  - `cgt-lean-track.md` — the Lean Formal Track companion.
  - `bookkeeping/` — the non-study layer: the book basis (start with `cgt-book-basis.md`), the publishing/pipeline toolkit, the canonical render engine, and `rev-ch01.md`…`rev-ch21.md` (each chapter's individual revision-history log).
- **`papers/`** — the mined primary literature the book was built from: `SOURCES.md`, 208 per-paper notes, the corpus and pattern analyses, the teaching and contest censuses, and the per-pattern dossier census (`patterns/`, incl. `candidates/`).
- **`youth-math-research-collection/`** — a separate future-project note, kept in this repo.

Chapters and their web editions contain study content only; every log and build record lives under `cgt-atlas-project/bookkeeping/`. To extend the book, start from `cgt-atlas-project/bookkeeping/cgt-book-basis.md`.
