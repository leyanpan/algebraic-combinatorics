## TARGET DominoTilings.TilingB_isFaultfree (theorem) — ELABORATED SIGNATURE
∀ (n : ℕ) (hn : Even n) (hn_ge : n ≥ 2), (DominoTilings.TilingB n hn hn_ge).isFaultfree

Docstring: The tilings B_n are faultfree (by reflection symmetry with A_n). 

## PROJECT DEPENDENCY DominoTilings.DominoTiling.isFaultfree (def)
{n m : ℕ} → DominoTilings.DominoTiling n m → Prop

Body:
fun {n m} T => ∀ k ≥ 1, k < n → ¬T.hasFaultAt k

Docstring: A tiling is faultfree if it has no faults at any column in range [1, n-1]. 

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

## PROJECT DEPENDENCY DominoTilings.DominoTiling.hasFaultAt (def)
{n m : ℕ} → DominoTilings.DominoTiling n m → ℕ → Prop

Body:
fun {n m} T k => k ≥ 1 ∧ k < n ∧ ∀ d ∈ T.dominos, ¬(d.minCol ≤ k ∧ k < d.maxCol)

Docstring: A tiling has a fault at column k if there is a vertical line between columns k and k+1
that does not cross any domino. Equivalently, no domino spans columns k and k+1. 

## PROJECT DEPENDENCY DominoTilings.DominoTiling.mk (constructor)
{n m : ℕ} →
  (dominos : Finset DominoTilings.Domino) →
    (∀ d ∈ dominos, d.cells ⊆ DominoTilings.Rectangle n m) →
      dominos.biUnion DominoTilings.Domino.cells = DominoTilings.Rectangle n m →
        (∀ d₁ ∈ dominos, ∀ d₂ ∈ dominos, d₁ ≠ d₂ → Disjoint d₁.cells d₂.cells) → DominoTilings.DominoTiling n m

## PROJECT DEPENDENCY DominoTilings.Domino (inductive)
Type

Body:
DominoTilings.Domino.mk : (cell1 cell2 : DominoTilings.Cell) →
  cell1 ≠ cell2 →
    cell1.1 = cell2.1 ∧ (cell1.2 + 1 = cell2.2 ∨ cell2.2 + 1 = cell1.2) ∨
        cell1.2 = cell2.2 ∧ (cell1.1 + 1 = cell2.1 ∨ cell2.1 + 1 = cell1.1) →
      DominoTilings.Domino

Docstring: A domino is a pair of adjacent cells, either horizontal or vertical. 

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

## PROJECT DEPENDENCY DominoTilings.DominoTiling.dominos (def)
{n m : ℕ} → DominoTilings.DominoTiling n m → Finset DominoTilings.Domino

Body:
fun n m self => self.1

Docstring: The set of dominos in the tiling 

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

## BASE-LIBRARY REF Even
{α : Type u_2} → [Add α] → α → Prop

Body:
fun {α} [Add α] a => ∃ r, a = r + r

Docstring: An element `a` of a type `α` with addition satisfies `Even a` if `a = r + r`,
for some `r : α`. 

## BASE-LIBRARY REF Nat.add
ℕ → ℕ → ℕ

Body:
fun x x_1 =>
  Nat.brecOn (motive := fun x => ℕ → ℕ) x_1
    (fun x f x_2 =>
      (match (motive := ℕ → (x : ℕ) → Nat.below (motive := fun x => ℕ → ℕ) x → ℕ) x_2, x with
        | a, Nat.zero => fun x => a
        | a, b.succ => fun x => (x.1 a).succ)
        f)
    x

Docstring: Addition of natural numbers, typically used via the `+` operator.

This function is overridden in both the kernel and the compiler to efficiently evaluate using the
arbitrary-precision arithmetic library. The definition provided here is the logical model.


## BASE-LIBRARY REF Nat.le
ℕ → ℕ → Prop

