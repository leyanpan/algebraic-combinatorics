## TARGET skewSchurPoly_zero (theorem) — ELABORATED SIGNATURE
∀ {N : ℕ} [inst : NeZero N] (lam : NPartition N), skewSchurPoly lam 0 = schurPoly lam

Docstring: When mu = 0, the skew Schur polynomial equals the regular Schur polynomial.
Remark \ref{rmk.sf.skew-0} in the source. 

## PROJECT DEPENDENCY NPartition (inductive)
ℕ → Type

Body:
NPartition.mk : {N : ℕ} → (parts : Fin N → ℕ) → Antitone parts → NPartition N

Docstring: An N-partition is a weakly decreasing N-tuple of nonnegative integers.
(Definition def.sf.Npar)

This is represented as a function `Fin N → ℕ` that is antitone
(i.e., `i ≤ j → parts j ≤ parts i`).

The field is named `antitone` to match Mathlib conventions. 

## PROJECT DEPENDENCY skewSchurPoly (def)
{N : ℕ} → [NeZero N] → NPartition N → NPartition N → MvPolynomial (Fin N) ℤ

Body:
fun {N} [NeZero N] lam mu => ∑ f ∈ ssytFillings lam mu, fillingMonomial f

Docstring: The skew Schur polynomial s_{λ/μ} is the sum of monomials x_T over all
semistandard skew tableaux of shape λ/μ.
Definition \ref{def.sf.skew-schur} in the source.

We define this as a sum over the finite set of valid SSYT fillings:
s_{λ/μ} = ∑_{T ∈ SSYT(λ/μ)} x_T

The definition proceeds by:
1. Representing tableaux as functions from the skew diagram to Fin N
2. Filtering for those satisfying the SSYT conditions (row-weak, column-strict)
3. Summing the associated monomials

## Relationship to Other Definitions

This project has two skew Schur polynomial definitions with different design tradeoffs:

| Definition | File | Input | Ring | Use case |
|------------|------|-------|------|----------|
| `skewSchurPoly` (this) | SchurBasics.lean | `NPartition N` | `ℤ` | Proofs using skew diagrams, symmetry |
| `AlgebraicCombinatorics.skewSchurPoly` | LittlewoodRichardson.lean | `Fin N → ℕ` | generic `R` | Littlewood-Richardson rule, generic rings |

**When to use which:**
- Use **this definition** when working with skew Young diagrams, SSYT fillings, or proving
  symmetry properties. It requires `[NeZero N]` and uses integer coefficients.
- Use **`AlgebraicCombinatorics.skewSchurPoly`** when you need a generic coefficient ring
  or when working with the Littlewood-Richardson rule. It takes unbundled `Fin N → ℕ`.

**Equivalence:** See `SSYTEquiv.lean` for the bridge between these definitions. 

## PROJECT DEPENDENCY NPartition.instZero (def)
{N : ℕ} → Zero (NPartition N)

Body:
fun {N} => { zero := NPartition.zero }

## PROJECT DEPENDENCY schurPoly (def)
{N : ℕ} → [NeZero N] → NPartition N → MvPolynomial (Fin N) ℤ

Body:
fun {N} [NeZero N] lam => ∑ f ∈ ssytFillingsYoung lam, fillingMonomialYoung f

Docstring: The Schur polynomial s_λ is the sum of monomials x_T over all SSYT of shape λ.
Definition \ref{def.sf.schur} in the source.

We define this as a sum over the finite set of valid SSYT fillings:
s_λ = ∑_{T ∈ SSYT(λ)} x_T

The definition proceeds by:
1. Representing tableaux as functions from the Young diagram to Fin N
2. Filtering for those satisfying the SSYT conditions (row-weak, column-strict)
3. Summing the associated monomials

This is equivalent to `skewSchurPoly lam 0` since `skewYoungDiagram lam 0 = lam.youngDiagram`.

## Relationship to Other Definitions

This project has two Schur polynomial definitions with different design tradeoffs:

| Definition | File | Input | Ring | Use case |
|------------|------|-------|------|----------|
| `schurPoly` (this) | SchurBasics.lean | `NPartition N` | `ℤ` | Proofs using Young diagrams, symmetry |
| `AlgebraicCombinatorics.schurPoly` | LittlewoodRichardson.lean | `Fin N → ℕ` | generic `R` | Littlewood-Richardson rule, generic rings |

**When to use which:**
- Use **this definition** when working with Young diagrams, SSYT fillings, or proving
  symmetry properties. It requires `[NeZero N]` and uses integer coefficients.
- Use **`AlgebraicCombinatorics.schurPoly`** when you need a generic coefficient ring
  or when working with the Littlewood-Richardson rule. It takes unbundled `Fin N → ℕ`.

**Equivalence:** The two definitions agree when the partition is valid. See:
- `SSYTEquiv.schurPoly_eq_schur`: relates this definition to `SymmetricFunctions.schur`
- `schurPoly_eq_AC_schurPoly`: relates this definition to `AlgebraicCombinatorics.schurPoly` 

## PROJECT DEPENDENCY SkewFilling (def)
{N : ℕ} → [NeZero N] → NPartition N → NPartition N → Type

