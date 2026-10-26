---
name: "cgt-publishing"
title: "The Atlas Publishing & Pipeline Toolkit"
type: "text/markdown"
---

# 🛠️ The Atlas Publishing & Pipeline Toolkit

*All document-generation work for the Atlas lives here — the export fix, the two-stage post-export test, and standalone runnable copies of chapter lab code — so the mathematics chapters stay mathematics. Created session 17, on the seventh external review of Chapter 1's recommendation.*

**The one-paragraph summary.** Nine external inspections have confirmed that the PDF export pipeline flattens the indentation of Python code blocks (measured: a loop body at 73.35 pt printed LEFT of its header at 78.75 pt; the reflection lab split across pages 9–10; in the seventh review the same damage to a verification script printed on pages 14–15; the eighth report re-measures the identical page-9 positions — `def D_rec(n):` and `D.append(...)` at 73.35 pt, `for i in range(2, n + 1):` at 78.75 pt — and the reflection block remains split). The tenth report (session 20), machine-checked against a second attached PDF of the same edition, adds a new detail: `D.append(...)` now extracts at 73.35 pt **plus one leading space** — the platform's own exports are not even consistent with each other, which confirms the damage happens inside the export pipeline per run, never in the stored source. The chapter sources are byte-audited clean — plain 0x20 indentation, leading-space census {0, 4, 8, 12, 15}, labs 100% ASCII after em-dash normalization — so the defect is the pipeline's, and the repair belongs here, not in the chapters. The web edition (§6) is now the **standard delivery format** for every chapter (session 21): Chapters 1–5 have theirs; rewrites and new chapters ship with one.

---

## 1 · The export fix (apply once, across all chapters)

**The eighth report's key insight makes the diagnosis two-layer: CSS alone cannot recover leading spaces that an earlier processing stage already discarded from the code text.** So repair — and test — in this order:

**Layer A — the text layer (check first).** The exported HTML's `<pre>` text must still *contain* the leading spaces of every code line. If a markdown-to-HTML converter, template, or minifier strips them upstream, no CSS can bring them back. The HTML gate (§2) localizes this without guesswork: run it on the exported HTML — **if it FAILs, the damage is in the text layer** (fix the exporter's code-text handling; do not touch CSS). This is machine-verified: a lab block with all leading spaces stripped fails the gate with exactly two flags (*a for-body sits left of its header*; *D.append sits left of its enclosing for*), while the intact block passes clean. **If the HTML gate PASSes but the PDF gate (§3) FAILs, the damage is in the rendering layer** — go to Layer B.

**Layer A damage is now evidenced, not hypothetical (session 19 — the PDF itself was attached and machine-analyzed in-sandbox):** the extracted text of the attached PDF's page 9 shows the deep indentation levels entirely absent (leading-space census {0, 4} where the source lab has {0, 4, 8} — and the reflection lab's 12/15 levels likewise gone), the gate logic flags it three times, a simulation of Python's block rule raises exactly the two IndentationErrors an interpreter would (both `for` headers), and the text content is identical modulo whitespace — the characters survived; only the nesting was destroyed. (Caveat, recorded honestly: OCR extraction can normalize whitespace itself; but the position measurements across five reports and the reviewer's independent extraction-then-compile failure agree with the transcript.) **Conclusion: an upstream stage discards the indentation before rendering — CSS alone cannot repair this export; the exporter's text handling must keep the leading spaces.**

**Layer B — the rendering layer.** The CSS, as supplied by the eighth report:

```css
pre {
    white-space: pre;
    tab-size: 4;
    break-inside: avoid;
    page-break-inside: avoid;
}
```

