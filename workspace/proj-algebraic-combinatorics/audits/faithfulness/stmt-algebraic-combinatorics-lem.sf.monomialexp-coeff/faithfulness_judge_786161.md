## TARGET AlgebraicCombinatorics.SymmetricFunctions.monomialExp_coeff_ne (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_1} [inst : CommSemiring R] {N : ℕ} (a b : Fin N → ℕ),
  a ≠ b →
    MvPolynomial.coeff (Finsupp.equivFunOnFinite.symm b) (AlgebraicCombinatorics.SymmetricFunctions.monomialExp a) = 0

Docstring: Coefficient of a different monomial in monomialExp a is 0. 

## TARGET AlgebraicCombinatorics.SymmetricFunctions.monomialExp_coeff_self (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_1} [inst : CommSemiring R] {N : ℕ} (a : Fin N → ℕ),
  MvPolynomial.coeff (Finsupp.equivFunOnFinite.symm a) (AlgebraicCombinatorics.SymmetricFunctions.monomialExp a) = 1

Docstring: Coefficient of the monomial x^a in monomialExp a is 1. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SymmetricFunctions.monomialExp (def)
{R : Type u_1} → [inst : CommSemiring R] → {N : ℕ} → (Fin N → ℕ) → MvPolynomial (Fin N) R

Body:
fun {R} [CommSemiring R] {N} a => ∏ i, MvPolynomial.X i ^ a i

Docstring: The monomial x^a = x₁^{a₁} x₂^{a₂} ⋯ x_N^{a_N} for a tuple a ∈ ℕ^N.
(Definition def.sf.sort (a)) 

## BASE-LIBRARY REF CommSemiring
Type u → Type u

Docstring: A commutative semiring is a semiring with commutative multiplication. 

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


## BASE-LIBRARY REF Ne
{α : Sort u} → α → α → Prop

Docstring: `a ≠ b`, or `Ne a b` is defined as `¬ (a = b)` or `a = b → False`,
and asserts that `a` and `b` are not equal.


Conventions for notations in identifiers:

 * The recommended spelling of `≠` in identifiers is `ne`.

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

## BASE-LIBRARY REF MvPolynomial.coeff
{R : Type u} → {σ : Type u_1} → [inst : CommSemiring R] → (σ →₀ ℕ) → MvPolynomial σ R → R

Docstring: The coefficient of the monomial `m` in the multi-variable polynomial `p`. 

## BASE-LIBRARY REF DFunLike.coe
{F : Sort u_1} → {α : outParam (Sort u_2)} → {β : outParam (α → Sort u_3)} → [self : DFunLike F α β] → F → (a : α) → β a

Docstring: The coercion from `F` to a function. 

## BASE-LIBRARY REF Equiv
Sort u_1 → Sort u_2 → Sort (max (max 1 u_1) u_2)

Docstring: `α ≃ β` is the type of functions from `α → β` with a two-sided inverse. 

## BASE-LIBRARY REF Finsupp
Type u_9 → (M : Type u_10) → [Zero M] → Type (max u_10 u_9)

Docstring: `Finsupp α M`, denoted `α →₀ M`, is the type of functions `f : α → M` such that
`f x = 0` for all but finitely many `x`. 

## BASE-LIBRARY REF MulZeroClass.toZero
{M₀ : Type u} → [self : MulZeroClass M₀] → Zero M₀

## BASE-LIBRARY REF Nat.instMulZeroClass
MulZeroClass ℕ

## BASE-LIBRARY REF EquivLike.toFunLike
{E : Sort u_1} → {α : Sort u_3} → {β : Sort u_4} → [EquivLike E α β] → FunLike E α β

## BASE-LIBRARY REF Equiv.instEquivLike
{α : Sort u} → {β : Sort v} → EquivLike (α ≃ β) α β

## BASE-LIBRARY REF Equiv.symm
{α : Sort u} → {β : Sort v} → α ≃ β → β ≃ α

Docstring: Inverse of an equivalence `e : α ≃ β`. 

## BASE-LIBRARY REF Finsupp.equivFunOnFinite
{α : Type u_1} → {M : Type u_4} → [inst : Zero M] → [Finite α] → (α →₀ M) ≃ (α → M)

Docstring: Given `Finite α`, `equivFunOnFinite` is the `Equiv` between `α →₀ β` and `α → β`.
(All functions on a finite type are finitely supported.) 

## BASE-LIBRARY REF Finite.of_fintype
∀ (α : Type u_4) [Fintype α], Finite α

