## TARGET PowerSeries.XnEquiv.invOfUnit (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_2} [inst : CommRing R] {n : ℕ} {a b : PowerSeries R} (ua ub : Rˣ),
  PowerSeries.constantCoeff a = ↑ua →
    PowerSeries.constantCoeff b = ↑ub → (a ≡[x^n] b) → a.invOfUnit ua ≡[x^n] b.invOfUnit ub

Docstring: x^n-equivalence is preserved by inversion via `invOfUnit` for FPS with invertible constant term
(Theorem `thm.fps.xneq.props` (d)).

The proof proceeds by strong induction on the coefficient index, using the formula
for coefficients of the inverse. 

## TARGET PowerSeries.XnEquiv.prod (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_1} [inst : CommSemiring R] {ι : Type u_2} [DecidableEq ι] {n : ℕ} {s : Finset ι}
  {a b : ι → PowerSeries R}, (∀ i ∈ s, a i ≡[x^n] b i) → ∏ i ∈ s, a i ≡[x^n] ∏ i ∈ s, b i

Docstring: x^n-equivalence is preserved by finite products (Theorem `thm.fps.xneq.props` (f), eq.thm.fps.xneq.props.e.*). 

## TARGET PowerSeries.XnEquiv.div (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_2} [inst : CommRing R] {n : ℕ} {a b c d : PowerSeries R},
  (a ≡[x^n] b) →
    (c ≡[x^n] d) →
      ∀ (u : Rˣ),
        PowerSeries.constantCoeff c = ↑u →
          ∀ (v : Rˣ), PowerSeries.constantCoeff d = ↑v → a * c.invOfUnit u ≡[x^n] b * d.invOfUnit v

Docstring: x^n-equivalence is preserved by division (Theorem `thm.fps.xneq.props` (e)). 

## TARGET PowerSeries.XnEquiv.smul (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_1} [inst : CommSemiring R] {n : ℕ} {a b : PowerSeries R}, (a ≡[x^n] b) → ∀ (r : R), r • a ≡[x^n] r • b

Docstring: x^n-equivalence is preserved by scalar multiplication (Theorem `thm.fps.xneq.props` (c)). 

## TARGET PowerSeries.XnEquiv.equivalence (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_1} [inst : CommSemiring R] (n : ℕ), Equivalence (PowerSeries.XnEquiv n)

Docstring: x^n-equivalence is an equivalence relation (Theorem `thm.fps.xneq.props` (a)). 

## TARGET PowerSeries.XnEquiv.sum (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_1} [inst : CommSemiring R] {ι : Type u_2} [DecidableEq ι] {n : ℕ} {s : Finset ι}
  {a b : ι → PowerSeries R}, (∀ i ∈ s, a i ≡[x^n] b i) → ∑ i ∈ s, a i ≡[x^n] ∑ i ∈ s, b i

Docstring: x^n-equivalence is preserved by finite sums (Theorem `thm.fps.xneq.props` (f), eq.thm.fps.xneq.props.e.+). 

## TARGET PowerSeries.XnEquiv.inv (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_2} [inst : Field K] {n : ℕ} {a b : PowerSeries K},
  PowerSeries.constantCoeff a ≠ 0 → PowerSeries.constantCoeff b ≠ 0 → (a ≡[x^n] b) → a⁻¹ ≡[x^n] b⁻¹

Docstring: x^n-equivalence is preserved by inversion for FPS over a field
(Theorem `thm.fps.xneq.props` (d)). 

## TARGET PowerSeries.XnEquiv.mul (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_1} [inst : CommSemiring R] {n : ℕ} {a b c d : PowerSeries R},
  (a ≡[x^n] b) → (c ≡[x^n] d) → a * c ≡[x^n] b * d

Docstring: x^n-equivalence is preserved by multiplication (Theorem `thm.fps.xneq.props` (b), eq.thm.fps.xneq.props.b.*). 

## TARGET PowerSeries.XnEquiv.sub (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_2} [inst : CommRing R] {n : ℕ} {a b c d : PowerSeries R}, (a ≡[x^n] b) → (c ≡[x^n] d) → a - c ≡[x^n] b - d

Docstring: x^n-equivalence is preserved by subtraction (Theorem `thm.fps.xneq.props` (b), eq.thm.fps.xneq.props.b.-). 

