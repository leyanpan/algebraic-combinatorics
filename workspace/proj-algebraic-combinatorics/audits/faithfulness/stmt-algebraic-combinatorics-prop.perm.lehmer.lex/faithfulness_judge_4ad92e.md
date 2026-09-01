## TARGET AlgebraicCombinatorics.Perm.lehmerCode_preserves_lexLt (theorem) — ELABORATED SIGNATURE
∀ {n : ℕ} (σ τ : Equiv.Perm (Fin n)),
  (AlgebraicCombinatorics.lexLt (fun i => ↑↑(σ i)) fun i => ↑↑(τ i)) →
    AlgebraicCombinatorics.lexLt (fun i => ↑(AlgebraicCombinatorics.Perm.lehmerEntry σ i)) fun i =>
      ↑(AlgebraicCombinatorics.Perm.lehmerEntry τ i)

Docstring: If σ, τ ∈ S_n satisfy (σ(1), ..., σ(n)) <_lex (τ(1), ..., τ(n)),
then L(σ) <_lex L(τ).

**Proposition prop.perm.lehmer.lex** from the source.

The proof uses the alternative characterization of Lehmer entries:
ℓ_i(σ) counts elements smaller than σ(i) that are not in the image of positions before i.
If σ and τ agree on positions below k and σ(k) < τ(k), then:
- For i < k: ℓ_i(σ) = ℓ_i(τ) (since the images below i are equal and σ(i) = τ(i))
- At k: ℓ_k(σ) < ℓ_k(τ) (since σ(k) is available for τ but not for σ)


## PROJECT DEPENDENCY AlgebraicCombinatorics.lexLt (def)
{n : ℕ} → (Fin n → ℤ) → (Fin n → ℤ) → Prop

Body:
fun {n} a b => ∃ k, (∀ i < k, a i = b i) ∧ a k < b k

Docstring: Lexicographic order on n-tuples of integers.
We say (a_1, ..., a_n) <_lex (b_1, ..., b_n) if there exists k ∈ [n]
such that a_k ≠ b_k and the smallest such k satisfies a_k < b_k.

Note: This is essentially `Pi.Lex (· < ·) (· < ·)` from Mathlib, specialized to `Fin n → ℤ`.
We define it directly here to match the source presentation.

See Definition 1.3.8 (def.perm.lehmer.lex-ord) in the source.


## PROJECT DEPENDENCY AlgebraicCombinatorics.Perm.lehmerEntry (def)
{n : ℕ} → Equiv.Perm (Fin n) → Fin n → ℕ

Body:
fun {n} σ i => {j | i < j ∧ σ i > σ j}.card

Docstring: For σ ∈ S_n and i ∈ [n], we define ℓ_i(σ) as the number of j > i such that σ(i) > σ(j).
This counts how many elements to the right of position i are smaller than σ(i).

This is the canonical definition of Lehmer entry used throughout the project.
The equivalent formulation `i < j ∧ σ j < σ i` is provided by `lehmerEntry_eq_filter_lt`.

See Definition 1.3.5 (def.perm.lehmer1) part (a) in the source.


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


## BASE-LIBRARY REF Int
Type

Docstring: The integers.

This type is special-cased by the compiler and overridden with an efficient implementation. The
runtime has a special representation for `Int` that stores “small” signed numbers directly, while
larger numbers use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)). A “small number” is an integer that can be encoded with one fewer bits
than the platform's pointer size (i.e. 63 bits on 64-bit architectures and 31 bits on 32-bit
architectures).


## BASE-LIBRARY REF instNatCastInt
NatCast ℤ

## BASE-LIBRARY REF Fin.val
{n : ℕ} → Fin n → ℕ

Docstring: The number that is strictly less than `n`.

`Fin.val` is a coercion, so any `Fin n` can be used in a position where a `Nat` is expected.


## BASE-LIBRARY REF DFunLike.coe
{F : Sort u_1} → {α : outParam (Sort u_2)} → {β : outParam (α → Sort u_3)} → [self : DFunLike F α β] → F → (a : α) → β a

Docstring: The coercion from `F` to a function. 

## BASE-LIBRARY REF EquivLike.toFunLike
{E : Sort u_1} → {α : Sort u_3} → {β : Sort u_4} → [EquivLike E α β] → FunLike E α β

## BASE-LIBRARY REF Equiv.instEquivLike
{α : Sort u} → {β : Sort v} → EquivLike (α ≃ β) α β

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

## BASE-LIBRARY REF Int.instLTInt
LT ℤ

## BASE-LIBRARY REF Finset.card
{α : Type u_1} → Finset α → ℕ

Docstring: `s.card` is the number of elements of `s`, aka its cardinality.

The notation `#s` can be accessed in the `Finset` locale. 

## BASE-LIBRARY REF Finset.filter
{α : Type u_1} → (p : α → Prop) → [DecidablePred p] → Finset α → Finset α

Docstring: `Finset.filter p s` is the set of elements of `s` that satisfy `p`.

For example, one can use `s.filter (· ∈ t)` to get the intersection of `s` with `t : Set α`
as a `Finset α` (when a `DecidablePred (· ∈ t)` instance is available). 

