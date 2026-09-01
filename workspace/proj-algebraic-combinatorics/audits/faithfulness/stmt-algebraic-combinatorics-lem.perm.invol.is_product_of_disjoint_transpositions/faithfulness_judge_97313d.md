## TARGET AlgebraicCombinatorics.involution_is_product_of_disjoint_transpositions (theorem) — ELABORATED SIGNATURE
∀ {X : Type u_1} [inst : DecidableEq X] [Fintype X] {σ : Equiv.Perm X},
  AlgebraicCombinatorics.IsInvolution σ →
    ∃ pairs,
      List.Pairwise (fun p q => p.1 ≠ q.1 ∧ p.1 ≠ q.2 ∧ p.2 ≠ q.1 ∧ p.2 ≠ q.2) pairs ∧
        (∀ p ∈ pairs, p.1 ≠ p.2) ∧ σ = (List.map (fun p => AlgebraicCombinatorics.transposition p.1 p.2) pairs).prod

Docstring: An involution of a finite set is a product of disjoint transpositions.
(Stated informally in the source) 

## PROJECT DEPENDENCY AlgebraicCombinatorics.IsInvolution (def)
{X : Type u_1} → Equiv.Perm X → Prop

Body:
fun {X} σ => σ * σ = 1

Docstring: A permutation is an involution if `σ ∘ σ = id`. (def.perm.invol)

From the textbook:
> An *involution* of X means a map f: X → X that satisfies f ∘ f = id.
> Clearly, an involution is always a permutation, and equals its own inverse.

Equivalent characterizations:
- `IsInvolution σ ↔ σ * σ = 1` (definition)
- `IsInvolution σ ↔ σ⁻¹ = σ` (see `isInvolution_iff_eq_inv`)
- `IsInvolution σ ↔ Function.Involutive σ` (see `isInvolution_iff_involutive`)
- `IsInvolution σ ↔ ∀ x, σ (σ x) = x` (see `isInvolution_iff_forall`)


## PROJECT DEPENDENCY AlgebraicCombinatorics.transposition (def)
{X : Type u_1} → [DecidableEq X] → X → X → Equiv.Perm X

Body:
fun {X} [DecidableEq X] i j => Equiv.swap i j

Docstring: The transposition swapping `i` and `j`. In Mathlib, this is `Equiv.swap i j`.
(def.perm.tij)

A transposition `t_{i,j}` is the permutation of `X` that:
- sends `i` to `j` (see `transposition_apply_left`)
- sends `j` to `i` (see `transposition_apply_right`)
- leaves all other elements unchanged (see `transposition_apply_of_ne_of_ne`) 

## BASE-LIBRARY REF DecidableEq
Sort u → Sort (max 1 u)

Docstring: Propositional equality is `Decidable` for all elements of a type.

In other words, an instance of `DecidableEq α` is a means of deciding the proposition `a = b` is
for all `a b : α`.


## BASE-LIBRARY REF Fintype
Type u_4 → Type u_4

Docstring: `Fintype α` means that `α` is finite, i.e. there are only
finitely many distinct elements of type `α`. The evidence of this
is a finset `elems` (a list up to permutation without duplicates),
together with a proof that everything of type `α` is in the list. 

## BASE-LIBRARY REF Equiv.Perm
Sort u_1 → Sort (max 1 u_1)

Docstring: `Perm α` is the type of bijections from `α` to itself. 

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


## BASE-LIBRARY REF Prod
Type u → Type v → Type (max u v)

Docstring: The product type, usually written `α × β`. Product types are also called pair or tuple types.
Elements of this type are pairs in which the first element is an `α` and the second element is a
`β`.

Products nest to the right, so `(x, y, z) : α × β × γ` is equivalent to `(x, (y, z)) : α × (β × γ)`.


Conventions for notations in identifiers:

 * The recommended spelling of `×` in identifiers is `Prod`.

