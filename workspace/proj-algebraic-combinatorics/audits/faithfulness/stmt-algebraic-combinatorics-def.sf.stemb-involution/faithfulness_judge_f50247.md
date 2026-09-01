## TARGET AlgebraicCombinatorics.stembridgeInvolution (def) — ELABORATED SIGNATURE
{N : ℕ} →
  {lam mu : Fin N → ℕ} →
    (nu : Fin N → ℕ) →
      (T : AlgebraicCombinatorics.Tableau lam mu) →
        AlgebraicCombinatorics.IsSemistandard T →
          ¬AlgebraicCombinatorics.IsYamanouchi nu T → AlgebraicCombinatorics.Tableau lam mu

Body:
fun {N} {lam mu} nu T hT hnotYam =>
  have hviolator := ⋯;
  let j := (AlgebraicCombinatorics.violatorColumns nu T).max' hviolator;
  let α := nu + AlgebraicCombinatorics.contentColGeq T j;
  have hnotPart := ⋯;
  have hmisstep := ⋯;
  let k := (AlgebraicCombinatorics.misstepSet α).min' hmisstep;
  have hk_mem := ⋯;
  have hk := ⋯;
  AlgebraicCombinatorics.benderKnuthPrefixMatching k hk j T hT

Docstring: Stembridge's involution on non-Yamanouchi tableaux.
For T not ν-Yamanouchi:
1. Let j = findViolatorColumn ν T (largest column where ν + cont(col_{≥j}(T)) is not a partition)
2. Let k = findMisstepIndex ν T j (smallest index where the partition condition fails)
3. Apply BK_k to columns 1, ..., j-1 of T using benderKnuthPrefixMatching

This involution pairs non-Yamanouchi tableaux such that their alternant
contributions cancel.

**Key insight**: The violator column j and misstep index k are the same for T and T'
because benderKnuthPrefixMatching leaves columns ≥ j unchanged.
This ensures the involution is well-defined and pairs tableaux correctly.

**Implementation note**: We use the helper functions findViolatorColumn and findMisstepIndex
to extract j and k, then apply benderKnuthPrefixMatching. The proofs that these functions return
valid values (Some j, Some k) follow from the non-Yamanouchi assumption.

**Implementation**: Uses `violatorColumns_nonempty_of_not_yamanouchi` to find j,
`misstepSet_nonempty_of_not_partition` to find k, then applies `benderKnuthPrefixMatching k j T`. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.Tableau (def)
{N : ℕ} → (Fin N → ℕ) → (Fin N → ℕ) → Type

