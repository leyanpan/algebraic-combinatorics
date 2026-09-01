## TARGET AlgebraicCombinatorics.InclusionExclusion.factorial_dvd_numSurj (theorem) — ELABORATED SIGNATURE
∀ (m n : ℕ), n.factorial ∣ AlgebraicCombinatorics.InclusionExclusion.numSurj m n

Docstring: `n!` divides `numSurj m n` because the action of `Perm (Fin n)` on surjective maps
is free, so each orbit has size `n!`. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.InclusionExclusion.numSurj (def)
ℕ → ℕ → ℕ

Body:
fun m n => Fintype.card { f // Function.Surjective f }

Docstring: The number of surjective maps from `Fin m` to `Fin n`. 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF Dvd.dvd
{α : Type u_1} → [self : Dvd α] → α → α → Prop

Docstring: Divisibility. `a ∣ b` (typed as `\|`) means that there is some `c` such that `b = a * c`. 

Conventions for notations in identifiers:

 * The recommended spelling of `∣` in identifiers is `dvd`.

## BASE-LIBRARY REF Nat.instDvd
Dvd ℕ

Docstring: Divisibility of natural numbers. `a ∣ b` (typed as `\|`) says that
there is some `c` such that `b = a * c`.


## BASE-LIBRARY REF Nat.factorial
ℕ → ℕ

Docstring: `Nat.factorial n` is the factorial of `n`. 

## BASE-LIBRARY REF Fintype.card
(α : Type u_4) → [Fintype α] → ℕ

Docstring: `card α` is the number of elements in `α`, defined when `α` is a fintype. 

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

## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


## BASE-LIBRARY REF Function.Surjective
{α : Sort u_1} → {β : Sort u_2} → (α → β) → Prop

Docstring: A function `f : α → β` is called surjective if every `b : β` is equal to `f a`
for some `a : α`. 

## BASE-LIBRARY REF Subtype.fintype
{α : Type u_1} → (p : α → Prop) → [DecidablePred p] → [Fintype α] → Fintype { x // p x }

## BASE-LIBRARY REF Fintype.decidableSurjectiveFintype
{α : Type u_1} → {β : Type u_2} → [DecidableEq β] → [Fintype α] → [Fintype β] → DecidablePred Function.Surjective

## BASE-LIBRARY REF instDecidableEqFin
(n : ℕ) → DecidableEq (Fin n)

## BASE-LIBRARY REF Fin.fintype
(n : ℕ) → Fintype (Fin n)

## BASE-LIBRARY REF Pi.instFintype
{α : Type u_3} →
  {β : α → Type u_4} → [DecidableEq α] → [Fintype α] → [(a : α) → Fintype (β a)] → Fintype ((a : α) → β a)

Docstring: A dependent product of fintypes, indexed by a fintype, is a fintype. 

## INFORMAL STATEMENT
Factorial divides number of surjections

\leanhelper  We have $n! \mid \mathrm{numSurj}(m, n)$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.perm
def.perm.perm

Let $X$ be a set. 

\textbf{(a)} A \emph{permutation} of $X$ means a bijection from $X$ to $X$. 

\textbf{(b)} It is known that the set of all permutations of $X$ is a group under composition. This group is called the \emph{symmetric group} of $X$, and is denoted by $S_X$. Its neutral element is the identity map $\operatorname {id}_X : X \to X$. Its size is $|X|!$ when $X$ is finite. 

\textbf{(c)} As usual in group theory, we will write $\alpha \beta $ for the composition $\alpha \circ \beta $ when $\alpha , \beta \in S_X$. This is the map that sends each $x \in X$ to $\alpha (\beta (x))$. 

\textbf{(d)} If $\alpha \in S_X$ and $i \in \mathbb {Z}$, then $\alpha ^i$ shall denote the $i$-th power of $\alpha $ in the group $S_X$. Note that $\alpha ^i = \underbrace{\alpha \circ \alpha \circ \cdots \circ \alpha }_{i\text{ times}}$ if $i \ge 0$. Also, $\alpha ^0 = \operatorname {id}_X$. Also, $\alpha ^{-1}$ is the inverse of $\alpha $ in the group $S_X$, that is, the inverse of the map $\alpha $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.sn-iven
def.perm.Sn-iven

Let $n \in \mathbb {Z}$. Then, $[n]$ shall mean the set $\{ 1, 2, \ldots , n\} $. This is an $n$-element set if $n \ge 0$, and is an empty set if $n \le 0$. 

The symmetric group $S_{[n]}$ (consisting of all permutations of $[n]$) will be denoted $S_n$ and called the $n$\emph{-th symmetric group}. Its size is $n!$ (when $n \ge 0$).

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.pie.numsurj
Number of surjections

\leanhelper  The \emph{number of surjective maps} from $[m]$ to $[n]$ is defined as 

\[  \mathrm{numSurj}(m, n) := \# \{ f\colon [m] \to [n] \mid f \text{ is surjective}\} .  \]

## VERDICT
{
  "verdict": "drift",
  "justification": "The target quantifies only over naturals: `\u2200 (m n : \u2115), ...`, and the project dependency likewise fixes `numSurj : \u2115 \u2192 \u2115 \u2192 \u2115`. By contrast, the blueprint defines `[n]` for `n \u2208 \u2124`, explicitly including nonpositive indices, and defines `numSurj(m,n)` using `[m]` and `[n]`. Although `n!` naturally restricts the meaningful claim to nonnegative `n`, nothing similarly restricts `m`; negative `m` denotes the empty set under the supplied definition. Thus the Lean binder `m : \u2115` narrows the blueprint's index range. To be faithful, the dependency should accept the blueprint\u2019s integer indices (interpreting `[k]` as empty for `k \u2264 0`), and the theorem should quantify over integer `m` and nonnegative `n` (or an equivalent encoding)."
}