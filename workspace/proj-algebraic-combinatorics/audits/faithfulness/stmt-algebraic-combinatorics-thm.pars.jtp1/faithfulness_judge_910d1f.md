## TARGET AlgebraicCombinatorics.jacobi_triple_product_fps' (theorem) — ELABORATED SIGNATURE
AlgebraicCombinatorics.jacobiLHS' = AlgebraicCombinatorics.jacobiRHS'

Docstring: **Jacobi's Triple Product Identity** (Theorem \ref{thm.pars.jtp1})

In the ring (ℤ[z^±])[[q]], we have:
  ∏_{n>0} ((1 + q^{2n-1}z)(1 + q^{2n-1}z^{-1})(1 - q^{2n})) = ∑_{ℓ∈ℤ} q^{ℓ²} z^ℓ

This is the main form of Jacobi's triple product identity, stated in the ring
JacobiRing = (ℤ[z^±])[[q]] = PowerSeries (LaurentPolynomial ℤ).

The left-hand side `jacobiLHS'` is the infinite product defined using:
- `jacobiZ` = T(1), the indeterminate z
- `jacobiZInv` = T(-1), the inverse z⁻¹
- `jacobiProductTerm n` = (1 + q^{2n+1}z)(1 + q^{2n+1}z⁻¹)(1 - q^{2(n+1)})

The right-hand side `jacobiRHS'` is the infinite sum:
- `jacobiSumTerm ℓ` = q^{ℓ²} z^ℓ

**Note**: The identity is stated in the specific ring JacobiRing with:
- q = X (the power series indeterminate)
- z = T(1) (the Laurent polynomial indeterminate)

A parameterized version `jacobiLHS q z` for arbitrary q, z would be mathematically
ill-formed because z⁻¹ does not exist for arbitrary z. The identity only makes
sense when z is invertible, which is the case in JacobiRing where z = T(1).

The proof uses Borcherds' approach via states and energy/particle number,
as implemented in the State infrastructure above.


## PROJECT DEPENDENCY AlgebraicCombinatorics.JacobiRing (def)
Type

Body:
PowerSeries (LaurentPolynomial ℤ)

Docstring: The ring (ℤ[z^±])[[q]] for Jacobi's triple product identity.
This is the ring of formal power series in q with coefficients that are
Laurent polynomials in z over ℤ. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.jacobiLHS' (def)
AlgebraicCombinatorics.JacobiRing

Body:
∏' (n : ℕ), AlgebraicCombinatorics.jacobiProductTerm n

Docstring: The left-hand side of Jacobi's triple product identity in JacobiRing:
  ∏_{n>0} ((1 + q^{2n-1}z)(1 + q^{2n-1}z^{-1})(1 - q^{2n}))

This is defined as an infinite product using the discrete topology on LaurentPolynomial ℤ
and the product topology on PowerSeries. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.jacobiRHS' (def)
AlgebraicCombinatorics.JacobiRing

Body:
∑' (ell : ℤ), AlgebraicCombinatorics.jacobiSumTerm ell

Docstring: The right-hand side of Jacobi's triple product identity in JacobiRing:
  ∑_{ℓ∈ℤ} q^{ℓ²} z^ℓ

This is defined as an infinite sum over ℤ. The sum is well-defined because
the exponent ℓ² grows quadratically, so only finitely many terms contribute
to each coefficient of q. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.jacobiProductTerm (def)
ℕ → AlgebraicCombinatorics.JacobiRing

Body:
fun n =>
  AlgebraicCombinatorics.jacobiFactorZ n * AlgebraicCombinatorics.jacobiFactorZInv n *
    AlgebraicCombinatorics.jacobiFactorQ n

Docstring: A single term in Jacobi's product:
  (1 + q^{2n-1}z)(1 + q^{2n-1}z^{-1})(1 - q^{2n})
indexed starting from n = 0 (corresponding to n = 1 in the mathematical formula). 

## PROJECT DEPENDENCY AlgebraicCombinatorics.jacobiSumTerm (def)
ℤ → AlgebraicCombinatorics.JacobiRing

Body:
fun ell => PowerSeries.X ^ ell.natAbs ^ 2 * AlgebraicCombinatorics.jacobiZPow ell

Docstring: A single term q^{ℓ²} z^ℓ in Jacobi's sum. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.jacobiFactorZ (def)
ℕ → AlgebraicCombinatorics.JacobiRing

