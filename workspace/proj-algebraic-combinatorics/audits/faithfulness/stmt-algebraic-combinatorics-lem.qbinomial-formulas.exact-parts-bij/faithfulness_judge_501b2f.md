## TARGET AlgebraicCombinatorics.QBinomialRec.partitionsInBoxExact_card_eq (theorem) — ELABORATED SIGNATURE
∀ (s k m : ℕ),
  m ≥ 1 →
    s ≥ k + 1 →
      (AlgebraicCombinatorics.QBinomialRec.partitionsInBoxExact s (k + 1) m).card =
        AlgebraicCombinatorics.QBinomialRec.countPartitionsInBox (s - (k + 1)) (k + 1) (m - 1)

Docstring: Key cardinality equality: partitions with exactly k+1 parts in (k+1) × m box biject with
partitions with at most k+1 parts in (k+1) × (m-1) box, via the "subtract 1 from each part"
bijection. This is the combinatorial heart of the q-Pascal identity.

The bijection:
- Forward: subtract 1 from each part, filter zeros (using `ofSums`)
- Inverse: add 1 to each part, pad with 1s to get exactly k+1 parts 

## PROJECT DEPENDENCY AlgebraicCombinatorics.QBinomialRec.partitionsInBoxExact (def)
(size : ℕ) → ℕ → ℕ → Finset size.Partition

Body:
fun size k m => {p | p.parts.card = k ∧ AlgebraicCombinatorics.QBinomialRec.partitionLargestPartLeq p m}

Docstring: Partitions with exactly k parts (not just at most k parts), fitting in a box with largest part ≤ m.
Used in the q-Pascal identity proof to split partitions by exact number of parts. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.QBinomialRec.countPartitionsInBox (def)
ℕ → ℕ → ℕ → ℕ

Body:
fun size k m => (AlgebraicCombinatorics.QBinomialRec.partitionsInBox size k m).card

Docstring: The count of partitions of a given size that fit in a k × m box. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.QBinomialRec.partitionLargestPartLeq (def)
{n : ℕ} → n.Partition → ℕ → Prop

Body:
fun {n} p m => ∀ i ∈ p.parts, i ≤ m

Docstring: A partition has largest part ≤ m if all parts are ≤ m.
This is used in the combinatorial definition of q-binomial coefficients. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.QBinomialRec.instDecidablePartitionLargestPartLeq (def)
{n m : ℕ} → (p : n.Partition) → Decidable (AlgebraicCombinatorics.QBinomialRec.partitionLargestPartLeq p m)

Body:
fun {n m} p => inferInstanceAs (Decidable (∀ i ∈ p.parts, i ≤ m))

## PROJECT DEPENDENCY AlgebraicCombinatorics.QBinomialRec.partitionsInBox (def)
(size : ℕ) → ℕ → ℕ → Finset size.Partition

Body:
fun size k m =>
  {p |
    AlgebraicCombinatorics.QBinomialRec.partitionLengthLeq p k ∧
      AlgebraicCombinatorics.QBinomialRec.partitionLargestPartLeq p m}

Docstring: The set of partitions of a given size that fit in a k × m box
(i.e., have length ≤ k and largest part ≤ m).

For the q-binomial `[n choose k]_q`, we use m = n - k.

**Argument order:** `(size k m : ℕ)` where:
- `size` is the partition size
- `k` is the maximum number of parts (length ≤ k)
- `m` is the maximum part size (largest part ≤ m)

This matches the convention in `AlgebraicCombinatorics.partitionsInBox` from `QBinomialBasic.lean`. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.QBinomialRec.partitionLengthLeq (def)
{n : ℕ} → n.Partition → ℕ → Prop

Body:
fun {n} p k => p.parts.card ≤ k

Docstring: A partition has length ≤ k if it has at most k parts.
This is used in the combinatorial definition of q-binomial coefficients. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.QBinomialRec.instDecidablePartitionLengthLeq (def)
{n k : ℕ} → (p : n.Partition) → Decidable (AlgebraicCombinatorics.QBinomialRec.partitionLengthLeq p k)

Body:
fun {n k} p => inferInstanceAs (Decidable (p.parts.card ≤ k))

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

## BASE-LIBRARY REF Finset
Type u_4 → Type u_4

Docstring: `Finset α` is the type of finite sets of elements of `α`. It is implemented
as a multiset (a list up to permutation) which has no duplicate elements. 

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

## BASE-LIBRARY REF Multiset.card
{α : Type u_1} → Multiset α → ℕ

Docstring: The cardinality of a multiset is the sum of the multiplicities
of all its elements, or simply the length of the underlying list. 

