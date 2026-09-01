## TARGET AlgebraicCombinatorics.pentagonal_deriv_identity (theorem) — ELABORATED SIGNATURE
PowerSeries.X * (PowerSeries.derivative ℤ) AlgebraicCombinatorics.pentagonalSeries =
  -AlgebraicCombinatorics.pentagonalSeries * AlgebraicCombinatorics.sigmaSeries

Docstring: The key identity x * Q' = -Q * S, where Q is the pentagonal series and S is the
sum of divisors generating function.

This follows from Euler's pentagonal number theorem (PQ = 1 where P is the partition
generating function) and the identity xP' = SP. Taking the derivative of PQ = 1 gives
P'Q + PQ' = 0, so Q' = -P'Q/P. Multiplying by x: xQ' = -xP'Q/P = -SQ (using xP' = SP).

Note: This lemma depends on `euler_pentagonal_number_theorem` and `partition_generating_function`
which are being proved separately. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.pentagonalSeries (def)
{R : Type u_1} → [CommRing R] → PowerSeries R

Body:
fun {R} [CommRing R] => PowerSeries.mk fun n => ↑(AlgebraicCombinatorics.pentagonalCoeff n)

Docstring: The alternating sum ∑_{k∈ℤ} (-1)^k x^{w_k} as a formal power series.
This is well-defined because the pentagonal numbers grow quadratically.

We define the coefficient at n to be (-1)^k if n = w_k for some k, and 0 otherwise.
Since pentagonal numbers are injective, this is well-defined. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.sigmaSeries (def)
PowerSeries ℤ

Body:
PowerSeries.mk fun n => if n = 0 then 0 else ↑((ArithmeticFunction.sigma 1) n)

Docstring: The sum of divisors generating function: S = ∑_{k>0} σ(k) x^k.
This is the generating function for the sum of divisors function σ₁. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.pentagonalCoeff (def)
ℕ → ℤ

Body:
fun n =>
  match AlgebraicCombinatorics.pentagonalNumberInverse n with
  | some k => (-1) ^ k.natAbs
  | none => 0

Docstring: The coefficient of x^n in the pentagonal series.
Returns (-1)^k if n = w_k for some k, and 0 otherwise.

Note: We use `k.natAbs` to compute the sign correctly for negative k,
since (-1)^k = (-1)^|k| for integers (as (-1)^{-m} = (-1)^m). 

## PROJECT DEPENDENCY AlgebraicCombinatorics.pentagonalNumberInverse (def)
ℕ → Option ℤ

Body:
fun n =>
  have bound := n + 1;
  have posResult :=
    List.find? (fun k => decide (AlgebraicCombinatorics.pentagonalNumber k = n)) do
      let a ← List.range bound
      pure ↑a;
  match posResult with
  | some k => some k
  | none =>
    have negResult :=
      List.find? (fun k => decide (AlgebraicCombinatorics.pentagonalNumber (-k - 1) = n)) do
        let a ← List.range bound
        pure ↑a;
    match negResult with
    | some k => some (-k - 1)
    | none => none

Docstring: Helper: Check if n is a pentagonal number and return the corresponding k.
Returns none if n is not a pentagonal number.

This is computable for any given n by checking a finite range of k values,
since pentagonal numbers grow quadratically. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.pentagonalNumber (def)
ℤ → ℕ

Body:
fun k => ((3 * k - 1) * k / 2).toNat

Docstring: The k-th pentagonal number, defined as w_k = (3k - 1) * k / 2.
This is always a nonnegative integer for any k ∈ ℤ.
(Definition \ref{def.pars.pent-num}) 

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

## BASE-LIBRARY REF PowerSeries
Type u_1 → Type (max u_1 0)

Docstring: Formal power series over a coefficient type `R` 

## BASE-LIBRARY REF Int
Type

Docstring: The integers.

This type is special-cased by the compiler and overridden with an efficient implementation. The
runtime has a special representation for `Int` that stores “small” signed numbers directly, while
larger numbers use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)). A “small number” is an integer that can be encoded with one fewer bits
than the platform's pointer size (i.e. 63 bits on 64-bit architectures and 31 bits on 32-bit
architectures).


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

