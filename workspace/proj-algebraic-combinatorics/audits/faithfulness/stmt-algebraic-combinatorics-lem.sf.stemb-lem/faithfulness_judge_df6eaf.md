## TARGET AlgebraicCombinatorics.stembridgeLemma (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_1} [inst : CommRing R] {N : ℕ} (lam mu nu : Fin N → ℕ),
  AlgebraicCombinatorics.IsNPartition lam →
    AlgebraicCombinatorics.IsNPartition mu →
      AlgebraicCombinatorics.IsNPartition nu →
        AlgebraicCombinatorics.alternant (nu + AlgebraicCombinatorics.rho N) *
            AlgebraicCombinatorics.skewSchurPoly lam mu =
          ∑ T,
            AlgebraicCombinatorics.alternant
              (nu + AlgebraicCombinatorics.contentTableau ↑T + AlgebraicCombinatorics.rho N)

Docstring: **Stembridge's Lemma (lem.sf.stemb-lem)**: The key technical lemma for
proving the Littlewood-Richardson rule.

For N-partitions lam, mu, nu:
a_{nu+ρ} · s_{lam/mu} = ∑_{T nu-Yamanouchi of shape lam/mu} a_{nu + cont(T) + ρ}

The sum on the RHS is over all nu-Yamanouchi semistandard tableaux T of shape lam/mu.
Note: The sum is finite since there are finitely many semistandard tableaux of any shape.

## Proof Strategy (from Stembridge 1997)

The proof uses a sign-reversing involution on non-Yamanouchi tableaux:

**Step 1**: Express the LHS using the alternant definition and symmetry of `skewSchurPoly`:
```
a_{ν+ρ} · s_{λ/μ} = ∑_{σ ∈ S_N} (-1)^σ · σ(x^{ν+ρ}) · s_{λ/μ}
                  = ∑_{σ ∈ S_N} (-1)^σ · σ(x^{ν+ρ} · s_{λ/μ})  (since s_{λ/μ} is symmetric)
```

**Step 2**: Expand `s_{λ/μ}` as a sum over semistandard tableaux:
```
= ∑_{T ∈ SSYT(λ/μ)} ∑_{σ ∈ S_N} (-1)^σ · x^{σ(ν+cont(T)+ρ)}
= ∑_{T ∈ SSYT(λ/μ)} a_{ν+cont(T)+ρ}
```

**Step 3**: Define a sign-reversing involution on non-Yamanouchi tableaux:
For T not ν-Yamanouchi:
- Let j be the largest "violator" column (where ν + cont(col≥j T) fails to be a partition)
- Let k be the smallest "misstep" index (where the partition condition fails)
- Apply the Bender-Knuth involution β_k to columns 1, ..., j-1 of T
- This gives T* with cont(T*) obtained from cont(T) by swapping entries k and k+1

**Step 4**: Show the involution is sign-reversing:
Since cont(T*) differs from cont(T) by swapping entries k and k+1:
```
a_{ν+cont(T*)+ρ} = -a_{ν+cont(T)+ρ}  (by alternant_swap)
```

**Step 5**: Conclude that non-Yamanouchi tableaux cancel in pairs.

## Dependencies

This proof requires:
1. `skewSchurPoly` to be properly defined as ∑_{T ∈ SSYT} x^{cont(T)}
2. `alternant_swap`: swapping two entries negates the alternant
3. `alternant_eq_zero_of_repeated`: equal entries give zero alternant
4. Bender-Knuth involutions β_k on tableaux
5. Properties of the involution (sign-reversing, fixed-point free on non-Yamanouchi)

Reference: [Stembridge, *A concise proof of the Littlewood-Richardson rule*, 2002] 

## PROJECT DEPENDENCY AlgebraicCombinatorics.IsNPartition (def)
{N : ℕ} → (Fin N → ℕ) → Prop

Body:
fun {N} lam => IsNPartition lam

Docstring: An N-partition is a weakly decreasing N-tuple of natural numbers.
(Used throughout the source)

This is an alias for the canonical definition in `NPartition.lean`. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.alternant (def)
{R : Type u_1} → [inst : CommRing R] → {N : ℕ} → (Fin N → ℕ) → MvPolynomial (Fin N) R

Body:
fun {R} [CommRing R] {N} α => ∑ σ, Equiv.Perm.sign σ • AlgebraicCombinatorics.xPow (α ∘ ⇑σ)

Docstring: The alternant a_α = ∑_{σ ∈ S_N} sign(σ) · x^(σ·α).
Here σ·α means (α_{σ(1)}, α_{σ(2)}, ..., α_{σ(N)}).

