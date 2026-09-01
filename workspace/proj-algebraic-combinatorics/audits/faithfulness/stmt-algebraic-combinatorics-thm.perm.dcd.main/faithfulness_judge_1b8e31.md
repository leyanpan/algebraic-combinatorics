## TARGET AlgebraicCombinatorics.CycleDecomposition.exists_dcd (theorem) — ELABORATED SIGNATURE
∀ {α : Type u_1} [DecidableEq α] [Fintype α] (σ : Equiv.Perm α),
  ∃ cycs,
    (∀ c ∈ cycs, c.IsCycle) ∧
      (↑cycs).Pairwise Equiv.Perm.Disjoint ∧ ∃ (h : (↑cycs).Pairwise Commute), cycs.noncommProd id h = σ

Docstring: Existence of DCD: Every permutation is a product of disjoint cycles.
This is Theorem \ref{thm.perm.dcd.main} (a). 

## TARGET AlgebraicCombinatorics.CycleDecomposition.dcd_unique_cycleType (theorem) — ELABORATED SIGNATURE
∀ {α : Type u_1} [inst : DecidableEq α] [inst_1 : Fintype α] (σ : Equiv.Perm α) (cycs : Finset (Equiv.Perm α)),
  (∀ c ∈ cycs, c.IsCycle) →
    (↑cycs).Pairwise Equiv.Perm.Disjoint →
      (∃ (h : (↑cycs).Pairwise Commute), cycs.noncommProd id h = σ) →
        Multiset.map (fun c => c.support.card) cycs.val = σ.cycleType

Docstring: Any two DCDs of the same permutation have the same cycle type (as a multiset of lengths).
This captures the essence of Theorem \ref{thm.perm.dcd.main} (b): the cycles of a DCD are
uniquely determined up to swapping and rotation, hence they have the same lengths.

In Mathlib's formalization, there is a canonical DCD (`cycleFactorsFinset`), so this is trivial:
any DCD must produce the same set of cycles as `cycleFactorsFinset`, just possibly listed
in a different order or with different rotations. 

## TARGET AlgebraicCombinatorics.CycleDecomposition.canonicalDcd_exists_unique (theorem) — ELABORATED SIGNATURE
∀ {α : Type u_1} [inst : DecidableEq α] [Fintype α] [inst_2 : LinearOrder α] [inst_3 : Inhabited α] (σ : Equiv.Perm α),
  ∃! cycleReps,
    (∀ l ∈ cycleReps, l ≠ []) ∧
      cycleReps.flatten.Nodup ∧
        (∀ (x : α), x ∈ cycleReps.flatten) ∧
          (∀ l ∈ cycleReps, ∀ x ∈ l, l.head! ≤ x) ∧
            List.Pairwise (fun l1 l2 => l1.head! > l2.head!) cycleReps ∧
              AlgebraicCombinatorics.CycleDecomposition.dcdListToPerm cycleReps = σ

## PROJECT DEPENDENCY AlgebraicCombinatorics.CycleDecomposition.dcdListToPerm (def)
{α : Type u_1} → [DecidableEq α] → List (List α) → Equiv.Perm α

Body:
fun {α} [DecidableEq α] cycleReps => (List.map List.formPerm cycleReps).prod

Docstring: Convert a list of lists representing cycles to a permutation by taking the product
of the cycle permutations. Each list `[a₁, a₂, ..., aₖ]` represents the k-cycle
`cyc_{a₁, a₂, ..., aₖ}` that sends a₁ → a₂ → ... → aₖ → a₁. 

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


## BASE-LIBRARY REF Finset
Type u_4 → Type u_4

Docstring: `Finset α` is the type of finite sets of elements of `α`. It is implemented
as a multiset (a list up to permutation) which has no duplicate elements. 

## BASE-LIBRARY REF And
Prop → Prop → Prop

Docstring: `And a b`, or `a ∧ b`, is the conjunction of propositions. It can be
constructed and destructed like a pair: if `ha : a` and `hb : b` then
`⟨ha, hb⟩ : a ∧ b`, and if `h : a ∧ b` then `h.left : a` and `h.right : b`.


