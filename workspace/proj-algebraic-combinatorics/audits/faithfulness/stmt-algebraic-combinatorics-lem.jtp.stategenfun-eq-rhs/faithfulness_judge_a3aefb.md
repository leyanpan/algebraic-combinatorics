## TARGET AlgebraicCombinatorics.stateGenFun_eq_jacobiRHS'_mul_partitionGenFunJacobi (theorem) — ELABORATED SIGNATURE
AlgebraicCombinatorics.stateGenFun = AlgebraicCombinatorics.jacobiRHS' * AlgebraicCombinatorics.partitionGenFunJacobi

## PROJECT DEPENDENCY AlgebraicCombinatorics.JacobiRing (def)
Type

Body:
PowerSeries (LaurentPolynomial ℤ)

Docstring: The ring (ℤ[z^±])[[q]] for Jacobi's triple product identity.
This is the ring of formal power series in q with coefficients that are
Laurent polynomials in z over ℤ. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.stateGenFun (def)
AlgebraicCombinatorics.JacobiRing

Body:
∑' (pair : ℤ × (n : ℕ) × n.Partition),
  have ℓ := pair.1;
  have n := pair.2.fst;
  AlgebraicCombinatorics.stateMonomial (ℓ.natAbs ^ 2 + 2 * n) ℓ

Docstring: The state generating function in JacobiRing:
  ∑_{S state} q^{energy(S)} z^{parnum(S)}

In Borcherds' proof, this is the key object that both the LHS and RHS of Jacobi's
triple product identity equal (after multiplying by the partition generating function).

Since states are in bijection with pairs (ℓ, μ) where ℓ ∈ ℤ and μ is a partition
(via `partitionToState_bijective`), and the bijection satisfies:
- energy(E_{ℓ,μ}) = ℓ² + 2|μ| (by `excitedState_energy`)
- parnum(E_{ℓ,μ}) = ℓ (by `excitedState_parnum`)

we can write the state generating function as:
  ∑_{ℓ∈ℤ} ∑_{n≥0} ∑_{μ partition of n} q^{ℓ² + 2n} z^ℓ

This equals:
  ∑_{ℓ∈ℤ} q^{ℓ²} z^ℓ · ∑_{n≥0} (number of partitions of n) · q^{2n}

which is jacobiRHS' · partitionGenFun[q²].


## PROJECT DEPENDENCY AlgebraicCombinatorics.jacobiRHS' (def)
AlgebraicCombinatorics.JacobiRing

Body:
∑' (ell : ℤ), AlgebraicCombinatorics.jacobiSumTerm ell

Docstring: The right-hand side of Jacobi's triple product identity in JacobiRing:
  ∑_{ℓ∈ℤ} q^{ℓ²} z^ℓ

This is defined as an infinite sum over ℤ. The sum is well-defined because
the exponent ℓ² grows quadratically, so only finitely many terms contribute
to each coefficient of q. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.partitionGenFunJacobi (def)
AlgebraicCombinatorics.JacobiRing

Body:
∑' (p : (n : ℕ) × n.Partition), PowerSeries.X ^ (2 * p.fst)

Docstring: The partition generating function in JacobiRing with q replaced by q².

This is ∑_{n≥0} p(n) q^{2n} where p(n) is the number of partitions of n.
Equivalently, it's the image of the partition generating function under the
substitution q ↦ q².

This is a key ingredient in proving Jacobi's triple product identity:
  stateGenFun = jacobiRHS' * partitionGenFunJacobi

Note: We define this as a sum over partitions rather than using the product
formula ∏_{k≥1}(1-q^{2k})^{-1} to match the structure of stateGenFun. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.stateMonomial (def)
ℕ → ℤ → AlgebraicCombinatorics.JacobiRing

Body:
fun e p => PowerSeries.X ^ e * AlgebraicCombinatorics.jacobiZPow p

Docstring: The monomial q^e * z^p in JacobiRing, representing a state with energy e and particle number p.
This is the building block for the state generating function. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.jacobiSumTerm (def)
ℤ → AlgebraicCombinatorics.JacobiRing

