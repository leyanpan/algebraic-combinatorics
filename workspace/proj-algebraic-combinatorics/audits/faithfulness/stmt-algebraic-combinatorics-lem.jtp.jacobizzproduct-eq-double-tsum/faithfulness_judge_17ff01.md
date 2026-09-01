## TARGET AlgebraicCombinatorics.jacobiZZProduct_eq_double_tsum (theorem) — ELABORATED SIGNATURE
AlgebraicCombinatorics.jacobiZZProduct =
  ∑' (pair : Finset ℕ × Finset ℕ),
    (∏ n ∈ pair.1, (AlgebraicCombinatorics.jacobiFactorZ n - 1)) *
      ∏ n ∈ pair.2, (AlgebraicCombinatorics.jacobiFactorZInv n - 1)

Docstring: The ZZ product equals a double sum over pairs (P, N) of finite subsets.
This combines the binary expansions of the Z and ZInv products.

The formula is:
  jacobiZZProduct = ∑' (P, N), (∏_{n∈P} (jacobiFactorZ n - 1)) * (∏_{n∈N} (jacobiFactorZInv n - 1))
                  = ∑' (P, N), X^{∑(2n+1) + ∑(2m+1)} * z^{|P|} * z^{-|N|}
                  = ∑' (P, N), X^{∑(2n+1) + ∑(2m+1)} * z^{|P| - |N|}

This is the key expansion needed to relate jacobiZZProduct to stateGenFun.

**Proof sketch**: Use `tprod_jacobiFactorZ_eq_tsum`, `tprod_jacobiFactorZInv_eq_tsum`,
and `Summable.tsum_mul_tsum` to expand the product of two sums into a double sum. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.JacobiRing (def)
Type

Body:
PowerSeries (LaurentPolynomial ℤ)

Docstring: The ring (ℤ[z^±])[[q]] for Jacobi's triple product identity.
This is the ring of formal power series in q with coefficients that are
Laurent polynomials in z over ℤ. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.jacobiZZProduct (def)
AlgebraicCombinatorics.JacobiRing

Body:
∏' (n : ℕ), AlgebraicCombinatorics.jacobiFactorZ n * AlgebraicCombinatorics.jacobiFactorZInv n

Docstring: The product of Z and ZInv factors (without the Q factor):
  ∏_{n>0} ((1 + q^{2n-1}z)(1 + q^{2n-1}z^{-1}))
This is the product that remains after canceling the (1-q^{2n}) factors. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.jacobiFactorZ (def)
ℕ → AlgebraicCombinatorics.JacobiRing

Body:
fun n => 1 + PowerSeries.X ^ (2 * n + 1) * AlgebraicCombinatorics.jacobiZ

Docstring: The factor (1 + q^{2n-1}z) in Jacobi's product, for n ≥ 1.
Here we index by n starting from 0, so the exponent is 2n+1. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.jacobiFactorZInv (def)
ℕ → AlgebraicCombinatorics.JacobiRing

Body:
fun n => 1 + PowerSeries.X ^ (2 * n + 1) * AlgebraicCombinatorics.jacobiZInv

Docstring: The factor (1 + q^{2n-1}z^{-1}) in Jacobi's product. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.jacobiZ (def)
AlgebraicCombinatorics.JacobiRing

Body:
PowerSeries.C (LaurentPolynomial.T 1)

Docstring: The Laurent polynomial variable z, viewed as a constant power series in JacobiRing.
This represents z = T(1) where T is the Laurent polynomial basis element. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.jacobiZInv (def)
AlgebraicCombinatorics.JacobiRing

Body:
PowerSeries.C (LaurentPolynomial.T (-1))

Docstring: The inverse z^{-1} = T(-1) as a constant power series. 

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

## BASE-LIBRARY REF tsum
{α : Type u_4} →
  {β : Type u_5} →
    [AddCommMonoid α] →
      [TopologicalSpace α] → (β → α) → optParam (SummationFilter β) (SummationFilter.unconditional β) → α

Docstring: `∑' i, f i` is the unconditional sum of `f` if it exists, or 0 otherwise.

More generally, if `L` is a `SummationFilter`, `∑'[L] i, f i` is the sum of `f` with respect to
`L` if it exists, and `0` otherwise.

(Note that even if the unconditional sum exists, it might not be unique if the topology is not
separated. When the support of `f` is finite, we make the most reasonable choice, to use the sum
over the support. Otherwise, we choose arbitrarily an `a` satisfying `HasSum f a`. Similar remarks
apply to more general summation filters.)


## BASE-LIBRARY REF Prod
Type u → Type v → Type (max u v)