## TARGET PowerSeries.XnEquiv.add (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_1} [inst : CommSemiring R] {n : ℕ} {a b c d : PowerSeries R},
  (a ≡[x^n] b) → (c ≡[x^n] d) → a + c ≡[x^n] b + d

Docstring: x^n-equivalence is preserved by addition (Theorem `thm.fps.xneq.props` (b), eq.thm.fps.xneq.props.b.+). 

## PROJECT DEPENDENCY PowerSeries.XnEquiv (def)
{R : Type u_1} → [CommSemiring R] → ℕ → PowerSeries R → PowerSeries R → Prop

Body:
fun {R} [CommSemiring R] n f g => ∀ m ≤ n, (PowerSeries.coeff m) f = (PowerSeries.coeff m) g

Docstring: Two formal power series are x^n-equivalent if their first n+1 coefficients agree.
This corresponds to Definition `def.fps.xneq` in the source text.

We say `XnEquiv n f g` to mean that for all m ∈ {0, 1, ..., n},
we have `[x^m] f = [x^m] g`. 

## BASE-LIBRARY REF CommRing
Type u → Type u

Docstring: A commutative ring is a ring with commutative multiplication. 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF PowerSeries
Type u_1 → Type (max u_1 0)

Docstring: Formal power series over a coefficient type `R` 

## BASE-LIBRARY REF Units
(α : Type u) → [Monoid α] → Type u

Docstring: Units of a `Monoid`, bundled version. Notation: `αˣ`.

An element of a `Monoid` is a unit if it has a two-sided inverse.
This version bundles the inverse element so that it can be computed.
For a predicate see `IsUnit`. 

## BASE-LIBRARY REF MonoidWithZero.toMonoid
{M₀ : Type u} → [self : MonoidWithZero M₀] → Monoid M₀

## BASE-LIBRARY REF Semiring.toMonoidWithZero
{α : Type u} → [self : Semiring α] → MonoidWithZero α

## BASE-LIBRARY REF CommSemiring.toSemiring
{R : Type u} → [self : CommSemiring R] → Semiring R

## BASE-LIBRARY REF CommRing.toCommSemiring
{α : Type u} → [s : CommRing α] → CommSemiring α

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

## BASE-LIBRARY REF RingHom.instFunLike
{α : Type u_2} → {β : Type u_3} → {x : NonAssocSemiring α} → {x_1 : NonAssocSemiring β} → FunLike (α →+* β) α β

## BASE-LIBRARY REF PowerSeries.constantCoeff
{R : Type u_1} → [inst : Semiring R] → PowerSeries R →+* R

Docstring: The constant coefficient of a formal power series. 

## BASE-LIBRARY REF Units.val
{α : Type u} → [inst : Monoid α] → αˣ → α

Docstring: The underlying value in the base `Monoid`. 

## BASE-LIBRARY REF PowerSeries.invOfUnit
{R : Type u_1} → [inst : Ring R] → PowerSeries R → Rˣ → PowerSeries R

Docstring: A formal power series is invertible if the constant coefficient is invertible. 

## BASE-LIBRARY REF CommRing.toRing
{α : Type u} → [self : CommRing α] → Ring α

## BASE-LIBRARY REF CommSemiring
Type u → Type u

Docstring: A commutative semiring is a semiring with commutative multiplication. 

## BASE-LIBRARY REF DecidableEq
Sort u → Sort (max 1 u)

Docstring: Propositional equality is `Decidable` for all elements of a type.

In other words, an instance of `DecidableEq α` is a means of deciding the proposition `a = b` is
for all `a b : α`.


## BASE-LIBRARY REF Finset
Type u_4 → Type u_4

Docstring: `Finset α` is the type of finite sets of elements of `α`. It is implemented
as a multiset (a list up to permutation) which has no duplicate elements. 

## BASE-LIBRARY REF Membership.mem
{α : outParam (Type u)} → {γ : Type v} → [self : Membership α γ] → γ → α → Prop

Docstring: The membership relation `a ∈ s : Prop` where `a : α`, `s : γ`. 

Conventions for notations in identifiers:

 * The recommended spelling of `∈` in identifiers is `mem`.

## BASE-LIBRARY REF Finset.instMembership
{α : Type u_1} → Membership α (Finset α)

## BASE-LIBRARY REF Finset.prod
{ι : Type u_1} → {M : Type u_3} → [CommMonoid M] → Finset ι → (ι → M) → M

