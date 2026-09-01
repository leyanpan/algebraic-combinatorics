## TARGET AlgebraicCombinatorics.SymmetricFunctions.monomialSymm_homogeneous_linearIndependent (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_1} [inst : CommSemiring R] {N : ℕ} (n : ℕ),
  LinearIndependent R fun mu => AlgebraicCombinatorics.SymmetricFunctions.monomialSymm ↑mu

Docstring: The monomial symmetric polynomials of size n are linearly independent.
(Theorem thm.sf.m-basis (d), linear independence part)

This follows from the fact that no two m_μ share any monomials, and each m_μ
contains at least one monomial.

Label: thm.sf.m-basis.d.indep 

## TARGET AlgebraicCombinatorics.SymmetricFunctions.monomialSymm_linearIndependent (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_1} [inst : CommSemiring R] {N : ℕ} (S : Finset (AlgebraicCombinatorics.SymmetricFunctions.NPartition N)),
  LinearIndependent R fun mu => AlgebraicCombinatorics.SymmetricFunctions.monomialSymm ↑mu

Docstring: The monomial symmetric polynomials are linearly independent.
(Theorem thm.sf.m-basis (a), linear independence part)

Label: thm.sf.m-basis.a.indep 

## TARGET AlgebraicCombinatorics.SymmetricFunctions.monomialSymm_homogeneous_spans (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_1} [inst : CommSemiring R] {N : ℕ} (n : ℕ),
  ∀ f ∈ AlgebraicCombinatorics.SymmetricFunctions.symmHomogeneous N R n,
    f ∈ Submodule.span R (Set.range fun mu => AlgebraicCombinatorics.SymmetricFunctions.monomialSymm ↑mu)

Docstring: The monomial symmetric polynomials of size n span 𝒮_n.
(Theorem thm.sf.m-basis (d), spanning part)

Label: thm.sf.m-basis.d.span 

## TARGET AlgebraicCombinatorics.SymmetricFunctions.symm_eq_sum_coeff_monomialSymm (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_1} [inst : CommSemiring R] {N : ℕ} (f : MvPolynomial (Fin N) R),
  f.IsSymmetric →
    ∀ (S : Finset (AlgebraicCombinatorics.SymmetricFunctions.NPartition N)),
      (∀ (mu : AlgebraicCombinatorics.SymmetricFunctions.NPartition N), NPartition.size mu ≤ f.totalDegree → mu ∈ S) →
        f =
          ∑ mu ∈ S,
            MvPolynomial.coeff (Finsupp.equivFunOnFinite.symm mu.parts) f •
              AlgebraicCombinatorics.SymmetricFunctions.monomialSymm mu

Docstring: Any symmetric polynomial f can be written as
f = ∑_μ ([x₁^{μ₁} x₂^{μ₂} ⋯ x_N^{μ_N}] f) m_μ
(Theorem thm.sf.m-basis (b))

Label: thm.sf.m-basis.b 

