## TARGET Nat.Partition.removeOne (def) — ELABORATED SIGNATURE
{n : ℕ} → (p : n.Partition) → 1 ∈ p.parts → (n - 1).Partition

Body:
fun {n} p h => Nat.Partition.ofSums (n - 1) (p.parts.erase 1) ⋯

Docstring: Remove one 1 from a partition containing 1 to get a partition of n-1. 

## TARGET Nat.Partition.addOne (def) — ELABORATED SIGNATURE
{n : ℕ} → n.Partition → (n + 1).Partition

Body:
fun {n} p => Nat.Partition.ofSums (n + 1) (1 ::ₘ p.parts) ⋯

Docstring: Add one 1 to a partition to get a partition of n+1. 

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

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

## BASE-LIBRARY REF HSub.hSub
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HSub α β γ] → α → β → γ

Docstring: `a - b` computes the difference of `a` and `b`.
The meaning of this notation is type-dependent.
* For natural numbers, this operator saturates at 0: `a - b = 0` when `a ≤ b`. 

Conventions for notations in identifiers:

 * The recommended spelling of `-` in identifiers is `sub` (when used as a binary operator).

## BASE-LIBRARY REF instHSub
{α : Type u_1} → [Sub α] → HSub α α α

## BASE-LIBRARY REF instSubNat
Sub ℕ

## BASE-LIBRARY REF Nat.Partition.ofSums
(n : ℕ) → (l : Multiset ℕ) → l.sum = n → n.Partition

Docstring: Given a multiset which sums to `n`, construct a partition of `n` with the same multiset, but
without the zeros.


## BASE-LIBRARY REF Multiset.erase
{α : Type u_1} → [DecidableEq α] → Multiset α → α → Multiset α

Docstring: `erase s a` is the multiset that subtracts 1 from the multiplicity of `a`. 

## BASE-LIBRARY REF instDecidableEqNat
DecidableEq ℕ

## BASE-LIBRARY REF HAdd.hAdd
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HAdd α β γ] → α → β → γ

Docstring: `a + b` computes the sum of `a` and `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `+` in identifiers is `add`.

## BASE-LIBRARY REF instHAdd
{α : Type u_1} → [Add α] → HAdd α α α

## BASE-LIBRARY REF instAddNat
Add ℕ

## BASE-LIBRARY REF Multiset.cons
{α : Type u_1} → α → Multiset α → Multiset α

Docstring: `cons a s` is the multiset which contains `s` plus one more instance of `a`. 

## INFORMAL STATEMENT
def.pars.removeOne-addOne

\leanhelper  Given a partition of $n$ that contains $1$ as a part, removing one copy of~ $1$ yields a partition of $n-1$. Conversely, adding one copy of~ $1$ to a partition of $n$ yields a partition of $n+1$.

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
  "verdict": "faithful",
  "justification": "The two declarations exactly implement the two directions of the blueprint. For removal, the binder `{n : \u2115} \u2192 (p : n.Partition) \u2192 1 \u2208 p.parts` matches \u201ca partition of n that contains 1 as a part,\u201d and the result `(n - 1).Partition` matches \u201cyields a partition of n\u22121.\u201d Its body uses `p.parts.erase 1`, and `Multiset.erase` \u201csubtracts 1 from the multiplicity,\u201d so precisely one copy is removed. For addition, `{n : \u2115} \u2192 n.Partition \u2192 (n + 1).Partition` matches the converse, and the body uses `1 ::\u2098 p.parts`, which adds exactly one occurrence of 1. Although natural subtraction saturates at zero, the removal hypothesis together with `Nat.Partition` being a multiset of positive integers summing to `n` ensures the relevant case has `n \u2265 1`. The use of `\u2115` does not lose realizable integer partitions here, since a finite tuple of positive integers cannot have negative size."
}