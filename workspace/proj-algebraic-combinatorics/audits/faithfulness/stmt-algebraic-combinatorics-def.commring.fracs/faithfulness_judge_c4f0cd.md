## TARGET AlgebraicCombinatorics.divByUnit (def) — ELABORATED SIGNATURE
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

## BASE-LIBRARY REF NonUnitalNonAssocRing.toNonUnitalNonAssocSemiring
{α : Type u} → [self : NonUnitalNonAssocRing α] → NonUnitalNonAssocSemiring α

## BASE-LIBRARY REF NonUnitalNonAssocCommRing.toNonUnitalNonAssocRing
{α : Type u} → [self : NonUnitalNonAssocCommRing α] → NonUnitalNonAssocRing α

## BASE-LIBRARY REF NonUnitalCommRing.toNonUnitalNonAssocCommRing
{α : Type u} → [self : NonUnitalCommRing α] → NonUnitalNonAssocCommRing α

## BASE-LIBRARY REF CommRing.toNonUnitalCommRing
{α : Type u} → [s : CommRing α] → NonUnitalCommRing α

## BASE-LIBRARY REF Units.val
{α : Type u} → [inst : Monoid α] → αˣ → α

Docstring: The underlying value in the base `Monoid`. 

## BASE-LIBRARY REF Inv.inv
{α : Type u} → [self : Inv α] → α → α

Docstring: `a⁻¹` computes the inverse of `a`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `⁻¹` in identifiers is `inv`.

## BASE-LIBRARY REF Units.instInv
{α : Type u} → [inst : Monoid α] → Inv αˣ

Docstring: The inverse of a unit in a `Monoid`. 

## INFORMAL STATEMENT
def.commring.fracs

Let $L$ be a commutative ring. Let $a\in L$. Assume that $a$ is invertible. Then: 

\textbf{(a)} The inverse of $a$ is called $a^{-1}$. 

\textbf{(b)} For any $b\in L$, the product $b\cdot a^{-1}$ is called $\frac{b}{a}$ (or $b/a$). 

\textbf{(c)} For any negative integer $n$, we define $a^{n}$ to be $\left( a^{-1}\right)^{-n}$. Thus, the $n$-th power $a^{n}$ is defined for each $n\in \mathbb {Z}$.

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.commring.inverse-2
def.commring.inverse

Let $L$ be a commutative ring. Let $a\in L$. Then: 

\textbf{(a)} An \emph{inverse} (or \emph{multiplicative inverse}) of $a$ means an element $b\in L$ such that $ab=ba=1$. 

\textbf{(b)} We say that $a$ is \emph{invertible} in $L$ (or a \emph{unit} of $L$) if $a$ has an inverse.

## VERDICT
{
  "verdict": "drift",
  "justification": "The target faithfully captures only clause (b): its binders `{L : Type u_2} \u2192 [CommRing L] \u2192 L \u2192 L\u02e3 \u2192 L` encode a commutative ring, an arbitrary `b : L`, and an invertible denominator as a bundled unit `a : L\u02e3`, while the body `b * \u2191a\u207b\u00b9` is exactly the informal \u201cthe product $b\\cdot a^{-1}$ is called $b/a$.\u201d Bundling `a` as a unit rather than taking `a : L` plus an invertibility hypothesis is an appropriate encoding, not drift. However, the INFORMAL STATEMENT also includes clause (a), naming the inverse, and especially clause (c): \u201cFor any negative integer $n$, we define $a^n$ to be $(a^{-1})^{-n}$ \u2026 for each $n\\in\\mathbb Z$.\u201d The target has no integer binder, negativity condition, or power definition, so it does not formalize the full blueprint statement. To be faithful, this declaration would need to be accompanied by, or replaced with, formal declarations covering clauses (a) and (c), including the negative-integer power rule; `divByUnit` itself correctly implements clause (b)."
}