## TARGET AlgebraicCombinatorics.partialDeriv (def) — ELABORATED SIGNATURE
{R : Type u_1} →
  [inst : CommSemiring R] → {σ : Type u_2} → [DecidableEq σ] → σ → MvPowerSeries σ R →ₗ[R] MvPowerSeries σ R

Body:
fun {R} [CommSemiring R] {σ} [DecidableEq σ] i =>
  {
    toFun := fun f m =>
      have m' := m + fun₀ | i => 1;
      ↑(m' i) * (MvPowerSeries.coeff m') f,
    map_add' := ⋯, map_smul' := ⋯ }

Docstring: The partial derivative of a multivariate power series with respect to variable `i`.
For `f = ∑_m a_m x^m`, we have `∂f/∂x_i = ∑_m m_i · a_m · x^{m - e_i}`
where `e_i` is the `i`-th standard basis vector. 

## BASE-LIBRARY REF CommSemiring
Type u → Type u

Docstring: A commutative semiring is a semiring with commutative multiplication. 

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

## BASE-LIBRARY REF MvPowerSeries
Type u_1 → Type u_2 → Type (max (max u_2 0) u_1)

Body:
fun σ R => (σ →₀ ℕ) → R

Docstring: Multivariate formal power series, where `σ` is the index set of the variables
and `R` is the coefficient ring. 

## BASE-LIBRARY REF MvPowerSeries.instAddCommMonoid
{σ : Type u_1} → {R : Type u_2} → [AddCommMonoid R] → AddCommMonoid (MvPowerSeries σ R)

Body:
fun {σ} {R} [AddCommMonoid R] => Pi.addCommMonoid

## BASE-LIBRARY REF AddCommMonoid
Type u → Type u

Docstring: An additive commutative monoid is an additive monoid with commutative `(+)`. 

## BASE-LIBRARY REF Pi.addCommMonoid
{I : Type u} → {f : I → Type v₁} → [(i : I) → AddCommMonoid (f i)] → AddCommMonoid ((i : I) → f i)

Body:
fun {I} {f} [(i : I) → AddCommMonoid (f i)] =>
  let __src := Pi.addMonoid;
  have __src_1 := Pi.addCommSemigroup;
  { toAddMonoid := __src, add_comm := ⋯ }

## BASE-LIBRARY REF Finsupp
Type u_9 → (M : Type u_10) → [Zero M] → Type (max u_10 u_9)

Docstring: `Finsupp α M`, denoted `α →₀ M`, is the type of functions `f : α → M` such that
`f x = 0` for all but finitely many `x`. 

## BASE-LIBRARY REF Nat.instMulZeroClass
MulZeroClass ℕ

Body:
{ toMul := instMulNat, toZero := Nat.instAddMonoid.toAddZeroClass.toZero, zero_mul := Nat.zero_mul,
  mul_zero := Nat.mul_zero }

## BASE-LIBRARY REF NonUnitalNonAssocSemiring
Type u → Type u

Docstring: A not-necessarily-unital, not-necessarily-associative semiring. See `CommutatorRing` and the
documentation thereof in case you need a `NonUnitalNonAssocSemiring` instance on a Lie ring
or a Lie algebra. 

## BASE-LIBRARY REF NonAssocSemiring
Type u → Type u

Docstring: A unital but not-necessarily-associative semiring. 

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

## BASE-LIBRARY REF AddCommMagma
Type u → Type u

Docstring: A commutative additive magma is a type with an addition which commutes. 

## BASE-LIBRARY REF AddCommSemigroup
Type u → Type u

Docstring: A commutative additive semigroup is a type with an associative commutative `(+)`. 

## BASE-LIBRARY REF AddCommSemigroup.add_comm
∀ {G : Type u} [self : AddCommSemigroup G] (a b : G), a + b = b + a

Docstring: Addition is commutative in a commutative additive magma. 

## BASE-LIBRARY REF AddCommMonoid.add_comm
∀ {M : Type u} [self : AddCommMonoid M] (a b : M), a + b = b + a

Docstring: Addition is commutative in a commutative additive magma. 

## BASE-LIBRARY REF Add
Type u → Type u

Docstring: The homogeneous version of `HAdd`: `a + b : α` where `a b : α`. 

## BASE-LIBRARY REF Add.add
{α : Type u} → [self : Add α] → α → α → α

Body:
fun α [self : Add α] => self.1

Docstring: `a + b` computes the sum of `a` and `b`. See `HAdd`. 

## BASE-LIBRARY REF Finsupp.instAdd
{ι : Type u_1} → {M : Type u_3} → [inst : AddZeroClass M] → Add (ι →₀ M)

Body:
fun {ι} {M} [AddZeroClass M] => { add := Finsupp.zipWith (fun x1 x2 => x1 + x2) ⋯ }

## BASE-LIBRARY REF AddZeroClass
Type u → Type u

Docstring: Typeclass for expressing that a type `M` with addition and a zero satisfies
`0 + a = a` and `a + 0 = a` for all `a : M`. 

