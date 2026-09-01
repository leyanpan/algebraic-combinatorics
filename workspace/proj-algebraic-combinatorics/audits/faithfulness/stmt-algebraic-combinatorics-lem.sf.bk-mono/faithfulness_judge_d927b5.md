## TARGET benderKnuthInvol_mono (theorem) — ELABORATED SIGNATURE
∀ {N : ℕ} [inst : NeZero N] (lam mu : NPartition N) (k : Fin N) (hk : ↑k + 1 < N),
  ∀ f ∈ ssytFillings lam mu,
    fillingMonomial (benderKnuthInvol lam mu k hk f) =
      (MvPolynomial.rename ⇑(simpleTransposition k hk)) (fillingMonomial f)

Docstring: The monomial effect of the Bender-Knuth involution:
x_{BK_k(f)} = (swap x_k x_{k+1}) · x_f

This says that BK_k effectively swaps the roles of variables x_k and x_{k+1}
in the monomial, which is the key property for proving symmetry.

The proof uses `benderKnuthInvol_content_swap_spec`: if the content swaps k and k+1,
then the monomial (which is ∏ i, X i ^ content(f)(i)) is renamed by swap k (k+1). 

## PROJECT DEPENDENCY NPartition (inductive)
ℕ → Type

Body:
NPartition.mk : {N : ℕ} → (parts : Fin N → ℕ) → Antitone parts → NPartition N

Docstring: An N-partition is a weakly decreasing N-tuple of nonnegative integers.
(Definition def.sf.Npar)

This is represented as a function `Fin N → ℕ` that is antitone
(i.e., `i ≤ j → parts j ≤ parts i`).

The field is named `antitone` to match Mathlib conventions. 

## PROJECT DEPENDENCY SkewFilling (def)
{N : ℕ} → [NeZero N] → NPartition N → NPartition N → Type

