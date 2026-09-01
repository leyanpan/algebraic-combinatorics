## TARGET AlgebraicCombinatorics.CycleDecomposition.dcdListToPerm_cyclesList_eq (theorem) — ELABORATED SIGNATURE
∀ {α : Type u_1} [inst : DecidableEq α] [inst_1 : Fintype α] [inst_2 : LinearOrder α] (σ : Equiv.Perm α)
  (cyclesList : List (List α)),
  cyclesList =
      List.map
        (fun x =>
          match x with
          | ⟨c, hc⟩ =>
            have hcycle := ⋯;
            AlgebraicCombinatorics.CycleDecomposition.cycleToCanonicalList c hcycle)
        σ.cycleFactorsFinset.toList.attach →
    (List.map List.formPerm cyclesList).prod = σ

Docstring: The product of formPerms of cyclesList equals σ. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.CycleDecomposition.cyclesList_pairwise_disjoint (theorem)
∀ {α : Type u_1} [inst : DecidableEq α] [inst_1 : Fintype α] [inst_2 : LinearOrder α] (σ : Equiv.Perm α)
  (cyclesList : List (List α)),
  cyclesList =
      List.map
        (fun x =>
          match x with
          | ⟨c, hc⟩ =>
            have hcycle := ⋯;
            AlgebraicCombinatorics.CycleDecomposition.cycleToCanonicalList c hcycle)
        σ.cycleFactorsFinset.toList.attach →
    List.Pairwise List.Disjoint cyclesList

Docstring: The cyclesList (list of canonical lists for each cycle) is pairwise List.Disjoint. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.CycleDecomposition.cycleToCanonicalList (def)
{α : Type u_1} → [DecidableEq α] → [Fintype α] → [LinearOrder α] → (c : Equiv.Perm α) → c.IsCycle → List α

Body:
fun {α} [DecidableEq α] [Fintype α] [LinearOrder α] c hc =>
  c.toList (AlgebraicCombinatorics.CycleDecomposition.cycleMinElem c hc)

Docstring: Get the canonical list representation of a cycle starting from its minimum element. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.CycleDecomposition.cycleMinElem (def)
{α : Type u_1} → [DecidableEq α] → [Fintype α] → [LinearOrder α] → (c : Equiv.Perm α) → c.IsCycle → α

Body:
fun {α} [DecidableEq α] [Fintype α] [LinearOrder α] c hc => c.support.min' ⋯

Docstring: Get the minimum element of a cycle's support. 

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

## BASE-LIBRARY REF LinearOrder
Type u_2 → Type u_2

Docstring: A linear order is reflexive, transitive, antisymmetric and total relation `≤`.
We assume that every linear ordered type has decidable `(≤)`, `(<)`, and `(=)`. 

## BASE-LIBRARY REF Equiv.Perm
Sort u_1 → Sort (max 1 u_1)

Docstring: `Perm α` is the type of bijections from `α` to itself. 

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

## BASE-LIBRARY REF List.map
{α : Type u_1} → {β : Type u_2} → (α → β) → List α → List β

Docstring: Applies a function to each element of the list, returning the resulting list of values.

`O(|l|)`.

Examples:
* `[a, b, c].map f = [f a, f b, f c]`
* `[].map Nat.succ = []`
* `["one", "two", "three"].map (·.length) = [3, 3, 5]`
* `["one", "two", "three"].map (·.reverse) = ["eno", "owt", "eerht"]`


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

## BASE-LIBRARY REF Membership.mem
{α : outParam (Type u)} → {γ : Type v} → [self : Membership α γ] → γ → α → Prop

Docstring: The membership relation `a ∈ s : Prop` where `a : α`, `s : γ`. 

Conventions for notations in identifiers:

 * The recommended spelling of `∈` in identifiers is `mem`.

## BASE-LIBRARY REF List.instMembership
{α : Type u} → Membership α (List α)

## BASE-LIBRARY REF Finset.toList
{α : Type u_1} → Finset α → List α

Docstring: Produce a list of the elements in the finite set using choice. 

## BASE-LIBRARY REF Equiv.Perm.cycleFactorsFinset
{α : Type u_2} → [DecidableEq α] → [Fintype α] → Equiv.Perm α → Finset (Equiv.Perm α)

Docstring: Factors a permutation `f` into a `Finset` of disjoint cyclic permutations that multiply to `f`.


