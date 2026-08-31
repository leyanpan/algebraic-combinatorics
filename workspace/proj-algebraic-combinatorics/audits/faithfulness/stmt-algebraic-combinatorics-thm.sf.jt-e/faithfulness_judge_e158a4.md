## TARGET SymmetricFunctions.jacobiTrudi_e (theorem) — ELABORATED SIGNATURE
∀ {N : ℕ} {R : Type u_1} [inst : CommRing R] (lam mu lamt muT : Fin N → ℕ)
  (hlam : ∀ (i j : Fin N), i ≤ j → lam j ≤ lam i) (hmu : ∀ (i j : Fin N), i ≤ j → mu j ≤ mu i),
  (∀ (i j : Fin N), i ≤ j → lamt j ≤ lamt i) →
    (∀ (i j : Fin N), i ≤ j → muT j ≤ muT i) →
      ∀ (hcontained : ∀ (i : Fin N), mu i ≤ lam i),
        SymmetricFunctions.NPartition.IsTranspose lam lamt →
          SymmetricFunctions.NPartition.IsTranspose mu muT →
            SymmetricFunctions.skewSchur
                { outer := { parts := lam, weaklyDecreasing := hlam },
                  inner := { parts := mu, weaklyDecreasing := hmu }, contained := ⋯ } =
              (Matrix.of fun i j =>
                  have n := ↑(lamt i) - ↑(muT j) - ↑↑i + ↑↑j;
                  if 0 ≤ n then MvPolynomial.esymm (Fin N) R n.toNat else 0).det

## PROJECT DEPENDENCY SymmetricFunctions.NPartition.IsTranspose (def)
{N M : ℕ} → (Fin N → ℕ) → (Fin M → ℕ) → Prop

Body:
fun {N M} lam lamt =>
  (∀ (i : Fin M), lamt i = {j | ↑i + 1 ≤ lam j}.card) ∧ ∀ (j : Fin N), lam j = {i | ↑j + 1 ≤ lamt i}.card

Docstring: Predicate asserting that `lamt` is the transpose of `lam`.
The transpose λᵗ of a partition λ satisfies:
(λᵗ)ᵢ = |{j : λⱼ ≥ i}| for each i.

Since we work with fixed-length tuples, this predicate captures
when two tuples represent transpose partitions (possibly with trailing zeros). 

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

## BASE-LIBRARY REF DFunLike.coe
{F : Sort u_1} → {α : outParam (Sort u_2)} → {β : outParam (α → Sort u_3)} → [self : DFunLike F α β] → F → (a : α) → β a

Docstring: The coercion from `F` to a function. 

## BASE-LIBRARY REF Equiv
Sort u_1 → Sort u_2 → Sort (max (max 1 u_1) u_2)

Docstring: `α ≃ β` is the type of functions from `α → β` with a two-sided inverse. 

## BASE-LIBRARY REF Matrix
Type u → Type u' → Type v → Type (max u u' v)

Docstring: `Matrix m n R` is the type of matrices with entries in `R`, whose rows are indexed by `m`
and whose columns are indexed by `n`. 

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


## BASE-LIBRARY REF Int
Type

Docstring: The integers.

This type is special-cased by the compiler and overridden with an efficient implementation. The
runtime has a special representation for `Int` that stores “small” signed numbers directly, while
larger numbers use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)). A “small number” is an integer that can be encoded with one fewer bits
than the platform's pointer size (i.e. 63 bits on 64-bit architectures and 31 bits on 32-bit
architectures).


## BASE-LIBRARY REF HAdd.hAdd
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HAdd α β γ] → α → β → γ

