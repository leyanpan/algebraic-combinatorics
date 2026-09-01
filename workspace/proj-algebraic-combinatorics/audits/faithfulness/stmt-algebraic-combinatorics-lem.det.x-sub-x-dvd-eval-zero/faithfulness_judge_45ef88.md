## TARGET AlgebraicCombinatorics.Determinants.X_sub_X_dvd_of_eval₂_eq_zero_fin_01 (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_1} [inst : CommRing R] (m : ℕ) (P : MvPolynomial (Fin (m + 2)) R),
  MvPolynomial.eval₂ MvPolynomial.C (fun i => if i = 0 then MvPolynomial.X 1 else MvPolynomial.X i) P = 0 →
    MvPolynomial.X 0 - MvPolynomial.X 1 ∣ P

Docstring: The multivariate factor theorem for Fin (m+2) with indices 0 and 1:
If P(X_0, X_1, ...) vanishes when X_0 is replaced by X_1, then (X_0 - X_1) divides P. 

## BASE-LIBRARY REF CommRing
Type u → Type u

Docstring: A commutative ring is a ring with commutative multiplication. 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF MvPolynomial
Type u_1 → (R : Type u_2) → [CommSemiring R] → Type (max u_2 u_1)

Docstring: Multivariate polynomial, where `σ` is the index set of the variables and
`R` is the coefficient ring 

## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


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

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

## BASE-LIBRARY REF CommRing.toCommSemiring
{α : Type u} → [s : CommRing α] → CommSemiring α

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

## BASE-LIBRARY REF MvPolynomial.eval₂
{R : Type u} →
  {S₁ : Type v} →
    {σ : Type u_1} →
      [inst : CommSemiring R] → [inst_1 : CommSemiring S₁] → (R →+* S₁) → (σ → S₁) → MvPolynomial σ R → S₁

Docstring: Evaluate a polynomial `p` given a valuation `g` of all the variables
and a ring hom `f` from the scalar ring to the target 

## BASE-LIBRARY REF MvPolynomial.commSemiring
{R : Type u} → {σ : Type u_1} → [inst : CommSemiring R] → CommSemiring (MvPolynomial σ R)

## BASE-LIBRARY REF MvPolynomial.C
{R : Type u} → {σ : Type u_1} → [inst : CommSemiring R] → R →+* MvPolynomial σ R

Docstring: `C a` is the constant polynomial with value `a` 

## BASE-LIBRARY REF ite
{α : Sort u} → (c : Prop) → [h : Decidable c] → α → α → α

Docstring: `if c then t else e` is notation for `ite c t e`, "if-then-else", which decides to
return `t` or `e` depending on whether `c` is true or false. The explicit argument
`c : Prop` does not have any actual computational content, but there is an additional
`[Decidable c]` argument synthesized by typeclass inference which actually
determines how to evaluate `c` to true or false. Write `if h : c then t else e`
instead for a "dependent if-then-else" `dite`, which allows `t`/`e` to use the fact
that `c` is true/false.


## BASE-LIBRARY REF Fin.instOfNat
{n : ℕ} → [NeZero n] → {i : ℕ} → OfNat (Fin n) i

## BASE-LIBRARY REF instNeZeroNatHAdd_1
∀ {n m : ℕ} [h : NeZero m], NeZero (n + m)

## BASE-LIBRARY REF Nat.instNeZeroSucc
∀ {n : ℕ}, NeZero (n + 1)

## BASE-LIBRARY REF instDecidableEqFin
(n : ℕ) → DecidableEq (Fin n)

## BASE-LIBRARY REF MvPolynomial.X
{R : Type u} → {σ : Type u_1} → [inst : CommSemiring R] → σ → MvPolynomial σ R

Docstring: `X n` is the degree `1` monomial $X_n$. 

## BASE-LIBRARY REF Zero.toOfNat0
{α : Type u_1} → [Zero α] → OfNat α 0

## BASE-LIBRARY REF MulZeroClass.toZero
{M₀ : Type u} → [self : MulZeroClass M₀] → Zero M₀

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.toMulZeroClass
{α : Type u} → [self : NonUnitalNonAssocSemiring α] → MulZeroClass α

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

## INFORMAL STATEMENT
lem.det.X-sub-X-dvd-eval-zero

\leanhelper  Let $R$ be an integral domain, and let $P \in R[x_0, x_1, \ldots , x_{m+1}]$. If $P$ vanishes when $x_0$ is replaced by $x_1$ (i.e., $P|_{x_0 = x_1} = 0$), then $(x_0 - x_1) \mid P$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.det.substxitoxj
def.det.substXiToXj

\leanhelper  The \emph{variable substitution} $\varphi _{i \to j}$ is the algebra homomorphism $R[x_1, \ldots , x_n] \to R[x_1, \ldots , x_n]$ that sends $x_i \mapsto x_j$ and fixes all other variables.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The formal binders `\u2200 {R : Type u_1} [CommRing R] (m : \u2115) (P : MvPolynomial (Fin (m + 2)) R)` cover the blueprint\u2019s polynomials `P \u2208 R[x_0, x_1, \u2026, x_{m+1}]`. The valuation `fun i => if i = 0 then MvPolynomial.X 1 else MvPolynomial.X i` sends `x\u2080` to `x\u2081` and fixes every other variable, exactly expressing `P|_{x\u2080 = x\u2081} = 0`; the conclusion `MvPolynomial.X 0 - MvPolynomial.X 1 \u2223 P` is precisely `(x\u2080 - x\u2081) \u2223 P`. The formal theorem assumes only `[CommRing R]`, whereas the blueprint assumes an integral domain. This is a strictly more general theorem with a weaker hypothesis, so it still implies the blueprint statement and is faithful."
}