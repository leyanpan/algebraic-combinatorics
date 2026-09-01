## TARGET DominoTilings.DominoTiling.restrictAfterVertical (def) — ELABORATED SIGNATURE
{n : ℕ} →
  (T : DominoTilings.DominoTiling (n + 1) 2) → DominoTilings.vertical_1_1 ∈ T.dominos → DominoTilings.DominoTiling n 2

Body:
fun {n} T hv =>
  {
    dominos :=
      Finset.image
        (fun x =>
          match x with
          | ⟨d, hd⟩ =>
            have hd' := ⋯;
            have hcols := ⋯;
            d.shiftNeg 1 ⋯ ⋯)
        (T.dominos.erase DominoTilings.vertical_1_1).attach,
    dominos_in_rect := ⋯, covers_all := ⋯, pairwise_disjoint := ⋯ }

Docstring: Extract the tiling of Rectangle n 2 from a tiling of Rectangle (n+1) 2
that has vertical_1_1 as its first domino.

This removes vertical_1_1 and shifts all remaining dominos one column left.
It is the left inverse of prependVertical. 

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

## PROJECT DEPENDENCY DominoTilings.Domino (inductive)
Type

Body:
DominoTilings.Domino.mk : (cell1 cell2 : DominoTilings.Cell) →
  cell1 ≠ cell2 →
    cell1.1 = cell2.1 ∧ (cell1.2 + 1 = cell2.2 ∨ cell2.2 + 1 = cell1.2) ∨
        cell1.2 = cell2.2 ∧ (cell1.1 + 1 = cell2.1 ∨ cell2.1 + 1 = cell1.1) →
      DominoTilings.Domino

Docstring: A domino is a pair of adjacent cells, either horizontal or vertical. 

## PROJECT DEPENDENCY DominoTilings.DominoTiling.dominos (def)
{n m : ℕ} → DominoTilings.DominoTiling n m → Finset DominoTilings.Domino

Body:
fun n m self => self.1

Docstring: The set of dominos in the tiling 

## PROJECT DEPENDENCY DominoTilings.vertical_1_1 (def)
DominoTilings.Domino

Body:
{ cell1 := (1, 1), cell2 := (1, 2), distinct := DominoTilings.vertical_1_1._proof_1,
  adjacent := DominoTilings.vertical_1_1._proof_2 }

Docstring: The vertical domino covering column 1 in a 2-row rectangle: cells (1,1) and (1,2). 

## PROJECT DEPENDENCY DominoTilings.DominoTiling.mk (constructor)
{n m : ℕ} →
  (dominos : Finset DominoTilings.Domino) →
    (∀ d ∈ dominos, d.cells ⊆ DominoTilings.Rectangle n m) →
      dominos.biUnion DominoTilings.Domino.cells = DominoTilings.Rectangle n m →
        (∀ d₁ ∈ dominos, ∀ d₂ ∈ dominos, d₁ ≠ d₂ → Disjoint d₁.cells d₂.cells) → DominoTilings.DominoTiling n m

## PROJECT DEPENDENCY DominoTilings.instDecidableEqDomino (def)
DecidableEq DominoTilings.Domino

Body:
DominoTilings.instDecidableEqDomino.decEq

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

## PROJECT DEPENDENCY DominoTilings.Domino.shiftNeg (def)
(d : DominoTilings.Domino) → (k : ℕ) → d.cell1.1 ≥ k + 1 → d.cell2.1 ≥ k + 1 → DominoTilings.Domino

Body:
fun d k h1 h2 =>
  { cell1 := (d.cell1.1 - k, d.cell1.2), cell2 := (d.cell2.1 - k, d.cell2.2), distinct := ⋯, adjacent := ⋯ }

Docstring: Shift a domino k columns to the left. Requires that both cells have column ≥ k+1. 

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

