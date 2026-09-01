## TARGET AlgebraicCombinatorics.FPS.Laurent.laurentSeries_eq_hsum_single (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] (x : LaurentSeries K), x = (AlgebraicCombinatorics.FPS.Laurent.singleFamily x).hsum

Docstring: **Every Laurent series is a sum of monomials**.
(Proposition prop.fps.laure.a=sumaixi, label: prop.fps.laure.a=sumaixi)

Any Laurent series `a` can be written as `∑_{i ∈ ℤ} aᵢ · xⁱ` where the sum
is taken over the support of `a`. This is the infinite sum version of `eq_sum_T`
for Laurent polynomials.

In Mathlib notation, we express this using `SummableFamily.hsum`, which represents
a formal infinite sum of Hahn series. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.FPS.Laurent.singleFamily (def)
{K : Type u_1} → [inst : CommRing K] → (x : LaurentSeries K) → HahnSeries.SummableFamily ℤ K ↑(HahnSeries.support x)

Body:
fun {K} [CommRing K] x =>
  {
    toFun := fun x_1 =>
      match x_1 with
      | ⟨g, property⟩ => (HahnSeries.single g) (x.coeff g),
    isPWO_iUnion_support' := ⋯, finite_co_support' := ⋯ }

Docstring: A summable family of single Hahn series indexed by the support of a given Laurent series.
This is used to express a Laurent series as an infinite sum of monomials. 

## BASE-LIBRARY REF CommRing
Type u → Type u

Docstring: A commutative ring is a ring with commutative multiplication. 

## BASE-LIBRARY REF LaurentSeries
(R : Type u) → [Zero R] → Type (max 0 u)

Docstring: `LaurentSeries R` is the type of formal Laurent series with coefficients in `R`, denoted `R⸨X⸩`.

It is implemented as a `HahnSeries` with value group `ℤ`.


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

## BASE-LIBRARY REF HahnSeries.SummableFamily.hsum
{Γ : Type u_1} →
  {R : Type u_3} →
    {α : Type u_5} →
      [inst : PartialOrder Γ] → [inst_1 : AddCommMonoid R] → HahnSeries.SummableFamily Γ R α → HahnSeries Γ R

Docstring: The infinite sum of a `SummableFamily` of Hahn series. 

## BASE-LIBRARY REF Int
Type

Docstring: The integers.

This type is special-cased by the compiler and overridden with an efficient implementation. The
runtime has a special representation for `Int` that stores “small” signed numbers directly, while
larger numbers use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)). A “small number” is an integer that can be encoded with one fewer bits
than the platform's pointer size (i.e. 63 bits on 64-bit architectures and 31 bits on 32-bit
architectures).


## BASE-LIBRARY REF Set.Elem
{α : Type u} → Set α → Type u

Docstring: Given the set `s`, `Elem s` is the `Type` of element of `s`.

It is currently an abbreviation so that instance coming from `Subtype` are available.
If you're interested in making it a `def`, as it probably should be,
you'll then need to create additional instances (and possibly prove lemmas about them).
See e.g. `Mathlib/Data/Set/Order.lean`.


## BASE-LIBRARY REF HahnSeries.support
{Γ : Type u_1} → {R : Type u_3} → [inst : PartialOrder Γ] → [inst_1 : Zero R] → HahnSeries Γ R → Set Γ

Docstring: The support of a Hahn series is just the set of indices whose coefficients are nonzero.
Notably, it is well-founded. 

## BASE-LIBRARY REF SemilatticeInf.toPartialOrder
{α : Type u} → [self : SemilatticeInf α] → PartialOrder α

## BASE-LIBRARY REF Lattice.toSemilatticeInf
{α : Type u} → [self : Lattice α] → SemilatticeInf α

## BASE-LIBRARY REF instLatticeInt
Lattice ℤ

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.toAddCommMonoid
{α : Type u} → [self : NonUnitalNonAssocSemiring α] → AddCommMonoid α

## BASE-LIBRARY REF HahnSeries.SummableFamily
(Γ : Type u_8) → (R : Type u_9) → [PartialOrder Γ] → [AddCommMonoid R] → Type u_7 → Type (max (max u_7 u_8) u_9)

Docstring: A family of Hahn series whose formal coefficient-wise sum is a Hahn series.  For each
coefficient of the sum to be well-defined, we require that only finitely many series are nonzero at
any given coefficient.  For the formal sum to be a Hahn series, we require that the union of the
supports of the constituent series is partially well-ordered. 

