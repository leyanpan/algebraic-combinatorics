## TARGET AlgebraicCombinatorics.InclusionExclusion.weighted_pie' (theorem) — ELABORATED SIGNATURE
∀ {ι : Type u_1} {U : Type u_2} {G : Type u_3} [DecidableEq ι] [inst : Fintype U] [inst_1 : DecidableEq U]
  [inst_2 : AddCommGroup G] (s : Finset ι) (A : ι → Finset U) (w : U → G),
  ∑ u ∈ s.inf fun i => (A i)ᶜ, w u = ∑ I ∈ s.powerset, (-1) ^ I.card • ∑ u ∈ I.inf A, w u

Docstring: **Theorem `thm.pie.2`** (alternative formulation with explicit index set):
The weighted PIE with an explicit finite index set `s` of "rules".

This version allows indexing by a subset `s` of a larger type `ι`, rather than requiring
a finite type for the index. 

## BASE-LIBRARY REF DecidableEq
Sort u → Sort (max 1 u)

Docstring: Propositional equality is `Decidable` for all elements of a type.

In other words, an instance of `DecidableEq α` is a means of deciding the proposition `a = b` is
for all `a b : α`.


## BASE-LIBRARY REF Fintype
Type u_4 → Type u_4

Docstring: `Fintype α` means that `α` is finite, i.e. there are only
finitely many distinct elements of type `α`. The evidence of this
is a finset `elems` (a list up to permutation without duplicates),
together with a proof that everything of type `α` is in the list. 

## BASE-LIBRARY REF AddCommGroup
Type u → Type u

Docstring: An additive commutative group is an additive group with commutative `(+)`. 

## BASE-LIBRARY REF Finset
Type u_4 → Type u_4

Docstring: `Finset α` is the type of finite sets of elements of `α`. It is implemented
as a multiset (a list up to permutation) which has no duplicate elements. 

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

## BASE-LIBRARY REF AddCommGroup.toAddCommMonoid
{G : Type u} → [self : AddCommGroup G] → AddCommMonoid G

## BASE-LIBRARY REF Finset.inf
{α : Type u_2} → {β : Type u_3} → [inst : SemilatticeInf α] → [OrderTop α] → Finset β → (β → α) → α

Docstring: Infimum of a finite set: `inf {a, b, c} f = f a ⊓ f b ⊓ f c` 

## BASE-LIBRARY REF Lattice.toSemilatticeInf
{α : Type u} → [self : Lattice α] → SemilatticeInf α

## BASE-LIBRARY REF Finset.instLattice
{α : Type u_1} → [DecidableEq α] → Lattice (Finset α)

## BASE-LIBRARY REF CoheytingAlgebra.toOrderTop
{α : Type u_4} → [self : CoheytingAlgebra α] → OrderTop α

## BASE-LIBRARY REF BiheytingAlgebra.toCoheytingAlgebra
{α : Type u_2} → [BiheytingAlgebra α] → CoheytingAlgebra α

## BASE-LIBRARY REF BooleanAlgebra.toBiheytingAlgebra
{α : Type u} → [BooleanAlgebra α] → BiheytingAlgebra α

## BASE-LIBRARY REF Finset.booleanAlgebra
{α : Type u_1} → [Fintype α] → [DecidableEq α] → BooleanAlgebra (Finset α)

## BASE-LIBRARY REF Compl.compl
{α : Type u_1} → [self : Compl α] → α → α

Docstring: Set / lattice complement 

Conventions for notations in identifiers:

 * The recommended spelling of `ᶜ` in identifiers is `compl`.

## BASE-LIBRARY REF BooleanAlgebra.toCompl
{α : Type u} → [self : BooleanAlgebra α] → Compl α

## BASE-LIBRARY REF Finset.powerset
{α : Type u_1} → Finset α → Finset (Finset α)

Docstring: When `s` is a finset, `s.powerset` is the finset of all subsets of `s` (seen as finsets). 

## BASE-LIBRARY REF HSMul.hSMul
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HSMul α β γ] → α → β → γ

Docstring: `a • b` computes the product of `a` and `b`.
The meaning of this notation is type-dependent, but it is intended to be used for left actions. 

