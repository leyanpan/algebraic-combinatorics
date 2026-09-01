## TARGET AlgebraicCombinatorics.SignedCounting.IsRootOfUnity (def) — ELABORATED SIGNATURE
{K : Type u_1} → [CommRing K] → K → ℕ → Prop

Body:
fun {K} [CommRing K] ω d => ω ^ d = 1

Docstring: An element `ω` is a *d-th root of unity* if `ω^d = 1`. (def.root-of-unity.prim (a))

This is the condition for membership in `rootsOfUnity d K` when `ω` is a unit.
For fields, we can state this directly without the unit requirement. 

## BASE-LIBRARY REF CommRing
Type u → Type u

Docstring: A commutative ring is a ring with commutative multiplication. 

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

## BASE-LIBRARY REF MonoidWithZero.toMonoid
{M₀ : Type u} → [self : MonoidWithZero M₀] → Monoid M₀

## BASE-LIBRARY REF Semiring.toMonoidWithZero
{α : Type u} → [self : Semiring α] → MonoidWithZero α

## BASE-LIBRARY REF CommSemiring.toSemiring
{R : Type u} → [self : CommSemiring R] → Semiring R

## BASE-LIBRARY REF CommRing.toCommSemiring
{α : Type u} → [s : CommRing α] → CommSemiring α

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF One.toOfNat1
{α : Type u_1} → [One α] → OfNat α 1

## BASE-LIBRARY REF AddMonoidWithOne.toOne
{R : Type u_2} → [self : AddMonoidWithOne R] → One R

## BASE-LIBRARY REF AddGroupWithOne.toAddMonoidWithOne
{R : Type u} → [self : AddGroupWithOne R] → AddMonoidWithOne R

## BASE-LIBRARY REF Ring.toAddGroupWithOne
{R : Type u} → [self : Ring R] → AddGroupWithOne R

## BASE-LIBRARY REF CommRing.toRing
{α : Type u} → [self : CommRing α] → Ring α

## INFORMAL STATEMENT
def.root-of-unity.prim

Let $K$ be a field. Let $d$ be a positive integer. 

\textbf{(a)} A \emph{$d$-th root of unity} in $K$ means an element $\omega $ of $K$ satisfying $\omega ^d = 1$. 

\textbf{(b)} A \emph{primitive $d$-th root of unity} in $K$ means an element $\omega $ of $K$ satisfying $\omega ^d = 1$ but $\omega ^i \neq 1$ for each $i \in \{ 1, 2, \ldots , d-1\} $. In other words, a primitive $d$-th root of unity in $K$ means an element of the multiplicative group $K^{\times }$ whose order is $d$.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The target formalizes part (a), as its docstring explicitly marks \u201c(def.root-of-unity.prim (a))\u201d. Its body, `fun {K} [CommRing K] \u03c9 d => \u03c9 ^ d = 1`, exactly matches the blueprint\u2019s definition: \u201can element \u03c9 of K satisfying \u03c9^d = 1.\u201d The formal binders are more general than the blueprint\u2019s \u201cLet K be a field\u201d and \u201cLet d be a positive integer\u201d: `[CommRing K]` is weaker than requiring a field, and `d : \u2115` also permits zero. These are genuine generalizations, not added restrictions, and the definition agrees on fields and positive `d`. Part (b) defines the separate notion of a primitive root and is not asserted by this `IsRootOfUnity` declaration."
}