## BASE-LIBRARY REF Equiv.Perm.IsCycle
{α : Type u_2} → Equiv.Perm α → Prop

Docstring: A cycle is a non-identity permutation where any two nonfixed points of the permutation are
related by repeated application of the permutation. 

## BASE-LIBRARY REF And.left
∀ {a b : Prop}, a ∧ b → a

Docstring: Extract the left conjunct from a conjunction. `h : a ∧ b` then
`h.left`, also notated as `h.1`, is a proof of `a`. 

## BASE-LIBRARY REF Finset
Type u_4 → Type u_4

Docstring: `Finset α` is the type of finite sets of elements of `α`. It is implemented
as a multiset (a list up to permutation) which has no duplicate elements. 

## BASE-LIBRARY REF Finset.instMembership
{α : Type u_1} → Membership α (Finset α)

## BASE-LIBRARY REF Equiv.Perm.support
{α : Type u_1} → [DecidableEq α] → [Fintype α] → Equiv.Perm α → Finset α

Docstring: The `Finset` of nonfixed points of a permutation. 

## BASE-LIBRARY REF DFunLike.coe
{F : Sort u_1} → {α : outParam (Sort u_2)} → {β : outParam (α → Sort u_3)} → [self : DFunLike F α β] → F → (a : α) → β a

Docstring: The coercion from `F` to a function. 

## BASE-LIBRARY REF EquivLike.toFunLike
{E : Sort u_1} → {α : Sort u_3} → {β : Sort u_4} → [EquivLike E α β] → FunLike E α β

## BASE-LIBRARY REF Equiv.instEquivLike
{α : Sort u} → {β : Sort v} → EquivLike (α ≃ β) α β

## BASE-LIBRARY REF Iff.mp
∀ {a b : Prop}, (a ↔ b) → a → b

Docstring: Modus ponens for if and only if. If `a ↔ b` and `a`, then `b`. 

## BASE-LIBRARY REF And
Prop → Prop → Prop

Docstring: `And a b`, or `a ∧ b`, is the conjunction of propositions. It can be
constructed and destructed like a pair: if `ha : a` and `hb : b` then
`⟨ha, hb⟩ : a ∧ b`, and if `h : a ∧ b` then `h.left : a` and `h.right : b`.


