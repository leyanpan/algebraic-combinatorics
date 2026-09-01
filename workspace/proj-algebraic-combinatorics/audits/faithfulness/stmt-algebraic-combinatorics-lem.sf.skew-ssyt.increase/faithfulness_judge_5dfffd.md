## TARGET SkewSSYT.row_weak_of_le (theorem) — ELABORATED SIGNATURE
∀ {N : ℕ} [inst : NeZero N] {lam mu : NPartition N} (T : SkewSSYT lam mu) {i : Fin N} {j₁ j₂ : ℕ},
  (i, j₁) ∈ skewYoungDiagram lam mu → (i, j₂) ∈ skewYoungDiagram lam mu → j₁ ≤ j₂ → T.entry (i, j₁) ≤ T.entry (i, j₂)

Docstring: In a semistandard skew tableau, entries increase weakly along rows (general version).
Lemma \ref{lem.sf.skew-ssyt.increase}(a) in the source. 

## TARGET SkewSSYT.monotone (theorem) — ELABORATED SIGNATURE
∀ {N : ℕ} [inst : NeZero N] {lam mu : NPartition N} (T : SkewSSYT lam mu) {i₁ i₂ : Fin N} {j₁ j₂ : ℕ},
  (i₁, j₁) ∈ skewYoungDiagram lam mu →
    (i₂, j₂) ∈ skewYoungDiagram lam mu → i₁ ≤ i₂ → j₁ ≤ j₂ → T.entry (i₁, j₁) ≤ T.entry (i₂, j₂)

Docstring: In a semistandard skew tableau, if (i₁, j₁) ≤ (i₂, j₂) componentwise,
then T(i₁, j₁) ≤ T(i₂, j₂).
Lemma \ref{lem.sf.skew-ssyt.increase}(d) in the source. 

## TARGET SkewSSYT.col_strict_of_lt (theorem) — ELABORATED SIGNATURE
∀ {N : ℕ} [inst : NeZero N] {lam mu : NPartition N} (T : SkewSSYT lam mu) {i₁ i₂ : Fin N} {j : ℕ},
  (i₁, j) ∈ skewYoungDiagram lam mu → (i₂, j) ∈ skewYoungDiagram lam mu → i₁ < i₂ → T.entry (i₁, j) < T.entry (i₂, j)

Docstring: In a semistandard skew tableau, entries increase strictly down columns.
Lemma \ref{lem.sf.skew-ssyt.increase}(c) in the source. 

## TARGET SkewSSYT.strict_monotone (theorem) — ELABORATED SIGNATURE
∀ {N : ℕ} [inst : NeZero N] {lam mu : NPartition N} (T : SkewSSYT lam mu) {i₁ i₂ : Fin N} {j₁ j₂ : ℕ},
  (i₁, j₁) ∈ skewYoungDiagram lam mu →
    (i₂, j₂) ∈ skewYoungDiagram lam mu → i₁ < i₂ → j₁ ≤ j₂ → T.entry (i₁, j₁) < T.entry (i₂, j₂)

Docstring: In a semistandard skew tableau, if i₁ < i₂ and j₁ ≤ j₂,
then T(i₁, j₁) < T(i₂, j₂).
Lemma \ref{lem.sf.skew-ssyt.increase}(e) in the source. 

## TARGET SkewSSYT.col_weak (theorem) — ELABORATED SIGNATURE
∀ {N : ℕ} [inst : NeZero N] {lam mu : NPartition N} (T : SkewSSYT lam mu) {i₁ i₂ : Fin N} {j : ℕ},
  (i₁, j) ∈ skewYoungDiagram lam mu → (i₂, j) ∈ skewYoungDiagram lam mu → i₁ ≤ i₂ → T.entry (i₁, j) ≤ T.entry (i₂, j)

Docstring: In a semistandard skew tableau, entries increase weakly down columns.
Lemma \ref{lem.sf.skew-ssyt.increase}(b) in the source. 

## PROJECT DEPENDENCY NPartition (inductive)
ℕ → Type

Body:
NPartition.mk : {N : ℕ} → (parts : Fin N → ℕ) → Antitone parts → NPartition N

Docstring: An N-partition is a weakly decreasing N-tuple of nonnegative integers.
(Definition def.sf.Npar)

This is represented as a function `Fin N → ℕ` that is antitone
(i.e., `i ≤ j → parts j ≤ parts i`).

The field is named `antitone` to match Mathlib conventions. 

