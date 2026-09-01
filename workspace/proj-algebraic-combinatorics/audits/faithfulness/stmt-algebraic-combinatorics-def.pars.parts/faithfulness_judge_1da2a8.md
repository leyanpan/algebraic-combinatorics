## TARGET Nat.Partition.parts_pos' (theorem) — ELABORATED SIGNATURE
∀ {n : ℕ} (p : n.Partition), ∀ i ∈ p.parts, 0 < i

Docstring: All parts of a partition are positive.
(Definition \ref{def.pars.parts} (a) - "tuple of positive integers")

This is a fundamental property: every entry in a partition is ≥ 1.
This is the defining property that distinguishes partitions from weak compositions. 

## TARGET Nat.Partition.eq_iff_parts_eq (theorem) — ELABORATED SIGNATURE
∀ {n : ℕ} (p q : n.Partition), p = q ↔ p.parts = q.parts

Docstring: Two partitions are equal iff their parts are equal.
(Definition \ref{def.pars.parts} - partitions are determined by their parts) 

## TARGET Nat.Partition.ofList' (def) — ELABORATED SIGNATURE
{n : ℕ} → (l : List ℕ) → (∀ i ∈ l, 0 < i) → l.sum = n → n.Partition

Body:
fun {n} l hl_pos hl_sum => { parts := ↑l, parts_pos := ⋯, parts_sum := ⋯ }

Docstring: Constructing a partition from a list of positive integers.
(Definition \ref{def.pars.parts} (a) - the tuple representation)

Given a list of positive integers that sums to n, we can construct a partition of n.
The list need not be sorted; Mathlib's `Partition` uses multisets. 

## TARGET Nat.Partition.size_eq (theorem) — ELABORATED SIGNATURE
∀ {n : ℕ} (p : n.Partition), p.parts.sum = n

Docstring: The size of a partition is the sum of its parts.
(Definition \ref{def.pars.parts} (c))

For a partition of n, the size is n. This is guaranteed by `Partition.parts_sum`.
The type `Partition n` itself encodes that the partition has size n. 

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

## BASE-LIBRARY REF Multiset
Type u → Type u

Docstring: `Multiset α` is the quotient of `List α` by list permutation. The result
is a type of finite sets with duplicates allowed. 

## BASE-LIBRARY REF Multiset.instMembership
{α : Type u_1} → Membership α (Multiset α)

## BASE-LIBRARY REF Nat.Partition.parts
{n : ℕ} → n.Partition → Multiset ℕ

Docstring: positive integers summing to `n` 

## BASE-LIBRARY REF LT.lt
{α : Type u} → [self : LT α] → α → α → Prop

Docstring: The less-than relation: `x < y` 

Conventions for notations in identifiers:

 * The recommended spelling of `<` in identifiers is `lt`.

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

## BASE-LIBRARY REF Iff
Prop → Prop → Prop

Docstring: If and only if, or logical bi-implication. `a ↔ b` means that `a` implies `b` and vice versa.
By `propext`, this implies that `a` and `b` are equal and hence any expression involving `a`
is equivalent to the corresponding expression with `b` instead.


Conventions for notations in identifiers:

 * The recommended spelling of `↔` in identifiers is `iff`.

 * The recommended spelling of `<->` in identifiers is `iff` (prefer `↔` over `<->`).

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

## BASE-LIBRARY REF List.sum
{α : Type u_1} → [Add α] → [Zero α] → List α → α

Docstring: Computes the sum of the elements of a list.

Examples:
* `[a, b, c].sum = a + (b + (c + 0))`
* `[1, 2, 5].sum = 8`


## BASE-LIBRARY REF instAddNat
Add ℕ

## BASE-LIBRARY REF MulZeroClass.toZero
{M₀ : Type u} → [self : MulZeroClass M₀] → Zero M₀

## BASE-LIBRARY REF Nat.instMulZeroClass
MulZeroClass ℕ

## BASE-LIBRARY REF Nat.Partition.mk
{n : ℕ} → (parts : Multiset ℕ) → (∀ {i : ℕ}, i ∈ parts → 0 < i) → parts.sum = n → n.Partition

