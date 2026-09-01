## TARGET AlgebraicCombinatorics.State.fromFinsetPair_energy (theorem) — ELABORATED SIGNATURE
∀ (P N : Finset ℕ),
  (AlgebraicCombinatorics.State.fromFinsetPair P N).energy = ∑ n ∈ P, (2 * n + 1) + ∑ n ∈ N, (2 * n + 1)

## PROJECT DEPENDENCY AlgebraicCombinatorics.State.energy (def)
AlgebraicCombinatorics.State → ℕ

Body:
fun S => ∑ p ∈ ⋯.toFinset, (2 * Int.natAbs p + 1) + ∑ p ∈ ⋯.toFinset, (2 * Int.natAbs p - 1)

Docstring: The energy of a state S is:
  energy(S) = ∑_{p≥0, p∈S} (2p+1) - ∑_{p<0, p∉S} (2p+1)

In the tex source, levels are half-integers `q = p + 1/2`, and the formula is:
  energy(S) = ∑_{q>0, q∈S} 2q - ∑_{q<0, q∉S} 2q

Substituting q = p + 1/2:
- q > 0 ⟺ p ≥ 0
- 2q = 2(p + 1/2) = 2p + 1

For p ≥ 0: 2p + 1 = 2*p.natAbs + 1 (since p.natAbs = p for p ≥ 0)
For p < 0: -(2p + 1) = -2p - 1 = 2*|p| - 1 = 2*p.natAbs - 1 (since p.natAbs = -p for p < 0)

Thus energy is always a natural number. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.State.fromFinsetPair (def)
Finset ℕ → Finset ℕ → AlgebraicCombinatorics.State

Body:
fun P N =>
  { levels := {p | p ≥ 0 ∧ Int.toNat p ∈ P ∨ p < 0 ∧ Int.toNat (-p - 1) ∉ N}, finite_nonneg := ⋯,
    finite_negative_missing := ⋯ }

Docstring: Construct a state from a pair (P, N) of finite subsets of ℕ.
- P represents the nonnegative levels in the state (n ∈ P means n ∈ S.levels)
- N represents the negative levels that are MISSING from the state
  (n ∈ N means -(n+1) ∉ S.levels) 

## PROJECT DEPENDENCY AlgebraicCombinatorics.State (inductive)
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

## PROJECT DEPENDENCY AlgebraicCombinatorics.State.levels (def)
AlgebraicCombinatorics.State → Set AlgebraicCombinatorics.Level

Body:
fun self => self.1

Docstring: The set of levels in this state 

## PROJECT DEPENDENCY AlgebraicCombinatorics.State.finite_nonneg (theorem)
∀ (self : AlgebraicCombinatorics.State), {p | p ≥ 0 ∧ p ∈ self.levels}.Finite

Docstring: Only finitely many nonnegative levels (p ≥ 0, representing positive half-integers p+1/2 > 0) are in the state 

## PROJECT DEPENDENCY AlgebraicCombinatorics.State.finite_negative_missing (theorem)
∀ (self : AlgebraicCombinatorics.State), {p | p < 0 ∧ p ∉ self.levels}.Finite

Docstring: Only finitely many negative levels (p < 0, representing negative half-integers p+1/2 < 0) are NOT in the state 

## PROJECT DEPENDENCY AlgebraicCombinatorics.State.mk (constructor)
(levels : Set AlgebraicCombinatorics.Level) →
  {p | p ≥ 0 ∧ p ∈ levels}.Finite → {p | p < 0 ∧ p ∉ levels}.Finite → AlgebraicCombinatorics.State

## BASE-LIBRARY REF Finset
Type u_4 → Type u_4

Docstring: `Finset α` is the type of finite sets of elements of `α`. It is implemented
as a multiset (a list up to permutation) which has no duplicate elements. 

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

## BASE-LIBRARY REF Finset.sum
{ι : Type u_1} → {M : Type u_3} → [AddCommMonoid M] → Finset ι → (ι → M) → M

Docstring: `∑ x ∈ s, f x` is the sum of `f x` as `x` ranges over the elements
of the finite set `s`.

When the index type is a `Fintype`, the notation `∑ x, f x`, is a shorthand for
`∑ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF Nat.instAddCommMonoid
AddCommMonoid ℕ

## BASE-LIBRARY REF HMul.hMul
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HMul α β γ] → α → β → γ

Docstring: `a * b` computes the product of `a` and `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `*` in identifiers is `mul`.

## BASE-LIBRARY REF instHMul
{α : Type u_1} → [Mul α] → HMul α α α

## BASE-LIBRARY REF instMulNat
Mul ℕ

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

