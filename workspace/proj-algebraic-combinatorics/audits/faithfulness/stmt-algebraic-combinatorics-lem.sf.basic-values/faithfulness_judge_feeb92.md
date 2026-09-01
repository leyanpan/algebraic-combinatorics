## TARGET AlgebraicCombinatorics.SymmetricPolynomials.e_zero (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] {N : ℕ}, AlgebraicCombinatorics.SymmetricPolynomials.e 0 = 1

Docstring: e_0 = 1 (Example exa.sf.ehp.1 (e)).
Label: exa.sf.ehp.1 

## TARGET AlgebraicCombinatorics.SymmetricPolynomials.p_zero (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] {N : ℕ}, AlgebraicCombinatorics.SymmetricPolynomials.p 0 = ↑(Fintype.card (Fin N))

Docstring: p_0 = N (number of variables).
Note: The source defines p_0 = 1, but Mathlib defines p_0 = N.
Label: exa.sf.ehp.1 

## TARGET AlgebraicCombinatorics.SymmetricPolynomials.e_one (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] {N : ℕ}, AlgebraicCombinatorics.SymmetricPolynomials.e 1 = ∑ i, MvPolynomial.X i

Docstring: e_1 = ∑ x_i (Example exa.sf.ehp.1 (d)).
Label: exa.sf.ehp.1 

## TARGET AlgebraicCombinatorics.SymmetricPolynomials.h_one (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] {N : ℕ} [inst_1 : DecidableEq (Fin N)],
  AlgebraicCombinatorics.SymmetricPolynomials.h 1 = ∑ i, MvPolynomial.X i

Docstring: h_1 = ∑ x_i (Example exa.sf.ehp.1 (d)).
Label: exa.sf.ehp.1 

## TARGET AlgebraicCombinatorics.SymmetricPolynomials.p_one (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] {N : ℕ}, AlgebraicCombinatorics.SymmetricPolynomials.p 1 = ∑ i, MvPolynomial.X i

Docstring: p_1 = ∑ x_i (Example exa.sf.ehp.1 (d)).
Label: exa.sf.ehp.1 

## TARGET AlgebraicCombinatorics.SymmetricPolynomials.h_zero (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] {N : ℕ} [inst_1 : DecidableEq (Fin N)],
  AlgebraicCombinatorics.SymmetricPolynomials.h 0 = 1

Docstring: h_0 = 1 (Example exa.sf.ehp.1 (e)).
Label: exa.sf.ehp.1 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SymmetricPolynomials.P (def)
(K : Type u_2) → [CommRing K] → ℕ → Type u_2

Body:
fun K [CommRing K] N => MvPolynomial (Fin N) K

Docstring: The polynomial ring in N variables over K.
This corresponds to 𝒫 in the source (Definition def.sf.PS (a)).
Label: def.sf.PS 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SymmetricPolynomials.e (def)
{K : Type u_1} → [inst : CommRing K] → {N : ℕ} → ℕ → AlgebraicCombinatorics.SymmetricPolynomials.P K N

Body:
fun {K} [CommRing K] {N} n => MvPolynomial.esymm (Fin N) K n

Docstring: The n-th elementary symmetric polynomial.
Label: def.sf.ehp 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SymmetricPolynomials.P_isCommRing' (def)
{K : Type u_1} → [inst : CommRing K] → {N : ℕ} → CommRing (AlgebraicCombinatorics.SymmetricPolynomials.P K N)

Body:
fun {K} [CommRing K] {N} => inferInstance

Docstring: The polynomial ring P K N is a commutative K-algebra.
Label: def.sf.PS 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SymmetricPolynomials.p (def)
{K : Type u_1} → [inst : CommRing K] → {N : ℕ} → ℕ → AlgebraicCombinatorics.SymmetricPolynomials.P K N

Body:
fun {K} [CommRing K] {N} n => MvPolynomial.psum (Fin N) K n

Docstring: The n-th power sum symmetric polynomial.
Label: def.sf.ehp 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SymmetricPolynomials.h (def)
{K : Type u_1} →
  [inst : CommRing K] → {N : ℕ} → [DecidableEq (Fin N)] → ℕ → AlgebraicCombinatorics.SymmetricPolynomials.P K N

Body:
fun {K} [CommRing K] {N} [DecidableEq (Fin N)] n => MvPolynomial.hsymm (Fin N) K n

Docstring: The n-th complete homogeneous symmetric polynomial.
Label: def.sf.ehp 

## BASE-LIBRARY REF CommRing
Type u → Type u

Docstring: A commutative ring is a ring with commutative multiplication. 

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

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

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


