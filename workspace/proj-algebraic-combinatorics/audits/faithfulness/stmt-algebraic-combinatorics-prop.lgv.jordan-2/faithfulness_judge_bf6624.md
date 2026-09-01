## TARGET LGV1.no_nipats_under_nw (theorem) — ELABORATED SIGNATURE
∀ (A A' B B' : LGV1.LatticePoint),
  LGV1.isWeaklyNorthwestOf A' A → LGV1.isWeaklyNorthwestOf B' B → LGV1.numNipats2 A A' B' B = 0

Docstring: Under NW conditions, there are no nipats from (A,A') to (B',B).
Label: prop.lgv.jordan-2 

## TARGET LGV1.baby_jordan_curve (theorem) — ELABORATED SIGNATURE
∀ (A A' B B' : LGV1.LatticePoint),
  LGV1.isWeaklyNorthwestOf A' A →
    LGV1.isWeaklyNorthwestOf B' B →
      ∀ (p p' : LGV1.LatticePath), p.isPathFromTo A B' → p'.isPathFromTo A' B → ∃ v ∈ p.vertices A, v ∈ p'.vertices A'

Docstring: Baby Jordan curve theorem: Under NW conditions, paths must intersect.
(Proposition prop.lgv.jordan-2)
Label: prop.lgv.jordan-2

**Proof strategy** (from tex source, Section sec.details.det.comb):

The proof is by strong induction on ℓ(p) + ℓ(p'), the sum of path lengths.

**Base case**: If ℓ(p) + ℓ(p') = 0, then both paths are empty, so A = B' and A' = B.
From the NW conditions:
- A'.x ≤ A.x = B'.x ≤ B.x = A'.x, so A'.x = A.x
- A'.y ≥ A.y = B'.y ≥ B.y = A'.y, so A'.y = A.y
Thus A = A', and A is a common vertex.

**Induction step**: Assume the theorem holds for smaller path lengths.
If A = A', then A is a common vertex and we're done.
Otherwise, since A' is weakly NW of A and A ≠ A', we have either:
- Case 1: A'.y > A.y (A' strictly north of A)
- Case 2: A'.x < A.x (A' strictly west of A)

In Case 1 (A'.y > A.y):
- Let P be the next vertex after A on path p
- If the first step of p is north, then P = (A.x, A.y + 1)
- Since A'.y > A.y and integers, A'.y ≥ A.y + 1 = P.y
- So A' is still weakly NW of P
- The rest of p goes from P to B', and p' goes from A' to B
- By IH (with smaller path length), these paths intersect
- Any common vertex of (rest of p) and p' is also on p

- If the first step of p is east, then P = (A.x + 1, A.y)
- We need to look at the first step of p' and apply IH appropriately

Case 2 (A'.x < A.x) is symmetric, looking at the first step of p' instead.

The key insight is that the "river" created by path p from A to B' must be
crossed by path p' from A' to B, since A' is northwest of A and B' is
northwest of B.

Reference: https://math.stackexchange.com/questions/2870640/ 

## TARGET LGV1.isWeaklyNorthwestOf (def) — ELABORATED SIGNATURE
LGV1.LatticePoint → LGV1.LatticePoint → Prop

Body:
fun p q => p.x ≤ q.x ∧ p.y ≥ q.y

Docstring: Point p is weakly northwest of point q. 

## PROJECT DEPENDENCY LGV1.LatticePoint (def)
Type

Body:
ℤ × ℤ

Docstring: A point on the integer lattice ℤ².
The vertices of the integer lattice are pairs of integers.
Label: def.lgv.lattice 

## PROJECT DEPENDENCY LGV1.numNipats2 (def)
LGV1.LatticePoint → LGV1.LatticePoint → LGV1.LatticePoint → LGV1.LatticePoint → ℕ

Body:
fun A A' B B' =>
  have AB := ![A, A'];
  have BB := ![B, B'];
  (LGV1.nipatsFromTo AB BB).ncard

Docstring: Number of nipats from (A,A') to (B,B').
Defined as the cardinality of the set of non-intersecting path tuples. 

## PROJECT DEPENDENCY LGV1.LatticePath (def)
Type

Body:
List LGV1.LatticeStep

Docstring: A lattice path is a list of steps.

This type is equivalent to `LGV.LatticePath'` defined in LGV2.lean.
Conversion functions are provided:
- `latticePathToLatticePath' : LatticePath → LGV.LatticePath'`
- `latticePath'ToLatticePath : LGV.LatticePath' → LatticePath`
- `latticePathToLatticePath'_endpoint` proves endpoint preservation 

## PROJECT DEPENDENCY LGV1.LatticePath.isPathFromTo (def)
LGV1.LatticePath → LGV1.LatticePoint → LGV1.LatticePoint → Prop

Body:
fun path a b => path.endpoint a = b

Docstring: Check if a path goes from point a to point b. 

## PROJECT DEPENDENCY LGV1.LatticePath.vertices (def)
LGV1.LatticePath → LGV1.LatticePoint → List LGV1.LatticePoint

Body:
fun path start => (start :: List.scanl (fun p s => s.apply p) start path).tail

Docstring: All vertices visited by a path, including start and end. 

## PROJECT DEPENDENCY LGV1.LatticePoint.x (def)
LGV1.LatticePoint → ℤ

Body:
fun p => p.1

Docstring: The x-coordinate of a lattice point. 

## PROJECT DEPENDENCY LGV1.LatticePoint.y (def)
LGV1.LatticePoint → ℤ

Body:
fun p => p.2

Docstring: The y-coordinate of a lattice point. 

## PROJECT DEPENDENCY LGV1.kVertex (def)
ℕ → Type

Body:
fun k => Fin k → LGV1.LatticePoint

Docstring: A k-vertex is a k-tuple of lattice points.
Label: def.lgv.path-tups (a) 

## PROJECT DEPENDENCY LGV1.PathTuple (inductive)
(k : ℕ) → LGV1.kVertex k → LGV1.kVertex k → Type

Body:
LGV1.PathTuple.mk : {k : ℕ} →
  {A B : LGV1.kVertex k} →
    (paths : Fin k → LGV1.LatticePath) → (∀ (i : Fin k), (paths i).isPathFromTo (A i) (B i)) → LGV1.PathTuple k A B

Docstring: A path tuple from k-vertex A to k-vertex B.
Label: def.lgv.path-tups (c) 

## PROJECT DEPENDENCY LGV1.nipatsFromTo (def)
{k : ℕ} → (A B : LGV1.kVertex k) → Set (LGV1.PathTuple k A B)

Body:
fun {k} A B => {pt | pt.isNonIntersecting}

Docstring: The set of all non-intersecting path tuples (nipats) from A to B. 

## PROJECT DEPENDENCY LGV1.LatticeStep (inductive)
Type

Body:
LGV1.LatticeStep.east : LGV1.LatticeStep
LGV1.LatticeStep.north : LGV1.LatticeStep

Docstring: A step on the integer lattice: either east (right) or north (up).
- east: (i,j) → (i+1,j)
- north: (i,j) → (i,j+1)

This type is equivalent to `LGV.LatticeStep'` defined in LGV2.lean.
The equivalence is provided by `latticeStepEquiv : LatticeStep ≃ LGV.LatticeStep'`.

Label: eq.def.lgv.lattice.east, eq.def.lgv.lattice.north 

## PROJECT DEPENDENCY LGV1.LatticePath.endpoint (def)
LGV1.LatticePath → LGV1.LatticePoint → LGV1.LatticePoint

Body:
fun path start => List.foldl (fun p s => s.apply p) start path

Docstring: The endpoint of a path starting from a given point. 

## PROJECT DEPENDENCY LGV1.LatticeStep.apply (def)
LGV1.LatticeStep → LGV1.LatticePoint → LGV1.LatticePoint

Body:
fun s p =>
  match s with
  | LGV1.LatticeStep.east => (p.1 + 1, p.2)
  | LGV1.LatticeStep.north => (p.1, p.2 + 1)

Docstring: Apply a step to a lattice point. 

## PROJECT DEPENDENCY LGV1.PathTuple.isNonIntersecting (def)
{k : ℕ} → {A B : LGV1.kVertex k} → LGV1.PathTuple k A B → Prop

Body:
fun {k} {A B} pt => ∀ (i j : Fin k), i ≠ j → Disjoint (pt.verticesOf i) (pt.verticesOf j)

Docstring: A path tuple is non-intersecting (nipat) if no two distinct paths share a vertex.
Label: def.lgv.path-tups (d) 

## PROJECT DEPENDENCY LGV1.instReprLatticeStep.repr (def)
LGV1.LatticeStep → ℕ → Format

Body:
fun x prec =>
  match x with
  | LGV1.LatticeStep.east =>
    Repr.addAppParen (Format.nest (if prec ≥ 1024 then 1 else 2) (Std.Format.text "LGV1.LatticeStep.east")).group prec
  | LGV1.LatticeStep.north =>
    Repr.addAppParen (Format.nest (if prec ≥ 1024 then 1 else 2) (Std.Format.text "LGV1.LatticeStep.north")).group prec

## PROJECT DEPENDENCY LGV1.PathTuple.verticesOf (def)
{k : ℕ} → {A B : LGV1.kVertex k} → LGV1.PathTuple k A B → Fin k → Set LGV1.LatticePoint

Body:
fun {k} {A B} pt i => {p | p ∈ (pt.paths i).vertices (A i)}

Docstring: The set of vertices visited by a path in a path tuple. 

## PROJECT DEPENDENCY LGV1.PathTuple.paths (def)
{k : ℕ} → {A B : LGV1.kVertex k} → LGV1.PathTuple k A B → Fin k → LGV1.LatticePath

Body:
fun k A B self => self.1

Docstring: The i-th path in the tuple 

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

## BASE-LIBRARY REF Membership.mem
{α : outParam (Type u)} → {γ : Type v} → [self : Membership α γ] → γ → α → Prop

Docstring: The membership relation `a ∈ s : Prop` where `a : α`, `s : γ`. 

Conventions for notations in identifiers:

 * The recommended spelling of `∈` in identifiers is `mem`.

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


## BASE-LIBRARY REF List.instMembership
{α : Type u} → Membership α (List α)

## BASE-LIBRARY REF LE.le
{α : Type u} → [self : LE α] → α → α → Prop

Docstring: The less-equal relation: `x ≤ y` 

Conventions for notations in identifiers:

 * The recommended spelling of `≤` in identifiers is `le`.

 * The recommended spelling of `<=` in identifiers is `le` (prefer `≤` over `<=`).

## BASE-LIBRARY REF Int
Type

Docstring: The integers.

This type is special-cased by the compiler and overridden with an efficient implementation. The
runtime has a special representation for `Int` that stores “small” signed numbers directly, while
larger numbers use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)). A “small number” is an integer that can be encoded with one fewer bits
than the platform's pointer size (i.e. 63 bits on 64-bit architectures and 31 bits on 32-bit
architectures).


## BASE-LIBRARY REF Int.instLEInt
LE ℤ

## BASE-LIBRARY REF GE.ge
{α : Type u} → [LE α] → α → α → Prop

Docstring: `a ≥ b` is an abbreviation for `b ≤ a`. 

Conventions for notations in identifiers:

 * The recommended spelling of `≥` in identifiers is `ge`.

 * The recommended spelling of `>=` in identifiers is `ge` (prefer `≥` over `>=`).

## BASE-LIBRARY REF Prod
Type u → Type v → Type (max u v)

Docstring: The product type, usually written `α × β`. Product types are also called pair or tuple types.
Elements of this type are pairs in which the first element is an `α` and the second element is a
`β`.

Products nest to the right, so `(x, y, z) : α × β × γ` is equivalent to `(x, (y, z)) : α × (β × γ)`.


Conventions for notations in identifiers:

 * The recommended spelling of `×` in identifiers is `Prod`.

## BASE-LIBRARY REF Matrix.vecCons
{α : Type u} → {n : ℕ} → α → (Fin n → α) → Fin n.succ → α

Docstring: `vecCons h t` prepends an entry `h` to a vector `t`.

The inverse functions are `vecHead` and `vecTail`.
The notation `![a, b, ...]` expands to `vecCons a (vecCons b ...)`.


## BASE-LIBRARY REF Matrix.vecEmpty
{α : Type u} → Fin 0 → α

Docstring: `![]` is the vector with no entries. 

## BASE-LIBRARY REF Set.ncard
{α : Type u_1} → Set α → ℕ

Docstring: The cardinality of `s : Set α` . Has the junk value `0` if `s` is infinite 

## BASE-LIBRARY REF List.tail
{α : Type u} → List α → List α

Docstring: Drops the first element of a nonempty list, returning the tail. Returns `[]` when the argument is
empty.

Examples:
 * `["apple", "banana", "grape"].tail = ["banana", "grape"]`
 * `["apple"].tail = []`
 * `([] : List String).tail = []`


## BASE-LIBRARY REF List.cons
{α : Type u} → α → List α → List α

Docstring: The list whose first element is `head`, where `tail` is the rest of the list.
Usually written `head :: tail`.


Conventions for notations in identifiers:

 * The recommended spelling of `::` in identifiers is `cons`.

 * The recommended spelling of `[a]` in identifiers is `singleton`.

## BASE-LIBRARY REF List.scanl
{β : Type u_1} → {α : Type u_2} → (β → α → β) → β → List α → List β

Docstring: Fold a function `f` over the list from the left, returning the list of partial results.
```
scanl (+) 0 [1, 2, 3] = [0, 1, 3, 6]
```


## BASE-LIBRARY REF Prod.fst
{α : Type u} → {β : Type v} → α × β → α

Docstring: The first element of a pair. 

## BASE-LIBRARY REF Prod.snd
{α : Type u} → {β : Type v} → α × β → β

Docstring: The second element of a pair. 

## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


## BASE-LIBRARY REF Set
Type u → Type u

Docstring: A set is a collection of elements of some type `α`.

Although `Set` is defined as `α → Prop`, this is an implementation detail which should not be
relied on. Instead, `setOf` and membership of a set (`∈`) should be used to convert between sets
and predicates.


## BASE-LIBRARY REF setOf
{α : Type u} → (α → Prop) → Set α

Docstring: Turn a predicate `p : α → Prop` into a set, also written as `{x | p x}` 

## BASE-LIBRARY REF List.foldl
{α : Type u} → {β : Type v} → (α → β → α) → α → List β → α

Docstring: Folds a function over a list from the left, accumulating a value starting with `init`. The
accumulated value is combined with the each element of the list in order, using `f`.

Examples:
 * `[a, b, c].foldl f z  = f (f (f z a) b) c`
 * `[1, 2, 3].foldl (· ++ toString ·) "" = "123"`
 * `[1, 2, 3].foldl (s!"({·} {·})") "" = "((( 1) 2) 3)"`


## BASE-LIBRARY REF Unit
Type

Docstring: The canonical type with one element. This element is written `()`.

`Unit` has a number of uses:
* It can be used to model control flow that returns from a function call without providing other
  information.
* Monadic actions that return `Unit` have side effects without computing values.
* In polymorphic types, it can be used to indicate that no data is to be stored in a particular
  field.


## BASE-LIBRARY REF Prod.mk
{α : Type u} → {β : Type v} → α → β → α × β

Docstring: Constructs a pair. This is usually written `(x, y)` instead of `Prod.mk x y`.


Conventions for notations in identifiers:

 * The recommended spelling of `(a, b)` in identifiers is `mk`.

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

## BASE-LIBRARY REF instOfNat
{n : ℕ} → OfNat ℤ n

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

## BASE-LIBRARY REF ChainCompletePartialOrder.toPartialOrder
{α : Type u_2} → [self : ChainCompletePartialOrder α] → PartialOrder α

## BASE-LIBRARY REF ChainCompletePartialOrder.instOfCompleteLattice
{α : Type u_1} → [CompleteLattice α] → ChainCompletePartialOrder α

## BASE-LIBRARY REF CompleteBooleanAlgebra.toCompleteLattice
{α : Type u_1} → [self : CompleteBooleanAlgebra α] → CompleteLattice α

## BASE-LIBRARY REF CompleteAtomicBooleanAlgebra.toCompleteBooleanAlgebra
{α : Type u} → [self : CompleteAtomicBooleanAlgebra α] → CompleteBooleanAlgebra α

## BASE-LIBRARY REF Set.instCompleteAtomicBooleanAlgebra
{α : Type u_1} → CompleteAtomicBooleanAlgebra (Set α)

## BASE-LIBRARY REF HeytingAlgebra.toOrderBot
{α : Type u_4} → [self : HeytingAlgebra α] → OrderBot α

## BASE-LIBRARY REF Order.Frame.toHeytingAlgebra
{α : Type u_1} → [self : Order.Frame α] → HeytingAlgebra α

## BASE-LIBRARY REF CompleteDistribLattice.toFrame
{α : Type u_1} → [self : CompleteDistribLattice α] → Order.Frame α

## BASE-LIBRARY REF CompleteBooleanAlgebra.toCompleteDistribLattice
{α : Type u} → [CompleteBooleanAlgebra α] → CompleteDistribLattice α

## BASE-LIBRARY REF Std.Format
Type

Docstring: A representation of a set of strings, in which the placement of newlines and indentation differ.

Given a specific line width, specified in columns, the string that uses the fewest lines can be
selected.

The pretty-printing algorithm is based on Wadler's paper
[_A Prettier Printer_](https://homepages.inf.ed.ac.uk/wadler/papers/prettier/prettier.pdf).


## BASE-LIBRARY REF Repr.addAppParen
Format → ℕ → Format

Docstring: Adds parentheses to `f` if the precedence `prec` from the context is at least that of function
application.

Together with `reprArg`, this can be used to correctly parenthesize function application
syntax.


## BASE-LIBRARY REF Std.Format.group
Format → optParam Std.Format.FlattenBehavior Std.Format.FlattenBehavior.allOrNone → Format

Docstring: Creates a new flattening group for the given inner `Format`.  

## BASE-LIBRARY REF Std.Format.nest
ℤ → Format → Format

Docstring: `nest indent f` increases the current indentation level by `indent` while rendering `f`.

Example:
```lean example
open Std Format in
def fmtList (l : List Format) : Format :=
  let f := joinSep l  (", " ++ Format.line)
  group (nest 1 <| "[" ++ f ++ "]")
```

This will be written all on one line, but if the text is too large, the formatter will put in
linebreaks after the commas and indent later lines by 1.


## BASE-LIBRARY REF ite
{α : Sort u} → (c : Prop) → [h : Decidable c] → α → α → α

Docstring: `if c then t else e` is notation for `ite c t e`, "if-then-else", which decides to
return `t` or `e` depending on whether `c` is true or false. The explicit argument
`c : Prop` does not have any actual computational content, but there is an additional
`[Decidable c]` argument synthesized by typeclass inference which actually
determines how to evaluate `c` to true or false. Write `if h : c then t else e`
instead for a "dependent if-then-else" `dite`, which allows `t`/`e` to use the fact
that `c` is true/false.


## BASE-LIBRARY REF instLENat
LE ℕ

## BASE-LIBRARY REF Nat.decLe
(n m : ℕ) → Decidable (n ≤ m)

Docstring: A decision procedure for non-strict inequality of natural numbers, usually accessed via the
`DecidableLE Nat` instance.

Examples:
 * `(if 3 ≤ 4 then "yes" else "no") = "yes"`
 * `(if 6 ≤ 4 then "yes" else "no") = "no"`
 * `show 12 ≤ 12 by decide`
 * `show 5 ≤ 12 by decide`


## BASE-LIBRARY REF Std.Format.text
String → Format

Docstring: A node containing a plain string.

If the string contains newlines, the formatter emits them and then indents to the current level.


## BASE-LIBRARY REF Std.Format.FlattenBehavior.allOrNone
Std.Format.FlattenBehavior

Docstring: Either all `Format.line`s in the group will be newlines, or all of them will be spaces.


## INFORMAL STATEMENT
baby Jordan curve theorem

Let $A$, $B$, $A^{\prime }$ and $B^{\prime }$ be four lattice points satisfying 

\begin{align*}  \operatorname {x}\left( A^{\prime }\right) &  \leq \operatorname {x}\left( A\right) ,\  \  \  \  \  \  \  \  \  \  \operatorname {y}\left( A^{\prime }\right) \geq \operatorname {y}\left( A\right) ,\\ \operatorname {x}\left( B^{\prime }\right) &  \leq \operatorname {x}\left( B\right) ,\  \  \  \  \  \  \  \  \  \  \operatorname {y}\left( B^{\prime }\right) \geq \operatorname {y}\left( B\right) . \end{align*}

 (That is, $A'$ is weakly northwest of $A$, and $B'$ is weakly northwest of $B$.) 

Let $p$ be any path from $A$ to $B^{\prime }$. Let $p^{\prime }$ be any path from $A^{\prime }$ to $B$. Then, $p$ and $p^{\prime }$ have a vertex in common. 

In particular, there are no nipats from $(A, A')$ to $(B', B)$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.lgv.lattice
def.lgv.lattice

We consider the infinite simple digraph with vertex set $\mathbb {Z}^{2}$ (so the vertices are pairs of integers) and arcs 

\[  \left( i,j\right) \rightarrow \left( i+1,j\right) \  \  \  \  \  \  \  \  \  \  \text{for all }\left( i,j\right) \in \mathbb {Z}^{2}  \]

 and 

\[  \left( i,j\right) \rightarrow \left( i,j+1\right) \  \  \  \  \  \  \  \  \  \  \text{for all }\left( i,j\right) \in \mathbb {Z}^{2}.  \]

 The arcs of the first form are called \emph{east-steps} or \emph{right-steps}; the arcs of the second form are called \emph{north-steps} or \emph{up-steps}. 

The vertices of this digraph will be called \emph{lattice points} or \emph{grid points} or simply \emph{points}. 

The entire digraph will be denoted by $\mathbb {Z}^{2}$ and called the \emph{integer lattice} or \emph{integer grid}. 

Any path is uniquely determined by its starting point and its step sequence.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The main theorem exactly matches the blueprint. It quantifies over all four lattice points and assumes `LGV1.isWeaklyNorthwestOf A' A` and `LGV1.isWeaklyNorthwestOf B' B`; by the definition `fun p q => p.x \u2264 q.x \u2227 p.y \u2265 q.y`, these are precisely the two displayed northwest coordinate conditions. It then quantifies over arbitrary paths `p p'`, with premises `p.isPathFromTo A B'` and `p'.isPathFromTo A' B`, and concludes `\u2203 v \u2208 p.vertices A, v \u2208 p'.vertices A'`, exactly saying that the paths have a common vertex. The path definitions use lists of only `east` and `north` steps, matching the informal integer-lattice digraph, and `vertices` includes the starting point and all subsequently visited points. The corollary `LGV1.numNipats2 A A' B' B = 0` uses source tuple `![A,A']` and target tuple `![B',B]`, exactly the informal `(A,A')` to `(B',B)`. Although `Set.ncard` is zero for infinite sets as well, here paths between fixed endpoints consist of fixed finite numbers of east and north steps, so the relevant path-tuple set is finite; thus cardinality zero expresses that there are no nipats."
}