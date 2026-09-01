## TARGET AlgebraicCombinatorics.FPS.Laurent.BTRep.toFinsupp (def) — ELABORATED SIGNATURE
{n : ℤ} → AlgebraicCombinatorics.FPS.Laurent.BTRep n → AlgebraicCombinatorics.FPS.Laurent.BalancedTernaryRep n

Body:
fun {n} r =>
  { digits := { support := ⋯.toFinset, toFun := fun i => (r.digits i).toInt, mem_support_toFun := ⋯ },
    digits_range := ⋯, sum_eq := ⋯ }

Docstring: Convert a `BTRep` (inductive style from `LaurentSeries.lean`) 
to a `BalancedTernaryRep` (Finsupp style). 

## TARGET AlgebraicCombinatorics.FPS.Laurent.BalancedTernaryRep.toInductive (def) — ELABORATED SIGNATURE
{n : ℤ} → AlgebraicCombinatorics.FPS.Laurent.BalancedTernaryRep n → AlgebraicCombinatorics.FPS.Laurent.BTRep n

Body:
fun {n} r =>
  { digits := fun i => AlgebraicCombinatorics.FPS.Laurent.btDigitOfInt (r.digits i), finite_support := ⋯, sum_eq := ⋯ }

Docstring: Convert a `BalancedTernaryRep` (Finsupp style) to a 
`BTRep` (inductive style from `LaurentSeries.lean`). 

## TARGET AlgebraicCombinatorics.FPS.Laurent.balancedTernary_equiv (def) — ELABORATED SIGNATURE
(n : ℤ) → AlgebraicCombinatorics.FPS.Laurent.BalancedTernaryRep n ≃ AlgebraicCombinatorics.FPS.Laurent.BTRep n

Body:
fun n =>
  { toFun := AlgebraicCombinatorics.FPS.Laurent.BalancedTernaryRep.toInductive,
    invFun := AlgebraicCombinatorics.FPS.Laurent.BTRep.toFinsupp, left_inv := ⋯, right_inv := ⋯ }

Docstring: Type equivalence between the two balanced ternary representations.
This shows the types `BalancedTernaryRep n` and `AlgebraicCombinatorics.BalancedTernaryRepresentation n`
are equivalent (bijective correspondence). 

## PROJECT DEPENDENCY AlgebraicCombinatorics.FPS.Laurent.BTRep (def)
ℤ → Type

Body:
AlgebraicCombinatorics.BalancedTernaryRepresentation

## PROJECT DEPENDENCY AlgebraicCombinatorics.FPS.Laurent.BalancedTernaryRep (inductive)
ℤ → Type

Body:
AlgebraicCombinatorics.FPS.Laurent.BalancedTernaryRep.mk : {n : ℤ} →
  (digits : ℕ →₀ ℤ) →
    (∀ (i : ℕ), digits i ∈ AlgebraicCombinatorics.FPS.Laurent.btDigits) →
      ∑ i ∈ digits.support, digits i * 3 ^ i = n → AlgebraicCombinatorics.FPS.Laurent.BalancedTernaryRep n

Docstring: **Balanced Ternary Representation Definition**.
(Definition def.fps.laure.balanced-tern, label: def.fps.laure.balanced-tern)

A balanced ternary representation of an integer `n` is a finitely supported
function `f : ℕ → ℤ` with values in {-1, 0, 1} such that `n = ∑_i f(i) · 3^i`.

Unlike binary representations (where digits are 0 or 1), balanced ternary
allows digits to be -1, 0, or 1. This enables direct representation of
negative integers without a separate sign. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.FPS.Laurent.BalancedTernaryRep.mk (constructor)
{n : ℤ} →
  (digits : ℕ →₀ ℤ) →
    (∀ (i : ℕ), digits i ∈ AlgebraicCombinatorics.FPS.Laurent.btDigits) →
      ∑ i ∈ digits.support, digits i * 3 ^ i = n → AlgebraicCombinatorics.FPS.Laurent.BalancedTernaryRep n

## PROJECT DEPENDENCY AlgebraicCombinatorics.BalancedTernaryDigit (inductive)
Type

