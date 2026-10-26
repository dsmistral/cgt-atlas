---
name: cgt-atlas-project
description: "The CGT Atlas book: 21 chapter masters + web editions + pattern registry + book basis. The complete durable state for rebuilding the book; all session history was deliberately purged at the great cleanup (2026-10-26). Repo: dsmistral/cgt-atlas."
display_name: "CGT Atlas — The Book"
icon: 📕
---

# CGT Atlas — The Book (post-cleanup state)

**What this topic holds** — the complete durable state of *The Combinatorics & Graph Theory Atlas*, a 21-chapter lecture-course textbook:

- **`cgt-book-basis.md`** — START HERE. What the book is, the chapter map (Vols I–V), the Master Pattern Index P1–P45, the editorial/verification conventions, the build pipeline, the sources, and the rebuild protocol.
- **`cgt-ch1-counting.md` … `cgt-ch21-engines.md`** — the 21 chapter masters (the source of truth).
- **`cgt-ch1-web.html` … `cgt-ch21-web.html`** — the 21 pre-rendered, script-free web editions.
- **`cgt-pattern-map.html`** — the pattern registry (canonical names, all aliases, machine-readable JSON payload; P-IDs are immutable join keys).
- **`cgt-render-engine.md`** — the canonical `renderMd` engine master (how the HTML editions are built from the masters).
- **`cgt-publishing.md`** — the publishing/pipeline toolkit (export config + verification scripts + standalone lab code).
- **`cgt-lean-track.md`** — the unnumbered Lean Formal Track companion.

**The gathered sources live in the repo** (`papers/`): `SOURCES.md` (the source list), ~160 per-paper notes, `CORPUS.md`/`ANALYSIS.md`, the teaching/contest censuses, and the `patterns/` census. The classic-text sources of truth are named in the book basis.

**Repo (the self-sufficient resume point):** `dsmistral/cgt-atlas` — mirrors this folder plus `papers/` plus `youth-math-research-collection/` (a separate future-project idea kept in the same repo).

**Resume protocol (a new chat):** read this file, then `cgt-book-basis.md`; verify repo == local by a directory listing (names + sizes) if any work is planned. To extend a chapter: extend-never-rewrite on the master, machine-verify every claim before install (labs re-run exactly as printed), re-render the web edition through the engine (oracle-first: render the old payload byte-exact before rebuilding), keep the master's revision appendix current. For new book material, follow a book-building skill pipeline rather than rewriting wholesale.

**History note.** All session logs, the old master plan (atlas), the survey working records, the canvases, and the old repo (`cgt-atlas-backup`, including its full git history) were deliberately and irrecoverably deleted at the great cleanup, 2026-10-26, at the owner's direction — the chapters, the basis, the registry, and the sources above are the complete intended survivors. The chapters' own Revision History appendices remain (they are part of the books).
