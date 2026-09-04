## TARGET euler_odd_parts_identity (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] [inst_1 : TopologicalSpace K] [IsTopologicalRing K] [T2Space K] [NoZeroDivisors K],
  ∏' (i : ℕ+), Ring.inverse (1 - PowerSeries.X ^ (2 * ↑i - 1)) = ∏' (k : ℕ+), (1 + PowerSeries.X ^ ↑k)

Docstring: **Euler's Identity** (Proposition prop.gf.prod.euler-odd)

`∏_{i>0} (1 - x^{2i-1})⁻¹ = ∏_{k>0} (1 + x^k)`

This identity relates the generating function for partitions into odd parts
to the generating function for partitions into distinct parts.

The proof uses the fact that:
- The RHS is the generating function for partitions into distinct parts
- The LHS is the generating function for partitions into odd parts
- By Glaisher's theorem, these partition counts are equal

The algebraic proof (from the TeX source) shows:
1. `(1 + x^k)(1 - x^k) = 1 - x^{2k}`
2. `∏_{k>0}(1 + x^k) = ∏_{k>0}(1 - x^{2k}) / ∏_{k>0}(1 - x^k)`
3. The even factors cancel, leaving `1 / ∏_{k odd}(1 - x^k)` 

## BASE-LIBRARY REF CommRing
Type u → Type u

Docstring: A commutative ring is a ring with commutative multiplication. 

## BASE-LIBRARY REF TopologicalSpace
Type u → Type u

Docstring: A topology on `X`. 

## BASE-LIBRARY REF IsTopologicalRing
(R : Type u_1) → [TopologicalSpace R] → [NonUnitalNonAssocRing R] → Prop

Docstring: A topological ring is a ring `R` where addition, multiplication and negation are continuous.

If `R` is a (unital) ring, then continuity of negation can be derived from continuity of
multiplication as it is multiplication with `-1`. (See
`IsTopologicalSemiring.continuousNeg_of_mul` and
`topological_semiring.to_topological_add_group`) 

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

## BASE-LIBRARY REF T2Space
(X : Type u) → [TopologicalSpace X] → Prop

Docstring: A T₂ space, also known as a Hausdorff space, is one in which for every
`x ≠ y` there exists disjoint open sets around `x` and `y`. This is
the most widely used of the separation axioms. 

## BASE-LIBRARY REF NoZeroDivisors
(M₀ : Type u_2) → [Mul M₀] → [Zero M₀] → Prop

Docstring: Predicate typeclass for expressing that `a * b = 0` implies `a = 0` or `b = 0`
for all `a` and `b` of type `M₀`. It is weaker than `IsCancelMulZero` in general,
but equivalent to it if `M₀` is a (not necessarily unital or associative) ring. 

## BASE-LIBRARY REF Distrib
Type u_1 → Type u_1

Docstring: A typeclass stating that multiplication is left and right distributive
over addition. 

## BASE-LIBRARY REF NonUnitalNonAssocSemiring
Type u → Type u

Docstring: A not-necessarily-unital, not-necessarily-associative semiring. See `CommutatorRing` and the
documentation thereof in case you need a `NonUnitalNonAssocSemiring` instance on a Lie ring
or a Lie algebra. 

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.left_distrib
∀ {α : Type u} [self : NonUnitalNonAssocSemiring α] (a b c : α), a * (b + c) = a * b + a * c

Docstring: Multiplication is left distributive over addition 

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.right_distrib
∀ {α : Type u} [self : NonUnitalNonAssocSemiring α] (a b c : α), (a + b) * c = a * c + b * c

Docstring: Multiplication is right distributive over addition 

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

## BASE-LIBRARY REF MulZeroClass
Type u → Type u

Docstring: Typeclass for expressing that a type `M₀` with multiplication and a zero satisfies
`0 * a = 0` and `a * 0 = 0` for all `a : M₀`. 

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.zero_mul
∀ {α : Type u} [self : NonUnitalNonAssocSemiring α] (a : α), 0 * a = 0

Docstring: Zero is a left absorbing element for multiplication 

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.mul_zero
∀ {α : Type u} [self : NonUnitalNonAssocSemiring α] (a : α), a * 0 = 0

