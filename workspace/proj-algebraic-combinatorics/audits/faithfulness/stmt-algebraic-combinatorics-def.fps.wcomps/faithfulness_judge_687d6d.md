## TARGET AlgebraicCombinatorics.WeakComposition.size (def) — ELABORATED SIGNATURE
AlgebraicCombinatorics.WeakComposition → ℕ

Body:
fun α => List.sum α

Docstring: The size of a weak composition is the sum of its entries.

(Definition def.fps.wcomps, part (b))


## TARGET AlgebraicCombinatorics.WeakComposition.len (def) — ELABORATED SIGNATURE
AlgebraicCombinatorics.WeakComposition → ℕ

Body:
fun α => List.length α

Docstring: The length of a weak composition is the number of parts.
(We use `len` to avoid conflict with `List.length`.)

(Definition def.fps.wcomps, part (c))


## TARGET AlgebraicCombinatorics.WeakComposition.ofSize (def) — ELABORATED SIGNATURE
ℕ → Type

Body:
fun n => { α // α.size = n }

Docstring: A weak composition of `n` is a weak composition whose size is `n`.

(Definition def.fps.wcomps, part (d))


## TARGET AlgebraicCombinatorics.WeakComposition (def) — ELABORATED SIGNATURE
Type

Body:
List ℕ

Docstring: A weak composition is a finite tuple of nonnegative integers.

(Definition def.fps.wcomps, part (a))


## TARGET AlgebraicCombinatorics.WeakComposition.ofSizeIntoParts (def) — ELABORATED SIGNATURE
ℕ → ℕ → Type

Body:
fun n k => { α // α.size = n ∧ α.len = k }

Docstring: A weak composition of `n` into `k` parts is a tuple of `k` nonnegative integers summing to `n`.

(Definition def.fps.wcomps, part (e))


## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF List.sum
{α : Type u_1} → [Add α] → [Zero α] → List α → α

Docstring: Computes the sum of the elements of a list.

Examples:
* `[a, b, c].sum = a + (b + (c + 0))`
* `[1, 2, 5].sum = 8`


## BASE-LIBRARY REF instAddNat
Add ℕ

## BASE-LIBRARY REF MulZeroClass.toZero
{M₀ : Type u} → [self : MulZeroClass M₀] → Zero M₀

## BASE-LIBRARY REF Nat.instMulZeroClass
MulZeroClass ℕ

## BASE-LIBRARY REF List.length
{α : Type u_1} → List α → ℕ

Docstring: The length of a list.

This function is overridden in the compiler to `lengthTR`, which uses constant stack space.

Examples:
* `([] : List String).length = 0`
* `["green", "brown"].length = 2`


## BASE-LIBRARY REF Subtype
{α : Sort u} → (α → Prop) → Sort (max 1 u)

Docstring: All the elements of a type that satisfy a predicate.

`Subtype p`, usually written `{ x : α // p x }` or `{ x // p x }`, contains all elements `x : α` for
which `p x` is true. Its constructor is a pair of the value and the proof that it satisfies the
predicate. In run-time code, `{ x : α // p x }` is represented identically to `α`.

There is a coercion from `{ x : α // p x }` to `α`, so elements of a subtype may be used where the
underlying type is expected.

Examples:
 * `{ n : Nat // n % 2 = 0 }` is the type of even numbers.
 * `{ xs : Array String // xs.size = 5 }` is the type of arrays with five `String`s.
 * Given `xs : List α`, `List { x : α // x ∈ xs }` is the type of lists in which all elements are
   contained in `xs`.


Conventions for notations in identifiers:

 * The recommended spelling of `{ x // p x }` in identifiers is `subtype`.

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


## BASE-LIBRARY REF And
Prop → Prop → Prop

Docstring: `And a b`, or `a ∧ b`, is the conjunction of propositions. It can be
constructed and destructed like a pair: if `ha : a` and `hb : b` then
`⟨ha, hb⟩ : a ∧ b`, and if `h : a ∧ b` then `h.left : a` and `h.right : b`.


Conventions for notations in identifiers:

 * The recommended spelling of `∧` in identifiers is `and`.

 * The recommended spelling of `/\` in identifiers is `and` (prefer `∧` over `/\`).

## INFORMAL STATEMENT
def.fps.wcomps

\textbf{(a)} An \emph{(integer) weak composition} means a (finite) tuple of nonnegative integers. \medskip 

\textbf{(b)} The \emph{size} of a weak composition $\alpha =\left( \alpha _{1},\alpha _{2},\ldots ,\alpha _{m}\right) $ is defined to be the integer $\alpha _{1}+\alpha _{2}+\cdots +\alpha _{m}$. It is written $\left\vert \alpha \right\vert $. \medskip 

\textbf{(c)} The \emph{length} of a weak composition $\alpha =\left( \alpha _{1},\alpha _{2},\ldots ,\alpha _{m}\right) $ is defined to be the integer $m$. It is written $\ell \left( \alpha \right) $. \medskip 

\textbf{(d)} Let $n\in \mathbb {N}$. A \emph{weak composition of }$n$ means a weak composition whose size is $n$. \medskip 

\textbf{(e)} Let $n\in \mathbb {N}$ and $k\in \mathbb {N}$. A \emph{weak composition of }$n$\emph{ into }$k$\emph{ parts} is a weak composition whose size is $n$ and whose length is $k$.

## VERDICT
{
  "verdict": "faithful",
  "justification": "All five declarations match the corresponding clauses. (a) `WeakComposition := List \u2115` represents a finite ordered tuple whose entries are natural numbers, and `Nat` is \u201cthe natural numbers, starting at zero,\u201d hence nonnegative integers. (b) `size \u03b1 := List.sum \u03b1` is exactly the sum of the entries. (c) `len \u03b1 := List.length \u03b1` is exactly the number of parts. (d) `ofSize n := { \u03b1 // \u03b1.size = n }` is precisely the subtype of weak compositions having size `n`. (e) `ofSizeIntoParts n k := { \u03b1 // \u03b1.size = n \u2227 \u03b1.len = k }` is precisely the subtype having both size `n` and length `k`. The binders `n k : \u2115` agree with the blueprint\u2019s `n,k \u2208 \u2115`, and no additional hypotheses or restrictions are introduced."
}