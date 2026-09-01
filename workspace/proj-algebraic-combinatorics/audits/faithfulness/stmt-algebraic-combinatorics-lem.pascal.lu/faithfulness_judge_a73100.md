## TARGET AlgebraicCombinatorics.CauchyBinet.pascal_eq_LU (theorem) — ELABORATED SIGNATURE
∀ (n : ℕ),
  ((AlgebraicCombinatorics.CauchyBinet.pascalMatrix n).map fun x => ↑x) =
    ((AlgebraicCombinatorics.CauchyBinet.pascalLowerTriangular n).map fun x => ↑x) *
      (AlgebraicCombinatorics.CauchyBinet.pascalUpperTriangular n).map fun x => ↑x

Docstring: The Pascal matrix factors as L * U where L and U are lower and upper triangular.
This is the LU decomposition of the Pascal matrix.

The proof uses Vandermonde's identity: C(i+j, i) = ∑_k C(i,k) * C(j,k). 

## PROJECT DEPENDENCY AlgebraicCombinatorics.CauchyBinet.pascalMatrix (def)
(n : ℕ) → Matrix (Fin n) (Fin n) ℕ

Body:
fun n i j => (↑i + ↑j).choose ↑i

Docstring: The Pascal matrix with entries C(i+j, i).
(Proposition prop.det.pascal-LU)

Note: We use 0-indexing, so entry (i,j) is C(i+j, i). 

## PROJECT DEPENDENCY AlgebraicCombinatorics.CauchyBinet.pascalLowerTriangular (def)
(n : ℕ) → Matrix (Fin n) (Fin n) ℕ

Body:
fun n i k => (↑i).choose ↑k

Docstring: The lower triangular factor L in the LU decomposition of the Pascal matrix.
L_{i,k} = C(i, k) 

## PROJECT DEPENDENCY AlgebraicCombinatorics.CauchyBinet.pascalUpperTriangular (def)
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

## BASE-LIBRARY REF Matrix
Type u → Type u' → Type v → Type (max u u' v)

Docstring: `Matrix m n R` is the type of matrices with entries in `R`, whose rows are indexed by `m`
and whose columns are indexed by `n`. 

## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


## BASE-LIBRARY REF Int
Type

Docstring: The integers.

This type is special-cased by the compiler and overridden with an efficient implementation. The
runtime has a special representation for `Int` that stores “small” signed numbers directly, while
larger numbers use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)). A “small number” is an integer that can be encoded with one fewer bits
than the platform's pointer size (i.e. 63 bits on 64-bit architectures and 31 bits on 32-bit
architectures).


## BASE-LIBRARY REF Matrix.map
{m : Type u_2} → {n : Type u_3} → {α : Type v} → {β : Type w} → Matrix m n α → (α → β) → Matrix m n β

Docstring: `M.map f` is the matrix obtained by applying `f` to each entry of the matrix `M`.

This is available in bundled forms as:
* `AddMonoidHom.mapMatrix`
* `LinearMap.mapMatrix`
* `RingHom.mapMatrix`
* `AlgHom.mapMatrix`
* `Equiv.mapMatrix`
* `AddEquiv.mapMatrix`
* `LinearEquiv.mapMatrix`
* `RingEquiv.mapMatrix`
* `AlgEquiv.mapMatrix`


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

## BASE-LIBRARY REF HMul.hMul
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HMul α β γ] → α → β → γ

Docstring: `a * b` computes the product of `a` and `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `*` in identifiers is `mul`.

## BASE-LIBRARY REF Matrix.instHMulOfFintypeOfMulOfAddCommMonoid
{l : Type u_1} →
  {m : Type u_2} →
    {n : Type u_3} →
      {α : Type v} → [Fintype m] → [Mul α] → [AddCommMonoid α] → HMul (Matrix l m α) (Matrix m n α) (Matrix l n α)

Docstring: `M * N` is the usual product of matrices `M` and `N`, i.e. we have that
`(M * N) i k` is the dot product of the `i`-th row of `M` by the `k`-th column of `N`.
This is currently only defined when `m` is finite. 

## BASE-LIBRARY REF Fin.fintype
(n : ℕ) → Fintype (Fin n)

## BASE-LIBRARY REF Int.instMul
Mul ℤ

## BASE-LIBRARY REF Int.instAddCommMonoid
AddCommMonoid ℤ

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
lem.pascal.LU

\leanhelper  Then $A = L \cdot U$ (over $\mathbb {Z}$).

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
  "justification": "The target quantifies over every size, `\u2200 (n : \u2115)`, and states equality after mapping all three natural-valued matrices into `\u2124`: `((pascalMatrix n).map fun x => \u2191x) = ((pascalLowerTriangular n).map fun x => \u2191x) * ((pascalUpperTriangular n).map fun x => \u2191x)`. Thus it is exactly the informal claim \u201cThen A = L \u00b7 U (over \u2124).\u201d The dependency bodies agree with the informal definitions on `Fin n` indices: `A_{i,j} = (\u2191i + \u2191j).choose \u2191i`, `L_{i,k} = (\u2191i).choose \u2191k`, and `U_{k,j} = (\u2191j).choose \u2191k`, matching `A_{i,j}=binom{i+j}{i}`, `L_{i,k}=binom{i}{k}`, and `U_{k,j}=binom{j}{k}` for `0 \u2264 i,j,k \u2264 n\u22121`. Matrix multiplication is the usual finite dot-product multiplication over the integers, and there are no added hypotheses or narrowed index ranges."
}