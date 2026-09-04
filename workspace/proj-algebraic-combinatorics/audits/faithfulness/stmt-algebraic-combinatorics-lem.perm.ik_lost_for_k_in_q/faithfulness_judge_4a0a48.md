## TARGET Equiv.Perm.ik_lost_for_k_in_Q (theorem) — ELABORATED SIGNATURE
∀ {n : ℕ} (σ : Equiv.Perm (Fin n)) (i j k : Fin n),
  k ∈ σ.setQ i j → (i, k) ∈ σ.inversions \ (σ * Equiv.swap i j).inversions

Docstring: For k ∈ Q: (i, k) is a lost inversion. 

## PROJECT DEPENDENCY Equiv.Perm.setQ (def)
{n : ℕ} → Equiv.Perm (Fin n) → Fin n → Fin n → Finset (Fin n)

Body:
fun {n} σ i j => {k | i < k ∧ k < j ∧ σ j < σ k ∧ σ k < σ i}

Docstring: The set Q from Proposition prop.perm.lisitij:
Q = {k ∈ {i+1, ..., j-1} | σ(i) > σ(k) > σ(j)}
This counts elements between i and j whose images are strictly between σ(j) and σ(i). 

## PROJECT DEPENDENCY Equiv.Perm.inversions (def)
{n : ℕ} → Equiv.Perm (Fin n) → Finset (Fin n × Fin n)

Body:
fun {n} σ => {p | p.1 < p.2 ∧ σ p.2 < σ p.1}

Docstring: The set of inversions of a permutation. 

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

## BASE-LIBRARY REF Prod
Type u → Type v → Type (max u v)

Docstring: The product type, usually written `α × β`. Product types are also called pair or tuple types.
Elements of this type are pairs in which the first element is an `α` and the second element is a
`β`.

Products nest to the right, so `(x, y, z) : α × β × γ` is equivalent to `(x, (y, z)) : α × (β × γ)`.


Conventions for notations in identifiers:

 * The recommended spelling of `×` in identifiers is `Prod`.

## BASE-LIBRARY REF SDiff.sdiff
{α : Type u} → [self : SDiff α] → α → α → α

Body:
fun α [self : SDiff α] => self.1

Docstring: `a \ b` is the set difference of `a` and `b`,
consisting of all elements in `a` that are not in `b`.


