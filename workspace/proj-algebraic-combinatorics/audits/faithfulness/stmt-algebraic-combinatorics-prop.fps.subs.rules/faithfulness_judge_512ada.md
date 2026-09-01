## TARGET AlgebraicCombinatorics.fps_subs_div (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_2} [inst : Field K] (f₁ f₂ g : PowerSeries K),
  PowerSeries.constantCoeff g = 0 →
    PowerSeries.constantCoeff f₂ ≠ 0 →
      PowerSeries.subst g f₁ * (PowerSeries.subst g f₂)⁻¹ = PowerSeries.subst g (f₁ * f₂⁻¹)

Docstring: **Proposition 7.3.4(c)** (prop.fps.subs.rules)
(f₁ / f₂) ∘ g = (f₁ ∘ g) / (f₂ ∘ g) when f₂ is invertible.

Note: Division of power series requires working over a field. We state this
for the case where K is a field and f₂ has nonzero constant coefficient.

In the source, this is stated as: if f₂ is invertible (i.e., has nonzero constant term),
then f₂ ∘ g is automatically invertible and the division rule holds. 

## TARGET AlgebraicCombinatorics.fps_subs_X_left (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] (g : PowerSeries K),
  PowerSeries.constantCoeff g = 0 → PowerSeries.subst g PowerSeries.X = g

Docstring: **Proposition 7.3.4(g)** (prop.fps.subs.rules)
X ∘ g = g 

## TARGET AlgebraicCombinatorics.fps_subs_add (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] (f₁ f₂ g : PowerSeries K),
  PowerSeries.constantCoeff g = 0 → PowerSeries.subst g (f₁ + f₂) = PowerSeries.subst g f₁ + PowerSeries.subst g f₂

Docstring: **Proposition 7.3.4(a)** (prop.fps.subs.rules)
(f₁ + f₂) ∘ g = f₁ ∘ g + f₂ ∘ g 

## TARGET AlgebraicCombinatorics.fps_subs_summableFPSSum (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] {ι : Type u_2} (f : ι → PowerSeries K) (g : PowerSeries K)
  (hg : PowerSeries.constantCoeff g = 0) (hf : AlgebraicCombinatorics.FPS.SummableFPS f),
  PowerSeries.subst g (AlgebraicCombinatorics.FPS.summableFPSSum f hf) =
    AlgebraicCombinatorics.FPS.summableFPSSum (fun i => PowerSeries.subst g (f i)) ⋯

Docstring: **Proposition 7.3.4(h)** (prop.fps.subs.rules) - Infinite sum version
For a summable family (fᵢ)_{i∈I}, we have (∑ᵢ fᵢ) ∘ g = ∑ᵢ (fᵢ ∘ g).

This is the full infinite sum version of the substitution rule. The proof uses
the distributive law for multiplication over infinite sums and Fubini's theorem
for essentially finite double sums. 

## TARGET AlgebraicCombinatorics.fps_subs_sum (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] {ι : Type u_2} (s : Finset ι) (f : ι → PowerSeries K) (g : PowerSeries K),
  PowerSeries.constantCoeff g = 0 → PowerSeries.subst g (∑ i ∈ s, f i) = ∑ i ∈ s, PowerSeries.subst g (f i)

Docstring: **Proposition 7.3.4(h)** (prop.fps.subs.rules) - Finite sum version
For a finite sum (∑ᵢ∈s fᵢ), we have (∑ᵢ∈s fᵢ) ∘ g = ∑ᵢ∈s (fᵢ ∘ g). 

## TARGET AlgebraicCombinatorics.fps_subs_assoc_constCoeff (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] (g h : PowerSeries K),
  PowerSeries.constantCoeff g = 0 →
    PowerSeries.constantCoeff h = 0 → PowerSeries.constantCoeff (PowerSeries.subst h g) = 0

Docstring: **Proposition 7.3.4(e)** (prop.fps.subs.rules)
(f ∘ g) ∘ h = f ∘ (g ∘ h), and [x⁰](g ∘ h) = 0.

Part 1: The constant coefficient of g ∘ h is 0. 

## TARGET AlgebraicCombinatorics.fps_subs_assoc (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] (f g h : PowerSeries K),
  PowerSeries.constantCoeff g = 0 →
    PowerSeries.constantCoeff h = 0 →
      PowerSeries.subst h (PowerSeries.subst g f) = PowerSeries.subst (PowerSeries.subst h g) f

