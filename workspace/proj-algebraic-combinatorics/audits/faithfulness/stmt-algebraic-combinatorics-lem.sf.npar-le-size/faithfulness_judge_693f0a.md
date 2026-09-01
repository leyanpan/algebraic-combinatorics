## TARGET NPartition.size_le_of_le (theorem) — ELABORATED SIGNATURE
∀ {N : ℕ} {μ ν : NPartition N}, μ ≤ ν → μ.size ≤ ν.size

Docstring: μ ≤ ν implies |μ| ≤ |ν| 

## PROJECT DEPENDENCY NPartition (inductive)
ℕ → Type

Body:
NPartition.mk : {N : ℕ} → (parts : Fin N → ℕ) → Antitone parts → NPartition N

Docstring: An N-partition is a weakly decreasing N-tuple of nonnegative integers.
(Definition def.sf.Npar)

This is represented as a function `Fin N → ℕ` that is antitone
(i.e., `i ≤ j → parts j ≤ parts i`).

The field is named `antitone` to match Mathlib conventions. 

## PROJECT DEPENDENCY NPartition.instLE (def)
{N : ℕ} → LE (NPartition N)

Body:
fun {N} => { le := fun μ ν => ∀ (i : Fin N), μ.parts i ≤ ν.parts i }

Docstring: Containment of partitions: μ ≤ ν means μᵢ ≤ νᵢ for all i 

## PROJECT DEPENDENCY NPartition.size (def)
{N : ℕ} → NPartition N → ℕ

Body:
fun {N} μ => ∑ i, μ.parts i

Docstring: The size (or weight) of an N-partition is the sum of its entries.
If μ = (μ₁, μ₂, ..., μ_N), then |μ| = μ₁ + μ₂ + ... + μ_N. 

## PROJECT DEPENDENCY NPartition.parts (def)
{N : ℕ} → NPartition N → Fin N → ℕ

Body:
fun N self => self.1

Docstring: The entries of the N-partition as a function from `Fin N` to `ℕ` 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF LE.le
{α : Type u} → [self : LE α] → α → α → Prop

Docstring: The less-equal relation: `x ≤ y` 

Conventions for notations in identifiers:

 * The recommended spelling of `≤` in identifiers is `le`.

 * The recommended spelling of `<=` in identifiers is `le` (prefer `≤` over `<=`).

## BASE-LIBRARY REF instLENat
LE ℕ

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

## BASE-LIBRARY REF LE
Type u → Type u

Docstring: `LE α` is the typeclass which supports the notation `x ≤ y` where `x y : α`.

## BASE-LIBRARY REF LE.mk
{α : Type u} → (α → α → Prop) → LE α

## BASE-LIBRARY REF Finset.sum
{ι : Type u_1} → {M : Type u_3} → [AddCommMonoid M] → Finset ι → (ι → M) → M

Docstring: `∑ x ∈ s, f x` is the sum of `f x` as `x` ranges over the elements
of the finite set `s`.

When the index type is a `Fintype`, the notation `∑ x, f x`, is a shorthand for
`∑ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF Nat.instAddCommMonoid
AddCommMonoid ℕ

## BASE-LIBRARY REF Finset.univ
{α : Type u_1} → [Fintype α] → Finset α

Docstring: `univ` is the universal finite set of type `Finset α` implied from
the assumption `Fintype α`. 

## BASE-LIBRARY REF Fin.fintype
(n : ℕ) → Fintype (Fin n)

## INFORMAL STATEMENT
lem.sf.Npar-le-size

\leanhelper  If $\mu \leq \nu $ (componentwise), then $|\mu | \leq |\nu |$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.npar
def.sf.Npar

An $N$\emph{-partition} will mean a weakly decreasing $N$-tuple of nonnegative integers. In other words, an $N$-partition means an $N$-tuple $\left( \lambda _{1},\lambda _{2},\ldots ,\lambda _{N}\right) \in \mathbb {N}^{N}$ with $\lambda _{1}\geq \lambda _{2}\geq \cdots \geq \lambda _{N}$. 

The \emph{size} (or weight) of an $N$-partition $\lambda = (\lambda _1, \lambda _2, \ldots , \lambda _N)$ is defined to be $|\lambda | := \lambda _1 + \lambda _2 + \cdots + \lambda _N$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.npar-order
def.sf.Npar-order

\leanhelper  We define a partial order on $N$-partitions by componentwise comparison: $\mu \leq \nu $ iff $\mu _i \leq \nu _i$ for all $i \in [N]$.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The target quantifies over the same fixed length and partitions, `\u2200 {N : \u2115} {\u03bc \u03bd : NPartition N}`, and assumes exactly `\u03bc \u2264 \u03bd`. By `NPartition.instLE`, this means `\u2200 (i : Fin N), \u03bc.parts i \u2264 \u03bd.parts i`, matching \u201c\u03bc \u2264 \u03bd (componentwise)\u201d and the definition \u201c\u03bc\u1d62 \u2264 \u03bd\u1d62 for all i \u2208 [N].\u201d Its conclusion `\u03bc.size \u2264 \u03bd.size` matches `|\u03bc| \u2264 |\u03bd|`, since `NPartition.size` is `\u2211 i, \u03bc.parts i`, exactly the sum of all N entries. `NPartition` itself consists of antitone `Fin N \u2192 \u2115` functions, matching weakly decreasing N-tuples of nonnegative integers. No additional hypothesis or restricted quantifier is introduced."
}