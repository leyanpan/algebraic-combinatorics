## TARGET AlgebraicCombinatorics.pentagonalSeries (def) — ELABORATED SIGNATURE
{R : Type u_1} → [CommRing R] → PowerSeries R

Body:
fun {R} [CommRing R] => PowerSeries.mk fun n => ↑(AlgebraicCombinatorics.pentagonalCoeff n)

Docstring: The alternating sum ∑_{k∈ℤ} (-1)^k x^{w_k} as a formal power series.
This is well-defined because the pentagonal numbers grow quadratically.

We define the coefficient at n to be (-1)^k if n = w_k for some k, and 0 otherwise.
Since pentagonal numbers are injective, this is well-defined. 

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

## BASE-LIBRARY REF CommRing
Type u → Type u

Docstring: A commutative ring is a ring with commutative multiplication. 

## BASE-LIBRARY REF PowerSeries
Type u_1 → Type (max u_1 0)

Body:
fun R => MvPowerSeries Unit R

Docstring: Formal power series over a coefficient type `R` 

## BASE-LIBRARY REF AddGroupWithOne
Type u → Type u

Docstring: An `AddGroupWithOne` is an `AddGroup` with a 1. It also contains data for the unique
homomorphisms `ℕ → R` and `ℤ → R`. 

## BASE-LIBRARY REF Ring
Type u → Type u

Docstring: A `Ring` is a `Semiring` with negation making it an additive group. 

## BASE-LIBRARY REF Option
Type u → Type u

Docstring: Optional values, which are either `some` around a value from the underlying type or `none`.

`Option` can represent nullable types or computations that might fail. In the codomain of a function
type, it can also represent partiality.


## BASE-LIBRARY REF Pow
Type u → Type v → Type (max u v)

Docstring: The homogeneous version of `HPow`: `a ^ b : α` where `a : α`, `b : β`.
(The right argument is not the same as the left since we often want this even
in the homogeneous case.)

Types can choose to subscribe to particular defaulting behavior by providing
an instance to either `NatPow` or `HomogeneousPow`:
- `NatPow` is for types whose exponents is preferentially a `Nat`.
- `HomogeneousPow` is for types whose base and exponent are preferentially the same.


## BASE-LIBRARY REF Pow.pow
{α : Type u} → {β : Type v} → [self : Pow α β] → α → β → α

Body:
fun α β [self : Pow α β] => self.1

Docstring: `a ^ b` computes `a` to the power of `b`. See `HPow`. 

## BASE-LIBRARY REF Monoid
Type u → Type u

Docstring: A `Monoid` is a `Semigroup` with an element `1` such that `1 * a = a * 1 = a`. 

## BASE-LIBRARY REF Int.instMonoid
Monoid ℤ

Body:
inferInstance

## BASE-LIBRARY REF Int.instCommMonoid
CommMonoid ℤ

Body:
{ toMul := Int.instMul, mul_assoc := Int.mul_assoc, toOne := One.ofOfNat1, one_mul := Int.one_mul,
  mul_one := Int.mul_one, npow := fun n x => x ^ n, npow_zero := ⋯, npow_succ := ⋯, mul_comm := Int.mul_comm }

## BASE-LIBRARY REF Neg.neg
{α : Type u} → [self : Neg α] → α → α

Body:
fun α [self : Neg α] => self.1

Docstring: `-a` computes the negative or opposite of `a`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `-` in identifiers is `neg` (when used as a unary operator).

## BASE-LIBRARY REF Int.instNegInt
Neg ℤ

Body:
{ neg := Int.neg }

## BASE-LIBRARY REF Int.neg
ℤ → ℤ

Body:
fun n =>
  match n with
  | Int.ofNat n => Int.negOfNat n
  | Int.negSucc n => ↑n.succ

Docstring: Negation of integers, usually accessed via the `-` prefix operator.

This function is overridden by the compiler with an efficient implementation. This definition is
the logical model.

Examples:
 * `-(6 : Int) = -6`
 * `-(-6 : Int) = 6`
 * `(12 : Int).neg = -12`


## BASE-LIBRARY REF Int.ofNat
ℕ → ℤ

Docstring: A natural number is an integer.

This constructor covers the non-negative integers (from `0` to `∞`).


## BASE-LIBRARY REF Int.natAbs
ℤ → ℕ

Body:
fun m =>
  match m with
  | Int.ofNat m => m
  | Int.negSucc m => m.succ

Docstring: The absolute value of an integer is its distance from `0`.

This function is overridden by the compiler with an efficient implementation. This definition is
the logical model.

Examples:
 * `(7 : Int).natAbs = 7`
 * `(0 : Int).natAbs = 0`
 * `(-11 : Int).natAbs = 11`


## BASE-LIBRARY REF Add
Type u → Type u

