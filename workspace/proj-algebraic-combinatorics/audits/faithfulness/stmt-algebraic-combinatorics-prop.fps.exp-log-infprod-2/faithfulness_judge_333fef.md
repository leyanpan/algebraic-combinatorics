## TARGET PowerSeries.Log_tprod (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_2} [inst : CommRing K] [inst_1 : Algebra ℚ K] {I : Type u_3} (f : I → ↑PowerSeries.PowerSeries₁)
  (hf : PowerSeries.MultipliableFPS₁ f) (hf_sum : optParam (PowerSeries.SummableFPS₀ fun i => PowerSeries.Log (f i)) ⋯),
  PowerSeries.Log (PowerSeries.multipliableFPS₁Prod f hf) =
    PowerSeries.summableFPS₀Sum (fun i => PowerSeries.Log (f i)) hf_sum

Docstring: **Proposition prop.fps.Exp-Log-infprod**: Log converts infinite products to infinite sums.

If `(f_i)_{i ∈ I}` is a multipliable family of FPSs in `K⟦X⟧₁`, then:
1. `(Log f_i)_{i ∈ I}` is a summable family of FPSs in `K⟦X⟧₀`
2. `∏_{i ∈ I} f_i ∈ K⟦X⟧₁`
3. `Log(∏_{i ∈ I} f_i) = ∑_{i ∈ I} Log(f_i)`

This is the infinite version of `Log_mul`: `Log(fg) = Log(f) + Log(g)`.

The proof strategy:
1. Use `Log_mul` for finite products
2. Show that for multipliable families, the finite partial products converge
3. Use continuity of Log (which follows from the coefficient-wise definition)
   to pass to the limit


## PROJECT DEPENDENCY PowerSeries.PowerSeries₁ (def)
{R : Type u_2} → [CommRing R] → Set (PowerSeries R)

Body:
fun {R} [CommRing R] => {f | PowerSeries.constantCoeff f = 1}

Docstring: `R⟦X⟧₁` is the set of FPS with constant term 1.
This is Definition 7.8.6(b) (def.fps.Exp-Log-maps). 

## PROJECT DEPENDENCY PowerSeries.MultipliableFPS₁ (def)
{K : Type u_2} → [inst : CommRing K] → {I : Type u_3} → (I → ↑PowerSeries.PowerSeries₁) → Prop

Body:
fun {K} [CommRing K] {I} f => PowerSeries.Multipliable fun i => ↑(f i)

Docstring: A family of FPS in `K⟦X⟧₁` is multipliable if for each coefficient index n,
the n-th coefficient of the product is finitely determined.

This is the notion of multipliability appropriate for `K⟦X⟧₁`. 

## PROJECT DEPENDENCY PowerSeries.SummableFPS₀ (def)
{K : Type u_2} → [inst : CommRing K] → {I : Type u_3} → (I → ↑PowerSeries.PowerSeries₀) → Prop

Body:
fun {K} [CommRing K] {I} f => ∀ (n : ℕ), {i | (PowerSeries.coeff n) ↑(f i) ≠ 0}.Finite

Docstring: A family of FPS in `K⟦X⟧₀` is summable if for each coefficient index n,
only finitely many family members have nonzero n-th coefficient.

This is the notion of summability appropriate for `K⟦X⟧₀`. 

## PROJECT DEPENDENCY PowerSeries.Log (def)
{K : Type u_2} → [inst : CommRing K] → [Algebra ℚ K] → ↑PowerSeries.PowerSeries₁ → ↑PowerSeries.PowerSeries₀

Body:
fun {K} [CommRing K] [Algebra ℚ K] f => ⟨PowerSeries.subst (↑f - 1) (PowerSeries.logbar K), ⋯⟩

Docstring: The logarithm map `Log : K⟦X⟧₁ → K⟦X⟧₀` defined by `f ↦ logbar ∘ (f - 1)`.
This is Definition 7.8.6(c) (def.fps.Exp-Log-maps). 

## PROJECT DEPENDENCY PowerSeries.Log_summable_of_multipliable (theorem)
∀ {K : Type u_2} [inst : CommRing K] [inst_1 : Algebra ℚ K] {I : Type u_3} (f : I → ↑PowerSeries.PowerSeries₁),
  PowerSeries.MultipliableFPS₁ f → PowerSeries.SummableFPS₀ fun i => PowerSeries.Log (f i)