Body:
fun {N} [NeZero N] lam mu => { c // c ∈ skewYoungDiagram lam mu } → Fin N

Docstring: The type of all fillings of a skew diagram with entries in Fin N.
This is finite since the diagram is finite and Fin N is finite. 

## PROJECT DEPENDENCY ssytFillings (def)
{N : ℕ} → [inst : NeZero N] → (lam mu : NPartition N) → Finset (SkewFilling lam mu)

Body:
fun {N} [NeZero N] lam mu => Finset.filter (isSSYTFilling lam mu) Finset.univ

Docstring: The finite set of all valid SSYT fillings. 

## PROJECT DEPENDENCY fillingMonomial (def)
{N : ℕ} → [inst : NeZero N] → {lam mu : NPartition N} → SkewFilling lam mu → MvPolynomial (Fin N) ℤ

Body:
fun {N} [NeZero N] {lam mu} f => ∏ c, MvPolynomial.X (f c)

Docstring: The monomial associated to a filling.
x_f = ∏_{c ∈ Y(λ/μ)} x_{f(c)} 

## PROJECT DEPENDENCY benderKnuthInvol (def)
{N : ℕ} →
  [inst : NeZero N] → (lam mu : NPartition N) → (k : Fin N) → ↑k + 1 < N → SkewFilling lam mu → SkewFilling lam mu

Body:
fun {N} [NeZero N] lam mu k hk f =>
  have T := (skewFillingEquiv lam mu) f;
  if hT : AlgebraicCombinatorics.IsSemistandard T then
    (skewFillingEquiv lam mu).symm (AlgebraicCombinatorics.benderKnuth k hk T hT)
  else f

Docstring: The Bender-Knuth involution BK_k on skew fillings.

For a filling f and index k, BK_k swaps certain entries k and k+1 while preserving
the semistandardness property. The construction works row by row:
- In each row, identify which k's and (k+1)'s are "free" (not forced by column constraints)
- Use parenthesis-matching: each free (k+1) "matches" with the nearest unmatched free k to its left
- Only UNMATCHED free entries get swapped

**Implementation**: This bridges to the full implementation in `LittlewoodRichardson.lean`
via `skewFillingEquiv`. For SSYT fillings, it applies `AlgebraicCombinatorics.benderKnuth`;
for non-SSYT fillings, it returns the input unchanged (the lemmas only apply to SSYT anyway). 

## PROJECT DEPENDENCY simpleTransposition (def)
{N : ℕ} → (k : Fin N) → ↑k + 1 < N → Equiv.Perm (Fin N)

Body:
fun {N} k hk => Equiv.swap k ⟨↑k + 1, hk⟩

Docstring: The simple transposition swapping k and k+1.

This is an alternative signature for `AlgebraicCombinatorics.simpleTransposition`.
Instead of taking `Fin (N - 1)` (which encodes the constraint), this takes
`Fin N` with an explicit proof `hk : k.val + 1 < N`.

See `simpleTransposition_eq_canonical` for the equivalence with the canonical definition. 

## PROJECT DEPENDENCY skewYoungDiagram (def)
{N : ℕ} → [NeZero N] → NPartition N → NPartition N → Finset (Fin N × ℕ)

Body:
fun {N} [NeZero N] lam mu => lam.youngDiagram \ mu.youngDiagram

Docstring: The skew Young diagram Y(λ/μ) is the set difference Y(λ) \ Y(μ).
Definition \ref{def.sf.skew-diag} in the source.

**Note**: This is a duplicate of `NPartition.skewYoungDiagram` that requires `[NeZero N]`.
Prefer `NPartition.skewYoungDiagram` for new code as it works for all `N`.

For N-partitions λ and μ with μ ⊆ λ, the skew Young diagram Y(λ/μ) is defined as:
```
Y(λ) \ Y(μ) = {(i,j) | i ∈ [N] and j ∈ [λ_i] \ [μ_i]}
            = {(i,j) | i ∈ [N] and j ∈ ℤ and μ_i < j ≤ λ_i}
```
(The second form uses 1-indexed j as in the textbook.)

In our 0-indexed formalization, this becomes:
```
Y(λ/μ) = {(i,j) | i ∈ Fin N and μ_i ≤ j < λ_i}
```

Example: Y((4,3,1)/(2,1,0)) consists of cells:
- Row 0: (0, 2), (0, 3)  (since μ₀ = 2, λ₀ = 4)
- Row 1: (1, 1), (1, 2)  (since μ₁ = 1, λ₁ = 3)
- Row 2: (2, 0)          (since μ₂ = 0, λ₂ = 1) 

## PROJECT DEPENDENCY isSSYTFilling (def)
{N : ℕ} → [inst : NeZero N] → (lam mu : NPartition N) → SkewFilling lam mu → Prop

Body:
fun {N} [NeZero N] lam mu f =>
  (∀ (c1 c2 : { c // c ∈ skewYoungDiagram lam mu }), (↑c1).1 = (↑c2).1 → (↑c1).2 < (↑c2).2 → f c1 ≤ f c2) ∧
    ∀ (c1 c2 : { c // c ∈ skewYoungDiagram lam mu }), (↑c1).2 = (↑c2).2 → (↑c1).1 < (↑c2).1 → f c1 < f c2

Docstring: The set of fillings that correspond to valid semistandard tableaux.
We check the conditions on pairs of cells in the diagram:
- Row-weak: if c1 and c2 are in the same row with c1 to the left, then f(c1) ≤ f(c2)
- Column-strict: if c1 and c2 are in the same column with c1 above, then f(c1) < f(c2) 

## PROJECT DEPENDENCY isSSYTFilling_decidable (def)
{N : ℕ} → [inst : NeZero N] → (lam mu : NPartition N) → (f : SkewFilling lam mu) → Decidable (isSSYTFilling lam mu f)

Body:
fun {N} [NeZero N] lam mu f => id inferInstance

Docstring: The SSYT condition is decidable since we're quantifying over finite types. 

## PROJECT DEPENDENCY skewFilling_fintype (def)
{N : ℕ} → [inst : NeZero N] → (lam mu : NPartition N) → Fintype (SkewFilling lam mu)

Body:
fun {N} [NeZero N] lam mu => Fintype.ofFinite (SkewFilling lam mu)

Docstring: Fillings are finite. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.Tableau (def)
{N : ℕ} → (Fin N → ℕ) → (Fin N → ℕ) → Type

Body:
fun {N} lam mu => { c // c ∈ AlgebraicCombinatorics.skewYoungDiagram lam mu } → Fin N

Docstring: A tableau of shape lam/mu is a function from cells to [N]. 

## PROJECT DEPENDENCY NPartition.parts (def)
{N : ℕ} → NPartition N → Fin N → ℕ

Body:
fun N self => self.1

Docstring: The entries of the N-partition as a function from `Fin N` to `ℕ` 

## PROJECT DEPENDENCY skewFillingEquiv (def)
{N : ℕ} →
  [inst : NeZero N] → (lam mu : NPartition N) → SkewFilling lam mu ≃ AlgebraicCombinatorics.Tableau lam.parts mu.parts

Body:
fun {N} [NeZero N] lam mu => (skewCellEquiv lam mu).arrowCongr (Equiv.refl (Fin N))

Docstring: Filling bijection: convert between SkewFilling and Tableau.

This bridges the two representations by composing with the cell bijection. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.IsSemistandard (def)
{N : ℕ} → {lam mu : Fin N → ℕ} → AlgebraicCombinatorics.Tableau lam mu → Prop

Body:
fun {N} {lam mu} T =>
  (∀ (c₁ c₂ : { c // c ∈ AlgebraicCombinatorics.skewYoungDiagram lam mu }),
      (↑c₁).1 = (↑c₂).1 → (↑c₁).2 < (↑c₂).2 → T c₁ ≤ T c₂) ∧
    ∀ (c₁ c₂ : { c // c ∈ AlgebraicCombinatorics.skewYoungDiagram lam mu }),
      (↑c₁).2 = (↑c₂).2 → (↑c₁).1 < (↑c₂).1 → T c₁ < T c₂

Docstring: A tableau is semistandard if entries weakly increase along rows
and strictly increase down columns. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.isSemistandard_decidable (def)
{N : ℕ} →
  {lam mu : Fin N → ℕ} →
    (T : AlgebraicCombinatorics.Tableau lam mu) → Decidable (AlgebraicCombinatorics.IsSemistandard T)

Body:
fun {N} {lam mu} T => id inferInstance

Docstring: IsSemistandard is decidable since it's a conjunction of foralls over finite types. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.benderKnuth (def)
{N : ℕ} →
  {lam mu : Fin N → ℕ} →
    (k : Fin N) →
      ↑k + 1 < N →
        (T : AlgebraicCombinatorics.Tableau lam mu) →
          AlgebraicCombinatorics.IsSemistandard T → AlgebraicCombinatorics.Tableau lam mu

Body:
fun {N} {lam mu} k hk T _hT c =>
  if AlgebraicCombinatorics.isUnmatchedFreeK T k hk c then ⟨↑k + 1, hk⟩
  else if AlgebraicCombinatorics.isUnmatchedFreeKSucc T k hk c then k else T c

Docstring: The Bender-Knuth involution BK_k on semistandard tableaux.

This involution swaps UNMATCHED free k's with UNMATCHED free (k+1)'s in each row,
using a parenthesis-matching algorithm that preserves semistandardness.

**Algorithm** (for each row independently):
1. Identify all "free" entries (k's not paired with k+1 below, (k+1)'s not paired with k above)
2. Read free entries left-to-right, matching each (k+1) with nearest unmatched k to its left
3. Swap only the UNMATCHED entries: unmatched k → k+1, unmatched (k+1) → k

**Why this preserves row-weak ordering**:
- Matched pairs don't change
- Unmatched k's (which become k+1) are always to the RIGHT of all matched (k+1)'s
- Unmatched (k+1)'s (which become k) are always to the LEFT of all matched k's

**Key theorem**: This is an involution that preserves semistandardness
and swaps the counts of k and k+1 in the content.

**Note**: The naive cell-by-cell swap (swapping ALL free entries) is INCORRECT
because adjacent free k and free (k+1) would become (k+1, k), violating row-weak ordering.
The parenthesis-matching ensures only non-adjacent free entries get swapped. 

## PROJECT DEPENDENCY NPartition.youngDiagram (def)
{N : ℕ} → NPartition N → Finset (Fin N × ℕ)

Body:
fun {N} μ => Finset.univ.biUnion fun i => Finset.map { toFun := fun j => (i, j), inj' := ⋯ } (Finset.range (μ.parts i))

Docstring: The Young diagram Y(λ) of an N-partition λ is the set of cells (i, j) where
i ∈ Fin N and j < λ_i.
Definition def.sf.ydiag in the source.

Note: Mathlib has `YoungDiagram` which is more general (infinite diagrams).
Here we define a version specific to N-partitions. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.skewYoungDiagram (def)
{N : ℕ} → (Fin N → ℕ) → (Fin N → ℕ) → Set (Fin N × ℕ)

Body:
fun {N} lam mu => {c | mu c.1 < c.2 ∧ c.2 ≤ lam c.1}

Docstring: The skew Young diagram Y(lam/mu) as a set of cells.
A cell (i,j) is in Y(lam/mu) if mu_i < j ≤ lam_i.

**This is the `Set` version with 1-indexed columns (textbook convention).**
The first column is j = 1, not j = 0.

For the canonical `Finset` version with 0-indexed columns, see:
- `NPartition.skewYoungDiagram` in NPartition.lean (canonical, no `[NeZero N]` required)
- `skewYoungDiagram` in SchurBasics.lean (duplicate, requires `[NeZero N]`)

Comparison:
- Here: (i, j) ∈ Y(λ/μ) iff μ_i < j ≤ λ_i (1-indexed)
- NPartition/SchurBasics: (i, j) ∈ Y(λ/μ) iff μ_i ≤ j < λ_i (0-indexed)

The bijection between them is: (i, j) here ↔ (i, j-1) in NPartition/SchurBasics.
See `SchurBasics.mem_skewYoungDiagram_iff_mem_LR_shifted` for the conversion lemma. 

## PROJECT DEPENDENCY skewCellEquiv (def)
{N : ℕ} →
  [inst : NeZero N] →
    (lam mu : NPartition N) →
      { c // c ∈ skewYoungDiagram lam mu } ≃ { c // c ∈ AlgebraicCombinatorics.skewYoungDiagram lam.parts mu.parts }

Body:
fun {N} [NeZero N] lam mu =>
  {
    toFun := fun x =>
      match x with
      | ⟨c, hc⟩ => ⟨(c.1, c.2 + 1), ⋯⟩,
    invFun := fun x =>
      match x with
      | ⟨c, hc⟩ => ⟨(c.1, c.2 - 1), ⋯⟩,
    left_inv := ⋯, right_inv := ⋯ }

Docstring: Cell bijection: SchurBasics cell (i, j) ↔ LittlewoodRichardson cell (i, j+1).

SchurBasics: (i, j) ∈ Y(λ/μ) iff μ_i ≤ j < λ_i
LittlewoodRichardson: (i, j) ∈ Y(λ/μ) iff μ_i < j ≤ λ_i

The map (i, j) ↦ (i, j+1) transforms the first to the second. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.skewYoungDiagram_fintype (def)
{N : ℕ} → (lam mu : Fin N → ℕ) → Fintype { c // c ∈ AlgebraicCombinatorics.skewYoungDiagram lam mu }

Body:
fun {N} lam mu => ⋯.fintype

Docstring: The set of cells in the skew Young diagram as a Fintype. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.isUnmatchedFreeK (def)
{N : ℕ} →
  {lam mu : Fin N → ℕ} →
    AlgebraicCombinatorics.Tableau lam mu →
      (k : Fin N) → ↑k + 1 < N → { c // c ∈ AlgebraicCombinatorics.skewYoungDiagram lam mu } → Prop

Body:
fun {N} {lam mu} T k hk c =>
  T c = k ∧
    ¬AlgebraicCombinatorics.isForcedK T k hk c ∧
      AlgebraicCombinatorics.freeKCountUpTo T (↑c).1 k hk (↑c).2 > AlgebraicCombinatorics.freeKSuccCount T (↑c).1 k hk

Docstring: A free k at position c is "unmatched" in the parenthesis-matching sense.

The Bender-Knuth involution uses a parenthesis-matching algorithm:
- Read free entries left-to-right in each row
- Each free (k+1) matches with the nearest unmatched free k to its left
- Unmatched entries get swapped

A free k is unmatched iff at its position, the cumulative count of free k's exceeds
the TOTAL count of free (k+1)'s in the row. In other words, there aren't enough (k+1)'s
in the entire row to match all the k's up to this position.

This definition correctly implements the standard parenthesis-matching algorithm:
- Unmatched k's are exactly those at positions where there's an "excess" of k's
- These are the rightmost free k's that don't have a (k+1) to match with

Note: We compare freeKCountUpTo(c) with freeKSuccCount (total), not freeKSuccCountUpTo(c),
because a k can match with any (k+1) to its right, not just (k+1)'s up to its position. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.isUnmatchedFreeKSucc (def)
{N : ℕ} →
  {lam mu : Fin N → ℕ} →
    AlgebraicCombinatorics.Tableau lam mu →
      (k : Fin N) → ↑k + 1 < N → { c // c ∈ AlgebraicCombinatorics.skewYoungDiagram lam mu } → Prop

Body:
fun {N} {lam mu} T k hk c =>
  T c = ⟨↑k + 1, hk⟩ ∧
    ¬AlgebraicCombinatorics.isForcedKSucc T k hk c ∧
      AlgebraicCombinatorics.freeKCount T (↑c).1 k hk + AlgebraicCombinatorics.freeKSuccCountUpTo T (↑c).1 k hk (↑c).2 ≤
        AlgebraicCombinatorics.freeKSuccCount T (↑c).1 k hk

Docstring: A free (k+1) at position c is "unmatched" in the parenthesis-matching sense.

In the BK involution on a semistandard row with `a` free k's followed by `b` free (k+1)'s:
- If b > a: the LEFTMOST (b-a) free (k+1)'s are unmatched → become k
- If a ≥ b: all free (k+1)'s are matched (paired with the rightmost b free k's)

A free (k+1) at position c is unmatched iff it's among the leftmost (b-a) free (k+1)'s,
i.e., the cumulative count of free (k+1)'s up to c is at most (b-a).

Equivalently: `freeKSuccCountUpTo(c) + freeKCount ≤ freeKSuccCount`

This marks the LEFTMOST excess (k+1)'s as unmatched, which is correct for the BK involution.
The matched pairs are: leftmost min(a,b) k's paired with rightmost min(a,b) (k+1)'s.

Note: The previous (incorrect) definition used `freeKSuccCountUpTo > freeKCountUpTo`,
which marked RIGHTMOST (k+1)'s as unmatched — the wrong polarity. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.skewYoungDiagram_finite (theorem)
∀ {N : ℕ} (lam mu : Fin N → ℕ), (AlgebraicCombinatorics.skewYoungDiagram lam mu).Finite

Docstring: The skew Young diagram is finite. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.isForcedK (def)
{N : ℕ} →
  {lam mu : Fin N → ℕ} →
    AlgebraicCombinatorics.Tableau lam mu →
      (k : Fin N) → ↑k + 1 < N → { c // c ∈ AlgebraicCombinatorics.skewYoungDiagram lam mu } → Prop

Body:
fun {N} {lam mu} T k hk c =>
  T c = k ∧ ∃ c_below, (↑c_below).2 = (↑c).2 ∧ ↑(↑c).1 + 1 = ↑(↑c_below).1 ∧ T c_below = ⟨↑k + 1, hk⟩

Docstring: A cell containing k is "k-forced" if there's a k+1 directly BELOW it in the same column.
This means the k and the k+1 below it form a "pair" that won't be swapped by BK_k.

**Note**: The original (incorrect) definition said "k above k", but in a semistandard tableau,
entries strictly increase down columns, so you can't have the same value in vertically
adjacent cells. The correct definition is: k is paired with k+1 below it. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.freeKCountUpTo (def)
{N : ℕ} → {lam mu : Fin N → ℕ} → AlgebraicCombinatorics.Tableau lam mu → Fin N → (k : Fin N) → ↑k + 1 < N → ℕ → ℕ

Body:
fun {N} {lam mu} T i k hk j =>
  Nat.card { c // (↑c).1 = i ∧ (↑c).2 ≤ j ∧ T c = k ∧ ¬AlgebraicCombinatorics.isForcedK T k hk c }

Docstring: Count of free k's in row i with column at most j.
Used for the parenthesis-matching algorithm in Bender-Knuth. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.freeKSuccCount (def)
{N : ℕ} → {lam mu : Fin N → ℕ} → AlgebraicCombinatorics.Tableau lam mu → Fin N → (k : Fin N) → ↑k + 1 < N → ℕ

Body:
fun {N} {lam mu} T i k hk =>
  Nat.card { c // (↑c).1 = i ∧ T c = ⟨↑k + 1, hk⟩ ∧ ¬AlgebraicCombinatorics.isForcedKSucc T k hk c }

Docstring: Count of free (k+1)'s in row i. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.isForcedKSucc (def)
{N : ℕ} →
  {lam mu : Fin N → ℕ} →
    AlgebraicCombinatorics.Tableau lam mu →
      (k : Fin N) → ↑k + 1 < N → { c // c ∈ AlgebraicCombinatorics.skewYoungDiagram lam mu } → Prop

Body:
fun {N} {lam mu} T k hk c =>
  T c = ⟨↑k + 1, hk⟩ ∧ ∃ c_above, (↑c_above).2 = (↑c).2 ∧ ↑(↑c_above).1 + 1 = ↑(↑c).1 ∧ T c_above = k

Docstring: A cell containing k+1 is "(k+1)-forced" if there's a k directly ABOVE it in the same column.
This means the k above and this k+1 form a "pair" that won't be swapped by BK_k.

**Note**: The original (incorrect) definition said "k+1 below k+1", but in a semistandard
tableau, entries strictly increase down columns. The correct definition is: k+1 is paired
with k above it. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.freeKCount (def)
{N : ℕ} → {lam mu : Fin N → ℕ} → AlgebraicCombinatorics.Tableau lam mu → Fin N → (k : Fin N) → ↑k + 1 < N → ℕ

Body:
fun {N} {lam mu} T i k hk => Nat.card { c // (↑c).1 = i ∧ T c = k ∧ ¬AlgebraicCombinatorics.isForcedK T k hk c }

Docstring: Count of free k's in row i. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.freeKSuccCountUpTo (def)
{N : ℕ} → {lam mu : Fin N → ℕ} → AlgebraicCombinatorics.Tableau lam mu → Fin N → (k : Fin N) → ↑k + 1 < N → ℕ → ℕ

Body:
fun {N} {lam mu} T i k hk j =>
  Nat.card { c // (↑c).1 = i ∧ (↑c).2 ≤ j ∧ T c = ⟨↑k + 1, hk⟩ ∧ ¬AlgebraicCombinatorics.isForcedKSucc T k hk c }

Docstring: Count of free (k+1)'s in row i with column at most j.
Used for the parenthesis-matching algorithm in Bender-Knuth. 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF NeZero
{R : Type u_1} → [Zero R] → R → Prop

Docstring: A type-class version of `n ≠ 0`.  

## BASE-LIBRARY REF MulZeroClass.toZero
{M₀ : Type u} → [self : MulZeroClass M₀] → Zero M₀

## BASE-LIBRARY REF Nat.instMulZeroClass
MulZeroClass ℕ

## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


## BASE-LIBRARY REF LT.lt
{α : Type u} → [self : LT α] → α → α → Prop

Docstring: The less-than relation: `x < y` 

Conventions for notations in identifiers:

 * The recommended spelling of `<` in identifiers is `lt`.

## BASE-LIBRARY REF instLTNat
LT ℕ

## BASE-LIBRARY REF HAdd.hAdd
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HAdd α β γ] → α → β → γ

Docstring: `a + b` computes the sum of `a` and `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `+` in identifiers is `add`.

## BASE-LIBRARY REF instHAdd
{α : Type u_1} → [Add α] → HAdd α α α

## BASE-LIBRARY REF instAddNat
Add ℕ

## BASE-LIBRARY REF Fin.val
{n : ℕ} → Fin n → ℕ

Docstring: The number that is strictly less than `n`.

`Fin.val` is a coercion, so any `Fin n` can be used in a position where a `Nat` is expected.


## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

## BASE-LIBRARY REF Membership.mem
{α : outParam (Type u)} → {γ : Type v} → [self : Membership α γ] → γ → α → Prop

Docstring: The membership relation `a ∈ s : Prop` where `a : α`, `s : γ`. 

Conventions for notations in identifiers:

 * The recommended spelling of `∈` in identifiers is `mem`.

## BASE-LIBRARY REF Finset
Type u_4 → Type u_4

Docstring: `Finset α` is the type of finite sets of elements of `α`. It is implemented
as a multiset (a list up to permutation) which has no duplicate elements. 

## BASE-LIBRARY REF Finset.instMembership
{α : Type u_1} → Membership α (Finset α)

## BASE-LIBRARY REF Eq
{α : Sort u_1} → α → α → Prop

Docstring: The equality relation. It has one introduction rule, `Eq.refl`.
We use `a = b` as notation for `Eq a b`.
A fundamental property of equality is that it is an equivalence relation.
```
variable (α : Type) (a b c d : α)
variable (hab : a = b) (hcb : c = b) (hcd : c = d)

example : a = d :=
  Eq.trans (Eq.trans hab (Eq.symm hcb)) hcd
```
Equality is much more than an equivalence relation, however. It has the important property that every assertion
respects the equivalence, in the sense that we can substitute equal expressions without changing the truth value.
That is, given `h1 : a = b` and `h2 : p a`, we can construct a proof for `p b` using substitution: `Eq.subst h1 h2`.
Example:
```
example (α : Type) (a b : α) (p : α → Prop)
        (h1 : a = b) (h2 : p a) : p b :=
  Eq.subst h1 h2

example (α : Type) (a b : α) (p : α → Prop)
    (h1 : a = b) (h2 : p a) : p b :=
  h1 ▸ h2
```
The triangle in the second presentation is a macro built on top of `Eq.subst` and `Eq.symm`, and you can enter it by typing `\t`.
For more information: [Equality](https://lean-lang.org/theorem_proving_in_lean4/quantifiers_and_equality.html#equality)


Conventions for notations in identifiers:

 * The recommended spelling of `=` in identifiers is `eq`.

## BASE-LIBRARY REF MvPolynomial
Type u_1 → (R : Type u_2) → [CommSemiring R] → Type (max u_2 u_1)

Docstring: Multivariate polynomial, where `σ` is the index set of the variables and
`R` is the coefficient ring 

## BASE-LIBRARY REF Int
Type

Docstring: The integers.

This type is special-cased by the compiler and overridden with an efficient implementation. The
runtime has a special representation for `Int` that stores “small” signed numbers directly, while
larger numbers use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)). A “small number” is an integer that can be encoded with one fewer bits
than the platform's pointer size (i.e. 63 bits on 64-bit architectures and 31 bits on 32-bit
architectures).


## BASE-LIBRARY REF Int.instCommSemiring
CommSemiring ℤ

## BASE-LIBRARY REF DFunLike.coe
{F : Sort u_1} → {α : outParam (Sort u_2)} → {β : outParam (α → Sort u_3)} → [self : DFunLike F α β] → F → (a : α) → β a

Docstring: The coercion from `F` to a function. 

## BASE-LIBRARY REF AlgHom
(R : Type u) →
  (A : Type v) →
    (B : Type w) →
      [inst : CommSemiring R] →
        [inst_1 : Semiring A] → [inst_2 : Semiring B] → [Algebra R A] → [Algebra R B] → Type (max v w)

Docstring: Defining the homomorphism in the category R-Alg, denoted `A →ₐ[R] B`. 

## BASE-LIBRARY REF CommSemiring.toSemiring
{R : Type u} → [self : CommSemiring R] → Semiring R

## BASE-LIBRARY REF MvPolynomial.commSemiring
{R : Type u} → {σ : Type u_1} → [inst : CommSemiring R] → CommSemiring (MvPolynomial σ R)

## BASE-LIBRARY REF MvPolynomial.algebra
{R : Type u} →
  {S₁ : Type v} →
    {σ : Type u_1} →
      [inst : CommSemiring R] → [inst_1 : CommSemiring S₁] → [Algebra R S₁] → Algebra R (MvPolynomial σ S₁)

## BASE-LIBRARY REF Algebra.id
(R : Type u) → [inst : CommSemiring R] → Algebra R R

Docstring: The identity map inducing an `Algebra` structure. 

## BASE-LIBRARY REF AlgHom.funLike
{R : Type u} →
  {A : Type v} →
    {B : Type w} →
      [inst : CommSemiring R] →
        [inst_1 : Semiring A] →
          [inst_2 : Semiring B] → [inst_3 : Algebra R A] → [inst_4 : Algebra R B] → FunLike (A →ₐ[R] B) A B

## BASE-LIBRARY REF MvPolynomial.rename
{σ : Type u_1} →
  {τ : Type u_2} → {R : Type u_4} → [inst : CommSemiring R] → (σ → τ) → MvPolynomial σ R →ₐ[R] MvPolynomial τ R

Docstring: Rename all the variables in a multivariable polynomial. 

## BASE-LIBRARY REF Equiv.Perm
Sort u_1 → Sort (max 1 u_1)

Docstring: `Perm α` is the type of bijections from `α` to itself. 

## BASE-LIBRARY REF EquivLike.toFunLike
{E : Sort u_1} → {α : Sort u_3} → {β : Sort u_4} → [EquivLike E α β] → FunLike E α β

## BASE-LIBRARY REF Equiv.instEquivLike
{α : Sort u} → {β : Sort v} → EquivLike (α ≃ β) α β

## BASE-LIBRARY REF Antitone
{α : Type u} → {β : Type v} → [Preorder α] → [Preorder β] → (α → β) → Prop

Docstring: A function `f` is antitone if `a ≤ b` implies `f b ≤ f a`. 

## BASE-LIBRARY REF PartialOrder.toPreorder
{α : Type u_2} → [self : PartialOrder α] → Preorder α

## BASE-LIBRARY REF Fin.instPartialOrder
{n : ℕ} → PartialOrder (Fin n)

## BASE-LIBRARY REF Nat.instPreorder
Preorder ℕ

## BASE-LIBRARY REF Subtype
{α : Sort u} → (α → Prop) → Sort (max 1 u)

Docstring: All the elements of a type that satisfy a predicate.

`Subtype p`, usually written `{ x : α // p x }` or `{ x // p x }`, contains all elements `x : α` for
which `p x` is true. Its constructor is a pair of the value and the proof that it satisfies the
predicate. In run-time code, `{ x : α // p x }` is represented identically to `α`.

There is a coercion from `{ x : α // p x }` to `α`, so elements of a subtype may be used where the
underlying type is expected.

Examples:
 * `{ n : Nat // n % 2 = 0 }` is the type of even numbers.
 * `{ xs : Array String // xs.size = 5 }` is the type of arrays with five `String`s.
 * Given `xs : List α`, `List { x : α // x ∈ xs }` is the type of lists in which all elements are
   contained in `xs`.


Conventions for notations in identifiers:

 * The recommended spelling of `{ x // p x }` in identifiers is `subtype`.

## BASE-LIBRARY REF Prod
Type u → Type v → Type (max u v)

Docstring: The product type, usually written `α × β`. Product types are also called pair or tuple types.
Elements of this type are pairs in which the first element is an `α` and the second element is a
`β`.

Products nest to the right, so `(x, y, z) : α × β × γ` is equivalent to `(x, (y, z)) : α × (β × γ)`.


Conventions for notations in identifiers:

 * The recommended spelling of `×` in identifiers is `Prod`.

## BASE-LIBRARY REF Finset.filter
{α : Type u_1} → (p : α → Prop) → [DecidablePred p] → Finset α → Finset α

Docstring: `Finset.filter p s` is the set of elements of `s` that satisfy `p`.

For example, one can use `s.filter (· ∈ t)` to get the intersection of `s` with `t : Set α`
as a `Finset α` (when a `DecidablePred (· ∈ t)` instance is available). 

## BASE-LIBRARY REF Finset.univ
{α : Type u_1} → [Fintype α] → Finset α

Docstring: `univ` is the universal finite set of type `Finset α` implied from
the assumption `Fintype α`. 

## BASE-LIBRARY REF Finset.prod
{ι : Type u_1} → {M : Type u_3} → [CommMonoid M] → Finset ι → (ι → M) → M

Docstring: `∏ x ∈ s, f x` is the product of `f x` as `x` ranges over the elements of the finite set `s`.

When the index type is a `Fintype`, the notation `∏ x, f x`, is a shorthand for
`∏ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF CommRing.toCommMonoid
{α : Type u} → [self : CommRing α] → CommMonoid α

## BASE-LIBRARY REF MvPolynomial.instCommRingMvPolynomial
{R : Type u} → {σ : Type u_1} → [inst : CommRing R] → CommRing (MvPolynomial σ R)

## BASE-LIBRARY REF Int.instCommRing
CommRing ℤ

## BASE-LIBRARY REF Finset.Subtype.fintype
{α : Type u_1} → (s : Finset α) → Fintype { x // x ∈ s }

## BASE-LIBRARY REF MvPolynomial.X
{R : Type u} → {σ : Type u_1} → [inst : CommSemiring R] → σ → MvPolynomial σ R

Docstring: `X n` is the degree `1` monomial $X_n$. 

## BASE-LIBRARY REF Equiv
Sort u_1 → Sort u_2 → Sort (max (max 1 u_1) u_2)

Docstring: `α ≃ β` is the type of functions from `α → β` with a two-sided inverse. 

## BASE-LIBRARY REF dite
{α : Sort u} → (c : Prop) → [h : Decidable c] → (c → α) → (¬c → α) → α

Docstring: "Dependent" if-then-else, normally written via the notation `if h : c then t(h) else e(h)`,
is sugar for `dite c (fun h => t(h)) (fun h => e(h))`, and it is the same as
`if c then t else e` except that `t` is allowed to depend on a proof `h : c`,
and `e` can depend on `h : ¬c`. (Both branches use the same name for the hypothesis,
even though it has different types in the two cases.)

We use this to be able to communicate the if-then-else condition to the branches.
For example, `Array.get arr i h` expects a proof `h : i < arr.size` in order to
avoid a bounds check, so you can write `if h : i < arr.size then arr.get i h else ...`
to avoid the bounds check inside the if branch. (Of course in this case we have only
lifted the check into an explicit `if`, but we could also use this proof multiple times
or derive `i < arr.size` from some other proposition that we are checking in the `if`.)


## BASE-LIBRARY REF Equiv.symm
{α : Sort u} → {β : Sort v} → α ≃ β → β ≃ α

Docstring: Inverse of an equivalence `e : α ≃ β`. 

## BASE-LIBRARY REF Not
Prop → Prop

Docstring: `Not p`, or `¬p`, is the negation of `p`. It is defined to be `p → False`,
so if your goal is `¬p` you can use `intro h` to turn the goal into
`h : p ⊢ False`, and if you have `hn : ¬p` and `h : p` then `hn h : False`
and `(hn h).elim` will prove anything.
For more information: [Propositional Logic](https://lean-lang.org/theorem_proving_in_lean4/propositions_and_proofs.html#propositional-logic)


Conventions for notations in identifiers:

 * The recommended spelling of `¬` in identifiers is `not`.

## BASE-LIBRARY REF Equiv.swap
{α : Sort u_1} → [DecidableEq α] → α → α → Equiv.Perm α

Docstring: `swap a b` is the permutation that swaps `a` and `b` and
leaves other values as is. 

## BASE-LIBRARY REF instDecidableEqFin
(n : ℕ) → DecidableEq (Fin n)

## BASE-LIBRARY REF Fin.mk
{n : ℕ} → (val : ℕ) → val < n → Fin n

Docstring: Creates a `Fin n` from `i : Nat` and a proof that `i < n`. 

## BASE-LIBRARY REF SDiff.sdiff
{α : Type u} → [self : SDiff α] → α → α → α

Docstring: `a \ b` is the set difference of `a` and `b`,
consisting of all elements in `a` that are not in `b`.


Conventions for notations in identifiers:

 * The recommended spelling of `\` in identifiers is `sdiff`.

## BASE-LIBRARY REF Finset.instSDiff
{α : Type u_1} → [DecidableEq α] → SDiff (Finset α)

Docstring: `s \ t` is the set consisting of the elements of `s` that are not in `t`. 

## BASE-LIBRARY REF instDecidableEqProd
{α : Type u_1} → {β : Type u_2} → [DecidableEq α] → [DecidableEq β] → DecidableEq (α × β)

## BASE-LIBRARY REF instDecidableEqNat
DecidableEq ℕ

## BASE-LIBRARY REF And
Prop → Prop → Prop

Docstring: `And a b`, or `a ∧ b`, is the conjunction of propositions. It can be
constructed and destructed like a pair: if `ha : a` and `hb : b` then
`⟨ha, hb⟩ : a ∧ b`, and if `h : a ∧ b` then `h.left : a` and `h.right : b`.


Conventions for notations in identifiers:

 * The recommended spelling of `∧` in identifiers is `and`.

 * The recommended spelling of `/\` in identifiers is `and` (prefer `∧` over `/\`).

## BASE-LIBRARY REF Prod.fst
{α : Type u} → {β : Type v} → α × β → α

Docstring: The first element of a pair. 

## BASE-LIBRARY REF Subtype.val
{α : Sort u} → {p : α → Prop} → Subtype p → α

Docstring: The value in the underlying type that satisfies the predicate.


## BASE-LIBRARY REF Prod.snd
{α : Type u} → {β : Type v} → α × β → β

Docstring: The second element of a pair. 

## BASE-LIBRARY REF LE.le
{α : Type u} → [self : LE α] → α → α → Prop

Docstring: The less-equal relation: `x ≤ y` 

Conventions for notations in identifiers:

 * The recommended spelling of `≤` in identifiers is `le`.

 * The recommended spelling of `<=` in identifiers is `le` (prefer `≤` over `<=`).

## BASE-LIBRARY REF instLEFin
{n : ℕ} → LE (Fin n)

## BASE-LIBRARY REF instLTFin
{n : ℕ} → LT (Fin n)

## BASE-LIBRARY REF Decidable
Prop → Type

Docstring: Either a proof that `p` is true or a proof that `p` is false. This is equivalent to a `Bool` paired
with a proof that the `Bool` is `true` if and only if `p` is true.

`Decidable` instances are primarily used via `if`-expressions and the tactic `decide`. In
conditional expressions, the `Decidable` instance for the proposition is used to select a branch. At
run time, this case distinction code is identical to that which would be generated for a
`Bool`-based conditional. In proofs, the tactic `decide` synthesizes an instance of `Decidable p`,
attempts to reduce it to `isTrue h`, and then succeeds with the proof `h` if it can.

Because `Decidable` carries data, when writing `@[simp]` lemmas which include a `Decidable` instance
on the LHS, it is best to use `{_ : Decidable p}` rather than `[Decidable p]` so that non-canonical
instances can be found via unification rather than instance synthesis.


## BASE-LIBRARY REF id
{α : Sort u} → α → α

Docstring: The identity function. `id` takes an implicit argument `α : Sort u`
(a type in any universe), and an argument `a : α`, and returns `a`.

Although this may look like a useless function, one application of the identity
function is to explicitly put a type on an expression. If `e` has type `T`,
and `T'` is definitionally equal to `T`, then `@id T' e` typechecks, and Lean
knows that this expression has type `T'` rather than `T`. This can make a
difference for typeclass inference, since `T` and `T'` may have different
typeclass instances on them. `show T' from e` is sugar for an `@id T' e`
expression.


## BASE-LIBRARY REF inferInstance
{α : Sort u} → [i : α] → α

Docstring: `inferInstance` synthesizes a value of any target type by typeclass
inference. This function has the same type signature as the identity
function, but the square brackets on the `[i : α]` argument means that it will
attempt to construct this argument by typeclass inference. (This will fail if
`α` is not a `class`.) Example:
```
#check (inferInstance : Inhabited Nat) -- Inhabited Nat

def foo : Inhabited (Nat × Nat) :=
  inferInstance

example : foo.default = (default, default) :=
  rfl
```


## BASE-LIBRARY REF instDecidableAnd
{p q : Prop} → [dp : Decidable p] → [dq : Decidable q] → Decidable (p ∧ q)

## BASE-LIBRARY REF Fintype.decidableForallFintype
{α : Type u_1} → {p : α → Prop} → [DecidablePred p] → [Fintype α] → Decidable (∀ (a : α), p a)

## BASE-LIBRARY REF forall_prop_decidable
{p : Prop} → (P : p → Prop) → [Decidable p] → [(h : p) → Decidable (P h)] → Decidable (∀ (h : p), P h)

## BASE-LIBRARY REF Nat.decLt
(n m : ℕ) → Decidable (n < m)

Docstring: A decision procedure for strict inequality of natural numbers, usually accessed via the
`DecidableLT Nat` instance.

Examples:
 * `(if 3 < 4 then "yes" else "no") = "yes"`
 * `(if 4 < 4 then "yes" else "no") = "no"`
 * `(if 6 < 4 then "yes" else "no") = "no"`
 * `show 5 < 12 by decide`


## BASE-LIBRARY REF Fin.decLe
{n : ℕ} → (a b : Fin n) → Decidable (a ≤ b)

## BASE-LIBRARY REF Fin.decLt
{n : ℕ} → (a b : Fin n) → Decidable (a < b)

## BASE-LIBRARY REF Fintype
Type u_4 → Type u_4

Docstring: `Fintype α` means that `α` is finite, i.e. there are only
finitely many distinct elements of type `α`. The evidence of this
is a finset `elems` (a list up to permutation without duplicates),
together with a proof that everything of type `α` is in the list. 

## BASE-LIBRARY REF Fintype.ofFinite
(α : Type u_4) → [Finite α] → Fintype α

Docstring: Noncomputably get a `Fintype` instance from a `Finite` instance. This is not an
instance because we want `Fintype` instances to be useful for computations. 

## BASE-LIBRARY REF Set
Type u → Type u

Docstring: A set is a collection of elements of some type `α`.

Although `Set` is defined as `α → Prop`, this is an implementation detail which should not be
relied on. Instead, `setOf` and membership of a set (`∈`) should be used to convert between sets
and predicates.


## BASE-LIBRARY REF Set.instMembership
{α : Type u} → Membership α (Set α)

## BASE-LIBRARY REF Equiv.arrowCongr
{α₁ : Sort u_1} → {β₁ : Sort u_2} → {α₂ : Sort u_3} → {β₂ : Sort u_4} → α₁ ≃ α₂ → β₁ ≃ β₂ → (α₁ → β₁) ≃ (α₂ → β₂)

Docstring: If `α₁` is equivalent to `α₂` and `β₁` is equivalent to `β₂`, then the type of maps `α₁ → β₁`
is equivalent to the type of maps `α₂ → β₂`. 

## BASE-LIBRARY REF Equiv.refl
(α : Sort u_1) → α ≃ α

Docstring: Any type is equivalent to itself. 

## BASE-LIBRARY REF ite
{α : Sort u} → (c : Prop) → [h : Decidable c] → α → α → α

Docstring: `if c then t else e` is notation for `ite c t e`, "if-then-else", which decides to
return `t` or `e` depending on whether `c` is true or false. The explicit argument
`c : Prop` does not have any actual computational content, but there is an additional
`[Decidable c]` argument synthesized by typeclass inference which actually
determines how to evaluate `c` to true or false. Write `if h : c then t else e`
instead for a "dependent if-then-else" `dite`, which allows `t`/`e` to use the fact
that `c` is true/false.


## BASE-LIBRARY REF Classical.propDecidable
(a : Prop) → Decidable a

Docstring: All propositions are `Decidable`. 

## BASE-LIBRARY REF Finset.biUnion
{α : Type u_1} → {β : Type u_2} → [DecidableEq β] → Finset α → (α → Finset β) → Finset β

Docstring: `Finset.biUnion s t` is the union of `t a` over `a ∈ s`.

(This was formerly `bind` due to the monad structure on types with `DecidableEq`.) 

## BASE-LIBRARY REF Fin.fintype
(n : ℕ) → Fintype (Fin n)

## BASE-LIBRARY REF Finset.map
{α : Type u_1} → {β : Type u_2} → (α ↪ β) → Finset α → Finset β

Docstring: When `f` is an embedding of `α` in `β` and `s` is a finset in `α`, then `s.map f` is the image
finset in `β`. The embedding condition guarantees that there are no duplicates in the image. 

## BASE-LIBRARY REF Function.Embedding.mk
{α : Sort u_1} → {β : Sort u_2} → (toFun : α → β) → Function.Injective toFun → α ↪ β

## BASE-LIBRARY REF Prod.mk
{α : Type u} → {β : Type v} → α → β → α × β

Docstring: Constructs a pair. This is usually written `(x, y)` instead of `Prod.mk x y`.


Conventions for notations in identifiers:

 * The recommended spelling of `(a, b)` in identifiers is `mk`.

## BASE-LIBRARY REF Finset.range
ℕ → Finset ℕ

Docstring: `range n` is the set of natural numbers less than `n`. 

## BASE-LIBRARY REF setOf
{α : Type u} → (α → Prop) → Set α

Docstring: Turn a predicate `p : α → Prop` into a set, also written as `{x | p x}` 

## BASE-LIBRARY REF instLENat
LE ℕ

## BASE-LIBRARY REF Equiv.mk
{α : Sort u_1} →
  {β : Sort u_2} →
    (toFun : α → β) →
      (invFun : β → α) →
        autoParam (Function.LeftInverse invFun toFun) Equiv.left_inv._autoParam →
          autoParam (Function.RightInverse invFun toFun) Equiv.right_inv._autoParam → α ≃ β

## BASE-LIBRARY REF Subtype.mk
{α : Sort u} → {p : α → Prop} → (val : α) → p val → Subtype p

## BASE-LIBRARY REF HSub.hSub
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HSub α β γ] → α → β → γ

Docstring: `a - b` computes the difference of `a` and `b`.
The meaning of this notation is type-dependent.
* For natural numbers, this operator saturates at 0: `a - b = 0` when `a ≤ b`. 

Conventions for notations in identifiers:

 * The recommended spelling of `-` in identifiers is `sub` (when used as a binary operator).

## BASE-LIBRARY REF instHSub
{α : Type u_1} → [Sub α] → HSub α α α

## BASE-LIBRARY REF instSubNat
Sub ℕ

## BASE-LIBRARY REF Set.Finite.fintype
{α : Type u} → {s : Set α} → s.Finite → Fintype ↑s

Docstring: A finite set coerced to a type is a `Fintype`.
This is the `Fintype` projection for a `Set.Finite`.

Note that because `Finite` isn't a typeclass, this definition will not fire if it
is made into an instance 

## BASE-LIBRARY REF GT.gt
{α : Type u} → [LT α] → α → α → Prop

Docstring: `a > b` is an abbreviation for `b < a`. 

Conventions for notations in identifiers:

 * The recommended spelling of `>` in identifiers is `gt`.

## BASE-LIBRARY REF Set.Finite
{α : Type u} → Set α → Prop

Docstring: A set is finite if the corresponding `Subtype` is finite,
i.e., if there exists a natural `n : ℕ` and an equivalence `s ≃ Fin n`. 

## BASE-LIBRARY REF Exists
{α : Sort u} → (α → Prop) → Prop

Docstring: Existential quantification. If `p : α → Prop` is a predicate, then `∃ x : α, p x`
asserts that there is some `x` of type `α` such that `p x` holds.
To create an existential proof, use the `exists` tactic,
or the anonymous constructor notation `⟨x, h⟩`.
To unpack an existential, use `cases h` where `h` is a proof of `∃ x : α, p x`,
or `let ⟨x, hx⟩ := h` where `.

Because Lean has proof irrelevance, any two proofs of an existential are
definitionally equal. One consequence of this is that it is impossible to recover the
witness of an existential from the mere fact of its existence.
For example, the following does not compile:
```
example (h : ∃ x : Nat, x = x) : Nat :=
  let ⟨x, _⟩ := h  -- fail, because the goal is `Nat : Type`
  x
```
The error message `recursor 'Exists.casesOn' can only eliminate into Prop` means
that this only works when the current goal is another proposition:
```
example (h : ∃ x : Nat, x = x) : True :=
  let ⟨x, _⟩ := h  -- ok, because the goal is `True : Prop`
  trivial
```


## BASE-LIBRARY REF Nat.card
Type u_3 → ℕ

Docstring: `Nat.card α` is the cardinality of `α` as a natural number.
If `α` is infinite, `Nat.card α = 0`. 

## INFORMAL STATEMENT
lem.sf.bk-mono

\leanhelper  The monomial effect of the Bender–Knuth involution: $x_{\mathrm{BK}_k(f)} = (\text{swap } x_k\,  x_{k+1}) \cdot x_f$. 

This says that $\mathrm{BK}_k$ effectively swaps the roles of variables $x_k$ and $x_{k+1}$ in the monomial.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-conv-2eb59533
conv-2eb59533

In the Lean formalization, we use $\operatorname {Fin} n = \{ 0, 1, \ldots , n-1\} $ instead of the textbook’s $[n] = \{ 1, 2, \ldots , n\} $. Both are $n$-element sets, so their symmetric groups are isomorphic. Permutations are represented by the type of bijections $X \to X$ (denoted $\operatorname {Equiv.Perm}\,  X$ in Lean), which is a group under composition. Composition $\alpha \beta $ is the group multiplication $\alpha * \beta $, sending $x$ to $\alpha (\beta (x))$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.perm
def.perm.perm

Let $X$ be a set. 

\textbf{(a)} A \emph{permutation} of $X$ means a bijection from $X$ to $X$. 

\textbf{(b)} It is known that the set of all permutations of $X$ is a group under composition. This group is called the \emph{symmetric group} of $X$, and is denoted by $S_X$. Its neutral element is the identity map $\operatorname {id}_X : X \to X$. Its size is $|X|!$ when $X$ is finite. 

\textbf{(c)} As usual in group theory, we will write $\alpha \beta $ for the composition $\alpha \circ \beta $ when $\alpha , \beta \in S_X$. This is the map that sends each $x \in X$ to $\alpha (\beta (x))$. 

\textbf{(d)} If $\alpha \in S_X$ and $i \in \mathbb {Z}$, then $\alpha ^i$ shall denote the $i$-th power of $\alpha $ in the group $S_X$. Note that $\alpha ^i = \underbrace{\alpha \circ \alpha \circ \cdots \circ \alpha }_{i\text{ times}}$ if $i \ge 0$. Also, $\alpha ^0 = \operatorname {id}_X$. Also, $\alpha ^{-1}$ is the inverse of $\alpha $ in the group $S_X$, that is, the inverse of the map $\alpha $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.bk-invol
def.sf.bk-invol

\leanhelper  The \emph{Bender--Knuth involution} $\mathrm{BK}_k$ on fillings of $Y(\lambda /\mu )$. For a semistandard filling~ $f$, $\mathrm{BK}_k(f)$ swaps certain entries $k$ and $k{+}1$ while preserving semistandardness. For non-semistandard fillings, it returns the input unchanged.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.filling
def.sf.filling

\leanhelper  A \emph{filling} of a skew Young diagram $Y(\lambda /\mu )$ is a function $f : Y(\lambda /\mu ) \to [N]$. A filling is \emph{semistandard} if it satisfies the row-weak and column-strict conditions. The \emph{filling monomial} is $x_f = \prod _{c \in Y(\lambda /\mu )} x_{f(c)}$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.npar
def.sf.Npar

An $N$\emph{-partition} will mean a weakly decreasing $N$-tuple of nonnegative integers. In other words, an $N$-partition means an $N$-tuple $\left( \lambda _{1},\lambda _{2},\ldots ,\lambda _{N}\right) \in \mathbb {N}^{N}$ with $\lambda _{1}\geq \lambda _{2}\geq \cdots \geq \lambda _{N}$. 

The \emph{size} (or weight) of an $N$-partition $\lambda = (\lambda _1, \lambda _2, \ldots , \lambda _N)$ is defined to be $|\lambda | := \lambda _1 + \lambda _2 + \cdots + \lambda _N$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.npar-skewyoungdiagram
def.sf.Npar-skewYoungDiagram

\leanhelper  The \emph{skew Young diagram} $Y(\lambda /\mu )$ for $N$-partitions $\lambda , \mu $ is the set difference $Y(\lambda ) \setminus Y(\mu )$, consisting of cells $(i, j)$ with $\mu _i \leq j < \lambda _i$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.npar-youngdiagram
def.sf.Npar-youngDiagram

\leanhelper  The \emph{Young diagram} $Y(\lambda )$ of an $N$-partition $\lambda $ is the finite set of cells 

\[  Y(\lambda ) = \{ (i, j) : i \in [N],\;  0 \leq j < \lambda _i\} .  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.skew-ssyt
def.sf.skew-ssyt

Let $\lambda $ and $\mu $ be two $N$-partitions. 

A Young tableau $T$ of shape $\lambda /\mu $ is said to be \emph{semistandard} if its entries 

\begin{itemize} \item increase weakly along each row (from left to right); 

\item increase strictly down each column (from top to bottom). 

\end{itemize}

Formally speaking, this means that a Young tableau $T:Y\left( \lambda /\mu \right) \rightarrow \left[ N\right] $ is semistandard if and only if 

\begin{itemize} \item we have $T\left( i,j\right) \leq T\left( i,j+1\right) $ for any $\left( i,j\right) \in Y\left( \lambda /\mu \right) $ satisfying $\left( i,j+1\right) \in Y\left( \lambda /\mu \right) $; 

\item we have $T\left( i,j\right) <T\left( i+1,j\right) $ for any $\left( i,j\right) \in Y\left( \lambda /\mu \right) $ satisfying $\left( i+1,j\right) \in Y\left( \lambda /\mu \right) $. 

\end{itemize}

We let $\operatorname *{SSYT}\left( \lambda /\mu \right) $ denote the set of all semistandard Young tableaux of shape $\lambda /\mu $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.skew-tab
def.sf.skew-tab

Let $\lambda $ and $\mu $ be two $N$-partitions such that $\mu \subseteq \lambda $. A \emph{Young tableau} of shape $\lambda /\mu $ means a way of filling the boxes of $Y\left( \lambda /\mu \right) $ with elements of $\left[ N\right] $ (one element per box). Formally speaking, it is defined as a map $T:Y\left( \lambda /\mu \right) \rightarrow \left[ N\right] $. 

Young tableaux of shape $\lambda /\mu $ are often called \emph{skew Young tableaux}. 

If we don’t have $\mu \subseteq \lambda $, then we agree that there are no Young tableaux of shape $\lambda /\mu $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.ytab.skew-xt
def.sf.ytab.skew-xT

Let $\lambda $ and $\mu $ be two $N$-partitions. If $T$ is any Young tableau of shape $\lambda /\mu $, then we define the corresponding monomial

\[  x_{T}:=\prod _{c\text{ is a box of }Y\left( \lambda /\mu \right) }x_{T\left( c\right) }=\prod _{\left( i,j\right) \in Y\left( \lambda /\mu \right) }x_{T\left( i,j\right) }=\prod _{k=1}^{N}x_{k}^{\left( \text{\#  of times }k\text{ appears in }T\right) }.  \]

## VERDICT
{
  "verdict": "drift",
  "justification": "The formal theorem is restricted by the added binder `\u2200 f \u2208 ssytFillings lam mu`, whereas the informal statement gives the equation without a semistandard hypothesis: \u201c$x_{\\mathrm{BK}_k(f)} = (\\text{swap } x_k\\,x_{k+1}) \\cdot x_f$.\u201d This matters because the informal definition makes `BK_k` total and explicitly says: \u201cFor non-semistandard fillings, it returns the input unchanged,\u201d matching the dependency body\u2019s `else f`. For a non-semistandard filling whose numbers of `k` and `k+1` differ, the left side is therefore `x_f`, while renaming on the right swaps those exponents, so the unqualified equation need not hold. Thus the Lean theorem does not imply the stated claim for arbitrary fillings. To make it faithful, the blueprint statement would need to say that `f` is semistandard; alternatively, the formal binder could range over all fillings only if the non-semistandard branch of `benderKnuthInvol` were changed to have the required content-swapping effect. The `[NeZero N]` binder is not a substantive extra restriction here, since the subsequent `k : Fin N` and `hk : k.val + 1 < N` already force `N \u2265 2`."
}