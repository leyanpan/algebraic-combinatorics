## TARGET Equiv.Perm.setR (def) — ELABORATED SIGNATURE
{n : ℕ} → Equiv.Perm (Fin n) → Fin n → Fin n → Finset (Fin n)

Body:
fun {n} σ i j => {k | i < k ∧ k < j ∧ σ i < σ k ∧ σ k < σ j}

Docstring: The set R from Proposition prop.perm.lisitij:
R = {k ∈ {i+1, ..., j-1} | σ(i) < σ(k) < σ(j)}
This counts elements between i and j whose images are strictly between σ(i) and σ(j). 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF Equiv.Perm
Sort u_1 → Sort (max 1 u_1)

Docstring: `Perm α` is the type of bijections from `α` to itself. 

## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


## BASE-LIBRARY REF Finset
Type u_4 → Type u_4

Docstring: `Finset α` is the type of finite sets of elements of `α`. It is implemented
as a multiset (a list up to permutation) which has no duplicate elements. 

## BASE-LIBRARY REF Finset.filter
{α : Type u_1} → (p : α → Prop) → [DecidablePred p] → Finset α → Finset α

Docstring: `Finset.filter p s` is the set of elements of `s` that satisfy `p`.

For example, one can use `s.filter (· ∈ t)` to get the intersection of `s` with `t : Set α`
as a `Finset α` (when a `DecidablePred (· ∈ t)` instance is available). 

## BASE-LIBRARY REF And
Prop → Prop → Prop

Docstring: `And a b`, or `a ∧ b`, is the conjunction of propositions. It can be
constructed and destructed like a pair: if `ha : a` and `hb : b` then
`⟨ha, hb⟩ : a ∧ b`, and if `h : a ∧ b` then `h.left : a` and `h.right : b`.


Conventions for notations in identifiers:

 * The recommended spelling of `∧` in identifiers is `and`.

 * The recommended spelling of `/\` in identifiers is `and` (prefer `∧` over `/\`).

## BASE-LIBRARY REF LT.lt
{α : Type u} → [self : LT α] → α → α → Prop

Docstring: The less-than relation: `x < y` 

Conventions for notations in identifiers:

 * The recommended spelling of `<` in identifiers is `lt`.

## BASE-LIBRARY REF instLTFin
{n : ℕ} → LT (Fin n)

## BASE-LIBRARY REF DFunLike.coe
{F : Sort u_1} → {α : outParam (Sort u_2)} → {β : outParam (α → Sort u_3)} → [self : DFunLike F α β] → F → (a : α) → β a

Docstring: The coercion from `F` to a function. 

## BASE-LIBRARY REF EquivLike.toFunLike
{E : Sort u_1} → {α : Sort u_3} → {β : Sort u_4} → [EquivLike E α β] → FunLike E α β

## BASE-LIBRARY REF Equiv.instEquivLike
{α : Sort u} → {β : Sort v} → EquivLike (α ≃ β) α β

## BASE-LIBRARY REF instDecidableAnd
{p q : Prop} → [dp : Decidable p] → [dq : Decidable q] → Decidable (p ∧ q)

## BASE-LIBRARY REF Fin.decLt
{n : ℕ} → (a b : Fin n) → Decidable (a < b)

## BASE-LIBRARY REF Finset.univ
{α : Type u_1} → [Fintype α] → Finset α

Docstring: `univ` is the universal finite set of type `Finset α` implied from
the assumption `Fintype α`. 

## BASE-LIBRARY REF Fin.fintype
(n : ℕ) → Fintype (Fin n)

## INFORMAL STATEMENT
def.perm.setR

\leanhelper  The set $R$ from Proposition~ \ref{prop.perm.lisitij}: $R = \{ k \in \{ i+1, \ldots , j-1\}  \mid \sigma (i) < \sigma (k) < \sigma (j)\} $.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The formal body `fun {n} \u03c3 i j => {k | i < k \u2227 k < j \u2227 \u03c3 i < \u03c3 k \u2227 \u03c3 k < \u03c3 j}` exactly represents the blueprint\u2019s `R = { k \u2208 { i+1, ..., j-1} | \u03c3(i) < \u03c3(k) < \u03c3(j) }`: for `k : Fin n`, membership in `{i+1, \u2026, j-1}` is equivalently `i < k \u2227 k < j`, and the remaining conjuncts express the two strict image inequalities. The binders `{n : \u2115} \u2192 Equiv.Perm (Fin n) \u2192 Fin n \u2192 Fin n` supply precisely a finite permutation and indices; they add no mathematically contentful hypothesis."
}