## BASE-LIBRARY REF AddMonoidWithOne.toNatCast
{R : Type u_2} → [self : AddMonoidWithOne R] → NatCast R

## BASE-LIBRARY REF Fintype.card
(α : Type u_4) → [Fintype α] → ℕ

Docstring: `card α` is the number of elements in `α`, defined when `α` is a fintype. 

## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


## BASE-LIBRARY REF Fin.fintype
(n : ℕ) → Fintype (Fin n)

## BASE-LIBRARY REF Finset.sum
{ι : Type u_1} → {M : Type u_3} → [AddCommMonoid M] → Finset ι → (ι → M) → M

Docstring: `∑ x ∈ s, f x` is the sum of `f x` as `x` ranges over the elements
of the finite set `s`.

When the index type is a `Fintype`, the notation `∑ x, f x`, is a shorthand for
`∑ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF MvPolynomial
Type u_1 → (R : Type u_2) → [CommSemiring R] → Type (max u_2 u_1)

Docstring: Multivariate polynomial, where `σ` is the index set of the variables and
`R` is the coefficient ring 

## BASE-LIBRARY REF CommRing.toCommSemiring
{α : Type u} → [s : CommRing α] → CommSemiring α

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

## BASE-LIBRARY REF Finset.univ
{α : Type u_1} → [Fintype α] → Finset α

Docstring: `univ` is the universal finite set of type `Finset α` implied from
the assumption `Fintype α`. 

## BASE-LIBRARY REF MvPolynomial.X
{R : Type u} → {σ : Type u_1} → [inst : CommSemiring R] → σ → MvPolynomial σ R

Docstring: `X n` is the degree `1` monomial $X_n$. 

## BASE-LIBRARY REF DecidableEq
Sort u → Sort (max 1 u)

Docstring: Propositional equality is `Decidable` for all elements of a type.

In other words, an instance of `DecidableEq α` is a means of deciding the proposition `a = b` is
for all `a b : α`.


## BASE-LIBRARY REF MvPolynomial.esymm
(σ : Type u_5) → (R : Type u_6) → [inst : CommSemiring R] → [Fintype σ] → ℕ → MvPolynomial σ R

Docstring: The `n`th elementary symmetric `MvPolynomial σ R`.
It is the sum over all the degree n squarefree monomials in `MvPolynomial σ R`. 

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

## BASE-LIBRARY REF MvPolynomial.psum
(σ : Type u_5) → (R : Type u_6) → [inst : CommSemiring R] → [Fintype σ] → ℕ → MvPolynomial σ R

Docstring: The degree-`n` power sum symmetric `MvPolynomial σ R`.
It is the sum over all the `n`-th powers of the variables. 

## BASE-LIBRARY REF MvPolynomial.hsymm
(σ : Type u_5) → (R : Type u_6) → [inst : CommSemiring R] → [Fintype σ] → [DecidableEq σ] → ℕ → MvPolynomial σ R

Docstring: The `n`th complete homogeneous symmetric `MvPolynomial σ R`.
It is the sum over all the degree n monomials in `MvPolynomial σ R`. 

## INFORMAL STATEMENT
lem.sf.basic-values

\leanhelper  We have the following basic values: 

\begin{itemize} \item $e_0 = h_0 = 1$; 

\item $e_1 = h_1 = p_1 = \sum _{i=1}^N x_i$; 

\item $p_0 = N$ (the number of variables; note this differs from the textbook convention $p_0 = 1$). 

\end{itemize}

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.ehp
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
  "justification": "The five identities involving `e 0`, `h 0`, `e 1`, `h 1`, and `p 1` match the corresponding blueprint clauses. The `DecidableEq (Fin N)` binders on the `h` declarations are computational encoding required by `MvPolynomial.hsymm`, not a substantive restriction. However, `p_zero` drifts through the dependency `AlgebraicCombinatorics.SymmetricPolynomials.p`: its body is `MvPolynomial.psum (Fin N) K n`, so at zero it is the sum of one over all variables and the target states `p 0 = \u2191(Fintype.card (Fin N))`. In contrast, the informal definition fixes `p_n` by the case `1, if n = 0`, even though the informal lemma then asserts `$p_0 = N$`. After expanding that definition, the blueprint assertion is `1 = N`, whereas the formal assertion using the altered `p` definition is effectively `N = N`; thus the formal theorem does not imply the blueprint statement under its supplied definition. To make the package faithful, either the informal definition must be revised so that `p_0 := N` (consistent with the lemma\u2019s explicit convention), or the project definition `p` must use the supplied piecewise convention with `p 0 = 1`, in which case the target would have to state the resulting proposition `1 = \u2191N` rather than obtaining it tautologically from `MvPolynomial.psum`."
}