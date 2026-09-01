## TARGET LGV1.LatticePath.isPathFromTo_append (theorem) — ELABORATED SIGNATURE
∀ (head tail : LGV1.LatticePath) (A v B : LGV1.LatticePoint),
  head.isPathFromTo A v → tail.isPathFromTo v B → (head ++ tail).isPathFromTo A B

Docstring: If head goes A→v and tail goes v→B, then head ++ tail goes A→B. 

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

## PROJECT DEPENDENCY LGV1.LatticePoint (def)
Type

Body:
ℤ × ℤ

Docstring: A point on the integer lattice ℤ².
The vertices of the integer lattice are pairs of integers.
Label: def.lgv.lattice 

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

## PROJECT DEPENDENCY LGV1.instReprLatticeStep.repr (def)
LGV1.LatticeStep → ℕ → Format

Body:
fun x prec =>
  match x with
  | LGV1.LatticeStep.east =>
    Repr.addAppParen (Format.nest (if prec ≥ 1024 then 1 else 2) (Std.Format.text "LGV1.LatticeStep.east")).group prec
  | LGV1.LatticeStep.north =>
    Repr.addAppParen (Format.nest (if prec ≥ 1024 then 1 else 2) (Std.Format.text "LGV1.LatticeStep.north")).group prec

## BASE-LIBRARY REF HAppend.hAppend
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HAppend α β γ] → α → β → γ

Docstring: `a ++ b` is the result of concatenation of `a` and `b`, usually read "append".
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `++` in identifiers is `append`.

## BASE-LIBRARY REF instHAppendOfAppend
{α : Type u_1} → [Append α] → HAppend α α α

## BASE-LIBRARY REF List.instAppend
{α : Type u} → Append (List α)

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

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


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
lem.lgv.path-append

\leanhelper  If path $h$ goes from $A$ to $v$ and path $t$ goes from $v$ to $B$, then $h \cdot t$ goes from $A$ to $B$.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The blueprint says: \u201cIf path $h$ goes from $A$ to $v$ and path $t$ goes from $v$ to $B$, then $h \\cdot t$ goes from $A$ to $B$.\u201d The target quantifies exactly over paths and points, `\u2200 (head tail : LGV1.LatticePath) (A v B : LGV1.LatticePoint)`, and asserts `head.isPathFromTo A v \u2192 tail.isPathFromTo v B \u2192 (head ++ tail).isPathFromTo A B`. Here `LatticePath` is `List LatticeStep`, so `head ++ tail` is list concatenation, matching path composition $h \\cdot t$; and `isPathFromTo path a b` is defined as `path.endpoint a = b`, matching \u201cgoes from $a$ to $b$.\u201d There are no added hypotheses or narrowed quantifiers."
}