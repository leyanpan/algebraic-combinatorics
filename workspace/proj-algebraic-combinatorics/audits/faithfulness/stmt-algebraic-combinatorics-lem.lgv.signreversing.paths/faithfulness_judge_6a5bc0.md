## TARGET LGV.signReversing_paths (theorem) — ELABORATED SIGNATURE
∀ {V : Type u_3} [inst : DecidableEq V] {D : LGV.SimpleDigraph V} (hac : D.IsAcyclic) {k : ℕ} {A B : LGV.kVertex V k}
  (sp : LGV.pathTupleWithPerm A B) (hip : sp.snd.isIntersecting),
  ∃ i j,
    i ≠ j ∧
      ∃ v,
        ∃ (hvi : v ∈ (sp.snd.paths i).vertices) (hvj : v ∈ (sp.snd.paths j).vertices),
          (LGV.signReversing hac sp hip).snd.paths i =
              (LGV.exchangeTails (sp.snd.paths i) (sp.snd.paths j) v hvi hvj).1 ∧
            (LGV.signReversing hac sp hip).snd.paths j =
                (LGV.exchangeTails (sp.snd.paths i) (sp.snd.paths j) v hvi hvj).2 ∧
              ∀ (l : Fin k), l ≠ i → l ≠ j → (LGV.signReversing hac sp hip).snd.paths l = sp.snd.paths l

Docstring: The paths of signReversing are obtained by exchanging tails at indices i and j.
This captures the essential structural property of the sign-reversing involution
for the paths: paths at indices i and j have their tails exchanged at the crowded
point v, while all other paths remain unchanged. 

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

## PROJECT DEPENDENCY LGV.kVertex (def)
Type u_3 → ℕ → Type u_3

Body:
fun V k => Fin k → V

Docstring: A k-vertex is a k-tuple of vertices of D.
Definition def.lgv.path-tups(a) 

## PROJECT DEPENDENCY LGV.pathTupleWithPerm (def)
{V : Type u_3} → [DecidableEq V] → {D : LGV.SimpleDigraph V} → {k : ℕ} → LGV.kVertex V k → LGV.kVertex V k → Type u_3

Body:
fun {V} [DecidableEq V] {D} {k} A B => (σ : Equiv.Perm (Fin k)) × LGV.PathTuple D k A (LGV.permuteKVertex σ B)

Docstring: The set of path tuples from 𝐀 to σ(𝐁) paired with the permutation σ 

## PROJECT DEPENDENCY LGV.PathTuple.isIntersecting (def)
{V : Type u_3} →
  [inst : DecidableEq V] → {D : LGV.SimpleDigraph V} → {k : ℕ} → {A B : LGV.kVertex V k} → LGV.PathTuple D k A B → Prop

Body:
fun {V} [DecidableEq V] {D} {k} {A B} pt => ¬pt.isNonIntersecting

Docstring: A path tuple is intersecting (ipat) if some two paths share a vertex.
Definition def.lgv.path-tups(e) 

## PROJECT DEPENDENCY LGV.permuteKVertex (def)
{V : Type u_3} → {k : ℕ} → Equiv.Perm (Fin k) → LGV.kVertex V k → LGV.kVertex V k

Body:
fun {V} {k} σ A i => A (σ i)

Docstring: Permute a k-vertex by a permutation σ: σ(𝐀) = (A_{σ(1)}, A_{σ(2)}, ..., A_{σ(k)}).
Definition def.lgv.path-tups(b) 

## PROJECT DEPENDENCY LGV.PathTuple (inductive)
{V : Type u_3} → [DecidableEq V] → LGV.SimpleDigraph V → (k : ℕ) → LGV.kVertex V k → LGV.kVertex V k → Type u_3

Body:
LGV.PathTuple.mk : {V : Type u_3} →
  [inst : DecidableEq V] →
    {D : LGV.SimpleDigraph V} →
      {k : ℕ} →
        {A B : LGV.kVertex V k} →
          (paths : Fin k → D.Path) →
            (∀ (i : Fin k), (paths i).start = A i) → (∀ (i : Fin k), (paths i).finish = B i) → LGV.PathTuple D k A B

Docstring: A path tuple from 𝐀 to 𝐁 is a k-tuple (p₁, ..., pₖ) where pᵢ is a path from Aᵢ to Bᵢ.
Definition def.lgv.path-tups(c) 

