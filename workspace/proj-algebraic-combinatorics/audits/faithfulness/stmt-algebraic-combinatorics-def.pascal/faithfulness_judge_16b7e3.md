## TARGET AlgebraicCombinatorics.CauchyBinet.pascalMatrix (def) — ELABORATED SIGNATURE
(n : ℕ) → Matrix (Fin n) (Fin n) ℕ

Body:
fun n i j => (↑i + ↑j).choose ↑i

Docstring: The Pascal matrix with entries C(i+j, i).
(Proposition prop.det.pascal-LU)

Note: We use 0-indexing, so entry (i,j) is C(i+j, i). 

## TARGET AlgebraicCombinatorics.CauchyBinet.pascalLowerTriangular (def) — ELABORATED SIGNATURE
(n : ℕ) → Matrix (Fin n) (Fin n) ℕ

Body:
fun n i k => (↑i).choose ↑k

Docstring: The lower triangular factor L in the LU decomposition of the Pascal matrix.
L_{i,k} = C(i, k) 

## TARGET AlgebraicCombinatorics.CauchyBinet.pascalUpperTriangular (def) — ELABORATED SIGNATURE
(n : ℕ) → Matrix (Fin n) (Fin n) ℕ

Body:
fun n k j => (↑j).choose ↑k

Docstring: The upper triangular factor U in the LU decomposition of the Pascal matrix.
U_{k,j} = C(j, k) 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF Matrix
Type u → Type u' → Type v → Type (max u u' v)

Docstring: `Matrix m n R` is the type of matrices with entries in `R`, whose rows are indexed by `m`
and whose columns are indexed by `n`. 

## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


## BASE-LIBRARY REF Nat.choose
ℕ → ℕ → ℕ

Docstring: `choose n k` is the number of `k`-element subsets in an `n`-element set. Also known as binomial
coefficients. For the fact that this is the number of `k`-element-subsets of an `n`-element
set, see `Finset.card_powersetCard`. 

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


## INFORMAL STATEMENT
Pascal matrix and its LU factors

\leanhelper  Define the $n\times n$ Pascal matrix, the lower triangular factor $L$, and the upper triangular factor $U$ by: 

\begin{align*}  A_{i,j} & = \binom {i+j}{i}, &  L_{i,k} & = \binom {i}{k}, &  U_{k,j} & = \binom {j}{k}, \end{align*}

 for $0\le i,j,k \le n-1$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.binom.binom
def.binom.binom

For any numbers $n$ and $k$, we set

\begin{equation}  \binom {n}{k}=\begin{cases}  \frac{n\left( n-1\right) \left( n-2\right) \cdots \left( n-k+1\right) }{k!}, &  \text{if }k\in \mathbb {N};\\ 0, &  \text{else.}\end{cases} \end{equation}

 Note that “numbers” is to be understood fairly liberally here. In particular, $n$ can be any integer, rational, real or complex number (or, more generally, any element in a $\mathbb {Q}$-algebra), whereas $k$ can be anything (although the only nonzero values of $\binom {n}{k}$ will be achieved for $k\in \mathbb {N}$, by the above definition).

## VERDICT
{
  "verdict": "faithful",
  "justification": "The three bodies exactly implement the blueprint formulas with 0-based indices. `pascalMatrix` has binders `(n : \u2115)` and `i j : Fin n`, so `\u2191i, \u2191j` range over `0,\u2026,n-1`, and its body `(\u2191i + \u2191j).choose \u2191i` is `A_{i,j} = \\binom{i+j}{i}`. Likewise, `pascalLowerTriangular` uses `(\u2191i).choose \u2191k`, matching `L_{i,k} = \\binom{i}{k}`, and `pascalUpperTriangular` uses `(\u2191j).choose \u2191k`, matching `U_{k,j} = \\binom{j}{k}`. `Nat.choose` denotes the relevant binomial coefficient on these natural-number arguments, and the `Fin n` row and column types precisely encode the stated bounds `0 \u2264 i,j,k \u2264 n-1`."
}