## TARGET LGV1.firstIntersection_mem_path1 (theorem) — ELABORATED SIGNATURE
∀ {A A' B B' : LGV1.LatticePoint} (spt : LGV1.SignedPathTuple2 A A' B B') (h : spt.isIntersecting),
  LGV1.firstIntersection spt h ∈ spt.path1.vertices A'

Docstring: The first intersection point is in path1's vertices. 

## TARGET LGV1.firstIntersection_is_first (theorem) — ELABORATED SIGNATURE
∀ {A A' B B' : LGV1.LatticePoint} (spt : LGV1.SignedPathTuple2 A A' B B') (h : spt.isIntersecting),
  have v := LGV1.firstIntersection spt h;
  let idx := LGV1.firstIntersectionIdx spt h;
  (spt.path0.vertices A)[idx] = v ∧ ∀ (i : ℕ) (hi : i < idx), (spt.path0.vertices A)[i] ∉ spt.path1.vertices A'

Docstring: The first intersection point is the first vertex (by index in path0) shared by both paths.
This is a key property for proving the involution is involutive: after swapping tails,
the same point v is still the first intersection because:
1. The head of path0 (indices 0..idx) is unchanged
2. v is at index idx in both the original and swapped paths
3. No earlier vertex in path0's head is in path1's vertices (by minimality of findIdx) 

## TARGET LGV1.firstIntersection (def) — ELABORATED SIGNATURE
{A A' B B' : LGV1.LatticePoint} → (spt : LGV1.SignedPathTuple2 A A' B B') → spt.isIntersecting → LGV1.LatticePoint

Body:
fun {A A' B B'} spt h =>
  let idx := LGV1.firstIntersectionIdx spt h;
  let verts0 := spt.path0.vertices A;
  verts0[idx]

Docstring: The first intersection point of two intersecting paths.
This is the first vertex (by index in path0) that is shared by both paths. 

## TARGET LGV1.firstIntersection_mem_path0 (theorem) — ELABORATED SIGNATURE
∀ {A A' B B' : LGV1.LatticePoint} (spt : LGV1.SignedPathTuple2 A A' B B') (h : spt.isIntersecting),
  LGV1.firstIntersection spt h ∈ spt.path0.vertices A

Docstring: The first intersection point is in path0's vertices. 

## PROJECT DEPENDENCY LGV1.LatticePoint (def)
Type

Body:
ℤ × ℤ

Docstring: A point on the integer lattice ℤ².
The vertices of the integer lattice are pairs of integers.
Label: def.lgv.lattice 

## PROJECT DEPENDENCY LGV1.SignedPathTuple2 (inductive)
LGV1.LatticePoint → LGV1.LatticePoint → LGV1.LatticePoint → LGV1.LatticePoint → Type

