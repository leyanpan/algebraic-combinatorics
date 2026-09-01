## TARGET AlgebraicCombinatorics.InclusionExclusion.card_inf_S_avoid (theorem) — ELABORATED SIGNATURE
∀ (m n : ℕ) (t : Finset (Fin n)),
  (t.inf (AlgebraicCombinatorics.InclusionExclusion.S_avoid✝ m n)).card = (n - t.card) ^ m

Docstring: The cardinality of the intersection of `S_avoid` sets. 

## PROJECT DEPENDENCY _private.AlgebraicCombinatorics.SignedCounting.InclusionExclusion1.0.AlgebraicCombinatorics.InclusionExclusion.S_avoid (def)
(m n : ℕ) → Fin n → Finset (Fin m → Fin n)

Body:
fun m n i => {f | i ∉ Set.range f}

Docstring: For each `i : Fin n`, the set of functions `f : Fin m → Fin n` such that `i ∉ range f`. 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF Finset
Type u_4 → Type u_4

Docstring: `Finset α` is the type of finite sets of elements of `α`. It is implemented
as a multiset (a list up to permutation) which has no duplicate elements. 

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

## BASE-LIBRARY REF Finset.card
{α : Type u_1} → Finset α → ℕ

Docstring: `s.card` is the number of elements of `s`, aka its cardinality.

The notation `#s` can be accessed in the `Finset` locale. 

## BASE-LIBRARY REF Finset.inf
{α : Type u_2} → {β : Type u_3} → [inst : SemilatticeInf α] → [OrderTop α] → Finset β → (β → α) → α

Docstring: Infimum of a finite set: `inf {a, b, c} f = f a ⊓ f b ⊓ f c` 

## BASE-LIBRARY REF Lattice.toSemilatticeInf
{α : Type u} → [self : Lattice α] → SemilatticeInf α

## BASE-LIBRARY REF Finset.instLattice
{α : Type u_1} → [DecidableEq α] → Lattice (Finset α)

## BASE-LIBRARY REF Fintype.decidablePiFintype
{α : Type u_5} → {β : α → Type u_4} → [(a : α) → DecidableEq (β a)] → [Fintype α] → DecidableEq ((a : α) → β a)

## BASE-LIBRARY REF instDecidableEqFin
(n : ℕ) → DecidableEq (Fin n)

## BASE-LIBRARY REF Fin.fintype
(n : ℕ) → Fintype (Fin n)

## BASE-LIBRARY REF CoheytingAlgebra.toOrderTop
{α : Type u_4} → [self : CoheytingAlgebra α] → OrderTop α

## BASE-LIBRARY REF BiheytingAlgebra.toCoheytingAlgebra
{α : Type u_2} → [BiheytingAlgebra α] → CoheytingAlgebra α

## BASE-LIBRARY REF BooleanAlgebra.toBiheytingAlgebra
{α : Type u} → [BooleanAlgebra α] → BiheytingAlgebra α

## BASE-LIBRARY REF Finset.booleanAlgebra
{α : Type u_1} → [Fintype α] → [DecidableEq α] → BooleanAlgebra (Finset α)

## BASE-LIBRARY REF Pi.instFintype
{α : Type u_3} →
  {β : α → Type u_4} → [DecidableEq α] → [Fintype α] → [(a : α) → Fintype (β a)] → Fintype ((a : α) → β a)

Docstring: A dependent product of fintypes, indexed by a fintype, is a fintype. 

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

## BASE-LIBRARY REF Finset.filter
{α : Type u_1} → (p : α → Prop) → [DecidablePred p] → Finset α → Finset α

Docstring: `Finset.filter p s` is the set of elements of `s` that satisfy `p`.

For example, one can use `s.filter (· ∈ t)` to get the intersection of `s` with `t : Set α`
as a `Finset α` (when a `DecidablePred (· ∈ t)` instance is available). 

## BASE-LIBRARY REF Not
Prop → Prop

Docstring: `Not p`, or `¬p`, is the negation of `p`. It is defined to be `p → False`,
so if your goal is `¬p` you can use `intro h` to turn the goal into
`h : p ⊢ False`, and if you have `hn : ¬p` and `h : p` then `hn h : False`
and `(hn h).elim` will prove anything.
For more information: [Propositional Logic](https://lean-lang.org/theorem_proving_in_lean4/propositions_and_proofs.html#propositional-logic)


Conventions for notations in identifiers:

 * The recommended spelling of `¬` in identifiers is `not`.

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

## BASE-LIBRARY REF Set.range
{α : Type u} → {ι : Sort u_1} → (ι → α) → Set α

Docstring: Range of a function.

This function is more flexible than `f '' univ`, as the image requires that the domain is in Type
and not an arbitrary Sort. 

## BASE-LIBRARY REF instDecidableNot
{p : Prop} → [dp : Decidable p] → Decidable ¬p

## BASE-LIBRARY REF Fintype.decidableMemRangeFintype
{α : Type u_1} → {β : Type u_2} → [Fintype α] → [DecidableEq β] → (f : α → β) → DecidablePred fun x => x ∈ Set.range f

## BASE-LIBRARY REF Finset.univ
{α : Type u_1} → [Fintype α] → Finset α

Docstring: `univ` is the universal finite set of type `Finset α` implied from
the assumption `Fintype α`. 

## INFORMAL STATEMENT
Cardinality of intersection of avoid-sets

\leanhelper  For $t \subseteq [n]$, the cardinality of the intersection $\bigcap _{i \in t} S_{\mathrm{avoid}}(i)$ is $(n - |t|)^m$, where $S_{\mathrm{avoid}}(i) = \{ f\colon [m] \to [n] \mid i \notin \operatorname {im} f\} $.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The formal binders `\u2200 (m n : \u2115) (t : Finset (Fin n))` represent arbitrary finite subsets `t \u2286 [n]`. The dependency defines `S_avoid m n i` as `{f | i \u2209 Set.range f}`, exactly matching `S_avoid(i) = { f : [m] \u2192 [n] | i \u2209 im f }`. By `Finset.inf`, `(t.inf (S_avoid m n))` is the finite intersection over `i \u2208 t` (with the empty intersection interpreted as the universal finite set), and `.card = (n - t.card) ^ m` is precisely the claimed cardinality `(n - |t|)^m`. No additional hypotheses or narrowed quantifiers are present."
}