## TARGET AlgebraicCombinatorics.SymmetricFunctions.monomialSymm_basis_homogeneous (def) — ELABORATED SIGNATURE
{R : Type u_1} →
  [inst : CommSemiring R] →
    {N : ℕ} →
      (n : ℕ) →
        Module.Basis { nu // NPartition.size nu = n } R
          ↥(AlgebraicCombinatorics.SymmetricFunctions.symmHomogeneous N R n)

Body:
fun {R} [CommSemiring R] {N} n =>
  let v := AlgebraicCombinatorics.SymmetricFunctions.monomialSymmRestricted✝ n;
  have hli := ⋯;
  have hsp := ⋯;
  Module.Basis.mk hli hsp

Docstring: The monomial symmetric polynomials of size n form a basis of 𝒮_n.
(Theorem thm.sf.m-basis (d))

This combines linear independence (`monomialSymm_homogeneous_linearIndependent`)
and spanning (`monomialSymm_homogeneous_spans`).

Label: thm.sf.m-basis.d 

## TARGET AlgebraicCombinatorics.SymmetricFunctions.monomialSymm_spans (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_1} [inst : CommSemiring R] {N : ℕ} (f : MvPolynomial (Fin N) R),
  f.IsSymmetric → f ∈ Submodule.span R (Set.range fun mu => AlgebraicCombinatorics.SymmetricFunctions.monomialSymm mu)

Docstring: The monomial symmetric polynomials span the symmetric polynomials.
(Theorem thm.sf.m-basis (a), spanning part)

The proof proceeds by:
1. Writing f as a sum of monomials grouped by their sort
2. For symmetric f, all monomials with the same sort have the same coefficient
3. Factoring out the common coefficient from each group
4. Showing that the sum of monomials in each group equals monomialSymm μ

Label: thm.sf.m-basis.a.span 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SymmetricFunctions.NPartition (def)
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

## PROJECT DEPENDENCY NPartition.size (def)
{N : ℕ} → NPartition N → ℕ

Body:
fun {N} μ => ∑ i, μ.parts i

Docstring: The size (or weight) of an N-partition is the sum of its entries.
If μ = (μ₁, μ₂, ..., μ_N), then |μ| = μ₁ + μ₂ + ... + μ_N. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SymmetricFunctions.monomialSymm (def)
{R : Type u_1} →
  [inst : CommSemiring R] → {N : ℕ} → AlgebraicCombinatorics.SymmetricFunctions.NPartition N → MvPolynomial (Fin N) R

Body:
fun {R} [CommSemiring R] {N} mu =>
  ∑ a ∈ AlgebraicCombinatorics.SymmetricFunctions.sortPreimage mu,
    AlgebraicCombinatorics.SymmetricFunctions.monomialExp a

Docstring: The monomial symmetric polynomial m_μ corresponding to an N-partition μ.
(Definition def.sf.m)

m_μ = ∑_{a ∈ ℕ^N : sort(a) = μ} x^a

This is the sum of all monomials whose exponent tuple sorts to μ. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SymmetricFunctions.symmHomogeneous (def)
(N : ℕ) → (R : Type u_2) → [inst : CommSemiring R] → ℕ → Submodule R (MvPolynomial (Fin N) R)

Body:
fun N R [CommSemiring R] n =>
  { carrier := {f | f.IsSymmetric ∧ f.IsHomogeneous n}, add_mem' := ⋯, zero_mem' := ⋯, smul_mem' := ⋯ }

Docstring: The submodule of homogeneous symmetric polynomials of degree n.
(Theorem thm.sf.m-basis (c))

𝒮_n = {homogeneous symmetric polynomials of degree n}

Label: thm.sf.m-basis.c 

## PROJECT DEPENDENCY NPartition.parts (def)
{N : ℕ} → NPartition N → Fin N → ℕ

Body:
fun N self => self.1

Docstring: The entries of the N-partition as a function from `Fin N` to `ℕ` 

## PROJECT DEPENDENCY _private.AlgebraicCombinatorics.SymmetricFunctions.MonomialSymmetric.0.AlgebraicCombinatorics.SymmetricFunctions.monomialSymmRestricted (def)
{R : Type u_1} →
  [inst : CommSemiring R] →
    {N : ℕ} →
      (n : ℕ) → { nu // NPartition.size nu = n } → ↥(AlgebraicCombinatorics.SymmetricFunctions.symmHomogeneous N R n)

Body:
fun {R} [CommSemiring R] {N} n mu => ⟨AlgebraicCombinatorics.SymmetricFunctions.monomialSymm ↑mu, ⋯⟩

Docstring: The function that maps N-partitions of size n into the submodule of homogeneous 
symmetric polynomials of degree n. 

## PROJECT DEPENDENCY NPartition (inductive)
ℕ → Type

Body:
NPartition.mk : {N : ℕ} → (parts : Fin N → ℕ) → Antitone parts → NPartition N

Docstring: An N-partition is a weakly decreasing N-tuple of nonnegative integers.
(Definition def.sf.Npar)

This is represented as a function `Fin N → ℕ` that is antitone
(i.e., `i ≤ j → parts j ≤ parts i`).

The field is named `antitone` to match Mathlib conventions. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SymmetricFunctions.sortPreimage (def)
{N : ℕ} → AlgebraicCombinatorics.SymmetricFunctions.NPartition N → Finset (Fin N → ℕ)

Body:
fun {N} mu =>
  {a ∈ Fintype.piFinset fun x => Finset.range (NPartition.size mu + 1) |
    AlgebraicCombinatorics.SymmetricFunctions.sortTuple a = mu}

Docstring: The set of tuples a ∈ ℕ^N with sort(a) = μ and entries bounded by μ.size.
This is a finite set since entries are bounded. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SymmetricFunctions.monomialExp (def)
{R : Type u_1} → [inst : CommSemiring R] → {N : ℕ} → (Fin N → ℕ) → MvPolynomial (Fin N) R

Body:
fun {R} [CommSemiring R] {N} a => ∏ i, MvPolynomial.X i ^ a i

Docstring: The monomial x^a = x₁^{a₁} x₂^{a₂} ⋯ x_N^{a_N} for a tuple a ∈ ℕ^N.
(Definition def.sf.sort (a)) 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SymmetricFunctions.sortTuple (def)
{N : ℕ} → (Fin N → ℕ) → AlgebraicCombinatorics.SymmetricFunctions.NPartition N

Body:
fun {N} a =>
  {
    parts := fun i =>
      have sorted := (Multiset.map a Finset.univ.val).sort fun x1 x2 => x1 ≥ x2;
      if h : ↑i < sorted.length then sorted.get ⟨↑i, h⟩ else 0,
    antitone := ⋯ }

Docstring: Sort a tuple in weakly decreasing order to get an N-partition.
(Definition def.sf.sort (b)) 

## PROJECT DEPENDENCY NPartition.instDecidableEq (def)
{N : ℕ} → DecidableEq (NPartition N)

Body:
fun {N} μ ν => decidable_of_iff (μ.parts = ν.parts) ⋯

Docstring: Decidable equality for N-partitions. 

## PROJECT DEPENDENCY NPartition.mk (constructor)
{N : ℕ} → (parts : Fin N → ℕ) → Antitone parts → NPartition N

## BASE-LIBRARY REF CommSemiring
Type u → Type u

Docstring: A commutative semiring is a semiring with commutative multiplication. 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF LinearIndependent
{ι : Type u'} →
  (R : Type u_2) →
    {M : Type u_4} → (ι → M) → [inst : Semiring R] → [inst_1 : AddCommMonoid M] → [_root_.Module R M] → Prop

Docstring: `LinearIndependent R v` states the family of vectors `v` is linearly independent over `R`. 

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

## BASE-LIBRARY REF MvPolynomial
Type u_1 → (R : Type u_2) → [CommSemiring R] → Type (max u_2 u_1)

Docstring: Multivariate polynomial, where `σ` is the index set of the variables and
`R` is the coefficient ring 

## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


## BASE-LIBRARY REF Subtype.val
{α : Sort u} → {p : α → Prop} → Subtype p → α

Docstring: The value in the underlying type that satisfies the predicate.


## BASE-LIBRARY REF CommSemiring.toSemiring
{R : Type u} → [self : CommSemiring R] → Semiring R

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.toAddCommMonoid
{α : Type u} → [self : NonUnitalNonAssocSemiring α] → AddCommMonoid α

## BASE-LIBRARY REF NonAssocSemiring.toNonUnitalNonAssocSemiring
{α : Type u} → [self : NonAssocSemiring α] → NonUnitalNonAssocSemiring α

## BASE-LIBRARY REF Semiring.toNonAssocSemiring
{α : Type u} → [self : Semiring α] → NonAssocSemiring α

## BASE-LIBRARY REF MvPolynomial.commSemiring
{R : Type u} → {σ : Type u_1} → [inst : CommSemiring R] → CommSemiring (MvPolynomial σ R)

## BASE-LIBRARY REF MvPolynomial.module
{R : Type u} →
  {S₁ : Type v} →
    {σ : Type u_1} →
      [inst : Semiring R] → [inst_1 : CommSemiring S₁] → [_root_.Module R S₁] → _root_.Module R (MvPolynomial σ S₁)

## BASE-LIBRARY REF Semiring.toModule
{R : Type u_1} → [inst : Semiring R] → _root_.Module R R

## BASE-LIBRARY REF Finset
Type u_4 → Type u_4

Docstring: `Finset α` is the type of finite sets of elements of `α`. It is implemented
as a multiset (a list up to permutation) which has no duplicate elements. 

## BASE-LIBRARY REF Membership.mem
{α : outParam (Type u)} → {γ : Type v} → [self : Membership α γ] → γ → α → Prop

Docstring: The membership relation `a ∈ s : Prop` where `a : α`, `s : γ`. 

Conventions for notations in identifiers:

 * The recommended spelling of `∈` in identifiers is `mem`.

## BASE-LIBRARY REF SetLike.instMembership
{A : Type u_1} → {B : Type u_2} → [i : SetLike A B] → Membership B A

## BASE-LIBRARY REF Finset.instSetLike
{α : Type u_1} → SetLike (Finset α) α

Docstring: Convert a finset to a set in the natural way. 

## BASE-LIBRARY REF Submodule
(R : Type u) → (M : Type v) → [inst : Semiring R] → [inst_1 : AddCommMonoid M] → [_root_.Module R M] → Type v

Docstring: A submodule of a module is one which is closed under vector operations.
This is a sufficient condition for the subset of vectors in the submodule
to themselves form a module. 

## BASE-LIBRARY REF Submodule.setLike
{R : Type u} →
  {M : Type v} →
    [inst : Semiring R] → [inst_1 : AddCommMonoid M] → [inst_2 : _root_.Module R M] → SetLike (Submodule R M) M

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

## BASE-LIBRARY REF MvPolynomial.IsSymmetric
{σ : Type u_1} → {R : Type u_3} → [inst : CommSemiring R] → MvPolynomial σ R → Prop

Docstring: A `MvPolynomial φ` is symmetric if it is invariant under
permutations of its variables by the `rename` operation 

## BASE-LIBRARY REF LE.le
{α : Type u} → [self : LE α] → α → α → Prop

Docstring: The less-equal relation: `x ≤ y` 

Conventions for notations in identifiers:

 * The recommended spelling of `≤` in identifiers is `le`.

 * The recommended spelling of `<=` in identifiers is `le` (prefer `≤` over `<=`).

## BASE-LIBRARY REF instLENat
LE ℕ

## BASE-LIBRARY REF MvPolynomial.totalDegree
{R : Type u} → {σ : Type u_1} → [inst : CommSemiring R] → MvPolynomial σ R → ℕ

Docstring: `totalDegree p` gives the maximum |s| over the monomials X^s in `p` 

## BASE-LIBRARY REF Finset.instMembership
{α : Type u_1} → Membership α (Finset α)

## BASE-LIBRARY REF Finset.sum
{ι : Type u_1} → {M : Type u_3} → [AddCommMonoid M] → Finset ι → (ι → M) → M

Docstring: `∑ x ∈ s, f x` is the sum of `f x` as `x` ranges over the elements
of the finite set `s`.

When the index type is a `Fintype`, the notation `∑ x, f x`, is a shorthand for
`∑ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF HSMul.hSMul
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HSMul α β γ] → α → β → γ

Docstring: `a • b` computes the product of `a` and `b`.
The meaning of this notation is type-dependent, but it is intended to be used for left actions. 

Conventions for notations in identifiers:

 * The recommended spelling of `•` in identifiers is `smul`.

## BASE-LIBRARY REF instHSMul
{α : Type u_1} → {β : Type u_2} → [SMul α β] → HSMul α β β

## BASE-LIBRARY REF Algebra.toSMul
{R : Type u} → {A : Type v} → {inst : CommSemiring R} → {inst_1 : Semiring A} → [self : Algebra R A] → SMul R A

## BASE-LIBRARY REF MvPolynomial.algebra
{R : Type u} →
  {S₁ : Type v} →
    {σ : Type u_1} →
      [inst : CommSemiring R] → [inst_1 : CommSemiring S₁] → [Algebra R S₁] → Algebra R (MvPolynomial σ S₁)

## BASE-LIBRARY REF Algebra.id
(R : Type u) → [inst : CommSemiring R] → Algebra R R

Docstring: The identity map inducing an `Algebra` structure. 

## BASE-LIBRARY REF MvPolynomial.coeff
{R : Type u} → {σ : Type u_1} → [inst : CommSemiring R] → (σ →₀ ℕ) → MvPolynomial σ R → R

Docstring: The coefficient of the monomial `m` in the multi-variable polynomial `p`. 

## BASE-LIBRARY REF DFunLike.coe
{F : Sort u_1} → {α : outParam (Sort u_2)} → {β : outParam (α → Sort u_3)} → [self : DFunLike F α β] → F → (a : α) → β a

Docstring: The coercion from `F` to a function. 

## BASE-LIBRARY REF Equiv
Sort u_1 → Sort u_2 → Sort (max (max 1 u_1) u_2)

Docstring: `α ≃ β` is the type of functions from `α → β` with a two-sided inverse. 

## BASE-LIBRARY REF Finsupp
Type u_9 → (M : Type u_10) → [Zero M] → Type (max u_10 u_9)

Docstring: `Finsupp α M`, denoted `α →₀ M`, is the type of functions `f : α → M` such that
`f x = 0` for all but finitely many `x`. 

## BASE-LIBRARY REF MulZeroClass.toZero
{M₀ : Type u} → [self : MulZeroClass M₀] → Zero M₀

## BASE-LIBRARY REF Nat.instMulZeroClass
MulZeroClass ℕ

## BASE-LIBRARY REF EquivLike.toFunLike
{E : Sort u_1} → {α : Sort u_3} → {β : Sort u_4} → [EquivLike E α β] → FunLike E α β

## BASE-LIBRARY REF Equiv.instEquivLike
{α : Sort u} → {β : Sort v} → EquivLike (α ≃ β) α β

## BASE-LIBRARY REF Equiv.symm
{α : Sort u} → {β : Sort v} → α ≃ β → β ≃ α

Docstring: Inverse of an equivalence `e : α ≃ β`. 

## BASE-LIBRARY REF Finsupp.equivFunOnFinite
{α : Type u_1} → {M : Type u_4} → [inst : Zero M] → [Finite α] → (α →₀ M) ≃ (α → M)

Docstring: Given `Finite α`, `equivFunOnFinite` is the `Equiv` between `α →₀ β` and `α → β`.
(All functions on a finite type are finitely supported.) 

## BASE-LIBRARY REF Finite.of_fintype
∀ (α : Type u_4) [Fintype α], Finite α

Docstring: For efficiency reasons, we want `Finite` instances to have higher
priority than ones coming from `Fintype` instances. 

## BASE-LIBRARY REF Fin.fintype
(n : ℕ) → Fintype (Fin n)

## BASE-LIBRARY REF Module.Basis
Type u_1 →
  (R : Type u_3) →
    (M : Type u_6) →
      [inst : Semiring R] → [inst_1 : AddCommMonoid M] → [_root_.Module R M] → Type (max (max u_1 u_3) u_6)

Docstring: A `Basis ι R M` for a module `M` is the type of `ι`-indexed `R`-bases of `M`.

The basis vectors are available as `DFunLike.coe (b : Basis ι R M) : ι → M`.
To turn a linear independent family of vectors spanning `M` into a basis, use `Basis.mk`.
They are internally represented as linear equivs `M ≃ₗ[R] (ι →₀ R)`,
available as `Basis.repr`.


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

## BASE-LIBRARY REF Preorder.toLE
{α : Type u_2} → [self : Preorder α] → LE α

## BASE-LIBRARY REF PartialOrder.toPreorder
{α : Type u_2} → [self : PartialOrder α] → Preorder α

## BASE-LIBRARY REF Submodule.instPartialOrder
{R : Type u} →
  {M : Type v} →
    [inst : Semiring R] → [inst_1 : AddCommMonoid M] → [inst_2 : _root_.Module R M] → PartialOrder (Submodule R M)

## BASE-LIBRARY REF Top.top
{α : Type u_1} → [self : Top α] → α

Docstring: The top (`⊤`, `\top`) element 

Conventions for notations in identifiers:

 * The recommended spelling of `⊤` in identifiers is `top`.

## BASE-LIBRARY REF Submodule.instTop
{R : Type u_1} →
  {M : Type u_3} → [inst : Semiring R] → [inst_1 : AddCommMonoid M] → [inst_2 : _root_.Module R M] → Top (Submodule R M)

Docstring: The universal set is the top element of the lattice of submodules. 

## BASE-LIBRARY REF Module.Basis.mk
{ι : Type u_1} →
  {R : Type u_3} →
    {M : Type u_5} →
      [inst : Semiring R] →
        [inst_1 : AddCommMonoid M] →
          [inst_2 : _root_.Module R M] →
            {v : ι → M} → LinearIndependent R v → ⊤ ≤ Submodule.span R (Set.range v) → Module.Basis ι R M

Docstring: A linear independent family of vectors spanning the whole module is a basis. 

## BASE-LIBRARY REF Nat.instAddCommMonoid
AddCommMonoid ℕ

## BASE-LIBRARY REF Finset.univ
{α : Type u_1} → [Fintype α] → Finset α

Docstring: `univ` is the universal finite set of type `Finset α` implied from
the assumption `Fintype α`. 

## BASE-LIBRARY REF Submodule.mk
{R : Type u} →
  {M : Type v} →
    [inst : Semiring R] →
      [inst_1 : AddCommMonoid M] →
        [inst_2 : _root_.Module R M] →
          (toAddSubmonoid : AddSubmonoid M) →
            (∀ (c : R) {x : M}, x ∈ toAddSubmonoid.carrier → c • x ∈ toAddSubmonoid.carrier) → Submodule R M

## BASE-LIBRARY REF AddSubmonoid.mk
{M : Type u_3} →
  [inst : AddZeroClass M] → (toAddSubsemigroup : AddSubsemigroup M) → 0 ∈ toAddSubsemigroup.carrier → AddSubmonoid M

## BASE-LIBRARY REF AddMonoid.toAddZeroClass
{M : Type u} → [self : AddMonoid M] → AddZeroClass M

## BASE-LIBRARY REF AddCommMonoid.toAddMonoid
{M : Type u} → [self : AddCommMonoid M] → AddMonoid M

## BASE-LIBRARY REF AddSubsemigroup.mk
{M : Type u_3} →
  [inst : Add M] → (carrier : Set M) → (∀ {a b : M}, a ∈ carrier → b ∈ carrier → a + b ∈ carrier) → AddSubsemigroup M

## BASE-LIBRARY REF AddZero.toAdd
{M : Type u_2} → [self : AddZero M] → Add M

## BASE-LIBRARY REF AddZeroClass.toAddZero
{M : Type u} → [self : AddZeroClass M] → AddZero M

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

## BASE-LIBRARY REF MvPolynomial.IsHomogeneous
{σ : Type u_1} → {R : Type u_3} → [inst : CommSemiring R] → MvPolynomial σ R → ℕ → Prop

Docstring: A multivariate polynomial `φ` is homogeneous of degree `n`
if all monomials occurring in `φ` have degree `n`. 

## BASE-LIBRARY REF Subtype.mk
{α : Sort u} → {p : α → Prop} → (val : α) → p val → Subtype p

## BASE-LIBRARY REF Antitone
{α : Type u} → {β : Type v} → [Preorder α] → [Preorder β] → (α → β) → Prop

Docstring: A function `f` is antitone if `a ≤ b` implies `f b ≤ f a`. 

## BASE-LIBRARY REF Fin.instPartialOrder
{n : ℕ} → PartialOrder (Fin n)

## BASE-LIBRARY REF Nat.instPreorder
Preorder ℕ

## BASE-LIBRARY REF Finset.filter
{α : Type u_1} → (p : α → Prop) → [DecidablePred p] → Finset α → Finset α

Docstring: `Finset.filter p s` is the set of elements of `s` that satisfy `p`.

For example, one can use `s.filter (· ∈ t)` to get the intersection of `s` with `t : Set α`
as a `Finset α` (when a `DecidablePred (· ∈ t)` instance is available). 

## BASE-LIBRARY REF Fintype.piFinset
{α : Type u_1} → [DecidableEq α] → [Fintype α] → {δ : α → Type u_4} → ((a : α) → Finset (δ a)) → Finset ((a : α) → δ a)

Docstring: Given for all `a : α` a finset `t a` of `δ a`, then one can define the
finset `Fintype.piFinset t` of all functions taking values in `t a` for all `a`. This is the
analogue of `Finset.pi` where the base finset is `univ` (but formally they are not the same, as
there is an additional condition `i ∈ Finset.univ` in the `Finset.pi` definition). 

## BASE-LIBRARY REF instDecidableEqFin
(n : ℕ) → DecidableEq (Fin n)

## BASE-LIBRARY REF Finset.range
ℕ → Finset ℕ

Docstring: `range n` is the set of natural numbers less than `n`. 

## BASE-LIBRARY REF HAdd.hAdd
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HAdd α β γ] → α → β → γ

Docstring: `a + b` computes the sum of `a` and `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `+` in identifiers is `add`.

## BASE-LIBRARY REF instHAdd
{α : Type u_1} → [Add α] → HAdd α α α

## BASE-LIBRARY REF instAddNat
Add ℕ

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

## BASE-LIBRARY REF Finset.prod
{ι : Type u_1} → {M : Type u_3} → [CommMonoid M] → Finset ι → (ι → M) → M

Docstring: `∏ x ∈ s, f x` is the product of `f x` as `x` ranges over the elements of the finite set `s`.

When the index type is a `Fintype`, the notation `∏ x, f x`, is a shorthand for
`∏ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF CommSemiring.toCommMonoid
{R : Type u} → [self : CommSemiring R] → CommMonoid R

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

## BASE-LIBRARY REF MonoidWithZero.toMonoid
{M₀ : Type u} → [self : MonoidWithZero M₀] → Monoid M₀

## BASE-LIBRARY REF Semiring.toMonoidWithZero
{α : Type u} → [self : Semiring α] → MonoidWithZero α

## BASE-LIBRARY REF MvPolynomial.X
{R : Type u} → {σ : Type u_1} → [inst : CommSemiring R] → σ → MvPolynomial σ R

Docstring: `X n` is the degree `1` monomial $X_n$. 

## BASE-LIBRARY REF List
Type u → Type u

Docstring: Linked lists: ordered lists, in which each element has a reference to the next element.

Most operations on linked lists take time proportional to the length of the list, because each
element must be traversed to find the next element.

`List α` is isomorphic to `Array α`, but they are useful for different things:
* `List α` is easier for reasoning, and `Array α` is modeled as a wrapper around `List α`.
* `List α` works well as a persistent data structure, when many copies of the tail are shared. When
  the value is not shared, `Array α` will have better performance because it can do destructive
  updates.


## BASE-LIBRARY REF Multiset.sort
{α : Type u_1} →
  Multiset α →
    (r : autoParam (α → α → Prop) Multiset.sort._auto_1) →
      [DecidableRel r] → [IsTrans α r] → [Std.Antisymm r] → [Std.Total r] → List α

Docstring: `sort s` constructs a sorted list from the multiset `s`.
(Uses merge sort algorithm.) 

## BASE-LIBRARY REF Multiset.map
{α : Type u_1} → {β : Type v} → (α → β) → Multiset α → Multiset β

Docstring: `map f s` is the lift of the list `map` operation. The multiplicity
of `b` in `map f s` is the number of `a ∈ s` (counting multiplicity)
such that `f a = b`. 

## BASE-LIBRARY REF Finset.val
{α : Type u_4} → Finset α → Multiset α

Docstring: The underlying multiset 

## BASE-LIBRARY REF GE.ge
{α : Type u} → [LE α] → α → α → Prop

Docstring: `a ≥ b` is an abbreviation for `b ≤ a`. 

Conventions for notations in identifiers:

 * The recommended spelling of `≥` in identifiers is `ge`.

 * The recommended spelling of `>=` in identifiers is `ge` (prefer `≥` over `>=`).

## BASE-LIBRARY REF Nat.decLe
(n m : ℕ) → Decidable (n ≤ m)

Docstring: A decision procedure for non-strict inequality of natural numbers, usually accessed via the
`DecidableLE Nat` instance.

Examples:
 * `(if 3 ≤ 4 then "yes" else "no") = "yes"`
 * `(if 6 ≤ 4 then "yes" else "no") = "no"`
 * `show 12 ≤ 12 by decide`
 * `show 5 ≤ 12 by decide`


## BASE-LIBRARY REF instIsTransGe
∀ {α : Type u} [inst : Preorder α], IsTrans α fun x1 x2 => x2 ≤ x1

## BASE-LIBRARY REF instAntisymmGe
∀ {α : Type u} [inst : PartialOrder α], Std.Antisymm fun x1 x2 => x2 ≤ x1

## BASE-LIBRARY REF Nat.instPartialOrder
PartialOrder ℕ

## BASE-LIBRARY REF LE.total'
∀ {α : Type u} [inst : LinearOrder α], Std.Total fun x1 x2 => x2 ≤ x1

## BASE-LIBRARY REF Nat.instLinearOrder
LinearOrder ℕ

## BASE-LIBRARY REF dite
{α : Sort u} → (c : Prop) → [h : Decidable c] → (c → α) → (¬c → α) → α

Docstring: "Dependent" if-then-else, normally written via the notation `if h : c then t(h) else e(h)`,
is sugar for `dite c (fun h => t(h)) (fun h => e(h))`, and it is the same as
`if c then t else e` except that `t` is allowed to depend on a proof `h : c`,
and `e` can depend on `h : ¬c`. (Both branches use the same name for the hypothesis,
even though it has different types in the two cases.)

We use this to be able to communicate the if-then-else condition to the branches.
For example, `Array.get arr i h` expects a proof `h : i < arr.size` in order to
avoid a bounds check, so you can write `if h : i < arr.size then arr.get i h else ...`
to avoid the bounds check inside the if branch. (Of course in this case we have only
lifted the check into an explicit `if`, but we could also use this proof multiple times
or derive `i < arr.size` from some other proposition that we are checking in the `if`.)


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


## BASE-LIBRARY REF List.length
{α : Type u_1} → List α → ℕ

Docstring: The length of a list.

This function is overridden in the compiler to `lengthTR`, which uses constant stack space.

Examples:
* `([] : List String).length = 0`
* `["green", "brown"].length = 2`


## BASE-LIBRARY REF Nat.decLt
(n m : ℕ) → Decidable (n < m)

Docstring: A decision procedure for strict inequality of natural numbers, usually accessed via the
`DecidableLT Nat` instance.

Examples:
 * `(if 3 < 4 then "yes" else "no") = "yes"`
 * `(if 4 < 4 then "yes" else "no") = "no"`
 * `(if 6 < 4 then "yes" else "no") = "no"`
 * `show 5 < 12 by decide`


## BASE-LIBRARY REF List.get
{α : Type u} → (as : List α) → Fin as.length → α

Docstring: Returns the element at the provided index, counting from `0`.

In other words, for `i : Fin as.length`, `as.get i` returns the `i`'th element of the list `as`.
Because the index is a `Fin` bounded by the list's length, the index will never be out of bounds.

Examples:
 * `["spring", "summer", "fall", "winter"].get (2 : Fin 4) = "fall"`
 * `["spring", "summer", "fall", "winter"].get (0 : Fin 4) = "spring"`


## BASE-LIBRARY REF Fin.mk
{n : ℕ} → (val : ℕ) → val < n → Fin n

Docstring: Creates a `Fin n` from `i : Nat` and a proof that `i < n`. 

## BASE-LIBRARY REF Not
Prop → Prop

Docstring: `Not p`, or `¬p`, is the negation of `p`. It is defined to be `p → False`,
so if your goal is `¬p` you can use `intro h` to turn the goal into
`h : p ⊢ False`, and if you have `hn : ¬p` and `h : p` then `hn h : False`
and `(hn h).elim` will prove anything.
For more information: [Propositional Logic](https://lean-lang.org/theorem_proving_in_lean4/propositions_and_proofs.html#propositional-logic)


Conventions for notations in identifiers:

 * The recommended spelling of `¬` in identifiers is `not`.

## BASE-LIBRARY REF DecidableEq
Sort u → Sort (max 1 u)

Docstring: Propositional equality is `Decidable` for all elements of a type.

In other words, an instance of `DecidableEq α` is a means of deciding the proposition `a = b` is
for all `a b : α`.


## BASE-LIBRARY REF decidable_of_iff
{b : Prop} → (a : Prop) → (a ↔ b) → [Decidable a] → Decidable b

Docstring: Transfer decidability of `a` to decidability of `b`, if the propositions are equivalent.
**Important**: this function should be used instead of `rw` on `Decidable b`, because the
kernel will get stuck reducing the usage of `propext` otherwise,
and `decide` will not work. 

## BASE-LIBRARY REF Fintype.decidablePiFintype
{α : Type u_5} → {β : α → Type u_4} → [(a : α) → DecidableEq (β a)] → [Fintype α] → DecidableEq ((a : α) → β a)

## BASE-LIBRARY REF instDecidableEqNat
DecidableEq ℕ

## INFORMAL STATEMENT
thm.sf.m-basis

\textbf{(a)} The family $\left( m_{\lambda }\right) _{\lambda \text{ is an }N\text{-partition}}$ is a basis of the $K$-module $\mathcal{S}$. 

\textbf{(b)} Each symmetric polynomial $f\in \mathcal{S}$ satisfies

\[  f=\sum _{\substack {\lambda =\left( \lambda _{1},\lambda _{2},\ldots ,\lambda _{N}\right) \\ \text{is an }N\text{-partition}}}\left( \left[ x_{1}^{\lambda _{1}}x_{2}^{\lambda _{2}}\cdots x_{N}^{\lambda _{N}}\right] f\right) m_{\lambda }.  \]

\textbf{(c)} Let $n\in \mathbb {N}$. Let

\[  \mathcal{S}_{n}:=\left\{  \text{homogeneous symmetric polynomials }f\in \mathcal{P}\text{ of degree }n\right\}   \]

 (where we understand the zero polynomial $0\in \mathcal{P}$ to be homogeneous of every degree). Then, $\mathcal{S}_{n}$ is a $K$-submodule of $\mathcal{S}$. 

\textbf{(d)} The family $\left( m_{\lambda }\right) _{\lambda \text{ is an }N\text{-partition of size }n}$ is a basis of the $K$-module $\mathcal{S}_{n}$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-conv.sf.kn
conv.sf.KN

Fix a commutative ring $K$. Fix an $N\in \mathbb {N}$. Throughout this chapter, we will keep $K$ and $N$ fixed. Let $S_N$ denote the symmetric group, i.e., the group of all permutations of $[N] := \{ 1,2,\ldots ,N\} $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.alg.commring
def.alg.commring

A \emph{commutative ring} means a set $K$ equipped with three maps

\begin{align*}  \oplus &  :K\times K\rightarrow K,\\ \ominus &  :K\times K\rightarrow K,\\ \odot &  :K\times K\rightarrow K \end{align*}

 and two elements $\mathbf{0}\in K$ and $\mathbf{1}\in K$ satisfying the following axioms: 

\begin{enumerate} \item \emph{Commutativity of addition:} We have $a\oplus b=b\oplus a$ for all $a,b\in K$. 

\item \emph{Associativity of addition:} We have $a\oplus \left( b\oplus c\right) =\left( a\oplus b\right) \oplus c$ for all $a,b,c\in K$. 

\item \emph{Neutrality of zero:} We have $a\oplus \mathbf{0}=\mathbf{0}\oplus a=a$ for all $a\in K$. 

\item \emph{Subtraction undoes addition:} Let $a,b,c\in K$. We have $a\oplus b=c$ if and only if $a=c\ominus b$. 

\item \emph{Commutativity of multiplication:} We have $a\odot b=b\odot a$ for all $a,b\in K$. 

\item \emph{Associativity of multiplication:} We have $a\odot \left( b\odot c\right) =\left( a\odot b\right) \odot c$ for all $a,b,c\in K$. 

\item \emph{Distributivity:} We have

\[  a\odot \left( b\oplus c\right) =\left( a\odot b\right) \oplus \left( a\odot c\right) \  \  \  \  \  \  \  \  \  \  \text{and}\  \  \  \  \  \  \  \  \  \  \left( a\oplus b\right) \odot c=\left( a\odot c\right) \oplus \left( b\odot c\right)  \]

 for all $a,b,c\in K$. 

\item \emph{Neutrality of one:} We have $a\odot \mathbf{1}=\mathbf{1}\odot a=a$ for all $a\in K$. 

\item \emph{Annihilation:} We have $a\odot \mathbf{0}=\mathbf{0}\odot a=\mathbf{0}$ for all $a\in K$. 

\end{enumerate}

The operations $\oplus $, $\ominus $ and $\odot $ are called the \emph{addition}, the \emph{subtraction} and the \emph{multiplication} of the ring $K$. When confusion is unlikely, we will denote these three operations $\oplus $, $\ominus $ and $\odot $ by $+$, $-$ and $\cdot $, respectively, and we will abbreviate $a\odot b=a\cdot b$ by $ab$. 

The elements $\mathbf{0}$ and $\mathbf{1}$ are called the \emph{zero} and the \emph{unity} (or the \emph{one}) of the ring $K$. We will simply call these elements $0$ and $1$ when confusion with the corresponding numbers is unlikely. 

We will use \emph{PEMDAS conventions} for the three operations $\oplus $, $\ominus $ and $\odot $. These imply that the operation $\odot $ has higher precedence than $\oplus $ and $\ominus $, while the operations $\oplus $ and $\ominus $ are left-associative.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.alg.module
def.alg.module

Let $K$ be a commutative ring. 

A $K$\emph{-module} means a set $M$ equipped with three maps 

\begin{align*}  \oplus &  :M\times M\rightarrow M,\\ \ominus &  :M\times M\rightarrow M,\\ \rightharpoonup &  :K\times M\rightarrow M \end{align*}

 (notice that the third map has domain $K\times M$, not $M\times M$) and an element $\overrightarrow {0}\in M$ satisfying the following axioms: 

\begin{enumerate} \item \emph{Commutativity of addition:} We have $a\oplus b=b\oplus a$ for all $a,b\in M$. 

\item \emph{Associativity of addition:} We have $a\oplus \left( b\oplus c\right) =\left( a\oplus b\right) \oplus c$ for all $a,b,c\in M$. 

\item \emph{Neutrality of zero:} We have $a\oplus \overrightarrow {0}=\overrightarrow {0}\oplus a=a$ for all $a\in M$. 

\item \emph{Subtraction undoes addition:} Let $a,b,c\in M$. We have $a\oplus b=c$ if and only if $a=c\ominus b$. 

\item \emph{Associativity of scaling:} We have $u\rightharpoonup \left( v\rightharpoonup a\right) =\left( uv\right) \rightharpoonup a$ for all $u,v\in K$ and $a\in M$. 

\item \emph{Left distributivity:} We have $u\rightharpoonup \left( a\oplus b\right) =\left( u\rightharpoonup a\right) \oplus \left( u\rightharpoonup b\right) $ for all $u\in K$ and $a,b\in M$. 

\item \emph{Right distributivity:} We have $\left( u+v\right) \rightharpoonup a=\left( u\rightharpoonup a\right) \oplus \left( v\rightharpoonup a\right) $ for all $u,v\in K$ and $a\in M$. 

\item \emph{Neutrality of one:} We have $1\rightharpoonup a=a$ for all $a\in M$. 

\item \emph{Left annihilation:} We have $0\rightharpoonup a=\overrightarrow {0}$ for all $a\in M$. 

\item \emph{Right annihilation:} We have $u\rightharpoonup \overrightarrow {0}=\overrightarrow {0}$ for all $u\in K$. 

\end{enumerate}

The operations $\oplus $, $\ominus $ and $\rightharpoonup $ are called the \emph{addition}, the \emph{subtraction} and the \emph{scaling} (or the $K$\emph{-action}) of the $K$-module $M$. When confusion is unlikely, we will denote these three operations $\oplus $, $\ominus $ and $\rightharpoonup $ by $+$, $-$ and $\cdot $, respectively, and we will abbreviate $a\rightharpoonup b=a\cdot b$ by $ab$. 

The element $\overrightarrow {0}$ is called the \emph{zero} (or the \emph{zero vector}) of the $K$-module $M$. We will usually just call it $0$. 

When $M$ is a $K$-module, the elements of $M$ are called \emph{vectors}, while the elements of $K$ are called \emph{scalars}. 

We will use \emph{PEMDAS conventions} for the three operations $\oplus $, $\ominus $ and $\rightharpoonup $, with the operation $\rightharpoonup $ having higher precedence than $\oplus $ and $\ominus $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.perm
def.perm.perm

Let $X$ be a set. 

\textbf{(a)} A \emph{permutation} of $X$ means a bijection from $X$ to $X$. 

\textbf{(b)} It is known that the set of all permutations of $X$ is a group under composition. This group is called the \emph{symmetric group} of $X$, and is denoted by $S_X$. Its neutral element is the identity map $\operatorname {id}_X : X \to X$. Its size is $|X|!$ when $X$ is finite. 

\textbf{(c)} As usual in group theory, we will write $\alpha \beta $ for the composition $\alpha \circ \beta $ when $\alpha , \beta \in S_X$. This is the map that sends each $x \in X$ to $\alpha (\beta (x))$. 

\textbf{(d)} If $\alpha \in S_X$ and $i \in \mathbb {Z}$, then $\alpha ^i$ shall denote the $i$-th power of $\alpha $ in the group $S_X$. Note that $\alpha ^i = \underbrace{\alpha \circ \alpha \circ \cdots \circ \alpha }_{i\text{ times}}$ if $i \ge 0$. Also, $\alpha ^0 = \operatorname {id}_X$. Also, $\alpha ^{-1}$ is the inverse of $\alpha $ in the group $S_X$, that is, the inverse of the map $\alpha $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.sn-iven
def.perm.Sn-iven

Let $n \in \mathbb {Z}$. Then, $[n]$ shall mean the set $\{ 1, 2, \ldots , n\} $. This is an $n$-element set if $n \ge 0$, and is an empty set if $n \le 0$. 

The symmetric group $S_{[n]}$ (consisting of all permutations of $[n]$) will be denoted $S_n$ and called the $n$\emph{-th symmetric group}. Its size is $n!$ (when $n \ge 0$).

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.m
def.sf.m

Let $\lambda $ be any $N$-partition. Then, we define a symmetric polynomial $m_{\lambda }\in \mathcal{S}$ by

\[  m_{\lambda }:=\sum _{\substack {a\in \mathbb {N}^{N};\\ \operatorname *{sort}a=\lambda }}x^{a}.  \]

 This is called the \emph{monomial symmetric polynomial corresponding to }$\lambda $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.monomial
def.sf.monomial

\textbf{(a)} A \emph{monomial} is an expression of the form $x_1^{a_1} x_2^{a_2} \cdots x_N^{a_N}$ with $a_1, a_2, \ldots , a_N \in \mathbb {N}$. \medskip 

\textbf{(b)} The \emph{degree} $\deg \mathfrak {m}$ of a monomial $\mathfrak {m} = x_1^{a_1} x_2^{a_2} \cdots x_N^{a_N}$ is defined to be $a_1 + a_2 + \cdots + a_N \in \mathbb {N}$. \medskip 

\textbf{(c)} A monomial $\mathfrak {m} = x_1^{a_1} x_2^{a_2} \cdots x_N^{a_N}$ is said to be \emph{squarefree} if $a_1, a_2, \ldots , a_N \in \{ 0,1\} $. (This is saying that no square or higher power of an indeterminate appears in $\mathfrak {m}$; thus the name “squarefree”.) \medskip 

\textbf{(d)} A monomial $\mathfrak {m} = x_1^{a_1} x_2^{a_2} \cdots x_N^{a_N}$ is said to be \emph{primal} if there is at most one $i \in [N]$ satisfying $a_i > 0$. (This is saying that the monomial $\mathfrak {m}$ contains no two distinct indeterminates. Thus, a primal monomial is just $1$ or a power of an indeterminate.)

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.npar
def.sf.Npar

An $N$\emph{-partition} will mean a weakly decreasing $N$-tuple of nonnegative integers. In other words, an $N$-partition means an $N$-tuple $\left( \lambda _{1},\lambda _{2},\ldots ,\lambda _{N}\right) \in \mathbb {N}^{N}$ with $\lambda _{1}\geq \lambda _{2}\geq \cdots \geq \lambda _{N}$. 

The \emph{size} (or weight) of an $N$-partition $\lambda = (\lambda _1, \lambda _2, \ldots , \lambda _N)$ is defined to be $|\lambda | := \lambda _1 + \lambda _2 + \cdots + \lambda _N$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.ps
def.sf.PS

\textbf{(a)} Let $\mathcal{P}$ be the polynomial ring $K[x_1, x_2, \ldots , x_N]$ in $N$ variables over $K$. This is not just a ring; it is a commutative $K$-algebra. \medskip 

\textbf{(b)} The symmetric group $S_N$ acts on the set $\mathcal{P}$ according to the formula 

\[  \sigma \cdot f = f[x_{\sigma (1)}, x_{\sigma (2)}, \ldots , x_{\sigma (N)}] \quad \text{for any } \sigma \in S_N \text{ and any } f \in \mathcal{P}.  \]

 Here, $f[a_1, a_2, \ldots , a_N]$ means the result of substituting $a_1, a_2, \ldots , a_N$ for the indeterminates $x_1, x_2, \ldots , x_N$ in a polynomial $f \in \mathcal{P}$. 

Roughly speaking, the group $S_N$ is thus acting on $\mathcal{P}$ by permuting variables: A permutation $\sigma \in S_N$ transforms a polynomial $f$ by substituting $x_{\sigma (i)}$ for each $x_i$. 

Note that this action of $S_N$ on $\mathcal{P}$ is a well-defined group action (as we will see in Proposition~ \ref{prop.sf.SN-acts} below). \medskip 

\textbf{(c)} A polynomial $f \in \mathcal{P}$ is said to be \emph{symmetric} if it satisfies 

\[  \sigma \cdot f = f \quad \text{for all } \sigma \in S_N.  \]

\textbf{(d)} We let $\mathcal{S}$ be the set of all symmetric polynomials $f \in \mathcal{P}$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.sort
def.sf.sort

Let $a=\left( a_{1},a_{2},\ldots ,a_{N}\right) \in \mathbb {N}^{N}$. Then: 

\textbf{(a)} We let $x^{a}$ denote the monomial $x_{1}^{a_{1}}x_{2}^{a_{2}}\cdots x_{N}^{a_{N}}$. 

\textbf{(b)} We let $\operatorname *{sort}a$ mean the $N$-partition obtained from $a$ by sorting the entries of $a$ in weakly decreasing order.

## VERDICT
{
  "verdict": "faithful",
  "justification": "Taken together, the declarations formalize all four parts. For (a), `monomialSymm_linearIndependent` quantifies over every finite `S : Finset (\u2026NPartition N)` and gives linear independence of the corresponding restricted family; since linear relations are finitely supported, this yields independence of the full family. `monomialSymm_spans` states that every `f` satisfying `f.IsSymmetric` lies in the span of `Set.range fun mu => monomialSymm mu`. These are exactly the independence and spanning components of the claimed basis. For (b), `symm_eq_sum_coeff_monomialSymm` gives the stated coefficient expansion, with `MvPolynomial.coeff (Finsupp.equivFunOnFinite.symm mu.parts) f` representing `[x\u2081^{\u03bc\u2081}\u22efx_N^{\u03bc_N}]f`; the finite set `S` is required to contain every partition with `NPartition.size mu \u2264 f.totalDegree`, so omitted terms necessarily have zero coefficient, while any extra terms also have zero coefficient. For (c), `symmHomogeneous N R n` has carrier `{f | f.IsSymmetric \u2227 f.IsHomogeneous n}` and is constructed as a `Submodule`, matching `\ud835\udcae_n`; Mathlib's `IsHomogeneous` includes the zero polynomial as homogeneous in every degree. For (d), `monomialSymm_basis_homogeneous n` is explicitly a `Module.Basis {nu // NPartition.size nu = n} R \u21a5(symmHomogeneous N R n)`, with vectors supplied by `monomialSymmRestricted`, exactly indexing the basis by size-`n` partitions. The formal binder `[CommSemiring R]` is weaker than the blueprint's fixed commutative-ring assumption, so it is a faithful generalization rather than an added restriction: every commutative ring is a commutative semiring."
}