Conventions for notations in identifiers:

 * The recommended spelling of `∧` in identifiers is `and`.

 * The recommended spelling of `/\` in identifiers is `and` (prefer `∧` over `/\`).

## BASE-LIBRARY REF Membership.mem
{α : outParam (Type u)} → {γ : Type v} → [self : Membership α γ] → γ → α → Prop

Docstring: The membership relation `a ∈ s : Prop` where `a : α`, `s : γ`. 

Conventions for notations in identifiers:

 * The recommended spelling of `∈` in identifiers is `mem`.

## BASE-LIBRARY REF Finset.instMembership
{α : Type u_1} → Membership α (Finset α)

## BASE-LIBRARY REF Equiv.Perm.IsCycle
{α : Type u_2} → Equiv.Perm α → Prop

Docstring: A cycle is a non-identity permutation where any two nonfixed points of the permutation are
related by repeated application of the permutation. 

## BASE-LIBRARY REF Set.Pairwise
{α : Type u_1} → Set α → (α → α → Prop) → Prop

Docstring: The relation `r` holds pairwise on the set `s` if `r x y` for all *distinct* `x y ∈ s`. 

## BASE-LIBRARY REF SetLike.coe
{A : Type u_1} → {B : outParam (Type u_2)} → [self : SetLike A B] → A → Set B

Docstring: The coercion from a term of a `SetLike` to its corresponding `Set`. 

## BASE-LIBRARY REF Finset.instSetLike
{α : Type u_1} → SetLike (Finset α) α

Docstring: Convert a finset to a set in the natural way. 

## BASE-LIBRARY REF Equiv.Perm.Disjoint
{α : Type u_1} → Equiv.Perm α → Equiv.Perm α → Prop

Docstring: Two permutations `f` and `g` are `Disjoint` if their supports are disjoint, i.e.,
every element is fixed either by `f`, or by `g`. 

## BASE-LIBRARY REF Commute
{S : Type u_3} → [Mul S] → S → S → Prop

Docstring: Two elements commute if `a * b = b * a`. 

## BASE-LIBRARY REF Equiv.Perm.instMul
{α : Type u_4} → Mul (Equiv.Perm α)

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

## BASE-LIBRARY REF Finset.noncommProd
{α : Type u_3} →
  {β : Type u_4} → [inst : Monoid β] → (s : Finset α) → (f : α → β) → (↑s).Pairwise (Function.onFun Commute f) → β

Docstring: Product of a `s : Finset α` mapped with `f : α → β` with `[Monoid β]`,
given a proof that `*` commutes on all elements `f x` for `x ∈ s`. 

## BASE-LIBRARY REF DivInvMonoid.toMonoid
{G : Type u} → [self : DivInvMonoid G] → Monoid G

## BASE-LIBRARY REF Group.toDivInvMonoid
{G : Type u} → [self : Group G] → DivInvMonoid G

## BASE-LIBRARY REF Equiv.Perm.permGroup
{α : Type u_4} → Group (Equiv.Perm α)

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


## BASE-LIBRARY REF Multiset
Type u → Type u

Docstring: `Multiset α` is the quotient of `List α` by list permutation. The result
is a type of finite sets with duplicates allowed. 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF Multiset.map
{α : Type u_1} → {β : Type v} → (α → β) → Multiset α → Multiset β

Docstring: `map f s` is the lift of the list `map` operation. The multiplicity
of `b` in `map f s` is the number of `a ∈ s` (counting multiplicity)
such that `f a = b`. 

## BASE-LIBRARY REF Finset.card
{α : Type u_1} → Finset α → ℕ

Docstring: `s.card` is the number of elements of `s`, aka its cardinality.

The notation `#s` can be accessed in the `Finset` locale. 

## BASE-LIBRARY REF Equiv.Perm.support
{α : Type u_1} → [DecidableEq α] → [Fintype α] → Equiv.Perm α → Finset α

Docstring: The `Finset` of nonfixed points of a permutation. 

## BASE-LIBRARY REF Finset.val
{α : Type u_4} → Finset α → Multiset α

