---
name: "cgt-ch9-sumsets-shadows"
title: "Ch. 9 — Sumsets and Shadows: the Completed Arcs: A Lecture Course in the Feynman Style"
type: "text/markdown"
---

# Chapter 9 · Sumsets and Shadows: the Completed Arcs

*Part of the Combinatorics & Graph Theory Atlas (see the Atlas canvas for the chapter map and progress report).*

Two threads that began in Chapter 7 complete here, and the three flags its appendix left open close with them. The sumset thread asks how small A + B can be: the integer answer is a staircase, the prime-field answer is Cauchy–Davenport, and the master theorem is Kneser's, which prices a sumset by its periods — a price this chapter now computes in full, with the aperiodic assembly carried by two complete arguments: a two-case e-transform recursion for the weak form, and DeVos's intersection–union induction for the strong form. The shadow thread asks how few (k−1)-sets must sit underneath k given sets: the answer is the Kruskal–Katona theorem in its clique form, and the payoff is Daykin's mirror proof of EKR plus the deep cascade-uniqueness lemma, which together complete EKR uniqueness for every n > 2k — the thin range the earlier chapters honestly flagged. Between the threads, the zero-sum capstone EGZ fuses them. Every proof is complete or honestly cited, every claimed number is machine-checked, and the lab reproduces every census.

## How to read this chapter

**Notation.** A, B are nonempty finite subsets of an abelian group G, written additively; A + B = {a + b : a ∈ A, b ∈ B}, A − e = {a − e : a ∈ A}, and stab(S) = {g ∈ G : g + S = S} is the stabilizer. 𝔽_p is the field of order p and Z_n the cyclic group of order n. For the shadow thread: 𝓕, 𝓖 are k-uniform families of subsets of [n] = {1, …, n}; ∂𝓖 is the shadow (all (k−1)-sets contained in a member), ∂_j𝓖 the j-shadow, K^k_x the complete family (all k-subsets of a fixed x-set), 𝓕* = {[n]∖F : F ∈ 𝓕} the complement mirror; C(x, k) is the binomial coefficient, extended to real x ≥ k. Letters are re-stated locally where a lecture needs its own.

**The exercises are graded:** ●○○ *easy* (a direct application of one lecture idea), ●●○ *moderate* (two ideas, or one tricky step), ●●● *tough* (several chapter ideas combined). Hints travel with the problems; worked answers sit at the very end of the chapter. Try honestly before reading a hint. Beyond the graded set, ◆ **pattern-unknown** problems name no method and carry no hint: diagnosing which tool fits is part of the problem. And ◐ **Explorations** at the end are open-ended investigations with no single right answer — research training, not test preparation.

## The pattern table for this chapter

| Pattern | Plain language | Where you meet it |
|---------|---------------|-------------------|
| **P4 Induction** | Verify the base and run the recursion until a case fires; or induct on a measure every move decreases | L1 (staircase, m-fold), L2 (EGZ assembly), L3 (two cases, DeVos) |
| **P22 Polynomial method** | One polynomial vanishing on the grid; its top coefficient priced two ways | L1 |
| **P23 Compression / deformation** | Replace the object by a deformed one that is easier to read, preserving what matters | L2 (the e-transform), L3 |
| **Price the period, pass to the quotient (lore)** | When the obstruction is a subgroup of periods, quotient it away and price the deficit by its order | L2, L3 |
| **The real parameter is a price (lore)** | |𝓖| = C(x, k) buys no discount below: every j-shadow costs at least C(x, j), and adjacent-level equality pins the complete family | L4, L5 |
| **Ask what the dual object sees for free (lore)** | Complement the family before building machinery: intersection questions become containment questions | L4, L5 |

---

## Lecture 1 · The Staircase and Cauchy–Davenport

The sumset thread begins: instead of families of sets, **sets of numbers**, and the question becomes how small a sumset can be. The integer answer is a one-line staircase; the modular answer is a real theorem with two beautiful proofs — one by periodicity, one by the polynomial method of Chapter 6.

**Problem.** Nonempty finite A, B ⊆ ℤ: **|A + B| ≥ |A| + |B| − 1**, where A + B = {a + b}.

### 1.1 The integer staircase (P4, full)

Write A = {a₁ < … < a_s} and B = {b₁ < … < b_t}. The witness chain

a₁+b₁ < a₂+b₁ < a₃+b₁ < … < a_s+b₁ < a_s+b₂ < a_s+b₃ < … < a_s+b_t

is strictly increasing throughout — first climb the b₁ column, then walk the a_s row — and exhibits **s + t − 1 distinct sums**. ∎

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 880 330" font-family="Georgia, 'Times New Roman', serif">
  <defs>
    <marker id="stair-arrow" viewBox="0 0 10 10" refX="8" refY="5" markerWidth="6" markerHeight="6" orient="auto-start-reverse">
      <path d="M 0 1 L 8 5 L 0 9 z" fill="#2563eb"/>
    </marker>
  </defs>
  <rect x="0" y="0" width="880" height="330" fill="#ffffff"/>

  <!-- Left panel: sumset grid for A = {1, 2, 4}, B = {1, 3} -->
  <text x="235" y="28" text-anchor="middle" font-size="17" fill="#111827">A = {1, 2, 4}, B = {1, 3}: the sumset grid</text>
  <text x="145" y="88" text-anchor="middle" font-size="14" fill="#374151">a \ b</text>
  <text x="220" y="88" text-anchor="middle" font-size="14" fill="#374151">1</text>
  <text x="300" y="88" text-anchor="middle" font-size="14" fill="#374151">3</text>

  <!-- Row a = 1: (1,1) = 2 is on the staircase; (1,3) = 4 is interior -->
  <text x="145" y="132" text-anchor="middle" font-size="15" fill="#111827">1</text>
  <rect x="180" y="100" width="80" height="50" fill="#dbeafe" stroke="#2563eb" stroke-width="2.5"/>
  <text x="220" y="132" text-anchor="middle" font-size="15" fill="#1e3a8a">2</text>
  <rect x="260" y="100" width="80" height="50" fill="#ffffff" stroke="#e5e7eb" stroke-width="2"/>
  <text x="300" y="132" text-anchor="middle" font-size="15" fill="#6b7280">4</text>

  <!-- Row a = 2: (2,1) = 3 is on the staircase; (2,3) = 5 is interior duplicate -->
  <text x="145" y="182" text-anchor="middle" font-size="15" fill="#111827">2</text>
  <rect x="180" y="150" width="80" height="50" fill="#dbeafe" stroke="#2563eb" stroke-width="2.5"/>
  <text x="220" y="182" text-anchor="middle" font-size="15" fill="#1e3a8a">3</text>
  <rect x="260" y="150" width="80" height="50" fill="#ffffff" stroke="#e5e7eb" stroke-width="2"/>
  <text x="300" y="182" text-anchor="middle" font-size="15" fill="#6b7280">5</text>

  <!-- Row a = 4: (4,1) = 5 and (4,3) = 7 are on the staircase -->
  <text x="145" y="232" text-anchor="middle" font-size="15" fill="#111827">4</text>
  <rect x="180" y="200" width="80" height="50" fill="#dbeafe" stroke="#2563eb" stroke-width="2.5"/>
  <text x="220" y="232" text-anchor="middle" font-size="15" fill="#1e3a8a">5</text>
  <rect x="260" y="200" width="80" height="50" fill="#dbeafe" stroke="#2563eb" stroke-width="2.5"/>
  <text x="300" y="232" text-anchor="middle" font-size="15" fill="#1e3a8a">7</text>

  <!-- Staircase step arrows -->
  <line x1="220" y1="139" x2="220" y2="161" stroke="#2563eb" stroke-width="1.8" marker-end="url(#stair-arrow)"/>
  <line x1="220" y1="189" x2="220" y2="211" stroke="#2563eb" stroke-width="1.8" marker-end="url(#stair-arrow)"/>
  <line x1="238" y1="225" x2="282" y2="225" stroke="#2563eb" stroke-width="1.8" marker-end="url(#stair-arrow)"/>

  <text x="235" y="280" text-anchor="middle" font-size="13" fill="#111827">staircase 2 &lt; 3 &lt; 5 &lt; 7: four = s + t &#8722; 1 distinct sums</text>

  <!-- Center divider -->
  <line x1="440" y1="52" x2="440" y2="262" stroke="#e5e7eb" stroke-width="2"/>

  <!-- Right panel: number line and staircase heights for A + B = {2, 3, 4, 5, 7} -->
  <text x="660" y="28" text-anchor="middle" font-size="17" fill="#111827">A + B = {2, 3, 4, 5, 7}</text>
  <line x1="505" y1="230" x2="815" y2="230" stroke="#cbd5e1" stroke-width="2"/>

  <!-- Uniform horizontal positions: x(v) = 530 + (v - 2) * 52 for v in {2,3,4,5,6,7} -->
  <!-- v = 2 (staircase) -->
  <line x1="530" y1="230" x2="530" y2="195" stroke="#93c5fd" stroke-width="1.5"/>
  <circle cx="530" cy="195" r="10" fill="#dbeafe" stroke="#2563eb" stroke-width="2"/>
  <text x="530" y="175" text-anchor="middle" font-size="13" fill="#1e3a8a">2</text>
  <text x="530" y="250" text-anchor="middle" font-size="12" fill="#374151">1+1</text>

  <!-- v = 3 (staircase) -->
  <line x1="582" y1="230" x2="582" y2="170" stroke="#93c5fd" stroke-width="1.5"/>
  <circle cx="582" cy="170" r="10" fill="#dbeafe" stroke="#2563eb" stroke-width="2"/>
  <text x="582" y="150" text-anchor="middle" font-size="13" fill="#1e3a8a">3</text>
  <text x="582" y="250" text-anchor="middle" font-size="12" fill="#374151">2+1</text>

  <!-- v = 4 (interior extra sum 1+3, dashed ring) -->
  <line x1="634" y1="230" x2="634" y2="145" stroke="#d1d5db" stroke-width="1.5" stroke-dasharray="4,3"/>
  <circle cx="634" cy="145" r="10" fill="#ffffff" stroke="#6b7280" stroke-width="2" stroke-dasharray="4,2"/>
  <text x="634" y="125" text-anchor="middle" font-size="13" fill="#4b5563">4</text>
  <text x="634" y="250" text-anchor="middle" font-size="12" fill="#6b7280">1+3</text>

  <!-- v = 5 (staircase) -->
  <line x1="686" y1="230" x2="686" y2="120" stroke="#93c5fd" stroke-width="1.5"/>
  <circle cx="686" cy="120" r="10" fill="#dbeafe" stroke="#2563eb" stroke-width="2"/>
  <text x="686" y="100" text-anchor="middle" font-size="13" fill="#1e3a8a">5</text>
  <text x="686" y="250" text-anchor="middle" font-size="12" fill="#374151">4+1</text>

  <!-- v = 6 (missing value, tick only) -->
  <line x1="738" y1="225" x2="738" y2="235" stroke="#9ca3af" stroke-width="1.5"/>
  <text x="738" y="250" text-anchor="middle" font-size="12" fill="#9ca3af">(6)</text>

  <!-- v = 7 (staircase) -->
  <line x1="790" y1="230" x2="790" y2="70" stroke="#93c5fd" stroke-width="1.5"/>
  <circle cx="790" cy="70" r="10" fill="#dbeafe" stroke="#2563eb" stroke-width="2"/>
  <text x="790" y="50" text-anchor="middle" font-size="13" fill="#1e3a8a">7</text>
  <text x="790" y="250" text-anchor="middle" font-size="12" fill="#374151">4+3</text>

  <text x="660" y="280" text-anchor="middle" font-size="13" fill="#111827">|A + B| = 5 &#8805; s + t &#8722; 1 = 4: four staircase sums + interior 4</text>
  <text x="440" y="320" text-anchor="middle" font-size="14" fill="#374151">Figure 1 &#183; The sumset staircase: climb the first column, then walk the last row; every step is a new sum</text>
