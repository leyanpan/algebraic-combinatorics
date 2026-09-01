## TARGET DominoBridge.toDominoZ_cover (theorem) — ELABORATED SIGNATURE
∀ {n m : ℕ} (T : DominoTilings.DominoTiling n m),
  ⋃ d ∈ DominoBridge.dominoFinsetToSet T.dominos, d.toShape = DominoTilingsZ.Rectangle n m

Docstring: Converting a DominoTiling preserves the covering property. 

## PROJECT DEPENDENCY DominoTilings.DominoTiling (inductive)
ℕ → ℕ → Type

Body:
DominoTilings.DominoTiling.mk : {n m : ℕ} →
  (dominos : Finset DominoTilings.Domino) →
    (∀ d ∈ dominos, d.cells ⊆ DominoTilings.Rectangle n m) →
      dominos.biUnion DominoTilings.Domino.cells = DominoTilings.Rectangle n m →
        (∀ d₁ ∈ dominos, ∀ d₂ ∈ dominos, d₁ ≠ d₂ → Disjoint d₁.cells d₂.cells) → DominoTilings.DominoTiling n m

Docstring: A domino tiling of a rectangle is a finite set of dominos such that:
1. Each domino's cells are within the rectangle
2. The dominos partition the rectangle (cover all cells exactly once) 

## PROJECT DEPENDENCY DominoTilingsZ.Domino (inductive)
Type

Body:
DominoTilingsZ.Domino.horizontal : ℤ → ℤ → DominoTilingsZ.Domino
DominoTilingsZ.Domino.vertical : ℤ → ℤ → DominoTilingsZ.Domino

Docstring: A domino is either horizontal or vertical (Definition \ref{def.domino.shapes-and-tilings}(c)) 

## PROJECT DEPENDENCY DominoBridge.dominoFinsetToSet (def)
Finset DominoTilings.Domino → Set DominoTilingsZ.Domino

Body:
fun ds => {x | ∃ d ∈ ds, DominoBridge.toDominoZ d = x}

Docstring: Convert a Finset of DominoTilings.Domino to a Set of DominoTilingsZ.Domino. 

## PROJECT DEPENDENCY DominoTilings.DominoTiling.dominos (def)
{n m : ℕ} → DominoTilings.DominoTiling n m → Finset DominoTilings.Domino

Body:
fun n m self => self.1

Docstring: The set of dominos in the tiling 

## PROJECT DEPENDENCY DominoTilingsZ.Domino.toShape (def)
DominoTilingsZ.Domino → DominoTilingsZ.Shape

Body:
fun x =>
  match x with
  | DominoTilingsZ.Domino.horizontal i j => {(i, j), (i + 1, j)}
  | DominoTilingsZ.Domino.vertical i j => {(i, j), (i, j + 1)}

Docstring: The cells covered by a domino 

## PROJECT DEPENDENCY DominoTilingsZ.Rectangle (def)
ℕ → ℕ → DominoTilingsZ.Shape

Body:
fun n m => {p | 1 ≤ p.1 ∧ p.1 ≤ ↑n ∧ 1 ≤ p.2 ∧ p.2 ≤ ↑m}

Docstring: The n × m rectangle (Definition \ref{def.domino.shapes-and-tilings}(b)) 

## PROJECT DEPENDENCY DominoTilings.Domino (inductive)
Type

Body:
DominoTilings.Domino.mk : (cell1 cell2 : DominoTilings.Cell) →
  cell1 ≠ cell2 →
    cell1.1 = cell2.1 ∧ (cell1.2 + 1 = cell2.2 ∨ cell2.2 + 1 = cell1.2) ∨
        cell1.2 = cell2.2 ∧ (cell1.1 + 1 = cell2.1 ∨ cell2.1 + 1 = cell1.1) →
      DominoTilings.Domino

Docstring: A domino is a pair of adjacent cells, either horizontal or vertical. 

## PROJECT DEPENDENCY DominoTilings.Cell (def)
Type

Body:
ℕ × ℕ

Docstring: A cell in a rectangle, represented as a pair (column, row) with 1-indexing.
Column numbers go from 1 to n (left to right).
Row numbers go from 1 to m (bottom to top). 

