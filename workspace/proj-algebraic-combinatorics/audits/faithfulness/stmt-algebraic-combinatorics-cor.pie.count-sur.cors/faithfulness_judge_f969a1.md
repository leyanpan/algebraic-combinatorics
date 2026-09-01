## TARGET AlgebraicCombinatorics.InclusionExclusion.surjOn_alternating_sum_dvd_factorial (theorem) — ELABORATED SIGNATURE
∀ (m n : ℕ), ↑n.factorial ∣ ∑ k ∈ Finset.range (n + 1), (-1) ^ k * ↑(n.choose k) * (↑n - ↑k) ^ m

Docstring: **Corollary `cor.pie.count-sur.cors` (d)**: The alternating sum is divisible by `n!`.
This follows from the orbit-stabilizer theorem applied to the action of `Sₙ` on surjections. 

## TARGET AlgebraicCombinatorics.InclusionExclusion.surjOn_alternating_sum_eq_factorial (theorem) — ELABORATED SIGNATURE
∀ (n : ℕ), ∑ k ∈ Finset.range (n + 1), (-1) ^ k * ↑(n.choose k) * (↑n - ↑k) ^ n = ↑n.factorial

Docstring: **Corollary `cor.pie.count-sur.cors` (b)**: When `m = n`, the number of surjections
equals `n!` (the surjections are precisely the permutations). 

## TARGET AlgebraicCombinatorics.InclusionExclusion.surjOn_alternating_sum_eq_zero (theorem) — ELABORATED SIGNATURE
∀ (n m : ℕ), m < n → ∑ k ∈ Finset.range (n + 1), (-1) ^ k * ↑(n.choose k) * (↑n - ↑k) ^ m = 0

Docstring: **Corollary `cor.pie.count-sur.cors` (a)**: When `m < n`, there are no surjections,
so the alternating sum equals 0. 

## TARGET AlgebraicCombinatorics.InclusionExclusion.surjOn_alternating_sum_nonneg (theorem) — ELABORATED SIGNATURE
∀ (m n : ℕ), 0 ≤ ∑ k ∈ Finset.range (n + 1), (-1) ^ k * ↑(n.choose k) * (↑n - ↑k) ^ m

Docstring: **Corollary `cor.pie.count-sur.cors` (c)**: The alternating sum is always nonnegative
since it counts surjections. 

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

## BASE-LIBRARY REF Int
Type

Docstring: The integers.

This type is special-cased by the compiler and overridden with an efficient implementation. The
runtime has a special representation for `Int` that stores “small” signed numbers directly, while
larger numbers use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)). A “small number” is an integer that can be encoded with one fewer bits
than the platform's pointer size (i.e. 63 bits on 64-bit architectures and 31 bits on 32-bit
architectures).


## BASE-LIBRARY REF Int.instDvd
Dvd ℤ

Docstring: Divisibility of integers. `a ∣ b` (typed as `\|`) says that
there is some `c` such that `b = a * c`.


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

## BASE-LIBRARY REF Nat.factorial
ℕ → ℕ

Docstring: `Nat.factorial n` is the factorial of `n`. 

## BASE-LIBRARY REF Finset.sum
{ι : Type u_1} → {M : Type u_3} → [AddCommMonoid M] → Finset ι → (ι → M) → M

Docstring: `∑ x ∈ s, f x` is the sum of `f x` as `x` ranges over the elements
of the finite set `s`.

When the index type is a `Fintype`, the notation `∑ x, f x`, is a shorthand for
`∑ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF Int.instAddCommMonoid
AddCommMonoid ℤ

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

## BASE-LIBRARY REF HMul.hMul
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HMul α β γ] → α → β → γ

Docstring: `a * b` computes the product of `a` and `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `*` in identifiers is `mul`.

## BASE-LIBRARY REF instHMul
{α : Type u_1} → [Mul α] → HMul α α α

## BASE-LIBRARY REF Int.instMul
Mul ℤ

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

## BASE-LIBRARY REF Int.instMonoid
Monoid ℤ

## BASE-LIBRARY REF Neg.neg
{α : Type u} → [self : Neg α] → α → α

Docstring: `-a` computes the negative or opposite of `a`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `-` in identifiers is `neg` (when used as a unary operator).

## BASE-LIBRARY REF Int.instNegInt
Neg ℤ

