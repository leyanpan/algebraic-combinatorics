## TARGET AlgebraicCombinatorics.FPS.factorial_dvd_prod_odd_mul_pow (theorem) — ELABORATED SIGNATURE
∀ (n : ℕ), n.factorial ∣ (∏ i ∈ Finset.range n, (2 * i + 1)) * 2 ^ n

Docstring: n! divides the product (1·3·5·...·(2n-1)) · 2^n. 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF Dvd.dvd
{α : Type u_1} → [self : Dvd α] → α → α → Prop

Docstring: Divisibility. `a ∣ b` (typed as `\|`) means that there is some `c` such that `b = a * c`. 

Conventions for notations in identifiers:

 * The recommended spelling of `∣` in identifiers is `dvd`.

## BASE-LIBRARY REF Nat.instDvd
Dvd ℕ

Docstring: Divisibility of natural numbers. `a ∣ b` (typed as `\|`) says that
there is some `c` such that `b = a * c`.


## BASE-LIBRARY REF Nat.factorial
ℕ → ℕ

Docstring: `Nat.factorial n` is the factorial of `n`. 

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

## BASE-LIBRARY REF Finset.prod
{ι : Type u_1} → {M : Type u_3} → [CommMonoid M] → Finset ι → (ι → M) → M

Docstring: `∏ x ∈ s, f x` is the product of `f x` as `x` ranges over the elements of the finite set `s`.

When the index type is a `Fintype`, the notation `∏ x, f x`, is a shorthand for
`∏ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF Nat.instCommMonoid
CommMonoid ℕ

## BASE-LIBRARY REF Finset.range
ℕ → Finset ℕ

Docstring: `range n` is the set of natural numbers less than `n`. 

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

## INFORMAL STATEMENT
lem.binom.factorial_dvd_prod_odd_mul_pow

\leanhelper  For any $n\in \mathbb {N}$, $n!$ divides $\left(\prod _{i=0}^{n-1}(2i+1)\right)\cdot 2^n$.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The formal binder `\u2200 (n : \u2115)` exactly matches \u201cfor any $n\\in\\mathbb N$.\u201d By `Finset.range n`, the product `\u220f i \u2208 Finset.range n, (2 * i + 1)` ranges over precisely the natural numbers $i<n$, i.e. $i=0,\\ldots,n-1$. Thus the conclusion `n.factorial \u2223 (\u220f i \u2208 Finset.range n, (2 * i + 1)) * 2 ^ n` is exactly the asserted divisibility $n!\\mid\\left(\\prod_{i=0}^{n-1}(2i+1)\\right)2^n$, with no added hypotheses or restricted quantifiers."
}