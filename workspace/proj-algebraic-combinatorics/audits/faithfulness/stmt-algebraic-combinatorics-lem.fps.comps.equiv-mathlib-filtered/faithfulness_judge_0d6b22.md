## TARGET AlgebraicCombinatorics.Composition.equivMathlibFiltered (def) — ELABORATED SIGNATURE
(n k : ℕ) → AlgebraicCombinatorics.Composition.ofSizeIntoParts n k ≃ ↑{c | c.length = k}

Body:
fun n k =>
  {
    toFun := fun x =>
      match x with
      | ⟨α, hα⟩ => ⟨{ blocks := α.toBlocks, blocks_pos := ⋯, blocks_sum := ⋯ }, ⋯⟩,
    invFun := fun x =>
      match x with
      | ⟨c, hc⟩ => ⟨AlgebraicCombinatorics.Composition.ofBlocks c.blocks ⋯, ⋯⟩,
    left_inv := ⋯, right_inv := ⋯ }

Docstring: Equivalence between `Composition.ofSizeIntoParts n k` and the filtered set of Mathlib compositions
of `n` with length `k`.


## PROJECT DEPENDENCY AlgebraicCombinatorics.Composition.ofSizeIntoParts (def)
ℕ → ℕ → Type

Body:
fun n k => { α // α.size = n ∧ α.len = k }

Docstring: A composition of `n` into `k` parts is a composition with size `n` and length `k`.

(Definition def.fps.comps, part (e))


## PROJECT DEPENDENCY AlgebraicCombinatorics.Composition (def)
Type

Body:
List ℕ+

Docstring: An integer composition is a finite tuple of positive integers.
We represent it as a list of positive integers.

(Definition def.fps.comps, part (a))


## PROJECT DEPENDENCY AlgebraicCombinatorics.Composition.size (def)
AlgebraicCombinatorics.Composition → ℕ

Body:
fun α => (List.map (fun x => ↑x) α).sum

Docstring: The size of a composition is the sum of its entries.

(Definition def.fps.comps, part (b))


## PROJECT DEPENDENCY AlgebraicCombinatorics.Composition.len (def)
AlgebraicCombinatorics.Composition → ℕ

Body:
fun α => List.length α

Docstring: The length of a composition is the number of parts.
(We use `len` to avoid conflict with `List.length`.)

(Definition def.fps.comps, part (c))


## PROJECT DEPENDENCY AlgebraicCombinatorics.Composition.toBlocks (def)
AlgebraicCombinatorics.Composition → List ℕ

Body:
fun α => List.map (fun x => ↑x) α

Docstring: Convert a composition (List ℕ+) to a blocks list (List ℕ) 

## PROJECT DEPENDENCY AlgebraicCombinatorics.Composition.equivMathlib (def)
(n : ℕ) → AlgebraicCombinatorics.Composition.ofSize n ≃ Composition n

Body:
fun n =>
  {
    toFun := fun x =>
      match x with
      | ⟨α, hα⟩ => { blocks := α.toBlocks, blocks_pos := ⋯, blocks_sum := hα },
    invFun := fun c => ⟨AlgebraicCombinatorics.Composition.ofBlocks c.blocks ⋯, ⋯⟩, left_inv := ⋯, right_inv := ⋯ }

Docstring: Equivalence between our `Composition.ofSize n` and Mathlib's `Composition n`.
This allows us to use Mathlib's `composition_card` theorem.


## PROJECT DEPENDENCY AlgebraicCombinatorics.Composition.ofBlocks (def)
(blocks : List ℕ) → (∀ {i : ℕ}, i ∈ blocks → 0 < i) → AlgebraicCombinatorics.Composition

Body:
fun blocks hpos => List.pmap (fun i hi => ⟨i, hi⟩) blocks ⋯

Docstring: Convert a blocks list with positivity proof to a composition (List ℕ+) 

## PROJECT DEPENDENCY AlgebraicCombinatorics.Composition.ofSize (def)
ℕ → Type

Body:
fun n => { α // α.size = n }

Docstring: A composition of `n` is a composition whose size is `n`.

(Definition def.fps.comps, part (d))


## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF Equiv
Sort u_1 → Sort u_2 → Sort (max (max 1 u_1) u_2)

Docstring: `α ≃ β` is the type of functions from `α → β` with a two-sided inverse. 

## BASE-LIBRARY REF Set.Elem
{α : Type u} → Set α → Type u

Docstring: Given the set `s`, `Elem s` is the `Type` of element of `s`.

It is currently an abbreviation so that instance coming from `Subtype` are available.
If you're interested in making it a `def`, as it probably should be,
you'll then need to create additional instances (and possibly prove lemmas about them).
See e.g. `Mathlib/Data/Set/Order.lean`.


## BASE-LIBRARY REF Composition
ℕ → Type

Docstring: A composition of `n` is a list of positive integers summing to `n`. 

## BASE-LIBRARY REF setOf
{α : Type u} → (α → Prop) → Set α

Docstring: Turn a predicate `p : α → Prop` into a set, also written as `{x | p x}` 

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

## BASE-LIBRARY REF Composition.length
{n : ℕ} → Composition n → ℕ

Docstring: The length of a composition, i.e., the number of blocks in the composition. 

## BASE-LIBRARY REF Equiv.mk
{α : Sort u_1} →
  {β : Sort u_2} →
    (toFun : α → β) →
      (invFun : β → α) →
        autoParam (Function.LeftInverse invFun toFun) Equiv.left_inv._autoParam →
          autoParam (Function.RightInverse invFun toFun) Equiv.right_inv._autoParam → α ≃ β

## BASE-LIBRARY REF And
Prop → Prop → Prop

Docstring: `And a b`, or `a ∧ b`, is the conjunction of propositions. It can be
constructed and destructed like a pair: if `ha : a` and `hb : b` then
`⟨ha, hb⟩ : a ∧ b`, and if `h : a ∧ b` then `h.left : a` and `h.right : b`.


Conventions for notations in identifiers:

 * The recommended spelling of `∧` in identifiers is `and`.

 * The recommended spelling of `/\` in identifiers is `and` (prefer `∧` over `/\`).

## BASE-LIBRARY REF Subtype.mk
{α : Sort u} → {p : α → Prop} → (val : α) → p val → Subtype p

## BASE-LIBRARY REF Membership.mem
{α : outParam (Type u)} → {γ : Type v} → [self : Membership α γ] → γ → α → Prop

Docstring: The membership relation `a ∈ s : Prop` where `a : α`, `s : γ`. 

Conventions for notations in identifiers:

 * The recommended spelling of `∈` in identifiers is `mem`.

## BASE-LIBRARY REF Set
Type u → Type u

Docstring: A set is a collection of elements of some type `α`.

Although `Set` is defined as `α → Prop`, this is an implementation detail which should not be
relied on. Instead, `setOf` and membership of a set (`∈`) should be used to convert between sets
and predicates.


## BASE-LIBRARY REF Set.instMembership
{α : Type u} → Membership α (Set α)

## BASE-LIBRARY REF Composition.mk
{n : ℕ} → (blocks : List ℕ) → (∀ {i : ℕ}, i ∈ blocks → 0 < i) → blocks.sum = n → Composition n

## BASE-LIBRARY REF Composition.blocks
{n : ℕ} → Composition n → List ℕ

Docstring: List of positive integers summing to `n` 

## BASE-LIBRARY REF Composition.blocks_pos
∀ {n : ℕ} (self : Composition n) {i : ℕ}, i ∈ self.blocks → 0 < i

Docstring: Proof of positivity for `blocks` 

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


## BASE-LIBRARY REF PNat
Type

Docstring: `ℕ+` is the type of positive natural numbers. It is defined as a subtype,
and the VM representation of `ℕ+` is the same as `ℕ` because the proof
is not stored. 

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


## BASE-LIBRARY REF PNat.val
ℕ+ → ℕ

Docstring: The underlying natural number 

## BASE-LIBRARY REF List.length
{α : Type u_1} → List α → ℕ

Docstring: The length of a list.

This function is overridden in the compiler to `lengthTR`, which uses constant stack space.

Examples:
* `([] : List String).length = 0`
* `["green", "brown"].length = 2`


## BASE-LIBRARY REF List.instMembership
{α : Type u} → Membership α (List α)

## BASE-LIBRARY REF LT.lt
{α : Type u} → [self : LT α] → α → α → Prop

Docstring: The less-than relation: `x < y` 

Conventions for notations in identifiers:

 * The recommended spelling of `<` in identifiers is `lt`.

## BASE-LIBRARY REF instLTNat
LT ℕ

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

## BASE-LIBRARY REF List.pmap
{α : Type u_1} → {β : Type u_2} → {P : α → Prop} → ((a : α) → P a → β) → (l : List α) → (∀ a ∈ l, P a) → List β

Docstring: Maps a partially defined function (defined on those terms of `α` that satisfy a predicate `P`) over
a list `l : List α`, given a proof that every element of `l` in fact satisfies `P`.

`O(|l|)`. `List.pmap`, named for “partial map,” is the equivalent of `List.map` for such partial
functions.


## INFORMAL STATEMENT
lem.fps.comps.equiv-mathlib-filtered

\leanhelper  There is an equivalence between compositions of $n$ into $k$ parts and the subtype of Mathlib compositions of $n$ having length $k$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.comps
def.fps.comps

\textbf{(a)} An \emph{(integer) composition} means a (finite) tuple of positive integers. \medskip 

\textbf{(b)} The \emph{size} of an integer composition $\alpha =\left( \alpha _{1},\alpha _{2},\ldots ,\alpha _{m}\right) $ is defined to be the integer $\alpha _{1}+\alpha _{2}+\cdots +\alpha _{m}$. It is written $\left\vert \alpha \right\vert $. \medskip 

\textbf{(c)} The \emph{length} of an integer composition $\alpha =\left( \alpha _{1},\alpha _{2},\ldots ,\alpha _{m}\right) $ is defined to be the integer $m$. It is written $\ell \left( \alpha \right) $. \medskip 

\textbf{(d)} Let $n\in \mathbb {N}$. A \emph{composition of }$n$ means a composition whose size is $n$. \medskip 

\textbf{(e)} Let $n\in \mathbb {N}$ and $k\in \mathbb {N}$. A \emph{composition of }$n$\emph{ into }$k$\emph{ parts} is a composition whose size is $n$ and whose length is $k$.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The target quantifies exactly over `(n k : \u2115)` and gives `AlgebraicCombinatorics.Composition.ofSizeIntoParts n k \u2243 \u2191{c | c.length = k}`. The dependency defines the source as `{ \u03b1 // \u03b1.size = n \u2227 \u03b1.len = k}`, exactly the informal \u201ccompositions of n into k parts.\u201d By the base-library meaning of `Composition n`, the elements filtered on the right are Mathlib compositions of `n`, and `{c | c.length = k}` restricts them exactly to those \u201chaving length k.\u201d `Equiv` supplies the claimed two-sided equivalence, with no added hypotheses or narrowed quantifiers."
}