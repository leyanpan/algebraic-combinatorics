## TARGET SymmetricFunctions.pieri_horizontal (theorem) — ELABORATED SIGNATURE
∀ {N : ℕ} {R : Type u_1} [inst : CommRing R] (n : ℕ) (mu : SymmetricFunctions.NPartition N),
  MvPolynomial.hsymm (Fin N) R n * SymmetricFunctions.schur mu =
    ∑ lam ∈ SymmetricFunctions.horizontalNStripPartitions mu n, SymmetricFunctions.schur lam

## TARGET SymmetricFunctions.pieri_vertical (theorem) — ELABORATED SIGNATURE
∀ {N : ℕ} {R : Type u_1} [inst : CommRing R] (n : ℕ) (mu : SymmetricFunctions.NPartition N),
  MvPolynomial.esymm (Fin N) R n * SymmetricFunctions.schur mu =
    ∑ lam ∈ SymmetricFunctions.verticalNStripPartitions mu n, SymmetricFunctions.schur lam

## PROJECT DEPENDENCY SymmetricFunctions.NPartition (inductive)
ℕ → Type

Body:
SymmetricFunctions.NPartition.mk : {N : ℕ} → (parts : Fin N → ℕ) → (∀ (i j : Fin N), i ≤ j → parts j ≤ parts i) → SymmetricFunctions.NPartition N

Docstring: An N-partition is a list of length N with weakly decreasing nonnegative entries.
This corresponds to Definition def.sf.N-par in the source.

**Note:** This is `SymmetricFunctions.NPartition`, a local definition.
A canonical top-level `NPartition` exists in `NPartition.lean` with the same
semantics (using `antitone` as the field name instead of `weaklyDecreasing`).
See the section docstring for details. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SymmetricPolynomials.P_isCommRing' (def)
{K : Type u_1} → [inst : CommRing K] → {N : ℕ} → CommRing (AlgebraicCombinatorics.SymmetricPolynomials.P K N)

Body:
fun {K} [CommRing K] {N} => inferInstance

Docstring: The polynomial ring P K N is a commutative K-algebra.
Label: def.sf.PS 

## PROJECT DEPENDENCY SymmetricFunctions.schur (def)
{N : ℕ} → {R : Type u_1} → [inst : CommRing R] → SymmetricFunctions.NPartition N → MvPolynomial (Fin N) R

Body:
fun {N} {R} [CommRing R] lam => ∑ T ∈ SymmetricFunctions.ssytFinset lam, T.toMonomial

Docstring: The Schur polynomial s_λ defined as the sum over all SSYT of shape λ.
Definition def.sf.schur. 

## PROJECT DEPENDENCY SymmetricFunctions.horizontalNStripPartitions (def)
{N : ℕ} → SymmetricFunctions.NPartition N → ℕ → Finset (SymmetricFunctions.NPartition N)

Body:
fun {N} mu n =>
  Finset.image
    (fun x =>
      match x with
      | ⟨f, hf⟩ =>
        have hf' := ⋯;
        SymmetricFunctions.toNPartition f ⋯)
    {f ∈ SymmetricFunctions.potentialHorizontalStrips mu n |
        SymmetricFunctions.isWeaklyDecreasing f ∧
          SymmetricFunctions.isHorizontalStripFun f mu.parts ∧ SymmetricFunctions.hasSizeDiff mu.parts f n}.attach

Docstring: The set of N-partitions λ such that λ/μ is a horizontal n-strip.

This is the set of all N-partitions λ satisfying:
1. μ ⊆ λ (containment): μ_i ≤ λ_i for all i
2. Horizontal strip: μ_i ≥ λ_{i+1} for all i < N
3. Size: |λ| - |μ| = n

The set is finite because each λ_i is bounded. 

## PROJECT DEPENDENCY SymmetricFunctions.verticalNStripPartitions (def)
{N : ℕ} → SymmetricFunctions.NPartition N → ℕ → Finset (SymmetricFunctions.NPartition N)

Body:
fun {N} mu n =>
  Finset.image
    (fun x =>
      match x with
      | ⟨f, hf⟩ =>
        have hf' := ⋯;
        SymmetricFunctions.toNPartition f ⋯)
    {f ∈ SymmetricFunctions.potentialVerticalStrips mu |
        SymmetricFunctions.isWeaklyDecreasing f ∧
          SymmetricFunctions.isVerticalStripFun f mu.parts ∧ SymmetricFunctions.hasSizeDiff mu.parts f n}.attach

Docstring: The set of N-partitions λ such that λ/μ is a vertical n-strip.

This is the set of all N-partitions λ satisfying:
1. μ ⊆ λ (containment): μ_i ≤ λ_i for all i
2. Vertical strip: λ_i ≤ μ_i + 1 for all i
3. Size: |λ| - |μ| = n

