## TARGET SymmetricFunctions.nipatSSYTEquiv (def) — ELABORATED SIGNATURE
{N : ℕ} →
  (lam mu : Fin N → ℕ) →
    (hlam : ∀ (i j : Fin N), i ≤ j → lam j ≤ lam i) →
      (hmu : ∀ (i j : Fin N), i ≤ j → mu j ≤ mu i) →
        (hcontained : ∀ (i : Fin N), mu i ≤ lam i) →
          SymmetricFunctions.Nipat lam mu hlam hmu hcontained ≃
            SymmetricFunctions.SkewSSYT
              { outer := { parts := lam, weaklyDecreasing := hlam }, inner := { parts := mu, weaklyDecreasing := hmu },
                contained := ⋯ }

Body:
fun {N} lam mu hlam hmu hcontained =>
  { toFun := SymmetricFunctions.nipatToSSYT, invFun := SymmetricFunctions.ssytToNipat, left_inv := ⋯, right_inv := ⋯ }

Docstring: The equivalence between Nipat and SkewSSYT, established by the bijection functions. 

## PROJECT DEPENDENCY SymmetricFunctions.Nipat (inductive)
{N : ℕ} →
  (lam mu : Fin N → ℕ) →
    (∀ (i j : Fin N), i ≤ j → lam j ≤ lam i) →
      (∀ (i j : Fin N), i ≤ j → mu j ≤ mu i) → (∀ (i : Fin N), mu i ≤ lam i) → Type

Body:
SymmetricFunctions.Nipat.mk : {N : ℕ} →
  {lam mu : Fin N → ℕ} →
    {hlam : ∀ (i j : Fin N), i ≤ j → lam j ≤ lam i} →
      {hmu : ∀ (i j : Fin N), i ≤ j → mu j ≤ mu i} →
        {hcontained : ∀ (i : Fin N), mu i ≤ lam i} →
          (paths : (i : Fin N) → SymmetricFunctions.LatticePath (↑(mu i) - ↑↑i) (↑(lam i) - ↑↑i)) →
            (∀ (i j : Fin N),
                i < j →
                  ∀ (k : ℕ) (hk : k < (paths i).eastStepHeights.length) (k' : ℕ)
                    (hk' : k' < (paths j).eastStepHeights.length),
                    mu i + k = mu j + k' → (paths i).eastStepHeights[k] < (paths j).eastStepHeights[k']) →
              SymmetricFunctions.Nipat lam mu hlam hmu hcontained

Docstring: A non-intersecting path tuple (nipat) from sources A to targets B.
For Jacobi-Trudi, A_i = (μᵢ - i, 1) and B_i = (λᵢ - i, N). 

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

## PROJECT DEPENDENCY SymmetricFunctions.SkewPartition.mk (constructor)
{N : ℕ} → (outer inner : SymmetricFunctions.NPartition N) → inner ≤ outer → SymmetricFunctions.SkewPartition N

## PROJECT DEPENDENCY SymmetricFunctions.NPartition.mk (constructor)
{N : ℕ} → (parts : Fin N → ℕ) → (∀ (i j : Fin N), i ≤ j → parts j ≤ parts i) → SymmetricFunctions.NPartition N

## PROJECT DEPENDENCY SymmetricFunctions.nipatToSSYT (def)
{N : ℕ} →
  {lam mu : Fin N → ℕ} →
    {hlam : ∀ (i j : Fin N), i ≤ j → lam j ≤ lam i} →
      {hmu : ∀ (i j : Fin N), i ≤ j → mu j ≤ mu i} →
        {hcontained : ∀ (i : Fin N), mu i ≤ lam i} →
          SymmetricFunctions.Nipat lam mu hlam hmu hcontained →
            SymmetricFunctions.SkewSSYT
              { outer := { parts := lam, weaklyDecreasing := hlam }, inner := { parts := mu, weaklyDecreasing := hmu },
                contained := ⋯ }

Body:
fun {N} {lam mu} {hlam} {hmu} {hcontained} np =>
  { entries := fun i k => (np.paths i).eastStepHeights.get ⟨↑k, ⋯⟩, rowWeak := ⋯, colStrict := ⋯ }

Docstring: The bijection between nipats and SSYT, sending a nipat to the tableau
whose i-th row contains the heights of east-steps in path i. 

