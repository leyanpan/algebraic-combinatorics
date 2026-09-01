## TARGET AlgebraicCombinatorics.benderKnuth_monomial (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_1} [inst : CommRing R] {N : ℕ} {lam mu : Fin N → ℕ} (k : Fin N) (hk : ↑k + 1 < N)
  (T : AlgebraicCombinatorics.Tableau lam mu) (hT : AlgebraicCombinatorics.IsSemistandard T),
  AlgebraicCombinatorics.monomialTableau (AlgebraicCombinatorics.benderKnuth k hk T hT) =
    (MvPolynomial.rename ⇑(Equiv.swap k ⟨↑k + 1, hk⟩)) (AlgebraicCombinatorics.monomialTableau T)

Docstring: The monomial x_{BK_k(T)} equals s_k · x_T, where s_k swaps x_k and x_{k+1}.
This follows from benderKnuth_content_swap. 

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

## PROJECT DEPENDENCY AlgebraicCombinatorics.monomialTableau (def)
{R : Type u_1} →
  [inst : CommRing R] → {N : ℕ} → {lam mu : Fin N → ℕ} → AlgebraicCombinatorics.Tableau lam mu → MvPolynomial (Fin N) R

Body:
fun {R} [CommRing R] {N} {lam mu} T => AlgebraicCombinatorics.xPow (AlgebraicCombinatorics.contentTableau T)

