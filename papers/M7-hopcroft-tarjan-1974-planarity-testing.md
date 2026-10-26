# M7 - Hopcroft-Tarjan: efficient planarity testing

- Metadata: John E. Hopcroft and Robert E. Tarjan, "Efficient planarity testing", J. ACM 21(4): 549-568 (1974). Verified via the Princeton research record, dblp, and the J. ACM text references; the conference-abstract priority noted ("Planarity testing in V log V steps", Proc. IFIP Cong. 1971). Seed title/venue/year CONFIRMED; vol(4)/pages pinned. A J. ACM errata note for the paper exists (referenced in the journal's own record) - verification hygiene: cite the corrected text.
- Abstract or faithful summary (summarized, flagged sketch): an efficient (linear-time) algorithm deciding whether an arbitrary graph can be embedded in the plane. Per the paper's own framing: "The algorithm may be viewed as an iterative version of a method originally proposed by Auslander and Parter" and correctly formulated in later work (the lineage statement verified via the open J. ACM text record). The method: a DFS phase orders the vertices, the graph is decomposed into a path system, and the embedding is built up by adding paths one at a time, testing for planarity conflicts.
- The decisive moves:
  1. [P18 flagship] the proof IS the procedure: correctness and the O(V) complexity bound are established by the algorithm's phases; the classic "proof = procedure" paper of the batch (expected by seed).
  2. [P25 partial, unplanned] the graph encoded into DFS/path structures - the path decomposition is what makes the iterative addition tractable; the paper's own framing places it as the iterative version of the Auslander-Parter method.
  3. [honest] no P8/P4 credit: the analysis is not extremal-object analysis, and the iteration is not an induction ladder in the Atlas sense.
- New-pattern candidates: none.
- Full text: not fetched (open records located - scope rule unused; the abstract + the paper's own lineage statement via the open record suffice at flagged sketch).
- Corrections log: none vs seed (title/venue/year confirmed); vol(4)/pages pinned; the IFIP 1971 extended-abstract priority noted; the errata-note existence recorded.
