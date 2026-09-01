## TARGET AlgebraicCombinatorics.binomialGenFun_eq (theorem) — ELABORATED SIGNATURE
AlgebraicCombinatorics.binomialGenFun = AlgebraicCombinatorics.binomialGenFunClosedForm

Docstring: The binomial generating function equals its closed form.
`∑_{n,k∈ℕ} C(n,k) x^n y^k = 1/(1 - x(1+y))`

This is the main computation in the example from the source. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.BivFPS (def)
(R : Type u_2) → [CommSemiring R] → Type (max u_2 0)

Body:
fun R [CommSemiring R] => MvPowerSeries (Fin 2) R

Docstring: The algebra of formal power series in 2 variables (bivariate).
This corresponds to `K[[x, y]]` in the source. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.binomialGenFun (def)
AlgebraicCombinatorics.BivFPS ℚ

Body:
fun nm => ↑((nm 0).choose (nm 1))

Docstring: The generating function for binomial coefficients as a bivariate power series:
`∑_{n,k∈ℕ} C(n,k) x^n y^k`. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.binomialGenFunClosedForm (def)
AlgebraicCombinatorics.BivFPS ℚ

Body:
(1 - AlgebraicCombinatorics.BivFPS.x * (1 + AlgebraicCombinatorics.BivFPS.y)).invOfUnit 1

Docstring: The closed form `1/(1 - x(1+y))` for the binomial generating function. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.BivFPS.x (def)
{R : Type u_1} → [inst : CommSemiring R] → AlgebraicCombinatorics.BivFPS R

Body:
fun {R} [CommSemiring R] => MvPowerSeries.X 0

Docstring: The first variable `x` in a bivariate power series ring. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.BivFPS.y (def)
{R : Type u_1} → [inst : CommSemiring R] → AlgebraicCombinatorics.BivFPS R

Body:
fun {R} [CommSemiring R] => MvPowerSeries.X 1

Docstring: The second variable `y` in a bivariate power series ring. 

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

## BASE-LIBRARY REF Rat
Type

Docstring: Rational numbers, implemented as a pair of integers `num / den` such that the
denominator is positive and the numerator and denominator are coprime.


## BASE-LIBRARY REF Rat.commSemiring
CommSemiring ℚ

## BASE-LIBRARY REF CommSemiring
Type u → Type u

Docstring: A commutative semiring is a semiring with commutative multiplication. 

## BASE-LIBRARY REF MvPowerSeries
Type u_1 → Type u_2 → Type (max (max u_2 0) u_1)

Docstring: Multivariate formal power series, where `σ` is the index set of the variables
and `R` is the coefficient ring. 

## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

## BASE-LIBRARY REF Finsupp
Type u_9 → (M : Type u_10) → [Zero M] → Type (max u_10 u_9)

Docstring: `Finsupp α M`, denoted `α →₀ M`, is the type of functions `f : α → M` such that
`f x = 0` for all but finitely many `x`. 

## BASE-LIBRARY REF MulZeroClass.toZero
{M₀ : Type u} → [self : MulZeroClass M₀] → Zero M₀

## BASE-LIBRARY REF Nat.instMulZeroClass
MulZeroClass ℕ

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


## BASE-LIBRARY REF Rat.instNatCast
NatCast ℚ

## BASE-LIBRARY REF Nat.choose
ℕ → ℕ → ℕ

Docstring: `choose n k` is the number of `k`-element subsets in an `n`-element set. Also known as binomial
coefficients. For the fact that this is the number of `k`-element-subsets of an `n`-element
set, see `Finset.card_powersetCard`. 

## BASE-LIBRARY REF DFunLike.coe
{F : Sort u_1} → {α : outParam (Sort u_2)} → {β : outParam (α → Sort u_3)} → [self : DFunLike F α β] → F → (a : α) → β a

Docstring: The coercion from `F` to a function. 

## BASE-LIBRARY REF Finsupp.instFunLike
{α : Type u_1} → {M : Type u_4} → [inst : Zero M] → FunLike (α →₀ M) α M

## BASE-LIBRARY REF Fin.instOfNat
{n : ℕ} → [NeZero n] → {i : ℕ} → OfNat (Fin n) i

## BASE-LIBRARY REF MvPowerSeries.invOfUnit
{σ : Type u_1} → {R : Type u_2} → [inst : Ring R] → MvPowerSeries σ R → Rˣ → MvPowerSeries σ R

Docstring: A multivariate formal power series is invertible if the constant coefficient is invertible. 

## BASE-LIBRARY REF NormedRing.toRing
{α : Type u_5} → [self : NormedRing α] → Ring α

## BASE-LIBRARY REF NormedCommRing.toNormedRing
{α : Type u_5} → [self : NormedCommRing α] → NormedRing α

## BASE-LIBRARY REF NormedField.toNormedCommRing
{α : Type u_2} → [NormedField α] → NormedCommRing α

## BASE-LIBRARY REF Rat.instNormedField
NormedField ℚ

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

## BASE-LIBRARY REF MvPowerSeries.instAddGroup
{σ : Type u_1} → {R : Type u_2} → [AddGroup R] → AddGroup (MvPowerSeries σ R)

## BASE-LIBRARY REF Rat.addGroup
AddGroup ℚ

