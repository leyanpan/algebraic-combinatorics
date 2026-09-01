## TARGET AlgebraicCombinatorics.Determinants.X_sub_X_dvd_sub_subst (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_1} [inst : CommRing R] {σ : Type u_2} [inst_1 : DecidableEq σ] (p : MvPolynomial σ R) (i j : σ),
  i ≠ j → MvPolynomial.X i - MvPolynomial.X j ∣ p - (AlgebraicCombinatorics.Determinants.substXiToXj i j) p

Docstring: The multivariate factor theorem: (X_i - X_j) divides P - P|_{X_i = X_j}.
This is the multivariate analogue of Polynomial.sub_dvd_eval_sub. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.Determinants.substXiToXj (def)
{R : Type u_1} →
  [inst : CommRing R] → {σ : Type u_2} → [DecidableEq σ] → σ → σ → MvPolynomial σ R →ₐ[R] MvPolynomial σ R

Body:
fun {R} [CommRing R] {σ} [DecidableEq σ] i j =>
  MvPolynomial.aeval fun k => if k = i then MvPolynomial.X j else MvPolynomial.X k

Docstring: Substitution that replaces X_i with X_j in a multivariate polynomial. 

## BASE-LIBRARY REF CommRing
Type u → Type u

Docstring: A commutative ring is a ring with commutative multiplication. 

## BASE-LIBRARY REF DecidableEq
Sort u → Sort (max 1 u)

Docstring: Propositional equality is `Decidable` for all elements of a type.

In other words, an instance of `DecidableEq α` is a means of deciding the proposition `a = b` is
for all `a b : α`.


## BASE-LIBRARY REF MvPolynomial
Type u_1 → (R : Type u_2) → [CommSemiring R] → Type (max u_2 u_1)

Docstring: Multivariate polynomial, where `σ` is the index set of the variables and
`R` is the coefficient ring 

## BASE-LIBRARY REF CommRing.toCommSemiring
{α : Type u} → [s : CommRing α] → CommSemiring α

## BASE-LIBRARY REF Ne
{α : Sort u} → α → α → Prop

Docstring: `a ≠ b`, or `Ne a b` is defined as `¬ (a = b)` or `a = b → False`,
and asserts that `a` and `b` are not equal.


Conventions for notations in identifiers:

 * The recommended spelling of `≠` in identifiers is `ne`.

## BASE-LIBRARY REF Dvd.dvd
{α : Type u_1} → [self : Dvd α] → α → α → Prop

Docstring: Divisibility. `a ∣ b` (typed as `\|`) means that there is some `c` such that `b = a * c`. 

Conventions for notations in identifiers:

 * The recommended spelling of `∣` in identifiers is `dvd`.

## BASE-LIBRARY REF semigroupDvd
{α : Type u_1} → [Semigroup α] → Dvd α

Docstring: There are two possible conventions for divisibility, which coincide in a `CommMonoid`.
This matches the convention for ordinals. 

## BASE-LIBRARY REF SemigroupWithZero.toSemigroup
{S₀ : Type u} → [self : SemigroupWithZero S₀] → Semigroup S₀

## BASE-LIBRARY REF NonUnitalSemiring.toSemigroupWithZero
{α : Type u} → [self : NonUnitalSemiring α] → SemigroupWithZero α

## BASE-LIBRARY REF NonUnitalCommSemiring.toNonUnitalSemiring
{α : Type u} → [self : NonUnitalCommSemiring α] → NonUnitalSemiring α

## BASE-LIBRARY REF NonUnitalCommRing.toNonUnitalCommSemiring
{α : Type u} → [s : NonUnitalCommRing α] → NonUnitalCommSemiring α

## BASE-LIBRARY REF CommRing.toNonUnitalCommRing
{α : Type u} → [s : CommRing α] → NonUnitalCommRing α

## BASE-LIBRARY REF MvPolynomial.instCommRingMvPolynomial
{R : Type u} → {σ : Type u_1} → [inst : CommRing R] → CommRing (MvPolynomial σ R)

## BASE-LIBRARY REF HSub.hSub
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HSub α β γ] → α → β → γ

Docstring: `a - b` computes the difference of `a` and `b`.
The meaning of this notation is type-dependent.
* For natural numbers, this operator saturates at 0: `a - b = 0` when `a ≤ b`. 

Conventions for notations in identifiers:

 * The recommended spelling of `-` in identifiers is `sub` (when used as a binary operator).

## BASE-LIBRARY REF instHSub
{α : Type u_1} → [Sub α] → HSub α α α

## BASE-LIBRARY REF SubNegMonoid.toSub
{G : Type u} → [self : SubNegMonoid G] → Sub G

## BASE-LIBRARY REF AddGroup.toSubNegMonoid
{A : Type u} → [self : AddGroup A] → SubNegMonoid A

## BASE-LIBRARY REF AddGroupWithOne.toAddGroup
{R : Type u} → [self : AddGroupWithOne R] → AddGroup R

