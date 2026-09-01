## TARGET Equiv.Perm.sum_lehmerEntry_eq_length (theorem) — ELABORATED SIGNATURE
∀ {n : ℕ} (σ : Equiv.Perm (Fin n)), ∑ i, σ.lehmerEntry i = σ.length

Docstring: The sum of Lehmer entries equals the length. 

## PROJECT DEPENDENCY Equiv.Perm.lehmerEntry (def)
{n : ℕ} → Equiv.Perm (Fin n) → Fin n → ℕ

Body:
fun {n} σ i => AlgebraicCombinatorics.Perm.lehmerEntry σ i

Docstring: Alias for the canonical Lehmer entry definition from `AlgebraicCombinatorics.Perm.lehmerEntry`.
Counts inversions (i, j) with first coordinate i. 

## PROJECT DEPENDENCY Equiv.Perm.length (def)
{n : ℕ} → Equiv.Perm (Fin n) → ℕ

Body:
fun {n} σ => σ.inversions.card

Docstring: The length of a permutation is the number of its inversions. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.Perm.lehmerEntry (def)
{n : ℕ} → Equiv.Perm (Fin n) → Fin n → ℕ

Body:
fun {n} σ i => {j | i < j ∧ σ i > σ j}.card

Docstring: For σ ∈ S_n and i ∈ [n], we define ℓ_i(σ) as the number of j > i such that σ(i) > σ(j).
This counts how many elements to the right of position i are smaller than σ(i).

This is the canonical definition of Lehmer entry used throughout the project.
The equivalent formulation `i < j ∧ σ j < σ i` is provided by `lehmerEntry_eq_filter_lt`.

See Definition 1.3.5 (def.perm.lehmer1) part (a) in the source.


## PROJECT DEPENDENCY Equiv.Perm.inversions (def)
{n : ℕ} → Equiv.Perm (Fin n) → Finset (Fin n × Fin n)

Body:
fun {n} σ => {p | p.1 < p.2 ∧ σ p.2 < σ p.1}

Docstring: The set of inversions of a permutation. 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF Equiv.Perm
Sort u_1 → Sort (max 1 u_1)

Docstring: `Perm α` is the type of bijections from `α` to itself. 

## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


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

## BASE-LIBRARY REF Finset.sum
{ι : Type u_1} → {M : Type u_3} → [AddCommMonoid M] → Finset ι → (ι → M) → M

Docstring: `∑ x ∈ s, f x` is the sum of `f x` as `x` ranges over the elements
of the finite set `s`.

When the index type is a `Fintype`, the notation `∑ x, f x`, is a shorthand for
`∑ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF Nat.instAddCommMonoid
AddCommMonoid ℕ

## BASE-LIBRARY REF Finset.univ
{α : Type u_1} → [Fintype α] → Finset α

Docstring: `univ` is the universal finite set of type `Finset α` implied from
the assumption `Fintype α`. 

## BASE-LIBRARY REF Fin.fintype
(n : ℕ) → Fintype (Fin n)

## BASE-LIBRARY REF Finset.card
{α : Type u_1} → Finset α → ℕ

Docstring: `s.card` is the number of elements of `s`, aka its cardinality.

The notation `#s` can be accessed in the `Finset` locale. 

## BASE-LIBRARY REF Prod
Type u → Type v → Type (max u v)

Docstring: The product type, usually written `α × β`. Product types are also called pair or tuple types.
Elements of this type are pairs in which the first element is an `α` and the second element is a
`β`.

Products nest to the right, so `(x, y, z) : α × β × γ` is equivalent to `(x, (y, z)) : α × (β × γ)`.


Conventions for notations in identifiers:

 * The recommended spelling of `×` in identifiers is `Prod`.

## BASE-LIBRARY REF Finset.filter
{α : Type u_1} → (p : α → Prop) → [DecidablePred p] → Finset α → Finset α

Docstring: `Finset.filter p s` is the set of elements of `s` that satisfy `p`.

For example, one can use `s.filter (· ∈ t)` to get the intersection of `s` with `t : Set α`
as a `Finset α` (when a `DecidablePred (· ∈ t)` instance is available). 

## BASE-LIBRARY REF And
Prop → Prop → Prop

