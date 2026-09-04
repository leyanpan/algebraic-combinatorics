## TARGET AlgebraicCombinatorics.CauchyBinet.imageFinset (def) — ELABORATED SIGNATURE
{n : ℕ} → Equiv.Perm (Fin n) → Finset (Fin n) → Finset (Fin n)

Body:
fun {n} σ P => Finset.map { toFun := ⇑σ, inj' := ⋯ } P

Docstring: The image of a finset under a permutation.

This is definitionally equal to `PermFinset.imageFinset` (see `imageFinset_eq_permFinset`).
New code should prefer `PermFinset.imageFinset`. 

## TARGET AlgebraicCombinatorics.CauchyBinet.permsMapping (def) — ELABORATED SIGNATURE
{n : ℕ} → Finset (Fin n) → Finset (Fin n) → Finset (Equiv.Perm (Fin n))

Body:
fun {n} P Q => {σ | AlgebraicCombinatorics.CauchyBinet.imageFinset σ P = Q}

Docstring: The set of permutations that map P to Q.

This is definitionally equal to `PermFinset.permsMapping` (see `permsMapping_eq_permFinset`).
New code should prefer `PermFinset.permsMapping`. 

## TARGET AlgebraicCombinatorics.CauchyBinet.finsetSumFin (def) — ELABORATED SIGNATURE
{n : ℕ} → Finset (Fin n) → ℕ

Body:
fun {n} P => ∑ i ∈ P, ↑i

Docstring: Sum of elements in a finset of Fin n, viewed as natural numbers.
Used in the sign factor of the det(A+B) formula.

Note: This is named `finsetSumFin` to distinguish from `AlgebraicCombinatorics.QBinomialRec.finsetSumNat`,
which computes the sum of elements in a `Finset ℕ` directly.
Both compute "the sum of elements" but for different element types. 

## BASE-LIBRARY REF Equiv.Perm
Sort u_1 → Sort (max 1 u_1)

Body:
fun α => α ≃ α

Docstring: `Perm α` is the type of bijections from `α` to itself. 

## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


## BASE-LIBRARY REF Finset
Type u_4 → Type u_4

Docstring: `Finset α` is the type of finite sets of elements of `α`. It is implemented
as a multiset (a list up to permutation) which has no duplicate elements. 

## BASE-LIBRARY REF Finset.map
{α : Type u_1} → {β : Type u_2} → (α ↪ β) → Finset α → Finset β

Body:
fun {α} {β} f s => { val := Multiset.map (⇑f) s.val, nodup := ⋯ }

Docstring: When `f` is an embedding of `α` in `β` and `s` is a finset in `α`, then `s.map f` is the image
finset in `β`. The embedding condition guarantees that there are no duplicates in the image. 

## BASE-LIBRARY REF EquivLike
Sort u_1 → outParam (Sort u_2) → outParam (Sort u_3) → Sort (max (max (max 1 u_1) u_2) u_3)

Docstring: The class `EquivLike E α β` expresses that terms of type `E` have an
injective coercion to bijections between `α` and `β`.

Note that this does not directly extend `FunLike`, nor take `FunLike` as a parameter,
so we can state `coe_injective'` in a nicer way.

This typeclass is used in the definition of the isomorphism (or equivalence) typeclasses,
such as `ZeroEquivClass`, `MulEquivClass`, `MonoidEquivClass`, ....


## BASE-LIBRARY REF EquivLike.coe
{E : Sort u_1} → {α : outParam (Sort u_2)} → {β : outParam (Sort u_3)} → [self : EquivLike E α β] → E → α → β

Body:
fun E {α} {β} [self : EquivLike E α β] => self.1

Docstring: The coercion to a function in the forward direction. 

## BASE-LIBRARY REF EquivLike.toFunLike._proof_1
∀ {E : Sort u_3} {α : Sort u_1} {β : Sort u_2} [inst : EquivLike E α β] (e g : E),
  EquivLike.coe e = EquivLike.coe g → e = g

## BASE-LIBRARY REF Equiv.instEquivLike
{α : Sort u} → {β : Sort v} → EquivLike (α ≃ β) α β

Body:
fun {α} {β} => { coe := Equiv.toFun, inv := Equiv.invFun, left_inv := ⋯, right_inv := ⋯, coe_injective' := ⋯ }

## BASE-LIBRARY REF Equiv
Sort u_1 → Sort u_2 → Sort (max (max 1 u_1) u_2)

Docstring: `α ≃ β` is the type of functions from `α → β` with a two-sided inverse. 

## BASE-LIBRARY REF Equiv.invFun
{α : Sort u_1} → {β : Sort u_2} → α ≃ β → β → α

Body:
fun α β self => self.2

Docstring: The backward map of an equivalence.

Do NOT use `e.invFun` directly. Use the coercion of `e.symm` instead. 

## BASE-LIBRARY REF Equiv.left_inv
∀ {α : Sort u_1} {β : Sort u_2} (self : α ≃ β), Function.LeftInverse self.invFun self.toFun

## BASE-LIBRARY REF Equiv.right_inv
∀ {α : Sort u_1} {β : Sort u_2} (self : α ≃ β), Function.RightInverse self.invFun self.toFun

## BASE-LIBRARY REF Equiv.instEquivLike._proof_1
∀ {α : Sort u_1} {β : Sort u_2} (e₁ e₂ : α ≃ β), e₁.toFun = e₂.toFun → e₁.invFun = e₂.invFun → e₁ = e₂

## BASE-LIBRARY REF Finset.filter
{α : Type u_1} → (p : α → Prop) → [DecidablePred p] → Finset α → Finset α

Body:
fun {α} p [DecidablePred p] s => { val := Multiset.filter p s.val, nodup := ⋯ }

Docstring: `Finset.filter p s` is the set of elements of `s` that satisfy `p`.

For example, one can use `s.filter (· ∈ t)` to get the intersection of `s` with `t : Set α`
as a `Finset α` (when a `DecidablePred (· ∈ t)` instance is available). 

## BASE-LIBRARY REF Finset.decidableEq
{α : Type u_1} → [DecidableEq α] → DecidableEq (Finset α)

Body:
fun {α} [DecidableEq α] x x_1 =>
  match x, x_1 with
  | x, x_2 => decidable_of_iff (x.val = x_2.val) ⋯

## BASE-LIBRARY REF Finset.decidableEq.match_1
{α : Type u_1} →
  (motive : Finset α → Finset α → Sort u_2) → (x x_1 : Finset α) → ((x x_2 : Finset α) → motive x x_2) → motive x x_1

Body:
fun {α} motive x x_1 h_1 => h_1 x x_1

## BASE-LIBRARY REF decidable_of_iff
{b : Prop} → (a : Prop) → (a ↔ b) → [Decidable a] → Decidable b

Body:
fun {b} a h [Decidable a] => decidable_of_decidable_of_iff h

Docstring: Transfer decidability of `a` to decidability of `b`, if the propositions are equivalent.
**Important**: this function should be used instead of `rw` on `Decidable b`, because the
kernel will get stuck reducing the usage of `propext` otherwise,
and `decide` will not work. 

## BASE-LIBRARY REF Multiset
Type u → Type u

Body:
fun α => Quotient (List.isSetoid α)

Docstring: `Multiset α` is the quotient of `List α` by list permutation. The result
is a type of finite sets with duplicates allowed. 

## BASE-LIBRARY REF Finset.val
{α : Type u_4} → Finset α → Multiset α

Body:
fun α self => self.1

Docstring: The underlying multiset 

## BASE-LIBRARY REF Finset.val_inj
∀ {α : Type u_1} {s t : Finset α}, s.val = t.val ↔ s = t

## BASE-LIBRARY REF Multiset.decidableEq
{α : Type u_1} → [DecidableEq α] → DecidableEq (Multiset α)

Body:
fun {α} [DecidableEq α] x x_1 =>
  match x, x_1 with
  | s₁, s₂ => Quotient.recOnSubsingleton₂ s₁ s₂ fun x x_2 => decidable_of_iff' (x ≈ x_2) ⋯

## BASE-LIBRARY REF instDecidableEqFin.match_1
(n : ℕ) →
  (i j : Fin n) →
    (motive : Decidable (↑i = ↑j) → Sort u_1) →
      (x : Decidable (↑i = ↑j)) → ((h : ↑i = ↑j) → motive (isTrue h)) → ((h : ¬↑i = ↑j) → motive (isFalse h)) → motive x

Body:
fun n i j motive x h_1 h_2 => Decidable.casesOn x (fun h => h_2 h) fun h => h_1 h

## BASE-LIBRARY REF Fin.val
{n : ℕ} → Fin n → ℕ

Body:
fun n self => self.1

Docstring: The number that is strictly less than `n`.

`Fin.val` is a coercion, so any `Fin n` can be used in a position where a `Nat` is expected.


## BASE-LIBRARY REF decEq
{α : Sort u} → [inst : DecidableEq α] → (a b : α) → Decidable (a = b)

Body:
fun {α} [inst : DecidableEq α] a b => inst a b

Docstring: Checks whether two terms of a type are equal using the type's `DecidableEq` instance.


## BASE-LIBRARY REF Decidable.isTrue
{p : Prop} → p → Decidable p

Docstring: Proves that `p` is decidable by supplying a proof of `p` 

## BASE-LIBRARY REF Fin.eq_of_val_eq
∀ {n : ℕ} {i j : Fin n}, ↑i = ↑j → i = j

## BASE-LIBRARY REF Decidable.isFalse
{p : Prop} → ¬p → Decidable p

Docstring: Proves that `p` is decidable by supplying a proof of `¬p` 

## BASE-LIBRARY REF instDecidableEqFin._proof_1
∀ (n : ℕ) (i j : Fin n), ¬↑i = ↑j → i = j → False

## BASE-LIBRARY REF Finset.univ
{α : Type u_1} → [Fintype α] → Finset α

Body:
fun {α} [Fintype α] => Fintype.elems

Docstring: `univ` is the universal finite set of type `Finset α` implied from
the assumption `Fintype α`. 

## BASE-LIBRARY REF Equiv.instFintype
{α : Type u_1} → {β : Type u_2} → [DecidableEq α] → [DecidableEq β] → [Fintype α] → [Fintype β] → Fintype (α ≃ β)

Body:
fun {α} {β} [DecidableEq α] [DecidableEq β] [Fintype α] [Fintype β] =>
  if h : Fintype.card β = Fintype.card α then
    (Fintype.truncEquivFin α).recOnSubsingleton fun eα =>
      (Fintype.truncEquivFin β).recOnSubsingleton fun eβ =>
        Fintype.ofEquiv (Equiv.Perm α) ((Equiv.refl α).equivCongr (eα.trans (Eq.recOn h eβ.symm)))
  else { elems := ∅, complete := ⋯ }

## BASE-LIBRARY REF Fintype
Type u_4 → Type u_4

Docstring: `Fintype α` means that `α` is finite, i.e. there are only
finitely many distinct elements of type `α`. The evidence of this
is a finset `elems` (a list up to permutation without duplicates),
together with a proof that everything of type `α` is in the list. 

## BASE-LIBRARY REF dite
{α : Sort u} → (c : Prop) → [h : Decidable c] → (c → α) → (¬c → α) → α

Body:
fun {α} c [h : Decidable c] t e => Decidable.casesOn h e t

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


## BASE-LIBRARY REF Fintype.card
(α : Type u_4) → [Fintype α] → ℕ

Body:
fun α [Fintype α] => Finset.univ.card

Docstring: `card α` is the number of elements in `α`, defined when `α` is a fintype. 

## BASE-LIBRARY REF Trunc.recOnSubsingleton
{α : Sort u_1} →
  {C : Trunc α → Sort u_3} →
    [∀ (a : α), Subsingleton (C (Trunc.mk a))] → (q : Trunc α) → ((a : α) → C (Trunc.mk a)) → C q

Body:
fun {α} {C} [∀ (a : α), Subsingleton (C (Trunc.mk a))] q f => Trunc.rec f ⋯ q

Docstring: A version of `Trunc.recOn` assuming the codomain is a `Subsingleton`. 

## BASE-LIBRARY REF Trunc
Sort u → Sort u

Body:
fun α => Quotient trueSetoid

Docstring: `Trunc α` is the quotient of `α` by the always-true relation. This
is related to the propositional truncation in HoTT, and is similar
in effect to `Nonempty α`, but unlike `Nonempty α`, `Trunc α` is data,
so the VM representation is the same as `α`, and so this can be used to
maintain computability. 

## BASE-LIBRARY REF Equiv.instFintype._proof_1
∀ {α : Type u_1} {β : Type u_2} [inst : Fintype α] (a : α ≃ Fin (Fintype.card α)), Subsingleton (Fintype (α ≃ β))

## BASE-LIBRARY REF Fintype.truncEquivFin
(α : Type u_4) → [DecidableEq α] → [inst : Fintype α] → Trunc (α ≃ Fin (Fintype.card α))

Body:
fun α [DecidableEq α] [Fintype α] =>
  id
    (id
      (Quot.recOnSubsingleton (motive := fun s => (∀ (x : α), x ∈ s) → s.Nodup → Trunc (α ≃ Fin s.card)) Finset.univ.val
        (fun l h nd => Trunc.mk (List.Nodup.getEquivOfForallMemList l nd h).symm) ⋯ ⋯))

Docstring: There is (computably) an equivalence between `α` and `Fin (card α)`.

Since it is not unique and depends on which permutation
of the universe list is used, the equivalence is wrapped in `Trunc` to
preserve computability.

See `Fintype.equivFin` for the noncomputable version,
and `Fintype.truncEquivFinOfCardEq` and `Fintype.equivFinOfCardEq`
for an equiv `α ≃ Fin n` given `Fintype.card α = n`.

See `Fintype.truncFinBijection` for a version without `[DecidableEq α]`.


## BASE-LIBRARY REF Equiv.instFintype._proof_2
∀ {α : Type u_2} {β : Type u_1} [inst : Fintype β] (a : β ≃ Fin (Fintype.card β)), Subsingleton (Fintype (α ≃ β))

## BASE-LIBRARY REF Fintype.ofEquiv
{β : Type u_2} → (α : Type u_4) → [Fintype α] → α ≃ β → Fintype β

Body:
fun {β} α [Fintype α] f => Fintype.ofBijective ⇑f ⋯

Docstring: If `f : α ≃ β` and `α` is a fintype, then `β` is also a fintype. 

## BASE-LIBRARY REF fintypePerm
{α : Type u_1} → [DecidableEq α] → [Fintype α] → Fintype (Equiv.Perm α)

Body:
fun {α} [DecidableEq α] [Fintype α] => { elems := permsOfFinset Finset.univ, complete := ⋯ }

Docstring: The collection of permutations of a fintype is a fintype. 

## BASE-LIBRARY REF Equiv.equivCongr
{α : Sort u} → {β : Sort v} → {γ : Sort w} → {δ : Sort u_1} → α ≃ β → γ ≃ δ → α ≃ γ ≃ (β ≃ δ)

Body:
fun {α} {β} {γ} {δ} ab cd =>
  { toFun := fun ac => (ab.symm.trans ac).trans cd, invFun := fun bd => ab.trans (bd.trans cd.symm), left_inv := ⋯,
    right_inv := ⋯ }

Docstring: If `α` is equivalent to `β` and `γ` is equivalent to `δ`, then the type of equivalences `α ≃ γ`
is equivalent to the type of equivalences `β ≃ δ`. 

## BASE-LIBRARY REF Equiv.refl
(α : Sort u_1) → α ≃ α

Body:
fun α => { toFun := id, invFun := id, left_inv := ⋯, right_inv := ⋯ }

Docstring: Any type is equivalent to itself. 

## BASE-LIBRARY REF Fin.fintype
(n : ℕ) → Fintype (Fin n)

Body:
fun n => { elems := { val := ↑(List.finRange n), nodup := ⋯ }, complete := ⋯ }

## BASE-LIBRARY REF Multiset.ofList
{α : Type u_1} → List α → Multiset α

Body:
fun {α} => Quot.mk ⇑(List.isSetoid α)

Docstring: The quotient map from `List α` to `Multiset α`. 

## BASE-LIBRARY REF List.finRange
(n : ℕ) → List (Fin n)

Body:
fun n => List.ofFn fun i => i

Docstring: Lists all elements of `Fin n` in order, starting at `0`.

Examples:
* `List.finRange 0 = ([] : List (Fin 0))`
* `List.finRange 2 = ([0, 1] : List (Fin 2))`


## BASE-LIBRARY REF List.nodup_finRange
∀ (n : ℕ), (List.finRange n).Nodup

## BASE-LIBRARY REF List.mem_finRange
∀ {n : ℕ} (x : Fin n), x ∈ List.finRange n

## BASE-LIBRARY REF Finset.sum
{ι : Type u_1} → {M : Type u_3} → [AddCommMonoid M] → Finset ι → (ι → M) → M

Body:
fun {ι} {M} [AddCommMonoid M] s f => (Multiset.map f s.val).sum

Docstring: `∑ x ∈ s, f x` is the sum of `f x` as `x` ranges over the elements
of the finite set `s`.

When the index type is a `Fintype`, the notation `∑ x, f x`, is a shorthand for
`∑ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF Nat.instAddCommMonoid
AddCommMonoid ℕ

Body:
inferInstance

## BASE-LIBRARY REF AddCommMonoid
Type u → Type u

Docstring: An additive commutative monoid is an additive monoid with commutative `(+)`. 

## BASE-LIBRARY REF Nat.instAddCancelCommMonoid
AddCancelCommMonoid ℕ

Body:
{ add := Nat.add, add_assoc := Nat.add_assoc, zero := Nat.zero, zero_add := Nat.zero_add, add_zero := Nat.add_zero,
  nsmul := fun m n => m * n, nsmul_zero := Nat.zero_mul, nsmul_succ := Nat.succ_mul, add_comm := Nat.add_comm,
  toIsLeftCancelAdd := Nat.instAddCancelCommMonoid._proof_1 }

## INFORMAL STATEMENT
Subset sum and permutation sets

\leanhelper  For a subset $P\subseteq [n]$, define $\operatorname {sum}(P) = \sum _{i\in P} i$. 

For subsets $P,Q\subseteq [n]$, define $\operatorname {Perm}(P,Q) = \{ \sigma \in S_n : \sigma (P)=Q\} $ where $\sigma (P) = \{ \sigma (i) \mid i \in P\} $ denotes the image of $P$ under $\sigma $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-conv.det.sum-compl
conv.det.sum-compl

For any subset $I$ of $[n]$, we write $\widetilde{I} = [n] \setminus I$ for its complement, and $\operatorname {sum} S = \sum _{s \in S} s$ for any finite set $S$ of integers.

## VERDICT
{
  "verdict": "unclear",
  "discrepancies": [],
  "justification": "The package does not define the informal notation `[n]` or specify whether its elements are `0,\u2026,n\u22121` or `1,\u2026,n`. The formal side uses `Fin n`, whose elements are natural numbers strictly below `n`, and `finsetSumFin` has body `fun {n} P => \u2211 i \u2208 P, \u2191i`. If `[n] = {0,\u2026,n\u22121}`, all three definitions directly match the blueprint: `imageFinset` is the image under a permutation, `permsMapping` filters all permutations by that image equality, and `finsetSumFin` is the stated subset sum. If `[n] = {1,\u2026,n}`, the sum under the natural correspondence `i \u21a6 i+1` would instead be `\u2211 i \u2208 P, (\u2191i+1)`, so the formal sum differs by `|P|`. A definition of `[n]` (or an explicit indexing convention) is therefore needed to decide faithfulness."
}