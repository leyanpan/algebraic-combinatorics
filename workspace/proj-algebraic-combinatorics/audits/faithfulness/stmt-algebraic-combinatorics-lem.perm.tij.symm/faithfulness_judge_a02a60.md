## TARGET AlgebraicCombinatorics.transposition_symm (theorem) — ELABORATED SIGNATURE
∀ {X : Type u_1} [inst : DecidableEq X] (i j : X),
  AlgebraicCombinatorics.transposition i j = AlgebraicCombinatorics.transposition j i

Docstring: Transpositions are symmetric: `t_{i,j} = t_{j,i}`. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.transposition (def)
{X : Type u_1} → [DecidableEq X] → X → X → Equiv.Perm X

Body:
fun {X} [DecidableEq X] i j => Equiv.swap i j

Docstring: The transposition swapping `i` and `j`. In Mathlib, this is `Equiv.swap i j`.
(def.perm.tij)

A transposition `t_{i,j}` is the permutation of `X` that:
- sends `i` to `j` (see `transposition_apply_left`)
- sends `j` to `i` (see `transposition_apply_right`)
- leaves all other elements unchanged (see `transposition_apply_of_ne_of_ne`) 

## BASE-LIBRARY REF DecidableEq
Sort u → Sort (max 1 u)

Docstring: Propositional equality is `Decidable` for all elements of a type.

In other words, an instance of `DecidableEq α` is a means of deciding the proposition `a = b` is
for all `a b : α`.


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

## BASE-LIBRARY REF Equiv.Perm
Sort u_1 → Sort (max 1 u_1)

Docstring: `Perm α` is the type of bijections from `α` to itself. 

## BASE-LIBRARY REF Equiv.swap
{α : Sort u_1} → [DecidableEq α] → α → α → Equiv.Perm α

Docstring: `swap a b` is the permutation that swaps `a` and `b` and
leaves other values as is. 

## INFORMAL STATEMENT
lem.perm.tij.symm

\leanhelper  For any two distinct elements $i, j$ of a set $X$, we have $t_{i,j} = t_{j,i}$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.tij
def.perm.tij

Let $i$ and $j$ be two distinct elements of a set $X$. 

Then, the \emph{transposition} $t_{i,j}$ is the permutation of $X$ that sends $i$ to $j$, sends $j$ to $i$, and leaves all other elements of $X$ unchanged.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The blueprint states: \u201cFor any two distinct elements $i,j$ of a set $X$, we have $t_{i,j}=t_{j,i}$.\u201d The Lean target proves `\u2200 {X : Type u_1} [DecidableEq X] (i j : X), transposition i j = transposition j i`, with no distinctness hypothesis, so it is strictly more general in `i,j` and in particular implies the stated distinct case. The dependency defines `transposition i j` as `Equiv.swap i j`, matching the informal transposition. The `[DecidableEq X]` binder is the computational instance required by `Equiv.swap` and thus encodes the formal setting rather than adding a mathematical restriction to the symmetry claim."
}