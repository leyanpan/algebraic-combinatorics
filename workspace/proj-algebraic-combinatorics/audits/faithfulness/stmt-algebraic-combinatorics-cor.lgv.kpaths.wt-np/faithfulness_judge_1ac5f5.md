## TARGET LGV.lgv_nonpermutable (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_2} [inst : CommRing K] {k : ℕ} (w : LGV.ArcWeight LGV.integerLattice K) (A B : LGV.kVertex (ℤ × ℤ) k),
  LGV.xDecreasing A →
    LGV.yIncreasing A →
      LGV.xDecreasing B →
        LGV.yIncreasing B →
          (LGV.pathWeightMatrix LGV.integerLattice_pathFinite w A B).det =
            LGV.nipatWeightSum LGV.integerLattice_pathFinite w A B (Equiv.refl (Fin k))

## PROJECT DEPENDENCY LGV.ArcWeight (def)
{V : Type u_1} → LGV.SimpleDigraph V → Type u_3 → Type (max u_1 u_3)

Body:
fun {V} D K => (u v : V) → D.arc u v → K

Docstring: An arc weight function assigns a ring element to each arc.
Definition in Theorem thm.lgv.kpaths.wt 

## PROJECT DEPENDENCY LGV.integerLattice (def)
LGV.SimpleDigraph (ℤ × ℤ)

Body:
{ arc := fun u v => v.1 = u.1 + 1 ∧ v.2 = u.2 ∨ v.1 = u.1 ∧ v.2 = u.2 + 1, arc_irrefl := LGV.integerLattice._proof_1 }

Docstring: The integer lattice digraph ℤ².

This is the same lattice as in LGV1.lean, but using `SimpleDigraph` instead of
Mathlib's `Digraph`. See `integerLattice_arc_iff` for the characterization
and `integerLattice_toDigraph_adj_iff` for the equivalence with LGV1's definition. 

## PROJECT DEPENDENCY LGV.kVertex (def)
Type u_3 → ℕ → Type u_3

Body:
fun V k => Fin k → V

Docstring: A k-vertex is a k-tuple of vertices of D.
Definition def.lgv.path-tups(a) 

## PROJECT DEPENDENCY LGV.xDecreasing (def)
{k : ℕ} → LGV.kVertex (ℤ × ℤ) k → Prop

Body:
fun {k} A => ∀ (i j : Fin k), i ≤ j → LGV.xCoord (A j) ≤ LGV.xCoord (A i)

Docstring: A k-vertex has weakly decreasing x-coordinates 

## PROJECT DEPENDENCY LGV.yIncreasing (def)
{k : ℕ} → LGV.kVertex (ℤ × ℤ) k → Prop

Body:
fun {k} A => ∀ (i j : Fin k), i ≤ j → LGV.yCoord (A i) ≤ LGV.yCoord (A j)

Docstring: A k-vertex has weakly increasing y-coordinates 

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

## PROJECT DEPENDENCY LGV.integerLattice_pathFinite (theorem)
LGV.integerLattice.IsPathFinite

Docstring: The integer lattice is path-finite 

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

## PROJECT DEPENDENCY LGV.xCoord (def)
ℤ × ℤ → ℤ

Body:
Prod.fst

Docstring: The x-coordinate of a lattice point 

## PROJECT DEPENDENCY LGV.yCoord (def)
ℤ × ℤ → ℤ

Body:
Prod.snd

Docstring: The y-coordinate of a lattice point 

## PROJECT DEPENDENCY LGV.SimpleDigraph.IsPathFinite (def)
{V : Type u_1} → LGV.SimpleDigraph V → Prop

Body:
fun {V} D => ∀ (u v : V), {p | p.start = u ∧ p.finish = v}.Finite

Docstring: A digraph is path-finite if there are only finitely many paths between any two vertices.
Convention conv.lgv.digraph(b) 

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

## PROJECT DEPENDENCY LGV.SimpleDigraph.Path.vertices (def)
{V : Type u_1} → {D : LGV.SimpleDigraph V} → D.Path → List V

Body:
fun V D self => self.1

Docstring: The vertices of the path, in order 

## PROJECT DEPENDENCY LGV.SimpleDigraph.Path.nonempty (theorem)
∀ {V : Type u_1} {D : LGV.SimpleDigraph V} (self : D.Path), self.vertices ≠ []

