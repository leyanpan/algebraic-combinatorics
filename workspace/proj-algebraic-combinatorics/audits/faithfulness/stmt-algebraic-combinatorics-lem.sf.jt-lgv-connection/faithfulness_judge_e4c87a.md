## TARGET SymmetricFunctions.lgv_nipatWeightSum_eq_nipatSum (theorem) — ELABORATED SIGNATURE
∀ {N : ℕ} {R : Type u_1} [inst : CommRing R] (lam mu : Fin N → ℕ) (hlam : ∀ (i j : Fin N), i ≤ j → lam j ≤ lam i)
  (hmu : ∀ (i j : Fin N), i ≤ j → mu j ≤ mu i) (hcontained : ∀ (i : Fin N), mu i ≤ lam i),
  LGV.nipatWeightSum LGV.integerLattice_pathFinite SymmetricFunctions.jacobiTrudiArcWeight
      (SymmetricFunctions.jacobiTrudiSourceVertex mu) (SymmetricFunctions.jacobiTrudiTargetVertex lam)
      (Equiv.refl (Fin N)) =
    ∑ np, np.weight

Docstring: The LGV nipat weight sum equals our Nipat weight sum.

This connects the two representations of non-intersecting path tuples:
- LGV: `PathTuple` with `isNonIntersecting` (no shared vertices)
- Ours: `Nipat` with `colStrictPaths` (column-strictness)

The bijection works as follows:
- An LGV path from (a, 1) to (c, N) is encoded by its east-step heights
- This is exactly our `LatticePath` type
- Non-intersection of LGV paths ↔ column-strictness of east-step heights

The proof uses `pathTupleToNipat` to convert LGV nipats to our Nipat type,
with weight preservation via `pathTupleToNipat_weight`. 

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

## PROJECT DEPENDENCY AlgebraicCombinatorics.SymmetricPolynomials.P_isCommRing' (def)
{K : Type u_1} → [inst : CommRing K] → {N : ℕ} → CommRing (AlgebraicCombinatorics.SymmetricPolynomials.P K N)

Body:
fun {K} [CommRing K] {N} => inferInstance

Docstring: The polynomial ring P K N is a commutative K-algebra.
Label: def.sf.PS 

## PROJECT DEPENDENCY LGV.integerLattice (def)
LGV.SimpleDigraph (ℤ × ℤ)

Body:
{ arc := fun u v => v.1 = u.1 + 1 ∧ v.2 = u.2 ∨ v.1 = u.1 ∧ v.2 = u.2 + 1, arc_irrefl := LGV.integerLattice._proof_1 }

Docstring: The integer lattice digraph ℤ².

This is the same lattice as in LGV1.lean, but using `SimpleDigraph` instead of
Mathlib's `Digraph`. See `integerLattice_arc_iff` for the characterization
and `integerLattice_toDigraph_adj_iff` for the equivalence with LGV1's definition. 

## PROJECT DEPENDENCY LGV.integerLattice_pathFinite (theorem)
LGV.integerLattice.IsPathFinite

Docstring: The integer lattice is path-finite 

## PROJECT DEPENDENCY SymmetricFunctions.jacobiTrudiArcWeight (def)
{N : ℕ} → {R : Type u_1} → [inst : CommRing R] → LGV.ArcWeight LGV.integerLattice (MvPolynomial (Fin N) R)

Body:
fun {N} {R} [CommRing R] u v x =>
  if v.1 = u.1 + 1 ∧ v.2 = u.2 then if h : 1 ≤ u.2 ∧ u.2 ≤ ↑N then MvPolynomial.X ⟨(u.2 - 1).toNat, ⋯⟩ else 1 else 1

Docstring: The arc weight function for the Jacobi-Trudi proof.
East-steps at height j (where 1 ≤ j ≤ N) are weighted by X_{j-1}.
North-steps are weighted by 1.

Note: The lattice uses y-coordinates 1 to N, but Fin N uses 0 to N-1.
An east-step at y-coordinate y gets weight X_{y-1} when 1 ≤ y ≤ N. 

## PROJECT DEPENDENCY SymmetricFunctions.jacobiTrudiSourceVertex (def)
{N : ℕ} → (Fin N → ℕ) → LGV.kVertex (ℤ × ℤ) N

Body:
fun {N} mu i => (SymmetricFunctions.jacobiTrudiSourceX mu i, 1)

Docstring: The source k-vertex for the Jacobi-Trudi LGV setup: A_i = (μ_i - i, 1).
The y-coordinate 1 represents the starting height in the lattice. 

## PROJECT DEPENDENCY SymmetricFunctions.jacobiTrudiTargetVertex (def)
{N : ℕ} → (Fin N → ℕ) → LGV.kVertex (ℤ × ℤ) N

Body:
fun {N} lam j => (SymmetricFunctions.jacobiTrudiTargetX lam j, ↑N)

Docstring: The target k-vertex for the Jacobi-Trudi LGV setup: B_j = (λ_j - j, N).
The y-coordinate N represents the ending height in the lattice. 

## PROJECT DEPENDENCY SymmetricFunctions.Nipat (inductive)
{N : ℕ} →
  (lam mu : Fin N → ℕ) →
    (∀ (i j : Fin N), i ≤ j → lam j ≤ lam i) →
      (∀ (i j : Fin N), i ≤ j → mu j ≤ mu i) → (∀ (i : Fin N), mu i ≤ lam i) → Type

Body:
SymmetricFunctions.Nipat.mk : {N : ℕ} →
  {lam mu : Fin N → ℕ} →
    {hlam : ∀ (i j : Fin N), i ≤ j → lam j ≤ lam i} →
      {hmu : ∀ (i j : Fin N), i ≤ j → mu j ≤ mu i} →
        {hcontained : ∀ (i : Fin N), mu i ≤ lam i} →
          (paths : (i : Fin N) → SymmetricFunctions.LatticePath (↑(mu i) - ↑↑i) (↑(lam i) - ↑↑i)) →
            (∀ (i j : Fin N),
                i < j →
                  ∀ (k : ℕ) (hk : k < (paths i).eastStepHeights.length) (k' : ℕ)
                    (hk' : k' < (paths j).eastStepHeights.length),
                    mu i + k = mu j + k' → (paths i).eastStepHeights[k] < (paths j).eastStepHeights[k']) →
              SymmetricFunctions.Nipat lam mu hlam hmu hcontained

Docstring: A non-intersecting path tuple (nipat) from sources A to targets B.
For Jacobi-Trudi, A_i = (μᵢ - i, 1) and B_i = (λᵢ - i, N). 