</svg>
```

Tightness: when |A| = 1 or |B| = 1, equality |A+B| = |A| + |B| − 1 holds for every finite nonempty partner set; when |A|, |B| ≥ 2, equality holds if and only if A and B are arithmetic progressions with the *same* common difference d > 0, i.e. A = {a₀, a₀+d, …, a₀+(s−1)d} and B = {b₀, b₀+d, …, b₀+(t−1)d}. The structure theory of equality and near-equality in general abelian groups is Kneser's business, next lecture.

### 1.2 Modulo a prime: Cauchy–Davenport, by periodicity (full)

**Theorem (Cauchy–Davenport).** A, B ⊆ 𝔽_p nonempty: **|A + B| ≥ min(p, |A| + |B| − 1).**

*Proof (periodicity and the e-transform).* First observe the basic periodicity fact in 𝔽_p: if a nonempty subset S ⊆ 𝔽_p satisfies |(S + d) ∪ S| = |S| (i.e. S + d = S) for some d ≠ 0, then S = 𝔽_p. Indeed, since p is prime and d ≢ 0 (mod p), the multiples 0, d, 2d, …, (p−1)d exhaust 𝔽_p; picking any s₀ ∈ S, invariance under d gives s₀ + md ∈ S for all m ≥ 0, so S = 𝔽_p.

We now prove |A + B| ≥ min(p, |A| + |B| − 1) by induction on |B| ≥ 1. If |B| = 1, then |A + B| = |A| = min(p, |A| + 1 − 1). Suppose |B| ≥ 2. If |A| = p, then A = 𝔽_p and |A + B| = p ≥ min(p, |A| + |B| − 1). Otherwise ∅ ≠ A ⊊ 𝔽_p. Choose two distinct elements b₀, b₁ ∈ B, and set d = b₁ − b₀ ≠ 0. By the periodicity fact, A + d ≠ A, so there exists a ∈ A with a + b₁ − b₀ ∉ A. Set e = a − b₀ and form the deformed pair

A′ = A ∪ (B + e),  B′ = B ∩ (A − e).

Then b₀ ∈ B′ (since b₀ + e = a ∈ A) and b₁ ∉ B′ (since b₁ + e = a + b₁ − b₀ ∉ A), so 1 ≤ |B′| < |B|. Every sum x + y with x ∈ A′, y ∈ B′ lies in A + B (if x ∈ A, then y ∈ B ⟹ x + y ∈ A + B; if x = b + e ∈ B + e, then y + e ∈ A ⟹ x + y = (y + e) + b ∈ A + B), so A′ + B′ ⊆ A + B. Moreover, |B′| = |(B + e) ∩ A|, so inclusion–exclusion gives |A′| + |B′| = |A ∪ (B + e)| + |A ∩ (B + e)| = |A| + |B + e| = |A| + |B|. By the inductive hypothesis on (A′, B′),

|A + B| ≥ |A′ + B′| ≥ min(p, |A′| + |B′| − 1) = min(p, |A| + |B| − 1). ∎

The periodicity engine also drives the *iterated merge* S₀ = A, S_i = S_{i−1} ∪ (S_{i−1} + b_i) for b₁, …, b_{t−1} ∈ B ∖ {0}, which builds the multi-summand sumset S_{t−1} = A + {0, b₁} + … + {0, b_{t−1}}: a step |S_i| = |S_{i−1}| forces S_{i−1} + b_i = S_{i−1} and hence S_{i−1} = 𝔽_p. The lab runs this merge monitor across all pairs of subsets of 𝔽_5 and 𝔽_7 (with 0 ∈ B): across 8,624 processes and 9,759 zero-gain steps, a zero-gain step occurs **only** when the running set S_{i−1} has already become all of 𝔽_p, and the monitor simultaneously verifies |A + B| ≥ min(p, |A| + |B| − 1) on all 8,624 pairs.

### 1.3 The polynomial method proof (P22, full)

The second proof is the Chapter 6 engine running on a grid, and it is worth seeing in its purest form. One ingredient does all the work.

**Ingredient (the weighted-sum identity).** Let F be any field, and let A, B ⊆ F be finite nonempty subsets of sizes |A| = a and |B| = b. Define Π_A(x) = Π_{c∈A}(x − c) with formal derivative Π_A′(x) = Σ_{c∈A} Π_{d∈A∖{c}}(x − d), so that Π_A′(x₀) = Π_{c∈A∖{x₀}}(x₀ − c) ≠ 0 for each x₀ ∈ A, and define Π_B, Π_B′ likewise. For any polynomial f(x, y) ∈ F[x, y] of total degree ≤ a + b − 2,

Σ_{x∈A, y∈B} f(x, y) / (Π_A′(x) · Π_B′(y)) = [x^{a−1} y^{b−1}] f.

*Proof.* First we establish the univariate identity: for every integer 0 ≤ i ≤ a − 1,

Σ_{x₀∈A} x₀^i / Π_A′(x₀) = [i = a−1].

For each x₀ ∈ A, the Lagrange basis polynomial

L_{x₀}(x) = Π_A(x) / (Π_A′(x₀)(x − x₀)) = Π_{c∈A∖{x₀}} (x − c)/(x₀ − c) ∈ F[x]

has degree a − 1, leading coefficient [x^{a−1}] L_{x₀}(x) = 1/Π_A′(x₀), and satisfies L_{x₀}(x₁) = [x₁ = x₀] for all x₁ ∈ A. For any 0 ≤ i ≤ a − 1, the difference g(x) = x^i − Σ_{x₀∈A} x₀^i L_{x₀}(x) has degree at most a − 1 and vanishes at all a distinct points of A, so g(x) = 0 identically in F[x]. Comparing the coefficient of x^{a−1} on both sides of x^i = Σ_{x₀∈A} x₀^i L_{x₀}(x) yields [i = a−1] = Σ_{x₀∈A} x₀^i / Π_A′(x₀).

Now expand f(x, y) = Σ_{i+j ≤ a+b−2} f_{ij} x^i y^j. By linearity, the weighted sum splits over monomials and factors across A and B:

Σ_{x∈A, y∈B} f(x, y)/(Π_A′(x) Π_B′(y)) = Σ_{i+j ≤ a+b−2} f_{ij} (Σ_{x∈A} x^i/Π_A′(x))(Σ_{y∈B} y^j/Π_B′(y)).

Fix a pair (i, j) with i + j ≤ a + b − 2. If i ≤ a − 2, the x-sum is 0 by the univariate identity on A. If i ≥ a, then j ≤ a + b − 2 − i ≤ b − 2, so the y-sum is 0 by the univariate identity on B. If i = a − 1, then j ≤ b − 1, so the x-sum is 1 and the y-sum is [j = b − 1]. Thus only (i, j) = (a − 1, b − 1) survives, contributing f_{a−1,b−1} = [x^{a−1} y^{b−1}] f. ∎

*(Companion fact — the grid lemma, D1.* A polynomial f(x, y) ∈ F[x, y] with deg_x f < a and deg_y f < b vanishing on all of A × B is identically zero: write f(x, y) = Σ_{i=0}^{a−1} c_i(y) x^i; for each y₀ ∈ B, f(x, y₀) has degree < a and a roots in A, so c_i(y₀) = 0 for all y₀ ∈ B, and since deg_y c_i < b, each c_i(y) ≡ 0. D1 is the engine of the *classical* variant of this proof — where one starts from a higher-degree polynomial and reduces it to the grid — and is the two-variable echo of Chapter 6's multilinear lemma. Our f has total degree a + b − 2, so the weighted-sum identity alone finishes; the lab verifies D1 on 184 exact grid reconstructions.)*

**The proof of Cauchy–Davenport.** If a + b ≥ p + 1, then for every c ∈ 𝔽_p we have |A| + |c − B| = a + b > p, so A ∩ (c − B) ≠ ∅, meaning c ∈ A + B and hence |A + B| = p = min(p, a + b − 1). Assume now that a + b ≤ p + 1, so a + b − 2 ≤ p − 1, and suppose for contradiction that |A + B| ≤ a + b − 2 (which forces a + b − 2 ≥ 1). Since a + b − 2 ≤ p − 1 < p, we may choose a subset C ⊆ 𝔽_p with

A + B ⊆ C ⊆ 𝔽_p, |C| = a + b − 2.

Set f(x, y) = Π_{c∈C}(x + y − c) ∈ 𝔽_p[x, y], of total degree a + b − 2.

- **f vanishes on A × B:** for x ∈ A, y ∈ B, the sum x + y lies in A + B ⊆ C, so one factor is zero.
- Therefore the weighted sum Σ_{x∈A, y∈B} f(x, y)/(Π_A′(x) Π_B′(y)) is 0 in 𝔽_p.
- By the weighted-sum identity, this sum equals [x^{a−1} y^{b−1}] f = [x^{a−1} y^{b−1}] (x + y)^{a+b−2} = C(a + b − 2, a − 1). Since a + b − 2 ≤ p − 1, every positive integer factor in (a + b − 2)! is strictly less than p, so C(a+b−2, a−1) ≢ 0 (mod p).

Thus 0 ≡ C(a+b−2, a−1) ≢ 0 (mod p), a contradiction. ∎

Every ingredient is machine-checked: the univariate Lagrange identity (15,011 checks over 𝔽_5–𝔽_13), the weighted-sum identity including the dying logic (900 random polynomials), the grid lemma's interpolation (184 reconstructions), the binomial non-vanishing (all m ≤ p−1), and the vanishing step f(a,b) = 0 ⟺ a+b ∈ C (450 checks).

### 1.4 The m-fold corollary (full)

**m-fold Cauchy–Davenport.** For nonempty subsets A₁, A₂, …, A_m ⊆ 𝔽_p (m ≥ 1),

|A₁ + A₂ + … + A_m| ≥ min(p, Σ_{i=1}^m |A_i| − m + 1).

*Proof.* We induct on m ≥ 1. For m = 1, |A₁| = min(p, |A₁|) holds since A₁ ⊆ 𝔽_p. For m ≥ 2, set S = A₂ + … + A_m and s = Σ_{i=2}^m |A_i| − (m − 1) + 1. By the inductive hypothesis, |S| ≥ min(p, s). Applying the two-summand Cauchy–Davenport theorem to A₁ and S gives

|A₁ + S| ≥ min(p, |A₁| + |S| − 1) ≥ min(p, |A₁| + min(p, s) − 1).

If s ≥ p, then min(p, s) = p, and since |A₁| ≥ 1 we have |A₁| + p − 1 ≥ p and |A₁| + s − 1 ≥ p, so both sides equal p. If s < p, then min(p, s) = s, and the right side is min(p, |A₁| + s − 1) = min(p, Σ_{i=1}^m |A_i| − m + 1). ∎ (The lab stress-tests this on random m ≤ 4 families over 𝔽_5, 𝔽_7, 𝔽_11 — 600 trials, zero violations; Lecture 2 uses it twice.)

### 1.5 What to learn

Two proofs, two philosophies again. The periodicity argument is *dynamic*: deform the pair or grow the sumset and show the only way to stop is to finish. The polynomial argument is *static*: build one polynomial that vanishes on the grid, and price its top coefficient two ways. The grid lemma D1 is the polynomial method's workhorse — the same "small degree + many roots ⟹ zero" move as Chapter 6's multilinear lemma, in two variables. And note the exact fingerprint: the contradiction needed a+b−2 ≤ p−1, the same boundary the theorem itself respects.

---

## Lecture 2 · Kneser's Theorem and the Zero-Sum Capstone

Cauchy–Davenport lives in 𝔽_p, and the staircase lives in ℤ. Both are shadows of one master theorem: **Kneser's theorem**, which prices a sumset by its *period* — the translations that leave it alone. This lecture states Kneser, builds the e-transform toolkit that powers its proof (both properties proved in full), proves the quotient reduction completely, and hands the aperiodic step to the next lecture, which builds it in full. Then, as a capstone, the chapter's two threads — sets and sums — fuse in the Erdős–Ginzburg–Ziv theorem, proved here in full: pairing in the prime case, block extraction in the composite case, with the m-fold Cauchy–Davenport from Lecture 1 doing the arithmetic.

### 2.1 The statement, and what a stabilizer is

**Problem.** A, B nonempty finite subsets of an abelian group G. How small can A + B be?

In ℤ the answer is |A|+|B|−1 and the witness is an arithmetic-progression-like pair (Lecture 1's staircase). In 𝔽_p the answer is min(p, |A|+|B|−1) (Lecture 1, two proofs). In Z₆, take A = B = {0, 2, 4}: then A + B = {0, 2, 4} again — size **3**, not 5, not 3+3−1 = 5. What broke? The sumset is *periodic*: adding 2 to every element of {0,2,4} gives {0,2,4} back. Periods are not a pathology; they are the *third parameter* of the subject.

**Definition.** For S ⊆ G, the **stabilizer** of S is stab(S) = {g ∈ G : g + S = S}. 

**Lemma (the stabilizer is a subgroup; S is a union of cosets).** stab(S) is a subgroup of G, and if H = stab(S), then S is a union of H-cosets: s ∈ S ⟹ s + H ⊆ S.

*Proof.* 0 ∈ stab(S) (0 + S = S). If g, h stabilize S, then (g+h) + S = g + (h + S) = g + S = S, so g + h stabilizes. And g + S = S implies S = (−g) + S by translating both sides by −g, so −g stabilizes too: a subgroup. For the coset claim, s ∈ S and h ∈ H give h + s ∈ h + S = S. ∎

**Theorem (Kneser, 1953).** Let A, B be nonempty finite subsets of the abelian group G, and let H = stab(A+B). Then

**|A + B| ≥ |A+H| + |B+H| − |H| ≥ |A| + |B| − |H|.**

Both forms hold; the strong form |A+B| ≥ |A+H| + |B+H| − |H| is never weaker than the weak form |A+B| ≥ |A| + |B| − |H|, since A ⊆ A+H and B ⊆ B+H. Sanity checks: in ℤ the only finite set with a nonzero period is ∅, so H = {0} and Kneser is the staircase; in 𝔽_p the group has only two subgroups, {0} (where both forms give |A+B| ≥ |A|+|B|−1) and H = 𝔽_p (which occurs when A+B = 𝔽_p; there the weak bound |A+B| ≥ |A|+|B|−p is slack whenever |A|+|B| < 2p, whereas the strong bound gives |A+H| + |B+H| − |H| = p + p − p = p = |A+B| with equality). The theorem specializes correctly everywhere. (✎: in Z₆ with A = B = {0, 2, 4}, verify H = {0, 2, 4}, |A+B| = 3 = 3+3−3, and that A+B is exactly one H-coset — H itself.)

### 2.2 Tight examples and the census

Three regimes, three shapes:

- **H = {0}, tight:** A = B = {0, 1, …, k−1} in Z_n with n > 2k−2: A+B = {0, …, 2k−2}, size 2k−1 = k+k−1, no period. The staircase is tight in every group that has room for it.
- **H nontrivial, tight:** the coset A = B = H = {0,2,4} in Z₆ above; more generally A = B = a + H for any finite subgroup H: A+B = 2a + H, size |H| = |H|+|H|−|H|. Subgroups are the *atoms* of small sumsets.
- **Full group:** if A+B = G, then H = G: the strong form |A+H| + |B+H| − |H| = |G| + |G| − |G| = |G| is tight for every such pair, while the weak form |G| ≥ |A|+|B|−|G| is slack unless A = B = G.

The lab runs a census with the stabilizer computed exactly: all of Z₆, Z₇, Z₈, Z₉ (3,969 / 16,129 / 65,025 / 261,121 pairs) — **zero violations**, with every tight case accounted for by a subgroup exactly as above (an arithmetic progression when H = {0}, a coset structure when H ≠ {0}); the wider gate sampling — Z₁₀ up to size 5 (405,769 pairs), Z₁₂ up to size 4 (628,849), all of Z₃² (261,121), and 40,000 sampled pairs of Z₄² — is verification-basis record, not the printed lab.

### 2.3 The e-transform: the toolkit, proved (P23)

The engine behind the hard half of Kneser is Dyson's **e-transform** — a cousin of Chapter 7's shifting lecture: replace (A, B) by a deformed pair that is *easier to analyze* while the sumset only shrinks and the total size is preserved. Compression, not counting (P23 again).

**Definition.** For e ∈ G:

A(e) = A ∪ (B + e),  B(e) = B ∩ (A − e),

where A − e = {a − e : a ∈ A}. Note the shape: one set *grows* by a translate of the other, the other *shrinks* to what matches that translate.

**Property 1 (the sumset only shrinks): A(e) + B(e) ⊆ A + B.**

*Proof.* Take x ∈ A(e), y ∈ B(e); show x + y ∈ A + B. Two cases.

- x ∈ A: then y ∈ B(e) ⊆ B, so x + y ∈ A + B directly.
- x = b₁ + e with b₁ ∈ B: then y ∈ B ∩ (A − e), so y + e ∈ A, and x + y = b₁ + (y + e) ∈ B + A = A + B. ∎

The second case is the whole trick: the translate e, which created x, is *refunded* by B(e)'s membership test y + e ∈ A. What the transform gives with one hand it claws back with the other.

**Property 2 (the total size is preserved): |A(e)| + |B(e)| = |A| + |B|.**

*Proof.* First, (B ∩ (A − e)) + e = (B + e) ∩ A: both sides say {x : x − e ∈ B and x ∈ A + e}... check by translation — translating B ∩ (A−e) by e adds e to every element, giving exactly the elements that are in B+e and in A. So |B(e)| = |(B+e) ∩ A|, the translate having the same size. Now A(e) = A ∪ (B+e), so by inclusion–exclusion

|A(e)| + |(B+e) ∩ A| = |A ∪ (B+e)| + |A ∩ (B+e)| = |A| + |B+e| = |A| + |B|. ∎

**Monotonicity and termination.** A ⊆ A(e) always; B(e) ⊆ B always. If additionally B + e ⊄ A, the inclusion A ⊆ A(e) is *strict* — some element of B+e lies outside A — so by Property 2, |B(e)| < |B| strictly: the pair traded a unit of B for a unit of A. Since |B| is a positive integer that strictly decreases, the iteration terminates. Each step keeps Aᵢ + Bᵢ ⊆ A + B (Property 1) and |Aᵢ| + |Bᵢ| = |A| + |B| (Property 2).

The lab machine-checks both properties on every e ∈ G for random A, B in Z₆, Z₈, Z₃² — 6,900 checks, zero violations.

### 2.4 The assembly: the two moves

Here is the architecture of the full proof, in two moves.

**Move 1 (the aperiodic case).** If stab(A+B) = {0}, then |A+B| ≥ |A|+|B|−1. For ℤ this is the staircase (Lecture 1, proved); for 𝔽_p it is Cauchy–Davenport (Lecture 1, proved twice). For a general abelian group this is a real theorem, and the next lecture builds it in full. The engine is the e-transform of §2.3 — the toolkit above is complete — but one honest warning belongs here already: the transform preserves the sumset only up to *containment*, and the deformed pair can be *more* periodic than the original (the machine found a pair in Z₆ whose sumset is aperiodic while a perfectly legal transform of it is not — §3.2). So the aperiodic hypothesis must be handled with care: a two-case recursion carries the weak form (§3.1), and the strong form rides DeVos's intersection–union induction (§3.3). Sources: Kneser's original 1953 paper (Math. Z. 58), Dyson's 1945 transform argument, the self-contained treatment in Nathanson's *Additive Number Theory* (GTM 165), and Tao–Vu's *Additive Combinatorics*; the recent survey arXiv:2407.12253 traces the transform's history, and DeVos's short proof carries the strong form.

**Move 2 (the quotient reduction — proved in full).** Suppose Move 1 holds as a black box for every abelian group. Let H = stab(A+B). Since A and B are nonempty and finite, A+B is nonempty and finite, and for any s₀ ∈ A+B the coset s₀ + H lies in A+B, so H is a finite subgroup with |H| ≤ |A+B|. By §2.1, A+B is a union of H-cosets, and so are A+H and B+H. Pass to the quotient group G/H: the finite nonempty images S̄ = (A+B)/H, Ā = (A+H)/H, and B̄ = (B+H)/H satisfy S̄ = Ā + B̄, and

- |S̄| = |A+B| / |H|, |Ā| = |A+H| / |H|, |B̄| = |B+H| / |H| (each set is a disjoint union of H-cosets);
- **stab(S̄) is trivial in G/H:** if a coset g+H ∈ G/H satisfies (g+H) + S̄ = S̄, then for every s ∈ A+B the coset g+s+H belongs to S̄, so g+s ∈ A+B; thus g + (A+B) ⊆ A+B, and since A+B is finite, |g+(A+B)| = |A+B| forces g+(A+B) = A+B, so g ∈ H — the identity coset.

Apply Move 1 to Ā, B̄ in G/H: |S̄| ≥ |Ā| + |B̄| − 1. Multiply through by |H|:

**|A+B| ≥ |A+H| + |B+H| − |H| ≥ |A| + |B| − |H|.** ∎

Both Kneser forms at once, and the aperiodic black box is the only flagged input. Note the pleasing division of labor: the *hard* content is all in Move 1 (structure), and Move 2 is pure bookkeeping with cosets — the same "pass to the quotient where the obstruction vanishes" move that solved the Petersen graph's equitable quotient in Chapter 8.

### 2.5 The capstone: Erdős–Ginzburg–Ziv, in full

**Theorem (EGZ, 1961).** Any 2n−1 integers contain n whose sum is divisible by n.

Forty years of additive combinatorics in one sentence: 2n−1 is the cap (2n−2 can fail: n−1 zeros and n−1 ones). The proof below is complete.

**Step 1 — the prime case, n = p.** Represent the 2p−1 residues by their canonical integers in {0, 1, …, p−1}.

*Trivial case.* Some residue occurs ≥ p times: those p copies sum to p·v ≡ 0 (mod p). Done. So assume every residue occurs ≤ p−1 times (in particular, this forces p ≥ 3, as 2p−1 = 3 residues in 𝔽_2 always fall into the trivial case).

*Pairing lemma.* A multiset of 2m elements in which no value occurs more than m times can be split into m pairs, each with two distinct elements.

*Proof.* Sort the elements in ℤ as e₁ ≤ e₂ ≤ … ≤ e_{2m} and pair eᵢ with e_{i+m} for i = 1, …, m. If a pair had eᵢ = e_{i+m}, then the sorted run eᵢ, e_{i+1}, …, e_{i+m} would be m+1 equal elements — forbidden. ∎

Now remove any single element x from the multiset. The remaining 2p−2 = 2(p−1) elements still have every multiplicity ≤ p−1 = m, so the pairing lemma splits them into p−1 pairs {aᵢ, bᵢ} with aᵢ ≢ bᵢ (mod p) — each pair a 2-element subset of 𝔽_p. The **m-fold Cauchy–Davenport theorem** (§1.4) applied to these p−1 two-element subsets gives

|{a₁, b₁} + … + {a_{p−1}, b_{p−1}}| ≥ min(p, 2(p−1) − (p−1) + 1) = min(p, p) = p.

Every residue in 𝔽_p is achievable as a choice-sum — including **−x (mod p)**. Adjoining x to the p−1 chosen elements yields p elements summing to 0 (mod p). ∎

Watch how the book's patterns stack: the greedy pairing is compression (P23), the counting engine is m-fold C–D (P22/P4), and the conclusion is a *reachability* statement — the same "the achievable set is everything" move as the Hoffman-bound arguments of Chapter 8. The lab verifies the whole chain: exhaustive search over all multisets for n = 3–7 (21 / 120 / 715 / 4,368 / 27,132 multisets) — every one contains a zero-sum n-subset (the 20,000-sample sweeps at n = 9, 10 are gate record, not the printed lab); the pairing lemma on 800 random constrained multisets; and 900 full prime-case runs in which the choice-sumset always covered 𝔽_p and −x was always reachable (44 runs settled by the trivial case, counted separately).

**Step 2 — the multiplicative step from n and m to nm.** Suppose EGZ holds for n and for m; we prove it for nm. Given 2nm−1 integers, extract disjoint n-blocks, each with sum ≡ 0 (mod n), using EGZ(n) repeatedly: after j blocks, 2nm−1−nj elements remain, and one more extraction is possible whenever

2nm−1−nj ≥ 2n−1, i.e. n(2m−j) ≥ 2n, i.e. **j ≤ 2m−2**.

So we extract 2m−1 disjoint blocks B₁, …, B_{2m−1}, each of size n with sum sᵢ ≡ 0 (mod n). The quotients tᵢ = sᵢ/n are 2m−1 integers, so EGZ(m) selects m indices i₁ < i₂ < … < i_m with t_{i₁} + … + t_{i_m} ≡ 0 (mod m). The union B_{i₁} ∪ … ∪ B_{i_m} has nm elements with total sum n(t_{i₁} + … + t_{i_m}) ≡ 0 (mod nm). Thus EGZ(nm) holds. ∎

**Step 3 — assembly.** EGZ(1) is trivial (1 divides any single integer), EGZ(p) is Step 1, and Step 2 builds EGZ of any composite integer from its factors. Induction on the number of prime factors (with multiplicity) establishes EGZ(n) for every integer n ≥ 1. ∎

The lab runs the composite chain end-to-end on 300 random instances over (n, m) = (2,3), (3,2), (2,2), (2,5), (3,3): every instance yields its 2m−1 disjoint zero-sum-n blocks, and the EGZ(m) selection on the scaled block sums produces a genuine zero-sum-nm subset. (One lab bug is worth recording as a lesson: the verifier initially checked the final sum mod nm via the *scaled* sums, i.e. mod m, rather than mod nm — the fixed check confirms divisibility by nm itself.)

### 2.6 What to learn

Kneser's theorem is the bookkeeping of *periodicity*: whenever a sumset underperforms the staircase, the deficit is exactly paid by a subgroup of periods, and the coset structure is not an accident but a proof. The e-transform is the book's compression engine at its purest — shifting (Chapter 7's shifting lecture) deformed families toward the star, the merge deformed sumsets toward the field, and the e-transform deforms pairs toward a configuration where the period is visible. And EGZ shows what a toolkit is *for*: pairing (P23) feeds m-fold C–D (P22), whose prime case feeds a block reduction (P4), and the capstone theorem falls to three moves, each of which was already on the table. That is the Feynman test of understanding — *knowing how to redo the proof with the tools you own* — and the two sumset lectures own every tool of that thread. The next lecture completes what this one flags: it builds the aperiodic assembly in full, closing the appendix's third flag. The lecture after adds the last engine of the set-system thread — shadow pricing — and uses it to retire the first of the three; the second, the thin range, follows in the closing lecture — flagged honestly until then.

---

## Lecture 3 · The Assembly, Completed: Dyson's Recursion and DeVos's Proof

Lecture 2 proved Kneser's quotient move and left the aperiodic case as a flagged input. This lecture builds that input, twice. First the *weak* theorem — every pair with |A| + |B| ≤ |G| admits a proper subgroup H with |A + B| ≥ |A| + |B| − |H| — by a two-case recursion on Dyson's e-transform, the §2.3 toolkit doing exactly the work it was built for. The recursion is honest about its own reach: a plain induction cannot deliver the strong form, and a small example in Z₆ says why (§3.2). The strong form then rides DeVos's short intersection–union induction, presented in full (§3.3): one new notion — a *portion* of a sumset — and three counting equations close what the transform alone could not. With §2.4's quotient move, this completes the book's proof of Kneser's theorem and retires the appendix's third flag.

### 3.1 The weak form: a two-case recursion (P4, full)

**Theorem (weak Kneser).** A, B nonempty finite subsets of the abelian group G with |A| + |B| ≤ |G|. Then there is a *proper* finite subgroup H ⊊ G with

**|A + B| ≥ |A| + |B| − |H|.**

*Proof.* The recursion runs on the pair (A, B), preserving three invariants — A + B contains every later sumset, the total size never changes, B never empties — and it stops in one of two cases, each of which produces a proper subgroup.

**The base: |B| = 1.** Take H = {0}: |A + B| = |A| = |A| + |B| − 1, and {0} ⊊ G because |A| + |B| ≤ |G| with both sets nonempty rules out the trivial group.

**Case 1 (no witness).** Scan the pair for a *witness*: a triple (a, b′, b) ∈ A × B × B with a + b − b′ ∉ A. If none exists, then A + (b − b′) ⊆ A for every b, b′ ∈ B. Because A is finite and translation by d = b − b′ is injective, A + d ⊆ A forces |A + d| = |A| and hence A + d = A, so B − B ⊆ stab(A). Since stab(A) is a subgroup of G (§2.1), the subgroup H′ = ⟨B − B⟩ generated by B − B satisfies H′ ⊆ stab(A). Moreover, picking any a₀ ∈ A, the map h ↦ a₀ + h injects stab(A) into A, so H′ is finite with |H′| ≤ |stab(A)| ≤ |A|. Now four facts follow:

- B ⊆ b₀ + H′ for any fixed b₀ ∈ B (since every b − b₀ lies in B − B ⊆ H′), so |B| ≤ |H′|;
- H′ stabilizes A + b₀, so A + B ⊆ A + (b₀ + H′) = (A + b₀) + H′ = A + b₀, and the sumset collapses to a single translate: |A + B| = |A|;
- stab(A) ⊆ stab(A + B) (since g + A = A ⟹ g + (A + B) = (g + A) + B = A + B), so H′ ⊆ stab(A + B);
- H′ is a proper finite subgroup of G: |H′| ≤ |A| ≤ |G| − |B| ≤ |G| − 1 < |G|.

The bound reads |A + B| = |A| = |A| + |B| − |B| ≥ |A| + |B| − |H′|, with H′ ⊊ G finite. Done.

**Case 2 (a witness exists).** Take the canonical one — the lexicographically first (a, b′) ∈ A × B (a ascending, then b′ ascending) admitting some b ∈ B with a + b − b′ ∉ A, and the first such b — and set e = a − b′,

A′ = A ∪ (B + e),  B′ = B ∩ (A − e).

The §2.3 properties do the work:

- *Containment:* A′ + B′ ⊆ A + B (Property 1) — the first invariant survives.
- *Size preservation:* |A′| + |B′| = |A| + |B| (Property 2) — so the hypothesis |A| + |B| ≤ |G| survives, and so does nonemptiness: b′ + e = a ∈ A, so b′ ∈ B′, and A ⊆ A′.
- *Strict decrease:* the witness says b + e ∉ A, so B + e ⊄ A, and §2.3's monotonicity remark gives |B′| < |B|.

Recurse on (A′, B′). |B| is a positive integer that strictly decreases, so the recursion stops — at the base or at Case 1, whichever comes first. Unrolling: the terminal pair (A*, B*) has |A*| + |B*| = |A| + |B| and its own proper subgroup H (either {0} or its Case-1 H*), with |A* + B*| ≥ |A*| + |B*| − |H|; containment chains the bound up:

|A + B| ≥ |A* + B*| ≥ |A*| + |B*| − |H| = |A| + |B| − |H|. ∎

**Corollary (Cauchy–Davenport, recovered whole).** In 𝔽_p the only proper subgroup is {0}, so the weak form gives |A + B| ≥ |A| + |B| − 1 whenever |A| + |B| ≤ p. And if |A| + |B| ≥ p + 1, then for every c ∈ 𝔽_p the sets A and c − B meet (their sizes sum to more than p), so c ∈ A + B and A + B = 𝔽_p. Together: |A + B| ≥ min(p, |A| + |B| − 1), Lecture 1's theorem — recovered without reopening either of its proofs. ∎

**Machine record.** The recursion is deterministic under the canonical rule, so it can be censused. The sweep ran it on all 738,884 ordered pairs of nonempty subsets of the twelve groups of order ≤ 9 — every Case-2 step machine-checked for containment, size preservation, strict decrease, and nonemptiness, every Case-1 termination checked for H′ ⊆ stab(A), |B| ≤ |H′|, and the collapse A + B = A + b₀, every termination checked for the weak-form conclusion and for the properness of H when |A| + |B| ≤ |G|. Zero violations anywhere:

| Group | Pairs | Case-1 | Staircase bases | Case-2 steps | Max depth |
|-------|-------|--------|-----------------|--------------|-----------|
| Z₂ | 9 | 1 | 8 | 2 | 2 |
| Z₃ | 49 | 7 | 42 | 24 | 2 |
| Z₄ | 225 | 41 | 184 | 167 | 3 |
| Z₂² | 225 | 49 | 176 | 158 | 3 |
| Z₅ | 961 | 176 | 785 | 982 | 3 |
| Z₆ | 3,969 | 872 | 3,097 | 4,939 | 4 |
| Z₇ | 16,129 | 3,473 | 12,656 | 24,333 | 4 |
| Z₈ | 65,025 | 15,541 | 49,484 | 111,607 | 5 |
| Z₄×Z₂ | 65,025 | 16,607 | 48,418 | 109,052 | 5 |
| Z₂³ | 65,025 | 18,161 | 46,864 | 106,738 | 5 |
| Z₉ | 261,121 | 63,798 | 197,323 | 505,136 | 5 |
| Z₃² | 261,121 | 66,334 | 194,787 | 492,082 | 5 |
| **Total** | **738,884** | **185,060** | **553,824** | **1,355,220** | **5** |

The theorem is indifferent to which witness the rule picks — any witness works in Case 2 — but the census is not: these counts are the lexicographic rule's. (The lab, Part 4, runs the recursion exhaustively on Z₄, Z₆, Z₇ and prints the matching rows.)

### 3.2 An honesty interlude: why the recursion stops at the weak form

The tempting overreach: run the recursion to the end, then claim the terminal H′ stabilizes A + B and read off the strong form. The containment H′ ⊆ stab(A) ⊆ stab(A + B) is proved — but for the *terminal* pair, and the recursion only preserved the original sumset up to *containment*. Nothing stops the deformed pair from being more periodic than the original, and on a small example in Z₆ it happens: A = {0, 1, 3}, B = {0, 2}. Here stab(A + B) = {0} — the sumset A + B = {0, 1, 2, 3, 5} is aperiodic — yet the perfectly legal transform with witness (a, b′, b) = (0, 2, 0), e = 4 produces A′ = {0, 1, 3, 4} and B′ = {2}, whose sumset A′ + B′ = {0, 2, 3, 5} is stabilized by {0, 3}: aperiodicity is *destroyed* by the transform. Of the six (a, b′) pairs, four are genuine transforms (containment, size preservation, and strict decrease all hold); the canonical rule picks the first of them — (a, b′) = (0, 0) with b = 2, e = 0, giving A′ = {0, 1, 2, 3} and B′ = {0}, stabilizer still trivial — while the period-creating (0, 2) with e = 4 is legal but not canonical. The weak form survives because it never asks about stab(A + B) — it produces its own proper subgroup at the terminal pair, whichever pair that is. The strong form prices the *original* sumset's period, so it needs an argument that keeps the original in view throughout. DeVos's induction does exactly that, with no transforms at all.

### 3.3 The strong form: DeVos's intersection–union induction (full)

**Theorem (Kneser, strong form — DeVos's route).** Let X, Y be nonempty finite subsets of an abelian group G, and let K = stab(X + Y). Then

|X + Y| ≥ |X + K| + |Y + K| − |K|.

*Proof.* Since X and Y are nonempty and finite, X + Y is nonempty and finite, and for any s₀ ∈ X + Y the map k ↦ s₀ + k injects K into X + Y, so K is a finite subgroup with |K| ≤ |X + Y|. We induct on the positive integer measure |X + Y| + |X|. (The argument follows M. DeVos, *A short proof of Kneser's addition theorem for abelian groups*, 2007.)

**The quotient branch: K ≠ {0}.** Since K is finite and nontrivial, |K| ≥ 2. Pass to the quotient group G/K (§2.4, Move 2): the images X̄ = (X + K)/K and Ȳ = (Y + K)/K have sumset X̄ + Ȳ = (X + Y)/K with trivial stabilizer in G/K. Moreover, |X̄ + Ȳ| = |X + Y|/|K| ≤ |X + Y|/2 < |X + Y|, and since X + K is a union of at most |X| cosets of K, |X̄| = |X + K|/|K| ≤ |X|. Thus |X̄ + Ȳ| + |X̄| < |X + Y| + |X|, so the inductive hypothesis applies in G/K and gives |X̄ + Ȳ| ≥ |X̄| + |Ȳ| − 1. Multiplying by |K| yields |X + Y| ≥ |X + K| + |Y + K| − |K|.

**The aperiodic branch: K = {0}.** Assume henceforth that K = stab(X + Y) = {0}; we must prove |X + Y| ≥ |X| + |Y| − 1. If |X| = 1, then |X + Y| = |Y| = |X| + |Y| − 1 and we are done. Suppose |X| ≥ 2 and choose distinct x, x′ ∈ X. Since stab(Y) ⊆ stab(X + Y) = {0} and x′ − x ≠ 0, the element x′ − x does not stabilize Y, so there exists y ∈ Y with y + x′ − x ∉ Y. Replace Y by its translate Y′ = Y − y + x: the sizes |Y′| = |Y| and |X + Y′| = |X + Y| and the stabilizer stab(X + Y′) = {0} are unchanged, and now x ∈ X ∩ Y′ while x′ ∉ Y′, so ∅ ≠ X ∩ Y′ ⊊ X. Rename Y′ back to Y.

**Portions.** Call a nonempty subset Z ⊆ X + Y, with finite stabilizer H = stab(Z), a portion if

|Z| + |H| ≥ |X ∩ Y| + |(X ∪ Y) + H|.

Set Z₀ = (X ∩ Y) + (X ∪ Y). Since X ∩ Y ≠ ∅ and every pair (u, v) ∈ (X ∩ Y) × (X ∪ Y) has either u ∈ X, v ∈ Y or v ∈ X, u ∈ Y, Z₀ is a nonempty subset of X + Y, and the pair (X ∩ Y, X ∪ Y) has strictly smaller induction measure:

|Z₀| + |X ∩ Y| ≤ |X + Y| + |X ∩ Y| < |X + Y| + |X|.

By the inductive hypothesis applied to (X ∩ Y, X ∪ Y) with H₀ = stab(Z₀),

|Z₀| ≥ |(X ∩ Y) + H₀| + |(X ∪ Y) + H₀| − |H₀| ≥ |X ∩ Y| + |(X ∪ Y) + H₀| − |H₀|,

so Z₀ is a portion. Among all portions, choose a portion Z ⊆ X + Y whose stabilizer H = stab(Z) has |H| minimal (hence minimal under inclusion).

**The trivial exit: H = {0}.** Then |X + Y| ≥ |Z| ≥ |X ∩ Y| + |X ∪ Y| − 1 = |X| + |Y| − 1, and we are done.

**The nontrivial branch: H ≠ {0} — for a contradiction.** Since stab(X + Y) = {0} ≠ H, the sumset X + Y is not a union of H-cosets, so there exist a ∈ X and b ∈ Y such that the H-coset C := a + b + H satisfies C ⊄ X + Y. Define

X₁ = X ∩ (a + H),  Y₁ = Y ∩ (b + H),  X₂ = X ∩ (b + H),  Y₂ = Y ∩ (a + H),

so a ∈ X₁ ≠ ∅ and b ∈ Y₁ ≠ ∅. For i ∈ {1, 2} with Xᵢ, Yᵢ ≠ ∅, set Zᵢ = Z ∪ (Xᵢ + Yᵢ) ⊆ X + Y and Hᵢ = stab(Xᵢ + Yᵢ).

*The key observation.* Whenever Xᵢ, Yᵢ ≠ ∅, we have stab(Zᵢ) = Hᵢ ⊊ H and |Zᵢ| = |Z| + |Xᵢ + Yᵢ|:

- *Z is disjoint from C, and 0 < |Xᵢ + Yᵢ| < |H|:* because Z is a union of H-cosets and Z ⊆ X + Y while C ⊄ X + Y, Z cannot meet C, so Z ∩ C = ∅. Meanwhile, Xᵢ + Yᵢ is a nonempty subset of C ∩ (X + Y) ⊊ C, so 0 < |Xᵢ + Yᵢ| < |C| = |H| and |Zᵢ| = |Z| + |Xᵢ + Yᵢ|.
- *Hᵢ ⊆ H is a proper subgroup:* pick p₀ ∈ Xᵢ + Yᵢ ⊆ C. For any g ∈ Hᵢ, g + p₀ ∈ Xᵢ + Yᵢ ⊆ C, so g ∈ C − p₀ = H. If Hᵢ = H, then Xᵢ + Yᵢ would be a nonempty H-invariant subset of the single H-coset C, forcing Xᵢ + Yᵢ = C ⊆ X + Y — false. Thus Hᵢ ⊊ H.
- *stab(Zᵢ) = Hᵢ:* every g ∈ Hᵢ ⊆ H stabilizes both Z (as H = stab(Z)) and Xᵢ + Yᵢ, so Hᵢ ⊆ stab(Zᵢ). Conversely, let g ∈ stab(Zᵢ). Because H is a subgroup of G, translation by g permutes the H-cosets of G, and for every H-coset D we have |Zᵢ ∩ (g + D)| = |(g + Zᵢ) ∩ (g + D)| = |Zᵢ ∩ D|. Since Z is a union of H-cosets disjoint from C and Zᵢ ∩ C = Xᵢ + Yᵢ, C is the unique H-coset of G whose intersection with Zᵢ has cardinality strictly between 0 and |H| (every other H-coset meets Zᵢ in size 0 or |H|). Therefore g + C = C, which gives g ∈ H. Since g ∈ H = stab(Z), we have g + Z = Z, and intersecting g + Zᵢ = Zᵢ with C gives g + (Xᵢ + Yᵢ) = Xᵢ + Yᵢ, so g ∈ Hᵢ.

Because stab(Zᵢ) = Hᵢ ⊊ H, the minimality of |H| implies that Zᵢ is not a portion:

|Zᵢ| + |Hᵢ| < |X ∩ Y| + |(X ∪ Y) + Hᵢ|.

Furthermore, the inductive hypothesis applies to (Xᵢ, Yᵢ): since Z is a nonempty union of H-cosets, |H| ≤ |Z|, and Z ⊊ Zᵢ ⊆ X + Y gives |Xᵢ + Yᵢ| < |H| ≤ |Z| < |X + Y| while |Xᵢ| ≤ |X|, so |Xᵢ + Yᵢ| + |Xᵢ| < |X + Y| + |X|. Induction on (Xᵢ, Yᵢ) with stabilizer Hᵢ = stab(Xᵢ + Yᵢ) gives

|Xᵢ + Yᵢ| ≥ |Xᵢ + Hᵢ| + |Yᵢ + Hᵢ| − |Hᵢ|.

**Equation (1).** Subtract the non-portion inequality for Zᵢ from the portion inequality for Z, using |Zᵢ| = |Z| + |Xᵢ + Yᵢ| and the inductive bound on |Xᵢ + Yᵢ|:

|(X ∪ Y) + H| − |(X ∪ Y) + Hᵢ| < (|Z| + |H|) − (|Zᵢ| + |Hᵢ|) = |H| − |Xᵢ + Yᵢ| − |Hᵢ| ≤ |H| − |Xᵢ + Hᵢ| − |Yᵢ + Hᵢ|.  (1)

Equation (1) holds unconditionally for i = 1 (since X₁, Y₁ ≠ ∅), and for i = 2 whenever X₂, Y₂ ≠ ∅.

*Three degeneracies, each ruled out by (1) at i = 1.* Since H₁ ⊆ H, the set (X ∪ Y) + H₁ is a subset of (X ∪ Y) + H, and for any H-coset D, ((X ∪ Y) + H₁) ∩ D = ((X ∪ Y) ∩ D) + H₁. Inspect the cosets a + H (which lies in (X ∪ Y) + H since a ∈ X) and b + H (which lies in (X ∪ Y) + H since b ∈ Y):

- If **Y₂ = ∅**: then (X ∪ Y) ∩ (a + H) = X₁ ∪ Y₂ = X₁, so the number of elements of a + H lying in ((X ∪ Y) + H) ∖ ((X ∪ Y) + H₁) is |H| − |X₁ + H₁| > |H| − |X₁ + H₁| − |Y₁ + H₁| (as |Y₁ + H₁| ≥ |Y₁| ≥ 1), contradicting (1) at i = 1.
- If **X₂ = ∅**: then (X ∪ Y) ∩ (b + H) = X₂ ∪ Y₁ = Y₁, so the uncovered count on b + H is |H| − |Y₁ + H₁| > |H| − |X₁ + H₁| − |Y₁ + H₁| (as |X₁ + H₁| ≥ 1), contradicting (1) at i = 1.
- If **a + H = b + H**: then X₁ = X₂ and Y₁ = Y₂, and on the single coset a + H = b + H ⊆ (X ∪ Y) + H we have (X ∪ Y) ∩ (a + H) = X₁ ∪ Y₁, so the uncovered count on a + H is |H| − |(X₁ ∪ Y₁) + H₁| ≥ |H| − |X₁ + H₁| − |Y₁ + H₁|, again contradicting the strict inequality (1) at i = 1.

Thus X₂ ≠ ∅, Y₂ ≠ ∅, and a + H ≠ b + H, so equation (1) holds for both i = 1 and i = 2.

**Equation (2).** Because Hᵢ ⊆ H, the sets (X ∪ Y) + H, (X ∪ Y) + Hᵢ, H, Xᵢ + Hᵢ, and Yᵢ + Hᵢ are all unions of Hᵢ-cosets, so their cardinalities are multiples of |Hᵢ|. Since (X ∪ Y) + Hᵢ ⊆ (X ∪ Y) + H, the left side of (1) is a nonnegative multiple of |Hᵢ| strictly less than the multiple |H| − |Xᵢ + Hᵢ| − |Yᵢ + Hᵢ| of |Hᵢ|, which forces

|H| − |Xᵢ + Hᵢ| − |Yᵢ + Hᵢ| ≥ |Hᵢ|, and hence |H| ≥ |Xᵢ| + |Yᵢ| + |Hᵢ| — for i = 1, 2.  (2)

**Equation (3).** Since stab(X + Y) = {0} ⊊ H, minimality of |H| implies that X + Y is not a portion, so |X + Y| + 1 < |X ∩ Y| + |X ∪ Y| = |X| + |Y|, i.e. |X| + |Y| − |X + Y| ≥ 2 > 0. Define the uncovered parts of the two distinct cosets a + H and b + H:

A = (a + H) ∖ (X₁ ∪ Y₂) = (a + H) ∖ (X ∪ Y),  B = (b + H) ∖ (X₂ ∪ Y₁) = (b + H) ∖ (X ∪ Y).

Because a + H and b + H are disjoint cosets contained in (X ∪ Y) + H, the sets X ∪ Y, A, and B are pairwise disjoint subsets of (X ∪ Y) + H, giving |(X ∪ Y) + H| ≥ |X ∪ Y| + |A| + |B|. Moreover, Zᵢ = Z ⊎ (Xᵢ + Yᵢ) ⊆ X + Y gives |Z| ≤ |X + Y| − |Xᵢ + Yᵢ|. Substituting both into the portion inequality for Z yields, for i = 1, 2,

|H| ≥ |X ∩ Y| + |(X ∪ Y) + H| − |Z| ≥ |X ∩ Y| + |X ∪ Y| + |A| + |B| − |X + Y| + |Xᵢ + Yᵢ| = |A| + |B| + (|X| + |Y| − |X + Y|) + |Xᵢ + Yᵢ| > |A| + |B| + |Xᵢ| + |Yᵢ| − |Hᵢ|,  (3)

where the last step uses |X| + |Y| − |X + Y| > 0 and |Xᵢ + Yᵢ| ≥ |Xᵢ + Hᵢ| + |Yᵢ + Hᵢ| − |Hᵢ| ≥ |Xᵢ| + |Yᵢ| − |Hᵢ|.

**The coset count that cannot add up.** Add equation (2) for i = 1, 2 and equation (3) for i = 1, 2:

4|H| > 2(|A| + |B| + |X₁| + |Y₁| + |X₂| + |Y₂|), so 2|H| > |A| + |B| + |X₁| + |Y₁| + |X₂| + |Y₂|.

On the other hand, a + H = A ⊎ (X₁ ∪ Y₂) and b + H = B ⊎ (X₂ ∪ Y₁), so subadditivity gives |H| = |a + H| = |A| + |X₁ ∪ Y₂| ≤ |A| + |X₁| + |Y₂| and |H| = |b + H| = |B| + |X₂ ∪ Y₁| ≤ |B| + |X₂| + |Y₁|. Summing these two inequalities gives

2|H| ≤ |A| + |B| + |X₁| + |Y₁| + |X₂| + |Y₂| < 2|H|,

a contradiction. Thus the nontrivial branch H ≠ {0} cannot occur, completing the induction. ∎

**Machine record.** The machinery is deterministic, so it too was censused: on the 39,449 aperiodic pairs with |X| ≥ 2 of Z₆ (1,080), Z₇ (5,537), Z₈ (18,432), and Z₄×Z₂ (14,400), the translate step always lands ∅ ≠ X ∩ Y ⊊ X; Z₀ = (X ∩ Y) + (X ∪ Y) is always a portion; and the trivial exit always holds — the aperiodic staircase |X + Y| ≥ |X| + |Y| − 1, zero violations. The stabilizer of Z₀ is nontrivial on 3,604 of the pairs (Z₆ 60, Z₇ 0, Z₈ 930, Z₄×Z₂ 2,614), but on *every* pair there is also a trivial-stabilizer portion — so the stabilizer-minimal choice, the proof's, never fires the nontrivial branch in the data. The proof carries that branch anyway; that is what proofs are for, and the four equations above are what it costs. (Exercise 10 walks the canonical instance X = {0, 1}, Y = {0, 3, 4} in Z₆ — six portions, one of them Z₀ with stabilizer {0, 3}, five trivial; the lab, Part 4, enumerates them.)

With Move 2 (§2.4) and this lecture assembled, Kneser's theorem is the book's throughout: |A + B| ≥ |A + H| + |B + H| − |H| for H = stab(A + B), no flagged inputs left. **Flag (iii) retires.**

### 3.4 What to learn

Two assemblies, two temperaments. The recursion is P4 in its purest form: a deterministic procedure whose two exits are the two cases of the proof, the invariants doing the bookkeeping — and its honesty clause teaches as much as its success: the invariant was too weak for the strong form, and the Z₆ counterexample is a proof that no witness rule fixes that; some failures are structural, not tactical. DeVos's induction is the opposite temperament: no transforms, one well-chosen measure (|X + Y| + |X|), one new notion — the portion, which prices a piece of the sumset by its *own* stabilizer — and a final pair of cosets that cannot be partitioned as the arithmetic demands. The lesson to carry: when an invariant fails, the right move is sometimes not a better invariant but a different induction — DeVos never repairs the transform; he refuses it. And notice what made the strong form cheap: the portion inequality is Kneser's own bound applied to a sub-pair, the induction hypothesis doing at every level what the quotient move does once. With the strong form proved, the sumset thread is complete: staircase, C–D, Kneser, EGZ — every proof the book's.

---

## Lecture 4 · Shadows: The Kruskal–Katona Theorem

### 4.1 The question, and two costumes

The last engine of the set-system thread answers a deceptively simple question: **if you know how many k-sets you own, how few (k−1)-sets must sit underneath them?** The *shadow* ∂𝓖 of a k-uniform family 𝓖 is the family of all (k−1)-sets contained in some member of 𝓖; the j-shadow ∂_j𝓖 is the same construction iterated down to level j. Shadows look like bookkeeping; they are actually a *price system* — and pricing families by their shadows is what finally lets this book's counting world reach the structural questions the earlier routes left flagged.

**The theorem, costume one (the cascade).** Kruskal (1963) and Katona (1966), independently: among all families of N k-sets, the smallest shadow is achieved by the initial segments of the *colex order* — order k-sets by their largest element, ties broken by the next-largest, downward ({1,2} ≺ {1,3} ≺ {2,3} ≺ {1,4} ≺ …) — and take the first N. The cascade form makes the minimum computable: write N in its k-binomial representation

N = C(a_k, k) + C(a_{k−1}, k−1) + … + C(a_i, i)   (a_k > a_{k−1} > … > a_i ≥ i ≥ 1),

built greedily (a_k is the largest a with C(a, k) ≤ N, then descend a level), and then the minimum shadow size is C(a_k, k−1) + C(a_{k−1}, k−2) + … + C(a_i, i−1). This chapter cites the cascade theorem rather than proving it — it belongs to the same world as the compression philosophy of Chapter 7's shifting lecture (a canonical initial segment beats every deformation), raised to a complete classification.

**Costume two (the real parameter — the one this book uses).** Lovász's version prices a family by a single number: if |𝓖| = C(x, k) with x real and x ≥ k ≥ 1, then |∂𝓖| ≥ C(x, k−1). For each integer k ≥ 1, the real binomial polynomial C(x, k) = x(x−1)…(x−k+1)/k! (with C(x, 0) := 1) interpolates the integer binomials and is continuous and strictly increasing for real x ≥ k−1 (since each factor x−i is nonnegative and strictly increasing on [k−1, ∞), and positive on (k−1, ∞)). The two costumes are one theorem: the cascade pins the exact minimum integer-wise; the real form trades a little sharpness for portability — no bookkeeping, one price per family, pluggable into inductions (both §4.2 and §4.3 rely on exactly that).

**The machine census as referee.** Cascade versus colex initial segments: agreement on all 781 sizes (k = 2, 3, 4; every N ≤ C(12, k)); and cascade(10, 3) = 10 = C(5, 2) — the ten triples on a 5-set have exactly ten pairs underneath them. The real form, exhaustively: every one of the 32,767 nonempty 2-uniform families on [6] and every one of the 1,048,575 3-uniform families on [6] satisfies the bound (plus 24,000 sampled families at (7, 3), (7, 4), (8, 3), (8, 4) — zero violations), and **equality happens exactly when x is an integer and 𝓖 is the complete family K^k_x** — all k-subsets of a fixed x-set: all 99 exhaustive equality cases are precisely these, 57 at k = 2 (15 single edges + 20 triangles + 15 four-vertex cliques + 6 five-vertex + 1 six-vertex) and 42 at k = 3 (20 single triples + 15 + 6 + 1 complete families above them).

(✎: at k = 2 the shadow is the vertex set. The four edges {1,2}, {1,3}, {1,4}, {2,3} have |𝓖| = 4 = C(x, 2), so x = (1+√33)/2 ≈ 3.37, and the shadow {1, 2, 3, 4} has size 4 ≥ 3.37 ✓. The triangle {1,2}, {1,3}, {2,3} has x = 3 and shadow exactly {1, 2, 3} of size 3 = C(3, 1) — equality, and indeed the triangle is the complete family on {1, 2, 3}, as the equality structure demands.)

### 4.2 The clique form, and the proof (full)

The route to a complete proof is one more change of costume — from shadows to cliques. Fix r ≥ 1 and a family 𝓖 of r-subsets of a vertex set V. Call an (r+1)-set X a **clique** of 𝓖 if every r-subset of X belongs to 𝓖, and write K(𝓖) for the number of cliques. (The statement below assumes |𝓖| = C(x, r) with x ≥ r, i.e. a nonempty family.)

**Theorem (clique form; statement Lovász — from the cascade theorem —, short proof by Keevash, 2008).** If |𝓖| = C(x, r) with x real and x ≥ r ≥ 1, then K(𝓖) ≤ C(x, r+1).

*Proof.* We induct on r ≥ 1.

*Base r = 1.* 𝓖 is a family of x = |𝓖| singletons; every pair drawn from those x vertices forms a 2-clique, so K(𝓖) = C(x, 2) with equality.

*Step (r ≥ 2).* For each vertex v ∈ V, define its **link** L(v) = {T ⊆ V∖{v} : |T| = r−1 and T∪{v} ∈ 𝓖}. The map T ↦ T∪{v} is a bijection from L(v) to the members of 𝓖 containing v, so |L(v)| = d(v), the degree of v. Write K(v) for the number of cliques of 𝓖 containing v. If d(v) = 0, then K(v) = 0. If d(v) ≥ 1, then d(v) ≥ 1 = C(r−1, r−1), so by continuity and strict monotonicity of C(·, r−1) on [r−1, ∞) there is a unique real y_v ≥ r−1 with d(v) = C(y_v, r−1). We then have two ceilings on K(v):

1. **The link ceiling.** A clique X containing v has the form X = S∪{v} with |S| = r, and X is a clique of 𝓖 if and only if S ∈ 𝓖 and every (r−1)-subset T ⊂ S lies in L(v) — in particular, S is an r-clique of the (r−1)-uniform family L(v). Since y_v ≥ r−1 ≥ 1, the inductive hypothesis applied to L(v) gives K(v) ≤ K(L(v)) ≤ C(y_v, r) = C(y_v, r−1)·(y_v − r + 1)/r = d(v)·(y_v − r + 1)/r.
2. **The degree ceiling.** The map X ↦ X∖{v} sends cliques of 𝓖 containing v injectively into members of 𝓖 avoiding v. Thus K(v) ≤ |𝓖| − d(v) = C(x, r) − d(v).

**The per-vertex price.** We claim K(v) ≤ (x/r − 1)·d(v) for every vertex v ∈ V. For d(v) = 0 both sides are 0; for d(v) ≥ 1 there are two cases:

- If y_v ≤ x−1 (equivalently d(v) ≤ C(x−1, r−1)): ceiling 1 gives K(v) ≤ d(v)·(y_v − r + 1)/r ≤ d(v)·(x − r)/r = (x/r − 1)·d(v).
- If y_v > x−1 (equivalently d(v) > C(x−1, r−1)): ceiling 2 together with the polynomial Pascal identity C(x, r) − C(x−1, r−1) = C(x−1, r) gives K(v) ≤ C(x, r) − d(v) < C(x, r) − C(x−1, r−1) = C(x−1, r) = C(x−1, r−1)·(x − r)/r < d(v)·(x/r − 1), since x − r ≥ 0. (In particular, this second case is always strictly slack when x > r, and impossible when x = r since |𝓖| = 1 ⟹ d(v) ≤ 1 = C(r−1, r−1).)

**Summing.** Double counting vertex–clique and vertex–edge incidences gives (r+1)·K(𝓖) = Σ_v K(v) and Σ_v d(v) = r·|𝓖| = r·C(x, r). Hence

(r+1)·K(𝓖) = Σ_v K(v) ≤ (x/r − 1)·Σ_v d(v) = (x − r)·C(x, r) = (r+1)·C(x, r+1).

Dividing by r+1 gives K(𝓖) ≤ C(x, r+1). ∎

**Equality (for x ≥ r ≥ 1).** If x = r, then |𝓖| = C(r, r) = 1, which is already the complete family K^r_r on its r vertices, with K(𝓖) = 0 = C(r, r+1). For x > r (and r ≥ 2), equality K(𝓖) = C(x, r+1) forces K(v) = (x/r − 1)·d(v) for every vertex v. Since the second case y_v > x−1 is strictly slack when x > r, every active vertex (d(v) > 0) must sit in the first case with equality y_v = x−1, meaning d(v) = C(x−1, r−1). If n′ vertices are active, then r·C(x, r) = Σ_v d(v) = n′·C(x−1, r−1), so n′ = r·C(x, r)/C(x−1, r−1) = x. Thus x = n′ is an integer, the union of 𝓖 has x vertices, and C(x, r) distinct r-subsets of an x-element vertex set must be all of them: 𝓖 = K^r_x. Conversely, K^r_x attains K(K^r_x) = C(x, r+1). (Note that for r = 1, every nonempty 1-uniform family has integer size x = |𝓖| and is automatically K^1_x.) And the census agrees: all 99 exhaustive equality cases at (6, 2) and (6, 3) are exactly the complete families, in the clique form and in the shadow form alike.

**Corollary (the shadow form — Lovász's costume).** Let 𝓕 be a k-uniform family (k ≥ 1) with |𝓕| = C(x, k) for a real x ≥ k. Then |∂𝓕| ≥ C(x, k−1).

*Proof.* For k = 1, 𝓕 is nonempty so ∂𝓕 = {∅} has size 1 = C(x, 0). Assume k ≥ 2, and set 𝓖 = ∂𝓕, which is (k−1)-uniform. Since |𝓕| = C(x, k) ≥ 1, 𝓕 contains at least one k-set F, whose k subsets of size k−1 all lie in 𝓖; thus |𝓖| ≥ k > 1 = C(k−1, k−1). By continuity and strict monotonicity of C(·, k−1) on [k−1, ∞), there is a unique real y ≥ k−1 ≥ 1 with |𝓖| = C(y, k−1). Every F ∈ 𝓕 has all its (k−1)-subsets in ∂𝓕 = 𝓖, so every F ∈ 𝓕 is a k-clique of 𝓖. By the clique theorem applied to 𝓖,

C(x, k) = |𝓕| ≤ K(𝓖) ≤ C(y, k).

Since C(·, k) is strictly increasing on [k−1, ∞) and x, y ≥ k−1, this forces y ≥ x, and hence |∂𝓕| = C(y, k−1) ≥ C(x, k−1). ∎

**The j-form, by induction on the price.** The same argument iterates to every level 1 ≤ j < k: |𝓖| = C(x, k) implies |∂_j𝓖| ≥ C(x, j). One application gives |∂𝓖| ≥ C(x, k−1); now price ∂𝓖 by its own parameter — |∂𝓖| = C(x′, k−1) with x′ ≥ x — and apply again: |∂_{k−2}𝓖| ≥ C(x′, k−2) ≥ C(x, k−2); iterate down to level j. The engine is that each application prices the *current* family by its own real parameter, and parameters only grow as you descend. Machine check, exhaustive: at (6, 3) both j = 1 and j = 2 hold for all 1,048,575 families (zero violations), equality exactly the 42 complete families; at (6, 2), j = 1 holds for all 32,767 families, equality exactly the 57 complete families. ∎

### 4.3 Daykin's mirror: EKR a third way (full)

Now the payoff — the theorem this book has proved completely once (the circle method, Chapter 7's Lecture 3) and cited once (the shifting route, its closing step): a second complete proof, with no circles, no shifting, and no averaging — one disjointness observation, one j-form application, one monotone function. **Daykin's observation (1974)** is that complementation turns *intersection* facts into *containment* facts, and containment is exactly what shadows measure.

Let 𝓕 be a nonempty intersecting k-uniform family on [n] with k ≥ 1 and n ≥ 2k, and pass to complements: 𝓕* = {[n]∖F : F ∈ 𝓕}, uniform of size n−k ≥ k. Take the k-shadow of 𝓕* (with ∂_k𝓕* := 𝓕* when n − k = k) and read it in plain language:

∂_k𝓕* = {k-sets S : S ⊆ [n]∖F for some F ∈ 𝓕} = the k-sets **disjoint from a member of 𝓕**.

**The mirror disjointness.** 𝓕 ∩ ∂_k𝓕* = ∅. Indeed, a member F ∈ 𝓕 lying in ∂_k𝓕* would be disjoint from some F′ ∈ 𝓕 — impossible in an intersecting family, including the case F′ = F, since a k-set is never disjoint from itself (k ≥ 1). Both 𝓕 and ∂_k𝓕* are k-uniform, so

|𝓕| + |∂_k𝓕*| ≤ C(n, k).   (*)

**One application of the j-form.** Write |𝓕*| = |𝓕| = C(x, n−k) with x ≥ n−k ≥ k. The j-form at level j = k gives |∂_k𝓕*| ≥ C(x, k). Feeding this into (*):

C(x, n−k) + C(x, k) ≤ C(n, k).

Now define h(t) = C(t, n−k) + C(t, k) and watch two facts do all the work. First, h is strictly increasing for t ≥ n−k, since both binomials increase there. Second, Pascal at the integer point n−1:

h(n−1) = C(n−1, n−k) + C(n−1, k) = C(n−1, k−1) + C(n−1, k) = C(n, k).

So C(x, n−k) + C(x, k) ≤ h(n−1) with h increasing forces **x ≤ n−1**, and therefore

|𝓕| = C(x, n−k) ≤ C(n−1, n−k) = C(n−1, k−1). ∎

That is EKR — the book's second complete proof. At n = 2k the mirror *is* the complementary-pair argument of Chapter 7's Lecture 4: 𝓕* is then k-uniform, a k-set inside the complement of a k-set is exactly that complement, so ∂_k𝓕* = 𝓕* and (*) reads 2|𝓕| ≤ C(2k, k) — one member per complementary pair, Chapter 7's §4.1 re-derived.

**Machine record.** Exhaustive on [6]: every one of the 192 intersecting 2-uniform families (the empty family included) and all 59,049 intersecting 3-uniform families satisfy (*); the maximum 5 at (6, 2) is achieved by exactly the 6 stars (the n > 2k regime), the maximum 10 at (6, 3) by exactly 1,024 families (the n = 2k regime). One honest nuance the census surfaces: mirror-*equality* in (*) is not the same as maximality — at (6, 2) it holds for 26 families, the 6 stars and also the 20 triangles, which are sub-maximum (size 3) but still split C(6, 2) = 15 exactly; at (6, 3) it holds for all 1,024 maxima. The EKR bound comes from h's monotonicity, not from mirror-equality alone: a tight mirror can still sit at a loose x.

With this, **flag (i) of the appendix — the shifting route's closing induction — is retired**: EKR now has two complete proofs in this book (Chapter 7's circle-method Lecture 3; the mirror, here), and the shifting route's closing induction is cited for what it is — the field's standard third route, carrying none of this book's weight. (D. E. Daykin, "Erdős–Ko–Rado from Kruskal–Katona", J. Combin. Theory Ser. A 17 (1974) 254–255.)

### 4.4 The shade route to uniqueness — the missing brick

The mirror tempts an overreach: uniqueness by the same road. Suppose n > 2k and |𝓕| = C(n−1, k−1) exactly. Then (*) forces |∂_k𝓕*| ≤ C(n, k) − C(n−1, k−1) = C(n−1, k), while the j-form gives |∂_k𝓕*| ≥ C(x, k): so x = n−1, and **equality holds in the j-form, many levels deep** — the shadow drops from uniformity n−k all the way down to level k. If deep j-form equality forced 𝓕* to be the complete family K^{n−k}_{n−1} — all (n−k)-sets inside one fixed (n−1)-set — then every member of 𝓕 would contain the missing vertex z, and the star would follow: uniqueness proved.

The gap, closed in the next lecture: §4.2's equality analysis is proved for the shadow one level down and iterates level by level, and the seemingly deeper statement — "a family sitting at the cascade's minimum across many levels at once must be complete" — in fact follows from that same clique-equality analysis, applied once at the level adjacent to uniformity. That is the deep cascade-uniqueness lemma, built in four steps in §5.2. The ledger after this lecture: flag (i) closed here; flag (iii) (Kneser's aperiodic assembly) closed in Lecture 3; flag (ii) — the middle-J transport with its thin range, the honest forward pointer in Chapter 7's Lecture 4 — is the closing lecture's target.

**The Hilton–Milner gateway.** Once stars are the unique maximum (n > 2k), the next question writes itself: how big can an intersecting family with an **empty core** — no element common to all members — be? Hilton–Milner (1967): |𝓕| ≤ C(n−1, k−1) − C(n−k−1, k−1) + 1, tight at the family of all k-sets containing x and meeting a fixed Y (x ∉ Y, |Y| = k), together with Y itself. The machine census at (7, 3) confirms the shape of the world: Bron–Kerbosch over the 35 triples finds exactly 6,127 maximal intersecting families; the maximum 15 is achieved by exactly the 7 stars; among empty-core families the maximum is 13 = C(6, 2) − C(3, 2) + 1, the HM formula, achieved by exactly **175** families — and the census splits them into two shapes: 140 of the HM type (7 choices of x, 20 of Y) and 35 of a second shape, the k-sets meeting a fixed triple W in at least 2 points, which at k = 3 ties the HM family in size. The tie is a small-k phenomenon: at k ≥ 4 the two shapes separate — sizes 70 and 75 at (10, 4), 51 and 53 at (9, 4), 288 and 316 at (12, 5), the HM formula winning each time in this regime (Hilton–Milner's theorem) — and the *shape* comparison is genuinely subtle: it is the doorstep of the next theorem.

**Ahlswede–Khachatrian: the complete answer (citation gateway).** For n < 2k every two k-sets intersect, so the maximum is trivially C(n, k) — larger than any star; EKR's regime n ≥ 2k is exactly where the star C(n−1, k−1) wins. The complete answer for *all* (n, k) is Ahlswede–Khachatrian's complete intersection theorem (1997): the maximum is max over r ≥ 0 of |F_r|, where F_r is the family of k-sets meeting the initial segment [2r+1] in at least r+1 points. The star is r = 0; the Hilton–Milner world is r = 1; the sequence continues — at (7, 3) the sizes read [15, 13, 10, 0], at (5, 3) they read [6, 7, 10, 0] and the winner is r = 2 with 10 = C(5, 3), the whole level, as n < 2k demands. This chapter records the theorem as a gateway — stated, sampled by machine, proved nowhere here — and points the reader at Chapter 7's ◐15 for the exploration.

**Union-closed lore: the frontier one theorem away.** A family 𝓐 is *union-closed* if A ∪ B ∈ 𝓐 for all A, B ∈ 𝓐. Frankl's 1979 conjecture: in any finite union-closed family with at least one nonempty member, some element lies in at least half the members. It is open still — one of the great stubborn problems — and the best proved fraction is Gilmer's constant (3−√5)/2 ≈ 0.3819660112501051 (Gilmer 2022; improved slightly by subsequent authors), a breakthrough obtained by information-theoretic means. Two facts this chapter's own tools can verify. First, the free case: a union-closed family containing a singleton {x} already satisfies the conjecture for x — pair each set avoiding x with its union with {x}; the map is injective, ∪-closedness keeps the partner inside the family, and the avoiding sets are thereby outnumbered. Second, the census: on [3], all 121 nonempty union-closed families (120 with a nonempty member; {∅} alone is vacuous); on [4], all 4,959 (4,958); the singleton lemma on the 4,126 singleton-containing families of [4] — zero failures anywhere. (Survey: arXiv:2306.12351.)

### 4.5 What to learn

Shadow pricing completes the chapter's engine collection. The real parameter x is a *price*: a k-family costing C(x, k) gets no discount at any lower level — every j-shadow costs at least C(x, j) — and the complete families are the only exact price tags, the colex initial segments the only exact minimizers. Three routes to EKR now live in this book: averaging over circles (Chapter 7's Lecture 3), deforming by shifting (its Lecture 5, the last step cited), and pricing the complement mirror (this lecture) — and the third is by far the cheapest, which is a lesson in itself: *before building machinery, ask what the dual object sees for free*. What remains flagged, honestly: the deep-level cascade uniqueness and the thin range it serves — the closing lecture builds the first and completes the second, retiring the appendix's last flag. And the gateways installed here point beyond the course: Hilton–Milner for empty cores, Ahlswede–Khachatrian for all n, Gilmer's constant for union-closed families — the current frontier of the counting world this book has been teaching.

---

## Lecture 5 · Uniqueness Completed: The Shade Route

The last flag closes. Lecture 4 priced shadows, proved the clique form with its equality analysis, and used Daykin's mirror for a second complete proof of EKR — then stopped honestly at uniqueness: the mirror pins the *size* of a maximum family, but the brick it lacked was the statement that a family sitting at the cascade's minimum across many levels at once must be complete. This lecture builds that brick — the deep cascade-uniqueness lemma, in four steps from §4.2's own equality analysis — and spends it on the EKR uniqueness theorem for *every* n > 2k, thin range included. No circles, no shifting, no middle-J transport: the mirror, the j-form, and one squeeze.

### 5.1 From mirror-equality to the exact price

Recall the mirror (§4.3): 𝓕 intersecting and k-uniform on [n], n > 2k, 𝓕* = {[n]∖F : F ∈ 𝓕} uniform of size n − k ≥ k, the disjointness |𝓕| + |∂_k𝓕*| ≤ C(n, k), and the increasing function h(t) = C(t, n−k) + C(t, k) with h(n−1) = C(n, k). Writing |𝓕*| = |𝓕| = C(x, n−k), the j-form feeds |∂_k𝓕*| ≥ C(x, k) into the mirror, and h increasing forces x ≤ n−1: the EKR bound |𝓕| ≤ C(n−1, k−1) — Daykin's proof, complete.

Now suppose the family is *maximum*: |𝓕| = C(n−1, k−1) exactly. Then the parameter is pinned from both sides. The floor: C(x, n−k) = |𝓕| = C(n−1, n−k) with C(·, n−k) increasing gives x ≥ n−1; the cap: x ≤ n−1. So **x = n−1 exactly** — cap meets floor — and the two bounds on the shadow meet in the middle: |∂_k𝓕*| ≥ C(n−1, k) from the j-form and |∂_k𝓕*| ≤ C(n, k) − |𝓕| = C(n−1, k) from the mirror, so

**|∂_k𝓕*| = C(n−1, k) exactly:**

the mirror of a maximum family sits at the j-form's floor at level k, many levels below its uniformity n − k. One more bookkeeping device and the brick is assembled. For each level j with k ≤ j ≤ n−k, write x_j for the *own* real parameter of ∂_j𝓕* — that is, |∂_j𝓕*| = C(x_j, j) — so x_{n−k} = x = n−1 and x_k = n−1 (the shadow at level k costs exactly C(n−1, k)). The j-form applied to the level-j family reads |∂_{j−1}𝓕*| ≥ C(x_j, j−1); comparing with the definition of x_{j−1} and using that binomials increase: **x_{j−1} ≥ x_j — as the level descends, the parameter never decreases**. The chain

x_{n−k} ≤ x_{n−k−1} ≤ … ≤ x_k

is pinned at both ends by n−1, so every level's parameter is n−1: |∂_j𝓕*| = C(n−1, j) for all k ≤ j ≤ n−k. The parameters agree all the way down — but agreeing parameters do not yet say *complete*. The bridge is the next section's lemma.

### 5.2 The deep cascade-uniqueness lemma (four steps)

Everything rests on one corollary of §4.2's equality analysis, worth stating on its own:

**One-level corollary.** Let 𝓖 be r-uniform (r ≥ 2) with |𝓖| = C(x, r) for a real x ≥ r. If |∂𝓖| = C(x, r−1) — equality at the level adjacent to uniformity — then x is an integer and 𝓖 = K^r_x.

*Proof.* Every member of 𝓖 is an r-clique of its own (r−1)-uniform shadow ∂𝓖, so |𝓖| ≤ K(∂𝓖). Since |∂𝓖| = C(x, r−1) with x ≥ r > r−1 ≥ 1, the clique form of §4.2 applied to ∂𝓖 gives K(∂𝓖) ≤ C(x, r) = |𝓖|. Thus K(∂𝓖) = C(x, r) holds with equality. By §4.2's equality characterization (applied to the (r−1)-uniform family ∂𝓖 with parameter x > r−1), x is an integer and ∂𝓖 = K^{r−1}_x on some x-element vertex set U (for r−1 = 1, ∂𝓖 is a set of x = |∂𝓖| singletons, which is also K^1_x with x ∈ ℤ). Every member of 𝓖 has all its (r−1)-subsets inside U, hence is itself a subset of U; since |𝓖| = C(x, r), 𝓖 must consist of all r-subsets of U, so 𝓖 = K^r_x. ∎

**Lemma (deep cascade uniqueness).** Let 𝓖 be r-uniform (r ≥ 2) with |𝓖| = C(x, r) for a real x ≥ r. If for some integer level 1 ≤ j₀ < r the j₀-shadow satisfies |∂_{j₀}𝓖| = C(x, j₀) — equality pinned at a positive lower level — then x is an integer and 𝓖 = K^r_x.

*Proof.* (1) *The chain.* For each level j ∈ {j₀, …, r}, let x_j ≥ j be the real parameter of ∂_j𝓖 defined by |∂_j𝓖| = C(x_j, j) (with ∂_r𝓖 := 𝓖, so x_r = x). Applying the one-step shadow bound to ∂_j𝓖 gives C(x_{j−1}, j−1) = |∂_{j−1}𝓖| ≥ C(x_j, j−1), and since C(·, j−1) is strictly increasing on [j−1, ∞) for every j−1 ≥ j₀ ≥ 1, we obtain x_r ≤ x_{r−1} ≤ … ≤ x_{j₀}. (2) *Both ends equal x.* By hypothesis, C(x_{j₀}, j₀) = |∂_{j₀}𝓖| = C(x, j₀); since j₀ ≥ 1, strict monotonicity of C(·, j₀) on [j₀−1, ∞) forces x_{j₀} = x. (3) *The squeeze.* The monotone chain x = x_r ≤ x_{r−1} ≤ … ≤ x_{j₀} = x is constant, so x_{r−1} = x, i.e. |∂𝓖| = C(x, r−1). (4) *The adjacent-level corollary fires.* By the one-level corollary, x is an integer and 𝓖 = K^r_x. ∎

That is the whole "uniqueness theory of the binomial cascade" the shade route was missing: not a deeper theorem, but the observation that the equality analysis of §4.2 plus a monotone chain *is* the deep statement. Equality pinned at any depth propagates up to the adjacent level, and the adjacent level decides.

**Machine record.** The lemma says deep equality ⟺ complete, and the census confirms both directions at every reachable size, zero exceptions. Deep means: |𝓖| = C(u, k) with u = |∂₁𝓖| the union size, and |∂_j𝓖| = C(u, j) at every level 1 ≤ j < k — the real parameter resolves to the integer u (this is the shortcut the lab uses: no bisection, exact integer arithmetic). The counts: at (6, 3), of the 1,048,575 families exactly **42** are deep, and all 42 are complete — 20 single triples, 15 K³₄, 6 K³₅, and 1 K³₆, one complete family per choice of union set; at (6, 4), 32,767 families, **22** deep, all complete; at (7, 5), 2,097,151 families, **29** deep, all complete — 21 K⁵₅ + 7 K⁵₆ + 1 K⁵₇. And at r = 2 with x = 5, n = 7, a graph costume: of the 352,716 ten-edge graphs on [7], exactly **21** carry at least ten triangles — the clique-form equality K(𝓖) = C(5, 3) — and every one of them is K₅ plus two isolated vertices: the complete family K²₅, in its 21 placements. Deep equality and completeness coincide at every censusable size, which is what a proved lemma and an honest census should agree on. (The lab, Part 5, runs all four hunts with the integer shortcut.)

### 5.3 The star theorem, completed for every n > 2k

**Theorem (EKR uniqueness, complete range).** Let 𝓕 be an intersecting k-uniform family on [n] with k ≥ 1, n > 2k, and |𝓕| = C(n−1, k−1). Then 𝓕 is a star: all members share one fixed element.

*Proof.* Assemble the pieces. (1) *Cap meets floor* (§5.1): x = n−1 exactly and |∂_k𝓕*| = C(n−1, k) exactly. (2) *The squeeze* (§5.2): the parameters of the intermediate shadows are pinned at n−1 across the whole range [k, n−k]; since n > 2k and k ≥ 1, the adjacent level n−k−1 ≥ k ≥ 1 lies in that range, so |∂𝓕*| = C(n−1, n−k−1). (3) *The one-level corollary:* 𝓕* = K^{n−k}_{n−1} — every member of 𝓕* lies inside one fixed (n−1)-set, which must be [n]∖{z} for some z. (4) *Translate back:* F ∈ 𝓕 has [n]∖F ∈ 𝓕* ⊆ K^{n−k}_{n−1}, so [n]∖F ⊆ [n]∖{z}, so z ∈ F: every member of 𝓕 contains z, and |𝓕| = C(n−1, k−1) is the full count of k-sets through z. 𝓕 is the star at z. ∎

With Chapter 7's circle method (the bound) and its uniqueness lecture (the range its induction reached), this closes the EKR arc over the whole of n > 2k — including the thin range 2k < n < 3k, which the circle method crossed by a middle-J transport the book never needed to build. The transport is thereby bypassed, not disproved: Katona's classical proof of the uniqueness theorem walks exactly that road, and the shade route reaches the same summit from the other side. **Flag (ii) retires here**, and the forward pointer Chapter 7's Lecture 4 planted is landed.

*The mirror partition, at equality.* For the star itself the accounting is exact — worth reading as a check that the boundary of the proof is the boundary of the theorem. The star's mirror is the complete family 𝓕* = K^{n−k}_{n−1} inside V₀ = [n]∖{z}, with |𝓕*| = C(n−1, k−1), and — because k ≤ n−k — its k-shadow is *all* the C(n−1, k) k-sets inside V₀. Every k-set of [n] contains z or avoids it: a disjoint cover,

C(n−1, k−1) + C(n−1, k) = C(n, k) — Pascal, machine-checked at (9, 4) 56 + 70 = 126, (5, 2) 4 + 6 = 10, (7, 3) 15 + 20 = 35, (8, 3) 21 + 35 = 56.

*The (9, 4) budget, honestly.* The theorem covers (9, 4): the nine stars, size 56 = C(8, 3), are the only intersecting 4-families of that size. A census proof is out of reach — the book's depth-first hunt over the 126 four-sets of [9] ran some thirty million nodes and never produced a non-star of size 56; its best empty-core partial, 53, is exactly Hilton–Milner's bound at (9, 4) (§4.4's gateway), the largest an empty-core family can be. The census is evidence; the proved lemma is the proof. ◐15 inherits the hunt.

### 5.4 What to learn

The shade route is the book's last path up EKR and the cheapest of the three: no averaging, no shifting, no transport — one disjointness observation, one priced shadow, one squeeze. Its engine pairing deserves a name: §4.2's equality analysis was proved for *one* level, and the deep lemma is nothing but the observation that a monotone chain with pinned endpoints is constant — the squeeze does the work that a deeper theorem might have been asked to do. That is the general lesson about "genuinely deeper" bricks: sometimes the deeper statement is the shallow one, iterated by an invariant. And the specific lesson: when a proof stops for want of a uniqueness statement, price the *dual* object — the complement mirror — and ask what its shadows cost. The three flags the restructure left open are now closed: (iii) by the assembly (Lecture 3), (i) by the mirror (Lecture 4), (ii) here. The counting world this book has been teaching now runs from Sperner to the thin range with every load-bearing proof on the table; what remains beyond the course is gateway material, honestly labeled — Hilton–Milner, Ahlswede–Khachatrian, the union-closed frontier.

---

## The Trick Bag (reference card)

| Pattern | Plain language | Where you met it |
|---------|---------------|------------------|
| **P4 Induction** | Verify the base and run the recursion until a case fires; or induct on a measure every move decreases — the staircase chain, the m-fold merge, the two-case recursion, DeVos's |X+Y| + |X| | L1, L2, L3 |
| **P22 Polynomial method** | One polynomial vanishing on the grid; the weighted-sum identity prices its top coefficient two ways | L1 |
| **P23 Compression / deformation** | Replace the pair by a deformed one that is easier to read: the merge grows A, the e-transform trades B for A — sumset containment and total size preserved | L2, L3 |
| **Price the period, pass to the quotient (lore)** | When the obstruction is a subgroup of periods, quotient it away and price the deficit by its order — Kneser's Move 2 | L2, L3 |
| **The real parameter is a price (lore)** | |𝓖| = C(x, k) buys no discount at any level; every j-shadow costs at least C(x, j), and the complete families are the only exact price tags | L4, L5 |
| **Ask what the dual object sees for free (lore)** | Complement the family before building machinery: intersection becomes containment, and the shadow prices it | L4, L5 |

**Formula box:** staircase |A+B| ≥ |A|+|B|−1 over ℤ; Cauchy–Davenport |A+B| ≥ min(p, |A|+|B|−1) over 𝔽_p — proved twice (the merge/periodicity argument; the weighted-sum identity Σ f/(Π′Π′) = [x^{a−1}y^{b−1}]f, with the grid lemma D1) — and the m-fold min(p, Σ|Aᵢ| − m + 1). Kneser: |A+B| ≥ |A+H| + |B+H| − |H|, H = stab(A+B); weak form: |A|+|B| ≤ |G| ⟹ some proper H with |A+B| ≥ |A|+|B|−|H|, by the two-case e-transform recursion (Case 1: H′ = ⟨B−B⟩ ⊆ stab(A), collapse A+B = A+b₀; Case 2: witnessed transform e = a−b′, A′ = A∪(B+e), B′ = B∩(A−e)); strong form by DeVos: portions Z ⊆ X+Y with |Z|+|stab(Z)| ≥ |X∩Y|+|(X∪Y)+stab(Z)|, Z₀ = (X∩Y)+(X∪Y), the stabilizer-minimal choice, equations (1)(2)(3), the coset-partition contradiction. EGZ: 2n−1 integers contain n with sum ≡ 0 mod n — prime case by pairing plus m-fold C–D, composite by blocks. Shadows: the cascade/colex minimum; Lovász |∂𝓕| ≥ C(x, k−1) from the clique form K(𝓖) ≤ C(x, r+1) (Keevash's proof); the j-form |∂_j𝓖| ≥ C(x, j); equality ⟺ x ∈ ℤ and 𝓖 complete; deep cascade-uniqueness: equality pinned at any lower level squeezes to the adjacent level and forces K^r_x. Daykin mirror: |𝓕| + |∂_k𝓕*| ≤ C(n, k); h(t) = C(t, n−k) + C(t, k) increasing with h(n−1) = C(n, k) ⟹ EKR; at the maximum, cap meets floor: x = n−1, 𝓕* = K^{n−k}_{n−1} ⟹ the star — uniqueness for every n > 2k. Gateways: Hilton–Milner C(n−1, k−1) − C(n−k−1, k−1) + 1; Ahlswede–Khachatrian max over r of |F_r|; Frankl's union-closed conjecture with Gilmer's constant (3−√5)/2 ≈ 0.3819660112501051.

---

## Exercises (graded: ●○○ easy · ●●○ moderate · ●●● tough)

**Easy — one idea, applied directly**

1. ●○○ **The staircase, explicitly.** Take A = {2, 5, 9} and B = {1, 4}: write the witness chain of |A|+|B|−1 strictly increasing sums, then compute A+B in full and check the chain inside it. Where do the extra sums come from?

**Moderate — two ideas, or one tricky step**

2. ●●○ **Invariance forces everything.** Prove the periodicity engine of §1.2: if a nonempty finite S ⊆ 𝔽_p satisfies S + b = S for some b ≠ 0, then S = 𝔽_p. Then run both the one-translate-at-a-time union A ∪ (A + 2) ∪ (A + 3) = A + B and the iterated doubling S₀ = A, S_i = S_{i−1} ∪ (S_{i−1} + b_i) for A = {0, 1}, B = {0, 2, 3} in 𝔽₅, and compare what each step adds.

3. ●●○ **Stabilizers, computed.** For S = {0, 2, 4}, compute stab(S) in Z₈, then recompute it for the same set viewed inside Z₆ and explain the difference. Prove: for the cyclic interval S = {0, 1, …, k−1} in Z_n with 2k−2 < n, stab(S) = {0}, and the staircase is tight: |S+S| = 2k−1 = k+k−1. *Hint: a nonzero period g lies in S−S — an arithmetic condition on cyclic distances.*

4. ●●○ **The two-case recursion, by hand.** Run the recursion of §3.1 on three pairs in Z₆: A = B = {0, 2, 4}; A = {0, 1, 3} with B = {0, 2}; A = {0, 1, 3} with B = {0, 2, 3}. In each, say which case fires, exhibit the canonical witness (a, b′, b) and e = a − b′ at every step, and verify containment and size preservation at each step. *Hint: the second pair terminates in one step, with canonical witness (a, b′) = (0, 0) and b = 2.*

5. ●●○ **Case 1's subgroup, in detail.** At a Case-1 termination of the recursion of §3.1, prove: H′ = ⟨B − B⟩ is contained in stab(A), which is contained in stab(A + B); B lies inside a single coset b₀ + H′; and A + B collapses to the single translate A + b₀. Then say exactly where the hypothesis |A| + |B| ≤ |G| enters the proof, and what fails without it. *Hint: stab(A) = G forces A = G.*

6. ●●○ **The deep lemma on a small stage.** On [6], the star of all triples containing 1 and the complete family K³₅ on {2, 3, 4, 5, 6} cost the same: 10 = C(5, 3). Compute both shadows and explain, via the one-level corollary of §4.2's equality analysis, why only the complete family can sit at the deep-equality price through every level. *Hint: the star's shadow has 15 = C(6, 2) members — its real parameter jumps to 6 at the level below.*

**Tough — several chapter ideas combined**

7. ●●● **The partial-fraction identity.** For A ⊆ 𝔽_p with Π′(a) = Π_{a′∈A, a′≠a}(a − a′), prove Σ_{a∈A} a^i/Π′(a) = 0 for i < |A|−1 and = 1 for i = |A|−1. *Hint: Lagrange interpolation — both sides compute the leading coefficient of the interpolant.*

8. ●●● **The grid lemma, D1.** Prove: a polynomial f(x, y) with deg_x f < |A| and deg_y f < |B| that vanishes on all of A×B is identically zero; and the weighted-sum identity Σ_{a,b} f(a,b)/(Π′_A(a)Π′_B(b)) = [x^{|A|−1}y^{|B|−1}]f for total degree ≤ |A|+|B|−2. *Hint: two-stage Lagrange in x then y; for the identity, run the same computation on the monomial basis.*

9. ●●● **EGZ by hand, prime case.** Take the multiset {0, 0, 1, 1, 1, 2, 2, 4, 4} in 𝔽₅: run the full proof — remove x = 0, opposite-pair the sorted remainder, apply m-fold Cauchy–Davenport to the four 2-element pairs, and exhibit an explicit choice summing to −x. Then check the trivial case on {1, 1, 1, 1, 1, 0, 2, 2, 3}.

10. ●●● **The portion machinery, by hand.** Take X = {0, 1}, Y = {0, 3, 4} in Z₆. Verify that the translate step of §3.3 leaves Y as it is, compute Z₀ = (X ∩ Y) + (X ∪ Y) together with its stabilizer, and list all six portions of X + Y with their stabilizers. Which portions can the stabilizer-minimal choice pick, and why does the proof never need the nontrivial-stabilizer branch on this instance? *Hint: no 3-subset is a portion — a trivial-stabilizer portion needs |Z| ≥ 4, and the {0, 3}-periodic subsets are all even-sized.*

11. ●●● **Star mirror partitions, and the pinned parameter.** Verify the mirror partition for the star at (9, 4), (5, 2), (7, 3), and (8, 3): exhibit 𝓕* as a complete family, compute |𝓕*| and |∂_k𝓕*|, and check the disjoint cover against C(n, k). Then prove the cap-meets-floor step of §5.1: at a maximum-sized family, the increasing function h pins the mirror parameter down to x = n − 1 exactly. *Hint: both C(t, n−k) and C(t, k) increase on [n−k, n−1], and the maximum size is exactly C(n−1, n−k).*

12. ◆ EGZ(4) with a block certificate: from the 7 integers 1, 2, 3, 4, 5, 6, 7, extract three disjoint pairs with even sums, halve them, and use EGZ(2) on the three halves to exhibit four of the original integers with sum divisible by 4. Write the certificate, and verify it directly.

13. ◆ Kneser tight census for Z₆: the group has four subgroups. For each one, exhibit a pair (A, B) with stab(A+B) equal to that subgroup and Kneser tight *in the strong form* |A+B| = |A+H| + |B+H| − |H|, and say which pairs are also tight in the weak form.

14. ◐ **Tight Kneser pairs in Z₄².** The group Z₄² has one-dimensional and two-dimensional subgroups, over F₂-style and cyclic parts. Census pairs (A, B) of small size, compute H = stab(A+B) for each, and hunt for tight instances of every possible subgroup type — coset pairs, arithmetic-progression pairs, and anything that is neither. Is every tight pair a union of cosets of H in both arguments, or does the census find a genuinely ragged example?

15. ◐ **The thin range at (9, 4), hunted.** Uniqueness at (9, 4) — that the nine stars, size 56 = C(8, 3), are the *only* intersecting 4-families of that size — is a theorem of §5.3, so a machine hunt can only illustrate. Hunt anyway: search depth-first over the 126 four-sets of [9], extending an intersecting family one member at a time, and record the largest empty-core family you meet. The book's own search — some thirty million nodes deep — tops out at 53, exactly the Hilton–Milner bound at (9, 4), the largest an empty-core family can be; no non-star of size 56 exists to be found, and the proved lemma, not the census, is what carries that. What does the search's difficulty teach about census evidence in the middle range 2k < n < 3k?

**Graded backfill — five more, each hint naming its pattern**

16. ●○○ **The m-fold staircase, sharp and slack.** Prove the m-fold corollary of §1.4 yourself: for nonempty A₁, …, A_m ⊆ 𝔽_p, |A₁ + A₂ + … + A_m| ≥ min(p, Σ|A_i| − m + 1), merging two summands at a time and checking that the min(p, ·) caps compose through the induction. Then calibrate it on 2-element summands in 𝔽₇: with m = 3 the bound reads 4, with m = 4 it reads 5. Verify that {0,1}³ and {0,1}⁴ attain equality, exhibit a triple with slack, and run the census: all 9,261 ordered triples and all 194,481 ordered quadruples of 2-subsets of 𝔽₇. How many triples are tight, how many fill the whole field — and is the pure arithmetic progression {0,1}³ the typical tight shape, or does the census surprise you? *Hint: P4 — merge two summands at a time, the caps composing exactly as §1.4 shows; then the affine maps x ↦ ux + v of 𝔽₇ classify what tightness looks like.*

17. ●●○ **The engine's regime boundary.** The polynomial proof of §1.3 builds C of size a+b−2 containing A+B, and the contradiction needs the count C(a+b−2, a−1) nonzero mod p. Prove both sides of the boundary: (i) if a+b−2 ≤ p−1, the count is never ≡ 0 mod p; (ii) if a+b−2 ≥ p — with a, b ≤ p, as C–D itself forces — it is always ≡ 0: the engine provably cannot fire outside its regime, the boundary is a wall, not a slope. Verify the whole-field costume: at a+b−2 = p the set C would be all of 𝔽_p, Π_{c∈𝔽_p}(x+y−c) = (x+y)^p − (x+y), and the top coefficient is C(p, a−1) ≡ 0. Then the disassembly: p = 7, A = {0,1,3}, B = {0,2} — a pair with staircase slack. For all 35 choices of C ⊆ 𝔽₇ with |C| = 3, run the weighted-sum identity on f(x, y) = Π_{c∈C}(x+y−c): what does it return, and why is no contradiction available? *Hint: P22 — price the top coefficient two ways, then ask what its nonvanishing costs: which factorial does the regime protect, and who owns the other side of the boundary?*

18. ●●○ **A tight mirror that lies.** Daykin's mirror at (6, 2): 𝓕 intersecting and 2-uniform on [6], 𝓕* the family of complements (4-sets), and |𝓕| + |∂₂𝓕*| ≤ C(6, 2) = 15. Take the triangle 𝓕 = {12, 13, 23}: compute 𝓕*, compute ∂₂𝓕* — the pairs disjoint from some member of 𝓕 — and watch the mirror split 15 exactly, even though the triangle is far from maximum (the stars have 5). Explain the lie: mirror-equality and j-form tightness are independent. Price the triangle's mirror by its real parameter (C(x, 4) = 3), read the j-form floor at level 2, and measure the slack; then do the same for a star and watch the floor met exactly — cap meets floor only at a maximum family. Run the census: all 192 intersecting 2-families on [6] — which split the mirror exactly, and what are they? *Hint: ask what the dual object sees for free — complement first, price the shadow second; a tight mirror can still sit at a loose x.*

19. ●●○ **The cap is sharp: the census of near-misses.** EGZ needs 2n−1 integers; prove 2n−2 fails: the multiset {0^(n−1), 1^(n−1)} contains no n-subset with sum ≡ 0 mod n. Generalize the bookkeeping to any two-value multiset {a^(n−1), b^(n−1)}: which differences a − b dodge every zero-sum n-subset, and which never do? Then hunt for exotic avoiders: census every multiset of size 2n−2 over Z_n for n = 3 through 9 — 873,912 multisets in all — and classify what you find. Is every avoider two-value? How many are there at each n, and does a formula read them off? *Hint: the pairing lemma's sorted bookkeeping (P23): a zero-sum n-subset takes j copies of one value and n−j of the other; the gcd prices which differences can dodge.*

20. ●●● **The clique form in graph costume: ten edges, ten triangles.** Specialize the clique form to r = 2: a graph with m = C(x, 2) edges (x real, x ≥ 2) has at most C(x, 3) triangles. Run the lecture's proof in costume — the link of v is its neighborhood, the link ceiling counts edges inside N(v), the degree ceiling counts edges avoiding v — and prove the equality analysis at r = 2: t = C(x, 3) forces x to be an integer and the graph to be K_x plus isolated vertices. Now the hunt: on [7], ten edges. x = 5, so t ≤ 10; census all 352,716 ten-edge graphs, verify exactly 21 attain the bound — each one K₅ plus two isolated vertices, 21 = C(7, 5) placements — and read the distribution honestly: where does it jump? As a bonus, run the [6] costume end-to-end: all 32,767 nonempty graphs, equality exactly on the 57 complete families — the same 57 the shadow census of §4.1 priced at k = 2. *Hint: the real parameter is a price — C(x, 2) edges buy at most C(x, 3) triangles — and the ledger is P4's double count 3t = Σ_v K(v).*

---

## Answers to the Exercises

**A1.** The witness chain climbs the b₁ column then walks the a_s row: 2+1 = 3 < 5+1 = 6 < 9+1 = 10 < 9+4 = 13 — four = 3+2−1 strict sums. The full sumset is {3, 6, 9, 10, 13}, size 5 ≥ 4. The chain sits inside it; the extra element **9** (= 5+4) — and the duplicate 6 (= 2+4, already reached as 5+1) — come from the grid's interior cells above the staircase: the staircase witnesses the *minimum*; interior cells are surplus. (Part 1 runs the same check on Figure 1's data, A = {1, 2, 4}, B = {1, 3}.)

**A2.** If S + b = S with b ≠ 0 in 𝔽_p, then S + mb = S for every integer m, and the multiples of b exhaust 𝔽_p (b has order p, p prime). So S is invariant under every translation — and a nonempty translation-invariant subset of a transitive group is everything: pick s ∈ S; for any y ∈ 𝔽_p, y = s + (y−s) with y−s a multiple of b, so y ∈ S. S = 𝔽_p. The merge for A = {0, 1}, B = {0, 2, 3} in 𝔽₅, one translate at a time: S = {0, 1}; +2 gives {2, 3}, union {0, 1, 2, 3} — gain 2; +3 gives {3, 4}, union 𝔽₅ — gain 1. Every step gains, and the total 5 = |A+B| ≥ min(5, 2+3−1) = 4 ✓. The iterated doubling runs the same trajectory: S₀ = A = {0, 1}, step 1 forms S₁ = S₀ ∪ (S₀ + 2) = {0, 1, 2, 3} (gain 2), and step 2 forms S₂ = S₁ ∪ (S₁ + 3) = {0, 1, 2, 3} ∪ {3, 4, 0, 1} = 𝔽₅ (gain 1) — the doubling's added translate S₁ + 3 = {0, 1, 3, 4} contains the one-translate addition A + 3 = {3, 4}, so on this instance both routes gain the same fresh elements at every step. (Part 1's merge monitor runs exactly S_i = S_{i−1} ∪ (S_{i−1} + b_i): 9,759 zero-gain steps over 8,624 processes — every single one with S_{i−1} already equal to 𝔽_p.)

**A3.** Since 0 ∈ S = {0, 2, 4}, any period g ∈ stab(S) must satisfy g = 0 + g ∈ S, so stab(S) ⊆ {0, 2, 4}. In Z₈: S + 2 = {2, 4, 6} ≠ S and S + 4 = {4, 6, 0} ≠ S — stab is trivial, **{0}**. In Z₆: S + 2 = {2, 4, 0} = S and S + 4 = {4, 0, 2} = S, so stab = **{0, 2, 4}** (≅ Z₃). The same set, two different ambient groups: in Z₆ the element 2 has order 3 and S is its whole orbit — a subgroup; in Z₈ the order of 2 is 4 and the orbit {0, 2, 4, 6} has size 4 > |S|. Stabilizers are group-theoretic, not set-theoretic. For the cyclic interval S = {0, …, k−1} in Z_n with 2k−2 < n, represent Z_n by {0, 1, …, n−1}: a nonzero period g satisfies 0 ∈ S ⟹ g = 0 + g ∈ S, so 1 ≤ g ≤ k−1, and likewise −g ∈ stab(S) gives n − g ∈ S, so 1 ≤ n − g ≤ k−1; summing, n = g + (n−g) ≤ 2k−2 — contradicting the hypothesis. So stab = {0}, and S + S = {0, …, 2k−2} with no wraparound modulo n: size 2k−1 = k+k−1, the staircase tight.

**A4.** The first pair is Case 1 outright: B − B = {0, 2, 4} = stab(A), so no witness exists — every a + b − b′ lands back in A = {0, 2, 4}. H′ = {0, 2, 4}, B ⊆ 0 + H′, and A + B collapses to A + 0 = {0, 2, 4}: |A + B| = 3 = 3 + 3 − 3 ✓. The second pair takes one step. The canonical scan finds (a, b′) = (0, 0) admitting b = 2 (0 + 2 − 0 = 2 ∉ A), so e = 0: A′ = A ∪ (B + 0) = {0, 1, 2, 3}, B′ = B ∩ (A − 0) = {0}. Size preservation 4 + 1 = 3 + 2 ✓; containment A′ + B′ = {0, 1, 2, 3} ⊆ A + B = {0, 1, 2, 3, 5} ✓; strict decrease 1 < 2 ✓. Now |B′| = 1: the staircase base reads |A + B| ≥ |A′ + B′| = 4 ≥ 4. The third pair takes two. Step 1: the same witness (0, 0, 2), e = 0, but now B′ = {0, 2, 3} ∩ {0, 1, 3} = {0, 3}, with A′ = {0, 1, 2, 3} — preservation 4 + 2 = 3 + 3 ✓, strict decrease 2 < 3 ✓, containment A′ + B′ = {0, 1, 2, 3, 4, 5} ⊆ A + B = {0, 1, 2, 3, 4, 5} ✓. Step 2: the scan on (A′, B′) finds (a, b′) = (1, 0) admitting b = 3 (1 + 3 − 0 = 4 ∉ A′), so e = 1: A″ = A′ ∪ (B′ + 1) = {0, 1, 2, 3, 4}, B″ = B′ ∩ (A′ − 1) = {0} — preservation 5 + 1 = 4 + 2 ✓, containment ✓ — and the base reads |A + B| ≥ |A″ + B″| = 5 ≥ 5; the true sumset is all of Z₆, size 6 ≥ 5. Both descents end at the staircase base; the census counts them among Z₆'s 3,097 base terminations (against 872 Case-1 terminations).

**A5.** No witness means: for every a ∈ A and b, b′ ∈ B, a + b − b′ ∈ A — that is, A + (b − b′) ⊆ A for every difference. A is finite and translation by b − b′ is injective, so |A + (b − b′)| = |A| forces A + (b − b′) = A: every difference stabilizes A. So B − B ⊆ stab(A), and stab(A) being a subgroup gives H′ = ⟨B − B⟩ ⊆ stab(A), with |H′| ≤ |stab(A)| ≤ |A|. The chain to the sumset: g + A = A gives g + (A + B) = (g + A) + B = A + B, so stab(A) ⊆ stab(A + B). The coset: fixing b₀ ∈ B, every b ∈ B has b − b₀ ∈ B − B ⊆ H′, so B ⊆ b₀ + H′ — one H′-coset, and in particular |B| ≤ |H′|. The collapse: A + B ⊆ A + (b₀ + H′) = (A + b₀) + H′ = A + b₀ (the last step because H′ stabilizes A, hence A + b₀), and A + b₀ ⊆ A + B since b₀ ∈ B: so A + B = A + b₀, |A + B| = |A|. The bound: |A + B| = |A| = |A| + |B| − |B| ≥ |A| + |B| − |H′|. Properness is where the hypothesis enters: |H′| ≤ |stab(A)| ≤ |A| ≤ |G| − |B| ≤ |G| − 1, so H′ ⊊ G (equivalently: stab(A) = G would force A = G — a nonempty finite set stabilized by every element is the whole group — impossible when |A| ≤ |G| − 1, which |A| + |B| ≤ |G| with B nonempty grants). Without the hypothesis, A = G is a legal pair; then stab(A) = G, H′ = G is not proper, and the bound degenerates to |G| ≥ |A| + |B| − |G| — true but vacuous. That is exactly why the weak form carries the size hypothesis and the strong form (§3.3) does not.

**A6.** The star: ten triples through 1, |𝓖| = 10 = C(5, 3), so its price parameter is x = 5. Its shadow: every pair inside a triple through 1 — the five pairs containing 1 and the ten pairs among {2, …, 6} — fifteen = C(6, 2), against the j-form floor C(5, 2) = 10. Deep equality fails at the first level down: the star pays the minimum at level 3 but not at level 2. The complete family K³₅ on {2, …, 6} costs the same 10; its shadow is the ten pairs of the 5-set and its 1-shadow the 5 singletons = C(5, 1): deep equality at every positive level. The one-level corollary of §4.2's equality analysis explains the asymmetry: |𝓖| = C(x, k) *with* |∂𝓖| = C(x, k−1) forces x an integer and 𝓖 = K^k_x. The star fails the hypothesis (15 ≠ 10) and is not even a candidate for the deep-equality price; any family that *is* a candidate — sitting at the cascade's minimum at the uniformity level and the level below — is complete by the corollary. The deep lemma of §5.2 adds the propagation: equality pinned at *any* positive lower level squeezes up to the adjacent level, so deep equality at any positive depth forces completeness.

**A7.** The Lagrange basis polynomial L_a(x) = Π_{a′≠a}(x−a′)/Π′(a) has degree |A|−1, leading coefficient 1/Π′(a), and satisfies L_a(a′) = [a = a′]. For i ≤ |A|−1, the polynomial x^i has degree < |A| = the number of nodes, so it equals its own interpolation: x^i = Σ_{a∈A} a^i L_a(x) identically. Match leading coefficients: the left side contributes [i = |A|−1], the right side Σ a^i/Π′(a). Machine check: 15,011 evaluations over 𝔽₅–𝔽₁₃, zero exceptions.

**A8.** *Grid lemma (D1):* write f(x, y) = Σ_{i=0}^{|A|−1} c_i(y) x^i, where each coefficient c_i(y) is a polynomial in y of degree < |B|. For each fixed b ∈ B, the univariate polynomial f(x, b) has degree < |A| and vanishes at all |A| elements a ∈ A — |A| roots — so f(x, b) ≡ 0 in x; that is, c_i(b) = 0 for every 0 ≤ i < |A|. Consequently each c_i(y) has degree < |B| and vanishes at all |B| elements b ∈ B — |B| roots — so c_i ≡ 0: f ≡ 0. *Weighted-sum identity:* here we assume only total degree deg f ≤ |A|+|B|−2 (not deg_x f < |A|). Write f(x, y) = Σ_{i+j ≤ |A|+|B|−2} f_{ij} x^i y^j. By linearity, Σ_{a∈A, b∈B} f(a, b)/(Π′_A(a)Π′_B(b)) = Σ_{i+j ≤ |A|+|B|−2} f_{ij}·(Σ_{a∈A} a^i/Π′_A(a))·(Σ_{b∈B} b^j/Π′_B(b)). For each term with i + j ≤ |A|+|B|−2: if i < |A|−1, then Σ_{a∈A} a^i/Π′_A(a) = 0 by A7 applied to A; if i ≥ |A|, then j ≤ |A|+|B|−2−i ≤ |B|−2 < |B|−1, so Σ_{b∈B} b^j/Π′_B(b) = 0 by A7 applied to B; and if i = |A|−1, then j ≤ |B|−1, so the A-sum is 1 and the B-sum is [j = |B|−1] by A7. Only (i, j) = (|A|−1, |B|−1) survives, giving f_{|A|−1,|B|−1} = [x^{|A|−1}y^{|B|−1}]f. Machine check: 184 exact grid reconstructions and 900 random polynomials (including the terms with i ≥ |A|, which die by degree: j ≤ |B|−2).

**A9.** No value occurs 5 times, so the trivial case is off. Remove x = 0; the sorted remainder is 0, 1, 1, 1, 2, 2, 4, 4 — no value more than 4 = m times, so opposite pairing (element i with element i+4) gives the pairs **(0, 2), (1, 2), (1, 4), (1, 4)**, each with distinct entries. The m-fold Cauchy–Davenport bound: min(5, 2·4 − 4 + 1) = 5, so the choice-sumset is all of 𝔽₅ — in particular −x = 0 is a choice-sum. One: 0 + 2 + 4 + 4 = 10 ≡ 0 (mod 5). The five elements 0, 0, 2, 4, 4 sum to 10 ≡ 0 ✓. Trivial case {1,1,1,1,1,0,2,2,3}: the value 1 occurs 5 = p times; those five sum to 5 ≡ 0 (mod 5) ✓.

**A10.** The canonical translate leaves Y alone (y = 0): X ∩ Y = {0}, X ∪ Y = {0, 1, 3, 4}, so Z₀ = (X ∩ Y) + (X ∪ Y) = {0, 1, 3, 4} with stab(Z₀) = {0, 3}, and X + Y = {0, 1, 3, 4, 5}. The portion test reads |Z| + |stab(Z)| ≥ |X∩Y| + |(X∪Y) + stab(Z)|: for Z₀, 4 + 2 = 6 ≥ 1 + 4 = 5 ✓ (the union is already {0, 3}-invariant, so (X∪Y) + stab(Z₀) = X ∪ Y). The six portions: Z₀ itself, with stabilizer {0, 3}; the four 4-subsets {0, 1, 3, 5}, {0, 1, 4, 5}, {0, 3, 4, 5}, {1, 3, 4, 5}, each passing as 4 + 1 ≥ 1 + 4 = 5, all with trivial stabilizer; and the full sumset X + Y = {0, 1, 3, 4, 5}, with trivial stabilizer: 5 + 1 ≥ 5 ✓. No 3-subset passes (3 + 1 = 4 < 5), and no odd-sized set carries the {0, 3} stabilizer (its cosets are the pairs {g, g+3}), so every portion here has either the full {0, 3} or the trivial stabilizer. The proof's choice — a portion whose stabilizer is minimal by inclusion — therefore lands on a trivial-stabilizer portion, and the H ≠ {0} branch never fires on this instance. The machine sweep of §3.3 confirms this on every one of the 39,449 aperiodic pairs it covers: a trivial-stabilizer portion always exists, so the minimal choice is always trivial — the nontrivial branch is carried by the proof, not by the data.

**A11.** For the star at z, every complement [n]∖F avoids z, so 𝓕* consists of (n−k)-sets inside the (n−1)-set V₀ = [n]∖{z}; being maximum-sized, it is *all* of them: 𝓕* = K^{n−k}_{n−1}, with |𝓕*| = C(n−1, k−1). And since k ≤ n−k, every k-set inside V₀ extends to an (n−k)-set inside V₀, so ∂_k𝓕* is *all* C(n−1, k) k-sets of V₀. The accounting is a disjoint cover: every k-set of [n] either contains z (a star member, in 𝓕) or avoids z (in ∂_k𝓕*), and the two families are disjoint — so |𝓕| + |∂_k𝓕*| = C(n−1, k−1) + C(n−1, k) = C(n, k) exactly. Machine-verified: (9, 4) 56 + 70 = 126, (5, 2) 4 + 6 = 10, (7, 3) 15 + 20 = 35, (8, 3) 21 + 35 = 56 — every partition a disjoint cover. The cap-meets-floor step: at a maximum family, |𝓕| = C(x, n−k) = C(n−1, k−1) = C(n−1, n−k), and the mirror inequality plus the j-form give h(x) = C(x, n−k) + C(x, k) ≤ C(n, k) = h(n−1), with h strictly increasing on [n−k, n−1] (both binomials increase there) — so x ≤ n−1. The floor: C(x, n−k) = C(n−1, n−k) with C(·, n−k) increasing forces x ≥ n−1. Cap meets floor: **x = n−1 exactly**, and with it |∂_k𝓕*| = C(n−1, k) — the shadow pinned at the j-form's floor. §5.2's squeeze carries the pin up to the adjacent level, and the one-level corollary finishes: 𝓕* is complete, so 𝓕 is the star.

**A◆12.** Blocks with even sums: (1, 3) sum 4, (2, 4) sum 6, (5, 7) sum 12 — three disjoint pairs covering six of the seven integers, each sum ≡ 0 mod 2 ✓ (2m−1 = 3 blocks with n = 2, m = 2, extracted while j ≤ 2m−2 = 2 ✓). Halve: 2, 3, 6. EGZ(2) on these three integers: two with even sum — 2 and 6 ✓. The corresponding blocks (1,3) and (5,7): four integers **{1, 3, 5, 7}** with sum 16 ≡ 0 (mod 4) ✓ — verified directly: 16 mod 4 = 0. Certificate complete: blocks, halves, EGZ(2) selection, union.

**A◆13.** Z₆ has four subgroups. Tight pairs, strong form |A+B| = |A+H| + |B+H| − |H|:

- H = {0}: A = B = {0, 1}: A+B = {0, 1, 2}, and 3 = 2+2−1 ✓ — tight in both forms.
- H = {0, 3}: A = B = {0, 3}: A+B = {0, 3}, and 2 = 2+2−2 ✓ — both forms.
- H = {0, 2, 4}: A = B = {0, 2, 4}: A+B = {0, 2, 4}, and 3 = 3+3−3 ✓ — both forms; the coset pair of §2.2.
- H = Z₆: A = {0, 1, 2}, B = {0, 3, 4, 5}: A+B = Z₆ (check: 2+0 = 2, 2+4 = 0, 2+5 = 1, 0+3 = 3, 0+4 = 4, 0+5 = 5), and 6 = 6+6−6 ✓ — strong-tight; the weak form reads 6 ≥ 3+4−6 = 1, slack. (For weak tightness at H = Z₆ take A = B = Z₆: 6 = 6+6−6.)

The pattern the census surfaces: with H = {0} the tight pairs are arithmetic progressions (staircase shape); with H nontrivial they are coset pairs — unions of H-cosets; the full-group case is strong-tight by saturation. Part 1's Z₆ census: 3,969 pairs, zero violations, 1,004 tight.

**A16.** The induction merges the tail first: |A₂ + … + A_m| ≥ min(p, s − m + 2) with s = Σ_{i≥2}|A_i|, by hypothesis; then the two-summand bound prices |A₁ + (A₂ + … + A_m)| ≥ min(p, |A₁| + min(p, s − m + 2) − 1). The caps compose: if s − m + 2 ≥ p, the inner family is at the cap and the outer min is p, while Σ|A_i| − m + 1 ≥ p + |A₁| − 1 ≥ p — both sides p; otherwise the inner family has size ≥ s − m + 2, and the outer min is at least min(p, |A₁| + s − m + 1) = min(p, Σ|A_i| − m + 1), min(p, ·) being monotone. ∎ The calibration: {0,1}³ gives {0, 1, 2, 3} — 4 = min(7, 6 − 3 + 1), equality; {0,1}⁴ gives {0, 1, 2, 3, 4} — 5 = min(7, 8 − 4 + 1), equality (and in 𝔽₅, {0,1}³ gives 4 = min(5, 4) — equality against the cap itself). Slack: {0,1} + {0,2} + {0,4} = {0, 1, 2, 3, 4, 5, 6} — the whole field, against a bound of 4. The census: all 9,261 ordered triples of 2-subsets of 𝔽₇ — zero violations, 1,029 tight (choice-sumset of size exactly 4), 2,058 full (all of 𝔽₇), the remaining 6,174 in between; all 194,481 ordered quadruples — zero violations, 7,203 tight (exactly 5); and 250,047 ordered triples of subsets of sizes up to 3 — zero violations again. The surprise is in the shapes: under the 42 affine maps x ↦ ux + v of 𝔽₇, closed under reordering of the summands, the 1,029 tight triples sort into just 8 types, and the pure AP triple {0,1}³ is the rarest of them — 21 of 1,029, its orbit halved by the stabilizer x ↦ 6x + 1, which swaps 0 and 1. The largest type — 252 of 1,029 — is the mixed shape ({0,1}, {0,6}, {2,3}): {0,1} + {0,6} = {0, 1, 6}, and adding {2, 3} gives {1, 2, 3, 4}: tight, and visibly not an affine image of a triple with three equal summands, since affine maps preserve coincidences. Three one-repeat types sit at 126 each — ({0,1}, {0,1}, {2,3}) gives {2, 3, 4, 5} — and four all-distinct types complete the census: the mixed shape at 252 and three at 126, among them the spread ({0,1}, {2,3}, {4,5}) with choice-sumset {0, 1, 2, 6}. The lesson: the staircase minimum is an affine world, not a single-progression one — equality at the m-fold bound occurs whenever the m summands are arithmetic progressions sharing a common nonzero difference d ∈ 𝔽_p^×, but the mixed shapes show that sufficiency is not necessity: tightness does not mean arithmetic progressions, and equality at the m-fold bound is a whole equivalence class of shapes wide.

**A17.** (i) The ledger: C(a+b−2, a−1) · (a−1)! · (b−1)! = (a+b−2)!. In the regime a+b−2 ≤ p−1 every factor on the right is below p, so p divides nothing — and since the binomial times the two smaller factorials rebuilds the factorial, p ∤ C(a+b−2, a−1). (ii) Beyond, C–D's own constraints a, b ≤ p put p ≤ a+b−2 ≤ 2p−2: the numerator factorial carries exactly one factor p (no second multiple fits below 2p), while (a−1)! and (b−1)! stop short of p — so p divides the binomial exactly once, always. The count is identically zero mod p on the far side: the engine cannot fire there even in principle. Machine check: every prime p ≤ 19, all 1 ≤ a, b ≤ p — nonzero throughout the regime, zero at the boundary and beyond, zero exceptions in either direction. The whole-field costume: Π_{c∈𝔽_p}(z − c) = z^p − z, coefficients verified for every p ≤ 19 — so at a+b−2 = p the engine's polynomial is (x+y)^p − (x+y), its top coefficient C(p, a−1) ≡ 0, and the would-be contradiction reads 0 = 0. The disassembly: {0,1,3} + {0,2} = {0, 1, 2, 3, 5} — size 5 against the staircase bound 4, so no 3-set can contain the sumset. For each of the 35 choices of C the weighted-sum identity returns C(3, 2) = 3 mod 7 — the engine always tells the truth — and f vanishes on the whole grid for none of them: the vanishing hypothesis the contradiction feeds on is exactly what a slack pair refuses to supply. Cauchy–Davenport itself holds on both sides of the wall: exhaustive over the 961 ordered pairs of nonempty subsets of 𝔽₅ (811 tight) and the 16,129 of 𝔽₇ (9,857 tight), plus 200,000 sampled pairs of 𝔽₁₁ — zero violations anywhere. The moral: the polynomial proof owns a + b ≤ p + 1 and provably dies on a + b ≥ p + 2, where the periodicity proof takes over — the two proofs split 𝔽_p at exactly a + b = p + 1. The theorem's min(p, ·) is not a convenience; it is the seam between the two proofs.

**A18.** The triangle's mirror: 𝓕* = {3456, 2456, 1456}, and a pair lies in the shadow exactly when it sits inside one of these 4-sets — the three pairs of {4, 5, 6} and the nine pairs crossing from {1, 2, 3} to {4, 5, 6} — twelve in all. So |𝓕| + |∂₂𝓕*| = 3 + 12 = 15: the mirror splits C(6, 2) exactly. Yet EKR caps 𝓕 at C(5, 1) = 5, and the triangle has 3 — sub-maximum with a perfect mirror. The explanation: the mirror inequality and the j-form floor are independent constraints. Price the triangle's mirror: C(x, 4) = 3 gives x ≈ 4.63, so the j-form floor at level 2 is C(x, 2) ≈ 8.40 — and the shadow actually costs 12, a slack of ≈ 3.60. Slack in the j-form is what lets x sit below n − 1 = 5 at a mirror-exact family: h's monotonicity only ever says x ≤ n − 1, and a loose floor never pushes back. At a star both ends pin: |𝓕| = 5 = C(5, 4) makes x = 5 exactly, and the shadow is the ten pairs of {2, …, 6} — the complete family K²₅ — costing C(5, 2) = 10 on the nose: cap meets floor, the §5.1 pin, and the mirror partition reads C(5, 1) + C(5, 2) = C(6, 2) — Pascal at the star, §5.3's accounting at n = 6. The census: all 192 intersecting 2-families of [6] (the empty family included) satisfy the mirror — zero violations — and exactly 26 split it exactly: the 6 stars, which are the 6 maximum families, and the 20 triangles, nothing else. The j-form slack, machine-measured on all 26: zero on every star, ≈ 3.60 on every triangle. The lesson: mirror-equality is bookkeeping; maximality is a price. The EKR bound lives in h's monotonicity, not in the mirror's arithmetic — a tight mirror at a loose x is the census's standing warning against reading equality as extremality.

**A19.** The canonical near-miss: an n-subset of {0^(n−1), 1^(n−1)} must take j zeros and n − j ones with 1 ≤ j ≤ n − 1 — neither value alone has n copies — so its sum is n − j with 1 ≤ n − j ≤ n − 1, never ≡ 0 mod n. The same bookkeeping prices every two-value multiset {a^(n−1), b^(n−1)}: an n-subset takes j copies of a and n − j of b, 1 ≤ j ≤ n − 1, and the sum is ja + (n−j)b ≡ j(a−b) mod n. If gcd(a−b, n) = 1, then j(a−b) ≡ 0 forces j ≡ 0 — out of range — and the multiset avoids every zero-sum n-subset. If d = gcd(a−b, n) > 1, then j = n/d lands in range and (n/d)(a−b) ≡ 0 mod n: the multiset fails. So the two-value world splits cleanly: coprime differences dodge, non-coprime differences never do. The census hunts for anything else, and finds nothing: every multiset of size 2n−2 over Z_n for n = 3 through 9 — 15 + 84 + 495 + 3,003 + 18,564 + 116,280 + 735,471 = 873,912 multisets — and the avoiders are exactly the two-value coprime ones: zero exotic exceptions, zero non-coprime survivors. The counts read 3, 4, 10, 6, 21, 16, 27 — exactly n·φ(n)/2 at every n: n translations, φ(n) coprime partners, halved for the unordered pair. Divide the labor honestly, as ◐15 does at (9, 4): both two-value directions are proved above; the absence of exotics is census evidence through n = 9 — and is in fact a known theorem of Gao / Savchev–Chen in zero-sum theory, so the classification it supports (avoiders are two-value with coprime difference, nothing else) is not merely census here. The lesson: the EGZ cap is not merely sharp; one element below it, the landscape collapses to a two-value world priced by a gcd.

**A20.** The r = 2 specialization, in costume: the link L(v) is the neighborhood N(v), a 1-uniform family of size d(v) = C(y_v, 1), and its cliques are the pairs inside it, so the link ceiling reads K(v) ≤ C(d(v), 2) = d(v)(y_v − 1)/2 — triangles through v are edges inside N(v). The degree ceiling: deleting v from a triangle through v gives an edge avoiding v, injectively — K(v) ≤ m − d(v). The per-vertex price: if d(v) ≤ x − 1, the link ceiling gives K(v) ≤ d(v)(d(v) − 1)/2 ≤ d(v)(x − 2)/2 = (x/2 − 1)·d(v); if d(v) > x − 1, the degree ceiling gives K(v) ≤ m − d(v) < C(x, 2) − (x − 1) = (x−1)(x−2)/2 < (x/2 − 1)·d(v). Summing, 3t = Σ_v K(v) ≤ (x/2 − 1)·Σ_v d(v) = (x/2 − 1)·2m = (x − 2)·x(x−1)/2 = 3·C(x, 3): **t ≤ C(x, 3).** For x > 2, equality forces every active vertex into the first case at its boundary — d(v) = x − 1 — and then Σ_v d(v) = 2m = x(x−1) counts exactly x active vertices: x is an integer, and C(x, 2) edges on x vertices is K_x, plus isolated vertices (at the edge x = 2, one edge is K₂ with t = 0 = C(2, 3)). ∎ The hunt: on [7], m = 10 = C(5, 2), so t ≤ C(5, 3) = 10. The census over all 352,716 ten-edge graphs: the maximum 10 is attained exactly 21 times, and every attainer is K₅ plus two isolated vertices — C(7, 5) placements, the equality analysis walking in costume. The honest distribution: triangle counts run 0 through 7 (7 is reached by 2,310 graphs), then nothing at 8, nothing at 9, and the 21 at 10 — the summit is isolated, a gap of two below it. The ceilings are census-clean everywhere: K(v) ≤ 10 − d(v) and K(v) ≤ (3/2)·d(v) hold at every vertex of all 352,716 graphs, zero violations. The [6] bonus: all 32,767 nonempty graphs satisfy t ≤ C(x, 3) with x = (1 + √(1+8m))/2, and equality holds exactly on the 57 complete families — 15 single edges (t = 0 = C(2, 3)), 20 triangles, 15 copies of K₄, 6 of K₅, 1 of K₆. These are the same 57 that the §4.1 census found as the shadow's equality cases at k = 2: at r = 2 the clique costume and the shadow costume are one theorem, their equality cases literally coinciding — a complete graph is the only shape that pays exactly C(x, 2) for its edges, C(x, 3) for its triangles, and x for its vertex set. Machine check: zero violations throughout both censuses; every equality case complete in both.

---

## Computational Lab (verified)

### Part 1 — Sumsets: the staircase, Cauchy–Davenport, Kneser, and the e-transform

```python
from math import comb
from itertools import combinations

