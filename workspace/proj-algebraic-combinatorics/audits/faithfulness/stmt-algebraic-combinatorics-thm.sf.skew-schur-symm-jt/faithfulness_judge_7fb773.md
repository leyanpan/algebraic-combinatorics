## TARGET SymmetricFunctions.skewSchur_isSymmetric_jacobiTrudi (theorem) — ELABORATED SIGNATURE
∀ {N : ℕ} {R : Type u_1} [inst : CommRing R] (lam mu : Fin N → ℕ) (hlam : ∀ (i j : Fin N), i ≤ j → lam j ≤ lam i)
  (hmu : ∀ (i j : Fin N), i ≤ j → mu j ≤ mu i) (hcontained : ∀ (i : Fin N), mu i ≤ lam i),
  (SymmetricFunctions.skewSchur
      { outer := { parts := lam, weaklyDecreasing := hlam }, inner := { parts := mu, weaklyDecreasing := hmu },
        contained := ⋯ }).IsSymmetric

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

## PROJECT DEPENDENCY AlgebraicCombinatorics.SymmetricPolynomials.P_isCommRing' (def)
{K : Type u_1} → [inst : CommRing K] → {N : ℕ} → CommRing (AlgebraicCombinatorics.SymmetricPolynomials.P K N)

Body:
fun {K} [CommRing K] {N} => inferInstance

Docstring: The polynomial ring P K N is a commutative K-algebra.
Label: def.sf.PS 

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

## PROJECT DEPENDENCY AlgebraicCombinatorics.SymmetricPolynomials.P (def)
(K : Type u_2) → [CommRing K] → ℕ → Type u_2

Body:
fun K [CommRing K] N => MvPolynomial (Fin N) K

Docstring: The polynomial ring in N variables over K.
This corresponds to 𝒫 in the source (Definition def.sf.PS (a)).
Label: def.sf.PS 

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

## BASE-LIBRARY REF MvPolynomial.IsSymmetric
{σ : Type u_1} → {R : Type u_3} → [inst : CommSemiring R] → MvPolynomial σ R → Prop

Docstring: A `MvPolynomial φ` is symmetric if it is invariant under
permutations of its variables by the `rename` operation 

## BASE-LIBRARY REF CommRing.toCommSemiring
{α : Type u} → [s : CommRing α] → CommSemiring α

## INFORMAL STATEMENT
thm.sf.skew-schur-symm-jt

\leanhelper  Skew Schur polynomials are symmetric: for any partitions $\lambda \supseteq \mu $, $s_{\lambda /\mu }$ is a symmetric polynomial. 

This provides a proof of symmetry via the Jacobi–Trudi formula, without relying on the Bender–Knuth involution.

## INFORMAL DEPENDENCY stmt-algebraic-combinatorics-thm.sf.jt-h
First Jacobi–Trudi formula

Let $M\in \mathbb {N}$. Let $\lambda =\left( \lambda _{1},\lambda _{2},\ldots ,\lambda _{M}\right) $ and $\mu =\left( \mu _{1},\mu _{2},\ldots ,\mu _{M}\right) $ be two $M$-partitions (i.e., weakly decreasing $M$-tuples of nonnegative integers). Then,

\[  s_{\lambda /\mu }=\det \left( \left( h_{\lambda _{i}-\mu _{j}-i+j}\right) _{1\leq i\leq M,\  1\leq j\leq M}\right) .  \]

## INFORMAL DEPENDENCY stmt-algebraic-combinatorics-thm.sf.jt-matrix-det-symmetric
thm.sf.jt-matrix-det-symmetric

\leanhelper  The determinant of the Jacobi–Trudi matrix $\det (H)$ is a symmetric polynomial.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The formal theorem states that for every `N`, commutative coefficient ring `R`, weakly decreasing `lam mu : Fin N \u2192 \u2115`, and pointwise containment `hcontained : \u2200 i, mu i \u2264 lam i`, the polynomial `skewSchur ...` satisfies `.IsSymmetric`. This matches \u201cfor any partitions \u03bb \u2287 \u03bc, s_{\u03bb/\u03bc} is a symmetric polynomial.\u201d The definitions preserve the intended meanings: `NPartition` encodes weakly decreasing nonnegative N-tuples, `SkewPartition` encodes `\u03bc \u2286 \u03bb`, `skewSchur` is \u201cthe sum over all skew SSYT,\u201d and `MvPolynomial.IsSymmetric` means invariance under permutations of variables. The shared parameter `N` agrees with the informal Jacobi\u2013Trudi dependency\u2019s two `M`-partitions and gives an N-variable polynomial with tableau entries in `[N]`. The `[CommRing R]` binder is the coefficient-ring setting needed for the Jacobi\u2013Trudi determinant argument, rather than an unrelated mathematical restriction. The final sentence about proving symmetry via Jacobi\u2013Trudi describes the proof method, not an additional proposition that must appear in the theorem signature."
}