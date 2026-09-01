## TARGET DominoTilingsZ.restrictTilingLeft_isFaultfree (theorem) — ELABORATED SIGNATURE
∀ (n : ℕ) (T : DominoTilingsZ.Tiling (DominoTilingsZ.Rectangle n 2)) (k : ℕ) (hk : DominoTilingsZ.hasFault n T k),
  (∀ j < k, ¬DominoTilingsZ.hasFault n T j) → DominoTilingsZ.isFaultfree k (DominoTilingsZ.restrictTilingLeft n T k hk)

Docstring: The left restriction at a fault is faultfree if k is the smallest fault 

## PROJECT DEPENDENCY DominoTilingsZ.Tiling (inductive)
DominoTilingsZ.Shape → Type

Body:
DominoTilingsZ.Tiling.mk : {S : DominoTilingsZ.Shape} →
  (dominos : Set DominoTilingsZ.Domino) →
    dominos.PairwiseDisjoint DominoTilingsZ.Domino.toShape → ⋃ d ∈ dominos, d.toShape = S → DominoTilingsZ.Tiling S

Docstring: A domino tiling of a shape S is a set partition of S into dominos
(Definition \ref{def.domino.shapes-and-tilings}(d)) 

## PROJECT DEPENDENCY DominoTilingsZ.Rectangle (def)
ℕ → ℕ → DominoTilingsZ.Shape

Body:
fun n m => {p | 1 ≤ p.1 ∧ p.1 ≤ ↑n ∧ 1 ≤ p.2 ∧ p.2 ≤ ↑m}

Docstring: The n × m rectangle (Definition \ref{def.domino.shapes-and-tilings}(b)) 

## PROJECT DEPENDENCY DominoTilingsZ.hasFault (def)
(n : ℕ) → DominoTilingsZ.Tiling (DominoTilingsZ.Rectangle n 2) → ℕ → Prop

Body:
fun n T k =>
  k > 0 ∧
    k < n ∧
      ∀ d ∈ T.dominos,
        match d with
        | DominoTilingsZ.Domino.horizontal i j => i < ↑k ∨ i ≥ ↑k + 1
        | DominoTilingsZ.Domino.vertical i j => True

Docstring: A fault in a domino tiling is a vertical line that no domino straddles 

## PROJECT DEPENDENCY DominoTilingsZ.isFaultfree (def)
(n : ℕ) → DominoTilingsZ.Tiling (DominoTilingsZ.Rectangle n 2) → Prop

Body:
fun n T => n > 0 ∧ ∀ (k : ℕ), ¬DominoTilingsZ.hasFault n T k

Docstring: A tiling is faultfree if it is nonempty and has no fault 

## PROJECT DEPENDENCY DominoTilingsZ.restrictTilingLeft (def)
(n : ℕ) →
  (T : DominoTilingsZ.Tiling (DominoTilingsZ.Rectangle n 2)) →
    (k : ℕ) → DominoTilingsZ.hasFault n T k → DominoTilingsZ.Tiling (DominoTilingsZ.Rectangle k 2)

Body:
fun n T k hk => { dominos := {d | d ∈ T.dominos ∧ d.inLeftPart k}, pairwise_disjoint := ⋯, cover := ⋯ }

Docstring: Restrict a tiling to the left part at a fault position 

## PROJECT DEPENDENCY DominoTilingsZ.Shape (def)
Type

Body:
Set (ℤ × ℤ)

Docstring: A shape is a subset of ℤ² (Definition \ref{def.domino.shapes-and-tilings}(a)) 

## PROJECT DEPENDENCY DominoTilingsZ.Domino (inductive)
Type

Body:
DominoTilingsZ.Domino.horizontal : ℤ → ℤ → DominoTilingsZ.Domino
DominoTilingsZ.Domino.vertical : ℤ → ℤ → DominoTilingsZ.Domino

Docstring: A domino is either horizontal or vertical (Definition \ref{def.domino.shapes-and-tilings}(c)) 

## PROJECT DEPENDENCY DominoTilingsZ.Domino.toShape (def)
DominoTilingsZ.Domino → DominoTilingsZ.Shape

Body:
fun x =>
  match x with
  | DominoTilingsZ.Domino.horizontal i j => {(i, j), (i + 1, j)}
  | DominoTilingsZ.Domino.vertical i j => {(i, j), (i, j + 1)}

Docstring: The cells covered by a domino 

## PROJECT DEPENDENCY DominoTilingsZ.Tiling.dominos (def)
{S : DominoTilingsZ.Shape} → DominoTilingsZ.Tiling S → Set DominoTilingsZ.Domino