## PROJECT DEPENDENCY DominoTilings.Domino.mk (constructor)
(cell1 cell2 : DominoTilings.Cell) →
  cell1 ≠ cell2 →
    cell1.1 = cell2.1 ∧ (cell1.2 + 1 = cell2.2 ∨ cell2.2 + 1 = cell1.2) ∨
        cell1.2 = cell2.2 ∧ (cell1.1 + 1 = cell2.1 ∨ cell2.1 + 1 = cell1.1) →
      DominoTilings.Domino

## PROJECT DEPENDENCY DominoTilings.instDecidableEqDomino.decEq (def)
(x x_1 : DominoTilings.Domino) → Decidable (x = x_1)

Body:
fun x x_1 =>
  match x, x_1 with
  | { cell1 := a, cell2 := a_1, distinct := a_2, adjacent := a_3 },
    { cell1 := b, cell2 := b_1, distinct := b_2, adjacent := b_3 } =>
    if h : a = b then
      Eq.ndrec (motive := fun b =>
        (b_4 : b ≠ b_1) →
          (b_5 :
              b.1 = b_1.1 ∧ (b.2 + 1 = b_1.2 ∨ b_1.2 + 1 = b.2) ∨ b.2 = b_1.2 ∧ (b.1 + 1 = b_1.1 ∨ b_1.1 + 1 = b.1)) →
            Decidable
              ({ cell1 := a, cell2 := a_1, distinct := a_2, adjacent := a_3 } =
                { cell1 := b, cell2 := b_1, distinct := b_4, adjacent := b_5 }))
        (fun b b_4 =>
          if h : a_1 = b_1 then
            Eq.ndrec (motive := fun b =>
              (b_5 : a ≠ b) →
                (b_6 : a.1 = b.1 ∧ (a.2 + 1 = b.2 ∨ b.2 + 1 = a.2) ∨ a.2 = b.2 ∧ (a.1 + 1 = b.1 ∨ b.1 + 1 = a.1)) →
                  Decidable
                    ({ cell1 := a, cell2 := a_1, distinct := a_2, adjacent := a_3 } =
                      { cell1 := a, cell2 := b, distinct := b_5, adjacent := b_6 }))
              (fun b b_5 =>
                have h := ⋯;
                h ▸
                  have h := ⋯;
                  h ▸ isTrue ⋯)
              h b b_4
          else isFalse ⋯)
        h b_2 b_3
    else isFalse ⋯

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


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

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

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

## BASE-LIBRARY REF Finset.image
{α : Type u_1} → {β : Type u_2} → [DecidableEq β] → (α → β) → Finset α → Finset β

Docstring: `image f s` is the forward image of `s` under `f`. 

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

## BASE-LIBRARY REF Finset.erase
{α : Type u_1} → [DecidableEq α] → Finset α → α → Finset α

Docstring: `erase s a` is the set `s - {a}`, that is, the elements of `s` which are
not equal to `a`. 

## BASE-LIBRARY REF And
Prop → Prop → Prop

Docstring: `And a b`, or `a ∧ b`, is the conjunction of propositions. It can be
constructed and destructed like a pair: if `ha : a` and `hb : b` then
`⟨ha, hb⟩ : a ∧ b`, and if `h : a ∧ b` then `h.left : a` and `h.right : b`.


