## TARGET mem_skewYoungDiagram (theorem) — ELABORATED SIGNATURE
∀ {N : ℕ} [inst : NeZero N] {lam mu : NPartition N} {c : Fin N × ℕ},
  c ∈ skewYoungDiagram lam mu ↔ mu.parts c.1 ≤ c.2 ∧ c.2 < lam.parts c.1

Docstring: Membership in a skew Young diagram: (i, j) ∈ Y(λ/μ) iff μ_i ≤ j < λ_i.
This is the 0-indexed version of the textbook condition μ_i < j ≤ λ_i. 

## PROJECT DEPENDENCY NPartition (inductive)
ℕ → Type

Body:
NPartition.mk : {N : ℕ} → (parts : Fin N → ℕ) → Antitone parts → NPartition N

Docstring: An N-partition is a weakly decreasing N-tuple of nonnegative integers.
(Definition def.sf.Npar)

This is represented as a function `Fin N → ℕ` that is antitone
(i.e., `i ≤ j → parts j ≤ parts i`).

The field is named `antitone` to match Mathlib conventions. 

## PROJECT DEPENDENCY skewYoungDiagram (def)
{N : ℕ} → [NeZero N] → NPartition N → NPartition N → Finset (Fin N × ℕ)

Body:
fun {N} [NeZero N] lam mu => lam.youngDiagram \ mu.youngDiagram

Docstring: The skew Young diagram Y(λ/μ) is the set difference Y(λ) \ Y(μ).
Definition \ref{def.sf.skew-diag} in the source.

**Note**: This is a duplicate of `NPartition.skewYoungDiagram` that requires `[NeZero N]`.
Prefer `NPartition.skewYoungDiagram` for new code as it works for all `N`.

For N-partitions λ and μ with μ ⊆ λ, the skew Young diagram Y(λ/μ) is defined as:
```
Y(λ) \ Y(μ) = {(i,j) | i ∈ [N] and j ∈ [λ_i] \ [μ_i]}
            = {(i,j) | i ∈ [N] and j ∈ ℤ and μ_i < j ≤ λ_i}
```
(The second form uses 1-indexed j as in the textbook.)

In our 0-indexed formalization, this becomes:
```
Y(λ/μ) = {(i,j) | i ∈ Fin N and μ_i ≤ j < λ_i}
```

Example: Y((4,3,1)/(2,1,0)) consists of cells:
- Row 0: (0, 2), (0, 3)  (since μ₀ = 2, λ₀ = 4)
- Row 1: (1, 1), (1, 2)  (since μ₁ = 1, λ₁ = 3)
- Row 2: (2, 0)          (since μ₂ = 0, λ₂ = 1) 

## PROJECT DEPENDENCY NPartition.parts (def)
{N : ℕ} → NPartition N → Fin N → ℕ

Body:
fun N self => self.1

Docstring: The entries of the N-partition as a function from `Fin N` to `ℕ` 

## PROJECT DEPENDENCY NPartition.youngDiagram (def)
{N : ℕ} → NPartition N → Finset (Fin N × ℕ)