Docstring: The product type, usually written `α × β`. Product types are also called pair or tuple types.
Elements of this type are pairs in which the first element is an `α` and the second element is a
`β`.

Products nest to the right, so `(x, y, z) : α × β × γ` is equivalent to `(x, (y, z)) : α × (β × γ)`.


Conventions for notations in identifiers:

 * The recommended spelling of `×` in identifiers is `Prod`.

## BASE-LIBRARY REF Finset
Type u_4 → Type u_4

Docstring: `Finset α` is the type of finite sets of elements of `α`. It is implemented
as a multiset (a list up to permutation) which has no duplicate elements. 

## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF PowerSeries.instAddCommMonoid
{R : Type u_1} → [AddCommMonoid R] → AddCommMonoid (PowerSeries R)

## BASE-LIBRARY REF LaurentPolynomial
(R : Type u_3) → [Semiring R] → Type u_3

Docstring: The semiring of Laurent polynomials with coefficients in the semiring `R`.
We denote it by `R[T;T⁻¹]`.
The ring homomorphism `C : R →+* R[T;T⁻¹]` includes `R` as the constant polynomials. 

## BASE-LIBRARY REF Int
Type

Docstring: The integers.

This type is special-cased by the compiler and overridden with an efficient implementation. The
runtime has a special representation for `Int` that stores “small” signed numbers directly, while
larger numbers use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)). A “small number” is an integer that can be encoded with one fewer bits
than the platform's pointer size (i.e. 63 bits on 64-bit architectures and 31 bits on 32-bit
architectures).


## BASE-LIBRARY REF Int.instSemiring
Semiring ℤ

## BASE-LIBRARY REF AddMonoidAlgebra.addAddCommMonoid
{R : Type u_1} → {M : Type u_4} → [inst : Semiring R] → AddCommMonoid (AddMonoidAlgebra R M)

## BASE-LIBRARY REF PowerSeries.WithPiTopology.instTopologicalSpace
(R : Type u_1) → [TopologicalSpace R] → TopologicalSpace (PowerSeries R)

Docstring: The pointwise topology on `PowerSeries` 

## BASE-LIBRARY REF Bot.bot
{α : Type u_1} → [self : Bot α] → α

Docstring: The bot (`⊥`, `\bot`) element 

Conventions for notations in identifiers:

 * The recommended spelling of `⊥` in identifiers is `bot`.

## BASE-LIBRARY REF TopologicalSpace
Type u → Type u

Docstring: A topology on `X`. 

## BASE-LIBRARY REF OrderBot.toBot
{α : Type u} → {inst : LE α} → [self : OrderBot α] → Bot α

## BASE-LIBRARY REF Preorder.toLE
{α : Type u_2} → [self : Preorder α] → LE α

## BASE-LIBRARY REF PartialOrder.toPreorder
{α : Type u_2} → [self : PartialOrder α] → Preorder α

## BASE-LIBRARY REF SemilatticeSup.toPartialOrder
{α : Type u} → [self : SemilatticeSup α] → PartialOrder α

## BASE-LIBRARY REF Lattice.toSemilatticeSup
{α : Type u} → [self : Lattice α] → SemilatticeSup α

## BASE-LIBRARY REF CompleteLattice.toLattice
{α : Type u_8} → [self : CompleteLattice α] → Lattice α

## BASE-LIBRARY REF TopologicalSpace.instCompleteLattice
{α : Type u} → CompleteLattice (TopologicalSpace α)

Docstring: Topologies on `α` form a complete lattice, with `⊥` the discrete topology
and `⊤` the indiscrete topology. The infimum of a collection of topologies
is the topology generated by all their open sets, while the supremum is the
topology whose open sets are those sets open in every member of the collection. 

## BASE-LIBRARY REF BoundedOrder.toOrderBot
{α : Type u} → {inst : LE α} → [self : BoundedOrder α] → OrderBot α

## BASE-LIBRARY REF CompleteLattice.toBoundedOrder
{α : Type u_8} → [self : CompleteLattice α] → BoundedOrder α

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


## BASE-LIBRARY REF AddMonoidAlgebra.semiring
{R : Type u_1} → {M : Type u_4} → [inst : Semiring R] → [AddMonoid M] → Semiring (AddMonoidAlgebra R M)

## BASE-LIBRARY REF Int.instAddMonoid
AddMonoid ℤ

## BASE-LIBRARY REF Finset.prod
{ι : Type u_1} → {M : Type u_3} → [CommMonoid M] → Finset ι → (ι → M) → M

Docstring: `∏ x ∈ s, f x` is the product of `f x` as `x` ranges over the elements of the finite set `s`.

When the index type is a `Fintype`, the notation `∏ x, f x`, is a shorthand for
`∏ x ∈ Finset.univ, f x`. 