Docstring: Zero is a right absorbing element for multiplication 

## BASE-LIBRARY REF PowerSeries
Type u_1 → Type (max u_1 0)

Body:
fun R => MvPowerSeries Unit R

Docstring: Formal power series over a coefficient type `R` 

## BASE-LIBRARY REF tprod
{α : Type u_4} →
  {β : Type u_5} →
    [CommMonoid α] → [TopologicalSpace α] → (β → α) → optParam (SummationFilter β) (SummationFilter.unconditional β) → α

Body:
wrapped✝.1

Docstring: `∏' i, f i` is the unconditional product of `f`, if it exists, or 1 otherwise.

More generally, if `L` is a `SummationFilter`, `∏'[L] i, f i` is the product of `f` with respect to
`L` if it exists, and `1` otherwise.

(Note that even if the unconditional product exists, it might not be unique if the topology is not
separated. When the multiplicative support of `f` is finite, we make the most reasonable choice,
to use the product over the multiplicative support. Otherwise, we choose arbitrarily an `a`
satisfying `HasProd f a`. Similar remarks apply to more general summation filters.) 

## BASE-LIBRARY REF PNat
Type

Body:
{ n // 0 < n }

Docstring: `ℕ+` is the type of positive natural numbers. It is defined as a subtype,
and the VM representation of `ℕ+` is the same as `ℕ` because the proof
is not stored. 

## BASE-LIBRARY REF NonUnitalSemiring.mul_assoc
∀ {α : Type u} [self : NonUnitalSemiring α] (a b c : α), a * b * c = a * (b * c)

Docstring: Multiplication is associative 

## BASE-LIBRARY REF Semiring.one_mul
∀ {α : Type u} [self : Semiring α] (a : α), 1 * a = a

Docstring: One is a left neutral element for multiplication 

## BASE-LIBRARY REF Semiring.mul_one
∀ {α : Type u} [self : Semiring α] (a : α), a * 1 = a

Docstring: One is a right neutral element for multiplication 

## BASE-LIBRARY REF CommRing.mul_comm
∀ {α : Type u} [self : CommRing α] (a b : α), a * b = b * a

Docstring: Multiplication is commutative in a commutative multiplicative magma. 

## BASE-LIBRARY REF PowerSeries.instCommRing
{R : Type u_1} → [CommRing R] → CommRing (PowerSeries R)

Body:
fun {R} [CommRing R] => id inferInstance

## BASE-LIBRARY REF MvPowerSeries
Type u_1 → Type u_2 → Type (max (max u_2 0) u_1)

Body:
fun σ R => (σ →₀ ℕ) → R

Docstring: Multivariate formal power series, where `σ` is the index set of the variables
and `R` is the coefficient ring. 

## BASE-LIBRARY REF MvPowerSeries.instCommRing
{σ : Type u_1} → {R : Type u_2} → [CommRing R] → CommRing (MvPowerSeries σ R)

Body:
fun {σ} {R} [CommRing R] =>
  let __src := inferInstanceAs (CommSemiring (MvPowerSeries σ R));
  let __src_1 := inferInstanceAs (AddCommGroup (MvPowerSeries σ R));
  { toSemiring := __src.toSemiring, toNeg := __src_1.toNeg, toSub := __src_1.toSub, sub_eq_add_neg := ⋯,
    zsmul := SubNegMonoid.zsmul, zsmul_zero' := ⋯, zsmul_succ' := ⋯, zsmul_neg' := ⋯, neg_add_cancel := ⋯,
    toIntCast := MvPowerSeries.instRing.toAddGroupWithOne.toIntCast, intCast_ofNat := ⋯, intCast_negSucc := ⋯,
    mul_comm := ⋯ }

## BASE-LIBRARY REF PowerSeries.WithPiTopology.instTopologicalSpace
(R : Type u_1) → [TopologicalSpace R] → TopologicalSpace (PowerSeries R)

Body:
fun R [TopologicalSpace R] => Pi.topologicalSpace

Docstring: The pointwise topology on `PowerSeries` 

## BASE-LIBRARY REF Ring.inverse
{M₀ : Type u_2} → [MonoidWithZero M₀] → M₀ → M₀

Body:
fun {M₀} [MonoidWithZero M₀] x => if h : IsUnit x then ↑h.unit⁻¹ else 0

Docstring: Introduce a function `inverse` on a monoid with zero `M₀`, which sends `x` to `x⁻¹` if `x` is
invertible and to `0` otherwise.  This definition is somewhat ad hoc, but one needs a fully (rather
than partially) defined inverse function for some purposes, including for calculus.

Note that while this is in the `Ring` namespace for brevity, it requires the weaker assumption
`MonoidWithZero M₀` instead of `Ring M₀`. 

## BASE-LIBRARY REF Semiring
Type u → Type u

Docstring: A `Semiring` is a type with addition, multiplication, a `0` and a `1` where addition is
commutative and associative, multiplication is associative and left and right distributive over
addition, and `0` and `1` are additive and multiplicative identities. 

## BASE-LIBRARY REF PowerSeries.instSemiring
{R : Type u_1} → [Semiring R] → Semiring (PowerSeries R)

Body:
fun {R} [Semiring R] => id inferInstance

## BASE-LIBRARY REF MvPowerSeries.instSemiring
{σ : Type u_1} → {R : Type u_2} → [Semiring R] → Semiring (MvPowerSeries σ R)

Body:
fun {σ} {R} [Semiring R] =>
  let __src := inferInstanceAs (AddMonoidWithOne (MvPowerSeries σ R));
  let __src_1 := inferInstanceAs (Mul (MvPowerSeries σ R));
  have __src_2 := inferInstanceAs (AddCommMonoid (MvPowerSeries σ R));
  { toAddMonoid := __src.toAddMonoid, add_comm := ⋯, toMul := __src_1, left_distrib := ⋯, right_distrib := ⋯,
    zero_mul := ⋯, mul_zero := ⋯, mul_assoc := ⋯, toOne := __src.toOne, one_mul := ⋯, mul_one := ⋯,
    toNatCast := __src.toNatCast, natCast_zero := ⋯, natCast_succ := ⋯, npow := npowRecAuto, npow_zero := ⋯,
    npow_succ := ⋯ }

## BASE-LIBRARY REF CommSemiring
Type u → Type u

Docstring: A commutative semiring is a semiring with commutative multiplication. 

## BASE-LIBRARY REF Sub
Type u → Type u

Docstring: The homogeneous version of `HSub`: `a - b : α` where `a b : α`. 

## BASE-LIBRARY REF Sub.sub
{α : Type u} → [self : Sub α] → α → α → α

Body:
fun α [self : Sub α] => self.1

Docstring: `a - b` computes the difference of `a` and `b`. See `HSub`. 

## BASE-LIBRARY REF SubNegMonoid
Type u → Type u

Docstring: A `SubNegMonoid` is an `AddMonoid` with unary `-` and binary `-` operations
satisfying `sub_eq_add_neg : ∀ a b, a - b = a + -b`.

The default for `sub` is such that `a - b = a + -b` holds by definition.

Adding `sub` as a field rather than defining `a - b := a + -b` allows us to
avoid certain classes of unification failures, for example:
Let `foo X` be a type with a `∀ X, Sub (Foo X)` instance but no
`∀ X, Neg (Foo X)`. Suppose we also have an instance
`∀ X [Cromulent X], AddGroup (Foo X)`. Then the `(-)` coming from
`AddGroup.sub` cannot be definitionally equal to the `(-)` coming from
`Foo.Sub`.

In the same way, adding a `zsmul` field makes it possible to avoid definitional failures
in diamonds. See the definition of `AddMonoid` and Note [forgetful inheritance] for more
explanations on this.


## BASE-LIBRARY REF PowerSeries.instAddGroup
{R : Type u_1} → [AddGroup R] → AddGroup (PowerSeries R)

Body:
fun {R} [AddGroup R] => id inferInstance

## BASE-LIBRARY REF AddGroup
Type u → Type u

Docstring: An `AddGroup` is an `AddMonoid` with a unary `-` satisfying `-a + a = 0`.

There is also a binary operation `-` such that `a - b = a + -b`,
with a default so that `a - b = a + -b` holds by definition.

Use `AddGroup.ofLeftAxioms` or `AddGroup.ofRightAxioms` to define an
additive group structure on a type with the minimum proof obligations.


## BASE-LIBRARY REF MvPowerSeries.instAddGroup
{σ : Type u_1} → {R : Type u_2} → [AddGroup R] → AddGroup (MvPowerSeries σ R)

Body:
fun {σ} {R} [AddGroup R] => Pi.addGroup

## BASE-LIBRARY REF AddGroupWithOne
Type u → Type u

Docstring: An `AddGroupWithOne` is an `AddGroup` with a 1. It also contains data for the unique
homomorphisms `ℕ → R` and `ℤ → R`. 

## BASE-LIBRARY REF AddGroupWithOne.neg_add_cancel
∀ {R : Type u} [self : AddGroupWithOne R] (a : R), -a + a = 0

## BASE-LIBRARY REF Ring
Type u → Type u

Docstring: A `Ring` is a `Semiring` with negation making it an additive group. 

## BASE-LIBRARY REF One
Type u → Type u

Docstring: A type with a "one" element. 

## BASE-LIBRARY REF One.one
{α : Type u} → [self : One α] → α

Body:
fun α [self : One α] => self.1

Docstring: The "one" element of the type. 

## BASE-LIBRARY REF MvPowerSeries.instOne
{σ : Type u_1} → {R : Type u_2} → [Semiring R] → One (MvPowerSeries σ R)

Body:
fun {σ} {R} [Semiring R] => { one := (MvPowerSeries.monomial 0) 1 }

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

## BASE-LIBRARY REF MvPowerSeries.instModule
{σ : Type u_1} →
  {R : Type u_2} →
    {A : Type u_3} →
      [inst : Semiring R] → [inst_1 : AddCommMonoid A] → [_root_.Module R A] → _root_.Module R (MvPowerSeries σ A)

Body:
fun {σ} {R} {A} [Semiring R] [AddCommMonoid A] [_root_.Module R A] => Pi.module (σ →₀ ℕ) (fun a => A) R

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

## BASE-LIBRARY REF MvPowerSeries.monomial
{σ : Type u_1} → {R : Type u_2} → [inst : Semiring R] → (σ →₀ ℕ) → R →ₗ[R] MvPowerSeries σ R

Body:
fun {σ} {R} [Semiring R] n => LinearMap.single R (fun x => R) n

Docstring: The `n`th monomial as multivariate formal power series:
it is defined as the `R`-linear map from `R` to the semiring
of multivariate formal power series associating to each `a`
the map sending `n : σ →₀ ℕ` to the value `a`
and sending all other `x : σ →₀ ℕ` different from `n` to `0`. 

## BASE-LIBRARY REF Finsupp
Type u_9 → (M : Type u_10) → [Zero M] → Type (max u_10 u_9)

Docstring: `Finsupp α M`, denoted `α →₀ M`, is the type of functions `f : α → M` such that
`f x = 0` for all but finitely many `x`. 

## BASE-LIBRARY REF Pow
Type u → Type v → Type (max u v)

Docstring: The homogeneous version of `HPow`: `a ^ b : α` where `a : α`, `b : β`.
(The right argument is not the same as the left since we often want this even
in the homogeneous case.)

Types can choose to subscribe to particular defaulting behavior by providing
an instance to either `NatPow` or `HomogeneousPow`:
- `NatPow` is for types whose exponents is preferentially a `Nat`.
- `HomogeneousPow` is for types whose base and exponent are preferentially the same.


## BASE-LIBRARY REF Pow.pow
{α : Type u} → {β : Type v} → [self : Pow α β] → α → β → α

Body:
fun α β [self : Pow α β] => self.1

Docstring: `a ^ b` computes `a` to the power of `b`. See `HPow`. 

## BASE-LIBRARY REF Monoid
Type u → Type u

Docstring: A `Monoid` is a `Semigroup` with an element `1` such that `1 * a = a * 1 = a`. 

## BASE-LIBRARY REF MonoidWithZero
Type u → Type u

Docstring: A type `M₀` is a “monoid with zero” if it is a monoid with zero element, and `0` is left
and right absorbing. 

## BASE-LIBRARY REF PowerSeries.X
{R : Type u_1} → [Semiring R] → PowerSeries R

Body:
fun {R} [Semiring R] => MvPowerSeries.X ()

Docstring: The variable of the formal power series ring. 

## BASE-LIBRARY REF instSubNat
Sub ℕ

Body:
{ sub := Nat.sub }

Characterization: Natural subtraction truncates: `a - b = 0` whenever `b ≥ a`.

## BASE-LIBRARY REF Nat.sub
ℕ → ℕ → ℕ

Body:
fun x x_1 =>
  Nat.brecOn (motive := fun x => ℕ → ℕ) x_1
    (fun x f x_2 =>
      (match (motive := ℕ → (x : ℕ) → Nat.below (motive := fun x => ℕ → ℕ) x → ℕ) x_2, x with
        | a, 0 => fun x => a
        | a, b.succ => fun x => (x.1 a).pred)
        f)
    x

Docstring: Subtraction of natural numbers, truncated at `0`. Usually used via the `-` operator.

If a result would be less than zero, then the result is zero.

This definition is overridden in both the kernel and the compiler to efficiently evaluate using the
arbitrary-precision arithmetic library. The definition provided here is the logical model.

Examples:
* `5 - 3 = 2`
* `8 - 2 = 6`
* `8 - 8 = 0`
* `8 - 20 = 0`


Characterization: Natural subtraction truncates: `a - b = 0` whenever `b ≥ a`.

## BASE-LIBRARY REF Mul
Type u → Type u

Docstring: The homogeneous version of `HMul`: `a * b : α` where `a b : α`. 

## BASE-LIBRARY REF Mul.mul
{α : Type u} → [self : Mul α] → α → α → α

Body:
fun α [self : Mul α] => self.1

Docstring: `a * b` computes the product of `a` and `b`. See `HMul`. 

## BASE-LIBRARY REF Nat.mul
ℕ → ℕ → ℕ

Body:
fun x x_1 =>
  Nat.brecOn (motive := fun x => ℕ → ℕ) x_1
    (fun x f x_2 =>
      (match (motive := ℕ → (x : ℕ) → Nat.below (motive := fun x => ℕ → ℕ) x → ℕ) x_2, x with
        | x, 0 => fun x => 0
        | a, b.succ => fun x => (x.1 a).add a)
        f)
    x

Docstring: Multiplication of natural numbers, usually accessed via the `*` operator.

This function is overridden in both the kernel and the compiler to efficiently evaluate using the
arbitrary-precision arithmetic library. The definition provided here is the logical model.


## BASE-LIBRARY REF PNat.val
ℕ+ → ℕ

Body:
Subtype.val

Docstring: The underlying natural number 

## BASE-LIBRARY REF SummationFilter.unconditional
(β : Type u_2) → SummationFilter β

Body:
fun β => { filter := Filter.atTop }

Docstring: **Unconditional summation**: a function on `β` is said to be *unconditionally summable* if its
partial sums over finite subsets converge with respect to the `atTop` filter. 

## BASE-LIBRARY REF Add
Type u → Type u

Docstring: The homogeneous version of `HAdd`: `a + b : α` where `a b : α`. 

## BASE-LIBRARY REF Add.add
{α : Type u} → [self : Add α] → α → α → α

Body:
fun α [self : Add α] => self.1

Docstring: `a + b` computes the sum of `a` and `b`. See `HAdd`. 

## INFORMAL STATEMENT
Euler

We have

\[  \prod _{i>0}\left( 1-x^{2i-1}\right) ^{-1}=\prod _{k>0}\left( 1+x^{k}\right) .  \]

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.commring.fracs
def.commring.fracs

Let $L$ be a commutative ring. Let $a\in L$. Assume that $a$ is invertible. Then: 

\textbf{(a)} The inverse of $a$ is called $a^{-1}$. 

\textbf{(b)} For any $b\in L$, the product $b\cdot a^{-1}$ is called $\frac{b}{a}$ (or $b/a$). 

\textbf{(c)} For any negative integer $n$, we define $a^{n}$ to be $\left( a^{-1}\right)^{-n}$. Thus, the $n$-th power $a^{n}$ is defined for each $n\in \mathbb {Z}$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.commring.inverse-2
def.commring.inverse

Let $L$ be a commutative ring. Let $a\in L$. Then: 

\textbf{(a)} An \emph{inverse} (or \emph{multiplicative inverse}) of $a$ means an element $b\in L$ such that $ab=ba=1$. 

\textbf{(b)} We say that $a$ is \emph{invertible} in $L$ (or a \emph{unit} of $L$) if $a$ has an inverse.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.coeff
def.fps.coeff

If $n\in \mathbb {N}$, and if $\mathbf{a}=\left( a_{0},a_{1},a_{2},\ldots \right) \in K\left[\left[x\right]\right]$ is an FPS, then we define an element $\left[x^{n}\right]\mathbf{a}\in K$ by 

\[  \left[x^{n}\right]\mathbf{a}:=a_{n}.  \]

 This is called the \emph{coefficient of }$x^{n}$\emph{ in }$\mathbf{a}$, or the $n$\emph{-th coefficient} of $\mathbf{a}$, or the $x^{n}$\emph{-coefficient} of $\mathbf{a}$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.determines-xn-coeff
def.fps.determines-xn-coeff

Let $\left(\mathbf{a}_{i}\right)_{i\in I}\in K\left[\left[x\right]\right]^{I}$ be a (possibly infinite) family of FPSs. Let $n\in \mathbb {N}$. Let $M$ be a finite subset of $I$. 

\textbf{(a)} We say that $M$ \emph{determines the $x^{n}$-coefficient in the sum of} $\left(\mathbf{a}_{i}\right)_{i\in I}$ if every finite subset $J$ of $I$ satisfying $M\subseteq J\subseteq I$ satisfies 

\[  \left[x^{n}\right]\left(\sum _{i\in J}\mathbf{a}_{i}\right) =\left[x^{n}\right]\left(\sum _{i\in M}\mathbf{a}_{i}\right).  \]

\textbf{(b)} We say that $M$ \emph{determines the $x^{n}$-coefficient in the product of} $\left(\mathbf{a}_{i}\right)_{i\in I}$ if every finite subset $J$ of $I$ satisfying $M\subseteq J\subseteq I$ satisfies 

\[  \left[x^{n}\right]\left(\prod _{i\in J}\mathbf{a}_{i}\right) =\left[x^{n}\right]\left(\prod _{i\in M}\mathbf{a}_{i}\right).  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.fps
def.fps.fps

A \emph{formal power series} (or, short, \emph{FPS}) in $1$ indeterminate over $K$ means a sequence $\left(a_{0},a_{1},a_{2},\ldots \right) = \left(a_{n}\right)_{n\in \mathbb {N}} \in K^{\mathbb {N}}$ of elements of $K$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.multipliable
def.fps.multipliable

Let $\left(\mathbf{a}_{i}\right)_{i\in I}$ be a (possibly infinite) family of FPSs. Then: 

\textbf{(a)} The family $\left(\mathbf{a}_{i}\right)_{i\in I}$ is said to be \emph{multipliable} if and only if each coefficient in its product is finitely determined. 

\textbf{(b)} If the family $\left(\mathbf{a}_{i}\right)_{i\in I}$ is multipliable, then its \emph{product} $\prod _{i\in I}\mathbf{a}_{i}$ is defined to be the FPS whose $x^{n}$-coefficient (for any $n\in \mathbb {N}$) can be computed as follows: If $n\in \mathbb {N}$, and if $M$ is a finite subset of $I$ that determines the $x^{n}$-coefficient in the product of $\left( \mathbf{a}_{i}\right)_{i\in I}$, then 

\[  \left[x^{n}\right]\left(\prod _{i\in I}\mathbf{a}_{i}\right) =\left[x^{n}\right]\left(\prod _{i\in M}\mathbf{a}_{i}\right).  \]

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.summable
def.fps.summable

A (possibly infinite) family $\left(\mathbf{a}_{i}\right)_{i\in I}$ of FPSs is said to be \emph{summable} (or \emph{entrywise essentially finite}) if 

\[  \text{for each }n\in \mathbb {N}\text{, all but finitely many }i\in I\text{ satisfy }\left[x^{n}\right]\mathbf{a}_{i}=0.  \]

 In this case, the sum $\sum _{i\in I}\mathbf{a}_{i}$ is defined to be the FPS with 

\[  \left[x^{n}\right]\left(\sum _{i\in I}\mathbf{a}_{i}\right) =\underbrace{\sum _{i\in I}\left[x^{n}\right]\mathbf{a}_{i}}_{\substack {\text{an essentially}\\ \text{finite sum}}} \  \  \  \  \  \  \  \  \  \  \text{for all }n\in \mathbb {N}\text{.}  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.x
def.fps.x

Let $x$ denote the FPS $\left(0,1,0,0,0,\ldots \right)$. In other words, let $x$ denote the FPS with $\left[x^{1}\right]x=1$ and $\left[x^{i}\right]x=0$ for all $i\neq 1$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.xn-coeff-fin-determined
def.fps.xn-coeff-fin-determined

Let $\left(\mathbf{a}_{i}\right)_{i\in I}\in K\left[\left[x\right]\right]^{I}$ be a (possibly infinite) family of FPSs. Let $n\in \mathbb {N}$. 

\textbf{(a)} We say that \emph{the $x^{n}$-coefficient in the sum of} $\left(\mathbf{a}_{i}\right)_{i\in I}$ \emph{is finitely determined} if there is a finite subset $M$ of $I$ that determines the $x^{n}$-coefficient in the sum of $\left(\mathbf{a}_{i}\right)_{i\in I}$. 

\textbf{(b)} We say that \emph{the $x^{n}$-coefficient in the product of} $\left(\mathbf{a}_{i}\right)_{i\in I}$ \emph{is finitely determined} if there is a finite subset $M$ of $I$ that determines the $x^{n}$-coefficient in the product of $\left(\mathbf{a}_{i}\right)_{i\in I}$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.infsum.essfin
def.infsum.essfin

\textbf{(a)} A family $\left(a_{i}\right)_{i\in I}\in K^{I}$ of elements of $K$ is said to be \emph{essentially finite} if all but finitely many $i\in I$ satisfy $a_{i}=0$ (in other words, if the set $\left\{ i\in I\  \mid \  a_{i}\neq 0\right\} $ is finite). \medskip 

\textbf{(b)} Let $\left(a_{i}\right)_{i\in I}\in K^{I}$ be an essentially finite family of elements of $K$. Then, the infinite sum $\sum _{i\in I}a_{i}$ is defined to equal the finite sum $\sum _{\substack {i\in I;\\ a_{i}\neq 0}}a_{i}$. Such an infinite sum is said to be \emph{essentially finite}.

## VERDICT
{
  "verdict": "minor_discrepancy",
  "discrepancies": [
    {
      "root": "[NoZeroDivisors K]",
      "severity": "minor",
      "bridge": "The blueprint\u2019s ambient coefficient object is an arbitrary commutative ring, whereas the formal theorem assumes no zero divisors. Recover the arbitrary-ring identity by specializing the formal theorem to \u2124 with the discrete topology and applying the coefficientwise map \u2124[[x]] \u2192 K[[x]] induced by \u2124 \u2192 K. This map preserves X, the unit inverses (1 \u2212 X^n)\u207b\u00b9, and these coefficientwise-stabilizing infinite products. Thus the equality transfers to every commutative ring without reproving Euler\u2019s identity."
    }
  ],
  "justification": "The informal definitions place the identity in K[[x]] for a \u201ccommutative ring\u201d K, with no no-zero-divisors condition. The elaborated signature instead begins `\u2200 {K : Type u_1} [inst : CommRing K] ... [NoZeroDivisors K],`. The topological and Hausdorff assumptions are encoding needed for `tprod`: with the pointwise topology, the displayed products converge coefficientwise because each coefficient of their finite partial products eventually stabilizes, matching the blueprint\u2019s finitely determined product. Likewise, `Ring.inverse` agrees with the blueprint inverse here because every `1 - X^n` has constant coefficient 1 and is a unit. Hence only the extra `[NoZeroDivisors K]` restriction requires a bridge, and the universal base-change argument makes it minor."
}