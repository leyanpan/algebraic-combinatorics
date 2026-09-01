## TARGET AlgebraicCombinatorics.QBinomialRec.card_linearIndependent_tuples (theorem) — ELABORATED SIGNATURE
∀ {F : Type u_1} [inst : Field F] [inst_1 : Fintype F] {V : Type u_2} [inst_2 : AddCommGroup V]
  [inst_3 : _root_.Module F V] [Module.Finite F V] (n k : ℕ),
  Module.finrank F V = n →
    Nat.card { v // LinearIndependent F v } = ∏ i ∈ Finset.range k, (Fintype.card F ^ n - Fintype.card F ^ i)

Docstring: Lemma lem.pars.qbinom.lin-ind-count: The number of linearly independent k-tuples
of vectors in an n-dimensional F-vector space V is
∏_{i=0}^{k-1} (|F|ⁿ - |F|ⁱ).

The proof proceeds by induction on k:
- Base case (k = 0): There is exactly one 0-tuple, which is vacuously linearly independent.
- Inductive step: A linearly independent (k+1)-tuple (v₁, ..., v_{k+1}) corresponds to
  a linearly independent k-tuple (v₂, ..., v_{k+1}) together with a choice of v₁ outside
  the span of {v₂, ..., v_{k+1}}. The span has |F|^k elements, so there are |F|^n - |F|^k
  choices for v₁.

This uses `card_linearIndependent` from Mathlib which proves this via the equivalence
`equiv_linearIndependent`. 

## BASE-LIBRARY REF Field
Type u → Type u

Docstring: A `Field` is a `CommRing` with multiplicative inverses for nonzero elements.

An instance of `Field K` includes maps `ratCast : ℚ → K` and `qsmul : ℚ → K → K`.
Those two fields are needed to implement the `DivisionRing K → Algebra ℚ K` instance since we need
to control the specific definitions for some special cases of `K` (in particular `K = ℚ` itself).
See also note [forgetful inheritance].

If the field has positive characteristic `p`, our division by zero convention forces
`ratCast (1 / p) = 1 / 0 = 0`. 

## BASE-LIBRARY REF Fintype
Type u_4 → Type u_4

Docstring: `Fintype α` means that `α` is finite, i.e. there are only
finitely many distinct elements of type `α`. The evidence of this
is a finset `elems` (a list up to permutation without duplicates),
together with a proof that everything of type `α` is in the list. 

## BASE-LIBRARY REF AddCommGroup
Type u → Type u

Docstring: An additive commutative group is an additive group with commutative `(+)`. 

## BASE-LIBRARY REF Module
(R : Type u) → (M : Type v) → [Semiring R] → [AddCommMonoid M] → Type (max u v)

Docstring: A module is a generalization of vector spaces to a scalar semiring.
It consists of a scalar semiring `R` and an additive monoid of "vectors" `M`,
connected by a "scalar multiplication" operation `r • x : M`
(where `r : R` and `x : M`) with some natural associativity and
distributivity axioms similar to those on a ring. 

## BASE-LIBRARY REF DivisionSemiring.toSemiring
{K : Type u_2} → [self : DivisionSemiring K] → Semiring K

## BASE-LIBRARY REF Semifield.toDivisionSemiring
{K : Type u_2} → [self : Semifield K] → DivisionSemiring K

## BASE-LIBRARY REF Field.toSemifield
{K : Type u_1} → [Field K] → Semifield K

## BASE-LIBRARY REF AddCommGroup.toAddCommMonoid
{G : Type u} → [self : AddCommGroup G] → AddCommMonoid G

## BASE-LIBRARY REF Module.Finite
(R : Type u_1) → (M : Type u_4) → [inst : Semiring R] → [inst_1 : AddCommMonoid M] → [_root_.Module R M] → Prop

Docstring: A module over a semiring is `Module.Finite` if it is finitely generated as a module. 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


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

## BASE-LIBRARY REF Module.finrank
(R : Type u_1) → (M : Type u_2) → [inst : Semiring R] → [inst_1 : AddCommMonoid M] → [_root_.Module R M] → ℕ

Docstring: The rank of a module as a natural number.

For a finite-dimensional vector space `V` over a field `k`, `Module.finrank k V` is equal to
the dimension of `V` over `k`.

For a general module `M` over a ring `R`, `Module.finrank R M` is defined to be the supremum of the
cardinalities of the `R`-linearly independent subsets of `M`, if this supremum is finite. It is
defined by convention to be `0` if this supremum is infinite. See `Module.rank` for a
cardinal-valued version where infinite rank modules have rank an infinite cardinal.

Note that if `R` is not a field then there can exist modules `M` with `¬(Module.Finite R M)` but
`finrank R M ≠ 0`. For example `ℚ` has `finrank` equal to `1` over `ℤ`, because the nonempty
`ℤ`-linearly independent subsets of `ℚ` are precisely the nonzero singletons. 

## BASE-LIBRARY REF Nat.card
Type u_3 → ℕ

Docstring: `Nat.card α` is the cardinality of `α` as a natural number.
If `α` is infinite, `Nat.card α = 0`. 

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

## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


## BASE-LIBRARY REF LinearIndependent
{ι : Type u'} →
  (R : Type u_2) →
    {M : Type u_4} → (ι → M) → [inst : Semiring R] → [inst_1 : AddCommMonoid M] → [_root_.Module R M] → Prop

Docstring: `LinearIndependent R v` states the family of vectors `v` is linearly independent over `R`. 

## BASE-LIBRARY REF Finset.prod
{ι : Type u_1} → {M : Type u_3} → [CommMonoid M] → Finset ι → (ι → M) → M

Docstring: `∏ x ∈ s, f x` is the product of `f x` as `x` ranges over the elements of the finite set `s`.

When the index type is a `Fintype`, the notation `∏ x, f x`, is a shorthand for
`∏ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF Nat.instCommMonoid
CommMonoid ℕ

## BASE-LIBRARY REF Finset.range
ℕ → Finset ℕ

Docstring: `range n` is the set of natural numbers less than `n`. 

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

## BASE-LIBRARY REF Nat.instMonoid
Monoid ℕ

## BASE-LIBRARY REF Fintype.card
(α : Type u_4) → [Fintype α] → ℕ

Docstring: `card α` is the number of elements in `α`, defined when `α` is a fintype. 

## INFORMAL STATEMENT
lem.pars.qbinom.lin-ind-count

Let $F$ be a finite field. Let $n,k\in \mathbb {N}$. Let $V$ be an $n$-dimensional $F$-vector space. Then, 

\begin{align*} &  \left( \text{\#  of linearly independent }k\text{-tuples of vectors in }V\right) \\ &  =\left( \left\vert F\right\vert ^{n}-\left\vert F\right\vert ^{0}\right) \left( \left\vert F\right\vert ^{n}-\left\vert F\right\vert ^{1}\right) \cdots \left( \left\vert F\right\vert ^{n}-\left\vert F\right\vert ^{k-1}\right) =\prod _{i=0}^{k-1}\left( \left\vert F\right\vert ^{n}-\left\vert F\right\vert ^{i}\right) . \end{align*}

## VERDICT
{
  "verdict": "faithful",
  "justification": "The blueprint assumes \u201cLet F be a finite field\u201d and \u201cV be an n-dimensional F-vector space.\u201d These are represented by `[Field F] [Fintype F]`, `[Module F V] [Module.Finite F V]`, and the hypothesis `Module.finrank F V = n`. Here `Module.Finite` is part of encoding finite-dimensionality, not an additional mathematical restriction. The conclusion `Nat.card { v // LinearIndependent F v } = \u220f i \u2208 Finset.range k, (Fintype.card F ^ n - Fintype.card F ^ i)` counts the linearly independent families indexed by `Fin k`, i.e. k-tuples, and `Finset.range k` is exactly the index range `0 \u2264 i < k`. Thus its right-hand side is precisely `\u220f_{i=0}^{k-1} (|F|^n - |F|^i)`. Natural-number subtraction is appropriate for cardinalities; when `k > n`, the factor at `i = n` is zero. The formal and informal statements therefore agree."
}