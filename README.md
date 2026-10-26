# The Combinatorics & Graph Theory Atlas

A 21-chapter lecture-course textbook, rebuilt from scratch on a clean basis at the
great cleanup of 2026-10-26 (all prior repo history was deliberately purged; this
repo is the fresh start).

## Layout

- `cgt-atlas-project/` — the book itself:
  - `cgt-book-basis.md` — **start here**: what the book is, the chapter map
    (Vols I–V), the Master Pattern Index P1–P45, the editorial & verification
    conventions, the build pipeline, the sources, and the rebuild protocol.
  - `cgt-ch1-counting.md` … `cgt-ch21-engines.md` — the 21 chapter masters
    (source of truth; each carries its own Revision History appendix).
  - `cgt-ch1-web.html` … `cgt-ch21-web.html` — the 21 pre-rendered,
    script-free web editions.
  - `cgt-pattern-map.html` — the pattern registry (canonical names, all
    aliases, machine-readable JSON payload; P-IDs are immutable join keys).
  - `cgt-ch1-web.md` — the canonical `renderMd` engine master (how the HTML
    editions are built from the masters).
  - `cgt-publishing.md` — the publishing/pipeline toolkit.
  - `cgt-lean-track.md` — the unnumbered Lean Formal Track companion.
  - `KNOWLEDGE.md` — the minimal entrypoint / resume protocol.
- `papers/` — the gathered sources the book was built from: `SOURCES.md` (the
  source list), per-paper notes, `CORPUS.md` / `ANALYSIS.md`, the teaching and
  contest censuses, and the `patterns/` census.
- `youth-math-research-collection/` — a separate future-project idea kept in
  the same repo.

## Conventions

Masters are extended, never rewritten wholesale; every mathematical claim is
machine-verified before it is installed (labs re-run exactly as printed); web
editions are re-rendered through the engine master, oracle-first (the old
payload must render byte-exact before the new one is built); exports carry no
appendices; TeX is plain-Unicode in prose. To rebuild or extend the book,
follow `cgt-atlas-project/cgt-book-basis.md`.
