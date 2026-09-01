## TARGET AlgebraicCombinatorics.WeakComposition.toComposition (def) — ELABORATED SIGNATURE
(n k : ℕ) →
  AlgebraicCombinatorics.WeakComposition.ofSizeIntoParts n k ≃
    AlgebraicCombinatorics.Composition.ofSizeIntoParts (n + k) k

Body:
fun n k =>
  {
    toFun := fun x =>
      match x with
      | ⟨lst, ⋯⟩ => ⟨List.map (fun a => ⟨a + 1, ⋯⟩) lst, ⋯⟩,
    invFun := fun x =>
      match x with
      | ⟨lst, ⋯⟩ => ⟨List.map (fun b => ↑b - 1) lst, ⋯⟩,
    left_inv := ⋯, right_inv := ⋯ }

Docstring: Bijection between weak compositions of `n` into `k` parts and compositions of `n+k` into `k` parts.
Adding 1 to each entry of a weak composition gives a composition.

This is the key bijection used in the proof of Theorem thm.fps.comps.num-wcomps-n-k.


## PROJECT DEPENDENCY AlgebraicCombinatorics.WeakComposition.ofSizeIntoParts (def)
ℕ → ℕ → Type

Body:
fun n k => { α // α.size = n ∧ α.len = k }

Docstring: A weak composition of `n` into `k` parts is a tuple of `k` nonnegative integers summing to `n`.

(Definition def.fps.wcomps, part (e))


## PROJECT DEPENDENCY AlgebraicCombinatorics.Composition.ofSizeIntoParts (def)
ℕ → ℕ → Type

Body:
fun n k => { α // α.size = n ∧ α.len = k }

Docstring: A composition of `n` into `k` parts is a composition with size `n` and length `k`.

(Definition def.fps.comps, part (e))


## PROJECT DEPENDENCY AlgebraicCombinatorics.WeakComposition.ofSizeIntoParts_equiv (def)
(n k : ℕ) →
  AlgebraicCombinatorics.WeakComposition.ofSizeIntoParts n k ≃
    AlgebraicCombinatorics.WeakComposition.ofSizeIntoParts' n k

Body:
fun n k =>
  {
    toFun := fun x =>
      match x with
      | ⟨α, ⋯⟩ => ⟨α.toFun k hlen, ⋯⟩,
    invFun := fun x =>
      match x with
      | ⟨f, hsum⟩ => ⟨AlgebraicCombinatorics.WeakComposition.ofFun f, ⋯⟩,
    left_inv := ⋯, right_inv := ⋯ }

Docstring: The two representations (list-based and function-based) are equivalent.
The forward direction converts a list `[a₀, a₁, ..., aₖ₋₁]` to the function `i ↦ aᵢ`.
The backward direction converts a function `f : Fin k → ℕ` to the list `[f(0), f(1), ..., f(k-1)]`.


## PROJECT DEPENDENCY AlgebraicCombinatorics.WeakComposition (def)
Type

Body:
List ℕ

Docstring: A weak composition is a finite tuple of nonnegative integers.

(Definition def.fps.wcomps, part (a))


## PROJECT DEPENDENCY AlgebraicCombinatorics.WeakComposition.size (def)
AlgebraicCombinatorics.WeakComposition → ℕ

Body:
fun α => List.sum α

Docstring: The size of a weak composition is the sum of its entries.

(Definition def.fps.wcomps, part (b))


## PROJECT DEPENDENCY AlgebraicCombinatorics.WeakComposition.len (def)
AlgebraicCombinatorics.WeakComposition → ℕ

Body:
fun α => List.length α

Docstring: The length of a weak composition is the number of parts.
(We use `len` to avoid conflict with `List.length`.)

(Definition def.fps.wcomps, part (c))


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


## PROJECT DEPENDENCY AlgebraicCombinatorics.WeakComposition.ofSizeIntoParts' (def)
ℕ → ℕ → Type

Body:
fun n k => { f // ∑ i, f i = n }

Docstring: Alternative representation of weak compositions as functions `Fin k → ℕ`.
This is equivalent to `ofSizeIntoParts n k` but easier to work with for cardinality proofs.


## PROJECT DEPENDENCY AlgebraicCombinatorics.WeakComposition.toFun (def)
(α : AlgebraicCombinatorics.WeakComposition) → (k : ℕ) → α.len = k → Fin k → ℕ

Body:
fun α k hlen i => List.get α (Fin.cast ⋯ i)

Docstring: Convert a list-based weak composition to a function-based one. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.WeakComposition.ofSizeIntoParts'.toSym (def)
(n k : ℕ) → AlgebraicCombinatorics.WeakComposition.ofSizeIntoParts' n k → Sym (Fin k) n

Body:
fun n k x =>
  match x with
  | ⟨f, hf⟩ => ⟨∑ i, Multiset.replicate (f i) i, ⋯⟩

Docstring: Bijection from `ofSizeIntoParts' n k` to `Sym (Fin k) n`. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.WeakComposition.ofFun (def)
{k : ℕ} → (Fin k → ℕ) → AlgebraicCombinatorics.WeakComposition

Body:
fun {k} f => List.ofFn f

Docstring: Convert a function to a list. 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF Equiv
Sort u_1 → Sort u_2 → Sort (max (max 1 u_1) u_2)

Docstring: `α ≃ β` is the type of functions from `α → β` with a two-sided inverse. 

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

## BASE-LIBRARY REF Equiv.mk
{α : Sort u_1} →
  {β : Sort u_2} →
    (toFun : α → β) →
      (invFun : β → α) →
        autoParam (Function.LeftInverse invFun toFun) Equiv.left_inv._autoParam →
          autoParam (Function.RightInverse invFun toFun) Equiv.right_inv._autoParam → α ≃ β

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

## BASE-LIBRARY REF Subtype.mk
{α : Sort u} → {p : α → Prop} → (val : α) → p val → Subtype p

## BASE-LIBRARY REF And
Prop → Prop → Prop

Docstring: `And a b`, or `a ∧ b`, is the conjunction of propositions. It can be
constructed and destructed like a pair: if `ha : a` and `hb : b` then
`⟨ha, hb⟩ : a ∧ b`, and if `h : a ∧ b` then `h.left : a` and `h.right : b`.


Conventions for notations in identifiers:

 * The recommended spelling of `∧` in identifiers is `and`.

 * The recommended spelling of `/\` in identifiers is `and` (prefer `∧` over `/\`).

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

## BASE-LIBRARY REF Nat.succ_pos
∀ (n : ℕ), 0 < n.succ

## BASE-LIBRARY REF HSub.hSub
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HSub α β γ] → α → β → γ

Docstring: `a - b` computes the difference of `a` and `b`.
The meaning of this notation is type-dependent.
* For natural numbers, this operator saturates at 0: `a - b = 0` when `a ≤ b`. 

Conventions for notations in identifiers:

 * The recommended spelling of `-` in identifiers is `sub` (when used as a binary operator).

## BASE-LIBRARY REF instHSub
{α : Type u_1} → [Sub α] → HSub α α α

## BASE-LIBRARY REF instSubNat
Sub ℕ

## BASE-LIBRARY REF PNat.val
ℕ+ → ℕ

Docstring: The underlying natural number 

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

## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


## BASE-LIBRARY REF Finset.sum
{ι : Type u_1} → {M : Type u_3} → [AddCommMonoid M] → Finset ι → (ι → M) → M

Docstring: `∑ x ∈ s, f x` is the sum of `f x` as `x` ranges over the elements
of the finite set `s`.

When the index type is a `Fintype`, the notation `∑ x, f x`, is a shorthand for
`∑ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF Nat.instAddCommMonoid
AddCommMonoid ℕ

## BASE-LIBRARY REF Finset.univ
{α : Type u_1} → [Fintype α] → Finset α

Docstring: `univ` is the universal finite set of type `Finset α` implied from
the assumption `Fintype α`. 

## BASE-LIBRARY REF Fin.fintype
(n : ℕ) → Fintype (Fin n)

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


## BASE-LIBRARY REF List.sum
{α : Type u_1} → [Add α] → [Zero α] → List α → α

Docstring: Computes the sum of the elements of a list.

Examples:
* `[a, b, c].sum = a + (b + (c + 0))`
* `[1, 2, 5].sum = 8`


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


## BASE-LIBRARY REF List.get
{α : Type u} → (as : List α) → Fin as.length → α

Docstring: Returns the element at the provided index, counting from `0`.

In other words, for `i : Fin as.length`, `as.get i` returns the `i`'th element of the list `as`.
Because the index is a `Fin` bounded by the list's length, the index will never be out of bounds.

Examples:
 * `["spring", "summer", "fall", "winter"].get (2 : Fin 4) = "fall"`
 * `["spring", "summer", "fall", "winter"].get (0 : Fin 4) = "spring"`


## BASE-LIBRARY REF Fin.cast
{n m : ℕ} → n = m → Fin n → Fin m

Docstring: Uses a proof that two bounds are equal to allow a value bounded by one to be used with the other.

In other words, when `eq : n = m`, `Fin.cast eq i` converts `i : Fin n` into a `Fin m`.


## BASE-LIBRARY REF Sym
Type u_1 → ℕ → Type (max 0 u_1)

Docstring: The nth symmetric power is n-tuples up to permutation.  We define it
as a subtype of `Multiset` since these are well developed in the
library.  We also give a definition `Sym.sym'` in terms of vectors, and we
show these are equivalent in `Sym.symEquivSym'`.


## BASE-LIBRARY REF Multiset
Type u → Type u

Docstring: `Multiset α` is the quotient of `List α` by list permutation. The result
is a type of finite sets with duplicates allowed. 

## BASE-LIBRARY REF Multiset.card
{α : Type u_1} → Multiset α → ℕ

Docstring: The cardinality of a multiset is the sum of the multiplicities
of all its elements, or simply the length of the underlying list. 

## BASE-LIBRARY REF AddCancelCommMonoid.toAddCommMonoid
{M : Type u} → [self : AddCancelCommMonoid M] → AddCommMonoid M

## BASE-LIBRARY REF Multiset.instAddCancelCommMonoid
{α : Type u_1} → AddCancelCommMonoid (Multiset α)

## BASE-LIBRARY REF Multiset.replicate
{α : Type u_1} → ℕ → α → Multiset α

Docstring: `replicate n a` is the multiset containing only `a` with multiplicity `n`. 

## BASE-LIBRARY REF List.ofFn
{α : Type u_1} → {n : ℕ} → (Fin n → α) → List α

Docstring: Creates a list by applying `f` to each potential index in order, starting at `0`.

Examples:
* `List.ofFn (n := 3) toString = ["0", "1", "2"]`
* `List.ofFn (fun i => #["red", "green", "blue"].get i.val i.isLt) = ["red", "green", "blue"]`


## INFORMAL STATEMENT
lem.fps.wcomps.to-composition

\leanhelper  There is a bijection between weak compositions of $n$ into $k$ parts and compositions of $n+k$ into $k$ parts, defined by adding $1$ to each entry.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.comps
def.fps.comps

\textbf{(a)} An \emph{(integer) composition} means a (finite) tuple of positive integers. \medskip 

\textbf{(b)} The \emph{size} of an integer composition $\alpha =\left( \alpha _{1},\alpha _{2},\ldots ,\alpha _{m}\right) $ is defined to be the integer $\alpha _{1}+\alpha _{2}+\cdots +\alpha _{m}$. It is written $\left\vert \alpha \right\vert $. \medskip 

\textbf{(c)} The \emph{length} of an integer composition $\alpha =\left( \alpha _{1},\alpha _{2},\ldots ,\alpha _{m}\right) $ is defined to be the integer $m$. It is written $\ell \left( \alpha \right) $. \medskip 

\textbf{(d)} Let $n\in \mathbb {N}$. A \emph{composition of }$n$ means a composition whose size is $n$. \medskip 

\textbf{(e)} Let $n\in \mathbb {N}$ and $k\in \mathbb {N}$. A \emph{composition of }$n$\emph{ into }$k$\emph{ parts} is a composition whose size is $n$ and whose length is $k$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.wcomps
def.fps.wcomps

\textbf{(a)} An \emph{(integer) weak composition} means a (finite) tuple of nonnegative integers. \medskip 

\textbf{(b)} The \emph{size} of a weak composition $\alpha =\left( \alpha _{1},\alpha _{2},\ldots ,\alpha _{m}\right) $ is defined to be the integer $\alpha _{1}+\alpha _{2}+\cdots +\alpha _{m}$. It is written $\left\vert \alpha \right\vert $. \medskip 

\textbf{(c)} The \emph{length} of a weak composition $\alpha =\left( \alpha _{1},\alpha _{2},\ldots ,\alpha _{m}\right) $ is defined to be the integer $m$. It is written $\ell \left( \alpha \right) $. \medskip 

\textbf{(d)} Let $n\in \mathbb {N}$. A \emph{weak composition of }$n$ means a weak composition whose size is $n$. \medskip 

\textbf{(e)} Let $n\in \mathbb {N}$ and $k\in \mathbb {N}$. A \emph{weak composition of }$n$\emph{ into }$k$\emph{ parts} is a weak composition whose size is $n$ and whose length is $k$.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The target quantifies over exactly the intended parameters, `(n k : \u2115)`, and constructs an equivalence `WeakComposition.ofSizeIntoParts n k \u2243 Composition.ofSizeIntoParts (n + k) k`. By the dependency bodies, these are precisely tuples of nonnegative integers of size `n` and length `k`, and tuples of positive integers of size `n + k` and length `k`, respectively. Its forward map is explicitly `List.map (fun a => \u27e8a + 1, \u22ef\u27e9)`, so the bijection is \u201cdefined by adding 1 to each entry\u201d exactly as required. The inverse subtracts 1 from each positive entry, and `Equiv` supplies the required two-sided inverse. There are no additional hypotheses or narrowed quantifiers."
}