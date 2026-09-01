## TARGET FloorCeiling.floor_of_int (theorem) — ELABORATED SIGNATURE
∀ (n : ℤ), ⌊↑n⌋ = n

Docstring: The floor of an integer is itself.
(Example from the textbook: ⌊n⌋ = n for n ∈ ℤ) 

## TARGET FloorCeiling.ceil_def (theorem) — ELABORATED SIGNATURE
∀ (a : ℝ) (n : ℤ), ⌈a⌉ ≤ n ↔ a ≤ ↑n

Docstring: The ceiling of a real number is the smallest integer ≥ a.
(Definition \ref{def.pars.floor-ceil})

This is the characterization: ⌈a⌉ ≤ n iff a ≤ n. 

## TARGET FloorCeiling.nat_div_eq_floor (theorem) — ELABORATED SIGNATURE
∀ (n m : ℕ), m ≠ 0 → n / m = ⌊↑n / ↑m⌋₊

Docstring: Natural number division equals the floor of rational division.
This connects `n / m` (natural number division) to `⌊n/m⌋` (floor of rational division). 

## TARGET FloorCeiling.floor_def (theorem) — ELABORATED SIGNATURE
∀ (a : ℝ) (n : ℤ), n ≤ ⌊a⌋ ↔ ↑n ≤ a

Docstring: The floor of a real number is the largest integer ≤ a.
(Definition \ref{def.pars.floor-ceil})

This is the characterization: n ≤ ⌊a⌋ iff n ≤ a. 

## TARGET FloorCeiling.ceil_of_int (theorem) — ELABORATED SIGNATURE
∀ (n : ℤ), ⌈↑n⌉ = n

Docstring: The ceiling of an integer is itself.
(Example from the textbook: ⌈n⌉ = n for n ∈ ℤ) 

## BASE-LIBRARY REF Int
Type

Docstring: The integers.

This type is special-cased by the compiler and overridden with an efficient implementation. The
runtime has a special representation for `Int` that stores “small” signed numbers directly, while
larger numbers use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)). A “small number” is an integer that can be encoded with one fewer bits
than the platform's pointer size (i.e. 63 bits on 64-bit architectures and 31 bits on 32-bit
architectures).


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

## BASE-LIBRARY REF Int.floor
{α : Type u_2} → [inst : Ring α] → [inst_1 : LinearOrder α] → [FloorRing α] → α → ℤ

Docstring: `Int.floor a` is the greatest integer `z` such that `z ≤ a`. It is denoted with `⌊a⌋`. 

## BASE-LIBRARY REF Real
Type

Docstring: The type `ℝ` of real numbers constructed as equivalence classes of Cauchy sequences of rational
numbers. 

## BASE-LIBRARY REF Real.instRing
Ring ℝ

## BASE-LIBRARY REF Real.linearOrder
LinearOrder ℝ

## BASE-LIBRARY REF Real.instFloorRing
FloorRing ℝ

## BASE-LIBRARY REF Int.cast
{R : Type u} → [IntCast R] → ℤ → R

Docstring: The canonical homomorphism `Int → R`. In most use cases, the target type will have a ring structure,
and this homomorphism should be a ring homomorphism.

`IntCast` and `NatCast` exist to allow different libraries with their own types that can be notated
as natural numbers to have consistent `simp` normal forms without needing to create coercion
simplification sets that are aware of all combinations. Libraries should make it easy to work with
`IntCast` where possible. For instance, in Mathlib there will be such a homomorphism (and thus an
`IntCast R` instance) whenever `R` is an additive group with a `1`.


## BASE-LIBRARY REF Real.instIntCast
IntCast ℝ

## BASE-LIBRARY REF Iff
Prop → Prop → Prop

Docstring: If and only if, or logical bi-implication. `a ↔ b` means that `a` implies `b` and vice versa.
By `propext`, this implies that `a` and `b` are equal and hence any expression involving `a`
is equivalent to the corresponding expression with `b` instead.


Conventions for notations in identifiers:

 * The recommended spelling of `↔` in identifiers is `iff`.

 * The recommended spelling of `<->` in identifiers is `iff` (prefer `↔` over `<->`).

## BASE-LIBRARY REF LE.le
{α : Type u} → [self : LE α] → α → α → Prop

