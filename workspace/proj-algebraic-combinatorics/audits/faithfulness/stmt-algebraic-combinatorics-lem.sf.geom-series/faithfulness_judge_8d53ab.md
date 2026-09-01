## TARGET AlgebraicCombinatorics.SymmetricPolynomials.geom_series_mul_one_sub (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] {N : ℕ} (i : Fin N),
  ((1 - PowerSeries.X * PowerSeries.C (MvPolynomial.X i)) * PowerSeries.mk fun k => MvPolynomial.X i ^ k) = 1

Docstring: Geometric series identity: (1 - t·x) * (∑_{k≥0} t^k x^k) = 1.
This is the key lemma for the generating function proof of Newton-Girard. 

## TARGET AlgebraicCombinatorics.SymmetricPolynomials.prod_geom_series_mul_prod_one_sub (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] {N : ℕ},
  ((∏ i, (1 - PowerSeries.X * PowerSeries.C (MvPolynomial.X i))) * ∏ i, PowerSeries.mk fun k => MvPolynomial.X i ^ k) =
    1

Docstring: Product of geometric series equals 1 when multiplied by ∏(1 - t·x_i).
This is the generating function identity E(t) * H(t) = 1. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SymmetricPolynomials.P_isCommRing' (def)
{K : Type u_1} → [inst : CommRing K] → {N : ℕ} → CommRing (AlgebraicCombinatorics.SymmetricPolynomials.P K N)

Body:
fun {K} [CommRing K] {N} => inferInstance

Docstring: The polynomial ring P K N is a commutative K-algebra.
Label: def.sf.PS 

## PROJECT DEPENDENCY AlgebraicCombinatorics.SymmetricPolynomials.P (def)
(K : Type u_2) → [CommRing K] → ℕ → Type u_2

Body:
fun K [CommRing K] N => MvPolynomial (Fin N) K

Docstring: The polynomial ring in N variables over K.
This corresponds to 𝒫 in the source (Definition def.sf.PS (a)).
Label: def.sf.PS 

## BASE-LIBRARY REF CommRing
Type u → Type u

Docstring: A commutative ring is a ring with commutative multiplication. 

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

## BASE-LIBRARY REF PowerSeries
Type u_1 → Type (max u_1 0)

Docstring: Formal power series over a coefficient type `R` 

## BASE-LIBRARY REF MvPolynomial
Type u_1 → (R : Type u_2) → [CommSemiring R] → Type (max u_2 u_1)

Docstring: Multivariate polynomial, where `σ` is the index set of the variables and
`R` is the coefficient ring 

## BASE-LIBRARY REF CommRing.toCommSemiring
{α : Type u} → [s : CommRing α] → CommSemiring α

## BASE-LIBRARY REF HMul.hMul
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HMul α β γ] → α → β → γ

