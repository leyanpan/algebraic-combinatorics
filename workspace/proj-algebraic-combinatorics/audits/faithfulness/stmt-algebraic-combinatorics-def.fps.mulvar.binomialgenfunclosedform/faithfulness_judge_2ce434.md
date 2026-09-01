## TARGET AlgebraicCombinatorics.binomialGenFunClosedForm (def) — ELABORATED SIGNATURE
AlgebraicCombinatorics.BivFPS ℚ

Body:
(1 - AlgebraicCombinatorics.BivFPS.x * (1 + AlgebraicCombinatorics.BivFPS.y)).invOfUnit 1

Docstring: The closed form `1/(1 - x(1+y))` for the binomial generating function. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.BivFPS (def)
(R : Type u_2) → [CommSemiring R] → Type (max u_2 0)

Body:
fun R [CommSemiring R] => MvPowerSeries (Fin 2) R

Docstring: The algebra of formal power series in 2 variables (bivariate).
This corresponds to `K[[x, y]]` in the source. 

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

## BASE-LIBRARY REF Rat
Type

Docstring: Rational numbers, implemented as a pair of integers `num / den` such that the
denominator is positive and the numerator and denominator are coprime.


## BASE-LIBRARY REF Rat.commSemiring
CommSemiring ℚ

## BASE-LIBRARY REF MvPowerSeries.invOfUnit
{σ : Type u_1} → {R : Type u_2} → [inst : Ring R] → MvPowerSeries σ R → Rˣ → MvPowerSeries σ R

Docstring: A multivariate formal power series is invertible if the constant coefficient is invertible. 

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

## BASE-LIBRARY REF MvPowerSeries
Type u_1 → Type u_2 → Type (max (max u_2 0) u_1)

Docstring: Multivariate formal power series, where `σ` is the index set of the variables
and `R` is the coefficient ring. 

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

## BASE-LIBRARY REF CommSemiring
Type u → Type u

Docstring: A commutative semiring is a semiring with commutative multiplication. 

## BASE-LIBRARY REF MvPowerSeries.X
{σ : Type u_1} → {R : Type u_2} → [Semiring R] → σ → MvPowerSeries σ R

Docstring: The variables of the multivariate formal power series ring. 

## BASE-LIBRARY REF CommSemiring.toSemiring
{R : Type u} → [self : CommSemiring R] → Semiring R

## BASE-LIBRARY REF Fin.instOfNat
{n : ℕ} → [NeZero n] → {i : ℕ} → OfNat (Fin n) i

## INFORMAL STATEMENT
def.fps.mulvar.binomialGenFunClosedForm

\leanhelper  The \emph{closed form} of the binomial generating function is 

\[  \frac{1}{1 - x(1+y)} \in \mathbb {Q}[[x,y]].  \]

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

## VERDICT
{
  "verdict": "faithful",
  "justification": "The blueprint defines the closed form as `1 / (1 - x(1+y)) \u2208 \u211a[[x,y]]`. The target has type `AlgebraicCombinatorics.BivFPS \u211a`, whose body is `MvPowerSeries (Fin 2) \u211a`, and its body is `(1 - BivFPS.x * (1 + BivFPS.y)).invOfUnit 1`. Here `x` and `y` are respectively `MvPowerSeries.X 0` and `MvPowerSeries.X 1`, while `invOfUnit 1` constructs the inverse using the denominator\u2019s unit constant coefficient `1`. Thus the formal definition denotes exactly the stated reciprocal in the bivariate rational formal power series ring."
}