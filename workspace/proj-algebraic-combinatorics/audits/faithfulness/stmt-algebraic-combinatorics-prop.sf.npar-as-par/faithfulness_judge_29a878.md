## TARGET AlgebraicCombinatorics.SymmetricFunctions.NPartition.equivPartition (def) — ELABORATED SIGNATURE
{N : ℕ} → (n : ℕ) → { p // p.parts.card ≤ N } ≃ { mu // NPartition.size mu = n }

Body:
fun {N} n =>
  {
    toFun := fun x =>
      match x with
      | ⟨p, hp⟩ => ⟨AlgebraicCombinatorics.SymmetricFunctions.NPartition.ofPartition p hp, ⋯⟩,
    invFun := fun x =>
      match x with
      | ⟨mu, hmu⟩ =>
        let p' := mu.toPartition;
        have hp' := ⋯;
        ⟨hmu ▸ p', ⋯⟩,
    left_inv := ⋯, right_inv := ⋯ }

Docstring: The equivalence between partitions of length ≤ N that sum to n and N-partitions of size n.
(Proposition prop.sf.Npar-as-par)

This provides the bijection:
- Forward: pad partition with zeros to get N-partition
- Backward: remove trailing zeros from N-partition to get partition

Note: We state this as an `Equiv` which is the proper way to express a bijection in Mathlib. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SymmetricFunctions.NPartition (def)
ℕ → Type

Body:
fun N => NPartition N

Docstring: Alias for the canonical `NPartition` type within this namespace.
An N-partition is a weakly decreasing N-tuple of nonnegative integers.
(Definition def.sf.Npar)

This is represented as a function `Fin N → ℕ` that is antitone
(i.e., `i ≤ j → parts j ≤ parts i`).

All basic operations (`size`, `length`, `zero`, etc.) and lemmas are inherited
from the canonical `_root_.NPartition` definition in `NPartition.lean`. 

## PROJECT DEPENDENCY NPartition.size (def)
{N : ℕ} → NPartition N → ℕ

Body:
fun {N} μ => ∑ i, μ.parts i

Docstring: The size (or weight) of an N-partition is the sum of its entries.
If μ = (μ₁, μ₂, ..., μ_N), then |μ| = μ₁ + μ₂ + ... + μ_N. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SymmetricFunctions.NPartition.ofPartition (def)
{N n : ℕ} → (p : n.Partition) → p.parts.card ≤ N → AlgebraicCombinatorics.SymmetricFunctions.NPartition N

Body:
fun {N n} p hp => NPartition.ofPartition p hp

Docstring: Convert a partition (as a `Nat.Partition`) to an N-partition by padding with zeros.
Re-export of `_root_.NPartition.ofPartition`. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SymmetricFunctions.NPartition.ofPartition_size (theorem)
∀ {N n : ℕ} (p : n.Partition) (hp : p.parts.card ≤ N),
  NPartition.size (AlgebraicCombinatorics.SymmetricFunctions.NPartition.ofPartition p hp) = n

Docstring: The size of ofPartition p equals n (the sum of the original partition).
Re-export of `_root_.NPartition.ofPartition_size`. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SymmetricFunctions.NPartition.toPartition (def)
{N : ℕ} → (mu : AlgebraicCombinatorics.SymmetricFunctions.NPartition N) → (NPartition.size mu).Partition

Body:
fun {N} mu => NPartition.toPartition mu

Docstring: Convert an N-partition to a partition by removing trailing zeros.
Re-export of `_root_.NPartition.toPartition`. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SymmetricFunctions.NPartition.toPartition_card_le (theorem)
∀ {N : ℕ} (mu : AlgebraicCombinatorics.SymmetricFunctions.NPartition N), mu.toPartition.parts.card ≤ N

Docstring: The number of non-zero parts of an N-partition is at most N.
Re-export of `_root_.NPartition.toPartition_card_le`. 

## PROJECT DEPENDENCY NPartition (inductive)
ℕ → Type

Body:
NPartition.mk : {N : ℕ} → (parts : Fin N → ℕ) → Antitone parts → NPartition N

Docstring: An N-partition is a weakly decreasing N-tuple of nonnegative integers.
(Definition def.sf.Npar)

This is represented as a function `Fin N → ℕ` that is antitone
(i.e., `i ≤ j → parts j ≤ parts i`).

The field is named `antitone` to match Mathlib conventions. 

## PROJECT DEPENDENCY NPartition.parts (def)
{N : ℕ} → NPartition N → Fin N → ℕ

Body:
fun N self => self.1

Docstring: The entries of the N-partition as a function from `Fin N` to `ℕ` 

## PROJECT DEPENDENCY NPartition.ofPartition (def)
{N n : ℕ} → (p : n.Partition) → p.parts.card ≤ N → NPartition N

Body:
fun {N n} p _hp =>
  {
    parts := fun i =>
      have sorted := p.parts.sort fun x1 x2 => x1 ≥ x2;
      if h : ↑i < sorted.length then sorted.get ⟨↑i, h⟩ else 0,
    antitone := ⋯ }

Docstring: Convert a partition (as a `Nat.Partition`) to an N-partition by padding with zeros.
Requires that the partition has at most N parts.

This corresponds to the map in Proposition prop.sf.Npar-as-par:
(μ₁, μ₂, ..., μ_ℓ) ↦ (μ₁, μ₂, ..., μ_ℓ, 0, 0, ..., 0) 

## PROJECT DEPENDENCY NPartition.toPartition (def)
{N : ℕ} → (μ : NPartition N) → μ.size.Partition

Body:
fun {N} μ =>
  { parts := Multiset.filter (fun x => x ≠ 0) (Multiset.map μ.parts Finset.univ.val), parts_pos := ⋯, parts_sum := ⋯ }

Docstring: Convert an N-partition to a partition by removing trailing zeros. 

## PROJECT DEPENDENCY NPartition.mk (constructor)
{N : ℕ} → (parts : Fin N → ℕ) → Antitone parts → NPartition N

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF Equiv
Sort u_1 → Sort u_2 → Sort (max (max 1 u_1) u_2)

Docstring: `α ≃ β` is the type of functions from `α → β` with a two-sided inverse. 

## BASE-LIBRARY REF Subtype
{α : Sort u} → (α → Prop) → Sort (max 1 u)

Docstring: All the elements of a type that satisfy a predicate.

`Subtype p`, usually written `{ x : α // p x }` or `{ x // p x }`, contains all elements `x : α` for
which `p x` is true. Its constructor is a pair of the value and the proof that it satisfies the
predicate. In run-time code, `{ x : α // p x }` is represented identically to `α`.

There is a coercion from `{ x : α // p x }` to `α`, so elements of a subtype may be used where the
underlying type is expected.

Examples:
 * `{ n : Nat // n % 2 = 0 }` is the type of even numbers.
 * `{ xs : Array String // xs.size = 5 }` is the type of arrays with five `String`s.
 * Given `xs : List α`, `List { x : α // x ∈ xs }` is the type of lists in which all elements are
   contained in `xs`.


Conventions for notations in identifiers:

 * The recommended spelling of `{ x // p x }` in identifiers is `subtype`.

## BASE-LIBRARY REF Nat.Partition
ℕ → Type

Docstring: A partition of `n` is a multiset of positive integers summing to `n`. 

## BASE-LIBRARY REF LE.le
{α : Type u} → [self : LE α] → α → α → Prop

Docstring: The less-equal relation: `x ≤ y` 

Conventions for notations in identifiers:

 * The recommended spelling of `≤` in identifiers is `le`.

 * The recommended spelling of `<=` in identifiers is `le` (prefer `≤` over `<=`).

## BASE-LIBRARY REF instLENat
LE ℕ

## BASE-LIBRARY REF Multiset.card
{α : Type u_1} → Multiset α → ℕ

Docstring: The cardinality of a multiset is the sum of the multiplicities
of all its elements, or simply the length of the underlying list. 

## BASE-LIBRARY REF Nat.Partition.parts
{n : ℕ} → n.Partition → Multiset ℕ

Docstring: positive integers summing to `n` 

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

## BASE-LIBRARY REF Equiv.mk
{α : Sort u_1} →
  {β : Sort u_2} →
    (toFun : α → β) →
      (invFun : β → α) →
        autoParam (Function.LeftInverse invFun toFun) Equiv.left_inv._autoParam →
          autoParam (Function.RightInverse invFun toFun) Equiv.right_inv._autoParam → α ≃ β

## BASE-LIBRARY REF Subtype.mk
{α : Sort u} → {p : α → Prop} → (val : α) → p val → Subtype p

## BASE-LIBRARY REF Eq.rec
{α : Sort u_1} →
  {a : α} → {motive : (a_1 : α) → a = a_1 → Sort u} → motive a ⋯ → {a_1 : α} → (t : a = a_1) → motive a_1 t

## BASE-LIBRARY REF Finset.sum
{ι : Type u_1} → {M : Type u_3} → [AddCommMonoid M] → Finset ι → (ι → M) → M

Docstring: `∑ x ∈ s, f x` is the sum of `f x` as `x` ranges over the elements
of the finite set `s`.

When the index type is a `Fintype`, the notation `∑ x, f x`, is a shorthand for
`∑ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


## BASE-LIBRARY REF Nat.instAddCommMonoid
AddCommMonoid ℕ

## BASE-LIBRARY REF Finset.univ
{α : Type u_1} → [Fintype α] → Finset α

Docstring: `univ` is the universal finite set of type `Finset α` implied from
the assumption `Fintype α`. 

## BASE-LIBRARY REF Fin.fintype
(n : ℕ) → Fintype (Fin n)

## BASE-LIBRARY REF Antitone
{α : Type u} → {β : Type v} → [Preorder α] → [Preorder β] → (α → β) → Prop

Docstring: A function `f` is antitone if `a ≤ b` implies `f b ≤ f a`. 

## BASE-LIBRARY REF PartialOrder.toPreorder
{α : Type u_2} → [self : PartialOrder α] → Preorder α

## BASE-LIBRARY REF Fin.instPartialOrder
{n : ℕ} → PartialOrder (Fin n)

## BASE-LIBRARY REF Nat.instPreorder
Preorder ℕ

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


## BASE-LIBRARY REF Multiset.sort
{α : Type u_1} →
  Multiset α →
    (r : autoParam (α → α → Prop) Multiset.sort._auto_1) →
      [DecidableRel r] → [IsTrans α r] → [Std.Antisymm r] → [Std.Total r] → List α

Docstring: `sort s` constructs a sorted list from the multiset `s`.
(Uses merge sort algorithm.) 

## BASE-LIBRARY REF GE.ge
{α : Type u} → [LE α] → α → α → Prop

Docstring: `a ≥ b` is an abbreviation for `b ≤ a`. 

Conventions for notations in identifiers:

 * The recommended spelling of `≥` in identifiers is `ge`.

 * The recommended spelling of `>=` in identifiers is `ge` (prefer `≥` over `>=`).

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

## BASE-LIBRARY REF instAntisymmGe
∀ {α : Type u} [inst : PartialOrder α], Std.Antisymm fun x1 x2 => x2 ≤ x1

## BASE-LIBRARY REF Nat.instPartialOrder
PartialOrder ℕ

## BASE-LIBRARY REF LE.total'
∀ {α : Type u} [inst : LinearOrder α], Std.Total fun x1 x2 => x2 ≤ x1

## BASE-LIBRARY REF Nat.instLinearOrder
LinearOrder ℕ

## BASE-LIBRARY REF dite
{α : Sort u} → (c : Prop) → [h : Decidable c] → (c → α) → (¬c → α) → α

Docstring: "Dependent" if-then-else, normally written via the notation `if h : c then t(h) else e(h)`,
is sugar for `dite c (fun h => t(h)) (fun h => e(h))`, and it is the same as
`if c then t else e` except that `t` is allowed to depend on a proof `h : c`,
and `e` can depend on `h : ¬c`. (Both branches use the same name for the hypothesis,
even though it has different types in the two cases.)

We use this to be able to communicate the if-then-else condition to the branches.
For example, `Array.get arr i h` expects a proof `h : i < arr.size` in order to
avoid a bounds check, so you can write `if h : i < arr.size then arr.get i h else ...`
to avoid the bounds check inside the if branch. (Of course in this case we have only
lifted the check into an explicit `if`, but we could also use this proof multiple times
or derive `i < arr.size` from some other proposition that we are checking in the `if`.)


## BASE-LIBRARY REF LT.lt
{α : Type u} → [self : LT α] → α → α → Prop

Docstring: The less-than relation: `x < y` 

Conventions for notations in identifiers:

 * The recommended spelling of `<` in identifiers is `lt`.

## BASE-LIBRARY REF instLTNat
LT ℕ

## BASE-LIBRARY REF Fin.val
{n : ℕ} → Fin n → ℕ

Docstring: The number that is strictly less than `n`.

`Fin.val` is a coercion, so any `Fin n` can be used in a position where a `Nat` is expected.


## BASE-LIBRARY REF List.length
{α : Type u_1} → List α → ℕ

Docstring: The length of a list.

This function is overridden in the compiler to `lengthTR`, which uses constant stack space.

Examples:
* `([] : List String).length = 0`
* `["green", "brown"].length = 2`


## BASE-LIBRARY REF Nat.decLt
(n m : ℕ) → Decidable (n < m)

Docstring: A decision procedure for strict inequality of natural numbers, usually accessed via the
`DecidableLT Nat` instance.

Examples:
 * `(if 3 < 4 then "yes" else "no") = "yes"`
 * `(if 4 < 4 then "yes" else "no") = "no"`
 * `(if 6 < 4 then "yes" else "no") = "no"`
 * `show 5 < 12 by decide`


## BASE-LIBRARY REF List.get
{α : Type u} → (as : List α) → Fin as.length → α

Docstring: Returns the element at the provided index, counting from `0`.

In other words, for `i : Fin as.length`, `as.get i` returns the `i`'th element of the list `as`.
Because the index is a `Fin` bounded by the list's length, the index will never be out of bounds.

Examples:
 * `["spring", "summer", "fall", "winter"].get (2 : Fin 4) = "fall"`
 * `["spring", "summer", "fall", "winter"].get (0 : Fin 4) = "spring"`


## BASE-LIBRARY REF Fin.mk
{n : ℕ} → (val : ℕ) → val < n → Fin n

Docstring: Creates a `Fin n` from `i : Nat` and a proof that `i < n`. 

## BASE-LIBRARY REF Not
Prop → Prop

Docstring: `Not p`, or `¬p`, is the negation of `p`. It is defined to be `p → False`,
so if your goal is `¬p` you can use `intro h` to turn the goal into
`h : p ⊢ False`, and if you have `hn : ¬p` and `h : p` then `hn h : False`
and `(hn h).elim` will prove anything.
For more information: [Propositional Logic](https://lean-lang.org/theorem_proving_in_lean4/propositions_and_proofs.html#propositional-logic)


Conventions for notations in identifiers:

 * The recommended spelling of `¬` in identifiers is `not`.

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

## BASE-LIBRARY REF Nat.Partition.mk
{n : ℕ} → (parts : Multiset ℕ) → (∀ {i : ℕ}, i ∈ parts → 0 < i) → parts.sum = n → n.Partition

## BASE-LIBRARY REF Multiset.filter
{α : Type u_1} → (p : α → Prop) → [DecidablePred p] → Multiset α → Multiset α

Docstring: `Filter p s` returns the elements in `s` (with the same multiplicities)
which satisfy `p`, and removes the rest. 

## BASE-LIBRARY REF Ne
{α : Sort u} → α → α → Prop

Docstring: `a ≠ b`, or `Ne a b` is defined as `¬ (a = b)` or `a = b → False`,
and asserts that `a` and `b` are not equal.


Conventions for notations in identifiers:

 * The recommended spelling of `≠` in identifiers is `ne`.

## BASE-LIBRARY REF instDecidableNot
{p : Prop} → [dp : Decidable p] → Decidable ¬p

## BASE-LIBRARY REF instDecidableEqNat
DecidableEq ℕ

## BASE-LIBRARY REF Multiset.map
{α : Type u_1} → {β : Type v} → (α → β) → Multiset α → Multiset β

Docstring: `map f s` is the lift of the list `map` operation. The multiplicity
of `b` in `map f s` is the number of `a ∈ s` (counting multiplicity)
such that `f a = b`. 

## BASE-LIBRARY REF Finset.val
{α : Type u_4} → Finset α → Multiset α

Docstring: The underlying multiset 

## INFORMAL STATEMENT
prop.sf.Npar-as-par

There is a bijection

\begin{align*}  \left\{  \text{partitions of length }\leq N\right\}  &  \rightarrow \left\{  N\text{-partitions}\right\}  ,\\ \left( \lambda _{1},\lambda _{2},\ldots ,\lambda _{\ell }\right) &  \mapsto \left( \lambda _{1},\lambda _{2},\ldots ,\lambda _{\ell },\underbrace{0,0,\ldots ,0}_{N-\ell \text{ zeroes}}\right) . \end{align*}

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.npar
def.sf.Npar

An $N$\emph{-partition} will mean a weakly decreasing $N$-tuple of nonnegative integers. In other words, an $N$-partition means an $N$-tuple $\left( \lambda _{1},\lambda _{2},\ldots ,\lambda _{N}\right) \in \mathbb {N}^{N}$ with $\lambda _{1}\geq \lambda _{2}\geq \cdots \geq \lambda _{N}$. 

The \emph{size} (or weight) of an $N$-partition $\lambda = (\lambda _1, \lambda _2, \ldots , \lambda _N)$ is defined to be $|\lambda | := \lambda _1 + \lambda _2 + \cdots + \lambda _N$.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The blueprint states a bijection from \u201cpartitions of length \u2264 N\u201d to \u201cN-partitions,\u201d given by padding with zeros. The target universally quantifies both parameters, `{N : \u2115} \u2192 (n : \u2115) \u2192`, and gives the fiberwise equivalence `{ p // p.parts.card \u2264 N } \u2243 { mu // NPartition.size mu = n }`, where `p : n.Partition`. Thus, for every size `n`, it bijects partitions of size `n` and length at most `N` with N-partitions of size `n`. Taking all sizes yields the blueprint\u2019s unrestricted bijection, and the formal statement additionally records preservation of size. Its forward map is exactly `NPartition.ofPartition p hp`, whose body pads the descending parts with zeros, while the inverse `mu.toPartition` removes zeros. There are no added mathematical hypotheses."
}