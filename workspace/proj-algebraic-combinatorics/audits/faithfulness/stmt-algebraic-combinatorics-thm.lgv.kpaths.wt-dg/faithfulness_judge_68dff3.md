## TARGET LGV.lgv_weighted_digraph (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_2} [inst : CommRing K] {V : Type u_4} [inst_1 : DecidableEq V] {D : LGV.SimpleDigraph V}
  (hpf : D.IsPathFinite),
  D.IsAcyclic →
    ∀ {k : ℕ} (w : LGV.ArcWeight D K) (A B : LGV.kVertex V k),
      (LGV.pathWeightMatrix hpf w A B).det =
        ∑ σ, Equiv.Perm.sign σ • LGV.nipatWeightSum hpf w A (LGV.permuteKVertex σ B) σ

Docstring: LGV lemma, digraph weight version (Theorem thm.lgv.kpaths.wt-dg)
Label: thm.lgv.kpaths.wt-dg

For any path-finite acyclic digraph D with arc weights w ∈ K:
det((∑_{p : Aᵢ → Bⱼ} w(p))_{i,j}) = ∑_{σ ∈ Sₖ} (-1)^σ ∑_{𝐩 nipat from 𝐀 to σ(𝐁)} w(𝐩)

This generalizes the lattice version - we only use that D is path-finite and acyclic.

**Proof outline:**
1. By Leibniz formula: det(M) = ∑_σ (-1)^σ ∏_i M_{i,σ(i)}
2. Each M_{i,σ(i)} = ∑_{p : A_i → B_{σ(i)}} w(p), so the product expands to
   ∑_{𝐩 : path tuple from 𝐀 to σ(𝐁)} w(𝐩)
3. Thus det(M) = ∑_σ (-1)^σ ∑_{𝐩 : 𝐀 → σ(𝐁)} w(𝐩)
4. Split the inner sum into nipats and ipats
5. The sign-reversing involution on ipats shows ∑_{ipats} (-1)^σ w(𝐩) = 0
6. Only nipats remain: det(M) = ∑_σ (-1)^σ ∑_{𝐩 nipat from 𝐀 to σ(𝐁)} w(𝐩) 

## PROJECT DEPENDENCY LGV.SimpleDigraph (inductive)
Type u_1 → Type u_1

Body:
LGV.SimpleDigraph.mk : {V : Type u_1} → (arc : V → V → Prop) → (∀ (v : V), ¬arc v v) → LGV.SimpleDigraph V

Docstring: A simple digraph with vertex set V.
Convention conv.lgv.digraph(d): A simple digraph has arcs as pairs of distinct vertices. 

## PROJECT DEPENDENCY LGV.SimpleDigraph.IsPathFinite (def)
{V : Type u_1} → LGV.SimpleDigraph V → Prop

Body:
fun {V} D => ∀ (u v : V), {p | p.start = u ∧ p.finish = v}.Finite

Docstring: A digraph is path-finite if there are only finitely many paths between any two vertices.
Convention conv.lgv.digraph(b) 

## PROJECT DEPENDENCY LGV.SimpleDigraph.IsAcyclic (def)
{V : Type u_1} → LGV.SimpleDigraph V → Prop

Body:
fun {V} D => ∀ (p : D.Path), p.start = p.finish → p.vertices.length = 1

Docstring: A digraph is acyclic if it has no directed cycles.
Convention conv.lgv.digraph(c) 

## PROJECT DEPENDENCY LGV.ArcWeight (def)
{V : Type u_1} → LGV.SimpleDigraph V → Type u_3 → Type (max u_1 u_3)

Body:
fun {V} D K => (u v : V) → D.arc u v → K

Docstring: An arc weight function assigns a ring element to each arc.
Definition in Theorem thm.lgv.kpaths.wt 

## PROJECT DEPENDENCY LGV.kVertex (def)
Type u_3 → ℕ → Type u_3

Body:
fun V k => Fin k → V

Docstring: A k-vertex is a k-tuple of vertices of D.
Definition def.lgv.path-tups(a) 

## PROJECT DEPENDENCY LGV.pathWeightMatrix (def)
{K : Type u_2} →
  [CommRing K] →
    {V : Type u_3} →
      [DecidableEq V] →
        {D : LGV.SimpleDigraph V} →
          D.IsPathFinite → LGV.ArcWeight D K → {k : ℕ} → LGV.kVertex V k → LGV.kVertex V k → Matrix (Fin k) (Fin k) K

Body:
fun {K} [CommRing K] {V} [DecidableEq V] {D} hpf w {k} A B => Matrix.of fun i j => LGV.pathWeightSum hpf w (A i) (B j)

Docstring: The path weight matrix M_{i,j} = ∑_{p : Aᵢ → Bⱼ} w(p) 

## PROJECT DEPENDENCY LGV.nipatWeightSum (def)
{K : Type u_2} →
  [CommRing K] →
    {V : Type u_3} →
      [DecidableEq V] →
        {D : LGV.SimpleDigraph V} →
          D.IsPathFinite → LGV.ArcWeight D K → {k : ℕ} → LGV.kVertex V k → LGV.kVertex V k → Equiv.Perm (Fin k) → K

Body:
fun {K} [CommRing K] {V} [DecidableEq V] {D} hpf w {k} A B _σ =>
  ∑ pt ∈ LGV.nipatFinset hpf A B, LGV.pathTupleWeight w pt.paths

Docstring: Sum of weights over all nipats from 𝐀 to 𝐁
Note: σ is not used in this definition since the permutation is already
encoded in B (which should be permuteKVertex σ B' for some B') 

## PROJECT DEPENDENCY LGV.permuteKVertex (def)
{V : Type u_3} → {k : ℕ} → Equiv.Perm (Fin k) → LGV.kVertex V k → LGV.kVertex V k

Body:
fun {V} {k} σ A i => A (σ i)

Docstring: Permute a k-vertex by a permutation σ: σ(𝐀) = (A_{σ(1)}, A_{σ(2)}, ..., A_{σ(k)}).
Definition def.lgv.path-tups(b) 

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

## PROJECT DEPENDENCY LGV.SimpleDigraph.Path.vertices (def)
{V : Type u_1} → {D : LGV.SimpleDigraph V} → D.Path → List V

Body:
fun V D self => self.1

Docstring: The vertices of the path, in order 

## PROJECT DEPENDENCY LGV.SimpleDigraph.arc (def)
{V : Type u_1} → LGV.SimpleDigraph V → V → V → Prop

