## TARGET Nat.Partition.lhs_eq_sum_parts (theorem) — ELABORATED SIGNATURE
∀ (I : Set ℕ) [inst : DecidablePred fun x => x ∈ I] (n : ℕ),
  n * (Nat.Partition.restricted n fun x => x ∈ I).card = ∑ p ∈ Nat.Partition.restricted n fun x => x ∈ I, p.parts.sum

Docstring: LHS of the identity equals sum of parts over all partitions. 

## BASE-LIBRARY REF Set
Type u → Type u

Docstring: A set is a collection of elements of some type `α`.

Although `Set` is defined as `α → Prop`, this is an implementation detail which should not be
relied on. Instead, `setOf` and membership of a set (`∈`) should be used to convert between sets
and predicates.


## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF DecidablePred
{α : Sort u} → (α → Prop) → Sort (max 1 u)

Docstring: A decidable predicate.

A predicate is decidable if the corresponding proposition is `Decidable` for each possible argument.


## BASE-LIBRARY REF Membership.mem
{α : outParam (Type u)} → {γ : Type v} → [self : Membership α γ] → γ → α → Prop

Docstring: The membership relation `a ∈ s : Prop` where `a : α`, `s : γ`. 

Conventions for notations in identifiers:

 * The recommended spelling of `∈` in identifiers is `mem`.

## BASE-LIBRARY REF Set.instMembership
{α : Type u} → Membership α (Set α)

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

## BASE-LIBRARY REF HMul.hMul
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HMul α β γ] → α → β → γ

Docstring: `a * b` computes the product of `a` and `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `*` in identifiers is `mul`.

## BASE-LIBRARY REF instHMul
{α : Type u_1} → [Mul α] → HMul α α α

## BASE-LIBRARY REF instMulNat
Mul ℕ

## BASE-LIBRARY REF Finset.card
{α : Type u_1} → Finset α → ℕ

Docstring: `s.card` is the number of elements of `s`, aka its cardinality.

The notation `#s` can be accessed in the `Finset` locale. 

## BASE-LIBRARY REF Nat.Partition
ℕ → Type

Docstring: A partition of `n` is a multiset of positive integers summing to `n`. 

## BASE-LIBRARY REF Nat.Partition.restricted
(n : ℕ) → (p : ℕ → Prop) → [DecidablePred p] → Finset n.Partition

Docstring: The finset of those partitions in which every part satisfies a certain condition. 

## BASE-LIBRARY REF Finset.sum
{ι : Type u_1} → {M : Type u_3} → [AddCommMonoid M] → Finset ι → (ι → M) → M

Docstring: `∑ x ∈ s, f x` is the sum of `f x` as `x` ranges over the elements
of the finite set `s`.

When the index type is a `Fintype`, the notation `∑ x, f x`, is a shorthand for
`∑ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF Nat.instAddCommMonoid
AddCommMonoid ℕ

## BASE-LIBRARY REF Multiset.sum
{M : Type u_3} → [AddCommMonoid M] → Multiset M → M

Docstring: Sum of a multiset given a commutative additive monoid structure on `M`.
`sum {a, b, c} = a + b + c` 

## BASE-LIBRARY REF Nat.Partition.parts
{n : ℕ} → n.Partition → Multiset ℕ

Docstring: positive integers summing to `n` 

## INFORMAL STATEMENT
lem.pars.lhs-eq-sum-parts

\leanhelper  For any set $I\subseteq \{ 1,2,3,\ldots \} $ and $n\in \mathbb {N}$: 

\[  n\cdot |\operatorname {restricted}(n, I)| = \sum _{p\in \operatorname {restricted}(n,I)} |\, p\, |.  \]

## VERDICT
{
  "verdict": "faithful",
  "justification": "The formal equality matches the blueprint term-for-term: `n * (Nat.Partition.restricted n fun x => x \u2208 I).card` formalizes `n\u00b7|restricted(n,I)|`, while `\u2211 p \u2208 Nat.Partition.restricted n fun x => x \u2208 I, p.parts.sum` sums the parts of each restricted partition, corresponding to `\u2211_{p\u2208restricted(n,I)} |p|`. By the library definitions, `restricted` consists exactly of partitions whose every part satisfies membership in `I`, and `p.parts.sum` is the sum (size) of the partition. The formal quantifier `\u2200 (I : Set \u2115)` is slightly more general than the blueprint\u2019s `I \u2286 {1,2,3,\u2026}`; this does not weaken the theorem, and membership of `0` is immaterial because partition parts are positive. The binder `[DecidablePred fun x => x \u2208 I]` is the decidability data required to construct the `Finset` returned by `Nat.Partition.restricted`, so it is an encoding requirement rather than a mathematically substantive added hypothesis."
}