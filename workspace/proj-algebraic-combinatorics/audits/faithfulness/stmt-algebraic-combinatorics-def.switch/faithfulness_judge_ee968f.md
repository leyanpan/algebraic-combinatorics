## TARGET AlgebraicCombinatorics.SignedCounting.switch (def) — ELABORATED SIGNATURE
ℕ → Finset ℕ → Finset ℕ

Body:
fun i S => if (S ∩ {i, i + 1}).card = 1 then symmDiff S {i, i + 1} else S

Docstring: Switch `i` with `i+1` in a set: if exactly one of `{i, i+1}` is in `S`,
replace it with the other; otherwise leave `S` unchanged. 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF Finset
Type u_4 → Type u_4

Docstring: `Finset α` is the type of finite sets of elements of `α`. It is implemented
as a multiset (a list up to permutation) which has no duplicate elements. 

## BASE-LIBRARY REF ite
{α : Sort u} → (c : Prop) → [h : Decidable c] → α → α → α

Docstring: `if c then t else e` is notation for `ite c t e`, "if-then-else", which decides to
return `t` or `e` depending on whether `c` is true or false. The explicit argument
`c : Prop` does not have any actual computational content, but there is an additional
`[Decidable c]` argument synthesized by typeclass inference which actually
determines how to evaluate `c` to true or false. Write `if h : c then t else e`
instead for a "dependent if-then-else" `dite`, which allows `t`/`e` to use the fact
that `c` is true/false.


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

## BASE-LIBRARY REF Inter.inter
{α : Type u} → [self : Inter α] → α → α → α

Docstring: `a ∩ b` is the intersection of `a` and `b`. 

Conventions for notations in identifiers:

 * The recommended spelling of `∩` in identifiers is `inter`.

## BASE-LIBRARY REF Finset.instInter
{α : Type u_1} → [DecidableEq α] → Inter (Finset α)

Docstring: `s ∩ t` is the set such that `a ∈ s ∩ t` iff `a ∈ s` and `a ∈ t`. 

## BASE-LIBRARY REF instDecidableEqNat
DecidableEq ℕ

## BASE-LIBRARY REF Insert.insert
{α : outParam (Type u)} → {γ : Type v} → [self : Insert α γ] → α → γ → γ

Docstring: `insert x xs` inserts the element `x` into the collection `xs`. 

## BASE-LIBRARY REF Finset.instInsert
{α : Type u_1} → [DecidableEq α] → Insert α (Finset α)

Docstring: `insert a s` is the set `{a} ∪ s` containing `a` and the elements of `s`. 

## BASE-LIBRARY REF Singleton.singleton
{α : outParam (Type u)} → {β : Type v} → [self : Singleton α β] → α → β

Docstring: `singleton x` is a collection with the single element `x` (notation: `{x}`). 

Conventions for notations in identifiers:

 * The recommended spelling of `{x}` in identifiers is `singleton`.

## BASE-LIBRARY REF Finset.instSingleton
{α : Type u_1} → Singleton α (Finset α)

Docstring: `{a} : Finset a` is the set `{a}` containing `a` and nothing else.

This differs from `insert a ∅` in that it does not require a `DecidableEq` instance for `α`.


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

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

## BASE-LIBRARY REF symmDiff
{α : Type u_2} → [Max α] → [SDiff α] → α → α → α

Docstring: The symmetric difference operator on a type with `⊔` and `\` is `(A \ B) ⊔ (B \ A)`. 

## BASE-LIBRARY REF SemilatticeSup.toMax
{α : Type u} → [SemilatticeSup α] → Max α

## BASE-LIBRARY REF Lattice.toSemilatticeSup
{α : Type u} → [self : Lattice α] → SemilatticeSup α

## BASE-LIBRARY REF Finset.instLattice
{α : Type u_1} → [DecidableEq α] → Lattice (Finset α)

## BASE-LIBRARY REF Finset.instSDiff
{α : Type u_1} → [DecidableEq α] → SDiff (Finset α)

Docstring: `s \ t` is the set consisting of the elements of `s` that are not in `t`. 

## INFORMAL STATEMENT
def.switch

\leanhelper  For $i \in \mathbb {N}$, define the \emph{switch operation} $\operatorname {switch}_i$ on finite subsets $S$ of $\mathbb {N}$ by 

\[  \operatorname {switch}_i(S) := \begin{cases}  S \bigtriangleup \{ i, i+1\} , &  \text{if } |S \cap \{ i, i+1\} | = 1; \\ S, &  \text{otherwise.} \end{cases}  \]

 In other words, if exactly one of $i$ and $i+1$ belongs to $S$, then we replace it by the other; otherwise we leave $S$ unchanged.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The target has exactly the required domain and codomain, `\u2115 \u2192 Finset \u2115 \u2192 Finset \u2115`, matching \u201cfor i \u2208 \u2115\u201d and finite subsets `S` of `\u2115`. Its body, `if (S \u2229 {i, i + 1}).card = 1 then symmDiff S {i, i + 1} else S`, directly matches the two blueprint branches: `S \u25b3 {i,i+1}` when `|S \u2229 {i,i+1}| = 1`, and `S` otherwise. The supplied `Finset` intersection, cardinality, and `symmDiff` meanings agree with the informal definition, with no added hypotheses or narrowed quantifiers."
}