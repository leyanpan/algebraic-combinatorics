## TARGET SymmetricFunctions.jacobiTrudi_h (theorem) — ELABORATED SIGNATURE
∀ {N : ℕ} {R : Type u_1} [inst : CommRing R] (lam mu : Fin N → ℕ) (hlam : ∀ (i j : Fin N), i ≤ j → lam j ≤ lam i)
  (hmu : ∀ (i j : Fin N), i ≤ j → mu j ≤ mu i) (hcontained : ∀ (i : Fin N), mu i ≤ lam i),
  SymmetricFunctions.skewSchur
      { outer := { parts := lam, weaklyDecreasing := hlam }, inner := { parts := mu, weaklyDecreasing := hmu },
        contained := ⋯ } =
    (SymmetricFunctions.jacobiTrudiMatrixH lam mu).det

Docstring: First Jacobi-Trudi formula (Theorem thm.sf.jt-h)
Label: thm.sf.jt-h

s_{λ/μ} = det((h_{λᵢ - μⱼ - i + j})_{1 ≤ i,j ≤ M})

The proof uses the Lindström-Gessel-Viennot lemma with appropriate
source and target vertices in the integer lattice ℤ².

## Proof Strategy

**Step 1: Set up the LGV framework**
Define source vertices Aᵢ = (μᵢ - i, 1) and target vertices Bⱼ = (λⱼ - j, N) in ℤ².
The path weight matrix M_{i,j} = ∑_{p : Aᵢ → Bⱼ} w(p) where w(p) is the product
of x_h for each east-step at height h.

**Step 2: Identify M with the Jacobi-Trudi matrix**
By `pathWeightSum_eq_hsymm`, M_{i,j} = h_{λⱼ - μᵢ - j + i} = h_{λⱼ - μᵢ - (j - i)}.
Note: The textbook uses 1-indexed notation; our Lean formalization uses 0-indexed.
The matrix entry (i,j) is h_{λᵢ - μⱼ - i + j} in the textbook convention.

**Step 3: Apply the LGV lemma**
By `lgv_nonpermutable` (Corollary cor.lgv.kpaths.wt-np), since the source and
target vertices satisfy the sorting conditions (x-decreasing, y-increasing),
we have:
  det(M) = ∑_{nipats from 𝐀 to 𝐁} w(nipat)
where the sum is only over non-intersecting path tuples (nipats).

**Step 4: Establish the nipat-SSYT bijection**
By `nipat_ssyt_bijection`, there is a weight-preserving bijection between
nipats from 𝐀 to 𝐁 and SSYT of skew shape λ/μ:
- The nipat (p₁, ..., pₖ) maps to the tableau T where row i contains
  the heights of east-steps in path pᵢ (in weakly increasing order).
- Non-intersection of paths ensures column-strictness of the tableau.
- The weight w(nipat) = ∏ᵢ w(pᵢ) equals the monomial x^T.

**Step 5: Conclude**
det(M) = ∑_{nipats} w(nipat) = ∑_{SSYT T of shape λ/μ} x^T = s_{λ/μ}

## Key Lemmas Required

1. `pathWeightSum_eq_hsymm`: Path weight sums equal h_n (Observation 1)
2. `nipat_ssyt_bijection`: Bijection between nipats and SSYT (Observation 2)
3. `lgv_nonpermutable`: LGV lemma for sorted vertices (from LGV2.lean)
4. Sorting conditions on A and B vertices (follows from partition monotonicity)

## References
- TeX source: AlgebraicCombinatorics/tex/SymmetricFunctions/PieriJacobiTrudi.tex
- LGV infrastructure: AlgebraicCombinatorics/Determinants/LGV2.lean


## PROJECT DEPENDENCY SymmetricFunctions.skewSchur (def)
{N : ℕ} → {R : Type u_1} → [inst : CommRing R] → SymmetricFunctions.SkewPartition N → MvPolynomial (Fin N) R

Body:
fun {N} {R} [CommRing R] s => ∑ T ∈ SymmetricFunctions.skewSSYTFinset s, T.toMonomial

Docstring: The skew Schur polynomial s_{λ/μ} defined as the sum over all skew SSYT.
Definition def.sf.skew-schur. 

## PROJECT DEPENDENCY SymmetricFunctions.SkewPartition.mk (constructor)
{N : ℕ} → (outer inner : SymmetricFunctions.NPartition N) → inner ≤ outer → SymmetricFunctions.SkewPartition N

## PROJECT DEPENDENCY SymmetricFunctions.NPartition.mk (constructor)
{N : ℕ} → (parts : Fin N → ℕ) → (∀ (i j : Fin N), i ≤ j → parts j ≤ parts i) → SymmetricFunctions.NPartition N

## PROJECT DEPENDENCY AlgebraicCombinatorics.SymmetricPolynomials.P_isCommRing' (def)
{K : Type u_1} → [inst : CommRing K] → {N : ℕ} → CommRing (AlgebraicCombinatorics.SymmetricPolynomials.P K N)

Body:
fun {K} [CommRing K] {N} => inferInstance

Docstring: The polynomial ring P K N is a commutative K-algebra.
Label: def.sf.PS 

## PROJECT DEPENDENCY SymmetricFunctions.jacobiTrudiMatrixH (def)
{N : ℕ} →
  {R : Type u_1} → [inst : CommRing R] → (Fin N → ℕ) → (Fin N → ℕ) → Matrix (Fin N) (Fin N) (MvPolynomial (Fin N) R)

