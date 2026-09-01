## TARGET SymmetricFunctions.NPartition.IsTranspose.box_equiv (theorem) — ELABORATED SIGNATURE
∀ {N M : ℕ} {lam : Fin N → ℕ} {lamt : Fin M → ℕ},
  (∀ (i j : Fin N), i ≤ j → lam j ≤ lam i) →
    (∀ (i j : Fin M), i ≤ j → lamt j ≤ lamt i) →
      SymmetricFunctions.NPartition.IsTranspose lam lamt → ∀ (i : Fin N) (j : Fin M), ↑j + 1 ≤ lam i ↔ ↑i + 1 ≤ lamt j

Docstring: The transpose box equivalence: for weakly decreasing partitions λ and λᵗ
satisfying the transpose property, box (i, j) is in λ iff (j, i) is in λᵗ.

This is the key lemma that relates the two counting conditions:
j + 1 ≤ λ_i ↔ i + 1 ≤ λᵗ_j

The proof uses the weakly decreasing property: if j + 1 ≤ λ_i, then all
rows 0, 1, ..., i have at least j + 1 boxes, so λᵗ_j ≥ i + 1. 

## PROJECT DEPENDENCY SymmetricFunctions.NPartition.IsTranspose (def)
{N M : ℕ} → (Fin N → ℕ) → (Fin M → ℕ) → Prop

Body:
fun {N M} lam lamt =>
  (∀ (i : Fin M), lamt i = {j | ↑i + 1 ≤ lam j}.card) ∧ ∀ (j : Fin N), lam j = {i | ↑j + 1 ≤ lamt i}.card

Docstring: Predicate asserting that `lamt` is the transpose of `lam`.
The transpose λᵗ of a partition λ satisfies:
(λᵗ)ᵢ = |{j : λⱼ ≥ i}| for each i.

Since we work with fixed-length tuples, this predicate captures
when two tuples represent transpose partitions (possibly with trailing zeros). 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


## BASE-LIBRARY REF LE.le
{α : Type u} → [self : LE α] → α → α → Prop

Docstring: The less-equal relation: `x ≤ y` 

Conventions for notations in identifiers:

 * The recommended spelling of `≤` in identifiers is `le`.

 * The recommended spelling of `<=` in identifiers is `le` (prefer `≤` over `<=`).

## BASE-LIBRARY REF instLEFin
{n : ℕ} → LE (Fin n)

## BASE-LIBRARY REF instLENat
LE ℕ

## BASE-LIBRARY REF Iff
Prop → Prop → Prop

Docstring: If and only if, or logical bi-implication. `a ↔ b` means that `a` implies `b` and vice versa.
By `propext`, this implies that `a` and `b` are equal and hence any expression involving `a`
is equivalent to the corresponding expression with `b` instead.


Conventions for notations in identifiers:

 * The recommended spelling of `↔` in identifiers is `iff`.

 * The recommended spelling of `<->` in identifiers is `iff` (prefer `↔` over `<->`).

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


## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

## BASE-LIBRARY REF And
Prop → Prop → Prop

Docstring: `And a b`, or `a ∧ b`, is the conjunction of propositions. It can be
constructed and destructed like a pair: if `ha : a` and `hb : b` then
`⟨ha, hb⟩ : a ∧ b`, and if `h : a ∧ b` then `h.left : a` and `h.right : b`.


