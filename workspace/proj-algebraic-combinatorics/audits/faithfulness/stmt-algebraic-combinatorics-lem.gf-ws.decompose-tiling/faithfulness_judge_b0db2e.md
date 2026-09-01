## TARGET DominoTilingsZ.decomposeTiling (def) — ELABORATED SIGNATURE
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

## PROJECT DEPENDENCY DominoTilingsZ.Tiling.dominos (def)
{S : DominoTilingsZ.Shape} → DominoTilingsZ.Tiling S → Set DominoTilingsZ.Domino

Body:
fun S self => self.1

Docstring: The set of dominos in the tiling 

## PROJECT DEPENDENCY DominoTilingsZ.faultPositions_finite (theorem)
∀ (n : ℕ) (T : DominoTilingsZ.Tiling (DominoTilingsZ.Rectangle n 2)), (DominoTilingsZ.faultPositions n T).Finite

Docstring: The fault positions form a finite set (bounded by n) 

## PROJECT DEPENDENCY DominoTilingsZ.Tiling.mk (constructor)
{S : DominoTilingsZ.Shape} →
  (dominos : Set DominoTilingsZ.Domino) →
    dominos.PairwiseDisjoint DominoTilingsZ.Domino.toShape → ⋃ d ∈ dominos, d.toShape = S → DominoTilingsZ.Tiling S

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

## BASE-LIBRARY REF Sigma
{α : Type u} → (α → Type v) → Type (max u v)

Docstring: Dependent pairs, in which the second element's type depends on the value of the first element. The
type `Sigma β` is typically written `Σ a : α, β a` or `(a : α) × β a`.

Although its values are pairs, `Sigma` is sometimes known as the *dependent sum type*, since it is
the type level version of an indexed summation.


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

## BASE-LIBRARY REF PSigma.mk
{α : Sort u} → {β : α → Sort v} → (fst : α) → β fst → PSigma β

Docstring: Constructs a fully universe-polymorphic dependent pair. 

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


## BASE-LIBRARY REF LT.lt
{α : Type u} → [self : LT α] → α → α → Prop

Docstring: The less-than relation: `x < y` 

Conventions for notations in identifiers:

 * The recommended spelling of `<` in identifiers is `lt`.

## BASE-LIBRARY REF Sigma.mk
{α : Type u} → {β : α → Type v} → (fst : α) → β fst → Sigma β

Docstring: Constructs a dependent pair.

Using this constructor in a context in which the type is not known usually requires a type
ascription to determine `β`. This is because the desired relationship between the two values can't
generally be determined automatically.


## BASE-LIBRARY REF Fin.elim0
{α : Sort u} → Fin 0 → α

Docstring: The type `Fin 0` is uninhabited, so it can be used to derive any result whatsoever.

This is similar to `Empty.elim`. It can be thought of as a compiler-checked assertion that a code
path is unreachable, or a logical contradiction from which `False` and thus anything else could be
derived.


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

## BASE-LIBRARY REF Int.instAdd
Add ℤ

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
lem.gf-ws.decompose-tiling

\leanhelper  Given a tiling $T$ of $R_{n,2}$, there exists a $k$-tuple of faultfree tilings whose horizontal concatenation reproduces $T$. The decomposition is constructed recursively: for $n = 0$ it returns the empty tuple; if $T$ is faultfree it returns the singleton $(T)$; otherwise it cuts at the minimum fault and recurses on the right part.

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

## VERDICT
{
  "verdict": "drift",
  "justification": "The blueprint requires a tuple \u201cwhose horizontal concatenation reproduces T.\u201d The target codomain is only `(k : \u2115) \u00d7 (Fin k \u2192 (m : \u2115) \u00d7 { T' // DominoTilingsZ.isFaultfree m T' })`. Thus it certifies that every returned component is faultfree, but contains no condition relating the component widths or tilings back to the input `T`: there is no assertion that the widths sum to `n`, that the pieces occur in the required order, or that their horizontal concatenation equals `T`. The recursive body follows the described cutting algorithm, including the `n = 0`, faultfree, and minimum-fault cases, but it does not itself provide the missing reconstruction proposition in the declaration\u2019s result type. This is expressible using a reconstruction/concatenation predicate built from the available tiling, domino-set, and shift notions. To make the declaration faithful, define such a predicate (for example `ConcatenatesTo n T ts`) and return a subtype carrying a proof of it, such as `(k : \u2115) \u00d7 { ts : Fin k \u2192 (m : \u2115) \u00d7 {T' // isFaultfree m T'} // ConcatenatesTo n T ts }`, or provide a theorem asserting that `decomposeTiling n T` satisfies that predicate."
}