## BASE-LIBRARY REF One.toOfNat1
{α : Type u_1} → [One α] → OfNat α 1

## BASE-LIBRARY REF MvPowerSeries.instOne
{σ : Type u_1} → {R : Type u_2} → [Semiring R] → One (MvPowerSeries σ R)

## BASE-LIBRARY REF Rat.semiring
Semiring ℚ

## BASE-LIBRARY REF HMul.hMul
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HMul α β γ] → α → β → γ

Docstring: `a * b` computes the product of `a` and `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `*` in identifiers is `mul`.

## BASE-LIBRARY REF instHMul
{α : Type u_1} → [Mul α] → HMul α α α

## BASE-LIBRARY REF MvPowerSeries.instMul
{σ : Type u_1} → {R : Type u_2} → [Semiring R] → Mul (MvPowerSeries σ R)

## BASE-LIBRARY REF HAdd.hAdd
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HAdd α β γ] → α → β → γ

Docstring: `a + b` computes the sum of `a` and `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `+` in identifiers is `add`.

## BASE-LIBRARY REF instHAdd
{α : Type u_1} → [Add α] → HAdd α α α

## BASE-LIBRARY REF Distrib.toAdd
{R : Type u_1} → [self : Distrib R] → Add R

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

## BASE-LIBRARY REF MvPowerSeries.instCommRing
{σ : Type u_1} → {R : Type u_2} → [CommRing R] → CommRing (MvPowerSeries σ R)

## BASE-LIBRARY REF Rat.commRing
CommRing ℚ

## BASE-LIBRARY REF Units
(α : Type u) → [Monoid α] → Type u

Docstring: Units of a `Monoid`, bundled version. Notation: `αˣ`.

An element of a `Monoid` is a unit if it has a two-sided inverse.
This version bundles the inverse element so that it can be computed.
For a predicate see `IsUnit`. 

## BASE-LIBRARY REF MonoidWithZero.toMonoid
{M₀ : Type u} → [self : MonoidWithZero M₀] → Monoid M₀

## BASE-LIBRARY REF Semiring.toMonoidWithZero
{α : Type u} → [self : Semiring α] → MonoidWithZero α

## BASE-LIBRARY REF Ring.toSemiring
{R : Type u} → [self : Ring R] → Semiring R

## BASE-LIBRARY REF Units.instOne
{α : Type u} → [inst : Monoid α] → One αˣ

Docstring: Units of a monoid have a unit 

## BASE-LIBRARY REF MvPowerSeries.X
{σ : Type u_1} → {R : Type u_2} → [Semiring R] → σ → MvPowerSeries σ R

Docstring: The variables of the multivariate formal power series ring. 

## BASE-LIBRARY REF CommSemiring.toSemiring
{R : Type u} → [self : CommSemiring R] → Semiring R

## INFORMAL STATEMENT
thm.fps.mulvar.binomialGenFun-eq

\leanhelper  The binomial generating function equals its closed form: 

\[  \sum _{n,k\in \mathbb {N}} \binom {n}{k}\,  x^n y^k = \frac{1}{1-x(1+y)}.  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.binom.binom
def.binom.binom

For any numbers $n$ and $k$, we set

\begin{equation}  \binom {n}{k}=\begin{cases}  \frac{n\left( n-1\right) \left( n-2\right) \cdots \left( n-k+1\right) }{k!}, &  \text{if }k\in \mathbb {N};\\ 0, &  \text{else.}\end{cases} \end{equation}

 Note that “numbers” is to be understood fairly liberally here. In particular, $n$ can be any integer, rational, real or complex number (or, more generally, any element in a $\mathbb {Q}$-algebra), whereas $k$ can be anything (although the only nonzero values of $\binom {n}{k}$ will be achieved for $k\in \mathbb {N}$, by the above definition).

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.mulvar.binomialgenfun
def.fps.mulvar.binomialGenFun

\leanhelper  The \emph{binomial generating function} is the bivariate power series 

\[  \operatorname {BinGen} := \sum _{n,k\in \mathbb {N}} \binom {n}{k}\,  x^n y^k \in \mathbb {Q}[[x,y]],  \]

 whose coefficient at $x^n y^k$ is $\binom {n}{k}$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.mulvar.binomialgenfunclosedform
def.fps.mulvar.binomialGenFunClosedForm

\leanhelper  The \emph{closed form} of the binomial generating function is 

\[  \frac{1}{1 - x(1+y)} \in \mathbb {Q}[[x,y]].  \]

## VERDICT
{
  "verdict": "faithful",
  "justification": "The target asserts exactly `AlgebraicCombinatorics.binomialGenFun = AlgebraicCombinatorics.binomialGenFunClosedForm`, matching the blueprint\u2019s equality between the binomial generating function and its closed form. The left definition is a bivariate formal power series over `\u211a` with coefficient `\u2191((nm 0).choose (nm 1))`, so the coefficient of `x^n y^k` is the rational cast of `Nat.choose n k`, matching `\u2211_{n,k\u2208\u2115} binom(n,k) x^n y^k \u2208 \u211a[[x,y]]`. The right definition is `(1 - x * (1 + y)).invOfUnit 1`; since the denominator has constant coefficient `1`, this represents its formal-power-series inverse, matching `1/(1-x(1+y))`. The elaborated signature has no additional hypotheses or narrowed quantifiers."
}