Docstring: `a * b` computes the product of `a` and `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `*` in identifiers is `mul`.

## BASE-LIBRARY REF instHMul
{α : Type u_1} → [Mul α] → HMul α α α

## BASE-LIBRARY REF MvPowerSeries.instMul
{σ : Type u_1} → {R : Type u_2} → [Semiring R] → Mul (MvPowerSeries σ R)

## BASE-LIBRARY REF Unit
Type

Docstring: The canonical type with one element. This element is written `()`.

`Unit` has a number of uses:
* It can be used to model control flow that returns from a function call without providing other
  information.
* Monadic actions that return `Unit` have side effects without computing values.
* In polymorphic types, it can be used to indicate that no data is to be stored in a particular
  field.


## BASE-LIBRARY REF CommSemiring.toSemiring
{R : Type u} → [self : CommSemiring R] → Semiring R

## BASE-LIBRARY REF MvPolynomial.commSemiring
{R : Type u} → {σ : Type u_1} → [inst : CommSemiring R] → CommSemiring (MvPolynomial σ R)

## BASE-LIBRARY REF HSub.hSub
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HSub α β γ] → α → β → γ

Docstring: `a - b` computes the difference of `a` and `b`.
The meaning of this notation is type-dependent.
* For natural numbers, this operator saturates at 0: `a - b = 0` when `a ≤ b`. 

Conventions for notations in identifiers:

 * The recommended spelling of `-` in identifiers is `sub` (when used as a binary operator).

## BASE-LIBRARY REF instHSub
{α : Type u_1} → [Sub α] → HSub α α α

## BASE-LIBRARY REF SubNegMonoid.toSub
{G : Type u} → [self : SubNegMonoid G] → Sub G

## BASE-LIBRARY REF AddGroup.toSubNegMonoid
{A : Type u} → [self : AddGroup A] → SubNegMonoid A

## BASE-LIBRARY REF PowerSeries.instAddGroup
{R : Type u_1} → [AddGroup R] → AddGroup (PowerSeries R)

## BASE-LIBRARY REF AddGroupWithOne.toAddGroup
{R : Type u} → [self : AddGroupWithOne R] → AddGroup R

## BASE-LIBRARY REF Ring.toAddGroupWithOne
{R : Type u} → [self : Ring R] → AddGroupWithOne R

## BASE-LIBRARY REF CommRing.toRing
{α : Type u} → [self : CommRing α] → Ring α

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF One.toOfNat1
{α : Type u_1} → [One α] → OfNat α 1

## BASE-LIBRARY REF MvPowerSeries.instOne
{σ : Type u_1} → {R : Type u_2} → [Semiring R] → One (MvPowerSeries σ R)

## BASE-LIBRARY REF PowerSeries.X
{R : Type u_1} → [Semiring R] → PowerSeries R

Docstring: The variable of the formal power series ring. 

## BASE-LIBRARY REF DFunLike.coe
{F : Sort u_1} → {α : outParam (Sort u_2)} → {β : outParam (α → Sort u_3)} → [self : DFunLike F α β] → F → (a : α) → β a

Docstring: The coercion from `F` to a function. 

## BASE-LIBRARY REF RingHom
(α : Type u_5) → (β : Type u_6) → [NonAssocSemiring α] → [NonAssocSemiring β] → Type (max u_5 u_6)

Docstring: Bundled semiring homomorphisms; use this for bundled ring homomorphisms too.

This extends from both `MonoidHom` and `MonoidWithZeroHom` in order to put the fields in a
sensible order, even though `MonoidWithZeroHom` already extends `MonoidHom`. 

## BASE-LIBRARY REF Semiring.toNonAssocSemiring
{α : Type u} → [self : Semiring α] → NonAssocSemiring α

## BASE-LIBRARY REF PowerSeries.instSemiring
{R : Type u_1} → [Semiring R] → Semiring (PowerSeries R)

## BASE-LIBRARY REF RingHom.instFunLike
{α : Type u_2} → {β : Type u_3} → {x : NonAssocSemiring α} → {x_1 : NonAssocSemiring β} → FunLike (α →+* β) α β

## BASE-LIBRARY REF PowerSeries.C
{R : Type u_1} → [inst : Semiring R] → R →+* PowerSeries R

Docstring: The constant formal power series. 

## BASE-LIBRARY REF MvPolynomial.X
{R : Type u} → {σ : Type u_1} → [inst : CommSemiring R] → σ → MvPolynomial σ R

Docstring: `X n` is the degree `1` monomial $X_n$. 

## BASE-LIBRARY REF PowerSeries.mk
{R : Type u_2} → (ℕ → R) → PowerSeries R

Docstring: Constructor for formal power series. 

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

## BASE-LIBRARY REF Finset.prod
{ι : Type u_1} → {M : Type u_3} → [CommMonoid M] → Finset ι → (ι → M) → M

Docstring: `∏ x ∈ s, f x` is the product of `f x` as `x` ranges over the elements of the finite set `s`.

When the index type is a `Fintype`, the notation `∏ x, f x`, is a shorthand for
`∏ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF CommRing.toCommMonoid
{α : Type u} → [self : CommRing α] → CommMonoid α

