## TARGET Nat.Partition.oddPartsCount_eq_distinctPartsCount (theorem) — ELABORATED SIGNATURE
∀ (n : ℕ), Nat.Partition.oddPartsCount n = Nat.Partition.distinctPartsCount n

Docstring: Euler's odd-distinct identity in terms of counting functions. 

## TARGET Nat.Partition.odd_eq_distinct (theorem) — ELABORATED SIGNATURE
∀ (n : ℕ), (Nat.Partition.odds n).card = (Nat.Partition.distincts n).card

Docstring: Euler's odd-distinct identity: the number of partitions of n into odd parts
equals the number of partitions of n into distinct parts.
(Theorem \ref{thm.pars.odd-dist-equal})

This is Theorem 45 from Freek Wiedijk's list of 100 theorems.

The proof in Mathlib uses Glaisher's theorem, which generalizes this result:
for any positive integer d, the number of partitions with parts not divisible by d
equals the number of partitions where no part is repeated d or more times.
Euler's identity is the special case d = 2.

The bijective proof (sketched in the module docstring) works by:
- Merging pairs of equal parts (odd → distinct)
- Splitting even parts into halves (distinct → odd) 

## PROJECT DEPENDENCY Nat.Partition.oddPartsCount (def)
ℕ → ℕ

Body:
fun n => (Nat.Partition.odds n).card

Docstring: The number of partitions of n into odd parts: `p_odd(n)`.
(Definition \ref{def.pars.odd-dist-parts} (c))

This counts the partitions of n where every part is an odd number.
Uses Mathlib's `Nat.Partition.odds` which filters partitions by the
predicate `¬Even` (equivalent to `Odd` for positive integers). 

## PROJECT DEPENDENCY Nat.Partition.distinctPartsCount (def)
ℕ → ℕ

Body:
fun n => (Nat.Partition.distincts n).card

Docstring: The number of partitions of n into distinct parts: `p_dist(n)`.
(Definition \ref{def.pars.odd-dist-parts} (c))

This counts the partitions of n where all parts are different (no repeats).
Uses Mathlib's `Nat.Partition.distincts` which filters partitions by
the `Nodup` predicate on the parts multiset. 

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

## BASE-LIBRARY REF Finset.card
{α : Type u_1} → Finset α → ℕ

Docstring: `s.card` is the number of elements of `s`, aka its cardinality.

The notation `#s` can be accessed in the `Finset` locale. 

## BASE-LIBRARY REF Nat.Partition
ℕ → Type

Docstring: A partition of `n` is a multiset of positive integers summing to `n`. 

## BASE-LIBRARY REF Nat.Partition.odds
(n : ℕ) → Finset n.Partition

Docstring: The finset of those partitions in which every part is odd. 

## BASE-LIBRARY REF Nat.Partition.distincts
(n : ℕ) → Finset n.Partition

Docstring: The finset of those partitions in which each part is used at most once. 

## INFORMAL STATEMENT
Euler’s odd-distinct identity

We have $p_{\operatorname {odd}}\left( n\right) =p_{\operatorname {dist}}\left( n\right) $ for each $n\in \mathbb {N}$.

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
  "justification": "The target `oddPartsCount_eq_distinctPartsCount` states `\u2200 (n : \u2115), Nat.Partition.oddPartsCount n = Nat.Partition.distinctPartsCount n`, exactly matching \u201cfor each `n \u2208 \u2115`, `p_odd(n) = p_dist(n)`.\u201d Its dependencies unfold to `(Nat.Partition.odds n).card` and `(Nat.Partition.distincts n).card`; the supplied library definitions identify these as the finite sets of partitions whose parts are respectively all odd and each used at most once, matching the informal definitions of odd and distinct parts. Equivalently, the second target states this unfolded equality directly: `\u2200 (n : \u2115), (Nat.Partition.odds n).card = (Nat.Partition.distincts n).card`. There are no added hypotheses or restricted quantifiers."
}