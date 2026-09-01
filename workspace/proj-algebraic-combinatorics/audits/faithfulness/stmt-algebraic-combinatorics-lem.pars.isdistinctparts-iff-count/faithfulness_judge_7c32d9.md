## TARGET Nat.Partition.isDistinctParts_iff_count_le_one (theorem) — ELABORATED SIGNATURE
∀ {n : ℕ} (p : n.Partition), p.IsDistinctParts ↔ ∀ (i : ℕ), Multiset.count i p.parts ≤ 1

Docstring: Alternative characterization: a partition is into distinct parts iff
each part appears at most once. 

## PROJECT DEPENDENCY Nat.Partition.IsDistinctParts (def)
{n : ℕ} → n.Partition → Prop

Body:
fun {n} p => p.parts.Nodup

Docstring: A partition into distinct parts is a partition whose parts are all different.
(Definition \ref{def.pars.odd-dist-parts} (b))

For example, (7), (6,1), (5,2), (4,3), (4,2,1) are the partitions of 7 into
distinct parts. Note that repeated parts are not allowed. 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF Nat.Partition
ℕ → Type

Docstring: A partition of `n` is a multiset of positive integers summing to `n`. 

## BASE-LIBRARY REF Iff
Prop → Prop → Prop

Docstring: If and only if, or logical bi-implication. `a ↔ b` means that `a` implies `b` and vice versa.
By `propext`, this implies that `a` and `b` are equal and hence any expression involving `a`
is equivalent to the corresponding expression with `b` instead.


Conventions for notations in identifiers:

 * The recommended spelling of `↔` in identifiers is `iff`.

 * The recommended spelling of `<->` in identifiers is `iff` (prefer `↔` over `<->`).

## BASE-LIBRARY REF LE.le
{α : Type u} → [self : LE α] → α → α → Prop

Docstring: The less-equal relation: `x ≤ y` 

Conventions for notations in identifiers:

 * The recommended spelling of `≤` in identifiers is `le`.

 * The recommended spelling of `<=` in identifiers is `le` (prefer `≤` over `<=`).

## BASE-LIBRARY REF instLENat
LE ℕ

## BASE-LIBRARY REF Multiset.count
{α : Type u_1} → [DecidableEq α] → α → Multiset α → ℕ

Docstring: `count a s` is the multiplicity of `a` in `s`. 

## BASE-LIBRARY REF instDecidableEqNat
DecidableEq ℕ

## BASE-LIBRARY REF Nat.Partition.parts
{n : ℕ} → n.Partition → Multiset ℕ

Docstring: positive integers summing to `n` 

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

## BASE-LIBRARY REF Multiset.Nodup
{α : Type u_1} → Multiset α → Prop

Docstring: `Nodup s` means that `s` has no duplicates, i.e. the multiplicity of
any element is at most 1. 

## INFORMAL STATEMENT
lem.pars.isDistinctParts-iff-count

\leanhelper  A partition is into distinct parts iff each part appears at most once.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.comps
def.fps.comps

\textbf{(a)} An \emph{(integer) composition} means a (finite) tuple of positive integers. \medskip 

\textbf{(b)} The \emph{size} of an integer composition $\alpha =\left( \alpha _{1},\alpha _{2},\ldots ,\alpha _{m}\right) $ is defined to be the integer $\alpha _{1}+\alpha _{2}+\cdots +\alpha _{m}$. It is written $\left\vert \alpha \right\vert $. \medskip 

\textbf{(c)} The \emph{length} of an integer composition $\alpha =\left( \alpha _{1},\alpha _{2},\ldots ,\alpha _{m}\right) $ is defined to be the integer $m$. It is written $\ell \left( \alpha \right) $. \medskip 

\textbf{(d)} Let $n\in \mathbb {N}$. A \emph{composition of }$n$ means a composition whose size is $n$. \medskip 

\textbf{(e)} Let $n\in \mathbb {N}$ and $k\in \mathbb {N}$. A \emph{composition of }$n$\emph{ into }$k$\emph{ parts} is a composition whose size is $n$ and whose length is $k$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.pars.odd-dist-parts
def.pars.odd-dist-parts

Let $n\in \mathbb {Z}$. \medskip 

\textbf{(a)} A \emph{partition of }$n$\emph{ into odd parts} means a partition of $n$ whose all parts are odd. \medskip 

\textbf{(b)} A \emph{partition of }$n$\emph{ into distinct parts} means a partition of $n$ whose parts are distinct. \medskip 

\textbf{(c)} Let

\begin{align*}  p_{\operatorname {odd}}\left( n\right) &  :=\left( \text{\#  of partitions of }n\text{ into odd parts}\right) \  \  \  \  \  \  \  \  \  \  \text{and}\\ p_{\operatorname {dist}}\left( n\right) &  :=\left( \text{\#  of partitions of }n\text{ into distinct parts}\right) . \end{align*}

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.pars.parts
def.pars.parts

\textbf{(a)} An \emph{(integer) partition} means a (finite) weakly decreasing tuple of positive integers – i.e., a finite tuple $\left( \lambda _{1},\lambda _{2},\ldots ,\lambda _{m}\right) $ of positive integers such that $\lambda _{1}\geq \lambda _{2}\geq \cdots \geq \lambda _{m}$. 

Thus, partitions are the same as weakly decreasing compositions. Hence, the notions of \emph{size} and \emph{length} of a partition are automatically defined, since we have defined them for compositions (in Definition \ref{def.fps.comps}). \medskip 

\textbf{(b)} The \emph{parts} of a partition $\left( \lambda _{1},\lambda _{2},\ldots ,\lambda _{m}\right) $ are simply its entries $\lambda _{1},\lambda _{2},\ldots ,\lambda _{m}$. \medskip 

\textbf{(c)} Let $n\in \mathbb {Z}$. A \emph{partition of }$n$ means a partition whose size is $n$. \medskip 

\textbf{(d)} Let $n\in \mathbb {Z}$ and $k\in \mathbb {N}$. A \emph{partition of }$n$\emph{ into }$k$\emph{ parts} is a partition whose size is $n$ and whose length is $k$.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The target states `\u2200 {n : \u2115} (p : n.Partition), p.IsDistinctParts \u2194 \u2200 (i : \u2115), Multiset.count i p.parts \u2264 1`, exactly matching \u201cA partition is into distinct parts iff each part appears at most once.\u201d The dependency defines `p.IsDistinctParts` as `p.parts.Nodup`, and `Multiset.Nodup` means precisely that every element has multiplicity at most 1. Quantifying over every `i : \u2115`, rather than only over values occurring as parts, does not strengthen the condition materially, since absent values have count zero. Using `n : \u2115` is faithful to the represented setting: partitions have positive integer parts, hence nonnegative size; negative integers admit no such partitions."
}