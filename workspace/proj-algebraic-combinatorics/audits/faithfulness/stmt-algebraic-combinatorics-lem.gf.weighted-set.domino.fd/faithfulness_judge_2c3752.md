## TARGET DominoTilingsZ.tiling_decomposition_isomorphism (def) — ELABORATED SIGNATURE
DominoTilingsZ.TilingsHeight2.Isomorphism DominoTilingsZ.FaultfreeTilingsHeight2.tuples

Body:
{
  toEquiv :=
    {
      toFun := fun x =>
        match x with
        | ⟨n, T⟩ => DominoTilingsZ.decomposeTiling n T,
      invFun := fun x =>
        match x with
        | ⟨k, ts⟩ => DominoTilingsZ.composeTilings k ts,
      left_inv := DominoTilingsZ.tiling_decomposition_isomorphism._proof_1,
      right_inv := DominoTilingsZ.tiling_decomposition_isomorphism._proof_2 },
  weight_eq := DominoTilingsZ.tiling_decomposition_isomorphism._proof_3 }

Docstring: Main decomposition isomorphism (Lemma \ref{lem.gf.weighted-set.domino.fd}):

Any domino tiling of a height-2 rectangle can be decomposed **uniquely** into a 
tuple of faultfree tilings of (usually smaller) height-2 rectangles, by cutting 
it along its faults.

This gives an isomorphism of weighted sets:
  D ≅ F⁰ + F¹ + F² + F³ + ...
where D = TilingsHeight2 and F = FaultfreeTilingsHeight2.

The isomorphism preserves weights: the sum of the widths of the faultfree tilings
in the tuple equals the width of the original tiling. 

## PROJECT DEPENDENCY WeightedSet.Isomorphism (inductive)
{α : Type u_2} → {β : Type u_3} → WeightedSet α → WeightedSet β → Type (max u_2 u_3)

Body:
WeightedSet.Isomorphism.mk : {α : Type u_2} →
  {β : Type u_3} →
    {W₁ : WeightedSet α} →
      {W₂ : WeightedSet β} → (toEquiv : α ≃ β) → (∀ (a : α), W₂.weight (toEquiv a) = W₁.weight a) → W₁.Isomorphism W₂

Docstring: An isomorphism between weighted sets is a weight-preserving bijection.
(Definition \ref{def.gf-ws.weighted-sets}(d)) 

## PROJECT DEPENDENCY DominoTilingsZ.Tiling (inductive)
DominoTilingsZ.Shape → Type

Body:
DominoTilingsZ.Tiling.mk : {S : DominoTilingsZ.Shape} →
  (dominos : Set DominoTilingsZ.Domino) →
    dominos.PairwiseDisjoint DominoTilingsZ.Domino.toShape → ⋃ d ∈ dominos, d.toShape = S → DominoTilingsZ.Tiling S

Docstring: A domino tiling of a shape S is a set partition of S into dominos
(Definition \ref{def.domino.shapes-and-tilings}(d)) 

## PROJECT DEPENDENCY DominoTilingsZ.Rectangle (def)
ℕ → ℕ → DominoTilingsZ.Shape

Body:
fun n m => {p | 1 ≤ p.1 ∧ p.1 ≤ ↑n ∧ 1 ≤ p.2 ∧ p.2 ≤ ↑m}

Docstring: The n × m rectangle (Definition \ref{def.domino.shapes-and-tilings}(b)) 

## PROJECT DEPENDENCY DominoTilingsZ.isFaultfree (def)
(n : ℕ) → DominoTilingsZ.Tiling (DominoTilingsZ.Rectangle n 2) → Prop

Body:
fun n T => n > 0 ∧ ∀ (k : ℕ), ¬DominoTilingsZ.hasFault n T k

Docstring: A tiling is faultfree if it is nonempty and has no fault 

## PROJECT DEPENDENCY DominoTilingsZ.TilingsHeight2 (def)
WeightedSet ((n : ℕ) × DominoTilingsZ.Tiling (DominoTilingsZ.Rectangle n 2))

Body:
{
  weight := fun x =>
    match x with
    | ⟨n, snd⟩ => n }

Docstring: Domino tilings of height-2 rectangles, with weight = width of rectangle 

## PROJECT DEPENDENCY WeightedSet.tuples (def)
{α : Type u_2} → WeightedSet α → WeightedSet ((n : ℕ) × (Fin n → α))

Body:
fun {α} W =>
  {
    weight := fun x =>
      match x with
      | ⟨n, f⟩ => ∑ i, W.weight (f i) }

Docstring: The infinite disjoint union W^0 + W^1 + W^2 + ... of all tuples of elements.
This is the "Kleene star" construction on weighted sets.
An element is a pair (k, f) where k ∈ ℕ and f : Fin k → α is a k-tuple.
The weight of (k, f) is the sum of weights of the entries: ∑ᵢ |f(i)|. 

