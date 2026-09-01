## TARGET Equiv.Perm.canonicalReducedWord_isReduced (theorem) — ELABORATED SIGNATURE
∀ {n : ℕ} (σ : Equiv.Perm (Fin n)), Equiv.Perm.IsReduced σ.canonicalReducedWord

Docstring: The canonical reduced word is indeed reduced. 

## PROJECT DEPENDENCY Equiv.Perm.IsReduced (def)
{n : ℕ} → Equiv.Perm.Word n → Prop

Body:
fun {n} w => List.length w = (Equiv.Perm.wordProd w).length

Docstring: A word is reduced if its length equals the length of the permutation it represents. 

## PROJECT DEPENDENCY Equiv.Perm.canonicalReducedWord (def)
{n : ℕ} → Equiv.Perm (Fin n) → Equiv.Perm.Word n

Body:
fun {n} σ => (List.map σ.lehmerBlock (List.finRange n)).flatten

Docstring: **Proposition prop.perm.redword-lehmer**: The canonical reduced word for σ.
For each i, define a_i = cyc_{i', i'-1, ..., i} = s_{i'-1} s_{i'-2} ... s_i
where i' = i + ℓ_i(σ). Then σ = a_1 a_2 ... a_n.

This gives an explicit algorithm to construct a reduced word from the Lehmer code.
The word is constructed by concatenating the Lehmer blocks for each position i = 0, 1, ..., n-1. 

## PROJECT DEPENDENCY Equiv.Perm.Word (def)
ℕ → Type

Body:
fun n => List (Fin (n - 1))

Docstring: A word is a list of indices representing simple transpositions. 

## PROJECT DEPENDENCY Equiv.Perm.length (def)
{n : ℕ} → Equiv.Perm (Fin n) → ℕ

Body:
fun {n} σ => σ.inversions.card

Docstring: The length of a permutation is the number of its inversions. 

## PROJECT DEPENDENCY Equiv.Perm.wordProd (def)
{n : ℕ} → Equiv.Perm.Word n → Equiv.Perm (Fin n)

Body:
fun {n} w => (List.map Equiv.Perm.simpleTransposition w).prod

Docstring: The product of simple transpositions corresponding to a word. 

## PROJECT DEPENDENCY Equiv.Perm.lehmerBlock (def)
{n : ℕ} → Equiv.Perm (Fin n) → Fin n → Equiv.Perm.Word n

Body:
fun {n} σ i => List.map (fun k => ⟨↑i + σ.lehmerEntry i - 1 - ↑k, ⋯⟩) (List.finRange (σ.lehmerEntry i))

Docstring: The block a_i for row i: [s_{i'-1}, s_{i'-2}, ..., s_i] where i' = i + ℓ_i(σ).
This is a descending sequence of simple transpositions.
If ℓ_i(σ) = 0, this is the empty list.

The product of this block is the cycle (i', i'-1, ..., i) which moves element
at position i to position i'. 

## PROJECT DEPENDENCY Equiv.Perm.inversions (def)
{n : ℕ} → Equiv.Perm (Fin n) → Finset (Fin n × Fin n)

Body:
fun {n} σ => {p | p.1 < p.2 ∧ σ p.2 < σ p.1}

Docstring: The set of inversions of a permutation. 

## PROJECT DEPENDENCY Equiv.Perm.simpleTransposition (def)
{n : ℕ} → Fin (n - 1) → Equiv.Perm (Fin n)

Body:
fun {n} k => if h : n > 0 then Equiv.swap (Fin.castLE ⋯ k.castSucc) (Fin.castLE ⋯ k.succ) else 1

Docstring: The simple transposition `s_k` that swaps `k` and `k+1` in `Fin n`.
For `k : Fin (n-1)`, this swaps positions `k.castSucc` and `k.succ`.

**Note:** This is equivalent to `AlgebraicCombinatorics.simpleTransposition k` from `Basics.lean`.
See `simpleTransposition_eq_canonical` for the proof of equivalence.

**Recommended:** For new code, prefer `AlgebraicCombinatorics.simpleTransposition` (the canonical
definition). Use this definition when working with reduced words and Coxeter-style arguments
within this file. 

## PROJECT DEPENDENCY Equiv.Perm.lehmerEntry (def)
{n : ℕ} → Equiv.Perm (Fin n) → Fin n → ℕ

Body:
fun {n} σ i => AlgebraicCombinatorics.Perm.lehmerEntry σ i

