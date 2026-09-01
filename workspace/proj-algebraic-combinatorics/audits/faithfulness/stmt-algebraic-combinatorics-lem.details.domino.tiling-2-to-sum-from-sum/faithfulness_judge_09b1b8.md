## TARGET DominoTilings.DominoTiling.tiling_2_to_sum_from_sum (theorem) — ELABORATED SIGNATURE
∀ {n : ℕ} (x : DominoTilings.DominoTiling n 2 ⊕ DominoTilings.DominoTiling (n + 1) 2),
  (DominoTilings.DominoTiling.tiling_2_from_sum x).tiling_2_to_sum = x

Docstring: The roundtrip `tiling_2_to_sum (tiling_2_from_sum x) = x`.
This is the key property establishing that `tiling_2_from_sum` is a right inverse
of `tiling_2_to_sum`, which proves surjectivity of `tiling_2_to_sum` and
injectivity of `tiling_2_from_sum`. 

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

## PROJECT DEPENDENCY DominoTilings.DominoTiling.tiling_2_to_sum (def)
{n : ℕ} → DominoTilings.DominoTiling (n + 2) 2 → DominoTilings.DominoTiling n 2 ⊕ DominoTilings.DominoTiling (n + 1) 2

Body:
fun {n} T =>
  if hv : T.hasVerticalFirstColumn then
    let v := Classical.choose hv;
    have hv_spec := ⋯;
    have hv_mem := ⋯;
    have hv_cells := ⋯;
    Sum.inr (T.restrictAfterVerticalGen v hv_mem hv_cells)
  else
    have hpair := ⋯;
    let d1 := Classical.choose ⋯;
    have hd1_spec := ⋯;
    have hd1_mem := ⋯;
    have hd1_cells := ⋯;
    let d2 := Classical.choose ⋯;
    have hd2_spec := ⋯;
    have hd2_mem := ⋯;
    have hd2_cells := ⋯;
    Sum.inl (T.restrictAfterHorizontalPairGen d1 d2 hd1_mem hd2_mem hd1_cells hd2_cells)

Docstring: Forward map for the Fibonacci recurrence bijection.
Maps a 2×(n+2) tiling to either:
- `inl T'` where T' is a 2×n tiling (horizontal case)
- `inr T'` where T' is a 2×(n+1) tiling (vertical case) 

## PROJECT DEPENDENCY DominoTilings.DominoTiling.tiling_2_from_sum (def)
{n : ℕ} → DominoTilings.DominoTiling n 2 ⊕ DominoTilings.DominoTiling (n + 1) 2 → DominoTilings.DominoTiling (n + 2) 2

Body:
fun {n} => Sum.elim DominoTilings.DominoTiling.prependHorizontalPair DominoTilings.DominoTiling.prependVertical

Docstring: Backward map for the Fibonacci recurrence bijection.
Maps a sum to a 2×(n+2) tiling by prepending dominos. 

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

## PROJECT DEPENDENCY DominoTilings.DominoTiling.hasVerticalFirstColumn (def)
{n : ℕ} → DominoTilings.DominoTiling (n + 2) 2 → Prop

Body:
fun {n} T => ∃ d ∈ T.dominos, d.cells = {(1, 1), (1, 2)}

Docstring: A tiling has a vertical first column if some domino covers cells (1,1) and (1,2). 

## PROJECT DEPENDENCY DominoTilings.DominoTiling.instDecidableHasVerticalFirstColumn (def)
{n : ℕ} → (T : DominoTilings.DominoTiling (n + 2) 2) → Decidable T.hasVerticalFirstColumn

Body:
fun {n} T => id inferInstance

## PROJECT DEPENDENCY DominoTilings.DominoTiling.dominos (def)
{n m : ℕ} → DominoTilings.DominoTiling n m → Finset DominoTilings.Domino

Body:
fun n m self => self.1

Docstring: The set of dominos in the tiling 

## PROJECT DEPENDENCY DominoTilings.DominoTiling.restrictAfterVerticalGen (def)
{n : ℕ} →
  (T : DominoTilings.DominoTiling (n + 1) 2) →
    (v : DominoTilings.Domino) →
      v ∈ T.dominos → v.cells = DominoTilings.vertical_1_1.cells → DominoTilings.DominoTiling n 2