Body:
fun {N} {R} [CommRing R] lam mu => Matrix.of fun i j => SymmetricFunctions.hsymmExt (↑(lam i) - ↑(mu j) - ↑↑i + ↑↑j)

Docstring: The Jacobi-Trudi matrix for h (first Jacobi-Trudi formula).
Entry (i,j) is h_{λᵢ - μⱼ - i + j}. 

## PROJECT DEPENDENCY SymmetricFunctions.SkewPartition (inductive)
ℕ → Type

Body:
SymmetricFunctions.SkewPartition.mk : {N : ℕ} → (outer inner : SymmetricFunctions.NPartition N) → inner ≤ outer → SymmetricFunctions.SkewPartition N

Docstring: A skew partition λ/μ is a pair of N-partitions with μ ⊆ λ.
Definition def.sf.strips(a). 

## PROJECT DEPENDENCY SymmetricFunctions.SkewSSYT (inductive)
{N : ℕ} → SymmetricFunctions.SkewPartition N → Type

Body:
SymmetricFunctions.SkewSSYT.mk : {N : ℕ} →
  {s : SymmetricFunctions.SkewPartition N} →
    (entries : (i : Fin N) → Fin (s.outer.parts i - s.inner.parts i) → Fin N) →
      (∀ (i : Fin N) (j k : Fin (s.outer.parts i - s.inner.parts i)), j ≤ k → entries i j ≤ entries i k) →
        (∀ (i : Fin N) (hi : ↑i + 1 < N) (k : Fin (s.outer.parts i - s.inner.parts i)),
            s.inner.parts i + ↑k + 1 > s.inner.parts ⟨↑i + 1, hi⟩ ∧
                s.inner.parts i + ↑k + 1 ≤ s.outer.parts ⟨↑i + 1, hi⟩ →
              let k' := s.inner.parts i + ↑k - s.inner.parts ⟨↑i + 1, hi⟩;
              ∀ (hk' : k' < s.outer.parts ⟨↑i + 1, hi⟩ - s.inner.parts ⟨↑i + 1, hi⟩),
                entries i k < entries ⟨↑i + 1, hi⟩ ⟨k', hk'⟩) →
          SymmetricFunctions.SkewSSYT s

Docstring: A semistandard Young tableau of skew shape λ/μ with entries in [N].
Definition def.sf.skew-schur.

For a skew tableau, the column-strict condition requires that entries
are strictly increasing down columns, where column j of Y(λ/μ) consists
of boxes (i, j) with μᵢ < j ≤ λᵢ.

**Note:** This is one of two SkewSSYT definitions in this project:
- **This definition** (`SymmetricFunctions.SkewSSYT`): Uses dependent types. Takes
  `s : SkewPartition N` as a single bundled argument. No `[NeZero N]` requirement.
  Field names: `rowWeak`, `colStrict`.
- **Alternative definition** (`SchurBasics.SkewSSYT` in `SchurBasics.lean`): Uses
  `entry : Fin N × ℕ → Fin N` with a support condition. Extends `SkewYoungTableau`.
  Takes `lam mu : NPartition N` as separate arguments. Requires `[NeZero N]`.
  Field names: `row_weak`, `col_strict`.

See `SSYTEquiv.lean` for conversions between representations. 

## PROJECT DEPENDENCY SymmetricFunctions.skewSSYTFinset (def)
{N : ℕ} → (s : SymmetricFunctions.SkewPartition N) → Finset (SymmetricFunctions.SkewSSYT s)