Body:
AlgebraicCombinatorics.BalancedTernaryDigit.negOne : AlgebraicCombinatorics.BalancedTernaryDigit
AlgebraicCombinatorics.BalancedTernaryDigit.zero : AlgebraicCombinatorics.BalancedTernaryDigit
AlgebraicCombinatorics.BalancedTernaryDigit.one : AlgebraicCombinatorics.BalancedTernaryDigit

Docstring: The set of balanced ternary digits: {-1, 0, 1} 

## PROJECT DEPENDENCY AlgebraicCombinatorics.BalancedTernaryRepresentation.digits (def)
{n : ℤ} → AlgebraicCombinatorics.BalancedTernaryRepresentation n → ℕ → AlgebraicCombinatorics.BalancedTernaryDigit

Body:
fun n self => self.1

Docstring: The sequence of digits 

## PROJECT DEPENDENCY AlgebraicCombinatorics.BalancedTernaryDigit.instZero (def)
Zero AlgebraicCombinatorics.BalancedTernaryDigit

Body:
{ zero := AlgebraicCombinatorics.BalancedTernaryDigit.zero }

## PROJECT DEPENDENCY AlgebraicCombinatorics.BalancedTernaryRepresentation.finite_support (theorem)
∀ {n : ℤ} (self : AlgebraicCombinatorics.BalancedTernaryRepresentation n), {i | self.digits i ≠ 0}.Finite

Docstring: Only finitely many digits are nonzero 

## PROJECT DEPENDENCY AlgebraicCombinatorics.BalancedTernaryDigit.toInt (def)
AlgebraicCombinatorics.BalancedTernaryDigit → ℤ

Body:
fun x =>
  match x with
  | AlgebraicCombinatorics.BalancedTernaryDigit.negOne => -1
  | AlgebraicCombinatorics.BalancedTernaryDigit.zero => 0
  | AlgebraicCombinatorics.BalancedTernaryDigit.one => 1

Docstring: Convert a balanced ternary digit to an integer 

## PROJECT DEPENDENCY AlgebraicCombinatorics.BalancedTernaryRepresentation.mk (constructor)
{n : ℤ} →
  (digits : ℕ → AlgebraicCombinatorics.BalancedTernaryDigit) →
    {i | digits i ≠ 0}.Finite →
      ∑ᶠ (i : ℕ), (digits i).toInt * 3 ^ i = n → AlgebraicCombinatorics.BalancedTernaryRepresentation n

## PROJECT DEPENDENCY AlgebraicCombinatorics.FPS.Laurent.btDigitOfInt (def)
ℤ → AlgebraicCombinatorics.FPS.Laurent.BTDigit

Body:
fun z =>
  if z = -1 then AlgebraicCombinatorics.BalancedTernaryDigit.negOne
  else
    if z = 0 then AlgebraicCombinatorics.BalancedTernaryDigit.zero else AlgebraicCombinatorics.BalancedTernaryDigit.one

Docstring: Convert an integer in `btDigits` to a `BalancedTernaryDigit`. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.FPS.Laurent.BalancedTernaryRep.digits (def)
{n : ℤ} → AlgebraicCombinatorics.FPS.Laurent.BalancedTernaryRep n → ℕ →₀ ℤ

Body:
fun n self => self.1

Docstring: The digit function 

## PROJECT DEPENDENCY AlgebraicCombinatorics.BalancedTernaryRepresentation (inductive)
ℤ → Type

Body:
AlgebraicCombinatorics.BalancedTernaryRepresentation.mk : {n : ℤ} →
  (digits : ℕ → AlgebraicCombinatorics.BalancedTernaryDigit) →
    {i | digits i ≠ 0}.Finite →
      ∑ᶠ (i : ℕ), (digits i).toInt * 3 ^ i = n → AlgebraicCombinatorics.BalancedTernaryRepresentation n

Docstring: A balanced ternary representation of an integer `n` is an essentially finite
sequence `(b_i)_{i ∈ ℕ}` of elements in `{-1, 0, 1}` such that `n = ∑ b_i * 3^i`.

This corresponds to the Definition of balanced ternary representation in `sec.gf.laure`.


