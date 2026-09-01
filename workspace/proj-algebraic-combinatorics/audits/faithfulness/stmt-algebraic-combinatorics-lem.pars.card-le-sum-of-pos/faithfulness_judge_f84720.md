## TARGET Nat.Partition.card_le_sum_of_pos (theorem) — ELABORATED SIGNATURE
∀ (s : Multiset ℕ), (∀ i ∈ s, 0 < i) → s.card ≤ s.sum

Docstring: The cardinality of a multiset of positive naturals is at most its sum. 

## BASE-LIBRARY REF Multiset
Type u → Type u

Docstring: `Multiset α` is the quotient of `List α` by list permutation. The result
is a type of finite sets with duplicates allowed. 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF Membership.mem
{α : outParam (Type u)} → {γ : Type v} → [self : Membership α γ] → γ → α → Prop

Docstring: The membership relation `a ∈ s : Prop` where `a : α`, `s : γ`. 

Conventions for notations in identifiers:

 * The recommended spelling of `∈` in identifiers is `mem`.

## BASE-LIBRARY REF Multiset.instMembership
{α : Type u_1} → Membership α (Multiset α)

## BASE-LIBRARY REF LT.lt
{α : Type u} → [self : LT α] → α → α → Prop

Docstring: The less-than relation: `x < y` 

Conventions for notations in identifiers:

 * The recommended spelling of `<` in identifiers is `lt`.

## BASE-LIBRARY REF instLTNat
LT ℕ

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

## BASE-LIBRARY REF LE.le
{α : Type u} → [self : LE α] → α → α → Prop

Docstring: The less-equal relation: `x ≤ y` 

Conventions for notations in identifiers:

 * The recommended spelling of `≤` in identifiers is `le`.

 * The recommended spelling of `<=` in identifiers is `le` (prefer `≤` over `<=`).

## BASE-LIBRARY REF instLENat
LE ℕ

## BASE-LIBRARY REF Multiset.card
{α : Type u_1} → Multiset α → ℕ

Docstring: The cardinality of a multiset is the sum of the multiplicities
of all its elements, or simply the length of the underlying list. 

## BASE-LIBRARY REF Multiset.sum
{M : Type u_3} → [AddCommMonoid M] → Multiset M → M

Docstring: Sum of a multiset given a commutative additive monoid structure on `M`.
`sum {a, b, c} = a + b + c` 

## BASE-LIBRARY REF Nat.instAddCommMonoid
AddCommMonoid ℕ

## INFORMAL STATEMENT
lem.pars.card-le-sum-of-pos

\leanhelper  The cardinality of a multiset of positive naturals is at most its sum.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The formal theorem states `\u2200 (s : Multiset \u2115), (\u2200 i \u2208 s, 0 < i) \u2192 s.card \u2264 s.sum`, exactly matching \u201cThe cardinality of a multiset of positive naturals is at most its sum.\u201d Here `s : Multiset \u2115` supplies the multiset of naturals, `\u2200 i \u2208 s, 0 < i` expresses that all its elements are positive, `s.card` is its cardinality, and `s.sum` is its sum. There are no added substantive hypotheses or narrowed quantifiers."
}