Body:
fun {N} s =>
  Finset.map
    {
      toFun := fun x =>
        match x with
        | ⟨f, hf⟩ => SymmetricFunctions.fillingToSkewSSYT f ⋯,
      inj' := ⋯ }
    (SymmetricFunctions.ssytFillingFinset s).attach

Docstring: The set of all skew SSYT of shape λ/μ.
This is finite because it's a subset of all fillings, which is finite. 

## PROJECT DEPENDENCY SymmetricFunctions.SkewSSYT.toMonomial (def)
{N : ℕ} →
  {R : Type u_1} →
    [inst : CommRing R] →
      {s : SymmetricFunctions.SkewPartition N} → SymmetricFunctions.SkewSSYT s → MvPolynomial (Fin N) R

Body:
fun {N} {R} [CommRing R] {s} T => ∏ i, ∏ j, MvPolynomial.X (T.entries i j)

Docstring: The monomial x^T associated to a skew tableau T. 

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

## PROJECT DEPENDENCY SymmetricFunctions.NPartition.instLE (def)
{N : ℕ} → LE (SymmetricFunctions.NPartition N)

Body:
fun {N} => { le := SymmetricFunctions.NPartition.partLE }

## PROJECT DEPENDENCY AlgebraicCombinatorics.SymmetricPolynomials.P (def)
(K : Type u_2) → [CommRing K] → ℕ → Type u_2

Body:
fun K [CommRing K] N => MvPolynomial (Fin N) K

Docstring: The polynomial ring in N variables over K.
This corresponds to 𝒫 in the source (Definition def.sf.PS (a)).
Label: def.sf.PS 

## PROJECT DEPENDENCY SymmetricFunctions.hsymmExt (def)
{N : ℕ} → {R : Type u_1} → [inst : CommRing R] → ℤ → MvPolynomial (Fin N) R

Body:
fun {N} {R} [CommRing R] n => if 0 ≤ n then MvPolynomial.hsymm (Fin N) R n.toNat else 0

Docstring: Extended h_n: h_n = 0 for n < 0, h_0 = 1.
This is needed since the Jacobi-Trudi formula may have negative indices. 

## PROJECT DEPENDENCY SymmetricFunctions.NPartition.parts (def)
{N : ℕ} → SymmetricFunctions.NPartition N → Fin N → ℕ

Body:
fun N self => self.1

Docstring: The parts of the partition 

## PROJECT DEPENDENCY SymmetricFunctions.SkewPartition.outer (def)
{N : ℕ} → SymmetricFunctions.SkewPartition N → SymmetricFunctions.NPartition N

Body:
fun N self => self.1

Docstring: The outer partition λ 

## PROJECT DEPENDENCY SymmetricFunctions.SkewPartition.inner (def)
{N : ℕ} → SymmetricFunctions.SkewPartition N → SymmetricFunctions.NPartition N

Body:
fun N self => self.2

Docstring: The inner partition μ 

## PROJECT DEPENDENCY SymmetricFunctions.SkewFilling (def)
{N : ℕ} → SymmetricFunctions.SkewPartition N → Type

Body:
fun {N} s => (i : Fin N) → Fin (s.outer.parts i - s.inner.parts i) → Fin N

Docstring: A filling of a skew shape is a function assigning a value in Fin N to each cell.
We use `abbrev` instead of `def` to ensure type class inference can see through this. 

## PROJECT DEPENDENCY SymmetricFunctions.ssytFillingFinset (def)
{N : ℕ} → (s : SymmetricFunctions.SkewPartition N) → Finset (SymmetricFunctions.SkewFilling s)

Body:
fun {N} s => Finset.filter (SymmetricFunctions.isSSYTFilling s) Finset.univ

Docstring: The finite set of all fillings satisfying SSYT conditions. 

## PROJECT DEPENDENCY SymmetricFunctions.fillingToSkewSSYT (def)
{N : ℕ} →
  {s : SymmetricFunctions.SkewPartition N} →
    (f : SymmetricFunctions.SkewFilling s) → SymmetricFunctions.isSSYTFilling s f → SymmetricFunctions.SkewSSYT s

Body:
fun {N} {s} f hf => { entries := f, rowWeak := ⋯, colStrict := ⋯ }

Docstring: A filling satisfying SSYT conditions can be converted to a SkewSSYT. 

## PROJECT DEPENDENCY SymmetricFunctions.SkewSSYT.entries (def)
{N : ℕ} →
  {s : SymmetricFunctions.SkewPartition N} →
    SymmetricFunctions.SkewSSYT s → (i : Fin N) → Fin (s.outer.parts i - s.inner.parts i) → Fin N

Body:
fun N s self => self.1

Docstring: The entries of the tableau, only for boxes in Y(λ/μ).
Entry (i, k) corresponds to box (i, μᵢ + k + 1) in Y(λ/μ). 

## PROJECT DEPENDENCY SymmetricFunctions.NPartition.partLE (def)
{N : ℕ} → SymmetricFunctions.NPartition N → SymmetricFunctions.NPartition N → Prop

Body:
fun {N} mu lam => ∀ (i : Fin N), mu.parts i ≤ lam.parts i

Docstring: Containment of partitions: μ ⊆ λ means μᵢ ≤ λᵢ for all i 

## PROJECT DEPENDENCY SymmetricFunctions.isSSYTFilling (def)
{N : ℕ} → (s : SymmetricFunctions.SkewPartition N) → SymmetricFunctions.SkewFilling s → Prop

Body:
fun {N} s f => SymmetricFunctions.isRowWeak s f ∧ SymmetricFunctions.isColStrict s f

Docstring: Combined predicate for SSYT conditions. 

## PROJECT DEPENDENCY SymmetricFunctions.isSSYTFilling_decidable (def)
{N : ℕ} →
  (s : SymmetricFunctions.SkewPartition N) →
    (f : SymmetricFunctions.SkewFilling s) → Decidable (SymmetricFunctions.isSSYTFilling s f)

Body:
fun {N} s f => instDecidableAnd

Docstring: The SSYT predicate is decidable. 

## PROJECT DEPENDENCY SymmetricFunctions.skewFilling_fintype (def)
{N : ℕ} → (s : SymmetricFunctions.SkewPartition N) → Fintype (SymmetricFunctions.SkewFilling s)

Body:
fun {N} s => inferInstance

Docstring: The type of fillings of a skew shape is finite. 

## PROJECT DEPENDENCY SymmetricFunctions.SkewSSYT.mk (constructor)
{N : ℕ} →
  {s : SymmetricFunctions.SkewPartition N} →
    (entries : (i : Fin N) → Fin (s.outer.parts i - s.inner.parts i) → Fin N) →
      (∀ (i : Fin N) (j k : Fin (s.outer.parts i - s.inner.parts i)), j ≤ k → entries i j ≤ entries i k) →
        (∀ (i : Fin N) (hi : ↑i + 1 < N) (k : Fin (s.outer.parts i - s.inner.parts i)),
            s.inner.parts i + ↑k + 1 > s.inner.parts ⟨↑i + 1, hi⟩ ∧
                s.inner.parts i + ↑k + 1 ≤ s.outer.parts ⟨↑i + 1, hi⟩ →
              let k' := s.inner.parts i + ↑k - s.inner.parts ⟨↑i + 1, hi⟩;
              ∀ (hk' : k' < s.outer.parts ⟨↑i + 1, hi⟩ - s.inner.parts ⟨↑i + 1, hi⟩),
                entries i k < entries ⟨↑i + 1, hi⟩ ⟨k', hk'⟩) →
          SymmetricFunctions.SkewSSYT s

## PROJECT DEPENDENCY SymmetricFunctions.isRowWeak (def)
{N : ℕ} → (s : SymmetricFunctions.SkewPartition N) → SymmetricFunctions.SkewFilling s → Prop

Body:
fun {N} s f => ∀ (i : Fin N) (j k : Fin (s.outer.parts i - s.inner.parts i)), j ≤ k → f i j ≤ f i k

Docstring: Predicate for a filling satisfying the SSYT row-weak condition. 

## PROJECT DEPENDENCY SymmetricFunctions.isColStrict (def)
{N : ℕ} → (s : SymmetricFunctions.SkewPartition N) → SymmetricFunctions.SkewFilling s → Prop

Body:
fun {N} s f =>
  ∀ (i : Fin N) (hi : ↑i + 1 < N) (k : Fin (s.outer.parts i - s.inner.parts i)),
    s.inner.parts i + ↑k + 1 > s.inner.parts ⟨↑i + 1, hi⟩ ∧ s.inner.parts i + ↑k + 1 ≤ s.outer.parts ⟨↑i + 1, hi⟩ →
      have k' := s.inner.parts i + ↑k - s.inner.parts ⟨↑i + 1, hi⟩;
      ∀ (hk' : k' < s.outer.parts ⟨↑i + 1, hi⟩ - s.inner.parts ⟨↑i + 1, hi⟩), f i k < f ⟨↑i + 1, hi⟩ ⟨k', hk'⟩

Docstring: Predicate for a filling satisfying the SSYT column-strict condition.
This is a simplified version that checks the condition for adjacent rows. 

## PROJECT DEPENDENCY SymmetricFunctions.isRowWeak_decidable (def)
{N : ℕ} →
  (s : SymmetricFunctions.SkewPartition N) →
    (f : SymmetricFunctions.SkewFilling s) → Decidable (SymmetricFunctions.isRowWeak s f)

Body:
fun {N} s f => Fintype.decidableForallFintype

Docstring: The row-weak predicate is decidable. 

## PROJECT DEPENDENCY SymmetricFunctions.isColStrict_decidable (def)
{N : ℕ} →
  (s : SymmetricFunctions.SkewPartition N) →
    (f : SymmetricFunctions.SkewFilling s) → Decidable (SymmetricFunctions.isColStrict s f)

Body:
fun {N} s f => Fintype.decidableForallFintype

Docstring: The column-strict predicate is decidable. 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF CommRing
Type u → Type u

Docstring: A commutative ring is a ring with commutative multiplication. 

## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


## BASE-LIBRARY REF LE.le
{α : Type u} → [self : LE α] → α → α → Prop

Docstring: The less-equal relation: `x ≤ y` 

Conventions for notations in identifiers:

 * The recommended spelling of `≤` in identifiers is `le`.

 * The recommended spelling of `<=` in identifiers is `le` (prefer `≤` over `<=`).

## BASE-LIBRARY REF instLEFin
{n : ℕ} → LE (Fin n)

## BASE-LIBRARY REF instLENat
LE ℕ

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

## BASE-LIBRARY REF CommRing.toCommSemiring
{α : Type u} → [s : CommRing α] → CommSemiring α

## BASE-LIBRARY REF Matrix.det
{n : Type u_2} → [DecidableEq n] → [Fintype n] → {R : Type v} → [CommRing R] → Matrix n n R → R

Docstring: The determinant of a matrix given by the Leibniz formula. 

## BASE-LIBRARY REF instDecidableEqFin
(n : ℕ) → DecidableEq (Fin n)

## BASE-LIBRARY REF Fin.fintype
(n : ℕ) → Fintype (Fin n)

## BASE-LIBRARY REF Finset.sum
{ι : Type u_1} → {M : Type u_3} → [AddCommMonoid M] → Finset ι → (ι → M) → M

Docstring: `∑ x ∈ s, f x` is the sum of `f x` as `x` ranges over the elements
of the finite set `s`.

When the index type is a `Fintype`, the notation `∑ x, f x`, is a shorthand for
`∑ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.toAddCommMonoid
{α : Type u} → [self : NonUnitalNonAssocSemiring α] → AddCommMonoid α

## BASE-LIBRARY REF NonUnitalNonAssocRing.toNonUnitalNonAssocSemiring
{α : Type u} → [self : NonUnitalNonAssocRing α] → NonUnitalNonAssocSemiring α

## BASE-LIBRARY REF NonUnitalNonAssocCommRing.toNonUnitalNonAssocRing
{α : Type u} → [self : NonUnitalNonAssocCommRing α] → NonUnitalNonAssocRing α

## BASE-LIBRARY REF NonUnitalCommRing.toNonUnitalNonAssocCommRing
{α : Type u} → [self : NonUnitalCommRing α] → NonUnitalNonAssocCommRing α

## BASE-LIBRARY REF CommRing.toNonUnitalCommRing
{α : Type u} → [s : CommRing α] → NonUnitalCommRing α

## BASE-LIBRARY REF inferInstance
{α : Sort u} → [i : α] → α

Docstring: `inferInstance` synthesizes a value of any target type by typeclass
inference. This function has the same type signature as the identity
function, but the square brackets on the `[i : α]` argument means that it will
attempt to construct this argument by typeclass inference. (This will fail if
`α` is not a `class`.) Example:
```
#check (inferInstance : Inhabited Nat) -- Inhabited Nat

def foo : Inhabited (Nat × Nat) :=
  inferInstance

example : foo.default = (default, default) :=
  rfl
```


## BASE-LIBRARY REF MvPolynomial.instCommRingMvPolynomial
{R : Type u} → {σ : Type u_1} → [inst : CommRing R] → CommRing (MvPolynomial σ R)

## BASE-LIBRARY REF Matrix
Type u → Type u' → Type v → Type (max u u' v)

Docstring: `Matrix m n R` is the type of matrices with entries in `R`, whose rows are indexed by `m`
and whose columns are indexed by `n`. 

## BASE-LIBRARY REF DFunLike.coe
{F : Sort u_1} → {α : outParam (Sort u_2)} → {β : outParam (α → Sort u_3)} → [self : DFunLike F α β] → F → (a : α) → β a

Docstring: The coercion from `F` to a function. 

## BASE-LIBRARY REF Equiv
Sort u_1 → Sort u_2 → Sort (max (max 1 u_1) u_2)

Docstring: `α ≃ β` is the type of functions from `α → β` with a two-sided inverse. 

## BASE-LIBRARY REF EquivLike.toFunLike
{E : Sort u_1} → {α : Sort u_3} → {β : Sort u_4} → [EquivLike E α β] → FunLike E α β

## BASE-LIBRARY REF Equiv.instEquivLike
{α : Sort u} → {β : Sort v} → EquivLike (α ≃ β) α β

## BASE-LIBRARY REF Matrix.of
{m : Type u_2} → {n : Type u_3} → {α : Type v} → (m → n → α) ≃ Matrix m n α

Docstring: Cast a function into a matrix.

The two sides of the equivalence are definitionally equal types. We want to use an explicit cast
to distinguish the types because `Matrix` has different instances to pi types (such as `Pi.mul`,
which performs elementwise multiplication, vs `Matrix.mul`).

If you are defining a matrix, in terms of its entries, use `of (fun i j ↦ _)`. The
purpose of this approach is to ensure that terms of the form `(fun i j ↦ _) * (fun i j ↦ _)` do not
appear, as the type of `*` can be misleading.


## BASE-LIBRARY REF HAdd.hAdd
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HAdd α β γ] → α → β → γ

Docstring: `a + b` computes the sum of `a` and `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `+` in identifiers is `add`.

## BASE-LIBRARY REF Int
Type

Docstring: The integers.

This type is special-cased by the compiler and overridden with an efficient implementation. The
runtime has a special representation for `Int` that stores “small” signed numbers directly, while
larger numbers use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)). A “small number” is an integer that can be encoded with one fewer bits
than the platform's pointer size (i.e. 63 bits on 64-bit architectures and 31 bits on 32-bit
architectures).


