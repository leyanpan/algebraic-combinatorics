## TARGET DominoTilings.faultfree_bottom_vertical_classification (theorem) — ELABORATED SIGNATURE
∀ (n : ℕ) (T : DominoTilings.DominoTiling n 3),
  T.isFaultfree →
    T.hasBottomVerticalInCol 1 →
      Even n ∧ ∃ (hn : Even n) (hn_ge : n ≥ 2), T.TilingEquiv (DominoTilings.TilingB n hn hn_ge)

Docstring: (prop.gf.weighted-set.domino.Rn3.ABC (b))
The faultfree domino tilings of a height-3 rectangle with a vertical domino in
the bottom two squares of column 1 are precisely B_2, B_4, B_6, ...

This follows from part (a) by reflection across the horizontal axis.

Note: We use TilingEquiv instead of = because the Domino structure distinguishes
between different cell orderings. 

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

## PROJECT DEPENDENCY DominoTilings.DominoTiling.isFaultfree (def)
{n m : ℕ} → DominoTilings.DominoTiling n m → Prop

Body:
fun {n m} T => ∀ k ≥ 1, k < n → ¬T.hasFaultAt k

Docstring: A tiling is faultfree if it has no faults at any column in range [1, n-1]. 

## PROJECT DEPENDENCY DominoTilings.DominoTiling.hasBottomVerticalInCol (def)
{n m : ℕ} → DominoTilings.DominoTiling n m → ℕ → Prop

Body:
fun {n m} T c =>
  ∃ d ∈ T.dominos, d.isVertical ∧ d.cell1.1 = c ∧ (d.cell1.2 = 1 ∧ d.cell2.2 = 2 ∨ d.cell1.2 = 2 ∧ d.cell2.2 = 1)

Docstring: Whether a tiling contains a vertical domino in the bottom two squares of column c. 

## PROJECT DEPENDENCY DominoTilings.DominoTiling.TilingEquiv (def)
{n m : ℕ} → DominoTilings.DominoTiling n m → DominoTilings.DominoTiling n m → Prop

Body:
fun {n m} T₁ T₂ =>
  Finset.image DominoTilings.Domino.cells T₁.dominos = Finset.image DominoTilings.Domino.cells T₂.dominos

Docstring: Two tilings are equivalent if they cover the same cells with the same domino cell sets.

This is the appropriate notion of equality for tilings, since the Domino structure
distinguishes between {cell1 := a, cell2 := b} and {cell1 := b, cell2 := a} even
though they cover the same cells.

Note: This is a weaker notion than structural equality (T₁ = T₂), but is the
mathematically correct notion for classification theorems. 

## PROJECT DEPENDENCY DominoTilings.TilingB (def)
(n : ℕ) → Even n → n ≥ 2 → DominoTilings.DominoTiling n 3

Body:
fun n hn hn_ge =>
  {
    dominos :=
      DominoTilings.basementDominosB n ∪ {DominoTilings.leftWallB} ∪ {DominoTilings.rightWallB n} ∪
          DominoTilings.middleDominos n ∪
        DominoTilings.bottomDominosB n,
    dominos_in_rect := ⋯, covers_all := ⋯, pairwise_disjoint := ⋯ }

Docstring: Tiling B_n for even positive n ≥ 2.

This is the reflection of A_n across the horizontal axis.
It has a vertical domino in the bottom two squares of column 1.

(def.gf.weighted-set.domino.Rn3.ABC (b)) 

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

## PROJECT DEPENDENCY DominoTilings.DominoTiling.hasFaultAt (def)
{n m : ℕ} → DominoTilings.DominoTiling n m → ℕ → Prop

Body:
fun {n m} T k => k ≥ 1 ∧ k < n ∧ ∀ d ∈ T.dominos, ¬(d.minCol ≤ k ∧ k < d.maxCol)

Docstring: A tiling has a fault at column k if there is a vertical line between columns k and k+1
that does not cross any domino. Equivalently, no domino spans columns k and k+1. 

## PROJECT DEPENDENCY DominoTilings.DominoTiling.dominos (def)
{n m : ℕ} → DominoTilings.DominoTiling n m → Finset DominoTilings.Domino

Body:
fun n m self => self.1

Docstring: The set of dominos in the tiling 

## PROJECT DEPENDENCY DominoTilings.Domino.isVertical (def)
DominoTilings.Domino → Prop