**Equivalence with SchurBasics.alternant:**
This sum-based definition equals the determinant-based definition in
`alternant` (from SchurBasics.lean). See `alternant_eq_det` for the proof
that this equals `det(alternantMatrix α)`. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.rho (def)
(N : ℕ) → Fin N → ℕ

Body:
fun N i => N - 1 - ↑i

Docstring: The staircase partition ρ = (N-1, N-2, ..., 1, 0). 

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

## PROJECT DEPENDENCY AlgebraicCombinatorics.xPow (def)
{R : Type u_1} → [inst : CommRing R] → {N : ℕ} → (Fin N → ℕ) → MvPolynomial (Fin N) R

Body:
fun {R} [CommRing R] {N} α => AlgebraicCombinatorics.SymmetricFunctions.monomialExp α

Docstring: x^α = ∏ᵢ xᵢ^(αᵢ) for an N-tuple α.

This is an alias for `AlgebraicCombinatorics.SymmetricFunctions.monomialExp` from MonomialSymmetric.lean.
The two definitions are identical: both equal `∏ i, X i ^ α i`.

See also: `xPow_eq_monomialExp` for the equivalence lemma. 

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

## PROJECT DEPENDENCY AlgebraicCombinatorics.SymmetricFunctions.monomialExp (def)
{R : Type u_1} → [inst : CommSemiring R] → {N : ℕ} → (Fin N → ℕ) → MvPolynomial (Fin N) R

Body:
fun {R} [CommSemiring R] {N} a => ∏ i, MvPolynomial.X i ^ a i

Docstring: The monomial x^a = x₁^{a₁} x₂^{a₂} ⋯ x_N^{a_N} for a tuple a ∈ ℕ^N.
(Definition def.sf.sort (a)) 

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

## BASE-LIBRARY REF MvPolynomial.instCommRingMvPolynomial
{R : Type u} → {σ : Type u_1} → [inst : CommRing R] → CommRing (MvPolynomial σ R)

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

## BASE-LIBRARY REF Subtype.val
{α : Sort u} → {p : α → Prop} → Subtype p → α

Docstring: The value in the underlying type that satisfies the predicate.


## BASE-LIBRARY REF Equiv.Perm
Sort u_1 → Sort (max 1 u_1)

Docstring: `Perm α` is the type of bijections from `α` to itself. 

## BASE-LIBRARY REF Equiv.instFintype
{α : Type u_1} → {β : Type u_2} → [DecidableEq α] → [DecidableEq β] → [Fintype α] → [Fintype β] → Fintype (α ≃ β)

## BASE-LIBRARY REF instDecidableEqFin
(n : ℕ) → DecidableEq (Fin n)

## BASE-LIBRARY REF Fin.fintype
(n : ℕ) → Fintype (Fin n)

## BASE-LIBRARY REF HSMul.hSMul
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HSMul α β γ] → α → β → γ

Docstring: `a • b` computes the product of `a` and `b`.
The meaning of this notation is type-dependent, but it is intended to be used for left actions. 

Conventions for notations in identifiers:

 * The recommended spelling of `•` in identifiers is `smul`.

## BASE-LIBRARY REF Units
(α : Type u) → [Monoid α] → Type u

Docstring: Units of a `Monoid`, bundled version. Notation: `αˣ`.

An element of a `Monoid` is a unit if it has a two-sided inverse.
This version bundles the inverse element so that it can be computed.
For a predicate see `IsUnit`. 

## BASE-LIBRARY REF Int
Type

Docstring: The integers.

This type is special-cased by the compiler and overridden with an efficient implementation. The
runtime has a special representation for `Int` that stores “small” signed numbers directly, while
larger numbers use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)). A “small number” is an integer that can be encoded with one fewer bits
than the platform's pointer size (i.e. 63 bits on 64-bit architectures and 31 bits on 32-bit
architectures).


## BASE-LIBRARY REF Int.instMonoid
Monoid ℤ

## BASE-LIBRARY REF instHSMul
{α : Type u_1} → {β : Type u_2} → [SMul α β] → HSMul α β β

## BASE-LIBRARY REF Units.instSMul
{M : Type u_3} → {α : Type u_5} → [inst : Monoid M] → [SMul M α] → SMul Mˣ α

## BASE-LIBRARY REF SubNegMonoid.toZSMul
{M : Type u_2} → [SubNegMonoid M] → SMul ℤ M

