## TARGET AlgebraicCombinatorics.Composition.ofSize (def) — ELABORATED SIGNATURE
ℕ → Type

Body:
fun n => { α // α.size = n }

Docstring: A composition of `n` is a composition whose size is `n`.

(Definition def.fps.comps, part (d))


## TARGET AlgebraicCombinatorics.Composition.size (def) — ELABORATED SIGNATURE
AlgebraicCombinatorics.Composition → ℕ

Body:
fun α => (List.map (fun x => ↑x) α).sum

Docstring: The size of a composition is the sum of its entries.

(Definition def.fps.comps, part (b))


## TARGET AlgebraicCombinatorics.Composition.ofSizeIntoParts (def) — ELABORATED SIGNATURE
ℕ → ℕ → Type

Body:
fun n k => { α // α.size = n ∧ α.len = k }

Docstring: A composition of `n` into `k` parts is a composition with size `n` and length `k`.

(Definition def.fps.comps, part (e))


## TARGET AlgebraicCombinatorics.Composition.len (def) — ELABORATED SIGNATURE
AlgebraicCombinatorics.Composition → ℕ

Body:
fun α => List.length α

Docstring: The length of a composition is the number of parts.
(We use `len` to avoid conflict with `List.length`.)

(Definition def.fps.comps, part (c))


## TARGET AlgebraicCombinatorics.Composition (def) — ELABORATED SIGNATURE
Type

Body:
List ℕ+

Docstring: An integer composition is a finite tuple of positive integers.
We represent it as a list of positive integers.

(Definition def.fps.comps, part (a))


## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


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

## BASE-LIBRARY REF List.map
{α : Type u_1} → {β : Type u_2} → (α → β) → List α → List β

Docstring: Applies a function to each element of the list, returning the resulting list of values.

`O(|l|)`.

Examples:
* `[a, b, c].map f = [f a, f b, f c]`
* `[].map Nat.succ = []`
* `["one", "two", "three"].map (·.length) = [3, 3, 5]`
* `["one", "two", "three"].map (·.reverse) = ["eno", "owt", "eerht"]`


## BASE-LIBRARY REF PNat
Type

Docstring: `ℕ+` is the type of positive natural numbers. It is defined as a subtype,
and the VM representation of `ℕ+` is the same as `ℕ` because the proof
is not stored. 

## BASE-LIBRARY REF PNat.val
ℕ+ → ℕ

Docstring: The underlying natural number 

## BASE-LIBRARY REF And
Prop → Prop → Prop

Docstring: `And a b`, or `a ∧ b`, is the conjunction of propositions. It can be
constructed and destructed like a pair: if `ha : a` and `hb : b` then
`⟨ha, hb⟩ : a ∧ b`, and if `h : a ∧ b` then `h.left : a` and `h.right : b`.


Conventions for notations in identifiers:

 * The recommended spelling of `∧` in identifiers is `and`.

 * The recommended spelling of `/\` in identifiers is `and` (prefer `∧` over `/\`).

## BASE-LIBRARY REF List.length
{α : Type u_1} → List α → ℕ

Docstring: The length of a list.

This function is overridden in the compiler to `lengthTR`, which uses constant stack space.

Examples:
* `([] : List String).length = 0`
* `["green", "brown"].length = 2`


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


## INFORMAL STATEMENT
def.fps.comps

\textbf{(a)} An \emph{(integer) composition} means a (finite) tuple of positive integers. \medskip 

\textbf{(b)} The \emph{size} of an integer composition $\alpha =\left( \alpha _{1},\alpha _{2},\ldots ,\alpha _{m}\right) $ is defined to be the integer $\alpha _{1}+\alpha _{2}+\cdots +\alpha _{m}$. It is written $\left\vert \alpha \right\vert $. \medskip 

\textbf{(c)} The \emph{length} of an integer composition $\alpha =\left( \alpha _{1},\alpha _{2},\ldots ,\alpha _{m}\right) $ is defined to be the integer $m$. It is written $\ell \left( \alpha \right) $. \medskip 

\textbf{(d)} Let $n\in \mathbb {N}$. A \emph{composition of }$n$ means a composition whose size is $n$. \medskip 

\textbf{(e)} Let $n\in \mathbb {N}$ and $k\in \mathbb {N}$. A \emph{composition of }$n$\emph{ into }$k$\emph{ parts} is a composition whose size is $n$ and whose length is $k$.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The formal definitions match all five clauses. For (a), `Composition` has body `List \u2115+`, representing exactly a finite ordered tuple of positive integers. For (b), `size` is `fun \u03b1 => (List.map (fun x => \u2191x) \u03b1).sum`, exactly the sum of the underlying natural-number values of the positive entries. For (c), `len` is `fun \u03b1 => List.length \u03b1`, the number of parts. For (d), `ofSize : \u2115 \u2192 Type` has body `fun n => { \u03b1 // \u03b1.size = n }`, exactly compositions whose size is `n`. For (e), `ofSizeIntoParts : \u2115 \u2192 \u2115 \u2192 Type` has body `fun n k => { \u03b1 // \u03b1.size = n \u2227 \u03b1.len = k }`, exactly compositions of size `n` and length `k`. The binders `n k : \u2115` agree with the blueprint\u2019s `n,k \u2208 \u2115`, and no additional hypotheses or restrictions are introduced."
}