Docstring: The monomial x_T = ∏_i x_i^(# of i's in T) for a tableau T.
By definition, this equals x^(cont(T)). 

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

## PROJECT DEPENDENCY AlgebraicCombinatorics.xPow (def)
{R : Type u_1} → [inst : CommRing R] → {N : ℕ} → (Fin N → ℕ) → MvPolynomial (Fin N) R

Body:
fun {R} [CommRing R] {N} α => AlgebraicCombinatorics.SymmetricFunctions.monomialExp α

Docstring: x^α = ∏ᵢ xᵢ^(αᵢ) for an N-tuple α.

This is an alias for `AlgebraicCombinatorics.SymmetricFunctions.monomialExp` from MonomialSymmetric.lean.
The two definitions are identical: both equal `∏ i, X i ^ α i`.

See also: `xPow_eq_monomialExp` for the equivalence lemma. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.contentTableau (def)
{N : ℕ} → {lam mu : Fin N → ℕ} → AlgebraicCombinatorics.Tableau lam mu → Fin N → ℕ

Body:
fun {N} {lam mu} T i => Nat.card { c // T c = i }

Docstring: **Definition (def.sf.content)**: The content of a tableau T is the N-tuple counting
occurrences of each value.

For a tableau T of shape λ/μ, we define the content of T to be the N-tuple
(a₁, a₂, ..., a_N), where aᵢ = (# of i's in T) = (# of boxes c of T such that T(c) = i).

We denote this N-tuple by cont(T).

**Example**: If N=5, then cont([[1,1,2],[4]]) = (2,1,0,1,0).

**Key property** (eq.def.sf.content.xT=): x_T = x^(cont(T)) for any tableau T.
(Both sides equal ∏ᵢ xᵢ^(# of i's in T).) 

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

## PROJECT DEPENDENCY AlgebraicCombinatorics.SymmetricFunctions.monomialExp (def)
{R : Type u_1} → [inst : CommSemiring R] → {N : ℕ} → (Fin N → ℕ) → MvPolynomial (Fin N) R

Body:
fun {R} [CommSemiring R] {N} a => ∏ i, MvPolynomial.X i ^ a i

Docstring: The monomial x^a = x₁^{a₁} x₂^{a₂} ⋯ x_N^{a_N} for a tuple a ∈ ℕ^N.
(Definition def.sf.sort (a)) 

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

## BASE-LIBRARY REF CommRing
Type u → Type u

Docstring: A commutative ring is a ring with commutative multiplication. 

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

## BASE-LIBRARY REF CommRing.toCommSemiring
{α : Type u} → [s : CommRing α] → CommSemiring α

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

## BASE-LIBRARY REF Equiv.swap
{α : Sort u_1} → [DecidableEq α] → α → α → Equiv.Perm α

Docstring: `swap a b` is the permutation that swaps `a` and `b` and
leaves other values as is. 

## BASE-LIBRARY REF instDecidableEqFin
(n : ℕ) → DecidableEq (Fin n)

## BASE-LIBRARY REF Fin.mk
{n : ℕ} → (val : ℕ) → val < n → Fin n

Docstring: Creates a `Fin n` from `i : Nat` and a proof that `i < n`. 

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

## BASE-LIBRARY REF Membership.mem
{α : outParam (Type u)} → {γ : Type v} → [self : Membership α γ] → γ → α → Prop

Docstring: The membership relation `a ∈ s : Prop` where `a : α`, `s : γ`. 

Conventions for notations in identifiers:

 * The recommended spelling of `∈` in identifiers is `mem`.

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

## BASE-LIBRARY REF setOf
{α : Type u} → (α → Prop) → Set α

Docstring: Turn a predicate `p : α → Prop` into a set, also written as `{x | p x}` 

## BASE-LIBRARY REF instLENat
LE ℕ

## BASE-LIBRARY REF Nat.card
Type u_3 → ℕ

Docstring: `Nat.card α` is the cardinality of `α` as a natural number.
If `α` is infinite, `Nat.card α = 0`. 

## BASE-LIBRARY REF Not
Prop → Prop

Docstring: `Not p`, or `¬p`, is the negation of `p`. It is defined to be `p → False`,
so if your goal is `¬p` you can use `intro h` to turn the goal into
`h : p ⊢ False`, and if you have `hn : ¬p` and `h : p` then `hn h : False`
and `(hn h).elim` will prove anything.
For more information: [Propositional Logic](https://lean-lang.org/theorem_proving_in_lean4/propositions_and_proofs.html#propositional-logic)


Conventions for notations in identifiers:

 * The recommended spelling of `¬` in identifiers is `not`.

## BASE-LIBRARY REF GT.gt
{α : Type u} → [LT α] → α → α → Prop

Docstring: `a > b` is an abbreviation for `b < a`. 

Conventions for notations in identifiers:

 * The recommended spelling of `>` in identifiers is `gt`.

## BASE-LIBRARY REF CommSemiring
Type u → Type u

Docstring: A commutative semiring is a semiring with commutative multiplication. 

## BASE-LIBRARY REF Finset.prod
{ι : Type u_1} → {M : Type u_3} → [CommMonoid M] → Finset ι → (ι → M) → M

Docstring: `∏ x ∈ s, f x` is the product of `f x` as `x` ranges over the elements of the finite set `s`.

When the index type is a `Fintype`, the notation `∏ x, f x`, is a shorthand for
`∏ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF CommSemiring.toCommMonoid
{R : Type u} → [self : CommSemiring R] → CommMonoid R

## BASE-LIBRARY REF Finset.univ
{α : Type u_1} → [Fintype α] → Finset α

Docstring: `univ` is the universal finite set of type `Finset α` implied from
the assumption `Fintype α`. 

## BASE-LIBRARY REF Fin.fintype
(n : ℕ) → Fintype (Fin n)

## BASE-LIBRARY REF HPow.hPow
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HPow α β γ] → α → β → γ

Docstring: `a ^ b` computes `a` to the power of `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `^` in identifiers is `pow`.

## BASE-LIBRARY REF instHPow
{α : Type u_1} → {β : Type u_2} → [Pow α β] → HPow α β α

## BASE-LIBRARY REF Monoid.toNatPow
{M : Type u_2} → [Monoid M] → Pow M ℕ

## BASE-LIBRARY REF MonoidWithZero.toMonoid
{M₀ : Type u} → [self : MonoidWithZero M₀] → Monoid M₀

## BASE-LIBRARY REF Semiring.toMonoidWithZero
{α : Type u} → [self : Semiring α] → MonoidWithZero α

## BASE-LIBRARY REF MvPolynomial.X
{R : Type u} → {σ : Type u_1} → [inst : CommSemiring R] → σ → MvPolynomial σ R

Docstring: `X n` is the degree `1` monomial $X_n$. 

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


## INFORMAL STATEMENT
BK and the monomial of a tableau

\leanhelper  For the monomial associated to a tableau, $x^{\operatorname {cont}(\beta _k(T))} = \operatorname {rename}_{(k\; k{+}1)}(x^{\operatorname {cont}(T)})$. That is, the BK involution acts on monomials by the transposition $(k\; k{+}1)$.

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
  "verdict": "drift",
  "justification": "The target\u2019s LHS uses `monomialTableau (benderKnuth k hk T hT)`, but the dependency `benderKnuth` does not implement the blueprint\u2019s stated matching rule: \u201ceach free (k+1) matches with the nearest unmatched free k to its left.\u201d The difference enters through `isUnmatchedFreeK` and `isUnmatchedFreeKSucc`. For example, in a free row segment `k,k,k+1`, nearest-left matching pairs the `k+1` with the second `k`, leaving the first `k` unmatched. Instead, `isUnmatchedFreeK` uses `freeKCountUpTo ... > freeKSuccCount ...`, which marks the second/rightmost excess `k`. Dually, `isUnmatchedFreeKSucc` uses `freeKCount ... + freeKSuccCountUpTo ... \u2264 freeKSuccCount ...`, marking the leftmost excess `(k+1)`s, whereas nearest-left matching leaves the rightmost excess `(k+1)`s unmatched. Thus the referenced operation is not the informally defined \u03b2_k, even though this reversed choice can coincidentally produce the same swapped content. To match the blueprint, `isUnmatchedFreeK` should mark the leftmost excess k\u2019s (for instance, using `freeKCountUpTo ... + freeKSuccCount ... \u2264 freeKCount ...`), and `isUnmatchedFreeKSucc` should mark the rightmost excess successors (using `freeKSuccCountUpTo ... > freeKCount ...`). The target\u2019s arbitrary `{lam mu : Fin N \u2192 \u2115}` is otherwise a harmless generalization beyond N-partitions, and `(k : Fin N) (hk : \u2191k + 1 < N)` correctly encodes `k < N-1` in zero-based indexing."
}