Docstring: Alias for the canonical Lehmer entry definition from `AlgebraicCombinatorics.Perm.lehmerEntry`.
Counts inversions (i, j) with first coordinate i. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.Perm.lehmerEntry (def)
{n : ℕ} → Equiv.Perm (Fin n) → Fin n → ℕ

Body:
fun {n} σ i => {j | i < j ∧ σ i > σ j}.card

Docstring: For σ ∈ S_n and i ∈ [n], we define ℓ_i(σ) as the number of j > i such that σ(i) > σ(j).
This counts how many elements to the right of position i are smaller than σ(i).

This is the canonical definition of Lehmer entry used throughout the project.
The equivalent formulation `i < j ∧ σ j < σ i` is provided by `lehmerEntry_eq_filter_lt`.

See Definition 1.3.5 (def.perm.lehmer1) part (a) in the source.


## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF Equiv.Perm
Sort u_1 → Sort (max 1 u_1)

Docstring: `Perm α` is the type of bijections from `α` to itself. 

## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


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

## BASE-LIBRARY REF List.length
{α : Type u_1} → List α → ℕ

Docstring: The length of a list.

This function is overridden in the compiler to `lengthTR`, which uses constant stack space.

Examples:
* `([] : List String).length = 0`
* `["green", "brown"].length = 2`


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

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

## BASE-LIBRARY REF List.flatten
{α : Type u_1} → List (List α) → List α

Docstring: Concatenates a list of lists into a single list, preserving the order of the elements.

`O(|flatten L|)`.

Examples:
* `[["a"], ["b", "c"]].flatten = ["a", "b", "c"]`
* `[["a"], [], ["b", "c"], ["d", "e", "f"]].flatten = ["a", "b", "c", "d", "e", "f"]`


## BASE-LIBRARY REF List.map
{α : Type u_1} → {β : Type u_2} → (α → β) → List α → List β

Docstring: Applies a function to each element of the list, returning the resulting list of values.

`O(|l|)`.

Examples:
* `[a, b, c].map f = [f a, f b, f c]`
* `[].map Nat.succ = []`
* `["one", "two", "three"].map (·.length) = [3, 3, 5]`
* `["one", "two", "three"].map (·.reverse) = ["eno", "owt", "eerht"]`


## BASE-LIBRARY REF List.finRange
(n : ℕ) → List (Fin n)

Docstring: Lists all elements of `Fin n` in order, starting at `0`.

Examples:
* `List.finRange 0 = ([] : List (Fin 0))`
* `List.finRange 2 = ([0, 1] : List (Fin 2))`


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


## BASE-LIBRARY REF Finset.card
{α : Type u_1} → Finset α → ℕ

Docstring: `s.card` is the number of elements of `s`, aka its cardinality.

The notation `#s` can be accessed in the `Finset` locale. 

## BASE-LIBRARY REF Prod
Type u → Type v → Type (max u v)

Docstring: The product type, usually written `α × β`. Product types are also called pair or tuple types.
Elements of this type are pairs in which the first element is an `α` and the second element is a
`β`.

Products nest to the right, so `(x, y, z) : α × β × γ` is equivalent to `(x, (y, z)) : α × (β × γ)`.


Conventions for notations in identifiers:

 * The recommended spelling of `×` in identifiers is `Prod`.

## BASE-LIBRARY REF List.prod
{α : Type u_1} → [Mul α] → [One α] → List α → α

Docstring: Computes the product of the elements of a list.

Examples:

[a, b, c].prod = a * (b * (c * 1))
[2, 3, 5].prod = 30


## BASE-LIBRARY REF Equiv.Perm.instMul
{α : Type u_4} → Mul (Equiv.Perm α)

## BASE-LIBRARY REF Equiv.Perm.instOne
{α : Type u_4} → One (Equiv.Perm α)

## BASE-LIBRARY REF Fin.mk
{n : ℕ} → (val : ℕ) → val < n → Fin n

Docstring: Creates a `Fin n` from `i : Nat` and a proof that `i < n`. 

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

## BASE-LIBRARY REF Fin.val
{n : ℕ} → Fin n → ℕ

Docstring: The number that is strictly less than `n`.

`Fin.val` is a coercion, so any `Fin n` can be used in a position where a `Nat` is expected.


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

## BASE-LIBRARY REF LT.lt
{α : Type u} → [self : LT α] → α → α → Prop

Docstring: The less-than relation: `x < y` 

Conventions for notations in identifiers:

 * The recommended spelling of `<` in identifiers is `lt`.

## BASE-LIBRARY REF instLTFin
{n : ℕ} → LT (Fin n)

