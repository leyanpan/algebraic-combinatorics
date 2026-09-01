## TARGET AlgebraicCombinatorics.FPS.isDyckWord (def) — ELABORATED SIGNATURE
List Bool → Prop

Body:
fun w =>
  List.count true w = List.count false w ∧
    ∀ k ≤ w.length, List.count false (List.take k w) ≤ List.count true (List.take k w)

Docstring: A list is a Dyck word if it consists of 0s and 1s, has equal numbers
of each, and every prefix has at least as many 1s as 0s.

Here we represent 1 as `true` and 0 as `false`.

**Mathlib note**: This is an alternative representation to Mathlib's `DyckWord` structure,
which uses a `DyckStep` enum with constructors `U` (up) and `D` (down). The two representations
are equivalent via the bijection sending `true` to `U` and `false` to `D`. 

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


## BASE-LIBRARY REF Bool
Type

Docstring: The Boolean values, `true` and `false`.

Logically speaking, this is equivalent to `Prop` (the type of propositions). The distinction is
public important for programming: both propositions and their proofs are erased in the code generator,
while `Bool` corresponds to the Boolean type in most programming languages and carries precisely one
bit of run-time information.


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

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF List.count
{α : Type u} → [BEq α] → α → List α → ℕ

Docstring: Counts the number of times an element occurs in a list.

Examples:
* `[1, 1, 2, 3, 5].count 1 = 2`
* `[1, 1, 2, 3, 5].count 5 = 1`
* `[1, 1, 2, 3, 5].count 4 = 0`


## BASE-LIBRARY REF instBEqOfDecidableEq
{α : Type u_1} → [DecidableEq α] → BEq α

## BASE-LIBRARY REF instDecidableEqBool
DecidableEq Bool

## BASE-LIBRARY REF Bool.true
Bool

Docstring: The Boolean value `true`, not to be confused with the proposition `True`. 

## BASE-LIBRARY REF Bool.false
Bool

Docstring: The Boolean value `false`, not to be confused with the proposition `False`. 

## BASE-LIBRARY REF LE.le
{α : Type u} → [self : LE α] → α → α → Prop

Docstring: The less-equal relation: `x ≤ y` 

Conventions for notations in identifiers:

 * The recommended spelling of `≤` in identifiers is `le`.

 * The recommended spelling of `<=` in identifiers is `le` (prefer `≤` over `<=`).

## BASE-LIBRARY REF instLENat
LE ℕ

## BASE-LIBRARY REF List.length
{α : Type u_1} → List α → ℕ

Docstring: The length of a list.

This function is overridden in the compiler to `lengthTR`, which uses constant stack space.

Examples:
* `([] : List String).length = 0`
* `["green", "brown"].length = 2`


## BASE-LIBRARY REF List.take
{α : Type u} → ℕ → List α → List α

Docstring: Extracts the first `n` elements of `xs`, or the whole list if `n` is greater than `xs.length`.

`O(min n |xs|)`.

Examples:
* `[a, b, c, d, e].take 0 = []`
* `[a, b, c, d, e].take 3 = [a, b, c]`
* `[a, b, c, d, e].take 6 = [a, b, c, d, e]`


## INFORMAL STATEMENT
def.catalan.dyck

\leanhelper  A \emph{Dyck word} of length $2n$ is a list of $0$s and $1$s with equal numbers of each, such that every prefix has at least as many $1$s as $0$s.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The body exactly encodes the defining conditions: `List Bool` makes `w` a list consisting only of `0`s and `1`s (represented by `false` and `true`); `List.count true w = List.count false w` gives equal numbers of each; and `\u2200 k \u2264 w.length, List.count false (List.take k w) \u2264 List.count true (List.take k w)` says every prefix has at least as many `1`s as `0`s. Although the informal wording says \u201cof length $2n$\u201d and the formal definition has no `n` binder, equal counts imply that the total length is twice the number of `true` entries, so every word satisfying the predicate has length `2n` for some `n`. Thus no mathematically contentful condition is omitted or added."
}