## PROJECT DEPENDENCY SymmetricFunctions.ssytToNipat (def)
{N : ℕ} →
  {lam mu : Fin N → ℕ} →
    {hlam : ∀ (i j : Fin N), i ≤ j → lam j ≤ lam i} →
      {hmu : ∀ (i j : Fin N), i ≤ j → mu j ≤ mu i} →
        {hcontained : ∀ (i : Fin N), mu i ≤ lam i} →
          SymmetricFunctions.SkewSSYT
              { outer := { parts := lam, weaklyDecreasing := hlam }, inner := { parts := mu, weaklyDecreasing := hmu },
                contained := ⋯ } →
            SymmetricFunctions.Nipat lam mu hlam hmu hcontained

Body:
fun {N} {lam mu} {hlam} {hmu} {hcontained} T =>
  { paths := fun i => SymmetricFunctions.mkLatticePathFromEntries (lam i) (mu i) (↑i) (T.entries i) ⋯,
    colStrictPaths := ⋯ }

Docstring: The inverse bijection from SSYT to nipats, sending a tableau to the nipat
whose i-th path has east-steps at the heights given by row i of the tableau. 

## PROJECT DEPENDENCY SymmetricFunctions.ssytToNipat_nipatToSSYT (theorem)
∀ {N : ℕ} {lam mu : Fin N → ℕ} {hlam : ∀ (i j : Fin N), i ≤ j → lam j ≤ lam i}
  {hmu : ∀ (i j : Fin N), i ≤ j → mu j ≤ mu i} {hcontained : ∀ (i : Fin N), mu i ≤ lam i}
  (np : SymmetricFunctions.Nipat lam mu hlam hmu hcontained),
  SymmetricFunctions.ssytToNipat (SymmetricFunctions.nipatToSSYT np) = np

Docstring: ssytToNipat is a left inverse of nipatToSSYT. 

## PROJECT DEPENDENCY SymmetricFunctions.nipatToSSYT_ssytToNipat (theorem)
∀ {N : ℕ} {lam mu : Fin N → ℕ} {hlam : ∀ (i j : Fin N), i ≤ j → lam j ≤ lam i}
  {hmu : ∀ (i j : Fin N), i ≤ j → mu j ≤ mu i} {hcontained : ∀ (i : Fin N), mu i ≤ lam i}
  (T :
    SymmetricFunctions.SkewSSYT
      { outer := { parts := lam, weaklyDecreasing := hlam }, inner := { parts := mu, weaklyDecreasing := hmu },
        contained := ⋯ }),
  SymmetricFunctions.nipatToSSYT (SymmetricFunctions.ssytToNipat T) = T

Docstring: nipatToSSYT is a left inverse of ssytToNipat. 

## PROJECT DEPENDENCY SymmetricFunctions.LatticePath (inductive)
{N : ℕ} → ℤ → ℤ → Type

Body:
SymmetricFunctions.LatticePath.mk : {N : ℕ} →
  {a c : ℤ} →
    (eastStepHeights : List (Fin N)) →
      List.IsChain (fun x1 x2 => x1 ≤ x2) eastStepHeights →
        eastStepHeights.length = (c - a).toNat → SymmetricFunctions.LatticePath a c

Docstring: A lattice path in ℤ² from (a, 1) to (c, N) using north and east steps.
This is the type of paths relevant for the Jacobi-Trudi proof. 

## PROJECT DEPENDENCY SymmetricFunctions.LatticePath.eastStepHeights (def)
{N : ℕ} → {a c : ℤ} → SymmetricFunctions.LatticePath a c → List (Fin N)

Body:
fun N a c self => self.1

Docstring: The sequence of heights at which east-steps are taken.
A path from (a, 1) to (c, N) has exactly (c - a) east-steps
(when c ≥ a), and each east-step occurs at some height in [1, N]. 

## PROJECT DEPENDENCY SymmetricFunctions.SkewPartition (inductive)
ℕ → Type

Body:
SymmetricFunctions.SkewPartition.mk : {N : ℕ} → (outer inner : SymmetricFunctions.NPartition N) → inner ≤ outer → SymmetricFunctions.SkewPartition N

Docstring: A skew partition λ/μ is a pair of N-partitions with μ ⊆ λ.
Definition def.sf.strips(a). 

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

## PROJECT DEPENDENCY SymmetricFunctions.Nipat.paths (def)
{N : ℕ} →
  {lam mu : Fin N → ℕ} →
    {hlam : ∀ (i j : Fin N), i ≤ j → lam j ≤ lam i} →
      {hmu : ∀ (i j : Fin N), i ≤ j → mu j ≤ mu i} →
        {hcontained : ∀ (i : Fin N), mu i ≤ lam i} →
          SymmetricFunctions.Nipat lam mu hlam hmu hcontained →
            (i : Fin N) → SymmetricFunctions.LatticePath (↑(mu i) - ↑↑i) (↑(lam i) - ↑↑i)

Body:
fun N lam mu hlam hmu hcontained self => self.1

