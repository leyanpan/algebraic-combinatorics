## TARGET FPS.eval_eq_finsum (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] {A : Type u_2} [inst_1 : CommRing A] [inst_2 : Algebra K A] (f : Polynomial K)
  (a : A), FPS.polyEval f a = ∑ n ∈ f.support, (algebraMap K A) (f.coeff n) * a ^ n

Docstring: The evaluation f[a] can be written as a finite sum over the support of f.
This makes explicit that the sum in Definition 7.5.6 is essentially finite. 

## PROJECT DEPENDENCY FPS.polyEval (def)
{K : Type u_1} → [inst : CommRing K] → {A : Type u_2} → [inst_1 : CommRing A] → [Algebra K A] → Polynomial K → A → A

Body:
fun {K} [CommRing K] {A} [CommRing A] [Algebra K A] f a => (Polynomial.aeval a) f

Docstring: Evaluation of a polynomial at an element of a K-algebra.
This is Definition 7.5.6 (def.pol.subs).

Given a polynomial f ∈ K[X] and an element a of a K-algebra A,
we define f[a] := Σ_{n ∈ ℕ} f_n · a^n.

The sum is essentially finite since f is a polynomial (only finitely many
coefficients are nonzero).

In Mathlib, this is implemented as `Polynomial.aeval a f`. 

## BASE-LIBRARY REF CommRing
Type u → Type u

Docstring: A commutative ring is a ring with commutative multiplication. 

## BASE-LIBRARY REF Algebra
(R : Type u) → (A : Type v) → [CommSemiring R] → [Semiring A] → Type (max u v)

Docstring: An associative unital `R`-algebra is a semiring `A` equipped with a map into its center `R → A`.

See the implementation notes in this file for discussion of the details of this definition.


## BASE-LIBRARY REF CommRing.mul_comm
∀ {α : Type u} [self : CommRing α] (a b : α), a * b = b * a

Docstring: Multiplication is commutative in a commutative multiplicative magma. 

## BASE-LIBRARY REF CommSemiring
Type u → Type u

Docstring: A commutative semiring is a semiring with commutative multiplication. 

## BASE-LIBRARY REF Polynomial
(R : Type u_1) → [Semiring R] → Type u_1

Docstring: `Polynomial R` is the type of univariate polynomials over `R`,
denoted as `R[X]` within the `Polynomial` namespace.

Polynomials should be seen as (semi-)rings with the additional constructor `X`.
The embedding from `R` is called `C`. 

## BASE-LIBRARY REF Finset.sum
{ι : Type u_1} → {M : Type u_3} → [AddCommMonoid M] → Finset ι → (ι → M) → M

Body:
fun {ι} {M} [AddCommMonoid M] s f => (Multiset.map f s.val).sum

Docstring: `∑ x ∈ s, f x` is the sum of `f x` as `x` ranges over the elements
of the finite set `s`.