## BASE-LIBRARY REF instOfNat
{n : ℕ} → OfNat ℤ n

## BASE-LIBRARY REF Nat.choose
ℕ → ℕ → ℕ

Docstring: `choose n k` is the number of `k`-element subsets in an `n`-element set. Also known as binomial
coefficients. For the fact that this is the number of `k`-element-subsets of an `n`-element
set, see `Finset.card_powersetCard`. 

## BASE-LIBRARY REF HSub.hSub
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HSub α β γ] → α → β → γ

Docstring: `a - b` computes the difference of `a` and `b`.
The meaning of this notation is type-dependent.
* For natural numbers, this operator saturates at 0: `a - b = 0` when `a ≤ b`. 

Conventions for notations in identifiers:

 * The recommended spelling of `-` in identifiers is `sub` (when used as a binary operator).

## BASE-LIBRARY REF instHSub
{α : Type u_1} → [Sub α] → HSub α α α

## BASE-LIBRARY REF Int.instSub
Sub ℤ

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

## BASE-LIBRARY REF LT.lt
{α : Type u} → [self : LT α] → α → α → Prop

Docstring: The less-than relation: `x < y` 

Conventions for notations in identifiers:

 * The recommended spelling of `<` in identifiers is `lt`.

## BASE-LIBRARY REF instLTNat
LT ℕ

## BASE-LIBRARY REF LE.le
{α : Type u} → [self : LE α] → α → α → Prop

Docstring: The less-equal relation: `x ≤ y` 

Conventions for notations in identifiers:

 * The recommended spelling of `≤` in identifiers is `le`.

 * The recommended spelling of `<=` in identifiers is `le` (prefer `≤` over `<=`).

## BASE-LIBRARY REF Int.instLEInt
LE ℤ

## INFORMAL STATEMENT
cor.pie.count-sur.cors

Let $n \in \mathbb {N}$. Then: 

\textbf{(a)} We have $\sum _{k=0}^{n} (-1)^k \binom {n}{k} (n-k)^m = 0$ for any $m \in \mathbb {N}$ satisfying $m < n$. 

\textbf{(b)} We have $\sum _{k=0}^{n} (-1)^k \binom {n}{k} (n-k)^n = n!$. 

\textbf{(c)} We have $\sum _{k=0}^{n} (-1)^k \binom {n}{k} (n-k)^m \geq 0$ for each $m \in \mathbb {N}$. 

\textbf{(d)} We have $n! \mid \sum _{k=0}^{n} (-1)^k \binom {n}{k} (n-k)^m$ for each $m \in \mathbb {N}$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.binom.binom
def.binom.binom

For any numbers $n$ and $k$, we set

\begin{equation}  \binom {n}{k}=\begin{cases}  \frac{n\left( n-1\right) \left( n-2\right) \cdots \left( n-k+1\right) }{k!}, &  \text{if }k\in \mathbb {N};\\ 0, &  \text{else.}\end{cases} \end{equation}

 Note that “numbers” is to be understood fairly liberally here. In particular, $n$ can be any integer, rational, real or complex number (or, more generally, any element in a $\mathbb {Q}$-algebra), whereas $k$ can be anything (although the only nonzero values of $\binom {n}{k}$ will be achieved for $k\in \mathbb {N}$, by the above definition).

## VERDICT
{
  "verdict": "faithful",
  "justification": "All four declarations match the corresponding clauses, with the alternating sums interpreted in \u2124, as required by the signed factor `(-1)^k`. `Finset.range (n + 1)` indexes exactly `k = 0, \u2026, n`, and `Nat.choose n k` is the natural-number binomial coefficient. Clause (a) is represented by `\u2200 (n m : \u2115), m < n \u2192 \u2026 = 0`; clause (b) by `\u2200 (n : \u2115), \u2026 ^ n = \u2191n.factorial`; clause (c) by `\u2200 (m n : \u2115), 0 \u2264 \u2026`; and clause (d) by `\u2200 (m n : \u2115), \u2191n.factorial \u2223 \u2026`. Reordering the universally quantified `m` and `n` in (c) and (d) does not change the meaning. The casts `\u2191n`, `\u2191k`, `\u2191(n.choose k)`, and `\u2191n.factorial` consistently place subtraction, the sum, comparison, equality, and divisibility in the integers, faithfully encoding the informal signed sum."
}