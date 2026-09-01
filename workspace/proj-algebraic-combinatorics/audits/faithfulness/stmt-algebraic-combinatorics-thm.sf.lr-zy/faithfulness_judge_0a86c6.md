## TARGET AlgebraicCombinatorics.littlewoodRichardson (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_1} [inst : CommRing R] {N : ℕ} [IsDomain R] (lam mu nu : Fin N → ℕ),
  AlgebraicCombinatorics.IsNPartition lam →
    AlgebraicCombinatorics.IsNPartition mu →
      AlgebraicCombinatorics.IsNPartition nu →
        AlgebraicCombinatorics.schurPoly nu * AlgebraicCombinatorics.skewSchurPoly lam mu =
          ∑ T, AlgebraicCombinatorics.schurPoly (nu + AlgebraicCombinatorics.contentTableau ↑T)

## PROJECT DEPENDENCY AlgebraicCombinatorics.IsNPartition (def)
{N : ℕ} → (Fin N → ℕ) → Prop

Body:
fun {N} lam => IsNPartition lam

Docstring: An N-partition is a weakly decreasing N-tuple of natural numbers.
(Used throughout the source)

This is an alias for the canonical definition in `NPartition.lean`. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.schurPoly (def)
{R : Type u_1} → [inst : CommRing R] → {N : ℕ} → (Fin N → ℕ) → MvPolynomial (Fin N) R

Body:
fun {R} [CommRing R] {N} lam => AlgebraicCombinatorics.skewSchurPoly lam 0

Docstring: The Schur polynomial s_lam for an N-partition lam.
Defined as s_{lam/0}, i.e., the skew Schur polynomial with empty inner shape.

## Relationship to Other Definitions

This project has two Schur polynomial definitions with different design tradeoffs:

| Definition | File | Input | Ring | Use case |
|------------|------|-------|------|----------|
| `AlgebraicCombinatorics.schurPoly` (this) | LittlewoodRichardson.lean | `Fin N → ℕ` | generic `R` | Littlewood-Richardson rule, generic rings |
| `schurPoly` | SchurBasics.lean | `NPartition N` | `ℤ` | Proofs using Young diagrams, symmetry |

**When to use which:**
- Use **this definition** when you need a generic coefficient ring `R`, when working
  with the Littlewood-Richardson rule, or when you have an unbundled `Fin N → ℕ`.
- Use **`SchurBasics.schurPoly`** when working with Young diagrams, SSYT fillings
  as explicit structures, or proving symmetry properties. It requires `[NeZero N]`
  and uses integer coefficients.

**Equivalence:** The two definitions agree when the partition is valid. See:
- `SSYTEquiv.schurPoly_eq_schur`: relates `SchurBasics.schurPoly` to `SymmetricFunctions.schur`
- `schurPoly_eq_AC_schurPoly`: relates `SchurBasics.schurPoly` to this definition 

## PROJECT DEPENDENCY AlgebraicCombinatorics.skewSchurPoly (def)
{R : Type u_1} → [inst : CommRing R] → {N : ℕ} → (Fin N → ℕ) → (Fin N → ℕ) → MvPolynomial (Fin N) R

Body:
fun {R} [CommRing R] {N} lam mu => ∑ T, AlgebraicCombinatorics.xPow (AlgebraicCombinatorics.contentTableau ↑T)

Docstring: The skew Schur polynomial s_{lam/mu}.
Defined as a sum over semistandard tableaux of shape lam/mu:
s_{lam/mu} = ∑_{T semistandard of shape lam/mu} x^(cont(T))

Note: This is a finite sum since there are finitely many semistandard tableaux
of any given shape (entries are bounded by N).

## Relationship to Other Definitions

This project has two skew Schur polynomial definitions with different design tradeoffs:

| Definition | File | Input | Ring | Use case |
|------------|------|-------|------|----------|
| `AlgebraicCombinatorics.skewSchurPoly` (this) | LittlewoodRichardson.lean | `Fin N → ℕ` | generic `R` | Littlewood-Richardson rule, generic rings |
| `skewSchurPoly` | SchurBasics.lean | `NPartition N` | `ℤ` | Proofs using skew diagrams, symmetry |

