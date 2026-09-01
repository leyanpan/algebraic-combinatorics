## TARGET Nat.Partition.partsCount_one (theorem) — ELABORATED SIGNATURE
∀ (n : ℕ), Nat.Partition.partsCount 1 n = if n > 0 then 1 else 0

Docstring: `p_1(n) = [n > 0]`: the only partition of a positive `n` into 1 part is `(n)`.
(Proposition \ref{prop.pars.basics} (d)) 

## TARGET Nat.Partition.partsCount_two (theorem) — ELABORATED SIGNATURE
∀ (n : ℕ), Nat.Partition.partsCount 2 n = n / 2

Docstring: `p_2(n) = ⌊n/2⌋` for `n ∈ ℕ`.
(Proposition \ref{prop.pars.basics} (f))

The partitions of n into 2 parts are (n-1,1), (n-2,2), ..., (⌈n/2⌉, ⌊n/2⌋). 

## TARGET Nat.Partition.partsCount_recurrence (theorem) — ELABORATED SIGNATURE
∀ {k n : ℕ},
  k > 0 →
    n > 0 → Nat.Partition.partsCount k n = Nat.Partition.partsCount k (n - k) + Nat.Partition.partsCount (k - 1) (n - 1)

Docstring: The recurrence relation for partition numbers:
`p_k(n) = p_k(n-k) + p_{k-1}(n-1)` for `k > 0` and `n > 0`.
(Proposition \ref{prop.pars.basics} (e))

**Note:** The hypothesis `n > 0` is required because in natural number arithmetic,
`0 - 1 = 0`, so the recurrence fails for `k = 1, n = 0`:
- LHS = `p_1(0) = 0`
- RHS = `p_1(0) + p_0(0) = 0 + 1 = 1`

This classifies partitions into:
- Type 1: partitions with 1 as a part (bijection with partitions of n-1 into k-1 parts)
- Type 2: partitions without 1 (subtract 1 from each part → partitions of n-k into k parts)

The proof requires establishing two bijections:
1. {partitions of n into k parts containing 1} ↔ {partitions of n-1 into k-1 parts}
   via removeOne/addOne
2. {partitions of n into k parts not containing 1} ↔ {partitions of n-k into k parts}
   via subtractOneFromEach/addOneToEach 

## TARGET Nat.Partition.partsCount_of_gt (theorem) — ELABORATED SIGNATURE
∀ {k n : ℕ}, k > n → Nat.Partition.partsCount k n = 0

Docstring: There are no partitions of `n` into more than `n` parts.
(Proposition \ref{prop.pars.basics} (b)) 

## TARGET Nat.Partition.partitionCount_sum (theorem) — ELABORATED SIGNATURE
∀ (n : ℕ), Nat.Partition.partitionCount n = ∑ k ∈ Finset.range (n + 1), Nat.Partition.partsCount k n

Docstring: `p(n) = p_0(n) + p_1(n) + ... + p_n(n)` for `n ∈ ℕ`.
(Proposition \ref{prop.pars.basics} (g)) 

## TARGET Nat.Partition.partsCount_zero (theorem) — ELABORATED SIGNATURE
∀ (n : ℕ), Nat.Partition.partsCount 0 n = if n = 0 then 1 else 0

Docstring: `p_0(n) = [n = 0]`: the only partition into 0 parts is the empty partition of 0.
(Proposition \ref{prop.pars.basics} (c)) 

## PROJECT DEPENDENCY Nat.Partition.partsCount (def)
ℕ → ℕ → ℕ

Body:
fun k n => {p | p.parts.card = k}.card

Docstring: The function `p_k(n)`: the number of partitions of `n` into exactly `k` parts.
(Definition \ref{def.pars.pn-pkn} (a)) 

## PROJECT DEPENDENCY Nat.Partition.partitionCount (def)
ℕ → ℕ

Body:
fun n => Fintype.card n.Partition

Docstring: The partition function `p(n)`: the number of partitions of `n`.
(Definition \ref{def.pars.pn-pkn} (b)) 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


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

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

## BASE-LIBRARY REF ite
{α : Sort u} → (c : Prop) → [h : Decidable c] → α → α → α

