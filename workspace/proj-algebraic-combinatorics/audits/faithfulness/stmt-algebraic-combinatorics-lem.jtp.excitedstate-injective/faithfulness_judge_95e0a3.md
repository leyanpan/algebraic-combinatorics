## TARGET AlgebraicCombinatorics.State.excitedState_injective (theorem) — ELABORATED SIGNATURE
∀ (ell : ℤ) {n₁ n₂ : ℕ} (mu₁ : n₁.Partition) (mu₂ : n₂.Partition),
  AlgebraicCombinatorics.State.excitedState ell mu₁ = AlgebraicCombinatorics.State.excitedState ell mu₂ →
    ⟨n₁, mu₁⟩ = ⟨n₂, mu₂⟩

Docstring: excitedState is injective: different partitions give different states.
This follows from the fact that the levels in E_{ℓ,μ} uniquely encode μ.
The excited state records exactly which electrons jumped and by how much,
so the partition can be recovered from the state.

The proof uses the fact that with sorted parts, the function i ↦ parts[i] - i
is strictly decreasing, hence injective. This means the set of excited levels
{ell - 1 - i + parts[i] | i < k} uniquely determines the sequence of parts. 

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

## PROJECT DEPENDENCY AlgebraicCombinatorics.State.excitedState (def)
ℤ → {n : ℕ} → n.Partition → AlgebraicCombinatorics.State

Body:
fun ell {n} mu =>
  { levels := AlgebraicCombinatorics.State.excitedStateLevels ell mu, finite_nonneg := ⋯, finite_negative_missing := ⋯ }

Docstring: The excited state E_{ℓ,μ} obtained from the ground state by jumping electrons
according to the partition μ.

Given a partition μ = (μ₁, μ₂, ..., μₖ) of some n, we start with the ℓ-ground state
and let the k highest electrons jump by μ₁, μ₂, ..., μₖ steps respectively. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.Level (def)
Type

Body:
ℤ

Docstring: A "level" is a half-integer, represented as p + 1/2 for some integer p.
We represent it simply by the integer p. 

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

## BASE-LIBRARY REF Sigma
{α : Type u} → (α → Type v) → Type (max u v)

Docstring: Dependent pairs, in which the second element's type depends on the value of the first element. The
type `Sigma β` is typically written `Σ a : α, β a` or `(a : α) × β a`.

Although its values are pairs, `Sigma` is sometimes known as the *dependent sum type*, since it is
the type level version of an indexed summation.


## BASE-LIBRARY REF Sigma.mk
{α : Type u} → {β : α → Type v} → (fst : α) → β fst → Sigma β

Docstring: Constructs a dependent pair.

Using this constructor in a context in which the type is not known usually requires a type
ascription to determine `β`. This is because the desired relationship between the two values can't
generally be determined automatically.


## BASE-LIBRARY REF Set
Type u → Type u

Docstring: A set is a collection of elements of some type `α`.

Although `Set` is defined as `α → Prop`, this is an implementation detail which should not be
relied on. Instead, `setOf` and membership of a set (`∈`) should be used to convert between sets
and predicates.


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

## BASE-LIBRARY REF GE.ge
{α : Type u} → [LE α] → α → α → Prop

Docstring: `a ≥ b` is an abbreviation for `b ≤ a`. 

Conventions for notations in identifiers:

 * The recommended spelling of `≥` in identifiers is `ge`.

 * The recommended spelling of `>=` in identifiers is `ge` (prefer `≥` over `>=`).

## BASE-LIBRARY REF Int.instLEInt
LE ℤ

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNat
{n : ℕ} → OfNat ℤ n

## BASE-LIBRARY REF Membership.mem
{α : outParam (Type u)} → {γ : Type v} → [self : Membership α γ] → γ → α → Prop

Docstring: The membership relation `a ∈ s : Prop` where `a : α`, `s : γ`. 

Conventions for notations in identifiers:

 * The recommended spelling of `∈` in identifiers is `mem`.

## BASE-LIBRARY REF Set.instMembership
{α : Type u} → Membership α (Set α)

## BASE-LIBRARY REF LT.lt
{α : Type u} → [self : LT α] → α → α → Prop

Docstring: The less-than relation: `x < y` 

Conventions for notations in identifiers:

 * The recommended spelling of `<` in identifiers is `lt`.

## BASE-LIBRARY REF Int.instLTInt
LT ℤ

## BASE-LIBRARY REF Not
Prop → Prop