When the index type is a `Fintype`, the notation `∑ x, f x`, is a shorthand for
`∑ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF NonUnitalNonAssocSemiring
Type u → Type u

Docstring: A not-necessarily-unital, not-necessarily-associative semiring. See `CommutatorRing` and the
documentation thereof in case you need a `NonUnitalNonAssocSemiring` instance on a Lie ring
or a Lie algebra. 

## BASE-LIBRARY REF NonUnitalNonAssocRing
Type u → Type u

Docstring: A not-necessarily-unital, not-necessarily-associative ring. 

## BASE-LIBRARY REF AddCommGroup.add_comm
∀ {G : Type u} [self : AddCommGroup G] (a b : G), a + b = b + a

Docstring: Addition is commutative in a commutative additive magma. 

## BASE-LIBRARY REF NonUnitalNonAssocRing.left_distrib
∀ {α : Type u} [self : NonUnitalNonAssocRing α] (a b c : α), a * (b + c) = a * b + a * c

Docstring: Multiplication is left distributive over addition 

## BASE-LIBRARY REF NonUnitalNonAssocRing.right_distrib
∀ {α : Type u} [self : NonUnitalNonAssocRing α] (a b c : α), (a + b) * c = a * c + b * c

Docstring: Multiplication is right distributive over addition 

## BASE-LIBRARY REF NonUnitalNonAssocRing.zero_mul
∀ {α : Type u} [self : NonUnitalNonAssocRing α] (a : α), 0 * a = 0

Docstring: Zero is a left absorbing element for multiplication 

## BASE-LIBRARY REF NonUnitalNonAssocCommRing
Type u → Type u

Docstring: A non-unital non-associative commutative ring is a `NonUnitalNonAssocRing` with commutative
multiplication. 

## BASE-LIBRARY REF NonUnitalCommRing
Type u → Type u

Docstring: A non-unital commutative ring is a `NonUnitalRing` with commutative multiplication. 

## BASE-LIBRARY REF NonUnitalCommRing.mul_comm
∀ {α : Type u} [self : NonUnitalCommRing α] (a b : α), a * b = b * a

Docstring: Multiplication is commutative in a commutative multiplicative magma. 

## BASE-LIBRARY REF CommRing.toNonUnitalCommRing._proof_1
∀ {α : Type u_1} [s : CommRing α] (a b : α), a - b = a + -b

## BASE-LIBRARY REF Polynomial.support
{R : Type u} → [inst : Semiring R] → Polynomial R → Finset ℕ

Body:
fun {R} [Semiring R] x =>
  match x with
  | { toFinsupp := p } => p.support

Docstring: The set of all `n` such that `X^n` has a non-zero coefficient. 

## BASE-LIBRARY REF Mul
Type u → Type u

Docstring: The homogeneous version of `HMul`: `a * b : α` where `a b : α`. 

## BASE-LIBRARY REF Mul.mul
{α : Type u} → [self : Mul α] → α → α → α

Body:
fun α [self : Mul α] => self.1

Docstring: `a * b` computes the product of `a` and `b`. See `HMul`. 

## BASE-LIBRARY REF Distrib
Type u_1 → Type u_1

Docstring: A typeclass stating that multiplication is left and right distributive
over addition. 

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.left_distrib
∀ {α : Type u} [self : NonUnitalNonAssocSemiring α] (a b c : α), a * (b + c) = a * b + a * c

Docstring: Multiplication is left distributive over addition 

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.right_distrib
∀ {α : Type u} [self : NonUnitalNonAssocSemiring α] (a b c : α), (a + b) * c = a * c + b * c

Docstring: Multiplication is right distributive over addition 

## BASE-LIBRARY REF RingHom
(α : Type u_5) → (β : Type u_6) → [NonAssocSemiring α] → [NonAssocSemiring β] → Type (max u_5 u_6)

Docstring: Bundled semiring homomorphisms; use this for bundled ring homomorphisms too.

This extends from both `MonoidHom` and `MonoidWithZeroHom` in order to put the fields in a
sensible order, even though `MonoidWithZeroHom` already extends `MonoidHom`. 

## BASE-LIBRARY REF Semiring
Type u → Type u

Docstring: A `Semiring` is a type with addition, multiplication, a `0` and a `1` where addition is
commutative and associative, multiplication is associative and left and right distributive over
addition, and `0` and `1` are additive and multiplicative identities. 

## BASE-LIBRARY REF Semiring.one_mul
∀ {α : Type u} [self : Semiring α] (a : α), 1 * a = a

Docstring: One is a left neutral element for multiplication 

## BASE-LIBRARY REF Semiring.mul_one
∀ {α : Type u} [self : Semiring α] (a : α), a * 1 = a

Docstring: One is a right neutral element for multiplication 

## BASE-LIBRARY REF RingHom.instFunLike
{α : Type u_2} → {β : Type u_3} → {x : NonAssocSemiring α} → {x_1 : NonAssocSemiring β} → FunLike (α →+* β) α β

Body:
fun {α} {β} {x} {x_1} => { coe := fun f => (↑↑f).toFun, coe_injective' := ⋯ }

## BASE-LIBRARY REF NonAssocSemiring
Type u → Type u

Docstring: A unital but not-necessarily-associative semiring. 

## BASE-LIBRARY REF RingHom.instFunLike._proof_1
∀ {α : Type u_1} {β : Type u_2} {x : NonAssocSemiring α} {x_1 : NonAssocSemiring β} (f g : α →+* β),
  (fun f => (↑↑f).toFun) f = (fun f => (↑↑f).toFun) g → f = g

## BASE-LIBRARY REF algebraMap
(R : Type u) → (A : Type v) → [inst : CommSemiring R] → [inst_1 : Semiring A] → [Algebra R A] → R →+* A

Body:
fun R A [CommSemiring R] [Semiring A] [Algebra R A] => Algebra.algebraMap

Docstring: Embedding `R →+* A` given by `Algebra` structure. 

## BASE-LIBRARY REF Polynomial.coeff
{R : Type u} → [inst : Semiring R] → Polynomial R → ℕ → R

Body:
fun {R} [Semiring R] x =>
  match (motive := Polynomial R → ℕ → R) x with
  | { toFinsupp := p } => ⇑p

Docstring: `coeff p n` (often denoted `p.coeff n`) is the coefficient of `X^n` in `p`. 

## BASE-LIBRARY REF Pow
Type u → Type v → Type (max u v)

Docstring: The homogeneous version of `HPow`: `a ^ b : α` where `a : α`, `b : β`.
(The right argument is not the same as the left since we often want this even
in the homogeneous case.)

Types can choose to subscribe to particular defaulting behavior by providing
an instance to either `NatPow` or `HomogeneousPow`:
- `NatPow` is for types whose exponents is preferentially a `Nat`.
- `HomogeneousPow` is for types whose base and exponent are preferentially the same.


## BASE-LIBRARY REF Pow.pow
{α : Type u} → {β : Type v} → [self : Pow α β] → α → β → α

Body:
fun α β [self : Pow α β] => self.1

Docstring: `a ^ b` computes `a` to the power of `b`. See `HPow`. 

## BASE-LIBRARY REF Monoid
Type u → Type u

Docstring: A `Monoid` is a `Semigroup` with an element `1` such that `1 * a = a * 1 = a`. 

## BASE-LIBRARY REF MonoidWithZero
Type u → Type u

Docstring: A type `M₀` is a “monoid with zero” if it is a monoid with zero element, and `0` is left
and right absorbing. 

## BASE-LIBRARY REF NonUnitalSemiring.mul_assoc
∀ {α : Type u} [self : NonUnitalSemiring α] (a b c : α), a * b * c = a * (b * c)

Docstring: Multiplication is associative 

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.zero_mul
∀ {α : Type u} [self : NonUnitalNonAssocSemiring α] (a : α), 0 * a = 0

Docstring: Zero is a left absorbing element for multiplication 

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.mul_zero
∀ {α : Type u} [self : NonUnitalNonAssocSemiring α] (a : α), a * 0 = 0

Docstring: Zero is a right absorbing element for multiplication 

## BASE-LIBRARY REF AlgHom
(R : Type u) →
  (A : Type v) →
    (B : Type w) →
      [inst : CommSemiring R] →
        [inst_1 : Semiring A] → [inst_2 : Semiring B] → [Algebra R A] → [Algebra R B] → Type (max v w)

Docstring: Defining the homomorphism in the category R-Alg, denoted `A →ₐ[R] B`. 

## BASE-LIBRARY REF Polynomial.semiring
{R : Type u} → [inst : Semiring R] → Semiring (Polynomial R)

Body:
fun {R} [Semiring R] =>
  { toAdd := Polynomial.instAdd, add_assoc := ⋯, toZero := Polynomial.instZero, zero_add := ⋯, add_zero := ⋯,
    nsmul := fun n x => n • x, nsmul_zero := ⋯, nsmul_succ := ⋯, add_comm := ⋯, toMul := Polynomial.instMul,
    left_distrib := ⋯, right_distrib := ⋯, zero_mul := ⋯, mul_zero := ⋯, mul_assoc := ⋯, toOne := Polynomial.instOne,
    one_mul := ⋯, mul_one := ⋯, toNatCast := Polynomial.instNatCast, natCast_zero := ⋯, natCast_succ := ⋯,
    npow := Monoid.npow, npow_zero := ⋯, npow_succ := ⋯ }

## BASE-LIBRARY REF Polynomial.instAdd
{R : Type u} → [inst : Semiring R] → Add (Polynomial R)

Body:
fun {R} [Semiring R] =>
  {
    add := fun x x_1 =>
      match x with
      | { toFinsupp := a } =>
        match x_1 with
        | { toFinsupp := b } => { toFinsupp := a + b } }

## BASE-LIBRARY REF Polynomial.semiring._proof_1
∀ {R : Type u_1} [inst : Semiring R] (a b c : Polynomial R), a + b + c = a + (b + c)

## BASE-LIBRARY REF Polynomial.instZero
{R : Type u} → [inst : Semiring R] → Zero (Polynomial R)

Body:
fun {R} [Semiring R] => { zero := { toFinsupp := 0 } }

## BASE-LIBRARY REF Polynomial.semiring._proof_2
∀ {R : Type u_1} [inst : Semiring R] (a : Polynomial R), 0 + a = a

## BASE-LIBRARY REF Polynomial.semiring._proof_3
∀ {R : Type u_1} [inst : Semiring R] (a : Polynomial R), a + 0 = a

## BASE-LIBRARY REF Polynomial.instNSMul
{R : Type u} → [inst : Semiring R] → SMul ℕ (Polynomial R)

Body:
fun {R} [Semiring R] => { smul := fun r p => { toFinsupp := r • p.toFinsupp } }

## BASE-LIBRARY REF Polynomial.algebraOfAlgebra
{R : Type u} → {A : Type z} → [inst : CommSemiring R] → [inst_1 : Semiring A] → [Algebra R A] → Algebra R (Polynomial A)

Body:
fun {R} {A} [CommSemiring R] [Semiring A] [Algebra R A] =>
  { toSMul := Polynomial.smulZeroClass.toSMul, algebraMap := Polynomial.C.comp (algebraMap R A), commutes' := ⋯,
    smul_def' := ⋯ }

Docstring: Note that this instance also provides `Algebra R R[X]`. 

## BASE-LIBRARY REF Algebra.id
(R : Type u) → [inst : CommSemiring R] → Algebra R R

Docstring: The identity map inducing an `Algebra` structure. 

## BASE-LIBRARY REF AlgHom.funLike
{R : Type u} →
  {A : Type v} →
    {B : Type w} →
      [inst : CommSemiring R] →
        [inst_1 : Semiring A] →
          [inst_2 : Semiring B] → [inst_3 : Algebra R A] → [inst_4 : Algebra R B] → FunLike (A →ₐ[R] B) A B

Body:
fun {R} {A} {B} [CommSemiring R] [Semiring A] [Semiring B] [Algebra R A] [Algebra R B] =>
  { coe := fun f => (↑↑f.toRingHom).toFun, coe_injective' := ⋯ }

## BASE-LIBRARY REF AlgHom.funLike._proof_1
∀ {R : Type u_3} {A : Type u_1} {B : Type u_2} [inst : CommSemiring R] [inst_1 : Semiring A] [inst_2 : Semiring B]
  [inst_3 : Algebra R A] [inst_4 : Algebra R B] (f g : A →ₐ[R] B),
  (fun f => (↑↑f.toRingHom).toFun) f = (fun f => (↑↑f.toRingHom).toFun) g → f = g

## BASE-LIBRARY REF Polynomial.aeval
{R : Type u} →
  {A : Type z} → [inst : CommSemiring R] → [inst_1 : Semiring A] → [inst_2 : Algebra R A] → A → Polynomial R →ₐ[R] A

Body:
fun {R} {A} [CommSemiring R] [Semiring A] [Algebra R A] x => Polynomial.eval₂AlgHom' (Algebra.ofId R A) x ⋯

Docstring: Given a valuation `x` of the variable in an `R`-algebra `A`, `aeval R A x` is
the unique `R`-algebra homomorphism from `R[X]` to `A` sending `X` to `x`.

This is a stronger variant of the linear map `Polynomial.leval`. 

## INFORMAL STATEMENT
lem.pol.eval.finsum

\leanhelper  The evaluation $f\left[a\right]$ equals $\sum _{n\in \operatorname {supp}(f)}f_{n}\cdot a^{n}$, making the finiteness of the sum explicit.

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.alg.kalg
def.alg.Kalg

A $K$\emph{-algebra} is a set $A$ equipped with four maps

\begin{align*}  \oplus &  :A\times A\rightarrow A,\\ \ominus &  :A\times A\rightarrow A,\\ \odot &  :A\times A\rightarrow A,\\ \rightharpoonup &  :K\times A\rightarrow A \end{align*}

 and two elements $\overrightarrow {0}\in A$ and $\overrightarrow {1}\in A$ satisfying the following properties: 

\begin{enumerate} \item The set $A$, equipped with the maps $\oplus $, $\ominus $ and $\odot $ and the two elements $\overrightarrow {0}$ and $\overrightarrow {1}$, is a (noncommutative) ring. 

\item The set $A$, equipped with the maps $\oplus $, $\ominus $ and $\rightharpoonup $ and the element $\overrightarrow {0}$, is a $K$-module. 

\item We have

\begin{equation}  \lambda \rightharpoonup \left( a\odot b\right) =\left( \lambda \rightharpoonup a\right) \odot b=a\odot \left( \lambda \rightharpoonup b\right) \end{equation}

 for all $\lambda \in K$ and $a,b\in A$. 

\end{enumerate}

(Thus, in a nutshell, a $K$-algebra is a set $A$ that is simultaneously a ring and a $K$-module, with the property that the ring $A$ and the $K$-module $A$ have the same addition, the same subtraction and the same zero, and satisfy the additional compatibility property (\ref{eq.def.alg.Kalg.scaleinv}).)

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.alg.module
def.alg.module

Let $K$ be a commutative ring. 

A $K$\emph{-module} means a set $M$ equipped with three maps 

\begin{align*}  \oplus &  :M\times M\rightarrow M,\\ \ominus &  :M\times M\rightarrow M,\\ \rightharpoonup &  :K\times M\rightarrow M \end{align*}

 (notice that the third map has domain $K\times M$, not $M\times M$) and an element $\overrightarrow {0}\in M$ satisfying the following axioms: 

\begin{enumerate} \item \emph{Commutativity of addition:} We have $a\oplus b=b\oplus a$ for all $a,b\in M$. 

\item \emph{Associativity of addition:} We have $a\oplus \left( b\oplus c\right) =\left( a\oplus b\right) \oplus c$ for all $a,b,c\in M$. 

\item \emph{Neutrality of zero:} We have $a\oplus \overrightarrow {0}=\overrightarrow {0}\oplus a=a$ for all $a\in M$. 

\item \emph{Subtraction undoes addition:} Let $a,b,c\in M$. We have $a\oplus b=c$ if and only if $a=c\ominus b$. 

\item \emph{Associativity of scaling:} We have $u\rightharpoonup \left( v\rightharpoonup a\right) =\left( uv\right) \rightharpoonup a$ for all $u,v\in K$ and $a\in M$. 

\item \emph{Left distributivity:} We have $u\rightharpoonup \left( a\oplus b\right) =\left( u\rightharpoonup a\right) \oplus \left( u\rightharpoonup b\right) $ for all $u\in K$ and $a,b\in M$. 

\item \emph{Right distributivity:} We have $\left( u+v\right) \rightharpoonup a=\left( u\rightharpoonup a\right) \oplus \left( v\rightharpoonup a\right) $ for all $u,v\in K$ and $a\in M$. 

\item \emph{Neutrality of one:} We have $1\rightharpoonup a=a$ for all $a\in M$. 

\item \emph{Left annihilation:} We have $0\rightharpoonup a=\overrightarrow {0}$ for all $a\in M$. 

\item \emph{Right annihilation:} We have $u\rightharpoonup \overrightarrow {0}=\overrightarrow {0}$ for all $u\in K$. 

\end{enumerate}

The operations $\oplus $, $\ominus $ and $\rightharpoonup $ are called the \emph{addition}, the \emph{subtraction} and the \emph{scaling} (or the $K$\emph{-action}) of the $K$-module $M$. When confusion is unlikely, we will denote these three operations $\oplus $, $\ominus $ and $\rightharpoonup $ by $+$, $-$ and $\cdot $, respectively, and we will abbreviate $a\rightharpoonup b=a\cdot b$ by $ab$. 

The element $\overrightarrow {0}$ is called the \emph{zero} (or the \emph{zero vector}) of the $K$-module $M$. We will usually just call it $0$. 

When $M$ is a $K$-module, the elements of $M$ are called \emph{vectors}, while the elements of $K$ are called \emph{scalars}. 

We will use \emph{PEMDAS conventions} for the three operations $\oplus $, $\ominus $ and $\rightharpoonup $, with the operation $\rightharpoonup $ having higher precedence than $\oplus $ and $\ominus $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.alg.ring
def.alg.ring

The notion of a \emph{ring} (also known as a \emph{noncommutative ring}) is defined in the exact same way as we defined the notion of a commutative ring in Definition~ \ref{def.alg.commring}, except that the “Commutativity of multiplication” axiom is removed.

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.infsum.essfin
def.infsum.essfin

\textbf{(a)} A family $\left(a_{i}\right)_{i\in I}\in K^{I}$ of elements of $K$ is said to be \emph{essentially finite} if all but finitely many $i\in I$ satisfy $a_{i}=0$ (in other words, if the set $\left\{ i\in I\  \mid \  a_{i}\neq 0\right\} $ is finite). \medskip 

\textbf{(b)} Let $\left(a_{i}\right)_{i\in I}\in K^{I}$ be an essentially finite family of elements of $K$. Then, the infinite sum $\sum _{i\in I}a_{i}$ is defined to equal the finite sum $\sum _{\substack {i\in I;\\ a_{i}\neq 0}}a_{i}$. Such an infinite sum is said to be \emph{essentially finite}.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.pol.subs
def.pol.subs

Let $f\in K\left[ x\right] $ be a polynomial. Let $A$ be any $K$-algebra. Let $a\in A$ be any element. We then define an element $f\left[ a\right] \in A$ as follows: 

Write $f$ in the form $f=\sum _{n\in \mathbb {N}}f_{n}x^{n}$ with $f_{0},f_{1},f_{2},\ldots \in K$. (That is, $f_{n}=\left[ x^{n}\right] f$ for each $n\in \mathbb {N}$.) Then, set

\[  f\left[ a\right] :=\sum _{n\in \mathbb {N}}f_{n}a^{n}.  \]

 (This sum is essentially finite, since $f$ is a polynomial.) 

The element $f\left[ a\right] $ is also denoted by $f\circ a$ or by $f\left( a\right) $, and is called the \emph{value} of $f$ at $a$ (or the \emph{evaluation} of $f$ at $a$, or the \emph{result of substituting }$a$ for $x$ in $f$).

## VERDICT
{
  "verdict": "significant_divergence",
  "discrepancies": [
    {
      "root": "[CommRing A] on FPS.polyEval",
      "severity": "significant",
      "bridge": "The blueprint allows an arbitrary K-algebra A, whose underlying ring may be noncommutative. The formal definition FPS.polyEval, and consequently the theorem, is only available when A is a commutative ring. To recover the blueprint claim one must generalize polyEval to noncommutative rings (for example using Polynomial.aeval, which itself only requires a Semiring A with an Algebra K A structure) and prove the finite-support expansion in that generality. The stated theorem cannot itself be instantiated for a genuinely noncommutative A, so this requires a new generalized proof rather than a specialization."
    }
  ],
  "justification": "The blueprint says: \u201cLet A be any K-algebra,\u201d while def.alg.Kalg explicitly says its underlying structure is a \u201c(noncommutative) ring.\u201d In contrast, the elaborated target quantifies over `[inst_1 : CommRing A]`, inherited from the body/signature of `FPS.polyEval`, which requires `[CommRing A]`. Thus the theorem proves the evaluation formula only for commutative target algebras, omitting the genuinely noncommutative algebras covered by the informal statement. The displayed summand `(algebraMap K A) (f.coeff n) * a ^ n` otherwise correctly encodes the blueprint\u2019s scalar product `f_n \u00b7 a^n`, and `f.support` correctly indexes the nonzero coefficients."
}