Docstring: The tuple of paths, one for each i ∈ [N] 

## PROJECT DEPENDENCY SymmetricFunctions.Nipat.mk (constructor)
{N : ℕ} →
  {lam mu : Fin N → ℕ} →
    {hlam : ∀ (i j : Fin N), i ≤ j → lam j ≤ lam i} →
      {hmu : ∀ (i j : Fin N), i ≤ j → mu j ≤ mu i} →
        {hcontained : ∀ (i : Fin N), mu i ≤ lam i} →
          (paths : (i : Fin N) → SymmetricFunctions.LatticePath (↑(mu i) - ↑↑i) (↑(lam i) - ↑↑i)) →
            (∀ (i j : Fin N),
                i < j →
                  ∀ (k : ℕ) (hk : k < (paths i).eastStepHeights.length) (k' : ℕ)
                    (hk' : k' < (paths j).eastStepHeights.length),
                    mu i + k = mu j + k' → (paths i).eastStepHeights[k] < (paths j).eastStepHeights[k']) →
              SymmetricFunctions.Nipat lam mu hlam hmu hcontained

## PROJECT DEPENDENCY SymmetricFunctions.mkLatticePathFromEntries (def)
{N : ℕ} →
  (lam mu i : ℕ) →
    (entries : Fin (lam - mu) → Fin N) →
      (∀ (j k : Fin (lam - mu)), j ≤ k → entries j ≤ entries k) → SymmetricFunctions.LatticePath (↑mu - ↑i) (↑lam - ↑i)

Body:
fun {N} lam mu i entries hrowWeak => { eastStepHeights := List.ofFn entries, weaklyIncreasing := ⋯, length_eq := ⋯ }

Docstring: Helper to create a LatticePath from tableau entries for a single row.
Given entries for row i of a tableau, creates the corresponding lattice path
with east-steps at the heights given by the entries. 

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

## PROJECT DEPENDENCY SymmetricFunctions.LatticePath.mk (constructor)
{N : ℕ} →
  {a c : ℤ} →
    (eastStepHeights : List (Fin N)) →
      List.IsChain (fun x1 x2 => x1 ≤ x2) eastStepHeights →
        eastStepHeights.length = (c - a).toNat → SymmetricFunctions.LatticePath a c

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


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

## BASE-LIBRARY REF Equiv
Sort u_1 → Sort u_2 → Sort (max (max 1 u_1) u_2)

Docstring: `α ≃ β` is the type of functions from `α → β` with a two-sided inverse. 

## BASE-LIBRARY REF Equiv.mk
{α : Sort u_1} →
  {β : Sort u_2} →
    (toFun : α → β) →
      (invFun : β → α) →
        autoParam (Function.LeftInverse invFun toFun) Equiv.left_inv._autoParam →
          autoParam (Function.RightInverse invFun toFun) Equiv.right_inv._autoParam → α ≃ β

## BASE-LIBRARY REF HSub.hSub
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HSub α β γ] → α → β → γ

Docstring: `a - b` computes the difference of `a` and `b`.
The meaning of this notation is type-dependent.
* For natural numbers, this operator saturates at 0: `a - b = 0` when `a ≤ b`. 

Conventions for notations in identifiers:

 * The recommended spelling of `-` in identifiers is `sub` (when used as a binary operator).

## BASE-LIBRARY REF Int
Type

Docstring: The integers.

This type is special-cased by the compiler and overridden with an efficient implementation. The
runtime has a special representation for `Int` that stores “small” signed numbers directly, while
larger numbers use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)). A “small number” is an integer that can be encoded with one fewer bits
than the platform's pointer size (i.e. 63 bits on 64-bit architectures and 31 bits on 32-bit
architectures).


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


## BASE-LIBRARY REF LT.lt
{α : Type u} → [self : LT α] → α → α → Prop

Docstring: The less-than relation: `x < y` 

Conventions for notations in identifiers:

 * The recommended spelling of `<` in identifiers is `lt`.

## BASE-LIBRARY REF instLTFin
{n : ℕ} → LT (Fin n)

## BASE-LIBRARY REF instLTNat
LT ℕ

## BASE-LIBRARY REF List.length
{α : Type u_1} → List α → ℕ

Docstring: The length of a list.

This function is overridden in the compiler to `lengthTR`, which uses constant stack space.

Examples:
* `([] : List String).length = 0`
* `["green", "brown"].length = 2`


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

## BASE-LIBRARY REF HAdd.hAdd
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HAdd α β γ] → α → β → γ