## PROJECT DEPENDENCY AlgebraicCombinatorics.FPS.Laurent.btDigits (def)
Finset ℤ

Body:
{-1, 0, 1}

Docstring: The set of balanced ternary digits {-1, 0, 1}. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.BalancedTernaryDigit.zero (constructor)
AlgebraicCombinatorics.BalancedTernaryDigit

## PROJECT DEPENDENCY AlgebraicCombinatorics.instReprBalancedTernaryDigit.repr (def)
AlgebraicCombinatorics.BalancedTernaryDigit → ℕ → Format

Body:
fun x prec =>
  match x with
  | AlgebraicCombinatorics.BalancedTernaryDigit.negOne =>
    Repr.addAppParen
      (Format.nest (if prec ≥ 1024 then 1 else 2)
          (Std.Format.text "AlgebraicCombinatorics.BalancedTernaryDigit.negOne")).group
      prec
  | AlgebraicCombinatorics.BalancedTernaryDigit.zero =>
    Repr.addAppParen
      (Format.nest (if prec ≥ 1024 then 1 else 2)
          (Std.Format.text "AlgebraicCombinatorics.BalancedTernaryDigit.zero")).group
      prec
  | AlgebraicCombinatorics.BalancedTernaryDigit.one =>
    Repr.addAppParen
      (Format.nest (if prec ≥ 1024 then 1 else 2)
          (Std.Format.text "AlgebraicCombinatorics.BalancedTernaryDigit.one")).group
      prec

## PROJECT DEPENDENCY AlgebraicCombinatorics.FPS.Laurent.BTDigit (def)
Type

Body:
AlgebraicCombinatorics.BalancedTernaryDigit

## PROJECT DEPENDENCY AlgebraicCombinatorics.BalancedTernaryDigit.negOne (constructor)
AlgebraicCombinatorics.BalancedTernaryDigit

## PROJECT DEPENDENCY AlgebraicCombinatorics.BalancedTernaryDigit.one (constructor)
AlgebraicCombinatorics.BalancedTernaryDigit

## BASE-LIBRARY REF Int
Type

Docstring: The integers.

This type is special-cased by the compiler and overridden with an efficient implementation. The
runtime has a special representation for `Int` that stores “small” signed numbers directly, while
larger numbers use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)). A “small number” is an integer that can be encoded with one fewer bits
than the platform's pointer size (i.e. 63 bits on 64-bit architectures and 31 bits on 32-bit
architectures).


## BASE-LIBRARY REF Finsupp.mk
{α : Type u_9} →
  {M : Type u_10} →
    [inst : Zero M] → (support : Finset α) → (toFun : α → M) → (∀ (a : α), a ∈ support ↔ toFun a ≠ 0) → α →₀ M

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


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

## BASE-LIBRARY REF NonUnitalNormedCommRing.toNonUnitalCommRing
{α : Type u_5} → [self : NonUnitalNormedCommRing α] → NonUnitalCommRing α

## BASE-LIBRARY REF NormedCommRing.toNonUnitalNormedCommRing
{α : Type u_2} → [β : NormedCommRing α] → NonUnitalNormedCommRing α

Docstring: A normed commutative ring is a non-unital normed commutative ring. 

## BASE-LIBRARY REF Int.instNormedCommRing
NormedCommRing ℤ

## BASE-LIBRARY REF Set.Finite.toFinset
{α : Type u} → {s : Set α} → s.Finite → Finset α

Docstring: Using choice, get the `Finset` that represents this `Set`. 

## BASE-LIBRARY REF setOf
{α : Type u} → (α → Prop) → Set α

Docstring: Turn a predicate `p : α → Prop` into a set, also written as `{x | p x}` 

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

## BASE-LIBRARY REF Zero.toOfNat0
{α : Type u_1} → [Zero α] → OfNat α 0

## BASE-LIBRARY REF DFunLike.coe
{F : Sort u_1} → {α : outParam (Sort u_2)} → {β : outParam (α → Sort u_3)} → [self : DFunLike F α β] → F → (a : α) → β a

Docstring: The coercion from `F` to a function. 

## BASE-LIBRARY REF Finsupp
Type u_9 → (M : Type u_10) → [Zero M] → Type (max u_10 u_9)