## PROJECT DEPENDENCY SymmetricFunctions.Nipat.fintype (def)
{N : ℕ} →
  (lam mu : Fin N → ℕ) →
    (hlam : ∀ (i j : Fin N), i ≤ j → lam j ≤ lam i) →
      (hmu : ∀ (i j : Fin N), i ≤ j → mu j ≤ mu i) →
        (hcontained : ∀ (i : Fin N), mu i ≤ lam i) → Fintype (SymmetricFunctions.Nipat lam mu hlam hmu hcontained)

Body:
fun {N} lam mu hlam hmu hcontained =>
  Fintype.ofEquiv
    (SymmetricFunctions.SkewSSYT
      { outer := { parts := lam, weaklyDecreasing := hlam }, inner := { parts := mu, weaklyDecreasing := hmu },
        contained := ⋯ })
    (SymmetricFunctions.nipatSSYTEquiv lam mu hlam hmu hcontained).symm

Docstring: Fintype instance for Nipat via the equivalence with SkewSSYT. 

## PROJECT DEPENDENCY SymmetricFunctions.Nipat.weight (def)
{N : ℕ} →
  {R : Type u_1} →
    [inst : CommRing R] →
      {lam mu : Fin N → ℕ} →
        {hlam : ∀ (i j : Fin N), i ≤ j → lam j ≤ lam i} →
          {hmu : ∀ (i j : Fin N), i ≤ j → mu j ≤ mu i} →
            {hcontained : ∀ (i : Fin N), mu i ≤ lam i} →
              SymmetricFunctions.Nipat lam mu hlam hmu hcontained → MvPolynomial (Fin N) R

Body:
fun {N} {R} [CommRing R] {lam mu} {hlam} {hmu} {hcontained} np => ∏ i, (np.paths i).weight

Docstring: The weight of a nipat is the product of the weights of its component paths. 

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

## PROJECT DEPENDENCY AlgebraicCombinatorics.SymmetricPolynomials.P (def)
(K : Type u_2) → [CommRing K] → ℕ → Type u_2

Body:
fun K [CommRing K] N => MvPolynomial (Fin N) K

Docstring: The polynomial ring in N variables over K.
This corresponds to 𝒫 in the source (Definition def.sf.PS (a)).
Label: def.sf.PS 

## PROJECT DEPENDENCY LGV.SimpleDigraph.mk (constructor)
{V : Type u_1} → (arc : V → V → Prop) → (∀ (v : V), ¬arc v v) → LGV.SimpleDigraph V

## PROJECT DEPENDENCY LGV.SimpleDigraph.arc (def)
{V : Type u_1} → LGV.SimpleDigraph V → V → V → Prop

Body:
fun V self => self.1

Docstring: The arc relation: `arc u v` means there is an arc from `u` to `v` 

## PROJECT DEPENDENCY SymmetricFunctions.jacobiTrudiSourceX (def)
{N : ℕ} → (Fin N → ℕ) → Fin N → ℤ

Body:
fun {N} mu i => ↑(mu i) - ↑↑i

Docstring: The source vertex A_i = (μ_i - i, 1) for the Jacobi-Trudi LGV setup.
Here 1 represents the "starting height" in the lattice. 

## PROJECT DEPENDENCY SymmetricFunctions.jacobiTrudiTargetX (def)
{N : ℕ} → (Fin N → ℕ) → Fin N → ℤ

Body:
fun {N} lam j => ↑(lam j) - ↑↑j

Docstring: The target vertex B_j = (λ_j - j, N) for the Jacobi-Trudi LGV setup.
Here N represents the "ending height" in the lattice. 

## PROJECT DEPENDENCY SymmetricFunctions.LatticePath (inductive)
{N : ℕ} → ℤ → ℤ → Type

Body:
SymmetricFunctions.LatticePath.mk : {N : ℕ} →
  {a c : ℤ} →
    (eastStepHeights : List (Fin N)) →
      List.IsChain (fun x1 x2 => x1 ≤ x2) eastStepHeights →
        eastStepHeights.length = (c - a).toNat → SymmetricFunctions.LatticePath a c

Docstring: A lattice path in ℤ² from (a, 1) to (c, N) using north and east steps.
This is the type of paths relevant for the Jacobi-Trudi proof. 

## PROJECT DEPENDENCY SymmetricFunctions.LatticePath.eastStepHeights (def)
{N : ℕ} → {a c : ℤ} → SymmetricFunctions.LatticePath a c → List (Fin N)

Body:
fun N a c self => self.1

Docstring: The sequence of heights at which east-steps are taken.
A path from (a, 1) to (c, N) has exactly (c - a) east-steps
(when c ≥ a), and each east-step occurs at some height in [1, N]. 

## PROJECT DEPENDENCY SymmetricFunctions.SkewSSYT (inductive)
{N : ℕ} → SymmetricFunctions.SkewPartition N → Type

Body:
SymmetricFunctions.SkewSSYT.mk : {N : ℕ} →
  {s : SymmetricFunctions.SkewPartition N} →
    (entries : (i : Fin N) → Fin (s.outer.parts i - s.inner.parts i) → Fin N) →
      (∀ (i : Fin N) (j k : Fin (s.outer.parts i - s.inner.parts i)), j ≤ k → entries i j ≤ entries i k) →
        (∀ (i : Fin N) (hi : ↑i + 1 < N) (k : Fin (s.outer.parts i - s.inner.parts i)),
            s.inner.parts i + ↑k + 1 > s.inner.parts ⟨↑i + 1, hi⟩ ∧
                s.inner.parts i + ↑k + 1 ≤ s.outer.parts ⟨↑i + 1, hi⟩ →
              let k' := s.inner.parts i + ↑k - s.inner.parts ⟨↑i + 1, hi⟩;
              ∀ (hk' : k' < s.outer.parts ⟨↑i + 1, hi⟩ - s.inner.parts ⟨↑i + 1, hi⟩),
                entries i k < entries ⟨↑i + 1, hi⟩ ⟨k', hk'⟩) →
          SymmetricFunctions.SkewSSYT s

Docstring: A semistandard Young tableau of skew shape λ/μ with entries in [N].
Definition def.sf.skew-schur.

For a skew tableau, the column-strict condition requires that entries
are strictly increasing down columns, where column j of Y(λ/μ) consists
of boxes (i, j) with μᵢ < j ≤ λᵢ.

**Note:** This is one of two SkewSSYT definitions in this project:
- **This definition** (`SymmetricFunctions.SkewSSYT`): Uses dependent types. Takes
  `s : SkewPartition N` as a single bundled argument. No `[NeZero N]` requirement.
  Field names: `rowWeak`, `colStrict`.
- **Alternative definition** (`SchurBasics.SkewSSYT` in `SchurBasics.lean`): Uses
  `entry : Fin N × ℕ → Fin N` with a support condition. Extends `SkewYoungTableau`.
  Takes `lam mu : NPartition N` as separate arguments. Requires `[NeZero N]`.
  Field names: `row_weak`, `col_strict`.

