## TARGET PowerSeries.PowerSeries₁.subgroup (def) — ELABORATED SIGNATURE
{R : Type u_2} → [inst : Field R] → Subgroup (PowerSeries R)ˣ

Body:
fun {R} [Field R] => { carrier := {u | ↑u ∈ PowerSeries.PowerSeries₁}, mul_mem' := ⋯, one_mem' := ⋯, inv_mem' := ⋯ }

Docstring: `R⟦X⟧₁` forms a multiplicative subgroup of units.
This is Proposition 7.8.10(b) (prop.fps.Exp-Log-groups). 

## TARGET PowerSeries.PowerSeries₀.addSubgroup (def) — ELABORATED SIGNATURE
{R : Type u_2} → [inst : CommRing R] → AddSubgroup (PowerSeries R)

Body:
fun {R} [CommRing R] => { carrier := PowerSeries.PowerSeries₀, add_mem' := ⋯, zero_mem' := ⋯, neg_mem' := ⋯ }

Docstring: `R⟦X⟧₀` forms an additive subgroup.
This is Proposition 7.8.10(a) (prop.fps.Exp-Log-groups). 

## PROJECT DEPENDENCY PowerSeries.PowerSeries₁ (def)
{R : Type u_2} → [CommRing R] → Set (PowerSeries R)

Body:
fun {R} [CommRing R] => {f | PowerSeries.constantCoeff f = 1}

Docstring: `R⟦X⟧₁` is the set of FPS with constant term 1.
This is Definition 7.8.6(b) (def.fps.Exp-Log-maps). 

## PROJECT DEPENDENCY PowerSeries.PowerSeries₀ (def)
{R : Type u_2} → [CommRing R] → Set (PowerSeries R)

Body:
fun {R} [CommRing R] => {f | PowerSeries.constantCoeff f = 0}

Docstring: `R⟦X⟧₀` is the set of FPS with constant term 0.
This is Definition 7.8.6(a) (def.fps.Exp-Log-maps). 

## PROJECT DEPENDENCY PowerSeries.PowerSeries₀.add_mem (theorem)
∀ {R : Type u_2} [inst : CommRing R] {f g : PowerSeries R},
  f ∈ PowerSeries.PowerSeries₀ → g ∈ PowerSeries.PowerSeries₀ → f + g ∈ PowerSeries.PowerSeries₀

## PROJECT DEPENDENCY PowerSeries.PowerSeries₀.zero_mem (theorem)
∀ {R : Type u_2} [inst : CommRing R], 0 ∈ PowerSeries.PowerSeries₀

Docstring: `R⟦X⟧₀` is closed under addition and subtraction and contains 0.
This is Proposition 7.8.10(a) (prop.fps.Exp-Log-groups). 

## PROJECT DEPENDENCY PowerSeries.PowerSeries₀.neg_mem (theorem)
∀ {R : Type u_2} [inst : CommRing R] {f : PowerSeries R}, f ∈ PowerSeries.PowerSeries₀ → -f ∈ PowerSeries.PowerSeries₀

## BASE-LIBRARY REF Field
Type u → Type u

Docstring: A `Field` is a `CommRing` with multiplicative inverses for nonzero elements.

An instance of `Field K` includes maps `ratCast : ℚ → K` and `qsmul : ℚ → K → K`.
Those two fields are needed to implement the `DivisionRing K → Algebra ℚ K` instance since we need
to control the specific definitions for some special cases of `K` (in particular `K = ℚ` itself).
See also note [forgetful inheritance].

If the field has positive characteristic `p`, our division by zero convention forces
`ratCast (1 / p) = 1 / 0 = 0`. 

## BASE-LIBRARY REF Subgroup
(G : Type u_3) → [Group G] → Type u_3

Docstring: A subgroup of a group `G` is a subset containing 1, closed under multiplication
and closed under multiplicative inverse. 

## BASE-LIBRARY REF Units
(α : Type u) → [Monoid α] → Type u

Docstring: Units of a `Monoid`, bundled version. Notation: `αˣ`.

An element of a `Monoid` is a unit if it has a two-sided inverse.
This version bundles the inverse element so that it can be computed.
For a predicate see `IsUnit`. 

## BASE-LIBRARY REF PowerSeries
Type u_1 → Type (max u_1 0)

Docstring: Formal power series over a coefficient type `R` 

## BASE-LIBRARY REF MonoidWithZero.toMonoid
{M₀ : Type u} → [self : MonoidWithZero M₀] → Monoid M₀

## BASE-LIBRARY REF Semiring.toMonoidWithZero
{α : Type u} → [self : Semiring α] → MonoidWithZero α

## BASE-LIBRARY REF PowerSeries.instSemiring
{R : Type u_1} → [Semiring R] → Semiring (PowerSeries R)

## BASE-LIBRARY REF DivisionSemiring.toSemiring
{K : Type u_2} → [self : DivisionSemiring K] → Semiring K

## BASE-LIBRARY REF Semifield.toDivisionSemiring
{K : Type u_2} → [self : Semifield K] → DivisionSemiring K

## BASE-LIBRARY REF Field.toSemifield
{K : Type u_1} → [Field K] → Semifield K

## BASE-LIBRARY REF Units.instGroup
{α : Type u} → [inst : Monoid α] → Group αˣ

Docstring: Units of a monoid form a group. 

## BASE-LIBRARY REF Subgroup.mk
{G : Type u_3} →
  [inst : Group G] →
    (toSubmonoid : Submonoid G) → (∀ {x : G}, x ∈ toSubmonoid.carrier → x⁻¹ ∈ toSubmonoid.carrier) → Subgroup G

## BASE-LIBRARY REF Submonoid.mk
{M : Type u_3} → [inst : MulOneClass M] → (toSubsemigroup : Subsemigroup M) → 1 ∈ toSubsemigroup.carrier → Submonoid M

## BASE-LIBRARY REF Monoid.toMulOneClass
{M : Type u} → [self : Monoid M] → MulOneClass M

## BASE-LIBRARY REF DivInvMonoid.toMonoid
{G : Type u} → [self : DivInvMonoid G] → Monoid G

## BASE-LIBRARY REF Group.toDivInvMonoid
{G : Type u} → [self : Group G] → DivInvMonoid G

## BASE-LIBRARY REF Subsemigroup.mk
{M : Type u_3} →
  [inst : Mul M] → (carrier : Set M) → (∀ {a b : M}, a ∈ carrier → b ∈ carrier → a * b ∈ carrier) → Subsemigroup M

## BASE-LIBRARY REF MulOne.toMul
{M : Type u_2} → [self : MulOne M] → Mul M

## BASE-LIBRARY REF MulOneClass.toMulOne
{M : Type u} → [self : MulOneClass M] → MulOne M

## BASE-LIBRARY REF setOf
{α : Type u} → (α → Prop) → Set α

Docstring: Turn a predicate `p : α → Prop` into a set, also written as `{x | p x}` 

## BASE-LIBRARY REF Membership.mem
{α : outParam (Type u)} → {γ : Type v} → [self : Membership α γ] → γ → α → Prop

Docstring: The membership relation `a ∈ s : Prop` where `a : α`, `s : γ`. 

Conventions for notations in identifiers:

 * The recommended spelling of `∈` in identifiers is `mem`.

## BASE-LIBRARY REF Set
Type u → Type u

Docstring: A set is a collection of elements of some type `α`.

Although `Set` is defined as `α → Prop`, this is an implementation detail which should not be
relied on. Instead, `setOf` and membership of a set (`∈`) should be used to convert between sets
and predicates.


## BASE-LIBRARY REF Set.instMembership
{α : Type u} → Membership α (Set α)

## BASE-LIBRARY REF EuclideanDomain.toCommRing
{R : Type u} → [self : EuclideanDomain R] → CommRing R

## BASE-LIBRARY REF Field.toEuclideanDomain
{K : Type u_1} → [Field K] → EuclideanDomain K

## BASE-LIBRARY REF Units.val
{α : Type u} → [inst : Monoid α] → αˣ → α

Docstring: The underlying value in the base `Monoid`. 

## BASE-LIBRARY REF CommRing
Type u → Type u

Docstring: A commutative ring is a ring with commutative multiplication. 

## BASE-LIBRARY REF AddSubgroup
(G : Type u_3) → [AddGroup G] → Type u_3

Docstring: An additive subgroup of an additive group `G` is a subset containing 0, closed
under addition and additive inverse. 

## BASE-LIBRARY REF PowerSeries.instAddGroup
{R : Type u_1} → [AddGroup R] → AddGroup (PowerSeries R)

## BASE-LIBRARY REF AddGroupWithOne.toAddGroup
{R : Type u} → [self : AddGroupWithOne R] → AddGroup R

## BASE-LIBRARY REF Ring.toAddGroupWithOne
{R : Type u} → [self : Ring R] → AddGroupWithOne R

## BASE-LIBRARY REF CommRing.toRing
{α : Type u} → [self : CommRing α] → Ring α

## BASE-LIBRARY REF AddSubgroup.mk
{G : Type u_3} →
  [inst : AddGroup G] →
    (toAddSubmonoid : AddSubmonoid G) →
      (∀ {x : G}, x ∈ toAddSubmonoid.carrier → -x ∈ toAddSubmonoid.carrier) → AddSubgroup G

## BASE-LIBRARY REF AddSubmonoid.mk
{M : Type u_3} →
  [inst : AddZeroClass M] → (toAddSubsemigroup : AddSubsemigroup M) → 0 ∈ toAddSubsemigroup.carrier → AddSubmonoid M

## BASE-LIBRARY REF AddMonoid.toAddZeroClass
{M : Type u} → [self : AddMonoid M] → AddZeroClass M

## BASE-LIBRARY REF SubNegMonoid.toAddMonoid
{G : Type u} → [self : SubNegMonoid G] → AddMonoid G

## BASE-LIBRARY REF AddGroup.toSubNegMonoid
{A : Type u} → [self : AddGroup A] → SubNegMonoid A

## BASE-LIBRARY REF AddSubsemigroup.mk
{M : Type u_3} →
  [inst : Add M] → (carrier : Set M) → (∀ {a b : M}, a ∈ carrier → b ∈ carrier → a + b ∈ carrier) → AddSubsemigroup M

## BASE-LIBRARY REF AddZero.toAdd
{M : Type u_2} → [self : AddZero M] → Add M

## BASE-LIBRARY REF AddZeroClass.toAddZero
{M : Type u} → [self : AddZeroClass M] → AddZero M

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

## BASE-LIBRARY REF CommSemiring.toSemiring
{R : Type u} → [self : CommSemiring R] → Semiring R

## BASE-LIBRARY REF CommRing.toCommSemiring
{α : Type u} → [s : CommRing α] → CommSemiring α

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

## BASE-LIBRARY REF PowerSeries.instZero
{R : Type u_1} → [Zero R] → Zero (PowerSeries R)

## BASE-LIBRARY REF Neg.neg
{α : Type u} → [self : Neg α] → α → α

Docstring: `-a` computes the negative or opposite of `a`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `-` in identifiers is `neg` (when used as a unary operator).

## BASE-LIBRARY REF NegZeroClass.toNeg
{G : Type u_2} → [self : NegZeroClass G] → Neg G

## BASE-LIBRARY REF SubNegZeroMonoid.toNegZeroClass
{G : Type u_2} → [self : SubNegZeroMonoid G] → NegZeroClass G

## BASE-LIBRARY REF SubtractionMonoid.toSubNegZeroMonoid
{α : Type u_1} → [SubtractionMonoid α] → SubNegZeroMonoid α

## BASE-LIBRARY REF SubtractionCommMonoid.toSubtractionMonoid
{G : Type u} → [self : SubtractionCommMonoid G] → SubtractionMonoid G

## BASE-LIBRARY REF AddCommGroup.toDivisionAddCommMonoid
{G : Type u_1} → [AddCommGroup G] → SubtractionCommMonoid G

## BASE-LIBRARY REF PowerSeries.instAddCommGroup
{R : Type u_1} → [AddCommGroup R] → AddCommGroup (PowerSeries R)

## BASE-LIBRARY REF LieRing.toAddCommGroup
{L : Type v} → [self : LieRing L] → AddCommGroup L

## BASE-LIBRARY REF LieRing.ofAssociativeRing
{A : Type v} → [Ring A] → LieRing A

Docstring: An associative ring gives rise to a Lie ring by taking the bracket to be the ring commutator. 

## INFORMAL STATEMENT
prop.fps.Exp-Log-groups

\textbf{(a)} The subset $K\left[\left[ x\right]\right]_{0}$ of $K\left[\left[x\right]\right]$ is closed under addition and subtraction and contains $0$, and thus forms a group $\left(K\left[\left[x\right]\right]_{0},+,0\right)$. \medskip 

\textbf{(b)} The subset $K\left[\left[x\right]\right]_{1}$ of $K\left[\left[x\right]\right]$ is closed under multiplication and division and contains $1$, and thus forms a group $\left(K\left[\left[ x\right]\right]_{1},\cdot ,1\right)$.

## VERDICT
{
  "verdict": "drift",
  "justification": "Part (a) is faithful and slightly more general than a field-only reading: the target has `{R : Type u_2} \u2192 [CommRing R] \u2192 AddSubgroup (PowerSeries R)`, with carrier exactly `PowerSeries.PowerSeries\u2080 = {f | constantCoeff f = 0}`. An `AddSubgroup` supplies containment of `0` and closure under addition and additive inverse, hence subtraction, matching \u201cclosed under addition and subtraction and contains 0.\u201d Part (b), however, adds the mathematically substantive binder `[Field R]`: `{R : Type u_2} \u2192 [Field R] \u2192 Subgroup (PowerSeries R)\u02e3`. The blueprint merely states the claim for `K[[x]]\u2081`, while the project definition `PowerSeries.PowerSeries\u2081` itself only requires `[CommRing R]`. In fact, series with constant coefficient `1` are units over a commutative ring, so requiring a field unnecessarily narrows the coefficient rings and makes the formal statement weaker. Encoding the multiplicative group as a `Subgroup (PowerSeries R)\u02e3` is otherwise appropriate: its carrier `{u | \u2191u \u2208 PowerSeries.PowerSeries\u2081}` expresses constant coefficient `1`, and subgroup closure gives multiplication and inverse/division. To make the combined formalization faithful, change the binder of `PowerSeries.PowerSeries\u2081.subgroup` from `[Field R]` to `[CommRing R]` (with the corresponding proof that every constant-term-1 series is a unit)."
}