## BASE-LIBRARY REF Unit
Type

Docstring: The canonical type with one element. This element is written `()`.

`Unit` has a number of uses:
* It can be used to model control flow that returns from a function call without providing other
  information.
* Monadic actions that return `Unit` have side effects without computing values.
* In polymorphic types, it can be used to indicate that no data is to be stored in a particular
  field.


## BASE-LIBRARY REF Int.instSemiring
Semiring ℤ

## BASE-LIBRARY REF PowerSeries.X
{R : Type u_1} → [Semiring R] → PowerSeries R

Docstring: The variable of the formal power series ring. 

## BASE-LIBRARY REF DFunLike.coe
{F : Sort u_1} → {α : outParam (Sort u_2)} → {β : outParam (α → Sort u_3)} → [self : DFunLike F α β] → F → (a : α) → β a

Docstring: The coercion from `F` to a function. 

## BASE-LIBRARY REF Derivation
(R : Type u_1) →
  (A : Type u_2) →
    (M : Type u_3) →
      [inst : CommSemiring R] →
        [inst_1 : CommSemiring A] →
          [inst_2 : AddCommMonoid M] → [Algebra R A] → [_root_.Module A M] → [_root_.Module R M] → Type (max u_2 u_3)

Docstring: `D : Derivation R A M` is an `R`-linear map from `A` to `M` that satisfies the `leibniz`
equality. We also require that `D 1 = 0`. See `Derivation.mk'` for a constructor that deduces this
assumption from the Leibniz rule when `M` is cancellative.

TODO: update this when bimodules are defined. 

## BASE-LIBRARY REF Int.instCommSemiring
CommSemiring ℤ

## BASE-LIBRARY REF PowerSeries.instCommSemiring
{R : Type u_1} → [CommSemiring R] → CommSemiring (PowerSeries R)

## BASE-LIBRARY REF PowerSeries.instAddCommMonoid
{R : Type u_1} → [AddCommMonoid R] → AddCommMonoid (PowerSeries R)

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.toAddCommMonoid
{α : Type u} → [self : NonUnitalNonAssocSemiring α] → AddCommMonoid α

## BASE-LIBRARY REF NonAssocSemiring.toNonUnitalNonAssocSemiring
{α : Type u} → [self : NonAssocSemiring α] → NonUnitalNonAssocSemiring α

## BASE-LIBRARY REF Semiring.toNonAssocSemiring
{α : Type u} → [self : Semiring α] → NonAssocSemiring α

## BASE-LIBRARY REF CommSemiring.toSemiring
{R : Type u} → [self : CommSemiring R] → Semiring R

## BASE-LIBRARY REF PowerSeries.instAlgebra
{R : Type u_1} →
  {A : Type u_2} → [inst : Semiring A] → [inst_1 : CommSemiring R] → [Algebra R A] → Algebra R (PowerSeries A)

## BASE-LIBRARY REF Algebra.id
(R : Type u) → [inst : CommSemiring R] → Algebra R R

Docstring: The identity map inducing an `Algebra` structure. 

## BASE-LIBRARY REF Semiring.toModule
{R : Type u_1} → [inst : Semiring R] → _root_.Module R R

## BASE-LIBRARY REF PowerSeries.instModule
{R : Type u_1} →
  {A : Type u_2} →
    [inst : Semiring R] → [inst_1 : AddCommMonoid A] → [_root_.Module R A] → _root_.Module R (PowerSeries A)

## BASE-LIBRARY REF Derivation.instFunLike
{R : Type u_1} →
  {A : Type u_2} →
    {M : Type u_4} →
      [inst : CommSemiring R] →
        [inst_1 : CommSemiring A] →
          [inst_2 : AddCommMonoid M] →
            [inst_3 : Algebra R A] →
              [inst_4 : _root_.Module A M] → [inst_5 : _root_.Module R M] → FunLike (Derivation R A M) A M

## BASE-LIBRARY REF PowerSeries.derivative
(R : Type u_1) → [inst : CommSemiring R] → Derivation R (PowerSeries R) (PowerSeries R)

Docstring: The formal derivative of a formal power series 