**When to use which:**
- Use **this definition** when you need a generic coefficient ring `R`, when working
  with the Littlewood-Richardson rule, or when you have an unbundled `Fin N → ℕ`.
- Use **`SchurBasics.skewSchurPoly`** when working with skew Young diagrams, SSYT
  fillings as explicit structures, or proving symmetry properties. It requires
  `[NeZero N]` and uses integer coefficients.

**Equivalence:** See `SSYTEquiv.lean` for the bridge between these definitions. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.Tableau (def)
{N : ℕ} → (Fin N → ℕ) → (Fin N → ℕ) → Type

Body:
fun {N} lam mu => { c // c ∈ AlgebraicCombinatorics.skewYoungDiagram lam mu } → Fin N

Docstring: A tableau of shape lam/mu is a function from cells to [N]. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.IsYamanouchi (def)
{N : ℕ} → {lam mu : Fin N → ℕ} → (Fin N → ℕ) → AlgebraicCombinatorics.Tableau lam mu → Prop

Body:
fun {N} {lam mu} nu T =>
  AlgebraicCombinatorics.IsSemistandard T ∧
    ∀ j > 0, AlgebraicCombinatorics.IsNPartition (nu + AlgebraicCombinatorics.contentColGeq T j)

Docstring: A semistandard tableau T of shape λ/μ is ν-Yamanouchi if for each positive integer j,
the N-tuple ν + cont(col_{≥j}(T)) is an N-partition (i.e., weakly decreasing).

**Definition (def.sf.yamanouchi)**:
Let λ, μ, ν be three N-partitions. A semistandard tableau T of shape λ/μ is said to be
ν-Yamanouchi if for each positive integer j, the N-tuple ν + cont(col_{≥j}T) ∈ ℕ^N is
an N-partition (i.e., weakly decreasing).

**Key properties:**
- The condition ensures that as we process the tableau column by column from right to left,
  starting with tally ν, the running tally always remains weakly decreasing.
- For j = 1, we get that ν + cont(T) is an N-partition (see `IsYamanouchi.isNPartition_add_content`).
- A 0-Yamanouchi tableau (also called a "ballot tableau") has content that is itself an N-partition.

**Voting interpretation (rmk.sf.yamanouchi.votes):**
Think of each entry i in T as a vote for candidate i. Starting with tally ν and counting votes
column by column from right to left, the tally must remain weakly decreasing at every step.
Since columns have distinct entries (strictly increasing), no candidate gains more than one
vote at a time. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.yamanouchiTableau_fintype (def)
{N : ℕ} → (lam mu nu : Fin N → ℕ) → Fintype { T // AlgebraicCombinatorics.IsYamanouchi nu T }

Body:
fun {N} lam mu nu =>
  have h := ⋯;
  h.fintype

Docstring: The type of Yamanouchi tableaux of a given shape is finite.
This follows from the finiteness of tableaux (Yamanouchi tableaux are a subset). 

## PROJECT DEPENDENCY AlgebraicCombinatorics.contentTableau (def)
{N : ℕ} → {lam mu : Fin N → ℕ} → AlgebraicCombinatorics.Tableau lam mu → Fin N → ℕ

Body:
fun {N} {lam mu} T i => Nat.card { c // T c = i }

Docstring: **Definition (def.sf.content)**: The content of a tableau T is the N-tuple counting
occurrences of each value.

For a tableau T of shape λ/μ, we define the content of T to be the N-tuple
(a₁, a₂, ..., a_N), where aᵢ = (# of i's in T) = (# of boxes c of T such that T(c) = i).

We denote this N-tuple by cont(T).

**Example**: If N=5, then cont([[1,1,2],[4]]) = (2,1,0,1,0).

**Key property** (eq.def.sf.content.xT=): x_T = x^(cont(T)) for any tableau T.
(Both sides equal ∏ᵢ xᵢ^(# of i's in T).) 

## PROJECT DEPENDENCY IsNPartition (def)
{N : ℕ} → (Fin N → ℕ) → Prop

Body:
fun {N} lam => ∀ (i j : Fin N), i ≤ j → lam j ≤ lam i

Docstring: An N-partition predicate: an N-tuple is an N-partition if it is weakly decreasing.
This is equivalent to `Antitone` for functions `Fin N → ℕ`.
(Used throughout the source) 

## PROJECT DEPENDENCY AlgebraicCombinatorics.IsSemistandard (def)
{N : ℕ} → {lam mu : Fin N → ℕ} → AlgebraicCombinatorics.Tableau lam mu → Prop

Body:
fun {N} {lam mu} T =>
  (∀ (c₁ c₂ : { c // c ∈ AlgebraicCombinatorics.skewYoungDiagram lam mu }),
      (↑c₁).1 = (↑c₂).1 → (↑c₁).2 < (↑c₂).2 → T c₁ ≤ T c₂) ∧
    ∀ (c₁ c₂ : { c // c ∈ AlgebraicCombinatorics.skewYoungDiagram lam mu }),
      (↑c₁).2 = (↑c₂).2 → (↑c₁).1 < (↑c₂).1 → T c₁ < T c₂

Docstring: A tableau is semistandard if entries weakly increase along rows
and strictly increase down columns. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.semistandardTableau_fintype (def)
{N : ℕ} → (lam mu : Fin N → ℕ) → Fintype { T // AlgebraicCombinatorics.IsSemistandard T }

Body:
fun {N} lam mu => Fintype.subtype (Finset.filter AlgebraicCombinatorics.IsSemistandard Finset.univ) ⋯

Docstring: The type of semistandard tableaux of a given shape is finite.
This follows from the fact that entries are bounded by N and the shape is finite. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.xPow (def)
{R : Type u_1} → [inst : CommRing R] → {N : ℕ} → (Fin N → ℕ) → MvPolynomial (Fin N) R

Body:
fun {R} [CommRing R] {N} α => AlgebraicCombinatorics.SymmetricFunctions.monomialExp α

Docstring: x^α = ∏ᵢ xᵢ^(αᵢ) for an N-tuple α.

This is an alias for `AlgebraicCombinatorics.SymmetricFunctions.monomialExp` from MonomialSymmetric.lean.
The two definitions are identical: both equal `∏ i, X i ^ α i`.

See also: `xPow_eq_monomialExp` for the equivalence lemma. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.skewYoungDiagram (def)
{N : ℕ} → (Fin N → ℕ) → (Fin N → ℕ) → Set (Fin N × ℕ)

Body:
fun {N} lam mu => {c | mu c.1 < c.2 ∧ c.2 ≤ lam c.1}

Docstring: The skew Young diagram Y(lam/mu) as a set of cells.
A cell (i,j) is in Y(lam/mu) if mu_i < j ≤ lam_i.

**This is the `Set` version with 1-indexed columns (textbook convention).**
The first column is j = 1, not j = 0.

For the canonical `Finset` version with 0-indexed columns, see:
- `NPartition.skewYoungDiagram` in NPartition.lean (canonical, no `[NeZero N]` required)
- `skewYoungDiagram` in SchurBasics.lean (duplicate, requires `[NeZero N]`)

Comparison:
- Here: (i, j) ∈ Y(λ/μ) iff μ_i < j ≤ λ_i (1-indexed)
- NPartition/SchurBasics: (i, j) ∈ Y(λ/μ) iff μ_i ≤ j < λ_i (0-indexed)

The bijection between them is: (i, j) here ↔ (i, j-1) in NPartition/SchurBasics.
See `SchurBasics.mem_skewYoungDiagram_iff_mem_LR_shifted` for the conversion lemma. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.contentColGeq (def)
{N : ℕ} → {lam mu : Fin N → ℕ} → AlgebraicCombinatorics.Tableau lam mu → ℕ → Fin N → ℕ

Body:
fun {N} {lam mu} T j i => Nat.card { c // T ⟨↑c, ⋯⟩ = i }

Docstring: The content of a restricted tableau col_{≥j}(T).
Counts occurrences of each value in columns j and beyond. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.isSemistandard_decidable (def)
{N : ℕ} →
  {lam mu : Fin N → ℕ} →
    (T : AlgebraicCombinatorics.Tableau lam mu) → Decidable (AlgebraicCombinatorics.IsSemistandard T)

Body:
fun {N} {lam mu} T => id inferInstance

Docstring: IsSemistandard is decidable since it's a conjunction of foralls over finite types. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.tableau_fintype (def)
{N : ℕ} → (lam mu : Fin N → ℕ) → Fintype (AlgebraicCombinatorics.Tableau lam mu)

Body:
fun {N} lam mu => id inferInstance

Docstring: The type of all tableaux of a given shape is finite.
This follows from the fact that entries are in Fin N and the shape is finite. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SymmetricFunctions.monomialExp (def)
{R : Type u_1} → [inst : CommSemiring R] → {N : ℕ} → (Fin N → ℕ) → MvPolynomial (Fin N) R

Body:
fun {R} [CommSemiring R] {N} a => ∏ i, MvPolynomial.X i ^ a i

Docstring: The monomial x^a = x₁^{a₁} x₂^{a₂} ⋯ x_N^{a_N} for a tuple a ∈ ℕ^N.
(Definition def.sf.sort (a)) 

## PROJECT DEPENDENCY AlgebraicCombinatorics.skewYoungDiagram_fintype (def)
{N : ℕ} → (lam mu : Fin N → ℕ) → Fintype { c // c ∈ AlgebraicCombinatorics.skewYoungDiagram lam mu }

Body:
fun {N} lam mu => ⋯.fintype

Docstring: The set of cells in the skew Young diagram as a Fintype. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.skewYoungDiagram_finite (theorem)
∀ {N : ℕ} (lam mu : Fin N → ℕ), (AlgebraicCombinatorics.skewYoungDiagram lam mu).Finite

Docstring: The skew Young diagram is finite. 

## BASE-LIBRARY REF CommRing
Type u → Type u

Docstring: A commutative ring is a ring with commutative multiplication. 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF IsDomain
(α : Type u) → [Semiring α] → Prop

Docstring: A domain is a nontrivial semiring such that multiplication by a nonzero element
is cancellative on both sides. In other words, a nontrivial semiring `R` satisfying
`∀ {a b c : R}, a ≠ 0 → a * b = a * c → b = c` and
`∀ {a b c : R}, b ≠ 0 → a * b = c * b → a = c`.

This is implemented as a mixin for `Semiring α`.
To obtain an integral domain use `[CommRing α] [IsDomain α]`. 

## BASE-LIBRARY REF CommSemiring.toSemiring
{R : Type u} → [self : CommSemiring R] → Semiring R

## BASE-LIBRARY REF CommRing.toCommSemiring
{α : Type u} → [s : CommRing α] → CommSemiring α

## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


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

## BASE-LIBRARY REF MvPolynomial.instCommRingMvPolynomial
{R : Type u} → {σ : Type u_1} → [inst : CommRing R] → CommRing (MvPolynomial σ R)

## BASE-LIBRARY REF Finset.sum
{ι : Type u_1} → {M : Type u_3} → [AddCommMonoid M] → Finset ι → (ι → M) → M

Docstring: `∑ x ∈ s, f x` is the sum of `f x` as `x` ranges over the elements
of the finite set `s`.

When the index type is a `Fintype`, the notation `∑ x, f x`, is a shorthand for
`∑ x ∈ Finset.univ, f x`. 

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

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.toAddCommMonoid
{α : Type u} → [self : NonUnitalNonAssocSemiring α] → AddCommMonoid α

## BASE-LIBRARY REF Finset.univ
{α : Type u_1} → [Fintype α] → Finset α

Docstring: `univ` is the universal finite set of type `Finset α` implied from
the assumption `Fintype α`. 

## BASE-LIBRARY REF HAdd.hAdd
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HAdd α β γ] → α → β → γ

Docstring: `a + b` computes the sum of `a` and `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `+` in identifiers is `add`.

## BASE-LIBRARY REF instHAdd
{α : Type u_1} → [Add α] → HAdd α α α

## BASE-LIBRARY REF Pi.instAdd
{ι : Type u_1} → {M : ι → Type u_5} → [(i : ι) → Add (M i)] → Add ((i : ι) → M i)

## BASE-LIBRARY REF instAddNat
Add ℕ

## BASE-LIBRARY REF Subtype.val
{α : Sort u} → {p : α → Prop} → Subtype p → α

Docstring: The value in the underlying type that satisfies the predicate.


## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF Zero.toOfNat0
{α : Type u_1} → [Zero α] → OfNat α 0

## BASE-LIBRARY REF Pi.instZero
{ι : Type u_1} → {M : ι → Type u_5} → [(i : ι) → Zero (M i)] → Zero ((i : ι) → M i)

## BASE-LIBRARY REF MulZeroClass.toZero
{M₀ : Type u} → [self : MulZeroClass M₀] → Zero M₀

## BASE-LIBRARY REF Nat.instMulZeroClass
MulZeroClass ℕ

## BASE-LIBRARY REF Prod
Type u → Type v → Type (max u v)

Docstring: The product type, usually written `α × β`. Product types are also called pair or tuple types.
Elements of this type are pairs in which the first element is an `α` and the second element is a
`β`.

Products nest to the right, so `(x, y, z) : α × β × γ` is equivalent to `(x, (y, z)) : α × (β × γ)`.


Conventions for notations in identifiers:

 * The recommended spelling of `×` in identifiers is `Prod`.

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

## BASE-LIBRARY REF instLTNat
LT ℕ

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

## BASE-LIBRARY REF Fintype
Type u_4 → Type u_4

Docstring: `Fintype α` means that `α` is finite, i.e. there are only
finitely many distinct elements of type `α`. The evidence of this
is a finset `elems` (a list up to permutation without duplicates),
together with a proof that everything of type `α` is in the list. 

## BASE-LIBRARY REF Set.Finite
{α : Type u} → Set α → Prop

Docstring: A set is finite if the corresponding `Subtype` is finite,
i.e., if there exists a natural `n : ℕ` and an equivalence `s ≃ Fin n`. 

## BASE-LIBRARY REF setOf
{α : Type u} → (α → Prop) → Set α

Docstring: Turn a predicate `p : α → Prop` into a set, also written as `{x | p x}` 

## BASE-LIBRARY REF Set.Finite.fintype
{α : Type u} → {s : Set α} → s.Finite → Fintype ↑s

Docstring: A finite set coerced to a type is a `Fintype`.
This is the `Fintype` projection for a `Set.Finite`.

Note that because `Finite` isn't a typeclass, this definition will not fire if it
is made into an instance 

## BASE-LIBRARY REF Nat.card
Type u_3 → ℕ

Docstring: `Nat.card α` is the cardinality of `α` as a natural number.
If `α` is infinite, `Nat.card α = 0`. 

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

## BASE-LIBRARY REF Prod.fst
{α : Type u} → {β : Type v} → α × β → α

Docstring: The first element of a pair. 

## BASE-LIBRARY REF LT.lt
{α : Type u} → [self : LT α] → α → α → Prop

Docstring: The less-than relation: `x < y` 

Conventions for notations in identifiers:

 * The recommended spelling of `<` in identifiers is `lt`.

## BASE-LIBRARY REF Prod.snd
{α : Type u} → {β : Type v} → α × β → β

Docstring: The second element of a pair. 

## BASE-LIBRARY REF instLTFin
{n : ℕ} → LT (Fin n)

## BASE-LIBRARY REF Fintype.subtype
{α : Type u_1} → {p : α → Prop} → (s : Finset α) → (∀ (x : α), x ∈ s ↔ p x) → Fintype { x // p x }

Docstring: Given a predicate that can be represented by a finset, the subtype
associated to the predicate is a fintype. 

## BASE-LIBRARY REF Finset.filter
{α : Type u_1} → (p : α → Prop) → [DecidablePred p] → Finset α → Finset α

Docstring: `Finset.filter p s` is the set of elements of `s` that satisfy `p`.

For example, one can use `s.filter (· ∈ t)` to get the intersection of `s` with `t : Set α`
as a `Finset α` (when a `DecidablePred (· ∈ t)` instance is available). 

## BASE-LIBRARY REF GE.ge
{α : Type u} → [LE α] → α → α → Prop

Docstring: `a ≥ b` is an abbreviation for `b ≤ a`. 

Conventions for notations in identifiers:

 * The recommended spelling of `≥` in identifiers is `ge`.

 * The recommended spelling of `>=` in identifiers is `ge` (prefer `≥` over `>=`).

## BASE-LIBRARY REF Subtype.mk
{α : Sort u} → {p : α → Prop} → (val : α) → p val → Subtype p

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


## BASE-LIBRARY REF id
{α : Sort u} → α → α

Docstring: The identity function. `id` takes an implicit argument `α : Sort u`
(a type in any universe), and an argument `a : α`, and returns `a`.

Although this may look like a useless function, one application of the identity
function is to explicitly put a type on an expression. If `e` has type `T`,
and `T'` is definitionally equal to `T`, then `@id T' e` typechecks, and Lean
knows that this expression has type `T'` rather than `T`. This can make a
difference for typeclass inference, since `T` and `T'` may have different
typeclass instances on them. `show T' from e` is sugar for an `@id T' e`
expression.


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


## BASE-LIBRARY REF instDecidableAnd
{p q : Prop} → [dp : Decidable p] → [dq : Decidable q] → Decidable (p ∧ q)

## BASE-LIBRARY REF Fintype.decidableForallFintype
{α : Type u_1} → {p : α → Prop} → [DecidablePred p] → [Fintype α] → Decidable (∀ (a : α), p a)

## BASE-LIBRARY REF forall_prop_decidable
{p : Prop} → (P : p → Prop) → [Decidable p] → [(h : p) → Decidable (P h)] → Decidable (∀ (h : p), P h)

## BASE-LIBRARY REF instDecidableEqFin
(n : ℕ) → DecidableEq (Fin n)

## BASE-LIBRARY REF Nat.decLt
(n m : ℕ) → Decidable (n < m)

Docstring: A decision procedure for strict inequality of natural numbers, usually accessed via the
`DecidableLT Nat` instance.

Examples:
 * `(if 3 < 4 then "yes" else "no") = "yes"`
 * `(if 4 < 4 then "yes" else "no") = "no"`
 * `(if 6 < 4 then "yes" else "no") = "no"`
 * `show 5 < 12 by decide`


## BASE-LIBRARY REF Fin.decLe
{n : ℕ} → (a b : Fin n) → Decidable (a ≤ b)

## BASE-LIBRARY REF instDecidableEqNat
DecidableEq ℕ

## BASE-LIBRARY REF Fin.decLt
{n : ℕ} → (a b : Fin n) → Decidable (a < b)

## BASE-LIBRARY REF Pi.instFintype
{α : Type u_3} →
  {β : α → Type u_4} → [DecidableEq α] → [Fintype α] → [(a : α) → Fintype (β a)] → Fintype ((a : α) → β a)

Docstring: A dependent product of fintypes, indexed by a fintype, is a fintype. 

## BASE-LIBRARY REF Subtype.instDecidableEq
{α : Sort u} → {p : α → Prop} → [DecidableEq α] → DecidableEq { x // p x }

## BASE-LIBRARY REF instDecidableEqProd
{α : Type u_1} → {β : Type u_2} → [DecidableEq α] → [DecidableEq β] → DecidableEq (α × β)

## BASE-LIBRARY REF Fin.fintype
(n : ℕ) → Fintype (Fin n)

## BASE-LIBRARY REF CommSemiring
Type u → Type u

Docstring: A commutative semiring is a semiring with commutative multiplication. 

## BASE-LIBRARY REF Finset.prod
{ι : Type u_1} → {M : Type u_3} → [CommMonoid M] → Finset ι → (ι → M) → M

Docstring: `∏ x ∈ s, f x` is the product of `f x` as `x` ranges over the elements of the finite set `s`.

When the index type is a `Fintype`, the notation `∏ x, f x`, is a shorthand for
`∏ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF CommSemiring.toCommMonoid
{R : Type u} → [self : CommSemiring R] → CommMonoid R

## BASE-LIBRARY REF MvPolynomial.commSemiring
{R : Type u} → {σ : Type u_1} → [inst : CommSemiring R] → CommSemiring (MvPolynomial σ R)

## BASE-LIBRARY REF HPow.hPow
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HPow α β γ] → α → β → γ

Docstring: `a ^ b` computes `a` to the power of `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `^` in identifiers is `pow`.

## BASE-LIBRARY REF instHPow
{α : Type u_1} → {β : Type u_2} → [Pow α β] → HPow α β α

## BASE-LIBRARY REF Monoid.toNatPow
{M : Type u_2} → [Monoid M] → Pow M ℕ

## BASE-LIBRARY REF MonoidWithZero.toMonoid
{M₀ : Type u} → [self : MonoidWithZero M₀] → Monoid M₀

## BASE-LIBRARY REF Semiring.toMonoidWithZero
{α : Type u} → [self : Semiring α] → MonoidWithZero α

## BASE-LIBRARY REF MvPolynomial.X
{R : Type u} → {σ : Type u_1} → [inst : CommSemiring R] → σ → MvPolynomial σ R

Docstring: `X n` is the degree `1` monomial $X_n$. 

## INFORMAL STATEMENT
Zelevinsky’s generalized Littlewood–Richardson rule, in Yamanouchi form

Let $\lambda ,\mu ,\nu $ be three $N$-partitions. Then,

\begin{equation}  s_{\nu }\cdot s_{\lambda /\mu }=\sum _{\substack {T\text{ is a }\nu \text{-Yamanouchi}\\ \text{semistandard tableau}\\ \text{of shape }\lambda /\mu }}s_{\nu +\operatorname *{cont}T}. \end{equation}

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.col-tab
def.sf.col-tab

Let $\lambda $ and $\mu $ be two $N$-partitions. Let $T$ be a tableau of shape $\lambda /\mu $. Let $j$ be a positive integer. Then, $\operatorname {col}_{\geq j}T$ means the restriction of $T$ to columns $j,j+1,j+2,\ldots $ (that is, the result of removing the first $j-1$ columns from $T$). Formally speaking, this means the restriction of the map $T$ to the set $\left\{  \left( u,v\right) \in Y\left( \lambda /\mu \right) \  \mid \  v\geq j\right\}  $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.content
def.sf.content

Let $\lambda $ and $\mu $ be two $N$-partitions. Let $T$ be a tableau of shape $\lambda /\mu $. We define the \emph{content} of $T$ to be the $N$-tuple $\left( a_{1},a_{2},\ldots ,a_{N}\right) $, where

\[  a_{i}:=\left( \text{\#  of }i\text{'s in }T\right) =\left( \text{\#  of boxes }c\text{ of }T\text{ such that }T\left( c\right) =i\right) .  \]

 We denote this $N$-tuple by $\operatorname *{cont}T$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.skew-schur
def.sf.skew-schur

Let $\lambda $ and $\mu $ be two $N$-partitions. We define the \emph{skew Schur polynomial} $s_{\lambda /\mu }\in \mathcal{P}$ by

\[  s_{\lambda /\mu }:=\sum _{T\in \operatorname *{SSYT}\left( \lambda /\mu \right) }x_{T}.  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.skew-tab
def.sf.skew-tab

Let $\lambda $ and $\mu $ be two $N$-partitions such that $\mu \subseteq \lambda $. A \emph{Young tableau} of shape $\lambda /\mu $ means a way of filling the boxes of $Y\left( \lambda /\mu \right) $ with elements of $\left[ N\right] $ (one element per box). Formally speaking, it is defined as a map $T:Y\left( \lambda /\mu \right) \rightarrow \left[ N\right] $. 

Young tableaux of shape $\lambda /\mu $ are often called \emph{skew Young tableaux}. 

If we don’t have $\mu \subseteq \lambda $, then we agree that there are no Young tableaux of shape $\lambda /\mu $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.tuple-addition
def.sf.tuple-addition

\textbf{(a)} We let $\mathbf{0}$ denote the $N$-tuple $\left( 0,0,\ldots ,0\right) \in \mathbb {N}^{N}$. 

\medskip 

\textbf{(b)} Let $\alpha =\left( \alpha _{1},\alpha _{2},\ldots ,\alpha _{N}\right) $ and $\beta =\left( \beta _{1},\beta _{2},\ldots ,\beta _{N}\right) $ be two $N$-tuples in $\mathbb {N}^{N}$. Then, we set

\begin{align*}  \alpha +\beta &  :=\left( \alpha _{1}+\beta _{1},\alpha _{2}+\beta _{2},\ldots ,\alpha _{N}+\beta _{N}\right) \  \  \  \  \  \  \  \  \  \  \text{and}\\ \alpha -\beta &  :=\left( \alpha _{1}-\beta _{1},\alpha _{2}-\beta _{2},\ldots ,\alpha _{N}-\beta _{N}\right) . \end{align*}

 Note that $\alpha +\beta \in \mathbb {N}^{N}$, whereas $\alpha -\beta \in \mathbb {Z}^{N}$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.yamanouchi
def.sf.yamanouchi

Let $\lambda ,\mu ,\nu $ be three $N$-partitions. A semistandard tableau $T$ of shape $\lambda /\mu $ is said to be $\nu $-\emph{Yamanouchi} (this is an adjective) if for each positive integer $j$, the $N$-tuple $\nu +\operatorname *{cont}\left( \operatorname {col}_{\geq j}T\right) \in \mathbb {N}^{N}$ is an $N$-partition (i.e., weakly decreasing).

## VERDICT
{
  "verdict": "drift",
  "justification": "The decisive mismatch enters through `AlgebraicCombinatorics.Tableau`, whose body is unconditionally `fun {N} lam mu => { c // c \u2208 skewYoungDiagram lam mu } \u2192 Fin N`. Thus, when `\u03bc \u2288 \u03bb`, Lean can still have tableaux\u2014for example, if the cell subtype is empty, there is an empty function\u2014whereas the informal definition explicitly says: \u201cIf we don\u2019t have \u03bc \u2286 \u03bb, then we agree that there are no Young tableaux of shape \u03bb/\u03bc.\u201d Consequently, both `skewSchurPoly lam mu := \u2211 T, ...` and the target\u2019s Yamanouchi sum range over formally existing tableaux in cases where the blueprint requires an empty range. This matters because the target assumes only `IsNPartition lam`, `IsNPartition mu`, and `IsNPartition nu`, with no `\u03bc \u2286 \u03bb` hypothesis. To make the statement faithful, `Tableau lam mu` (and hence the semistandard/Yamanouchi and skew-Schur definitions depending on it) should be empty whenever `\u03bc \u2288 \u03bb`; alternatively one could add `\u03bc \u2286 \u03bb`, but that would narrow the blueprint, which explicitly specifies behavior without containment. The binder `[IsDomain R]` is also not stated by the blueprint, but the package does not fix the coefficient ring denoted by its `\ud835\udcab`; the tableau-definition mismatch alone decisively establishes drift."
}