## TARGET FPS.polynomialSubalgebra (def) — ELABORATED SIGNATURE
{K : Type u_1} → [inst : CommRing K] → Subalgebra K (PowerSeries K)

Body:
fun {K} [CommRing K] =>
  { carrier := {f | FPS.IsPolynomial f}, mul_mem' := ⋯, one_mem' := ⋯, add_mem' := ⋯, zero_mem' := ⋯,
    algebraMap_mem' := ⋯ }

Docstring: The set of polynomial power series forms a K-subalgebra of K[[x]].
This is Theorem 7.5.2 (thm.fps.pol.ring) in the source:
K[x] is a subring of K[[x]] (closed under +, -, *, contains 0 and 1)
and a K-submodule (closed under + and scalar multiplication). 

## TARGET FPS.polynomialSubmodule (def) — ELABORATED SIGNATURE
{K : Type u_1} → [inst : CommRing K] → Submodule K (PowerSeries K)

Body:
fun {K} [CommRing K] => Subalgebra.toSubmodule FPS.polynomialSubalgebra

Docstring: The underlying K-submodule of the polynomial subalgebra.
This is the "K-submodule" part of Theorem 7.5.2 (thm.fps.pol.ring):
K[x] is closed under + and scalar multiplication by elements of K. 

## TARGET FPS.polynomialSubring (def) — ELABORATED SIGNATURE
{K : Type u_1} → [inst : CommRing K] → Subring (PowerSeries K)

Body:
fun {K} [CommRing K] => FPS.polynomialSubalgebra.toSubring

Docstring: The underlying subring of the polynomial subalgebra.
This is the "subring" part of Theorem 7.5.2 (thm.fps.pol.ring):
K[x] is closed under +, -, *, and contains 0 and 1. 

## PROJECT DEPENDENCY FPS.IsPolynomial (def)
{K : Type u_1} → [CommRing K] → PowerSeries K → Prop

Body:
fun {K} [CommRing K] f => {n | (PowerSeries.coeff n) f ≠ 0}.Finite

Docstring: A power series is a polynomial if it has finite support, i.e., only finitely many
nonzero coefficients. This corresponds to Definition 7.5.1 (def.fps.pol) in the source. 

## PROJECT DEPENDENCY FPS.isPolynomial_mul (theorem)
∀ {K : Type u_1} [inst : CommRing K] {f g : PowerSeries K},
  FPS.IsPolynomial f → FPS.IsPolynomial g → FPS.IsPolynomial (f * g)

Docstring: The product of two polynomial power series is a polynomial.
This is the main content of Theorem 7.5.2 (thm.fps.pol.ring). 

## PROJECT DEPENDENCY FPS.isPolynomial_one (theorem)
∀ {K : Type u_1} [inst : CommRing K], FPS.IsPolynomial 1

Docstring: The constant power series 1 is a polynomial. 

## PROJECT DEPENDENCY FPS.isPolynomial_add (theorem)
∀ {K : Type u_1} [inst : CommRing K] {f g : PowerSeries K},
  FPS.IsPolynomial f → FPS.IsPolynomial g → FPS.IsPolynomial (f + g)

Docstring: The sum of two polynomial power series is a polynomial.
This is part of Theorem 7.5.2 (thm.fps.pol.ring). 

## PROJECT DEPENDENCY FPS.isPolynomial_zero (theorem)
∀ {K : Type u_1} [inst : CommRing K], FPS.IsPolynomial 0

Docstring: The zero power series is a polynomial. 

## BASE-LIBRARY REF CommRing
Type u → Type u

Docstring: A commutative ring is a ring with commutative multiplication. 

## BASE-LIBRARY REF Subalgebra
(R : Type u) → (A : Type v) → [inst : CommSemiring R] → [inst_1 : Semiring A] → [Algebra R A] → Type v

Docstring: A subalgebra is a sub(semi)ring that includes the range of `algebraMap`. 

## BASE-LIBRARY REF PowerSeries
Type u_1 → Type (max u_1 0)

Docstring: Formal power series over a coefficient type `R` 

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

## BASE-LIBRARY REF Subalgebra.mk
{R : Type u} →
  {A : Type v} →
    [inst : CommSemiring R] →
      [inst_1 : Semiring A] →
        [inst_2 : Algebra R A] →
          (toSubsemiring : Subsemiring A) → (∀ (r : R), (algebraMap R A) r ∈ toSubsemiring.carrier) → Subalgebra R A

## BASE-LIBRARY REF Subsemiring.mk
{R : Type u} →
  [inst : NonAssocSemiring R] →
    (toSubmonoid : Submonoid R) →
      (∀ {a b : R}, a ∈ toSubmonoid.carrier → b ∈ toSubmonoid.carrier → a + b ∈ toSubmonoid.carrier) →
        0 ∈ toSubmonoid.carrier → Subsemiring R

## BASE-LIBRARY REF Semiring.toNonAssocSemiring
{α : Type u} → [self : Semiring α] → NonAssocSemiring α

## BASE-LIBRARY REF Submonoid.mk
{M : Type u_3} → [inst : MulOneClass M] → (toSubsemigroup : Subsemigroup M) → 1 ∈ toSubsemigroup.carrier → Submonoid M

## BASE-LIBRARY REF MulZeroOneClass.toMulOneClass
{M₀ : Type u} → [self : MulZeroOneClass M₀] → MulOneClass M₀

## BASE-LIBRARY REF NonAssocSemiring.toMulZeroOneClass
{α : Type u} → [self : NonAssocSemiring α] → MulZeroOneClass α

## BASE-LIBRARY REF Subsemigroup.mk
{M : Type u_3} →
  [inst : Mul M] → (carrier : Set M) → (∀ {a b : M}, a ∈ carrier → b ∈ carrier → a * b ∈ carrier) → Subsemigroup M

## BASE-LIBRARY REF MulOne.toMul
{M : Type u_2} → [self : MulOne M] → Mul M

## BASE-LIBRARY REF MulOneClass.toMulOne
{M : Type u} → [self : MulOneClass M] → MulOne M

## BASE-LIBRARY REF setOf
{α : Type u} → (α → Prop) → Set α

Docstring: Turn a predicate `p : α → Prop` into a set, also written as `{x | p x}` 

## BASE-LIBRARY REF Submodule
(R : Type u) → (M : Type v) → [inst : Semiring R] → [inst_1 : AddCommMonoid M] → [_root_.Module R M] → Type v

Docstring: A submodule of a module is one which is closed under vector operations.
This is a sufficient condition for the subset of vectors in the submodule
to themselves form a module. 

## BASE-LIBRARY REF PowerSeries.instAddCommMonoid
{R : Type u_1} → [AddCommMonoid R] → AddCommMonoid (PowerSeries R)

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

## BASE-LIBRARY REF PowerSeries.instModule
{R : Type u_1} →
  {A : Type u_2} →
    [inst : Semiring R] → [inst_1 : AddCommMonoid A] → [_root_.Module R A] → _root_.Module R (PowerSeries A)

## BASE-LIBRARY REF LieAlgebra.toModule
{R : Type u} → {L : Type v} → {inst : CommRing R} → {inst_1 : LieRing L} → [self : LieAlgebra R L] → _root_.Module R L

## BASE-LIBRARY REF LieRing.ofAssociativeRing
{A : Type v} → [Ring A] → LieRing A

Docstring: An associative ring gives rise to a Lie ring by taking the bracket to be the ring commutator. 

## BASE-LIBRARY REF CommRing.toRing
{α : Type u} → [self : CommRing α] → Ring α

## BASE-LIBRARY REF LieAlgebra.ofAssociativeAlgebra
{A : Type v} → [inst : Ring A] → {R : Type u} → [inst_1 : CommRing R] → [Algebra R A] → LieAlgebra R A

Docstring: An associative algebra gives rise to a Lie algebra by taking the bracket to be the ring
commutator. 

## BASE-LIBRARY REF DFunLike.coe
{F : Sort u_1} → {α : outParam (Sort u_2)} → {β : outParam (α → Sort u_3)} → [self : DFunLike F α β] → F → (a : α) → β a

Docstring: The coercion from `F` to a function. 

## BASE-LIBRARY REF OrderEmbedding
(α : Type u_6) → (β : Type u_7) → [LE α] → [LE β] → Type (max u_6 u_7)

Docstring: An order embedding is an embedding `f : α ↪ β` such that `a ≤ b ↔ (f a) ≤ (f b)`.
This definition is an abbreviation of `RelEmbedding (≤) (≤)`. 

## BASE-LIBRARY REF NonAssocSemiring.toNonUnitalNonAssocSemiring
{α : Type u} → [self : NonAssocSemiring α] → NonUnitalNonAssocSemiring α

## BASE-LIBRARY REF Algebra.toModule
{R : Type u_2} → {A : Type u_3} → {x : CommSemiring R} → {x_1 : Semiring A} → [Algebra R A] → _root_.Module R A

## BASE-LIBRARY REF Preorder.toLE
{α : Type u_2} → [self : Preorder α] → LE α

## BASE-LIBRARY REF PartialOrder.toPreorder
{α : Type u_2} → [self : PartialOrder α] → Preorder α

## BASE-LIBRARY REF Subalgebra.instPartialOrder
{R : Type u} →
  {A : Type v} →
    [inst : CommSemiring R] → [inst_1 : Semiring A] → [inst_2 : Algebra R A] → PartialOrder (Subalgebra R A)

## BASE-LIBRARY REF Submodule.instPartialOrder
{R : Type u} →
  {M : Type v} →
    [inst : Semiring R] → [inst_1 : AddCommMonoid M] → [inst_2 : _root_.Module R M] → PartialOrder (Submodule R M)

## BASE-LIBRARY REF instFunLikeOrderEmbedding
(α : Type u_6) → (β : Type u_7) → [inst : LE α] → [inst_1 : LE β] → FunLike (α ↪o β) α β

## BASE-LIBRARY REF Subalgebra.toSubmodule
{R : Type u} →
  {A : Type v} →
    [inst : CommSemiring R] → [inst_1 : Semiring A] → [inst_2 : Algebra R A] → Subalgebra R A ↪o Submodule R A

Docstring: The forgetful map from `Subalgebra` to `Submodule` as an `OrderEmbedding` 

## BASE-LIBRARY REF Subring
(R : Type u) → [Ring R] → Type u

Docstring: `Subring R` is the type of subrings of `R`. A subring of `R` is a subset `s` that is a
multiplicative submonoid and an additive subgroup. Note in particular that it shares the
same 0 and 1 as R. 

## BASE-LIBRARY REF PowerSeries.instRing
{R : Type u_1} → [Ring R] → Ring (PowerSeries R)

## BASE-LIBRARY REF Subalgebra.toSubring
{R : Type u} →
  {A : Type v} → [inst : CommRing R] → [inst_1 : Ring A] → [inst_2 : Algebra R A] → Subalgebra R A → Subring A

Docstring: A subalgebra over a ring is also a `Subring`. 

## BASE-LIBRARY REF Set.Finite
{α : Type u} → Set α → Prop

Docstring: A set is finite if the corresponding `Subtype` is finite,
i.e., if there exists a natural `n : ℕ` and an equivalence `s ≃ Fin n`. 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF Ne
{α : Sort u} → α → α → Prop

Docstring: `a ≠ b`, or `Ne a b` is defined as `¬ (a = b)` or `a = b → False`,
and asserts that `a` and `b` are not equal.


Conventions for notations in identifiers:

 * The recommended spelling of `≠` in identifiers is `ne`.

## BASE-LIBRARY REF LinearMap
{R : Type u_14} →
  {S : Type u_15} →
    [inst : Semiring R] →
      [inst_1 : Semiring S] →
        (R →+* S) →
          (M : Type u_16) →
            (M₂ : Type u_17) →
              [inst_2 : AddCommMonoid M] →
                [inst_3 : AddCommMonoid M₂] → [_root_.Module R M] → [_root_.Module S M₂] → Type (max u_16 u_17)

Docstring: A map `f` between an `R`-module and an `S`-module over a ring homomorphism `σ : R →+* S`
is semilinear if it satisfies the two properties `f (x + y) = f x + f y` and
`f (c • x) = (σ c) • f x`. Elements of `LinearMap σ M M₂` (available under the notation
`M →ₛₗ[σ] M₂`) are bundled versions of such maps. For plain linear maps (i.e. for which
`σ = RingHom.id R`), the notation `M →ₗ[R] M₂` is available. An unbundled version of plain linear
maps is available with the predicate `IsLinearMap`, but it should be avoided most of the time. 

## BASE-LIBRARY REF RingHom.id
(α : Type u_5) → [inst : NonAssocSemiring α] → α →+* α

Docstring: The identity ring homomorphism from a semiring to itself. 

## BASE-LIBRARY REF Semiring.toModule
{R : Type u_1} → [inst : Semiring R] → _root_.Module R R

## BASE-LIBRARY REF LinearMap.instFunLike
{R : Type u_1} →
  {S : Type u_5} →
    {M : Type u_8} →
      {M₃ : Type u_11} →
        [inst : Semiring R] →
          [inst_1 : Semiring S] →
            [inst_2 : AddCommMonoid M] →
              [inst_3 : AddCommMonoid M₃] →
                [inst_4 : _root_.Module R M] →
                  [inst_5 : _root_.Module S M₃] → {σ : R →+* S} → FunLike (M →ₛₗ[σ] M₃) M M₃

## BASE-LIBRARY REF PowerSeries.coeff
{R : Type u_1} → [inst : Semiring R] → ℕ → PowerSeries R →ₗ[R] R

Docstring: The `n`th coefficient of a formal power series. 

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF Zero.toOfNat0
{α : Type u_1} → [Zero α] → OfNat α 0

## BASE-LIBRARY REF MulZeroClass.toZero
{M₀ : Type u} → [self : MulZeroClass M₀] → Zero M₀

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.toMulZeroClass
{α : Type u} → [self : NonUnitalNonAssocSemiring α] → MulZeroClass α

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


## BASE-LIBRARY REF One.toOfNat1
{α : Type u_1} → [One α] → OfNat α 1

## BASE-LIBRARY REF MvPowerSeries.instOne
{σ : Type u_1} → {R : Type u_2} → [Semiring R] → One (MvPowerSeries σ R)

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

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.toDistrib
{α : Type u} → [self : NonUnitalNonAssocSemiring α] → Distrib α

## BASE-LIBRARY REF PowerSeries.instCommRing
{R : Type u_1} → [CommRing R] → CommRing (PowerSeries R)

## BASE-LIBRARY REF PowerSeries.instZero
{R : Type u_1} → [Zero R] → Zero (PowerSeries R)

## INFORMAL STATEMENT
thm.fps.pol.ring

The set $K\left[ x\right] $ is a subring of $K\left[ \left[ x\right] \right] $ (that is, it is closed under addition, subtraction and multiplication, and contains the zero $\underline{0}$ and the unity $\underline{1}$) and is a $K$-submodule of $K\left[ \left[ x\right] \right] $ (that is, it is closed under addition and scaling by elements of $K$).

## INFORMAL DEFINITION stmt-algebraic-combinatorics-conv.det.k
conv.det.K

For the rest of this section, we fix a commutative ring $K$. In most examples, $K$ will be $\mathbb {Z}$ or $\mathbb {Q}$ or a polynomial ring.

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.coeff
def.fps.coeff

If $n\in \mathbb {N}$, and if $\mathbf{a}=\left( a_{0},a_{1},a_{2},\ldots \right) \in K\left[\left[x\right]\right]$ is an FPS, then we define an element $\left[x^{n}\right]\mathbf{a}\in K$ by 

\[  \left[x^{n}\right]\mathbf{a}:=a_{n}.  \]

 This is called the \emph{coefficient of }$x^{n}$\emph{ in }$\mathbf{a}$, or the $n$\emph{-th coefficient} of $\mathbf{a}$, or the $x^{n}$\emph{-coefficient} of $\mathbf{a}$.

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.pol
def.fps.pol

\textbf{(a)} An FPS $a\in K\left[ \left[ x\right] \right] $ is said to be a \emph{polynomial} if all but finitely many $n\in \mathbb {N}$ satisfy $\left[ x^{n}\right] a=0$ (that is, if all but finitely many coefficients of $a$ are $0$). \medskip 

\textbf{(b)} We let $K\left[ x\right] $ be the set of all polynomials $a\in K\left[ \left[ x\right] \right] $. This set $K\left[ x\right] $ is a subring of $K\left[ \left[ x\right] \right] $ (according to Theorem \ref{thm.fps.pol.ring} below), and is called the \emph{univariate polynomial ring} over $K$.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The blueprint fixes \u201ca commutative ring K,\u201d matching the sole substantive binder `{K : Type u_1} \u2192 [inst : CommRing K]`; no extra hypothesis or narrowed quantifier is introduced. The formal polynomial set is exactly the intended one: `carrier := {f | FPS.IsPolynomial f}`, where `FPS.IsPolynomial f` is `{n | (PowerSeries.coeff n) f \u2260 0}.Finite`, equivalent to the informal requirement that all but finitely many coefficients are zero. `FPS.polynomialSubring` is `FPS.polynomialSubalgebra.toSubring`, so this same carrier is a subring, encoding closure under addition, subtraction, and multiplication and containment of zero and one. Likewise, `FPS.polynomialSubmodule` is `Subalgebra.toSubmodule FPS.polynomialSubalgebra`, so the same carrier is a `K`-submodule, encoding closure under addition and scaling by elements of `K`. The intermediate `Subalgebra K (PowerSeries K)` packages these compatible ring and scalar-closure facts and is at least as strong as the blueprint statement."
}