Body:
fun S self => self.1

Docstring: The set of dominos in the tiling 

## PROJECT DEPENDENCY DominoTilingsZ.Tiling.mk (constructor)
{S : DominoTilingsZ.Shape} →
  (dominos : Set DominoTilingsZ.Domino) →
    dominos.PairwiseDisjoint DominoTilingsZ.Domino.toShape → ⋃ d ∈ dominos, d.toShape = S → DominoTilingsZ.Tiling S

## PROJECT DEPENDENCY DominoTilingsZ.Domino.inLeftPart (def)
DominoTilingsZ.Domino → ℕ → Prop

Body:
fun d k => ∀ p ∈ d.toShape, p.1 ≤ ↑k

Docstring: A domino is in the left part (all x-coordinates ≤ k) 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

## BASE-LIBRARY REF LT.lt
{α : Type u} → [self : LT α] → α → α → Prop

Docstring: The less-than relation: `x < y` 

Conventions for notations in identifiers:

 * The recommended spelling of `<` in identifiers is `lt`.

## BASE-LIBRARY REF instLTNat
LT ℕ

## BASE-LIBRARY REF Not
Prop → Prop

Docstring: `Not p`, or `¬p`, is the negation of `p`. It is defined to be `p → False`,
so if your goal is `¬p` you can use `intro h` to turn the goal into
`h : p ⊢ False`, and if you have `hn : ¬p` and `h : p` then `hn h : False`
and `(hn h).elim` will prove anything.
For more information: [Propositional Logic](https://lean-lang.org/theorem_proving_in_lean4/propositions_and_proofs.html#propositional-logic)


Conventions for notations in identifiers:

 * The recommended spelling of `¬` in identifiers is `not`.

## BASE-LIBRARY REF Set
Type u → Type u

Docstring: A set is a collection of elements of some type `α`.

Although `Set` is defined as `α → Prop`, this is an implementation detail which should not be
relied on. Instead, `setOf` and membership of a set (`∈`) should be used to convert between sets
and predicates.


## BASE-LIBRARY REF Set.PairwiseDisjoint
{α : Type u_1} → {ι : Type u_4} → [inst : PartialOrder α] → [OrderBot α] → Set ι → (ι → α) → Prop

Docstring: A set is `PairwiseDisjoint` under `f`, if the images of any distinct two elements under `f`
are disjoint.

`s.Pairwise Disjoint` is (definitionally) the same as `s.PairwiseDisjoint id`. We prefer the latter
in order to allow dot notation on `Set.PairwiseDisjoint`, even though the former unfolds more
nicely. 

## BASE-LIBRARY REF ChainCompletePartialOrder.toPartialOrder
{α : Type u_2} → [self : ChainCompletePartialOrder α] → PartialOrder α

## BASE-LIBRARY REF ChainCompletePartialOrder.instOfCompleteLattice
{α : Type u_1} → [CompleteLattice α] → ChainCompletePartialOrder α

## BASE-LIBRARY REF CompleteBooleanAlgebra.toCompleteLattice
{α : Type u_1} → [self : CompleteBooleanAlgebra α] → CompleteLattice α

## BASE-LIBRARY REF CompleteAtomicBooleanAlgebra.toCompleteBooleanAlgebra
{α : Type u} → [self : CompleteAtomicBooleanAlgebra α] → CompleteBooleanAlgebra α

## BASE-LIBRARY REF Set.instCompleteAtomicBooleanAlgebra
{α : Type u_1} → CompleteAtomicBooleanAlgebra (Set α)

## BASE-LIBRARY REF Prod
Type u → Type v → Type (max u v)

Docstring: The product type, usually written `α × β`. Product types are also called pair or tuple types.
Elements of this type are pairs in which the first element is an `α` and the second element is a
`β`.

Products nest to the right, so `(x, y, z) : α × β × γ` is equivalent to `(x, (y, z)) : α × (β × γ)`.


Conventions for notations in identifiers:

 * The recommended spelling of `×` in identifiers is `Prod`.

## BASE-LIBRARY REF Int
Type

Docstring: The integers.

This type is special-cased by the compiler and overridden with an efficient implementation. The
runtime has a special representation for `Int` that stores “small” signed numbers directly, while
larger numbers use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)). A “small number” is an integer that can be encoded with one fewer bits
than the platform's pointer size (i.e. 63 bits on 64-bit architectures and 31 bits on 32-bit
architectures).


## BASE-LIBRARY REF HeytingAlgebra.toOrderBot
{α : Type u_4} → [self : HeytingAlgebra α] → OrderBot α

