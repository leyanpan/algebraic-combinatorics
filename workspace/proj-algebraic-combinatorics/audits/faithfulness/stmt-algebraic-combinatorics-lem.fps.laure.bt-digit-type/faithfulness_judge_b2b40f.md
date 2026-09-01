## TARGET AlgebraicCombinatorics.BalancedTernaryDigit.toInt (def) — ELABORATED SIGNATURE
AlgebraicCombinatorics.BalancedTernaryDigit → ℤ

Body:
fun x =>
  match x with
  | AlgebraicCombinatorics.BalancedTernaryDigit.negOne => -1
  | AlgebraicCombinatorics.BalancedTernaryDigit.zero => 0
  | AlgebraicCombinatorics.BalancedTernaryDigit.one => 1

Docstring: Convert a balanced ternary digit to an integer 

## TARGET AlgebraicCombinatorics.BalancedTernaryDigit (inductive) — ELABORATED SIGNATURE
Type

Body:
AlgebraicCombinatorics.BalancedTernaryDigit.negOne : AlgebraicCombinatorics.BalancedTernaryDigit
AlgebraicCombinatorics.BalancedTernaryDigit.zero : AlgebraicCombinatorics.BalancedTernaryDigit
AlgebraicCombinatorics.BalancedTernaryDigit.one : AlgebraicCombinatorics.BalancedTernaryDigit

Docstring: The set of balanced ternary digits: {-1, 0, 1} 

## TARGET AlgebraicCombinatorics.BalancedTernaryDigit.toInt_injective (theorem) — ELABORATED SIGNATURE
Function.Injective AlgebraicCombinatorics.BalancedTernaryDigit.toInt

Docstring: Different digits have different integer values 

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

## BASE-LIBRARY REF Int
Type

Docstring: The integers.

This type is special-cased by the compiler and overridden with an efficient implementation. The
runtime has a special representation for `Int` that stores “small” signed numbers directly, while
larger numbers use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)). A “small number” is an integer that can be encoded with one fewer bits
than the platform's pointer size (i.e. 63 bits on 64-bit architectures and 31 bits on 32-bit
architectures).


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

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNat
{n : ℕ} → OfNat ℤ n

## BASE-LIBRARY REF Function.Injective
{α : Sort u_1} → {β : Sort u_2} → (α → β) → Prop

Docstring: A function `f : α → β` is called injective if `f x = f y` implies `x = y`. 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


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
Balanced ternary digit type

\leanhelper  A balanced ternary digit is one of $-1$, $0$, or $1$. There is an injection from the set of balanced ternary digits to $\mathbb {Z}$ sending each digit to its integer value. This injection is injective, and two digits are equal if and only if their integer values are congruent modulo $3$.

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
  "justification": "The inductive declaration has exactly the three constructors `negOne`, `zero`, and `one`, matching \u201cone of $-1$, $0$, or $1$.\u201d The body of `BalancedTernaryDigit.toInt` sends them respectively to `-1`, `0`, and `1` in `\u2124`, matching \u201csending each digit to its integer value,\u201d and `toInt_injective : Function.Injective ...toInt` directly states injectivity. The final congruence clause is also implied: the three integer images `-1`, `0`, and `1` are pairwise incongruent modulo `3`, so two such digits have congruent values exactly when they are equal. There are no added binders or hypotheses restricting the blueprint statement."
}