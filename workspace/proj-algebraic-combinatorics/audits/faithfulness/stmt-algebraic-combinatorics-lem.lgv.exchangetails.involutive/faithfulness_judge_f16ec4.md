## TARGET LGV.exchangeTails_involutive (theorem) — ELABORATED SIGNATURE
∀ {V : Type u_3} [inst : DecidableEq V] {D : LGV.SimpleDigraph V},
  D.IsAcyclic →
    ∀ (p q : D.Path) (v : V) (hv_p : v ∈ p.vertices) (hv_q : v ∈ q.vertices),
      let p' := (LGV.exchangeTails p q v hv_p hv_q).1;
      let q' := (LGV.exchangeTails p q v hv_p hv_q).2;
      have hv_p' := ⋯;
      have hv_q' := ⋯;
      LGV.exchangeTails p' q' v hv_p' hv_q' = (p, q)

## PROJECT DEPENDENCY LGV.SimpleDigraph (inductive)
Type u_1 → Type u_1

Body:
LGV.SimpleDigraph.mk : {V : Type u_1} → (arc : V → V → Prop) → (∀ (v : V), ¬arc v v) → LGV.SimpleDigraph V

Docstring: A simple digraph with vertex set V.
Convention conv.lgv.digraph(d): A simple digraph has arcs as pairs of distinct vertices. 

## PROJECT DEPENDENCY LGV.SimpleDigraph.IsAcyclic (def)
{V : Type u_1} → LGV.SimpleDigraph V → Prop

Body:
fun {V} D => ∀ (p : D.Path), p.start = p.finish → p.vertices.length = 1

Docstring: A digraph is acyclic if it has no directed cycles.
Convention conv.lgv.digraph(c) 

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

## PROJECT DEPENDENCY LGV.SimpleDigraph.Path.vertices (def)
{V : Type u_1} → {D : LGV.SimpleDigraph V} → D.Path → List V

Body:
fun V D self => self.1

Docstring: The vertices of the path, in order 

## PROJECT DEPENDENCY LGV.exchangeTails (def)
{V : Type u_3} →
  [DecidableEq V] →
    {D : LGV.SimpleDigraph V} → (p q : D.Path) → (v : V) → v ∈ p.vertices → v ∈ q.vertices → D.Path × D.Path

Body:
fun {V} [DecidableEq V] {D} p q v hv_p hv_q =>
  let sp_p := p.splitAt v hv_p;
  let sp_q := q.splitAt v hv_q;
  let head_p := sp_p.1;
  let tail_p := sp_p.2;
  let head_q := sp_q.1;
  let tail_q := sp_q.2;
  have h1 := ⋯;
  have h2 := ⋯;
  (head_p.concat tail_q h1, head_q.concat tail_p h2)

Docstring: Exchange the tails of two paths at a common vertex.
If p goes A → v → B and q goes A' → v → B', then after exchange:
p' goes A → v → B' and q' goes A' → v → B 

## PROJECT DEPENDENCY LGV.exchangeTails_fst_mem_v (theorem)
∀ {V : Type u_3} [inst : DecidableEq V] {D : LGV.SimpleDigraph V} (p q : D.Path) (v : V) (hv_p : v ∈ p.vertices)
  (hv_q : v ∈ q.vertices), v ∈ (LGV.exchangeTails p q v hv_p hv_q).1.vertices

Docstring: The crowded point v is in the first exchanged path's vertices.
Since head_p ends at v, and concat uses head_p.vertices ++ tail_q.vertices.tail,
v is in the first path. 

## PROJECT DEPENDENCY LGV.exchangeTails_snd_mem_v (theorem)
∀ {V : Type u_3} [inst : DecidableEq V] {D : LGV.SimpleDigraph V} (p q : D.Path) (v : V) (hv_p : v ∈ p.vertices)
  (hv_q : v ∈ q.vertices), v ∈ (LGV.exchangeTails p q v hv_p hv_q).2.vertices

Docstring: The crowded point v is in the second exchanged path's vertices.
Since head_q ends at v, and concat uses head_q.vertices ++ tail_p.vertices.tail,
v is in the second path. 