## BASE-LIBRARY REF Ring.toAddGroupWithOne
{R : Type u} → [self : Ring R] → AddGroupWithOne R

## BASE-LIBRARY REF CommRing.toRing
{α : Type u} → [self : CommRing α] → Ring α

## BASE-LIBRARY REF MvPolynomial.X
{R : Type u} → {σ : Type u_1} → [inst : CommSemiring R] → σ → MvPolynomial σ R

Docstring: `X n` is the degree `1` monomial $X_n$. 

## BASE-LIBRARY REF DFunLike.coe
{F : Sort u_1} → {α : outParam (Sort u_2)} → {β : outParam (α → Sort u_3)} → [self : DFunLike F α β] → F → (a : α) → β a

Docstring: The coercion from `F` to a function. 

## BASE-LIBRARY REF AlgHom
(R : Type u) →
  (A : Type v) →
    (B : Type w) →
      [inst : CommSemiring R] →
        [inst_1 : Semiring A] → [inst_2 : Semiring B] → [Algebra R A] → [Algebra R B] → Type (max v w)

Docstring: Defining the homomorphism in the category R-Alg, denoted `A →ₐ[R] B`. 

## BASE-LIBRARY REF CommSemiring.toSemiring
{R : Type u} → [self : CommSemiring R] → Semiring R

## BASE-LIBRARY REF MvPolynomial.commSemiring
{R : Type u} → {σ : Type u_1} → [inst : CommSemiring R] → CommSemiring (MvPolynomial σ R)

## BASE-LIBRARY REF MvPolynomial.algebra
{R : Type u} →
  {S₁ : Type v} →
    {σ : Type u_1} →
      [inst : CommSemiring R] → [inst_1 : CommSemiring S₁] → [Algebra R S₁] → Algebra R (MvPolynomial σ S₁)

## BASE-LIBRARY REF Algebra.id
(R : Type u) → [inst : CommSemiring R] → Algebra R R

Docstring: The identity map inducing an `Algebra` structure. 

## BASE-LIBRARY REF AlgHom.funLike
{R : Type u} →
  {A : Type v} →
    {B : Type w} →
      [inst : CommSemiring R] →
        [inst_1 : Semiring A] →
          [inst_2 : Semiring B] → [inst_3 : Algebra R A] → [inst_4 : Algebra R B] → FunLike (A →ₐ[R] B) A B

## BASE-LIBRARY REF MvPolynomial.aeval
{R : Type u} →
  {S₁ : Type v} →
    {σ : Type u_1} →
      [inst : CommSemiring R] →
        [inst_1 : CommSemiring S₁] → [inst_2 : Algebra R S₁] → (σ → S₁) → MvPolynomial σ R →ₐ[R] S₁

Docstring: A map `σ → S₁` where `S₁` is an algebra over `R` generates an `R`-algebra homomorphism
from multivariate polynomials over `σ` to `S₁`. 

## BASE-LIBRARY REF ite
{α : Sort u} → (c : Prop) → [h : Decidable c] → α → α → α

Docstring: `if c then t else e` is notation for `ite c t e`, "if-then-else", which decides to
return `t` or `e` depending on whether `c` is true or false. The explicit argument
`c : Prop` does not have any actual computational content, but there is an additional
`[Decidable c]` argument synthesized by typeclass inference which actually
determines how to evaluate `c` to true or false. Write `if h : c then t else e`
instead for a "dependent if-then-else" `dite`, which allows `t`/`e` to use the fact
that `c` is true/false.


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

## INFORMAL STATEMENT
lem.det.X-sub-X-dvd-sub-subst

\leanhelper  Let $p \in R[x_1, \ldots , x_n]$ be a multivariate polynomial and $i \neq j$. Then $(x_i - x_j) \mid p - p|_{x_i = x_j}$, where $p|_{x_i = x_j}$ denotes the substitution of $x_j$ for $x_i$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.det.substxitoxj
def.det.substXiToXj

\leanhelper  The \emph{variable substitution} $\varphi _{i \to j}$ is the algebra homomorphism $R[x_1, \ldots , x_n] \to R[x_1, \ldots , x_n]$ that sends $x_i \mapsto x_j$ and fixes all other variables.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The target states, for `p : MvPolynomial \u03c3 R` and `i j : \u03c3`, that `i \u2260 j \u2192 X i - X j \u2223 p - (substXiToXj i j) p`, exactly matching \u201cLet \u2026 `i \u2260 j`. Then `(x_i - x_j) \u2223 p - p|_{x_i = x_j}`.\u201d The dependency body `MvPolynomial.aeval fun k => if k = i then X j else X k` sends `x_i \u21a6 x_j` and fixes every other variable, matching the informal definition. The binders `[CommRing R]` provide the natural coefficient setting needed for subtraction, while `[DecidableEq \u03c3]` merely implements the conditional substitution and is not a mathematical restriction. Quantifying over an arbitrary variable type `\u03c3` is more general than the displayed finite variables `x\u2081,\u2026,x\u2099`, so it does not weaken the blueprint statement."
}