## TARGET AlgebraicCombinatorics.DoublyInfinitePowerSeries.coeff_eq_single_contrib (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : Semiring K] (f : AlgebraicCombinatorics.DoublyInfinitePowerSeries K) (m : ℤ),
  f.coeff m = f.coeff m * (AlgebraicCombinatorics.DoublyInfinitePowerSeries.single m).coeff m

Docstring: The representation f = ∑_{n∈ℤ} (coeff f n) · x^n holds pointwise:
at position m, f m = (coeff f m) · 1 + ∑_{n≠m} (coeff f n) · 0 = coeff f m. 

## TARGET AlgebraicCombinatorics.DoublyInfinitePowerSeries.eq_coeff_at_position (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : Semiring K] (f : AlgebraicCombinatorics.DoublyInfinitePowerSeries K) (m : ℤ), f m = f.coeff m

Docstring: Any doubly infinite power series f equals (coeff f n) at position n.
This is the pointwise characterization of the notation ∑_{n∈ℤ} a_n x^n:
at each position m, the coefficient is a_m.

This formalizes the representation mentioned at the end of Definition `def.fps.laure.double`:
"we will later use the notation ∑_{n∈ℤ} a_n x^n for a family (a_n)_{n∈ℤ}".

Note: This is a formal identity of families. The "sum" is well-defined because
at each coefficient position m, only the term n = m contributes. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.DoublyInfinitePowerSeries (def)
(K : Type u_1) → [Semiring K] → Type u_1

Body:
fun K [Semiring K] => ℤ → K

Docstring: The K-module of doubly infinite power series K[[x^±]].

An element is a family `(a_n)_{n ∈ ℤ}` of elements of K. Addition and scalar
multiplication are defined entrywise.

Note: This is NOT a ring because multiplication is not always well-defined
(the convolution sum may be infinite).

This corresponds to Definition `def.fps.laure.double`.


## PROJECT DEPENDENCY AlgebraicCombinatorics.DoublyInfinitePowerSeries.coeff (def)
{K : Type u_1} → [inst : Semiring K] → AlgebraicCombinatorics.DoublyInfinitePowerSeries K → ℤ → K

Body:
fun {K} [Semiring K] f n => f n

Docstring: The coefficient of x^n in a doubly infinite power series 

## PROJECT DEPENDENCY AlgebraicCombinatorics.DoublyInfinitePowerSeries.single (def)
{K : Type u_1} → [inst : Semiring K] → ℤ → AlgebraicCombinatorics.DoublyInfinitePowerSeries K

Body:
fun {K} [Semiring K] n m => if m = n then 1 else 0

Docstring: The element x^n in K[[x^±]], represented as a family 

## BASE-LIBRARY REF Semiring
Type u → Type u

Docstring: A `Semiring` is a type with addition, multiplication, a `0` and a `1` where addition is
commutative and associative, multiplication is associative and left and right distributive over
addition, and `0` and `1` are additive and multiplicative identities. 

## BASE-LIBRARY REF Int
Type

Docstring: The integers.

This type is special-cased by the compiler and overridden with an efficient implementation. The
runtime has a special representation for `Int` that stores “small” signed numbers directly, while
larger numbers use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)). A “small number” is an integer that can be encoded with one fewer bits
than the platform's pointer size (i.e. 63 bits on 64-bit architectures and 31 bits on 32-bit
architectures).


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

## BASE-LIBRARY REF HMul.hMul
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HMul α β γ] → α → β → γ

Docstring: `a * b` computes the product of `a` and `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `*` in identifiers is `mul`.

## BASE-LIBRARY REF instHMul
{α : Type u_1} → [Mul α] → HMul α α α

## BASE-LIBRARY REF Distrib.toMul
{R : Type u_1} → [self : Distrib R] → Mul R

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.toDistrib
{α : Type u} → [self : NonUnitalNonAssocSemiring α] → Distrib α

## BASE-LIBRARY REF NonAssocSemiring.toNonUnitalNonAssocSemiring
{α : Type u} → [self : NonAssocSemiring α] → NonUnitalNonAssocSemiring α

## BASE-LIBRARY REF Semiring.toNonAssocSemiring
{α : Type u} → [self : Semiring α] → NonAssocSemiring α

## BASE-LIBRARY REF ite
{α : Sort u} → (c : Prop) → [h : Decidable c] → α → α → α

Docstring: `if c then t else e` is notation for `ite c t e`, "if-then-else", which decides to
return `t` or `e` depending on whether `c` is true or false. The explicit argument
`c : Prop` does not have any actual computational content, but there is an additional
`[Decidable c]` argument synthesized by typeclass inference which actually
determines how to evaluate `c` to true or false. Write `if h : c then t else e`
instead for a "dependent if-then-else" `dite`, which allows `t`/`e` to use the fact
that `c` is true/false.


## BASE-LIBRARY REF Int.instDecidableEq
DecidableEq ℤ

Docstring: Decides whether two integers are equal. Usually accessed via the `DecidableEq Int` instance.

This function is overridden by the compiler with an efficient implementation. This definition is the
logical model.

Examples:
* `show (7 : Int) = (3 : Int) + (4 : Int) by decide`
* `if (6 : Int) = (3 : Int) * (2 : Int) then "yes" else "no" = "yes"`
* `(¬ (6 : Int) = (3 : Int)) = true`


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

## BASE-LIBRARY REF AddCommMonoidWithOne.toAddMonoidWithOne
{R : Type u_2} → [self : AddCommMonoidWithOne R] → AddMonoidWithOne R

## BASE-LIBRARY REF NonAssocSemiring.toAddCommMonoidWithOne
{α : Type u} → [self : NonAssocSemiring α] → AddCommMonoidWithOne α

## BASE-LIBRARY REF Zero.toOfNat0
{α : Type u_1} → [Zero α] → OfNat α 0

## BASE-LIBRARY REF MulZeroClass.toZero
{M₀ : Type u} → [self : MulZeroClass M₀] → Zero M₀

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.toMulZeroClass
{α : Type u} → [self : NonUnitalNonAssocSemiring α] → MulZeroClass α

## INFORMAL STATEMENT
Coefficient decomposition of doubly infinite power series

\leanhelper  For any $f = (a_n) \in K[\! [x^{\pm }]\! ]$ and $m \in \mathbb {Z}$, $f$ evaluated at position $m$ gives $a_m$. Equivalently, the coefficient of $f$ at $m$ equals the scalar by which $f$ scales the $m$-th basis vector $(\delta _{n,m})_{n \in \mathbb {Z}}$.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The first target states exactly the pointwise claim: `\u2200 ... (f) (m : \u2124), f m = f.coeff m`. Since `DoublyInfinitePowerSeries K` is defined as `\u2124 \u2192 K` and `coeff` has body `fun f n => f n`, this is precisely the blueprint\u2019s \u201cfor any `f = (a_n)` ... `f` evaluated at position `m` gives `a_m`.\u201d The second target states `f.coeff m = f.coeff m * (single m).coeff m`; unfolding `single`, its coefficient at `m` is `if m = m then 1 else 0 = 1`, so the right-hand side is the contribution `a_m \u00b7 \u03b4_{m,m} = a_m` of the `m`-th basis vector, matching the stated equivalent coefficient decomposition. The `[Semiring K]` binder comes from the project definition of `DoublyInfinitePowerSeries K` and supplies the multiplication, zero, and one needed to express this basis-vector contribution; it fixes the formal coefficient setting rather than adding an unrelated hypothesis."
}