See `SSYTEquiv.lean` for conversions between representations. 

## PROJECT DEPENDENCY SymmetricFunctions.SkewPartition.mk (constructor)
{N : ℕ} → (outer inner : SymmetricFunctions.NPartition N) → inner ≤ outer → SymmetricFunctions.SkewPartition N

## PROJECT DEPENDENCY SymmetricFunctions.NPartition.mk (constructor)
{N : ℕ} → (parts : Fin N → ℕ) → (∀ (i j : Fin N), i ≤ j → parts j ≤ parts i) → SymmetricFunctions.NPartition N

## PROJECT DEPENDENCY SymmetricFunctions.SkewSSYT.fintype (def)
{N : ℕ} → (s : SymmetricFunctions.SkewPartition N) → Fintype (SymmetricFunctions.SkewSSYT s)

Body:
fun {N} s =>
  let S := { f // SymmetricFunctions.isSSYTFilling s f };
  have e :=
    {
      toFun := fun x =>
        match x with
        | ⟨f, hf⟩ => SymmetricFunctions.fillingToSkewSSYT f hf,
      invFun := fun T => ⟨T.entries, ⋯⟩, left_inv := ⋯, right_inv := ⋯ };
  Fintype.ofEquiv S e

Docstring: Fintype instance for SkewSSYT via the equivalence with valid fillings. 

## PROJECT DEPENDENCY SymmetricFunctions.nipatSSYTEquiv (def)
{N : ℕ} →
  (lam mu : Fin N → ℕ) →
    (hlam : ∀ (i j : Fin N), i ≤ j → lam j ≤ lam i) →
      (hmu : ∀ (i j : Fin N), i ≤ j → mu j ≤ mu i) →
        (hcontained : ∀ (i : Fin N), mu i ≤ lam i) →
          SymmetricFunctions.Nipat lam mu hlam hmu hcontained ≃
            SymmetricFunctions.SkewSSYT
              { outer := { parts := lam, weaklyDecreasing := hlam }, inner := { parts := mu, weaklyDecreasing := hmu },
                contained := ⋯ }

Body:
fun {N} lam mu hlam hmu hcontained =>
  { toFun := SymmetricFunctions.nipatToSSYT, invFun := SymmetricFunctions.ssytToNipat, left_inv := ⋯, right_inv := ⋯ }

Docstring: The equivalence between Nipat and SkewSSYT, established by the bijection functions. 

## PROJECT DEPENDENCY SymmetricFunctions.LatticePath.weight (def)
{N : ℕ} → {R : Type u_1} → [inst : CommRing R] → {a c : ℤ} → SymmetricFunctions.LatticePath a c → MvPolynomial (Fin N) R

Body:
fun {N} {R} [CommRing R] {a c} p => (List.map (fun j => MvPolynomial.X j) p.eastStepHeights).prod

Docstring: The weight of a lattice path is the product of x_j for each east-step at height j.
This corresponds to the weight function w in the source. 

## PROJECT DEPENDENCY SymmetricFunctions.Nipat.paths (def)
{N : ℕ} →
  {lam mu : Fin N → ℕ} →
    {hlam : ∀ (i j : Fin N), i ≤ j → lam j ≤ lam i} →
      {hmu : ∀ (i j : Fin N), i ≤ j → mu j ≤ mu i} →
        {hcontained : ∀ (i : Fin N), mu i ≤ lam i} →
          SymmetricFunctions.Nipat lam mu hlam hmu hcontained →
            (i : Fin N) → SymmetricFunctions.LatticePath (↑(mu i) - ↑↑i) (↑(lam i) - ↑↑i)

Body:
fun N lam mu hlam hmu hcontained self => self.1

Docstring: The tuple of paths, one for each i ∈ [N] 

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

## PROJECT DEPENDENCY LGV.pathWeight (def)
{V : Type u_1} → {K : Type u_2} → [CommRing K] → {D : LGV.SimpleDigraph V} → LGV.ArcWeight D K → D.Path → K

Body:
fun {V} {K} [CommRing K] {D} w p => LGV.pathWeightAux w p.vertices ⋯

Docstring: The weight of a path is the product of weights of its arcs.
w(p) := ∏_{a is an arc of p} w(a) 

## PROJECT DEPENDENCY SymmetricFunctions.SkewPartition (inductive)
ℕ → Type

Body:
SymmetricFunctions.SkewPartition.mk : {N : ℕ} → (outer inner : SymmetricFunctions.NPartition N) → inner ≤ outer → SymmetricFunctions.SkewPartition N

Docstring: A skew partition λ/μ is a pair of N-partitions with μ ⊆ λ.
Definition def.sf.strips(a). 

## PROJECT DEPENDENCY SymmetricFunctions.NPartition.parts (def)
{N : ℕ} → SymmetricFunctions.NPartition N → Fin N → ℕ

Body:
fun N self => self.1

Docstring: The parts of the partition 

## PROJECT DEPENDENCY SymmetricFunctions.SkewPartition.outer (def)
{N : ℕ} → SymmetricFunctions.SkewPartition N → SymmetricFunctions.NPartition N

Body:
fun N self => self.1

Docstring: The outer partition λ 

## PROJECT DEPENDENCY SymmetricFunctions.SkewPartition.inner (def)
{N : ℕ} → SymmetricFunctions.SkewPartition N → SymmetricFunctions.NPartition N

Body:
fun N self => self.2

Docstring: The inner partition μ 

## PROJECT DEPENDENCY SymmetricFunctions.NPartition (inductive)
ℕ → Type

Body:
SymmetricFunctions.NPartition.mk : {N : ℕ} → (parts : Fin N → ℕ) → (∀ (i j : Fin N), i ≤ j → parts j ≤ parts i) → SymmetricFunctions.NPartition N

Docstring: An N-partition is a list of length N with weakly decreasing nonnegative entries.
This corresponds to Definition def.sf.N-par in the source.

**Note:** This is `SymmetricFunctions.NPartition`, a local definition.
A canonical top-level `NPartition` exists in `NPartition.lean` with the same
semantics (using `antitone` as the field name instead of `weaklyDecreasing`).
See the section docstring for details. 

## PROJECT DEPENDENCY SymmetricFunctions.NPartition.instLE (def)
{N : ℕ} → LE (SymmetricFunctions.NPartition N)

Body:
fun {N} => { le := SymmetricFunctions.NPartition.partLE }

## PROJECT DEPENDENCY SymmetricFunctions.SkewFilling (def)
{N : ℕ} → SymmetricFunctions.SkewPartition N → Type

Body:
fun {N} s => (i : Fin N) → Fin (s.outer.parts i - s.inner.parts i) → Fin N

Docstring: A filling of a skew shape is a function assigning a value in Fin N to each cell.
We use `abbrev` instead of `def` to ensure type class inference can see through this. 

## PROJECT DEPENDENCY SymmetricFunctions.isSSYTFilling (def)
{N : ℕ} → (s : SymmetricFunctions.SkewPartition N) → SymmetricFunctions.SkewFilling s → Prop

Body:
fun {N} s f => SymmetricFunctions.isRowWeak s f ∧ SymmetricFunctions.isColStrict s f

Docstring: Combined predicate for SSYT conditions. 

## PROJECT DEPENDENCY SymmetricFunctions.fillingToSkewSSYT (def)
{N : ℕ} →
  {s : SymmetricFunctions.SkewPartition N} →
    (f : SymmetricFunctions.SkewFilling s) → SymmetricFunctions.isSSYTFilling s f → SymmetricFunctions.SkewSSYT s

Body:
fun {N} {s} f hf => { entries := f, rowWeak := ⋯, colStrict := ⋯ }

Docstring: A filling satisfying SSYT conditions can be converted to a SkewSSYT. 

## PROJECT DEPENDENCY SymmetricFunctions.SkewSSYT.entries (def)
{N : ℕ} →
  {s : SymmetricFunctions.SkewPartition N} →
    SymmetricFunctions.SkewSSYT s → (i : Fin N) → Fin (s.outer.parts i - s.inner.parts i) → Fin N

Body:
fun N s self => self.1

Docstring: The entries of the tableau, only for boxes in Y(λ/μ).
Entry (i, k) corresponds to box (i, μᵢ + k + 1) in Y(λ/μ). 

## PROJECT DEPENDENCY SymmetricFunctions.SkewSSYT.toFilling_isSSYTFilling (theorem)
∀ {N : ℕ} {s : SymmetricFunctions.SkewPartition N} (T : SymmetricFunctions.SkewSSYT s),
  SymmetricFunctions.isSSYTFilling s T.toFilling

Docstring: A SkewSSYT's entries form a valid SSYT filling. 

## PROJECT DEPENDENCY SymmetricFunctions.isSSYTFilling_decidable (def)
{N : ℕ} →
  (s : SymmetricFunctions.SkewPartition N) →
    (f : SymmetricFunctions.SkewFilling s) → Decidable (SymmetricFunctions.isSSYTFilling s f)

Body:
fun {N} s f => instDecidableAnd

Docstring: The SSYT predicate is decidable. 

## PROJECT DEPENDENCY SymmetricFunctions.skewFilling_fintype (def)
{N : ℕ} → (s : SymmetricFunctions.SkewPartition N) → Fintype (SymmetricFunctions.SkewFilling s)

Body:
fun {N} s => inferInstance

Docstring: The type of fillings of a skew shape is finite. 

## PROJECT DEPENDENCY SymmetricFunctions.nipatToSSYT (def)
{N : ℕ} →
  {lam mu : Fin N → ℕ} →
    {hlam : ∀ (i j : Fin N), i ≤ j → lam j ≤ lam i} →
      {hmu : ∀ (i j : Fin N), i ≤ j → mu j ≤ mu i} →
        {hcontained : ∀ (i : Fin N), mu i ≤ lam i} →
          SymmetricFunctions.Nipat lam mu hlam hmu hcontained →
            SymmetricFunctions.SkewSSYT
              { outer := { parts := lam, weaklyDecreasing := hlam }, inner := { parts := mu, weaklyDecreasing := hmu },
                contained := ⋯ }

Body:
fun {N} {lam mu} {hlam} {hmu} {hcontained} np =>
  { entries := fun i k => (np.paths i).eastStepHeights.get ⟨↑k, ⋯⟩, rowWeak := ⋯, colStrict := ⋯ }

Docstring: The bijection between nipats and SSYT, sending a nipat to the tableau
whose i-th row contains the heights of east-steps in path i. 

## PROJECT DEPENDENCY SymmetricFunctions.ssytToNipat (def)
{N : ℕ} →
  {lam mu : Fin N → ℕ} →
    {hlam : ∀ (i j : Fin N), i ≤ j → lam j ≤ lam i} →
      {hmu : ∀ (i j : Fin N), i ≤ j → mu j ≤ mu i} →
        {hcontained : ∀ (i : Fin N), mu i ≤ lam i} →
          SymmetricFunctions.SkewSSYT
              { outer := { parts := lam, weaklyDecreasing := hlam }, inner := { parts := mu, weaklyDecreasing := hmu },
                contained := ⋯ } →
            SymmetricFunctions.Nipat lam mu hlam hmu hcontained

Body:
fun {N} {lam mu} {hlam} {hmu} {hcontained} T =>
  { paths := fun i => SymmetricFunctions.mkLatticePathFromEntries (lam i) (mu i) (↑i) (T.entries i) ⋯,
    colStrictPaths := ⋯ }

Docstring: The inverse bijection from SSYT to nipats, sending a tableau to the nipat
whose i-th path has east-steps at the heights given by row i of the tableau. 

## PROJECT DEPENDENCY SymmetricFunctions.ssytToNipat_nipatToSSYT (theorem)
∀ {N : ℕ} {lam mu : Fin N → ℕ} {hlam : ∀ (i j : Fin N), i ≤ j → lam j ≤ lam i}
  {hmu : ∀ (i j : Fin N), i ≤ j → mu j ≤ mu i} {hcontained : ∀ (i : Fin N), mu i ≤ lam i}
  (np : SymmetricFunctions.Nipat lam mu hlam hmu hcontained),
  SymmetricFunctions.ssytToNipat (SymmetricFunctions.nipatToSSYT np) = np

Docstring: ssytToNipat is a left inverse of nipatToSSYT. 

## PROJECT DEPENDENCY SymmetricFunctions.nipatToSSYT_ssytToNipat (theorem)
∀ {N : ℕ} {lam mu : Fin N → ℕ} {hlam : ∀ (i j : Fin N), i ≤ j → lam j ≤ lam i}
  {hmu : ∀ (i j : Fin N), i ≤ j → mu j ≤ mu i} {hcontained : ∀ (i : Fin N), mu i ≤ lam i}
  (T :
    SymmetricFunctions.SkewSSYT
      { outer := { parts := lam, weaklyDecreasing := hlam }, inner := { parts := mu, weaklyDecreasing := hmu },
        contained := ⋯ }),
  SymmetricFunctions.nipatToSSYT (SymmetricFunctions.ssytToNipat T) = T

Docstring: nipatToSSYT is a left inverse of ssytToNipat. 

## PROJECT DEPENDENCY LGV.SimpleDigraph.Path.vertices (def)
{V : Type u_1} → {D : LGV.SimpleDigraph V} → D.Path → List V

Body:
fun V D self => self.1

Docstring: The vertices of the path, in order 

## PROJECT DEPENDENCY LGV.SimpleDigraph.Path.nonempty (theorem)
∀ {V : Type u_1} {D : LGV.SimpleDigraph V} (self : D.Path), self.vertices ≠ []

Docstring: The path is nonempty 

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

## PROJECT DEPENDENCY SymmetricFunctions.NPartition.partLE (def)
{N : ℕ} → SymmetricFunctions.NPartition N → SymmetricFunctions.NPartition N → Prop

Body:
fun {N} mu lam => ∀ (i : Fin N), mu.parts i ≤ lam.parts i

Docstring: Containment of partitions: μ ⊆ λ means μᵢ ≤ λᵢ for all i 

## PROJECT DEPENDENCY SymmetricFunctions.isRowWeak (def)
{N : ℕ} → (s : SymmetricFunctions.SkewPartition N) → SymmetricFunctions.SkewFilling s → Prop

Body:
fun {N} s f => ∀ (i : Fin N) (j k : Fin (s.outer.parts i - s.inner.parts i)), j ≤ k → f i j ≤ f i k

Docstring: Predicate for a filling satisfying the SSYT row-weak condition. 

## PROJECT DEPENDENCY SymmetricFunctions.isColStrict (def)
{N : ℕ} → (s : SymmetricFunctions.SkewPartition N) → SymmetricFunctions.SkewFilling s → Prop

Body:
fun {N} s f =>
  ∀ (i : Fin N) (hi : ↑i + 1 < N) (k : Fin (s.outer.parts i - s.inner.parts i)),
    s.inner.parts i + ↑k + 1 > s.inner.parts ⟨↑i + 1, hi⟩ ∧ s.inner.parts i + ↑k + 1 ≤ s.outer.parts ⟨↑i + 1, hi⟩ →
      have k' := s.inner.parts i + ↑k - s.inner.parts ⟨↑i + 1, hi⟩;
      ∀ (hk' : k' < s.outer.parts ⟨↑i + 1, hi⟩ - s.inner.parts ⟨↑i + 1, hi⟩), f i k < f ⟨↑i + 1, hi⟩ ⟨k', hk'⟩

Docstring: Predicate for a filling satisfying the SSYT column-strict condition.
This is a simplified version that checks the condition for adjacent rows. 

## PROJECT DEPENDENCY SymmetricFunctions.SkewSSYT.mk (constructor)
{N : ℕ} →
  {s : SymmetricFunctions.SkewPartition N} →
    (entries : (i : Fin N) → Fin (s.outer.parts i - s.inner.parts i) → Fin N) →
      (∀ (i : Fin N) (j k : Fin (s.outer.parts i - s.inner.parts i)), j ≤ k → entries i j ≤ entries i k) →
        (∀ (i : Fin N) (hi : ↑i + 1 < N) (k : Fin (s.outer.parts i - s.inner.parts i)),
            s.inner.parts i + ↑k + 1 > s.inner.parts ⟨↑i + 1, hi⟩ ∧
                s.inner.parts i + ↑k + 1 ≤ s.outer.parts ⟨↑i + 1, hi⟩ →
              let k' := s.inner.parts i + ↑k - s.inner.parts ⟨↑i + 1, hi⟩;
              ∀ (hk' : k' < s.outer.parts ⟨↑i + 1, hi⟩ - s.inner.parts ⟨↑i + 1, hi⟩),
                entries i k < entries ⟨↑i + 1, hi⟩ ⟨k', hk'⟩) →
          SymmetricFunctions.SkewSSYT s

## PROJECT DEPENDENCY SymmetricFunctions.SkewSSYT.toFilling (def)
{N : ℕ} → {s : SymmetricFunctions.SkewPartition N} → SymmetricFunctions.SkewSSYT s → SymmetricFunctions.SkewFilling s

Body:
fun {N} {s} T => T.entries

Docstring: Convert a SkewSSYT to a filling. 

## PROJECT DEPENDENCY SymmetricFunctions.isRowWeak_decidable (def)
{N : ℕ} →
  (s : SymmetricFunctions.SkewPartition N) →
    (f : SymmetricFunctions.SkewFilling s) → Decidable (SymmetricFunctions.isRowWeak s f)

Body:
fun {N} s f => Fintype.decidableForallFintype

Docstring: The row-weak predicate is decidable. 

## PROJECT DEPENDENCY SymmetricFunctions.isColStrict_decidable (def)
{N : ℕ} →
  (s : SymmetricFunctions.SkewPartition N) →
    (f : SymmetricFunctions.SkewFilling s) → Decidable (SymmetricFunctions.isColStrict s f)

Body:
fun {N} s f => Fintype.decidableForallFintype

Docstring: The column-strict predicate is decidable. 

## PROJECT DEPENDENCY SymmetricFunctions.Nipat.mk (constructor)
{N : ℕ} →
  {lam mu : Fin N → ℕ} →
    {hlam : ∀ (i j : Fin N), i ≤ j → lam j ≤ lam i} →
      {hmu : ∀ (i j : Fin N), i ≤ j → mu j ≤ mu i} →
        {hcontained : ∀ (i : Fin N), mu i ≤ lam i} →
          (paths : (i : Fin N) → SymmetricFunctions.LatticePath (↑(mu i) - ↑↑i) (↑(lam i) - ↑↑i)) →
            (∀ (i j : Fin N),
                i < j →
                  ∀ (k : ℕ) (hk : k < (paths i).eastStepHeights.length) (k' : ℕ)
                    (hk' : k' < (paths j).eastStepHeights.length),
                    mu i + k = mu j + k' → (paths i).eastStepHeights[k] < (paths j).eastStepHeights[k']) →
              SymmetricFunctions.Nipat lam mu hlam hmu hcontained

## PROJECT DEPENDENCY SymmetricFunctions.mkLatticePathFromEntries (def)
{N : ℕ} →
  (lam mu i : ℕ) →
    (entries : Fin (lam - mu) → Fin N) →
      (∀ (j k : Fin (lam - mu)), j ≤ k → entries j ≤ entries k) → SymmetricFunctions.LatticePath (↑mu - ↑i) (↑lam - ↑i)

Body:
fun {N} lam mu i entries hrowWeak => { eastStepHeights := List.ofFn entries, weaklyIncreasing := ⋯, length_eq := ⋯ }

Docstring: Helper to create a LatticePath from tableau entries for a single row.
Given entries for row i of a tableau, creates the corresponding lattice path
with east-steps at the heights given by the entries. 

## PROJECT DEPENDENCY LGV.pathsIntersect (def)
{V : Type u_3} → [DecidableEq V] → {D : LGV.SimpleDigraph V} → D.Path → D.Path → Prop

Body:
fun {V} [DecidableEq V] {D} p q => ∃ v ∈ p.vertices, v ∈ q.vertices

Docstring: Two paths have a vertex in common 

## PROJECT DEPENDENCY SymmetricFunctions.LatticePath.mk (constructor)
{N : ℕ} →
  {a c : ℤ} →
    (eastStepHeights : List (Fin N)) →
      List.IsChain (fun x1 x2 => x1 ≤ x2) eastStepHeights →
        eastStepHeights.length = (c - a).toNat → SymmetricFunctions.LatticePath a c

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF CommRing
Type u → Type u

Docstring: A commutative ring is a ring with commutative multiplication. 

## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


## BASE-LIBRARY REF LE.le
{α : Type u} → [self : LE α] → α → α → Prop

Docstring: The less-equal relation: `x ≤ y` 

Conventions for notations in identifiers:

 * The recommended spelling of `≤` in identifiers is `le`.

 * The recommended spelling of `<=` in identifiers is `le` (prefer `≤` over `<=`).

## BASE-LIBRARY REF instLEFin
{n : ℕ} → LE (Fin n)

## BASE-LIBRARY REF instLENat
LE ℕ

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

## BASE-LIBRARY REF MvPolynomial
Type u_1 → (R : Type u_2) → [CommSemiring R] → Type (max u_2 u_1)

Docstring: Multivariate polynomial, where `σ` is the index set of the variables and
`R` is the coefficient ring 

## BASE-LIBRARY REF CommRing.toCommSemiring
{α : Type u} → [s : CommRing α] → CommSemiring α

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

## BASE-LIBRARY REF Finset.sum
{ι : Type u_1} → {M : Type u_3} → [AddCommMonoid M] → Finset ι → (ι → M) → M

Docstring: `∑ x ∈ s, f x` is the sum of `f x` as `x` ranges over the elements
of the finite set `s`.

When the index type is a `Fintype`, the notation `∑ x, f x`, is a shorthand for
`∑ x ∈ Finset.univ, f x`. 

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

## BASE-LIBRARY REF DecidableEq
Sort u → Sort (max 1 u)

Docstring: Propositional equality is `Decidable` for all elements of a type.

In other words, an instance of `DecidableEq α` is a means of deciding the proposition `a = b` is
for all `a b : α`.


## BASE-LIBRARY REF Equiv.Perm
Sort u_1 → Sort (max 1 u_1)

Docstring: `Perm α` is the type of bijections from `α` to itself. 

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


## BASE-LIBRARY REF MvPolynomial.instCommRingMvPolynomial
{R : Type u} → {σ : Type u_1} → [inst : CommRing R] → CommRing (MvPolynomial σ R)

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

## BASE-LIBRARY REF ite
{α : Sort u} → (c : Prop) → [h : Decidable c] → α → α → α

Docstring: `if c then t else e` is notation for `ite c t e`, "if-then-else", which decides to
return `t` or `e` depending on whether `c` is true or false. The explicit argument
`c : Prop` does not have any actual computational content, but there is an additional
`[Decidable c]` argument synthesized by typeclass inference which actually
determines how to evaluate `c` to true or false. Write `if h : c then t else e`
instead for a "dependent if-then-else" `dite`, which allows `t`/`e` to use the fact
that `c` is true/false.


## BASE-LIBRARY REF instDecidableAnd
{p q : Prop} → [dp : Decidable p] → [dq : Decidable q] → Decidable (p ∧ q)

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


## BASE-LIBRARY REF Int.instLEInt
LE ℤ

## BASE-LIBRARY REF Nat.cast
{R : Type u} → [NatCast R] → ℕ → R

Docstring: The canonical homomorphism `Nat → R`. In most use cases, the target type will have a (semi)ring
structure, and this homomorphism should be a (semi)ring homomorphism.

`NatCast` and `IntCast` exist to allow different libraries with their own types that can be notated
as natural numbers to have consistent `simp` normal forms without needing to create coercion
simplification sets that are aware of all combinations. Libraries should make it easy to work with
`NatCast` where possible. For instance, in Mathlib there will be such a homomorphism (and thus a
`NatCast R` instance) whenever `R` is an additive monoid with a `1`.

The prototypical example is `Int.ofNat`.


## BASE-LIBRARY REF instNatCastInt
NatCast ℤ

## BASE-LIBRARY REF Int.decLe
(a b : ℤ) → Decidable (a ≤ b)

Docstring: Decides whether `a ≤ b`.

```
#eval ¬ ( (7 : Int) ≤ (0 : Int) ) -- true
#eval (0 : Int) ≤ (0 : Int) -- true
#eval (7 : Int) ≤ (10 : Int) -- true
```

Implemented by efficient native code. 

## BASE-LIBRARY REF MvPolynomial.X
{R : Type u} → {σ : Type u_1} → [inst : CommSemiring R] → σ → MvPolynomial σ R

Docstring: `X n` is the degree `1` monomial $X_n$. 

## BASE-LIBRARY REF Fin.mk
{n : ℕ} → (val : ℕ) → val < n → Fin n

Docstring: Creates a `Fin n` from `i : Nat` and a proof that `i < n`. 

## BASE-LIBRARY REF Int.toNat
ℤ → ℕ

Docstring: Converts an integer into a natural number. Negative numbers are converted to `0`.

Examples:
* `(7 : Int).toNat = 7`
* `(0 : Int).toNat = 0`
* `(-7 : Int).toNat = 0`


## BASE-LIBRARY REF HSub.hSub
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HSub α β γ] → α → β → γ

