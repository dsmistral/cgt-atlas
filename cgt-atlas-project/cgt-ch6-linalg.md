---
name: "cgt-ch6-linalg"
title: "Ch. 6 — Linear-Algebraic Methods: A Lecture Course in the Feynman Style"
type: "text/markdown"
---

# Chapter 6 · Linear-Algebraic Methods

*Part of the Combinatorics & Graph Theory Atlas (see the Atlas canvas for the chapter map and progress report).*

The great discovery of 20th-century combinatorics: many counting bounds are secretly **dimension bounds**. Encode sets as vectors, and "you can't have too many" becomes "vectors can't exceed the dimension of the space". This edition is a lecture course in four lectures — Fisher's inequality two ways, Oddtown and Eventown (where the field chooses the answer), the polynomial method, and the friendship theorem — every proof complete, every claimed number machine-checked. The polynomial method — a one-line proof of Oddtown's descendants and the engine behind the best known Ramsey lower bounds — gets a full lecture of its own, and returns in Chapter 8, running on the Hamming cube. The eigenvalue half of the subject — eigenvalues as averaging machines, spectral Turán, two-distance sets, and the modern toolkit of interlacing, the Hoffman bounds, Lovász theta, and Delsarte's linear program — is the subject of Chapter 8, *Spectral Methods and the Modern Toolkit*; this chapter closes exactly where that one picks up.

## How to read this chapter

**Notation.** [n] = {1, …, n}; a family F = {A_1, …, A_m} of subsets has characteristic (0/1) column vectors v_i ∈ R^n (or F_p^n). G = (V, E) is a graph on n vertices with m edges, adjacency matrix A, eigenvalues λ1 ≥ … ≥ λn; d-regular means every degree d; J is the all-ones matrix, I the identity, 𝟙 the all-ones vector, and 𝟙⊥ the hyperplane of vectors with coordinate sum 0. ω is the clique number, α the independence number. C(a, b) is the binomial coefficient (with C(a, b) = 0 for b < 0 or b > a); F_p the field of integers mod p; ||x|| the Euclidean norm. Letters are re-stated locally where a lecture needs its own (m in particular is the number of sets in the intersection families of L1–L3).

**The exercises are graded:** ●○○ *easy* (a direct application of one lecture idea), ●●○ *moderate* (two ideas, or one tricky step), ●●● *tough* (several chapter ideas combined). Hints travel with the problems; worked answers sit at the very end of the chapter. Try honestly before reading a hint. Beyond the graded set, ◆ **pattern-unknown** problems name no method and carry no hint: diagnosing which tool fits is part of the problem. And ◐ **Explorations** at the end are open-ended investigations with no single right answer — research training, not test preparation.

## The pattern table for this chapter

| Pattern | Plain language | Where you meet it |
|---------|---------------|-------------------|
| **P19 Rank / dimension** | Build a matrix whose rank you can bound two ways; dimension is a counting bound in disguise | L1, L4; Ch. 8 (two-distance sets) |
| **P19′ Independence via dot products** | Self-products nonzero, cross-products zero — over the field the congruences name — forces linear independence | L2, L3 |
| **P22 Polynomial method** | One polynomial per set, vanishing on all the others; the dimension of a polynomial space caps the family | L1, L3; Ch. 8 (two-distance sets, Delsarte) |
| **P19/P22 face — slice rank** | The tensor-power face of the same dimension budget: slice-decompose a diagonal tensor and uniformly-bounded families stay exponentially small (Croot–Lev–Pach; Ellenberg–Gijswijt). One face, two entries: the engine is a P19 rank argument (the slices bound a dimension) AND a P22 polynomial argument (the slices are indexed by a vanishing polynomial's monomials) — the survey's census fired both patterns in the same proofs, so the face names both, no double credit | Ch. 14 L6 (the cap set theorem) |
| **P21 Spectral / Rayleigh** | Eigenvalues as averaging devices: Rayleigh lower bound, structure upper bound, operator norm on 𝟙⊥ | Ch. 8 (the spectral lectures) |
| **P20 Weight shifting / symmetrization** | Move weight toward the extremal configuration without losing the objective. Usage-evidence note: genuinely under-used in the field — the survey's classics reach for shifting (P23) or averaging (P10) when they symmetrize (Katona's circle method is P10 partial work) | Ch. 8 (Motzkin–Straus) |

---

## Lecture 1 · Fisher's Inequality, Two Ways

**Problem.** A_1, …, A_m are distinct subsets of an n-element set; every pair intersects in **exactly λ** points (λ ≥ 0); and no |A_i| equals λ. Then **m ≤ n**.

Two engines solve this, one getting m ≤ n + 1 and the other closing the last notch. They are worth learning as a pair: the first is the seed of the Frankl–Wilson theory (Lecture 3); the second is the Gram-matrix machine you will reuse all chapter.

### 1.1 Bose's polynomials — honest, and one short of the goal

To each set A_i associate the polynomial in n variables x_1, …, x_n (one per ground element):

p_i(x) = Σ_{k ∈ A_i} x_k − λ.

Evaluate at the 0/1 vectors v_j: p_i(v_j) = |A_i ∩ A_j| − λ. For i ≠ j that is λ − λ = 0; for i = j it is |A_i| − λ ≠ 0. So the **evaluation matrix** (p_i(v_j)) is diagonal with nonzero diagonal entries — invertible — and the p_i are linearly independent.

Where do they live? Each p_i is a linear combination of 1, x_1, …, x_n: a space of dimension n + 1. Independence forces

**m ≤ n + 1.**

One notch short — and honestly so: nothing in the argument uses that the coefficients of the x_k in p_i are all **1**. Machine check on the two classical tight examples: the Fano plane's evaluation matrix is 2I (each line has |A| − λ = 3 − 1 = 2 on the diagonal), determinant 2⁷ = 128; the 4-point near-pencil's is diag(2, 1, 1, 1), determinant 2.

### 1.2 The Gram matrix — positive definite, rank ≤ n, done

Take the characteristic vectors v_i ∈ R^n and the m×m matrix of dot products M = (v_i · v_j) = (|A_i ∩ A_j|):

M = λJ + D, where D = diag(|A_1| − λ, …, |A_m| − λ), with all diagonal entries d_i = |A_i| − λ > 0 (since for m = 1, m ≤ n is trivial when n ≥ 1, and for m ≥ 2, |A_i| ≥ |A_i ∩ A_j| = λ with |A_i| ≠ λ forces |A_i| > λ).

**Claim 1: M is positive definite.** For any x ≠ 0:
xᵀMx = λ(Σ_i x_i)² + Σ_i (|A_i| − λ)x_i².
The first term is ≥ 0 (since λ ≥ 0); the second is > 0 because |A_i| − λ > 0 and at least one coordinate satisfies x_i ≠ 0. So xᵀMx > 0: M is positive definite, and **rank M = m**.

**Claim 2: rank M ≤ n.** M = V Vᵀ where V stacks the row vectors v_iᵀ as rows (V is m×n), and rank(V Vᵀ) ≤ rank V ≤ n.

Combining: m = rank M ≤ n. ∎

✎ **Checkpoint — determinants, computed two ways.** For D = diag(d_1, …, d_m) with every d_i > 0, the **determinant lemma** states det(λJ + D) = det(D)·(1 + λ·Σ_i 1/d_i).
*Proof of the determinant lemma.* Since d_i > 0, D is invertible and λJ + D = D(I + λD⁻¹𝟙𝟙ᵀ). Here λD⁻¹𝟙𝟙ᵀ is a rank-1 matrix whose unique potentially nonzero eigenvalue is its trace, tr(λD⁻¹𝟙𝟙ᵀ) = λ𝟙ᵀD⁻¹𝟙 = λ·Σ_i 1/d_i, with the remaining m − 1 eigenvalues equal to 0. Adding I shifts the eigenvalues to 1 + λ·Σ_i 1/d_i (once) and 1 (m − 1 times), so det(I + λD⁻¹𝟙𝟙ᵀ) = 1 + λ·Σ_i 1/d_i, and multiplying by det(D) = Π_i d_i gives the formula. ∎
This lemma prices both tight examples with d_i = |A_i| − λ. Fano plane (seven 3-point lines on seven points, λ = 1, d_i = 2): det = 2⁷·(1 + 7/2) = 128·4.5 = **576** = 24². Near-pencil on 4 points (one 3-point line plus the three 2-point lines through the fourth point; D = diag(2,1,1,1)): det = 2·(1 + 1/2 + 1 + 1 + 1) = **9**. Both check against direct elimination; both families have m = n, so Fisher is tight. And Sylvester's criterion runs live on the Fano Gram: its leading principal minors are 3, 8, 20, 48, 112, 256, 576 — all positive, positive definiteness confirmed without writing a single quadratic form.

### 1.3 Corollary — de Bruijn–Erdős (P19 applied to geometry)

**n ≥ 3 non-collinear points determine at least n distinct lines.**
*Proof.* Let L be the set of lines determined by the n points, with |L| = N. For each point p, let A_p ⊆ L be the set of lines passing through p. Any two distinct points determine a unique line, so |A_p ∩ A_q| = 1 = λ for p ≠ q. Because the n points are not all collinear, no single line contains all n points: for each point p, picking a line ℓ ∈ A_p and a point r ∉ ℓ, the line pr is a second line in A_p, so |A_p| ≥ 2 ≠ λ. In particular, the sets A_p are distinct (if A_p = A_q, then |A_p ∩ A_q| = |A_p| ≥ 2, contradicting |A_p ∩ A_q| = 1). Applying Fisher's inequality to the n sets A_p ⊆ L gives n ≤ |L| = N. ∎

✎ **Checkpoint.** Enumerate the linear spaces on 4 labeled points (any two points on exactly one line, each line of size ≥ 2, not all 4 points collinear): there are exactly **5** — four near-pencils (choose the point off the 3-point line, giving 4 lines) and one affine plane (all six pairs as lines, giving 6 lines) — the affine plane AG(2, 2). The brute-force census is Exercise 15; every one of the five satisfies N ≥ n, as de Bruijn–Erdős demands.

