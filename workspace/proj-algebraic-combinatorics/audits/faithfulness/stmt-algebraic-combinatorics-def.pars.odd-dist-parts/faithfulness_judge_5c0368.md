## TARGET Nat.Partition.IsDistinctParts (def) — ELABORATED SIGNATURE
{n : ℕ} → n.Partition → Prop

Body:
fun {n} p => p.parts.Nodup

Docstring: A partition into distinct parts is a partition whose parts are all different.
(Definition \ref{def.pars.odd-dist-parts} (b))

For example, (7), (6,1), (5,2), (4,3), (4,2,1) are the partitions of 7 into
distinct parts. Note that repeated parts are not allowed. 

## TARGET Nat.Partition.distinctPartsCount (def) — ELABORATED SIGNATURE
ℕ → ℕ

Body:
fun n => (Nat.Partition.distincts n).card

Docstring: The number of partitions of n into distinct parts: `p_dist(n)`.
(Definition \ref{def.pars.odd-dist-parts} (c))

This counts the partitions of n where all parts are different (no repeats).
Uses Mathlib's `Nat.Partition.distincts` which filters partitions by
the `Nodup` predicate on the parts multiset. 

## TARGET Nat.Partition.IsOddParts (def) — ELABORATED SIGNATURE
{n : ℕ} → n.Partition → Prop

Body:
fun {n} p => ∀ i ∈ p.parts, Odd i

Docstring: A partition into odd parts is a partition whose all parts are odd.
(Definition \ref{def.pars.odd-dist-parts} (a))

For example, (7), (5,1,1), (3,3,1), (3,1,1,1,1), (1,1,1,1,1,1,1) are the
partitions of 7 into odd parts. 

## TARGET Nat.Partition.oddPartsCount (def) — ELABORATED SIGNATURE
ℕ → ℕ

Body:
fun n => (Nat.Partition.odds n).card

Docstring: The number of partitions of n into odd parts: `p_odd(n)`.
(Definition \ref{def.pars.odd-dist-parts} (c))

This counts the partitions of n where every part is an odd number.
Uses Mathlib's `Nat.Partition.odds` which filters partitions by the
predicate `¬Even` (equivalent to `Odd` for positive integers). 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF Nat.Partition
ℕ → Type

Docstring: A partition of `n` is a multiset of positive integers summing to `n`. 

## BASE-LIBRARY REF Multiset.Nodup
{α : Type u_1} → Multiset α → Prop

Docstring: `Nodup s` means that `s` has no duplicates, i.e. the multiplicity of
any element is at most 1. 

## BASE-LIBRARY REF Nat.Partition.parts
{n : ℕ} → n.Partition → Multiset ℕ

Docstring: positive integers summing to `n` 

## BASE-LIBRARY REF Finset.card
{α : Type u_1} → Finset α → ℕ

Docstring: `s.card` is the number of elements of `s`, aka its cardinality.

The notation `#s` can be accessed in the `Finset` locale. 

## BASE-LIBRARY REF Nat.Partition.distincts
(n : ℕ) → Finset n.Partition

Docstring: The finset of those partitions in which each part is used at most once. 

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

## BASE-LIBRARY REF Odd
{α : Type u_2} → [Semiring α] → α → Prop

Docstring: An element `a` of a semiring is odd if there exists `k` such `a = 2*k + 1`. 

## BASE-LIBRARY REF Nat.instSemiring
Semiring ℕ

## BASE-LIBRARY REF Nat.Partition.odds
(n : ℕ) → Finset n.Partition

Docstring: The finset of those partitions in which every part is odd. 

## INFORMAL STATEMENT
def.pars.odd-dist-parts

Let $n\in \mathbb {Z}$. \medskip 

\textbf{(a)} A \emph{partition of }$n$\emph{ into odd parts} means a partition of $n$ whose all parts are odd. \medskip 

\textbf{(b)} A \emph{partition of }$n$\emph{ into distinct parts} means a partition of $n$ whose parts are distinct. \medskip 

\textbf{(c)} Let

\begin{align*}  p_{\operatorname {odd}}\left( n\right) &  :=\left( \text{\#  of partitions of }n\text{ into odd parts}\right) \  \  \  \  \  \  \  \  \  \  \text{and}\\ p_{\operatorname {dist}}\left( n\right) &  :=\left( \text{\#  of partitions of }n\text{ into distinct parts}\right) . \end{align*}

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

## VERDICT
{
  "verdict": "drift",
  "justification": "The informal statement quantifies over integers: \u201cLet $n\\in\\mathbb Z$,\u201d and defines both kinds of partitions and both counting functions for such $n$. All four Lean declarations restrict the index to naturals: `IsDistinctParts : {n : \u2115} \u2192 n.Partition \u2192 Prop`, `IsOddParts : {n : \u2115} \u2192 n.Partition \u2192 Prop`, and both counts have type `\u2115 \u2192 \u2115`. This is a narrowed domain and leaves the definitions for negative integers unspecified, so it is weaker than the blueprint. On natural indices, the bodies are faithful: `p.parts.Nodup` means no repeated parts; `\u2200 i \u2208 p.parts, Odd i` means every part is odd; and the cardinalities of `Nat.Partition.distincts n` and `Nat.Partition.odds n` give the stated counts. To make the package faithful, either the blueprint must say `n \u2208 \u2115`, or the formal declarations must use an integer-indexed notion of partition/count, with no partitions\u2014and hence count zero\u2014for negative indices."
}