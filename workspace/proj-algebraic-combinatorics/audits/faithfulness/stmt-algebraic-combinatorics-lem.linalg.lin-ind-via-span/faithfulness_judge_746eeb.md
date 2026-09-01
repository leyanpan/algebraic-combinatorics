## TARGET AlgebraicCombinatorics.QBinomialRec.linearIndependent_iff_not_mem_span_of_lt (theorem) — ELABORATED SIGNATURE
∀ {F : Type u_1} [inst : Field F] {V : Type u_2} [inst_1 : AddCommGroup V] [inst_2 : _root_.Module F V] {k : ℕ}
  (v : Fin k → V), LinearIndependent F v ↔ ∀ (i : Fin k), v i ∉ Submodule.span F (v '' {j | ↑j < ↑i})

Docstring: Lemma lem.linalg.lin-ind-via-span: A k-tuple (v₁, v₂, ..., vₖ) is linearly independent
if and only if each vᵢ ∉ span{v₁, ..., vᵢ₋₁}.

This is the inductive characterization of linear independence. 

## BASE-LIBRARY REF Field
Type u → Type u

Docstring: A `Field` is a `CommRing` with multiplicative inverses for nonzero elements.

An instance of `Field K` includes maps `ratCast : ℚ → K` and `qsmul : ℚ → K → K`.
Those two fields are needed to implement the `DivisionRing K → Algebra ℚ K` instance since we need
to control the specific definitions for some special cases of `K` (in particular `K = ℚ` itself).
See also note [forgetful inheritance].

If the field has positive characteristic `p`, our division by zero convention forces
`ratCast (1 / p) = 1 / 0 = 0`. 

## BASE-LIBRARY REF AddCommGroup
Type u → Type u

Docstring: An additive commutative group is an additive group with commutative `(+)`. 

## BASE-LIBRARY REF Module
(R : Type u) → (M : Type v) → [Semiring R] → [AddCommMonoid M] → Type (max u v)

Docstring: A module is a generalization of vector spaces to a scalar semiring.
It consists of a scalar semiring `R` and an additive monoid of "vectors" `M`,
connected by a "scalar multiplication" operation `r • x : M`
(where `r : R` and `x : M`) with some natural associativity and
distributivity axioms similar to those on a ring. 

## BASE-LIBRARY REF DivisionSemiring.toSemiring
{K : Type u_2} → [self : DivisionSemiring K] → Semiring K

## BASE-LIBRARY REF Semifield.toDivisionSemiring
{K : Type u_2} → [self : Semifield K] → DivisionSemiring K

## BASE-LIBRARY REF Field.toSemifield
{K : Type u_1} → [Field K] → Semifield K

## BASE-LIBRARY REF AddCommGroup.toAddCommMonoid
{G : Type u} → [self : AddCommGroup G] → AddCommMonoid G

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


## BASE-LIBRARY REF Iff
Prop → Prop → Prop

Docstring: If and only if, or logical bi-implication. `a ↔ b` means that `a` implies `b` and vice versa.
By `propext`, this implies that `a` and `b` are equal and hence any expression involving `a`
is equivalent to the corresponding expression with `b` instead.


Conventions for notations in identifiers:

 * The recommended spelling of `↔` in identifiers is `iff`.

 * The recommended spelling of `<->` in identifiers is `iff` (prefer `↔` over `<->`).