Docstring: If `(f_i)_{i ∈ I}` is a multipliable family in `K⟦X⟧₁`, then `(Log f_i)_{i ∈ I}` is
a summable family in `K⟦X⟧₀`.

This is part of Proposition prop.fps.Exp-Log-infprod from the source material. 

## PROJECT DEPENDENCY PowerSeries.PowerSeries₀ (def)
{R : Type u_2} → [CommRing R] → Set (PowerSeries R)

Body:
fun {R} [CommRing R] => {f | PowerSeries.constantCoeff f = 0}

Docstring: `R⟦X⟧₀` is the set of FPS with constant term 0.
This is Definition 7.8.6(a) (def.fps.Exp-Log-maps). 

## PROJECT DEPENDENCY PowerSeries.multipliableFPS₁Prod (def)
{K : Type u_2} →
  [inst : CommRing K] →
    {I : Type u_3} → (f : I → ↑PowerSeries.PowerSeries₁) → PowerSeries.MultipliableFPS₁ f → ↑PowerSeries.PowerSeries₁

Body:
fun {K} [CommRing K] {I} f hf => ⟨PowerSeries.tprod (fun i => ↑(f i)) hf, ⋯⟩

Docstring: The product of a multipliable family in `K⟦X⟧₁` as an element of `K⟦X⟧₁`. 

## PROJECT DEPENDENCY PowerSeries.summableFPS₀Sum (def)
{K : Type u_2} →
  [inst : CommRing K] →
    {I : Type u_3} → (f : I → ↑PowerSeries.PowerSeries₀) → PowerSeries.SummableFPS₀ f → ↑PowerSeries.PowerSeries₀

Body:
fun {K} [CommRing K] {I} f _hf => ⟨PowerSeries.mk fun n => ∑ᶠ (i : I), (PowerSeries.coeff n) ↑(f i), ⋯⟩

Docstring: The coefficient-wise sum of a summable family in `K⟦X⟧₀`.

**Important:** This is defined coefficient-wise using `mk`, NOT using `finsum` on the entire
power series. The reason is that `finsum` returns 0 when the support is infinite, but
`SummableFPS₀` only guarantees finite support for each coefficient, not for the entire family.

For each coefficient n, only finitely many terms contribute (by `SummableFPS₀`), so the
finsum `∑ᶠ i, coeff n (f i).val` is well-defined and equals a finite sum. 

## PROJECT DEPENDENCY PowerSeries.Multipliable (def)
{R : Type u_1} → [CommRing R] → {I : Type u_2} → (I → PowerSeries R) → Prop

Body:
fun {R} [CommRing R] {I} a => ∀ (n : ℕ), PowerSeries.CoeffFinitelyDeterminedInProd a n

Docstring: A family `(a_i)_{i ∈ I}` of FPS is multipliable if for each `n ∈ ℕ`,
the `x^n`-coefficient in its product is finitely determined.
(Label: def.fps.multipliable part (a)) 

## PROJECT DEPENDENCY PowerSeries.logbar (def)
(K : Type u_1) → [inst : CommRing K] → [Algebra ℚ K] → PowerSeries K

Body:
fun K [CommRing K] [Algebra ℚ K] => PowerSeries.mk fun n => if n = 0 then 0 else (algebraMap ℚ K) ((-1) ^ (n - 1) / ↑n)

Docstring: The logarithm series `logbar = ∑_{n≥1} (-1)^{n-1}/n · x^n`, which is the Mercator series
for `log(1+x)`. This is `\overline{\log}` in Definition 7.8.2 (def.fps.exp-log). 

## PROJECT DEPENDENCY PowerSeries.tprod (def)
{R : Type u_1} →
  [inst : CommRing R] → {I : Type u_2} → (a : I → PowerSeries R) → PowerSeries.Multipliable a → PowerSeries R

Body:
fun {R} [CommRing R] {I} a ha => PowerSeries.mk fun n => PowerSeries.tprodCoeff a ha n

