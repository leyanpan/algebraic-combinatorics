## TARGET AlgebraicCombinatorics.Composition.card_ofSizeIntoParts_pos (theorem) — ELABORATED SIGNATURE
∀ (n k : ℕ),
  0 < n → 0 < k → Fintype.card (AlgebraicCombinatorics.Composition.ofSizeIntoParts n k) = (n - 1).choose (k - 1)

Docstring: **Theorem thm.fps.comps.num-comps-n-k**:
For `n > 0` and `k > 0`, the number of compositions of `n` into `k` parts is `Nat.choose (n-1) (k-1)`.

Note: The source text states this as `C(n-1, n-k) = C(n-1, k-1)` for `n > 0`, but
`C(n-1, n-k)` uses integer binomial coefficients where `C(-1, -k) = 0` for `k > 0`.
In Lean's `Nat.choose` with truncating subtraction, `Nat.choose (0-1) (0-k) = Nat.choose 0 0 = 1`,
which is incorrect for the case `n = 0, k > 0`. Additionally, when `n > 0` and `k = 0`,
the formula `Nat.choose (n-1) (k-1) = Nat.choose (n-1) 0 = 1`, but there are no compositions
of `n > 0` into 0 parts (the count should be 0).

Therefore, we require both `n > 0` and `k > 0`, and handle edge cases separately.


## TARGET AlgebraicCombinatorics.Composition.card_ofSizeIntoParts_zero (theorem) — ELABORATED SIGNATURE
∀ (k : ℕ), Fintype.card (AlgebraicCombinatorics.Composition.ofSizeIntoParts 0 k) = if k = 0 then 1 else 0

Docstring: For `n = 0`, the only composition is the empty one (into 0 parts).
There are no compositions of 0 into k > 0 parts (since all parts must be positive).


## TARGET AlgebraicCombinatorics.Composition.card_ofSizeIntoParts_k_zero (theorem) — ELABORATED SIGNATURE
∀ (n : ℕ), 0 < n → Fintype.card (AlgebraicCombinatorics.Composition.ofSizeIntoParts n 0) = 0

Docstring: For `n > 0` and `k = 0`, there are no compositions (since compositions have positive parts,
and the sum of zero positive integers is 0, not `n`).


## PROJECT DEPENDENCY AlgebraicCombinatorics.Composition.ofSizeIntoParts (def)
ℕ → ℕ → Type

