## TARGET AlgebraicCombinatorics.FPS.Laurent.kBounded_unique (theorem) — ELABORATED SIGNATURE
∀ (k : ℕ),
  ∀ n ∈ AlgebraicCombinatorics.FPS.Laurent.Icc_symm (AlgebraicCombinatorics.FPS.Laurent.maxBT k),
    ∃! f,
      f ∈ AlgebraicCombinatorics.FPS.Laurent.kBoundedBTReps k ∧
        AlgebraicCombinatorics.FPS.Laurent.kBoundedBTValue k f = n

Docstring: **Each integer in `[-M_k, M_k]` has a unique k-bounded balanced ternary representation**.

This is the finite version of the balanced ternary uniqueness theorem.

The proof uses a cardinality argument:
- There are `3^{k+1}` k-bounded representations (`card_kBoundedBTReps`)
- The target set `Icc_symm (maxBT k)` has cardinality `3^{k+1}` (`card_Icc_symm_maxBT`)
- Each representation maps to a value in the target set (`kBoundedBTValue_mem_Icc`)
- By the pigeonhole principle, the map is a bijection

(Part of Theorem thm.fps.laure.balanced-tern-rep-uniq) 

## TARGET AlgebraicCombinatorics.balancedTernaryRepresentation_bounded_unique (theorem) — ELABORATED SIGNATURE
∀ (k : ℕ) (n : ℤ),
  |n| ≤ ∑ i ∈ Finset.range (k + 1), 3 ^ i →
    ∀ (r₁ r₂ : AlgebraicCombinatorics.BalancedTernaryRepresentation n),
      r₁.isBounded k → r₂.isBounded k → r₁.digits = r₂.digits

Docstring: Each integer n with |n| ≤ 3^0 + 3^1 + ... + 3^k has a unique k-bounded
balanced ternary representation.

This is the key lemma used in the rigorous proof of
Theorem `thm.fps.laure.balanced-tern-rep-uniq`. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.FPS.Laurent.Icc_symm (def)
ℕ → Finset ℤ

Body:
fun M => Finset.Icc (-↑M) ↑M

Docstring: The set of integers from -M to M. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.FPS.Laurent.maxBT (def)
ℕ → ℕ

Body:
fun k => ∑ i ∈ Finset.range (k + 1), 3 ^ i

Docstring: The maximum absolute value representable with k+1 balanced ternary digits:
`M_k = 3^0 + 3^1 + ... + 3^k = (3^{k+1} - 1) / 2` 

## PROJECT DEPENDENCY AlgebraicCombinatorics.FPS.Laurent.kBoundedBTReps (def)
(k : ℕ) → Finset (Fin (k + 1) → ℤ)

Body:
fun k => Fintype.piFinset fun x => AlgebraicCombinatorics.FPS.Laurent.btDigits

Docstring: A k-bounded balanced ternary representation is a function `f : Fin (k+1) → {-1, 0, 1}`.

These are representations where `f(i) = 0` for all `i > k`. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.FPS.Laurent.kBoundedBTValue (def)
(k : ℕ) → (Fin (k + 1) → ℤ) → ℤ

Body:
fun k f => ∑ i, f i * 3 ^ ↑i

Docstring: The value of a k-bounded balanced ternary representation. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.FPS.Laurent.btDigits (def)
Finset ℤ

Body:
{-1, 0, 1}

Docstring: The set of balanced ternary digits {-1, 0, 1}. 

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


## PROJECT DEPENDENCY AlgebraicCombinatorics.BalancedTernaryRepresentation.isBounded (def)
{n : ℤ} → AlgebraicCombinatorics.BalancedTernaryRepresentation n → ℕ → Prop

Body:
fun {n} r k => ∀ i > k, r.digits i = 0

Docstring: A balanced ternary representation is k-bounded if b_{k+1} = b_{k+2} = ... = 0. 

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

## PROJECT DEPENDENCY AlgebraicCombinatorics.BalancedTernaryDigit.toInt (def)
AlgebraicCombinatorics.BalancedTernaryDigit → ℤ

