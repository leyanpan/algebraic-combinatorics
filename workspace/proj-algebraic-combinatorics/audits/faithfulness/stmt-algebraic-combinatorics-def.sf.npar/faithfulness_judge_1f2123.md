## TARGET AlgebraicCombinatorics.SymmetricFunctions.NPartition (def) — ELABORATED SIGNATURE
ℕ → Type

Body:
fun N => NPartition N

Docstring: Alias for the canonical `NPartition` type within this namespace.
An N-partition is a weakly decreasing N-tuple of nonnegative integers.
(Definition def.sf.Npar)

This is represented as a function `Fin N → ℕ` that is antitone
(i.e., `i ≤ j → parts j ≤ parts i`).

All basic operations (`size`, `length`, `zero`, etc.) and lemmas are inherited
from the canonical `_root_.NPartition` definition in `NPartition.lean`. 

## PROJECT DEPENDENCY NPartition (inductive)
ℕ → Type

Body:
NPartition.mk : {N : ℕ} → (parts : Fin N → ℕ) → Antitone parts → NPartition N

Docstring: An N-partition is a weakly decreasing N-tuple of nonnegative integers.
(Definition def.sf.Npar)

This is represented as a function `Fin N → ℕ` that is antitone
(i.e., `i ≤ j → parts j ≤ parts i`).

The field is named `antitone` to match Mathlib conventions. 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


## BASE-LIBRARY REF Antitone
{α : Type u} → {β : Type v} → [Preorder α] → [Preorder β] → (α → β) → Prop

Docstring: A function `f` is antitone if `a ≤ b` implies `f b ≤ f a`. 

## BASE-LIBRARY REF PartialOrder.toPreorder
{α : Type u_2} → [self : PartialOrder α] → Preorder α

## BASE-LIBRARY REF Fin.instPartialOrder
{n : ℕ} → PartialOrder (Fin n)

## BASE-LIBRARY REF Nat.instPreorder
Preorder ℕ

## INFORMAL STATEMENT
def.sf.Npar

An $N$\emph{-partition} will mean a weakly decreasing $N$-tuple of nonnegative integers. In other words, an $N$-partition means an $N$-tuple $\left( \lambda _{1},\lambda _{2},\ldots ,\lambda _{N}\right) \in \mathbb {N}^{N}$ with $\lambda _{1}\geq \lambda _{2}\geq \cdots \geq \lambda _{N}$. 

The \emph{size} (or weight) of an $N$-partition $\lambda = (\lambda _1, \lambda _2, \ldots , \lambda _N)$ is defined to be $|\lambda | := \lambda _1 + \lambda _2 + \cdots + \lambda _N$.

## VERDICT
{
  "verdict": "drift",
  "justification": "The type component is faithful: the target is an alias `fun N => NPartition N`, and the dependency constructs values from `parts : Fin N \u2192 \u2115` with `Antitone parts`, exactly encoding a weakly decreasing `N`-tuple of nonnegative integers. However, the informal statement also defines size: \u201c`|\u03bb| := \u03bb\u2081 + \u03bb\u2082 + \u22ef + \u03bb_N`.\u201d Neither the target body nor any supplied dependency defines this operation; the docstring\u2019s claim that `size` is inherited is not itself a definition. Thus the declaration formalizes only the first paragraph. To be faithful to the full blueprint entry, the relevant dependency or an accompanying declaration must define `size` as the finite sum of all `N` parts (and the target namespace may alias/inherit that definition)."
}