Docstring: The underlying multiset 

## BASE-LIBRARY REF Equiv.Perm.cycleType
{α : Type u_1} → [Fintype α] → [DecidableEq α] → Equiv.Perm α → Multiset ℕ

Docstring: The cycle type of a permutation 

## BASE-LIBRARY REF LinearOrder
Type u_2 → Type u_2

Docstring: A linear order is reflexive, transitive, antisymmetric and total relation `≤`.
We assume that every linear ordered type has decidable `(≤)`, `(<)`, and `(=)`. 

## BASE-LIBRARY REF Inhabited
Sort u → Sort (max 1 u)

Docstring: `Inhabited α` is a typeclass that says that `α` has a designated element,
called `(default : α)`. This is sometimes referred to as a "pointed type".

This class is used by functions that need to return a value of the type
when called "out of domain". For example, `Array.get! arr i : α` returns
a value of type `α` when `arr : Array α`, but if `i` is not in range of
the array, it reports a panic message, but this does not halt the program,
so it must still return a value of type `α` (and in fact this is required
for logical consistency), so in this case it returns `default`.


## BASE-LIBRARY REF ExistsUnique
{α : Sort u_1} → (α → Prop) → Prop

Docstring: For `p : α → Prop`, `ExistsUnique p` means that there exists a unique `x : α` with `p x`. 

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


## BASE-LIBRARY REF List.instMembership
{α : Type u} → Membership α (List α)

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

## BASE-LIBRARY REF List.Nodup
{α : Type u} → List α → Prop

Docstring: The list has no duplicates: it contains every element at most once.

It is defined as `Pairwise (· ≠ ·)`: each element is unequal to all other elements.


## BASE-LIBRARY REF List.flatten
{α : Type u_1} → List (List α) → List α

Docstring: Concatenates a list of lists into a single list, preserving the order of the elements.

`O(|flatten L|)`.

Examples:
* `[["a"], ["b", "c"]].flatten = ["a", "b", "c"]`
* `[["a"], [], ["b", "c"], ["d", "e", "f"]].flatten = ["a", "b", "c", "d", "e", "f"]`


## BASE-LIBRARY REF LE.le
{α : Type u} → [self : LE α] → α → α → Prop

Docstring: The less-equal relation: `x ≤ y` 

Conventions for notations in identifiers:

 * The recommended spelling of `≤` in identifiers is `le`.

 * The recommended spelling of `<=` in identifiers is `le` (prefer `≤` over `<=`).

## BASE-LIBRARY REF Preorder.toLE
{α : Type u_2} → [self : Preorder α] → LE α

## BASE-LIBRARY REF PartialOrder.toPreorder
{α : Type u_2} → [self : PartialOrder α] → Preorder α

## BASE-LIBRARY REF SemilatticeInf.toPartialOrder
{α : Type u} → [self : SemilatticeInf α] → PartialOrder α

## BASE-LIBRARY REF Lattice.toSemilatticeInf
{α : Type u} → [self : Lattice α] → SemilatticeInf α

## BASE-LIBRARY REF DistribLattice.toLattice
{α : Type u_1} → [self : DistribLattice α] → Lattice α

## BASE-LIBRARY REF instDistribLatticeOfLinearOrder
{α : Type u} → [LinearOrder α] → DistribLattice α

## BASE-LIBRARY REF List.head!
{α : Type u_1} → [Inhabited α] → List α → α

Docstring: Returns the first element in the list. If the list is empty, panics and returns `default`.

Safer alternatives include:
* `List.head`, which requires a proof that the list is non-empty,
* `List.head?`, which returns an `Option`, and
* `List.headD`, which returns an explicitly-provided fallback value on empty lists.


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


## BASE-LIBRARY REF GT.gt
{α : Type u} → [LT α] → α → α → Prop

Docstring: `a > b` is an abbreviation for `b < a`. 

Conventions for notations in identifiers:

 * The recommended spelling of `>` in identifiers is `gt`.

## BASE-LIBRARY REF Preorder.toLT
{α : Type u_2} → [self : Preorder α] → LT α