# Staircase witnesses: Figure 1 and Exercise 1 (A1)
for A, B in [([1, 2, 4], [1, 3]), ([2, 5, 9], [1, 4])]:
    chain = [a + B[0] for a in A] + [A[-1] + b for b in B[1:]]
    print(chain, sorted({a + b for a in A for b in B}))

def elems(mask, p): return [i for i in range(p) if mask >> i & 1]

# Cauchy-Davenport by periodicity / e-transform induction on |B| (1.2)
def cd_etransform_trace(A, B, p):
    As, Bs = set(A), set(B)
    if not As or not Bs: return As, Bs
    while len(Bs) > 1 and len(As) < p:
        b0, b1 = sorted(Bs)[:2]
        d = (b1 - b0) % p
        a = next(x for x in sorted(As) if (x + d) % p not in As)
        e = (a - b0) % p
        As, Bs = As | {(b + e) % p for b in Bs}, {b for b in Bs if (b + e) % p in As}
    return As, Bs

cd_pairs = cd_viol = cd_tight = 0
for p, cap in [(2, 2), (3, 3), (5, 5), (7, 7), (11, 4), (13, 3)]:
    subs = [m for m in range(1, 2**p) if bin(m).count("1") <= cap]
    for Am in subs:
        for Bm in subs:
            a, b = elems(Am, p), elems(Bm, p)
            s = {(x + y) % p for x in a for y in b}
            bound = min(p, len(a) + len(b) - 1)
            cd_pairs += 1; cd_viol += len(s) < bound; cd_tight += len(s) == bound
