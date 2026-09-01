## TARGET AlgebraicCombinatorics.FPS.binom_def_formula (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : Field K] [inst_1 : CharZero K] (r : K) (n : ℕ),
  Ring.choose r n = (descPochhammer ℤ n).smeval r / ↑n.factorial

Docstring: **Definition \ref{def.binom.binom}** (Binomial Coefficient Formula):
For any element $r$ in a field of characteristic zero and $n \in \mathbb{N}$,
$$\binom{r}{n} = \frac{r(r-1)(r-2)\cdots(r-n+1)}{n!}$$

This is the fundamental definition of the binomial coefficient.
In Mathlib, this is expressed using the descending Pochhammer symbol:
`(descPochhammer ℤ n).smeval r = n.factorial • Ring.choose r n`

For fields of characteristic zero, we can write this as a division. 

## BASE-LIBRARY REF Field
Type u → Type u

Docstring: A `Field` is a `CommRing` with multiplicative inverses for nonzero elements.

An instance of `Field K` includes maps `ratCast : ℚ → K` and `qsmul : ℚ → K → K`.
Those two fields are needed to implement the `DivisionRing K → Algebra ℚ K` instance since we need
to control the specific definitions for some special cases of `K` (in particular `K = ℚ` itself).
See also note [forgetful inheritance].

If the field has positive characteristic `p`, our division by zero convention forces
`ratCast (1 / p) = 1 / 0 = 0`. 

## BASE-LIBRARY REF CharZero
(R : Type u_1) → [AddMonoidWithOne R] → Prop

Docstring: Typeclass for monoids with characteristic zero.
  (This is usually stated on fields but it makes sense for any additive monoid with 1.)

*Warning*: for a semiring `R`, `CharZero R` and `CharP R 0` need not coincide.
* `CharZero R` requires an injection `ℕ ↪ R`;
* `CharP R 0` asks that only `0 : ℕ` maps to `0 : R` under the map `ℕ → R`.
  For instance, endowing `{0, 1}` with addition given by `max` (i.e. `1` is absorbing), shows that
  `CharZero {0, 1}` does not hold and yet `CharP {0, 1} 0` does.
  This example is formalized in `Counterexamples/CharPZeroNeCharZero.lean`.


## BASE-LIBRARY REF AddGroupWithOne.toAddMonoidWithOne
{R : Type u} → [self : AddGroupWithOne R] → AddMonoidWithOne R

## BASE-LIBRARY REF Ring.toAddGroupWithOne
{R : Type u} → [self : Ring R] → AddGroupWithOne R

## BASE-LIBRARY REF DivisionRing.toRing
{K : Type u_2} → [self : DivisionRing K] → Ring K

## BASE-LIBRARY REF Field.toDivisionRing
{K : Type u} → [self : Field K] → DivisionRing K

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

## BASE-LIBRARY REF EuclideanDomain.toCommRing
{R : Type u} → [self : EuclideanDomain R] → CommRing R

## BASE-LIBRARY REF Field.toEuclideanDomain
{K : Type u_1} → [Field K] → EuclideanDomain K

## BASE-LIBRARY REF Monoid.toNatPow
{M : Type u_2} → [Monoid M] → Pow M ℕ

## BASE-LIBRARY REF MonoidWithZero.toMonoid
{M₀ : Type u} → [self : MonoidWithZero M₀] → Monoid M₀

## BASE-LIBRARY REF Semiring.toMonoidWithZero
{α : Type u} → [self : Semiring α] → MonoidWithZero α

## BASE-LIBRARY REF DivisionSemiring.toSemiring
{K : Type u_2} → [self : DivisionSemiring K] → Semiring K

## BASE-LIBRARY REF Semifield.toDivisionSemiring
{K : Type u_2} → [self : Semifield K] → DivisionSemiring K

## BASE-LIBRARY REF Field.toSemifield
{K : Type u_1} → [Field K] → Semifield K

## BASE-LIBRARY REF instBinomialRingOfModuleNNRat
{R : Type u_1} → [inst : AddCommMonoid R] → [_root_.Module ℚ≥0 R] → [inst_2 : Pow R ℕ] → BinomialRing R

## BASE-LIBRARY REF AddCommMonoidWithOne.toAddCommMonoid
{R : Type u_2} → [self : AddCommMonoidWithOne R] → AddCommMonoid R

## BASE-LIBRARY REF AddCommGroupWithOne.toAddCommMonoidWithOne
{R : Type u} → [self : AddCommGroupWithOne R] → AddCommMonoidWithOne R

## BASE-LIBRARY REF Algebra.toModule
{R : Type u_2} → {A : Type u_3} → {x : CommSemiring R} → {x_1 : Semiring A} → [Algebra R A] → _root_.Module R A

