## TARGET SymmetricFunctions.schur_zero (theorem) — ELABORATED SIGNATURE
∀ {N : ℕ} {R : Type u_1} [inst : CommRing R], SymmetricFunctions.schur 0 = 1

Docstring: The Schur polynomial of the zero partition is 1.
This is because the only SSYT of shape 0 is the empty tableau with monomial 1. 

## PROJECT DEPENDENCY SymmetricFunctions.schur (def)
{N : ℕ} → {R : Type u_1} → [inst : CommRing R] → SymmetricFunctions.NPartition N → MvPolynomial (Fin N) R

Body:
fun {N} {R} [CommRing R] lam => ∑ T ∈ SymmetricFunctions.ssytFinset lam, T.toMonomial

Docstring: The Schur polynomial s_λ defined as the sum over all SSYT of shape λ.
Definition def.sf.schur. 

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

## PROJECT DEPENDENCY SymmetricFunctions.NPartition.instZero (def)
{N : ℕ} → Zero (SymmetricFunctions.NPartition N)

Body:
fun {N} => { zero := SymmetricFunctions.NPartition.zero N }

## PROJECT DEPENDENCY AlgebraicCombinatorics.SymmetricPolynomials.P_isCommRing' (def)
{K : Type u_1} → [inst : CommRing K] → {N : ℕ} → CommRing (AlgebraicCombinatorics.SymmetricPolynomials.P K N)

Body:
fun {K} [CommRing K] {N} => inferInstance

Docstring: The polynomial ring P K N is a commutative K-algebra.
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

## PROJECT DEPENDENCY SymmetricFunctions.NPartition.zero (def)
(N : ℕ) → SymmetricFunctions.NPartition N

Body:
fun N => { parts := fun x => 0, weaklyDecreasing := ⋯ }

Docstring: The zero partition (0, 0, ..., 0) 

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

## PROJECT DEPENDENCY SymmetricFunctions.NPartition.mk (constructor)
{N : ℕ} → (parts : Fin N → ℕ) → (∀ (i j : Fin N), i ≤ j → parts j ≤ parts i) → SymmetricFunctions.NPartition N

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

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF Zero.toOfNat0
{α : Type u_1} → [Zero α] → OfNat α 0

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

## BASE-LIBRARY REF Zero
Type u → Type u

Docstring: A type with a zero element. 

## BASE-LIBRARY REF Zero.mk
{α : Type u} → α → Zero α

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

## BASE-LIBRARY REF LT.lt
{α : Type u} → [self : LT α] → α → α → Prop

Docstring: The less-than relation: `x < y` 

Conventions for notations in identifiers:

 * The recommended spelling of `<` in identifiers is `lt`.

## BASE-LIBRARY REF instLTNat
LT ℕ

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

## BASE-LIBRARY REF Fin.val
{n : ℕ} → Fin n → ℕ

Docstring: The number that is strictly less than `n`.

`Fin.val` is a coercion, so any `Fin n` can be used in a position where a `Nat` is expected.


## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

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

## BASE-LIBRARY REF Fin.fintype
(n : ℕ) → Fintype (Fin n)

## BASE-LIBRARY REF MvPolynomial.X
{R : Type u} → {σ : Type u_1} → [inst : CommSemiring R] → σ → MvPolynomial σ R

Docstring: `X n` is the degree `1` monomial $X_n$. 

## BASE-LIBRARY REF Finset.filter
{α : Type u_1} → (p : α → Prop) → [DecidablePred p] → Finset α → Finset α

Docstring: `Finset.filter p s` is the set of elements of `s` that satisfy `p`.

For example, one can use `s.filter (· ∈ t)` to get the intersection of `s` with `t : Set α`
as a `Finset α` (when a `DecidablePred (· ∈ t)` instance is available). 

## BASE-LIBRARY REF And
Prop → Prop → Prop

Docstring: `And a b`, or `a ∧ b`, is the conjunction of propositions. It can be
constructed and destructed like a pair: if `ha : a` and `hb : b` then
`⟨ha, hb⟩ : a ∧ b`, and if `h : a ∧ b` then `h.left : a` and `h.right : b`.


