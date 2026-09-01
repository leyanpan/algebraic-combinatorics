## TARGET AlgebraicCombinatorics.SubtractiveMethods.signProduct_eq_prod_pow (theorem) — ELABORATED SIGNATURE
∀ {n d : ℕ} (e : Fin d → ZMod 2) (x : Fin n → Fin d),
  AlgebraicCombinatorics.SubtractiveMethods.signProduct e x =
    ∏ k,
      AlgebraicCombinatorics.SubtractiveMethods.toSign (e k) ^
        AlgebraicCombinatorics.SubtractiveMethods.multiplicity x k

Docstring: The product can be rewritten in terms of multiplicities:
`∏_i e_{x_i} = ∏_k e_k^{m_k}` where `m_k` is the multiplicity of `k` in `x`.

Label: Equation `pf.lem.cancel.all-even.l2.e=e` 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SubtractiveMethods.signProduct (def)
{n d : ℕ} → (Fin d → ZMod 2) → (Fin n → Fin d) → ℤ

Body:
fun {n d} e x => ∏ i, AlgebraicCombinatorics.SubtractiveMethods.toSign (e (x i))

Docstring: The product `e_{x_1} * e_{x_2} * ... * e_{x_n}` for a sign tuple `e` and
index tuple `x` 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SubtractiveMethods.toSign (def)
ZMod 2 → ℤ

Body:
fun b => if b = 0 then 1 else -1

Docstring: Convert a ZMod 2 value to a sign: 0 ↦ 1, 1 ↦ -1 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SubtractiveMethods.multiplicity (def)
{n d : ℕ} → (Fin n → Fin d) → Fin d → ℕ

Body:
fun {n d} x k => {i | x i = k}.card

Docstring: The multiplicity of element `k` in tuple `x` 

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


## BASE-LIBRARY REF ZMod
ℕ → Type

Docstring: The integers modulo `n : ℕ`. 

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

## BASE-LIBRARY REF Int
Type

Docstring: The integers.

This type is special-cased by the compiler and overridden with an efficient implementation. The
runtime has a special representation for `Int` that stores “small” signed numbers directly, while
larger numbers use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)). A “small number” is an integer that can be encoded with one fewer bits
than the platform's pointer size (i.e. 63 bits on 64-bit architectures and 31 bits on 32-bit
architectures).


## BASE-LIBRARY REF Finset.prod
{ι : Type u_1} → {M : Type u_3} → [CommMonoid M] → Finset ι → (ι → M) → M

Docstring: `∏ x ∈ s, f x` is the product of `f x` as `x` ranges over the elements of the finite set `s`.

