## TARGET Nat.Partition.symToPartsMultiset_fold_max (theorem) — ELABORATED SIGNATURE
∀ {n : ℕ} (ℓ : ℕ) (s : Sym (Fin ℓ) n), Multiset.fold max 0 (Nat.Partition.symToPartsMultiset✝ ℓ s) = ℓ

Docstring: The largest part (fold max 0) of symToPartsMultiset is ℓ. 

## TARGET Nat.Partition.symToPartsMultiset_card (theorem) — ELABORATED SIGNATURE
∀ {n : ℕ} (ℓ : ℕ) (s : Sym (Fin ℓ) n), (Nat.Partition.symToPartsMultiset✝ ℓ s).card = n + 1

Docstring: The cardinality of symToPartsMultiset is n + 1. 

## TARGET Nat.Partition.symToPartsMultiset_erase (theorem) — ELABORATED SIGNATURE
∀ {n : ℕ} (ℓ : ℕ) (s : Sym (Fin ℓ) n),
  (Nat.Partition.symToPartsMultiset✝ ℓ s).erase ℓ = Multiset.map (fun x => ↑x + 1) ↑s

Docstring: Erasing ℓ from symToPartsMultiset recovers the mapped parts. 

## TARGET Nat.Partition.symToPartsMultiset_sum_range (theorem) — ELABORATED SIGNATURE
∀ (k ℓ : ℕ),
  k ≥ 1 → ℓ ≥ 1 → ∀ (s : Sym (Fin ℓ) (k - 1)), (Nat.Partition.symToPartsMultiset✝ ℓ s).sum ∈ Finset.Icc k (k * ℓ)

Docstring: The sum of symToPartsMultiset lies in [k, k*ℓ] for s : Sym (Fin ℓ) (k-1). 

## TARGET Nat.Partition.symToPartsMultiset_pos (theorem) — ELABORATED SIGNATURE
∀ {n : ℕ}, ∀ ℓ ≥ 1, ∀ (s : Sym (Fin ℓ) n), ∀ x ∈ Nat.Partition.symToPartsMultiset✝ ℓ s, 0 < x

Docstring: All parts in symToPartsMultiset are positive. 

## PROJECT DEPENDENCY _private.AlgebraicCombinatorics.Partitions.Basics.0.Nat.Partition.symToPartsMultiset (def)
{n : ℕ} → (ℓ : ℕ) → Sym (Fin ℓ) n → Multiset ℕ

Body:
fun {n} ℓ s => ℓ ::ₘ Multiset.map (fun x => ↑x + 1) ↑s

Docstring: The multiset ℓ ::ₘ (s.val.map (fun x => x.val + 1)) for a Sym (Fin ℓ) n. 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF Sym
Type u_1 → ℕ → Type (max 0 u_1)

Docstring: The nth symmetric power is n-tuples up to permutation.  We define it
as a subtype of `Multiset` since these are well developed in the
library.  We also give a definition `Sym.sym'` in terms of vectors, and we
show these are equivalent in `Sym.symEquivSym'`.


## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


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

## BASE-LIBRARY REF Multiset.fold
{α : Type u_1} → (op : α → α → α) → [hc : Std.Commutative op] → [ha : Std.Associative op] → α → Multiset α → α

Docstring: `fold op b s` folds a commutative associative operation `op` over
the multiset `s`. 

## BASE-LIBRARY REF Max.max
{α : Type u} → [self : Max α] → α → α → α

Docstring: Returns the greater of its two arguments. 

Conventions for notations in identifiers:

 * The recommended spelling of `max` in identifiers is `max`.

 * The recommended spelling of `⊔` in identifiers is `sup` (`⊔` is the preferred notation for `max` when the type is not linearly ordered.).

## BASE-LIBRARY REF Nat.instMax
Max ℕ

## BASE-LIBRARY REF Nat.instCommutativeMax
Std.Commutative max

## BASE-LIBRARY REF Nat.instAssociativeMax
Std.Associative max

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

## BASE-LIBRARY REF Multiset.card
{α : Type u_1} → Multiset α → ℕ

Docstring: The cardinality of a multiset is the sum of the multiplicities
of all its elements, or simply the length of the underlying list. 

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

## BASE-LIBRARY REF Multiset
Type u → Type u

Docstring: `Multiset α` is the quotient of `List α` by list permutation. The result
is a type of finite sets with duplicates allowed. 

## BASE-LIBRARY REF Multiset.erase
{α : Type u_1} → [DecidableEq α] → Multiset α → α → Multiset α

Docstring: `erase s a` is the multiset that subtracts 1 from the multiplicity of `a`. 

## BASE-LIBRARY REF instDecidableEqNat
DecidableEq ℕ

## BASE-LIBRARY REF Multiset.map
{α : Type u_1} → {β : Type v} → (α → β) → Multiset α → Multiset β