Docstring: The homogeneous version of `HAdd`: `a + b : α` where `a b : α`. 

## BASE-LIBRARY REF Add.add
{α : Type u} → [self : Add α] → α → α → α

Body:
fun α [self : Add α] => self.1

Docstring: `a + b` computes the sum of `a` and `b`. See `HAdd`. 

## BASE-LIBRARY REF Nat.add
ℕ → ℕ → ℕ

Body:
fun x x_1 =>
  Nat.brecOn (motive := fun x => ℕ → ℕ) x_1
    (fun x f x_2 =>
      (match (motive := ℕ → (x : ℕ) → Nat.below (motive := fun x => ℕ → ℕ) x → ℕ) x_2, x with
        | a, Nat.zero => fun x => a
        | a, b.succ => fun x => (x.1 a).succ)
        f)
    x

Docstring: Addition of natural numbers, typically used via the `+` operator.

This function is overridden in both the kernel and the compiler to efficiently evaluate using the
arbitrary-precision arithmetic library. The definition provided here is the logical model.


## BASE-LIBRARY REF List.find?
{α : Type u} → (α → Bool) → List α → Option α

Body:
fun {α} p x =>
  List.brecOn x fun x f =>
    (match (motive := (x : List α) → List.below x → Option α) x with
      | [] => fun x => none
      | a :: as => fun x =>
        match p a with
        | true => some a
        | false => x.1)
      f

Docstring: Returns the first element of the list for which the predicate `p` returns `true`, or `none` if no
such element is found.

`O(|l|)`.

Examples:
* `[7, 6, 5, 8, 1, 2, 6].find? (· < 5) = some 1`
* `[7, 6, 5, 8, 1, 2, 6].find? (· < 1) = none`


## BASE-LIBRARY REF Decidable.decide
(p : Prop) → [h : Decidable p] → Bool

Body:
fun p [h : Decidable p] => Decidable.casesOn h (fun x => false) fun x => true

Docstring: Converts a decidable proposition into a `Bool`.

If `p : Prop` is decidable, then `decide p : Bool` is the Boolean value
that is `true` if `p` is true and `false` if `p` is false.


## BASE-LIBRARY REF Nat.decEq
(n m : ℕ) → Decidable (n = m)

Body:
fun n m =>
  match h : n.beq m with
  | true => isTrue ⋯
  | false => isFalse ⋯

Docstring: A decision procedure for equality of natural numbers, usually accessed via the `DecidableEq Nat`
instance.

This function is overridden in both the kernel and the compiler to efficiently evaluate using the
arbitrary-precision arithmetic library. The definition provided here is the logical model.

Examples:
 * `Nat.decEq 5 5 = isTrue rfl`
 * `(if 3 = 4 then "yes" else "no") = "no"`
 * `show 12 = 12 by decide`


## BASE-LIBRARY REF Bind.bind
{m : Type u → Type v} → [self : Bind m] → {α β : Type u} → m α → (α → m β) → m β

Body:
fun m [self : Bind m] => self.1

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


## BASE-LIBRARY REF Monad
(Type u → Type v) → Type (max (u + 1) v)