Docstring: Non-strict, or weak, inequality of natural numbers, usually accessed via the `≤` operator.


## BASE-LIBRARY REF Nat.lt
ℕ → ℕ → Prop

Body:
fun n m => n.succ.le m

Docstring: Strict inequality of natural numbers, usually accessed via the `<` operator.

It is defined as `n < m = n + 1 ≤ m`.


## BASE-LIBRARY REF Union.union
{α : Type u} → [self : Union α] → α → α → α

Body:
fun α [self : Union α] => self.1

Docstring: `a ∪ b` is the union of `a` and `b`. 

Conventions for notations in identifiers:

 * The recommended spelling of `∪` in identifiers is `union`.

## BASE-LIBRARY REF Finset
Type u_4 → Type u_4

Docstring: `Finset α` is the type of finite sets of elements of `α`. It is implemented
as a multiset (a list up to permutation) which has no duplicate elements. 

## BASE-LIBRARY REF Finset.instUnion
{α : Type u_1} → [DecidableEq α] → Union (Finset α)

Body:
fun {α} [DecidableEq α] => { union := fun s t => { val := s.val.ndunion t.val, nodup := ⋯ } }

Docstring: `s ∪ t` is the set such that `a ∈ s ∪ t` iff `a ∈ s` or `a ∈ t`. 

## BASE-LIBRARY REF Singleton.singleton
{α : outParam (Type u)} → {β : Type v} → [self : Singleton α β] → α → β

Body:
fun {α} β [self : Singleton α β] => self.1

Docstring: `singleton x` is a collection with the single element `x` (notation: `{x}`). 

Conventions for notations in identifiers:

 * The recommended spelling of `{x}` in identifiers is `singleton`.

## BASE-LIBRARY REF Finset.instSingleton
{α : Type u_1} → Singleton α (Finset α)

Body:
fun {α} => { singleton := fun a => { val := {a}, nodup := ⋯ } }

Docstring: `{a} : Finset a` is the set `{a}` containing `a` and nothing else.

This differs from `insert a ∅` in that it does not require a `DecidableEq` instance for `α`.


## BASE-LIBRARY REF Multiset
Type u → Type u

Body:
fun α => Quotient (List.isSetoid α)

Docstring: `Multiset α` is the quotient of `List α` by list permutation. The result
is a type of finite sets with duplicates allowed. 

## BASE-LIBRARY REF Finset.val
{α : Type u_4} → Finset α → Multiset α

Body:
fun α self => self.1

Docstring: The underlying multiset 

## BASE-LIBRARY REF HasSubset.Subset
{α : Type u} → [self : HasSubset α] → α → α → Prop

Body:
fun α [self : HasSubset α] => self.1

Docstring: Subset relation: `a ⊆ b`  

Conventions for notations in identifiers:

 * The recommended spelling of `⊆` in identifiers is `subset`.

## BASE-LIBRARY REF Finset.instHasSubset
{α : Type u_1} → HasSubset (Finset α)

Body:
fun {α} => { Subset := fun s t => ∀ ⦃a : α⦄, a ∈ s → a ∈ t }

## BASE-LIBRARY REF Finset.biUnion
{α : Type u_1} → {β : Type u_2} → [DecidableEq β] → Finset α → (α → Finset β) → Finset β

Body:
fun {α} {β} [DecidableEq β] s t => (s.val.bind fun a => (t a).val).toFinset

Docstring: `Finset.biUnion s t` is the union of `t a` over `a ∈ s`.

(This was formerly `bind` due to the monad structure on types with `DecidableEq`.) 

## BASE-LIBRARY REF Prod
Type u → Type v → Type (max u v)

Docstring: The product type, usually written `α × β`. Product types are also called pair or tuple types.
Elements of this type are pairs in which the first element is an `α` and the second element is a
`β`.

Products nest to the right, so `(x, y, z) : α × β × γ` is equivalent to `(x, (y, z)) : α × (β × γ)`.