The set is finite because each λ_i ∈ {μ_i, μ_i + 1}. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SymmetricPolynomials.P (def)
(K : Type u_2) → [CommRing K] → ℕ → Type u_2

Body:
fun K [CommRing K] N => MvPolynomial (Fin N) K

Docstring: The polynomial ring in N variables over K.
This corresponds to 𝒫 in the source (Definition def.sf.PS (a)).
Label: def.sf.PS 

## PROJECT DEPENDENCY SymmetricFunctions.SSYT (inductive)
{N : ℕ} → SymmetricFunctions.NPartition N → Type

Body:
SymmetricFunctions.SSYT.mk : {N : ℕ} →
  {lam : SymmetricFunctions.NPartition N} →
    (entries : (i : Fin N) → Fin (lam.parts i) → Fin N) →
      (∀ (i : Fin N) (j k : Fin (lam.parts i)), j ≤ k → entries i j ≤ entries i k) →
        (∀ (i : Fin N) (hi : ↑i + 1 < N) (j : Fin (lam.parts i)) (hj : ↑j < lam.parts ⟨↑i + 1, hi⟩),
            entries i j < entries ⟨↑i + 1, hi⟩ ⟨↑j, hj⟩) →
          SymmetricFunctions.SSYT lam

Docstring: A semistandard Young tableau (SSYT) of shape λ with entries in [N].
The entries are weakly increasing along rows and strictly increasing down columns.
Definition def.sf.ssyt.

**Note:** This is one of two SSYT definitions in this project:
- **This definition** (`SymmetricFunctions.SSYT`): Uses dependent types
  `entries : (i : Fin N) → (j : Fin (lam.parts i)) → Fin N`. Standalone structure.
  No `[NeZero N]` requirement. Field names: `rowWeak`, `colStrict`.
- **Alternative definition** (`SchurBasics.SSYT` in `SchurBasics.lean`): Uses
  `entry : Fin N × ℕ → Fin N` with a support condition. Extends `YoungTableau`.
  Requires `[NeZero N]`. Field names: `row_weak`, `col_strict`.

The equivalence between these definitions is established in `SSYTEquiv.lean` via
`SSYTEquiv.ssytEquiv`. Use `SSYTEquiv.toSchurBasicsSSYT` and `SSYTEquiv.toSFSSYT`
to convert between representations.

**When to use which:**
- Use this definition when the dependent type ensures bounds checking at compile time,
  or when `[NeZero N]` is not available.
- Use `SchurBasics.SSYT` when working with cell coordinates `(i, j)` directly, or when
  extending the `YoungTableau` structure is beneficial. 

## PROJECT DEPENDENCY SymmetricFunctions.ssytFinset (def)
{N : ℕ} → (lam : SymmetricFunctions.NPartition N) → Finset (SymmetricFunctions.SSYT lam)

