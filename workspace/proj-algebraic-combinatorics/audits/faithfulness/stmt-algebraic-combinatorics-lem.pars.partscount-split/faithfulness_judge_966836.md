## TARGET Nat.Partition.partsCount_split (theorem) — ELABORATED SIGNATURE
∀ {k n : ℕ},
  Nat.Partition.partsCount k n = (Nat.Partition.partsWithOne k n).card + (Nat.Partition.partsWithoutOne k n).card

## PROJECT DEPENDENCY Nat.Partition.partsCount (def)
ℕ → ℕ → ℕ

Body:
fun k n => {p | p.parts.card = k}.card

Docstring: The function `p_k(n)`: the number of partitions of `n` into exactly `k` parts.
(Definition \ref{def.pars.pn-pkn} (a)) 

## PROJECT DEPENDENCY Nat.Partition.partsWithOne (def)
ℕ → (n : ℕ) → Finset n.Partition

Body:
fun k n => {p | p.parts.card = k ∧ p.containsOne}

Docstring: Partitions of n into k parts that contain 1. 

## PROJECT DEPENDENCY Nat.Partition.partsWithoutOne (def)
ℕ → (n : ℕ) → Finset n.Partition

Body:
fun k n => {p | p.parts.card = k ∧ ¬p.containsOne}

Docstring: Partitions of n into k parts that don't contain 1. 

## PROJECT DEPENDENCY Nat.Partition.containsOne (def)
{n : ℕ} → n.Partition → Prop

Body:
fun {n} p => 1 ∈ p.parts

Docstring: A partition containing 1 as a part. 

## PROJECT DEPENDENCY Nat.Partition.instDecidablePredContainsOne (def)
{n : ℕ} → DecidablePred Nat.Partition.containsOne

Body:
fun {n} p => Multiset.decidableMem 1 p.parts

## BASE-LIBRARY REF Add
Type u → Type u

Docstring: The homogeneous version of `HAdd`: `a + b : α` where `a b : α`. 

## BASE-LIBRARY REF Add.add
{α : Type u} → [self : Add α] → α → α → α

Body:
fun α [self : Add α] => self.1

Docstring: `a + b` computes the sum of `a` and `b`. See `HAdd`. 

## BASE-LIBRARY REF Nat.add
ℕ → ℕ → ℕ

Body:
fun x x_1 =>
  Nat.brecOn (motive := fun x => ℕ → ℕ) x_1
    (fun x f x_2 =>
      (match (motive := ℕ → (x : ℕ) → Nat.below (motive := fun x => ℕ → ℕ) x → ℕ) x_2, x with
        | a, Nat.zero => fun x => a
        | a, b.succ => fun x => (x.1 a).succ)
        f)
    x

Docstring: Addition of natural numbers, typically used via the `+` operator.

This function is overridden in both the kernel and the compiler to efficiently evaluate using the
arbitrary-precision arithmetic library. The definition provided here is the logical model.


## BASE-LIBRARY REF Finset.card
{α : Type u_1} → Finset α → ℕ

Body:
fun {α} s => s.val.card

Docstring: `s.card` is the number of elements of `s`, aka its cardinality.

The notation `#s` can be accessed in the `Finset` locale. 

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

## BASE-LIBRARY REF Multiset.card
{α : Type u_1} → Multiset α → ℕ

Body:
fun {α} => Quot.lift List.length ⋯

Docstring: The cardinality of a multiset is the sum of the multiplicities
of all its elements, or simply the length of the underlying list. 

## BASE-LIBRARY REF Nat.Partition.parts
{n : ℕ} → n.Partition → Multiset ℕ

Body:
fun n self => self.1

Docstring: positive integers summing to `n` 

## BASE-LIBRARY REF Nat.decEq
(n m : ℕ) → Decidable (n = m)

Body:
fun n m =>
  match h : n.beq m with
  | true => isTrue ⋯
  | false => isFalse ⋯

Docstring: A decision procedure for equality of natural numbers, usually accessed via the `DecidableEq Nat`
instance.

This function is overridden in both the kernel and the compiler to efficiently evaluate using the
arbitrary-precision arithmetic library. The definition provided here is the logical model.

Examples:
 * `Nat.decEq 5 5 = isTrue rfl`
 * `(if 3 = 4 then "yes" else "no") = "no"`
 * `show 12 = 12 by decide`


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


## BASE-LIBRARY REF Finset
Type u_4 → Type u_4

Docstring: `Finset α` is the type of finite sets of elements of `α`. It is implemented
as a multiset (a list up to permutation) which has no duplicate elements. 

## BASE-LIBRARY REF instDecidableAnd.match_1
{q : Prop} →
  (motive : Decidable q → Sort u_1) →
    (dq : Decidable q) → ((hq : q) → motive (isTrue hq)) → ((hq : ¬q) → motive (isFalse hq)) → motive dq

Body:
fun {q} motive dq h_1 h_2 => Decidable.casesOn dq (fun h => h_2 h) fun h => h_1 h

## BASE-LIBRARY REF Decidable.isTrue
{p : Prop} → p → Decidable p

Docstring: Proves that `p` is decidable by supplying a proof of `p` 

## BASE-LIBRARY REF And.intro
∀ {a b : Prop}, a → b → a ∧ b

Docstring: `And.intro : a → b → a ∧ b` is the constructor for the And operation. 

## BASE-LIBRARY REF Decidable.isFalse
{p : Prop} → ¬p → Decidable p

Docstring: Proves that `p` is decidable by supplying a proof of `¬p` 