Docstring: The infinite product of a multipliable family of formal power series.
For a multipliable family `(a_i)_{i ∈ I}`, this is the FPS whose `x^n`-coefficient
equals the `x^n`-coefficient of any finite partial product that determines it.
(Label: def.fps.multipliable part (b)) 

## PROJECT DEPENDENCY PowerSeries.MultipliableFPS₁.prod_mem (theorem)
∀ {K : Type u_2} [inst : CommRing K] {I : Type u_3} (f : I → ↑PowerSeries.PowerSeries₁)
  (hf : PowerSeries.MultipliableFPS₁ f), PowerSeries.tprod (fun i => ↑(f i)) hf ∈ PowerSeries.PowerSeries₁

Docstring: For a multipliable family in `K⟦X⟧₁`, the product is also in `K⟦X⟧₁`. 

## PROJECT DEPENDENCY PowerSeries.CoeffFinitelyDeterminedInProd (def)
{R : Type u_1} → [CommRing R] → {I : Type u_2} → (I → PowerSeries R) → ℕ → Prop

Body:
fun {R} [CommRing R] {I} a n => ∃ M, PowerSeries.DeterminesCoeffInProd a M n

Docstring: The `x^n`-coefficient in the product of `(a_i)_{i ∈ I}` is finitely determined
if there exists a finite subset `M` that determines it.
(Label: def.fps.xn-coeff-fin-determined part (b)) 

## PROJECT DEPENDENCY PowerSeries.tprodCoeff (def)
{R : Type u_1} → [inst : CommRing R] → {I : Type u_2} → (a : I → PowerSeries R) → PowerSeries.Multipliable a → ℕ → R

Body:
fun {R} [CommRing R] {I} a ha n => (PowerSeries.coeff n) (∏ i ∈ Exists.choose ⋯, a i)

Docstring: For a multipliable family, the `n`-th coefficient of the infinite product.
This is the common value of `(∏ i ∈ M, a i).coeff n` for any finite `M` that
determines the `x^n`-coefficient.
(Label: def.fps.multipliable part (b)) 

## PROJECT DEPENDENCY PowerSeries.DeterminesCoeffInProd (def)
{R : Type u_1} → [CommRing R] → {I : Type u_2} → (I → PowerSeries R) → Finset I → ℕ → Prop

Body:
fun {R} [CommRing R] {I} a M n =>
  ∀ (J : Finset I), M ⊆ J → (PowerSeries.coeff n) (∏ i ∈ J, a i) = (PowerSeries.coeff n) (∏ i ∈ M, a i)

Docstring: A finite subset `M` of `I` determines the `x^n`-coefficient in the product of
a family `(a_i)_{i ∈ I}` if for every finite superset `J` of `M`, the `x^n`-coefficient
of `∏_{i ∈ J} a_i` equals that of `∏_{i ∈ M} a_i`.
(Label: def.fps.determines-xn-coeff part (b)) 

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

## BASE-LIBRARY REF Set.Elem
{α : Type u} → Set α → Type u

Docstring: Given the set `s`, `Elem s` is the `Type` of element of `s`.

It is currently an abbreviation so that instance coming from `Subtype` are available.
If you're interested in making it a `def`, as it probably should be,
you'll then need to create additional instances (and possibly prove lemmas about them).
See e.g. `Mathlib/Data/Set/Order.lean`.


## BASE-LIBRARY REF PowerSeries
Type u_1 → Type (max u_1 0)

Docstring: Formal power series over a coefficient type `R` 

## BASE-LIBRARY REF optParam
(α : Sort u) → α → Sort u

Docstring: Gadget for optional parameter support.

A binder like `(x : α := default)` in a declaration is syntax sugar for
`x : optParam α default`, and triggers the elaborator to attempt to use
`default` to supply the argument if it is not supplied.


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

## BASE-LIBRARY REF Set
Type u → Type u

Docstring: A set is a collection of elements of some type `α`.

Although `Set` is defined as `α → Prop`, this is an implementation detail which should not be
relied on. Instead, `setOf` and membership of a set (`∈`) should be used to convert between sets
and predicates.


## BASE-LIBRARY REF setOf
{α : Type u} → (α → Prop) → Set α

Docstring: Turn a predicate `p : α → Prop` into a set, also written as `{x | p x}` 

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

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF One.toOfNat1
{α : Type u_1} → [One α] → OfNat α 1