Body:
fun n => 1 + PowerSeries.X ^ (2 * n + 1) * AlgebraicCombinatorics.jacobiZ

Docstring: The factor (1 + q^{2n-1}z) in Jacobi's product, for n ≥ 1.
Here we index by n starting from 0, so the exponent is 2n+1. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.jacobiFactorZInv (def)
ℕ → AlgebraicCombinatorics.JacobiRing

Body:
fun n => 1 + PowerSeries.X ^ (2 * n + 1) * AlgebraicCombinatorics.jacobiZInv

Docstring: The factor (1 + q^{2n-1}z^{-1}) in Jacobi's product. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.jacobiFactorQ (def)
ℕ → AlgebraicCombinatorics.JacobiRing

Body:
fun n => 1 - PowerSeries.X ^ (2 * (n + 1))

Docstring: The factor (1 - q^{2n}) in Jacobi's product.
Here we index by n starting from 0, so the exponent is 2(n+1). 

## PROJECT DEPENDENCY AlgebraicCombinatorics.jacobiZPow (def)
ℤ → AlgebraicCombinatorics.JacobiRing

Body:
fun ell => PowerSeries.C (LaurentPolynomial.T ell)

Docstring: z^ℓ for any integer ℓ, as a constant power series. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.jacobiZ (def)
AlgebraicCombinatorics.JacobiRing

Body:
PowerSeries.C (LaurentPolynomial.T 1)

Docstring: The Laurent polynomial variable z, viewed as a constant power series in JacobiRing.
This represents z = T(1) where T is the Laurent polynomial basis element. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.jacobiZInv (def)
AlgebraicCombinatorics.JacobiRing

Body:
PowerSeries.C (LaurentPolynomial.T (-1))

Docstring: The inverse z^{-1} = T(-1) as a constant power series. 

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

## BASE-LIBRARY REF PowerSeries
Type u_1 → Type (max u_1 0)

Docstring: Formal power series over a coefficient type `R` 

## BASE-LIBRARY REF LaurentPolynomial
(R : Type u_3) → [Semiring R] → Type u_3

Docstring: The semiring of Laurent polynomials with coefficients in the semiring `R`.
We denote it by `R[T;T⁻¹]`.
The ring homomorphism `C : R →+* R[T;T⁻¹]` includes `R` as the constant polynomials. 

## BASE-LIBRARY REF Int
Type

Docstring: The integers.

This type is special-cased by the compiler and overridden with an efficient implementation. The
runtime has a special representation for `Int` that stores “small” signed numbers directly, while
larger numbers use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)). A “small number” is an integer that can be encoded with one fewer bits
than the platform's pointer size (i.e. 63 bits on 64-bit architectures and 31 bits on 32-bit
architectures).


## BASE-LIBRARY REF Int.instSemiring
Semiring ℤ

## BASE-LIBRARY REF tprod
{α : Type u_4} →
  {β : Type u_5} →
    [CommMonoid α] → [TopologicalSpace α] → (β → α) → optParam (SummationFilter β) (SummationFilter.unconditional β) → α

Docstring: `∏' i, f i` is the unconditional product of `f`, if it exists, or 1 otherwise.

More generally, if `L` is a `SummationFilter`, `∏'[L] i, f i` is the product of `f` with respect to
`L` if it exists, and `1` otherwise.

(Note that even if the unconditional product exists, it might not be unique if the topology is not
separated. When the multiplicative support of `f` is finite, we make the most reasonable choice,
to use the product over the multiplicative support. Otherwise, we choose arbitrarily an `a`
satisfying `HasProd f a`. Similar remarks apply to more general summation filters.) 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF CommRing.toCommMonoid
{α : Type u} → [self : CommRing α] → CommMonoid α

## BASE-LIBRARY REF PowerSeries.instCommRing
{R : Type u_1} → [CommRing R] → CommRing (PowerSeries R)

## BASE-LIBRARY REF AddMonoidAlgebra.commRing
{R : Type u_1} → {M : Type u_4} → [inst : CommRing R] → [AddCommMonoid M] → CommRing (AddMonoidAlgebra R M)

## BASE-LIBRARY REF Int.instCommRing
CommRing ℤ

## BASE-LIBRARY REF Int.instAddCommMonoid
AddCommMonoid ℤ

## BASE-LIBRARY REF PowerSeries.WithPiTopology.instTopologicalSpace
(R : Type u_1) → [TopologicalSpace R] → TopologicalSpace (PowerSeries R)