Body:
fun ell => PowerSeries.X ^ ell.natAbs ^ 2 * AlgebraicCombinatorics.jacobiZPow ell

Docstring: A single term q^{ℓ²} z^ℓ in Jacobi's sum. 

## PROJECT DEPENDENCY AlgebraicCombinatorics.jacobiZPow (def)
ℤ → AlgebraicCombinatorics.JacobiRing

Body:
fun ell => PowerSeries.C (LaurentPolynomial.T ell)

Docstring: z^ℓ for any integer ℓ, as a constant power series. 

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

## BASE-LIBRARY REF AddMonoidAlgebra.semiring
{R : Type u_1} → {M : Type u_4} → [inst : Semiring R] → [AddMonoid M] → Semiring (AddMonoidAlgebra R M)

## BASE-LIBRARY REF Int.instAddMonoid
AddMonoid ℤ

## BASE-LIBRARY REF PowerSeries
Type u_1 → Type (max u_1 0)

Docstring: Formal power series over a coefficient type `R` 

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

## BASE-LIBRARY REF Sigma
{α : Type u} → (α → Type v) → Type (max u v)

Docstring: Dependent pairs, in which the second element's type depends on the value of the first element. The
type `Sigma β` is typically written `Σ a : α, β a` or `(a : α) × β a`.

Although its values are pairs, `Sigma` is sometimes known as the *dependent sum type*, since it is
the type level version of an indexed summation.


## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF Nat.Partition
ℕ → Type

Docstring: A partition of `n` is a multiset of positive integers summing to `n`. 

## BASE-LIBRARY REF PowerSeries.instAddCommMonoid
{R : Type u_1} → [AddCommMonoid R] → AddCommMonoid (PowerSeries R)

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

## BASE-LIBRARY REF Prod.fst
{α : Type u} → {β : Type v} → α × β → α

Docstring: The first element of a pair. 

## BASE-LIBRARY REF Sigma.fst
{α : Type u} → {β : α → Type v} → Sigma β → α

Docstring: The first component of a dependent pair.


## BASE-LIBRARY REF Prod.snd
{α : Type u} → {β : Type v} → α × β → β

Docstring: The second element of a pair. 

## BASE-LIBRARY REF HAdd.hAdd
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HAdd α β γ] → α → β → γ

