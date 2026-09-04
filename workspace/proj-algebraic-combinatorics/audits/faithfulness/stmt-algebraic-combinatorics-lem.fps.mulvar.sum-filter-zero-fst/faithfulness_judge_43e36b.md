## TARGET AlgebraicCombinatorics.sum_filter_zero_fst (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_1} [inst : CommSemiring R] {σ : Type u_2} [inst_1 : DecidableEq σ] (i : σ) (m : σ →₀ ℕ)
  (f g : MvPowerSeries σ R),
  ∑ p ∈ Finset.antidiagonal (m + fun₀ | i => 1) with ¬(fun₀ | i => 1) ≤ p.1,
      ↑(p.1 i) * (MvPowerSeries.coeff p.1) f * (MvPowerSeries.coeff p.2) g =
    0

Docstring: Terms where `p.1 i = 0` contribute zero to the first derivative sum. 

## BASE-LIBRARY REF CommSemiring
Type u → Type u

Docstring: A commutative semiring is a semiring with commutative multiplication. 

## BASE-LIBRARY REF Finsupp
Type u_9 → (M : Type u_10) → [Zero M] → Type (max u_10 u_9)

Docstring: `Finsupp α M`, denoted `α →₀ M`, is the type of functions `f : α → M` such that
`f x = 0` for all but finitely many `x`. 

## BASE-LIBRARY REF MulZeroClass
Type u → Type u

Docstring: Typeclass for expressing that a type `M₀` with multiplication and a zero satisfies
`0 * a = 0` and `a * 0 = 0` for all `a : M₀`. 

## BASE-LIBRARY REF Nat.instMulZeroClass
MulZeroClass ℕ

Body:
{ toMul := instMulNat, toZero := Nat.instAddMonoid.toAddZeroClass.toZero, zero_mul := Nat.zero_mul,
  mul_zero := Nat.mul_zero }

## BASE-LIBRARY REF Nat.instAddMonoid
AddMonoid ℕ

Body:
inferInstance

## BASE-LIBRARY REF Nat.zero_mul
∀ (n : ℕ), 0 * n = 0

## BASE-LIBRARY REF Nat.mul_zero
∀ (n : ℕ), n * 0 = 0

## BASE-LIBRARY REF MvPowerSeries
Type u_1 → Type u_2 → Type (max (max u_2 0) u_1)

Body:
fun σ R => (σ →₀ ℕ) → R

Docstring: Multivariate formal power series, where `σ` is the index set of the variables
and `R` is the coefficient ring. 

## BASE-LIBRARY REF Finset.sum
{ι : Type u_1} → {M : Type u_3} → [AddCommMonoid M] → Finset ι → (ι → M) → M

Body:
fun {ι} {M} [AddCommMonoid M] s f => (Multiset.map f s.val).sum

Docstring: `∑ x ∈ s, f x` is the sum of `f x` as `x` ranges over the elements
of the finite set `s`.

