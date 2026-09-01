## TARGET AlgebraicCombinatorics.FPS.Laurent.laurentPolynomialToSeries_coeff (theorem) — ELABORATED SIGNATURE
∀ {K : Type u_1} [inst : CommRing K] (p : LaurentPolynomial K) (n : ℤ),
  (AlgebraicCombinatorics.FPS.Laurent.laurentPolynomialToSeries p).coeff n = p n

Docstring: The embedding preserves coefficients. 

## TARGET AlgebraicCombinatorics.laurentPolyToSeries_single (theorem) — ELABORATED SIGNATURE
∀ (K : Type u_1) [inst : CommRing K] (n : ℤ) (r : K),
  ((AlgebraicCombinatorics.laurentPolyToSeries K) fun₀ | n => r) = (HahnSeries.single n) r

Docstring: The Laurent polynomial to series map sends single n r to single n r. 

## TARGET AlgebraicCombinatorics.laurentPolyToSeries_coeff (theorem) — ELABORATED SIGNATURE
∀ (K : Type u_1) [inst : CommRing K] (f : LaurentPolynomial K) (n : ℤ),
  ((AlgebraicCombinatorics.laurentPolyToSeries K) f).coeff n = f n

Docstring: The Laurent polynomial to series map preserves coefficients. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.FPS.Laurent.laurentPolynomialToSeries (def)
{K : Type u_1} → [inst : CommRing K] → LaurentPolynomial K → LaurentSeries K