Body:
fun d => d.cell1.1 = d.cell2.1

Docstring: A domino is vertical if both cells are in the same column. 

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

## PROJECT DEPENDENCY DominoTilings.basementDominosB (def)
ℕ → Finset DominoTilings.Domino

Body:
fun n =>
  Finset.map
    { toFun := fun i => { cell1 := (2 * i + 1, 3), cell2 := (2 * i + 2, 3), distinct := ⋯, adjacent := ⋯ },
      inj' := DominoTilings.basementDominosB._proof_3 }
    (Finset.range (n / 2))

Docstring: The "basement" dominos for tiling B_n: horizontal dominos filling row 3 (the top row).
Named "basement" by analogy with A_n, though in B_n these are at the top due to reflection. 

## PROJECT DEPENDENCY DominoTilings.leftWallB (def)
DominoTilings.Domino

Body:
{ cell1 := (1, 2), cell2 := (1, 1), distinct := DominoTilings.vertical_1_1_flip._proof_1,
  adjacent := DominoTilings.vertical_1_1_flip._proof_2 }

Docstring: The left wall for tiling B_n: vertical domino in column 1, rows 1-2.
Note: cell ordering matches reflectDomino3 applied to leftWall. 

## PROJECT DEPENDENCY DominoTilings.rightWallB (def)
ℕ → DominoTilings.Domino

Body:
fun n => { cell1 := (n, 2), cell2 := (n, 1), distinct := ⋯, adjacent := ⋯ }

Docstring: The right wall for tiling B_n: vertical domino in column n, rows 1-2.
Note: cell ordering matches reflectDomino3 applied to rightWall. 

## PROJECT DEPENDENCY DominoTilings.middleDominos (def)
ℕ → Finset DominoTilings.Domino

Body:
fun n =>
  Finset.map
    { toFun := fun i => { cell1 := (2 * i + 2, 2), cell2 := (2 * i + 3, 2), distinct := ⋯, adjacent := ⋯ },
      inj' := DominoTilings.middleDominos._proof_5 }
    (Finset.range (n / 2 - 1))

Docstring: The middle dominos for tiling A_n: horizontal dominos in row 2 (except first/last columns). 

## PROJECT DEPENDENCY DominoTilings.bottomDominosB (def)
ℕ → Finset DominoTilings.Domino

Body:
fun n =>
  Finset.map
    { toFun := fun i => { cell1 := (2 * i + 2, 1), cell2 := (2 * i + 3, 1), distinct := ⋯, adjacent := ⋯ },
      inj' := DominoTilings.bottomDominosB._proof_3 }
    (Finset.range (n / 2 - 1))

Docstring: The bottom dominos for tiling B_n: horizontal dominos in row 1 (except first/last columns). 

## PROJECT DEPENDENCY DominoTilings.Domino.minCol (def)
DominoTilings.Domino → ℕ

Body:
fun d => min d.cell1.1 d.cell2.1

Docstring: The leftmost column touched by a domino. 

## PROJECT DEPENDENCY DominoTilings.Domino.maxCol (def)
DominoTilings.Domino → ℕ

Body:
fun d => max d.cell1.1 d.cell2.1

Docstring: The rightmost column touched by a domino. 

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

## PROJECT DEPENDENCY DominoTilings.Domino.mk (constructor)
(cell1 cell2 : DominoTilings.Cell) →
  cell1 ≠ cell2 →
    cell1.1 = cell2.1 ∧ (cell1.2 + 1 = cell2.2 ∨ cell2.2 + 1 = cell1.2) ∨
        cell1.2 = cell2.2 ∧ (cell1.1 + 1 = cell2.1 ∨ cell2.1 + 1 = cell1.1) →
      DominoTilings.Domino

## PROJECT DEPENDENCY DominoTilings.vertical_1_1_flip (def)
DominoTilings.Domino

Body:
{ cell1 := (1, 2), cell2 := (1, 1), distinct := DominoTilings.vertical_1_1_flip._proof_1,
  adjacent := DominoTilings.vertical_1_1_flip._proof_2 }

Docstring: The "flipped" vertical domino with cell1 and cell2 swapped. 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

## BASE-LIBRARY REF And
Prop → Prop → Prop

Docstring: `And a b`, or `a ∧ b`, is the conjunction of propositions. It can be
constructed and destructed like a pair: if `ha : a` and `hb : b` then
`⟨ha, hb⟩ : a ∧ b`, and if `h : a ∧ b` then `h.left : a` and `h.right : b`.


Conventions for notations in identifiers:

 * The recommended spelling of `∧` in identifiers is `and`.

 * The recommended spelling of `/\` in identifiers is `and` (prefer `∧` over `/\`).

## BASE-LIBRARY REF Even
{α : Type u_2} → [Add α] → α → Prop

Docstring: An element `a` of a type `α` with addition satisfies `Even a` if `a = r + r`,
for some `r : α`. 

## BASE-LIBRARY REF instAddNat
Add ℕ

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


## BASE-LIBRARY REF GE.ge
{α : Type u} → [LE α] → α → α → Prop

Docstring: `a ≥ b` is an abbreviation for `b ≤ a`. 

Conventions for notations in identifiers:

 * The recommended spelling of `≥` in identifiers is `ge`.

 * The recommended spelling of `>=` in identifiers is `ge` (prefer `≥` over `>=`).

## BASE-LIBRARY REF instLENat
LE ℕ

## BASE-LIBRARY REF Finset
Type u_4 → Type u_4

Docstring: `Finset α` is the type of finite sets of elements of `α`. It is implemented
as a multiset (a list up to permutation) which has no duplicate elements. 

## BASE-LIBRARY REF Membership.mem
{α : outParam (Type u)} → {γ : Type v} → [self : Membership α γ] → γ → α → Prop

Docstring: The membership relation `a ∈ s : Prop` where `a : α`, `s : γ`. 

Conventions for notations in identifiers:

 * The recommended spelling of `∈` in identifiers is `mem`.

## BASE-LIBRARY REF Finset.instMembership
{α : Type u_1} → Membership α (Finset α)

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

## BASE-LIBRARY REF LT.lt
{α : Type u} → [self : LT α] → α → α → Prop

Docstring: The less-than relation: `x < y` 

Conventions for notations in identifiers:

 * The recommended spelling of `<` in identifiers is `lt`.

## BASE-LIBRARY REF instLTNat
LT ℕ

## BASE-LIBRARY REF Not
Prop → Prop

Docstring: `Not p`, or `¬p`, is the negation of `p`. It is defined to be `p → False`,
so if your goal is `¬p` you can use `intro h` to turn the goal into
`h : p ⊢ False`, and if you have `hn : ¬p` and `h : p` then `hn h : False`
and `(hn h).elim` will prove anything.
For more information: [Propositional Logic](https://lean-lang.org/theorem_proving_in_lean4/propositions_and_proofs.html#propositional-logic)


Conventions for notations in identifiers:

 * The recommended spelling of `¬` in identifiers is `not`.

## BASE-LIBRARY REF Prod.fst
{α : Type u} → {β : Type v} → α × β → α

Docstring: The first element of a pair. 

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

## BASE-LIBRARY REF Finset.image
{α : Type u_1} → {β : Type u_2} → [DecidableEq β] → (α → β) → Finset α → Finset β

Docstring: `image f s` is the forward image of `s` under `f`. 

## BASE-LIBRARY REF Finset.decidableEq
{α : Type u_1} → [DecidableEq α] → DecidableEq (Finset α)

## BASE-LIBRARY REF Union.union
{α : Type u} → [self : Union α] → α → α → α

Docstring: `a ∪ b` is the union of `a` and `b`. 

Conventions for notations in identifiers:

 * The recommended spelling of `∪` in identifiers is `union`.

## BASE-LIBRARY REF Finset.instUnion
{α : Type u_1} → [DecidableEq α] → Union (Finset α)

Docstring: `s ∪ t` is the set such that `a ∈ s ∪ t` iff `a ∈ s` or `a ∈ t`. 

## BASE-LIBRARY REF Singleton.singleton
{α : outParam (Type u)} → {β : Type v} → [self : Singleton α β] → α → β

Docstring: `singleton x` is a collection with the single element `x` (notation: `{x}`). 

Conventions for notations in identifiers:

 * The recommended spelling of `{x}` in identifiers is `singleton`.

## BASE-LIBRARY REF Finset.instSingleton
{α : Type u_1} → Singleton α (Finset α)

Docstring: `{a} : Finset a` is the set `{a}` containing `a` and nothing else.

This differs from `insert a ∅` in that it does not require a `DecidableEq` instance for `α`.


## BASE-LIBRARY REF HAdd.hAdd
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HAdd α β γ] → α → β → γ

Docstring: `a + b` computes the sum of `a` and `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `+` in identifiers is `add`.

## BASE-LIBRARY REF instHAdd
{α : Type u_1} → [Add α] → HAdd α α α

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

## BASE-LIBRARY REF Finset.map
{α : Type u_1} → {β : Type u_2} → (α ↪ β) → Finset α → Finset β

Docstring: When `f` is an embedding of `α` in `β` and `s` is a finset in `α`, then `s.map f` is the image
finset in `β`. The embedding condition guarantees that there are no duplicates in the image. 

## BASE-LIBRARY REF Function.Embedding.mk
{α : Sort u_1} → {β : Sort u_2} → (toFun : α → β) → Function.Injective toFun → α ↪ β

## BASE-LIBRARY REF Prod.mk
{α : Type u} → {β : Type v} → α → β → α × β

Docstring: Constructs a pair. This is usually written `(x, y)` instead of `Prod.mk x y`.


Conventions for notations in identifiers:

 * The recommended spelling of `(a, b)` in identifiers is `mk`.

## BASE-LIBRARY REF SProd.sprod
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : SProd α β γ] → α → β → γ

Docstring: The Cartesian product `s ×ˢ t` is the set of `(a, b)` such that `a ∈ s` and `b ∈ t`. 

## BASE-LIBRARY REF Finset.instSProd
{α : Type u_1} → {β : Type u_2} → SProd (Finset α) (Finset β) (Finset (α × β))

## BASE-LIBRARY REF Finset.range
ℕ → Finset ℕ

Docstring: `range n` is the set of natural numbers less than `n`. 

## BASE-LIBRARY REF LE.le
{α : Type u} → [self : LE α] → α → α → Prop

Docstring: The less-equal relation: `x ≤ y` 

Conventions for notations in identifiers:

 * The recommended spelling of `≤` in identifiers is `le`.

 * The recommended spelling of `<=` in identifiers is `le` (prefer `≤` over `<=`).

## BASE-LIBRARY REF DecidableEq
Sort u → Sort (max 1 u)

Docstring: Propositional equality is `Decidable` for all elements of a type.

In other words, an instance of `DecidableEq α` is a means of deciding the proposition `a = b` is
for all `a b : α`.


## BASE-LIBRARY REF HMul.hMul
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HMul α β γ] → α → β → γ

Docstring: `a * b` computes the product of `a` and `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `*` in identifiers is `mul`.

## BASE-LIBRARY REF instHMul
{α : Type u_1} → [Mul α] → HMul α α α

## BASE-LIBRARY REF instMulNat
Mul ℕ

## BASE-LIBRARY REF HDiv.hDiv
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HDiv α β γ] → α → β → γ

Docstring: `a / b` computes the result of dividing `a` by `b`.
The meaning of this notation is type-dependent.
* For most types like `Nat`, `Int`, `Rat`, `Real`, `a / 0` is defined to be `0`.
* For `Nat`, `a / b` rounds downwards.
* For `Int`, `a / b` rounds downwards if `b` is positive or upwards if `b` is negative.
  It is implemented as `Int.ediv`, the unique function satisfying
  `a % b + b * (a / b) = a` and `0 ≤ a % b < natAbs b` for `b ≠ 0`.
  Other rounding conventions are available using the functions
  `Int.fdiv` (floor rounding) and `Int.tdiv` (truncation rounding).
* For `Float`, `a / 0` follows the IEEE 754 semantics for division,
  usually resulting in `inf` or `nan`. 

Conventions for notations in identifiers:

 * The recommended spelling of `/` in identifiers is `div`.

## BASE-LIBRARY REF instHDiv
{α : Type u_1} → [Div α] → HDiv α α α

## BASE-LIBRARY REF Nat.instDiv
Div ℕ

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

## BASE-LIBRARY REF Min.min
{α : Type u} → [self : Min α] → α → α → α

Docstring: Returns the lesser of its two arguments. 

Conventions for notations in identifiers:

 * The recommended spelling of `min` in identifiers is `min`.

 * The recommended spelling of `⊓` in identifiers is `inf` (`⊓` is the preferred notation for `min` when the type is not linearly ordered.).

## BASE-LIBRARY REF instMinNat
Min ℕ

## BASE-LIBRARY REF Max.max
{α : Type u} → [self : Max α] → α → α → α

Docstring: Returns the greater of its two arguments. 

Conventions for notations in identifiers:

 * The recommended spelling of `max` in identifiers is `max`.

 * The recommended spelling of `⊔` in identifiers is `sup` (`⊔` is the preferred notation for `max` when the type is not linearly ordered.).

## BASE-LIBRARY REF Nat.instMax
Max ℕ

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

## BASE-LIBRARY REF Decidable.isFalse
{p : Prop} → ¬p → Decidable p

Docstring: Proves that `p` is decidable by supplying a proof of `¬p` 

## INFORMAL STATEMENT
lem.details.domino.classification-part-b

\leanhelper  If $T$ is a faultfree tiling of $R_{n,3}$ with a vertical domino in the bottom two squares of column~ $1$, then $n$ is even and $T = B_n$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.details.domino.reflecttiling3
def.details.domino.reflectTiling3

\leanhelper  Given a tiling $T$ of $R_{n,3}$, the \emph{reflection} of $T$ is the tiling obtained by applying the cell map $(x, y) \mapsto (x, 4 - y)$ to every cell of every domino. This swaps rows $1 \leftrightarrow 3$ and fixes row $2$.

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.gf.weighted-set.domino.rn3.abc
def.gf.weighted-set.domino.Rn3.ABC

\textbf{(a)} For each even positive integer $n$, we let $A_{n}$ be the domino tiling of $R_{n,3}$ consisting of the following dominos: 

\begin{itemize} \item the horizontal dominos $\left\{  \left( 2i-1,\  1\right) ,\  \left( 2i,\  1\right) \right\}  $ for all $i\in \left[ n/2\right] $, which fill the bottom row of $R_{n,3}$, and which we call the \textbf{basement dominos}; 

\item the vertical domino $\left\{  \left( 1,2\right) ,\  \left( 1,3\right) \right\}  $ in the first column, which we call the \textbf{left wall}; 

\item the vertical domino $\left\{  \left( n,2\right) ,\  \left( n,3\right) \right\}  $ in the last column, which we call the \textbf{right wall}; 

\item the horizontal dominos $\left\{  \left( 2i,\  2\right) ,\  \left( 2i+1,\  2\right) \right\}  $ for all $i\in \left[ n/2-1\right] $, which fill the middle row of $R_{n,3}$ (except for the first and last columns), and which we call the \textbf{middle dominos}; 

\item the horizontal dominos $\left\{  \left( 2i,\  3\right) ,\  \left( 2i+1,\  3\right) \right\}  $ for all $i\in \left[ n/2-1\right] $, which fill the top row of $R_{n,3}$ (except for the first and last columns), and which we call the \textbf{top dominos}. 

\end{itemize}

\textbf{(b)} For each even positive integer $n$, we let $B_{n}$ be the domino tiling of $R_{n,3}$ obtained by reflecting $A_{n}$ across the horizontal axis of symmetry of $R_{n,3}$ (swapping row $1$ with row $3$ and fixing row $2$). \medskip 

\textbf{(c)} We let $C$ denote the domino tiling of $R_{2,3}$ consisting of three horizontal dominos: $\left\{ (1,1),(2,1)\right\} $, $\left\{ (1,2),(2,2)\right\} $, and $\left\{ (1,3),(2,3)\right\} $.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The blueprint says: \u201cIf T is a faultfree tiling of R_{n,3} with a vertical domino in the bottom two squares of column 1, then n is even and T = B_n.\u201d The elaborated signature quantifies exactly over \u201c(n : \u2115) (T : DominoTilings.DominoTiling n 3)\u201d and assumes \u201cT.isFaultfree\u201d and \u201cT.hasBottomVerticalInCol 1\u201d. Its conclusion gives \u201cEven n\u201d and \u201cT.TilingEquiv (DominoTilings.TilingB n hn hn_ge)\u201d. `TilingEquiv` compares the finite sets of domino cell-sets, so it is the appropriate exact mathematical equality despite the formal `Domino` type retaining an irrelevant ordering of its two cells. The body of `TilingB` matches the informal reflected tiling B_n: top-row basement dominos, bottom vertical walls in columns 1 and n, and the stated interior horizontal dominos. The additional witness \u201chn_ge : n \u2265 2\u201d is not an added hypothesis: it is proved in the conclusion and is needed to construct `TilingB`; it merely records that an even positive admissible width is at least 2. Thus the Lean conclusion is at least as strong as the blueprint conclusion."
}