Docstring: `a - b` computes the difference of `a` and `b`.
The meaning of this notation is type-dependent.
* For natural numbers, this operator saturates at 0: `a - b = 0` when `a ≤ b`. 

Conventions for notations in identifiers:

 * The recommended spelling of `-` in identifiers is `sub` (when used as a binary operator).

## BASE-LIBRARY REF instHSub
{α : Type u_1} → [Sub α] → HSub α α α

## BASE-LIBRARY REF Int.instSub
Sub ℤ

## BASE-LIBRARY REF Not
Prop → Prop

Docstring: `Not p`, or `¬p`, is the negation of `p`. It is defined to be `p → False`,
so if your goal is `¬p` you can use `intro h` to turn the goal into
`h : p ⊢ False`, and if you have `hn : ¬p` and `h : p` then `hn h : False`
and `(hn h).elim` will prove anything.
For more information: [Propositional Logic](https://lean-lang.org/theorem_proving_in_lean4/propositions_and_proofs.html#propositional-logic)


Conventions for notations in identifiers:

 * The recommended spelling of `¬` in identifiers is `not`.

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

## BASE-LIBRARY REF Prod.mk
{α : Type u} → {β : Type v} → α → β → α × β

Docstring: Constructs a pair. This is usually written `(x, y)` instead of `Prod.mk x y`.


Conventions for notations in identifiers:

 * The recommended spelling of `(a, b)` in identifiers is `mk`.

## BASE-LIBRARY REF Fin.val
{n : ℕ} → Fin n → ℕ

Docstring: The number that is strictly less than `n`.

`Fin.val` is a coercion, so any `Fin n` can be used in a position where a `Nat` is expected.


## BASE-LIBRARY REF LT.lt
{α : Type u} → [self : LT α] → α → α → Prop

Docstring: The less-than relation: `x < y` 

Conventions for notations in identifiers:

 * The recommended spelling of `<` in identifiers is `lt`.

## BASE-LIBRARY REF instLTFin
{n : ℕ} → LT (Fin n)

## BASE-LIBRARY REF instLTNat
LT ℕ

## BASE-LIBRARY REF List.length
{α : Type u_1} → List α → ℕ

Docstring: The length of a list.

This function is overridden in the compiler to `lengthTR`, which uses constant stack space.

Examples:
* `([] : List String).length = 0`
* `["green", "brown"].length = 2`


## BASE-LIBRARY REF instAddNat
Add ℕ

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


## BASE-LIBRARY REF List.instGetElemNatLtLength
{α : Type u_1} → GetElem (List α) ℕ α fun as i => i < as.length

## BASE-LIBRARY REF Fintype
Type u_4 → Type u_4

Docstring: `Fintype α` means that `α` is finite, i.e. there are only
finitely many distinct elements of type `α`. The evidence of this
is a finset `elems` (a list up to permutation without duplicates),
together with a proof that everything of type `α` is in the list. 

## BASE-LIBRARY REF Fintype.ofEquiv
{β : Type u_2} → (α : Type u_4) → [Fintype α] → α ≃ β → Fintype β

Docstring: If `f : α ≃ β` and `α` is a fintype, then `β` is also a fintype. 

## BASE-LIBRARY REF Equiv.symm
{α : Sort u} → {β : Sort v} → α ≃ β → β ≃ α

Docstring: Inverse of an equivalence `e : α ≃ β`. 

## BASE-LIBRARY REF Finset.prod
{ι : Type u_1} → {M : Type u_3} → [CommMonoid M] → Finset ι → (ι → M) → M

Docstring: `∏ x ∈ s, f x` is the product of `f x` as `x` ranges over the elements of the finite set `s`.

When the index type is a `Fintype`, the notation `∏ x, f x`, is a shorthand for
`∏ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF CommRing.toCommMonoid
{α : Type u} → [self : CommRing α] → CommMonoid α

## BASE-LIBRARY REF Fin.fintype
(n : ℕ) → Fintype (Fin n)

## BASE-LIBRARY REF Set.Finite
{α : Type u} → Set α → Prop

Docstring: A set is finite if the corresponding `Subtype` is finite,
i.e., if there exists a natural `n : ℕ` and an equivalence `s ≃ Fin n`. 

## BASE-LIBRARY REF setOf
{α : Type u} → (α → Prop) → Set α

Docstring: Turn a predicate `p : α → Prop` into a set, also written as `{x | p x}` 

## BASE-LIBRARY REF Finset
Type u_4 → Type u_4

Docstring: `Finset α` is the type of finite sets of elements of `α`. It is implemented
as a multiset (a list up to permutation) which has no duplicate elements. 

## BASE-LIBRARY REF Set.Finite.toFinset
{α : Type u} → {s : Set α} → s.Finite → Finset α

Docstring: Using choice, get the `Finset` that represents this `Set`. 

## BASE-LIBRARY REF List.IsChain
{α : Type u_1} → (α → α → Prop) → List α → Prop

Docstring: `IsChain R l` means that `R` holds between adjacent elements of `l`. Example:
```
IsChain R [a, b, c, d] ↔ R a b ∧ R b c ∧ R c d
```


## BASE-LIBRARY REF instSubNat
Sub ℕ

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

## BASE-LIBRARY REF GT.gt
{α : Type u} → [LT α] → α → α → Prop

Docstring: `a > b` is an abbreviation for `b < a`. 

Conventions for notations in identifiers:

 * The recommended spelling of `>` in identifiers is `gt`.

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

## BASE-LIBRARY REF Equiv
Sort u_1 → Sort u_2 → Sort (max (max 1 u_1) u_2)

Docstring: `α ≃ β` is the type of functions from `α → β` with a two-sided inverse. 

## BASE-LIBRARY REF Equiv.mk
{α : Sort u_1} →
  {β : Sort u_2} →
    (toFun : α → β) →
      (invFun : β → α) →
        autoParam (Function.LeftInverse invFun toFun) Equiv.left_inv._autoParam →
          autoParam (Function.RightInverse invFun toFun) Equiv.right_inv._autoParam → α ≃ β

## BASE-LIBRARY REF Subtype.mk
{α : Sort u} → {p : α → Prop} → (val : α) → p val → Subtype p

## BASE-LIBRARY REF Subtype.fintype
{α : Type u_1} → (p : α → Prop) → [DecidablePred p] → [Fintype α] → Fintype { x // p x }

## BASE-LIBRARY REF List.prod
{α : Type u_1} → [Mul α] → [One α] → List α → α

Docstring: Computes the product of the elements of a list.

Examples:

[a, b, c].prod = a * (b * (c * 1))
[2, 3, 5].prod = 30


## BASE-LIBRARY REF Distrib.toMul
{R : Type u_1} → [self : Distrib R] → Mul R

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.toDistrib
{α : Type u} → [self : NonUnitalNonAssocSemiring α] → Distrib α

## BASE-LIBRARY REF List.map
{α : Type u_1} → {β : Type u_2} → (α → β) → List α → List β

Docstring: Applies a function to each element of the list, returning the resulting list of values.

`O(|l|)`.

Examples:
* `[a, b, c].map f = [f a, f b, f c]`
* `[].map Nat.succ = []`
* `["one", "two", "three"].map (·.length) = [3, 3, 5]`
* `["one", "two", "three"].map (·.reverse) = ["eno", "owt", "eerht"]`


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

## BASE-LIBRARY REF List.get
{α : Type u} → (as : List α) → Fin as.length → α

Docstring: Returns the element at the provided index, counting from `0`.

In other words, for `i : Fin as.length`, `as.get i` returns the `i`'th element of the list `as`.
Because the index is a `Fin` bounded by the list's length, the index will never be out of bounds.

Examples:
 * `["spring", "summer", "fall", "winter"].get (2 : Fin 4) = "fall"`
 * `["spring", "summer", "fall", "winter"].get (0 : Fin 4) = "spring"`


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

## BASE-LIBRARY REF LE
Type u → Type u

Docstring: `LE α` is the typeclass which supports the notation `x ≤ y` where `x y : α`.

## BASE-LIBRARY REF LE.mk
{α : Type u} → (α → α → Prop) → LE α

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


## BASE-LIBRARY REF Pi.instFintype
{α : Type u_3} →
  {β : α → Type u_4} → [DecidableEq α] → [Fintype α] → [(a : α) → Fintype (β a)] → Fintype ((a : α) → β a)

Docstring: A dependent product of fintypes, indexed by a fintype, is a fintype. 

## BASE-LIBRARY REF instDecidableEqFin
(n : ℕ) → DecidableEq (Fin n)

## BASE-LIBRARY REF List.brecOn
{α : Type u} → {motive : List α → Sort u_1} → (t : List α) → ((t : List α) → List.below t → motive t) → motive t

## BASE-LIBRARY REF List.below
{α : Type u} → {motive : List α → Sort u_1} → List α → Sort (max (u + 1) u_1)

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

## BASE-LIBRARY REF Fintype.decidableForallFintype
{α : Type u_1} → {p : α → Prop} → [DecidablePred p] → [Fintype α] → Decidable (∀ (a : α), p a)

## BASE-LIBRARY REF Nat.decidableForallFin
{n : ℕ} → (P : Fin n → Prop) → [DecidablePred P] → Decidable (∀ (i : Fin n), P i)

## BASE-LIBRARY REF forall_prop_decidable
{p : Prop} → (P : p → Prop) → [Decidable p] → [(h : p) → Decidable (P h)] → Decidable (∀ (h : p), P h)

## BASE-LIBRARY REF Fin.decLe
{n : ℕ} → (a b : Fin n) → Decidable (a ≤ b)

## BASE-LIBRARY REF Nat.decLt
(n m : ℕ) → Decidable (n < m)

Docstring: A decision procedure for strict inequality of natural numbers, usually accessed via the
`DecidableLT Nat` instance.

Examples:
 * `(if 3 < 4 then "yes" else "no") = "yes"`
 * `(if 4 < 4 then "yes" else "no") = "no"`
 * `(if 6 < 4 then "yes" else "no") = "no"`
 * `show 5 < 12 by decide`


## BASE-LIBRARY REF Nat.decLe
(n m : ℕ) → Decidable (n ≤ m)

Docstring: A decision procedure for non-strict inequality of natural numbers, usually accessed via the
`DecidableLE Nat` instance.

Examples:
 * `(if 3 ≤ 4 then "yes" else "no") = "yes"`
 * `(if 6 ≤ 4 then "yes" else "no") = "no"`
 * `show 12 ≤ 12 by decide`
 * `show 5 ≤ 12 by decide`


## BASE-LIBRARY REF Fin.decLt
{n : ℕ} → (a b : Fin n) → Decidable (a < b)

## BASE-LIBRARY REF List.ofFn
{α : Type u_1} → {n : ℕ} → (Fin n → α) → List α

Docstring: Creates a list by applying `f` to each potential index in order, starting at `0`.

Examples:
* `List.ofFn (n := 3) toString = ["0", "1", "2"]`
* `List.ofFn (fun i => #["red", "green", "blue"].get i.val i.isLt) = ["red", "green", "blue"]`


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
lem.sf.jt-lgv-connection

\leanhelper  The LGV non-intersecting path tuple weight sum (using the LGV non-intersection condition) equals the nipat weight sum (using the column-strictness condition): 

\[  \sum _{\mathbf{p} \text{ LGV-nipat}} w(\mathbf{p}) = \sum _{\mathbf{p} \text{ nipat}} w(\mathbf{p}).  \]

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.jt-source-target
def.sf.jt-source-target

\leanhelper  Define two $N$-vertices $\mathbf{A} = (A_1, \ldots , A_N)$ and $\mathbf{B} = (B_1, \ldots , B_N)$ by 

\[  A_i := (\mu _i - i,\;  1) \quad \text{and} \quad B_i := (\lambda _i - i,\;  N) \quad \text{for each } i \in [N].  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.nipat
def.sf.nipat

\leanhelper  A \emph{non-intersecting path tuple} (nipat) from $\mathbf{A} = (A_1, \ldots , A_N)$ to $\mathbf{B} = (B_1, \ldots , B_N)$ is an $N$-tuple of lattice paths $(p_1, \ldots , p_N)$ where $p_i$ goes from $(\mu _i - i, 1)$ to $(\lambda _i - i, N)$, subject to a column-strictness condition: for $i < j$, if east steps $k$ (in path~ $i$) and $k'$ (in path~ $j$) correspond to the same tableau column ($\mu _i + k = \mu _j + k'$), then the height of path~ $i$ at step~ $k$ is strictly less than the height of path~ $j$ at step~ $k'$. 

The \emph{weight} of a nipat is $\prod _{i} w(p_i)$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.npar
def.sf.Npar

An $N$\emph{-partition} will mean a weakly decreasing $N$-tuple of nonnegative integers. In other words, an $N$-partition means an $N$-tuple $\left( \lambda _{1},\lambda _{2},\ldots ,\lambda _{N}\right) \in \mathbb {N}^{N}$ with $\lambda _{1}\geq \lambda _{2}\geq \cdots \geq \lambda _{N}$. 

The \emph{size} (or weight) of an $N$-partition $\lambda = (\lambda _1, \lambda _2, \ldots , \lambda _N)$ is defined to be $|\lambda | := \lambda _1 + \lambda _2 + \cdots + \lambda _N$.

## VERDICT
{
  "verdict": "drift",
  "justification": "The elaborated theorem is restricted by the mathematically substantive binders `hlam : \u2200 ... lam j \u2264 lam i`, `hmu : \u2200 ... mu j \u2264 mu i`, and `hcontained : \u2200 i, mu i \u2264 lam i`. The informal statement merely asserts `\u2211_{p LGV-nipat} w(p) = \u2211_{p nipat} w(p)`, and its definition of `nipat` specifies endpoints and column-strictness but does not require that `lam` and `mu` be weakly decreasing or that `mu_i \u2264 lam_i`. The supplied definition of an `N`-partition explains that term, but the statement never declares `lam` and `mu` to be N-partitions; likewise, no informal definition imposes containment. The restriction enters both the target binders and the dependency `SymmetricFunctions.Nipat`, whose type itself requires `hlam`, `hmu`, and `hcontained`. To be faithful, either the blueprint must explicitly assume that `lam` and `mu` are N-partitions with `mu \u2286 lam`, or `SymmetricFunctions.Nipat` and the theorem must be generalized to arbitrary `lam mu`, representing genuine lattice paths (and hence correctly handling impossible endpoints). The arbitrary `[CommRing R]` is a harmless generalization, not the source of drift."
}