## BASE-LIBRARY REF Int.instCommRing
CommRing ℤ

## BASE-LIBRARY REF Neg.neg
{α : Type u} → [self : Neg α] → α → α

Docstring: `-a` computes the negative or opposite of `a`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `-` in identifiers is `neg` (when used as a unary operator).

## BASE-LIBRARY REF NegZeroClass.toNeg
{G : Type u_2} → [self : NegZeroClass G] → Neg G

## BASE-LIBRARY REF SubNegZeroMonoid.toNegZeroClass
{G : Type u_2} → [self : SubNegZeroMonoid G] → NegZeroClass G

## BASE-LIBRARY REF SubtractionMonoid.toSubNegZeroMonoid
{α : Type u_1} → [SubtractionMonoid α] → SubNegZeroMonoid α

## BASE-LIBRARY REF SubtractionCommMonoid.toSubtractionMonoid
{G : Type u} → [self : SubtractionCommMonoid G] → SubtractionMonoid G

## BASE-LIBRARY REF AddCommGroup.toDivisionAddCommMonoid
{G : Type u_1} → [AddCommGroup G] → SubtractionCommMonoid G

## BASE-LIBRARY REF PowerSeries.instAddCommGroup
{R : Type u_1} → [AddCommGroup R] → AddCommGroup (PowerSeries R)

## BASE-LIBRARY REF Int.instAddCommGroup
AddCommGroup ℤ

## BASE-LIBRARY REF CommRing
Type u → Type u

Docstring: A commutative ring is a ring with commutative multiplication. 

## BASE-LIBRARY REF PowerSeries.mk
{R : Type u_2} → (ℕ → R) → PowerSeries R

Docstring: Constructor for formal power series. 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF Int.cast
{R : Type u} → [IntCast R] → ℤ → R

Docstring: The canonical homomorphism `Int → R`. In most use cases, the target type will have a ring structure,
and this homomorphism should be a ring homomorphism.

`IntCast` and `NatCast` exist to allow different libraries with their own types that can be notated
as natural numbers to have consistent `simp` normal forms without needing to create coercion
simplification sets that are aware of all combinations. Libraries should make it easy to work with
`IntCast` where possible. For instance, in Mathlib there will be such a homomorphism (and thus an
`IntCast R` instance) whenever `R` is an additive group with a `1`.


## BASE-LIBRARY REF AddGroupWithOne.toIntCast
{R : Type u} → [self : AddGroupWithOne R] → IntCast R

## BASE-LIBRARY REF Ring.toAddGroupWithOne
{R : Type u} → [self : Ring R] → AddGroupWithOne R

## BASE-LIBRARY REF CommRing.toRing
{α : Type u} → [self : CommRing α] → Ring α

## BASE-LIBRARY REF ite
{α : Sort u} → (c : Prop) → [h : Decidable c] → α → α → α

Docstring: `if c then t else e` is notation for `ite c t e`, "if-then-else", which decides to
return `t` or `e` depending on whether `c` is true or false. The explicit argument
`c : Prop` does not have any actual computational content, but there is an additional
`[Decidable c]` argument synthesized by typeclass inference which actually
determines how to evaluate `c` to true or false. Write `if h : c then t else e`
instead for a "dependent if-then-else" `dite`, which allows `t`/`e` to use the fact
that `c` is true/false.


## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

## BASE-LIBRARY REF instDecidableEqNat
DecidableEq ℕ

## BASE-LIBRARY REF instOfNat
{n : ℕ} → OfNat ℤ n

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


## BASE-LIBRARY REF instNatCastInt
NatCast ℤ

## BASE-LIBRARY REF ArithmeticFunction
(R : Type u_1) → [Zero R] → Type (max 0 u_1)

Docstring: An arithmetic function is a function from `ℕ` that maps 0 to 0. In the literature, they are
often instead defined as functions from `ℕ+`. Multiplication on `ArithmeticFunctions` is by
Dirichlet convolution. 

## BASE-LIBRARY REF MulZeroClass.toZero
{M₀ : Type u} → [self : MulZeroClass M₀] → Zero M₀

## BASE-LIBRARY REF Nat.instMulZeroClass
MulZeroClass ℕ

