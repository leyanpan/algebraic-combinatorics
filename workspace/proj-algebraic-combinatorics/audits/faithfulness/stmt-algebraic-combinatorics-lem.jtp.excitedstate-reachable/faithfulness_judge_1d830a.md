## TARGET AlgebraicCombinatorics.State.excitedState_reachable (theorem) — ELABORATED SIGNATURE
∀ (ell : ℤ) {n : ℕ} (mu : n.Partition),
  (AlgebraicCombinatorics.State.groundState ell).ReachableByJumps (AlgebraicCombinatorics.State.excitedState ell mu)

Docstring: The excited state is reachable from the ground state by a sequence of jumps.
This follows from the construction: we apply k jumps, one for each part of μ.

The proof proceeds by induction on the number of parts k = (mu.parts.sort (· ≥ ·)).length:
- Base case (k = 0): The excited state has levels {p | p < ell} = groundState.levels,
  so ReachableByJumps.refl applies.
- Inductive case (k > 0): We construct k jumps where the i-th jump (0-indexed) is
  from level (ell - 1 - i) by parts[i] steps. Each jump is valid because:
  1. (ell - 1 - i) is in the intermediate state (it's < ell - i)
  2. (ell - 1 - i + parts[i]) is NOT in the intermediate state (requires parts[i] > 0
     and no collision with previous jump targets)
  3. parts[i] > 0 (all parts of a partition are positive)


## PROJECT DEPENDENCY AlgebraicCombinatorics.State.ReachableByJumps (inductive)
AlgebraicCombinatorics.State → AlgebraicCombinatorics.State → Prop

Body:
AlgebraicCombinatorics.State.ReachableByJumps.refl : ∀ {T : AlgebraicCombinatorics.State}, T.ReachableByJumps T
AlgebraicCombinatorics.State.ReachableByJumps.step : ∀ {T : AlgebraicCombinatorics.State} (S S' : AlgebraicCombinatorics.State) (p : AlgebraicCombinatorics.Level) (q : ℕ)
  (hp : p ∈ S.levels) (hpq : p + ↑q ∉ S.levels) (hq : q > 0),
  T.ReachableByJumps S → S' = S.jump p q hp hpq hq → T.ReachableByJumps S'

Docstring: A state S is reachable from T by a sequence of jumps. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.State.groundState (def)
ℤ → AlgebraicCombinatorics.State

Body:
fun ell => { levels := {p | p < ell}, finite_nonneg := ⋯, finite_negative_missing := ⋯ }

Docstring: The ℓ-ground state G_ℓ = {all levels < ℓ}.

In the half-integer convention, G_ℓ contains all half-integer levels q < ℓ.
In our integer representation (where level q = p + 1/2), this is {p : p < ℓ}.

For ℓ ≥ 0:
- Nonnegative integers in G_ℓ: {0, 1, ..., ℓ-1}
- No negative integers are missing from G_ℓ

For ℓ < 0:
- No nonnegative integers are in G_ℓ
- Negative integers missing from G_ℓ: {ℓ, ℓ+1, ..., -1} 

## PROJECT DEPENDENCY AlgebraicCombinatorics.State.excitedState (def)
ℤ → {n : ℕ} → n.Partition → AlgebraicCombinatorics.State

Body:
fun ell {n} mu =>
  { levels := AlgebraicCombinatorics.State.excitedStateLevels ell mu, finite_nonneg := ⋯, finite_negative_missing := ⋯ }

Docstring: The excited state E_{ℓ,μ} obtained from the ground state by jumping electrons
according to the partition μ.

Given a partition μ = (μ₁, μ₂, ..., μₖ) of some n, we start with the ℓ-ground state
and let the k highest electrons jump by μ₁, μ₂, ..., μₖ steps respectively. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.State (inductive)
Type

Body:
AlgebraicCombinatorics.State.mk : (levels : Set AlgebraicCombinatorics.Level) →
  {p | p ≥ 0 ∧ p ∈ levels}.Finite → {p | p < 0 ∧ p ∉ levels}.Finite → AlgebraicCombinatorics.State

Docstring: A "state" is a set of levels that contains all but finitely many negative levels
and only finitely many positive levels.

This is used in Borcherds' proof of Jacobi's triple product identity.

**Important convention**: A "level" in the tex source is a half-integer `p + 1/2` for some integer p.
We represent it by the integer p. Thus:
- "positive level" in the tex source means `p + 1/2 > 0`, i.e., `p ≥ 0` in our representation
- "negative level" in the tex source means `p + 1/2 < 0`, i.e., `p < 0` in our representation

The structure tracks:
- `finite_nonneg`: the set of nonnegative integers p (representing positive half-integer levels) in S
- `finite_negative_missing`: the set of negative integers p (representing negative half-integer levels) NOT in S 

## PROJECT DEPENDENCY AlgebraicCombinatorics.Level (def)
Type

Body:
ℤ

Docstring: A "level" is a half-integer, represented as p + 1/2 for some integer p.
We represent it simply by the integer p. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.State.levels (def)
AlgebraicCombinatorics.State → Set AlgebraicCombinatorics.Level

Body:
fun self => self.1

Docstring: The set of levels in this state 

## PROJECT DEPENDENCY AlgebraicCombinatorics.State.jump (def)
(S : AlgebraicCombinatorics.State) →
  (p : AlgebraicCombinatorics.Level) → (q : ℕ) → p ∈ S.levels → p + ↑q ∉ S.levels → q > 0 → AlgebraicCombinatorics.State

Body:
fun S p q _hp _hpq _hq => { levels := S.levels \ {p} ∪ {p + ↑q}, finite_nonneg := ⋯, finite_negative_missing := ⋯ }

Docstring: Jump operation: if p ∈ S and p + q ∉ S, then jump_{p,q}(S) = (S \ {p}) ∪ {p + q}. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.State.mk (constructor)
(levels : Set AlgebraicCombinatorics.Level) →
  {p | p ≥ 0 ∧ p ∈ levels}.Finite → {p | p < 0 ∧ p ∉ levels}.Finite → AlgebraicCombinatorics.State

## PROJECT DEPENDENCY AlgebraicCombinatorics.State.excitedStateLevels (def)
ℤ → {n : ℕ} → n.Partition → Set AlgebraicCombinatorics.Level

Body:
fun ell {n} mu =>
  let parts := mu.parts.sort fun x1 x2 => x1 ≥ x2;
  let k := parts.length;
  {p | p < ell - ↑k} ∪ {p | ∃ i, p = ell - 1 - ↑↑i + ↑(parts.get (Fin.cast ⋯ i))}

Docstring: The explicit set of levels in an excited state E_{ℓ,μ}.
E_{ℓ,μ} = {p | p < ℓ-k} ∪ {ℓ-1-i+μ_i | i ∈ {0,...,k-1}}
where k is the number of parts and μ_i are the parts (sorted in decreasing order).

We use `mu.parts.sort (· ≥ ·)` to get a canonical decreasing ordering of parts.
This ensures that the excited levels uniquely encode the partition, since with sorted
parts the function `i ↦ parts[i] - i` is strictly decreasing (hence injective). 

## PROJECT DEPENDENCY AlgebraicCombinatorics.State.excitedStateLevels_finite_nonneg (theorem)
∀ (ell : ℤ) {n : ℕ} (mu : n.Partition), {p | p ≥ 0 ∧ p ∈ AlgebraicCombinatorics.State.excitedStateLevels ell mu}.Finite

Docstring: The excited state has finitely many nonnegative levels. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.State.excitedStateLevels_finite_negative_missing (theorem)
∀ (ell : ℤ) {n : ℕ} (mu : n.Partition), {p | p < 0 ∧ p ∉ AlgebraicCombinatorics.State.excitedStateLevels ell mu}.Finite

Docstring: The excited state has finitely many missing negative levels. 

## BASE-LIBRARY REF Int
Type

Docstring: The integers.

This type is special-cased by the compiler and overridden with an efficient implementation. The
runtime has a special representation for `Int` that stores “small” signed numbers directly, while
larger numbers use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)). A “small number” is an integer that can be encoded with one fewer bits
than the platform's pointer size (i.e. 63 bits on 64-bit architectures and 31 bits on 32-bit
architectures).


## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF Nat.Partition
ℕ → Type

Docstring: A partition of `n` is a multiset of positive integers summing to `n`. 

## BASE-LIBRARY REF Membership.mem
{α : outParam (Type u)} → {γ : Type v} → [self : Membership α γ] → γ → α → Prop

Docstring: The membership relation `a ∈ s : Prop` where `a : α`, `s : γ`. 

Conventions for notations in identifiers:

 * The recommended spelling of `∈` in identifiers is `mem`.

## BASE-LIBRARY REF Set
Type u → Type u

Docstring: A set is a collection of elements of some type `α`.

Although `Set` is defined as `α → Prop`, this is an implementation detail which should not be
relied on. Instead, `setOf` and membership of a set (`∈`) should be used to convert between sets
and predicates.


## BASE-LIBRARY REF Set.instMembership
{α : Type u} → Membership α (Set α)

## BASE-LIBRARY REF Not
Prop → Prop

Docstring: `Not p`, or `¬p`, is the negation of `p`. It is defined to be `p → False`,
so if your goal is `¬p` you can use `intro h` to turn the goal into
`h : p ⊢ False`, and if you have `hn : ¬p` and `h : p` then `hn h : False`
and `(hn h).elim` will prove anything.
For more information: [Propositional Logic](https://lean-lang.org/theorem_proving_in_lean4/propositions_and_proofs.html#propositional-logic)


Conventions for notations in identifiers:

 * The recommended spelling of `¬` in identifiers is `not`.

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

## BASE-LIBRARY REF GT.gt
{α : Type u} → [LT α] → α → α → Prop

Docstring: `a > b` is an abbreviation for `b < a`. 

Conventions for notations in identifiers:

 * The recommended spelling of `>` in identifiers is `gt`.

## BASE-LIBRARY REF instLTNat
LT ℕ

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

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

## BASE-LIBRARY REF setOf
{α : Type u} → (α → Prop) → Set α

Docstring: Turn a predicate `p : α → Prop` into a set, also written as `{x | p x}` 

## BASE-LIBRARY REF LT.lt
{α : Type u} → [self : LT α] → α → α → Prop

Docstring: The less-than relation: `x < y` 

Conventions for notations in identifiers:

 * The recommended spelling of `<` in identifiers is `lt`.

## BASE-LIBRARY REF Int.instLTInt
LT ℤ

## BASE-LIBRARY REF Set.Finite
{α : Type u} → Set α → Prop

Docstring: A set is finite if the corresponding `Subtype` is finite,
i.e., if there exists a natural `n : ℕ` and an equivalence `s ≃ Fin n`. 

## BASE-LIBRARY REF And
Prop → Prop → Prop

Docstring: `And a b`, or `a ∧ b`, is the conjunction of propositions. It can be
constructed and destructed like a pair: if `ha : a` and `hb : b` then
`⟨ha, hb⟩ : a ∧ b`, and if `h : a ∧ b` then `h.left : a` and `h.right : b`.


Conventions for notations in identifiers:

 * The recommended spelling of `∧` in identifiers is `and`.

 * The recommended spelling of `/\` in identifiers is `and` (prefer `∧` over `/\`).

## BASE-LIBRARY REF GE.ge
{α : Type u} → [LE α] → α → α → Prop

Docstring: `a ≥ b` is an abbreviation for `b ≤ a`. 

Conventions for notations in identifiers:

 * The recommended spelling of `≥` in identifiers is `ge`.

 * The recommended spelling of `>=` in identifiers is `ge` (prefer `≥` over `>=`).

## BASE-LIBRARY REF Int.instLEInt
LE ℤ

## BASE-LIBRARY REF instOfNat
{n : ℕ} → OfNat ℤ n

## BASE-LIBRARY REF Union.union
{α : Type u} → [self : Union α] → α → α → α

Docstring: `a ∪ b` is the union of `a` and `b`. 

Conventions for notations in identifiers:

 * The recommended spelling of `∪` in identifiers is `union`.

## BASE-LIBRARY REF Set.instUnion
{α : Type u} → Union (Set α)

## BASE-LIBRARY REF SDiff.sdiff
{α : Type u} → [self : SDiff α] → α → α → α

Docstring: `a \ b` is the set difference of `a` and `b`,
consisting of all elements in `a` that are not in `b`.


Conventions for notations in identifiers:

 * The recommended spelling of `\` in identifiers is `sdiff`.

## BASE-LIBRARY REF Set.instSDiff
{α : Type u} → SDiff (Set α)

## BASE-LIBRARY REF Singleton.singleton
{α : outParam (Type u)} → {β : Type v} → [self : Singleton α β] → α → β

Docstring: `singleton x` is a collection with the single element `x` (notation: `{x}`). 

Conventions for notations in identifiers:

 * The recommended spelling of `{x}` in identifiers is `singleton`.

## BASE-LIBRARY REF Set.instSingletonSet
{α : Type u} → Singleton α (Set α)

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


## BASE-LIBRARY REF Multiset.sort
{α : Type u_1} →
  Multiset α →
    (r : autoParam (α → α → Prop) Multiset.sort._auto_1) →
      [DecidableRel r] → [IsTrans α r] → [Std.Antisymm r] → [Std.Total r] → List α

Docstring: `sort s` constructs a sorted list from the multiset `s`.
(Uses merge sort algorithm.) 

## BASE-LIBRARY REF Nat.Partition.parts
{n : ℕ} → n.Partition → Multiset ℕ

Docstring: positive integers summing to `n` 

## BASE-LIBRARY REF instLENat
LE ℕ

## BASE-LIBRARY REF Nat.decLe
(n m : ℕ) → Decidable (n ≤ m)

Docstring: A decision procedure for non-strict inequality of natural numbers, usually accessed via the
`DecidableLE Nat` instance.

Examples:
 * `(if 3 ≤ 4 then "yes" else "no") = "yes"`
 * `(if 6 ≤ 4 then "yes" else "no") = "no"`
 * `show 12 ≤ 12 by decide`
 * `show 5 ≤ 12 by decide`


## BASE-LIBRARY REF instIsTransGe
∀ {α : Type u} [inst : Preorder α], IsTrans α fun x1 x2 => x2 ≤ x1

## BASE-LIBRARY REF Nat.instPreorder
Preorder ℕ

## BASE-LIBRARY REF instAntisymmGe
∀ {α : Type u} [inst : PartialOrder α], Std.Antisymm fun x1 x2 => x2 ≤ x1

## BASE-LIBRARY REF Nat.instPartialOrder
PartialOrder ℕ

## BASE-LIBRARY REF LE.total'
∀ {α : Type u} [inst : LinearOrder α], Std.Total fun x1 x2 => x2 ≤ x1

## BASE-LIBRARY REF Nat.instLinearOrder
LinearOrder ℕ

## BASE-LIBRARY REF List.length
{α : Type u_1} → List α → ℕ

Docstring: The length of a list.

This function is overridden in the compiler to `lengthTR`, which uses constant stack space.

Examples:
* `([] : List String).length = 0`
* `["green", "brown"].length = 2`


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


## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


## BASE-LIBRARY REF Fin.val
{n : ℕ} → Fin n → ℕ

Docstring: The number that is strictly less than `n`.

`Fin.val` is a coercion, so any `Fin n` can be used in a position where a `Nat` is expected.


## BASE-LIBRARY REF List.get
{α : Type u} → (as : List α) → Fin as.length → α

Docstring: Returns the element at the provided index, counting from `0`.

In other words, for `i : Fin as.length`, `as.get i` returns the `i`'th element of the list `as`.
Because the index is a `Fin` bounded by the list's length, the index will never be out of bounds.

Examples:
 * `["spring", "summer", "fall", "winter"].get (2 : Fin 4) = "fall"`
 * `["spring", "summer", "fall", "winter"].get (0 : Fin 4) = "spring"`


## BASE-LIBRARY REF Fin.cast
{n m : ℕ} → n = m → Fin n → Fin m

Docstring: Uses a proof that two bounds are equal to allow a value bounded by one to be used with the other.

In other words, when `eq : n = m`, `Fin.cast eq i` converts `i : Fin n` into a `Fin m`.


## INFORMAL STATEMENT
lem.jtp.excitedState-reachable

\leanhelper  The excited state $E_{\ell ,\lambda }$ is reachable from the ground state $G_\ell $ by a sequence of jumps (in the sense of Definition~ \ref{def.jtp.jump}).

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.jtp.jump
def.jtp.jump

\leanhelper  If $S$ is a state, $p\in S$, and $q$ is a positive integer such that $p+q\notin S$, then the state 

\[  \operatorname {jump}_{p,q}S:=\left( S\setminus \left\{  p\right\}  \right) \cup \left\{  p+q\right\}   \]

 is said to be obtained from $S$ by letting the electron at level $p$ \emph{jump} $q$ steps to the right.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The blueprint asserts that \u201cThe excited state E_{\u2113,\u03bb} is reachable from the ground state G_\u2113 by a sequence of jumps.\u201d The target states exactly `\u2200 (ell : \u2124) {n : \u2115} (mu : n.Partition), (groundState ell).ReachableByJumps (excitedState ell mu)`. Here `ReachableByJumps.refl` and `.step` encode a finite sequence of jumps, and each step requires precisely the informal conditions `p \u2208 S`, `p + q \u2209 S`, and positive `q`, with `jump` having levels `(S.levels \\ {p}) \u222a {p + q}`. The definitions of `groundState` and `excitedState` provide the indicated `G_\u2113` and `E_{\u2113,\u03bb}`. The binders merely quantify the integer charge and an arbitrary partition and add no contentful hypothesis."
}