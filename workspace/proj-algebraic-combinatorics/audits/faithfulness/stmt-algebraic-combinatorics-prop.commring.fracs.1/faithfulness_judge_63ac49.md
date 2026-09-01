## TARGET AlgebraicCombinatorics.fracs1_zpow_mul (theorem) — ELABORATED SIGNATURE
∀ {L : Type u_2} [inst : CommRing L] (u : Lˣ) (n m : ℤ), (u ^ n) ^ m = u ^ (n * m)

Docstring: **Proposition (prop.commring.fracs.1d)**: `(a^n)^m = a^{nm}` for all integers `n, m`. 

## TARGET AlgebraicCombinatorics.fracs1_div_mul_div (theorem) — ELABORATED SIGNATURE
∀ {L : Type u_2} [inst : CommRing L] (a c : Lˣ) (b d : L),
  AlgebraicCombinatorics.divByUnit b a * AlgebraicCombinatorics.divByUnit d c =
    AlgebraicCombinatorics.divByUnit (b * d) (a * c)

Docstring: **Proposition (prop.commring.fracs.1e)**: `(b/a) * (d/c) = (bd)/(ac)`. 

## TARGET AlgebraicCombinatorics.fracs1_mul_zpow (theorem) — ELABORATED SIGNATURE
∀ {L : Type u_2} [inst : CommRing L] (u v : Lˣ) (n : ℤ), (u * v) ^ n = u ^ n * v ^ n

Docstring: **Proposition (prop.commring.fracs.1d)**: `(a * b)^n = a^n * b^n` for all integers `n`. 

## TARGET AlgebraicCombinatorics.fracs1_div_eq_iff (theorem) — ELABORATED SIGNATURE
∀ {L : Type u_2} [inst : CommRing L] (a : Lˣ) (b c : L), AlgebraicCombinatorics.divByUnit c a = b ↔ c = ↑a * b

Docstring: **Proposition (prop.commring.fracs.1f)**: `c/a = b` iff `c = a * b`. 

## TARGET AlgebraicCombinatorics.fracs1_zpow_neg_eq_inv_zpow (theorem) — ELABORATED SIGNATURE
∀ {L : Type u_2} [inst : CommRing L] (u : Lˣ) (n : ℤ), u ^ (-n) = u⁻¹ ^ n

Docstring: **Proposition (prop.commring.fracs.1c)**: For a unit `u` and integer `n`,
`u^{-n} = (u⁻¹)^n`. 

## TARGET AlgebraicCombinatorics.fracs1_isUnit_mul (theorem) — ELABORATED SIGNATURE
∀ {L : Type u_2} [inst : CommRing L] {a b : L}, IsUnit a → IsUnit b → IsUnit (a * b)

Docstring: **Proposition (prop.commring.fracs.1b)**: If `a` and `b` are invertible,
then `a * b` is invertible. 

## TARGET AlgebraicCombinatorics.fracs1_mul_inv_comm (theorem) — ELABORATED SIGNATURE
∀ {L : Type u_2} [inst : CommRing L] (u v : Lˣ), (u * v)⁻¹ = u⁻¹ * v⁻¹

Docstring: **Proposition (prop.commring.fracs.1b)**: In a commutative ring,
`(a * b)⁻¹ = a⁻¹ * b⁻¹` for units. 

## TARGET AlgebraicCombinatorics.fracs1_inv_eq_one_mul_inv (theorem) — ELABORATED SIGNATURE
∀ {L : Type u_2} [inst : CommRing L] (u : Lˣ), u⁻¹ = 1 * u⁻¹

Docstring: **Proposition (prop.commring.fracs.1a)**: For an invertible element `a`,
the inverse `a⁻¹` equals `1/a` (i.e., `1 * a⁻¹`).
This is essentially definitional in Mathlib. 

## TARGET AlgebraicCombinatorics.fracs1_div_add_div (theorem) — ELABORATED SIGNATURE
∀ {L : Type u_2} [inst : CommRing L] (a c : Lˣ) (b d : L),
  AlgebraicCombinatorics.divByUnit b a + AlgebraicCombinatorics.divByUnit d c =
    AlgebraicCombinatorics.divByUnit (b * ↑c + ↑a * d) (a * c)

Docstring: **Proposition (prop.commring.fracs.1e)**: `b/a + d/c = (bc + ad)/(ac)`. 

