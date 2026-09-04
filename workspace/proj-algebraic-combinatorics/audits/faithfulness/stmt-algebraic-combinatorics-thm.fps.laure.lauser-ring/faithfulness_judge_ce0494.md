## TARGET AlgebraicCombinatorics.FPS.Laurent.LaurentSeries_X_isUnit (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K], IsUnit ((HahnSeries.single 1) 1)

Docstring: The variable `X` in Laurent series (as single 1 1) is a unit. 

## TARGET AlgebraicCombinatorics.FPS.Laurent.laurentSeries_algebra (def) — ELABORATED SIGNATURE
{K : Type u_1} → [inst : CommRing K] → Algebra K (LaurentSeries K)

Body:
fun {K} [CommRing K] => inferInstance

## PROJECT DEPENDENCY AlgebraicCombinatorics.FPS.Laurent.laurentSeries_commRing (def)
{K : Type u_1} → [inst : CommRing K] → CommRing (LaurentSeries K)

Body:
fun {K} [CommRing K] => inferInstance

Docstring: **Laurent series form a commutative K-algebra**.
(Theorem thm.fps.laure.lauser-ring, label: thm.fps.laure.lauser-ring)

This is the key structural result for Laurent series. 

## BASE-LIBRARY REF CommRing
Type u → Type u

Docstring: A commutative ring is a ring with commutative multiplication. 

## BASE-LIBRARY REF IsUnit
{M : Type u_1} → [Monoid M] → M → Prop

Body:
fun {M} [Monoid M] a => ∃ u, ↑u = a

Docstring: An element `a : M` of a `Monoid` is a unit if it has a two-sided inverse.
The actual definition says that `a` is equal to some `u : Mˣ`, where
`Mˣ` is a bundled version of `IsUnit`. 

## BASE-LIBRARY REF HahnSeries
(Γ : Type u_1) → (R : Type u_2) → [PartialOrder Γ] → [Zero R] → Type (max u_1 u_2)

Docstring: If `Γ` is linearly ordered and `R` has zero, then `R⟦Γ⟧` consists of
formal series over `Γ` with coefficients in `R`, whose supports are well-founded. 

## BASE-LIBRARY REF SemilatticeInf
Type u → Type u

Docstring: A `SemilatticeInf` is a meet-semilattice, that is, a partial order
with a meet (a.k.a. glb / greatest lower bound, inf / infimum) operation
`⊓` which is the greatest element smaller than both factors. 

## BASE-LIBRARY REF Lattice
Type u → Type u

Docstring: A lattice is a join-semilattice which is also a meet-semilattice. 

## BASE-LIBRARY REF Lattice.inf
{α : Type u} → [self : Lattice α] → α → α → α

Body:
fun α [self : Lattice α] => self.2

Docstring: The binary infimum, used to derive `Min α` 

## BASE-LIBRARY REF Lattice.inf_le_left
∀ {α : Type u} [self : Lattice α] (a b : α), Lattice.inf a b ≤ a

Docstring: The infimum is a lower bound on the first argument 

## BASE-LIBRARY REF Lattice.inf_le_right
∀ {α : Type u} [self : Lattice α] (a b : α), Lattice.inf a b ≤ b

Docstring: The infimum is a lower bound on the second argument 

## BASE-LIBRARY REF Lattice.le_inf
∀ {α : Type u} [self : Lattice α] (a b c : α), a ≤ b → a ≤ c → a ≤ Lattice.inf b c

Docstring: The infimum is the *greatest* lower bound 

## BASE-LIBRARY REF Int.instLinearOrder
LinearOrder ℤ

Body:
{ toLE := Int.instLEInt, toLT := Int.instLTInt, le_refl := Int.le_refl, le_trans := @Int.le_trans,
  lt_iff_le_not_ge := @Int.lt_iff_le_not_le, le_antisymm := @Int.le_antisymm, toMin := Int.instMin,
  toMax := Int.instMax, toOrd := instOrdInt, le_total := Int.le_total, toDecidableLE := Int.decLe,
  toDecidableEq := Int.instDecidableEq, toDecidableLT := Int.decLt, min_def := Int.instLinearOrder._proof_1,
  max_def := Int.instLinearOrder._proof_2, compare_eq_compareOfLessAndEq := Int.instLinearOrder._proof_3 }