Body:
LGV1.SignedPathTuple2.mk : {A A' B B' : LGV1.LatticePoint} →
  (path0 path1 : LGV1.LatticePath) →
    (toBB' : Bool) →
      path0.isPathFromTo A (if toBB' = true then B else B') →
        path1.isPathFromTo A' (if toBB' = true then B' else B) → LGV1.SignedPathTuple2 A A' B B'

Docstring: A path tuple from (A,A') to (B,B') or (B',B) with a sign.
Sign is +1 for (B,B') and -1 for (B',B). 

## PROJECT DEPENDENCY LGV1.SignedPathTuple2.isIntersecting (def)
{A A' B B' : LGV1.LatticePoint} → LGV1.SignedPathTuple2 A A' B B' → Prop

Body:
fun {A A' B B'} spt => ∃ v ∈ spt.path0.vertices A, v ∈ spt.path1.vertices A'

Docstring: Check if a signed path tuple is intersecting (the two paths share a vertex). 

## PROJECT DEPENDENCY LGV1.LatticePath.vertices (def)
LGV1.LatticePath → LGV1.LatticePoint → List LGV1.LatticePoint

Body:
fun path start => (start :: List.scanl (fun p s => s.apply p) start path).tail

Docstring: All vertices visited by a path, including start and end. 

## PROJECT DEPENDENCY LGV1.SignedPathTuple2.path1 (def)
{A A' B B' : LGV1.LatticePoint} → LGV1.SignedPathTuple2 A A' B B' → LGV1.LatticePath

Body:
fun A A' B B' self => self.2

Docstring: The second path 

## PROJECT DEPENDENCY LGV1.firstIntersectionIdx (def)
{A A' B B' : LGV1.LatticePoint} → (spt : LGV1.SignedPathTuple2 A A' B B') → spt.isIntersecting → ℕ

Body:
fun {A A' B B'} spt _h =>
  have verts0 := spt.path0.vertices A;
  have verts1 := spt.path1.vertices A';
  List.findIdx (fun v => decide (v ∈ verts1)) verts0

Docstring: The index of the first intersection point in path0's vertices.
This is the smallest index i such that (path0.vertices A)[i] ∈ path1.vertices A'. 

## PROJECT DEPENDENCY LGV1.SignedPathTuple2.path0 (def)
{A A' B B' : LGV1.LatticePoint} → LGV1.SignedPathTuple2 A A' B B' → LGV1.LatticePath

Body:
fun A A' B B' self => self.1

Docstring: The first path 

## PROJECT DEPENDENCY LGV1.firstIntersectionIdx_lt (theorem)
∀ {A A' B B' : LGV1.LatticePoint} (spt : LGV1.SignedPathTuple2 A A' B B') (h : spt.isIntersecting),
  LGV1.firstIntersectionIdx spt h < (spt.path0.vertices A).length

Docstring: The index of the first intersection point is valid (less than the length of path0's vertices). 

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

## PROJECT DEPENDENCY LGV1.LatticeStep.apply (def)
LGV1.LatticeStep → LGV1.LatticePoint → LGV1.LatticePoint

Body:
fun s p =>
  match s with
  | LGV1.LatticeStep.east => (p.1 + 1, p.2)
  | LGV1.LatticeStep.north => (p.1, p.2 + 1)

Docstring: Apply a step to a lattice point. 

## PROJECT DEPENDENCY LGV1.LatticePath.endpoint (def)
LGV1.LatticePath → LGV1.LatticePoint → LGV1.LatticePoint

Body:
fun path start => List.foldl (fun p s => s.apply p) start path

Docstring: The endpoint of a path starting from a given point. 

## PROJECT DEPENDENCY LGV1.instReprLatticeStep.repr (def)
LGV1.LatticeStep → ℕ → Format

Body:
fun x prec =>
  match x with
  | LGV1.LatticeStep.east =>
    Repr.addAppParen (Format.nest (if prec ≥ 1024 then 1 else 2) (Std.Format.text "LGV1.LatticeStep.east")).group prec
  | LGV1.LatticeStep.north =>
    Repr.addAppParen (Format.nest (if prec ≥ 1024 then 1 else 2) (Std.Format.text "LGV1.LatticeStep.north")).group prec

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

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF And
Prop → Prop → Prop

Docstring: `And a b`, or `a ∧ b`, is the conjunction of propositions. It can be
constructed and destructed like a pair: if `ha : a` and `hb : b` then
`⟨ha, hb⟩ : a ∧ b`, and if `h : a ∧ b` then `h.left : a` and `h.right : b`.


Conventions for notations in identifiers:

 * The recommended spelling of `∧` in identifiers is `and`.

 * The recommended spelling of `/\` in identifiers is `and` (prefer `∧` over `/\`).

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

## BASE-LIBRARY REF GetElem.getElem
{coll : Type u} →
  {idx : Type v} →
    {elem : outParam (Type w)} →
      {valid : outParam (coll → idx → Prop)} →
        [self : GetElem coll idx elem valid] → (xs : coll) → (i : idx) → valid xs i → elem

Docstring: The syntax `arr[i]` gets the `i`'th element of the collection `arr`. If there
are proof side conditions to the application, they will be automatically
inferred by the `get_elem_tactic` tactic.


Conventions for notations in identifiers:

 * The recommended spelling of `xs[i]` in identifiers is `getElem`.

 * The recommended spelling of `xs[i]'h` in identifiers is `getElem`.

## BASE-LIBRARY REF LT.lt
{α : Type u} → [self : LT α] → α → α → Prop

Docstring: The less-than relation: `x < y` 

Conventions for notations in identifiers:

 * The recommended spelling of `<` in identifiers is `lt`.

## BASE-LIBRARY REF instLTNat
LT ℕ

## BASE-LIBRARY REF List.length
{α : Type u_1} → List α → ℕ

Docstring: The length of a list.

This function is overridden in the compiler to `lengthTR`, which uses constant stack space.

Examples:
* `([] : List String).length = 0`
* `["green", "brown"].length = 2`


## BASE-LIBRARY REF List.instGetElemNatLtLength
{α : Type u_1} → GetElem (List α) ℕ α fun as i => i < as.length

## BASE-LIBRARY REF Not
Prop → Prop

Docstring: `Not p`, or `¬p`, is the negation of `p`. It is defined to be `p → False`,
so if your goal is `¬p` you can use `intro h` to turn the goal into
`h : p ⊢ False`, and if you have `hn : ¬p` and `h : p` then `hn h : False`
and `(hn h).elim` will prove anything.
For more information: [Propositional Logic](https://lean-lang.org/theorem_proving_in_lean4/propositions_and_proofs.html#propositional-logic)


Conventions for notations in identifiers:

 * The recommended spelling of `¬` in identifiers is `not`.

## BASE-LIBRARY REF Nat.lt_trans
∀ {n m k : ℕ}, n < m → m < k → n < k

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


## BASE-LIBRARY REF Bool
Type

Docstring: The Boolean values, `true` and `false`.

Logically speaking, this is equivalent to `Prop` (the type of propositions). The distinction is
public important for programming: both propositions and their proofs are erased in the code generator,
while `Bool` corresponds to the Boolean type in most programming languages and carries precisely one
bit of run-time information.


## BASE-LIBRARY REF ite
{α : Sort u} → (c : Prop) → [h : Decidable c] → α → α → α

Docstring: `if c then t else e` is notation for `ite c t e`, "if-then-else", which decides to
return `t` or `e` depending on whether `c` is true or false. The explicit argument
`c : Prop` does not have any actual computational content, but there is an additional
`[Decidable c]` argument synthesized by typeclass inference which actually
determines how to evaluate `c` to true or false. Write `if h : c then t else e`
instead for a "dependent if-then-else" `dite`, which allows `t`/`e` to use the fact
that `c` is true/false.


## BASE-LIBRARY REF Bool.true
Bool

Docstring: The Boolean value `true`, not to be confused with the proposition `True`. 

## BASE-LIBRARY REF instDecidableEqBool
DecidableEq Bool

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


## BASE-LIBRARY REF List.findIdx
{α : Type u} → (α → Bool) → List α → ℕ

Docstring: Returns the index of the first element for which `p` returns `true`, or the length of the list if
there is no such element.

Examples:
* `[7, 6, 5, 8, 1, 2, 6].findIdx (· < 5) = 4`
* `[7, 6, 5, 8, 1, 2, 6].findIdx (· < 1) = 7`


## BASE-LIBRARY REF Decidable.decide
(p : Prop) → [h : Decidable p] → Bool

Docstring: Converts a decidable proposition into a `Bool`.

If `p : Prop` is decidable, then `decide p : Bool` is the Boolean value
that is `true` if `p` is true and `false` if `p` is false.


## BASE-LIBRARY REF List.instDecidableMemOfLawfulBEq
{α : Type u} → [inst : BEq α] → [LawfulBEq α] → (a : α) → (as : List α) → Decidable (a ∈ as)

## BASE-LIBRARY REF instBEqProd
{α : Type u_1} → {β : Type u_2} → [BEq α] → [BEq β] → BEq (α × β)

## BASE-LIBRARY REF instBEqOfDecidableEq
{α : Type u_1} → [DecidableEq α] → BEq α

## BASE-LIBRARY REF Int.instDecidableEq
DecidableEq ℤ

Docstring: Decides whether two integers are equal. Usually accessed via the `DecidableEq Int` instance.

This function is overridden by the compiler with an efficient implementation. This definition is the
logical model.

Examples:
* `show (7 : Int) = (3 : Int) + (4 : Int) by decide`
* `if (6 : Int) = (3 : Int) * (2 : Int) then "yes" else "no" = "yes"`
* `(¬ (6 : Int) = (3 : Int)) = true`


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

## BASE-LIBRARY REF Prod.fst
{α : Type u} → {β : Type v} → α × β → α

Docstring: The first element of a pair. 

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNat
{n : ℕ} → OfNat ℤ n

## BASE-LIBRARY REF Prod.snd
{α : Type u} → {β : Type v} → α × β → β

Docstring: The second element of a pair. 

## BASE-LIBRARY REF List.foldl
{α : Type u} → {β : Type v} → (α → β → α) → α → List β → α

Docstring: Folds a function over a list from the left, accumulating a value starting with `init`. The
accumulated value is combined with the each element of the list in order, using `f`.

Examples:
 * `[a, b, c].foldl f z  = f (f (f z a) b) c`
 * `[1, 2, 3].foldl (· ++ toString ·) "" = "123"`
 * `[1, 2, 3].foldl (s!"({·} {·})") "" = "((( 1) 2) 3)"`


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

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

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
lem.lgv.first-intersection-props

\leanhelper  The \emph{first intersection point} $v$ of an intersecting signed path tuple $(p_0, p_1)$ satisfies: 

\begin{enumerate} \item $v$ lies on $p_0$ (at the first intersection index). 

\item $v$ lies on $p_1$. 

\item $v$ is \emph{first}: no vertex of $p_0$ at an earlier index belongs to $p_1$. 

\end{enumerate}

## VERDICT
{
  "verdict": "faithful",
  "justification": "The formal declarations collectively match all three blueprint properties for every intersecting signed path tuple, with exactly the blueprint hypothesis `(h : spt.isIntersecting)`. The point is defined by `firstIntersection spt h = (spt.path0.vertices A)[firstIntersectionIdx spt h]`, and `firstIntersection_mem_path0` proves it lies in `spt.path0.vertices A`, matching \u201cv lies on p\u2080 (at the first intersection index).\u201d `firstIntersection_mem_path1` proves `firstIntersection spt h \u2208 spt.path1.vertices A'`, matching \u201cv lies on p\u2081.\u201d Finally, `firstIntersection_is_first` proves `\u2200 (i : \u2115) (hi : i < idx), (spt.path0.vertices A)[i] \u2209 spt.path1.vertices A'`, exactly matching \u201cno vertex of p\u2080 at an earlier index belongs to p\u2081.\u201d The dependency `firstIntersectionIdx` uses `List.findIdx` on membership in path1, whose documented meaning is the first satisfying index, and `h` ensures such an index exists."
}