## PROJECT DEPENDENCY DominoTilings.Domino.cells (def)
DominoTilings.Domino → Finset DominoTilings.Cell

Body:
fun d => {d.cell1, d.cell2}

Docstring: The set of cells covered by a domino. 

## PROJECT DEPENDENCY DominoTilings.Rectangle (def)
ℕ → ℕ → Finset DominoTilings.Cell

Body:
fun n m =>
  Finset.map
    {
      toFun := fun x =>
        match x with
        | (x, y) => (x + 1, y + 1),
      inj' := DominoTilings.Rectangle._proof_1 }
    (Finset.range n ×ˢ Finset.range m)

Docstring: The rectangle R_{n,m} is the set of cells {(x, y) : 1 ≤ x ≤ n, 1 ≤ y ≤ m}. 

## PROJECT DEPENDENCY DominoBridge.toDominoZ (def)
DominoTilings.Domino → DominoTilingsZ.Domino

Body:
fun d =>
  if d.isHorizontal then
    have minCol := min d.cell1.1 d.cell2.1;
    DominoTilingsZ.Domino.horizontal ↑minCol ↑d.cell1.2
  else
    have minRow := min d.cell1.2 d.cell2.2;
    DominoTilingsZ.Domino.vertical ↑d.cell1.1 ↑minRow

Docstring: Convert a DominoTilings.Domino to DominoTilingsZ.Domino.

The conversion uses the minimum coordinate as the anchor point:
- A horizontal domino becomes DominoTilingsZ.Domino.horizontal (min col) row
- A vertical domino becomes DominoTilingsZ.Domino.vertical col (min row) 

## PROJECT DEPENDENCY DominoTilingsZ.Shape (def)
Type

Body:
Set (ℤ × ℤ)

Docstring: A shape is a subset of ℤ² (Definition \ref{def.domino.shapes-and-tilings}(a)) 

## PROJECT DEPENDENCY DominoTilings.Domino.cell1 (def)
DominoTilings.Domino → DominoTilings.Cell

Body:
fun self => self.1

Docstring: The first cell of the domino 

## PROJECT DEPENDENCY DominoTilings.Domino.cell2 (def)
DominoTilings.Domino → DominoTilings.Cell

Body:
fun self => self.2

Docstring: The second cell of the domino 

## PROJECT DEPENDENCY DominoTilings.Domino.isHorizontal (def)
DominoTilings.Domino → Prop

Body:
fun d => d.cell1.2 = d.cell2.2

Docstring: A domino is horizontal if both cells are in the same row. 

## PROJECT DEPENDENCY DominoTilings.Domino.instDecidablePredIsHorizontal (def)
DecidablePred DominoTilings.Domino.isHorizontal

Body:
fun d => inferInstanceAs (Decidable (d.cell1.2 = d.cell2.2))

## PROJECT DEPENDENCY DominoTilingsZ.Domino.horizontal (constructor)
ℤ → ℤ → DominoTilingsZ.Domino

## PROJECT DEPENDENCY DominoTilingsZ.Domino.vertical (constructor)
ℤ → ℤ → DominoTilingsZ.Domino

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

## BASE-LIBRARY REF Set
Type u → Type u

Docstring: A set is a collection of elements of some type `α`.

Although `Set` is defined as `α → Prop`, this is an implementation detail which should not be
relied on. Instead, `setOf` and membership of a set (`∈`) should be used to convert between sets
and predicates.


## BASE-LIBRARY REF Prod
Type u → Type v → Type (max u v)

Docstring: The product type, usually written `α × β`. Product types are also called pair or tuple types.
Elements of this type are pairs in which the first element is an `α` and the second element is a
`β`.

Products nest to the right, so `(x, y, z) : α × β × γ` is equivalent to `(x, (y, z)) : α × (β × γ)`.


Conventions for notations in identifiers:

 * The recommended spelling of `×` in identifiers is `Prod`.

## BASE-LIBRARY REF Int
Type

Docstring: The integers.

This type is special-cased by the compiler and overridden with an efficient implementation. The
runtime has a special representation for `Int` that stores “small” signed numbers directly, while
larger numbers use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)). A “small number” is an integer that can be encoded with one fewer bits
than the platform's pointer size (i.e. 63 bits on 64-bit architectures and 31 bits on 32-bit
architectures).