Conventions for notations in identifiers:

 * The recommended spelling of `×` in identifiers is `Prod`.

## BASE-LIBRARY REF instDecidableEqProd.match_3
{α : Type u_1} →
  {β : Type u_2} → (motive : α × β → Sort u_3) → (x : α × β) → ((a' : α) → (b' : β) → motive (a', b')) → motive x

Body:
fun {α} {β} motive x h_1 => Prod.casesOn x fun fst snd => h_1 fst snd

## BASE-LIBRARY REF instDecidableEqProd.match_1
{β : Type u_1} →
  (b b' : β) →
    (motive : Decidable (b = b') → Sort u_2) →
      (x : Decidable (b = b')) →
        ((e₂ : b = b') → motive (isTrue e₂)) → ((n₂ : ¬b = b') → motive (isFalse n₂)) → motive x

Body:
fun {β} b b' motive x h_1 h_2 => Decidable.casesOn x (fun h => h_2 h) fun h => h_1 h

## BASE-LIBRARY REF decEq
{α : Sort u} → [inst : DecidableEq α] → (a b : α) → Decidable (a = b)

Body:
fun {α} [inst : DecidableEq α] a b => inst a b

Docstring: Checks whether two terms of a type are equal using the type's `DecidableEq` instance.


## BASE-LIBRARY REF Decidable.isTrue
{p : Prop} → p → Decidable p

Docstring: Proves that `p` is decidable by supplying a proof of `p` 

## BASE-LIBRARY REF instDecidableEqProd._proof_1
∀ {α : Type u_2} {β : Type u_1} (a : α) (b : β) (a' : α) (b' : β), a = a' → b = b' → (a, b) = (a', b')

## BASE-LIBRARY REF Decidable.isFalse
{p : Prop} → ¬p → Decidable p

Docstring: Proves that `p` is decidable by supplying a proof of `¬p` 

## BASE-LIBRARY REF instDecidableEqProd._proof_2
∀ {α : Type u_2} {β : Type u_1} (a : α) (b : β) (a' : α) (b' : β), ¬b = b' → (a, b) = (a', b') → False

## BASE-LIBRARY REF instDecidableEqProd._proof_3
∀ {α : Type u_2} {β : Type u_1} (a : α) (b : β) (a' : α) (b' : β), ¬a = a' → (a, b) = (a', b') → False

## BASE-LIBRARY REF Nat.decEq
(n m : ℕ) → Decidable (n = m)

Body:
fun n m =>
  match h : n.beq m with
  | true => isTrue ⋯
  | false => isFalse ⋯

Docstring: A decision procedure for equality of natural numbers, usually accessed via the `DecidableEq Nat`
instance.

This function is overridden in both the kernel and the compiler to efficiently evaluate using the
arbitrary-precision arithmetic library. The definition provided here is the logical model.

Examples:
 * `Nat.decEq 5 5 = isTrue rfl`
 * `(if 3 = 4 then "yes" else "no") = "no"`
 * `show 12 = 12 by decide`


## BASE-LIBRARY REF Disjoint
{α : Type u_1} → [inst : PartialOrder α] → [OrderBot α] → α → α → Prop

Body:
fun {α} [PartialOrder α] [OrderBot α] a b => ∀ ⦃x : α⦄, x ≤ a → x ≤ b → x ≤ ⊥

Docstring: Two elements of a lattice are disjoint if their inf is the bottom element.
  (This generalizes disjoint sets, viewed as members of the subset lattice.)

Note that we define this without reference to `⊓`, as this allows us to talk about orders where
the infimum is not unique, or where implementing `Inf` would require additional `Decidable`
arguments. 

## BASE-LIBRARY REF Finset.partialOrder
{α : Type u_1} → PartialOrder (Finset α)

Body:
fun {α} => inferInstance

## BASE-LIBRARY REF PartialOrder
Type u_2 → Type u_2

Docstring: A partial order is a reflexive, transitive, antisymmetric relation `≤`. 

## BASE-LIBRARY REF Finset.instPartialOrder
{α : Type u_1} → PartialOrder (Finset α)

Body:
fun {α} => PartialOrder.ofSetLike (Finset α) α

## BASE-LIBRARY REF Finset.instOrderBot
{α : Type u_1} → OrderBot (Finset α)

Body:
fun {α} => { bot := ∅, bot_le := ⋯ }

## BASE-LIBRARY REF EmptyCollection.emptyCollection
{α : Type u} → [self : EmptyCollection α] → α

Body:
fun α [self : EmptyCollection α] => self.1

Docstring: `∅` or `{}` is the empty set or empty collection.
It is supported by the `EmptyCollection` typeclass. 

Conventions for notations in identifiers:

 * The recommended spelling of `{}` in identifiers is `empty`.

 * The recommended spelling of `∅` in identifiers is `empty`.

## BASE-LIBRARY REF Finset.instEmptyCollection
{α : Type u_1} → EmptyCollection (Finset α)

Body:
fun {α} => { emptyCollection := Finset.empty }

## BASE-LIBRARY REF Finset.empty_subset
∀ {α : Type u_1} (s : Finset α), ∅ ⊆ s

## BASE-LIBRARY REF Prod.fst
{α : Type u} → {β : Type v} → α × β → α

Body:
fun α β self => self.1

Docstring: The first element of a pair. 

## BASE-LIBRARY REF Add
Type u → Type u

Docstring: The homogeneous version of `HAdd`: `a + b : α` where `a b : α`. 

## BASE-LIBRARY REF Add.add
{α : Type u} → [self : Add α] → α → α → α

Body:
fun α [self : Add α] => self.1

Docstring: `a + b` computes the sum of `a` and `b`. See `HAdd`. 

## BASE-LIBRARY REF Prod.snd
{α : Type u} → {β : Type v} → α × β → β

Body:
fun α β self => self.2

Docstring: The second element of a pair. 

## BASE-LIBRARY REF Finset.map
{α : Type u_1} → {β : Type u_2} → (α ↪ β) → Finset α → Finset β

Body:
fun {α} {β} f s => { val := Multiset.map (⇑f) s.val, nodup := ⋯ }

Docstring: When `f` is an embedding of `α` in `β` and `s` is a finset in `α`, then `s.map f` is the image
finset in `β`. The embedding condition guarantees that there are no duplicates in the image. 

## BASE-LIBRARY REF Mul
Type u → Type u

Docstring: The homogeneous version of `HMul`: `a * b : α` where `a b : α`. 

## BASE-LIBRARY REF Mul.mul
{α : Type u} → [self : Mul α] → α → α → α

Body:
fun α [self : Mul α] => self.1

Docstring: `a * b` computes the product of `a` and `b`. See `HMul`. 

## BASE-LIBRARY REF Nat.mul
ℕ → ℕ → ℕ

Body:
fun x x_1 =>
  Nat.brecOn (motive := fun x => ℕ → ℕ) x_1
    (fun x f x_2 =>
      (match (motive := ℕ → (x : ℕ) → Nat.below (motive := fun x => ℕ → ℕ) x → ℕ) x_2, x with
        | x, 0 => fun x => 0
        | a, b.succ => fun x => (x.1 a).add a)
        f)
    x

Docstring: Multiplication of natural numbers, usually accessed via the `*` operator.

This function is overridden in both the kernel and the compiler to efficiently evaluate using the
arbitrary-precision arithmetic library. The definition provided here is the logical model.


## BASE-LIBRARY REF Finset.range
ℕ → Finset ℕ

Body:
fun n => { val := Multiset.range n, nodup := ⋯ }

Docstring: `range n` is the set of natural numbers less than `n`. 

## BASE-LIBRARY REF Div
Type u → Type u

Docstring: The homogeneous version of `HDiv`: `a / b : α` where `a b : α`. 

## BASE-LIBRARY REF Div.div
{α : Type u} → [self : Div α] → α → α → α

Body:
fun α [self : Div α] => self.1

Docstring: `a / b` computes the result of dividing `a` by `b`. See `HDiv`. 

## BASE-LIBRARY REF Nat.instDiv
Div ℕ

Body:
{ div := Nat.div }

## BASE-LIBRARY REF Nat.div
ℕ → ℕ → ℕ

Body:
fun x y => if hy : 0 < y then Nat.div.go y hy x.succ x ⋯ else 0

Docstring: Division of natural numbers, discarding the remainder. Division by `0` returns `0`. Usually accessed
via the `/` operator.

This operation is sometimes called “floor division.”

This function is overridden at runtime with an efficient implementation. This definition is
the logical model.

Examples:
 * `21 / 3 = 7`
 * `21 / 5 = 4`
 * `0 / 22 = 0`
 * `5 / 0 = 0`


## BASE-LIBRARY REF Sub
Type u → Type u

Docstring: The homogeneous version of `HSub`: `a - b : α` where `a b : α`. 

## BASE-LIBRARY REF Sub.sub
{α : Type u} → [self : Sub α] → α → α → α

Body:
fun α [self : Sub α] => self.1

Docstring: `a - b` computes the difference of `a` and `b`. See `HSub`. 

## BASE-LIBRARY REF instSubNat
Sub ℕ

Body:
{ sub := Nat.sub }

Characterization: Natural subtraction truncates: `a - b = 0` whenever `b ≥ a`.

## BASE-LIBRARY REF Nat.sub
ℕ → ℕ → ℕ

Body:
fun x x_1 =>
  Nat.brecOn (motive := fun x => ℕ → ℕ) x_1
    (fun x f x_2 =>
      (match (motive := ℕ → (x : ℕ) → Nat.below (motive := fun x => ℕ → ℕ) x → ℕ) x_2, x with
        | a, 0 => fun x => a
        | a, b.succ => fun x => (x.1 a).pred)
        f)
    x

Docstring: Subtraction of natural numbers, truncated at `0`. Usually used via the `-` operator.

If a result would be less than zero, then the result is zero.

This definition is overridden in both the kernel and the compiler to efficiently evaluate using the
arbitrary-precision arithmetic library. The definition provided here is the logical model.

Examples:
* `5 - 3 = 2`
* `8 - 2 = 6`
* `8 - 8 = 0`
* `8 - 20 = 0`


Characterization: Natural subtraction truncates: `a - b = 0` whenever `b ≥ a`.

## BASE-LIBRARY REF Insert.insert
{α : outParam (Type u)} → {γ : Type v} → [self : Insert α γ] → α → γ → γ

Body:
fun {α} γ [self : Insert α γ] => self.1

Docstring: `insert x xs` inserts the element `x` into the collection `xs`. 

## BASE-LIBRARY REF Finset.instInsert
{α : Type u_1} → [DecidableEq α] → Insert α (Finset α)

Body:
fun {α} [DecidableEq α] => { insert := fun a s => { val := Multiset.ndinsert a s.val, nodup := ⋯ } }

Docstring: `insert a s` is the set `{a} ∪ s` containing `a` and the elements of `s`. 

## BASE-LIBRARY REF SProd.sprod
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : SProd α β γ] → α → β → γ

Body:
fun α β {γ} [self : SProd α β γ] => self.1

Docstring: The Cartesian product `s ×ˢ t` is the set of `(a, b)` such that `a ∈ s` and `b ∈ t`. 

## BASE-LIBRARY REF Finset.instSProd
{α : Type u_1} → {β : Type u_2} → SProd (Finset α) (Finset β) (Finset (α × β))

Body:
fun {α} {β} => { sprod := Finset.product }

## BASE-LIBRARY REF Finset.product
{α : Type u_1} → {β : Type u_2} → Finset α → Finset β → Finset (α × β)

Body:
fun {α} {β} s t => { val := s.val ×ˢ t.val, nodup := ⋯ }

Docstring: `product s t` is the set of pairs `(a, b)` such that `a ∈ s` and `b ∈ t`. 

## BASE-LIBRARY REF Min.min
{α : Type u} → [self : Min α] → α → α → α

Body:
fun α [self : Min α] => self.1

Docstring: Returns the lesser of its two arguments. 

Conventions for notations in identifiers:

 * The recommended spelling of `min` in identifiers is `min`.

 * The recommended spelling of `⊓` in identifiers is `inf` (`⊓` is the preferred notation for `min` when the type is not linearly ordered.).

## BASE-LIBRARY REF minOfLe
{α : Type u_1} → [inst : LE α] → [DecidableRel LE.le] → Min α

Body:
fun {α} [LE α] [DecidableRel LE.le] => { min := fun x y => if x ≤ y then x else y }

Docstring: Constructs a `Min` instance from a decidable `≤` operation.


## BASE-LIBRARY REF Nat.decLe
(n m : ℕ) → Decidable (n ≤ m)

Body:
fun n m => if h : n.ble m = true then isTrue ⋯ else isFalse ⋯

Docstring: A decision procedure for non-strict inequality of natural numbers, usually accessed via the
`DecidableLE Nat` instance.

Examples:
 * `(if 3 ≤ 4 then "yes" else "no") = "yes"`
 * `(if 6 ≤ 4 then "yes" else "no") = "no"`
 * `show 12 ≤ 12 by decide`
 * `show 5 ≤ 12 by decide`


## BASE-LIBRARY REF Max.max
{α : Type u} → [self : Max α] → α → α → α

Body:
fun α [self : Max α] => self.1

Docstring: Returns the greater of its two arguments. 

Conventions for notations in identifiers:

 * The recommended spelling of `max` in identifiers is `max`.

 * The recommended spelling of `⊔` in identifiers is `sup` (`⊔` is the preferred notation for `max` when the type is not linearly ordered.).

## BASE-LIBRARY REF Nat.instMax
Max ℕ

Body:
maxOfLe

## BASE-LIBRARY REF maxOfLe
{α : Type u_1} → [inst : LE α] → [DecidableRel LE.le] → Max α

Body:
fun {α} [LE α] [DecidableRel LE.le] => { max := fun x y => if x ≤ y then y else x }

Docstring: Constructs a `Max` instance from a decidable `≤` operation.


## BASE-LIBRARY REF dite
{α : Sort u} → (c : Prop) → [h : Decidable c] → (c → α) → (¬c → α) → α

Body:
fun {α} c [h : Decidable c] t e => Decidable.casesOn h e t

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

Body:
fun {α} {a} {motive} m {b} h => h ▸ m

Docstring: Non-dependent recursor for the equality type. 

## INFORMAL STATEMENT
lem.details.domino.TilingB-faultfree

\leanhelper  For each even $n \ge 2$, the tiling $B_n$ is faultfree.

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
  "verdict": "unclear",
  "discrepancies": [],
  "justification": "The informal claim says only \u201cthe tiling $B_n$ is faultfree,\u201d but the package supplies no INFORMAL DEFINITION of \u201cfaultfree\u201d or of a fault. The formal predicate unfolds to `\u2200 k \u2265 1, k < n \u2192 \u00acT.hasFaultAt k`, where `hasFaultAt k` means `k \u2265 1 \u2227 k < n \u2227 \u2200 d \u2208 T.dominos, \u00ac(d.minCol \u2264 k \u2227 k < d.maxCol)`. Although the formal `TilingB` body matches the supplied reflected construction of $B_n$, there is no blueprint-side definition with which to compare this formal notion of faultfreeness. An informal definition of faults/faultfree is needed to decide faithfulness."
}