## BASE-LIBRARY REF PowerSeries.instCommRing
{R : Type u_1} → [CommRing R] → CommRing (PowerSeries R)

## BASE-LIBRARY REF Finset.univ
{α : Type u_1} → [Fintype α] → Finset α

Docstring: `univ` is the universal finite set of type `Finset α` implied from
the assumption `Fintype α`. 

## BASE-LIBRARY REF Fin.fintype
(n : ℕ) → Fintype (Fin n)

## BASE-LIBRARY REF inferInstance
{α : Sort u} → [i : α] → α

Docstring: `inferInstance` synthesizes a value of any target type by typeclass
inference. This function has the same type signature as the identity
function, but the square brackets on the `[i : α]` argument means that it will
attempt to construct this argument by typeclass inference. (This will fail if
`α` is not a `class`.) Example:
```
#check (inferInstance : Inhabited Nat) -- Inhabited Nat

def foo : Inhabited (Nat × Nat) :=
  inferInstance

example : foo.default = (default, default) :=
  rfl
```


## BASE-LIBRARY REF MvPolynomial.instCommRingMvPolynomial
{R : Type u} → {σ : Type u_1} → [inst : CommRing R] → CommRing (MvPolynomial σ R)

## INFORMAL STATEMENT
lem.sf.geom-series

\leanhelper  For each $i$, the geometric series identity $(1 - t x_i) \cdot \sum _{k \geq 0} (t x_i)^k = 1$ holds in the power series ring $\mathcal{P}[[t]]$. Taking the product over all $i \in [N]$, we obtain the generating function identity $E(t) \cdot H(t) = 1$, where $E(t) = \prod _{i=1}^N (1 - t x_i)$ and $H(t) = \prod _{i=1}^N \sum _{k \geq 0} (t x_i)^k$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.coeff
def.fps.coeff

If $n\in \mathbb {N}$, and if $\mathbf{a}=\left( a_{0},a_{1},a_{2},\ldots \right) \in K\left[\left[x\right]\right]$ is an FPS, then we define an element $\left[x^{n}\right]\mathbf{a}\in K$ by 

\[  \left[x^{n}\right]\mathbf{a}:=a_{n}.  \]

 This is called the \emph{coefficient of }$x^{n}$\emph{ in }$\mathbf{a}$, or the $n$\emph{-th coefficient} of $\mathbf{a}$, or the $x^{n}$\emph{-coefficient} of $\mathbf{a}$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.fps
def.fps.fps

A \emph{formal power series} (or, short, \emph{FPS}) in $1$ indeterminate over $K$ means a sequence $\left(a_{0},a_{1},a_{2},\ldots \right) = \left(a_{n}\right)_{n\in \mathbb {N}} \in K^{\mathbb {N}}$ of elements of $K$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.geometric-series
def.fps.geometric-series

\leanhelper  The \emph{geometric series} is the FPS $\frac{1}{1-x} = (1-x)^{-1} \in K[[x]]$ (where $K$ is a field).

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.lim.issummable
def.fps.lim.isSummable

\leanhelper  A family $(f_n)_{n \in \mathbb {N}}$ of FPSs is \emph{summable} if for each $n \in \mathbb {N}$, the set $\{ i \in \mathbb {N} : [x^n] f_i \neq 0\} $ is finite.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.lim.tsum
def.fps.lim.tsum

\leanhelper  The \emph{infinite sum} of a summable family $(f_n)_{n \in \mathbb {N}}$ is the FPS $\sum _{n \in \mathbb {N}} f_n$ whose $n$-th coefficient is $\sum _{i \in S_n} [x^n] f_i$, where $S_n = \{ i : [x^n] f_i \neq 0\} $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.ops
def.fps.ops

\textbf{(a)} The \emph{sum} of two FPSs $\mathbf{a}=\left( a_{0},a_{1},a_{2},\ldots \right)$ and $\mathbf{b}=\left(b_{0},b_{1},b_{2},\ldots \right)$ is defined to be the FPS

