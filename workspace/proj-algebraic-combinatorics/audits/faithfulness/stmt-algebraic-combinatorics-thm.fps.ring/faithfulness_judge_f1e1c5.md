## TARGET AlgebraicCombinatorics.FPS.smul_mul_fps (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_1} [inst : CommRing R] (c : R) (f g : PowerSeries R), c • (f * g) = c • f * g

Docstring: (c) Scaling commutes with multiplication (Theorem thm.fps.ring (c)) 

## TARGET AlgebraicCombinatorics.FPS.smul_eq_C_mul_fps (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_1} [inst : CommRing R] (c : R) (f : PowerSeries R), c • f = PowerSeries.C c * f

Docstring: (d) Scaling equals multiplication by constant (Theorem thm.fps.ring (d)) 

## BASE-LIBRARY REF CommRing
Type u → Type u

Docstring: A commutative ring is a ring with commutative multiplication. 

## BASE-LIBRARY REF PowerSeries
Type u_1 → Type (max u_1 0)

Docstring: Formal power series over a coefficient type `R` 

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

## BASE-LIBRARY REF Algebra.toSMul
{R : Type u} → {A : Type v} → {inst : CommSemiring R} → {inst_1 : Semiring A} → [self : Algebra R A] → SMul R A

## BASE-LIBRARY REF CommRing.toCommSemiring
{α : Type u} → [s : CommRing α] → CommSemiring α

## BASE-LIBRARY REF PowerSeries.instSemiring
{R : Type u_1} → [Semiring R] → Semiring (PowerSeries R)

## BASE-LIBRARY REF CommSemiring.toSemiring
{R : Type u} → [self : CommSemiring R] → Semiring R

## BASE-LIBRARY REF PowerSeries.instAlgebra
{R : Type u_1} →
  {A : Type u_2} → [inst : Semiring A] → [inst_1 : CommSemiring R] → [Algebra R A] → Algebra R (PowerSeries A)

## BASE-LIBRARY REF Algebra.id
(R : Type u) → [inst : CommSemiring R] → Algebra R R

Docstring: The identity map inducing an `Algebra` structure. 

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

## BASE-LIBRARY REF RingHom.instFunLike
{α : Type u_2} → {β : Type u_3} → {x : NonAssocSemiring α} → {x_1 : NonAssocSemiring β} → FunLike (α →+* β) α β

## BASE-LIBRARY REF PowerSeries.C
{R : Type u_1} → [inst : Semiring R] → R →+* PowerSeries R

Docstring: The constant formal power series. 

## INFORMAL STATEMENT
thm.fps.ring

\textbf{(a)} The set $K\left[\left[x\right]\right]$ is a commutative ring (with its operations $+$, $-$ and $\cdot $ defined in Definition \ref{def.fps.ops}). Its zero and its unity are the FPSs $\underline{0}=\left(0,0,0,\ldots \right)$ and $\underline{1}=\left( 1,0,0,0,\ldots \right)$. This means, concretely, that the following facts hold: 

\begin{enumerate} \item \emph{Commutativity of addition:} We have $\mathbf{a}+\mathbf{b}=\mathbf{b}+\mathbf{a}$ for all $\mathbf{a},\mathbf{b}\in K\left[\left[ x\right]\right]$. 

\item \emph{Associativity of addition:} We have $\mathbf{a}+\left( \mathbf{b}+\mathbf{c}\right) =\left(\mathbf{a}+\mathbf{b}\right) +\mathbf{c}$ for all $\mathbf{a},\mathbf{b},\mathbf{c}\in K\left[\left[ x\right]\right]$. 

\item \emph{Neutrality of zero:} We have $\mathbf{a}+\underline{0}=\underline{0}+\mathbf{a}=\mathbf{a}$ for all $\mathbf{a}\in K\left[\left[ x\right]\right]$. 

\item \emph{Subtraction undoes addition:} Let $\mathbf{a},\mathbf{b},\mathbf{c}\in K\left[\left[x\right]\right]$. We have $\mathbf{a}+\mathbf{b}=\mathbf{c}$ if and only if $\mathbf{a}=\mathbf{c}-\mathbf{b}$. 

\item \emph{Commutativity of multiplication:} We have $\mathbf{ab}=\mathbf{ba}$ for all $\mathbf{a},\mathbf{b}\in K\left[\left[x\right] \right]$. 

\item \emph{Associativity of multiplication:} We have $\mathbf{a}\left( \mathbf{bc}\right) =\left(\mathbf{ab}\right)\mathbf{c}$ for all $\mathbf{a},\mathbf{b},\mathbf{c}\in K\left[\left[x\right]\right]$. 

\item \emph{Distributivity:} We have