Body:
fun {N} [NeZero N] lam mu => { c // c ∈ skewYoungDiagram lam mu } → Fin N

Docstring: The type of all fillings of a skew diagram with entries in Fin N.
This is finite since the diagram is finite and Fin N is finite. 

## PROJECT DEPENDENCY ssytFillings (def)
{N : ℕ} → [inst : NeZero N] → (lam mu : NPartition N) → Finset (SkewFilling lam mu)

Body:
fun {N} [NeZero N] lam mu => Finset.filter (isSSYTFilling lam mu) Finset.univ

Docstring: The finite set of all valid SSYT fillings. 

## PROJECT DEPENDENCY fillingMonomial (def)
{N : ℕ} → [inst : NeZero N] → {lam mu : NPartition N} → SkewFilling lam mu → MvPolynomial (Fin N) ℤ

Body:
fun {N} [NeZero N] {lam mu} f => ∏ c, MvPolynomial.X (f c)

Docstring: The monomial associated to a filling.
x_f = ∏_{c ∈ Y(λ/μ)} x_{f(c)} 

## PROJECT DEPENDENCY NPartition.zero (def)
{N : ℕ} → NPartition N

Body:
fun {N} => { parts := fun x => 0, antitone := ⋯ }

Docstring: The zero N-partition (0, 0, ..., 0) 

## PROJECT DEPENDENCY Filling (def)
{N : ℕ} → [NeZero N] → NPartition N → Type

Body:
fun {N} [NeZero N] lam => { c // c ∈ lam.youngDiagram } → Fin N

Docstring: The type of all fillings of a Young diagram with entries in Fin N.
This is finite since the diagram is finite and Fin N is finite. 

## PROJECT DEPENDENCY ssytFillingsYoung (def)
{N : ℕ} → [inst : NeZero N] → (lam : NPartition N) → Finset (Filling lam)

Body:
fun {N} [NeZero N] lam => Finset.filter (isSSYTFillingYoung lam) Finset.univ

Docstring: The finite set of all valid SSYT fillings of a Young diagram. 

## PROJECT DEPENDENCY fillingMonomialYoung (def)
{N : ℕ} → [inst : NeZero N] → {lam : NPartition N} → Filling lam → MvPolynomial (Fin N) ℤ

Body:
fun {N} [NeZero N] {lam} f => ∏ c, MvPolynomial.X (f c)

Docstring: The monomial associated to a filling of a Young diagram.
x_f = ∏_{c ∈ Y(λ)} x_{f(c)} 

## PROJECT DEPENDENCY skewYoungDiagram (def)
{N : ℕ} → [NeZero N] → NPartition N → NPartition N → Finset (Fin N × ℕ)

Body:
fun {N} [NeZero N] lam mu => lam.youngDiagram \ mu.youngDiagram

Docstring: The skew Young diagram Y(λ/μ) is the set difference Y(λ) \ Y(μ).
Definition \ref{def.sf.skew-diag} in the source.

**Note**: This is a duplicate of `NPartition.skewYoungDiagram` that requires `[NeZero N]`.
Prefer `NPartition.skewYoungDiagram` for new code as it works for all `N`.

For N-partitions λ and μ with μ ⊆ λ, the skew Young diagram Y(λ/μ) is defined as:
```
Y(λ) \ Y(μ) = {(i,j) | i ∈ [N] and j ∈ [λ_i] \ [μ_i]}
            = {(i,j) | i ∈ [N] and j ∈ ℤ and μ_i < j ≤ λ_i}
```
(The second form uses 1-indexed j as in the textbook.)

In our 0-indexed formalization, this becomes:
```
Y(λ/μ) = {(i,j) | i ∈ Fin N and μ_i ≤ j < λ_i}
```

Example: Y((4,3,1)/(2,1,0)) consists of cells:
- Row 0: (0, 2), (0, 3)  (since μ₀ = 2, λ₀ = 4)
- Row 1: (1, 1), (1, 2)  (since μ₁ = 1, λ₁ = 3)
- Row 2: (2, 0)          (since μ₂ = 0, λ₂ = 1) 

## PROJECT DEPENDENCY isSSYTFilling (def)
{N : ℕ} → [inst : NeZero N] → (lam mu : NPartition N) → SkewFilling lam mu → Prop

Body:
fun {N} [NeZero N] lam mu f =>
  (∀ (c1 c2 : { c // c ∈ skewYoungDiagram lam mu }), (↑c1).1 = (↑c2).1 → (↑c1).2 < (↑c2).2 → f c1 ≤ f c2) ∧
    ∀ (c1 c2 : { c // c ∈ skewYoungDiagram lam mu }), (↑c1).2 = (↑c2).2 → (↑c1).1 < (↑c2).1 → f c1 < f c2

Docstring: The set of fillings that correspond to valid semistandard tableaux.
We check the conditions on pairs of cells in the diagram:
- Row-weak: if c1 and c2 are in the same row with c1 to the left, then f(c1) ≤ f(c2)
- Column-strict: if c1 and c2 are in the same column with c1 above, then f(c1) < f(c2) 

## PROJECT DEPENDENCY isSSYTFilling_decidable (def)
{N : ℕ} → [inst : NeZero N] → (lam mu : NPartition N) → (f : SkewFilling lam mu) → Decidable (isSSYTFilling lam mu f)

Body:
fun {N} [NeZero N] lam mu f => id inferInstance

Docstring: The SSYT condition is decidable since we're quantifying over finite types. 

## PROJECT DEPENDENCY skewFilling_fintype (def)
{N : ℕ} → [inst : NeZero N] → (lam mu : NPartition N) → Fintype (SkewFilling lam mu)

Body:
fun {N} [NeZero N] lam mu => Fintype.ofFinite (SkewFilling lam mu)

Docstring: Fillings are finite. 

## PROJECT DEPENDENCY NPartition.mk (constructor)
{N : ℕ} → (parts : Fin N → ℕ) → Antitone parts → NPartition N

## PROJECT DEPENDENCY NPartition.youngDiagram (def)
{N : ℕ} → NPartition N → Finset (Fin N × ℕ)

Body:
fun {N} μ => Finset.univ.biUnion fun i => Finset.map { toFun := fun j => (i, j), inj' := ⋯ } (Finset.range (μ.parts i))

Docstring: The Young diagram Y(λ) of an N-partition λ is the set of cells (i, j) where
i ∈ Fin N and j < λ_i.
Definition def.sf.ydiag in the source.

Note: Mathlib has `YoungDiagram` which is more general (infinite diagrams).
Here we define a version specific to N-partitions. 

## PROJECT DEPENDENCY isSSYTFillingYoung (def)
{N : ℕ} → [inst : NeZero N] → (lam : NPartition N) → Filling lam → Prop

Body:
fun {N} [NeZero N] lam f =>
  (∀ (c1 c2 : { c // c ∈ lam.youngDiagram }), (↑c1).1 = (↑c2).1 → (↑c1).2 < (↑c2).2 → f c1 ≤ f c2) ∧
    ∀ (c1 c2 : { c // c ∈ lam.youngDiagram }), (↑c1).2 = (↑c2).2 → (↑c1).1 < (↑c2).1 → f c1 < f c2

Docstring: The set of fillings that correspond to valid semistandard tableaux.
We check the conditions on pairs of cells in the diagram:
- Row-weak: if c1 and c2 are in the same row with c1 to the left, then f(c1) ≤ f(c2)
- Column-strict: if c1 and c2 are in the same column with c1 above, then f(c1) < f(c2) 

## PROJECT DEPENDENCY isSSYTFillingYoung_decidable (def)
{N : ℕ} → [inst : NeZero N] → (lam : NPartition N) → (f : Filling lam) → Decidable (isSSYTFillingYoung lam f)

Body:
fun {N} [NeZero N] lam f => id inferInstance

Docstring: The SSYT condition is decidable since we're quantifying over finite types. 

## PROJECT DEPENDENCY filling_fintype (def)
{N : ℕ} → [inst : NeZero N] → (lam : NPartition N) → Fintype (Filling lam)

Body:
fun {N} [NeZero N] lam => Fintype.ofFinite (Filling lam)

Docstring: Fillings are finite. 

## PROJECT DEPENDENCY NPartition.parts (def)
{N : ℕ} → NPartition N → Fin N → ℕ

Body:
fun N self => self.1

Docstring: The entries of the N-partition as a function from `Fin N` to `ℕ` 

## BASE-LIBRARY REF NeZero
{R : Type u_1} → [Zero R] → R → Prop

Docstring: A type-class version of `n ≠ 0`.  

## BASE-LIBRARY REF MulZeroClass
Type u → Type u

Docstring: Typeclass for expressing that a type `M₀` with multiplication and a zero satisfies
`0 * a = 0` and `a * 0 = 0` for all `a : M₀`. 

## BASE-LIBRARY REF Nat.instMulZeroClass
MulZeroClass ℕ

Body:
{ toMul := instMulNat, toZero := Nat.instAddMonoid.toAddZeroClass.toZero, zero_mul := Nat.zero_mul,
  mul_zero := Nat.mul_zero }

## BASE-LIBRARY REF Nat.instAddMonoid
AddMonoid ℕ

Body:
inferInstance

## BASE-LIBRARY REF Nat.zero_mul
∀ (n : ℕ), 0 * n = 0

## BASE-LIBRARY REF Nat.mul_zero
∀ (n : ℕ), n * 0 = 0

## BASE-LIBRARY REF MvPolynomial
Type u_1 → (R : Type u_2) → [CommSemiring R] → Type (max u_2 u_1)

Body:
fun σ R [CommSemiring R] => AddMonoidAlgebra R (σ →₀ ℕ)

Docstring: Multivariate polynomial, where `σ` is the index set of the variables and
`R` is the coefficient ring 

## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


## BASE-LIBRARY REF Int.instCommSemiring
CommSemiring ℤ

Body:
inferInstance

## BASE-LIBRARY REF CommSemiring
Type u → Type u

Docstring: A commutative semiring is a semiring with commutative multiplication. 

## BASE-LIBRARY REF Int.instCommRing
CommRing ℤ

Body:
let __spread.0 := Int.instAddCommGroup;
let __spread.1 := Int.instCommSemigroup;
{ toAddMonoid := __spread.0.toAddMonoid, add_comm := ⋯, toMul := __spread.1.toMul, left_distrib := Int.mul_add,
  right_distrib := Int.add_mul, zero_mul := Int.zero_mul, mul_zero := Int.mul_zero,
  mul_assoc := Int.instCommRing._proof_3, toOne := Int.instMonoid.toMulOneClass.toOne, one_mul := Int.one_mul,
  mul_one := Int.mul_one, natCast := fun x => ↑x, natCast_zero := Int.instCommRing._proof_4,
  natCast_succ := Int.instCommRing._proof_5, npow := fun n x => x ^ n, npow_zero := ⋯, npow_succ := ⋯,
  toNeg := __spr …

## BASE-LIBRARY REF Zero
Type u → Type u

Docstring: A type with a zero element. 

## BASE-LIBRARY REF Zero.zero
{α : Type u} → [self : Zero α] → α

Body:
fun α [self : Zero α] => self.1

Docstring: The zero element of the type. 

## BASE-LIBRARY REF Antitone
{α : Type u} → {β : Type v} → [Preorder α] → [Preorder β] → (α → β) → Prop

Body:
fun {α} {β} [Preorder α] [Preorder β] f => ∀ ⦃a b : α⦄, a ≤ b → f b ≤ f a

Docstring: A function `f` is antitone if `a ≤ b` implies `f b ≤ f a`. 

## BASE-LIBRARY REF PartialOrder
Type u_2 → Type u_2

Docstring: A partial order is a reflexive, transitive, antisymmetric relation `≤`. 

## BASE-LIBRARY REF Fin.instPartialOrder
{n : ℕ} → PartialOrder (Fin n)

Body:
fun {n} => inferInstance

## BASE-LIBRARY REF Fin.instLinearOrder
{n : ℕ} → LinearOrder (Fin n)

Body:
fun {n} => Function.Injective.linearOrder Fin.val ⋯ ⋯ ⋯ ⋯ ⋯ ⋯

## BASE-LIBRARY REF Nat.instPreorder
Preorder ℕ

Body:
inferInstance

## BASE-LIBRARY REF Preorder
Type u_2 → Type u_2

Docstring: A preorder is a reflexive, transitive relation `≤`.
In a preorder, `a < b` means `a ≤ b ∧ ¬b ≤ a`, and `<` is defined this way by default.
You can override this definition to set a better def-eq.


## BASE-LIBRARY REF Nat.instLinearOrder
LinearOrder ℕ

Body:
{ le := Nat.le, lt := Nat.lt, le_refl := Nat.le_refl, le_trans := @Nat.le_trans,
  lt_iff_le_not_ge := @Nat.lt_iff_le_not_le, le_antisymm := @Nat.le_antisymm, toMin := instMinNat, toMax := Nat.instMax,
  toOrd := instOrdNat, le_total := Nat.le_total, toDecidableLE := inferInstance, toDecidableEq := inferInstance,
  toDecidableLT := inferInstance, min_def := Nat.instLinearOrder._proof_1, max_def := Nat.instLinearOrder._proof_2,
  compare_eq_compareOfLessAndEq := Nat.instLinearOrder._proof_3 }

## BASE-LIBRARY REF Finset.sum
{ι : Type u_1} → {M : Type u_3} → [AddCommMonoid M] → Finset ι → (ι → M) → M

Body:
fun {ι} {M} [AddCommMonoid M] s f => (Multiset.map f s.val).sum

Docstring: `∑ x ∈ s, f x` is the sum of `f x` as `x` ranges over the elements
of the finite set `s`.

When the index type is a `Fintype`, the notation `∑ x, f x`, is a shorthand for
`∑ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF NonUnitalNonAssocSemiring
Type u → Type u

Docstring: A not-necessarily-unital, not-necessarily-associative semiring. See `CommutatorRing` and the
documentation thereof in case you need a `NonUnitalNonAssocSemiring` instance on a Lie ring
or a Lie algebra. 

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

## BASE-LIBRARY REF CommRing
Type u → Type u

Docstring: A commutative ring is a ring with commutative multiplication. 

## BASE-LIBRARY REF MvPolynomial.instCommRingMvPolynomial
{R : Type u} → {σ : Type u_1} → [inst : CommRing R] → CommRing (MvPolynomial σ R)

Body:
fun {R} {σ} [CommRing R] => AddMonoidAlgebra.commRing

## BASE-LIBRARY REF AddMonoidAlgebra.commRing
{R : Type u_1} → {M : Type u_4} → [inst : CommRing R] → [AddCommMonoid M] → CommRing (AddMonoidAlgebra R M)

Body:
fun {R} {M} [CommRing R] [AddCommMonoid M] => { toRing := AddMonoidAlgebra.ring, mul_comm := ⋯ }

## BASE-LIBRARY REF Finsupp
Type u_9 → (M : Type u_10) → [Zero M] → Type (max u_10 u_9)

Docstring: `Finsupp α M`, denoted `α →₀ M`, is the type of functions `f : α → M` such that
`f x = 0` for all but finitely many `x`. 

## BASE-LIBRARY REF Finsupp.instAddCommMonoid
{ι : Type u_1} → {M : Type u_3} → [inst : AddCommMonoid M] → AddCommMonoid (ι →₀ M)

Body:
fun {ι} {M} [AddCommMonoid M] => { toAddMonoid := Finsupp.instAddMonoid, add_comm := ⋯ }

## BASE-LIBRARY REF Nat.instAddCommMonoid
AddCommMonoid ℕ

Body:
inferInstance

## BASE-LIBRARY REF Prod
Type u → Type v → Type (max u v)

Docstring: The product type, usually written `α × β`. Product types are also called pair or tuple types.
Elements of this type are pairs in which the first element is an `α` and the second element is a
`β`.

Products nest to the right, so `(x, y, z) : α × β × γ` is equivalent to `(x, (y, z)) : α × (β × γ)`.


Conventions for notations in identifiers:

 * The recommended spelling of `×` in identifiers is `Prod`.

## BASE-LIBRARY REF Finset
Type u_4 → Type u_4

Docstring: `Finset α` is the type of finite sets of elements of `α`. It is implemented
as a multiset (a list up to permutation) which has no duplicate elements. 

## BASE-LIBRARY REF Multiset
Type u → Type u

Body:
fun α => Quotient (List.isSetoid α)

Docstring: `Multiset α` is the quotient of `List α` by list permutation. The result
is a type of finite sets with duplicates allowed. 

## BASE-LIBRARY REF Finset.val
{α : Type u_4} → Finset α → Multiset α

Body:
fun α self => self.1

Docstring: The underlying multiset 

## BASE-LIBRARY REF Finset.filter
{α : Type u_1} → (p : α → Prop) → [DecidablePred p] → Finset α → Finset α

Body:
fun {α} p [DecidablePred p] s => { val := Multiset.filter p s.val, nodup := ⋯ }

Docstring: `Finset.filter p s` is the set of elements of `s` that satisfy `p`.

For example, one can use `s.filter (· ∈ t)` to get the intersection of `s` with `t : Set α`
as a `Finset α` (when a `DecidablePred (· ∈ t)` instance is available). 

## BASE-LIBRARY REF Finset.univ
{α : Type u_1} → [Fintype α] → Finset α

Body:
fun {α} [Fintype α] => Fintype.elems

Docstring: `univ` is the universal finite set of type `Finset α` implied from
the assumption `Fintype α`. 

## BASE-LIBRARY REF Finset.prod
{ι : Type u_1} → {M : Type u_3} → [CommMonoid M] → Finset ι → (ι → M) → M

Body:
fun {ι} {M} [CommMonoid M] s f => (Multiset.map f s.val).prod

Docstring: `∏ x ∈ s, f x` is the product of `f x` as `x` ranges over the elements of the finite set `s`.

When the index type is a `Fintype`, the notation `∏ x, f x`, is a shorthand for
`∏ x ∈ Finset.univ, f x`. 

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

## BASE-LIBRARY REF Finset.Subtype.fintype
{α : Type u_1} → (s : Finset α) → Fintype { x // x ∈ s }

Body:
fun {α} s => { elems := s.attach, complete := ⋯ }

## BASE-LIBRARY REF Finset.attach
{α : Type u_1} → (s : Finset α) → Finset { x // x ∈ s }

Body:
fun {α} s => { val := s.val.attach, nodup := ⋯ }

Docstring: `attach s` takes the elements of `s` and forms a new set of elements of the subtype
`{x // x ∈ s}`. 

## BASE-LIBRARY REF Finset.mem_attach
∀ {α : Type u_1} (s : Finset α) (x : { x // x ∈ s }), x ∈ s.attach

## BASE-LIBRARY REF MvPolynomial.X
{R : Type u} → {σ : Type u_1} → [inst : CommSemiring R] → σ → MvPolynomial σ R

Body:
fun {R} {σ} [CommSemiring R] n => (MvPolynomial.monomial fun₀ | n => 1) 1

Docstring: `X n` is the degree `1` monomial $X_n$. 

## BASE-LIBRARY REF SDiff.sdiff
{α : Type u} → [self : SDiff α] → α → α → α

Body:
fun α [self : SDiff α] => self.1

Docstring: `a \ b` is the set difference of `a` and `b`,
consisting of all elements in `a` that are not in `b`.


Conventions for notations in identifiers:

 * The recommended spelling of `\` in identifiers is `sdiff`.

## BASE-LIBRARY REF Finset.instSDiff
{α : Type u_1} → [DecidableEq α] → SDiff (Finset α)

Body:
fun {α} [DecidableEq α] => { sdiff := fun s₁ s₂ => { val := s₁.val - s₂.val, nodup := ⋯ } }

Docstring: `s \ t` is the set consisting of the elements of `s` that are not in `t`. 

## BASE-LIBRARY REF instDecidableEqProd.match_3
{α : Type u_1} →
  {β : Type u_2} → (motive : α × β → Sort u_3) → (x : α × β) → ((a' : α) → (b' : β) → motive (a', b')) → motive x

Body:
fun {α} {β} motive x h_1 => Prod.casesOn x fun fst snd => h_1 fst snd

## BASE-LIBRARY REF instDecidableEqProd.match_1
{β : Type u_1} →
  (b b' : β) →
    (motive : Decidable (b = b') → Sort u_2) →
      (x : Decidable (b = b')) →
        ((e₂ : b = b') → motive (isTrue e₂)) → ((n₂ : ¬b = b') → motive (isFalse n₂)) → motive x

Body:
fun {β} b b' motive x h_1 h_2 => Decidable.casesOn x (fun h => h_2 h) fun h => h_1 h

## BASE-LIBRARY REF decEq
{α : Sort u} → [inst : DecidableEq α] → (a b : α) → Decidable (a = b)

Body:
fun {α} [inst : DecidableEq α] a b => inst a b

Docstring: Checks whether two terms of a type are equal using the type's `DecidableEq` instance.


## BASE-LIBRARY REF Decidable.isTrue
{p : Prop} → p → Decidable p

Docstring: Proves that `p` is decidable by supplying a proof of `p` 

## BASE-LIBRARY REF instDecidableEqProd._proof_1
∀ {α : Type u_2} {β : Type u_1} (a : α) (b : β) (a' : α) (b' : β), a = a' → b = b' → (a, b) = (a', b')

## BASE-LIBRARY REF Decidable.isFalse
{p : Prop} → ¬p → Decidable p

Docstring: Proves that `p` is decidable by supplying a proof of `¬p` 

## BASE-LIBRARY REF instDecidableEqProd._proof_2
∀ {α : Type u_2} {β : Type u_1} (a : α) (b : β) (a' : α) (b' : β), ¬b = b' → (a, b) = (a', b') → False

## BASE-LIBRARY REF instDecidableEqProd._proof_3
∀ {α : Type u_2} {β : Type u_1} (a : α) (b : β) (a' : α) (b' : β), ¬a = a' → (a, b) = (a', b') → False

## BASE-LIBRARY REF instDecidableEqFin.match_1
(n : ℕ) →
  (i j : Fin n) →
    (motive : Decidable (↑i = ↑j) → Sort u_1) →
      (x : Decidable (↑i = ↑j)) → ((h : ↑i = ↑j) → motive (isTrue h)) → ((h : ¬↑i = ↑j) → motive (isFalse h)) → motive x

Body:
fun n i j motive x h_1 h_2 => Decidable.casesOn x (fun h => h_2 h) fun h => h_1 h

## BASE-LIBRARY REF Fin.val
{n : ℕ} → Fin n → ℕ

Body:
fun n self => self.1

Docstring: The number that is strictly less than `n`.

`Fin.val` is a coercion, so any `Fin n` can be used in a position where a `Nat` is expected.


## BASE-LIBRARY REF Fin.eq_of_val_eq
∀ {n : ℕ} {i j : Fin n}, ↑i = ↑j → i = j

## BASE-LIBRARY REF instDecidableEqFin._proof_1
∀ (n : ℕ) (i j : Fin n), ¬↑i = ↑j → i = j → False

## BASE-LIBRARY REF Prod.fst
{α : Type u} → {β : Type v} → α × β → α

Body:
fun α β self => self.1

Docstring: The first element of a pair. 

## BASE-LIBRARY REF Nat.lt
ℕ → ℕ → Prop

Body:
fun n m => n.succ.le m

Docstring: Strict inequality of natural numbers, usually accessed via the `<` operator.

It is defined as `n < m = n + 1 ≤ m`.


## BASE-LIBRARY REF Prod.snd
{α : Type u} → {β : Type v} → α × β → β

Body:
fun α β self => self.2

Docstring: The second element of a pair. 

## BASE-LIBRARY REF instDecidableAnd.match_1
{q : Prop} →
  (motive : Decidable q → Sort u_1) →
    (dq : Decidable q) → ((hq : q) → motive (isTrue hq)) → ((hq : ¬q) → motive (isFalse hq)) → motive dq

Body:
fun {q} motive dq h_1 h_2 => Decidable.casesOn dq (fun h => h_2 h) fun h => h_1 h

## BASE-LIBRARY REF And.intro
∀ {a b : Prop}, a → b → a ∧ b

Docstring: `And.intro : a → b → a ∧ b` is the constructor for the And operation. 

## BASE-LIBRARY REF instDecidableAnd._proof_1
∀ {p q : Prop}, ¬q → p ∧ q → False

## BASE-LIBRARY REF instDecidableAnd._proof_2
∀ {p q : Prop}, ¬p → p ∧ q → False

## BASE-LIBRARY REF Fintype.decidableForallFintype
{α : Type u_1} → {p : α → Prop} → [DecidablePred p] → [Fintype α] → Decidable (∀ (a : α), p a)

Body:
fun {α} {p} [DecidablePred p] [Fintype α] => decidable_of_iff (∀ a ∈ Finset.univ, p a) ⋯

## BASE-LIBRARY REF Fintype
Type u_4 → Type u_4

Docstring: `Fintype α` means that `α` is finite, i.e. there are only
finitely many distinct elements of type `α`. The evidence of this
is a finset `elems` (a list up to permutation without duplicates),
together with a proof that everything of type `α` is in the list. 

## BASE-LIBRARY REF decidable_of_iff
{b : Prop} → (a : Prop) → (a ↔ b) → [Decidable a] → Decidable b

Body:
fun {b} a h [Decidable a] => decidable_of_decidable_of_iff h

Docstring: Transfer decidability of `a` to decidability of `b`, if the propositions are equivalent.
**Important**: this function should be used instead of `rw` on `Decidable b`, because the
kernel will get stuck reducing the usage of `propext` otherwise,
and `decide` will not work. 

## BASE-LIBRARY REF Fintype.decidableForallFintype._proof_1
∀ {α : Type u_1} {p : α → Prop} [inst : Fintype α], (∀ a ∈ Finset.univ, p a) ↔ ∀ (a : α), p a

## BASE-LIBRARY REF Finset.decidableDforallFinset
{α : Type u_1} →
  {s : Finset α} →
    {p : (a : α) → a ∈ s → Prop} →
      [_hp : (a : α) → (h : a ∈ s) → Decidable (p a h)] → Decidable (∀ (a : α) (h : a ∈ s), p a h)

Body:
fun {α} {s} {p} [(a : α) → (h : a ∈ s) → Decidable (p a h)] => Multiset.decidableDforallMultiset

## BASE-LIBRARY REF forall_prop_decidable
{p : Prop} → (P : p → Prop) → [Decidable p] → [(h : p) → Decidable (P h)] → Decidable (∀ (h : p), P h)

Body:
fun {p} P [Decidable p] [(h : p) → Decidable (P h)] => if h : p then decidable_of_decidable_of_iff ⋯ else isTrue ⋯

## BASE-LIBRARY REF dite
{α : Sort u} → (c : Prop) → [h : Decidable c] → (c → α) → (¬c → α) → α

Body:
fun {α} c [h : Decidable c] t e => Decidable.casesOn h e t

Docstring: "Dependent" if-then-else, normally written via the notation `if h : c then t(h) else e(h)`,
is sugar for `dite c (fun h => t(h)) (fun h => e(h))`, and it is the same as
`if c then t else e` except that `t` is allowed to depend on a proof `h : c`,
and `e` can depend on `h : ¬c`. (Both branches use the same name for the hypothesis,
even though it has different types in the two cases.)

We use this to be able to communicate the if-then-else condition to the branches.
For example, `Array.get arr i h` expects a proof `h : i < arr.size` in order to
avoid a bounds check, so you can write `if h : i < arr.size then arr.get i h else ...`
to avoid the bounds check inside the if branch. (Of course in this case we have only
lifted the check into an explicit `if`, but we could also use this proof multiple times
or derive `i < arr.size` from some other proposition that we are checking in the `if`.)


## BASE-LIBRARY REF decidable_of_decidable_of_iff
{p q : Prop} → [Decidable p] → (p ↔ q) → Decidable q

Body:
fun {p q} [Decidable p] h => if hp : p then isTrue ⋯ else isFalse ⋯

Docstring: Transfer a decidability proof across an equivalence of propositions. 

## BASE-LIBRARY REF forall_prop_decidable._proof_1
∀ {p : Prop} (P : p → Prop) (h : p), P h ↔ ∀ (h : p), P h

## BASE-LIBRARY REF forall_prop_decidable._proof_2
∀ {p : Prop} (P : p → Prop), ¬p → ∀ (h2 : p), P h2

## BASE-LIBRARY REF Nat.decLt
(n m : ℕ) → Decidable (n < m)

Body:
fun n m => n.succ.decLe m

Docstring: A decision procedure for strict inequality of natural numbers, usually accessed via the
`DecidableLT Nat` instance.

Examples:
 * `(if 3 < 4 then "yes" else "no") = "yes"`
 * `(if 4 < 4 then "yes" else "no") = "no"`
 * `(if 6 < 4 then "yes" else "no") = "no"`
 * `show 5 < 12 by decide`


## BASE-LIBRARY REF Fin.decLe
{n : ℕ} → (a b : Fin n) → Decidable (a ≤ b)

Body:
fun {n} a b => (↑a).decLe ↑b

## BASE-LIBRARY REF Nat.decLe
(n m : ℕ) → Decidable (n ≤ m)

Body:
fun n m => if h : n.ble m = true then isTrue ⋯ else isFalse ⋯

Docstring: A decision procedure for non-strict inequality of natural numbers, usually accessed via the
`DecidableLE Nat` instance.

Examples:
 * `(if 3 ≤ 4 then "yes" else "no") = "yes"`
 * `(if 6 ≤ 4 then "yes" else "no") = "no"`
 * `show 12 ≤ 12 by decide`
 * `show 5 ≤ 12 by decide`


## BASE-LIBRARY REF Fin.decLt
{n : ℕ} → (a b : Fin n) → Decidable (a < b)

Body:
fun {n} a b => (↑a).decLt ↑b

## BASE-LIBRARY REF Fintype.ofFinite
(α : Type u_4) → [Finite α] → Fintype α

Body:
fun α [Finite α] => ⋯.some

Docstring: Noncomputably get a `Fintype` instance from a `Finite` instance. This is not an
instance because we want `Fintype` instances to be useful for computations. 

## BASE-LIBRARY REF Finset.biUnion
{α : Type u_1} → {β : Type u_2} → [DecidableEq β] → Finset α → (α → Finset β) → Finset β

Body:
fun {α} {β} [DecidableEq β] s t => (s.val.bind fun a => (t a).val).toFinset

Docstring: `Finset.biUnion s t` is the union of `t a` over `a ∈ s`.

(This was formerly `bind` due to the monad structure on types with `DecidableEq`.) 

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

## BASE-LIBRARY REF Finset.map
{α : Type u_1} → {β : Type u_2} → (α ↪ β) → Finset α → Finset β

Body:
fun {α} {β} f s => { val := Multiset.map (⇑f) s.val, nodup := ⋯ }

Docstring: When `f` is an embedding of `α` in `β` and `s` is a finset in `α`, then `s.map f` is the image
finset in `β`. The embedding condition guarantees that there are no duplicates in the image. 

## BASE-LIBRARY REF Finset.range
ℕ → Finset ℕ

Body:
fun n => { val := Multiset.range n, nodup := ⋯ }

Docstring: `range n` is the set of natural numbers less than `n`. 

## INFORMAL STATEMENT
lem.sf.skew-schur-zero-sb

\leanhelper  For any $N$-partition $\lambda $, we have $s_{\lambda /\mathbf{0}} = s_\lambda $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.monomial
def.sf.monomial

\textbf{(a)} A \emph{monomial} is an expression of the form $x_1^{a_1} x_2^{a_2} \cdots x_N^{a_N}$ with $a_1, a_2, \ldots , a_N \in \mathbb {N}$. \medskip 

\textbf{(b)} The \emph{degree} $\deg \mathfrak {m}$ of a monomial $\mathfrak {m} = x_1^{a_1} x_2^{a_2} \cdots x_N^{a_N}$ is defined to be $a_1 + a_2 + \cdots + a_N \in \mathbb {N}$. \medskip 

\textbf{(c)} A monomial $\mathfrak {m} = x_1^{a_1} x_2^{a_2} \cdots x_N^{a_N}$ is said to be \emph{squarefree} if $a_1, a_2, \ldots , a_N \in \{ 0,1\} $. (This is saying that no square or higher power of an indeterminate appears in $\mathfrak {m}$; thus the name “squarefree”.) \medskip 

\textbf{(d)} A monomial $\mathfrak {m} = x_1^{a_1} x_2^{a_2} \cdots x_N^{a_N}$ is said to be \emph{primal} if there is at most one $i \in [N]$ satisfying $a_i > 0$. (This is saying that the monomial $\mathfrak {m}$ contains no two distinct indeterminates. Thus, a primal monomial is just $1$ or a power of an indeterminate.)

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.npar
def.sf.Npar

An $N$\emph{-partition} will mean a weakly decreasing $N$-tuple of nonnegative integers. In other words, an $N$-partition means an $N$-tuple $\left( \lambda _{1},\lambda _{2},\ldots ,\lambda _{N}\right) \in \mathbb {N}^{N}$ with $\lambda _{1}\geq \lambda _{2}\geq \cdots \geq \lambda _{N}$. 

The \emph{size} (or weight) of an $N$-partition $\lambda = (\lambda _1, \lambda _2, \ldots , \lambda _N)$ is defined to be $|\lambda | := \lambda _1 + \lambda _2 + \cdots + \lambda _N$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.npar-order
def.sf.Npar-order

\leanhelper  We define a partial order on $N$-partitions by componentwise comparison: $\mu \leq \nu $ iff $\mu _i \leq \nu _i$ for all $i \in [N]$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.par-subset
def.sf.par-subset

Let $\lambda $ and $\mu $ be two $N$-partitions. 

We say that $\mu \subseteq \lambda $ if and only if $Y\left( \mu \right) \subseteq Y\left( \lambda \right) $. Equivalently, $\mu \subseteq \lambda $ if and only if

\[  \text{each }i\in \left[ N\right] \text{ satisfies }\mu _{i}\leq \lambda _{i}.  \]

 Thus we have defined a partial order $\subseteq $ on the set of all $N$-partitions.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.schur
def.sf.schur

Let $\lambda $ be an $N$-partition. We define the \emph{Schur polynomial} $s_{\lambda }\in \mathcal{P}$ by

\[  s_{\lambda }:=\sum _{T\in \operatorname *{SSYT}\left( \lambda \right) }x_{T}.  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.skew-diag
def.sf.skew-diag

Let $\lambda $ and $\mu $ be two $N$-partitions such that $\mu \subseteq \lambda $. Then, we define the \emph{skew Young diagram} $Y\left( \lambda /\mu \right) $ to be the set difference

\begin{align*}  Y\left( \lambda \right) \setminus Y\left( \mu \right) &  =\left\{  \left( i,j\right) \  \mid \  i\in \left[ N\right] \text{ and }j\in \left[ \lambda _{i}\right] \setminus \left[ \mu _{i}\right] \right\}  \\ &  =\left\{  \left( i,j\right) \  \mid \  i\in \left[ N\right] \text{ and }j\in \mathbb {Z}\text{ and }\mu _{i}<j\leq \lambda _{i}\right\}  . \end{align*}

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.skew-schur
def.sf.skew-schur

Let $\lambda $ and $\mu $ be two $N$-partitions. We define the \emph{skew Schur polynomial} $s_{\lambda /\mu }\in \mathcal{P}$ by

\[  s_{\lambda /\mu }:=\sum _{T\in \operatorname *{SSYT}\left( \lambda /\mu \right) }x_{T}.  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.ssyt
def.sf.ssyt

Let $\lambda $ be an $N$-partition. 

A Young tableau $T$ of shape $\lambda $ is said to be \emph{semistandard} if its entries 

\begin{itemize} \item increase weakly along each row (from left to right); 

\item increase strictly down each column (from top to bottom). 

\end{itemize}

Formally speaking, this means that a Young tableau $T:Y\left( \lambda \right) \rightarrow \left[ N\right] $ is semistandard if and only if 

\begin{itemize} \item we have $T\left( i,j\right) \leq T\left( i,j+1\right) $ for any $\left( i,j\right) \in Y\left( \lambda \right) $ satisfying $\left( i,j+1\right) \in Y\left( \lambda \right) $; 

\item we have $T\left( i,j\right) <T\left( i+1,j\right) $ for any $\left( i,j\right) \in Y\left( \lambda \right) $ satisfying $\left( i+1,j\right) \in Y\left( \lambda \right) $. 

\end{itemize}

We let $\operatorname *{SSYT}\left( \lambda \right) $ denote the set of all semistandard Young tableaux of shape $\lambda $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.strips
def.sf.strips

Let $\lambda $ and $\mu $ be two $N$-partitions. 

\textbf{(a)} We write $\lambda /\mu $ for the pair $\left( \mu ,\lambda \right) $. Such a pair is called a \emph{skew partition}. 

\textbf{(b)} We say that $\lambda /\mu $ is a \emph{horizontal strip} if we have $\mu \subseteq \lambda $ and the Young diagram $Y\left( \lambda /\mu \right) $ has no two boxes lying in the same column. 

\textbf{(c)} We say that $\lambda /\mu $ is a \emph{vertical strip} if we have $\mu \subseteq \lambda $ and the Young diagram $Y\left( \lambda /\mu \right) $ has no two boxes lying in the same row. 

Now, let $n\in \mathbb {N}$. 

\textbf{(d)} We say that $\lambda /\mu $ is a \emph{horizontal }$n$\emph{-strip} if $\lambda /\mu $ is a horizontal strip and satisfies $\left\vert Y\left( \lambda /\mu \right) \right\vert =n$. 

\textbf{(e)} We say that $\lambda /\mu $ is a \emph{vertical }$n$\emph{-strip} if $\lambda /\mu $ is a vertical strip and satisfies $\left\vert Y\left( \lambda /\mu \right) \right\vert =n$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.ydiag
def.sf.ydiag

Let $\lambda $ be an $N$-partition. 

The \emph{Young diagram} of $\lambda $ is defined as the set

\[  \left\{  \left( i,j\right) \  \mid \  i\in \left[ N\right] \text{ and }j\in \left[ \lambda _{i}\right] \right\}  \subseteq \left\{  1,2,3,\ldots \right\}  ^{2}.  \]

 We visually represent each element $\left( i,j\right) $ of this Young diagram as a box in row $i$ and column $j$. 

We denote the Young diagram of $\lambda $ by $Y\left( \lambda \right) $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.ytab
def.sf.ytab

Let $\lambda $ be an $N$-partition. 

A \emph{Young tableau} of shape $\lambda $ means a way of filling the boxes of $Y\left( \lambda \right) $ with elements of $\left[ N\right] $ (one element per box). Formally speaking, it is defined as a map $T:Y\left( \lambda \right) \rightarrow \left[ N\right] $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.ytab.xt
def.sf.ytab.xT

Let $\lambda $ be an $N$-partition. If $T$ is any Young tableau of shape $\lambda $, then we define the corresponding monomial

\[  x_{T}:=\prod _{c\text{ is a box of }Y\left( \lambda \right) }x_{T\left( c\right) }=\prod _{\left( i,j\right) \in Y\left( \lambda \right) }x_{T\left( i,j\right) }=\prod _{k=1}^{N}x_{k}^{\left( \text{\#  of times }k\text{ appears in }T\right) }.  \]

## VERDICT
{
  "verdict": "minor_discrepancy",
  "discrepancies": [
    {
      "root": "[inst : NeZero N]",
      "severity": "minor",
      "bridge": "Handle the excluded case N = 0 directly. Then Fin 0 is empty, every NPartition 0 has the unique empty tuple of parts, both the Young diagram and the skew diagram against 0 are empty, and each SSYT sum consists of the unique empty filling with monomial equal to the empty product 1. Hence skewSchurPoly lam 0 = schurPoly lam also holds for N = 0 by unfolding the definitions."
    }
  ],
  "justification": "The blueprint says, \u201cFor any N-partition \u03bb, we have s_{\u03bb/0} = s_\u03bb,\u201d without requiring N \u2260 0. The elaborated signature instead begins \u201c\u2200 {N : \u2115} [inst : NeZero N] (lam : NPartition N),\u201d so it excludes N = 0. All positive N are covered, and the omitted empty case is routine from the displayed definition bodies. The formal definitions otherwise match the blueprint: skewSchurPoly is the sum over SSYT fillings of Y(\u03bb) \\ Y(0), while schurPoly is the corresponding sum over SSYT fillings of Y(\u03bb); NPartition.zero has all parts zero."
}