## TARGET AlgebraicCombinatorics.fracs1_zpow_add (theorem) — ELABORATED SIGNATURE
∀ {L : Type u_2} [inst : CommRing L] (u : Lˣ) (n m : ℤ), u ^ (n + m) = u ^ n * u ^ m

Docstring: **Proposition (prop.commring.fracs.1d)**: `a^{n+m} = a^n * a^m` for all integers `n, m`. 

## TARGET AlgebraicCombinatorics.fracs1_mul_inv_rev (theorem) — ELABORATED SIGNATURE
∀ {L : Type u_2} [inst : CommRing L] (u v : Lˣ), (u * v)⁻¹ = v⁻¹ * u⁻¹

Docstring: **Proposition (prop.commring.fracs.1b)**: `(a * b)⁻¹ = b⁻¹ * a⁻¹` for units. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.divByUnit (def)
{L : Type u_2} → [inst : CommRing L] → L → Lˣ → L

Body:
fun {L} [CommRing L] b a => b * ↑a⁻¹

Docstring: Division notation for units: `b / a` means `b * a⁻¹`.
This formalizes the notation `b/a` for `a` invertible in the text. 

## BASE-LIBRARY REF CommRing
Type u → Type u

Docstring: A commutative ring is a ring with commutative multiplication. 

## BASE-LIBRARY REF Units
(α : Type u) → [Monoid α] → Type u

Docstring: Units of a `Monoid`, bundled version. Notation: `αˣ`.

An element of a `Monoid` is a unit if it has a two-sided inverse.
This version bundles the inverse element so that it can be computed.
For a predicate see `IsUnit`. 

## BASE-LIBRARY REF MonoidWithZero.toMonoid
{M₀ : Type u} → [self : MonoidWithZero M₀] → Monoid M₀

## BASE-LIBRARY REF Semiring.toMonoidWithZero
{α : Type u} → [self : Semiring α] → MonoidWithZero α

## BASE-LIBRARY REF CommSemiring.toSemiring
{R : Type u} → [self : CommSemiring R] → Semiring R

## BASE-LIBRARY REF CommRing.toCommSemiring
{α : Type u} → [s : CommRing α] → CommSemiring α

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

## BASE-LIBRARY REF HPow.hPow
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HPow α β γ] → α → β → γ

Docstring: `a ^ b` computes `a` to the power of `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `^` in identifiers is `pow`.

## BASE-LIBRARY REF instHPow
{α : Type u_1} → {β : Type u_2} → [Pow α β] → HPow α β α

## BASE-LIBRARY REF DivInvMonoid.toZPow
{M : Type u_2} → [DivInvMonoid M] → Pow M ℤ

## BASE-LIBRARY REF Units.instDivInvMonoid
{α : Type u} → [inst : Monoid α] → DivInvMonoid αˣ

Docstring: Units of a monoid form a `DivInvMonoid`. 

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

## BASE-LIBRARY REF Distrib.toMul
{R : Type u_1} → [self : Distrib R] → Mul R

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.toDistrib
{α : Type u} → [self : NonUnitalNonAssocSemiring α] → Distrib α

## BASE-LIBRARY REF NonUnitalNonAssocRing.toNonUnitalNonAssocSemiring
{α : Type u} → [self : NonUnitalNonAssocRing α] → NonUnitalNonAssocSemiring α

## BASE-LIBRARY REF NonUnitalNonAssocCommRing.toNonUnitalNonAssocRing
{α : Type u} → [self : NonUnitalNonAssocCommRing α] → NonUnitalNonAssocRing α

## BASE-LIBRARY REF NonUnitalCommRing.toNonUnitalNonAssocCommRing
{α : Type u} → [self : NonUnitalCommRing α] → NonUnitalNonAssocCommRing α

## BASE-LIBRARY REF CommRing.toNonUnitalCommRing
{α : Type u} → [s : CommRing α] → NonUnitalCommRing α

## BASE-LIBRARY REF Units.instMul
{α : Type u} → [inst : Monoid α] → Mul αˣ

Docstring: Units of a monoid have an induced multiplication. 

## BASE-LIBRARY REF Iff
Prop → Prop → Prop

Docstring: If and only if, or logical bi-implication. `a ↔ b` means that `a` implies `b` and vice versa.
By `propext`, this implies that `a` and `b` are equal and hence any expression involving `a`
is equivalent to the corresponding expression with `b` instead.


Conventions for notations in identifiers:

 * The recommended spelling of `↔` in identifiers is `iff`.

 * The recommended spelling of `<->` in identifiers is `iff` (prefer `↔` over `<->`).

## BASE-LIBRARY REF Units.val
{α : Type u} → [inst : Monoid α] → αˣ → α

Docstring: The underlying value in the base `Monoid`. 

## BASE-LIBRARY REF Neg.neg
{α : Type u} → [self : Neg α] → α → α

Docstring: `-a` computes the negative or opposite of `a`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `-` in identifiers is `neg` (when used as a unary operator).

## BASE-LIBRARY REF Int.instNegInt
Neg ℤ

## BASE-LIBRARY REF Inv.inv
{α : Type u} → [self : Inv α] → α → α

Docstring: `a⁻¹` computes the inverse of `a`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `⁻¹` in identifiers is `inv`.

## BASE-LIBRARY REF Units.instInv
{α : Type u} → [inst : Monoid α] → Inv αˣ

Docstring: The inverse of a unit in a `Monoid`. 

## BASE-LIBRARY REF IsUnit
{M : Type u_1} → [Monoid M] → M → Prop

Docstring: An element `a : M` of a `Monoid` is a unit if it has a two-sided inverse.
The actual definition says that `a` is equal to some `u : Mˣ`, where
`Mˣ` is a bundled version of `IsUnit`. 

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF One.toOfNat1
{α : Type u_1} → [One α] → OfNat α 1

## BASE-LIBRARY REF Units.instOne
{α : Type u} → [inst : Monoid α] → One αˣ

Docstring: Units of a monoid have a unit 

## BASE-LIBRARY REF HAdd.hAdd
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HAdd α β γ] → α → β → γ

Docstring: `a + b` computes the sum of `a` and `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `+` in identifiers is `add`.