## PROJECT DEPENDENCY LGV.SimpleDigraph.Path.start (def)
{V : Type u_1} → {D : LGV.SimpleDigraph V} → D.Path → V

Body:
fun {V} {D} p => p.vertices.head ⋯

Docstring: The starting vertex of a path 

## PROJECT DEPENDENCY LGV.SimpleDigraph.Path.finish (def)
{V : Type u_1} → {D : LGV.SimpleDigraph V} → D.Path → V

Body:
fun {V} {D} p => p.vertices.getLast ⋯

Docstring: The ending vertex of a path 

## PROJECT DEPENDENCY LGV.SimpleDigraph.arc (def)
{V : Type u_1} → LGV.SimpleDigraph V → V → V → Prop

Body:
fun V self => self.1

Docstring: The arc relation: `arc u v` means there is an arc from `u` to `v` 

## PROJECT DEPENDENCY LGV.SimpleDigraph.Path.splitAt (def)
{V : Type u_3} → [DecidableEq V] → {D : LGV.SimpleDigraph V} → (p : D.Path) → (v : V) → v ∈ p.vertices → D.Path × D.Path

Body:
fun {V} [DecidableEq V] {D} p v hv =>
  let idx := List.findIdx (fun x => decide (x = v)) p.vertices;
  let head := List.take (idx + 1) p.vertices;
  let tail := List.drop idx p.vertices;
  have h_idx_lt := ⋯;
  have h_head_ne := ⋯;
  have h_tail_ne := ⋯;
  have h_head_arcs := ⋯;
  have h_tail_arcs := ⋯;
  ({ vertices := head, nonempty := h_head_ne, arcs_valid := h_head_arcs },
    { vertices := tail, nonempty := h_tail_ne, arcs_valid := h_tail_arcs })

Docstring: Split a path at a vertex v, returning (head ending at v, tail starting at v).
The head includes v, the tail starts at v. 

## PROJECT DEPENDENCY LGV.SimpleDigraph.Path.concat (def)
{V : Type u_3} → {D : LGV.SimpleDigraph V} → (p q : D.Path) → p.finish = q.start → D.Path

Body:
fun {V} {D} p q hpq =>
  let vertices := p.vertices ++ q.vertices.tail;
  have h_ne := ⋯;
  have h_arcs := ⋯;
  { vertices := vertices, nonempty := h_ne, arcs_valid := h_arcs }

Docstring: Concatenate two paths where the first path ends at v and the second starts at v.
The resulting path goes from the start of the first to the end of the second.
The vertex v appears once in the result (not duplicated). 

## PROJECT DEPENDENCY LGV.SimpleDigraph.Path.nonempty (theorem)
∀ {V : Type u_1} {D : LGV.SimpleDigraph V} (self : D.Path), self.vertices ≠ []

Docstring: The path is nonempty 

## PROJECT DEPENDENCY LGV.SimpleDigraph.Path.mk (constructor)
{V : Type u_1} →
  {D : LGV.SimpleDigraph V} →
    (vertices : List V) →
      vertices ≠ [] →
        (∀ (i : ℕ) (hi : i + 1 < vertices.length), D.arc (vertices.get ⟨i, ⋯⟩) (vertices.get ⟨i + 1, hi⟩)) → D.Path

## BASE-LIBRARY REF DecidableEq
Sort u → Sort (max 1 u)

Docstring: Propositional equality is `Decidable` for all elements of a type.

In other words, an instance of `DecidableEq α` is a means of deciding the proposition `a = b` is
for all `a b : α`.


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

## BASE-LIBRARY REF Prod.fst
{α : Type u} → {β : Type v} → α × β → α

Docstring: The first element of a pair. 

## BASE-LIBRARY REF Prod.snd
{α : Type u} → {β : Type v} → α × β → β

Docstring: The second element of a pair. 

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

## BASE-LIBRARY REF Prod
Type u → Type v → Type (max u v)

Docstring: The product type, usually written `α × β`. Product types are also called pair or tuple types.
Elements of this type are pairs in which the first element is an `α` and the second element is a
`β`.

Products nest to the right, so `(x, y, z) : α × β × γ` is equivalent to `(x, (y, z)) : α × (β × γ)`.