## BASE-LIBRARY REF AddGroup.toSubNegMonoid
{A : Type u} → [self : AddGroup A] → SubNegMonoid A

## BASE-LIBRARY REF AddGroupWithOne.toAddGroup
{R : Type u} → [self : AddGroupWithOne R] → AddGroup R

## BASE-LIBRARY REF Ring.toAddGroupWithOne
{R : Type u} → [self : Ring R] → AddGroupWithOne R

## BASE-LIBRARY REF CommRing.toRing
{α : Type u} → [self : CommRing α] → Ring α

## BASE-LIBRARY REF DFunLike.coe
{F : Sort u_1} → {α : outParam (Sort u_2)} → {β : outParam (α → Sort u_3)} → [self : DFunLike F α β] → F → (a : α) → β a

Docstring: The coercion from `F` to a function. 

## BASE-LIBRARY REF MonoidHom
(M : Type u_10) → (N : Type u_11) → [MulOne M] → [MulOne N] → Type (max u_10 u_11)

Docstring: `M →* N` is the type of functions `M → N` that preserve the `MulOne` structure.
`MonoidHom` is used for both monoid and group homomorphisms.

When possible, instead of parametrizing results over `(f : M →* N)`,
you should parametrize over `(F : Type*) [MonoidHomClass F M N] (f : F)`.

When you extend this structure, make sure to extend `MonoidHomClass`.


## BASE-LIBRARY REF MulOneClass.toMulOne
{M : Type u} → [self : MulOneClass M] → MulOne M

## BASE-LIBRARY REF Monoid.toMulOneClass
{M : Type u} → [self : Monoid M] → MulOneClass M

## BASE-LIBRARY REF DivInvMonoid.toMonoid
{G : Type u} → [self : DivInvMonoid G] → Monoid G

## BASE-LIBRARY REF Group.toDivInvMonoid
{G : Type u} → [self : Group G] → DivInvMonoid G

## BASE-LIBRARY REF Equiv.Perm.permGroup
{α : Type u_4} → Group (Equiv.Perm α)

## BASE-LIBRARY REF Units.instMulOneClass
{α : Type u} → [inst : Monoid α] → MulOneClass αˣ

Docstring: Units of a monoid have a multiplication and multiplicative identity. 

## BASE-LIBRARY REF MonoidHom.instFunLike
{M : Type u_4} → {N : Type u_5} → [inst : MulOne M] → [inst_1 : MulOne N] → FunLike (M →* N) M N

## BASE-LIBRARY REF Equiv.Perm.sign
{α : Type u} → [DecidableEq α] → [Fintype α] → Equiv.Perm α →* ℤˣ

Docstring: `SignType.sign` of a permutation returns the signature or parity of a permutation, `1` for even
permutations, `-1` for odd permutations. It is the unique surjective group homomorphism from
`Perm α` to the group with two elements. 

## BASE-LIBRARY REF Function.comp
{α : Sort u} → {β : Sort v} → {δ : Sort w} → (β → δ) → (α → β) → α → δ

Docstring: Function composition, usually written with the infix operator `∘`. A new function is created from
two existing functions, where one function's output is used as input to the other.

Examples:
 * `Function.comp List.reverse (List.drop 2) [3, 2, 4, 1] = [1, 4]`
 * `(List.reverse ∘ List.drop 2) [3, 2, 4, 1] = [1, 4]`


Conventions for notations in identifiers:

 * The recommended spelling of `∘` in identifiers is `comp`.

## BASE-LIBRARY REF EquivLike.toFunLike
{E : Sort u_1} → {α : Sort u_3} → {β : Sort u_4} → [EquivLike E α β] → FunLike E α β

## BASE-LIBRARY REF Equiv.instEquivLike
{α : Sort u} → {β : Sort v} → EquivLike (α ≃ β) α β

## BASE-LIBRARY REF HSub.hSub
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HSub α β γ] → α → β → γ

Docstring: `a - b` computes the difference of `a` and `b`.
The meaning of this notation is type-dependent.
* For natural numbers, this operator saturates at 0: `a - b = 0` when `a ≤ b`. 

Conventions for notations in identifiers:

 * The recommended spelling of `-` in identifiers is `sub` (when used as a binary operator).

## BASE-LIBRARY REF instHSub
{α : Type u_1} → [Sub α] → HSub α α α

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

## BASE-LIBRARY REF Fin.val
{n : ℕ} → Fin n → ℕ

Docstring: The number that is strictly less than `n`.

`Fin.val` is a coercion, so any `Fin n` can be used in a position where a `Nat` is expected.


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