## BASE-LIBRARY REF LinearIndependent
{ι : Type u'} →
  (R : Type u_2) →
    {M : Type u_4} → (ι → M) → [inst : Semiring R] → [inst_1 : AddCommMonoid M] → [_root_.Module R M] → Prop

Docstring: `LinearIndependent R v` states the family of vectors `v` is linearly independent over `R`. 

## BASE-LIBRARY REF Not
Prop → Prop

Docstring: `Not p`, or `¬p`, is the negation of `p`. It is defined to be `p → False`,
so if your goal is `¬p` you can use `intro h` to turn the goal into
`h : p ⊢ False`, and if you have `hn : ¬p` and `h : p` then `hn h : False`
and `(hn h).elim` will prove anything.
For more information: [Propositional Logic](https://lean-lang.org/theorem_proving_in_lean4/propositions_and_proofs.html#propositional-logic)


Conventions for notations in identifiers:

 * The recommended spelling of `¬` in identifiers is `not`.

## BASE-LIBRARY REF Membership.mem
{α : outParam (Type u)} → {γ : Type v} → [self : Membership α γ] → γ → α → Prop

Docstring: The membership relation `a ∈ s : Prop` where `a : α`, `s : γ`. 

Conventions for notations in identifiers:

 * The recommended spelling of `∈` in identifiers is `mem`.

## BASE-LIBRARY REF Submodule
(R : Type u) → (M : Type v) → [inst : Semiring R] → [inst_1 : AddCommMonoid M] → [_root_.Module R M] → Type v

Docstring: A submodule of a module is one which is closed under vector operations.
This is a sufficient condition for the subset of vectors in the submodule
to themselves form a module. 

## BASE-LIBRARY REF SetLike.instMembership
{A : Type u_1} → {B : Type u_2} → [i : SetLike A B] → Membership B A

## BASE-LIBRARY REF Submodule.setLike
{R : Type u} →
  {M : Type v} →
    [inst : Semiring R] → [inst_1 : AddCommMonoid M] → [inst_2 : _root_.Module R M] → SetLike (Submodule R M) M

## BASE-LIBRARY REF Submodule.span
(R : Type u_1) →
  {M : Type u_4} →
    [inst : Semiring R] → [inst_1 : AddCommMonoid M] → [inst_2 : _root_.Module R M] → Set M → Submodule R M

Docstring: The span of a set `s ⊆ M` is the smallest submodule of M that contains `s`. 

## BASE-LIBRARY REF Set.image
{α : Type u} → {β : Type v} → (α → β) → Set α → Set β

Docstring: The image of `s : Set α` by `f : α → β`, written `f '' s`, is the set of `b : β` such that
`f a = b` for some `a ∈ s`. 

## BASE-LIBRARY REF setOf
{α : Type u} → (α → Prop) → Set α

Docstring: Turn a predicate `p : α → Prop` into a set, also written as `{x | p x}` 

## BASE-LIBRARY REF LT.lt
{α : Type u} → [self : LT α] → α → α → Prop

Docstring: The less-than relation: `x < y` 

Conventions for notations in identifiers:

 * The recommended spelling of `<` in identifiers is `lt`.

## BASE-LIBRARY REF instLTNat
LT ℕ

## BASE-LIBRARY REF Fin.val
{n : ℕ} → Fin n → ℕ

Docstring: The number that is strictly less than `n`.

`Fin.val` is a coercion, so any `Fin n` can be used in a position where a `Nat` is expected.


## INFORMAL STATEMENT
lem.linalg.lin-ind-via-span

Let $F$ be a field. Let $V$ be an $F$-vector space. Let $\left( v_{1},v_{2},\ldots ,v_{k}\right) $ be a $k$-tuple of vectors in $V$. Then, $\left( v_{1},v_{2},\ldots ,v_{k}\right) $ is linearly independent if and only if each $i\in \left\{  1,2,\ldots ,k\right\}  $ satisfies $v_{i}\notin \operatorname {span}\left( v_{1},v_{2},\ldots ,v_{i-1}\right) $ (where the span $\operatorname {span}\left( {}\right) $ of an empty list is understood to be the set $\left\{  \mathbf{0}\right\}  $ consisting only of the zero vector $\mathbf{0}$). In other words, $\left( v_{1},v_{2},\ldots ,v_{k}\right) $ is linearly independent if and only if we have 

\begin{align*}  v_{1} &  \notin \underbrace{\operatorname {span}\left( {}\right) }_{=\left\{  \mathbf{0}\right\}  }\  \  \  \  \  \  \  \  \  \  \text{and}\\ v_{2} &  \notin \operatorname {span}\left( v_{1}\right) \  \  \  \  \  \  \  \  \  \  \text{and}\\ v_{3} &  \notin \operatorname {span}\left( v_{1},v_{2}\right) \  \  \  \  \  \  \  \  \  \  \text{and}\\ &  \cdots \  \  \  \  \  \  \  \  \  \  \text{and}\\ v_{k} &  \notin \operatorname {span}\left( v_{1},v_{2},\ldots ,v_{k-1}\right) . \end{align*}

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.qbinomial-formulas.span-map
def.qbinomial-formulas.span-map

\leanhelper  The \emph{span map} sends a linearly independent $k$-tuple $(v_1, \ldots , v_k)$ in $V$ to its span $\mathrm{span}(v_1, \ldots , v_k)$, viewed as a $k$-dimensional subspace.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The formal binders `{F : Type u_1} [Field F] {V : Type u_2} [AddCommGroup V] [Module F V] {k : \u2115} (v : Fin k \u2192 V)` faithfully encode a field, an F-vector space, and a k-tuple. The equivalence `LinearIndependent F v \u2194 \u2200 (i : Fin k), v i \u2209 Submodule.span F (v '' {j | \u2191j < \u2191i})` exactly matches the blueprint\u2019s claim that the tuple is linearly independent iff every `v_i` is outside the span of its predecessors. The use of `Fin k` merely changes from the blueprint\u2019s one-based indexing to zero-based indexing: `{j | \u2191j < \u2191i}` is precisely the set of earlier indices. For the first index this set is empty, and `Submodule.span F \u2205` is the zero submodule, corresponding to the stated convention that the empty span is `{0}`. No mathematically substantive hypothesis or restriction has been added."
}