## PROJECT DEPENDENCY SkewSSYT (inductive)
{N : ℕ} → [NeZero N] → NPartition N → NPartition N → Type

Body:
SkewSSYT.mk : {N : ℕ} →
  [inst : NeZero N] →
    {lam mu : NPartition N} →
      (toSkewYoungTableau : SkewYoungTableau lam mu) →
        (∀ (i : Fin N) (j₁ j₂ : ℕ),
            (i, j₁) ∈ skewYoungDiagram lam mu →
              (i, j₂) ∈ skewYoungDiagram lam mu →
                j₁ < j₂ → toSkewYoungTableau.entry (i, j₁) ≤ toSkewYoungTableau.entry (i, j₂)) →
          (∀ (i₁ i₂ : Fin N) (j : ℕ),
              (i₁, j) ∈ skewYoungDiagram lam mu →
                (i₂, j) ∈ skewYoungDiagram lam mu →
                  i₁ < i₂ → toSkewYoungTableau.entry (i₁, j) < toSkewYoungTableau.entry (i₂, j)) →
            SkewSSYT lam mu

Docstring: A semistandard skew Young tableau is a skew tableau where:
- entries increase weakly along each row (left to right)
- entries increase strictly down each column (top to bottom)
Definition \ref{def.sf.skew-ssyt} in the source.

**Note:** This is one of two SkewSSYT definitions in this project:
- **This definition** (`SchurBasics.SkewSSYT`): Uses `entry : Fin N × ℕ → Fin N` with a
  support condition. Extends `SkewYoungTableau`. Takes `lam mu : NPartition N` as separate
  arguments. Requires `[NeZero N]`. Field names: `row_weak`, `col_strict`.
- **Alternative definition** (`SymmetricFunctions.SkewSSYT` in `PieriJacobiTrudi.lean`):
  Uses dependent types. Takes `s : SkewPartition N` as a single bundled argument.
  No `[NeZero N]` requirement. Field names: `rowWeak`, `colStrict`.

See `SSYTEquiv.lean` for conversions between representations. 

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

## PROJECT DEPENDENCY SkewYoungTableau.entry (def)
{N : ℕ} → [inst : NeZero N] → {lam mu : NPartition N} → SkewYoungTableau lam mu → Fin N × ℕ → Fin N

Body:
fun N [NeZero N] lam mu self => self.1

Docstring: The filling function T : Y(λ/μ) → [N] 

## PROJECT DEPENDENCY SkewSSYT.toSkewYoungTableau (def)
{N : ℕ} → [inst : NeZero N] → {lam mu : NPartition N} → SkewSSYT lam mu → SkewYoungTableau lam mu

Body:
fun N [NeZero N] lam mu self => self.1

## PROJECT DEPENDENCY SkewYoungTableau (inductive)
{N : ℕ} → [NeZero N] → NPartition N → NPartition N → Type

Body:
SkewYoungTableau.mk : {N : ℕ} →
  [inst : NeZero N] →
    {lam mu : NPartition N} →
      (entry : Fin N × ℕ → Fin N) → (∀ c ∉ skewYoungDiagram lam mu, entry c = 0) → SkewYoungTableau lam mu

Docstring: A skew Young tableau of shape λ/μ is a filling of Y(λ/μ) with elements of [N].
Definition \ref{def.sf.skew-tab} in the source.

Formally, a Young tableau of shape λ/μ is a map T : Y(λ/μ) → [N].
We represent this as a total function `entry : Fin N × ℕ → Fin N` with a support
condition that entries outside the skew diagram are 0.

Young tableaux of shape λ/μ are often called "skew Young tableaux".

Note: If μ ⊈ λ (i.e., not μ ≤ λ), then there are no Young tableaux of shape λ/μ
because the skew diagram would be empty or malformed. 

## PROJECT DEPENDENCY NPartition.youngDiagram (def)
{N : ℕ} → NPartition N → Finset (Fin N × ℕ)

