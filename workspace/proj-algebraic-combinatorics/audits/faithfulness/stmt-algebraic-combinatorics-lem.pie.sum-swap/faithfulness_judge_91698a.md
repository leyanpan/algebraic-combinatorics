## TARGET BooleanMobius.sum_powerset_powerset_swap (theorem) — ELABORATED SIGNATURE
∀ {α : Type u_1} [inst : DecidableEq α] {Q : Finset α} {A : Type u_2} [inst_1 : AddCommGroup A]
  (f : Finset α → Finset α → A),
  ∑ J ∈ Q.powerset, ∑ P ∈ J.powerset, f J P = ∑ P ∈ Q.powerset, ∑ J ∈ Q.powerset with P ⊆ J, f J P

Docstring: A helper lemma for swapping sums over pairs (J, P) with P ⊆ J ⊆ Q
to pairs (P, J) with P ⊆ J ⊆ Q. 

## BASE-LIBRARY REF DecidableEq
Sort u → Sort (max 1 u)

Docstring: Propositional equality is `Decidable` for all elements of a type.

In other words, an instance of `DecidableEq α` is a means of deciding the proposition `a = b` is
for all `a b : α`.


## BASE-LIBRARY REF Finset
Type u_4 → Type u_4

Docstring: `Finset α` is the type of finite sets of elements of `α`. It is implemented
as a multiset (a list up to permutation) which has no duplicate elements. 

## BASE-LIBRARY REF AddCommGroup
Type u → Type u

Docstring: An additive commutative group is an additive group with commutative `(+)`. 

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

## BASE-LIBRARY REF Finset.sum
{ι : Type u_1} → {M : Type u_3} → [AddCommMonoid M] → Finset ι → (ι → M) → M

Docstring: `∑ x ∈ s, f x` is the sum of `f x` as `x` ranges over the elements
of the finite set `s`.

When the index type is a `Fintype`, the notation `∑ x, f x`, is a shorthand for
`∑ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF AddCommGroup.toAddCommMonoid
{G : Type u} → [self : AddCommGroup G] → AddCommMonoid G

## BASE-LIBRARY REF Finset.powerset
{α : Type u_1} → Finset α → Finset (Finset α)

Docstring: When `s` is a finset, `s.powerset` is the finset of all subsets of `s` (seen as finsets). 

## BASE-LIBRARY REF Finset.filter
{α : Type u_1} → (p : α → Prop) → [DecidablePred p] → Finset α → Finset α

Docstring: `Finset.filter p s` is the set of elements of `s` that satisfy `p`.

For example, one can use `s.filter (· ∈ t)` to get the intersection of `s` with `t : Set α`
as a `Finset α` (when a `DecidablePred (· ∈ t)` instance is available). 

## BASE-LIBRARY REF HasSubset.Subset
{α : Type u} → [self : HasSubset α] → α → α → Prop

Docstring: Subset relation: `a ⊆ b`  

Conventions for notations in identifiers:

 * The recommended spelling of `⊆` in identifiers is `subset`.

## BASE-LIBRARY REF Finset.instHasSubset
{α : Type u_1} → HasSubset (Finset α)

## BASE-LIBRARY REF Finset.instDecidableRelSubset
{α : Type u_1} → [DecidableEq α] → DecidableRel fun x1 x2 => x1 ⊆ x2

## INFORMAL STATEMENT
lem.pie.sum-swap

\leanhelper  Let $Q$ be a finite set, $A$ an additive abelian group, and $f$ a function that assigns to each pair $(J, P)$ of subsets of $Q$ an element of $A$. Then 

\[  \sum _{J \subseteq Q} \sum _{P \subseteq J} f(J, P) = \sum _{P \subseteq Q} \sum _{\substack {J \subseteq Q;\\ P \subseteq J}} f(J, P).  \]

## VERDICT
{
  "verdict": "faithful",
  "justification": "The formal binders match the blueprint: `{Q : Finset \u03b1}` represents the finite set Q, `[AddCommGroup A]` matches \u201cA an additive abelian group,\u201d and `f : Finset \u03b1 \u2192 Finset \u03b1 \u2192 A` is a harmlessly more general version of a function on pairs of subsets of Q, since every occurrence is evaluated only on `J \u2286 Q` and `P \u2286 J`. The equality `\u2211 J \u2208 Q.powerset, \u2211 P \u2208 J.powerset, f J P = \u2211 P \u2208 Q.powerset, \u2211 J \u2208 Q.powerset with P \u2286 J, f J P` exactly expresses the two orders of summation in the blueprint. The binder `[DecidableEq \u03b1]` is an encoding requirement for finite-set powersets and decidable subset filtering, not a mathematically contentful restriction."
}