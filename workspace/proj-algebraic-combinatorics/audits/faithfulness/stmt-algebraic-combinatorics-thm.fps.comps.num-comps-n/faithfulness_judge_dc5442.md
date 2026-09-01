## TARGET AlgebraicCombinatorics.Composition.card_ofSize (theorem) — ELABORATED SIGNATURE
∀ (n : ℕ), Fintype.card (AlgebraicCombinatorics.Composition.ofSize n) = if n = 0 then 1 else 2 ^ (n - 1)

Docstring: **Theorem thm.fps.comps.num-comps-n**:
The number of compositions of `n` is `2^(n-1)` when `n > 0`, and `1` when `n = 0`.

This is proved by establishing an equivalence with Mathlib's `Composition n` and using
`composition_card` from Mathlib.


## TARGET AlgebraicCombinatorics.Composition.card_ofSize_pos (theorem) — ELABORATED SIGNATURE
∀ (n : ℕ), 0 < n → Fintype.card (AlgebraicCombinatorics.Composition.ofSize n) = 2 ^ (n - 1)

Docstring: For `n > 0`, the number of compositions of `n` is `2^(n-1)`.


## PROJECT DEPENDENCY AlgebraicCombinatorics.Composition.ofSize (def)
ℕ → Type

Body:
fun n => { α // α.size = n }

Docstring: A composition of `n` is a composition whose size is `n`.

(Definition def.fps.comps, part (d))


## PROJECT DEPENDENCY AlgebraicCombinatorics.Composition.fintypeOfSize (def)
(n : ℕ) → Fintype (AlgebraicCombinatorics.Composition.ofSize n)

Body:
fun n => Fintype.ofEquiv (Composition n) (AlgebraicCombinatorics.Composition.equivMathlib n).symm

Docstring: The set of all compositions of `n` is finite.


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


## PROJECT DEPENDENCY AlgebraicCombinatorics.Composition.toBlocks (def)
AlgebraicCombinatorics.Composition → List ℕ

Body:
fun α => List.map (fun x => ↑x) α

Docstring: Convert a composition (List ℕ+) to a blocks list (List ℕ) 

## PROJECT DEPENDENCY AlgebraicCombinatorics.Composition.ofBlocks (def)
(blocks : List ℕ) → (∀ {i : ℕ}, i ∈ blocks → 0 < i) → AlgebraicCombinatorics.Composition

Body:
fun blocks hpos => List.pmap (fun i hi => ⟨i, hi⟩) blocks ⋯

Docstring: Convert a blocks list with positivity proof to a composition (List ℕ+) 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


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

## BASE-LIBRARY REF Fintype.card
(α : Type u_4) → [Fintype α] → ℕ

Docstring: `card α` is the number of elements in `α`, defined when `α` is a fintype. 

## BASE-LIBRARY REF ite
{α : Sort u} → (c : Prop) → [h : Decidable c] → α → α → α

Docstring: `if c then t else e` is notation for `ite c t e`, "if-then-else", which decides to
return `t` or `e` depending on whether `c` is true or false. The explicit argument
`c : Prop` does not have any actual computational content, but there is an additional
`[Decidable c]` argument synthesized by typeclass inference which actually
determines how to evaluate `c` to true or false. Write `if h : c then t else e`
instead for a "dependent if-then-else" `dite`, which allows `t`/`e` to use the fact
that `c` is true/false.


## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

## BASE-LIBRARY REF instDecidableEqNat
DecidableEq ℕ

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

## BASE-LIBRARY REF LT.lt
{α : Type u} → [self : LT α] → α → α → Prop

Docstring: The less-than relation: `x < y` 

Conventions for notations in identifiers:

 * The recommended spelling of `<` in identifiers is `lt`.

## BASE-LIBRARY REF instLTNat
LT ℕ

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

## BASE-LIBRARY REF Fintype
Type u_4 → Type u_4

Docstring: `Fintype α` means that `α` is finite, i.e. there are only
finitely many distinct elements of type `α`. The evidence of this
is a finset `elems` (a list up to permutation without duplicates),
together with a proof that everything of type `α` is in the list. 

## BASE-LIBRARY REF Fintype.ofEquiv
{β : Type u_2} → (α : Type u_4) → [Fintype α] → α ≃ β → Fintype β

Docstring: If `f : α ≃ β` and `α` is a fintype, then `β` is also a fintype. 

## BASE-LIBRARY REF Composition
ℕ → Type

Docstring: A composition of `n` is a list of positive integers summing to `n`. 

## BASE-LIBRARY REF compositionFintype
(n : ℕ) → Fintype (Composition n)

## BASE-LIBRARY REF Equiv.symm
{α : Sort u} → {β : Sort v} → α ≃ β → β ≃ α

Docstring: Inverse of an equivalence `e : α ≃ β`. 

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

## BASE-LIBRARY REF Composition.mk
{n : ℕ} → (blocks : List ℕ) → (∀ {i : ℕ}, i ∈ blocks → 0 < i) → blocks.sum = n → Composition n

## BASE-LIBRARY REF Subtype.mk
{α : Sort u} → {p : α → Prop} → (val : α) → p val → Subtype p

## BASE-LIBRARY REF Composition.blocks
{n : ℕ} → Composition n → List ℕ

Docstring: List of positive integers summing to `n` 

## BASE-LIBRARY REF Composition.blocks_pos
∀ {n : ℕ} (self : Composition n) {i : ℕ}, i ∈ self.blocks → 0 < i

Docstring: Proof of positivity for `blocks` 

## BASE-LIBRARY REF Membership.mem
{α : outParam (Type u)} → {γ : Type v} → [self : Membership α γ] → γ → α → Prop

Docstring: The membership relation `a ∈ s : Prop` where `a : α`, `s : γ`. 

Conventions for notations in identifiers:

 * The recommended spelling of `∈` in identifiers is `mem`.

## BASE-LIBRARY REF List.instMembership
{α : Type u} → Membership α (List α)

## BASE-LIBRARY REF List.pmap
{α : Type u_1} → {β : Type u_2} → {P : α → Prop} → ((a : α) → P a → β) → (l : List α) → (∀ a ∈ l, P a) → List β

Docstring: Maps a partially defined function (defined on those terms of `α` that satisfy a predicate `P`) over
a list `l : List α`, given a proof that every element of `l` in fact satisfies `P`.

`O(|l|)`. `List.pmap`, named for “partial map,” is the equivalent of `List.map` for such partial
functions.


## INFORMAL STATEMENT
thm.fps.comps.num-comps-n

Let $n\in \mathbb {N}$. Then, the \#  of compositions of $n$ is

\[ \begin{cases}  2^{n-1}, &  \text{if }n>0;\\ 1, &  \text{if }n=0. \end{cases}  \]

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
  "justification": "The main target quantifies exactly as required, `\u2200 (n : \u2115)`, and states `Fintype.card (AlgebraicCombinatorics.Composition.ofSize n) = if n = 0 then 1 else 2 ^ (n - 1)`, which is equivalent to the blueprint\u2019s two cases: `2^{n-1}` if `n>0` and `1` if `n=0`. The counted type is faithful to the informal definition: `Composition` is `List \u2115+`, representing finite tuples of positive integers; `size` is the sum of their underlying naturals; and `ofSize n` is `{ \u03b1 // \u03b1.size = n }`. In particular, the empty list supplies the unique composition of zero. The auxiliary target `card_ofSize_pos`, with binders `\u2200 (n : \u2115), 0 < n \u2192 ...`, faithfully states the positive-case specialization; the complete piecewise blueprint theorem is already supplied by `card_ofSize`."
}