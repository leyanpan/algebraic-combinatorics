## TARGET AlgebraicCombinatorics.Sn (def) — ELABORATED SIGNATURE
ℕ → Type

Body:
fun n => Equiv.Perm (Fin n)

Docstring: The n-th symmetric group `S_n` is the group of permutations of `[n]`.
    (def.perm.Sn-iven)

In the textbook, `S_n` is defined as `S_[n]`, the symmetric group of `[n] = {1, 2, ..., n}`.
In Lean, we represent this as `Equiv.Perm (Fin n)`, the group of permutations of
`Fin n = {0, 1, ..., n-1}`.

The size of `S_n` is `n!` (see `sn_card`). 

## TARGET AlgebraicCombinatorics.sn_card (theorem) — ELABORATED SIGNATURE
∀ (n : ℕ), Fintype.card (AlgebraicCombinatorics.Sn n) = n.factorial

Docstring: The symmetric group `S_n` has `n!` elements. (def.perm.Sn-iven)

This is the key cardinality result: `|S_n| = n!` 

## TARGET AlgebraicCombinatorics.bracketN (def) — ELABORATED SIGNATURE
ℕ → Type

Body:
fun n => Fin n

Docstring: The set `[n]` from the textbook is represented by `Fin n` in Lean.

In the textbook (def.perm.Sn-iven), `[n]` denotes `{1, 2, ..., n}`.
In Lean, `Fin n` represents `{0, 1, ..., n-1}`.

Both are n-element sets for n ≥ 0, so their symmetric groups are isomorphic.
We use `Fin n` as it is the standard representation in Mathlib. 

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

## BASE-LIBRARY REF Fintype.card
(α : Type u_4) → [Fintype α] → ℕ

Docstring: `card α` is the number of elements in `α`, defined when `α` is a fintype. 

## BASE-LIBRARY REF Equiv.instFintype
{α : Type u_1} → {β : Type u_2} → [DecidableEq α] → [DecidableEq β] → [Fintype α] → [Fintype β] → Fintype (α ≃ β)

## BASE-LIBRARY REF instDecidableEqFin
(n : ℕ) → DecidableEq (Fin n)

## BASE-LIBRARY REF Fin.fintype
(n : ℕ) → Fintype (Fin n)

## BASE-LIBRARY REF Nat.factorial
ℕ → ℕ

Docstring: `Nat.factorial n` is the factorial of `n`. 

## INFORMAL STATEMENT
def.perm.Sn-iven

Let $n \in \mathbb {Z}$. Then, $[n]$ shall mean the set $\{ 1, 2, \ldots , n\} $. This is an $n$-element set if $n \ge 0$, and is an empty set if $n \le 0$. 

The symmetric group $S_{[n]}$ (consisting of all permutations of $[n]$) will be denoted $S_n$ and called the $n$\emph{-th symmetric group}. Its size is $n!$ (when $n \ge 0$).

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.perm
def.perm.perm

Let $X$ be a set. 

\textbf{(a)} A \emph{permutation} of $X$ means a bijection from $X$ to $X$. 

\textbf{(b)} It is known that the set of all permutations of $X$ is a group under composition. This group is called the \emph{symmetric group} of $X$, and is denoted by $S_X$. Its neutral element is the identity map $\operatorname {id}_X : X \to X$. Its size is $|X|!$ when $X$ is finite. 

\textbf{(c)} As usual in group theory, we will write $\alpha \beta $ for the composition $\alpha \circ \beta $ when $\alpha , \beta \in S_X$. This is the map that sends each $x \in X$ to $\alpha (\beta (x))$. 

\textbf{(d)} If $\alpha \in S_X$ and $i \in \mathbb {Z}$, then $\alpha ^i$ shall denote the $i$-th power of $\alpha $ in the group $S_X$. Note that $\alpha ^i = \underbrace{\alpha \circ \alpha \circ \cdots \circ \alpha }_{i\text{ times}}$ if $i \ge 0$. Also, $\alpha ^0 = \operatorname {id}_X$. Also, $\alpha ^{-1}$ is the inverse of $\alpha $ in the group $S_X$, that is, the inverse of the map $\alpha $.

## VERDICT
{
  "verdict": "drift",
  "justification": "The blueprint begins, \u201cLet $n \\in \\mathbb Z$,\u201d and defines $[n]$ for negative indices as well: it \u201cis an empty set if $n \\le 0$.\u201d By contrast, both defining declarations have the restricted binder `\u2115 \u2192 Type`: `bracketN` is `fun n => Fin n`, and `Sn` is `fun n => Equiv.Perm (Fin n)`. Thus they cannot even take a negative integer index, so the blueprint\u2019s definitions of `[n]` and `S_n` for `n < 0` are omitted. This is a mathematically contentful narrowing from integers to naturals, not merely an encoding detail. The shift from `{1,\u2026,n}` to `Fin n = {0,\u2026,n-1}` is otherwise a harmless finite-set representation, and `sn_card : \u2200 (n : \u2115), Fintype.card (Sn n) = n.factorial` faithfully covers the blueprint\u2019s cardinality claim \u201cwhen $n \\ge 0$.\u201d To make the package faithful, the index binder of `bracketN` and consequently `Sn` should range over integers, with `bracketN n` representing `{i \\in \\mathbb Z \\mid 1 \\le i \\land i \\le n}` (hence empty for negative `n`), while the cardinality theorem should quantify over integer `n` subject to `0 \u2264 n` and compare with the factorial of the corresponding natural number."
}