## BASE-LIBRARY REF CommSemiring.toSemiring
{R : Type u} → [self : CommSemiring R] → Semiring R

## BASE-LIBRARY REF MvPolynomial.X
{R : Type u} → {σ : Type u_1} → [inst : CommSemiring R] → σ → MvPolynomial σ R

Docstring: `X n` is the degree `1` monomial $X_n$. 

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

## INFORMAL STATEMENT
Stembridge’s Lemma

Let $\lambda ,\mu ,\nu $ be three $N$-partitions. Then,

\[  a_{\nu +\rho }\cdot s_{\lambda /\mu }=\sum _{\substack {T\text{ is a }\nu \text{-Yamanouchi}\\ \text{semistandard tableau}\\ \text{of shape }\lambda /\mu }}a_{\nu +\operatorname *{cont}T+\rho }.  \]

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.bk-forced-free
Forced and free cells

\leanhelper  Let $T$ be a semistandard tableau and let $k < N-1$. A cell $c = (i,j)$ with $T(c) = k$ is \emph{forced} if there exists a cell $(i+1,j)$ directly below with $T(i+1,j) = k+1$. Similarly for $T(c) = k+1$ with a cell directly above having value~ $k$. Free cells are those that are not forced. 

Among the free cells, the \emph{parenthesis-matching algorithm} classifies each as \emph{matched} or \emph{unmatched}: reading free entries left-to-right in each row, each free $(k{+}1)$ matches with the nearest unmatched free $k$ to its left. Unmatched entries are those remaining after this process.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.bk-involution
Bender–Knuth involution βk

\leanhelper  Let $T$ be a semistandard tableau of shape $\lambda /\mu $ and let $k < N-1$. The \emph{Bender--Knuth involution} $\beta _k(T)$ is obtained from $T$ by swapping only the \emph{unmatched} free $k$’s and unmatched free $(k{+}1)$’s: 

\[  \beta _k(T)(c) = \begin{cases}  k+1 &  \text{if } c \text{ is an unmatched free } k, \\ k &  \text{if } c \text{ is an unmatched free } k{+}1, \\ T(c) &  \text{otherwise.} \end{cases}  \]

 Forced cells and matched free cells are left unchanged.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.bk-prefix
Prefix-restricted Bender–Knuth

\leanhelper  The \emph{prefix-restricted BK involution} $\beta _k^{<j}$ applies the parenthesis-matching swap of $k$ and $k{+}1$ only to cells in columns $< j$. Cells in columns $\geq j$ are left unchanged: 