Conventions for notations in identifiers:

 * The recommended spelling of `\` in identifiers is `sdiff`.

## BASE-LIBRARY REF Finset.instSDiff
{α : Type u_1} → [DecidableEq α] → SDiff (Finset α)

Body:
fun {α} [DecidableEq α] => { sdiff := fun s₁ s₂ => { val := s₁.val - s₂.val, nodup := ⋯ } }

Docstring: `s \ t` is the set consisting of the elements of `s` that are not in `t`. 

## BASE-LIBRARY REF instDecidableEqProd.match_3
{α : Type u_1} →
  {β : Type u_2} → (motive : α × β → Sort u_3) → (x : α × β) → ((a' : α) → (b' : β) → motive (a', b')) → motive x

Body:
fun {α} {β} motive x h_1 => Prod.casesOn x fun fst snd => h_1 fst snd

## BASE-LIBRARY REF instDecidableEqProd.match_1
{β : Type u_1} →
  (b b' : β) →
    (motive : Decidable (b = b') → Sort u_2) →
      (x : Decidable (b = b')) →
        ((e₂ : b = b') → motive (isTrue e₂)) → ((n₂ : ¬b = b') → motive (isFalse n₂)) → motive x

Body:
fun {β} b b' motive x h_1 h_2 => Decidable.casesOn x (fun h => h_2 h) fun h => h_1 h

## BASE-LIBRARY REF decEq
{α : Sort u} → [inst : DecidableEq α] → (a b : α) → Decidable (a = b)

Body:
fun {α} [inst : DecidableEq α] a b => inst a b

Docstring: Checks whether two terms of a type are equal using the type's `DecidableEq` instance.


## BASE-LIBRARY REF Decidable.isTrue
{p : Prop} → p → Decidable p

Docstring: Proves that `p` is decidable by supplying a proof of `p` 

## BASE-LIBRARY REF instDecidableEqProd._proof_1
∀ {α : Type u_2} {β : Type u_1} (a : α) (b : β) (a' : α) (b' : β), a = a' → b = b' → (a, b) = (a', b')

## BASE-LIBRARY REF Decidable.isFalse
{p : Prop} → ¬p → Decidable p

Docstring: Proves that `p` is decidable by supplying a proof of `¬p` 

## BASE-LIBRARY REF instDecidableEqProd._proof_2
∀ {α : Type u_2} {β : Type u_1} (a : α) (b : β) (a' : α) (b' : β), ¬b = b' → (a, b) = (a', b') → False

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


## BASE-LIBRARY REF Fin.eq_of_val_eq
∀ {n : ℕ} {i j : Fin n}, ↑i = ↑j → i = j

## BASE-LIBRARY REF instDecidableEqFin._proof_1
∀ (n : ℕ) (i j : Fin n), ¬↑i = ↑j → i = j → False

## BASE-LIBRARY REF Mul
Type u → Type u

Docstring: The homogeneous version of `HMul`: `a * b : α` where `a b : α`. 

## BASE-LIBRARY REF Mul.mul
{α : Type u} → [self : Mul α] → α → α → α

Body:
fun α [self : Mul α] => self.1

Docstring: `a * b` computes the product of `a` and `b`. See `HMul`. 

## BASE-LIBRARY REF Equiv.Perm.instMul
{α : Type u_4} → Mul (Equiv.Perm α)

Body:
fun {α} => { mul := fun f g => Equiv.trans g f }

Characterization: `(σ * τ) x = σ (τ x)`: multiplication is composition, right factor first (`Equiv.Perm.coe_mul`).

## BASE-LIBRARY REF Equiv.trans
{α : Sort u} → {β : Sort v} → {γ : Sort w} → α ≃ β → β ≃ γ → α ≃ γ

Body:
fun {α} {β} {γ} e₁ e₂ => { toFun := ⇑e₂ ∘ ⇑e₁, invFun := ⇑e₁.symm ∘ ⇑e₂.symm, left_inv := ⋯, right_inv := ⋯ }

Docstring: Composition of equivalences `e₁ : α ≃ β` and `e₂ : β ≃ γ`. 

## BASE-LIBRARY REF Equiv.swap
{α : Sort u_1} → [DecidableEq α] → α → α → Equiv.Perm α

Body:
fun {α} [DecidableEq α] a b =>
  { toFun := Equiv.swapCore a b, invFun := Equiv.swapCore a b, left_inv := ⋯, right_inv := ⋯ }

Docstring: `swap a b` is the permutation that swaps `a` and `b` and
leaves other values as is. 

## BASE-LIBRARY REF Finset.filter
{α : Type u_1} → (p : α → Prop) → [DecidablePred p] → Finset α → Finset α

Body:
fun {α} p [DecidablePred p] s => { val := Multiset.filter p s.val, nodup := ⋯ }

Docstring: `Finset.filter p s` is the set of elements of `s` that satisfy `p`.

For example, one can use `s.filter (· ∈ t)` to get the intersection of `s` with `t : Set α`
as a `Finset α` (when a `DecidablePred (· ∈ t)` instance is available). 

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

## BASE-LIBRARY REF instDecidableAnd.match_1
{q : Prop} →
  (motive : Decidable q → Sort u_1) →
    (dq : Decidable q) → ((hq : q) → motive (isTrue hq)) → ((hq : ¬q) → motive (isFalse hq)) → motive dq

Body:
fun {q} motive dq h_1 h_2 => Decidable.casesOn dq (fun h => h_2 h) fun h => h_1 h

## BASE-LIBRARY REF And.intro
∀ {a b : Prop}, a → b → a ∧ b

Docstring: `And.intro : a → b → a ∧ b` is the constructor for the And operation. 

## BASE-LIBRARY REF instDecidableAnd._proof_1
∀ {p q : Prop}, ¬q → p ∧ q → False

## BASE-LIBRARY REF instDecidableAnd._proof_2
∀ {p q : Prop}, ¬p → p ∧ q → False

## BASE-LIBRARY REF Fin.decLt
{n : ℕ} → (a b : Fin n) → Decidable (a < b)

Body:
fun {n} a b => (↑a).decLt ↑b

## BASE-LIBRARY REF Nat.decLt
(n m : ℕ) → Decidable (n < m)

Body:
fun n m => n.succ.decLe m

Docstring: A decision procedure for strict inequality of natural numbers, usually accessed via the
`DecidableLT Nat` instance.

Examples:
 * `(if 3 < 4 then "yes" else "no") = "yes"`
 * `(if 4 < 4 then "yes" else "no") = "no"`
 * `(if 6 < 4 then "yes" else "no") = "no"`
 * `show 5 < 12 by decide`


## BASE-LIBRARY REF Finset.univ
{α : Type u_1} → [Fintype α] → Finset α

Body:
fun {α} [Fintype α] => Fintype.elems

Docstring: `univ` is the universal finite set of type `Finset α` implied from
the assumption `Fintype α`. 

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

## BASE-LIBRARY REF Fintype
Type u_4 → Type u_4

Docstring: `Fintype α` means that `α` is finite, i.e. there are only
finitely many distinct elements of type `α`. The evidence of this
is a finset `elems` (a list up to permutation without duplicates),
together with a proof that everything of type `α` is in the list. 

## BASE-LIBRARY REF SProd.sprod
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : SProd α β γ] → α → β → γ

Body:
fun α β {γ} [self : SProd α β γ] => self.1

Docstring: The Cartesian product `s ×ˢ t` is the set of `(a, b)` such that `a ∈ s` and `b ∈ t`. 

## BASE-LIBRARY REF Finset.instSProd
{α : Type u_1} → {β : Type u_2} → SProd (Finset α) (Finset β) (Finset (α × β))

Body:
fun {α} {β} => { sprod := Finset.product }

## BASE-LIBRARY REF instFintypeProd._proof_1
∀ (α : Type u_1) (β : Type u_2) [inst : Fintype α] [inst_1 : Fintype β] (x : α × β), x ∈ Finset.univ ×ˢ Finset.univ

## INFORMAL STATEMENT
lem.perm.ik_lost_for_k_in_Q

\leanhelper  For $k \in Q$: the pair $(i, k)$ is a lost inversion. Before the swap, $\sigma (i) > \sigma (k)$ so $(i,k)$ is an inversion. After the swap, $(\sigma t_{i,j})(i) = \sigma (j) < \sigma (k)$, so it is not.

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.setq
def.perm.setQ

\leanhelper  The set $Q$ from Proposition~ \ref{prop.perm.lisitij}: $Q = \{ k \in \{ i+1, \ldots , j-1\}  \mid \sigma (j) < \sigma (k) < \sigma (i)\} $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.sn-iven
def.perm.Sn-iven

Let $n \in \mathbb {Z}$. Then, $[n]$ shall mean the set $\{ 1, 2, \ldots , n\} $. This is an $n$-element set if $n \ge 0$, and is an empty set if $n \le 0$. 

The symmetric group $S_{[n]}$ (consisting of all permutations of $[n]$) will be denoted $S_n$ and called the $n$\emph{-th symmetric group}. Its size is $n!$ (when $n \ge 0$).

## VERDICT
{
  "verdict": "faithful",
  "discrepancies": [],
  "justification": "Unfolding `setQ`, the hypothesis `k \u2208 \u03c3.setQ i j` is exactly `i < k \u2227 k < j \u2227 \u03c3 j < \u03c3 k \u2227 \u03c3 k < \u03c3 i`, matching the blueprint\u2019s `k \u2208 Q`. Unfolding `inversions` and finset difference, the conclusion says `(i,k)` is an inversion of `\u03c3` and is not an inversion of `\u03c3 * Equiv.swap i j`. Since permutation multiplication satisfies `(\u03c3 * \u03c4) x = \u03c3 (\u03c4 x)`, the latter permutation is precisely `\u03c3 \u2218 t_{i,j}` as in the informal statement. Thus the formal conclusion exactly expresses that `(i,k)` is a lost inversion. Using `Fin n` rather than the one-based set `[n]` is a routine finite-order re-encoding and does not alter the claim."
}