## TARGET AlgebraicCombinatorics.FPS.goldenRatioMinus (def) — ELABORATED SIGNATURE
ℝ

Body:
(1 - √5) / 2

Docstring: The conjugate golden ratio $\phi_- = \frac{1 - \sqrt{5}}{2}$.

**Mathlib note**: This is equal to `Real.goldenConj` in Mathlib. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.FPS.goldenRatioPlus (def)
ℝ

Body:
(1 + √5) / 2

Docstring: The golden ratio $\phi_+ = \frac{1 + \sqrt{5}}{2}$.

**Mathlib note**: This is equal to `Real.goldenRatio` in Mathlib. 

## BASE-LIBRARY REF Real
Type

Docstring: The type `ℝ` of real numbers constructed as equivalence classes of Cauchy sequences of rational
numbers. 

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

## BASE-LIBRARY REF DivInvMonoid.toDiv
{G : Type u} → [self : DivInvMonoid G] → Div G

## BASE-LIBRARY REF Real.instDivInvMonoid
DivInvMonoid ℝ

## BASE-LIBRARY REF HSub.hSub
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HSub α β γ] → α → β → γ

Docstring: `a - b` computes the difference of `a` and `b`.
The meaning of this notation is type-dependent.
* For natural numbers, this operator saturates at 0: `a - b = 0` when `a ≤ b`. 

Conventions for notations in identifiers:

 * The recommended spelling of `-` in identifiers is `sub` (when used as a binary operator).

## BASE-LIBRARY REF instHSub
{α : Type u_1} → [Sub α] → HSub α α α

## BASE-LIBRARY REF Real.instSub
Sub ℝ

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF One.toOfNat1
{α : Type u_1} → [One α] → OfNat α 1

## BASE-LIBRARY REF Real.instOne
One ℝ

## BASE-LIBRARY REF Real.sqrt
ℝ → ℝ

Docstring: The square root of a real number. This returns 0 for negative inputs.

This has notation `√x`. Note that `√x⁻¹` is parsed as `√(x⁻¹)`. 

## BASE-LIBRARY REF instOfNatAtLeastTwo
{R : Type u_1} → {n : ℕ} → [NatCast R] → [n.AtLeastTwo] → OfNat R n

Docstring: Recognize numeric literals which are at least `2` as terms of `R` via `Nat.cast`. This
instance is what makes things like `37 : R` type check.  Note that `0` and `1` are not needed
because they are recognized as terms of `R` (at least when `R` is an `AddMonoidWithOne`) through
`Zero` and `One`, respectively. 

## BASE-LIBRARY REF Real.instNatCast
NatCast ℝ

## BASE-LIBRARY REF HAdd.hAdd
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HAdd α β γ] → α → β → γ

Docstring: `a + b` computes the sum of `a` and `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `+` in identifiers is `add`.

## BASE-LIBRARY REF instHAdd
{α : Type u_1} → [Add α] → HAdd α α α

## BASE-LIBRARY REF Real.instAdd
Add ℝ

## INFORMAL STATEMENT
def.fib.golden_ratio_minus

\leanhelper  The \emph{conjugate golden ratio} $\phi _- = \frac{1-\sqrt{5}}{2}$.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The informal definition specifies \u201cthe conjugate golden ratio \u03c6\u208b = (1\u2212\u221a5)/2.\u201d The Lean target is a parameter-free definition of type `\u211d` with body `(1 - \u221a5) / 2`, using real subtraction, real square root, and real division. This exactly matches the blueprint formula, with no added hypotheses or restricted quantifiers."
}