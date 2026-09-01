## TARGET AlgebraicCombinatorics.FPS.binom_zero_left_pos (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_1} [inst : CommRing R] [inst_1 : BinomialRing R] [NatPowAssoc R] {k : ℕ}, 0 < k → Ring.choose 0 k = 0

Docstring: For $k > 0$, we have $\binom{0}{k} = 0$.

This follows from the definition: the product $0 \cdot (-1) \cdot (-2) \cdots$ has a factor of $0$. 

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

## BASE-LIBRARY REF Zero.toOfNat0
{α : Type u_1} → [Zero α] → OfNat α 0

## BASE-LIBRARY REF MulZeroClass.toZero
{M₀ : Type u} → [self : MulZeroClass M₀] → Zero M₀

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.toMulZeroClass
{α : Type u} → [self : NonUnitalNonAssocSemiring α] → MulZeroClass α

## INFORMAL STATEMENT
lem.binom.zero_left_pos

\leanhelper  For $k > 0$, we have $\binom {0}{k} = 0$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.binom.binom
def.binom.binom

For any numbers $n$ and $k$, we set

\begin{equation}  \binom {n}{k}=\begin{cases}  \frac{n\left( n-1\right) \left( n-2\right) \cdots \left( n-k+1\right) }{k!}, &  \text{if }k\in \mathbb {N};\\ 0, &  \text{else.}\end{cases} \end{equation}

 Note that “numbers” is to be understood fairly liberally here. In particular, $n$ can be any integer, rational, real or complex number (or, more generally, any element in a $\mathbb {Q}$-algebra), whereas $k$ can be anything (although the only nonzero values of $\binom {n}{k}$ will be achieved for $k\in \mathbb {N}$, by the above definition).

## VERDICT
{
  "verdict": "unstatable",
  "justification": "The blueprint definition explicitly allows the lower argument to be non-natural: \u201c$k$ can be anything,\u201d with $\\binom nk=0$ when $k\\notin\\mathbb N$. Thus \u201cFor $k>0$\u201d is not restricted to natural $k$. The target instead binds `{k : \u2115}` and asserts only `0 < k \u2192 Ring.choose 0 k = 0`. This narrowing enters through `Ring.choose` itself, whose signature ends in `R \u2192 \u2115 \u2192 R`; it cannot represent the blueprint\u2019s off-natural cases. A faithful statement would require a generalized binomial operation with an index type broad enough to include non-natural values, defined to be zero outside `\u2115`, and then quantify over all positive indices. The additional `CommRing`, `BinomialRing`, and `NatPowAssoc` structure does not repair this index mismatch."
}