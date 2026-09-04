## TARGET AlgebraicCombinatorics.SymmetricPolynomials.psum_generates_symmetric (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] {N : ℕ} [Algebra ℚ K] [IsDomain K]
  (f : ↥(AlgebraicCombinatorics.SymmetricPolynomials.S K N)),
  ∃! g, (MvPolynomial.aeval fun i => MvPolynomial.psum (Fin N) K (↑i + 1)) g = ↑f

Docstring: Over a ℚ-algebra, every symmetric polynomial can be uniquely written as a polynomial
in p_1, ..., p_N.
(Theorem thm.sf.ftsf (c), generation part).
Label: thm.sf.ftsf 

## TARGET AlgebraicCombinatorics.SymmetricPolynomials.esymm_generates_symmetric (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] {N : ℕ} (f : ↥(AlgebraicCombinatorics.SymmetricPolynomials.S K N)),
  ∃! g, (MvPolynomial.esymmAlgHom (Fin N) K N) g = f

Docstring: Every symmetric polynomial can be uniquely written as a polynomial in e_1, ..., e_N.
(Theorem thm.sf.ftsf (a), generation part).
Label: thm.sf.ftsf 

## TARGET AlgebraicCombinatorics.SymmetricPolynomials.psum_algebraicIndependent (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] {N : ℕ} [Algebra ℚ K] [IsDomain K],
  AlgebraicIndependent K fun i => MvPolynomial.psum (Fin N) K (↑i + 1)

Docstring: The power sums p_1, ..., p_N are algebraically independent over a ℚ-algebra.
(Theorem thm.sf.ftsf (c), algebraic independence part).

The proof follows the same strategy as for hsymm_algebraicIndependent:
1. The map aeval psum lands in S K N (since psum is symmetric)
2. Factor aeval psum as: MvPolynomial → S K N → P K N
3. The composition esymmAlgEquiv'.symm ∘ (factored map) : MvPolynomial → MvPolynomial is surjective
   (because X_i = esymmAlgEquiv'.symm (esymm (i+1)) and esymm is in the range by Newton's identities)
4. A surjective algebra endomorphism of K[X_1, ..., X_n] is bijective (transcendence degree argument)
5. Therefore the factored map is bijective, hence aeval psum is injective

Label: thm.sf.ftsf 

## TARGET AlgebraicCombinatorics.SymmetricPolynomials.esymm_algebraicIndependent (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] {N : ℕ}, AlgebraicIndependent K fun i => MvPolynomial.esymm (Fin N) K (↑i + 1)

Docstring: The elementary symmetric polynomials e_1, ..., e_N are algebraically independent.
This means: if P(e_1, ..., e_N) = 0 for some polynomial P ∈ K[y_1, ..., y_N], then P = 0.
(Theorem thm.sf.ftsf (a), algebraic independence part).
Label: thm.sf.ftsf 

## TARGET AlgebraicCombinatorics.SymmetricPolynomials.hsymm_algebraicIndependent (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] {N : ℕ} [inst_1 : DecidableEq (Fin N)] [IsDomain K],
  AlgebraicIndependent K fun i => MvPolynomial.hsymm (Fin N) K (↑i + 1)

Docstring: The complete homogeneous symmetric polynomials h_1, ..., h_N are algebraically independent.
(Theorem thm.sf.ftsf (b), algebraic independence part).

The proof uses the Newton-Girard relations to show that the map sending polynomials
to their evaluation at h_1, ..., h_N factors through the symmetric subalgebra S,
and this factored map is bijective.