## BASE-LIBRARY REF MulZeroClass
Type u → Type u

Docstring: Typeclass for expressing that a type `M₀` with multiplication and a zero satisfies
`0 * a = 0` and `a * 0 = 0` for all `a : M₀`. 

## BASE-LIBRARY REF NonUnitalNonAssocSemiring
Type u → Type u

Docstring: A not-necessarily-unital, not-necessarily-associative semiring. See `CommutatorRing` and the
documentation thereof in case you need a `NonUnitalNonAssocSemiring` instance on a Lie ring
or a Lie algebra. 

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.zero_mul
∀ {α : Type u} [self : NonUnitalNonAssocSemiring α] (a : α), 0 * a = 0

Docstring: Zero is a left absorbing element for multiplication 

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.mul_zero
∀ {α : Type u} [self : NonUnitalNonAssocSemiring α] (a : α), a * 0 = 0

Docstring: Zero is a right absorbing element for multiplication 

## BASE-LIBRARY REF NonUnitalNonAssocRing
Type u → Type u

Docstring: A not-necessarily-unital, not-necessarily-associative ring. 

## BASE-LIBRARY REF AddCommGroup.add_comm
∀ {G : Type u} [self : AddCommGroup G] (a b : G), a + b = b + a

Docstring: Addition is commutative in a commutative additive magma. 

## BASE-LIBRARY REF NonUnitalNonAssocRing.left_distrib
∀ {α : Type u} [self : NonUnitalNonAssocRing α] (a b c : α), a * (b + c) = a * b + a * c

Docstring: Multiplication is left distributive over addition 

## BASE-LIBRARY REF NonUnitalNonAssocRing.right_distrib
∀ {α : Type u} [self : NonUnitalNonAssocRing α] (a b c : α), (a + b) * c = a * c + b * c

Docstring: Multiplication is right distributive over addition 

## BASE-LIBRARY REF NonUnitalNonAssocRing.zero_mul
∀ {α : Type u} [self : NonUnitalNonAssocRing α] (a : α), 0 * a = 0

Docstring: Zero is a left absorbing element for multiplication 

## BASE-LIBRARY REF NonUnitalNonAssocCommRing
Type u → Type u

Docstring: A non-unital non-associative commutative ring is a `NonUnitalNonAssocRing` with commutative
multiplication. 

## BASE-LIBRARY REF NonUnitalCommRing
Type u → Type u

Docstring: A non-unital commutative ring is a `NonUnitalRing` with commutative multiplication. 

## BASE-LIBRARY REF NonUnitalCommRing.mul_comm
∀ {α : Type u} [self : NonUnitalCommRing α] (a b : α), a * b = b * a

Docstring: Multiplication is commutative in a commutative multiplicative magma. 

## BASE-LIBRARY REF MonoidWithZero
Type u → Type u

Docstring: A type `M₀` is a “monoid with zero” if it is a monoid with zero element, and `0` is left
and right absorbing. 

## BASE-LIBRARY REF Semiring
Type u → Type u

Docstring: A `Semiring` is a type with addition, multiplication, a `0` and a `1` where addition is
commutative and associative, multiplication is associative and left and right distributive over
addition, and `0` and `1` are additive and multiplicative identities. 

## BASE-LIBRARY REF NonUnitalSemiring.mul_assoc
∀ {α : Type u} [self : NonUnitalSemiring α] (a b c : α), a * b * c = a * (b * c)

Docstring: Multiplication is associative 

## BASE-LIBRARY REF Semiring.one_mul
∀ {α : Type u} [self : Semiring α] (a : α), 1 * a = a

Docstring: One is a left neutral element for multiplication 

## BASE-LIBRARY REF Semiring.mul_one
∀ {α : Type u} [self : Semiring α] (a : α), a * 1 = a

Docstring: One is a right neutral element for multiplication 

## BASE-LIBRARY REF HahnSeries.instSemiring
{Γ : Type u_1} →
  {R : Type u_3} →
    [inst : AddCommMonoid Γ] →
      [inst_1 : PartialOrder Γ] → [IsOrderedCancelAddMonoid Γ] → [inst : Semiring R] → Semiring (HahnSeries Γ R)