## PROJECT DEPENDENCY LGV.SimpleDigraph.Path.vertices (def)
{V : Type u_1} → {D : LGV.SimpleDigraph V} → D.Path → List V

Body:
fun V D self => self.1

Docstring: The vertices of the path, in order 

## PROJECT DEPENDENCY LGV.PathTuple.paths (def)
{V : Type u_3} →
  [inst : DecidableEq V] →
    {D : LGV.SimpleDigraph V} → {k : ℕ} → {A B : LGV.kVertex V k} → LGV.PathTuple D k A B → Fin k → D.Path

Body:
fun V [DecidableEq V] D k A B self => self.1

Docstring: The paths in the tuple 

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

## PROJECT DEPENDENCY LGV.signReversing (def)
{V : Type u_3} →
  [inst : DecidableEq V] →
    {D : LGV.SimpleDigraph V} →
      D.IsAcyclic →
        {k : ℕ} →
          {A B : LGV.kVertex V k} → (sp : LGV.pathTupleWithPerm A B) → sp.snd.isIntersecting → LGV.pathTupleWithPerm A B

Body:
fun {V} [DecidableEq V] {D} _hac {k} {A B} sp hip =>
  match LGV.getCanonicalIntersectionData sp.snd hip with
  | ⟨⟨i, ⟨j, ⟨v, ⋯⟩⟩⟩, hij⟩ =>
    let newPaths := fun l =>
      if h : l = i then (LGV.exchangeTails (sp.snd.paths i) (sp.snd.paths j) v hvi hvj).1
      else if h' : l = j then (LGV.exchangeTails (sp.snd.paths i) (sp.snd.paths j) v hvi hvj).2 else sp.snd.paths l;
    have h_starts := ⋯;
    have h_finishes := ⋯;
    ⟨sp.fst * Equiv.swap i j, { paths := newPaths, starts := h_starts, finishes := h_finishes }⟩