Docstring: **Proposition 7.3.4(e)** (prop.fps.subs.rules)
(f ∘ g) ∘ h = f ∘ (g ∘ h)

Part 2: Associativity of composition. 

## TARGET AlgebraicCombinatorics.fps_subs_X_right (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] (g : PowerSeries K), PowerSeries.subst PowerSeries.X g = g

Docstring: **Proposition 7.3.4(g)** (prop.fps.subs.rules)
g ∘ X = g 

## TARGET AlgebraicCombinatorics.fps_subs_summable (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] {ι : Type u_2} (f : ι → PowerSeries K) (g : PowerSeries K),
  PowerSeries.constantCoeff g = 0 →
    AlgebraicCombinatorics.FPS.SummableFPS f → AlgebraicCombinatorics.FPS.SummableFPS fun i => PowerSeries.subst g (f i)

Docstring: **Proposition 7.3.4(h)** (prop.fps.subs.rules) - Summability preservation
If (fᵢ)_{i∈I} is a summable family and g has constant term 0,
then (fᵢ ∘ g)_{i∈I} is also summable.

The key insight is that [x^n](fᵢ ∘ g) only depends on [x^0]fᵢ, ..., [x^n]fᵢ.
If all these are 0, then [x^n](fᵢ ∘ g) = 0. So the set of i with
[x^n](fᵢ ∘ g) ≠ 0 is contained in the finite union ⋃_{k≤n} {i | [x^k]fᵢ ≠ 0}. 

## TARGET AlgebraicCombinatorics.fps_subs_const (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] (a : K) (g : PowerSeries K),
  PowerSeries.constantCoeff g = 0 → PowerSeries.subst g (PowerSeries.C a) = PowerSeries.C a

Docstring: **Proposition 7.3.4(f)** (prop.fps.subs.rules)
a ∘ g = a for any constant a ∈ K. 

## TARGET AlgebraicCombinatorics.fps_subs_mul (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] (f₁ f₂ g : PowerSeries K),
  PowerSeries.constantCoeff g = 0 → PowerSeries.subst g (f₁ * f₂) = PowerSeries.subst g f₁ * PowerSeries.subst g f₂

Docstring: **Proposition 7.3.4(b)** (prop.fps.subs.rules)
(f₁ · f₂) ∘ g = (f₁ ∘ g) · (f₂ ∘ g) 

## TARGET AlgebraicCombinatorics.fps_subs_pow (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] (f g : PowerSeries K),
  PowerSeries.constantCoeff g = 0 → ∀ (k : ℕ), PowerSeries.subst g (f ^ k) = PowerSeries.subst g f ^ k

Docstring: **Proposition 7.3.4(d)** (prop.fps.subs.rules)
f^k ∘ g = (f ∘ g)^k 

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

## BASE-LIBRARY REF Field
Type u → Type u

Docstring: A `Field` is a `CommRing` with multiplicative inverses for nonzero elements.

An instance of `Field K` includes maps `ratCast : ℚ → K` and `qsmul : ℚ → K → K`.
Those two fields are needed to implement the `DivisionRing K → Algebra ℚ K` instance since we need
to control the specific definitions for some special cases of `K` (in particular `K = ℚ` itself).
See also note [forgetful inheritance].

If the field has positive characteristic `p`, our division by zero convention forces
`ratCast (1 / p) = 1 / 0 = 0`. 

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

## BASE-LIBRARY REF RingHom
(α : Type u_5) → (β : Type u_6) → [NonAssocSemiring α] → [NonAssocSemiring β] → Type (max u_5 u_6)

Docstring: Bundled semiring homomorphisms; use this for bundled ring homomorphisms too.

This extends from both `MonoidHom` and `MonoidWithZeroHom` in order to put the fields in a
sensible order, even though `MonoidWithZeroHom` already extends `MonoidHom`. 

## BASE-LIBRARY REF Semiring.toNonAssocSemiring
{α : Type u} → [self : Semiring α] → NonAssocSemiring α

## BASE-LIBRARY REF PowerSeries.instSemiring
{R : Type u_1} → [Semiring R] → Semiring (PowerSeries R)

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

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

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

## BASE-LIBRARY REF EuclideanDomain.toCommRing
{R : Type u} → [self : EuclideanDomain R] → CommRing R

