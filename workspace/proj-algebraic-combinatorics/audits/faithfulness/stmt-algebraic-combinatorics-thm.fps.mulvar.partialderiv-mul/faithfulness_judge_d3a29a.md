## TARGET AlgebraicCombinatorics.partialDeriv_mul (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_1} [inst : CommSemiring R] {σ : Type u_2} [inst_1 : DecidableEq σ] (i : σ) (f g : MvPowerSeries σ R),
  (AlgebraicCombinatorics.partialDeriv i) (f * g) =
    (AlgebraicCombinatorics.partialDeriv i) f * g + f * (AlgebraicCombinatorics.partialDeriv i) g

Docstring: The partial derivative satisfies the product rule. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.partialDeriv (def)
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

## BASE-LIBRARY REF DecidableEq
Sort u → Sort (max 1 u)

Docstring: Propositional equality is `Decidable` for all elements of a type.

In other words, an instance of `DecidableEq α` is a means of deciding the proposition `a = b` is
for all `a b : α`.


## BASE-LIBRARY REF MvPowerSeries
Type u_1 → Type u_2 → Type (max (max u_2 0) u_1)

Docstring: Multivariate formal power series, where `σ` is the index set of the variables
and `R` is the coefficient ring. 

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

## BASE-LIBRARY REF CommSemiring.toSemiring
{R : Type u} → [self : CommSemiring R] → Semiring R

## BASE-LIBRARY REF RingHom.id
(α : Type u_5) → [inst : NonAssocSemiring α] → α →+* α

Docstring: The identity ring homomorphism from a semiring to itself. 

## BASE-LIBRARY REF Semiring.toNonAssocSemiring
{α : Type u} → [self : Semiring α] → NonAssocSemiring α

## BASE-LIBRARY REF MvPowerSeries.instAddCommMonoid
{σ : Type u_1} → {R : Type u_2} → [AddCommMonoid R] → AddCommMonoid (MvPowerSeries σ R)

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.toAddCommMonoid
{α : Type u} → [self : NonUnitalNonAssocSemiring α] → AddCommMonoid α

## BASE-LIBRARY REF NonAssocSemiring.toNonUnitalNonAssocSemiring
{α : Type u} → [self : NonAssocSemiring α] → NonUnitalNonAssocSemiring α

## BASE-LIBRARY REF MvPowerSeries.instModule
{σ : Type u_1} →
  {R : Type u_2} →
    {A : Type u_3} →
      [inst : Semiring R] → [inst_1 : AddCommMonoid A] → [_root_.Module R A] → _root_.Module R (MvPowerSeries σ A)

## BASE-LIBRARY REF Semiring.toModule
{R : Type u_1} → [inst : Semiring R] → _root_.Module R R

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

## BASE-LIBRARY REF MvPowerSeries.instSemiring
{σ : Type u_1} → {R : Type u_2} → [Semiring R] → Semiring (MvPowerSeries σ R)

## BASE-LIBRARY REF LinearMap.mk
{R : Type u_14} →
  {S : Type u_15} →
    [inst : Semiring R] →
      [inst_1 : Semiring S] →
        {σ : R →+* S} →
          {M : Type u_16} →
            {M₂ : Type u_17} →
              [inst_2 : AddCommMonoid M] →
                [inst_3 : AddCommMonoid M₂] →
                  [inst_4 : _root_.Module R M] →
                    [inst_5 : _root_.Module S M₂] →
                      (toAddHom : M →ₙ+ M₂) →
                        (∀ (m : R) (x : M), toAddHom.toFun (m • x) = σ m • toAddHom.toFun x) → M →ₛₗ[σ] M₂

## BASE-LIBRARY REF AddHom.mk
{M : Type u_10} →
  {N : Type u_11} →
    [inst : Add M] → [inst_1 : Add N] → (toFun : M → N) → (∀ (x y : M), toFun (x + y) = toFun x + toFun y) → M →ₙ+ N

## BASE-LIBRARY REF AddCommMagma.toAdd
{G : Type u} → [self : AddCommMagma G] → Add G

## BASE-LIBRARY REF AddCommSemigroup.toAddCommMagma
{G : Type u} → [self : AddCommSemigroup G] → AddCommMagma G