## BASE-LIBRARY REF Prod.fst
{α : Type u} → {β : Type v} → α × β → α

Docstring: The first element of a pair. 

## BASE-LIBRARY REF Prod.snd
{α : Type u} → {β : Type v} → α × β → β

Docstring: The second element of a pair. 

## BASE-LIBRARY REF DFunLike.coe
{F : Sort u_1} → {α : outParam (Sort u_2)} → {β : outParam (α → Sort u_3)} → [self : DFunLike F α β] → F → (a : α) → β a

Docstring: The coercion from `F` to a function. 

## BASE-LIBRARY REF EquivLike.toFunLike
{E : Sort u_1} → {α : Sort u_3} → {β : Sort u_4} → [EquivLike E α β] → FunLike E α β

## BASE-LIBRARY REF Equiv.instEquivLike
{α : Sort u} → {β : Sort v} → EquivLike (α ≃ β) α β

## BASE-LIBRARY REF instDecidableAnd
{p q : Prop} → [dp : Decidable p] → [dq : Decidable q] → Decidable (p ∧ q)

## BASE-LIBRARY REF Fin.decLt
{n : ℕ} → (a b : Fin n) → Decidable (a < b)

## BASE-LIBRARY REF Finset.univ
{α : Type u_1} → [Fintype α] → Finset α

Docstring: `univ` is the universal finite set of type `Finset α` implied from
the assumption `Fintype α`. 

## BASE-LIBRARY REF instFintypeProd
(α : Type u_4) → (β : Type u_5) → [Fintype α] → [Fintype β] → Fintype (α × β)

## BASE-LIBRARY REF Fin.fintype
(n : ℕ) → Fintype (Fin n)

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


## BASE-LIBRARY REF Equiv.swap
{α : Sort u_1} → [DecidableEq α] → α → α → Equiv.Perm α

Docstring: `swap a b` is the permutation that swaps `a` and `b` and
leaves other values as is. 

## BASE-LIBRARY REF instDecidableEqFin
(n : ℕ) → DecidableEq (Fin n)

## BASE-LIBRARY REF Fin.castLE
{n m : ℕ} → n ≤ m → Fin n → Fin m

Docstring: Coarsens a bound to one at least as large.

See also `Fin.castAdd` for a version that represents the larger bound with addition rather than an
explicit inequality proof.


## BASE-LIBRARY REF Fin.castSucc
{n : ℕ} → Fin n → Fin (n + 1)

Docstring: Coarsens a bound by one.


## BASE-LIBRARY REF Fin.succ
{n : ℕ} → Fin n → Fin (n + 1)

Docstring: The successor, with an increased bound.

This differs from adding `1`, which instead wraps around.

Examples:
* `(2 : Fin 3).succ = (3 : Fin 4)`
* `(2 : Fin 3) + 1 = (0 : Fin 3)`


## BASE-LIBRARY REF Not
Prop → Prop