## BASE-LIBRARY REF Field.toEuclideanDomain
{K : Type u_1} → [Field K] → EuclideanDomain K

## BASE-LIBRARY REF Ne
{α : Sort u} → α → α → Prop

Docstring: `a ≠ b`, or `Ne a b` is defined as `¬ (a = b)` or `a = b → False`,
and asserts that `a` and `b` are not equal.


Conventions for notations in identifiers:

 * The recommended spelling of `≠` in identifiers is `ne`.

## BASE-LIBRARY REF MvPowerSeries
Type u_1 → Type u_2 → Type (max (max u_2 0) u_1)

Docstring: Multivariate formal power series, where `σ` is the index set of the variables
and `R` is the coefficient ring. 

## BASE-LIBRARY REF Unit
Type

Docstring: The canonical type with one element. This element is written `()`.

`Unit` has a number of uses:
* It can be used to model control flow that returns from a function call without providing other
  information.
* Monadic actions that return `Unit` have side effects without computing values.
* In polymorphic types, it can be used to indicate that no data is to be stored in a particular
  field.


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

## BASE-LIBRARY REF PowerSeries.subst
{R : Type u_2} →
  [inst : CommRing R] →
    {τ : Type u_3} →
      {S : Type u_4} → [inst_1 : CommRing S] → [Algebra R S] → MvPowerSeries τ S → PowerSeries R → MvPowerSeries τ S

Docstring: Substitution of power series into a power series. 

## BASE-LIBRARY REF Algebra.id
(R : Type u) → [inst : CommSemiring R] → Algebra R R

Docstring: The identity map inducing an `Algebra` structure. 

## BASE-LIBRARY REF CommRing.toCommSemiring
{α : Type u} → [s : CommRing α] → CommSemiring α

## BASE-LIBRARY REF Inv.inv
{α : Type u} → [self : Inv α] → α → α

Docstring: `a⁻¹` computes the inverse of `a`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `⁻¹` in identifiers is `inv`.

## BASE-LIBRARY REF PowerSeries.instInv
{k : Type u_2} → [Field k] → Inv (PowerSeries k)

## BASE-LIBRARY REF CommRing
Type u → Type u

Docstring: A commutative ring is a ring with commutative multiplication. 

## BASE-LIBRARY REF CommSemiring.toSemiring
{R : Type u} → [self : CommSemiring R] → Semiring R

## BASE-LIBRARY REF PowerSeries.X
{R : Type u_1} → [Semiring R] → PowerSeries R

Docstring: The variable of the formal power series ring. 

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

## BASE-LIBRARY REF PowerSeries.instCommRing
{R : Type u_1} → [CommRing R] → CommRing (PowerSeries R)

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

## BASE-LIBRARY REF PowerSeries.instAddCommMonoid
{R : Type u_1} → [AddCommMonoid R] → AddCommMonoid (PowerSeries R)

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.toAddCommMonoid
{α : Type u} → [self : NonUnitalNonAssocSemiring α] → AddCommMonoid α

## BASE-LIBRARY REF PowerSeries.C
{R : Type u_1} → [inst : Semiring R] → R →+* PowerSeries R

Docstring: The constant formal power series. 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


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

## BASE-LIBRARY REF Set.Finite
{α : Type u} → Set α → Prop

Docstring: A set is finite if the corresponding `Subtype` is finite,
i.e., if there exists a natural `n : ℕ` and an equivalence `s ≃ Fin n`. 

## BASE-LIBRARY REF setOf
{α : Type u} → (α → Prop) → Set α

Docstring: Turn a predicate `p : α → Prop` into a set, also written as `{x | p x}` 

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

## BASE-LIBRARY REF NonAssocSemiring.toNonUnitalNonAssocSemiring
{α : Type u} → [self : NonAssocSemiring α] → NonUnitalNonAssocSemiring α

## BASE-LIBRARY REF PowerSeries.instModule
{R : Type u_1} →
  {A : Type u_2} →
    [inst : Semiring R] → [inst_1 : AddCommMonoid A] → [_root_.Module R A] → _root_.Module R (PowerSeries A)

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

## BASE-LIBRARY REF PowerSeries.coeff
{R : Type u_1} → [inst : Semiring R] → ℕ → PowerSeries R →ₗ[R] R

Docstring: The `n`th coefficient of a formal power series. 

## BASE-LIBRARY REF PowerSeries.mk
{R : Type u_2} → (ℕ → R) → PowerSeries R