## BASE-LIBRARY REF HahnSeries.SummableFamily.mk
{Γ : Type u_8} →
  {R : Type u_9} →
    [inst : PartialOrder Γ] →
      [inst_1 : AddCommMonoid R] →
        {α : Type u_7} →
          (toFun : α → HahnSeries Γ R) →
            (⋃ a, (toFun a).support).IsPWO →
              (∀ (g : Γ), {a | (toFun a).coeff g ≠ 0}.Finite) → HahnSeries.SummableFamily Γ R α

## BASE-LIBRARY REF HahnSeries
(Γ : Type u_1) → (R : Type u_2) → [PartialOrder Γ] → [Zero R] → Type (max u_1 u_2)

Docstring: If `Γ` is linearly ordered and `R` has zero, then `R⟦Γ⟧` consists of
formal series over `Γ` with coefficients in `R`, whose supports are well-founded. 

## BASE-LIBRARY REF AddZero.toZero
{M : Type u_2} → [self : AddZero M] → Zero M

## BASE-LIBRARY REF AddZeroClass.toAddZero
{M : Type u} → [self : AddZeroClass M] → AddZero M

## BASE-LIBRARY REF AddMonoid.toAddZeroClass
{M : Type u} → [self : AddMonoid M] → AddZeroClass M

## BASE-LIBRARY REF AddCommMonoid.toAddMonoid
{M : Type u} → [self : AddCommMonoid M] → AddMonoid M

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

## BASE-LIBRARY REF DFunLike.coe
{F : Sort u_1} → {α : outParam (Sort u_2)} → {β : outParam (α → Sort u_3)} → [self : DFunLike F α β] → F → (a : α) → β a

Docstring: The coercion from `F` to a function. 

## BASE-LIBRARY REF ZeroHom
(M : Type u_10) → (N : Type u_11) → [Zero M] → [Zero N] → Type (max u_10 u_11)

Docstring: `ZeroHom M N` is the type of functions `M → N` that preserve zero.

When possible, instead of parametrizing results over `(f : ZeroHom M N)`,
you should parametrize over `(F : Type*) [ZeroHomClass F M N] (f : F)`.

When you extend this structure, make sure to also extend `ZeroHomClass`.


## BASE-LIBRARY REF HahnSeries.instZero
{Γ : Type u_1} → {R : Type u_3} → [inst : PartialOrder Γ] → [inst_1 : Zero R] → Zero (HahnSeries Γ R)

## BASE-LIBRARY REF ZeroHom.funLike
{M : Type u_4} → {N : Type u_5} → [inst : Zero M] → [inst_1 : Zero N] → FunLike (ZeroHom M N) M N

## BASE-LIBRARY REF HahnSeries.single
{Γ : Type u_1} → {R : Type u_3} → [inst : PartialOrder Γ] → [inst_1 : Zero R] → Γ → ZeroHom R (HahnSeries Γ R)

Docstring: `single a r` is the Hahn series which has coefficient `r` at `a` and zero otherwise. 

## BASE-LIBRARY REF HahnSeries.coeff
{Γ : Type u_1} → {R : Type u_2} → [inst : PartialOrder Γ] → [inst_1 : Zero R] → HahnSeries Γ R → Γ → R

Docstring: The coefficient function of a Hahn Series. 

## INFORMAL STATEMENT
Right-multiplication by T on Laurent series

\leanhelper  A Laurent series $f \in K((x))$ equals the summable-family sum of the monomials $f_n \cdot x^n$ (each being the family $(\delta _{m,n} \cdot f_n)_{m \in \mathbb {Z}}$). This constructs an explicit summable family whose sum recovers $f$.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The blueprint says that a Laurent series \u201cequals the summable-family sum of the monomials $f_n\\cdot x^n$,\u201d with each monomial represented by $(\\delta_{m,n}f_n)_{m\\in\\mathbb Z}$. The target asserts exactly `x = (AlgebraicCombinatorics.FPS.Laurent.singleFamily x).hsum`. By the body of `singleFamily`, its term at an index `g` in `HahnSeries.support x` is `(HahnSeries.single g) (x.coeff g)`, and `HahnSeries.single` is the series with coefficient `x.coeff g` at `g` and zero elsewhere, i.e. the stated monomial. Indexing the sum by the support merely omits zero monomials and still recovers the stated decomposition. The binder `[CommRing K]` supplies the coefficient setting needed for this construction; if the notation $K((x))$ was intended only for fields, the formal theorem is more general, not weaker."
}