When the index type is a `Fintype`, the notation `∏ x, f x`, is a shorthand for
`∏ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF Int.instCommMonoid
CommMonoid ℤ

## BASE-LIBRARY REF Finset.univ
{α : Type u_1} → [Fintype α] → Finset α

Docstring: `univ` is the universal finite set of type `Finset α` implied from
the assumption `Fintype α`. 

## BASE-LIBRARY REF Fin.fintype
(n : ℕ) → Fintype (Fin n)

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

## BASE-LIBRARY REF ite
{α : Sort u} → (c : Prop) → [h : Decidable c] → α → α → α

Docstring: `if c then t else e` is notation for `ite c t e`, "if-then-else", which decides to
return `t` or `e` depending on whether `c` is true or false. The explicit argument
`c : Prop` does not have any actual computational content, but there is an additional
`[Decidable c]` argument synthesized by typeclass inference which actually
determines how to evaluate `c` to true or false. Write `if h : c then t else e`
instead for a "dependent if-then-else" `dite`, which allows `t`/`e` to use the fact
that `c` is true/false.


## BASE-LIBRARY REF Zero.toOfNat0
{α : Type u_1} → [Zero α] → OfNat α 0

## BASE-LIBRARY REF MulZeroClass.toZero
{M₀ : Type u} → [self : MulZeroClass M₀] → Zero M₀

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.toMulZeroClass
{α : Type u} → [self : NonUnitalNonAssocSemiring α] → MulZeroClass α

## BASE-LIBRARY REF NonUnitalNonAssocRing.toNonUnitalNonAssocSemiring
{α : Type u} → [self : NonUnitalNonAssocRing α] → NonUnitalNonAssocSemiring α

## BASE-LIBRARY REF NonUnitalNonAssocCommRing.toNonUnitalNonAssocRing
{α : Type u} → [self : NonUnitalNonAssocCommRing α] → NonUnitalNonAssocRing α

## BASE-LIBRARY REF NonUnitalCommRing.toNonUnitalNonAssocCommRing
{α : Type u} → [self : NonUnitalCommRing α] → NonUnitalNonAssocCommRing α

## BASE-LIBRARY REF CommRing.toNonUnitalCommRing
{α : Type u} → [s : CommRing α] → NonUnitalCommRing α

## BASE-LIBRARY REF ZMod.commRing
(n : ℕ) → CommRing (ZMod n)

## BASE-LIBRARY REF ZMod.decidableEq
(n : ℕ) → DecidableEq (ZMod n)

## BASE-LIBRARY REF instOfNat
{n : ℕ} → OfNat ℤ n

## BASE-LIBRARY REF Neg.neg
{α : Type u} → [self : Neg α] → α → α

Docstring: `-a` computes the negative or opposite of `a`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `-` in identifiers is `neg` (when used as a unary operator).

## BASE-LIBRARY REF Int.instNegInt
Neg ℤ

## BASE-LIBRARY REF Finset.card
{α : Type u_1} → Finset α → ℕ

Docstring: `s.card` is the number of elements of `s`, aka its cardinality.

The notation `#s` can be accessed in the `Finset` locale. 

## BASE-LIBRARY REF Finset.filter
{α : Type u_1} → (p : α → Prop) → [DecidablePred p] → Finset α → Finset α

Docstring: `Finset.filter p s` is the set of elements of `s` that satisfy `p`.

For example, one can use `s.filter (· ∈ t)` to get the intersection of `s` with `t : Set α`
as a `Finset α` (when a `DecidablePred (· ∈ t)` instance is available). 

## BASE-LIBRARY REF instDecidableEqFin
(n : ℕ) → DecidableEq (Fin n)

## INFORMAL STATEMENT
lem.cancel.all-even.signProduct-eq-prod-pow

\leanhelper  Let $n,d\in \mathbb {N}$. Let $e = (e_1, \ldots , e_d) \in \{ 1,-1\} ^d$ and $x = (x_1, \ldots , x_n) \in [d]^n$. For each $k \in [d]$, let $m_k$ be the multiplicity of $k$ in $x$. Then 

\[  e_{x_{1}}e_{x_{2}}\cdots e_{x_{n}}=e_{1}^{m_{1}}e_{2}^{m_{2}}\cdots e_{d}^{m_{d}}.  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.cancel.multiplicity
def.cancel.multiplicity

\leanhelper  For an $n$-tuple $x : \operatorname {Fin} n \to \operatorname {Fin} d$ and $k \in \operatorname {Fin} d$, the \emph{multiplicity} of $k$ in $x$ is the number of all $i \in \operatorname {Fin} n$ satisfying $x(i) = k$.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The formal binders `\u2200 {n d : \u2115} (e : Fin d \u2192 ZMod 2) (x : Fin n \u2192 Fin d)` match the blueprint\u2019s natural numbers and finite tuples, with `ZMod 2` serving as an exact encoding of `{1,-1}` through `toSign b := if b = 0 then 1 else -1`. The left side unfolds to `\u220f i, toSign (e (x i))`, exactly the product `e_{x\u2081}\u22efe_{x\u2099}` under that encoding. The right side is `\u220f k, toSign (e k) ^ multiplicity x k`, where `multiplicity x k := {i | x i = k}.card`, matching the informal definition of `m_k`. There are no added hypotheses or narrowed ranges."
}