Body:
fun {N} lam =>
  Finset.map
    {
      toFun := fun x =>
        match x with
        | ⟨f, hf⟩ => SymmetricFunctions.fillingToSSYT lam f ⋯,
      inj' := ⋯ }
    (SymmetricFunctions.ssytFillingFinsetNonSkew lam).attach

Docstring: The set of all SSYT of shape λ.
This is finite because it's a subset of all fillings, which is finite. 

## PROJECT DEPENDENCY SymmetricFunctions.SSYT.toMonomial (def)
{N : ℕ} →
  {R : Type u_1} →
    [inst : CommRing R] → {lam : SymmetricFunctions.NPartition N} → SymmetricFunctions.SSYT lam → MvPolynomial (Fin N) R

Body:
fun {N} {R} [CommRing R] {lam} T => ∏ i, ∏ j, MvPolynomial.X (T.entries i j)

Docstring: The monomial x^T associated to a tableau T.
x_T = ∏_{(i,j) ∈ Y(λ)} x_{T(i,j)} 

## PROJECT DEPENDENCY SymmetricFunctions.isWeaklyDecreasing (def)
{N : ℕ} → (Fin N → ℕ) → Prop

Body:
fun {N} f => ∀ (i j : Fin N), i ≤ j → f j ≤ f i

Docstring: Check if a function forms a valid N-partition (weakly decreasing). 

## PROJECT DEPENDENCY SymmetricFunctions.isHorizontalStripFun (def)
{N : ℕ} → (Fin N → ℕ) → (Fin N → ℕ) → Prop

Body:
fun {N} lam mu => ∀ (i : Fin N) (hi : ↑i + 1 < N), mu i ≥ lam ⟨↑i + 1, hi⟩

Docstring: A skew partition λ/μ is a horizontal strip if no two boxes lie in the same column.
Equivalently: μ_i ≥ λ_{i+1} for all i.

The argument order `(lam, mu)` matches standard mathematical notation λ/μ.

**Related definitions:**
- `SkewPartition.isHorizontalStrip`: Bundled version for `SkewPartition N` 

## PROJECT DEPENDENCY SymmetricFunctions.NPartition.parts (def)
{N : ℕ} → SymmetricFunctions.NPartition N → Fin N → ℕ

Body:
fun N self => self.1

Docstring: The parts of the partition 

## PROJECT DEPENDENCY SymmetricFunctions.hasSizeDiff (def)
{N : ℕ} → (Fin N → ℕ) → (Fin N → ℕ) → ℕ → Prop

Body:
fun {N} mu lam n => ∑ i, lam i = ∑ i, mu i + n

Docstring: Check if |λ| - |μ| = n. 

## PROJECT DEPENDENCY SymmetricFunctions.instDecidableIsWeaklyDecreasing (def)
{N : ℕ} → (f : Fin N → ℕ) → Decidable (SymmetricFunctions.isWeaklyDecreasing f)

Body:
fun {N} f => Fintype.decidableForallFintype

## PROJECT DEPENDENCY SymmetricFunctions.instDecidableIsHorizontalStripFun (def)
{N : ℕ} → (lam mu : Fin N → ℕ) → Decidable (SymmetricFunctions.isHorizontalStripFun lam mu)

Body:
fun {N} lam mu => Fintype.decidableForallFintype

Docstring: Decidable instance for horizontal strip predicate. 

## PROJECT DEPENDENCY SymmetricFunctions.instDecidableHasSizeDiff (def)
{N : ℕ} → (mu lam : Fin N → ℕ) → (n : ℕ) → Decidable (SymmetricFunctions.hasSizeDiff mu lam n)

Body:
fun {N} mu lam n => inferInstanceAs (Decidable (∑ i, lam i = ∑ i, mu i + n))

## PROJECT DEPENDENCY SymmetricFunctions.potentialHorizontalStrips (def)
{N : ℕ} → SymmetricFunctions.NPartition N → ℕ → Finset (Fin N → ℕ)

Body:
fun {N} mu n => Fintype.piFinset fun i => Finset.Icc (mu.parts i) (SymmetricFunctions.horizontalStripUpperBound mu n i)

Docstring: A function from Fin N to ℕ that could potentially form a horizontal n-strip with μ.
This is the set of all functions bounded by the horizontal strip constraints. 

## PROJECT DEPENDENCY SymmetricFunctions.NPartition.instDecidableEq (def)
{N : ℕ} → DecidableEq (SymmetricFunctions.NPartition N)

Body:
fun {N} lam mu => decidable_of_iff (lam.parts = mu.parts) ⋯

Docstring: Decidable equality for N-partitions. 

## PROJECT DEPENDENCY SymmetricFunctions.toNPartition (def)
{N : ℕ} → (f : Fin N → ℕ) → SymmetricFunctions.isWeaklyDecreasing f → SymmetricFunctions.NPartition N

Body:
fun {N} f hf => { parts := f, weaklyDecreasing := hf }

Docstring: Convert a valid function to an NPartition. 

## PROJECT DEPENDENCY SymmetricFunctions.isVerticalStripFun (def)
{N : ℕ} → (Fin N → ℕ) → (Fin N → ℕ) → Prop

Body:
fun {N} lam mu => ∀ (i : Fin N), lam i ≤ mu i + 1

Docstring: A skew partition λ/μ is a vertical strip if no two boxes lie in the same row.
Equivalently: λ_i ≤ μ_i + 1 for all i.

The argument order `(lam, mu)` matches standard mathematical notation λ/μ.

**Related definitions:**
- `SkewPartition.isVerticalStrip`: Bundled version for `SkewPartition N` 

## PROJECT DEPENDENCY SymmetricFunctions.instDecidableIsVerticalStripFun (def)
{N : ℕ} → (lam mu : Fin N → ℕ) → Decidable (SymmetricFunctions.isVerticalStripFun lam mu)

Body:
fun {N} lam mu => Fintype.decidableForallFintype

Docstring: Decidable instance for vertical strip predicate. 

## PROJECT DEPENDENCY SymmetricFunctions.potentialVerticalStrips (def)
{N : ℕ} → SymmetricFunctions.NPartition N → Finset (Fin N → ℕ)

Body:
fun {N} mu => Fintype.piFinset fun i => Finset.Icc (mu.parts i) (SymmetricFunctions.verticalStripUpperBound mu i)

Docstring: A function from Fin N to ℕ that could potentially form a vertical n-strip with μ. 

## PROJECT DEPENDENCY SymmetricFunctions.Filling (def)
{N : ℕ} → SymmetricFunctions.NPartition N → Type

Body:
fun {N} lam => (i : Fin N) → Fin (lam.parts i) → Fin N

Docstring: A filling of a non-skew shape λ. 

## PROJECT DEPENDENCY SymmetricFunctions.ssytFillingFinsetNonSkew (def)
{N : ℕ} → (lam : SymmetricFunctions.NPartition N) → Finset (SymmetricFunctions.Filling lam)

Body:
fun {N} lam => Finset.filter (SymmetricFunctions.isSSYTFillingNonSkew lam) Finset.univ

Docstring: Finset of valid fillings for non-skew shapes. 

## PROJECT DEPENDENCY SymmetricFunctions.fillingToSSYT (def)
{N : ℕ} →
  (lam : SymmetricFunctions.NPartition N) →
    (f : SymmetricFunctions.Filling lam) → SymmetricFunctions.isSSYTFillingNonSkew lam f → SymmetricFunctions.SSYT lam

Body:
fun {N} lam f hf => { entries := f, rowWeak := ⋯, colStrict := ⋯ }

Docstring: Convert a valid filling to an SSYT. 

## PROJECT DEPENDENCY SymmetricFunctions.SSYT.entries (def)
{N : ℕ} →
  {lam : SymmetricFunctions.NPartition N} → SymmetricFunctions.SSYT lam → (i : Fin N) → Fin (lam.parts i) → Fin N

Body:
fun N lam self => self.1

Docstring: The entries of the tableau 

## PROJECT DEPENDENCY SymmetricFunctions.horizontalStripUpperBound (def)
{N : ℕ} → SymmetricFunctions.NPartition N → ℕ → Fin N → ℕ

Body:
fun {N} mu n i => if h : ↑i = 0 then mu.parts ⟨0, ⋯⟩ + n else mu.parts ⟨↑i - 1, ⋯⟩

Docstring: The bound for each λ_i when forming a horizontal strip with μ.
λ_i must satisfy μ_i ≤ λ_i ≤ bound_i where:
- For i = 0: bound_0 = μ_0 + n (since |λ| - |μ| = n and all parts are bounded by λ_0)
- For i > 0: bound_i = μ_{i-1} (horizontal strip condition: μ_{i-1} ≥ λ_i) 

## PROJECT DEPENDENCY SymmetricFunctions.NPartition.mk (constructor)
{N : ℕ} → (parts : Fin N → ℕ) → (∀ (i j : Fin N), i ≤ j → parts j ≤ parts i) → SymmetricFunctions.NPartition N

## PROJECT DEPENDENCY SymmetricFunctions.verticalStripUpperBound (def)
{N : ℕ} → SymmetricFunctions.NPartition N → Fin N → ℕ

Body:
fun {N} mu i => mu.parts i + 1

Docstring: The bound for each λ_i when forming a vertical strip with μ.
λ_i must satisfy μ_i ≤ λ_i ≤ μ_i + 1 (vertical strip condition). 

## PROJECT DEPENDENCY SymmetricFunctions.isSSYTFillingNonSkew (def)
{N : ℕ} → (lam : SymmetricFunctions.NPartition N) → SymmetricFunctions.Filling lam → Prop

Body:
fun {N} lam f => SymmetricFunctions.isRowWeakFilling lam f ∧ SymmetricFunctions.isColStrictFilling lam f

Docstring: Combined SSYT predicate for non-skew fillings. 

## PROJECT DEPENDENCY SymmetricFunctions.isSSYTFillingNonSkew_decidable (def)
{N : ℕ} →
  (lam : SymmetricFunctions.NPartition N) →
    (f : SymmetricFunctions.Filling lam) → Decidable (SymmetricFunctions.isSSYTFillingNonSkew lam f)

Body:
fun {N} lam f => instDecidableAnd

Docstring: Decidability of SSYT predicate for non-skew fillings. 

## PROJECT DEPENDENCY SymmetricFunctions.filling_fintype (def)
{N : ℕ} → (lam : SymmetricFunctions.NPartition N) → Fintype (SymmetricFunctions.Filling lam)

Body:
fun {N} lam => inferInstance

Docstring: Fintype instance for fillings of non-skew shapes. 

## PROJECT DEPENDENCY SymmetricFunctions.SSYT.mk (constructor)
{N : ℕ} →
  {lam : SymmetricFunctions.NPartition N} →
    (entries : (i : Fin N) → Fin (lam.parts i) → Fin N) →
      (∀ (i : Fin N) (j k : Fin (lam.parts i)), j ≤ k → entries i j ≤ entries i k) →
        (∀ (i : Fin N) (hi : ↑i + 1 < N) (j : Fin (lam.parts i)) (hj : ↑j < lam.parts ⟨↑i + 1, hi⟩),
            entries i j < entries ⟨↑i + 1, hi⟩ ⟨↑j, hj⟩) →
          SymmetricFunctions.SSYT lam

## PROJECT DEPENDENCY SymmetricFunctions.isRowWeakFilling (def)
{N : ℕ} → (lam : SymmetricFunctions.NPartition N) → SymmetricFunctions.Filling lam → Prop

Body:
fun {N} lam f => ∀ (i : Fin N) (j k : Fin (lam.parts i)), j ≤ k → f i j ≤ f i k

Docstring: Row-weak predicate for fillings of non-skew shapes. 

## PROJECT DEPENDENCY SymmetricFunctions.isColStrictFilling (def)
{N : ℕ} → (lam : SymmetricFunctions.NPartition N) → SymmetricFunctions.Filling lam → Prop

Body:
fun {N} lam f =>
  ∀ (i : Fin N) (hi : ↑i + 1 < N) (j : Fin (lam.parts i)) (hj : ↑j < lam.parts ⟨↑i + 1, hi⟩),
    f i j < f ⟨↑i + 1, hi⟩ ⟨↑j, hj⟩

Docstring: Column-strict predicate for fillings of non-skew shapes. 

## PROJECT DEPENDENCY SymmetricFunctions.isRowWeakFilling_decidable (def)
{N : ℕ} →
  (lam : SymmetricFunctions.NPartition N) →
    (f : SymmetricFunctions.Filling lam) → Decidable (SymmetricFunctions.isRowWeakFilling lam f)

Body:
fun {N} lam f => Fintype.decidableForallFintype

Docstring: Decidability of row-weak for non-skew fillings. 

## PROJECT DEPENDENCY SymmetricFunctions.isColStrictFilling_decidable (def)
{N : ℕ} →
  (lam : SymmetricFunctions.NPartition N) →
    (f : SymmetricFunctions.Filling lam) → Decidable (SymmetricFunctions.isColStrictFilling lam f)

Body:
fun {N} lam f => Fintype.decidableForallFintype

Docstring: Decidability of column-strict for non-skew fillings. 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF CommRing
Type u → Type u

Docstring: A commutative ring is a ring with commutative multiplication. 

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

## BASE-LIBRARY REF MvPolynomial
Type u_1 → (R : Type u_2) → [CommSemiring R] → Type (max u_2 u_1)

Docstring: Multivariate polynomial, where `σ` is the index set of the variables and
`R` is the coefficient ring 

## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


## BASE-LIBRARY REF CommRing.toCommSemiring
{α : Type u} → [s : CommRing α] → CommSemiring α

## BASE-LIBRARY REF HMul.hMul
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HMul α β γ] → α → β → γ