## BASE-LIBRARY REF AddMonoidWithOne.toOne
{R : Type u_2} → [self : AddMonoidWithOne R] → One R

## BASE-LIBRARY REF AddGroupWithOne.toAddMonoidWithOne
{R : Type u} → [self : AddGroupWithOne R] → AddMonoidWithOne R

## BASE-LIBRARY REF Ring.toAddGroupWithOne
{R : Type u} → [self : Ring R] → AddGroupWithOne R

## BASE-LIBRARY REF CommRing.toRing
{α : Type u} → [self : CommRing α] → Ring α

## BASE-LIBRARY REF Subtype.val
{α : Sort u} → {p : α → Prop} → Subtype p → α

Docstring: The value in the underlying type that satisfies the predicate.


## BASE-LIBRARY REF Membership.mem
{α : outParam (Type u)} → {γ : Type v} → [self : Membership α γ] → γ → α → Prop

Docstring: The membership relation `a ∈ s : Prop` where `a : α`, `s : γ`. 

Conventions for notations in identifiers:

 * The recommended spelling of `∈` in identifiers is `mem`.

## BASE-LIBRARY REF Set.instMembership
{α : Type u} → Membership α (Set α)

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF Set.Finite
{α : Type u} → Set α → Prop

Docstring: A set is finite if the corresponding `Subtype` is finite,
i.e., if there exists a natural `n : ℕ` and an equivalence `s ≃ Fin n`. 

## BASE-LIBRARY REF Ne
{α : Sort u} → α → α → Prop

Docstring: `a ≠ b`, or `Ne a b` is defined as `¬ (a = b)` or `a = b → False`,
and asserts that `a` and `b` are not equal.


Conventions for notations in identifiers:

 * The recommended spelling of `≠` in identifiers is `ne`.

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

## BASE-LIBRARY REF PowerSeries.instAddCommMonoid
{R : Type u_1} → [AddCommMonoid R] → AddCommMonoid (PowerSeries R)

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.toAddCommMonoid
{α : Type u} → [self : NonUnitalNonAssocSemiring α] → AddCommMonoid α

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

## BASE-LIBRARY REF Subtype.mk
{α : Sort u} → {p : α → Prop} → (val : α) → p val → Subtype p

## BASE-LIBRARY REF PowerSeries.subst
{R : Type u_2} →
  [inst : CommRing R] →
    {τ : Type u_3} →
      {S : Type u_4} → [inst_1 : CommRing S] → [Algebra R S] → MvPowerSeries τ S → PowerSeries R → MvPowerSeries τ S

Docstring: Substitution of power series into a power series. 

## BASE-LIBRARY REF Unit
Type

Docstring: The canonical type with one element. This element is written `()`.

`Unit` has a number of uses:
* It can be used to model control flow that returns from a function call without providing other
  information.
* Monadic actions that return `Unit` have side effects without computing values.
* In polymorphic types, it can be used to indicate that no data is to be stored in a particular
  field.


## BASE-LIBRARY REF Algebra.id
(R : Type u) → [inst : CommSemiring R] → Algebra R R

Docstring: The identity map inducing an `Algebra` structure. 

## BASE-LIBRARY REF HSub.hSub
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HSub α β γ] → α → β → γ

Docstring: `a - b` computes the difference of `a` and `b`.
The meaning of this notation is type-dependent.
* For natural numbers, this operator saturates at 0: `a - b = 0` when `a ≤ b`. 

Conventions for notations in identifiers:

 * The recommended spelling of `-` in identifiers is `sub` (when used as a binary operator).

## BASE-LIBRARY REF MvPowerSeries
Type u_1 → Type u_2 → Type (max (max u_2 0) u_1)

Docstring: Multivariate formal power series, where `σ` is the index set of the variables
and `R` is the coefficient ring. 

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

## BASE-LIBRARY REF MvPowerSeries.instOne
{σ : Type u_1} → {R : Type u_2} → [Semiring R] → One (MvPowerSeries σ R)

## BASE-LIBRARY REF PowerSeries.mk
{R : Type u_2} → (ℕ → R) → PowerSeries R

Docstring: Constructor for formal power series. 