\[  \left(a_{0}+b_{0},\  \  a_{1}+b_{1},\  \  a_{2}+b_{2},\  \  \ldots \right).  \]

 It is denoted by $\mathbf{a}+\mathbf{b}$. \medskip 

\textbf{(b)} The \emph{difference} of two FPSs $\mathbf{a}=\left(a_{0},a_{1},a_{2},\ldots \right)$ and $\mathbf{b}=\left(b_{0},b_{1},b_{2},\ldots \right)$ is defined to be the FPS

\[  \left(a_{0}-b_{0},\  \  a_{1}-b_{1},\  \  a_{2}-b_{2},\  \  \ldots \right).  \]

 It is denoted by $\mathbf{a}-\mathbf{b}$. \medskip 

\textbf{(c)} If $\lambda \in K$ and if $\mathbf{a}=\left(a_{0},a_{1},a_{2},\ldots \right)$ is an FPS, then we define an FPS 

\[  \lambda \mathbf{a}:=\left(\lambda a_{0},\lambda a_{1},\lambda a_{2},\ldots \right).  \]

\textbf{(d)} The \emph{product} of two FPSs $\mathbf{a}=\left(a_{0},a_{1},a_{2},\ldots \right)$ and $\mathbf{b}=\left(b_{0},b_{1},b_{2},\ldots \right)$ is defined to be the FPS $\left(c_{0},c_{1},c_{2},\ldots \right)$, where 

\begin{align*}  c_{n} &  =\sum _{i=0}^{n}a_{i}b_{n-i}=\sum _{\substack {\left(i,j\right) \in \mathbb {N}^{2};\\ \begin{bgroup} i+j=n

\end{bgroup}}}a_{i}b_{j}\\ &  =a_{0}b_{n}+a_{1}b_{n-1}+a_{2}b_{n-2}+\cdots +a_{n}b_{0}\  \  \  \  \  \  \  \  \  \  \text{for each }n\in \mathbb {N}. \end{align*}

 This product is denoted by $\mathbf{a}\cdot \mathbf{b}$ or just by $\mathbf{ab}$. \medskip 

\textbf{(e)} For each $a\in K$, we define $\underline{a}$ to be the FPS $\left(a,0,0,0,\ldots \right)$. An FPS of the form $\underline{a}$ for some $a\in K$ (that is, an FPS $\left(a_{0},a_{1},a_{2},\ldots \right)$ satisfying $a_{1}=a_{2}=a_{3}=\cdots =0$) is said to be \emph{constant}. \medskip 

\textbf{(f)} The set of all FPSs (in $1$ indeterminate over $K$) is denoted $K\left[\left[x\right]\right]$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.x
def.fps.x

Let $x$ denote the FPS $\left(0,1,0,0,0,\ldots \right)$. In other words, let $x$ denote the FPS with $\left[x^{1}\right]x=1$ and $\left[x^{i}\right]x=0$ for all $i\neq 1$.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The first declaration quantifies over every variable, `\u2200 {N : \u2115} (i : Fin N)`, matching \u201cFor each i,\u201d and states `((1 - PowerSeries.X * PowerSeries.C (MvPolynomial.X i)) * PowerSeries.mk fun k => MvPolynomial.X i ^ k) = 1`. Here `PowerSeries.X` is the power-series variable t, `PowerSeries.C (MvPolynomial.X i)` is the constant series x_i, and `PowerSeries.mk fun k => ... ^ k` has k-th coefficient x_i^k, hence represents `\u2211_{k\u22650} (t x_i)^k`. The second declaration takes products over all `i : Fin N` and states exactly that the product of the `(1 - t x_i)` factors times the product of their geometric series is `1`, matching `E(t) \u00b7 H(t) = 1`. Its coefficient ring is `MvPolynomial (Fin N) K`, which is the defined polynomial ring `P K N`. Both signatures assume `[CommRing K]`, whereas the supplied informal geometric-series definition mentions a field; this is a strictly more general result with weaker algebraic hypotheses, not drift."
}