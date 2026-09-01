## TARGET LGV.exchangeTails_weight (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_2} [inst : CommRing K] {V : Type u_3} [inst_1 : DecidableEq V] {D : LGV.SimpleDigraph V}
  (w : LGV.ArcWeight D K) (p q : D.Path) (v : V) (hv_p : v ∈ p.vertices) (hv_q : v ∈ q.vertices),
  LGV.pathWeight w p * LGV.pathWeight w q =
    LGV.pathWeight w (LGV.exchangeTails p q v hv_p hv_q).1 * LGV.pathWeight w (LGV.exchangeTails p q v hv_p hv_q).2

Docstring: Exchanging tails preserves the total weight.


**Proof outline:** The key insight is that `pathWeight` is multiplicative over path
concatenation: if p = p₁ ++ p₂ (concatenation at a shared vertex), then
w(p) = w(p₁) * w(p₂).

When we exchange tails at vertex v:
- p has weight w(p_head) * w(p_tail) where p_head ends at v and p_tail starts at v
- q has weight w(q_head) * w(q_tail) where q_head ends at v and q_tail starts at v
- p' = p_head ++ q_tail has weight w(p_head) * w(q_tail)
- q' = q_head ++ p_tail has weight w(q_head) * w(p_tail)

Thus: w(p) * w(q) = w(p_head) * w(p_tail) * w(q_head) * w(q_tail)
                  = w(p_head) * w(q_tail) * w(q_head) * w(p_tail)  (by commutativity)
                  = w(p') * w(q')

**Status:** Now that `exchangeTails` is defined, the proof follows from
multiplicativity of `pathWeight` and commutativity of multiplication in K.
The proof requires showing pathWeight is multiplicative over path concatenation. 

## PROJECT DEPENDENCY LGV.SimpleDigraph (inductive)
Type u_1 → Type u_1

Body:
LGV.SimpleDigraph.mk : {V : Type u_1} → (arc : V → V → Prop) → (∀ (v : V), ¬arc v v) → LGV.SimpleDigraph V

Docstring: A simple digraph with vertex set V.
Convention conv.lgv.digraph(d): A simple digraph has arcs as pairs of distinct vertices. 

## PROJECT DEPENDENCY LGV.ArcWeight (def)
{V : Type u_1} → LGV.SimpleDigraph V → Type u_3 → Type (max u_1 u_3)

Body:
fun {V} D K => (u v : V) → D.arc u v → K

Docstring: An arc weight function assigns a ring element to each arc.
Definition in Theorem thm.lgv.kpaths.wt 

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

## PROJECT DEPENDENCY LGV.pathWeight (def)
{V : Type u_1} → {K : Type u_2} → [CommRing K] → {D : LGV.SimpleDigraph V} → LGV.ArcWeight D K → D.Path → K

Body:
fun {V} {K} [CommRing K] {D} w p => LGV.pathWeightAux w p.vertices ⋯

Docstring: The weight of a path is the product of weights of its arcs.
w(p) := ∏_{a is an arc of p} w(a) 

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

## PROJECT DEPENDENCY LGV.SimpleDigraph.arc (def)
{V : Type u_1} → LGV.SimpleDigraph V → V → V → Prop

Body:
fun V self => self.1

Docstring: The arc relation: `arc u v` means there is an arc from `u` to `v` 

## PROJECT DEPENDENCY LGV.pathWeightAux (def)
{V : Type u_1} →
  {K : Type u_2} →
    [CommRing K] →
      {D : LGV.SimpleDigraph V} →
        LGV.ArcWeight D K →
          (vertices : List V) →
            (∀ (i : ℕ) (hi : i + 1 < vertices.length), D.arc (vertices.get ⟨i, ⋯⟩) (vertices.get ⟨i + 1, hi⟩)) → K