## BASE-LIBRARY REF finsum
{M : Type u_7} → {α : Sort u_8} → [AddCommMonoid M] → (α → M) → M

Docstring: Sum of `f x` as `x` ranges over the elements of the support of `f`, if it's finite. Zero
otherwise. 

## BASE-LIBRARY REF ite
{α : Sort u} → (c : Prop) → [h : Decidable c] → α → α → α

Docstring: `if c then t else e` is notation for `ite c t e`, "if-then-else", which decides to
return `t` or `e` depending on whether `c` is true or false. The explicit argument
`c : Prop` does not have any actual computational content, but there is an additional
`[Decidable c]` argument synthesized by typeclass inference which actually
determines how to evaluate `c` to true or false. Write `if h : c then t else e`
instead for a "dependent if-then-else" `dite`, which allows `t`/`e` to use the fact
that `c` is true/false.


## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

## BASE-LIBRARY REF instDecidableEqNat
DecidableEq ℕ

## BASE-LIBRARY REF algebraMap
(R : Type u) → (A : Type v) → [inst : CommSemiring R] → [inst_1 : Semiring A] → [Algebra R A] → R →+* A

Docstring: Embedding `R →+* A` given by `Algebra` structure. 

## BASE-LIBRARY REF HDiv.hDiv
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HDiv α β γ] → α → β → γ

Docstring: `a / b` computes the result of dividing `a` by `b`.
The meaning of this notation is type-dependent.
* For most types like `Nat`, `Int`, `Rat`, `Real`, `a / 0` is defined to be `0`.
* For `Nat`, `a / b` rounds downwards.
* For `Int`, `a / b` rounds downwards if `b` is positive or upwards if `b` is negative.
  It is implemented as `Int.ediv`, the unique function satisfying
  `a % b + b * (a / b) = a` and `0 ≤ a % b < natAbs b` for `b ≠ 0`.
  Other rounding conventions are available using the functions
  `Int.fdiv` (floor rounding) and `Int.tdiv` (truncation rounding).
* For `Float`, `a / 0` follows the IEEE 754 semantics for division,
  usually resulting in `inf` or `nan`. 

Conventions for notations in identifiers:

 * The recommended spelling of `/` in identifiers is `div`.

## BASE-LIBRARY REF instHDiv
{α : Type u_1} → [Div α] → HDiv α α α

## BASE-LIBRARY REF Rat.instDiv
Div ℚ

Docstring: Division of rational numbers. Note: `div a 0 = 0`.  Written with a separate function `Rat.div`
as a wrapper so that the definition is not unfolded at `.instance` transparency. 

## BASE-LIBRARY REF HPow.hPow
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HPow α β γ] → α → β → γ

Docstring: `a ^ b` computes `a` to the power of `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `^` in identifiers is `pow`.

## BASE-LIBRARY REF instHPow
{α : Type u_1} → {β : Type u_2} → [Pow α β] → HPow α β α

## BASE-LIBRARY REF Rat.instPowNat
Pow ℚ ℕ

## BASE-LIBRARY REF Neg.neg
{α : Type u} → [self : Neg α] → α → α

Docstring: `-a` computes the negative or opposite of `a`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `-` in identifiers is `neg` (when used as a unary operator).

## BASE-LIBRARY REF Rat.instNeg
Neg ℚ

## BASE-LIBRARY REF Rat.instOfNat
{n : ℕ} → OfNat ℚ n

## BASE-LIBRARY REF instSubNat
Sub ℕ

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


## BASE-LIBRARY REF Rat.instNatCast
NatCast ℚ

## BASE-LIBRARY REF Exists
{α : Sort u} → (α → Prop) → Prop

Docstring: Existential quantification. If `p : α → Prop` is a predicate, then `∃ x : α, p x`
asserts that there is some `x` of type `α` such that `p x` holds.
To create an existential proof, use the `exists` tactic,
or the anonymous constructor notation `⟨x, h⟩`.
To unpack an existential, use `cases h` where `h` is a proof of `∃ x : α, p x`,
or `let ⟨x, hx⟩ := h` where `.