## BASE-LIBRARY REF instHAdd
{α : Type u_1} → [Add α] → HAdd α α α

## BASE-LIBRARY REF Int.instAdd
Add ℤ

## BASE-LIBRARY REF HSub.hSub
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HSub α β γ] → α → β → γ

Docstring: `a - b` computes the difference of `a` and `b`.
The meaning of this notation is type-dependent.
* For natural numbers, this operator saturates at 0: `a - b = 0` when `a ≤ b`. 

Conventions for notations in identifiers:

 * The recommended spelling of `-` in identifiers is `sub` (when used as a binary operator).

## BASE-LIBRARY REF instHSub
{α : Type u_1} → [Sub α] → HSub α α α

## BASE-LIBRARY REF Int.instSub
Sub ℤ

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


## BASE-LIBRARY REF instNatCastInt
NatCast ℤ

## BASE-LIBRARY REF Fin.val
{n : ℕ} → Fin n → ℕ

Docstring: The number that is strictly less than `n`.

`Fin.val` is a coercion, so any `Fin n` can be used in a position where a `Nat` is expected.


## BASE-LIBRARY REF instSubNat
Sub ℕ

## BASE-LIBRARY REF LT.lt
{α : Type u} → [self : LT α] → α → α → Prop

Docstring: The less-than relation: `x < y` 