**What you now own:** the evaluation-matrix reflex (a polynomial per set, vanishing on the others) and the Gram template — *dot-product pattern ⇒ positive definiteness ⇒ rank = m ⇒ m ≤ n* — a machine you can retarget at dozens of theorems (Exercises 5, 8, and 11; Chapter 8's two-distance lecture runs it in geometry).

---

## Lecture 2 · Oddtown and Eventown: The Field Chooses the Answer

**Problem (Oddtown).** A family of subsets of an n-set, each of **odd** size, with **even** pairwise intersections. Then the family has at most **n** members.

### 2.1 Independence over F_2 (P19′)

Take characteristic vectors v_i in the vector space **F_2ⁿ** — work mod 2, because the problem is stated in parities. Then
v_i · v_i = |A_i| ≡ 1 (odd), and v_i · v_j ≡ 0 (even) for i ≠ j.
Suppose Σ c_i v_i = 0 is a linear dependence. Dot with v_j: every cross term dies, and the only survivor is c_j·(v_j · v_j) = c_j. So c_j = 0 for all j: the v_i are linearly independent, and F_2ⁿ has only n independent vectors. ∎

The census confirms the bound is tight: on [3] the maximum Oddtown has 3 members, on [4] it has 4 (Exercise 1 — the four 3-subsets of [4] do it).

### 2.2 The twist — Eventown, and the field's revenge

If instead all sizes **and** all intersections are **even**, the family can have 2^{⌊n/2⌋} members: partition the ground set into pairs and take all unions of pairs. Every set has even size; every intersection is even. So flipping one parity changes the answer from linear to *exponential*. The rank argument explains why it **must** collapse:

**Eventown upper bound.** Over F₂, Eventown's vectors satisfy v_i · v_j = 0 for **all** i, j — including i = j, since every |A_i| is even. So the symmetric bilinear form (x, y) ↦ x · y vanishes on the entire span W = span_F₂{v_1, …, v_m} ⊆ F₂ⁿ: for x = Σ_i a_i v_i and y = Σ_j b_j v_j, x · y = Σ_{i,j} a_i b_j (v_i · v_j) = 0. Every vector of W is orthogonal to every vector of W, i.e. **W ⊆ W⊥**. Because the dot product on F₂ⁿ is nondegenerate, dim W + dim W⊥ = n, whence 2 dim W ≤ n and dim W ≤ ⌊n/2⌋. Distinct sets have distinct characteristic vectors inside W, so |F| ≤ |W| = 2^{dim W} ≤ 2^{⌊n/2⌋}. ∎ (Exercise 2; census: maximum 2 on [3], 4 on [4] — both matching the formula.)

### 2.3 The same trick over any prime

Nothing is special about 2. Fix a prime p and a residue k ≢ 0 (mod p): if every |A_i| ≡ k and every pairwise intersection ≡ 0 (mod p), the same dotting argument over F_p gives v_i·v_i = k ≠ 0 and v_i·v_j = 0 — independence again, so **m ≤ n for every prime**. Machine census for p = 3, k = 1 on [4]: maximum family size 4 = n, attained by the singletons. The lesson generalizes: the modulus is not decoration — it is the theorem (Exercise 6).

### 2.4 One more parity flip — symmetric differences

Suppose instead all pairwise **symmetric differences** are even: |A_i △ A_j| ≡ 0 (mod 2) for all i, j. Since |A △ B| = |A| + |B| − 2|A ∩ B| ≡ |A| + |B| (mod 2), every |A_i| has the **same parity** — so for n ≥ 1 the whole family sits inside one parity class of 2^{n−1} sets, and that is the sharp bound (Exercise 12; census: maximum 8 = 2³ on [4], attained by all the odd sets). Three parity conditions, three answers: n, 2^{⌊n/2⌋}, 2^{n−1}.

**What you now own:** the reflex of doing inner products over the field the *congruences* point to (P19′), and the habit of asking how the answer changes with the modulus — the contrast is usually the real theorem.

---

## Lecture 3 · Polynomials That Count: Ray-Chaudhuri–Wilson, Frankl–Wilson, and Ramsey Graphs

The evaluation-matrix idea of Lecture 1 was deliberately wasteful: the polynomials p_i = Σ_{k∈A_i}x_k − λ lived in a space of dimension n + 1, but we never asked what the *smallest* natural space is. This lecture asks, and the dividends are the strongest intersection theorems known — and, via a construction, quasipolynomial lower bounds for Ramsey numbers.

### 3.1 The multilinear lemma

On the cube {0,1}^n every function f : {0,1}^n → F (any field F) is given by a unique **multilinear** polynomial (each variable to degree ≤ 1): x_i² = x_i on {0, 1} kills higher powers, and the 2^n multilinear monomials x_S = Π_{i∈S} x_i (S ⊆ [n], with x_∅ = 1) are linearly independent as functions — evaluating x_S at the indicator vectors 1_T ordered by nondecreasing size |T| gives x_S(1_T) = 1 iff S ⊆ T, an upper-triangular matrix with 1s on the diagonal. So the space of multilinear polynomials of degree ≤ s has dimension

**Σ_{i=0}^{s} C(n, i)** — one basis monomial x_S per subset S ⊆ [n] of size |S| ≤ s.

### 3.2 The non-uniform warm-up: Bose again, generalized

Let A_1, …, A_m be distinct sets whose pairwise intersections all lie in a set L = {ℓ_1, …, ℓ_s} of s allowed values, with no |A_i| in L. Define

f_i(x) = Π_{ℓ ∈ L}(|A_i ∩ x| − ℓ), where |A_i ∩ x| means Σ_{k∈A_i} x_k.

Then f_i(v_j) = 0 for i ≠ j (since |A_i ∩ A_j| ∈ L, one factor vanishes) and f_i(v_i) = Π_{ℓ∈L}(|A_i| − ℓ) ≠ 0 (since |A_i| ∉ L). Expand each f_i(x) and replace every power x_k^r (r ≥ 2) by x_k to obtain a multilinear polynomial f̃_i(x) of degree ≤ s that agrees with f_i on {0,1}^n. The evaluation matrix (f̃_i(v_j)) is diagonal with nonzero diagonal entries — invertible — so the f̃_i are linearly independent in the space of multilinear polynomials of degree ≤ s, giving

**m ≤ Σ_{i≤s} C(n, i).**

Bose's m ≤ n + 1 is the case s = 1 with L = {λ}. Fisher's m ≤ n (uniformity not required!) is the Gram matrix's extra notch.

### 3.3 Ray-Chaudhuri–Wilson: the slice trick

**Theorem (RCW).** Let F = {A_1, …, A_m} be a family of k-subsets of [n] whose pairwise intersections all lie in a set L ⊆ {0, 1, …, k − 1} of size |L| = s (with s ≤ k ≤ n). Then

**m ≤ C(n, s).**

*Proof.* Since L ⊆ {0, 1, …, k − 1}, we have k ∉ L, so the multilinearized polynomials f̃_i from §3.2 satisfy f̃_i(v_i) = Π_{ℓ∈L}(k − ℓ) ≠ 0 and f̃_i(v_j) = 0 for i ≠ j. Thus f̃_1, …, f̃_m are linearly independent even as functions restricted to {v_1, …, v_m}. Now restrict to the **slice** {x ∈ {0,1}^n : Σ_j x_j = k} — the k-subsets of [n] — where all the v_j live. On this slice, any multilinear monomial x_S = Π_{i∈S} x_i of degree |S| < k can be rewritten as a linear combination of multilinear monomials of degree |S| + 1: using x_j² = x_j on {0, 1}^n,

k·x_S = x_S·Σ_j x_j = Σ_{j∈S} x_S·x_j + Σ_{j∉S} x_S·x_j = |S|·x_S + Σ_{j∉S} x_{S∪j},

and since |S| < k we have k − |S| > 0, so

x_S = (1/(k − |S|))·Σ_{j∉S} x_{S∪j}

for all x on the slice. Iterating this substitution for every monomial of degree 0, 1, …, s − 1 (since s ≤ k, every step has |S| ≤ s − 1 < k), every multilinear polynomial of degree ≤ s coincides on the slice with a linear combination of the C(n, s) multilinear monomials of degree **exactly s**. Since f̃_1, …, f̃_m remain linearly independent as functions on {v_1, …, v_m} inside the slice, they span an m-dimensional subspace of a function space spanned by C(n, s) monomials, forcing **m ≤ C(n, s)**. ∎

The slice identity is the whole trick: *uniformity converts "degree ≤ s" into "degree exactly s"*, saving the sum over lower degrees. Machine tightness checks (n = 6, k = 3): for L = {0, 2} the maximum family has 4 members (bound C(6,2) = 15); for L = {0, 1} it is again 4 (Exercise 14 closes this one by hand and finds the truth beneath the bound); for L = {1, 2} the maximum is **10 = C(5,2)** — all triples containing a fixed point — the bound C(6,2) = 15 is honest but not always attained.

### 3.4 Frankl–Wilson: Fermat does the bookkeeping (P22 over F_p)

**Theorem (Frankl–Wilson, modular form).** Fix a prime p and an integer k. If every |A_i| ≡ k (mod p) and every pairwise intersection |A_i ∩ A_j| ≢ k (mod p), then

**m ≤ Σ_{i=0}^{p−1} C(n, i).**

*Proof.* Work over F_p and define, for each set, the Fermat polynomial

p_A(x) = 1 − (|A ∩ x| − k)^{p−1}.

By Fermat's little theorem in F_p, t^{p−1} = 1 if t ≢ 0 (mod p) and t^{p−1} = 0 if t ≡ 0 (mod p) (since p − 1 ≥ 1). Thus at the characteristic vectors v_B ∈ {0,1}^n, p_A(v_A) = 1 − (|A| − k)^{p−1} = 1 − 0 = 1 (sizes are ≡ k), while for B ≠ A, p_A(v_B) = 1 − (|A ∩ B| − k)^{p−1} = 1 − 1 = 0 (intersections are ≢ k). After multilinearizing via x_r² = x_r, the evaluation matrix (p̃_A(v_B)) is the m × m identity matrix I_m over F_p, so the p̃_A are linearly independent over F_p. Since p_A(x) has degree ≤ p − 1, each p̃_A(x) lies in the span of the multilinear monomials Π_{r∈S} x_r with |S| ≤ p − 1 (each monomial of (Σ_{r∈A}x_r − k)^{p−1} uses at most p − 1 distinct variables), a space of dimension Σ_{i=0}^{p−1} C(n, i). ∎

For p = 2 the Fermat polynomial is p_A(x) = 1 − (|A∩x| − k): the independence argument **is** Oddtown's, in disguise — the polynomial method did not replace the linear algebra; it organized it.

### 3.5 The payoff: explicit Ramsey graphs

Turn the theorem into graphs: for a prime p and integers 1 ≤ k ≤ m − 1, let the vertices be the C(m, k) k-subsets of [m] (all of size ≡ k mod p), joining A ≠ B by an edge iff |A ∩ B| ≢ k (mod p). A clique is then a family of k-subsets whose pairwise intersections avoid the residue class k mod p — Frankl–Wilson caps it at Σ_{i≤p−1}C(m, i) (or even C(m, p−1) via the slice reduction when k ≥ p − 1). An independent set is a family of k-subsets whose pairwise intersections all lie in L = {ℓ ∈ {0, …, k − 1} : ℓ ≡ k (mod p)} — Ray-Chaudhuri–Wilson caps it at C(m, |L|), where |L| = ⌊k/p⌋. Two worked instances, fully machine-checked:

**p = 2, m = 5, k = 3.** Vertices: the ten 3-subsets of [5]; join iff |A ∩ B| is even, i.e. (distinct 3-sets meet in 1 or 2 points) iff |A ∩ B| = 2. Complementing each vertex (A ↦ [5] ∖ A) turns this into the graph on 2-subsets of [5] where adjacency means *intersecting* — the complement of the Kneser graph KG(5,2), better known as the **complement of the Petersen graph**. The machine finds ω = 4 (a maximum clique is the set of four triples inside a fixed 4-set, e.g. all triples of {2,3,4,5}) and α = 2. The theory's caps — Frankl–Wilson Σ_{i≤1}C(5,i) = 6 for cliques, RCW C(5,1) = 5 for independent sets — are honest but loose here: 6 and 5 versus the true 4 and 2.

**p = 3, m = 7, k = 4.** Vertices: the thirty-five 4-subsets of [7]; join iff |A ∩ B| ≢ 1 (mod 3) — distinct 4-sets meet in 1, 2 or 3 points, so this joins exactly the pairs meeting in 2 or 3. Machine: ω = 15 (all 4-sets avoiding a fixed point — any two of them share ≥ 2 points), α = 2; caps: Frankl–Wilson Σ_{i≤2}C(7,i) = 29, RCW C(7,1) = 7. Again valid, again loose.

✎ **Checkpoint — parameters must not degenerate.** Try p = 3, m = 7, k = 5: two distinct 5-subsets of [7] meet in 3 or 4 points — residues 0 and 1 mod 3, never 2 ≡ k (mod 3). So *every* pair gets joined: the construction collapses to K₂₁ (ω = 21, α = 1) and proves nothing. In general, two distinct k-subsets of [m] intersect in sizes ranging over {max(0, 2k − m), …, k − 1}, an interval of min(k, m − k) consecutive integers; whenever min(k, m − k) < p and k − p < max(0, 2k − m), the residue k mod p never occurs among pairwise intersections and the graph degenerates into K_{C(m,k)}. Check a purported construction for degeneracy before believing its bounds.

**The Ramsey corollary (cited, not proven here).** Run the same construction at scale: take k = p² − 1 (so k ≡ −1 (mod p), and the only intersection sizes below k congruent to k (mod p) are p − 1, 2p − 1, …, p² − p − 1, giving |L| = p − 1). Then both the clique number and the independence number are bounded above by C(m, p−1), while the vertex count is N = C(m, p² − 1). Choosing m = p³, Frankl and Wilson (1981) obtained explicit graphs with no clique or independent set of size K = C(p³, p−1) + 1 on

N = C(p³, p² − 1) = exp(Ω(log²K / log log K))

vertices — a quasipolynomial constructive Ramsey lower bound that stood for a quarter century, until Barak–Rao–Shaltiel–Wigderson (2006) improved it. The two worked graphs above are this construction at toy scale; the full optimization is cited to the papers, flagged as beyond this chapter's scope.

**What you now own:** the multilinear lemma, the slice trick (uniformity as a dimension discount), Fermat polynomials as bookkeeping, and the reflex of testing a construction's parameters for degeneracy before trusting its bounds.

---

## Lecture 4 · The Friendship Theorem

**Problem.** If in a simple graph G on n ≥ 3 vertices every two distinct vertices have **exactly one** common neighbor, then some vertex is adjacent to **all** others — and the graph is a "windmill": t ≥ 1 triangles glued at one central vertex (n = 2t + 1).

The proof has three load-bearing parts, each complete here (the middle one was a flagged sketch in the reference literature for years; it is a degree-class argument, and it assembles cleanly).

### 4.1 Claim 1 — non-adjacent vertices have equal degrees

**Claim 1.** If x ≁ y then d(x) = d(y).
*Proof.* Let z be the unique common neighbor of x and y. The natural move is to send each u ∈ N(x), u ≠ z, to the unique common neighbor α(u) of the pair (u, y) — but the codomain needs care, and the first draft of this proof (with its mirror, answer A5) missed it: α(u) can be **z itself**. In W₂, with x = a_1, y = a_2, u = b_1, the pair (u, y) has common neighbor the hub — which is z. So α does not in general land in N(y)∖{z}; the argument must excise one vertex from each side, and the excised vertices are forced. The members of N(x)∖{z} adjacent to z are exactly the common neighbors of the pair (x, z): there is at most one (two would give the pair (x, z) two common neighbors) and at least one (that pair's common neighbor u_0 is adjacent to x and to z, and is not z itself) — so **exactly one**, u_0 = cn(x, z). Mirror-wise, v_0 = cn(y, z) is the unique z-adjacent member of N(y)∖{z}. Now take u ∈ N(x)∖{z, u_0}. Then u ≁ y (else u is a second common neighbor of x and y), so the pair (u, y) has its unique common neighbor α(u), and: α(u) ≠ z, because z ≁ u — u_0 is the *only* z-adjacent member of N(x)∖{z}; α(u) ≠ x, because x ≁ y; and α(u) ≠ v_0 — if it were, the pair (u, z) would have the two common neighbors x and v_0, distinct since x ≁ y while v_0 ~ y. And α is injective on this domain: if α(u_1) = α(u_2) = w with u_1 ≠ u_2, then w is adjacent to u_1 and u_2, and so is x — the pair (u_1, u_2) would have the two common neighbors x and w, and w ≠ x because x ≁ y while w ~ y. So α is injective from N(x)∖{z, u_0} into N(y)∖{z, v_0}, giving d(x) − 2 ≤ d(y) − 2. The mirror construction (swap x and y, u_0 ↔ v_0) is an injection the other way, so d(y) − 2 ≤ d(x) − 2: **d(x) = d(y)**. ∎ (The census below runs the diagnostic both ways: the un-excisioned codomain claim fails in every one of the 120 census graphs that have non-adjacent pairs — α(u) = z in each of the 1,320 pairs — while the u_0/v_0 excision verifies on all of them.)

Contrapositive, worth enshrining: **distinct degrees force adjacency.** (Machine: the claim holds in every graph of the census below — 121 friendship graphs, zero exceptions.)

### 4.2 Claim 2 — no universal vertex is impossible (the ERS brick)

**Claim 2.** Every friendship graph on n ≥ 3 vertices has a universal vertex.
*Proof.* Suppose not. Since n ≥ 3 and every pair of vertices has a common neighbor, no vertex has degree 0, so every degree lies in {1, …, n − 2}. Partition V into degree classes. If some degree class is a singleton {x}, then every y ≠ x has d(y) ≠ d(x), so by Claim 1's contrapositive x is adjacent to every other vertex: d(x) = n − 1, universal, contradiction. So every nonempty degree class has ≥ 2 members; in particular, picking any nonempty degree class B (of common degree k), B contains at least two distinct vertices b_1, b_2.

Now watch the cross-class edges. Every w ∉ B has degree ≠ k, so w is adjacent to **every** vertex of B (Claim 1's contrapositive). In particular every w ∉ B is a common neighbor of the pair (b_1, b_2) — which has exactly one common neighbor. So |V ∖ B| ≤ 1.

Two cases. If V ∖ B = {z}: z is adjacent to all of B (distinct degrees), so d(z) = n − 1 — universal, contradiction. If V ∖ B = ∅: the graph is k-regular, and the spectral lemma below (§4.4) forces k = 2, n = 3 — the triangle K₃, in which every vertex has degree 2 = n − 1 and is universal. Contradiction again. ∎

### 4.3 Assembly — the universal vertex pins down the windmill

Let u be universal. Put H = G − u. If H contained a 3-vertex path w–x–y with w ≠ y, the pair (w, y) would have common neighbors x **and** u — two, contradiction. (This also rules out any triangle w–x–y in H.) So H has maximum degree ≤ 1: a matching plus isolated vertices. But an isolated vertex z of H has N_G(z) = {u}, while N_G(u) = V ∖ {u} — the pair (z, u) has N_G(z) ∩ N_G(u) = ∅, **zero** common neighbors. Contradiction. So H has no isolated vertices and is a perfect matching: n − 1 is even, n = 2t + 1 (t ≥ 1), and G is exactly t triangles sharing u: the windmill W_t. ∎

**Figure 1** draws W₄ alongside the deleted state H = G − u; check all three pair types: two vertices from different blades share only u; the two vertices of one blade share only u; and the pair (u, a_i) shares only the blade-partner b_i.

### 4.4 The spectral lemma — friendship graphs are (almost) never regular

**Lemma.** A k-regular friendship graph on n ≥ 3 vertices exists only for k = 2, n = 3 (the triangle K₃).
*Proof.* Let A be the adjacency matrix. "Exactly one common neighbor per pair" is a matrix equation: (A²)_{uv} = 1 for u ≠ v and (A²)_{uu} = d(u) = k on the diagonal:

**A² = J + (k − 1)I.**

Applying both sides to the all-ones vector 𝟙 gives k²𝟙 = A²𝟙 = (J + (k − 1)I)𝟙 = (n + k − 1)𝟙, so n = k(k − 1) + 1. Since A is real symmetric and J𝟙 = n𝟙, 𝟙 is an eigenvector of A with eigenvalue k, and A preserves the orthogonal complement 𝟙⊥ (of dimension n − 1). On 𝟙⊥, J acts as 0, so A² acts as (k − 1)I; thus A's eigenvalues on 𝟙⊥ are ±√(k − 1) with nonnegative integer multiplicities a, b satisfying a + b = n − 1. Because G is a simple graph, the trace of A is 0:

k + (a − b)√(k − 1) = 0.

Since n ≥ 3, we have k ≥ 2 (as k = 1 gives n = 1). If k − 1 is not a perfect square, √(k − 1) is irrational, so a − b = 0 and k = 0 — impossible. Thus k − 1 = t² for a positive integer t, giving k = t² + 1 and (b − a)t = t² + 1. Then t | t² + 1 forces t | 1, so **t = 1, k = 2**, and n = k(k − 1) + 1 = 3, which is K₃. ∎

A counting cross-check of the regular case — honest label: it re-derives the n–k ledger of the matrix equation above by double counting (P2) but is *not* a complete second proof, because it excludes no even k ≥ 4 (parity kills only the odd k: n = k(k−1) + 1 is always odd, so nk = 2|E| even forces k even — k = 4, 6, … survive; the trace ledger above is what excludes them). Length-2 walks between distinct ordered pairs (u, v) number n(n − 1) — one per ordered pair — and also Σ_{w∈V} d(w)(d(w) − 1) = n·k(k − 1) (choosing the middle vertex w and two distinct neighbors). Dividing by n gives n − 1 = k(k − 1), i.e. **n = k(k − 1) + 1**. For k = 2: n = 3.

### 4.5 Census, spectra, and the shape of the answer

Machine census, all labeled graphs on n = 3 … 7 vertices: friendship graphs number **1, 0, 15, 0, 105** — every single one a windmill with a universal vertex, Claim 1 holding throughout. The count has a clean formula: for n = 3 (t = 1), W_1 = K₃ has all 3 vertices universal, giving 1 labeled graph; for odd n = 2t + 1 ≥ 5 (t ≥ 2), the universal hub has degree 2t > 2 and is unique (n choices), and the remaining n − 1 vertices form a perfect matching ((n − 2)!! ways), giving n(n − 2)!! labeled friendship graphs: 5·3!! = 15, 7·5!! = 105.

The windmill's spectrum is explicit (Exercise 9 derives it): W_t has eigenvalues 1 (t − 1 times), −1 (t times), and (1 ± √(1+8t))/2. So W_2 carries {(1±√17)/2, 1, −1, −1} and W_3 carries {3, 1, 1, −1, −1, −1, −2}. Non-regular friendship graphs satisfy the matrix equation in its honest form A² = J + (D − I) with D = diag(degrees) — the lab verifies it entry by entry on W_2, and on the triangle K₃ it reads A² = I + J with det A = 2.

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 880 390" font-family="system-ui, -apple-system, 'Segoe UI', sans-serif">
  <defs>
    <marker id="arrow-slate" viewBox="0 0 10 10" refX="8" refY="5" markerWidth="6" markerHeight="6" orient="auto-start-reverse">
      <path d="M 0 1 L 8 5 L 0 9 z" fill="#475569"/>
    </marker>
    <marker id="arrow-red" viewBox="0 0 10 10" refX="8" refY="5" markerWidth="6" markerHeight="6" orient="auto-start-reverse">
      <path d="M 0 1 L 8 5 L 0 9 z" fill="#dc2626"/>
    </marker>
  </defs>
  <rect x="0" y="0" width="880" height="390" fill="#ffffff"/>
  <text x="32" y="30" font-size="16.5" font-weight="700" fill="#193e5c">Figure 1 &#183; The windmill W&#8324; (n = 9, t = 4) and the deletion assembly H = G &#8722; u (Lecture 4, &#167;&#167;4.3&#8211;4.5)</text>

  <!-- Panel A: Symmetric Windmill W_4 -->
  <text x="155" y="58" font-size="13" font-weight="700" fill="#1e293b" text-anchor="middle">A. Windmill W&#8324; (universal hub u)</text>

  <!-- Spokes from hub u=(155, 195) to the 4 blades -->
  <g stroke="#2563eb" stroke-width="2.8">
    <!-- Blade 1 (top-left): a1=(75, 105), b1=(125, 80) -->
    <line x1="155" y1="195" x2="75" y2="105"/>
    <line x1="155" y1="195" x2="125" y2="80"/>
    <!-- Blade 2 (top-right): a2=(185, 80), b2=(235, 105) -->
    <line x1="155" y1="195" x2="185" y2="80"/>
    <line x1="155" y1="195" x2="235" y2="105"/>
    <!-- Blade 3 (bottom-right): a3=(235, 285), b3=(185, 310) -->
    <line x1="155" y1="195" x2="235" y2="285"/>
    <line x1="155" y1="195" x2="185" y2="310"/>
    <!-- Blade 4 (bottom-left): a4=(125, 310), b4=(75, 285) -->
    <line x1="155" y1="195" x2="125" y2="310"/>
    <line x1="155" y1="195" x2="75" y2="285"/>
  </g>

  <!-- Blade matching edges in W_4 -->
  <g stroke="#dc2626" stroke-width="3.8">
    <line x1="75" y1="105" x2="125" y2="80"/>
    <line x1="185" y1="80" x2="235" y2="105"/>
    <line x1="235" y1="285" x2="185" y2="310"/>
    <line x1="125" y1="310" x2="75" y2="285"/>
  </g>

  <!-- Central hub vertex u -->
  <circle cx="155" cy="195" r="16" fill="#dc2626" stroke="#172333" stroke-width="2"/>
  <text x="155" y="200" font-size="14" font-weight="700" fill="#ffffff" text-anchor="middle">u</text>

  <!-- Blade 1 vertices -->
  <circle cx="75" cy="105" r="15" fill="#dbeafe" stroke="#2563eb" stroke-width="2.2"/>
  <text x="75" y="110" font-size="13" font-weight="700" fill="#172333" text-anchor="middle">a&#8321;</text>
  <circle cx="125" cy="80" r="15" fill="#dbeafe" stroke="#2563eb" stroke-width="2.2"/>
  <text x="125" y="85" font-size="13" font-weight="700" fill="#172333" text-anchor="middle">b&#8321;</text>

  <!-- Blade 2 vertices -->
  <circle cx="185" cy="80" r="15" fill="#dbeafe" stroke="#2563eb" stroke-width="2.2"/>
  <text x="185" y="85" font-size="13" font-weight="700" fill="#172333" text-anchor="middle">a&#8322;</text>
  <circle cx="235" cy="105" r="15" fill="#dbeafe" stroke="#2563eb" stroke-width="2.2"/>
  <text x="235" y="110" font-size="13" font-weight="700" fill="#172333" text-anchor="middle">b&#8322;</text>

  <!-- Blade 3 vertices -->
  <circle cx="235" cy="285" r="15" fill="#dbeafe" stroke="#2563eb" stroke-width="2.2"/>
  <text x="235" y="290" font-size="13" font-weight="700" fill="#172333" text-anchor="middle">a&#8323;</text>
  <circle cx="185" cy="310" r="15" fill="#dbeafe" stroke="#2563eb" stroke-width="2.2"/>
  <text x="185" y="315" font-size="13" font-weight="700" fill="#172333" text-anchor="middle">b&#8323;</text>

  <!-- Blade 4 vertices -->
  <circle cx="125" cy="310" r="15" fill="#dbeafe" stroke="#2563eb" stroke-width="2.2"/>
  <text x="125" y="315" font-size="13" font-weight="700" fill="#172333" text-anchor="middle">a&#8324;</text>
  <circle cx="75" cy="285" r="15" fill="#dbeafe" stroke="#2563eb" stroke-width="2.2"/>
  <text x="75" y="290" font-size="13" font-weight="700" fill="#172333" text-anchor="middle">b&#8324;</text>

  <!-- Panel B: Deleted state H = G - u and forbidden isolated vertex z -->
  <text x="375" y="58" font-size="13" font-weight="700" fill="#1e293b" text-anchor="middle">B. Deleted state H = G &#8722; u (&#167;4.3)</text>

  <!-- Dashed deleted spokes from deleted hub u=(375, 175) -->
  <g stroke="#94a3b8" stroke-width="1.8" stroke-dasharray="5,4">
    <line x1="375" y1="175" x2="310" y2="105"/>
    <line x1="375" y1="175" x2="350" y2="85"/>
    <line x1="375" y1="175" x2="400" y2="85"/>
    <line x1="375" y1="175" x2="440" y2="105"/>
    <line x1="375" y1="175" x2="440" y2="245"/>
    <line x1="375" y1="175" x2="400" y2="265"/>
    <line x1="375" y1="175" x2="350" y2="265"/>
    <line x1="375" y1="175" x2="310" y2="245"/>
    <!-- Dashed spoke to hypothetical isolated vertex z=(375, 325) -->
    <line x1="375" y1="175" x2="375" y2="325" stroke="#dc2626" stroke-dasharray="4,4"/>
  </g>

  <!-- Remaining solid red matching edges in H = G - u -->
  <g stroke="#dc2626" stroke-width="3.5">
    <line x1="310" y1="105" x2="350" y2="85"/>
    <line x1="400" y1="85" x2="440" y2="105"/>
    <line x1="440" y1="245" x2="400" y2="265"/>
    <line x1="350" y1="265" x2="310" y2="245"/>
  </g>

  <!-- Deleted hub u (dashed circle) -->
  <circle cx="375" cy="175" r="14" fill="#f8fafc" stroke="#64748b" stroke-width="2" stroke-dasharray="4,3"/>
  <text x="375" y="180" font-size="13" font-weight="700" fill="#64748b" text-anchor="middle">u</text>

  <!-- Blade nodes in H -->
  <circle cx="310" cy="105" r="12" fill="#dbeafe" stroke="#2563eb" stroke-width="2"/>
  <text x="310" y="109" font-size="11" font-weight="700" fill="#172333" text-anchor="middle">a&#8321;</text>
  <circle cx="350" cy="85" r="12" fill="#dbeafe" stroke="#2563eb" stroke-width="2"/>
  <text x="350" y="89" font-size="11" font-weight="700" fill="#172333" text-anchor="middle">b&#8321;</text>
  <circle cx="400" cy="85" r="12" fill="#dbeafe" stroke="#2563eb" stroke-width="2"/>
  <text x="400" y="89" font-size="11" font-weight="700" fill="#172333" text-anchor="middle">a&#8322;</text>
  <circle cx="440" cy="105" r="12" fill="#dbeafe" stroke="#2563eb" stroke-width="2"/>
  <text x="440" y="109" font-size="11" font-weight="700" fill="#172333" text-anchor="middle">b&#8322;</text>
  <circle cx="440" cy="245" r="12" fill="#dbeafe" stroke="#2563eb" stroke-width="2"/>
  <text x="440" y="249" font-size="11" font-weight="700" fill="#172333" text-anchor="middle">a&#8323;</text>
  <circle cx="400" cy="265" r="12" fill="#dbeafe" stroke="#2563eb" stroke-width="2"/>
  <text x="400" y="269" font-size="11" font-weight="700" fill="#172333" text-anchor="middle">b&#8323;</text>
  <circle cx="350" cy="265" r="12" fill="#dbeafe" stroke="#2563eb" stroke-width="2"/>
  <text x="350" y="269" font-size="11" font-weight="700" fill="#172333" text-anchor="middle">a&#8324;</text>
  <circle cx="310" cy="245" r="12" fill="#dbeafe" stroke="#2563eb" stroke-width="2"/>
  <text x="310" y="249" font-size="11" font-weight="700" fill="#172333" text-anchor="middle">b&#8324;</text>

  <!-- Forbidden isolated leftover vertex z in H -->
  <circle cx="375" cy="325" r="13" fill="#fef2f2" stroke="#dc2626" stroke-width="2" stroke-dasharray="4,3"/>
  <text x="375" y="330" font-size="12" font-weight="700" fill="#dc2626" text-anchor="middle">z</text>
  <line x1="435" y1="325" x2="392" y2="325" stroke="#dc2626" stroke-width="1.6" marker-end="url(#arrow-red)"/>
  <text x="375" y="362" font-size="11.5" fill="#dc2626" font-weight="600" text-anchor="middle">isolated z in H &#8658; cn(z, u) = &#8709; (forbidden)</text>

  <!-- Right Panel: Three pair types and census notes -->
  <text x="490" y="90" font-size="13.5" fill="#172333" font-weight="700">Every pair has a unique common neighbor:</text>
  <text x="490" y="118" font-size="12.5" fill="#172333">&#8226; Cross-blade pair (a&#8321;, b&#8322;) &#8594; only hub u</text>
  <text x="490" y="142" font-size="12.5" fill="#172333">&#8226; In-blade pair (a&#8321;, b&#8321;) &#8594; only hub u</text>
  <text x="490" y="166" font-size="12.5" fill="#172333">&#8226; Hub-blade pair (u, a&#8321;) &#8594; only partner b&#8321;</text>

  <text x="490" y="204" font-size="12.5" fill="#475569">Assembly (&#167;4.3): deleting universal u (dashed)</text>
  <text x="490" y="224" font-size="12.5" fill="#475569">leaves H = G &#8722; u with max degree &#8804; 1 (no path</text>
  <text x="490" y="244" font-size="12.5" fill="#475569">P&#8323; or triangle K&#8323;). Any isolated vertex z in H</text>
  <text x="490" y="264" font-size="12.5" fill="#475569">would leave (z, u) with 0 common neighbors,</text>
  <text x="490" y="284" font-size="12.5" fill="#475569">forcing H to be a perfect matching (red).</text>

  <text x="490" y="320" font-size="12.5" fill="#475569">Census (n = 3&#8230;7): 1, 0, 15, 0, 105 labeled</text>
  <text x="490" y="340" font-size="12.5" fill="#475569">friendship graphs &#8212; 1 for n = 3 (K&#8323;) and</text>
  <text x="490" y="360" font-size="12.5" fill="#475569">n(n &#8722; 2)!! for odd n = 2t + 1 &#8805; 5.</text>
</svg>
```

**What you now own:** the common-neighbor bijection (Claim 1), the degree-class split (Claim 2 — pigeonhole plus one adjacency observation), the assembly, and the reflex of writing combinatorial information as a matrix equation before thinking.

---

## The Trick Bag (reference card)

| Pattern | Plain language | Where you met it |
|---------|---------------|------------------|
| **P19 Rank / dimension** | Gram or evaluation matrix; rank bounded above by ambient dimension and below by positive definiteness / invertibility | L1, L4; Ch. 8 (two-distance sets) |
| **P19′ Independence via dot products** | Self-products nonzero, cross-products zero — over the field the congruences name | L2, L3 |
| **P22 Polynomial method** | One polynomial per set, vanishing on the others; slice trick for uniform families; Fermat for modular conditions; Krawtchouk combinations as certificates | L1, L3; Ch. 8 (two-distance sets, Delsarte) |
| **P21 Spectral / Rayleigh** | λ1 ≥ 2m/n from the average; structure caps λ1; operator norm μ on 𝟙⊥ prices pseudorandomness; smallest eigenvalue prices independence | Ch. 8 (the spectral lectures) |
| **P20 Weight shifting** | Merge weight into better-connected vertices; the support shrinks to a clique at no cost | Ch. 8 (Motzkin–Straus) |
| **The field chooses itself (lore)** | Parity/mod-p conditions in the statement ⇒ do linear algebra over F_p | L2, L3 |
| **Center before counting (lore)** | Subtract the mean; the centered Gram carries the true rank (k − 1, not k) | Ch. 8 (two-distance sets) |
| **Test parameters for degeneracy (lore)** | A construction whose forbidden values never occur proves nothing (the K₂₁ non-example) | L3 |
| **Compress before you bound (lore)** | Restrict the matrix to a subspace or partition first: interlacing makes every such restriction honest, and equitable quotients give exact eigenvalues | Ch. 8 (interlacing) |
| **Distribute, then average (lore)** | Sum a quantity over all pairs before bounding it: character sums come out as squares, distance distributions as feasible points | Ch. 8 (Delsarte) |

**Formula box:** Fisher: pairwise intersections exactly λ ≥ 0, no |A_i| = λ ⇒ m ≤ n; Bose: m ≤ n + 1 via diagonal evaluation; det(λJ + D) = det(D)(1 + λΣ1/d_i). Oddtown ≤ n; Eventown ≤ 2^{⌊n/2⌋}; same-parity sizes ⇒ ≤ 2^{n−1} (n ≥ 1); mod-p analogue ≤ n for every prime. RCW: k-uniform, intersections in L ⊆ {0, …, k−1} ⇒ ≤ C(n, |L|). Frankl–Wilson: sizes ≡ k, intersections ≢ k (mod p) ⇒ ≤ Σ_{i≤p−1}C(n,i); Ramsey corollary R(K,K) ≥ exp(c·log²K/log log K) (cited). Friendship (n ≥ 3): every pair exactly one common neighbor ⇒ windmill W_t (n = 2t + 1), labeled count 1 for n = 3 and n(n−2)!! for odd n ≥ 5; k-regular friendship ⇒ k = 2, n = 3 (n = k(k−1)+1); W_t spectrum {1^{t−1}, −1^t, (1±√(1+8t))/2}. The spectral half of this card — Rayleigh averaging, the expander-mixing lemma, Motzkin–Straus and spectral Turán, s-distance sets, interlacing, the Hoffman bounds, Lovász theta, and the Delsarte LP with its Krawtchouk certificates — moved with the spectral lectures to Chapter 8 (Spectral Methods and the Modern Toolkit).

---

## Exercises (graded: ●○○ easy · ●●○ moderate · ●●● tough)

**Easy — one idea, applied directly**

1. ●○○ **An Oddtown census.** Show that the Oddtown bound n is attained on [4]: exhibit four sets, and explain why the census says no fifth can join. *Hint: L2.1; the four 3-subsets of [4].*
2. ●○○ **Eventown's ceiling.** Prove that an Eventown family on [n] has at most 2^{⌊n/2⌋} members. *Hint: P19′ — the span W satisfies W ⊆ W⊥.*
3. ●○○ **An odd determinant.** L2.1 proved Oddtown over F₂. Re-prove it over the rationals: show the Oddtown Gram matrix is congruent to the identity mod 2, deduce that its determinant is odd — hence nonzero — and conclude m ≤ n, noting which fields the argument reaches. Then show the same route dies for Eventown: exhibit an Eventown family on [4] whose Gram matrix is singular, and name the step of the mod-2 proof that has no rational analogue. *Hint: P19′ — the congruence is the whole engine: diagonal odd, off-diagonal even, so G ≡ I (mod 2); for the witness, pair [4] up as {1,2}, {3,4} and add their union.*
4. ●○○ **Weighted blocks.** Put a real weight w_i on each point of [n] and define the weighted intersection ⟨A, B⟩ = Σ_{i∈A∩B} w_i. Suppose the sets A_1, …, A_m pairwise meet in the same weighted amount Λ > 0, and every weighted size ⟨A_i, A_i⟩ is strictly larger than Λ. Prove m ≤ n — no integrality anywhere in the statement. Then audit the proof: which hypotheses does the argument actually consume — the positivity of the weights, some parity, or neither? *Hint: P19 — G = ΛJ + diag(⟨A_i, A_i⟩ − Λ); watch closely what the lemma of L1.2 ever asks about the w_i.*

**Moderate — two ideas, or one tricky step**

5. ●●○ **The Fano plane's Gram.** Compute the determinant of the Fano plane's intersection matrix (diagonal 3, off-diagonal 1) — both by the determinant lemma of L1.2 and by Sylvester's minors — and explain what each computation certifies. *Hint: 2I + J; the lemma's 1 + λΣ1/d_i.*
6. ●●○ **The F₃ analogue.** Prove: if every |A_i| ≡ 1 (mod 3) and every pairwise intersection ≡ 0 (mod 3), then the family has at most n members. Which step of L2.1 survives unchanged, and what does the census on [4] say the extremal family is? *Hint: P19′ over F₃.*
7. ●●○ **Friendship Claim 1.** Prove that in a friendship graph, non-adjacent vertices have equal degrees, and state the contrapositive that powers Claim 2. *Hint: the excised common-neighbor map α: N(x)∖{z, u_0} → N(y)∖{z, v_0}; injectivity via the two-common-neighbors contradiction.*
8. ●●○ **Auditing Fisher's boundary (|A_i| = λ).** Suppose distinct sets A_1, …, A_m ⊆ [n] pairwise meet in λ ≥ 1 points. When every |A_i| > λ, the determinant lemma of L1.2 prices det(λJ + D) > 0 and gives m ≤ n. Audit what happens if the hypothesis |A_i| ≠ λ is dropped: show that at most one set can have size λ, explain where the determinant-lemma formula breaks when |A_1| = λ, and prove directly that m ≤ n still holds. Finally, verify sharpness on the near-pencil on [n] (n ≥ 3) and the Fano plane. *Hint: P19 — if |A_1| = λ, then A_1 ⊆ A_j for all j ≥ 2, and the remainders A_j ∖ A_1 are nonempty and pairwise disjoint inside [n] ∖ A_1.*
9. ●●○ **Windmill spectra.** Derive the full spectrum of the windmill W_t: show 1 occurs t − 1 times, −1 occurs t times, and the two remaining eigenvalues solve λ² − λ − 2t = 0. Verify against W_2 and W_3. *Hint: vectors (1, −1) supported on one blade; differences of blade sums; then the 2×2 quotient {hub} ∪ {symmetrized blade}.*
10. ●●○ **Hadamard orders are multiples of four.** An n × n ±1 matrix H with HHᵀ = nI is a Hadamard matrix. Prove: if one exists with n ≥ 3, then 4 | n — and conclude that no Hadamard matrix of order 3 exists. *Hint: P19 + P2 — normalize the first row to all + by flipping columns, then census the columns by the sign pair they carry in rows 2 and 3 (the four patterns a, b, c, d); count the same columns three ways: against row 2's balance, against row 3's balance, and against the orthogonality of rows 2 and 3.*

**Tough — several chapter ideas combined**

11. ●●● **Graham–Pollak, and the cover that cheats.** Prove that the edges of K_n cannot be **partitioned** into fewer than n − 1 complete bipartite graphs — and contrast: they can be **covered** by ⌈log₂n⌉. *Hint: P19 — on V = {Σx = 0} use the partition identity Σᵢ 2 s_{A_i}s_{B_i} = −||x||² and the vectors z_i = |B_i|·1_{A_i} − |A_i|·1_{B_i}; for the cover, give each vertex its binary address and cut by bit.*
12. ●●● **One more parity class.** Prove: a family of subsets of [n] (n ≥ 1) whose pairwise symmetric differences are all even has at most 2^{n−1} members, sharply. *Hint: |A △ B| ≡ |A| + |B| (mod 2); one parity class.*
13. ●●● **The ten-vertex Ramsey graph.** Build the graph on the 3-subsets of [5] joining A, B when |A ∩ B| = 2. Prove ω = 4 and α = 2 by hand, verify the theoretical caps (6 and 5), and identify the graph as the complement of the Petersen graph. *Hint: L3.5; complement each triple to a 2-subset and watch "intersect in 2" become "intersect in 1".*

**Pattern unknown — you choose the tool** *No hints, no difficulty rating: diagnosing the problem is part of the problem. Worked answers still wait at the end.*

14. ◆ On [6], how large can a family of 3-subsets be if all pairwise intersections lie in {0, 1}? The general theory offers a bound; the truth is smaller. Find both, and close the gap by hand.
15. ◆ Enumerate every (finite) linear space on 4 labeled points: any two points on exactly one line, each line ≥ 2 points, not all collinear. How many are there, and what does each say about de Bruijn–Erdős?
16. ◆ Find the independence number of the Petersen graph and prove by hand that every independent set attaining it is one of five configurations.

**Explorations — ◐ research-style training** *No single right answer — what you should find is described in each.*

17. ◐ **A Ramsey graph factory.** For several primes p, ground sizes m and uniform sizes k, build the Frankl–Wilson graphs of L3.5 (vertices = k-subsets of [m], join on the wrong residue class), compute ω and α exhaustively, and compare against the Frankl–Wilson and RCW caps. Hunt for degenerate parameters — can you predict degeneracy before the machine finds it? How close do the actual cliques come to the caps as m grows?

---

## Computational Lab (verified)

Two parts, all deterministic; the printed outputs were produced by machine runs of exactly this logic (the verification record in the appendix enumerates the runs). Part 1 verifies the F_p rank machine on Oddtown, Eventown, and the F₃ singletons, the determinant lemma on the Fano plane and the near-pencils, the linear spaces on [4], and the Frankl–Wilson Ramsey parameters. Part 2 runs the friendship census for n = 3 … 7, the Claim 1 excision diagnostic across all 1,320 non-adjacent pairs, and the matrix equation A² = J + (D − I) on W_2. Runtime note: Part 2's n = 7 census takes a few minutes.

### Part 1 — Rank machines over F_p, determinants, linear spaces, and Frankl–Wilson

```python
from itertools import combinations
import math

# 1. Rank machine over F_p (p prime), guarding empty inputs
def fp_rank(rows, p):
    if not rows or not rows[0]:
        return 0
    M = [[x % p for x in r] for r in rows]
    r0, rank = 0, 0
    for c in range(len(M[0])):
        pvt = next((i for i in range(r0, len(M)) if M[i][c] % p), -1)
        if pvt < 0:
            continue
        M[r0], M[pvt] = M[pvt], M[r0]
        inv = pow(M[r0][c], p - 2, p)  # Fermat inverse in F_p
        M[r0] = [(a * inv) % p for a in M[r0]]
        for i in range(len(M)):
            if i != r0 and M[i][c] % p:
                f = M[i][c]
                M[i] = [(a - f * b) % p for a, b in zip(M[i], M[r0])]
        r0 += 1
        rank += 1
        if r0 == len(M):
            break
    return rank

def vec(A, n):
    return [1 if i in A else 0 for i in range(n)]

oddtown  = [vec({0,1,2}, 4), vec({0,1,3}, 4), vec({0,2,3}, 4), vec({1,2,3}, 4)]
eventown = [vec(set(), 4), vec({0,1}, 4), vec({2,3}, 4), vec({0,1,2,3}, 4)]
f3_fam   = [vec({0}, 4), vec({1}, 4), vec({2}, 4), vec({3}, 4)]
print("Ranks (Oddtown/F2, Eventown/F2, Singletons/F3):",
      fp_rank(oddtown, 2), fp_rank(eventown, 2), fp_rank(f3_fam, 3))

# 2. L1.2 Determinant Lemma & Sylvester leading principal minors (Fano & near-pencils)
def det_lemma_int(d_list, lam=1):
    if any(d <= 0 for d in d_list):
        raise ValueError("Every d_i = |A_i| - lam must be strictly positive.")
    m = len(d_list)
    return math.prod(d_list) + lam * sum(
        math.prod(d_list[j] for j in range(m) if j != i) for i in range(m)
    )

fano_minors = [det_lemma_int([2] * k, 1) for k in range(1, 8)]
near_pencil_dets = [det_lemma_int([1] * (n - 1) + [n - 2], 1) for n in range(3, 8)]
print("Fano leading minors (k=1..7):", fano_minors)
print("Near-pencil dets (n=3..7):   ", near_pencil_dets)

# 3. L1.3 / A15 Exhaustive census of linear spaces on n = 4 labeled points
candidate_lines = [set(c) for r in (2, 3) for c in combinations(range(4), r)]
pairs_4 = [set(p) for p in combinations(range(4), 2)]
lin_spaces_4 = [
    fam for r in range(1, len(candidate_lines) + 1)
    for fam in combinations(candidate_lines, r)
    if all(sum(1 for L in fam if p.issubset(L)) == 1 for p in pairs_4)
]
print("Linear spaces on [4]:", len(lin_spaces_4),
      "with line counts", sorted(len(fam) for fam in lin_spaces_4))

# 4. L3.5 Frankl-Wilson Ramsey graph check (exact clique/independence numbers & degeneracy guard)
def fw_ramsey_stats(p, m, k):
    if not (1 <= k <= m - 1):
        raise ValueError("Require 1 <= k <= m - 1.")
    verts = [set(c) for c in combinations(range(m), k)]
    N = len(verts)
    adj = [0] * N
    for i in range(N):
        for j in range(i + 1, N):
            if len(verts[i] & verts[j]) % p != k % p:
                adj[i] |= 1 << j
                adj[j] |= 1 << i

    def max_clique_size(cands):
        if not cands:
            return 0
        best = 0
        while cands and len(cands) > best:
            v = cands.pop()
            best = max(best, 1 + max_clique_size(cands & {u for u in cands if (adj[v] >> u) & 1}))
        return best

    all_v = (1 << N) - 1
    omega = max_clique_size(set(range(N)))
    # Switch to complement adjacency for independence number alpha
    for i in range(N):
        adj[i] = (~adj[i]) & all_v & ~(1 << i)
    alpha = max_clique_size(set(range(N)))
    fw_cap = sum(math.comb(m, i) for i in range(p))
    rcw_cap = math.comb(m, k // p)
    degen_complete = min(k, m - k) < p
    return N, omega, alpha, fw_cap, rcw_cap, degen_complete

print("FW(2,5,3):", fw_ramsey_stats(2, 5, 3))
print("FW(3,7,4):", fw_ramsey_stats(3, 7, 4))
print("FW(3,7,5):", fw_ramsey_stats(3, 7, 5))
```

**Verified output.**

```
Ranks (Oddtown/F2, Eventown/F2, Singletons/F3): 4 2 4
Fano leading minors (k=1..7): [3, 8, 20, 48, 112, 256, 576]
Near-pencil dets (n=3..7):    [4, 9, 16, 25, 36]
Linear spaces on [4]: 5 with line counts [4, 4, 4, 4, 6]
FW(2,5,3): (10, 4, 2, 6, 5, False)
FW(3,7,4): (35, 15, 2, 29, 7, False)
FW(3,7,5): (21, 21, 1, 29, 7, True)
```

Oddtown: four 3-subsets of [4] — sizes 3 odd, pairwise intersections 2 even — rank **4 = family size = n**: the independence proof of L2, live and tight. Eventown: the unions-of-pairs family — rank only **2** over F₂: the rank argument genuinely collapses, which is *why* Eventown permits exponentially many sets. F₃: the singleton family (sizes ≡ 1, intersections ≡ 0 mod 3) has rank **4**: the mod-p independence argument runs verbatim outside F₂. The determinant lemma prices the Fano Gram's leading minors — det(2I_k + J_k) = 2^{k−1}(k + 2): 3, 8, 20, 48, 112, 256, 576 = 24² — and the near-pencil determinants (n − 1)²: 4, 9, 16, 25, 36. The linear-space census on [4] finds exactly 5 spaces with line counts [4, 4, 4, 4, 6] — four near-pencils (N = n, de Bruijn–Erdős tight) and the affine plane AG(2,2) (N = 6 > n). The Frankl–Wilson tuples: FW(2,5,3) — 10 vertices, ω = 4, α = 2, caps 6/5, not degenerate; FW(3,7,4) — 35 vertices, ω = 15, α = 2, caps 29/7; FW(3,7,5) — 21 vertices and the graph is complete (ω = 21 = N, α = 1): among 5-subset intersections mod 3 the forbidden residue 2 never occurs, the degeneracy flag reads True — the K₂₁ non-example of the §3.5 checkpoint, live.

### Part 2 — The friendship census (n = 3 … 7), Claim 1 diagnostic, and W₂ walk matrix

```python
from itertools import combinations

def double_fact(k):
    res = 1
    for x in range(k, 0, -2):
        res *= x
    return res

def windmill_formula(n):
    if n < 3 or n % 2 == 0:
        return 0
    if n == 3:
        return 1                   # K_3 has all 3 vertices universal (1 labeled graph, not 3*1!!)
    return n * double_fact(n - 2)  # unique hub (n ways) * blade matching ((n-2)!! ways)

def is_friendship(n, adj):
    if n < 3:
        return False               # guard n < 3 (rules out vacuous K_1 at n = 1)
    for u in range(n):
        au = adj[u]
        for v in range(u + 1, n):
            if (au & adj[v]).bit_count() != 1:
                return False
    return True

def cn(adj, u, v):
    mask = adj[u] & adj[v]
    return (mask & -mask).bit_length() - 1

nonadj_graphs, nonadj_pairs, naive_fails, excised_ok = 0, 0, 0, 0

for n in range(1, 8):
    count = 0
    if n >= 3:
        for mask in range(1 << (n * (n - 1) // 2)):
            adj = [0] * n
            e = 0
            for u in range(n):
                for v in range(u + 1, n):
                    if (mask >> e) & 1:
                        adj[u] |= 1 << v
                        adj[v] |= 1 << u
                    e += 1
            if is_friendship(n, adj):
                count += 1
                degs = [adj[u].bit_count() for u in range(n)]
                assert (n - 1) in degs  # universal vertex exists (Claim 2)
                has_nonadj = False
                for x, y in combinations(range(n), 2):
                    if not ((adj[x] >> y) & 1):
                        has_nonadj = True
                        nonadj_pairs += 1
                        assert degs[x] == degs[y]  # Claim 1
                        z = cn(adj, x, y)
                        u0, v0 = cn(adj, x, z), cn(adj, y, z)
                        if cn(adj, u0, y) == z:
                            naive_fails += 1
                        dom = [u for u in range(n) if ((adj[x] >> u) & 1) and u not in (z, u0)]
                        cod = {v for v in range(n) if ((adj[y] >> v) & 1) and v not in (z, v0)}
                        img = {cn(adj, u, y) for u in dom}
                        if img == cod and len(img) == len(dom):
                            excised_ok += 1
                if has_nonadj:
                    nonadj_graphs += 1
    assert count == windmill_formula(n)
    if n >= 3:
        print(f"n={n}: count={count} (formula={windmill_formula(n)})")

print(f"Claim 1 diagnostic: {nonadj_graphs} graphs with non-adjacent pairs, "
      f"{nonadj_pairs} pairs; naive fails={naive_fails}, excised bijections={excised_ok}")

# Verify A^2 = J + (D - I) on W_2 (hub 0, blades {1,2} and {3,4})
W2 = [
    [0, 1, 1, 1, 1],
    [1, 0, 1, 0, 0],
    [1, 1, 0, 0, 0],
    [1, 0, 0, 0, 1],
    [1, 0, 0, 1, 0],
]
A2 = [[sum(W2[i][k] * W2[k][j] for k in range(5)) for j in range(5)] for i in range(5)]
for row in A2:
    print(row)
```

**Verified output.**

```
n=3: count=1 (formula=1)
n=4: count=0 (formula=0)
n=5: count=15 (formula=15)
n=6: count=0 (formula=0)
n=7: count=105 (formula=105)
Claim 1 diagnostic: 120 graphs with non-adjacent pairs, 1320 pairs; naive fails=1320, excised bijections=1320
[4, 1, 1, 1, 1]
[1, 2, 1, 1, 1]
[1, 1, 2, 1, 1]
[1, 1, 1, 2, 1]
[1, 1, 1, 1, 2]
```

Every counted graph is a windmill with a universal hub (the census asserts Claim 2's universal vertex and Claim 1's equal degrees graph by graph), and the counts match the honest formula — 1 for n = 3 and n(n−2)!! for odd n ≥ 5: 5·3!! = 15, 7·5!! = 105; the 2k+1 parity is visible in the zeros. The Claim 1 diagnostic runs the common-neighbor map both ways across all 1,320 non-adjacent pairs of the 120 census graphs that have them: the naive un-excisioned map α: N(x)∖{z} → N(y)∖{z} fails in every single pair (α(u) = z is generic), while the excised bijection N(x)∖{z, u_0} → N(y)∖{z, v_0} verifies on every pair. And the matrix equation of §4.4, entry by entry on W_2 (hub 0, blades (1,2), (3,4)): A² = J + (D − I) — diagonal = degrees (4, 2, 2, 2, 2), every off-diagonal entry = 1. The diagonal is *not* constant — the graph is not regular — exactly the case the spectral lemma handles by exclusion.

## Answers to the Exercises

**A1.** The four 3-subsets of [4] — {1,2,3}, {1,2,4}, {1,3,4}, {2,3,4} — have odd sizes (3) and pairwise intersections of size 2 (even): an Oddtown of size 4 = n. No fifth set can join: five characteristic vectors in F₂⁴ cannot be independent (L2.1's argument caps the family at n = 4), and any family of five would have to be. Machine check: exhaustive census — maximum Oddtown size 3 on [3], 4 on [4]; the exhibited family is extremal.

**A2.** Over F₂ every vector of the family has even self-product (sizes even) and even cross-products (intersections even): all pairwise products vanish. For x = Σa_iv_i and y = Σb_jv_j in the span W: x·y = Σ_{i,j}a_ib_j(v_i·v_j) = 0. So W ⊆ W⊥, giving dim W ≤ n/2, and the family injects into W: |F| ≤ 2^{dim W} ≤ 2^{⌊n/2⌋}. Sharp: partition [n] into pairs and take all 2^{⌊n/2⌋} unions. Machine check: census maxima 2 on [3] and 4 on [4] — both exactly the formula.

**A3.** (a) The Gram matrix G = VVᵀ has diagonal entries |A_i| — odd — and off-diagonal entries |A_i ∩ A_j| — even: G ≡ I_m (mod 2). The determinant is an integer polynomial in the entries, so det G ≡ det I_m = 1 (mod 2): the determinant is an odd integer, in particular nonzero. Thus G is nonsingular over F₂ (and every field of characteristic 2) as well as over ℚ and ℝ (and every field of characteristic 0) — though not necessarily over F_p for an odd prime p dividing det G, as the det G = 9 ≡ 0 (mod 3) extremal family in the machine check below illustrates. Working over ℚ, m = rank G ≤ rank V ≤ n. (b) Eventown: all sizes and intersections are even, so G ≡ 0 (mod 2) — the mod-2 determinant congruence returns 0 ≡ 0 and certifies nothing. Over ℚ the Gram rank argument fails honestly: the pairing family A_1 = {1,2}, A_2 = {3,4}, A_3 = {1,2,3,4} on [4] has Gram [[2,0,2],[0,2,2],[2,2,4]], whose third row is the sum of the first two — det G = 0, singular, for a perfectly legal Eventown of size 3 (or 4 if ∅ is included). The step of the mod-2 proof with no rational analogue is self-orthogonality (W ⊆ W⊥): over F₂, v·v = |A| ≡ 0 (mod 2) is possible for v ≠ 0, whereas over ℚ the standard inner product is positive definite (⟨x, x⟩ > 0 for every x ≠ 0), so W ∩ W⊥ = {0} and no nonzero subspace can sit inside its own orthogonal complement. Eventown's 2^{⌊n/2⌋} is genuinely a characteristic-2 theorem, while Oddtown's n works in every field. That is the real content of the comparison. ∎ Machine check: across all 34 Oddtown families on [4], every Gram determinant is odd and nonzero, with maximum size 4 attained by the four singletons (G = I₄, det G = 1) and the four triples of Exercise 1 (G = I₄ + 2J₄, det G = 9 — singular over F₃, nonsingular over every field of characteristic ≠ 3); the Eventown witness has det G = 0 and rank G = 2.

**A4.** The weighted intersection matrix G = (⟨A_i, A_j⟩) is ΛJ + D with D = diag(⟨A_1, A_1⟩ − Λ, …, ⟨A_m, A_m⟩ − Λ), whose diagonal entries are strictly positive by hypothesis. Since Λ > 0 as well, the determinant lemma of L1.2 prices det G = Π_{i=1}^m (⟨A_i, A_i⟩ − Λ) · (1 + Λ Σ_{i=1}^m 1/(⟨A_i, A_i⟩ − Λ)) > 0, and every leading principal minor is likewise positive: G is positive definite, hence nonsingular (rank G = m). Meanwhile G = V W Vᵀ, where V is the m × n incidence matrix and W = diag(w_1, …, w_n), so m = rank G = rank(VWVᵀ) ≤ rank V ≤ n. ∎ The audit: read the proof again — it never touches the individual weights w_i except through their aggregated sums ⟨A_i, A_j⟩. All it consumes is the matrix pattern: constant off-diagonal Λ > 0 and diagonal entries strictly larger. The weights can be arbitrary real numbers, negative or zero included — G = ΛJ + D with D ≻ 0 and Λ > 0 is positive definite regardless of how the entries were manufactured from W, and rank(VWVᵀ) ≤ rank V ≤ n holds for every n × n matrix W. Positivity of the w_i buys the interpretation of ⟨·,·⟩ as a genuine inner product on ℝⁿ, not the bound; integrality was never invited. Machine check: the triangle family {1,2}, {2,3}, {1,3} with weights w_1 = w_2 = w_3 = a > 0 (a fourth point weighted b, unused) has Λ = a and G = a(I + J₃), determinant 4a³ — verified across sampled (a, b); the lemma's formula matched direct elimination on 120 random instances (k = 2 … 7, exact integer arithmetic); and the census hunted for violations under mixed-sign weight vectors on [4] (e.g. (3, −2, 5, −1)): every constant-Λ > 0 family with all weighted sizes > Λ still has m ≤ 4 — zero exceptions.

**A5.** The Fano plane has seven lines of size 3 with pairwise intersections exactly 1, so its Gram matrix is M = J + 2I. Its eigenvalues are 2 (multiplicity 6, on 𝟙⊥) and 2 + 7 = 9 (multiplicity 1, on 𝟙), giving det M = 2⁶·9 = **576** = 24². The determinant lemma of L1.2 agrees: det(D)(1 + λΣ1/d_i) with D = 2I₇, λ = 1, gives 2⁷(1 + 7/2) = 128·4.5 = 576. Sylvester's leading principal minors — det(2I_k + J_k) = 2^{k−1}(k + 2) for k = 1, …, 7, namely 3, 8, 20, 48, 112, 256, 576 — are all strictly positive, certifying positive definiteness (hence rank M = 7 = m) without writing a quadratic form; the eigenvalue computation certifies the same thing and prices the determinant. Fisher: m = n = 7, tight.

**A6.** Over F₃: v_i·v_i = |A_i| ≡ 1 ≠ 0 and v_i·v_j ≡ 0 for i ≠ j. Dotting a dependence Σc_iv_i = 0 with v_j leaves c_j·1 = 0, i.e. c_j = 0 in F₃ — the L2.1 argument survives verbatim because its only ingredients were "self-products nonzero, cross-products zero", and 1 ≠ 0 holds in every field. So m ≤ n. (The general statement: sizes ≡ k ≢ 0 mod p, intersections ≡ 0 mod p ⇒ m ≤ n, any prime.) Census on [4]: maximum 4, attained by the singletons {1}, {2}, {3}, {4} — sizes 1 ≡ 1 mod 3, intersections 0.

**A7.** Let z be the unique common neighbor of the non-adjacent x, y. The trap first: sending each u ∈ N(x)∖{z} to the common neighbor α(u) of the pair (u, y) does **not** land in N(y)∖{z}, because α(u) = z is possible — generic, even: in W₂ with x = a_1, y = a_2, u = b_1, the pair (u, y) has common neighbor the hub, which is z. The repair excises one vertex from each side, and the excised vertices are forced. Exactly one member of N(x)∖{z} is adjacent to z: at most one, else the pair (x, z) has two common neighbors; at least one, namely u_0 = cn(x, z). Mirror-wise, v_0 = cn(y, z) is the unique z-adjacent member of N(y)∖{z}. For u ∈ N(x)∖{z, u_0}: u ≁ y, else u would be a second common neighbor of x and y — so the pair (u, y) has its unique common neighbor α(u), and α(u) ≠ z (z ≁ u, u_0 being the unique z-adjacent member of N(x)∖{z}), α(u) ≠ x (x ≁ y), and α(u) ≠ v_0 (else the pair (u, z) has the two common neighbors x and v_0, distinct because x ≁ y while v_0 ~ y). If α(u_1) = α(u_2) = w with u_1 ≠ u_2, then w and x are two distinct common neighbors of the pair (u_1, u_2) — w ≠ x because x ≁ y while w ~ y. Contradiction: α is injective from N(x)∖{z, u_0} into N(y)∖{z, v_0}, giving d(x) − 2 ≤ d(y) − 2; the mirror argument reverses it, and d(x) = d(y). Contrapositive: distinct degrees ⇒ adjacency. Machine check: the claim verified in all 121 friendship graphs of the n = 3 … 7 census — with the diagnostic run both ways: the un-excisioned codomain claim fails in all 120 graphs that have non-adjacent pairs (α(u) = z occurring in every one of the 1,320 pairs), while the u_0/v_0 excision verifies on every pair.

**A8.** When every |A_i| > λ, the Gram matrix G = λJ + D has D = diag(|A_1| − λ, …, |A_m| − λ) ≻ 0, and the determinant lemma of L1.2 prices det G = Π_{i=1}^m (|A_i| − λ) · (1 + λ Σ_{i=1}^m 1/(|A_i| − λ)) > 0. Since G = VVᵀ for the m × n incidence matrix V, m = rank G ≤ rank V ≤ n. *The audit when |A_i| = λ is permitted:* first, at most one set in the family can have size λ — if |A_1| = |A_2| = λ, then |A_1 ∩ A_2| = λ forces A_1 = A_2, contradicting distinctness. Second, if |A_1| = λ and |A_i| > λ for i ≥ 2, then d_1 = |A_1| − λ = 0, so D is singular and the factored form Π_i d_i(1 + λΣ_i 1/d_i) hits a division by zero in 1/d_1 — though expanding the product before dividing gives λΠ_{i≥2} d_i > 0, so G is actually still nonsingular. Even simpler, the combinatorial patch bypasses matrices altogether when |A_1| = λ: since |A_1 ∩ A_j| = λ = |A_1| for every j ≥ 2, we have A_1 ⊆ A_j for all j ≥ 2. Therefore the m − 1 remainder sets B_j = A_j ∖ A_1 ⊆ [n] ∖ A_1 (j = 2, …, m) are nonempty (as |A_j| > λ) and pairwise disjoint (since B_i ∩ B_j = (A_i ∩ A_j) ∖ A_1 = A_1 ∖ A_1 = ∅). At most n − λ nonempty pairwise disjoint sets fit inside [n] ∖ A_1, so m − 1 ≤ n − λ, giving m ≤ n − λ + 1 ≤ n (since λ ≥ 1). Sharpness: the near-pencil on [n] (n ≥ 3) — the n − 1 pairs {1, i} for i = 2, …, n together with {2, …, n} — has λ = 1, m = n, and det G = 1^{n−1}(n − 2)(1 + (n − 1)/1 + 1/(n − 2)) = (n − 1)² (4, 9, 16, 25, 36 for n = 3 … 7); the Fano plane has λ = 1, m = n = 7, det G = 576 (Exercise 5's matrix). Machine check: the exhaustive census of all 65,536 subfamilies of 2^[4] — every constant-λ family (λ ≥ 1) with all sizes > λ has m ≤ 4, the maximum 4 attained by exactly five families (the four near-pencil labelings and the four triples of Exercise 1); relaxing the strictness to ≥ λ leaves the maximum at 4, confirming the patch; near-pencil Gram determinants (n − 1)² = 4, 9, 16, 25, 36 for n = 3 … 7 and the Fano 576, each verified against the lemma's formula and by direct elimination.

**A9.** Three families of eigenvectors. (i) (1, −1) supported on the two vertices of blade i (hub 0): A maps it to −1 times itself — the blade partner is its only non-hub neighbor and the hub coordinate picks up 0: eigenvalue **−1**, one per blade, t in all. (ii) (1, 1) on blade i minus (1, 1) on blade j (hub 0): the hub coordinate stays 0 (contributions cancel), each blade vertex's entry becomes its blade partner's 1: eigenvalue **1**, t − 1 in all. (iii) The remaining 2 dimensions: the equitable partition {hub} ∪ {symmetrized blades} has quotient [[0, 2t], [1, 1]] (hub adjacent to 2 vertices per blade; a blade vertex adjacent to hub plus one in-blade neighbor): characteristic polynomial λ² − λ − 2t, so the last two eigenvalues are **(1 ± √(1+8t))/2**. Total count: t + (t−1) + 2 = 2t + 1 = n ✓, trace 0 ✓. W₂: {(1±√17)/2, 1, −1, −1} ✓; W₃: {3, 1, 1, −1, −1, −1, −2} ✓ — both verified by direct machine computation of the spectra.

**A10.** Multiply each column j of H by H_{1j} ∈ {±1}; this leaves HHᵀ = nI unchanged (since (HD)(HD)ᵀ = HD²Hᵀ = HHᵀ) and makes row 1 all +1s. Since n ≥ 3, rows 2 and 3 exist and are orthogonal to row 1 and to each other. Census the n columns by the ordered sign pair (row-2 sign, row-3 sign): a columns (+,+), b (+,−), c (−,+), d (−,−) — four patterns, every column in exactly one. Now count the same columns four ways. Total: a + b + c + d = n. Orthogonality of rows 1 and 2: (a + b) − (c + d) = 0, so a + b = n/2. Orthogonality of rows 1 and 3: (a + c) − (b + d) = 0, so a + c = n/2. Orthogonality of rows 2 and 3: (a + d) − (b + c) = 0, so a + d = b + c. From a + b = a + c = n/2 we get b = c; then 2b = b + c = n/2, so n = 4b is a multiple of 4 — and back-substituting, a = b = c = d = n/4, every sign pattern occupying exactly a quarter of the columns. Orders 1 and 2 are the trivial exceptions (H₁ = [1]; H₂ exists), so from n = 3 on, 4 | n — and in particular no Hadamard matrix of order 3 exists (nor of any order ≡ 2 mod 4). ∎ Machine check: Sylvester's recursion [[H, H], [H, −H]] produces H₂, H₄, H₈ with HHᵀ = nI; Paley's construction at q = 11 (quadratic residues {1, 3, 4, 5, 9} mod 11) produces H₁₂ with HHᵀ = 12I; the three-row census on H₄, H₈, H₁₂ returns a = b = c = d = n/4 exactly; and the exhaustive sweep of all 512 sign matrices of order 3 finds none with orthogonal rows.

**A11.** *Partition lower bound.* Suppose the edges of K_n are partitioned into complete bipartite graphs K_{A_i, B_i}, i = 1 … r. Discarding any empty bicliques, we may assume |A_i| ≥ 1 and |B_i| ≥ 1 for all i. The partition says: each unordered pair is separated by exactly one biclique, i.e. Σ_i (a_ib_iᵀ + b_ia_iᵀ) = J − I (a_i = 1_{A_i} etc.). For x ∈ V = 𝟙⊥: xᵀ(J−I)x = −||x||², so **Σ_i 2 s_{A_i}s_{B_i} = −||x||²**, where s_A(x) = Σ_{u∈A}x_u. Now the vectors z_i = |B_i|a_i − |A_i|b_i lie in V (z_i·𝟙 = |A_i||B_i| − |A_i||B_i| = 0). Since dim V = n − 1, if r ≤ n − 2 there exists a nonzero x ∈ V orthogonal to every z_i. Orthogonality reads |B_i|s_{A_i} = |A_i|s_{B_i}, and since |A_i|, |B_i| ≥ 1, s_{A_i}s_{B_i} = (|B_i|/|A_i|)s_{A_i}² ≥ 0 for every i. Summing: −||x||²/2 = Σ_i s_{A_i}s_{B_i} ≥ 0 — forcing x = 0, a contradiction. So r ≥ n − 1, and the staircase {i} | {i+1, …, n}, i = 1 … n−1, partitions K_n into exactly n − 1 bicliques: tight. ∎ *Cover upper bound.* Give vertex v the binary address of v−1 in ⌈log₂n⌉ bits, and let biclique i take A = addresses with bit i equal to 0, B = bit i equal to 1: every edge has differing addresses, hence differing bits somewhere, and is covered — ⌈log₂n⌉ bicliques suffice (they overlap; that is the difference between a cover and a partition). Machine check, exhaustive: minimum partition sizes for n = 3, 4, 5 are 2, 3, 4 = n − 1 (no partition with n − 2 exists; the staircase attains), while minimum cover sizes are 2, 2, 3 = ⌈log₂n⌉ — the partition/cover gap is real and machine-confirmed.

**A12.** Since |A △ B| = |A| + |B| − 2|A ∩ B| ≡ |A| + |B| (mod 2), the condition that all pairwise symmetric differences are even forces |A_i| ≡ |A_j| (mod 2) for all i, j: every set in the family has one fixed size parity c ∈ {0, 1}. For n ≥ 1 the binomial identity Σ_{k=0}^n (−1)^k C(n, k) = (1 − 1)^n = 0 shows that [n] has equally many even-sized and odd-sized subsets, namely 2^{n−1} of each. So the family is contained in a single parity class {A ⊆ [n] : |A| ≡ c}, which has exactly 2^{n−1} members: |F| ≤ 2^{n−1}, attained sharply by taking the whole class. Machine check: census maximum on [4] is 8 = 2³, attained by all odd (or all even) sets. Note the three parities of L2 in a table: odd sizes/even intersections ⇒ n; all even ⇒ 2^{⌊n/2⌋}; even differences ⇒ 2^{n−1}.

**A13.** The vertices of G are the C(5,3) = 10 three-subsets of [5], with A ~ B iff |A ∩ B| = 2. Complementing each 3-subset, A ↦ Ā = [5] ∖ A, is a bijection onto the C(5,2) = 10 two-subsets of [5], with |Ā ∩ B̄| = 5 − |A ∪ B| = 5 − (6 − |A ∩ B|) = |A ∩ B| − 1. Thus A ~ B (|A ∩ B| = 2) iff |Ā ∩ B̄| = 1: the graph is the line graph L(K₅) — the **complement of the Petersen graph** KG(5,2) (where 2-subsets are adjacent iff they are disjoint). *Proof that ω(G) = 4:* by the complementation bijection, a clique in G is a family of 2-subsets of [5] (edges of K₅) pairwise intersecting in 1 vertex. If a clique has ≥ 2 edges, say e_1 = {a, b} and e_2 = {a, c} (b ≠ c), then every other edge in the clique must intersect both: either it contains a, or it is e_3 = {b, c}. If {b, c} is in the clique, no fourth edge can intersect all three of {a, b}, {a, c}, {b, c} (a 2-subset meeting all three must contain at least two of a, b, c, hence equal one of them), so a triangle of K₅ gives a clique of size 3. If {b, c} is not in the clique, every edge in the clique contains a — a star centered at a, of size at most 4 (the four pairs {a, x}, x ∈ [5] ∖ {a}). So ω(G) = 4, and the maximum cliques are exactly the five stars, i.e. the families {T : a ∉ T} of all four 3-subsets of a fixed 4-subset [5] ∖ {a}. *Proof that α(G) = 2:* an independent set in G corresponds to a family of pairwise disjoint 2-subsets of [5]; since 2·3 = 6 > 5, at most ⌊5/2⌋ = 2 fit, and {{1,2}, {3,4}} achieves 2. The theoretical caps — Frankl–Wilson Σ_{i≤1}C(5,i) = 6 for ω and RCW C(5,1) = 5 for α — are valid upper bounds, honest but loose at this scale (4 ≤ 6, 2 ≤ 5). ∎ Machine check: exhaustive census — ω = 4 with the maximum cliques exactly the five families "all triples of a fixed 4-set", α = 2 with zero independent triples; the complement identified as the Petersen graph (15 edges, 3-regular, girth 5).

**A14.** The tool: RCW with k = 3, L = {0, 1} caps the family at C(6, 2) = 15 — true but far from sharp. The truth is **4**. Any two blocks of the family share at most one point, so each pair of points lies in at most one block: counting pairs, 3·|F| ≤ C(6,2) = 15, giving |F| ≤ 5. If |F| = 5, every pair of points lies in exactly one block — a Steiner system S(2, 3, 6); but each point would then lie in (6−1)/(3−1) = 5/2 blocks, not an integer — impossible (equivalently: S(2,3,v) needs v ≡ 1, 3 mod 6). So |F| ≤ 4, and 4 is attained: {1,2,3}, {1,4,5}, {2,4,6}, {3,5,6} — pairwise intersections exactly 1. Machine check: exhaustive census maximum is 4, and this family is extremal. Lesson: RCW's bound is general-purpose, not tight — when it leaves a gap, plain pair-counting plus divisibility may close it.

**A15.** A linear space on {1,2,3,4}: any two points on exactly one line; lines of size ≥ 2; not all points on one line. If some line has 3 points, say {1,2,3}: the pairs with 4 need lines {1,4}, {2,4}, {3,4} (any larger line through 4 would create a second line through a pair already on the 3-line), and {1,2,3} must be a line — the near-pencil; 4 choices of the excluded point. If no line has 3 points, every pair is its own line: the affine plane AG(2,2) — 1 more. Total: **5** labeled spaces (4 near-pencils + 1 affine plane). The 4 near-pencils have N = 4 = n — de Bruijn–Erdős tight at n = 4 — while the affine plane has N = 6 > 4 = n; all five satisfy N ≥ n, the census the ✎ checkpoint of L1.3 promised. Machine check: brute-force enumeration of all set systems on 4 points finds exactly these five, with line counts [4, 4, 4, 4, 6].

**A16.** In the Petersen graph KG(5,2), vertices are the 2-subsets of [5] and edges join disjoint pairs, so an independent set in KG(5,2) is a clique in its complement L(K₅) — namely, a family I of 2-subsets of [5] that pairwise intersect. By the exact case analysis proved in A13 (every pairwise-intersecting family of edges of K₅ is either contained in a triangle K₃ — size at most 3 — or in a star — size at most 4), α(KG(5,2)) = 4, and the independent sets attaining it are precisely the **five stars** S_a = {all 2-subsets of [5] containing a}, a = 1, …, 5. ∎ Machine check: exhaustive enumeration — α = 4, exactly 5 maximum independent sets, the stars.

---

## Revision History & Verification Notes

**Editions.** Reference edition (five problem families: Fisher/de Bruijn–Erdős, Oddtown/Eventown, friendship, spectral Mantel, expander-mixing; one verified lab) → **Feynman lecture edition** (this edition): 8 lectures. Everything from the reference canon is preserved inside the narrative, and the flagged sketches are now complete proofs: Bose's polynomial method in full (L1), the Frankl–Wilson theory in full — multilinear lemma, RCW with the slice trick, the Fermat-polynomial theorem, two worked Ramsey graphs (L3) — the friendship theorem's equal-degree brick reconstructed in full (L4, Claims 1–2), spectral Turán via Motzkin–Straus (L6), and the two-distance capstone (L7) which is entirely new to the chapter. The canon-audit additions are installed as Lecture 8 — interlacing (unifying L4–L6 retroactively), the Hoffman bounds, Lovász theta with θ(C₅) = √5 and the capacity Θ(C₅) = √5, and Delsarte's linear program with four LP-exact code bounds. The full Atlas exercise standard is installed (tiers, ◆ pattern-unknown, ◐ Explorations, worked answers, this appendix), the lab is rebuilt in five verified parts, and four figures are embedded (windmill W₄; the Motzkin–Straus merge walk on the paw; pentagon + octahedron witnesses; Lovász's umbrella). **Restructure (session 37).** The chapter slimmed from eight lectures to four: the four spectral lectures (eigenvalues as averaging machines, Motzkin–Straus and spectral Turán, two-distance sets, the modern toolkit) moved verbatim — with their exercises, worked answers, lab Parts 3–5, and three of the four figures — into the new Chapter 8, *Spectral Methods and the Modern Toolkit*; this file is now the four-lecture linear-algebraic core (Fisher, Oddtown/Eventown, the polynomial method, friendship), and exercise and lab numbering were re-set accordingly: 13 exercises (9 graded + 3 ◆ + 1 ◐), 12 worked answers, lab in two parts. The session-64 adversarial review then audited the whole chapter with a fresh machine battery — one load-bearing proof repair (Claim 1's common-neighbor map, with its A5 mirror) and four record-level fixes, the mathematics otherwise untouched (the review record below).

**Corrections during the rewrite (verification-pass honesty).** Three working errors were caught by the machine before anything was installed: (1) the near-pencil Fisher Gram determinant computes to **9** (determinant lemma: 2·(1 + 1/2 + 1 + 1 + 1)), not the 7 an early working note expected — the checkpoint in L1.2 now records the computation; (2) the first choice of worked Frankl–Wilson Ramsey instance, p = 3, m = 7, k = 5, is **degenerate** (all intersections fall in residues 0, 1 mod 3, never the forbidden 2 — the "graph" is K₂₁); the worked example switched to k = 4 (35 vertices) and the degeneracy became the L3.5 checkpoint lesson; (3) the equidistant lemma was first drafted with the non-centered Gram (δ²/2)(J + I) — positive definite, det(J_k+I_k) = k + 1, rank k — the wrong matrix, since the hypothesis does not place the points at equal norm from the origin; the installed proof centers first, and the failed shortcut survives as a checkpoint in Chapter 8's two-distance lecture. One honest gap is recorded rather than hidden: RCW's bound C(6,2) = 15 for 3-subsets of [6] with intersections in {0,1} is far from the true maximum 4 (A◆1).

**Canon-coverage audit (executed).** A standing Atlas goal is auditing each chapter against the broader canon. This chapter's audit produced four proposals — the **Hoffman bound**, **Lovász theta**, the **Delsarte LP**, and **eigenvalue interlacing** — which were approved and installed as Lecture 8 of the eight-lecture edition; after the session-37 restructure that lecture lives in Chapter 8 (Spectral Methods and the Modern Toolkit), with the connections the audit predicted: interlacing explains retroactively why the spectral moves of the lectures that moved there were legal (the unification note in Chapter 8's interlacing section), Hoffman extends spectral averaging into a quantitative independence cap, and theta and Delsarte continue the polynomial method into semidefinite and linear programming. The audit's citation decisions already implemented: the sharp general s-distance bound C(d+s,s) is cited (Bannai–Bannai–Stanton 1983; Petrov–Pohoata 2019) while the elementary C(d+s+1,s) is proved — a two-distance-lecture decision that travelled to Chapter 8 with that lecture, as did the cited m(d) table and the flagged Larman–Rogers–Seidel integrality phenomenon (n > 2d + 3); the Frankl–Wilson Ramsey corollary (quasipolynomial R(k,k) ≥ exp(c·log²k/log log k), improved only in 2006 by Barak–Rao–Shaltiel–Wigderson) is cited, not proven, in Lecture 3. The toolkit lecture's own citations: theta's multiplicativity under the strong product and Θ(C₅) = √5 (Lovász 1979); the perfect-graph collapse θ = α = χ(Ḡ); A(8,3) = 20 by the shortened Hamming code, cited literature against the LP's honest 128/5.

**Figures.** One figure is embedded as fenced SVG at its lecture location per the dual-presentation convention (prose and lab code stay terminal-portable): Figure 1 (Lecture 4), redesigned as two panels in the expansion pass — panel A the windmill W₄ (hub and eight blade vertices at computed coordinates, all three pair types annotated), panel B the deletion assembly H = G − u (dashed deleted spokes, the solid red perfect matching, and the forbidden isolated vertex z with the (z, u) pair it would strand); its data and geometry machine-verified before drawing (the windmill's pair checks; node separation, bounds, and every text claim cross-checked). The earlier edition's Figures 2–4 (the paw's Motzkin–Straus walk, the pentagon + octahedron two-distance witnesses, Lovász's umbrella for C₅) moved with their lectures to Chapter 8.

**Verification record (all deterministic, exhaustive where feasible; the Python labs above are the reader's runnable copies of the same logic — the eight-lecture edition's lab Parts 3–5 also ran here, and their runnable code moved to Chapter 8 with the spectral lectures).** Fisher: Fano Gram 2I + J, det 576, Sylvester minors 3, 8, 20, 48, 112, 256, 576; Bose evaluation matrices — Fano 2I det 128, near-pencil diag(2,1,1,1) det 2; near-pencil Gram det 9 (determinant lemma, cross-checked); 4-point linear-space census: exactly 5 (4 near-pencils + 1 affine plane). Parity families: Oddtown max 3 on [3], 4 on [4]; Eventown 2 and 4 (= 2^{⌊n/2⌋}); F₃ analogue max 4 on [4] (singletons); △-even max 8 on [4] (= 2^{n−1}); the n = 6 pairwise-even 3-set family max 4 (witness the four {x, 5, 6}), against FW's cap 7 and the F₂-orthogonality cap 6. RCW n = 6, k = 3: maxima 4 / 4 / 10 for L = {0,1} / {0,2} / {1,2} (cap 15; the {1,2} case's 10 = all triples through a fixed point). Ramsey graphs: p = 2, m = 5, k = 3 — 10 vertices, ω = 4, α = 2, caps 6/5, identified as Petersen's complement; p = 3, m = 7, k = 4 — 35 vertices, ω = 15, α = 2, caps 29/7; p = 3, m = 7, k = 5 degenerate (K₂₁). Graham–Pollak: minimum partition = n − 1 for n = 3, 4, 5 (staircase attains; no n − 2 partition exists), minimum cover = ⌈log₂n⌉ = 2, 2, 3 — the z_i-span proof of A7 machine-confirmed on all three censuses. Friendship: census 1, 0, 15, 0, 105 for n = 3…7, all windmills, Claim 1 in all, counts = n·(n−2)!! at n = 5 and n = 7 (at n = 3 the formula's 3·1!! = 3 hub-plus-matching descriptions all describe the same labeled K₃ — the formula's lone exception, the triangle being the one windmill whose three hub choices coincide); W₂/W₃ satisfy A² = J + (D − I) exactly, triangle A² = I + J with det A = 2; spectra W₂ = {(1±√17)/2, 1, −1, −1}, W₃ = {3, 1, 1, −1, −1, −1, −2}. Spectral: Jacobi validated on K_{2,3} {√6, 0, 0, 0, −√6}, C₅ {2, 0.618×2, −1.618×2}, Petersen {3, 1⁵, −2⁴}; Mantel lemmas on every triangle-free graph with n = 5, 6; spectral Turán λ1 ≤ (1−1/ω)n on all 33,792 graphs with n = 5, 6, K_{3,3} equality λ1 = 3; expander-mixing sharp form over all disjoint S, T — Petersen (μ = 2) and K_{3,3} (μ = 3, the −d degeneracy) tight, C₅ slack (max ratio 4/3 < μ = φ). Motzkin–Straus detector: all 64 graphs on 4 vertices, 1/40 mesh (12,341 lattice points) — never above (1−1/ω)/2, 42 attainments (integrality of 1600·(1−1/ω)/2 for ω = 1, 2, 4); all 1,024 graphs on 5 vertices, 1/10 mesh (1,001 points) plus 200 LCG randoms each — never above. Two-distance: centered Gram spectrum {1×(k−1), 0} and det(J_k+I_k) = k+1 for k = 2…9; simplex w_i = e_i − 𝟙/k pairwise distance² = 2, norms² = (k−1)/k; dimension identities Σ_q C(d+s−q, s−q) = C(d+s+1, s) and the spherical alternating sum, d ≤ 6, s ≤ 4; witnesses — pentagon squared distances {1.38197, 3.61803} with evaluation rank 5 (spherical dim 5: tight), octahedron {2, 4} rank 6 (spherical 9, paraboloid 15), {0,1,2} rank 3 (paraboloid dim 6); spherical quotient monomial ranks: circle deg ≤ 2 → 5, deg ≤ 1 → 3; sphere deg ≤ 2 → 9, deg ≤ 1 → 4, deg ≤ 3 → 16. Grid censuses: {0…8} max 3; 7×7 grid — no 5-subset two-distance (all C(49,5) = 1,906,884), 4 attained by the square {4, 8}; 3×3×3 — no 7-subset (all C(27,7) = 888,030), 6 attained by the octahedron {2, 4}. Lecture 8: interlacing — 23/23 fixed-seed (987654321) random compression trials; windmill quotients [[0, 2t], [1, 1]] with spectra inside the full Jacobi spectra (W₂ {(1±√17)/2}, W₃ {3, −2}); inertia bound — all 1,099 graphs with n ≤ 5, zero violations, 633 tight on the n − p side (954 on n − q, 966 on the combined min side; Petersen n − p = 4 = α, C₅ n − p = 2 = α); Hoffman — all 1,122 d-regular graphs with n = 4…7 and λ_n < 0 ({7, 13, 171, 931} by n), zero violations, 225 tight (7/7, 1/13, 111/171, 106/931); Petersen star equality ⟨𝟙_S,𝟙_S⟩_M = 8, ⟨𝟙_S,𝟙⟩_M = 20, ⟨𝟙,𝟙⟩_M = 50, 8·50 = 400 = 20², with M𝟙_S = 2𝟙 and M𝟙 = 5𝟙; cocktail party K₆∖3K₂ spectrum {4, 0³, −2²}, bound 2 tight; chromatic bound — all 191 d-regular graphs with n = 4…6, zero violations, quotient chain (tr B = 0, μ_1 = d, Σ_{i≥2}μ_i = −d ≥ (k−1)λ_n) verified 191/191; theta — umbrella distance-2 products ≤ 1.7 × 10⁻¹⁶, edge products (√5−1)/2 = 1/φ exactly, value 1/cos²ψ = √5; circulant certificate eigenvalues {√5/5, (5−√5)/10 ×2, 0 ×2}, tr = 1, J•X = √5 to 10⁻¹²; strong product — 0 independent 6-subsets of the C(25,6) = 177,100, exactly 10 independent 5-sets, diagonal {(i, 2i mod 5)} independent; Delsarte — Krawtchouk's two definitions agree for n = 5…8, all (i, k); the [7,4] Hamming code — 16 words, min 3, ordered pair counts [16, 0, 0, 112, 112, 0, 0, 16], Delsarte sums [256, 0, 0, 0, 1792, 0, 0, 0]; [7,3] simplex — 8 words, all nonzero weights 4; [8,4] extended — 16 words, min 4; [6,3] punctured simplex — 8 words, min 3; ten exact-fraction certificates valid ((5,3), (6,3), (7,3), (7,4), (8,4), (8,5), (6,4), (4,4), (5,5), (6,5)); Plotkin 29/29 (2 ≤ n ≤ 10, 2d > n); the LP solved exactly (BigInt vertex enumeration, primal and dual) on all 16 instances — (4,2) 8, (4,3) 8/3, (4,4) 2, (5,2) 16, (5,3) 4, (5,4) 8/3, (5,5) 2, (6,2) 32, (6,3) 8, (6,4) 4, (6,5) 12/5, (7,3) 16, (7,4) 8, (8,3) 128/5, (8,4) 16, (8,5) 4 — primal == dual 16/16; brute table for n ≤ 6 certified: A(4,2)=8, A(4,3)=2, A(4,4)=2, A(5,2)=16, A(5,3)=4, A(5,4)=2, A(5,5)=2, A(6,2)=32, A(6,3)=8, A(6,4)=4, A(6,5)=2 — eight LP-tight plus three ((4,3), (5,4), (6,5)) closed by exhaustive search.

**Restructure verification (session 37).** The four-lecture edition was produced by verbatim extraction, checked by string comparison: every exported block — Lectures 5–8, exercises 2, 5, 11, 13, 14, 15, 19, 21, 22, answers A2, A5, A11, A13, A14, A15, A◆4, lab Parts 3–5, Figures 2–4 — is present byte-identically in the Chapter 8 skeleton (zero content loss). The retained text was re-scanned for stale references; two stale exercise pointers were corrected (the de Bruijn–Erdős checkpoint pointed at “Exercise 14” and the RCW tightness note at “Exercise 13” — the exercises that actually do that work were ◆17 and ◆16 in the old numbering, ◆11 and ◆10 now). The spectral, two-distance, and toolkit runs recorded above moved with their lectures and remain the verification basis for Chapter 8’s lab; the runs supporting the retained lectures are unchanged. Hygiene re-verified after the edit (fence balance, no mojibake, single trailing newline), and the web edition was rebuilt and byte-verified.

**Standing decisions.** Lecture bodies carry no session references; history lives here. The chapter proves what it uses and cites what it does not: the Frankl–Wilson Ramsey corollary is cited, not proven. The two-distance citation decisions (the proved elementary bound C(d+s+1, s) against the cited sharp C(d+s, s); the cited m(d) table; the flagged Larman–Rogers–Seidel phenomenon) moved with the two-distance lecture to Chapter 8, as did the canon audit's four installed proposals (interlacing, Hoffman, theta, Delsarte — Chapter 8's toolkit lecture) and the Volume II items that lived in the spectral lectures: the SDP lifts of the Delsarte LP (the first level of the hierarchy is run there), the honest (8,3) gap (LP 128/5 against the cited truth 20), the Borsuk conjecture's two-distance connection, and the 27-point Schläfli construction written out — Chapter 8's backlog when that chapter is polished. The web edition embeds this chapter byte-identically (the standard delivery format); the PDF export check is the user-owned release gate, then learner testing.

**Backfill (session 41).** Five graded exercises (14–18) with pattern-mapped hints were added, per the atlas-wide backfill mandate: Bose's bound (constant pairwise intersection λ ≥ 1, the Gram walk via the determinant lemma, sharpness at the near-pencil and the Fano plane — plus the audit of the strict inequality, where the Gram proof breaks but the bound survives by the disjoint-remainders patch); the regular friendship exception (K₃ is the only regular friendship graph — the trace ledger on A² = J + (d−1)I); the Hadamard order divisibility (the three-row census: n = 4b, every sign pattern n/4); the odd determinant (Oddtown over ℚ — one congruence, every field — against Eventown's genuinely characteristic-2 bound, with the singular pairing-family Gram); and weighted blocks (Bose over a weighted intersection — the proof consumes the Gram pattern, not the weights). Worked answers A14–A18 were machine-verified before installation: the exhaustive census of all 65,536 subfamilies of 2^[4] — every constant-λ (λ ≥ 1) family with all sizes > λ has m ≤ 4 (maximum attained by exactly five families: the four near-pencil labelings and the four triples), and the maximum is unchanged when the strictness is relaxed to ≥ λ; near-pencil Gram determinants (n−1)² for n = 3…7 and the Fano 576, re-verified against the lemma and direct elimination, the lemma itself cross-checked on 120 random instances (k = 2…7, exact integer arithmetic); the friendship census over all labeled graphs on at most six vertices (property counts 0, 1, 0, 15, 0 for n = 2…6; K₃ the only regular carrier; W₂ and W₃ canonical copies non-regular); Sylvester H₂/H₄/H₈ and Paley H₁₂ (q = 11) verified HHᵀ = nI with the three-row census returning n/4 each, and the exhaustive 512-matrix sweep confirming no order-3 Hadamard; every [4]-Oddtown Gram determinant odd (34 families, zero exceptions), the Eventown witness singular with its third row the sum of the first two; and the weighted walk verified on the triangle example (det 4a³) and hunted under mixed-sign weight vectors — zero violations, confirming the bound consumes only the Gram pattern.

**Adversarial review (session 64).** The review arc's two arguing experts (skeptic and engineer) took this chapter chunk by chunk — correctness, coherence, exposition, figure aid — extend-never-rewrite, every retained objection machine-verified before any edit. Verdict: the mathematics is otherwise CLEAN, with one load-bearing proof defect caught, confirmed, and repaired in place. **The defect (D1):** Claim 1's proof (L4.1) and its mirror in A5 asserted that the common-neighbor map α sends N(x)∖{z} injectively into N(y)∖{z} — but α(u) = z is possible and generic (in W₂ with x = a_1, y = a_2, u = b_1 the pair (u, y) has common neighbor the hub, which is z); the machine census shows the un-excisioned codomain claim failing in all 120 census graphs that have non-adjacent pairs — in every one of the 1,320 pairs. The claim itself is true; both sites now carry the repaired argument (excise u_0 = cn(x, z) and v_0 = cn(y, z) — each the *unique* z-adjacent member of its side — and inject N(x)∖{z, u_0} into N(y)∖{z, v_0}, d(x) − 2 ≤ d(y) − 2, mirror back), machine-verified on all 1,320 pairs. **Four minor fixes (D2–D5):** the L4.1 census aside now says 121 friendship graphs (1 + 0 + 15 + 0 + 105 — the "120" had dropped the triangle); this record's "counts = n·(n−2)!!" now carries the n = 3 exception (the formula's 3·1!! = 3 hub-plus-matching descriptions all describe the same labeled K₃; the lecture's own text only ever claims n = 5 and n = 7); §4.4's counting derivation is relabeled an honest cross-check (it re-derives n = k(k−1) + 1 but excludes no k ≥ 3 — parity kills only the odd k, and the trace ledger does the excluding); and A17's machine check now names both maximum Oddtown families on [4] (the four singletons, G = I, det 1, and the four triples, G = I + 2J, det 9 — the census's 34 nonempty families carry exactly two of size 4). **The fresh battery (all green, condensed):** Fisher block — Fano Gram 2I + J det 576, Sylvester minors 3, 8, 20, 48, 112, 256, 576, Bose evaluations 128/2, near-pencil Gram determinants (n−1)² = 4, 9, 16, 25, 36, the determinant lemma 0/120 mismatches, the 4-point linear-space census = 5, the 65,536-subfamily A14 census (max 4, exactly five extremal families, relaxed-λ maximum unchanged, no family with two λ-sized sets). Parity block — Oddtown 3 on [3], 4 on [4]; Eventown 2 and 4 = 2^⌊n/2⌋; F₃ analogue max 4 (singletons); △-even 8; n = 6 even-triples max 4; A17's 34 families all Gram determinants odd, Eventown witness singular. Polynomial block — RCW n = 6, k = 3 maxima 4/4/10 (the {1,2} case's 10 = triples through a fixed point); A◆1 max 4 with the {1,2,3}/{1,4,5}/{2,4,6}/{3,5,6} witness; the Ramsey graphs: p = 2, m = 5, k = 3 — 10 vertices, ω = 4, α = 2, maximum cliques exactly the all-triples-of-a-fixed-4-set, complement ≅ Petersen (15 edges, 3-regular, girth 5, twelve 5-cycles); p = 3, m = 7, k = 4 — 35 vertices, ω = 15 (all 4-sets avoiding a fixed point), α = 2 (zero independent triples), caps 29/7; k = 5 degenerate K₂₁. Friendship block — census 1, 0, 15, 0, 105, all windmills, Claim 1 in all, the D1 diagnostic run both ways; spectra W₁–W₅ against {1^(t−1), −1^t, (1±√(1+8t))/2} to 10⁻¹⁴ (Jacobi); quotient [[0, 2t], [1, 1]] with λ²−λ−2t and both eigenvalues inside the full spectra; W₂/W₃ A² = J + (D − I) entry-exact, the lab's printed matrix reproduced; triangle A² = I + J with det A = 2; A15's n ≤ 6 census (K₃ the only regular carrier, W₃ canonical copy non-regular, K₃'s ledger n = d²−d+1). Graham–Pollak — minimum partitions 2/3/4 = n − 1 (no n−2 partition exists; the staircase attains; the valid partitions number 4/70/6,180), minimum covers 2/2/3 = ⌈log₂n⌉ (no 2-cover at n = 5; the binary-address cover attains), and the z_i-span proof machine-confirmed (z_i ∈ 𝟙⊥, rank n − 1, Σ 2 s_{A_i}s_{B_i} = −‖x‖² exactly, on every valid partition). Hadamard — Sylvester H₂/H₄/H₈ and Paley H₁₂ (q = 11, residues {1, 3, 4, 5, 9}) all HHᵀ = nI, the three-row census a = b = c = d = n/4 over all row triples, the 512-sweep with no order-3 matrix. Petersen α = 4 with exactly the five stars (A◆3); A9's census: zero triples of 3-sets pairwise meeting in exactly 1; lab Part 1's "4 2 4" reproduced. **Checker-side honesty (the session-61 lesson; six alarms this session, all the reviewer's own, all re-run green against the chapter):** a Bareiss pivot-product bug; an A17 tie-keeping bug; the W₂/W₃ diagonal oracle (priced d − 1 where the equation says d — the chapter was right); the complement-regularity false alarm of the first Ramsey run; a partition-census phantom-block off-by-one; and two Legendre-table slips in the Paley check. Figures: Figure 1 (W₄) adequate — coordinates, edge colors, and all three pair-type annotations verified against the construction. Cross-references: the Chapter 8 (spectral home) and Chapter 7 (EKR) pointers are valid post-restructure, and the pattern index is consistent with the atlas (P19's reverse row lists this chapter's 2, 4, 7, 14–18, P19′ folded per convention; exercise 16's P2 mention is on P2's row). Per the rebuild rule the web edition and the .html export were rebuilt — fidelity proof first — and the review arc advances to Chapter 7.

**Survey-adoption pass (session 80).** The paper-pattern survey's chunk-15 synthesis (papers/ANALYSIS.md, §2, in the cgt-atlas-backup repo) recommended naming **slice rank** as the tensor-power face of the existing P19/P22 entries rather than minting a new pattern ID; executed here — a face row added to the pattern table pointing at Ch. 14 L6, where the cap-set theorem runs the exact same dimension budget in tensor powers. No proof, exercise, or answer changed. The .html export was rebaked per the rebuild rule, fidelity-first.

**Face-note extension (session 83).** The survey's face-naming instruction where one face spans SEVERAL patterns — say so in detail, both entries named — is executed on this row. Slice rank is the Atlas's clearest two-entry face: the CLP/EG engine is simultaneously P19's dimension budget (rank bounds the family) and P22's polynomial method (the slices are indexed by the monomials of P(x, y) = Π(1 − (x_i + y_i)²), vanishing off-diagonal); the survey's census fired both patterns together in both I9 (Croot–Lev–Pach) and I10 (Ellenberg–Gijswijt), and its recommendation was to name the face in BOTH entries rather than mint a new ID. The face row above now carries the one-face-two-entries clause. No proof, exercise, or answer changed. The .html export is rebaked at this session's export pass.

**Usage-evidence note (session 83).** The paper-pattern survey's usage ledger (papers/ANALYSIS.md, §4) names P20's honest headline: the symmetrization work the classics actually do is performed by P23 shifting or P10 averaging — and the survey's recommendation, "the Atlas P20 entry should note this," is executed in this table's P20 row (the same datum is installed in Chapter 3's P20 card, the entry's other home). The entry stays canonical — Motzkin–Straus and the shifting card are this volume's showcase — the note records the field's usage honestly. No proof, exercise, or answer changed. The .html export is rebaked at this session's export pass.

**Expansion-pass adoption (session 90).** A user-provided expansion draft of this chapter was adopted on merit through the role-scoped pipeline (R1 structural/pedagogical review → R2 adversarial proof referee → R3 computational scientist & illustrator → R4 assembly, run as cycles over the live delta, machine-verification and pattern-audit gates cross-cutting). The draft as a file was rejected (MathJax CDN — the no-script rule); its content, translated to plain-Unicode atlas notation, was adopted. **Master-defect repairs installed (R2-verified before install):** §1.2's Claim 2 now reads M = V Vᵀ (the master's "VᵀV" was dimensionally impossible); Claim 1's λ ≥ 1 reading corrected to the problem's λ ≥ 0 with an explicit d_i > 0 derivation; §3.2's multilinearization gap closed — load-bearing, since products of s linear forms are NOT multilinear for s ≥ 2, and §3.3's slice proof inherits the repair (the explicit f̃_i, agreeing with f on the cube, degree ≤ s); §3.3's over-restrictive guard s ≤ k−1 corrected to s ≤ k (raising needs only |S| ≤ s−1 < k); Exercise 7's hint now names the excised map α: N(x)∖{z, u_0} → N(y)∖{z, v_0} (a leftover of the session-64 repair, which the old hint predated); §4.5's census formula now states the n = 3 exception honestly in text, lab, figure, and formula box (1 for n = 3; n(n−2)!! for odd n ≥ 5); §1.3's distinctness hand-wave replaced by the |A_p| = |A_q| ≥ 2 vs. λ = 1 contradiction, with n ≥ 3 in the statement. **Upgrades installed:** the full determinant-lemma proof (rank-1 eigenvalue argument) at §1.2's checkpoint; the full de Bruijn–Erdős proof in §1.3; Eventown's nondegeneracy explicit (§2.2, dim W + dim W⊥ = n); the explicit upper-triangular evaluation x_S(1_T) = 1 iff S ⊆ T (§3.1); §3.4's Frankl–Wilson proof with the explicit multilinearization and evaluation matrix; §3.5's caps made explicit (FW Σ ≤ C(m, p−1) via the slice refinement when k ≥ p−1; RCW ≤ C(m, ⌊k/p⌋)), the precise degeneracy criterion (min(k, m−k) < p ⟺ k−p < max(0, 2k−m), proven equivalent to the lab's simpler form over a 175-case grid), and the Ramsey corollary with explicit parameters (k = p²−1, m = p³, K = C(p³, p−1)+1, N = C(p³, p²−1) = exp(Ω(log²K/log log K))); the friendship lecture tightened throughout (n ≥ 3 and t ≥ 1 in the problem, the no-degree-0 justification, the clean degree-class argument, the triangle folded into the assembly, the full spectral lemma ending at K₃, the counting cross-check relabeled honestly); the two-panel Figure 1; both lab parts extended; and the answer upgrades — A3's field-reach honesty (det odd reaches ℚ, ℝ, F₂ — but not F_p for an odd p dividing the determinant, the det 9 ≡ 0 mod 3 extremal family illustrating), A5's closed form det(2I_k + J_k) = 2^{k−1}(k+2), A8's "expanding before dividing gives λΠ_{i≥2}d_i > 0 — still nonsingular" parenthetical, A10's four-way column census with (HD)(HD)ᵀ = HD²Hᵀ, A11's empty-biclique discard (|A_i|, |B_i| ≥ 1 closing the division gap), A12's binomial-identity proof of the class size, A13's full by-hand ω = 4 triangle-vs-star case analysis with α = 2 via 2·3 > 5 and the L(K₅) identification, A16's five-stars proof via A13's case analysis. **Exercise reorganization (session-85 tier-folding precedent, adopted on merit):** the session-41 backfill is folded into the tiers — old 17 → E3, old 18 → E4, old 14 → E8 (restructured as the Fisher-boundary audit), old 16 → E10 — and the old exercise 15 (the regular friendship exception) is dropped as redundant with §4.4's now-complete spectral lemma; the census is 13 graded + 3 ◆ + 1 ◐ = 17 exercises with 16 worked answers (the exploration keeps none, per the atlas convention). Renumbering map (old → new): 1→1, 2→2, 17→3, 18→4, 3→5, 4→6, 5→7, 14→8, 6→9, 16→10, 7→11, 8→12, 9→13, ◆10→◆14, ◆11→◆15, ◆12→◆16, ◐13→◐17; the answers follow (new A1–A16 = old A1, A2, A17, A18, A3, A4, A5, A14, A6, A16, A7, A8, A9, A◆1, A◆2, A◆3). Exercise references in the earlier records above retain the pre-adoption numbering; this map resolves them. **Rejected, with grounds:** the draft as a file (MathJax CDN, the no-script rule — content only); the draft's regression of the exercise symbols to words (the atlas-standard ●○○/●●○/●●● and ◆/◐ restored); the draft's receipt drops from A8/A9/A10/A11/A12/A14/A16 (every answer retains its machine-check line — the session-86 rule; the drops were restored with fresh verification), with A15's receipt legitimately relocated to lab Part 1's linear-space census. **R2's battery (all 20 queue items green, fresh runs):** determinant lemma 0/300 random mismatches; the d₁ = 0 case det = λΠ_{i≥2}d_i (0/200); the Fano Gram's actual leading minors 3, 8, 20, 48, 112, 256, 576 (det 576 = 24²); near-pencil (n−1)² = 4, 9, 16, 25, 36; the five 4-point linear spaces with line counts [4, 4, 4, 4, 6]; the RCW maxima 4/4/10 confirmed by exhaustive witness + no-larger scans; the multilinearization identity f̃ = f on {0,1}^n with degree ≤ s; the s = k slice case (n = 4, k = 2, L = {0,1}: C(4,2) = 6 attained); the |L| = ⌊k/p⌋ grid and the 3-way degeneracy equivalence (brute force = draft criterion = lab criterion, 175 cases, 0 mismatches); the Ramsey corollary parameters exact for all p = 3 … 50 (|L| = p−1; N = C(p³, p²−1), the ratio log N·log log K/log²K ≥ 0.40 over the grid, trending to the asymptotic 1/4); the friendship census 1, 0, 15, 0, 105 by an independent backtracking enumeration, 121 windmills all with universal hub, zero degree-0, Claim 1 zero violations; the D1 diagnostic 120 graphs / 1,320 pairs / naive failures 1,320 / excised bijections 1,320; W_t spectra t = 1 … 5 entry-exact (blade (1,−1) vectors at −1, blade-sum differences at 1, quotient [[0, 2t], [1, 1]] with λ² − λ − 2t, multiplicities summing to n, trace 0), W₂ and W₃ spectra verified, triangle A² = I + J with det A = 2; FW(2,5,3): N = 10, ω = 4 (witness + no-5 exhaustive), α = 2 (no-3 exhaustive), exactly five maximum cliques (the stars), complement ≅ KG(5,2) by direct pair check; FW(3,7,4): N = 35, ω = 15 (exact MIS branch-and-bound + witness), α = 2 (C(35,3) exhaustive); FW(3,7,5): K₂₁; Petersen α = 4 with exactly five maximum independent sets; det 9 ≡ 0 (mod 3); the binomial identity; lab Part 1's outputs reproduced by independent recomputation (rank triple "4 2 4"; the minors, dets, spaces, and FW tuples); the W₂ walk matrix = J + (D − I); the (3,7,5) degeneracy flag. **Checker-side honesty (three test bugs found and fixed during R2, all the referee's own, none math defects):** the Fano Gram was first built with diagonal 2 instead of 2I + J's diagonal 3; the RCW branch-and-bound had a pruning bug (it returned 3/4/6) and was replaced by exhaustive witness + no-larger scans (4/4/10); the W₃ spectrum was first compared as an ordered list (the multiset match was correct), and the n = 1 vacuous K₁ was briefly flagged by a guard-less property count (the lab's is_friendship n < 3 guard excludes it — judged LIVE in R3). **R3:** the two-panel Figure 1's geometry machine-validated (hub degree 8, four blade edges, 12 edges; the H panel matching-only plus the isolated z with the forbidden (z, u) spoke; node separation and bounds; every text claim cross-checked against R2's combinatorics); the lab code line-by-line under the no-dead-clause rule — fp_rank's empty-input guard, is_friendship's n < 3 guard, and det_lemma_int's d > 0 guard all judged LIVE (the first two robustness, the third hypothesis-encoding), max_clique_size correct, the near-pencil candidate-lines construction honest, cn() context-safe. The .html export was rebaked per the rebuild rule, fidelity-first.

---
*Chapter status: ✅ **Feynman edition, four-lecture core (session 37) + exercise backfill (session 41) + adversarial review (session 64) + expansion pass (session 90)** — 4 lectures, all proofs complete (the reference edition's two flagged sketches — the ERS brick and the polynomial method — now in full), 1 verified figure (two-panel); 13 graded exercises + 3 ◆ pattern-unknown + 1 ◐ exploration, 16 worked answers machine-verified; lab in 2 verified parts (F_p ranks, determinants, linear spaces, Frankl–Wilson parameters; friendship census, Claim 1 diagnostic, W₂ walk matrix). The spectral half of the subject — averaging machines, Motzkin–Straus and spectral Turán, two-distance sets, the interlacing/Hoffman/theta/Delsarte toolkit — is Chapter 8, *Spectral Methods and the Modern Toolkit*. The session-64 adversarial review audited the chapter end to end — one proof repaired in place (Claim 1's common-neighbor map, with its A7 mirror), the mathematics otherwise clean — and the session-90 expansion pass adopted the user-provided draft on merit (repairs, upgrades, the two-panel figure, extended labs, the exercise reorganization — the record above). Ships with its web edition (the standard delivery format): the HTML canvas embeds this chapter byte-identically; print to PDF from a browser for a correct export.*