Body:
fun {N} lam mu => { c // c ∈ AlgebraicCombinatorics.skewYoungDiagram lam mu } → Fin N

Docstring: A tableau of shape lam/mu is a function from cells to [N]. 

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

## PROJECT DEPENDENCY AlgebraicCombinatorics.IsYamanouchi (def)
{N : ℕ} → {lam mu : Fin N → ℕ} → (Fin N → ℕ) → AlgebraicCombinatorics.Tableau lam mu → Prop

Body:
fun {N} {lam mu} nu T =>
  AlgebraicCombinatorics.IsSemistandard T ∧
    ∀ j > 0, AlgebraicCombinatorics.IsNPartition (nu + AlgebraicCombinatorics.contentColGeq T j)

Docstring: A semistandard tableau T of shape λ/μ is ν-Yamanouchi if for each positive integer j,
the N-tuple ν + cont(col_{≥j}(T)) is an N-partition (i.e., weakly decreasing).

**Definition (def.sf.yamanouchi)**:
Let λ, μ, ν be three N-partitions. A semistandard tableau T of shape λ/μ is said to be
ν-Yamanouchi if for each positive integer j, the N-tuple ν + cont(col_{≥j}T) ∈ ℕ^N is
an N-partition (i.e., weakly decreasing).

**Key properties:**
- The condition ensures that as we process the tableau column by column from right to left,
  starting with tally ν, the running tally always remains weakly decreasing.
- For j = 1, we get that ν + cont(T) is an N-partition (see `IsYamanouchi.isNPartition_add_content`).
- A 0-Yamanouchi tableau (also called a "ballot tableau") has content that is itself an N-partition.

**Voting interpretation (rmk.sf.yamanouchi.votes):**
Think of each entry i in T as a vote for candidate i. Starting with tally ν and counting votes
column by column from right to left, the tally must remain weakly decreasing at every step.
Since columns have distinct entries (strictly increasing), no candidate gains more than one
vote at a time. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.violatorColumns (def)
{N : ℕ} → {lam mu : Fin N → ℕ} → (Fin N → ℕ) → AlgebraicCombinatorics.Tableau lam mu → Finset ℕ

Body:
fun {N} {lam mu} nu T =>
  have maxCol := Finset.univ.sup lam;
  {j ∈ Finset.range (maxCol + 2) | j > 0 ∧ ¬AlgebraicCombinatorics.isPartitionAtColumn nu T j}

Docstring: The set of columns where ν + cont(col_{≥j}(T)) fails to be a partition.

Note: We use `maxCol + 2` in the range to ensure that `j = maxCol + 1` is included.
This is important because for `j > maxCol`, `contentColGeq T j = 0`, so we're checking
if `nu` itself is an N-partition. Without this, the lemma
`violatorColumns_nonempty_of_not_yamanouchi` would fail when `nu` is not an N-partition
but `nu + contentColGeq T j` is an N-partition for all `j ≤ maxCol`. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.violatorColumns_nonempty_of_not_yamanouchi (theorem)
∀ {N : ℕ} {lam mu nu : Fin N → ℕ} {T : AlgebraicCombinatorics.Tableau lam mu},
  AlgebraicCombinatorics.IsSemistandard T →
    ¬AlgebraicCombinatorics.IsYamanouchi nu T → (AlgebraicCombinatorics.violatorColumns nu T).Nonempty

Docstring: For a semistandard tableau T that is not ν-Yamanouchi, the violator columns set is nonempty. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.contentColGeq (def)
{N : ℕ} → {lam mu : Fin N → ℕ} → AlgebraicCombinatorics.Tableau lam mu → ℕ → Fin N → ℕ

Body:
fun {N} {lam mu} T j i => Nat.card { c // T ⟨↑c, ⋯⟩ = i }

Docstring: The content of a restricted tableau col_{≥j}(T).
Counts occurrences of each value in columns j and beyond. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.IsNPartition (def)
{N : ℕ} → (Fin N → ℕ) → Prop

Body:
fun {N} lam => IsNPartition lam

Docstring: An N-partition is a weakly decreasing N-tuple of natural numbers.
(Used throughout the source)

This is an alias for the canonical definition in `NPartition.lean`. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.misstepSet (def)
{N : ℕ} → (Fin N → ℕ) → Finset (Fin N)

Body:
fun {N} α => {k | AlgebraicCombinatorics.isMisstep α k}

Docstring: The set of misstep indices for a tuple α. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.misstepSet_nonempty_of_not_partition (theorem)
∀ {N : ℕ} {α : Fin N → ℕ}, ¬AlgebraicCombinatorics.IsNPartition α → (AlgebraicCombinatorics.misstepSet α).Nonempty

Docstring: The misstep set is nonempty when the tuple is not a partition. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.benderKnuthPrefixMatching (def)
{N : ℕ} →
  {lam mu : Fin N → ℕ} →
    (k : Fin N) →
      ↑k + 1 < N →
        ℕ →
          (T : AlgebraicCombinatorics.Tableau lam mu) →
            AlgebraicCombinatorics.IsSemistandard T → AlgebraicCombinatorics.Tableau lam mu

Body:
fun {N} {lam mu} k hk j T _hT c =>
  if AlgebraicCombinatorics.isUnmatchedFreeKPrefix T k hk j c then ⟨↑k + 1, hk⟩
  else if AlgebraicCombinatorics.isUnmatchedFreeKSuccPrefix T k hk j c then k else T c

Docstring: Apply the Bender-Knuth involution BK_k to columns < j of a tableau (matching-based version).

This definition uses `isUnmatchedFreeKPrefix` and `isUnmatchedFreeKSuccPrefix`
(which compute matching restricted to columns < j) instead of simple free conditions.
This is the correct definition that preserves row-weak ordering.

The matching-based conditions ensure that only unmatched free entries are swapped,
preserving the row-weak property. See `benderKnuthPrefixMatching_row_weak_stembridge` below. 

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

## PROJECT DEPENDENCY AlgebraicCombinatorics.isPartitionAtColumn (def)
{N : ℕ} → {lam mu : Fin N → ℕ} → (Fin N → ℕ) → AlgebraicCombinatorics.Tableau lam mu → ℕ → Prop

Body:
fun {N} {lam mu} nu T j => AlgebraicCombinatorics.IsNPartition (nu + AlgebraicCombinatorics.contentColGeq T j)

Docstring: Check if ν + cont(col_{≥j}(T)) is an N-partition. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.isPartitionAtColumn_decidable (def)
{N : ℕ} →
  {lam mu : Fin N → ℕ} →
    (nu : Fin N → ℕ) →
      (T : AlgebraicCombinatorics.Tableau lam mu) →
        (j : ℕ) → Decidable (AlgebraicCombinatorics.isPartitionAtColumn nu T j)

Body:
fun {N} {lam mu} nu T j => id (id inferInstance)

Docstring: Decidability of isPartitionAtColumn. 

## PROJECT DEPENDENCY IsNPartition (def)
{N : ℕ} → (Fin N → ℕ) → Prop

Body:
fun {N} lam => ∀ (i j : Fin N), i ≤ j → lam j ≤ lam i

Docstring: An N-partition predicate: an N-tuple is an N-partition if it is weakly decreasing.
This is equivalent to `Antitone` for functions `Fin N → ℕ`.
(Used throughout the source) 

## PROJECT DEPENDENCY AlgebraicCombinatorics.isMisstep (def)
{N : ℕ} → (Fin N → ℕ) → Fin N → Prop

Body:
fun {N} α k => ∃ (h : ↑k + 1 < N), α k < α ⟨↑k + 1, h⟩

Docstring: Check if index k is a misstep: α_k < α_{k+1}. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.isMisstep_decidable (def)
{N : ℕ} → (α : Fin N → ℕ) → (k : Fin N) → Decidable (AlgebraicCombinatorics.isMisstep α k)

Body:
fun {N} α k => id inferInstance

Docstring: Decidability of isMisstep. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.isUnmatchedFreeKPrefix (def)
{N : ℕ} →
  {lam mu : Fin N → ℕ} →
    AlgebraicCombinatorics.Tableau lam mu →
      (k : Fin N) → ↑k + 1 < N → ℕ → { c // c ∈ AlgebraicCombinatorics.skewYoungDiagram lam mu } → Prop

Body:
fun {N} {lam mu} T k hk j c =>
  (↑c).2 < j ∧
    T c = k ∧
      ¬AlgebraicCombinatorics.isForcedK T k hk c ∧
        AlgebraicCombinatorics.freeKCountUpToPrefix T (↑c).1 k hk j (↑c).2 >
          AlgebraicCombinatorics.freeKSuccCountPrefix T (↑c).1 k hk j

Docstring: A free k at position c is "unmatched" within the column prefix (columns < j).

This is the prefix-restricted version of `isUnmatchedFreeK`. The matching is computed
using only free entries in columns < j, not the entire row.

A free k is unmatched in the prefix iff at its position, the cumulative count of
free k's (in the prefix) exceeds the TOTAL count of free (k+1)'s (in the prefix).

**Usage**: Used by `benderKnuthPrefixMatching` to correctly preserve row-weak ordering. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.isUnmatchedFreeKSuccPrefix (def)
{N : ℕ} →
  {lam mu : Fin N → ℕ} →
    AlgebraicCombinatorics.Tableau lam mu →
      (k : Fin N) → ↑k + 1 < N → ℕ → { c // c ∈ AlgebraicCombinatorics.skewYoungDiagram lam mu } → Prop

Body:
fun {N} {lam mu} T k hk j c =>
  (↑c).2 < j ∧
    T c = ⟨↑k + 1, hk⟩ ∧
      ¬AlgebraicCombinatorics.isForcedKSucc T k hk c ∧
        AlgebraicCombinatorics.freeKCountPrefix T (↑c).1 k hk j +
            AlgebraicCombinatorics.freeKSuccCountUpToPrefix T (↑c).1 k hk j (↑c).2 ≤
          AlgebraicCombinatorics.freeKSuccCountPrefix T (↑c).1 k hk j

Docstring: A free (k+1) at position c is "unmatched" within the column prefix (columns < j).

This is the prefix-restricted version of `isUnmatchedFreeKSucc`. The matching is computed
using only free entries in columns < j, not the entire row.

A free (k+1) is unmatched in the prefix iff it's among the leftmost excess (k+1)'s,
i.e., the cumulative count of free (k+1)'s up to c plus the total free k count
is at most the total free (k+1) count (all counts restricted to the prefix).

**Usage**: Used by `benderKnuthPrefixMatching` to correctly preserve row-weak ordering. 

## PROJECT DEPENDENCY IsNPartition.instDecidable (def)
{N : ℕ} → (lam : Fin N → ℕ) → Decidable (IsNPartition lam)

Body:
fun {N} lam => inferInstanceAs (Decidable (∀ (i j : Fin N), i ≤ j → lam j ≤ lam i))

Docstring: `IsNPartition` is decidable since it's a finite conjunction of decidable inequalities. 

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

## PROJECT DEPENDENCY AlgebraicCombinatorics.freeKCountUpToPrefix (def)
{N : ℕ} → {lam mu : Fin N → ℕ} → AlgebraicCombinatorics.Tableau lam mu → Fin N → (k : Fin N) → ↑k + 1 < N → ℕ → ℕ → ℕ

Body:
fun {N} {lam mu} T i k hk j col =>
  Nat.card { c // (↑c).1 = i ∧ (↑c).2 ≤ col ∧ (↑c).2 < j ∧ T c = k ∧ ¬AlgebraicCombinatorics.isForcedK T k hk c }

Docstring: Count of free k's in row i with column ≤ col, restricted to columns < j.
Used for the parenthesis-matching algorithm in benderKnuthPrefixMatching. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.freeKSuccCountPrefix (def)
{N : ℕ} → {lam mu : Fin N → ℕ} → AlgebraicCombinatorics.Tableau lam mu → Fin N → (k : Fin N) → ↑k + 1 < N → ℕ → ℕ

Body:
fun {N} {lam mu} T i k hk j =>
  Nat.card { c // (↑c).1 = i ∧ (↑c).2 < j ∧ T c = ⟨↑k + 1, hk⟩ ∧ ¬AlgebraicCombinatorics.isForcedKSucc T k hk c }

Docstring: Count of free (k+1)'s in row i restricted to columns < j. 

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

## PROJECT DEPENDENCY AlgebraicCombinatorics.freeKCountPrefix (def)
{N : ℕ} → {lam mu : Fin N → ℕ} → AlgebraicCombinatorics.Tableau lam mu → Fin N → (k : Fin N) → ↑k + 1 < N → ℕ → ℕ

Body:
fun {N} {lam mu} T i k hk j => AlgebraicCombinatorics.freeKCountBefore T i k hk j

Docstring: Count of free k's in row i restricted to columns < j.
This is an alias for `freeKCountBefore` for use in the prefix-matching context. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.freeKSuccCountUpToPrefix (def)
{N : ℕ} → {lam mu : Fin N → ℕ} → AlgebraicCombinatorics.Tableau lam mu → Fin N → (k : Fin N) → ↑k + 1 < N → ℕ → ℕ → ℕ

Body:
fun {N} {lam mu} T i k hk j col =>
  Nat.card
    { c //
      (↑c).1 = i ∧ (↑c).2 ≤ col ∧ (↑c).2 < j ∧ T c = ⟨↑k + 1, hk⟩ ∧ ¬AlgebraicCombinatorics.isForcedKSucc T k hk c }

Docstring: Count of free (k+1)'s in row i with column ≤ col, restricted to columns < j.
Used for the parenthesis-matching algorithm in benderKnuthPrefixMatching. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.freeKCountBefore (def)
{N : ℕ} → {lam mu : Fin N → ℕ} → AlgebraicCombinatorics.Tableau lam mu → Fin N → (k : Fin N) → ↑k + 1 < N → ℕ → ℕ

Body:
fun {N} {lam mu} T i k hk j =>
  Nat.card { c // (↑c).1 = i ∧ (↑c).2 < j ∧ T c = k ∧ ¬AlgebraicCombinatorics.isForcedK T k hk c }

Docstring: Count of free k's in row i with column strictly less than j.
Used for the parenthesis-matching algorithm in Bender-Knuth. 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


## BASE-LIBRARY REF Not
Prop → Prop

Docstring: `Not p`, or `¬p`, is the negation of `p`. It is defined to be `p → False`,
so if your goal is `¬p` you can use `intro h` to turn the goal into
`h : p ⊢ False`, and if you have `hn : ¬p` and `h : p` then `hn h : False`
and `(hn h).elim` will prove anything.
For more information: [Propositional Logic](https://lean-lang.org/theorem_proving_in_lean4/propositions_and_proofs.html#propositional-logic)


Conventions for notations in identifiers:

 * The recommended spelling of `¬` in identifiers is `not`.

## BASE-LIBRARY REF Finset.Nonempty
{α : Type u_1} → Finset α → Prop

Docstring: The property `s.Nonempty` expresses the fact that the finset `s` is not empty. It should be used
in theorem assumptions instead of `∃ x, x ∈ s` or `s ≠ ∅` as it gives access to a nice API thanks
to the dot notation. 

## BASE-LIBRARY REF Finset.max'
{α : Type u_2} → [LinearOrder α] → (s : Finset α) → s.Nonempty → α

Docstring: Given a nonempty finset `s` in a linear order `α`, then `s.max' H` is its maximum, as an
element of `α`, where `H` is a proof of nonemptiness. Without this assumption, use instead `s.max`,
taking values in `WithBot α`. 

## BASE-LIBRARY REF Nat.instLinearOrder
LinearOrder ℕ

## BASE-LIBRARY REF HAdd.hAdd
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HAdd α β γ] → α → β → γ

Docstring: `a + b` computes the sum of `a` and `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `+` in identifiers is `add`.

## BASE-LIBRARY REF instHAdd
{α : Type u_1} → [Add α] → HAdd α α α

## BASE-LIBRARY REF Pi.instAdd
{ι : Type u_1} → {M : ι → Type u_5} → [(i : ι) → Add (M i)] → Add ((i : ι) → M i)

## BASE-LIBRARY REF instAddNat
Add ℕ

## BASE-LIBRARY REF Finset.min'
{α : Type u_2} → [LinearOrder α] → (s : Finset α) → s.Nonempty → α

Docstring: Given a nonempty finset `s` in a linear order `α`, then `s.min' H` is its minimum, as an
element of `α`, where `H` is a proof of nonemptiness. Without this assumption, use instead `s.min`,
taking values in `WithTop α`. 

## BASE-LIBRARY REF Fin.instLinearOrder
{n : ℕ} → LinearOrder (Fin n)

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

## BASE-LIBRARY REF LT.lt
{α : Type u} → [self : LT α] → α → α → Prop

Docstring: The less-than relation: `x < y` 

Conventions for notations in identifiers:

 * The recommended spelling of `<` in identifiers is `lt`.

## BASE-LIBRARY REF instLTNat
LT ℕ

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

## BASE-LIBRARY REF Set
Type u → Type u

Docstring: A set is a collection of elements of some type `α`.

Although `Set` is defined as `α → Prop`, this is an implementation detail which should not be
relied on. Instead, `setOf` and membership of a set (`∈`) should be used to convert between sets
and predicates.


## BASE-LIBRARY REF Set.instMembership
{α : Type u} → Membership α (Set α)

## BASE-LIBRARY REF And
Prop → Prop → Prop

Docstring: `And a b`, or `a ∧ b`, is the conjunction of propositions. It can be
constructed and destructed like a pair: if `ha : a` and `hb : b` then
`⟨ha, hb⟩ : a ∧ b`, and if `h : a ∧ b` then `h.left : a` and `h.right : b`.


Conventions for notations in identifiers:

 * The recommended spelling of `∧` in identifiers is `and`.

 * The recommended spelling of `/\` in identifiers is `and` (prefer `∧` over `/\`).

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

## BASE-LIBRARY REF GT.gt
{α : Type u} → [LT α] → α → α → Prop

Docstring: `a > b` is an abbreviation for `b < a`. 

Conventions for notations in identifiers:

 * The recommended spelling of `>` in identifiers is `gt`.

## BASE-LIBRARY REF Finset.sup
{α : Type u_2} → {β : Type u_3} → [inst : SemilatticeSup α] → [OrderBot α] → Finset β → (β → α) → α

Docstring: Supremum of a finite set: `sup {a, b, c} f = f a ⊔ f b ⊔ f c` 

## BASE-LIBRARY REF Lattice.toSemilatticeSup
{α : Type u} → [self : Lattice α] → SemilatticeSup α

## BASE-LIBRARY REF Nat.instLattice
Lattice ℕ

Docstring: This instance is necessary, otherwise the lattice operations would be derived via
`ConditionallyCompleteLinearOrderBot` and marked as noncomputable. 

## BASE-LIBRARY REF Nat.instOrderBot
OrderBot ℕ

## BASE-LIBRARY REF Finset.univ
{α : Type u_1} → [Fintype α] → Finset α

Docstring: `univ` is the universal finite set of type `Finset α` implied from
the assumption `Fintype α`. 

## BASE-LIBRARY REF Fin.fintype
(n : ℕ) → Fintype (Fin n)

## BASE-LIBRARY REF Finset.filter
{α : Type u_1} → (p : α → Prop) → [DecidablePred p] → Finset α → Finset α

Docstring: `Finset.filter p s` is the set of elements of `s` that satisfy `p`.

For example, one can use `s.filter (· ∈ t)` to get the intersection of `s` with `t : Set α`
as a `Finset α` (when a `DecidablePred (· ∈ t)` instance is available). 

## BASE-LIBRARY REF instDecidableAnd
{p q : Prop} → [dp : Decidable p] → [dq : Decidable q] → Decidable (p ∧ q)

## BASE-LIBRARY REF Nat.decLt
(n m : ℕ) → Decidable (n < m)

Docstring: A decision procedure for strict inequality of natural numbers, usually accessed via the
`DecidableLT Nat` instance.

Examples:
 * `(if 3 < 4 then "yes" else "no") = "yes"`
 * `(if 4 < 4 then "yes" else "no") = "no"`
 * `(if 6 < 4 then "yes" else "no") = "no"`
 * `show 5 < 12 by decide`


## BASE-LIBRARY REF instDecidableNot
{p : Prop} → [dp : Decidable p] → Decidable ¬p

## BASE-LIBRARY REF Finset.range
ℕ → Finset ℕ

Docstring: `range n` is the set of natural numbers less than `n`. 

## BASE-LIBRARY REF Nat.card
Type u_3 → ℕ

Docstring: `Nat.card α` is the cardinality of `α` as a natural number.
If `α` is infinite, `Nat.card α = 0`. 

## BASE-LIBRARY REF GE.ge
{α : Type u} → [LE α] → α → α → Prop

Docstring: `a ≥ b` is an abbreviation for `b ≤ a`. 

Conventions for notations in identifiers:

 * The recommended spelling of `≥` in identifiers is `ge`.

 * The recommended spelling of `>=` in identifiers is `ge` (prefer `≥` over `>=`).

## BASE-LIBRARY REF instLENat
LE ℕ

## BASE-LIBRARY REF Subtype.mk
{α : Sort u} → {p : α → Prop} → (val : α) → p val → Subtype p

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

## BASE-LIBRARY REF Fin.mk
{n : ℕ} → (val : ℕ) → val < n → Fin n

Docstring: Creates a `Fin n` from `i : Nat` and a proof that `i < n`. 

## BASE-LIBRARY REF setOf
{α : Type u} → (α → Prop) → Set α

Docstring: Turn a predicate `p : α → Prop` into a set, also written as `{x | p x}` 

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


## BASE-LIBRARY REF exists_prop_decidable
{p : Prop} → (P : p → Prop) → [Decidable p] → [(h : p) → Decidable (P h)] → Decidable (∃ (h : p), P h)

## BASE-LIBRARY REF inferInstanceAs
(α : Sort u) → [i : α] → α

Docstring: `inferInstanceAs α` synthesizes a value of any target type by typeclass
inference. This is just like `inferInstance` except that `α` is given
explicitly instead of being inferred from the target type. It is especially
useful when the target type is some `α'` which is definitionally equal to `α`,
but the instance we are looking for is only registered for `α` (because
typeclass search does not unfold most definitions, but definitional equality
does.) Example:
```
#check inferInstanceAs (Inhabited Nat) -- Inhabited Nat
```


## BASE-LIBRARY REF Nat.decidableForallFin
{n : ℕ} → (P : Fin n → Prop) → [DecidablePred P] → Decidable (∀ (i : Fin n), P i)

## BASE-LIBRARY REF forall_prop_decidable
{p : Prop} → (P : p → Prop) → [Decidable p] → [(h : p) → Decidable (P h)] → Decidable (∀ (h : p), P h)

## BASE-LIBRARY REF Fin.decLe
{n : ℕ} → (a b : Fin n) → Decidable (a ≤ b)

## BASE-LIBRARY REF Nat.decLe
(n m : ℕ) → Decidable (n ≤ m)

Docstring: A decision procedure for non-strict inequality of natural numbers, usually accessed via the
`DecidableLE Nat` instance.

Examples:
 * `(if 3 ≤ 4 then "yes" else "no") = "yes"`
 * `(if 6 ≤ 4 then "yes" else "no") = "no"`
 * `show 12 ≤ 12 by decide`
 * `show 5 ≤ 12 by decide`


## INFORMAL STATEMENT
Stembridge’s involution

\leanhelper  For a semistandard tableau $T$ that is not $\nu $-Yamanouchi, define $T^* = \operatorname {stemb}_\nu (T)$ as follows: 

\begin{enumerate} \item Let $j$ be the \emph{largest} violator column (where $\nu + \operatorname {cont}(\operatorname {col}_{\geq j} T)$ is not a partition). 

\item Let $k$ be the \emph{smallest} misstep index of $\nu + \operatorname {cont}(\operatorname {col}_{\geq j} T)$. 

\item Apply the prefix-restricted BK involution: $T^* = \beta _k^{<j}(T)$. 

\end{enumerate}

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.bk-forced-free
Forced and free cells

\leanhelper  Let $T$ be a semistandard tableau and let $k < N-1$. A cell $c = (i,j)$ with $T(c) = k$ is \emph{forced} if there exists a cell $(i+1,j)$ directly below with $T(i+1,j) = k+1$. Similarly for $T(c) = k+1$ with a cell directly above having value~ $k$. Free cells are those that are not forced. 

Among the free cells, the \emph{parenthesis-matching algorithm} classifies each as \emph{matched} or \emph{unmatched}: reading free entries left-to-right in each row, each free $(k{+}1)$ matches with the nearest unmatched free $k$ to its left. Unmatched entries are those remaining after this process.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.bk-involution
Bender–Knuth involution βk

\leanhelper  Let $T$ be a semistandard tableau of shape $\lambda /\mu $ and let $k < N-1$. The \emph{Bender--Knuth involution} $\beta _k(T)$ is obtained from $T$ by swapping only the \emph{unmatched} free $k$’s and unmatched free $(k{+}1)$’s: 

\[  \beta _k(T)(c) = \begin{cases}  k+1 &  \text{if } c \text{ is an unmatched free } k, \\ k &  \text{if } c \text{ is an unmatched free } k{+}1, \\ T(c) &  \text{otherwise.} \end{cases}  \]

 Forced cells and matched free cells are left unchanged.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.bk-prefix
Prefix-restricted Bender–Knuth

\leanhelper  The \emph{prefix-restricted BK involution} $\beta _k^{<j}$ applies the parenthesis-matching swap of $k$ and $k{+}1$ only to cells in columns $< j$. Cells in columns $\geq j$ are left unchanged: 

\[  \beta _k^{<j}(T)(c) = \begin{cases}  k+1 &  \text{if the column of } c \text{ is } < j \text{ and } c \text{ is unmatched free } k \text{ in prefix}, \\ k &  \text{if the column of } c \text{ is } < j \text{ and } c \text{ is unmatched free } k{+}1 \text{ in prefix}, \\ T(c) &  \text{otherwise.} \end{cases}  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.col-tab
def.sf.col-tab

Let $\lambda $ and $\mu $ be two $N$-partitions. Let $T$ be a tableau of shape $\lambda /\mu $. Let $j$ be a positive integer. Then, $\operatorname {col}_{\geq j}T$ means the restriction of $T$ to columns $j,j+1,j+2,\ldots $ (that is, the result of removing the first $j-1$ columns from $T$). Formally speaking, this means the restriction of the map $T$ to the set $\left\{  \left( u,v\right) \in Y\left( \lambda /\mu \right) \  \mid \  v\geq j\right\}  $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.content
def.sf.content

Let $\lambda $ and $\mu $ be two $N$-partitions. Let $T$ be a tableau of shape $\lambda /\mu $. We define the \emph{content} of $T$ to be the $N$-tuple $\left( a_{1},a_{2},\ldots ,a_{N}\right) $, where

\[  a_{i}:=\left( \text{\#  of }i\text{'s in }T\right) =\left( \text{\#  of boxes }c\text{ of }T\text{ such that }T\left( c\right) =i\right) .  \]

 We denote this $N$-tuple by $\operatorname *{cont}T$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.npar
def.sf.Npar

An $N$\emph{-partition} will mean a weakly decreasing $N$-tuple of nonnegative integers. In other words, an $N$-partition means an $N$-tuple $\left( \lambda _{1},\lambda _{2},\ldots ,\lambda _{N}\right) \in \mathbb {N}^{N}$ with $\lambda _{1}\geq \lambda _{2}\geq \cdots \geq \lambda _{N}$. 

The \emph{size} (or weight) of an $N$-partition $\lambda = (\lambda _1, \lambda _2, \ldots , \lambda _N)$ is defined to be $|\lambda | := \lambda _1 + \lambda _2 + \cdots + \lambda _N$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.npar-order
def.sf.Npar-order

\leanhelper  We define a partial order on $N$-partitions by componentwise comparison: $\mu \leq \nu $ iff $\mu _i \leq \nu _i$ for all $i \in [N]$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.npar-youngdiagram
def.sf.Npar-youngDiagram

\leanhelper  The \emph{Young diagram} $Y(\lambda )$ of an $N$-partition $\lambda $ is the finite set of cells 

\[  Y(\lambda ) = \{ (i, j) : i \in [N],\;  0 \leq j < \lambda _i\} .  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.par-subset
def.sf.par-subset

Let $\lambda $ and $\mu $ be two $N$-partitions. 

We say that $\mu \subseteq \lambda $ if and only if $Y\left( \mu \right) \subseteq Y\left( \lambda \right) $. Equivalently, $\mu \subseteq \lambda $ if and only if

\[  \text{each }i\in \left[ N\right] \text{ satisfies }\mu _{i}\leq \lambda _{i}.  \]

 Thus we have defined a partial order $\subseteq $ on the set of all $N$-partitions.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.skew-diag
def.sf.skew-diag

Let $\lambda $ and $\mu $ be two $N$-partitions such that $\mu \subseteq \lambda $. Then, we define the \emph{skew Young diagram} $Y\left( \lambda /\mu \right) $ to be the set difference

\begin{align*}  Y\left( \lambda \right) \setminus Y\left( \mu \right) &  =\left\{  \left( i,j\right) \  \mid \  i\in \left[ N\right] \text{ and }j\in \left[ \lambda _{i}\right] \setminus \left[ \mu _{i}\right] \right\}  \\ &  =\left\{  \left( i,j\right) \  \mid \  i\in \left[ N\right] \text{ and }j\in \mathbb {Z}\text{ and }\mu _{i}<j\leq \lambda _{i}\right\}  . \end{align*}

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.ssyt
def.sf.ssyt

Let $\lambda $ be an $N$-partition. 

A Young tableau $T$ of shape $\lambda $ is said to be \emph{semistandard} if its entries 

\begin{itemize} \item increase weakly along each row (from left to right); 

\item increase strictly down each column (from top to bottom). 

\end{itemize}

Formally speaking, this means that a Young tableau $T:Y\left( \lambda \right) \rightarrow \left[ N\right] $ is semistandard if and only if 

\begin{itemize} \item we have $T\left( i,j\right) \leq T\left( i,j+1\right) $ for any $\left( i,j\right) \in Y\left( \lambda \right) $ satisfying $\left( i,j+1\right) \in Y\left( \lambda \right) $; 

\item we have $T\left( i,j\right) <T\left( i+1,j\right) $ for any $\left( i,j\right) \in Y\left( \lambda \right) $ satisfying $\left( i+1,j\right) \in Y\left( \lambda \right) $. 

\end{itemize}

We let $\operatorname *{SSYT}\left( \lambda \right) $ denote the set of all semistandard Young tableaux of shape $\lambda $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.stemb-violator-misstep
Violator columns and misstep indices

\leanhelper  Let $T$ be a semistandard tableau and $\nu $ an $N$-tuple. A positive integer $j$ is a \emph{violator column} if $\nu + \operatorname {cont}(\operatorname {col}_{\geq j} T)$ is not an $N$-partition. An index $k$ is a \emph{misstep} for an $N$-tuple $\alpha $ if $k + 1 < N$ and $\alpha _k < \alpha _{k+1}$ (i.e., the partition condition fails at~ $k$).

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.yamanouchi
def.sf.yamanouchi

Let $\lambda ,\mu ,\nu $ be three $N$-partitions. A semistandard tableau $T$ of shape $\lambda /\mu $ is said to be $\nu $-\emph{Yamanouchi} (this is an adjective) if for each positive integer $j$, the $N$-tuple $\nu +\operatorname *{cont}\left( \operatorname {col}_{\geq j}T\right) \in \mathbb {N}^{N}$ is an $N$-partition (i.e., weakly decreasing).

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.ydiag
def.sf.ydiag

Let $\lambda $ be an $N$-partition. 

The \emph{Young diagram} of $\lambda $ is defined as the set

\[  \left\{  \left( i,j\right) \  \mid \  i\in \left[ N\right] \text{ and }j\in \left[ \lambda _{i}\right] \right\}  \subseteq \left\{  1,2,3,\ldots \right\}  ^{2}.  \]

 We visually represent each element $\left( i,j\right) $ of this Young diagram as a box in row $i$ and column $j$. 

We denote the Young diagram of $\lambda $ by $Y\left( \lambda \right) $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.ytab
def.sf.ytab

Let $\lambda $ be an $N$-partition. 

A \emph{Young tableau} of shape $\lambda $ means a way of filling the boxes of $Y\left( \lambda \right) $ with elements of $\left[ N\right] $ (one element per box). Formally speaking, it is defined as a map $T:Y\left( \lambda \right) \rightarrow \left[ N\right] $.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The target takes exactly the relevant inputs and hypotheses: `(T : Tableau lam mu) \u2192 IsSemistandard T \u2192 \u00ac IsYamanouchi nu T`, matching \u201cFor a semistandard tableau T that is not \u03bd-Yamanouchi.\u201d Its body chooses `j := (violatorColumns nu T).max' ...`, then `\u03b1 := nu + contentColGeq T j`, then `k := (misstepSet \u03b1).min' ...`, and returns `benderKnuthPrefixMatching k hk j T hT`. These are respectively the blueprint\u2019s \u201clargest violator column,\u201d \u201csmallest misstep index,\u201d and `\u03b2_k^{<j}(T)`. The dependency bodies implement the required tests: `j > 0 \u2227 \u00ac isPartitionAtColumn nu T j`, `isMisstep \u03b1 k := \u2203 h : \u2191k + 1 < N, \u03b1 k < \u03b1 \u27e8\u2191k + 1,h\u27e9`, and the BK operation changes only unmatched free entries with column `< j`. Although the elaborated signature allows arbitrary `lam`, `mu`, and `nu` rather than requiring the blueprint\u2019s N-partition and containment conditions, this is a strictly more general domain, not an added restriction. On the intended domain, `nu` is a partition, so columns beyond the maximum tableau column cannot be violators; hence the finite `violatorColumns` maximum agrees with the blueprint\u2019s largest positive violator."
}