## BASE-LIBRARY REF Set.iUnion
{α : Type u} → {ι : Sort v} → (ι → Set α) → Set α

Docstring: Indexed union of a family of sets 

## BASE-LIBRARY REF Membership.mem
{α : outParam (Type u)} → {γ : Type v} → [self : Membership α γ] → γ → α → Prop

Docstring: The membership relation `a ∈ s : Prop` where `a : α`, `s : γ`. 

Conventions for notations in identifiers:

 * The recommended spelling of `∈` in identifiers is `mem`.

## BASE-LIBRARY REF Set.instMembership
{α : Type u} → Membership α (Set α)

## BASE-LIBRARY REF Finset
Type u_4 → Type u_4

Docstring: `Finset α` is the type of finite sets of elements of `α`. It is implemented
as a multiset (a list up to permutation) which has no duplicate elements. 

## BASE-LIBRARY REF Finset.instMembership
{α : Type u_1} → Membership α (Finset α)

## BASE-LIBRARY REF HasSubset.Subset
{α : Type u} → [self : HasSubset α] → α → α → Prop

Docstring: Subset relation: `a ⊆ b`  

Conventions for notations in identifiers:

 * The recommended spelling of `⊆` in identifiers is `subset`.

## BASE-LIBRARY REF Finset.instHasSubset
{α : Type u_1} → HasSubset (Finset α)

## BASE-LIBRARY REF Finset.biUnion
{α : Type u_1} → {β : Type u_2} → [DecidableEq β] → Finset α → (α → Finset β) → Finset β

Docstring: `Finset.biUnion s t` is the union of `t a` over `a ∈ s`.

(This was formerly `bind` due to the monad structure on types with `DecidableEq`.) 

## BASE-LIBRARY REF instDecidableEqProd
{α : Type u_1} → {β : Type u_2} → [DecidableEq α] → [DecidableEq β] → DecidableEq (α × β)

## BASE-LIBRARY REF instDecidableEqNat
DecidableEq ℕ

## BASE-LIBRARY REF Ne
{α : Sort u} → α → α → Prop

Docstring: `a ≠ b`, or `Ne a b` is defined as `¬ (a = b)` or `a = b → False`,
and asserts that `a` and `b` are not equal.


Conventions for notations in identifiers:

 * The recommended spelling of `≠` in identifiers is `ne`.

## BASE-LIBRARY REF Disjoint
{α : Type u_1} → [inst : PartialOrder α] → [OrderBot α] → α → α → Prop

Docstring: Two elements of a lattice are disjoint if their inf is the bottom element.
  (This generalizes disjoint sets, viewed as members of the subset lattice.)

Note that we define this without reference to `⊓`, as this allows us to talk about orders where
the infimum is not unique, or where implementing `Inf` would require additional `Decidable`
arguments. 

## BASE-LIBRARY REF Finset.partialOrder
{α : Type u_1} → PartialOrder (Finset α)

## BASE-LIBRARY REF Finset.instOrderBot
{α : Type u_1} → OrderBot (Finset α)

## BASE-LIBRARY REF setOf
{α : Type u} → (α → Prop) → Set α

Docstring: Turn a predicate `p : α → Prop` into a set, also written as `{x | p x}` 

## BASE-LIBRARY REF Exists
{α : Sort u} → (α → Prop) → Prop

Docstring: Existential quantification. If `p : α → Prop` is a predicate, then `∃ x : α, p x`
asserts that there is some `x` of type `α` such that `p x` holds.
To create an existential proof, use the `exists` tactic,
or the anonymous constructor notation `⟨x, h⟩`.
To unpack an existential, use `cases h` where `h` is a proof of `∃ x : α, p x`,
or `let ⟨x, hx⟩ := h` where `.

Because Lean has proof irrelevance, any two proofs of an existential are
definitionally equal. One consequence of this is that it is impossible to recover the
witness of an existential from the mere fact of its existence.
For example, the following does not compile:
```
example (h : ∃ x : Nat, x = x) : Nat :=
  let ⟨x, _⟩ := h  -- fail, because the goal is `Nat : Type`
  x
