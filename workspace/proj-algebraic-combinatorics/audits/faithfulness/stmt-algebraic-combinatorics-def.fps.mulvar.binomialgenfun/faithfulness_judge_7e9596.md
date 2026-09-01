## TARGET AlgebraicCombinatorics.binomialGenFun (def) — ELABORATED SIGNATURE
AlgebraicCombinatorics.BivFPS ℚ

Body:
fun nm => ↑((nm 0).choose (nm 1))

Docstring: The generating function for binomial coefficients as a bivariate power series:
`∑_{n,k∈ℕ} C(n,k) x^n y^k`. 

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

## BASE-LIBRARY REF Rat
Type

Docstring: Rational numbers, implemented as a pair of integers `num / den` such that the
denominator is positive and the numerator and denominator are coprime.


## BASE-LIBRARY REF Rat.commSemiring
CommSemiring ℚ

## BASE-LIBRARY REF Finsupp
Type u_9 → (M : Type u_10) → [Zero M] → Type (max u_10 u_9)

Docstring: `Finsupp α M`, denoted `α →₀ M`, is the type of functions `f : α → M` such that
`f x = 0` for all but finitely many `x`. 

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

## BASE-LIBRARY REF CommSemiring
Type u → Type u

Docstring: A commutative semiring is a semiring with commutative multiplication. 

## BASE-LIBRARY REF MvPowerSeries
Type u_1 → Type u_2 → Type (max (max u_2 0) u_1)

Docstring: Multivariate formal power series, where `σ` is the index set of the variables
and `R` is the coefficient ring. 

## BASE-LIBRARY REF MvPowerSeries.X
{σ : Type u_1} → {R : Type u_2} → [Semiring R] → σ → MvPowerSeries σ R

Docstring: The variables of the multivariate formal power series ring. 

## BASE-LIBRARY REF CommSemiring.toSemiring
{R : Type u} → [self : CommSemiring R] → Semiring R

## INFORMAL STATEMENT
def.fps.mulvar.binomialGenFun

\leanhelper  The \emph{binomial generating function} is the bivariate power series 

\[  \operatorname {BinGen} := \sum _{n,k\in \mathbb {N}} \binom {n}{k}\,  x^n y^k \in \mathbb {Q}[[x,y]],  \]

 whose coefficient at $x^n y^k$ is $\binom {n}{k}$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.binom.binom
def.binom.binom

For any numbers $n$ and $k$, we set

\begin{equation}  \binom {n}{k}=\begin{cases}  \frac{n\left( n-1\right) \left( n-2\right) \cdots \left( n-k+1\right) }{k!}, &  \text{if }k\in \mathbb {N};\\ 0, &  \text{else.}\end{cases} \end{equation}

 Note that “numbers” is to be understood fairly liberally here. In particular, $n$ can be any integer, rational, real or complex number (or, more generally, any element in a $\mathbb {Q}$-algebra), whereas $k$ can be anything (although the only nonzero values of $\binom {n}{k}$ will be achieved for $k\in \mathbb {N}$, by the above definition).

## VERDICT
{
  "verdict": "faithful",
  "justification": "The target is an element of `AlgebraicCombinatorics.BivFPS \u211a`, whose body is `MvPowerSeries (Fin 2) \u211a`, matching the required `\u211a[[x,y]]`. Its coefficient function is exactly `fun nm => \u2191((nm 0).choose (nm 1))`: for an exponent vector `nm`, index `0` is the exponent of the first variable `x` (as confirmed by `BivFPS.x := MvPowerSeries.X 0`), and index `1` is the exponent of the second variable `y`. Thus the coefficient of `x^n y^k` is the rational cast of `Nat.choose n k`, i.e. `\\binom n k`, exactly as required by \u201cwhose coefficient at $x^n y^k$ is $\\binom n k$.\u201d"
}