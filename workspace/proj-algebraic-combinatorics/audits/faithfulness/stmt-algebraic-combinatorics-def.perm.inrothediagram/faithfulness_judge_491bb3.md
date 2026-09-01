## TARGET Equiv.Perm.inRotheDiagram (def) — ELABORATED SIGNATURE
{n : ℕ} → Equiv.Perm (Fin n) → Fin n → Fin n → Prop

Body:
fun {n} σ i j => j < σ i ∧ i < σ⁻¹ j

Docstring: A cell (i, j) is in the Rothe diagram of σ if σ(i) > j and σ⁻¹(j) > i.
These are the cells that are not "hit" by the Lehmer lasers. 

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

## BASE-LIBRARY REF Inv.inv
{α : Type u} → [self : Inv α] → α → α

Docstring: `a⁻¹` computes the inverse of `a`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `⁻¹` in identifiers is `inv`.

## BASE-LIBRARY REF Equiv.Perm.instInv
{α : Type u_4} → Inv (Equiv.Perm α)

## INFORMAL STATEMENT
def.perm.inRotheDiagram

\leanhelper  A cell $(i, j)$ is in the \emph{Rothe diagram} of $\sigma $ if $j < \sigma (i)$ and $i < \sigma ^{-1}(j)$. These are the cells that are not “hit” by either the row or column of a permutation matrix entry.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The formal body `fun {n} \u03c3 i j => j < \u03c3 i \u2227 i < \u03c3\u207b\u00b9 j` exactly matches the informal definition: \u201cA cell `(i, j)` is in the Rothe diagram of `\u03c3` if `j < \u03c3(i)` and `i < \u03c3\u207b\u00b9(j)`.\u201d The binders `{n : \u2115} \u2192 Equiv.Perm (Fin n) \u2192 Fin n \u2192 Fin n \u2192 Prop` encode the finite permutation setting and cell indices without adding any mathematically substantive hypothesis. The final sentence about cells not hit by the row or column of a permutation-matrix entry is explanatory rather than an additional condition."
}