## BASE-LIBRARY REF AddCommMonoid.toAddCommSemigroup
{M : Type u} → [self : AddCommMonoid M] → AddCommSemigroup M

## BASE-LIBRARY REF Finsupp
Type u_9 → (M : Type u_10) → [Zero M] → Type (max u_10 u_9)

Docstring: `Finsupp α M`, denoted `α →₀ M`, is the type of functions `f : α → M` such that
`f x = 0` for all but finitely many `x`. 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF MulZeroClass.toZero
{M₀ : Type u} → [self : MulZeroClass M₀] → Zero M₀

## BASE-LIBRARY REF Nat.instMulZeroClass
MulZeroClass ℕ

## BASE-LIBRARY REF Finsupp.instAdd
{ι : Type u_1} → {M : Type u_3} → [inst : AddZeroClass M] → Add (ι →₀ M)

## BASE-LIBRARY REF AddMonoid.toAddZeroClass
{M : Type u} → [self : AddMonoid M] → AddZeroClass M

## BASE-LIBRARY REF Nat.instAddMonoid
AddMonoid ℕ

## BASE-LIBRARY REF Finsupp.single
{α : Type u_1} → {M : Type u_5} → [inst : Zero M] → α → M → α →₀ M

Docstring: `single a b` is the finitely supported function with value `b` at `a` and zero otherwise. 

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

## BASE-LIBRARY REF Distrib.toMul
{R : Type u_1} → [self : Distrib R] → Mul R

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

## BASE-LIBRARY REF AddCommMonoidWithOne.toAddMonoidWithOne
{R : Type u_2} → [self : AddCommMonoidWithOne R] → AddMonoidWithOne R

## BASE-LIBRARY REF NonAssocSemiring.toAddCommMonoidWithOne
{α : Type u} → [self : NonAssocSemiring α] → AddCommMonoidWithOne α

## BASE-LIBRARY REF Finsupp.instFunLike
{α : Type u_1} → {M : Type u_4} → [inst : Zero M] → FunLike (α →₀ M) α M

## BASE-LIBRARY REF MvPowerSeries.coeff
{σ : Type u_1} → {R : Type u_2} → [inst : Semiring R] → (σ →₀ ℕ) → MvPowerSeries σ R →ₗ[R] R

Docstring: The `n`th coefficient of a multivariate formal power series. 

## INFORMAL STATEMENT
Product rule for partial derivatives

\leanhelper  The partial derivative satisfies the product rule: 

\[  \frac{\partial (fg)}{\partial x_i} = \frac{\partial f}{\partial x_i} \cdot g + f \cdot \frac{\partial g}{\partial x_i}.  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.mulvar.partialderiv
def.fps.mulvar.partialDeriv

\leanhelper  Let $\sigma $ be a type of variable indices and let $i \in \sigma $. The \emph{partial derivative} of a multivariate power series $f = \sum _{\mathbf{m}} a_{\mathbf{m}}\,  \mathbf{x}^{\mathbf{m}}$ with respect to $x_i$ is the power series 

\[  \frac{\partial f}{\partial x_i} = \sum _{\mathbf{m}} (m_i + 1) \cdot a_{\mathbf{m} + \mathbf{e}_i} \cdot \mathbf{x}^{\mathbf{m}},  \]

 where $\mathbf{e}_i$ is the $i$-th standard basis vector (i.e., $\mathbf{e}_i = (\delta _{j,i})_{j \in \sigma }$). 

This defines an $R$-linear map $\partial /\partial x_i \colon R[[\mathbf{x}]] \to R[[\mathbf{x}]]$.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The target states exactly the displayed Leibniz rule: `partialDeriv i (f * g) = partialDeriv i f * g + f * partialDeriv i g`, matching `\u2202(fg)/\u2202x_i = (\u2202f/\u2202x_i)\u00b7g + f\u00b7(\u2202g/\u2202x_i)`. The dependency defines the coefficient at `m` using `m' := m + single i 1` and `\u2191(m' i) * coeff m' f`, which is the informal `(m_i + 1) \u00b7 a_{m+e_i}` formula. The binders `[CommSemiring R]` provide the coefficient algebra needed for multiplication, scalar casts, and linearity; `[DecidableEq \u03c3]` is an encoding requirement for constructing the standard basis finitely supported function and is not a substantive restriction on the mathematical index set."
}