Conventions for notations in identifiers:

 * The recommended spelling of `•` in identifiers is `smul`.

## BASE-LIBRARY REF Int
Type

Docstring: The integers.

This type is special-cased by the compiler and overridden with an efficient implementation. The
runtime has a special representation for `Int` that stores “small” signed numbers directly, while
larger numbers use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)). A “small number” is an integer that can be encoded with one fewer bits
than the platform's pointer size (i.e. 63 bits on 64-bit architectures and 31 bits on 32-bit
architectures).


## BASE-LIBRARY REF instHSMul
{α : Type u_1} → {β : Type u_2} → [SMul α β] → HSMul α β β

## BASE-LIBRARY REF SubNegMonoid.toZSMul
{M : Type u_2} → [SubNegMonoid M] → SMul ℤ M

## BASE-LIBRARY REF AddGroup.toSubNegMonoid
{A : Type u} → [self : AddGroup A] → SubNegMonoid A

## BASE-LIBRARY REF AddCommGroup.toAddGroup
{G : Type u} → [self : AddCommGroup G] → AddGroup G

## BASE-LIBRARY REF HPow.hPow
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HPow α β γ] → α → β → γ

Docstring: `a ^ b` computes `a` to the power of `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `^` in identifiers is `pow`.

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF instHPow
{α : Type u_1} → {β : Type u_2} → [Pow α β] → HPow α β α

## BASE-LIBRARY REF Monoid.toNatPow
{M : Type u_2} → [Monoid M] → Pow M ℕ

## BASE-LIBRARY REF Int.instMonoid
Monoid ℤ

## BASE-LIBRARY REF Neg.neg
{α : Type u} → [self : Neg α] → α → α

Docstring: `-a` computes the negative or opposite of `a`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `-` in identifiers is `neg` (when used as a unary operator).

## BASE-LIBRARY REF Int.instNegInt
Neg ℤ

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNat
{n : ℕ} → OfNat ℤ n

## BASE-LIBRARY REF Finset.card
{α : Type u_1} → Finset α → ℕ

Docstring: `s.card` is the number of elements of `s`, aka its cardinality.

The notation `#s` can be accessed in the `Finset` locale. 

## INFORMAL STATEMENT
Weighted PIE, explicit index set

\leanhelper  Let $U$ be a finite set, $s$ a finite index set, $A_i$ subsets of $U$ for $i \in s$, $G$ an additive abelian group, and $w\colon U \to G$ a weight function. Then, 

\[  \sum _{\substack {u \in U \\ u \notin A_i\  \forall \,  i \in s}} w(u) = \sum _{I \subseteq s} (-1)^{|I|} \sum _{\substack {u \in U \\ u \in A_i\  \forall \,  i \in I}} w(u).  \]

## VERDICT
{
  "verdict": "faithful",
  "justification": "The formal equality exactly expresses the weighted inclusion\u2013exclusion formula. The left side, `\u2211 u \u2208 s.inf fun i => (A i)\u1d9c, w u`, sums over the finite universe `U` those `u` lying in every complement `(A i)\u1d9c` for `i \u2208 s`, matching \u201c`u \u2209 A_i \u2200 i \u2208 s`.\u201d The right side, `\u2211 I \u2208 s.powerset, (-1) ^ I.card \u2022 \u2211 u \u2208 I.inf A, w u`, ranges over all `I \u2286 s`, uses the sign `(-1)^{|I|}`, and sums over the intersection of the `A_i` for `i \u2208 I`. For empty `s` or `I`, `Finset.inf` uses the top element of `Finset U`, namely the whole finite universe, as required by vacuous universal quantification. The binders `[Fintype U] [DecidableEq U]` encode that `U` is finite and permit finite-set complements; `[AddCommGroup G]` is exactly the additive abelian-group assumption. `[DecidableEq \u03b9]` is representation infrastructure for `s : Finset \u03b9`. Although `A : \u03b9 \u2192 Finset U` is defined on a larger ambient type rather than only on `s`, the formula accesses it only at indices in `s`, so this is a harmless encoding and, as the docstring notes, allows a more general ambient index type."
}