Body:
fun x =>
  match x with
  | AlgebraicCombinatorics.BalancedTernaryDigit.negOne => -1
  | AlgebraicCombinatorics.BalancedTernaryDigit.zero => 0
  | AlgebraicCombinatorics.BalancedTernaryDigit.one => 1

Docstring: Convert a balanced ternary digit to an integer 

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

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF Int
Type

Docstring: The integers.

This type is special-cased by the compiler and overridden with an efficient implementation. The
runtime has a special representation for `Int` that stores “small” signed numbers directly, while
larger numbers use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)). A “small number” is an integer that can be encoded with one fewer bits
than the platform's pointer size (i.e. 63 bits on 64-bit architectures and 31 bits on 32-bit
architectures).


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

## BASE-LIBRARY REF ExistsUnique
{α : Sort u_1} → (α → Prop) → Prop

Docstring: For `p : α → Prop`, `ExistsUnique p` means that there exists a unique `x : α` with `p x`. 

## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


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

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

## BASE-LIBRARY REF And
Prop → Prop → Prop

Docstring: `And a b`, or `a ∧ b`, is the conjunction of propositions. It can be
constructed and destructed like a pair: if `ha : a` and `hb : b` then
`⟨ha, hb⟩ : a ∧ b`, and if `h : a ∧ b` then `h.left : a` and `h.right : b`.


Conventions for notations in identifiers:

 * The recommended spelling of `∧` in identifiers is `and`.

 * The recommended spelling of `/\` in identifiers is `and` (prefer `∧` over `/\`).

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

## BASE-LIBRARY REF Finset.Icc
{α : Type u_1} → [inst : Preorder α] → [LocallyFiniteOrder α] → α → α → Finset α

Docstring: The finset $[a, b]$ of elements `x` such that `a ≤ x` and `x ≤ b`. Basically `Set.Icc a b` as a
finset. 

## BASE-LIBRARY REF PartialOrder.toPreorder
{α : Type u_2} → [self : PartialOrder α] → Preorder α

## BASE-LIBRARY REF SemilatticeInf.toPartialOrder
{α : Type u} → [self : SemilatticeInf α] → PartialOrder α

## BASE-LIBRARY REF Lattice.toSemilatticeInf
{α : Type u} → [self : Lattice α] → SemilatticeInf α

## BASE-LIBRARY REF instLatticeInt
Lattice ℤ

## BASE-LIBRARY REF Int.instLocallyFiniteOrder
LocallyFiniteOrder ℤ

## BASE-LIBRARY REF Neg.neg
{α : Type u} → [self : Neg α] → α → α

Docstring: `-a` computes the negative or opposite of `a`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `-` in identifiers is `neg` (when used as a unary operator).

## BASE-LIBRARY REF Int.instNegInt
Neg ℤ

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

## BASE-LIBRARY REF Finset.sum
{ι : Type u_1} → {M : Type u_3} → [AddCommMonoid M] → Finset ι → (ι → M) → M

Docstring: `∑ x ∈ s, f x` is the sum of `f x` as `x` ranges over the elements
of the finite set `s`.

When the index type is a `Fintype`, the notation `∑ x, f x`, is a shorthand for
`∑ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF Nat.instAddCommMonoid
AddCommMonoid ℕ

## BASE-LIBRARY REF Finset.range
ℕ → Finset ℕ

Docstring: `range n` is the set of natural numbers less than `n`. 

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

## BASE-LIBRARY REF Nat.instMonoid
Monoid ℕ

## BASE-LIBRARY REF Fintype.piFinset
{α : Type u_1} → [DecidableEq α] → [Fintype α] → {δ : α → Type u_4} → ((a : α) → Finset (δ a)) → Finset ((a : α) → δ a)

Docstring: Given for all `a : α` a finset `t a` of `δ a`, then one can define the
finset `Fintype.piFinset t` of all functions taking values in `t a` for all `a`. This is the
analogue of `Finset.pi` where the base finset is `univ` (but formally they are not the same, as
there is an additional condition `i ∈ Finset.univ` in the `Finset.pi` definition). 