Body:
fun V self => self.1

Docstring: The arc relation: `arc u v` means there is an arc from `u` to `v` 

## PROJECT DEPENDENCY LGV.pathWeightSum (def)
{K : Type u_2} →
  [CommRing K] →
    {V : Type u_3} → [DecidableEq V] → {D : LGV.SimpleDigraph V} → D.IsPathFinite → LGV.ArcWeight D K → V → V → K

Body:
fun {K} [CommRing K] {V} [DecidableEq V] {D} hpf w u v => ∑ p ∈ LGV.pathsFromTo D hpf u v, LGV.pathWeight w p

Docstring: The sum of weights of all paths from u to v.
∑_{p : u → v} w(p) 

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

## PROJECT DEPENDENCY LGV.nipatFinset (def)
{V : Type u_3} →
  [inst : DecidableEq V] →
    {D : LGV.SimpleDigraph V} → D.IsPathFinite → {k : ℕ} → (A B : LGV.kVertex V k) → Finset (LGV.PathTuple D k A B)

Body:
fun {V} [DecidableEq V] {D} hpf {k} A B => ⋯.toFinset

Docstring: Convert nipatSet to Finset using the finiteness proof 

## PROJECT DEPENDENCY LGV.pathTupleWeight (def)
{V : Type u_1} →
  {K : Type u_2} → [CommRing K] → {D : LGV.SimpleDigraph V} → {k : ℕ} → LGV.ArcWeight D K → (Fin k → D.Path) → K

Body:
fun {V} {K} [CommRing K] {D} {k} w ps => ∏ i, LGV.pathWeight w (ps i)

Docstring: The weight of a path tuple is the product of weights of its component paths.
w(𝐩) := w(p₁) w(p₂) ⋯ w(pₖ) 

## PROJECT DEPENDENCY LGV.PathTuple.paths (def)
{V : Type u_3} →
  [inst : DecidableEq V] →
    {D : LGV.SimpleDigraph V} → {k : ℕ} → {A B : LGV.kVertex V k} → LGV.PathTuple D k A B → Fin k → D.Path

Body:
fun V [DecidableEq V] D k A B self => self.1

Docstring: The paths in the tuple 

## PROJECT DEPENDENCY LGV.SimpleDigraph.Path.nonempty (theorem)
∀ {V : Type u_1} {D : LGV.SimpleDigraph V} (self : D.Path), self.vertices ≠ []

Docstring: The path is nonempty 

## PROJECT DEPENDENCY LGV.pathsFromTo (def)
{V : Type u_3} → [DecidableEq V] → (D : LGV.SimpleDigraph V) → D.IsPathFinite → V → V → Finset D.Path

Body:
fun {V} [DecidableEq V] D hpf u v => ⋯.toFinset

Docstring: The set of paths from u to v in a path-finite digraph 

## PROJECT DEPENDENCY LGV.pathWeight (def)
{V : Type u_1} → {K : Type u_2} → [CommRing K] → {D : LGV.SimpleDigraph V} → LGV.ArcWeight D K → D.Path → K

Body:
fun {V} {K} [CommRing K] {D} w p => LGV.pathWeightAux w p.vertices ⋯

Docstring: The weight of a path is the product of weights of its arcs.
w(p) := ∏_{a is an arc of p} w(a) 

## PROJECT DEPENDENCY LGV.nipatSet (def)
{V : Type u_3} →
  [inst : DecidableEq V] → {D : LGV.SimpleDigraph V} → {k : ℕ} → (A B : LGV.kVertex V k) → Set (LGV.PathTuple D k A B)

Body:
fun {V} [DecidableEq V] {D} {k} A B => {pt | pt.isNonIntersecting}

Docstring: The set of non-intersecting path tuples from 𝐀 to 𝐁 

## PROJECT DEPENDENCY LGV.nipatSetFinite (def)
∀ {V : Type u_3} [inst : DecidableEq V] {D : LGV.SimpleDigraph V},
  D.IsPathFinite → ∀ {k : ℕ} (A B : LGV.kVertex V k), (LGV.nipatSet A B).Finite

Body:
fun {V} [DecidableEq V] {D} hpf {k} A B =>
  have h_all_finite :=
    let pathSets := fun i => {p | p.start = A i ∧ p.finish = B i};
    have h_each_finite := fun i => hpf (A i) (B i);
    have h_prod_finite := Set.Finite.pi fun i => h_each_finite i;
    let f := fun x =>
      match x with
      | ⟨pt, property⟩ => ⟨pt.paths, fun i x => ⟨pt.starts i, pt.finishes i⟩⟩;
    have hf_inj := fun ⦃h⦄ =>
      match h with
      | ⟨pt1, property⟩ => fun ⦃h⦄ =>
        match h with
        | ⟨pt2, property_1⟩ => fun heq =>
          Eq.mpr (id (Subtype.mk.injEq pt1 property pt2 property_1))
            (LGV.PathTuple.casesOn (motive := fun t => pt1 = t → pt1 = pt2) pt1
              (fun paths starts finishes h =>
                Eq.ndrec (motive := fun pt1 => pt1 ∈ {pt | True} → pt1.paths = pt2.paths → pt1 = pt2)
                  (fun property heq =>
                    LGV.PathTuple.casesOn (motive := fun t =>
                      pt2 = t → { paths := paths, starts := starts, finishes := finishes } = pt2) pt2
                      (fun paths_1 starts_1 finishes_1 h =>
                        Eq.ndrec (motive := fun pt2 =>
                          pt2 ∈ {pt | True} →
                            { paths := paths, starts := starts, finishes := finishes }.paths = pt2.paths →
                              { paths := paths, starts := starts, finishes := finishes } = pt2)
                          (fun property heq =>
                            Eq.mpr (id (LGV.PathTuple.mk.injEq paths starts finishes paths_1 starts_1 finishes_1)) heq)
                          (Eq.symm h) property_1 heq)
                      (Eq.refl pt2))
                  (Eq.symm h) property
                  (Eq.mp
                    (Subtype.mk.injEq pt1.paths
                      (fun i x => ⟨(↑⟨pt1, property⟩).starts i, (↑⟨pt1, property⟩).finishes i⟩) pt2.paths fun i x =>
                      ⟨(↑⟨pt2, property_1⟩).starts i, (↑⟨pt2, property_1⟩).finishes i⟩)
                    heq))
              (Eq.refl pt1));
    have h_pi_finite := h_prod_finite;
    have h_finite := Finite.of_injective f hf_inj;
    Set.finite_coe_iff.mp h_finite;
  Set.Finite.subset h_all_finite fun x x_1 => trivial

