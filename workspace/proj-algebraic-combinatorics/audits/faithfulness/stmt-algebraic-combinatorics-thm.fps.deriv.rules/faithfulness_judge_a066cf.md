## TARGET AlgebraicCombinatorics.FPS.derivative_eq_imp_diff_const (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_5} [inst : CommRing R] [IsAddTorsionFree R] {f g : PowerSeries R},
  (PowerSeries.derivative R) f = (PowerSeries.derivative R) g → ∀ (n : ℕ), n ≠ 0 → (PowerSeries.coeff n) (f - g) = 0

Docstring: **Theorem thm.fps.deriv.rules (h)**: Two power series with equal derivatives
differ by a constant.

Note: Mathlib states this as: if `f' = g'` and `f₀ = g₀`, then `f = g`.
We state the equivalent: if `f' = g'`, then `f - g` has zero derivative,
hence is constant (all higher coefficients are zero). 

## TARGET AlgebraicCombinatorics.FPS.derivative_summableFPSSum (theorem) — ELABORATED SIGNATURE
∀ {R' : Type u_2} [inst : CommRing R'] {ι : Type u_3} (f : ι → PowerSeries R')
  (hf : AlgebraicCombinatorics.FPS.SummableFPS f),
  (PowerSeries.derivative R') (AlgebraicCombinatorics.FPS.summableFPSSum f hf) =
    AlgebraicCombinatorics.FPS.summableFPSSum (fun i => (PowerSeries.derivative R') (f i)) ⋯

Docstring: **Theorem thm.fps.deriv.rules (b)** (infinite version):
Derivative commutes with infinite summable sums.

If (fᵢ)_{i ∈ I} is a summable family of FPSs, then (fᵢ')_{i ∈ I} is summable
and (∑ fᵢ)' = ∑ fᵢ'. 

## TARGET AlgebraicCombinatorics.FPS.derivative_pow' (theorem) — ELABORATED SIGNATURE
∀ {A : Type u_4} [inst : CommRing A] (g : PowerSeries A) (n : ℕ),
  (PowerSeries.derivative A) (g ^ n) = ↑n * g ^ (n - 1) * (PowerSeries.derivative A) g

Docstring: **Theorem thm.fps.deriv.rules (f)**: Power rule for power series. 

## TARGET AlgebraicCombinatorics.FPS.derivative_comp (theorem) — ELABORATED SIGNATURE
∀ {A : Type u_4} [inst : CommRing A] (f g : PowerSeries A),
  PowerSeries.HasSubst g →
    (PowerSeries.derivative A) (PowerSeries.subst g f) =
      PowerSeries.subst g ((PowerSeries.derivative A) f) * (PowerSeries.derivative A) g

Docstring: **Theorem thm.fps.deriv.rules (g)**: Chain rule for power series.

This holds when `g` has nilpotent constant coefficient (in particular when `[x⁰]g = 0`). 

## TARGET AlgebraicCombinatorics.FPS.derivative_sum (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_1} [inst : CommSemiring R] {ι : Type u_2} (s : Finset ι) (f : ι → PowerSeries R),
  (PowerSeries.derivative R) (∑ i ∈ s, f i) = ∑ i ∈ s, (PowerSeries.derivative R) (f i)

Docstring: **Theorem thm.fps.deriv.rules (b)** (finite version):
Derivative commutes with finite sums. 

## TARGET AlgebraicCombinatorics.FPS.derivative_mul (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_1} [inst : CommSemiring R] (f g : PowerSeries R),
  (PowerSeries.derivative R) (f * g) = (PowerSeries.derivative R) f * g + f * (PowerSeries.derivative R) g

Docstring: **Theorem thm.fps.deriv.rules (d)**: Leibniz rule for power series. 

## TARGET AlgebraicCombinatorics.FPS.derivative_div (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_3} [inst : Field K] (f g : PowerSeries K),
  PowerSeries.constantCoeff g ≠ 0 →
    (PowerSeries.derivative K) (f * g⁻¹) =
      ((PowerSeries.derivative K) f * g - f * (PowerSeries.derivative K) g) * g⁻¹ ^ 2

Docstring: **Theorem thm.fps.deriv.rules (e)**: Quotient rule for power series.

Note: In Mathlib, this is stated as `(f⁻¹)' = -f⁻¹² · f'`.
The full quotient rule follows from combining this with Leibniz. 

## TARGET AlgebraicCombinatorics.FPS.derivative_smul (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_1} [inst : CommSemiring R] (c : R) (f : PowerSeries R),
  (PowerSeries.derivative R) (c • f) = c • (PowerSeries.derivative R) f

Docstring: **Theorem thm.fps.deriv.rules (c)**: Derivative commutes with scalar multiplication. 

## TARGET AlgebraicCombinatorics.FPS.derivative_add (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_1} [inst : CommSemiring R] (f g : PowerSeries R),
  (PowerSeries.derivative R) (f + g) = (PowerSeries.derivative R) f + (PowerSeries.derivative R) g

Docstring: **Theorem thm.fps.deriv.rules (a)**: Derivative is additive. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.FPS.SummableFPS (def)
{R : Type u_1} → [CommRing R] → {ι : Type u_2} → (ι → PowerSeries R) → Prop

Body:
fun {R} [CommRing R] {ι} f => ∀ (n : ℕ), {i | (PowerSeries.coeff n) (f i) ≠ 0}.Finite

Docstring: A family of FPS is summable if for each coefficient index n,
all but finitely many family members have that coefficient equal to zero.
(Definition def.fps.summable) 

## PROJECT DEPENDENCY AlgebraicCombinatorics.FPS.summableFPSSum (def)
{R : Type u_1} →
  [inst : CommRing R] →
    {ι : Type u_2} → (f : ι → PowerSeries R) → AlgebraicCombinatorics.FPS.SummableFPS f → PowerSeries R

Body:
fun {R} [CommRing R] {ι} f _hf => PowerSeries.mk fun n => ∑ᶠ (i : ι), (PowerSeries.coeff n) (f i)

Docstring: The sum of a summable family of FPS.
(Definition def.fps.summable, eq. eq.def.fps.summable.sum)

For a summable family (fᵢ)_{i ∈ I}, the sum ∑_{i ∈ I} fᵢ is the FPS whose
n-th coefficient is ∑_{i ∈ I} [x^n] fᵢ (an essentially finite sum). 

## PROJECT DEPENDENCY AlgebraicCombinatorics.FPS.summableFPS_derivative (theorem)
∀ {R' : Type u_2} [inst : CommRing R'] {ι : Type u_3} (f : ι → PowerSeries R'),
  AlgebraicCombinatorics.FPS.SummableFPS f →
    AlgebraicCombinatorics.FPS.SummableFPS fun i => (PowerSeries.derivative R') (f i)

Docstring: If (fᵢ) is a summable family, then (fᵢ') is also summable. 

## BASE-LIBRARY REF CommRing
Type u → Type u

Docstring: A commutative ring is a ring with commutative multiplication. 

## BASE-LIBRARY REF IsAddTorsionFree
(M : Type u_2) → [AddMonoid M] → Prop

Docstring: An additive monoid is torsion-free if scalar multiplication by every non-zero element `n : ℕ` is
injective. 

## BASE-LIBRARY REF AddMonoidWithOne.toAddMonoid
{R : Type u_2} → [self : AddMonoidWithOne R] → AddMonoid R

## BASE-LIBRARY REF AddGroupWithOne.toAddMonoidWithOne
{R : Type u} → [self : AddGroupWithOne R] → AddMonoidWithOne R

## BASE-LIBRARY REF Ring.toAddGroupWithOne
{R : Type u} → [self : Ring R] → AddGroupWithOne R

## BASE-LIBRARY REF CommRing.toRing
{α : Type u} → [self : CommRing α] → Ring α

## BASE-LIBRARY REF PowerSeries
Type u_1 → Type (max u_1 0)

Docstring: Formal power series over a coefficient type `R` 

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

## BASE-LIBRARY REF DFunLike.coe
{F : Sort u_1} → {α : outParam (Sort u_2)} → {β : outParam (α → Sort u_3)} → [self : DFunLike F α β] → F → (a : α) → β a

Docstring: The coercion from `F` to a function. 

## BASE-LIBRARY REF Derivation
(R : Type u_1) →
  (A : Type u_2) →
    (M : Type u_3) →
      [inst : CommSemiring R] →
        [inst_1 : CommSemiring A] →
          [inst_2 : AddCommMonoid M] → [Algebra R A] → [_root_.Module A M] → [_root_.Module R M] → Type (max u_2 u_3)

Docstring: `D : Derivation R A M` is an `R`-linear map from `A` to `M` that satisfies the `leibniz`
equality. We also require that `D 1 = 0`. See `Derivation.mk'` for a constructor that deduces this
assumption from the Leibniz rule when `M` is cancellative.

TODO: update this when bimodules are defined. 

## BASE-LIBRARY REF CommRing.toCommSemiring
{α : Type u} → [s : CommRing α] → CommSemiring α

## BASE-LIBRARY REF PowerSeries.instCommSemiring
{R : Type u_1} → [CommSemiring R] → CommSemiring (PowerSeries R)

## BASE-LIBRARY REF PowerSeries.instAddCommMonoid
{R : Type u_1} → [AddCommMonoid R] → AddCommMonoid (PowerSeries R)

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.toAddCommMonoid
{α : Type u} → [self : NonUnitalNonAssocSemiring α] → AddCommMonoid α

## BASE-LIBRARY REF NonAssocSemiring.toNonUnitalNonAssocSemiring
{α : Type u} → [self : NonAssocSemiring α] → NonUnitalNonAssocSemiring α

## BASE-LIBRARY REF Semiring.toNonAssocSemiring
{α : Type u} → [self : Semiring α] → NonAssocSemiring α

## BASE-LIBRARY REF CommSemiring.toSemiring
{R : Type u} → [self : CommSemiring R] → Semiring R

## BASE-LIBRARY REF PowerSeries.instAlgebra
{R : Type u_1} →
  {A : Type u_2} → [inst : Semiring A] → [inst_1 : CommSemiring R] → [Algebra R A] → Algebra R (PowerSeries A)

## BASE-LIBRARY REF Algebra.id
(R : Type u) → [inst : CommSemiring R] → Algebra R R

Docstring: The identity map inducing an `Algebra` structure. 

## BASE-LIBRARY REF Semiring.toModule
{R : Type u_1} → [inst : Semiring R] → _root_.Module R R

## BASE-LIBRARY REF PowerSeries.instModule
{R : Type u_1} →
  {A : Type u_2} →
    [inst : Semiring R] → [inst_1 : AddCommMonoid A] → [_root_.Module R A] → _root_.Module R (PowerSeries A)

## BASE-LIBRARY REF Derivation.instFunLike
{R : Type u_1} →
  {A : Type u_2} →
    {M : Type u_4} →
      [inst : CommSemiring R] →
        [inst_1 : CommSemiring A] →
          [inst_2 : AddCommMonoid M] →
            [inst_3 : Algebra R A] →
              [inst_4 : _root_.Module A M] → [inst_5 : _root_.Module R M] → FunLike (Derivation R A M) A M

## BASE-LIBRARY REF PowerSeries.derivative
(R : Type u_1) → [inst : CommSemiring R] → Derivation R (PowerSeries R) (PowerSeries R)

Docstring: The formal derivative of a formal power series 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF Ne
{α : Sort u} → α → α → Prop

Docstring: `a ≠ b`, or `Ne a b` is defined as `¬ (a = b)` or `a = b → False`,
and asserts that `a` and `b` are not equal.


Conventions for notations in identifiers:

 * The recommended spelling of `≠` in identifiers is `ne`.

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

## BASE-LIBRARY REF LinearMap
{R : Type u_14} →
  {S : Type u_15} →
    [inst : Semiring R] →
      [inst_1 : Semiring S] →
        (R →+* S) →
          (M : Type u_16) →
            (M₂ : Type u_17) →
              [inst_2 : AddCommMonoid M] →
                [inst_3 : AddCommMonoid M₂] → [_root_.Module R M] → [_root_.Module S M₂] → Type (max u_16 u_17)

Docstring: A map `f` between an `R`-module and an `S`-module over a ring homomorphism `σ : R →+* S`
is semilinear if it satisfies the two properties `f (x + y) = f x + f y` and
`f (c • x) = (σ c) • f x`. Elements of `LinearMap σ M M₂` (available under the notation
`M →ₛₗ[σ] M₂`) are bundled versions of such maps. For plain linear maps (i.e. for which
`σ = RingHom.id R`), the notation `M →ₗ[R] M₂` is available. An unbundled version of plain linear
maps is available with the predicate `IsLinearMap`, but it should be avoided most of the time. 

## BASE-LIBRARY REF RingHom.id
(α : Type u_5) → [inst : NonAssocSemiring α] → α →+* α

Docstring: The identity ring homomorphism from a semiring to itself. 

## BASE-LIBRARY REF LinearMap.instFunLike
{R : Type u_1} →
  {S : Type u_5} →
    {M : Type u_8} →
      {M₃ : Type u_11} →
        [inst : Semiring R] →
          [inst_1 : Semiring S] →
            [inst_2 : AddCommMonoid M] →
              [inst_3 : AddCommMonoid M₃] →
                [inst_4 : _root_.Module R M] →
                  [inst_5 : _root_.Module S M₃] → {σ : R →+* S} → FunLike (M →ₛₗ[σ] M₃) M M₃

## BASE-LIBRARY REF PowerSeries.coeff
{R : Type u_1} → [inst : Semiring R] → ℕ → PowerSeries R →ₗ[R] R

Docstring: The `n`th coefficient of a formal power series. 

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

## BASE-LIBRARY REF Zero.toOfNat0
{α : Type u_1} → [Zero α] → OfNat α 0

## BASE-LIBRARY REF MulZeroClass.toZero
{M₀ : Type u} → [self : MulZeroClass M₀] → Zero M₀

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.toMulZeroClass
{α : Type u} → [self : NonUnitalNonAssocSemiring α] → MulZeroClass α

## BASE-LIBRARY REF NonUnitalNonAssocRing.toNonUnitalNonAssocSemiring
{α : Type u} → [self : NonUnitalNonAssocRing α] → NonUnitalNonAssocSemiring α

## BASE-LIBRARY REF NonUnitalNonAssocCommRing.toNonUnitalNonAssocRing
{α : Type u} → [self : NonUnitalNonAssocCommRing α] → NonUnitalNonAssocRing α

## BASE-LIBRARY REF NonUnitalCommRing.toNonUnitalNonAssocCommRing
{α : Type u} → [self : NonUnitalCommRing α] → NonUnitalNonAssocCommRing α

## BASE-LIBRARY REF CommRing.toNonUnitalCommRing
{α : Type u} → [s : CommRing α] → NonUnitalCommRing α

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


## BASE-LIBRARY REF AddMonoidWithOne.toNatCast
{R : Type u_2} → [self : AddMonoidWithOne R] → NatCast R

## BASE-LIBRARY REF MvPowerSeries.instAddMonoidWithOne
{σ : Type u_1} → {R : Type u_2} → [Semiring R] → AddMonoidWithOne (MvPowerSeries σ R)

## BASE-LIBRARY REF instSubNat
Sub ℕ

## BASE-LIBRARY REF PowerSeries.HasSubst
{τ : Type u_3} → {S : Type u_4} → [CommRing S] → MvPowerSeries τ S → Prop

Docstring: (Possibly multivariate) power series which can be substituted in a `PowerSeries`. 

## BASE-LIBRARY REF PowerSeries.subst
{R : Type u_2} →
  [inst : CommRing R] →
    {τ : Type u_3} →
      {S : Type u_4} → [inst_1 : CommRing S] → [Algebra R S] → MvPowerSeries τ S → PowerSeries R → MvPowerSeries τ S

Docstring: Substitution of power series into a power series. 

## BASE-LIBRARY REF MvPowerSeries
Type u_1 → Type u_2 → Type (max (max u_2 0) u_1)

Docstring: Multivariate formal power series, where `σ` is the index set of the variables
and `R` is the coefficient ring. 

## BASE-LIBRARY REF CommSemiring
Type u → Type u

Docstring: A commutative semiring is a semiring with commutative multiplication. 

## BASE-LIBRARY REF Finset
Type u_4 → Type u_4

Docstring: `Finset α` is the type of finite sets of elements of `α`. It is implemented
as a multiset (a list up to permutation) which has no duplicate elements. 

## BASE-LIBRARY REF Finset.sum
{ι : Type u_1} → {M : Type u_3} → [AddCommMonoid M] → Finset ι → (ι → M) → M

Docstring: `∑ x ∈ s, f x` is the sum of `f x` as `x` ranges over the elements
of the finite set `s`.

When the index type is a `Fintype`, the notation `∑ x, f x`, is a shorthand for
`∑ x ∈ Finset.univ, f x`. 

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

## BASE-LIBRARY REF Field
Type u → Type u

Docstring: A `Field` is a `CommRing` with multiplicative inverses for nonzero elements.

An instance of `Field K` includes maps `ratCast : ℚ → K` and `qsmul : ℚ → K → K`.
Those two fields are needed to implement the `DivisionRing K → Algebra ℚ K` instance since we need
to control the specific definitions for some special cases of `K` (in particular `K = ℚ` itself).
See also note [forgetful inheritance].

If the field has positive characteristic `p`, our division by zero convention forces
`ratCast (1 / p) = 1 / 0 = 0`. 

## BASE-LIBRARY REF RingHom
(α : Type u_5) → (β : Type u_6) → [NonAssocSemiring α] → [NonAssocSemiring β] → Type (max u_5 u_6)

Docstring: Bundled semiring homomorphisms; use this for bundled ring homomorphisms too.

This extends from both `MonoidHom` and `MonoidWithZeroHom` in order to put the fields in a
sensible order, even though `MonoidWithZeroHom` already extends `MonoidHom`. 

## BASE-LIBRARY REF DivisionSemiring.toSemiring
{K : Type u_2} → [self : DivisionSemiring K] → Semiring K

## BASE-LIBRARY REF Semifield.toDivisionSemiring
{K : Type u_2} → [self : Semifield K] → DivisionSemiring K

## BASE-LIBRARY REF Field.toSemifield
{K : Type u_1} → [Field K] → Semifield K

## BASE-LIBRARY REF RingHom.instFunLike
{α : Type u_2} → {β : Type u_3} → {x : NonAssocSemiring α} → {x_1 : NonAssocSemiring β} → FunLike (α →+* β) α β

## BASE-LIBRARY REF PowerSeries.constantCoeff
{R : Type u_1} → [inst : Semiring R] → PowerSeries R →+* R

Docstring: The constant coefficient of a formal power series. 

## BASE-LIBRARY REF EuclideanDomain.toCommRing
{R : Type u} → [self : EuclideanDomain R] → CommRing R

## BASE-LIBRARY REF Field.toEuclideanDomain
{K : Type u_1} → [Field K] → EuclideanDomain K

## BASE-LIBRARY REF Semifield.toCommSemiring
{K : Type u_2} → [self : Semifield K] → CommSemiring K

## BASE-LIBRARY REF Inv.inv
{α : Type u} → [self : Inv α] → α → α

Docstring: `a⁻¹` computes the inverse of `a`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `⁻¹` in identifiers is `inv`.

## BASE-LIBRARY REF PowerSeries.instInv
{k : Type u_2} → [Field k] → Inv (PowerSeries k)

## BASE-LIBRARY REF DivisionRing.toRing
{K : Type u_2} → [self : DivisionRing K] → Ring K

## BASE-LIBRARY REF Field.toDivisionRing
{K : Type u} → [self : Field K] → DivisionRing K

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

## BASE-LIBRARY REF Set.Finite
{α : Type u} → Set α → Prop

Docstring: A set is finite if the corresponding `Subtype` is finite,
i.e., if there exists a natural `n : ℕ` and an equivalence `s ≃ Fin n`. 

## BASE-LIBRARY REF setOf
{α : Type u} → (α → Prop) → Set α

Docstring: Turn a predicate `p : α → Prop` into a set, also written as `{x | p x}` 

## BASE-LIBRARY REF PowerSeries.mk
{R : Type u_2} → (ℕ → R) → PowerSeries R

Docstring: Constructor for formal power series. 

## BASE-LIBRARY REF finsum
{M : Type u_7} → {α : Sort u_8} → [AddCommMonoid M] → (α → M) → M

Docstring: Sum of `f x` as `x` ranges over the elements of the support of `f`, if it's finite. Zero
otherwise. 

## INFORMAL STATEMENT
thm.fps.deriv.rules

\textbf{(a)} We have $\left( f+g\right) ^{\prime }=f^{\prime }+g^{\prime }$ for any $f,g\in K\left[ \left[ x\right] \right] $. \medskip 

\textbf{(b)} If $\left( f_{i}\right) _{i\in I}$ is a summable family of FPSs, then the family $\left( f_{i}^{\prime }\right) _{i\in I}$ is summable as well, and we have

\[  \left( \sum _{i\in I}f_{i}\right) ^{\prime }=\sum _{i\in I}f_{i}^{\prime }.  \]

\textbf{(c)} We have $\left( cf\right) ^{\prime }=cf^{\prime }$ for any $c\in K$ and $f\in K\left[ \left[ x\right] \right] $. \medskip 

\textbf{(d)} We have $\left( fg\right) ^{\prime }=f^{\prime }g+fg^{\prime }$ for any $f,g\in K\left[ \left[ x\right] \right] $. (This is known as the \emph{Leibniz rule}.) \medskip 

\textbf{(e)} If $f,g\in K\left[ \left[ x\right] \right] $ are two FPSs such that $g$ is invertible, then

\[  \left( \frac{f}{g}\right) ^{\prime }=\frac{f^{\prime }g-fg^{\prime }}{g^{2}}.  \]

 (This is known as the \emph{quotient rule}.) \medskip 

\textbf{(f)} If $g\in K\left[ \left[ x\right] \right] $ is an FPS, then $\left( g^{n}\right) ^{\prime }=ng^{\prime }g^{n-1}$ for any $n\in \mathbb {N}$ (where the expression $ng^{\prime }g^{n-1}$ is to be understood as $0$ if $n=0$). \medskip 

\textbf{(g)} Given two FPSs $f,g\in K\left[ \left[ x\right] \right] $, we have 

\[  \left( f\circ g\right) ^{\prime }=\left( f^{\prime }\circ g\right) \cdot g^{\prime } \]

 if $f$ is a polynomial or if $\left[ x^{0}\right] g=0$. (This is known as the \emph{chain rule}.) \medskip 

\textbf{(h)} If $K$ is a $\mathbb {Q}$-algebra, and if two FPSs $f,g\in K\left[ \left[ x\right] \right] $ satisfy $f^{\prime }=g^{\prime }$, then $f-g$ is constant.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-conv.det.k
conv.det.K

For the rest of this section, we fix a commutative ring $K$. In most examples, $K$ will be $\mathbb {Z}$ or $\mathbb {Q}$ or a polynomial ring.

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.alg.kalg
def.alg.Kalg

A $K$\emph{-algebra} is a set $A$ equipped with four maps

\begin{align*}  \oplus &  :A\times A\rightarrow A,\\ \ominus &  :A\times A\rightarrow A,\\ \odot &  :A\times A\rightarrow A,\\ \rightharpoonup &  :K\times A\rightarrow A \end{align*}

 and two elements $\overrightarrow {0}\in A$ and $\overrightarrow {1}\in A$ satisfying the following properties: 

\begin{enumerate} \item The set $A$, equipped with the maps $\oplus $, $\ominus $ and $\odot $ and the two elements $\overrightarrow {0}$ and $\overrightarrow {1}$, is a (noncommutative) ring. 

\item The set $A$, equipped with the maps $\oplus $, $\ominus $ and $\rightharpoonup $ and the element $\overrightarrow {0}$, is a $K$-module. 

\item We have

\begin{equation}  \lambda \rightharpoonup \left( a\odot b\right) =\left( \lambda \rightharpoonup a\right) \odot b=a\odot \left( \lambda \rightharpoonup b\right) \end{equation}

 for all $\lambda \in K$ and $a,b\in A$. 

\end{enumerate}

(Thus, in a nutshell, a $K$-algebra is a set $A$ that is simultaneously a ring and a $K$-module, with the property that the ring $A$ and the $K$-module $A$ have the same addition, the same subtraction and the same zero, and satisfy the additional compatibility property (\ref{eq.def.alg.Kalg.scaleinv}).)

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.alg.ring
def.alg.ring

The notion of a \emph{ring} (also known as a \emph{noncommutative ring}) is defined in the exact same way as we defined the notion of a commutative ring in Definition~ \ref{def.alg.commring}, except that the “Commutativity of multiplication” axiom is removed.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.coeff
def.fps.coeff

If $n\in \mathbb {N}$, and if $\mathbf{a}=\left( a_{0},a_{1},a_{2},\ldots \right) \in K\left[\left[x\right]\right]$ is an FPS, then we define an element $\left[x^{n}\right]\mathbf{a}\in K$ by 

\[  \left[x^{n}\right]\mathbf{a}:=a_{n}.  \]

 This is called the \emph{coefficient of }$x^{n}$\emph{ in }$\mathbf{a}$, or the $n$\emph{-th coefficient} of $\mathbf{a}$, or the $x^{n}$\emph{-coefficient} of $\mathbf{a}$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.deriv
def.fps.deriv

Let $f\in K\left[ \left[ x\right] \right] $ be an FPS. Then, the \emph{derivative} $f^{\prime }$ of $f$ is an FPS defined as follows: Write $f$ as $f=\sum _{n\in \mathbb {N}}f_{n}x^{n}$ (with $f_{0},f_{1},f_{2},\ldots \in K$), and set

\[  f^{\prime }:=\sum _{n>0}nf_{n}x^{n-1}.  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.fps
def.fps.fps

A \emph{formal power series} (or, short, \emph{FPS}) in $1$ indeterminate over $K$ means a sequence $\left(a_{0},a_{1},a_{2},\ldots \right) = \left(a_{n}\right)_{n\in \mathbb {N}} \in K^{\mathbb {N}}$ of elements of $K$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.ops
def.fps.ops

\textbf{(a)} The \emph{sum} of two FPSs $\mathbf{a}=\left( a_{0},a_{1},a_{2},\ldots \right)$ and $\mathbf{b}=\left(b_{0},b_{1},b_{2},\ldots \right)$ is defined to be the FPS

\[  \left(a_{0}+b_{0},\  \  a_{1}+b_{1},\  \  a_{2}+b_{2},\  \  \ldots \right).  \]

 It is denoted by $\mathbf{a}+\mathbf{b}$. \medskip 

\textbf{(b)} The \emph{difference} of two FPSs $\mathbf{a}=\left(a_{0},a_{1},a_{2},\ldots \right)$ and $\mathbf{b}=\left(b_{0},b_{1},b_{2},\ldots \right)$ is defined to be the FPS

\[  \left(a_{0}-b_{0},\  \  a_{1}-b_{1},\  \  a_{2}-b_{2},\  \  \ldots \right).  \]

 It is denoted by $\mathbf{a}-\mathbf{b}$. \medskip 

\textbf{(c)} If $\lambda \in K$ and if $\mathbf{a}=\left(a_{0},a_{1},a_{2},\ldots \right)$ is an FPS, then we define an FPS 

\[  \lambda \mathbf{a}:=\left(\lambda a_{0},\lambda a_{1},\lambda a_{2},\ldots \right).  \]

\textbf{(d)} The \emph{product} of two FPSs $\mathbf{a}=\left(a_{0},a_{1},a_{2},\ldots \right)$ and $\mathbf{b}=\left(b_{0},b_{1},b_{2},\ldots \right)$ is defined to be the FPS $\left(c_{0},c_{1},c_{2},\ldots \right)$, where 

\begin{align*}  c_{n} &  =\sum _{i=0}^{n}a_{i}b_{n-i}=\sum _{\substack {\left(i,j\right) \in \mathbb {N}^{2};\\ \begin{bgroup} i+j=n

\end{bgroup}}}a_{i}b_{j}\\ &  =a_{0}b_{n}+a_{1}b_{n-1}+a_{2}b_{n-2}+\cdots +a_{n}b_{0}\  \  \  \  \  \  \  \  \  \  \text{for each }n\in \mathbb {N}. \end{align*}

 This product is denoted by $\mathbf{a}\cdot \mathbf{b}$ or just by $\mathbf{ab}$. \medskip 

\textbf{(e)} For each $a\in K$, we define $\underline{a}$ to be the FPS $\left(a,0,0,0,\ldots \right)$. An FPS of the form $\underline{a}$ for some $a\in K$ (that is, an FPS $\left(a_{0},a_{1},a_{2},\ldots \right)$ satisfying $a_{1}=a_{2}=a_{3}=\cdots =0$) is said to be \emph{constant}. \medskip 

\textbf{(f)} The set of all FPSs (in $1$ indeterminate over $K$) is denoted $K\left[\left[x\right]\right]$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.pol
def.fps.pol

\textbf{(a)} An FPS $a\in K\left[ \left[ x\right] \right] $ is said to be a \emph{polynomial} if all but finitely many $n\in \mathbb {N}$ satisfy $\left[ x^{n}\right] a=0$ (that is, if all but finitely many coefficients of $a$ are $0$). \medskip 

\textbf{(b)} We let $K\left[ x\right] $ be the set of all polynomials $a\in K\left[ \left[ x\right] \right] $. This set $K\left[ x\right] $ is a subring of $K\left[ \left[ x\right] \right] $ (according to Theorem \ref{thm.fps.pol.ring} below), and is called the \emph{univariate polynomial ring} over $K$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.subs
def.fps.subs

Let $f$ and $g$ be two FPSs in $K[[x]]$. Assume that $[x^0]g = 0$ (that is, $g = g_1 x + g_2 x^2 + g_3 x^3 + \cdots $ for some $g_1, g_2, g_3, \ldots \in K$). 

We then define an FPS $f[g] \in K[[x]]$ as follows: 

Write $f$ in the form $f = \sum _{n \in \mathbb {N}} f_n x^n$ with $f_0, f_1, f_2, \ldots \in K$. (That is, $f_n = [x^n]f$ for each $n \in \mathbb {N}$.) Then, set 

\[  f[g] := \sum _{n \in \mathbb {N}} f_n g^n.  \]

 (This sum is well-defined, as we will see in Proposition \ref{prop.fps.subs.wd} \textbf{(b)} below.) 

This FPS $f[g]$ is also denoted by $f \circ g$, and is called the \emph{composition} of $f$ with $g$, or the result of \emph{substituting} $g$ for $x$ in $f$. 

Equivalently, the $n$-th coefficient of $f[g]$ is the finite sum 

\[  [x^n](f[g]) = \sum _{d=0}^{n} f_d \cdot [x^n](g^d).  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.summable
def.fps.summable

A (possibly infinite) family $\left(\mathbf{a}_{i}\right)_{i\in I}$ of FPSs is said to be \emph{summable} (or \emph{entrywise essentially finite}) if 

\[  \text{for each }n\in \mathbb {N}\text{, all but finitely many }i\in I\text{ satisfy }\left[x^{n}\right]\mathbf{a}_{i}=0.  \]

 In this case, the sum $\sum _{i\in I}\mathbf{a}_{i}$ is defined to be the FPS with 

\[  \left[x^{n}\right]\left(\sum _{i\in I}\mathbf{a}_{i}\right) =\underbrace{\sum _{i\in I}\left[x^{n}\right]\mathbf{a}_{i}}_{\substack {\text{an essentially}\\ \text{finite sum}}} \  \  \  \  \  \  \  \  \  \  \text{for all }n\in \mathbb {N}\text{.}  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.x
def.fps.x

Let $x$ denote the FPS $\left(0,1,0,0,0,\ldots \right)$. In other words, let $x$ denote the FPS with $\left[x^{1}\right]x=1$ and $\left[x^{i}\right]x=0$ for all $i\neq 1$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.infsum.essfin
def.infsum.essfin

\textbf{(a)} A family $\left(a_{i}\right)_{i\in I}\in K^{I}$ of elements of $K$ is said to be \emph{essentially finite} if all but finitely many $i\in I$ satisfy $a_{i}=0$ (in other words, if the set $\left\{ i\in I\  \mid \  a_{i}\neq 0\right\} $ is finite). \medskip 

\textbf{(b)} Let $\left(a_{i}\right)_{i\in I}\in K^{I}$ be an essentially finite family of elements of $K$. Then, the infinite sum $\sum _{i\in I}a_{i}$ is defined to equal the finite sum $\sum _{\substack {i\in I;\\ a_{i}\neq 0}}a_{i}$. Such an infinite sum is said to be \emph{essentially finite}.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.pol.subs
def.pol.subs

Let $f\in K\left[ x\right] $ be a polynomial. Let $A$ be any $K$-algebra. Let $a\in A$ be any element. We then define an element $f\left[ a\right] \in A$ as follows: 

Write $f$ in the form $f=\sum _{n\in \mathbb {N}}f_{n}x^{n}$ with $f_{0},f_{1},f_{2},\ldots \in K$. (That is, $f_{n}=\left[ x^{n}\right] f$ for each $n\in \mathbb {N}$.) Then, set

\[  f\left[ a\right] :=\sum _{n\in \mathbb {N}}f_{n}a^{n}.  \]

 (This sum is essentially finite, since $f$ is a polynomial.) 

The element $f\left[ a\right] $ is also denoted by $f\circ a$ or by $f\left( a\right) $, and is called the \emph{value} of $f$ at $a$ (or the \emph{evaluation} of $f$ at $a$, or the \emph{result of substituting }$a$ for $x$ in $f$).

## VERDICT
{
  "verdict": "drift",
  "justification": "The package is not faithful as a whole because parts (e) and (g) add mathematically substantive restrictions.\n\nFor (e), the blueprint assumes only the fixed commutative ring and says \u201csuch that g is invertible.\u201d The target instead binds `\u2200 {K} [inst : Field K] ...` and assumes `PowerSeries.constantCoeff g \u2260 0`. Requiring the entire coefficient ring to be a field is stronger than requiring this particular power series to be invertible; over a general commutative ring, invertibility corresponds to the constant coefficient being a unit, not merely nonzero. Thus `derivative_div` does not cover the blueprint\u2019s general commutative-ring case. It should use `[CommRing K]` with a unit/invertibility hypothesis on `g` (and a general inverse for units, or an explicitly supplied inverse), rather than `[Field K]` and nonzeroness.\n\nFor (g), the blueprint states the chain rule \u201cif f is a polynomial or if [x\u2070]g = 0.\u201d The target `derivative_comp` has only the premise `PowerSeries.HasSubst g`, independent of `f`. Consequently it omits the polynomial branch for arbitrary `g`. It should assume a disjunction expressing that `f` has finite coefficient support or that `PowerSeries.coeff 0 g = 0`, with substitution/evaluation defined for both branches. Allowing nilpotent constant coefficients through `HasSubst g` would itself be a legitimate generalization, but it does not compensate for omitting the polynomial case.\n\nThe other displayed rules match or are valid generalizations. In particular, (h)\u2019s `[IsAddTorsionFree R]` is weaker than the blueprint\u2019s \u201cK is a \u211a-algebra,\u201d so `derivative_eq_imp_diff_const` is more general, and its conclusion `\u2200 n, n \u2260 0 \u2192 coeff n (f - g) = 0` exactly says that `f-g` is constant. The semiring assumptions in the additive, scalar, product, power, and finite-sum rules are likewise harmless generalizations."
}