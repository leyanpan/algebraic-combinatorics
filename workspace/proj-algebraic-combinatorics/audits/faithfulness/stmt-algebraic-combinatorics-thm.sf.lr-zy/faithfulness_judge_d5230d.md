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


## INFORMAL STATEMENT
Zelevinsky’s generalized Littlewood–Richardson rule, in Yamanouchi form

Let $\lambda ,\mu ,\nu $ be three $N$-partitions. Then,

\begin{equation}  s_{\nu }\cdot s_{\lambda /\mu }=\sum _{\substack {T\text{ is a }\nu \text{-Yamanouchi}\\ \text{semistandard tableau}\\ \text{of shape }\lambda /\mu }}s_{\nu +\operatorname *{cont}T}. \end{equation}

## INFORMAL DEPENDENCY stmt-algebraic-combinatorics-lem.cring.reg.cancel
lem.cring.reg.cancel

Let $L$ be a commutative ring. Let $a,u,v\in L$ be such that $a$ is regular. Assume that $au=av$. Then, $u=v$.

## INFORMAL DEPENDENCY stmt-algebraic-combinatorics-lem.sf.arho-reg
lem.sf.arho-reg

The element $a_{\rho }$ of the polynomial ring $\mathcal{P}$ is regular.

## INFORMAL DEPENDENCY stmt-algebraic-combinatorics-lem.sf.schur-alternant
Schur–alternant relation

\leanhelper  Let $\lambda $ be an $N$-partition. Then, 

\[  a_{\lambda + \rho } = a_{\rho } \cdot s_{\lambda }.  \]

 (This is Theorem~ \ref{thm.sf.schur-symm}~ \textbf{(b)}.)

## INFORMAL DEPENDENCY stmt-algebraic-combinatorics-lem.sf.stemb-lem
Stembridge’s Lemma

Let $\lambda ,\mu ,\nu $ be three $N$-partitions. Then,

\[  a_{\nu +\rho }\cdot s_{\lambda /\mu }=\sum _{\substack {T\text{ is a }\nu \text{-Yamanouchi}\\ \text{semistandard tableau}\\ \text{of shape }\lambda /\mu }}a_{\nu +\operatorname *{cont}T+\rho }.  \]

## VERDICT
{
  "verdict": "drift",
  "justification": "The tableau indexing and summands are faithful: the formal `\u2211 T` ranges over the inferred subtype `{ T // IsYamanouchi nu T }`; `IsYamanouchi` includes `IsSemistandard T`, while `Tableau lam mu` fixes shape `lam/mu`, and the summand is exactly `schurPoly (nu + contentTableau \u2191T)`. However, the elaborated target adds the mathematically substantive binder `[IsDomain R]` and asserts the identity only for coefficient rings that are domains: `\u2200 {R} [CommRing R] ... [IsDomain R]`. The informal statement has no domain hypothesis, and its cited cancellation route only requires a regular element in a commutative ring (`lem.cring.reg.cancel` together with `a_\u03c1` regular), not that the whole coefficient ring be a domain. Thus the Lean statement implies the ordinary rule in its permitted domain setting, but the informal statement does not imply the claimed family over every arbitrary domain `R`; conversely, as a generic-ring formalization it is unnecessarily restricted. The drift enters at the target binder `[IsDomain R]`. Removing that binder and proving the equality under `[CommRing R]` would match the generic polynomial definitions and the source\u2019s stated assumptions."
}