## BASE-LIBRARY REF And
Prop → Prop → Prop

Docstring: `And a b`, or `a ∧ b`, is the conjunction of propositions. It can be
constructed and destructed like a pair: if `ha : a` and `hb : b` then
`⟨ha, hb⟩ : a ∧ b`, and if `h : a ∧ b` then `h.left : a` and `h.right : b`.


Conventions for notations in identifiers:

 * The recommended spelling of `∧` in identifiers is `and`.

 * The recommended spelling of `/\` in identifiers is `and` (prefer `∧` over `/\`).

## BASE-LIBRARY REF List.Pairwise
{α : Type u} → (α → α → Prop) → List α → Prop

Docstring: Each element of a list is related to all later elements of the list by `R`.

`Pairwise R l` means that all the elements of `l` with earlier indexes are `R`-related to all the
elements with later indexes.

For example, `Pairwise (· ≠ ·) l` asserts that `l` has no duplicates, and `Pairwise (· < ·) l`
asserts that `l` is (strictly) sorted.

Examples:
 * `Pairwise (· < ·) [1, 2, 3] ↔ (1 < 2 ∧ 1 < 3) ∧ 2 < 3`
 * `Pairwise (· = ·) [1, 2, 3] = False`
 * `Pairwise (· ≠ ·) [1, 2, 3] = True`


## BASE-LIBRARY REF Ne
{α : Sort u} → α → α → Prop

Docstring: `a ≠ b`, or `Ne a b` is defined as `¬ (a = b)` or `a = b → False`,
and asserts that `a` and `b` are not equal.


Conventions for notations in identifiers:

 * The recommended spelling of `≠` in identifiers is `ne`.

## BASE-LIBRARY REF Prod.fst
{α : Type u} → {β : Type v} → α × β → α

Docstring: The first element of a pair. 

## BASE-LIBRARY REF Prod.snd
{α : Type u} → {β : Type v} → α × β → β

Docstring: The second element of a pair. 

## BASE-LIBRARY REF Membership.mem
{α : outParam (Type u)} → {γ : Type v} → [self : Membership α γ] → γ → α → Prop

Docstring: The membership relation `a ∈ s : Prop` where `a : α`, `s : γ`. 

Conventions for notations in identifiers:

 * The recommended spelling of `∈` in identifiers is `mem`.

## BASE-LIBRARY REF List.instMembership
{α : Type u} → Membership α (List α)

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

## BASE-LIBRARY REF List.prod
{α : Type u_1} → [Mul α] → [One α] → List α → α

Docstring: Computes the product of the elements of a list.

Examples:

[a, b, c].prod = a * (b * (c * 1))
[2, 3, 5].prod = 30


## BASE-LIBRARY REF Equiv.Perm.instMul
{α : Type u_4} → Mul (Equiv.Perm α)

## BASE-LIBRARY REF Equiv.Perm.instOne
{α : Type u_4} → One (Equiv.Perm α)

## BASE-LIBRARY REF List.map
{α : Type u_1} → {β : Type u_2} → (α → β) → List α → List β

Docstring: Applies a function to each element of the list, returning the resulting list of values.

`O(|l|)`.

Examples:
* `[a, b, c].map f = [f a, f b, f c]`
* `[].map Nat.succ = []`
* `["one", "two", "three"].map (·.length) = [3, 3, 5]`
* `["one", "two", "three"].map (·.reverse) = ["eno", "owt", "eerht"]`


## BASE-LIBRARY REF HMul.hMul
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HMul α β γ] → α → β → γ

Docstring: `a * b` computes the product of `a` and `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `*` in identifiers is `mul`.

## BASE-LIBRARY REF instHMul
{α : Type u_1} → [Mul α] → HMul α α α

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF One.toOfNat1
{α : Type u_1} → [One α] → OfNat α 1

## BASE-LIBRARY REF Equiv.swap
{α : Sort u_1} → [DecidableEq α] → α → α → Equiv.Perm α