Docstring: `Finsupp α M`, denoted `α →₀ M`, is the type of functions `f : α → M` such that
`f x = 0` for all but finitely many `x`. 

## BASE-LIBRARY REF Finsupp.instFunLike
{α : Type u_1} → {M : Type u_4} → [inst : Zero M] → FunLike (α →₀ M) α M

## BASE-LIBRARY REF Equiv
Sort u_1 → Sort u_2 → Sort (max (max 1 u_1) u_2)

Docstring: `α ≃ β` is the type of functions from `α → β` with a two-sided inverse. 

## BASE-LIBRARY REF Equiv.mk
{α : Sort u_1} →
  {β : Sort u_2} →
    (toFun : α → β) →
      (invFun : β → α) →
        autoParam (Function.LeftInverse invFun toFun) Equiv.left_inv._autoParam →
          autoParam (Function.RightInverse invFun toFun) Equiv.right_inv._autoParam → α ≃ β

## BASE-LIBRARY REF Membership.mem
{α : outParam (Type u)} → {γ : Type v} → [self : Membership α γ] → γ → α → Prop

Docstring: The membership relation `a ∈ s : Prop` where `a : α`, `s : γ`. 

Conventions for notations in identifiers:

 * The recommended spelling of `∈` in identifiers is `mem`.

## BASE-LIBRARY REF Finset
Type u_4 → Type u_4

Docstring: `Finset α` is the type of finite sets of elements of `α`. It is implemented
as a multiset (a list up to permutation) which has no duplicate elements. 

## BASE-LIBRARY REF Finset.instMembership
{α : Type u_1} → Membership α (Finset α)

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

## BASE-LIBRARY REF Finset.sum
{ι : Type u_1} → {M : Type u_3} → [AddCommMonoid M] → Finset ι → (ι → M) → M

Docstring: `∑ x ∈ s, f x` is the sum of `f x` as `x` ranges over the elements
of the finite set `s`.

When the index type is a `Fintype`, the notation `∑ x, f x`, is a shorthand for
`∑ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF Int.instAddCommMonoid
AddCommMonoid ℤ

## BASE-LIBRARY REF Finsupp.support
{α : Type u_9} → {M : Type u_10} → [inst : Zero M] → (α →₀ M) → Finset α

Docstring: The support of a finitely supported function (aka `Finsupp`). 

## BASE-LIBRARY REF HMul.hMul
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HMul α β γ] → α → β → γ

Docstring: `a * b` computes the product of `a` and `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `*` in identifiers is `mul`.

## BASE-LIBRARY REF instHMul
{α : Type u_1} → [Mul α] → HMul α α α

## BASE-LIBRARY REF Int.instMul
Mul ℤ

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

## BASE-LIBRARY REF instOfNat
{n : ℕ} → OfNat ℤ n

## BASE-LIBRARY REF Zero
Type u → Type u

Docstring: A type with a zero element. 

## BASE-LIBRARY REF Zero.mk
{α : Type u} → α → Zero α

## BASE-LIBRARY REF Set.Finite
{α : Type u} → Set α → Prop

Docstring: A set is finite if the corresponding `Subtype` is finite,
i.e., if there exists a natural `n : ℕ` and an equivalence `s ≃ Fin n`. 

## BASE-LIBRARY REF Unit
Type

Docstring: The canonical type with one element. This element is written `()`.

`Unit` has a number of uses:
* It can be used to model control flow that returns from a function call without providing other
  information.
* Monadic actions that return `Unit` have side effects without computing values.
* In polymorphic types, it can be used to indicate that no data is to be stored in a particular
  field.


## BASE-LIBRARY REF Neg.neg
{α : Type u} → [self : Neg α] → α → α

Docstring: `-a` computes the negative or opposite of `a`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `-` in identifiers is `neg` (when used as a unary operator).

## BASE-LIBRARY REF Int.instNegInt
Neg ℤ

## BASE-LIBRARY REF finsum
{M : Type u_7} → {α : Sort u_8} → [AddCommMonoid M] → (α → M) → M

Docstring: Sum of `f x` as `x` ranges over the elements of the support of `f`, if it's finite. Zero
otherwise. 

