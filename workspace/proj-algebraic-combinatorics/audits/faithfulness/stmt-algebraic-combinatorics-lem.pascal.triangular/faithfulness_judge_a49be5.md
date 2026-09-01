## TARGET AlgebraicCombinatorics.CauchyBinet.pascalUpperTriangular_diag (theorem) — ELABORATED SIGNATURE
∀ (n : ℕ) (i : Fin n), AlgebraicCombinatorics.CauchyBinet.pascalUpperTriangular n i i = 1

Docstring: The upper triangular factor U has all diagonal entries equal to 1. 

## TARGET AlgebraicCombinatorics.CauchyBinet.pascalLowerTriangular_diag (theorem) — ELABORATED SIGNATURE
∀ (n : ℕ) (i : Fin n), AlgebraicCombinatorics.CauchyBinet.pascalLowerTriangular n i i = 1

Docstring: The lower triangular factor L has all diagonal entries equal to 1. 

## TARGET AlgebraicCombinatorics.CauchyBinet.pascalUpperTriangular_is_upper (theorem) — ELABORATED SIGNATURE
∀ (n : ℕ) (k j : Fin n), k > j → AlgebraicCombinatorics.CauchyBinet.pascalUpperTriangular n k j = 0

Docstring: The upper triangular factor U is indeed upper triangular. 

## TARGET AlgebraicCombinatorics.CauchyBinet.pascalLowerTriangular_is_lower (theorem) — ELABORATED SIGNATURE
∀ (n : ℕ) (i k : Fin n), i < k → AlgebraicCombinatorics.CauchyBinet.pascalLowerTriangular n i k = 0

Docstring: The lower triangular factor L is indeed lower triangular. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.CauchyBinet.pascalUpperTriangular (def)
(n : ℕ) → Matrix (Fin n) (Fin n) ℕ

Body:
fun n k j => (↑j).choose ↑k

Docstring: The upper triangular factor U in the LU decomposition of the Pascal matrix.
U_{k,j} = C(j, k) 

## PROJECT DEPENDENCY AlgebraicCombinatorics.CauchyBinet.pascalLowerTriangular (def)
(n : ℕ) → Matrix (Fin n) (Fin n) ℕ

Body:
fun n i k => (↑i).choose ↑k

Docstring: The lower triangular factor L in the LU decomposition of the Pascal matrix.
L_{i,k} = C(i, k) 

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

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

## BASE-LIBRARY REF GT.gt
{α : Type u} → [LT α] → α → α → Prop

Docstring: `a > b` is an abbreviation for `b < a`. 

Conventions for notations in identifiers:

 * The recommended spelling of `>` in identifiers is `gt`.

## BASE-LIBRARY REF instLTFin
{n : ℕ} → LT (Fin n)

## BASE-LIBRARY REF LT.lt
{α : Type u} → [self : LT α] → α → α → Prop

Docstring: The less-than relation: `x < y` 

Conventions for notations in identifiers:

 * The recommended spelling of `<` in identifiers is `lt`.

## BASE-LIBRARY REF Matrix
Type u → Type u' → Type v → Type (max u u' v)

Docstring: `Matrix m n R` is the type of matrices with entries in `R`, whose rows are indexed by `m`
and whose columns are indexed by `n`. 

## BASE-LIBRARY REF Nat.choose
ℕ → ℕ → ℕ

Docstring: `choose n k` is the number of `k`-element subsets in an `n`-element set. Also known as binomial
coefficients. For the fact that this is the number of `k`-element-subsets of an `n`-element
set, see `Finset.card_powersetCard`. 

## BASE-LIBRARY REF Fin.val
{n : ℕ} → Fin n → ℕ

Docstring: The number that is strictly less than `n`.

`Fin.val` is a coercion, so any `Fin n` can be used in a position where a `Nat` is expected.


## INFORMAL STATEMENT
Triangularity and unit diagonal

\leanhelper  $L$ is lower triangular ($L_{i,k} = 0$ for $i < k$) with $L_{i,i} = 1$. $U$ is upper triangular ($U_{k,j} = 0$ for $k > j$) with $U_{k,k} = 1$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.binom.binom
def.binom.binom

For any numbers $n$ and $k$, we set

\begin{equation}  \binom {n}{k}=\begin{cases}  \frac{n\left( n-1\right) \left( n-2\right) \cdots \left( n-k+1\right) }{k!}, &  \text{if }k\in \mathbb {N};\\ 0, &  \text{else.}\end{cases} \end{equation}

 Note that “numbers” is to be understood fairly liberally here. In particular, $n$ can be any integer, rational, real or complex number (or, more generally, any element in a $\mathbb {Q}$-algebra), whereas $k$ can be anything (although the only nonzero values of $\binom {n}{k}$ will be achieved for $k\in \mathbb {N}$, by the above definition).

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.pascal
Pascal matrix and its LU factors

\leanhelper  Define the $n\times n$ Pascal matrix, the lower triangular factor $L$, and the upper triangular factor $U$ by: 

\begin{align*}  A_{i,j} & = \binom {i+j}{i}, &  L_{i,k} & = \binom {i}{k}, &  U_{k,j} & = \binom {j}{k}, \end{align*}

 for $0\le i,j,k \le n-1$.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The four declarations exactly formalize the two triangularity and two unit-diagonal claims over the prescribed indices `Fin n` (that is, `0 \u2264 i,j,k \u2264 n-1`). The definitions give `pascalLowerTriangular n i k = (\u2191i).choose \u2191k`, matching `L_{i,k} = \\binom{i}{k}`, and `pascalUpperTriangular n k j = (\u2191j).choose \u2191k`, matching `U_{k,j} = \\binom{j}{k}`. The signatures assert respectively `i < k \u2192 L_{i,k} = 0`, `L_{i,i} = 1`, `k > j \u2192 U_{k,j} = 0`, and `U_{i,i} = 1`, exactly matching the informal statement. There are no added hypotheses or narrowed index ranges."
}