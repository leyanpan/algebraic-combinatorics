## TARGET AlgebraicCombinatorics.SubtractiveMethods.signTupleEquivSubset (def) — ELABORATED SIGNATURE
(d : ℕ) → (Fin d → ZMod 2) ≃ Finset (Fin d)

Body:
fun d =>
  { toFun := AlgebraicCombinatorics.SubtractiveMethods.signTupleToSubset,
    invFun := AlgebraicCombinatorics.SubtractiveMethods.subsetToSignTuple, left_inv := ⋯, right_inv := ⋯ }

Docstring: Equivalence between sign tuples and subsets of `[d]` 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SubtractiveMethods.signTupleToSubset (def)
{d : ℕ} → (Fin d → ZMod 2) → Finset (Fin d)

Body:
fun {d} e => {k | e k = 1}

Docstring: Bijection between sign tuples and subsets of `[d]`:
A sign tuple `(e_1, ..., e_d) ∈ {1,-1}^d` corresponds to the set
`{i ∈ [d] | e_i = -1}` of positions with -1. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SubtractiveMethods.subsetToSignTuple (def)
{d : ℕ} → Finset (Fin d) → Fin d → ZMod 2

Body:
fun {d} S k => if k ∈ S then 1 else 0

Docstring: Inverse of signTupleToSubset: given a subset S, produce the sign tuple
where position k has value 1 (representing -1) iff k ∈ S 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SubtractiveMethods.subsetToSignTuple_signTupleToSubset (theorem)
∀ {d : ℕ} (e : Fin d → ZMod 2),
  AlgebraicCombinatorics.SubtractiveMethods.subsetToSignTuple
      (AlgebraicCombinatorics.SubtractiveMethods.signTupleToSubset e) =
    e

## PROJECT DEPENDENCY AlgebraicCombinatorics.SubtractiveMethods.signTupleToSubset_subsetToSignTuple (theorem)
∀ {d : ℕ} (S : Finset (Fin d)),
  AlgebraicCombinatorics.SubtractiveMethods.signTupleToSubset
      (AlgebraicCombinatorics.SubtractiveMethods.subsetToSignTuple S) =
    S

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF Equiv
Sort u_1 → Sort u_2 → Sort (max (max 1 u_1) u_2)

Docstring: `α ≃ β` is the type of functions from `α → β` with a two-sided inverse. 

## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


## BASE-LIBRARY REF ZMod
ℕ → Type

Docstring: The integers modulo `n : ℕ`. 

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

## BASE-LIBRARY REF Finset
Type u_4 → Type u_4

Docstring: `Finset α` is the type of finite sets of elements of `α`. It is implemented
as a multiset (a list up to permutation) which has no duplicate elements. 

## BASE-LIBRARY REF Equiv.mk
{α : Sort u_1} →
  {β : Sort u_2} →
    (toFun : α → β) →
      (invFun : β → α) →
        autoParam (Function.LeftInverse invFun toFun) Equiv.left_inv._autoParam →
          autoParam (Function.RightInverse invFun toFun) Equiv.right_inv._autoParam → α ≃ β

## BASE-LIBRARY REF Finset.filter
{α : Type u_1} → (p : α → Prop) → [DecidablePred p] → Finset α → Finset α

Docstring: `Finset.filter p s` is the set of elements of `s` that satisfy `p`.

For example, one can use `s.filter (· ∈ t)` to get the intersection of `s` with `t : Set α`
as a `Finset α` (when a `DecidablePred (· ∈ t)` instance is available). 

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

## BASE-LIBRARY REF One.toOfNat1
{α : Type u_1} → [One α] → OfNat α 1

## BASE-LIBRARY REF AddMonoidWithOne.toOne
{R : Type u_2} → [self : AddMonoidWithOne R] → One R

## BASE-LIBRARY REF AddGroupWithOne.toAddMonoidWithOne
{R : Type u} → [self : AddGroupWithOne R] → AddMonoidWithOne R

## BASE-LIBRARY REF Ring.toAddGroupWithOne
{R : Type u} → [self : Ring R] → AddGroupWithOne R

## BASE-LIBRARY REF DivisionRing.toRing
{K : Type u_2} → [self : DivisionRing K] → Ring K

## BASE-LIBRARY REF Field.toDivisionRing
{K : Type u} → [self : Field K] → DivisionRing K

## BASE-LIBRARY REF ZMod.instField
(p : ℕ) → [hp : Fact (Nat.Prime p)] → Field (ZMod p)

Docstring: Field structure on `ZMod p` if `p` is prime. 

## BASE-LIBRARY REF Nat.fact_prime_two
Fact (Nat.Prime 2)

## BASE-LIBRARY REF ZMod.decidableEq
(n : ℕ) → DecidableEq (ZMod n)

## BASE-LIBRARY REF Finset.univ
{α : Type u_1} → [Fintype α] → Finset α

Docstring: `univ` is the universal finite set of type `Finset α` implied from
the assumption `Fintype α`. 

## BASE-LIBRARY REF Fin.fintype
(n : ℕ) → Fintype (Fin n)

## BASE-LIBRARY REF ite
{α : Sort u} → (c : Prop) → [h : Decidable c] → α → α → α

Docstring: `if c then t else e` is notation for `ite c t e`, "if-then-else", which decides to
return `t` or `e` depending on whether `c` is true or false. The explicit argument
`c : Prop` does not have any actual computational content, but there is an additional
`[Decidable c]` argument synthesized by typeclass inference which actually
determines how to evaluate `c` to true or false. Write `if h : c then t else e`
instead for a "dependent if-then-else" `dite`, which allows `t`/`e` to use the fact
that `c` is true/false.


## BASE-LIBRARY REF Membership.mem
{α : outParam (Type u)} → {γ : Type v} → [self : Membership α γ] → γ → α → Prop

