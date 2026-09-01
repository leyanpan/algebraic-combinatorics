## TARGET AlgebraicCombinatorics.FPS.g_series' (def) — ELABORATED SIGNATURE
{K : Type u_1} → [inst : CommRing K] → [BinomialRing K] → K → PowerSeries K

Body:
fun {K} [CommRing K] [BinomialRing K] n => PowerSeries.binomialSeries K n

Docstring: The series g = (1+x)^n = binomialSeries K n 

## TARGET AlgebraicCombinatorics.FPS.f_series' (def) — ELABORATED SIGNATURE
{K : Type u_1} → [inst : CommRing K] → [BinomialRing K] → K → PowerSeries K

Body:
fun {K} [CommRing K] [BinomialRing K] n =>
  PowerSeries.mk fun m => if Even m then Ring.choose (n + ↑(m / 2) - 1) (m / 2) else 0

Docstring: The series f = ∑_i C(n+i-1, i) x^{2i} used in the proof 

## BASE-LIBRARY REF CommRing
Type u → Type u

Docstring: A commutative ring is a ring with commutative multiplication. 

## BASE-LIBRARY REF BinomialRing
(R : Type u_1) → [AddCommMonoid R] → [Pow R ℕ] → Type u_1

Docstring: A binomial ring is a ring for which ascending Pochhammer evaluations are uniquely divisible by
suitable factorials. We define this notion as a mixin for additive commutative monoids with natural
number powers, but retain the ring name. We introduce `Ring.multichoose` as the uniquely defined
quotient. 

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

## BASE-LIBRARY REF Monoid.toNatPow
{M : Type u_2} → [Monoid M] → Pow M ℕ

## BASE-LIBRARY REF MonoidWithZero.toMonoid
{M₀ : Type u} → [self : MonoidWithZero M₀] → Monoid M₀

## BASE-LIBRARY REF Semiring.toMonoidWithZero
{α : Type u} → [self : Semiring α] → MonoidWithZero α

## BASE-LIBRARY REF CommSemiring.toSemiring
{R : Type u} → [self : CommSemiring R] → Semiring R

## BASE-LIBRARY REF CommRing.toCommSemiring
{α : Type u} → [s : CommRing α] → CommSemiring α

## BASE-LIBRARY REF PowerSeries
Type u_1 → Type (max u_1 0)

Docstring: Formal power series over a coefficient type `R` 

## BASE-LIBRARY REF PowerSeries.binomialSeries
{R : Type u_1} → [inst : CommRing R] → [BinomialRing R] → (A : Type u_3) → [One A] → [SMul R A] → R → PowerSeries A

Docstring: The power series for `(1 + X) ^ r`. 

## BASE-LIBRARY REF AddMonoidWithOne.toOne
{R : Type u_2} → [self : AddMonoidWithOne R] → One R

## BASE-LIBRARY REF AddGroupWithOne.toAddMonoidWithOne
{R : Type u} → [self : AddGroupWithOne R] → AddMonoidWithOne R

## BASE-LIBRARY REF Ring.toAddGroupWithOne
{R : Type u} → [self : Ring R] → AddGroupWithOne R

## BASE-LIBRARY REF CommRing.toRing
{α : Type u} → [self : CommRing α] → Ring α

## BASE-LIBRARY REF Algebra.toSMul
{R : Type u} → {A : Type v} → {inst : CommSemiring R} → {inst_1 : Semiring A} → [self : Algebra R A] → SMul R A

## BASE-LIBRARY REF Algebra.id
(R : Type u) → [inst : CommSemiring R] → Algebra R R

Docstring: The identity map inducing an `Algebra` structure. 

## BASE-LIBRARY REF PowerSeries.mk
{R : Type u_2} → (ℕ → R) → PowerSeries R

Docstring: Constructor for formal power series. 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF ite
{α : Sort u} → (c : Prop) → [h : Decidable c] → α → α → α

Docstring: `if c then t else e` is notation for `ite c t e`, "if-then-else", which decides to
return `t` or `e` depending on whether `c` is true or false. The explicit argument
`c : Prop` does not have any actual computational content, but there is an additional
`[Decidable c]` argument synthesized by typeclass inference which actually
determines how to evaluate `c` to true or false. Write `if h : c then t else e`
instead for a "dependent if-then-else" `dite`, which allows `t`/`e` to use the fact
that `c` is true/false.