Docstring: The pointwise topology on `PowerSeries` 

## BASE-LIBRARY REF Bot.bot
{α : Type u_1} → [self : Bot α] → α

Docstring: The bot (`⊥`, `\bot`) element 

Conventions for notations in identifiers:

 * The recommended spelling of `⊥` in identifiers is `bot`.

## BASE-LIBRARY REF TopologicalSpace
Type u → Type u

Docstring: A topology on `X`. 

## BASE-LIBRARY REF OrderBot.toBot
{α : Type u} → {inst : LE α} → [self : OrderBot α] → Bot α

## BASE-LIBRARY REF Preorder.toLE
{α : Type u_2} → [self : Preorder α] → LE α

## BASE-LIBRARY REF PartialOrder.toPreorder
{α : Type u_2} → [self : PartialOrder α] → Preorder α

## BASE-LIBRARY REF SemilatticeSup.toPartialOrder
{α : Type u} → [self : SemilatticeSup α] → PartialOrder α

## BASE-LIBRARY REF Lattice.toSemilatticeSup
{α : Type u} → [self : Lattice α] → SemilatticeSup α

## BASE-LIBRARY REF CompleteLattice.toLattice
{α : Type u_8} → [self : CompleteLattice α] → Lattice α

## BASE-LIBRARY REF TopologicalSpace.instCompleteLattice
{α : Type u} → CompleteLattice (TopologicalSpace α)

Docstring: Topologies on `α` form a complete lattice, with `⊥` the discrete topology
and `⊤` the indiscrete topology. The infimum of a collection of topologies
is the topology generated by all their open sets, while the supremum is the
topology whose open sets are those sets open in every member of the collection. 

## BASE-LIBRARY REF BoundedOrder.toOrderBot
{α : Type u} → {inst : LE α} → [self : BoundedOrder α] → OrderBot α

## BASE-LIBRARY REF CompleteLattice.toBoundedOrder
{α : Type u_8} → [self : CompleteLattice α] → BoundedOrder α

## BASE-LIBRARY REF SummationFilter.unconditional
(β : Type u_2) → SummationFilter β

Docstring: **Unconditional summation**: a function on `β` is said to be *unconditionally summable* if its
partial sums over finite subsets converge with respect to the `atTop` filter. 

## BASE-LIBRARY REF tsum
{α : Type u_4} →
  {β : Type u_5} →
    [AddCommMonoid α] →
      [TopologicalSpace α] → (β → α) → optParam (SummationFilter β) (SummationFilter.unconditional β) → α

Docstring: `∑' i, f i` is the unconditional sum of `f` if it exists, or 0 otherwise.

More generally, if `L` is a `SummationFilter`, `∑'[L] i, f i` is the sum of `f` with respect to
`L` if it exists, and `0` otherwise.

(Note that even if the unconditional sum exists, it might not be unique if the topology is not
separated. When the support of `f` is finite, we make the most reasonable choice, to use the sum
over the support. Otherwise, we choose arbitrarily an `a` satisfying `HasSum f a`. Similar remarks
apply to more general summation filters.)


## BASE-LIBRARY REF PowerSeries.instAddCommMonoid
{R : Type u_1} → [AddCommMonoid R] → AddCommMonoid (PowerSeries R)

## BASE-LIBRARY REF AddMonoidAlgebra.addAddCommMonoid
{R : Type u_1} → {M : Type u_4} → [inst : Semiring R] → AddCommMonoid (AddMonoidAlgebra R M)

## BASE-LIBRARY REF HMul.hMul
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HMul α β γ] → α → β → γ