Conventions for notations in identifiers:

 * The recommended spelling of `×` in identifiers is `Prod`.

## BASE-LIBRARY REF Prod.mk
{α : Type u} → {β : Type v} → α → β → α × β

Docstring: Constructs a pair. This is usually written `(x, y)` instead of `Prod.mk x y`.


Conventions for notations in identifiers:

 * The recommended spelling of `(a, b)` in identifiers is `mk`.

## BASE-LIBRARY REF Not
Prop → Prop

Docstring: `Not p`, or `¬p`, is the negation of `p`. It is defined to be `p → False`,
so if your goal is `¬p` you can use `intro h` to turn the goal into
`h : p ⊢ False`, and if you have `hn : ¬p` and `h : p` then `hn h : False`
and `(hn h).elim` will prove anything.
For more information: [Propositional Logic](https://lean-lang.org/theorem_proving_in_lean4/propositions_and_proofs.html#propositional-logic)


Conventions for notations in identifiers:

 * The recommended spelling of `¬` in identifiers is `not`.

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF List.length
{α : Type u_1} → List α → ℕ

Docstring: The length of a list.

This function is overridden in the compiler to `lengthTR`, which uses constant stack space.

Examples:
* `([] : List String).length = 0`
* `["green", "brown"].length = 2`


## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

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

## BASE-LIBRARY REF List.head
{α : Type u} → (as : List α) → as ≠ [] → α

Docstring: Returns the first element of a non-empty list.


## BASE-LIBRARY REF List.getLast
{α : Type u} → (as : List α) → as ≠ [] → α

Docstring: Returns the last element of a non-empty list.

Examples:
* `["circle", "rectangle"].getLast (by decide) = "rectangle"`
* `["circle"].getLast (by decide) = "circle"`


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


## BASE-LIBRARY REF List.take
{α : Type u} → ℕ → List α → List α

Docstring: Extracts the first `n` elements of `xs`, or the whole list if `n` is greater than `xs.length`.

`O(min n |xs|)`.

Examples:
* `[a, b, c, d, e].take 0 = []`
* `[a, b, c, d, e].take 3 = [a, b, c]`
* `[a, b, c, d, e].take 6 = [a, b, c, d, e]`


## BASE-LIBRARY REF List.drop
{α : Type u} → ℕ → List α → List α

Docstring: Removes the first `n` elements of the list `xs`. Returns the empty list if `n` is greater than the
length of the list.

`O(min n |xs|)`.

Examples:
* `[0, 1, 2, 3, 4].drop 0 = [0, 1, 2, 3, 4]`
* `[0, 1, 2, 3, 4].drop 3 = [3, 4]`
* `[0, 1, 2, 3, 4].drop 6 = []`


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

## BASE-LIBRARY REF List.tail
{α : Type u} → List α → List α

Docstring: Drops the first element of a nonempty list, returning the tail. Returns `[]` when the argument is
empty.

Examples:
 * `["apple", "banana", "grape"].tail = ["banana", "grape"]`
 * `["apple"].tail = []`
 * `([] : List String).tail = []`


## INFORMAL STATEMENT
Exchange of tails is an involution

\leanhelper  Let $D$ be an acyclic digraph, and let $p, q$ be paths sharing a vertex $v$. Let $(p', q')$ be the result of exchanging the tails of $p$ and $q$ at $v$. Then exchanging the tails of $p'$ and $q'$ at $v$ returns $(p, q)$.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The blueprint assumes \u201can acyclic digraph\u201d and paths \u201csharing a vertex v\u201d; the target has exactly `D.IsAcyclic \u2192 \u2200 (p q : D.Path) (v : V) (hv_p : v \u2208 p.vertices) (hv_q : v \u2208 q.vertices)`. It defines `p'` and `q'` as the two components of `LGV.exchangeTails p q v hv_p hv_q`, then concludes that exchanging at `v` again gives `(p, q)`, exactly matching \u201cexchanging the tails of p\u2032 and q\u2032 at v returns (p, q).\u201d The `[DecidableEq V]` binder supports the computational definition of `Path.splitAt`, which uses `List.findIdx` and equality testing; it is an encoding requirement rather than an additional graph-theoretic hypothesis."
}