## BASE-LIBRARY REF instHAdd
{α : Type u_1} → [Add α] → HAdd α α α

## BASE-LIBRARY REF Distrib.toAdd
{R : Type u_1} → [self : Distrib R] → Add R

## BASE-LIBRARY REF Int.instAdd
Add ℤ

## INFORMAL STATEMENT
prop.commring.fracs.1

Let $L$ be a commutative ring. Then: 

\textbf{(a)} Any invertible element $a\in L$ satisfies $a^{-1}=1/a$. 

\textbf{(b)} For any invertible elements $a,b\in L$, the element $ab$ is invertible as well, and satisfies $\left(ab\right)^{-1}=b^{-1}a^{-1}=a^{-1}b^{-1}$. 

\textbf{(c)} If $a\in L$ is invertible, and if $n\in \mathbb {Z}$ is arbitrary, then $a^{-n}=\left(a^{-1}\right)^{n}=\left(a^{n}\right)^{-1}$. 

\textbf{(d)} Laws of exponents hold for negative exponents as well: If $a$ and $b$ are invertible elements of $L$, then

\begin{align*}  a^{n+m} &  =a^{n}a^{m}\  \  \  \  \  \  \  \  \  \  \text{for all }n,m\in \mathbb {Z};\\ \left( ab\right) ^{n} &  =a^{n}b^{n}\  \  \  \  \  \  \  \  \  \  \text{for all }n\in \mathbb {Z};\\ \left( a^{n}\right) ^{m} &  =a^{nm}\  \  \  \  \  \  \  \  \  \  \text{for all }n,m\in \mathbb {Z}. \end{align*}

\textbf{(e)} Laws of fractions hold: If $a$ and $c$ are two invertible elements of $L$, and if $b$ and $d$ are any two elements of $L$, then 

\[  \frac{b}{a}+\frac{d}{c}=\frac{bc+ad}{ac}\  \  \  \  \  \  \  \  \  \  \text{and}\  \  \  \  \  \  \  \  \  \  \frac{b}{a}\cdot \frac{d}{c}=\frac{bd}{ac}.  \]

\textbf{(f)} Division undoes multiplication: If $a,b,c$ are three elements of $L$ with $a$ being invertible, then the equality $\frac{c}{a}=b$ is equivalent to $c=ab$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.alg.commring
def.alg.commring

A \emph{commutative ring} means a set $K$ equipped with three maps

\begin{align*}  \oplus &  :K\times K\rightarrow K,\\ \ominus &  :K\times K\rightarrow K,\\ \odot &  :K\times K\rightarrow K \end{align*}

 and two elements $\mathbf{0}\in K$ and $\mathbf{1}\in K$ satisfying the following axioms: 

\begin{enumerate} \item \emph{Commutativity of addition:} We have $a\oplus b=b\oplus a$ for all $a,b\in K$. 