Body:
fun {V} {K} [CommRing K] {D} w vertices arcs_valid =>
  List.brecOn (motive := fun vertices =>
    (∀ (i : ℕ) (hi : i + 1 < vertices.length), D.arc (vertices.get ⟨i, ⋯⟩) (vertices.get ⟨i + 1, hi⟩)) → K) vertices
    (fun vertices f arcs_valid =>
      (match (motive :=
          (vertices : List V) →
            (∀ (i : ℕ) (hi : i + 1 < vertices.length), D.arc (vertices.get ⟨i, ⋯⟩) (vertices.get ⟨i + 1, hi⟩)) →
              List.below (motive := fun vertices =>
                  (∀ (i : ℕ) (hi : i + 1 < vertices.length), D.arc (vertices.get ⟨i, ⋯⟩) (vertices.get ⟨i + 1, hi⟩)) →
                    K)
                  vertices →
                K)
          vertices, arcs_valid with
        | [], arcs_valid => fun x => 1
        | [head], arcs_valid => fun x => 1
        | v₀ :: v₁ :: rest, arcs_valid => fun x =>
          have h := ⋯;
          have arc_proof := ⋯;
          have rest_arcs_valid := ⋯;
          w v₀ v₁ arc_proof * x.1 rest_arcs_valid)
        f)
    arcs_valid

Docstring: Helper function to compute the product of arc weights along a vertex list.
Uses recursion on the structure of the list.
- For an empty list or single vertex, the weight is 1 (no arcs).
- For a list [v₀, v₁, ...], the weight is w(v₀, v₁) * (weight of [v₁, ...]). 

## PROJECT DEPENDENCY LGV.SimpleDigraph.Path.arcs_valid (theorem)
∀ {V : Type u_1} {D : LGV.SimpleDigraph V} (self : D.Path) (i : ℕ) (hi : i + 1 < self.vertices.length),
  D.arc (self.vertices.get ⟨i, ⋯⟩) (self.vertices.get ⟨i + 1, hi⟩)

Docstring: Consecutive vertices are connected by arcs 

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

## PROJECT DEPENDENCY LGV.SimpleDigraph.Path.finish (def)
{V : Type u_1} → {D : LGV.SimpleDigraph V} → D.Path → V

Body:
fun {V} {D} p => p.vertices.getLast ⋯

Docstring: The ending vertex of a path 

## PROJECT DEPENDENCY LGV.SimpleDigraph.Path.start (def)
{V : Type u_1} → {D : LGV.SimpleDigraph V} → D.Path → V

Body:
fun {V} {D} p => p.vertices.head ⋯

Docstring: The starting vertex of a path 

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

## PROJECT DEPENDENCY LGV.SimpleDigraph.Path.mk (constructor)
{V : Type u_1} →
  {D : LGV.SimpleDigraph V} →
    (vertices : List V) →
      vertices ≠ [] →
        (∀ (i : ℕ) (hi : i + 1 < vertices.length), D.arc (vertices.get ⟨i, ⋯⟩) (vertices.get ⟨i + 1, hi⟩)) → D.Path

## PROJECT DEPENDENCY LGV.SimpleDigraph.Path.nonempty (theorem)
∀ {V : Type u_1} {D : LGV.SimpleDigraph V} (self : D.Path), self.vertices ≠ []

Docstring: The path is nonempty 

## BASE-LIBRARY REF CommRing
Type u → Type u

Docstring: A commutative ring is a ring with commutative multiplication. 

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

## BASE-LIBRARY REF HMul.hMul
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HMul α β γ] → α → β → γ