print(cd_pairs, cd_viol, cd_tight)

# Iterated merge monitor S_i = S_{i-1} | (S_{i-1} + b_i) (1.2 and A2)
proc = zg = zg_full = holds = 0
for p in (5, 7):
    subs = [m for m in range(1, 2**p)]
    for Am in subs:
        for Bm in [m for m in subs if m & 1]:
            proc += 1
            a, b = elems(Am, p), [x for x in elems(Bm, p) if x]
            S = set(a)
            for x in b:                      # the nonzero elements only
                before = len(S)
                S |= {(y + x) % p for y in S}
                if len(S) == before:
                    zg += 1
                    zg_full += S == set(range(p))    # invariance -> already everything
            allS = {(x + y) % p for x in elems(Am, p) for y in elems(Bm, p)}
            As_t, Bs_t = cd_etransform_trace(a, elems(Bm, p), p)
            holds += (len(allS) >= min(p, len(As_t) + len(Bs_t) - 1) ==
                      min(p, len(a) + len(elems(Bm, p)) - 1))
print(proc, zg, zg == zg_full, holds)

# Polynomial method suite (1.3, A7, A8, A17)
pf_checks = pf_bad = 0
for p in (5, 7, 11, 13):
    for a in range(2, min(p, 5) + 1):
        for A in combinations(range(p), a):
            inv_d = [pow(prod := 1, 1, p) for _ in A]
            for idx, x0 in enumerate(A):
                pr = 1
                for x1 in A:
                    if x1 != x0: pr = (pr * (x0 - x1)) % p
                inv_d[idx] = pow(pr, p - 2, p)
            for i in range(a):
                pf_checks += 1
                val = sum(pow(A[idx], i, p) * inv_d[idx] for idx in range(a)) % p
                pf_bad += val != (1 if i == a - 1 else 0)