Docstring: `a * b` computes the product of `a` and `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `*` in identifiers is `mul`.

## BASE-LIBRARY REF instHMul
{α : Type u_1} → [Mul α] → HMul α α α

## BASE-LIBRARY REF MvPowerSeries.instMul
{σ : Type u_1} → {R : Type u_2} → [Semiring R] → Mul (MvPowerSeries σ R)

## BASE-LIBRARY REF Unit
Type

Docstring: The canonical type with one element. This element is written `()`.

`Unit` has a number of uses:
* It can be used to model control flow that returns from a function call without providing other
  information.
* Monadic actions that return `Unit` have side effects without computing values.
* In polymorphic types, it can be used to indicate that no data is to be stored in a particular
  field.


## BASE-LIBRARY REF AddMonoidAlgebra.semiring
{R : Type u_1} → {M : Type u_4} → [inst : Semiring R] → [AddMonoid M] → Semiring (AddMonoidAlgebra R M)

## BASE-LIBRARY REF Int.instAddMonoid
AddMonoid ℤ

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

## BASE-LIBRARY REF PowerSeries.instSemiring
{R : Type u_1} → [Semiring R] → Semiring (PowerSeries R)

## BASE-LIBRARY REF PowerSeries.X
{R : Type u_1} → [Semiring R] → PowerSeries R

Docstring: The variable of the formal power series ring. 

## BASE-LIBRARY REF Nat.instMonoid
Monoid ℕ

## BASE-LIBRARY REF Int.natAbs
ℤ → ℕ

Docstring: The absolute value of an integer is its distance from `0`.

This function is overridden by the compiler with an efficient implementation. This definition is
the logical model.

Examples:
 * `(7 : Int).natAbs = 7`
 * `(0 : Int).natAbs = 0`
 * `(-11 : Int).natAbs = 11`


## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

## BASE-LIBRARY REF HAdd.hAdd
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HAdd α β γ] → α → β → γ

Docstring: `a + b` computes the sum of `a` and `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `+` in identifiers is `add`.

## BASE-LIBRARY REF instHAdd
{α : Type u_1} → [Add α] → HAdd α α α

## BASE-LIBRARY REF Distrib.toAdd
{R : Type u_1} → [self : Distrib R] → Add R

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.toDistrib
{α : Type u} → [self : NonUnitalNonAssocSemiring α] → Distrib α

## BASE-LIBRARY REF NonUnitalNonAssocRing.toNonUnitalNonAssocSemiring
{α : Type u} → [self : NonUnitalNonAssocRing α] → NonUnitalNonAssocSemiring α

## BASE-LIBRARY REF NonUnitalNonAssocCommRing.toNonUnitalNonAssocRing
{α : Type u} → [self : NonUnitalNonAssocCommRing α] → NonUnitalNonAssocRing α

## BASE-LIBRARY REF NonUnitalCommRing.toNonUnitalNonAssocCommRing
{α : Type u} → [self : NonUnitalCommRing α] → NonUnitalNonAssocCommRing α

## BASE-LIBRARY REF CommRing.toNonUnitalCommRing
{α : Type u} → [s : CommRing α] → NonUnitalCommRing α

## BASE-LIBRARY REF One.toOfNat1
{α : Type u_1} → [One α] → OfNat α 1

## BASE-LIBRARY REF MvPowerSeries.instOne
{σ : Type u_1} → {R : Type u_2} → [Semiring R] → One (MvPowerSeries σ R)

## BASE-LIBRARY REF instAddNat
Add ℕ

## BASE-LIBRARY REF instMulNat
Mul ℕ

## BASE-LIBRARY REF HSub.hSub
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HSub α β γ] → α → β → γ

Docstring: `a - b` computes the difference of `a` and `b`.
The meaning of this notation is type-dependent.
* For natural numbers, this operator saturates at 0: `a - b = 0` when `a ≤ b`. 

Conventions for notations in identifiers:

 * The recommended spelling of `-` in identifiers is `sub` (when used as a binary operator).

## BASE-LIBRARY REF instHSub
{α : Type u_1} → [Sub α] → HSub α α α

## BASE-LIBRARY REF SubNegMonoid.toSub
{G : Type u} → [self : SubNegMonoid G] → Sub G

## BASE-LIBRARY REF AddGroup.toSubNegMonoid
{A : Type u} → [self : AddGroup A] → SubNegMonoid A

## BASE-LIBRARY REF PowerSeries.instAddGroup
{R : Type u_1} → [AddGroup R] → AddGroup (PowerSeries R)

## BASE-LIBRARY REF AddGroupWithOne.toAddGroup
{R : Type u} → [self : AddGroupWithOne R] → AddGroup R

## BASE-LIBRARY REF Ring.toAddGroupWithOne
{R : Type u} → [self : Ring R] → AddGroupWithOne R

## BASE-LIBRARY REF AddMonoidAlgebra.ring
{R : Type u_1} → {M : Type u_4} → [inst : Ring R] → [AddMonoid M] → Ring (AddMonoidAlgebra R M)

## BASE-LIBRARY REF Int.instRing
Ring ℤ