## BASE-LIBRARY REF Order.Frame.toHeytingAlgebra
{α : Type u_1} → [self : Order.Frame α] → HeytingAlgebra α

## BASE-LIBRARY REF CompleteDistribLattice.toFrame
{α : Type u_1} → [self : CompleteDistribLattice α] → Order.Frame α

## BASE-LIBRARY REF CompleteBooleanAlgebra.toCompleteDistribLattice
{α : Type u} → [CompleteBooleanAlgebra α] → CompleteDistribLattice α

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

## BASE-LIBRARY REF Set.iUnion
{α : Type u} → {ι : Sort v} → (ι → Set α) → Set α

Docstring: Indexed union of a family of sets 

## BASE-LIBRARY REF Membership.mem
{α : outParam (Type u)} → {γ : Type v} → [self : Membership α γ] → γ → α → Prop

Docstring: The membership relation `a ∈ s : Prop` where `a : α`, `s : γ`. 

Conventions for notations in identifiers:

 * The recommended spelling of `∈` in identifiers is `mem`.

## BASE-LIBRARY REF Set.instMembership
{α : Type u} → Membership α (Set α)

## BASE-LIBRARY REF setOf
{α : Type u} → (α → Prop) → Set α

Docstring: Turn a predicate `p : α → Prop` into a set, also written as `{x | p x}` 

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

## BASE-LIBRARY REF Int.instLEInt
LE ℤ

## BASE-LIBRARY REF instOfNat
{n : ℕ} → OfNat ℤ n

## BASE-LIBRARY REF Prod.fst
{α : Type u} → {β : Type v} → α × β → α

Docstring: The first element of a pair. 

## BASE-LIBRARY REF Nat.cast
{R : Type u} → [NatCast R] → ℕ → R

Docstring: The canonical homomorphism `Nat → R`. In most use cases, the target type will have a (semi)ring
structure, and this homomorphism should be a (semi)ring homomorphism.

`NatCast` and `IntCast` exist to allow different libraries with their own types that can be notated
as natural numbers to have consistent `simp` normal forms without needing to create coercion
simplification sets that are aware of all combinations. Libraries should make it easy to work with
`NatCast` where possible. For instance, in Mathlib there will be such a homomorphism (and thus a
`NatCast R` instance) whenever `R` is an additive monoid with a `1`.

The prototypical example is `Int.ofNat`.


## BASE-LIBRARY REF instNatCastInt
NatCast ℤ

## BASE-LIBRARY REF Prod.snd
{α : Type u} → {β : Type v} → α × β → β

Docstring: The second element of a pair. 

## BASE-LIBRARY REF GT.gt
{α : Type u} → [LT α] → α → α → Prop

Docstring: `a > b` is an abbreviation for `b < a`. 

Conventions for notations in identifiers:

 * The recommended spelling of `>` in identifiers is `gt`.

## BASE-LIBRARY REF Or
Prop → Prop → Prop

Docstring: `Or a b`, or `a ∨ b`, is the disjunction of propositions. There are two
constructors for `Or`, called `Or.inl : a → a ∨ b` and `Or.inr : b → a ∨ b`,
and you can use `match` or `cases` to destruct an `Or` assumption into the
two cases.


Conventions for notations in identifiers:

 * The recommended spelling of `∨` in identifiers is `or`.

 * The recommended spelling of `\/` in identifiers is `or` (prefer `∨` over `\/`).

## BASE-LIBRARY REF Int.instLTInt
LT ℤ

## BASE-LIBRARY REF GE.ge
{α : Type u} → [LE α] → α → α → Prop

Docstring: `a ≥ b` is an abbreviation for `b ≤ a`. 

Conventions for notations in identifiers:

 * The recommended spelling of `≥` in identifiers is `ge`.

 * The recommended spelling of `>=` in identifiers is `ge` (prefer `≥` over `>=`).

## BASE-LIBRARY REF HAdd.hAdd
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HAdd α β γ] → α → β → γ