Body:
fun {n} T v hv hv_cells =>
  {
    dominos :=
      Finset.image
        (fun x =>
          match x with
          | ⟨d, hd⟩ =>
            have hd' := ⋯;
            have hcols := ⋯;
            d.shiftNeg 1 ⋯ ⋯)
        (T.dominos.erase v).attach,
    dominos_in_rect := ⋯, covers_all := ⋯, pairwise_disjoint := ⋯ }

Docstring: Generalized version of restrictAfterVertical that works with any domino v
having cells = {(1,1), (1,2)}. 

## PROJECT DEPENDENCY DominoTilings.DominoTiling.horizontalPair_of_not_hasVerticalFirstColumn (theorem)
∀ {n : ℕ} (T : DominoTilings.DominoTiling (n + 2) 2),
  ¬T.hasVerticalFirstColumn →
    (∃ d₁ ∈ T.dominos, d₁.cells = {(1, 1), (2, 1)}) ∧ ∃ d₂ ∈ T.dominos, d₂.cells = {(1, 2), (2, 2)}

Docstring: If a tiling doesn't have a vertical first column, then it has a horizontal pair. 

## PROJECT DEPENDENCY DominoTilings.DominoTiling.restrictAfterHorizontalPairGen (def)
{n : ℕ} →
  (T : DominoTilings.DominoTiling (n + 2) 2) →
    (d1 d2 : DominoTilings.Domino) →
      d1 ∈ T.dominos →
        d2 ∈ T.dominos → d1.cells = {(1, 1), (2, 1)} → d2.cells = {(1, 2), (2, 2)} → DominoTilings.DominoTiling n 2

Body:
fun {n} T d1 d2 hd1 hd2 hd1_cells hd2_cells =>
  {
    dominos :=
      Finset.image
        (fun x =>
          match x with
          | ⟨d, hd⟩ =>
            have hd' := ⋯;
            have hd'' := ⋯;
            have hcols := ⋯;
            d.shiftNeg 2 ⋯ ⋯)
        ((T.dominos.erase d1).erase d2).attach,
    dominos_in_rect := ⋯, covers_all := ⋯, pairwise_disjoint := ⋯ }

Docstring: Generalized version of restrictAfterHorizontalPair that works with any dominos d1, d2
having the appropriate cells. 

## PROJECT DEPENDENCY DominoTilings.DominoTiling.prependHorizontalPair (def)
{n : ℕ} → DominoTilings.DominoTiling n 2 → DominoTilings.DominoTiling (n + 2) 2

Body:
fun {n} T =>
  {
    dominos :=
      insert DominoTilings.horizontal_1_1
        (insert DominoTilings.horizontal_1_2 (Finset.image (fun d => d.shiftNat 2) T.dominos)),
    dominos_in_rect := ⋯, covers_all := ⋯, pairwise_disjoint := ⋯ }

Docstring: Prepend two horizontal dominos at (1,1)-(2,1) and (1,2)-(2,2) to a tiling of Rectangle n 2,
creating a tiling of Rectangle (n+2) 2.

This is one of the inverse maps in the Fibonacci recurrence bijection.
The two horizontal dominos cover the first two columns, creating a fault at x=2. 

## PROJECT DEPENDENCY DominoTilings.DominoTiling.prependVertical (def)
{n : ℕ} → DominoTilings.DominoTiling n 2 → DominoTilings.DominoTiling (n + 1) 2

Body:
fun {n} T =>
  { dominos := insert DominoTilings.vertical_1_1 (Finset.image (fun d => d.shiftNat 1) T.dominos), dominos_in_rect := ⋯,
    covers_all := ⋯, pairwise_disjoint := ⋯ }

Docstring: Prepend a vertical domino at (1,1)-(1,2) to a tiling of Rectangle n 2,
creating a tiling of Rectangle (n+1) 2.

This is one of the inverse maps in the Fibonacci recurrence bijection.
The vertical domino covers the entire first column, creating a fault at x=1. 

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

## PROJECT DEPENDENCY DominoTilings.Domino.shiftNeg (def)
(d : DominoTilings.Domino) → (k : ℕ) → d.cell1.1 ≥ k + 1 → d.cell2.1 ≥ k + 1 → DominoTilings.Domino

Body:
fun d k h1 h2 =>
  { cell1 := (d.cell1.1 - k, d.cell1.2), cell2 := (d.cell2.1 - k, d.cell2.2), distinct := ⋯, adjacent := ⋯ }

Docstring: Shift a domino k columns to the left. Requires that both cells have column ≥ k+1. 

## PROJECT DEPENDENCY DominoTilings.horizontal_1_1 (def)
DominoTilings.Domino

