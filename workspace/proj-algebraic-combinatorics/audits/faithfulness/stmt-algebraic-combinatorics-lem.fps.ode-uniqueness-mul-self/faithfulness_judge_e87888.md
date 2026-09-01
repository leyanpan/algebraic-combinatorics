## TARGET PowerSeries.eq_of_derivative_eq_mul_self (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_2} [inst : CommRing K] [Algebra ℚ K] {h₁ h₂ g : PowerSeries K},
  (PowerSeries.derivative K) h₁ = h₁ * g →
    (PowerSeries.derivative K) h₂ = h₂ * g → PowerSeries.constantCoeff h₁ = PowerSeries.constantCoeff h₂ → h₁ = h₂

Docstring: Uniqueness lemma: if two power series satisfy the same first-order linear ODE
`h' = h * g` with the same initial condition, they are equal.
This is used to prove `Exp_add`. 

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

## BASE-LIBRARY REF CommSemiring.toSemiring
{R : Type u} → [self : CommSemiring R] → Semiring R

## BASE-LIBRARY REF CommRing.toCommSemiring
{α : Type u} → [s : CommRing α] → CommSemiring α

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


## BASE-LIBRARY REF RingHom
(α : Type u_5) → (β : Type u_6) → [NonAssocSemiring α] → [NonAssocSemiring β] → Type (max u_5 u_6)

Docstring: Bundled semiring homomorphisms; use this for bundled ring homomorphisms too.

This extends from both `MonoidHom` and `MonoidWithZeroHom` in order to put the fields in a
sensible order, even though `MonoidWithZeroHom` already extends `MonoidHom`. 

## BASE-LIBRARY REF PowerSeries.instSemiring
{R : Type u_1} → [Semiring R] → Semiring (PowerSeries R)

## BASE-LIBRARY REF RingHom.instFunLike
{α : Type u_2} → {β : Type u_3} → {x : NonAssocSemiring α} → {x_1 : NonAssocSemiring β} → FunLike (α →+* β) α β

## BASE-LIBRARY REF PowerSeries.constantCoeff
{R : Type u_1} → [inst : Semiring R] → PowerSeries R →+* R

Docstring: The constant coefficient of a formal power series. 

## INFORMAL STATEMENT
ODE uniqueness: h' = h ·g

\leanhelper  Let $h_1, h_2, g \in K[\! [x ]\! ]$. If $h_1' = h_1 \cdot g$ and $h_2' = h_2 \cdot g$ and $[x^0] h_1 = [x^0] h_2$, then $h_1 = h_2$.

## VERDICT
{
  "verdict": "drift",
  "justification": "The informal statement says only \u201cLet $h_1,h_2,g\\in K[[x]]$\u201d and gives no hypothesis that $K$ is a commutative ring or a $\\mathbb Q$-algebra. The elaborated target instead quantifies over `\u2200 {K : Type u_2} [inst : CommRing K] [Algebra \u211a K] ...`, restricting the result to commutative $\\mathbb Q$-algebras. These are mathematically contentful added hypotheses, especially `[Algebra \u211a K]`: without characteristic-zero/divisibility assumptions, uniqueness is generally false (for example, in characteristic $p$, the derivative of $x^p$ is zero, so $0$ and $x^p$ satisfy the equation with `g = 0` and have the same constant coefficient). Thus the formal theorem does not cover the unrestricted coefficient setting stated by the blueprint. To make it faithful, the informal statement should explicitly assume that $K$ is a commutative $\\mathbb Q$-algebra (or state whatever sufficient coefficient assumptions are intended); alternatively, the target\u2019s coefficient binders would need to be generalized if a valid weaker setting is intended."
}