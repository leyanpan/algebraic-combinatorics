## TARGET LGV.latticePath'Equiv (def) — ELABORATED SIGNATURE
(start : ℤ × ℤ) → LGV.LatticePath' ≃ { p // p.start = start }

Body:
fun start =>
  { toFun := fun path => ⟨path.toPath start, ⋯⟩, invFun := fun p => LGV.pathToLatticePath' ↑p, left_inv := ⋯,
    right_inv := ⋯ }

Docstring: The bijection between LatticePath' and SimpleDigraph.Path starting at a fixed point.

This establishes that the two path representations are equivalent, which is the key
step needed to bridge LGV1.lean's counting results with LGV2.lean's weighted results. 

## PROJECT DEPENDENCY LGV.LatticePath' (def)
Type

Body:
List LGV.LatticeStep'

Docstring: A lattice path as a list of steps (matching LGV1.lean's definition) 

## PROJECT DEPENDENCY LGV.SimpleDigraph.Path (inductive)
{V : Type u_1} → LGV.SimpleDigraph V → Type u_1

Body:
LGV.SimpleDigraph.Path.mk : {V : Type u_1} →
  {D : LGV.SimpleDigraph V} →
    (vertices : List V) →
      vertices ≠ [] →
        (∀ (i : ℕ) (hi : i + 1 < vertices.length), D.arc (vertices.get ⟨i, ⋯⟩) (vertices.get ⟨i + 1, hi⟩)) → D.Path

Docstring: A path in a digraph is a list of vertices where consecutive vertices are connected by arcs.
A path may contain 0 arcs (in which case start and end are identical). 

## PROJECT DEPENDENCY LGV.integerLattice (def)
LGV.SimpleDigraph (ℤ × ℤ)

Body:
{ arc := fun u v => v.1 = u.1 + 1 ∧ v.2 = u.2 ∨ v.1 = u.1 ∧ v.2 = u.2 + 1, arc_irrefl := LGV.integerLattice._proof_1 }

Docstring: The integer lattice digraph ℤ².

This is the same lattice as in LGV1.lean, but using `SimpleDigraph` instead of
Mathlib's `Digraph`. See `integerLattice_arc_iff` for the characterization
and `integerLattice_toDigraph_adj_iff` for the equivalence with LGV1's definition. 

## PROJECT DEPENDENCY LGV.SimpleDigraph.Path.start (def)
{V : Type u_1} → {D : LGV.SimpleDigraph V} → D.Path → V

Body:
fun {V} {D} p => p.vertices.head ⋯

Docstring: The starting vertex of a path 

## PROJECT DEPENDENCY LGV.LatticePath'.toPath (def)
LGV.LatticePath' → ℤ × ℤ → LGV.integerLattice.Path

Body:
fun path start => { vertices := path.toVertices start, nonempty := ⋯, arcs_valid := ⋯ }

Docstring: Convert a lattice path to a SimpleDigraph.Path 

## PROJECT DEPENDENCY LGV.LatticePath'.toPath_start (theorem)
∀ (path : LGV.LatticePath') (start : ℤ × ℤ), (path.toPath start).start = start

Docstring: The start of the converted path is the original start point 

## PROJECT DEPENDENCY LGV.pathToLatticePath' (def)
LGV.integerLattice.Path → LGV.LatticePath'

Body:
fun p => LGV.verticesToSteps' p.vertices ⋯

Docstring: Convert a SimpleDigraph.Path to a LatticePath' 

## PROJECT DEPENDENCY LGV.LatticeStep' (inductive)
Type

Body:
LGV.LatticeStep'.east : LGV.LatticeStep'
LGV.LatticeStep'.north : LGV.LatticeStep'

Docstring: A lattice step on the integer lattice: either east (+1,0) or north (0,+1).

This is the canonical definition for lattice steps. LGV1.lean defines an equivalent
type `LGV1.LatticeStep` with an explicit equivalence `LGV1.latticeStepEquiv`.

The two types are isomorphic via:
- `LGV1.latticeStepEquiv : LGV1.LatticeStep ≃ LGV.LatticeStep'`
- `LGV1.latticePathToLatticePath' : LGV1.LatticePath → LGV.LatticePath'`
- `LGV1.latticePath'ToLatticePath : LGV.LatticePath' → LGV1.LatticePath`

Note: The duplication exists because LGV1 imports LGV2, so LGV2 cannot reference
LGV1's definitions. Both definitions are intentionally kept compatible. 

## PROJECT DEPENDENCY LGV.SimpleDigraph (inductive)
Type u_1 → Type u_1

Body:
LGV.SimpleDigraph.mk : {V : Type u_1} → (arc : V → V → Prop) → (∀ (v : V), ¬arc v v) → LGV.SimpleDigraph V

Docstring: A simple digraph with vertex set V.
Convention conv.lgv.digraph(d): A simple digraph has arcs as pairs of distinct vertices. 

## PROJECT DEPENDENCY LGV.SimpleDigraph.arc (def)
{V : Type u_1} → LGV.SimpleDigraph V → V → V → Prop

Body:
fun V self => self.1

Docstring: The arc relation: `arc u v` means there is an arc from `u` to `v` 

## PROJECT DEPENDENCY LGV.SimpleDigraph.mk (constructor)
{V : Type u_1} → (arc : V → V → Prop) → (∀ (v : V), ¬arc v v) → LGV.SimpleDigraph V

## PROJECT DEPENDENCY LGV.SimpleDigraph.Path.vertices (def)
{V : Type u_1} → {D : LGV.SimpleDigraph V} → D.Path → List V

Body:
fun V D self => self.1

Docstring: The vertices of the path, in order 

## PROJECT DEPENDENCY LGV.SimpleDigraph.Path.nonempty (theorem)
∀ {V : Type u_1} {D : LGV.SimpleDigraph V} (self : D.Path), self.vertices ≠ []

Docstring: The path is nonempty 

## PROJECT DEPENDENCY LGV.SimpleDigraph.Path.mk (constructor)
{V : Type u_1} →
  {D : LGV.SimpleDigraph V} →
    (vertices : List V) →
      vertices ≠ [] →
        (∀ (i : ℕ) (hi : i + 1 < vertices.length), D.arc (vertices.get ⟨i, ⋯⟩) (vertices.get ⟨i + 1, hi⟩)) → D.Path

## PROJECT DEPENDENCY LGV.LatticePath'.toVertices (def)
LGV.LatticePath' → ℤ × ℤ → List (ℤ × ℤ)

Body:
fun path start =>
  List.brecOn (motive := fun path => ℤ × ℤ → List (ℤ × ℤ)) path
    (fun path f start =>
      (match (motive :=
          (path : LGV.LatticePath') → List.below (motive := fun path => ℤ × ℤ → List (ℤ × ℤ)) path → List (ℤ × ℤ))
          path with
        | [] => fun x => [start]
        | s :: rest => fun x => start :: x.1 (s.apply start))
        f)
    start

Docstring: Compute all vertices visited by a lattice path, including start.
For path = [s₁, s₂, ..., sₙ], this returns [start, s₁(start), s₂(s₁(start)), ...] 

## PROJECT DEPENDENCY LGV.LatticePath'.toVertices_nonempty (theorem)
∀ (path : LGV.LatticePath') (start : ℤ × ℤ), path.toVertices start ≠ []

Docstring: The vertices list is nonempty 

## PROJECT DEPENDENCY LGV.LatticePath'.toVertices_arcs_valid (theorem)
∀ (path : LGV.LatticePath') (start : ℤ × ℤ) (i : ℕ) (hi : i + 1 < (path.toVertices start).length),
  LGV.integerLattice.arc ((path.toVertices start).get ⟨i, ⋯⟩) ((path.toVertices start).get ⟨i + 1, hi⟩)

Docstring: Consecutive vertices in toVertices are connected by arcs 

## PROJECT DEPENDENCY LGV.verticesToSteps' (def)
(vs : List (ℤ × ℤ)) →
  (∀ (i : ℕ) (hi : i + 1 < vs.length), LGV.integerLattice.arc (vs.get ⟨i, ⋯⟩) (vs.get ⟨i + 1, hi⟩)) → LGV.LatticePath'

Body:
fun x x_1 =>
  List.brecOn (motive := fun x =>
    (∀ (i : ℕ) (hi : i + 1 < x.length), LGV.integerLattice.arc (x.get ⟨i, ⋯⟩) (x.get ⟨i + 1, hi⟩)) → LGV.LatticePath') x
    (fun x f x_2 =>
      (match (motive :=
          (x : List (ℤ × ℤ)) →
            (∀ (i : ℕ) (hi : i + 1 < x.length), LGV.integerLattice.arc (x.get ⟨i, ⋯⟩) (x.get ⟨i + 1, hi⟩)) →
              List.below (motive := fun x =>
                  (∀ (i : ℕ) (hi : i + 1 < x.length), LGV.integerLattice.arc (x.get ⟨i, ⋯⟩) (x.get ⟨i + 1, hi⟩)) →
                    LGV.LatticePath')
                  x →
                LGV.LatticePath')
          x, x_2 with
        | [], x => fun x => []
        | [head], x => fun x => []
        | u :: v :: rest, harcs => fun x =>
          let h := ⋯;
          LGV.arcToStep' u v h :: x.1 ⋯)
        f)
    x_1

Docstring: Convert a vertex list to a step list (partial inverse of toVertices) 

## PROJECT DEPENDENCY LGV.LatticeStep'.apply (def)
LGV.LatticeStep' → ℤ × ℤ → ℤ × ℤ

Body:
fun s p =>
  match s with
  | LGV.LatticeStep'.east => (p.1 + 1, p.2)
  | LGV.LatticeStep'.north => (p.1, p.2 + 1)

Docstring: Apply a step to a lattice point 

## PROJECT DEPENDENCY LGV.arcToStep' (def)
(u v : ℤ × ℤ) → LGV.integerLattice.arc u v → LGV.LatticeStep'

Body:
fun u v _h => if v.1 = u.1 + 1 then LGV.LatticeStep'.east else LGV.LatticeStep'.north

Docstring: Convert an arc in the integer lattice to a step.
This is the inverse operation to LatticeStep'.apply. 

## PROJECT DEPENDENCY LGV.instReprLatticeStep'.repr (def)
LGV.LatticeStep' → ℕ → Format

Body:
fun x prec =>
  match x with
  | LGV.LatticeStep'.east =>
    Repr.addAppParen (Format.nest (if prec ≥ 1024 then 1 else 2) (Std.Format.text "LGV.LatticeStep'.east")).group prec
  | LGV.LatticeStep'.north =>
    Repr.addAppParen (Format.nest (if prec ≥ 1024 then 1 else 2) (Std.Format.text "LGV.LatticeStep'.north")).group prec

## PROJECT DEPENDENCY LGV.LatticeStep'.east (constructor)
LGV.LatticeStep'

## PROJECT DEPENDENCY LGV.LatticeStep'.north (constructor)
LGV.LatticeStep'

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


## BASE-LIBRARY REF Equiv
Sort u_1 → Sort u_2 → Sort (max (max 1 u_1) u_2)

Docstring: `α ≃ β` is the type of functions from `α → β` with a two-sided inverse. 

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

## BASE-LIBRARY REF Equiv.mk
{α : Sort u_1} →
  {β : Sort u_2} →
    (toFun : α → β) →
      (invFun : β → α) →
        autoParam (Function.LeftInverse invFun toFun) Equiv.left_inv._autoParam →
          autoParam (Function.RightInverse invFun toFun) Equiv.right_inv._autoParam → α ≃ β

## BASE-LIBRARY REF Subtype.mk
{α : Sort u} → {p : α → Prop} → (val : α) → p val → Subtype p

## BASE-LIBRARY REF Subtype.val
{α : Sort u} → {p : α → Prop} → Subtype p → α

Docstring: The value in the underlying type that satisfies the predicate.


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


## BASE-LIBRARY REF Ne
{α : Sort u} → α → α → Prop

Docstring: `a ≠ b`, or `Ne a b` is defined as `¬ (a = b)` or `a = b → False`,
and asserts that `a` and `b` are not equal.


Conventions for notations in identifiers:

 * The recommended spelling of `≠` in identifiers is `ne`.

## BASE-LIBRARY REF List.nil
{α : Type u} → List α

Docstring: The empty list, usually written `[]`. 

Conventions for notations in identifiers:

 * The recommended spelling of `[]` in identifiers is `nil`.

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


## BASE-LIBRARY REF Fin.mk
{n : ℕ} → (val : ℕ) → val < n → Fin n

Docstring: Creates a `Fin n` from `i : Nat` and a proof that `i < n`. 

## BASE-LIBRARY REF Nat.lt_of_succ_lt
∀ {n m : ℕ}, n.succ < m → n < m

## BASE-LIBRARY REF Or
Prop → Prop → Prop

Docstring: `Or a b`, or `a ∨ b`, is the disjunction of propositions. There are two
constructors for `Or`, called `Or.inl : a → a ∨ b` and `Or.inr : b → a ∨ b`,
and you can use `match` or `cases` to destruct an `Or` assumption into the
two cases.


Conventions for notations in identifiers:

 * The recommended spelling of `∨` in identifiers is `or`.

 * The recommended spelling of `\/` in identifiers is `or` (prefer `∨` over `\/`).

## BASE-LIBRARY REF And
Prop → Prop → Prop

Docstring: `And a b`, or `a ∧ b`, is the conjunction of propositions. It can be
constructed and destructed like a pair: if `ha : a` and `hb : b` then
`⟨ha, hb⟩ : a ∧ b`, and if `h : a ∧ b` then `h.left : a` and `h.right : b`.


Conventions for notations in identifiers:

 * The recommended spelling of `∧` in identifiers is `and`.

 * The recommended spelling of `/\` in identifiers is `and` (prefer `∧` over `/\`).

## BASE-LIBRARY REF Prod.fst
{α : Type u} → {β : Type v} → α × β → α

Docstring: The first element of a pair. 

## BASE-LIBRARY REF Int.instAdd
Add ℤ

## BASE-LIBRARY REF instOfNat
{n : ℕ} → OfNat ℤ n

## BASE-LIBRARY REF Prod.snd
{α : Type u} → {β : Type v} → α × β → β

Docstring: The second element of a pair. 

## BASE-LIBRARY REF List.head
{α : Type u} → (as : List α) → as ≠ [] → α

Docstring: Returns the first element of a non-empty list.


## BASE-LIBRARY REF Not
Prop → Prop

Docstring: `Not p`, or `¬p`, is the negation of `p`. It is defined to be `p → False`,
so if your goal is `¬p` you can use `intro h` to turn the goal into
`h : p ⊢ False`, and if you have `hn : ¬p` and `h : p` then `hn h : False`
and `(hn h).elim` will prove anything.
For more information: [Propositional Logic](https://lean-lang.org/theorem_proving_in_lean4/propositions_and_proofs.html#propositional-logic)


Conventions for notations in identifiers:

 * The recommended spelling of `¬` in identifiers is `not`.

## BASE-LIBRARY REF List.brecOn
{α : Type u} → {motive : List α → Sort u_1} → (t : List α) → ((t : List α) → List.below t → motive t) → motive t

## BASE-LIBRARY REF List.below
{α : Type u} → {motive : List α → Sort u_1} → List α → Sort (max (u + 1) u_1)

## BASE-LIBRARY REF Unit
Type

Docstring: The canonical type with one element. This element is written `()`.

`Unit` has a number of uses:
* It can be used to model control flow that returns from a function call without providing other
  information.
* Monadic actions that return `Unit` have side effects without computing values.
* In polymorphic types, it can be used to indicate that no data is to be stored in a particular
  field.


## BASE-LIBRARY REF List.cons
{α : Type u} → α → List α → List α

Docstring: The list whose first element is `head`, where `tail` is the rest of the list.
Usually written `head :: tail`.


Conventions for notations in identifiers:

 * The recommended spelling of `::` in identifiers is `cons`.

 * The recommended spelling of `[a]` in identifiers is `singleton`.

## BASE-LIBRARY REF Prod.mk
{α : Type u} → {β : Type v} → α → β → α × β

Docstring: Constructs a pair. This is usually written `(x, y)` instead of `Prod.mk x y`.


Conventions for notations in identifiers:

 * The recommended spelling of `(a, b)` in identifiers is `mk`.

## BASE-LIBRARY REF ite
{α : Sort u} → (c : Prop) → [h : Decidable c] → α → α → α

Docstring: `if c then t else e` is notation for `ite c t e`, "if-then-else", which decides to
return `t` or `e` depending on whether `c` is true or false. The explicit argument
`c : Prop` does not have any actual computational content, but there is an additional
`[Decidable c]` argument synthesized by typeclass inference which actually
determines how to evaluate `c` to true or false. Write `if h : c then t else e`
instead for a "dependent if-then-else" `dite`, which allows `t`/`e` to use the fact
that `c` is true/false.


## BASE-LIBRARY REF Int.instDecidableEq
DecidableEq ℤ

Docstring: Decides whether two integers are equal. Usually accessed via the `DecidableEq Int` instance.

This function is overridden by the compiler with an efficient implementation. This definition is the
logical model.

Examples:
* `show (7 : Int) = (3 : Int) + (4 : Int) by decide`
* `if (6 : Int) = (3 : Int) * (2 : Int) then "yes" else "no" = "yes"`
* `(¬ (6 : Int) = (3 : Int)) = true`


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


## BASE-LIBRARY REF GE.ge
{α : Type u} → [LE α] → α → α → Prop

Docstring: `a ≥ b` is an abbreviation for `b ≤ a`. 

Conventions for notations in identifiers:

 * The recommended spelling of `≥` in identifiers is `ge`.

 * The recommended spelling of `>=` in identifiers is `ge` (prefer `≥` over `>=`).

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
Lattice path conversion is a bijection

\leanhelper  There is a bijection between step-based lattice paths (lists of east/north steps starting at a given point) and vertex-based digraph paths in $\mathbb {Z}^2$ starting at that point. The forward direction computes the list of visited vertices; the backward direction recovers the step sequence from consecutive vertex pairs.

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
  "justification": "The target quantifies over every starting point via `(start : \u2124 \u00d7 \u2124)` and gives an equivalence `LGV.LatticePath' \u2243 { p // p.start = start }`. Here `LGV.LatticePath'` is exactly `List LGV.LatticeStep'`, whose constructors are `east` and `north`, while the subtype on the right consists exactly of paths in `LGV.integerLattice` starting at the specified point. The dependency `LGV.integerLattice` has precisely the blueprint\u2019s east and north arcs. The body also realizes the stated maps: `path.toPath start` uses `path.toVertices start` for the forward conversion, and `LGV.pathToLatticePath'` uses `LGV.verticesToSteps' p.vertices` to recover steps from consecutive vertices. `Equiv` supplies the required two-sided inverse, so this is a bijection with no extra mathematical hypotheses or narrowed quantifiers."
}