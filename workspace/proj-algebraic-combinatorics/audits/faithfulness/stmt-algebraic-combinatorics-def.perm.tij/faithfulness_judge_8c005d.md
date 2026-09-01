## TARGET AlgebraicCombinatorics.transposition (def) — ELABORATED SIGNATURE
{X : Type u_1} → [DecidableEq X] → X → X → Equiv.Perm X

Body:
fun {X} [DecidableEq X] i j => Equiv.swap i j

Docstring: The transposition swapping `i` and `j`. In Mathlib, this is `Equiv.swap i j`.
(def.perm.tij)

A transposition `t_{i,j}` is the permutation of `X` that:
- sends `i` to `j` (see `transposition_apply_left`)
- sends `j` to `i` (see `transposition_apply_right`)
- leaves all other elements unchanged (see `transposition_apply_of_ne_of_ne`) 

## TARGET AlgebraicCombinatorics.transposition_apply_of_ne_of_ne (theorem) — ELABORATED SIGNATURE
∀ {X : Type u_1} [inst : DecidableEq X] {i j x : X}, x ≠ i → x ≠ j → (AlgebraicCombinatorics.transposition i j) x = x

Docstring: The transposition `t_{i,j}` leaves all other elements unchanged. (def.perm.tij) 

## TARGET AlgebraicCombinatorics.transposition_apply_left (theorem) — ELABORATED SIGNATURE
∀ {X : Type u_1} [inst : DecidableEq X] (i j : X), (AlgebraicCombinatorics.transposition i j) i = j

Docstring: The transposition `t_{i,j}` sends `i` to `j`. (def.perm.tij) 

## TARGET AlgebraicCombinatorics.transposition_apply_right (theorem) — ELABORATED SIGNATURE
∀ {X : Type u_1} [inst : DecidableEq X] (i j : X), (AlgebraicCombinatorics.transposition i j) j = i

Docstring: The transposition `t_{i,j}` sends `j` to `i`. (def.perm.tij) 

## BASE-LIBRARY REF DecidableEq
Sort u → Sort (max 1 u)

Docstring: Propositional equality is `Decidable` for all elements of a type.

In other words, an instance of `DecidableEq α` is a means of deciding the proposition `a = b` is
for all `a b : α`.


## BASE-LIBRARY REF Equiv.Perm
Sort u_1 → Sort (max 1 u_1)

Docstring: `Perm α` is the type of bijections from `α` to itself. 

## BASE-LIBRARY REF Equiv.swap
{α : Sort u_1} → [DecidableEq α] → α → α → Equiv.Perm α

Docstring: `swap a b` is the permutation that swaps `a` and `b` and
leaves other values as is. 

## BASE-LIBRARY REF Ne
{α : Sort u} → α → α → Prop

Docstring: `a ≠ b`, or `Ne a b` is defined as `¬ (a = b)` or `a = b → False`,
and asserts that `a` and `b` are not equal.


Conventions for notations in identifiers:

 * The recommended spelling of `≠` in identifiers is `ne`.

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

## BASE-LIBRARY REF DFunLike.coe
{F : Sort u_1} → {α : outParam (Sort u_2)} → {β : outParam (α → Sort u_3)} → [self : DFunLike F α β] → F → (a : α) → β a

Docstring: The coercion from `F` to a function. 

## BASE-LIBRARY REF EquivLike.toFunLike
{E : Sort u_1} → {α : Sort u_3} → {β : Sort u_4} → [EquivLike E α β] → FunLike E α β

## BASE-LIBRARY REF Equiv.instEquivLike
{α : Sort u} → {β : Sort v} → EquivLike (α ≃ β) α β

## INFORMAL STATEMENT
def.perm.tij

Let $i$ and $j$ be two distinct elements of a set $X$. 

Then, the \emph{transposition} $t_{i,j}$ is the permutation of $X$ that sends $i$ to $j$, sends $j$ to $i$, and leaves all other elements of $X$ unchanged.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The formalization defines `transposition i j` as `Equiv.swap i j`, whose documented meaning is the permutation that \u201cswaps `a` and `b` and leaves other values as is.\u201d The three theorems exactly provide the stated behavior: `(transposition i j) i = j`, `(transposition i j) j = i`, and, under `x \u2260 i \u2192 x \u2260 j`, `(transposition i j) x = x`. Although the blueprint assumes \u201c`i` and `j` [are] two distinct elements,\u201d the formal binders impose no `i \u2260 j`; this makes the declarations strictly more general, and they imply the blueprint statement by specialization to distinct `i,j`. The `[DecidableEq X]` binder is the computational instance required by `Equiv.swap`, encoding the formal construction rather than a mathematically contentful alteration of the transposition claim."
}