Conventions for notations in identifiers:

 * The recommended spelling of `∧` in identifiers is `and`.

 * The recommended spelling of `/\` in identifiers is `and` (prefer `∧` over `/\`).

## BASE-LIBRARY REF Equiv.Perm.mem_cycleFactorsFinset_iff
∀ {α : Type u_2} [inst : DecidableEq α] [inst_1 : Fintype α] {f p : Equiv.Perm α},
  p ∈ f.cycleFactorsFinset ↔ p.IsCycle ∧ ∀ a ∈ p.support, p a = f a

## BASE-LIBRARY REF Finset.mem_toList
∀ {α : Type u_1} {a : α} {s : Finset α}, a ∈ s.toList ↔ a ∈ s

## BASE-LIBRARY REF List.attach
{α : Type u_1} → (l : List α) → List { x // x ∈ l }

Docstring: “Attaches” the proof that the elements of `l` are in fact elements of `l`, producing a new list with
the same elements but in the subtype `{ x // x ∈ l }`.

`O(1)`.

This function is primarily used to allow definitions by [well-founded
recursion](https://lean-lang.org/doc/reference/4.28.0/find/?domain=Verso.Genre.Manual.section&name=well-founded-recursion) that use higher-order functions (such as
`List.map`) to prove that an value taken from a list is smaller than the list. This allows the
well-founded recursion mechanism to prove that the function terminates.


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

## BASE-LIBRARY REF List.formPerm
{α : Type u_1} → [DecidableEq α] → List α → Equiv.Perm α

Docstring: A list `l : List α` can be interpreted as an `Equiv.Perm α` where each element in the list
is permuted to the next one, defined as `formPerm`. When we have that `Nodup l`,
we prove that `Equiv.Perm.support (formPerm l) = l.toFinset`, and that
`formPerm l` is rotationally invariant, in `formPerm_rotate`.


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


## BASE-LIBRARY REF List.Disjoint
{α : Type u_1} → List α → List α → Prop

Docstring: `Disjoint l₁ l₂` means that `l₁` and `l₂` have no elements in common. 

## BASE-LIBRARY REF Equiv.Perm.toList
{α : Type u_1} → [Fintype α] → [DecidableEq α] → Equiv.Perm α → α → List α

Docstring: `Equiv.Perm.toList (f : Perm α) (x : α)` generates the list `[x, f x, f (f x), ...]`
until looping. That means when `f x = x`, `toList f x = []`.


## BASE-LIBRARY REF Finset.min'
{α : Type u_2} → [LinearOrder α] → (s : Finset α) → s.Nonempty → α

Docstring: Given a nonempty finset `s` in a linear order `α`, then `s.min' H` is its minimum, as an
element of `α`, where `H` is a proof of nonemptiness. Without this assumption, use instead `s.min`,
taking values in `WithTop α`. 

## BASE-LIBRARY REF Equiv.Perm.IsCycle.nonempty_support
∀ {α : Type u_2} [inst : Fintype α] [inst_1 : DecidableEq α] {g : Equiv.Perm α}, g.IsCycle → g.support.Nonempty

Docstring: Support of a cycle is nonempty 

## INFORMAL STATEMENT
lem.dcdListToPerm_cyclesList_eq

\leanhelper  The product of the cycle permutations of the canonical list representations of $\sigma $’s cycles equals $\sigma $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-conv-2eb59533
conv-2eb59533

In the Lean formalization, we use $\operatorname {Fin} n = \{ 0, 1, \ldots , n-1\} $ instead of the textbook’s $[n] = \{ 1, 2, \ldots , n\} $. Both are $n$-element sets, so their symmetric groups are isomorphic. Permutations are represented by the type of bijections $X \to X$ (denoted $\operatorname {Equiv.Perm}\,  X$ in Lean), which is a group under composition. Composition $\alpha \beta $ is the group multiplication $\alpha * \beta $, sending $x$ to $\alpha (\beta (x))$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.cycleminelem
def.cycleMinElem

\leanhelper  Let $c$ be a cycle permutation (i.e., $c$ is a cycle in the sense of Definition~ \ref{def.perm.cycs.cycs}). The \emph{minimum element} of $c$ is the smallest element in the support of $c$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.cycletocanonicallist
def.cycleToCanonicalList

\leanhelper  Let $c$ be a cycle permutation. The \emph{canonical list representation} of $c$ is the list $(a, c(a), c^2(a), \ldots )$ where $a$ is the minimum element of $c$ (Definition~ \ref{def.cycleMinElem}).

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.dcdlisttoperm
def.dcdListToPerm

\leanhelper  Given a list of lists (each representing a cycle), the corresponding permutation is obtained by composing the cycle permutations $\operatorname {cyc}_{a_1, a_2, \ldots , a_m}$ for each list $(a_1, a_2, \ldots , a_m)$ in the input.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.comps
def.fps.comps

\textbf{(a)} An \emph{(integer) composition} means a (finite) tuple of positive integers. \medskip 

\textbf{(b)} The \emph{size} of an integer composition $\alpha =\left( \alpha _{1},\alpha _{2},\ldots ,\alpha _{m}\right) $ is defined to be the integer $\alpha _{1}+\alpha _{2}+\cdots +\alpha _{m}$. It is written $\left\vert \alpha \right\vert $. \medskip 

\textbf{(c)} The \emph{length} of an integer composition $\alpha =\left( \alpha _{1},\alpha _{2},\ldots ,\alpha _{m}\right) $ is defined to be the integer $m$. It is written $\ell \left( \alpha \right) $. \medskip 

\textbf{(d)} Let $n\in \mathbb {N}$. A \emph{composition of }$n$ means a composition whose size is $n$. \medskip 

\textbf{(e)} Let $n\in \mathbb {N}$ and $k\in \mathbb {N}$. A \emph{composition of }$n$\emph{ into }$k$\emph{ parts} is a composition whose size is $n$ and whose length is $k$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.pars.parts
def.pars.parts

\textbf{(a)} An \emph{(integer) partition} means a (finite) weakly decreasing tuple of positive integers – i.e., a finite tuple $\left( \lambda _{1},\lambda _{2},\ldots ,\lambda _{m}\right) $ of positive integers such that $\lambda _{1}\geq \lambda _{2}\geq \cdots \geq \lambda _{m}$. 

Thus, partitions are the same as weakly decreasing compositions. Hence, the notions of \emph{size} and \emph{length} of a partition are automatically defined, since we have defined them for compositions (in Definition \ref{def.fps.comps}). \medskip 

\textbf{(b)} The \emph{parts} of a partition $\left( \lambda _{1},\lambda _{2},\ldots ,\lambda _{m}\right) $ are simply its entries $\lambda _{1},\lambda _{2},\ldots ,\lambda _{m}$. \medskip 

\textbf{(c)} Let $n\in \mathbb {Z}$. A \emph{partition of }$n$ means a partition whose size is $n$. \medskip 

\textbf{(d)} Let $n\in \mathbb {Z}$ and $k\in \mathbb {N}$. A \emph{partition of }$n$\emph{ into }$k$\emph{ parts} is a partition whose size is $n$ and whose length is $k$.

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.cycs.cycs
def.perm.cycs.cycs

Let $X$ be a finite set. Let $\sigma $ be a permutation of $X$. \medskip 

\textbf{(a)} The \emph{cycles} of $\sigma $ are defined to be the cycles in the DCD of $\sigma $ (as defined in Theorem \ref{thm.perm.dcd.main} \textbf{(a)}). (This includes $1$-cycles, if there are any in the DCD of $\sigma $.) 

We shall equate a cycle of $\sigma $ with any of its cyclic rotations; thus, for example, $\left( 3,1,4\right) $ and $\left( 1,4,3\right) $ shall be regarded as being the same cycle (but $\left( 3,1,4\right) $ and $\left( 3,4,1\right) $ shall not). \medskip 

\textbf{(b)} The \emph{cycle lengths partition} of $\sigma $ shall denote the partition of $\left\vert X\right\vert $ obtained by writing down the lengths of the cycles of $\sigma $ in weakly decreasing order.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.perm
def.perm.perm

Let $X$ be a set. 

\textbf{(a)} A \emph{permutation} of $X$ means a bijection from $X$ to $X$. 

\textbf{(b)} It is known that the set of all permutations of $X$ is a group under composition. This group is called the \emph{symmetric group} of $X$, and is denoted by $S_X$. Its neutral element is the identity map $\operatorname {id}_X : X \to X$. Its size is $|X|!$ when $X$ is finite. 

\textbf{(c)} As usual in group theory, we will write $\alpha \beta $ for the composition $\alpha \circ \beta $ when $\alpha , \beta \in S_X$. This is the map that sends each $x \in X$ to $\alpha (\beta (x))$. 

\textbf{(d)} If $\alpha \in S_X$ and $i \in \mathbb {Z}$, then $\alpha ^i$ shall denote the $i$-th power of $\alpha $ in the group $S_X$. Note that $\alpha ^i = \underbrace{\alpha \circ \alpha \circ \cdots \circ \alpha }_{i\text{ times}}$ if $i \ge 0$. Also, $\alpha ^0 = \operatorname {id}_X$. Also, $\alpha ^{-1}$ is the inverse of $\alpha $ in the group $S_X$, that is, the inverse of the map $\alpha $.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The formal conclusion `(List.map List.formPerm cyclesList).prod = \u03c3`, under the defining hypothesis that `cyclesList` is the map of `cycleToCanonicalList` over `\u03c3.cycleFactorsFinset.toList`, directly matches \u201cThe product of the cycle permutations of the canonical list representations of \u03c3\u2019s cycles equals \u03c3.\u201d The dependency body `cycleToCanonicalList c hcycle = c.toList (cycleMinElem c hcycle)` agrees with the informal canonical list beginning at the minimum support element, and `List.formPerm` interprets each such list as its cycle permutation. Although `cycleFactorsFinset` uses `IsCycle`, whose docstring excludes the identity, while the informal definition explicitly says cycles include 1-cycles, this does not change the asserted product: every 1-cycle is the identity permutation, so inserting or omitting such factors leaves the product equal to `\u03c3`. The binders `[Fintype \u03b1]` and `[DecidableEq \u03b1]` encode the finite permutation setting, while `[LinearOrder \u03b1]` is needed to state the specified minimum-element canonicalization. The auxiliary `cyclesList` binder with an equality hypothesis is merely a definitional presentation of the canonical cycle list, not an additional mathematical restriction."
}