## TARGET AlgebraicCombinatorics.SignedCounting.sign_cancel2 (theorem) — ELABORATED SIGNATURE
∀ {α : Type u_1} [inst : DecidableEq α] {R : Type u_2} [inst_1 : AddCommGroup R] (A X : Finset α),
  X ⊆ A →
    ∀ (sign : α → R) (f : ↥X → ↥X),
      (∀ (I : ↥X), f (f I) = I) →
        (∀ (I : ↥X), f I ≠ I) → (∀ (I : ↥X), sign ↑(f I) = -sign ↑I) → ∑ I ∈ A, sign I = ∑ I ∈ A \ X, sign I

Docstring: **Cancellation Principle, Take 2** (lem.sign.cancel2)

Let `A` be a finite set, `X ⊆ A`, and `sign : A → R` for any additive abelian group `R`.
If `f : X → X` is an involution with no fixed points satisfying
`sign(f(I)) = -sign(I)` for all `I ∈ X`, then `∑_{I ∈ A} sign(I) = ∑_{I ∈ A \ X} sign(I)`.

This version works for any additive abelian group (no 2-torsion requirement).


## BASE-LIBRARY REF DecidableEq
Sort u → Sort (max 1 u)

Docstring: Propositional equality is `Decidable` for all elements of a type.

In other words, an instance of `DecidableEq α` is a means of deciding the proposition `a = b` is
for all `a b : α`.


## BASE-LIBRARY REF AddCommGroup
Type u → Type u

Docstring: An additive commutative group is an additive group with commutative `(+)`. 

## BASE-LIBRARY REF Finset
Type u_4 → Type u_4

Docstring: `Finset α` is the type of finite sets of elements of `α`. It is implemented
as a multiset (a list up to permutation) which has no duplicate elements. 

## BASE-LIBRARY REF HasSubset.Subset
{α : Type u} → [self : HasSubset α] → α → α → Prop

Docstring: Subset relation: `a ⊆ b`  

Conventions for notations in identifiers:

 * The recommended spelling of `⊆` in identifiers is `subset`.

## BASE-LIBRARY REF Finset.instHasSubset
{α : Type u_1} → HasSubset (Finset α)

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

## BASE-LIBRARY REF Membership.mem
{α : outParam (Type u)} → {γ : Type v} → [self : Membership α γ] → γ → α → Prop

Docstring: The membership relation `a ∈ s : Prop` where `a : α`, `s : γ`. 

Conventions for notations in identifiers:

 * The recommended spelling of `∈` in identifiers is `mem`.

## BASE-LIBRARY REF SetLike.instMembership
{A : Type u_1} → {B : Type u_2} → [i : SetLike A B] → Membership B A

## BASE-LIBRARY REF Finset.instSetLike
{α : Type u_1} → SetLike (Finset α) α

Docstring: Convert a finset to a set in the natural way. 

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

## BASE-LIBRARY REF Ne
{α : Sort u} → α → α → Prop

Docstring: `a ≠ b`, or `Ne a b` is defined as `¬ (a = b)` or `a = b → False`,
and asserts that `a` and `b` are not equal.


Conventions for notations in identifiers:

 * The recommended spelling of `≠` in identifiers is `ne`.

## BASE-LIBRARY REF Subtype.val
{α : Sort u} → {p : α → Prop} → Subtype p → α

Docstring: The value in the underlying type that satisfies the predicate.


## BASE-LIBRARY REF Neg.neg
{α : Type u} → [self : Neg α] → α → α

Docstring: `-a` computes the negative or opposite of `a`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `-` in identifiers is `neg` (when used as a unary operator).

## BASE-LIBRARY REF NegZeroClass.toNeg
{G : Type u_2} → [self : NegZeroClass G] → Neg G

## BASE-LIBRARY REF SubNegZeroMonoid.toNegZeroClass
{G : Type u_2} → [self : SubNegZeroMonoid G] → NegZeroClass G

## BASE-LIBRARY REF SubtractionMonoid.toSubNegZeroMonoid
{α : Type u_1} → [SubtractionMonoid α] → SubNegZeroMonoid α

## BASE-LIBRARY REF SubtractionCommMonoid.toSubtractionMonoid
{G : Type u} → [self : SubtractionCommMonoid G] → SubtractionMonoid G

## BASE-LIBRARY REF AddCommGroup.toDivisionAddCommMonoid
{G : Type u_1} → [AddCommGroup G] → SubtractionCommMonoid G