## BASE-LIBRARY REF CommRing.toCommMonoid
{α : Type u} → [self : CommRing α] → CommMonoid α

## BASE-LIBRARY REF PowerSeries.instCommRing
{R : Type u_1} → [CommRing R] → CommRing (PowerSeries R)

## BASE-LIBRARY REF AddMonoidAlgebra.commRing
{R : Type u_1} → {M : Type u_4} → [inst : CommRing R] → [AddCommMonoid M] → CommRing (AddMonoidAlgebra R M)

## BASE-LIBRARY REF Int.instCommRing
CommRing ℤ

## BASE-LIBRARY REF Int.instAddCommMonoid
AddCommMonoid ℤ

## BASE-LIBRARY REF Prod.fst
{α : Type u} → {β : Type v} → α × β → α

Docstring: The first element of a pair. 

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

## BASE-LIBRARY REF AddMonoidAlgebra.ring
{R : Type u_1} → {M : Type u_4} → [inst : Ring R] → [AddMonoid M] → Ring (AddMonoidAlgebra R M)

## BASE-LIBRARY REF Int.instRing
Ring ℤ

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

## BASE-LIBRARY REF Prod.snd
{α : Type u} → {β : Type v} → α × β → β

Docstring: The second element of a pair. 

## BASE-LIBRARY REF SummationFilter.unconditional
(β : Type u_2) → SummationFilter β

Docstring: **Unconditional summation**: a function on `β` is said to be *unconditionally summable* if its
partial sums over finite subsets converge with respect to the `atTop` filter. 

## BASE-LIBRARY REF PowerSeries
Type u_1 → Type (max u_1 0)

Docstring: Formal power series over a coefficient type `R` 

## BASE-LIBRARY REF tprod
{α : Type u_4} →
  {β : Type u_5} →
    [CommMonoid α] → [TopologicalSpace α] → (β → α) → optParam (SummationFilter β) (SummationFilter.unconditional β) → α

Docstring: `∏' i, f i` is the unconditional product of `f`, if it exists, or 1 otherwise.

More generally, if `L` is a `SummationFilter`, `∏'[L] i, f i` is the product of `f` with respect to
`L` if it exists, and `1` otherwise.

(Note that even if the unconditional product exists, it might not be unique if the topology is not
separated. When the multiplicative support of `f` is finite, we make the most reasonable choice,
to use the product over the multiplicative support. Otherwise, we choose arbitrarily an `a`
satisfying `HasProd f a`. Similar remarks apply to more general summation filters.) 

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

## BASE-LIBRARY REF NonUnitalNonAssocRing.toNonUnitalNonAssocSemiring
{α : Type u} → [self : NonUnitalNonAssocRing α] → NonUnitalNonAssocSemiring α

## BASE-LIBRARY REF NonUnitalNonAssocCommRing.toNonUnitalNonAssocRing
{α : Type u} → [self : NonUnitalNonAssocCommRing α] → NonUnitalNonAssocRing α

## BASE-LIBRARY REF NonUnitalCommRing.toNonUnitalNonAssocCommRing
{α : Type u} → [self : NonUnitalCommRing α] → NonUnitalNonAssocCommRing α

## BASE-LIBRARY REF CommRing.toNonUnitalCommRing
{α : Type u} → [s : CommRing α] → NonUnitalCommRing α

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

## BASE-LIBRARY REF PowerSeries.instSemiring
{R : Type u_1} → [Semiring R] → Semiring (PowerSeries R)

## BASE-LIBRARY REF PowerSeries.X
{R : Type u_1} → [Semiring R] → PowerSeries R

Docstring: The variable of the formal power series ring. 

## BASE-LIBRARY REF instAddNat
Add ℕ

## BASE-LIBRARY REF instMulNat
Mul ℕ

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

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

## BASE-LIBRARY REF LaurentPolynomial.T
{R : Type u_1} → [inst : Semiring R] → ℤ → LaurentPolynomial R

Docstring: The function `n ↦ T ^ n`, implemented as a sequence `ℤ → R[T;T⁻¹]`.

Using directly `T ^ n` does not work, since we want the exponents to be of Type `ℤ` and there
is no `ℤ`-power defined on `R[T;T⁻¹]`.  Using that `T` is a unit introduces extra coercions.
For these reasons, the definition of `T` is as a sequence. 

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

## INFORMAL STATEMENT
lem.jtp.jacobiZZProduct-eq-double-tsum

\leanhelper  The $z$-dependent product admits a binary expansion as a double sum: 