## BASE-LIBRARY REF Nat.Partition.parts
{n : ℕ} → n.Partition → Multiset ℕ

Docstring: positive integers summing to `n` 

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

## BASE-LIBRARY REF LE.le
{α : Type u} → [self : LE α] → α → α → Prop

Docstring: The less-equal relation: `x ≤ y` 

Conventions for notations in identifiers:

 * The recommended spelling of `≤` in identifiers is `le`.

 * The recommended spelling of `<=` in identifiers is `le` (prefer `≤` over `<=`).

## BASE-LIBRARY REF Decidable
Prop → Type

Docstring: Either a proof that `p` is true or a proof that `p` is false. This is equivalent to a `Bool` paired
with a proof that the `Bool` is `true` if and only if `p` is true.

`Decidable` instances are primarily used via `if`-expressions and the tactic `decide`. In
conditional expressions, the `Decidable` instance for the proposition is used to select a branch. At
run time, this case distinction code is identical to that which would be generated for a
`Bool`-based conditional. In proofs, the tactic `decide` synthesizes an instance of `Decidable p`,
attempts to reduce it to `isTrue h`, and then succeeds with the proof `h` if it can.

Because `Decidable` carries data, when writing `@[simp]` lemmas which include a `Decidable` instance
on the LHS, it is best to use `{_ : Decidable p}` rather than `[Decidable p]` so that non-canonical
instances can be found via unification rather than instance synthesis.


## BASE-LIBRARY REF inferInstanceAs
(α : Sort u) → [i : α] → α

Docstring: `inferInstanceAs α` synthesizes a value of any target type by typeclass
inference. This is just like `inferInstance` except that `α` is given
explicitly instead of being inferred from the target type. It is especially
useful when the target type is some `α'` which is definitionally equal to `α`,
but the instance we are looking for is only registered for `α` (because
typeclass search does not unfold most definitions, but definitional equality
does.) Example:
```
#check inferInstanceAs (Inhabited Nat) -- Inhabited Nat
```


## BASE-LIBRARY REF Multiset.decidableDforallMultiset
{α : Type u_1} →
  {m : Multiset α} →
    {p : (a : α) → a ∈ m → Prop} →
      [_hp : (a : α) → (h : a ∈ m) → Decidable (p a h)] → Decidable (∀ (a : α) (h : a ∈ m), p a h)

## BASE-LIBRARY REF Nat.decLe
(n m : ℕ) → Decidable (n ≤ m)

Docstring: A decision procedure for non-strict inequality of natural numbers, usually accessed via the
`DecidableLE Nat` instance.

Examples:
 * `(if 3 ≤ 4 then "yes" else "no") = "yes"`
 * `(if 6 ≤ 4 then "yes" else "no") = "no"`
 * `show 12 ≤ 12 by decide`
 * `show 5 ≤ 12 by decide`


## INFORMAL STATEMENT
lem.qbinomial-formulas.exact-parts-bij

\leanhelper  For $m \ge 1$ and $s \ge k+1$, the number of partitions of $s$ with exactly $k+1$ parts, each $\le m$, equals the number of partitions of $s - (k+1)$ fitting in a $(k+1) \times (m-1)$ box: 

\[  |\mathrm{partitionsInBoxExact}(s, k{+}1, m)| = c(s{-}(k{+}1), k{+}1, m{-}1).  \]

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.pars.partsandlargestcount
def.pars.partsAndLargestCount

\leanhelper  Let $k,\ell \in \mathbb {N}$. 

\begin{enumerate} \item $q_{k,\ell }(n) := |\{ p \vdash n : \ell (p) = k,\; \text{largest part of }p = \ell \} |$. 

\item $Q(k,\ell ) := \sum _{n=k}^{k\ell } q_{k,\ell }(n)$, the total number of such partitions over all valid sizes. 

\end{enumerate}

## VERDICT
{
  "verdict": "faithful",
  "justification": "The formal binders `\u2200 (s k m : \u2115), m \u2265 1 \u2192 s \u2265 k + 1 \u2192` exactly match the blueprint\u2019s conditions \u201cFor $m \\ge 1$ and $s \\ge k+1$.\u201d By definition, `partitionsInBoxExact s (k + 1) m` consists of partitions of size `s` satisfying `p.parts.card = k + 1` and `\u2200 i \u2208 p.parts, i \u2264 m`, matching \u201cpartitions of $s$ with exactly $k+1$ parts, each $\\le m$.\u201d The right side unfolds as the cardinality of partitions of size `s - (k + 1)` with length at most `k + 1` and every part at most `m - 1`, exactly the stated `(k+1) \u00d7 (m-1)` box count. Thus the displayed formal equality and the blueprint equality coincide."
}