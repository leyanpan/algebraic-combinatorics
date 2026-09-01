## TARGET AlgebraicCombinatorics.SignedCounting.sign_cancel1 (theorem) — ELABORATED SIGNATURE
∀ {α : Type u_1} [inst : DecidableEq α] {R : Type u_2} [inst_1 : AddCommGroup R] [NoZeroSMulDivisors ℕ R]
  (A X : Finset α),
  X ⊆ A →
    ∀ (sign : α → R) (f : ↥X → ↥X),
      Function.Bijective f → (∀ (I : ↥X), sign ↑(f I) = -sign ↑I) → ∑ I ∈ A, sign I = ∑ I ∈ A \ X, sign I

Docstring: **Cancellation Principle, Take 1** (lem.sign.cancel1)

Let `A` be a finite set, `X ⊆ A`, and `sign : A → R` where `R` is an additive group
with no 2-torsion (i.e., `2a = 0 → a = 0`). If `f : X → X` is a bijection satisfying
`sign(f(I)) = -sign(I)` for all `I ∈ X`, then `∑_{I ∈ A} sign(I) = ∑_{I ∈ A \ X} sign(I)`.

This version requires `R` to have no 2-torsion (e.g., `R = ℤ`, `ℚ`, `ℝ`).


## BASE-LIBRARY REF DecidableEq
Sort u → Sort (max 1 u)

Docstring: Propositional equality is `Decidable` for all elements of a type.

In other words, an instance of `DecidableEq α` is a means of deciding the proposition `a = b` is
for all `a b : α`.


## BASE-LIBRARY REF AddCommGroup
Type u → Type u

Docstring: An additive commutative group is an additive group with commutative `(+)`. 

## BASE-LIBRARY REF NoZeroSMulDivisors
(R : Type u_4) → (M : Type u_5) → [Zero R] → [Zero M] → [SMul R M] → Prop

Docstring: `NoZeroSMulDivisors R M` states that a scalar multiple is `0` only if either argument is `0`.
This is a version of saying that `M` is torsion free, without assuming `R` is zero-divisor free.

The main application of `NoZeroSMulDivisors R M`, when `M` is a module,
is the result `smul_eq_zero`: a scalar multiple is `0` iff either argument is `0`.

It is a generalization of the `NoZeroDivisors` class to heterogeneous multiplication.


## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF MulZeroClass.toZero
{M₀ : Type u} → [self : MulZeroClass M₀] → Zero M₀

## BASE-LIBRARY REF Nat.instMulZeroClass
MulZeroClass ℕ

## BASE-LIBRARY REF NegZeroClass.toZero
{G : Type u_2} → [self : NegZeroClass G] → Zero G

## BASE-LIBRARY REF SubNegZeroMonoid.toNegZeroClass
{G : Type u_2} → [self : SubNegZeroMonoid G] → NegZeroClass G

## BASE-LIBRARY REF SubtractionMonoid.toSubNegZeroMonoid
{α : Type u_1} → [SubtractionMonoid α] → SubNegZeroMonoid α

## BASE-LIBRARY REF SubtractionCommMonoid.toSubtractionMonoid
{G : Type u} → [self : SubtractionCommMonoid G] → SubtractionMonoid G

## BASE-LIBRARY REF AddCommGroup.toDivisionAddCommMonoid
{G : Type u_1} → [AddCommGroup G] → SubtractionCommMonoid G

## BASE-LIBRARY REF AddMonoid.toNatSMul
{M : Type u_2} → [AddMonoid M] → SMul ℕ M

## BASE-LIBRARY REF SubNegMonoid.toAddMonoid
{G : Type u} → [self : SubNegMonoid G] → AddMonoid G

## BASE-LIBRARY REF AddGroup.toSubNegMonoid
{A : Type u} → [self : AddGroup A] → SubNegMonoid A

## BASE-LIBRARY REF AddCommGroup.toAddGroup
{G : Type u} → [self : AddCommGroup G] → AddGroup G

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

## BASE-LIBRARY REF Function.Bijective
{α : Sort u₁} → {β : Sort u₂} → (α → β) → Prop

Docstring: A function is called bijective if it is both injective and surjective. 

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
Cancellation principle, take 1

Let $\mathcal{A}$ be a finite set. Let $\mathcal{X}$ be a subset of $\mathcal{A}$. 

For each $I \in \mathcal{A}$, let $\operatorname {sign} I$ be an element of an additive abelian group $R$ with no $2$-torsion (i.e., $2a = 0$ implies $a = 0$). Let $f : \mathcal{X} \to \mathcal{X}$ be a bijection with the property that 

\[  \operatorname {sign}(f(I)) = -\operatorname {sign} I \qquad \text{for all } I \in \mathcal{X}.  \]

 (Such a bijection $f$ is called \emph{sign-reversing}.) Then, 

\[  \sum _{I \in \mathcal{A}} \operatorname {sign} I = \sum _{I \in \mathcal{A} \setminus \mathcal{X}} \operatorname {sign} I.  \]

## VERDICT
{
  "verdict": "drift",
  "justification": "The blueprint requires only that `R` have \u201cno 2-torsion (i.e., `2a = 0` implies `a = 0`)\u201d, whereas the elaborated signature assumes `[NoZeroSMulDivisors \u2115 R]`. By its supplied definition/docstring, this requires every natural scalar multiple to be zero only when the scalar or element is zero, so it rules out all natural-number torsion, not merely 2-torsion. This is a mathematically stronger, added typeclass hypothesis and therefore makes the theorem weaker than the blueprint. The difference enters through the target binder `[NoZeroSMulDivisors \u2115 R]`; it should be replaced by an explicit assumption such as `\u2200 a : R, 2 \u2022 a = 0 \u2192 a = 0` (or an exactly equivalent no-2-torsion class). The other differences are harmless: `[DecidableEq \u03b1]` supports finite-set operations, and taking `sign : \u03b1 \u2192 R` rather than only on `A` is representational because the conclusion and hypothesis use it only on elements of `A` or `X \u2286 A`."
}