## TARGET SymmetricFunctions.pieri_vertical (theorem) — ELABORATED SIGNATURE
∀ {N : ℕ} {R : Type u_1} [inst : CommRing R] (n : ℕ) (mu : SymmetricFunctions.NPartition N),
  MvPolynomial.esymm (Fin N) R n * SymmetricFunctions.schur mu =
    ∑ lam ∈ SymmetricFunctions.verticalNStripPartitions mu n, SymmetricFunctions.schur lam

Docstring: Second Pieri rule (Theorem thm.sf.pieri(b))
Label: exe.sf.pieri

e_n · s_μ = ∑_{λ/μ is vertical n-strip} s_λ

where e_n is the n-th elementary symmetric polynomial.

This is Exercise exe.sf.pieri in the TeX source. The proof requires the
Robinson-Schensted-Knuth (RSK) column insertion bijection, or alternatively
can be derived from `pieri_horizontal` via the ω-involution. 

## TARGET SymmetricFunctions.pieri_horizontal (theorem) — ELABORATED SIGNATURE
∀ {N : ℕ} {R : Type u_1} [inst : CommRing R] (n : ℕ) (mu : SymmetricFunctions.NPartition N),
  MvPolynomial.hsymm (Fin N) R n * SymmetricFunctions.schur mu =
    ∑ lam ∈ SymmetricFunctions.horizontalNStripPartitions mu n, SymmetricFunctions.schur lam

Docstring: First Pieri rule (Theorem thm.sf.pieri(a))
Label: exe.sf.pieri

h_n · s_μ = ∑_{λ/μ is horizontal n-strip} s_λ

where h_n is the n-th complete homogeneous symmetric polynomial.

This is Exercise exe.sf.pieri in the TeX source. The proof requires the
Robinson-Schensted-Knuth (RSK) row insertion bijection, which is not yet
formalized in this project. 

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

## PROJECT DEPENDENCY SymmetricFunctions.isVerticalStripFun (def)
{N : ℕ} → (Fin N → ℕ) → (Fin N → ℕ) → Prop

Body:
fun {N} lam mu => ∀ (i : Fin N), lam i ≤ mu i + 1

Docstring: A skew partition λ/μ is a vertical strip if no two boxes lie in the same row.
Equivalently: λ_i ≤ μ_i + 1 for all i.

The argument order `(lam, mu)` matches standard mathematical notation λ/μ.

**Related definitions:**
- `SkewPartition.isVerticalStrip`: Bundled version for `SkewPartition N` 

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

## PROJECT DEPENDENCY SymmetricFunctions.instDecidableIsVerticalStripFun (def)
{N : ℕ} → (lam mu : Fin N → ℕ) → Decidable (SymmetricFunctions.isVerticalStripFun lam mu)

Body:
fun {N} lam mu => Fintype.decidableForallFintype

Docstring: Decidable instance for vertical strip predicate. 

## PROJECT DEPENDENCY SymmetricFunctions.instDecidableHasSizeDiff (def)
{N : ℕ} → (mu lam : Fin N → ℕ) → (n : ℕ) → Decidable (SymmetricFunctions.hasSizeDiff mu lam n)

Body:
fun {N} mu lam n => inferInstanceAs (Decidable (∑ i, lam i = ∑ i, mu i + n))

## PROJECT DEPENDENCY SymmetricFunctions.potentialVerticalStrips (def)
{N : ℕ} → SymmetricFunctions.NPartition N → Finset (Fin N → ℕ)

Body:
fun {N} mu => Fintype.piFinset fun i => Finset.Icc (mu.parts i) (SymmetricFunctions.verticalStripUpperBound mu i)

Docstring: A function from Fin N to ℕ that could potentially form a vertical n-strip with μ. 

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

## PROJECT DEPENDENCY SymmetricFunctions.isHorizontalStripFun (def)
{N : ℕ} → (Fin N → ℕ) → (Fin N → ℕ) → Prop

Body:
fun {N} lam mu => ∀ (i : Fin N) (hi : ↑i + 1 < N), mu i ≥ lam ⟨↑i + 1, hi⟩

Docstring: A skew partition λ/μ is a horizontal strip if no two boxes lie in the same column.
Equivalently: μ_i ≥ λ_{i+1} for all i.

The argument order `(lam, mu)` matches standard mathematical notation λ/μ.

**Related definitions:**
- `SkewPartition.isHorizontalStrip`: Bundled version for `SkewPartition N` 