Body:
fun {N} μ => Finset.univ.biUnion fun i => Finset.map { toFun := fun j => (i, j), inj' := ⋯ } (Finset.range (μ.parts i))

Docstring: The Young diagram Y(λ) of an N-partition λ is the set of cells (i, j) where
i ∈ Fin N and j < λ_i.
Definition def.sf.ydiag in the source.

Note: Mathlib has `YoungDiagram` which is more general (infinite diagrams).
Here we define a version specific to N-partitions. 

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


## BASE-LIBRARY REF NeZero
{R : Type u_1} → [Zero R] → R → Prop

Docstring: A type-class version of `n ≠ 0`.  

## BASE-LIBRARY REF MulZeroClass.toZero
{M₀ : Type u} → [self : MulZeroClass M₀] → Zero M₀

## BASE-LIBRARY REF Nat.instMulZeroClass
MulZeroClass ℕ

## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


## BASE-LIBRARY REF Membership.mem
{α : outParam (Type u)} → {γ : Type v} → [self : Membership α γ] → γ → α → Prop

Docstring: The membership relation `a ∈ s : Prop` where `a : α`, `s : γ`. 

Conventions for notations in identifiers:

 * The recommended spelling of `∈` in identifiers is `mem`.

## BASE-LIBRARY REF Prod
Type u → Type v → Type (max u v)

Docstring: The product type, usually written `α × β`. Product types are also called pair or tuple types.
Elements of this type are pairs in which the first element is an `α` and the second element is a
`β`.

Products nest to the right, so `(x, y, z) : α × β × γ` is equivalent to `(x, (y, z)) : α × (β × γ)`.


Conventions for notations in identifiers:

 * The recommended spelling of `×` in identifiers is `Prod`.

## BASE-LIBRARY REF Finset
Type u_4 → Type u_4

Docstring: `Finset α` is the type of finite sets of elements of `α`. It is implemented
as a multiset (a list up to permutation) which has no duplicate elements. 

## BASE-LIBRARY REF Finset.instMembership
{α : Type u_1} → Membership α (Finset α)

## BASE-LIBRARY REF Prod.mk
{α : Type u} → {β : Type v} → α → β → α × β

Docstring: Constructs a pair. This is usually written `(x, y)` instead of `Prod.mk x y`.


Conventions for notations in identifiers:

 * The recommended spelling of `(a, b)` in identifiers is `mk`.

## BASE-LIBRARY REF LE.le
{α : Type u} → [self : LE α] → α → α → Prop

Docstring: The less-equal relation: `x ≤ y` 

Conventions for notations in identifiers:

 * The recommended spelling of `≤` in identifiers is `le`.

 * The recommended spelling of `<=` in identifiers is `le` (prefer `≤` over `<=`).

## BASE-LIBRARY REF instLENat
LE ℕ

## BASE-LIBRARY REF instLEFin
{n : ℕ} → LE (Fin n)

## BASE-LIBRARY REF LT.lt
{α : Type u} → [self : LT α] → α → α → Prop

Docstring: The less-than relation: `x < y` 

Conventions for notations in identifiers:

 * The recommended spelling of `<` in identifiers is `lt`.

## BASE-LIBRARY REF instLTFin
{n : ℕ} → LT (Fin n)

## BASE-LIBRARY REF Antitone
{α : Type u} → {β : Type v} → [Preorder α] → [Preorder β] → (α → β) → Prop

Docstring: A function `f` is antitone if `a ≤ b` implies `f b ≤ f a`. 

## BASE-LIBRARY REF PartialOrder.toPreorder
{α : Type u_2} → [self : PartialOrder α] → Preorder α

## BASE-LIBRARY REF Fin.instPartialOrder
{n : ℕ} → PartialOrder (Fin n)

## BASE-LIBRARY REF Nat.instPreorder
Preorder ℕ

## BASE-LIBRARY REF instLTNat
LT ℕ

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

## BASE-LIBRARY REF Not
Prop → Prop

Docstring: `Not p`, or `¬p`, is the negation of `p`. It is defined to be `p → False`,
so if your goal is `¬p` you can use `intro h` to turn the goal into
`h : p ⊢ False`, and if you have `hn : ¬p` and `h : p` then `hn h : False`
and `(hn h).elim` will prove anything.
For more information: [Propositional Logic](https://lean-lang.org/theorem_proving_in_lean4/propositions_and_proofs.html#propositional-logic)


Conventions for notations in identifiers:

 * The recommended spelling of `¬` in identifiers is `not`.

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

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF Fin.instOfNat
{n : ℕ} → [NeZero n] → {i : ℕ} → OfNat (Fin n) i

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

## BASE-LIBRARY REF Finset.range
ℕ → Finset ℕ

Docstring: `range n` is the set of natural numbers less than `n`. 

## INFORMAL STATEMENT
lem.sf.skew-ssyt.increase

Let $\lambda $ and $\mu $ be two $N$-partitions. Let $T$ be a semistandard Young tableau of shape $\lambda /\mu $. Then: \medskip 

\textbf{(a)} If $\left( i,j_{1}\right) $ and $\left( i,j_{2}\right) $ are two elements of $Y\left( \lambda /\mu \right) $ satisfying $j_{1}\leq j_{2}$, then $T\left( i,j_{1}\right) \leq T\left( i,j_{2}\right) $. \medskip 

\textbf{(b)} If $\left( i_{1},j\right) $ and $\left( i_{2},j\right) $ are two elements of $Y\left( \lambda /\mu \right) $ satisfying $i_{1}\leq i_{2}$, then $T\left( i_{1},j\right) \leq T\left( i_{2},j\right) $. \medskip 

\textbf{(c)} If $\left( i_{1},j\right) $ and $\left( i_{2},j\right) $ are two elements of $Y\left( \lambda /\mu \right) $ satisfying $i_{1}<i_{2}$, then $T\left( i_{1},j\right) <T\left( i_{2},j\right) $. \medskip 

\textbf{(d)} If $\left( i_{1},j_{1}\right) $ and $\left( i_{2},j_{2}\right) $ are two elements of $Y\left( \lambda /\mu \right) $ satisfying $i_{1}\leq i_{2}$ and $j_{1}\leq j_{2}$, then $T\left( i_{1},j_{1}\right) \leq T\left( i_{2},j_{2}\right) $. \medskip 

\textbf{(e)} If $\left( i_{1},j_{1}\right) $ and $\left( i_{2},j_{2}\right) $ are two elements of $Y\left( \lambda /\mu \right) $ satisfying $i_{1}<i_{2}$ and $j_{1}\leq j_{2}$, then $T\left( i_{1},j_{1}\right) <T\left( i_{2},j_{2}\right) $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.npar
def.sf.Npar

An $N$\emph{-partition} will mean a weakly decreasing $N$-tuple of nonnegative integers. In other words, an $N$-partition means an $N$-tuple $\left( \lambda _{1},\lambda _{2},\ldots ,\lambda _{N}\right) \in \mathbb {N}^{N}$ with $\lambda _{1}\geq \lambda _{2}\geq \cdots \geq \lambda _{N}$. 

The \emph{size} (or weight) of an $N$-partition $\lambda = (\lambda _1, \lambda _2, \ldots , \lambda _N)$ is defined to be $|\lambda | := \lambda _1 + \lambda _2 + \cdots + \lambda _N$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.npar-order
def.sf.Npar-order

\leanhelper  We define a partial order on $N$-partitions by componentwise comparison: $\mu \leq \nu $ iff $\mu _i \leq \nu _i$ for all $i \in [N]$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.par-subset
def.sf.par-subset

Let $\lambda $ and $\mu $ be two $N$-partitions. 

We say that $\mu \subseteq \lambda $ if and only if $Y\left( \mu \right) \subseteq Y\left( \lambda \right) $. Equivalently, $\mu \subseteq \lambda $ if and only if

\[  \text{each }i\in \left[ N\right] \text{ satisfies }\mu _{i}\leq \lambda _{i}.  \]

 Thus we have defined a partial order $\subseteq $ on the set of all $N$-partitions.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.skew-diag
def.sf.skew-diag

Let $\lambda $ and $\mu $ be two $N$-partitions such that $\mu \subseteq \lambda $. Then, we define the \emph{skew Young diagram} $Y\left( \lambda /\mu \right) $ to be the set difference

\begin{align*}  Y\left( \lambda \right) \setminus Y\left( \mu \right) &  =\left\{  \left( i,j\right) \  \mid \  i\in \left[ N\right] \text{ and }j\in \left[ \lambda _{i}\right] \setminus \left[ \mu _{i}\right] \right\}  \\ &  =\left\{  \left( i,j\right) \  \mid \  i\in \left[ N\right] \text{ and }j\in \mathbb {Z}\text{ and }\mu _{i}<j\leq \lambda _{i}\right\}  . \end{align*}

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.skew-ssyt
def.sf.skew-ssyt

Let $\lambda $ and $\mu $ be two $N$-partitions. 

A Young tableau $T$ of shape $\lambda /\mu $ is said to be \emph{semistandard} if its entries 

\begin{itemize} \item increase weakly along each row (from left to right); 

\item increase strictly down each column (from top to bottom). 

\end{itemize}

Formally speaking, this means that a Young tableau $T:Y\left( \lambda /\mu \right) \rightarrow \left[ N\right] $ is semistandard if and only if 

\begin{itemize} \item we have $T\left( i,j\right) \leq T\left( i,j+1\right) $ for any $\left( i,j\right) \in Y\left( \lambda /\mu \right) $ satisfying $\left( i,j+1\right) \in Y\left( \lambda /\mu \right) $; 

\item we have $T\left( i,j\right) <T\left( i+1,j\right) $ for any $\left( i,j\right) \in Y\left( \lambda /\mu \right) $ satisfying $\left( i+1,j\right) \in Y\left( \lambda /\mu \right) $. 

\end{itemize}

We let $\operatorname *{SSYT}\left( \lambda /\mu \right) $ denote the set of all semistandard Young tableaux of shape $\lambda /\mu $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.skew-tab
def.sf.skew-tab

Let $\lambda $ and $\mu $ be two $N$-partitions such that $\mu \subseteq \lambda $. A \emph{Young tableau} of shape $\lambda /\mu $ means a way of filling the boxes of $Y\left( \lambda /\mu \right) $ with elements of $\left[ N\right] $ (one element per box). Formally speaking, it is defined as a map $T:Y\left( \lambda /\mu \right) \rightarrow \left[ N\right] $. 

Young tableaux of shape $\lambda /\mu $ are often called \emph{skew Young tableaux}. 

If we don’t have $\mu \subseteq \lambda $, then we agree that there are no Young tableaux of shape $\lambda /\mu $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.strips
def.sf.strips

Let $\lambda $ and $\mu $ be two $N$-partitions. 

\textbf{(a)} We write $\lambda /\mu $ for the pair $\left( \mu ,\lambda \right) $. Such a pair is called a \emph{skew partition}. 

\textbf{(b)} We say that $\lambda /\mu $ is a \emph{horizontal strip} if we have $\mu \subseteq \lambda $ and the Young diagram $Y\left( \lambda /\mu \right) $ has no two boxes lying in the same column. 

\textbf{(c)} We say that $\lambda /\mu $ is a \emph{vertical strip} if we have $\mu \subseteq \lambda $ and the Young diagram $Y\left( \lambda /\mu \right) $ has no two boxes lying in the same row. 

Now, let $n\in \mathbb {N}$. 

\textbf{(d)} We say that $\lambda /\mu $ is a \emph{horizontal }$n$\emph{-strip} if $\lambda /\mu $ is a horizontal strip and satisfies $\left\vert Y\left( \lambda /\mu \right) \right\vert =n$. 

\textbf{(e)} We say that $\lambda /\mu $ is a \emph{vertical }$n$\emph{-strip} if $\lambda /\mu $ is a vertical strip and satisfies $\left\vert Y\left( \lambda /\mu \right) \right\vert =n$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.ydiag
def.sf.ydiag

Let $\lambda $ be an $N$-partition. 

The \emph{Young diagram} of $\lambda $ is defined as the set

\[  \left\{  \left( i,j\right) \  \mid \  i\in \left[ N\right] \text{ and }j\in \left[ \lambda _{i}\right] \right\}  \subseteq \left\{  1,2,3,\ldots \right\}  ^{2}.  \]

 We visually represent each element $\left( i,j\right) $ of this Young diagram as a box in row $i$ and column $j$. 

We denote the Young diagram of $\lambda $ by $Y\left( \lambda \right) $.

## VERDICT
{
  "verdict": "drift",
  "justification": "All five targets correctly match clauses (a)\u2013(e) in their cell-membership, index-order, and entry-order conclusions. However, every elaborated signature begins with `\u2200 {N : \u2115} [inst : NeZero N]`, whereas the blueprint quantifies over `N`-partitions and does not require `N \u2260 0`. Since `NeZero N` means `N \u2260 0`, this excludes the `N = 0` case and is an added, mathematically contentful restriction, even though that case is trivial or vacuous. The restriction enters through the dependencies `SkewSSYT`, `SkewYoungTableau`, `skewYoungDiagram`, and `SkewYoungTableau.entry`, all of which require `[NeZero N]`, rather than through the substantive inequalities in the targets. To make the declarations faithful, those dependencies should be represented without `[NeZero N]`\u2014in particular, without relying on a distinguished `0 : Fin N` for the total-function support convention\u2014and the targets should quantify over all `N : \u2115`. The fact that the formal definitions also permit tableaux when `\u03bc \u2288 \u03bb` only makes the theorems more general: the informal definition declares that no such tableaux exist, so it does not weaken the blueprint clauses."
}