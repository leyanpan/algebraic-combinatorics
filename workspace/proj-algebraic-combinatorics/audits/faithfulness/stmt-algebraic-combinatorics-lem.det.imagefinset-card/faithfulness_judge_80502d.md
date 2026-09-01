## TARGET PermFinset.imageFinset_card (theorem) — ELABORATED SIGNATURE
∀ {n : ℕ} (σ : Equiv.Perm (Fin n)) (P : Finset (Fin n)), (PermFinset.imageFinset σ P).card = P.card

Docstring: The image has the same cardinality as the original set. 

## PROJECT DEPENDENCY PermFinset.imageFinset (def)
{n : ℕ} → Equiv.Perm (Fin n) → Finset (Fin n) → Finset (Fin n)

Body:
fun {n} σ P => Finset.map { toFun := ⇑σ, inj' := ⋯ } P

Docstring: The image of a finset under a permutation. 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF Equiv.Perm
Sort u_1 → Sort (max 1 u_1)

Docstring: `Perm α` is the type of bijections from `α` to itself. 

## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


## BASE-LIBRARY REF Finset
Type u_4 → Type u_4

Docstring: `Finset α` is the type of finite sets of elements of `α`. It is implemented
as a multiset (a list up to permutation) which has no duplicate elements. 

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

## BASE-LIBRARY REF Finset.map
{α : Type u_1} → {β : Type u_2} → (α ↪ β) → Finset α → Finset β

Docstring: When `f` is an embedding of `α` in `β` and `s` is a finset in `α`, then `s.map f` is the image
finset in `β`. The embedding condition guarantees that there are no duplicates in the image. 

## BASE-LIBRARY REF Function.Embedding.mk
{α : Sort u_1} → {β : Sort u_2} → (toFun : α → β) → Function.Injective toFun → α ↪ β

## BASE-LIBRARY REF DFunLike.coe
{F : Sort u_1} → {α : outParam (Sort u_2)} → {β : outParam (α → Sort u_3)} → [self : DFunLike F α β] → F → (a : α) → β a

Docstring: The coercion from `F` to a function. 

## BASE-LIBRARY REF EquivLike.toFunLike
{E : Sort u_1} → {α : Sort u_3} → {β : Sort u_4} → [EquivLike E α β] → FunLike E α β

## BASE-LIBRARY REF Equiv.instEquivLike
{α : Sort u} → {β : Sort v} → EquivLike (α ≃ β) α β

## INFORMAL STATEMENT
lem.det.imageFinset-card

\leanhelper  The image of a finset under a permutation has the same cardinality: $|\sigma (P)| = |P|$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.det.imagefinset
def.det.imageFinset

\leanhelper  The \emph{image} of a finite subset $P \subseteq [n]$ under a permutation $\sigma \in S_n$ is $\sigma (P) = \{ \sigma (i) \mid i \in P\} $.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The blueprint quantifies over a finite subset `P \u2286 [n]` and a permutation `\u03c3 \u2208 S\u2099`, asserting `|\u03c3(P)| = |P|`. The target has exactly the corresponding binders, `\u2200 {n : \u2115} (\u03c3 : Equiv.Perm (Fin n)) (P : Finset (Fin n))`, and conclusion `(PermFinset.imageFinset \u03c3 P).card = P.card`. Here `Fin n` is the canonical `n`-element set, `Equiv.Perm (Fin n)` is a permutation of it, and `Finset (Fin n)` represents its finite subsets. Moreover, `PermFinset.imageFinset` is defined as `Finset.map { toFun := \u21d1\u03c3, inj' := \u22ef } P`, which is precisely `{\u03c3(i) | i \u2208 P}`; its injective embedding correctly preserves distinct elements. Thus the formal conclusion exactly expresses the stated cardinality equality, with no added hypotheses or narrowed quantifiers."
}