## PROJECT DEPENDENCY SymmetricFunctions.instDecidableIsHorizontalStripFun (def)
{N : ℕ} → (lam mu : Fin N → ℕ) → Decidable (SymmetricFunctions.isHorizontalStripFun lam mu)

Body:
fun {N} lam mu => Fintype.decidableForallFintype

Docstring: Decidable instance for horizontal strip predicate. 

## PROJECT DEPENDENCY SymmetricFunctions.potentialHorizontalStrips (def)
{N : ℕ} → SymmetricFunctions.NPartition N → ℕ → Finset (Fin N → ℕ)

Body:
fun {N} mu n => Fintype.piFinset fun i => Finset.Icc (mu.parts i) (SymmetricFunctions.horizontalStripUpperBound mu n i)

Docstring: A function from Fin N to ℕ that could potentially form a horizontal n-strip with μ.
This is the set of all functions bounded by the horizontal strip constraints. 

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

## PROJECT DEPENDENCY SymmetricFunctions.verticalStripUpperBound (def)
{N : ℕ} → SymmetricFunctions.NPartition N → Fin N → ℕ

Body:
fun {N} mu i => mu.parts i + 1

Docstring: The bound for each λ_i when forming a vertical strip with μ.
λ_i must satisfy μ_i ≤ λ_i ≤ μ_i + 1 (vertical strip condition). 

## PROJECT DEPENDENCY SymmetricFunctions.NPartition.mk (constructor)
{N : ℕ} → (parts : Fin N → ℕ) → (∀ (i j : Fin N), i ≤ j → parts j ≤ parts i) → SymmetricFunctions.NPartition N

## PROJECT DEPENDENCY SymmetricFunctions.horizontalStripUpperBound (def)
{N : ℕ} → SymmetricFunctions.NPartition N → ℕ → Fin N → ℕ

Body:
fun {N} mu n i => if h : ↑i = 0 then mu.parts ⟨0, ⋯⟩ + n else mu.parts ⟨↑i - 1, ⋯⟩

Docstring: The bound for each λ_i when forming a horizontal strip with μ.
λ_i must satisfy μ_i ≤ λ_i ≤ bound_i where:
- For i = 0: bound_0 = μ_0 + n (since |λ| - |μ| = n and all parts are bounded by λ_0)
- For i > 0: bound_i = μ_{i-1} (horizontal strip condition: μ_{i-1} ≥ λ_i) 

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

## BASE-LIBRARY REF CommRing
Type u → Type u

Docstring: A commutative ring is a ring with commutative multiplication. 

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


## BASE-LIBRARY REF CommRing.mul_comm
∀ {α : Type u} [self : CommRing α] (a b : α), a * b = b * a

Docstring: Multiplication is commutative in a commutative multiplicative magma. 

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

## BASE-LIBRARY REF NonUnitalNonAssocSemiring
Type u → Type u

Docstring: A not-necessarily-unital, not-necessarily-associative semiring. See `CommutatorRing` and the
documentation thereof in case you need a `NonUnitalNonAssocSemiring` instance on a Lie ring
or a Lie algebra. 

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.left_distrib
∀ {α : Type u} [self : NonUnitalNonAssocSemiring α] (a b c : α), a * (b + c) = a * b + a * c

Docstring: Multiplication is left distributive over addition 

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.right_distrib
∀ {α : Type u} [self : NonUnitalNonAssocSemiring α] (a b c : α), (a + b) * c = a * c + b * c

Docstring: Multiplication is right distributive over addition 

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

## BASE-LIBRARY REF CommRing.toNonUnitalCommRing._proof_1
∀ {α : Type u_1} [s : CommRing α] (a b : α), a - b = a + -b

## BASE-LIBRARY REF MvPolynomial.esymm
(σ : Type u_5) → (R : Type u_6) → [inst : CommSemiring R] → [Fintype σ] → ℕ → MvPolynomial σ R

Body:
fun σ R [CommSemiring R] [Fintype σ] n => ∑ t ∈ Finset.powersetCard n Finset.univ, ∏ i ∈ t, MvPolynomial.X i

Docstring: The `n`th elementary symmetric `MvPolynomial σ R`.
It is the sum over all the degree n squarefree monomials in `MvPolynomial σ R`. 

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

## BASE-LIBRARY REF Finset.sum
{ι : Type u_1} → {M : Type u_3} → [AddCommMonoid M] → Finset ι → (ι → M) → M

Body:
fun {ι} {M} [AddCommMonoid M] s f => (Multiset.map f s.val).sum

