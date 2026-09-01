## TARGET AlgebraicCombinatorics.SymmetricPolynomials.sum_count_eq_card (theorem) — ELABORATED SIGNATURE
∀ {N : ℕ} [inst : DecidableEq (Fin N)] (m : ℕ) (s : Sym (Fin N) m), ∑ i, Multiset.count i ↑s = m

Docstring: Key lemma: For any multiset s of size m, the sum of counts over all elements equals m.
This is used in the proof of the Newton-Girard formula for h and p.
Label: thm.sf.NG 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF DecidableEq
Sort u → Sort (max 1 u)

Docstring: Propositional equality is `Decidable` for all elements of a type.

In other words, an instance of `DecidableEq α` is a means of deciding the proposition `a = b` is
for all `a b : α`.


## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


## BASE-LIBRARY REF Sym
Type u_1 → ℕ → Type (max 0 u_1)

Docstring: The nth symmetric power is n-tuples up to permutation.  We define it
as a subtype of `Multiset` since these are well developed in the
library.  We also give a definition `Sym.sym'` in terms of vectors, and we
show these are equivalent in `Sym.symEquivSym'`.


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

## BASE-LIBRARY REF Finset.sum
{ι : Type u_1} → {M : Type u_3} → [AddCommMonoid M] → Finset ι → (ι → M) → M

Docstring: `∑ x ∈ s, f x` is the sum of `f x` as `x` ranges over the elements
of the finite set `s`.

When the index type is a `Fintype`, the notation `∑ x, f x`, is a shorthand for
`∑ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF Nat.instAddCommMonoid
AddCommMonoid ℕ

## BASE-LIBRARY REF Finset.univ
{α : Type u_1} → [Fintype α] → Finset α

Docstring: `univ` is the universal finite set of type `Finset α` implied from
the assumption `Fintype α`. 

## BASE-LIBRARY REF Fin.fintype
(n : ℕ) → Fintype (Fin n)

## BASE-LIBRARY REF Multiset.count
{α : Type u_1} → [DecidableEq α] → α → Multiset α → ℕ

Docstring: `count a s` is the multiplicity of `a` in `s`. 

## BASE-LIBRARY REF Subtype.val
{α : Sort u} → {p : α → Prop} → Subtype p → α

Docstring: The value in the underlying type that satisfies the predicate.


## BASE-LIBRARY REF Multiset
Type u → Type u

Docstring: `Multiset α` is the quotient of `List α` by list permutation. The result
is a type of finite sets with duplicates allowed. 

## BASE-LIBRARY REF Multiset.card
{α : Type u_1} → Multiset α → ℕ

Docstring: The cardinality of a multiset is the sum of the multiplicities
of all its elements, or simply the length of the underlying list. 

## INFORMAL STATEMENT
lem.sf.sum-count-eq-card

\leanhelper  For any multiset $s$ of elements from $[N]$ of size $m$, the sum of counts $\sum _{i=1}^N \text{count}(i, s)$ equals $m$.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The binder `s : Sym (Fin N) m` represents a multiset of degree/size `m` over the canonical `N`-element type `Fin N`, matching \u201ca multiset s of elements from [N] of size m.\u201d The conclusion `\u2211 i, Multiset.count i \u2191s = m` sums the multiplicity of every `i : Fin N` via `Finset.univ`, exactly matching `\u2211_{i=1}^N count(i,s) = m` up to the harmless indexing convention for the canonical N-element set. The instance `[DecidableEq (Fin N)]` is only the computational structure required by `Multiset.count`, not a mathematically contentful added hypothesis."
}