## BASE-LIBRARY REF List.prod
{α : Type u_1} → [Mul α] → [One α] → List α → α

Docstring: Computes the product of the elements of a list.

Examples:

[a, b, c].prod = a * (b * (c * 1))
[2, 3, 5].prod = 30


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


## BASE-LIBRARY REF List.formPerm
{α : Type u_1} → [DecidableEq α] → List α → Equiv.Perm α

Docstring: A list `l : List α` can be interpreted as an `Equiv.Perm α` where each element in the list
is permuted to the next one, defined as `formPerm`. When we have that `Nodup l`,
we prove that `Equiv.Perm.support (formPerm l) = l.toFinset`, and that
`formPerm l` is rotationally invariant, in `formPerm_rotate`.


## INFORMAL STATEMENT
disjoint cycle decomposition of permutations

Let $X$ be a finite set. Let $\sigma $ be a permutation of $X$. Then: \medskip 

\textbf{(a)} There is a list

\begin{align*} &  \Big(\left( a_{1,1},a_{1,2},\ldots ,a_{1,n_{1}}\right) ,\\ &  \  \  \  \left( a_{2,1},a_{2,2},\ldots ,a_{2,n_{2}}\right) ,\\ &  \  \  \  \ldots ,\\ &  \  \  \  \left( a_{k,1},a_{k,2},\ldots ,a_{k,n_{k}}\right) \Big) \end{align*}

 of nonempty lists of elements of $X$ such that: 

\begin{itemize} \item each element of $X$ appears exactly once in the composite list

\begin{align*} &  (a_{1,1},a_{1,2},\ldots ,a_{1,n_{1}},\\ &  \  \  \  a_{2,1},a_{2,2},\ldots ,a_{2,n_{2}},\\ &  \  \  \  \ldots ,\\ &  \  \  \  a_{k,1},a_{k,2},\ldots ,a_{k,n_{k}}), \end{align*}

 and 

\item we have

\[  \sigma =\operatorname *{cyc}\nolimits _{a_{1,1},a_{1,2},\ldots ,a_{1,n_{1}}}\circ \operatorname *{cyc}\nolimits _{a_{2,1},a_{2,2},\ldots ,a_{2,n_{2}}}\circ \cdots \circ \operatorname *{cyc}\nolimits _{a_{k,1},a_{k,2},\ldots ,a_{k,n_{k}}}.  \]

\end{itemize}

Such a list is called a \emph{disjoint cycle decomposition} (or short \emph{DCD}) of $\sigma $. Its entries (which themselves are lists of elements of $X$) are called the \emph{cycles} of $\sigma $. \medskip 

\textbf{(b)} Any two DCDs of $\sigma $ can be obtained from each other by (repeatedly) swapping the cycles with each other, and rotating each cycle (i.e., replacing $\left( a_{i,1},a_{i,2},\ldots ,a_{i,n_{i}}\right) $ by $\left( a_{i,2},a_{i,3},\ldots ,a_{i,n_{i}},a_{i,1}\right) $). \medskip 

\textbf{(c)} Now assume that $X$ is a set of integers (or, more generally, any totally ordered finite set). Then, there is a unique DCD 

\begin{align*} &  \Big(\left( a_{1,1},a_{1,2},\ldots ,a_{1,n_{1}}\right) ,\\ &  \  \  \  \left( a_{2,1},a_{2,2},\ldots ,a_{2,n_{2}}\right) ,\\ &  \  \  \  \ldots ,\\ &  \  \  \  \left( a_{k,1},a_{k,2},\ldots ,a_{k,n_{k}}\right) \Big) \end{align*}

 of $\sigma $ that satisfies the additional requirements that 

\begin{itemize} \item we have $a_{i,1}\leq a_{i,p}$ for each $i\in \left[ k\right] $ and each $p\in \left[ n_{i}\right] $ (that is, each cycle in this DCD is written with its smallest entry first), and 

\item we have $a_{1,1}>a_{2,1}>\cdots >a_{k,1}$ (that is, the cycles appear in this DCD in the order of decreasing first entries). 

\end{itemize}

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.cycs
def.perm.cycs