Conventions for notations in identifiers:

 * The recommended spelling of `∧` in identifiers is `and`.

 * The recommended spelling of `/\` in identifiers is `and` (prefer `∧` over `/\`).

## BASE-LIBRARY REF Ne
{α : Sort u} → α → α → Prop

Docstring: `a ≠ b`, or `Ne a b` is defined as `¬ (a = b)` or `a = b → False`,
and asserts that `a` and `b` are not equal.


Conventions for notations in identifiers:

 * The recommended spelling of `≠` in identifiers is `ne`.

## BASE-LIBRARY REF GE.ge
{α : Type u} → [LE α] → α → α → Prop

Docstring: `a ≥ b` is an abbreviation for `b ≤ a`. 

Conventions for notations in identifiers:

 * The recommended spelling of `≥` in identifiers is `ge`.

 * The recommended spelling of `>=` in identifiers is `ge` (prefer `≥` over `>=`).

## BASE-LIBRARY REF instLENat
LE ℕ

## BASE-LIBRARY REF Prod.fst
{α : Type u} → {β : Type v} → α × β → α

Docstring: The first element of a pair. 

## BASE-LIBRARY REF Finset.attach
{α : Type u_1} → (s : Finset α) → Finset { x // x ∈ s }

Docstring: `attach s` takes the elements of `s` and forms a new set of elements of the subtype
`{x // x ∈ s}`. 

## BASE-LIBRARY REF HasSubset.Subset
{α : Type u} → [self : HasSubset α] → α → α → Prop

Docstring: Subset relation: `a ⊆ b`  

Conventions for notations in identifiers:

 * The recommended spelling of `⊆` in identifiers is `subset`.

## BASE-LIBRARY REF Finset.instHasSubset
{α : Type u_1} → HasSubset (Finset α)

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

## BASE-LIBRARY REF Finset.biUnion
{α : Type u_1} → {β : Type u_2} → [DecidableEq β] → Finset α → (α → Finset β) → Finset β

Docstring: `Finset.biUnion s t` is the union of `t a` over `a ∈ s`.

(This was formerly `bind` due to the monad structure on types with `DecidableEq`.) 

## BASE-LIBRARY REF instDecidableEqProd
{α : Type u_1} → {β : Type u_2} → [DecidableEq α] → [DecidableEq β] → DecidableEq (α × β)

## BASE-LIBRARY REF instDecidableEqNat
DecidableEq ℕ

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

## BASE-LIBRARY REF Or
Prop → Prop → Prop

Docstring: `Or a b`, or `a ∨ b`, is the disjunction of propositions. There are two
constructors for `Or`, called `Or.inl : a → a ∨ b` and `Or.inr : b → a ∨ b`,
and you can use `match` or `cases` to destruct an `Or` assumption into the
two cases.


Conventions for notations in identifiers:

 * The recommended spelling of `∨` in identifiers is `or`.

 * The recommended spelling of `\/` in identifiers is `or` (prefer `∨` over `\/`).

## BASE-LIBRARY REF Prod.snd
{α : Type u} → {β : Type v} → α × β → β

Docstring: The second element of a pair. 

## BASE-LIBRARY REF Prod.mk
{α : Type u} → {β : Type v} → α → β → α × β

Docstring: Constructs a pair. This is usually written `(x, y)` instead of `Prod.mk x y`.


Conventions for notations in identifiers:

 * The recommended spelling of `(a, b)` in identifiers is `mk`.

## BASE-LIBRARY REF DecidableEq
Sort u → Sort (max 1 u)

Docstring: Propositional equality is `Decidable` for all elements of a type.

In other words, an instance of `DecidableEq α` is a means of deciding the proposition `a = b` is
for all `a b : α`.


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

## BASE-LIBRARY REF Prod
Type u → Type v → Type (max u v)

Docstring: The product type, usually written `α × β`. Product types are also called pair or tuple types.
Elements of this type are pairs in which the first element is an `α` and the second element is a
`β`.

Products nest to the right, so `(x, y, z) : α × β × γ` is equivalent to `(x, (y, z)) : α × (β × γ)`.


Conventions for notations in identifiers:

 * The recommended spelling of `×` in identifiers is `Prod`.

## BASE-LIBRARY REF Insert.insert
{α : outParam (Type u)} → {γ : Type v} → [self : Insert α γ] → α → γ → γ

Docstring: `insert x xs` inserts the element `x` into the collection `xs`. 

## BASE-LIBRARY REF Finset.instInsert
{α : Type u_1} → [DecidableEq α] → Insert α (Finset α)

Docstring: `insert a s` is the set `{a} ∪ s` containing `a` and the elements of `s`. 

## BASE-LIBRARY REF Singleton.singleton
{α : outParam (Type u)} → {β : Type v} → [self : Singleton α β] → α → β

Docstring: `singleton x` is a collection with the single element `x` (notation: `{x}`). 

Conventions for notations in identifiers:

 * The recommended spelling of `{x}` in identifiers is `singleton`.

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


## BASE-LIBRARY REF dite
{α : Sort u} → (c : Prop) → [h : Decidable c] → (c → α) → (¬c → α) → α

Docstring: "Dependent" if-then-else, normally written via the notation `if h : c then t(h) else e(h)`,
is sugar for `dite c (fun h => t(h)) (fun h => e(h))`, and it is the same as
`if c then t else e` except that `t` is allowed to depend on a proof `h : c`,
and `e` can depend on `h : ¬c`. (Both branches use the same name for the hypothesis,
even though it has different types in the two cases.)

We use this to be able to communicate the if-then-else condition to the branches.
For example, `Array.get arr i h` expects a proof `h : i < arr.size` in order to
avoid a bounds check, so you can write `if h : i < arr.size then arr.get i h else ...`
to avoid the bounds check inside the if branch. (Of course in this case we have only
lifted the check into an explicit `if`, but we could also use this proof multiple times
or derive `i < arr.size` from some other proposition that we are checking in the `if`.)


## BASE-LIBRARY REF Eq.ndrec
{α : Sort u2} → {a : α} → {motive : α → Sort u1} → motive a → {b : α} → a = b → motive b

Docstring: Non-dependent recursor for the equality type. 

## BASE-LIBRARY REF Decidable.isTrue
{p : Prop} → p → Decidable p

Docstring: Proves that `p` is decidable by supplying a proof of `p` 

## BASE-LIBRARY REF Not
Prop → Prop

Docstring: `Not p`, or `¬p`, is the negation of `p`. It is defined to be `p → False`,
so if your goal is `¬p` you can use `intro h` to turn the goal into
`h : p ⊢ False`, and if you have `hn : ¬p` and `h : p` then `hn h : False`
and `(hn h).elim` will prove anything.
For more information: [Propositional Logic](https://lean-lang.org/theorem_proving_in_lean4/propositions_and_proofs.html#propositional-logic)


Conventions for notations in identifiers:

 * The recommended spelling of `¬` in identifiers is `not`.

## BASE-LIBRARY REF Decidable.isFalse
{p : Prop} → ¬p → Decidable p

Docstring: Proves that `p` is decidable by supplying a proof of `¬p` 

## INFORMAL STATEMENT
lem.details.domino.restrictAfterVertical

\leanhelper  Given a tiling $T$ of $R_{n+1,2}$ that contains the vertical domino $\{ (1,1),(1,2)\} $, removing it and shifting all other dominos left by $1$ gives a valid tiling of $R_{n,2}$.

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
  "justification": "The informal hypothesis says that T \u201ccontains the vertical domino { (1,1),(1,2) },\u201d where a domino is a shape, hence an unordered set of two cells. The formal binder instead requires `DominoTilings.vertical_1_1 \u2208 T.dominos`, and `vertical_1_1` is the specifically ordered value `{ cell1 := (1, 1), cell2 := (1, 2), ... }`. The project\u2019s `Domino` inductive permits the reverse representation with `cell1 := (1,2)` and `cell2 := (1,1)`, while its decidable equality is structural, so that reverse domino is not equal to `vertical_1_1` even though its `cells` finset is the same informal domino. Thus the binder `hv` narrows the informal hypothesis and the body\u2019s `erase DominoTilings.vertical_1_1` only removes that chosen orientation. To make the declaration faithful, either make `Domino` canonically unordered/canonically oriented, or replace `hv` by existence of a domino `d \u2208 T.dominos` whose `d.cells = vertical_1_1.cells`, then erase and shift that `d`."
}