_state = 12345
def rnd(n):
    global _state
    _state = (48271 * _state) % 2147483647
    return _state % n

grid_checks = grid_bad = 0
for p, max_ab in [(3, 2), (5, 4), (7, 7)]:
    for a in range(2, max_ab + 1):
        for b in range(2, max_ab + 1):
            A, B = list(range(a)), list(range(b))
            for _ in range(4):
                coeffs = [[rnd(p) for _ in range(b)] for _ in range(a)]
                vals = {(x, y): sum(coeffs[i][j] * pow(x, i, p) * pow(y, j, p)
                                    for i in range(a) for j in range(b)) % p
                        for x in A for y in B}
                grid_checks += 1
                # Reconstruct via 2D Lagrange and verify uniqueness (D1)
                rec_ok = True
                for x0 in range(p):
                    for y0 in range(p):
                        truth = sum(coeffs[i][j] * pow(x0, i, p) * pow(y0, j, p)
                                    for i in range(a) for j in range(b)) % p
                        interp = 0
                        for xa in A:
                            la = 1
                            for xa2 in A:
                                if xa2 != xa:
                                    la = la * (x0 - xa2) * pow(xa - xa2, p - 2, p) % p
                            for yb in B:
                                lb = 1
                                for yb2 in B:
                                    if yb2 != yb:
                                        lb = lb * (y0 - yb2) * pow(yb - yb2, p - 2, p) % p
                                interp = (interp + vals[(xa, yb)] * la * lb) % p
                        if interp != truth: rec_ok = False
                grid_bad += not rec_ok

