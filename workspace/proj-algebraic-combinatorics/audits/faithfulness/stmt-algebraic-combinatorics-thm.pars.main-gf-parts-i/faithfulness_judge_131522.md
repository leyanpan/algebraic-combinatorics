## TARGET Nat.Partition.partitionCount_genFun_partsIn (theorem) — ELABORATED SIGNATURE
∀ {R : Type u_1} [inst : CommSemiring R] [inst_1 : TopologicalSpace R] [T2Space R] [IsTopologicalSemiring R] (I : Set ℕ)
  [inst_4 : DecidablePred fun x => x ∈ I],
  HasProd (fun k => if k + 1 ∈ I then ∑' (j : ℕ), PowerSeries.X ^ ((k + 1) * j) else 1)
    (PowerSeries.mk fun n => ↑(Nat.Partition.partsInCount I n))

Docstring: The generating function for partitions with parts in a set I:
`∑_{n≥0} p_I(n) x^n = ∏_{k∈I} 1/(1-x^k)`.
(Theorem \ref{thm.pars.main-gf-parts-I})

This generalizes both the standard partition generating function (I = ℕ⁺)
and the finite product version (I = {1, ..., m}).

The product is over k in I, expressed here with shifted index as a conditional
infinite product. Each factor `∑' j, X^((k+1)*j)` equals `1/(1-X^(k+1))` as
a geometric series.

**Proof sketch:** The bijection from the TeX source maps each essentially finite
family `(u_i)_{i∈I}` of nonnegative integers to the partition containing each
`i ∈ I` exactly `u_i` times. The coefficient of `X^n` on the product side counts
such families with `∑_{i∈I} i·u_i = n`, which bijects with partitions of `n`
having all parts in `I`. 

## PROJECT DEPENDENCY Nat.Partition.partsInCount (def)
(I : Set ℕ) → [DecidablePred fun x => x ∈ I] → ℕ → ℕ

Body:
fun I [DecidablePred fun x => x ∈ I] n => (Nat.Partition.restricted n fun x => x ∈ I).card

Docstring: The number of partitions of `n` with all parts in a set `I`.
(Used in Theorem \ref{thm.pars.main-gf-parts-I}) 

## BASE-LIBRARY REF CommSemiring
Type u → Type u

Docstring: A commutative semiring is a semiring with commutative multiplication. 

## BASE-LIBRARY REF TopologicalSpace
Type u → Type u

Docstring: A topology on `X`. 

## BASE-LIBRARY REF T2Space
(X : Type u) → [TopologicalSpace X] → Prop

Docstring: A T₂ space, also known as a Hausdorff space, is one in which for every
`x ≠ y` there exists disjoint open sets around `x` and `y`. This is
the most widely used of the separation axioms. 

## BASE-LIBRARY REF IsTopologicalSemiring
(R : Type u_1) → [TopologicalSpace R] → [NonUnitalNonAssocSemiring R] → Prop

Docstring: a topological semiring is a semiring `R` where addition and multiplication are continuous.
We allow for non-unital and non-associative semirings as well.

The `IsTopologicalSemiring` class should *only* be instantiated in the presence of a
`NonUnitalNonAssocSemiring` instance; if there is an instance of `NonUnitalNonAssocRing`,
then `IsTopologicalRing` should be used. Note: in the presence of `NonAssocRing`, these classes are
mathematically equivalent (see `IsTopologicalSemiring.continuousNeg_of_mul` or
`IsTopologicalSemiring.toIsTopologicalRing`). 

## BASE-LIBRARY REF NonAssocSemiring.toNonUnitalNonAssocSemiring
{α : Type u} → [self : NonAssocSemiring α] → NonUnitalNonAssocSemiring α

## BASE-LIBRARY REF Semiring.toNonAssocSemiring
{α : Type u} → [self : Semiring α] → NonAssocSemiring α

## BASE-LIBRARY REF CommSemiring.toSemiring
{R : Type u} → [self : CommSemiring R] → Semiring R

## BASE-LIBRARY REF Set
Type u → Type u

Docstring: A set is a collection of elements of some type `α`.

Although `Set` is defined as `α → Prop`, this is an implementation detail which should not be
relied on. Instead, `setOf` and membership of a set (`∈`) should be used to convert between sets
and predicates.


## BASE-LIBRARY REF Nat
Type

Docstring: The natural numbers, starting at zero.

This type is special-cased by both the kernel and the compiler, and overridden with an efficient
implementation. Both use a fast arbitrary-precision arithmetic library (usually
[GMP](https://gmplib.org/)); at runtime, `Nat` values that are sufficiently small are unboxed.


## BASE-LIBRARY REF DecidablePred
{α : Sort u} → (α → Prop) → Sort (max 1 u)

Docstring: A decidable predicate.

A predicate is decidable if the corresponding proposition is `Decidable` for each possible argument.


## BASE-LIBRARY REF Membership.mem
{α : outParam (Type u)} → {γ : Type v} → [self : Membership α γ] → γ → α → Prop

Docstring: The membership relation `a ∈ s : Prop` where `a : α`, `s : γ`. 

Conventions for notations in identifiers:

 * The recommended spelling of `∈` in identifiers is `mem`.

## BASE-LIBRARY REF Set.instMembership
{α : Type u} → Membership α (Set α)

## BASE-LIBRARY REF HasProd
{α : Type u_1} →
  {β : Type u_2} →
    [CommMonoid α] →
      [TopologicalSpace α] → (β → α) → α → optParam (SummationFilter β) (SummationFilter.unconditional β) → Prop

Docstring: `HasProd f a L` means that the (potentially infinite) product of the `f b` for `b : β` converges
to `a` along the SummationFilter `L`.

By default `L` is the `unconditional` one, corresponding to the limit of all finite sets towards
the entire type. So we take the product over bigger and bigger finite sets. This product operation
is invariant under permuting the terms (while products for more general summation filters usually
are not).

For the definition and many statements, `α` does not need to be a topological monoid, only a monoid
with a topology (i.e. the multiplication is not assumed to be continuous). We only add this
assumption later, for the lemmas where it is relevant.

These are defined in an identical way to infinite sums (`HasSum`). For example, we say that
the function `ℕ → ℝ` sending `n` to `1 / 2` has a product of `0`, rather than saying that it does
not converge as some authors would. 

## BASE-LIBRARY REF PowerSeries
Type u_1 → Type (max u_1 0)

Docstring: Formal power series over a coefficient type `R` 

## BASE-LIBRARY REF CommSemiring.toCommMonoid
{R : Type u} → [self : CommSemiring R] → CommMonoid R

## BASE-LIBRARY REF PowerSeries.instCommSemiring
{R : Type u_1} → [CommSemiring R] → CommSemiring (PowerSeries R)

## BASE-LIBRARY REF PowerSeries.WithPiTopology.instTopologicalSpace
(R : Type u_1) → [TopologicalSpace R] → TopologicalSpace (PowerSeries R)

Docstring: The pointwise topology on `PowerSeries` 

## BASE-LIBRARY REF ite
{α : Sort u} → (c : Prop) → [h : Decidable c] → α → α → α

Docstring: `if c then t else e` is notation for `ite c t e`, "if-then-else", which decides to
return `t` or `e` depending on whether `c` is true or false. The explicit argument
`c : Prop` does not have any actual computational content, but there is an additional
`[Decidable c]` argument synthesized by typeclass inference which actually
determines how to evaluate `c` to true or false. Write `if h : c then t else e`
instead for a "dependent if-then-else" `dite`, which allows `t`/`e` to use the fact
that `c` is true/false.


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

## BASE-LIBRARY REF OfNat.ofNat
{α : Type u} → (x : ℕ) → [self : OfNat α x] → α

Docstring: The `OfNat.ofNat` function is automatically inserted by the parser when
the user writes a numeric literal like `1 : α`. Implementations of this
typeclass can therefore customize the behavior of `n : α` based on `n` and
`α`. 

## BASE-LIBRARY REF instOfNatNat
(n : ℕ) → OfNat ℕ n

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


## BASE-LIBRARY REF PowerSeries.instAddCommMonoid
{R : Type u_1} → [AddCommMonoid R] → AddCommMonoid (PowerSeries R)

## BASE-LIBRARY REF NonUnitalNonAssocSemiring.toAddCommMonoid
{α : Type u} → [self : NonUnitalNonAssocSemiring α] → AddCommMonoid α

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

## BASE-LIBRARY REF HMul.hMul
{α : Type u} → {β : Type v} → {γ : outParam (Type w)} → [self : HMul α β γ] → α → β → γ

Docstring: `a * b` computes the product of `a` and `b`.
The meaning of this notation is type-dependent. 

Conventions for notations in identifiers:

 * The recommended spelling of `*` in identifiers is `mul`.

## BASE-LIBRARY REF instHMul
{α : Type u_1} → [Mul α] → HMul α α α

## BASE-LIBRARY REF instMulNat
Mul ℕ

## BASE-LIBRARY REF SummationFilter.unconditional
(β : Type u_2) → SummationFilter β

Docstring: **Unconditional summation**: a function on `β` is said to be *unconditionally summable* if its
partial sums over finite subsets converge with respect to the `atTop` filter. 

## BASE-LIBRARY REF One.toOfNat1
{α : Type u_1} → [One α] → OfNat α 1

## BASE-LIBRARY REF MvPowerSeries.instOne
{σ : Type u_1} → {R : Type u_2} → [Semiring R] → One (MvPowerSeries σ R)

## BASE-LIBRARY REF Unit
Type

Docstring: The canonical type with one element. This element is written `()`.

`Unit` has a number of uses:
* It can be used to model control flow that returns from a function call without providing other
  information.
* Monadic actions that return `Unit` have side effects without computing values.
* In polymorphic types, it can be used to indicate that no data is to be stored in a particular
  field.


## BASE-LIBRARY REF PowerSeries.mk
{R : Type u_2} → (ℕ → R) → PowerSeries R

Docstring: Constructor for formal power series. 

## BASE-LIBRARY REF Nat.cast
{R : Type u} → [NatCast R] → ℕ → R

Docstring: The canonical homomorphism `Nat → R`. In most use cases, the target type will have a (semi)ring
structure, and this homomorphism should be a (semi)ring homomorphism.

`NatCast` and `IntCast` exist to allow different libraries with their own types that can be notated
as natural numbers to have consistent `simp` normal forms without needing to create coercion
simplification sets that are aware of all combinations. Libraries should make it easy to work with
`NatCast` where possible. For instance, in Mathlib there will be such a homomorphism (and thus a
`NatCast R` instance) whenever `R` is an additive monoid with a `1`.

The prototypical example is `Int.ofNat`.


## BASE-LIBRARY REF AddMonoidWithOne.toNatCast
{R : Type u_2} → [self : AddMonoidWithOne R] → NatCast R

## BASE-LIBRARY REF AddCommMonoidWithOne.toAddMonoidWithOne
{R : Type u_2} → [self : AddCommMonoidWithOne R] → AddMonoidWithOne R

## BASE-LIBRARY REF NonAssocSemiring.toAddCommMonoidWithOne
{α : Type u} → [self : NonAssocSemiring α] → AddCommMonoidWithOne α

## BASE-LIBRARY REF Finset.card
{α : Type u_1} → Finset α → ℕ

Docstring: `s.card` is the number of elements of `s`, aka its cardinality.

The notation `#s` can be accessed in the `Finset` locale. 

## BASE-LIBRARY REF Nat.Partition
ℕ → Type

Docstring: A partition of `n` is a multiset of positive integers summing to `n`. 

## BASE-LIBRARY REF Nat.Partition.restricted
(n : ℕ) → (p : ℕ → Prop) → [DecidablePred p] → Finset n.Partition

Docstring: The finset of those partitions in which every part satisfies a certain condition. 

## INFORMAL STATEMENT
thm.pars.main-gf-parts-I

Let $I$ be a subset of $\left\{  1,2,3,\ldots \right\}  $. For each $n\in \mathbb {N}$, let $p_{I}\left( n\right) $ be the \#  of partitions $\lambda $ of $n$ such that all parts of $\lambda $ belong to $I$. Then, 

\[  \sum _{n\in \mathbb {N}}p_{I}\left( n\right) x^{n}=\prod _{k\in I}\frac{1}{1-x^{k}}.  \]

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.fps.comps
def.fps.comps

\textbf{(a)} An \emph{(integer) composition} means a (finite) tuple of positive integers. \medskip 

\textbf{(b)} The \emph{size} of an integer composition $\alpha =\left( \alpha _{1},\alpha _{2},\ldots ,\alpha _{m}\right) $ is defined to be the integer $\alpha _{1}+\alpha _{2}+\cdots +\alpha _{m}$. It is written $\left\vert \alpha \right\vert $. \medskip 

\textbf{(c)} The \emph{length} of an integer composition $\alpha =\left( \alpha _{1},\alpha _{2},\ldots ,\alpha _{m}\right) $ is defined to be the integer $m$. It is written $\ell \left( \alpha \right) $. \medskip 

\textbf{(d)} Let $n\in \mathbb {N}$. A \emph{composition of }$n$ means a composition whose size is $n$. \medskip 

\textbf{(e)} Let $n\in \mathbb {N}$ and $k\in \mathbb {N}$. A \emph{composition of }$n$\emph{ into }$k$\emph{ parts} is a composition whose size is $n$ and whose length is $k$.

## INFORMAL DEFINITION stmt-algebraic-combinatorics-def.pars.parts
def.pars.parts

\textbf{(a)} An \emph{(integer) partition} means a (finite) weakly decreasing tuple of positive integers – i.e., a finite tuple $\left( \lambda _{1},\lambda _{2},\ldots ,\lambda _{m}\right) $ of positive integers such that $\lambda _{1}\geq \lambda _{2}\geq \cdots \geq \lambda _{m}$. 

Thus, partitions are the same as weakly decreasing compositions. Hence, the notions of \emph{size} and \emph{length} of a partition are automatically defined, since we have defined them for compositions (in Definition \ref{def.fps.comps}). \medskip 

\textbf{(b)} The \emph{parts} of a partition $\left( \lambda _{1},\lambda _{2},\ldots ,\lambda _{m}\right) $ are simply its entries $\lambda _{1},\lambda _{2},\ldots ,\lambda _{m}$. \medskip 

\textbf{(c)} Let $n\in \mathbb {Z}$. A \emph{partition of }$n$ means a partition whose size is $n$. \medskip 

\textbf{(d)} Let $n\in \mathbb {Z}$ and $k\in \mathbb {N}$. A \emph{partition of }$n$\emph{ into }$k$\emph{ parts} is a partition whose size is $n$ and whose length is $k$.

## VERDICT
{
  "verdict": "faithful",
  "justification": "The informal statement assumes \u201cI be a subset of {1,2,3,\u2026}\u201d and counts partitions whose parts belong to I. The formal dependency defines `partsInCount I n` as `(Nat.Partition.restricted n fun x => x \u2208 I).card`, and `Nat.Partition.restricted` selects exactly those partitions for which every part satisfies membership in `I`, so the coefficients agree with `p_I(n)`. The target\u2019s factor at index `k` is conditional on `k + 1 \u2208 I` and is `\u2211' j, X ^ ((k + 1) * j)`, exactly the geometric-series factor for the positive part `k+1`; indices not in I contribute `1`. Thus `HasProd ... (PowerSeries.mk fun n => \u2191(partsInCount I n))` expresses the stated product as the generating series. Although the formal binder is `(I : Set \u2115)` rather than restricting I to positive naturals, this is a harmless generalization: the shifted product only tests positive numbers `k+1`, and partition parts are positive, so membership of `0` affects neither side. The binders `[DecidablePred fun x => x \u2208 I]` and `[TopologicalSpace R] [T2Space R] [IsTopologicalSemiring R]` supply decidability and the convergence setting needed for `ite`, `tsum`, and `HasProd`; they encode the formal realization of the infinite formal-power-series product rather than changing the combinatorial identity. Quantification over every suitable commutative semiring `R` is also a generalization of the coefficient identity."
}