## BASE-LIBRARY REF ite
{α : Sort u} → (c : Prop) → [h : Decidable c] → α → α → α

Docstring: `if c then t else e` is notation for `ite c t e`, "if-then-else", which decides to
return `t` or `e` depending on whether `c` is true or false. The explicit argument
`c : Prop` does not have any actual computational content, but there is an additional
`[Decidable c]` argument synthesized by typeclass inference which actually
determines how to evaluate `c` to true or false. Write `if h : c then t else e`
instead for a "dependent if-then-else" `dite`, which allows `t`/`e` to use the fact
that `c` is true/false.


## BASE-LIBRARY REF Int.instDecidableEq
DecidableEq ℤ

Docstring: Decides whether two integers are equal. Usually accessed via the `DecidableEq Int` instance.

This function is overridden by the compiler with an efficient implementation. This definition is the
logical model.

Examples:
* `show (7 : Int) = (3 : Int) + (4 : Int) by decide`
* `if (6 : Int) = (3 : Int) * (2 : Int) then "yes" else "no" = "yes"`
* `(¬ (6 : Int) = (3 : Int)) = true`


## BASE-LIBRARY REF Insert.insert
{α : outParam (Type u)} → {γ : Type v} → [self : Insert α γ] → α → γ → γ

Docstring: `insert x xs` inserts the element `x` into the collection `xs`. 

## BASE-LIBRARY REF Finset.instInsert
{α : Type u_1} → [DecidableEq α] → Insert α (Finset α)

Docstring: `insert a s` is the set `{a} ∪ s` containing `a` and the elements of `s`. 

## BASE-LIBRARY REF Singleton.singleton
{α : outParam (Type u)} → {β : Type v} → [self : Singleton α β] → α → β

Docstring: `singleton x` is a collection with the single element `x` (notation: `{x}`). 

Conventions for notations in identifiers:

 * The recommended spelling of `{x}` in identifiers is `singleton`.

## BASE-LIBRARY REF Finset.instSingleton
{α : Type u_1} → Singleton α (Finset α)

Docstring: `{a} : Finset a` is the set `{a}` containing `a` and nothing else.

This differs from `insert a ∅` in that it does not require a `DecidableEq` instance for `α`.


## BASE-LIBRARY REF Std.Format
Type

Docstring: A representation of a set of strings, in which the placement of newlines and indentation differ.

Given a specific line width, specified in columns, the string that uses the fewest lines can be
selected.