Docstring: `swap a b` is the permutation that swaps `a` and `b` and
leaves other values as is. 

## INFORMAL STATEMENT
lem.perm.invol.is_product_of_disjoint_transpositions

\leanhelper  Every involution of a finite set is a product of pairwise disjoint transpositions.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-conv-2eb59533
conv-2eb59533

In the Lean formalization, we use $\operatorname {Fin} n = \{ 0, 1, \ldots , n-1\} $ instead of the textbook’s $[n] = \{ 1, 2, \ldots , n\} $. Both are $n$-element sets, so their symmetric groups are isomorphic. Permutations are represented by the type of bijections $X \to X$ (denoted $\operatorname {Equiv.Perm}\,  X$ in Lean), which is a group under composition. Composition $\alpha \beta $ is the group multiplication $\alpha * \beta $, sending $x$ to $\alpha (\beta (x))$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.invol
def.perm.invol

Let $X$ be a set. An \emph{involution} of $X$ means a map $f : X \to X$ that satisfies $f \circ f = \operatorname {id}$. Clearly, an involution is always a permutation, and equals its own inverse.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.perm
def.perm.perm

Let $X$ be a set. 

\textbf{(a)} A \emph{permutation} of $X$ means a bijection from $X$ to $X$. 

\textbf{(b)} It is known that the set of all permutations of $X$ is a group under composition. This group is called the \emph{symmetric group} of $X$, and is denoted by $S_X$. Its neutral element is the identity map $\operatorname {id}_X : X \to X$. Its size is $|X|!$ when $X$ is finite. 

\textbf{(c)} As usual in group theory, we will write $\alpha \beta $ for the composition $\alpha \circ \beta $ when $\alpha , \beta \in S_X$. This is the map that sends each $x \in X$ to $\alpha (\beta (x))$. 

\textbf{(d)} If $\alpha \in S_X$ and $i \in \mathbb {Z}$, then $\alpha ^i$ shall denote the $i$-th power of $\alpha $ in the group $S_X$. Note that $\alpha ^i = \underbrace{\alpha \circ \alpha \circ \cdots \circ \alpha }_{i\text{ times}}$ if $i \ge 0$. Also, $\alpha ^0 = \operatorname {id}_X$. Also, $\alpha ^{-1}$ is the inverse of $\alpha $ in the group $S_X$, that is, the inverse of the map $\alpha $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.tij
def.perm.tij

Let $i$ and $j$ be two distinct elements of a set $X$. 

Then, the \emph{transposition} $t_{i,j}$ is the permutation of $X$ that sends $i$ to $j$, sends $j$ to $i$, and leaves all other elements of $X$ unchanged.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The blueprint says, \u201cEvery involution of a finite set is a product of pairwise disjoint transpositions.\u201d The formal binders `\u2200 {X : Type u_1} ... [Fintype X] {\u03c3 : Equiv.Perm X}, IsInvolution \u03c3 \u2192` quantify over permutations of an arbitrary finite type, and `IsInvolution \u03c3` unfolds to `\u03c3 * \u03c3 = 1`, matching the defined condition `f \u2218 f = id`. The witness `pairs` represents the transpositions; `(\u2200 p \u2208 pairs, p.1 \u2260 p.2)` ensures each `Equiv.swap p.1 p.2` is a genuine transposition, while `List.Pairwise (fun p q => p.1 \u2260 q.1 \u2227 p.1 \u2260 q.2 \u2227 p.2 \u2260 q.1 \u2227 p.2 \u2260 q.2) pairs` says distinct listed transpositions have disjoint supports. Finally, `\u03c3 = (List.map ... pairs).prod` states the required product decomposition. The additional `[DecidableEq X]` is an encoding requirement of `transposition`, whose body uses `Equiv.swap`; it is not a mathematically substantive restriction on the finite-set statement."
}