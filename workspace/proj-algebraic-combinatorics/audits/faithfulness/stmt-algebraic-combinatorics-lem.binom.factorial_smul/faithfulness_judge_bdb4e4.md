## TARGET AlgebraicCombinatorics.FPS.binom_factorial_smul (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_1} [inst : CommRing R] [inst_1 : BinomialRing R] [NatPowAssoc R] (r : R) (n : ℕ),
  n.factorial • Ring.choose r n = (descPochhammer ℤ n).smeval r

Docstring: The binomial coefficient satisfies the factorial formula:
$$n! \cdot \binom{r}{n} = r(r-1)(r-2)\cdots(r-n+1)$$

This is `Ring.descPochhammer_eq_factorial_smul_choose` in Mathlib. 

## BASE-LIBRARY REF CommRing
Type u → Type u

Docstring: A commutative ring is a ring with commutative multiplication. 

## BASE-LIBRARY REF BinomialRing
(R : Type u_1) → [AddCommMonoid R] → [Pow R ℕ] → Type u_1

Docstring: A binomial ring is a ring for which ascending Pochhammer evaluations are uniquely divisible by
suitable factorials. We define this notion as a mixin for additive commutative monoids with natural
number powers, but retain the ring name. We introduce `Ring.multichoose` as the uniquely defined
quotient. 

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

## BASE-LIBRARY REF NatPowAssoc
(M : Type u_2) → [MulOneClass M] → [Pow M ℕ] → Prop

Docstring: A mixin for power-associative multiplication. 

## BASE-LIBRARY REF MulZeroOneClass.toMulOneClass
{M₀ : Type u} → [self : MulZeroOneClass M₀] → MulOneClass M₀

## BASE-LIBRARY REF NonAssocSemiring.toMulZeroOneClass
{α : Type u} → [self : NonAssocSemiring α] → MulZeroOneClass α

## BASE-LIBRARY REF Semiring.toNonAssocSemiring
{α : Type u} → [self : Semiring α] → NonAssocSemiring α

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

## BASE-LIBRARY REF HSMul.hSMul
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HSMul α β γ] → α → β → γ

Docstring: `a • b` computes the product of `a` and `b`.
The meaning of this notation is type-dependent, but it is intended to be used for left actions. 

Conventions for notations in identifiers:

 * The recommended spelling of `•` in identifiers is `smul`.

## BASE-LIBRARY REF instHSMul
{α : Type u_1} → {β : Type u_2} → [SMul α β] → HSMul α β β

## BASE-LIBRARY REF AddMonoid.toNatSMul
{M : Type u_2} → [AddMonoid M] → SMul ℕ M

## BASE-LIBRARY REF AddMonoidWithOne.toAddMonoid
{R : Type u_2} → [self : AddMonoidWithOne R] → AddMonoid R

## BASE-LIBRARY REF AddGroupWithOne.toAddMonoidWithOne
{R : Type u} → [self : AddGroupWithOne R] → AddMonoidWithOne R

## BASE-LIBRARY REF Ring.toAddGroupWithOne
{R : Type u} → [self : Ring R] → AddGroupWithOne R

## BASE-LIBRARY REF CommRing.toRing
{α : Type u} → [self : CommRing α] → Ring α

## BASE-LIBRARY REF Nat.factorial
ℕ → ℕ

Docstring: `Nat.factorial n` is the factorial of `n`. 

## BASE-LIBRARY REF Ring.choose
{R : Type u_1} → [inst : AddCommGroupWithOne R] → [inst_1 : Pow R ℕ] → [BinomialRing R] → R → ℕ → R

Docstring: The binomial coefficient `choose r n` generalizes the natural number `Nat.choose` function,
interpreted in terms of choosing without replacement. 

## BASE-LIBRARY REF NonAssocRing.toAddCommGroupWithOne
{α : Type u_1} → [self : NonAssocRing α] → AddCommGroupWithOne α

## BASE-LIBRARY REF NonAssocCommRing.toNonAssocRing
{α : Type u} → [self : NonAssocCommRing α] → NonAssocRing α

## BASE-LIBRARY REF CommRing.toNonAssocCommRing
{α : Type u} → [CommRing α] → NonAssocCommRing α