Body:
{ cell1 := (1, 1), cell2 := (2, 1), distinct := DominoTilings.horizontal_1_1._proof_1,
  adjacent := DominoTilings.horizontal_1_1._proof_2 }

Docstring: The horizontal domino covering row 1, columns 1-2: cells (1,1) and (2,1). 

## PROJECT DEPENDENCY DominoTilings.horizontal_1_2 (def)
DominoTilings.Domino

Body:
{ cell1 := (1, 2), cell2 := (2, 2), distinct := DominoTilings.horizontal_1_2._proof_1,
  adjacent := DominoTilings.horizontal_1_2._proof_2 }

Docstring: The horizontal domino covering row 2, columns 1-2: cells (1,2) and (2,2). 

## PROJECT DEPENDENCY DominoTilings.Domino.shiftNat (def)
DominoTilings.Domino → ℕ → DominoTilings.Domino

Body:
fun d k => { cell1 := (d.cell1.1 + k, d.cell1.2), cell2 := (d.cell2.1 + k, d.cell2.2), distinct := ⋯, adjacent := ⋯ }

Docstring: Shift a domino k columns to the right. 

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


## BASE-LIBRARY REF Sum
Type u → Type v → Type (max u v)

Docstring: The disjoint union of types `α` and `β`, ordinarily written `α ⊕ β`.

An element of `α ⊕ β` is either an `a : α` wrapped in `Sum.inl` or a `b : β` wrapped in `Sum.inr`.
`α ⊕ β` is not equivalent to the set-theoretic union of `α` and `β` because its values include an
indication of which of the two types was chosen. The union of a singleton set with itself contains
one element, while `Unit ⊕ Unit` contains distinct values `inl ()` and `inr ()`.


## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

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


## BASE-LIBRARY REF Classical.choose
{α : Sort u} → {p : α → Prop} → (∃ x, p x) → α

Docstring: Given that there exists an element satisfying `p`, returns one such element.

This is a straightforward consequence of, and equivalent to, `Classical.choice`.

See also `choose_spec`, which asserts that the returned value has property `p`.


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

## BASE-LIBRARY REF Prod
Type u → Type v → Type (max u v)

Docstring: The product type, usually written `α × β`. Product types are also called pair or tuple types.
Elements of this type are pairs in which the first element is an `α` and the second element is a
`β`.

Products nest to the right, so `(x, y, z) : α × β × γ` is equivalent to `(x, (y, z)) : α × (β × γ)`.


Conventions for notations in identifiers:

 * The recommended spelling of `×` in identifiers is `Prod`.

## BASE-LIBRARY REF Finset.instInsert
{α : Type u_1} → [DecidableEq α] → Insert α (Finset α)

Docstring: `insert a s` is the set `{a} ∪ s` containing `a` and the elements of `s`. 

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

## BASE-LIBRARY REF Finset.instSingleton
{α : Type u_1} → Singleton α (Finset α)

Docstring: `{a} : Finset a` is the set `{a}` containing `a` and nothing else.

This differs from `insert a ∅` in that it does not require a `DecidableEq` instance for `α`.


## BASE-LIBRARY REF Sum.inr
{α : Type u} → {β : Type v} → β → α ⊕ β

Docstring: Right injection into the sum type `α ⊕ β`. 

## BASE-LIBRARY REF Not
Prop → Prop

