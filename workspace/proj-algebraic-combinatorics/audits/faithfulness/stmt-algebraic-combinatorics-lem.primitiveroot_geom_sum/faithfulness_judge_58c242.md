## TARGET AlgebraicCombinatorics.SignedCounting.primitiveRoot_geom_sum_eq_zero (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] [IsDomain K] {ω : K} {d : ℕ},
  IsPrimitiveRoot ω d → 1 < d → ∑ i ∈ Finset.range d, ω ^ i = 0

Docstring: **Geometric sum of primitive roots** (used in the discrete Fourier transform)

If `ω` is a primitive d-th root of unity with `d > 1`, then
`1 + ω + ω² + ... + ω^{d-1} = 0`.

This is the key identity that enables cancellation in sums involving roots of unity.
It generalizes `1 + (-1) = 0` (the case `d = 2`).

This is `IsPrimitiveRoot.geom_sum_eq_zero` from Mathlib, included here for documentation. 

## BASE-LIBRARY REF CommRing
Type u → Type u

Docstring: A commutative ring is a ring with commutative multiplication. 

## BASE-LIBRARY REF IsDomain
(α : Type u) → [Semiring α] → Prop

Docstring: A domain is a nontrivial semiring such that multiplication by a nonzero element
is cancellative on both sides. In other words, a nontrivial semiring `R` satisfying
`∀ {a b c : R}, a ≠ 0 → a * b = a * c → b = c` and
`∀ {a b c : R}, b ≠ 0 → a * b = c * b → a = c`.

This is implemented as a mixin for `Semiring α`.
To obtain an integral domain use `[CommRing α] [IsDomain α]`. 

## BASE-LIBRARY REF CommSemiring.toSemiring
{R : Type u} → [self : CommSemiring R] → Semiring R

## BASE-LIBRARY REF CommRing.toCommSemiring
{α : Type u} → [s : CommRing α] → CommSemiring α

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF IsPrimitiveRoot
{M : Type u_1} → [CommMonoid M] → M → ℕ → Prop

Docstring: An element `ζ` is a primitive `k`-th root of unity if `ζ ^ k = 1`,
and if `l` satisfies `ζ ^ l = 1` then `k ∣ l`. 

## BASE-LIBRARY REF CommRing.toCommMonoid
{α : Type u} → [self : CommRing α] → CommMonoid α

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

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.toAddCommMonoid
{α : Type u} → [self : NonUnitalNonAssocSemiring α] → AddCommMonoid α

## BASE-LIBRARY REF NonUnitalNonAssocRing.toNonUnitalNonAssocSemiring
{α : Type u} → [self : NonUnitalNonAssocRing α] → NonUnitalNonAssocSemiring α

## BASE-LIBRARY REF NonUnitalNonAssocCommRing.toNonUnitalNonAssocRing
{α : Type u} → [self : NonUnitalNonAssocCommRing α] → NonUnitalNonAssocRing α

## BASE-LIBRARY REF NonUnitalCommRing.toNonUnitalNonAssocCommRing
{α : Type u} → [self : NonUnitalCommRing α] → NonUnitalNonAssocCommRing α

## BASE-LIBRARY REF CommRing.toNonUnitalCommRing
{α : Type u} → [s : CommRing α] → NonUnitalCommRing α

## BASE-LIBRARY REF Finset.range
ℕ → Finset ℕ

Docstring: `range n` is the set of natural numbers less than `n`. 

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

## BASE-LIBRARY REF Zero.toOfNat0
{α : Type u_1} → [Zero α] → OfNat α 0

## BASE-LIBRARY REF MulZeroClass.toZero
{M₀ : Type u} → [self : MulZeroClass M₀] → Zero M₀

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.toMulZeroClass
{α : Type u} → [self : NonUnitalNonAssocSemiring α] → MulZeroClass α

## INFORMAL STATEMENT
lem.primitiveRoot_geom_sum

\leanhelper  If $\omega $ is a primitive $d$-th root of unity with $d > 1$, then 

\[  1 + \omega + \omega ^2 + \cdots + \omega ^{d-1} = 0.  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.root-of-unity.prim
def.root-of-unity.prim

Let $K$ be a field. Let $d$ be a positive integer. 

\textbf{(a)} A \emph{$d$-th root of unity} in $K$ means an element $\omega $ of $K$ satisfying $\omega ^d = 1$. 

\textbf{(b)} A \emph{primitive $d$-th root of unity} in $K$ means an element $\omega $ of $K$ satisfying $\omega ^d = 1$ but $\omega ^i \neq 1$ for each $i \in \{ 1, 2, \ldots , d-1\} $. In other words, a primitive $d$-th root of unity in $K$ means an element of the multiplicative group $K^{\times }$ whose order is $d$.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The target assumes `IsPrimitiveRoot \u03c9 d \u2192 1 < d` and concludes `\u2211 i \u2208 Finset.range d, \u03c9 ^ i = 0`. By `Finset.range`, the indices are exactly `0, \u2026, d-1`, so this sum is `1 + \u03c9 + \u03c9\u00b2 + \u22ef + \u03c9^(d-1)`, matching the blueprint. The base-library `IsPrimitiveRoot` definition\u2014`\u03c9 ^ d = 1` and every `l` with `\u03c9 ^ l = 1` is divisible by `d`\u2014expresses that the multiplicative order is `d`, matching the informal primitive-root definition under `1 < d`. The binders `[CommRing K] [IsDomain K]` allow any commutative integral domain, whereas the informal definition says \u201cLet `K` be a field\u201d; this is a genuine generalization to a wider class, not an added restriction, so the Lean theorem implies the blueprint statement."
}