Body:
fun {K} [CommRing K] p => { coeff := ⇑p, isPWO_support' := ⋯ }

Docstring: A Laurent polynomial can be viewed as a Laurent series.

This is the inclusion `K[T;T⁻¹] → K⸨X⸩`. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.laurentPolyToSeries (def)
(K : Type u_1) → [inst : CommRing K] → LaurentPolynomial K →+* LaurentSeries K

Body:
fun K [CommRing K] => AddMonoidAlgebra.liftNCRingHom HahnSeries.C (AlgebraicCombinatorics.singleMonoidHom✝ K) ⋯

Docstring: The ring homomorphism from Laurent polynomials to Laurent series.
This embeds K[x^±] into K((x)) by mapping each Laurent polynomial to the corresponding
Laurent series with the same coefficients.

This is mentioned after Theorem `thm.fps.laure.lauser-ring`. 

## PROJECT DEPENDENCY _private.AlgebraicCombinatorics.LaurentSeries.0.AlgebraicCombinatorics.singleMonoidHom (def)
(K : Type u_1) → [inst : CommRing K] → Multiplicative ℤ →* LaurentSeries K

Body:
fun K [CommRing K] => { toFun := fun n => (HahnSeries.single (Multiplicative.toAdd n)) 1, map_one' := ⋯, map_mul' := ⋯ }

Docstring: Helper monoid homomorphism: maps n ∈ ℤ (as a multiplicative element) to the single
Hahn series x^n. This is used to construct the Laurent polynomial embedding. 

## BASE-LIBRARY REF CommRing
Type u → Type u

Docstring: A commutative ring is a ring with commutative multiplication. 

## BASE-LIBRARY REF LaurentPolynomial
(R : Type u_3) → [Semiring R] → Type u_3

Docstring: The semiring of Laurent polynomials with coefficients in the semiring `R`.
We denote it by `R[T;T⁻¹]`.
The ring homomorphism `C : R →+* R[T;T⁻¹]` includes `R` as the constant polynomials. 

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

## BASE-LIBRARY REF HahnSeries.coeff
{Γ : Type u_1} → {R : Type u_2} → [inst : PartialOrder Γ] → [inst_1 : Zero R] → HahnSeries Γ R → Γ → R

Docstring: The coefficient function of a Hahn Series. 

## BASE-LIBRARY REF SemilatticeInf.toPartialOrder
{α : Type u} → [self : SemilatticeInf α] → PartialOrder α

## BASE-LIBRARY REF Lattice.toSemilatticeInf
{α : Type u} → [self : Lattice α] → SemilatticeInf α

## BASE-LIBRARY REF instLatticeInt
Lattice ℤ

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

## BASE-LIBRARY REF DFunLike.coe
{F : Sort u_1} → {α : outParam (Sort u_2)} → {β : outParam (α → Sort u_3)} → [self : DFunLike F α β] → F → (a : α) → β a

Docstring: The coercion from `F` to a function. 

## BASE-LIBRARY REF Finsupp
Type u_9 → (M : Type u_10) → [Zero M] → Type (max u_10 u_9)

Docstring: `Finsupp α M`, denoted `α →₀ M`, is the type of functions `f : α → M` such that
`f x = 0` for all but finitely many `x`. 

## BASE-LIBRARY REF NonAssocSemiring.toNonUnitalNonAssocSemiring
{α : Type u} → [self : NonAssocSemiring α] → NonUnitalNonAssocSemiring α

## BASE-LIBRARY REF Semiring.toNonAssocSemiring
{α : Type u} → [self : Semiring α] → NonAssocSemiring α

## BASE-LIBRARY REF Finsupp.instFunLike
{α : Type u_1} → {M : Type u_4} → [inst : Zero M] → FunLike (α →₀ M) α M

## BASE-LIBRARY REF LaurentSeries
(R : Type u) → [Zero R] → Type (max 0 u)

Docstring: `LaurentSeries R` is the type of formal Laurent series with coefficients in `R`, denoted `R⸨X⸩`.

It is implemented as a `HahnSeries` with value group `ℤ`.


## BASE-LIBRARY REF HahnSeries.mk
{Γ : Type u_1} →
  {R : Type u_2} →
    [inst : PartialOrder Γ] → [inst_1 : Zero R] → (coeff : Γ → R) → (Function.support coeff).IsPWO → HahnSeries Γ R

## BASE-LIBRARY REF RingHom
(α : Type u_5) → (β : Type u_6) → [NonAssocSemiring α] → [NonAssocSemiring β] → Type (max u_5 u_6)

Docstring: Bundled semiring homomorphisms; use this for bundled ring homomorphisms too.

This extends from both `MonoidHom` and `MonoidWithZeroHom` in order to put the fields in a
sensible order, even though `MonoidWithZeroHom` already extends `MonoidHom`. 

## BASE-LIBRARY REF AddMonoidAlgebra.nonAssocSemiring
{R : Type u_1} → {M : Type u_4} → [inst : Semiring R] → [AddZeroClass M] → NonAssocSemiring (AddMonoidAlgebra R M)

## BASE-LIBRARY REF AddMonoid.toAddZeroClass
{M : Type u} → [self : AddMonoid M] → AddZeroClass M

## BASE-LIBRARY REF Int.instAddMonoid
AddMonoid ℤ

## BASE-LIBRARY REF HahnSeries.instNonAssocSemiring
{Γ : Type u_1} →
  {R : Type u_3} →
    [inst : AddCommMonoid Γ] →
      [inst_1 : PartialOrder Γ] →
        [IsOrderedCancelAddMonoid Γ] → [inst : NonAssocSemiring R] → NonAssocSemiring (HahnSeries Γ R)

## BASE-LIBRARY REF Int.instAddCommMonoid
AddCommMonoid ℤ

## BASE-LIBRARY REF IsStrictOrderedRing.toIsOrderedCancelAddMonoid
∀ {R : Type u_1} {inst : Semiring R} {inst_1 : PartialOrder R} [self : IsStrictOrderedRing R],
  IsOrderedCancelAddMonoid R

## BASE-LIBRARY REF Int.instSemiring
Semiring ℤ

## BASE-LIBRARY REF Int.instIsStrictOrderedRing
IsStrictOrderedRing ℤ

## BASE-LIBRARY REF RingHom.instFunLike
{α : Type u_2} → {β : Type u_3} → {x : NonAssocSemiring α} → {x_1 : NonAssocSemiring β} → FunLike (α →+* β) α β

## BASE-LIBRARY REF Finsupp.single
{α : Type u_1} → {M : Type u_5} → [inst : Zero M] → α → M → α →₀ M

Docstring: `single a b` is the finitely supported function with value `b` at `a` and zero otherwise. 

## BASE-LIBRARY REF ZeroHom
(M : Type u_10) → (N : Type u_11) → [Zero M] → [Zero N] → Type (max u_10 u_11)

Docstring: `ZeroHom M N` is the type of functions `M → N` that preserve zero.

When possible, instead of parametrizing results over `(f : ZeroHom M N)`,
you should parametrize over `(F : Type*) [ZeroHomClass F M N] (f : F)`.

When you extend this structure, make sure to also extend `ZeroHomClass`.


## BASE-LIBRARY REF HahnSeries
(Γ : Type u_1) → (R : Type u_2) → [PartialOrder Γ] → [Zero R] → Type (max u_1 u_2)

Docstring: If `Γ` is linearly ordered and `R` has zero, then `R⟦Γ⟧` consists of
formal series over `Γ` with coefficients in `R`, whose supports are well-founded. 

## BASE-LIBRARY REF HahnSeries.instZero
{Γ : Type u_1} → {R : Type u_3} → [inst : PartialOrder Γ] → [inst_1 : Zero R] → Zero (HahnSeries Γ R)

## BASE-LIBRARY REF ZeroHom.funLike
{M : Type u_4} → {N : Type u_5} → [inst : Zero M] → [inst_1 : Zero N] → FunLike (ZeroHom M N) M N

## BASE-LIBRARY REF HahnSeries.single
{Γ : Type u_1} → {R : Type u_3} → [inst : PartialOrder Γ] → [inst_1 : Zero R] → Γ → ZeroHom R (HahnSeries Γ R)

Docstring: `single a r` is the Hahn series which has coefficient `r` at `a` and zero otherwise. 

## BASE-LIBRARY REF AddMonoidAlgebra.liftNCRingHom
{k : Type u₁} →
  {G : Type u₂} →
    {R : Type u_2} →
      [inst : Semiring k] →
        [inst_1 : AddMonoid G] →
          [inst_2 : Semiring R] →
            (f : k →+* R) →
              (g : Multiplicative G →* R) →
                (∀ (x : k) (y : Multiplicative G), Commute (f x) (g y)) → AddMonoidAlgebra k G →+* R

Docstring: `liftNC` as a `RingHom`, for when `f` and `g` commute 

## BASE-LIBRARY REF HahnSeries.instSemiring
{Γ : Type u_1} →
  {R : Type u_3} →
    [inst : AddCommMonoid Γ] →
      [inst_1 : PartialOrder Γ] → [IsOrderedCancelAddMonoid Γ] → [inst : Semiring R] → Semiring (HahnSeries Γ R)

## BASE-LIBRARY REF HahnSeries.C
{Γ : Type u_1} →
  {R : Type u_3} →
    [inst : AddCommMonoid Γ] →
      [inst_1 : PartialOrder Γ] →
        [inst_2 : IsOrderedCancelAddMonoid Γ] → [inst_3 : NonAssocSemiring R] → R →+* HahnSeries Γ R

Docstring: `C a` is the constant Hahn Series `a`. `C` is provided as a ring homomorphism. 

## BASE-LIBRARY REF MonoidHom
(M : Type u_10) → (N : Type u_11) → [MulOne M] → [MulOne N] → Type (max u_10 u_11)

Docstring: `M →* N` is the type of functions `M → N` that preserve the `MulOne` structure.
`MonoidHom` is used for both monoid and group homomorphisms.

When possible, instead of parametrizing results over `(f : M →* N)`,
you should parametrize over `(F : Type*) [MonoidHomClass F M N] (f : F)`.

When you extend this structure, make sure to extend `MonoidHomClass`.


## BASE-LIBRARY REF Multiplicative
Type u_1 → Type u_1

Docstring: If `α` carries some additive structure, then `Multiplicative α` carries the corresponding
multiplicative structure. 

## BASE-LIBRARY REF MulOneClass.toMulOne
{M : Type u} → [self : MulOneClass M] → MulOne M

## BASE-LIBRARY REF Multiplicative.mulOneClass
{α : Type u} → [AddZeroClass α] → MulOneClass (Multiplicative α)

## BASE-LIBRARY REF MulZeroOneClass.toMulOneClass
{M₀ : Type u} → [self : MulZeroOneClass M₀] → MulOneClass M₀

## BASE-LIBRARY REF NonAssocSemiring.toMulZeroOneClass
{α : Type u} → [self : NonAssocSemiring α] → MulZeroOneClass α

## BASE-LIBRARY REF MonoidHom.mk
{M : Type u_10} →
  {N : Type u_11} →
    [inst : MulOne M] →
      [inst_1 : MulOne N] →
        (toOneHom : OneHom M N) → (∀ (x y : M), toOneHom.toFun (x * y) = toOneHom.toFun x * toOneHom.toFun y) → M →* N

## BASE-LIBRARY REF OneHom.mk
{M : Type u_10} → {N : Type u_11} → [inst : One M] → [inst_1 : One N] → (toFun : M → N) → toFun 1 = 1 → OneHom M N

## BASE-LIBRARY REF MulOne.toOne
{M : Type u_2} → [self : MulOne M] → One M

## BASE-LIBRARY REF Equiv
Sort u_1 → Sort u_2 → Sort (max (max 1 u_1) u_2)

Docstring: `α ≃ β` is the type of functions from `α → β` with a two-sided inverse. 

## BASE-LIBRARY REF EquivLike.toFunLike
{E : Sort u_1} → {α : Sort u_3} → {β : Sort u_4} → [EquivLike E α β] → FunLike E α β

## BASE-LIBRARY REF Equiv.instEquivLike
{α : Sort u} → {β : Sort v} → EquivLike (α ≃ β) α β

## BASE-LIBRARY REF Multiplicative.toAdd
{α : Type u} → Multiplicative α ≃ α

Docstring: Reinterpret `x : Multiplicative α` as an element of `α`. 

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

## BASE-LIBRARY REF AddGroupWithOne.toAddMonoidWithOne
{R : Type u} → [self : AddGroupWithOne R] → AddMonoidWithOne R

## BASE-LIBRARY REF Ring.toAddGroupWithOne
{R : Type u} → [self : Ring R] → AddGroupWithOne R

## BASE-LIBRARY REF CommRing.toRing
{α : Type u} → [self : CommRing α] → Ring α

## INFORMAL STATEMENT
Embedding preserves coefficients

\leanhelper  The embedding preserves coefficients: for any Laurent polynomial $p$ and $n \in \mathbb {Z}$, the $n$-th coefficient of the image equals $p(n)$. Moreover, $T(n)$ maps to the monomial $x^n$ in $K((x))$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-conv.fps.exp.k-q-alg
conv.fps.exp.K-Q-alg

Throughout this section (unless otherwise stated), we assume that $K$ is not just a commutative ring, but actually a commutative $\mathbb {Q}$-algebra.

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.determines-xn-coeff
def.fps.determines-xn-coeff

Let $\left(\mathbf{a}_{i}\right)_{i\in I}\in K\left[\left[x\right]\right]^{I}$ be a (possibly infinite) family of FPSs. Let $n\in \mathbb {N}$. Let $M$ be a finite subset of $I$. 

\textbf{(a)} We say that $M$ \emph{determines the $x^{n}$-coefficient in the sum of} $\left(\mathbf{a}_{i}\right)_{i\in I}$ if every finite subset $J$ of $I$ satisfying $M\subseteq J\subseteq I$ satisfies 

\[  \left[x^{n}\right]\left(\sum _{i\in J}\mathbf{a}_{i}\right) =\left[x^{n}\right]\left(\sum _{i\in M}\mathbf{a}_{i}\right).  \]

\textbf{(b)} We say that $M$ \emph{determines the $x^{n}$-coefficient in the product of} $\left(\mathbf{a}_{i}\right)_{i\in I}$ if every finite subset $J$ of $I$ satisfying $M\subseteq J\subseteq I$ satisfies 

\[  \left[x^{n}\right]\left(\prod _{i\in J}\mathbf{a}_{i}\right) =\left[x^{n}\right]\left(\prod _{i\in M}\mathbf{a}_{i}\right).  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.exp-log
def.fps.exp-log

Define three FPS $\exp $, $\overline{\log }$ and $\overline{\exp }$ in $K\left[\left[x\right]\right]$ by 

\begin{align*}  \exp &  :=\sum _{n\in \mathbb {N}}\frac{1}{n!}x^{n},\\ \overline{\log } &  :=\sum _{n\geq 1}\frac{\left(-1\right)^{n-1}}{n}x^{n},\\ \overline{\exp } &  :=\exp -1=\sum _{n\geq 1}\frac{1}{n!}x^{n}. \end{align*}

(The last equality sign here follows from $\exp =\sum _{n\in \mathbb {N}}\frac{1}{n!}x^{n}=\underbrace{\frac{1}{0!}}_{=1}\underbrace{x^{0}}_{=1} +\sum _{n\geq 1}\frac{1}{n!}x^{n}=1+\sum _{n\geq 1}\frac{1}{n!}x^{n}$.)

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.exp-log-maps
def.fps.Exp-Log-maps

\textbf{(a)} We let $K\left[\left[x\right] \right]_{0}$ denote the set of all FPSs $f\in K\left[\left[x\right] \right]$ with $\left[x^{0}\right]f=0$. \medskip 

\textbf{(b)} We let $K\left[\left[x\right]\right]_{1}$ denote the set of all FPSs $f\in K\left[\left[x\right]\right]$ with $\left[ x^{0}\right]f=1$. \medskip 

\textbf{(c)} We define two maps 

\begin{align*}  \operatorname {Exp}:K\left[\left[x\right]\right]_{0} &  \rightarrow K\left[\left[x\right]\right]_{1},\\ g &  \mapsto \exp \circ g \end{align*}

 and 

\begin{align*}  \operatorname {Log}:K\left[\left[x\right]\right]_{1} &  \rightarrow K\left[\left[x\right]\right]_{0},\\ f &  \mapsto \overline{\log }\circ \left(f-1\right). \end{align*}

 (These two maps are well-defined according to parts \textbf{(c)} and \textbf{(d)} of Lemma \ref{lem.fps.Exp-Log-maps-wd} below.)

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.fps
def.fps.fps

A \emph{formal power series} (or, short, \emph{FPS}) in $1$ indeterminate over $K$ means a sequence $\left(a_{0},a_{1},a_{2},\ldots \right) = \left(a_{n}\right)_{n\in \mathbb {N}} \in K^{\mathbb {N}}$ of elements of $K$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.laure.double
def.fps.laure.double

Let $K\left[ \left[ x^{\pm }\right] \right] $ be the $K$-module $K^{\mathbb {Z}}$ of all families $\left( a_{n}\right) _{n\in \mathbb {Z}}=\left( \ldots ,a_{-2},a_{-1},a_{0},a_{1},a_{2},\ldots \right) $ of elements of $K$. Its addition and its scaling are defined entrywise:

\begin{align*}  \left( a_{n}\right) _{n\in \mathbb {Z}}+\left( b_{n}\right) _{n\in \mathbb {Z}} &  =\left( a_{n}+b_{n}\right) _{n\in \mathbb {Z}};\\ \lambda \left( a_{n}\right) _{n\in \mathbb {Z}} &  =\left( \lambda a_{n}\right) _{n\in \mathbb {Z}}\  \  \  \  \  \  \  \  \  \  \text{for each }\lambda \in K. \end{align*}

 An element of $K\left[ \left[ x^{\pm }\right] \right] $ will be called a \emph{doubly infinite power series}. We use the notation $\sum _{n\in \mathbb {Z}}a_{n}x^{n}$ for a family $\left( a_{n}\right) _{n\in \mathbb {Z}}\in K\left[ \left[ x^{\pm }\right] \right] $.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.laure.laupol
def.fps.laure.laupol

Let $K\left[ x^{\pm }\right] $ be the $K$-submodule of $K\left[ \left[ x^{\pm }\right] \right] $ consisting of all \textbf{essentially finite} families $\left( a_{n}\right) _{n\in \mathbb {Z}}$. The elements of $K\left[ x^{\pm }\right] $ are called \emph{Laurent polynomials} in the indeterminate $x$ over $K$. 

We define a multiplication on $K\left[ x^{\pm }\right] $ by setting

\[  \left( a_{n}\right) _{n\in \mathbb {Z}}\cdot \left( b_{n}\right) _{n\in \mathbb {Z}}=\left( c_{n}\right) _{n\in \mathbb {Z}},\  \  \  \  \  \  \  \  \  \  \text{where}\  \  \  \  \  \  \  \  \  \  c_{n}=\sum _{i\in \mathbb {Z}}a_{i}b_{n-i}.  \]

 The sum $\sum _{i\in \mathbb {Z}}a_{i}b_{n-i}$ is well-defined because it is essentially finite. 

We define an element $x\in K\left[ x^{\pm }\right] $ by

\[  x=\left( \delta _{i,1}\right) _{i\in \mathbb {Z}}.  \]

In Mathlib, Laurent polynomials are represented as finitely supported functions $\mathbb {Z} \to K$ (the group algebra of $\mathbb {Z}$ over $K$).

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.laure.lauser
def.fps.laure.lauser

We let $K\left( \left( x\right) \right) $ be the subset of $K\left[ \left[ x^{\pm }\right] \right] $ consisting of all families $\left( a_{i}\right) _{i\in \mathbb {Z}}\in K\left[ \left[ x^{\pm }\right] \right] $ such that the sequence $\left( a_{-1},a_{-2},a_{-3},\ldots \right) $ is essentially finite – i.e., such that all sufficiently low $i\in \mathbb {Z}$ satisfy $a_{i}=0$. 

The elements of $K\left( \left( x\right) \right) $ are called \emph{Laurent series} in one indeterminate $x$ over $K$. 

In Mathlib, Laurent series are implemented as Hahn series over $\mathbb {Z}$ with coefficients in $K$, which are functions $\mathbb {Z} \to K$ whose support is well-founded (equivalently, bounded below). The formalization also provides a predicate on doubly infinite power series that captures this textbook definition.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.laure.singlefamily
Summable family of monomials

\leanhelper  Given a Laurent series $\mathbf{a} = (a_n)_{n \in \mathbb {Z}}$, the family of monomials $\bigl(a_g \cdot x^g\bigr)_{g \in \operatorname {supp}(\mathbf{a})}$ forms a summable family. This construction is the key ingredient for expressing a Laurent series as a formal infinite sum of monomials.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.multipliable
def.fps.multipliable

Let $\left(\mathbf{a}_{i}\right)_{i\in I}$ be a (possibly infinite) family of FPSs. Then: 

\textbf{(a)} The family $\left(\mathbf{a}_{i}\right)_{i\in I}$ is said to be \emph{multipliable} if and only if each coefficient in its product is finitely determined. 

\textbf{(b)} If the family $\left(\mathbf{a}_{i}\right)_{i\in I}$ is multipliable, then its \emph{product} $\prod _{i\in I}\mathbf{a}_{i}$ is defined to be the FPS whose $x^{n}$-coefficient (for any $n\in \mathbb {N}$) can be computed as follows: If $n\in \mathbb {N}$, and if $M$ is a finite subset of $I$ that determines the $x^{n}$-coefficient in the product of $\left( \mathbf{a}_{i}\right)_{i\in I}$, then 

\[  \left[x^{n}\right]\left(\prod _{i\in I}\mathbf{a}_{i}\right) =\left[x^{n}\right]\left(\prod _{i\in M}\mathbf{a}_{i}\right).  \]

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.summable
def.fps.summable

A (possibly infinite) family $\left(\mathbf{a}_{i}\right)_{i\in I}$ of FPSs is said to be \emph{summable} (or \emph{entrywise essentially finite}) if 

\[  \text{for each }n\in \mathbb {N}\text{, all but finitely many }i\in I\text{ satisfy }\left[x^{n}\right]\mathbf{a}_{i}=0.  \]

 In this case, the sum $\sum _{i\in I}\mathbf{a}_{i}$ is defined to be the FPS with 

\[  \left[x^{n}\right]\left(\sum _{i\in I}\mathbf{a}_{i}\right) =\underbrace{\sum _{i\in I}\left[x^{n}\right]\mathbf{a}_{i}}_{\substack {\text{an essentially}\\ \text{finite sum}}} \  \  \  \  \  \  \  \  \  \  \text{for all }n\in \mathbb {N}\text{.}  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.summable-multipliable
Summable and multipliable families

\leanhelper  A family $(f_i)_{i \in I}$ of FPSs in $K[\! [x ]\! ]_0$ is \emph{summable} if for each coefficient index $n$, only finitely many $[x^n](f_i)$ are nonzero. 

A family $(f_i)_{i \in I}$ of FPSs in $K[\! [x ]\! ]_1$ is \emph{multipliable} if for each coefficient index $n$, all but finitely many $f_i$ satisfy $[x^k](f_i - 1) = 0$ for all $1 \le k \le n$. 

For summable families, the coefficient-wise sum $\sum _{i \in I} f_i$ belongs to $K[\! [x ]\! ]_0$. For multipliable families, the product $\prod _{i \in I} f_i$ belongs to $K[\! [x ]\! ]_1$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.x
def.fps.x

Let $x$ denote the FPS $\left(0,1,0,0,0,\ldots \right)$. In other words, let $x$ denote the FPS with $\left[x^{1}\right]x=1$ and $\left[x^{i}\right]x=0$ for all $i\neq 1$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.xn-coeff-fin-determined
def.fps.xn-coeff-fin-determined

Let $\left(\mathbf{a}_{i}\right)_{i\in I}\in K\left[\left[x\right]\right]^{I}$ be a (possibly infinite) family of FPSs. Let $n\in \mathbb {N}$. 

\textbf{(a)} We say that \emph{the $x^{n}$-coefficient in the sum of} $\left(\mathbf{a}_{i}\right)_{i\in I}$ \emph{is finitely determined} if there is a finite subset $M$ of $I$ that determines the $x^{n}$-coefficient in the sum of $\left(\mathbf{a}_{i}\right)_{i\in I}$. 

\textbf{(b)} We say that \emph{the $x^{n}$-coefficient in the product of} $\left(\mathbf{a}_{i}\right)_{i\in I}$ \emph{is finitely determined} if there is a finite subset $M$ of $I$ that determines the $x^{n}$-coefficient in the product of $\left(\mathbf{a}_{i}\right)_{i\in I}$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.infsum.essfin
def.infsum.essfin

\textbf{(a)} A family $\left(a_{i}\right)_{i\in I}\in K^{I}$ of elements of $K$ is said to be \emph{essentially finite} if all but finitely many $i\in I$ satisfy $a_{i}=0$ (in other words, if the set $\left\{ i\in I\  \mid \  a_{i}\neq 0\right\} $ is finite). \medskip 

\textbf{(b)} Let $\left(a_{i}\right)_{i\in I}\in K^{I}$ be an essentially finite family of elements of $K$. Then, the infinite sum $\sum _{i\in I}a_{i}$ is defined to equal the finite sum $\sum _{\substack {i\in I;\\ a_{i}\neq 0}}a_{i}$. Such an infinite sum is said to be \emph{essentially finite}.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The coefficient clause is stated exactly by both `\u2200 {K} [CommRing K] (p : LaurentPolynomial K) (n : \u2124), (laurentPolynomialToSeries p).coeff n = p n` and `\u2200 (K) [CommRing K] (f : LaurentPolynomial K) (n : \u2124), ((laurentPolyToSeries K) f).coeff n = f n`, matching \u201cfor any Laurent polynomial p and n \u2208 \u2124, the n-th coefficient of the image equals p(n).\u201d The monomial clause follows from `\u2200 (n : \u2124) (r : K), (laurentPolyToSeries K) (fun\u2080 | n => r) = HahnSeries.single n r`: specializing to `r = 1` says the basis Laurent monomial at exponent `n` maps to the Hahn-series monomial `x^n`, as required by \u201cT(n) maps to the monomial x^n.\u201d Indeed, the formal theorem is stronger because it handles arbitrary coefficients `r`. Finally, although the section convention assumes a commutative \u211a-algebra, the formal binders require only `[CommRing K]`; this is a strictly more general statement with weaker hypotheses, so it remains faithful."
}