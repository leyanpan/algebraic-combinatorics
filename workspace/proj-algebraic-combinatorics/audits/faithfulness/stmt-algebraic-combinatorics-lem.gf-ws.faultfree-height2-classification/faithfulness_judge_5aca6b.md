## TARGET DominoTilingsZ.faultfree_height2_classification (theorem) — ELABORATED SIGNATURE
∀ (n : ℕ) (T : DominoTilingsZ.Tiling (DominoTilingsZ.Rectangle n 2)), DominoTilingsZ.isFaultfree n T → n = 1 ∨ n = 2

Docstring: The only faultfree tilings of height-2 rectangles have width 1 or 2 

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

## PROJECT DEPENDENCY DominoTilingsZ.isFaultfree (def)
(n : ℕ) → DominoTilingsZ.Tiling (DominoTilingsZ.Rectangle n 2) → Prop

Body:
fun n T => n > 0 ∧ ∀ (k : ℕ), ¬DominoTilingsZ.hasFault n T k

Docstring: A tiling is faultfree if it is nonempty and has no fault 

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

## PROJECT DEPENDENCY DominoTilingsZ.Tiling.dominos (def)
{S : DominoTilingsZ.Shape} → DominoTilingsZ.Tiling S → Set DominoTilingsZ.Domino

Body:
fun S self => self.1

Docstring: The set of dominos in the tiling 

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

## BASE-LIBRARY REF Or
Prop → Prop → Prop

Docstring: `Or a b`, or `a ∨ b`, is the disjunction of propositions. There are two
constructors for `Or`, called `Or.inl : a → a ∨ b` and `Or.inr : b → a ∨ b`,
and you can use `match` or `cases` to destruct an `Or` assumption into the
two cases.


Conventions for notations in identifiers:

 * The recommended spelling of `∨` in identifiers is `or`.

 * The recommended spelling of `\/` in identifiers is `or` (prefer `∨` over `\/`).

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

## BASE-LIBRARY REF LT.lt
{α : Type u} → [self : LT α] → α → α → Prop

Docstring: The less-than relation: `x < y` 

Conventions for notations in identifiers:

 * The recommended spelling of `<` in identifiers is `lt`.

## BASE-LIBRARY REF Int.instLTInt
LT ℤ

## BASE-LIBRARY REF GE.ge
{α : Type u} → [LE α] → α → α → Prop

Docstring: `a ≥ b` is an abbreviation for `b ≤ a`. 

Conventions for notations in identifiers:

 * The recommended spelling of `≥` in identifiers is `ge`.

 * The recommended spelling of `>=` in identifiers is `ge` (prefer `≥` over `>=`).

## BASE-LIBRARY REF True
Prop

Docstring: `True` is a proposition and has only an introduction rule, `True.intro : True`.
In other words, `True` is simply true, and has a canonical proof, `True.intro`
For more information: [Propositional Logic](https://lean-lang.org/theorem_proving_in_lean4/propositions_and_proofs.html#propositional-logic)


## INFORMAL STATEMENT
lem.gf-ws.faultfree-height2-classification

\leanhelper  The only faultfree tilings of height-$2$ rectangles have width $1$ or $2$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.domino.shapes-and-tilings
def.domino.shapes-and-tilings

\textbf{(a)} A \emph{shape} means a subset of $\mathbb {Z}^{2}$. 

We draw each $\left( i,j\right) \in \mathbb {Z}^{2}$ as a unit square with center at the point $\left( i,j\right) $ (in Cartesian coordinates); thus, a shape can be drawn as a cluster of squares. \medskip 

\textbf{(b)} For any $n,m\in \mathbb {N}$, the shape $R_{n,m}$ (called the $n\times m$\emph{-rectangle}) is defined to be

\[  \left\{  1,2,\ldots ,n\right\}  \times \left\{  1,2,\ldots ,m\right\}  =\left\{  \left( i,j\right) \in \mathbb {Z}^{2}\  \mid \  1\leq i\leq n\text{ and }1\leq j\leq m\right\}  .  \]

\textbf{(c)} A \emph{domino} means a size-$2$ shape of the form

\begin{align*} &  \left\{  \left( i,j\right) ,\  \left( i+1,j\right) \right\}  \text{ (a ``\emph{horizontal domino}'')}\  \  \  \  \  \  \  \  \  \  \text{or}\\ &  \left\{  \left( i,j\right) ,\  \left( i,j+1\right) \right\}  \text{ (a ``\emph{vertical domino}'')}\end{align*}

 for some $\left( i,j\right) \in \mathbb {Z}^{2}$. \medskip 

\textbf{(d)} A \emph{domino tiling} of a shape $S$ is a set partition of $S$ into dominos (i.e., a set of disjoint dominos whose union is $S$). \medskip 

\textbf{(e)} For any $n,m\in \mathbb {N}$, let $d_{n,m}$ be the \#  of domino tilings of $R_{n,m}$.

## VERDICT
{
  "verdict": "unclear",
  "justification": "The target states `\u2200 (n : \u2115) (T : Tiling (Rectangle n 2)), isFaultfree n T \u2192 n = 1 \u2228 n = 2`, which matches the classification\u2019s quantifier and conclusion. However, the blueprint package never defines \u201cfaultfree.\u201d The formal dependency defines it as `n > 0 \u2227 \u2200 (k : \u2115), \u00ac hasFault n T k`, with `hasFault` restricted by `k > 0 \u2227 k < n` and a specific no-horizontal-domino-straddles condition. In particular, the added conjunct `n > 0` could materially exclude the width-zero rectangle rather than merely encode notation. Without an informal definition of \u201cfault\u201d and \u201cfaultfree,\u201d it is impossible to determine whether these conditions capture the blueprint term. The package would need the blueprint\u2019s definition of faultfree tilings, including whether nonemptiness is required and which boundary lines count as faults."
}