Docstring: `a + b` computes the sum of `a` and `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `+` in identifiers is `add`.

## BASE-LIBRARY REF instHAdd
{α : Type u_1} → [Add α] → HAdd α α α

## BASE-LIBRARY REF instAddNat
Add ℕ

## BASE-LIBRARY REF GetElem.getElem
{coll : Type u} →
  {idx : Type v} →
    {elem : outParam (Type w)} →
      {valid : outParam (coll → idx → Prop)} →
        [self : GetElem coll idx elem valid] → (xs : coll) → (i : idx) → valid xs i → elem

Docstring: The syntax `arr[i]` gets the `i`'th element of the collection `arr`. If there
are proof side conditions to the application, they will be automatically
inferred by the `get_elem_tactic` tactic.


Conventions for notations in identifiers:

 * The recommended spelling of `xs[i]` in identifiers is `getElem`.

 * The recommended spelling of `xs[i]'h` in identifiers is `getElem`.

## BASE-LIBRARY REF List
Type u → Type u

Docstring: Linked lists: ordered lists, in which each element has a reference to the next element.

Most operations on linked lists take time proportional to the length of the list, because each
element must be traversed to find the next element.

`List α` is isomorphic to `Array α`, but they are useful for different things:
* `List α` is easier for reasoning, and `Array α` is modeled as a wrapper around `List α`.
* `List α` works well as a persistent data structure, when many copies of the tail are shared. When
  the value is not shared, `Array α` will have better performance because it can do destructive
  updates.


## BASE-LIBRARY REF List.instGetElemNatLtLength
{α : Type u_1} → GetElem (List α) ℕ α fun as i => i < as.length

## BASE-LIBRARY REF instSubNat
Sub ℕ

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

## BASE-LIBRARY REF List.get
{α : Type u} → (as : List α) → Fin as.length → α

Docstring: Returns the element at the provided index, counting from `0`.

In other words, for `i : Fin as.length`, `as.get i` returns the `i`'th element of the list `as`.
Because the index is a `Fin` bounded by the list's length, the index will never be out of bounds.

Examples:
 * `["spring", "summer", "fall", "winter"].get (2 : Fin 4) = "fall"`
 * `["spring", "summer", "fall", "winter"].get (0 : Fin 4) = "spring"`


## BASE-LIBRARY REF List.IsChain
{α : Type u_1} → (α → α → Prop) → List α → Prop

Docstring: `IsChain R l` means that `R` holds between adjacent elements of `l`. Example:
```
IsChain R [a, b, c, d] ↔ R a b ∧ R b c ∧ R c d
```


## BASE-LIBRARY REF Int.toNat
ℤ → ℕ

Docstring: Converts an integer into a natural number. Negative numbers are converted to `0`.

Examples:
* `(7 : Int).toNat = 7`
* `(0 : Int).toNat = 0`
* `(-7 : Int).toNat = 0`


## BASE-LIBRARY REF LE
Type u → Type u

Docstring: `LE α` is the typeclass which supports the notation `x ≤ y` where `x y : α`.

## BASE-LIBRARY REF LE.mk
{α : Type u} → (α → α → Prop) → LE α

## BASE-LIBRARY REF List.ofFn
{α : Type u_1} → {n : ℕ} → (Fin n → α) → List α

Docstring: Creates a list by applying `f` to each potential index in order, starting at `0`.

Examples:
* `List.ofFn (n := 3) toString = ["0", "1", "2"]`
* `List.ofFn (fun i => #["red", "green", "blue"].get i.val i.isLt) = ["red", "green", "blue"]`


## INFORMAL STATEMENT
lem.sf.nipat-ssyt-equiv

\leanhelper  The forward and inverse maps of the nipat–SSYT bijection form an equivalence of types: 

\[  \mathrm{Nipat}(\lambda , \mu ) \simeq \mathrm{SkewSSYT}(\lambda /\mu ).  \]

## VERDICT
{
  "verdict": "faithful",
  "justification": "The blueprint asserts that the forward and inverse maps give an equivalence `Nipat(\u03bb, \u03bc) \u2243 SkewSSYT(\u03bb/\u03bc)`. The target has exactly this codomain and domain: `SymmetricFunctions.Nipat lam mu hlam hmu hcontained \u2243 SymmetricFunctions.SkewSSYT { outer := ... lam ..., inner := ... mu ..., contained := ... }`. Its body uses `toFun := SymmetricFunctions.nipatToSSYT` and `invFun := SymmetricFunctions.ssytToNipat`, with both inverse laws supplied. The binders `hlam`, `hmu`, and `hcontained` merely encode that `lam` and `mu` are partitions with `\u03bc \u2286 \u03bb`, as required to form the skew shape `\u03bb/\u03bc`; they are not additional restrictions beyond the objects named in the blueprint."
}