## BASE-LIBRARY REF GT.gt
{α : Type u} → [LT α] → α → α → Prop

Docstring: `a > b` is an abbreviation for `b < a`. 

Conventions for notations in identifiers:

 * The recommended spelling of `>` in identifiers is `gt`.

## BASE-LIBRARY REF instDecidableAnd
{p q : Prop} → [dp : Decidable p] → [dq : Decidable q] → Decidable (p ∧ q)

## BASE-LIBRARY REF Fin.decLt
{n : ℕ} → (a b : Fin n) → Decidable (a < b)

## BASE-LIBRARY REF Finset.univ
{α : Type u_1} → [Fintype α] → Finset α

Docstring: `univ` is the universal finite set of type `Finset α` implied from
the assumption `Fintype α`. 

## BASE-LIBRARY REF Fin.fintype
(n : ℕ) → Fintype (Fin n)

## INFORMAL STATEMENT
prop.perm.lehmer.lex

Let $\sigma \in S_{n}$ and $\tau \in S_{n}$ be such that 

\[  \left(\sigma \left(1\right),\sigma \left(2\right),\ldots ,\sigma \left( n\right)\right) <_{\operatorname {lex}}\left(\tau \left(1\right) ,\tau \left(2\right),\ldots ,\tau \left(n\right)\right).  \]

 Then, 

\[  \left(\ell _{1}\left(\sigma \right),\ell _{2}\left(\sigma \right) ,\ldots ,\ell _{n}\left(\sigma \right)\right) <_{\operatorname {lex}}\left( \ell _{1}\left(\tau \right),\ell _{2}\left(\tau \right),\ldots ,\ell _{n}\left(\tau \right)\right).  \]

 (In other words, $L\left(\sigma \right) <_{\operatorname {lex}} L\left( \tau \right)$.)

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.lehmer.lex-ord
def.perm.lehmer.lex-ord

Let $\left(a_{1},a_{2},\ldots ,a_{n}\right)$ and $\left(b_{1},b_{2},\ldots ,b_{n}\right)$ be two $n$-tuples of integers. We say that 

\[  \left(a_{1},a_{2},\ldots ,a_{n}\right) <_{\operatorname {lex}}\left( b_{1},b_{2},\ldots ,b_{n}\right)  \]

 if and only if 

\begin{itemize} \item there exists some $k\in \left[n\right]$ such that $a_{k}\neq b_{k}$, and 

\item the \textbf{smallest} such $k$ satisfies $a_{k}<b_{k}$. 

\end{itemize}

 The relation $<_{\operatorname {lex}}$ is a strict total order on $\mathbb {Z}^n$ (the lexicographic order).

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.notations
def.perm.notations

Let $n \in \mathbb {N}$ and $\sigma \in S_n$. We introduce three notations for $\sigma $: 

\textbf{(a)} A \emph{two-line notation} of $\sigma $ means a $2 \times n$-array 

\[  \begin{pmatrix}  p_1 

&  p_2 

&  \cdots 

&  p_n 

\\ \sigma (p_1) 

&  \sigma (p_2) 

&  \cdots 

&  \sigma (p_n) 

\end{pmatrix},  \]

 where the entries $p_1, p_2, \ldots , p_n$ of the top row are the $n$ elements of $[n]$ in some order. Commonly, we pick $p_i = i$. 

\textbf{(b)} The \emph{one-line notation} (short, \emph{OLN}) of $\sigma $ means the $n$-tuple $(\sigma (1), \sigma (2), \ldots , \sigma (n))$. 

\textbf{(c)} The \emph{cycle digraph} of $\sigma $ is the directed graph with vertices $1, 2, \ldots , n$ and arcs $i \to \sigma (i)$ for all $i \in [n]$.

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
  "verdict": "faithful",
  "justification": "The target quantifies over exactly two permutations of an n-element ordered set, `\u2200 {n : \u2115} (\u03c3 \u03c4 : Equiv.Perm (Fin n))`, and assumes lexicographic comparison of their one-line values: `lexLt (fun i => \u2191\u2191(\u03c3 i)) (fun i => \u2191\u2191(\u03c4 i))`. By the body of `lexLt`, this means `\u2203 k, (\u2200 i < k, a i = b i) \u2227 a k < b k`, which is equivalent to the informal definition that the smallest differing coordinate has the smaller entry. Its conclusion applies the same relation to `lehmerEntry \u03c3` and `lehmerEntry \u03c4`. The dependency body `lehmerEntry \u03c3 i := {j | i < j \u2227 \u03c3 i > \u03c3 j}.card` exactly matches the informal definition of `\u2113_i(\u03c3)` as the number of later positions carrying smaller values. The use of zero-based `Fin n` rather than `[n] = {1,\u2026,n}` is only an order-preserving reindexing of the same n positions and values, so it does not change lexicographic order or Lehmer entries. The casts to `\u2124` merely place the natural-valued coordinates in the integer tuples required by `lexLt`. There are no added mathematical hypotheses or narrowed quantifiers."
}