\[  \mathbf{a}\left(\mathbf{b}+\mathbf{c}\right) =\mathbf{ab}+\mathbf{ac}\  \  \  \  \  \  \  \  \  \  \text{and}\  \  \  \  \  \  \  \  \  \  \left(\mathbf{a}+\mathbf{b}\right)\mathbf{c}=\mathbf{ac}+\mathbf{bc} \]

 for all $\mathbf{a},\mathbf{b},\mathbf{c}\in K\left[\left[x\right] \right]$. 

\item \emph{Neutrality of one:} We have $\mathbf{a}\cdot \underline{1}=\underline{1}\cdot \mathbf{a}=\mathbf{a}$ for all $\mathbf{a}\in K\left[ \left[x\right]\right]$. 

\item \emph{Annihilation:} We have $\mathbf{a}\cdot \underline{0}=\underline{0}\cdot \mathbf{a}=\underline{0}$ for all $\mathbf{a}\in K\left[ \left[x\right]\right]$. 

\end{enumerate}

\textbf{(b)} Furthermore, $K\left[\left[x\right]\right]$ is a $K$-module (with its scaling being the map that sends each $\left( \lambda ,\mathbf{a}\right) \in K\times K\left[\left[x\right]\right]$ to the FPS $\lambda \mathbf{a}$ defined in Definition \ref{def.fps.ops} \textbf{(c)}). Its zero vector is $\underline{0}$. Concretely, this means that: 

\begin{enumerate} \item[10.]\emph{Associativity of scaling:} We have $\lambda \left( \mu \mathbf{a}\right) =\left( \lambda \mu \right) \mathbf{a}$ for all $\lambda ,\mu \in K$ and $\mathbf{a}\in K\left[\left[x\right]\right]$. 

\item[11.]\emph{Left distributivity:} We have $\lambda \left( \mathbf{a}+\mathbf{b}\right) =\lambda \mathbf{a}+\lambda \mathbf{b}$ for all $\lambda \in K$ and $\mathbf{a},\mathbf{b}\in K\left[\left[x\right]\right]$. 

\item[12.]\emph{Right distributivity:} We have $\left( \lambda +\mu \right) \mathbf{a}=\lambda \mathbf{a}+\mu \mathbf{a}$ for all $\lambda ,\mu \in K$ and $\mathbf{a}\in K\left[\left[x\right]\right]$. 

\item[13.]\emph{Neutrality of one:} We have $1\mathbf{a}=\mathbf{a}$ for all $\mathbf{a}\in K\left[\left[x\right]\right]$. 

\item[14.]\emph{Left annihilation:} We have $0\mathbf{a}=\underline{0}$ for all $\mathbf{a}\in K\left[\left[x\right]\right]$. 

\item[15.]\emph{Right annihilation:} We have $\lambda \underline{0}=\underline{0}$ for all $\lambda \in K$. 

\end{enumerate}

\textbf{(c)} We have $\lambda \left(\mathbf{a}\cdot \mathbf{b}\right) =\left(\lambda \mathbf{a}\right)\cdot \mathbf{b}=\mathbf{a}\cdot \left( \lambda \mathbf{b}\right)$ for all $\lambda \in K$ and $\mathbf{a},\mathbf{b}\in K\left[\left[x\right]\right]$. \medskip 

\textbf{(d)} Finally, we have $\lambda \mathbf{a}=\underline{\lambda }\cdot \mathbf{a}$ for all $\lambda \in K$ and $\mathbf{a}\in K\left[\left[ x\right]\right]$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.fps
def.fps.fps

A \emph{formal power series} (or, short, \emph{FPS}) in $1$ indeterminate over $K$ means a sequence $\left(a_{0},a_{1},a_{2},\ldots \right) = \left(a_{n}\right)_{n\in \mathbb {N}} \in K^{\mathbb {N}}$ of elements of $K$.

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

## VERDICT
{
  "verdict": "faithful",
  "justification": "The first declaration states `\u2200 ... [CommRing R] (c : R) (f g : PowerSeries R), c \u2022 (f * g) = c \u2022 f * g`, exactly the first equality in part (c), `\u03bb(a\u00b7b) = (\u03bba)\u00b7b`. The remaining equality `(\u03bba)\u00b7b = a\u00b7(\u03bbb)` follows in the declared commutative-ring setting by commutativity of formal-power-series multiplication (equivalently, apply the displayed identity after swapping `f` and `g`). The second declaration states `\u2200 ... (c : R) (f : PowerSeries R), c \u2022 f = PowerSeries.C c * f`, matching part (d), `\u03bba = \\underline{\u03bb}\u00b7a`, since `PowerSeries.C` is documented as the constant formal power series. The `[CommRing R]` binder supplies the coefficient-ring setting required by the blueprint\u2019s ring, subtraction, module, and commutative-multiplication assertions; it is not an additional restriction beyond that mathematical setting."
}