## BASE-LIBRARY REF Even
{α : Type u_2} → [Add α] → α → Prop

Docstring: An element `a` of a type `α` with addition satisfies `Even a` if `a = r + r`,
for some `r : α`. 

## BASE-LIBRARY REF instAddNat
Add ℕ

## BASE-LIBRARY REF Nat.instDecidablePredEven
DecidablePred Even

## BASE-LIBRARY REF Ring.choose
{R : Type u_1} → [inst : AddCommGroupWithOne R] → [inst_1 : Pow R ℕ] → [BinomialRing R] → R → ℕ → R

Docstring: The binomial coefficient `choose r n` generalizes the natural number `Nat.choose` function,
interpreted in terms of choosing without replacement. 

## BASE-LIBRARY REF NonAssocRing.toAddCommGroupWithOne
{α : Type u_1} → [self : NonAssocRing α] → AddCommGroupWithOne α

## BASE-LIBRARY REF NonAssocCommRing.toNonAssocRing
{α : Type u} → [self : NonAssocCommRing α] → NonAssocRing α

## BASE-LIBRARY REF CommRing.toNonAssocCommRing
{α : Type u} → [CommRing α] → NonAssocCommRing α

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

## BASE-LIBRARY REF HDiv.hDiv
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HDiv α β γ] → α → β → γ

Docstring: `a / b` computes the result of dividing `a` by `b`.
The meaning of this notation is type-dependent.
* For most types like `Nat`, `Int`, `Rat`, `Real`, `a / 0` is defined to be `0`.
* For `Nat`, `a / b` rounds downwards.
* For `Int`, `a / b` rounds downwards if `b` is positive or upwards if `b` is negative.
  It is implemented as `Int.ediv`, the unique function satisfying
  `a % b + b * (a / b) = a` and `0 ≤ a % b < natAbs b` for `b ≠ 0`.
  Other rounding conventions are available using the functions
  `Int.fdiv` (floor rounding) and `Int.tdiv` (truncation rounding).
* For `Float`, `a / 0` follows the IEEE 754 semantics for division,
  usually resulting in `inf` or `nan`. 

Conventions for notations in identifiers:

 * The recommended spelling of `/` in identifiers is `div`.

## BASE-LIBRARY REF instHDiv
{α : Type u_1} → [Div α] → HDiv α α α

## BASE-LIBRARY REF Nat.instDiv
Div ℕ

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

## BASE-LIBRARY REF Zero.toOfNat0
{α : Type u_1} → [Zero α] → OfNat α 0

## BASE-LIBRARY REF MulZeroClass.toZero
{M₀ : Type u} → [self : MulZeroClass M₀] → Zero M₀

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.toMulZeroClass
{α : Type u} → [self : NonUnitalNonAssocSemiring α] → MulZeroClass α

## INFORMAL STATEMENT
def.fps.f-series-g-series

\leanhelper  Define two FPSs for the binomial identity: 

\begin{align*}  f(n) & := \sum _{i\in \mathbb {N}} \binom {n+i-1}{i} x^{2i} \quad \text{(i.e., the even-indexed coefficients of $(1-x^2)^{-n}$)}, \\ g(n) & := \sum _{j\in \mathbb {N}} \binom {n}{j} x^j = (1+x)^n. \end{align*}

## VERDICT
{
  "verdict": "faithful",
  "justification": "The formal definitions match both displayed series. For `f`, the body `PowerSeries.mk fun m => if Even m then Ring.choose (n + \u2191(m / 2) - 1) (m / 2) else 0` gives coefficient zero at odd indices and, at `m = 2i`, coefficient `Ring.choose (n + i - 1) i`, exactly encoding `f(n) := \u2211_{i\u2208\u2115} binom(n+i-1,i) x^{2i}`. For `g`, the body `PowerSeries.binomialSeries K n` uses the library operation documented as \u201cThe power series for `(1 + X) ^ r`,\u201d matching `g(n) := \u2211_{j\u2208\u2115} binom(n,j)x^j = (1+x)^n`. The binders `{K} [CommRing K] [BinomialRing K] (n : K)` provide the coefficient setting needed for generalized binomial coefficients and formal power series; the informal statement imposes no conflicting coefficient domain or narrower type for `n`."
}