Docstring: `Not p`, or `¬p`, is the negation of `p`. It is defined to be `p → False`,
so if your goal is `¬p` you can use `intro h` to turn the goal into
`h : p ⊢ False`, and if you have `hn : ¬p` and `h : p` then `hn h : False`
and `(hn h).elim` will prove anything.
For more information: [Propositional Logic](https://lean-lang.org/theorem_proving_in_lean4/propositions_and_proofs.html#propositional-logic)


Conventions for notations in identifiers:

 * The recommended spelling of `¬` in identifiers is `not`.

## BASE-LIBRARY REF One.toOfNat1
{α : Type u_1} → [One α] → OfNat α 1

## INFORMAL STATEMENT
thm.perm.canonicalReducedWord-isReduced

\leanhelper  The canonical reduced word is indeed reduced: it is a word of length $\ell (\sigma )$ whose product is $\sigma $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-conv-2eb59533
conv-2eb59533

In the Lean formalization, we use $\operatorname {Fin} n = \{ 0, 1, \ldots , n-1\} $ instead of the textbook’s $[n] = \{ 1, 2, \ldots , n\} $. Both are $n$-element sets, so their symmetric groups are isomorphic. Permutations are represented by the type of bijections $X \to X$ (denoted $\operatorname {Equiv.Perm}\,  X$ in Lean), which is a group under composition. Composition $\alpha \beta $ is the group multiplication $\alpha * \beta $, sending $x$ to $\alpha (\beta (x))$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-conv.perm.simple
conv.perm.simple

A \emph{simple transposition} in $S_n$ means one of the $n-1$ transpositions $s_0, s_1, \ldots , s_{n-2}$. We shall occasionally abbreviate “simple transposition” as “simple”.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.canonicalreducedword
def.perm.canonicalReducedWord

\leanhelper  The \emph{canonical reduced word} for $\sigma $ is the concatenation of Lehmer blocks: 

\[  w(\sigma ) = a_0 \mathbin {+\! +} a_1 \mathbin {+\! +} \cdots \mathbin {+\! +} a_{n-1}.  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.isreduced
def.perm.IsReduced

\leanhelper  A word $w = (k_1, \ldots , k_q)$ is \emph{reduced} if its length $q$ equals $\ell (s_{k_1} \cdots s_{k_q})$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.perm
def.perm.perm

Let $X$ be a set. 

\textbf{(a)} A \emph{permutation} of $X$ means a bijection from $X$ to $X$. 

\textbf{(b)} It is known that the set of all permutations of $X$ is a group under composition. This group is called the \emph{symmetric group} of $X$, and is denoted by $S_X$. Its neutral element is the identity map $\operatorname {id}_X : X \to X$. Its size is $|X|!$ when $X$ is finite. 

\textbf{(c)} As usual in group theory, we will write $\alpha \beta $ for the composition $\alpha \circ \beta $ when $\alpha , \beta \in S_X$. This is the map that sends each $x \in X$ to $\alpha (\beta (x))$. 

\textbf{(d)} If $\alpha \in S_X$ and $i \in \mathbb {Z}$, then $\alpha ^i$ shall denote the $i$-th power of $\alpha $ in the group $S_X$. Note that $\alpha ^i = \underbrace{\alpha \circ \alpha \circ \cdots \circ \alpha }_{i\text{ times}}$ if $i \ge 0$. Also, $\alpha ^0 = \operatorname {id}_X$. Also, $\alpha ^{-1}$ is the inverse of $\alpha $ in the group $S_X$, that is, the inverse of the map $\alpha $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.si
def.perm.si

Let $n \in \mathbb {N}$ and $i \in [n-1]$. Then, the \emph{simple transposition} $s_i$ is defined by 

\[  s_i := t_{i, i+1} \in S_n.  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.sn-iven
def.perm.Sn-iven

Let $n \in \mathbb {Z}$. Then, $[n]$ shall mean the set $\{ 1, 2, \ldots , n\} $. This is an $n$-element set if $n \ge 0$, and is an empty set if $n \le 0$. 

The symmetric group $S_{[n]}$ (consisting of all permutations of $[n]$) will be denoted $S_n$ and called the $n$\emph{-th symmetric group}. Its size is $n!$ (when $n \ge 0$).

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.tij
def.perm.tij

Let $i$ and $j$ be two distinct elements of a set $X$. 

Then, the \emph{transposition} $t_{i,j}$ is the permutation of $X$ that sends $i$ to $j$, sends $j$ to $i$, and leaves all other elements of $X$ unchanged.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.word
def.perm.Word

\leanhelper  A \emph{word} (of length $q$) in $S_n$ is a finite sequence $(k_1, k_2, \ldots , k_q)$ where each $k_i \in \{ 0, 1, \ldots , n-2\} $ is an index of a simple transposition.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.wordprod
def.perm.wordProd

\leanhelper  The \emph{product} of a word $w = (k_1, \ldots , k_q)$ is the permutation $s_{k_1} s_{k_2} \cdots s_{k_q}$.

## VERDICT
{
  "verdict": "drift",
  "justification": "The informal statement requires both that the canonical word has length \u2113(\u03c3) and that \u201cits product is \u03c3.\u201d The formal conclusion is only `Equiv.Perm.IsReduced \u03c3.canonicalReducedWord`, which unfolds via `IsReduced` to `List.length \u03c3.canonicalReducedWord = (Equiv.Perm.wordProd \u03c3.canonicalReducedWord).length`. This compares the word\u2019s length with the inversion length of its own product; it does not state `Equiv.Perm.wordProd \u03c3.canonicalReducedWord = \u03c3`, and consequently does not directly state that its length is `\u03c3.length`. The difference is in the TARGET conclusion, not in an added binder. To match the blueprint, the conclusion should additionally assert `Equiv.Perm.wordProd \u03c3.canonicalReducedWord = \u03c3` and, either directly or through `IsReduced`, that `List.length \u03c3.canonicalReducedWord = \u03c3.length`; for example, a conjunction of the product equality with `IsReduced \u03c3.canonicalReducedWord` would express the intended content."
}