Body:
fun {N} μ => Finset.univ.biUnion fun i => Finset.map { toFun := fun j => (i, j), inj' := ⋯ } (Finset.range (μ.parts i))

Docstring: The Young diagram Y(λ) of an N-partition λ is the set of cells (i, j) where
i ∈ Fin N and j < λ_i.
Definition def.sf.ydiag in the source.

Note: Mathlib has `YoungDiagram` which is more general (infinite diagrams).
Here we define a version specific to N-partitions. 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF NeZero
{R : Type u_1} → [Zero R] → R → Prop

Docstring: A type-class version of `n ≠ 0`.  

## BASE-LIBRARY REF MulZeroClass.toZero
{M₀ : Type u} → [self : MulZeroClass M₀] → Zero M₀

## BASE-LIBRARY REF Nat.instMulZeroClass
MulZeroClass ℕ

## BASE-LIBRARY REF Prod
Type u → Type v → Type (max u v)

Docstring: The product type, usually written `α × β`. Product types are also called pair or tuple types.
Elements of this type are pairs in which the first element is an `α` and the second element is a
`β`.

Products nest to the right, so `(x, y, z) : α × β × γ` is equivalent to `(x, (y, z)) : α × (β × γ)`.


Conventions for notations in identifiers:

 * The recommended spelling of `×` in identifiers is `Prod`.

## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


## BASE-LIBRARY REF Iff
Prop → Prop → Prop

Docstring: If and only if, or logical bi-implication. `a ↔ b` means that `a` implies `b` and vice versa.
By `propext`, this implies that `a` and `b` are equal and hence any expression involving `a`
is equivalent to the corresponding expression with `b` instead.


Conventions for notations in identifiers:

 * The recommended spelling of `↔` in identifiers is `iff`.

 * The recommended spelling of `<->` in identifiers is `iff` (prefer `↔` over `<->`).

## BASE-LIBRARY REF Membership.mem
{α : outParam (Type u)} → {γ : Type v} → [self : Membership α γ] → γ → α → Prop

Docstring: The membership relation `a ∈ s : Prop` where `a : α`, `s : γ`. 

Conventions for notations in identifiers:

 * The recommended spelling of `∈` in identifiers is `mem`.

## BASE-LIBRARY REF Finset
Type u_4 → Type u_4

Docstring: `Finset α` is the type of finite sets of elements of `α`. It is implemented
as a multiset (a list up to permutation) which has no duplicate elements. 

## BASE-LIBRARY REF Finset.instMembership
{α : Type u_1} → Membership α (Finset α)

## BASE-LIBRARY REF And
Prop → Prop → Prop

Docstring: `And a b`, or `a ∧ b`, is the conjunction of propositions. It can be
constructed and destructed like a pair: if `ha : a` and `hb : b` then
`⟨ha, hb⟩ : a ∧ b`, and if `h : a ∧ b` then `h.left : a` and `h.right : b`.


Conventions for notations in identifiers:

 * The recommended spelling of `∧` in identifiers is `and`.

 * The recommended spelling of `/\` in identifiers is `and` (prefer `∧` over `/\`).

## BASE-LIBRARY REF LE.le
{α : Type u} → [self : LE α] → α → α → Prop

Docstring: The less-equal relation: `x ≤ y` 

Conventions for notations in identifiers:

 * The recommended spelling of `≤` in identifiers is `le`.

 * The recommended spelling of `<=` in identifiers is `le` (prefer `≤` over `<=`).

## BASE-LIBRARY REF instLENat
LE ℕ

## BASE-LIBRARY REF Prod.fst
{α : Type u} → {β : Type v} → α × β → α

Docstring: The first element of a pair. 

## BASE-LIBRARY REF Prod.snd
{α : Type u} → {β : Type v} → α × β → β

Docstring: The second element of a pair. 

## BASE-LIBRARY REF LT.lt
{α : Type u} → [self : LT α] → α → α → Prop

Docstring: The less-than relation: `x < y` 

Conventions for notations in identifiers:

 * The recommended spelling of `<` in identifiers is `lt`.

## BASE-LIBRARY REF instLTNat
LT ℕ

## BASE-LIBRARY REF Antitone
{α : Type u} → {β : Type v} → [Preorder α] → [Preorder β] → (α → β) → Prop

Docstring: A function `f` is antitone if `a ≤ b` implies `f b ≤ f a`. 

## BASE-LIBRARY REF PartialOrder.toPreorder
{α : Type u_2} → [self : PartialOrder α] → Preorder α

## BASE-LIBRARY REF Fin.instPartialOrder
{n : ℕ} → PartialOrder (Fin n)

## BASE-LIBRARY REF Nat.instPreorder
Preorder ℕ

## BASE-LIBRARY REF SDiff.sdiff
{α : Type u} → [self : SDiff α] → α → α → α

Docstring: `a \ b` is the set difference of `a` and `b`,
consisting of all elements in `a` that are not in `b`.


Conventions for notations in identifiers:

 * The recommended spelling of `\` in identifiers is `sdiff`.

## BASE-LIBRARY REF Finset.instSDiff
{α : Type u_1} → [DecidableEq α] → SDiff (Finset α)

Docstring: `s \ t` is the set consisting of the elements of `s` that are not in `t`. 

## BASE-LIBRARY REF instDecidableEqProd
{α : Type u_1} → {β : Type u_2} → [DecidableEq α] → [DecidableEq β] → DecidableEq (α × β)

## BASE-LIBRARY REF instDecidableEqFin
(n : ℕ) → DecidableEq (Fin n)

## BASE-LIBRARY REF instDecidableEqNat
DecidableEq ℕ

## BASE-LIBRARY REF Finset.biUnion
{α : Type u_1} → {β : Type u_2} → [DecidableEq β] → Finset α → (α → Finset β) → Finset β

Docstring: `Finset.biUnion s t` is the union of `t a` over `a ∈ s`.

(This was formerly `bind` due to the monad structure on types with `DecidableEq`.) 

## BASE-LIBRARY REF Finset.univ
{α : Type u_1} → [Fintype α] → Finset α

Docstring: `univ` is the universal finite set of type `Finset α` implied from
the assumption `Fintype α`. 

## BASE-LIBRARY REF Fin.fintype
(n : ℕ) → Fintype (Fin n)

## BASE-LIBRARY REF Finset.map
{α : Type u_1} → {β : Type u_2} → (α ↪ β) → Finset α → Finset β

Docstring: When `f` is an embedding of `α` in `β` and `s` is a finset in `α`, then `s.map f` is the image
finset in `β`. The embedding condition guarantees that there are no duplicates in the image. 

## BASE-LIBRARY REF Function.Embedding.mk
{α : Sort u_1} → {β : Sort u_2} → (toFun : α → β) → Function.Injective toFun → α ↪ β

## BASE-LIBRARY REF Prod.mk
{α : Type u} → {β : Type v} → α → β → α × β

Docstring: Constructs a pair. This is usually written `(x, y)` instead of `Prod.mk x y`.


Conventions for notations in identifiers:

 * The recommended spelling of `(a, b)` in identifiers is `mk`.

## BASE-LIBRARY REF Finset.range
ℕ → Finset ℕ

Docstring: `range n` is the set of natural numbers less than `n`. 

## INFORMAL STATEMENT
lem.sf.skew-diag-mem

\leanhelper  A cell $(i,j)$ belongs to $Y(\lambda /\mu )$ if and only if $\mu _i \le j < \lambda _i$ (in 0-indexed coordinates).

## INFORMAL DEFINITION stmt-algebraic-combinatorics-conv-2eb59533
conv-2eb59533

In the Lean formalization, we use $\operatorname {Fin} n = \{ 0, 1, \ldots , n-1\} $ instead of the textbook’s $[n] = \{ 1, 2, \ldots , n\} $. Both are $n$-element sets, so their symmetric groups are isomorphic. Permutations are represented by the type of bijections $X \to X$ (denoted $\operatorname {Equiv.Perm}\,  X$ in Lean), which is a group under composition. Composition $\alpha \beta $ is the group multiplication $\alpha * \beta $, sending $x$ to $\alpha (\beta (x))$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.perm
def.perm.perm

Let $X$ be a set. 

\textbf{(a)} A \emph{permutation} of $X$ means a bijection from $X$ to $X$. 

\textbf{(b)} It is known that the set of all permutations of $X$ is a group under composition. This group is called the \emph{symmetric group} of $X$, and is denoted by $S_X$. Its neutral element is the identity map $\operatorname {id}_X : X \to X$. Its size is $|X|!$ when $X$ is finite. 

\textbf{(c)} As usual in group theory, we will write $\alpha \beta $ for the composition $\alpha \circ \beta $ when $\alpha , \beta \in S_X$. This is the map that sends each $x \in X$ to $\alpha (\beta (x))$. 

\textbf{(d)} If $\alpha \in S_X$ and $i \in \mathbb {Z}$, then $\alpha ^i$ shall denote the $i$-th power of $\alpha $ in the group $S_X$. Note that $\alpha ^i = \underbrace{\alpha \circ \alpha \circ \cdots \circ \alpha }_{i\text{ times}}$ if $i \ge 0$. Also, $\alpha ^0 = \operatorname {id}_X$. Also, $\alpha ^{-1}$ is the inverse of $\alpha $ in the group $S_X$, that is, the inverse of the map $\alpha $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.npar
def.sf.Npar

An $N$\emph{-partition} will mean a weakly decreasing $N$-tuple of nonnegative integers. In other words, an $N$-partition means an $N$-tuple $\left( \lambda _{1},\lambda _{2},\ldots ,\lambda _{N}\right) \in \mathbb {N}^{N}$ with $\lambda _{1}\geq \lambda _{2}\geq \cdots \geq \lambda _{N}$. 

The \emph{size} (or weight) of an $N$-partition $\lambda = (\lambda _1, \lambda _2, \ldots , \lambda _N)$ is defined to be $|\lambda | := \lambda _1 + \lambda _2 + \cdots + \lambda _N$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.npar-skewyoungdiagram
def.sf.Npar-skewYoungDiagram

\leanhelper  The \emph{skew Young diagram} $Y(\lambda /\mu )$ for $N$-partitions $\lambda , \mu $ is the set difference $Y(\lambda ) \setminus Y(\mu )$, consisting of cells $(i, j)$ with $\mu _i \leq j < \lambda _i$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.npar-youngdiagram
def.sf.Npar-youngDiagram

\leanhelper  The \emph{Young diagram} $Y(\lambda )$ of an $N$-partition $\lambda $ is the finite set of cells 

\[  Y(\lambda ) = \{ (i, j) : i \in [N],\;  0 \leq j < \lambda _i\} .  \]

## VERDICT
{
  "verdict": "drift",
  "justification": "The membership characterization itself matches exactly: the target concludes `c \u2208 skewYoungDiagram lam mu \u2194 mu.parts c.1 \u2264 c.2 \u2227 c.2 < lam.parts c.1`, corresponding to \u201c$(i,j)$ belongs to $Y(\\lambda/\\mu)$ iff $\\mu_i \\le j < \\lambda_i$.\u201d However, the elaborated target adds `[inst : NeZero N]`, restricting it to `N \u2260 0`, while the blueprint quantifies over $N$-partitions without requiring $N>0$. This restriction enters through the project dependency `skewYoungDiagram`, whose signature itself requires `[NeZero N]`; its own docstring notes that this is a duplicate and that `NPartition.skewYoungDiagram` works for all `N`. Thus the extra hypothesis is not required to encode the diagram or membership relation. To make the declaration faithful, use or redefine `skewYoungDiagram` without `[NeZero N]` and remove `[inst : NeZero N]` from `mem_skewYoungDiagram`."
}