Docstring: `a + b` computes the sum of `a` and `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `+` in identifiers is `add`.

## BASE-LIBRARY REF instHAdd
{α : Type u_1} → [Add α] → HAdd α α α

## BASE-LIBRARY REF instAddNat
Add ℕ

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

## BASE-LIBRARY REF Nat.instMonoid
Monoid ℕ

## BASE-LIBRARY REF Int.natAbs
ℤ → ℕ

Docstring: The absolute value of an integer is its distance from `0`.

This function is overridden by the compiler with an efficient implementation. This definition is
the logical model.

Examples:
 * `(7 : Int).natAbs = 7`
 * `(0 : Int).natAbs = 0`
 * `(-11 : Int).natAbs = 11`


## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

## BASE-LIBRARY REF instMulNat
Mul ℕ

## BASE-LIBRARY REF SummationFilter.unconditional
(β : Type u_2) → SummationFilter β

Docstring: **Unconditional summation**: a function on `β` is said to be *unconditionally summable* if its
partial sums over finite subsets converge with respect to the `atTop` filter. 

## BASE-LIBRARY REF MonoidWithZero.toMonoid
{M₀ : Type u} → [self : MonoidWithZero M₀] → Monoid M₀

## BASE-LIBRARY REF Semiring.toMonoidWithZero
{α : Type u} → [self : Semiring α] → MonoidWithZero α

## BASE-LIBRARY REF PowerSeries.instSemiring
{R : Type u_1} → [Semiring R] → Semiring (PowerSeries R)

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

## INFORMAL STATEMENT
lem.jtp.stateGenFun-eq-rhs

\leanhelper  The state generating function equals the RHS of Jacobi’s identity times the partition generating function: 

\[  \sum _{S\text{ state}}q^{\operatorname {energy}S}z^{\operatorname {parnum}S} =\left(\sum _{\ell \in \mathbb {Z}}q^{\ell ^{2}}z^{\ell }\right) \prod _{n>0}(1-q^{2n})^{-1}.  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.coeff
def.fps.coeff

If $n\in \mathbb {N}$, and if $\mathbf{a}=\left( a_{0},a_{1},a_{2},\ldots \right) \in K\left[\left[x\right]\right]$ is an FPS, then we define an element $\left[x^{n}\right]\mathbf{a}\in K$ by 

\[  \left[x^{n}\right]\mathbf{a}:=a_{n}.  \]

 This is called the \emph{coefficient of }$x^{n}$\emph{ in }$\mathbf{a}$, or the $n$\emph{-th coefficient} of $\mathbf{a}$, or the $x^{n}$\emph{-coefficient} of $\mathbf{a}$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.fps
def.fps.fps

A \emph{formal power series} (or, short, \emph{FPS}) in $1$ indeterminate over $K$ means a sequence $\left(a_{0},a_{1},a_{2},\ldots \right) = \left(a_{n}\right)_{n\in \mathbb {N}} \in K^{\mathbb {N}}$ of elements of $K$.

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

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.jtp.partitiongenfunjacobi
def.jtp.partitionGenFunJacobi

\leanhelper  The \emph{partition generating function in JacobiRing} is 

\[  \sum _{\mu \text{ partition}} q^{2|\mu |} = \prod _{k>0}(1-q^{2k})^{-1} \in (\mathbb {Z}[z^{\pm }])[[q]].  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.jtp.state
def.jtp.state

\leanhelper  A \emph{level} is a number of the form $p+\frac{1}{2}$ with $p\in \mathbb {Z}$. A \emph{state} is a set of levels that contains all but finitely many negative levels, and only finitely many positive levels. 

For any state $S$, we define: 

\begin{itemize} \item the \emph{energy} of $S$ to be 

\[  \operatorname {energy}S:=\sum _{\substack {p>0;\\ p\in S}}2p -\sum _{\substack {p<0;\\ p\notin S}}2p \in \mathbb {N};  \]

\item the \emph{particle number} of $S$ to be 

\[  \operatorname {parnum}S:=\left(\text{\#  of positive levels in } S\right) -\left(\text{\#  of negative levels not in } S\right)\in \mathbb {Z}.  \]

\end{itemize}

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.jtp.stategenfun
def.jtp.stateGenFun

\leanhelper  The \emph{state generating function} is the formal sum over all integer–partition pairs $(\ell , \mu )$: 

\[  \mathcal{S} = \sum _{\ell \in \mathbb {Z}} \sum _{\mu \text{ partition}} q^{\ell ^2 + 2|\mu |} z^\ell \in (\mathbb {Z}[z^{\pm }])[[q]].  \]

 It is defined as the formal sum $\sum '_{(\ell , \mu )} q^{\ell ^2 + 2|\mu |} z^\ell $ over all integer–partition pairs.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The binder-free target asserts exactly `stateGenFun = jacobiRHS' * partitionGenFunJacobi`. Its dependencies expand to the intended three series: `stateGenFun` is `\u2211' (pair : \u2124 \u00d7 (n : \u2115) \u00d7 n.Partition), stateMonomial (\u2113.natAbs ^ 2 + 2 * n) \u2113`, i.e. `\u2211_{\u2113,\u03bc} q^{\u2113\u00b2+2|\u03bc|}z^\u2113`; `jacobiRHS'` is `\u2211' (ell : \u2124), jacobiSumTerm ell`, i.e. `\u2211_{\u2113\u2208\u2124} q^{\u2113\u00b2}z^\u2113`; and `partitionGenFunJacobi` is `\u2211' (p : (n : \u2115) \u00d7 n.Partition), PowerSeries.X ^ (2 * p.fst)`, i.e. `\u2211_\u03bc q^{2|\u03bc|}`. The informal definition identifies this last series with `\u220f_{k>0}(1-q^{2k})\u207b\u00b9`, so the formal right side matches the displayed blueprint right side. The formal multiplication is multiplication in `PowerSeries (LaurentPolynomial \u2124)`, matching the FPS product, and there are no added hypotheses or narrowed binders."
}