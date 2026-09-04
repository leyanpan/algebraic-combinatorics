## TARGET DominoTilingsZ.weightGenFun_tilingsHeight2 (theorem) — ELABORATED SIGNATURE
DominoTilingsZ.TilingsHeight2.weightGenFun DominoTilingsZ.tilingsHeight2_isFiniteType =
  PowerSeries.mk fun n => ↑(Nat.fib (n + 1))

Docstring: The generating function of height-2 tilings equals 1/(1-x-x²),
which is the Fibonacci generating function 

## PROJECT DEPENDENCY WeightedSet.weightGenFun (def)
{R : Type u_1} → [CommSemiring R] → {α : Type u_2} → (W : WeightedSet α) → W.IsFiniteType → PowerSeries R

Body:
fun {R} [CommSemiring R] {α} W hft => PowerSeries.mk fun n => ↑(W.countOfWeight hft n)

Docstring: The weight generating function of a finite-type weighted set is the FPS
∑_{n ∈ ℕ} (# of elements of weight n) · x^n.
(Definition \ref{def.gf-ws.weighted-sets}(c)) 

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

## PROJECT DEPENDENCY DominoTilingsZ.TilingsHeight2 (def)
WeightedSet ((n : ℕ) × DominoTilingsZ.Tiling (DominoTilingsZ.Rectangle n 2))

Body:
{
  weight := fun x =>
    match x with
    | ⟨n, snd⟩ => n }

Docstring: Domino tilings of height-2 rectangles, with weight = width of rectangle 

## PROJECT DEPENDENCY DominoTilingsZ.tilingsHeight2_isFiniteType (theorem)
DominoTilingsZ.TilingsHeight2.IsFiniteType

Docstring: TilingsHeight2 is a finite-type weighted set 

## PROJECT DEPENDENCY WeightedSet (inductive)
Type u_2 → Type u_2

Body:
WeightedSet.mk : {α : Type u_2} → (α → ℕ) → WeightedSet α

Docstring: A weighted set is a type equipped with a weight function to ℕ.
(Definition \ref{def.gf-ws.weighted-sets}(a)) 

## PROJECT DEPENDENCY WeightedSet.IsFiniteType (def)
{α : Type u_2} → WeightedSet α → Prop

Body:
fun {α} W => ∀ (n : ℕ), {a | W.weight a = n}.Finite

Docstring: A weighted set is finite-type if for each n ∈ ℕ, there are only finitely many
elements of weight n. (Definition \ref{def.gf-ws.weighted-sets}(b)) 

## PROJECT DEPENDENCY WeightedSet.countOfWeight (def)
{α : Type u_2} → (W : WeightedSet α) → W.IsFiniteType → ℕ → ℕ

Body:
fun {α} W hft n => ⋯.toFinset.card

Docstring: For a finite-type weighted set, the count of elements of weight n 

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

## PROJECT DEPENDENCY WeightedSet.mk (constructor)
{α : Type u_2} → (α → ℕ) → WeightedSet α

## PROJECT DEPENDENCY WeightedSet.weight (def)
{α : Type u_2} → WeightedSet α → α → ℕ

Body:
fun α self => self.1

Docstring: The weight function assigning a natural number to each element 

## BASE-LIBRARY REF PowerSeries
Type u_1 → Type (max u_1 0)

Body:
fun R => MvPowerSeries Unit R

Docstring: Formal power series over a coefficient type `R` 

## BASE-LIBRARY REF Rat
Type

Docstring: Rational numbers, implemented as a pair of integers `num / den` such that the
denominator is positive and the numerator and denominator are coprime.


## BASE-LIBRARY REF Rat.commSemiring
CommSemiring ℚ

Body:
inferInstance

## BASE-LIBRARY REF CommSemiring
Type u → Type u

Docstring: A commutative semiring is a semiring with commutative multiplication. 

## BASE-LIBRARY REF Rat.commRing
CommRing ℚ

Body:
let __spread.0 := Rat.addCommGroup;
let __spread.1 := Rat.commMonoid;
{ toAddMonoid := __spread.0.toAddMonoid, add_comm := ⋯, toMul := __spread.1.toMul, left_distrib := Rat.mul_add,
  right_distrib := Rat.add_mul, zero_mul := Rat.zero_mul, mul_zero := Rat.mul_zero, mul_assoc := Rat.commRing._proof_1,
  toOne := __spread.1.toOne, one_mul := Rat.commRing._proof_5, mul_one := Rat.commRing._proof_6,
  natCast := fun n => ↑↑n, natCast_zero := Rat.commRing._proof_7, natCast_succ := ⋯, npow := Monoid.npow,
  npow_zero := Rat.commRing._proof_8, npow_succ := Rat.commRing._proof_9, toNeg := __spread.0.t …

## BASE-LIBRARY REF Sigma
{α : Type u} → (α → Type v) → Type (max u v)

Docstring: Dependent pairs, in which the second element's type depends on the value of the first element. The
type `Sigma β` is typically written `Σ a : α, β a` or `(a : α) × β a`.

Although its values are pairs, `Sigma` is sometimes known as the *dependent sum type*, since it is
the type level version of an indexed summation.


## BASE-LIBRARY REF Rat.instNatCast
NatCast ℚ

Body:
{ natCast := fun n => Rat.ofInt ↑n }

## BASE-LIBRARY REF Rat.ofInt
ℤ → ℚ

Body:
fun num => { num := num, den_nz := instInhabitedRat._proof_1, reduced := ⋯ }

Docstring: Embedding of `Int` in the rational numbers. 

## BASE-LIBRARY REF Nat.fib
ℕ → ℕ

Body:
fun n => ((fun p => (p.2, p.1 + p.2))^[n] (0, 1)).1

Docstring: Implementation of the Fibonacci sequence satisfying
`fib 0 = 0, fib 1 = 1, fib (n + 2) = fib n + fib (n + 1)`.

*Note:* We use a stream iterator for better performance when compared to the naive recursive
implementation.


## BASE-LIBRARY REF Add
Type u → Type u

Docstring: The homogeneous version of `HAdd`: `a + b : α` where `a b : α`. 

## BASE-LIBRARY REF Add.add
{α : Type u} → [self : Add α] → α → α → α

Body:
fun α [self : Add α] => self.1

Docstring: `a + b` computes the sum of `a` and `b`. See `HAdd`. 

## BASE-LIBRARY REF Nat.add
ℕ → ℕ → ℕ

Body:
fun x x_1 =>
  Nat.brecOn (motive := fun x => ℕ → ℕ) x_1
    (fun x f x_2 =>
      (match (motive := ℕ → (x : ℕ) → Nat.below (motive := fun x => ℕ → ℕ) x → ℕ) x_2, x with
        | a, Nat.zero => fun x => a
        | a, b.succ => fun x => (x.1 a).succ)
        f)
    x

Docstring: Addition of natural numbers, typically used via the `+` operator.

This function is overridden in both the kernel and the compiler to efficiently evaluate using the
arbitrary-precision arithmetic library. The definition provided here is the logical model.


## BASE-LIBRARY REF AddMonoidWithOne
Type u_2 → Type u_2

Docstring: An `AddMonoidWithOne` is an `AddMonoid` with a `1`.
It also contains data for the unique homomorphism `ℕ → R`. 

## BASE-LIBRARY REF AddCommMonoidWithOne
Type u_2 → Type u_2

Docstring: An `AddCommMonoidWithOne` is an `AddMonoidWithOne` satisfying `a + b = b + a`. 

## BASE-LIBRARY REF NonAssocSemiring
Type u → Type u

Docstring: A unital but not-necessarily-associative semiring. 

## BASE-LIBRARY REF AddCommMonoid.add_comm
∀ {M : Type u} [self : AddCommMonoid M] (a b : M), a + b = b + a

Docstring: Addition is commutative in a commutative additive magma. 

## BASE-LIBRARY REF Semiring
Type u → Type u

Docstring: A `Semiring` is a type with addition, multiplication, a `0` and a `1` where addition is
commutative and associative, multiplication is associative and left and right distributive over
addition, and `0` and `1` are additive and multiplicative identities. 

## BASE-LIBRARY REF Semiring.one_mul
∀ {α : Type u} [self : Semiring α] (a : α), 1 * a = a

Docstring: One is a left neutral element for multiplication 

## BASE-LIBRARY REF Semiring.mul_one
∀ {α : Type u} [self : Semiring α] (a : α), a * 1 = a

Docstring: One is a right neutral element for multiplication 

## BASE-LIBRARY REF Set.PairwiseDisjoint
{α : Type u_1} → {ι : Type u_4} → [inst : PartialOrder α] → [OrderBot α] → Set ι → (ι → α) → Prop

Body:
fun {α} {ι} [PartialOrder α] [OrderBot α] s f => s.Pairwise (Function.onFun Disjoint f)

Docstring: A set is `PairwiseDisjoint` under `f`, if the images of any distinct two elements under `f`
are disjoint.

`s.Pairwise Disjoint` is (definitionally) the same as `s.PairwiseDisjoint id`. We prefer the latter
in order to allow dot notation on `Set.PairwiseDisjoint`, even though the former unfolds more
nicely. 

## BASE-LIBRARY REF ChainCompletePartialOrder
Type u_2 → Type u_2

Docstring: A chain complete partial order (CCPO) is a nonempty partial order such that every
nonempty chain has a supremum (which we call `cSup`) 

## BASE-LIBRARY REF ChainCompletePartialOrder.instOfCompleteLattice
{α : Type u_1} → [CompleteLattice α] → ChainCompletePartialOrder α

Body:
fun {α} [CompleteLattice α] =>
  { toPartialOrder := CompleteLattice.instOmegaCompletePartialOrder.toPartialOrder, cSup := fun c => sSup ↑c,
    le_cSup := ⋯, cSup_le := ⋯ }

## BASE-LIBRARY REF CompleteLattice
Type u_8 → Type u_8

Docstring: A complete lattice is a bounded lattice which has suprema and infima for every subset. 

## BASE-LIBRARY REF CompleteLattice.instOmegaCompletePartialOrder
{α : Type u_2} → [CompleteLattice α] → OmegaCompletePartialOrder α

Body:
fun {α} [inst : CompleteLattice α] =>
  { toPartialOrder := inst.toCompleteSemilatticeInf.toPartialOrder, ωSup := fun c => ⨆ i, c i, le_ωSup := ⋯,
    ωSup_le := ⋯ }

Docstring: Any complete lattice has an `ω`-CPO structure where the countable supremum is a special case
of arbitrary suprema. 

## BASE-LIBRARY REF NonemptyChain
(α : Type u_2) → [LE α] → Type u_2

Docstring: The type of nonempty chains of an order 

## BASE-LIBRARY REF SupSet.sSup
{α : Type u_1} → [self : SupSet α] → Set α → α

Body:
fun α [self : SupSet α] => self.1

Docstring: Supremum of a set 

## BASE-LIBRARY REF SetLike.coe
{A : Type u_1} → {B : outParam (Type u_2)} → [self : SetLike A B] → A → Set B

Body:
fun A {B} [self : SetLike A B] => self.1

Docstring: The coercion from a term of a `SetLike` to its corresponding `Set`. 

## BASE-LIBRARY REF CompleteBooleanAlgebra
Type u_1 → Type u_1

Docstring: A complete Boolean algebra is a Boolean algebra that is also a complete distributive lattice.

It is only completely distributive if it is also atomic.


## BASE-LIBRARY REF CompleteAtomicBooleanAlgebra
Type u → Type u

Docstring: A complete atomic Boolean algebra is a complete Boolean algebra
that is also completely distributive.

We take iSup_iInf_eq as the definition here,
and prove later on that this implies atomicity.


## BASE-LIBRARY REF Set.instCompleteAtomicBooleanAlgebra
{α : Type u_1} → CompleteAtomicBooleanAlgebra (Set α)

Body:
fun {α} =>
  let __src := Set.instBooleanAlgebra;
  { toLattice := __src.toLattice, toSupSet := Set.instSupSet, le_sSup := ⋯, sSup_le := ⋯, toInfSet := Set.instInfSet,
    sInf_le := ⋯, le_sInf := ⋯, toTop := __src.toTop, le_top := ⋯, toBot := __src.toBot, bot_le := ⋯, le_sup_inf := ⋯,
    toCompl := __src.toCompl, toSDiff := __src.toSDiff, toHImp := __src.toHImp, inf_compl_le_bot := ⋯,
    top_le_sup_compl := ⋯, sdiff_eq := ⋯, himp_eq := ⋯, iInf_iSup_eq := ⋯ }

## BASE-LIBRARY REF BooleanAlgebra
Type u → Type u

Docstring: A Boolean algebra is a bounded distributive lattice with a complement operator `ᶜ` such that
`x ⊓ xᶜ = ⊥` and `x ⊔ xᶜ = ⊤`. For convenience, it must also provide a set difference operation `\`
and a Heyting implication `⇨` satisfying `x \ y = x ⊓ yᶜ` and `x ⇨ y = y ⊔ xᶜ`.

This is a generalization of (classical) logic of propositions, or the powerset lattice.

Since `BoundedOrder`, `OrderBot`, and `OrderTop` are mixins that require `LE`
to be present at define-time, the `extends` mechanism does not work with them.
Instead, we extend using the underlying `Bot` and `Top` data typeclasses, and replicate the
order axioms of those classes here. A "forgetful" instance back to `BoundedOrder` is provided.


## BASE-LIBRARY REF Set.instBooleanAlgebra
{α : Type u_1} → BooleanAlgebra (Set α)

Body:
fun {α} =>
  let __spread.0 := inferInstance;
  let __spread.1 := inferInstance;
  { toDistribLattice := __spread.0, compl := fun x => xᶜ, sdiff := fun x1 x2 => x1 \ x2, toHImp := __spread.1.toHImp,
    toTop := __spread.1.toTop, toBot := __spread.1.toBot, inf_compl_le_bot := ⋯, top_le_sup_compl := ⋯, le_top := ⋯,
    bot_le := ⋯, sdiff_eq := ⋯, himp_eq := ⋯ }

## BASE-LIBRARY REF Set.instSupSet
{α : Type u} → SupSet (Set α)

Body:
fun {α} => { sSup := fun s => {a | ∃ t ∈ s, a ∈ t} }

## BASE-LIBRARY REF Set.instCompleteAtomicBooleanAlgebra._proof_1
∀ {α : Type u_1} (x : Set (Set α)), ∀ t ∈ x, ∀ x_1 ∈ t, ∃ t ∈ x, x_1 ∈ t

## BASE-LIBRARY REF Set.instCompleteAtomicBooleanAlgebra._proof_2
∀ {α : Type u_1} (x : Set (Set α)) (x_1 : Set α), (∀ b ∈ x, b ≤ x_1) → ∀ x_2 ∈ sSup x, x_2 ∈ x_1

## BASE-LIBRARY REF Set.instInfSet
{α : Type u} → InfSet (Set α)

Body:
fun {α} => { sInf := fun s => {a | ∀ t ∈ s, a ∈ t} }

## BASE-LIBRARY REF Prod
Type u → Type v → Type (max u v)

Docstring: The product type, usually written `α × β`. Product types are also called pair or tuple types.
Elements of this type are pairs in which the first element is an `α` and the second element is a
`β`.

Products nest to the right, so `(x, y, z) : α × β × γ` is equivalent to `(x, (y, z)) : α × (β × γ)`.


Conventions for notations in identifiers:

 * The recommended spelling of `×` in identifiers is `Prod`.

## BASE-LIBRARY REF HeytingAlgebra
Type u_4 → Type u_4

Docstring: A Heyting algebra is a bounded lattice with an additional binary operation `⇨` called Heyting
implication such that `(a ⇨ ·)` is right adjoint to `(a ⊓ ·)`. 

## BASE-LIBRARY REF Order.Frame.toHeytingAlgebra
{α : Type u_1} → [self : Order.Frame α] → HeytingAlgebra α

Body:
fun α self =>
  { toLattice := self.toLattice, toOrderTop := self.toOrderTop, toHImp := self.toHImp, le_himp_iff := ⋯,
    toOrderBot := self.toOrderBot, toCompl := self.toCompl, himp_bot := ⋯ }

## BASE-LIBRARY REF Order.Frame
Type u_1 → Type u_1

Docstring: A frame, aka complete Heyting algebra, is a complete lattice whose `⊓` distributes over `⨆`. 

## BASE-LIBRARY REF Order.Frame.toCompleteLattice
{α : Type u_1} → [self : Order.Frame α] → CompleteLattice α

Body:
fun α [self : Order.Frame α] => self.1

## BASE-LIBRARY REF Order.Frame.toHImp
{α : Type u_1} → [self : Order.Frame α] → HImp α

Body:
fun α [self : Order.Frame α] => self.2

## BASE-LIBRARY REF Order.Frame.le_himp_iff
∀ {α : Type u_1} [self : Order.Frame α] (a b c : α), a ≤ b ⇨ c ↔ a ⊓ b ≤ c

Docstring: `(a ⇨ ·)` is right adjoint to `(a ⊓ ·)` 

## BASE-LIBRARY REF CompleteDistribLattice
Type u_1 → Type u_1

Docstring: A complete distributive lattice is a complete lattice whose `⊔` and `⊓` respectively
distribute over `⨅` and `⨆`. 

## BASE-LIBRARY REF BiheytingAlgebra
Type u_4 → Type u_4

Docstring: A bi-Heyting algebra is a Heyting algebra that is also a co-Heyting algebra. 

## BASE-LIBRARY REF CompleteBooleanAlgebra.toCompleteDistribLattice._proof_4
∀ {α : Type u_1} [inst : CompleteBooleanAlgebra α] (a b c : α), a ≤ b ⇨ c ↔ a ⊓ b ≤ c

## BASE-LIBRARY REF CompleteBooleanAlgebra.toCompleteDistribLattice._proof_5
∀ {α : Type u_1} [inst : CompleteBooleanAlgebra α] (a : α), a ⇨ ⊥ = aᶜ

## BASE-LIBRARY REF BiheytingAlgebra.sdiff_le_iff
∀ {α : Type u_4} [self : BiheytingAlgebra α] (a b c : α), a \ b ≤ c ↔ a ≤ b ⊔ c

Docstring: `(· \ a)` is left adjoint to `(· ⊔ a)` 

## BASE-LIBRARY REF Set.iUnion
{α : Type u} → {ι : Sort v} → (ι → Set α) → Set α

Body:
fun {α} {ι} s => iSup s

Docstring: Indexed union of a family of sets 

## BASE-LIBRARY REF Set.Mem
{α : Type u} → Set α → α → Prop

Body:
fun {α} s a => s a

Docstring: Membership in a set 

## BASE-LIBRARY REF Int.instLEInt
LE ℤ

Body:
{ le := Int.le }

## BASE-LIBRARY REF Int.le
ℤ → ℤ → Prop

Body:
fun a b => (b - a).NonNeg

Docstring: Non-strict inequality of integers, usually accessed via the `≤` operator.

`a ≤ b` is defined as `b - a ≥ 0`, using `Int.NonNeg`.


## BASE-LIBRARY REF Int.ofNat
ℕ → ℤ

Docstring: A natural number is an integer.

This constructor covers the non-negative integers (from `0` to `∞`).


## BASE-LIBRARY REF Prod.fst
{α : Type u} → {β : Type v} → α × β → α

Body:
fun α β self => self.1

Docstring: The first element of a pair. 

## BASE-LIBRARY REF Prod.snd
{α : Type u} → {β : Type v} → α × β → β

Body:
fun α β self => self.2

Docstring: The second element of a pair. 

## BASE-LIBRARY REF Set.Finite
{α : Type u} → Set α → Prop

Body:
fun {α} s => Finite ↑s

Docstring: A set is finite if the corresponding `Subtype` is finite,
i.e., if there exists a natural `n : ℕ` and an equivalence `s ≃ Fin n`. 

## BASE-LIBRARY REF Finset.card
{α : Type u_1} → Finset α → ℕ

Body:
fun {α} s => s.val.card

Docstring: `s.card` is the number of elements of `s`, aka its cardinality.

The notation `#s` can be accessed in the `Finset` locale. 

## BASE-LIBRARY REF Set.Finite.toFinset
{α : Type u} → {s : Set α} → s.Finite → Finset α

Body:
fun {α} {s} h => s.toFinset

Docstring: Using choice, get the `Finset` that represents this `Set`. 

## BASE-LIBRARY REF Insert.insert
{α : outParam (Type u)} → {γ : Type v} → [self : Insert α γ] → α → γ → γ

Body:
fun {α} γ [self : Insert α γ] => self.1

Docstring: `insert x xs` inserts the element `x` into the collection `xs`. 

## BASE-LIBRARY REF Set.instInsert
{α : Type u} → Insert α (Set α)

Body:
fun {α} => { insert := Set.insert }

## BASE-LIBRARY REF Set.insert
{α : Type u} → α → Set α → Set α

Body:
fun {α} a s => {b | b = a ∨ b ∈ s}

Docstring: `Set.insert a s` is the set `{a} ∪ s`.

Note that you should **not** use this definition directly, but instead write `insert a s` (which is
mediated by the `Insert` typeclass). 

## BASE-LIBRARY REF Singleton.singleton
{α : outParam (Type u)} → {β : Type v} → [self : Singleton α β] → α → β

Body:
fun {α} β [self : Singleton α β] => self.1

Docstring: `singleton x` is a collection with the single element `x` (notation: `{x}`). 

Conventions for notations in identifiers:

 * The recommended spelling of `{x}` in identifiers is `singleton`.

## BASE-LIBRARY REF Set.instSingletonSet
{α : Type u} → Singleton α (Set α)

Body:
fun {α} => { singleton := Set.singleton }

## BASE-LIBRARY REF Set.singleton
{α : Type u} → α → Set α

Body:
fun {α} a => {b | b = a}

Docstring: The singleton of an element `a` is the set with `a` as a single element.

Note that you should **not** use this definition directly, but instead write `{a}`. 

## BASE-LIBRARY REF Int.instAdd
Add ℤ

Body:
{ add := Int.add }

## BASE-LIBRARY REF Int.add
ℤ → ℤ → ℤ

Body:
fun m n =>
  match m, n with
  | Int.ofNat m, Int.ofNat n => Int.ofNat (m + n)
  | Int.ofNat m, Int.negSucc n => Int.subNatNat m n.succ
  | Int.negSucc m, Int.ofNat n => Int.subNatNat n m.succ
  | Int.negSucc m, Int.negSucc n => Int.negSucc (m + n).succ

Docstring: Addition of integers, usually accessed via the `+` operator.

This function is overridden by the compiler with an efficient implementation. This definition is
the logical model.

Examples:
 * `(7 : Int) + (6 : Int) = 13`
 * `(6 : Int) + (-6 : Int) = 0`


## INFORMAL STATEMENT
lem.gf-ws.weightGenFun-tilingsHeight2

\leanhelper  The weight generating function of $D$ equals $\sum _n f_{n+1} x^n$, the Fibonacci generating function.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fib.fibonacci
def.fib.fibonacci

\leanhelper  The \emph{Fibonacci sequence} $(f_0, f_1, f_2, \ldots )$ is defined by $f_0 = 0$, $f_1 = 1$, and $f_n = f_{n-1} + f_{n-2}$ for $n \geq 2$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.coeff
def.fps.coeff

If $n\in \mathbb {N}$, and if $\mathbf{a}=\left( a_{0},a_{1},a_{2},\ldots \right) \in K\left[\left[x\right]\right]$ is an FPS, then we define an element $\left[x^{n}\right]\mathbf{a}\in K$ by 

\[  \left[x^{n}\right]\mathbf{a}:=a_{n}.  \]

 This is called the \emph{coefficient of }$x^{n}$\emph{ in }$\mathbf{a}$, or the $n$\emph{-th coefficient} of $\mathbf{a}$, or the $x^{n}$\emph{-coefficient} of $\mathbf{a}$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.fps
def.fps.fps

A \emph{formal power series} (or, short, \emph{FPS}) in $1$ indeterminate over $K$ means a sequence $\left(a_{0},a_{1},a_{2},\ldots \right) = \left(a_{n}\right)_{n\in \mathbb {N}} \in K^{\mathbb {N}}$ of elements of $K$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.gf
def.fps.gf

\leanhelper  The \emph{(ordinary) generating function} of a sequence $(a_0, a_1, a_2, \ldots )$ is the FPS $(a_0, a_1, a_2, \ldots ) = \sum _{n\geq 0} a_n x^n$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.lim.issummable
def.fps.lim.isSummable

\leanhelper  A family $(f_n)_{n \in \mathbb {N}}$ of FPSs is \emph{summable} if for each $n \in \mathbb {N}$, the set $\{ i \in \mathbb {N} : [x^n] f_i \neq 0\} $ is finite.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.lim.tsum
def.fps.lim.tsum

\leanhelper  The \emph{infinite sum} of a summable family $(f_n)_{n \in \mathbb {N}}$ is the FPS $\sum _{n \in \mathbb {N}} f_n$ whose $n$-th coefficient is $\sum _{i \in S_n} [x^n] f_i$, where $S_n = \{ i : [x^n] f_i \neq 0\} $.

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.infsum.essfin
def.infsum.essfin

\textbf{(a)} A family $\left(a_{i}\right)_{i\in I}\in K^{I}$ of elements of $K$ is said to be \emph{essentially finite} if all but finitely many $i\in I$ satisfy $a_{i}=0$ (in other words, if the set $\left\{ i\in I\  \mid \  a_{i}\neq 0\right\} $ is finite). \medskip 

\textbf{(b)} Let $\left(a_{i}\right)_{i\in I}\in K^{I}$ be an essentially finite family of elements of $K$. Then, the infinite sum $\sum _{i\in I}a_{i}$ is defined to equal the finite sum $\sum _{\substack {i\in I;\\ a_{i}\neq 0}}a_{i}$. Such an infinite sum is said to be \emph{essentially finite}.

## VERDICT
{
  "verdict": "faithful",
  "discrepancies": [],
  "justification": "The target states `TilingsHeight2.weightGenFun tilingsHeight2_isFiniteType = PowerSeries.mk fun n => \u2191(Nat.fib (n + 1))`. Unfolding `WeightedSet.weightGenFun`, the left side is the FPS whose coefficient at `n` is the number of elements of `TilingsHeight2` of weight `n`; unfolding `TilingsHeight2`, these are tilings of `Rectangle n 2`, with weight equal to the width `n`. The right side is precisely the FPS with coefficient `f_{n+1}`, since `Nat.fib` satisfies `fib 0 = 0`, `fib 1 = 1`, and the stated Fibonacci recurrence. Thus it exactly certifies the informal claim that the weight generating function of `D` is `\u2211_n f_{n+1} x^n`."
}