Body:
fun {Γ} {R} [AddCommMonoid Γ] [PartialOrder Γ] [IsOrderedCancelAddMonoid Γ] [Semiring R] =>
  { toNonUnitalSemiring := HahnSeries.instNonUnitalSemiring, toOne := HahnSeries.instNonAssocSemiring.toOne,
    one_mul := ⋯, mul_one := ⋯, toNatCast := HahnSeries.instNonAssocSemiring.toNatCast, natCast_zero := ⋯,
    natCast_succ := ⋯, npow := npowRecAuto, npow_zero := ⋯, npow_succ := ⋯ }

## BASE-LIBRARY REF AddCommMonoid
Type u → Type u

Docstring: An additive commutative monoid is an additive monoid with commutative `(+)`. 

## BASE-LIBRARY REF PartialOrder
Type u_2 → Type u_2

Docstring: A partial order is a reflexive, transitive, antisymmetric relation `≤`. 

## BASE-LIBRARY REF IsOrderedCancelAddMonoid
(α : Type u_2) → [AddCommMonoid α] → [PartialOrder α] → Prop

Docstring: An ordered cancellative additive monoid is an ordered additive
monoid in which addition is cancellative and monotone. 

## BASE-LIBRARY REF HahnSeries.instNonUnitalSemiring
{Γ : Type u_1} →
  {R : Type u_3} →
    [inst : AddCommMonoid Γ] →
      [inst_1 : PartialOrder Γ] →
        [IsOrderedCancelAddMonoid Γ] → [inst : NonUnitalSemiring R] → NonUnitalSemiring (HahnSeries Γ R)

Body:
fun {Γ} {R} [AddCommMonoid Γ] [PartialOrder Γ] [IsOrderedCancelAddMonoid Γ] [NonUnitalSemiring R] =>
  { toNonUnitalNonAssocSemiring := HahnSeries.instNonUnitalNonAssocSemiring, mul_assoc := ⋯ }

## BASE-LIBRARY REF HahnSeries.instNonAssocSemiring
{Γ : Type u_1} →
  {R : Type u_3} →
    [inst : AddCommMonoid Γ] →
      [inst_1 : PartialOrder Γ] →
        [IsOrderedCancelAddMonoid Γ] → [inst : NonAssocSemiring R] → NonAssocSemiring (HahnSeries Γ R)

Body:
fun {Γ} {R} [AddCommMonoid Γ] [PartialOrder Γ] [IsOrderedCancelAddMonoid Γ] [NonAssocSemiring R] =>
  { toNonUnitalNonAssocSemiring := HahnSeries.instNonUnitalNonAssocSemiring,
    toOne := HahnSeries.instAddCommMonoidWithOne.toOne, one_mul := ⋯, mul_one := ⋯,
    toNatCast := HahnSeries.instAddCommMonoidWithOne.toNatCast, natCast_zero := ⋯, natCast_succ := ⋯ }

## BASE-LIBRARY REF HahnSeries.instSemiring._proof_3
∀ {Γ : Type u_1} {R : Type u_2} [inst : AddCommMonoid Γ] [inst_1 : PartialOrder Γ] [inst_2 : IsOrderedCancelAddMonoid Γ]
  [inst_3 : Semiring R] (a : HahnSeries Γ R), 1 * a = a

## BASE-LIBRARY REF HahnSeries.instSemiring._proof_4
∀ {Γ : Type u_1} {R : Type u_2} [inst : AddCommMonoid Γ] [inst_1 : PartialOrder Γ] [inst_2 : IsOrderedCancelAddMonoid Γ]
  [inst_3 : Semiring R] (a : HahnSeries Γ R), a * 1 = a

## BASE-LIBRARY REF Int.instAddCommMonoid
AddCommMonoid ℤ

Body:
inferInstance

## BASE-LIBRARY REF Int.instAddCommGroup
AddCommGroup ℤ