Docstring: `∑ x ∈ s, f x` is the sum of `f x` as `x` ranges over the elements
of the finite set `s`.

When the index type is a `Fintype`, the notation `∑ x, f x`, is a shorthand for
`∑ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF MvPolynomial.hsymm
(σ : Type u_5) → (R : Type u_6) → [inst : CommSemiring R] → [Fintype σ] → [DecidableEq σ] → ℕ → MvPolynomial σ R

Body:
fun σ R [CommSemiring R] [Fintype σ] [DecidableEq σ] n => ∑ s, (Multiset.map MvPolynomial.X ↑s).prod

Docstring: The `n`th complete homogeneous symmetric `MvPolynomial σ R`.
It is the sum over all the degree n monomials in `MvPolynomial σ R`. 

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


## BASE-LIBRARY REF decEq
{α : Sort u} → [inst : DecidableEq α] → (a b : α) → Decidable (a = b)

Body:
fun {α} [inst : DecidableEq α] a b => inst a b

Docstring: Checks whether two terms of a type are equal using the type's `DecidableEq` instance.


## BASE-LIBRARY REF Fin.eq_of_val_eq
∀ {n : ℕ} {i j : Fin n}, ↑i = ↑j → i = j

## BASE-LIBRARY REF instDecidableEqFin._proof_1
∀ (n : ℕ) (i j : Fin n), ¬↑i = ↑j → i = j → False

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

## BASE-LIBRARY REF Nat.instMulZeroClass
MulZeroClass ℕ

Body:
{ toMul := instMulNat, toZero := Nat.instAddMonoid.toAddZeroClass.toZero, zero_mul := Nat.zero_mul,
  mul_zero := Nat.mul_zero }

## BASE-LIBRARY REF Finsupp.instAddCommMonoid
{ι : Type u_1} → {M : Type u_3} → [inst : AddCommMonoid M] → AddCommMonoid (ι →₀ M)

Body:
fun {ι} {M} [AddCommMonoid M] => { toAddMonoid := Finsupp.instAddMonoid, add_comm := ⋯ }

## BASE-LIBRARY REF Nat.instAddCommMonoid
AddCommMonoid ℕ

Body:
inferInstance

## BASE-LIBRARY REF Finset
Type u_4 → Type u_4

Docstring: `Finset α` is the type of finite sets of elements of `α`. It is implemented
as a multiset (a list up to permutation) which has no duplicate elements. 

## BASE-LIBRARY REF Finset.image
{α : Type u_1} → {β : Type u_2} → [DecidableEq β] → (α → β) → Finset α → Finset β

Body:
fun {α} {β} [DecidableEq β] f s => (Multiset.map f s.val).toFinset

Docstring: `image f s` is the forward image of `s` under `f`. 

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

## BASE-LIBRARY REF instDecidableAnd.match_1
{q : Prop} →
  (motive : Decidable q → Sort u_1) →
    (dq : Decidable q) → ((hq : q) → motive (isTrue hq)) → ((hq : ¬q) → motive (isFalse hq)) → motive dq

Body:
fun {q} motive dq h_1 h_2 => Decidable.casesOn dq (fun h => h_2 h) fun h => h_1 h

## BASE-LIBRARY REF instDecidableAnd._proof_1
∀ {p q : Prop}, ¬q → p ∧ q → False

## BASE-LIBRARY REF instDecidableAnd._proof_2
∀ {p q : Prop}, ¬p → p ∧ q → False

## BASE-LIBRARY REF Finset.attach
{α : Type u_1} → (s : Finset α) → Finset { x // x ∈ s }

Body:
fun {α} s => { val := s.val.attach, nodup := ⋯ }

Docstring: `attach s` takes the elements of `s` and forms a new set of elements of the subtype
`{x // x ∈ s}`. 

## BASE-LIBRARY REF Nat.lt
ℕ → ℕ → Prop

Body:
fun n m => n.succ.le m

Docstring: Strict inequality of natural numbers, usually accessed via the `<` operator.

It is defined as `n < m = n + 1 ≤ m`.


## BASE-LIBRARY REF Add
Type u → Type u

Docstring: The homogeneous version of `HAdd`: `a + b : α` where `a b : α`. 

## BASE-LIBRARY REF Add.add
{α : Type u} → [self : Add α] → α → α → α

Body:
fun α [self : Add α] => self.1

Docstring: `a + b` computes the sum of `a` and `b`. See `HAdd`. 

## BASE-LIBRARY REF Nat.add
ℕ → ℕ → ℕ

Body:
fun x x_1 =>
  Nat.brecOn (motive := fun x => ℕ → ℕ) x_1
    (fun x f x_2 =>
      (match (motive := ℕ → (x : ℕ) → Nat.below (motive := fun x => ℕ → ℕ) x → ℕ) x_2, x with
        | a, Nat.zero => fun x => a
        | a, b.succ => fun x => (x.1 a).succ)
        f)
    x

Docstring: Addition of natural numbers, typically used via the `+` operator.

This function is overridden in both the kernel and the compiler to efficiently evaluate using the
arbitrary-precision arithmetic library. The definition provided here is the logical model.


## BASE-LIBRARY REF Finset.map
{α : Type u_1} → {β : Type u_2} → (α ↪ β) → Finset α → Finset β

Body:
fun {α} {β} f s => { val := Multiset.map (⇑f) s.val, nodup := ⋯ }

Docstring: When `f` is an embedding of `α` in `β` and `s` is a finset in `α`, then `s.map f` is the image
finset in `β`. The embedding condition guarantees that there are no duplicates in the image. 

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

## BASE-LIBRARY REF Finset.univ
{α : Type u_1} → [Fintype α] → Finset α

Body:
fun {α} [Fintype α] => Fintype.elems

Docstring: `univ` is the universal finite set of type `Finset α` implied from
the assumption `Fintype α`. 

## BASE-LIBRARY REF MvPolynomial.X
{R : Type u} → {σ : Type u_1} → [inst : CommSemiring R] → σ → MvPolynomial σ R

Body:
fun {R} {σ} [CommSemiring R] n => (MvPolynomial.monomial fun₀ | n => 1) 1

Docstring: `X n` is the degree `1` monomial $X_n$. 

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

## BASE-LIBRARY REF Nat.decidableForallFin
{n : ℕ} → (P : Fin n → Prop) → [DecidablePred P] → Decidable (∀ (i : Fin n), P i)

Body:
fun {n} P [DecidablePred P] => decidable_of_iff (∀ (k : ℕ) (h : k < n), P ⟨k, h⟩) ⋯

## BASE-LIBRARY REF Nat.decidableForallFin._proof_1
∀ {n : ℕ} (P : Fin n → Prop), (∀ (k : ℕ) (h : k < n), P ⟨k, h⟩) ↔ ∀ (i : Fin n), P i

## BASE-LIBRARY REF Nat.decidableBallLT
(n : ℕ) →
  (P : (k : ℕ) → k < n → Prop) →
    [(n_1 : ℕ) → (h : n_1 < n) → Decidable (P n_1 h)] → Decidable (∀ (n_1 : ℕ) (h : n_1 < n), P n_1 h)

Body:
fun x x_1 x_2 =>
  Nat.brecOn (motive := fun x =>
    (x_3 : (k : ℕ) → k < x → Prop) →
      ((n : ℕ) → (h : n < x) → Decidable (x_3 n h)) → Decidable (∀ (n : ℕ) (h : n < x), x_3 n h))
    x
    (fun x f x_3 x_4 =>
      (match (motive :=
          (x : ℕ) →
            (x_5 : (k : ℕ) → k < x → Prop) →
              ((n : ℕ) → (h : n < x) → Decidable (x_5 n h)) →
                Nat.below (motive := fun x =>
                    (x_7 : (k : ℕ) → k < x → Prop) →
                      ((n : ℕ) → (h : n < x) → Decidable (x_7 n h)) → Decidable (∀ (n : ℕ) (h : n < x), x_7 n h))
                    x …

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


## BASE-LIBRARY REF inferInstanceAs
(α : Sort u) → [i : α] → α

Body:
fun α [i : α] => i

Docstring: `inferInstanceAs α` synthesizes a value of any target type by typeclass
inference. This is just like `inferInstance` except that `α` is given
explicitly instead of being inferred from the target type. It is especially
useful when the target type is some `α'` which is definitionally equal to `α`,
but the instance we are looking for is only registered for `α` (because
typeclass search does not unfold most definitions, but definitional equality
does.) Example:
```
#check inferInstanceAs (Inhabited Nat) -- Inhabited Nat
```


## BASE-LIBRARY REF Fintype.piFinset
{α : Type u_1} → [DecidableEq α] → [Fintype α] → {δ : α → Type u_4} → ((a : α) → Finset (δ a)) → Finset ((a : α) → δ a)

Body:
fun {α} [DecidableEq α] [Fintype α] {δ} t => Finset.map { toFun := fun f a => f a ⋯, inj' := ⋯ } (Finset.univ.pi t)

Docstring: Given for all `a : α` a finset `t a` of `δ a`, then one can define the
finset `Fintype.piFinset t` of all functions taking values in `t a` for all `a`. This is the
analogue of `Finset.pi` where the base finset is `univ` (but formally they are not the same, as
there is an additional condition `i ∈ Finset.univ` in the `Finset.pi` definition). 

## BASE-LIBRARY REF Finset.Icc
{α : Type u_1} → [inst : Preorder α] → [LocallyFiniteOrder α] → α → α → Finset α

Body:
fun {α} [Preorder α] [LocallyFiniteOrder α] a b => LocallyFiniteOrder.finsetIcc a b

Docstring: The finset $[a, b]$ of elements `x` such that `a ≤ x` and `x ≤ b`. Basically `Set.Icc a b` as a
finset. 

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

## BASE-LIBRARY REF Nat.instLocallyFiniteOrder
LocallyFiniteOrder ℕ

Body:
{ finsetIcc := fun a b => { val := ↑(List.range' a (b + 1 - a)), nodup := ⋯ },
  finsetIco := fun a b => { val := ↑(List.range' a (b - a)), nodup := ⋯ },
  finsetIoc := fun a b => { val := ↑(List.range' (a + 1) (b - a)), nodup := ⋯ },
  finsetIoo := fun a b => { val := ↑(List.range' (a + 1) (b - a - 1)), nodup := ⋯ }, finset_mem_Icc := ⋯,
  finset_mem_Ico := ⋯, finset_mem_Ioc := ⋯, finset_mem_Ioo := ⋯ }

## BASE-LIBRARY REF List.range'
ℕ → ℕ → optParam ℕ 1 → List ℕ

Docstring: Returns a list of the numbers with the given length `len`, starting at `start` and increasing by
`step` at each element.

In other words, `List.range' start len step` is `[start, start+step, ..., start+(len-1)*step]`.

Examples:
 * `List.range' 0 3 (step := 1) = [0, 1, 2]`
 * `List.range' 0 3 (step := 2) = [0, 2, 4]`
 * `List.range' 0 4 (step := 2) = [0, 2, 4, 6]`
 * `List.range' 3 4 (step := 2) = [3, 5, 7, 9]`


## BASE-LIBRARY REF instSubNat
Sub ℕ

Body:
{ sub := Nat.sub }

Characterization: Natural subtraction truncates: `a - b = 0` whenever `b ≥ a`.

## BASE-LIBRARY REF Nat.instLocallyFiniteOrder._proof_10
∀ (a b : ℕ), (List.range' a (b + 1 - a)).Nodup

## BASE-LIBRARY REF Nat.instLocallyFiniteOrder._proof_11
∀ (a b : ℕ), (List.range' a (b - a)).Nodup

## BASE-LIBRARY REF Nat.instLocallyFiniteOrder._proof_12
∀ (a b : ℕ), (List.range' (a + 1) (b - a)).Nodup

## BASE-LIBRARY REF Nat.instLocallyFiniteOrder._proof_13
∀ (a b : ℕ), (List.range' (a + 1) (b - a - 1)).Nodup

## BASE-LIBRARY REF Nat.instLocallyFiniteOrder._proof_3
∀ (a b x : ℕ), x ∈ { val := ↑(List.range' a (b + 1 - a)), nodup := ⋯ } ↔ a ≤ x ∧ x ≤ b

## BASE-LIBRARY REF Nat.instLocallyFiniteOrder._proof_5
∀ (a b x : ℕ), x ∈ { val := ↑(List.range' a (b - a)), nodup := ⋯ } ↔ a ≤ x ∧ x < b

## BASE-LIBRARY REF Nat.instLocallyFiniteOrder._proof_7
∀ (a b x : ℕ), x ∈ { val := ↑(List.range' (a + 1) (b - a)), nodup := ⋯ } ↔ a < x ∧ x ≤ b

## BASE-LIBRARY REF Fintype.decidablePiFintype
{α : Type u_5} → {β : α → Type u_4} → [(a : α) → DecidableEq (β a)] → [Fintype α] → DecidableEq ((a : α) → β a)

Body:
fun {α} {β} [(a : α) → DecidableEq (β a)] [Fintype α] f g => decidable_of_iff (∀ a ∈ Finset.univ, f a = g a) ⋯

## BASE-LIBRARY REF Fintype.decidablePiFintype._proof_2
∀ {α : Type u_1} {β : α → Type u_2} [inst : Fintype α] (f g : (a : α) → β a), (∀ a ∈ Finset.univ, f a = g a) ↔ f = g

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


## BASE-LIBRARY REF Pi.instFintype
{α : Type u_3} →
  {β : α → Type u_4} → [DecidableEq α] → [Fintype α] → [(a : α) → Fintype (β a)] → Fintype ((a : α) → β a)

Body:
fun {α} {β} [DecidableEq α] [Fintype α] [(a : α) → Fintype (β a)] =>
  { elems := Fintype.piFinset fun x => Finset.univ, complete := ⋯ }

Docstring: A dependent product of fintypes, indexed by a fintype, is a fintype. 

## BASE-LIBRARY REF Fin.decLt
{n : ℕ} → (a b : Fin n) → Decidable (a < b)

Body:
fun {n} a b => (↑a).decLt ↑b

## INFORMAL STATEMENT
Pieri rules

Let $n\in \mathbb {N}$. Let $\mu $ be an $N$-partition. Then: 

\textbf{(a)} We have

\[  h_{n}s_{\mu }=\sum _{\substack {\lambda \text{ is an }N\text{-partition;}\\ \lambda /\mu \text{ is a horizontal }n\text{-strip}}}s_{\lambda }.  \]

\textbf{(b)} We have

\[  e_{n}s_{\mu }=\sum _{\substack {\lambda \text{ is an }N\text{-partition;}\\ \lambda /\mu \text{ is a vertical }n\text{-strip}}}s_{\lambda }.  \]

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.npar-order
def.sf.Npar-order

\leanhelper  We define a partial order on $N$-partitions by componentwise comparison: $\mu \leq \nu $ iff $\mu _i \leq \nu _i$ for all $i \in [N]$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.par-subset
def.sf.par-subset

Let $\lambda $ and $\mu $ be two $N$-partitions. 

We say that $\mu \subseteq \lambda $ if and only if $Y\left( \mu \right) \subseteq Y\left( \lambda \right) $. Equivalently, $\mu \subseteq \lambda $ if and only if

\[  \text{each }i\in \left[ N\right] \text{ satisfies }\mu _{i}\leq \lambda _{i}.  \]

 Thus we have defined a partial order $\subseteq $ on the set of all $N$-partitions.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.skew-diag
def.sf.skew-diag

Let $\lambda $ and $\mu $ be two $N$-partitions such that $\mu \subseteq \lambda $. Then, we define the \emph{skew Young diagram} $Y\left( \lambda /\mu \right) $ to be the set difference

\begin{align*}  Y\left( \lambda \right) \setminus Y\left( \mu \right) &  =\left\{  \left( i,j\right) \  \mid \  i\in \left[ N\right] \text{ and }j\in \left[ \lambda _{i}\right] \setminus \left[ \mu _{i}\right] \right\}  \\ &  =\left\{  \left( i,j\right) \  \mid \  i\in \left[ N\right] \text{ and }j\in \mathbb {Z}\text{ and }\mu _{i}<j\leq \lambda _{i}\right\}  . \end{align*}

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

## VERDICT
{
  "verdict": "faithful",
  "discrepancies": [],
  "justification": "Both target declarations exactly express the two Pieri identities. For (a), the formal left side is `MvPolynomial.hsymm (Fin N) R n * SymmetricFunctions.schur mu`, matching informal `h_n s_\u03bc`; `MvPolynomial.hsymm` is explicitly \u201cthe sum over all the degree n monomials,\u201d and `schur` is the tableau definition of `s_\u03bc`. The index set `horizontalNStripPartitions mu n` filters N-partitions satisfying containment, `isHorizontalStripFun f mu.parts` (the condition `\u03bc_i \u2265 \u03bb_{i+1}`), and `hasSizeDiff mu.parts f n` (`|\u03bb| = |\u03bc| + n`), exactly matching \u201c`\u03bb/\u03bc` is a horizontal n-strip.\u201d For (b), `MvPolynomial.esymm (Fin N) R n` is the sum of degree-n squarefree monomials, matching `e_n`, while `verticalNStripPartitions mu n` imposes containment, `\u03bb_i \u2264 \u03bc_i + 1`, and size difference n, exactly matching a vertical n-strip. `NPartition` is a weakly decreasing `Fin N \u2192 \u2115`, which is merely the zero-based Lean encoding of the informal weakly decreasing N-tuple. Quantification over an arbitrary commutative coefficient ring is a valid generalization of the polynomial identities, not a restriction."
}