## TARGET AlgebraicCombinatorics.InclusionExclusion.card_Derangement_eq (theorem) — ELABORATED SIGNATURE
∀ (n : ℕ), Fintype.card (AlgebraicCombinatorics.InclusionExclusion.Derangement (Fin n)) = numDerangements n

Docstring: The cardinality of `Derangement (Fin n)` equals Mathlib's `numDerangements n`. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.InclusionExclusion.Derangement (def)
Type u_1 → Type (max 0 u_1)

Body:
fun α => { σ // ∀ (x : α), σ x ≠ x }

Docstring: **Definition `def.pie.dera`**: A derangement of a type `α` is a permutation with no fixed points.

This is definitionally equal to `↥(derangements α)` from `Mathlib.Combinatorics.Derangements.Basic`.

**Textbook definition:** "A derangement of a set X means a permutation of X that has no fixed points."

**Examples from the textbook:**
- D₀ = 1: The identity on ∅ is a derangement (vacuously no fixed points)
- D₁ = 0: The identity on {0} fixes 0, so it's not a derangement
- D₂ = 1: Only the swap (0 1) is a derangement
- D₃ = 2: The two 3-cycles (0 1 2) and (0 2 1) are derangements 

## PROJECT DEPENDENCY AlgebraicCombinatorics.InclusionExclusion.instFintypeDerangementOfDecidableEq (def)
{α : Type u_1} → [DecidableEq α] → [Fintype α] → Fintype (AlgebraicCombinatorics.InclusionExclusion.Derangement α)

Body:
fun {α} [DecidableEq α] [Fintype α] => Subtype.fintype fun σ => ∀ (x : α), σ x ≠ x

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


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

## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


## BASE-LIBRARY REF instDecidableEqFin
(n : ℕ) → DecidableEq (Fin n)

## BASE-LIBRARY REF Fin.fintype
(n : ℕ) → Fintype (Fin n)

## BASE-LIBRARY REF numDerangements
ℕ → ℕ

Docstring: The number of derangements of an `n`-element set. 

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

## BASE-LIBRARY REF Equiv.Perm
Sort u_1 → Sort (max 1 u_1)

Docstring: `Perm α` is the type of bijections from `α` to itself. 

## BASE-LIBRARY REF Ne
{α : Sort u} → α → α → Prop

Docstring: `a ≠ b`, or `Ne a b` is defined as `¬ (a = b)` or `a = b → False`,
and asserts that `a` and `b` are not equal.


Conventions for notations in identifiers:

 * The recommended spelling of `≠` in identifiers is `ne`.

## BASE-LIBRARY REF DFunLike.coe
{F : Sort u_1} → {α : outParam (Sort u_2)} → {β : outParam (α → Sort u_3)} → [self : DFunLike F α β] → F → (a : α) → β a

Docstring: The coercion from `F` to a function. 

## BASE-LIBRARY REF EquivLike.toFunLike
{E : Sort u_1} → {α : Sort u_3} → {β : Sort u_4} → [EquivLike E α β] → FunLike E α β

## BASE-LIBRARY REF Equiv.instEquivLike
{α : Sort u} → {β : Sort v} → EquivLike (α ≃ β) α β

## BASE-LIBRARY REF DecidableEq
Sort u → Sort (max 1 u)

Docstring: Propositional equality is `Decidable` for all elements of a type.

In other words, an instance of `DecidableEq α` is a means of deciding the proposition `a = b` is
for all `a b : α`.


## BASE-LIBRARY REF Fintype
Type u_4 → Type u_4

Docstring: `Fintype α` means that `α` is finite, i.e. there are only
finitely many distinct elements of type `α`. The evidence of this
is a finset `elems` (a list up to permutation without duplicates),
together with a proof that everything of type `α` is in the list. 

## BASE-LIBRARY REF Subtype.fintype
{α : Type u_1} → (p : α → Prop) → [DecidablePred p] → [Fintype α] → Fintype { x // p x }

## BASE-LIBRARY REF Fintype.decidableForallFintype
{α : Type u_1} → {p : α → Prop} → [DecidablePred p] → [Fintype α] → Decidable (∀ (a : α), p a)

## BASE-LIBRARY REF instDecidableNot
{p : Prop} → [dp : Decidable p] → Decidable ¬p

## BASE-LIBRARY REF Equiv.instFintype
{α : Type u_1} → {β : Type u_2} → [DecidableEq α] → [DecidableEq β] → [Fintype α] → [Fintype β] → Fintype (α ≃ β)

## INFORMAL STATEMENT
Derangement type matches Mathlib

\leanhelper  The number of derangements of $[n]$ (as defined in Definition~ \ref{def.pie.dera}) agrees with Mathlib’s derangement count.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.perm
def.perm.perm

Let $X$ be a set. 

\textbf{(a)} A \emph{permutation} of $X$ means a bijection from $X$ to $X$. 

\textbf{(b)} It is known that the set of all permutations of $X$ is a group under composition. This group is called the \emph{symmetric group} of $X$, and is denoted by $S_X$. Its neutral element is the identity map $\operatorname {id}_X : X \to X$. Its size is $|X|!$ when $X$ is finite. 

\textbf{(c)} As usual in group theory, we will write $\alpha \beta $ for the composition $\alpha \circ \beta $ when $\alpha , \beta \in S_X$. This is the map that sends each $x \in X$ to $\alpha (\beta (x))$. 

\textbf{(d)} If $\alpha \in S_X$ and $i \in \mathbb {Z}$, then $\alpha ^i$ shall denote the $i$-th power of $\alpha $ in the group $S_X$. Note that $\alpha ^i = \underbrace{\alpha \circ \alpha \circ \cdots \circ \alpha }_{i\text{ times}}$ if $i \ge 0$. Also, $\alpha ^0 = \operatorname {id}_X$. Also, $\alpha ^{-1}$ is the inverse of $\alpha $ in the group $S_X$, that is, the inverse of the map $\alpha $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.pie.dera
def.pie.dera

A \emph{derangement} of a set $X$ means a permutation of $X$ that has no fixed points.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The blueprint says: \u201cThe number of derangements of $[n]$ \u2026 agrees with Mathlib\u2019s derangement count.\u201d The target states for every natural number, `\u2200 (n : \u2115), Fintype.card (Derangement (Fin n)) = numDerangements n`. Here `Fin n` is the canonical type of natural numbers below `n`, hence the formal realization of `[n]`; `Fintype.card` gives the number of elements; and `numDerangements n` is documented as \u201cThe number of derangements of an `n`-element set.\u201d Moreover, the dependency defines `Derangement \u03b1` as `{ \u03c3 // \u2200 (x : \u03b1), \u03c3 x \u2260 x }`, with `\u03c3` a permutation, exactly matching the informal definition \u201ca permutation of $X$ that has no fixed points.\u201d The only required `DecidableEq` and `Fintype` instances are automatically available for `Fin n` and merely encode finitary cardinality computation; they add no mathematical restriction."
}