## BASE-LIBRARY REF instDecidableAnd._proof_1
∀ {p q : Prop}, ¬q → p ∧ q → False

## BASE-LIBRARY REF instDecidableAnd._proof_2
∀ {p q : Prop}, ¬p → p ∧ q → False

## BASE-LIBRARY REF absurd
{a : Prop} → {b : Sort v} → a → ¬a → b

Body:
fun {a} {b} h₁ h₂ => False.rec (fun x => b) ⋯

Docstring: Anything follows from two contradictory hypotheses. Example:
```
example (hp : p) (hnp : ¬p) : q := absurd hp hnp
```
For more information: [Propositional Logic](https://lean-lang.org/theorem_proving_in_lean4/propositions_and_proofs.html#propositional-logic)


## BASE-LIBRARY REF Multiset
Type u → Type u

Body:
fun α => Quotient (List.isSetoid α)

Docstring: `Multiset α` is the quotient of `List α` by list permutation. The result
is a type of finite sets with duplicates allowed. 

## BASE-LIBRARY REF Multiset.Mem
{α : Type u_1} → Multiset α → α → Prop

Body:
fun {α} s a => Quot.liftOn s (fun l => a ∈ l) ⋯

Docstring: `a ∈ s` means that `a` has nonzero multiplicity in `s`. 

## BASE-LIBRARY REF Multiset.decidableMem
{α : Type u_1} → [DecidableEq α] → (a : α) → (s : Multiset α) → Decidable (a ∈ s)

Body:
fun {α} [DecidableEq α] a s => Quot.recOnSubsingleton s fun l => inferInstanceAs (Decidable (a ∈ l))

## BASE-LIBRARY REF Quot.recOnSubsingleton
{α : Sort u} →
  {r : α → α → Prop} →
    {motive : Quot r → Sort v} →
      [h : ∀ (a : α), Subsingleton (motive (Quot.mk r a))] → (q : Quot r) → ((a : α) → motive (Quot.mk r a)) → motive q

Body:
fun {α} {r} {motive} [∀ (a : α), Subsingleton (motive (Quot.mk r a))] q f => Quot.rec (fun a => f a) ⋯ q

Docstring: An alternative induction principle for quotients that can be used when the target type is a
subsingleton, in which all elements are equal.

In these cases, the proof that the function respects the quotient's relation is trivial, so any
function can be lifted.

`Quot.rec` does not assume that the type is a subsingleton.


## BASE-LIBRARY REF List
Type u → Type u

Docstring: Linked lists: ordered lists, in which each element has a reference to the next element.

Most operations on linked lists take time proportional to the length of the list, because each
element must be traversed to find the next element.

`List α` is isomorphic to `Array α`, but they are useful for different things:
* `List α` is easier for reasoning, and `Array α` is modeled as a wrapper around `List α`.
* `List α` works well as a persistent data structure, when many copies of the tail are shared. When
  the value is not shared, `Array α` will have better performance because it can do destructive
  updates.


## BASE-LIBRARY REF Setoid.r
{α : Sort u} → [self : Setoid α] → α → α → Prop

Body:
fun α [self : Setoid α] => self.1

Docstring: `x ≈ y` is the distinguished equivalence relation of a setoid. 

## BASE-LIBRARY REF List.isSetoid
(α : Type u_1) → Setoid (List α)

Body:
fun α => { r := List.Perm, iseqv := ⋯ }

## BASE-LIBRARY REF Multiset.decidableMem._proof_1
∀ {α : Type u_1} (a : α) (a_1 : List α), Subsingleton (Decidable (a ∈ Quot.mk (⇑(List.isSetoid α)) a_1))

## BASE-LIBRARY REF inferInstanceAs
(α : Sort u) → [i : α] → α

Body:
fun α [i : α] => i

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


## BASE-LIBRARY REF List.instDecidableMemOfLawfulBEq
{α : Type u} → [inst : BEq α] → [LawfulBEq α] → (a : α) → (as : List α) → Decidable (a ∈ as)

Body:
fun {α} [BEq α] [LawfulBEq α] a as => decidable_of_decidable_of_iff ⋯

## INFORMAL STATEMENT
lem.pars.partsCount-split

\leanhelper  The set of partitions of $n$ into $k$ parts splits into those containing~ $1$ and those not containing~ $1$: 

\[  p_k(n) = |\{ \text{partitions with 1}\} | + |\{ \text{partitions without 1}\} |.  \]

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
  "verdict": "minor_discrepancy",
  "discrepancies": [
    {
      "root": "\u2200 {k n : \u2115}",
      "severity": "minor",
      "bridge": "The blueprint defines and states p_k(n) for n \u2208 \u2124, whereas the theorem only quantifies over natural n. For n \u2265 0, identify the integer n with its corresponding natural number and apply the formal theorem. For n < 0, no finite tuple of positive integers can have size n, so there are no partitions of n; consequently p_k(n), the count containing 1, and the count not containing 1 are all zero, and the claimed equality is immediate."
    }
  ],
  "justification": "The elaborated signature restricts the indices to `\u2200 {k n : \u2115}`, while the blueprint definition says, \u201cLet $n\\in\\mathbb Z$ and $k\\in\\mathbb N$\u201d and defines $p_k(n)$ there. After unfolding the project definitions, the formal equality correctly partitions `{p | p.parts.card = k}` into the complementary predicates `p.containsOne` and `\u00acp.containsOne`, with `containsOne` defined as `1 \u2208 p.parts`. Thus the only gap is the routine negative-integer boundary case."
}