Conventions for notations in identifiers:

 * The recommended spelling of `∧` in identifiers is `and`.

 * The recommended spelling of `/\` in identifiers is `and` (prefer `∧` over `/\`).

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

## BASE-LIBRARY REF instDecidableEqFin
(n : ℕ) → DecidableEq (Fin n)

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


## BASE-LIBRARY REF Fin.decLt
{n : ℕ} → (a b : Fin n) → Decidable (a < b)

## INFORMAL STATEMENT
lem.sf.schur-zero

\leanhelper  The Schur polynomial of the zero partition is $1$: $s_0 = 1$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-conv-2eb59533
conv-2eb59533

In the Lean formalization, we use $\operatorname {Fin} n = \{ 0, 1, \ldots , n-1\} $ instead of the textbook’s $[n] = \{ 1, 2, \ldots , n\} $. Both are $n$-element sets, so their symmetric groups are isomorphic. Permutations are represented by the type of bijections $X \to X$ (denoted $\operatorname {Equiv.Perm}\,  X$ in Lean), which is a group under composition. Composition $\alpha \beta $ is the group multiplication $\alpha * \beta $, sending $x$ to $\alpha (\beta (x))$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.perm
def.perm.perm

Let $X$ be a set. 

\textbf{(a)} A \emph{permutation} of $X$ means a bijection from $X$ to $X$. 

\textbf{(b)} It is known that the set of all permutations of $X$ is a group under composition. This group is called the \emph{symmetric group} of $X$, and is denoted by $S_X$. Its neutral element is the identity map $\operatorname {id}_X : X \to X$. Its size is $|X|!$ when $X$ is finite. 

\textbf{(c)} As usual in group theory, we will write $\alpha \beta $ for the composition $\alpha \circ \beta $ when $\alpha , \beta \in S_X$. This is the map that sends each $x \in X$ to $\alpha (\beta (x))$. 

\textbf{(d)} If $\alpha \in S_X$ and $i \in \mathbb {Z}$, then $\alpha ^i$ shall denote the $i$-th power of $\alpha $ in the group $S_X$. Note that $\alpha ^i = \underbrace{\alpha \circ \alpha \circ \cdots \circ \alpha }_{i\text{ times}}$ if $i \ge 0$. Also, $\alpha ^0 = \operatorname {id}_X$. Also, $\alpha ^{-1}$ is the inverse of $\alpha $ in the group $S_X$, that is, the inverse of the map $\alpha $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.filling
def.sf.filling

\leanhelper  A \emph{filling} of a skew Young diagram $Y(\lambda /\mu )$ is a function $f : Y(\lambda /\mu ) \to [N]$. A filling is \emph{semistandard} if it satisfies the row-weak and column-strict conditions. The \emph{filling monomial} is $x_f = \prod _{c \in Y(\lambda /\mu )} x_{f(c)}$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.hsymm-ext
def.sf.hsymm-ext

\leanhelper  The extended $h_n$: $h_n = 0$ for $n < 0$, $h_0 = 1$. This is needed since the Jacobi–Trudi formula may have negative indices.

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.npar-skewyoungdiagram
def.sf.Npar-skewYoungDiagram

\leanhelper  The \emph{skew Young diagram} $Y(\lambda /\mu )$ for $N$-partitions $\lambda , \mu $ is the set difference $Y(\lambda ) \setminus Y(\mu )$, consisting of cells $(i, j)$ with $\mu _i \leq j < \lambda _i$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.npar-youngdiagram
def.sf.Npar-youngDiagram

\leanhelper  The \emph{Young diagram} $Y(\lambda )$ of an $N$-partition $\lambda $ is the finite set of cells 

\[  Y(\lambda ) = \{ (i, j) : i \in [N],\;  0 \leq j < \lambda _i\} .  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.row-partition
def.sf.row-partition

\leanhelper  The \emph{row partition} $(n, 0, 0, \ldots , 0)$ with $n$ boxes in the first row. This is the partition corresponding to $h_n$. Requires $N > 0$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.schur
def.sf.schur

Let $\lambda $ be an $N$-partition. We define the \emph{Schur polynomial} $s_{\lambda }\in \mathcal{P}$ by

\[  s_{\lambda }:=\sum _{T\in \operatorname *{SSYT}\left( \lambda \right) }x_{T}.  \]

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.ytab.skew-xt
def.sf.ytab.skew-xT

Let $\lambda $ and $\mu $ be two $N$-partitions. If $T$ is any Young tableau of shape $\lambda /\mu $, then we define the corresponding monomial

\[  x_{T}:=\prod _{c\text{ is a box of }Y\left( \lambda /\mu \right) }x_{T\left( c\right) }=\prod _{\left( i,j\right) \in Y\left( \lambda /\mu \right) }x_{T\left( i,j\right) }=\prod _{k=1}^{N}x_{k}^{\left( \text{\#  of times }k\text{ appears in }T\right) }.  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.ytab.xt
def.sf.ytab.xT

Let $\lambda $ be an $N$-partition. If $T$ is any Young tableau of shape $\lambda $, then we define the corresponding monomial

\[  x_{T}:=\prod _{c\text{ is a box of }Y\left( \lambda \right) }x_{T\left( c\right) }=\prod _{\left( i,j\right) \in Y\left( \lambda \right) }x_{T\left( i,j\right) }=\prod _{k=1}^{N}x_{k}^{\left( \text{\#  of times }k\text{ appears in }T\right) }.  \]

## VERDICT
{
  "verdict": "faithful",
  "justification": "The target states `\u2200 {N : \u2115} {R : Type u_1} [inst : CommRing R], SymmetricFunctions.schur 0 = 1`, exactly matching \u201cThe Schur polynomial of the zero partition is 1: s\u2080 = 1.\u201d The dependency `schur lam := \u2211 T \u2208 ssytFinset lam, T.toMonomial` agrees with the informal definition `s_\u03bb := \u2211_{T \u2208 SSYT(\u03bb)} x_T`, while `NPartition.zero` has every part equal to `0` and `SSYT.toMonomial` is the product over all cells. The implicit coefficient ring binder `[CommRing R]` supplies the algebraic setting required by the project\u2019s definition of `schur`; it does not add a contentful hypothesis about the zero partition. Quantification over every `N`, including `N = 0`, is at least as general as the blueprint and introduces no restriction."
}