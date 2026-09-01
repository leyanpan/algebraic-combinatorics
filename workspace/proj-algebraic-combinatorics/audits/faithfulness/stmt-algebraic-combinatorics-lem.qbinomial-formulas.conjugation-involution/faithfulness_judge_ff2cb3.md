## TARGET AlgebraicCombinatorics.QBinomialRec.conjugatePartition_involution' (theorem) — ELABORATED SIGNATURE
∀ (m : ℕ) (p : m.Partition),
  AlgebraicCombinatorics.QBinomialRec.conjugatePartition'✝ m
      (AlgebraicCombinatorics.QBinomialRec.conjugatePartition'✝¹ m p) =
    p

## PROJECT DEPENDENCY _private.AlgebraicCombinatorics.Partitions.QBinomialFormulas.0.AlgebraicCombinatorics.QBinomialRec.conjugatePartition' (def)
(m : ℕ) → m.Partition → m.Partition

Body:
fun m p =>
  let μ := AlgebraicCombinatorics.QBinomialRec.partitionToYoungDiagram'✝ m p;
  have hcard := ⋯;
  have hsum := ⋯;
  { parts := ↑μ.transpose.rowLens, parts_pos := ⋯, parts_sum := ⋯ }

## PROJECT DEPENDENCY _private.AlgebraicCombinatorics.Partitions.QBinomialFormulas.0.AlgebraicCombinatorics.QBinomialRec.partitionToYoungDiagram' (def)
(m : ℕ) → m.Partition → YoungDiagram

Body:
fun m p => YoungDiagram.ofRowLens (p.parts.sort fun x1 x2 => x1 ≥ x2) ⋯

## PROJECT DEPENDENCY _private.AlgebraicCombinatorics.Partitions.QBinomialFormulas.0.AlgebraicCombinatorics.QBinomialRec.parts_sort_sorted' (theorem)
∀ (m : ℕ) (p : m.Partition), (p.parts.sort fun x1 x2 => x1 ≥ x2).SortedGE

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF Nat.Partition
ℕ → Type

Docstring: A partition of `n` is a multiset of positive integers summing to `n`. 

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

## BASE-LIBRARY REF YoungDiagram
Type

Docstring: A Young diagram is a finite collection of cells on the `ℕ × ℕ` grid such that whenever
a cell is present, so are all the ones above and to the left of it. Like matrices, an `(i, j)` cell
is a cell in row `i` and column `j`, where rows are enumerated downward and columns rightward.

Young diagrams are modeled as finite sets in `ℕ × ℕ` that are lower sets with respect to the
standard order on products. 

## BASE-LIBRARY REF YoungDiagram.card
YoungDiagram → ℕ

Docstring: Cardinality of a Young diagram 

## BASE-LIBRARY REF YoungDiagram.transpose
YoungDiagram → YoungDiagram

Docstring: The `transpose` of a Young diagram is obtained by swapping i's with j's. 

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

## BASE-LIBRARY REF YoungDiagram.rowLens
YoungDiagram → List ℕ

Docstring: List of row lengths of a Young diagram 

## BASE-LIBRARY REF Nat.Partition.mk
{n : ℕ} → (parts : Multiset ℕ) → (∀ {i : ℕ}, i ∈ parts → 0 < i) → parts.sum = n → n.Partition

## BASE-LIBRARY REF Multiset.ofList
{α : Type u_1} → List α → Multiset α

Docstring: The quotient map from `List α` to `Multiset α`. 

## BASE-LIBRARY REF YoungDiagram.ofRowLens
(w : List ℕ) → w.SortedGE → YoungDiagram

Docstring: Young diagram from a sorted list 

## BASE-LIBRARY REF Multiset.sort
{α : Type u_1} →
  Multiset α →
    (r : autoParam (α → α → Prop) Multiset.sort._auto_1) →
      [DecidableRel r] → [IsTrans α r] → [Std.Antisymm r] → [Std.Total r] → List α

Docstring: `sort s` constructs a sorted list from the multiset `s`.
(Uses merge sort algorithm.) 

## BASE-LIBRARY REF Nat.Partition.parts
{n : ℕ} → n.Partition → Multiset ℕ

Docstring: positive integers summing to `n` 

## BASE-LIBRARY REF GE.ge
{α : Type u} → [LE α] → α → α → Prop

Docstring: `a ≥ b` is an abbreviation for `b ≤ a`. 

Conventions for notations in identifiers:

 * The recommended spelling of `≥` in identifiers is `ge`.

 * The recommended spelling of `>=` in identifiers is `ge` (prefer `≥` over `>=`).

## BASE-LIBRARY REF instLENat
LE ℕ

## BASE-LIBRARY REF Nat.decLe
(n m : ℕ) → Decidable (n ≤ m)

Docstring: A decision procedure for non-strict inequality of natural numbers, usually accessed via the
`DecidableLE Nat` instance.

Examples:
 * `(if 3 ≤ 4 then "yes" else "no") = "yes"`
 * `(if 6 ≤ 4 then "yes" else "no") = "no"`
 * `show 12 ≤ 12 by decide`
 * `show 5 ≤ 12 by decide`


## BASE-LIBRARY REF instIsTransGe
∀ {α : Type u} [inst : Preorder α], IsTrans α fun x1 x2 => x2 ≤ x1

## BASE-LIBRARY REF Nat.instPreorder
Preorder ℕ

## BASE-LIBRARY REF instAntisymmGe
∀ {α : Type u} [inst : PartialOrder α], Std.Antisymm fun x1 x2 => x2 ≤ x1

## BASE-LIBRARY REF Nat.instPartialOrder
PartialOrder ℕ

## BASE-LIBRARY REF LE.total'
∀ {α : Type u} [inst : LinearOrder α], Std.Total fun x1 x2 => x2 ≤ x1

## BASE-LIBRARY REF Nat.instLinearOrder
LinearOrder ℕ

## BASE-LIBRARY REF List.SortedGE
{α : Type u_1} → [Preorder α] → List α → Prop

Docstring: `l.SortedGE` means that the list is antitonic. 

## INFORMAL STATEMENT
lem.qbinomial-formulas.conjugation-involution

\leanhelper  Young diagram conjugation (transposition) is an involution on partitions of $n$ that interchanges “all parts $\le k$” with “at most $k$ parts”. Specifically, if $p$ is a partition of $n$ with all parts $\le k$, then its conjugate has at most $k$ parts, and vice versa. Moreover, conjugating twice recovers the original partition.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-conv-2eb59533
conv-2eb59533

In the Lean formalization, we use $\operatorname {Fin} n = \{ 0, 1, \ldots , n-1\} $ instead of the textbook’s $[n] = \{ 1, 2, \ldots , n\} $. Both are $n$-element sets, so their symmetric groups are isomorphic. Permutations are represented by the type of bijections $X \to X$ (denoted $\operatorname {Equiv.Perm}\,  X$ in Lean), which is a group under composition. Composition $\alpha \beta $ is the group multiplication $\alpha * \beta $, sending $x$ to $\alpha (\beta (x))$.

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.perm
def.perm.perm

Let $X$ be a set. 

\textbf{(a)} A \emph{permutation} of $X$ means a bijection from $X$ to $X$. 

\textbf{(b)} It is known that the set of all permutations of $X$ is a group under composition. This group is called the \emph{symmetric group} of $X$, and is denoted by $S_X$. Its neutral element is the identity map $\operatorname {id}_X : X \to X$. Its size is $|X|!$ when $X$ is finite. 

\textbf{(c)} As usual in group theory, we will write $\alpha \beta $ for the composition $\alpha \circ \beta $ when $\alpha , \beta \in S_X$. This is the map that sends each $x \in X$ to $\alpha (\beta (x))$. 

\textbf{(d)} If $\alpha \in S_X$ and $i \in \mathbb {Z}$, then $\alpha ^i$ shall denote the $i$-th power of $\alpha $ in the group $S_X$. Note that $\alpha ^i = \underbrace{\alpha \circ \alpha \circ \cdots \circ \alpha }_{i\text{ times}}$ if $i \ge 0$. Also, $\alpha ^0 = \operatorname {id}_X$. Also, $\alpha ^{-1}$ is the inverse of $\alpha $ in the group $S_X$, that is, the inverse of the map $\alpha $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.is-transpose
def.sf.is-transpose

\leanhelper  Two functions $\lambda : \mathrm{Fin}\, N \to \mathbb {N}$ and $\lambda ^t : \mathrm{Fin}\, M \to \mathbb {N}$ are \emph{transposes} of each other if for all $i < N$ and $j < M$: 

\[  \lambda _i > j \iff \lambda ^t_j > i.  \]

 This is the symmetric characterization of the transpose relation between Young diagrams.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.npar
def.sf.Npar

An $N$\emph{-partition} will mean a weakly decreasing $N$-tuple of nonnegative integers. In other words, an $N$-partition means an $N$-tuple $\left( \lambda _{1},\lambda _{2},\ldots ,\lambda _{N}\right) \in \mathbb {N}^{N}$ with $\lambda _{1}\geq \lambda _{2}\geq \cdots \geq \lambda _{N}$. 

The \emph{size} (or weight) of an $N$-partition $\lambda = (\lambda _1, \lambda _2, \ldots , \lambda _N)$ is defined to be $|\lambda | := \lambda _1 + \lambda _2 + \cdots + \lambda _N$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.npartition-transpose
def.sf.npartition-transpose

\leanhelper  The \emph{transpose} (or \emph{conjugate}) of an $N$-partition $\lambda $ is the partition $\lambda ^t$ whose $i$-th part equals $|\{ j : j < N,\;  \lambda _j > i\} |$, i.e., the number of parts of $\lambda $ that exceed $i$. Requires $N > 0$; the result is a partition of length $\lambda _1$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.npartitionsofsize
def.sf.NPartitionsOfSize

\leanhelper  The finite set of $N$-partitions of size $n$.

## VERDICT
{
  "verdict": "drift",
  "justification": "The target formalizes only the final clause: `\u2200 (m : \u2115) (p : m.Partition), conjugatePartition' m (conjugatePartition' m p) = p`, matching \u201cMoreover, conjugating twice recovers the original partition.\u201d It does not formalize the preceding claim: \u201cif `p` is a partition of `n` with all parts `\u2264 k`, then its conjugate has at most `k` parts, and vice versa.\u201d In particular, the elaborated signature has no binder `(k : \u2115)` and no conclusion relating a bound on `p.parts` to the number of parts of its conjugate. The supplied definition of `conjugatePartition'` does construct the partition from the transposed Young diagram, so the discrepancy enters in the TARGET theorem\u2019s binders and conclusion, not in that definition. To be faithful to the full blueprint statement, the target must additionally quantify over `k` and assert the two directions (or an equivalence) between \u201call parts of `p` are at most `k`\u201d and \u201cthe conjugate has at most `k` parts,\u201d alongside the involution equality."
}