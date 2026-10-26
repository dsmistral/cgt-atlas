# M5 - Alon-Shapira: every monotone graph property is testable

- Metadata: Noga Alon and Asaf Shapira, "Every monotone graph property is testable", SIAM J. Comput. 38(2): 505-522 (2008). Verified via the Princeton research record (Vol. 38, No. 2, 2008) and the M6 bibliography (SIAM J. Comput. 38 (2008), pp. 505-522); the STOC 2005 preliminary version recorded per citing bibliographies. Title/venue/year CONFIRMED as seeded; vol(2)/pages pinned.
- Abstract or faithful summary (summarized, flagged sketch): every monotone graph property can be tested with one-sided error by a randomized algorithm making a constant number of queries (the constant depending only on epsilon and the property). The proof: monotone properties are characterized by a finite set of "forbidden" colored reduced graphs; the tester samples an equipartition, estimates densities, and decides by checking the reduced coloring against the finite forbidden set - the (colored) regularity lemma carries the whole argument (per the paper's own framing and the survey literature).
- The decisive moves:
  1. [P30 genuine - seed expected] the testing framework is regularity-powered end to end: the finite approximation of the property goes through the regularity lemma's reduced graphs.
  2. [P18 genuine] the randomized tester IS the procedure; the theorem is the algorithm's correctness with a constant query bound.
  3. [P25 partial] the property reduced to a finite set of forbidden colorings of reduced graphs - the finite encoding is what makes constant-query testing possible.
- New-pattern candidates: none.
- Full text: not fetched; the circulating author/preliminary PDF located - scope rule unused; abstract + bibliographic records suffice at flagged sketch.
- Corrections log: none vs seed (title/venue/year confirmed); vol(2)/pages pinned (38(2): 505-522); the STOC 2005 preliminary-version priority noted.
