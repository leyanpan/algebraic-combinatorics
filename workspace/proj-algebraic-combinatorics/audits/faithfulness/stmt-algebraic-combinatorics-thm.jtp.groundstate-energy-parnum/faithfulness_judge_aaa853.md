## TARGET AlgebraicCombinatorics.State.groundState_energy (theorem) — ELABORATED SIGNATURE
∀ (ell : ℤ), (AlgebraicCombinatorics.State.groundState ell).energy = ell.natAbs ^ 2

Docstring: The energy of the ground state G_ℓ is ℓ².

For ℓ ≥ 0:
- G_ℓ = {p : p < ℓ}
- Nonnegative integers in G_ℓ: {0, 1, ..., ℓ-1}
- Energy from nonneg: (2*0+1) + (2*1+1) + ... + (2*(ℓ-1)+1) = 1 + 3 + 5 + ... + (2ℓ-1) = ℓ²
- No negative integers are missing, so energy from neg_missing = 0
- Total energy = ℓ²

For ℓ < 0:
- G_ℓ = {p : p < ℓ}
- No nonnegative integers in G_ℓ, so energy from nonneg = 0
- Negative integers missing from G_ℓ: {ℓ, ℓ+1, ..., -1}
- Energy from neg_missing: (2*|ℓ|-1) + (2*|ℓ+1|-1) + ... + (2*|-1|-1)
                         = (2*|ℓ|-1) + (2*(|ℓ|-1)-1) + ... + (2*1-1)
                         = (2|ℓ|-1) + (2|ℓ|-3) + ... + 1 = |ℓ|² = ℓ²

The proof is technical and involves showing that:
- The sum 1 + 3 + 5 + ... + (2n-1) = n² (sum of first n odd numbers)
- The correct correspondence between the finite sets and the sums


## TARGET AlgebraicCombinatorics.State.groundState_parnum (theorem) — ELABORATED SIGNATURE
∀ (ell : ℤ), (AlgebraicCombinatorics.State.groundState ell).parnum = ell

Docstring: The particle number of the ground state G_ℓ is ℓ. 

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

## PROJECT DEPENDENCY AlgebraicCombinatorics.State.groundState (def)
ℤ → AlgebraicCombinatorics.State

Body:
fun ell => { levels := {p | p < ell}, finite_nonneg := ⋯, finite_negative_missing := ⋯ }

Docstring: The ℓ-ground state G_ℓ = {all levels < ℓ}.

In the half-integer convention, G_ℓ contains all half-integer levels q < ℓ.
In our integer representation (where level q = p + 1/2), this is {p : p < ℓ}.

For ℓ ≥ 0:
- Nonnegative integers in G_ℓ: {0, 1, ..., ℓ-1}
- No negative integers are missing from G_ℓ

For ℓ < 0:
- No nonnegative integers are in G_ℓ
- Negative integers missing from G_ℓ: {ℓ, ℓ+1, ..., -1} 

## PROJECT DEPENDENCY AlgebraicCombinatorics.State.parnum (def)
AlgebraicCombinatorics.State → ℤ

Body:
fun S => ↑⋯.toFinset.card - ↑⋯.toFinset.card

Docstring: The particle number of a state S is:
  parnum(S) = #{p ≥ 0 : p ∈ S} - #{p < 0 : p ∉ S}

In the tex source, this counts the number of positive half-integer levels in S
minus the number of negative half-integer levels not in S. 

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

## BASE-LIBRARY REF Int
Type

Docstring: The integers.

This type is special-cased by the compiler and overridden with an efficient implementation. The
runtime has a special representation for `Int` that stores “small” signed numbers directly, while
larger numbers use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)). A “small number” is an integer that can be encoded with one fewer bits
than the platform's pointer size (i.e. 63 bits on 64-bit architectures and 31 bits on 32-bit
architectures).


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

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF HPow.hPow
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HPow α β γ] → α → β → γ

Docstring: `a ^ b` computes `a` to the power of `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `^` in identifiers is `pow`.

## BASE-LIBRARY REF instHPow
{α : Type u_1} → {β : Type u_2} → [Pow α β] → HPow α β α

## BASE-LIBRARY REF Monoid.toNatPow
{M : Type u_2} → [Monoid M] → Pow M ℕ

## BASE-LIBRARY REF Nat.instMonoid
Monoid ℕ

## BASE-LIBRARY REF Int.natAbs
ℤ → ℕ

Docstring: The absolute value of an integer is its distance from `0`.

This function is overridden by the compiler with an efficient implementation. This definition is
the logical model.

Examples:
 * `(7 : Int).natAbs = 7`
 * `(0 : Int).natAbs = 0`
 * `(-11 : Int).natAbs = 11`


## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

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

## BASE-LIBRARY REF Int.instSub
Sub ℤ

## BASE-LIBRARY REF Nat.cast
{R : Type u} → [NatCast R] → ℕ → R

Docstring: The canonical homomorphism `Nat → R`. In most use cases, the target type will have a (semi)ring
structure, and this homomorphism should be a (semi)ring homomorphism.

`NatCast` and `IntCast` exist to allow different libraries with their own types that can be notated
as natural numbers to have consistent `simp` normal forms without needing to create coercion
simplification sets that are aware of all combinations. Libraries should make it easy to work with
`NatCast` where possible. For instance, in Mathlib there will be such a homomorphism (and thus a
`NatCast R` instance) whenever `R` is an additive monoid with a `1`.

The prototypical example is `Int.ofNat`.


## BASE-LIBRARY REF instNatCastInt
NatCast ℤ

## BASE-LIBRARY REF Finset.card
{α : Type u_1} → Finset α → ℕ

Docstring: `s.card` is the number of elements of `s`, aka its cardinality.

The notation `#s` can be accessed in the `Finset` locale. 

## BASE-LIBRARY REF Set.Finite
{α : Type u} → Set α → Prop

Docstring: A set is finite if the corresponding `Subtype` is finite,
i.e., if there exists a natural `n : ℕ` and an equivalence `s ≃ Fin n`. 

## INFORMAL STATEMENT
thm.jtp.groundState-energy-parnum

\leanhelper  For any $\ell \in \mathbb {Z}$, we have $\operatorname {energy}G_{\ell }=\ell ^{2}$ and $\operatorname {parnum}G_{\ell }=\ell $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.jtp.groundstate
def.jtp.groundState

\leanhelper  For $\ell \in \mathbb {Z}$, the \emph{$\ell $-ground state} is 

\[  G_{\ell }:=\left\{  \text{all levels }<\ell \right\} .  \]

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
  "justification": "The two target declarations exactly split the blueprint\u2019s conjunction. They quantify without added hypotheses over the required domain: `\u2200 (ell : \u2124)`. The first concludes `(groundState ell).energy = ell.natAbs ^ 2`, which is the natural-number value of the blueprint\u2019s `energy G_\u2113 = \u2113\u00b2`; since energy is defined in `\u2115`, `ell.natAbs ^ 2` is precisely the nonnegative square of the integer \u2113. The second concludes `(groundState ell).parnum = ell`, exactly matching `parnum G_\u2113 = \u2113`. The dependency `groundState` has levels `{p | p < ell}`; under the stated representation `q = p + 1/2`, this corresponds to the informal set of half-integer levels `q < \u2113`. The formal `energy` and `parnum` bodies likewise use the specified nonnegative-present and negative-missing levels with the correct weights and signed cardinality difference. Thus, taken together, the declarations imply the full informal statement with no contentful restriction or added hypothesis."
}