Docstring: `∏ x ∈ s, f x` is the product of `f x` as `x` ranges over the elements of the finite set `s`.

When the index type is a `Fintype`, the notation `∏ x, f x`, is a shorthand for
`∏ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF CommSemiring.toCommMonoid
{R : Type u} → [self : CommSemiring R] → CommMonoid R

## BASE-LIBRARY REF PowerSeries.instCommSemiring
{R : Type u_1} → [CommSemiring R] → CommSemiring (PowerSeries R)

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

## BASE-LIBRARY REF PowerSeries.instAlgebra
{R : Type u_1} →
  {A : Type u_2} → [inst : Semiring A] → [inst_1 : CommSemiring R] → [Algebra R A] → Algebra R (PowerSeries A)

## BASE-LIBRARY REF Algebra.id
(R : Type u) → [inst : CommSemiring R] → Algebra R R

Docstring: The identity map inducing an `Algebra` structure. 

## BASE-LIBRARY REF Equivalence
{α : Sort u} → (α → α → Prop) → Prop

Docstring: An equivalence relation `r : α → α → Prop` is a relation that is

* reflexive: `r x x`,
* symmetric: `r x y` implies `r y x`, and
* transitive: `r x y` and `r y z` implies `r x z`.

Equality is an equivalence relation, and equivalence relations share many of the properties of
equality.


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

## BASE-LIBRARY REF NonAssocSemiring.toNonUnitalNonAssocSemiring
{α : Type u} → [self : NonAssocSemiring α] → NonUnitalNonAssocSemiring α

## BASE-LIBRARY REF Field
Type u → Type u

Docstring: A `Field` is a `CommRing` with multiplicative inverses for nonzero elements.

An instance of `Field K` includes maps `ratCast : ℚ → K` and `qsmul : ℚ → K → K`.
Those two fields are needed to implement the `DivisionRing K → Algebra ℚ K` instance since we need
to control the specific definitions for some special cases of `K` (in particular `K = ℚ` itself).
See also note [forgetful inheritance].

If the field has positive characteristic `p`, our division by zero convention forces
`ratCast (1 / p) = 1 / 0 = 0`. 

## BASE-LIBRARY REF Ne
{α : Sort u} → α → α → Prop

Docstring: `a ≠ b`, or `Ne a b` is defined as `¬ (a = b)` or `a = b → False`,
and asserts that `a` and `b` are not equal.


Conventions for notations in identifiers:

 * The recommended spelling of `≠` in identifiers is `ne`.

## BASE-LIBRARY REF DivisionSemiring.toSemiring
{K : Type u_2} → [self : DivisionSemiring K] → Semiring K

## BASE-LIBRARY REF Semifield.toDivisionSemiring
{K : Type u_2} → [self : Semifield K] → DivisionSemiring K

## BASE-LIBRARY REF Field.toSemifield
{K : Type u_1} → [Field K] → Semifield K

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

## BASE-LIBRARY REF LE.le
{α : Type u} → [self : LE α] → α → α → Prop

Docstring: The less-equal relation: `x ≤ y` 

Conventions for notations in identifiers:

 * The recommended spelling of `≤` in identifiers is `le`.

 * The recommended spelling of `<=` in identifiers is `le` (prefer `≤` over `<=`).

## BASE-LIBRARY REF instLENat
LE ℕ

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

## INFORMAL STATEMENT
thm.fps.xneq.props

Let $n\in \mathbb {N}$. \medskip 

\textbf{(a)} The relation $\overset {x^{n}}{\equiv }$ on $K\left[\left[ x\right]\right]$ is an equivalence relation. In other words: 

\begin{itemize} \item This relation is reflexive (i.e., we have $f\overset {x^{n}}{\equiv }f$ for each $f\in K\left[\left[x\right]\right]$). 

\item This relation is transitive (i.e., if three FPSs $f,g,h\in K\left[ \left[x\right]\right]$ satisfy $f\overset {x^{n}}{\equiv }g$ and $g\overset {x^{n}}{\equiv }h$, then $f\overset {x^{n}}{\equiv }h$). 

\item This relation is symmetric (i.e., if two FPSs $f,g\in K\left[\left[ x\right]\right]$ satisfy $f\overset {x^{n}}{\equiv }g$, then $g\overset {x^{n}}{\equiv }f$). 

\end{itemize}

\textbf{(b)} If $a,b,c,d\in K\left[\left[x\right]\right]$ are four FPSs satisfying $a\overset {x^{n}}{\equiv }b$ and $c\overset {x^{n}}{\equiv }d$, then we also have 

\begin{align} &  a+c\overset {x^{n}}{\equiv }b+d;\\ &  a-c\overset {x^{n}}{\equiv }b-d;\\ &  ac\overset {x^{n}}{\equiv }bd.  \end{align}

\textbf{(c)} If $a,b\in K\left[\left[x\right]\right]$ are two FPSs satisfying $a\overset {x^{n}}{\equiv }b$, then $\lambda a\overset {x^{n}}{\equiv }\lambda b$ for each $\lambda \in K$. \medskip 

\textbf{(d)} If $a,b\in K\left[\left[x\right]\right]$ are two invertible FPSs satisfying $a\overset {x^{n}}{\equiv }b$, then $a^{-1} \overset {x^{n}}{\equiv }b^{-1}$. \medskip 

\textbf{(e)} If $a,b,c,d\in K\left[\left[x\right]\right]$ are four FPSs satisfying $a\overset {x^{n}}{\equiv }b$ and $c\overset {x^{n}}{\equiv }d$, and if the FPSs $c$ and $d$ are invertible, then we also have 

\begin{equation}  \frac{a}{c}\overset {x^{n}}{\equiv }\frac{b}{d}.  \end{equation}

\textbf{(f)} Let $S$ be a finite set. Let $\left(a_{s}\right)_{s\in S}\in K\left[\left[x\right]\right]^{S}$ and $\left(b_{s}\right)_{s\in S}\in K\left[\left[x\right]\right]^{S}$ be two families of FPSs such that 

\begin{equation}  \text{each }s\in S\text{ satisfies }a_{s}\overset {x^{n}}{\equiv }b_{s}.  \end{equation}

 Then, we have 

\begin{align} &  \sum _{s\in S}a_{s}\overset {x^{n}}{\equiv }\sum _{s\in S}b_{s} ;\\ &  \prod _{s\in S}a_{s}\overset {x^{n}}{\equiv }\prod _{s\in S}b_{s}.  \end{align}

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.xneq
def.fps.xneq

Let $n\in \mathbb {N}$. Let $f,g\in K\left[\left[x\right]\right]$ be two FPSs. We write $f\overset {x^{n}}{\equiv }g$ if and only if 

\[  \text{each }m\in \left\{ 0,1,\ldots ,n\right\} \text{ satisfies } \left[x^{m}\right]f=\left[x^{m}\right]g.  \]

Thus, we have defined a binary relation $\overset {x^{n}}{\equiv }$ on the set $K\left[\left[x\right]\right]$. We say that an FPS $f$ is $x^{n}$\emph{-equivalent} to an FPS $g$ if and only if $f\overset {x^{n}}{\equiv }g$.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The project definition exactly matches the blueprint definition: `PowerSeries.XnEquiv n f g` has body `\u2200 m \u2264 n, coeff m f = coeff m g`, corresponding to \u201ceach m \u2208 {0,1,\u2026,n} satisfies [x^m]f = [x^m]g.\u201d The targets then cover every listed property: `equivalence` gives (a); `add`, `sub`, and `mul` give (b); `smul` gives (c); `invOfUnit` gives (d) over a commutative ring when the constant coefficients are represented by units, while `inv` gives the field specialization under the equivalent nonzero-constant condition; `div` expresses (e) as `a * c.invOfUnit u \u2261[x^n] b * d.invOfUnit v`; and `sum` and `prod` give (f). The unit binders and equations, e.g. `(ua ub : R\u02e3), constantCoeff a = \u2191ua \u2192 constantCoeff b = \u2191ub`, encode the invertibility assumptions on the power series rather than adding unrelated hypotheses. The `[DecidableEq \u03b9]` binders in `sum` and `prod` are implementation-level encoding for `Finset`. Several declarations are strictly more general than the blueprint\u2019s common coefficient setting\u2014for example, equivalence, addition, multiplication, scalar multiplication, sums, and products only assume `[CommSemiring R]`, while subtraction and unit-based inversion assume `[CommRing R]`; this stronger generality does not impair faithfulness."
}