Because Lean has proof irrelevance, any two proofs of an existential are
definitionally equal. One consequence of this is that it is impossible to recover the
witness of an existential from the mere fact of its existence.
For example, the following does not compile:
```
example (h : ∃ x : Nat, x = x) : Nat :=
  let ⟨x, _⟩ := h  -- fail, because the goal is `Nat : Type`
  x
```
The error message `recursor 'Exists.casesOn' can only eliminate into Prop` means
that this only works when the current goal is another proposition:
```
example (h : ∃ x : Nat, x = x) : True :=
  let ⟨x, _⟩ := h  -- ok, because the goal is `True : Prop`
  trivial
```


## BASE-LIBRARY REF Finset
Type u_4 → Type u_4

Docstring: `Finset α` is the type of finite sets of elements of `α`. It is implemented
as a multiset (a list up to permutation) which has no duplicate elements. 

## BASE-LIBRARY REF Finset.prod
{ι : Type u_1} → {M : Type u_3} → [CommMonoid M] → Finset ι → (ι → M) → M

Docstring: `∏ x ∈ s, f x` is the product of `f x` as `x` ranges over the elements of the finite set `s`.

When the index type is a `Fintype`, the notation `∏ x, f x`, is a shorthand for
`∏ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF CommRing.toCommMonoid
{α : Type u} → [self : CommRing α] → CommMonoid α

## BASE-LIBRARY REF PowerSeries.instCommRing
{R : Type u_1} → [CommRing R] → CommRing (PowerSeries R)

## BASE-LIBRARY REF Exists.choose
{α : Sort u_1} → {p : α → Prop} → (∃ a, p a) → α

Docstring: Extract an element from an existential statement, using `Classical.choose`. 

## BASE-LIBRARY REF HasSubset.Subset
{α : Type u} → [self : HasSubset α] → α → α → Prop

Docstring: Subset relation: `a ⊆ b`  

Conventions for notations in identifiers:

 * The recommended spelling of `⊆` in identifiers is `subset`.

## BASE-LIBRARY REF Finset.instHasSubset
{α : Type u_1} → HasSubset (Finset α)

## INFORMAL STATEMENT
prop.fps.Exp-Log-infprod

Assume that $K$ is a commutative $\mathbb {Q}$-algebra. Let $\left( f_{i}\right) _{i\in I}\in K\left[ \left[ x\right] \right] ^{I}$ be a multipliable family of FPSs in $K\left[ \left[ x\right] \right] _{1}$. Then, $\left( \operatorname {Log}f_{i}\right) _{i\in I}$ is a summable family of FPS in $K\left[ \left[ x\right] \right] _{0}$, and we have $\prod \limits _{i\in I}f_{i}\in K\left[ \left[ x\right] \right] _{1}$ and

\[  \operatorname {Log}\left( \prod \limits _{i\in I}f_{i}\right) =\sum _{i\in I}\left( \operatorname {Log}f_{i}\right) .  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-conv.fps.exp.k-q-alg
conv.fps.exp.K-Q-alg

Throughout this section (unless otherwise stated), we assume that $K$ is not just a commutative ring, but actually a commutative $\mathbb {Q}$-algebra.

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.determines-xn-coeff
def.fps.determines-xn-coeff

Let $\left(\mathbf{a}_{i}\right)_{i\in I}\in K\left[\left[x\right]\right]^{I}$ be a (possibly infinite) family of FPSs. Let $n\in \mathbb {N}$. Let $M$ be a finite subset of $I$. 

\textbf{(a)} We say that $M$ \emph{determines the $x^{n}$-coefficient in the sum of} $\left(\mathbf{a}_{i}\right)_{i\in I}$ if every finite subset $J$ of $I$ satisfying $M\subseteq J\subseteq I$ satisfies 

\[  \left[x^{n}\right]\left(\sum _{i\in J}\mathbf{a}_{i}\right) =\left[x^{n}\right]\left(\sum _{i\in M}\mathbf{a}_{i}\right).  \]

\textbf{(b)} We say that $M$ \emph{determines the $x^{n}$-coefficient in the product of} $\left(\mathbf{a}_{i}\right)_{i\in I}$ if every finite subset $J$ of $I$ satisfying $M\subseteq J\subseteq I$ satisfies 

\[  \left[x^{n}\right]\left(\prod _{i\in J}\mathbf{a}_{i}\right) =\left[x^{n}\right]\left(\prod _{i\in M}\mathbf{a}_{i}\right).  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.exp-log
def.fps.exp-log

Define three FPS $\exp $, $\overline{\log }$ and $\overline{\exp }$ in $K\left[\left[x\right]\right]$ by 

\begin{align*}  \exp &  :=\sum _{n\in \mathbb {N}}\frac{1}{n!}x^{n},\\ \overline{\log } &  :=\sum _{n\geq 1}\frac{\left(-1\right)^{n-1}}{n}x^{n},\\ \overline{\exp } &  :=\exp -1=\sum _{n\geq 1}\frac{1}{n!}x^{n}. \end{align*}

(The last equality sign here follows from $\exp =\sum _{n\in \mathbb {N}}\frac{1}{n!}x^{n}=\underbrace{\frac{1}{0!}}_{=1}\underbrace{x^{0}}_{=1} +\sum _{n\geq 1}\frac{1}{n!}x^{n}=1+\sum _{n\geq 1}\frac{1}{n!}x^{n}$.)

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.exp-log-maps
def.fps.Exp-Log-maps

\textbf{(a)} We let $K\left[\left[x\right] \right]_{0}$ denote the set of all FPSs $f\in K\left[\left[x\right] \right]$ with $\left[x^{0}\right]f=0$. \medskip 

\textbf{(b)} We let $K\left[\left[x\right]\right]_{1}$ denote the set of all FPSs $f\in K\left[\left[x\right]\right]$ with $\left[ x^{0}\right]f=1$. \medskip 

\textbf{(c)} We define two maps 

\begin{align*}  \operatorname {Exp}:K\left[\left[x\right]\right]_{0} &  \rightarrow K\left[\left[x\right]\right]_{1},\\ g &  \mapsto \exp \circ g \end{align*}

 and 

\begin{align*}  \operatorname {Log}:K\left[\left[x\right]\right]_{1} &  \rightarrow K\left[\left[x\right]\right]_{0},\\ f &  \mapsto \overline{\log }\circ \left(f-1\right). \end{align*}

 (These two maps are well-defined according to parts \textbf{(c)} and \textbf{(d)} of Lemma \ref{lem.fps.Exp-Log-maps-wd} below.)

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.summable-multipliable
Summable and multipliable families

\leanhelper  A family $(f_i)_{i \in I}$ of FPSs in $K[\! [x ]\! ]_0$ is \emph{summable} if for each coefficient index $n$, only finitely many $[x^n](f_i)$ are nonzero. 

A family $(f_i)_{i \in I}$ of FPSs in $K[\! [x ]\! ]_1$ is \emph{multipliable} if for each coefficient index $n$, all but finitely many $f_i$ satisfy $[x^k](f_i - 1) = 0$ for all $1 \le k \le n$. 

For summable families, the coefficient-wise sum $\sum _{i \in I} f_i$ belongs to $K[\! [x ]\! ]_0$. For multipliable families, the product $\prod _{i \in I} f_i$ belongs to $K[\! [x ]\! ]_1$.

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
  "verdict": "faithful",
  "justification": "The binders `\u2200 {K} [CommRing K] [Algebra \u211a K] {I} (f : I \u2192 \u2191PowerSeries\u2081) (hf : MultipliableFPS\u2081 f)` match \u201cAssume that K is a commutative \u211a-algebra\u201d and a \u201cmultipliable family \u2026 in K[[x]]\u2081.\u201d The displayed equality exactly matches `Log(\u220f i, f_i) = \u2211 i, Log(f_i)`: `multipliableFPS\u2081Prod` is the coefficientwise infinite product specified by the blueprint, while `summableFPS\u2080Sum` is its coefficientwise essentially finite sum. The other two asserted clauses are encoded/available from the same hypothesis: `Log_summable_of_multipliable f hf` proves that `(Log (f i))` is summable, and `multipliableFPS\u2081Prod f hf` has type `PowerSeries\u2081`, encoding that the product belongs to `K[[x]]\u2081`. Although `hf_sum : optParam (SummableFPS\u2080 ...) \u22ef` appears as a binder, it is not a contentful added restriction: its proposition follows from `hf` by `Log_summable_of_multipliable`, and the optional default supplies that proof. Thus the target together with its stated dependencies implies every clause of the blueprint proposition."
}