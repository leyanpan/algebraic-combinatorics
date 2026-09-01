## TARGET Nat.Partition.partsAndLargestCountTotal_eq (theorem) — ELABORATED SIGNATURE
∀ (k ℓ : ℕ), k ≥ 1 → ℓ ≥ 1 → Nat.Partition.partsAndLargestCountTotal k ℓ = (k + ℓ - 2).choose (k - 1)

Docstring: Proposition \ref{prop.pars.qbinom.intro-count-binom}: For positive integers k and ℓ,
the number of partitions with exactly k parts and largest part ℓ equals C(k+ℓ-2, k-1).

**Proof outline**: A partition with k parts and largest part ℓ has the form
(ℓ, λ₂, ..., λₖ) where ℓ ≥ λ₂ ≥ ... ≥ λₖ ≥ 1.

The tuple (λ₂, ..., λₖ) is a weakly decreasing sequence of k-1 positive integers,
each at most ℓ. This is equivalent to choosing a (k-1)-element multisubset
of {1, 2, ..., ℓ}, which by the "stars and bars" formula equals
C(ℓ + (k-1) - 1, k-1) = C(k + ℓ - 2, k - 1).

Note: This formula is independent of the size n of the partition.

**Bijection details**:
- Forward: partition (ℓ, λ₂, ..., λₖ) ↦ multiset {λ₂-1, ..., λₖ-1} ⊆ Fin ℓ
- Backward: multiset {a₁, ..., aₖ₋₁} ⊆ Fin ℓ ↦ partition (ℓ, a₁+1, ..., aₖ₋₁+1) sorted

This is well-defined because:
1. Each λᵢ ∈ {1, ..., ℓ}, so λᵢ - 1 ∈ {0, ..., ℓ-1} = Fin ℓ
2. Each aᵢ ∈ Fin ℓ gives aᵢ + 1 ∈ {1, ..., ℓ}
3. The resulting partition has largest part ℓ (which is explicitly the first part)
4. The partition has k parts (one ℓ, plus k-1 from the multiset) 

## PROJECT DEPENDENCY Nat.Partition.partsAndLargestCountTotal (def)
ℕ → ℕ → ℕ

Body:
fun k ℓ => ∑ n ∈ Finset.Icc k (k * ℓ), Nat.Partition.partsAndLargestCount k ℓ n

Docstring: The total count of partitions with exactly k parts and largest part ℓ (summed over all sizes).
The size ranges from k (minimum, when all parts are 1 except the largest) to k*ℓ (maximum,
when all parts equal ℓ). 

## PROJECT DEPENDENCY Nat.Partition.partsAndLargestCount (def)
ℕ → ℕ → ℕ → ℕ

Body:
fun k ℓ n => {p | p.numParts = k ∧ p.largestPart = ℓ}.card

Docstring: The count of partitions with exactly k parts and largest part ℓ, for a specific size n. 

## PROJECT DEPENDENCY Nat.Partition.numParts (def)
{n : ℕ} → n.Partition → ℕ

Body:
fun {n} p => p.parts.card

Docstring: The number of parts of a partition equals the cardinality of its parts multiset. 

## PROJECT DEPENDENCY Nat.Partition.largestPart (def)
{n : ℕ} → n.Partition → ℕ

Body:
fun {n} p => Multiset.fold max 0 p.parts

Docstring: The largest part of a partition (0 for the empty partition).
(Convention \ref{conv.pars.largest-part-0}) 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF GE.ge
{α : Type u} → [LE α] → α → α → Prop

Docstring: `a ≥ b` is an abbreviation for `b ≤ a`. 

Conventions for notations in identifiers:

 * The recommended spelling of `≥` in identifiers is `ge`.

 * The recommended spelling of `>=` in identifiers is `ge` (prefer `≥` over `>=`).

## BASE-LIBRARY REF instLENat
LE ℕ

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

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

## BASE-LIBRARY REF Nat.choose
ℕ → ℕ → ℕ

Docstring: `choose n k` is the number of `k`-element subsets in an `n`-element set. Also known as binomial
coefficients. For the fact that this is the number of `k`-element-subsets of an `n`-element
set, see `Finset.card_powersetCard`. 

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

## BASE-LIBRARY REF Finset.sum
{ι : Type u_1} → {M : Type u_3} → [AddCommMonoid M] → Finset ι → (ι → M) → M

Docstring: `∑ x ∈ s, f x` is the sum of `f x` as `x` ranges over the elements
of the finite set `s`.

When the index type is a `Fintype`, the notation `∑ x, f x`, is a shorthand for
`∑ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF Nat.instAddCommMonoid
AddCommMonoid ℕ

## BASE-LIBRARY REF Finset.Icc
{α : Type u_1} → [inst : Preorder α] → [LocallyFiniteOrder α] → α → α → Finset α

Docstring: The finset $[a, b]$ of elements `x` such that `a ≤ x` and `x ≤ b`. Basically `Set.Icc a b` as a
finset. 

## BASE-LIBRARY REF Nat.instPreorder
Preorder ℕ

## BASE-LIBRARY REF Nat.instLocallyFiniteOrder
LocallyFiniteOrder ℕ

## BASE-LIBRARY REF HMul.hMul
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HMul α β γ] → α → β → γ

Docstring: `a * b` computes the product of `a` and `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `*` in identifiers is `mul`.

## BASE-LIBRARY REF instHMul
{α : Type u_1} → [Mul α] → HMul α α α