Docstring: The sign-reversing involution on intersecting path tuples.
For an ipat (σ, 𝐩), we:
1. Find the smallest i such that p_i contains a crowded point
2. Find the first crowded point v on p_i
3. Find the largest j such that v is on p_j
4. Exchange tails of p_i and p_j at v
5. Compose σ with the transposition t_{i,j}
This gives (σ ∘ t_{i,j}, 𝐩') which is still an ipat.

**Implementation note:** The permutation component is `sp.1 * Equiv.swap i j` where
i and j are the intersection indices. The path tuple component uses `exchangeTails`
to swap the tails of paths i and j at the crowded vertex v. 

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

## PROJECT DEPENDENCY LGV.PathTuple.isNonIntersecting (def)
{V : Type u_3} →
  [inst : DecidableEq V] → {D : LGV.SimpleDigraph V} → {k : ℕ} → {A B : LGV.kVertex V k} → LGV.PathTuple D k A B → Prop

Body:
fun {V} [DecidableEq V] {D} {k} {A B} pt => ∀ (i j : Fin k), i ≠ j → ¬LGV.pathsIntersect (pt.paths i) (pt.paths j)

Docstring: A path tuple is non-intersecting (nipat) if no two paths share a vertex.
Definition def.lgv.path-tups(d) 

## PROJECT DEPENDENCY LGV.SimpleDigraph.arc (def)
{V : Type u_1} → LGV.SimpleDigraph V → V → V → Prop

Body:
fun V self => self.1

Docstring: The arc relation: `arc u v` means there is an arc from `u` to `v` 

## PROJECT DEPENDENCY LGV.getCanonicalIntersectionData (def)
{V : Type u_3} →
  [inst : DecidableEq V] →
    {D : LGV.SimpleDigraph V} →
      {k : ℕ} →
        {A B : LGV.kVertex V k} → (pt : LGV.PathTuple D k A B) → pt.isIntersecting → { data // data.fst ≠ data.snd.fst }

Body:
fun {V} [DecidableEq V] {D} {k} {A B} pt hip =>
  have hne := ⋯;
  let i := pt.crowdedPathIndices.min' hne;
  have hi := ⋯;
  let idx := pt.firstCrowdedIndexOnPath i;
  have h_idx := ⋯;
  let v := (pt.paths i).vertices.get ⟨idx, h_idx⟩;
  have hv_crowded := ⋯;
  have hv_i := ⋯;
  have h_sdiff_ne := ⋯;
  let j := (pt.pathIndicesContaining v \ {i}).max' h_sdiff_ne;
  have hj_mem := ⋯;
  have hj_ne_i := ⋯;
  have hv_j := ⋯;
  ⟨⟨i, ⟨j, ⟨v, ⋯⟩⟩⟩, ⋯⟩

Docstring: Canonical intersection data: deterministically selects (i, j, v) for an intersecting path tuple.
- i = smallest crowded path index
- v = first crowded vertex on path i
- j = largest path index containing v (other than i) 

## PROJECT DEPENDENCY LGV.PathTuple.mk (constructor)
{V : Type u_3} →
  [inst : DecidableEq V] →
    {D : LGV.SimpleDigraph V} →
      {k : ℕ} →
        {A B : LGV.kVertex V k} →
          (paths : Fin k → D.Path) →
            (∀ (i : Fin k), (paths i).start = A i) → (∀ (i : Fin k), (paths i).finish = B i) → LGV.PathTuple D k A B

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

## PROJECT DEPENDENCY LGV.pathsIntersect (def)
{V : Type u_3} → [DecidableEq V] → {D : LGV.SimpleDigraph V} → D.Path → D.Path → Prop

Body:
fun {V} [DecidableEq V] {D} p q => ∃ v ∈ p.vertices, v ∈ q.vertices

Docstring: Two paths have a vertex in common 

## PROJECT DEPENDENCY LGV.PathTuple.crowdedPathIndices (def)
{V : Type u_3} →
  [inst : DecidableEq V] →
    {D : LGV.SimpleDigraph V} → {k : ℕ} → {A B : LGV.kVertex V k} → LGV.PathTuple D k A B → Finset (Fin k)

Body:
fun {V} [DecidableEq V] {D} {k} {A B} pt =>
  {i | ∃ j, i ≠ j ∧ ((pt.paths i).vertices.toFinset ∩ (pt.paths j).vertices.toFinset).Nonempty}

Docstring: The set of path indices that have a crowded vertex (shared with another path) 

## PROJECT DEPENDENCY LGV.PathTuple.minCrowdedPathIndex (def)
{V : Type u_3} →
  [inst : DecidableEq V] →
    {D : LGV.SimpleDigraph V} →
      {k : ℕ} → {A B : LGV.kVertex V k} → (pt : LGV.PathTuple D k A B) → pt.isIntersecting → Fin k

Body:
fun {V} [DecidableEq V] {D} {k} {A B} pt hip => pt.crowdedPathIndices.min' ⋯

Docstring: Get the smallest crowded path index. 

## PROJECT DEPENDENCY LGV.PathTuple.firstCrowdedIndexOnPath (def)
{V : Type u_3} →
  [inst : DecidableEq V] →
    {D : LGV.SimpleDigraph V} → {k : ℕ} → {A B : LGV.kVertex V k} → LGV.PathTuple D k A B → Fin k → ℕ

Body:
fun {V} [DecidableEq V] {D} {k} {A B} pt i =>
  List.findIdx (fun v => decide (v ∈ pt.crowdedVerticesOnPath i)) (pt.paths i).vertices

Docstring: The index of the first crowded vertex on a path (by position) 

## PROJECT DEPENDENCY LGV.PathTuple.firstCrowdedIndexOnPath_lt_length (theorem)
∀ {V : Type u_3} [inst : DecidableEq V] {D : LGV.SimpleDigraph V} {k : ℕ} {A B : LGV.kVertex V k}
  (pt : LGV.PathTuple D k A B), ∀ i ∈ pt.crowdedPathIndices, pt.firstCrowdedIndexOnPath i < (pt.paths i).vertices.length

Docstring: The first crowded vertex on path i (when i is a crowded path index) exists in the path 

## PROJECT DEPENDENCY LGV.PathTuple.crowdedVerticesOnPath (def)
{V : Type u_3} →
  [inst : DecidableEq V] →
    {D : LGV.SimpleDigraph V} → {k : ℕ} → {A B : LGV.kVertex V k} → LGV.PathTuple D k A B → Fin k → Finset V

Body:
fun {V} [DecidableEq V] {D} {k} {A B} pt i =>
  {v ∈ (pt.paths i).vertices.toFinset | ∃ j, i ≠ j ∧ v ∈ (pt.paths j).vertices}

Docstring: The set of crowded vertices on a specific path 

## PROJECT DEPENDENCY LGV.PathTuple.firstCrowdedVertex_mem_crowdedVerticesOnPath (theorem)
∀ {V : Type u_3} [inst : DecidableEq V] {D : LGV.SimpleDigraph V} {k : ℕ} {A B : LGV.kVertex V k}
  (pt : LGV.PathTuple D k A B) (i : Fin k) (hi : i ∈ pt.crowdedPathIndices),
  let idx := pt.firstCrowdedIndexOnPath i;
  have h := ⋯;
  (pt.paths i).vertices.get ⟨idx, h⟩ ∈ pt.crowdedVerticesOnPath i

Docstring: The vertex at firstCrowdedIndexOnPath is in crowdedVerticesOnPath 

## PROJECT DEPENDENCY LGV.PathTuple.pathIndicesContaining (def)
{V : Type u_3} →
  [inst : DecidableEq V] →
    {D : LGV.SimpleDigraph V} → {k : ℕ} → {A B : LGV.kVertex V k} → LGV.PathTuple D k A B → V → Finset (Fin k)

Body:
fun {V} [DecidableEq V] {D} {k} {A B} pt v => {i | v ∈ (pt.paths i).vertices}

Docstring: The set of path indices that contain a given vertex 

## PROJECT DEPENDENCY LGV.PathTuple.pathIndicesContaining_sdiff_singleton_nonempty (theorem)
∀ {V : Type u_3} [inst : DecidableEq V] {D : LGV.SimpleDigraph V} {k : ℕ} {A B : LGV.kVertex V k}
  (pt : LGV.PathTuple D k A B),
  ∀ i ∈ pt.crowdedPathIndices, ∀ v ∈ pt.crowdedVerticesOnPath i, (pt.pathIndicesContaining v \ {i}).Nonempty

Docstring: If i is a crowded path index, the set of other path indices containing a crowded vertex on i
is nonempty 

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


## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF Sigma.fst
{α : Type u} → {β : α → Type v} → Sigma β → α

Docstring: The first component of a dependent pair.


## BASE-LIBRARY REF Equiv.Perm
Sort u_1 → Sort (max 1 u_1)

Docstring: `Perm α` is the type of bijections from `α` to itself. 

## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


## BASE-LIBRARY REF Sigma.snd
{α : Type u} → {β : α → Type v} → (self : Sigma β) → β self.fst

Docstring: The second component of a dependent pair. Its type depends on the first component.


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

## BASE-LIBRARY REF Ne
{α : Sort u} → α → α → Prop

Docstring: `a ≠ b`, or `Ne a b` is defined as `¬ (a = b)` or `a = b → False`,
and asserts that `a` and `b` are not equal.


Conventions for notations in identifiers:

 * The recommended spelling of `≠` in identifiers is `ne`.

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

## BASE-LIBRARY REF Sigma
{α : Type u} → (α → Type v) → Type (max u v)

Docstring: Dependent pairs, in which the second element's type depends on the value of the first element. The
type `Sigma β` is typically written `Σ a : α, β a` or `(a : α) × β a`.

Although its values are pairs, `Sigma` is sometimes known as the *dependent sum type*, since it is
the type level version of an indexed summation.


## BASE-LIBRARY REF DFunLike.coe
{F : Sort u_1} → {α : outParam (Sort u_2)} → {β : outParam (α → Sort u_3)} → [self : DFunLike F α β] → F → (a : α) → β a

Docstring: The coercion from `F` to a function. 

## BASE-LIBRARY REF EquivLike.toFunLike
{E : Sort u_1} → {α : Sort u_3} → {β : Sort u_4} → [EquivLike E α β] → FunLike E α β

## BASE-LIBRARY REF Equiv.instEquivLike
{α : Sort u} → {β : Sort v} → EquivLike (α ≃ β) α β

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

## BASE-LIBRARY REF Sigma.mk
{α : Type u} → {β : α → Type v} → (fst : α) → β fst → Sigma β

Docstring: Constructs a dependent pair.

Using this constructor in a context in which the type is not known usually requires a type
ascription to determine `β`. This is because the desired relationship between the two values can't
generally be determined automatically.


## BASE-LIBRARY REF Subtype.mk
{α : Sort u} → {p : α → Prop} → (val : α) → p val → Subtype p

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


## BASE-LIBRARY REF instDecidableEqFin
(n : ℕ) → DecidableEq (Fin n)

## BASE-LIBRARY REF HMul.hMul
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HMul α β γ] → α → β → γ

Docstring: `a * b` computes the product of `a` and `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `*` in identifiers is `mul`.

## BASE-LIBRARY REF instHMul
{α : Type u_1} → [Mul α] → HMul α α α

## BASE-LIBRARY REF Equiv.Perm.instMul
{α : Type u_4} → Mul (Equiv.Perm α)

## BASE-LIBRARY REF Equiv.swap
{α : Sort u_1} → [DecidableEq α] → α → α → Equiv.Perm α

Docstring: `swap a b` is the permutation that swaps `a` and `b` and
leaves other values as is. 

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

## BASE-LIBRARY REF List.head
{α : Type u} → (as : List α) → as ≠ [] → α

Docstring: Returns the first element of a non-empty list.


## BASE-LIBRARY REF List.getLast
{α : Type u} → (as : List α) → as ≠ [] → α

Docstring: Returns the last element of a non-empty list.

Examples:
* `["circle", "rectangle"].getLast (by decide) = "rectangle"`
* `["circle"].getLast (by decide) = "circle"`


## BASE-LIBRARY REF Finset.Nonempty
{α : Type u_1} → Finset α → Prop

Docstring: The property `s.Nonempty` expresses the fact that the finset `s` is not empty. It should be used
in theorem assumptions instead of `∃ x, x ∈ s` or `s ≠ ∅` as it gives access to a nice API thanks
to the dot notation. 

## BASE-LIBRARY REF Finset.min'
{α : Type u_2} → [LinearOrder α] → (s : Finset α) → s.Nonempty → α

Docstring: Given a nonempty finset `s` in a linear order `α`, then `s.min' H` is its minimum, as an
element of `α`, where `H` is a proof of nonemptiness. Without this assumption, use instead `s.min`,
taking values in `WithTop α`. 

## BASE-LIBRARY REF Fin.instLinearOrder
{n : ℕ} → LinearOrder (Fin n)

## BASE-LIBRARY REF Finset
Type u_4 → Type u_4

Docstring: `Finset α` is the type of finite sets of elements of `α`. It is implemented
as a multiset (a list up to permutation) which has no duplicate elements. 

## BASE-LIBRARY REF Finset.instMembership
{α : Type u_1} → Membership α (Finset α)

## BASE-LIBRARY REF SDiff.sdiff
{α : Type u} → [self : SDiff α] → α → α → α

Docstring: `a \ b` is the set difference of `a` and `b`,
consisting of all elements in `a` that are not in `b`.


Conventions for notations in identifiers:

 * The recommended spelling of `\` in identifiers is `sdiff`.

## BASE-LIBRARY REF Finset.instSDiff
{α : Type u_1} → [DecidableEq α] → SDiff (Finset α)

Docstring: `s \ t` is the set consisting of the elements of `s` that are not in `t`. 

## BASE-LIBRARY REF Singleton.singleton
{α : outParam (Type u)} → {β : Type v} → [self : Singleton α β] → α → β

Docstring: `singleton x` is a collection with the single element `x` (notation: `{x}`). 

Conventions for notations in identifiers:

 * The recommended spelling of `{x}` in identifiers is `singleton`.

## BASE-LIBRARY REF Finset.instSingleton
{α : Type u_1} → Singleton α (Finset α)

Docstring: `{a} : Finset a` is the set `{a}` containing `a` and nothing else.

This differs from `insert a ∅` in that it does not require a `DecidableEq` instance for `α`.


## BASE-LIBRARY REF Finset.max'
{α : Type u_2} → [LinearOrder α] → (s : Finset α) → s.Nonempty → α

Docstring: Given a nonempty finset `s` in a linear order `α`, then `s.max' H` is its maximum, as an
element of `α`, where `H` is a proof of nonemptiness. Without this assumption, use instead `s.max`,
taking values in `WithBot α`. 

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


## BASE-LIBRARY REF Finset.filter
{α : Type u_1} → (p : α → Prop) → [DecidablePred p] → Finset α → Finset α

Docstring: `Finset.filter p s` is the set of elements of `s` that satisfy `p`.

For example, one can use `s.filter (· ∈ t)` to get the intersection of `s` with `t : Set α`
as a `Finset α` (when a `DecidablePred (· ∈ t)` instance is available). 

## BASE-LIBRARY REF Inter.inter
{α : Type u} → [self : Inter α] → α → α → α

Docstring: `a ∩ b` is the intersection of `a` and `b`. 

Conventions for notations in identifiers:

 * The recommended spelling of `∩` in identifiers is `inter`.

## BASE-LIBRARY REF Finset.instInter
{α : Type u_1} → [DecidableEq α] → Inter (Finset α)

Docstring: `s ∩ t` is the set such that `a ∈ s ∩ t` iff `a ∈ s` and `a ∈ t`. 

## BASE-LIBRARY REF List.toFinset
{α : Type u_1} → [DecidableEq α] → List α → Finset α

Docstring: `toFinset l` removes duplicates from the list `l` to produce a finset. 

## BASE-LIBRARY REF Nat.decidableExistsFin
{n : ℕ} → (P : Fin n → Prop) → [DecidablePred P] → Decidable (∃ i, P i)

## BASE-LIBRARY REF instDecidableAnd
{p q : Prop} → [dp : Decidable p] → [dq : Decidable q] → Decidable (p ∧ q)

## BASE-LIBRARY REF instDecidableNot
{p : Prop} → [dp : Decidable p] → Decidable ¬p

## BASE-LIBRARY REF Finset.decidableNonempty
{α : Type u_1} → {s : Finset α} → Decidable s.Nonempty

## BASE-LIBRARY REF Finset.univ
{α : Type u_1} → [Fintype α] → Finset α

Docstring: `univ` is the universal finite set of type `Finset α` implied from
the assumption `Fintype α`. 

## BASE-LIBRARY REF Fin.fintype
(n : ℕ) → Fintype (Fin n)

## BASE-LIBRARY REF Finset.decidableMem
{α : Type u_1} → [_h : DecidableEq α] → (a : α) → (s : Finset α) → Decidable (a ∈ s)

## BASE-LIBRARY REF List.instDecidableMemOfLawfulBEq
{α : Type u} → [inst : BEq α] → [LawfulBEq α] → (a : α) → (as : List α) → Decidable (a ∈ as)

## BASE-LIBRARY REF instBEqOfDecidableEq
{α : Type u_1} → [DecidableEq α] → BEq α

## BASE-LIBRARY REF instLawfulBEq
∀ {α : Type u_1} [inst : DecidableEq α], LawfulBEq α

## INFORMAL STATEMENT
Paths of sign-reversing map

\leanhelper  The sign-reversing map $\varphi $ applied to $(\sigma , \mathbf{p})$ produces paths $\mathbf{p}'$ such that: paths at indices $i$ and $j$ have their tails exchanged at the crowded vertex $v$, while all other paths remain unchanged.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.lgv.crowded
def.lgv.crowded

\leanhelper  Let $\mathbf{p} = (p_1, \ldots , p_k)$ be a path tuple. 

\textbf{(a)} A vertex $v$ is \emph{crowded} in $\mathbf{p}$ if $v$ lies on at least two distinct paths $p_i, p_j$ with $i \ne j$. 

\textbf{(b)} The \emph{crowded path indices} of $\mathbf{p}$ is the set of indices $i$ such that $p_i$ contains a vertex shared with some other path $p_j$. 

\textbf{(c)} For an ipat $\mathbf{p}$, the \emph{minimum crowded path index} is the smallest $i$ in the crowded path indices. 

\textbf{(d)} The \emph{crowded vertices on path $i$} is the set of vertices on $p_i$ that also appear on some other path.

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

## VERDICT
{
  "verdict": "faithful",
  "justification": "The formal conclusion exactly captures the stated path behavior: it provides distinct indices and a common vertex, `\u2203 i j, i \u2260 j \u2227 \u2203 v, \u2203 (hvi : v \u2208 ...paths i...vertices) (hvj : v \u2208 ...paths j...vertices)`, so `v` is crowded in the informal sense, and asserts that the two output paths are the components of `LGV.exchangeTails ... v hvi hvj`, while `\u2200 (l : Fin k), l \u2260 i \u2192 l \u2260 j \u2192 ...paths l = sp.snd.paths l` says every other path is unchanged. This matches \u201cpaths at indices i and j have their tails exchanged at the crowded vertex v, while all other paths remain unchanged.\u201d The binders `{D : LGV.SimpleDigraph V} (hac : D.IsAcyclic)` generalize the lattice setting: the informal integer lattice is acyclic, while the Lean theorem works for every acyclic simple digraph. `[DecidableEq V]` supports the computational definitions of intersection and splitting and is not a substantive restriction in the blueprint\u2019s lattice setting."
}