Docstring: The set of nipats is finite (follows from path-finiteness) 

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

## PROJECT DEPENDENCY LGV.PathTuple.isNonIntersecting (def)
{V : Type u_3} →
  [inst : DecidableEq V] → {D : LGV.SimpleDigraph V} → {k : ℕ} → {A B : LGV.kVertex V k} → LGV.PathTuple D k A B → Prop

Body:
fun {V} [DecidableEq V] {D} {k} {A B} pt => ∀ (i j : Fin k), i ≠ j → ¬LGV.pathsIntersect (pt.paths i) (pt.paths j)

Docstring: A path tuple is non-intersecting (nipat) if no two paths share a vertex.
Definition def.lgv.path-tups(d) 

## PROJECT DEPENDENCY LGV.PathTuple.starts (theorem)
∀ {V : Type u_3} [inst : DecidableEq V] {D : LGV.SimpleDigraph V} {k : ℕ} {A B : LGV.kVertex V k}
  (self : LGV.PathTuple D k A B) (i : Fin k), (self.paths i).start = A i

Docstring: Each path starts at the corresponding source vertex 

## PROJECT DEPENDENCY LGV.PathTuple.finishes (theorem)
∀ {V : Type u_3} [inst : DecidableEq V] {D : LGV.SimpleDigraph V} {k : ℕ} {A B : LGV.kVertex V k}
  (self : LGV.PathTuple D k A B) (i : Fin k), (self.paths i).finish = B i

Docstring: Each path ends at the corresponding target vertex 

## PROJECT DEPENDENCY LGV.PathTuple.mk (constructor)
{V : Type u_3} →
  [inst : DecidableEq V] →
    {D : LGV.SimpleDigraph V} →
      {k : ℕ} →
        {A B : LGV.kVertex V k} →
          (paths : Fin k → D.Path) →
            (∀ (i : Fin k), (paths i).start = A i) → (∀ (i : Fin k), (paths i).finish = B i) → LGV.PathTuple D k A B

## PROJECT DEPENDENCY LGV.PathTuple.mk.injEq (theorem)
∀ {V : Type u_3} [inst : DecidableEq V] {D : LGV.SimpleDigraph V} {k : ℕ} {A B : LGV.kVertex V k}
  (paths : Fin k → D.Path) (starts : ∀ (i : Fin k), (paths i).start = A i)
  (finishes : ∀ (i : Fin k), (paths i).finish = B i) (paths_1 : Fin k → D.Path)
  (starts_1 : ∀ (i : Fin k), (paths_1 i).start = A i) (finishes_1 : ∀ (i : Fin k), (paths_1 i).finish = B i),
  ({ paths := paths, starts := starts, finishes := finishes } =
      { paths := paths_1, starts := starts_1, finishes := finishes_1 }) =
    (paths = paths_1)

## PROJECT DEPENDENCY LGV.pathsIntersect (def)
{V : Type u_3} → [DecidableEq V] → {D : LGV.SimpleDigraph V} → D.Path → D.Path → Prop

Body:
fun {V} [DecidableEq V] {D} p q => ∃ v ∈ p.vertices, v ∈ q.vertices

Docstring: Two paths have a vertex in common 

## BASE-LIBRARY REF CommRing
Type u → Type u

Docstring: A commutative ring is a ring with commutative multiplication. 

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

## BASE-LIBRARY REF Matrix.det
{n : Type u_2} → [DecidableEq n] → [Fintype n] → {R : Type v} → [CommRing R] → Matrix n n R → R

Docstring: The determinant of a matrix given by the Leibniz formula. 

## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


## BASE-LIBRARY REF instDecidableEqFin
(n : ℕ) → DecidableEq (Fin n)

## BASE-LIBRARY REF Fin.fintype
(n : ℕ) → Fintype (Fin n)

## BASE-LIBRARY REF Finset.sum
{ι : Type u_1} → {M : Type u_3} → [AddCommMonoid M] → Finset ι → (ι → M) → M

Docstring: `∑ x ∈ s, f x` is the sum of `f x` as `x` ranges over the elements
of the finite set `s`.