## BASE-LIBRARY REF instDecidableEqFin
(n : ℕ) → DecidableEq (Fin n)

## BASE-LIBRARY REF Fin.fintype
(n : ℕ) → Fintype (Fin n)

## BASE-LIBRARY REF Int.instAddCommMonoid
AddCommMonoid ℤ

## BASE-LIBRARY REF Finset.univ
{α : Type u_1} → [Fintype α] → Finset α

Docstring: `univ` is the universal finite set of type `Finset α` implied from
the assumption `Fintype α`. 

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

## BASE-LIBRARY REF Int.instMonoid
Monoid ℤ

## BASE-LIBRARY REF instOfNat
{n : ℕ} → OfNat ℤ n

## BASE-LIBRARY REF Fin.val
{n : ℕ} → Fin n → ℕ

Docstring: The number that is strictly less than `n`.

`Fin.val` is a coercion, so any `Fin n` can be used in a position where a `Nat` is expected.


## BASE-LIBRARY REF Insert.insert
{α : outParam (Type u)} → {γ : Type v} → [self : Insert α γ] → α → γ → γ

Docstring: `insert x xs` inserts the element `x` into the collection `xs`. 

## BASE-LIBRARY REF Finset.instInsert
{α : Type u_1} → [DecidableEq α] → Insert α (Finset α)

Docstring: `insert a s` is the set `{a} ∪ s` containing `a` and the elements of `s`. 

## BASE-LIBRARY REF Int.instDecidableEq
DecidableEq ℤ

Docstring: Decides whether two integers are equal. Usually accessed via the `DecidableEq Int` instance.

This function is overridden by the compiler with an efficient implementation. This definition is the
logical model.

Examples:
* `show (7 : Int) = (3 : Int) + (4 : Int) by decide`
* `if (6 : Int) = (3 : Int) * (2 : Int) then "yes" else "no" = "yes"`
* `(¬ (6 : Int) = (3 : Int)) = true`


## BASE-LIBRARY REF Singleton.singleton
{α : outParam (Type u)} → {β : Type v} → [self : Singleton α β] → α → β

Docstring: `singleton x` is a collection with the single element `x` (notation: `{x}`). 

Conventions for notations in identifiers:

 * The recommended spelling of `{x}` in identifiers is `singleton`.

## BASE-LIBRARY REF Finset.instSingleton
{α : Type u_1} → Singleton α (Finset α)

Docstring: `{a} : Finset a` is the set `{a}` containing `a` and nothing else.

This differs from `insert a ∅` in that it does not require a `DecidableEq` instance for `α`.


## BASE-LIBRARY REF LE.le
{α : Type u} → [self : LE α] → α → α → Prop

Docstring: The less-equal relation: `x ≤ y` 

Conventions for notations in identifiers:

 * The recommended spelling of `≤` in identifiers is `le`.

 * The recommended spelling of `<=` in identifiers is `le` (prefer `≤` over `<=`).

## BASE-LIBRARY REF Int.instLEInt
LE ℤ

## BASE-LIBRARY REF abs
{α : Type u_1} → [Lattice α] → [AddGroup α] → α → α

Docstring: `abs a`, denoted `|a|`, is the absolute value of `a` 

## BASE-LIBRARY REF Int.instAddGroup
AddGroup ℤ

## BASE-LIBRARY REF Set.Finite
{α : Type u} → Set α → Prop

Docstring: A set is finite if the corresponding `Subtype` is finite,
i.e., if there exists a natural `n : ℕ` and an equivalence `s ≃ Fin n`. 

## BASE-LIBRARY REF setOf
{α : Type u} → (α → Prop) → Set α

Docstring: Turn a predicate `p : α → Prop` into a set, also written as `{x | p x}` 

## BASE-LIBRARY REF Ne
{α : Sort u} → α → α → Prop

Docstring: `a ≠ b`, or `Ne a b` is defined as `¬ (a = b)` or `a = b → False`,
and asserts that `a` and `b` are not equal.


