## TARGET AlgebraicCombinatorics.schurPoly_eq_alternant_div (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_1} [inst : CommRing R] {N : ℕ} (lam : Fin N → ℕ),
  AlgebraicCombinatorics.IsNPartition lam →
    AlgebraicCombinatorics.alternant (lam + AlgebraicCombinatorics.rho N) =
      AlgebraicCombinatorics.alternant (AlgebraicCombinatorics.rho N) * AlgebraicCombinatorics.schurPoly lam

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

## PROJECT DEPENDENCY AlgebraicCombinatorics.SymmetricFunctions.monomialExp (def)
{R : Type u_1} → [inst : CommSemiring R] → {N : ℕ} → (Fin N → ℕ) → MvPolynomial (Fin N) R

Body:
fun {R} [CommSemiring R] {N} a => ∏ i, MvPolynomial.X i ^ a i

Docstring: The monomial x^a = x₁^{a₁} x₂^{a₂} ⋯ x_N^{a_N} for a tuple a ∈ ℕ^N.
(Definition def.sf.sort (a)) 

## PROJECT DEPENDENCY AlgebraicCombinatorics.Tableau (def)
{N : ℕ} → (Fin N → ℕ) → (Fin N → ℕ) → Type

Body:
fun {N} lam mu => { c // c ∈ AlgebraicCombinatorics.skewYoungDiagram lam mu } → Fin N

Docstring: A tableau of shape lam/mu is a function from cells to [N]. 

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

## INFORMAL STATEMENT
Schur–alternant relation

\leanhelper  Let $\lambda $ be an $N$-partition. Then, 

\[  a_{\lambda + \rho } = a_{\rho } \cdot s_{\lambda }.  \]

 (This is Theorem~ \ref{thm.sf.schur-symm}~ \textbf{(b)}.)

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.alternants
def.sf.alternants

\textbf{(a)} We let $\rho $ be the $N$-tuple $\left( N-1,N-2,\ldots ,N-N\right) \in \mathbb {N}^{N}$. \medskip 

\textbf{(b)} For any $N$-tuple $\alpha =\left( \alpha _{1},\alpha _{2},\ldots ,\alpha _{N}\right) \in \mathbb {N}^{N}$, we define

\[  a_{\alpha }:=\det \left( \underbrace{\left( x_{i}^{\alpha _{j}}\right) _{1\leq i\leq N,\  1\leq j\leq N}}_{\in \mathcal{P}^{N\times N}}\right) \in \mathcal{P}.  \]

 This is called the $\alpha $\emph{-alternant} (of $x_{1},x_{2},\ldots ,x_{N}$).

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.npar
def.sf.Npar

An $N$\emph{-partition} will mean a weakly decreasing $N$-tuple of nonnegative integers. In other words, an $N$-partition means an $N$-tuple $\left( \lambda _{1},\lambda _{2},\ldots ,\lambda _{N}\right) \in \mathbb {N}^{N}$ with $\lambda _{1}\geq \lambda _{2}\geq \cdots \geq \lambda _{N}$. 

The \emph{size} (or weight) of an $N$-partition $\lambda = (\lambda _1, \lambda _2, \ldots , \lambda _N)$ is defined to be $|\lambda | := \lambda _1 + \lambda _2 + \cdots + \lambda _N$.

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.rhopartition
def.sf.rhoPartition

\leanhelper  The $\rho $ vector $(N{-}1, N{-}2, \ldots , 0)$ is itself an $N$-partition (since it is strictly decreasing, hence weakly decreasing).

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.schur
def.sf.schur

Let $\lambda $ be an $N$-partition. We define the \emph{Schur polynomial} $s_{\lambda }\in \mathcal{P}$ by

\[  s_{\lambda }:=\sum _{T\in \operatorname *{SSYT}\left( \lambda \right) }x_{T}.  \]

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.tuple-addition
def.sf.tuple-addition

\textbf{(a)} We let $\mathbf{0}$ denote the $N$-tuple $\left( 0,0,\ldots ,0\right) \in \mathbb {N}^{N}$. 

\medskip 

\textbf{(b)} Let $\alpha =\left( \alpha _{1},\alpha _{2},\ldots ,\alpha _{N}\right) $ and $\beta =\left( \beta _{1},\beta _{2},\ldots ,\beta _{N}\right) $ be two $N$-tuples in $\mathbb {N}^{N}$. Then, we set

\begin{align*}  \alpha +\beta &  :=\left( \alpha _{1}+\beta _{1},\alpha _{2}+\beta _{2},\ldots ,\alpha _{N}+\beta _{N}\right) \  \  \  \  \  \  \  \  \  \  \text{and}\\ \alpha -\beta &  :=\left( \alpha _{1}-\beta _{1},\alpha _{2}-\beta _{2},\ldots ,\alpha _{N}-\beta _{N}\right) . \end{align*}

 Note that $\alpha +\beta \in \mathbb {N}^{N}$, whereas $\alpha -\beta \in \mathbb {Z}^{N}$.

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
  "justification": "The formal binder `\u2200 {R : Type u_1} [inst : CommRing R] {N : \u2115} (lam : Fin N \u2192 \u2115), AlgebraicCombinatorics.IsNPartition lam \u2192 ...` matches \u201cLet \u03bb be an N-partition,\u201d since `IsNPartition lam` unfolds to `\u2200 i j, i \u2264 j \u2192 lam j \u2264 lam i`, exactly a weakly decreasing N-tuple of naturals. The conclusion is precisely `alternant (lam + rho N) = alternant (rho N) * schurPoly lam`, matching `a_{\u03bb+\u03c1} = a_\u03c1 \u00b7 s_\u03bb`; function addition is componentwise, and `rho N i = N - 1 - i` represents `(N-1,\u2026,0)`. The formal alternant\u2019s signed permutation sum is the determinant alternant from the informal definition, while `schurPoly lam = skewSchurPoly lam 0` expands to the sum of tableau-content monomials for ordinary shape \u03bb, matching the informal tableau definition of `s_\u03bb`. Quantification over every commutative coefficient ring `R` is consistent with, and at least as general as, the blueprint\u2019s arbitrary commutative ring `K`; no additional mathematically restrictive hypothesis is introduced."
}