Docstring: `Not p`, or `¬p`, is the negation of `p`. It is defined to be `p → False`,
so if your goal is `¬p` you can use `intro h` to turn the goal into
`h : p ⊢ False`, and if you have `hn : ¬p` and `h : p` then `hn h : False`
and `(hn h).elim` will prove anything.
For more information: [Propositional Logic](https://lean-lang.org/theorem_proving_in_lean4/propositions_and_proofs.html#propositional-logic)


Conventions for notations in identifiers:

 * The recommended spelling of `¬` in identifiers is `not`.

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


## BASE-LIBRARY REF Sum.inl
{α : Type u} → {β : Type v} → α → α ⊕ β

Docstring: Left injection into the sum type `α ⊕ β`. 

## BASE-LIBRARY REF Sum.elim
{α : Type u_1} → {β : Type u_2} → {γ : Sort u_3} → (α → γ) → (β → γ) → α ⊕ β → γ

Docstring: Case analysis for sums that applies the appropriate function `f` or `g` after checking which
constructor is present.


## BASE-LIBRARY REF Or
Prop → Prop → Prop

Docstring: `Or a b`, or `a ∨ b`, is the disjunction of propositions. There are two
constructors for `Or`, called `Or.inl : a → a ∨ b` and `Or.inr : b → a ∨ b`,
and you can use `match` or `cases` to destruct an `Or` assumption into the
two cases.


Conventions for notations in identifiers:

 * The recommended spelling of `∨` in identifiers is `or`.

 * The recommended spelling of `\/` in identifiers is `or` (prefer `∨` over `\/`).

## BASE-LIBRARY REF Prod.fst
{α : Type u} → {β : Type v} → α × β → α

Docstring: The first element of a pair. 

## BASE-LIBRARY REF Prod.snd
{α : Type u} → {β : Type v} → α × β → β

Docstring: The second element of a pair. 

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


## BASE-LIBRARY REF id
{α : Sort u} → α → α

Docstring: The identity function. `id` takes an implicit argument `α : Sort u`
(a type in any universe), and an argument `a : α`, and returns `a`.

Although this may look like a useless function, one application of the identity
function is to explicitly put a type on an expression. If `e` has type `T`,
and `T'` is definitionally equal to `T`, then `@id T' e` typechecks, and Lean
knows that this expression has type `T'` rather than `T`. This can make a
difference for typeclass inference, since `T` and `T'` may have different
typeclass instances on them. `show T' from e` is sugar for an `@id T' e`
expression.


## BASE-LIBRARY REF inferInstance
{α : Sort u} → [i : α] → α

Docstring: `inferInstance` synthesizes a value of any target type by typeclass
inference. This function has the same type signature as the identity
function, but the square brackets on the `[i : α]` argument means that it will
attempt to construct this argument by typeclass inference. (This will fail if
`α` is not a `class`.) Example:
```
#check (inferInstance : Inhabited Nat) -- Inhabited Nat

def foo : Inhabited (Nat × Nat) :=
  inferInstance

example : foo.default = (default, default) :=
  rfl
```


## BASE-LIBRARY REF Finset.decidableExistsAndFinset
{α : Type u_1} → {s : Finset α} → {p : α → Prop} → [_hp : (a : α) → Decidable (p a)] → Decidable (∃ a ∈ s, p a)

## BASE-LIBRARY REF Finset.decidableEq
{α : Type u_1} → [DecidableEq α] → DecidableEq (Finset α)

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

## BASE-LIBRARY REF GE.ge
{α : Type u} → [LE α] → α → α → Prop

Docstring: `a ≥ b` is an abbreviation for `b ≤ a`. 

Conventions for notations in identifiers:

 * The recommended spelling of `≥` in identifiers is `ge`.

 * The recommended spelling of `>=` in identifiers is `ge` (prefer `≥` over `>=`).

## BASE-LIBRARY REF instLENat
LE ℕ

## BASE-LIBRARY REF Finset.attach
{α : Type u_1} → (s : Finset α) → Finset { x // x ∈ s }

Docstring: `attach s` takes the elements of `s` and forms a new set of elements of the subtype
`{x // x ∈ s}`. 

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
lem.details.domino.tiling-2-to-sum-from-sum

\leanhelper  For every $x \in \mathrm{Tiling}(R_{n,2}) \sqcup \mathrm{Tiling}(R_{n+1,2})$, classifying the prepended tiling by its first-column structure and then restricting recovers $x$. This shows that the prepending map is injective and the classification map is surjective.

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
  "verdict": "faithful",
  "justification": "The elaborated signature quantifies without extra hypotheses: `\u2200 {n : \u2115} (x : DominoTiling n 2 \u2295 DominoTiling (n + 1) 2), (tiling_2_from_sum x).tiling_2_to_sum = x`. This exactly expresses the blueprint\u2019s \u201cFor every x \u2208 Tiling(R_{n,2}) \u2a3f Tiling(R_{n+1,2}), classifying the prepended tiling ... and then restricting recovers x.\u201d The dependency `tiling_2_from_sum` prepends the horizontal pair in the left summand and a vertical domino in the right summand, while `tiling_2_to_sum` classifies by `hasVerticalFirstColumn` and applies the corresponding restriction. Thus the displayed equality is precisely the claimed roundtrip. It also entails the stated injectivity of the prepending map and surjectivity of the classification map. The finite-set encoding of rectangles and tilings matches the informal definitions on these finite positive-coordinate rectangles; the ordered representation of a domino only gives a somewhat broader representation and does not add a restrictive hypothesis."
}