Docstring: [Monads](https://en.wikipedia.org/wiki/Monad_(functional_programming)) are an abstraction of
sequential control flow and side effects used in functional programming. Monads allow both
sequencing of effects and data-dependent effects: the values that result from an early step may
influence the effects carried out in a later step.

The `Monad` API may be used directly. However, it is most commonly accessed through
[`do`-notation](https://lean-lang.org/doc/reference/4.28.0/find/?domain=Verso.Genre.Manual.section&name=do-notation).

Most `Monad` instances provide implementations of `pure` and `bind`, and use default implementations
for the other methods inherited from `Applicative`. Monads should satisfy certain laws, but
instances are not required to prove this. An instance of `LawfulMonad` expresses that a given
monad's operations are lawful.


## BASE-LIBRARY REF List.instMonad
Monad List

Body:
{ map := fun {α β} f l => List.map f l, pure := fun {α} x => [x],
  seq := fun {α β} f x => (fun {α β} l f => List.flatMap f l) f fun y => (fun {α β} f l => List.map f l) y (x ()),
  seqLeft := fun {α β} x y =>
    (fun {α β} l f => List.flatMap f l) x fun a =>
      (fun {α β} l f => List.flatMap f l) (y ()) fun x => (fun {α} x => [x]) a,
  seqRight := fun {α β} x y => (fun {α β} l f => List.flatMap f l) x fun x => y (),
  bind := fun {α β} l f => List.flatMap f l }

## BASE-LIBRARY REF List.map
{α : Type u_1} → {β : Type u_2} → (α → β) → List α → List β

Body:
fun {α} {β} f x =>
  List.brecOn x fun x f_1 =>
    (match (motive := (x : List α) → List.below x → List β) x with
      | [] => fun x => []
      | a :: as => fun x => f a :: x.1)
      f_1

Docstring: Applies a function to each element of the list, returning the resulting list of values.

`O(|l|)`.

Examples:
* `[a, b, c].map f = [f a, f b, f c]`
* `[].map Nat.succ = []`
* `["one", "two", "three"].map (·.length) = [3, 3, 5]`
* `["one", "two", "three"].map (·.reverse) = ["eno", "owt", "eerht"]`


## BASE-LIBRARY REF Function.comp
{α : Sort u} → {β : Sort v} → {δ : Sort w} → (β → δ) → (α → β) → α → δ

Body:
fun {α} {β} {δ} f g x => f (g x)

Docstring: Function composition, usually written with the infix operator `∘`. A new function is created from
two existing functions, where one function's output is used as input to the other.

Examples:
 * `Function.comp List.reverse (List.drop 2) [3, 2, 4, 1] = [1, 4]`
 * `(List.reverse ∘ List.drop 2) [3, 2, 4, 1] = [1, 4]`


Conventions for notations in identifiers:

 * The recommended spelling of `∘` in identifiers is `comp`.

## BASE-LIBRARY REF Function.const
{α : Sort u} → (β : Sort v) → α → β → α

Body:
fun {α} β a x => a

Docstring: The constant function that ignores its argument.

If `a : α`, then `Function.const β a : β → α` is the “constant function with value `a`”. For all
arguments `b : β`, `Function.const β a b = a`.

Examples:
 * `Function.const Bool 10 true = 10`
 * `Function.const Bool 10 false = 10`
 * `Function.const String 10 "any string" = 10`


## BASE-LIBRARY REF List.cons
{α : Type u} → α → List α → List α

Docstring: The list whose first element is `head`, where `tail` is the rest of the list.
Usually written `head :: tail`.


Conventions for notations in identifiers:

 * The recommended spelling of `::` in identifiers is `cons`.

 * The recommended spelling of `[a]` in identifiers is `singleton`.

## BASE-LIBRARY REF List.nil
{α : Type u} → List α

Docstring: The empty list, usually written `[]`. 

Conventions for notations in identifiers:

 * The recommended spelling of `[]` in identifiers is `nil`.

## BASE-LIBRARY REF List.flatMap
{α : Type u} → {β : Type v} → (α → List β) → List α → List β

Body:
fun {α} {β} b as => (List.map b as).flatten

Docstring: Applies a function that returns a list to each element of a list, and concatenates the resulting
lists.

Examples:
* `[2, 3, 2].flatMap List.range = [0, 1, 0, 1, 2, 0, 1]`
* `["red", "blue"].flatMap String.toList = ['r', 'e', 'd', 'b', 'l', 'u', 'e']`


## BASE-LIBRARY REF Unit.unit
Unit

Body:
PUnit.unit

Docstring: The only element of the unit type.

It can be written as an empty tuple: `()`.


## BASE-LIBRARY REF List.range
ℕ → List ℕ

Body:
fun n => List.range.loop n []

Docstring: Returns a list of the numbers from `0` to `n` exclusive, in increasing order.

`O(n)`.

Examples:
* `range 5 = [0, 1, 2, 3, 4]`
* `range 0 = []`
* `range 2 = [0, 1]`


## BASE-LIBRARY REF Pure.pure
{f : Type u → Type v} → [self : Pure f] → {α : Type u} → α → f α

Body:
fun f [self : Pure f] => self.1

Docstring: Given `a : α`, then `pure a : f α` represents an action that does nothing and returns `a`.

Examples:
* `(pure "hello" : Option String) = some "hello"`
* `(pure "hello" : Except (Array String) String) = Except.ok "hello"`
* `(pure "hello" : StateM Nat String).run 105 = ("hello", 105)`


## BASE-LIBRARY REF Applicative
(Type u → Type v) → Type (max (u + 1) v)

Docstring: An [applicative functor](https://lean-lang.org/doc/reference/4.28.0/find/?domain=Verso.Genre.Manual.section&name=monads-and-do) is more powerful than a `Functor`, but
less powerful than a `Monad`.

Applicative functors capture sequencing of effects with the `<*>` operator, overloaded as `seq`, but
not data-dependent effects. The results of earlier computations cannot be used to control later
effects.

Applicative functors should satisfy four laws. Instances of `Applicative` are not required to prove
that they satisfy these laws, which are part of the `LawfulApplicative` class.


## BASE-LIBRARY REF Option.some
{α : Type u} → α → Option α

Docstring: Some value of type `α`. 

## BASE-LIBRARY REF Sub
Type u → Type u

Docstring: The homogeneous version of `HSub`: `a - b : α` where `a b : α`. 

## BASE-LIBRARY REF Sub.sub
{α : Type u} → [self : Sub α] → α → α → α

Body:
fun α [self : Sub α] => self.1

Docstring: `a - b` computes the difference of `a` and `b`. See `HSub`. 

## BASE-LIBRARY REF Int.instSub
Sub ℤ

Body:
{ sub := Int.sub }

## BASE-LIBRARY REF Int.sub
ℤ → ℤ → ℤ

Body:
fun m n => m + -n

Docstring: Subtraction of integers, usually accessed via the `-` operator.

This function is overridden by the compiler with an efficient implementation. This definition is
the logical model.

Examples:
* `(63 : Int) - (6 : Int) = 57`
* `(7 : Int) - (0 : Int) = 7`
* `(0 : Int) - (7 : Int) = -7`


## BASE-LIBRARY REF Option.none
{α : Type u} → Option α

Docstring: No value. 

## BASE-LIBRARY REF Int.toNat
ℤ → ℕ

Body:
fun x =>
  match x with
  | Int.ofNat n => n
  | Int.negSucc a => 0

Docstring: Converts an integer into a natural number. Negative numbers are converted to `0`.

Examples:
* `(7 : Int).toNat = 7`
* `(0 : Int).toNat = 0`
* `(-7 : Int).toNat = 0`


Characterization: `Int.toNat n = n` for `n ≥ 0` and `0` for `n < 0` (truncation).

## BASE-LIBRARY REF Div
Type u → Type u

Docstring: The homogeneous version of `HDiv`: `a / b : α` where `a b : α`. 

## BASE-LIBRARY REF Div.div
{α : Type u} → [self : Div α] → α → α → α

Body:
fun α [self : Div α] => self.1

Docstring: `a / b` computes the result of dividing `a` by `b`. See `HDiv`. 

## BASE-LIBRARY REF Int.instDiv
Div ℤ

Body:
{ div := Int.ediv }

Docstring: The `Div Int` and `Mod Int` instances use `Int.ediv` and `Int.emod` for compatibility with SMT-LIB and
because mathematical reasoning tends to be easier.


## BASE-LIBRARY REF Mul
Type u → Type u

Docstring: The homogeneous version of `HMul`: `a * b : α` where `a b : α`. 

## BASE-LIBRARY REF Mul.mul
{α : Type u} → [self : Mul α] → α → α → α

Body:
fun α [self : Mul α] => self.1

Docstring: `a * b` computes the product of `a` and `b`. See `HMul`. 

## BASE-LIBRARY REF Int.instMul
Mul ℤ

Body:
{ mul := Int.mul }

## BASE-LIBRARY REF Int.mul
ℤ → ℤ → ℤ

Body:
fun m n =>
  match m, n with
  | Int.ofNat m, Int.ofNat n => Int.ofNat (m * n)
  | Int.ofNat m, Int.negSucc n => Int.negOfNat (m * n.succ)
  | Int.negSucc m, Int.ofNat n => Int.negOfNat (m.succ * n)
  | Int.negSucc m, Int.negSucc n => Int.ofNat (m.succ * n.succ)

Docstring: Multiplication of integers, usually accessed via the `*` operator.

This function is overridden by the compiler with an efficient implementation. This definition is
the logical model.

Examples:
 * `(63 : Int) * (6 : Int) = 378`
 * `(6 : Int) * (-6 : Int) = -36`
 * `(7 : Int) * (0 : Int) = 0`


## INFORMAL STATEMENT
def.pent.pentagonalSeries

\leanhelper  The \emph{pentagonal series} is the formal power series 

\[  Q = \sum _{n\geq 0} \mathrm{pentagonalCoeff}(n)\,  x^n = \sum _{k\in \mathbb {Z}} (-1)^k x^{w_k} \in R[[x]].  \]

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

## VERDICT
{
  "verdict": "faithful",
  "discrepancies": [],
  "justification": "The target is exactly the coefficientwise formal power series `PowerSeries.mk fun n => \u2191(pentagonalCoeff n)`, matching `Q = \u2211_{n\u22650} pentagonalCoeff(n) x^n`. After unfolding, `pentagonalCoeff n` returns `(-1) ^ k.natAbs` when `pentagonalNumberInverse n = some k` and `0` otherwise, matching the informal coefficient definition `(-1)^{|k|}` or `0`. The inverse searches all nonnegative candidates `k < n+1` and all negative candidates `-k-1` with `k < n+1`; any solution of `w_k=n` lies in these ranges, so this finite search implements the informal existential condition. Finally, `pentagonalNumber k = ((3*k-1)*k/2).toNat` agrees with the stated natural number `w_k=((3k-1)k)/2`, since that quotient is always a nonnegative integer. The `[CommRing R]` binder supplies the formal coefficient setting and the cast of integer coefficients into `R`; it does not alter the represented series."
}