## TARGET SymmetricFunctions.NPartition.rowPartition_size (theorem) — ELABORATED SIGNATURE
∀ (N n : ℕ) (hN : 0 < N), (SymmetricFunctions.NPartition.rowPartition N n hN).size = n

Docstring: The row partition has size n. 

## TARGET SymmetricFunctions.NPartition.colPartition_size (theorem) — ELABORATED SIGNATURE
∀ (N n : ℕ) (hn : n ≤ N), (SymmetricFunctions.NPartition.colPartition N n hn).size = n

Docstring: The column partition has size n. 

## PROJECT DEPENDENCY SymmetricFunctions.NPartition.size (def)
{N : ℕ} → SymmetricFunctions.NPartition N → ℕ

Body:
fun {N} lam => ∑ i, lam.parts i

Docstring: The size (sum of parts) of an N-partition 

## PROJECT DEPENDENCY SymmetricFunctions.NPartition.rowPartition (def)
(N : ℕ) → ℕ → 0 < N → SymmetricFunctions.NPartition N

Body:
fun N n _hN => { parts := fun i => if ↑i = 0 then n else 0, weaklyDecreasing := ⋯ }

Docstring: The row partition (n, 0, 0, ..., 0) with n boxes in the first row.
This is the partition corresponding to h_n (complete homogeneous symmetric polynomial).
Requires N > 0 to have at least one row. 

## PROJECT DEPENDENCY SymmetricFunctions.NPartition.colPartition (def)
(N n : ℕ) → n ≤ N → SymmetricFunctions.NPartition N

Body:
fun N n _hn => { parts := fun i => if ↑i < n then 1 else 0, weaklyDecreasing := ⋯ }