Docstring: `map f s` is the lift of the list `map` operation. The multiplicity
of `b` in `map f s` is the number of `a ∈ s` (counting multiplicity)
such that `f a = b`. 

## BASE-LIBRARY REF Fin.val
{n : ℕ} → Fin n → ℕ

Docstring: The number that is strictly less than `n`.

`Fin.val` is a coercion, so any `Fin n` can be used in a position where a `Nat` is expected.


## BASE-LIBRARY REF Subtype.val
{α : Sort u} → {p : α → Prop} → Subtype p → α

Docstring: The value in the underlying type that satisfies the predicate.


## BASE-LIBRARY REF GE.ge
{α : Type u} → [LE α] → α → α → Prop

Docstring: `a ≥ b` is an abbreviation for `b ≤ a`. 

Conventions for notations in identifiers:

 * The recommended spelling of `≥` in identifiers is `ge`.

 * The recommended spelling of `>=` in identifiers is `ge` (prefer `≥` over `>=`).

## BASE-LIBRARY REF instLENat
LE ℕ

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

## BASE-LIBRARY REF Finset.Icc
{α : Type u_1} → [inst : Preorder α] → [LocallyFiniteOrder α] → α → α → Finset α

Docstring: The finset $[a, b]$ of elements `x` such that `a ≤ x` and `x ≤ b`. Basically `Set.Icc a b` as a
finset. 

## BASE-LIBRARY REF Nat.instPreorder
Preorder ℕ

## BASE-LIBRARY REF Nat.instLocallyFiniteOrder
LocallyFiniteOrder ℕ

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

## BASE-LIBRARY REF Multiset.sum
{M : Type u_3} → [AddCommMonoid M] → Multiset M → M

Docstring: Sum of a multiset given a commutative additive monoid structure on `M`.
`sum {a, b, c} = a + b + c` 

## BASE-LIBRARY REF Nat.instAddCommMonoid
AddCommMonoid ℕ

## BASE-LIBRARY REF Multiset.instMembership
{α : Type u_1} → Membership α (Multiset α)

## BASE-LIBRARY REF LT.lt
{α : Type u} → [self : LT α] → α → α → Prop

Docstring: The less-than relation: `x < y` 

Conventions for notations in identifiers:

 * The recommended spelling of `<` in identifiers is `lt`.

## BASE-LIBRARY REF instLTNat
LT ℕ

## BASE-LIBRARY REF Multiset.cons
{α : Type u_1} → α → Multiset α → Multiset α

Docstring: `cons a s` is the multiset which contains `s` plus one more instance of `a`. 

## INFORMAL STATEMENT
lem.pars.symToPartsMultiset-props

\leanhelper  Properties of the multiset $(\ell , a_1+1, a_2+1, \ldots , a_{k-1}+1)$ for a $(k-1)$-element multisubset $(a_1, \ldots , a_{k-1})$ of $\{ 0,1,\ldots ,\ell -1\} $: 

\begin{enumerate} \item All elements are positive (since $\ell \ge 1$ and each $a_i+1\ge 1$). 

\item Cardinality is $k$ (one $\ell $ plus $k-1$ from the multisubset). 

\item Largest part is $\ell $. 

\item Removing $\ell $ recovers the remaining parts $(a_1+1, \ldots , a_{k-1}+1)$. 

\item The sum lies in $[k, k\ell ]$. 

\end{enumerate}

## VERDICT
{
  "verdict": "faithful",
  "justification": "The five declarations exactly formalize the five listed properties using the dependency body `\u2113 ::\u2098 Multiset.map (fun x => \u2191x + 1) \u2191s`. Positivity is stated under the blueprint\u2019s assumption `\u2200 \u2113 \u2265 1 ... 0 < x`. Cardinality is `(symToPartsMultiset\u271d \u2113 s).card = n + 1`, which becomes `k` when `n = k - 1` and `k \u2265 1`. The largest-part claim is `Multiset.fold max 0 ... = \u2113`. Erasure is exactly `(symToPartsMultiset\u271d \u2113 s).erase \u2113 = Multiset.map (fun x => \u2191x + 1) \u2191s`; this remains correct even when a mapped part also equals `\u2113`, since erasing one occurrence removes the distinguished consed occurrence up to multiset equality. Finally, for `s : Sym (Fin \u2113) (k - 1)`, the sum theorem assumes `k \u2265 1` and `\u2113 \u2265 1` and concludes membership in `Finset.Icc k (k * \u2113)`, exactly the interval `[k, k\u2113]`. The cardinality, maximum, and erasure declarations are stated more generally using arbitrary `n` (and the maximum/erasure claims do not require `\u2113 \u2265 1`), which strengthens rather than weakens the blueprint statement."
}