Conventions for notations in identifiers:

 * The recommended spelling of `<` in identifiers is `lt`.

## BASE-LIBRARY REF instLTNat
LT ℕ

## BASE-LIBRARY REF instAddNat
Add ℕ

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

## BASE-LIBRARY REF And
Prop → Prop → Prop

Docstring: `And a b`, or `a ∧ b`, is the conjunction of propositions. It can be
constructed and destructed like a pair: if `ha : a` and `hb : b` then
`⟨ha, hb⟩ : a ∧ b`, and if `h : a ∧ b` then `h.left : a` and `h.right : b`.


Conventions for notations in identifiers:

 * The recommended spelling of `∧` in identifiers is `and`.

 * The recommended spelling of `/\` in identifiers is `and` (prefer `∧` over `/\`).

## BASE-LIBRARY REF GT.gt
{α : Type u} → [LT α] → α → α → Prop

Docstring: `a > b` is an abbreviation for `b < a`. 

Conventions for notations in identifiers:

 * The recommended spelling of `>` in identifiers is `gt`.

## BASE-LIBRARY REF Fin.mk
{n : ℕ} → (val : ℕ) → val < n → Fin n

Docstring: Creates a `Fin n` from `i : Nat` and a proof that `i < n`. 

## BASE-LIBRARY REF instLTFin
{n : ℕ} → LT (Fin n)

## BASE-LIBRARY REF Finset
Type u_4 → Type u_4

Docstring: `Finset α` is the type of finite sets of elements of `α`. It is implemented
as a multiset (a list up to permutation) which has no duplicate elements. 

## BASE-LIBRARY REF Finset.map
{α : Type u_1} → {β : Type u_2} → (α ↪ β) → Finset α → Finset β

Docstring: When `f` is an embedding of `α` in `β` and `s` is a finset in `α`, then `s.map f` is the image
finset in `β`. The embedding condition guarantees that there are no duplicates in the image. 

## BASE-LIBRARY REF Subtype
{α : Sort u} → (α → Prop) → Sort (max 1 u)

Docstring: All the elements of a type that satisfy a predicate.

`Subtype p`, usually written `{ x : α // p x }` or `{ x // p x }`, contains all elements `x : α` for
which `p x` is true. Its constructor is a pair of the value and the proof that it satisfies the
predicate. In run-time code, `{ x : α // p x }` is represented identically to `α`.

There is a coercion from `{ x : α // p x }` to `α`, so elements of a subtype may be used where the
underlying type is expected.

Examples:
 * `{ n : Nat // n % 2 = 0 }` is the type of even numbers.
 * `{ xs : Array String // xs.size = 5 }` is the type of arrays with five `String`s.
 * Given `xs : List α`, `List { x : α // x ∈ xs }` is the type of lists in which all elements are
   contained in `xs`.


Conventions for notations in identifiers:

 * The recommended spelling of `{ x // p x }` in identifiers is `subtype`.

## BASE-LIBRARY REF Membership.mem
{α : outParam (Type u)} → {γ : Type v} → [self : Membership α γ] → γ → α → Prop

Docstring: The membership relation `a ∈ s : Prop` where `a : α`, `s : γ`. 

Conventions for notations in identifiers:

 * The recommended spelling of `∈` in identifiers is `mem`.

## BASE-LIBRARY REF Finset.instMembership
{α : Type u_1} → Membership α (Finset α)

## BASE-LIBRARY REF Function.Embedding.mk
{α : Sort u_1} → {β : Sort u_2} → (toFun : α → β) → Function.Injective toFun → α ↪ β

## BASE-LIBRARY REF Finset.attach
{α : Type u_1} → (s : Finset α) → Finset { x // x ∈ s }

Docstring: `attach s` takes the elements of `s` and forms a new set of elements of the subtype
`{x // x ∈ s}`. 

## BASE-LIBRARY REF Finset.prod
{ι : Type u_1} → {M : Type u_3} → [CommMonoid M] → Finset ι → (ι → M) → M

Docstring: `∏ x ∈ s, f x` is the product of `f x` as `x` ranges over the elements of the finite set `s`.

When the index type is a `Fintype`, the notation `∏ x, f x`, is a shorthand for
`∏ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF CommRing.toCommMonoid
{α : Type u} → [self : CommRing α] → CommMonoid α

## BASE-LIBRARY REF Finset.univ
{α : Type u_1} → [Fintype α] → Finset α

Docstring: `univ` is the universal finite set of type `Finset α` implied from
the assumption `Fintype α`. 

## BASE-LIBRARY REF MvPolynomial.X
{R : Type u} → {σ : Type u_1} → [inst : CommSemiring R] → σ → MvPolynomial σ R

Docstring: `X n` is the degree `1` monomial $X_n$. 

## BASE-LIBRARY REF LE
Type u → Type u

Docstring: `LE α` is the typeclass which supports the notation `x ≤ y` where `x y : α`.

## BASE-LIBRARY REF LE.mk
{α : Type u} → (α → α → Prop) → LE α

## BASE-LIBRARY REF ite
{α : Sort u} → (c : Prop) → [h : Decidable c] → α → α → α

Docstring: `if c then t else e` is notation for `ite c t e`, "if-then-else", which decides to
return `t` or `e` depending on whether `c` is true or false. The explicit argument
`c : Prop` does not have any actual computational content, but there is an additional
`[Decidable c]` argument synthesized by typeclass inference which actually
determines how to evaluate `c` to true or false. Write `if h : c then t else e`
instead for a "dependent if-then-else" `dite`, which allows `t`/`e` to use the fact
that `c` is true/false.


## BASE-LIBRARY REF Int.instLEInt
LE ℤ

## BASE-LIBRARY REF instOfNat
{n : ℕ} → OfNat ℤ n

## BASE-LIBRARY REF Int.decLe
(a b : ℤ) → Decidable (a ≤ b)

Docstring: Decides whether `a ≤ b`.

```
#eval ¬ ( (7 : Int) ≤ (0 : Int) ) -- true
#eval (0 : Int) ≤ (0 : Int) -- true
#eval (7 : Int) ≤ (10 : Int) -- true
```

Implemented by efficient native code. 

## BASE-LIBRARY REF MvPolynomial.hsymm
(σ : Type u_5) → (R : Type u_6) → [inst : CommSemiring R] → [Fintype σ] → [DecidableEq σ] → ℕ → MvPolynomial σ R

Docstring: The `n`th complete homogeneous symmetric `MvPolynomial σ R`.
It is the sum over all the degree n monomials in `MvPolynomial σ R`. 

## BASE-LIBRARY REF Int.toNat
ℤ → ℕ

Docstring: Converts an integer into a natural number. Negative numbers are converted to `0`.

Examples:
* `(7 : Int).toNat = 7`
* `(0 : Int).toNat = 0`
* `(-7 : Int).toNat = 0`


## BASE-LIBRARY REF Zero.toOfNat0
{α : Type u_1} → [Zero α] → OfNat α 0

## BASE-LIBRARY REF MulZeroClass.toZero
{M₀ : Type u} → [self : MulZeroClass M₀] → Zero M₀

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.toMulZeroClass
{α : Type u} → [self : NonUnitalNonAssocSemiring α] → MulZeroClass α

## BASE-LIBRARY REF Finset.filter
{α : Type u_1} → (p : α → Prop) → [DecidablePred p] → Finset α → Finset α

Docstring: `Finset.filter p s` is the set of elements of `s` that satisfy `p`.

For example, one can use `s.filter (· ∈ t)` to get the intersection of `s` with `t : Set α`
as a `Finset α` (when a `DecidablePred (· ∈ t)` instance is available). 

## BASE-LIBRARY REF Decidable
Prop → Type

Docstring: Either a proof that `p` is true or a proof that `p` is false. This is equivalent to a `Bool` paired
with a proof that the `Bool` is `true` if and only if `p` is true.

`Decidable` instances are primarily used via `if`-expressions and the tactic `decide`. In
conditional expressions, the `Decidable` instance for the proposition is used to select a branch. At
run time, this case distinction code is identical to that which would be generated for a
`Bool`-based conditional. In proofs, the tactic `decide` synthesizes an instance of `Decidable p`,
attempts to reduce it to `isTrue h`, and then succeeds with the proof `h` if it can.

Because `Decidable` carries data, when writing `@[simp]` lemmas which include a `Decidable` instance
on the LHS, it is best to use `{_ : Decidable p}` rather than `[Decidable p]` so that non-canonical
instances can be found via unification rather than instance synthesis.


## BASE-LIBRARY REF instDecidableAnd
{p q : Prop} → [dp : Decidable p] → [dq : Decidable q] → Decidable (p ∧ q)

## BASE-LIBRARY REF Fintype
Type u_4 → Type u_4

Docstring: `Fintype α` means that `α` is finite, i.e. there are only
finitely many distinct elements of type `α`. The evidence of this
is a finset `elems` (a list up to permutation without duplicates),
together with a proof that everything of type `α` is in the list. 

## BASE-LIBRARY REF Pi.instFintype
{α : Type u_3} →
  {β : α → Type u_4} → [DecidableEq α] → [Fintype α] → [(a : α) → Fintype (β a)] → Fintype ((a : α) → β a)

Docstring: A dependent product of fintypes, indexed by a fintype, is a fintype. 

## BASE-LIBRARY REF Fintype.decidableForallFintype
{α : Type u_1} → {p : α → Prop} → [DecidablePred p] → [Fintype α] → Decidable (∀ (a : α), p a)

## BASE-LIBRARY REF Nat.decidableForallFin
{n : ℕ} → (P : Fin n → Prop) → [DecidablePred P] → Decidable (∀ (i : Fin n), P i)

## BASE-LIBRARY REF forall_prop_decidable
{p : Prop} → (P : p → Prop) → [Decidable p] → [(h : p) → Decidable (P h)] → Decidable (∀ (h : p), P h)

## BASE-LIBRARY REF Fin.decLe
{n : ℕ} → (a b : Fin n) → Decidable (a ≤ b)

## BASE-LIBRARY REF Nat.decLt
(n m : ℕ) → Decidable (n < m)

Docstring: A decision procedure for strict inequality of natural numbers, usually accessed via the
`DecidableLT Nat` instance.

Examples:
 * `(if 3 < 4 then "yes" else "no") = "yes"`
 * `(if 4 < 4 then "yes" else "no") = "no"`
 * `(if 6 < 4 then "yes" else "no") = "no"`
 * `show 5 < 12 by decide`


## BASE-LIBRARY REF Nat.decLe
(n m : ℕ) → Decidable (n ≤ m)

Docstring: A decision procedure for non-strict inequality of natural numbers, usually accessed via the
`DecidableLE Nat` instance.

Examples:
 * `(if 3 ≤ 4 then "yes" else "no") = "yes"`
 * `(if 6 ≤ 4 then "yes" else "no") = "no"`
 * `show 12 ≤ 12 by decide`
 * `show 5 ≤ 12 by decide`


## BASE-LIBRARY REF Fin.decLt
{n : ℕ} → (a b : Fin n) → Decidable (a < b)

## INFORMAL STATEMENT
First Jacobi–Trudi formula

Let $M\in \mathbb {N}$. Let $\lambda =\left( \lambda _{1},\lambda _{2},\ldots ,\lambda _{M}\right) $ and $\mu =\left( \mu _{1},\mu _{2},\ldots ,\mu _{M}\right) $ be two $M$-partitions (i.e., weakly decreasing $M$-tuples of nonnegative integers). Then,

\[  s_{\lambda /\mu }=\det \left( \left( h_{\lambda _{i}-\mu _{j}-i+j}\right) _{1\leq i\leq M,\  1\leq j\leq M}\right) .  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.det.det
def.det.det

Let $n \in \mathbb {N}$. Let $A \in K^{n \times n}$ be an $n \times n$-matrix. The \emph{determinant} $\det A$ of $A$ is defined to be the element 

\[  \sum _{\sigma \in S_n} (-1)^{\sigma } \underbrace{A_{1,\sigma (1)} A_{2,\sigma (2)} \cdots A_{n,\sigma (n)}}_{ = \prod _{i=1}^{n} A_{i,\sigma (i)}}  \]

 of $K$. Here: 

\begin{itemize} \item we let $S_n$ denote the $n$-th symmetric group (i.e., the group of permutations of $[n] = \{ 1, 2, \ldots , n\} $); 

\item we let $(-1)^{\sigma }$ denote the sign of the permutation $\sigma $ (as defined in Definition~ \ref{def.perm.sign}). 

\end{itemize}

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.invs
def.perm.invs

Let $n\in \mathbb {N}$ and $\sigma \in S_{n}$. \medskip 

\textbf{(a)} An \emph{inversion} of $\sigma $ means a pair $\left(i,j\right)$ of elements of $\left[n\right]$ such that $i<j$ and $\sigma \left(i\right) >\sigma \left(j\right)$. \medskip 

\textbf{(b)} The \emph{length} (also known as the \emph{Coxeter length}) of $\sigma $ is the \#  of inversions of $\sigma $. It is called $\ell \left( \sigma \right)$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.perm
def.perm.perm

Let $X$ be a set. 

\textbf{(a)} A \emph{permutation} of $X$ means a bijection from $X$ to $X$. 

\textbf{(b)} It is known that the set of all permutations of $X$ is a group under composition. This group is called the \emph{symmetric group} of $X$, and is denoted by $S_X$. Its neutral element is the identity map $\operatorname {id}_X : X \to X$. Its size is $|X|!$ when $X$ is finite. 

\textbf{(c)} As usual in group theory, we will write $\alpha \beta $ for the composition $\alpha \circ \beta $ when $\alpha , \beta \in S_X$. This is the map that sends each $x \in X$ to $\alpha (\beta (x))$. 

\textbf{(d)} If $\alpha \in S_X$ and $i \in \mathbb {Z}$, then $\alpha ^i$ shall denote the $i$-th power of $\alpha $ in the group $S_X$. Note that $\alpha ^i = \underbrace{\alpha \circ \alpha \circ \cdots \circ \alpha }_{i\text{ times}}$ if $i \ge 0$. Also, $\alpha ^0 = \operatorname {id}_X$. Also, $\alpha ^{-1}$ is the inverse of $\alpha $ in the group $S_X$, that is, the inverse of the map $\alpha $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.sign
def.perm.sign

Let $n \in \mathbb {N}$. The \emph{sign} of a permutation $\sigma \in S_n$ is defined to be the integer $(-1)^{\ell (\sigma )}$. 

It is denoted by $(-1)^{\sigma }$ or $\operatorname {sgn}(\sigma )$ or $\operatorname {sign}(\sigma )$ or $\varepsilon (\sigma )$. It is also known as the \emph{signature} of $\sigma $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.sn-iven
def.perm.Sn-iven

Let $n \in \mathbb {Z}$. Then, $[n]$ shall mean the set $\{ 1, 2, \ldots , n\} $. This is an $n$-element set if $n \ge 0$, and is an empty set if $n \le 0$. 

The symmetric group $S_{[n]}$ (consisting of all permutations of $[n]$) will be denoted $S_n$ and called the $n$\emph{-th symmetric group}. Its size is $n!$ (when $n \ge 0$).

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.skew-schur
def.sf.skew-schur

Let $\lambda $ and $\mu $ be two $N$-partitions. We define the \emph{skew Schur polynomial} $s_{\lambda /\mu }\in \mathcal{P}$ by

\[  s_{\lambda /\mu }:=\sum _{T\in \operatorname *{SSYT}\left( \lambda /\mu \right) }x_{T}.  \]

## VERDICT
{
  "verdict": "unstatable",
  "justification": "The blueprint quantifies over \u201ctwo M-partitions\u201d and imposes no containment hypothesis before asserting the identity. The target instead has the additional binder `hcontained : \u2200 (i : Fin N), mu i \u2264 lam i`. Moreover, this restriction is forced by the dependency `SymmetricFunctions.SkewPartition.mk`, whose third argument is `inner \u2264 outer`, together with `NPartition.partLE`, whose body is `\u2200 i, mu.parts i \u2264 lam.parts i`; `SymmetricFunctions.skewSchur` only accepts such a `SkewPartition`. Thus the blueprint\u2019s claimed `s_{\u03bb/\u03bc}` for arbitrary pairs of partitions cannot be stated using the supplied project definition, rather than merely being omitted by the target. To make it statable and faithful, `SkewPartition`/`skewSchur` and their tableau dependencies would need to be generalized to arbitrary pairs of partitions with a specified meaning for noncontained pairs. Alternatively, the informal theorem would need an explicit assumption `\u03bc \u2286 \u03bb`, in which case the present target would match it."
}