Body:
fun n k => { α // α.size = n ∧ α.len = k }

Docstring: A composition of `n` into `k` parts is a composition with size `n` and length `k`.

(Definition def.fps.comps, part (e))


## PROJECT DEPENDENCY AlgebraicCombinatorics.Composition.fintypeOfSizeIntoParts (def)
(n k : ℕ) → Fintype (AlgebraicCombinatorics.Composition.ofSizeIntoParts n k)

Body:
fun n k => Fintype.ofEquiv (↑{c | c.length = k}) (AlgebraicCombinatorics.Composition.equivMathlibFiltered n k).symm

Docstring: The set of all compositions of `n` into `k` parts is finite.


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


## PROJECT DEPENDENCY AlgebraicCombinatorics.Composition.equivMathlibFiltered (def)
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

## BASE-LIBRARY REF Nat.choose
ℕ → ℕ → ℕ

Docstring: `choose n k` is the number of `k`-element subsets in an `n`-element set. Also known as binomial
coefficients. For the fact that this is the number of `k`-element-subsets of an `n`-element
set, see `Finset.card_powersetCard`. 

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

## BASE-LIBRARY REF ite
{α : Sort u} → (c : Prop) → [h : Decidable c] → α → α → α

Docstring: `if c then t else e` is notation for `ite c t e`, "if-then-else", which decides to
return `t` or `e` depending on whether `c` is true or false. The explicit argument
`c : Prop` does not have any actual computational content, but there is an additional
`[Decidable c]` argument synthesized by typeclass inference which actually
determines how to evaluate `c` to true or false. Write `if h : c then t else e`
instead for a "dependent if-then-else" `dite`, which allows `t`/`e` to use the fact
that `c` is true/false.


## BASE-LIBRARY REF instDecidableEqNat
DecidableEq ℕ

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

## BASE-LIBRARY REF And
Prop → Prop → Prop

Docstring: `And a b`, or `a ∧ b`, is the conjunction of propositions. It can be
constructed and destructed like a pair: if `ha : a` and `hb : b` then
`⟨ha, hb⟩ : a ∧ b`, and if `h : a ∧ b` then `h.left : a` and `h.right : b`.


Conventions for notations in identifiers:

 * The recommended spelling of `∧` in identifiers is `and`.

 * The recommended spelling of `/\` in identifiers is `and` (prefer `∧` over `/\`).

## BASE-LIBRARY REF Fintype
Type u_4 → Type u_4

Docstring: `Fintype α` means that `α` is finite, i.e. there are only
finitely many distinct elements of type `α`. The evidence of this
is a finset `elems` (a list up to permutation without duplicates),
together with a proof that everything of type `α` is in the list. 

## BASE-LIBRARY REF Fintype.ofEquiv
{β : Type u_2} → (α : Type u_4) → [Fintype α] → α ≃ β → Fintype β

Docstring: If `f : α ≃ β` and `α` is a fintype, then `β` is also a fintype. 

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

## BASE-LIBRARY REF Composition.length
{n : ℕ} → Composition n → ℕ

Docstring: The length of a composition, i.e., the number of blocks in the composition. 

## BASE-LIBRARY REF Subtype.fintype
{α : Type u_1} → (p : α → Prop) → [DecidablePred p] → [Fintype α] → Fintype { x // p x }

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

## BASE-LIBRARY REF Set.decidableSetOf
{α : Type u} → (a : α) → (p : α → Prop) → [Decidable (p a)] → Decidable (a ∈ {a | p a})

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

## BASE-LIBRARY REF List.length
{α : Type u_1} → List α → ℕ

Docstring: The length of a list.

This function is overridden in the compiler to `lengthTR`, which uses constant stack space.

Examples:
* `([] : List String).length = 0`
* `["green", "brown"].length = 2`


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

## BASE-LIBRARY REF Subtype.mk
{α : Sort u} → {p : α → Prop} → (val : α) → p val → Subtype p

## BASE-LIBRARY REF Composition.mk
{n : ℕ} → (blocks : List ℕ) → (∀ {i : ℕ}, i ∈ blocks → 0 < i) → blocks.sum = n → Composition n

## BASE-LIBRARY REF Composition.blocks
{n : ℕ} → Composition n → List ℕ

Docstring: List of positive integers summing to `n` 

## BASE-LIBRARY REF Composition.blocks_pos
∀ {n : ℕ} (self : Composition n) {i : ℕ}, i ∈ self.blocks → 0 < i

Docstring: Proof of positivity for `blocks` 

## BASE-LIBRARY REF List.instMembership
{α : Type u} → Membership α (List α)

## BASE-LIBRARY REF List.pmap
{α : Type u_1} → {β : Type u_2} → {P : α → Prop} → ((a : α) → P a → β) → (l : List α) → (∀ a ∈ l, P a) → List β

Docstring: Maps a partially defined function (defined on those terms of `α` that satisfy a predicate `P`) over
a list `l : List α`, given a proof that every element of `l` in fact satisfies `P`.

`O(|l|)`. `List.pmap`, named for “partial map,” is the equivalent of `List.map` for such partial
functions.


## INFORMAL STATEMENT
thm.fps.comps.num-comps-n-k

Let $n,k\in \mathbb {N}$. Then, the \#  of compositions of $n$ into $k$ parts is

\[  \binom {n-1}{n-k}=\begin{cases}  \binom {n-1}{k-1}, &  \text{if }n>0;\\ \delta _{k,0}, &  \text{if }n=0. \end{cases}  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-conv.det.k
conv.det.K

For the rest of this section, we fix a commutative ring $K$. In most examples, $K$ will be $\mathbb {Z}$ or $\mathbb {Q}$ or a polynomial ring.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.alg.commring
def.alg.commring

A \emph{commutative ring} means a set $K$ equipped with three maps

\begin{align*}  \oplus &  :K\times K\rightarrow K,\\ \ominus &  :K\times K\rightarrow K,\\ \odot &  :K\times K\rightarrow K \end{align*}

 and two elements $\mathbf{0}\in K$ and $\mathbf{1}\in K$ satisfying the following axioms: 

\begin{enumerate} \item \emph{Commutativity of addition:} We have $a\oplus b=b\oplus a$ for all $a,b\in K$. 

\item \emph{Associativity of addition:} We have $a\oplus \left( b\oplus c\right) =\left( a\oplus b\right) \oplus c$ for all $a,b,c\in K$. 

\item \emph{Neutrality of zero:} We have $a\oplus \mathbf{0}=\mathbf{0}\oplus a=a$ for all $a\in K$. 

\item \emph{Subtraction undoes addition:} Let $a,b,c\in K$. We have $a\oplus b=c$ if and only if $a=c\ominus b$. 

\item \emph{Commutativity of multiplication:} We have $a\odot b=b\odot a$ for all $a,b\in K$. 

\item \emph{Associativity of multiplication:} We have $a\odot \left( b\odot c\right) =\left( a\odot b\right) \odot c$ for all $a,b,c\in K$. 

\item \emph{Distributivity:} We have

\[  a\odot \left( b\oplus c\right) =\left( a\odot b\right) \oplus \left( a\odot c\right) \  \  \  \  \  \  \  \  \  \  \text{and}\  \  \  \  \  \  \  \  \  \  \left( a\oplus b\right) \odot c=\left( a\odot c\right) \oplus \left( b\odot c\right)  \]

 for all $a,b,c\in K$. 

\item \emph{Neutrality of one:} We have $a\odot \mathbf{1}=\mathbf{1}\odot a=a$ for all $a\in K$. 

\item \emph{Annihilation:} We have $a\odot \mathbf{0}=\mathbf{0}\odot a=\mathbf{0}$ for all $a\in K$. 

\end{enumerate}

The operations $\oplus $, $\ominus $ and $\odot $ are called the \emph{addition}, the \emph{subtraction} and the \emph{multiplication} of the ring $K$. When confusion is unlikely, we will denote these three operations $\oplus $, $\ominus $ and $\odot $ by $+$, $-$ and $\cdot $, respectively, and we will abbreviate $a\odot b=a\cdot b$ by $ab$. 

The elements $\mathbf{0}$ and $\mathbf{1}$ are called the \emph{zero} and the \emph{unity} (or the \emph{one}) of the ring $K$. We will simply call these elements $0$ and $1$ when confusion with the corresponding numbers is unlikely. 

We will use \emph{PEMDAS conventions} for the three operations $\oplus $, $\ominus $ and $\odot $. These imply that the operation $\odot $ has higher precedence than $\oplus $ and $\ominus $, while the operations $\oplus $ and $\ominus $ are left-associative.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.kron-delta
def.kron-delta

If $i$ and $j$ are any objects, then $\delta _{i,j}$ means the element 

\[  \delta _{i,j} = \begin{cases}  1, &  \text{if } i = j; \\ 0, &  \text{if } i \neq j \end{cases}  \]

 of $K$.

## VERDICT
{
  "verdict": "faithful",
  "justification": "Taken together, the three declarations are an exhaustive case split of \u201cLet n,k\u2208\u2115.\u201d For `0 < n` and `0 < k`, the first target gives exactly `Fintype.card ... = (n - 1).choose (k - 1)`. The omitted `k = 0` case is supplied by `\u2200 (n : \u2115), 0 < n \u2192 ... n 0 = 0`, which is the intended value of the informal `binom (n-1) (k-1)` when the lower index is `-1`. The `n = 0` branch is supplied by `\u2200 (k : \u2115), ... = if k = 0 then 1 else 0`, exactly the natural-number form of `\u03b4_{k,0}`. Thus the positivity hypotheses in the first target do not weaken the package: the excluded cases are covered by the other two targets. The dependency `ofSizeIntoParts n k := { \u03b1 // \u03b1.size = n \u2227 \u03b1.len = k }`, with `Composition := List \u2115+`, `size` the sum, and `len` the list length, matches compositions of `n` into `k` positive parts. The source\u2019s first binomial expression uses indices that may be negative and therefore cannot be written literally using `Nat.choose` and truncating subtraction; the case split states its equivalent cardinal values and avoids the false truncated-Nat interpretation."
}