When the index type is a `Fintype`, the notation `∑ x, f x`, is a shorthand for
`∑ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF Equiv.Perm
Sort u_1 → Sort (max 1 u_1)

Docstring: `Perm α` is the type of bijections from `α` to itself. 

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.toAddCommMonoid
{α : Type u} → [self : NonUnitalNonAssocSemiring α] → AddCommMonoid α

## BASE-LIBRARY REF NonUnitalNonAssocRing.toNonUnitalNonAssocSemiring
{α : Type u} → [self : NonUnitalNonAssocRing α] → NonUnitalNonAssocSemiring α

## BASE-LIBRARY REF NonUnitalNonAssocCommRing.toNonUnitalNonAssocRing
{α : Type u} → [self : NonUnitalNonAssocCommRing α] → NonUnitalNonAssocRing α

## BASE-LIBRARY REF NonUnitalCommRing.toNonUnitalNonAssocCommRing
{α : Type u} → [self : NonUnitalCommRing α] → NonUnitalNonAssocCommRing α

## BASE-LIBRARY REF CommRing.toNonUnitalCommRing
{α : Type u} → [s : CommRing α] → NonUnitalCommRing α

## BASE-LIBRARY REF Finset.univ
{α : Type u_1} → [Fintype α] → Finset α

Docstring: `univ` is the universal finite set of type `Finset α` implied from
the assumption `Fintype α`. 

## BASE-LIBRARY REF Equiv.instFintype
{α : Type u_1} → {β : Type u_2} → [DecidableEq α] → [DecidableEq β] → [Fintype α] → [Fintype β] → Fintype (α ≃ β)

## BASE-LIBRARY REF HSMul.hSMul
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HSMul α β γ] → α → β → γ

Docstring: `a • b` computes the product of `a` and `b`.
The meaning of this notation is type-dependent, but it is intended to be used for left actions. 

Conventions for notations in identifiers:

 * The recommended spelling of `•` in identifiers is `smul`.

## BASE-LIBRARY REF Units
(α : Type u) → [Monoid α] → Type u

Docstring: Units of a `Monoid`, bundled version. Notation: `αˣ`.

An element of a `Monoid` is a unit if it has a two-sided inverse.
This version bundles the inverse element so that it can be computed.
For a predicate see `IsUnit`. 

## BASE-LIBRARY REF Int
Type

Docstring: The integers.

This type is special-cased by the compiler and overridden with an efficient implementation. The
runtime has a special representation for `Int` that stores “small” signed numbers directly, while
larger numbers use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)). A “small number” is an integer that can be encoded with one fewer bits
than the platform's pointer size (i.e. 63 bits on 64-bit architectures and 31 bits on 32-bit
architectures).


## BASE-LIBRARY REF Int.instMonoid
Monoid ℤ

## BASE-LIBRARY REF instHSMul
{α : Type u_1} → {β : Type u_2} → [SMul α β] → HSMul α β β

## BASE-LIBRARY REF Units.instSMul
{M : Type u_3} → {α : Type u_5} → [inst : Monoid M] → [SMul M α] → SMul Mˣ α

## BASE-LIBRARY REF SubNegMonoid.toZSMul
{M : Type u_2} → [SubNegMonoid M] → SMul ℤ M

## BASE-LIBRARY REF AddGroup.toSubNegMonoid
{A : Type u} → [self : AddGroup A] → SubNegMonoid A

## BASE-LIBRARY REF AddGroupWithOne.toAddGroup
{R : Type u} → [self : AddGroupWithOne R] → AddGroup R

## BASE-LIBRARY REF Ring.toAddGroupWithOne
{R : Type u} → [self : Ring R] → AddGroupWithOne R

## BASE-LIBRARY REF CommRing.toRing
{α : Type u} → [self : CommRing α] → Ring α

## BASE-LIBRARY REF DFunLike.coe
{F : Sort u_1} → {α : outParam (Sort u_2)} → {β : outParam (α → Sort u_3)} → [self : DFunLike F α β] → F → (a : α) → β a

Docstring: The coercion from `F` to a function. 

## BASE-LIBRARY REF MonoidHom
(M : Type u_10) → (N : Type u_11) → [MulOne M] → [MulOne N] → Type (max u_10 u_11)

Docstring: `M →* N` is the type of functions `M → N` that preserve the `MulOne` structure.
`MonoidHom` is used for both monoid and group homomorphisms.

When possible, instead of parametrizing results over `(f : M →* N)`,
you should parametrize over `(F : Type*) [MonoidHomClass F M N] (f : F)`.

When you extend this structure, make sure to extend `MonoidHomClass`.


## BASE-LIBRARY REF MulOneClass.toMulOne
{M : Type u} → [self : MulOneClass M] → MulOne M

## BASE-LIBRARY REF Monoid.toMulOneClass
{M : Type u} → [self : Monoid M] → MulOneClass M

## BASE-LIBRARY REF DivInvMonoid.toMonoid
{G : Type u} → [self : DivInvMonoid G] → Monoid G

## BASE-LIBRARY REF Group.toDivInvMonoid
{G : Type u} → [self : Group G] → DivInvMonoid G

## BASE-LIBRARY REF Equiv.Perm.permGroup
{α : Type u_4} → Group (Equiv.Perm α)

## BASE-LIBRARY REF Units.instMulOneClass
{α : Type u} → [inst : Monoid α] → MulOneClass αˣ

Docstring: Units of a monoid have a multiplication and multiplicative identity. 

## BASE-LIBRARY REF MonoidHom.instFunLike
{M : Type u_4} → {N : Type u_5} → [inst : MulOne M] → [inst_1 : MulOne N] → FunLike (M →* N) M N

## BASE-LIBRARY REF Equiv.Perm.sign
{α : Type u} → [DecidableEq α] → [Fintype α] → Equiv.Perm α →* ℤˣ

Docstring: `SignType.sign` of a permutation returns the signature or parity of a permutation, `1` for even
permutations, `-1` for odd permutations. It is the unique surjective group homomorphism from
`Perm α` to the group with two elements. 

## BASE-LIBRARY REF Not
Prop → Prop

Docstring: `Not p`, or `¬p`, is the negation of `p`. It is defined to be `p → False`,
so if your goal is `¬p` you can use `intro h` to turn the goal into
`h : p ⊢ False`, and if you have `hn : ¬p` and `h : p` then `hn h : False`
and `(hn h).elim` will prove anything.
For more information: [Propositional Logic](https://lean-lang.org/theorem_proving_in_lean4/propositions_and_proofs.html#propositional-logic)


Conventions for notations in identifiers:

 * The recommended spelling of `¬` in identifiers is `not`.

## BASE-LIBRARY REF Set.Finite
{α : Type u} → Set α → Prop

Docstring: A set is finite if the corresponding `Subtype` is finite,
i.e., if there exists a natural `n : ℕ` and an equivalence `s ≃ Fin n`. 

## BASE-LIBRARY REF setOf
{α : Type u} → (α → Prop) → Set α

Docstring: Turn a predicate `p : α → Prop` into a set, also written as `{x | p x}` 

## BASE-LIBRARY REF And
Prop → Prop → Prop

Docstring: `And a b`, or `a ∧ b`, is the conjunction of propositions. It can be
constructed and destructed like a pair: if `ha : a` and `hb : b` then
`⟨ha, hb⟩ : a ∧ b`, and if `h : a ∧ b` then `h.left : a` and `h.right : b`.


Conventions for notations in identifiers:

 * The recommended spelling of `∧` in identifiers is `and`.

 * The recommended spelling of `/\` in identifiers is `and` (prefer `∧` over `/\`).

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

## BASE-LIBRARY REF Matrix
Type u → Type u' → Type v → Type (max u u' v)

Docstring: `Matrix m n R` is the type of matrices with entries in `R`, whose rows are indexed by `m`
and whose columns are indexed by `n`. 

## BASE-LIBRARY REF Equiv
Sort u_1 → Sort u_2 → Sort (max (max 1 u_1) u_2)

Docstring: `α ≃ β` is the type of functions from `α → β` with a two-sided inverse. 

## BASE-LIBRARY REF EquivLike.toFunLike
{E : Sort u_1} → {α : Sort u_3} → {β : Sort u_4} → [EquivLike E α β] → FunLike E α β

## BASE-LIBRARY REF Equiv.instEquivLike
{α : Sort u} → {β : Sort v} → EquivLike (α ≃ β) α β

## BASE-LIBRARY REF Matrix.of
{m : Type u_2} → {n : Type u_3} → {α : Type v} → (m → n → α) ≃ Matrix m n α

Docstring: Cast a function into a matrix.

The two sides of the equivalence are definitionally equal types. We want to use an explicit cast
to distinguish the types because `Matrix` has different instances to pi types (such as `Pi.mul`,
which performs elementwise multiplication, vs `Matrix.mul`).

If you are defining a matrix, in terms of its entries, use `of (fun i j ↦ _)`. The
purpose of this approach is to ensure that terms of the form `(fun i j ↦ _) * (fun i j ↦ _)` do not
appear, as the type of `*` can be misleading.


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


## BASE-LIBRARY REF Finset
Type u_4 → Type u_4

Docstring: `Finset α` is the type of finite sets of elements of `α`. It is implemented
as a multiset (a list up to permutation) which has no duplicate elements. 

## BASE-LIBRARY REF Set.Finite.toFinset
{α : Type u} → {s : Set α} → s.Finite → Finset α

Docstring: Using choice, get the `Finset` that represents this `Set`. 

## BASE-LIBRARY REF Finset.prod
{ι : Type u_1} → {M : Type u_3} → [CommMonoid M] → Finset ι → (ι → M) → M

Docstring: `∏ x ∈ s, f x` is the product of `f x` as `x` ranges over the elements of the finite set `s`.

When the index type is a `Fintype`, the notation `∏ x, f x`, is a shorthand for
`∏ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF CommRing.toCommMonoid
{α : Type u} → [self : CommRing α] → CommMonoid α