Docstring: `a * b` computes the product of `a` and `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `*` in identifiers is `mul`.

## BASE-LIBRARY REF instHMul
{α : Type u_1} → [Mul α] → HMul α α α

## BASE-LIBRARY REF Distrib.toMul
{R : Type u_1} → [self : Distrib R] → Mul R

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.toDistrib
{α : Type u} → [self : NonUnitalNonAssocSemiring α] → Distrib α

## BASE-LIBRARY REF NonUnitalNonAssocRing.toNonUnitalNonAssocSemiring
{α : Type u} → [self : NonUnitalNonAssocRing α] → NonUnitalNonAssocSemiring α

## BASE-LIBRARY REF NonUnitalNonAssocCommRing.toNonUnitalNonAssocRing
{α : Type u} → [self : NonUnitalNonAssocCommRing α] → NonUnitalNonAssocRing α

## BASE-LIBRARY REF NonUnitalCommRing.toNonUnitalNonAssocCommRing
{α : Type u} → [self : NonUnitalCommRing α] → NonUnitalNonAssocCommRing α

## BASE-LIBRARY REF CommRing.toNonUnitalCommRing
{α : Type u} → [s : CommRing α] → NonUnitalCommRing α

## BASE-LIBRARY REF MvPolynomial.hsymm
(σ : Type u_5) → (R : Type u_6) → [inst : CommSemiring R] → [Fintype σ] → [DecidableEq σ] → ℕ → MvPolynomial σ R

Docstring: The `n`th complete homogeneous symmetric `MvPolynomial σ R`.
It is the sum over all the degree n monomials in `MvPolynomial σ R`. 

## BASE-LIBRARY REF Fin.fintype
(n : ℕ) → Fintype (Fin n)

## BASE-LIBRARY REF instDecidableEqFin
(n : ℕ) → DecidableEq (Fin n)

## BASE-LIBRARY REF Finset.sum
{ι : Type u_1} → {M : Type u_3} → [AddCommMonoid M] → Finset ι → (ι → M) → M

Docstring: `∑ x ∈ s, f x` is the sum of `f x` as `x` ranges over the elements
of the finite set `s`.

When the index type is a `Fintype`, the notation `∑ x, f x`, is a shorthand for
`∑ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.toAddCommMonoid
{α : Type u} → [self : NonUnitalNonAssocSemiring α] → AddCommMonoid α