```
The error message `recursor 'Exists.casesOn' can only eliminate into Prop` means
that this only works when the current goal is another proposition:
```
example (h : ∃ x : Nat, x = x) : True :=
  let ⟨x, _⟩ := h  -- ok, because the goal is `True : Prop`
  trivial
```


## BASE-LIBRARY REF And
Prop → Prop → Prop

Docstring: `And a b`, or `a ∧ b`, is the conjunction of propositions. It can be
constructed and destructed like a pair: if `ha : a` and `hb : b` then
`⟨ha, hb⟩ : a ∧ b`, and if `h : a ∧ b` then `h.left : a` and `h.right : b`.


Conventions for notations in identifiers:

 * The recommended spelling of `∧` in identifiers is `and`.

 * The recommended spelling of `/\` in identifiers is `and` (prefer `∧` over `/\`).

## BASE-LIBRARY REF Insert.insert
{α : outParam (Type u)} → {γ : Type v} → [self : Insert α γ] → α → γ → γ

Docstring: `insert x xs` inserts the element `x` into the collection `xs`. 

## BASE-LIBRARY REF Set.instInsert
{α : Type u} → Insert α (Set α)

## BASE-LIBRARY REF Prod.mk
{α : Type u} → {β : Type v} → α → β → α × β

Docstring: Constructs a pair. This is usually written `(x, y)` instead of `Prod.mk x y`.


Conventions for notations in identifiers:

 * The recommended spelling of `(a, b)` in identifiers is `mk`.

## BASE-LIBRARY REF Singleton.singleton
{α : outParam (Type u)} → {β : Type v} → [self : Singleton α β] → α → β

Docstring: `singleton x` is a collection with the single element `x` (notation: `{x}`). 

Conventions for notations in identifiers:

 * The recommended spelling of `{x}` in identifiers is `singleton`.

## BASE-LIBRARY REF Set.instSingletonSet
{α : Type u} → Singleton α (Set α)

## BASE-LIBRARY REF HAdd.hAdd
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HAdd α β γ] → α → β → γ

Docstring: `a + b` computes the sum of `a` and `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `+` in identifiers is `add`.

## BASE-LIBRARY REF instHAdd
{α : Type u_1} → [Add α] → HAdd α α α

## BASE-LIBRARY REF Int.instAdd
Add ℤ

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNat
{n : ℕ} → OfNat ℤ n

## BASE-LIBRARY REF LE.le
{α : Type u} → [self : LE α] → α → α → Prop

Docstring: The less-equal relation: `x ≤ y` 

Conventions for notations in identifiers:

 * The recommended spelling of `≤` in identifiers is `le`.

 * The recommended spelling of `<=` in identifiers is `le` (prefer `≤` over `<=`).

## BASE-LIBRARY REF Int.instLEInt
LE ℤ

## BASE-LIBRARY REF Prod.fst
{α : Type u} → {β : Type v} → α × β → α

Docstring: The first element of a pair. 

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

## BASE-LIBRARY REF Prod.snd
{α : Type u} → {β : Type v} → α × β → β

Docstring: The second element of a pair. 

## BASE-LIBRARY REF Or
Prop → Prop → Prop

Docstring: `Or a b`, or `a ∨ b`, is the disjunction of propositions. There are two
constructors for `Or`, called `Or.inl : a → a ∨ b` and `Or.inr : b → a ∨ b`,
and you can use `match` or `cases` to destruct an `Or` assumption into the
two cases.


Conventions for notations in identifiers:

 * The recommended spelling of `∨` in identifiers is `or`.

 * The recommended spelling of `\/` in identifiers is `or` (prefer `∨` over `\/`).

## BASE-LIBRARY REF instAddNat
Add ℕ

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

## BASE-LIBRARY REF Finset.instInsert
{α : Type u_1} → [DecidableEq α] → Insert α (Finset α)