Docstring: `a + b` computes the sum of `a` and `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `+` in identifiers is `add`.

## BASE-LIBRARY REF instHAdd
{α : Type u_1} → [Add α] → HAdd α α α

## BASE-LIBRARY REF Int.instAdd
Add ℤ

## BASE-LIBRARY REF True
Prop

Docstring: `True` is a proposition and has only an introduction rule, `True.intro : True`.
In other words, `True` is simply true, and has a canonical proof, `True.intro`
For more information: [Propositional Logic](https://lean-lang.org/theorem_proving_in_lean4/propositions_and_proofs.html#propositional-logic)


## BASE-LIBRARY REF Insert.insert
{α : outParam (Type u)} → {γ : Type v} → [self : Insert α γ] → α → γ → γ

Docstring: `insert x xs` inserts the element `x` into the collection `xs`. 

## BASE-LIBRARY REF Set.instInsert
{α : Type u} → Insert α (Set α)

## BASE-LIBRARY REF Prod.mk
{α : Type u} → {β : Type v} → α → β → α × β

Docstring: Constructs a pair. This is usually written `(x, y)` instead of `Prod.mk x y`.


Conventions for notations in identifiers:

 * The recommended spelling of `(a, b)` in identifiers is `mk`.

## BASE-LIBRARY REF Singleton.singleton
{α : outParam (Type u)} → {β : Type v} → [self : Singleton α β] → α → β

Docstring: `singleton x` is a collection with the single element `x` (notation: `{x}`). 

Conventions for notations in identifiers:

 * The recommended spelling of `{x}` in identifiers is `singleton`.

## BASE-LIBRARY REF Set.instSingletonSet
{α : Type u} → Singleton α (Set α)

## INFORMAL STATEMENT
lem.gf-ws.restrict-left-faultfree

\leanhelper  The left restriction at the \emph{minimum} fault position is faultfree. That is, if $k$ is the smallest fault of $T$ and $j < k$, then $j$ is not a fault of the restricted tiling.

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.bk-forced-free
Forced and free cells

\leanhelper  Let $T$ be a semistandard tableau and let $k < N-1$. A cell $c = (i,j)$ with $T(c) = k$ is \emph{forced} if there exists a cell $(i+1,j)$ directly below with $T(i+1,j) = k+1$. Similarly for $T(c) = k+1$ with a cell directly above having value~ $k$. Free cells are those that are not forced. 

Among the free cells, the \emph{parenthesis-matching algorithm} classifies each as \emph{matched} or \emph{unmatched}: reading free entries left-to-right in each row, each free $(k{+}1)$ matches with the nearest unmatched free $k$ to its left. Unmatched entries are those remaining after this process.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.bk-involution
Bender–Knuth involution βk

\leanhelper  Let $T$ be a semistandard tableau of shape $\lambda /\mu $ and let $k < N-1$. The \emph{Bender--Knuth involution} $\beta _k(T)$ is obtained from $T$ by swapping only the \emph{unmatched} free $k$’s and unmatched free $(k{+}1)$’s: 

\[  \beta _k(T)(c) = \begin{cases}  k+1 &  \text{if } c \text{ is an unmatched free } k, \\ k &  \text{if } c \text{ is an unmatched free } k{+}1, \\ T(c) &  \text{otherwise.} \end{cases}  \]

 Forced cells and matched free cells are left unchanged.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.bk-prefix
Prefix-restricted Bender–Knuth

\leanhelper  The \emph{prefix-restricted BK involution} $\beta _k^{<j}$ applies the parenthesis-matching swap of $k$ and $k{+}1$ only to cells in columns $< j$. Cells in columns $\geq j$ are left unchanged: 

\[  \beta _k^{<j}(T)(c) = \begin{cases}  k+1 &  \text{if the column of } c \text{ is } < j \text{ and } c \text{ is unmatched free } k \text{ in prefix}, \\ k &  \text{if the column of } c \text{ is } < j \text{ and } c \text{ is unmatched free } k{+}1 \text{ in prefix}, \\ T(c) &  \text{otherwise.} \end{cases}  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.col-tab
def.sf.col-tab

Let $\lambda $ and $\mu $ be two $N$-partitions. Let $T$ be a tableau of shape $\lambda /\mu $. Let $j$ be a positive integer. Then, $\operatorname {col}_{\geq j}T$ means the restriction of $T$ to columns $j,j+1,j+2,\ldots $ (that is, the result of removing the first $j-1$ columns from $T$). Formally speaking, this means the restriction of the map $T$ to the set $\left\{  \left( u,v\right) \in Y\left( \lambda /\mu \right) \  \mid \  v\geq j\right\}  $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.content
def.sf.content

Let $\lambda $ and $\mu $ be two $N$-partitions. Let $T$ be a tableau of shape $\lambda /\mu $. We define the \emph{content} of $T$ to be the $N$-tuple $\left( a_{1},a_{2},\ldots ,a_{N}\right) $, where

\[  a_{i}:=\left( \text{\#  of }i\text{'s in }T\right) =\left( \text{\#  of boxes }c\text{ of }T\text{ such that }T\left( c\right) =i\right) .  \]

 We denote this $N$-tuple by $\operatorname *{cont}T$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.npar
def.sf.Npar

An $N$\emph{-partition} will mean a weakly decreasing $N$-tuple of nonnegative integers. In other words, an $N$-partition means an $N$-tuple $\left( \lambda _{1},\lambda _{2},\ldots ,\lambda _{N}\right) \in \mathbb {N}^{N}$ with $\lambda _{1}\geq \lambda _{2}\geq \cdots \geq \lambda _{N}$. 

The \emph{size} (or weight) of an $N$-partition $\lambda = (\lambda _1, \lambda _2, \ldots , \lambda _N)$ is defined to be $|\lambda | := \lambda _1 + \lambda _2 + \cdots + \lambda _N$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.npar-order
def.sf.Npar-order

\leanhelper  We define a partial order on $N$-partitions by componentwise comparison: $\mu \leq \nu $ iff $\mu _i \leq \nu _i$ for all $i \in [N]$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.npar-youngdiagram
def.sf.Npar-youngDiagram

\leanhelper  The \emph{Young diagram} $Y(\lambda )$ of an $N$-partition $\lambda $ is the finite set of cells 

\[  Y(\lambda ) = \{ (i, j) : i \in [N],\;  0 \leq j < \lambda _i\} .  \]

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.ssyt
def.sf.ssyt

Let $\lambda $ be an $N$-partition. 

A Young tableau $T$ of shape $\lambda $ is said to be \emph{semistandard} if its entries 

\begin{itemize} \item increase weakly along each row (from left to right); 

\item increase strictly down each column (from top to bottom). 

\end{itemize}

Formally speaking, this means that a Young tableau $T:Y\left( \lambda \right) \rightarrow \left[ N\right] $ is semistandard if and only if 

\begin{itemize} \item we have $T\left( i,j\right) \leq T\left( i,j+1\right) $ for any $\left( i,j\right) \in Y\left( \lambda \right) $ satisfying $\left( i,j+1\right) \in Y\left( \lambda \right) $; 

\item we have $T\left( i,j\right) <T\left( i+1,j\right) $ for any $\left( i,j\right) \in Y\left( \lambda \right) $ satisfying $\left( i+1,j\right) \in Y\left( \lambda \right) $. 

\end{itemize}

We let $\operatorname *{SSYT}\left( \lambda \right) $ denote the set of all semistandard Young tableaux of shape $\lambda $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.stemb-violator-misstep
Violator columns and misstep indices

\leanhelper  Let $T$ be a semistandard tableau and $\nu $ an $N$-tuple. A positive integer $j$ is a \emph{violator column} if $\nu + \operatorname {cont}(\operatorname {col}_{\geq j} T)$ is not an $N$-partition. An index $k$ is a \emph{misstep} for an $N$-tuple $\alpha $ if $k + 1 < N$ and $\alpha _k < \alpha _{k+1}$ (i.e., the partition condition fails at~ $k$).

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.ydiag
def.sf.ydiag

Let $\lambda $ be an $N$-partition. 

The \emph{Young diagram} of $\lambda $ is defined as the set

\[  \left\{  \left( i,j\right) \  \mid \  i\in \left[ N\right] \text{ and }j\in \left[ \lambda _{i}\right] \right\}  \subseteq \left\{  1,2,3,\ldots \right\}  ^{2}.  \]

 We visually represent each element $\left( i,j\right) $ of this Young diagram as a box in row $i$ and column $j$. 

We denote the Young diagram of $\lambda $ by $Y\left( \lambda \right) $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.ytab
def.sf.ytab

Let $\lambda $ be an $N$-partition. 

A \emph{Young tableau} of shape $\lambda $ means a way of filling the boxes of $Y\left( \lambda \right) $ with elements of $\left[ N\right] $ (one element per box). Formally speaking, it is defined as a map $T:Y\left( \lambda \right) \rightarrow \left[ N\right] $.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The formal binders exactly encode that `k` is the minimum fault: `hk : DominoTilingsZ.hasFault n T k` says that `k` is a fault, while `(\u2200 j < k, \u00ac DominoTilingsZ.hasFault n T j)` says that no smaller position is a fault. The conclusion `DominoTilingsZ.isFaultfree k (DominoTilingsZ.restrictTilingLeft n T k hk)` directly states that the left restriction is faultfree. Although `isFaultfree` quantifies over every natural fault position, `hasFault k ... j` itself includes `j < k`, so positions outside the restricted rectangle's interior are automatically not faults. Its additional conjunct `k > 0` is already supplied by `hk`, since `hasFault n T k` includes `k > 0`. Thus this faithfully formalizes: \u201cThe left restriction at the minimum fault position is faultfree.\u201d"
}