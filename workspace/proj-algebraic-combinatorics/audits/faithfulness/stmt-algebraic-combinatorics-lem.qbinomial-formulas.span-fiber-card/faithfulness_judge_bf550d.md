## TARGET AlgebraicCombinatorics.QBinomialRec.spanMap_fiber_card (theorem) — ELABORATED SIGNATURE
∀ {F : Type u_1} [inst : Field F] [inst_1 : Fintype F] {V : Type u_2} [inst_2 : AddCommGroup V]
  [inst_3 : _root_.Module F V] [Module.Finite F V] (k : ℕ) (W : { W // Module.finrank F ↥W = k }),
  Nat.card { v // AlgebraicCombinatorics.QBinomialRec.spanMap k v = W } =
    ∏ i ∈ Finset.range k, (Fintype.card F ^ k - Fintype.card F ^ i)

Docstring: Key lemma for thm.pars.qbinom.subsp-count: Each k-dimensional subspace W has exactly
∏_{i=0}^{k-1} (q^k - q^i) preimages under the span map.

This is because the preimages are exactly the ordered bases of W:
- A linearly independent k-tuple v with span(v) = W must lie entirely in W
- Since W is k-dimensional and v has k linearly independent vectors, v spans W automatically
- Thus the preimages are exactly the linearly independent k-tuples in W
- By card_linearIndependent, the count is ∏_{i=0}^{k-1} (q^k - q^i)

This is the key step in the proof of qBinomial_subspace_count. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.QBinomialRec.spanMap (def)
{F : Type u_1} →
  [inst : Field F] →
    {V : Type u_2} →
      [inst_1 : AddCommGroup V] →
        [inst_2 : _root_.Module F V] → (k : ℕ) → { v // LinearIndependent F v } → { W // Module.finrank F ↥W = k }

Body:
fun {F} [Field F] {V} [AddCommGroup V] [_root_.Module F V] k x =>
  match x with
  | ⟨v, hv⟩ => ⟨Submodule.span F (Set.range v), ⋯⟩

Docstring: The span map sends a linearly independent k-tuple to its span (a k-dimensional subspace). 

## BASE-LIBRARY REF Field
Type u → Type u

Docstring: A `Field` is a `CommRing` with multiplicative inverses for nonzero elements.

An instance of `Field K` includes maps `ratCast : ℚ → K` and `qsmul : ℚ → K → K`.
Those two fields are needed to implement the `DivisionRing K → Algebra ℚ K` instance since we need
to control the specific definitions for some special cases of `K` (in particular `K = ℚ` itself).
See also note [forgetful inheritance].

If the field has positive characteristic `p`, our division by zero convention forces
`ratCast (1 / p) = 1 / 0 = 0`. 

## BASE-LIBRARY REF Fintype
Type u_4 → Type u_4

Docstring: `Fintype α` means that `α` is finite, i.e. there are only
finitely many distinct elements of type `α`. The evidence of this
is a finset `elems` (a list up to permutation without duplicates),
together with a proof that everything of type `α` is in the list. 

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

## BASE-LIBRARY REF Module.Finite
(R : Type u_1) → (M : Type u_4) → [inst : Semiring R] → [inst_1 : AddCommMonoid M] → [_root_.Module R M] → Prop

Docstring: A module over a semiring is `Module.Finite` if it is finitely generated as a module. 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF Subtype
{α : Sort u} → (α → Prop) → Sort (max 1 u)

Docstring: All the elements of a type that satisfy a predicate.

`Subtype p`, usually written `{ x : α // p x }` or `{ x // p x }`, contains all elements `x : α` for
which `p x` is true. Its constructor is a pair of the value and the proof that it satisfies the
predicate. In run-time code, `{ x : α // p x }` is represented identically to `α`.

There is a coercion from `{ x : α // p x }` to `α`, so elements of a subtype may be used where the
underlying type is expected.

Examples:
 * `{ n : Nat // n % 2 = 0 }` is the type of even numbers.
 * `{ xs : Array String // xs.size = 5 }` is the type of arrays with five `String`s.
 * Given `xs : List α`, `List { x : α // x ∈ xs }` is the type of lists in which all elements are
   contained in `xs`.


Conventions for notations in identifiers:

 * The recommended spelling of `{ x // p x }` in identifiers is `subtype`.

## BASE-LIBRARY REF Submodule
(R : Type u) → (M : Type v) → [inst : Semiring R] → [inst_1 : AddCommMonoid M] → [_root_.Module R M] → Type v

Docstring: A submodule of a module is one which is closed under vector operations.
This is a sufficient condition for the subset of vectors in the submodule
to themselves form a module. 

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

## BASE-LIBRARY REF Module.finrank
(R : Type u_1) → (M : Type u_2) → [inst : Semiring R] → [inst_1 : AddCommMonoid M] → [_root_.Module R M] → ℕ

Docstring: The rank of a module as a natural number.

For a finite-dimensional vector space `V` over a field `k`, `Module.finrank k V` is equal to
the dimension of `V` over `k`.

For a general module `M` over a ring `R`, `Module.finrank R M` is defined to be the supremum of the
cardinalities of the `R`-linearly independent subsets of `M`, if this supremum is finite. It is
defined by convention to be `0` if this supremum is infinite. See `Module.rank` for a
cardinal-valued version where infinite rank modules have rank an infinite cardinal.

Note that if `R` is not a field then there can exist modules `M` with `¬(Module.Finite R M)` but
`finrank R M ≠ 0`. For example `ℚ` has `finrank` equal to `1` over `ℤ`, because the nonempty
`ℤ`-linearly independent subsets of `ℚ` are precisely the nonzero singletons. 

## BASE-LIBRARY REF Membership.mem
{α : outParam (Type u)} → {γ : Type v} → [self : Membership α γ] → γ → α → Prop

Docstring: The membership relation `a ∈ s : Prop` where `a : α`, `s : γ`. 

Conventions for notations in identifiers:

 * The recommended spelling of `∈` in identifiers is `mem`.

## BASE-LIBRARY REF SetLike.instMembership
{A : Type u_1} → {B : Type u_2} → [i : SetLike A B] → Membership B A

## BASE-LIBRARY REF Submodule.setLike
{R : Type u} →
  {M : Type v} →
    [inst : Semiring R] → [inst_1 : AddCommMonoid M] → [inst_2 : _root_.Module R M] → SetLike (Submodule R M) M

## BASE-LIBRARY REF Submodule.addCommMonoid
{R : Type u} →
  {M : Type v} →
    [inst : Semiring R] →
      [inst_1 : AddCommMonoid M] → {module_M : _root_.Module R M} → (p : Submodule R M) → AddCommMonoid ↥p

## BASE-LIBRARY REF Submodule.module
{R : Type u} →
  {M : Type v} →
    [inst : Semiring R] →
      [inst_1 : AddCommMonoid M] → {module_M : _root_.Module R M} → (p : Submodule R M) → _root_.Module R ↥p

## BASE-LIBRARY REF Nat.card
Type u_3 → ℕ

Docstring: `Nat.card α` is the cardinality of `α` as a natural number.
If `α` is infinite, `Nat.card α = 0`. 

## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


## BASE-LIBRARY REF LinearIndependent
{ι : Type u'} →
  (R : Type u_2) →
    {M : Type u_4} → (ι → M) → [inst : Semiring R] → [inst_1 : AddCommMonoid M] → [_root_.Module R M] → Prop

Docstring: `LinearIndependent R v` states the family of vectors `v` is linearly independent over `R`. 

## BASE-LIBRARY REF Finset.prod
{ι : Type u_1} → {M : Type u_3} → [CommMonoid M] → Finset ι → (ι → M) → M

Docstring: `∏ x ∈ s, f x` is the product of `f x` as `x` ranges over the elements of the finite set `s`.

When the index type is a `Fintype`, the notation `∏ x, f x`, is a shorthand for
`∏ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF Nat.instCommMonoid
CommMonoid ℕ

## BASE-LIBRARY REF Finset.range
ℕ → Finset ℕ

Docstring: `range n` is the set of natural numbers less than `n`. 

## BASE-LIBRARY REF HSub.hSub
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HSub α β γ] → α → β → γ

Docstring: `a - b` computes the difference of `a` and `b`.
The meaning of this notation is type-dependent.
* For natural numbers, this operator saturates at 0: `a - b = 0` when `a ≤ b`. 

Conventions for notations in identifiers:

 * The recommended spelling of `-` in identifiers is `sub` (when used as a binary operator).

## BASE-LIBRARY REF instHSub
{α : Type u_1} → [Sub α] → HSub α α α

## BASE-LIBRARY REF instSubNat
Sub ℕ

## BASE-LIBRARY REF HPow.hPow
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HPow α β γ] → α → β → γ

Docstring: `a ^ b` computes `a` to the power of `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `^` in identifiers is `pow`.

## BASE-LIBRARY REF instHPow
{α : Type u_1} → {β : Type u_2} → [Pow α β] → HPow α β α

## BASE-LIBRARY REF Monoid.toNatPow
{M : Type u_2} → [Monoid M] → Pow M ℕ

## BASE-LIBRARY REF Nat.instMonoid
Monoid ℕ

## BASE-LIBRARY REF Fintype.card
(α : Type u_4) → [Fintype α] → ℕ

Docstring: `card α` is the number of elements in `α`, defined when `α` is a fintype. 

## BASE-LIBRARY REF Subtype.mk
{α : Sort u} → {p : α → Prop} → (val : α) → p val → Subtype p

## BASE-LIBRARY REF Submodule.span
(R : Type u_1) →
  {M : Type u_4} →
    [inst : Semiring R] → [inst_1 : AddCommMonoid M] → [inst_2 : _root_.Module R M] → Set M → Submodule R M

Docstring: The span of a set `s ⊆ M` is the smallest submodule of M that contains `s`. 

## BASE-LIBRARY REF Set.range
{α : Type u} → {ι : Sort u_1} → (ι → α) → Set α

Docstring: Range of a function.

This function is more flexible than `f '' univ`, as the image requires that the domain is in Type
and not an arbitrary Sort. 

## INFORMAL STATEMENT
lem.qbinomial-formulas.span-fiber-card

\leanhelper  Each $k$-dimensional subspace $W$ has exactly $\prod _{i=0}^{k-1} (|F|^k - |F|^i)$ preimages under the span map. These are precisely the ordered bases of $W$: the linearly independent $k$-tuples in $W$ that automatically span $W$ by dimension count.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.qbinomial-formulas.span-map
def.qbinomial-formulas.span-map

\leanhelper  The \emph{span map} sends a linearly independent $k$-tuple $(v_1, \ldots , v_k)$ in $V$ to its span $\mathrm{span}(v_1, \ldots , v_k)$, viewed as a $k$-dimensional subspace.

## VERDICT
{
  "verdict": "drift",
  "justification": "The blueprint quantifies over \u201cEach $k$-dimensional subspace $W$\u201d and does not require the ambient space $V$ to be finite-dimensional. The elaborated target adds the contentful binder `[Module.Finite F V]`. This excludes finite-dimensional subspaces of infinite-dimensional ambient vector spaces, even though the fiber-count formula depends only on $W$ and remains meaningful there. The target also explicitly restricts to `[Fintype F]`, whereas the supplied informal statement does not state that $F$ is finite; this is a narrowed quantifier unless finiteness is added to the blueprint. To make the declaration faithful, at minimum remove `[Module.Finite F V]`. Either the blueprint should explicitly assume that $F$ is finite, or the formal statement should be generalized from `Fintype.card F` and natural-number cardinality to an appropriate cardinal-valued formulation for arbitrary fields."
}