## BASE-LIBRARY REF MvPolynomial.esymm
(σ : Type u_5) → (R : Type u_6) → [inst : CommSemiring R] → [Fintype σ] → ℕ → MvPolynomial σ R

Docstring: The `n`th elementary symmetric `MvPolynomial σ R`.
It is the sum over all the degree n squarefree monomials in `MvPolynomial σ R`. 

## INFORMAL STATEMENT
Pieri rules

Let $n\in \mathbb {N}$. Let $\mu $ be an $N$-partition. Then: 

\textbf{(a)} We have

\[  h_{n}s_{\mu }=\sum _{\substack {\lambda \text{ is an }N\text{-partition;}\\ \lambda /\mu \text{ is a horizontal }n\text{-strip}}}s_{\lambda }.  \]

\textbf{(b)} We have

\[  e_{n}s_{\mu }=\sum _{\substack {\lambda \text{ is an }N\text{-partition;}\\ \lambda /\mu \text{ is a vertical }n\text{-strip}}}s_{\lambda }.  \]

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.essfinsum
def.fps.essFinSum

\leanhelper  For an essentially finite family $(a_i)_{i\in I}$, the \emph{essentially finite sum} $\sum _{i\in I} a_i$ is defined as $\sum _{i\in S} a_i$ where $S = \{ i\in I \mid a_i \neq 0\} $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.fps
def.fps.fps