ws_checks = ws_bad = van_checks = van_bad = 0
for p in (5, 7, 11):
    for t in range(300):
        a, b = 1 + rnd(p - 1), 1 + rnd(p - 1)
        A = sorted(set(range(p)), key=lambda _: rnd(1000))[:a]
        B = sorted(set(range(p)), key=lambda _: rnd(1000))[:b]
        invA = [pow(eval("*".join(str((x - x2) % p) for x2 in A if x2 != x) or "1"),
                    p - 2, p) for x in A]
        invB = [pow(eval("*".join(str((y - y2) % p) for y2 in B if y2 != y) or "1"),
                    p - 2, p) for y in B]
        deg = a + b - 2
        terms = [(i, j, rnd(p)) for i in range(deg + 1) for j in range(deg + 1 - i)]
        wsum = 0
        for ix, x in enumerate(A):
            for iy, y in enumerate(B):
                fxy = sum(c * pow(x, i, p) * pow(y, j, p) for i, j, c in terms) % p
                wsum = (wsum + fxy * invA[ix] * invB[iy]) % p
        top = next((c for i, j, c in terms if i == a - 1 and j == b - 1), 0) % p
        ws_checks += 1; ws_bad += wsum != top
        if t < 150:
            C = sorted(set(range(p)), key=lambda _: rnd(1000))[:rnd(p + 1)]
            Cset = set(C)
            van_checks += 1
            for x in A:
                for y in B:
                    fval = 1
                    for c in C: fval = (fval * (x + y - c)) % p
                    van_bad += (fval == 0) != (((x + y) % p) in Cset)

wall_bad = dis_van = 0
for p in (2, 3, 5, 7, 11, 13, 17, 19):
    for a in range(1, p + 1):
        for b in range(1, p + 1):
            if a + b - 2 >= 0:
                v = comb(a + b - 2, a - 1) % p
                wall_bad += (v == 0) if a + b - 2 <= p - 1 else (v != 0)
A7, B7, p7 = [0, 1, 3], [0, 2], 7
invA7 = [pow(eval("*".join(str((x - x2) % 7) for x2 in A7 if x2 != x)), 5, 7) for x in A7]
invB7 = [pow(eval("*".join(str((y - y2) % 7) for y2 in B7 if y2 != y)), 5, 7) for y in B7]
dis_vals = set()
for C in combinations(range(7), 3):
    s = 0
    all_zero = True
    for ix, x in enumerate(A7):
        for iy, y in enumerate(B7):
            fxy = 1
            for c in C: fxy = (fxy * (x + y - c)) % 7
            if fxy != 0: all_zero = False
            s = (s + fxy * invA7[ix] * invB7[iy]) % 7
    dis_vals.add(s); dis_van += all_zero
print("poly suite:", pf_checks, pf_bad, grid_checks, grid_bad,
      ws_checks, ws_bad, van_checks, van_bad, wall_bad, dis_vals, dis_van)

# Kneser census (weak and strong forms) over Z_6 through Z_9
for n in (6, 7, 8, 9):
    subs = [m for m in range(1, 2**n)]
    pairs = viol = tight = s_viol = 0
    for Am in subs:
        for Bm in subs:
            a, b = elems(Am, n), elems(Bm, n)
            S = {(x + y) % n for x in a for y in b}
            Hset = [g for g in range(n) if all((s + g) % n in S for s in S)]
            H = len(Hset)
            AH = {(x + h) % n for x in a for h in Hset}
            BH = {(y + h) % n for y in b for h in Hset}
            pairs += 1
            viol += len(S) < len(a) + len(b) - H
            s_viol += len(S) < len(AH) + len(BH) - H
            tight += len(S) == len(a) + len(b) - H
    print(f"Z_{n}: pairs {pairs}, violations {viol}/{s_viol}, tight {tight}")