## BASE-LIBRARY REF ArithmeticFunction.instFunLikeNat
{R : Type u_1} → [inst : Zero R] → FunLike (ArithmeticFunction R) ℕ R

## BASE-LIBRARY REF ArithmeticFunction.sigma
ℕ → ArithmeticFunction ℕ

Docstring: `σ k n` is the sum of the `k`th powers of the divisors of `n` 

## BASE-LIBRARY REF Option
Type u → Type u

Docstring: Optional values, which are either `some` around a value from the underlying type or `none`.

`Option` can represent nullable types or computations that might fail. In the codomain of a function
type, it can also represent partiality.


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

## BASE-LIBRARY REF Int.instMonoid
Monoid ℤ

## BASE-LIBRARY REF Int.instNegInt
Neg ℤ

## BASE-LIBRARY REF Int.natAbs
ℤ → ℕ

Docstring: The absolute value of an integer is its distance from `0`.

This function is overridden by the compiler with an efficient implementation. This definition is
the logical model.

Examples:
 * `(7 : Int).natAbs = 7`
 * `(0 : Int).natAbs = 0`
 * `(-11 : Int).natAbs = 11`


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

## BASE-LIBRARY REF List.find?
{α : Type u} → (α → Bool) → List α → Option α

Docstring: Returns the first element of the list for which the predicate `p` returns `true`, or `none` if no
such element is found.

`O(|l|)`.

Examples:
* `[7, 6, 5, 8, 1, 2, 6].find? (· < 5) = some 1`
* `[7, 6, 5, 8, 1, 2, 6].find? (· < 1) = none`


## BASE-LIBRARY REF Decidable.decide
(p : Prop) → [h : Decidable p] → Bool

Docstring: Converts a decidable proposition into a `Bool`.

If `p : Prop` is decidable, then `decide p : Bool` is the Boolean value
that is `true` if `p` is true and `false` if `p` is false.


## BASE-LIBRARY REF Bind.bind
{m : Type u → Type v} → [self : Bind m] → {α β : Type u} → m α → (α → m β) → m β

Docstring: Sequences two computations, allowing the second to depend on the value computed by the first.

If `x : m α` and `f : α → m β`, then `x >>= f : m β` represents the result of executing `x` to get
a value of type `α` and then passing it to `f`.


Conventions for notations in identifiers:

 * The recommended spelling of `>>=` in identifiers is `bind`.

## BASE-LIBRARY REF List
Type u → Type u

Docstring: Linked lists: ordered lists, in which each element has a reference to the next element.

Most operations on linked lists take time proportional to the length of the list, because each
element must be traversed to find the next element.

`List α` is isomorphic to `Array α`, but they are useful for different things:
* `List α` is easier for reasoning, and `Array α` is modeled as a wrapper around `List α`.
* `List α` works well as a persistent data structure, when many copies of the tail are shared. When
  the value is not shared, `Array α` will have better performance because it can do destructive
  updates.


## BASE-LIBRARY REF Monad.toBind
{m : Type u → Type v} → [self : Monad m] → Bind m

## BASE-LIBRARY REF List.instMonad
Monad List

## BASE-LIBRARY REF List.range
ℕ → List ℕ

Docstring: Returns a list of the numbers from `0` to `n` exclusive, in increasing order.

`O(n)`.

Examples:
* `range 5 = [0, 1, 2, 3, 4]`
* `range 0 = []`
* `range 2 = [0, 1]`


## BASE-LIBRARY REF Pure.pure
{f : Type u → Type v} → [self : Pure f] → {α : Type u} → α → f α

Docstring: Given `a : α`, then `pure a : f α` represents an action that does nothing and returns `a`.

Examples:
* `(pure "hello" : Option String) = some "hello"`
* `(pure "hello" : Except (Array String) String) = Except.ok "hello"`
* `(pure "hello" : StateM Nat String).run 105 = ("hello", 105)`


## BASE-LIBRARY REF Applicative.toPure
{f : Type u → Type v} → [self : Applicative f] → Pure f

## BASE-LIBRARY REF Monad.toApplicative
{m : Type u → Type v} → [self : Monad m] → Applicative m

