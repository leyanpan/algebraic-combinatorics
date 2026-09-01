## TARGET AlgebraicCombinatorics.InclusionExclusion.Derangement.equivDerangements (def) — ELABORATED SIGNATURE
(α : Type u_1) → AlgebraicCombinatorics.InclusionExclusion.Derangement α ≃ ↑(derangements α)

Body:
fun α => { toFun := fun σ => ⟨↑σ, ⋯⟩, invFun := fun σ => ⟨↑σ, ⋯⟩, left_inv := ⋯, right_inv := ⋯ }

Docstring: The `Derangement` type is equivalent to the subtype of `derangements α`.
This establishes that our explicit type is equivalent to Mathlib's set-based definition. 

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

## PROJECT DEPENDENCY AlgebraicCombinatorics.InclusionExclusion.Derangement.mem_derangements (theorem)
∀ {α : Type u_1} (σ : AlgebraicCombinatorics.InclusionExclusion.Derangement α), ↑σ ∈ derangements α

Docstring: A derangement is a permutation in `derangements α`.
This shows our definition matches Mathlib's `derangements` set. 

## BASE-LIBRARY REF Equiv
Sort u_1 → Sort u_2 → Sort (max (max 1 u_1) u_2)

Docstring: `α ≃ β` is the type of functions from `α → β` with a two-sided inverse. 

## BASE-LIBRARY REF Set.Elem
{α : Type u} → Set α → Type u

Docstring: Given the set `s`, `Elem s` is the `Type` of element of `s`.

It is currently an abbreviation so that instance coming from `Subtype` are available.
If you're interested in making it a `def`, as it probably should be,
you'll then need to create additional instances (and possibly prove lemmas about them).
See e.g. `Mathlib/Data/Set/Order.lean`.


## BASE-LIBRARY REF Equiv.Perm
Sort u_1 → Sort (max 1 u_1)

Docstring: `Perm α` is the type of bijections from `α` to itself. 

## BASE-LIBRARY REF derangements
(α : Type u_1) → Set (Equiv.Perm α)

Docstring: A permutation is a derangement if it has no fixed points. 

## BASE-LIBRARY REF Equiv.mk
{α : Sort u_1} →
  {β : Sort u_2} →
    (toFun : α → β) →
      (invFun : β → α) →
        autoParam (Function.LeftInverse invFun toFun) Equiv.left_inv._autoParam →
          autoParam (Function.RightInverse invFun toFun) Equiv.right_inv._autoParam → α ≃ β

## BASE-LIBRARY REF Subtype.mk
{α : Sort u} → {p : α → Prop} → (val : α) → p val → Subtype p

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

## BASE-LIBRARY REF Subtype.val
{α : Sort u} → {p : α → Prop} → Subtype p → α

Docstring: The value in the underlying type that satisfies the predicate.


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

## INFORMAL STATEMENT
Equivalence to Mathlib’s derangements

\leanhelper  The set of derangements of $\alpha $ (as defined in Definition~ \ref{def.pie.dera}) is in bijection with the set of fixed-point-free permutations from Mathlib.

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
  "justification": "The target gives, for every type `\u03b1`, an equivalence `AlgebraicCombinatorics.InclusionExclusion.Derangement \u03b1 \u2243 \u2191(derangements \u03b1)`. By the project definition, the left side is `{ \u03c3 // \u2200 (x : \u03b1), \u03c3 x \u2260 x }`, namely permutations of `\u03b1` with no fixed points. By the base-library docstring, `derangements \u03b1` is the set of permutations with no fixed points, and `\u2191(derangements \u03b1)` is its subtype of elements. Since `\u03b1 \u2243 \u03b2` is a function with a two-sided inverse, this is exactly the claimed bijection between the derangements defined in Definition `def.pie.dera` and Mathlib\u2019s fixed-point-free permutations. There are no added hypotheses or restricted quantifiers."
}