Key steps:
1. The map aeval hsymm lands in S K N (since hsymm is symmetric)
2. Factor aeval hsymm as: MvPolynomial → S K N → P K N
3. The composition esymmAlgEquiv'.symm ∘ (factored map) : MvPolynomial → MvPolynomial is surjective
   (because X_i = esymmAlgEquiv'.symm (esymm (i+1)) and esymm is in the range by Newton-Girard)
4. A surjective algebra endomorphism of K[X_1, ..., X_n] is bijective
5. Therefore the factored map is bijective, hence aeval hsymm is injective

Label: thm.sf.ftsf 

## TARGET AlgebraicCombinatorics.SymmetricPolynomials.hsymm_generates_symmetric (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] {N : ℕ} [inst_1 : DecidableEq (Fin N)] [IsDomain K]
  (f : ↥(AlgebraicCombinatorics.SymmetricPolynomials.S K N)),
  ∃! g, (MvPolynomial.aeval fun i => MvPolynomial.hsymm (Fin N) K (↑i + 1)) g = ↑f

Docstring: Every symmetric polynomial can be uniquely written as a polynomial in h_1, ..., h_N.
(Theorem thm.sf.ftsf (b), generation part).
Label: thm.sf.ftsf 

## TARGET AlgebraicCombinatorics.SymmetricPolynomials.esymmAlgEquiv' (def) — ELABORATED SIGNATURE
{K : Type u_1} →
  [inst : CommRing K] → {N : ℕ} → MvPolynomial (Fin N) K ≃ₐ[K] ↥(AlgebraicCombinatorics.SymmetricPolynomials.S K N)

Body:
fun {K} [CommRing K] {N} => MvPolynomial.esymmAlgEquiv (Fin N) K ⋯

Docstring: The elementary symmetric polynomials e_1, ..., e_N generate the symmetric subalgebra
and the map g ↦ g[e_1, ..., e_N] is a K-algebra isomorphism.
(Theorem thm.sf.ftsf (a)).
Label: thm.sf.ftsf 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SymmetricPolynomials.P (def)
(K : Type u_2) → [CommRing K] → ℕ → Type u_2

Body:
fun K [CommRing K] N => MvPolynomial (Fin N) K

Docstring: The polynomial ring in N variables over K.
This corresponds to 𝒫 in the source (Definition def.sf.PS (a)).
Label: def.sf.PS 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SymmetricPolynomials.S (def)
(K : Type u_2) → [inst : CommRing K] → (N : ℕ) → Subalgebra K (AlgebraicCombinatorics.SymmetricPolynomials.P K N)

Body:
fun K [CommRing K] N => MvPolynomial.symmetricSubalgebra (Fin N) K

Docstring: The ring of symmetric polynomials in N variables over K.

This is the K-subalgebra S of P consisting of all symmetric polynomials,
i.e., polynomials f such that σ · f = f for all permutations σ ∈ S_N.

The terminology "ring of symmetric polynomials" comes from the fact that
this subalgebra is closed under addition, multiplication, and scalar
multiplication by elements of K (Theorem thm.sf.S-subalg).

Label: def.sf.ring-of-symm 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SymmetricPolynomials.P_isAlgebra' (def)
{K : Type u_1} → [inst : CommRing K] → {N : ℕ} → Algebra K (AlgebraicCombinatorics.SymmetricPolynomials.P K N)

Body:
fun {K} [CommRing K] {N} => inferInstance

Docstring: The polynomial ring P K N is a K-algebra.
Label: def.sf.PS 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SymmetricPolynomials.P_isCommRing' (def)
{K : Type u_1} → [inst : CommRing K] → {N : ℕ} → CommRing (AlgebraicCombinatorics.SymmetricPolynomials.P K N)

Body:
fun {K} [CommRing K] {N} => inferInstance

Docstring: The polynomial ring P K N is a commutative K-algebra.
Label: def.sf.PS 

## BASE-LIBRARY REF CommRing
Type u → Type u

Docstring: A commutative ring is a ring with commutative multiplication. 

## BASE-LIBRARY REF Algebra
(R : Type u) → (A : Type v) → [CommSemiring R] → [Semiring A] → Type (max u v)

Docstring: An associative unital `R`-algebra is a semiring `A` equipped with a map into its center `R → A`.

See the implementation notes in this file for discussion of the details of this definition.


## BASE-LIBRARY REF Rat
Type

Docstring: Rational numbers, implemented as a pair of integers `num / den` such that the
denominator is positive and the numerator and denominator are coprime.


## BASE-LIBRARY REF Rat.commSemiring
CommSemiring ℚ

Body:
inferInstance

## BASE-LIBRARY REF CommSemiring
Type u → Type u

Docstring: A commutative semiring is a semiring with commutative multiplication. 

## BASE-LIBRARY REF Rat.commRing
CommRing ℚ

Body:
let __spread.0 := Rat.addCommGroup;
let __spread.1 := Rat.commMonoid;
{ toAddMonoid := __spread.0.toAddMonoid, add_comm := ⋯, toMul := __spread.1.toMul, left_distrib := Rat.mul_add,
  right_distrib := Rat.add_mul, zero_mul := Rat.zero_mul, mul_zero := Rat.mul_zero, mul_assoc := Rat.commRing._proof_1,
  toOne := __spread.1.toOne, one_mul := Rat.commRing._proof_5, mul_one := Rat.commRing._proof_6,
  natCast := fun n => ↑↑n, natCast_zero := Rat.commRing._proof_7, natCast_succ := ⋯, npow := Monoid.npow,
  npow_zero := Rat.commRing._proof_8, npow_succ := Rat.commRing._proof_9, toNeg := __spread.0.t …

## BASE-LIBRARY REF IsDomain
(α : Type u) → [Semiring α] → Prop

Docstring: A domain is a nontrivial semiring such that multiplication by a nonzero element
is cancellative on both sides. In other words, a nontrivial semiring `R` satisfying
`∀ {a b c : R}, a ≠ 0 → a * b = a * c → b = c` and
`∀ {a b c : R}, b ≠ 0 → a * b = c * b → a = c`.

This is implemented as a mixin for `Semiring α`.
To obtain an integral domain use `[CommRing α] [IsDomain α]`. 

## BASE-LIBRARY REF Subalgebra
(R : Type u) → (A : Type v) → [inst : CommSemiring R] → [inst_1 : Semiring A] → [Algebra R A] → Type v

Docstring: A subalgebra is a sub(semi)ring that includes the range of `algebraMap`. 

## BASE-LIBRARY REF MvPolynomial.commSemiring
{R : Type u} → {σ : Type u_1} → [inst : CommSemiring R] → CommSemiring (MvPolynomial σ R)

Body:
fun {R} {σ} [CommSemiring R] => AddMonoidAlgebra.commSemiring

## BASE-LIBRARY REF AddMonoidAlgebra.commSemiring
{R : Type u_1} → {M : Type u_4} → [inst : CommSemiring R] → [AddCommMonoid M] → CommSemiring (AddMonoidAlgebra R M)

Body:
fun {R} {M} [CommSemiring R] [AddCommMonoid M] => { toSemiring := AddMonoidAlgebra.semiring, mul_comm := ⋯ }

## BASE-LIBRARY REF Finsupp
Type u_9 → (M : Type u_10) → [Zero M] → Type (max u_10 u_9)

Docstring: `Finsupp α M`, denoted `α →₀ M`, is the type of functions `f : α → M` such that
`f x = 0` for all but finitely many `x`. 

## BASE-LIBRARY REF Nat.instMulZeroClass
MulZeroClass ℕ

Body:
{ toMul := instMulNat, toZero := Nat.instAddMonoid.toAddZeroClass.toZero, zero_mul := Nat.zero_mul,
  mul_zero := Nat.mul_zero }

## BASE-LIBRARY REF Finsupp.instAddCommMonoid
{ι : Type u_1} → {M : Type u_3} → [inst : AddCommMonoid M] → AddCommMonoid (ι →₀ M)

Body:
fun {ι} {M} [AddCommMonoid M] => { toAddMonoid := Finsupp.instAddMonoid, add_comm := ⋯ }

## BASE-LIBRARY REF Nat.instAddCommMonoid
AddCommMonoid ℕ

Body:
inferInstance

## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


## BASE-LIBRARY REF MvPolynomial.algebra
{R : Type u} →
  {S₁ : Type v} →
    {σ : Type u_1} →
      [inst : CommSemiring R] → [inst_1 : CommSemiring S₁] → [Algebra R S₁] → Algebra R (MvPolynomial σ S₁)

Body:
fun {R} {S₁} {σ} [CommSemiring R] [CommSemiring S₁] [Algebra R S₁] => AddMonoidAlgebra.algebra

## BASE-LIBRARY REF AddMonoidAlgebra.algebra
{R : Type u_1} →
  {A : Type u_4} →
    {M : Type u_7} →
      [inst : CommSemiring R] →
        [inst_1 : Semiring A] → [Algebra R A] → [inst_3 : AddMonoid M] → Algebra R (AddMonoidAlgebra A M)

Body:
fun {R} {A} {M} [CommSemiring R] [Semiring A] [Algebra R A] [AddMonoid M] =>
  { toSMul := AddMonoidAlgebra.smulZeroClass.toSMul,
    algebraMap := AddMonoidAlgebra.singleZeroRingHom.comp (algebraMap R A), commutes' := ⋯, smul_def' := ⋯ }

Docstring: The instance `Algebra R R[M]` whenever we have `Algebra R R`.

In particular this provides the instance `Algebra R R[M]`. 

## BASE-LIBRARY REF Algebra.id
(R : Type u) → [inst : CommSemiring R] → Algebra R R

Docstring: The identity map inducing an `Algebra` structure. 

## BASE-LIBRARY REF SetLike
Type u_1 → outParam (Type u_2) → Type (max u_1 u_2)

Docstring: A class to indicate that there is a canonical injection between `A` and `Set B`.

This has the effect of giving terms of `A` elements of type `B` (through a `Membership`
instance) and a compatible coercion to `Type*` as a subtype.

Note: if `SetLike.coe` is a projection, implementers should create a simp lemma such as
```
@[simp] lemma mem_carrier {p : MySubobject X} : x ∈ p.carrier ↔ x ∈ (p : Set X) := Iff.rfl
```
to normalize terms.

If you declare an unbundled subclass of `SetLike`, for example:
```
class MulMemClass (S : Type*) (M : Type*) [Mul M] [SetLike S M] where
  ...
```
Then you should *not* repeat the `outParam` declaration so `SetLike` will supply the value instead.
This ensures your subclass will not have issues with synthesis of the `[Mul M]` parameter starting
before the value of `M` is known.


## BASE-LIBRARY REF SetLike.coe
{A : Type u_1} → {B : outParam (Type u_2)} → [self : SetLike A B] → A → Set B

Body:
fun A {B} [self : SetLike A B] => self.1

Docstring: The coercion from a term of a `SetLike` to its corresponding `Set`. 

## BASE-LIBRARY REF Subalgebra.instSetLike
{R : Type u} →
  {A : Type v} → [inst : CommSemiring R] → [inst_1 : Semiring A] → [inst_2 : Algebra R A] → SetLike (Subalgebra R A) A

Body:
fun {R} {A} [CommSemiring R] [Semiring A] [Algebra R A] => { coe := fun s => s.carrier, coe_injective' := ⋯ }

## BASE-LIBRARY REF Semiring
Type u → Type u

Docstring: A `Semiring` is a type with addition, multiplication, a `0` and a `1` where addition is
commutative and associative, multiplication is associative and left and right distributive over
addition, and `0` and `1` are additive and multiplicative identities. 

## BASE-LIBRARY REF Subsemigroup.carrier
{M : Type u_3} → [inst : Mul M] → Subsemigroup M → Set M

Body:
fun M [Mul M] self => self.1

Docstring: The carrier of a subsemigroup. 

## BASE-LIBRARY REF ExistsUnique
{α : Sort u_1} → (α → Prop) → Prop

Body:
fun {α} p => ∃ x, p x ∧ ∀ (y : α), p y → y = x

Docstring: For `p : α → Prop`, `ExistsUnique p` means that there exists a unique `x : α` with `p x`. 

## BASE-LIBRARY REF MvPolynomial
Type u_1 → (R : Type u_2) → [CommSemiring R] → Type (max u_2 u_1)

Body:
fun σ R [CommSemiring R] => AddMonoidAlgebra R (σ →₀ ℕ)

Docstring: Multivariate polynomial, where `σ` is the index set of the variables and
`R` is the coefficient ring 

## BASE-LIBRARY REF AlgHom
(R : Type u) →
  (A : Type v) →
    (B : Type w) →
      [inst : CommSemiring R] →
        [inst_1 : Semiring A] → [inst_2 : Semiring B] → [Algebra R A] → [Algebra R B] → Type (max v w)

Docstring: Defining the homomorphism in the category R-Alg, denoted `A →ₐ[R] B`. 

## BASE-LIBRARY REF AlgHom.funLike
{R : Type u} →
  {A : Type v} →
    {B : Type w} →
      [inst : CommSemiring R] →
        [inst_1 : Semiring A] →
          [inst_2 : Semiring B] → [inst_3 : Algebra R A] → [inst_4 : Algebra R B] → FunLike (A →ₐ[R] B) A B

Body:
fun {R} {A} {B} [CommSemiring R] [Semiring A] [Semiring B] [Algebra R A] [Algebra R B] =>
  { coe := fun f => (↑↑f.toRingHom).toFun, coe_injective' := ⋯ }

## BASE-LIBRARY REF AlgHom.funLike._proof_1
∀ {R : Type u_3} {A : Type u_1} {B : Type u_2} [inst : CommSemiring R] [inst_1 : Semiring A] [inst_2 : Semiring B]
  [inst_3 : Algebra R A] [inst_4 : Algebra R B] (f g : A →ₐ[R] B),
  (fun f => (↑↑f.toRingHom).toFun) f = (fun f => (↑↑f.toRingHom).toFun) g → f = g

## BASE-LIBRARY REF MvPolynomial.aeval
{R : Type u} →
  {S₁ : Type v} →
    {σ : Type u_1} →
      [inst : CommSemiring R] →
        [inst_1 : CommSemiring S₁] → [inst_2 : Algebra R S₁] → (σ → S₁) → MvPolynomial σ R →ₐ[R] S₁

Body:
fun {R} {S₁} {σ} [CommSemiring R] [CommSemiring S₁] [Algebra R S₁] f =>
  let __src := MvPolynomial.eval₂Hom (algebraMap R S₁) f;
  { toRingHom := __src, commutes' := ⋯ }

Docstring: A map `σ → S₁` where `S₁` is an algebra over `R` generates an `R`-algebra homomorphism
from multivariate polynomials over `σ` to `S₁`. 

## BASE-LIBRARY REF MvPolynomial.psum
(σ : Type u_5) → (R : Type u_6) → [inst : CommSemiring R] → [Fintype σ] → ℕ → MvPolynomial σ R

Body:
fun σ R [CommSemiring R] [Fintype σ] n => ∑ i, MvPolynomial.X i ^ n

Docstring: The degree-`n` power sum symmetric `MvPolynomial σ R`.
It is the sum over all the `n`-th powers of the variables. 

## BASE-LIBRARY REF Fin.fintype
(n : ℕ) → Fintype (Fin n)

Body:
fun n => { elems := { val := ↑(List.finRange n), nodup := ⋯ }, complete := ⋯ }

## BASE-LIBRARY REF Multiset.ofList
{α : Type u_1} → List α → Multiset α

Body:
fun {α} => Quot.mk ⇑(List.isSetoid α)

Docstring: The quotient map from `List α` to `Multiset α`. 

## BASE-LIBRARY REF List.finRange
(n : ℕ) → List (Fin n)

Body:
fun n => List.ofFn fun i => i

Docstring: Lists all elements of `Fin n` in order, starting at `0`.

Examples:
* `List.finRange 0 = ([] : List (Fin 0))`
* `List.finRange 2 = ([0, 1] : List (Fin 2))`


## BASE-LIBRARY REF List.nodup_finRange
∀ (n : ℕ), (List.finRange n).Nodup

## BASE-LIBRARY REF List.mem_finRange
∀ {n : ℕ} (x : Fin n), x ∈ List.finRange n

## BASE-LIBRARY REF Add
Type u → Type u

Docstring: The homogeneous version of `HAdd`: `a + b : α` where `a b : α`. 

## BASE-LIBRARY REF Add.add
{α : Type u} → [self : Add α] → α → α → α

Body:
fun α [self : Add α] => self.1

Docstring: `a + b` computes the sum of `a` and `b`. See `HAdd`. 

## BASE-LIBRARY REF Nat.add
ℕ → ℕ → ℕ

Body:
fun x x_1 =>
  Nat.brecOn (motive := fun x => ℕ → ℕ) x_1
    (fun x f x_2 =>
      (match (motive := ℕ → (x : ℕ) → Nat.below (motive := fun x => ℕ → ℕ) x → ℕ) x_2, x with
        | a, Nat.zero => fun x => a
        | a, b.succ => fun x => (x.1 a).succ)
        f)
    x

Docstring: Addition of natural numbers, typically used via the `+` operator.

This function is overridden in both the kernel and the compiler to efficiently evaluate using the
arbitrary-precision arithmetic library. The definition provided here is the logical model.


## BASE-LIBRARY REF Fin.val
{n : ℕ} → Fin n → ℕ

Body:
fun n self => self.1

Docstring: The number that is strictly less than `n`.

`Fin.val` is a coercion, so any `Fin n` can be used in a position where a `Nat` is expected.


## BASE-LIBRARY REF MvPolynomial.symmetricSubalgebra
(σ : Type u_5) → (R : Type u_6) → [inst : CommSemiring R] → Subalgebra R (MvPolynomial σ R)

Body:
fun σ R [CommSemiring R] =>
  { carrier := setOf MvPolynomial.IsSymmetric, mul_mem' := ⋯, one_mem' := ⋯, add_mem' := ⋯, zero_mem' := ⋯,
    algebraMap_mem' := ⋯ }

Docstring: The subalgebra of symmetric `MvPolynomial`s. 

## BASE-LIBRARY REF Subalgebra.algebra
{R : Type u} →
  {A : Type v} →
    [inst : CommSemiring R] → [inst_1 : Semiring A] → [inst_2 : Algebra R A] → (S : Subalgebra R A) → Algebra R ↥S

Body:
fun {R} {A} [CommSemiring R] [Semiring A] [Algebra R A] S => S.algebra'

## BASE-LIBRARY REF Subalgebra.algebra'
{R' : Type u'} →
  {R : Type u} →
    {A : Type v} →
      [inst : CommSemiring R] →
        [inst_1 : Semiring A] →
          [inst_2 : Algebra R A] →
            (S : Subalgebra R A) →
              [inst_3 : CommSemiring R'] →
                [inst_4 : SMul R' R] → [inst_5 : Algebra R' A] → [IsScalarTower R' R A] → Algebra R' ↥S

Body:
fun {R'} {R} {A} [CommSemiring R] [Semiring A] [Algebra R A] S [CommSemiring R'] [SMul R' R] [Algebra R' A]
    [IsScalarTower R' R A] =>
  { toSMul := DistribMulAction.toDistribSMul.toSMul, algebraMap := (algebraMap R' A).codRestrict S ⋯, commutes' := ⋯,
    smul_def' := ⋯ }

## BASE-LIBRARY REF Subalgebra.instModuleSubtypeMem._proof_1
∀ {R : Type u_1} {A : Type u_2} [inst : CommSemiring R] [inst_1 : Semiring A] [inst_2 : Algebra R A],
  IsScalarTower R R A

## BASE-LIBRARY REF MvPolynomial.esymmAlgHom
(σ : Type u_1) →
  (R : Type u_3) →
    (n : ℕ) →
      [inst : CommSemiring R] → [Fintype σ] → MvPolynomial (Fin n) R →ₐ[R] ↥(MvPolynomial.symmetricSubalgebra σ R)

Body:
fun σ R n [CommSemiring R] [Fintype σ] => MvPolynomial.aeval fun i => ⟨MvPolynomial.esymm σ R (↑i + 1), ⋯⟩

Docstring: The `R`-algebra homomorphism from $R[x_1,\dots,x_n]$ to the symmetric subalgebra of
$R[\{x_i \mid i ∈ σ\}]$ sending $x_i$ to the $i$-th elementary symmetric polynomial. 

## BASE-LIBRARY REF AlgebraicIndependent
{ι : Type u_1} →
  (R : Type u_3) → {A : Type u_5} → (ι → A) → [inst : CommRing R] → [inst_1 : CommRing A] → [Algebra R A] → Prop

Body:
fun {ι} R {A} x [CommRing R] [CommRing A] [Algebra R A] => Function.Injective ⇑(MvPolynomial.aeval x)

Docstring: `AlgebraicIndependent R x` states the family of elements `x`
is algebraically independent over `R`, meaning that the canonical
map out of the multivariable polynomial ring is injective. 

## BASE-LIBRARY REF MvPolynomial.esymm
(σ : Type u_5) → (R : Type u_6) → [inst : CommSemiring R] → [Fintype σ] → ℕ → MvPolynomial σ R

Body:
fun σ R [CommSemiring R] [Fintype σ] n => ∑ t ∈ Finset.powersetCard n Finset.univ, ∏ i ∈ t, MvPolynomial.X i

Docstring: The `n`th elementary symmetric `MvPolynomial σ R`.
It is the sum over all the degree n squarefree monomials in `MvPolynomial σ R`. 

## BASE-LIBRARY REF MvPolynomial.hsymm
(σ : Type u_5) → (R : Type u_6) → [inst : CommSemiring R] → [Fintype σ] → [DecidableEq σ] → ℕ → MvPolynomial σ R

Body:
fun σ R [CommSemiring R] [Fintype σ] [DecidableEq σ] n => ∑ s, (Multiset.map MvPolynomial.X ↑s).prod

Docstring: The `n`th complete homogeneous symmetric `MvPolynomial σ R`.
It is the sum over all the degree n monomials in `MvPolynomial σ R`. 

## BASE-LIBRARY REF AlgEquiv
(R : Type u) →
  (A : Type v) →
    (B : Type w) →
      [inst : CommSemiring R] →
        [inst_1 : Semiring A] → [inst_2 : Semiring B] → [Algebra R A] → [Algebra R B] → Type (max v w)

Docstring: An equivalence of algebras (denoted as `A ≃ₐ[R] B`)
is an equivalence of rings commuting with the actions of scalars. 

## BASE-LIBRARY REF MvPolynomial.esymmAlgEquiv
(σ : Type u_1) →
  (R : Type u_3) →
    {n : ℕ} →
      [inst : Fintype σ] →
        [inst_1 : CommRing R] →
          Fintype.card σ = n → MvPolynomial (Fin n) R ≃ₐ[R] ↥(MvPolynomial.symmetricSubalgebra σ R)

Body:
fun σ R {n} [Fintype σ] [CommRing R] hn => AlgEquiv.ofBijective (MvPolynomial.esymmAlgHom σ R n) ⋯

Docstring: If the cardinality of `σ` is `n`, then `esymmAlgHom σ R n` is an isomorphism. 

## BASE-LIBRARY REF Fintype.card_fin
∀ (n : ℕ), Fintype.card (Fin n) = n

## BASE-LIBRARY REF MvPolynomial.instCommRingMvPolynomial
{R : Type u} → {σ : Type u_1} → [inst : CommRing R] → CommRing (MvPolynomial σ R)

Body:
fun {R} {σ} [CommRing R] => AddMonoidAlgebra.commRing

## BASE-LIBRARY REF AddMonoidAlgebra.commRing
{R : Type u_1} → {M : Type u_4} → [inst : CommRing R] → [AddCommMonoid M] → CommRing (AddMonoidAlgebra R M)

Body:
fun {R} {M} [CommRing R] [AddCommMonoid M] => { toRing := AddMonoidAlgebra.ring, mul_comm := ⋯ }

## INFORMAL STATEMENT
Fundamental Theorem of Symmetric Polynomials

\textbf{(a)} The elementary symmetric polynomials $e_1, e_2, \ldots , e_N$ are algebraically independent (over $K$) and generate the $K$-algebra $\mathcal{S}$. 

In other words, each $f \in \mathcal{S}$ can be uniquely written as a polynomial in $e_1, e_2, \ldots , e_N$. 

In yet other words, the map 

\begin{align*}  K[y_1, y_2, \ldots , y_N] & \to \mathcal{S}, \\ g & \mapsto g[e_1, e_2, \ldots , e_N] \end{align*}

 is a $K$-algebra isomorphism. \medskip 

\textbf{(b)} The complete homogeneous symmetric polynomials $h_1, h_2, \ldots , h_N$ are algebraically independent (over $K$) and generate the $K$-algebra $\mathcal{S}$. 

In other words, each $f \in \mathcal{S}$ can be uniquely written as a polynomial in $h_1, h_2, \ldots , h_N$. 

In yet other words, the map 

\begin{align*}  K[y_1, y_2, \ldots , y_N] & \to \mathcal{S}, \\ g & \mapsto g[h_1, h_2, \ldots , h_N] \end{align*}

 is a $K$-algebra isomorphism. \medskip 

\textbf{(c)} Now assume that $K$ is a commutative $\mathbb {Q}$-algebra (e.g., a field of characteristic $0$). Then, the power sums $p_1, p_2, \ldots , p_N$ are algebraically independent (over $K$) and generate the $K$-algebra $\mathcal{S}$. 

In other words, each $f \in \mathcal{S}$ can be uniquely written as a polynomial in $p_1, p_2, \ldots , p_N$. 

In yet other words, the map 

\begin{align*}  K[y_1, y_2, \ldots , y_N] & \to \mathcal{S}, \\ g & \mapsto g[p_1, p_2, \ldots , p_N] \end{align*}

 is a $K$-algebra isomorphism.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-conv.fps.exp.k-q-alg
conv.fps.exp.K-Q-alg

Throughout this section (unless otherwise stated), we assume that $K$ is not just a commutative ring, but actually a commutative $\mathbb {Q}$-algebra.

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.ehp
def.sf.ehp

\textbf{(a)} For each $n \in \mathbb {Z}$, define a symmetric polynomial $e_n \in \mathcal{S}$ by 

\[  e_n = \sum _{\substack {(i_1, i_2, \ldots , i_n) \in [N]^n; \\ i_1 < i_2 < \cdots < i_n}} x_{i_1} x_{i_2} \cdots x_{i_n} = (\text{sum of all squarefree monomials of degree } n).  \]

 This $e_n$ is called the $n$-th \emph{elementary symmetric polynomial} in $x_1, x_2, \ldots , x_N$. \medskip 

\textbf{(b)} For each $n \in \mathbb {Z}$, define a symmetric polynomial $h_n \in \mathcal{S}$ by 

\[  h_n = \sum _{\substack {(i_1, i_2, \ldots , i_n) \in [N]^n; \\ i_1 \leq i_2 \leq \cdots \leq i_n}} x_{i_1} x_{i_2} \cdots x_{i_n} = (\text{sum of all monomials of degree } n).  \]

 This $h_n$ is called the $n$-th \emph{complete homogeneous symmetric polynomial} in $x_1, x_2, \ldots , x_N$. \medskip 

\textbf{(c)} For each $n \in \mathbb {Z}$, define a symmetric polynomial $p_n \in \mathcal{S}$ by 

\begin{align*}  p_n & = \begin{cases}  x_1^n + x_2^n + \cdots + x_N^n, &  \text{if } n > 0; \\ 1, &  \text{if } n = 0; \\ 0, &  \text{if } n < 0 \end{cases}\\ & = (\text{sum of all primal monomials of degree } n). \end{align*}

 This $p_n$ is called the $n$-th \emph{power sum} in $x_1, x_2, \ldots , x_N$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.monomial
def.sf.monomial

\textbf{(a)} A \emph{monomial} is an expression of the form $x_1^{a_1} x_2^{a_2} \cdots x_N^{a_N}$ with $a_1, a_2, \ldots , a_N \in \mathbb {N}$. \medskip 

\textbf{(b)} The \emph{degree} $\deg \mathfrak {m}$ of a monomial $\mathfrak {m} = x_1^{a_1} x_2^{a_2} \cdots x_N^{a_N}$ is defined to be $a_1 + a_2 + \cdots + a_N \in \mathbb {N}$. \medskip 

\textbf{(c)} A monomial $\mathfrak {m} = x_1^{a_1} x_2^{a_2} \cdots x_N^{a_N}$ is said to be \emph{squarefree} if $a_1, a_2, \ldots , a_N \in \{ 0,1\} $. (This is saying that no square or higher power of an indeterminate appears in $\mathfrak {m}$; thus the name “squarefree”.) \medskip 

\textbf{(d)} A monomial $\mathfrak {m} = x_1^{a_1} x_2^{a_2} \cdots x_N^{a_N}$ is said to be \emph{primal} if there is at most one $i \in [N]$ satisfying $a_i > 0$. (This is saying that the monomial $\mathfrak {m}$ contains no two distinct indeterminates. Thus, a primal monomial is just $1$ or a power of an indeterminate.)

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.ring-of-symm
def.sf.ring-of-symm

The $K$-subalgebra $\mathcal{S}$ of $\mathcal{P}$ is called the \emph{ring of symmetric polynomials in} $N$ \emph{variables over} $K$.

## VERDICT
{
  "verdict": "significant_divergence",
  "discrepancies": [
    {
      "root": "[IsDomain K] on hsymm_algebraicIndependent and hsymm_generates_symmetric",
      "severity": "significant",
      "bridge": "To recover part (b), one must prove algebraic independence and unique generation by h\u2081,\u2026,h_N for arbitrary commutative rings with zero divisors, which the formal theorems exclude. This requires establishing bijectivity of the evaluation map over general commutative rings, for example through universal Newton\u2013Girard identities and the elementary-symmetric equivalence; it is a substantive extension, not a routine instance discharge."
    },
    {
      "root": "[IsDomain K] on psum_algebraicIndependent and psum_generates_symmetric",
      "severity": "significant",
      "bridge": "To recover part (c), one must remove the domain hypothesis and prove that evaluation at p\u2081,\u2026,p_N is bijective for every commutative \u211a-algebra, including those with zero divisors. The supplied formal results do not cover these rings; extending them requires a substantive argument using Newton identities and invertibility of positive integers in a \u211a-algebra."
    }
  ],
  "justification": "Part (a) is faithfully covered: `esymm_algebraicIndependent` assumes only `[CommRing K]`, `esymm_generates_symmetric` gives `\u2203! g`, and `esymmAlgEquiv'` directly supplies the stated K-algebra isomorphism. Part (b), however, is stated in the blueprint under \u201cFix a commutative ring K,\u201d while both h-targets require `[IsDomain K]`. Part (c) says only \u201cassume that K is a commutative \u211a-algebra,\u201d whereas both power-sum targets require `[Algebra \u211a K] [IsDomain K]`. Thus the formal package omits the claimed h- and p-results for commutative rings or \u211a-algebras with zero divisors."
}