Docstring: `insert a s` is the set `{a} ∪ s` containing `a` and the elements of `s`. 

## BASE-LIBRARY REF Finset.instSingleton
{α : Type u_1} → Singleton α (Finset α)

Docstring: `{a} : Finset a` is the set `{a}` containing `a` and nothing else.

This differs from `insert a ∅` in that it does not require a `DecidableEq` instance for `α`.


## BASE-LIBRARY REF Finset.map
{α : Type u_1} → {β : Type u_2} → (α ↪ β) → Finset α → Finset β

Docstring: When `f` is an embedding of `α` in `β` and `s` is a finset in `α`, then `s.map f` is the image
finset in `β`. The embedding condition guarantees that there are no duplicates in the image. 

## BASE-LIBRARY REF Function.Embedding.mk
{α : Sort u_1} → {β : Sort u_2} → (toFun : α → β) → Function.Injective toFun → α ↪ β

## BASE-LIBRARY REF SProd.sprod
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : SProd α β γ] → α → β → γ

Docstring: The Cartesian product `s ×ˢ t` is the set of `(a, b)` such that `a ∈ s` and `b ∈ t`. 

## BASE-LIBRARY REF Finset.instSProd
{α : Type u_1} → {β : Type u_2} → SProd (Finset α) (Finset β) (Finset (α × β))

## BASE-LIBRARY REF Finset.range
ℕ → Finset ℕ

Docstring: `range n` is the set of natural numbers less than `n`. 

## BASE-LIBRARY REF ite
{α : Sort u} → (c : Prop) → [h : Decidable c] → α → α → α

Docstring: `if c then t else e` is notation for `ite c t e`, "if-then-else", which decides to
return `t` or `e` depending on whether `c` is true or false. The explicit argument
`c : Prop` does not have any actual computational content, but there is an additional
`[Decidable c]` argument synthesized by typeclass inference which actually
determines how to evaluate `c` to true or false. Write `if h : c then t else e`
instead for a "dependent if-then-else" `dite`, which allows `t`/`e` to use the fact
that `c` is true/false.


## BASE-LIBRARY REF Min.min
{α : Type u} → [self : Min α] → α → α → α

Docstring: Returns the lesser of its two arguments. 

Conventions for notations in identifiers:

 * The recommended spelling of `min` in identifiers is `min`.

 * The recommended spelling of `⊓` in identifiers is `inf` (`⊓` is the preferred notation for `min` when the type is not linearly ordered.).

## BASE-LIBRARY REF instMinNat
Min ℕ

## BASE-LIBRARY REF DecidablePred
{α : Sort u} → (α → Prop) → Sort (max 1 u)

Docstring: A decidable predicate.

A predicate is decidable if the corresponding proposition is `Decidable` for each possible argument.


## BASE-LIBRARY REF inferInstanceAs
(α : Sort u) → [i : α] → α

Docstring: `inferInstanceAs α` synthesizes a value of any target type by typeclass
inference. This is just like `inferInstance` except that `α` is given
explicitly instead of being inferred from the target type. It is especially
useful when the target type is some `α'` which is definitionally equal to `α`,
but the instance we are looking for is only registered for `α` (because
typeclass search does not unfold most definitions, but definitional equality
does.) Example:
```
#check inferInstanceAs (Inhabited Nat) -- Inhabited Nat
```


## BASE-LIBRARY REF Decidable
Prop → Type

Docstring: Either a proof that `p` is true or a proof that `p` is false. This is equivalent to a `Bool` paired
with a proof that the `Bool` is `true` if and only if `p` is true.

`Decidable` instances are primarily used via `if`-expressions and the tactic `decide`. In
conditional expressions, the `Decidable` instance for the proposition is used to select a branch. At
run time, this case distinction code is identical to that which would be generated for a
`Bool`-based conditional. In proofs, the tactic `decide` synthesizes an instance of `Decidable p`,
attempts to reduce it to `isTrue h`, and then succeeds with the proof `h` if it can.