Body:
{ toAdd := Int.instAdd, add_assoc := Int.add_assoc, toZero := Zero.ofOfNat0, zero_add := Int.zero_add,
  add_zero := Int.add_zero, nsmul := fun x1 x2 => ↑x1 * x2, nsmul_zero := Int.zero_mul,
  nsmul_succ := Int.instAddCommGroup._proof_1, toNeg := Int.instNegInt, toSub := Int.instSub, sub_eq_add_neg := ⋯,
  zsmul := fun x1 x2 => x1 * x2, zsmul_zero' := Int.zero_mul, zsmul_succ' := ⋯, zsmul_neg' := ⋯,
  neg_add_cancel := Int.add_left_neg, add_comm := Int.add_comm }

## BASE-LIBRARY REF Int.instSemiring
Semiring ℤ

Body:
inferInstance

## BASE-LIBRARY REF Int.instCommSemiring
CommSemiring ℤ

Body:
inferInstance

## BASE-LIBRARY REF Int.instIsStrictOrderedRing
IsStrictOrderedRing ℤ

## BASE-LIBRARY REF CommRing.mul_comm
∀ {α : Type u} [self : CommRing α] (a b : α), a * b = b * a

Docstring: Multiplication is commutative in a commutative multiplicative magma. 

## BASE-LIBRARY REF ZeroHom
(M : Type u_10) → (N : Type u_11) → [Zero M] → [Zero N] → Type (max u_10 u_11)

Docstring: `ZeroHom M N` is the type of functions `M → N` that preserve zero.

When possible, instead of parametrizing results over `(f : ZeroHom M N)`,
you should parametrize over `(F : Type*) [ZeroHomClass F M N] (f : F)`.

When you extend this structure, make sure to also extend `ZeroHomClass`.


## BASE-LIBRARY REF HahnSeries.instZero
{Γ : Type u_1} → {R : Type u_3} → [inst : PartialOrder Γ] → [inst_1 : Zero R] → Zero (HahnSeries Γ R)

