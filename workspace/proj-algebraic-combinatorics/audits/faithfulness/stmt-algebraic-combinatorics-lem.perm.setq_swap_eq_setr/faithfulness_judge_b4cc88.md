## TARGET Equiv.Perm.setQ_swap_eq_setR (theorem) — ELABORATED SIGNATURE
∀ {n : ℕ} (σ : Equiv.Perm (Fin n)) (i j : Fin n), (σ * Equiv.swap i j).setQ i j = σ.setR i j

Docstring: Key symmetry: Q for σ * swap i j equals R for σ (when σ(i) < σ(j)).
This allows us to reduce the case σ(i) < σ(j) to the case σ(i) > σ(j). 

## PROJECT DEPENDENCY Equiv.Perm.setQ (def)
{n : ℕ} → Equiv.Perm (Fin n) → Fin n → Fin n → Finset (Fin n)

Body:
fun {n} σ i j => {k | i < k ∧ k < j ∧ σ j < σ k ∧ σ k < σ i}

Docstring: The set Q from Proposition prop.perm.lisitij:
Q = {k ∈ {i+1, ..., j-1} | σ(i) > σ(k) > σ(j)}
This counts elements between i and j whose images are strictly between σ(j) and σ(i). 

## PROJECT DEPENDENCY Equiv.Perm.setR (def)
{n : ℕ} → Equiv.Perm (Fin n) → Fin n → Fin n → Finset (Fin n)

Body:
fun {n} σ i j => {k | i < k ∧ k < j ∧ σ i < σ k ∧ σ k < σ j}

Docstring: The set R from Proposition prop.perm.lisitij:
R = {k ∈ {i+1, ..., j-1} | σ(i) < σ(k) < σ(j)}
This counts elements between i and j whose images are strictly between σ(i) and σ(j). 

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

## BASE-LIBRARY REF Finset
Type u_4 → Type u_4

Docstring: `Finset α` is the type of finite sets of elements of `α`. It is implemented
as a multiset (a list up to permutation) which has no duplicate elements. 

## BASE-LIBRARY REF HMul.hMul
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HMul α β γ] → α → β → γ

Docstring: `a * b` computes the product of `a` and `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `*` in identifiers is `mul`.

## BASE-LIBRARY REF instHMul
{α : Type u_1} → [Mul α] → HMul α α α

## BASE-LIBRARY REF Equiv.Perm.instMul
{α : Type u_4} → Mul (Equiv.Perm α)

## BASE-LIBRARY REF Equiv.swap
{α : Sort u_1} → [DecidableEq α] → α → α → Equiv.Perm α

Docstring: `swap a b` is the permutation that swaps `a` and `b` and
leaves other values as is. 

## BASE-LIBRARY REF instDecidableEqFin
(n : ℕ) → DecidableEq (Fin n)

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

## BASE-LIBRARY REF Fin.fintype
(n : ℕ) → Fintype (Fin n)

## INFORMAL STATEMENT
lem.perm.setQ_swap_eq_setR

\leanhelper  The set $Q$ for $\sigma \cdot t_{i,j}$ equals the set $R$ for $\sigma $. This key symmetry allows reducing the case $\sigma (i) < \sigma (j)$ to the case $\sigma (i) > \sigma (j)$ in the transposition length formula.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-conv-2eb59533
conv-2eb59533

In the Lean formalization, we use $\operatorname {Fin} n = \{ 0, 1, \ldots , n-1\} $ instead of the textbook’s $[n] = \{ 1, 2, \ldots , n\} $. Both are $n$-element sets, so their symmetric groups are isomorphic. Permutations are represented by the type of bijections $X \to X$ (denoted $\operatorname {Equiv.Perm}\,  X$ in Lean), which is a group under composition. Composition $\alpha \beta $ is the group multiplication $\alpha * \beta $, sending $x$ to $\alpha (\beta (x))$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.perm
def.perm.perm

Let $X$ be a set. 

\textbf{(a)} A \emph{permutation} of $X$ means a bijection from $X$ to $X$. 

\textbf{(b)} It is known that the set of all permutations of $X$ is a group under composition. This group is called the \emph{symmetric group} of $X$, and is denoted by $S_X$. Its neutral element is the identity map $\operatorname {id}_X : X \to X$. Its size is $|X|!$ when $X$ is finite. 

\textbf{(c)} As usual in group theory, we will write $\alpha \beta $ for the composition $\alpha \circ \beta $ when $\alpha , \beta \in S_X$. This is the map that sends each $x \in X$ to $\alpha (\beta (x))$. 

\textbf{(d)} If $\alpha \in S_X$ and $i \in \mathbb {Z}$, then $\alpha ^i$ shall denote the $i$-th power of $\alpha $ in the group $S_X$. Note that $\alpha ^i = \underbrace{\alpha \circ \alpha \circ \cdots \circ \alpha }_{i\text{ times}}$ if $i \ge 0$. Also, $\alpha ^0 = \operatorname {id}_X$. Also, $\alpha ^{-1}$ is the inverse of $\alpha $ in the group $S_X$, that is, the inverse of the map $\alpha $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.setq
def.perm.setQ

\leanhelper  The set $Q$ from Proposition~ \ref{prop.perm.lisitij}: $Q = \{ k \in \{ i+1, \ldots , j-1\}  \mid \sigma (j) < \sigma (k) < \sigma (i)\} $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.setr
def.perm.setR

\leanhelper  The set $R$ from Proposition~ \ref{prop.perm.lisitij}: $R = \{ k \in \{ i+1, \ldots , j-1\}  \mid \sigma (i) < \sigma (k) < \sigma (j)\} $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.tij
def.perm.tij

Let $i$ and $j$ be two distinct elements of a set $X$. 

Then, the \emph{transposition} $t_{i,j}$ is the permutation of $X$ that sends $i$ to $j$, sends $j$ to $i$, and leaves all other elements of $X$ unchanged.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The target states `\u2200 {n : \u2115} (\u03c3 : Equiv.Perm (Fin n)) (i j : Fin n), (\u03c3 * Equiv.swap i j).setQ i j = \u03c3.setR i j`, exactly matching \u201cThe set Q for \u03c3 \u00b7 t_{i,j} equals the set R for \u03c3.\u201d The multiplication convention also agrees: the informal definition says `\u03b1\u03b2` sends `x` to `\u03b1(\u03b2(x))`, so `\u03c3 * Equiv.swap i j` is \u03c3 after the transposition. The project bodies match the informal set definitions: `setQ` requires `i < k \u2227 k < j \u2227 \u03c3 j < \u03c3 k \u2227 \u03c3 k < \u03c3 i`, while `setR` requires `i < k \u2227 k < j \u2227 \u03c3 i < \u03c3 k \u2227 \u03c3 k < \u03c3 j`. Although the informal definition introduces `t_{i,j}` for distinct `i,j`, the Lean theorem quantifies over all `i j`; this is a strictly more general statement, not a weakening. Likewise, the theorem is unconditional rather than assuming `\u03c3(i) < \u03c3(j)`, so the parenthetical use case in the prose does not introduce a missing hypothesis."
}