Docstring: `a + b` computes the sum of `a` and `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `+` in identifiers is `add`.

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

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

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

## BASE-LIBRARY REF MvPolynomial.esymm
(σ : Type u_5) → (R : Type u_6) → [inst : CommSemiring R] → [Fintype σ] → ℕ → MvPolynomial σ R

Docstring: The `n`th elementary symmetric `MvPolynomial σ R`.
It is the sum over all the degree n squarefree monomials in `MvPolynomial σ R`. 

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

## BASE-LIBRARY REF NonUnitalNonAssocRing.toNonUnitalNonAssocSemiring
{α : Type u} → [self : NonUnitalNonAssocRing α] → NonUnitalNonAssocSemiring α

## BASE-LIBRARY REF NonUnitalNonAssocCommRing.toNonUnitalNonAssocRing
{α : Type u} → [self : NonUnitalNonAssocCommRing α] → NonUnitalNonAssocRing α

## BASE-LIBRARY REF NonUnitalCommRing.toNonUnitalNonAssocCommRing
{α : Type u} → [self : NonUnitalCommRing α] → NonUnitalNonAssocCommRing α

## BASE-LIBRARY REF CommRing.toNonUnitalCommRing
{α : Type u} → [s : CommRing α] → NonUnitalCommRing α

## INFORMAL STATEMENT
Second Jacobi–Trudi formula

Let $\lambda $ and $\mu $ be two partitions. Let $\lambda ^{t}$ and $\mu ^{t}$ be the transposes of $\lambda $ and $\mu $. Let $M\in \mathbb {N}$ be such that both $\lambda ^{t}$ and $\mu ^{t}$ have length $\leq M$. We extend the partitions $\lambda ^{t}$ and $\mu ^{t}$ to $M$-tuples (by inserting zeroes at the end). Write these $M$-tuples $\lambda ^{t}$ and $\mu ^{t}$ as $\lambda ^{t}=\left( \lambda _{1}^{t},\lambda _{2}^{t},\ldots ,\lambda _{M}^{t}\right) $ and $\mu ^{t}=\left( \mu _{1}^{t},\mu _{2}^{t},\ldots ,\mu _{M}^{t}\right) $. Then,

\[  s_{\lambda /\mu }=\det \left( \left( e_{\lambda _{i}^{t}-\mu _{j}^{t}-i+j}\right) _{1\leq i\leq M,\  1\leq j\leq M}\right) .  \]

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.alg.ring
def.alg.ring

The notion of a \emph{ring} (also known as a \emph{noncommutative ring}) is defined in the exact same way as we defined the notion of a commutative ring in Definition~ \ref{def.alg.commring}, except that the “Commutativity of multiplication” axiom is removed.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.comps
def.fps.comps

\textbf{(a)} An \emph{(integer) composition} means a (finite) tuple of positive integers. \medskip 

\textbf{(b)} The \emph{size} of an integer composition $\alpha =\left( \alpha _{1},\alpha _{2},\ldots ,\alpha _{m}\right) $ is defined to be the integer $\alpha _{1}+\alpha _{2}+\cdots +\alpha _{m}$. It is written $\left\vert \alpha \right\vert $. \medskip 

\textbf{(c)} The \emph{length} of an integer composition $\alpha =\left( \alpha _{1},\alpha _{2},\ldots ,\alpha _{m}\right) $ is defined to be the integer $m$. It is written $\ell \left( \alpha \right) $. \medskip 

\textbf{(d)} Let $n\in \mathbb {N}$. A \emph{composition of }$n$ means a composition whose size is $n$. \medskip 

\textbf{(e)} Let $n\in \mathbb {N}$ and $k\in \mathbb {N}$. A \emph{composition of }$n$\emph{ into }$k$\emph{ parts} is a composition whose size is $n$ and whose length is $k$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.wcomps
def.fps.wcomps

\textbf{(a)} An \emph{(integer) weak composition} means a (finite) tuple of nonnegative integers. \medskip 

\textbf{(b)} The \emph{size} of a weak composition $\alpha =\left( \alpha _{1},\alpha _{2},\ldots ,\alpha _{m}\right) $ is defined to be the integer $\alpha _{1}+\alpha _{2}+\cdots +\alpha _{m}$. It is written $\left\vert \alpha \right\vert $. \medskip 

\textbf{(c)} The \emph{length} of a weak composition $\alpha =\left( \alpha _{1},\alpha _{2},\ldots ,\alpha _{m}\right) $ is defined to be the integer $m$. It is written $\ell \left( \alpha \right) $. \medskip 

\textbf{(d)} Let $n\in \mathbb {N}$. A \emph{weak composition of }$n$ means a weak composition whose size is $n$. \medskip 

\textbf{(e)} Let $n\in \mathbb {N}$ and $k\in \mathbb {N}$. A \emph{weak composition of }$n$\emph{ into }$k$\emph{ parts} is a weak composition whose size is $n$ and whose length is $k$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.pars.parts
def.pars.parts

\textbf{(a)} An \emph{(integer) partition} means a (finite) weakly decreasing tuple of positive integers – i.e., a finite tuple $\left( \lambda _{1},\lambda _{2},\ldots ,\lambda _{m}\right) $ of positive integers such that $\lambda _{1}\geq \lambda _{2}\geq \cdots \geq \lambda _{m}$. 

Thus, partitions are the same as weakly decreasing compositions. Hence, the notions of \emph{size} and \emph{length} of a partition are automatically defined, since we have defined them for compositions (in Definition \ref{def.fps.comps}). \medskip 

\textbf{(b)} The \emph{parts} of a partition $\left( \lambda _{1},\lambda _{2},\ldots ,\lambda _{m}\right) $ are simply its entries $\lambda _{1},\lambda _{2},\ldots ,\lambda _{m}$. \medskip 

\textbf{(c)} Let $n\in \mathbb {Z}$. A \emph{partition of }$n$ means a partition whose size is $n$. \medskip 

\textbf{(d)} Let $n\in \mathbb {Z}$ and $k\in \mathbb {N}$. A \emph{partition of }$n$\emph{ into }$k$\emph{ parts} is a partition whose size is $n$ and whose length is $k$.

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.npartition-transpose
def.sf.npartition-transpose

\leanhelper  The \emph{transpose} (or \emph{conjugate}) of an $N$-partition $\lambda $ is the partition $\lambda ^t$ whose $i$-th part equals $|\{ j : j < N,\;  \lambda _j > i\} |$, i.e., the number of parts of $\lambda $ that exceed $i$. Requires $N > 0$; the result is a partition of length $\lambda _1$.

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.skew-diag
def.sf.skew-diag

Let $\lambda $ and $\mu $ be two $N$-partitions such that $\mu \subseteq \lambda $. Then, we define the \emph{skew Young diagram} $Y\left( \lambda /\mu \right) $ to be the set difference

\begin{align*}  Y\left( \lambda \right) \setminus Y\left( \mu \right) &  =\left\{  \left( i,j\right) \  \mid \  i\in \left[ N\right] \text{ and }j\in \left[ \lambda _{i}\right] \setminus \left[ \mu _{i}\right] \right\}  \\ &  =\left\{  \left( i,j\right) \  \mid \  i\in \left[ N\right] \text{ and }j\in \mathbb {Z}\text{ and }\mu _{i}<j\leq \lambda _{i}\right\}  . \end{align*}

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.skew-schur
def.sf.skew-schur

Let $\lambda $ and $\mu $ be two $N$-partitions. We define the \emph{skew Schur polynomial} $s_{\lambda /\mu }\in \mathcal{P}$ by

\[  s_{\lambda /\mu }:=\sum _{T\in \operatorname *{SSYT}\left( \lambda /\mu \right) }x_{T}.  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.skew-ssyt
def.sf.skew-ssyt

Let $\lambda $ and $\mu $ be two $N$-partitions. 

A Young tableau $T$ of shape $\lambda /\mu $ is said to be \emph{semistandard} if its entries 

\begin{itemize} \item increase weakly along each row (from left to right); 

\item increase strictly down each column (from top to bottom). 

\end{itemize}

Formally speaking, this means that a Young tableau $T:Y\left( \lambda /\mu \right) \rightarrow \left[ N\right] $ is semistandard if and only if 

\begin{itemize} \item we have $T\left( i,j\right) \leq T\left( i,j+1\right) $ for any $\left( i,j\right) \in Y\left( \lambda /\mu \right) $ satisfying $\left( i,j+1\right) \in Y\left( \lambda /\mu \right) $; 

\item we have $T\left( i,j\right) <T\left( i+1,j\right) $ for any $\left( i,j\right) \in Y\left( \lambda /\mu \right) $ satisfying $\left( i+1,j\right) \in Y\left( \lambda /\mu \right) $. 

\end{itemize}

We let $\operatorname *{SSYT}\left( \lambda /\mu \right) $ denote the set of all semistandard Young tableaux of shape $\lambda /\mu $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.skew-tab
def.sf.skew-tab

Let $\lambda $ and $\mu $ be two $N$-partitions such that $\mu \subseteq \lambda $. A \emph{Young tableau} of shape $\lambda /\mu $ means a way of filling the boxes of $Y\left( \lambda /\mu \right) $ with elements of $\left[ N\right] $ (one element per box). Formally speaking, it is defined as a map $T:Y\left( \lambda /\mu \right) \rightarrow \left[ N\right] $. 

Young tableaux of shape $\lambda /\mu $ are often called \emph{skew Young tableaux}. 

If we don’t have $\mu \subseteq \lambda $, then we agree that there are no Young tableaux of shape $\lambda /\mu $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.sort
def.sf.sort

Let $a=\left( a_{1},a_{2},\ldots ,a_{N}\right) \in \mathbb {N}^{N}$. Then: 

\textbf{(a)} We let $x^{a}$ denote the monomial $x_{1}^{a_{1}}x_{2}^{a_{2}}\cdots x_{N}^{a_{N}}$. 

\textbf{(b)} We let $\operatorname *{sort}a$ mean the $N$-partition obtained from $a$ by sorting the entries of $a$ in weakly decreasing order.

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.ytab.skew-xt
def.sf.ytab.skew-xT

Let $\lambda $ and $\mu $ be two $N$-partitions. If $T$ is any Young tableau of shape $\lambda /\mu $, then we define the corresponding monomial

\[  x_{T}:=\prod _{c\text{ is a box of }Y\left( \lambda /\mu \right) }x_{T\left( c\right) }=\prod _{\left( i,j\right) \in Y\left( \lambda /\mu \right) }x_{T\left( i,j\right) }=\prod _{k=1}^{N}x_{k}^{\left( \text{\#  of times }k\text{ appears in }T\right) }.  \]

## VERDICT
{
  "verdict": "drift",
  "justification": "The blueprint quantifies an independent determinant size: \u201cLet M \u2208 \u2115 be such that both \u03bb\u1d57 and \u03bc\u1d57 have length \u2264 M\u201d and uses an M\u00d7M matrix. The target instead has only one size binder, `\u2200 {N : \u2115} ... (lam mu lamt muT : Fin N \u2192 \u2115)`, and its determinant is indexed by `Fin N`. Thus it identifies M with the number N of polynomial variables/rows and, through `IsTranspose lam lamt`, restricts both transposes to fit in that same N, rather than allowing arbitrary M. It also adds `hcontained : \u2200 i, mu i \u2264 lam i`, although the blueprint says merely \u201cLet \u03bb and \u03bc be two partitions\u201d; its informal skew-Schur definitions cover noncontained pairs by having no tableaux. This added hypothesis enters because `SymmetricFunctions.SkewPartition.mk` and hence `SymmetricFunctions.skewSchur` require `inner \u2264 outer`. To be faithful, the target should use separate binders `N M`, take `lam mu : Fin N \u2192 \u2115` and `lamt muT : Fin M \u2192 \u2115`, use `IsTranspose` across those sizes, and take the determinant over `Fin M`. It should also remove the containment restriction by extending `skewSchur` to arbitrary pairs (returning the empty-tableau sum when not contained), or state the equality by cases; alternatively the blueprint would need to assume `\u03bc \u2286 \u03bb`."
}