Body:
fun {Γ} {R} [PartialOrder Γ] [Zero R] => { zero := { coeff := 0, isPWO_support' := ⋯ } }

## BASE-LIBRARY REF Zero
Type u → Type u

Docstring: A type with a zero element. 

## BASE-LIBRARY REF Pi.instZero
{ι : Type u_1} → {M : ι → Type u_5} → [(i : ι) → Zero (M i)] → Zero ((i : ι) → M i)

Body:
fun {ι} {M} [(i : ι) → Zero (M i)] => { zero := fun x => 0 }

## BASE-LIBRARY REF HahnSeries.instZero._proof_1
∀ {Γ : Type u_1} {R : Type u_2} [inst : PartialOrder Γ] [inst_1 : Zero R], (Function.support 0).IsPWO

## BASE-LIBRARY REF ZeroHom.funLike
{M : Type u_4} → {N : Type u_5} → [inst : Zero M] → [inst_1 : Zero N] → FunLike (ZeroHom M N) M N

Body:
fun {M} {N} [Zero M] [Zero N] => { coe := ZeroHom.toFun, coe_injective' := ⋯ }

## BASE-LIBRARY REF ZeroHom.funLike._proof_1
∀ {M : Type u_1} {N : Type u_2} [inst : Zero M] [inst_1 : Zero N] (f g : ZeroHom M N), f.toFun = g.toFun → f = g

## BASE-LIBRARY REF HahnSeries.single
{Γ : Type u_1} → {R : Type u_3} → [inst : PartialOrder Γ] → [inst_1 : Zero R] → Γ → ZeroHom R (HahnSeries Γ R)

Body:
fun {Γ} {R} [PartialOrder Γ] [Zero R] a =>
  { toFun := fun r => { coeff := Pi.single a r, isPWO_support' := ⋯ }, map_zero' := ⋯ }

Docstring: `single a r` is the Hahn series which has coefficient `r` at `a` and zero otherwise. 

## BASE-LIBRARY REF Int.ofNat
ℕ → ℤ

Docstring: A natural number is an integer.

This constructor covers the non-negative integers (from `0` to `∞`).


## BASE-LIBRARY REF One
Type u → Type u

Docstring: A type with a "one" element. 

## BASE-LIBRARY REF One.one
{α : Type u} → [self : One α] → α

Body:
fun α [self : One α] => self.1

Docstring: The "one" element of the type. 

## BASE-LIBRARY REF AddMonoidWithOne
Type u_2 → Type u_2

Docstring: An `AddMonoidWithOne` is an `AddMonoid` with a `1`.
It also contains data for the unique homomorphism `ℕ → R`. 

## BASE-LIBRARY REF AddGroupWithOne
Type u → Type u

Docstring: An `AddGroupWithOne` is an `AddGroup` with a 1. It also contains data for the unique
homomorphisms `ℕ → R` and `ℤ → R`. 

## BASE-LIBRARY REF Ring
Type u → Type u

Docstring: A `Ring` is a `Semiring` with negation making it an additive group. 

## BASE-LIBRARY REF Algebra
(R : Type u) → (A : Type v) → [CommSemiring R] → [Semiring A] → Type (max u v)

Docstring: An associative unital `R`-algebra is a semiring `A` equipped with a map into its center `R → A`.

See the implementation notes in this file for discussion of the details of this definition.


## BASE-LIBRARY REF LaurentSeries
(R : Type u) → [Zero R] → Type (max 0 u)

Body:
fun R [Zero R] => HahnSeries ℤ R

Docstring: `LaurentSeries R` is the type of formal Laurent series with coefficients in `R`, denoted `R⸨X⸩`.

It is implemented as a `HahnSeries` with value group `ℤ`.


## BASE-LIBRARY REF HahnSeries.powerSeriesAlgebra
(Γ : Type u_1) →
  (R : Type u_2) →
    [inst : CommSemiring R] →
      [inst_1 : Semiring Γ] →
        [inst_2 : PartialOrder Γ] →
          [inst_3 : IsStrictOrderedRing Γ] →
            {S : Type u_4} → [inst_4 : CommSemiring S] → [Algebra S (PowerSeries R)] → Algebra S (HahnSeries Γ R)

Body:
fun Γ R [CommSemiring R] [Semiring Γ] [PartialOrder Γ] [IsStrictOrderedRing Γ] {S} [CommSemiring S]
    [Algebra S (PowerSeries R)] =>
  ((HahnSeries.ofPowerSeries Γ R).comp (algebraMap S (PowerSeries R))).toAlgebra

## BASE-LIBRARY REF CommSemiring
Type u → Type u

Docstring: A commutative semiring is a semiring with commutative multiplication. 

## BASE-LIBRARY REF IsStrictOrderedRing
(R : Type u_1) → [Semiring R] → [PartialOrder R] → Prop

Docstring: A strict ordered semiring is a nontrivial semiring with a partial order such that addition is
strictly monotone and multiplication by a positive number is strictly monotone. 

## BASE-LIBRARY REF PowerSeries
Type u_1 → Type (max u_1 0)

Body:
fun R => MvPowerSeries Unit R

Docstring: Formal power series over a coefficient type `R` 

## BASE-LIBRARY REF PowerSeries.instSemiring
{R : Type u_1} → [Semiring R] → Semiring (PowerSeries R)

Body:
fun {R} [Semiring R] => id inferInstance

## BASE-LIBRARY REF HahnSeries.instCommSemiring
{Γ : Type u_1} →
  {R : Type u_3} →
    [inst : AddCommMonoid Γ] →
      [inst_1 : PartialOrder Γ] → [IsOrderedCancelAddMonoid Γ] → [inst : CommSemiring R] → CommSemiring (HahnSeries Γ R)

Body:
fun {Γ} {R} [AddCommMonoid Γ] [PartialOrder Γ] [IsOrderedCancelAddMonoid Γ] [CommSemiring R] =>
  { toSemiring := HahnSeries.instSemiring, mul_comm := ⋯ }

## BASE-LIBRARY REF RingHom.comp
{α : Type u_2} →
  {β : Type u_3} →
    {γ : Type u_4} →
      {x : NonAssocSemiring α} →
        {x_1 : NonAssocSemiring β} → {x_2 : NonAssocSemiring γ} → (β →+* γ) → (α →+* β) → α →+* γ

Body:
fun {α} {β} {γ} {x} {x_1} {x_2} g f =>
  have __src := g.toNonUnitalRingHom.comp f.toNonUnitalRingHom;
  { toFun := ⇑g ∘ ⇑f, map_one' := ⋯, map_mul' := ⋯, map_zero' := ⋯, map_add' := ⋯ }

Docstring: Composition of ring homomorphisms is a ring homomorphism. 

## BASE-LIBRARY REF HahnSeries.ofPowerSeries
(Γ : Type u_1) →
  (R : Type u_2) →
    [inst : Semiring R] →
      [inst_1 : Semiring Γ] →
        [inst_2 : PartialOrder Γ] → [inst_3 : IsStrictOrderedRing Γ] → PowerSeries R →+* HahnSeries Γ R

Body:
fun Γ R [Semiring R] [Semiring Γ] [PartialOrder Γ] [IsStrictOrderedRing Γ] =>
  (HahnSeries.embDomainRingHom (Nat.castAddMonoidHom Γ) ⋯ ⋯).comp HahnSeries.toPowerSeries.symm.toRingHom

Docstring: Casts a power series as a Hahn series with coefficients from a `StrictOrderedSemiring`. 

## BASE-LIBRARY REF algebraMap
(R : Type u) → (A : Type v) → [inst : CommSemiring R] → [inst_1 : Semiring A] → [Algebra R A] → R →+* A

Body:
fun R A [CommSemiring R] [Semiring A] [Algebra R A] => Algebra.algebraMap

Docstring: Embedding `R →+* A` given by `Algebra` structure. 

## BASE-LIBRARY REF PowerSeries.instAlgebra
{R : Type u_1} →
  {A : Type u_2} → [inst : Semiring A] → [inst_1 : CommSemiring R] → [Algebra R A] → Algebra R (PowerSeries A)

Body:
fun {R} {A} [Semiring A] [CommSemiring R] [Algebra R A] => id inferInstance

## BASE-LIBRARY REF MvPowerSeries
Type u_1 → Type u_2 → Type (max (max u_2 0) u_1)

Body:
fun σ R => (σ →₀ ℕ) → R

Docstring: Multivariate formal power series, where `σ` is the index set of the variables
and `R` is the coefficient ring. 

## BASE-LIBRARY REF MvPowerSeries.instAlgebra
{σ : Type u_1} →
  {R : Type u_2} →
    {A : Type u_3} → [inst : CommSemiring R] → [inst_1 : Semiring A] → [Algebra R A] → Algebra R (MvPowerSeries σ A)

Body:
fun {σ} {R} {A} [CommSemiring R] [Semiring A] [Algebra R A] =>
  { toSMul := DistribMulAction.toDistribSMul.toSMul,
    algebraMap := (MvPowerSeries.map (algebraMap R A)).comp MvPowerSeries.C, commutes' := ⋯, smul_def' := ⋯ }

## BASE-LIBRARY REF Algebra.id
(R : Type u) → [inst : CommSemiring R] → Algebra R R

Docstring: The identity map inducing an `Algebra` structure. 

## BASE-LIBRARY REF HahnSeries.instCommRing
{Γ : Type u_1} →
  {R : Type u_3} →
    [inst : AddCommMonoid Γ] →
      [inst_1 : PartialOrder Γ] → [IsOrderedCancelAddMonoid Γ] → [inst : CommRing R] → CommRing (HahnSeries Γ R)

Body:
fun {Γ} {R} [AddCommMonoid Γ] [PartialOrder Γ] [IsOrderedCancelAddMonoid Γ] [CommRing R] =>
  { toRing := HahnSeries.instRing, mul_comm := ⋯ }

## BASE-LIBRARY REF HahnSeries.instRing
{Γ : Type u_1} →
  {R : Type u_3} →
    [inst : AddCommMonoid Γ] →
      [inst_1 : PartialOrder Γ] → [IsOrderedCancelAddMonoid Γ] → [inst : Ring R] → Ring (HahnSeries Γ R)

Body:
fun {Γ} {R} [AddCommMonoid Γ] [PartialOrder Γ] [IsOrderedCancelAddMonoid Γ] [Ring R] =>
  { toSemiring := HahnSeries.instSemiring, toNeg := HahnSeries.instAddCommGroup.toNeg,
    toSub := HahnSeries.instAddCommGroup.toSub, sub_eq_add_neg := ⋯, zsmul := SubNegMonoid.zsmul, zsmul_zero' := ⋯,
    zsmul_succ' := ⋯, zsmul_neg' := ⋯, neg_add_cancel := ⋯,
    toIntCast := HahnSeries.instAddCommGroupWithOne.toAddGroupWithOne.toIntCast, intCast_ofNat := ⋯,
    intCast_negSucc := ⋯ }

## BASE-LIBRARY REF HahnSeries.instCommRing._proof_1
∀ {Γ : Type u_1} {R : Type u_2} [inst : AddCommMonoid Γ] [inst_1 : PartialOrder Γ] [inst_2 : IsOrderedCancelAddMonoid Γ]
  [inst_3 : CommRing R] (a b : HahnSeries Γ R), a * b = b * a

## INFORMAL STATEMENT
thm.fps.laure.lauser-ring

The subset $K\left( \left( x\right) \right) $ is a $K$-submodule of $K\left[ \left[ x^{\pm }\right] \right] $. It has a multiplication given by the same convolution rule as $K\left[ x^{\pm }\right] $: namely,

\[  \left( a_{n}\right) _{n\in \mathbb {Z}}\cdot \left( b_{n}\right) _{n\in \mathbb {Z}}=\left( c_{n}\right) _{n\in \mathbb {Z}},\  \  \  \  \  \  \  \  \  \  \text{where}\  \  \  \  \  \  \  \  \  \  c_{n}=\sum _{i\in \mathbb {Z}}a_{i}b_{n-i}.  \]

 The sum $\sum _{i\in \mathbb {Z}}a_{i}b_{n-i}$ is well-defined because for sufficiently low $i$ we have $a_i = 0$, and for sufficiently high $i$ we have $b_{n-i} = 0$. 

Equipped with this multiplication, $K\left( \left( x\right) \right) $ is a commutative $K$-algebra with unity $\left( \delta _{i,0}\right) _{i\in \mathbb {Z}}$. The element $x$ is invertible in this algebra.

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.commring.inverse-2
def.commring.inverse

Let $L$ be a commutative ring. Let $a\in L$. Then: 

\textbf{(a)} An \emph{inverse} (or \emph{multiplicative inverse}) of $a$ means an element $b\in L$ such that $ab=ba=1$. 

\textbf{(b)} We say that $a$ is \emph{invertible} in $L$ (or a \emph{unit} of $L$) if $a$ has an inverse.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.laure.double
def.fps.laure.double

Let $K\left[ \left[ x^{\pm }\right] \right] $ be the $K$-module $K^{\mathbb {Z}}$ of all families $\left( a_{n}\right) _{n\in \mathbb {Z}}=\left( \ldots ,a_{-2},a_{-1},a_{0},a_{1},a_{2},\ldots \right) $ of elements of $K$. Its addition and its scaling are defined entrywise:

\begin{align*}  \left( a_{n}\right) _{n\in \mathbb {Z}}+\left( b_{n}\right) _{n\in \mathbb {Z}} &  =\left( a_{n}+b_{n}\right) _{n\in \mathbb {Z}};\\ \lambda \left( a_{n}\right) _{n\in \mathbb {Z}} &  =\left( \lambda a_{n}\right) _{n\in \mathbb {Z}}\  \  \  \  \  \  \  \  \  \  \text{for each }\lambda \in K. \end{align*}

 An element of $K\left[ \left[ x^{\pm }\right] \right] $ will be called a \emph{doubly infinite power series}. We use the notation $\sum _{n\in \mathbb {Z}}a_{n}x^{n}$ for a family $\left( a_{n}\right) _{n\in \mathbb {Z}}\in K\left[ \left[ x^{\pm }\right] \right] $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.laure.laupol
def.fps.laure.laupol

Let $K\left[ x^{\pm }\right] $ be the $K$-submodule of $K\left[ \left[ x^{\pm }\right] \right] $ consisting of all \textbf{essentially finite} families $\left( a_{n}\right) _{n\in \mathbb {Z}}$. The elements of $K\left[ x^{\pm }\right] $ are called \emph{Laurent polynomials} in the indeterminate $x$ over $K$. 

We define a multiplication on $K\left[ x^{\pm }\right] $ by setting

\[  \left( a_{n}\right) _{n\in \mathbb {Z}}\cdot \left( b_{n}\right) _{n\in \mathbb {Z}}=\left( c_{n}\right) _{n\in \mathbb {Z}},\  \  \  \  \  \  \  \  \  \  \text{where}\  \  \  \  \  \  \  \  \  \  c_{n}=\sum _{i\in \mathbb {Z}}a_{i}b_{n-i}.  \]

 The sum $\sum _{i\in \mathbb {Z}}a_{i}b_{n-i}$ is well-defined because it is essentially finite. 

We define an element $x\in K\left[ x^{\pm }\right] $ by

\[  x=\left( \delta _{i,1}\right) _{i\in \mathbb {Z}}.  \]

In Mathlib, Laurent polynomials are represented as finitely supported functions $\mathbb {Z} \to K$ (the group algebra of $\mathbb {Z}$ over $K$).

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.laure.lauser
def.fps.laure.lauser

We let $K\left( \left( x\right) \right) $ be the subset of $K\left[ \left[ x^{\pm }\right] \right] $ consisting of all families $\left( a_{i}\right) _{i\in \mathbb {Z}}\in K\left[ \left[ x^{\pm }\right] \right] $ such that the sequence $\left( a_{-1},a_{-2},a_{-3},\ldots \right) $ is essentially finite – i.e., such that all sufficiently low $i\in \mathbb {Z}$ satisfy $a_{i}=0$. 

The elements of $K\left( \left( x\right) \right) $ are called \emph{Laurent series} in one indeterminate $x$ over $K$. 

In Mathlib, Laurent series are implemented as Hahn series over $\mathbb {Z}$ with coefficients in $K$, which are functions $\mathbb {Z} \to K$ whose support is well-founded (equivalently, bounded below). The formalization also provides a predicate on doubly infinite power series that captures this textbook definition.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.infsum.essfin
def.infsum.essfin

\textbf{(a)} A family $\left(a_{i}\right)_{i\in I}\in K^{I}$ of elements of $K$ is said to be \emph{essentially finite} if all but finitely many $i\in I$ satisfy $a_{i}=0$ (in other words, if the set $\left\{ i\in I\  \mid \  a_{i}\neq 0\right\} $ is finite). \medskip 

\textbf{(b)} Let $\left(a_{i}\right)_{i\in I}\in K^{I}$ be an essentially finite family of elements of $K$. Then, the infinite sum $\sum _{i\in I}a_{i}$ is defined to equal the finite sum $\sum _{\substack {i\in I;\\ a_{i}\neq 0}}a_{i}$. Such an infinite sum is said to be \emph{essentially finite}.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.kron-delta
def.kron-delta

If $i$ and $j$ are any objects, then $\delta _{i,j}$ means the element 

\[  \delta _{i,j} = \begin{cases}  1, &  \text{if } i = j; \\ 0, &  \text{if } i \neq j \end{cases}  \]

 of $K$.

## VERDICT
{
  "verdict": "unclear",
  "discrepancies": [],
  "justification": "The available signatures certify the structural and invertibility conclusions: `laurentSeries_commRing` has type `CommRing (LaurentSeries K)`, `laurentSeries_algebra` has type `Algebra K (LaurentSeries K)`, and `LaurentSeries_X_isUnit` asserts `IsUnit ((HahnSeries.single 1) 1)`, matching \u201ca commutative K-algebra\u201d and \u201cThe element x is invertible.\u201d Also, `LaurentSeries R` unfolds to `HahnSeries \u2124 R`, consistent with the blueprint\u2019s stated Mathlib representation. However, the blueprint additionally fixes the operations concretely: `c_n = \u2211_{i\u2208\u2124} a_i b_{n-i}`, inherited entrywise module operations, and unity `(\u03b4_{i,0})`. The relevant formal bodies are only `fun {K} [CommRing K] => inferInstance`; the supplied Hahn-series instance chain omits the multiplication, scalar-action, and one implementations behind `\u22ef` or unavailable dependencies. Thus the package does not determine whether those concrete operations and their well-definedness agree with the blueprint. A coefficient formula for Hahn-series multiplication and lemmas/bodies identifying scalar multiplication and `1` coefficientwise would be needed to decide faithfulness."
}