Docstring: Constructor for formal power series. 

## BASE-LIBRARY REF finsum
{M : Type u_7} → {α : Sort u_8} → [AddCommMonoid M] → (α → M) → M

Docstring: Sum of `f x` as `x` ranges over the elements of the support of `f`, if it's finite. Zero
otherwise. 

## INFORMAL STATEMENT
prop.fps.subs.rules

Composition of FPSs satisfies the rules you would expect it to satisfy: 

\textbf{(a)} If $f_1, f_2, g \in K[[x]]$ satisfy $[x^0]g = 0$, then $(f_1 + f_2) \circ g = f_1 \circ g + f_2 \circ g$. 

\textbf{(b)} If $f_1, f_2, g \in K[[x]]$ satisfy $[x^0]g = 0$, then $(f_1 \cdot f_2) \circ g = (f_1 \circ g) \cdot (f_2 \circ g)$. 

\textbf{(c)} If $f_1, f_2, g \in K[[x]]$ satisfy $[x^0]g = 0$, then $\frac{f_1}{f_2} \circ g = \frac{f_1 \circ g}{f_2 \circ g}$, as long as $f_2$ is invertible. (In particular, $f_2 \circ g$ is automatically invertible under these assumptions.) 

\textbf{(d)} If $f, g \in K[[x]]$ satisfy $[x^0]g = 0$, then $f^k \circ g = (f \circ g)^k$ for each $k \in \mathbb {N}$. 

\textbf{(e)} If $f, g, h \in K[[x]]$ satisfy $[x^0]g = 0$ and $[x^0]h = 0$, then $[x^0](g \circ h) = 0$ and $(f \circ g) \circ h = f \circ (g \circ h)$. 

\textbf{(f)} We have $\underline{a} \circ g = \underline{a}$ for each $a \in K$ and $g \in K[[x]]$. 

\textbf{(g)} We have $x \circ g = g \circ x = g$ for each $g \in K[[x]]$. 

\textbf{(h)} If $(f_i)_{i \in I} \in K[[x]]^I$ is a summable family of FPSs, and if $g \in K[[x]]$ is an FPS satisfying $[x^0]g = 0$, then the family $(f_i \circ g)_{i \in I} \in K[[x]]^I$ is summable as well and we have $(\sum _{i \in I} f_i) \circ g = \sum _{i \in I} f_i \circ g$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.coeff
def.fps.coeff

If $n\in \mathbb {N}$, and if $\mathbf{a}=\left( a_{0},a_{1},a_{2},\ldots \right) \in K\left[\left[x\right]\right]$ is an FPS, then we define an element $\left[x^{n}\right]\mathbf{a}\in K$ by 

\[  \left[x^{n}\right]\mathbf{a}:=a_{n}.  \]

 This is called the \emph{coefficient of }$x^{n}$\emph{ in }$\mathbf{a}$, or the $n$\emph{-th coefficient} of $\mathbf{a}$, or the $x^{n}$\emph{-coefficient} of $\mathbf{a}$.

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

## VERDICT
{
  "verdict": "drift",
  "justification": "Parts (f) and the left-hand identity in (g) are unnecessarily restricted. The blueprint states \u201ca\u0332 \u2218 g = a\u0332 for each a \u2208 K and g \u2208 K[[x]]\u201d and \u201cx \u2218 g = g \u2218 x = g for each g \u2208 K[[x]],\u201d with no condition on the constant coefficient of g. However, `AlgebraicCombinatorics.fps_subs_const` has the added binder `PowerSeries.constantCoeff g = 0 \u2192 ...`, and `AlgebraicCombinatorics.fps_subs_X_left` likewise has `PowerSeries.constantCoeff g = 0 \u2192 ...`. These added hypotheses make those declarations weaker and prevent them from implying the stated identities for arbitrary `g`. The unrestricted claims are statable using the total `PowerSeries.subst` operation, as already demonstrated by the unrestricted signature of `fps_subs_X_right`. To be faithful, remove the constant-coefficient hypotheses from `fps_subs_const` and `fps_subs_X_left` (or, if the underlying substitution implementation does not satisfy these identities outside zero-constant inputs, change that dependency or provide the appropriate unrestricted operation). The other listed declarations match their corresponding clauses, with the field and nonzero-constant assumptions in part (c) encoding division by an invertible power series."
}