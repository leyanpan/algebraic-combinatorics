## TARGET Nat.Partition.isOddParts_iff (theorem) — ELABORATED SIGNATURE
∀ {n : ℕ} (p : n.Partition), p.IsOddParts ↔ ∀ i ∈ p.parts, Odd i

Docstring: A partition is into odd parts iff all its parts satisfy `Odd`. 

## PROJECT DEPENDENCY Nat.Partition.IsOddParts (def)
{n : ℕ} → n.Partition → Prop

Body:
fun {n} p => ∀ i ∈ p.parts, Odd i

Docstring: A partition into odd parts is a partition whose all parts are odd.
(Definition \ref{def.pars.odd-dist-parts} (a))

For example, (7), (5,1,1), (3,3,1), (3,1,1,1,1), (1,1,1,1,1,1,1) are the
partitions of 7 into odd parts. 

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

## BASE-LIBRARY REF Odd
{α : Type u_2} → [Semiring α] → α → Prop

Docstring: An element `a` of a semiring is odd if there exists `k` such `a = 2*k + 1`. 

## BASE-LIBRARY REF Nat.instSemiring
Semiring ℕ

## INFORMAL STATEMENT
lem.pars.isOddParts-iff

\leanhelper  A partition is into odd parts iff all its parts are odd.

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
  "justification": "The informal statement says, \u201cA partition is into odd parts iff all its parts are odd.\u201d The target states exactly `\u2200 {n : \u2115} (p : n.Partition), p.IsOddParts \u2194 \u2200 i \u2208 p.parts, Odd i`. Moreover, the dependency `Nat.Partition.IsOddParts` is defined by `fun {n} p => \u2200 i \u2208 p.parts, Odd i`, matching informal Definition (a): a partition into odd parts is one \u201cwhose all parts are odd.\u201d Thus both sides of the equivalence coincide definitionally. Restricting the index to `n : \u2115` is inherent in the available `Nat.Partition : \u2115 \u2192 Type`; it introduces no additional hypothesis on represented partitions."
}