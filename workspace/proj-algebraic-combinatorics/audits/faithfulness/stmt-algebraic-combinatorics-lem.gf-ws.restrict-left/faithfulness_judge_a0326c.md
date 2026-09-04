## TARGET DominoTilingsZ.restrictTilingLeft (def) — ELABORATED SIGNATURE
(n : ℕ) →
  (T : DominoTilingsZ.Tiling (DominoTilingsZ.Rectangle n 2)) →
    (k : ℕ) → DominoTilingsZ.hasFault n T k → DominoTilingsZ.Tiling (DominoTilingsZ.Rectangle k 2)

Body:
fun n T k hk => { dominos := {d | d ∈ T.dominos ∧ d.inLeftPart k}, pairwise_disjoint := ⋯, cover := ⋯ }

Docstring: Restrict a tiling to the left part at a fault position 

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

## PROJECT DEPENDENCY DominoTilingsZ.Tiling.mk (constructor)
{S : DominoTilingsZ.Shape} →
  (dominos : Set DominoTilingsZ.Domino) →
    dominos.PairwiseDisjoint DominoTilingsZ.Domino.toShape → ⋃ d ∈ dominos, d.toShape = S → DominoTilingsZ.Tiling S

## PROJECT DEPENDENCY DominoTilingsZ.Domino (inductive)
Type

Body:
DominoTilingsZ.Domino.horizontal : ℤ → ℤ → DominoTilingsZ.Domino
DominoTilingsZ.Domino.vertical : ℤ → ℤ → DominoTilingsZ.Domino

Docstring: A domino is either horizontal or vertical (Definition \ref{def.domino.shapes-and-tilings}(c)) 

## PROJECT DEPENDENCY DominoTilingsZ.Tiling.dominos (def)
{S : DominoTilingsZ.Shape} → DominoTilingsZ.Tiling S → Set DominoTilingsZ.Domino

Body:
fun S self => self.1

Docstring: The set of dominos in the tiling 

## PROJECT DEPENDENCY DominoTilingsZ.Domino.inLeftPart (def)
DominoTilingsZ.Domino → ℕ → Prop

Body:
fun d k => ∀ p ∈ d.toShape, p.1 ≤ ↑k

Docstring: A domino is in the left part (all x-coordinates ≤ k) 

## PROJECT DEPENDENCY DominoTilingsZ.Shape (def)
Type

Body:
Set (ℤ × ℤ)

Docstring: A shape is a subset of ℤ² (Definition \ref{def.domino.shapes-and-tilings}(a)) 

## PROJECT DEPENDENCY DominoTilingsZ.Domino.toShape (def)
DominoTilingsZ.Domino → DominoTilingsZ.Shape

Body:
fun x =>
  match x with
  | DominoTilingsZ.Domino.horizontal i j => {(i, j), (i + 1, j)}
  | DominoTilingsZ.Domino.vertical i j => {(i, j), (i, j + 1)}

Docstring: The cells covered by a domino 

## BASE-LIBRARY REF Set.Mem
{α : Type u} → Set α → α → Prop

Body:
fun {α} s a => s a

Docstring: Membership in a set 

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

## BASE-LIBRARY REF InfSet.sInf
{α : Type u_1} → [self : InfSet α] → Set α → α

Body:
fun α [self : InfSet α] => self.1

Docstring: Infimum of a set 

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

## BASE-LIBRARY REF Nat.lt
ℕ → ℕ → Prop

Body:
fun n m => n.succ.le m

Docstring: Strict inequality of natural numbers, usually accessed via the `<` operator.

It is defined as `n < m = n + 1 ≤ m`.


## BASE-LIBRARY REF Int.instLTInt
LT ℤ

Body:
{ lt := Int.lt }

## BASE-LIBRARY REF Int.lt
ℤ → ℤ → Prop

Body:
fun a b => a + 1 ≤ b

Docstring: Strict inequality of integers, usually accessed via the `<` operator.

`a < b` when `a + 1 ≤ b`.


## BASE-LIBRARY REF Add
Type u → Type u

Docstring: The homogeneous version of `HAdd`: `a + b : α` where `a b : α`. 

## BASE-LIBRARY REF Add.add
{α : Type u} → [self : Add α] → α → α → α

Body:
fun α [self : Add α] => self.1

Docstring: `a + b` computes the sum of `a` and `b`. See `HAdd`. 

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

## INFORMAL STATEMENT
lem.gf-ws.restrict-left

\leanhelper  Given a tiling $T$ of $R_{n,2}$ with a fault at position $k$, the set of dominos lying in the left part forms a valid tiling of $R_{k,2}$.

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
  "verdict": "unclear",
  "discrepancies": [],
  "justification": "The blueprint says only \u201cwith a fault at position $k$\u201d and supplies no informal definition of a fault. The formal predicate unfolds to `k > 0 \u2227 k < n \u2227 \u2200 d \u2208 T.dominos, ...`, where a horizontal domino at `(i,j)` must satisfy `i < \u2191k \u2228 i \u2265 \u2191k + 1`. Thus it specifically treats faults as interior cuts between columns `k` and `k+1` and excludes the boundary positions `k = 0` and `k = n`. The supplied informal definition covers shapes, rectangles, dominos, and tilings, but not faults, so the package does not determine whether these range and non-straddling conditions exactly match the blueprint\u2019s meaning. An informal definition of \u201cfault at position $k$,\u201d particularly its allowed boundary positions, is needed. Conditional on that match, the target body does return exactly the tiling whose domino set is `{d | d \u2208 T.dominos \u2227 d.inLeftPart k}`, as claimed."
}