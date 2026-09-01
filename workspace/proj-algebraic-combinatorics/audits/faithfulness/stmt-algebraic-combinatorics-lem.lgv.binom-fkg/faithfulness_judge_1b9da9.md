## TARGET LGV.binom_2x2_ineq (theorem) — ELABORATED SIGNATURE
∀ (a b c d : ℕ), b ≤ a → d ≤ c → ↑(a.choose d) * ↑(b.choose c) ≤ ↑(a.choose c) * ↑(b.choose d)

Docstring: The FKG inequality for binomial coefficients:
C(a,c) * C(b,d) ≥ C(a,d) * C(b,c) when a ≥ b and c ≥ d.

This handles all cases including when some choose values are zero. 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF LE.le
{α : Type u} → [self : LE α] → α → α → Prop

Docstring: The less-equal relation: `x ≤ y` 

Conventions for notations in identifiers:

 * The recommended spelling of `≤` in identifiers is `le`.

 * The recommended spelling of `<=` in identifiers is `le` (prefer `≤` over `<=`).

## BASE-LIBRARY REF instLENat
LE ℕ

## BASE-LIBRARY REF Int
Type

Docstring: The integers.

This type is special-cased by the compiler and overridden with an efficient implementation. The
runtime has a special representation for `Int` that stores “small” signed numbers directly, while
larger numbers use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)). A “small number” is an integer that can be encoded with one fewer bits
than the platform's pointer size (i.e. 63 bits on 64-bit architectures and 31 bits on 32-bit
architectures).


## BASE-LIBRARY REF Int.instLEInt
LE ℤ

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

## BASE-LIBRARY REF Nat.choose
ℕ → ℕ → ℕ

Docstring: `choose n k` is the number of `k`-element subsets in an `n`-element set. Also known as binomial
coefficients. For the fact that this is the number of `k`-element-subsets of an `n`-element
set, see `Finset.card_powersetCard`. 

## INFORMAL STATEMENT
FKG inequality for binomial coefficients

\leanhelper  Let $a, b, c, d$ be nonnegative integers with $a \ge b$ and $c \ge d$. Then 

\[  \binom {a}{d} \binom {b}{c} \le \binom {a}{c} \binom {b}{d}.  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.binom.binom
def.binom.binom

For any numbers $n$ and $k$, we set

\begin{equation}  \binom {n}{k}=\begin{cases}  \frac{n\left( n-1\right) \left( n-2\right) \cdots \left( n-k+1\right) }{k!}, &  \text{if }k\in \mathbb {N};\\ 0, &  \text{else.}\end{cases} \end{equation}

 Note that “numbers” is to be understood fairly liberally here. In particular, $n$ can be any integer, rational, real or complex number (or, more generally, any element in a $\mathbb {Q}$-algebra), whereas $k$ can be anything (although the only nonzero values of $\binom {n}{k}$ will be achieved for $k\in \mathbb {N}$, by the above definition).

## VERDICT
{
  "verdict": "faithful",
  "justification": "The blueprint quantifies over \u201cnonnegative integers\u201d and assumes \u201ca \u2265 b and c \u2265 d\u201d; the Lean binders `\u2200 (a b c d : \u2115), b \u2264 a \u2192 d \u2264 c \u2192` encode exactly those domains and inequalities. Its conclusion `\u2191(a.choose d) * \u2191(b.choose c) \u2264 \u2191(a.choose c) * \u2191(b.choose d)` is precisely `binom(a,d) binom(b,c) \u2264 binom(a,c) binom(b,d)`. By the supplied docstring, `Nat.choose n k` is the binomial coefficient, including the zero cases, and the casts into `\u2124` preserve the intended integer-valued comparison. Thus the formal and informal statements agree."
}