Docstring: `And a b`, or `a ∧ b`, is the conjunction of propositions. It can be
constructed and destructed like a pair: if `ha : a` and `hb : b` then
`⟨ha, hb⟩ : a ∧ b`, and if `h : a ∧ b` then `h.left : a` and `h.right : b`.


Conventions for notations in identifiers:

 * The recommended spelling of `∧` in identifiers is `and`.

 * The recommended spelling of `/\` in identifiers is `and` (prefer `∧` over `/\`).

## BASE-LIBRARY REF LT.lt
{α : Type u} → [self : LT α] → α → α → Prop

Docstring: The less-than relation: `x < y` 

Conventions for notations in identifiers:

 * The recommended spelling of `<` in identifiers is `lt`.

## BASE-LIBRARY REF instLTFin
{n : ℕ} → LT (Fin n)

## BASE-LIBRARY REF GT.gt
{α : Type u} → [LT α] → α → α → Prop

Docstring: `a > b` is an abbreviation for `b < a`. 

Conventions for notations in identifiers:

 * The recommended spelling of `>` in identifiers is `gt`.

## BASE-LIBRARY REF DFunLike.coe
{F : Sort u_1} → {α : outParam (Sort u_2)} → {β : outParam (α → Sort u_3)} → [self : DFunLike F α β] → F → (a : α) → β a

Docstring: The coercion from `F` to a function. 

## BASE-LIBRARY REF EquivLike.toFunLike
{E : Sort u_1} → {α : Sort u_3} → {β : Sort u_4} → [EquivLike E α β] → FunLike E α β

## BASE-LIBRARY REF Equiv.instEquivLike
{α : Sort u} → {β : Sort v} → EquivLike (α ≃ β) α β

## BASE-LIBRARY REF instDecidableAnd
{p q : Prop} → [dp : Decidable p] → [dq : Decidable q] → Decidable (p ∧ q)

## BASE-LIBRARY REF Fin.decLt
{n : ℕ} → (a b : Fin n) → Decidable (a < b)

## BASE-LIBRARY REF Finset
Type u_4 → Type u_4

Docstring: `Finset α` is the type of finite sets of elements of `α`. It is implemented
as a multiset (a list up to permutation) which has no duplicate elements. 

## BASE-LIBRARY REF Prod.fst
{α : Type u} → {β : Type v} → α × β → α

Docstring: The first element of a pair. 

## BASE-LIBRARY REF Prod.snd
{α : Type u} → {β : Type v} → α × β → β

Docstring: The second element of a pair. 

## BASE-LIBRARY REF instFintypeProd
(α : Type u_4) → (β : Type u_5) → [Fintype α] → [Fintype β] → Fintype (α × β)

## INFORMAL STATEMENT
lem.perm.sum-lehmer-eq-length

\leanhelper  The sum of Lehmer entries equals the length: $\sum _{i \in [n]} \ell _i(\sigma ) = \ell (\sigma )$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-conv-2eb59533
conv-2eb59533

In the Lean formalization, we use $\operatorname {Fin} n = \{ 0, 1, \ldots , n-1\} $ instead of the textbook’s $[n] = \{ 1, 2, \ldots , n\} $. Both are $n$-element sets, so their symmetric groups are isomorphic. Permutations are represented by the type of bijections $X \to X$ (denoted $\operatorname {Equiv.Perm}\,  X$ in Lean), which is a group under composition. Composition $\alpha \beta $ is the group multiplication $\alpha * \beta $, sending $x$ to $\alpha (\beta (x))$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.lehmer1
def.perm.lehmer1

Let $n\in \mathbb {N}$. \medskip 

\textbf{(a)} For each $\sigma \in S_{n}$ and $i\in \left[n\right]$, we set 

\begin{align*}  \ell _{i}\left(\sigma \right) := &  \left(\text{\#  of all }j\in \left[n\right] \text{ satisfying }i<j\text{ and }\sigma \left(i\right) >\sigma \left(j\right)\right) \\ = &  \left(\text{\#  of all }j\in \left\{ i+1,i+2,\ldots ,n\right\}  \text{ such that }\sigma \left(i\right)>\sigma \left(j\right)\right). \end{align*}

   \medskip 

\textbf{(b)} For each $m\in \mathbb {Z}$, we let $\left[m\right]_{0}$ denote the set $\left\{ 0,1,\ldots ,m\right\} $. (This is an empty set when $m<0$.)   \medskip 

\textbf{(c)} We let $H_{n}$ denote the set 

\begin{align*} &  \left[n-1\right]_{0}\times \left[n-2\right]_{0}\times \cdots \times \left[n-n\right]_{0}\\ &  = \left\{ \left(j_{1},j_{2},\ldots ,j_{n}\right)\in \mathbb {N}^{n} \  \mid \  j_{i}\leq n-i\text{ for each }i\in \left[n\right]\right\} . \end{align*}

 This set $H_{n}$ has size $n!$.   \medskip 

\textbf{(d)} Each $\sigma \in S_n$ and each $i\in [n]$ satisfy $\ell _i(\sigma ) \in \{ 0,1,\ldots ,n-i\}  = [n-i]_0$.   \medskip 

\textbf{(e)} We define the map 

\begin{align*}  L:S_{n} & \rightarrow H_{n},\\ \sigma & \mapsto \left(\ell _{1}\left(\sigma \right),\ell _{2}\left( \sigma \right),\ldots ,\ell _{n}\left(\sigma \right)\right). \end{align*}

 If $\sigma \in S_{n}$ is a permutation, then the $n$-tuple $L\left(\sigma \right)$ is called the \emph{Lehmer code} (or just the \emph{code}) of $\sigma $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.perm
def.perm.perm

Let $X$ be a set. 

\textbf{(a)} A \emph{permutation} of $X$ means a bijection from $X$ to $X$. 

\textbf{(b)} It is known that the set of all permutations of $X$ is a group under composition. This group is called the \emph{symmetric group} of $X$, and is denoted by $S_X$. Its neutral element is the identity map $\operatorname {id}_X : X \to X$. Its size is $|X|!$ when $X$ is finite. 

\textbf{(c)} As usual in group theory, we will write $\alpha \beta $ for the composition $\alpha \circ \beta $ when $\alpha , \beta \in S_X$. This is the map that sends each $x \in X$ to $\alpha (\beta (x))$. 

\textbf{(d)} If $\alpha \in S_X$ and $i \in \mathbb {Z}$, then $\alpha ^i$ shall denote the $i$-th power of $\alpha $ in the group $S_X$. Note that $\alpha ^i = \underbrace{\alpha \circ \alpha \circ \cdots \circ \alpha }_{i\text{ times}}$ if $i \ge 0$. Also, $\alpha ^0 = \operatorname {id}_X$. Also, $\alpha ^{-1}$ is the inverse of $\alpha $ in the group $S_X$, that is, the inverse of the map $\alpha $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.sn-iven
def.perm.Sn-iven

Let $n \in \mathbb {Z}$. Then, $[n]$ shall mean the set $\{ 1, 2, \ldots , n\} $. This is an $n$-element set if $n \ge 0$, and is an empty set if $n \le 0$. 

The symmetric group $S_{[n]}$ (consisting of all permutations of $[n]$) will be denoted $S_n$ and called the $n$\emph{-th symmetric group}. Its size is $n!$ (when $n \ge 0$).

## VERDICT
{
  "verdict": "unclear",
  "justification": "The Lean target states `\u2200 {n : \u2115} (\u03c3 : Equiv.Perm (Fin n)), \u2211 i, \u03c3.lehmerEntry i = \u03c3.length`, where `Equiv.Perm.length` is definitionally `\u03c3.inversions.card` and `\u03c3.inversions` consists of pairs satisfying `p.1 < p.2 \u2227 \u03c3 p.2 < \u03c3 p.1`. Its `lehmerEntry` correctly matches the informal definition of `\u2113_i(\u03c3)` as the number of `j` with `i < j` and `\u03c3(i) > \u03c3(j)`. However, the informal statement\u2019s right-hand side is merely called \u201cthe length,\u201d `\u2113(\u03c3)`, and the package supplies no informal definition saying that this length is the number of inversions. Thus the package does not determine whether the project definition `Equiv.Perm.length := \u03c3.inversions.card` has the intended blueprint meaning. An informal definition of `\u2113(\u03c3)` is needed; if it defines length as the inversion count, the declaration is faithful."
}