## TARGET AlgebraicCombinatorics.MathlibComposition.compositionToFinset (def) — ELABORATED SIGNATURE
(n : ℕ) → Composition n ≃ Finset (Fin (n - 1))

Body:
fun n => (compositionEquiv n).trans (compositionAsSetEquiv n)

Docstring: Equivalence between Mathlib's `Composition n` and subsets of `Fin (n-1)`. 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF Equiv
Sort u_1 → Sort u_2 → Sort (max (max 1 u_1) u_2)

Docstring: `α ≃ β` is the type of functions from `α → β` with a two-sided inverse. 

## BASE-LIBRARY REF Composition
ℕ → Type

Docstring: A composition of `n` is a list of positive integers summing to `n`. 

## BASE-LIBRARY REF Finset
Type u_4 → Type u_4

Docstring: `Finset α` is the type of finite sets of elements of `α`. It is implemented
as a multiset (a list up to permutation) which has no duplicate elements. 

## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


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

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

## BASE-LIBRARY REF Equiv.trans
{α : Sort u} → {β : Sort v} → {γ : Sort w} → α ≃ β → β ≃ γ → α ≃ γ

Docstring: Composition of equivalences `e₁ : α ≃ β` and `e₂ : β ≃ γ`. 

## BASE-LIBRARY REF CompositionAsSet
ℕ → Type

Docstring: Combinatorial viewpoint on a composition of `n`, by seeing it as non-empty blocks of
consecutive integers in `{0, ..., n-1}`. We register every block by its left end-point, yielding
a finset containing `0`. As this does not make sense for `n = 0`, we add `n` to this finset, and
get a finset of `{0, ..., n}` containing `0` and `n`. This is the data in the structure
`CompositionAsSet n`. 

## BASE-LIBRARY REF compositionEquiv
(n : ℕ) → Composition n ≃ CompositionAsSet n

Docstring: Equivalence between `Composition n` and `CompositionAsSet n`. 

## BASE-LIBRARY REF compositionAsSetEquiv
(n : ℕ) → CompositionAsSet n ≃ Finset (Fin (n - 1))

Docstring: Bijection between compositions of `n` and subsets of `{0, ..., n-2}`, defined by
considering the restriction of the subset to `{1, ..., n-1}` and shifting to the left by one. 

## INFORMAL STATEMENT
lem.fps.comps.compositionToFinset

\leanhelper  There is an equivalence between Mathlib’s compositions of $n$ and subsets of $\{ 1, 2, \ldots , n-1\} $, obtained by composing two Mathlib equivalences.

## VERDICT
{
  "verdict": "drift",
  "justification": "The blueprint requires an equivalence with subsets of \u201c$\\{1,2,\\ldots,n-1\\}$,\u201d whereas the elaborated codomain is `Finset (Fin (n - 1))`. By the supplied `Fin` docstring, `Fin (n - 1)` consists of naturals below `n - 1`, namely indices `{0, \u2026, n-2}`, not `{1, \u2026, n-1}`. The difference enters through `compositionAsSetEquiv (n : \u2115) : CompositionAsSet n \u2243 Finset (Fin (n - 1))`; its docstring explicitly says that it shifts the restriction to `{1, \u2026, n-1}` left by one, producing subsets of `{0, \u2026, n-2}`. To make the declaration faithful, that dependency\u2014and consequently the target codomain\u2014should instead use a type representing the literal interval `{1, \u2026, n-1}` and omit/undo the left shift. Alternatively, the informal statement would need to specify the shifted encoding by subsets of `{0, \u2026, n-2}`."
}