Let $X$ be a set. Let $i_1, i_2, \ldots , i_k$ be $k$ distinct elements of $X$. Then, 

\[  \operatorname {cyc}_{i_1, i_2, \ldots , i_k}  \]

 means the permutation of $X$ that sends 

\begin{align*} & i_1 \text{ to } i_2, \\ & i_2 \text{ to } i_3, \\ & \ldots , \\ & i_{k-1} \text{ to } i_k, \\ & i_k \text{ to } i_1 \end{align*}

 and leaves all other elements of $X$ unchanged. In other words, $\operatorname {cyc}_{i_1, i_2, \ldots , i_k}$ means the permutation of $X$ that satisfies 

\[  \operatorname {cyc}_{i_1, \ldots , i_k}(p) = \begin{cases}  i_{j+1}, &  \text{if } p = i_j \text{ for some } j \in \{ 1, 2, \ldots , k\} ;\\ p, &  \text{otherwise} \end{cases}  \]

 for every $p \in X$, where $i_{k+1}$ means $i_1$. 

This permutation is called a $k$\emph{-cycle}.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.perm
def.perm.perm

Let $X$ be a set. 

\textbf{(a)} A \emph{permutation} of $X$ means a bijection from $X$ to $X$. 

\textbf{(b)} It is known that the set of all permutations of $X$ is a group under composition. This group is called the \emph{symmetric group} of $X$, and is denoted by $S_X$. Its neutral element is the identity map $\operatorname {id}_X : X \to X$. Its size is $|X|!$ when $X$ is finite. 

\textbf{(c)} As usual in group theory, we will write $\alpha \beta $ for the composition $\alpha \circ \beta $ when $\alpha , \beta \in S_X$. This is the map that sends each $x \in X$ to $\alpha (\beta (x))$. 

\textbf{(d)} If $\alpha \in S_X$ and $i \in \mathbb {Z}$, then $\alpha ^i$ shall denote the $i$-th power of $\alpha $ in the group $S_X$. Note that $\alpha ^i = \underbrace{\alpha \circ \alpha \circ \cdots \circ \alpha }_{i\text{ times}}$ if $i \ge 0$. Also, $\alpha ^0 = \operatorname {id}_X$. Also, $\alpha ^{-1}$ is the inverse of $\alpha $ in the group $S_X$, that is, the inverse of the map $\alpha $.

## VERDICT
{
  "verdict": "drift",
  "justification": "The package weakens and restricts the blueprint in several places. For (b), the blueprint asserts that \u201cAny two DCDs of \u03c3 can be obtained from each other\u201d by swapping cycles and rotating them, whereas `dcd_unique_cycleType` concludes only `Multiset.map (fun c => c.support.card) cycs.val = \u03c3.cycleType`. Equality of the multiset of cycle lengths does not express, and is strictly weaker than, equivalence of the actual cycles under swapping and rotation. This declaration should instead quantify over two list-based DCDs and assert equality modulo an outer permutation and rotations of the inner lists. For (c), `canonicalDcd_exists_unique` adds the binder `[Inhabited \u03b1]`, while the blueprint covers \u201cany totally ordered finite set,\u201d including the empty set. This is a mathematically contentful restriction introduced solely because the predicate uses `List.head!`; the empty ordered finite type has the unique empty DCD. Faithfulness would require removing `[Inhabited \u03b1]` and replacing `head!` with a head/minimum construction justified by the existing hypotheses `l \u2260 []`. Moreover, for (a), `exists_dcd` witnesses a `Finset (Equiv.Perm \u03b1)` of nonidentity `IsCycle`s and gives disjointness and a product equation, but does not directly witness the blueprint\u2019s `List (List \u03b1)` with nonempty entries and the explicit condition that every element of `X` occurs exactly once; in particular fixed points are omitted from `IsCycle` factors because `IsCycle` is nonidentity, while the blueprint represents them by singleton lists. A direct faithful declaration would use list representatives with nonemptiness, `flatten.Nodup`, universal membership in the flattening, and the `dcdListToPerm` product equation, as in the predicate used by the third target."
}