## BASE-LIBRARY REF Finsupp.zipWith
{α : Type u_1} →
  {M : Type u_4} →
    {N : Type u_5} →
      {O : Type u_6} →
        [inst : Zero M] →
          [inst_1 : Zero N] → [inst_2 : Zero O] → (f : M → N → O) → f 0 0 = 0 → (α →₀ M) → (α →₀ N) → α →₀ O

Body:
fun {α} {M} {N} {O} [Zero M] [Zero N] [Zero O] f hf g₁ g₂ =>
  Finsupp.onFinset (g₁.support ∪ g₂.support) (fun a => f (g₁ a) (g₂ a)) ⋯

Docstring: Given finitely supported functions `g₁ : α →₀ M` and `g₂ : α →₀ N` and function `f : M → N → O`,
`Finsupp.zipWith f hf g₁ g₂` is the finitely supported function `α →₀ O` satisfying
`zipWith f hf g₁ g₂ a = f (g₁ a) (g₂ a)`, which is well-defined when `f 0 0 = 0`. 

## BASE-LIBRARY REF Finsupp.instAdd._proof_1
∀ {M : Type u_1} [inst : AddZeroClass M], 0 + 0 = 0

## BASE-LIBRARY REF AddMonoid
Type u → Type u

Docstring: An `AddMonoid` is an `AddSemigroup` with an element `0` such that `0 + a = a + 0 = a`. 

## BASE-LIBRARY REF AddMonoid.zero_add
∀ {M : Type u} [self : AddMonoid M] (a : M), 0 + a = a

Docstring: Zero is a left neutral element for addition 

## BASE-LIBRARY REF AddMonoid.add_zero
∀ {M : Type u} [self : AddMonoid M] (a : M), a + 0 = a

Docstring: Zero is a right neutral element for addition 

## BASE-LIBRARY REF Nat.instAddMonoid
AddMonoid ℕ

Body:
inferInstance

## BASE-LIBRARY REF Nat.instAddCommMonoid
AddCommMonoid ℕ

Body:
inferInstance

## BASE-LIBRARY REF Finsupp.single
{α : Type u_1} → {M : Type u_5} → [inst : Zero M] → α → M → α →₀ M

Body:
fun {α} {M} [Zero M] a b => { support := if b = 0 then ∅ else {a}, toFun := Pi.single a b, mem_support_toFun := ⋯ }

Docstring: `single a b` is the finitely supported function with value `b` at `a` and zero otherwise. 

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

## BASE-LIBRARY REF Finsupp.instFunLike
{α : Type u_1} → {M : Type u_4} → [inst : Zero M] → FunLike (α →₀ M) α M

Body:
fun {α} {M} [Zero M] => { coe := Finsupp.toFun, coe_injective' := ⋯ }

## BASE-LIBRARY REF Zero
Type u → Type u

Docstring: A type with a zero element. 

## BASE-LIBRARY REF Finsupp.instFunLike._proof_1
∀ {α : Type u_1} {M : Type u_2} [inst : Zero M], Function.Injective Finsupp.toFun

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

## INFORMAL STATEMENT
def.fps.mulvar.partialDeriv

\leanhelper  Let $\sigma $ be a type of variable indices and let $i \in \sigma $. The \emph{partial derivative} of a multivariate power series $f = \sum _{\mathbf{m}} a_{\mathbf{m}}\,  \mathbf{x}^{\mathbf{m}}$ with respect to $x_i$ is the power series 

\[  \frac{\partial f}{\partial x_i} = \sum _{\mathbf{m}} (m_i + 1) \cdot a_{\mathbf{m} + \mathbf{e}_i} \cdot \mathbf{x}^{\mathbf{m}},  \]

 where $\mathbf{e}_i$ is the $i$-th standard basis vector (i.e., $\mathbf{e}_i = (\delta _{j,i})_{j \in \sigma }$). 

This defines an $R$-linear map $\partial /\partial x_i \colon R[[\mathbf{x}]] \to R[[\mathbf{x}]]$.

## VERDICT
{
  "verdict": "faithful",
  "discrepancies": [],
  "justification": "Unfolding the body, the coefficient of the output at `m` is `\u2191((m + fun\u2080 | i => 1) i) * (MvPowerSeries.coeff (m + fun\u2080 | i => 1)) f`. Here `fun\u2080 | i => 1` is the standard basis exponent `e_i`, and evaluation at `i` gives `(m + e_i) i = m i + 1`. Thus this is exactly the informal coefficient `(m_i + 1) \u00b7 a_{m + e_i}`. The result is bundled as `MvPowerSeries \u03c3 R \u2192\u2097[R] MvPowerSeries \u03c3 R`, matching \u201cThis defines an `R`-linear map.\u201d The `[DecidableEq \u03c3]` binder is implementation data needed for the finitely supported standard basis vector, and `[CommSemiring R]` supplies the coefficient and linear structures used by the statement."
}