## BASE-LIBRARY REF DFunLike.coe
{F : Sort u_1} → {α : outParam (Sort u_2)} → {β : outParam (α → Sort u_3)} → [self : DFunLike F α β] → F → (a : α) → β a

Docstring: The coercion from `F` to a function. 

## BASE-LIBRARY REF RingHom
(α : Type u_5) → (β : Type u_6) → [NonAssocSemiring α] → [NonAssocSemiring β] → Type (max u_5 u_6)

Docstring: Bundled semiring homomorphisms; use this for bundled ring homomorphisms too.

This extends from both `MonoidHom` and `MonoidWithZeroHom` in order to put the fields in a
sensible order, even though `MonoidWithZeroHom` already extends `MonoidHom`. 

## BASE-LIBRARY REF Semiring.toNonAssocSemiring
{α : Type u} → [self : Semiring α] → NonAssocSemiring α

## BASE-LIBRARY REF RingHom.instFunLike
{α : Type u_2} → {β : Type u_3} → {x : NonAssocSemiring α} → {x_1 : NonAssocSemiring β} → FunLike (α →+* β) α β

## BASE-LIBRARY REF PowerSeries.C
{R : Type u_1} → [inst : Semiring R] → R →+* PowerSeries R

Docstring: The constant formal power series. 

## BASE-LIBRARY REF LaurentPolynomial.T
{R : Type u_1} → [inst : Semiring R] → ℤ → LaurentPolynomial R

Docstring: The function `n ↦ T ^ n`, implemented as a sequence `ℤ → R[T;T⁻¹]`.

Using directly `T ^ n` does not work, since we want the exponents to be of Type `ℤ` and there
is no `ℤ`-power defined on `R[T;T⁻¹]`.  Using that `T` is a unit introduces extra coercions.
For these reasons, the definition of `T` is as a sequence. 

## BASE-LIBRARY REF instOfNat
{n : ℕ} → OfNat ℤ n

## BASE-LIBRARY REF Neg.neg
{α : Type u} → [self : Neg α] → α → α

Docstring: `-a` computes the negative or opposite of `a`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `-` in identifiers is `neg` (when used as a unary operator).

## BASE-LIBRARY REF Int.instNegInt
Neg ℤ

## INFORMAL STATEMENT
Jacobi’s triple product identity, take 1

In the ring $\left( \mathbb {Z}\left[ z^{\pm }\right] \right) \left[ \left[ q\right] \right] $, we have 

\[  \prod _{n>0}\left( \left( 1+q^{2n-1}z\right) \left( 1+q^{2n-1} z^{-1}\right) \left( 1-q^{2n}\right) \right) =\sum _{\ell \in \mathbb {Z} }q^{\ell ^{2}}z^{\ell }.  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.jtp.jacobizzproduct
def.jtp.jacobiZZProduct

\leanhelper  The \emph{$z$-dependent product} is 

\[  \prod _{n>0}\left((1+q^{2n-1}z)(1+q^{2n-1}z^{-1})\right) \in (\mathbb {Z}[z^{\pm }])[[q]].  \]

## VERDICT
{
  "verdict": "faithful",
  "justification": "The target has no added binders or hypotheses and asserts exactly `AlgebraicCombinatorics.jacobiLHS' = AlgebraicCombinatorics.jacobiRHS'`. Its ambient type is `JacobiRing`, whose body is `PowerSeries (LaurentPolynomial \u2124)`, matching \u201cin the ring `(\u2124[z^{\u00b1}])[[q]]`.\u201d The left side unfolds to `\u220f' (n : \u2115), jacobiProductTerm n`, with factors `1 + X^(2*n+1) * jacobiZ`, `1 + X^(2*n+1) * jacobiZInv`, and `1 - X^(2*(n+1))`; indexing `n : \u2115` from zero is exactly the reindexing of the blueprint\u2019s `n>0` factors with exponents `2n-1, 2n-1, 2n`. Here `jacobiZ = C (T 1)` and `jacobiZInv = C (T (-1))`, so these are `z` and `z\u207b\u00b9`. The right side unfolds to `\u2211' (ell : \u2124), X ^ ell.natAbs ^ 2 * C (T ell)`, which is `\u2211_{\u2113\u2208\u2124} q^{\u2113\u00b2}z^\u2113`. Thus the formal definitions reproduce both sides of the stated identity without a mathematically contentful restriction or extra assumption."
}