When the index type is a `Fintype`, the notation `∑ x, f x`, is a shorthand for
`∑ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF Prod
Type u → Type v → Type (max u v)

Docstring: The product type, usually written `α × β`. Product types are also called pair or tuple types.
Elements of this type are pairs in which the first element is an `α` and the second element is a
`β`.

Products nest to the right, so `(x, y, z) : α × β × γ` is equivalent to `(x, (y, z)) : α × (β × γ)`.


Conventions for notations in identifiers:

 * The recommended spelling of `×` in identifiers is `Prod`.

## BASE-LIBRARY REF NonUnitalNonAssocSemiring
Type u → Type u

Docstring: A not-necessarily-unital, not-necessarily-associative semiring. See `CommutatorRing` and the
documentation thereof in case you need a `NonUnitalNonAssocSemiring` instance on a Lie ring
or a Lie algebra. 

## BASE-LIBRARY REF NonAssocSemiring
Type u → Type u

Docstring: A unital but not-necessarily-associative semiring. 

## BASE-LIBRARY REF Semiring
Type u → Type u

Docstring: A `Semiring` is a type with addition, multiplication, a `0` and a `1` where addition is
commutative and associative, multiplication is associative and left and right distributive over
addition, and `0` and `1` are additive and multiplicative identities. 

## BASE-LIBRARY REF Semiring.one_mul
∀ {α : Type u} [self : Semiring α] (a : α), 1 * a = a

Docstring: One is a left neutral element for multiplication 

## BASE-LIBRARY REF Semiring.mul_one
∀ {α : Type u} [self : Semiring α] (a : α), a * 1 = a

Docstring: One is a right neutral element for multiplication 

## BASE-LIBRARY REF Finset.filter
{α : Type u_1} → (p : α → Prop) → [DecidablePred p] → Finset α → Finset α

Body:
fun {α} p [DecidablePred p] s => { val := Multiset.filter p s.val, nodup := ⋯ }

Docstring: `Finset.filter p s` is the set of elements of `s` that satisfy `p`.

For example, one can use `s.filter (· ∈ t)` to get the intersection of `s` with `t : Set α`
as a `Finset α` (when a `DecidablePred (· ∈ t)` instance is available). 

## BASE-LIBRARY REF Finsupp.instLE
{ι : Type u_1} → {M : Type u_2} → [inst : Zero M] → [LE M] → LE (ι →₀ M)

Body:
fun {ι} {M} [Zero M] [LE M] => { le := fun f g => ∀ (i : ι), f i ≤ g i }

## BASE-LIBRARY REF Zero
Type u → Type u

Docstring: A type with a zero element. 

## BASE-LIBRARY REF LE
Type u → Type u

Docstring: `LE α` is the typeclass which supports the notation `x ≤ y` where `x y : α`.

## BASE-LIBRARY REF Finsupp.instFunLike
{α : Type u_1} → {M : Type u_4} → [inst : Zero M] → FunLike (α →₀ M) α M

Body:
fun {α} {M} [Zero M] => { coe := Finsupp.toFun, coe_injective' := ⋯ }

## BASE-LIBRARY REF Nat.le
ℕ → ℕ → Prop

Docstring: Non-strict, or weak, inequality of natural numbers, usually accessed via the `≤` operator.


## BASE-LIBRARY REF Finsupp.single
{α : Type u_1} → {M : Type u_5} → [inst : Zero M] → α → M → α →₀ M

Body:
fun {α} {M} [Zero M] a b => { support := if b = 0 then ∅ else {a}, toFun := Pi.single a b, mem_support_toFun := ⋯ }

Docstring: `single a b` is the finitely supported function with value `b` at `a` and zero otherwise. 

## BASE-LIBRARY REF Prod.fst
{α : Type u} → {β : Type v} → α × β → α

Body:
fun α β self => self.1

Docstring: The first element of a pair. 

## BASE-LIBRARY REF instDecidableAnd.match_1
{q : Prop} →
  (motive : Decidable q → Sort u_1) →
    (dq : Decidable q) → ((hq : q) → motive (isTrue hq)) → ((hq : ¬q) → motive (isFalse hq)) → motive dq

Body:
fun {q} motive dq h_1 h_2 => Decidable.casesOn dq (fun h => h_2 h) fun h => h_1 h

## BASE-LIBRARY REF Decidable.isFalse
{p : Prop} → ¬p → Decidable p

Docstring: Proves that `p` is decidable by supplying a proof of `¬p` 

## BASE-LIBRARY REF absurd
{a : Prop} → {b : Sort v} → a → ¬a → b

Body:
fun {a} {b} h₁ h₂ => False.rec (fun x => b) ⋯

Docstring: Anything follows from two contradictory hypotheses. Example:
```
example (hp : p) (hnp : ¬p) : q := absurd hp hnp
```
For more information: [Propositional Logic](https://lean-lang.org/theorem_proving_in_lean4/propositions_and_proofs.html#propositional-logic)


## BASE-LIBRARY REF Decidable.isTrue
{p : Prop} → p → Decidable p

Docstring: Proves that `p` is decidable by supplying a proof of `p` 

## BASE-LIBRARY REF Finsupp.decidableLE
{ι : Type u_1} →
  {α : Type u_3} →
    [inst : AddCommMonoid α] →
      [inst_1 : PartialOrder α] → [CanonicallyOrderedAdd α] → [DecidableLE α] → DecidableLE (ι →₀ α)

Body:
fun {ι} {α} [AddCommMonoid α] [PartialOrder α] [CanonicallyOrderedAdd α] [DecidableLE α] f g =>
  decidable_of_iff (∀ i ∈ f.support, f i ≤ g i) ⋯

## BASE-LIBRARY REF AddCommMonoid
Type u → Type u

Docstring: An additive commutative monoid is an additive monoid with commutative `(+)`. 

## BASE-LIBRARY REF PartialOrder
Type u_2 → Type u_2

Docstring: A partial order is a reflexive, transitive, antisymmetric relation `≤`. 

## BASE-LIBRARY REF CanonicallyOrderedAdd
(α : Type u_1) → [Add α] → [LE α] → Prop

Docstring: An ordered additive monoid is `CanonicallyOrderedAdd`
if the ordering coincides with the subtractibility relation,
which is to say, `a ≤ b` iff there exists `c` with `b = a + c`.
This is satisfied by the natural numbers, for example, but not
the integers or other nontrivial `OrderedAddCommGroup`s.

We have `a ≤ b + a` and `a ≤ a + b` as separate fields. In the commutative case the second field
is redundant, but in the noncommutative case (satisfied most relevantly by the ordinals), this
extra field allows us to prove more things without the extra commutativity assumption. 

## BASE-LIBRARY REF DecidableLE
(α : Type u) → [LE α] → Type (max 0 u)

Body:
fun α [LE α] => DecidableRel LE.le

Docstring: Abbreviation for `DecidableRel (· ≤ · : α → α → Prop)`. 

## BASE-LIBRARY REF decidable_of_iff
{b : Prop} → (a : Prop) → (a ↔ b) → [Decidable a] → Decidable b

Body:
fun {b} a h [Decidable a] => decidable_of_decidable_of_iff h

Docstring: Transfer decidability of `a` to decidability of `b`, if the propositions are equivalent.
**Important**: this function should be used instead of `rw` on `Decidable b`, because the
kernel will get stuck reducing the usage of `propext` otherwise,
and `decide` will not work. 

## BASE-LIBRARY REF Nat.instAddCommMonoid
AddCommMonoid ℕ

Body:
inferInstance

## BASE-LIBRARY REF Nat.instAddCancelCommMonoid
AddCancelCommMonoid ℕ

Body:
{ add := Nat.add, add_assoc := Nat.add_assoc, zero := Nat.zero, zero_add := Nat.zero_add, add_zero := Nat.add_zero,
  nsmul := fun m n => m * n, nsmul_zero := Nat.zero_mul, nsmul_succ := Nat.succ_mul, add_comm := Nat.add_comm,
  toIsLeftCancelAdd := Nat.instAddCancelCommMonoid._proof_1 }

## BASE-LIBRARY REF Nat.instPartialOrder
PartialOrder ℕ

Body:
inferInstance

## BASE-LIBRARY REF Nat.instLinearOrder
LinearOrder ℕ

Body:
{ le := Nat.le, lt := Nat.lt, le_refl := Nat.le_refl, le_trans := @Nat.le_trans,
  lt_iff_le_not_ge := @Nat.lt_iff_le_not_le, le_antisymm := @Nat.le_antisymm, toMin := instMinNat, toMax := Nat.instMax,
  toOrd := instOrdNat, le_total := Nat.le_total, toDecidableLE := inferInstance, toDecidableEq := inferInstance,
  toDecidableLT := inferInstance, min_def := Nat.instLinearOrder._proof_1, max_def := Nat.instLinearOrder._proof_2,
  compare_eq_compareOfLessAndEq := Nat.instLinearOrder._proof_3 }

## BASE-LIBRARY REF Nat.instCanonicallyOrderedAdd
CanonicallyOrderedAdd ℕ

## BASE-LIBRARY REF Nat.decLe
(n m : ℕ) → Decidable (n ≤ m)

Body:
fun n m => if h : n.ble m = true then isTrue ⋯ else isFalse ⋯

Docstring: A decision procedure for non-strict inequality of natural numbers, usually accessed via the
`DecidableLE Nat` instance.

Examples:
 * `(if 3 ≤ 4 then "yes" else "no") = "yes"`
 * `(if 6 ≤ 4 then "yes" else "no") = "no"`
 * `show 12 ≤ 12 by decide`
 * `show 5 ≤ 12 by decide`


## BASE-LIBRARY REF Finset.HasAntidiagonal.antidiagonal
{A : Type u_1} → {inst : AddMonoid A} → [self : Finset.HasAntidiagonal A] → A → Finset (A × A)

Body:
fun A {inst} [self : Finset.HasAntidiagonal A] => self.1

Docstring: The antidiagonal of an element `n` is the finset of pairs `(i, j)` such that `i + j = n`. 

## BASE-LIBRARY REF Finsupp.instAddMonoid
{ι : Type u_1} → {M : Type u_3} → [inst : AddMonoid M] → AddMonoid (ι →₀ M)

Body:
fun {ι} {M} [AddMonoid M] =>
  { toAdd := Finsupp.instAdd, add_assoc := ⋯, toZero := Finsupp.instZero, zero_add := ⋯, add_zero := ⋯,
    nsmul := fun n x => n • x, nsmul_zero := ⋯, nsmul_succ := ⋯ }

## BASE-LIBRARY REF AddMonoid
Type u → Type u

Docstring: An `AddMonoid` is an `AddSemigroup` with an element `0` such that `0 + a = a + 0 = a`. 

## BASE-LIBRARY REF Finsupp.instAdd
{ι : Type u_1} → {M : Type u_3} → [inst : AddZeroClass M] → Add (ι →₀ M)

Body:
fun {ι} {M} [AddZeroClass M] => { add := Finsupp.zipWith (fun x1 x2 => x1 + x2) ⋯ }

## BASE-LIBRARY REF Finsupp.instAddMonoid._proof_3
∀ {ι : Type u_1} {M : Type u_2} [inst : AddMonoid M] (a b c : ι →₀ M), a + b + c = a + (b + c)

## BASE-LIBRARY REF Finsupp.instZero
{α : Type u_1} → {M : Type u_4} → [inst : Zero M] → Zero (α →₀ M)

Body:
fun {α} {M} [Zero M] => { zero := { support := ∅, toFun := 0, mem_support_toFun := ⋯ } }

## BASE-LIBRARY REF Finsupp.instAddMonoid._proof_5
∀ {ι : Type u_1} {M : Type u_2} [inst : AddMonoid M] (a : ι →₀ M), 0 + a = a

## BASE-LIBRARY REF Finsupp.instAddMonoid._proof_6
∀ {ι : Type u_1} {M : Type u_2} [inst : AddMonoid M] (a : ι →₀ M), a + 0 = a

## BASE-LIBRARY REF Finsupp.instNatSMul
{ι : Type u_1} → {M : Type u_3} → [inst : AddMonoid M] → SMul ℕ (ι →₀ M)

Body:
fun {ι} {M} [AddMonoid M] => { smul := fun n v => Finsupp.mapRange (fun x => n • x) ⋯ v }

Docstring: Note the general `SMul` instance for `Finsupp` doesn't apply as `ℕ` is not distributive
unless `F i`'s addition is commutative. 

## BASE-LIBRARY REF Finsupp.instAddMonoid._proof_7
∀ {ι : Type u_1} {M : Type u_2} [inst : AddMonoid M] (x : ι →₀ M), 0 • x = 0

## BASE-LIBRARY REF Finsupp.instHasAntidiagonal
{α : Type u} → [DecidableEq α] → Finset.HasAntidiagonal (α →₀ ℕ)

Body:
fun {α} [DecidableEq α] => { antidiagonal := fun f => f.antidiagonal'.support, mem_antidiagonal := ⋯ }

Docstring: The antidiagonal of `s : α →₀ ℕ` is the finset of all pairs `(t₁, t₂) : (α →₀ ℕ) × (α →₀ ℕ)`
such that `t₁ + t₂ = s`. 

## BASE-LIBRARY REF Add
Type u → Type u

Docstring: The homogeneous version of `HAdd`: `a + b : α` where `a b : α`. 

## BASE-LIBRARY REF Add.add
{α : Type u} → [self : Add α] → α → α → α

Body:
fun α [self : Add α] => self.1

Docstring: `a + b` computes the sum of `a` and `b`. See `HAdd`. 

## BASE-LIBRARY REF Mul
Type u → Type u

Docstring: The homogeneous version of `HMul`: `a * b : α` where `a b : α`. 

## BASE-LIBRARY REF Mul.mul
{α : Type u} → [self : Mul α] → α → α → α

Body:
fun α [self : Mul α] => self.1

Docstring: `a * b` computes the product of `a` and `b`. See `HMul`. 

## BASE-LIBRARY REF Distrib
Type u_1 → Type u_1

Docstring: A typeclass stating that multiplication is left and right distributive
over addition. 

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.left_distrib
∀ {α : Type u} [self : NonUnitalNonAssocSemiring α] (a b c : α), a * (b + c) = a * b + a * c

Docstring: Multiplication is left distributive over addition 

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.right_distrib
∀ {α : Type u} [self : NonUnitalNonAssocSemiring α] (a b c : α), (a + b) * c = a * c + b * c

Docstring: Multiplication is right distributive over addition 

## BASE-LIBRARY REF AddMonoidWithOne
Type u_2 → Type u_2

Docstring: An `AddMonoidWithOne` is an `AddMonoid` with a `1`.
It also contains data for the unique homomorphism `ℕ → R`. 

## BASE-LIBRARY REF AddCommMonoidWithOne
Type u_2 → Type u_2

Docstring: An `AddCommMonoidWithOne` is an `AddMonoidWithOne` satisfying `a + b = b + a`. 

## BASE-LIBRARY REF AddCommMonoid.add_comm
∀ {M : Type u} [self : AddCommMonoid M] (a b : M), a + b = b + a

Docstring: Addition is commutative in a commutative additive magma. 

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

Body:
fun α [NonAssocSemiring α] => { toFun := id, map_one' := ⋯, map_mul' := ⋯, map_zero' := ⋯, map_add' := ⋯ }

Docstring: The identity ring homomorphism from a semiring to itself. 

## BASE-LIBRARY REF MvPowerSeries.instAddCommMonoid
{σ : Type u_1} → {R : Type u_2} → [AddCommMonoid R] → AddCommMonoid (MvPowerSeries σ R)

Body:
fun {σ} {R} [AddCommMonoid R] => Pi.addCommMonoid

## BASE-LIBRARY REF Pi.addCommMonoid
{I : Type u} → {f : I → Type v₁} → [(i : I) → AddCommMonoid (f i)] → AddCommMonoid ((i : I) → f i)

Body:
fun {I} {f} [(i : I) → AddCommMonoid (f i)] =>
  let __src := Pi.addMonoid;
  have __src_1 := Pi.addCommSemigroup;
  { toAddMonoid := __src, add_comm := ⋯ }

## BASE-LIBRARY REF MvPowerSeries.instModule
{σ : Type u_1} →
  {R : Type u_2} →
    {A : Type u_3} →
      [inst : Semiring R] → [inst_1 : AddCommMonoid A] → [_root_.Module R A] → _root_.Module R (MvPowerSeries σ A)

Body:
fun {σ} {R} {A} [Semiring R] [AddCommMonoid A] [_root_.Module R A] => Pi.module (σ →₀ ℕ) (fun a => A) R

## BASE-LIBRARY REF Module
(R : Type u) → (M : Type v) → [Semiring R] → [AddCommMonoid M] → Type (max u v)

Docstring: A module is a generalization of vector spaces to a scalar semiring.
It consists of a scalar semiring `R` and an additive monoid of "vectors" `M`,
connected by a "scalar multiplication" operation `r • x : M`
(where `r : R` and `x : M`) with some natural associativity and
distributivity axioms similar to those on a ring. 

## BASE-LIBRARY REF Pi.module
(I : Type u) →
  (f : I → Type v) →
    (α : Type u_1) →
      {r : Semiring α} →
        {m : (i : I) → AddCommMonoid (f i)} → [(i : I) → _root_.Module α (f i)] → _root_.Module α ((i : I) → f i)

Body:
fun I f α {r} {m} [(i : I) → _root_.Module α (f i)] =>
  let __src := Pi.distribMulAction α;
  { toDistribMulAction := __src, add_smul := ⋯, zero_smul := ⋯ }

## BASE-LIBRARY REF Semiring.toModule._proof_1
∀ {R : Type u_1} [inst : Semiring R] (a : R), a * 0 = 0

## BASE-LIBRARY REF Semiring.toModule._proof_2
∀ {R : Type u_1} [inst : Semiring R] (a b c : R), a * (b + c) = a * b + a * c

## BASE-LIBRARY REF Semiring.toModule._proof_3
∀ {R : Type u_1} [inst : Semiring R] (a b c : R), (a + b) * c = a * c + b * c

## BASE-LIBRARY REF Semiring.toModule._proof_4
∀ {R : Type u_1} [inst : Semiring R] (a : R), 0 * a = 0

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

Body:
fun {R} {S} {M} {M₃} [Semiring R] [Semiring S] [AddCommMonoid M] [AddCommMonoid M₃] [_root_.Module R M]
    [_root_.Module S M₃] {σ} =>
  { coe := fun f => f.toFun, coe_injective' := ⋯ }

## BASE-LIBRARY REF RingHom
(α : Type u_5) → (β : Type u_6) → [NonAssocSemiring α] → [NonAssocSemiring β] → Type (max u_5 u_6)

Docstring: Bundled semiring homomorphisms; use this for bundled ring homomorphisms too.

This extends from both `MonoidHom` and `MonoidWithZeroHom` in order to put the fields in a
sensible order, even though `MonoidWithZeroHom` already extends `MonoidHom`. 

## BASE-LIBRARY REF LinearMap.instFunLike._proof_1
∀ {R : Type u_3} {S : Type u_4} {M : Type u_2} {M₃ : Type u_1} [inst : Semiring R] [inst_1 : Semiring S]
  [inst_2 : AddCommMonoid M] [inst_3 : AddCommMonoid M₃] [inst_4 : _root_.Module R M] [inst_5 : _root_.Module S M₃]
  {σ : R →+* S} (f g : M →ₛₗ[σ] M₃), (fun f => f.toFun) f = (fun f => f.toFun) g → f = g

## BASE-LIBRARY REF MvPowerSeries.coeff
{σ : Type u_1} → {R : Type u_2} → [inst : Semiring R] → (σ →₀ ℕ) → MvPowerSeries σ R →ₗ[R] R

Body:
fun {σ} {R} [Semiring R] n => LinearMap.proj n

Docstring: The `n`th coefficient of a multivariate formal power series. 

## BASE-LIBRARY REF Prod.snd
{α : Type u} → {β : Type v} → α × β → β

Body:
fun α β self => self.2

Docstring: The second element of a pair. 

## BASE-LIBRARY REF Zero.zero
{α : Type u} → [self : Zero α] → α

Body:
fun α [self : Zero α] => self.1

Docstring: The zero element of the type. 

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.zero_mul
∀ {α : Type u} [self : NonUnitalNonAssocSemiring α] (a : α), 0 * a = 0

Docstring: Zero is a left absorbing element for multiplication 

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.mul_zero
∀ {α : Type u} [self : NonUnitalNonAssocSemiring α] (a : α), a * 0 = 0

Docstring: Zero is a right absorbing element for multiplication 

## INFORMAL STATEMENT
lem.fps.mulvar.sum-filter-zero-fst

\leanhelper  In the sum over $\operatorname {antidiagonal}(\mathbf{m} + \mathbf{e}_i)$, the terms with $a_i = 0$ (i.e., $\mathbf{e}_i \not\leq \mathbf{a}$) contribute zero to $\sum _{(\mathbf{a},\mathbf{b})} a_i \cdot [{\mathbf{x}}^{\mathbf{a}}]\,  f \cdot [{\mathbf{x}}^{\mathbf{b}}]\,  g$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.mulvar.partialderiv
def.fps.mulvar.partialDeriv

\leanhelper  Let $\sigma $ be a type of variable indices and let $i \in \sigma $. The \emph{partial derivative} of a multivariate power series $f = \sum _{\mathbf{m}} a_{\mathbf{m}}\,  \mathbf{x}^{\mathbf{m}}$ with respect to $x_i$ is the power series 

\[  \frac{\partial f}{\partial x_i} = \sum _{\mathbf{m}} (m_i + 1) \cdot a_{\mathbf{m} + \mathbf{e}_i} \cdot \mathbf{x}^{\mathbf{m}},  \]

 where $\mathbf{e}_i$ is the $i$-th standard basis vector (i.e., $\mathbf{e}_i = (\delta _{j,i})_{j \in \sigma }$). 

This defines an $R$-linear map $\partial /\partial x_i \colon R[[\mathbf{x}]] \to R[[\mathbf{x}]]$.

## VERDICT
{
  "verdict": "faithful",
  "discrepancies": [],
  "justification": "The formal theorem exactly states that the filtered contribution is zero: it sums over `Finset.antidiagonal (m + fun\u2080 | i => 1)` subject to `\u00ac(fun\u2080 | i => 1) \u2264 p.1`, and concludes that the sum of `\u2191(p.1 i) * coeff p.1 f * coeff p.2 g` is `0`. This matches the blueprint\u2019s \u201cterms with `a_i = 0` (i.e., `e_i \u2270 a`) contribute zero\u201d to the indicated coefficient sum. The pointwise order on `Finsupp` and the body of `Finsupp.single` make the filter precisely the stated standard-basis condition. `[DecidableEq \u03c3]` supplies the finite antidiagonal/singleton encoding, while `[CommSemiring R]` supplies the coefficient arithmetic; neither changes the asserted mathematical content."
}