## BASE-LIBRARY REF Multiset.ofList
{α : Type u_1} → List α → Multiset α

Docstring: The quotient map from `List α` to `Multiset α`. 

## BASE-LIBRARY REF Multiset.sum
{M : Type u_3} → [AddCommMonoid M] → Multiset M → M

Docstring: Sum of a multiset given a commutative additive monoid structure on `M`.
`sum {a, b, c} = a + b + c` 

## BASE-LIBRARY REF Nat.instAddCommMonoid
AddCommMonoid ℕ

## INFORMAL STATEMENT
def.pars.parts

\textbf{(a)} An \emph{(integer) partition} means a (finite) weakly decreasing tuple of positive integers – i.e., a finite tuple $\left( \lambda _{1},\lambda _{2},\ldots ,\lambda _{m}\right) $ of positive integers such that $\lambda _{1}\geq \lambda _{2}\geq \cdots \geq \lambda _{m}$. 

Thus, partitions are the same as weakly decreasing compositions. Hence, the notions of \emph{size} and \emph{length} of a partition are automatically defined, since we have defined them for compositions (in Definition \ref{def.fps.comps}). \medskip 

\textbf{(b)} The \emph{parts} of a partition $\left( \lambda _{1},\lambda _{2},\ldots ,\lambda _{m}\right) $ are simply its entries $\lambda _{1},\lambda _{2},\ldots ,\lambda _{m}$. \medskip 

\textbf{(c)} Let $n\in \mathbb {Z}$. A \emph{partition of }$n$ means a partition whose size is $n$. \medskip 

\textbf{(d)} Let $n\in \mathbb {Z}$ and $k\in \mathbb {N}$. A \emph{partition of }$n$\emph{ into }$k$\emph{ parts} is a partition whose size is $n$ and whose length is $k$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.comps
def.fps.comps

\textbf{(a)} An \emph{(integer) composition} means a (finite) tuple of positive integers. \medskip 

\textbf{(b)} The \emph{size} of an integer composition $\alpha =\left( \alpha _{1},\alpha _{2},\ldots ,\alpha _{m}\right) $ is defined to be the integer $\alpha _{1}+\alpha _{2}+\cdots +\alpha _{m}$. It is written $\left\vert \alpha \right\vert $. \medskip 

\textbf{(c)} The \emph{length} of an integer composition $\alpha =\left( \alpha _{1},\alpha _{2},\ldots ,\alpha _{m}\right) $ is defined to be the integer $m$. It is written $\ell \left( \alpha \right) $. \medskip 

\textbf{(d)} Let $n\in \mathbb {N}$. A \emph{composition of }$n$ means a composition whose size is $n$. \medskip 

\textbf{(e)} Let $n\in \mathbb {N}$ and $k\in \mathbb {N}$. A \emph{composition of }$n$\emph{ into }$k$\emph{ parts} is a composition whose size is $n$ and whose length is $k$.

## VERDICT
{
  "verdict": "drift",
  "justification": "The blueprint explicitly quantifies clause (c) over integers: \u201cLet $n\\in\\mathbb Z$. A partition of $n$ means\u2026\u201d, whereas every relevant formal declaration is restricted by `{n : \u2115}`, through the dependency `Nat.Partition : \u2115 \u2192 Type`; for example, `size_eq` has `\u2200 {n : \u2115} (p : n.Partition), p.parts.sum = n`, and `ofList'` likewise constructs only `n.Partition` for `n : \u2115`. This is a narrowed index range. The multiset representation itself is compatible with weakly decreasing tuples\u2014each finite multiset of positive naturals has a canonical decreasing enumeration\u2014and `0 < i` plus the sum equation correctly encode positivity and size. However, the formal declarations cannot even state the blueprint\u2019s notion of a partition indexed by a negative integer (which should have no inhabitants). To make the formalization faithful, replace or wrap `Nat.Partition` with a type indexed by `\u2124`, with parts summing to the integer index (and hence empty for negative indices), or change the blueprint\u2019s binder from `n \u2208 \u2124` to `n \u2208 \u2115`."
}