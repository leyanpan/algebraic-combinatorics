## TARGET AlgebraicCombinatorics.SignedCounting.acceptable_nonAcceptablePartner_iff (theorem) — ELABORATED SIGNATURE
∀ (n m : ℕ),
  0 < n →
    ∀ I ∈ AlgebraicCombinatorics.SignedCounting.acceptableSets n m,
      AlgebraicCombinatorics.SignedCounting.partner I ∉ AlgebraicCombinatorics.SignedCounting.acceptableSets n m ↔
        0 ∉ I ∧ I.card = m

Docstring: The set of acceptable sets with non-acceptable partners consists exactly of
m-element subsets of `{0, ..., n-1}` that do not contain 0.

Note: We require `0 < n` because when `n = 0`, the partner of `∅` is `{0}` which
is not in `range 0`, but `∅.card = 0` may not equal `m`. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SignedCounting.acceptableSets (def)
ℕ → ℕ → Finset (Finset ℕ)

Body:
fun n m => {I ∈ (Finset.range n).powerset | I.card ≤ m}

Docstring: The finset of acceptable sets: subsets of `Finset.range n` with cardinality at most `m`. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SignedCounting.partner (def)
Finset ℕ → Finset ℕ

Body:
fun I => symmDiff I {0}

Docstring: The partner of a finite set `I` is `I △ {0}` (symmetric difference with singleton 0).
If `0 ∈ I`, this removes 0; if `0 ∉ I`, this adds 0. 

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

## BASE-LIBRARY REF Finset
Type u_4 → Type u_4

Docstring: `Finset α` is the type of finite sets of elements of `α`. It is implemented
as a multiset (a list up to permutation) which has no duplicate elements. 

## BASE-LIBRARY REF Membership.mem
{α : outParam (Type u)} → {γ : Type v} → [self : Membership α γ] → γ → α → Prop

Docstring: The membership relation `a ∈ s : Prop` where `a : α`, `s : γ`. 

Conventions for notations in identifiers:

 * The recommended spelling of `∈` in identifiers is `mem`.

## BASE-LIBRARY REF Finset.instMembership
{α : Type u_1} → Membership α (Finset α)

## BASE-LIBRARY REF Iff
Prop → Prop → Prop

Docstring: If and only if, or logical bi-implication. `a ↔ b` means that `a` implies `b` and vice versa.
By `propext`, this implies that `a` and `b` are equal and hence any expression involving `a`
is equivalent to the corresponding expression with `b` instead.


Conventions for notations in identifiers:

 * The recommended spelling of `↔` in identifiers is `iff`.

 * The recommended spelling of `<->` in identifiers is `iff` (prefer `↔` over `<->`).

## BASE-LIBRARY REF Not
Prop → Prop