\[  \beta _k^{<j}(T)(c) = \begin{cases}  k+1 &  \text{if the column of } c \text{ is } < j \text{ and } c \text{ is unmatched free } k \text{ in prefix}, \\ k &  \text{if the column of } c \text{ is } < j \text{ and } c \text{ is unmatched free } k{+}1 \text{ in prefix}, \\ T(c) &  \text{otherwise.} \end{cases}  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.col-tab
def.sf.col-tab

Let $\lambda $ and $\mu $ be two $N$-partitions. Let $T$ be a tableau of shape $\lambda /\mu $. Let $j$ be a positive integer. Then, $\operatorname {col}_{\geq j}T$ means the restriction of $T$ to columns $j,j+1,j+2,\ldots $ (that is, the result of removing the first $j-1$ columns from $T$). Formally speaking, this means the restriction of the map $T$ to the set $\left\{  \left( u,v\right) \in Y\left( \lambda /\mu \right) \  \mid \  v\geq j\right\}  $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.content
def.sf.content

Let $\lambda $ and $\mu $ be two $N$-partitions. Let $T$ be a tableau of shape $\lambda /\mu $. We define the \emph{content} of $T$ to be the $N$-tuple $\left( a_{1},a_{2},\ldots ,a_{N}\right) $, where

\[  a_{i}:=\left( \text{\#  of }i\text{'s in }T\right) =\left( \text{\#  of boxes }c\text{ of }T\text{ such that }T\left( c\right) =i\right) .  \]

 We denote this $N$-tuple by $\operatorname *{cont}T$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.npar
def.sf.Npar

An $N$\emph{-partition} will mean a weakly decreasing $N$-tuple of nonnegative integers. In other words, an $N$-partition means an $N$-tuple $\left( \lambda _{1},\lambda _{2},\ldots ,\lambda _{N}\right) \in \mathbb {N}^{N}$ with $\lambda _{1}\geq \lambda _{2}\geq \cdots \geq \lambda _{N}$. 

The \emph{size} (or weight) of an $N$-partition $\lambda = (\lambda _1, \lambda _2, \ldots , \lambda _N)$ is defined to be $|\lambda | := \lambda _1 + \lambda _2 + \cdots + \lambda _N$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.npar-order
def.sf.Npar-order

\leanhelper  We define a partial order on $N$-partitions by componentwise comparison: $\mu \leq \nu $ iff $\mu _i \leq \nu _i$ for all $i \in [N]$.

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.skew-diag
def.sf.skew-diag

Let $\lambda $ and $\mu $ be two $N$-partitions such that $\mu \subseteq \lambda $. Then, we define the \emph{skew Young diagram} $Y\left( \lambda /\mu \right) $ to be the set difference

\begin{align*}  Y\left( \lambda \right) \setminus Y\left( \mu \right) &  =\left\{  \left( i,j\right) \  \mid \  i\in \left[ N\right] \text{ and }j\in \left[ \lambda _{i}\right] \setminus \left[ \mu _{i}\right] \right\}  \\ &  =\left\{  \left( i,j\right) \  \mid \  i\in \left[ N\right] \text{ and }j\in \mathbb {Z}\text{ and }\mu _{i}<j\leq \lambda _{i}\right\}  . \end{align*}

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.stemb-involution
Stembridge’s involution

\leanhelper  For a semistandard tableau $T$ that is not $\nu $-Yamanouchi, define $T^* = \operatorname {stemb}_\nu (T)$ as follows: 

\begin{enumerate} \item Let $j$ be the \emph{largest} violator column (where $\nu + \operatorname {cont}(\operatorname {col}_{\geq j} T)$ is not a partition). 

\item Let $k$ be the \emph{smallest} misstep index of $\nu + \operatorname {cont}(\operatorname {col}_{\geq j} T)$. 

\item Apply the prefix-restricted BK involution: $T^* = \beta _k^{<j}(T)$. 

\end{enumerate}

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.stemb-violator-misstep
Violator columns and misstep indices

\leanhelper  Let $T$ be a semistandard tableau and $\nu $ an $N$-tuple. A positive integer $j$ is a \emph{violator column} if $\nu + \operatorname {cont}(\operatorname {col}_{\geq j} T)$ is not an $N$-partition. An index $k$ is a \emph{misstep} for an $N$-tuple $\alpha $ if $k + 1 < N$ and $\alpha _k < \alpha _{k+1}$ (i.e., the partition condition fails at~ $k$).

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.yamanouchi
def.sf.yamanouchi

Let $\lambda ,\mu ,\nu $ be three $N$-partitions. A semistandard tableau $T$ of shape $\lambda /\mu $ is said to be $\nu $-\emph{Yamanouchi} (this is an adjective) if for each positive integer $j$, the $N$-tuple $\nu +\operatorname *{cont}\left( \operatorname {col}_{\geq j}T\right) \in \mathbb {N}^{N}$ is an $N$-partition (i.e., weakly decreasing).

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
  "verdict": "drift",
  "justification": "The target quantifies over all three partitions, `\u2200 ... (lam mu nu : Fin N \u2192 \u2115), IsNPartition lam \u2192 IsNPartition mu \u2192 IsNPartition nu \u2192 ...`, as does the blueprint. However, the informal definition stipulates: \u201cIf we don\u2019t have \u03bc \u2286 \u03bb, then we agree that there are no Young tableaux of shape \u03bb/\u03bc.\u201d The project dependency `AlgebraicCombinatorics.Tableau` instead has body `fun ... lam mu => { c // c \u2208 skewYoungDiagram lam mu } \u2192 Fin N`, with no condition `\u03bc \u2286 \u03bb`. Thus even when containment fails, it treats the cells satisfying `mu c.1 < c.2 \u2227 c.2 \u2264 lam c.1` as a shape and can have tableaux (in particular, an empty domain has a tableau whenever `Fin N` is inhabited). Consequently `skewSchurPoly` and the RHS sum over formal tableaux not admitted by the blueprint convention. The Yamanouchi and semistandard predicates themselves otherwise match the stated indexing condition. To make the declaration faithful, the difference should be fixed in the shape/tableau dependencies\u2014make `Tableau lam mu` empty when `\u03bc \u2288 \u03bb`, and have `skewSchurPoly` and the Yamanouchi tableau type use that convention\u2014or state the conclusion by cases with zero sums when containment fails. Merely adding a `\u03bc \u2286 \u03bb` binder to the target would add a hypothesis absent from the blueprint and would itself be a restriction."
}