## BASE-LIBRARY REF NNRat
Type

Docstring: Nonnegative rational numbers. 

## BASE-LIBRARY REF instCommSemiringNNRat
CommSemiring ℚ≥0

## BASE-LIBRARY REF DivisionSemiring.toNNRatAlgebra
{R : Type u_2} → [inst : DivisionSemiring R] → [CharZero R] → Algebra ℚ≥0 R

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

## BASE-LIBRARY REF DivisionRing.toDivInvMonoid
{K : Type u_2} → [self : DivisionRing K] → DivInvMonoid K

## BASE-LIBRARY REF Polynomial.smeval
{R : Type u_3} →
  [inst : Semiring R] →
    Polynomial R → {S : Type u_4} → [inst_1 : AddCommMonoid S] → [Pow S ℕ] → [MulActionWithZero R S] → S → S

Docstring: Evaluate a polynomial `p` in the scalar semiring `R` at an element `x` in the target `S` using
scalar multiple `R`-action. 

## BASE-LIBRARY REF Int
Type

Docstring: The integers.

This type is special-cased by the compiler and overridden with an efficient implementation. The
runtime has a special representation for `Int` that stores “small” signed numbers directly, while
larger numbers use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)). A “small number” is an integer that can be encoded with one fewer bits
than the platform's pointer size (i.e. 63 bits on 64-bit architectures and 31 bits on 32-bit
architectures).


## BASE-LIBRARY REF Ring.toSemiring
{R : Type u} → [self : Ring R] → Semiring R

## BASE-LIBRARY REF Int.instRing
Ring ℤ

## BASE-LIBRARY REF descPochhammer
(R : Type u) → [inst : Ring R] → ℕ → Polynomial R

Docstring: `descPochhammer R n` is the polynomial `X * (X - 1) * ... * (X - n + 1)`,
with coefficients in the ring `R`.


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

## BASE-LIBRARY REF Module.toMulActionWithZero
{R : Type u_5} →
  {M : Type u_6} → {x : Semiring R} → {x_1 : AddCommMonoid M} → [_root_.Module R M] → MulActionWithZero R M

Docstring: A module over a semiring automatically inherits a `MulActionWithZero` structure. 

## BASE-LIBRARY REF AddCommGroup.toIntModule
(M : Type u_3) → [inst : AddCommGroup M] → _root_.Module ℤ M

## BASE-LIBRARY REF LieRing.toAddCommGroup
{L : Type v} → [self : LieRing L] → AddCommGroup L

## BASE-LIBRARY REF LieRing.ofAssociativeRing
{A : Type v} → [Ring A] → LieRing A

Docstring: An associative ring gives rise to a Lie ring by taking the bracket to be the ring commutator. 

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

## BASE-LIBRARY REF Nat.factorial
ℕ → ℕ

Docstring: `Nat.factorial n` is the factorial of `n`. 

## INFORMAL STATEMENT
def.binom.binom

For any numbers $n$ and $k$, we set

\begin{equation}  \binom {n}{k}=\begin{cases}  \frac{n\left( n-1\right) \left( n-2\right) \cdots \left( n-k+1\right) }{k!}, &  \text{if }k\in \mathbb {N};\\ 0, &  \text{else.}\end{cases} \end{equation}

 Note that “numbers” is to be understood fairly liberally here. In particular, $n$ can be any integer, rational, real or complex number (or, more generally, any element in a $\mathbb {Q}$-algebra), whereas $k$ can be anything (although the only nonzero values of $\binom {n}{k}$ will be achieved for $k\in \mathbb {N}$, by the above definition).

## VERDICT
{
  "verdict": "drift",
  "justification": "The target quantifies only over `\u2200 {K} [Field K] [CharZero K] (r : K) (n : \u2115)`, whereas the blueprint allows the upper argument to be \u201cany element in a \u211a-algebra\u201d and the lower argument `k` to \u201cbe anything,\u201d with value `0` when `k \u2209 \u2115`. Thus `[Field K]` is a mathematically substantive restriction beyond being a \u211a-algebra, and `(n : \u2115)` narrows the lower-index quantifier and entirely omits the blueprint\u2019s non-natural branch. On the natural-index field branch, `(descPochhammer \u2124 n).smeval r / \u2191n.factorial` correctly represents the stated falling-product formula. The drift enters both in the target binders and through `Ring.choose`, whose signature itself accepts only a natural-number index. To be faithful, the coefficient should be defined over the intended \u211a-algebra setting\u2014using rational scalar multiplication rather than field division if necessary\u2014and `Ring.choose` should be wrapped or replaced by an extended definition that agrees with it for natural lower indices and is `0` otherwise; the theorem should then cover both branches."
}