Docstring: The path is nonempty 

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

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


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

## BASE-LIBRARY REF instDecidableEqProd
{α : Type u_1} → {β : Type u_2} → [DecidableEq α] → [DecidableEq β] → DecidableEq (α × β)

## BASE-LIBRARY REF Int.instDecidableEq
DecidableEq ℤ

Docstring: Decides whether two integers are equal. Usually accessed via the `DecidableEq Int` instance.

This function is overridden by the compiler with an efficient implementation. This definition is the
logical model.

Examples:
* `show (7 : Int) = (3 : Int) + (4 : Int) by decide`
* `if (6 : Int) = (3 : Int) * (2 : Int) then "yes" else "no" = "yes"`
* `(¬ (6 : Int) = (3 : Int)) = true`


## BASE-LIBRARY REF Equiv.refl
(α : Sort u_1) → α ≃ α

Docstring: Any type is equivalent to itself. 

## INFORMAL STATEMENT
LGV lemma, nonpermutable lattice weight version

Consider the setting of Theorem~ \ref{thm.lgv.kpaths.wt}, but additionally assume that 

\begin{align}  \operatorname {x}(A_1) & \ge \operatorname {x}(A_2) \ge \cdots \ge \operatorname {x}(A_k);  \\ \operatorname {y}(A_1) & \le \operatorname {y}(A_2) \le \cdots \le \operatorname {y}(A_k);  \\ \operatorname {x}(B_1) & \ge \operatorname {x}(B_2) \ge \cdots \ge \operatorname {x}(B_k);  \\ \operatorname {y}(B_1) & \le \operatorname {y}(B_2) \le \cdots \le \operatorname {y}(B_k).  \end{align}

 Here, $\operatorname {x}(P)$ and $\operatorname {y}(P)$ denote the two coordinates of any point $P \in \mathbb {Z}^2$. 

Then, there are no nipats from $\mathbf{A}$ to $\sigma (\mathbf{B})$ when $\sigma \in S_k$ is not the identity permutation $\operatorname {id} \in S_k$. Therefore, the claim of Theorem~ \ref{thm.lgv.kpaths.wt} simplifies to 

\begin{equation}  \det \! \left(\left(\sum _{p : A_i \to B_j} w(p)\right)_{1 \le i \le k,\;  1 \le j \le k}\right) = \sum _{\substack {\mathbf{p} \text{ is a nipat} \\ \text{from } \mathbf{A} \text{ to } \mathbf{B}}} w(\mathbf{p}).  \end{equation}

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.jt-arc-weight
def.sf.jt-arc-weight

\leanhelper  The arc weight function for the Jacobi–Trudi proof on the integer lattice $\mathbb {Z}^2$: east-steps at height $y$ (with $1 \leq y \leq N$) are weighted by $x_{y-1}$; north-steps are weighted by $1$.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The target quantifies over an arbitrary commutative ring and arc weighting and assumes exactly the four coordinate conditions: `LGV.xDecreasing A`, `LGV.yIncreasing A`, `LGV.xDecreasing B`, and `LGV.yIncreasing B`. By their bodies, these are precisely the weak chains `x(A\u2081) \u2265 \u22ef \u2265 x(A\u2096)`, `y(A\u2081) \u2264 \u22ef \u2264 y(A\u2096)` and the corresponding chains for `B`. The graph `LGV.integerLattice` has exactly the east and north arcs of the blueprint. The conclusion identifies `det (pathWeightMatrix ... w A B)`, whose entries are `\u2211 p : A\u1d62 \u2192 B\u2c7c, w(p)`, with `nipatWeightSum ... w A B (Equiv.refl (Fin k))`; despite its permutation parameter, that definition sums exactly the weights of non-intersecting path tuples from `A` to `B`, matching the displayed equation. The prose assertion that nonidentity permutations admit no nipats is not a separate conjunct in the target, but it follows from the same four ordering hypotheses in this northeast lattice: any nonidentity permutation has an inversion, and the corresponding two monotone lattice paths have oppositely ordered endpoints and must intersect. Thus omitting that intermediate consequence does not weaken the mathematical statement. The `[CommRing K]` binder is the algebraic setting needed for the determinant and weighted sums, not an additional contentful restriction."
}