A \emph{formal power series} (or, short, \emph{FPS}) in $1$ indeterminate over $K$ means a sequence $\left(a_{0},a_{1},a_{2},\ldots \right) = \left(a_{n}\right)_{n\in \mathbb {N}} \in K^{\mathbb {N}}$ of elements of $K$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.gf
def.fps.gf

\leanhelper  The \emph{(ordinary) generating function} of a sequence $(a_0, a_1, a_2, \ldots )$ is the FPS $(a_0, a_1, a_2, \ldots ) = \sum _{n\geq 0} a_n x^n$.

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.pol
def.fps.pol

\textbf{(a)} An FPS $a\in K\left[ \left[ x\right] \right] $ is said to be a \emph{polynomial} if all but finitely many $n\in \mathbb {N}$ satisfy $\left[ x^{n}\right] a=0$ (that is, if all but finitely many coefficients of $a$ are $0$). \medskip 

\textbf{(b)} We let $K\left[ x\right] $ be the set of all polynomials $a\in K\left[ \left[ x\right] \right] $. This set $K\left[ x\right] $ is a subring of $K\left[ \left[ x\right] \right] $ (according to Theorem \ref{thm.fps.pol.ring} below), and is called the \emph{univariate polynomial ring} over $K$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.wcomps
def.fps.wcomps

\textbf{(a)} An \emph{(integer) weak composition} means a (finite) tuple of nonnegative integers. \medskip 

\textbf{(b)} The \emph{size} of a weak composition $\alpha =\left( \alpha _{1},\alpha _{2},\ldots ,\alpha _{m}\right) $ is defined to be the integer $\alpha _{1}+\alpha _{2}+\cdots +\alpha _{m}$. It is written $\left\vert \alpha \right\vert $. \medskip 

\textbf{(c)} The \emph{length} of a weak composition $\alpha =\left( \alpha _{1},\alpha _{2},\ldots ,\alpha _{m}\right) $ is defined to be the integer $m$. It is written $\ell \left( \alpha \right) $. \medskip 

\textbf{(d)} Let $n\in \mathbb {N}$. A \emph{weak composition of }$n$ means a weak composition whose size is $n$. \medskip 

\textbf{(e)} Let $n\in \mathbb {N}$ and $k\in \mathbb {N}$. A \emph{weak composition of }$n$\emph{ into }$k$\emph{ parts} is a weak composition whose size is $n$ and whose length is $k$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.x
def.fps.x

Let $x$ denote the FPS $\left(0,1,0,0,0,\ldots \right)$. In other words, let $x$ denote the FPS with $\left[x^{1}\right]x=1$ and $\left[x^{i}\right]x=0$ for all $i\neq 1$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.infsum.essfin
def.infsum.essfin

\textbf{(a)} A family $\left(a_{i}\right)_{i\in I}\in K^{I}$ of elements of $K$ is said to be \emph{essentially finite} if all but finitely many $i\in I$ satisfy $a_{i}=0$ (in other words, if the set $\left\{ i\in I\  \mid \  a_{i}\neq 0\right\} $ is finite). \medskip 

\textbf{(b)} Let $\left(a_{i}\right)_{i\in I}\in K^{I}$ be an essentially finite family of elements of $K$. Then, the infinite sum $\sum _{i\in I}a_{i}$ is defined to equal the finite sum $\sum _{\substack {i\in I;\\ a_{i}\neq 0}}a_{i}$. Such an infinite sum is said to be \emph{essentially finite}.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.perm
def.perm.perm

Let $X$ be a set. 

\textbf{(a)} A \emph{permutation} of $X$ means a bijection from $X$ to $X$. 