## BASE-LIBRARY REF Polynomial.smeval
{R : Type u_3} →
  [inst : Semiring R] →
    Polynomial R → {S : Type u_4} → [inst_1 : AddCommMonoid S] → [Pow S ℕ] → [MulActionWithZero R S] → S → S

Docstring: Evaluate a polynomial `p` in the scalar semiring `R` at an element `x` in the target `S` using
scalar multiple `R`-action. 

## BASE-LIBRARY REF Int
Type

Docstring: The integers.

This type is special-cased by the compiler and overridden with an efficient implementation. The
runtime has a special representation for `Int` that stores “small” signed numbers directly, while
larger numbers use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)). A “small number” is an integer that can be encoded with one fewer bits
than the platform's pointer size (i.e. 63 bits on 64-bit architectures and 31 bits on 32-bit
architectures).


## BASE-LIBRARY REF Ring.toSemiring
{R : Type u} → [self : Ring R] → Semiring R

## BASE-LIBRARY REF Int.instRing
Ring ℤ

## BASE-LIBRARY REF descPochhammer
(R : Type u) → [inst : Ring R] → ℕ → Polynomial R

Docstring: `descPochhammer R n` is the polynomial `X * (X - 1) * ... * (X - n + 1)`,
with coefficients in the ring `R`.


## BASE-LIBRARY REF Module.toMulActionWithZero
{R : Type u_5} →
  {M : Type u_6} → {x : Semiring R} → {x_1 : AddCommMonoid M} → [_root_.Module R M] → MulActionWithZero R M

Docstring: A module over a semiring automatically inherits a `MulActionWithZero` structure. 

## BASE-LIBRARY REF AddCommGroup.toIntModule
(M : Type u_3) → [inst : AddCommGroup M] → _root_.Module ℤ M

## BASE-LIBRARY REF LieRing.toAddCommGroup
{L : Type v} → [self : LieRing L] → AddCommGroup L

## BASE-LIBRARY REF LieRing.ofAssociativeRing
{A : Type v} → [Ring A] → LieRing A

Docstring: An associative ring gives rise to a Lie ring by taking the bracket to be the ring commutator. 

## INFORMAL STATEMENT
lem.binom.factorial_smul

\leanhelper  For any element $r$ in a binomial ring and $n \in \mathbb {N}$, $n! \cdot \binom {r}{n} = r(r-1)(r-2)\cdots (r-n+1)$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.binom.binom
def.binom.binom

For any numbers $n$ and $k$, we set

\begin{equation}  \binom {n}{k}=\begin{cases}  \frac{n\left( n-1\right) \left( n-2\right) \cdots \left( n-k+1\right) }{k!}, &  \text{if }k\in \mathbb {N};\\ 0, &  \text{else.}\end{cases} \end{equation}

 Note that “numbers” is to be understood fairly liberally here. In particular, $n$ can be any integer, rational, real or complex number (or, more generally, any element in a $\mathbb {Q}$-algebra), whereas $k$ can be anything (although the only nonzero values of $\binom {n}{k}$ will be achieved for $k\in \mathbb {N}$, by the above definition).

## VERDICT
{
  "verdict": "faithful",
  "justification": "The formal conclusion exactly matches the blueprint: `n.factorial \u2022 Ring.choose r n = (descPochhammer \u2124 n).smeval r` expresses `n! \u00b7 binom r n = r(r-1)\u2026(r-n+1)`, since `Ring.choose` is the generalized binomial coefficient and `descPochhammer` is documented as `X * (X - 1) * ... * (X - n + 1)`. The binders `(r : R) (n : \u2115)` match \u201cany element `r` \u2026 and `n \u2208 \u2115`.\u201d The assumptions `[CommRing R] [BinomialRing R]` encode the stated setting of a binomial ring: `BinomialRing` is formally only a mixin over an additive commutative monoid with powers, so the separate `CommRing` binder supplies the actual ring structure implicit in the informal term. Likewise `[NatPowAssoc R]` ensures that the power operation used by that mixin has the ordinary repeated-multiplication behavior; for the standard powers intended by the informal products, this is a formal compatibility condition rather than a substantive narrowing."
}