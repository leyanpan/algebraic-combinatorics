## TARGET AlgebraicCombinatorics.FPS.Laurent.balancedTernary_exists_unique (theorem) — ELABORATED SIGNATURE
∀ (n : ℤ),
  ∃! f,
    (∀ (i : ℕ), f i ∈ AlgebraicCombinatorics.FPS.Laurent.btDigits) ∧
      AlgebraicCombinatorics.FPS.Laurent.balancedTernaryValue f = n

Docstring: **Unique Balanced Ternary Representation Theorem**.
(Theorem thm.fps.laure.balanced-tern-rep-uniq, label: thm.fps.laure.balanced-tern-rep-uniq)

Each integer `n` has a unique balanced ternary representation. More precisely, there exists
a unique finitely supported function `f : ℕ → ℤ` with values in {-1, 0, 1} such that
`n = ∑_{i ∈ support(f)} f(i) · 3^i`.

This theorem generalizes the binary representation uniqueness to allow negative digits,
which enables representing negative integers directly (without a separate sign).

The proof uses Laurent polynomials and the key identity:
  `∏_{i=0}^{k} (1 + x^{3^i} + x^{-3^i}) = ∑_{|n| ≤ M_k} x^n`
where `M_k = 3^0 + 3^1 + ... + 3^k = (3^{k+1} - 1) / 2`.

Comparing coefficients shows that each integer in `[-M_k, M_k]` has exactly one
k-bounded balanced ternary representation. Taking `k → ∞` gives the full result.

Historical note: Balanced ternary representations were used in the Soviet Setun computer
(1960s/70s). The uniqueness theorem goes back to Fibonacci. 

## TARGET AlgebraicCombinatorics.balancedTernaryRepresentation_unique (theorem) — ELABORATED SIGNATURE
∀ (n : ℤ) (r₁ r₂ : AlgebraicCombinatorics.BalancedTernaryRepresentation n), r₁.digits = r₂.digits

Docstring: The balanced ternary representation of an integer is unique.
This is Theorem `thm.fps.laure.balanced-tern-rep-uniq`. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.FPS.Laurent.btDigits (def)
Finset ℤ

Body:
{-1, 0, 1}

Docstring: The set of balanced ternary digits {-1, 0, 1}. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.FPS.Laurent.balancedTernaryValue (def)
(ℕ →₀ ℤ) → ℤ

Body:
fun f => ∑ i ∈ f.support, f i * 3 ^ i

Docstring: The value of a finitely supported balanced ternary representation. 

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

## BASE-LIBRARY REF Int
Type

Docstring: The integers.

This type is special-cased by the compiler and overridden with an efficient implementation. The
runtime has a special representation for `Int` that stores “small” signed numbers directly, while
larger numbers use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)). A “small number” is an integer that can be encoded with one fewer bits
than the platform's pointer size (i.e. 63 bits on 64-bit architectures and 31 bits on 32-bit
architectures).


## BASE-LIBRARY REF ExistsUnique
{α : Sort u_1} → (α → Prop) → Prop

Docstring: For `p : α → Prop`, `ExistsUnique p` means that there exists a unique `x : α` with `p x`. 

## BASE-LIBRARY REF Finsupp
Type u_9 → (M : Type u_10) → [Zero M] → Type (max u_10 u_9)

Docstring: `Finsupp α M`, denoted `α →₀ M`, is the type of functions `f : α → M` such that
`f x = 0` for all but finitely many `x`. 

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

## BASE-LIBRARY REF And
Prop → Prop → Prop

Docstring: `And a b`, or `a ∧ b`, is the conjunction of propositions. It can be
constructed and destructed like a pair: if `ha : a` and `hb : b` then
`⟨ha, hb⟩ : a ∧ b`, and if `h : a ∧ b` then `h.left : a` and `h.right : b`.


Conventions for notations in identifiers:

 * The recommended spelling of `∧` in identifiers is `and`.

 * The recommended spelling of `/\` in identifiers is `and` (prefer `∧` over `/\`).

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

## BASE-LIBRARY REF DFunLike.coe
{F : Sort u_1} → {α : outParam (Sort u_2)} → {β : outParam (α → Sort u_3)} → [self : DFunLike F α β] → F → (a : α) → β a

Docstring: The coercion from `F` to a function. 

## BASE-LIBRARY REF Finsupp.instFunLike
{α : Type u_1} → {M : Type u_4} → [inst : Zero M] → FunLike (α →₀ M) α M

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

## BASE-LIBRARY REF Singleton.singleton
{α : outParam (Type u)} → {β : Type v} → [self : Singleton α β] → α → β

Docstring: `singleton x` is a collection with the single element `x` (notation: `{x}`). 

Conventions for notations in identifiers:

 * The recommended spelling of `{x}` in identifiers is `singleton`.

## BASE-LIBRARY REF Finset.instSingleton
{α : Type u_1} → Singleton α (Finset α)

Docstring: `{a} : Finset a` is the set `{a}` containing `a` and nothing else.

This differs from `insert a ∅` in that it does not require a `DecidableEq` instance for `α`.


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
thm.fps.laure.balanced-tern-rep-uniq

Each integer $n$ has a unique balanced ternary representation.

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
  "justification": "The first target directly matches the full blueprint theorem. Its binder `\u2200 (n : \u2124), \u2203! f, ...` expresses existence and uniqueness for every integer. The inferred `f : \u2115 \u2192\u2080 \u2124` is finitely supported, exactly encoding the definition\u2019s \u201cessentially finite sequence.\u201d The condition `\u2200 (i : \u2115), f i \u2208 btDigits`, together with `btDigits = {-1, 0, 1}`, gives the required digit range. Finally, `balancedTernaryValue f = n`, whose body is `\u2211 i \u2208 f.support, f i * 3 ^ i`, is equivalent to the informal equation `n = \u2211_{i\u2208\u2115} b_i 3^i` because a finitely supported sequence sums over its support and equality is symmetric. The second target, `\u2200 (n : \u2124) (r\u2081 r\u2082 : BalancedTernaryRepresentation n), r\u2081.digits = r\u2082.digits`, correctly states the uniqueness component for the structured representation type; existence is already supplied by the first target."
}