## BASE-LIBRARY REF Finset.sum
{ι : Type u_1} → {M : Type u_3} → [AddCommMonoid M] → Finset ι → (ι → M) → M

Docstring: `∑ x ∈ s, f x` is the sum of `f x` as `x` ranges over the elements
of the finite set `s`.

When the index type is a `Fintype`, the notation `∑ x, f x`, is a shorthand for
`∑ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF AddCommGroup.toAddCommMonoid
{G : Type u} → [self : AddCommGroup G] → AddCommMonoid G

## BASE-LIBRARY REF SDiff.sdiff
{α : Type u} → [self : SDiff α] → α → α → α

Docstring: `a \ b` is the set difference of `a` and `b`,
consisting of all elements in `a` that are not in `b`.


Conventions for notations in identifiers:

 * The recommended spelling of `\` in identifiers is `sdiff`.

## BASE-LIBRARY REF Finset.instSDiff
{α : Type u_1} → [DecidableEq α] → SDiff (Finset α)

Docstring: `s \ t` is the set consisting of the elements of `s` that are not in `t`. 

## INFORMAL STATEMENT
Cancellation principle, take 2

Let $\mathcal{A}$ be a finite set. Let $\mathcal{X}$ be a subset of $\mathcal{A}$. 

For each $I \in \mathcal{A}$, let $\operatorname {sign} I$ be an element of some additive abelian group. Let $f : \mathcal{X} \to \mathcal{X}$ be an involution (i.e., a map satisfying $f \circ f = \operatorname {id}$) that has no fixed points. Assume that 

\[  \operatorname {sign}(f(I)) = -\operatorname {sign} I \qquad \text{for all } I \in \mathcal{X}.  \]

 Then, 

\[  \sum _{I \in \mathcal{A}} \operatorname {sign} I = \sum _{I \in \mathcal{A} \setminus \mathcal{X}} \operatorname {sign} I.  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.invol
def.perm.invol

Let $X$ be a set. An \emph{involution} of $X$ means a map $f : X \to X$ that satisfies $f \circ f = \operatorname {id}$. Clearly, an involution is always a permutation, and equals its own inverse.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.perm.perm
def.perm.perm

Let $X$ be a set. 

\textbf{(a)} A \emph{permutation} of $X$ means a bijection from $X$ to $X$. 

\textbf{(b)} It is known that the set of all permutations of $X$ is a group under composition. This group is called the \emph{symmetric group} of $X$, and is denoted by $S_X$. Its neutral element is the identity map $\operatorname {id}_X : X \to X$. Its size is $|X|!$ when $X$ is finite. 

\textbf{(c)} As usual in group theory, we will write $\alpha \beta $ for the composition $\alpha \circ \beta $ when $\alpha , \beta \in S_X$. This is the map that sends each $x \in X$ to $\alpha (\beta (x))$. 

\textbf{(d)} If $\alpha \in S_X$ and $i \in \mathbb {Z}$, then $\alpha ^i$ shall denote the $i$-th power of $\alpha $ in the group $S_X$. Note that $\alpha ^i = \underbrace{\alpha \circ \alpha \circ \cdots \circ \alpha }_{i\text{ times}}$ if $i \ge 0$. Also, $\alpha ^0 = \operatorname {id}_X$. Also, $\alpha ^{-1}$ is the inverse of $\alpha $ in the group $S_X$, that is, the inverse of the map $\alpha $.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The formal binders match the blueprint: `A X : Finset \u03b1` represents the finite sets, `X \u2286 A` is the required subset relation, and `f : \u21a5X \u2192 \u21a5X` is a self-map of `X`. The hypotheses `(\u2200 I, f (f I) = I)` and `(\u2200 I, f I \u2260 I)` state exactly that `f` is an involution with no fixed points. Likewise, `(\u2200 I : \u21a5X, sign \u2191(f I) = -sign \u2191I)` is the stated sign-reversal condition on every `I \u2208 X`, and the conclusion `\u2211 I \u2208 A, sign I = \u2211 I \u2208 A \\ X, sign I` is exactly the claimed cancellation identity. The formal `sign : \u03b1 \u2192 R` is defined on an ambient type rather than only on `A`, but the theorem only uses its restriction to `A`; this is a harmless ambient encoding and does not change the assertion. `[AddCommGroup R]` is precisely the additive abelian group assumption, while `[DecidableEq \u03b1]` is the computational instance needed for finset difference and is not a mathematically contentful extra hypothesis."
}