# e-transform stress (2.3)
_state = 12345
checks = viol = 0
for n, dims in [(6, None), (8, None), (9, (3, 3))]:
    def elem(): return [rnd(3), rnd(3)] if dims else rnd(n)
    def add(x, y): return [(x[0]+y[0]) % 3, (x[1]+y[1]) % 3] if dims else (x + y) % n
    def sub(x, y): return [(x[0]-y[0]) % 3, (x[1]-y[1]) % 3] if dims else (x - y) % n
    def key(z): return tuple(z) if dims else (z,)
    for _ in range(300):
        A, asz = [], 1 + rnd(4)
        while len(A) < asz:
            e = elem()
            if not any(key(e) == key(a) for a in A): A.append(e)
        B, bsz = [], 1 + rnd(4)
        while len(B) < bsz:
            e = elem()
            if not any(key(e) == key(b) for b in B): B.append(e)
        AB = {key(add(a, b)) for a in A for b in B}
        for ei in range(n):
            e = [ei // 3, ei % 3] if dims else ei
            Ae = A + [x for x in (add(b, e) for b in B)
                      if not any(key(x) == key(a) for a in A)]
            Be = [b for b in B if any(key(sub(a, e)) == key(b) for a in A)]
            checks += 1
            viol += any(key(add(x, y)) not in AB for x in Ae for y in Be)
            viol += len(Ae) + len(Be) != len(A) + len(B)
print(checks, viol)

# m-fold Cauchy-Davenport random stress (1.4) and F_7 2-subset census (A16)
trials = viol = 0
for p in (5, 7):
    for _ in range(300):
        m = 2 + rnd(3)
        sets = []
        for _ in range(m):
            s, sz = set(), 1 + rnd(3)
            while len(s) < sz: s.add(rnd(p))
            sets.append(s)
        cur = set(sets[0])
        for s in sets[1:]:
            cur = {(x + a) % p for x in cur for a in s}
        trials += 1
        viol += len(cur) < min(p, sum(map(len, sets)) - m + 1)
print(trials, viol)

pairs7 = [tuple(c) for c in combinations(range(7), 2)]
tri_tot = tri_tight = tri_full = quad_tot = quad_tight = 0
tight_list = []
for A1 in pairs7:
    for A2 in pairs7:
        s12 = {(x + y) % 7 for x in A1 for y in A2}
        for A3 in pairs7:
            s123 = {(x + z) % 7 for x in s12 for z in A3}
            tri_tot += 1
            if len(s123) == 4:
                tri_tight += 1; tight_list.append((A1, A2, A3))
            elif len(s123) == 7: tri_full += 1
            for A4 in pairs7:
                s1234 = {(x + w) % 7 for x in s123 for w in A4}
                quad_tot += 1
                if len(s1234) == 5: quad_tight += 1
unseen, orbits = set(tight_list), []
perms = ((0, 1, 2), (0, 2, 1), (1, 0, 2), (1, 2, 0), (2, 0, 1), (2, 1, 0))
while unseen:
    rep = min(unseen)
    orb = {tuple(tuple(sorted((u * x + v) % 7 for x in S)) for S in
                 (rep[i], rep[j], rep[k]))
           for u in range(1, 7) for v in range(7) for i, j, k in perms}
    orbits.append(len(orb)); unseen -= orb
print("A16 F_7:", tri_tot, tri_tight, tri_full, quad_tot, quad_tight, sorted(orbits))
```

**Verified output.** The staircase witnesses print `[2, 3, 5, 7] [2, 3, 4, 5, 7]` and `[3, 6, 10, 13] [3, 6, 9, 10, 13]` — the chains of 4 = 3+2−1 strict sums inside the full sumsets of size 5 (Figure 1's and Exercise 1's data). Cauchy–Davenport over 𝔽₂, 𝔽₃, 𝔽₅, 𝔽₇ (all pairs), 𝔽₁₁ up to size 4, 𝔽₁₃ up to size 3: `473998 0 42081` — **473,998 pairs, zero violations, 42,081 tight**. The merge/periodicity monitor over 𝔽₅ and 𝔽₇ (every A, every B containing 0, skipping the trivial b = 0 step, and verifying §1.2's e-transform induction alongside it) prints `8624 9759 True 8624`: 8,624 processes, **9,759** zero-gain steps, every single one fired only when the running set was already the whole field — invariance forces everything — and the bound held in all 8,624. The polynomial method suite prints `poly suite: 15011 0 184 0 900 0 450 0 0 {3} 0` — **15,011** univariate Lagrange evaluations, **184** grid reconstructions, **900** weighted-sum identity tests, **450** vanishing checks, the p ≤ 19 binomial regime-wall verification, and the 35 subsets C disassembly of A17, all with zero errors. The Kneser census, exhaustive over Z₆ through Z₉ with both weak and strong forms checked, prints `Z_6: pairs 3969, violations 0/0, tight 1004`, `Z_7: pairs 16129, violations 0/0, tight 3382`, `Z_8: pairs 65025, violations 0/0, tight 7269`, `Z_9: pairs 261121, violations 0/0, tight 17524` — **zero violations** anywhere. The e-transform stress (300 random pairs in each of Z₆, Z₈, Z₃², every e in the group) prints `6900 0`: both properties — sumset containment and size preservation — hold in all **6,900** checks. The m-fold corollary over 𝔽₅ and 𝔽₇ prints `600 0` — **600** random families of m ≤ 4 sets, zero violations — and the A16 census over 𝔽₇ prints `A16 F_7: 9261 1029 2058 194481 7203 [21, 126, 126, 126, 126, 126, 126, 252]`.

### Part 2 — EGZ: exhaustive, by pairing, and by blocks

```python
from math import gcd

_state = 12345
def rnd(n):
    global _state
    _state = (48271 * _state) % 2147483647
    return _state % n

def egz_holds_multiset(counts, n):        # counts[v] = multiplicity of v; DP
    if n < 1 or sum(counts) < n: return False
    dp = [[False] * n for _ in range(2 * n)]
    dp[0][0] = True
    for v in range(n):
        for _ in range(counts[v]):
            for j in range(2 * n - 2, -1, -1):
                for s in range(n):
                    if dp[j][s]: dp[j + 1][(s + v) % n] = True
    return dp[n][0]

for n in range(3, 8):                      # n = 7 takes a few minutes
    counts = [0] * n; total = passed = 0
    def rec(i, left):
        global total, passed
        if i == n - 1:
            counts[i] = left
            total += 1
            passed += egz_holds_multiset(counts, n)
            counts[i] = 0
            return
        for c in range(left + 1):
            counts[i] = c; rec(i + 1, left - c)
        counts[i] = 0
    rec(0, 2 * n - 1)
    print(f"n = {n}: multisets {total}, containing a zero-sum n-subset: {passed}")

# Pairing lemma on 800 random constrained multisets (2.5)
trials = fails = 0
for _ in range(800):
    m = 2 + rnd(4)
    pool = 2 + rnd(m + 1)
    mult = []
    while len(mult) < 2 * m:
        v = rnd(pool)
        if mult.count(v) < m: mult.append(v)
    s = sorted(mult)
    trials += 1
    fails += any(s[i] == s[i + m] for i in range(m))
print("pairing:", trials, "failures:", fails)

# Prime-case EGZ engine over F_5 and F_7 (2.5 and A9)
runs = trivial = ok = covered = pair_fails = 0
for p in (5, 7):
    for _ in range(450):
        mult = [rnd(p) for _ in range(2 * p - 1)]
        runs += 1
        if any(mult.count(v) >= p for v in range(p)):
            trivial += 1
            continue
        x = mult[0]
        rest = sorted(mult[1:])
        prs = [(rest[i], rest[i + p - 1]) for i in range(p - 1)]
        if any(a == b for a, b in prs):
            pair_fails += 1
            continue
        cur = set(prs[0])
        for a, b in prs[1:]:
            cur = {(u + v) % p for u in cur for v in (a, b)}
        covered += len(cur) == p
        ok += (p - x) % p in cur
print("prime case:", runs, "trivial:", trivial, "pair_fails:", pair_fails,
      "non-trivial succeeded:", ok, "choice-sumset covered field:", covered)

def zero_sum_subset(a, k):
    n = len(a)
    if k < 0 or n < k: return None
    def rec(start, left, acc, s):
        if left == 0: return acc if s % k == 0 else None
        for i in range(start, n - left + 1):
            r = rec(i + 1, left - 1, acc + [i], s + a[i])
            if r is not None: return r
        return None
    return rec(0, k, [], 0)

# Composite chain: verify divisibility of the unscaled nm-subset sum mod nm (2.5)
trials = fails = 0
for n, m in [(2, 3), (3, 2), (2, 2), (2, 5), (3, 3)]:
    for _ in range(60):
        arr = [rnd(50) for _ in range(2 * n * m - 1)]
        pool, blocks, block_sums = arr[:], [], []
        for _ in range(2 * m - 1):
            idx = zero_sum_subset([v % n for v in pool], n)
            if idx is None:                     # EGZ(n) says this never happens
                fails += 1
                break
            blk = [pool[i] for i in idx]
            blocks.append(blk)
            block_sums.append(sum(blk) // n)
            pool = [v for j, v in enumerate(pool) if j not in idx]
        else:
            sel = zero_sum_subset([v % m for v in block_sums], m)
            trials += 1
            chosen = [x for i in (sel or []) for x in blocks[i]]
            fails += (sel is None or len(chosen) != n * m
                      or sum(chosen) % (n * m) != 0)
print("composite chain:", trials, "failures:", fails)

# A19: Near-miss census of 2n - 2 multisets over Z_n for n = 3..9
tot_all = exotic_all = 0
av_counts = []
for n in range(3, 10):
    counts = [0] * n; tot = av = exotic = 0
    def rec_av(i, left):
        global tot, av, exotic
        if i == n - 1:
            counts[i] = left; tot += 1
            if not egz_holds_multiset(counts, n):
                av += 1
                vals = [v for v in range(n) if counts[v] > 0]
                if not (len(vals) == 2 and counts[vals[0]] == n - 1
                        and counts[vals[1]] == n - 1
                        and gcd(vals[0] - vals[1], n) == 1):
                    exotic += 1
            counts[i] = 0; return
        for c in range(left + 1):
            counts[i] = c; rec_av(i + 1, left - c)
        counts[i] = 0
    rec_av(0, 2 * n - 2)
    tot_all += tot; exotic_all += exotic; av_counts.append(av)
print("A19 (2n-2) census:", tot_all, "avoiders:", av_counts, "exotic:", exotic_all)
```

**Verified output.** The exhaustive sweep prints `n = 3: multisets 21, containing a zero-sum n-subset: 21`, then `120 / 120`, `715 / 715`, `4368 / 4368`, and finally `n = 7: multisets 27132, containing a zero-sum n-subset: 27132` — **every** multiset of 2n−1 residues contains n summing to 0, for every n ≤ 7. The pairing lemma on 800 random constrained multisets prints `pairing: 800 failures: 0` — the opposite pairing never pairs an element with its equal. The prime-case engine over 𝔽₅ and 𝔽₇ prints `prime case: 900 trivial: 44 pair_fails: 0 non-trivial succeeded: 856 choice-sumset covered field: 856`: 44 runs settled by the trivial ≥ p-copies case, and in **all 856** remaining runs the four-step machine worked end to end — pairs distinct, choice-sumset equal to the whole field (the m-fold Cauchy–Davenport bound, achieved), and −x reachable. The composite chain over (n, m) = (2,3), (3,2), (2,2), (2,5), (3,3) prints `composite chain: 300 failures: 0`: every instance extracted its 2m−1 disjoint zero-mod-n blocks, EGZ(m) selected on the scaled sums, and the union certified a genuine zero-mod-nm subset. Finally, the A19 near-miss census over 3 ≤ n ≤ 9 prints `A19 (2n-2) census: 873912 avoiders: [3, 4, 10, 6, 21, 16, 27] exotic: 0`.

### Part 3 — Shadows and the frontiers: Kruskal–Katona, the Daykin mirror, Hilton–Milner, union-closed

```python
from math import comb, sqrt
from fractions import Fraction
from itertools import combinations

def bits(m): return bin(m).count("1")

# (a) the cascade formula vs the colex initial segments
def cascade(N, k):
    if N <= 0 or k <= 0: return 0
    total, a_prev = 0, None
    while N > 0 and k >= 1:
        a = k
        while comb(a + 1, k) <= N: a += 1
        if a_prev is not None and a >= a_prev: a = a_prev - 1
        total += comb(a, k - 1)
        N -= comb(a, k)
        a_prev, k = a, k - 1
    return total

agree = total = 0
for k in (2, 3, 4):
    sets = sorted(combinations(range(12), k), key=lambda S: tuple(reversed(S)))
    for N in range(1, len(sets) + 1):
        total += 1
        sh = {S[:i] + S[i+1:] for S in sets[:N] for i in range(k)}
        if len(sh) == cascade(N, k): agree += 1
print("cascade == colex shadows:", agree, "/", total, "; cascade(10, 3) =", cascade(10, 3))

# (b, c, d) Lovasz form, j-form, clique form — exhaustive on [6]
def comb_real(x, k):
    if k < 0: return 0.0
    r = 1.0
    for i in range(k): r = r * (x - i) / (i + 1)
    return r

def real_param(m, k):
    if k <= 0 or m <= 0: return 0.0
    lo, hi = float(k - 1), 40.0
    while comb_real(hi, k) < m: hi *= 2
    for _ in range(60):
        mid = (lo + hi) / 2
        if comb_real(mid, k) < m: lo = mid
        else: hi = mid
    return (lo + hi) / 2

def census(n, k):
    if k < 1 or n < k: return (0,) * 8
    sets = [m for m in range(1 << n) if bits(m) == k]
    t = len(sets)
    subs = []                      # (k-1)-subset masks of each member
    for m in sets:
        subs.append({m & ~(1 << e) for e in range(n) if m >> e & 1})
    hisets = [m for m in range(1 << n) if bits(m) == k + 1]
    quads = []                     # each (k+1)-set as the list of its k-subsets
    for m in hisets:
        quads.append([m & ~(1 << e) for e in range(n) if m >> e & 1])
    badL = eqL = eqLc = badJ = eqJ = badC = eqC = eqCc = 0
    for mask in range(1, 1 << t):
        idx = [i for i in range(t) if mask >> i & 1]
        m = len(idx)
        x = real_param(m, k)
        union = 0
        sh = set()
        for i in idx:
            union |= sets[i]
            sh |= subs[i]
        if len(sh) < comb_real(x, k - 1) - 1e-9: badL += 1
        complete = (m == comb(bits(union), k))
        if abs(len(sh) - comb_real(x, k - 1)) < 1e-9:
            eqL += 1
            if complete: eqLc += 1
        if bits(union) < x - 1e-9: badJ += 1       # j = 1 shadow = the union
        if abs(bits(union) - x) < 1e-9: eqJ += 1
        famset = {sets[i] for i in idx}
        K = 0
        for q in quads:
            if all(g in famset for g in q): K += 1
        if K > comb_real(x, k + 1) + 1e-9: badC += 1
        if abs(K - comb_real(x, k + 1)) < 1e-9:
            eqC += 1
            if complete: eqCc += 1
    return badL, eqL, eqLc, badJ, eqJ, badC, eqC, eqCc

for k in (2, 3):
    bL, eL, eLc, bJ, eJ, bC, eC, eCc = census(6, k)
    print(f"census (6,{k}): Lovasz bad {bL}, eq {eL} (complete {eLc}); "
          f"j=1 bad {bJ}, eq {eJ}; clique bad {bC}, eq {eC} (complete {eCc})")

# (e) the Daykin mirror, exhaustive at (6,2) and (6,3), plus A18 slack check
def mirror62():
    edges = [m for m in range(1 << 6) if bits(m) == 2]
    t = len(edges)
    dj = [sum(1 << j for j in range(t) if not (edges[i] & edges[j])) for i in range(t)]
    count = viol = maxsz = maxcnt = eq = 0
    star_slacks, tri_slacks = [], []
    for mask in range(1 << t):
        if any(mask & dj[i] for i in range(t) if mask >> i & 1): continue
        count += 1
        sz = bits(mask)
        sh = 0
        for i in range(t):
            if mask >> i & 1: sh |= dj[i]
        if sz + bits(sh) > comb(6, 2): viol += 1
        if sz > maxsz: maxsz, maxcnt = sz, 1
        elif sz == maxsz: maxcnt += 1
        if sz + bits(sh) == comb(6, 2):
            eq += 1
            x = real_param(sz, 4)
            slack = round(bits(sh) - comb_real(x, 2), 2)
            if sz == 5: star_slacks.append(slack)
            elif sz == 3: tri_slacks.append(slack)
    print("mirror (6,2): families", count, "violations", viol,
          "max", maxsz, "(by", str(maxcnt) + ")", "mirror-eq", eq,
          "star/tri slacks:", len(star_slacks), set(star_slacks),
          len(tri_slacks), set(tri_slacks))

def mirror63():
    tr = [m for m in range(1 << 6) if bits(m) == 3]
    pairs, seen = [], set()
    for t in tr:
        if t not in seen:
            pairs.append((t, 63 ^ t)); seen.add(t); seen.add(63 ^ t)
    count = viol = maxsz = maxcnt = eq = 0
    for d in range(3 ** 10):
        fam, dd = [], d
        for p in range(10):
            r = dd % 3; dd //= 3
            if r: fam.append(pairs[p][r - 1])
        count += 1
        if 2 * len(fam) > comb(6, 3): viol += 1   # n = 2k: shadow of F* is F*
        if len(fam) > maxsz: maxsz, maxcnt = len(fam), 1
        elif len(fam) == maxsz: maxcnt += 1
        if 2 * len(fam) == comb(6, 3): eq += 1
    print("mirror (6,3): families", count, "violations", viol,
          "max", maxsz, "(by", str(maxcnt) + ")", "mirror-eq", eq)

mirror62(); mirror63()

# (f) Hilton-Milner census at (7, 3), Bron-Kerbosch, plus AK & HM comparisons
def hm73():
    tr = [m for m in range(1 << 7) if bits(m) == 3]
    t = len(tr)
    adj = [[j for j in range(t) if j != i and tr[i] & tr[j]] for i in range(t)]
    maximal = []
    def bk(R, P, X):
        if not P and not X:
            maximal.append(list(R)); return
        pivot = max(P + X, key=lambda u: sum(1 for v in adj[u] if v in P))
        for v in list(P):
            if v in adj[pivot]: continue
            bk(R + [v], [w for w in P if w in adj[v]], [w for w in X if w in adj[v]])
            P.remove(v); X.append(v)
    bk([], list(range(t)), [])
    maxsz = max(len(c) for c in maximal)
    stars = sum(1 for c in maximal if len(c) == maxsz)
    def core(c):
        r = 127
        for i in c: r &= tr[i]
        return r
    empty = [c for c in maximal if core(c) == 0]
    cmax = max(len(c) for c in empty)
    cwin = [c for c in empty if len(c) == cmax]
    hm = f1 = 0
    for c in cwin:
        fam = {tr[i] for i in c}
        if any(fam == ({Y} | {F for F in tr if F >> x & 1 and F & Y})
               for x in range(7) for Y in tr if not Y >> x & 1): hm += 1
        elif any(fam == {F for F in tr if bits(F & W) >= 2} for W in tr): f1 += 1
    print("HM (7,3): maximal", len(maximal), "; max", maxsz, "(by", str(stars) +
          " stars); empty-core max", cmax, "(by", str(len(cwin)) + ":",
          str(hm) + " HM +", str(f1) + " F1)")
    for n_ak in (7, 5):
        ks = [m for m in range(1 << n_ak) if bits(m) == 3]
        sizes = [sum(1 for F in ks if bits(F & ((1 << (2 * r + 1)) - 1)) >= r + 1)
                 for r in range(4)]
        print(f"AK sizes ({n_ak},3):", sizes)
    for n_c, k_c in [(10, 4), (9, 4), (12, 5)]:
        hm_sz = comb(n_c - 1, k_c - 1) - comb(n_c - k_c - 1, k_c - 1) + 1
        f1_sz = 3 * comb(n_c - 3, k_c - 2) + comb(n_c - 3, k_c - 3)
        print(f"({n_c},{k_c}): F1 = {f1_sz}, HM = {hm_sz}")

hm73()

# (h) union-closed, exhaustive
def union_closed(n):
    if n < 1: return 0, 0, 0, 0, 0
    join = [[a | b for b in range(1 << n)] for a in range(1 << n)]
    closed = nonempty = fails = withsing = singbad = 0
    for mask in range(1, 1 << (1 << n)):
        fam = [i for i in range(1 << n) if mask >> i & 1]
        if any(not (mask >> join[i][j] & 1) for i in fam for j in fam): continue
        closed += 1
        if any(fam):
            nonempty += 1
            if not any(2 * sum(1 for f in fam if f >> x & 1) >= len(fam)
                       for x in range(n)): fails += 1
        singles = [f for f in fam if bits(f) == 1]
        if singles:
            withsing += 1
            for s in singles:
                if 2 * sum(1 for f in fam if f & s) < len(fam): singbad += 1
    return closed, nonempty, fails, withsing, singbad

for n in (3, 4):
    cl, ne, f, ws, sb = union_closed(n)
    print(f"union-closed [{n}]: {cl} families ({ne} with a nonempty member), "
          f"conjecture failures {f}; singleton lemma on {ws} families, bad {sb}")
print("Gilmer constant:", (3 - sqrt(5)) / 2)
```

**Verified output.** The cascade agrees with the colex initial segments on **781/781** sizes (k = 2, 3, 4; every N ≤ C(12, k)), and cascade(10, 3) = 10 = C(5, 2). The censuses: at (6, 2) all 32,767 nonempty families pass the Lovász form with **57** equalities — every one a complete family —, the j = 1 form with the same 57, and the clique form with the same 57; at (6, 3) all 1,048,575 families pass all three checks with **42** equalities each, again exactly the complete families (x an integer), as §4.2's equality analysis demands. The Daykin mirror: **192** intersecting families at (6, 2), zero violations of |𝓕| + |∂_k𝓕*| ≤ C(6, k), maximum 5 achieved by exactly the 6 stars, mirror-equality at 26 (the 6 stars with j-form slack 0.0 plus the 20 sub-maximum triangles with j-form slack 3.6 — tight mirror, loose x); at (6, 3), **59,049** families, zero violations, maximum 10 by exactly 1,024, mirror-equality at all 1,024. Hilton–Milner at (7, 3): Bron–Kerbosch finds **6,127** maximal intersecting families; the maximum 15 belongs to exactly the 7 stars; the empty-core maximum is **13** — the HM formula C(6, 2) − C(3, 2) + 1 — achieved by exactly **175** families, **140** of the HM type and **35** of the F₁ type and none other; the AK sizes read [15, 13, 10, 0] at (7, 3) and [6, 7, 10, 0] at (5, 3), and the (10, 4), (9, 4), (12, 5) comparisons print F1 = 70, HM = 75, F1 = 51, HM = 53, F1 = 288, HM = 316. Union-closed: on [3], **121** nonempty families (120 with a nonempty member; {∅} alone is vacuous), zero conjecture failures; on [4], **4,959** (4,958), zero failures; the singleton lemma holds on all 98 singleton-containing families of [3] and all 4,126 of [4], zero bad; Gilmer's constant prints 0.3819660112501051.

### Part 4 — The assembly: the two-case recursion and DeVos's portions

```python
from itertools import combinations

def elems(mask, n): return [i for i in range(n) if mask >> i & 1]
def sumset(A, B, n): return {(a + b) % n for a in A for b in B}
def stab(S, n):
    s = set(S)
    if not s: return list(range(n))
    return [g for g in range(n) if all((x + g) % n in s for x in s)]
def closure(diffs, n):
    H, todo = {0}, list(diffs)
    while todo:
        d = todo.pop()
        for g in list(H):
            for h in ((g + d) % n, (g - d) % n):
                if h not in H: H.add(h); todo.append(h)
    return sorted(H)
def witness(A, B, n):
    for a in sorted(A):
        for bp in sorted(B):
            for b in sorted(B):
                if (a + b - bp) % n not in set(A):
                    return a, bp, b
    return None
def recurse(A, B, n):
    """Two-case recursion, canonical rule; every step verified."""
    As, Bs, steps = set(A), set(B), 0
    if not As or not Bs: return "empty", 0
    AB = sumset(As, Bs, n)
    while len(Bs) > 1:
        w = witness(sorted(As), sorted(Bs), n)
        if w is None:                                   # Case 1
            H = closure({(b - bp) % n for b in Bs for bp in Bs}, n)
            assert all((a + h) % n in As for a in As for h in H)
            b0 = min(Bs)
            assert Bs <= {(b0 + h) % n for h in H}      # |B| <= |H'|
            assert sumset(As, Bs, n) == {(a + b0) % n for a in As}
            return "case1", steps
        a, bp, b = w                                     # Case 2
        e = (a - bp) % n
        Anew = As | {(x + e) % n for x in Bs}
        Bnew = Bs & {(x - e) % n for x in As}
        assert sumset(Anew, Bnew, n) <= AB              # containment
        assert len(Anew) + len(Bnew) == len(As) + len(Bs)  # size preservation
        assert 0 < len(Bnew) < len(Bs) and bp in Bnew    # strict decrease
        As, Bs, steps = Anew, Bnew, steps + 1
    return "base", steps

# Exercise 4 (A4): three hand pairs in Z_6
for A4, B4 in [([0, 2, 4], [0, 2, 4]), ([0, 1, 3], [0, 2]), ([0, 1, 3], [0, 2, 3])]:
    print("A4:", A4, B4, "->", recurse(A4, B4, 6))

for n in (4, 6, 7):                                      # Z_7 takes a minute
    pairs = case1 = bases = steps = 0
    for Am in range(1, 1 << n):
        for Bm in range(1, 1 << n):
            kind, st = recurse(elems(Am, n), elems(Bm, n), n)
            pairs += 1; steps += st
            if kind == "case1": case1 += 1
            else: bases += 1
    print(f"Z_{n}: pairs {pairs}, case1 {case1}, bases {bases}, steps {steps}")

# the aperiodicity counterexample of 3.2
A, B, n = [0, 1, 3], [0, 2], 6
AB = sumset(A, B, n)
print("stab(A+B):", stab(AB, n))
for a in A:
    for bp in B:
        e = (a - bp) % n
        Ap = sorted(set(A) | {(x + e) % n for x in B})
        Bp = sorted(set(B) & {(x - e) % n for x in A})
        if (sumset(Ap, Bp, n) <= AB and len(Ap) + len(Bp) == len(A) + len(B)
                and len(Bp) < len(B)):
            print(f"transform a={a} b'={bp} e={e}: {Ap} + {Bp}, stab",
                  stab(sumset(Ap, Bp, n), n))

# DeVos's portions on the canonical instance of 3.3 (guarded for nonempty Z)
X, Y, n = [0, 1], [0, 3, 4], 6
XYt = sumset(X, Y, n)
def is_portion(Z):
    if not Z: return False, []
    H = stab(Z, n)
    inter = set(X) & set(Y)
    uniH = sumset(sorted(set(X) | set(Y)), H, n)
    return len(Z) + len(H) >= len(inter) + len(uniH), H
for r in range(1, len(XYt) + 1):
    for Zc in combinations(sorted(XYt), r):
        ok, H = is_portion(set(Zc))
        if ok: print("portion:", sorted(Zc), "stab", H)

# DeVos aperiodic pair census across Z_6, Z_7, Z_8, and Z_4 x Z_2 (3.3)
for label, order, add_fn, sub_fn in [
    ("Z_6", 6, lambda a, b: (a + b) % 6, lambda a, b: (a - b) % 6),
    ("Z_7", 7, lambda a, b: (a + b) % 7, lambda a, b: (a - b) % 7),
    ("Z_8", 8, lambda a, b: (a + b) % 8, lambda a, b: (a - b) % 8),
    ("Z_4xZ_2", 8, lambda a, b: ((a & 3) + (b & 3)) % 4 | ((a ^ b) & 4),
                   lambda a, b: ((a & 3) - (b & 3)) % 4 | ((a ^ b) & 4)),
]:
    ap_pairs = z0_nontriv = viol_ap = 0
    for Xm in range(1, 1 << order):
        Xs = [i for i in range(order) if Xm >> i & 1]
        if len(Xs) < 2: continue
        x0, x1 = Xs[0], Xs[1]
        dx = sub_fn(x1, x0)
        for Ym in range(1, 1 << order):
            Ys = [i for i in range(order) if Ym >> i & 1]
            S = {add_fn(x, y) for x in Xs for y in Ys}
            if any(all(add_fn(s, g) in S for s in S) for g in range(1, order)):
                continue
            ap_pairs += 1
            y0 = next(y for y in Ys if add_fn(y, dx) not in set(Ys))
            shift = sub_fn(x0, y0)
            Yt = {add_fn(y, shift) for y in Ys}
            inter, uni = set(Xs) & Yt, set(Xs) | Yt
            Z0 = {add_fn(u, v) for u in inter for v in uni}
            H0 = [g for g in range(order) if all(add_fn(z, g) in Z0 for z in Z0)]
            uniH0 = {add_fn(u, h) for u in uni for h in H0}
            if not (0 < len(inter) < len(Xs)) or len(Z0) + len(H0) < len(inter) + len(uniH0):
                viol_ap += 1
            if len(H0) > 1: z0_nontriv += 1
    print(f"DeVos {label}: aperiodic |X|>=2 pairs {ap_pairs}, Z0 nontrivial {z0_nontriv}, viol {viol_ap}")
```

**Verified output.** The Exercise 4 hand traces print `A4: [0, 2, 4] [0, 2, 4] -> ('case1', 0)`, `A4: [0, 1, 3] [0, 2] -> ('base', 1)`, and `A4: [0, 1, 3] [0, 2, 3] -> ('base', 2)`. The recursion sweep prints `Z_4: pairs 225, case1 41, bases 184, steps 167`, `Z_6: pairs 3969, case1 872, bases 3097, steps 4939`, `Z_7: pairs 16129, case1 3473, bases 12656, steps 24333` — the matching rows of §3.1's table (the full twelve-group sweep, 738,884 pairs with zero violations, is the TypeScript run recorded in the appendix; the census counts are the canonical lexicographic rule's). The counterexample prints `stab(A+B): [0]` and four transform lines — the period-creating (a, b′) = (0, 2) with e = 4 producing A′ = [0, 1, 3, 4], B′ = [2] with stab [0, 3], and the three other genuine transforms — the canonical (0, 0) among them — keeping the trivial stabilizer [0] — the §3.2 warning, machine-witnessed. The portion enumeration prints exactly six lines: `[0, 1, 3, 4] stab [0, 3]`, the four trivial-stabilizer 4-subsets `[0, 1, 3, 5]`, `[0, 1, 4, 5]`, `[0, 3, 4, 5]`, `[1, 3, 4, 5]`, and the full sumset `[0, 1, 3, 4, 5] stab [0]` — Exercise 10's list, reproduced. Finally, the DeVos aperiodic sweep prints `DeVos Z_6: aperiodic |X|>=2 pairs 1080, Z0 nontrivial 60, viol 0`, `DeVos Z_7: aperiodic |X|>=2 pairs 5537, Z0 nontrivial 0, viol 0`, `DeVos Z_8: aperiodic |X|>=2 pairs 18432, Z0 nontrivial 930, viol 0`, and `DeVos Z_4xZ_2: aperiodic |X|>=2 pairs 14400, Z0 nontrivial 2614, viol 0`.

### Part 5 — The shade route: deep censuses and the mirror arithmetic

```python
from math import comb
from itertools import combinations

def deep_census(n, k):
    """Deep equality via the integer shortcut: |G| = C(u,k) with u the union
    size, and every j-shadow exactly C(u, j).  Deep ⟺ complete, by 5.2."""
    if k < 1 or n < k: return
    sets = [m for m in range(1 << n) if bin(m).count("1") == k]
    t = len(sets)
    deep = complete = 0
    by_u = {}
    for mask in range(1, 1 << t):
        fam = [sets[i] for i in range(t) if mask >> i & 1]
        union = 0
        for f in fam: union |= f
        u = bin(union).count("1")
        if len(fam) != comb(u, k): continue            # parameter must be u
        cur, ok = fam, True
        for j in range(k - 1, 0, -1):
            sh = set()
            for f in cur:
                for e in range(n):
                    if f >> e & 1: sh.add(f & ~(1 << e))
            if len(sh) != comb(u, j): ok = False; break
            cur = sorted(sh)
        if ok:
            deep += 1
            complete += len(fam) == comb(u, k)        # automatic: deep => complete
            by_u[u] = by_u.get(u, 0) + 1
    print(f"({n},{k}): families {(1 << t) - 1}, deep {deep}, complete {complete}, by_u {by_u}")

deep_census(6, 3); deep_census(6, 4); deep_census(7, 5)   # (7,5) takes minutes

# the (3,2,5) hunt: ten edges, ten triangles, on [7], plus A20 distribution & ceilings
edges = list(combinations(range(7), 2))
tris = [(edges.index((a, b)), edges.index((a, c)), edges.index((b, c)))
        for a, b, c in combinations(range(7), 3)]
v_edges = [[i for i, e in enumerate(edges) if v in e] for v in range(7)]
v_tris = [[t for t in tris if any(ti in v_edges[v] for ti in t)] for v in range(7)]
total = hits = ceil_viol = 0
tri_hist = [0] * 11
for combo in combinations(range(21), 10):
    s = set(combo)
    tri = sum(1 for t in tris if t[0] in s and t[1] in s and t[2] in s)
    total += 1
    tri_hist[tri] += 1
    for v in range(7):
        dv = sum(1 for e in v_edges[v] if e in s)
        kv = sum(1 for t in v_tris[v] if t[0] in s and t[1] in s and t[2] in s)
        if kv > 10 - dv or 2 * kv > 3 * dv: ceil_viol += 1
    if tri >= 10:
        deg = sorted(sum(1 for e in combo if v in edges[e]) for v in range(7))
        assert deg == [0, 0, 4, 4, 4, 4, 4]             # K5 + two isolated
        hits += 1
print("10-edge graphs on [7]:", total, "with >= 10 triangles:", hits,
      "ceil_viol:", ceil_viol, "hist[7..10]:", tri_hist[7:])

# the star mirror partitions and the cap-meets-floor arithmetic
for n, k in [(9, 4), (5, 2), (7, 3), (8, 3)]:
    star, shade = comb(n - 1, k - 1), comb(n - 1, k)
    print(f"({n},{k}): |F*| = {star} + |d_k F*| = {shade} = {star + shade}"
          f" = C({n},{k}) = {comb(n, k)}")
print("h(t) = C(t,5)+C(t,4):", [comb(t, 5) + comb(t, 4) for t in (5, 6, 7, 8)],
      "h(8) = C(9,4) =", comb(9, 4))
```

**Verified output.** The deep censuses print `(6,3): families 1048575, deep 42, complete 42, by_u {3: 20, 4: 15, 5: 6, 6: 1}`, `(6,4): families 32767, deep 22, complete 22, by_u {4: 15, 5: 6, 6: 1}`, `(7,5): families 2097151, deep 29, complete 29, by_u {5: 21, 6: 7, 7: 1}` — deep equality and completeness coincide at every size, zero exceptions, as the §5.2 lemma demands (the 29 at (7, 5) split 21 K⁵₅ + 7 K⁵₆ + 1 K⁵₇ by union set; the (7, 5) sweep takes a few minutes). The hunt prints `10-edge graphs on [7]: 352716 with >= 10 triangles: 21 ceil_viol: 0 hist[7..10]: [2310, 0, 0, 21]`, every hit asserting the K₅-plus-two-isolated degree pattern — the 21 placements of the complete family K²₅ — with zero per-vertex ceiling violations and the gap at 8 and 9 triangles verified. The mirror arithmetic prints `(9,4): |F*| = 56 + |d_k F*| = 70 = 126 = C(9,4) = 126`, likewise (5, 2) 4 + 6 = 10, (7, 3) 15 + 20 = 35, (8, 3) 21 + 35 = 56 — every partition a disjoint cover — and the h-values `[6, 21, 56, 126]` with `h(8) = C(9,4) = 126`: strictly increasing, capped exactly at Pascal's point, so cap meets floor and x = n − 1 exactly.

---

## Revision History & Verification Notes

**Editions.** Born inside Chapter 7: the staircase/Cauchy–Davenport, Kneser/EGZ, and shadows lectures date from that chapter's Feynman lecture edition, with their exercises, answers, and lab parts (one exception at the export: the skew battery, Part 6(g) there, stayed in Chapter 7, where it anchors its §2.3's warning and its Exercise 10/A10). The **session-38 restructure** moved the three lectures verbatim into this file with the old numbering deliberately inherited (sections 6.x–8.x; exercises 2, 10, 11, 12, 13, 14, ◆18, ◆20, ◐23; answers A2, A10–A14, A◆18, A◆20; lab Parts 4–6; Figure 2). This edition — the restructure's planned polish, executed as task B3d — completes the authoring: the chapter gets its own introduction, notation, pattern table, Trick Bag, and formula box; the inherited lectures become 1, 2, and 4, and two NEW lectures join — Lecture 3 (the aperiodic assembly: the weak form by the two-case e-transform recursion, the strong form by DeVos's intersection–union induction — flag (iii) closed) and Lecture 5 (the thin range completed by the shade route, through the deep cascade-uniqueness lemma — flag (ii) closed; with flag (i) closed by Daykin's mirror in Lecture 4, all three of Chapter 7's open flags retire here). Exercises renumber 1–11 graded plus ◆12–13 and ◐14–15, answers A1–A11 and A◆12–A◆13, the lab becomes Parts 1–5, the figure 1. Outside the renumbering and re-aiming tokens, the inherited lecture bodies, exercises, answers, and lab parts are byte-identical to the export; the new material was authored against this edition's machine runs. The session-67 adversarial review then audited the chapter end to end — one lecture-wording repair (§3.2's canonical-witness attribution, with Part 4's verified-output sentence matched to it), four record-level alignments (§1.2's merge processes 7,279 → the lab's 8,624 over 𝔽₅/𝔽₇; §2.3's 28,000 → 6,900; §2.2's and §2.5's gate runs re-attributed to the verification record; §2.5's trivial-case count 225 → the lab's 44), one monitor-output repair (Part 1's and A2's zero-gain count 16,988 → the true 9,759), and one lab-code repair (Part 3(h)'s union-closed mask range) — the mathematics otherwise clean.

**Verification basis.** The inherited numbers (the Kneser census, the e-transform stress, the EGZ sweeps, the shadow/mirror/Hilton–Milner/union-closed censuses) were executed and recorded during Chapter 7's life; the lab Parts 1–3 are the reader's runnable copies of exactly that logic, renumbered only. The new numbers were machine-verified at authoring, all clean: (1) the two-case recursion on all 738,884 pairs of the twelve groups of order ≤ 9 — 185,060 Case-1 terminations, 553,824 staircase bases, 1,355,220 Case-2 steps, maximum depth 5, every step and termination checked as §3.1 lists, zero violations; (2) the aperiodicity counterexample of §3.2, all four genuine transforms enumerated; (3) the DeVos machinery on the 39,449 aperiodic pairs of Z₆, Z₇, Z₈, and Z₄×Z₂ — translate, Z₀-portion, and aperiodic-staircase checks all clean, stab(Z₀) nontrivial on 3,604 pairs (60 / 0 / 930 / 2,614), a trivial-stabilizer portion on every pair; (4) the deep censuses — (6, 3) 1,048,575 families → 42 deep, all complete; (6, 4) 32,767 → 22; (7, 5) 2,097,151 → 29 (21 K⁵₅ + 7 K⁵₆ + 1 K⁵₇); and the (3, 2, 5) hunt: exactly 21 of the 352,716 ten-edge graphs on [7] carry at least ten triangles, all K₅ plus two isolated vertices; (5) the mirror arithmetic and the star mirror partitions of §5.3; (6) the (9, 4) depth-first hunt of ◐15's record (best empty-core partial 53, the Hilton–Milner bound). The lab Parts 4–5 are runnable copies of runs (1)–(5). The transform itself was verified the standard way: an exact-token replacement pipeline, every anchor asserted unique before the swap; a residual scan for stale-reference shapes (all zero); and a hygiene gate — five lecture headers, twenty-four subsection headers, twelve balanced fence lines, zero mojibake, zero session references in lecture bodies, one trailing newline — before the master and its canvas were written from the same string and read back equal.

**Standing decisions.** Lecture bodies carry no session references; history lives here. The chapter proves what it uses and cites what it does not: the cascade costume of Kruskal–Katona is cited while the clique form (statement Lovász, proof Keevash) is proved; Katona's classical route to the EKR uniqueness theorem is cited while the shade route is proved, and the middle-J transport of Chapter 7's Lecture 4 is bypassed, not rebuilt; Hilton–Milner, Ahlswede–Khachatrian, and Gilmer's constant stand as gateways; DeVos's proof is presented in full and cited to its author, with Nathanson's GTM 165 and the survey arXiv:2407.12253 carrying the transform's history; the two-case recursion is presented with this book's canonical lexicographic witness rule — the theorem is indifferent to the rule, the census is not, and the §3.1 counts are the rule's; the (9, 4) uniqueness census is honestly recorded as beyond the book's brute budget, the hunt inheriting to ◐15. The web edition embeds this chapter byte-identically (the standard delivery format); the PDF export check is the user-owned release gate; learner testing now follows the completion of the whole project scope, at the user's direction.

**Figures.** One figure, embedded as a fenced SVG at its lecture location per the dual-presentation convention (prose and lab code stay terminal-portable), renumbered 1 in this edition: Figure 1 (L1) — the sumset staircase: climb the first column, then walk the last row; every step is a new sum. The figure data were machine-verified before drawing and moved verified; the caption carries this chapter's numbering.

**Backfill (session 41).** Five graded exercises (16–20) with pattern-mapped hints were added, per the atlas-wide backfill mandate, with worked answers A16–A20 continuing the exercise numbering (14–15 are explorations and carry no answers): the m-fold corollary proved and calibrated (zero violations over all 9,261 ordered triples and all 194,481 ordered quadruples of 2-subsets of 𝔽₇, plus 250,047 mixed-size triples; 1,029 tight triples sorting into 8 affine types — the AP triple the rarest, 21 of 1,029; 7,203 tight quadruples); the polynomial engine's regime boundary (the count C(a+b−2, a−1) is never ≡ 0 mod p below a+b = p+1 and always ≡ 0 beyond, all primes p ≤ 19 — the boundary is a wall, not a slope; the whole-field costume z^p − z verified coefficient-by-coefficient for p ≤ 19; the disassembly on {0,1,3} + {0,2} — all 35 choices of C return C(3, 2) = 3 mod 7, vanishing on no full grid; Cauchy–Davenport exhaustive on 𝔽₅ (961 pairs, 811 tight) and 𝔽₇ (16,129 pairs, 9,857 tight) and 200,000 sampled pairs of 𝔽₁₁, zero violations); the tight-mirror nuance (all 192 intersecting 2-families of [6]: zero mirror violations, exactly 26 mirror-tight — the 6 stars, which are the maximum families, and the 20 triangles; j-form slack 0 on every star against ≈ 3.60 on every triangle, x ≈ 4.63 priced by C(x, 4) = 3); the EGZ cap's near-miss census (all 873,912 multisets of size 2n−2 over Z_n, n = 3..9: the avoiders are exactly the two-value multisets {a^(n−1), b^(n−1)} with gcd(a−b, n) = 1 — counts 3, 4, 10, 6, 21, 16, 27 = n·φ(n)/2 at every n, zero exotic exceptions, the classification honestly scoped to the census); and the clique form in graph costume (all 32,767 nonempty graphs on [6]: t ≤ C(x, 3) with equality exactly the 57 complete families — the §4.1 shadow census's 57 re-read through the clique form; all 352,716 ten-edge graphs on [7]: maximum t = 10 attained exactly 21 times, every attainer K₅ + 2 isolated, the distribution jumping from 2,310 graphs at 7 straight to the 21 at 10 with nothing at 8 or 9; the per-vertex ceilings K(v) ≤ 10 − d(v) and K(v) ≤ (3/2)d(v) clean at every vertex of every graph). Every answer was machine-verified before installation.

**Adversarial review (session 67).** The review arc's two arguing experts (skeptic and engineer) took this chapter chunk by chunk — correctness, coherence, exposition, figure aid — extend-never-rewrite, every retained objection machine-verified before any edit. Verdict: the mathematics is otherwise CLEAN, with one lecture-wording defect, four record-level attribution defects, one monitor-output defect, and one lab-code defect caught, confirmed, and repaired in place. **The defects (machine-sealed):** (1) §3.2's counterexample paragraph said the canonical rule picks the period-creating transform — false: the canonical rule (the lexicographically first (a, b′) admitting some b) picks (a, b′) = (0, 0) with b = 2, e = 0, giving A′ = {0, 1, 2, 3} and B′ = {0} and keeping the trivial stabilizer, while the period-creating (0, 2) with e = 4 is legal but second in the witness order (the four genuine transforms, lex order: (0, 0), (0, 2), (1, 2), (3, 0)); the sentence now says so, and Part 4's verified-output paragraph names the period-creating line as period-creating, the canonical (0, 0) among the trivial-stabilizer three. (2) §1.2 credited the merge monitor with 7,279 processes on sampled pairs in 𝔽₁₁ — the printed lab runs 𝔽₅ and 𝔽₇ only, 8,624 processes; aligned. (3) §2.3 credited the e-transform stress with 28,000 checks over Z₆, Z₈, Z₃² and Z₄² — the printed lab runs Z₆, Z₈, Z₃², 300 random pairs each, every e: 6,900 checks; aligned. (4) §2.2 credited the printed lab with the gate's wider Kneser sampling (Z₁₀ to size 5, Z₁₂ to size 4, all of Z₃², 40,000 sampled Z₄² pairs) — re-attributed to the verification record; the printed census is Z₆–Z₉. (5) §2.5 credited the printed lab with the gate's 20,000-sample sweeps at n = 9, 10 — re-attributed the same way; the printed lab is exhaustive n = 3–7. (6) §2.5's prime-case sentence counted 225 trivial-case runs — the lab's own printed record says 44 (900 runs, trivial 44, non-trivial 856); aligned to it. (7) Part 1's verified output recorded 16,988 zero-gain steps — under the printed code the count is 9,759 (all with the running set already the whole field; the theory decomposes it 9,681 + 78), reproduced twice; the recorded line now prints `8624 9759 True 8624`, and A2's citation carries the same number. (8) Part 3(h)'s union-closed block enumerated `for mask in range(1, 1 << n)` — 7 masks at n = 3 and 15 at n = 4, which cannot produce the recorded census; the corrected `range(1, 1 << (1 << n))` reproduces the record exactly ([3] 121 closed, 120 nonempty, 0 failures, 98 with a singleton, 0 bad; [4] 4,959 / 4,958 / 0 / 4,126 / 0) — recorded outputs correct, printed code repaired, outputs unchanged. **The fresh battery (all green, condensed):** the weak-form recursion census on all twelve groups of order ≤ 9 exact against §3.1's table (738,884 pairs, 185,060 Case-1, 553,824 staircase bases, 1,355,220 Case-2 steps, max depth 5, zero violations of any property); the §3.2 counterexample and Exercise 10's six portions reproduced exactly; DeVos's machinery on the 39,449 aperiodic pairs of Z₆, Z₇, Z₈, Z₄×Z₂ (translate, Z₀-portion, trivial exit all clean; stab(Z₀) nontrivial on 3,604 = 60 / 0 / 930 / 2,614); the lab's LCG engines reproduced line for line (the staircase witness, 473,998 C–D pairs with 42,081 tight, the merge monitor, the e-transform 6,900, the m-fold 600, EGZ exhaustive 21 / 120 / 715 / 4,368 / 27,132, the pairing 800, the prime case 900 / 44 / 856 / 856, the composite chain 300); A16's 9,261 triples, 194,481 quadruples, and 250,047 mixed sums with the 8-type orbit classification exact; A17's regime boundary (the binomial wall at every prime p ≤ 19, the whole-field costume, the disassembly, F₅ and F₇ exhaustive plus F₁₁ sampled); A19's near-miss census — all 873,912 multisets n = 3–9, avoiders exactly the two-value coprime families, counts n·φ(n)/2, zero exotics; the shadow censuses — deep = complete with zero exceptions at (6, 2), (6, 3) (42), (6, 4) (22), and (7, 5) (29 = 21 K⁵₅ + 7 K⁵₆ + 1 K⁵₇); the mirror partitions and star mirrors ((9, 4) 56 + 70 = 126, (5, 2) 4 + 6, (7, 3) 15 + 20, (8, 3) 21 + 35; h(t) = C(t, 5) + C(t, 4) = 6, 21, 56, 126 with h(8) = C(9, 4)); the ten-edge hunt's 352,716 graphs (2,310 at t = 7, none at 8 or 9, exactly 21 at t = 10, all K₅ plus two isolated, the per-vertex ceilings K(v) ≤ 10 − d(v) and K(v) ≤ (3/2)d(v) clean at every vertex of every graph); the [6] costume's 57 equality families (15 edges, 20 triangles, 15 K₄, 6 K₅, 1 K₆); the HM(7, 3) maximal census (6,127 maximal families, maximum 15 by the 7 stars, empty-core maximum 13 by the 140 HM-type + 35 F₁, none unmatched); the AK sizes [15, 13, 10, 0]; the union-closed census under the repaired range; and Gilmer's constant (3 − √5)/2; and the (9, 4) empty-core hunt of ◐15, here upgraded from honest budget to proof: a branch-and-bound search (6,374 nodes, no budget exhaustion) certifies that no intersecting 4-family on [9] with empty core reaches 54 — the maximum is exactly 53, the Hilton–Milner size, attained by the HM-type family (verified pairwise intersecting with core ∅). Cross-references: the Chapter 6, 7, and 8 pointers valid (the multilinear lemma, the circle method, the complementary pair, the shifting lecture, ◐15, the equitable quotient); the pattern index consistent with the atlas (P4: 16, 20; P22: 17; P23: 19; the lore rows 11 and 18). Checker-side alarms, all the reviewer's own, re-run green: the DeVos Z₄×Z₂ record requires the column-major encoding where the recursion census is row-major, the product-group negation is not N−j in mixed moduli, and the review's own census tools threw three self-bugs (a 32-bit shift wrap in the (7,5) pin census, a combinatorial-iterator placeholder, and a per-vertex push duplication in the ten-edge hunt) — each caught by its own count check and fixed before any finding was recorded. Per the rebuild rule the web edition and the .html export were rebuilt — fidelity proof first — and the review arc advances to Chapter 10.

**Expansion-pass adoption (session 93).** An expansion-pass draft of this chapter — HTML/MathJax, adopted content-only per the atlas's no-script rule — was referee-adopted under the standing protocol: register-first extraction, an R1 diff ledger (adopt/merge/reject/defect), R2 re-verification of every printed receipt, R3 figure validation, extend-never-rewrite assembly. The edits it drove: proofs tightened across all five lectures (§1.1's same-difference characterization of staircase equality; §1.2's merge by iterated doubling, with the e-transform induction traced in the lab; §1.3's Lagrange-basis identity with the explicit a + b ≥ p + 1 whole-field case; §1.4's explicit induction; §2.1's strong-form-first ordering; §2.2's finite-subgroup qualifier; §2.4's Move 2 with H finite; §2.5's EGZ canonicalized — p ≥ 3 forced, aᵢ ≢ bᵢ (mod p), the multiplicative step, explicit block indices; §3.1's finiteness arguments; §3.3 rebuilt with the draft's fuller DeVos proof — K finite, quotient-branch measure drop, translate invariances, stab(Zᵢ) via the unique H-coset; §4.2's y_v existence/uniqueness and equality analysis; §5.2's guarded one-level corollary and deep lemma); three master defects sealed (D1: EGZ is 1961, not 1965 — Erdős–Ginzburg–Ziv, Bull. Res. Council Israel 10F, 1961; D2: §4.4's "two lectures ahead" → "in the next lecture"; D3: Figure 1 highlighted the wrong cells — the interior 4 blue, the staircase 2 white — the redesign highlights the staircase cells 2, 3, 5, 7 with step arrows, witness labels, and a number line, geometry-validated cell by cell); two answer merges (A16's lesson: common-difference sufficiency plus the equivalence-class honesty; A17's moral: the boundary owned precisely, min(p, ·) the seam); two web-verified claims adopted (Gilmer's bound "improved slightly by subsequent authors" — improvements followed within days; A19's near-miss classification credited to Gao / Savchev–Chen, defensible via Gao–Zhuang 2005 at G = Cₙ); Exercise 2 now runs both merge routes and compares; and A8's weighted-sum identity re-proved from total degree alone via the monomial route (the old text interpolated in x under a hypothesis the identity does not carry). The lab's five parts are the draft's fuller runnable copies, with two draft defects caught and sealed in place: (1) the A16 orbit loop classified under the 42 affine maps alone — under that closure the 1,029 tight triples give [21, 42×24], while the recorded 8-type census [21, 126×6, 252] is the affine-plus-summand-reordering (S₃) classification; the printed code now closes under both and reproduces the record exactly, and A16's prose says so; (2) the DeVos Z₄×Z₂ block carried the row-major encoding while its record (14,400 aperiodic pairs, 2,614 nontrivial stab(Z₀), 0 violations) is column-major — the standing session-67 checker alarm; the lambdas repaired, the record unchanged, re-verified. Every receipt re-verified green in a fresh TypeScript battery before installation — the two witnesses; C–D 473,998/0/42,081; the merge monitor 8,624/9,759/all-full; the polynomial suite 15,011 evaluations + 184 grid reconstructions + 900 weighted-sum tests + 450 vanishing checks + the p ≤ 19 regime wall + the 35-subset disassembly (returning {3}, zero vanishing grids); Kneser both forms over Z₆–Z₉ (3,969/16,129/65,025/261,121 pairs; 0/0 violations; tight 1,004/3,382/7,269/17,524); the e-transform 6,900; the m-fold 600; A16 (9,261/1,029/2,058/194,481/7,203, orbits [21, 126×6, 252]); EGZ (21/120/715/4,368/27,132; pairing 800; prime case 900/44/0 pair-fails/856/856; composite chain 300 with the unscaled mod-nm and size checks); A19 (873,912 multisets; counts [3, 4, 10, 6, 21, 16, 27]; 0 exotics); the cascade 781/781 and cascade(10, 3) = 10; the shadow censuses 57×3 at (6, 2) and 42×3 at (6, 3), all equalities complete; the mirrors (192 families/0 violations/max 5 by 6/mirror-eq 26, j-form slack 0.0 on the stars and 3.6 on the triangles; 59,049/0/10 by 1,024/1,024); Hilton–Milner at (7, 3) (6,127 maximal; max 15 by 7; empty-core 13 by 175 = 140 HM + 35 F₁); the AK sizes [15, 13, 10, 0] and [6, 7, 10, 0]; F1/HM 70/75, 51/53, 288/316; union-closed 121 (120)/0 and 4,959 (4,958)/0; Gilmer 0.3819660112501051; the A4 traces ('case1', 0), ('base', 1), ('base', 2); the recursion rows Z₄/Z₆/Z₇ (225/41/184/167, 3,969/872/3,097/4,939, 16,129/3,473/12,656/24,333); the §3.2 counterexample with its four transforms and the six portions; DeVos 1,080/60/0, 5,537/0/0, 18,432/930/0, 14,400/2,614/0; the deep censuses 42/22/29 with the by_u histograms exact; the ten-edge hunt 352,716/21/0 ceiling violations/hist [2,310, 0, 0, 21]; the mirror partitions and h-values [6, 21, 56, 126] — and the twelve-group recursion sweep re-run in TypeScript, all twelve rows of §3.1's table exact (738,884 pairs, 185,060 Case-1 terminations, 553,824 staircase bases, 1,355,220 steps, maximum depth 5). Checker honesty, recorded: three checker-side bugs during verification (an awk extraction bug that dropped same-line <pre> content — two findings retracted, the draft keeps the comb import and the Gilmer and h(8) prints; a negative-mod slip in a first polynomial-suite port; an order-of-operations slip in a first quick-sweep) — each caught, fixed, and superseded; the two draft defects above are the only ones that reached the master's repair queue.

---
*Chapter status: ✅ **Feynman edition + exercise backfill (session 41) + adversarial review (session 67) + expansion-pass adoption (session 93)** — 5 lectures (the staircase and Cauchy–Davenport; Kneser's theorem and the zero-sum capstone; the assembly completed: Dyson's recursion and DeVos's proof; shadows: the Kruskal–Katona theorem; uniqueness completed: the shade route), all proofs complete with citations kept honest; 1 verified figure; 16 graded exercises + 2 ◆ pattern-unknown + 2 ◐ explorations, 18 worked answers machine-verified; lab in 5 verified parts (sumsets; EGZ; shadows and the frontiers; the assembly; the shade route). Born in Chapter 7, exported by the restructure, completed here as a standalone course: the sumset and shadow arcs close, and with them the three flags the restructure left open. The session-67 adversarial review audited the chapter end to end — one lecture-wording repair (§3.2's canonical-witness attribution), four record-level alignments (§1.2's merge processes, §2.3's e-transform checks, §2.2's and §2.5's gate attributions, §2.5's trivial-case count), one monitor-output repair (Part 1's and A2's zero-gain count), and one lab-code repair (Part 3(h)'s union-closed range), the mathematics otherwise clean. The session-93 expansion pass was then adopted under referee protocol — proofs tightened across all five lectures, the redesigned Figure 1 (the old figure highlighted the wrong cells), the EGZ date sealed at 1961, the lab's five parts replaced by the draft's fuller runnable copies with two draft defects machine-sealed (the A16 orbit closure, the DeVos Z₄×Z₂ encoding), and every receipt re-verified green in a fresh TypeScript battery, the twelve-group sweep included. Ships with its web edition (the standard delivery format): the HTML canvas embeds this chapter byte-identically; print to PDF from a browser for a correct export.*