\textbf{(b)} It is known that the set of all permutations of $X$ is a group under composition. This group is called the \emph{symmetric group} of $X$, and is denoted by $S_X$. Its neutral element is the identity map $\operatorname {id}_X : X \to X$. Its size is $|X|!$ when $X$ is finite. 

\textbf{(c)} As usual in group theory, we will write $\alpha \beta $ for the composition $\alpha \circ \beta $ when $\alpha , \beta \in S_X$. This is the map that sends each $x \in X$ to $\alpha (\beta (x))$. 

\textbf{(d)} If $\alpha \in S_X$ and $i \in \mathbb {Z}$, then $\alpha ^i$ shall denote the $i$-th power of $\alpha $ in the group $S_X$. Note that $\alpha ^i = \underbrace{\alpha \circ \alpha \circ \cdots \circ \alpha }_{i\text{ times}}$ if $i \ge 0$. Also, $\alpha ^0 = \operatorname {id}_X$. Also, $\alpha ^{-1}$ is the inverse of $\alpha $ in the group $S_X$, that is, the inverse of the map $\alpha $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.sn-iven
def.perm.Sn-iven

Let $n \in \mathbb {Z}$. Then, $[n]$ shall mean the set $\{ 1, 2, \ldots , n\} $. This is an $n$-element set if $n \ge 0$, and is an empty set if $n \le 0$. 

The symmetric group $S_{[n]}$ (consisting of all permutations of $[n]$) will be denoted $S_n$ and called the $n$\emph{-th symmetric group}. Its size is $n!$ (when $n \ge 0$).

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.pol.subs
def.pol.subs

Let $f\in K\left[ x\right] $ be a polynomial. Let $A$ be any $K$-algebra. Let $a\in A$ be any element. We then define an element $f\left[ a\right] \in A$ as follows: 

Write $f$ in the form $f=\sum _{n\in \mathbb {N}}f_{n}x^{n}$ with $f_{0},f_{1},f_{2},\ldots \in K$. (That is, $f_{n}=\left[ x^{n}\right] f$ for each $n\in \mathbb {N}$.) Then, set

\[  f\left[ a\right] :=\sum _{n\in \mathbb {N}}f_{n}a^{n}.  \]

 (This sum is essentially finite, since $f$ is a polynomial.) 

The element $f\left[ a\right] $ is also denoted by $f\circ a$ or by $f\left( a\right) $, and is called the \emph{value} of $f$ at $a$ (or the \emph{evaluation} of $f$ at $a$, or the \emph{result of substituting }$a$ for $x$ in $f$).

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.ehp
def.sf.ehp

\textbf{(a)} For each $n \in \mathbb {Z}$, define a symmetric polynomial $e_n \in \mathcal{S}$ by 

\[  e_n = \sum _{\substack {(i_1, i_2, \ldots , i_n) \in [N]^n; \\ i_1 < i_2 < \cdots < i_n}} x_{i_1} x_{i_2} \cdots x_{i_n} = (\text{sum of all squarefree monomials of degree } n).  \]

 This $e_n$ is called the $n$-th \emph{elementary symmetric polynomial} in $x_1, x_2, \ldots , x_N$. \medskip 

\textbf{(b)} For each $n \in \mathbb {Z}$, define a symmetric polynomial $h_n \in \mathcal{S}$ by 

\[  h_n = \sum _{\substack {(i_1, i_2, \ldots , i_n) \in [N]^n; \\ i_1 \leq i_2 \leq \cdots \leq i_n}} x_{i_1} x_{i_2} \cdots x_{i_n} = (\text{sum of all monomials of degree } n).  \]

 This $h_n$ is called the $n$-th \emph{complete homogeneous symmetric polynomial} in $x_1, x_2, \ldots , x_N$. \medskip 

\textbf{(c)} For each $n \in \mathbb {Z}$, define a symmetric polynomial $p_n \in \mathcal{S}$ by 

\begin{align*}  p_n & = \begin{cases}  x_1^n + x_2^n + \cdots + x_N^n, &  \text{if } n > 0; \\ 1, &  \text{if } n = 0; \\ 0, &  \text{if } n < 0 \end{cases}\\ & = (\text{sum of all primal monomials of degree } n). \end{align*}

 This $p_n$ is called the $n$-th \emph{power sum} in $x_1, x_2, \ldots , x_N$.

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.npar-youngdiagram
def.sf.Npar-youngDiagram

\leanhelper  The \emph{Young diagram} $Y(\lambda )$ of an $N$-partition $\lambda $ is the finite set of cells 