Conventions for notations in identifiers:

 * The recommended spelling of `≠` in identifiers is `ne`.

## BASE-LIBRARY REF Zero.toOfNat0
{α : Type u_1} → [Zero α] → OfNat α 0

## BASE-LIBRARY REF finsum
{M : Type u_7} → {α : Sort u_8} → [AddCommMonoid M] → (α → M) → M

Docstring: Sum of `f x` as `x` ranges over the elements of the support of `f`, if it's finite. Zero
otherwise. 

## BASE-LIBRARY REF GT.gt
{α : Type u} → [LT α] → α → α → Prop

Docstring: `a > b` is an abbreviation for `b < a`. 

Conventions for notations in identifiers:

 * The recommended spelling of `>` in identifiers is `gt`.

## BASE-LIBRARY REF instLTNat
LT ℕ

## BASE-LIBRARY REF Zero
Type u → Type u

Docstring: A type with a zero element. 

## BASE-LIBRARY REF Zero.mk
{α : Type u} → α → Zero α

## BASE-LIBRARY REF Unit
Type

Docstring: The canonical type with one element. This element is written `()`.

`Unit` has a number of uses:
* It can be used to model control flow that returns from a function call without providing other
  information.
* Monadic actions that return `Unit` have side effects without computing values.
* In polymorphic types, it can be used to indicate that no data is to be stored in a particular
  field.


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


## BASE-LIBRARY REF ite
{α : Sort u} → (c : Prop) → [h : Decidable c] → α → α → α

Docstring: `if c then t else e` is notation for `ite c t e`, "if-then-else", which decides to
return `t` or `e` depending on whether `c` is true or false. The explicit argument
`c : Prop` does not have any actual computational content, but there is an additional
`[Decidable c]` argument synthesized by typeclass inference which actually
determines how to evaluate `c` to true or false. Write `if h : c then t else e`
instead for a "dependent if-then-else" `dite`, which allows `t`/`e` to use the fact
that `c` is true/false.


## BASE-LIBRARY REF GE.ge
{α : Type u} → [LE α] → α → α → Prop

Docstring: `a ≥ b` is an abbreviation for `b ≤ a`. 

Conventions for notations in identifiers:

 * The recommended spelling of `≥` in identifiers is `ge`.

 * The recommended spelling of `>=` in identifiers is `ge` (prefer `≥` over `>=`).

## BASE-LIBRARY REF instLENat
LE ℕ

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
k-bounded balanced ternary uniqueness

\leanhelper  Each integer $n$ with $|n| \le 3^0 + 3^1 + \cdots + 3^k$ has a unique $k$-bounded balanced ternary representation.

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
  "justification": "The first target directly formalizes the full existence-and-uniqueness claim. It quantifies `\u2200 (k : \u2115), \u2200 n \u2208 Icc_symm (maxBT k)` and concludes `\u2203! f, f \u2208 kBoundedBTReps k \u2227 kBoundedBTValue k f = n`. By definition, `Icc_symm (maxBT k)` is the integers between `-\u2211 i \u2208 Finset.range (k+1), 3^i` and that sum, equivalent to the blueprint condition `|n| \u2264 3^0 + \u22ef + 3^k`. Also, `kBoundedBTReps k` consists exactly of functions on `Fin (k+1)` with values in `{-1,0,1}`, and `kBoundedBTValue` is `\u2211 i, f i * 3^i`; extending such a function by zero above `k` gives precisely an essentially finite, k-bounded representation in the informal sense. Thus its `\u2203!` supplies both existence and uniqueness. The second target, `balancedTernaryRepresentation_bounded_unique`, only states pairwise uniqueness\u2014`r\u2081.isBounded k \u2192 r\u2082.isBounded k \u2192 r\u2081.digits = r\u2082.digits`\u2014and would not alone formalize the word \u201chas,\u201d since it contains no existence conclusion. In this package, however, existence and uniqueness are already asserted by `kBounded_unique`, so the package implies the full blueprint statement; the second declaration is a compatible uniqueness lemma rather than a weakening of the complete formalization."
}