Conventions for notations in identifiers:

 * The recommended spelling of `∧` in identifiers is `and`.

 * The recommended spelling of `/\` in identifiers is `and` (prefer `∧` over `/\`).

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

## BASE-LIBRARY REF Finset.filter
{α : Type u_1} → (p : α → Prop) → [DecidablePred p] → Finset α → Finset α

Docstring: `Finset.filter p s` is the set of elements of `s` that satisfy `p`.

For example, one can use `s.filter (· ∈ t)` to get the intersection of `s` with `t : Set α`
as a `Finset α` (when a `DecidablePred (· ∈ t)` instance is available). 

## BASE-LIBRARY REF Nat.decLe
(n m : ℕ) → Decidable (n ≤ m)

Docstring: A decision procedure for non-strict inequality of natural numbers, usually accessed via the
`DecidableLE Nat` instance.

Examples:
 * `(if 3 ≤ 4 then "yes" else "no") = "yes"`
 * `(if 6 ≤ 4 then "yes" else "no") = "no"`
 * `show 12 ≤ 12 by decide`
 * `show 5 ≤ 12 by decide`


## BASE-LIBRARY REF Finset.univ
{α : Type u_1} → [Fintype α] → Finset α

Docstring: `univ` is the universal finite set of type `Finset α` implied from
the assumption `Fintype α`. 

## BASE-LIBRARY REF Fin.fintype
(n : ℕ) → Fintype (Fin n)

## INFORMAL STATEMENT
lem.sf.transpose-box-equiv

\leanhelper  If $\lambda $ and $\lambda ^t$ are transposes, then there is a bijection between the boxes of the Young diagram of $\lambda $ (pairs $(i,j)$ with $j < \lambda _i$) and those of $\lambda ^t$ (pairs $(j,i)$ with $i < \lambda ^t_j$), given by swapping coordinates.

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.is-transpose
def.sf.is-transpose

\leanhelper  Two functions $\lambda : \mathrm{Fin}\, N \to \mathbb {N}$ and $\lambda ^t : \mathrm{Fin}\, M \to \mathbb {N}$ are \emph{transposes} of each other if for all $i < N$ and $j < M$: 

\[  \lambda _i > j \iff \lambda ^t_j > i.  \]

 This is the symmetric characterization of the transpose relation between Young diagrams.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.npar
def.sf.Npar

An $N$\emph{-partition} will mean a weakly decreasing $N$-tuple of nonnegative integers. In other words, an $N$-partition means an $N$-tuple $\left( \lambda _{1},\lambda _{2},\ldots ,\lambda _{N}\right) \in \mathbb {N}^{N}$ with $\lambda _{1}\geq \lambda _{2}\geq \cdots \geq \lambda _{N}$. 

The \emph{size} (or weight) of an $N$-partition $\lambda = (\lambda _1, \lambda _2, \ldots , \lambda _N)$ is defined to be $|\lambda | := \lambda _1 + \lambda _2 + \cdots + \lambda _N$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.npar-youngdiagram
def.sf.Npar-youngDiagram

\leanhelper  The \emph{Young diagram} $Y(\lambda )$ of an $N$-partition $\lambda $ is the finite set of cells 

\[  Y(\lambda ) = \{ (i, j) : i \in [N],\;  0 \leq j < \lambda _i\} .  \]

## VERDICT
{
  "verdict": "drift",
  "justification": "The blueprint fixes \u201ctransposes\u201d by the pointwise condition \u201cfor all i < N and j < M: \u03bb_i > j \u2194 \u03bb\u1d57_j > i.\u201d The target instead assumes `SymmetricFunctions.NPartition.IsTranspose lam lamt`, whose body is the stronger pair of exact cardinality equations `lamt i = {j | \u2191i + 1 \u2264 lam j}.card` and `lam j = {i | \u2191j + 1 \u2264 lamt i}.card`. These equations impose truncation/boundedness not present in the informal definition. For example, with `N = M = 1` and both sole entries equal to `2`, the informal pointwise transpose condition holds, but the project predicate fails because the relevant cardinality is only `1`. Thus the target covers fewer pairs than the blueprint. The difference enters through the body of `SymmetricFunctions.NPartition.IsTranspose`, rather than through the target conclusion. The conclusion `\u2200 i j, \u2191j + 1 \u2264 lam i \u2194 \u2191i + 1 \u2264 lamt j` faithfully expresses the box correspondence on the bounded indices, and coordinate swapping then gives the stated bijection. To make the declaration faithful, redefine or replace `IsTranspose` with the blueprint\u2019s pointwise equivalence (or add the missing bounds explicitly to the informal definition). The weak-decreasing binders encode that `lam` and `lamt` are partitions, but they do not repair the stronger transpose predicate."
}