\[  \prod _{n>0}((1+q^{2n-1}z)(1+q^{2n-1}z^{-1})) = \sum _{P,N \text{ finite}} \left(\prod _{n\in P}(q^{2n+1}z)\right)\left(\prod _{n\in N}(q^{2n+1}z^{-1})\right).  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.coeff
def.fps.coeff

If $n\in \mathbb {N}$, and if $\mathbf{a}=\left( a_{0},a_{1},a_{2},\ldots \right) \in K\left[\left[x\right]\right]$ is an FPS, then we define an element $\left[x^{n}\right]\mathbf{a}\in K$ by 

\[  \left[x^{n}\right]\mathbf{a}:=a_{n}.  \]

 This is called the \emph{coefficient of }$x^{n}$\emph{ in }$\mathbf{a}$, or the $n$\emph{-th coefficient} of $\mathbf{a}$, or the $x^{n}$\emph{-coefficient} of $\mathbf{a}$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.fps
def.fps.fps

A \emph{formal power series} (or, short, \emph{FPS}) in $1$ indeterminate over $K$ means a sequence $\left(a_{0},a_{1},a_{2},\ldots \right) = \left(a_{n}\right)_{n\in \mathbb {N}} \in K^{\mathbb {N}}$ of elements of $K$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.lim.ismultipliable
def.fps.lim.isMultipliable

\leanhelper  A family $(f_n)_{n \in \mathbb {N}}$ of FPSs is \emph{multipliable} if (1) $[x^0]f_i = 1$ for all $i$, and (2) for each $n \in \mathbb {N}$, there exists $N$ such that for all $i \geq N$ and all $k \leq n$, $[x^k]f_i = \delta _{k,0}$ (i.e., eventually all $f_i$ are $\equiv 1 \pmod{x^{n+1}}$).

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.lim.issummable
def.fps.lim.isSummable

\leanhelper  A family $(f_n)_{n \in \mathbb {N}}$ of FPSs is \emph{summable} if for each $n \in \mathbb {N}$, the set $\{ i \in \mathbb {N} : [x^n] f_i \neq 0\} $ is finite.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.lim.tprod
def.fps.lim.tprod

\leanhelper  The \emph{infinite product} of a multipliable family $(f_n)_{n \in \mathbb {N}}$ is the FPS $\prod _{n \in \mathbb {N}} f_n$ whose $n$-th coefficient equals $[x^n](\prod _{j=0}^{N} f_j)$ for any sufficiently large $N$.

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.xneq
def.fps.xneq

Let $n\in \mathbb {N}$. Let $f,g\in K\left[\left[x\right]\right]$ be two FPSs. We write $f\overset {x^{n}}{\equiv }g$ if and only if 

\[  \text{each }m\in \left\{ 0,1,\ldots ,n\right\} \text{ satisfies } \left[x^{m}\right]f=\left[x^{m}\right]g.  \]

Thus, we have defined a binary relation $\overset {x^{n}}{\equiv }$ on the set $K\left[\left[x\right]\right]$. We say that an FPS $f$ is $x^{n}$\emph{-equivalent} to an FPS $g$ if and only if $f\overset {x^{n}}{\equiv }g$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.jtp.jacobizzproduct
def.jtp.jacobiZZProduct

\leanhelper  The \emph{$z$-dependent product} is 

\[  \prod _{n>0}\left((1+q^{2n-1}z)(1+q^{2n-1}z^{-1})\right) \in (\mathbb {Z}[z^{\pm }])[[q]].  \]

## VERDICT
{
  "verdict": "faithful",
  "justification": "The target has no added binders or hypotheses and states exactly an equality in `JacobiRing = PowerSeries (LaurentPolynomial \u2124)`. Its left side is `jacobiZZProduct`, whose body is `\u220f' (n : \u2115), jacobiFactorZ n * jacobiFactorZInv n`; using the factor bodies, this is the blueprint\u2019s `\u220f_{n>0} ((1+q^{2n-1}z)(1+q^{2n-1}z^{-1}))`, reindexed from positive `n` to zero-based `n : \u2115`, as explicitly reflected by the exponents `2*n+1`. The right side quantifies over `pair : Finset \u2115 \u00d7 Finset \u2115`, exactly pairs of finite subsets `(P,N)`, and its factors reduce to `jacobiFactorZ n - 1 = q^(2n+1)z` and `jacobiFactorZInv n - 1 = q^(2n+1)z\u207b\u00b9`. Thus `\u2211' pair, (\u220f n \u2208 pair.1, ...) * \u220f n \u2208 pair.2, ...` is precisely the stated double sum over finite `P,N`. The formal `X`, `jacobiZ`, and `jacobiZInv` represent the blueprint\u2019s `q`, `z`, and `z\u207b\u00b9`, respectively."
}