\[  Y(\lambda ) = \{ (i, j) : i \in [N],\;  0 \leq j < \lambda _i\} .  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.par-subset
def.sf.par-subset

Let $\lambda $ and $\mu $ be two $N$-partitions. 

We say that $\mu \subseteq \lambda $ if and only if $Y\left( \mu \right) \subseteq Y\left( \lambda \right) $. Equivalently, $\mu \subseteq \lambda $ if and only if

\[  \text{each }i\in \left[ N\right] \text{ satisfies }\mu _{i}\leq \lambda _{i}.  \]

 Thus we have defined a partial order $\subseteq $ on the set of all $N$-partitions.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.ps
def.sf.PS

\textbf{(a)} Let $\mathcal{P}$ be the polynomial ring $K[x_1, x_2, \ldots , x_N]$ in $N$ variables over $K$. This is not just a ring; it is a commutative $K$-algebra. \medskip 

\textbf{(b)} The symmetric group $S_N$ acts on the set $\mathcal{P}$ according to the formula 

\[  \sigma \cdot f = f[x_{\sigma (1)}, x_{\sigma (2)}, \ldots , x_{\sigma (N)}] \quad \text{for any } \sigma \in S_N \text{ and any } f \in \mathcal{P}.  \]

 Here, $f[a_1, a_2, \ldots , a_N]$ means the result of substituting $a_1, a_2, \ldots , a_N$ for the indeterminates $x_1, x_2, \ldots , x_N$ in a polynomial $f \in \mathcal{P}$. 

Roughly speaking, the group $S_N$ is thus acting on $\mathcal{P}$ by permuting variables: A permutation $\sigma \in S_N$ transforms a polynomial $f$ by substituting $x_{\sigma (i)}$ for each $x_i$. 

Note that this action of $S_N$ on $\mathcal{P}$ is a well-defined group action (as we will see in Proposition~ \ref{prop.sf.SN-acts} below). \medskip 

\textbf{(c)} A polynomial $f \in \mathcal{P}$ is said to be \emph{symmetric} if it satisfies 

\[  \sigma \cdot f = f \quad \text{for all } \sigma \in S_N.  \]

\textbf{(d)} We let $\mathcal{S}$ be the set of all symmetric polynomials $f \in \mathcal{P}$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.ring-of-symm
def.sf.ring-of-symm

The $K$-subalgebra $\mathcal{S}$ of $\mathcal{P}$ is called the \emph{ring of symmetric polynomials in} $N$ \emph{variables over} $K$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.schur
def.sf.schur

Let $\lambda $ be an $N$-partition. We define the \emph{Schur polynomial} $s_{\lambda }\in \mathcal{P}$ by

\[  s_{\lambda }:=\sum _{T\in \operatorname *{SSYT}\left( \lambda \right) }x_{T}.  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.skew-diag
def.sf.skew-diag

Let $\lambda $ and $\mu $ be two $N$-partitions such that $\mu \subseteq \lambda $. Then, we define the \emph{skew Young diagram} $Y\left( \lambda /\mu \right) $ to be the set difference

\begin{align*}  Y\left( \lambda \right) \setminus Y\left( \mu \right) &  =\left\{  \left( i,j\right) \  \mid \  i\in \left[ N\right] \text{ and }j\in \left[ \lambda _{i}\right] \setminus \left[ \mu _{i}\right] \right\}  \\ &  =\left\{  \left( i,j\right) \  \mid \  i\in \left[ N\right] \text{ and }j\in \mathbb {Z}\text{ and }\mu _{i}<j\leq \lambda _{i}\right\}  . \end{align*}

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

## VERDICT
{
  "verdict": "faithful",
  "justification": "Both declarations directly formalize the two Pieri rules. The binders `\u2200 {N : \u2115} {R : Type u_1} [CommRing R] (n : \u2115) (mu : SymmetricFunctions.NPartition N)` match \u201cLet n \u2208 \u2115. Let \u03bc be an N-partition\u201d in the intended polynomial ring over a commutative coefficient ring; quantifying over `N` and `R` merely makes the ambient setting explicit and general. For (a), `MvPolynomial.hsymm (Fin N) R n * ...` is the complete homogeneous polynomial `h_n` times `s_\u03bc`, while `horizontalNStripPartitions mu n` consists exactly of N-partitions \u03bb satisfying containment, `\u03bc_i \u2265 \u03bb_{i+1}`, and size difference n, hence exactly those for which \u201c\u03bb/\u03bc is a horizontal n-strip.\u201d For (b), `MvPolynomial.esymm (Fin N) R n * ...` is `e_n s_\u03bc`, and `verticalNStripPartitions mu n` consists exactly of N-partitions \u03bb satisfying containment, `\u03bb_i \u2264 \u03bc_i + 1`, and size difference n, hence exactly the vertical n-strips. Finally, `schur lam := \u2211 T \u2208 ssytFinset lam, T.toMonomial` agrees with the blueprint definition `s_\u03bb := \u2211_{T\u2208SSYT(\u03bb)} x_T`. Thus each finite sum has precisely the blueprint\u2019s index set and summand."
}