(`white-space: pre`: the source's own line breaks and leading spaces render verbatim — no re-flow, no re-indent, no wrapping. `break-inside: avoid` + `page-break-inside: avoid`: no page break may cut a block in half — the same protection the vector figures already carry in-image. `tab-size: 4` is defensive only: the Atlas sources are byte-audited 0x20-only, no tabs.)

After each export, run both gates (§2 and §3). **The document build fails if either gate fails.**

## 2 · Stage 1 — the HTML gate: `postexport_selftest.py`

*Checks the exported HTML: extracts every `<pre>` block containing Python and verifies the code's structure survived (loop bodies strictly right of their headers, the measured `D.append` defect specifically hunted, and every block still compiles). No dependencies; Python 3 only.*

**Status: logic machine-verified** — in a TypeScript port it passes on both Chapter 1 lab blocks as stored and catches a deliberately dedented block. Run: `python3 postexport_selftest.py <exported-file.html>`

```python
#!/usr/bin/env python3
"""postexport_selftest.py -- close the loop on the PDF export pipeline.

Usage:   python3 postexport_selftest.py <exported-file.html>

Extracts every <pre> block containing Python from the exported chapter and
checks that the export preserved the code's structure. A pipeline that
re-indents code (the defect six inspections have measured in the PDF)
fails here before any reader ever sees it. No dependencies; Python 3 only.
"""
import sys
from html.parser import HTMLParser


class CodeGrabber(HTMLParser):
    """Collects the text of every <pre>...</pre> block."""

    def __init__(self):
        super().__init__()
        self.stack, self.blocks = [], []

    def handle_starttag(self, tag, attrs):
        if tag == "pre":
            self.stack.append([])

    def handle_endtag(self, tag):
        if tag == "pre" and self.stack:
            text = "".join(self.stack.pop())
            (self.blocks if not self.stack else self.stack[-1]).append(text)

    def handle_data(self, data):
        if self.stack:
            self.stack[-1].append(data)


def width(line):
    """Leading-space count (a tab would already be a defect)."""
    return len(line) - len(line.lstrip(" "))


def check(code, index):
    lines = code.splitlines()
    problems = []
    for i, line in enumerate(lines):
        s = line.strip()
        if s.startswith("for ") and s.endswith(":"):
            for j in range(i + 1, len(lines)):       # first body line
                body = lines[j].strip()
                if not body or body.startswith("#"):
                    continue
                if width(lines[j]) <= width(line):
                    problems.append(f"block {index}, line {j+1}: a for-body "
                                    f"sits left of (or level with) its header")
                break
        if "D.append" in line:                      # the measured defect
            heads = [h for h in range(i)
                     if lines[h].strip().startswith("for "")]
            if heads and width(line) <= width(lines[heads[-1]]):
                problems.append(f"block {index}, line {i+1}: D.append sits "
                                f"left of its enclosing for -- the PDF defect")
    try:
        compile(code, f"<pre block {index}>", "exec")
    except SyntaxError as exc:
        problems.append(f"block {index}: does not even compile: {exc}")
    return problems


def main(path):
    grabber = CodeGrabber()
    with open(path, encoding="utf-8") as fh:
        grabber.feed(fh.read())
    blocks = [b for b in grabber.blocks if "def " in b]
    if not blocks:
        print("FAIL: no <pre> blocks containing Python were found")
        return 1
    problems = [p for i, b in enumerate(blocks, 1) for p in check(b, i)]
    if problems:
        print("FAIL -- the export damaged the code:")
        for p in problems:
            print("  " + p)
        return 1
    print(f"PASS -- {len(blocks)} code block(s) survived the export intact")
    return 0


if __name__ == "__main__":
    sys.exit(main(sys.argv[1]))
```

## 3 · Stage 2 — the PDF gate: `pdf_stage_test.py` *(new, drafted per the seventh review)*

*The seventh review's correct criticism of Stage 1: an HTML gate can pass while the PDF remains broken — the problematic deliverable is the PDF itself. This gate tests the final PDF. It executes the original sources as ground truth, extracts every monospace line of the PDF **with its x-position**, reconstructs each line's indentation from the geometry, requires every original file to appear line-for-line indent-identical, and executes the extraction. Any mismatch fails the document build.*

**Status: drafted, reader-run — logic machine-verified via a TypeScript port.** The port (locate → reconstruct → compare → split-check) passes a synthetic clean render (spaces rendered as exact x-positions, indents 0/4/4/8/4 recovered exactly), passes a render whose leading spaces survived as literal text, passes a clean block embedded in monospace noise, and **fails the measured-defect render** — def/`D = [1, 0]`/`D.append` at 73.35 pt with `for` at 78.75 pt reports precisely: *line 2: PDF indent 0, expected 4; line 3: PDF indent 1, expected 4; line 4: PDF indent 0, expected 8*. A dropped line reports *not found intact*, and the **page-split check (added session 19)** fails a block cut across pages 9–10 — exactly the reflection lab's situation in the attached PDF — and a three-page spill, while whole blocks pass. The gate's underlying logic was also validated against the **real attached PDF** (session 19): applied to the extracted page-9 text it flags 3 problems, the extraction's indent census is {0, 4} against the source's {0, 4, 8}, a simulation of Python's block rule raises exactly the two IndentationErrors an interpreter would, and the content is identical modulo whitespace. The authoring sandbox executes no Python, so the PyMuPDF extraction layer itself is verification level 4: *not claimed verified until a reader reports a real run.* Requires PyMuPDF (`pip install pymupdf`).

```python
#!/usr/bin/env python3
"""pdf_stage_test.py -- the PDF gate of the Atlas publish test.

Usage:  python3 pdf_stage_test.py <exported-file.pdf> <original1.py> [<original2.py> ...]

The HTML gate (postexport_selftest.py) checks the exported HTML; this script
checks the FINAL PDF, because an HTML gate can pass while the PDF is broken
-- the failure mode six external inspections have now measured in exported
Atlas PDFs (a loop body printed LEFT of its header: 73.35 pt vs 78.75 pt).

The three acceptance tests (per the ninth external report) -- the publish
fix is accepted only when ALL THREE pass on the final PDF:
  T1. The Python extracted from the final PDF compiles and runs.
  T2. All indentation levels match the original source.
  T3. No executable code block is split across pages.

Per original source file:
  1. GROUND TRUTH: compile and execute it; capture stdout.
  2. LOCATE: find its significant lines (blanks ignored) as a contiguous run
     of the PDF's monospace-line stream, matching stripped text first.
  3. RECONSTRUCT: rebuild each line's leading spaces from geometry --
     indent = round((x_origin - run_left_margin) / char_width), with
     char_width measured from the PDF's own spans. Literal leading spaces
     that survived into the text are honored instead.
  4. COMPARE (T2): every line's reconstructed indent must equal the
     original's. A re-indented OR wrapped (re-flowed) line fails here, by
     design.
  5. SPLIT (T3): every line of the located run must sit on ONE page -- a
     block cut by a page break fails, naming the pages.
  6. EXECUTE (T1): compile and run the reconstructed code; it must run
     clean and match the ground-truth output.
Any failure fails the document build (exit 1).

Honest limits, stated not hidden: blank lines inside the originals are not
reconstructed (the Atlas labs have none inside strings); a wrapped line is a
FAILURE, not a pass -- code must not re-flow; the monospace font-name list
may need one edit to match your exporter's code font (see MONO_MARKERS).

Requires: pip install pymupdf      (imports as fitz)
"""
import statistics
import subprocess
import sys
from pathlib import Path

try:
    import fitz  # PyMuPDF
except ImportError:
    sys.exit("PyMuPDF is required:  pip install pymupdf")

# Edit this to match the exporter's code font if extraction finds nothing.
MONO_MARKERS = ("Mono", "mono", "Consol", "Courier", "Menlo", "LucidaConsole")


def mono_lines(pdf_path):
    """Every all-monospace line of the PDF, in reading order.

    Yields (text, x0, char_w, page). Prose lines and mixed prose/code lines
    are skipped, so inline code inside sentences cannot pollute the stream.
    """
    out = []
    with fitz.open(pdf_path) as doc:
        for pno, page in enumerate(doc, 1):
            for block in page.get_text("dict")["blocks"]:
                for line in block.get("lines", []):
                    spans = line["spans"]
                    if not spans:
                        continue
                    if not all(any(m in s["font"] for m in MONO_MARKERS)
                               for s in spans):
                        continue
                    text = "".join(s["text"] for s in spans)
                    s0 = spans[0]
                    x0 = s0["origin"][0] if "origin" in s0 else s0["bbox"][0]
                    char_w = ((s0["bbox"][2] - s0["bbox"][0])
                              / max(len(s0["text"]), 1))
                    out.append((text, x0, char_w, pno))
    if not out:
        sys.exit("FAIL: no monospace lines found in the PDF -- edit "
                 "MONO_MARKERS to match the exporter's code font")
    return out


def leading(line):
    return len(line) - len(line.lstrip(" "))


def check_original(path, stream):
    code = Path(path).read_text(encoding="utf-8")
    compile(code, path, "exec")                 # refuse broken originals
    run = subprocess.run([sys.executable, str(path)],
                         capture_output=True, text=True, timeout=120)
    if run.returncode != 0:
        sys.exit(f"FAIL: the original {path} does not execute:\n{run.stderr}")
    truth = run.stdout

    sig = [l for l in code.splitlines() if l.strip()]   # significant lines
    stripped = [l.strip() for l in sig]
    hay = [t.strip() for t, _, _, _ in stream]
    start = next((i for i in range(len(hay) - len(sig) + 1)
                  if hay[i:i + len(sig)] == stripped), None)
    if start is None:
        return [f"{path}: not found intact in the PDF -- lines missing, "
                f"re-flowed (wrapped), or text-damaged"]

    region = stream[start:start + len(sig)]
    pages = sorted({p for _, _, _, p in region})
    if len(pages) > 1:                        # acceptance test T3
        return [f"{path}: the code block is SPLIT across pages "
                f"{pages[0]}-{pages[-1]} -- a page break cut it in half"]
    left = min(x0 for _, x0, _, _ in region)
    char_w = statistics.median(w for _, _, w, _ in region if w > 0)
    problems, rebuilt = [], []
    for k, ((text, x0, _, _), orig) in enumerate(zip(region, sig)):
        if text.startswith(" "):               # spaces survived in the text
            ext, ext_indent = text, leading(text)
        else:                                  # spaces became position only
            ext_indent = round((x0 - left) / char_w)
            ext = " " * ext_indent + text.strip()
        rebuilt.append(ext)
        if ext_indent != leading(orig):
            problems.append(f"{path}: line {k+1} ({orig.strip()[:40]}...): "
                            f"PDF indent {ext_indent}, expected "
                            f"{leading(orig)} (x-origin {x0:.2f} pt vs run "
                            f"left margin {left:.2f} pt, char width "
                            f"{char_w:.2f} pt)")
    if problems:
        return problems

    extracted = "\n".join(rebuilt) + "\n"
    try:
        compile(extracted, f"<extracted from PDF: {path}>", "exec")
    except SyntaxError as exc:
        return [f"{path}: extracted code does not compile: {exc}"]
    run = subprocess.run([sys.executable, "-c", extracted],
                         capture_output=True, text=True, timeout=120)
    if run.returncode != 0:
        return [f"{path}: extracted code fails at run time:\n{run.stderr}"]
    if run.stdout != truth:
        return [f"{path}: extracted code output differs from the original"]
    return []


def main():
    if len(sys.argv) < 3:
        sys.exit(__doc__)
    pdf_path, originals = sys.argv[1], sys.argv[2:]
    stream = mono_lines(pdf_path)
    problems = [p for o in originals for p in check_original(o, stream)]
    if problems:
        print("FAIL -- the PDF damaged the code; the build is not clean:")
        for p in problems:
            print("  " + p)
        return 1
    print(f"PASS -- {len(originals)} source file(s) survived the PDF export "
          f"intact, indent-identical, and executable")
    return 0


if __name__ == "__main__":
    sys.exit(main())
```

## 4 · Standalone lab distribution — Chapter 1

*Per the seventh review: usable code must not depend on the document renderer. Save each block below as its own file and run it directly — this is the same code as in the chapter, byte-identical, and the chapter remains authoritative: any future change propagates to both places.*

**`lab1_derangement_engines.py`** — both derangement engines + the Catalan recurrence, cross-checked by execution (verified 2026-10-09: D_n for n = 2..9 = 1, 2, 9, 44, 265, 1854, 14833, 133496, both engines agreeing; D₉/9! ≈ 1/e; Catalan n = 0..10 = 1, 1, 2, 5, 14, 42, 132, 429, 1430, 4862, 16796, recurrence matching the closed form):

```python
from math import comb, factorial

def D_rec(n):                       # recurrence engine (Lecture 1.2)
    D = [1, 0]
    for i in range(2, n + 1):
        D.append((i - 1) * (D[i-1] + D[i-2]))
    return D[n]

def D_ie(n):                        # inclusion-exclusion engine (Lecture 1.1)
    return sum((-1)**k * comb(n, k) * factorial(n - k) for k in range(n + 1))

def C_rec(n):                       # Catalan first-return recurrence (Lecture 2.2)
    C = [1]
    for i in range(1, n + 1):
        C.append(sum(C[k] * C[i-1-k] for k in range(i)))
    return C[n]

assert all(D_rec(n) == D_ie(n) for n in range(2, 10))
assert C_rec(10) == comb(20, 10) // 11
```

**`lab2_reflection_bijection.py`** — the reflection bijection and its inverse, round-tripped over all small paths (verified 2026-10-10: n = 2 — 4 bad paths, 4 distinct images, all paths to (3,1) covered, both round trips exact; n = 3 — 15 bad paths, 15 images, all 15 paths to (4,2) covered, both round trips exact; and `forward('EEEN')` returns None — the alarm proving the inverse must search for x = y+1):

```python
from itertools import permutations

def all_paths(a, b):
    return {''.join(p) for p in permutations('E'*a + 'N'*b)}

def forward(p):    # bad path to (n,n): swap head at first touch of y = x+1
    x = y = 0
    for k, s in enumerate(p):
        x += (s == 'E'); y += (s == 'N')
        if y == x + 1:
            return p[:k+1].translate(str.maketrans('EN','NE')) + p[k+1:]
    return None                      # no touch: map undefined -- bug alarm

def inverse(p):    # any path to (n+1, n-1): swap head at first touch of x = y+1
    x = y = 0
    for k, s in enumerate(p):
        x += (s == 'E'); y += (s == 'N')
        if x == y + 1:
            return p[:k+1].translate(str.maketrans('EN','NE')) + p[k+1:]
    return None

for n in (2, 3):
    bads = [p for p in all_paths(n, n) if forward(p) is not None]
    images = [forward(p) for p in bads]
    assert set(images) == all_paths(n+1, n-1)           # bijection, both sides
    assert all(inverse(forward(p)) == p for p in bads)  # round trip, bad side
    assert all(forward(inverse(q)) == q
               for q in all_paths(n+1, n-1))            # round trip, mirror side

assert forward('EEEN') is None   # the WRONG inverse hunts y = x+1 here: nothing to find
```

## 5 · The publish checklist (run after any pipeline change)

1. Run the HTML gate on a current export *before* changing anything — it tells you which layer is broken: FAIL ⇒ text layer (leading spaces already discarded upstream; fix the exporter's code-text handling first — CSS cannot help), PASS ⇒ rendering layer.
2. Apply the fix for the layer it named: Layer A in §1 for the text, Layer B (the CSS block in §1) for the rendering.
3. Export Chapter 1 to HTML → run the HTML gate: `python3 postexport_selftest.py chapter1.html` — must print PASS.
4. Export to PDF → run the PDF gate: `python3 pdf_stage_test.py chapter1.pdf lab1_derangement_engines.py lab2_reflection_bijection.py` — must print PASS, indent-identical and executable.
5. Only then apply the fix across all chapters and re-export; the two gates travel with the pipeline from now on.
6. The reader-side definitive test is unchanged: the labs run on a Raspberry Pi in under a second, and the recorded outputs are the reference.

**Definition of done — the ninth report's three acceptance tests (adopted verbatim, session 19).** The publishing fix is accepted only when, on the final regenerated PDF: **T1** the Python extracted from the PDF compiles and runs; **T2** all indentation levels match the original source; **T3** no executable code block is split across pages. The PDF gate enforces all three (T1 = the execute step, T2 = the indent compare, T3 = the page-split check added session 19 — a gap the report's third criterion exposed: the reflection lab really is cut across pages 9–10 in the attached PDF). In its simplest form, as the tenth report restates it: **both published Python labs compile and run after extraction from the final PDF, and their code blocks remain on single pages.**

## 6 · The web edition — the standard delivery format for every chapter (built session 20; standard adopted session 21, on the user's direction)

*The tenth report asked for the original HTML and the actual PDF-generation script, so the cause could be diagnosed directly. Recorded honestly: no export or generation tool exists in the workspace — the PDF export is the platform's own feature, and its script cannot be obtained from here. The pipeline fix in §1 is therefore written for whoever repairs the platform exporter. Until then, the web edition is the working route — and, per the user's session-21 direction, the standard delivery format: every chapter ships one, rewrites and new chapters at delivery time. Chapters 1–5 have theirs.*

**What it is.** Per chapter, a standalone HTML page ("Chapter N — Web Edition") that embeds the chapter source **byte-identically** — as a base64 payload, chosen because the canvas HTML format forbids raw markdown fences in the page; the decode is byte-exact — and renders it locally with the correct styling already applied: `white-space: pre` and `break-inside: avoid` on every code block, A4 `@page` print rules, SVG figures inline. No network, no external scripts, nothing between the source and the page. The builder is one template head (per-chapter name/title/banner) + the verified renderer tail; the markdown canvas remains the authoritative source and the web edition is a derived export artifact.

**The rebuild rule (adopted session 21, learned the hard way).** A chapter edit invalidates its web edition: **rebuild and re-verify byte-exact on every source change** — a stale embed is a defect. The session-21 harness caught exactly this on Chapter 1 (its appendix count-updates postdated the session-20 build) and it was rebuilt from the current source (61,727 bytes, embed re-verified).

**How to use it.** Open the web edition → Ctrl/Cmd + P → *Save as PDF*. Both layers the toolkit diagnoses are handled by construction: the text layer is the embedded byte-identical source, and the rendering layer is the page's own CSS. The printed PDF keeps the code's exact indentation and does not split code blocks across pages. Then certify with the PDF gate (§3) — or, per the tenth report's simple acceptance test, extract each lab from the printed PDF and compile it.

**Machine verification (session 20, the original build; session 21, the standardization).** The renderer is machine-verified via a TypeScript port run on the full chapter: the base64 payload decodes byte-exactly to the chapter source; all 8 fenced blocks render — the 5 `<pre>` blocks decode back byte-identical to the source (both labs included, deep-indent census preserved) and the 3 SVG figures pass through unescaped; the fence detector (constructed without literal backticks) is verified equivalent to the literal fence test on a 601-line corpus; every construct class renders (headings, rules, blockquote, table with separator row dropped, ordered and unordered lists, paragraphs); the known stray-asterisk line stays literal. Session 21 standardized the builder and ran it for **Ch. 2 (2 labs), Ch. 3 (2 labs), Ch. 4 (1 lab)** — each embed verified twice (encode→decode round-trip, and extract-from-canvas decode-diff), after a construct survey of each chapter (no links, no raw HTML outside fences, no indented-code lines, no exotic list markers) — and re-ran the harness over all four web editions in a single pass: embeds byte-exact against the **current** sources, every `<pre>` block entity-decodes back byte-identical, no unrendered fences. What was once **not** claimed is now certified: the browser print itself — **verification level 4, achieved session 22.** The first external review of Chapter 2 was conducted on a PDF the reader printed from the Chapter 2 web edition: both labs extracted from the printed PDF compile and run, every recorded count matches (1858/1858, 576/576, 30 at m = 11, 1990 at δ = 2 — each independently re-verified in-sandbox during the same audit), the code indentation is preserved, and no lab block is split across pages — the acceptance tests T1–T3 pass on the web-edition route, reader-run. The platform's own PDF export remains unrepaired; the web edition is the certified route around it. Session 23 built the **Ch. 5 web edition** (shipped with its rewrite) and rebuilt **Ch. 2's** (Joyal §4.5 + the four figures), both verified the standard way: payload byte-identical twice over, every code block entity-decodes byte-identical, the 4 new SVG figures pass through raw, zero unrendered fences — and the harness pass found and repaired a legacy defect in **all five** web editions: the `<title>` lines of the Ch. 1–4 pages (built session 21) carried malformed non-ASCII bytes; all five titles are now pure-ASCII HTML entities (`&middot;`, `&#8212;`, `&amp;`), payloads untouched.

*Status: toolkit created session 17; eighth report incorporated session 18 (two-layer diagnosis + exporter CSS); ninth report incorporated session 19 (PDF attached and machine-analyzed in-sandbox — Layer A text damage evidenced: census {0,4} vs {0,4,8}, 3 gate flags, 2 simulated IndentationErrors, content identical modulo whitespace; page-split check added to the PDF gate and machine-verified; the three acceptance tests T1/T2/T3 adopted as the definition of done). HTML gate machine-verified (TS port), including against the real attached PDF's extracted text; PDF gate drafted, its locate/reconstruct/compare/split logic machine-verified via a TS port, the PyMuPDF extraction layer awaiting a reader's run report; both labs distributed standalone, byte-identical to the chapter (verified by diff). Tenth report incorporated session 20: second attached PDF, same edition, same defect — with a new measurement (`D.append` at 73.35 pt + one leading space), so the platform's own exports are mutually inconsistent; no export or generation tool exists in the workspace (the export is the platform's feature — honest blocker), so the Chapter 1 web edition was built as the working export route (§6): byte-identical base64 embedding diff-verified, renderer machine-verified on the full chapter, browser print awaiting a reader's run. Session 21: the web edition adopted as the standard delivery format (user direction); Ch. 2–4 web editions built and verified (each embed byte-exact twice; all four pass the harness in one pass); Ch. 1's web edition caught stale by the harness and rebuilt from the current source; the rebuild rule adopted (rebuild + re-verify on every chapter edit). Session 22: **the web-edition route certified reader-side (level 4)** — the Ch. 2 external review audited a PDF printed from the Ch. 2 web edition: labs extracted from the printed PDF compile and run with all counts matching, indentation preserved, no split blocks (T1–T3 pass); Ch. 2's web edition rebuilt after the review's error fixes, per the rebuild rule. Session 23: Ch. 5's web edition built with its Feynman rewrite; Ch. 2's rebuilt again (Joyal §4.5 + the four vector figures), both byte-exact through the full harness; the legacy `<title>` defect (malformed bytes in the Ch. 1–4 pages, inherited from the session-21 build) found and repaired — all five titles now pure-ASCII HTML entities, payloads untouched. Session 24: Ch. 2's web edition rebuilt again after the backlog pass (Lecture 7, §6.4, exercises 12–14/18/22, lab Parts 3–4) — payload byte-exact through the harness plus an independent GNU-base64 md5 cross-check against the chapter source, and the verified renderer re-run on the new source (4 `<pre>` blocks entity-decode byte-identical, 5 SVG figures pass raw, no unrendered fences, the chapter's first in-answer table renders). Chapter 1's mathematical revision cycle is closed — remaining work on this file is pipeline work, not chapter work.*
## 7 · The session-78 export-hygiene + light-set changes (user-directed)

