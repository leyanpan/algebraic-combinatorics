## TARGET AlgebraicCombinatorics.contentTableau_eq_of_iff (theorem) — ELABORATED SIGNATURE
∀ {N : ℕ} {lam mu : Fin N → ℕ} (T T' : AlgebraicCombinatorics.Tableau lam mu) (i : Fin N),
  (∀ (c : { c // c ∈ AlgebraicCombinatorics.skewYoungDiagram lam mu }), T' c = i ↔ T c = i) →
    AlgebraicCombinatorics.contentTableau T' i = AlgebraicCombinatorics.contentTableau T i

Docstring: If two tableaux have the same cells with value i (i.e., T' c = i ↔ T c = i for all c),
then they have the same content at i. This is useful for proving that transformations
that don't affect certain values preserve the content at those values. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.Tableau (def)
{N : ℕ} → (Fin N → ℕ) → (Fin N → ℕ) → Type

Body:
fun {N} lam mu => { c // c ∈ AlgebraicCombinatorics.skewYoungDiagram lam mu } → Fin N

Docstring: A tableau of shape lam/mu is a function from cells to [N]. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.skewYoungDiagram (def)
{N : ℕ} → (Fin N → ℕ) → (Fin N → ℕ) → Set (Fin N × ℕ)

Body:
fun {N} lam mu => {c | mu c.1 < c.2 ∧ c.2 ≤ lam c.1}

Docstring: The skew Young diagram Y(lam/mu) as a set of cells.
A cell (i,j) is in Y(lam/mu) if mu_i < j ≤ lam_i.

**This is the `Set` version with 1-indexed columns (textbook convention).**
The first column is j = 1, not j = 0.

For the canonical `Finset` version with 0-indexed columns, see:
- `NPartition.skewYoungDiagram` in NPartition.lean (canonical, no `[NeZero N]` required)
- `skewYoungDiagram` in SchurBasics.lean (duplicate, requires `[NeZero N]`)

Comparison:
- Here: (i, j) ∈ Y(λ/μ) iff μ_i < j ≤ λ_i (1-indexed)
- NPartition/SchurBasics: (i, j) ∈ Y(λ/μ) iff μ_i ≤ j < λ_i (0-indexed)

The bijection between them is: (i, j) here ↔ (i, j-1) in NPartition/SchurBasics.
See `SchurBasics.mem_skewYoungDiagram_iff_mem_LR_shifted` for the conversion lemma. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.contentTableau (def)
{N : ℕ} → {lam mu : Fin N → ℕ} → AlgebraicCombinatorics.Tableau lam mu → Fin N → ℕ

Body:
fun {N} {lam mu} T i => Nat.card { c // T c = i }

Docstring: **Definition (def.sf.content)**: The content of a tableau T is the N-tuple counting
occurrences of each value.

For a tableau T of shape λ/μ, we define the content of T to be the N-tuple
(a₁, a₂, ..., a_N), where aᵢ = (# of i's in T) = (# of boxes c of T such that T(c) = i).

We denote this N-tuple by cont(T).

**Example**: If N=5, then cont([[1,1,2],[4]]) = (2,1,0,1,0).

**Key property** (eq.def.sf.content.xT=): x_T = x^(cont(T)) for any tableau T.
(Both sides equal ∏ᵢ xᵢ^(# of i's in T).) 

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

## BASE-LIBRARY REF Prod
Type u → Type v → Type (max u v)

Docstring: The product type, usually written `α × β`. Product types are also called pair or tuple types.
Elements of this type are pairs in which the first element is an `α` and the second element is a
`β`.

Products nest to the right, so `(x, y, z) : α × β × γ` is equivalent to `(x, (y, z)) : α × (β × γ)`.


Conventions for notations in identifiers:

 * The recommended spelling of `×` in identifiers is `Prod`.

## BASE-LIBRARY REF Membership.mem
{α : outParam (Type u)} → {γ : Type v} → [self : Membership α γ] → γ → α → Prop

Docstring: The membership relation `a ∈ s : Prop` where `a : α`, `s : γ`. 

Conventions for notations in identifiers:

 * The recommended spelling of `∈` in identifiers is `mem`.

## BASE-LIBRARY REF Set
Type u → Type u

Docstring: A set is a collection of elements of some type `α`.

Although `Set` is defined as `α → Prop`, this is an implementation detail which should not be
relied on. Instead, `setOf` and membership of a set (`∈`) should be used to convert between sets
and predicates.


## BASE-LIBRARY REF Set.instMembership
{α : Type u} → Membership α (Set α)

## BASE-LIBRARY REF Iff
Prop → Prop → Prop

Docstring: If and only if, or logical bi-implication. `a ↔ b` means that `a` implies `b` and vice versa.
By `propext`, this implies that `a` and `b` are equal and hence any expression involving `a`
is equivalent to the corresponding expression with `b` instead.


Conventions for notations in identifiers:

 * The recommended spelling of `↔` in identifiers is `iff`.

 * The recommended spelling of `<->` in identifiers is `iff` (prefer `↔` over `<->`).

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

## BASE-LIBRARY REF setOf
{α : Type u} → (α → Prop) → Set α

Docstring: Turn a predicate `p : α → Prop` into a set, also written as `{x | p x}` 

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

## BASE-LIBRARY REF instLTNat
LT ℕ

## BASE-LIBRARY REF Prod.fst
{α : Type u} → {β : Type v} → α × β → α

Docstring: The first element of a pair. 

## BASE-LIBRARY REF Prod.snd
{α : Type u} → {β : Type v} → α × β → β

Docstring: The second element of a pair. 

## BASE-LIBRARY REF LE.le
{α : Type u} → [self : LE α] → α → α → Prop

Docstring: The less-equal relation: `x ≤ y` 

Conventions for notations in identifiers:

 * The recommended spelling of `≤` in identifiers is `le`.

 * The recommended spelling of `<=` in identifiers is `le` (prefer `≤` over `<=`).

## BASE-LIBRARY REF instLENat
LE ℕ

## BASE-LIBRARY REF Nat.card
Type u_3 → ℕ

Docstring: `Nat.card α` is the cardinality of `α` as a natural number.
If `α` is infinite, `Nat.card α = 0`. 

## INFORMAL STATEMENT
Content equality from pointwise characterization

\leanhelper  If two tableaux $T, T'$ of the same shape satisfy $T'(c) = i \iff T(c) = i$ for all cells $c$, then $\operatorname {cont}(T')_i = \operatorname {cont}(T)_i$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.content
def.sf.content

Let $\lambda $ and $\mu $ be two $N$-partitions. Let $T$ be a tableau of shape $\lambda /\mu $. We define the \emph{content} of $T$ to be the $N$-tuple $\left( a_{1},a_{2},\ldots ,a_{N}\right) $, where

\[  a_{i}:=\left( \text{\#  of }i\text{'s in }T\right) =\left( \text{\#  of boxes }c\text{ of }T\text{ such that }T\left( c\right) =i\right) .  \]

 We denote this $N$-tuple by $\operatorname *{cont}T$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.sf.skew-tab
def.sf.skew-tab

Let $\lambda $ and $\mu $ be two $N$-partitions such that $\mu \subseteq \lambda $. A \emph{Young tableau} of shape $\lambda /\mu $ means a way of filling the boxes of $Y\left( \lambda /\mu \right) $ with elements of $\left[ N\right] $ (one element per box). Formally speaking, it is defined as a map $T:Y\left( \lambda /\mu \right) \rightarrow \left[ N\right] $. 

Young tableaux of shape $\lambda /\mu $ are often called \emph{skew Young tableaux}. 

If we don’t have $\mu \subseteq \lambda $, then we agree that there are no Young tableaux of shape $\lambda /\mu $.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The formal hypothesis exactly matches the blueprint: `\u2200 (c : { c // c \u2208 skewYoungDiagram lam mu }), T' c = i \u2194 T c = i` quantifies over every cell of the common shape and asserts the same pointwise characterization of the cells containing `i`. By definition, `contentTableau T i = Nat.card { c // T c = i }`, so the hypothesis identifies precisely the two fiber types whose cardinalities form the stated content entries, yielding `contentTableau T' i = contentTableau T i`. The formal binders `lam mu : Fin N \u2192 \u2115` do not require them to be N-partitions or require `\u03bc \u2286 \u03bb`; this makes the theorem more general than the blueprint rather than weaker, since it still includes the blueprint\u2019s partition-shaped cases. Likewise, representing `[N]` by `Fin N` is an index encoding, not a mathematically contentful restriction."
}