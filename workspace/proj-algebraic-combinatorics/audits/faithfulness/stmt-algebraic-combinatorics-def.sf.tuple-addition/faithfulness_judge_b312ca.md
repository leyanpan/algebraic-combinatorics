## TARGET AlgebraicCombinatorics.addTuple (def) — ELABORATED SIGNATURE
{N : ℕ} → (Fin N → ℕ) → (Fin N → ℕ) → Fin N → ℕ

Body:
fun {N} α β => α + β

Docstring: Addition of N-tuples, defined entrywise. (def.sf.tuple-addition (b))
Note: This is definitionally equal to `(· + ·)` on `Fin N → ℕ` via Mathlib's Pi.instAdd. 

## TARGET AlgebraicCombinatorics.subTuple (def) — ELABORATED SIGNATURE
{N : ℕ} → (Fin N → ℕ) → (Fin N → ℕ) → Fin N → ℤ

Body:
fun {N} α β i => ↑(α i) - ↑(β i)

Docstring: Subtraction of N-tuples, defined entrywise. Note: result is in ℤ.
(def.sf.tuple-addition (b)) 

## TARGET AlgebraicCombinatorics.zeroTuple (def) — ELABORATED SIGNATURE
{N : ℕ} → Fin N → ℕ

Body:
fun {N} => 0

Docstring: The zero N-tuple (0, 0, ..., 0). (def.sf.tuple-addition (a))
Note: This is definitionally equal to `(0 : Fin N → ℕ)` via Mathlib's Pi.instZero. 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF Fin
ℕ → Type

Docstring: Natural numbers less than some upper bound.

In particular, a `Fin n` is a natural number `i` with the constraint that `i < n`. It is the
canonical type with `n` elements.


## BASE-LIBRARY REF HAdd.hAdd
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HAdd α β γ] → α → β → γ

Docstring: `a + b` computes the sum of `a` and `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `+` in identifiers is `add`.

## BASE-LIBRARY REF instHAdd
{α : Type u_1} → [Add α] → HAdd α α α

## BASE-LIBRARY REF Pi.instAdd
{ι : Type u_1} → {M : ι → Type u_5} → [(i : ι) → Add (M i)] → Add ((i : ι) → M i)

## BASE-LIBRARY REF instAddNat
Add ℕ

## BASE-LIBRARY REF Int
Type

Docstring: The integers.

This type is special-cased by the compiler and overridden with an efficient implementation. The
runtime has a special representation for `Int` that stores “small” signed numbers directly, while
larger numbers use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)). A “small number” is an integer that can be encoded with one fewer bits
than the platform's pointer size (i.e. 63 bits on 64-bit architectures and 31 bits on 32-bit
architectures).


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

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF Zero.toOfNat0
{α : Type u_1} → [Zero α] → OfNat α 0

## BASE-LIBRARY REF Pi.instZero
{ι : Type u_1} → {M : ι → Type u_5} → [(i : ι) → Zero (M i)] → Zero ((i : ι) → M i)

## BASE-LIBRARY REF MulZeroClass.toZero
{M₀ : Type u} → [self : MulZeroClass M₀] → Zero M₀

## BASE-LIBRARY REF Nat.instMulZeroClass
MulZeroClass ℕ

## INFORMAL STATEMENT
def.sf.tuple-addition

\textbf{(a)} We let $\mathbf{0}$ denote the $N$-tuple $\left( 0,0,\ldots ,0\right) \in \mathbb {N}^{N}$. 

\medskip 

\textbf{(b)} Let $\alpha =\left( \alpha _{1},\alpha _{2},\ldots ,\alpha _{N}\right) $ and $\beta =\left( \beta _{1},\beta _{2},\ldots ,\beta _{N}\right) $ be two $N$-tuples in $\mathbb {N}^{N}$. Then, we set

\begin{align*}  \alpha +\beta &  :=\left( \alpha _{1}+\beta _{1},\alpha _{2}+\beta _{2},\ldots ,\alpha _{N}+\beta _{N}\right) \  \  \  \  \  \  \  \  \  \  \text{and}\\ \alpha -\beta &  :=\left( \alpha _{1}-\beta _{1},\alpha _{2}-\beta _{2},\ldots ,\alpha _{N}-\beta _{N}\right) . \end{align*}

 Note that $\alpha +\beta \in \mathbb {N}^{N}$, whereas $\alpha -\beta \in \mathbb {Z}^{N}$.

## VERDICT
{
  "verdict": "faithful",
  "justification": "All three definitions match the blueprint entrywise. For (a), `zeroTuple : {N : \u2115} \u2192 Fin N \u2192 \u2115` with body `fun {N} => 0` is exactly the constant-zero element of `\u2115^N`, corresponding to \u201cthe N-tuple `(0,0,\u2026,0) \u2208 \u2115^N`.\u201d For (b), `addTuple : {N : \u2115} \u2192 (Fin N \u2192 \u2115) \u2192 (Fin N \u2192 \u2115) \u2192 Fin N \u2192 \u2115` has body `\u03b1 + \u03b2`; via `Pi.instAdd` and `instAddNat`, this is entrywise natural-number addition, exactly `(\u03b1\u1d62 + \u03b2\u1d62)`, with result in `\u2115^N`. Finally, `subTuple : {N : \u2115} \u2192 (Fin N \u2192 \u2115) \u2192 (Fin N \u2192 \u2115) \u2192 Fin N \u2192 \u2124` has body `fun ... i => \u2191(\u03b1 i) - \u2191(\u03b2 i)`, so subtraction is performed in `\u2124` after the canonical casts from `\u2115`, exactly implementing the statement that `\u03b1 \u2212 \u03b2` has entries `\u03b1\u1d62 \u2212 \u03b2\u1d62` and lies in `\u2124^N`. Representing N-tuples by functions `Fin N \u2192 _` faithfully supplies N indexed coordinates, without additional hypotheses or narrowed quantifiers."
}