## BASE-LIBRARY REF Set
Type u → Type u

Docstring: A set is a collection of elements of some type `α`.

Although `Set` is defined as `α → Prop`, this is an implementation detail which should not be
relied on. Instead, `setOf` and membership of a set (`∈`) should be used to convert between sets
and predicates.


## BASE-LIBRARY REF True
Prop

Docstring: `True` is a proposition and has only an introduction rule, `True.intro : True`.
In other words, `True` is simply true, and has a canonical proof, `True.intro`
For more information: [Propositional Logic](https://lean-lang.org/theorem_proving_in_lean4/propositions_and_proofs.html#propositional-logic)


## BASE-LIBRARY REF Set.pi
{ι : Type u_1} → {α : ι → Type u_2} → Set ι → ((i : ι) → Set (α i)) → Set ((i : ι) → α i)

Docstring: Given an index set `ι` and a family of sets `t : Π i, Set (α i)`, `pi s t`
is the set of dependent functions `f : Πa, π a` such that `f i` belongs to `t i`
whenever `i ∈ s`. 

## BASE-LIBRARY REF Set.univ
{α : Type u} → Set α

Docstring: The universal set on a type `α` is the set containing all elements of `α`.

This is conceptually the "same as" `α` (in set theory, it is actually the same), but type theory
makes the distinction that `α` is a type while `Set.univ` is a term of type `Set α`. `Set.univ` can
itself be coerced to a type `↥Set.univ` which is in bijection with (but distinct from) `α`. 

## BASE-LIBRARY REF Set.Finite.pi
∀ {ι : Type u_3} [Finite ι] {κ : ι → Type u_4} {t : (i : ι) → Set (κ i)},
  (∀ (i : ι), (t i).Finite) → (Set.univ.pi t).Finite

Docstring: Finite product of finite sets is finite 

## BASE-LIBRARY REF Finite.of_fintype
∀ (α : Type u_4) [Fintype α], Finite α

Docstring: For efficiency reasons, we want `Finite` instances to have higher
priority than ones coming from `Fintype` instances. 

## BASE-LIBRARY REF Set.Elem
{α : Type u} → Set α → Type u

Docstring: Given the set `s`, `Elem s` is the `Type` of element of `s`.

It is currently an abbreviation so that instance coming from `Subtype` are available.
If you're interested in making it a `def`, as it probably should be,
you'll then need to create additional instances (and possibly prove lemmas about them).
See e.g. `Mathlib/Data/Set/Order.lean`.


## BASE-LIBRARY REF Membership.mem
{α : outParam (Type u)} → {γ : Type v} → [self : Membership α γ] → γ → α → Prop

Docstring: The membership relation `a ∈ s : Prop` where `a : α`, `s : γ`. 

Conventions for notations in identifiers:

 * The recommended spelling of `∈` in identifiers is `mem`.

## BASE-LIBRARY REF Set.instMembership
{α : Type u} → Membership α (Set α)

## BASE-LIBRARY REF Subtype.mk
{α : Sort u} → {p : α → Prop} → (val : α) → p val → Subtype p

## BASE-LIBRARY REF And.intro
∀ {a b : Prop}, a → b → a ∧ b

Docstring: `And.intro : a → b → a ∧ b` is the constructor for the And operation. 

## BASE-LIBRARY REF Function.Injective
{α : Sort u_1} → {β : Sort u_2} → (α → β) → Prop

Docstring: A function `f : α → β` is called injective if `f x = f y` implies `x = y`. 

## BASE-LIBRARY REF Eq.mpr
{α β : Sort u} → α = β → β → α

Docstring: If `h : α = β` is a proof of type equality, then `h.mpr : β → α` is the induced
"cast" operation in the reverse direction, mapping elements of `β` to elements of `α`.

You can prove theorems about the resulting element by induction on `h`, since
`rfl.mpr` is definitionally the identity function.


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


## BASE-LIBRARY REF Subtype.mk.injEq
∀ {α : Sort u} {p : α → Prop} (val : α) (property : p val) (val_1 : α) (property_1 : p val_1),
  (⟨val, property⟩ = ⟨val_1, property_1⟩) = (val = val_1)

## BASE-LIBRARY REF Eq.ndrec
{α : Sort u2} → {a : α} → {motive : α → Sort u1} → motive a → {b : α} → a = b → motive b

Docstring: Non-dependent recursor for the equality type. 

## BASE-LIBRARY REF Eq.symm
∀ {α : Sort u} {a b : α}, a = b → b = a

Docstring: Equality is symmetric: if `a = b` then `b = a`.

Because this is in the `Eq` namespace, if you have a variable `h : a = b`,
`h.symm` can be used as shorthand for `Eq.symm h` as a proof of `b = a`.

For more information: [Equality](https://lean-lang.org/theorem_proving_in_lean4/quantifiers_and_equality.html#equality)


## BASE-LIBRARY REF Eq.refl
∀ {α : Sort u_1} (a : α), a = a

Docstring: `Eq.refl a : a = a` is reflexivity, the unique constructor of the
equality type. See also `rfl`, which is usually used instead. 

## BASE-LIBRARY REF Eq.mp
{α β : Sort u} → α = β → α → β

Docstring: If `h : α = β` is a proof of type equality, then `h.mp : α → β` is the induced
"cast" operation, mapping elements of `α` to elements of `β`.

You can prove theorems about the resulting element by induction on `h`, since
`rfl.mp` is definitionally the identity function.


## BASE-LIBRARY REF Subtype.val
{α : Sort u} → {p : α → Prop} → Subtype p → α

Docstring: The value in the underlying type that satisfies the predicate.


## BASE-LIBRARY REF Finite
Sort u_3 → Prop

Docstring: A type is `Finite` if it is in bijective correspondence to some `Fin n`.

This is similar to `Fintype`, but `Finite` is a proposition rather than data.
A particular benefit to this is that `Finite` instances are definitionally equal to one another
(due to proof irrelevance) rather than being merely propositionally equal,
and, furthermore, `Finite` instances generally avoid the need for `Decidable` instances.
One other notable difference is that `Finite` allows there to be `Finite p` instances
for all `p : Prop`, which is not allowed by `Fintype` due to universe constraints.
An application of this is that `Finite (x ∈ s → β x)` follows from the general instance for pi
types, assuming `[∀ x, Finite (β x)]`.
Implementation note: this is a reason `Finite α` is not defined as `Nonempty (Fintype α)`.

Every `Fintype` instance provides a `Finite` instance via `Finite.of_fintype`.
Conversely, one can noncomputably create a `Fintype` instance from a `Finite` instance
via `Fintype.ofFinite`. In a proof one might write
```lean
  have := Fintype.ofFinite α
```
to obtain such an instance.

Do not write noncomputable `Fintype` instances; instead write `Finite` instances
and use this `Fintype.ofFinite` interface.
The `Fintype` instances should be relied upon to be computable for evaluation purposes.

Theorems should use `Finite` instead of `Fintype`, unless definitions in the theorem statement
require `Fintype`.
Definitions should prefer `Finite` as well, unless it is important that the definitions
are meant to be computable in the reduction or `#eval` sense.


## BASE-LIBRARY REF Finite.of_injective
∀ {α : Sort u_4} {β : Sort u_5} [Finite β] (f : α → β), Function.Injective f → Finite α

## BASE-LIBRARY REF Iff.mp
∀ {a b : Prop}, (a ↔ b) → a → b

Docstring: Modus ponens for if and only if. If `a ↔ b` and `a`, then `b`. 

## BASE-LIBRARY REF Set.finite_coe_iff
∀ {α : Type u} {s : Set α}, Finite ↑s ↔ s.Finite

## BASE-LIBRARY REF Set.Finite.subset
∀ {α : Type u} {s : Set α}, s.Finite → ∀ {t : Set α}, t ⊆ s → t.Finite

## BASE-LIBRARY REF trivial
True

Docstring: `True` is true, and `True.intro` (or more commonly, `trivial`)
is the proof. 

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

## BASE-LIBRARY REF List.cons
{α : Type u} → α → List α → List α

Docstring: The list whose first element is `head`, where `tail` is the rest of the list.
Usually written `head :: tail`.


Conventions for notations in identifiers:

 * The recommended spelling of `::` in identifiers is `cons`.

 * The recommended spelling of `[a]` in identifiers is `singleton`.

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


## BASE-LIBRARY REF List.instMembership
{α : Type u} → Membership α (List α)

## INFORMAL STATEMENT
LGV lemma, digraph weight version

Let $K$ be a commutative ring. 

Let $D$ be a path-finite (but possibly infinite) acyclic digraph. 

For each arc $a$ of $D$, let $w(a) \in K$. For each path $p$ of $D$, define $w(p) := \prod _{a \text{ is an arc of } p} w(a)$. For each path tuple $\mathbf{p} = (p_1, \ldots , p_k)$, define $w(\mathbf{p}) := w(p_1) \cdots w(p_k)$. 

Let $k \in \mathbb {N}$. Let $\mathbf{A} = (A_1, \ldots , A_k)$ and $\mathbf{B} = (B_1, \ldots , B_k)$ be two $k$-tuples of vertices of $D$. Then, 

\[  \det \! \left(\left(\sum _{p : A_i \to B_j} w(p)\right)_{1 \le i \le k,\;  1 \le j \le k}\right) = \sum _{\sigma \in S_k} (-1)^{\sigma } \sum _{\substack {\mathbf{p} \text{ is a nipat} \\ \text{from } \mathbf{A} \text{ to } \sigma (\mathbf{B})}} w(\mathbf{p}).  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-conv.det.matrices
conv.det.matrices

Let $n, m \in \mathbb {N}$. 

\textbf{(a)} If $A$ is an $n \times m$-matrix, then $A_{i,j}$ shall mean the $(i,j)$-th entry of $A$, that is, the entry of $A$ in row $i$ and column $j$. 

\textbf{(b)} If $a_{i,j}$ is an element of $K$ for each $i \in [n]$ and each $j \in [m]$, then 

\[  \left( a_{i,j} \right)_{1 \leq i \leq n,\;  1 \leq j \leq m}  \]

 shall denote the $n \times m$-matrix whose $(i,j)$-th entry is $a_{i,j}$ for all $i \in [n]$ and $j \in [m]$. 

\textbf{(c)} We let $K^{n \times m}$ denote the set of all $n \times m$-matrices with entries in $K$. This is a $K$-module. If $n = m$, this is also a $K$-algebra. 

\textbf{(d)} Let $A \in K^{n \times m}$ be an $n \times m$-matrix. The \emph{transpose} $A^T$ of $A$ is defined to be the $m \times n$-matrix whose entries are given by 

\[  \left( A^T \right)_{i,j} = A_{j,i} \quad \text{for all } i \in [m] \text{ and } j \in [n].  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.alg.commring
def.alg.commring

A \emph{commutative ring} means a set $K$ equipped with three maps

\begin{align*}  \oplus &  :K\times K\rightarrow K,\\ \ominus &  :K\times K\rightarrow K,\\ \odot &  :K\times K\rightarrow K \end{align*}

 and two elements $\mathbf{0}\in K$ and $\mathbf{1}\in K$ satisfying the following axioms: 

\begin{enumerate} \item \emph{Commutativity of addition:} We have $a\oplus b=b\oplus a$ for all $a,b\in K$. 

\item \emph{Associativity of addition:} We have $a\oplus \left( b\oplus c\right) =\left( a\oplus b\right) \oplus c$ for all $a,b,c\in K$. 

\item \emph{Neutrality of zero:} We have $a\oplus \mathbf{0}=\mathbf{0}\oplus a=a$ for all $a\in K$. 

\item \emph{Subtraction undoes addition:} Let $a,b,c\in K$. We have $a\oplus b=c$ if and only if $a=c\ominus b$. 

\item \emph{Commutativity of multiplication:} We have $a\odot b=b\odot a$ for all $a,b\in K$. 

\item \emph{Associativity of multiplication:} We have $a\odot \left( b\odot c\right) =\left( a\odot b\right) \odot c$ for all $a,b,c\in K$. 

\item \emph{Distributivity:} We have

\[  a\odot \left( b\oplus c\right) =\left( a\odot b\right) \oplus \left( a\odot c\right) \  \  \  \  \  \  \  \  \  \  \text{and}\  \  \  \  \  \  \  \  \  \  \left( a\oplus b\right) \odot c=\left( a\odot c\right) \oplus \left( b\odot c\right)  \]

 for all $a,b,c\in K$. 

\item \emph{Neutrality of one:} We have $a\odot \mathbf{1}=\mathbf{1}\odot a=a$ for all $a\in K$. 

\item \emph{Annihilation:} We have $a\odot \mathbf{0}=\mathbf{0}\odot a=\mathbf{0}$ for all $a\in K$. 

\end{enumerate}

The operations $\oplus $, $\ominus $ and $\odot $ are called the \emph{addition}, the \emph{subtraction} and the \emph{multiplication} of the ring $K$. When confusion is unlikely, we will denote these three operations $\oplus $, $\ominus $ and $\odot $ by $+$, $-$ and $\cdot $, respectively, and we will abbreviate $a\odot b=a\cdot b$ by $ab$. 

The elements $\mathbf{0}$ and $\mathbf{1}$ are called the \emph{zero} and the \emph{unity} (or the \emph{one}) of the ring $K$. We will simply call these elements $0$ and $1$ when confusion with the corresponding numbers is unlikely. 

We will use \emph{PEMDAS conventions} for the three operations $\oplus $, $\ominus $ and $\odot $. These imply that the operation $\odot $ has higher precedence than $\oplus $ and $\ominus $, while the operations $\oplus $ and $\ominus $ are left-associative.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.alg.kalg
def.alg.Kalg

A $K$\emph{-algebra} is a set $A$ equipped with four maps

\begin{align*}  \oplus &  :A\times A\rightarrow A,\\ \ominus &  :A\times A\rightarrow A,\\ \odot &  :A\times A\rightarrow A,\\ \rightharpoonup &  :K\times A\rightarrow A \end{align*}

 and two elements $\overrightarrow {0}\in A$ and $\overrightarrow {1}\in A$ satisfying the following properties: 

\begin{enumerate} \item The set $A$, equipped with the maps $\oplus $, $\ominus $ and $\odot $ and the two elements $\overrightarrow {0}$ and $\overrightarrow {1}$, is a (noncommutative) ring. 

\item The set $A$, equipped with the maps $\oplus $, $\ominus $ and $\rightharpoonup $ and the element $\overrightarrow {0}$, is a $K$-module. 

\item We have

\begin{equation}  \lambda \rightharpoonup \left( a\odot b\right) =\left( \lambda \rightharpoonup a\right) \odot b=a\odot \left( \lambda \rightharpoonup b\right) \end{equation}

 for all $\lambda \in K$ and $a,b\in A$. 

\end{enumerate}

(Thus, in a nutshell, a $K$-algebra is a set $A$ that is simultaneously a ring and a $K$-module, with the property that the ring $A$ and the $K$-module $A$ have the same addition, the same subtraction and the same zero, and satisfy the additional compatibility property (\ref{eq.def.alg.Kalg.scaleinv}).)

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.alg.module
def.alg.module

Let $K$ be a commutative ring. 

A $K$\emph{-module} means a set $M$ equipped with three maps 

\begin{align*}  \oplus &  :M\times M\rightarrow M,\\ \ominus &  :M\times M\rightarrow M,\\ \rightharpoonup &  :K\times M\rightarrow M \end{align*}

 (notice that the third map has domain $K\times M$, not $M\times M$) and an element $\overrightarrow {0}\in M$ satisfying the following axioms: 

\begin{enumerate} \item \emph{Commutativity of addition:} We have $a\oplus b=b\oplus a$ for all $a,b\in M$. 

\item \emph{Associativity of addition:} We have $a\oplus \left( b\oplus c\right) =\left( a\oplus b\right) \oplus c$ for all $a,b,c\in M$. 

\item \emph{Neutrality of zero:} We have $a\oplus \overrightarrow {0}=\overrightarrow {0}\oplus a=a$ for all $a\in M$. 

\item \emph{Subtraction undoes addition:} Let $a,b,c\in M$. We have $a\oplus b=c$ if and only if $a=c\ominus b$. 

\item \emph{Associativity of scaling:} We have $u\rightharpoonup \left( v\rightharpoonup a\right) =\left( uv\right) \rightharpoonup a$ for all $u,v\in K$ and $a\in M$. 

\item \emph{Left distributivity:} We have $u\rightharpoonup \left( a\oplus b\right) =\left( u\rightharpoonup a\right) \oplus \left( u\rightharpoonup b\right) $ for all $u\in K$ and $a,b\in M$. 

\item \emph{Right distributivity:} We have $\left( u+v\right) \rightharpoonup a=\left( u\rightharpoonup a\right) \oplus \left( v\rightharpoonup a\right) $ for all $u,v\in K$ and $a\in M$. 

\item \emph{Neutrality of one:} We have $1\rightharpoonup a=a$ for all $a\in M$. 

\item \emph{Left annihilation:} We have $0\rightharpoonup a=\overrightarrow {0}$ for all $a\in M$. 

\item \emph{Right annihilation:} We have $u\rightharpoonup \overrightarrow {0}=\overrightarrow {0}$ for all $u\in K$. 

\end{enumerate}

The operations $\oplus $, $\ominus $ and $\rightharpoonup $ are called the \emph{addition}, the \emph{subtraction} and the \emph{scaling} (or the $K$\emph{-action}) of the $K$-module $M$. When confusion is unlikely, we will denote these three operations $\oplus $, $\ominus $ and $\rightharpoonup $ by $+$, $-$ and $\cdot $, respectively, and we will abbreviate $a\rightharpoonup b=a\cdot b$ by $ab$. 

The element $\overrightarrow {0}$ is called the \emph{zero} (or the \emph{zero vector}) of the $K$-module $M$. We will usually just call it $0$. 

When $M$ is a $K$-module, the elements of $M$ are called \emph{vectors}, while the elements of $K$ are called \emph{scalars}. 

We will use \emph{PEMDAS conventions} for the three operations $\oplus $, $\ominus $ and $\rightharpoonup $, with the operation $\rightharpoonup $ having higher precedence than $\oplus $ and $\ominus $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.alg.ring
def.alg.ring

The notion of a \emph{ring} (also known as a \emph{noncommutative ring}) is defined in the exact same way as we defined the notion of a commutative ring in Definition~ \ref{def.alg.commring}, except that the “Commutativity of multiplication” axiom is removed.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.det.det
def.det.det

Let $n \in \mathbb {N}$. Let $A \in K^{n \times n}$ be an $n \times n$-matrix. The \emph{determinant} $\det A$ of $A$ is defined to be the element 

\[  \sum _{\sigma \in S_n} (-1)^{\sigma } \underbrace{A_{1,\sigma (1)} A_{2,\sigma (2)} \cdots A_{n,\sigma (n)}}_{ = \prod _{i=1}^{n} A_{i,\sigma (i)}}  \]

 of $K$. Here: 

\begin{itemize} \item we let $S_n$ denote the $n$-th symmetric group (i.e., the group of permutations of $[n] = \{ 1, 2, \ldots , n\} $); 

\item we let $(-1)^{\sigma }$ denote the sign of the permutation $\sigma $ (as defined in Definition~ \ref{def.perm.sign}). 

\end{itemize}

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.invs
def.perm.invs

Let $n\in \mathbb {N}$ and $\sigma \in S_{n}$. \medskip 

\textbf{(a)} An \emph{inversion} of $\sigma $ means a pair $\left(i,j\right)$ of elements of $\left[n\right]$ such that $i<j$ and $\sigma \left(i\right) >\sigma \left(j\right)$. \medskip 

\textbf{(b)} The \emph{length} (also known as the \emph{Coxeter length}) of $\sigma $ is the \#  of inversions of $\sigma $. It is called $\ell \left( \sigma \right)$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.perm
def.perm.perm

Let $X$ be a set. 

\textbf{(a)} A \emph{permutation} of $X$ means a bijection from $X$ to $X$. 

\textbf{(b)} It is known that the set of all permutations of $X$ is a group under composition. This group is called the \emph{symmetric group} of $X$, and is denoted by $S_X$. Its neutral element is the identity map $\operatorname {id}_X : X \to X$. Its size is $|X|!$ when $X$ is finite. 

\textbf{(c)} As usual in group theory, we will write $\alpha \beta $ for the composition $\alpha \circ \beta $ when $\alpha , \beta \in S_X$. This is the map that sends each $x \in X$ to $\alpha (\beta (x))$. 

\textbf{(d)} If $\alpha \in S_X$ and $i \in \mathbb {Z}$, then $\alpha ^i$ shall denote the $i$-th power of $\alpha $ in the group $S_X$. Note that $\alpha ^i = \underbrace{\alpha \circ \alpha \circ \cdots \circ \alpha }_{i\text{ times}}$ if $i \ge 0$. Also, $\alpha ^0 = \operatorname {id}_X$. Also, $\alpha ^{-1}$ is the inverse of $\alpha $ in the group $S_X$, that is, the inverse of the map $\alpha $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.sign
def.perm.sign

Let $n \in \mathbb {N}$. The \emph{sign} of a permutation $\sigma \in S_n$ is defined to be the integer $(-1)^{\ell (\sigma )}$. 

It is denoted by $(-1)^{\sigma }$ or $\operatorname {sgn}(\sigma )$ or $\operatorname {sign}(\sigma )$ or $\varepsilon (\sigma )$. It is also known as the \emph{signature} of $\sigma $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.sn-iven
def.perm.Sn-iven

Let $n \in \mathbb {Z}$. Then, $[n]$ shall mean the set $\{ 1, 2, \ldots , n\} $. This is an $n$-element set if $n \ge 0$, and is an empty set if $n \le 0$. 

The symmetric group $S_{[n]}$ (consisting of all permutations of $[n]$) will be denoted $S_n$ and called the $n$\emph{-th symmetric group}. Its size is $n!$ (when $n \ge 0$).

## VERDICT
{
  "verdict": "faithful",
  "justification": "The formal binders match the blueprint: `\u2200 {K} [CommRing K] ... {D : LGV.SimpleDigraph V} (hpf : D.IsPathFinite), D.IsAcyclic \u2192 \u2200 {k} (w : LGV.ArcWeight D K) (A B : LGV.kVertex V k)` corresponds to \u201cLet K be a commutative ring,\u201d \u201cD be a path-finite ... acyclic digraph,\u201d arc weights, arbitrary `k \u2208 \u2115`, and two k-tuples. The conclusion also matches definitionally: `pathWeightMatrix` has entries `pathWeightSum ... (A i) (B j)`, which sums the products of arc weights over paths; `nipatWeightSum ... A (permuteKVertex \u03c3 B) \u03c3` sums `pathTupleWeight` over tuples whose component paths share no vertex; and `permuteKVertex \u03c3 B i = B (\u03c3 i)` is exactly the stated `\u03c3(B)`. Finally, `Equiv.Perm.sign \u03c3 \u2022 ...` realizes the factor `(-1)^\u03c3`, and the outer finite sum ranges over all permutations of `Fin k`, the zero-based encoding of `S_k`. The additional `[DecidableEq V]` is computational/encoding infrastructure needed for path-intersection predicates and finite-set sums, not a mathematically substantive restriction. Although the formal graph type is `SimpleDigraph`, its only explicit simplicity condition excludes loops, and acyclicity already excludes any loop arc under the supplied path and acyclicity definitions, so this does not narrow the acyclic case asserted by the blueprint."
}