Docstring: `Not p`, or `¬p`, is the negation of `p`. It is defined to be `p → False`,
so if your goal is `¬p` you can use `intro h` to turn the goal into
`h : p ⊢ False`, and if you have `hn : ¬p` and `h : p` then `hn h : False`
and `(hn h).elim` will prove anything.
For more information: [Propositional Logic](https://lean-lang.org/theorem_proving_in_lean4/propositions_and_proofs.html#propositional-logic)


Conventions for notations in identifiers:

 * The recommended spelling of `¬` in identifiers is `not`.

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

## BASE-LIBRARY REF LE.le
{α : Type u} → [self : LE α] → α → α → Prop

Docstring: The less-equal relation: `x ≤ y` 

Conventions for notations in identifiers:

 * The recommended spelling of `≤` in identifiers is `le`.

 * The recommended spelling of `<=` in identifiers is `le` (prefer `≤` over `<=`).

## BASE-LIBRARY REF instLENat
LE ℕ

## BASE-LIBRARY REF Nat.decLe
(n m : ℕ) → Decidable (n ≤ m)

Docstring: A decision procedure for non-strict inequality of natural numbers, usually accessed via the
`DecidableLE Nat` instance.

Examples:
 * `(if 3 ≤ 4 then "yes" else "no") = "yes"`
 * `(if 6 ≤ 4 then "yes" else "no") = "no"`
 * `show 12 ≤ 12 by decide`
 * `show 5 ≤ 12 by decide`


## BASE-LIBRARY REF Finset.powerset
{α : Type u_1} → Finset α → Finset (Finset α)

Docstring: When `s` is a finset, `s.powerset` is the finset of all subsets of `s` (seen as finsets). 

## BASE-LIBRARY REF Finset.range
ℕ → Finset ℕ

Docstring: `range n` is the set of natural numbers less than `n`. 

## BASE-LIBRARY REF symmDiff
{α : Type u_2} → [Max α] → [SDiff α] → α → α → α

Docstring: The symmetric difference operator on a type with `⊔` and `\` is `(A \ B) ⊔ (B \ A)`. 

## BASE-LIBRARY REF SemilatticeSup.toMax
{α : Type u} → [SemilatticeSup α] → Max α

## BASE-LIBRARY REF Lattice.toSemilatticeSup
{α : Type u} → [self : Lattice α] → SemilatticeSup α

## BASE-LIBRARY REF Finset.instLattice
{α : Type u_1} → [DecidableEq α] → Lattice (Finset α)

## BASE-LIBRARY REF instDecidableEqNat
DecidableEq ℕ

## BASE-LIBRARY REF Finset.instSDiff
{α : Type u_1} → [DecidableEq α] → SDiff (Finset α)

Docstring: `s \ t` is the set consisting of the elements of `s` that are not in `t`. 

## BASE-LIBRARY REF Singleton.singleton
{α : outParam (Type u)} → {β : Type v} → [self : Singleton α β] → α → β

Docstring: `singleton x` is a collection with the single element `x` (notation: `{x}`). 

Conventions for notations in identifiers:

 * The recommended spelling of `{x}` in identifiers is `singleton`.

## BASE-LIBRARY REF Finset.instSingleton
{α : Type u_1} → Singleton α (Finset α)

Docstring: `{a} : Finset a` is the set `{a}` containing `a` and nothing else.

This differs from `insert a ∅` in that it does not require a `DecidableEq` instance for `α`.


## INFORMAL STATEMENT
thm.acceptable_nonAcceptablePartner_iff

\leanhelper  Let $n \geq 1$, $m \in \mathbb {N}$, and let $I$ be an acceptable set (i.e., $I \subseteq \{ 0, \ldots , n-1\} $ with $|I| \leq m$). Then the partner $I'$ of $I$ is non-acceptable if and only if $0 \notin I$ and $|I| = m$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.acceptablesets
def.acceptableSets

\leanhelper  The \emph{acceptable sets} for parameters $n, m \in \mathbb {N}$ are the subsets of $\{ 0, 1, \ldots , n-1\} $ with cardinality at most $m$: 

\[  \mathcal{A}(n, m) := \bigl\{ I \subseteq \{ 0, \ldots , n-1\}  : |I| \leq m\bigr\} .  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.partner
def.partner

\leanhelper  The \emph{partner} of a finite set $I$ of natural numbers is the symmetric difference $I' := I \bigtriangleup \{ 0\} $. If $0 \in I$, then $I' = I \setminus \{ 0\} $; if $0 \notin I$, then $I' = I \cup \{ 0\} $.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The binders `\u2200 (n m : \u2115), 0 < n \u2192 \u2200 I \u2208 acceptableSets n m` exactly match \u201cLet n \u2265 1, m \u2208 \u2115, and let I be an acceptable set,\u201d since for naturals `0 < n` is equivalent to `n \u2265 1`. The body of `acceptableSets`, `{I \u2208 (Finset.range n).powerset | I.card \u2264 m}`, expresses precisely `I \u2286 {0,\u2026,n\u22121}` with `|I| \u2264 m`. The conclusion `partner I \u2209 acceptableSets n m \u2194 0 \u2209 I \u2227 I.card = m` exactly matches \u201cthe partner I\u2032 is non-acceptable iff 0 \u2209 I and |I| = m,\u201d and `partner I := symmDiff I {0}` agrees with the informal definition."
}