## PROJECT DEPENDENCY DominoTilingsZ.FaultfreeTilingsHeight2 (def)
WeightedSet ((n : ℕ) × { T // DominoTilingsZ.isFaultfree n T })

Body:
{
  weight := fun x =>
    match x with
    | ⟨n, snd⟩ => n }

Docstring: Faultfree tilings of height-2 rectangles 

## PROJECT DEPENDENCY WeightedSet.Isomorphism.mk (constructor)
{α : Type u_2} →
  {β : Type u_3} →
    {W₁ : WeightedSet α} →
      {W₂ : WeightedSet β} → (toEquiv : α ≃ β) → (∀ (a : α), W₂.weight (toEquiv a) = W₁.weight a) → W₁.Isomorphism W₂

## PROJECT DEPENDENCY DominoTilingsZ.decomposeTiling (def)
(n : ℕ) →
  DominoTilingsZ.Tiling (DominoTilingsZ.Rectangle n 2) →
    (k : ℕ) × (Fin k → (m : ℕ) × { T' // DominoTilingsZ.isFaultfree m T' })

Body:
fun n T => DominoTilingsZ.decomposeTiling._unary ⟨n, T⟩

Docstring: The decomposition function: given a tiling of a height-2 rectangle, produce a tuple
of faultfree tilings by cutting along all faults.

For example, a tiling with faults at positions k₁ < k₂ < ... < kₘ decomposes into
m+1 faultfree tilings of widths k₁, k₂-k₁, ..., n-kₘ.

The empty tiling (n=0) decomposes into the empty tuple (k=0). 

Implementation: We recursively find the minimum fault position, cut the tiling there,
and decompose the right part. The left part at a minimum fault is always faultfree.
If no faults exist, the entire tiling is faultfree and returned as a singleton. 

## PROJECT DEPENDENCY DominoTilingsZ.composeTilings (def)
(k : ℕ) →
  (Fin k → (m : ℕ) × { T' // DominoTilingsZ.isFaultfree m T' }) →
    (n : ℕ) × DominoTilingsZ.Tiling (DominoTilingsZ.Rectangle n 2)

Body:
fun k ts =>
  let totalWidth := ∑ i, (ts i).fst;
  ⟨totalWidth, { dominos := DominoTilingsZ.composeTilings_dominos k ts, pairwise_disjoint := ⋯, cover := ⋯ }⟩

Docstring: The composition function: given a tuple of faultfree tilings, concatenate them
horizontally to produce a single tiling.

Each faultfree tiling is shifted by the cumulative width of the previous tilings,
and the union of all shifted dominos forms the composed tiling.

This is the inverse of decomposeTiling. 

## PROJECT DEPENDENCY WeightedSet (inductive)
Type u_2 → Type u_2

Body:
WeightedSet.mk : {α : Type u_2} → (α → ℕ) → WeightedSet α

Docstring: A weighted set is a type equipped with a weight function to ℕ.
(Definition \ref{def.gf-ws.weighted-sets}(a)) 

## PROJECT DEPENDENCY WeightedSet.weight (def)
{α : Type u_2} → WeightedSet α → α → ℕ

Body:
fun α self => self.1

Docstring: The weight function assigning a natural number to each element 

## PROJECT DEPENDENCY DominoTilingsZ.Shape (def)
Type

Body:
Set (ℤ × ℤ)

Docstring: A shape is a subset of ℤ² (Definition \ref{def.domino.shapes-and-tilings}(a)) 

## PROJECT DEPENDENCY DominoTilingsZ.Domino (inductive)
Type

Body:
DominoTilingsZ.Domino.horizontal : ℤ → ℤ → DominoTilingsZ.Domino
DominoTilingsZ.Domino.vertical : ℤ → ℤ → DominoTilingsZ.Domino

Docstring: A domino is either horizontal or vertical (Definition \ref{def.domino.shapes-and-tilings}(c)) 

## PROJECT DEPENDENCY DominoTilingsZ.Domino.toShape (def)
DominoTilingsZ.Domino → DominoTilingsZ.Shape

Body:
fun x =>
  match x with
  | DominoTilingsZ.Domino.horizontal i j => {(i, j), (i + 1, j)}
  | DominoTilingsZ.Domino.vertical i j => {(i, j), (i, j + 1)}

Docstring: The cells covered by a domino 

## PROJECT DEPENDENCY DominoTilingsZ.hasFault (def)
(n : ℕ) → DominoTilingsZ.Tiling (DominoTilingsZ.Rectangle n 2) → ℕ → Prop

Body:
fun n T k =>
  k > 0 ∧
    k < n ∧
      ∀ d ∈ T.dominos,
        match d with
        | DominoTilingsZ.Domino.horizontal i j => i < ↑k ∨ i ≥ ↑k + 1
        | DominoTilingsZ.Domino.vertical i j => True

Docstring: A fault in a domino tiling is a vertical line that no domino straddles 

## PROJECT DEPENDENCY WeightedSet.mk (constructor)
{α : Type u_2} → (α → ℕ) → WeightedSet α

## PROJECT DEPENDENCY DominoTilingsZ.decomposeTiling._unary (def)
(n : ℕ) ×' DominoTilingsZ.Tiling (DominoTilingsZ.Rectangle n 2) →
  (k : ℕ) × (Fin k → (m : ℕ) × { T' // DominoTilingsZ.isFaultfree m T' })

Body:
WellFounded.Nat.fix (fun x => PSigma.casesOn x fun n T => n) fun _x a =>
  PSigma.casesOn (motive := fun _x =>
    ((y : (n : ℕ) ×' DominoTilingsZ.Tiling (DominoTilingsZ.Rectangle n 2)) →
        InvImage (fun x1 x2 => x1 < x2) (fun x => PSigma.casesOn x fun n T => n) y _x →
          (k : ℕ) × (Fin k → (m : ℕ) × { T' // DominoTilingsZ.isFaultfree m T' })) →
      (k : ℕ) × (Fin k → (m : ℕ) × { T' // DominoTilingsZ.isFaultfree m T' }))
    _x
    (fun n T a =>
      (match (motive :=
          (x : ℕ) →
            (x_1 : DominoTilingsZ.Tiling (DominoTilingsZ.Rectangle x 2)) →
              ((y : (n : ℕ) ×' DominoTilingsZ.Tiling (DominoTilingsZ.Rectangle n 2)) →
                  InvImage (fun x1 x2 => x1 < x2) (fun x => PSigma.casesOn x fun n T => n) y ⟨x, x_1⟩ →
                    (k : ℕ) × (Fin k → (m : ℕ) × { T' // DominoTilingsZ.isFaultfree m T' })) →
                (k : ℕ) × (Fin k → (m : ℕ) × { T' // DominoTilingsZ.isFaultfree m T' }))
          n, T with
        | 0, x => fun x => ⟨0, Fin.elim0⟩
        | n.succ, T => fun x =>
          if hne : (DominoTilingsZ.faultPositions (n + 1) T).Nonempty then
            let k := DominoTilingsZ.minFault (n + 1) T hne;
            have hk := ⋯;
            have hk_min := ⋯;
            let left := DominoTilingsZ.restrictTilingLeft (n + 1) T k hk;
            have left_ff := ⋯;
            let right := DominoTilingsZ.restrictTilingRight (n + 1) T k hk;
            have hk_pos := ⋯;
            have hk_lt := ⋯;
            have hdec := ⋯;
            match x ⟨n + 1 - k, right⟩ ⋯ with
            | ⟨m, ts⟩ => ⟨m + 1, fun i => if hi : ↑i = 0 then ⟨k, ⟨left, left_ff⟩⟩ else ts ⟨↑i - 1, ⋯⟩⟩
          else
            have hff := ⋯;
            ⟨1, fun x => ⟨n + 1, ⟨T, hff⟩⟩⟩)
        a)
    a

Docstring: The decomposition function: given a tiling of a height-2 rectangle, produce a tuple
of faultfree tilings by cutting along all faults.

For example, a tiling with faults at positions k₁ < k₂ < ... < kₘ decomposes into
m+1 faultfree tilings of widths k₁, k₂-k₁, ..., n-kₘ.

The empty tiling (n=0) decomposes into the empty tuple (k=0). 

Implementation: We recursively find the minimum fault position, cut the tiling there,
and decompose the right part. The left part at a minimum fault is always faultfree.
If no faults exist, the entire tiling is faultfree and returned as a singleton. 

## PROJECT DEPENDENCY DominoTilingsZ.Tiling.mk (constructor)
{S : DominoTilingsZ.Shape} →
  (dominos : Set DominoTilingsZ.Domino) →
    dominos.PairwiseDisjoint DominoTilingsZ.Domino.toShape → ⋃ d ∈ dominos, d.toShape = S → DominoTilingsZ.Tiling S

## PROJECT DEPENDENCY DominoTilingsZ.composeTilings_dominos (def)
(k : ℕ) → (Fin k → (m : ℕ) × { T' // DominoTilingsZ.isFaultfree m T' }) → Set DominoTilingsZ.Domino

Body:
fun k ts => ⋃ i, DominoTilingsZ.composeTilings_component_dominos k ts i

Docstring: The union of all shifted dominos for composition 

## PROJECT DEPENDENCY DominoTilingsZ.Tiling.dominos (def)
{S : DominoTilingsZ.Shape} → DominoTilingsZ.Tiling S → Set DominoTilingsZ.Domino

Body:
fun S self => self.1

Docstring: The set of dominos in the tiling 

## PROJECT DEPENDENCY DominoTilingsZ.faultPositions (def)
(n : ℕ) → DominoTilingsZ.Tiling (DominoTilingsZ.Rectangle n 2) → Set ℕ

Body:
fun n T => {k | DominoTilingsZ.hasFault n T k}

Docstring: The set of fault positions in a tiling 

## PROJECT DEPENDENCY DominoTilingsZ.faultPositions_nonempty_decidable (def)
(n : ℕ) →
  (T : DominoTilingsZ.Tiling (DominoTilingsZ.Rectangle n 2)) → Decidable (DominoTilingsZ.faultPositions n T).Nonempty

Body:
fun n T =>
  have h := Finset.decidableNonempty;
  ⋯.mp h

Docstring: Decidability instance for faultPositions.Nonempty 

## PROJECT DEPENDENCY DominoTilingsZ.minFault (def)
(n : ℕ) → (T : DominoTilingsZ.Tiling (DominoTilingsZ.Rectangle n 2)) → (DominoTilingsZ.faultPositions n T).Nonempty → ℕ

Body:
fun n T hne => ⋯.toFinset.min' ⋯

Docstring: The minimum fault position in a tiling (when faults exist) 

## PROJECT DEPENDENCY DominoTilingsZ.restrictTilingLeft (def)
(n : ℕ) →
  (T : DominoTilingsZ.Tiling (DominoTilingsZ.Rectangle n 2)) →
    (k : ℕ) → DominoTilingsZ.hasFault n T k → DominoTilingsZ.Tiling (DominoTilingsZ.Rectangle k 2)

Body:
fun n T k hk => { dominos := {d | d ∈ T.dominos ∧ d.inLeftPart k}, pairwise_disjoint := ⋯, cover := ⋯ }

Docstring: Restrict a tiling to the left part at a fault position 

## PROJECT DEPENDENCY DominoTilingsZ.restrictTilingRight (def)
(n : ℕ) →
  (T : DominoTilingsZ.Tiling (DominoTilingsZ.Rectangle n 2)) →
    (k : ℕ) → DominoTilingsZ.hasFault n T k → DominoTilingsZ.Tiling (DominoTilingsZ.Rectangle (n - k) 2)

Body:
fun n T k hk =>
  { dominos := (fun d => d.shiftNeg k) '' {d | d ∈ T.dominos ∧ d.inRightPart k}, pairwise_disjoint := ⋯, cover := ⋯ }

Docstring: Restrict a tiling to the right part at a fault position, shifted to origin 

## PROJECT DEPENDENCY DominoTilingsZ.composeTilings_component_dominos (def)
(k : ℕ) → (Fin k → (m : ℕ) × { T' // DominoTilingsZ.isFaultfree m T' }) → Fin k → Set DominoTilingsZ.Domino

Body:
fun k ts i => (fun d => d.shiftNat (DominoTilingsZ.partialWidthSum k ts i)) '' (↑(ts i).snd).dominos

Docstring: The set of dominos for the i-th component in the composition, shifted appropriately 

## PROJECT DEPENDENCY DominoTilingsZ.faultPositions_finite (theorem)
∀ (n : ℕ) (T : DominoTilingsZ.Tiling (DominoTilingsZ.Rectangle n 2)), (DominoTilingsZ.faultPositions n T).Finite

Docstring: The fault positions form a finite set (bounded by n) 

## PROJECT DEPENDENCY DominoTilingsZ.Domino.inLeftPart (def)
DominoTilingsZ.Domino → ℕ → Prop

Body:
fun d k => ∀ p ∈ d.toShape, p.1 ≤ ↑k

Docstring: A domino is in the left part (all x-coordinates ≤ k) 

## PROJECT DEPENDENCY DominoTilingsZ.Domino.shiftNeg (def)
DominoTilingsZ.Domino → ℕ → DominoTilingsZ.Domino

Body:
fun d offset => d.shift (-↑offset)

Docstring: Shift a domino by a negative offset (for decomposition) 

## PROJECT DEPENDENCY DominoTilingsZ.Domino.inRightPart (def)
DominoTilingsZ.Domino → ℕ → Prop

Body:
fun d k => ∀ p ∈ d.toShape, p.1 ≥ ↑k + 1

Docstring: A domino is in the right part (all x-coordinates ≥ k+1) 

## PROJECT DEPENDENCY DominoTilingsZ.Domino.shiftNat (def)
DominoTilingsZ.Domino → ℕ → DominoTilingsZ.Domino

Body:
fun d offset => d.shift ↑offset

Docstring: Shift a domino by a natural number offset (for composition) 

## PROJECT DEPENDENCY DominoTilingsZ.partialWidthSum (def)
(k : ℕ) → (Fin k → (m : ℕ) × { T' // DominoTilingsZ.isFaultfree m T' }) → Fin k → ℕ

Body:
fun k ts i => ∑ j, (ts ⟨↑j, ⋯⟩).fst

Docstring: The partial sum of widths up to (but not including) index i 

## PROJECT DEPENDENCY DominoTilingsZ.Domino.shift (def)
DominoTilingsZ.Domino → ℤ → DominoTilingsZ.Domino

Body:
fun d offset =>
  match d with
  | DominoTilingsZ.Domino.horizontal i j => DominoTilingsZ.Domino.horizontal (i + offset) j
  | DominoTilingsZ.Domino.vertical i j => DominoTilingsZ.Domino.vertical (i + offset) j

Docstring: Shift a domino horizontally by an offset 

## PROJECT DEPENDENCY DominoTilingsZ.Domino.horizontal (constructor)
ℤ → ℤ → DominoTilingsZ.Domino

## PROJECT DEPENDENCY DominoTilingsZ.Domino.vertical (constructor)
ℤ → ℤ → DominoTilingsZ.Domino

## BASE-LIBRARY REF Sigma
{α : Type u} → (α → Type v) → Type (max u v)

Docstring: Dependent pairs, in which the second element's type depends on the value of the first element. The
type `Sigma β` is typically written `Σ a : α, β a` or `(a : α) × β a`.

Although its values are pairs, `Sigma` is sometimes known as the *dependent sum type*, since it is
the type level version of an indexed summation.


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

## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


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

## BASE-LIBRARY REF Equiv.mk
{α : Sort u_1} →
  {β : Sort u_2} →
    (toFun : α → β) →
      (invFun : β → α) →
        autoParam (Function.LeftInverse invFun toFun) Equiv.left_inv._autoParam →
          autoParam (Function.RightInverse invFun toFun) Equiv.right_inv._autoParam → α ≃ β

## BASE-LIBRARY REF Equiv
Sort u_1 → Sort u_2 → Sort (max (max 1 u_1) u_2)

Docstring: `α ≃ β` is the type of functions from `α → β` with a two-sided inverse. 

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

## BASE-LIBRARY REF DFunLike.coe
{F : Sort u_1} → {α : outParam (Sort u_2)} → {β : outParam (α → Sort u_3)} → [self : DFunLike F α β] → F → (a : α) → β a

Docstring: The coercion from `F` to a function. 

## BASE-LIBRARY REF EquivLike.toFunLike
{E : Sort u_1} → {α : Sort u_3} → {β : Sort u_4} → [EquivLike E α β] → FunLike E α β

## BASE-LIBRARY REF Equiv.instEquivLike
{α : Sort u} → {β : Sort v} → EquivLike (α ≃ β) α β

## BASE-LIBRARY REF Set
Type u → Type u

Docstring: A set is a collection of elements of some type `α`.

Although `Set` is defined as `α → Prop`, this is an implementation detail which should not be
relied on. Instead, `setOf` and membership of a set (`∈`) should be used to convert between sets
and predicates.


## BASE-LIBRARY REF Set.PairwiseDisjoint
{α : Type u_1} → {ι : Type u_4} → [inst : PartialOrder α] → [OrderBot α] → Set ι → (ι → α) → Prop

Docstring: A set is `PairwiseDisjoint` under `f`, if the images of any distinct two elements under `f`
are disjoint.

`s.Pairwise Disjoint` is (definitionally) the same as `s.PairwiseDisjoint id`. We prefer the latter
in order to allow dot notation on `Set.PairwiseDisjoint`, even though the former unfolds more
nicely. 

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


## BASE-LIBRARY REF HeytingAlgebra.toOrderBot
{α : Type u_4} → [self : HeytingAlgebra α] → OrderBot α

## BASE-LIBRARY REF Order.Frame.toHeytingAlgebra
{α : Type u_1} → [self : Order.Frame α] → HeytingAlgebra α

## BASE-LIBRARY REF CompleteDistribLattice.toFrame
{α : Type u_1} → [self : CompleteDistribLattice α] → Order.Frame α

## BASE-LIBRARY REF CompleteBooleanAlgebra.toCompleteDistribLattice
{α : Type u} → [CompleteBooleanAlgebra α] → CompleteDistribLattice α

## BASE-LIBRARY REF Set.iUnion
{α : Type u} → {ι : Sort v} → (ι → Set α) → Set α

Docstring: Indexed union of a family of sets 

## BASE-LIBRARY REF Membership.mem
{α : outParam (Type u)} → {γ : Type v} → [self : Membership α γ] → γ → α → Prop

Docstring: The membership relation `a ∈ s : Prop` where `a : α`, `s : γ`. 

Conventions for notations in identifiers:

 * The recommended spelling of `∈` in identifiers is `mem`.

## BASE-LIBRARY REF Set.instMembership
{α : Type u} → Membership α (Set α)

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

## BASE-LIBRARY REF LE.le
{α : Type u} → [self : LE α] → α → α → Prop

Docstring: The less-equal relation: `x ≤ y` 

Conventions for notations in identifiers:

 * The recommended spelling of `≤` in identifiers is `le`.

 * The recommended spelling of `<=` in identifiers is `le` (prefer `≤` over `<=`).

## BASE-LIBRARY REF Int.instLEInt
LE ℤ

## BASE-LIBRARY REF instOfNat
{n : ℕ} → OfNat ℤ n

## BASE-LIBRARY REF Prod.fst
{α : Type u} → {β : Type v} → α × β → α

Docstring: The first element of a pair. 

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

## BASE-LIBRARY REF Prod.snd
{α : Type u} → {β : Type v} → α × β → β

Docstring: The second element of a pair. 

## BASE-LIBRARY REF GT.gt
{α : Type u} → [LT α] → α → α → Prop

Docstring: `a > b` is an abbreviation for `b < a`. 

Conventions for notations in identifiers:

 * The recommended spelling of `>` in identifiers is `gt`.

## BASE-LIBRARY REF instLTNat
LT ℕ

## BASE-LIBRARY REF Not
Prop → Prop

Docstring: `Not p`, or `¬p`, is the negation of `p`. It is defined to be `p → False`,
so if your goal is `¬p` you can use `intro h` to turn the goal into
`h : p ⊢ False`, and if you have `hn : ¬p` and `h : p` then `hn h : False`
and `(hn h).elim` will prove anything.
For more information: [Propositional Logic](https://lean-lang.org/theorem_proving_in_lean4/propositions_and_proofs.html#propositional-logic)


Conventions for notations in identifiers:

 * The recommended spelling of `¬` in identifiers is `not`.

## BASE-LIBRARY REF Finset.sum
{ι : Type u_1} → {M : Type u_3} → [AddCommMonoid M] → Finset ι → (ι → M) → M

Docstring: `∑ x ∈ s, f x` is the sum of `f x` as `x` ranges over the elements
of the finite set `s`.

When the index type is a `Fintype`, the notation `∑ x, f x`, is a shorthand for
`∑ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF Nat.instAddCommMonoid
AddCommMonoid ℕ

## BASE-LIBRARY REF Finset.univ
{α : Type u_1} → [Fintype α] → Finset α

Docstring: `univ` is the universal finite set of type `Finset α` implied from
the assumption `Fintype α`. 

## BASE-LIBRARY REF Fin.fintype
(n : ℕ) → Fintype (Fin n)

## BASE-LIBRARY REF PSigma.mk
{α : Sort u} → {β : α → Sort v} → (fst : α) → β fst → PSigma β

Docstring: Constructs a fully universe-polymorphic dependent pair. 

## BASE-LIBRARY REF Sigma.fst
{α : Type u} → {β : α → Type v} → Sigma β → α

Docstring: The first component of a dependent pair.


## BASE-LIBRARY REF Sigma.mk
{α : Type u} → {β : α → Type v} → (fst : α) → β fst → Sigma β

Docstring: Constructs a dependent pair.

Using this constructor in a context in which the type is not known usually requires a type
ascription to determine `β`. This is because the desired relationship between the two values can't
generally be determined automatically.


## BASE-LIBRARY REF Insert.insert
{α : outParam (Type u)} → {γ : Type v} → [self : Insert α γ] → α → γ → γ

Docstring: `insert x xs` inserts the element `x` into the collection `xs`. 

## BASE-LIBRARY REF Set.instInsert
{α : Type u} → Insert α (Set α)

## BASE-LIBRARY REF Prod.mk
{α : Type u} → {β : Type v} → α → β → α × β

Docstring: Constructs a pair. This is usually written `(x, y)` instead of `Prod.mk x y`.


Conventions for notations in identifiers:

 * The recommended spelling of `(a, b)` in identifiers is `mk`.

## BASE-LIBRARY REF Singleton.singleton
{α : outParam (Type u)} → {β : Type v} → [self : Singleton α β] → α → β

Docstring: `singleton x` is a collection with the single element `x` (notation: `{x}`). 

Conventions for notations in identifiers:

 * The recommended spelling of `{x}` in identifiers is `singleton`.

## BASE-LIBRARY REF Set.instSingletonSet
{α : Type u} → Singleton α (Set α)

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

## BASE-LIBRARY REF LT.lt
{α : Type u} → [self : LT α] → α → α → Prop

Docstring: The less-than relation: `x < y` 

Conventions for notations in identifiers:

 * The recommended spelling of `<` in identifiers is `lt`.

## BASE-LIBRARY REF Or
Prop → Prop → Prop

Docstring: `Or a b`, or `a ∨ b`, is the disjunction of propositions. There are two
constructors for `Or`, called `Or.inl : a → a ∨ b` and `Or.inr : b → a ∨ b`,
and you can use `match` or `cases` to destruct an `Or` assumption into the
two cases.


Conventions for notations in identifiers:

 * The recommended spelling of `∨` in identifiers is `or`.

 * The recommended spelling of `\/` in identifiers is `or` (prefer `∨` over `\/`).

## BASE-LIBRARY REF Int.instLTInt
LT ℤ

## BASE-LIBRARY REF GE.ge
{α : Type u} → [LE α] → α → α → Prop

Docstring: `a ≥ b` is an abbreviation for `b ≤ a`. 

Conventions for notations in identifiers:

 * The recommended spelling of `≥` in identifiers is `ge`.

 * The recommended spelling of `>=` in identifiers is `ge` (prefer `≥` over `>=`).

## BASE-LIBRARY REF True
Prop

Docstring: `True` is a proposition and has only an introduction rule, `True.intro : True`.
In other words, `True` is simply true, and has a canonical proof, `True.intro`
For more information: [Propositional Logic](https://lean-lang.org/theorem_proving_in_lean4/propositions_and_proofs.html#propositional-logic)


## BASE-LIBRARY REF PSigma
{α : Sort u} → (α → Sort v) → Sort (max (max 1 u) v)

Docstring: Fully universe-polymorphic dependent pairs, in which the second element's type depends on the value
of the first element and both types are allowed to be propositions. The type `PSigma β` is typically
written `Σ' a : α, β a` or `(a : α) ×' β a`.

In practice, this generality leads to universe level constraints that are difficult to solve, so
`PSigma` is rarely used in manually-written code. It is usually only used in automation that
constructs pairs of arbitrary types.

To pair a value with a proof that a predicate holds for it, use `Subtype`. To demonstrate that a
value exists that satisfies a predicate, use `Exists`. A dependent pair with a proposition as its
first component is not typically useful due to proof irrelevance: there's no point in depending on a
specific proof because all proofs are equal anyway.


## BASE-LIBRARY REF WellFounded.Nat.fix
{α : Sort u} →
  {motive : α → Sort v} →
    (h : α → ℕ) →
      ((x : α) → ((y : α) → InvImage (fun x1 x2 => x1 < x2) h y x → motive y) → motive x) → (x : α) → motive x

Docstring: A well-founded fixpoint operator specialized for `Nat`-valued measures. Given a measure `h`, it expects
its higher order function argument `F` to invoke its argument only on values `y` that are smaller
than `x` with regard to `h`.

In contrast to `WellFounded.fix`, this fixpoint operator reduces on closed terms. (More precisely:
when `h x` evaluates to a ground value)



## BASE-LIBRARY REF PSigma.casesOn
{α : Sort u} →
  {β : α → Sort v} →
    {motive : PSigma β → Sort u_1} → (t : PSigma β) → ((fst : α) → (snd : β fst) → motive ⟨fst, snd⟩) → motive t

## BASE-LIBRARY REF InvImage
{α : Sort u} → {β : Sort v} → (β → β → Prop) → (α → β) → α → α → Prop

Docstring: The inverse image of `r : β → β → Prop` by a function `α → β` is the relation
`s : α → α → Prop` defined by `s a b = r (f a) (f b)`.


## BASE-LIBRARY REF Fin.elim0
{α : Sort u} → Fin 0 → α

Docstring: The type `Fin 0` is uninhabited, so it can be used to derive any result whatsoever.

This is similar to `Empty.elim`. It can be thought of as a compiler-checked assertion that a code
path is unreachable, or a logical contradiction from which `False` and thus anything else could be
derived.


## BASE-LIBRARY REF instAddNat
Add ℕ

## BASE-LIBRARY REF Nat.succ
ℕ → ℕ

Docstring: The successor of a natural number `n`.

Using `Nat.succ n` should usually be avoided in favor of `n + 1`, which is the [simp normal
form](https://lean-lang.org/doc/reference/4.28.0/find/?domain=Verso.Genre.Manual.section&name=simp-normal-forms).


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


## BASE-LIBRARY REF Set.Nonempty
{α : Type u} → Set α → Prop

Docstring: The property `s.Nonempty` expresses the fact that the set `s` is not empty. It should be used
in theorem assumptions instead of `∃ x, x ∈ s` or `s ≠ ∅` as it gives access to a nice API thanks
to the dot notation. 

## BASE-LIBRARY REF HSub.hSub
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HSub α β γ] → α → β → γ

Docstring: `a - b` computes the difference of `a` and `b`.
The meaning of this notation is type-dependent.
* For natural numbers, this operator saturates at 0: `a - b = 0` when `a ≤ b`. 

Conventions for notations in identifiers:

 * The recommended spelling of `-` in identifiers is `sub` (when used as a binary operator).

## BASE-LIBRARY REF instHSub
{α : Type u_1} → [Sub α] → HSub α α α

## BASE-LIBRARY REF instSubNat
Sub ℕ

## BASE-LIBRARY REF Fin.val
{n : ℕ} → Fin n → ℕ

Docstring: The number that is strictly less than `n`.

`Fin.val` is a coercion, so any `Fin n` can be used in a position where a `Nat` is expected.


## BASE-LIBRARY REF instDecidableEqNat
DecidableEq ℕ

## BASE-LIBRARY REF Subtype.mk
{α : Sort u} → {p : α → Prop} → (val : α) → p val → Subtype p

## BASE-LIBRARY REF Fin.mk
{n : ℕ} → (val : ℕ) → val < n → Fin n

Docstring: Creates a `Fin n` from `i : Nat` and a proof that `i < n`. 

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


## BASE-LIBRARY REF Finset.Nonempty
{α : Type u_1} → Finset α → Prop

Docstring: The property `s.Nonempty` expresses the fact that the finset `s` is not empty. It should be used
in theorem assumptions instead of `∃ x, x ∈ s` or `s ≠ ∅` as it gives access to a nice API thanks
to the dot notation. 

## BASE-LIBRARY REF Set.Finite.toFinset
{α : Type u} → {s : Set α} → s.Finite → Finset α

Docstring: Using choice, get the `Finset` that represents this `Set`. 

## BASE-LIBRARY REF Finset.decidableNonempty
{α : Type u_1} → {s : Finset α} → Decidable s.Nonempty

## BASE-LIBRARY REF Eq.mp
{α β : Sort u} → α = β → α → β

Docstring: If `h : α = β` is a proof of type equality, then `h.mp : α → β` is the induced
"cast" operation, mapping elements of `α` to elements of `β`.

You can prove theorems about the resulting element by induction on `h`, since
`rfl.mp` is definitionally the identity function.


## BASE-LIBRARY REF Finset.min'
{α : Type u_2} → [LinearOrder α] → (s : Finset α) → s.Nonempty → α

Docstring: Given a nonempty finset `s` in a linear order `α`, then `s.min' H` is its minimum, as an
element of `α`, where `H` is a proof of nonemptiness. Without this assumption, use instead `s.min`,
taking values in `WithTop α`. 

## BASE-LIBRARY REF Nat.instLinearOrder
LinearOrder ℕ

## BASE-LIBRARY REF Set.image
{α : Type u} → {β : Type v} → (α → β) → Set α → Set β

Docstring: The image of `s : Set α` by `f : α → β`, written `f '' s`, is the set of `b : β` such that
`f a = b` for some `a ∈ s`. 

## BASE-LIBRARY REF Subtype.val
{α : Sort u} → {p : α → Prop} → Subtype p → α

Docstring: The value in the underlying type that satisfies the predicate.


## BASE-LIBRARY REF Sigma.snd
{α : Type u} → {β : α → Type v} → (self : Sigma β) → β self.fst

Docstring: The second component of a dependent pair. Its type depends on the first component.


## BASE-LIBRARY REF Set.Finite
{α : Type u} → Set α → Prop

Docstring: A set is finite if the corresponding `Subtype` is finite,
i.e., if there exists a natural `n : ℕ` and an equivalence `s ≃ Fin n`. 

## BASE-LIBRARY REF Neg.neg
{α : Type u} → [self : Neg α] → α → α

Docstring: `-a` computes the negative or opposite of `a`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `-` in identifiers is `neg` (when used as a unary operator).

## BASE-LIBRARY REF Int.instNegInt
Neg ℤ

## INFORMAL STATEMENT
lem.gf.weighted-set.domino.fd

Any domino tiling of a height-$2$ rectangle can be decomposed uniquely into a tuple of faultfree tilings of (usually smaller) height-$2$ rectangles, by cutting it along its faults. (If the original tiling was faultfree, then it decomposes into a $1$-tuple. If the original tiling was empty, then it decomposes into a $0$-tuple.) 

Moreover, the sum of the weights of the faultfree tilings in the tuple is the weight of the original tiling. (In other words, if a tiling $T$ decomposes into the tuple $\left( T_{1},T_{2},\ldots ,T_{k}\right) $, then $\left\vert T\right\vert =\left\vert T_{1}\right\vert +\left\vert T_{2}\right\vert +\cdots +\left\vert T_{k}\right\vert $.) 

In the language of weighted sets, this yields an isomorphism 

\[  D\cong F^{0}+F^{1}+F^{2}+F^{3}+\cdots ,  \]

 and therefore, by the infinite analogue of Proposition~ \ref{prop.gf-ws.djun}, 

\[  \overline{D} =\overline{F^{0}+F^{1}+F^{2}+F^{3}+\cdots }=\overline{F^{0}}+\overline{F^{1}}+\overline{F^{2}}+\overline{F^{3}}+\cdots .  \]

 By Proposition~ \ref{prop.gf-ws.pow}, this equals 

\[  \overline{F}^{0}+\overline{F}^{1}+\overline{F}^{2}+\overline{F}^{3}+\cdots =\frac{1}{1-\overline{F}}.  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-a0000000001
a0000000001

Let $A$ be a weighted set. Then, $A^{k}$ (for $k\in \mathbb {N}$) means the weighted set $\underbrace{A\times A\times \cdots \times A}_{k\text{ times}}$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.domino.shapes-and-tilings
def.domino.shapes-and-tilings

\textbf{(a)} A \emph{shape} means a subset of $\mathbb {Z}^{2}$. 

We draw each $\left( i,j\right) \in \mathbb {Z}^{2}$ as a unit square with center at the point $\left( i,j\right) $ (in Cartesian coordinates); thus, a shape can be drawn as a cluster of squares. \medskip 

\textbf{(b)} For any $n,m\in \mathbb {N}$, the shape $R_{n,m}$ (called the $n\times m$\emph{-rectangle}) is defined to be

\[  \left\{  1,2,\ldots ,n\right\}  \times \left\{  1,2,\ldots ,m\right\}  =\left\{  \left( i,j\right) \in \mathbb {Z}^{2}\  \mid \  1\leq i\leq n\text{ and }1\leq j\leq m\right\}  .  \]

\textbf{(c)} A \emph{domino} means a size-$2$ shape of the form

\begin{align*} &  \left\{  \left( i,j\right) ,\  \left( i+1,j\right) \right\}  \text{ (a ``\emph{horizontal domino}'')}\  \  \  \  \  \  \  \  \  \  \text{or}\\ &  \left\{  \left( i,j\right) ,\  \left( i,j+1\right) \right\}  \text{ (a ``\emph{vertical domino}'')}\end{align*}

 for some $\left( i,j\right) \in \mathbb {Z}^{2}$. \medskip 

\textbf{(d)} A \emph{domino tiling} of a shape $S$ is a set partition of $S$ into dominos (i.e., a set of disjoint dominos whose union is $S$). \medskip 

\textbf{(e)} For any $n,m\in \mathbb {N}$, let $d_{n,m}$ be the \#  of domino tilings of $R_{n,m}$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.coeff
def.fps.coeff

If $n\in \mathbb {N}$, and if $\mathbf{a}=\left( a_{0},a_{1},a_{2},\ldots \right) \in K\left[\left[x\right]\right]$ is an FPS, then we define an element $\left[x^{n}\right]\mathbf{a}\in K$ by 

\[  \left[x^{n}\right]\mathbf{a}:=a_{n}.  \]

 This is called the \emph{coefficient of }$x^{n}$\emph{ in }$\mathbf{a}$, or the $n$\emph{-th coefficient} of $\mathbf{a}$, or the $x^{n}$\emph{-coefficient} of $\mathbf{a}$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.fps
def.fps.fps

A \emph{formal power series} (or, short, \emph{FPS}) in $1$ indeterminate over $K$ means a sequence $\left(a_{0},a_{1},a_{2},\ldots \right) = \left(a_{n}\right)_{n\in \mathbb {N}} \in K^{\mathbb {N}}$ of elements of $K$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.ops
def.fps.ops

\textbf{(a)} The \emph{sum} of two FPSs $\mathbf{a}=\left( a_{0},a_{1},a_{2},\ldots \right)$ and $\mathbf{b}=\left(b_{0},b_{1},b_{2},\ldots \right)$ is defined to be the FPS

\[  \left(a_{0}+b_{0},\  \  a_{1}+b_{1},\  \  a_{2}+b_{2},\  \  \ldots \right).  \]

 It is denoted by $\mathbf{a}+\mathbf{b}$. \medskip 

\textbf{(b)} The \emph{difference} of two FPSs $\mathbf{a}=\left(a_{0},a_{1},a_{2},\ldots \right)$ and $\mathbf{b}=\left(b_{0},b_{1},b_{2},\ldots \right)$ is defined to be the FPS

\[  \left(a_{0}-b_{0},\  \  a_{1}-b_{1},\  \  a_{2}-b_{2},\  \  \ldots \right).  \]

 It is denoted by $\mathbf{a}-\mathbf{b}$. \medskip 

\textbf{(c)} If $\lambda \in K$ and if $\mathbf{a}=\left(a_{0},a_{1},a_{2},\ldots \right)$ is an FPS, then we define an FPS 

\[  \lambda \mathbf{a}:=\left(\lambda a_{0},\lambda a_{1},\lambda a_{2},\ldots \right).  \]

\textbf{(d)} The \emph{product} of two FPSs $\mathbf{a}=\left(a_{0},a_{1},a_{2},\ldots \right)$ and $\mathbf{b}=\left(b_{0},b_{1},b_{2},\ldots \right)$ is defined to be the FPS $\left(c_{0},c_{1},c_{2},\ldots \right)$, where 

\begin{align*}  c_{n} &  =\sum _{i=0}^{n}a_{i}b_{n-i}=\sum _{\substack {\left(i,j\right) \in \mathbb {N}^{2};\\ \begin{bgroup} i+j=n

\end{bgroup}}}a_{i}b_{j}\\ &  =a_{0}b_{n}+a_{1}b_{n-1}+a_{2}b_{n-2}+\cdots +a_{n}b_{0}\  \  \  \  \  \  \  \  \  \  \text{for each }n\in \mathbb {N}. \end{align*}

 This product is denoted by $\mathbf{a}\cdot \mathbf{b}$ or just by $\mathbf{ab}$. \medskip 

\textbf{(e)} For each $a\in K$, we define $\underline{a}$ to be the FPS $\left(a,0,0,0,\ldots \right)$. An FPS of the form $\underline{a}$ for some $a\in K$ (that is, an FPS $\left(a_{0},a_{1},a_{2},\ldots \right)$ satisfying $a_{1}=a_{2}=a_{3}=\cdots =0$) is said to be \emph{constant}. \medskip 

\textbf{(f)} The set of all FPSs (in $1$ indeterminate over $K$) is denoted $K\left[\left[x\right]\right]$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.summable
def.fps.summable

A (possibly infinite) family $\left(\mathbf{a}_{i}\right)_{i\in I}$ of FPSs is said to be \emph{summable} (or \emph{entrywise essentially finite}) if 

\[  \text{for each }n\in \mathbb {N}\text{, all but finitely many }i\in I\text{ satisfy }\left[x^{n}\right]\mathbf{a}_{i}=0.  \]

 In this case, the sum $\sum _{i\in I}\mathbf{a}_{i}$ is defined to be the FPS with 

\[  \left[x^{n}\right]\left(\sum _{i\in I}\mathbf{a}_{i}\right) =\underbrace{\sum _{i\in I}\left[x^{n}\right]\mathbf{a}_{i}}_{\substack {\text{an essentially}\\ \text{finite sum}}} \  \  \  \  \  \  \  \  \  \  \text{for all }n\in \mathbb {N}\text{.}  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.x
def.fps.x

Let $x$ denote the FPS $\left(0,1,0,0,0,\ldots \right)$. In other words, let $x$ denote the FPS with $\left[x^{1}\right]x=1$ and $\left[x^{i}\right]x=0$ for all $i\neq 1$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.gf-ws.djun
def.gf-ws.djun

Let $A$ and $B$ be two weighted sets. Then, the weighted set $A+B$ is defined to be the disjoint union of $A$ and $B$, with the weight function inherited from $A$ and $B$ (meaning that each element of $A$ has the same weight that it had in $A$, and each element of $B$ has the same weight that it had in $B$). Formally speaking, this means that $A+B$ is the set $\left( \left\{  0\right\}  \times A\right) \cup \left( \left\{  1\right\}  \times B\right) $, with the weight function given by 

\begin{equation}  \left\vert \left( 0,a\right) \right\vert =\left\vert a\right\vert \  \  \  \  \  \  \  \  \  \  \text{for each }a\in A \end{equation}

 and

\begin{equation}  \left\vert \left( 1,b\right) \right\vert =\left\vert b\right\vert \  \  \  \  \  \  \  \  \  \  \text{for each }b\in B. \end{equation}

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.gf-ws.prod
def.gf-ws.prod

Let $A$ and $B$ be two weighted sets. Then, the weighted set $A\times B$ is defined to be the Cartesian product of the sets $A$ and $B$ (that is, the set $\left\{  \left( a,b\right) \  \mid \  a\in A\text{ and }b\in B\right\}  $), with the weight function defined as follows: For any $\left( a,b\right) \in A\times B$, we set

\begin{equation}  \left\vert \left( a,b\right) \right\vert =\left\vert a\right\vert +\left\vert b\right\vert . \end{equation}

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.gf-ws.weighted-sets
def.gf-ws.weighted-sets

\textbf{(a)} A \emph{weighted set} is a set $A$ equipped with a function $w:A\rightarrow \mathbb {N}$, which is called the \emph{weight function} of this weighted set. For each $a\in A$, the value $w\left( a\right) $ is denoted $\left\vert a\right\vert $ and is called the \emph{weight} of $a$ (in our weighted set). \medskip 

Usually, instead of explicitly specifying the weight function $w$ as a function, we will simply specify the weight $\left\vert a\right\vert $ for each $a\in A$. The weighted set consisting of the set $A$ and the weight function $w$ will be called $\left( A,w\right) $ or simply $A$ when the weight function $w$ is clear from the context. \medskip 

\textbf{(b)} A weighted set $A$ is said to be \emph{finite-type} if for each $n\in \mathbb {N}$, there are only finitely many $a\in A$ having weight $\left\vert a\right\vert =n$. \medskip 

\textbf{(c)} If $A$ is a finite-type weighted set, then the \emph{weight generating function} of $A$ is defined to be the FPS

\[  \sum _{a\in A}x^{\left\vert a\right\vert }=\sum _{n\in \mathbb {N}}\left( \text{\#  of }a\in A\text{ having weight }n\right) \cdot x^{n}\in \mathbb {Z}\left[ \left[ x\right] \right] .  \]

 This FPS is denoted by $\overline{A}$. \medskip 

\textbf{(d)} An \emph{isomorphism} between two weighted sets $A$ and $B$ means a bijection $\rho :A\rightarrow B$ that preserves the weight (i.e., each $a\in A$ satisfies $\left\vert \rho \left( a\right) \right\vert =\left\vert a\right\vert $). \medskip 

\textbf{(e)} We say that two weighted sets $A$ and $B$ are \emph{isomorphic} (this is written $A\cong B$) if there exists an isomorphism between $A$ and $B$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.infsum.essfin
def.infsum.essfin

\textbf{(a)} A family $\left(a_{i}\right)_{i\in I}\in K^{I}$ of elements of $K$ is said to be \emph{essentially finite} if all but finitely many $i\in I$ satisfy $a_{i}=0$ (in other words, if the set $\left\{ i\in I\  \mid \  a_{i}\neq 0\right\} $ is finite). \medskip 

\textbf{(b)} Let $\left(a_{i}\right)_{i\in I}\in K^{I}$ be an essentially finite family of elements of $K$. Then, the infinite sum $\sum _{i\in I}a_{i}$ is defined to equal the finite sum $\sum _{\substack {i\in I;\\ a_{i}\neq 0}}a_{i}$. Such an infinite sum is said to be \emph{essentially finite}.

## VERDICT
{
  "verdict": "unstatable",
  "justification": "The target faithfully captures only the decomposition-isomorphism portion: `DominoTilingsZ.TilingsHeight2.Isomorphism DominoTilingsZ.FaultfreeTilingsHeight2.tuples`, with `toFun := ... decomposeTiling`, inverse `composeTilings`, and `weight_eq`, expresses a unique weight-preserving bijection with finite tuples, including the 0-tuple and 1-tuple cases implemented by `decomposeTiling._unary`. However, the INFORMAL STATEMENT also asserts the generating-function conclusions `\\overline D = \\overline{F^0+F^1+\\cdots}` and `= 1/(1-\\overline F)`. No project definition in the package provides finite-type weighted sets, weight generating functions, formal power series, infinite sums, or the geometric-series expression, so these clauses cannot be stated using the available formal definitions. To make the complete blueprint statement statable and faithful, the project dependencies would need formal definitions of finite-type and `\\overline A`, the tuple/disjoint-union generating-function theorem, and the geometric-series identity; the target would then need to include those equalities or be accompanied by formal corollaries deriving them. As supplied, it is a faithful formalization of the first part but the complete INFORMAL STATEMENT is unstatable."
}