## BASE-LIBRARY REF Set.Finite.toFinset
{α : Type u} → {s : Set α} → s.Finite → Finset α

Docstring: Using choice, get the `Finset` that represents this `Set`. 

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

## BASE-LIBRARY REF instOfNat
{n : ℕ} → OfNat ℤ n

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

## BASE-LIBRARY REF Int.natAbs
ℤ → ℕ

Docstring: The absolute value of an integer is its distance from `0`.

This function is overridden by the compiler with an efficient implementation. This definition is
the logical model.

Examples:
 * `(7 : Int).natAbs = 7`
 * `(0 : Int).natAbs = 0`
 * `(-11 : Int).natAbs = 11`


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

## BASE-LIBRARY REF HSub.hSub
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HSub α β γ] → α → β → γ

Docstring: `a - b` computes the difference of `a` and `b`.
The meaning of this notation is type-dependent.
* For natural numbers, this operator saturates at 0: `a - b = 0` when `a ≤ b`. 

Conventions for notations in identifiers:

 * The recommended spelling of `-` in identifiers is `sub` (when used as a binary operator).

## BASE-LIBRARY REF instHSub
{α : Type u_1} → [Sub α] → HSub α α α

## BASE-LIBRARY REF instSubNat
Sub ℕ

## BASE-LIBRARY REF Or
Prop → Prop → Prop

Docstring: `Or a b`, or `a ∨ b`, is the disjunction of propositions. There are two
constructors for `Or`, called `Or.inl : a → a ∨ b` and `Or.inr : b → a ∨ b`,
and you can use `match` or `cases` to destruct an `Or` assumption into the
two cases.


Conventions for notations in identifiers:

 * The recommended spelling of `∨` in identifiers is `or`.

 * The recommended spelling of `\/` in identifiers is `or` (prefer `∨` over `\/`).

## BASE-LIBRARY REF Finset.instMembership
{α : Type u_1} → Membership α (Finset α)

## BASE-LIBRARY REF Int.toNat
ℤ → ℕ

Docstring: Converts an integer into a natural number. Negative numbers are converted to `0`.

Examples:
* `(7 : Int).toNat = 7`
* `(0 : Int).toNat = 0`
* `(-7 : Int).toNat = 0`


## BASE-LIBRARY REF Int.instSub
Sub ℤ

## BASE-LIBRARY REF Neg.neg
{α : Type u} → [self : Neg α] → α → α

Docstring: `-a` computes the negative or opposite of `a`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `-` in identifiers is `neg` (when used as a unary operator).

## BASE-LIBRARY REF Int.instNegInt
Neg ℤ

## BASE-LIBRARY REF Set.Finite
{α : Type u} → Set α → Prop

Docstring: A set is finite if the corresponding `Subtype` is finite,
i.e., if there exists a natural `n : ℕ` and an equivalence `s ≃ Fin n`. 

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
lem.jtp.fromFinsetPair-energy

\leanhelper  For any pair $(P, N)$ of finite subsets of $\mathbb {N}$, 

\[  \operatorname {energy}(\operatorname {fromFinsetPair}(P,N)) = \sum _{n\in P}(2n+1) + \sum _{n\in N}(2n+1).  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.jtp.fromfinsetpair
def.jtp.fromFinsetPair

\leanhelper  Given a pair $(P, N)$ of finite subsets of $\mathbb {N}$, define the state $\operatorname {fromFinsetPair}(P, N)$ whose levels are 

\[  \{ p\geq 0 : p \in P\}  \cup \{ p < 0 : (-p-1) \notin N\} .  \]

 Here $P$ encodes the nonneg levels present, and $N$ encodes the negative levels missing (with $n \in N$ meaning level $-(n+1)$ is missing).

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.jtp.state
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
  "verdict": "faithful",
  "justification": "The target quantifies without added hypotheses over exactly \u201c\u2200 (P N : Finset \u2115),\u201d matching \u201cfor any pair (P, N) of finite subsets of \u2115.\u201d Its conclusion is exactly \u201cenergy = \u2211 n \u2208 P, (2 * n + 1) + \u2211 n \u2208 N, (2 * n + 1).\u201d The dependency `fromFinsetPair` has levels \u201cp \u2265 0 \u2227 Int.toNat p \u2208 P \u2228 p < 0 \u2227 Int.toNat (-p - 1) \u2209 N,\u201d matching the informal definition. For a missing negative level `p = -(n+1)`, the formal energy summand `2 * Int.natAbs p - 1` is `2(n+1)-1 = 2n+1`, while a present nonnegative level `n` contributes `2n+1`. Thus the formal and blueprint statements agree."
}