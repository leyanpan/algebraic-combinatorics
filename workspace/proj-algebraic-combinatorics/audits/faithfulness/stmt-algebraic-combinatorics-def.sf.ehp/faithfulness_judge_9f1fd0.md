## TARGET AlgebraicCombinatorics.SymmetricPolynomials.p (def) — ELABORATED SIGNATURE
{K : Type u_1} → [inst : CommRing K] → {N : ℕ} → ℕ → AlgebraicCombinatorics.SymmetricPolynomials.P K N

Body:
fun {K} [CommRing K] {N} n => MvPolynomial.psum (Fin N) K n

Docstring: The n-th power sum symmetric polynomial.
Label: def.sf.ehp 

## TARGET AlgebraicCombinatorics.SymmetricPolynomials.e (def) — ELABORATED SIGNATURE
{K : Type u_1} → [inst : CommRing K] → {N : ℕ} → ℕ → AlgebraicCombinatorics.SymmetricPolynomials.P K N

Body:
fun {K} [CommRing K] {N} n => MvPolynomial.esymm (Fin N) K n

Docstring: The n-th elementary symmetric polynomial.
Label: def.sf.ehp 

## TARGET AlgebraicCombinatorics.SymmetricPolynomials.h (def) — ELABORATED SIGNATURE
{K : Type u_1} →
  [inst : CommRing K] → {N : ℕ} → [DecidableEq (Fin N)] → ℕ → AlgebraicCombinatorics.SymmetricPolynomials.P K N

Body:
fun {K} [CommRing K] {N} [DecidableEq (Fin N)] n => MvPolynomial.hsymm (Fin N) K n

Docstring: The n-th complete homogeneous symmetric polynomial.
Label: def.sf.ehp 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SymmetricPolynomials.P (def)
(K : Type u_2) → [CommRing K] → ℕ → Type u_2

Body:
fun K [CommRing K] N => MvPolynomial (Fin N) K

Docstring: The polynomial ring in N variables over K.
This corresponds to 𝒫 in the source (Definition def.sf.PS (a)).
Label: def.sf.PS 

## BASE-LIBRARY REF CommRing
Type u → Type u

Docstring: A commutative ring is a ring with commutative multiplication. 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF MvPolynomial.psum
(σ : Type u_5) → (R : Type u_6) → [inst : CommSemiring R] → [Fintype σ] → ℕ → MvPolynomial σ R

Docstring: The degree-`n` power sum symmetric `MvPolynomial σ R`.
It is the sum over all the `n`-th powers of the variables. 

## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


## BASE-LIBRARY REF CommRing.toCommSemiring
{α : Type u} → [s : CommRing α] → CommSemiring α

## BASE-LIBRARY REF Fin.fintype
(n : ℕ) → Fintype (Fin n)

## BASE-LIBRARY REF MvPolynomial.esymm
(σ : Type u_5) → (R : Type u_6) → [inst : CommSemiring R] → [Fintype σ] → ℕ → MvPolynomial σ R

Docstring: The `n`th elementary symmetric `MvPolynomial σ R`.
It is the sum over all the degree n squarefree monomials in `MvPolynomial σ R`. 

## BASE-LIBRARY REF DecidableEq
Sort u → Sort (max 1 u)

Docstring: Propositional equality is `Decidable` for all elements of a type.

In other words, an instance of `DecidableEq α` is a means of deciding the proposition `a = b` is
for all `a b : α`.


## BASE-LIBRARY REF MvPolynomial.hsymm
(σ : Type u_5) → (R : Type u_6) → [inst : CommSemiring R] → [Fintype σ] → [DecidableEq σ] → ℕ → MvPolynomial σ R

Docstring: The `n`th complete homogeneous symmetric `MvPolynomial σ R`.
It is the sum over all the degree n monomials in `MvPolynomial σ R`. 

## BASE-LIBRARY REF MvPolynomial
Type u_1 → (R : Type u_2) → [CommSemiring R] → Type (max u_2 u_1)

Docstring: Multivariate polynomial, where `σ` is the index set of the variables and
`R` is the coefficient ring 

## INFORMAL STATEMENT
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

## VERDICT
{
  "verdict": "drift",
  "justification": "All three formal definitions narrow the blueprint\u2019s quantifier. The informal statement says \u201cFor each $n \\in \\mathbb Z$\u201d for $e_n$, $h_n$, and $p_n$, whereas the elaborated signatures end in `\u2115 \u2192 ...`. Thus negative indices are omitted; this restriction enters through the final `\u2115` binder of each target declaration. The definitions should instead take an integer index and define the negative-index cases consistently with the displayed formulas (in particular, as zero where there are no monomials of negative degree).\n\nThere is also a separate mismatch in `p` at zero. The blueprint explicitly requires `p_n = 1, if n = 0`, while the body is `MvPolynomial.psum (Fin N) K n`. The base-library documentation says `psum` \u201cis the sum over all the `n`-th powers of the variables,\u201d so at `n = 0` this sums one copy of `1` for every variable, rather than uniformly giving `1` (e.g. it gives the scalar corresponding to `N`). To be faithful, `p` must special-case `n = 0` as `1`, positive indices as `MvPolynomial.psum ...`, and negative indices as `0`. The `DecidableEq (Fin N)` binder on `h` is only computational encoding needed by `MvPolynomial.hsymm`, not mathematical drift."
}