Docstring: `if c then t else e` is notation for `ite c t e`, "if-then-else", which decides to
return `t` or `e` depending on whether `c` is true or false. The explicit argument
`c : Prop` does not have any actual computational content, but there is an additional
`[Decidable c]` argument synthesized by typeclass inference which actually
determines how to evaluate `c` to true or false. Write `if h : c then t else e`
instead for a "dependent if-then-else" `dite`, which allows `t`/`e` to use the fact
that `c` is true/false.


## BASE-LIBRARY REF GT.gt
{α : Type u} → [LT α] → α → α → Prop

Docstring: `a > b` is an abbreviation for `b < a`. 

Conventions for notations in identifiers:

 * The recommended spelling of `>` in identifiers is `gt`.

## BASE-LIBRARY REF instLTNat
LT ℕ

## BASE-LIBRARY REF Nat.decLt
(n m : ℕ) → Decidable (n < m)

Docstring: A decision procedure for strict inequality of natural numbers, usually accessed via the
`DecidableLT Nat` instance.

Examples:
 * `(if 3 < 4 then "yes" else "no") = "yes"`
 * `(if 4 < 4 then "yes" else "no") = "no"`
 * `(if 6 < 4 then "yes" else "no") = "no"`
 * `show 5 < 12 by decide`


## BASE-LIBRARY REF HDiv.hDiv
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HDiv α β γ] → α → β → γ

Docstring: `a / b` computes the result of dividing `a` by `b`.
The meaning of this notation is type-dependent.
* For most types like `Nat`, `Int`, `Rat`, `Real`, `a / 0` is defined to be `0`.
* For `Nat`, `a / b` rounds downwards.
* For `Int`, `a / b` rounds downwards if `b` is positive or upwards if `b` is negative.
  It is implemented as `Int.ediv`, the unique function satisfying
  `a % b + b * (a / b) = a` and `0 ≤ a % b < natAbs b` for `b ≠ 0`.
  Other rounding conventions are available using the functions
  `Int.fdiv` (floor rounding) and `Int.tdiv` (truncation rounding).
* For `Float`, `a / 0` follows the IEEE 754 semantics for division,
  usually resulting in `inf` or `nan`. 

Conventions for notations in identifiers:

 * The recommended spelling of `/` in identifiers is `div`.

## BASE-LIBRARY REF instHDiv
{α : Type u_1} → [Div α] → HDiv α α α

## BASE-LIBRARY REF Nat.instDiv
Div ℕ

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

## BASE-LIBRARY REF Finset.sum
{ι : Type u_1} → {M : Type u_3} → [AddCommMonoid M] → Finset ι → (ι → M) → M

Docstring: `∑ x ∈ s, f x` is the sum of `f x` as `x` ranges over the elements
of the finite set `s`.

When the index type is a `Fintype`, the notation `∑ x, f x`, is a shorthand for
`∑ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF Nat.instAddCommMonoid
AddCommMonoid ℕ

## BASE-LIBRARY REF Finset.range
ℕ → Finset ℕ

Docstring: `range n` is the set of natural numbers less than `n`. 

## BASE-LIBRARY REF instDecidableEqNat
DecidableEq ℕ

## BASE-LIBRARY REF Finset.card
{α : Type u_1} → Finset α → ℕ

Docstring: `s.card` is the number of elements of `s`, aka its cardinality.

The notation `#s` can be accessed in the `Finset` locale. 

## BASE-LIBRARY REF Nat.Partition
ℕ → Type

Docstring: A partition of `n` is a multiset of positive integers summing to `n`. 

## BASE-LIBRARY REF Finset.filter
{α : Type u_1} → (p : α → Prop) → [DecidablePred p] → Finset α → Finset α

Docstring: `Finset.filter p s` is the set of elements of `s` that satisfy `p`.

For example, one can use `s.filter (· ∈ t)` to get the intersection of `s` with `t : Set α`
as a `Finset α` (when a `DecidablePred (· ∈ t)` instance is available). 

## BASE-LIBRARY REF Multiset.card
{α : Type u_1} → Multiset α → ℕ

