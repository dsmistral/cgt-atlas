---
name: cgt-atlas-project
description: "The CGT Atlas book: 21 chapter masters + web editions + pattern registry + book basis. The complete durable state for rebuilding the book; all session history was deliberately purged at the great cleanup (2026-10-26). Repo: dsmistral/cgt-atlas."
display_name: "CGT Atlas — The Book"
icon: 📕
---

# CGT Atlas — The Book

**What this topic holds** — the complete durable state of *The Combinatorics & Graph Theory Atlas*, a 21-chapter lecture-course textbook, reorganized for study on 2026-10-26:

- **`cgt-ch1-counting.md` … `cgt-ch21-engines.md`** — the 21 chapter masters (the source of truth).
- **`cgt-ch1-web.html` … `cgt-ch21-web.html`** — the 21 pre-rendered, script-free web editions.
- **`cgt-pattern-map.html`** — the pattern registry (canonical names, all aliases, machine-readable JSON payload; P-IDs are immutable join keys).
- **`cgt-lean-track.md`** — the unnumbered Lean Formal Track companion.
- **`bookkeeping/`** — everything that is NOT study content: **`cgt-book-basis.md`** (START HERE — what the book is, the chapter map, the Master Pattern Index P1–P45, the editorial/verification conventions, the sources, the rebuild protocol), **`cgt-publishing.md`** (the publishing/pipeline toolkit), **`cgt-render-engine.md`** (the canonical renderMd engine master), and **`rev-ch01.md` … `rev-ch21.md`** — each chapter's individual Revision History & Verification Notes log, extracted verbatim from its master at the reorganization.

**Content rule (standing).** The chapter masters, the web editions, the pattern map, and the Lean track carry ONLY what is relevant for study — mathematics, labs, exercises, receipts. No session logs, no book-building records, no pipeline prose. All logs, provenance, and build methodology live under `bookkeeping/`, with one individual log per chapter.

**The gathered sources live in the repo** (`papers/`): `SOURCES.md` (the source list), 208 per-paper notes (`A1–Y7`: one note per paper — claim, proof idea, pattern read), `CORPUS.md`/`ANALYSIS.md`, the teaching/contest censuses, and `patterns/` (the per-pattern dossier census, including `candidates/`). The classic-text sources of truth are named in the book basis.

**Repo is MAIN (standing rule).** `dsmistral/cgt-atlas` is the master of record. At every resume: check the repo first (directory listing + commit head) and treat any local mirror as secondary. If the local file layer becomes inaccessible, push any dangling changes, results, and logs to the repo and flag them in this file — the main resume point — so the next pass reads them here, syncs the repo-only extras down, and cleans up.

**Resume protocol (a new chat).** Read this file, then `bookkeeping/cgt-book-basis.md`; verify repo == local by a directory listing (names + sizes) before any work is planned. To extend a chapter: extend-never-rewrite on the master, machine-verify every claim before install (labs re-run exactly as printed), re-render the web edition through `bookkeeping/cgt-render-engine.md` (oracle-first: render the old payload byte-exact before rebuilding), and update the chapter's log `bookkeeping/rev-chNN.md`. For new book material, follow a book-building skill pipeline rather than rewriting wholesale.

**History note.** All session logs, the old master plan (atlas), the survey working records, the canvases, and the old repo (`cgt-atlas-backup`, including its full git history) were deliberately and unrecoverably deleted at the great cleanup, 2026-10-26, at the owner's direction. The chapters' revision logs survive under `bookkeeping/`; nothing else from the history does.