\item \emph{Associativity of addition:} We have $a\oplus \left( b\oplus c\right) =\left( a\oplus b\right) \oplus c$ for all $a,b,c\in K$. 

\item \emph{Neutrality of zero:} We have $a\oplus \mathbf{0}=\mathbf{0}\oplus a=a$ for all $a\in K$. 

\item \emph{Subtraction undoes addition:} Let $a,b,c\in K$. We have $a\oplus b=c$ if and only if $a=c\ominus b$. 

\item \emph{Commutativity of multiplication:} We have $a\odot b=b\odot a$ for all $a,b\in K$. 

\item \emph{Associativity of multiplication:} We have $a\odot \left( b\odot c\right) =\left( a\odot b\right) \odot c$ for all $a,b,c\in K$. 

\item \emph{Distributivity:} We have

\[  a\odot \left( b\oplus c\right) =\left( a\odot b\right) \oplus \left( a\odot c\right) \  \  \  \  \  \  \  \  \  \  \text{and}\  \  \  \  \  \  \  \  \  \  \left( a\oplus b\right) \odot c=\left( a\odot c\right) \oplus \left( b\odot c\right)  \]

 for all $a,b,c\in K$. 

\item \emph{Neutrality of one:} We have $a\odot \mathbf{1}=\mathbf{1}\odot a=a$ for all $a\in K$. 

\item \emph{Annihilation:} We have $a\odot \mathbf{0}=\mathbf{0}\odot a=\mathbf{0}$ for all $a\in K$. 

\end{enumerate}

The operations $\oplus $, $\ominus $ and $\odot $ are called the \emph{addition}, the \emph{subtraction} and the \emph{multiplication} of the ring $K$. When confusion is unlikely, we will denote these three operations $\oplus $, $\ominus $ and $\odot $ by $+$, $-$ and $\cdot $, respectively, and we will abbreviate $a\odot b=a\cdot b$ by $ab$. 

The elements $\mathbf{0}$ and $\mathbf{1}$ are called the \emph{zero} and the \emph{unity} (or the \emph{one}) of the ring $K$. We will simply call these elements $0$ and $1$ when confusion with the corresponding numbers is unlikely. 

We will use \emph{PEMDAS conventions} for the three operations $\oplus $, $\ominus $ and $\odot $. These imply that the operation $\odot $ has higher precedence than $\oplus $ and $\ominus $, while the operations $\oplus $ and $\ominus $ are left-associative.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.commring.fracs
def.commring.fracs

Let $L$ be a commutative ring. Let $a\in L$. Assume that $a$ is invertible. Then: 

\textbf{(a)} The inverse of $a$ is called $a^{-1}$. 

\textbf{(b)} For any $b\in L$, the product $b\cdot a^{-1}$ is called $\frac{b}{a}$ (or $b/a$). 

\textbf{(c)} For any negative integer $n$, we define $a^{n}$ to be $\left( a^{-1}\right)^{-n}$. Thus, the $n$-th power $a^{n}$ is defined for each $n\in \mathbb {Z}$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.commring.inverse-2
def.commring.inverse

Let $L$ be a commutative ring. Let $a\in L$. Then: 

\textbf{(a)} An \emph{inverse} (or \emph{multiplicative inverse}) of $a$ means an element $b\in L$ such that $ab=ba=1$. 

\textbf{(b)} We say that $a$ is \emph{invertible} in $L$ (or a \emph{unit} of $L$) if $a$ has an inverse.

## VERDICT
{
  "verdict": "drift",
  "justification": "Clause (c) states the full chain \u201c$a^{-n}=(a^{-1})^n=(a^n)^{-1}$.\u201d The corresponding declaration `fracs1_zpow_neg_eq_inv_zpow` has binders `(u : L\u02e3) (n : \u2124)` but concludes only `u ^ (-n) = u\u207b\u00b9 ^ n`; no target states the second required equality `u\u207b\u00b9 ^ n = (u ^ n)\u207b\u00b9`. The other targets match clauses (a), (b), (d), (e), and (f), with `divByUnit b a := b * \u2191a\u207b\u00b9` correctly implementing the blueprint\u2019s fraction definition. To make the package faithful, add a theorem `\u2200 (u : L\u02e3) (n : \u2124), u\u207b\u00b9 ^ n = (u ^ n)\u207b\u00b9`, or strengthen the clause-(c) target to assert both equalities."
}