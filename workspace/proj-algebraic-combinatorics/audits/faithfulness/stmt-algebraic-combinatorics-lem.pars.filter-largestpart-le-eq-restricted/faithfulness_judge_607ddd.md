## TARGET Nat.Partition.filter_largestPart_le_eq_restricted (theorem) — ELABORATED SIGNATURE
∀ (n m : ℕ), {p | p.largestPart ≤ m} = Nat.Partition.restricted n fun x => x ≤ m

Docstring: The set of partitions with largest part ≤ m equals the set of partitions
with all parts ≤ m (i.e., `restricted n (· ≤ m)`).

This is a key equivalence used in the proof of Theorem \ref{thm.pars.main-gf-0n}. 

## PROJECT DEPENDENCY Nat.Partition.largestPart (def)
{n : ℕ} → n.Partition → ℕ

Body:
fun {n} p => Multiset.fold max 0 p.parts

Docstring: The largest part of a partition (0 for the empty partition).
(Convention \ref{conv.pars.largest-part-0}) 

## BASE-LIBRARY REF Finset
Type u_4 → Type u_4

Docstring: `Finset α` is the type of finite sets of elements of `α`. It is implemented
as a multiset (a list up to permutation) which has no duplicate elements. 

## BASE-LIBRARY REF Nat.Partition
ℕ → Type

Docstring: A partition of `n` is a multiset of positive integers summing to `n`. 

## BASE-LIBRARY REF Finset.filter
{α : Type u_1} → (p : α → Prop) → [DecidablePred p] → Finset α → Finset α

Body:
fun {α} p [DecidablePred p] s => { val := Multiset.filter p s.val, nodup := ⋯ }

Docstring: `Finset.filter p s` is the set of elements of `s` that satisfy `p`.

For example, one can use `s.filter (· ∈ t)` to get the intersection of `s` with `t : Set α`
as a `Finset α` (when a `DecidablePred (· ∈ t)` instance is available). 

## BASE-LIBRARY REF Nat.le
ℕ → ℕ → Prop

Docstring: Non-strict, or weak, inequality of natural numbers, usually accessed via the `≤` operator.


## BASE-LIBRARY REF Nat.decLe
(n m : ℕ) → Decidable (n ≤ m)

Body:
fun n m => if h : n.ble m = true then isTrue ⋯ else isFalse ⋯

Docstring: A decision procedure for non-strict inequality of natural numbers, usually accessed via the
`DecidableLE Nat` instance.

Examples:
 * `(if 3 ≤ 4 then "yes" else "no") = "yes"`
 * `(if 6 ≤ 4 then "yes" else "no") = "no"`
 * `show 12 ≤ 12 by decide`
 * `show 5 ≤ 12 by decide`


## BASE-LIBRARY REF Finset.univ
{α : Type u_1} → [Fintype α] → Finset α

Body:
fun {α} [Fintype α] => Fintype.elems

Docstring: `univ` is the universal finite set of type `Finset α` implied from
the assumption `Fintype α`. 

## BASE-LIBRARY REF Nat.Partition.instFintype
(n : ℕ) → Fintype n.Partition

Body:
fun n => Fintype.ofSurjective (Nat.Partition.ofComposition n) ⋯

Docstring: Show there are finitely many partitions by considering the surjection from compositions to
partitions.


## BASE-LIBRARY REF Nat.Partition.restricted
(n : ℕ) → (p : ℕ → Prop) → [DecidablePred p] → Finset n.Partition

Body:
fun n p [DecidablePred p] => {x | ∀ i ∈ x.parts, p i}

Docstring: The finset of those partitions in which every part satisfies a certain condition. 

## BASE-LIBRARY REF Multiset.fold
{α : Type u_1} → (op : α → α → α) → [hc : Std.Commutative op] → [ha : Std.Associative op] → α → Multiset α → α

Body:
fun {α} op [Std.Commutative op] [Std.Associative op] => Multiset.foldr op

Docstring: `fold op b s` folds a commutative associative operation `op` over
the multiset `s`. 

## BASE-LIBRARY REF Max.max
{α : Type u} → [self : Max α] → α → α → α

Body:
fun α [self : Max α] => self.1

Docstring: Returns the greater of its two arguments. 

Conventions for notations in identifiers:

 * The recommended spelling of `max` in identifiers is `max`.

 * The recommended spelling of `⊔` in identifiers is `sup` (`⊔` is the preferred notation for `max` when the type is not linearly ordered.).

## BASE-LIBRARY REF Nat.instMax
Max ℕ

Body:
maxOfLe

## BASE-LIBRARY REF maxOfLe
{α : Type u_1} → [inst : LE α] → [DecidableRel LE.le] → Max α

Body:
fun {α} [LE α] [DecidableRel LE.le] => { max := fun x y => if x ≤ y then y else x }

Docstring: Constructs a `Max` instance from a decidable `≤` operation.


## BASE-LIBRARY REF Nat.instCommutativeMax
Std.Commutative max

## BASE-LIBRARY REF Nat.instAssociativeMax
Std.Associative max

## BASE-LIBRARY REF Nat.Partition.parts
{n : ℕ} → n.Partition → Multiset ℕ

Body:
fun n self => self.1

Docstring: positive integers summing to `n` 

## INFORMAL STATEMENT
lem.pars.filter-largestPart-le-eq-restricted

\leanhelper  The set of partitions of $n$ whose largest part is $\le m$ equals the set of partitions of $n$ with all parts $\le m$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-conv.pars.largest-part-0
conv.pars.largest-part-0

We agree to say that the largest part of the empty partition $\left( {}\right) $ is $0$ (even though this partition has no parts).

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
  "discrepancies": [],
  "justification": "The formal theorem quantifies over `\u2200 (n m : \u2115)` and equates `{p | p.largestPart \u2264 m}` with `Nat.Partition.restricted n fun x => x \u2264 m`. Unfolding `restricted` gives exactly the partitions `x : Nat.Partition n` satisfying `\u2200 i \u2208 x.parts, i \u2264 m`. Unfolding `largestPart` gives `Multiset.fold max 0 p.parts`, the maximum of the parts with value `0` for the empty partition, matching the blueprint convention. Thus the two sides are precisely \u201cpartitions of n whose largest part is \u2264 m\u201d and \u201cpartitions of n with all parts \u2264 m,\u201d as claimed."
}