Docstring: The column partition (1, 1, ..., 1, 0, ..., 0) with n ones (n boxes in first column).
This is the partition corresponding to e_n (elementary symmetric polynomial).
Requires n ≤ N (can't have more rows than N). 

## PROJECT DEPENDENCY SymmetricFunctions.NPartition (inductive)
ℕ → Type

Body:
SymmetricFunctions.NPartition.mk : {N : ℕ} → (parts : Fin N → ℕ) → (∀ (i j : Fin N), i ≤ j → parts j ≤ parts i) → SymmetricFunctions.NPartition N

Docstring: An N-partition is a list of length N with weakly decreasing nonnegative entries.
This corresponds to Definition def.sf.N-par in the source.

**Note:** This is `SymmetricFunctions.NPartition`, a local definition.
A canonical top-level `NPartition` exists in `NPartition.lean` with the same
semantics (using `antitone` as the field name instead of `weaklyDecreasing`).
See the section docstring for details. 

## PROJECT DEPENDENCY SymmetricFunctions.NPartition.parts (def)
{N : ℕ} → SymmetricFunctions.NPartition N → Fin N → ℕ

Body:
fun N self => self.1

Docstring: The parts of the partition 

## PROJECT DEPENDENCY SymmetricFunctions.NPartition.mk (constructor)
{N : ℕ} → (parts : Fin N → ℕ) → (∀ (i j : Fin N), i ≤ j → parts j ≤ parts i) → SymmetricFunctions.NPartition N

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF LT.lt
{α : Type u} → [self : LT α] → α → α → Prop

Docstring: The less-than relation: `x < y` 

Conventions for notations in identifiers:

 * The recommended spelling of `<` in identifiers is `lt`.

## BASE-LIBRARY REF instLTNat
LT ℕ

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

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

## BASE-LIBRARY REF LE.le
{α : Type u} → [self : LE α] → α → α → Prop

Docstring: The less-equal relation: `x ≤ y` 

Conventions for notations in identifiers:

 * The recommended spelling of `≤` in identifiers is `le`.

 * The recommended spelling of `<=` in identifiers is `le` (prefer `≤` over `<=`).

## BASE-LIBRARY REF instLENat
LE ℕ

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

## BASE-LIBRARY REF ite
{α : Sort u} → (c : Prop) → [h : Decidable c] → α → α → α

Docstring: `if c then t else e` is notation for `ite c t e`, "if-then-else", which decides to
return `t` or `e` depending on whether `c` is true or false. The explicit argument
`c : Prop` does not have any actual computational content, but there is an additional
`[Decidable c]` argument synthesized by typeclass inference which actually
determines how to evaluate `c` to true or false. Write `if h : c then t else e`
instead for a "dependent if-then-else" `dite`, which allows `t`/`e` to use the fact
that `c` is true/false.


## BASE-LIBRARY REF Fin.val
{n : ℕ} → Fin n → ℕ

Docstring: The number that is strictly less than `n`.

`Fin.val` is a coercion, so any `Fin n` can be used in a position where a `Nat` is expected.


## BASE-LIBRARY REF instDecidableEqNat
DecidableEq ℕ

## BASE-LIBRARY REF Nat.decLt
(n m : ℕ) → Decidable (n < m)

Docstring: A decision procedure for strict inequality of natural numbers, usually accessed via the
`DecidableLT Nat` instance.

Examples:
 * `(if 3 < 4 then "yes" else "no") = "yes"`
 * `(if 4 < 4 then "yes" else "no") = "no"`
 * `(if 6 < 4 then "yes" else "no") = "no"`
 * `show 5 < 12 by decide`


## BASE-LIBRARY REF instLEFin
{n : ℕ} → LE (Fin n)

## INFORMAL STATEMENT
lem.sf.Npar-row-col

\leanhelper  The \emph{row partition} $(n, 0, \ldots , 0)$ has size $n$. The \emph{column partition} $(1, 1, \ldots , 1, 0, \ldots , 0)$ (with $n$ ones, $n \leq N$) has size $n$.

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.col-partition
def.sf.col-partition

\leanhelper  The \emph{column partition} $(1, 1, \ldots , 1, 0, \ldots , 0)$ with $n$ ones (i.e., $n$ boxes in the first column). This is the partition corresponding to $e_n$. Requires $n \leq N$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.ehp-through-m.onesthenzeros
def.sf.ehp-through-m.onesThenZeros

\leanhelper  The $N$-partition $(1, 1, \ldots , 1, 0, 0, \ldots , 0)$ with $n$ ones and $N - n$ zeros.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.hsymm-ext
def.sf.hsymm-ext

\leanhelper  The extended $h_n$: $h_n = 0$ for $n < 0$, $h_0 = 1$. This is needed since the Jacobi–Trudi formula may have negative indices.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.npar
def.sf.Npar

An $N$\emph{-partition} will mean a weakly decreasing $N$-tuple of nonnegative integers. In other words, an $N$-partition means an $N$-tuple $\left( \lambda _{1},\lambda _{2},\ldots ,\lambda _{N}\right) \in \mathbb {N}^{N}$ with $\lambda _{1}\geq \lambda _{2}\geq \cdots \geq \lambda _{N}$. 

The \emph{size} (or weight) of an $N$-partition $\lambda = (\lambda _1, \lambda _2, \ldots , \lambda _N)$ is defined to be $|\lambda | := \lambda _1 + \lambda _2 + \cdots + \lambda _N$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.npar-youngdiagram
def.sf.Npar-youngDiagram

\leanhelper  The \emph{Young diagram} $Y(\lambda )$ of an $N$-partition $\lambda $ is the finite set of cells 

\[  Y(\lambda ) = \{ (i, j) : i \in [N],\;  0 \leq j < \lambda _i\} .  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.row-partition
def.sf.row-partition

\leanhelper  The \emph{row partition} $(n, 0, 0, \ldots , 0)$ with $n$ boxes in the first row. This is the partition corresponding to $h_n$. Requires $N > 0$.

## VERDICT
{
  "verdict": "faithful",
  "justification": "Both declarations exactly match the two blueprint claims under the stated existence conditions. For rows, the formal binders `\u2200 (N n : \u2115) (hN : 0 < N)` agree with the informal definition\u2019s \u201cRequires `N > 0`,\u201d and `rowPartition` has parts `if \u2191i = 0 then n else 0`; its `size := \u2211 i, parts i` is therefore `n`, matching \u201cThe row partition `(n, 0, \u2026, 0)` has size `n`.\u201d For columns, the formal binders `\u2200 (N n : \u2115) (hn : n \u2264 N)` exactly match \u201cwith `n` ones, `n \u2264 N`,\u201d while `colPartition` has parts `if \u2191i < n then 1 else 0`; summing over `Fin N` gives `n`, matching the asserted size. The conditions `0 < N` and `n \u2264 N` are not added drift: they are explicitly required by the corresponding informal definitions and are needed for these `N`-partitions to have the described forms."
}