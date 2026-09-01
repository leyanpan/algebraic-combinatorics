## TARGET AlgebraicCombinatorics.isUnmatchedFreeKSucc (def) — ELABORATED SIGNATURE
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

## TARGET AlgebraicCombinatorics.isForcedK (def) — ELABORATED SIGNATURE
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

## TARGET AlgebraicCombinatorics.isForcedKSucc (def) — ELABORATED SIGNATURE
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

## TARGET AlgebraicCombinatorics.isUnmatchedFreeK (def) — ELABORATED SIGNATURE
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

## PROJECT DEPENDENCY AlgebraicCombinatorics.Tableau (def)
{N : ℕ} → (Fin N → ℕ) → (Fin N → ℕ) → Type

Body:
fun {N} lam mu => { c // c ∈ AlgebraicCombinatorics.skewYoungDiagram lam mu } → Fin N

Docstring: A tableau of shape lam/mu is a function from cells to [N]. 

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

## PROJECT DEPENDENCY AlgebraicCombinatorics.freeKSuccCount (def)
{N : ℕ} → {lam mu : Fin N → ℕ} → AlgebraicCombinatorics.Tableau lam mu → Fin N → (k : Fin N) → ↑k + 1 < N → ℕ

Body:
fun {N} {lam mu} T i k hk =>
  Nat.card { c // (↑c).1 = i ∧ T c = ⟨↑k + 1, hk⟩ ∧ ¬AlgebraicCombinatorics.isForcedKSucc T k hk c }

Docstring: Count of free (k+1)'s in row i. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.freeKCountUpTo (def)
{N : ℕ} → {lam mu : Fin N → ℕ} → AlgebraicCombinatorics.Tableau lam mu → Fin N → (k : Fin N) → ↑k + 1 < N → ℕ → ℕ

Body:
fun {N} {lam mu} T i k hk j =>
  Nat.card { c // (↑c).1 = i ∧ (↑c).2 ≤ j ∧ T c = k ∧ ¬AlgebraicCombinatorics.isForcedK T k hk c }

Docstring: Count of free k's in row i with column at most j.
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

## BASE-LIBRARY REF Fin.mk
{n : ℕ} → (val : ℕ) → val < n → Fin n

Docstring: Creates a `Fin n` from `i : Nat` and a proof that `i < n`. 

## BASE-LIBRARY REF Not
Prop → Prop

Docstring: `Not p`, or `¬p`, is the negation of `p`. It is defined to be `p → False`,
so if your goal is `¬p` you can use `intro h` to turn the goal into
`h : p ⊢ False`, and if you have `hn : ¬p` and `h : p` then `hn h : False`
and `(hn h).elim` will prove anything.
For more information: [Propositional Logic](https://lean-lang.org/theorem_proving_in_lean4/propositions_and_proofs.html#propositional-logic)


Conventions for notations in identifiers:

 * The recommended spelling of `¬` in identifiers is `not`.

## BASE-LIBRARY REF LE.le
{α : Type u} → [self : LE α] → α → α → Prop

Docstring: The less-equal relation: `x ≤ y` 

Conventions for notations in identifiers:

 * The recommended spelling of `≤` in identifiers is `le`.

 * The recommended spelling of `<=` in identifiers is `le` (prefer `≤` over `<=`).

## BASE-LIBRARY REF instLENat
LE ℕ

## BASE-LIBRARY REF Prod.fst
{α : Type u} → {β : Type v} → α × β → α

Docstring: The first element of a pair. 

## BASE-LIBRARY REF Subtype.val
{α : Sort u} → {p : α → Prop} → Subtype p → α

Docstring: The value in the underlying type that satisfies the predicate.


## BASE-LIBRARY REF Prod.snd
{α : Type u} → {β : Type v} → α × β → β

Docstring: The second element of a pair. 

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


## BASE-LIBRARY REF GT.gt
{α : Type u} → [LT α] → α → α → Prop

Docstring: `a > b` is an abbreviation for `b < a`. 

Conventions for notations in identifiers:

 * The recommended spelling of `>` in identifiers is `gt`.

## BASE-LIBRARY REF setOf
{α : Type u} → (α → Prop) → Set α

Docstring: Turn a predicate `p : α → Prop` into a set, also written as `{x | p x}` 

## BASE-LIBRARY REF Nat.card
Type u_3 → ℕ

Docstring: `Nat.card α` is the cardinality of `α` as a natural number.
If `α` is infinite, `Nat.card α = 0`. 

## INFORMAL STATEMENT
Forced and free cells

\leanhelper  Let $T$ be a semistandard tableau and let $k < N-1$. A cell $c = (i,j)$ with $T(c) = k$ is \emph{forced} if there exists a cell $(i+1,j)$ directly below with $T(i+1,j) = k+1$. Similarly for $T(c) = k+1$ with a cell directly above having value~ $k$. Free cells are those that are not forced. 

Among the free cells, the \emph{parenthesis-matching algorithm} classifies each as \emph{matched} or \emph{unmatched}: reading free entries left-to-right in each row, each free $(k{+}1)$ matches with the nearest unmatched free $k$ to its left. Unmatched entries are those remaining after this process.

## VERDICT
{
  "verdict": "drift",
  "justification": "The forced-cell targets are faithful: `isForcedK` requires `T c = k` and a cell in the same column with row index one greater and value `k+1`; `isForcedKSucc` is the corresponding directly-above condition. The absence of a semistandardness binder in `T : Tableau lam mu` makes these definitions more general, not weaker on the blueprint\u2019s semistandard tableaux.\n\nThe unmatched predicates, however, reverse the parenthesis matching described by the blueprint: \u201ceach free `(k+1)` matches with the nearest unmatched free `k` to its left.\u201d In a semistandard row containing `a` free k\u2019s followed by `b` free `(k+1)`\u2019s, this matches the rightmost `min(a,b)` k\u2019s with the leftmost `min(a,b)` successors. Thus excess unmatched k\u2019s are the leftmost ones, while excess unmatched `(k+1)`\u2019s are the rightmost ones.\n\nInstead, `isUnmatchedFreeK` uses `freeKCountUpTo ... c.2 > freeKSuccCount ...`, selecting the rightmost excess k\u2019s. For example, with two free k\u2019s and one free `(k+1)`, the algorithm leaves the first k unmatched, but this inequality selects the second. Likewise, `isUnmatchedFreeKSucc` uses `freeKCount ... + freeKSuccCountUpTo ... c.2 \u2264 freeKSuccCount ...`, selecting the leftmost excess successors; with one free k and two free `(k+1)`\u2019s, the algorithm leaves the second successor unmatched, while the formal predicate selects the first.\n\nThe drift enters directly in the bodies of `AlgebraicCombinatorics.isUnmatchedFreeK` and `AlgebraicCombinatorics.isUnmatchedFreeKSucc`, not in the counting dependencies. For semistandard rows, the intended count tests would instead be respectively `freeKCountUpTo(c) + freeKSuccCount \u2264 freeKCount` and `freeKSuccCountUpTo(c) > freeKCount` (or the matching algorithm could be formalized directly)."
}