Because `Decidable` carries data, when writing `@[simp]` lemmas which include a `Decidable` instance
on the LHS, it is best to use `{_ : Decidable p}` rather than `[Decidable p]` so that non-canonical
instances can be found via unification rather than instance synthesis.


## INFORMAL STATEMENT
lem.details.domino.toDominoZ-cover

\leanhelper  If a set of natural-number-based dominos covers the natural-number-based rectangle $R_{n,m}$, then their images under the coordinate casting cover the $\mathbb {Z}$-based rectangle $R_{n,m}$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.details.domino.bridge-conversions
def.details.domino.bridge-conversions

\leanhelper  \textbf{(a)} There is a conversion from natural-number-based dominos (with natural number coordinates) to integer-based dominos (with integer coordinates) given by casting each coordinate. \medskip 

\textbf{(b)} There is a conversion from integer-based dominos with positive coordinates back to natural-number-based dominos. \medskip 

\textbf{(c)} There is a conversion from natural-number-based tilings of $R_{n,m}$ to integer-based tilings of $R_{n,m}$ obtained by converting each domino.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.domino.shapes-and-tilings
def.domino.shapes-and-tilings

\textbf{(a)} A \emph{shape} means a subset of $\mathbb {Z}^{2}$. 

We draw each $\left( i,j\right) \in \mathbb {Z}^{2}$ as a unit square with center at the point $\left( i,j\right) $ (in Cartesian coordinates); thus, a shape can be drawn as a cluster of squares. \medskip 

\textbf{(b)} For any $n,m\in \mathbb {N}$, the shape $R_{n,m}$ (called the $n\times m$\emph{-rectangle}) is defined to be

\[  \left\{  1,2,\ldots ,n\right\}  \times \left\{  1,2,\ldots ,m\right\}  =\left\{  \left( i,j\right) \in \mathbb {Z}^{2}\  \mid \  1\leq i\leq n\text{ and }1\leq j\leq m\right\}  .  \]

\textbf{(c)} A \emph{domino} means a size-$2$ shape of the form

\begin{align*} &  \left\{  \left( i,j\right) ,\  \left( i+1,j\right) \right\}  \text{ (a ``\emph{horizontal domino}'')}\  \  \  \  \  \  \  \  \  \  \text{or}\\ &  \left\{  \left( i,j\right) ,\  \left( i,j+1\right) \right\}  \text{ (a ``\emph{vertical domino}'')}\end{align*}

 for some $\left( i,j\right) \in \mathbb {Z}^{2}$. \medskip 

\textbf{(d)} A \emph{domino tiling} of a shape $S$ is a set partition of $S$ into dominos (i.e., a set of disjoint dominos whose union is $S$). \medskip 

\textbf{(e)} For any $n,m\in \mathbb {N}$, let $d_{n,m}$ be the \#  of domino tilings of $R_{n,m}$.

## VERDICT
{
  "verdict": "drift",
  "justification": "The blueprint quantifies over any covering set: \u201cIf a set of natural-number-based dominos covers \u2026 then their images \u2026 cover.\u201d The Lean target instead binds `(T : DominoTilings.DominoTiling n m)`. By the constructor of `DominoTilings.DominoTiling`, such a `T` must satisfy not only `dominos.biUnion Domino.cells = Rectangle n m`, but also containment and pairwise disjointness: `(\u2200 d \u2208 dominos, d.cells \u2286 Rectangle n m)` and `(\u2200 d\u2081 \u2208 dominos, \u2200 d\u2082 \u2208 dominos, d\u2081 \u2260 d\u2082 \u2192 Disjoint d\u2081.cells d\u2082.cells)`. These are mathematically contentful added hypotheses, so the theorem only handles tilings rather than every set that covers the rectangle. The coordinate conversion and resulting union otherwise match the stated conclusion. To be faithful, the target should quantify over a finset `ds : Finset DominoTilings.Domino`, assume only `ds.biUnion DominoTilings.Domino.cells = DominoTilings.Rectangle n m`, and conclude `\u22c3 d \u2208 DominoBridge.dominoFinsetToSet ds, d.toShape = DominoTilingsZ.Rectangle n m`."
}