The pretty-printing algorithm is based on Wadler's paper
[_A Prettier Printer_](https://homepages.inf.ed.ac.uk/wadler/papers/prettier/prettier.pdf).


## BASE-LIBRARY REF Repr.addAppParen
Format → ℕ → Format

Docstring: Adds parentheses to `f` if the precedence `prec` from the context is at least that of function
application.

Together with `reprArg`, this can be used to correctly parenthesize function application
syntax.


## BASE-LIBRARY REF Std.Format.group
Format → optParam Std.Format.FlattenBehavior Std.Format.FlattenBehavior.allOrNone → Format

Docstring: Creates a new flattening group for the given inner `Format`.  

## BASE-LIBRARY REF Std.Format.nest
ℤ → Format → Format

Docstring: `nest indent f` increases the current indentation level by `indent` while rendering `f`.

Example:
```lean example
open Std Format in
def fmtList (l : List Format) : Format :=
  let f := joinSep l  (", " ++ Format.line)
  group (nest 1 <| "[" ++ f ++ "]")
```

This will be written all on one line, but if the text is too large, the formatter will put in
linebreaks after the commas and indent later lines by 1.


## BASE-LIBRARY REF GE.ge
{α : Type u} → [LE α] → α → α → Prop

Docstring: `a ≥ b` is an abbreviation for `b ≤ a`. 

Conventions for notations in identifiers:

 * The recommended spelling of `≥` in identifiers is `ge`.

 * The recommended spelling of `>=` in identifiers is `ge` (prefer `≥` over `>=`).

## BASE-LIBRARY REF instLENat
LE ℕ

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

## BASE-LIBRARY REF Nat.decLe
(n m : ℕ) → Decidable (n ≤ m)

Docstring: A decision procedure for non-strict inequality of natural numbers, usually accessed via the
`DecidableLE Nat` instance.

Examples:
 * `(if 3 ≤ 4 then "yes" else "no") = "yes"`
 * `(if 6 ≤ 4 then "yes" else "no") = "no"`
 * `show 12 ≤ 12 by decide`
 * `show 5 ≤ 12 by decide`


## BASE-LIBRARY REF Std.Format.text
String → Format

Docstring: A node containing a plain string.

If the string contains newlines, the formatter emits them and then indents to the current level.


## BASE-LIBRARY REF Std.Format.FlattenBehavior.allOrNone
Std.Format.FlattenBehavior

Docstring: Either all `Format.line`s in the group will be newlines, or all of them will be spaces.


## INFORMAL STATEMENT
Equivalence between the two balanced ternary representations

\leanhelper  The two formulations of balanced ternary representations (the finitely-supported-function formulation and the digit-sequence formulation) are equivalent: for each $n \in \mathbb {Z}$, the two types of balanced ternary representations of $n$ are in bijection. The conversions are mutual inverses (up to the digit representation).

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.infprod.essfinite
def.fps.infprod.essFinite

\leanhelper  A family $(k_i)_{i \in I}$ of natural numbers is \emph{essentially finite} if all but finitely many entries equal $0$, i.e., the set $\{ i \in I : k_i \neq 0\} $ is finite. This corresponds to $S^I_{\mathrm{fin}}$ in the source.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.infprod.sfini
def.fps.infprod.SfinI

\leanhelper  The set $S^I_{\mathrm{fin}}$ of \emph{essentially finite families} in $\prod _{i \in I} S_i$ is the set of all families $(k_i)_{i \in I}$ such that $k_i \in S_i$ for all $i$ and the family $(k_i)$ is essentially finite.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.laure.balanced-tern
def.fps.laure.balanced-tern

\leanhelper  A \emph{balanced ternary representation} of an integer $n$ means an essentially finite sequence $\left( b_{i}\right) _{i\in \mathbb {N}}=\left( b_{0},b_{1},b_{2},\ldots \right) \in \left\{  0,1,-1\right\}  ^{\mathbb {N}}$ such that

\[  n=\sum _{i\in \mathbb {N}}b_{i}3^{i}.  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.laure.binary-rep
def.fps.laure.binary-rep

\leanhelper  A \emph{binary representation} of an integer $n$ means an essentially finite sequence $\left( b_{i}\right) _{i\in \mathbb {N}}=\left( b_{0},b_{1},b_{2},\ldots \right) \in \left\{  0,1\right\}  ^{\mathbb {N}}$ such that

\[  n=\sum _{i\in \mathbb {N}}b_{i}2^{i}.  \]

 (Recall that “essentially finite” means “all but finitely many $i\in \mathbb {N}$ satisfy $b_{i}=0$”.)

## VERDICT
{
  "verdict": "faithful",
  "justification": "The blueprint says that \u201cfor each n \u2208 \u2124, the two types of balanced ternary representations of n are in bijection\u201d and that the conversions are mutual inverses. The declaration `balancedTernary_equiv` has exactly the corresponding binder and conclusion: `(n : \u2124) \u2192 BalancedTernaryRep n \u2243 BTRep n`; by the supplied `Equiv` definition, this contains functions with two-sided inverse proofs. Its `toFun` and `invFun` are precisely the supplied conversions `BalancedTernaryRep.toInductive` and `BTRep.toFinsupp`. The two representation types also match the stated formulations: `BalancedTernaryRep` uses `digits : \u2115 \u2192\u2080 \u2124`, requires every digit to lie in `btDigits = {-1, 0, 1}`, and requires `\u2211 i \u2208 digits.support, digits i * 3 ^ i = n`; `BTRep`, definitionally `BalancedTernaryRepresentation`, uses a sequence `\u2115 \u2192 BalancedTernaryDigit`, finite nonzero support, and the corresponding finitely supported sum equal to `n`. Reversing the displayed equality from the informal `n = \u2211 ...` is immaterial. There are no added hypotheses or narrowed quantifiers."
}