## BASE-LIBRARY REF Option.some
{α : Type u} → α → Option α

Docstring: Some value of type `α`. 

## BASE-LIBRARY REF HSub.hSub
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HSub α β γ] → α → β → γ

Docstring: `a - b` computes the difference of `a` and `b`.
The meaning of this notation is type-dependent.
* For natural numbers, this operator saturates at 0: `a - b = 0` when `a ≤ b`. 

Conventions for notations in identifiers:

 * The recommended spelling of `-` in identifiers is `sub` (when used as a binary operator).

## BASE-LIBRARY REF instHSub
{α : Type u_1} → [Sub α] → HSub α α α

## BASE-LIBRARY REF Int.instSub
Sub ℤ

## BASE-LIBRARY REF Option.none
{α : Type u} → Option α

Docstring: No value. 

## BASE-LIBRARY REF Int.toNat
ℤ → ℕ

Docstring: Converts an integer into a natural number. Negative numbers are converted to `0`.

Examples:
* `(7 : Int).toNat = 7`
* `(0 : Int).toNat = 0`
* `(-7 : Int).toNat = 0`


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

## BASE-LIBRARY REF Int.instDiv
Div ℤ

Docstring: The `Div Int` and `Mod Int` instances use `Int.ediv` and `Int.emod` for compatibility with SMT-LIB and
because mathematical reasoning tends to be easier.


## BASE-LIBRARY REF Int.instMul
Mul ℤ

## INFORMAL STATEMENT
lem.jtp.pentagonal-deriv-identity

\leanhelper  We have $xQ'=-QS$, where $Q$ is the pentagonal series and $S$ is the sum-of-divisors generating function.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.jtp.sigmaseries
def.jtp.sigmaSeries

\leanhelper  The \emph{sum-of-divisors generating function} is 

\[  S = \sum _{k>0} \sigma (k)\,  x^k \in \mathbb {Z}[[x]],  \]

 where $\sigma (k) = \sigma _1(k) = \sum _{d\mid k} d$ is the sum of positive divisors of~ $k$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.pars.pent-num
def.pars.pent-num

For any $k\in \mathbb {Z}$, define a nonnegative integer $w_{k}\in \mathbb {N}$ by 

\[  w_{k}=\frac{\left( 3k-1\right) k}{2}.  \]

 This is called the $k$\emph{-th pentagonal number}.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.pent.coeff
def.pent.coeff

\leanhelper  The \emph{pentagonal coefficient} at $n\in \mathbb {N}$ is 

\[  \mathrm{pentagonalCoeff}(n) = \begin{cases}  (-1)^{|k|} &  \text{if } n = w_k \text{ for some } k\in \mathbb {Z}, \\ 0 &  \text{otherwise}. \end{cases}  \]

 This is well-defined by the injectivity of pentagonal numbers (Lemma~ \ref{lem.pent.injective}).

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.pent.pentagonalseries
def.pent.pentagonalSeries

\leanhelper  The \emph{pentagonal series} is the formal power series 

\[  Q = \sum _{n\geq 0} \mathrm{pentagonalCoeff}(n)\,  x^n = \sum _{k\in \mathbb {Z}} (-1)^k x^{w_k} \in R[[x]].  \]

## VERDICT
{
  "verdict": "faithful",
  "justification": "The target states exactly `PowerSeries.X * (PowerSeries.derivative \u2124) ...pentagonalSeries = -...pentagonalSeries * ...sigmaSeries`, matching \u201cWe have $xQ'=-QS$.\u201d There are no added binders or hypotheses. The referenced bodies also match the blueprint definitions: `sigmaSeries` has coefficient `0` at zero and `((ArithmeticFunction.sigma 1) n)` otherwise, while `pentagonalSeries` is built from `pentagonalCoeff`, whose nonzero value is `(-1) ^ k.natAbs`, corresponding to $(-1)^{|k|}$. The finite inverse search enumerates nonnegative indices and indices `-k - 1`, and `pentagonalNumber k = ((3 * k - 1) * k / 2).toNat` implements the stated $w_k=(3k-1)k/2$. Thus the named series and the formal derivative identity have the intended meanings."
}