Docstring: The cardinality of a multiset is the sum of the multiplicities
of all its elements, or simply the length of the underlying list. 

## BASE-LIBRARY REF Nat.Partition.parts
{n : ℕ} → n.Partition → Multiset ℕ

Docstring: positive integers summing to `n` 

## BASE-LIBRARY REF Finset.univ
{α : Type u_1} → [Fintype α] → Finset α

Docstring: `univ` is the universal finite set of type `Finset α` implied from
the assumption `Fintype α`. 

## BASE-LIBRARY REF Nat.Partition.instFintype
(n : ℕ) → Fintype n.Partition

Docstring: Show there are finitely many partitions by considering the surjection from compositions to
partitions.


## BASE-LIBRARY REF Fintype.card
(α : Type u_4) → [Fintype α] → ℕ

Docstring: `card α` is the number of elements in `α`, defined when `α` is a fintype. 

## INFORMAL STATEMENT
prop.pars.basics

Let $n\in \mathbb {Z}$ and $k\in \mathbb {N}$. \medskip 

\textbf{(a)} We have $p_{k}\left( n\right) =0$ whenever $n<0$ and $k\in \mathbb {N}$. \medskip 

\textbf{(b)} We have $p_{k}\left( n\right) =0$ whenever $k>n$. \medskip 

\textbf{(c)} We have $p_{0}\left( n\right) =\left[ n=0 \right]$. \medskip 

\textbf{(d)} We have $p_{1}\left( n\right) =\left[ n>0 \right]$. \medskip 

\textbf{(e)} We have $p_{k}\left( n\right) =p_{k}\left( n-k\right) +p_{k-1}\left( n-1\right) $ whenever $k>0$. \medskip 

\textbf{(f)} We have $p_{2}\left( n\right) =\left\lfloor n/2\right\rfloor $ whenever $n\in \mathbb {N}$. \medskip 

\textbf{(g)} We have $p\left( n\right) =p_{0}\left( n\right) +p_{1}\left( n\right) +\cdots +p_{n}\left( n\right) $ whenever $n\in \mathbb {N}$. \medskip 

\textbf{(h)} We have $p\left( n\right) =0$ whenever $n<0$.

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.pars.pn-pkn
def.pars.pn-pkn

\textbf{(a)} Let $n\in \mathbb {Z}$ and $k\in \mathbb {N}$. Then, we set

\[  p_{k}\left( n\right) :=\left( \text{\#  of partitions of }n\text{ into }k\text{ parts}\right) .  \]

\textbf{(b)} Let $n\in \mathbb {Z}$. Then, we set

\[  p\left( n\right) :=\left( \text{\#  of partitions of }n\right) .  \]

 This is called the $n$\emph{-th partition number}.

## VERDICT
{
  "verdict": "unstatable",
  "justification": "The blueprint fixes `n \u2208 \u2124` and includes the negative-index clauses \u201c`p_k(n)=0 whenever n<0`\u201d and \u201c`p(n)=0 whenever n<0`\u201d. It also states the recurrence for every integer `n` whenever `k>0`. But the project dependencies are restricted to naturals: `Nat.Partition.partsCount : \u2115 \u2192 \u2115 \u2192 \u2115` and `Nat.Partition.partitionCount : \u2115 \u2192 \u2115`, so negative arguments cannot even be supplied. Correspondingly, the targets quantify only `n : \u2115`, omit clauses (a) and (h), and `partsCount_recurrence` adds the contentful binder `n > 0`; this is needed only because its expressions use saturating natural subtraction, whereas the blueprint uses integer subtraction and requires no such hypothesis. Thus the supplied declarations cannot express the full proposition, rather than merely proving a different statable version. To make it faithful, add integer-indexed definitions, e.g. `partsCount : \u2115 \u2192 \u2124 \u2192 \u2115` and `partitionCount : \u2124 \u2192 \u2115`, agreeing with `Nat.Partition` counts on nonnegative indices and returning zero on negative indices; then state (a)\u2013(h), with recurrence quantified over `n : \u2124` and no `n > 0` assumption. The natural-only targets for (f) and (g) are compatible with those particular clauses, but they do not remedy the package-level mismatch."
}