Docstring: The membership relation `a ∈ s : Prop` where `a : α`, `s : γ`. 

Conventions for notations in identifiers:

 * The recommended spelling of `∈` in identifiers is `mem`.

## BASE-LIBRARY REF Finset.instMembership
{α : Type u_1} → Membership α (Finset α)

## BASE-LIBRARY REF Finset.decidableMem
{α : Type u_1} → [_h : DecidableEq α] → (a : α) → (s : Finset α) → Decidable (a ∈ s)

## BASE-LIBRARY REF instDecidableEqFin
(n : ℕ) → DecidableEq (Fin n)

## BASE-LIBRARY REF Zero.toOfNat0
{α : Type u_1} → [Zero α] → OfNat α 0

## BASE-LIBRARY REF MulZeroClass.toZero
{M₀ : Type u} → [self : MulZeroClass M₀] → Zero M₀

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.toMulZeroClass
{α : Type u} → [self : NonUnitalNonAssocSemiring α] → MulZeroClass α

## BASE-LIBRARY REF NonUnitalNonAssocRing.toNonUnitalNonAssocSemiring
{α : Type u} → [self : NonUnitalNonAssocRing α] → NonUnitalNonAssocSemiring α

## BASE-LIBRARY REF NonUnitalNonAssocCommRing.toNonUnitalNonAssocRing
{α : Type u} → [self : NonUnitalNonAssocCommRing α] → NonUnitalNonAssocRing α

## BASE-LIBRARY REF NonUnitalCommRing.toNonUnitalNonAssocCommRing
{α : Type u} → [self : NonUnitalCommRing α] → NonUnitalNonAssocCommRing α

## BASE-LIBRARY REF CommRing.toNonUnitalCommRing
{α : Type u} → [s : CommRing α] → NonUnitalCommRing α

## BASE-LIBRARY REF ZMod.commRing
(n : ℕ) → CommRing (ZMod n)

## INFORMAL STATEMENT
lem.cancel.signTupleEquivSubset

\leanhelper  There is a bijection between sign tuples $\{ 1,-1\} ^d$ and subsets of $[d]$, sending each tuple $e$ to the set $S = \{ i \in [d] \mid e_i = -1\} $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-conv-2eb59533
conv-2eb59533

In the Lean formalization, we use $\operatorname {Fin} n = \{ 0, 1, \ldots , n-1\} $ instead of the textbook’s $[n] = \{ 1, 2, \ldots , n\} $. Both are $n$-element sets, so their symmetric groups are isomorphic. Permutations are represented by the type of bijections $X \to X$ (denoted $\operatorname {Equiv.Perm}\,  X$ in Lean), which is a group under composition. Composition $\alpha \beta $ is the group multiplication $\alpha * \beta $, sending $x$ to $\alpha (\beta (x))$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.cancel.signtupletosubset
Sign tuple to subset

\leanhelper  The map $\operatorname {signTupleToSubset} : (\operatorname {Fin} d \to \mathbb {Z}/2\mathbb {Z}) \to \mathcal{P}(\operatorname {Fin} d)$ sends a sign tuple $e$ to the set $S = \{ k \in \operatorname {Fin} d \mid e_k = 1\} $ (i.e., the positions where $\operatorname {toSign}(e_k) = -1$).

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.cancel.tosign
Sign conversion

\leanhelper  The function $\operatorname {toSign} : \mathbb {Z}/2\mathbb {Z} \to \mathbb {Z}$ converts elements of $\mathbb {Z}/2\mathbb {Z}$ to signs: $\operatorname {toSign}(0) = 1$ and $\operatorname {toSign}(1) = -1$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.perm
def.perm.perm

Let $X$ be a set. 

\textbf{(a)} A \emph{permutation} of $X$ means a bijection from $X$ to $X$. 

\textbf{(b)} It is known that the set of all permutations of $X$ is a group under composition. This group is called the \emph{symmetric group} of $X$, and is denoted by $S_X$. Its neutral element is the identity map $\operatorname {id}_X : X \to X$. Its size is $|X|!$ when $X$ is finite. 

\textbf{(c)} As usual in group theory, we will write $\alpha \beta $ for the composition $\alpha \circ \beta $ when $\alpha , \beta \in S_X$. This is the map that sends each $x \in X$ to $\alpha (\beta (x))$. 

\textbf{(d)} If $\alpha \in S_X$ and $i \in \mathbb {Z}$, then $\alpha ^i$ shall denote the $i$-th power of $\alpha $ in the group $S_X$. Note that $\alpha ^i = \underbrace{\alpha \circ \alpha \circ \cdots \circ \alpha }_{i\text{ times}}$ if $i \ge 0$. Also, $\alpha ^0 = \operatorname {id}_X$. Also, $\alpha ^{-1}$ is the inverse of $\alpha $ in the group $S_X$, that is, the inverse of the map $\alpha $.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The blueprint asserts a bijection between sign tuples and subsets of `[d]`, \u201csending each tuple `e` to the set \u2026 where `e_i = -1`.\u201d Its definitions encode sign tuples as `Fin d \u2192 ZMod 2`, encode `[d]` as `Fin d`, and specify that residue `1` represents sign `-1`. The target `(d : \u2115) \u2192 (Fin d \u2192 ZMod 2) \u2243 Finset (Fin d)` gives exactly such a bijection, with `toFun := signTupleToSubset`; that dependency has body `fun e => {k | e k = 1}`, exactly the specified subset. Its inverse has body `fun S k => if k \u2208 S then 1 else 0`, and the two cited inverse laws establish the equivalence. `Finset (Fin d)` faithfully represents subsets because `Fin d` is finite, and there are no additional mathematical hypotheses."
}