Docstring: `Not p`, or `¬p`, is the negation of `p`. It is defined to be `p → False`,
so if your goal is `¬p` you can use `intro h` to turn the goal into
`h : p ⊢ False`, and if you have `hn : ¬p` and `h : p` then `hn h : False`
and `(hn h).elim` will prove anything.
For more information: [Propositional Logic](https://lean-lang.org/theorem_proving_in_lean4/propositions_and_proofs.html#propositional-logic)


Conventions for notations in identifiers:

 * The recommended spelling of `¬` in identifiers is `not`.

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


## BASE-LIBRARY REF Union.union
{α : Type u} → [self : Union α] → α → α → α

Docstring: `a ∪ b` is the union of `a` and `b`. 

Conventions for notations in identifiers:

 * The recommended spelling of `∪` in identifiers is `union`.

## BASE-LIBRARY REF Set.instUnion
{α : Type u} → Union (Set α)

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
lem.jtp.excitedState-injective

\leanhelper  For fixed $\ell \in \mathbb {Z}$, the map $\lambda \mapsto E_{\ell ,\lambda }$ is injective: if $E_{\ell ,\mu _1} = E_{\ell ,\mu _2}$, then $\mu _1 = \mu _2$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.jtp.excitedstate
def.jtp.excitedState

\leanhelper  For any partition $\lambda =(\lambda _{1},\lambda _{2},\ldots ,\lambda _{k})$ and any $\ell \in \mathbb {Z}$, the \emph{excited state} $E_{\ell ,\lambda }$ is defined by starting with the $\ell $-ground state $G_{\ell }$ and then successively letting the $k$ electrons at the highest levels jump $\lambda _{1},\lambda _{2},\ldots ,\lambda _{k}$ steps to the right, respectively: 

\[  E_{\ell ,\lambda }=\left\{  \text{all levels }<\ell -k\right\}  \cup \left\{  \ell -i+\tfrac {1}{2}+\lambda _{i}\  \mid \  i\in \{ 1,\ldots ,k\} \right\} .  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.jtp.groundstate
def.jtp.groundState

\leanhelper  For $\ell \in \mathbb {Z}$, the \emph{$\ell $-ground state} is 

\[  G_{\ell }:=\left\{  \text{all levels }<\ell \right\} .  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.jtp.jump
def.jtp.jump

\leanhelper  If $S$ is a state, $p\in S$, and $q$ is a positive integer such that $p+q\notin S$, then the state 

\[  \operatorname {jump}_{p,q}S:=\left( S\setminus \left\{  p\right\}  \right) \cup \left\{  p+q\right\}   \]

 is said to be obtained from $S$ by letting the electron at level $p$ \emph{jump} $q$ steps to the right.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.jtp.state
def.jtp.state

\leanhelper  A \emph{level} is a number of the form $p+\frac{1}{2}$ with $p\in \mathbb {Z}$. A \emph{state} is a set of levels that contains all but finitely many negative levels, and only finitely many positive levels. 

For any state $S$, we define: 

\begin{itemize} \item the \emph{energy} of $S$ to be 

\[  \operatorname {energy}S:=\sum _{\substack {p>0;\\ p\in S}}2p -\sum _{\substack {p<0;\\ p\notin S}}2p \in \mathbb {N};  \]

\item the \emph{particle number} of $S$ to be 

\[  \operatorname {parnum}S:=\left(\text{\#  of positive levels in } S\right) -\left(\text{\#  of negative levels not in } S\right)\in \mathbb {Z}.  \]

\end{itemize}

## VERDICT
{
  "verdict": "faithful",
  "justification": "The blueprint says: \u201cFor fixed \u2113 \u2208 \u2124, the map \u03bb \u21a6 E_{\u2113,\u03bb} is injective: if E_{\u2113,\u03bc\u2081} = E_{\u2113,\u03bc\u2082}, then \u03bc\u2081 = \u03bc\u2082.\u201d The Lean signature quantifies `\u2200 (ell : \u2124) {n\u2081 n\u2082 : \u2115} (mu\u2081 : n\u2081.Partition) (mu\u2082 : n\u2082.Partition)` and concludes from `excitedState ell mu\u2081 = excitedState ell mu\u2082` that `\u27e8n\u2081, mu\u2081\u27e9 = \u27e8n\u2082, mu\u2082\u27e9`. The dependent-pair equality is the appropriate encoding of equality between partitions whose partitioned integers may initially differ; it establishes both `n\u2081 = n\u2082` and equality of the corresponding partitions. The dependency `excitedStateLevels` also matches the informal formula under the integer representation of half-integer levels: zero-based index `i` gives `ell - 1 - i + parts[i]`, corresponding to the informal one-based `ell - i + 1/2 + \u03bb\u1d62`. There are no added mathematical hypotheses or narrowed quantifiers."
}