**The light durable set.** The durable master copy now keeps only: KNOWLEDGE.md, this toolkit, the atlas, the seventeen chapter masters, the sixteen .html exports, and ONE web frame — `cgt-ch1-web.md`, the canonical renderMd v2 frame/engine master (the session-77 canary). The fifteen per-chapter web editions were retired: every frame's payload was its chapter master, and the v2 engine is byte-identical (md5 d5eaa031…) across all sixteen, so nothing unique was lost; the GitHub history retains every retired frame.

**The export-hygiene rule.** The .html exports ship clean — no export banner, no Revision History & Verification Notes appendix, no chapter-status footer; the development record lives in the chapter canvas only. All sixteen were cleaned in place at session 78 under machine gates (zero banner/appendix/status strings; line 38 = `<main id="content">`; tail = `</main></body></html>`; mojibake 0; 16/16 PASS; the head and print CSS untouched).

**The standing rebake route (from session 78 on).** Chapter master → render with the canonical frame's renderMd v2 engine (evaluated verbatim, never re-implemented) → bake into the standard head/tail shell → strip the banner, the appendix, and the status footer → run the hygiene gates. The §6 rebuild rule now applies to the .html export; there is no per-chapter web edition to rebuild.

**Print note.** The removed banner carried the print-to-PDF instructions; the `@page` and `@media print` CSS is unchanged, so browser print-to-PDF behaves exactly as before — the instructions now live here instead of in every export.
