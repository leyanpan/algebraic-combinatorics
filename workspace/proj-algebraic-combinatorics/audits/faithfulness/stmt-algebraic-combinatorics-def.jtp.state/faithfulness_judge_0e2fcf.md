## TARGET AlgebraicCombinatorics.State (inductive) — ELABORATED SIGNATURE
Type

Body:
AlgebraicCombinatorics.State.mk : (levels : Set AlgebraicCombinatorics.Level) →
  {p | p ≥ 0 ∧ p ∈ levels}.Finite → {p | p < 0 ∧ p ∉ levels}.Finite → AlgebraicCombinatorics.State

Docstring: A "state" is a set of levels that contains all but finitely many negative levels
and only finitely many positive levels.

This is used in Borcherds' proof of Jacobi's triple product identity.

**Important convention**: A "level" in the tex source is a half-integer `p + 1/2` for some integer p.
We represent it by the integer p. Thus:
- "positive level" in the tex source means `p + 1/2 > 0`, i.e., `p ≥ 0` in our representation
- "negative level" in the tex source means `p + 1/2 < 0`, i.e., `p < 0` in our representation

The structure tracks:
- `finite_nonneg`: the set of nonnegative integers p (representing positive half-integer levels) in S
- `finite_negative_missing`: the set of negative integers p (representing negative half-integer levels) NOT in S 

## PROJECT DEPENDENCY AlgebraicCombinatorics.Level (def)
Type

Body:
ℤ

Docstring: A "level" is a half-integer, represented as p + 1/2 for some integer p.
We represent it simply by the integer p. 

## BASE-LIBRARY REF Set
Type u → Type u

Docstring: A set is a collection of elements of some type `α`.

Although `Set` is defined as `α → Prop`, this is an implementation detail which should not be
relied on. Instead, `setOf` and membership of a set (`∈`) should be used to convert between sets
and predicates.


## BASE-LIBRARY REF Set.Finite
{α : Type u} → Set α → Prop

Docstring: A set is finite if the corresponding `Subtype` is finite,
i.e., if there exists a natural `n : ℕ` and an equivalence `s ≃ Fin n`. 

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

## BASE-LIBRARY REF GE.ge
{α : Type u} → [LE α] → α → α → Prop

Docstring: `a ≥ b` is an abbreviation for `b ≤ a`. 

Conventions for notations in identifiers:

 * The recommended spelling of `≥` in identifiers is `ge`.

 * The recommended spelling of `>=` in identifiers is `ge` (prefer `≥` over `>=`).

## BASE-LIBRARY REF Int.instLEInt
LE ℤ

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNat
{n : ℕ} → OfNat ℤ n

## BASE-LIBRARY REF Membership.mem
{α : outParam (Type u)} → {γ : Type v} → [self : Membership α γ] → γ → α → Prop

Docstring: The membership relation `a ∈ s : Prop` where `a : α`, `s : γ`. 

Conventions for notations in identifiers:

 * The recommended spelling of `∈` in identifiers is `mem`.

## BASE-LIBRARY REF Set.instMembership
{α : Type u} → Membership α (Set α)

## BASE-LIBRARY REF LT.lt
{α : Type u} → [self : LT α] → α → α → Prop

Docstring: The less-than relation: `x < y` 

Conventions for notations in identifiers:

 * The recommended spelling of `<` in identifiers is `lt`.

## BASE-LIBRARY REF Int.instLTInt
LT ℤ

## BASE-LIBRARY REF Not
Prop → Prop

Docstring: `Not p`, or `¬p`, is the negation of `p`. It is defined to be `p → False`,
so if your goal is `¬p` you can use `intro h` to turn the goal into
`h : p ⊢ False`, and if you have `hn : ¬p` and `h : p` then `hn h : False`
and `(hn h).elim` will prove anything.
For more information: [Propositional Logic](https://lean-lang.org/theorem_proving_in_lean4/propositions_and_proofs.html#propositional-logic)


Conventions for notations in identifiers:

 * The recommended spelling of `¬` in identifiers is `not`.

## BASE-LIBRARY REF Int
Type

Docstring: The integers.

This type is special-cased by the compiler and overridden with an efficient implementation. The
runtime has a special representation for `Int` that stores “small” signed numbers directly, while
larger numbers use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)). A “small number” is an integer that can be encoded with one fewer bits
than the platform's pointer size (i.e. 63 bits on 64-bit architectures and 31 bits on 32-bit
architectures).


## INFORMAL STATEMENT
def.jtp.state

\leanhelper  A \emph{level} is a number of the form $p+\frac{1}{2}$ with $p\in \mathbb {Z}$. A \emph{state} is a set of levels that contains all but finitely many negative levels, and only finitely many positive levels. 

For any state $S$, we define: 

\begin{itemize} \item the \emph{energy} of $S$ to be 

\[  \operatorname {energy}S:=\sum _{\substack {p>0;\\ p\in S}}2p -\sum _{\substack {p<0;\\ p\notin S}}2p \in \mathbb {N};  \]

\item the \emph{particle number} of $S$ to be 

\[  \operatorname {parnum}S:=\left(\text{\#  of positive levels in } S\right) -\left(\text{\#  of negative levels not in } S\right)\in \mathbb {Z}.  \]

\end{itemize}

## VERDICT
{
  "verdict": "drift",
  "justification": "The `State` constructor faithfully captures the state condition: `levels : Set AlgebraicCombinatorics.Level`, `{p | p \u2265 0 \u2227 p \u2208 levels}.Finite`, and `{p | p < 0 \u2227 p \u2209 levels}.Finite` exactly encode, under `Level = \u2124` representing `p + 1/2`, \u201conly finitely many positive levels\u201d and \u201call but finitely many negative levels.\u201d However, the informal statement also says, \u201cFor any state S, we define\u201d both `energy S ... \u2208 \u2115` and `parnum S ... \u2208 \u2124`. The target body contains only `State.mk` and provides neither definition. Thus it formalizes only the first part of the blueprint. To make the whole statement faithful, retain this `State` declaration and add definitions `energy : State \u2192 \u2115` and `parnum : State \u2192 \u2124` implementing the displayed sums and cardinality difference, with the half-integer representation accounted for."
}