Docstring: The less-equal relation: `x ≤ y` 

Conventions for notations in identifiers:

 * The recommended spelling of `≤` in identifiers is `le`.

 * The recommended spelling of `<=` in identifiers is `le` (prefer `≤` over `<=`).

## BASE-LIBRARY REF Int.instLEInt
LE ℤ

## BASE-LIBRARY REF Int.ceil
{α : Type u_2} → [inst : Ring α] → [inst_1 : LinearOrder α] → [FloorRing α] → α → ℤ

Docstring: `Int.ceil a` is the smallest integer `z` such that `a ≤ z`. It is denoted with `⌈a⌉`. 

## BASE-LIBRARY REF Real.instLE
LE ℝ

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF Ne
{α : Sort u} → α → α → Prop

Docstring: `a ≠ b`, or `Ne a b` is defined as `¬ (a = b)` or `a = b → False`,
and asserts that `a` and `b` are not equal.


Conventions for notations in identifiers:

 * The recommended spelling of `≠` in identifiers is `ne`.

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

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

## BASE-LIBRARY REF Nat.floor
{α : Type u_2} → [inst : Semiring α] → [inst_1 : PartialOrder α] → [FloorSemiring α] → α → ℕ

Docstring: `⌊a⌋₊` is the greatest natural `n` such that `n ≤ a`. If `a` is negative, then `⌊a⌋₊ = 0`. 

## BASE-LIBRARY REF Rat
Type

Docstring: Rational numbers, implemented as a pair of integers `num / den` such that the
denominator is positive and the numerator and denominator are coprime.


## BASE-LIBRARY REF Rat.semiring
Semiring ℚ

## BASE-LIBRARY REF Rat.instPartialOrder
PartialOrder ℚ

## BASE-LIBRARY REF FloorRing.toFloorSemiring
{α : Type u_2} → [inst : Ring α] → [inst_1 : LinearOrder α] → [IsStrictOrderedRing α] → [FloorRing α] → FloorSemiring α

## BASE-LIBRARY REF NormedRing.toRing
{α : Type u_5} → [self : NormedRing α] → Ring α

## BASE-LIBRARY REF NormedCommRing.toNormedRing
{α : Type u_5} → [self : NormedCommRing α] → NormedRing α

## BASE-LIBRARY REF NormedField.toNormedCommRing
{α : Type u_2} → [NormedField α] → NormedCommRing α

## BASE-LIBRARY REF Rat.instNormedField
NormedField ℚ

## BASE-LIBRARY REF Rat.linearOrder
LinearOrder ℚ

## BASE-LIBRARY REF Rat.instIsStrictOrderedRing
IsStrictOrderedRing ℚ

## BASE-LIBRARY REF Rat.instFloorRing
FloorRing ℚ

## BASE-LIBRARY REF Rat.instDiv
Div ℚ

Docstring: Division of rational numbers. Note: `div a 0 = 0`.  Written with a separate function `Rat.div`
as a wrapper so that the definition is not unfolded at `.instance` transparency. 

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

## INFORMAL STATEMENT
def.pars.floor-ceil

Let $a$ be a real number. 

Then, $\left\lfloor a\right\rfloor $ (called the \emph{floor} of $a$) means the largest integer that is $\leq a$. 

Likewise, $\left\lceil a\right\rceil $ (called the \emph{ceiling} of $a$) means the smallest integer that is $\geq a$.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The decisive declarations are `FloorCeiling.floor_def`, with `\u2200 (a : \u211d) (n : \u2124), n \u2264 \u230aa\u230b \u2194 \u2191n \u2264 a`, and `FloorCeiling.ceil_def`, with `\u2200 (a : \u211d) (n : \u2124), \u2308a\u2309 \u2264 n \u2194 a \u2264 \u2191n`. Since `\u230aa\u230b` and `\u2308a\u2309` are integers, these characterize them respectively as the greatest integer at most `a` and the least integer at least `a`, exactly matching the blueprint. The binders quantify over every real `a` and every integer `n`, with no added hypotheses. `floor_of_int`, `ceil_of_int`, and `nat_div_eq_floor` are ancillary consequences/applications; they do not weaken the two exact characterizations."
}