Docstring: `a * b` computes the product of `a` and `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `*` in identifiers is `mul`.

## BASE-LIBRARY REF instHMul
{α : Type u_1} → [Mul α] → HMul α α α

## BASE-LIBRARY REF Distrib.toMul
{R : Type u_1} → [self : Distrib R] → Mul R

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.toDistrib
{α : Type u} → [self : NonUnitalNonAssocSemiring α] → Distrib α

## BASE-LIBRARY REF NonUnitalNonAssocRing.toNonUnitalNonAssocSemiring
{α : Type u} → [self : NonUnitalNonAssocRing α] → NonUnitalNonAssocSemiring α

## BASE-LIBRARY REF NonUnitalNonAssocCommRing.toNonUnitalNonAssocRing
{α : Type u} → [self : NonUnitalNonAssocCommRing α] → NonUnitalNonAssocRing α

## BASE-LIBRARY REF NonUnitalCommRing.toNonUnitalNonAssocCommRing
{α : Type u} → [self : NonUnitalCommRing α] → NonUnitalNonAssocCommRing α

## BASE-LIBRARY REF CommRing.toNonUnitalCommRing
{α : Type u} → [s : CommRing α] → NonUnitalCommRing α

## BASE-LIBRARY REF Prod.fst
{α : Type u} → {β : Type v} → α × β → α

Docstring: The first element of a pair. 

## BASE-LIBRARY REF Prod.snd
{α : Type u} → {β : Type v} → α × β → β

Docstring: The second element of a pair. 

## BASE-LIBRARY REF Not
Prop → Prop

Docstring: `Not p`, or `¬p`, is the negation of `p`. It is defined to be `p → False`,
so if your goal is `¬p` you can use `intro h` to turn the goal into
`h : p ⊢ False`, and if you have `hn : ¬p` and `h : p` then `hn h : False`
and `(hn h).elim` will prove anything.
For more information: [Propositional Logic](https://lean-lang.org/theorem_proving_in_lean4/propositions_and_proofs.html#propositional-logic)


Conventions for notations in identifiers:

 * The recommended spelling of `¬` in identifiers is `not`.

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

## BASE-LIBRARY REF List.brecOn
{α : Type u} → {motive : List α → Sort u_1} → (t : List α) → ((t : List α) → List.below t → motive t) → motive t

## BASE-LIBRARY REF List.below
{α : Type u} → {motive : List α → Sort u_1} → List α → Sort (max (u + 1) u_1)

## BASE-LIBRARY REF One.toOfNat1
{α : Type u_1} → [One α] → OfNat α 1

## BASE-LIBRARY REF AddMonoidWithOne.toOne
{R : Type u_2} → [self : AddMonoidWithOne R] → One R

## BASE-LIBRARY REF AddGroupWithOne.toAddMonoidWithOne
{R : Type u} → [self : AddGroupWithOne R] → AddMonoidWithOne R

## BASE-LIBRARY REF Ring.toAddGroupWithOne
{R : Type u} → [self : Ring R] → AddGroupWithOne R

## BASE-LIBRARY REF CommRing.toRing
{α : Type u} → [self : CommRing α] → Ring α

## BASE-LIBRARY REF List.cons
{α : Type u} → α → List α → List α

Docstring: The list whose first element is `head`, where `tail` is the rest of the list.
Usually written `head :: tail`.


Conventions for notations in identifiers:

 * The recommended spelling of `::` in identifiers is `cons`.

 * The recommended spelling of `[a]` in identifiers is `singleton`.

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


## BASE-LIBRARY REF List.getLast
{α : Type u} → (as : List α) → as ≠ [] → α

Docstring: Returns the last element of a non-empty list.

Examples:
* `["circle", "rectangle"].getLast (by decide) = "rectangle"`
* `["circle"].getLast (by decide) = "circle"`


## BASE-LIBRARY REF List.head
{α : Type u} → (as : List α) → as ≠ [] → α

Docstring: Returns the first element of a non-empty list.


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
Exchange of tails preserves weight

\leanhelper  Let $D$ be an acyclic digraph with arc weight function $w$. Let $p$ and $q$ be two paths sharing a vertex $v$. Let $(p', q')$ be the result of exchanging the tails of $p$ and $q$ at $v$ (i.e., $p'$ takes the head of $p$ up to $v$ followed by the tail of $q$ from $v$, and symmetrically for $q'$). Then $w(p) \cdot w(q) = w(p') \cdot w(q')$.

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.lgv.path-tups
def.lgv.path-tups

Let $k\in \mathbb {N}$. 

\textbf{(a)} A $k$\emph{-vertex} means a $k$-tuple of lattice points. 

\textbf{(b)} If $\mathbf{A}=\left( A_{1},A_{2},\ldots ,A_{k}\right) $ is a $k$-vertex, and if $\sigma \in S_{k}$ is a permutation, then $\sigma \left( \mathbf{A}\right) $ shall denote the $k$-vertex $\left( A_{\sigma \left( 1\right) },A_{\sigma \left( 2\right) },\ldots ,A_{\sigma \left( k\right) }\right) $. 

\textbf{(c)} If $\mathbf{A}=\left( A_{1},A_{2},\ldots ,A_{k}\right) $ and $\mathbf{B}=\left( B_{1},B_{2},\ldots ,B_{k}\right) $ are two $k$-vertices, then a \emph{path tuple} from $\mathbf{A}$ to $\mathbf{B}$ means a $k$-tuple $\left( p_{1},p_{2},\ldots ,p_{k}\right) $, where each $p_{i}$ is a path from $A_{i}$ to $B_{i}$. 

\textbf{(d)} A path tuple $\left( p_{1},p_{2},\ldots ,p_{k}\right) $ is said to be \emph{non-intersecting} if no two of the paths $p_{1},p_{2},\ldots ,p_{k}$ have any vertex in common. We abbreviate “non-intersecting path tuple” as \emph{nipat}. 

\textbf{(e)} A path tuple $\left( p_{1},p_{2},\ldots ,p_{k}\right) $ is said to be \emph{intersecting} if it is not non-intersecting (i.e., if two of its paths have a vertex in common). We abbreviate “intersecting path tuple” as \emph{ipat}.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.perm
def.perm.perm

Let $X$ be a set. 

\textbf{(a)} A \emph{permutation} of $X$ means a bijection from $X$ to $X$. 

\textbf{(b)} It is known that the set of all permutations of $X$ is a group under composition. This group is called the \emph{symmetric group} of $X$, and is denoted by $S_X$. Its neutral element is the identity map $\operatorname {id}_X : X \to X$. Its size is $|X|!$ when $X$ is finite. 

\textbf{(c)} As usual in group theory, we will write $\alpha \beta $ for the composition $\alpha \circ \beta $ when $\alpha , \beta \in S_X$. This is the map that sends each $x \in X$ to $\alpha (\beta (x))$. 

\textbf{(d)} If $\alpha \in S_X$ and $i \in \mathbb {Z}$, then $\alpha ^i$ shall denote the $i$-th power of $\alpha $ in the group $S_X$. Note that $\alpha ^i = \underbrace{\alpha \circ \alpha \circ \cdots \circ \alpha }_{i\text{ times}}$ if $i \ge 0$. Also, $\alpha ^0 = \operatorname {id}_X$. Also, $\alpha ^{-1}$ is the inverse of $\alpha $ in the group $S_X$, that is, the inverse of the map $\alpha $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.jt-arc-weight
def.sf.jt-arc-weight

\leanhelper  The arc weight function for the Jacobi–Trudi proof on the integer lattice $\mathbb {Z}^2$: east-steps at height $y$ (with $1 \leq y \leq N$) are weighted by $x_{y-1}$; north-steps are weighted by $1$.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The formal conclusion exactly states the claimed weight preservation: `pathWeight w p * pathWeight w q = pathWeight w (...).1 * pathWeight w (...).2`, where `exchangeTails` is defined as `(head_p.concat tail_q ..., head_q.concat tail_p ...)`, matching the informal `(p', q')`. The informal hypothesis that `D` is \u201can acyclic digraph\u201d is omitted: the signature quantifies over every `{D : LGV.SimpleDigraph V}`. This is a valid strengthening/generalization, since it includes all acyclic simple digraphs and the identity does not require acyclicity. Likewise, repeated occurrences of `v` only arise in the extra generality; on an acyclic path the occurrence is unique, while `splitAt` selects the first occurrence in general. The binder `[DecidableEq V]` is an implementation-level requirement used by `splitAt` through `List.findIdx`, rather than a substantive restriction on the combinatorial claim. Finally, `[CommRing K]` supplies the commutative multiplication needed to reorder the four path-segment weights; the theorem is polymorphic over all such weight rings rather than being restricted to the particular lattice weights from the surrounding context."
}