## BASE-LIBRARY REF instMulNat
Mul ℕ

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

## BASE-LIBRARY REF And
Prop → Prop → Prop

Docstring: `And a b`, or `a ∧ b`, is the conjunction of propositions. It can be
constructed and destructed like a pair: if `ha : a` and `hb : b` then
`⟨ha, hb⟩ : a ∧ b`, and if `h : a ∧ b` then `h.left : a` and `h.right : b`.


Conventions for notations in identifiers:

 * The recommended spelling of `∧` in identifiers is `and`.

 * The recommended spelling of `/\` in identifiers is `and` (prefer `∧` over `/\`).

## BASE-LIBRARY REF instDecidableAnd
{p q : Prop} → [dp : Decidable p] → [dq : Decidable q] → Decidable (p ∧ q)

## BASE-LIBRARY REF instDecidableEqNat
DecidableEq ℕ

## BASE-LIBRARY REF Finset.univ
{α : Type u_1} → [Fintype α] → Finset α

Docstring: `univ` is the universal finite set of type `Finset α` implied from
the assumption `Fintype α`. 

## BASE-LIBRARY REF Nat.Partition.instFintype
(n : ℕ) → Fintype n.Partition

Docstring: Show there are finitely many partitions by considering the surjection from compositions to
partitions.


## BASE-LIBRARY REF Multiset.card
{α : Type u_1} → Multiset α → ℕ

Docstring: The cardinality of a multiset is the sum of the multiplicities
of all its elements, or simply the length of the underlying list. 

## BASE-LIBRARY REF Nat.Partition.parts
{n : ℕ} → n.Partition → Multiset ℕ

Docstring: positive integers summing to `n` 

## BASE-LIBRARY REF Multiset.fold
{α : Type u_1} → (op : α → α → α) → [hc : Std.Commutative op] → [ha : Std.Associative op] → α → Multiset α → α

Docstring: `fold op b s` folds a commutative associative operation `op` over
the multiset `s`. 

## BASE-LIBRARY REF Max.max
{α : Type u} → [self : Max α] → α → α → α

Docstring: Returns the greater of its two arguments. 

Conventions for notations in identifiers:

 * The recommended spelling of `max` in identifiers is `max`.

 * The recommended spelling of `⊔` in identifiers is `sup` (`⊔` is the preferred notation for `max` when the type is not linearly ordered.).

## BASE-LIBRARY REF Nat.instMax
Max ℕ

## BASE-LIBRARY REF Nat.instCommutativeMax
Std.Commutative max

## BASE-LIBRARY REF Nat.instAssociativeMax
Std.Associative max

## INFORMAL STATEMENT
prop.pars.qbinom.intro-count-binom

For positive integers $k$ and $\ell $, 

\[  Q(k,\ell ) = \binom {k+\ell -2}{k-1}.  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-conv.pars.largest-part-0
conv.pars.largest-part-0

We agree to say that the largest part of the empty partition $\left( {}\right) $ is $0$ (even though this partition has no parts).

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.binom.binom
def.binom.binom

For any numbers $n$ and $k$, we set

\begin{equation}  \binom {n}{k}=\begin{cases}  \frac{n\left( n-1\right) \left( n-2\right) \cdots \left( n-k+1\right) }{k!}, &  \text{if }k\in \mathbb {N};\\ 0, &  \text{else.}\end{cases} \end{equation}

 Note that “numbers” is to be understood fairly liberally here. In particular, $n$ can be any integer, rational, real or complex number (or, more generally, any element in a $\mathbb {Q}$-algebra), whereas $k$ can be anything (although the only nonzero values of $\binom {n}{k}$ will be achieved for $k\in \mathbb {N}$, by the above definition).

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.pars.partsandlargestcount
def.pars.partsAndLargestCount

\leanhelper  Let $k,\ell \in \mathbb {N}$. 

\begin{enumerate} \item $q_{k,\ell }(n) := |\{ p \vdash n : \ell (p) = k,\; \text{largest part of }p = \ell \} |$. 

\item $Q(k,\ell ) := \sum _{n=k}^{k\ell } q_{k,\ell }(n)$, the total number of such partitions over all valid sizes. 

\end{enumerate}

## VERDICT
{
  "verdict": "faithful",
  "justification": "The blueprint quantifies \u201cFor positive integers k and \u2113,\u201d and the elaborated signature has exactly `\u2200 (k \u2113 : \u2115), k \u2265 1 \u2192 \u2113 \u2265 1 \u2192 ...`. Its left-hand side unfolds to `\u2211 n \u2208 Finset.Icc k (k * \u2113), Nat.Partition.partsAndLargestCount k \u2113 n`, matching the informal definition `Q(k,\u2113) := \u2211_{n=k}^{k\u2113} q_{k,\u2113}(n)`. The summand counts partitions satisfying `p.numParts = k \u2227 p.largestPart = \u2113`; `numParts` is the cardinality of the parts multiset, and `largestPart` folds `max` from `0`, matching the partition-length condition and the stated empty-partition convention. The right-hand side `(k + \u2113 - 2).choose (k - 1)` matches `\\binom{k+\u2113-2}{k-1}`. Under `k \u2265 1` and `\u2113 \u2265 1`, natural-number subtraction gives the intended nonnegative integer arguments, and `Nat.choose` has the standard binomial-coefficient meaning. No mathematically contentful extra hypothesis or restricted quantifier is introduced."
}