Docstring: For efficiency reasons, we want `Finite` instances to have higher
priority than ones coming from `Fintype` instances. 

## BASE-LIBRARY REF Fin.fintype
(n : ℕ) → Fintype (Fin n)

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF Zero.toOfNat0
{α : Type u_1} → [Zero α] → OfNat α 0

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.toMulZeroClass
{α : Type u} → [self : NonUnitalNonAssocSemiring α] → MulZeroClass α

## BASE-LIBRARY REF NonAssocSemiring.toNonUnitalNonAssocSemiring
{α : Type u} → [self : NonAssocSemiring α] → NonUnitalNonAssocSemiring α

## BASE-LIBRARY REF Semiring.toNonAssocSemiring
{α : Type u} → [self : Semiring α] → NonAssocSemiring α

## BASE-LIBRARY REF CommSemiring.toSemiring
{R : Type u} → [self : CommSemiring R] → Semiring R

## BASE-LIBRARY REF One.toOfNat1
{α : Type u_1} → [One α] → OfNat α 1

## BASE-LIBRARY REF AddMonoidWithOne.toOne
{R : Type u_2} → [self : AddMonoidWithOne R] → One R

## BASE-LIBRARY REF AddCommMonoidWithOne.toAddMonoidWithOne
{R : Type u_2} → [self : AddCommMonoidWithOne R] → AddMonoidWithOne R

## BASE-LIBRARY REF NonAssocSemiring.toAddCommMonoidWithOne
{α : Type u} → [self : NonAssocSemiring α] → AddCommMonoidWithOne α

## BASE-LIBRARY REF MvPolynomial
Type u_1 → (R : Type u_2) → [CommSemiring R] → Type (max u_2 u_1)

Docstring: Multivariate polynomial, where `σ` is the index set of the variables and
`R` is the coefficient ring 

## BASE-LIBRARY REF Finset.prod
{ι : Type u_1} → {M : Type u_3} → [CommMonoid M] → Finset ι → (ι → M) → M

Docstring: `∏ x ∈ s, f x` is the product of `f x` as `x` ranges over the elements of the finite set `s`.

When the index type is a `Fintype`, the notation `∏ x, f x`, is a shorthand for
`∏ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF CommSemiring.toCommMonoid
{R : Type u} → [self : CommSemiring R] → CommMonoid R

## BASE-LIBRARY REF MvPolynomial.commSemiring
{R : Type u} → {σ : Type u_1} → [inst : CommSemiring R] → CommSemiring (MvPolynomial σ R)

## BASE-LIBRARY REF Finset.univ
{α : Type u_1} → [Fintype α] → Finset α

Docstring: `univ` is the universal finite set of type `Finset α` implied from
the assumption `Fintype α`. 

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
lem.sf.monomialExp-coeff

\leanhelper  The coefficient of $x^a$ in $x^a$ is $1$. The coefficient of $x^b$ in $x^a$ is $0$ when $a \neq b$.

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.sort
def.sf.sort

Let $a=\left( a_{1},a_{2},\ldots ,a_{N}\right) \in \mathbb {N}^{N}$. Then: 

\textbf{(a)} We let $x^{a}$ denote the monomial $x_{1}^{a_{1}}x_{2}^{a_{2}}\cdots x_{N}^{a_{N}}$. 

\textbf{(b)} We let $\operatorname *{sort}a$ mean the $N$-partition obtained from $a$ by sorting the entries of $a$ in weakly decreasing order.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The two declarations exactly formalize the two blueprint clauses. `monomialExp_coeff_self` states for every exponent tuple `a : Fin N \u2192 \u2115` that `coeff (Finsupp.equivFunOnFinite.symm a) (monomialExp a) = 1`, matching \u201cThe coefficient of $x^a$ in $x^a$ is $1$.\u201d Likewise, `monomialExp_coeff_ne` assumes `a \u2260 b` and concludes `coeff (Finsupp.equivFunOnFinite.symm b) (monomialExp a) = 0`, matching \u201cThe coefficient of $x^b$ in $x^a$ is $0$ when $a \\neq b$.\u201d The dependency defines `monomialExp a` as `\u220f i, MvPolynomial.X i ^ a i`, exactly the informal monomial $x^a=\\prod_i x_i^{a_i}$. The equivalence merely converts the finite tuple `b : Fin N \u2192 \u2115` into the finitely supported exponent representation expected by `MvPolynomial.coeff`. The universally quantified coefficient type `[CommSemiring R]` supplies the polynomial setting and makes the result more general; it does not narrow the informal assertion."
}